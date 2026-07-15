### Start VirtualBox Application

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Launch the VirtualBox application from the command line. Once installed, VirtualBox can be started using this command or found in the Kali Linux application menu.

```bash
kali@kali:~$ virtualbox
kali@kali:~$ 

```

--------------------------------

### List Kali Examples in cryptmypi

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Lists available example configurations for Kali Linux within the cryptmypi script's examples directory. This helps users identify pre-configured setups for their needs.

```bash
kali@kali:~$ ls -aFl examples/ | grep kali

```

--------------------------------

### Install Instaloader using pip

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This command demonstrates the basic installation of the Instaloader package using pip, the Python package installer. It's a straightforward way to get the application running if Python and pip are already configured.

```bash
pip3 install instaloader
```

--------------------------------

### Build Test Kernel Installer

Source: https://www.kali.org/docs/nethunter/porting-nethunter-kernel-builder

This snippet initiates the kernel building process using the 'build.sh' script. It involves selecting environment setup and kernel configuration/compilation options.

```bash
./build.sh
```

--------------------------------

### Install LXD and Initialize on Ubuntu Host

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Installs the LXD snap package and performs the initial setup for LXD on an Ubuntu host. This is the first step to launching Kali Linux containers.

```bash
kali@kali:~$ sudo snap install lxd
kali@kali:~$ lxd init

```

--------------------------------

### Install virt-manager for Kali VM Setup

Source: https://www.kali.org/docs/virtualization/install-qemu-guest-vm

Installs the virt-manager package, which provides a graphical interface for managing KVM/QEMU virtual machines. This command is run on the host Debian-based system to prepare for VM creation. It ensures all necessary dependencies for virt-manager are fetched and installed.

```bash
sudo apt update && sudo apt install virt-manager -y
```

--------------------------------

### Download and Execute Xfce4 Setup Script

Source: https://www.kali.org/docs/general-use/xfce-with-rdp

This sequence of commands downloads the xfce4.sh script from a GitLab repository, makes it executable, and then runs it with superuser privileges. This is a convenient way to perform the RDP and Xfce setup, especially within a Docker environment where initial package installations might be required.

```shell
# If on Docker, run the following command first before continuing:
root@182156129:/$ apt update && DEBIAN_FRONTEND=noninteractive apt install -y wget kali-linux-headless

kali@kali:~$ wget https://gitlab.com/kalilinux/recipes/kali-scripts/-/raw/main/xfce4.sh
kali@kali:~$ 
kali@kali:~$ chmod +x xfce4.sh
kali@kali:~$ 
kali@kali:~$ sudo ./xfce4.sh
kali@kali:~$ 

```

--------------------------------

### Setup Kali Build Environment

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Installs necessary packages like git, live-build, simple-cdd, cdebootstrap, and curl, then clones the Kali live-build-config repository. This prepares the system for building custom Kali ISO images.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y git live-build simple-cdd cdebootstrap curl
kali@kali:~$ 
kali@kali:~$ git clone https://gitlab.com/kalilinux/build-scripts/live-build-config.git

```

--------------------------------

### Run an Installed Python Application

Source: https://www.kali.org/docs/general-use/python3-external-packages

Shows how to execute a Python application that has been installed via pipx. The example displays the help message for the 'xsstrike' tool, indicating successful installation and availability.

```bash
xsstrike -h
usage: xsstrike [-h] [-u target] [--data paramdata] [-e encode] [--fuzzer]
                [--update] [--timeout timeout] [--proxy] [--crawl] [--json]
                [--path] [--seeds args_seeds] [-f args_file] [-l level]
                [--headers [add_headers]] [-t threadcount] [-d delay]
                [--skip] [--skip-dom] [--blind]
                [--console-log-level {debug,info,run,good,warning,error,critical,vuln}]
                [--file-log-level {debug,info,run,good,warning,error,critical,vuln}]
                [--log-file log_file] [-n payload_count]
[...]
```

--------------------------------

### Install and Enable Cloud-Init for DigitalOcean

Source: https://www.kali.org/docs/cloud/digitalocean

Installs the cloud-init package, configures it to use DigitalOcean's data sources, and enables the cloud-init service to start on boot. Cloud-init is essential for cloud instance initialization.

```bash
kali@kali:~$ sudo apt install -y cloud-init
kali@kali:~$ sudo sh -c "echo 'datasource_list: [ ConfigDrive, DigitalOcean, NoCloud, None ]' > /etc/cloud/cloud.cfg.d/99_digitalocean.cfg"
kali@kali:~$ sudo systemctl enable cloud-init --now
```

--------------------------------

### Start Nexmon Monitor Mode

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This sequence of commands disables Wi-Fi, brings up the wlan0 interface, and starts Nexmon in monitor mode with specific settings. It requires root privileges and the Nexmon module to be installed.

```bash
$ svc wifi disable
$ ifconfig wlan0 up
$ nexutil -s0x613 -i -v2
```

--------------------------------

### Example Kali Linux Pre-seed Configuration (Debian Installer)

Source: https://www.kali.org/docs/installation/network-pxe

This is an example of a pre-seed file used for automating the Kali Linux installation process via PXE. It specifies package selections, user information, and locale settings. Lines can be commented out to enable manual prompts for specific configurations.

```text
kali@kali:~$ cat <<'EOF' | sudo tee /opt/pxe/preseed.cfg
# Package selection
d-i pkgsel/include string kali-linux-default kali-desktop-xfce

# User information
d-i passwd/user-fullname string kali
d-i passwd/username string kali
d-i passwd/user-password password kali
d-i passwd/user-password-again password kali

EOF
```

--------------------------------

### Initialize Metasploit Database with msfdb init (Shell)

Source: https://www.kali.org/docs/tools/starting-metasploit-framework-in-kali

This command initializes the Metasploit Framework's PostgreSQL database. It starts the database service, creates the 'msf' user and databases, generates a configuration file, and sets up the initial database schema. This is a quick way to get the database ready for use.

```shell
kali@kali:~$ sudo msfdb init
[+] Starting database
[+] Creating database user 'msf'
[+] Creating databases 'msf'
[+] Creating databases 'msf_test'
[+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml'
[+] Creating initial database schema
kali@kali:~$ 

```

--------------------------------

### Start PostgreSQL Service for Metasploit (Shell)

Source: https://www.kali.org/docs/tools/starting-metasploit-framework-in-kali

This command starts the PostgreSQL service, which is required by the Metasploit Framework. It ensures that the database backend is running before attempting to initialize or connect to it.

```shell
kali@kali:~$ sudo msfdb start
[+] Starting database
kali@kali:~$ 

```

--------------------------------

### Mounting and Chrooting into Target System (Shell)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This snippet demonstrates how to mount essential system directories and then chroot into the target installation directory. This is a crucial step before installing system packages or making configuration changes to the new system. It ensures that subsequent commands operate within the context of the newly installed system.

```shell
$ for n in dev proc sys run etc/resolv.conf; do mount --bind /$n /target/$n; done
$ chroot /target
$ mount -a

```

--------------------------------

### Configure Package Management Actions

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Specifies packages to be purged and installed during the Kali Linux setup. This example shows installing `tree` and `htop`.

```bash
export _PKGSPURGE=""
export _PKGSINSTALL="tree htop"
```

--------------------------------

### Start RDP Service

Source: https://www.kali.org/docs/general-use/xfce-with-rdp

This command starts the xrdp service. The method for starting the service differs based on the environment. For AWS instances, 'systemctl enable xrdp --now' is used to ensure it starts on boot and is running. For WSL and Docker, the older '/etc/init.d/xrdp start' script is used.

```shell
# If on AWS
kali@kali:~$ sudo systemctl enable xrdp --now
kali@kali:~$ 

# If on WSL or Docker
kali@kali:~$ sudo /etc/init.d/xrdp start
kali@kali:~$ 

```

--------------------------------

### Install VirtualBox from Kali Repositories

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Install VirtualBox and the generic Linux headers directly from the Kali Linux repositories. This is a straightforward method for getting VirtualBox up and running.

```bash
kali@kali:~$ sudo apt update
[...]
kali@kali:~$ 
kali@kali:~$ sudo apt install virtualbox linux-headers-generic
[...]
kali@kali:~$ 

```

--------------------------------

### Debian Photon Install File Configuration

Source: https://www.kali.org/docs/development/intermediate-packaging-example

Defines which files to install and their destination directories within the package. It copies core files, plugins, the main script, and the helper script to their respective locations.

```install
core usr/share/photon/
plugins usr/share/photon/
photon.py usr/share/photon/
debian/helper-script/photon usr/bin/
```

--------------------------------

### Running x86 Executables After QEMU Installation

Source: https://www.kali.org/docs/arm/x86-on-arm

This example shows the process of attempting to run an x86 executable (PowerShell in this case) before and after installing qemu-user-static. Initially, it fails with an 'exec format error'. After the QEMU installation, the same executable runs successfully, demonstrating the emulation capability.

```bash
# Before qemu-user-static install
kali@kali:~$ sudo dpkg --add-architecture amd64
kali@kali:~$ 
kali@kali:~$ sudo apt install -y powershell
kali@kali:~$ 
kali@kali:~$ file /opt/microsoft/powershell/7/pwsh
/opt/microsoft/powershell/7/pwsh: ELF 64-bit LSB pie executable, x86-64, version 1 (GNU/Linux), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=9c3feab2531f770c71d023f031faf37758181701, stripped
kali@kali:~$ 
kali@kali:~$ pwsh
zsh: exec format error: pwsh
kali@kali:~$ 
# After qemu-user-static install
kali@kali:~$ sudo apt install -y qemu-user-static binfmt-support
kali@kali:~$ 
kali@kali:~$ pwsh
PowerShell 7.1.3
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.


┌──(kali㉿kali)-[/home/kali]
└─PS> 

```

--------------------------------

### Build Kali Nethunter Installer from Source

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This section outlines the steps to clone the kali-nethunter-installer repository, set it up, and build a full installer for specific LineageOS versions. Dependencies include git and the build scripts.

```bash
# Clone and setup kali-nethunter-installer
$ git clone https://gitlab.com/kalilinux/nethunter/build-scripts/kali-nethunter-installer.git
$ cd kali-nethunter-installer
$ ./bootstrap.sh
[?] Would you like to grab the full history of kernels? (y/N):
[?] Would you like to use SSH authentication (faster, but requires a GitLab account with SSH keys)? (y/N): N
[i] Running command: git clone --depth 1 https://gitlab.com/kalilinux/nethunter/build-scripts/kali-nethunter-kernels.git kernels
Cloning into 'kernels'...

# Build full installer
## LOS 21
$ ./build.py -k beyond1lte-los -14 -fs full
## LOS 22.2
$ ./build.py -k beyond1lte-los -15 -fs full
## LOS 23.0
$ ./build.py -k beyond1lte-los -16 -fs full
```

--------------------------------

### Start and Access Kali Linux VM with Vagrant

Source: https://www.kali.org/docs/virtualization/install-vagrant-guest-vm

This section demonstrates how to start a Kali Linux VM using Vagrant and then SSH into it. The 'vagrant up' command downloads the specified box if not found and boots the virtual machine. 'vagrant ssh' allows you to connect to the running VM via SSH. The output shows the VM booting process and successful connection.

```bash
kali@kali:~/vagrant$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'kalilinux/rolling' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'kalilinux/rolling'
    default: URL: https://vagrantcloud.com/kalilinux/rolling
==> default: Adding box 'kalilinux/rolling' (v2025.2.1) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/kalilinux/boxes/rolling/versions/2025.2.1/providers/virtualbox.box
==> default: Successfully added box 'kalilinux/rolling' (v2025.2.1) for 'virtualbox'!
[...]
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /home/morales/vagrant

kali@kali:~/vagrant$

kali@kali:~/vagrant$ vagrant ssh
Linux kali 5.16.0-kali7-amd64 #1 SMP PREEMPT Debian 5.16.18-1kali1 (2022-04-01) x86_64

The programs included with the Kali GNU/Linux system are free software; 
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
kali@kali:~$ 
kali@kali:~$ exit

kali@kali:~/vagrant$

```

--------------------------------

### Enable and Start snapd Services

Source: https://www.kali.org/docs/tools/snap

Enables and starts the snapd and snapd.apparmor services using systemctl. This ensures that snapd runs automatically on boot and is active.

```bash
sudo systemctl enable --now snapd apparmor
```

--------------------------------

### Start VNC Server (Bash)

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This command starts a VNC server on display :1. It allows remote access to a graphical desktop session. Ensure the VNC server is installed and configured before running this command.

```bash
vncserver :1
```

--------------------------------

### Copy and Edit Kernel Configuration

Source: https://www.kali.org/docs/nethunter/porting-nethunter-kernel-builder

This section covers copying an example configuration file to 'local.config' and then editing it to match your device's kernel specifications. This step is crucial for a successful build.

```bash
kali@kali:~$ cp local.config.examples/CONFIG_YOU_WANT local.config
kali@kali:~$ nano local.config
```

--------------------------------

### Install pyenv using the official script

Source: https://www.kali.org/docs/general-use/using-eol-python-versions

Downloads and executes the official pyenv installation script to install pyenv. This is a convenient way to get pyenv set up on your system.

```bash
kali@kali:~$ curl https://pyenv.run | bash
[...]
kali@kali:~$
```

--------------------------------

### Install Mali Driver (Shell)

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Completes the installation of the Mali driver by running the make and make install commands. This step finalizes the driver setup on the system.

```shell
kali@kali:~$ make
kali@kali:~$ make install
```

--------------------------------

### Install and Verify Hashcat with CUDA

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

Installs Hashcat using apt and verifies its integration with CUDA and OpenCL devices. This step ensures that the system recognizes the GPU for accelerated computations.

```bash
kali@kali:~$ sudo apt install -y hashcat
kali@kali:~$ 
kali@kali:~$ hashcat -I
hashcat (v6.0.0) starting...

CUDA Info:
==========

CUDA.Version.: 10.2

Backend Device ID #1 (Alias: #2)
  Name...........: GeForce GTX 1060 6GB
  Processor(s)...: 10
  Clock..........: 1771
  Memory.Total...: 6075 MB
  Memory.Free....: 5908 MB

OpenCL Info:
============

OpenCL Platform ID #1
  Vendor..: NVIDIA Corporation
  Name....: NVIDIA CUDA
  Version.: OpenCL 1.2 CUDA 10.2.185

  Backend Device ID #2 (Alias: #1)
    Type...........: GPU
    Vendor.ID......: 32
    Vendor.........: NVIDIA Corporation
    Name...........: GeForce GTX 1060 6GB
    Version........: OpenCL 1.2 CUDA
    Processor(s)...: 10
    Clock..........: 1771
    Memory.Total...: 6075 MB (limited to 1518 MB allocatable in one block)
    Memory.Free....: 5888 MB
    OpenCL.Version.: OpenCL C 1.2
    Driver.Version.: 440.100

kali@kali:~$
```

--------------------------------

### Install and Enable SSH Server

Source: https://www.kali.org/docs/cloud/digitalocean

Installs the OpenSSH server package, enables the SSH service to start on boot, and prepares the system for remote SSH access. This is crucial for managing the droplet after deployment.

```bash
kali@kali:~$ sudo apt install -y openssh-server
kali@kali:~$ sudo systemctl enable ssh.service --now
```

--------------------------------

### Install and Use clinfo for Troubleshooting

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

Installs the 'clinfo' utility, which provides detailed information about OpenCL platforms and devices. This is useful for diagnosing issues related to OpenCL driver or hardware compatibility.

```bash
kali@kali:~$ sudo apt install -y clinfo
kali@kali:~$ 
kali@kali:~$ clinfo
Number of platforms                               1
  Platform Name                                   NVIDIA CUDA
  Platform Vendor                                 NVIDIA Corporation
  Platform Version                                OpenCL 1.2 CUDA 10.1.120
  Platform Profile                                FULL_PROFILE
  Platform Extensions                             cl_khr_global_int32_base_atomics cl_khr_global_int32_extended_atomics cl_khr_local_int32_base_atomics cl_khr_local_int32_extended_atomics cl_khr_fp64 cl_khr_byte_addressable_store cl_khr_icd cl_khr_gl_sharing cl_nv_compiler_options cl_nv_device_attribute_query cl_nv_pragma_unroll cl_nv_copy_opts cl_nv_create_buffer
  Platform Extensions function suffix             NV

  Platform Name                                   NVIDIA CUDA
[...]
kali@kali:~$ 
kali@kali:~$ clinfo | wc -l
116
kali@kali:~$
```

--------------------------------

### Install Dependencies and Kali Packages (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Installs essential build dependencies and then installs the previously downloaded Kali archive keyring and live-build .deb packages.

```bash
$ sudo apt install -y git live-build simple-cdd cdebootstrap curl
$
$ sudo dpkg -i kali-archive-keyring_2022.1_all.deb
$ sudo dpkg -i live-build_20230502+kali3_all.deb
```

--------------------------------

### Install Kali Linux AppxBundle (PowerShell)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This PowerShell script downloads the Kali Linux AppxBundle and then adds it as an installed application. This method is an alternative to installing directly from the Microsoft Store.

```powershell
Invoke-WebRequest -Uri https://aka.ms/wsl-kali-linux-new -OutFile .\kali-linux.AppxBundle -UseBasicParsing -TimeoutSec 1800
Add-AppxPackage .\kali-linux.AppxBundle
```

--------------------------------

### Install Kali WSL using wsl --install

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command installs WSL and Kali Linux. It enables necessary Windows features like Virtual Machine Platform and Windows Subsystem for Linux, installs the WSL kernel, and downloads the Kali Linux Rolling distribution. This method is straightforward but may install an outdated Kali version on Windows 10 builds before November 2022.

```bash
wsl --install --distribution kali-linux
```

--------------------------------

### Analyze Kali Linux Installation Debug Logs

Source: https://www.kali.org/docs/troubleshooting/troubleshooting-a-kali-linux-install

This snippet shows an example of debug logs from a failed Kali Linux installation. It highlights error messages related to insufficient disk space and tar process failures. Analyzing these logs is crucial for diagnosing installation problems.

```text
Aug 19 23:45:05 base-installer: error: The tar process copying the live system failed (only 152937 out of 286496 files have been copied, last file was ).
Aug 19 23:45:05 main-menu[927]: (process:7553): tar: write error: No space left on device
Aug 19 23:45:05 main-menu[927]: WARNING **: Configuring 'live-installer' failed with error code 1
Aug 19 23:45:05 main-menu[927]: WARNING **: Menu item 'live-installer' failed.
Aug 19 23:50:23 main-menu[927]: INFO: Modifying debconf priority limit from 'high' to 'medium'
Aug 19 23:50:23 debconf: Setting debconf/priority to medium
Aug 19 23:56:49 main-menu[927]: INFO: Menu item 'save-logs' selected

```

--------------------------------

### Install Required Tools for Kali ARM Build

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Installs essential tools like debootstrap and qemu-user-static required for building a Kali Linux ARM image. This is a one-time setup task.

```bash
kali@kali:~$ sudo apt install -y debootstrap qemu-user-static

```

--------------------------------

### Setting up LUKS Encryption on USB Partitions

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This section details the process of setting up LUKS (Linux Unified Key Setup) encryption on specific partitions of the USB drive. It uses the `cryptsetup` command to format partitions with LUKS1 for compatibility with the boot loader and then opens these encrypted partitions.

```bash
$ sudo cryptsetup luksFormat --type=luks1 /dev/sda1
$ sudo cryptsetup luksFormat /dev/sda4
$ sudo cryptsetup luksFormat /dev/sda5

$ sudo cryptsetup open /dev/sda1 LUKS_BOOT
$ sudo cryptsetup open /dev/sda4 LUKS_SWAP
$ sudo cryptsetup open /dev/sda5 LUKS_ROOT
```

--------------------------------

### Debian Test Control File Example

Source: https://www.kali.org/docs/development/contributing-runtime-tests

An example of a debian/tests/control file demonstrating test definitions, dependencies, and restrictions. This file specifies test scripts and their requirements.

```text
Tests: fred, bill, bongo
Depends: pkg1, pkg2 [amd64] | pkg3 (>= 3)
Restrictions: needs-root, breaks-testbed

```

--------------------------------

### Install Kali Linux on WSL using wsl --install

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command installs Kali Linux directly on WSL. It downloads and sets up the distribution, prompting the user to create a UNIX username and password. Note that older Windows 10 versions might install an outdated Kali version.

```bash
C:\Users\Win>wsl --install --distribution kali-linux
Downloading: Kali Linux Rolling
Installing: Kali Linux Rolling
Kali Linux Rolling has been installed.
Launching Kali Linux Rolling...

C:\Users\Win>

Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: kali
New password:
Retype new password:
passwd: password updated successfully
Installation successful!
kali@DESKTOP-AJVAG8O:~$ uname -a
Linux DESKTOP-AJVAG8O 5.10.16.3-microsoft-standard-WSL2 #1 SMP Fri Apr 2 22:23:49 UTC 2021 x86_64 GNU/Linux
kali@DESKTOP-AJVAG8O:~$ id
uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev)
kali@DESKTOP-AJVAG8O:~$ grep VERSION= /etc/*release
/etc/os-release:VERSION="2019.2"
kali@DESKTOP-AJVAG8O:~$
```

--------------------------------

### Install mesa-utils (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command installs the 'mesa-utils' package, which provides utilities like `glxinfo`. This package is necessary for checking OpenGL and 3D rendering capabilities on the system.

```bash
kali@kali:~$ sudo apt install -y mesa-utils
kali@kali:~$
```

--------------------------------

### Install Kernel Headers and Build Tools for NVIDIA Driver

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

Installs the necessary kernel headers and build tools (kbuild infrastructure) required for compiling out-of-tree kernel modules, such as the NVIDIA driver. This is a prerequisite for a successful NVIDIA driver installation.

```bash
kali@kali:~$ sudo apt install -y linux-headers-amd64
kali@kali:~$ 

```

--------------------------------

### Python Pip Test Control File Examples

Source: https://www.kali.org/docs/development/contributing-runtime-tests

Examples of debian/tests/control files for 'python-pip' tests, demonstrating the use of multiple 'Tests' entries with different restrictions.

```text
Tests: pip3-root.sh
Restrictions: needs-root

Tests: pip3-user.sh
Restrictions: breaks-testbed

```

--------------------------------

### Install LXD and Launch Kali GUI Container on Ubuntu

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Installs LXD via snap, creates a GUI profile, and launches a Kali GUI container. This involves downloading a profile script, creating an LXC profile, and then launching the container with the specified profiles.

```bash
kali@kali:~$ sudo snap install lxd
kali@kali:~$ lxd init
kali@kali:~$ wget https://blog.simos.info/wp-content/uploads/2018/06/lxdguiprofile.txt
kali@kali:~$ lxc profile create gui
kali@kali:~$ cat lxdguiprofile.txt | lxc profile edit gui
kali@kali:~$ lxc profile list
kali@kali:~$ lxc launch --profile default --profile gui images:kali/current/amd64    gui-kali
```

--------------------------------

### Install VMware Modules via vmware-modconfig (Bash)

Source: https://www.kali.org/docs/virtualization/install-vmware-host

This command attempts to install all necessary VMware kernel modules. It's a troubleshooting step when VMware fails to start. The output can be redirected to grep for specific error messages.

```bash
kali@kali:~$ sudo vmware-modconfig --console --install-all
kali@kali:~$ sudo vmware-modconfig --console --install-all 2>&1 | grep error
```

--------------------------------

### Import and Apply Patches with gbp pq

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet demonstrates the command-line process for importing and applying patches using the `gbp pq` tool. It shows the output of importing patches and switching between branches, indicating the status of patch application.

```bash
kali@kali:~/kali/packages/finalrecon$ gbp pq import
gbp:info: Trying to apply patches at 'f1c4c9f8d25224186749ce69a9f403f207feda03'
gbp:info: 0 patches listed in 'debian/patches/series' imported on 'patch-queue/kali/master'
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ gbp pq export
gbp:info: On 'patch-queue/kali/master', switching to 'kali/master'
gbp:info: Generating patches from git (kali/master..patch-queue/kali/master)
kali@kali:~/kali/packages/finalrecon$
```

--------------------------------

### Kali Linux Preseed Configuration Options

Source: https://www.kali.org/docs/installation/network-pxe

A collection of debconf preseeding options for automating the Kali Linux installation process. These options cover various aspects of the installation, including locale, keyboard, disk partitioning, network configuration, package selection, and user setup.

```debian-preseed
# Region Information
d-i time/zone string US/Eastern
d-i debian-installer/locale string en_US
d-i debian-installer/language string en
d-i debian-installer/country string US
d-i debian-installer/locale string en_US.UTF-8
d-i keyboard-configuration/xkb-keymap select us

# Hard drive
d-i grub-installer/bootdev string /dev/sda

d-i netcfg/get_hostname string kali
d-i netcfg/get_domain string unnasigned-domain
tasksel tasksel/first multiselect standard
d-i mirror/country string enter information manually
d-i mirror/suite string kali-rolling
d-i mirror/codename string kali-rolling
d-i mirror/http/hostname string http.kali.org
d-i mirror/http/directory string /kali
d-i mirror/http/proxy string
d-i partman-auto/method string regular
d-i partman-auto-lvm/guided_size string max
d-i partman-auto/choose_recipe select atomic
d-i partman-partitioning/confirm_write_new_label boolean true
d-i partman/choose_partition select finish
d-i partman/confirm boolean true
d-i partman/confirm_nooverwrite boolean true
d-i partman-md/confirm boolean true
d-i partman-partitioning/confirm_write_new_label boolean true
d-i partman/choose_partition select finish
d-i partman/confirm boolean true
d-i partman/confirm_nooverwrite boolean true
d-i grub-installer/only_debian boolean true
d-i grub-installer/with_other_os boolean true
d-i finish-install/reboot_in_progress note
d-i apt-setup/services-select multiselect
d-i apt-setup/non-free boolean true
d-i apt-setup/contrib boolean true
d-i apt-setup/disable-cdrom-entries boolean true
d-i apt-setup/enable-source-repositories boolean false
d-i pkgsel/upgrade select full-upgrade
d-i passwd/root-login boolean false
d-i preseed/early_command string anna-install eatmydata-udeb
d-i pkgsel/update-policy select none
popularity-contest popularity-contest/participate boolean false
encfs encfs/security-information boolean true
encfs encfs/security-information seen true
console-setup console-setup/charmap47 select UTF-8
samba-common samba-common/dhcp boolean false
macchanger macchanger/automatically_run boolean false
kismet-capture-common kismet-capture-common/install-users string
kismet-capture-common kismet-capture-common/install-setuid boolean true
wireshark-common wireshark-common/install-setuid boolean true
sslh sslh/inetd_or_standalone select standalone
atftpd atftpd/use_inetd boolean false
```

--------------------------------

### Configure Kali Tweaks for Hardening

Source: https://www.kali.org/docs/installation/barebone-kali

This command launches the 'kali-tweaks' utility, which allows users to configure various system settings and hardening options. The guide specifically recommends unchecking options within the 'Hardening' section to enhance system security for daily use.

```shell
kali@kali:~$ kali-tweaks

```

--------------------------------

### Specify Files for Installation in debian/finalrecon.install

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet lists the files and directories to be installed on the system when the FinalRecon package is unpacked. It ensures that configuration files, the main script, modules, and wordlists are placed in the correct system directory.

```text
conf usr/share/finalrecon/
finalrecon.py usr/share/finalrecon/
modules usr/share/finalrecon/
wordlists usr/share/finalrecon/
```

--------------------------------

### Create and Edit Custom Kernel Configuration

Source: https://www.kali.org/docs/nethunter/porting-nethunter-kernel-builder

This snippet demonstrates creating a custom 'local.config' file by copying a generic 'config' and then editing it. It's a recommended approach for devices not listed in examples.

```bash
kali@kali:~$ cp config local.config
kali@kali:~$ nano local.config
```

--------------------------------

### Add Unattended Installation Preseed File to Kali ISO

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This snippet adds a preseed file for unattended Kali installations. It downloads a pre-configured preseed file and saves it as `preseed.cfg` within the `kali-config/common/debian-installer/` directory, enabling automated setup.

```bash
kali@kali:~$ mkdir -pv kali-config/common/debian-installer/
kali@kali:~$ wget https://gitlab.com/kalilinux/recipes/kali-preseed-examples/-/raw/main/kali-linux-full-unattended.preseed -O kali-config/common/debian-installer/preseed.cfg

```

--------------------------------

### Start XFCE Desktop Environment (Bash)

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This command initiates the XFCE desktop environment. It's commonly used in VNC startup scripts or local X session configurations to launch the XFCE graphical interface.

```bash
startxfce4 &
```

--------------------------------

### NetHunter Command Line Interface (Shell)

Source: https://www.kali.org/docs/nethunter/nethunter-rootless

Provides commands to interact with the NetHunter environment, including starting the CLI, configuring and starting the KeX desktop experience, and running commands within NetHunter, with options for both standard and root access.

```shell
# Start Kali NetHunter command line interface
nethunter

# Configure KeX password (first use)
nethunter kex passwd

# Start Kali NetHunter Desktop Experience
nethunter kex &

# Stop Kali NetHunter Desktop Experience
nethunter kex stop

# Run a command in NetHunter environment
nethunter <command>

# Start Kali NetHunter CLI as root
nethunter -r

# Configure KeX password for root
nethunter -r kex passwd

# Start Kali NetHunter Desktop Experience as root
nethunter -r kex &

# Stop Kali NetHunter Desktop Experience root sessions
nethunter -r kex stop

# Kill all KeX sessions
nethunter -r kex kill

# Run a command in NetHunter environment as root
nethunter -r <command>

# Abbreviated command
nh

```

--------------------------------

### Execute Guacamole Standalone Installation Script

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This command executes the Guacamole installation script with specific parameters for a standalone setup. It disables multi-factor authentication (--nomfa), enables MySQL installation (--installmysql), and sets custom passwords for MySQL (--mysqlpwd) and Guacamole (--guacpwd).

```bash
kali@kali:~$ cd /tmp/guac-install/
kali@kali:/tmp/guac-install$ sudo ./guac-install.sh --nomfa --installmysql --mysqlpwd S3cur3Pa$$w0rd --guacpwd P@s$W0rD
[...] 
Cleanup install files...

Installation Complete
- Visit: http://localhost:8080/guacamole/
- Default login (username/password): guacadmin/guacadmin
***Be sure to change the password***.
kali@kali:/tmp/guac-install$ 

```

--------------------------------

### Start Metasploit Services (Bash)

Source: https://www.kali.org/docs/nethunter/testing-checklist

This command sequence starts the PostgreSQL database and Metasploit services, essential for running Metasploit Framework. Ensure these services are running before attempting to use Metasploit.

```bash
service postgresql start && service metasploit start
```

--------------------------------

### Install LXC and Configure Network on Kali Host

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Installs LXC and related networking packages, then configures the default LXC network settings using a heredoc to define bridge and apparmor configurations. It also starts and enables the default virtual network.

```bash
kali@kali:~$ sudo apt install -y lxc libvirt0 libpam-cgfs bridge-utils libvirt-clients libvirt-daemon-system iptables ebtables dnsmasq-base
kali@kali:~$ 
kali@kali:~$ sudo cat <<EOF > /etc/lxc/default.conf
lxc.net.0.type = veth
lxc.net.0.link = virbr0
lxc.net.0.flags = up
lxc.apparmor.profile = generated
lxc.apparmor.allow_nesting = 1
EOF
kali@kali:~$ 
kali@kali:~$ sudo virsh net-start default
kali@kali:~$ sudo virsh net-autostart default
```

--------------------------------

### Installing GRUB2 and Cryptsetup Packages (Debian/Ubuntu)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Installs the necessary packages for GRUB2 bootloader management and cryptsetup-initramfs for handling encrypted devices during the initramfs stage. These packages are essential for booting a system with encrypted partitions, particularly the boot partition.

```shell
$ apt-get install grub-common grub-efi-amd64 os-prober
$ apt-get install cryptsetup-initramfs

```

--------------------------------

### Create Initrd and Boot Image

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This snippet guides through creating an initial RAM disk (initrd) and a bootable image for the ODROID. It involves chrooting into the root filesystem, installing necessary tools, generating the initrd using mkinitramfs with LZMA compression, and then creating the 'uInitrd' file using mkimage. The kernel version needs to be adjusted for the 'mkinitramfs' command.

```bash
kali@kali:~$ LANG=C chroot ~/arm-stuff/images/root/
kali@kali:~$ sudo apt install -y initramfs-tools uboot-mkimage
kali@kali:~$ cd /
kali@kali:~$ # Change the example "3.8.13" to your current odroid kernel revision
kali@kali:~$ mkinitramfs -c lzma -o ./initramfs 3.8.13
kali@kali:~$ mkimage -A arm -O linux -T ramdisk -C none -a 0 -e 0 -n initramfs -d ./initramfs ./uInitrd
kali@kali:~$ rm initramfs
kali@kali:~$ exit

```

--------------------------------

### Build Kali Installer ISO

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Builds a Kali Installer ISO image by running the build.sh script with both --verbose and --installer flags. This command generates an installer image instead of the default live image, providing customization options during installation.

```bash
kali@kali:~/live-build-config$ ./build.sh --verbose --installer

```

--------------------------------

### Install Git and Clone Guacamole Installer Script

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This snippet demonstrates how to update package lists, install the Git version control system, and clone the Guacamole installation script from GitHub to a temporary directory. This is the first step in setting up Guacamole.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt install -y git
kali@kali:~$ 
kali@kali:~$ git clone https://github.com/MysticRyuujin/guac-install.git /tmp/guac-install
kali@kali:~$ 

```

--------------------------------

### Install Snapper and Related Tools on Kali Linux

Source: https://www.kali.org/docs/installation/btrfs

Installs essential tools for BTRFS snapshotting on Kali Linux, including snapper, snapper-gui, and grub-btrfs. This enables automatic snapshot creation and integration with the GRUB boot menu.

```bash
# Set a secure root password or you'll struggle to log into a recovery shell
$ sudo passwd

# Install some essential tools
$ sudo apt update && sudo apt install btrfs-progs snapper snapper-gui grub-btrfs

# Create the snapper configuration for the root filesystem "/"
$ sudo cp /usr/share/snapper/config-templates/default /etc/snapper/configs/root
$ sudo sed -i 's/^SNAPPER_CONFIGS=""/SNAPPER_CONFIGS="root"/' /etc/default/snapper
```

--------------------------------

### Managing Boot Slots with Fastboot

Source: https://www.kali.org/docs/nethunter-pro

This snippet provides essential fastboot commands for devices with A/B partitions. It shows how to flash to a specific slot, check the current slot, and set the active slot, crucial for dual-booting or recovery scenarios.

```bash
# If your device has A/B partitions, you can choose the slot while flashing, e.g., `fastboot flash boot_a nethunterpro*boot-{model}-{variant}.img`.
# Run `fastboot getvar current-slot` to get the active slot in fastboot.
# Run `fastboot set_active {a or b}` to change the active slot.
# Do not forget to erase the dtbo before booting.

```

--------------------------------

### Install Kali NetHunter Pro on QCOM Android Devices (SD Card)

Source: https://www.kali.org/docs/nethunter-pro

Commands for installing Kali NetHunter Pro on Qualcomm devices via an SD card. This involves decompressing the image, converting it, and flashing it to the SD card, followed by flashing the boot image and potentially erasing the dtbo.

```bash
# Install on SDCard:
$ xz -d kali-nethunterpro-2025.4-sdm845.img.xz
$ simg2img flash userdata nethunterpro-*-sdm845*rootfs.img rootfs_ext4.img
$ dd if=rootfs_ext4.img of={sdcard_block_device} bs=1M oflag=sync status=progress
$ fastboot flash boot nethunterpro*boot-{model}-{variant}.img
$ fastboot erase dtbo # if your device has dtbo partition

```

--------------------------------

### Install and Initialize Waydroid on Kali

Source: https://www.kali.org/docs/nethunter-pro/waydroid

Installs the Waydroid package using apt and then initializes the Android container. A reboot is required after initialization for Waydroid to function correctly.

```bash
sudo apt install waydroid
sudo waydroid init
reboot

```

--------------------------------

### Display Help for Raspberry Pi Build Script (Shell)

Source: https://www.kali.org/docs/development/arm-build-scripts

This example shows how to display the help screen for the `raspberry-pi.sh` build script. The help output details various command-line options for specifying architecture, desktop environment, image type, and debugging.

```shell
./raspberry-pi.sh --help

```

--------------------------------

### Partitioning USB Drive using sgdisk

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This section provides an alternative method for partitioning the target USB drive using the `sgdisk` command-line utility. It demonstrates how to zap existing partitions, create new ones with specified sizes, set their types, assign names, and configure hybrid MBR settings.

```bash
$ sgdisk --zap-all /dev/sda
$ sgdisk --new=1:0:+4096M /dev/sda
$ sgdisk --new=2:0:+2M /dev/sda
$ sgdisk --new=3:0:+128M /dev/sda
$ sgdisk --new=4:0:+8192M /dev/sda
$ sgdisk --new=5:0:0 /dev/sda
$ sgdisk --typecode=1:8301 --typecode=2:ef02 --typecode=3:ef00 --typecode=4:8200 --typecode=5:8300 /dev/sda
$ sgdisk --change-name=1:/boot --change-name=2:GRUB --change-name=3:EFI-SP --change-name=4:swap --change-name=5:rootfs /dev/sda
$ sgdisk --hybrid 1:2:3 /dev/sda
$ sgdisk --print /dev/sda
```

--------------------------------

### Dynamically Configure dnsmasq for PXE Boot (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This script dynamically generates a dnsmasq configuration file. It sets the network interface, DHCP range, boot file, TFTP root, and DHCP options based on the current network settings. This is useful for resolving IP conflicts and ensuring proper PXE boot setup.

```bash
kali@kali:~$ interface=eth0
kali@kali:~$ 
network=$( ip -4 addr show dev ${interface} | grep -oP '(?<=inet\s)\d+(\.\d+){2}' )
kali@kali:~$ 
cat <<EOF | sudo tee /etc/dnsmasq.conf
interface=${interface}
dhcp-range=${network}.100,${network}.200,12h
dhcp-boot=pxelinux.0
enable-tftp
tftp-root=/tftpboot/
dhcp-option=3,$( ip -4 route show dev ${interface} | grep -oP '(?<=default\svia\s)(\d+(\.\d+){3})' )
dhcp-option=6,8.8.8.8,8.8.4.4
EOF
kali@kali:~$ 
sudo systemctl restart dnsmasq
kali@kali:~$ 
sudo systemctl status dnsmasq
```

--------------------------------

### Restart and Enable dnsmasq Service

Source: https://www.kali.org/docs/installation/network-pxe

Restarts the dnsmasq service to apply the configuration changes and enables it to start automatically on system boot. This ensures the PXE server is running and accessible.

```bash
sudo systemctl restart dnsmasq
sudo systemctl enable dnsmasq
```

--------------------------------

### Python Pip Package Management Test Script

Source: https://www.kali.org/docs/development/contributing-runtime-tests

This shell script automates the installation, listing, showing, and uninstallation of a Python package named 'world' using pip. It includes setup for a testing user and environment, and checks the installed package's metadata.

```shell
#!/bin/sh

export HOME=$AUTOPKGTEST_TMP
export PATH=$PATH:$HOME/.local/bin
export PIP_DISABLE_PIP_VERSION_CHECK=1

if [ $(id -u) = 0 ]
then
    adduser --quiet --system --group --no-create-home testing
    user=testing
    mkdir $HOME/.cache
    chown -R $user $HOME
    runuser="runuser -p -u $user --"
else
    runuser=""
fi

$runuser python3 -m pip install world
$runuser python3 -m pip list --format=columns
$runuser python3 -m pip show world
ls -ld $HOME/.local/lib/python3.*.dist-info
$runuser python3 -m pip uninstall -y world
$runuser python3 -m pip list --format=columns
# Temporarily disabled.  See #912379
#$runuser python3 -m pip list --outdated
if [ $(id -u) = 0 ]
then
    deluser --quiet testing
fi

```

--------------------------------

### Install VirtualBox and Extension Pack (Oracle Repo)

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Install VirtualBox, its Extension Pack, and the necessary Linux headers from the Oracle repository. This command fetches and installs the latest stable version of VirtualBox and its associated components.

```bash
kali@kali:~$ sudo apt install virtualbox virtualbox-ext-pack linux-headers-generic
[...]
kali@kali:~$ 

```

--------------------------------

### Install Approx Caching Proxy

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Installs the 'approx' package, a caching proxy designed to speed up the download of build dependencies for sbuild. This command is executed on the Kali system using apt.

```bash
sudo apt install -y approx

```

--------------------------------

### Install Kaboxer Tool

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Installs the Kaboxer command-line tool on Kali Linux using the apt package manager. This is the first step to begin packaging applications.

```bash
kali@kali:~$ sudo apt install -y kaboxer

```

--------------------------------

### Partitioning USB Drive using gdisk

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This section describes partitioning a target USB drive using the `gdisk` command-line utility. It outlines the creation of partitions for boot, BIOS boot, EFI system, swap, and the main Linux filesystem, specifying their sizes and types.

```bash
sudo gdisk /dev/sda
/dev/sda1,   4.0 GiB, type 8301, Linux reserved, will become /boot
/dev/sda2,   2.0 MiB, type ef02, BIOS boot, will contain grub2
/dev/sda3, 128.0 MiB, type ef00, EFI system partition
/dev/sda4,   8.0 GiB, type 8200, Linux swap
/dev/sda5,  <something big>, type 8300, Linux filesystem, will be the main partition
```

--------------------------------

### Install Kali NetHunter Pro on QCOM Android Devices (eMMC)

Source: https://www.kali.org/docs/nethunter-pro

Instructions for flashing Kali NetHunter Pro directly to the eMMC storage of Qualcomm devices using fastboot. This includes flashing the rootfs image, boot image, and erasing the dtbo partition if applicable.

```bash
# Install on EMMC (fastboot method):
$ xz -d kali-nethunterpro-2025.4-sdm845.img.xz
$ fastboot flash userdata nethunterpro-*-sdm845*rootfs.img
$ fastboot flash boot nethunterpro*boot-{model}-{variant}.img
$ fastboot erase dtbo # if your device has dtbo partition

```

--------------------------------

### Install Packaging Tools on Kali Linux

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Installs essential tools for software packaging on Kali Linux using the apt package manager. This includes build tools, version control, and utilities for Debian packaging.

```bash
kali@kali:~$ sudo apt update
[...] 
kali@kali:~$ sudo apt install -y sbuild mmdebstrap uidmap apt-file gitk git-lfs myrepos debhelper devscripts dput lintian quilt
[...]
kali@kali:~$
```

--------------------------------

### Install Kali NetHunter Pro on PinePhone/Pro Devices

Source: https://www.kali.org/docs/nethunter-pro

This snippet demonstrates the commands to decompress and flash the Kali NetHunter Pro image onto PinePhone/Pro devices using `dd`. Ensure the correct device path (`/dev/mmcblkX`) is used.

```bash
xz -d kali-nethunterpro-2025.4-pinephone-phosh.img.xz
dd if=kali-nethunterpro-2025.4-pinephone-phosh.img of=/dev/mmcblkX bs=1M oflag=sync status=progress

```

--------------------------------

### Configuring LUKS Encryption and Initramfs (Shell)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This extensive snippet covers the setup for LUKS encrypted partitions. It includes creating a secure key file, setting permissions, adding the key to the encrypted partitions, configuring /etc/crypttab to define the encrypted devices and their keys, and finally updating the initramfs to include the necessary decryption tools and keys.

```shell
$ echo "KEYFILE_PATTERN=/etc/luks/*.keyfile" >>/etc/cryptsetup-initramfs/conf-hook
$ echo "UMASK=0077" >>/etc/initramfs-tools/initramfs.conf
$ mkdir -p /etc/luks
$ dd if=/dev/urandom of=/etc/luks/boot_os.keyfile bs=4096 count=1
$ chmod u=rx,go-rwx /etc/luks
$ chmod u=r,go-rwx /etc/luks/boot_os.keyfile
$ cryptsetup luksAddKey /dev/sdb1 /etc/luks/boot_os.keyfile
$ cryptsetup luksAddKey /dev/sdb4 /etc/luks/boot_os.keyfile
$ cryptsetup luksAddKey /dev/sdb5 /etc/luks/boot_os.keyfile
$ echo "LUKS_BOOT UUID=$( blkid -s UUID -o value /dev/sdb1) /etc/luks/boot_os.keyfile luks,discard" >>/etc/crypttab
$ echo "LUKS_SWAP UUID=$( blkid -s UUID -o value /dev/sdb4) /etc/luks/boot_os.keyfile luks,discard" >>/etc/crypttab
$ echo "LUKS_ROOT UUID=$( blkid -s UUID -o value /dev/sdb5) /etc/luks/boot_os.keyfile luks,discard" >>/etc/crypttab
$ /usr/sbin/update-initramfs -u -k all

```

--------------------------------

### Install Package from Kali Bleeding Edge Repository

Source: https://www.kali.org/docs/general-use/kali-bleeding-edge

Installs a specified package from the kali-bleeding-edge repository. This command requires root privileges and assumes the repository has already been enabled. The output shows the package download and installation process.

```bash
kali@kali:~$ sudo apt install gitleaks/kali-bleeding-edge
Reading package lists... Done
Building dependency tree
Reading state information... Done
Selected version '7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1' (http.kali.org [amd64]) for 'gitleaks'
The following packages will be upgraded:
  gitleaks
1 upgraded, 0 newly installed, 0 to remove and 283 not upgraded.
Need to get 2504 kB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 http://kali.download/kali kali-bleeding-edge/main amd64 gitleaks amd64 7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1 [2504 kB]
Fetched 2504 kB in 2s (1257 kB/s)
(Reading database ... 106991 files and directories currently installed.)
Preparing to unpack .../gitleaks_7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1_amd64.deb ...
Unpacking gitleaks (7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1) over (7.4.0-0kali1) ...
Setting up gitleaks (7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1) ...
Processing triggers for kali-menu (2021.1.4) ...
```

--------------------------------

### Verify and Launch Imported Kali Linux on WSL

Source: https://www.kali.org/docs/wsl/wsl-preparations

After importing the rootfs, this command verifies the installation by listing available WSL distributions and then launches the imported Kali Linux environment. The output shows the distribution status and the prompt changes to the Kali environment, allowing verification of system information.

```bash
C:\Users\Win\Downloads>wsl --list --verbose
  NAME          STATE           VERSION
* kali-wsl      Stopped         2

C:\Users\Win\Downloads>

C:\Users\Win\Downloads>wsl --distribution kali-wsl
┏━(Message from Kali developers)
┃
┃ This is a minimal installation of Kali Linux, you likely
┃ want to install supplementary tools. Learn how:
┃ ⇒ https://www.kali.org/docs/troubleshooting/common-minimum-setup/
┗━(Run: “touch ~/.hushlogin” to hide this message)
┌──(root㉿DESKTOP-AJVAG8O)-[/mnt/c/Users/Win/Downloads]
└─# uname -a
Linux DESKTOP-AJVAG8O 5.10.16.3-microsoft-standard-WSL2 #1 SMP Fri Apr 2 22:23:49 UTC 2021 x86_64 GNU/Linux

┌──(root㉿DESKTOP-AJVAG8O)-[/mnt/c/Users/Win/Downloads]
└─# id
uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users)

┌──(root㉿DESKTOP-AJVAG8O)-[/mnt/c/Users/Win/Downloads]
└─#
```

--------------------------------

### Install NVIDIA Driver and CUDA Toolkit

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

Installs the NVIDIA proprietary driver and the CUDA toolkit, which enables GPU acceleration for compatible applications. This step also addresses potential conflicts with the nouveau driver and suggests a reboot.

```bash
kali@kali:~$ sudo apt install -y nvidia-driver nvidia-cuda-toolkit

┌─────────────────────────────────┤ Configuring xserver-xorg-video-nvidia ├─────────────────────────────────┐
│                                                                                                           │
│ Conflicting nouveau kernel module loaded                                                                  │
│                                                                                                           │
│ The free nouveau kernel module is currently loaded and conflicts with the non-free nvidia kernel module.  │
│                                                                                                           │
│ The easiest way to fix this is to reboot the machine once the installation has finished.                  │
│                                                                                                           │
│                                                  <Ok>                                                     │
│                                                                                                           │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────┘

kali@kali:~$ 
kali@kali:~$ sudo reboot -f
kali@kali:~$ 

```

--------------------------------

### Install Live Build and CDEBootstrap Packages

Source: https://www.kali.org/docs/development/generate-updated-kali-iso

Installs the 'live-build' and 'cdebootstrap' packages required for building Kali ISOs. This command updates the package list and then installs the specified packages non-interactively.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y git live-build cdebootstrap

```

--------------------------------

### Add Waydroid Official Repository on Kali

Source: https://www.kali.org/docs/nethunter-pro/waydroid

Downloads and executes the Waydroid repository setup script. It fetches the latest repository information and adds it to your system's sources for package management.

```bash
curl -sSL https://repo.waydro.id -o wd.sh
sudo bash wd.sh bookworm

```

--------------------------------

### Install Kali Linux GNOME Desktop Environment

Source: https://www.kali.org/docs/general-use/xfce-faq

Installs the Kali Linux GNOME desktop environment. This command is used to switch back to GNOME after having installed Xfce.

```bash
sudo apt update && sudo apt install -y kali-desktop-gnome
```

--------------------------------

### Push Kali Nethunter Installer to Device

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This command transfers the built Kali Nethunter installer zip file from the computer to the Android device's SD card using ADB. This prepares the installer for installation via Magisk.

```bash
adb push nethunter-20250629_171321-beyond1lte-los-fifteen-kalifs_full.zip /sdcard/
```

--------------------------------

### Make VMware Installer Executable and Run

Source: https://www.kali.org/docs/virtualization/install-vmware-host

After downloading the VMware installer, this command makes the 'vmware.bundle' file executable using `chmod`. Subsequently, it runs the installer with superuser privileges using `sudo`. The output indicates the successful installation of VMware Workstation.

```bash
kali@kali:~$ chmod +x ~/Downloads/vmware.bundle
kali@kali:~$ 
kali@kali:~$ sudo ~/Downloads/vmware.bundle
Extracting VMware Installer...done.
Installing VMware Workstation 17.0.2
    Configuring...
[######################################################################] 100%
Installation was successful.
kali@kali:~$
```

--------------------------------

### Install VirtualBox Guest Additions on Kali

Source: https://www.kali.org/docs/virtualization/install-virtualbox-guest-additions-legacy

Copies the Guest Additions run file from the virtual CD-ROM to the Downloads directory, makes it executable, and then runs the installer. A reboot is required after installation to apply the changes.

```bash
kali@kali:~$ cp /media/cdrom/VBoxLinuxAdditions.run ~/Downloads/
kali@kali:~$ chmod 0755 ~/Downloads/VBoxLinuxAdditions.run
kali@kali:~$ cd ~/Downloads/
kali@kali:~/Downloads$ ./VBoxLinuxAdditions.run
```

--------------------------------

### Mounting EFI Partition and btrfs Subvolumes Post-Installation

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This sequence of commands demonstrates how to unmount a previously mounted point, create the EFI boot directory, mount the correct EFI partition from the USB drive, and then mount the necessary btrfs subvolumes for home and root. This is a crucial step after modifying fstab to ensure correct system mounting.

```shell
$ umount /mnt/point
$ mkdir -p /target/boot/efi
$ mount /dev/sdb3 /target/boot/efi
$ mount -o subvol=@home /dev/mapper/LUKS_ROOT /target/home
$ mount -o subvol=@root /dev/mapper/LUKS_ROOT /target/root
```

--------------------------------

### Start and Attach to Privileged Kali LXC Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Starts a stopped Kali LXC container in detached mode and then attaches to its console. This allows for direct interaction with the container's shell for further configuration like setting a root password and installing packages.

```bash
kali@kali:~$ sudo lxc-start -n my-kali -d
kali@kali:~$ sudo lxc-attach -n my-kali
```

--------------------------------

### Build Installer Updater Image for OnePlus 7

Source: https://www.kali.org/docs/nethunter/building-nethunter

This command builds an installer updater image for a OnePlus 7 device running Android 10. The '-i' flag indicates the creation of an installer updater. The output is a zip file intended for updating the NetHunter installer itself.

```bash
kali@kali:~/kali-nethunter-installer$ python3 build.py -k oneplus7-oos --ten -i

```

--------------------------------

### Install QEMU and OVMF Packages

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Installs the QEMU emulator, QEMU system emulator for x86 architecture, and OVMF (Open Virtual Machine Firmware) for UEFI support. These packages are required for virtualizing Kali Linux.

```bash
kali@kali:$ sudo apt update
kali@kali:$ sudo apt install -y qemu qemu-system-x86 ovmf

```

--------------------------------

### Install Dependencies and Create Image File

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

Installs necessary packages like kpartx, xz-utils, gdisk, and vboot utilities, then creates a raw disk image file of a specified size using dd.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils gdisk uboot-mkimage u-boot-tools vboot-kernel-utils vboot-utils cgpt
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ dd if=/dev/zero of=kali-custom-chrome.img conv=fsync bs=4M count=7000

```

--------------------------------

### Install dnsmasq for PXE Server

Source: https://www.kali.org/docs/installation/network-pxe

Installs the dnsmasq package, which provides DHCP, TFTP, and PXE boot services necessary for network booting Kali Linux. This is the first step in manually setting up a PXE server.

```bash
sudo apt install -y dnsmasq
```

--------------------------------

### Create Executable Helper Script for Instaloader

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This script creates a helper executable named 'instaloader' in the debian/helper-script directory. When executed, it uses 'python3' to run the actual Instaloader script located at '/usr/share/instaloader/instaloader.py', passing any arguments along. This allows the application to be run directly from the command line without specifying the Python interpreter or file extension.

```shell
#!/bin/sh
exec python3 /usr/share/instaloader/instaloader.py "$@"
```

--------------------------------

### Install Git, GCC, Make, and Headers on Kali

Source: https://www.kali.org/docs/virtualization/install-vmware-guest-tools-legacy

Installs necessary packages for compiling VMware Tools, including git, gcc, make, and kernel headers specific to the running kernel. This is a prerequisite for patching and installing VMware Tools.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y git gcc make linux-headers-$( uname -r )
```

--------------------------------

### Configure Autologin and Startx

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This code snippet demonstrates how to configure the ODROID to automatically log in and start the graphical environment upon boot. It involves appending a conditional statement to the '~/.bash_profile' that checks if the display is not set and the current terminal is '/dev/ttySAC1', then executes 'startx'. It also mentions copying '/etc/skel/.profile' if '.bash_profile' does not exist.

```bash
# If you don't have a .bash_profile, copy it from /etc/skel/.profile first
kali@kali:~$ cat <<EOF >> ~/.bash_profile
if [ -z "$DISPLAY" ] && [ $(tty) = /dev/ttySAC1 ]; then
startx
fi
EOF

```

--------------------------------

### Configure git-buildpackage (gbp)

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Sets up the configuration file for git-buildpackage (gbp). This configuration enables pristine-tar, sets an export directory for builds, and configures options for dch, import-orig, and pq commands. Replace 'email@domain.com' with your actual email.

```bash
kali@kali:~$ cat <<EOF > ~/.gbp.conf
[DEFAULT]
pristine-tar = True
cleaner = /bin/true

[buildpackage]
export-dir = $HOME/kali/build-area/
ignore-branch = True
ignore-new = True
sign-tags = True

[dch]
ignore-branch = True
multimaint-merge = True

[import-orig]
filter-pristine-tar = True
sign-tags = True

[pq]
patch-numbers = False
EOF
kali@kali:~$
```

--------------------------------

### Download and Install Patched QEMU Package

Source: https://www.kali.org/docs/arm/x86-on-arm

This snippet demonstrates how to download a specific version of the qemu-user-static package from a Debian snapshot and install it using dpkg. This is a workaround for potential issues with the current qemu-user-static version.

```bash
kali@kali:~$ wget https://snapshot.debian.org/archive/debian/20240509T024809Z/pool/main/q/qemu/qemu-user-static_8.2.3%2Bds-2_arm64.deb
kali@kali:~$ 
kali@kali:~$ sudo apt install ./qemu-user-static_8.2.3+ds-2_arm64.deb
kali@kali:~$
```

--------------------------------

### Check for mesa-opencl-icd (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command checks if the 'mesa-opencl-icd' package is installed, which might conflict with NVIDIA's OpenCL setup. It uses `dpkg -l` and `grep` to search for the specific package. If found, it should be removed.

```bash
kali@kali:~$ dpkg -l |  grep -i mesa-opencl-icd
ii  mesa-opencl-icd:amd64                 19.3.2-1                        amd64        free implementation of the OpenCL API -- ICD runtime
kali@kali:~$
```

--------------------------------

### Manage Metasploit Database with msfdb (Shell)

Source: https://www.kali.org/docs/tools/starting-metasploit-framework-in-kali

The `msfdb` command is a utility for managing the Metasploit Framework database. It offers various subcommands to initialize, reinitialize, delete, start, stop, check the status of, and run `msfconsole` with the database.

```shell
kali@kali:~$ sudo msfdb
Manage the metasploit framework database

  msfdb init     # start and initialize the database
  msfdb reinit   # delete and reinitialize the database
  msfdb delete   # delete database and stop using it
  msfdb start    # start the database
  msfdb stop     # stop the database
  msfdb status   # check service status
  msfdb run      # start the database and run msfconsole

kali@kali:~$ 

```

--------------------------------

### Manage Kali LXC Containers (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Provides common commands for managing LXC containers, including starting, stopping, listing, getting information, and removing containers. These are essential utilities for container lifecycle management.

```bash
Start: `sudo lxc-start -n my-kali -d`
Stop: `sudo lxc-stop -n my-kali`
List: `sudo lxc-ls -f`
Info: `sudo lxc-info -n my-kali`
Remove: `sudo lxc-destroy -n my-kali`

```

--------------------------------

### Update Kali Linux System

Source: https://www.kali.org/docs/installation/barebone-kali

This command updates the package list and performs a full system upgrade on Kali Linux, ensuring all installed packages are up-to-date. The '-y' flag automatically confirms any prompts during the upgrade process. It also includes a check and conditional reboot if required by the updates.

```shell
kali@kali:~$ sudo apt update && sudo apt full-upgrade -y
....
kali@kali:~$ 
kali@kali:~$ [ -f /var/run/reboot-required ] && sudo reboot -f

```

--------------------------------

### Install Necessary Packages for VMware

Source: https://www.kali.org/docs/virtualization/install-vmware-host

This command installs essential packages required for VMware installation and operation on Kali Linux. It includes build tools, kernel headers matching the running kernel, and the 'libaio1' library.

```bash
kali@kali:~$ sudo apt install -y build-essential linux-headers-$( uname -r ) vlan libaio1
[...] 
kali@kali:~$
```

--------------------------------

### Install Kali Metapackage using APT

Source: https://www.kali.org/docs/general-use/metapackages

Command to install a specific Kali Linux metapackage, such as 'kali-linux-default', using the apt package manager. This command installs the metapackage and all its dependencies.

```bash
sudo apt install -y kali-linux-default
```

--------------------------------

### Install Xfce and RDP on Kali Linux

Source: https://www.kali.org/docs/general-use/xfce-with-rdp

This script automates the installation of Xfce4, necessary Xorg components, and xrdp for RDP access. It also configures xrdp to use port 3390 instead of the default 3389. This process requires root privileges and can take a significant amount of time due to package downloads and installations.

```shell
#!/bin/sh
echo "[i] Updating and upgrading Kali (this will take a while)"
apt-get update
apt-get full-upgrade -y

echo "[i] Installing Xfce4 & xrdp (this will take a while as well)"
apt-get install -y kali-desktop-xfce xorg xrdp xorgxrdp

echo "[i] Configuring xrdp to listen to port 3390 (but not starting the service)"
sed -i 's/port=3389/port=3390/g' /etc/xrdp/xrdp.ini

```

--------------------------------

### Integrate Preseed into Initrd for Unattended Kali Install (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This script demonstrates how to integrate a preseed configuration file into the Kali Linux initrd image for unattended installations. It involves navigating to the initrd directory, decompressing it, copying the preseed file, appending it to the initrd archive, and then recompressing the initrd. This process is crucial for network-based automated deployments.

```bash
kali@kali:~$ cd /tftpboot/debian-installer/amd64/
kali@kali:/tftpboot/debian-installer/amd64$ sudo gunzip initrd.gz
kali@kali:/tftpboot/debian-installer/amd64$
kali@kali:/tftpboot/debian-installer/amd64$ sudo cp -v /opt/pxe/preseed.cfg preseed.cfg
'/opt/pxe/preseed.cfg' -> './preseed.cfg'
kali@kali:/tftpboot/debian-installer/amd64$
kali@kali:/tftpboot/debian-installer/amd64$ echo preseed.cfg | sudo cpio -H newc -o -A -F initrd
6 blocks
kali@kali:/tftpboot/debian-installer/amd64$ sudo gzip initrd
kali@kali:/tftpboot/debian-installer/amd64$
```

--------------------------------

### Change Root Password in Kali Linux

Source: https://www.kali.org/docs/installation/barebone-kali

This snippet demonstrates how to change the root user's password on a Kali Linux system. It involves switching to the root user using 'sudo su' and then using the 'passwd' command to set a new password. This is a crucial step for system security after installation.

```shell
kali@kali:~$ sudo su
[sudo] password for kali:
root@kali:/home/kali#
root@kali:/home/kali# passwd
New password:
Retype new password:
passwd: password updated successfully

root@kali:/home/kali#

```

--------------------------------

### Install QEMU and Binfmt Support for x86 Emulation

Source: https://www.kali.org/docs/arm/x86-on-arm

This command sequence installs the necessary packages for running x86 code on an ARM device. It includes qemu-user-static for emulation, binfmt-support for automatic execution of foreign binaries, and adds the amd64 architecture to support x86_64 packages. It also installs the amd64 version of libc6, which is often required by x86 executables.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt install -y qemu-user-static binfmt-support
kali@kali:~$ 
kali@kali:~$ sudo dpkg --add-architecture amd64
kali@kali:~$ 
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt install libc6:amd64
kali@kali:~$
```

--------------------------------

### Launch Tor Browser on Kali Linux

Source: https://www.kali.org/docs/tools/tor

This command initiates the Tor Browser Launcher. On the first run, it downloads and installs Tor Browser with signature verification. Subsequent runs will be used to update and launch the browser. This command requires no arguments.

```bash
torbrowser-launcher
```

--------------------------------

### Install Firmware for Intel SOF Audio Devices

Source: https://www.kali.org/docs/troubleshooting/no-sound

This command installs the necessary firmware for Intel SOF audio devices, which is required for some recent Intel sound cards to function correctly on baremetal Kali installations. It is safe to install even if not strictly needed.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt install -y firmware-sof-signed
kali@kali:~$ 

```

--------------------------------

### Initialize Kali Linux VM with Vagrant

Source: https://www.kali.org/docs/virtualization/install-vagrant-guest-vm

This snippet shows the command to initialize a new Vagrant environment for Kali Linux using the 'kalilinux/rolling' box. It creates a basic Vagrantfile, which is the configuration file for Vagrant. The Vagrantfile specifies the box to be used, and after initialization, you can start the VM with 'vagrant up'.

```bash
kali@kali:~/vagrant$ vagrant init kalilinux/rolling
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

kali@kali:~/vagrant$
kali@kali:~/vagrant$ cat Vagrantfile | grep -v '#'

Vagrant.configure("2") do |config|

  config.vm.box = "kalilinux/rolling"

end

kali@kali:~/vagrant$

```

--------------------------------

### Extract Kali VirtualBox VM Image using 7z

Source: https://www.kali.org/docs/virtualization/import-premade-virtualbox

This command extracts the Kali Linux VirtualBox image from a 7z archive. It requires the 7z utility to be installed on the system. The input is the name of the .7z file, and the output is the extracted VM files.

```bash
kali@kali:~$ 7z x kali-linux-2025.4-virtualbox-amd64.7z
[...]
kali@kali:~$ 

```

--------------------------------

### Install pipx using apt

Source: https://www.kali.org/docs/general-use/python3-external-packages

Installs the pipx utility using the apt package manager. This command is used when pipx is not pre-installed on Kali Linux.

```bash
sudo apt install -y pipx
```

--------------------------------

### Install Waydroid Prerequisites on Kali

Source: https://www.kali.org/docs/nethunter-pro/waydroid

Installs necessary packages like curl and ca-certificates required for adding the Waydroid repository. This is a foundational step before proceeding with Waydroid installation.

```bash
sudo apt install curl ca-certificates -y

```

--------------------------------

### Overlay Custom Wallpaper on Kali ISO

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This command sequence downloads a custom wallpaper and places it within the ISO's file structure. The wallpaper is overlaid by placing it in the `kali-config/common/includes.chroot/usr/share/wallpapers/kali/contents/images/` directory.

```bash
kali@kali:~$ mkdir -pv kali-config/common/includes.chroot/usr/share/wallpapers/kali/contents/images/
kali@kali:~$ wget https://www.kali.org/dojo/blackhat-2015/wp-blue.png
kali@kali:~$ mv wp-blue.png kali-config/common/includes.chroot/usr/share/wallpapers/kali/contents/images

```

--------------------------------

### Upgrade Android Versions using ADB and TWRP

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This sequence demonstrates upgrading the Android system through multiple versions using ADB to push ZIP files to the device and TWRP to install them. It includes commands for pushing ROM zip files and initiating the installation process within TWRP, as well as wiping the data partition, which is crucial for preventing device unresponsiveness after upgrades.

```bash
kali@kali:~$ adb push cm-13.1.2-ZNH2KAS3P0-bacon-signed-8502142fdc.zip /sdcard/Download/cm-13.1.2.zip; adb shell 'twrp install /sdcard/Download/cm-13.1.2.zip'
kali@kali:~$ 
kali@kali:~$ adb push lineage-17.1-20210325-nightly-bacon-signed.zip /sdcard/Download/los-17.1.zip; adb shell 'twrp install /sdcard/Download/los-17.1.zip'
kali@kali:~$ 
kali@kali:~$ adb push lineage-18.1-20240306-nightly-bacon-signed.zip /sdcard/Download/los-18.1.zip; adb shell 'twrp install /sdcard/Download/los-18.1.zip'
kali@kali:~$ adb shell 'twrp wipe data'    # Alt: adb shell 'twrp format data'
kali@kali:~$ 
kali@kali:~$ adb reboot
```

--------------------------------

### Install NetHunter on Termux (Shell)

Source: https://www.kali.org/docs/nethunter/nethunter-rootless

This script installs NetHunter on Termux by setting up storage access, installing wget, downloading the NetHunter installer script, and making it executable.

```shell
kali@kali:~$ termux-setup-storage
kali@kali:~$ pkg install wget
kali@kali:~$ wget -O install-nethunter-termux https://offs.ec/2MceZWr
kali@kali:~$ chmod +x install-nethunter-termux
kali@kali:~$ ./install-nethunter-termux

```

--------------------------------

### Create Mirror Directories

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Sets up the necessary directories for storing Kali Linux mirror data and assigns ownership to the dedicated mirror user.

```bash
sudo mkdir -p /srv/mirrors/kali{,-images}
sudo chown archvsync:archvsync /srv/mirrors/kali{,-images}
```

--------------------------------

### Install Win-KeX in Kali WSL

Source: https://www.kali.org/docs/wsl/win-kex

Installs the Win-KeX package within a Kali Linux environment running on WSL 2. It requires updating the package list before installation.

```bash
sudo apt update

sudo apt install -y kali-win-kex
```

--------------------------------

### Managing Python 2 to 3 Symlink in Kali

Source: https://www.kali.org/docs/general-use/python3-transition

Users can control whether '/usr/bin/python' points to Python 2 or Python 3. Installing 'python-is-python2' makes it point to Python 2, while 'python-is-python3' makes it point to Python 3. This action also affects the login message.

```bash
sudo apt remove python-is-python2
sudo apt install -y python-is-python3
```

--------------------------------

### Example Custom Build Values Configuration (Shell)

Source: https://www.kali.org/docs/development/arm-build-scripts

This snippet shows commented-out examples of custom values that can be set in `builder.txt` to modify the build process. These include options for version, hostname, locale, disk space, compression, filesystem type, and network settings.

```shell
# Version Kali release
#version=${version:-$(cat .release)}

# Custom hostname variable
#hostname=kali

# Choose a locale
#locale="en_US.UTF-8"

# Free space added to the rootfs in MiB
#free_space="300"

# /boot partition in MiB
#bootsize="128"

# Select compression, xz or none
#compress="xz"

# Choose filesystem format to format ( ext3 or ext4 )
#fstype="ext4"

# Disable IPV6 ( yes or no)
#disable_ipv6="yes"

# Make SWAP ( yes or no)
#swap="no"

# DNS server
#nameserver="8.8.8.8"

# To limit the number of CPU cores to use during compression
# Use 0 for unlimited CPU cores, -1 to subtract 1 cores from the total
#cpu_cores="4"

# To limit the CPU usage during compression
# 0 or 100 No limit, 10 = percentage use, 50, 75, 90, etc.
#cpu_limit="85"

# If you have your own preferred mirrors, set them here.
#mirror="http://http.kali.org/kali"

# If you use a custom mirror that your users won't have access to , you can replace_mirror to point them at the official mirrors instead.
#replace_mirror="http://http.kali.org/kali"

# Use packages from the listed components of the archive.
#components="main,contrib,non-free,non-free-firmware"

# Suite to use, valid options are:
# kali-rolling, kali-dev, kali-dev-only, kali-last-snapshot
#suite="kali-last-snapshot"

# If you build against something other than kali-rolling, you can set this so that the finished image will point to the kali-rolling suite
#replace_suite="kali-rolling"

# Default file name
# On the Raspberry Pi script, this would result in
# "kali-linux-202X-WXX-raspberry-pi-arm64" for the default filename.
# For release builds from Kali Linux, the requirements are that it start with kali-linux
# and end with the architecture.
#image_name="kali-linux-$(date +%Y)-W$(date +%U)-${hw_model}-${variant}"

```

--------------------------------

### Create VNC Configuration Directory and Startup File

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This command sequence creates a hidden .vnc directory in the user's home directory, which is necessary for VNC configuration. It then opens the xstartup file within this directory using the 'vim' editor, where VNC session startup commands will be placed.

```bash
kali@kali:~$ mkdir -p ~/.vnc/
kali@kali:~$ 
kali@kali:~$ vim ~/.vnc/xstartup
kali@kali:~$ 
kali@kali:~$ cat ~/.vnc/xstartup
#!/bin/sh

#############################

```

--------------------------------

### Install Kali ARM Build Prerequisites

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

This command installs the necessary tools and dependencies required for building Kali Linux ARM images. It includes packages like debootstrap, qemu-user-static, and cross-compilation tools.

```bash
kali@kali:~$ git clone https://gitlab.com/kalilinux/build-scripts/kali-arm.git
kali@kali:~$ dpkg --add-architecture i386
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y debootstrap qemu-user-static device-tree-compiler lzma lzop u-boot-tools libncurses5:i386 pixz
```

--------------------------------

### Install and Extract Kernel Sources (Bash)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Installs a specific version of the Linux kernel source code and prepares the directory structure for compilation. It fetches the 'linux-source-5.15' package, creates a '~/src/' directory if it doesn't exist, changes into it, and then extracts the downloaded kernel source archive.

```bash
$ sudo apt-get install linux-source-5.15
$ mkdir -p ~/src/
$ cd ~/src/
$ tar -xzf /usr/src/linux-source-5.15.tar.xz

```

--------------------------------

### Define Package Contents with debian/instaloader.install

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This script defines the files to be installed and their target directories. It specifies the Python script and its associated data files, along with the helper script for command-line execution. Ensure the paths are correct for your package structure.

```shell
instaloader.py usr/share/instaloader/
instaloader usr/share/instaloader/
debian/helper-script/instaloader usr/bin/
```

--------------------------------

### Install Kali Linux Large Package

Source: https://www.kali.org/docs/wsl/win-kex

Installs the 'Kali with the lot' package, which includes a comprehensive set of traditional Kali Linux default tools. This is an optional step for users who require a fuller Kali environment.

```bash
sudo apt install -y kali-linux-large
```

--------------------------------

### Start Kali Xfce Panel in GUI Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Launches the Xfce desktop panel as the 'kali' user within the GUI container. This command is used after setting up the user and environment to start the graphical interface.

```bash
kali@kali:~$ lxc exec gui-kali -- sudo -u kali xfce4-panel
```

--------------------------------

### Update Repos and Install Prerequisites for Kali ISO Build

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This command sequence updates the package repositories, installs essential tools like git, live-build, cdebootstrap, and devscripts, and then clones the live-build-config repository. These are the initial steps required before customizing the Kali ISO.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y git live-build cdebootstrap devscripts
kali@kali:~$ git clone https://gitlab.com/kalilinux/build-scripts/live-build-config.git
kali@kali:~$ cd live-build-config/
```

--------------------------------

### Install rEFInd on Kali Linux

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

Installs the rEFInd boot manager on Kali Linux using the apt package manager. It first updates the package list and then installs rEFInd. The process includes an interactive prompt to automatically configure rEFInd to the EFI System Partition (ESP).

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt install -y refind

```

--------------------------------

### Install Flatpak and Flathub on Kali Linux

Source: https://www.kali.org/docs/tools/flatpak

Installs the Flatpak package manager and adds the Flathub remote repository. This allows users to install applications distributed via Flatpak. Requires root privileges.

```bash
sudo apt update
sudo apt install -y flatpak
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

--------------------------------

### Install GNOME Software Flatpak Plugin on Kali Linux

Source: https://www.kali.org/docs/tools/flatpak

Installs the necessary plugin for GNOME Software to manage Flatpak applications. This enables users to discover, install, and manage Flatpak apps through the graphical software center. Requires root privileges.

```bash
sudo apt install gnome-software-plugin-flatpak
```

--------------------------------

### Prepare Chroot Environment for RPi Kali Linux

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Sets up a chroot environment to manage the Kali Linux installation on the Raspberry Pi's SD card. This involves mounting necessary partitions and system directories, and installing QEMU for cross-architecture emulation.

```bash
sudo mkdir -vp /mnt/chroot/
sudo mount /dev/sdX2 /mnt/chroot/
sudo mount /dev/sdX1 /mnt/chroot/boot/
sudo mount -t proc none /mnt/chroot/proc
sudo mount -t sysfs none /mnt/chroot/sys
sudo mount -o bind /dev /mnt/chroot/dev
sudo mount -o bind /dev/pts /mnt/chroot/dev/pts
sudo apt install -y qemu-user-static
sudo cp /usr/bin/qemu-aarch64-static /mnt/chroot/usr/bin/

```

--------------------------------

### Enable Kaboxer Debhelper Integration in Debian Rules

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This example demonstrates modifying the debian/rules file to enable Kaboxer's debhelper integrations by updating the `dh` command with `--with kaboxer --buildsystem=kaboxer`.

```makefile
kali@kali:~$ cat debian/rules
#!/usr/bin/make -f

%:
	dh $@ --with=kaboxer --buildsystem=kaboxer

```

--------------------------------

### Install Docker CE on Kali Linux

Source: https://www.kali.org/docs/containers/installing-docker-on-kali

Installs the latest version of Docker CE (Community Edition), Docker CLI, and containerd.io after configuring the Docker repository. This command updates the package list and then installs the specified Docker packages.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y docker-ce docker-ce-cli containerd.io
```

--------------------------------

### Install a Python Package using pipx

Source: https://www.kali.org/docs/general-use/python3-external-packages

Installs a Python package globally using pipx. This command assumes the package is available on the Python Package Index (PyPI). It also indicates that the installed application will be available in the system's PATH.

```bash
pipx install xsstrike
  installed package xsstrike 3.2.2, installed using Python 3.12.6
  These apps are now globally available
    - xsstrike
done!
```

--------------------------------

### Configure Git for User Information and Signing

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Sets global Git configuration for user name, email, and signing key. It also enables commit signing by default. Ensure user.name and user.email match your GPG key details to avoid errors. Replace the example key with your actual GPG key ID.

```bash
kali@kali:~$ git config --global user.name "First Last"
kali@kali:~$ 
kali@kali:~$ git config --global user.email email@domain.com
kali@kali:~$ 
kali@kali:~$ git config --global user.signingkey ABC123DE4567890123G4567HIJK890LM12345N6
kali@kali:~$ 
kali@kali:~$ git config --global commit.gpgsign true
kali@kali:~$
```

--------------------------------

### View Kali Offline Install Source List

Source: https://www.kali.org/docs/general-use/kali-linux-sources-list-repositories

Displays the content of the /etc/apt/sources.list file to check if the system is configured for offline installation using CD-ROM media. This is useful for diagnosing update issues.

```bash
kali@kali:~$ cat /etc/apt/sources.list
#

# deb cdrom:[Kali GNU/Linux 2020.1a _Kali-last-snapshot_ - Official amd64 DVD Binary-1 with firmware 20200213-14:56]/ kali-rolling main non-free

#deb cdrom:[Kali GNU/Linux 2020.1a _Kali-last-snapshot_ - Official amd64 DVD Binary-1 with firmware 20200213-14:56]/ kali-rolling main non-free

# This system was installed using small removable media
# (e.g. netinst, live or single CD). The matching "deb cdrom"
# entries were disabled at the end of the installation process.
# For information about how to configure apt package sources,
# see the sources.list(5) manual.
kali@kali:~$
```

--------------------------------

### Copy SSH Public Key to Clipboard

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Installs the xclip utility and copies the SSH public key to the system clipboard, making it easy to paste into remote services like GitLab.

```bash
kali@kali:~$ sudo apt install -y xclip
[...] 
kali@kali:~$ 
cat ~/.ssh/id_rsa.pub | xclip
kali@kali:~$
```

--------------------------------

### Install and Configure Desktop Environment (Bash)

Source: https://www.kali.org/docs/general-use/switching-desktop-environments

Updates the system, installs the specified Kali desktop metapackage (e.g., kali-desktop-kde), and configures the default session manager. This involves using apt for package management and update-alternatives for session configuration.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt install -y kali-desktop-kde
kali@kali:~$ 
kali@kali:~$ sudo update-alternatives --config x-session-manager
kali@kali:~$ 

```

--------------------------------

### Using dpkg to Find Package Information

Source: https://www.kali.org/docs/community/submitting-issues-kali-bug-tracker

This snippet demonstrates how to use `dpkg` commands to find information about installed packages, specifically the 'chromium' package. The output includes the package name, version, architecture, and a brief description, which can be valuable for bug reports.

```bash
kali@kali:~$ which chromium
/usr/bin/chromium
kali@kali:~$ 
type chromium
chromium is /usr/bin/chromium
kali@kali:~$ 
dpkg --search /usr/bin/chromium
chromium: /usr/bin/chromium
kali@kali:~$ 
dpkg --list chromium
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name           Version      Architecture Description
+++-==============-============-============-=================================
ii  chromium       76.0.3809.100-1 amd64       web browser
kali@kali:~$ 
dpkg --status chromium
Package: chromium
Status: install ok installed
Priority: optional
Section: web
Installed-Size: 188290
Maintainer: Debian Chromium Team <chromium@packages.debian.org>
Architecture: amd64
Source: chromium-browser
Version: 76.0.3809.100-1
[...]
kali@kali:~$ 

```

--------------------------------

### Configure Hijacker for Monitor Mode

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This snippet shows the shell commands to set up the Hijacker app for Wi-Fi monitor mode. It involves setting the LD_PRELOAD environment variable and using nexutil to configure the Wi-Fi interface. Ensure the Nexmon library is correctly placed.

```shell
LD_PRELOAD=/data/user/0/com.hijacker/files/lib/libnexmon.so
if [ `dumpsys wifi | grep “Wi-Fi is” | cut -d" " -f3` == “enabled” ]; then svc wifi disable; sleep 2; ifconfig wlan0 up; fi; nexutil -s0x613 -i -v2
```

--------------------------------

### Install Kali Default Tools

Source: https://www.kali.org/docs/cloud/linode

Installs the default set of Kali Linux tools on an existing Linode instance. This command updates the package list and then installs the 'kali-linux-default' metapackage. It assumes you have a working Kali Linux environment with apt package manager.

```bash
kali@kali:~$ sudo apt update && sudo apt install kali-linux-default -y

```

--------------------------------

### Dockerfile for hello-cli Application

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Defines a Dockerfile for the 'hello-cli' application. It specifies the base Debian image, installs Python dependencies, copies the application binary, and records the application version.

```dockerfile
FROM debian:stable-slim
RUN apt update && apt install -y \
    python3 \
    python3-prompt-toolkit
COPY ./hello /usr/bin/hello
RUN mkdir /kaboxer \
 && hello version > /kaboxer/version

```

--------------------------------

### pipx Installation with PATH Warning

Source: https://www.kali.org/docs/general-use/python3-external-packages

Illustrates the output from pipx when a newly installed application's executable directory is not found in the system's PATH. It provides guidance on how to resolve this issue.

```bash
pipx install xyz
  installed package xyz 1.0, installed using Python 3.12.6
  These apps are now globally available
    - xyz
   Note: '/home/kali/.local/bin' is not on your PATH environment variable.
    These apps will not be globally accessible until your PATH is updated.
    Run `pipx ensurepath` to automatically add it, or manually modify your
    PATH in your shell's config file (e.g. ~/.bashrc).
done!
```

--------------------------------

### Verify Mirror and Download Speed from France with curl and wget

Source: https://www.kali.org/docs/troubleshooting/download-speed-issues

This example demonstrates using `curl` to identify a mirror from France, then using `wget` to download the ISO from that mirror and report the download speed. This combined approach helps in gathering all necessary information for bug reporting, including the specific mirror and the achieved download rate.

```bash
kali@kali:~$ curl -i https://cdimage.kali.org/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
HTTP/1.1 302 Found
Server: nginx
Content-Type: text/html; charset=utf-8
Content-Length: 0
Connection: keep-alive
Cache-Control: private, no-cache
Link: <https://kali.download/base-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso>; rel=duplicate; pri=1; geo=ae
Location: https://archive-4.kali.org/kali-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso

kali@kali:~$ wget https://archive-4.kali.org/kali-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
--2025-06-18 10:56:00--  https://archive-4.kali.org/kali-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
Resolving archive-4.kali.org (archive-4.kali.org)... 2001:41d0:2:f566::, 176.31.228.102
Connecting to archive-4.kali.org (archive-4.kali.org)|2001:41d0:2:f566::|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4478939136 (4.2G) [application/octet-stream]
Saving to: ‘kali-linux-2025.4-installer-amd64.iso’

kali-linux-2025.4-installer-amd64.iso   0% [ ] 615.75K   610KB/s

kali@kali:~$
```

--------------------------------

### Clone Kernel Builder and Prepare Environment

Source: https://www.kali.org/docs/nethunter/porting-nethunter-kernel-builder

This snippet clones the Kali NetHunter kernel builder repository and navigates into the cloned directory. It's the initial step to set up the build environment.

```bash
kali@kali:~$ git clone https://gitlab.com/kalilinux/nethunter/build-scripts/kali-nethunter-kernel-builder
kali@kali:~$ cd kali-nethunter-kernel-builder/
```

--------------------------------

### Install Encryption and Boot Packages in Chroot

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Installs essential packages for disk encryption (`cryptsetup`, `lvm2`), remote unlock (`dropbear-initramfs`), and system utilities (`busybox`) within the chroot environment. It also ensures the latest Kali kernel and bootloader are installed.

```bash
sudo env LANG=C chroot /mnt/chroot/
apt update
apt install -y busybox cryptsetup dropbear-initramfs lvm2
apt install -y kalipi-kernel kalipi-bootloader kalipi-re4son-firmware

```

--------------------------------

### Mount VMware Tools ISO and Copy Installer

Source: https://www.kali.org/docs/virtualization/install-vmware-guest-tools-legacy

Mounts the VMware Tools ISO image to /media/cdrom/ and copies the VMwareTools tarball to the user's downloads directory. This prepares the installer for patching and compilation.

```bash
kali@kali:~$ sudo mkdir -p /media/cdrom/
kali@kali:~$ sudo mount /dev/cdrom /media/cdrom/
kali@kali:~$ cp -f /media/cdrom/VMwareTools-*.tar.gz ~/downloads/
```

--------------------------------

### Install Missing libaio1 Package

Source: https://www.kali.org/docs/virtualization/install-vmware-host

This snippet addresses the 'libaio missing' error that can occur when running VMware. It shows how to install the 'libaio1' package using `apt`, which is often required for VMware to function correctly.

```bash
kali@kali:~$ vmware
[AppLoader] Use shipped Linux kernel AIO access library.
An up-to-date "libaio" or "libaio1" package from your system is preferred.
kali@kali:~$ 
kali@kali:~$ sudo apt install -y libaio1
[...] 
kali@kali:~$
```

--------------------------------

### Install docker.io on Kali Linux

Source: https://www.kali.org/docs/containers/installing-docker-on-kali

Installs the 'docker.io' package, which is the container version of Docker available in Kali's repositories. This method requires using 'sudo' for Docker commands unless the user is added to the 'docker' group.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y docker.io
kali@kali:~$ sudo systemctl enable docker --now
kali@kali:~$ sudo usermod -aG docker $USER
```

--------------------------------

### Install Build Dependencies (Bash)

Source: https://www.kali.org/docs/development/rebuilding-a-package-from-source

This snippet installs the necessary build dependencies identified by 'dpkg-checkbuilddeps'. The '-y' flag automatically confirms the installation.

```bash
kali@kali:~$ sudo apt install -y dh-autoreconf libnfc-dev libssl-dev
```

--------------------------------

### Install Python Package with APT

Source: https://www.kali.org/docs/general-use/python3-external-packages

This command installs a Python package using the APT package manager. This is the preferred method if the package is available in the Kali Linux repositories.

```bash
sudo apt install faraday
```

--------------------------------

### Install adb and fastboot (Debian/Ubuntu)

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-xiaomi-mi-a3

Installs the Android Debug Bridge (adb) and fastboot tools on Debian-based systems like Kali Linux. These tools are essential for interacting with Android devices in various states.

```bash
kali@kali:~$ sudo apt update
[...] 
kali@kali:~$ sudo apt install adb fastboot
[...] 
kali@kali:~$ 

```

--------------------------------

### Install snapd on Kali Linux

Source: https://www.kali.org/docs/tools/snap

Installs the snapd package on Kali Linux using the apt package manager. This involves updating the package list first to ensure the latest version is fetched.

```bash
sudo apt update
sudo apt install -y snapd
```

--------------------------------

### Install Magisk via ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

Installs the Magisk application onto an Android device using the Android Debug Bridge (ADB). This method requires developer settings and USB debugging to be enabled on the device. It downloads the Magisk APK and then installs it.

```bash
kali@kali:~$ wget 'https://github.com/topjohnwu/Magisk/releases/download/v28.0/Magisk-v28.0.apk'
kali@kali:~$ adb install Magisk-v28.0.apk
Performing Streamed Install
Success
kali@kali:~$
```

--------------------------------

### Configure Advanced Win-KeX Seamless Mode with Icon and Start Directory

Source: https://www.kali.org/docs/wsl/win-kex

This advanced configuration enhances the Win-KeX seamless mode profile by adding a custom icon and setting a specific starting directory. The 'kali-menu.png' should be copied to the user's picture directory.

```json
{
        "guid": "{55ca431a-3a87-5fb3-83cd-11ececc031d2}",
        "hidden": false,
        "icon": "file:///c:/users/<windows user>/pictures/icons/kali-menu.png",
        "name": "Win-KeX",
        "commandline": "wsl -d kali-linux kex --sl --wtstart -s",
        "startingDirectory" : "//wsl$/kali-linux/home/<kali user>"
}
```

--------------------------------

### Build Kali ISO with Different Desktop Environments (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Demonstrates how to build Kali ISOs with various desktop environments like Gnome and KDE. The --variant option selects the desired desktop environment.

```bash
kali@kali:~/live-build-config$ # These are the different Desktop Environment build options:
kali@kali:~/live-build-config$ #./build.sh --variant {xfce,gnome,kde,mate,e17,lxde,i3} --verbose
kali@kali:~/live-build-config$

kali@kali:~/live-build-config$ # To build a Gnome ISO:
kali@kali:~/live-build-config$ ./build.sh --variant gnome --verbose
kali@kali:~/live-build-config$

kali@kali:~/live-build-config$ # To build a KDE ISO:
kali@kali:~/live-build-config$ ./build.sh --variant kde --verbose
```

--------------------------------

### Install New Package (Bash)

Source: https://www.kali.org/docs/development/rebuilding-a-package-from-source

After a successful build, this command installs the newly created Debian package. It uses 'dpkg -i' to install the .deb file, using a wildcard to match the generated package name.

```bash
kali@kali:~$ sudo dpkg -i ../libfreefare*.deb
```

--------------------------------

### Configure Custom Syslinux Boot Entry for Kali ISO

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This command configures a custom syslinux boot entry for the Kali ISO. It specifies parameters for the kernel and initrd, including a preseed file for automated installation, allowing for unattended ISO deployment.

```bash
kali@kali:~$ cat <<EOF > kali-config/common/includes.binary/isolinux/install.cfg
label install
    menu label ^Install Automated
    linux /install/vmlinuz
    initrd /install/initrd.gz
    append vga=788 -- quiet file=/cdrom/install/preseed.cfg locale=en_US keymap=us hostname=kali domain=local.lan
EOF

```

--------------------------------

### Accessing Man Pages and Help Information

Source: https://www.kali.org/docs/community/getting-help

Demonstrates how to access command-line help and documentation using man pages and alternative help flags. It also shows how to search for commands using 'apropos'.

```bash
man <command>
<command> --help
<command> -help
<command> -h
<command> -H
```

```bash
kali@kali:~$ apropos "copy file"
cp (1)               - copy files and directories
cpio (1)             - copy files to and from archives
install (1)          - copy files and set attributes
ntfscp (8)           - copy file to an NTFS volume.
kali@kali:~$ 
```

--------------------------------

### Import Kali Linux GPG Key

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Imports the official Kali Linux archive signing key using either a direct download and pipe to gpg or by fetching from a keyserver. Requires GPG to be installed.

```bash
$ wget -q -O - https://archive.kali.org/archive-key.asc | gpg --import

```

```bash
$ gpg --keyserver hkps://keys.openpgp.org --recv-key 827C8569F2518CC677FECA1AED65462EC8D5E4C5

```

--------------------------------

### Install VirtualBox Extension Pack (Kali Repos)

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Install the VirtualBox Extension Pack from Kali repositories to enable advanced features like USB 2.0/3.0 support, disk encryption, and remote desktop protocol (RDP).

```bash
kali@kali:~$ sudo apt install virtualbox-ext-pack
[...]
kali@kali:~$ 

```

--------------------------------

### Install Dependencies and Create Image Directory

Source: https://www.kali.org/docs/development/custom-efikamx-image

Installs necessary packages like kpartx and xz-utils, creates a directory for image files, and then creates an empty image file using dd. This prepares the environment for image creation.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils sharutils
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ dd if=/dev/zero of=kali-custom-efikamx.img conv=fsync bs=4M count=7000

```

--------------------------------

### Start Kali LXC Container (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Starts the LXC container named 'my-kali' in the background. This command initiates the container's operating system and makes it accessible.

```bash
kali@kali:~$ lxc-start -n my-kali -d

```

--------------------------------

### Pip Install Error: Externally Managed Environment

Source: https://www.kali.org/docs/general-use/python3-external-packages

This output shows the error message encountered when attempting to use 'pip install' for system-wide or user-specific installations on Kali Linux, indicating that the environment is externally managed and suggesting alternatives like APT or pipx.

```text
┌──(kali㉿kali)-[~]
└─$ sudo pip install xyz
error: externally-managed-environment

? This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.

    If you wish to install a non-Kali-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have pypy3-venv installed.

    If you wish to install a non-Kali-packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.

    For more information, refer to the following:
    * https://www.kali.org/docs/general-use/python3-external-packages/
    * /usr/share/doc/python3.12/README.venv

note: If you believe this is a mistake, please contact your Python
installation or OS distribution provider.  You can override this,
    at the risk of breaking your Python installation or OS, by passing
--break-system-packages.
hint: See PEP 668 for the detailed specification.


```

--------------------------------

### Update and Upgrade Kali Linux (Shell)

Source: https://www.kali.org/docs/nethunter/nethunter-rootless

Commands to update the package list and upgrade installed packages in Kali Linux, followed by an optional command to install the default Kali Linux desktop environment.

```shell
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y kali-linux-default

```

--------------------------------

### List All Snapshots using Snapper CLI

Source: https://www.kali.org/docs/installation/btrfs

This command lists all available snapshots across all configurations using the snapper command-line tool.

```bash
$ sudo snapper list -a
```

--------------------------------

### Reload and Provision Kali Linux VM with Vagrant

Source: https://www.kali.org/docs/virtualization/install-vagrant-guest-vm

This section shows commands to apply configuration changes and re-run provisioning scripts on a Vagrant-managed Kali Linux VM. 'vagrant reload' applies changes to the Vagrantfile without destroying the VM. 'vagrant provision' runs the provisioning scripts on an already running VM. 'vagrant up --provision' starts a VM and provisions it, while 'vagrant reload --provision' reboots and provisions.

```bash
kali@kali:~$ vagrant reload
kali@kali:~$ 

# To re-provision the VM:
$ vagrant provision  # provision the powered on VM
$ vagrant up --provision  # when VM is powered off, power it on then provision
$ vagrant reload --provision  # reboot the VM then provision

```

--------------------------------

### Install Kali Linux Xfce Desktop Environment

Source: https://www.kali.org/docs/general-use/xfce-faq

Installs the Kali Linux Xfce desktop environment and configures it as the default display manager. It also provides commands to switch back to GNOME or remove GNOME if desired.

```bash
sudo apt update && sudo apt install -y kali-desktop-xfce
update-alternatives --config x-session-manager
# Optional: Remove GNOME desktop environment
# apt purge --autoremove kali-desktop-gnome
```

--------------------------------

### Debian Test Control File with Test-Command

Source: https://www.kali.org/docs/development/contributing-runtime-tests

An example of a debian/tests/control file using the 'Test-Command' directive to execute a command directly as a test. This avoids the need for separate test scripts for simple commands.

```text
Test-Command: foo-cli --list --verbose
Depends: foo
Restrictions: needs-root

```

--------------------------------

### Install Magisk via TWRP using ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

Installs the Magisk application through the TWRP recovery environment, initiated via ADB commands. This involves pushing the Magisk APK to the device's storage and then instructing TWRP to install it. The process includes mounting partitions, patching the boot image, and repacking it.

```bash
kali@kali:~$ wget 'https://github.com/topjohnwu/Magisk/releases/download/v27.0/Magisk-v27.0.apk'
kali@kali:~$ adb push Magisk-v27.0.apk /sdcard/Download/Magisk-27.apk
Magisk-v27.0.apk: 1 file pushed, 0 skipped. 7.1 MB/s (12498796 bytes in 1.680s)
kali@kali:~$ 
kali@kali:~$ adb shell 'twrp install /sdcard/Download/Magisk-27.apk'
Installing zip file '/sdcard/Download/Magisk-27.apk'
Unmounting System...
***********************
 Magisk 27.0 Installer
***********************
- Mounting /system
- Device is system-as-root
- Legacy SAR, force kernel to load rootfs
- No vbmeta partition, patch vbmeta in boot image
- System-as-root, keep dm-verity
- Target image: /dev/block/mmcblk0p7
- Device platform: armeabi-v7a
- Constructing environment
- Adding addon.d survival script
- Unpacking boot image
- Checking ramdisk status
- Stock boot image detected
- Patching ramdisk
- Repacking boot image
- Flashing new boot image
- Unmounting partitions
- Done
Done processing script file
kali@kali:~$ 
kali@kali:~$ adb reboot
```

--------------------------------

### Install Podman on Debian-based Systems

Source: https://www.kali.org/docs/containers/using-kali-podman-images

Installs the Podman containerization platform on Debian-based systems using the apt package manager. This is a prerequisite for using Podman images.

```bash
kali@kali:~$ sudo apt update && sudo apt install -y podman

```

--------------------------------

### Update and Install Kali Linux Packages

Source: https://www.kali.org/docs/arm/gemini-pda

This snippet shows how to update the package list and install the default Kali Linux metapackage. It requires root privileges and an active internet connection.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$
kali@kali:~$ sudo apt install -y kali-linux-default
```

--------------------------------

### Install Python Dependencies for Radxa Zero eMMC Installation

Source: https://www.kali.org/docs/arm/radxa-zero-emmc

Installs necessary Python packages, including 'pyamlboot', which is required for interacting with the Radxa Zero in maskrom mode. This step is crucial for the Linux-based eMMC writing process.

```bash
sudo apt update
sudo apt install python3-pip
sudo pip3 install pyamlboot
```

--------------------------------

### Install Dependencies and Create Image File

Source: https://www.kali.org/docs/development/custom-raspberry-pi-image

Installs necessary packages like kpartx and xz-utils, then creates a raw disk image file of a specified size using dd. This image will serve as the container for the Raspberry Pi root filesystem and boot images.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils sharutils
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ dd if=/dev/zero of=kali-custom-rpi.img conv=fsync bs=4M count=7000

```

--------------------------------

### Install Tor and Tor Browser Launcher on Kali Linux

Source: https://www.kali.org/docs/tools/tor

This command updates the package list and installs the 'tor' and 'torbrowser-launcher' packages. Ensure you have an active internet connection. No specific input is required beyond executing the command.

```bash
sudo apt update
sudo apt install -y tor torbrowser-launcher
```

--------------------------------

### Download VMware Installer

Source: https://www.kali.org/docs/virtualization/install-vmware-host

This snippet shows how to download the VMware Workstation installer using `curl`. It specifies a user agent to mimic a browser and saves the downloaded file as 'vmware.bundle' in the Downloads directory. It also includes commands to verify the downloaded file type and size.

```bash
kali@kali:~$ sudo apt install -y curl
[...] 
kali@kali:~$ curl -A "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0" \
  -o Downloads/vmware.bundle \
  -L https://www.vmware.com/go/getworkstation-linux
kali@kali:~$ 
kali@kali:~$ file Downloads/vmware.bundle
Downloads/vmware.bundle: a bash script executable (binary data)
kali@kali:~$ 
kali@kali:~$ ls -lah Downloads/vmware.bundle
-rw-r--r-- 1 kali kali 514M Oct  3 02:13 Downloads/vmware.bundle
kali@kali:~$
```

--------------------------------

### Install Linux Kernel Headers for Kali

Source: https://www.kali.org/docs/virtualization/install-virtualbox-guest-additions-legacy

Installs the necessary Linux kernel headers required for VirtualBox Guest Additions. This command updates the package list and then installs the headers matching the currently running kernel version. Ensure you have an active internet connection.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y linux-headers-$( uname -r )
```

--------------------------------

### Download and Configure Mirror Sync Tool

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Downloads the ftpsync tool, unpacks it, and configures the mirror settings by editing the ftpsync configuration file. Key parameters like MIRRORNAME, TO, RSYNC_PATH, and RSYNC_HOST are set.

```bash
$ sudo su - archvsync
$ wget https://archive.kali.org/ftpsync.tar.gz
$ tar zxf ftpsync.tar.gz

$ whoami
archvsync
$ cp etc/ftpsync-kali.conf.sample etc/ftpsync-kali.conf
$ vim etc/ftpsync-kali.conf
$ grep -E '^[^#]' etc/ftpsync-kali.conf
MIRRORNAME=`hostname -f`
TO="/srv/mirrors/kali/"
RSYNC_PATH="kali"
RSYNC_HOST="archive.kali.org"

```

--------------------------------

### Install Yubikey Personalization Tool and Smart Card Daemon

Source: https://www.kali.org/docs/general-use/configuring-yubikeys-for-ssh-authentication

Installs the necessary tools for Yubikey personalization and smart card services on Kali Linux. This is a prerequisite for further configuration.

```bash
kali@kali:~$ sudo apt install -y yubikey-personalization scdaemon

```

--------------------------------

### Configure Build Rules in debian/rules

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet demonstrates the debian/rules file configuration for building the FinalRecon package. It uses `make` and `dh` commands, sets the Python package name, and ensures the main script is executable after installation.

```makefile
#!/usr/bin/make -f
#export DH_VERBOSE = 1
export PYBUILD_NAME=finalrecon

%:
	dh $@ --with python3

override_dh_install:
	dh_install
	chmod 0755 debian/finalrecon/usr/share/finalrecon/finalrecon.py
```

--------------------------------

### Configure Advanced Win-KeX Windowed Mode with Icon and Start Directory

Source: https://www.kali.org/docs/wsl/win-kex

This advanced configuration enhances the Win-KeX windowed mode profile by including a custom icon and specifying a starting directory within the Kali Linux environment. Ensure the 'kali-menu.png' is placed in the specified Windows user pictures directory.

```json
{
        "guid": "{55ca431a-3a87-5fb3-83cd-11ececc031d2}",
        "hidden": false,
        "icon": "file:///c:/users/<windows user>/pictures/icons/kali-menu.png",
        "name": "Win-KeX",
        "commandline": "wsl -d kali-linux kex --wtstart -s",
        "startingDirectory" : "//wsl$/kali-linux/home/<kali user>"
}
```

--------------------------------

### Install pyenv Dependencies on Kali

Source: https://www.kali.org/docs/general-use/using-eol-python-versions

Installs necessary build tools and libraries required to compile Python from source using pyenv. These dependencies ensure that Python can be successfully built and installed on the system.

```bash
kali@kali:~$ sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python3-openssl git
[...]
kali@kali:~$
```

--------------------------------

### Enable and Start Bluetooth Service (Raspberry Pi 400)

Source: https://www.kali.org/docs/arm/raspberry-pi-400

These commands enable and start the necessary services for Bluetooth functionality on the Raspberry Pi 400. `hciuart.service` is a prerequisite for the `bluetooth.service`. Running these commands ensures that Bluetooth can be used after the system boots.

```bash
kali@kali:~$ sudo systemctl enable --now hciuart.service
kali@kali:~$ sudo systemctl enable --now bluetooth.service

```

--------------------------------

### Install Kernel Compilation Packages (Bash)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Installs essential packages required for compiling the Linux kernel on Debian-based systems like Kali. These include build tools, ncurses for configuration, fakeroot for simulating root privileges, xz-utils for compression, libelf-dev for ELF file handling, libssl-dev for SSL libraries, and dwarves for debugging information.

```bash
$ sudo apt-get install build-essential libncurses5-dev fakeroot xz-utils libelf-dev libssl-dev dwarves

```

--------------------------------

### Sideload Magisk zip (adb)

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-xiaomi-mi-a3

Installs the Magisk rooting solution onto an Android device using the 'adb sideload' command. This process is performed after installing a custom ROM and while the device is in recovery mode.

```bash
kali@kali:~/Downloads$ adb devices
dea044c9    sideload

kali@kali:~/Downloads$ adb sideload Magisk-v28.1.apk
[...] 
kali@kali:~/Downloads$

```

--------------------------------

### Start Monitor Mode for WiFi (Bash)

Source: https://www.kali.org/docs/nethunter/testing-checklist

This command sequence starts monitor mode on the wlan1 interface, creating a new monitor interface named 'mon0'. It then uses airodump-ng to capture network traffic on this monitor interface.

```bash
airmon-ng start wlan1 && airodump-ng mon0
```

--------------------------------

### Update Kali Linux System

Source: https://www.kali.org/docs/virtualization/install-vmware-host

Before installing VMware, ensure your Kali Linux system is up-to-date. This involves updating the package list and performing a full upgrade. A reboot may be required if kernel updates have been installed.

```bash
kali@kali:~$ sudo apt update
[...] 
kali@kali:~$ sudo apt full-upgrade -y
[...] 
kali@kali:~$ [ -f /var/run/reboot-required ] && sudo reboot -f
kali@kali:~$
```

--------------------------------

### Helper Script for Photon Executable

Source: https://www.kali.org/docs/development/intermediate-packaging-example

A simple shell script that acts as a wrapper to execute the 'photon.py' script using python3. This script is installed in the system's binary directory.

```sh
#!/bin/sh
exec python3 /usr/share/photon/photon.py "$@"
```

--------------------------------

### Install LXC and Dependencies (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Installs the LXC package and necessary dependencies for managing containers on a Kali Linux system. This command ensures all required tools are available for containerization.

```bash
kali@kali:~$ sudo apt install -y lxc libvirt0 libpam-cgfs bridge-utils libvirt-clients libvirt-daemon-system iptables ebtables dnsmasq-base

```

--------------------------------

### Search for a Python Package using apt

Source: https://www.kali.org/docs/general-use/python3-external-packages

Demonstrates how to search for a package using the apt package manager. This is a preliminary step to check if a package is available in Kali's repositories before resorting to pipx.

```bash
apt search xsstrike
```

--------------------------------

### Install Kali NetHunter via TWRP using ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

Installs the Kali NetHunter zip package onto an Android device using TWRP recovery, initiated via ADB. This command pushes the NetHunter zip file to the device's download directory and then executes the TWRP installation command.

```bash
kali@kali:~$ adb push nethunter-*-oneplus1-los-eleven-kalifs-full.zip /sdcard/Download/nh-11.zip; adb shell 'twrp install /sdcard/Download/nh-11.zip'
[...] 
kali@kali:~$ adb reboot
```

--------------------------------

### Build Custom Kali ISO Image

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This command initiates the ISO build process using the configured `live-build` settings. The `-v` flag enables verbose output. The build can take a significant amount of time depending on system resources and internet speed.

```bash
kali@kali:~$ ./build.sh -v

```

--------------------------------

### Install Dependencies and Create Image File

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Installs necessary packages like kpartx and xz-utils, creates a directory for images, and then generates a blank image file of a specified size using dd. This file will serve as the container for the ODROID rootfs and boot images.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils uboot-mkimage
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ dd if=/dev/zero of=kali-custom-odroid.img conv=fsync bs=4M count=7000

```

--------------------------------

### View cryptmypi Kali Encrypted Basic Configuration

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Displays the content of the `cryptmypi.conf` file for the `kali-encrypted-basic` example. This configuration file contains settings for creating an encrypted Kali system, including kernel selection and SSH server options.

```bash
kali@kali:~$ cat kali-encrypted-basic/cryptmypi.conf
###############################################################################
## cryptmypi profile ##########################################################


# EXAMPLE OF A ENCRYPTED KALI CONFIGURATION
#   Will create a encrypted Kali system:
#   - during boot the encryption password will be prompted
#   - with ssh server (available after boot)
#       The id_rsa.pub public key will be added to authorized_keys
#
#   Some optional hooks are defined on stage2:
#   - "optional-sys-rootpassword" that sets root password


# General settings ------------------------------------------------------------
# You need to choose a kernel compatible with your RPi version.
#   Kali RPi images name its kernels:
#   - Re4son+ is for armv6 devices (ie. RPi1, RPi0, and RPi0w)
#   - v7+ and v8+ suffixes are for the 32bit and 64bit armv7 devices (ie. RPi 3)
#   - l+ suffix in the name means they will be ready for the RPi4.
export _KERNEL_VERSION_FILTER="v8+"

# HOSTNAME
#   Each element of the hostname must be from 1 to 63 characters long and
#   the entire hostname, including the dots, can be at most 253

```

--------------------------------

### Run Win-KeX in Window Mode

Source: https://www.kali.org/docs/wsl/win-kex

Starts Win-KeX in a dedicated window with sound support. This command can be executed either from within the Kali WSL environment or from the Windows command prompt.

```bash
kex --win -s
```

```bash
wsl -d kali-linux kex --win -s
```

--------------------------------

### Prepare ODROID Boot Partition

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This section focuses on preparing the boot partition for the ODROID. It involves copying the compiled kernel ('zImage') and the generated initrd ('uInitrd') to the boot directory. It also includes creating a 'boot.txt' file with essential boot parameters and generating a 'boot.scr' file from 'boot.txt' using the 'mkimage' tool.

```bash
kali@kali:~$ mv ~/arm-stuff/images/root/uInitrd ~/arm-stuff/images/boot/
kali@kali:~$ cp arch/arm/boot/zImage ~/arm-stuff/images/boot/
kali@kali:~$ cat <<EOF > ~/arm-stuff/images/boot/boot.txt
setenv initrd_high "0xffffffff"
setenv fdt_high "0xffffffff"
setenv bootcmd "fatload mmc 0:1 0x40008000 zImage; fatload mmc 0:1 0x42000000 uInitrd; bootm 0x40008000 0x42000000"
setenv bootargs "console=tty1 console=ttySAC1,115200n8 root=LABEL=kaliroot rootwait ro mem=2047M"
boot
EOF
kali@kali:~$ mkimage -A arm -T script -C none -n "Boot.scr for ODROID" -d ~/arm-stuff/images/boot/boot.txt ~/arm-stuff/images/boot/boot.scr

```

--------------------------------

### Install Python Application with Pipx

Source: https://www.kali.org/docs/general-use/python3-external-packages

This command installs a Python application using pipx, which automatically creates and manages an isolated virtual environment for the application. This prevents conflicts with system-wide Python packages managed by APT.

```bash
pipx install xyz
```

--------------------------------

### Install Utilities and Create Image File

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Installs necessary utilities like kpartx and xz-utils, then creates a blank image file of a specified size using dd. This image file will later contain the Kali rootfs and boot images.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils sharutils
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~/arm-stuff/images$ dd if=/dev/zero of=kali-custom-ss808.img conv=fsync bs=4M count=7000

```

--------------------------------

### Configure Docker CE Repository on Kali Linux

Source: https://www.kali.org/docs/containers/installing-docker-on-kali

Sets up the Docker CE repository on Kali Linux by adding the Docker repository to apt sources and importing the GPG key. This is necessary for installing the latest 'docker-ce' version.

```bash
kali@kali:~$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian trixie stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list
kali@kali:~$ curl -fsSL https://download.docker.com/linux/debian/gpg |
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

--------------------------------

### Update System and Download Kali Packages (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Updates the system's package list and upgrades installed packages. It then downloads the Kali archive keyring and live-build package.

```bash
$ sudo apt update
$ sudo apt full-upgrade -y
$
wget https://http.kali.org/pool/main/k/kali-archive-keyring/kali-archive-keyring_2022.1_all.deb
$ wget https://http.kali.org/pool/main/l/live-build/live-build_20230502+kali3_all.deb
```

--------------------------------

### Install Kali Metapackages using Kali-Tweaks

Source: https://www.kali.org/docs/general-use/metapackages

Instructions for using the 'kali-tweaks' tool to install metapackage groups. This involves launching the tool, navigating to the 'Metapackages' tab, selecting desired groups, and applying the changes.

```bash
kali-tweaks
```

--------------------------------

### Configure /etc/crypttab for Encrypted Partitions

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Creates or updates the /etc/crypttab file, which provides cryptsetup with the necessary options to unlock encrypted devices during the boot process. This example sets up an entry for a partition identified by its PARTUUID.

```bash
echo -e 'crypt\tPARTUUID=ed889dad-02\tnone\tluks' > /etc/crypttab
```

--------------------------------

### Manually Install Kernel Headers and Rebuild DKMS

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

This command sequence manually installs kernel headers and rebuilds DKMS modules for the latest installed kernel. It's useful for immediate application after a kernel upgrade when the automatic APT hook hasn't run yet. It includes steps to update package lists, install headers, and then rebuild DKMS modules.

```bash
# pick the highest installed kernel (not `uname -r`)
kali@kali:~$ newk=$(ls -1 /lib/modules | sort -V | tail -1)

# install headers for that kernel
kali@kali:~$ sudo apt-get update
[...]
kali@kali:~$ sudo apt-get install -y "linux-headers-$newk" || echo "linux-headers-$newk not available"
[...]
# rebuild DKMS modules for that kernel
kali@kali:~$ if command -v dkms >/dev/null;
  sudo dkms autoinstall -k "$newk"
fi

```

--------------------------------

### Install Utilities and Create Image File for CuBox

Source: https://www.kali.org/docs/development/custom-cubox-image

Installs necessary utilities (kpartx, xz-utils, sharutils) and creates a raw disk image file named 'kali-custom-cubox.img' with a size of 7000 blocks of 4MB each. This image will store the CuBox rootfs and boot images.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils sharutils
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ dd if=/dev/zero of=kali-custom-cubox.img conv=fsync bs=4M count=7000

```

--------------------------------

### Set Up Base Kali ARM rootfs with Debootstrap

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Creates the directory structure for the root filesystem and uses debootstrap to install a base ARM rootfs from Kali Linux repositories. It also copies qemu-arm-static for the second-stage chroot.

```bash
kali@kali:~$ mkdir -p ~/arm-stuff/kernel # should have already been created when setting up x-compilation
kali@kali:~$ mkdir -p ~/arm-stuff/rootfs
kali@kali:~$ cd ~/arm-stuff/rootfs/
kali@kali:~$ 
kali@kali:~$ debootstrap --foreign --arch $architecture kali-rolling kali-$architecture http://http.kali.org/kali
kali@kali:~$ cp /usr/bin/qemu-arm-static kali-$architecture/usr/bin/

```

--------------------------------

### Create wpa_supplicant.conf for Headless Wi-Fi Setup

Source: https://www.kali.org/docs/arm/raspberry-pi-4

This command generates a `wpa_supplicant.conf` file to connect to a wireless network automatically on boot. Replace `YOURNETWORK` with your Wi-Fi network name. The command will prompt for your Wi-Fi password.

```bash
wpa_passphrase YOURNETWORK > wpa_supplicant.conf
```

--------------------------------

### Install Mali Graphic Drivers Dependencies and Download Files (Shell)

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Installs essential build tools and downloads the Mali driver components and related libraries. This step ensures all necessary software is present before compilation.

```shell
kali@kali:~$ # http://malideveloper.arm.com/develop-for-mali/drivers/open-source-mali-gpus-linux-exadri2-and-x11-display-drivers/
kali@kali:~$ sudo apt install -y build-essential autoconf automake make libtool xorg xorg-dev xutils-dev libdrm-dev
kali@kali:~$ wget http://malideveloper.arm.com/downloads/drivers/DX910/r3p2-01rel0/DX910-SW-99003-r3p2-01rel0.tgz
kali@kali:~$ wget http://malideveloper.arm.com/downloads/drivers/DX910/r3p2-01rel0/DX910-SW-99006-r3p2-01rel0.tgz
kali@kali:~$ wget --no-check-certificate https://dl.dropbox.com/u/65312725/mali_opengl_hf_lib.tgz
kali@kali:~$
```

--------------------------------

### Check WSL Distribution Versions (PowerShell)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command lists all installed WSL distributions, their current state (Stopped/Running), and their WSL version. It's useful for verifying the current version of a distribution before and after an upgrade.

```powershell
wsl --list --verbose
```

--------------------------------

### Clone Kaboxer Repository

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Clones the Kaboxer source code repository from GitLab using Git. This is necessary to access example application directories like 'hello-kbx'.

```bash
kali@kali:~$ git clone https://gitlab.com/kalilinux/tools/kaboxer.git
Cloning into 'kaboxer'...
[...]

kali@kali:~$ cd kaboxer/hello-kbx

```

--------------------------------

### Configure Btrfs Subvolumes for Kali Linux

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

These commands are essential for setting up Btrfs subvolumes on the root partition during Kali Linux installation. They involve mounting, creating, and setting default subvolumes, as well as copying the fstab file.

```bash
$ mkdir -p /mnt/point/
$ mount -o subvol=/ /dev/mapper/LUKS_ROOT /mnt/point
$ cd /mnt/point/
$ btrfs subvolume create @
$ btrfs subvolume create @home
$ btrfs subvolume create @root
$ btrfs subvolume create @snapshots
$ btrfs subvolume list .
$ btrfs subvolume set-default 257 . # where 257 is the subvolume ID that was displayed for @
$ cd /
$ umount /mnt/point
$ umount /target/boot/efi # only required when booted in EFI mode
$ umount /target/boot
$ umount /target
$ mount -o subvol=@ /dev/mapper/LUKS_ROOT /target
$ mkdir -p /target/boot
$ mkdir -p /target/etc
$ mkdir -p /target/media
$ mkdir -p /target/snapshots
$ mount /dev/mapper/LUKS_BOOT /target/boot
$ mount -o subvol=@rootfs /dev/mapper/LUKS_ROOT /mnt/point
$ cp /mnt/point/etc/fstab /target/etc/fstab

```

--------------------------------

### Boot Kali ISO with QEMU (BIOS Mode)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Boots the Kali Linux Live ISO image using QEMU in BIOS mode. It utilizes the created virtual hard disk and specifies the path to the ISO file. The '-boot once=d' option ensures booting from the CD-ROM first.

```bash
kali@kali:$ qemu-system-x86_64 \
  -enable-kvm \
  -drive if=virtio,aio=threads,cache=unsafe,format=qcow2,file=/tmp/kali-test.hdd.img \
  -cdrom /home/kali/live-build-config/images/kali-linux-rolling-live-amd64.iso \
  -boot once=d

```

--------------------------------

### Install Raspberry Pi Zero 2 W Kernel Headers

Source: https://www.kali.org/docs/arm/raspberry-pi-zero-2-w

On the Raspberry Pi Zero 2 W, standard kernel header packages like `linux-headers-$(uname -r)` are not used. Instead, you need to install `linux-headers-rpi-v7` and `linux-headers-rpi-v7l`. This snippet first updates the package list and then installs the required header packages.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y linux-headers-rpi-v7 linux-headers-rpi-v7l
```

--------------------------------

### Verify NVIDIA Driver and CUDA Installation

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

Verifies that the NVIDIA driver and CUDA toolkit have been installed correctly. It uses `nvidia-smi` to display GPU status, driver version, and CUDA version, and `lspci` to confirm the NVIDIA kernel driver is in use.

```bash
kali@kali:~$ nvidia-smi
Tue Jan 28 11:37:47 2020
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 430.64       Driver Version: 430.64       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------|
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 106...  Off  | 00000000:07:00.0  On |                  N/A |
|  0%   50C    P8     7W / 120W |    116MiB /  6075MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0       807      G   /usr/lib/xorg/Xorg                           112MiB |
|    0       979      G   xfwm4                                          2MiB |
+-----------------------------------------------------------------------------+
kali@kali:~$ 
kali@kali:~$ lspci | grep -i vga
07:00.0 VGA compatible controller: NVIDIA Corporation GP106 [GeForce GTX 1060 6GB] (rev a1)
kali@kali:~$ 
kali@kali:~$ lspci -s 07:00.0 -v
[...]        Kernel driver in use: nvidia        Kernel modules: nvidia
kali@kali:~$ 

```

--------------------------------

### Patch VMware Modules for Newer Kernels (Bash)

Source: https://www.kali.org/docs/virtualization/install-vmware-host

This script patches VMware modules to support newer kernels in Kali Linux. It clones the vmware-host-modules repository, applies necessary patches, and installs the modules. Ensure git is installed before running.

```bash
kali@kali:~$ sudo apt install -y git
kali@kali:~$ sudo git clone \
  -b workstation-$( grep player.product.version /etc/vmware/config | sed '/.*"(.*)".*/ s//1/g' ) \
  https://github.com/mkubecek/vmware-host-modules.git \
  /opt/vmware-host-modules/
kali@kali:~$ cd /opt/vmware-host-modules/
kali@kali:/opt/vmware-host-modules$ sudo make
kali@kali:/opt/vmware-host-modules$ grep -q pte_offset_map ./vmmon-only/include/pgtbl.h && \
  sudo sed -i 's/pte_offset_map/pte_offset_kernel/' ./vmmon-only/include/pgtbl.h
kali@kali:/opt/vmware-host-modules$ sudo make install
```

--------------------------------

### Check PATH Environment Variable

Source: https://www.kali.org/docs/general-use/python3-external-packages

Displays the current value of the PATH environment variable. This is used to verify if the directory where pipx installs executables (~/.local/bin) is included, allowing globally installed Python applications to be run from the terminal.

```bash
echo $PATH
/home/kali/.local/bin:[...]
```

--------------------------------

### Launch msfconsole and Verify Database Status (Shell)

Source: https://www.kali.org/docs/tools/starting-metasploit-framework-in-kali

This command launches the Metasploit Framework console (`msfconsole`) quietly (`-q`). After launching, the `db_status` command is used to verify that the console is connected to the PostgreSQL database.

```shell
kali@kali:~$ msfconsole -q
msf6 > 
msf6 > db_status
[*] Connected to msf. Connection type: postgresql.
msf6 > 

```

--------------------------------

### Install and Use Python Packages with Pip for Python 2.7

Source: https://www.kali.org/docs/general-use/using-eol-python-versions

This snippet demonstrates how to install a Python package, such as 'requests', using the installed pip for Python 2.7. It also shows the general command for running a Python script using the specific Python version.

```shell
kali@kali:~$ python2.7 -m pip install requests
kali@kali:~$ python2.7 <file>
```

--------------------------------

### Create TFTP User and Set Directory Permissions (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This command creates a system user named 'tftp' and then recursively changes the ownership of the /opt/pxe/ and /tftpboot/ directories to this new user. This is a security measure to ensure proper access control for TFTP operations.

```bash
kali@kali:~$ sudo adduser --system --home /opt/pxe/ tftp
adduser: Warning: The home dir /opt/pxe/ you specified already exists.
Adding system user `tftp' (UID 117) ...
Adding new user `tftp' (UID 117) with group `nogroup' ...
adduser: The home directory `/opt/pxe/' already exists.  Not touching this directory.
adduser: Warning: The home directory `/opt/pxe/' does not belong to the user you are currently creating.
kali@kali:~$ 
kali@kali:~$ sudo chown -R tftp: /opt/pxe/ /tftpboot/
```

--------------------------------

### Install ADB and Fastboot on Kali Linux Host

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

Installs the Android Debug Bridge (ADB) and fastboot tools on a Kali Linux host system. These tools are essential for interacting with the Android device in various states, including recovery and bootloader modes, and for flashing firmware.

```bash
kali@kali:~$ sudo apt update
[...]
kali@kali:~$ sudo apt install --yes adb fastboot
[...]
kali@kali:~$ 
```

--------------------------------

### Build Package with sbuild (Initial Attempt)

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This command attempts to build a Debian package using sbuild. It requires the project's changes to be committed to Git. The example shows an error due to uncommitted changes.

```bash
kali@kali:~/kali/packages/instaloader$ gbp buildpackage --git-builder=sbuild
gbp:error: Can't determine package type: Failed to read changelog: can't get HEAD:debian/changelog:fatal: path 'debian/changelog' exists on disk, but not in 'HEAD'
kali@kali:~/kali/packages/instaloader$
```

--------------------------------

### Configure Build Environment and Clone Config (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Sets up the debootstrap script for Kali and clones the live-build-config repository from GitLab. This prepares the environment for building the Kali ISO.

```bash
$ cd /usr/share/debootstrap/scripts/
$ (echo "default_mirror http://http.kali.org/kali"; sed -e "s/debian-archive-keyring.gpg/kali-archive-keyring.gpg/g" sid) > /tmp/kali
$ sudo mv /tmp/kali .
$ sudo ln -s kali kali-rolling
$
$ cd ~/
$ git clone https://gitlab.com/kalilinux/build-scripts/live-build-config.git
$
$ cd live-build-config/
```

--------------------------------

### Download and Install Pip for Python 2.7

Source: https://www.kali.org/docs/general-use/using-eol-python-versions

This snippet shows how to download the get-pip.py script using curl and then execute it with python2.7 to install pip. This is a common method for setting up pip in isolated Python environments.

```shell
kali@kali:~$ curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
kali@kali:~$ python2.7 get-pip.py
```

--------------------------------

### Install Utilities and Create Image File for Beaglebone Black

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Installs necessary utilities (kpartx, xz-utils, sharutils) and creates a raw disk image file for the Beaglebone Black. The image size is set to 7000 blocks of 4MB each.

```bash
kali@kali:~$ sudo apt install -y kpartx xz-utils sharutils
kali@kali:~$ mkdir -p ~/arm-stuff/images/
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ dd if=/dev/zero of=kali-custom-bbb.img conv=fsync bs=4M count=7000

```

--------------------------------

### Configure Advanced Win-KeX ESM Mode with Icon and Start Directory

Source: https://www.kali.org/docs/wsl/win-kex

This advanced configuration customizes the Win-KeX ESM mode profile with a custom icon and a designated starting directory. The 'kali-menu.png' icon file needs to be placed in the user's picture directory.

```json
{
        "guid": "{55ca431a-3a87-5fb3-83cd-11ecedd031d2}",
        "hidden": false,
        "icon": "file:///c:/users/<windows user>/pictures/icons/kali-menu.png",
        "name": "Win-KeX",
        "commandline": "wsl -d kali-linux kex --esm --wtstart -s",
        "startingDirectory" : "//wsl$/kali-linux/home/<kali user>"
}
```

--------------------------------

### Create and Set Permissions for TFTP Boot Script (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This script automates the download and extraction of Kali Linux Netboot images. It creates a directory, downloads the latest netboot.tar.gz, extracts it, and cleans up the archive. The script is then made executable and owned by root.

```bash
kali@kali:~$ sudo mkdir -pv /opt/pxe/
mkdir: created directory '/opt/pxe/'
kali@kali:~$ 
kali@kali:~$ cat <<'EOF' | sudo tee /opt/pxe/tftpboot.sh
#!/usr/bin/env sh

## Our desired path for the PXE image to be saved to
tftp=/tftpboot

## amd64 (64-bit)
arch=amd64

## Complete remove and create the previous directory containing the PXE image
rm -rfv "${tftp:?}"/*

## Download the newest version
wget "https://http.kali.org/kali/dists/kali-rolling/main/installer-${arch}/current/images/netboot/netboot.tar.gz" -O "${tftp}/netboot.tar.gz"

## Extract
tar -zxpvf /tftpboot/netboot.tar.gz -C "${tftp}"

## Clean up
rm -v "${tftp}/netboot.tar.gz"
EOF
kali@kali:~$ 
kali@kali:~$ sudo chmod 0700 /opt/pxe/tftpboot.sh
kali@kali:~$ 
kali@kali:~$ sudo chown root: /opt/pxe/tftpboot.sh
```

--------------------------------

### Install kali-root-login Package on Kali Linux

Source: https://www.kali.org/docs/general-use/enabling-root

Installs the 'kali-root-login' package using apt. This package modifies system configuration files to enable root login for GNOME (GDM3) and KDE display managers. It does not require any input and will automatically handle the necessary file diversions and installations.

```bash
kali@kali:~$ sudo apt -y install kali-root-login
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  kali-root-login
0 upgraded, 1 newly installed, 0 to remove and 1516 not upgraded.
Need to get 6,776 B of archives.
After this operation, 33.8 kB of additional disk space will be used.
Get:1 http://kali.download/kali kali-rolling/main amd64 kali-root-login all 2019.4.0 [6,776 B]
Fetched 6,776 B in 1s (10.9 kB/s)
Selecting previously unselected package kali-root-login.
(Reading database ... 333464 files and directories currently installed.)
Preparing to unpack .../kali-root-login_2019.4.0_all.deb ...
Adding 'diversion of /etc/gdm3/daemon.conf to /etc/gdm3/daemon.conf.original by kali-root-login'
Adding 'diversion of /etc/pam.d/gdm-password to /etc/pam.d/gdm-password.original by kali-root-login'
Adding 'diversion of /etc/pam.d/gdm-autologin to /etc/pam.d/gdm-autologin.original by kali-root-login'
Adding 'diversion of /etc/pam.d/lightdm-autologin to /etc/pam.d/lightdm-autologin.original by kali-root-login'
Adding 'diversion of /etc/pam.d/sddm to /etc/pam.d/sddm.original by kali-root-login'
Adding 'diversion of /etc/sddm.conf to /etc/sddm.conf.original by kali-root-login'
Unpacking kali-root-login (2019.4.0) ...
Setting up kali-root-login (2019.4.0) ...
Installing /usr/share/kali-root-login/daemon.conf as /etc/gdm3/daemon.conf
Installing /usr/share/kali-root-login/gdm-password as /etc/pam.d/gdm-password
Installing /usr/share/kali-root-login/gdm-autologin as /etc/pam.d/gdm-autologin
Installing /usr/share/kali-root-login/lightdm-autologin as /etc/pam.d/lightdm-autologin
Installing /usr/share/kali-root-login/sddm as /etc/pam.d/sddm
Installing /usr/share/kali-root-login/sddm.conf as /etc/sddm.conf
kali@kali:~$
```

--------------------------------

### Install TigerVNC Server

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This snippet shows the command to install the TigerVNC standalone server package using apt. TigerVNC is a popular VNC server implementation that will be used to provide graphical access to Kali.

```bash
kali@kali:~$ sudo apt install -y tigervnc-standalone-server
kali@kali:~$ 

```

--------------------------------

### Configure Kali Linux VM Network and Provisioning with Vagrant

Source: https://www.kali.org/docs/virtualization/install-vagrant-guest-vm

This Ruby code snippet demonstrates advanced Vagrantfile configurations for a Kali Linux VM. It includes setting up a forwarded port (guest:80 to host:8080), a private network with a static IP, disabling the VirtualBox GUI, allocating more memory, and provisioning the VM with a shell script to update packages and install 'crowbar'.

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "kalilinux/rolling"

  # Create a forwarded port
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network. In VirtualBox, this is a Host-Only network
  config.vm.network "private_network", ip: "192.168.33.10"

  # VirtualBox specific settings
  config.vm.provider "virtualbox" do |vb|
    # Hide the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end

  # Provision the machine with a shell script
  config.vm.provision "shell", inline: <<-EOF
    sudo apt update
    sudo apt install -y crowbar
  EOF
end

```

--------------------------------

### Install DKMS for Kernel Module Management

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Install the `dkms` package. Dynamic Kernel Module Support (DKMS) is used to automatically rebuild VirtualBox's kernel modules whenever the Linux kernel is updated, ensuring VirtualBox remains functional across kernel upgrades.

```bash
kali@kali:~$ sudo apt install dkms
[...]
kali@kali:~$ 

```

--------------------------------

### Configure XFCE (LightDM) for Read-Only Snapshots

Source: https://www.kali.org/docs/installation/btrfs

This command modifies the LightDM configuration file to enable booting into read-only snapshots for XFCE desktop environment by setting a specific option.

```bash
# Reconfigure lightdm to allow booting into read-only snapshots
$ sudo sed -i 's/^#user-authority-in-system-dir=false/user-authority-in-system-dir=true/' /etc/lightdm/lightdm.conf
$
$ sudo reboot
```

--------------------------------

### Install dbus-x11 for WSL RDP/Xfce

Source: https://www.kali.org/docs/general-use/xfce-with-rdp

For users setting up RDP and Xfce on Windows Subsystem for Linux (WSL), the 'dbus-x11' package is a necessary dependency. This command installs the package, enabling proper communication for the desktop environment and RDP client to connect.

```shell
kali@kali:~$ sudo apt install -y dbus-x11
kali@kali:~$ 

```

--------------------------------

### Install openssh-client-gssapi for GSS-API Support

Source: https://www.kali.org/docs/general-use/ssh-configuration

Installs the `openssh-client-gssapi` package to ensure support for GSS-API authentication methods in the SSH client. This package is intended to reduce the attack surface of the main `openssh-client` package by separating GSS-API functionality. It is pre-installed in recent Kali Linux versions but can be manually installed if needed.

```bash
kali@kali:~$ sudo apt update
[...] 
kali@kali:~$ sudo apt install -y openssh-client-gssapi
[...] 
kali@kali:~$
```

--------------------------------

### Automating ISO Image Mirroring with Cron

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Sets up a daily cron job to automatically mirror Kali Linux ISO images. This involves copying a sample configuration file, editing it to specify the destination directory, and then adding a cron entry to schedule the mirroring script. The `crontab -e` command opens the crontab for editing, and `crontab -l` lists the current cron jobs.

```bash
$ whoami
archvsync
$ cp etc/mirror-kali-images.conf.sample etc/mirror-kali-images.conf
$ vim etc/mirror-kali-images.conf
$ grep -E '^[^#]' etc/mirror-kali-images.conf
TO="/srv/mirrors/kali-images/"
$ crontab -e
$ crontab -l
# m h  dom mon  dow   command
39 3 * * * ~/bin/mirror-kali-images

```

--------------------------------

### Manage Kali Linux Podman Containers

Source: https://www.kali.org/docs/containers/using-kali-podman-images

Demonstrates how to list all Podman containers (including stopped ones), start a stopped container, and attach to a running container. These commands are essential for managing the lifecycle of Kali Linux containers.

```bash
kali@kali:~$ podman ps -a
kali@kali:~$ podman start 7df5f0dbe6b7
kali@kali:~$ podman attach 7df5f0dbe6b7

```

--------------------------------

### Kali Rolling Repository Configuration

Source: https://www.kali.org/docs/general-use/kali-branches

This snippet shows the standard configuration for the kali-rolling repository in the /etc/apt/sources.list file. It enables users to access the primary repository for most Kali Linux users, providing updated packages verified for installability.

```bash
deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
```

--------------------------------

### Build Package with sbuild (After Installing dh-python)

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This command attempts to build the package again after installing the 'dh-python' dependency. It shows the build process continuing past the previous error, although Lintian may still report issues.

```bash
kali@kali:~/kali/packages/instaloader$ gbp buildpackage --git-builder=sbuild
gbp:info: Exporting 'HEAD' to '/home/kali/kali/build-area/instaloader-tmp'
gbp:info: Moving '/home/kali/kali/build-area/instaloader-tmp' to '/home/kali/kali/build-area/instaloader-4.4.4'
gbp:info: Performing the build
dh clean --with python3 --buildsystem=pybuild
[...] 

+------------------------------------------------------------------------------+
| Package contents                                                             |
+------------------------------------------------------------------------------+

[...] 

Install lintian build dependencies (apt-based resolver)
-------------------------------------------------------

[...] 

E: instaloader source: source-is-missing [docs/_static/bootstrap-4.1.3.bundle.min.js]
W: instaloader: no-manual-page [usr/bin/instaloader]

E: Lintian run failed (runtime error)

[...] 

+------------------------------------------------------------------------------+
| Summary                                                                      |

```

--------------------------------

### Update Kali Linux System

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Before installing VirtualBox, ensure your Kali Linux system is up-to-date. This involves updating the package list, performing a full upgrade, and optionally rebooting if required.

```bash
kali@kali:~$ sudo apt update
[...]
kali@kali:~$ 
kali@kali:~$ sudo apt full-upgrade -y
[...]
kali@kali:~$ 
kali@kali:~$ [ -f /var/run/reboot-required ] && sudo reboot -f
kali@kali:~$ 

```

--------------------------------

### Build Kali Live ISO

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Navigates to the live-build-config directory and executes the build.sh script with verbose output to generate a Kali Live ISO image. The process downloads required packages and may take a significant amount of time.

```bash
kali@kali:~$ cd live-build-config/
kali@kali:~/live-build-config$ ./build.sh --verbose
[...] 
***
GENERATED KALI IMAGE: ./images/kali-linux-rolling-live-amd64.iso
***
kali@kali:~$ 

```

--------------------------------

### Configure dnsmasq for PXE Boot

Source: https://www.kali.org/docs/installation/network-pxe

Configures dnsmasq to enable DHCP, TFTP, and PXE booting. It sets the DHCP range, specifies the boot file (pxelinux.0), defines the TFTP root directory, and configures DNS servers and gateway options for the network environment.

```bash
cat <<EOF | sudo tee /etc/dnsmasq.conf
interface=eth0
dhcp-range=192.168.101.100,192.168.101.200,12h
dhcp-boot=pxelinux.0
enable-tftp
tftp-root=/tftpboot/
dhcp-option=3,192.168.101.1
dhcp-option=6,8.8.8.8,8.8.4.4
EOF
```

--------------------------------

### Configure btrfs Subvolume Mounts in fstab

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This snippet illustrates the lines added to the fstab file for mounting various btrfs subvolumes, including root, home, and snapshots. It also includes mount options optimized for SSDs, such as 'ssd' and 'compress=lzo'. The example shows how to differentiate between LUKS_ROOT and LUKS_BOOT for different mount points.

```shell
/dev/mapper/LUKS_ROOT /               btrfs   defaults,noatime,ssd,compress=lzo,subvol=@              0 0
/dev/mapper/LUKS_BOOT /boot           ext4    defaults,noatime                                                    0 1
/dev/mapper/LUKS_ROOT /home           btrfs   defaults,noatime,ssd,compress=lzo,subvol=@home      0 2
/dev/<bos>/LUKS_ROOT /root           btrfs   defaults,noatime,ssd,compress=lzo,subvol=@root      0 3
/dev/mapper/LUKS_ROOT /snapshots      btrfs   defaults,noatime,ssd,compress=lzo,subvol=@snapshots 0 4
/dev/mapper/LUKS_SWAP none            swap    sw                                                                          0 0
```

--------------------------------

### Update Kali System using APT

Source: https://www.kali.org/docs/general-use/metapackages

Commands to update the Kali Linux system's package list and upgrade installed packages. This is a recommended prerequisite before installing new metapackages to ensure compatibility and avoid potential conflicts.

```bash
sudo apt update
sudo apt full-upgrade -y
```

--------------------------------

### Configure, Compile, and Install Linux Kernel for ARM

Source: https://www.kali.org/docs/development/custom-cubox-image

This snippet details the process of configuring the kernel using 'make menuconfig', compiling it efficiently using multiple cores, installing modules to a specified path, and creating a 'uImage' for ARM architecture. It assumes a standard Linux build environment.

```bash
kali@kali:~$ make menuconfig
kali@kali:~$ make -j$( cat /proc/cpuinfo|grep processor | wc -l )
kali@kali:~$ make modules_install INSTALL_MOD_PATH=~/arm-stuff/images/root
kali@kali:~$ make uImage
kali@kali:~$ cp arch/arm/boot/uImage ~/arm-stuff/images/root/boot
```

--------------------------------

### Create Fake LUKS Filesystem for Initramfs

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This process involves creating a dummy LUKS file and opening it with cryptsetup to ensure cryptsetup is included in the initramfs. It requires formatting the fake LUKS partition and then mounting it.

```bash
dd if=/dev/zero of=/tmp/fakeroot.img bs=1M count=20
exit
```

```bash
sudo cryptsetup luksFormat /mnt/chroot/tmp/fakeroot.img
sudo cryptsetup luksOpen /mnt/chroot/tmp/fakeroot.img crypt
sudo mkfs.ext4 /dev/mapper/crypt
```

--------------------------------

### Flash boot image (fastboot)

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-xiaomi-mi-a3

Flashes a custom boot image, specifically 'boot_los22.img', to both boot partitions (boot_a and boot_b) of an Android device using fastboot. This is typically done to install a custom recovery or kernel.

```bash
kali@kali:~$ cd Downloads/
[...] 
kali@kali:~/Downloads$ fastboot flash boot_a boot_los22.img
[...] 
kali@kali:~/Downloads$ fastboot flash boot_b boot_los22.img
[...] 
kali@kali:~/Downloads$

```

--------------------------------

### Install Missing dh-python Dependency

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This command installs the 'dh-python' package, which is a common missing dependency causing build failures in Debian packaging, specifically related to Python integration with debhelper.

```bash
kali@kali:~/kali/packages/instaloader$ sudo apt install -y dh-python
kali@kali:~/kali/packages/instaloader$
```

--------------------------------

### List and Resume Exited Kali Linux Docker Container

Source: https://www.kali.org/docs/containers/using-kali-docker-images

This section shows how to list all Docker containers, including exited ones, and then start a previously stopped container using its ID. After starting, you can attach to it.

```bash
docker container list --all
docker start d36922fa21e8
```

--------------------------------

### Enable and Start Bluetooth Service on Raspberry Pi 4

Source: https://www.kali.org/docs/arm/raspberry-pi-4

These commands enable and start the necessary services for Bluetooth functionality on the Raspberry Pi 4. `hciuart.service` is a prerequisite for the `bluetooth.service`.

```bash
sudo systemctl enable --now hciuart.service
sudo systemctl enable --now bluetooth.service
```

--------------------------------

### Install Kali Packages within Container (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Updates the package list and installs the 'kali-linux-default' meta-package inside the 'my-kali' LXC container. This ensures the container has a standard set of Kali Linux tools.

```bash
kali@kali:~$ lxc-attach -n my-kali apt update
kali@kali:~$ lxc-attach -n my-kali apt install -y kali-linux-default

```

--------------------------------

### Configure and Compile Kernel (Bash)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Navigates to the kernel source directory and initiates the kernel configuration and compilation process. 'make menuconfig' opens a text-based interface for customizing kernel options. The 'make deb-pkg' command compiles the kernel and creates Debian packages, automatically handling necessary patches and setting a local version and package version.

```bash
$ cd ~/src/linux-source-5.15/
$ make menuconfig
$ make clean
$ make deb-pkg LOCALVERSION=-custom KDEB_PKGVERSION=$(make kernelversion)-1

```

--------------------------------

### Install Custom Kernel Package (Bash)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Installs the newly compiled custom Linux kernel Debian package. This package includes an initial RAM disk capable of decrypting LUKS partitions and places necessary files on the /boot partition for GRUB2 to find, simplifying the boot process for encrypted systems.

```bash
$ sudo dpkg -i ~/src/linux-image-5.15.5-custom_5.15.5-1_amd64.deb

```

--------------------------------

### Create ext4 Filesystem on USB Partition

Source: https://www.kali.org/docs/usb/usb-persistence

This command formats the newly created partition (e.g., `/dev/sdX3`) with an ext4 file system and labels it 'persistence'. The `mkfs.ext4` command is used for this purpose, and the output shows the filesystem creation details.

```bash
kali@kali:~$ usb=/dev/sdX
kali@kali:~$ 
kali@kali:~$ sudo mkfs.ext4 -L persistence ${usb}3
mke2fs 1.47.2 (1-Jan-2025)
Creating filesystem with 14114816 4k blocks and 3530752 inodes
Filesystem UUID: ccb5cd13-3675-40ac-8b81-a684802a8dd0
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624, 11239424

Allocating group tables: done
Writing inode tables: done
Creating journal (65536 blocks): done
Writing superblocks and filesystem accounting information: done

kali@kali:~$ 

```

--------------------------------

### Install PipeWire Audio Metapackage

Source: https://www.kali.org/docs/troubleshooting/no-sound

If audio issues persist after upgrading to Kali 2023.2 and rebooting, this command installs the `pipewire-audio` metapackage. This may resolve problems related to PipeWire's audio functionality. A subsequent reboot is advised.

```bash
kali@kali:~$ sudo apt install --mark-auto -y pipewire-audio

```

--------------------------------

### Enable Virtual Machine Platform Feature (Command Prompt)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command enables the 'VirtualMachinePlatform' Windows feature, which is a prerequisite for running WSL 2. It requires administrator privileges. The '/all' flag ensures all sub-features are enabled, and '/norestart' prevents an immediate reboot.

```cmd
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

--------------------------------

### Patch and Compile VMware Tools

Source: https://www.kali.org/docs/virtualization/install-vmware-guest-tools-legacy

Navigates to the vmware-tools-patches directory and executes the untar-and-patch-and-compile.sh script. This script handles the patching, compilation, and installation of VMware Tools.

```bash
kali@kali:~$ cd /opt/vmware-tools-patches/
kali@kali:/opt/vmware-tools-patches$ ./untar-and-patch-and-compile.sh
```

--------------------------------

### Install Packages in Kali GUI Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Updates package lists and installs essential Kali Linux and Xfce desktop packages within the running GUI container. This ensures the container has the necessary software for a graphical environment.

```bash
kali@kali:~$ lxc exec gui-kali -- apt update
kali@kali:~$ lxc exec gui-kali -- apt install -y kali-linux-default
kali@kali:~$ lxc exec gui-kali -- apt install -y kali-desktop-xfce
```

--------------------------------

### Build NetHunter Kernel Installer Zip

Source: https://www.kali.org/docs/nethunter/porting-nethunter

This snippet details the process of building the NetHunter kernel installer zip file after adding your compiled kernel to the repository. It uses a Python script and requires specifying the device codename and Android version.

```bash
kali@kali:~$ cd kali-nethunter-installer/
kali@kali:~$ ./build.py -i -k your_device_codename --your_android_version
```

--------------------------------

### Configure GNOME (GDM) for Read-Only Snapshots

Source: https://www.kali.org/docs/installation/btrfs

This section provides steps to reconfigure GNOME's display manager (GDM) to allow booting into read-only snapshots by creating separate subvolumes for GDM and AccountService directories and updating fstab.

```bash
# Reconfigure gdm to allow booting into read-only snapshots
# GDM needs to have write access to "/var/lib/gdm3" and "/var/lib/AccountService" during login.
# We have to create additional subvolumes for them:

$ mount # Pick your main partition, </dev/sda1> in our example, replace </dev/sda1> it with yours
$ sudo mount </dev/sda1> /mnt
$ sudo btrfs subvolume create /mnt/@var@lib@gdm3
$ sudo btrfs subvolume create /mnt/@var@lib@AccountsService

$ sudo mv /var/lib/gdm3/* /var/lib/gdm3/.* /mnt/@var@lib@gdm3
$ sudo mv /var/lib/AccountsService/* /var/lib/AccountsService/.* /mnt/@var@lib@AccountsService/

$ sudo vi /etc/fstab # Add the following (substitute the <UUID> with yours)

# /var/lib/gdm3 was on /dev/sda1 during installation
UUID=<dc1ca012-9349-4fcf-b761-ca323379b019> /var/lib/gdm3   btrfs   defaults,subvol=@var@lib@gdm3 0       0

# /var/lib/AccountsService was on /dev/sda1 during installation
UUID=<dc1ca012-9349-4fcf-b761-ca323379b019> /var/lib/AccountsService   btrfs   defaults,subvol=@var@lib@AccountsService 0       0

# Reboot for the changes to take effect
$ sudo reboot
```

--------------------------------

### Install Kali Linux Kernel Build Dependencies

Source: https://www.kali.org/docs/development/recompiling-the-kali-linux-kernel

Installs the necessary build tools and libraries required for compiling the Linux kernel on Kali Linux. This includes essential packages like 'build-essential' and 'libncurses5-dev'.

```bash
kali@kali:~$ sudo apt install -y build-essential libncurses5-dev fakeroot xz-utils

```

--------------------------------

### Install Kali Packages within LXD Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Updates the package list and installs the 'kali-linux-default' and 'kali-desktop-xfce' packages inside the running Kali LXD container 'my-kali'. This command is executed remotely against the container.

```bash
kali@kali:~$ lxc exec my-kali -- apt update
kali@kali:~$ lxc exec my-kali -- apt install -y kali-linux-default kali-desktop-xfce

```

--------------------------------

### Push Optional Magisk Modules to Device

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

These commands push the Magisk Overlayfs and PlayIntegrityFix modules to the Android device's SD card, making them available for installation through the Magisk app.

```bash
adb push magisk-overlayfs-release.zip /sdcard/
adb push PlayIntegrityFix_v3.3-inject-manual.zip /sdcard/
```

--------------------------------

### Check WSL Kernel Installation (WMI)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command uses Windows Management Instrumentation (WMI) to check if the 'Windows Subsystem for Linux Update' package is installed. This is relevant for ensuring the WSL kernel is correctly set up. It queries the Win32_Product class for the specific software name.

```powershell
Get-WmiObject -Class Win32_Product | Where-Object {$_.Name -eq "Windows Subsystem for Linux Update"}
```

--------------------------------

### Create TFTP Root Directory

Source: https://www.kali.org/docs/installation/network-pxe

Creates the directory '/tftpboot/' which will serve as the root for TFTP transfers. This directory will store the Kali Linux Netboot images required for PXE booting.

```bash
sudo mkdir -pv /tftpboot/
```

--------------------------------

### Initiate Kali Pi Build Script

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Command to execute the `cryptmypi.sh` script to build an encrypted Kali Linux system. It requires root privileges and specifies the example configuration file to use.

```bash
sudo ./cryptmypi.sh examples/kali-encrypted-basic
```

--------------------------------

### Install Python 2.7.18 using pyenv

Source: https://www.kali.org/docs/general-use/using-eol-python-versions

Installs Python version 2.7.18 using pyenv. This command downloads the source code for Python 2.7.18 and compiles it, making it available for use on the system.

```bash
kali@kali:~$ pyenv install 2.7.18
Downloading Python-2.7.18.tar.xz...
-> https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tar.xz
Installing Python-2.7.18...
Installed Python-2.7.18 to /home/kali/.pyenv/versions/2.7.18

kali@kali:~$
```

--------------------------------

### Add EFI Partition Entry to fstab

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This snippet shows how to add an entry to the /etc/fstab file to correctly mount the EFI system partition. It requires the PARTUUID of the target USB drive's EFI partition. This ensures the system boots from the correct EFI partition, especially when installing to a USB drive.

```shell
PARTUUID=<whatever> /boot/efi vfat umask=0077 0 1
```

--------------------------------

### Image Creation and Installation for ODROID-C2

Source: https://www.kali.org/docs/arm/odroid-c2

This snippet demonstrates the command to create a Kali Linux image for the ODROID-C2 using `xzcat` and `dd`. It requires a Kali Linux environment and a microSD card or eMMC module. The process will overwrite the target storage device.

```bash
xzcat images/kali-linux-2025.4-odroid-c2-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Set Default WSL Version to 2 (PowerShell)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command sets the default version for new WSL installations to version 2. It's a prerequisite for ensuring newly installed Linux distributions utilize WSL 2 features. No specific inputs are required, and the output confirms successful completion.

```powershell
wsl --set-default-version 2
```

--------------------------------

### Build Kali ISO using Live Build Scripts

Source: https://www.kali.org/docs/development/generate-updated-kali-iso

Navigates to the live build configuration directory and executes commands to clean, configure, and build a Kali Linux ISO image. 'lb clean --purge' removes previous build artifacts, 'lb config' sets up the build environment, and 'lb build' starts the ISO generation process.

```bash
kali@kali:~$ cd live-build-config/
kali@kali:~$ lb clean --purge
kali@kali:~$ lb config
kali@kali:~$ lb build

```

--------------------------------

### Display Partition Table with cgpt show

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This command displays the current partition list and their attributes, including labels, types, UUIDs, and boot priorities. It's useful for verifying the partition setup after making changes.

```bash
kali@kali:~$ cgpt show /dev/sdX
```

--------------------------------

### Check Installed OpenCL ICD Loaders (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command lists installed packages related to OpenCL ICD loaders, helping to identify potential conflicts or confirm the presence of NVIDIA or generic loaders. It uses `dpkg -l` to query the package database and `grep` to filter for relevant entries.

```bash
kali@kali:~$ dpkg -l |  grep -i icd
ii  nvidia-egl-icd:amd64                 430.64-5                        amd64        NVIDIA EGL installable client driver (ICD)
ii  nvidia-opencl-icd:amd64              430.64-5                        amd64        NVIDIA OpenCL installable client driver (ICD)
ii  nvidia-vulkan-icd:amd64              430.64-5                        amd64        NVIDIA Vulkan installable client driver (ICD)
ii  ocl-icd-libopencl1:amd64             2.2.12-2                        amd64        Generic OpenCL ICD Loader
ii  ocl-icd-opencl-dev:amd64             2.2.12-2                        amd64        OpenCL development files
kali@kali:~$
```

--------------------------------

### Add Kali CD-ROM Repository

Source: https://www.kali.org/docs/general-use/kali-linux-sources-list-repositories

Adds the Kali Linux CD-ROM as a package source using the 'apt-cdrom add' command. This command scans the inserted media and updates the sources.list file to include it, enabling installations from the disc.

```bash
kali@kali:~$ sudo apt-cdrom add
Using CD-ROM mount point /media/cdrom/
Identifying... [ea19ff4bedaa6c8f4662c0e8c58ed44c-2]
Scanning disc for index files...
Found 2 package indexes, 0 source indexes, 0 translation indexes and 0 signatures
This disc is called:
'Kali GNU/Linux 2020.1a _Kali-last-snapshot_ - Official amd64 DVD Binary-1 with firmware 20200213-14:56'
Reading Package Indexes... Done
Writing new source list
Source list entries for this disc are:
deb cdrom:[Kali GNU/Linux 2020.1a _Kali-last-snapshot_ - Official amd64 DVD Binary-1 with firmware 20200213-14:56]/ kali-rolling main non-free
Repeat this process for the rest of the CDs in your set.
kali@kali:~$
```

--------------------------------

### Enable WSL features using PowerShell

Source: https://www.kali.org/docs/wsl/wsl-preparations

This PowerShell command enables the 'Microsoft-Windows-Subsystem-Linux' and 'VirtualMachinePlatform' optional features online. This is a prerequisite for WSL 2 installation. The command prompts for a restart to finalize the changes.

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux,VirtualMachinePlatform
```

--------------------------------

### Extract and Clean Up Netboot Image

Source: https://www.kali.org/docs/installation/network-pxe

Extracts the contents of the downloaded 'netboot.tar.gz' file into the '/tftpboot/' directory. It then removes the original tarball to keep the directory clean.

```bash
sudo tar -zxpvf /tftpboot/netboot.tar.gz -C /tftpboot
sudo rm -v /tftpboot/netboot.tar.gz
```

--------------------------------

### Instaloader Python Version and Requirements

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This Python code snippet from setup.py specifies the minimum Python version required for Instaloader (>= 3.5) and lists its core dependency, 'requests' (>= 2.4). It also includes a conditional dependency for Windows users.

```python
#!/usr/bin/env python3
[...] 
if sys.version_info < (3, 5):
    sys.exit('Instaloader requires Python >= 3.5.')

requirements = ['requests>=2.4']

if platform.system() == 'Windows' and sys.version_info < (3, 6):
    requirements.append('win_unicode_console')
[...] 
    install_requires=requirements,
    python_requires='>=3.5',
[...]
```

--------------------------------

### Sideload LineageOS zip (adb)

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-xiaomi-mi-a3

Installs a LineageOS ROM zip file onto an Android device using the 'adb sideload' command. This method is commonly used when the device is in recovery mode and connected via ADB.

```bash
kali@kali:~/Downloads$ adb devices
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
dea044c9    sideload

kali@kali:~/Downloads$ adb sideload lineage-22.0-20241114-UNOFFICIAL-laurel_sprout.zip
[...] 
kali@kali:~/Downloads$

```

--------------------------------

### Unlock Encrypted Partitions with cryptsetup

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This command sequence is used to unlock encrypted partitions on a target USB drive during the Kali Linux installation. It requires the device path of the encrypted partitions and assigns logical volume names for access.

```bash
$ cryptsetup open /dev/sdb1 LUKS_BOOT
$ cryptsetup open /dev/sdb4 LUKS_SWAP
$ cryptsetup open /dev/sdb5 LUKS_ROOT

```

--------------------------------

### Add VirtualBox Oracle Repository

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Add the VirtualBox repository to your APT sources list. This allows your system to find and install VirtualBox packages directly from Oracle's official distribution channel. Ensure to use the correct Debian version (e.g., 'bullseye') and architecture ('amd64').

```bash
kali@kali:~$ echo "deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian bullseye contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
kali@kali:~$ 

```

--------------------------------

### Setup ARM Cross-Compilation Environment

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Downloads and extracts the Linaro ARM cross-compilation toolchain and sets the CC environment variable. This is a prerequisite for building the ARM kernel on a non-ARM development environment.

```bash
kali@kali:~$ cd ~/arm-stuff/
kali@kali:~$ wget https://launchpad.net/linaro-toolchain-binaries/trunk/2013.03/+download/gcc-linaro-arm-linux-gnueabihf-4.7-2013.03-20130313_linux.tar.bz2
kali@kali:~$ tar -xjf gcc-linaro-arm-linux-gnueabihf-4.7-2013.03-20130313_linux.tar.bz2
kali@kali:~$ export CC=`pwd`/gcc-linaro-arm-linux-gnueabihf-4.7-2013.03-20130313_linux/bin/arm-linux-gnueabihf-
```

--------------------------------

### List Compiled Kernel Packages (Bash)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Lists the generated Debian kernel package files in the parent directory. This command helps identify the exact filenames of the compiled kernel image and headers, which are needed for the installation step.

```bash
$ ls ../*.deb

```

--------------------------------

### Update Packages and Install Kernel Headers

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

Steps to update system packages and install the correct kernel headers for the running kernel, which is often necessary after system upgrades or when dealing with driver issues. This is typically performed from a TTY session.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y "linux-headers-$(uname -r)" || echo "headers not available for $(uname -r)"
```

--------------------------------

### Push Nexmon Module to Device

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This command transfers the Nexmon S10 module zip file to the Android device's SD card using ADB, preparing it for installation via the Magisk app.

```bash
adb push nexmon-s10.zip /sdcard/
```

--------------------------------

### Verify GPG Key Fingerprint

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Displays the fingerprint of the imported Kali Linux GPG key to confirm its authenticity. Requires GPG to be installed.

```bash
$ gpg --fingerprint 827C8569F2518CC677FECA1AED65462EC8D5E4C5

```

--------------------------------

### Formatting Encrypted and Unencrypted USB Partitions

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This section covers formatting the prepared partitions on the USB drive. It includes formatting the LUKS-encrypted boot partition with ext4, the EFI system partition with FAT16, the LUKS-encrypted swap partition, and the LUKS-encrypted root partition with btrfs.

```bash
$ sudo mkfs.ext4 -L boot /dev/mapper/LUKS_BOOT
$ sudo mkfs.vfat -F 16 -n EFI-SP /dev/sda3
$ sudo mkswap -L swap /dev/mapper/LUKS_SWAP
$ sudo mkfs.btrfs -L root /dev/mapper/LUKS_ROOT
```

--------------------------------

### Import VirtualBox GPG Keys

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

Import the necessary GPG keys for the Oracle VirtualBox third-party repository. This step is crucial for verifying the authenticity of the packages downloaded from Oracle's servers.

```bash
kali@kali:~$ curl -fsSL https://www.virtualbox.org/download/oracle_vbox_2016.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/oracle_vbox_2016.gpg
[...]
kali@kali:~$ curl -fsSL https://www.virtualbox.org/download/oracle_vbox.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/oracle_vbox.gpg
[...]
kali@kali:~$ 

```

--------------------------------

### Install Raspberry Pi Kernel Headers

Source: https://www.kali.org/docs/arm/raspberry-pi

These commands update the package list and install the necessary kernel headers for the Raspberry Pi image. This is required for building external kernel modules. The specific package name is `linux-headers-rpi-v6`.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y linux-headers-rpi-v6
```

--------------------------------

### Install openssh-client-ssh1 for Legacy SSH Support

Source: https://www.kali.org/docs/general-use/ssh-configuration

Installs the `openssh-client-ssh1` package to restore support for SSHv1 protocol and DSA keys, which have been removed from newer OpenSSH versions. This is useful for connecting to older or legacy SSH servers. The package provides `ssh1`, `scp1`, and `ssh-keygen1` binaries.

```bash
kali@kali:~$ sudo apt update
[...] 
kali@kali:~$ sudo apt install -y openssh-client-ssh1
[...] 
kali@kali:~$ dpkg --listfiles openssh-client-ssh1 | grep bin/
/usr/bin/scp1
/usr/bin/ssh-keygen1
/usr/bin/ssh1
kali@kali:~$ ssh1 -V
OpenSSH_7.5p1 Debian-17, OpenSSL 3.3.2 3 Sep 2024
kali@kali:~$
```

--------------------------------

### Build 64-bit ARM Kernel Toolchain and Compile

Source: https://www.kali.org/docs/nethunter/porting-nethunter

This snippet shows how to clone the GCC toolchain for 64-bit ARM devices (aarch64), set the appropriate environment variables, and start the kernel compilation. This is necessary for modern 64-bit Android devices.

```bash
kali@kali:~$ git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 -b android10-release toolchain64
kali@kali:~$ export ARCH=arm64
kali@kali:~$ export SUBARCH=arm64
kali@kali:~$ export CROSS_COMPILE=`pwd`/toolchain64/bin/aarch64-linux-android-
kali@kali:~$ make your_device_codename
kali@kali:~$ make -j$(nproc)
```

--------------------------------

### Copy Custom Kernel Configuration (Bash)

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

Copies an existing kernel configuration file to be used for the new compilation. If a custom '.config' file is available, it's placed in the kernel source directory. Alternatively, it shows how to copy the configuration of the currently running kernel (e.g., 'config-5.14.0-kali4-amd64') as a starting point for the new '.config' file.

```bash
$ cp /boot/config-5.14.0-kali4-amd64 ~/src/linux-source-5.15/.config

```

--------------------------------

### Rebuild DKMS Modules

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

Command to rebuild installed DKMS modules for the currently running kernel. This is a crucial step after installing kernel headers or updating the kernel to ensure that third-party modules (like NVIDIA drivers) are compatible.

```bash
sudo dkms autoinstall -k "$(uname -r)" || true
```

--------------------------------

### Enable WSL features using DISM

Source: https://www.kali.org/docs/wsl/wsl-preparations

These DISM commands enable the 'VirtualMachinePlatform' and 'Microsoft-Windows-Subsystem-Linux' features on Windows. These are prerequisites for installing WSL 2. The commands are run from an Administrator command prompt and require a system restart to complete.

```batch
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all
```

--------------------------------

### Define Stage 1 Hooks for Encryption

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Defines the custom Stage 1 profile hooks. The `stage1_hooks` function is called during the build process. If not defined, a prompt will be displayed. This example calls `stage1profile_encryption`.

```bash
stage1_hooks(){
    stage1profile_encryption
}
```

--------------------------------

### Install Kali Linux to microSD Card on Pinebook Pro

Source: https://www.kali.org/docs/arm/pinebook-pro

This command uses `xzcat` to decompress the Kali Linux image and `dd` to write it to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss on other drives. The `bs=4M` option sets the block size for faster writing, and `status=progress` shows the writing progress.

```bash
$ xzcat kali-linux-2025.4-pinebook-pro-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress

```

--------------------------------

### Make zz-cryptsetup Hook Executable

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Sets the executable permission for the 'zz-cryptsetup' initramfs hook script. This allows mkinitramfs to run the hook during the initramfs generation process.

```bash
chmod +x /etc/initramfs-tools/hooks/zz-cryptsetup
```

--------------------------------

### Backup and Replace Btrfs Root Subvolume

Source: https://www.kali.org/docs/installation/btrfs

This section details the process of backing up the current root subvolume ('@') and then creating a new writable snapshot from a read-only snapshot. This effectively rolls back the system to a previous state.

```bash
sudo mv /mnt/@ /mnt/@_old
sudo btrfs subvolume snapshot /mnt/@.snapshots/6/snapshot /mnt/@
```

--------------------------------

### Import Kali Linux rootfs to WSL

Source: https://www.kali.org/docs/wsl/wsl-preparations

This method involves importing a pre-generated Kali Linux root filesystem (tar.gz) into WSL. It requires the rootfs file to be present and uses 'wsl --import' to create a new WSL distribution. The command specifies the distribution name, the directory for its data, and the path to the rootfs file.

```bash
C:\Users\Win\Downloads>dir
[...]
05/04/2023  21:12    <DIR>          .
05/04/2023  21:12    <DIR>          ..
05/04/2023  21:11       217,859,650 kali-linux-rolling-wsl-rootfs-amd64.tar.gz
               1 File(s)    217,859,650 bytes
               2 Dir(s)  40,346,128,384 bytes free

C:\Users\Win\Downloads>
wsl --list --verbose
Windows Subsystem for Linux has no installed distributions.
Distributions can be installed by visiting the Microsoft Store:
https://aka.ms/wslstore
C:\Users\Win\Downloads>

C:\Users\Win\Downloads>wsl --import kali-wsl  wsl-test  .\kali-linux-rolling-wsl-rootfs-amd64.tar.gz
C:\Users\Win\Downloads>
C:\Users\Win\Downloads>dir
[...]
05/04/2023  21:13    <DIR>          .
05/04/2023  21:13    <DIR>          ..
05/04/2023  21:11       217,859,650 kali-linux-rolling-wsl-rootfs-amd64.tar.gz
05/04/2023  21:13    <DIR>          wsl-test
               1 File(s)    217,859,650 bytes
               3 Dir(s)  39,582,310,400 bytes free

C:\Users\Win\Downloads>
```

--------------------------------

### Modify Dropbear Initramfs Script for Networking Delay (Bash)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This modification to `/usr/share/initramfs-tools/scripts/init-premount/dropbear` introduces a 5-second delay before starting the Dropbear SSH server. This ensures that networking is properly initialized before Dropbear attempts to run, preventing potential connection issues. This change may need to be reapplied after `dropbear-initramfs` package updates.

```bash
[ "$BOOT" != nfs ] || configure_networking
sleep 5
run_dropbear &
echo $! >/run/dropbear.pid

```

--------------------------------

### Link Init in Rootfs

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Creates a symbolic link named 'init' in the root of the mounted root filesystem, pointing to '/sbin/init'. This ensures that the system correctly identifies and executes the init process upon boot.

```bash
kali@kali:~$ cd ~/arm-stuff/images/root/
kali@kali:~$ ln -s /sbin/init init

```

--------------------------------

### Define Symbolic Links in debian/links

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet defines symbolic links in the debian/links file. It creates a symlink from the installed Python script to a location in the system's PATH, making the `finalrecon` command directly executable.

```text
usr/share/finalrecon/finalrecon.py usr/bin/finalrecon
```

--------------------------------

### Configure Sbuild to Get a Shell on Build Failure

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Sets up sbuild to automatically launch a shell within the build environment when a build fails. This is achieved by defining the 'build-failed-commands' in the sbuild configuration file, allowing for post-mortem debugging.

```perl
# get a shell when the build fails
$external_commands = {
  "build-failed-commands" => [ [ '%SBUILD_SHELL' ] ],
};

```

--------------------------------

### Initial GitHub Watch File Configuration

Source: https://www.kali.org/docs/development/intro-to-packaging-example

An initial configuration for a debian/watch file targeting GitHub releases. It includes filename mangling to standardize tarball names but may not correctly sort pre-release versions.

```text
version=4
opts=filenamemangle=s/.+\/v?(\d\S+)\.tar\.gz/instaloader-$1\.tar\.gz/ \
  https://github.com/instaloader/instaloader/tags .*/v?(\d\S+)\.tar\.gz

```

--------------------------------

### Run Airodump-ng with Nexmon

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This command initiates the airodump-ng tool within a Kali Nethunter chroot environment to capture Wi-Fi traffic. The LD_PRELOAD environment variable is essential for loading the Nexmon shared library.

```bash
$ export LD_PRELOAD=/lib/kalilibnexmon.so
$ airodump-ng wlan0
```

--------------------------------

### Automate VMware Module Updates with Kernel Updates (Bash)

Source: https://www.kali.org/docs/virtualization/install-vmware-host

This script configures a kernel install hook to automatically re-patch VMware modules whenever the Kali Linux kernel is updated. It clones the necessary modules and runs make commands to ensure compatibility. This requires root privileges.

```bash
kali@kali:~$ sudo tee /etc/kernel/install.d/99-vmmodules.install << EOF
#!/bin/bash

export LANG=C

COMMAND="$1"
KERNEL_VERSION="${2:-$( /usr/bin/uname -r )}"
BOOT_DIR_ABS="$3"
KERNEL_IMAGE="$4"

VMWARE_VERSION=$(/usr/bin/grep player.product.version /etc/vmware/config | /usr/bin/sed '/.*"(.*)".*/ s//1/g')

ret=0

{
    [ -z "${VMWARE_VERSION}" ] && exit 0

    /usr/bin/git clone -b workstation-"${VMWARE_VERSION}" https://github.com/mkubecek/vmware-host-modules.git /opt/vmware-host-modules-"${VMWARE_VERSION}"/
    cd /opt/vmware-host-modules-"${VMWARE_VERSION}"/

    /usr/bin/make VM_UNAME="${KERNEL_VERSION}"
    /usr/bin/make install VM_UNAME="${KERNEL_VERSION}"

    ((ret+=$?))

} || {
    echo "Unknown error occurred."
    ret=1

}

exit ${ret}
EOF
kali@kali:~$
```

--------------------------------

### Install Kali Linux Image to microSD Card using dd

Source: https://www.kali.org/docs/arm/banana-pro

This command uses the dd utility to write a compressed Kali Linux image file to a microSD card. Ensure you replace '/dev/sdX' with the correct device path for your microSD card, as an incorrect path can lead to data loss on other drives. The xzcat command decompresses the image on the fly.

```bash
xzcat images/kali-linux-2025.4-banana-pro-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Configure sbuild for Isolated Builds

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Configures sbuild, a tool for building packages in an isolated environment. This setup enables building 'Architecture: all' packages, building source packages, disabling host source cleaning, enabling lintian with informational tags, and using the 'unshare' backend for chroot mode.

```perl
kali@kali:~$ mkdir -p ~/.config/sbuild/
kali@kali:~$ 
kali@kali:~$ cat <<'EOF' > ~/.config/sbuild/config.pl
# build 'Architecture: all' packages
$build_arch_all = 1;
# build the source package
$build_source = 1;
# do not run the clean target on the host
$clean_source = 0;
# run lintian, show informational tags
$run_lintian = 1;
$lintian_opts = ['-I'];

# enable network access during builds
$enable_network = 1;

# use the unshare backend
$chroot_mode = "unshare";
# keep the chroot tarball for a week
$unshare_mmdebstrap_auto_create = 1;
$unshare_mmdebstrap_keep_tarball = 1;
$unshare_mmdebstrap_max_age = 604800;
# perform the builds in /var/tmp/
$unshare_tmpdir_template = "/var/tmp/sbuild.XXXXXXXXXX";
EOF
```

--------------------------------

### Manage Kali LXD Container Lifecycle

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Provides commands to manage the lifecycle of an LXD container named 'my-kali'. Includes starting, stopping, and removing the container.

```bash
lxc start my-kali
lxc stop my-kali
lxc destroy my-kali

```

--------------------------------

### Download Kali PXE Netboot Images

Source: https://www.kali.org/docs/installation/network-pxe

Downloads the Kali Linux Netboot image (netboot.tar.gz) for the amd64 architecture from the official Kali repository. The image is saved to the '/tftpboot/' directory, preparing it for TFTP serving.

```bash
# 64-bit:
sudo wget https://http.kali.org/kali/dists/kali-rolling/main/installer-amd64/current/images/netboot/netboot.tar.gz -P /tftpboot/
```

--------------------------------

### Configure Win-KeX Windowed Mode in Windows Terminal

Source: https://www.kali.org/docs/wsl/win-kex

This configuration sets up a basic Windows Terminal profile for Win-KeX in windowed mode with sound enabled. It defines the GUID, name, and the command to execute WSL with the specified Kali Linux distribution and kex command.

```json
{
      "guid": "{55ca431a-3a87-5fb3-83cd-11ececc031d2}",
      "hidden": false,
      "name": "Win-KeX",
      "commandline": "wsl -d kali-linux kex --wtstart -s"
}
```

--------------------------------

### Launch Kali Linux LXD Container on Ubuntu Host

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Launches a Kali Linux container named 'my-kali' using the 'kali/current/amd64' image from the LXD image server. This command assumes LXD has been installed and initialized.

```bash
kali@kali:~$ lxc launch images:kali/current/amd64 my-kali

```

--------------------------------

### Auto-install Kernel Headers and Rebuild DKMS with APT Hook

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

This script adds an APT hook to automatically install kernel headers and rebuild DKMS modules for the newest kernel. It ensures that DKMS-backed modules remain synchronized after kernel updates, preventing graphical session failures. Failures in header installation or module building are ignored to prevent blocking system upgrades.

```bash
kali@kali:~$ sudo tee /etc/apt/apt.conf.d/99-kernel-headers-dkms >/dev/null <<'EOF'
DPkg::Post-Invoke {"bash -c 'set -e; newk=$(ls -1 /lib/modules 2>/dev/null | sort -V | tail -1); if [ -n $newk ] && [ ! -d /usr/src/linux-headers-$newk ]; then echo [apt] Installing headers for $newk >&2; apt-get -y install linux-headers-$newk || true; fi; if command -v dkms >/dev/null; then dkms autoinstall -k $newk || true; fi'"};
EOF
kali@kali:~$ 

```

--------------------------------

### Install Raspberry Pi Kernel Headers

Source: https://www.kali.org/docs/arm/raspberry-pi-64-bit

This command updates the package list and installs the necessary kernel headers for Raspberry Pi devices, specifically `linux-headers-rpi-2712` and `linux-headers-rpi-v8`. These headers are required for building external kernel modules and are included by default in Kali Raspberry Pi images, but can be reinstalled if removed.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt install -y linux-headers-rpi-2712 linux-headers-rpi-v8
```

--------------------------------

### Configure Shared Container for Multi-Component Applications

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This configuration within `components` for a 'gui' component sets `reuse_container: true`, indicating that this component should run within the same container as other components, facilitating a shared container setup.

```yaml
components:
  [...]
  gui:
    [...]
    reuse_container: true

```

--------------------------------

### Display Network Interface Configuration (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This command displays the IP address configuration for all network interfaces. It is used to verify the IP address of the 'eth0' interface, which is essential for identifying potential IP range conflicts with the DHCP server.

```bash
kali@kali:~$ ip a
```

--------------------------------

### Identify and Mount Btrfs Root Subvolume

Source: https://www.kali.org/docs/installation/btrfs

This snippet shows how to find the physical partition containing Btrfs subvolumes and then mount the root subvolume ('@') to a temporary location. This is the first step in accessing and manipulating snapshots.

```bash
mount | grep 'subvol='
sudo mount /dev/sda2 -o subvol=/ /mnt
```

--------------------------------

### Initial rsync Synchronization for Kali Mirror

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Performs an initial synchronization of the Kali package repository and ISO images from a remote mirror. This is done using the `rsync` command with specific flags for archive mode, preserving hard links, and preserving permissions. The `&` symbol runs the command in the background.

```bash
$ whoami
archvsync
$ rsync -qaH ftp.halifax.rwth-aachen.de::kali /srv/mirrors/kali/ &
$ rsync -qaH ftp.halifax.rwth-aachen.de::kali-images /srv/mirrors/kali-images/ &

```

--------------------------------

### Clone VMware Tools Patches Repository

Source: https://www.kali.org/docs/virtualization/install-vmware-guest-tools-legacy

Clones the vmware-tools-patches Git repository from GitHub to the /opt/vmware-tools-patches/ directory. This repository contains scripts and patches required for the installation process.

```bash
kali@kali:~$ sudo git clone https://github.com/rasa/vmware-tools-patches.git /opt/vmware-tools-patches/
```

--------------------------------

### Rollback to a Previous Snapshot

Source: https://www.kali.org/docs/installation/btrfs

This sequence of commands details the process of rolling back the system to a previous snapshot. It involves identifying the root partition, mounting it, backing up the current root subvolume, and then creating a new read-write snapshot from the desired read-only snapshot.

```bash
# get the device that contains your "/" subvolume and remember it for the next step:
mount | grep 'subvol=/@)'

# mount your root partition (replace "/dev/sda2" with yours from above):
sudo mount /dev/sda2 -o subvol=/ /mnt

# Move the old root away:
sudo mv /mnt/@ /mnt/@_badroot

# Roll back to a previous snapshot by creating a read-write copy of it as "@":
sudo btrfs subvolume snapshot /mnt/@.snapshots/XXXXX/snapshot /mnt/@

# That's it, reboot:
sudo reboot -f

```

--------------------------------

### Blacklist Nouveau Driver for NVIDIA Installation

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

This procedure disables the open-source `nouveau` graphics driver, which is a prerequisite for installing proprietary NVIDIA drivers. It involves unloading the module for the current session, persistently blacklisting it by creating a configuration file, and rebuilding the initramfs to ensure the changes take effect on the next boot.

```bash
# unload nouveau for the running session (may fail if in use)
kali@kali:~$ sudo modprobe -r nouveau || true
[...]
# blacklist nouveau persistently
kali@kali:~$ echo "blacklist nouveau" | sudo tee /etc/modprobe.d/blacklist-nouveau.conf

# rebuild initramfs so the change takes effect on next boot
kali@kali:~$ sudo update-initramfs -u
[...]

```

--------------------------------

### Configure Approx Proxy Mappings

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Defines the remote repository mappings for the 'approx' caching proxy. This configuration snippet shows how to add Kali's repository alongside Debian's, ensuring 'approx' knows where to fetch packages from.

```ini
debian          http://ftp.debian.org/debian
debian-security	http://security.debian.org/debian-security
kali            http://kali.download/kali

```

--------------------------------

### Check for Python Package Availability with APT

Source: https://www.kali.org/docs/general-use/python3-external-packages

This command searches the Kali Linux APT repositories for a package. It's recommended to check if a desired Python application is available through APT before resorting to pipx.

```bash
apt search faraday | grep ^faraday
```

--------------------------------

### Rebuild Latest Kali Image with Specific Version (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Builds the latest Kali image using the 'kali-last-snapshot' distribution. This command specifies installer options, a target version, and a subdirectory for the output.

```bash
kali@kali:~$ time ./build.sh \
  --verbose \
  --installer \
  --distribution kali-last-snapshot \
  --version 2025.4 \
  --subdir kali-2025.4
[...]
***
GENERATED KALI IMAGE: ./images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
***
kali@kali:~$
```

--------------------------------

### Include Nessus Debian Package in Kali ISO Build

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This command places a Nessus Debian package (.deb) into the `packages.chroot` directory. This ensures that the Nessus package is included in the final Kali ISO build, making it available after installation.

```bash
kali@kali:~$ mkdir -p kali-config/common/packages.chroot/
kali@kali:~$ mv Nessus-*amd64.deb kali-config/common/packages.chroot/

```

--------------------------------

### Exit Chroot Environment

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Command to exit the chroot environment after manual modifications or setup.

```shell
kali@kali:~$ exit
```

--------------------------------

### Pull and Run Kali Linux Podman Image

Source: https://www.kali.org/docs/containers/using-kali-podman-images

Pulls the Kali Linux rolling release image and starts an interactive, TTY-enabled container. This allows direct interaction with the Kali environment within Podman.

```bash
kali@kali:~$ podman pull kali-rolling
kali@kali:~$ podman run --tty --interactive kali-rolling

```

--------------------------------

### Import Pre-built Kali VM Disk Image in Proxmox

Source: https://www.kali.org/docs/virtualization/install-proxmox-guest-vm

This process imports a pre-built Kali Linux QCOW2 disk image into Proxmox VE for use as a virtual machine. It involves renaming the downloaded image, finding its location, and using the `qm importdisk` command to add it as a virtual disk to a new VM. Ensure the VM ID and storage name are correct for your Proxmox setup.

```bash
find / -name kali-linux-2025.4-qemu-amd64.iso
mv kali-linux-2025.4-qemu-amd64.iso kali-linux-2025.4-qemu-amd64.qcow2
qm importdisk 108 kali-linux-2025.4-qemu-amd64.qcow2 local-lvm
```

--------------------------------

### Define Stage 2 Optional Hooks for Root Password

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Defines optional Stage 2 hooks, which are called during the stage 2 build by the `stage2-runoptional` hook. This example calls `myhooks` with the argument `optional-sys-rootpassword`.

```bash
stage2_optional_hooks(){
    myhooks "optional-sys-rootpassword"
}
```

--------------------------------

### Basic Kali Vagrantfile Configuration

Source: https://www.kali.org/docs/virtualization/customizing-kali-vagrant

This snippet shows the default Vagrantfile configuration for a Kali Linux virtual machine. It specifies the box to be used, which is 'kalilinux/rolling'. This is a fundamental setup for initializing a Kali environment with Vagrant.

```ruby
Vagrant.configure("2") do |config|

  config.vm.box = "kalilinux/rolling"





end

```

--------------------------------

### List Kernel Modules and Configure Bootloader

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This snippet demonstrates how to list available kernel modules in the /lib/modules directory and append an initramfs configuration to the /boot/config.txt file. This is crucial for ensuring the correct kernel and initramfs are loaded on boot.

```bash
ls -l /lib/modules/ | awk -F" " '{print $9}'
echo "initramfs initramfs.gz followkernel" >> /boot/config.txt
```

--------------------------------

### Remove mesa-opencl-icd (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command removes the 'mesa-opencl-icd' package using `apt`. This is a necessary step if the package is found to be installed and may cause conflicts with the NVIDIA OpenCL driver.

```bash
kali@kali:~$ sudo apt remove mesa-opencl-icd
kali@kali:~$
```

--------------------------------

### Boot Kali ISO with QEMU (UEFI Mode)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Boots the Kali Linux Live ISO image using QEMU in UEFI mode. This configuration includes the necessary OVMF firmware files for UEFI booting, alongside the virtual hard disk and ISO image. The UEFI firmware files are set to read-only.

```bash
kali@kali:$ qemu-system-x86_64 \
  -enable-kvm \
  -drive if=virtio,aio=threads,cache=unsafe,format=qcow2,file=/tmp/kali-test.hdd.img \
  -drive if=pflash,format=raw,readonly,file=/usr/share/OVMF/OVMF_CODE.fd \
  -drive if=pflash,format=raw,readonly,file=/usr/share/OVMF/OVMF_VARS.fd \
  -cdrom /home/kali/live-build-config/images/kali-linux-rolling-live-amd64.iso \
  -boot once=d

```

--------------------------------

### Update Kali Linux System

Source: https://www.kali.org/docs/cloud/digitalocean

Updates the package list and performs a full upgrade of the installed packages on a Kali Linux system. This ensures all software is up-to-date.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ sudo apt full-upgrade -y
```

--------------------------------

### Build App and Scripts Updater Image for OnePlus 7

Source: https://www.kali.org/docs/nethunter/building-nethunter

This command builds an updater image containing NetHunter apps and scripts for a OnePlus 7 device running Android 10. It uses the specified kernel and Android version. The output is a zip file for updating an existing installation.

```bash
kali@kali:~/kali-nethunter-installer$ python3 build.py -k oneplus7-oos --ten

```

--------------------------------

### Debian Rules File for Python Package Build

Source: https://www.kali.org/docs/development/intermediate-packaging-example

Configures the build process for the 'photon' Python package using debhelper. It specifies the package name and uses the python3 build system, without needing a separate setup.py.

```makefile
#!/usr/bin/make -f
#export DH_VERBOSE = 1
export PYBUILD_NAME=photon

%:
	dh $@ --with python3
```

--------------------------------

### Install Kali Linux to eMMC on Pinebook Pro

Source: https://www.kali.org/docs/arm/pinebook-pro

This command writes the Kali Linux image to the Pinebook Pro's internal eMMC storage. It uses `xzcat` for decompression and `dd` for writing. Replace `/dev/mmcblk1` with the correct eMMC device path, as selecting the wrong device will result in data loss. The `bs=4M` flag optimizes write speed, and `status=progress` displays the operation's progress.

```bash
$ xzcat kali-linux-2025.4-pinebook-pro-arm64.img.xz | sudo dd of=/dev/mmcblk1 bs=4M status=progress

```

--------------------------------

### Check VirtualMachinePlatform Feature Status (PowerShell)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This PowerShell command checks if the 'VirtualMachinePlatform' optional feature is installed on your Windows system. This is a crucial step for WSL 2 functionality. It outputs a table indicating the feature's status.

```powershell
Get-WindowsOptionalFeature -Online | Where-Object {$_.FeatureName -eq "VirtualMachinePlatform"} | Format-Table
```

--------------------------------

### Manually Install/Upgrade Kept-Back Packages

Source: https://www.kali.org/docs/troubleshooting/handling-common-apt-errors

Handles cases where APT holds back a package, often due to potential conflicts or removals of other packages. Explicitly installing the kept-back package can reveal the dependencies involved and allow for manual confirmation of removals.

```bash
kali@kali:~$ sudo apt full-upgrade
[...] The following packages have been kept back:
  kali-desktop-xfce
[...]
```

```bash
kali@kali:~$ sudo apt install kali-desktop-xfce
[...] The following packages will be REMOVED:
  pipewire-media-session
The following packages will be upgraded:
  [...] kali-desktop-xfce [...]
Do you want to continue? [Y/n] n
```

--------------------------------

### Check dnsmasq Service Status (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This command checks the current status of the dnsmasq service. It helps determine if the service is running and displays recent log entries, which can be crucial for diagnosing network boot issues.

```bash
kali@kali:~$ sudo systemctl status dnsmasq
```

--------------------------------

### Create Kernel Boot Configuration Files

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This snippet creates two configuration files, 'config-sd' and 'config-usb', in the /tmp directory. These files contain kernel boot parameters tailored for booting from an SD card or a USB drive, respectively, specifying console output, root device, and filesystem type.

```bash
kali@kali:~$ echo "console=tty1 debug verbose root=/dev/mmcblk1p3 rootwait rw rootfstype=ext4" > /tmp/config-sd
kali@kali:~$ echo "console=tty1 debug verbose root=/dev/sda3 rootwait rw rootfstype=ext4" > /tmp/config-usb
```

--------------------------------

### Shutdown Kali Linux VM

Source: https://www.kali.org/docs/cloud/digitalocean

Shuts down the Kali Linux virtual machine. This command is typically run after all setup and cleanup operations are completed, preparing the system for image creation.

```bash
kali@kali:~$ poweroff
```

--------------------------------

### Resolve Broken Packages with 'apt full-upgrade'

Source: https://www.kali.org/docs/troubleshooting/handling-common-apt-errors

Addresses situations where 'apt upgrade' fails due to unmet dependencies or conflicts. 'apt full-upgrade' attempts to resolve these by installing new packages or removing existing ones if necessary to complete the upgrade.

```bash
kali@kali:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following packages have unmet dependencies:
 libwacom9 : Depends: libwacom-common (= 2.2.0-1) but 1.8-2 is to be installed
E: Broken packages
```

```bash
kali@kali:~$ sudo apt full-upgrade
# ... (output showing resolution) ...
```

--------------------------------

### Compile EfikaMX Kernel and Modules

Source: https://www.kali.org/docs/development/custom-efikamx-image

Clones the kernel source, sets up the ARM architecture and cross-compilation environment, configures the kernel using 'efikamx_defconfig' and 'menuconfig', compiles the kernel and modules, and installs them into the image's root filesystem. It also copies the compiled kernel image and creates a boot script.

```bash
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/
kali@kali:~$ cd ~/arm-stuff/kernel/
kali@kali:~$ git clone --depth 1 https://github.com/genesi/linux-legacy.git
kali@kali:~$ cd linux-legacy/
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/arm-eabi-linaro-4.6.2/bin/arm-eabi-
kali@kali:~$ make efikamx_defconfig

# configure your kernel !
kali@kali:~$ make menuconfig
kali@kali:~$ make -j$(cat /proc/cpuinfo|grep processor | wc -l)
kali@kali:~$ make modules_install INSTALL_MOD_PATH=~/arm-stuff/images/root
kali@kali:~$ make uImage
kali@kali:~$ cp arch/arm/boot/uImage ~/arm-stuff/images/boot
kali@kali:~

```

```bash
kali@kali:~$ cat <<EOF > ~/arm-stuff/images/boot/boot.script
setenv ramdisk uInitrd;
setenv kernel uImage;
setenv bootargs console=tty1 root=/dev/mmcblk0p2 rootwait rootfstype=ext4 rw quiet;
${loadcmd} ${ramdiskaddr} ${ramdisk};
if imi ${ramdiskaddr}; then; else
setenv bootargs ${bootargs} noinitrd;
setenv ramdiskaddr "";
fi;
${loadcmd} ${kerneladdr} ${kernel}
if imi ${kerneladdr}; then
bootm ${kerneladdr} ${ramdiskaddr}
fi;
EOF
kali@kali:~

```

```bash
kali@kali:~$ mkimage -A arm -T script -C none -n "Boot.scr for EfikaMX" -d ~/arm-stuff/images/boot/boot.script ~/arm-stuff/images/boot/boot.scr

```

--------------------------------

### Upgrade All Packages in Kali Linux (Bash)

Source: https://www.kali.org/docs/general-use/updating-a-package

Upgrades all installed packages on Kali Linux to their latest available versions. This command should be run after updating the package list.

```bash
kali@kali:~$ sudo apt full-upgrade
```

--------------------------------

### Configure Nuke Password for Kali Linux Data Destruction

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

Installs and configures the 'cryptsetup-nuke-password' package to set a special password that destroys data on encrypted partitions when entered at boot. This is a safety measure for sensitive data.

```bash
sudo apt install -y cryptsetup-nuke-password

sudo dpkg-reconfigure cryptsetup-nuke-password
INFO: Storing the nuke password's crypted hash in /etc/cryptsetup-nuke-password/password_hash
Processing triggers for initramfs-tools (0.145) ...
update-initramfs: Generating /boot/initrd.img-6.11.2-amd64
```

--------------------------------

### Prevent updatedb Indexing of Snapshots

Source: https://www.kali.org/docs/installation/btrfs

This command modifies the updatedb configuration file to exclude snapshot directories from system indexing, preventing potential performance degradation.

```bash
sudo sed -i '/# PRUNENAMES=/ a PRUNENAMES = ".snapshots"' /etc/updatedb.conf
```

--------------------------------

### Check PostgreSQL Service Status (Shell)

Source: https://www.kali.org/docs/tools/starting-metasploit-framework-in-kali

This command checks the status of the PostgreSQL service. It verifies if the service is active and listening on the default port (5432). The output includes systemd status and network connection details.

```shell
kali@kali:~$ sudo msfdb status
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; disabled; vendor preset: disabled)
     Active: active (exited) since Sun 2021-02-07 02:15:42 EST; 4s ago
    Process: 157089 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 157089 (code=exited, status=0/SUCCESS)

Feb 07 02:15:42 kali systemd[1]: Starting PostgreSQL RDBMS...
Feb 07 02:15:42 kali systemd[1]: Finished PostgreSQL RDBMS.

COMMAND     PID     USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
postgres 157071 postgres    5u  IPv6 647182      0t0  TCP localhost:5432 (LISTEN)
postgres 157071 postgres    6u  IPv4 647183      0t0  TCP localhost:5432 (LISTEN)


UID          PID    PPID  C STIME TTY      STAT   TIME CMD
postgres  157071       1  1 02:15 ?        Ss     0:00 /usr/lib/postgresql/13/bin/postgres -D /var/lib/postgresql/13/main -c config_file=/etc/postgresql/13/main/postgresql.conf

[i] No configuration file found
kali@kali:~$ 

```

--------------------------------

### Define ARM Architecture and Packages

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Defines environment variables for the target ARM architecture (e.g., armhf) and lists the packages to be installed in the Kali ARM image. These variables are used throughout the build process.

```bash
kali@kali:~$ export packages="xfce4 kali-menu wpasupplicant kali-defaults initramfs-tools u-boot-tools nmap openssh-server"
kali@kali:~$ export architecture="armhf"

```

--------------------------------

### Backup and Prepare Disk for Encryption

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This sequence of commands performs essential pre-encryption tasks. It includes syncing data, unmounting partitions, creating backup directories, backing up the chroot environment using rsync, closing the LUKS volume, and re-partitioning the target disk (sdX) to prepare for a new encrypted partition.

```bash
sync
exit
sudo umount /mnt/chroot/{boot,sys,proc,dev/pts,dev}
sudo mkdir -vp /mnt/{backup,encrypted}
sudo rsync -avh /mnt/chroot/* /mnt/backup/
sudo cryptsetup luksClose crypt
sudo umount /mnt/chroot
echo -e "d\n2\nw" | sudo fdisk /dev/sdX
echo -e "n\np\n2\n\n\nw" | sudo fdisk /dev/sdX
```

--------------------------------

### Display Kali Linux Distribution Information

Source: https://www.kali.org/docs/cloud/digitalocean

Retrieves and displays detailed information about the Kali Linux distribution, including its distributor ID, description, release version, and codename. This command is useful for verifying the installed Kali version.

```bash
kali@kali-s-1vcpu-1gb-nyc3-01:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Kali
Description:	Kali GNU/Linux Rolling
Release:	2019.2
Codename:	n/a


```

--------------------------------

### Delete Snapshots using Snapper CLI

Source: https://www.kali.org/docs/installation/btrfs

This command provides a template for deleting snapshots using the snapper command-line tool, allowing deletion by snapshot number or a range of numbers.

```bash
`sudo snapper delete <number-or-number-range>`
```

--------------------------------

### Schedule Automatic Netboot Image Updates with Cron (Bash)

Source: https://www.kali.org/docs/installation/network-pxe

This command adds a cron job to the 'tftp' user's crontab. The job is scheduled to run every Tuesday at 05:00 and executes the '/opt/pxe/tftpboot.sh' script, which updates the Netboot images. Output is redirected to /dev/null to prevent unnecessary logging.

```bash
kali@kali:~$ sudo crontab -u tftp -e
[...] 
0 5 * * 2 /opt/pxe/tftpboot.sh >/dev/null
```

--------------------------------

### Modify Python Code to Disable Requirements Check

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the modification of a Python script (`finalrecon.py`) to disable the requirements checking functionality. The original code that reads `requirements.txt` and checks for installed packages is commented out.

```python
#with open(path_to_script + '/requirements.txt', 'r') as rqr:
#      pkg_list = rqr.read().strip().split('
')

#print('\n' + G + '[+]' + C + ' Checking Dependencies...' + W + '\n')

#for pkg in pkg_list:
#      spec = importlib.util.find_spec(pkg)
#      if spec is None:
#              print(R + '[-]' + W + ' {}'.format(pkg) + C + ' is not Installed!' + W)
#              fail = True
#      else:
#              pass
#if fail == True:
#      print('\n' + R + '[-]' + C + ' Please Execute ' + W + 'pip3 install -r requirements.txt' + C + ' to Install Missing Packages' + W + '\n')
#      os.remove(pid_path)
#      sys.exit()
```

--------------------------------

### Create zz-cryptsetup Initramfs Hook

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Creates the 'zz-cryptsetup' hook script within the initramfs-tools configuration directory. This script is responsible for copying necessary files like crypttab and fstab into the initramfs, enabling encrypted root support.

```bash
#!/bin/sh
set -e

PREREQ=""
prereqs()
{
	echo "${PREREQ}"
}

case "${1}" in
	prereqs)
		prereqs
		exit 0
		;;
esac

. /usr/share/initramfs-tools/hook-functions

mkdir -p ${DESTDIR}/cryptroot || true
cat /etc/crypttab >> ${DESTDIR}/cryptroot/crypttab
cat /etc/fstab >> ${DESTDIR}/cryptroot/fstab
cat /etc/crypttab >> ${DESTDIR}/etc/crypttab
cat /etc/fstab >> ${DESTDIR}/etc/fstab
copy_file config /etc/initramfs-tools/unlock.sh /etc/unlock.sh

```

--------------------------------

### Encrypt Partition with LUKS

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This command formats the specified partition (`/dev/sdX3`) with LUKS (Linux Unified Key Setup) encryption. It prompts the user to enter and verify a strong passphrase, which is essential for decrypting the partition later. Overwriting existing data is irreversible.

```bash
kali@kali:~$ sudo cryptsetup --verbose --verify-passphrase luksFormat /dev/sdX3
WARNING!\n========\nThis will overwrite data on /dev/sdX3 irrevocably.\n\nAre you sure? (Type 'yes' in capital letters): YES
Enter passphrase for /dev/sdX3:
Verify passphrase:
Existing 'ext4' superblock signature on device /dev/sdX3 will be wiped.
Key slot 0 created.
Command successful.
kali@kali:~$ 

```

--------------------------------

### Configure Hostname and Block Device

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Sets the hostname for the Kali Linux system and specifies the block device for the installation. The hostname must consist of ASCII letters, digits, and hyphens. The block device is typically an SD card or USB drive, identifiable using `lsblk`.

```bash
export _HOSTNAME="kali-encrypted-basic"
export _BLKDEV="/dev/sdX"
```

--------------------------------

### Reset Kali Linux Xfce Configuration

Source: https://www.kali.org/docs/general-use/xfce-faq

Resets Kali Linux Xfce configuration by removing cache, config, and local directories. This is useful for troubleshooting display issues after installing Xfce.

```bash
rm -r .cache .config .local
# Reboot after running this command
```

--------------------------------

### Edit Package Source Code (Shell Command)

Source: https://www.kali.org/docs/development/rebuilding-a-package-from-source

This command shows how to edit a specific source file within the downloaded package. In this example, it uses 'vim' to modify 'mifare-classic-format.c'.

```shell
kali@kali:~$ vim examples/mifare-classic-format.c
```

--------------------------------

### Display Kali Linux Kernel and System Information

Source: https://www.kali.org/docs/cloud/digitalocean

Retrieves and displays comprehensive information about the Linux kernel and system architecture for the Kali Linux installation. This includes kernel version, operating system, and hardware details.

```bash
kali@kali-s-1vcpu-1gb-nyc3-01:~$ uname -a
Linux kali-s-1vcpu-1gb-nyc3-01 4.19.0-kali5-amd64 #1 SMP Debian 4.19.37-2kali1 (2019-05-15) x86_64 GNU/Linux

```

--------------------------------

### Verify Guacamole, Tomcat, and MySQL Service Status

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This command checks the status of the Tomcat, Guacamole daemon (guacd), and MySQL services. It confirms that all essential components for Guacamole are running correctly after installation.

```bash
kali@kali:~$ systemctl status tomcat9 guacd mysql
● tomcat9.service - Apache Tomcat 9 Web Application Server
     Loaded: loaded (/lib/systemd/system/tomcat9.service; enabled; vendor preset: disabled)
     Active: active (running) since Thu 2020-03-05 17:39:38 GMT; 1min 14s ago
       Docs: https://tomcat.apache.org/tomcat-9.0-doc/index.html
   Main PID: 33192 (java)
      Tasks: 47 (limit: 19107)
     Memory: 454.8M
     CGroup: /system.slice/tomcat9.service
             └─33192 /usr/lib/jvm/default-java/bin/java -Djava.util.logging.config.file=/var/lib/tomcat9/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djava.a>

● guacd.service - LSB: Guacamole proxy daemon
     Loaded: loaded (/etc/init.d/guacd; generated)
     Active: active (running) since Thu 2020-03-05 14:04:34 GMT; 3h 36min ago
       Docs: man:systemd-sysv-generator(8)
      Tasks: 1 (limit: 19107)
     Memory: 11.5M
     CGroup: /system.slice/guacd.service
             └─991 /usr/local/sbin/guacd -p /var/run/guacd.pid

Warning: Journal has been rotated since unit was started. Log output is incomplete or unavailable.

● mysql.service - LSB: Start and stop the mysql database server daemon
     Loaded: loaded (/etc/init.d/mysql; generated)
     Active: active (running) since Thu 2020-03-05 17:39:46 GMT; 1min 6s ago
       Docs: man:systemd-sysv-generator(8)
      Tasks: 34 (limit: 19107)
     Memory: 88.9M
     CGroup: /system.slice/mysql.service
             ├─33670 /bin/sh /usr/bin/mysqld_safe
             ├─33787 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib/x86_64-linux-gnu/mariadb19/plugin --user=mysql --skip-log-error --pid-file=/run/mysqld/mysqld.pid --soc>
             └─33788 logger -t mysqld -p daemon error
kali@kali:/tmp/guac-install$ 

```

--------------------------------

### Update and Upgrade Kali Linux System

Source: https://www.kali.org/docs/troubleshooting/no-sound

These commands update the package list and perform a full system upgrade, which is necessary to automatically install PipeWire when upgrading to Kali 2023.2. A reboot is recommended after the upgrade.

```bash
kali@kali:~$ sudo apt update
kali@kali:~$ 
kali@kali:~$ sudo apt full-upgrade -y
kali@kali:~$ 

```

--------------------------------

### Downgrade Package to Kali Rolling Repository

Source: https://www.kali.org/docs/general-use/kali-bleeding-edge

Downgrades a specified package to the version available in the kali-rolling (stable) repository. This command requires root privileges and is used to revert a package previously installed from a testing or unstable repository. The output confirms the downgrade process.

```bash
kali@kali:~$ $ sudo apt install gitleaks/kali-rolling
Reading package lists... Done
Building dependency tree
Reading state information... Done
Selected version '7.4.0-0kali1' (kali-rolling [amd64]) for 'gitleaks'
The following packages will be DOWNGRADED:
  gitleaks
0 upgraded, 0 newly installed, 1 downgraded, 0 to remove and 282 not upgraded.
Need to get 2504 kB of archives.
After this operation, 0 B of additional disk space will be used.
Do you want to continue? [Y/n]
Get:1 http://kali.download/kali kali-rolling/main amd64 gitleaks amd64 7.4.0-0kali1 [2504 kB]
Fetched 2504 kB in 2s (1060 kB/s)
dpkg: warning: downgrading gitleaks from 7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1 to 7.4.0-0kali1
(Reading database ... 106747 files and directories currently installed.)
Preparing to unpack .../gitleaks_7.4.0-0kali1_amd64.deb ...
Unpacking gitleaks (7.4.0-0kali1) over (7.4.0+git20210412.1.6f5ad9d-0kali1~jan+nus1) ...
Setting up gitleaks (7.4.0-0kali1) ...
Processing triggers for kali-menu (2021.1.4) ...
```

--------------------------------

### Configure Flatpak Theme Support on Kali Linux

Source: https://www.kali.org/docs/tools/flatpak

Enables Flatpak applications to use local system themes for better visual consistency. This involves copying themes to the user's theme directory and overriding Flatpak's filesystem access. Requires root privileges for the override command.

```bash
mkdir -p ~/.themes
cp -a /usr/share/themes/* ~/.themes/
sudo flatpak override --filesystem=~/.themes/
```

--------------------------------

### Backup NetHunter Rootfs (Shell)

Source: https://www.kali.org/docs/nethunter/nethunter-rootless

Creates a compressed archive of the NetHunter root filesystem (kali-arm64 or kali-armhf) and moves it to the Android downloads folder for backup purposes. Ensure all NetHunter sessions are stopped before running.

```shell
# For arm64 devices
tar -cJf kali-arm64.tar.xz kali-arm64 && mv kali-arm64.tar.xz storage/downloads

# For older armhf devices (if applicable)
tar -cJf kali-armhf.tar.xz kali-armhf && mv kali-armhf.tar.xz storage/downloads

```

--------------------------------

### Enable Password-less Sudo on Kali

Source: https://www.kali.org/docs/general-use/sudo

This command installs a package and reconfigures it to allow a user to be added to a trusted group, enabling password-less sudo. This simplifies administrative tasks but poses a security risk if the user account is compromised.

```bash
kali@kali:~$ sudo apt install -y kali-grant-root && sudo dpkg-reconfigure kali-grant-root

```

--------------------------------

### Update APT Cache After Adding Repository

Source: https://www.kali.org/docs/virtualization/install-virtualbox-host

After adding a new repository, it's essential to update your APT package cache. This command refreshes the list of available packages from all configured sources, including the newly added VirtualBox repository.

```bash
kali@kali:~$ sudo apt update
[...]
kali@kali:~$ 

```

--------------------------------

### Download and Extract Kali Linux Kernel Source Code (4.9)

Source: https://www.kali.org/docs/development/recompiling-the-kali-linux-kernel

Downloads the Linux kernel source code for version 4.9 and extracts it into a user-specific directory for modification. It assumes the 'linux-source-4.9' package is installed.

```bash
kali@kali:~$ sudo apt install -y linux-source-4.9
kali@kali:~$ ls /usr/src
linux-config-4.9  linux-patch-4.9-rt.patch.xz  linux-source-4.9.tar.xz
kali@kali:~$ mkdir -p ~/kernel/
kali@kali:~$ cd ~/kernel/
kali@kali:~/kernel$ tar -xaf /usr/src/linux-source-4.9.tar.xz

```

--------------------------------

### Configure and Cross-Compile Chromium Kernel

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This section outlines the steps for configuring and cross-compiling the Chromium kernel for an ARM architecture. It involves setting environment variables for the architecture and cross-compiler, preparing the configuration, disabling specific kernel features (LSM), modifying a header file, and then running the compilation process using 'make'. It also includes steps for installing modules and copying firmware.

```bash
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/arm-eabi-linaro-4.6.2/bin/arm-eabi-
kali@kali:~$ 
kali@kali:~$ ./chromeos/scripts/prepareconfig chromeos-exynos5

# Disable LSM
kali@kali:~$ sed -i 's/CONFIG_SECURITY_CHROMIUMOS=y/# CONFIG_SECURITY_CHROMIUMOS is not set/g' .config

# If cross compiling, do this once:
kali@kali:~$ sed -i 's/if defined(__linux__)/if defined(__linux__) ||defined(__KERNEL__) /g' include/drm/drm.h

kali@kali:~$ make menuconfig
kali@kali:~$ make -j$(cat /proc/cpuinfo|grep processor | wc -l)
kali@kali:~$ make dtbs
kali@kali:~$ cp ./scripts/dtc/dtc /usr/bin/
kali@kali:~$ mkimage -f kernel.its kernel.itb
kali@kali:~$ make modules_install INSTALL_MOD_PATH=~/arm-stuff/images/root/

# Copy over firmware. Ideally use the original firmware (/lib/firmware) from the Chromebook.
kali@kali:~$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/dwmw2/linux-firmware.git
kali@kali:~$ cp -rf linux-firmware/* ~/arm-stuff/images/root/lib/firmware/
kali@kali:~$ rm -rf linux-firmware
```

--------------------------------

### Perform Second-Stage Chroot for Kali ARM

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Chroots into the base rootfs to perform the second-stage debootstrap installation and configure essential image settings like repositories, hostname, and network interfaces. This stage prepares the image for further customization.

```bash
kali@kali:~$ cd ~/arm-stuff/rootfs/
kali@kali:~$ LANG=C chroot kali-$architecture /debootstrap/debootstrap --second-stage
kali@kali:~$ 
cat <<EOF > kali-$architecture/etc/apt/sources.list
deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
EOF
kali@kali:~$ 
kali@kali:~$ echo "kali" > kali-$architecture/etc/hostname
kali@kali:~$ 
kali@kali:~$ cat <<EOF > kali-$architecture/etc/network/interfaces
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet dhcp
EOF
kali@kali:~$ 
kali@kali:~$ cat <<EOF > kali-$architecture/etc/resolv.conf
nameserver 8.8.8.8
EOF

```

--------------------------------

### Compile Raspberry Pi Kernel and Modules

Source: https://www.kali.org/docs/development/custom-raspberry-pi-image

Clones the Raspberry Pi kernel and tools repositories, sets up the ARM cross-compilation environment, configures the kernel using a default defconfig, and compiles it. It then installs the modules into the image's root filesystem.

```bash
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/
kali@kali:~$ cd ~/arm-stuff/kernel/
kali@kali:~$ git clone https://github.com/raspberrypi/tools.git
kali@kali:~$ git clone https://github.com/raspberrypi/linux.git raspberrypi
kali@kali:~$ cd raspberrypi/
kali@kali:~$ touch .scmversion
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/arm-eabi-linaro-4.6.2/bin/arm-eabi-
kali@kali:~$ make bcmrpi_cutdown_defconfig

kali@kali:~$ # configure your kernel !
kali@kali:~$ make menuconfig
kali@kali:~$ make -j$(cat /proc/cpuinfo|grep processor | wc -l)
kali@kali:~$ make modules_install INSTALL_MOD_PATH=~/arm-stuff/images/root
kali@kali:~$ cd ../tools/mkimage/
kali@kali:~$ python imagetool-uncompressed.py ../../raspberrypi/arch/arm/boot/Image

```

--------------------------------

### Closing Encrypted USB Partitions

Source: https://www.kali.org/docs/usb/usb-standalone-encrypted

This final step in the preparation process involves closing the LUKS-encrypted partitions on the USB drive using the `cryptsetup close` command. This action removes the mapped devices and effectively locks the encrypted partitions.

```bash
$ sudo cryptsetup close LUKS_BOOT
$ sudo cryptsetup close LUKS_SWAP
$ sudo cryptsetup close LUKS_ROOT
```

--------------------------------

### Build Raspberry Pi 4 Kali Linux Image (Shell)

Source: https://www.kali.org/docs/development/arm-build-scripts

This script demonstrates the workflow for building a Kali Linux image for the Raspberry Pi 4. It requires cloning the repository, installing dependencies, and executing the specific build script. The output image location and format depend on the system architecture.

```shell
cd ~/
git clone https://gitlab.com/kalilinux/build-scripts/kali-arm
cd ~/kali-arm/
sudo ./common.d/build_deps.sh
sudo ./raspberry-pi.sh

```

--------------------------------

### Create and Format a New USB Partition with fdisk

Source: https://www.kali.org/docs/usb/usb-persistence

This command uses `fdisk` to create a new primary partition on the USB drive. The input `printf "p\nn\np\n\n\np\nw"` automates the process of printing the partition table, creating a new partition, setting it as primary, accepting default sizes, and writing the changes.

```bash
kali@kali:~$ usb=/dev/sdX
kali@kali:~$ 
kali@kali:~$ sudo fdisk $usb <<< $(printf "p\nn\np\n\n\np\nw")
[...] 
kali@kali:~$ 

```

--------------------------------

### Disable Xfce Compositor for Terminal Issues

Source: https://www.kali.org/docs/general-use/xfce-faq

Disables the xfwm4 compositor in Xfce to resolve issues where the terminal window appears but remains empty. It also provides instructions for installing and auto-starting the 'compton' compositor as an alternative.

```bash
# Disable xfwm4 compositor
# Go to Settings -> Window Manager Tweaks -> Compositor tab -> Uncheck Enable display compositing

# Install and auto-start Compton compositor
sudo apt install -y compton
# Go to Settings -> Session and Startup -> Application Autostart -> Add
# Name: Compton
# Command: compton
```

--------------------------------

### Initiate WiFi Attack Tools (Bash)

Source: https://www.kali.org/docs/nethunter/testing-checklist

This command sequence brings up the external WiFi interface (wlan1) and initiates the wifite tool to scan for networks. It's a preliminary step for wireless security testing.

```bash
ifconfig wlan1 up && wifite
```

--------------------------------

### Partition and Format Image File

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This script partitions the created image file into two primary partitions using parted: a FAT32 boot partition and an ext4 root partition. It then sets up loop devices, maps partitions using kpartx, formats them with appropriate file systems (vfat and ext4), and mounts them for further operations.

```bash
kali@kali:~$ parted kali-custom-odroid.img --script -- mklabel msdos
kali@kali:~$ parted kali-custom-odroid.img --script -- mkpart primary fat32 4096s 266239s
kali@kali:~$ parted kali-custom-odroid.img --script -- mkpart primary ext4 266240s 100%
kali@kali:~$ 
loopdevice=`losetup -f --show kali-custom-odroid.img`
kpartx -va $loopdevice| sed -E 's/.*(loop[0-9])p.*/\1/g' | head -1`
device="/dev/mapper/${device}"
bootp=${device}p1
rootp=${device}p2
mkfs.vfat $bootp
mkfs.ext4 -L kaliroot $rootp
mkdir -p boot root
mount $bootp boot
mount $rootp root

```

--------------------------------

### Extract Kali VMware VM Image using 7z

Source: https://www.kali.org/docs/virtualization/import-premade-vmware

This command extracts the Kali Linux VMware image archive using the 7z utility. Ensure you have 7z installed on your system. The command takes the archive file as input and extracts its contents to the current directory.

```bash
kali@kali:~$ 7z x kali-linux-2025.4-vmware-amd64.7z
[...]
kali@kali:~$ 

```

--------------------------------

### Configure Watch File for GitHub Releases

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This snippet shows a debian/watch file configured to monitor GitHub releases for the 'instaloader' project. It includes options to mangle filenames and use 'uversionmangle' to correctly sort release candidates and pre-releases before final versions, ensuring accurate version detection.

```text
version=4
opts=uversionmangle=s/(\d)[_\.\-\+]?((RC|rc|pre|dev|beta|alpha|a)\d*)$// \
  https://github.com/instaloader/instaloader/tags .*/v?(\S+)\.tar\.gz

```

--------------------------------

### Create Third-Stage Chroot Script for Kali ARM

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Defines the 'third-stage' script executed within the chroot environment. This script updates package lists, installs essential packages like locales, git, and u-boot-tools, sets the default user password, and applies system configurations.

```shell
kali@kali:~$ cat <<EOF > kali-$architecture/third-stage
#!/bin/sh
dpkg-divert --add --local --divert /usr/sbin/invoke-rc.d.chroot --rename /usr/sbin/invoke-rc.d
cp /bin/true /usr/sbin/invoke-rc.d

apt-get update
apt-get install -y locales-all
#locale-gen en_US.UTF-8

debconf-set-selections /debconf.set
rm -f /debconf.set
apt-get update
apt-get install -y locales-all
apt-get install -y git-core binutils ca-certificates initramfs-tools u-boot-tools
apt-get install -y locales console-common less vim git
echo "kali:kali" | chpasswd
sed -i -e 's/KERNEL!=\"eth*|/KERNEL!=\"/' /lib/udev/rules.d/75-persistent-net-generator.rules
rm -f /etc/udev/rules.d/70-persistent-net.rules
apt-get install -y --force-yes ${packages}

rm -f /usr/sbin/invoke-rc.d
dpkg-divert --remove --rename /usr/sbin/invoke-rc.d

rm -f /third-stage
EOF
```

--------------------------------

### Configure APT Sources for Kali ARM chroot

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

This snippet demonstrates how to configure the APT sources list within a Kali Linux ARM chroot environment. It creates a new sources.list file with the specified repository.

```bash
kali@kali:~$ cat <<EOF > kali-$architecture/etc/apt/sources.list
deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
EOF
```

```text
deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
```

--------------------------------

### Write Kali Image to USB and Repair GPT

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This snippet demonstrates how to write a Kali Linux image file to a specified USB device and then repair its GPT (GUID Partition Table). Ensure '/dev/sdX' is replaced with the correct device label for your USB drive.

```bash
kali@kali:~$ dd if=kali-linux-chrome.img of=/dev/sdX conv=fsync bs=4M
kali@kali:~$ cgpt repair /dev/sdX
```

--------------------------------

### Set Default Shell and Unset Session Managers (Bash)

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This snippet sets the default shell to bash and unsets session manager variables. These commands are typically used in shell configuration files to ensure a clean environment for starting graphical sessions.

```bash
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
export SHELL=/bin/bash
```

--------------------------------

### Set Kali Linux to use local time (RTC)

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-windows

This command configures the Kali Linux system clock to use the Real-Time Clock (RTC) for local time, which helps synchronize time between Windows and Linux in a dual-boot setup. It adjusts the system clock accordingly. To revert, use '0' instead of '1'.

```bash
kali@kali:~$ timedatectl set-local-rtc 1 --adjust-system-clock
kali@kali:~$ 

```

--------------------------------

### Create U-Boot Boot Script for CuBox

Source: https://www.kali.org/docs/development/custom-cubox-image

This snippet demonstrates how to create a boot script for U-Boot on a CuBox. It uses a heredoc to define the script content, which includes logic for detecting the root device (USB, MMC, IDE) and setting boot arguments. The script is then converted into a U-Boot executable format using 'mkimage'.

```bash
kali@kali:~$ cat <<EOF > ~/arm-stuff/images/root/boot/boot.txt
echo "== Executing ${directory}${bootscript} on ${device_name} partition ${partition} =="
setenv unit_no 0
setenv root_device ?

if itest.s ${device_name} -eq usb; then
itest.s $root_device -eq ? && ext4ls usb 0:1 /dev && setenv root_device /dev/sda1 && setenv unit_no 0
itest.s $root_device -eq ? && ext4ls usb 1:1 /dev && setenv root_device /dev/sda1 && setenv unit_no 1
fi

if itest.s ${device_name} -eq mmc; then
itest.s $root_device -eq ? && ext4ls mmc 0:2 /dev && setenv root_device /dev/mmcblk0p2
itest.s $root_device -eq ? && ext4ls mmc 0:1 /dev && setenv root_device /dev/mmcblk0p1
fi

if itest.s ${device_name} -eq ide; then
itest.s $root_device -eq ? && ext4ls ide 0:1 /dev && setenv root_device /dev/sda1
fi

if itest.s $root_device -ne ?; then
setenv bootargs "console=ttyS0,115200n8 vmalloc=448M video=dovefb:lcd0:1920x1080-32@60-edid clcd.lcd0_enable=1 clcd.lcd1_enable=0 root=${root_device} rootfstype=ext4"
setenv loadimage "${fstype}load ${device_name} ${unit_no}:${partition} 0x00200000 ${directory}${image_name}"
$loadimage && bootm 0x00200000
echo "!! Unable to load ${directory}${image_name} from ${device_name} ${unit_no}:${partition} !!"
exit
fi

echo "!! Unable to locate root partition on ${device_name} !!"
EOF
kali@kali:~$ mkimage -A arm -T script -C none -n "Boot.scr for CuBox" -d ~/arm-stuff/images/root/boot/boot.txt ~/arm-stuff/images/root/boot/boot.scr
```

--------------------------------

### Get Display Information with xdpyinfo

Source: https://www.kali.org/docs/general-use/fixing-dpi

This command retrieves detailed information about the X display, including screen dimensions and resolution (DPI). It helps determine the current detected screen size and DPI, which is crucial for identifying font scaling problems. The output shows pixel dimensions and dots per inch.

```bash
kali@kali:~$ xdpyinfo | grep 'dimensions\|resolution'
  dimensions:	1680x1050 pixels (160x90 millimeters)
  resolution:	267x296 dots per inch
kali@kali:~$ 
```

--------------------------------

### Preventing Network Service Persistence on Reboot (Kali Linux)

Source: https://www.kali.org/docs/policy/kali-linux-network-service-policy

Demonstrates how Kali Linux's default policy prevents network services from persisting across reboots, as seen during the installation of apt-cacher-ng. The `update-rc.d` script automatically disables network services.

```bash
kali@kali:~$ sudo apt install -y apt-cacher-ng
[...]
Setting up apt-cacher-ng (0.7.11-1) ...
update-rc.d: We have no instructions for the apt-cacher-ng init script.
update-rc.d: It looks like a network service, we disable it.
[...]
kali@kali:~$ 

```

--------------------------------

### Disabling Python 2 Compatibility Login Message

Source: https://www.kali.org/docs/general-use/python3-transition

To hide the login message indicating Python 2 is still the default for '/usr/bin/python', users can either remove the 'python-is-python2' package or create a specific file to disable the warning. This allows for a cleaner login experience.

```bash
mkdir -p ~/.local/share/kali-motd
touch ~/.local/share/kali-motd/disable-old-python-warning
```

--------------------------------

### Generate SSH and GPG Keys for Secure Packaging

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Generates SSH and GPG keys for secure access to repositories and signing packages. SSH keys are recommended for quicker access, while GPG keys ensure the authenticity of your work.

```bash
kali@kali:~$ ssh-keygen -t rsa
[...] 
kali@kali:~$ 
gpg --gen-key
gpg (GnuPG) 1.4.12; Copyright (C) 2012 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: directory `/home/packaging/.gnupg' created
gpg: new configuration file `/home/packaging/.gnupg/gpg.conf' created
gpg: WARNING: options in `/home/packaging/.gnupg/gpg.conf' are not yet active during this run
gpg: keyring `/home/packaging/.gnupg/secring.gpg' created
gpg: keyring `/home/packaging/.gnupg/pubring.gpg' created
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
 Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)
Requested keysize is 2048 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
Key does not expire at all
Is this correct? (y/N) y

You need a user ID to identify your key; the software constructs the user ID
from the Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"

Real name: First Last
Email address: email@domain.com
Comment:
You selected this USER-ID:
     "First Last <email@domain.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
You need a Passphrase to protect your secret key.

We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.

Not enough random bytes available. Please do some other work to give
the OS a chance to collect more entropy! (Need 284 more bytes)

gpg: /home/packaging/.gnupg/trustdb.gpg: trustdb created
gpg: key A123BC4D marked as ultimately trusted
pub   2048R/1234AB5C 2000-00-00
      Key fingerprint = 12AB 34C4 67DE F890 12G3  H45I 6789 J90K L123 MN4O
uid                  First Last <email@domain.com>
sub   2048R/12345A6B 2000-00-00
kali@kali:~$
```

--------------------------------

### Configure Quilt for Patch Management

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Sets up the configuration for Quilt, a tool used for managing patches. This configuration specifies the patch directory and provides options for diff and refresh arguments, including color output and timestamp/index exclusion.

```bash
kali@kali:~$ cat <<EOF > ~/.quiltrc
export QUILT_PATCHES=debian/patches
QUILT_DIFF_ARGS="--no-timestamps --no-index -p ab --color=auto"
QUILT_DIFF_OPTS="-p"
QUILT_PUSH_ARGS="--color=auto"
QUILT_REFRESH_ARGS="--no-timestamps --no-index -p ab"
EOF
kali@kali:~$
```

--------------------------------

### Adjust Time Zone for Guacamole Installation

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This snippet shows how to remove the current time zone link and create a new symbolic link to set the system's time zone to 'US/Central'. This is a workaround for a known bug in Apache Guacamole that affects the Eastern Daylight Time (EDT) zone.

```bash
kali@kali:~$ sudo rm /etc/localtime
kali@kali:~$ 
kali@kali:~$ sudo ln -s /usr/share/zoneinfo/US/Central /etc/localtime

```

--------------------------------

### Configure devscripts for Package Building

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Customizes the devscripts configuration, including build directories, uploader settings, changelog management, signing key ID, lintian options, and uscan destination. Ensure DEBSIGN_KEYID matches your GPG key ID.

```bash
kali@kali:~$ cat <<EOF > ~/.devscripts
DEBRELEASE_DEBS_DIR=$HOME/kali/build-area/
DEBRELEASE_UPLOADER=dput

DEBCHANGE_AUTO_NMU=no
DEBCHANGE_MULTIMAINT_MERGE=yes
DEBCHANGE_PRESERVE=yes
DEBCHANGE_RELEASE_HEURISTIC=changelog

DEBSIGN_KEYID=ABC123DE4567890123G4567HIJK890LM12345N6

DEBUILD_LINTIAN_OPTS="--color always -I"

USCAN_DESTDIR=$HOME/kali/upstream/
EOF
kali@kali:~$ 
kali@kali:~$ mkdir -pv $HOME/kali/{build-area,upstream}
```

--------------------------------

### Fixing Python Script Shebang Lines

Source: https://www.kali.org/docs/general-use/python3-transition

When encountering Python scripts with outdated shebang lines (e.g., '/usr/bin/python'), users need to update them to explicitly point to either Python 2 ('/usr/bin/python2') or Python 3 ('/usr/bin/python3'). This ensures the script is executed with the correct interpreter.

```text
#!/usr/bin/python3
#!/usr/bin/python2
#!/usr/bin/env python3
#!/usr/bin/env python2
```

--------------------------------

### Configure File System Mounts in Kaboxer Components

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This YAML configuration defines a mount for a Kaboxer component, making a host directory (`/var/lib/hello-kbx`) available inside the container at a specified target path (`/data`). This is useful for data persistence and sharing.

```yaml
components:
  default:
    [...]
    mounts:
      - source: /var/lib/hello-kbx
        target: /data

```

--------------------------------

### Configure NVIDIA Driver for DPI Settings

Source: https://www.kali.org/docs/general-use/fixing-dpi

This sequence installs `nvidia-xconfig`, generates a basic Xorg configuration file, moves it to the appropriate directory, and then modifies the configuration to disable EDID-based DPI detection and set a custom DPI value. This method is specific to systems using NVIDIA graphics drivers.

```shell
kali@kali:~$ sudo apt install -y nvidia-xconfig
kali@kali:~$ 
kali@kali:~$ sudo nvidia-xconfig
kali@kali:~$ 
kali@kali:~$ sudo mv /etc/X11/xorg.conf /usr/share/X11/xorg.conf.d/20-nvidia.conf
kali@kali:~$
```

--------------------------------

### Decode EDID Monitor Data with edid-decode

Source: https://www.kali.org/docs/general-use/fixing-dpi

This command decodes the Extended Display Identification Data (EDID) from the monitor, providing detailed information about its capabilities and characteristics. It's used here to check if the monitor's reported physical size and timings are accurate, which can be a source of incorrect DPI calculations. Requires installation of `edid-decode`.

```bash
kali@kali:~$ sudo apt install -y edid-decode
kali@kali:~$ 
kali@kali:~$ xrandr --props | edid-decode -c -s
EDID version: 1.3
[...]
Maximum image size: 16 cm x 9 cm
[...]
Warnings:

Block 0 (Base Block):
  Basic Display Parameters & Features: Dubious maximum image size (160x90 is smaller than 10x10 cm)

Failures:

All Blocks:
  One or more of the timings is out of range of the Monitor Ranges:
    Vertical Freq: 24 - 75 Hz (Monitor: 23 - 75 Hz)
    Horizontal Freq: 27.000 - 79.976 kHz (Monitor: 26.000 - 68.000 kHz)
    Maximum Clock: 148.500 MHz (Monitor: 150.000 MHz)

EDID conformity: FAIL
kali@kali:~$ 
```

--------------------------------

### Build Docker Image Directly (CLI)

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Command to build a Docker image directly using the 'docker build' command. This is useful for debugging when the 'kaboxer build' command fails, as it provides more detailed error messages. Requires membership in the 'docker' group or root rights.

```bash
docker build -f hello-cli.Dockerfile -t kaboxer/hello-cli .

```

--------------------------------

### Set Custom Mirror for Build (Shell)

Source: https://www.kali.org/docs/development/arm-build-scripts

This command demonstrates how to configure a custom local mirror for the build process by writing to the `builder.txt` file. This is useful for faster builds when a local mirror is available.

```shell
echo 'mirror="http://192.168.1.100/kali"' > ./builder.txt

```

--------------------------------

### Create New User for Docker RDP

Source: https://www.kali.org/docs/general-use/xfce-with-rdp

When using RDP with Kali in a Docker container, it is recommended to create a new user instead of using the root user. The 'adduser kali' command initiates an interactive process to create a new user named 'kali' with a home directory and prompts for password and user information.

```shell
kali@kali:~$ adduser kali
[...] 
kali@kali:~$ 

```

--------------------------------

### Debian Copyright File Configuration

Source: https://www.kali.org/docs/development/intermediate-packaging-example

Defines the copyright and licensing information for the 'photon' package. It specifies the upstream contact, source, and license details for different file sets within the package.

```debian
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: photon
Upstream-Contact: s0md3v <s0md3v@gmail.com>
Source: https://gihub.com/s0md3v/Photon

Files: *
Copyright: 2020 s0md3v <s0md3v@gmail.com>
License: GPL-3+

Files: debian/*
Copyright: 2020 Joseph O'Gorman <gamb1t@kali.org>
License: GPL-3+

License: GPL-3+
 This package is free software; you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation; either version 3 of the License, or
 (at your option) any later version.
 .
 This package is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.
 .
 You should have received a copy of the GNU General Public License
 along with this program. If not, see <https://www.gnu.org/licenses/>
 .
 On Debian systems, the complete text of the GNU General
 Public License version 3 can be found in "/usr/share/common-licenses/GPL-3".
```

--------------------------------

### Verify Initramfs Contents

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

These commands are used to inspect the contents of the generated initramfs archive. By grepping for specific files like 'cryptsetup', 'authorized_keys', or 'unlock.sh', you can verify that the necessary components for decryption and system access are included.

```bash
lsinitramfs /boot/initramfs.gz | grep cryptsetup
lsinitramfs /boot/initramfs.gz | grep authorized
lsinitramfs /boot/initramfs.gz | grep unlock.sh
```

--------------------------------

### Set Boot Partition Priority with cgpt

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This section explains how to assign boot priorities to partitions on the USB drive using the `cgpt add` command. Higher priority numbers boot first. This is crucial for ensuring the correct kernel boots from the device.

```bash
kali@kali:~$ cgpt add -i 1 -S 1 -T 5 -P 10 -l KERN-A /dev/sdX
kali@kali:~$ cgpt add -i 2 -S 1 -T 5 -P 5 -l KERN-B /dev/sdX
```

--------------------------------

### Copy Kali Rootfs and Set DNS

Source: https://www.kali.org/docs/development/custom-cubox-image

Copies the pre-built Kali ARM root filesystem from '~/arm-stuff/rootfs/kali-armhf/' to the mounted 'root' directory using rsync for efficient file transfer. It also configures the DNS resolver by creating or overwriting 'root/etc/resolv.conf' with Google's public DNS server.

```bash
kali@kali:~$ rsync -HPavz /root/arm-stuff/rootfs/kali-armhf/ root
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf

```

--------------------------------

### Verify startkderc Configuration for VMware Fix

Source: https://www.kali.org/docs/virtualization/troubleshooting-vmware

This command displays the content of the `~/.config/startkderc` file to verify that the `systemdBoot` setting has been correctly set to `false`, confirming the fix for copy/paste and drag/drop issues in Kali KDE on VMware.

```bash
cat ~/.config/startkderc

```

--------------------------------

### Prepare Boot Partition for SD and USB

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This snippet prepares the boot partitions for SD and USB devices by writing the newly packed kernel images ('newkern-sd' and 'newkern-usb') to the respective boot partitions using the 'dd' command. It also includes commands to unmount the root partition and clean up loop devices.

```bash
kali@kali:~$ dd if=/tmp/newkern-sd of=$bootp1 conv=fsync # first boot partition for SD
kali@kali:~$ dd if=/tmp/newkern-usb of=$bootp2 conv=fsync # second boot partition for USB
kali@kali:~$ 
kali@kali:~$ umount $rootp
kali@kali:~$ 
kali@kali:~$ kpartx -dv $loopdevice
kali@kali:~$ losetup -d $loopdevice
```

--------------------------------

### Create QEMU Virtual Hard Disk

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Creates a qcow2 formatted virtual hard disk image named 'kali-test.hdd.img' with a size of 20GB in the /tmp directory. This disk will be used by the QEMU virtual machine.

```bash
kali@kali:$ qemu-img create \
  -f qcow2 \
  /tmp/kali-test.hdd.img \
  20G

```

--------------------------------

### Partition and Format Image File for CuBox

Source: https://www.kali.org/docs/development/custom-cubox-image

Partitions the 'kali-custom-cubox.img' file using msdos label and creates a primary ext4 partition. It then sets up a loop device for the image, maps the partition using kpartx, and formats the first partition as ext4. Finally, it mounts the formatted partition to a 'root' directory.

```bash
kali@kali:~$ parted kali-custom-cubox.img --script -- mklabel msdos
kali@kali:~$ parted kali-custom-cubox.img --script -- mkpart primary ext4 0 -1

```

```bash
kali@kali:~$ loopdevice=$(losetup -f --show kali-custom-cubox.img)
kali@kali:~$ device=`kpartx -va $loopdevice| sed -E 's/.*(loop[0-9])p.*/1/g' | head -1`
kali@kali:~$ device="/dev/mapper/${device}"
kali@kali:~$ rootp=${device}p1
kali@kali:~
kali@kali:~$ mkfs.ext4 $rootp
kali@kali:~$ mkdir -p root
kali@kali:~$ mount $rootp root

```

--------------------------------

### Configure Xorg for Mali Graphics

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Creates a basic xorg.conf file within the rootfs to configure the X server for Mali graphics drivers. This configuration specifies the 'mali' driver, sets up frame buffer device options, and defines screen and DRI settings for optimal performance.

```bash
kali@kali:~$ cat <<EOF > root/etc/X11/xorg.conf
# X.Org X server configuration file for xfree86-video-mali

Section "Device"
Identifier "Mali-Fbdev"
# Driver "mali"
Option "fbdev" "/dev/fb1"
Option "DRI2" "true"
Option "DRI2_PAGE_FLIP" "true"
Option "DRI2_WAIT_VSYNC" "true"
Option "UMP_CACHED" "true"
Option "UMP_LOCK" "false"
EndSection

Section "Screen"
Identifier "Mali-Screen"
Device "Mali-Fbdev"
DefaultDepth 24
EndSection

Section "DRI"
Mode 0666
EndSection
EOF

```

--------------------------------

### List APFS Disks and Partitions using diskutil

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

This command displays detailed information about all disks and their partitions, including APFS containers and volumes. It is crucial for identifying the correct disk identifier (e.g., disk0s2) before performing any resize operations. No external dependencies are required as 'diskutil' is a built-in macOS utility.

```bash
$ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                 Apple_APFS Container disk1         499.9 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +499.9 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD            16.6 GB    disk1s1
   2:                APFS Volume Preboot                 21.4 MB    disk1s2
   3:                APFS Volume Recovery                516.2 MB   disk1s3
   4:                APFS Volume VM                      20.5 KB    disk1s4

$
```

--------------------------------

### Build Kaboxer Docker Image (CLI)

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Command to build a Docker image for a Kaboxer application. This command requires privileges to use Docker and may fail if the user is not part of the 'docker' or 'kaboxer' group.

```bash
kaboxer build hello-cli

```

--------------------------------

### Verify APFS Container Resize with diskutil list

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

After executing the resize command, this command is used again to verify that the APFS container has been successfully resized to the target size. It confirms the updated size in the output, ensuring the operation was successful and the space is now available.

```bash
$ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                 Apple_APFS Container disk1         400.0 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +400.0 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD            16.6 GB    disk1s1
   2:                APFS Volume Preboot                 21.4 MB    disk1s2
   3:                APFS Volume Recovery                516.2 MB   disk1s3
   4:                APFS Volume VM                      20.5 KB    disk1s4
$
```

--------------------------------

### Create Mirror User Account

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Creates a new user account specifically for managing the Kali Linux mirror. This user is created with a disabled password and a bash shell.

```bash
sudo adduser --disabled-password --shell /bin/bash archvsync
Adding user 'archvsync' ...
[...]
Is the information correct? [Y/n] 
```

--------------------------------

### Manually Invoking x86 Binaries with QEMU

Source: https://www.kali.org/docs/arm/x86-on-arm

This command provides a way to manually execute an x86 binary if it's not automatically recognized and run by qemu-user-static. It directly invokes the qemu-x86_64-static emulator with the target binary as an argument.

```bash
kali@kali:~$ qemu-x86_64-static my_x86_code
kali@kali:~$
```

--------------------------------

### Verify New Partition with lsblk

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

The `lsblk` command lists block devices and their partitions. This is used to verify that the new partition (e.g., `/dev/sdX3`) has been successfully created after running `fdisk`.

```bash
kali@kali:~$ lsblk /dev/sdX
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sdc      8:32   1 58.4G  0 disk
├─sdc1   8:33   1  4.6G  0 part
├─sdc2   8:34   1    4M  0 part
└─sdc3   8:35   1 53.8G  0 part
kali@kali:~$ 

```

--------------------------------

### Run Win-KeX in Seamless Mode

Source: https://www.kali.org/docs/wsl/win-kex

Activates Win-KeX in seamless mode, allowing applications and menus to be shared between Windows and Kali. Sound support is included, and the command can be executed from Kali WSL or Windows command prompt.

```bash
kex --sl -s
```

```bash
wsl -d kali-linux kex --sl -s
```

--------------------------------

### Switch Kali to Graphical Desktop Environment

Source: https://www.kali.org/docs/arm/raspberry-pi-zero-2-w

This command sequence allows you to switch the Kali Linux Raspberry Pi Zero 2 W from its default command-line interface (CLI) to a graphical desktop environment. It uses `systemctl` to set the default target to graphical and then reboots the system. This is useful for users who want a visual interface but should be used cautiously due to the Pi Zero 2 W's limited RAM.

```bash
kali@kali:~$ sudo systemctl set-default graphical
kali@kali:~$ sudo reboot
```

--------------------------------

### Search for 'requests' package using apt-cache

Source: https://www.kali.org/docs/development/intro-to-packaging-example

These commands demonstrate how to search for the 'requests' Python library within the Kali Linux package repository using 'apt-cache'. It shows initial broad searches and then refined searches using '--names-only' to narrow down results.

```bash
apt-cache search requests | wc -l
apt-cache search --names-only requests | wc -l
apt-cache search --names-only python-requests
apt-cache search --names-only python-requests | grep -vi 'doc'
apt-cache search --names-only python3-requests
```

--------------------------------

### Verify New Partition with lsblk

Source: https://www.kali.org/docs/usb/usb-persistence

After creating a new partition with `fdisk`, this command is used again to verify that the new partition (e.g., `/dev/sdX3`) has been successfully created and added to the USB drive's partition table.

```bash
kali@kali:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
[...] 
sdb      8:48   1  58.4G  0 disk
├─sdb1   8:49   1   4.6G  0 part
├─sdb2   8:50   1     4M  0 part
└─sdb3   8:51   1  53.8G  0 part
kali@kali:~$ 

```

--------------------------------

### Build 32-bit ARM Kernel Toolchain and Compile

Source: https://www.kali.org/docs/nethunter/porting-nethunter

This snippet demonstrates how to clone the GCC toolchain for 32-bit ARM devices, set environment variables for the architecture and cross-compiler, and initiate the kernel build process. It's essential for older, non-64-bit Android devices.

```bash
kali@kali:~$ git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.7 toolchain
kali@kali:~$ export ARCH=arm
kali@kali:~$ export SUBARCH=arm
kali@kali:~$ export CROSS_COMPILE=`pwd`/toolchain/bin/arm-eabi-
kali@kali:~$ make your_device_codename
kali@kali:~$ make -j$(nproc)
```

--------------------------------

### Modify Network Interfaces File (Text Configuration)

Source: https://www.kali.org/docs/arm/raspberry-pi-zero-w-pi-tail

This shows the configuration change needed in the `/etc/network/interfaces` file. It replaces a static IP configuration with a DHCP client and adds a `post-up` command to execute a script that will set a predictable IP address.

```text
iface sepultura inet dhcp
  post-up /boot/change_ip.sh

```

--------------------------------

### Image Creation using dd Utility for ODROID-C0/C1/C1+

Source: https://www.kali.org/docs/arm/odroid-c

This command uses the 'dd' utility to write a Kali Linux image to a storage device. It's crucial to replace '/dev/sdX' with the correct device path to avoid data loss. The 'xzcat' command decompresses the image on the fly, and 'bs=4M' sets the block size for faster transfer. 'status=progress' shows the transfer progress.

```bash
xzcat kali-linux-2025.4-odroid-c-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Mount Partition and Create persistence.conf

Source: https://www.kali.org/docs/usb/usb-persistence

This sequence of commands creates a mount point, mounts the persistence partition, creates the `persistence.conf` file with the content `/ union`, and then unmounts the partition. This configuration enables the persistence feature for the Kali Live USB.

```bash
kali@kali:~$ usb=/dev/sdX
kali@kali:~$ 
kali@kali:~$ sudo mkdir -pv /mnt/my_usb
mkdir: created directory '/mnt/my_usb'
kali@kali:~$ 
kali@kali:~$ sudo mount -v ${usb}3 /mnt/my_usb
mount: /dev/sdX3 mounted on /mnt/my_usb.
kali@kali:~$ 
kali@kali:~$ echo "/ union" | sudo tee /mnt/my_usb/persistence.conf
/ union
kali@kali:~$ sudo umount -v ${usb}3
umount: /mnt/my_usb (/dev/sdX3) unmounted
kali@kali:~$ 

```

--------------------------------

### Create Directories for Finalrecon Package

Source: https://www.kali.org/docs/development/advanced-packaging-example

This command creates the directory structure required for the finalrecon package. It uses `mkdir -p` to ensure parent directories are created if they don't exist and creates both the package directory and an upstream directory. This is a standard shell command.

```shell
kali@kali:~$ mkdir -p ~/kali/packages/finalrecon/ ~/kali/upstream/
kali@kali:~$ 

```

--------------------------------

### Updated Debian Copyright File with MIT License

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This snippet demonstrates an updated debian/copyright file using the MIT license for both upstream and packaging work. It includes specific author details and the MIT license text.

```text
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Source: https://github.com/instaloader/instaloader
Upstream-Name: instaloader

Files: *
Copyright:
 2016-2020 Alexander Graf <mail@agraf.me>
 2016-2020 André Koch-Kramer <koch-kramer@web.de>
License: MIT

Files: debian/*
Copyright: 2020 Joseph O'Gorman <gamb1t@kali.org>
License: MIT

License: MIT
 The MIT License
 Permission is hereby granted, free of charge, to any person obtaining a copy
 of this software and associated documentation files (the "Software"), to deal
 in the Software without restriction, including without limitation the rights to
 use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
 of the Software, and to permit persons to whom the Software is furnished to do
 so, subject to the following conditions:
 .
 The above copyright notice and this permission notice shall be included in all
 copies or substantial portions of the Software.
 .
 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 SOFTWARE.
```

--------------------------------

### Image Kali Linux on CubieBoard2 using dd

Source: https://www.kali.org/docs/arm/cubieboard2

This command uses the dd utility to write a compressed Kali Linux image to a microSD card for the CubieBoard2. Ensure you replace '/dev/sdX' with the correct device path for your microSD card, as an incorrect path can lead to data loss. The 'xzcat' command decompresses the image on the fly, and 'status=progress' provides real-time feedback.

```bash
xzcat kali-linux-2025.4-cubieboard2-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Build Android 10 Image with Kalifs for OnePlus 7

Source: https://www.kali.org/docs/nethunter/building-nethunter

This command builds a full Android 10 image with the Kalifs rootfs for a OnePlus 7 device. It specifies the kernel, Android version, and rootfs type. The output is a flashable zip file.

```bash
kali@kali:~/kali-nethunter-installer$ python3 build.py -k oneplus7-oos --ten -fs full
[i] Reading: kernels/devices.yml
[i] Kernel ID: oneplus7-oos
[i] Android version: ten
[i] NetHunter release version: 20241022_132726
[i] rootfs: full
[i] From: kernels/devices.yml
[i]   kernelstring: NetHunter kernel
[i]   devicenames :  ['OnePlus7', 'oneplus7', 'guacamoleb', 'Guacamoleb', 'OnePlus7Pro', 'GM1915', 'GM1910', 'guacamole', 'Guacamole', 'OnePlus7T', 'OnePlus7TPro']
[i]   arch        : arm64
[i]   flasher     : anykernel
[i]   ramdisk     : auto
[i]   resolution  : 1080x2340
[i]   block       : /dev/block/bootdevice/by-name/boot
[i]   version     : 1.0
[i]   supersu     : auto
[i]   modules     : 1
[i]   slot_device : 1
[i]   author      : Re4son & yesimxev
[i] Downloading all NetHunter apps
[...]
[+] Finished creating zip
[i] Adding Kali rootfs archive to the installer zip
[+]   Added: kali-nethunter-rootfs-full-arm64.tar.xz
[+] Finished adding rootfs
[+] Created Kali NetHunter installer: nethunter-20241022_132726-oneplus7-oos-ten-kalifs-full.zip
kali@kali:~/kali-nethunter-installer$
kali@kali:~/kali-nethunter-installer$ ls -lh nethunter-20241022_132726-oneplus7-oos-ten-kalifs-full.zip
-rw-r--r-- 1 root root 2.3G Oct 22 13:28 nethunter-20241022_132726-oneplus7-oos-ten-kalifs-full.zip
```

--------------------------------

### Verify ISO Signature with .sha256sum File (Linux/macOS)

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Verifies the integrity of a downloaded Kali Linux ISO image using its corresponding .sha256sum signature file. Requires the 'shasum' command.

```bash
$ grep kali-linux-2025.4-live-amd64.iso kali-linux-2025.4-live-amd64.txt.sha256sum | shasum -a 256 -c

```

--------------------------------

### Query Detailed GPU Information with nvidia-smi (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command provides verbose, detailed information about the specified GPU (index 0 in this case). It includes driver and CUDA versions, GPU name, temperature, clock speeds, and running processes using the GPU. This is crucial for diagnosing GPU performance and issues.

```bash
kali@kali:~$ nvidia-smi -i 0 -q

==============NVSMI LOG==============

Timestamp                           : Fri Feb 14 13:26:21 2020
Driver Version                      : 430.64
CUDA Version                        : 10.1

Attached GPUs                       : 1
GPU 00000000:07:00.0
    Product Name                    : GeForce GTX 1060 6GB
    Product Brand                   : GeForce
    Display Mode                    : Enabled
    Display Active                  : Enabled
    Persistence Mode                : Disabled
    Accounting Mode                 : Disabled
    Accounting Mode Buffer Size     : 4000
[...]
    Temperature
        GPU Current Temp            : 49 C
        GPU Shutdown Temp           : 102 C
        GPU Slowdown Temp           : 99 C
[...]
    Clocks
        Graphics                    : 139 MHz
        SM                          : 139 MHz
        Memory                      : 405 MHz
        Video                       : 544 MHz
[...]
    Processes
        Process ID                  : 815
            Type                    : G
            Name                    : /usr/lib/xorg/Xorg
            Used GPU Memory         : 132 MiB
        Process ID                  : 994
            Type                    : G
            Name                    : xfwm4
            Used GPU Memory         : 2 MiB
kali@kali:~$
```

--------------------------------

### Flash Stock ROM and TWRP Recovery using Fastboot

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This section details the process of flashing a stock ROM and TWRP recovery image onto the device using fastboot commands. It involves unlocking the bootloader, flashing various partition images, and then flashing the custom recovery. Ensure you have the correct userdata image for your device's storage capacity.

```bash
kali@kali:~$ mkdir -pv cm/ && cd cm/ && unzip ../cm-11.0-XNPH44S-bacon-signed-fastboot.zip
kali@kali:~/cm$ fastboot oem unlock
kali@kali:~/cm$ fastboot flash modem NON-HLOS.bin
kali@kali:~/cm$ fastboot flash sbl1 sbl1.mbn
kali@kali:~/cm$ fastboot flash dbi sdi.mbn
kali@kali:~/cm$ fastboot flash aboot emmc_appsboot.mbn
kali@kali:~/cm$ fastboot flash rpm rpm.mbn
kali@kali:~/cm$ fastboot flash tz tz.mbn
kali@kali:~/cm$ fastboot flash LOGO logo.bin
kali@kali:~/cm$ fastboot flash oppostanvbk static_nvbk.bin
kali@kali:~/cm$ #fastboot flash recovery recovery.img
kali@kali:~/cm$ fastboot flash system system.img
kali@kali:~/cm$ fastboot flash boot boot.img
kali@kali:~/cm$ fastboot flash cache cache.img
kali@kali:~/cm$ #fastboot flash userdata userdata.img      # OnePlus One 16GB
kali@kali:~/cm$ fastboot flash userdata userdata_64G.img   # OnePlus One 64GB
kali@kali:~/cm$ cd ../ && rm -rf cm/
kali@kali:~$ 
kali@kali:~$ fastboot flash recovery twrp-3.6.2_9-0-bacon.img
kali@kali:~$ 
kali@kali:~$ fastboot boot twrp-3.6.2_9-0-bacon.img
```

--------------------------------

### Partition and Format Image File

Source: https://www.kali.org/docs/development/custom-raspberry-pi-image

Partitions the created image file into two primary partitions (FAT32 for boot, ext4 for root) using parted, then formats them. It also sets up loop devices and mounts the partitions for further manipulation.

```bash
kali@kali:~$ parted kali-custom-rpi.img --script -- mklabel msdos
kali@kali:~$ parted kali-custom-rpi.img --script -- mkpart primary fat32 0 64
kali@kali:~$ parted kali-custom-rpi.img --script -- mkpart primary ext4 64 -1

kali@kali:~$ loopdevice=`losetup -f --show kali-custom-rpi.img`
kali@kali:~$ device=`kpartx -va $loopdevice | sed -E 's/.*(loop[0-9])p.*/\1/g' | head -1`
kali@kali:~$ device="/dev/mapper/${device}"
kali@kali:~$ bootp=${device}p1
kali@kali:~$ rootp=${device}p2
kali@kali:~
kali@kali:~$ mkfs.vfat $bootp
kali@kali:~$ mkfs.ext4 $rootp
kali@kali:~$ mkdir -p root
kali@kali:~$ mkdir -p boot
kali@kali:~$ mount $rootp root
kali@kali:~$ mount $bootp boot

```

--------------------------------

### Configure Boot Arguments with libubootenv-tool

Source: https://www.kali.org/docs/arm/nanopc-t

This snippet demonstrates how to set custom boot arguments for the NanoPC-T3. It involves creating a configuration file with desired arguments and then using `fw_setenv` to write these to the microSD card. This allows for modifications to the kernel command line.

```shell
echo "console=ttySAC0,115200n8 root=/dev/mmcblk0p2 rootfstype=ext3 rootwait rw consoleblank=0 net.ifnames=0\nbootdelay 1" > env.conf
fw_setenv /dev/mmcblk0 -s env.conf
```

--------------------------------

### Configure rsync Daemon for Mirroring

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Enables and configures the rsync daemon to serve Kali Linux mirror directories. This involves modifying the rsync service configuration and defining export paths.

```bash
sudo sed -i -e "s/RSYNC_ENABLE=false/RSYNC_ENABLE=true/" /etc/default/rsync
sudo vim /etc/rsyncd.conf
$ cat /etc/rsyncd.conf
uid = nobody
gid = nogroup
max connections = 25
socket options = SO_KEEPALIVE

[kali]
path = /srv/mirrors/kali
comment = The Kali Archive
read only = true

[kali-images]
path = /srv/mirrors/kali-images
comment = The Kali ISO images
read only = true
$ sudo service rsync start
Starting rsync daemon: rsync.
```

--------------------------------

### Configure Sbuild to Use Approx Caching Proxy

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Configures sbuild to utilize the 'approx' caching proxy by specifying the proxy's address in the mmdebstrap arguments. This ensures that build dependencies are fetched through the local cache.

```perl
# use a caching proxy
push @{$unshare_mmdebstrap_extra_args}, "*", [
  '--aptopt=Acquire::HTTP::Proxy "http://localhost:9999";',
];

```

--------------------------------

### Build Kali ISO (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Executes the build script to generate the Kali Linux ISO image. The --verbose flag provides detailed output during the build process.

```bash
$ ./build.sh --verbose
```

--------------------------------

### Cloud Enum Test Control File

Source: https://www.kali.org/docs/development/contributing-runtime-tests

A simple debian/tests/control file for the 'cloud_enum' test, using 'Test-Command' and specifying a 'superficial' restriction.

```text
Test-Command: cloud_enum --help
Depends: @
Restrictions: superficial

```

--------------------------------

### Demonstrate Sudo Usage on Kali

Source: https://www.kali.org/docs/general-use/sudo

This sequence of commands demonstrates the effect of using 'sudo' to access restricted directories like '/root'. It shows the initial permission denied error for a non-root user and how 'sudo' with authentication grants access. It also includes the commands to enable password-less sudo and verifies access afterward.

```bash
kali@kali:~$ ls /root
ls: cannot open directory '/root': Permission denied
kali@kali:~$ 
kali@kali:~$ sudo ls /root
[sudo] password for kali:
hello
kali@kali:~$ sudo apt install -y kali-grant-root
[...]
kali@kali:~$ sudo dpkg-reconfigure kali-grant-root
[...]
kali@kali:~$ sudo ls /root
hello
kali@kali:~$ 

```

--------------------------------

### Check Direct Rendering Status with glxinfo (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command uses `glxinfo` to check if direct rendering is enabled on the system. Direct rendering is essential for efficient 3D graphics performance. 'Yes' indicates that it is enabled.

```bash
kali@kali:~$ glxinfo | grep -i "direct rendering"
direct rendering: Yes
kali@kali:~$
```

--------------------------------

### Enable Cryptsetup in Initramfs Configuration (Bash)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This command enables the `cryptsetup` hook for the initramfs by appending `CRYPTSETUP=y` to the `/etc/cryptsetup-initramfs/conf-hook` file. This ensures that cryptsetup functionalities are included in the initramfs image, which is necessary for unlocking encrypted devices during boot.

```bash
echo CRYPTSETUP=y >> /etc/cryptsetup-initramfs/conf-hook

```

--------------------------------

### Configure Debian Control File for FinalRecon Package

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet illustrates the configuration of the debian/control file for the FinalRecon package. It specifies package metadata, build dependencies, and runtime dependencies, including Python libraries. The 'Architecture: all' setting is typical for Python scripts.

```bash
kali@kali:~/kali/packages/finalrecon$ vim debian/control
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ cat debian/control
Source: finalrecon
Section: misc
Priority: optional
Maintainer: Kali Developers <devel@kali.org>
Uploaders: Joseph O'Gorman <gamb1t@kali.org>
Build-Depends: debhelper-compat (= 12),
               dh-python,
               python3-aiodns,
               python3-aiohttp,
               python3-all,
               python3-bs4,
               python3-dnslib,
               python3-icmplib,
               python3-ipwhois,
               python3-lxml,
               python3-psycopg2,
               python3-requests,
               python3-tldextract,
Standards-Version: 4.5.0
Homepage: https://github.com/thewhiteh4t/FinalRecon
Vcs-Browser: https://gitlab.com/kalilinux/packages/finalrecon
Vcs-Git: https://gitlab.com/kalilinux/packages/finalrecon

Package: finalrecon
Architecture: all
Depends: ${misc:Depends},
         ${python3:Depends},
         python3-aiodns,
         python3-aiohttp,
         python3-bs4,
         python3-dnslib,
         python3-icmplib,
         python3-ipwhois,
         python3-lxml,
         python3-psycopg2,
         python3-requests,
         python3-tldextract,
Description: A fast and simple python script for web reconnaissance
 A fast and simple python script for web reconnaissance that follows
 a modular structure and provides detailed information on various areas.
kali@kali:~/kali/packages/finalrecon$

```

--------------------------------

### Clone cryptmypi Script for Automation

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Clones the cryptmypi script repository from GitHub. This script is designed to automate the process of setting up an encrypted Kali Linux system, reducing manual effort.

```bash
kali@kali:~$ git clone https://github.com/unixabg/cryptmypi.git

```

--------------------------------

### Configure Login Screen DPI for HiDPI

Source: https://www.kali.org/docs/general-use/hidpi

Adjusts the 'xft-dpi' setting in the LightDM greeter configuration file (/etc/lightdm/lightdm-gtk-greeter.conf) to improve the display of the login screen on HiDPI monitors. A value of 180 or higher is suggested.

```bash
kali@kali:~$ grep xft-dpi /etc/lightdm/lightdm-gtk-greeter.conf
xft-dpi = 96
kali@kali:~$ 
kali@kali:~$ sudo vim /etc/lightdm/lightdm-gtk-greeter.conf
kali@kali:~$ 
kali@kali:~$ cat /etc/lightdm/lightdm-gtk-greeter.conf
[greeter]
[...]
xft-dpi = 180
[...]
kali@kali:~$
```

--------------------------------

### Fetch ODROID Kernel Sources

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This snippet fetches the ODROID kernel sources using git and places them in the specified directory. It uses a specific branch ('odroid-3.8.y') and creates an empty '.scmversion' file.

```bash
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/
kali@kali:~$ cd ~/arm-stuff/kernel/
kali@kali:~$ git clone --depth 1 https://github.com/hardkernel/linux.git -b odroid-3.8.y odroid
kali@kali:~$ cd odroid/
kali@kali:~$ touch .scmversion

```

--------------------------------

### Create ext4 Filesystem and Label

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This command creates an ext4 filesystem on the opened LUKS container (`/dev/mapper/my_usb`) and labels it 'persistence'. The ext4 filesystem is a common choice for Linux partitions. The output confirms the filesystem creation and provides its UUID.

```bash
kali@kali:~$ sudo mkfs.ext4 -L persistence /dev/mapper/my_usb
mke2fs 1.47.2 (1-Jan-2025) 
Creating filesystem with 14110720 4k blocks and 3530752 inodes
Filesystem UUID: aca1783a-4665-4077-b555-c748e391def1
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
	4096000, 7962624, 11239424

Allocating group tables: done
Writing inode tables: done
Creating journal (65536 blocks): done
Writing superblocks and filesystem accounting information: done

kali@kali:~$ 

```

--------------------------------

### Partition and Format Image File

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

Uses parted and gdisk to create a GPT partition table with three partitions within the disk image. It then sets up loop devices, maps partitions using kpartx, and formats the third partition as ext4.

```bash
kali@kali:~$ parted kali-custom-chrome.img --script -- mklabel msdos
kali@kali:~$ parted kali-custom-chrome.img --script -- mktable gpt
kali@kali:~$ gdisk kali-custom-chrome.img <<EOF
x
l
8192
m
n
1

+16M
7f00
n
2

+16M
7f00
n
3

w
y
EOF

kali@kali:~$ loopdevice=`losetup -f --show kali-custom-chrome.img`
kali@kali:~$ device=`kpartx -va $loopdevice| sed -E 's/.*(loop[0-9])p.*/\1/g' | head -1`
kali@kali:~$ device="/dev/mapper/${device}"
kali@kali:~$ bootp1=${device}p1
kali@kali:~$ bootp2=${device}p2
kali@kali:~$ rootp=${device}p3

kali@kali:~$ mkfs.ext4 $rootp
kali@kali:~$ mkdir -p root
kali@kali:~$ mount $rootp root

```

--------------------------------

### Upgrade WSL Distribution to Version 2 (PowerShell)

Source: https://www.kali.org/docs/wsl/wsl-preparations

This command upgrades a specified WSL distribution (e.g., 'kali-linux') to WSL version 2. The process may take a few minutes. It's essential to run this command to leverage WSL 2 features for existing distributions.

```powershell
wsl --set-version kali-linux 2
```

--------------------------------

### Configure Version Tracking in debian/watch

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the debian/watch file configuration for tracking the latest Git commit of the FinalRecon project. It includes commented-out options for tracking tagged releases, which can be enabled later.

```text
version=4
opts=mode=git,pgpmode=none \
  https://github.com/thewhiteh4t/FinalRecon HEAD

# Use the following when upstream starts to tag releases:
#opts=filenamemangle=s/.+\/v?(\d\S+)\.tar\.gz/finalrecon-$1\.tar\.gz/ \
#  https://github.com/thewhiteh4t/FinalRecon/tags .*/v?(\d\S+)\.tar\.gz
```

--------------------------------

### Flash Kali Linux Image to microSD Card (Raspberry Pi 400)

Source: https://www.kali.org/docs/arm/raspberry-pi-400

This command uses `xzcat` to decompress the Kali Linux image and `dd` to write it to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss on other drives. The `bs=4M` option sets the block size for faster writing, and `status=progress` shows the writing progress.

```bash
xzcat kali-linux-2025.4-raspberry-pi-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress

```

```bash
xzcat kali-linux-2025.4-raspberry-pi-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress

```

--------------------------------

### Copy Kali Rootfs and Configure Network

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Copies the pre-built Kali root filesystem into the mounted image directory using rsync. It also sets up a basic DNS resolver configuration by adding Google's nameserver to the resolv.conf file within the rootfs.

```bash
kali@kali:~$ rsync -HPavz /root/arm-stuff/rootfs/kali-armhf-xfce4/ root
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf

```

--------------------------------

### Image ODROID System to SD Card

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This snippet covers the final steps of preparing the SD card for the ODROID. It includes unmounting partitions, detaching loop devices, downloading and extracting a boot archive, and using a script ('sd_fusing.sh') to flash the image. The core operation is using 'dd' to write the Kali Linux ODROID image to the specified device, which requires careful attention to the correct device label.

```bash
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ umount $bootp
kali@kali:~$ umount $rootp
kali@kali:~$ kpartx -dv $loopdevice
kali@kali:~$ wget http://www.mdrjr.net/odroid/mirror/old-releases/BSPs/Alpha4/unpacked/boot.tar.gz
kali@kali:~$ tar -zxpf boot.tar.gz
kali@kali:~$ cd boot/
kali@kali:~$ sh sd_fusing.sh $loopdevice
kali@kali:~$ cd ../
kali@kali:~$ losetup -d $loopdevice
kali@kali:~$ dd if=kali-linux-odroid.img of=/dev/sdX conv=fsync bs=4M

```

--------------------------------

### Pack Kernel with Vbutil for SD and USB Boot

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This section uses the 'vbutil_kernel' tool to pack the compiled kernel image ('kernel.itb') with specific boot configurations for both SD and USB devices. It utilizes predefined keyblocks and private keys for signing the kernel, creating 'newkern-sd' and 'newkern-usb' files.

```bash
kali@kali:~$ vbutil_kernel --pack /tmp/newkern-sd --keyblock /usr/share/vboot/devkeys/kernel.keyblock --version 1 --signprivate /usr/share/vboot/devkeys/kali@kali:~$ kernel_data_key.vbprivk --config=/tmp/config-sd --vmlinuz kernel.itb --arch arm
kali@kali:~$ vbutil_kernel --pack /tmp/newkern-usb --keyblock /usr/share/vboot/devkeys/kernel.keyblock --version 1 --signprivate /usr/share/vboot/devkeys/kali@kali:~$ kernel_data_key.vbprivk --config=/tmp/config-usb --vmlinuz kernel.itb --arch arm
```

--------------------------------

### Fix 'Authentication Required to Create Managed Color Device' Error

Source: https://www.kali.org/docs/general-use/xfce-with-rdp

This configuration snippet resolves a common polkit error related to color management when connecting via RDP. It creates a policy file that grants all users the necessary permissions to manage color devices, allowing the Xfce desktop to initialize correctly without authentication prompts.

```shell
kali@kali:~$ cat <<EOF | sudo tee /etc/polkit-1/localauthority/50-local.d/45-allow-colord.pkla
[Allow Colord all Users]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
ResultAny=no
ResultInactive=no
ResultActive=yes
EOF
kali@kali:~$ 

```

--------------------------------

### Adjust Chroots for Kali Builds

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Configures the mmdebstrap arguments for Kali chroots, specifying components, keyring, and APT source list modifications. This snippet is typically used within a Perl script or configuration file for build systems.

```perl
push @{$unshare_mmdebstrap_extra_args}, "kali-*", [
  '--components=main contrib non-free non-free-firmware',
  '--include=kali-archive-keyring',
  '--setup-hook=sed -i s/https/http/ "$1"/etc/apt/sources.list',
];
EOF
```

--------------------------------

### Generate SHA256 Checksum (Windows)

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Generates the SHA256 checksum for a downloaded Kali Linux ISO image file using the certutil command. Requires certutil to be available in the Windows environment.

```bash
certutil -hashfile kali-linux-2025.4-live-amd64.iso sha256

```

--------------------------------

### Configure Root File System fstab

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Creates an fstab file for the root file system, defining mount points for the root partition and the U-Boot boot partition. This ensures proper mounting of file systems upon boot.

```bash
kali@kali:~$ cat <<EOF > root/etc/fstab
/dev/mmcblk0p2 / auto errors=remount-ro 0 1
/dev/mmcblk0p1 /boot/uboot auto defaults 0 0
EOF
```

--------------------------------

### Configure Kali Boot for Encrypted Filesystem

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Steps to mount necessary directories, chroot into the encrypted system, and update boot configuration files like fstab and initramfs for proper booting with LUKS encryption. It includes commands to check UUIDs and edit unlock scripts.

```bash
$ sudo mount /dev/sdX1 /mnt/encrypted/boot/
$ sudo mount -t proc none /mnt/encrypted/proc
$ sudo mount -t sysfs none /mnt/encrypted/sys
$ sudo mount -o bind /dev /mnt/encrypted/dev
$ sudo mount -o bind /dev/pts /mnt/encrypted/dev/pts
$ sudo env LANG=C chroot /mnt/encrypted
┌──(root㉿kali)-[/]
└─# blkid /dev/sdX2
/dev/sdX2: UUID="173e2de4-0501-4d8e-9039-a4923bfa5ee7" TYPE="crypto_LUKS" PARTUUID="e1750e08-02"

┌──(root㉿kali)-[/]
└─# cat /etc/fstab
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
proc            /proc           proc    defaults          0       0

UUID=173e2de4-0501-4d8e-9039-a4923bfa5ee7 /               ext4 errors=remount-ro 0       1
LABEL=BOOT      /boot           vfat    defaults          0       2

┌──(root㉿kali)-[/]
└─# vim /etc/initramfs-tools/unlock.sh

┌──(root㉿kali)-[/]
└─# cat /etc/initramfs-tools/unlock.sh
#!/bin/sh

export PATH='/sbin:/bin:/usr/sbin:/usr/bin'

while true; do
	test -e /dev/mapper/crypt && break || cryptsetup luksOpen /dev/disk/by-uuid/173e2de4-0501-4d8e-9039-a4923bfa5ee7 crypt
done

/scripts/local-top/cryptroot
for i in $(ps aux | grep 'cryptroot' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i; done
for i in $(ps aux | grep 'askpass' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i; done
for i in $(ps aux | grep 'ask-for-password' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i; done
for i in $(ps aux | grep '\-sh' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i; done
exit 0

┌──(root㉿kali)-[/]
└─# vim /etc/crypttab

┌──(root㉿kali)-[/]
└─# cat /etc/crypttab
crypt	PARTUUID=e1750e08-02	none	luks

┌──(root㉿kali)-[/]
└─# mkinitramfs -o /boot/initramfs.gz 5.15.44-Re4son-v8l+

```

--------------------------------

### Check Device CPU ABI using ADB Shell

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This snippet demonstrates how to connect to a device via ADB shell and check its CPU Application Binary Interface (ABI). This is useful for determining compatibility with software, especially for devices like the OnePlus One which is ARM but not ARM64. The output 'armeabi-v7a' confirms the ARM architecture.

```bash
kali@kali:~$ adb shell
bacon:/ $ getprop ro.product.cpu.abi
armeabi-v7a
bacon:/ $
```

--------------------------------

### Add Kali Source Repository

Source: https://www.kali.org/docs/general-use/kali-linux-sources-list-repositories

Appends a deb-src line to the /etc/apt/sources.list file, enabling the download of source packages. This is useful for compiling software or debugging issues by examining the source code.

```bash
kali@kali:~$ echo "deb-src http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware" | sudo tee -a /etc/apt/sources.list

```

--------------------------------

### Troubleshoot Xorg Display Issues (Raspberry Pi 400)

Source: https://www.kali.org/docs/arm/raspberry-pi-400

This command moves the `99-vc4.conf` file from its default location to the user's home directory. This action attempts to resolve display issues on the Raspberry Pi 400 by allowing Xorg to use its default display configurations instead of potentially conflicting settings.

```bash
kali@kali:~$ sudo mv -v /etc/X11/Xorg.conf.d/99-vc4.conf ~

```

--------------------------------

### Configure Boot Files for Beaglebone Black

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Creates a uEnv.txt file for boot configuration and copies the compiled kernel image (zImage), device tree blobs (dtbs), modules, and firmware to their respective locations on the boot and root file systems.

```bash
kali@kali:~$ cat <<EOF > boot/uEnv.txt
mmcroot=/dev/mmcblk0p2 ro
mmcrootfstype=ext4 rootwait fixrtc
uenvcmd=run loaduimage; run loadfdt; run mmcargs; bootz 0x80200000 - 0x80F80000
EOF
kali@kali:~$ cp -v kernel/linux-dev/deploy/3.8.13-bone20.zImage boot/zImage
kali@kali:~$ mkdir -p boot/dtbs
kali@kali:~$ tar -xovf kernel/linux-dev/deploy/3.8.13-bone20-dtbs.tar.gz -C boot/dtbs/
kali@kali:~$ tar -xovf kernel/linux-dev/deploy/3.8.13-bone20-modules.tar.gz -C root/
kali@kali:~$ tar -xovf kernel/linux-dev/deploy/3.8.13-bone20-firmware.tar.gz -C root/lib/firmware/
```

--------------------------------

### Configure Git Merge Driver for debian/changelog

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Adds a custom Git merge driver configuration for debian/changelog files. This ensures that changes to changelog files are handled correctly during merges. It also sets up the attributes file to use this merge driver.

```bash
kali@kali:~$ cat <<EOF >> ~/.gitconfig
[merge "dpkg-mergechangelogs"]
         name = debian/changelog merge driver
         driver = dpkg-mergechangelogs -m %O %A %B %A
EOF
kali@kali:~$ 
kali@kali:~$ mkdir -pv ~/.config/git/
kali@kali:~$ 
kali@kali:~$ grep mergechangelogs ~/.config/git/attributes \
  || echo "debian/changelog merge=dpkg-mergechangelogs" >> ~/.config/git/attributes
kali@kali:~$
```

--------------------------------

### Customize Kali ISO Package List

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This snippet shows how to overwrite the default Kali package list. By creating a custom `kali.list.chroot` file, you can specify exactly which packages should be included in the final ISO, ensuring a lean and tailored distribution.

```bash
kali@kali:~$ cat <<EOF > kali-config/variant-default/package-lists/kali.list.chroot
kali-root-login
kali-defaults
kali-menu
kali-debtags
kali-archive-keyring
debian-installer-launcher
alsa-tools
locales-all
dconf-tools
openssh-server
EOF

```

--------------------------------

### Create and Execute Unlock Script for Initramfs (Bash)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This script, `unlock.sh`, is designed to run within the initramfs environment. It attempts to open an encrypted LUKS device using `cryptsetup` and then cleans up related processes. It requires the `cryptsetup` package and assumes the encrypted device is accessible via `/dev/disk/by-uuid/`.

```bash
#!/bin/sh

export PATH='/sbin:/bin:/usr/sbin:/usr/bin'

while true; do
	test -e /dev/mapper/crypt && break || cryptsetup luksOpen /dev/disk/by-uuid/$REPLACE_LATER crypt
done

/scripts/local-top/cryptroot
for i in $(ps aux | grep 'cryptroot' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i;
done
for i in $(ps aux | grep 'askpass' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i;
done
for i in $(ps aux | grep 'ask-for-password' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i;
done
for i in $(ps aux | grep '\-sh' | grep -v 'grep' | awk '{print $1}'); do kill -9 $i;
done
exit 0
```

--------------------------------

### Configure Win-KeX Seamless Mode in Windows Terminal

Source: https://www.kali.org/docs/wsl/win-kex

This configuration sets up a basic Windows Terminal profile for Win-KeX in seamless mode with sound enabled. It uses the '--sl' flag for seamless mode and specifies the command to execute WSL with Kali Linux.

```json
{
      "guid": "{55ca431a-3a87-5fb3-83cd-11ececc031d2}",
      "hidden": false,
      "name": "Win-KeX",
      "commandline": "wsl -d kali-linux kex --sl --wtstart -s"
}
```

--------------------------------

### Debian Copyright File Structure

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This snippet shows the basic structure of a debian/copyright file, including format, source, upstream information, file sections, copyright holders, and license details. It adheres to the Debian copyright format specification.

```text
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Source: <url://example.com>
Upstream-Name: instaloader
Upstream-Contact: <preferred name and address to reach the upstream project>

Files:
 *
Copyright:
 <years> <put author's name and email here>
 <years> <likewise for another author>
License: <special license>
 <Put the license of the package here indented by 1 space>
 <This follows the format of Description: lines in control file>
 .
 <Including paragraphs>

Files:
 debian/*
Copyright:
 2020 Joseph O'Gorman <gamb1t@kali.org>
License: GPL-2+
 This package is free software; you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation; either version 2 of the License, or
 (at your option) any later version.
 .
 This package is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.
 .
 You should have received a copy of the GNU General Public License
 along with this program. If not, see <https://www.gnu.org/licenses/>
Comment:
 On Debian systems, the complete text of the GNU General
 Public License version 2 can be found in "/usr/share/common-licenses/GPL-2".
```

--------------------------------

### Copy Rootfs and Configure Serial Console

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Copies the pre-built Kali armhf root filesystem to the mounted image using rsync. It then configures the serial console by modifying the inittab file to add a getty process for ttySAC1, optionally enabling autologin. It also ensures ttySAC1 is linked correctly in udev and adds serial console entries to securetty.

```bash
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ rsync -HPavz ~/arm-stuff/rootfs/kali-armhf/ root
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf

# Edit ~/arm-stuff/images/root/etc/inittab
# Add to the 'Example how to put a getty on a serial line' section:
T1:12345:respawn:/sbin/agetty 115200 ttySAC1 vt100
# Or for autologin:
T1:12345:respawn:/bin/login -f root ttySAC1 /dev/ttySAC1 >&1

# Edit ~/arm-stuff/images/root/etc/udev/links.conf to ensure ttySAC1 entry exists:
M null c 1 3
M console c 5 1
M ttySAC1 c 5 1

# Add ttySAC entries to securetty:
kali@kali:~$ cat <<EOF >> root/etc/securetty
ttySAC0
ttySAC1
ttySAC2
EOF

```

--------------------------------

### Flash Kali Linux Image to microSD Card using dd

Source: https://www.kali.org/docs/arm/beaglebone-black

This command uses the 'dd' utility to write a compressed Kali Linux image file to a microSD card. It's crucial to replace '/dev/sdX' with the correct device path for your microSD card to avoid data loss on other drives. The 'xzcat' command decompresses the image on the fly, and 'status=progress' provides feedback during the operation.

```bash
xzcat images/kali-linux-2025.4-beaglebone-black-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Edit Debian Changelog - Shell and Plain Text

Source: https://www.kali.org/docs/development/intermediate-packaging-example

This snippet demonstrates the process of editing and viewing the debian/changelog file using shell commands. It shows the initial command to open the file in vim and then displays the content of the changelog file after modifications.

```shell
kali@kali:~/kali/packages/photon$ vim debian/changelog
kali@kali:~/kali/packages/photon$ 
kali@kali:~/kali/packages/photon$ cat debian/changelog
photon (1.3.0-0kali1) kali-dev; urgency=medium

  * Initial release

 -- Joseph O'Gorman <gamb1t@kali.org>  Mon, 13 Jul 2020 17:28:51 -0400
kali@kali:~/kali/packages/photon$ 

```

--------------------------------

### Write Kali Linux Image to Radxa Zero eMMC (Linux - SD Card Boot)

Source: https://www.kali.org/docs/arm/radxa-zero-emmc

Writes a Kali Linux image to the Radxa Zero's eMMC by first booting the device from a microSD card. The image is then transferred to the eMMC using the 'dd' utility. **Warning**: Ensure `/dev/mmcblk0` is the correct device path to avoid data loss on other drives.

```bash
xzcat kali-linux-2025.4-radxa-zero-emmc-arm64.img.xz | sudo dd of=/dev/mmcblk0 bs=4M status=progress
```

--------------------------------

### Run Win-KeX in Enhanced Session Mode

Source: https://www.kali.org/docs/wsl/win-kex

Launches Win-KeX using an enhanced session mode, similar to Hyper-V, with sound support and an ARM workaround. This command can be run from Kali WSL or Windows command prompt.

```bash
kex --esm --ip -s
```

```bash
wsl -d kali-linux kex --esm --ip -s
```

--------------------------------

### Configure and Compile Mali Driver (Shell)

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Configures the Mali driver build with specific compiler flags and library paths, then compiles the driver. This step involves setting environment variables for compilation and running the configure script.

```shell
kali@kali:~$ CFLAGS="-O3 -Wall -W -Wextra -I/usr/include/libdrm -IDX910-SW-99006-r3p2-01rel0/driver/src/ump/include" LDFLAGS="-L/usr/lib -lMali -lUMP -lpthread" ./configure --prefix=/usr --x-includes=/usr/include --x-libraries=/usr/lib
kali@kali:~$ cp -rf ../../../DX910-SW-99006-r3p2-01rel0/driver/src/ump/include/ump src/
kali@kali:~$ mkdir -p umplock/
kali@kali:~$ cd umplock/
kali@kali:~$ wget http://service.i-onik.de/a10_source_1.5/lichee/linux-3.0/modules/mali/DX910-SW-99002-r3p0-04rel0/driver/src/devicedrv/umplock/umplock_ioctl.h
kali@kali:~$ cd ../
kali@kali:~$
```

--------------------------------

### Reboot to Enable Live USB Persistence

Source: https://www.kali.org/docs/usb/usb-persistence

After setting up the persistence, this command initiates a system reboot. Upon rebooting, the user should select the 'Live USB Persistence' option from the boot menu to utilize the configured persistence.

```bash
kali@kali:~$ reboot

```

--------------------------------

### Copy Kali Rootfs and Configure System

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

Copies the Kali root filesystem to the mounted image using rsync. It then sets the DNS server and creates a custom Xorg configuration file for touchpad settings.

```bash
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ rsync -HPavz ~/arm-stuff/rootfs/kali-armhf/ root
kali@kali:~$ 
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf
kali@kali:~$ 
kali@kali:~$ mkdir -p root/etc/X11/xorg.conf.d/
kali@kali:~$ cat <<EOF > root/etc/X11/xorg.conf.d/50-touchpad.conf
Section "InputClass"
Identifier "touchpad"
MatchIsTouchpad "on"
Driver "synaptics"
Option "TapButton1" "1"
Option "TapButton2" "3"
Option "TapButton3" "2"
Option "FingerLow" "15"
Option "FingerHigh" "20"
Option "FingerPress" "256"
EndSection
EOF

```

--------------------------------

### Manual ftpsync Trigger for Testing

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Manually triggers a synchronization run using the `ftpsync` script for testing purposes. This command is executed as the dedicated mirror user and specifies the sync action and the target repository.

```bash
$ whoami
archvsync
$ ~/bin/ftpsync sync:archive:kali

```

--------------------------------

### Image Kali Linux to microSD Card for RIoTboard (Shell)

Source: https://www.kali.org/docs/arm/riotboard

This command uses `xzcat` and `dd` to decompress and write a Kali Linux image file to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss on other drives. The `bs=4M` option sets the block size for faster writing, and `status=progress` shows the transfer progress.

```shell
xzcat kali-linux-2025.4-riotboard-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress

```

--------------------------------

### Create New Persistent Partition

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This command uses `fdisk` to create a new partition on the USB drive for persistence. It interactively prompts for partition type and size. The `printf` command provides automated input to `fdisk` for creating a primary partition in the remaining space.

```bash
kali@kali:~$ sudo fdisk /dev/sdX <<< $(printf "p\nn\np\n\n\n\np\nw")

```

--------------------------------

### Flash LineageOS and GApps using ADB Sideload

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This snippet demonstrates how to flash a LineageOS build and MindTheGapps package onto an Android device using ADB sideload. Ensure ADB is set up and the device is in recovery mode.

```bash
adb -d sideload lineage-22.2-20250627-nightly-beyond1lte-signed.zip
adb -d sideload MindTheGapps-15.0.0-arm64-20250214_082511.zip
```

--------------------------------

### Define Private Network for Inter-Component Communication

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This YAML configuration defines a private network named 'hello-kbx' for Kaboxer components. Components connected to this network can communicate with each other, even if they are not directly accessible from the host.

```yaml
components:
  default:
    [...]
    networks:
      - hello-kbx

```

--------------------------------

### Debian Watch File for Version Monitoring

Source: https://www.kali.org/docs/development/intermediate-packaging-example

Specifies how to monitor for new upstream versions of the 'photon' package. It uses version 4 of the watch file format and defines a filename mangling rule for tarballs.

```watch
version=4
opts=filenamemangle=s/.+/v?(\d\S+)\.tar\.gz/photon-$1\.tar\.gz/ \
  https://github.com/s0md3v/photon/tags .*/v?(\d\S+)\.tar\.gz
```

--------------------------------

### Build Package with sbuild (After Committing Changes)

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This command attempts to build the package again after ensuring all necessary changes, including debian/ files, are committed to Git. It demonstrates the successful export and build process.

```bash
kali@kali:~/kali/packages/instaloader$ gbp buildpackage --git-builder=sbuild
gbp:info: Exporting 'HEAD' to '/home/kali/kali/build-area/instaloader-tmp'
gbp:info: Moving '/home/kali/kali/build-area/instaloader-tmp' to '/home/kali/kali/build-area/instaloader-4.4.4'
gbp:info: Performing the build
dh clean --with python3 --buildsystem=pybuild
[...] 
+------------------------------------------------------------------------------+
| Package contents                                                             |
+------------------------------------------------------------------------------+

[...] 

Install lintian build dependencies (apt-based resolver)
-------------------------------------------------------

[...] 

E: instaloader source: source-is-missing [docs/_static/bootstrap-4.1.3.bundle.min.js]
W: instaloader: no-manual-page [usr/bin/instaloader]

E: Lintian run failed (runtime error)

[...] 

+------------------------------------------------------------------------------+
| Summary                                                                      |

```

--------------------------------

### Enable ARM Cross-Compilation Environment

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

This section details how to set up the cross-compilation environment for ARM builds. It involves exporting the architecture and cloning a specific GCC toolchain.

```bash
kali@kali:~$ export ARCH=arm
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/toolchains/
kali@kali:~$ cd ~/arm-stuff/kernel/toolchains/
kali@kali:~$ git clone git://gitlab.com/kalilinux/packages/gcc-arm-eabi-linaro-4-6-2.git
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/gcc-arm-eabi-linaro-4.6.2/bin/arm-eabi-
```

--------------------------------

### Enable SSH Service on Kali ISO Build via Chroot Hook

Source: https://www.kali.org/docs/development/dojo-mastering-live-build

This snippet demonstrates enabling the SSH service by default on the custom Kali ISO. It uses a chroot hook script (`01-start-ssh.chroot`) to execute `systemctl enable ssh` during the build process, ensuring SSH is active on first boot.

```bash
kali@kali:~$ echo 'systemctl enable ssh' >>  kali-config/common/hooks/01-start-ssh.chroot
kali@kali:~$ chmod +x kali-config/common/hooks/01-start-ssh.chroot

```

--------------------------------

### Debian Rules Makefile Skeleton

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This snippet shows the beginning of a debian/rules file, which is a Makefile used for building Debian packages. It includes commented-out options for verbosity and build flags.

```makefile
#!/usr/bin/make -f

# See debhelper(7) (uncomment to enable).
# Output every command that modifies files on the build system.
#export DH_VERBOSE = 1


# See FEATURE AREAS in dpkg-buildflags(1).
#export DEB_BUILD_MAINT_OPTIONS = hardening=+all

# See ENVIRONMENT in dpkg-buildflags(1).

```

--------------------------------

### Create Initramfs for Kali Linux on Raspberry Pi

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This command generates an initramfs archive, which is essential for the boot process, especially when dealing with encrypted root filesystems. It requires the specific kernel version and name to be provided.

```bash
mkinitramfs -o /boot/initramfs.gz 5.15.44-Re4son-v8l+
```

--------------------------------

### Basic Debian Rules File Structure

Source: https://www.kali.org/docs/development/intro-to-packaging-example

A minimal debian/rules file using 'dh' to pass all arguments. This serves as a base for more complex build configurations, often seen in Debian packaging.

```makefile
%:
	dh $@

```

--------------------------------

### Configure and Cross-Compile ODROID Kernel

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

This section details the configuration and cross-compilation of the ODROID kernel. It involves setting environment variables for the architecture and cross-compiler, applying default configurations for specific ODROID models, enabling kernel options like LZMA compression, and performing the compilation using multiple cores. A modification to 'include/uapi/drm/drm.h' is also included for cross-compilation scenarios.

```bash
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/arm-eabi-linaro-4.6.2/bin/arm-eabi-
kali@kali:~$ # for ODROID-X2
kali@kali:~$ make odroidx2_defconfig
kali@kali:~$ # for ODROID-U2
kali@kali:~$ make odroidu2_defconfig
kali@kali:~$ # configure your kernel !
kali@kali:~$ make menuconfig
kali@kali:~$ # and enable
kali@kali:~$ CONFIG_HAVE_KERNEL_LZMA=y
kali@kali:~$ CONFIG_RD_LZMA=y
kali@kali:~$ # If cross compiling, run this once
kali@kali:~$ sed -i 's/if defined(__linux__)/if defined(__linux__) ||defined(__KERNEL__) /g' include/uapi/drm/drm.h
kali@kali:~$ make -j $(cat /proc/cpuinfo|grep processor | wc -l)
kali@kali:~$ make modules_install INSTALL_MOD_PATH=~/arm-stuff/images/root/

```

--------------------------------

### Check Attached Devices in Fastboot Mode

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This command verifies that the Fastboot tool can detect the device while it is in bootloader mode. It lists connected devices recognized by Fastboot. This is a crucial step after rebooting into bootloader mode.

```bash
kali@kali:~$ fastboot devices
dea044c9     fastboot

kali@kali:~

```

--------------------------------

### Add and Commit Debian Files

Source: https://www.kali.org/docs/development/intro-to-packaging-example

These commands add the debian/ directory containing package control files to Git and then commit them with a message. This is a prerequisite for a successful sbuild if changes were not previously committed.

```bash
kali@kali:~/kali/packages/instaloader$ git add debian/
kali@kali:~/kali/packages/instaloader$
kali@kali:~/kali/packages/instaloader$ git commit -m "Initial release"
[kali/master 10a9e96] Add debian/ files
 8 files changed, 94 insertions(+)
 create mode 100644 debian/changelog
 create mode 100644 debian/control
 create mode 100644 debian/copyright
 create mode 100755 debian/helper-script/instaloader
 create mode 100644 debian/instaloader.install
 create mode 100755 debian/rules
 create mode 100644 debian/source/format
 create mode 100644 debian/watch
kali@kali:~/kali/packages/instaloader$
```

--------------------------------

### Prepare and Mount Rootfs for Kali ARM Build

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Sets environment variables and mounts necessary directories for the chroot environment during the Kali ARM rootfs build process. It ensures proper isolation and access to host system resources.

```shell
kali@kali:~$ export MALLOC_CHECK_=0 # workaround for LP: #520465
kali@kali:~$ export LC_ALL=C
kali@kali:~$ export DEBIAN_FRONTEND=noninteractive
kali@kali:~$ 
kali@kali:~$ mount -t proc proc kali-$architecture/proc
kali@kali:~$ mount -o bind /dev/ kali-$architecture/dev/
kali@kali:~$ mount -o bind /dev/pts kali-$architecture/dev/pts
kali@kali:~$ 
kali@kali:~$ cat <<EOF > kali-$architecture/debconf.set
console-common console-data/keymap/policy select Select keymap from full list
console-common console-data/keymap/full select en-latin1-nodeadkeys
EOF
```

--------------------------------

### Fetch Chromium Kernel Sources

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This snippet demonstrates how to create a directory, navigate into it, and clone the Chromium kernel sources from a Git repository. It specifies a particular branch ('chromeos-3.4') for the kernel version.

```bash
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/
kali@kali:~$ cd ~/arm-stuff/kernel/
kali@kali:~$ git clone http://git.chromium.org/chromiumos/third_party/kernel.git -b chromeos-3.4 chromeos
kali@kali:~$ cd chromeos/
```

--------------------------------

### Image Mini-X microSD Card with Kali Linux using dd

Source: https://www.kali.org/docs/arm/mini-x

This command uses `xzcat` to decompress the Kali Linux image and pipes it to `dd` for writing to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss.

```bash
xzcat kali-linux-2025.4-mini-x-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Generate SHA256 Checksum (Linux/macOS)

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Calculates the SHA256 checksum for a downloaded Kali Linux ISO image file. Assumes the ISO file is in the current directory.

```bash
$ shasum -a 256 kali-linux-2025.4-live-amd64.iso

```

--------------------------------

### Verify USB Drive Partitions with lsblk

Source: https://www.kali.org/docs/usb/usb-persistence

This command displays the block devices and their partitions, helping to identify the USB drive and its existing partitions. It's crucial for determining the correct device name and partition numbers before proceeding.

```bash
kali@kali:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:16   0   2.7T  0 disk
├─sda1   8:17   0   512M  0 part /boot/efi
├─sda2   8:18   0   2.7T  0 part /
└─sda3   8:19   0   977M  0 part [SWAP]
sdX      8:32   1  58.4G  0 disk
├─sdX1   8:33   1   4.6G  0 part
└─sdX2   8:34   1     4M  0 part
kali@kali:~$ 
kali@kali:~$ usb=/dev/sdX

```

--------------------------------

### Define Kaboxer Application Metadata (YAML)

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This YAML file defines the metadata for a Kaboxer application, including its ID, name, description, packaging revision, and component run mode and executable. It's crucial for distributing and running containerized applications seamlessly.

```yaml
application:
  id: hello-cli
  name: Hello World for Kaboxer (CLI)
  description: >
    hello-kbx is the hello-world application demonstrator for Kaboxer
packaging:
  revision: 1
components:
  default:
    run_mode: cli
    executable: /usr/bin/hello cli

```

--------------------------------

### Verify GNOME Wayland Configuration

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

Command to search for Wayland-related configurations within the GDM3 directory. This helps in verifying if Wayland is enabled or commented out in the GDM configuration file, which is important for GNOME sessions.

```bash
sudo grep -r "Wayland" /etc/gdm3/
```

--------------------------------

### Download Kali Linux LXC Image (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Creates a new Kali Linux LXC container named 'my-kali' by downloading the latest image from the official image server. Prompts the user for distribution, release, and architecture details.

```bash
kali@kali:~$ lxc-create -t download -n my-kali

```

--------------------------------

### Configure and Build Kernel

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Sets up ARM cross-compilation environment variables, applies a default kernel configuration for MK808, allows for manual configuration via menuconfig, and then builds the kernel and its modules. It also downloads and copies firmware files required for hardware support.

```bash
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/arm-eabi-linaro-4.6.2/bin/arm-eabi-
kali@kali:$

# A basic configuration for the UG802 and MK802 III
# make rk30_hotdog_ti_defconfig

# A basic configuration for the MK808
kali@kali:~$ make rk30_hotdog_defconfig

kali@kali:~$ # configure your kernel !
kali@kali:~$ make menuconfig

kali@kali:~$ # Configure the kernel as per http://www.armtvtech.com/armtvtechforum/viewtopic.php?f=66&t;=835
kali@kali:~$ ./make_kernel_ruikemei.sh

```

```bash
kali@kali:~$ make modules -j$(cat /proc/cpuinfo|grep processor | wc -l)
kali@kali:~$ make modules_install INSTALL_MOD_PATH=~/arm-stuff/images/root
kali@kali:~$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/dwmw2/linux-firmware.git firmware-git
kali@kali:~$ mkdir -p ~/arm-stuff/images/root/lib/firmware
kali@kali:~$ cp -rf firmware-git/* ~/arm-stuff/images/root/lib/firmware/
kali@kali:~$ rm -rf firmware-git

```

--------------------------------

### Configure rEFInd on macOS/OS X El Capitan and later

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

Provides steps to mount the EFI boot volume on macOS/OS X El Capitan (10.11) or later to access and edit the rEFInd configuration file. It uses a custom script 'mountesp' to mount the EFI System Partition (ESP).

```bash
$ cd ~/Downloads/refind-bin-*
$ 
$ sudo ./mountesp
The ESP has been identified as /dev/disk0s1; attempting to mount it....
The ESP is mounted at /Volumes/ESP
username@Usernames-Mac refind-bin-0.12.0 %

$ 
$ vim /Volumes/ESP/EFI/refind/refind.conf
$ 

```

--------------------------------

### Compile U-Boot for Beaglebone Black

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Clones the U-Boot repository, checks out a specific version, applies a patch, and configures and compiles U-Boot for the am335x_evm target. This prepares the bootloader for the Beaglebone Black.

```bash
kali@kali:~$ git clone git://git.denx.de/u-boot.git
kali@kali:~$ cd u-boot/
kali@kali:~$ git checkout v2013.04 -b beaglebone-black
kali@kali:~$ wget https://raw.github.com/eewiki/u-boot-patches/master/v2013.04/0001-am335x_evm-uEnv.txt-bootz-n-fixes.patch
kali@kali:~$ patch -p1 < 0001-am335x_evm-uEnv.txt-bootz-n-fixes.patch
kali@kali:~$ make ARCH=arm CROSS_COMPILE=${CC} distclean
kali@kali:~$ make ARCH=arm CROSS_COMPILE=${CC} am335x_evm_config
kali@kali:~$ make ARCH=arm CROSS_COMPILE=${CC}
kali@kali:~$ cd ../
```

--------------------------------

### List Patch Files in Debian Directory

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the contents of the `debian/patches/` directory, listing the patch files that have been created and are managed by the packaging system. This includes the patches for disabling requirements and version checks.

```bash
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ ls debian/patches/
disable-requirements-check.patch  disable-ver_check.patch  series
kali@kali:~/kali/packages/finalrecon$
```

--------------------------------

### Image Kali to microSD Card using dd

Source: https://www.kali.org/docs/arm/cubox

This command uses `xzcat` to decompress the Kali Linux image and pipes it to `dd` for writing to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card to avoid data loss. The `bs=4M` option sets the block size for faster transfer, and `status=progress` shows the transfer progress.

```bash
xzcat kali-linux-2025.4-cubox-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Add Copyright Information to debian/copyright

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows how to format and add copyright details for the FinalRecon package in the debian/copyright file. It specifies the copyright format, upstream information, and license details for different file sets.

```text
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: finalrecon
Upstream-Contact: thewhiteh4t <thewhiteh4t@protonmail.com>
Source: https://github.com/thewhiteh4t/FinalRecon

Files: *
Copyright: 2020 thewhiteh4t <thewhiteh4t@protonmail.com>
License: MIT

Files: debian/*
Copyright: 2020 Joseph O'Gorman <gamb1t@kali.org>
License: MIT

License: MIT
 Copyright (c) 2020 thewhiteh4t
 .
 Permission is hereby granted, free of charge, to any person obtaining a copy
 of this software and associated documentation files (the "Software"), to deal
 in the Software without restriction, including without limitation the rights
 to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 copies of the Software, and to permit persons to whom the Software is
 furnished to do so, subject to the following conditions:
 .
 The above copyright notice and this permission notice shall be included in all
 copies or substantial portions of the Software.
 .
 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 SOFTWARE.
```

--------------------------------

### Create Privileged Kali LXC Container on Kali Host

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Creates a privileged Kali Linux container using the `lxc-create` command with the `download` template. This process involves specifying the distribution, release, and architecture to download the appropriate Kali image.

```bash
kali@kali:~$ lxc-create -t download -n my-kali
```

--------------------------------

### Compress Kali VMDK for Upload

Source: https://www.kali.org/docs/cloud/digitalocean

Compresses a Kali Linux VMDK file using bzip2, preparing it for upload to cloud storage. This is a prerequisite for creating a custom image on platforms like DigitalOcean.

```bash
$ bzip2 kali.vmdk
```

--------------------------------

### Flash Kali Image to Storage using dd

Source: https://www.kali.org/docs/arm/chromebook-veyron

This command uses `xzcat` to decompress the Kali Linux image and pipes it to `dd` for writing to a specified storage device. Ensure you replace `/dev/sdX` with the correct device path to avoid data loss. The `bs=4M` option sets the block size for faster transfer, and `status=progress` shows the transfer status.

```bash
xzcat kali-linux-2025.4-chromebook-veyron-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Flash Kali Linux Image to microSD Card using dd

Source: https://www.kali.org/docs/arm/raspberry-pi-64-bit

This command uses `xzcat` to decompress the Kali Linux image and pipes it to `dd` for writing to a microSD card. It supports both 32-bit (armhf) and 64-bit (arm64) images. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss on your computer's hard drive. The `bs=4M` option sets the block size for faster writing, and `status=progress` shows the writing progress.

```bash
xzcat kali-linux-2025.4-raspberry-pi-armhf-xfce-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

```bash
xzcat kali-linux-2025.4-raspberry-pi-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Set Up SSH Authorized Keys for Mirror Trigger

Source: https://www.kali.org/docs/community/setting-up-a-kali-linux-mirror

Configures the SSH authorized keys for the mirror user to allow archive.kali.org to trigger mirror updates. This involves creating the .ssh directory, setting permissions, and adding the public key.

```bash
$ whoami
archvsync
$ mkdir -p ~/.ssh/
$ chmod 0700 ~/.ssh/
$ wget -O - -q https://archive.kali.org/pushmirror.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
```

--------------------------------

### Image Kali to microSD Card using dd

Source: https://www.kali.org/docs/arm/nanopi2

This command uses `xzcat` to decompress the Kali Linux image and pipes it to `dd` for writing to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card to avoid data loss. The `bs=4M` option sets the block size for faster transfer, and `status=progress` shows the transfer progress.

```bash
xzcat kali-linux-2025.4-nanopi2-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Imaging microSD Card with dd Utility

Source: https://www.kali.org/docs/arm/efikamx

This command uses the `dd` utility to write a Kali Linux image file to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss. The `conv=fsync` option ensures data is physically written before the command exits, and `bs=4M` sets the block size for faster transfer.

```bash
dd if=kali-linux-2025.4-efikamx.img of=/dev/sdX conv=fsync bs=4M
```

--------------------------------

### Run Kaboxer Application (CLI)

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Command to run a Kaboxer application within its container. This command may encounter permission errors if required directories are not accessible or mounted correctly.

```bash
kali@kali:~$ kaboxer run hello-cli

```

--------------------------------

### Copy and Configure Kali Root Filesystem

Source: https://www.kali.org/docs/development/custom-raspberry-pi-image

Copies the pre-built Kali ARM root filesystem into the mounted root partition of the image file using rsync. It also sets up a basic DNS resolver configuration.

```bash
kali@kali:~$ rsync -HPavz /root/arm-stuff/rootfs/kali-armel/ root
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf

```

--------------------------------

### Configure Kaboxer Docker Image Registry

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This snippet shows the configuration within `kaboxer.yaml` to specify the Docker registry URL and image name for retrieving the container image.

```yaml
kali@kali:~$ cat kaboxer.yaml
[...]
container:
  type: docker
  origin:
    registry:
      url: https://registry.gitlab.com
      image: kalilinux/packages/hello-kbx/hello

```

--------------------------------

### Update and Check WSL Status (CLI)

Source: https://www.kali.org/docs/wsl/wsl-preparations

These commands interact with the Windows Subsystem for Linux (WSL) command-line interface. `wsl --update` attempts to update the WSL kernel and components, while `wsl --status` and `wsl --version` provide information about the current WSL configuration and version, helping to diagnose operational issues.

```bash
wsl --update
wsl --status
wsl --version
```

--------------------------------

### Configure Kali Menu Categories in kaboxer.yaml

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This snippet shows how to add categories to a Kaboxer application's desktop file by modifying the `kaboxer.yaml` configuration. The `categories` field under `application` allows specifying multiple categories, separated by semicolons, which helps in organizing applications within the Kali menu.

```yaml
application:
  [...] 
  categories: Utility;06-02-bluetooth-tools;06-wireless-attacks

```

--------------------------------

### Extract and Prepare Mali Driver Source (Shell)

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Extracts the Mali driver source code archives and navigates into the X11 driver directory. This prepares the source code for compilation.

```shell
kali@kali:~$ tar -xzvf DX910-SW-99003-r3p2-01rel0.tgz
kali@kali:~$ tar -xzvf DX910-SW-99006-r3p2-01rel0.tgz
kali@kali:~$ cd DX910-SW-99003-r3p2-01rel0/x11/xf86-video-mali-0.0.1/
kali@kali:~$ ./autogen.sh
kali@kali:~$ chmod +x configure
kali@kali:~$
```

--------------------------------

### Configure Debian Control File for Kaboxer Integration

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This snippet shows how to modify the debian/control file to include 'kaboxer' in Build-Depends and ensure `${misc:Depends}` is present for proper dependency injection by `dh_kaboxer`.

```bash
kali@kali:~$ cat debian/control
Source: hello-kbx
[...]
Build-Depends: debhelper-compat (= 13), kaboxer
[...]

Package: hello-cli-kbx
Architecture: all
Depends: ${misc:Depends}
[...]
```

--------------------------------

### Add CAN-ISOTP Driver Submodule to Kernel Sources

Source: https://www.kali.org/docs/nethunter/nethunter-kernel-9-config-8

This snippet shows how to integrate the CAN-ISOTP driver into the Linux kernel. It involves adding the driver as a Git submodule, downloading a necessary header file, and updating the kernel's Kconfig and Makefile to recognize the new driver.

```bash
git submodule add https://github.com/V0lk3n/can-isotp drivers/net/can/can-isotp

cd include/uapi/linux/can
wget https://raw.githubusercontent.com/v0lk3n/can-isotp/refs/heads/master/include/uapi/linux/can/isotp.h

# Edit drivers/net/can/Kconfig and add:
source "drivers/net/can/can-isotp/Kconfig"

# Edit drivers/net/can/Makefile and add:
obj-y += can-isotp/
```

--------------------------------

### Format Partition with LUKS Encryption (Older LUKS)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This command formats the second partition of the specified device (/dev/sdX2) with LUKS encryption using AES-CBC-ESSIV with a 256-bit key, but utilizes PBKDF2 for key derivation. This is suitable for older systems or when compatibility with older LUKS versions is required.

```bash
sudo cryptsetup -v -y --pbkdf pbkdf2 --cipher aes-cbc-essiv:sha256 --key-size 256 luksFormat /dev/sdX2
```

--------------------------------

### Build Kali Linux Image for BeagleBone Black

Source: https://www.kali.org/docs/arm/beaglebone-black

This script is used to generate a Kali Linux image file for the BeagleBone Black. It requires cloning the Kali-ARM Build-Scripts repository and executing the 'beaglebone-black.sh' script within a Kali Linux environment. The output is an '.xz' compressed image file.

```bash
# Clone the repository
git clone https://gitlab.com/kalilinux/build-scripts/kali-arm.git
cd kali-arm

# Execute the build script (ensure you are in a Kali Linux environment)
./beaglebone-black.sh
```

--------------------------------

### Configure and Manage CAN Interfaces

Source: https://www.kali.org/docs/nethunter/nethunter-carsenal

This section details how to set up and manage CAN interfaces for CARsenal. It includes commands for creating virtual CAN interfaces, setting MTU and txqueuelen values, and bringing the interface online. These commands are essential for establishing communication over the CAN bus.

```bash
# For VCAN Type : create interface first
sudo ip link add dev <caniface> type vcan

# If MTU or txqueuelen value specified
sudo ip link set <caniface> mtu <Value>
sudo ip link set <caniface> txqueuelen <Value>

# Brought UP interface
sudo ip link set <caniface> up
```

--------------------------------

### Image Kali Linux to microSD Card using dd

Source: https://www.kali.org/docs/arm/banana-pi

This command uses `xzcat` to decompress the Kali Linux image and pipes it to `dd` to write it to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card to avoid data loss. The `bs=4M` option sets the block size for faster writing, and `status=progress` shows the transfer progress.

```bash
xzcat images/kali-linux-2025.4-banana-pi-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Managing Service Allowlists and Blocklists (Kali Linux)

Source: https://www.kali.org/docs/policy/kali-linux-network-service-policy

Illustrates how to view and manage the service allowlists and blocklists within the `/usr/sbin/update-rc.d` file. This file determines which services are permitted or denied automatic startup at boot time.

```bash
kali@kali:~$ tail -95 /usr/sbin/update-rc.d | more
[...]
__DATA__
#
# List of blocklisted init scripts
#
apache2 disabled
avahi-daemon disabled
bluetooth disabled
cups disabled
dictd disabled
ssh disabled
[...]
#
# List of allowlisted init scripts
#
acpid enabled
acpi-fakekey enabled
acpi-support enabled
alsa-utils enabled
anacron enabled
[...]


```

--------------------------------

### Check Device Bootloader Status with Fastboot

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This Fastboot command queries the device to display information about its bootloader status, including whether it is locked or unlocked, and if tampering has occurred. This helps determine if an unlock operation is necessary.

```bash
kali@kali:~$ fastboot oem device-info
(bootloader)     Device tampered: false
(bootloader)     Device unlocked: false
(bootloader)     Charger screen enabled: false
(bootloader)     Display panel:
OKAY [  0.005s]
Finished. Total time: 0.005s

kali@kali:~

```

--------------------------------

### Build Kali Linux Image for Radxa Zero (sdcard)

Source: https://www.kali.org/docs/arm/radxa-zero-sdcard

This script is used to generate a Kali Linux image for the Radxa Zero when using an SD card. It requires cloning the Kali-ARM Build-Scripts repository and executing the 'radxa-zero-sdcard.sh' script. The output is an 'img.xz' file.

```bash
# Example command (actual script execution not shown)
./radxa-zero-sdcard.sh
```

--------------------------------

### Switch Kali back to Command-Line Interface (CLI)

Source: https://www.kali.org/docs/arm/raspberry-pi-zero-2-w

This command sequence reverts the Kali Linux system on the Raspberry Pi Zero 2 W back to the command-line interface (CLI) from the graphical desktop. It uses `systemctl` to set the default target to multi-user and then reboots the system. This is recommended to conserve resources on the Raspberry Pi Zero 2 W.

```bash
kali@kali:~$ sudo systemctl set-default multi-user
kali@kali:~$ sudo reboot
```

--------------------------------

### Create and Execute Cleanup Script for Kali ARM Rootfs

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Creates a 'cleanup' script to remove cached files and perform other cleanup tasks within the chroot environment. It then makes the script executable, runs it, and finally unmounts the previously mounted directories.

```shell
kali@kali:~$ cat <<EOF > kali-$architecture/cleanup
#!/bin/sh
rm -rf /root/.bash_history
apt-get update
apt-get clean
rm -f cleanup
EOF
kali@kali:~$ 
kali@kali:~$ chmod +x kali-$architecture/cleanup
kali@kali:~$ LANG=C chroot kali-$architecture /cleanup
kali@kali:~$ 
kali@kali:~$ umount kali-$architecture/proc
kali@kali:~$ umount kali-$architecture/dev/pts
kali@kali:~$ umount kali-$architecture/dev/
kali@kali:~$ 
kali@kali:~$ cd ../
```

--------------------------------

### Configure LXC for Unprivileged Containers (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Sets up LXC to run containers in an unprivileged user context. This involves configuring user namespaces, network interfaces, and AppArmor profiles for enhanced security. It modifies system configuration files and user-specific LXC settings.

```bash
kali@kali:~$ echo "$USER veth virbr0 10" | sudo tee -i /etc/lxc/lxc-usernet
kali@kali:~$ sudo sh -c 'echo "kernel.unprivileged_userns_clone=1" > /etc/sysctl.d/80-lxc-userns.conf'
kali@kali:~$ sudo sysctl kernel.unprivileged_userns_clone=1
kali@kali:~$ sudo chmod u+s /usr/libexec/lxc/lxc-user-nic
kali@kali:~$ 
kali@kali:~$ mkdir -p ~/.config/lxc
kali@kali:~$ cp /etc/lxc/default.conf ~/.config/lxc/default.conf
kali@kali:~$ sed -i 's/lxc.apparmor.profile = generated/lxc.apparmor.profile = unconfined/g' ~/.config/lxc/default.conf

```

```bash
kali@kali:~$ echo lxc.idmap = u 0 100000 65536 >> ~/.config/lxc/default.conf
kali@kali:~$ echo lxc.idmap = g 0 100000 65536 >> ~/.config/lxc/default.conf

```

--------------------------------

### Open Encrypted LUKS Partition

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This command opens the LUKS-encrypted partition, making it accessible as a device mapper entry (e.g., `/dev/mapper/my_usb`). You will be prompted to enter the passphrase created during the `luksFormat` step. This is a prerequisite for creating a filesystem on the encrypted partition.

```bash
kali@kali:~$ sudo cryptsetup luksOpen /dev/sdX3 my_usb
Enter passphrase for /dev/sdX3:
kali@kali:~$ 

```

--------------------------------

### Manually Change Wi-Fi Channels

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

Demonstrates how to manually switch Wi-Fi channels using the nexutil command in an Android terminal. This is useful when the Hijacker app doesn't automatically select the desired channels.

```shell
nexutil -k36/80
nexutil -k40/80
```

--------------------------------

### Partition and Format Beaglebone Black Image File

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Partitions the created image file using 'parted' and 'fdisk' to create a boot partition (64MB, FAT32) and a root partition (ext4). It then mounts these partitions for further use.

```bash
kali@kali:~$ parted --script kali-custom-bbb.img mklabel msdos
kali@kali:~$ fdisk kali-custom-bbb.img <<EOF
n
p
1

+64M
t
e
p
w
EOF
kali@kali:~$ parted --script kali-custom-bbb.img set 1 boot on
kali@kali:~$ fdisk kali-custom-bbb.img <<EOF
n
p
2

w
EOF


```

```bash
kali@kali:~$ loopdevice=`losetup -f --show kali-custom-bbb.img`
kali@kali:~$ device=`kpartx -va $loopdevice| sed -E 's/.*(loop[0-9])p.*/1/g' | head -1`
kali@kali:~$ device="/dev/mapper/${device}"
kali@kali:~$ bootp=${device}p1
kali@kali:~$ rootp=${device}p2
kali@kali:~

kali@kali:~$ mkfs.vfat -F 16 $bootp -n boot
kali@kali:~$ mkfs.ext4 $rootp -L kaliroot
kali@kali:~$ mkdir -p boot
kali@kali:~$ mkdir -p root
kali@kali:~$ mount $bootp boot
kali@kali:~$ mount $rootp root


```

--------------------------------

### Restore Data to Encrypted Kali Partition

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Commands to open a LUKS encrypted device, format it, mount it, and restore data using rsync. This process assumes the partition is already encrypted and a backup exists.

```bash
$ sudo cryptsetup -v luksOpen /dev/sdX2 crypt
$ sudo mkfs.ext4 /dev/mapper/crypt
$ sudo mount /dev/mapper/crypt /mnt/encrypted/
$ sudo rsync -avh /mnt/backup/* /mnt/encrypted/
$ sync

```

--------------------------------

### Update APT Package Lists

Source: https://www.kali.org/docs/troubleshooting/handling-common-apt-errors

Ensures APT has the latest information about available packages and their versions. This is a prerequisite for most package management operations and can resolve many unexpected issues.

```bash
kali@kali:~$ sudo apt update
Get:1 http://http.kali.org/kali kali-rolling InRelease [41.2 kB]
[...]
```

--------------------------------

### Copy Kali Rootfs and Configure Network

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Copies the pre-built Kali ARM root filesystem to the mounted root partition of the Beaglebone Black image. It also configures the DNS resolver by adding Google's public DNS server.

```bash
kali@kali:~$ rsync -HPavz /root/arm-stuff/rootfs/kali-armhf/ root
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf


```

--------------------------------

### Flash Kali Linux Image to SD Card using dd

Source: https://www.kali.org/docs/arm/radxa-zero-sdcard

This command uses the 'dd' utility to write a compressed Kali Linux image file to a microSD card. It's crucial to replace '/dev/sdX' with the correct device path for your SD card to avoid data loss. The 'xzcat' command decompresses the image on the fly.

```bash
xzcat kali-linux-2025.4-radxa-zero-sdcard-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Build Docker Image and Store in Debian Package

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

This configuration sets the `DH_KABOXER_BUILD_STRATEGY` environment variable in debian/rules to 'tarball', instructing the build system to build the Docker image and include it within the Debian package.

```makefile
kali@kali:~$ cat debian/rules
#!/usr/bin/make -f

export DH_KABOXER_BUILD_STRATEGY=tarball

%:
	dh $@ --with=kaboxer --buildsystem=kaboxer

```

--------------------------------

### Partition and Format Image File

Source: https://www.kali.org/docs/development/custom-efikamx-image

Uses the parted utility to create a new MS-DOS partition table on the image file and then defines two primary partitions: one for boot and another for the root filesystem. It then formats these partitions using ext2 and ext4 respectively and mounts them.

```bash
kali@kali:~$ parted kali-custom-efikamx.img --script -- mklabel msdos
kali@kali:~$ parted kali-custom-efikamx.img --script -- mkpart primary ext2 4096s 266239s
kali@kali:~$ parted kali-custom-efikamx.img --script -- mkpart primary ext4 266240s 100%

```

```bash
kali@kali:~$ loopdevice=$( losetup -f --show kali-custom-efikamx.img )
kali@kali:~$ device=$( kpartx -va $loopdevice| sed -E 's/.*(loop[0-9])p.*/\1/g' | head -1 )
kali@kali:~$ device="/dev/mapper/${device}"
kali@kali:~$ bootp=${device}p1
kali@kali:~$ rootp=${device}p2
kali@kali:~
kali@kali:~$ mkfs.ext2 $bootp
kali@kali:~$ mkfs.ext4 $rootp
kali@kali:~$ mkdir -p boot
kali@kali:~$ mkdir -p root
kali@kali:~$ mount $bootp boot
kali@kali:~$ mount $rootp root

```

--------------------------------

### Configure Static IP with DHCP and Post-Up Script (Bash)

Source: https://www.kali.org/docs/arm/raspberry-pi-zero-w-pi-tail

This snippet shows how to modify the network interfaces file to use DHCP and execute a script after the network is up. The script, `change_ip.sh`, dynamically assigns an IP address with the last octet set to 200, ensuring a predictable IP for the device. This is useful when the DHCP server might assign different IPs after reboots.

```bash
#!/bin/bash

# Get the current DHCP-assigned IP address and gateway
IP_ADDRESS=$(ip -4 -o addr show wlan0 | awk '{print $4}')
GATEWAY=$(ip route | awk '/default via/ {print $3}')

# Extract the first three octets
BASE_IP=$(echo $IP_ADDRESS | cut -d'.' -f1-3)

# Assign the new IP address with the last octet set to 200
NEW_IP="$BASE_IP.200"

# Modify the IP address while preserving other DHCP configuration
ifconfig wlan0 $NEW_IP netmask 255.255.255.0 up
route add default gw $GATEWAY

```

--------------------------------

### Replay CAN Log Files with canplayer

Source: https://www.kali.org/docs/nethunter/nethunter-carsenal

Demonstrates the use of 'canplayer' from the can-utils suite to replay logged CAN traffic. This functionality is critical for re-simulating specific scenarios, testing responses to recorded events, and analyzing past bus activity.

```bash
# Example usage of canplayer (assuming can0 is up and logfile.log exists)
canplayer can0 -i logfile.log
```

--------------------------------

### Copy and Modify Kali Root Filesystem

Source: https://www.kali.org/docs/development/custom-efikamx-image

Copies the pre-built Kali root filesystem into the mounted root partition of the image file using rsync. It then sets up a nameserver configuration and modifies the udev init script.

```bash
kali@kali:~$ rsync -HPavz /root/arm-stuff/rootfs/kali-armhf/ root
kali@kali:~$ echo nameserver 8.8.8.8 > root/etc/resolv.conf
kali@kali:~$ sed 's/0-1/0//g' root/etc/init.d/udev

```

--------------------------------

### Unlock the Device Bootloader with Fastboot

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This Fastboot command initiates the process of unlocking the device's bootloader. Unlocking the bootloader grants write access to partitions, enabling the flashing of custom ROMs and other modifications. This action may wipe user data on the device.

```bash
kali@kali:~$ fastboot oem unlock
OKAY [  0.022s]
Finished. Total time: 0.022s

kali@kali:~

```

--------------------------------

### Flash Kali Image to microSD Card using dd

Source: https://www.kali.org/docs/arm/nanopc-t

This command flashes a compressed Kali Linux image to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card to avoid data loss. The `status=progress` flag provides real-time feedback on the operation.

```shell
xzcat kali-linux-2025.4-nanopc-t-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Image Flashing with dd Utility

Source: https://www.kali.org/docs/arm/ss808-mk808

This command uses the `dd` utility to write a Kali Linux image file to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card, as an incorrect path can lead to data loss on other drives. The `conv=fsync` option ensures data is physically written before the command completes, and `bs=4M` sets the block size for faster transfer.

```bash
dd if=kali-linux-2025.4-SS808.img of=/dev/sdX conv=fsync bs=4M
```

--------------------------------

### Partition and Format Image File

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Uses parted to create a new MS-DOS partition table and a primary ext4 partition on the image file. It then sets up a loop device, maps partitions using kpartx, and formats the partition with ext4.

```bash
kali@kali:~$ parted kali-custom-ss808.img --script -- mklabel msdos
kali@kali:~$ parted kali-custom-ss808.img --script -- mkpart primary ext4 1 -1

```

```bash
kali@kali:~$ loopdevice=`losetup -f --show kali-custom-ss808.img`
kali@kali:~$ device=`kpartx -va $loopdevice| sed -E 's/.*(loop[0-9])p.*/1/g' | head -1`
kali@kali:~$ device="/dev/mapper/${device}"
kali@kali:~$ rootp=${device}p1
kali@kali:~
kali@kali:~$ mkfs.ext4 $rootp
kali@kali:~$ mkdir -p root/
kali@kali:~$ mount $rootp root

```

--------------------------------

### Image Kali ISO to USB Drive

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This command copies the Kali Linux ISO image to the specified USB drive. Ensure you replace '/dev/sdX' with your actual USB device. The `conv=fsync` option ensures data is physically written before the command exits.

```bash
kali@kali:~$ sudo dd if=kali-linux-2025.4-live-amd64.iso of=/dev/sdX conv=fsync bs=4M

```

--------------------------------

### Inspect USB Partition Structure

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This command displays the current partition table of the USB drive. It helps to identify existing partitions and available space for creating a new one. The output shows partition numbers, sizes, types, and file systems.

```bash
kali@kali:~$ sudo parted /dev/sdX print
Model: SanDisk Extreme (scsi)
Disk /dev/sdX: 62.7GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      32.8kB  4927MB  4927MB  primary               boot, hidden
 2      4927MB  4932MB  4194kB  primary

kali@kali:~$ 

```

--------------------------------

### Append SSH Public Key to Authorized Keys (Bash)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This command appends an SSH public key (`id_rsa.pub`) to the Dropbear `authorized_keys` file, enabling key-based authentication for remote unlocking. It then removes the public key file from the system. Ensure the public key is correctly formatted and appended with a space after the command.

```bash
cat id_rsa.pub >> /etc/dropbear/initramfs/authorized_keys && rm -v id_rsa.pub

```

--------------------------------

### Download and Image Kali Linux to RPi SD Card

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Downloads the latest Kali Linux 64-bit image for Raspberry Pi and writes it to an SD card using `dd`. Ensure you replace `/dev/sdX` with the correct device identifier for your SD card to avoid data loss.

```bash
wget https://kali.download/arm-images/kali-2025.4/kali-linux-2025.4-raspberry-pi-arm64.img.xz
xzcat kali-linux-2025.4-raspberry-pi-arm64.img.xz | sudo dd of=/dev/sdX bs=512k status=progress

```

--------------------------------

### Configure Python Build with PyBuild and DH

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This snippet configures the debian/rules file for a Python application. It specifies the use of 'dh' with the 'python3' build system and 'pybuild', and sets the PYBUILD_NAME environment variable. This is essential for correctly building Python packages that have a setup.py file.

```makefile
#!/usr/bin/make -f

export PYBUILD_NAME = instaloader

%:
	dh $@ --with python3 --buildsystem=pybuild

```

--------------------------------

### Benchmark Hashcat Performance

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

Runs Hashcat's built-in benchmark test to measure the performance of different hashing algorithms on the configured hardware. This helps in understanding the cracking speed for various hash types.

```bash
kali@kali:~$ hashcat -b | uniq
hashcat (v6.0.0) starting in benchmark mode...

Benchmarking uses hand-optimized kernel code by default.
You can use it in your cracking session by setting the -O option.
Note: Using optimized kernel code limits the maximum supported password length.
To disable the optimized kernel code in benchmark mode, use the -w option.

* Device #1: WARNING! Kernel exec timeout is not disabled.
             This may cause "CL_OUT_OF_RESOURCES" or related errors.
             To disable the timeout, see: https://hashcat.net/q/timeoutpatch
* Device #2: WARNING! Kernel exec timeout is not disabled.
             This may cause "CL_OUT_OF_RESOURCES" or related errors.
             To disable the timeout, see: https://hashcat.net/q/timeoutpatch
CUDA API (CUDA 10.2)
====================
* Device #1: GeForce GTX 1060 6GB, 5908/6075 MB, 10MCU

OpenCL API (OpenCL 1.2 CUDA 10.2.185) - Platform #1 [NVIDIA Corporation]
========================================================================
* Device #2: GeForce GTX 1060 6GB, skipped

Benchmark relevant options:
===========================
* --optimized-kernel-enable

Hashmode: 0 - MD5
Speed.#1.........: 14350.4 MH/s (46.67ms) @ Accel:64 Loops:1024 Thr:1024 Vec:8

Hashmode: 100 - SHA1
Speed.#1.........:  4800.5 MH/s (69.83ms) @ Accel:32 Loops:1024 Thr:1024 Vec:1
[...]
Started: Tue Jul 21 17:12:39 2020
Stopped: Tue Jul 21 17:16:10 2020
kali@kali:~$
```

--------------------------------

### Copy Firmware and Kernel Image to Boot Partition

Source: https://www.kali.org/docs/development/custom-raspberry-pi-image

Clones the Raspberry Pi firmware repository, copies its boot files to the image's boot partition, and replaces the default kernel image with the newly compiled one. It also sets the kernel command line arguments.

```bash
kali@kali:~$ cd ~/arm-stuff/images/
kali@kali:~$ git clone git://github.com/raspberrypi/firmware.git rpi-firmware
kali@kali:~$ cp -rf rpi-firmware/boot/* boot/
kali@kali:~$ rm -rf rpi-firmware
kali@kali:~
kali@kali:~$ cp ~/arm-stuff/kernel/tools/mkimage/kernel.img boot/
kali@kali:~$ echo "dwc_otg.lpm_enable=0 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 rootwait" > boot/cmdline.txt

```

--------------------------------

### Configure Authorized Keys for SSH Unlock Command (Bash)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This configuration adds a command to the `authorized_keys` file for Dropbear. When an SSH connection is made with a matching key, it will execute the specified `/etc/unlock.sh` script and then exit. This allows for remote unlocking of encrypted drives.

```bash
command="/etc/unlock.sh; exit"

```

--------------------------------

### Flash Magisk for Root Access using ADB Sideload

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This command flashes the Magisk zip file to gain root access on the Android device via ADB sideload. It's crucial to use the specified version (28.1) to avoid compatibility issues with Kali Nethunter.

```bash
adb -d sideload Magisk-v28.1.zip
```

--------------------------------

### Download Package Source (Bash)

Source: https://www.kali.org/docs/development/rebuilding-a-package-from-source

This snippet demonstrates how to download the source code for a specific package using apt. It first updates the package list and then fetches the source for 'libfreefare'. Finally, it changes the directory into the extracted source folder.

```bash
kali@kali:~$ # Get the source package
kali@kali:~$ sudo apt update
kali@kali:~$ apt source libfreefare
kali@kali:~$ cd libfreefare-0.4.0/
```

--------------------------------

### Clone Kali CDImage Git Repository

Source: https://www.kali.org/docs/development/generate-updated-kali-iso

Clones the Kali 'cdimage' Git repository, which contains the live-build configuration scripts. This command fetches the latest build scripts from the specified GitLab repository.

```bash
kali@kali:~$ git clone git://gitlab.com/kalilinux/build-scripts/live-build-config.git

```

--------------------------------

### Apply Wireless Injection Patches to Kernel

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This snippet downloads two patch files for wireless injection and then applies them to the kernel source code using the 'patch' command. It first creates a directory for patches and then uses wget to download the patch files.

```bash
kali@kali:~$ mkdir -p ../patches/
kali@kali:~$ wget http://patches.aircrack-ng.org/mac80211.compat08082009.wl_frag+ack_v1.patch -O ../patches/mac80211.patch
kali@kali:~$ wget http://patches.aircrack-ng.org/channel-negative-one-maxim.patch -O ../patches/negative.patch
kali@kali:~$ patch -p1 < ../patches/negative.patch
kali@kali:~$ patch -p1 < ../patches/mac80211.patch
```

--------------------------------

### Image Kali Linux to microSD Card using dd

Source: https://www.kali.org/docs/arm/odroid-xu3

This command streams a compressed Kali Linux image file and pipes it to the `dd` utility for writing to a specified storage device. Ensure you replace `/dev/sdX` with the correct device path to avoid data loss. The `status=progress` flag provides real-time feedback on the transfer.

```bash
xzcat images/kali-linux-2025.4-odroid-xu3-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Image Kali Linux to microSD using dd

Source: https://www.kali.org/docs/arm/usb-armory-mki

This command uses 'xzcat' to decompress the Kali Linux image and 'dd' to write it to a microSD card. Ensure you replace '/dev/sdX' with the correct device path for your microSD card. This process will erase all data on the target device.

```bash
xzcat kali-linux-2025.4-usb-armory-mki-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Fix Audio in Kali GUI Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Configures PulseAudio server settings for both root and the 'kali' user within the container to enable audio playback. This involves setting environment variables and modifying the client configuration, followed by a container restart.

```bash
kali@kali:~$ lxc exec my-kali -- sh -c "echo 'export PULSE_SERVER=unix:/tmp/.pulse-native' | tee --append /root/.profile"
kali@kali:~$ lxc exec my-kali -- sh -c "echo 'export PULSE_SERVER=unix:/tmp/.pulse-native' | tee --append /home/kali/.profile"
kali@kali:~$ lxc exec my-kali -- sh -c "echo 'default-server = unix:/tmp/.pulse-native' | tee --append /etc/pulse/client.conf"
kali@kali:~$ lxc restart my-kali
```

--------------------------------

### Image Kali Linux to SD Card using dd

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Uses the `dd` command to write a Kali Linux image file to an SD card. It's crucial to replace `/dev/sdX` with the correct device identifier for the SD card to avoid data loss.

```bash
kali@kali:~$ dd if=kali-linux-bbb.img of=/dev/sdX conv=fsync bs=4M
```

--------------------------------

### Create Non-Root User in Container (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Creates a new user within the 'my-kali' LXC container and adds them to the 'sudo' group. Replace '<username>' with the desired username. This allows for user-specific operations within the container.

```bash
kali@kali:~$ lxc-attach -n my-kali --clear-env adduser <username>
kali@kali:~$ lxc-attach -n my-kali --clear-env adduser <username> sudo

```

--------------------------------

### Format Partition with LUKS Encryption (RPi4 4GB+)

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

This command formats the second partition of the specified device (/dev/sdX2) with LUKS encryption using AES-CBC-ESSIV with a 256-bit key. This is the recommended command for Raspberry Pi 4 devices with 4GB or more RAM.

```bash
sudo cryptsetup -v -y --cipher aes-cbc-essiv:sha256 --key-size 256 luksFormat /dev/sdX2
```

--------------------------------

### Copy Existing SSH Public Key

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Copies an existing SSH public key (id_rsa.pub) from the user's home directory to the chroot environment. This key can then be used by Dropbear.

```bash
$ sudo cp ~/.ssh/id_rsa.pub /mnt/chroot/
```

--------------------------------

### Halt Kali Linux VM with Vagrant

Source: https://www.kali.org/docs/virtualization/install-vagrant-guest-vm

This command gracefully shuts down the running Kali Linux virtual machine managed by Vagrant. It ensures that the VM is stopped cleanly, preventing data corruption. This is a standard command for managing the lifecycle of Vagrant-managed environments.

```bash
kali@kali:~/vagrant$ vagrant halt
==> default: Attempting graceful shutdown of VM...

kali@kali:~/vagrant$

```

--------------------------------

### Configure Win-KeX ESM Mode in Windows Terminal

Source: https://www.kali.org/docs/wsl/win-kex

This configuration sets up a basic Windows Terminal profile for Win-KeX in Enhanced Session Mode (ESM) with sound enabled. It utilizes the '--esm' flag for this mode and specifies the command for WSL and Kali Linux.

```json
{
      "guid": "{55ca431a-3a87-5fb3-83cd-11ecedc031d2}",
      "hidden": false,
      "name": "Win-KeX",
      "commandline": "wsl -d kali-linux kex --esm --wtstart -s"
}
```

--------------------------------

### Configure Kali Linux Kernel from Existing Config

Source: https://www.kali.org/docs/development/recompiling-the-kali-linux-kernel

Copies the configuration file of the currently running kernel to be used as the base for the new kernel compilation. This helps maintain existing settings while allowing for modifications.

```bash
kali@kali:~/kernel$ cp /boot/config-4.9.0-kali1-amd64 ~/kernel/linux-source-4.9/.config

```

--------------------------------

### Flash Kali Linux Image to microSD Card (Raspberry Pi 4)

Source: https://www.kali.org/docs/arm/raspberry-pi-4

This command uses `xzcat` to decompress the Kali Linux image and `dd` to write it to a microSD card. Ensure you replace `/dev/sdX` with the correct device path for your microSD card. This process will erase all data on the card.

```bash
xzcat kali-linux-2025.4-raspberry-pi-armhf.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

```bash
xzcat kali-linux-2025.4-raspberry-pi-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Configure Kernel Command Line for Encrypted Root

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Modifies the `/boot/cmdline.txt` file to specify the encrypted root filesystem. It changes the root path to `/dev/mapper/crypt` and adds `cryptdevice=PARTUUID=<partuuid>:crypt` to inform the kernel about the encrypted device during boot.

```bash
vim /boot/cmdline.txt
cat /boot/cmdline.txt

```

```text
dwc_otg.fiq_fix_enable=2 console=serial0,115200 kgdboc=serial0,115200 console=tty1 root=/dev/mapper/crypt cryptdevice=PARTUUID=ed889dad-02:crypt rootfstype=ext4 fsck.repair=yes rootwait net.ifnames=0

```

--------------------------------

### Enable Cross-Compilation for ARM

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Sets environment variables ARCH and CROSS_COMPILE to enable Linaro cross-compilation for ARM architecture. These variables must be set at the beginning of each session.

```bash
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/gcc-arm-eabi-linaro-4.6.2/bin/arm-eabi-

```

--------------------------------

### Configure and Build CuBox Kernel

Source: https://www.kali.org/docs/development/custom-cubox-image

Sets the ARCH environment variable to 'arm' and defines the CROSS_COMPILE path for ARM cross-compilation. It then uses 'cubox_defconfig' to configure the kernel build specifically for the CuBox architecture. This prepares the kernel for compilation.

```bash
kali@kali:~$ export ARCH=arm
kali@kali:~$ export CROSS_COMPILE=~/arm-stuff/kernel/toolchains/arm-eabi-linaro-4.6.2/bin/arm-eabi-
kali@kali:~$ make cubox_defconfig

```

--------------------------------

### Login to Kali LXD Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Connects to the console of the 'my-kali' LXD container as the user 'kali'. This allows interactive use of the Kali Linux environment within the container.

```bash
kali@kali:~$ lxc console my-kali

```

--------------------------------

### Prepare Root User for SSH Key Access

Source: https://www.kali.org/docs/cloud/digitalocean

Disables the root password login and creates the necessary .ssh directory for the root user. This is a security measure required by DigitalOcean for custom images, enforcing SSH key authentication.

```bash
kali@kali:~$ passwd -d root
kali@kali:~$ mkdir -p /root/.ssh/
```

--------------------------------

### Configure SSH Local Keyfile

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Sets the path to the local SSH private key file. The corresponding public key will be added to the system's root authorized keys for remote access.

```bash
export _SSH_LOCAL_KEYFILE="$_USER_HOME/.ssh/id_rsa"
```

--------------------------------

### Login to Kali LXC Container (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Connects to the console of the LXC container named 'my-kali'. This allows interactive access to the container's command line.

```bash
kali@kali:~$ lxc-console

```

--------------------------------

### Commit Changes to Git Repository

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet demonstrates the standard Git commands used to stage and commit code modifications. It shows adding the modified `finalrecon.py` file and committing it with a descriptive message.

```bash
kali@kali:~/kali/packages/finalrecon$ vim finalrecon.py
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ git add finalrecon.py
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ git commit -m "disable requirements check"
[...]
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ vim finalrecon.py
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ git add finalrecon.py
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ git commit -m "disable ver_check"
[...]
kali@kali:~/kali/packages/finalrecon$
```

--------------------------------

### Determine Kali Linux Download Mirror with curl

Source: https://www.kali.org/docs/troubleshooting/download-speed-issues

This command uses `curl` to initiate a download request and displays the HTTP headers, including the 'Location' header which indicates the mirror server you are being redirected to. This helps in identifying the specific mirror serving your download.

```bash
kali@kali:~$ curl -i https://cdimage.kali.org/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
HTTP/1.1 302 Found
Server: nginx
Content-Type: text/html; charset=utf-8
Content-Length: 0
Connection: keep-alive
Cache-Control: private, no-cache
Link: <https://kali.download/base-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso>; rel=duplicate; pri=1; geo=ae
Link: <https://ask4.mm.fcix.net/kali-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso>; rel=duplicate; pri=2; geo=gb
Link: <https://ftp.hands.com/kali-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso>; rel=duplicate; pri=3; geo=gb
Location: https://mirror.vinehost.net/kali-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso

kali@kali:~$
```

--------------------------------

### Create Patch File for Requirements Check

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet displays the content of a patch file (`disable-requirements-check.patch`) generated after modifying `finalrecon.py`. It details the changes made, specifically commenting out the dependency checking code block.

```diff
From: Joseph O'Gorman <gamb1t@kali.org>
Subject: disable requirements check

---
 finalrecon.py | 32 ++++++++++++++++----------------
 1 file changed, 16 insertions(+), 16 deletions(-)

diff --git a/finalrecon.py b/finalrecon.py
index 735f40b..95e99f1 100644
--- a/finalrecon.py
+++ b/finalrecon.py
@@ -26,22 +26,22 @@ else:

 path_to_script = os.path.dirname(os.path.realpath(__file__))

-#with open(path_to_script + '/requirements.txt', 'r') as rqr:
-#      pkg_list = rqr.read().strip().split('\n')
-#
-#print('\n' + G + '[+]' + C + ' Checking Dependencies...' + W + '\n')
-#
-#for pkg in pkg_list:
-#      spec = importlib.util.find_spec(pkg)
-#      if spec is None:
-#              print(R + '[-]' + W + ' {}'.format(pkg) + C + ' is not Installed!' + W)
-#              fail = True
-#      else:
-#              pass
-#if fail == True:
-#      print('\n' + R + '[-]' + C + ' Please Execute ' + W + 'pip3 install -r requirements.txt' + C + ' to Install Missing Packages' + W + '\n')
-#      os.remove(pid_path)
-#      sys.exit()
+#with open(path_to_script + '/requirements.txt', 'r') as rqr:
+#      pkg_list = rqr.read().strip().split('\n')
+#
+#print('\n' + G + '[+]' + C + ' Checking Dependencies...' + W + '\n')
+#
+#for pkg in pkg_list:
+#      spec = importlib.util.find_spec(pkg)
+#      if spec is None:
+#              print(R + '[-]' + W + ' {}'.format(pkg) + C + ' is not Installed!' + W)
+#              fail = True
+#      else:
+#              pass
+#if fail == True:
+#      print('\n' + R + '[-]' + C + ' Please Execute ' + W + 'pip3 install -r requirements.txt' + C + ' to Install Missing Packages' + W + '\n')
+#      os.remove(pid_path)
+#      sys.exit()

 import argparse

```

--------------------------------

### Pull and Run Kali Linux Docker Image

Source: https://www.kali.org/docs/containers/using-kali-docker-images

This snippet demonstrates how to pull the latest Kali Linux rolling release Docker image and then run an interactive, TTY-enabled container. Note that systemd functionality is not enabled by default and requires Dockerfile modifications.

```bash
docker pull docker.io/kalilinux/kali-rolling
docker run --tty --interactive kalilinux/kali-rolling
```

--------------------------------

### Extract and Copy Mali Libraries (Shell)

Source: https://www.kali.org/docs/development/custom-odroid-kernel-image

Extracts the downloaded Mali OpenGL HF library and copies its contents to the system's library directory. This makes the Mali libraries available to the system.

```shell
kali@kali:~$ tar -xzvf mali_opengl_hf_lib.tgz
kali@kali:~$ cp mali_opengl_hf_lib/* /usr/lib/
kali@kali:~$
```

--------------------------------

### Flash Image to USB Device

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Uses the dd command to write the created Kali Linux image file to a specified USB device (e.g., SD card). It's crucial to replace '/dev/sdX' with the correct device identifier to avoid data loss on the wrong drive.

```bash
kali@kali:~$ dd if=kali-linux-ss808.img of=/dev/sdX conv=fsync bs=4M

```

--------------------------------

### Flash Custom Splash Screen via ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

This command uses ADB sideload to flash a custom splash screen zip file. Ensure your device is in recovery mode and ADB is enabled. The process will automatically reboot the device upon completion.

```shell
adb -d sideload G97X_Splash_Screen_Changer_by_SoLdieR9312_splash.zip
```

--------------------------------

### Navigate to cryptmypi Directory

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Changes the current working directory to the cloned cryptmypi repository. This is a necessary step before executing any of the script's functionalities.

```bash
kali@kali:~$ cd cryptmypi/

```

--------------------------------

### Blacklist Nouveau Driver and Recover System

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

Commands to blacklist the Nouveau driver to prevent it from loading on boot and steps to remove the blacklist if the system fails to boot into the graphical environment. This involves removing a configuration file and updating the initramfs.

```bash
sudo reboot
sudo rm /etc/modprobe.d/blacklist-nouveau.conf
sudo update-initramfs -u
sudo reboot
```

--------------------------------

### Debian Build Rules for python-icmplib with PyBuild

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet defines the debian/rules file, which configures the build process for the python-icmplib package using PyBuild. It sets the PYBUILD_NAME to 'icmplib' to ensure PyBuild uses the correct Python module name, and invokes the standard debhelper commands with Python 3 support.

```makefile
#!/usr/bin/make -f
#export DH_VERBOSE = 1
export PYBUILD_NAME=icmplib

%:
	dh $@ --with python3 --buildsystem=pybuild
```

--------------------------------

### Specify Kali Linux Image and SHA Checksum

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Provides the URL for the Kali Linux ARM image and its corresponding SHA256 checksum. This ensures the integrity of the downloaded image file.

```bash
export _IMAGEURL=https://kali.download/arm-images/kali-2025.4/kali-linux-2025.4-raspberry-pi-arm64.img.xz
export _IMAGESHA="9ef1a0c011c274a81baaa626206ec985e1caa9494dab2b88ecec0a2473d6cf1f"
```

--------------------------------

### Modify Kaboxer YAML for Volume Mounts (Shell)

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Shell command using 'sed' to modify the Kaboxer YAML file, changing a volume mount path from '/var/lib/hello-kbx' to '/tmp/hello-kbx'. This is a workaround for permission issues when creating directories.

```bash
$ sed -i 's;/var/lib/hello-kbx;/tmp/hello-kbx;' *.kaboxer.yaml

```

--------------------------------

### Set DEBFULLNAME and DEBEMAIL Environment Variables

Source: https://www.kali.org/docs/development/setting-up-packaging-system

Configures the DEBFULLNAME and DEBEMAIL environment variables in the ~/.aliases file. This ensures that your full name and email address are set for build processes. It checks if the variables already exist before adding them to prevent duplicates.

```bash
kali@kali:~$ grep -q DEBFULLNAME ~/.profile \
  || echo "export DEBFULLNAME='First Last'" >> ~/.aliases
kali@kali:~$ 
kali@kali:~$ grep -q DEBEMAIL ~/.profile \
  || echo "export DEBEMAIL=email@domain.com" >> ~/.aliases
kali@kali:~$
```

--------------------------------

### Connect to ODROID UART Console using screen

Source: https://www.kali.org/docs/arm/odroid-u

This command connects to the ODROID's serial console using the `screen` utility. It is used for troubleshooting boot process issues. The command connects to `/dev/ttySAC1` at a baud rate of 115200.

```bash
screen /dev/ttySAC1 115200

```

--------------------------------

### Connect to Kali Droplet via SSH

Source: https://www.kali.org/docs/cloud/digitalocean

Establishes an SSH connection to a newly created Kali Linux droplet on DigitalOcean. It requires specifying the private SSH key and the droplet's IP address. The command handles host key verification and displays system information upon successful connection.

```bash
$ ssh -i MY_KEY kali@192.168.1.1
The authenticity of host '192.168.1.1 (192.168.1.1)' can't be established.
ECDSA key fingerprint is SHA256:d83fcd43d25e2a7edd291666160b47360cc85870ded.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'IP' (ECDSA) to the list of known hosts.
Linux kali-s-1vcpu-1gb-nyc3-01 4.19.0-kali5-amd64 #1 SMP Debian 4.19.37-2kali1 (2019-05-15) x86_64
The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.
Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.

```

--------------------------------

### Execute Third-Stage Chroot Script

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Makes the 'third-stage' script executable and then runs it within the chroot environment. This command applies the customizations defined in the script to the Kali ARM rootfs.

```shell
kali@kali:~$ chmod +x kali-$architecture/third-stage
kali@kali:~$ LANG=C chroot kali-$architecture /third-stage
```

--------------------------------

### Update GRUB Configuration

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

Command to update the GRUB bootloader configuration after making changes to `/etc/default/grub`. This ensures that the new kernel parameters and settings are applied on the next boot.

```bash
sudo update-grub
```

--------------------------------

### Query X Server DPI Settings with xrdb

Source: https://www.kali.org/docs/general-use/fixing-dpi

This command queries the X server's database to check for pre-defined DPI settings. It's a first step in diagnosing display issues. No specific inputs are required, and it outputs any found customization or font-related settings.

```bash
kali@kali:~$ xrdb -q
*customization:	-color
Xft.antialias:	1
Xft.hinting:	1
Xft.hintstyle:	hintslight
Xft.rgba:	rgb
Xcursor.theme_core:	1
kali@kali:~$ 
```

--------------------------------

### Configure pyenv for Zsh shell

Source: https://www.kali.org/docs/general-use/using-eol-python-versions

Adds the necessary environment variables and initialization commands to the `.zshrc` file for pyenv to function correctly within the Zsh shell. This ensures pyenv is available and configured when you open a new Zsh session.

```bash
kali@kali:~$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
kali@kali:~$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
kali@kali:~$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init --path)"
fi' >> ~/.zshrc
```

--------------------------------

### Create Non-Root User in Kali GUI Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Creates a non-root user named 'kali' inside the GUI container, adds them to the sudo group, and configures bashrc for display and sudo for disabling core dumps. This is crucial for running GUI applications as a regular user.

```bash
kali@kali:~$ lxc exec gui-kali -- adduser kali
kali@kali:~$ lxc exec gui-kali -- usermod -aG sudo kali
kali@kali:~$ lxc exec gui-kali -- sed -i '1 i\nTERM=xterm-256color' /home/kali/.bashrc
kali@kali:~$ lxc exec gui-kali -- echo "export DISPLAY=:0" >> /home/kali/.bashrc
kali@kali:~$ lxc exec gui-kali -- sh -c "echo 'Set disable_coredump false' > /etc/sudo.conf"
```

--------------------------------

### Create Kernel Device Tree Source (DTS) File

Source: https://www.kali.org/docs/development/custom-chromebook-kernel-image

This code block creates a 'kernel.its' file using a here-document. This file defines the structure of the kernel image and its associated Flattened Device Tree (FDT) blobs, specifying kernel data, FDT data, and configuration details.

```bash
kali@kali:~$ cat <<EOF > kernel.its
/dts-v1/;

/ {
description = "Chrome OS kernel image with one or more FDT blobs";
#address-cells = ;
images {
kernel@1{
description = "kernel";
data = /incbin/("arch/arm/boot/zImage");
type = "kernel_noload";
arch = "arm";
os = "linux";
compression = "none";
load = ;
entry = ;
};
fdt@1{
description = "exynos5250-snow.dtb";
data = /incbin/("arch/arm/boot/exynos5250-snow.dtb");
type = "flat_dt";
arch = "arm";
compression = "none";
hash@1{
algo = "sha1";
};
};
};
configurations {
default = "conf@1";
conf@1{
kernel = "kernel@1";
fdt = "fdt@1";
};
};
};
EOF
```

--------------------------------

### Check Screen Resolution and Connected Displays with xrandr

Source: https://www.kali.org/docs/general-use/fixing-dpi

The xrandr command manages the screen resolution and rotation. This specific usage queries the current screen configuration, including connected displays, their resolutions, and physical dimensions. It helps verify consistency with other display information tools.

```bash
kali@kali:~$ xrandr -q | grep -iw 'screen\|connected'
Screen 0: minimum 8 x 8, current 1680 x 1050, maximum 32767 x 32767
HDMI-0 connected 1680x1050+0+0 (normal left inverted right x axis y axis) 160mm x 90mm
kali@kali:~$ 
```

--------------------------------

### Restore Kali Linux Encrypted Data from LUKS Header Backup

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This procedure decrypts the previously encrypted LUKS header backup file using OpenSSL and then restores it to the target encrypted partition using 'cryptsetup'. This action overwrites the existing header, so caution is advised.

```bash
sudo openssl enc -d -aes-256-cbc -in luksheader.back.enc -out luksheader.back
enter AES-256-CBC decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
sudo cryptsetup luksHeaderRestore --header-backup-file luksheader.back /dev/sdc3

WARNING!
========
Device /dev/sdc3 already contains LUKS2 header. Replacing header will destroy existing keyslots.

Are you sure? (Type 'yes' in capital letters): YES
```

--------------------------------

### Check for Build Dependencies (Bash)

Source: https://www.kali.org/docs/development/rebuilding-a-package-from-source

This command checks for any unmet build dependencies required to compile the package. If no output is produced, all dependencies are satisfied. Otherwise, it lists the missing dependencies.

```bash
kali@kali:~$ dpkg-checkbuilddeps
```

--------------------------------

### Verify GPG Card Status

Source: https://www.kali.org/docs/general-use/configuring-yubikeys-for-ssh-authentication

Checks if GPG (GNU Privacy Guard) can detect the Yubikey as a smart card after it has been configured to CCID mode. This confirms the Yubikey is ready for GPG operations.

```bash
kali@kali:~$ gpg --card-status
Reader ...........: Yubico Yubikey 4 OTP U2F CCID 00 00
Version ..........: 2.1
Manufacturer .....: Yubico
Key attributes ...: rsa2048 rsa2048 rsa2048
Max. PIN lengths .: 127 127 127
PIN retry counter : 3 0 3

```

--------------------------------

### Identify Active OpenCL ICD Loader (Bash)

Source: https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux

This command uses `clinfo` to query and display information about the currently active OpenCL ICD loader. It helps confirm which loader is being used by the system, such as the generic OpenCL ICD Loader.

```bash
kali@kali:~$ clinfo | grep -i "icd loader"
ICD loader properties
  ICD loader Name                                 OpenCL ICD Loader
  ICD loader Vendor                               OCL Icd free software
  ICD loader Version                              2.2.12
  ICD loader Profile                              OpenCL 2.2
kali@kali:~$
```

--------------------------------

### Verify Kali Linux ISO Checksum

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Validates the integrity of the downloaded Kali Linux ISO image by comparing its computed SHA256 checksum against the one listed in the verified SHA256SUMS file. This command is for Linux and macOS environments.

```bash
$ grep kali-linux-2025.4-live-amd64.iso SHA256SUMS | shasum -a 256 -c

```

--------------------------------

### Clone Kernel Source and Apply Patches

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Clones the rk3066 kernel source code from a GitHub repository and applies specific patches related to mac80211 compatibility and channel negative one. These patches are necessary for proper Wi-Fi functionality on the target hardware.

```bash
kali@kali:~$ sudo apt install -y xz-utils
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/
kali@kali:~$ cd ~/arm-stuff/kernel/
kali@kali:~$ 
git clone git://github.com/aloksinha2001/picuntu-3.0.8-alok.git rk3066-kernel
kali@kali:~$ cd rk3066-kernel/
kali@kali:~$ sed -i "/vpu_service/d" arch/arm/plat-rk/Makefile

```

```bash
kali@kali:~$ mkdir -p ../initramfs/
kali@kali:~$ wget http://208.88.127.99/initramfs.cpio -O ../initramfs/initramfs.cpio
kali@kali:$

mkdir -p ../patches/
kali@kali:~$ wget http://patches.aircrack-ng.org/mac80211.compat08082009.wl_frag+ack_v1.patch -O ../patches/mac80211.patch
kali@kali:~$ wget http://patches.aircrack-ng.org/channel-negative-one-maxim.patch- O ../patches/negative.patch
kali@kali:~$ patch -p1 < ../patches/mac80211.patch
kali@kali:~$ patch -p1 < ../patches/negative.patch
kali@kali:$

```

--------------------------------

### Add Hlcan Driver Submodule to Kernel Sources

Source: https://www.kali.org/docs/nethunter/nethunter-kernel-9-config-8

This snippet demonstrates how to add the Hlcan USB CAN driver as a Git submodule to the kernel sources. It involves cloning the repository and then updating the Kconfig and Makefile in the kernel's CAN drivers directory to include the new submodule.

```bash
git submodule add https://github.com/V0lk3n/usb-can-2-module drivers/net/can/usb-can-2-module

# Edit drivers/net/can/Kconfig and add:
source "drivers/net/can/usb-can-2-module/Kconfig"

# Edit drivers/net/can/Makefile and add:
obj-y += usb-can-2-module/
```

--------------------------------

### Configure Console Colors (Bash)

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Sets the TERM environment variable to 'xterm-256color' in the user's .bashrc file within the container and sources the file. This enhances terminal color support for a better user experience.

```bash
kali@kali:~$ sed -i '1 i\TERM=xterm-256color' ~/.bashrc
kali@kali:~$ . ~/.bashrc

```

--------------------------------

### Unmount and Image SD Card

Source: https://www.kali.org/docs/development/custom-raspberry-pi-image

Unmounts the boot and root partitions from the image file, detaches the loop device, and then uses the dd command to write the custom Kali Linux image to the SD card. This step requires careful replacement of '/dev/sdX' with the correct device identifier for the SD card.

```bash
kali@kali:~$ umount $rootp
kali@kali:~$ umount $bootp
kali@kali:~$ kpartx -dv $loopdevice
kali@kali:~$ losetup -d $loopdevice

While ‘/dev/sdX’ is used in the command, the ‘/dev/sdX’ should be replaced with the proper device label. ‘/dev/sdX’ will not overwrite any devices, and can safely be used in documentation to prevent accidental overwrites. Please use the correct device label.
Use the **dd** command to image this file to your SD card. In our example, we assume the storage device is located at `/dev/sdX`. **Change this as needed** :
kali@kali:~$ dd if=kali-linux-rpi.img of=/dev/sdX conv=fsync bs=4M

```

--------------------------------

### Configure Kali Linux Kernel Manually

Source: https://www.kali.org/docs/development/recompiling-the-kali-linux-kernel

Opens the kernel configuration menu interface, allowing for detailed customization of kernel options, drivers, and features. This is an alternative to using an existing configuration file.

```bash
kali@kali:~/kernel$ make menuconfig

```

--------------------------------

### Configure Qt Scaling Factor for HiDPI in Xfce

Source: https://www.kali.org/docs/general-use/hidpi

Sets the Qt scaling factor to 2 for HiDPI displays in Xfce. This is done by adding an export command to the ~/.xsessionrc file, which affects Qt-based applications like qTerminal.

```bash
kali@kali:~$ echo export QT_SCALE_FACTOR=2 >> ~/.xsessionrc
kali@kali:~$
```

--------------------------------

### Add User to Kaboxer Group

Source: https://www.kali.org/docs/development/packaging-apps-with-kaboxer

Adds the current user to the 'kaboxer' group to grant necessary permissions for accessing the Docker daemon. This is often required for users who are not part of the 'docker' group.

```bash
kali@kali:~$ sudo adduser $USER kaboxer

```

--------------------------------

### Configure ODROID-C2 Bootloader Parameters

Source: https://www.kali.org/docs/arm/odroid-c2

This snippet shows how to modify the bootloader parameters for the ODROID-C2 by editing the `/etc/default/u-boot` file. After modification, `u-boot-update` must be run to apply the changes. This is useful for kernel command line adjustments.

```bash
# Example modification to disable USB autosuspend
# Add or modify the U_BOOT_PARAMETERS line in /etc/default/u-boot
# U_BOOT_PARAMETERS="usbcore.autosuspend=-1"

# After editing the file, run:
u-boot-update
```

--------------------------------

### Bypass Git Commit Requirement for Testing

Source: https://www.kali.org/docs/development/intro-to-packaging-example

This command allows testing package build values in debian/ without committing to Git. It uses --git-export=WC to export the working copy. After successful testing, changes can be committed.

```bash
gbp buildpackage --git-builder=sbuild --git-export=WC
```

--------------------------------

### Invoke Kali ARM Build Script for Raspberry Pi

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

This command executes the specific build script for a Raspberry Pi, targeting a particular version of Kali Linux. Ensure the build prerequisites and cross-compilation environment are set up beforehand.

```bash
kali@kali:~$ cd ~/
kali@kali:~$ kali-arm-build-scripts/rpi.sh 2016.2
```

--------------------------------

### Backup and Encrypt LUKS Headers for Kali Linux Recovery

Source: https://www.kali.org/docs/usb/usb-persistence-encryption

This process backs up the LUKS header of an encrypted partition to a file and then encrypts this backup using OpenSSL with AES-256-CBC. The original header is then securely shredded. This is a crucial step before initiating data destruction.

```bash
sudo cryptsetup luksHeaderBackup --header-backup-file luksheader.back /dev/sdX3
sudo openssl enc -e -aes-256-cbc -in luksheader.back -out luksheader.back.enc
enter AES-256-CBC encryption password:
Verifying - enter AES-256-CBC encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
ls -lh luksheader.back*
-r-------- 1 root root 16M Jun  6 07:28 luksheader.back
-rw-r--r-- 1 root root 17M Jun  6 07:29 luksheader.back.enc
file luksheader.back*
luksheader.back:     regular file, no read permission
luksheader.back.enc: openssl enc'd data with salted password
sudo shred -v luksheader.back
shred: luksheader.back: pass 1/3 (random)...
shred: luksheader.back: pass 2/3 (random)...
shred: luksheader.back: pass 3/3 (random)...
```

--------------------------------

### Add dm-crypt Module to Initramfs

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Ensures the 'dm-crypt' kernel module is included in the initramfs by adding it to the /etc/initramfs-tools/modules file. This is necessary for handling encrypted devices during boot.

```bash
# List of modules that you want to include in your initramfs.
# They will be loaded at boot time in the order below.
#
# Syntax:  module_name [args ...]
#
# You must run update-initramfs(8) to effect this change.
#
# Examples:
#
# raid1
# sd_mod
dm_crypt

```

--------------------------------

### LUKS NUKE Kali Password Reset

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Command to reconfigure the cryptsetup package, which can be used to nuke (reset) the LUKS encryption password. This is a utility for managing encryption keys.

```bash
kali@kali:~$ dpkg-reconfigure cryptsetup-nuke-password

```

--------------------------------

### Measure Kali Linux Download Speed with wget

Source: https://www.kali.org/docs/troubleshooting/download-speed-issues

This command uses `wget` to download a Kali Linux ISO file and reports the download speed. This information is crucial for diagnosing slow download issues and can be included when submitting bug reports. It shows the progress, current speed, and estimated time remaining.

```bash
kali@kali:~$ get https://kali.download/base-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
--2025-06-18 10:53:17--  https://kali.download/base-images/kali-2025.4/kali-linux-2025.4-installer-amd64.iso
Resolving kali.download (kali.download)... 2606:4700::6811:fdef, 2606:4700::6811:feef, 104.17.254.239, ...
Connecting to kali.download (kali.download)|2606:4700::6811:fdef|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4478939136 (4.2G) [application/octet-stream]
Saving to: ‘kali-linux-2025.4-installer-amd64.iso’

kali-linux-2025.4-installer-amd64.iso   6% [====> ] 196.46M  31.6MB/s    eta 81s

kali@kali:~$
```

--------------------------------

### Verify SHA256SUMS File Signature

Source: https://www.kali.org/docs/introduction/download-official-kali-linux-images

Verifies the detached signature of the SHA256SUMS file using the imported Kali Linux GPG key. This step confirms that the SHA256SUMS file has not been tampered with and originates from the Kali Linux development team.

```bash
$ gpg --verify SHA256SUMS.gpg SHA256SUMS

```

--------------------------------

### Attach to a Running Kali Linux Docker Container

Source: https://www.kali.org/docs/containers/using-kali-docker-images

This command allows you to attach to a running Docker container, resuming your session in its current state. You may need to press Enter once after attaching to see the prompt.

```bash
docker attach d36922fa21e8
```

--------------------------------

### Clone and Patch Kernel for CuBox

Source: https://www.kali.org/docs/development/custom-cubox-image

Clones the Linux kernel source code from a GitHub repository and applies a specific patch ('mac80211.compat08082009.wl_frag+ack_v1.patch') to it. This step is necessary for compiling the kernel and modules for the CuBox ARM device, especially if not using ARM hardware for development.

```bash
kali@kali:~$ mkdir -p ~/arm-stuff/kernel/
kali@kali:~$ cd ~/arm-stuff/kernel/
kali@kali:~$ git clone --depth 1 https://github.com/rabeeh/linux.git
kali@kali:~$ cd linux/
kali@kali:~$ touch .scmversion
kali@kali:~$ mkdir -p ../patches/
kali@kali:~$ wget http://patches.aircrack-ng.org/mac80211.compat08082009.wl_frag+ack_v1.patch -O ../patches/mac80211.patch
kali@kali:~$ patch -p1 --no-backup-if-mismatch < ../patches/mac80211.patch

```

--------------------------------

### Create and Configure Non-Root User in LXD Container

Source: https://www.kali.org/docs/containers/kalilinux-lxc-images

Creates a new non-root user named 'kali' within the 'my-kali' LXD container, adds them to the 'sudo' group, configures their bashrc for terminal type, and disables core dumps for sudo.

```bash
kali@kali:~$ lxc exec my-kali -- adduser kali
kali@kali:~$ lxc exec my-kali -- usermod -aG sudo kali
kali@kali:~$ lxc exec my-kali -- sed -i '1 i\TERM=xterm-256color' /home/kali/.bashrc
kali@kali:~$ lxc exec my-kali -- sh -c "echo 'Set disable_coredump false' > /etc/sudo.conf"

```

--------------------------------

### Configure NVIDIA Driver for Wayland

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

Modifies the GRUB configuration to enable NVIDIA driver features necessary for Wayland sessions. Specifically, it adds `nvidia_drm.modeset=1` to the kernel command line, allowing the driver to manage display modes early in the boot process.

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi=strict loglevel=3 nvidia_drm.modeset=1"
sudo update-grub
```

--------------------------------

### Troubleshoot Display Output by Removing Xorg Config (Raspberry Pi 4)

Source: https://www.kali.org/docs/arm/raspberry-pi-4

If you are experiencing display issues on your Raspberry Pi 4 with Kali Linux, removing the `99-vc4.conf` file may help by allowing Xorg to use default configurations. This command moves the file to your home directory.

```bash
sudo mv -v /etc/X11/Xorg.conf.d/99-vc4.conf ~
```

--------------------------------

### Add User to vboxusers Group (Linux)

Source: https://www.kali.org/docs/usb/boot-usb-in-virtualbox

This command adds the current user to the 'vboxusers' group, which is necessary for USB access in VirtualBox on Linux systems. Ensure you log out and back in after running this command for the changes to take effect.

```bash
kali@kali:~$ sudo usermod -aG vboxusers $USER
kali@kali:~$ 

```

--------------------------------

### Write Image to SD Card

Source: https://www.kali.org/docs/development/custom-efikamx-image

Uses the dd command to write the created custom Kali image file to the SD card. It's crucial to replace '/dev/sdX' with the correct device label for the target SD card to avoid data loss.

```bash
kali@kali:~$ dd if=kali-linux-efikamx.img of=/dev/sdX conv=fsync bs=4M

```

--------------------------------

### Write Kali Linux Image to Radxa Zero eMMC (Linux - Maskrom Mode)

Source: https://www.kali.org/docs/arm/radxa-zero-emmc

Writes a Kali Linux image to the Radxa Zero's eMMC using the 'dd' utility after it has been erased and presented as a USB storage device. **Warning**: Ensure `/dev/sdX` is the correct device path to avoid data loss on other drives.

```bash
xzcat kali-linux-2025.4-radxa-zero-emmc-arm64.img.xz | sudo dd of=/dev/sdX bs=4M status=progress
```

--------------------------------

### Create Patch File for Version Check

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the content of the `disable-ver_check.patch` file. It details the change made to `finalrecon.py`, specifically commenting out the `ver_check()` function call.

```diff
From: Joseph O'Gorman <gamb1t@kali.org>
Subject: disable ver_check

---
 finalrecon.py | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

diff --git a/finalrecon.py b/finalrecon.py
index 95e99f1..d21877c 100644
--- a/finalrecon.py
+++ b/finalrecon.py
@@ -207,7 +207,7 @@ def full_recon():
 try:
        fetch_meta()
        banner()
-       ver_check()
+       #ver_check()

        if target.startswith(('http', 'https')) == False:
                print(R + '[-]' + C + ' Protocol Missing, Include ' + W + 'http://' + C + ' or ' + W + 'https://' + '\n')

```

--------------------------------

### Edit NVIDIA Xorg Configuration for DPI

Source: https://www.kali.org/docs/general-use/fixing-dpi

This command opens the NVIDIA Xorg configuration file for editing. The goal is to add or modify the `Option "UseEdidDpi" "False"` and `Option "DPI" "99 x 99"` lines within the `Section "Device"` to enforce custom DPI settings.

```shell
kali@kali:~$ sudo vim /usr/share/X11/xorg.conf.d/20-nvidia.conf
kali@kali:~$ 
kali@kali:~$ cat /usr/share/X11/xorg.conf.d/20-nvidia.conf
[...]
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    Option         "UseEdidDpi" "False"
    Option         "DPI" "99 x 99"
EndSection
[...]
kali@kali:~$ 
kali@kali:~$ xfce4-session-logout --logout
kali@kali:~$
```

--------------------------------

### Tune GRUB Kernel Command Line

Source: https://www.kali.org/docs/troubleshooting/graphics-issues-on-bare-metal-installation

This command modifies the GRUB kernel command line to adjust boot verbosity and ACPI handling. It uses `sed` to update the `GRUB_CMDLINE_LINUX_DEFAULT` setting in `/etc/default/grub`, followed by `update-grub` to apply the changes. Caution is advised as disabling ACPI can cause hardware issues.

```bash
kali@kali:~$ sudo sed -i 's/^GRUB_CMDLINE_LINUX_DEFAULT=.*/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi=strict loglevel=3"/' /etc/default/grub
kali@kali:~$ sudo update-grub
[...]
kali@kali:~$ 

```

--------------------------------

### Resize APFS Container using diskutil apfs resizeContainer

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

This command resizes an APFS container to a specified size. It requires administrator privileges (sudo) and the target APFS container's identifier. The command performs file system checks and modifies the partition map to achieve the new size. Ensure you have a backup before proceeding, as incorrect usage can lead to data loss.

```bash
$ sudo diskutil apfs resizeContainer disk0s2 400g
Password:
Started APFS operation
Aligning shrink delta to 99,898,105,856 bytes and targeting a new physical store size of 400,000,000,000 bytes
Determined the minimum size for the targeted physical store of this APFS Container to be 17,949,245,440 bytes
Resizing APFS Container designated by APFS Container Reference disk1
The specific APFS Physical Store being resized is disk0s2
Verifying storage system
Using live mode
Performing fsck_apfs -n -x -l /dev/disk0s2
Checking volume
Checking the container superblock
Checking the EFI jumpstart record
Checking the space manager
Checking the object map
Checking the APFS volume superblock
Checking the object map
Checking the fsroot tree
Checking the snapshot metadata tree
Checking the extent ref tree
Checking the snapshots
Checking the APFS volume superblock
Checking the object map
Checking the fsroot tree
Checking the snapshot metadata tree
Checking the extent ref tree
Checking the snapshots
Checking the APFS volume superblock
Checking the object map
Checking the fsroot tree
Checking the snapshot metadata tree
Checking the extent ref tree
Checking the snapshots
Checking the APFS volume superblock
Checking the object map
Checking the fsroot tree
Checking the snapshot metadata tree
Checking the extent ref tree
Checking the snapshots
Verifying allocated space
The volume /dev/disk0s2 appears to be OK
Storage system check exit code is 0
Shrinking APFS Physical Store disk0s2 from 499,898,105,856 to 400,000,000,000 bytes
Shrinking APFS data structures
Shrinking partition
Modifying partition map
Finished APFS operation
$
```

--------------------------------

### List SSH Host Keys in Kali Linux

Source: https://www.kali.org/docs/general-use/ssh-configuration

This command lists the SSH host keys typically found in the /etc/ssh directory. These keys are essential for the SSH server's functionality and should be unique to each machine.

```bash
kali@kali:~$ ls -l /etc/ssh/ssh_host_*
-rw------- 1 root root 1373 Feb  3 23:50 /etc/ssh/ssh_host_dsa_key
-rw-r--r-- 1 root root  599 Feb  3 23:50 /etc/ssh/ssh_host_dsa_key.pub
-rw------- 1 root root  505 Feb  3 23:50 /etc/ssh/ssh_host_ecdsa_key
-rw-r--r-- 1 root root  171 Feb  3 23:50 /etc/ssh/ssh_host_ecdsa_key.pub
-rw------- 1 root root  399 Feb  3 23:50 /etc/ssh/ssh_host_ed25519_key
-rw-r--r-- 1 root root   91 Feb  3 23:50 /etc/ssh/ssh_host_ed25519_key.pub
-rw------- 1 root root 2590 Feb  3 23:50 /etc/ssh/ssh_host_rsa_key
-rw-r--r-- 1 root root  563 Feb  3 23:50 /etc/ssh/ssh_host_rsa_key.pub

```

--------------------------------

### Dump CAN Bus Traffic with candump

Source: https://www.kali.org/docs/nethunter/nethunter-carsenal

Illustrates how to use the 'candump' tool from the can-utils suite to capture and display CAN bus traffic. This is essential for monitoring communication, debugging issues, and analyzing the behavior of electronic control units (ECUs) in a vehicle.

```bash
# Example usage of candump (assuming can0 is up)
candump can0
```

--------------------------------

### Unmount and Detach Image

Source: https://www.kali.org/docs/development/custom-kali-arm-ss808-image

Unmounts the root filesystem from the image file and detaches the loop device. This is a cleanup step to ensure the image file is in a consistent state before flashing.

```bash
kali@kali:~$ umount $rootp
kali@kali:~$ kpartx -dv $loopdevice
kali@kali:~$ losetup -d $loopdevice

```

--------------------------------

### Manually Chroot into Kali ARM Rootfs

Source: https://www.kali.org/docs/development/kali-linux-arm-chroot

Allows for manual interaction and modification within the chroot environment of the Kali ARM rootfs. This is useful for making ad-hoc changes or debugging.

```shell
kali@kali:~$ LANG=C chroot kali-$architecture
```

--------------------------------

### Remove Xorg Configuration for Display Output

Source: https://www.kali.org/docs/arm/raspberry-pi-64-bit

This command moves the Xorg configuration file `/etc/X11/Xorg.conf.d/99-vc4.conf` to the user's home directory. This is a troubleshooting step for display issues on Raspberry Pi, where removing this file allows Xorg to attempt using default configurations, potentially resolving display problems.

```bash
kali@kali:~$ sudo mv -v /etc/X11/Xorg.conf.d/99-vc4.conf ~
```

--------------------------------

### Debian Watch File for GitHub Releases of icmplib

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the debian/watch file, which is used to monitor upstream releases of the icmplib package from GitHub. It specifies the GitHub repository, a pattern to extract version numbers from release tags, and a filename mangling rule to ensure consistent tarball naming.

```text
version=4
opts=filenamemangle=s/.+/v?(dS+).tar.gz/icmplib-$1.tar.gz/ \
  https://github.com/ValentinBELYN/icmplib/tags .*/v?(dS+).tar.gz
```

--------------------------------

### Display Kali Linux Memory Usage

Source: https://www.kali.org/docs/cloud/digitalocean

Shows the current memory and swap usage for the Kali Linux system in a human-readable format. It details total, used, and free memory, as well as swap space utilization.

```bash
kali@kali-s-1vcpu-1gb-nyc3-01:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:           987Mi        51Mi        527Mi        1.0Mi        407Mi        790Mi
Swap:            0B          0B          0B

```

--------------------------------

### Cleanup System Logs and History

Source: https://www.kali.org/docs/cloud/digitalocean

Removes unused packages, cleans the package cache, clears log files, and clears the command history. This reduces the image size and removes sensitive information before uploading.

```bash
kali@kali:~$ apt autoremove
kali@kali:~$ apt autoclean
kali@kali:~$ rm -rf /var/log/*
kali@kali:~$ history -c
```

--------------------------------

### Configure GTK Scaling Factor for HiDPI in Xfce

Source: https://www.kali.org/docs/general-use/hidpi

Sets the GTK scaling factor to 2 for HiDPI displays in Xfce. This involves modifying the ~/.xsessionrc file and using xfconf-query to set window scaling and theme. A logout/login is recommended for changes to take full effect.

```bash
kali@kali:~$ echo export GDK_SCALE=2 >> ~/.xsessionrc
kali@kali:~$ 
kali@kali:~$ xfconf-query -c xfwm4 -p /general/theme -s Kali-Dark-xHiDPI
kali@kali:~$ 
kali@kali:~$ xfconf-query -c xsettings -p /Gdk/WindowScalingFactor -n -t 'int' -s 2
kali@kali:~$
```

--------------------------------

### Generate New SSH Key for Dropbear

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Generates a new SSH key pair with RSA encryption and a key length of 4096 bits, specifically naming the output files for Dropbear usage. The public key is then copied to the chroot environment.

```bash
ssh-keygen -t rsa -b 4096
# [...] Enter file in which to save the key (/home/kali/.ssh/id_rsa): /home/kali/.ssh/id_rsa_dropbear
# [...] Enter passphrase (empty for no passphrase):
# [...] Enter same passphrase again:
# [...] Your identification has been saved in /home/kali/.ssh/id_rsa_dropbear
# [...] Your public key has been saved in /home/kali/.ssh/id_rsa_dropbear.pub
# [...] 
$ sudo cp ~/.ssh/id_rsa_dropbear.pub /mnt/chroot/
```

--------------------------------

### Remove Desktop Environment Metapackage (Bash)

Source: https://www.kali.org/docs/general-use/switching-desktop-environments

Removes a desktop environment metapackage, such as kali-desktop-xfce, using apt purge with the --allow-remove-essential flag. This is necessary because these metapackages are system-protected.

```bash
kali@kali:~$ sudo apt purge --autoremove --allow-remove-essential kali-desktop-xfce
kali@kali:~$ 

```

--------------------------------

### Convert Log Files with asc2log and log2asc

Source: https://www.kali.org/docs/nethunter/nethunter-carsenal

Explains the utility of 'asc2log' and 'log2asc' from the can-utils suite for converting CAN log file formats. 'asc2log' converts from ASC format to a compact log format, while 'log2asc' performs the reverse. This is useful for interoperability with different logging tools.

```bash
# Convert ASC to compact log
asc2log input.asc output.log

# Convert compact log to ASC
log2asc input.log output.asc
```

--------------------------------

### Update /etc/fstab for Encrypted Filesystem

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Modifies the /etc/fstab file to point the root filesystem to the encrypted device, identified as /dev/mapper/crypt. This ensures the system mounts the encrypted partition correctly at boot.

```bash
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
proc            /proc           proc    defaults          0       0

/dev/mapper/crypt /               ext4 errors=remount-ro 0       0
#UUID=747bfa7c-edd2-471f-8fff-0ecafc2d3791 /               ext4 errors=remount-ro 0       1
LABEL=BOOT      /boot           vfat    defaults          0       2

```

--------------------------------

### Generate CAN Frames with cangen

Source: https://www.kali.org/docs/nethunter/nethunter-carsenal

Demonstrates the usage of the 'cangen' tool from the can-utils suite. 'cangen' is used to generate CAN frames for testing purposes, allowing users to simulate traffic on the CAN bus. This is useful for testing the functionality of other CAN-related tools and systems.

```bash
# Example usage of cangen (assuming can0 is up)
cangen can0
```

--------------------------------

### Disable systemd Boot in Kali KDE for VMware

Source: https://www.kali.org/docs/virtualization/troubleshooting-vmware

This command modifies the KDE configuration to disable the systemd user instance, which resolves copy/paste and drag/drop issues in VMware virtual machines. It creates or updates the `~/.config/startkderc` file.

```bash
kwriteconfig5 --file startkderc --group General --key systemdBoot false

```

--------------------------------

### Check Attached Devices with ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This command verifies that the Android Debug Bridge (ADB) can detect and communicate with the connected device. It lists all attached devices and their status. Ensure 'Android debugging' is enabled on the device.

```bash
kali@kali:~$ adb devices
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
dea044c9    device

kali@kali:~

```

--------------------------------

### Bypass debootstrap Version Check (Bash)

Source: https://www.kali.org/docs/development/live-build-a-custom-kali-iso

Modifies the build.sh script to bypass the debootstrap version check. This is sometimes necessary on non-Kali Debian-based systems.

```bash
$ cat build.sh
[...]
		ver_debootstrap=$(dpkg-query -f '${Version}' -W debootstrap)
		if dpkg --compare-versions "$ver_debootstrap" lt "1.0.97"; then
			echo "ERROR: You need debootstrap (>= 1.0.97), you have $ver_debootstrap" >&2
			#exit 1
		fi
[...]
$
```

--------------------------------

### Inspect NVIDIA Driver DPI Settings in Xorg Log

Source: https://www.kali.org/docs/general-use/fixing-dpi

This command searches the Xorg log file for DPI settings related to the NVIDIA driver. It reveals how the driver is attempting to set the DPI, often based on EDID data from the monitor. This helps identify if the graphics driver is the source of incorrect DPI values.

```bash
kali@kali:~$ grep DPI /var/log/Xorg.0.log
[     7.324] (--) NVIDIA(0): DPI set to (266, 296); computed from "UseEdidDpi" X config
kali@kali:~$ 
```

--------------------------------

### Reboot Device to Bootloader Mode with ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

This ADB command reboots the connected Android device directly into bootloader mode, also known as Fastboot mode. This is a prerequisite for unlocking the bootloader and flashing custom ROMs. The device must be connected and recognized by ADB.

```bash
kali@kali:~$ adb reboot bootloader
kali@kali:~

```

--------------------------------

### Update Debian Changelog for FinalRecon Package

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows how to update the debian/changelog file for the FinalRecon package. It includes the command to edit the file using vim and the resulting content after an initial release. The changelog tracks version, distribution, and description changes.

```bash
kali@kali:~/kali/packages/finalrecon$ vim debian/changelog
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ cat debian/changelog
finalrecon (0.0~git20201107.0d41eb6-0kali1) kali-dev; urgency=medium

  * Initial release

 -- Joseph O'Gorman <gamb1t@kali.org>  Fri, 22 Apr 2022 11:33:33 +0700
kali@kali:~/kali/packages/finalrecon$

```

--------------------------------

### Stop Nexmon Monitor Mode

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-samsung-galaxy-s10

These commands stop Nexmon's monitor mode and re-enable the Wi-Fi service. This is used to revert the network interface back to its normal operational state.

```bash
$ nexutil -m0
$ svc wifi enable
```

--------------------------------

### List Git Branches and Status

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the output of `git branch -v`, which lists all local branches and their latest commit information. It helps in verifying the current state of the branches, including the `patch-queue/kali/master` branch with the applied patches.

```bash
kali@kali:~/kali/packages/finalrecon$
kali@kali:~/kali/packages/finalrecon$ git branch -v
* kali/master             bd003d7 New upstream version 0.0~git20201107.0d41eb6
  patch-queue/kali/master 2935f22 disable ver_check
  pristine-tar            2413cfe pristine-tar data for finalrecon_0.0~git20201107.0d41eb6.orig.tar.gz
  upstream                bd003d7 New upstream version 0.0~git20201107.0d41eb6
kali@kali:~/kali/packages/finalrecon$
```

--------------------------------

### Compile Linux Kernel for Beaglebone Black

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Clones the linux-dev repository, checks out a specific kernel branch, builds the kernel using a provided script, and applies a patch. This process generates the kernel image and associated files.

```bash
kali@kali:~$ mkdir -p kernel/
kali@kali:~$ cd kernel/
kali@kali:~$ git clone git://github.com/RobertCNelson/linux-dev.git
kali@kali:~$ cd linux-dev/
kali@kali:~$ git checkout origin/am33x-v3.8 -b tmp
kali@kali:~$ ./build_kernel.sh
kali@kali:~$ mkdir -p ../patches/
kali@kali:~$ wget http://patches.aircrack-ng.org/mac80211.compat08082009.wl_frag+ack_v1.patch -O ../patches/mac80211.patch
kali@kali:~$ cd KERNEL/
kali@kali:~$ patch -p1 --no-backup-if-mismatch < ../../patches/mac80211.patch
kali@kali:~$ cd ../
kali@kali:~$ ./tools/rebuild.sh
kali@kali:~$ cd ../
```

--------------------------------

### Unmount and Detach Image Partitions

Source: https://www.kali.org/docs/development/custom-efikamx-image

Unmounts the boot and root partitions from the image file, detaches the loop device, and removes the loop device. This cleans up the mounted partitions and releases the loop device.

```bash
kali@kali:~$ umount $bootp
kali@kali:~$ umount $rootp
kali@kali:~$ kpartx -dv $loopdevice
kali@kali:~$ losetup -d $loopdevice

```

--------------------------------

### Configure rEFInd on Kali Linux

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

Specifies the location of the rEFInd configuration file on Kali Linux for editing. This command allows direct access to modify rEFInd settings on the Kali Linux system.

```bash
kali@kali:~$ sudo vim /boot/efi/EFI/refind/refind.conf
kali@kali:~$ 

```

--------------------------------

### Configure rEFInd on macOS/OS X Yosemite and earlier

Source: https://www.kali.org/docs/installation/dual-boot-kali-with-mac

Details how to edit the rEFInd configuration file on macOS/OS X Yosemite (10.10) or earlier. On these versions, the EFI boot volume is not automatically mounted, and the configuration file is directly accessible.

```bash
$ sudo vim /EFI/refind/refind.conf
$ s

```

--------------------------------

### Define ELM327 Driver Kconfig (Kernel 4.11+)

Source: https://www.kali.org/docs/nethunter/nethunter-kernel-9-config-8

Adds the configuration option for the ELM327 based OBD-II CAN interface to the kernel's Kconfig file. This enables users to select the driver during kernel configuration, with dependencies on TTY and support for RX offload.

```kconfig
config CAN_CAN327
	tristate "Serial / USB serial ELM327 based OBD-II Interfaces (can327)"
	depends on TTY
	select CAN_RX_OFFLOAD
	help
	  CAN driver for several 'low cost' OBD-II interfaces based on the
	  ELM327 OBD-II interpreter chip.

	  This is a best effort driver - the ELM327 interface was never
	  designed to be used as a standalone CAN interface. However, it can
	  still be used for simple request-response protocols (such as OBD II),
	  and to monitor broadcast messages on a bus (such as in a vehicle).

	  Please refer to the documentation for information on how to use it:
	  Documentation/networking/device_drivers/can/can327.rst

	  If this driver is built as a module, it will be called can327.
```

--------------------------------

### Debian Copyright Information for icmplib

Source: https://www.kali.org/docs/development/advanced-packaging-example

This snippet shows the debian/copyright file for the python-icmplib package. It specifies the upstream name, contact, source URL, and licensing details for the software and Debian-specific packaging files. The license is LGPL-3+.

```text
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: icmplib
Upstream-Contact: Valentin BELYN <valentin-hello@gmx.com>
Source: https://github.com/ValentinBELYN/icmplib

Files: *
Copyright: 2020 Valentin BELYN <valentin-hello@gmx.com>
License: LGPL-3+

Files: debian/*
Copyright: 2020 Joseph O'Gorman <gamb1t@kali.org>
License: LGPL-3+

License: LGPL-3+
 This program is free software; you can redistribute it and/or modify it
 under the terms of the GNU Lesser General Public License as
 published by the Free Software Foundation; either version 3 of
 the License, or (at your option) any later version.
 .
 This program is distributed in the hope that it will be useful, but
 WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
 Lesser General Public License for more details.
 .
 You should have received a copy of the GNU Lesser General Public
 License along with this program; if not, see <https://www.gnu.org/licenses/>.
 .
 On Debian systems, the full text of the GNU Lesser General Public
 License version 3 can be found in the file
 `/usr/share/common-licenses/LGPL-3'.
```

--------------------------------

### Pytest-factoryboy Control File and Test Script

Source: https://www.kali.org/docs/development/contributing-runtime-tests

This configuration defines a test for 'pytest-factoryboy' that depends on 'python3-pytest-pep8'. The associated shell script executes pytest tests within a temporary directory, iterating through available Python 3 versions.

```text
Tests: test3-pytest-factoryboy
Depends: @, python3-pytest-pep8

```

```shell
#!/bin/sh
set -e
cp -r tests "$AUTOPKGTEST_TMP/" && cd "$AUTOPKGTEST_TMP"
for py in $(py3versions -i); do
    $py -Wd -m pytest -v -x tests 2>&1;
done

```

--------------------------------

### Unmount and Close Encrypted Kali Partition

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Commands to properly unmount all mounted filesystems from the encrypted partition and then close the LUKS container. This is a crucial step to ensure data integrity and security.

```bash
exit
$ sudo umount /mnt/encrypted/{boot,sys,proc,dev/pts,dev}
$ sudo umount /mnt/encrypted
$ sudo cryptsetup luksClose crypt

```

--------------------------------

### Erase eMMC on Radxa Zero using Maskrom Mode (Linux)

Source: https://www.kali.org/docs/arm/radxa-zero-emmc

Uses the 'boot-g12.py' script with 'radxa-zero-erase-emmc.bin' to erase the eMMC on the Radxa Zero. This prepares the eMMC for a new image and exposes it as a USB storage device.

```bash
sudo boot-g12.py radxa-zero-erase-emmc.bin
```

--------------------------------

### Verify TWRP Recovery Access using ADB

Source: https://www.kali.org/docs/nethunter/installing-nethunter-on-the-oneplus-one

After flashing TWRP, this command verifies that the device is recognized in recovery mode by ADB. This confirms that the recovery partition has been successfully flashed and the device is ready for further operations.

```bash
kali@bdesktop:~$ adb devices
List of devices attached
dea044c9  recovery

kali@bdesktop:~$
```

--------------------------------

### Add ELM327 Driver (Kernel 4.11+)

Source: https://www.kali.org/docs/nethunter/nethunter-kernel-9-config-8

Adds the ELM327 CAN driver as a git submodule for kernel versions 4.11 and higher. This involves cloning the driver repository and copying the necessary source file.

```bash
git submodule add https://github.com/V0lk3n/elmcan drivers/net/can/elmcan
cp drivers/net/can/elmcan/can327.c drivers/net/can/
```

--------------------------------

### Enabling Network Service Persistence Across Reboots (Kali Linux)

Source: https://www.kali.org/docs/policy/kali-linux-network-service-policy

Shows how to override the default Kali Linux policy and enable a network service to persist across reboots using the `systemctl enable` command. This is useful when specific services are required to be active after a system restart.

```bash
kali@kali:~$ sudo systemctl enable apt-cacher-ng
Synchronizing state of apt-cacher-ng.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable apt-cacher-ng
insserv: warning: current start runlevel(s) (empty) of script `apt-cacher-ng' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `apt-cacher-ng' overrides LSB defaults (0 1 6).


```

--------------------------------

### Add ELM327 Driver (Kernel < 4.11)

Source: https://www.kali.org/docs/nethunter/nethunter-kernel-9-config-8

Adds the ELM327 CAN driver as a git submodule for kernel versions lower than 4.11, using a specific branch for compatibility. This involves cloning the driver repository into the appropriate kernel directory.

```bash
git submodule add -b linux-pre-4.11 https://github.com/V0lk3n/elmcan drivers/net/can/elmcan
```

--------------------------------

### Enable OS Prober in GRUB Configuration

Source: https://www.kali.org/docs/troubleshooting/dual-boot

This snippet demonstrates how to ensure the GRUB bootloader is configured to detect other operating systems. It involves modifying the `/etc/default/grub` file to uncomment the `GRUB_DISABLE_OS_PROBER=false` line, which enables the os-prober utility. This is a crucial step for GRUB to scan for and list other bootable partitions.

```bash
kali@kali:~$ cat /etc/default/grub | grep GRUB_DISABLE_OS_PROBER
#GRUB_DISABLE_OS_PROBER=false
kali@kali:~$ 
kali@kali:~$ sudo sed -i 's/#GRUB_DISABLE_OS_PROBER=false/GRUB_DISABLE_OS_PROBER=false/' /etc/default/grub
kali@kali:~$ 
kali@kali:~$ cat /etc/default/grub | grep GRUB_DISABLE_OS_PROBER
GRUB_DISABLE_OS_PROBER=false
kali@kali:~$
```

--------------------------------

### Redirect Audio Output to 3.5mm Jack (Raspberry Pi 4)

Source: https://www.kali.org/docs/arm/raspberry-pi-4

This command redirects audio output from HDMI to the 3.5mm audio jack on the Raspberry Pi 4. It modifies the ALSA mixer settings.

```bash
sudo amixer -c 0 set numid=3 1
```

--------------------------------

### Set Root Password in Kali Linux

Source: https://www.kali.org/docs/general-use/enabling-root

This command allows you to set or change the password for the root user. It prompts for the current user's password (if using sudo) and then for the new root password twice. This is a prerequisite for enabling direct root login.

```bash
kali@kali:~$ sudo passwd
[sudo] password for kali:
New password:
Retype new password:
passwd: password updated successfully
kali@kali:~$
```

--------------------------------

### Configure LUKS Encryption Settings

Source: https://www.kali.org/docs/arm/raspberry-pi-with-luks-full-disk-encryption-2

Defines the encryption cipher, password, and extra options for LUKS encryption. The cipher `aes-cbc-essiv:sha256` is used. Extra options can be specified for specific hardware, like reducing memory requirements on Raspberry Pi models.

```bash
export _LUKSCIPHER="aes-cbc-essiv:sha256"
export _LUKSPASSWD="luks_password"
export _LUKSEXTRA=""
```

--------------------------------

### Configure SSH Root Login in Kali Linux

Source: https://www.kali.org/docs/general-use/enabling-root

This snippet demonstrates how to check and modify the SSH daemon configuration to allow or disallow root login. It involves grepping the `sshd_config` file for the `PermitRootLogin` directive and potentially restarting the SSH service. The `man sshd_config` command provides details on the available options.

```bash
kali@kali:~$ grep PermitRootLogin /etc/ssh/sshd_config
#PermitRootLogin prohibit-password
# the setting of "PermitRootLogin without-password".
kali@kali:~$ 
kali@kali:~$ man sshd_config | grep -C 1 prohibit-password
     PermitRootLogin
             Specifies whether root can log in using ssh(1).  The argument must be yes, prohibit-password, forced-commands-only, or no.  The default
             is prohibit-password.

             If this option is set to prohibit-password (or its deprecated alias, without-password), password and keyboard-interactive authentication
             are disabled for root.
kali@kali:~$ 
kali@kali:~$ sudo systemctl restart ssh
kali@kali:~$
```

--------------------------------

### Clean up loop devices

Source: https://www.kali.org/docs/development/custom-beaglebone-black-image

Unmounts any mounted partitions associated with a loop device and detaches the loop device itself. This is a cleanup step after imaging an SD card.

```bash
kali@kali:~$ umount $rootp
kali@kali:~$ kpartx -dv $loopdevice
kali@kali:~$ losetup -d $loopdevice
```

--------------------------------

### Build Modified Package (Bash)

Source: https://www.kali.org/docs/development/rebuilding-a-package-from-source

This command initiates the process of building the modified package from its source code. It utilizes the 'dpkg-buildpackage' tool, which handles the compilation and packaging process.

```bash
kali@kali:~$ dpkg-buildpackage
```

--------------------------------

### Change Yubikey PINs using GPG

Source: https://www.kali.org/docs/general-use/configuring-yubikeys-for-ssh-authentication

Modifies the default PIN and Admin PIN for the Yubikey using GPG commands. This is a crucial security step to protect your Yubikey.

```bash
kali@kali:~$ gpg --change-pin
gpg: OpenPGP card no. F8482212202010006041587850000 detected

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? 1 # Enter a new PIN
PIN changed.

1 - change PIN

Your selection? 3 # Enter a new admin PIN
PIN changed.

Your selection? q

```

--------------------------------

### Check Network Ports for Guacamole Services

Source: https://www.kali.org/docs/general-use/guacamole-kali-in-browser

This command uses 'ss' to display network socket statistics, filtering for processes related to MySQL ('mysqld'), Guacamole ('guacd'), and Tomcat ('java'). It verifies that these services are listening on their expected ports (3306 for MySQL, 4822 for Guacamole, and 8080 for Tomcat).

```bash
kali@kali:/tmp/guac-install$ sudo ss -antup | grep "mysqld\|guacd\|java"
tcp    LISTEN  0       80                 127.0.0.1:3306         0.0.0.0:*       users:(("mysqld",pid=33787,fd=21))
tcp    LISTEN  0       5                  127.0.0.1:4822         0.0.0.0:*       users:(("guacd",pid=991,fd=4))
tcp    LISTEN  0       100                        *:8080               *:*       users:(("java",pid=33192,fd=36))
kali@kali:/tmp/guac-install$ 

```

--------------------------------

### Set Cursor Size for HiDPI in Xfce

Source: https://www.kali.org/docs/general-use/hidpi

Forces a specific cursor size (e.g., 48 pixels) for HiDPI displays in Xfce by setting the XCURSOR_SIZE environment variable in ~/.xsessionrc. The value may need adjustment based on display resolution and user preference.

```bash
kali@kali:~$ echo export XCURSOR_SIZE=48 >> ~/.xsessionrc
kali@kali:~$
```

--------------------------------

### Detect Yubikey using pcsc_scan

Source: https://www.kali.org/docs/general-use/configuring-yubikeys-for-ssh-authentication

Scans for connected smart card readers and identifies the Yubikey. This command helps verify if the system recognizes the Yubikey hardware.

```bash
kali@kali:~$ pcsc_scan
Scanning present readers...
Reader 0: Yubico Yubikey 4 OTP+U2F+CCID 00 00
  Card state: Card inserted,
Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
    Yubico Yubikey 4 OTP+CCID

```

--------------------------------

### Send CAN Frames with cansend

Source: https://www.kali.org/docs/nethunter/nethunter-carsenal

Shows how to use the 'cansend' tool from the can-utils suite to transmit individual CAN frames onto the bus. This tool is valuable for sending specific commands or test messages to ECUs, aiding in diagnostics and security testing.

```bash
# Example usage of cansend (assuming can0 is up)
cansend can0 123#11223344
```