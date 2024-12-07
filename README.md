# Born2BeRoot
Born2BeRoot is a system administration project designed to introduce students to the world of virtualization and server management. The goal is to set up a virtual machine (VM) with strict system administration requirements, following specific rules and guidelines.

Core learning objectives and skills gained through the project:

- Virtualization: Create and configure virtual machines using VirtualBox or UTM.
- Server Setup: Install and secure a minimal operating system (Debian or Rocky Linux) without a graphical interface.
- System Security:
	- Enforce strong password policies.
	- Secure user privileges using sudo with logging and restrictions.
	- Implement firewalls (UFW or Firewalld) to allow only essential connections.
- Encryption and Partitioning: Configure encrypted partitions using Logical Volume Manager (LVM) for data security.
- Monitoring and Automation: Automate system status updates using bash scripting and cron jobs.
- Networking: Set up and secure SSH for remote server access on a custom port.
- Practical Knowledge: Understand core concepts like firewalls, AppArmor/SELinux, and user management while adhering to strict system rules.

Prerequisitites:

Tools required:
	VMware, VirtualBox, or bare-metal server.
	In my case I have used VMware fusion, since it's free and reliable.
Debian ISO file:
	https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/ is for 64-bit AMD/Intel processors (the amd64 architecture).
	https://cdimage.debian.org/debian-cd/current/arm64/iso-cd/ is for 64-bit ARM processors (the arm64 architecture).
	In today's guide we will be using a MAC which uses and ARM processor.

a Couple of things to note:
- Make sure you write down every username and password you will be creating. (documentation is critical in the real world)
- You can create any number of users with any names.
- The port forwarding for SSH is only required for school 42 project otherwise you can just use port 22.
- The setup can take between 30 to 50 minutes to complete.

Let's get to it:
## Setting up the Debian ISO image on VMware
1 - Open VMware and select "Install from disc or image.

https://imgur.com/ay7XIjD

2 - Select the ISO image you have downloaded then click continue.

https://imgur.com/Dvhcys6

3 - Click finish.

https://imgur.com/hknWgeI

4 - Chose where you would want to install your VM and click save.

https://imgur.com/5gKdoQV

Now your VM will launch.

## Debian Installation

1 - click on Install as shown.

https://imgur.com/q78paEf

2 - Select a language, in our case English.

https://imgur.com/iDdEh5V

3 - Chose the United States.

https://imgur.com/tEr9FvR

4 - Then chose the keyboard language.

https://imgur.com/0QWzNX2

5 - Chose a hostname, if it is for Ecole42, use your username + 42.

https://imgur.com/rFCIBaV

6 - Click enter to skip the domain name.

https://imgur.com/iWAvsXl

7 - Add a Root Password and you will be prompted to type it again. !!Make sure you write it down!!

https://imgur.com/e5gw2nM

8 - You can type a name for the new user name.

https://imgur.com/MCfXUu1

9 - Type a username for your account. !!Make sure you write it down!!

https://imgur.com/qcU2zUn

10 - Add a password then will be prompted to enter it again. !!Make sure you write it down!!

https://imgur.com/q7BxcGU

11 - Select Central

https://imgur.com/5Est90e

12 - For best security purposes and the goal of this project. Select the last option. Use entire disk and set up encrypted LVM.

https://imgur.com/MmBxikE

13 - Select the disk for partitionning

https://imgur.com/c1mFVrT

14 - select Separate /home, /var, and /tmp partitions.

https://imgur.com/5lgDfJw

15 - Click Yes.

https://imgur.com/P3YdWX5

16 - Click cancel.
! If you're working on the Born2BeRoot project for learning purposes or testing, it's okay to cancel to save time.
! For real-world applications or scenarios involving sensitive data, allow the overwriting to complete for the best security.

https://imgur.com/kWFUFMP

17 - add an encryption passphrase. !!Make sure you write it down!!

https://imgur.com/tyHlXwB 

18 - Select "max" to ensure the entire available space of the volume group is allocated.

https://imgur.com/t8DAB7y

19 - Click finish partitioning and write changes to disk

https://imgur.com/SYf18UO

20 - Select yes.

https://imgur.com/j9VR7tX

21 - Select no. 

https://imgur.com/QcmPBaA 

22 - select your country.

https://imgur.com/nO6utqC

23 - Select deb.debian.org.

https://imgur.com/ZLRcE9W

24 - Leave blank and click enter.

https://imgur.com/JtUe8Cs

25 - Since we are focusing on the project, click "No".

https://imgur.com/OOnAkfr

26 - Unselect SSH server and standard system utilities. This will allow us to customize our server the way we want.

https://imgur.com/v3Hj6C7

27 - Then click continue to finish the installation. Congrats, you were able to install Debian!!

https://imgur.com/SIt2r8j

