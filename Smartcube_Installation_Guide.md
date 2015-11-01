## Smartcube Installation Guide ##

- **Cluster configuration**<br>
 scworker00, IP: 10.64.51.148<br>
 scworker01, IP: 10.64.51.149<br>
 scbackup00, IP: 10.64.51.150<br>
- **Operating System**<br>
 SUSE Linux Enterprise Server 12<br>
- **ISO Image**<br>
 SLE-12-Server-DVD-x86_64-GM-DVD1.iso<br>

----------

1. **Stage-0-Initialization**<br>
 Description: Add user `smartcube` with `sudo` permission<br>
 Install File: *`Stage-0-Initializaiton`*(Upload via WinSCP)<br>
 Install File Location: *`/root/Stage-0-Initializaiton`*<br>
 VM involved: scworker00, scworker01, scbackup00<br>
 Login user: `root`<br>
 Resources required: `None`<br>
 Script prepared: `$ROOT_HOME/smartcube-init`(Upload via WinSCP)<br>
 Easy install:<br>
 ```Bash
 cd $ROOT_HOME/smartcube-init
 sh smartcube-init.sh install
 ```
 Set password:<br>
 ```Bash
 passwd smartcube
 ```

2. **Mount hard disk**<br>
 Login user: `smartcube`<br>
 Resources required:<br>
 `Hard disk 1: /dev/sdb, 500GB`<br>
 `Hard disk 2: /dev/sdc, 10TB`<br>
 `Hard disk 3: /dev/sdd, 10TB`<br>
 Script prepared: `$SMARTCUBE_HOME/smartcube-mount`(Upload via WinSCP)<br>
 Easy install:<br>
 ```Bash
 cd $ROOT_HOME/smartcube-mount
 sh smartcube-mount.sh install
 ```

3. **Install basic packages and softwares**<br>
 Login user: `smartcube`<br>
 Resources required:<br>
 `Local zypper repository: $SMARTCUBE_HOME/disk/sle12.tar.gz`<br>
 `Local zypper repository configture file: $SMARTCUBE_HOME/disk/localrepo.repo`<br>
 `Docker configture file: $SMARTCUBE_HOME/disk/docker.config`<br>
 `Hadoop setup file: $SMARTCUBE_HOME/disk/Smartcube.tar.gz`<br>
 `Bashrc configure file: $SMARTCUBE_HOME/disk/bashrc.config`<br>
 (Upload via WinSCP)<br>
 Script prepared: `$SMARTCUBE_HOME/smartcube-preparation`(Upload via WinSCP)<br>
 Easy install:<br>
 ```Bash
 cd $ROOT_HOME/smartcube-preparation
 sh smartcube-preparation.sh install
 ```
 (Note: Relogin as `smartcube` to enable execute docker commands without `sudo`)<br>
