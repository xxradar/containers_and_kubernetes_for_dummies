## Container basics 
#### Checking kernel versions
Check the kernel version of the host
```
ubuntu@ip-10-1-1-52:~$ uname -r
5.11.0-1020-aws
ubuntu@ip-10-1-1-52:~$
```
Check the kernel version inside the container
```
ubuntu@ip-10-1-1-52:~$ docker run -it xxradar/hackon
root@fccf362838ae:/# uname -r
5.11.0-1020-aws
root@fccf362838ae:/# exit
exit
ubuntu@ip-10-1-1-52:~$
```

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
#### You can find namespace information using `lsns`
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

### Now create a new container
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


#### Now filter on the network namespace and find all processes that shares the network namespace
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

### Now let's create a container that share the network namespace
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

### Sharing the process namespace
```
ubuntu@ip-10-1-1-52:~$ docker run -it  --pid=host xxradar/hackon
root@b41d22f63525:/# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  1.0 168752 10404 ?        Ss    2021  48:24 /lib/systemd/systemd --system --deserialize 32
root           2  0.0  0.0      0     0 ?        S     2021   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<    2021   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<    2021   0:00 [rcu_par_gp]
root           6  0.0  0.0      0     0 ?        I<    2021   0:00 [kworker/0:0H-events_highpri]
root           9  0.0  0.0      0     0 ?        I<    2021   0:00 [mm_percpu_wq]
root          10  0.0  0.0      0     0 ?        S     2021   0:00 [rcu_tasks_rude_]
root          11  0.0  0.0      0     0 ?        S     2021   0:00 [rcu_tasks_trace]
root          12  0.0  0.0      0     0 ?        S     2021  25:08 [ksoftirqd/0]
root          13  0.0  0.0      0     0 ?        I     2021  10:10 [rcu_sched]
root          14  0.0  0.0      0     0 ?        S     2021   1:28 [migration/0]
root          15  0.0  0.0      0     0 ?        S     2021   0:00 [idle_inject/0]
root          16  0.0  0.0      0     0 ?        S     2021   0:00 [cpuhp/0]
root          17  0.0  0.0      0     0 ?        S     2021   0:00 [kdevtmpfs]
root          18  0.0  0.0      0     0 ?        I<    2021   0:00 [netns]
root          19  0.0  0.0      0     0 ?        I<    2021   0:00 [inet_frag_wq]
root          20  0.0  0.0      0     0 ?        S     2021   0:00 [kauditd]
root          21  0.0  0.0      0     0 ?        S     2021   0:12 [khungtaskd]
root          22  0.0  0.0      0     0 ?        S     2021   0:00 [oom_reaper]
root          23  0.0  0.0      0     0 ?        I<    2021   0:00 [writeback]
root          24  0.0  0.0      0     0 ?        S     2021   7:36 [kcompactd0]
root          25  0.0  0.0      0     0 ?        SN    2021   0:00 [ksmd]
root          26  0.0  0.0      0     0 ?        SN    2021   0:20 [khugepaged]
root          72  0.0  0.0      0     0 ?        I<    2021   0:00 [kintegrityd]
root          73  0.0  0.0      0     0 ?        I<    2021   0:00 [kblockd]
root          74  0.0  0.0      0     0 ?        I<    2021   0:00 [blkcg_punt_bio]
root          75  0.0  0.0      0     0 ?        I<    2021   0:00 [tpm_dev_wq]
root          76  0.0  0.0      0     0 ?        I<    2021   0:00 [ata_sff]
root          77  0.0  0.0      0     0 ?        I<    2021   0:00 [md]
root          78  0.0  0.0      0     0 ?        I<    2021   0:00 [edac-poller]
root          79  0.0  0.0      0     0 ?        I<    2021   0:00 [devfreq_wq]
root          80  0.0  0.0      0     0 ?        S     2021   0:00 [watchdogd]
root          82  0.0  0.0      0     0 ?        I<    2021   0:29 [kworker/0:1H-kblockd]
root          84  0.0  0.0      0     0 ?        S     2021   0:47 [kswapd0]
root          85  0.0  0.0      0     0 ?        S     2021   0:00 [ecryptfs-kthrea]
root          87  0.0  0.0      0     0 ?        I<    2021   0:00 [kthrotld]
root          88  0.0  0.0      0     0 ?        I<    2021   0:00 [acpi_thermal_pm]
...
root     2604849  0.0  0.9  13800  9068 ?        Ss   15:37   0:00 sshd: ubuntu [priv]
1000     2604926  0.0  0.5  13932  5272 ?        S    15:38   0:00 sshd: ubuntu@pts/1
1000     2604927  0.0  0.5  10172  5100 ?        Ss+  15:38   0:00 -bash
root     2640798  0.0  0.0      0     0 ?        I    16:36   0:00 [kworker/u30:2-ext4-rsv-conversion]
root     2651221  0.0  0.0      0     0 ?        I    16:53   0:00 [kworker/u30:1-events_unbound]
root     2651272  0.0  0.0      0     0 ?        I    16:54   0:00 [kworker/0:1-events]
root     2655153  0.0  0.0      0     0 ?        I    17:00   0:00 [kworker/u30:0-events_power_efficient]
root     2655424  0.0  0.0      0     0 ?        I    17:00   0:00 [kworker/0:0-events]
1000     2655568  0.8  4.8 1201596 48532 ?       Sl+  17:00   0:00 docker run -it --pid=host xxradar/hackon
root     2655589  0.4  0.8 711280  8136 ?        Sl   17:00   0:00 /usr/bin/containerd-shim-runc-v2 -namespace moby -id b41d22f635253056c39c89fcd49d197a616b6b2a188e8f14a83adee636f4774c -address /run/containerd/container
root     2655611  0.6  0.3   4116  3356 pts/0    Ss   17:00   0:00 /bin/bash
root     2655728  0.0  0.2   5888  2792 pts/0    R+   17:00   0:00 ps aux
root     2662138  0.0  0.0      0     0 ?        S<   Mar11   0:00 [loop5]
root     3139386  0.0  0.4 236320  4460 ?        Ssl  Mar01   0:00 /usr/lib/policykit-1/polkitd --no-debug
root     3404358  0.0  0.0      0     0 ?        S<   Feb24   0:00 [loop6]
root     3587899  0.0  0.0      0     0 ?        S<   Mar17   0:00 [loop8]
root@b41d22f63525:/#
```
Inside the container ...
```
root@b41d22f63525:/# ps -ax -n -o pid,netns,utsns,ipcns,mntns,pidns,cmd | grep -i bash
2592665          -          -          -          -          - -bash
2604927          -          -          -          -          - -bash
2655611 4026532361 4026532358 4026532359 4026532357 4026531836 /bin/bash
2657728 4026532361 4026532358 4026532359 4026532357 4026531836 grep --color=auto -i bash
root@b41d22f63525:/#
```
On the host ...
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o pid,netns,utsns,ipcns,mntns,pidns,cmd | grep 4026531836
      1 4026532040 4026531838 4026531839 4026531840 4026531836 /lib/systemd/systemd --system --deserialize 32
      2 4026532040 4026531838 4026531839 4026531840 4026531836 [kthreadd]
      3 4026532040 4026531838 4026531839 4026531840 4026531836 [rcu_gp]
      4 4026532040 4026531838 4026531839 4026531840 4026531836 [rcu_par_gp]
      6 4026532040 4026531838 4026531839 4026531840 4026531836 [kworker/0:0H-events_highpri]
      9 4026532040 4026531838 4026531839 4026531840 4026531836 [mm_percpu_wq]
     10 4026532040 4026531838 4026531839 4026531840 4026531836 [rcu_tasks_rude_]
     11 4026532040 4026531838 4026531839 4026531840 4026531836 [rcu_tasks_trace]
     12 4026532040 4026531838 4026531839 4026531840 4026531836 [ksoftirqd/0]
     13 4026532040 4026531838 4026531839 4026531840 4026531836 [rcu_sched]
     14 4026532040 4026531838 4026531839 4026531840 4026531836 [migration/0]
