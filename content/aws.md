# AWS (Linux)

## Enable password login

- Check [this](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-password-login/) first

## Add a user
- `sudo adduser [user name]`
- `sudo password [user name]`

## Change user name

- Check [this](https://serverfault.com/questions/437342/how-can-i-rename-an-unix-user)

## Add sudo user

- Check [this](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-centos-quickstart)

## Steps to expand EBS disk size

1. Modify the size in the Volume page
1. `sudo yum install xfsprogs`
1. ``` shell
    [ec2-user ~]$ lsblk
    NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    xvda    202:0    0  30G  0 disk
    └─xvda1 202:1    0  30G  0 part /
    xvdb    202:16   0  30G  0 disk /mnt
    xvdf    202:80   0  35G  0 disk
    └─xvdf1 202:81   0   8G  0 part
    [ec2-user ~]$ df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/xvda1            8.0G  943M  6.9G  12% /
    tmpfs                 1.9G     0  1.9G   0% /dev/shm
    /dev/xvdf            1014M   33M  982M   4% /mnt
    [ec2-user ~]$sudo growpart /dev/xvdf 1
    CHANGED: disk=/dev/xvdf partition=1: start=4096 old: size=16773086,end=16777182 new: size=73396190,end=73400286
    [ec2-user ~]$ sudo xfs_growfs -d /mnt
    meta-data=/dev/xvdf              isize=256    agcount=4, agsize=65536 blks
            =                       sectsz=512   attr=2
    data     =                       bsize=4096   blocks=262144, imaxpct=25
            =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0
    log      =internal               bsize=4096   blocks=2560, version=2
            =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0
    data blocks changed from 262144 to 26214400

   ```
