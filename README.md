# Arch-Linux-Installation-and-Configuration-Documentation
Create Your Own Virtual Machine: A Step-by-Step Walkthrough of Arch Linux Installation
<br> <br>
**Introduction**

This document outlines the process of installing and configuring Arch Linux on macOS using VirtualBox virtualization software.
The goal was to perform a complete installation of Arch Linux manually, from setting up the virtual environment to enabling a fully functional graphical user interface (GUI).
The system was also customized to include SSH, Zsh with color support, and other essential command-line enhancements.
<br> <br>

1. Virtual Machine Preparation

The setup began with preparing a virtual environment in VirtualBox.
VirtualBox was downloaded and installed from the official Oracle website, and the Archboot AARCH64 ISO was obtained from the Archboot repository, as it supports ARM-based Macs. Here is the link where you can install the Unofficial ARM-based Arch: https://release.archboot.com/aarch64/latest/iso/ 

Once installed, a new virtual machine was created with the following configuration:

Operating System: Linux (ARM 64-bit)

Memory (RAM): 8 GB

CPU Cores: 10

Disk Storage: 20 GB (Virtual Disk Image)

Boot Mode: UEFI

The Archboot ISO file was mounted, and the VM was started to launch the Arch Linux installer.
 <img width="967" height="491" alt="508808273-297b2cae-3223-4427-9042-2fa0dfa8a8f7" src="https://github.com/user-attachments/assets/a7937d60-3959-40c6-b362-4292407fe857" />

2. Launching the Arch Linux Installer
When booting the ISO, the system displayed the Archboot UEFI menu.
The default “Launch UEFI Archboot” option was selected to start the live environment.
During the guided setup:
The language and locale were chosen.


“No” was selected for the online installation mode to use the local ISO packages.

<img width="313" height="69" alt="508811137-90468b86-3a85-4281-9073-238576db0416" src="https://github.com/user-attachments/assets/3c359001-d135-4d9e-865c-b9794ef9f0d7" />

Select your timezone and region, which are configured based on the user’s location.


After these initial selections, I selected Archboot Setup to begin disk preparation.
<br> <br> <br> 
**3. Disk Partitioning and File System Setup**
<img width="522" height="283" alt="Screenshot 2025-11-03 at 2 36 41 PM" src="https://github.com/user-attachments/assets/e7a74d6f-bfa3-4ae8-ade5-5bce1b189bd2" />

I selected **“Prepare Storage Device”** menu to create and format the necessary partitions.  
I performed **Quick Setup** on `/dev/sda`, defining the following layout:

| Partition | Purpose             | File System | Size           |
|------------|---------------------|--------------|----------------|
| /dev/sda1  | EFI System Partition | FAT32        | 512 MB         |
| /dev/sda2  | Swap Space           | SWAP         | 2 GB           |
| /dev/sda3  | Root (`/`)           | ext4         | Remaining space |
| /dev/sda4  | Home (`/home`)       | ext4         | Remaining space |

All partitions were formatted accordingly, and existing data was cleared.  
This configuration ensured compatibility with **UEFI** and provided separate areas for system and user data.
<br> <br> <br>
**4. Installing Base Packages**

Once I completed the disk setup, I moved on to installing the base system packages using the built-in Archboot package installer.
From the menu, I selected “Install Packages”, and when prompted, I confirmed by choosing “Yes.”

The installer automatically began downloading and installing the essential components required for Arch Linux to function properly.
These included:

base – the core system utilities and tools

linux – the main Linux kernel

linux-firmware – firmware files for hardware compatibility

networkmanager – a network configuration tool that manages wired and wireless connections

After the installation completed, the system automatically generated the file system table (fstab).
This file defines how and where the partitions I created earlier will mount every time the system boots.
<br> <br> <br> 
Here’s that section rewritten in a **personal, natural, and professional style**, matching the tone of your previous section:

---

## **5. System Configuration**
<br> <br> <br> 
Select Configur System. 
 <img width="522" height="283" alt="Screenshot 2025-11-03 at 2 36 41 PM" src="https://github.com/user-attachments/assets/8974b166-098c-4655-91b9-daf26b220112" />

This step focused on setting up the system’s language, user accounts, and network identification so Arch Linux could run properly on my virtual machine.

I started by editing the localization and hostname files to ensure everything matched my region and system name.
Here’s what I configured:

* In **`/etc/locale.conf`**, I added:

  ```
  LANG=en_US.UTF-8
  ```

* Then, I opened **`/etc/locale.gen`** and un-commented the following line to enable the U.S. locale:

  ```
  en_US.UTF-8 UTF-8
  ```

