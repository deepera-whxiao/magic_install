## Smartcube Installation Guide ##

- **Cluster configuration**<br>
 `scworker00`, IP: 10.64.51.148<br>
 `scworker01`, IP: 10.64.51.149<br>
 `scbackup00`, IP: 10.64.51.150<br>
- **Operating System**<br>
 SUSE Linux Enterprise Server 12<br>
- **ISO Image**<br>
 SLE-12-Server-DVD-x86_64-GM-DVD1.iso<br>

----------

1. **Stage-0-Initialization**<br>
 Description: Add user `smartcube` with `sudo` permission<br>
 Install File Required: *`Stage-0-Initializaiton`*(Upload via WinSCP)<br>
 Install File Location: *`/root/Stage-0-Initializaiton`*($STAGE0_HOME)<br>
 VM involved: `scworker00`, `scworker01`, `scbackup00`<br>
 Login user: `root`<br>
 Easy install:<br>
 ```Bash
 cd $STAGE0_HOME
 bash install-stage-0
 ```
 Set password for user `smartcube`:<br>
 ```Bash
 passwd smartcube
 ```

2. **Stage-1-Preparation**<br>
 Description: Configure network and Mount hard disk<br>
 Install File Required: *`Stage-1-Preparation`*(Upload via WinSCP)<br>
 Install File Location: *`/home/smartcube/Stage-1-Preparation`*($STAGE1_HOME)<br>
 VMs involved: `scworker00`, `scworker01`, `scbackup00`<br>
 Login user: `smartcube`<br>
 Easy install:<br>
 Step 1: Edit */etc/hostname* file<br>
 ```Bash
 sudo vim /etc/hostname
 ```
 Change the hostname(Take `scworker00` as an example)<br>
 ```
 scworker00
 ```
 Step 2: Edit */etc/hosts* file<br>
 ```Bash
 sudo vim /etc/hosts
 ```
 Append the following lines:<br>
 ```
 10.64.51.148, scworker00
 10.64.51.149, scworker01
 10.64.51.150, scbackup00
 ```
 Step 3: Restart the network service and verify hostname configuration(Take `scworker00` as an example)<br>
 ```Bash
 sudo hostname scworker00
 sudo service network restart
 hostname
 ```
 Step 4: Configure SSH atuo login among `scworker00`, `scworker01`, `scbackup00`<br>
 a. For `scworker00`<br>
 ```
 ssh-keygen -t rsa -q
 > Enter file in which to save the key (/home/smartcube/.ssh/id_rsa):
 > Enter passphrase (empty for no passphrase):
 > Enter same passphrase again:
 cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
 chmod 600 ~/.ssh/authorized_keys
 mv .ssh/id_rsa .ssh/id_rsa.pub .ssh/authorized_keys tmp-ssh/
 scp -r .ssh smartcube@scworker01:/home/smartcube
 scp -r .ssh smartcube@scbackup00:/home/smartcube
 ```
 b. For `scworker01`, `scbackup00`<br>
 ```Bash
 ssh smartcube@scworker00
 ```
 Step 5: Mount hard disk<br>
 ```Bash
 cd $STAGE1_HOME
 bash install-stage-1
 ```

2. ****<br>
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
 Script prepared: `$SMARTCUBE_HOME/smartcube-preparation`(Upload via WinSCP)<br
 Easy install:<br>
 ```Bash
 cd $ROOT_HOME/smartcube-preparation
 sh smartcube-preparation.sh install
 ```
 (Note: Relogin as `smartcube` to enable execute docker commands without `sudo`)<br>
