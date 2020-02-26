## Setup XRDP on Kubuntu OS

#### Installation using shell script file

1. download install-xrdp-3.0.sh

2. Execute command line below to grant access 'sh' and Execute the shell script.

   ```bash
    sudo unzip install-xrdp-3.0.sh.zip
    sudo chmod 755 ~/Downloads/install-xrdp-3.0.sh
    
    sudo ./install-xrdp-3.0.sh
    # select 'yes' for all requests except 'sound' request. 
   ```

3. reboot  and connection test with the thin client.



####Precautions

1. If you want to add remote desktop user,  make a user in ubuntu. One user cannot be accused in  two session.