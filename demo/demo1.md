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

#### Sharing the process ns
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
root          89  0.0  0.0      0     0 ?        S     2021   0:00 [xenbus]
root          90  0.0  0.0      0     0 ?        S     2021   0:00 [xenwatch]
root          91  0.0  0.0      0     0 ?        I<    2021   0:00 [nvme-wq]
root          92  0.0  0.0      0     0 ?        I<    2021   0:00 [nvme-reset-wq]
root          93  0.0  0.0      0     0 ?        I<    2021   0:00 [nvme-delete-wq]
root          94  0.0  0.0      0     0 ?        S     2021   0:00 [scsi_eh_0]
root          95  0.0  0.0      0     0 ?        I<    2021   0:00 [scsi_tmf_0]
root          96  0.0  0.0      0     0 ?        S     2021   0:00 [scsi_eh_1]
root          97  0.0  0.0      0     0 ?        I<    2021   0:00 [scsi_tmf_1]
root          99  0.0  0.0      0     0 ?        I<    2021   0:00 [vfio-irqfd-clea]
root         100  0.0  0.0      0     0 ?        I<    2021   0:00 [ipv6_addrconf]
root         109  0.0  0.0      0     0 ?        I<    2021   0:00 [kstrp]
root         112  0.0  0.0      0     0 ?        I<    2021   0:00 [zswap-shrink]
root         113  0.0  0.0      0     0 ?        I<    2021   0:00 [kworker/u31:0]
root         118  0.0  0.0      0     0 ?        I<    2021   0:00 [charger_manager]
root         119  0.0  0.0      0     0 ?        S     2021   0:36 [jbd2/xvda1-8]
root         120  0.0  0.0      0     0 ?        I<    2021   0:00 [ext4-rsv-conver]
root         203  0.0  0.0      0     0 ?        I<    2021   0:00 [cryptd]
root         259  0.0  0.0      0     0 ?        I<    2021   0:00 [kaluad]
root         260  0.0  0.0      0     0 ?        I<    2021   0:00 [kmpath_rdacd]
root         261  0.0  0.0      0     0 ?        I<    2021   0:00 [kmpathd]
root         262  0.0  0.0      0     0 ?        I<    2021   0:00 [kmpath_handlerd]
root         263  0.0  1.8 280208 17996 ?        SLsl  2021  17:26 /sbin/multipathd -d -s
root         273  0.0  0.0      0     0 ?        S<    2021   0:00 [loop1]
root         424  0.0  0.0   2548   740 ?        Ss    2021   0:00 /usr/sbin/acpid
root         432  0.0  0.2   8544  2388 ?        Ss    2021   0:20 /usr/sbin/cron -f
103          434  0.0  0.3   7920  3576 ?        Ss    2021   0:12 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
root         445  0.0  1.3  29540 13312 ?        Ss    2021   0:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
104          447  0.0  0.3 224508  3468 ?        Ssl   2021   0:26 /usr/sbin/rsyslogd -n -iNONE
root         451  0.0  0.5  17760  5516 ?        Ss    2021   0:17 /lib/systemd/systemd-logind
daemon       455  0.0  0.2   3800  2024 ?        Ss    2021   0:00 /usr/sbin/atd -f
root         456  0.0  2.4 1345452 24812 ?       Ssl   2021  81:37 /usr/bin/containerd
root         477  0.0  0.1   7360  1748 ?        Ss+   2021   0:00 /sbin/agetty -o -p -- \u --keep-baud 115200,38400,9600 ttyS0 vt220
root         482  0.0  0.1   5836  1480 ?        Ss+   2021   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
root         542  0.0  1.0 108116 10944 ?        Ssl   2021   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         575  0.0  5.1 1393068 51036 ?       Ssl   2021  22:13 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
root         627  0.0  0.4  12184  4000 ?        Ss    2021   1:53 sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand /usr/share/ec2-instance-connect/eic_run_authorized_keys %u %f -o AuthorizedKeysCommandUser ec2-instance
root         655  0.0  0.0   2496   592 ?        S     2021   0:00 bpfilter_umh
1000        2196  0.0  0.6  18512  6272 ?        Ss    2021   0:01 /lib/systemd/systemd --user
1000        2197  0.0  0.4 104296  4404 ?        S     2021   0:00 (sd-pam)
root        3967  0.0  0.2  82956  2780 ?        Ss    2021   0:00 gpg-agent --homedir /root/.gnupg --use-standard-socket --daemon
1000        4154  0.0  0.2  82956  2808 ?        SLs   2021   0:05 /usr/bin/gpg-agent --supervised
root       14596  0.0  0.0      0     0 ?        I<    2021   0:00 [xfsalloc]
root       14597  0.0  0.0      0     0 ?        I<    2021   0:00 [xfs_mru_cache]
root       61943  0.0  0.5 242016  5616 ?        Ssl   2021   5:01 /usr/lib/accountsservice/accounts-daemon
root      389789  0.0  0.0      0     0 ?        S<   Jan12   0:00 [loop12]
_apt      403272  0.0  0.3  26752  3896 ?        Ss   Jan14   0:40 /lib/systemd/systemd-networkd
tcpdump   403277  0.0  0.7  24040  7300 ?        Ss   Jan14   0:22 /lib/systemd/systemd-resolved
root      403282  0.0  4.9 244232 49232 ?        S<s  Jan14   1:38 /lib/systemd/systemd-journald
102       403375  0.0  0.2  90240  2432 ?        Ssl  Jan14   0:08 /lib/systemd/systemd-timesyncd
root      404352  0.0  0.4  18872  4460 ?        Ss   Jan14   0:07 /lib/systemd/systemd-udevd
root      445014  0.0  0.0      0     0 ?        S<   Jan19   0:00 [loop3]
1000      445060  0.0  0.2   7264  2560 ?        Ss   Jan19   0:00 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
1000      464368  0.0  2.8 946736 28604 ?        Sl   Jan20  17:22 .terraform/providers/registry.terraform.io/hashicorp/aws/3.70.0/linux_amd64/terraform-provider-aws_v3.70.0_x5
root      511934  0.0  0.2  20892  2116 ?        Sl   Feb10   0:00 /opt/forticlient/fmon -s /opt/forticlient/vir_sig/ -o /opt/forticlient/ --unit /opt/forticlient/ -a
root      511935  0.0  0.2  11620  2088 ?        S    Feb10   0:00 /opt/forticlient//scanunit -p 60545 -s /opt/forticlient/vir_sig/ -a
1000      639543  0.0  0.2   3800  2040 ?        S    Feb05  65:12 /opt/forticlient/fortitraylauncher
root      639612  0.9  1.2 10029772 12812 ?      Ssl  Feb05 798:20 /opt/forticlient/fctsched
107       823830  0.0  0.0   9756   344 ?        Ss   Feb11   0:00 /usr/sbin/uuidd --socket-activation
root     1233694  0.0  0.0      0     0 ?        S<   Mar29   0:00 [loop9]
root     1514613  0.0  0.0      0     0 ?        S<   Feb21   0:00 [loop11]
root     1514907  0.0  0.6 1235064 6960 ?        Ssl  Feb21   2:32 /snap/amazon-ssm-agent/5163/amazon-ssm-agent
root     1515006  0.0  1.2 1247272 12856 ?       Sl   Feb21   1:47 /snap/amazon-ssm-agent/5163/ssm-agent-worker
root     1576021  0.0  0.0      0     0 ?        S<   Mar15   0:00 [loop2]
root     1899836  0.0  0.0      0     0 ?        S<   Mar25   0:00 [loop4]
root     2462539  0.0  0.0      0     0 ?        S<   11:39   0:00 [loop0]
root     2462598  0.0  4.0 726736 40440 ?        Ssl  11:39   0:02 /usr/lib/snapd/snapd
root     2549116  0.0  0.0      0     0 ?        I    14:02   0:00 [kworker/0:2-cgroup_pidlist_destroy]
root     2584183  0.0  0.9 711920  9632 ?        Sl   15:02   0:01 /usr/bin/containerd-shim-runc-v2 -namespace moby -id 126286cced081dbd56a1518a8f091ce362c2f19cb09b9cc463d507dc89a88a27 -address /run/containerd/container
root     2584204  0.0  0.5  10656  5796 ?        Ss   15:02   0:00 nginx: master process nginx -g daemon off;
tcpdump  2584258  0.0  0.2  11060  2576 ?        S    15:02   0:00 nginx: worker process
root     2592576  0.0  0.9  13800  9060 ?        Ss   15:17   0:00 sshd: ubuntu [priv]
1000     2592664  0.0  0.5  13932  5932 ?        S    15:17   0:00 sshd: ubuntu@pts/2
1000     2592665  0.0  0.5  10172  5176 ?        Ss   15:17   0:00 -bash
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
Inside the container
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

