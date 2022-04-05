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


#### find the pid of what you want to check ...
```

ubuntu@ip-10-1-1-52:~$ ps aux | grep nginx
root     2584204  0.0  0.5  10656  5796 ?        Ss   15:02   0:00 nginx: master process nginx -g daemon off;
systemd+ 2584258  0.0  0.2  11060  2576 ?        S    15:02   0:00 nginx: worker process
ubuntu   2606061  0.0  0.0   8168   660 pts/1    S+   15:40   0:00 grep --color=auto nginx
ubuntu@ip-10-1-1-52:~$```


### Now you can find the netns of pid to check 
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o netns,cmd,pid | grep 2584204
4026532300 nginx: master process nginx -g daemon off;
4026532300 nginx: worker process
4026532040 grep --color=auto nginx
ubuntu@ip-10-1-1-52:~$

```
### Now let's create a container that share the the nginx namespace
```
docker run -it  --net=container:126286cced08 xxradar/hackon
```

### Now we know the netns and we can find everything that shares it ...
```
ubuntu@ip-10-1-1-52:~$ sudo ps -ax -n -o netns,cmd,pid | grep 4026532300
4026532300 nginx: master process nginx 2584204
4026532300 nginx: worker process       2584258
4026532300 /bin/bash                   2604631
ubuntu@ip-10-1-1-52:~$
```
```
ubuntu@ip-10-1-1-52:~$ sudo lsns
        NS TYPE   NPROCS     PID USER             COMMAND
4026531835 cgroup    127       1 root             /lib/systemd/systemd --system --deserialize 32
4026531836 pid       124       1 root             /lib/systemd/systemd --system --deserialize 32
4026531837 user      126       1 root             /lib/systemd/systemd --system --deserialize 32
4026531838 uts       121       1 root             /lib/systemd/systemd --system --deserialize 32
4026531839 ipc       124       1 root             /lib/systemd/systemd --system --deserialize 32
4026531840 mnt       117       1 root             /lib/systemd/systemd --system --deserialize 32
4026531860 mnt         1      17 root             kdevtmpfs
4026532040 net       123       1 root             /lib/systemd/systemd --system --deserialize 32
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
4026532300 net         3 2584204 root             nginx: master process nginx -g daemon off;
4026532343 uts         1     451 root             /lib/systemd/systemd-logind
4026532355 mnt         1 2610803 root             /bin/bash
4026532356 uts         1 2610803 root             /bin/bash
4026532357 ipc         1 2610803 root             /bin/bash
4026532358 pid         1 2610803 root             /bin/bash
ubuntu@ip-10-1-1-52:~$
```
