## What about kubernetes?

#### Let’s create a pod.
```
$ kubectl run --image nginx www-demo
pod/www-demo created$ kubectl get po -o wide
NAME                       READY   STATUS    RESTARTS       AGE   IP           NODE           NOMINATED NODE   READINESS GATES
www-demo                   1/1     Running   0              44s   10.0.1.207   ip-10-1-2-40   <none>           <none>
```
On the correct node, we can find the nginx process
```
$ ps aux | grep -i nginx
root      6229  0.0  0.0   9092  6548 ?        Ss   16:07   0:00 nginx: master process nginx -g daemon off;$ sudo ps -ax -n -o pid,netns,utsns,ipcns,mntns,pidns,cmd | \
grep 6229
 6229 4026532927 4026532396 4026532397 4026532456 4026532457 nginx: master process nginx -g daemon off;$ sudo ps -ax -n -o pid,netns,utsns,ipcns,mntns,pidns,cmd | \
grep 4026532927
 4759 4026532927 4026532396 4026532397 4026532395 4026532398 /pause
 6229 4026532927 4026532396 4026532397 4026532456 4026532457 nginx: master process nginx -g daemon off;
 6778 4026532927 4026532396 4026532397 4026532456 4026532457 nginx: worker process
```
We now found all the processes that share the netns, but what we see is even more interesting. We found the /pause container. It’s a container which holds the network netns, utsns and ipcns namespace for the pod. Kubernetes creates the `/pause` containers to acquire for example the respective pod’s IP address and share it with all other containers that join that pod.

#### Could we modify the content of the www-demo ?
```
$ sudo nsenter --target 6229 --mount --uts --ipc --net --pid
root@www-demo-8c4d7cc75-vfh9d:/# echo  /
"Hacking" >/usr/share/nginx/html/hacking.html$ exit$ kubectl run -it --rm --image xxradar/hackon debug
root@debug:/# curl 10.0.1.207/hacking.html
Hacking
...
```
#### Crictl magic

```
$ sudo crictl list

$ sudo crictl inspect e6120476c6999 | jq -r .info.pid
5333

$ sudo ps -ax -o pid,netns,cmd | grep -i 5333
 5333 4026532876 node ./index.js

$ sudo ps -ax -o pid,netns,cmd | grep -i 4026532876
 4870 4026532876 /pause
 5333 4026532876 node ./index.js
$
````