...
```
#### Hacking at full speed
A cleaner way to find the processID PID
```
ubuntu@ip-10-1-1-52:~$ PID=$(sudo docker inspect --format '{{.State.Pid}}' wwwdemo)
ubuntu@ip-10-1-1-52:~$ echo $PID
2584204
ubuntu@ip-10-1-1-52:~$
```
Now we can try to `enter` the container namespaces ...
```
ubuntu@ip-10-1-1-52:~$ PID=$(sudo docker inspect --format '{{.State.Pid}}' wwwdemo)
ubuntu@ip-10-1-1-52:~$ echo $PID
2584204
```
```
ubuntu@ip-10-1-1-52:~$ sudo nsenter --target $PID --mount --uts --ipc --net --pid
root@126286cced08:/# cat /etc/hostname
126286cced08
root@126286cced08:/# uname -a
Linux 126286cced08 5.11.0-1020-aws #21~20.04.2-Ubuntu SMP Fri Oct 1 13:03:59 UTC 2021 x86_64 GNU/Linux
root@126286cced08:/# cat /etc/nginx/conf.d/default.conf
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
root@126286cced08:/# echo  "Hacking" >/usr/share/nginx/html/hacking.html
root@126286cced08:/#
```
From another container ...
```
root@a813420e05c5:/# curl 172.17.0.2/hacking.html
Hacking
root@a813420e05c5:/#
```
Or from the host (you can run any tool installed on the host inside the container !! )
```
ubuntu@ip-10-1-1-52:~$ sudo nsenter -t $PID -n ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
24: eth0@if25: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
ubuntu@ip-10-1-1-52:~$
```
