## How to install YONA in KUBUNTU OS

Basically, Yona installation is in two steps:

#### 1. Install MariaDB

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



#### 2. Install Yona

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



## # Install Yona (use Docker)

### 0. Install docker and docker-compose

Excute command line bellow to install docker

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker

### use Docker without 'sudo'
sudo usermod -aG docker $USER
```



Install docker-compose

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

### If the command docker-compose fails after installation, check your path. You can also create a symbolic link to /usr/bin or any other directory in your path.

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

### Check installation.
docker-compose --version
```





### 1. Docker-compose.yml file

```bash
version: '2'
services:
  yona:
    image: pokev25/yona:latest
    container_name: yona
    restart: always
    environment:
      - BEFORE_SCRIPT=before.sh
      - JAVA_OPTS=-Xmx2048m -Xms1024m
    volumes:
      - /home/yona/data:/yona/data                    # 데이터를 유지할 위치 설정
    ports:
      - "9000:9000"

  yona_db:
    image: mariadb
    container_name: yo_db
    restart: always
    volumes:
      - /home/yona/mysql/data:/var/lib/mysql          # 데이터를 유지할 위치 설정
    ports:
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: 1234
      MYSQL_DATABASE: yona
      MYSQL_USER: test
      MYSQL_PASSWORD: 1234
    command:
      - --character-set-server=utf8mb4
      - --collation-server=utf8mb4_unicode_ci

```



### 2. Execute docker-compose.yml

```bash
sudo docker-compose -f docker-file.yml up -d
```

Execution will terminate with an error that the password is wrong. It's noraml :). (Application Setup is not yet complete.)

1. Modify the application  configuration file which is gernerated on terminate.

   ```bash
   cd /home/yona/data/conf 
   sudo nano application.conf
   ```

   ```yaml
   ~~~~
   
   # MariaDB
   
   db.default.driver=org.mariadb.jdbc.Driver
   
   #db.default.url="jdbc:mariadb://127.0.0.1:3306/db_name?useServerPrepStmts=true"
   
   db.default.url="jdbc:mariadb://127.0.0.1:3306/yona?useServerPrepStmts=true"
   
   db.default.user=test
   
   db.default.password="1234"
   
   ~~~~
   application.scheme="http"
   
   application.hostname="192.168.0.0" # Changed according to the router's host ip.
   
   application.port="9000"
   ~~~
   smtp.host = smtp.gmail.com
   
   smtp.port = 465
   
   smtp.ssl = true
   
   smtp.user = "admin's mail@gmail.com"
   
   # Be careful!!! Not to leak password
   
   smtp.password = "password"
   
   smtp.domain = gmail.com
   
   #true to use mock mailer for testing, false for using real mail server
   
   smtp.mock = false
   
   # optional, size of mail archive for tests, default: 5
   
   smtp.archive.size = 5
   
   ~~~~
   ```

   

2. Excute docker-compose.yml

   ```bash
   cd {docker-compose's path}
   sudo docker-compose up -d
   ```

   