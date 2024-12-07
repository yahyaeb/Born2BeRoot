<div align="center">

# Born2BeRoot

<img src="https://imgur.com/OLwhOjp.png" alt="Logo" width="150">

</div>

## Table of Contents

1. [Introduction](#Born2BeRoot)
2. [Objectives](#objectives)
3. [Prerequisites](#prerequisites)
4. [Project Overview](#project-overview)
5. [System Setup](#system-setup)
6. [System Security](#system-security)
7. [Testing](#testing)
8. [Conclusion](#conclusion)
9. [Resources](#resources)


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
   ![Step 5](https://imgur.com/6mtvsNm.png)  
6. Click **Enter** to skip the domain name.  
   ![Step 6](https://i.imgur.com/iWAvsXl.png)  
7. Add a root password and confirm it. **Make sure you write it down!**  
   ![Step 7](https://i.imgur.com/e5gw2nM.png)  
8. Type a name for the new user.  
   ![Step 8](https://imgur.com/DZtcDZ5.png)  
9. Type a username for your account. **Make sure you write it down!**  
   ![Step 9](https://imgur.com/VjI501U.png)  
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
   ![Login Step](https://imgur.com/jffxekz.png)  

You are now in the VM and ready to proceed with further installations.

---

### Step 2: Update and Install Essential Packages

Run the following commands step-by-step:

1. **Switch to Root User**  
   - To run installations as root, execute: `su -`

2. **Update and Upgrade Debian**  
   - Update the system: `apt-get update -y`  
   - Upgrade the system: `apt-get upgrade -y`  

3. **Install `sudo`**  
   - Install `sudo`: `apt install sudo -y`  
   - Check the installed version: `sudo --version`  

4. **Install `vim`**  
   - Install `vim`: `apt install vim -y`  
   - Check the installed version: `vim --version`  

5. **Install `git`**  
   - Install `git`: `apt install git -y`  
   - Check the installed version: `git --version`  

6. **Install SSH Server**  
   - Install OpenSSH Server: `apt install openssh-server -y`  
   - Check the service status: `systemctl status ssh`  

7. **Install UFW (Firewall)**  
   - Install UFW: `apt install ufw -y`  
   - Check the installed version: `ufw --version`  

8. **Install Password Quality Checking Library**  
   - Install the library: `apt-get install libpam-pwquality -y`  


	
### Grant Sudo Permissions

1. **Add Your User to the `sudo` Group**  
   - Add your user to the `sudo` group: `usermod -aG sudo your_username`  
   - Verify the group membership: `getent group sudo`  

2. **Edit the `sudoers` File to Grant Full Permissions**  
   - Open the `sudoers` file: `vim /etc/sudoers`  
   - Add the following line under `# User privilege specification`:  
     ```  
     your_username ALL=(ALL) ALL  
     ```  

3. **Save and Exit**  
   - Save the changes and close the file.  


### Configure UFW

Assuming you are still working with root access, you can directly type the commands. If not, prepend each command with `sudo`.

1. **Enable UFW**  
   - Enable the firewall: `ufw enable`  

2. **Check UFW Status**  
   - View the status of UFW, including allowed rules: `ufw status numbered`  

3. **Allow SSH and Port 4242**  
   - Allow SSH access: `ufw allow ssh`  
   - Allow port 4242 (requires port forwarding configuration after this step): `ufw allow 4242`  

4. **Verify Allowed Ports**  
   - Recheck the UFW rules and allowed ports: `ufw status numbered`  



### Enable Port Forwarding on VMware Fusion Through Terminal

1. **Edit the NAT Configuration File**  
   - Open the NAT configuration file:  
     `sudo vim /Library/Preferences/VMware\ Fusion/vmnet8/nat.conf`  

2. **Add the Port Forwarding Rule**  
   - Under `[incomingtcp]`, add the following line:  
     ```  
     4242 = your_vm_IP_address:22  
     ```  

3. **Restart VMware Networking**  
   - Stop VMware networking:  
     `sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --stop`  
   - Start VMware networking:  
     `sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --start`  

   Port forwarding should now be enabled.

4. **Reboot Your VM**  
   - Reboot your virtual machine to ensure the configuration changes take effect.  

5. **Run Commands with `sudo` After Reboot**  
   - After rebooting, it is recommended to use `sudo` when running any commands to complete the configuration.  


### Configure Password Quality Policy

1. **Edit the PAM Configuration**  
   - Open the PAM configuration file:  
     `sudo vim /etc/pam.d/common-password`  

2. **Locate the Line for Password Quality**  
   - Find this line:  
     ```  
     password requisite pam_pwquality.so  
     ```  

3. **Update the Line with the Following Parameters**  
   - Add the following to the line:  
     ```  
     minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root  
     ```  

4. **Final Line Should Look Like This**  

     ` password requisite pam_pwquality.so minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root  `

5. **Save and Exit**  

6. **Edit Login Settings**  
- Open the login settings file:  
  `sudo vim /etc/login.defs`  

7. **Locate the Password Aging Section** 
- Find this section:  
  ```  
  PASS_MAX_DAYS 9999  
  PASS_MIN_DAYS 0  
  PASS_WARN_AGE 7  
  ```  

8. **Update the Section to the Following**  
```
  PASS_MAX_DAYS 30  
  PASS_MIN_DAYS 2  
  PASS_WARN_AGE 7  
```

9. **Reboot the VM**  
- Reboot the VM to apply the changes:  
  `sudo reboot`  

10. **Verify Permissions on Newly Created Users**  
 - Check password aging and restrictions for a user:  
   `sudo chage -l username`  

11. **Apply the Policy to Existing Users**  
 - If you need to update the policy for existing users, run:  
   `sudo chage -m 2 -M 30 -W 7 username`  


### Configure Sudo Logs

1. Navigate to your home directory:  
   - `cd`  

2. Go to the `/var/log` directory:  
   - `cd /var/log`  

3. Create a new directory for sudo logs:  
   - `mkdir sudo`  

4. Navigate into the newly created `sudo` directory:  
   - `cd sudo`  

5. Create the `sudo.log` file:  
   - `touch sudo.log`  

Done!


### Configure the `sudoers` File to Activate Logging

1. **Edit the `sudoers` File**  
   - Open the file:  
     `sudo vim /etc/sudoers`  

2. **Locate the Configuration Section**  
   - Look for the section that says:  
     ```  
     #See the man page for the details of how to write a sudoers file.  
     ```  

3. **Remove Existing `Defaults` Statements**  
   - Remove all pre-written `Defaults` statements in this section.

4. **Paste the Following Configuration**  
```
Defaults env_reset
Defaults mail_badpass
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin"
Defaults badpass_message="Password is wrong, please try again!"
Defaults passwd_tries=3
Defaults logfile="/var/log/sudo/sudo.log"
Defaults log_input, log_output
Defaults requiretty
```


5. **Save and Exit**  

---

### Disable Root Access Through SSH

1. **Edit the SSH Configuration File**  
- Open the SSH configuration file:  
  `sudo vim /etc/ssh/sshd_config`  

2. **Locate the `PermitRootLogin` Setting**  
- Look for the line:  
  ```  
  PermitRootLogin  
  ```  

3. **Update the Setting**  
- Change its value from `Password Required` to `no`:  
  ```  
  PermitRootLogin no  
  ```  

4. **Save and Exit**  

These steps will configure sudo logging and enhance security by disabling root access via SSH.

---

### Testing

- Verify all user accounts comply with the password policy.
- Test SSH access using a non-root user.
- Check disk partitions to ensure LVM is correctly implemented:
	`lsblk`

---

Congratulations you are now done setting up Debian as a server.

---
**Acknowledgements**

I personally made this guide, but I want to give credit to [Pasquale Rossi's Born2BeRoot Guide](https://github.com/pasqualerossi/Born2BeRoot-Guide), which was the inspiration and guide I used to complete this project.