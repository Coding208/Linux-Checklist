<details open>
  <summary>  README Basics  </summary>
  <br>
  
 Read the README. Get root passwords and authorized users. 

Answer forensic questions. If you need to find files use the command ```find /home -name '*' -type f``` You can change “/home” to “/” if you want to search the entire computer.

Manage users. Delete any that aren’t supposed to exist. Undisable the accounts that are supposed to exist. Make sure everyone who should be admin is admin and everyone who is supposed to be standard is standard. Add any that are needed. Make sure to unlock and re-lock. System Settings> Users and Groups > Unlock.

Look in the README for “insecure” passwords. Change those users’ passwords.

sudo ufw enable Allow any ports in the README

Correct file permissions: Execute the following commands to put correct file permissions on important system files (with sudo): 

```chmod -R 444 /var/log```

```chmod 440 /etc/passwd```

```chmod 440 /etc/shadow```

```chmod 440 /etc/group```

```chmod -R 444 /etc/ssh```

</details>
<details open> 
  <summary>  Bad Stuff  </summary>
</br>
Delete all non-work related files (If specified in readme) use: ```find / -name '*.<file extension>' -type f -delete```
  Remove .mp3, .mov, .mp4, .avi, .mpg, .mpeg, .flac, .m4a, .flv, .ogg, .gif, .png, .jpg, and .jpeg.

sudo apt-get install bum Use bum to look for bad services. Remove apache, nginx, bind9 (DNS), ssh, or FTP unless otherwise stated in the README. Type sudo bum to start bum.

```sysctl -n net.ipv4.tcp_syncookies``` stops bad cookies. 

```sudo nano /etc/apt/sources.list``` Check for any bad sources

```sudo nano /etc/hosts``` Check for any redirects

```sudo crontab -e``` - check for anything in there, it might be malicious. 

```sudo nano /etc/lightdm/lightdm.conf``` and add ```allow-guest=false``` at the bottom, then do “sudo service lightdm restart”  (make sure you aren’t doing any updates when you restart lightdm)

Remove hacking tools. Open Ubuntu Software center and look at recently installed software for “nmap”, “ophcrack”, or anything else that looks suspicious. If in doubt look up its name.

Remove non-work related software. Anything that looks like a game should be removed. If in doubt look it up. If you find a file called “passwords.txt” make sure to delete it.

Disable samba (unless readme says otherwise) using sudo service smbd stop and sudo service samba stop (also uninstall samba too)

Purge netcat. Use ```sudo apt-get purge netcat nc netcat-*``` to purge all forms of netcat.

Secure Ports. Follow these steps: sudo ss -ln | grep tcp This lists all open ports Look at the list of open ports and use sudo lsof -i :<Port> to get the program Determine if the port is a backdoor (if it has nc or netcat in the name it is a backdoor) Determine if the program is supposed to be on the computer These ports are safe: 22, 53, 631, 35509

Disable FTP services:
Bring up a terminal, and type ```service --status-all``` and press Enter
Type ```sudo apt-get remove pure-ftpd``` and press Enter. Type the password, and press enter. Hit yes, and enter.

</details>
<details open> 
  <summary>  Update/File editing  </summary>
</br>
  
Go to terminal and ```sudo apt-get update``` and then ```sudo apt-get upgrade``` and ```sudo apt-get dist-upgrade```  Let the apps update while you are doing other stuff.
  
System Settings>Software&Updates have it check for recommended updates once a day.

After Updates Complete: sudo restart lightdm This gives points for editing lightdm.conf

```sudo nano /etc/ssh/sshd_config``` and add ```PermitRootLogin no``` to the bottom. You might need to stop ssh, edit config, and restart. ```sudo service ssh restart```

```sudo nano /etc/pam.d/common-password``` Install ```sudo apt-get install libpam-cracklib``` and then add ```password requisite pam_cracklib.so minlen=10``` to the end of the file. 

```sudo nano /etc/pam.d/common-password``` Use ^W and look for ```pam_unix.so``` add ```minlen=8``` to the end of this line
</details>
<details open>
  <summary> Password Config </summary>
    <br>
  
  sudo nano /etc/login.defs change/add to:
<pre>
  PASS_MAX_DAYS 90
  PASS_MIN_DAYS 7
  PASS_WARN_AGE 14
</pre>


