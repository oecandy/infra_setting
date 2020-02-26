# How to use Wekan

Wekan is a kanban board based open-source.

 

## Install Rocketchat

snapd can be installed from the command line: (If it is already installed, skip)

```bash
$ sudo apt update
$ sudo apt install snapd
```

and install wekan:

```bash
snap install wekan
```

setting wekan configuration.

```bash
# set base-url : ex)http://wekan.smarf.kr/
snap set wekan root-url='https://example.com/something'

snap set wekan port='3001'
```

run from the command line:

```bash
# start|stop|restart|status
$ sudo service snap.wekan.wekan start
```



## Setup backup directory

Create backup directory and set permissions

```bash
$ sudo mkdir /var/snap/wekan/common/db-backups
$ sudo chmod 777 /var/snap/wekan/common/db-backups
```



## Backup

As normal user as archive:

```bash
$ wekan.database-backup
```

Backup is created in directory:

```bash
/var/snap/wekan/common/db-backups
```

There is optional Backup file is optional parameter `$ wekan.database-backup BACKUPFILENAME`, but probably it does not work.



## List backups

You need to first create one backup, otherwise this command shows error.

To list existing backups in default directory, as normal user:

```bash
$ wekan.database-list-backups
```



## Restore backup

As normal user:

You can check on what port snap mongo is running with:

```bash
$ sudo netstat -plant | grep mongo
```

Then stop service and connect to that port, for example:

```bash
$ sudo service snap.wekan.wekan stop
# this port is changed depending on the result of previous step.
$ mongo --port 27019	
```

Then look what database name wekan database has:

```sql
> show dbs
```

Delete database(If the database name is wekan):

```sql
> use wekan
> db.dropDatabase();
```

```bash
> exit
```

Then restore database to inside snap mongo:

```bash
$ wekan.database-restore FULL-PATH-TO-BACKUP-FILENAME

$ sudo service snap.wekan.wekan start
```



## write backup-scrip(If it is already worked, skip)

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

