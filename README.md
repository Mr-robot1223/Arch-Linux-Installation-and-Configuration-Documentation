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