```sudo visudo``` Make sure only the default account can sudo.
  
### Might be bad 
```sudo nano /etc/pam.d/common-auth``` Use ^W to find pam_tally2.so add deny=5 unlock_time=1800 to the end of the line. This denies password attempts and adds a lockout period.

</details>


<details open> 
<summary>  Users </summary>
</br>
  
Disable Admin on non-admin members

Enable Admin on Admin members

Turn of auto sign in on everyone except for yourself

Change weak passwords
</details>

<details open>
<summary> SECONDARY! </summary>
</br>
For more items, look at https://github.com/Forty-Bot/linux-checklist

<details open>
<summary><h2>Remove Unauthorized Users</h2></summary>
<br>
<pre>sudo userdel $user</pre>
Be careful, if you delete a user that is authorized, you can't get points back by re-creating it
</details>

<details open>
<summary><h2>Remove Users from Sudo Group</h2></summary>
<br>
<pre>sudo deluser $user $group</pre>
</details>

<details open>
<summary><h2>Add Users to Groups According to README</h2></summary>
<br>
<pre>sudo usermod -a -G $group $user</pre>
</details>

<details open>
<summary><h2>Create New Users According to README</h2></summary>
<br>
<pre>sudo adduser $user</pre>
</details>

<details open>
<summary><h2>Password Rules</h2></summary>
Edit /etc/login.defs and add to the bottom:
<pre>
PASS_MIN_DAYS 7
PASS_MAX_DAYS 90
PASS_WARN_AGE 14
</pre>
</details>

<details open>
<summary><h2>Enable UFW</h2></summary>
<br>
<pre>sudo ufw enable</pre>
</details>

<details open>
<summary><h2>Remove Rogue Services</h2></summary>
<br>
<pre>sudo service --status-all</pre>
<pre>sudo systemctl disable $service</pre>
</details>


<details open>
<summary><h2>Enable Automatic Updates (Daily)</h2></summary>
<br>
<pre>sudo apt install unattended-upgrades</pre>
</details>

<details open>
<summary><h2>Update Systemd</h2></summary>
<br>
<pre>sudo apt upgrade systemd</pre>
</details>

<details open>
<summary><h2>Update OpenSSH if README requires it</h2></summary>
<br>
<pre>sudo apt upgrade openssh</pre>
</details>

<details open>
<summary><h2>Look for txt files in home directories</h2></summary>
<br>
<pre>sudo find /home -name '*.txt'</pre>
</details>

<details open>
<summary><h2>Look for mp3 files in home directories</h2></summary>
<br>
<pre>sudo find /home -name '*.mp3'</pre>
</details>

<details open>
<summary><h2>Look for image files in home directories</h2></summary>
<br>
<pre>sudo find /home -name '*.jpg'; sudo find /home -name '*.jpeg'; sudo find /home -name '*.png'</pre>
</details>

<details open>
<summary><h2>Remove hacker stuffs</h2></summary>
<br>
<pre>sudo apt purge wireshark* ophcrack* john* deluge* nmap* hydra*</pre>
</details>

<details open>
<summary><h2>Disable SSH root login</h2></summary>
<h3>Edit /etc/ssh/sshd_config</h3>
<h3>Replace:</h3>
<pre>PermitRootLogin yes</pre>
<h3>With:</h3>
<pre>PermitRootLogin no</pre>
</details>

<details open>
<summary><h1>Somewhat Useful Snippets:</h1></summary>

<h2>List all files in a directories and its subdirectories:</h2>
<pre>sudo ls -Ra *</pre>

<h2>Check for blank passwords:</h2>
<pre>sudo passwd -S $user | grep NP</pre>

<h2>List non-system users:</h2>
<pre>awk -F: '($3>=1000)&&($3<60000)&&($1!="nobody"){print $1}' /etc/passwd</pre>

<h2>Check Ports:</h2>
<pre>sudo ss -ln</pre>

<h2>Close a Port:</h2>
<pre>sudo lsof -i :$port</pre>

<h2>Find Where a Program is Located:</h2>
<pre>whereis $program</pre>

<h2>Enable Cookie Protection:</h2>
<pre>sudo sysctl -n net.ipv4.tcp_syncookies</pre>
</details>
</details>

This checklist is courtesy of WCTA in Las Vegas Nevada