* In **`/etc/hostname`**, becaused I installed Arch 3-4 times to gain more experience, I put different names, but make sure to remember your host name. I named my recent virtual machine:

  ```
  fayaz
  ```

* Finally, I edited **`/etc/hosts`** to properly link the hostname with the system’s network:

  ```
  127.0.1.1   fayaz.localdomain   fayaz
  ```

Once the configuration files were set, I created a **root password** to secure the system.
During setup, I chose **Zsh** as my default shell because it offers more features and flexibility than Bash.
I also created a personal user account, gave it administrator privileges, and added it to the **wheel** group so it could use `sudo` for system management commands. Choose Nano and then select BusyBox. 
 <img width="566" height="230" alt="Screenshot 2025-11-03 at 2 38 36 PM" src="https://github.com/user-attachments/assets/d6c11cc6-c7d6-45ad-80ca-753f2bbd1824" />
<img width="539" height="220" alt="Screenshot 2025-11-03 at 2 39 02 PM" src="https://github.com/user-attachments/assets/d541fe31-6cbb-423c-85b3-1be83d43e32f" />

6. Selecting Shell
   Select default shell. And as per Professor Codi's instruction, you should install a different shell other than bash, so you can either select a different shell inside the Default Shell menu, or you can install it later in the terminal. 
<img width="499" height="264" alt="Screenshot 2025-11-03 at 2 42 27 PM" src="https://github.com/user-attachments/assets/4aeddbe7-e966-4029-ae94-0dcb9095466f" />


Select ZSH, if you want to have a different Shell other than Bash.
<img width="663" height="377" alt="Screenshot 2025-11-03 at 2 42 44 PM" src="https://github.com/user-attachments/assets/c5781d60-ca02-4451-89cc-7e0b3488ce5c" />

7. Locale and Language Setup

Before installing the bootloader, I configured the system language settings.
I opened /etc/locale.conf and added:
<br> 
LANG=en_US.UTF-8
LC_COLLATE=C
<br>
<img width="222" height="106" alt="Screenshot 2025-11-03 at 2 46 51 PM" src="https://github.com/user-attachments/assets/a4e7a6d8-a97d-4ef9-9a5a-6308ebbb199c" />

<br>
Then, in /etc/locale.gen, I uncommented this line:
<br>
en_US.UTF-8 UTF-8
<br>
<img width="258" height="958" alt="Screenshot 2025-11-03 at 2 48 03 PM" src="https://github.com/user-attachments/assets/f1eb076c-28fb-4f8c-bf02-22da084e6d51" />


This enabled U.S. English with UTF-8 encoding for the system, ensuring proper text display and compatibility.

8. Bootloader Installation

After completing the system configuration, I proceeded to install the bootloader, which is responsible for initializing the operating system at startup.
From the Archboot setup menu, I selected “Install Bootloader.”

When prompted, I chose GRUB UEFI as the bootloader option. GRUB was selected because it is one of the most reliable and widely supported bootloaders available for Linux, and it works seamlessly with systems using UEFI (like my VirtualBox configuration).

During installation, I reviewed the configuration file but left all default settings unchanged to maintain compatibility with the system’s existing partition setup. This ensured that GRUB could correctly detect the EFI System Partition and load the Linux kernel without any errors.

Once the installation was complete, I exited the setup and selected “Reboot System.”
After the virtual machine restarted, the GRUB menu appeared briefly, confirming that the installation had succeeded.
The system then booted into the Arch Linux command-line interface (CLI), where I was able to log in using the credentials I had created earlier.

