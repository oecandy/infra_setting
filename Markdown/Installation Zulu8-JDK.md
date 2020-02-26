## How to install ZULU-JAVA 8 in MANJARO OS

1. Go to  https://www.azul.com/downloads/zulu-community/?&version=java-8-lts&os=&os=scientific-linux&architecture=x86-64-bit&package=jdk

2. Download zulu jdk ver.8u232b18(.tar.gz)

3. Unzip the file.
   
```bash
   sudo tar -xvzf jdk-7u7-linux-i586.tar.gz
   ```
   
4. Move the directory to /usr/lib/jvm/{jdk directory}
   
   ```bash
   sudo mv {zulu-jdk-8} /usr/lib/jvm/{zulu-jdk-8}
   ```
   
5. Set default java to zulu 8
   confirm the installed java list : 
   
   ```bash
   archlinux-java status
   ```
   
   set default java : 
   
   ```bash
   archlinux-java set {java}
   ```
   
   

## How to install ZULU-JAVA 8 in KUBUNTU OS

1. Import Azul's public key.
   
```bash
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
   ```
   
2. Add the Azul package to the APT repository.
   
```bash
   sudo apt-add-repository 'deb http://repos.azulsystems.com/ubuntu stable main'
   ```
   
3. Update the information about available packages.
   
   ```bash
   sudo apt-get update
   ```
   
4. Install Zulu by using the following command:
   
   ```bash
   sudo apt-get -y install zulu-8
   ```
   
   