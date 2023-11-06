Read the README. Get root passwords and authorized users.

Answer forensic questions. If you need to find files use the command ```find /home -name '*' -type f``` You can change “/home” to “/” if you want to search the entire computer.

Manage users. Delete any that aren’t supposed to exist. Undisable the accounts that are supposed to exist. Make sure everyone who should be admin is admin and everyone who is supposed to be standard is standard. Add any that are needed. Make sure to unlock and re-lock. System Settings> Users and Groups > Unlock.

Look in the README for “insecure” passwords. Change those users’ passwords.

System Settings>Software&Updates have it check for recommended updates once a day.

Delete all non-work related files (If specified in readme) use: find / -name '*.<file extension>' -type f -delete Remove .mp3, .mov, .mp4, .avi, .mpg, .mpeg, .flac, .m4a, .flv, .ogg, .gif, .png, .jpg, and .jpeg.

sudo ufw enable Allow any ports in the README

sysctl -n net.ipv4.tcp_syncookies stops bad cookies.

sudo nano /etc/apt/sources.list Check for any bad sources

sudo nano /etc/hosts Check for any redirects

sudo crontab -e - check for anything in there, it might be malicious.

sudo nano /etc/lightdm/lightdm.conf and add allow-guest=false at the bottom, then do “sudo service lightdm restart” (make sure you aren’t doing any updates when you restart lightdm)

Remove hacking tools. Open Ubuntu Software center and look at recently installed software for “nmap”, “ophcrack”, or anything else that looks suspicious. If in doubt look up its name.

Remove non-work related software. Anything that looks like a game should be removed. If in doubt look it up. If you find a file called “passwords.txt” make sure to delete it.

Go to terminal and sudo apt-get update and then sudo apt-get upgrade and sudo apt-get dist-upgrade Let the apps update while you are doing other stuff.

After Updates Complete: sudo restart lightdm This gives points for editing lightdm.conf

sudo nano /etc/ssh/sshd_config and add PermitRootLogin no to the bottom. You might need to stop ssh, edit config, and restart. sudo service ssh restart

sudo nano /etc/pam.d/common-password Install sudo apt-get install libpam-cracklib and then add password requisite pam_cracklib.so minlen=10 to the end of the file.

sudo nano /etc/pam.d/common-password Use ^W and look for pam_unix.so add minlen=8 to the end of this line

sudo apt-get install bum Use bum to look for bad services. Remove apache, nginx, bind9 (DNS), ssh, or FTP unless otherwise stated in the README. Type sudo bum to start bum.

Disable samba (unless readme says otherwise) using sudo service smbd stop and sudo service samba stop (also uninstall samba too) sudo nano /etc/login.defs change/add to:
<details open>
  <summary> your wierd </summary>
    <br>
<code>
PASS_MAX_DAYS 90
PASS_MIN_DAYS 7
PASS_WARN_AGE 14
</code>
  </details>
sudo nano /etc/pam.d/common-auth Use ^W to find pam_tally2.so add deny=5 unlock_time=1800 to the end of the line. This denies password attempts and adds a lockout period.

sudo visudo Make sure only the default account can sudo.

Purge netcat. Use sudo apt-get purge netcat nc netcat-* to purge all forms of netcat.

Secure Ports. Follow these steps: sudo ss -ln | grep tcp This lists all open ports Look at the list of open ports and use sudo lsof -i :<Port> to get the program Determine if the port is a backdoor (if it has nc or netcat in the name it is a backdoor) Determine if the program is supposed to be on the computer These ports are safe: 22, 53, 631, 35509

Correct file permissions: Execute the following commands to put correct file permissions on important system files (with sudo): chmod -R 444 /var/log chmod 440 /etc/passwd chmod 440 /etc/shadow chmod 440 /etc/group chmod -R 444 /etc/ssh

Disable FTP services: Bring up a terminal, and type service --status-all and press Enter Type sudo apt-get remove pure-ftpd and press Enter. Type the password, and press enter. Hit yes, and enter.

Nmap is prohibited software. (If applicable) to remove: In the terminal, type sudo apt-get remove zenmap or sudo apt-get remove nmap and press Enter. Type the password, hit enter, then say yes and hit enter.

Other malicious software: sudo apt-get remove ophcrack This is a hacking tool. Antivirus: sudo apt-get install clamtk This installs an antivirus.

Do you hate the Ubuntu Software Center? Use this terminal command to search installed packages: sudo apt list --installed | grep <NAME>

Do you love using the command line to install and remove stuff? To install stuff: sudo apt-get install <PACKAGE NAME> To remove stuff: sudo apt-get remove <PACKAGE NAME>

This checklist is courtesy of SWCTA in Las Vegas Nevada
