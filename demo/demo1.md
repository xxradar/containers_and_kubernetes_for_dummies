## Container basics 

#### Lets create a container ...
```
ubuntu@ip-10-1-1-52:~$ docker run -d --name wwwdemo nginx
126286cced081dbd56a1518a8f091ce362c2f19cb09b9cc463d507dc89a88a27
ubuntu@ip-10-1-1-52:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
126286cced08   nginx     "/docker-entrypoint.…"   7 seconds ago   Up 6 seconds   80/tcp    wwwdemo
ubuntu@ip-10-1-1-52:~$
```

```
ubuntu@ip-10-1-1-52:~$ ps aux | grep -i nginx
root     2584204  0.0  0.5  10656  5796 ?        Ss   15:02   0:00 nginx: master process nginx -g daemon off;
systemd+ 2584258  0.0  0.2  11060  2576 ?        S    15:02   0:00 nginx: worker process
ubuntu   2585516  0.0  0.0   8164   724 pts/1    S+   15:05   0:00 grep --color=auto -i nginx
ubuntu@ip-10-1-1-52:~$
```
#### you can find namespace information using`lsns`
```
ubuntu@ip-10-1-1-52:/$ sudo lsns
        NS TYPE   NPROCS     PID USER             COMMAND
4026531835 cgroup    120       1 root             /lib/systemd/systemd --system --deserialize 32
4026531836 pid       118       1 root             /lib/systemd/systemd --system --deserialize 32
4026531837 user      119       1 root             /lib/systemd/systemd --system --deserialize 32
4026531838 uts       115       1 root             /lib/systemd/systemd --system --deserialize 32
4026531839 ipc       118       1 root             /lib/systemd/systemd --system --deserialize 32
4026531840 mnt       111       1 root             /lib/systemd/systemd --system --deserialize 32
4026531860 mnt         1      17 root             kdevtmpfs
4026532040 net       117       1 root             /lib/systemd/systemd --system --deserialize 32
4026532222 mnt         1  404352 root             /lib/systemd/systemd-udevd
4026532223 uts         1  404352 root             /lib/systemd/systemd-udevd
4026532225 mnt         1  403375 systemd-timesync /lib/systemd/systemd-timesyncd
4026532226 uts         1  403375 systemd-timesync /lib/systemd/systemd-timesyncd
4026532227 mnt         1  403272 systemd-network  /lib/systemd/systemd-networkd
4026532228 mnt         1  403277 systemd-resolve  /lib/systemd/systemd-resolved
4026532234 net         1  823830 uuidd            /usr/sbin/uuidd --socket-activation
4026532284 mnt         1     451 root             /lib/systemd/systemd-logind
4026532291 mnt         1  823830 uuidd            /usr/sbin/uuidd --socket-activation
4026532292 user        1  823830 uuidd            /usr/sbin/uuidd --socket-activation
4026532295 mnt         2 2584204 root             nginx: master process nginx -g daemon off;
4026532296 uts         2 2584204 root             nginx: master process nginx -g daemon off;
4026532297 ipc         2 2584204 root             nginx: master process nginx -g daemon off;
4026532298 pid         2 2584204 root             nginx: master process nginx -g daemon off;
4026532300 net         2 2584204 root             nginx: master process nginx -g daemon off;
4026532343 uts         1     451 root             /lib/systemd/systemd-logind
ubuntu@ip-10-1-1-52:/$

```

