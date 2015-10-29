## Smartcube Installation Guide ##

 - **Cluster configuration**
scworker00, IP: 10.64.51.148<br>
scworker01, IP: 10.64.51.149<br>
scbackup00, IP: 10.64.51.150<br>
 - **Operating System**  
 SUSE Linux Enterprise Server 12  
 - **ISO Image**  
 SLE-12-Server-DVD-x86_64-GM-DVD1.iso  

----------

1. **Add user `smartcube` with `sudo` permission**
Login user: `Root`
Resources required: `None`
Script prepared: `$ROOT_HOME/smartcube-init`(Upload via WinSCP)
Easy install:
```bash
cd $ROOT_HOME/smartcube-init
sh smartcube-init.sh install
```
Set password:
```bash
passwd smartcube
```

2. **Mount hard disk**
Login user: `smartcube`
Resources required:
`Hard disk 1: /dev/sdb, 500GB`
`Hard disk 2: /dev/sdc, 10TB`
`Hard disk 3: /dev/sdd, 10TB`
Script prepared: `$SMARTCUBE_HOME/smartcube-mount`(Upload via WinSCP)
Easy install:
```bash
cd $ROOT_HOME/smartcube-mount
sh smartcube-mount.sh install
```

3. **Install basic packages and softwares**
Login user: `smartcube`
Resources required:
`Local zypper repository: $SMARTCUBE_HOME/disk/sle12.tar.gz`
`Local zypper repository configture file: $SMARTCUBE_HOME/disk/localrepo.repo`
`Docker configture file: $SMARTCUBE_HOME/disk/docker.config`
`Hadoop setup file: $SMARTCUBE_HOME/disk/Smartcube.tar.gz`
`Bashrc configure file: $SMARTCUBE_HOME/disk/bashrc.config`
(Upload via WinSCP)
Script prepared: `$SMARTCUBE_HOME/smartcube-preparation`(Upload via WinSCP)
Easy install:
```bash
cd $ROOT_HOME/smartcube-preparation
sh smartcube-preparation.sh install
```
(Note: Relogin as smartcube to enable execute docker command without sudo)
