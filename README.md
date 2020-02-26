## How to install YONA in KUBUNTU OS

Basically, Yona installation is in two steps:

#### 1. MariaDB install

1. Add the MariaDB package to the APT repository.

   ```bash
   apt install python-software-properties
   apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
   add-apt-repository 'deb [arch=amd64,i386,ppc64el] http://ftp.kaist.ac.kr/mariadb/repo/10.1/ubuntu xenial main'
   apt update
   ```

2. Install MariaDB by using the following command:
   ```bash
   apt install mariadb-server
   ```
   
3. Confirm installation.

   ```bash
   root@smarfpc:~# netstat -tnlp | grep 3306
   tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      27469/mysqld 
   ```



#### 2. Create user and database after installing DB

1. Connect to MariaDB with root

   ```bash
   mysql -uroot 
   ```

2. Create user `ucsm` and set password. 'ucsm90-='

   ```mysql
   create user 'ucsm'@'localhost' IDENTIFIED BY 'ucsm90-=';
   ```

3. Create database `yona` (set UTF8 extended chars).

   ```mysql
   create database yona
     DEFAULT CHARACTER SET utf8mb4
     DEFAULT COLLATE utf8mb4_bin
   ;
   ```

4. Grant privileges

   ```mysql
   GRANT ALL ON yona.* to 'yona'@'localhost';
   ```

5. Test.

   ```bash
   mysql -u yona -p'yonadan'
   use yona
   ```

#### MariaDB Command Line

```bash
sudo service mariadb restart
sudo service mariadb start
sudo service mariadb stop
sudo service mariadb status
```



#### 2. Yona install

0. Prerequisite

   note. **Please refer to "Installation Zulu8-JDK" MARKDOWN.**

1. Download the latest version of Yona from https://github.com/yona-projects/yona/releases and unzip it.

   ```bash
   sudo wget https://github.com/yona-projects/yona/releases/download/v1.3.0/yona-v1.3.0-bin.zip
   sudo unzip yona.zip
   ```

2. Go to the unpacked location and run `bin/yona`.

   ```bash
   cd yona
   bin/yona
   sudo ./yona
   ```

3. Execution will terminate with an error that the password is wrong. It's noraml. Don't worry. :)

4. DB configuration

   note : ***You need to modify the DB connection settings to connect the MariaDB you installed earlier.
   In the application.conf file under the conf folder, change the password in the following section to the db password set above***

   ```properties
   ...
   db.default.driver=org.mariadb.jdbc.Driver
   db.default.url="jdbc:mariadb://127.0.0.1:3306/yona?useServerPrepStmts=true"
   db.default.user=ucsm
   db.default.password="ucsm90-="
   ...
   ```