#### Now create a new container
```
docker run -it  xxradar/hackon
```
```
ubuntu@ip-10-1-1-52:~$ sudo lsns
        NS TYPE   NPROCS     PID USER             COMMAND
4026531835 cgroup    128       1 root             /lib/systemd/systemd --system --deserialize 32
4026531836 pid       125       1 root             /lib/systemd/systemd --system --deserialize 32
4026531837 user      127       1 root             /lib/systemd/systemd --system --deserialize 32
4026531838 uts       122       1 root             /lib/systemd/systemd --system --deserialize 32
4026531839 ipc       125       1 root             /lib/systemd/systemd --system --deserialize 32
4026531840 mnt       118       1 root             /lib/systemd/systemd --system --deserialize 32
4026531860 mnt         1      17 root             kdevtmpfs
4026532040 net       124       1 root             /lib/systemd/systemd --system --deserialize 32
4026532222 mnt         1  404352 root             /lib/systemd/systemd-udevd
4026532223 uts         1  404352 root             /lib/systemd/systemd-udevd
4026532225 mnt         1  403375 systemd-timesync /lib/systemd/systemd-timesyncd
4026532226 uts         1  403375 systemd-timesync /lib/systemd/systemd-timesyncd
4026532227 mnt         1  403272 systemd-network  /lib/systemd/systemd-networkd
4026532228 mnt         1  403277 systemd-resolve  /lib/systemd/systemd-resolved
4026532234 net         1  823830 uuidd            /usr/sbin/uuidd --socket-activation
4026532284 mnt         1     451 root             /lib/systemd/systemd-logind
4026532291 mnt         1  823830 uuidd            /usr/sbin/uuidd --socket-activation
4026532292 user        1  823830 uuidd            /usr/sbin/uuidd --socket-activation
4026532295 mnt         2 2584204 root             nginx: master process nginx -g daemon off;
4026532296 uts         2 2584204 root             nginx: master process nginx -g daemon off;
4026532297 ipc         2 2584204 root             nginx: master process nginx -g daemon off;
4026532298 pid         2 2584204 root             nginx: master process nginx -g daemon off;
4026532300 net         2 2584204 root             nginx: master process nginx -g daemon off;
4026532343 uts         1     451 root             /lib/systemd/systemd-logind
4026532357 mnt         1 2611797 root             /bin/bash
4026532358 uts         1 2611797 root             /bin/bash
4026532359 ipc         1 2611797 root             /bin/bash
4026532360 pid         1 2611797 root             /bin/bash
4026532362 net         1 2611797 root             /bin/bash
ubuntu@ip-10-1-1-52:~$
```
As you can see, the new container is a process in an new mnt, uts, ipc, pid and net namespace. <br>
`lsns` is only showing basic info. So let's see to get at the bottom of this.


####  First find the pid and namespace of what you want to check ...
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o pid,netns,cmd | grep nginx
2584204 4026532300 nginx: master process nginx -g daemon off;
2584258 4026532300 nginx: worker process
2639111 4026532040 grep --color=auto nginx
```
We can see that the `nginx: master` and `nginx: worker` process are sharing the same network namespace


#### Now filter on the network namespace and find all processes that share the network namespace
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o pid,netns,cmd | grep 4026532300
2584204 4026532300 nginx: master process nginx -g daemon off;
2584258 4026532300 nginx: worker process
2641178 4026532040 grep --color=auto 4026532300
ubuntu@ip-10-1-1-52:~$
```
Note: You can find other namespaces also
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o pid,netns,utsns,ipcns,mntns,pidns,cmd | grep 4026532300
2584204 4026532300 4026532296 4026532297 4026532295 4026532298 nginx: master process nginx -g daemon off;
2584258 4026532300 4026532296 4026532297 4026532295 4026532298 nginx: worker process
2649322 4026532040 4026531838 4026531839 4026531840 4026531836 grep --color=auto 4026532300
ubuntu@ip-10-1-1-52:~$
```

#### Now let's create a container that share the the nginx namespace
You can do this via `--net=container:<containerid>`
```
docker run -it  --net=container:126286cced08 xxradar/hackon
```
Note: Inside this container, you can find the network namespace identifier
```
root@126286cced08:/# ps -ax -n -o pid,netns,cmd
    PID      NETNS CMD
      1 4026532300 /bin/bash
     11 4026532300 ps -ax -n -o pid,netns,cmd
root@126286cced08:/#
```


#### Let's check the processes that share the namespace ...
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o pid,netns,cmd | grep 4026532300
2584204 4026532300 nginx: master process nginx -g daemon off;
2584258 4026532300 nginx: worker process
2642881 4026532300 /bin/bash
2643312 4026532040 grep --color=auto 4026532300
ubuntu@ip-10-1-1-52:~$
```

