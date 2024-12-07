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

1. lets switch user to root to run installations. type 
	su -
# Update and Upgrade System Packages
apt-get update -y
apt-get upgrade -y

# Install Necessary Packages
apt install sudo -y  # Install sudo
sudo --version       # Verify sudo installation

apt install vim -y   # Install vim
vim --version        # Verify vim installation

apt install git -y   # Install git
git --version        # Verify git installation

apt install openssh-server -y  # Install SSH server
systemctl status ssh           # Verify SSH installation

apt install ufw -y    # Install UFW (firewall)
ufw --version         # Verify UFW installation

apt-get install libpam-pwquality -y  # Install Password Quality Checking library

# Grant User Sudo Permissions
usermod -aG sudo your_username       # Add user to sudo group
getent group sudo                    # Verify user is in sudo group

# Edit Sudoers File for Full Permissions
vim /etc/sudoers
# Add the following under "# User privilege specification":
# your_username ALL=(ALL) ALL

# Configure UFW
ufw enable                          # Enable UFW
ufw status numbered                 # Check UFW status
ufw allow ssh                       # Allow SSH
ufw allow 4242                      # Allow port 4242
ufw status numbered                 # Verify UFW rules

# Enable Port Forwarding on VMware Fusion
sudo vim /Library/Preferences/VMware\ Fusion/vmnet8/nat.conf
# Add this under [incomingtcp]:
# 4242 = your_vm_IP_address:22
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --stop
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --start

# Configure Password Quality Checking Library
sudo vim /etc/pam.d/common-password
# Update the line to:
# password requisite pam_pwquality.so retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root

sudo vim /etc/login.defs
# Update these settings:
# PASS_MAX_DAYS 30
# PASS_MIN_DAYS 2
# PASS_WARN_AGE 7

sudo reboot  # Restart VM

# Check Password Policy for Users
sudo chage -l username
# For older users, apply policy:
sudo chage -m 2 -M 30 -W 7 username

# Configure Sudo Logs
cd /var/log
mkdir sudo
cd sudo
touch sudo.log

# Edit Sudoers for Logging
sudo vim /etc/sudoers
# Replace "Defaults" with the following:
# Defaults	env_reset
# Defaults	mail_badpass
# Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin"
# Defaults	badpass_message="Password is wrong, please try again!"
# Defaults	passwd_tries=3
# Defaults	logfile="/var/log/sudo/sudo.log"
# Defaults	log_input, log_output
# Defaults	requiretty

# Disable Root Access via SSH
sudo vim /etc/ssh/sshd_config
# Change "PermitRootLogin" from "Password Required" to "no"