<img width="315" height="152" alt="508830531-2dc8bb4c-9bf0-4702-a00d-e7f58119e6ed" src="https://github.com/user-attachments/assets/08df1e24-89b4-42b1-b04e-8697fedf8080" />
<br> 
Select GRUB 
<br>
<img width="466" height="199" alt="Screenshot 2025-11-03 at 2 55 01 PM" src="https://github.com/user-attachments/assets/1d92b795-de0c-4bf3-9e91-b4a48e299832" />
<br> 
Reboot System to restart your Installation
<img width="506" height="255" alt="Screenshot 2025-11-03 at 2 56 56 PM" src="https://github.com/user-attachments/assets/1ea2a897-d498-444c-8f25-6dbccfb4b36e" />
<br> 
walaaaaaaaa........................................! 
You have successfully installed Arch Linux! (if you still didn't forget your username and password)
<img width="945" height="250" alt="Screenshot 2025-11-03 at 2 59 02 PM" src="https://github.com/user-attachments/assets/084a3f1e-48f3-466f-a704-eb276c8cffb0" />

**9. Post-Installation Configuration**

After the first successful boot, I logged into the system using the new user account I created earlier.
The first step was to verify the default shell environment. I ran:
echo $SHELL

The output confirmed that Zsh was successfully set as my default shell:
/usr/bin/zsh

This verified that my earlier configuration during installation had worked correctly.

**10. Installing and Configuring SSH**

Next, I installed and set up the SSH service to allow secure remote access to my Arch Linux system.

To install SSH, I ran:
sudo pacman -Sy openssh

Once installed, I started the service and enabled it to launch automatically at boot:
sudo systemctl start sshd
sudo systemctl enable sshd

Finally, I verified that the SSH service was running properly with:
systemctl status sshd

This confirmed that SSH was active and ready for remote connections.
<br>
<img width="1629" height="1045" alt="Screenshot 2025-11-03 at 3 11 17 PM" src="https://github.com/user-attachments/assets/a4c88ec5-8993-4396-a1ea-5f86cc12456c" />

**11. Enabling Color Output in Zsh**

To improve readability in the terminal, I enabled color support in Zsh by modifying the shell configuration file.

I opened the configuration file with: 
nano ~/.zshrc

Then, I added the following lines to enable color output and customize the shell prompt:
alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias diff='diff --color=auto'
PROMPT='%F{green}%n@%m%f:%F{blue}%~%f%# '

I made many syntax errors here, so I would definitely make sure to memorize these commands correctly. 
Now, I saved the file control + o > OK > control + x to exit the Nano
<img width="1613" height="1051" alt="Screenshot 2025-11-03 at 3 39 51 PM" src="https://github.com/user-attachments/assets/806377bb-f96e-416a-a800-8f3c1279dc83" />

To confirm that terminal color coding was properly configured, I created a test setup inside the terminal.
Since the home directory was initially empty, I created a new directory and a few sample files to verify visual output. 
mkdir test_folder
touch file1.txt file2.sh
ls --color=auto

<img width="1575" height="1023" alt="Screenshot 2025-11-03 at 4 06 09 PM" src="https://github.com/user-attachments/assets/cf8161fb-9fad-4862-bf3f-79c8bdcacce9" />

**12. Installing the GNOME Desktop Environment**

After completing the command-line configuration and verifying color support in the terminal, I decided to install a graphical user interface (GUI) to make Arch Linux easier to navigate and manage visually.

First Attempt – Installing LXQt

My first choice was the LXQt desktop environment because of its lightweight performance and low system resource usage. I installed it using the following commands:
sudo pacman -S xorg sddm lxqt
sudo systemctl enable sddm
sudo systemctl start sddm

These commands installed the X Window System (xorg), the Simple Desktop Display Manager (sddm), and the LXQt environment itself.
However, after rebooting, the system froze on the login screen and did not allow me to log in or access the terminal — even common shortcuts like Ctrl + Alt + F2 didn’t respond.

After several attempts to troubleshoot the issue, I decided to reinstall Arch Linux from scratch and repeat the entire setup process — from partitioning to configuration.
<img width="1613" height="1095" alt="Screenshot 2025-11-03 at 4 35 17 PM" src="https://github.com/user-attachments/assets/80da8847-cb13-4c15-8ddc-e0cff37c03eb" />

<bra> <bra>
**Second Attempt – Installing GNOME**

For the second installation, I switched to the GNOME desktop environment, which is known for its stability and strong integration with Arch Linux.
The installation was completed with the following commands: 
sudo pacman -S gnome
sudo pacman -S gdm
sudo systemctl enable --now gdm.service

his installed GNOME and enabled GDM (GNOME Display Manager) to launch automatically at startup.

After rebooting, the system successfully booted into the GNOME login screen, displaying my user account (“fayaz”) — confirming that the graphical environment was functioning properly and stable.
<img width="1495" height="1082" alt="Screenshot 2025-11-03 at 5 46 40 PM" src="https://github.com/user-attachments/assets/dbc403f8-b996-42ea-8247-201ceb7f25aa" />

**13. Additional Zsh Enhancements
**
To make the terminal even more efficient and easier to navigate, I added a few more helpful aliases to my Zsh configuration file. These commands made it faster to list and view directory contents while maintaining color support.

I edited the configuration file using:
nano ~/.zshrc

Then, I added the following lines:
alias la='ls -A --color=auto'
alias l='ls -CF --color=auto'

After saving the file, I reloaded the configuration to apply the changes:
source ~/.zshrc

Finally, I verified that the new aliases worked correctly — directory listings and color-coded output displayed as expected, improving both usability and readability of the terminal.
<img width="1300" height="899" alt="Screenshot 2025-11-03 at 6 46 45 PM" src="https://github.com/user-attachments/assets/719b8ee4-e650-4a09-98a5-6d78205315e6" />
