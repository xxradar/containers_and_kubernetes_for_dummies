## Creating a container image
```
 curl https://raw.githubusercontent.com/xxradar/TLSSAN_scanner/master/tlssan_scan.sh >tlssan_scan.sh
```
```
cat <<EOF >Dockerfile
FROM ubuntu:latest
MAINTAINER xxradar xxadar@radarhack.com
RUN apt-get update && apt-get install -y openssl
RUN apt-get -y install ca-certificates
WORKDIR /scripts
COPY tlssan_scan.sh tlssan_scan.sh
ENTRYPOINT ["/scripts/tlssan_scan.sh"]
EOF
```

```
ubuntu@ip-10-1-1-52:~/test$ docker build --no-cache -t tls_scan  .
Sending build context to Docker daemon   5.12kB
Step 1/8 : FROM ubuntu:latest
 ---> ff0fea8310f3
Step 2/8 : MAINTAINER xxradar xxadar@radarhack.com
 ---> Running in a1be1236b2bd
Removing intermediate container a1be1236b2bd
 ---> 456be680e5ac
Step 3/8 : RUN apt-get update && apt-get install -y openssl
 ---> Running in 85644ce80cd3
Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:5 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [1100 kB]
Get:6 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1726 kB]
Get:7 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [864 kB]
Get:8 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [25.8 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/universe amd64 Packages [11.3 MB]
Get:10 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [177 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal/restricted amd64 Packages [33.4 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal/main amd64 Packages [1275 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [1150 kB]
Get:14 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [2142 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [1174 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 Packages [30.3 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [51.2 kB]
Get:18 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [26.0 kB]
Fetched 21.7 MB in 2s (9933 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  libssl1.1
Suggested packages:
  ca-certificates
The following NEW packages will be installed:
  libssl1.1 openssl
0 upgraded, 2 newly installed, 0 to remove and 1 not upgraded.
Need to get 1942 kB of archives.
After this operation, 5412 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libssl1.1 amd64 1.1.1f-1ubuntu2.12 [1322 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 openssl amd64 1.1.1f-1ubuntu2.12 [620 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 1942 kB in 1s (2414 kB/s)
Selecting previously unselected package libssl1.1:amd64.
(Reading database ... 4127 files and directories currently installed.)
Preparing to unpack .../libssl1.1_1.1.1f-1ubuntu2.12_amd64.deb ...
Unpacking libssl1.1:amd64 (1.1.1f-1ubuntu2.12) ...
Selecting previously unselected package openssl.
Preparing to unpack .../openssl_1.1.1f-1ubuntu2.12_amd64.deb ...
Unpacking openssl (1.1.1f-1ubuntu2.12) ...
Setting up libssl1.1:amd64 (1.1.1f-1ubuntu2.12) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.30.0 /usr/local/share/perl/5.30.0 /usr/lib/x86_64-linux-gnu/perl5/5.30 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.30 /usr/share/perl/5.30 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up openssl (1.1.1f-1ubuntu2.12) ...
Processing triggers for libc-bin (2.31-0ubuntu9.7) ...
Removing intermediate container 85644ce80cd3
 ---> 83ce8f33037c
Step 4/8 : RUN apt-get -y install ca-certificates
 ---> Running in 8caf393f6ff8
Reading package lists...
Building dependency tree...
Reading state information...
The following NEW packages will be installed:
  ca-certificates
0 upgraded, 1 newly installed, 0 to remove and 1 not upgraded.
Need to get 145 kB of archives.
After this operation, 389 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 ca-certificates all 20210119~20.04.2 [145 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 145 kB in 0s (340 kB/s)
Selecting previously unselected package ca-certificates.
(Reading database ... 4289 files and directories currently installed.)
Preparing to unpack .../ca-certificates_20210119~20.04.2_all.deb ...
Unpacking ca-certificates (20210119~20.04.2) ...
Setting up ca-certificates (20210119~20.04.2) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.30.0 /usr/local/share/perl/5.30.0 /usr/lib/x86_64-linux-gnu/perl5/5.30 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.30 /usr/share/perl/5.30 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Updating certificates in /etc/ssl/certs...
128 added, 0 removed; done.
Processing triggers for ca-certificates (20210119~20.04.2) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
Removing intermediate container 8caf393f6ff8
 ---> 49886a54c590
Step 5/8 : USER xxradar
 ---> Running in d8f385b2a699
Removing intermediate container d8f385b2a699
 ---> 5b05517af437
Step 6/8 : WORKDIR /scripts
 ---> Running in f470db4d84ed
Removing intermediate container f470db4d84ed
 ---> 4c0a629c5192
Step 7/8 : COPY tlssan_scan.sh tlssan_scan.sh
 ---> d7ec5779c0fd
Step 8/8 : ENTRYPOINT ["/scripts/tlssan_scan.sh"]
 ---> Running in f194ecd54949
Removing intermediate container f194ecd54949
 ---> d2df99bdc66b
Successfully built d2df99bdc66b
Successfully tagged tls_scan:latest
```
```
ubuntu@ip-10-1-1-52:~/test$ docker images
REPOSITORY                                             TAG       IMAGE ID       CREATED              SIZE
tls_scan                                               latest    d2df99bdc66b   7 seconds ago        116MB
debian                                                 latest    d69c6cd3a20d   7 days ago           124MB
ubuntu                                                 latest    ff0fea8310f3   2 weeks ago          72.8MB
974654858447.dkr.ecr.eu-west-3.amazonaws.com/xxradar   latest    02f266b0bdae   7 months ago         109MB
tcpdump                                                v2        02f266b0bdae   7 months ago         109MB
public.ecr.aws/g6o9y4z7/tcpdump                        latest    02f266b0bdae   7 months ago         109MB
public.ecr.aws/g6o9y4z7/xxradar                        latest    02f266b0bdae   7 months ago         109MB
nginx                                                  latest    dd34e67e3371   7 months ago         133MB
974654858447.dkr.ecr.eu-west-3.amazonaws.com/hackon    latest    dd34e67e3371   7 months ago         133MB
ubuntu                                                 18.04     39a8cfeef173   8 months ago         63.1MB
xxradar/hackon                                         latest    c336a56a3899   20 months ago        202MB
974654858447.dkr.ecr.eu-west-3.amazonaws.com/hackon    <none>    c336a56a3899   20 months ago        202MB
dockersec/tcpdump                                      latest    f90950058033   3 years ago          133MB
xxradar/naxsi5                                         latest    9f530a416ad6   6 years ago          212MB
ubuntu@ip-10-1-1-52:~/test$
```
```
$ trivy image tls_scan
2022-04-05T18:56:45.653Z	INFO	Need to update DB
2022-04-05T18:56:45.654Z	INFO	Downloading DB...
31.06 MiB / 31.06 MiB [---------------------------------------------------------------------------------------------------------------------------------------------------------------------------] 100.00% 7.95 MiB p/s 4s
2022-04-05T18:56:55.731Z	INFO	Detected OS: ubuntu
2022-04-05T18:56:55.731Z	INFO	Detecting Ubuntu vulnerabilities...
2022-04-05T18:56:55.742Z	INFO	Number of language-specific files: 0

tls_scan (ubuntu 20.04)
=======================
Total: 14 (UNKNOWN: 0, LOW: 12, MEDIUM: 2, HIGH: 0, CRITICAL: 0)

+-----------+------------------+----------+--------------------------+--------------------------+---------------------------------------+
|  LIBRARY  | VULNERABILITY ID | SEVERITY |    INSTALLED VERSION     |      FIXED VERSION       |                 TITLE                 |
+-----------+------------------+----------+--------------------------+--------------------------+---------------------------------------+
| bash      | CVE-2019-18276   | LOW      | 5.0-6ubuntu1.1           |                          | bash: when effective UID is not       |
|           |                  |          |                          |                          | equal to its real UID the...          |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2019-18276 |
+-----------+------------------+          +--------------------------+--------------------------+---------------------------------------+
| coreutils | CVE-2016-2781    |          | 8.30-3ubuntu2            |                          | coreutils: Non-privileged             |
|           |                  |          |                          |                          | session can escape to the             |
|           |                  |          |                          |                          | parent session in chroot              |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2016-2781  |
+-----------+------------------+          +--------------------------+--------------------------+---------------------------------------+
| libgmp10  | CVE-2021-43618   |          | 2:6.2.0+dfsg-4           |                          | gmp: Integer overflow and resultant   |
|           |                  |          |                          |                          | buffer overflow via crafted input     |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2021-43618 |
+-----------+------------------+          +--------------------------+--------------------------+---------------------------------------+
| libpcre3  | CVE-2017-11164   |          | 2:8.39-12build1          |                          | pcre: OP_KETRMAX feature in the       |
|           |                  |          |                          |                          | match function in pcre_exec.c         |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2017-11164 |
+           +------------------+          +                          +--------------------------+---------------------------------------+
|           | CVE-2019-20838   |          |                          |                          | pcre: Buffer over-read in JIT         |
|           |                  |          |                          |                          | when UTF is disabled and \X or...     |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2019-20838 |
+           +------------------+          +                          +--------------------------+---------------------------------------+
|           | CVE-2020-14155   |          |                          |                          | pcre: Integer overflow when           |
|           |                  |          |                          |                          | parsing callout numeric arguments     |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2020-14155 |
+-----------+------------------+          +--------------------------+--------------------------+---------------------------------------+
| libsepol1 | CVE-2021-36084   |          | 3.0-1                    |                          | libsepol: use-after-free in           |
|           |                  |          |                          |                          | __cil_verify_classperms()             |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2021-36084 |
+           +------------------+          +                          +--------------------------+---------------------------------------+
|           | CVE-2021-36085   |          |                          |                          | libsepol: use-after-free in           |
|           |                  |          |                          |                          | __cil_verify_classperms()             |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2021-36085 |
+           +------------------+          +                          +--------------------------+---------------------------------------+
|           | CVE-2021-36086   |          |                          |                          | libsepol: use-after-free in           |
|           |                  |          |                          |                          | cil_reset_classpermission()           |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2021-36086 |
+           +------------------+          +                          +--------------------------+---------------------------------------+
|           | CVE-2021-36087   |          |                          |                          | libsepol: heap-based buffer           |
|           |                  |          |                          |                          | overflow in ebitmap_match_any()       |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2021-36087 |
+-----------+------------------+          +--------------------------+--------------------------+---------------------------------------+
| login     | CVE-2013-4235    |          | 1:4.8.1-1ubuntu5.20.04.1 |                          | shadow-utils: TOCTOU race             |
|           |                  |          |                          |                          | conditions by copying and             |
|           |                  |          |                          |                          | removing directory trees              |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2013-4235  |
+-----------+                  +          +                          +--------------------------+                                       +
| passwd    |                  |          |                          |                          |                                       |
|           |                  |          |                          |                          |                                       |
|           |                  |          |                          |                          |                                       |
|           |                  |          |                          |                          |                                       |
+-----------+------------------+----------+--------------------------+--------------------------+---------------------------------------+
| perl-base | CVE-2020-16156   | MEDIUM   | 5.30.0-9ubuntu0.2        |                          | perl-CPAN: Bypass of verification     |
|           |                  |          |                          |                          | of signatures in CHECKSUMS files      |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2020-16156 |
+-----------+------------------+          +--------------------------+--------------------------+---------------------------------------+
| zlib1g    | CVE-2018-25032   |          | 1:1.2.11.dfsg-2ubuntu1.2 | 1:1.2.11.dfsg-2ubuntu1.3 | zlib: A flaw in zlib-1.2.11           |
|           |                  |          |                          |                          | when compressing (not                 |
|           |                  |          |                          |                          | decompressing!) certain inputs.       |
|           |                  |          |                          |                          | -->avd.aquasec.com/nvd/cve-2018-25032 |
+-----------+------------------+----------+--------------------------+--------------------------+---------------------------------------+
ubuntu@ip-10-1-1-52:~/test$
```
```
cat <<EOF >fdevsec.yaml
version: v1

id:
  org: 506202ab-209a-49d9-aaa3-59ea5xxxxxxf
  app: 47638376-dc2c-4f77-9193-c3a2exxxxxx0

scanners:
- sast
- sca
- secret

languages:
- python
EOF
```
```
ubuntu@ip-10-1-1-52:~/test$ docker pull registry.fortidevsec.forticloud.com/fdevsec_sast:latest
...
```
```
ubuntu@ip-10-1-1-52:~/test$ docker run -i --mount type=bind,source="$(pwd)",target=/scan  registry.fortidevsec.forticloud.com/fdevsec_sast:latest
2022/04/05 19:13:37 INFO: Not GIT repo.
2022/04/05 19:13:37 Loaded scan config for Org ID:  506202ab-209a-49d9-aaa3-59ea554452df
2022/04/05 19:13:37 Languages configured in conf file:  []
Doesnt seem like its git repo.
2022/04/05 19:13:37 Unable to create local git. exit status 128
2022/04/05 19:13:37 Detected languages are:  []
2022/04/05 19:13:37 Scanners configured in conf file:  [sast sca secret]
2022/04/05 19:13:38 Total local scanners enabled: 2
2022/04/05 19:13:38 Running parallel scan as per user config.
2022/04/05 19:13:39 gitleaksOutput file not Generated.
2022/04/05 19:13:51 FortiDevSec SAST scanner done, exiting.
ubuntu@ip-10-1-1-52:~/test$
```
```
ubuntu@ip-10-1-1-52:~/test$ docker tag tls_scan xxradar/tlsscanner:001
```
```
ubuntu@ip-10-1-1-52:~/test$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: xxradar
Password:
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```
```
ubuntu@ip-10-1-1-52:~/test$ docker push xxradar/tlsscanner:001
The push refers to repository [docker.io/xxradar/tlsscanner]
196c170a6b4a: Pushed
ae4f105c7a2d: Pushed
83c146231f55: Pushed
c47e2c7d9cb4: Pushed
867d0767a47c: Mounted from library/ubuntu
001: digest: sha256:4534b6953777a25bca78b3e4a0a5e500cdeb90f7564544defb59839c90b5f410 size: 1365
ubuntu@ip-10-1-1-52:~/test$
```
