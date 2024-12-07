# Born2BeRoot
**Born2BeRoot** is a system administration project designed as an introduction to the world of virtualization and server management. The goal is to set up a virtual machine (VM) with strict system administration requirements, following specific rules and guidelines.

### Core Learning Objectives and Skills Gained:
- **Virtualization**: Create and configure virtual machines.
- **Server Setup**: Install and secure a minimal operating system (Debian or Rocky Linux) without a graphical interface.
- **System Security**:
  - Enforce strong password policies.
  - Secure user privileges using `sudo` with logging and restrictions.
  - Implement firewalls (UFW or Firewalld) to allow only essential connections.
- **Encryption and Partitioning**: Configure encrypted partitions using Logical Volume Manager (LVM) for data security.
- **Monitoring and Automation**: Automate system status updates using Bash scripting and cron jobs.
- **Networking**: Set up and secure SSH for remote server access on a custom port.
- **Practical Knowledge**: Understand core concepts like firewalls, AppArmor/SELinux, and user management while adhering to strict system rules.

---

### Prerequisites:
#### Tools Required:
- **VMware, VirtualBox, or bare-metal server**:
  - In my case, I used VMware Fusion since it's free and reliable.
- **Debian ISO file**:
  - [64-bit AMD/Intel processors (amd64)](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
  - [64-bit ARM processors (arm64)](https://cdimage.debian.org/debian-cd/current/arm64/iso-cd/)
  - In this guide, I will use a **Mac** with an ARM processor.

---

### A Couple of Things to Note:
- Make sure to write down every username and password you create (documentation is critical in real-world scenarios).
- You can create any number of users with any names.
- Port forwarding for SSH is only required for the School 42 project; otherwise, you can use port 22.
- The setup may take between **30 to 50 minutes** to complete.

---

### Let's Get Started:
## Setting Up the Debian ISO Image on VMware
1. Open VMware and select "Install from disc or image."  
   ![Step 1](https://i.imgur.com/ay7XIjD.png)  
2. Select the ISO image you downloaded, then click **Continue.**  
   ![Step 2](https://i.imgur.com/Dvhcys6.png)  
3. Click **Finish.**  
   ![Step 3](https://i.imgur.com/hknWgeI.png)  
4. Choose where to install your VM, then click **Save.**  
   ![Step 4](https://i.imgur.com/5gKdoQV.png)  

Your VM will now launch.

---

## Debian Installation
1. Click **Install** as shown.  
   ![Step 1](https://i.imgur.com/q78paEf.png)  
2. Select a language, in our case **English.**  
   ![Step 2](https://i.imgur.com/iDdEh5V.png)  
3. Choose the **United States.**  
   ![Step 3](https://i.imgur.com/tEr9FvR.png)  
4. Select the keyboard language.  
   ![Step 4](https://i.imgur.com/0QWzNX2.png)  
5. Choose a hostname. If it is for École 42, use your username + "42".  
   ![Step 5](https://i.imgur.com/rFCIBaV.png)  
6. Click **Enter** to skip the domain name.  
   ![Step 6](https://i.imgur.com/iWAvsXl.png)  
7. Add a root password and confirm it. **Make sure you write it down!**  
   ![Step 7](https://i.imgur.com/e5gw2nM.png)  
8. Type a name for the new user.  
   ![Step 8](https://i.imgur.com/MCfXUu1.png)  
9. Type a username for your account. **Make sure you write it down!**  
   ![Step 9](https://i.imgur.com/qcU2zUn.png)  
10. Add a password and confirm it. **Make sure you write it down!**  
    ![Step 10](https://i.imgur.com/q7BxcGU.png)  
11. Select your time zone, e.g., **Central.**  
    ![Step 11](https://i.imgur.com/5Est90e.png)  
12. For best security and to meet project requirements, select **"Use entire disk and set up encrypted LVM."**  
    ![Step 12](https://i.imgur.com/MmBxikE.png)  
13. Select the disk for partitioning.  
    ![Step 13](https://i.imgur.com/c1mFVrT.png)  
14. Select **Separate /home, /var, and /tmp partitions.**  
    ![Step 14](https://i.imgur.com/5lgDfJw.png)  
15. Click **Yes** to confirm.  
    ![Step 15](https://i.imgur.com/P3YdWX5.png)  
16. Click **Cancel** to skip overwriting the disk (for learning purposes).  
    ![Step 16](https://i.imgur.com/kWFUFMP.png)  
    - *If working on a production server, allow the overwrite for better security.*  
17. Add an encryption passphrase. **Make sure you write it down!**  
    ![Step 17](https://i.imgur.com/tyHlXwB.png)  
18. Select **"max"** to allocate the entire available space to the volume group.  
    ![Step 18](https://i.imgur.com/t8DAB7y.png)  
19. Click **Finish partitioning and write changes to disk.**  
    ![Step 19](https://i.imgur.com/SYf18UO.png)  
20. Select **Yes** to confirm.  
    ![Step 20](https://i.imgur.com/j9VR7tX.png)  
21. Select **No** when prompted to scan extra installation media.  
    ![Step 21](https://i.imgur.com/QcmPBaA.png)  
22. Select your country, e.g., **France.**  
    ![Step 22](https://i.imgur.com/nO6utqC.png)  
23. Select **deb.debian.org** as the mirror.  
    ![Step 23](https://i.imgur.com/ZLRcE9W.png)  
24. Leave the proxy configuration blank and click **Enter.**  
    ![Step 24](https://i.imgur.com/JtUe8Cs.png)  
25. Click **No** to skip participation in the package usage survey.  
    ![Step 25](https://i.imgur.com/OOnAkfr.png)  
26. Unselect **SSH server** and **Standard system utilities.**  
    ![Step 26](https://i.imgur.com/v3Hj6C7.png)  
    - *This allows you to customize your server configuration from scratch.*  
27. Click **Continue** to finish the installation.  
    ![Step 27](https://i.imgur.com/SIt2r8j.png)  

**Congratulations! You’ve successfully installed Debian!**

## Installing SSH, UFW, SUDO, VIM, and Other Packages

### Step 1: Launch and Log In
1. Launch Debian and enter the encryption passphrase you set up earlier.  
   ![Launch Step](https://imgur.com/kvaZ40X.png)  

2. Enter the username and password you set up earlier. Note that the password is not visible as you type, but it is being entered.  
   ![Login Step](https://imgur.com/R7aKlCd.png)  

You are now in the VM and ready to proceed with further installations.

---

### Step 2: Update and Install Essential Packages

Run the following commands step-by-step:

1. Switch to Root User
	To run installations as root, execute: su -
2. Update and Upgrade Debian
	apt-get update -y
	apt-get upgrade -y
4. Install sudo
	apt install sudo -y
	sudo --version
5. Install vim
	apt install vim -y
	vim --version 
6. Install git
	apt install git -y
	git --version
7. Install SSH Server
	apt install openssh-server -y
	systemctl status ssh
8. Install UFW (firewall)
	apt install ufw -y
	ufw --version 
8. Install Quality Checking Library
	apt-get install libpam-pwquality -y

	
## Grant Sudo Permissions
1. Add your user to the sudo group
	usermod -aG sudo your_username
	getent group sudo
2. Edit the sudoers file to grant full permissions
	vim /etc/sudoers
Add this under # User privilege specification:
	your_username ALL=(ALL) ALL
3. then save and exit.

## Configure UFW
Assuming that we are still with root access, you can directly type the commands, otherwise start with sudo then add your commands.
1. Enable UFW
	ufw enable
2. Check UFW status
	ufw status numbered
3. Allow SSH and port 4242(port forwarding needed after this step)
	ufw allow ssh
	ufw allow 4242
4. Verify allowed ports
	ufw status numbered


## Enable Port Forwarding on VMware Fusion through Terminal:

1. Edit the NAT configuration file
	sudo vim /Library/Preferences/VMware\ Fusion/vmnet8/nat.conf
2. Add this under [incomingtcp]:
	4242 = your_vm_IP_address:22
3. Restart VMware networking
	1 - sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --stop
	2 - sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --start
port forwarding should now be enabled.

By now, I would recommend your reboot your VM to continue with configuring your VM.

After the reboot, I would recommend using sudo to run any commands to complete the configuration.

Configure Password Quality Policy

1. Edit the PAM configuration:
	sudo vim /etc/pam.d/common-password
2. Find this line 
	"password		requisite		pam_pwquality.so"
3. Add the following line to it: 
	"minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root"
4. the new line should look as follow
	"password  requisite     pam_pwquality.so  retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root"
5. save and exit
6. Edit login settings
	sudo vim /etc/login.defs
7. Find this section 
	PASS_MAX_DAYS 9999 PASS_MIN_DAYS 0 PASS_WARN_AGE 7
8. update it to 
	PASS_MAX_DAYS 30 PASS_MIN_DAYS 2 PASS_WARN_AGE 7
9. sudo reboot, to restart the VM.

To check permissions on newly created users, type the following command: 
	sudo chage -l username
Keep in mind that this password policy will apply to newly created users, if needed to update the policy on older users run the following command.
	sudo chage -m 2 -M 30 -W 7 username

## Configure Sudo Logs
1. type cd
2. cd /var/log
3. mkdir sudo
4. cd sudo
5. touch sudo.log


Let's now configure the sudoers file to activate our logs file.
1. sudo vim /etc/sudoers, then edit right below "See the man page for the details of how to write a suoders file.
remove all the "Defaults" written statements and paste the following:

Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin"
Defaults	badpass_message="Password is wrong, please try again!"
Defaults	passwd_tries=3
Defaults	logfile="/var/log/sudo/sudo.log"
Defaults	log_input, log_output
Defaults	requiretty

One more critical step is to disable Root access through SSH.
1. To do so, login to your VM
2. type sudo vim /etc/ssh/sshd_config
3. look for PermitRootLogin and change it from Password Required to no.
4. save and exit.