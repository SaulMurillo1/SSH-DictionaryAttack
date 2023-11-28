<h1>SSH Dictionary Attack</h1>


<h2>Description</h2>
This project consists of using nmap, hydra, & msfconsole as Linux tools to perfrom dictionary attacks on a targeted SSH server. 
<br />
<br />
<br />

Disclaimer: The Kali Linux user machine and target machine used in this project was provided to me by INE for educational purposes. The misuse of the information in this project lab can result in criminal charges brought against the individual/individuals in question.
<br />


<h2>Languages and Utilities Used</h2>

- <b>nmap</b>
- <b>hydra</b>
- <b>msfconsole</b>


<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Project walk-through:</h2>

<p align="left">
Ping target machine to verify that it is active, then run nmap scan to look for open tcp ports: <br/>
<br/>
- INE has provided me with Kali Linux GUI & target machine (target machine is one ip address above from mine).  I will run an ip a command to verify my own ip address. Then, I'll run a ping command to verify the target ip address is active.
<br/>
- Once I can verify that the target machine is active, I will run nmap scan to look for open tcp ports and try to obtain port information. 
<br/>
- Down below, we can see that port 22 (SSH) is open and its version is OpenSSH (Ubuntu Linux), which tells us that it is running Linux.
<br/>
<br/>
Commands: ip a
<br/>
ping 192.239.69.3
<br/>
nmap 192.239.69.3
<br/>
nmap 192.239.69.3 -p 22 -sV -O
<br/>
<br/>
<img src="https://i.imgur.com/WAHtHYv.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<img src="https://i.imgur.com/7f8KtmC.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Utilize Hydra (Linux tool) to perform a dictionary attack on the target SSH server: <br/>
<br/>
- Hydra is a brute-forcing tool that helps penetration testers and ethical hackers crack the passwords of network services. Hydra can perform rapid dictionary attacks against more than 50 protocols. This includes telnet, SSH, FTP, HTTP, HTTPS, SMB, databases, and several other services.
<br/>
- Below, we can see that I used the Hydra tool to see if I could successfully find a password for a user named "student".
<br/>
- From the results, it looks like the Hydra tool was able to successfully find a valid password for the user "student" by using the rockyou wordlist.
<br/>
<br/>
Commands: gzip -d /usr/share/wordlists/rockyou.txt.gz
<br/>
hydra -l student -P /usr/share/wordlists/rockyou.txt 192.239.69.3 ssh
<br/>
<br/>
<img src="https://i.imgur.com/2BTukDQ.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Now that we have a valid password for the user "student", test an SSH log in: <br/>
<br/>
- We can see that I was able to successfully log into the SSH server, however it looks like the "student" user cannot really do much in regards with user permissions. 
<br/>
<br/>
Command: ssh student@192.239.69.3
<br/>
<br/>
<img src="https://i.imgur.com/NkUnaRy.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Utilize the Nmap tool to try and find a valid password for user "administrator": <br/>
<br/>
- We can see that nmap started brute forcing by trying multiple passwords for user "administrator" until if found a match with the password sunshine. 
<br/>
<br/>
Commands: echo "administrator" > user
<br/>
nmap 192.239.69.3 -p 22 --script ssh-brute --script-args userdb=/root/user
<br/>
<br/>
<img src="https://i.imgur.com/hyyFnMI.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Utilize the msfconsole (Metasploit) tool to conduct a dictionary attack and try to find a valid password for user "root": <br/>
<br/>
- We can see that Metasploit was able to use a wordlist to successfully find a password (attack) for the user "root". 
<br/>
<br/>
Commands: msfconsole
<br/>
use auxiliary/scanner/ssh/ssh_login
<br/>
set rhosts 192.239.69.3
<br/>
set userpass_file /usr/share/wordlists/metasploit/root_userpass.txt
<br/>
set stop_on_success true
<br/>
set verbose true
<br/>
exploit
<br/>
<br/>
<img src="https://i.imgur.com/EckkDx3.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<img src="https://i.imgur.com/7lV2bHA.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<img src="https://i.imgur.com/hV3G79C.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<img src="https://i.imgur.com/bFKCi8s.png" height="80%" width="80%" alt="SSH Dictionary Attack" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />



</p>
