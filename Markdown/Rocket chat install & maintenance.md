# How to use Rocketchat

Rocketchat is free open source solution for team communications.

supported web site.

http://chat.domain.com 

Supported Application.(IOS, Android)

https://play.google.com/store/apps/details?id=chat.rocket.android (Android)

 



## Install Rocketchat

snapd can be installed from the command line: 

```bash
$ sudo apt update
$ sudo apt install snapd
```

and install rocketchat-server:

```bash
$ sudo snap install rocketchat-server
```

run from the command line:

```bash
# start|stop|restart|status
$ sudo service snap.rocketchat-server.rocketchat-server start
```



## Backup

As normal user as archive:

```bash
sudo snap run rocketchat-server.backupdb
```



Backup is created in path bellow:

```bash
 /var/snap/rocketchat-server/common/backup/
```



## Restore backup

first, stop rocket chat-server:

```bash
sudo service snap.rocketchat-server.rocketchat-server stop
```



As normal user:

```bash
sudo snap run rocketchat-server.restoredb /var/snap/rocketchat-server/common/backup/rocketchat_backup.tgz
```



## write backup-scrip

Make a directory on the path you want and Grant permission to access for the directory :

```bash
$ sudo mkdir crontab_script

$ sudo nano mongdb_backup.sh

$ sudo chmod 755 mongdb_backup.sh
```



Write the shell script for back-up: 

```sh
#!/bin/sh
echo "backup wekan_db..."
sudo wekan.database-backup
echo "completed"
echo "backup rocketchat_db"
sudo snap run rocketchat-server.backupdb
echo "completed"
```



As root user then execute crontab:

```bash
$ sudo su

# crontab -e
```



Add a crontab rule(period 6hours): 

```sh
0 */6 * * * /home/smarf/Application/crontab_script/mongo_backup.sh >> /home/smarf/Application/crontab_script/crontab_log/mongo_backup.log  2>&1
```



Restart the cron service:

```bash
# sudo service cron restart
```

