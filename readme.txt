# ekz1

# DHCP server
1. Installation
```bash
$ sudo apt install isc-dhcp-server
```
2. Configuration
```bash
$ sudo nano /etc/dhcp/dhcpd.conf
```
3. Config for auto dhcp and static
```bash
sunbet 172.16.2.0 netmast 255.255.255.240 {
  range 192.168.188.10 192.168.188.20;
  option routers 172.16.2.1;
  option subnet-mask 255.255.255.240;
  option broadcast-address 172.16.2.15;
}

host static-cli {
hardware ithernet XX:XX:XX:XX:XX:XX; # MAC address
fixed-address 172.168.2.2;
}
```
4. Restart service and enable
```bash
$ sudo systemctl restart isc-dhcp-server
$ sudo systemctl enable isc-dhcp-server
```
___

# Crontab
1. Open crontab
```bash
$ sudo crontab -e
```
2. Add mail for logs
```bash
MAILTO=email@example.com
```
4. Setup crontab script
```bash
0 */1 * * * /path/to/script
^  ^  ^ ^ ^
m  h  d m w
```
___

# Samba server
1. Install samba
```bash
$ sudo apt install samba
```
2. Create directory and add privileges
```bash
$ sudo mkdir sambafolder
$ sudo chown $USER: /path/to/sambafolder
```
3. Add folder to /etc/samba/smb.conf
```bash
[netfolder]
   path = /path/to/sambafolder
   writable = yes
   public = no
```
4. Set password for user
```bash
$ sudo smbpasswd -a user
```
5. Restart samba service
```bash
$ sudo systemctl restart smbd
```
# Samba client
1. Install required packages
```bash
$ sudo apt install cifs-utils
```
2. Create mount point directory
```bash
mkdir /mnt/sambafolder
```
3. Create credentials for samba connection
```bash
$ nano ~/.smbcred

username=target_user_name
password=target_user_password
```
4. Set ownetship of the cred file
```bash
$ sudo chown $USER: ~/.smbcred
$ sudo chmod 600 ~/.smbcred
```
5. Mount share folder
```bash
$ sudo mount -t cifs -o credentials=~/.smbcred //x.x.x.x/path/to/share /mnt/sambafolder
```
6. Optional (if cred not working) mount without credential file
```bash
$ sudo mount -t cifs //x.x.x.x/path/to/share /mnt/sambafolder
```
___

# DNS server with BIND
*Simply put just config DNS server with webmin*
1. Add webmin repo to sources.list
```bash
...
deb http://download.webmin.com/download/repository sarge contrib
```
2. Update sources and install webmin
```bash
$ sudo update
$ sudo apt install webmin
```
3. Do something with DNS server in web interface. Good luck :)
___

*written by Dmitriy A.*
