# clone-linux

This is a tool to clone your linux root "/" system and your separate home "/home" partition, if there is one, to 
another disk in a seamlessly and safely way. You may use it to move your data to a Solid State Drive (SSD) when upgrading your computer or to create a isolated environment for testing purposes.

## Credits 
 
This script is a fork of the code posted by WinEunuuchs2Unix at [askubuntu.com](https://bit.ly/34RNGbv) as a tool to avoid
losing the whole system when upgrading from Ubuntu 16.04, 17.04 or 17.10 LTS to 18.04 LTS.

## Changings

I removed some features like changing release-upgrades file, moving your cron jobs to a hold folder, among other
things. I also added the ability to detect and clone, not just the root partition, but the /home partition too, among 
other things to turn the cloning process easier and safer.

## Preparation

### Booting and Partitioning

* Your boot loader must be grub2 and and you'll have to remove all changes made by grub-customizer if installed.

* You'll need to create a BIOS boot partition of at least 1MiB to boot from a BIOS/GPT layout. 

* You'll need to create an EFI system partition of at least 100MiB to boot from an UEFI/MBR or an UEFI/GPT layout.

* These booting partitions need to be created before your system partitions for GRUB to work properly.

* You must create empty ext4 partitions large enough to hold your boot and home (if there is one) partitions.

* For information about how to create them, visit: https://wiki.archlinux.org/index.php/Partitioning   

### Prerequisites

* The script must be ran in a terminal running bash shell and whiptail package has to be installed.

* You must be cloning from inside your mounted root system and mounted home partition.
 
* Your target clone partitions must not be mounted and have to be an ext4 file system.

### Warnings

* When you are recloning, any new data on the previous clone partition will be deleted.

* Don't use your computer while it's being cloned because you may end up with inconsistent data between your cloned source and clone target.

* IF YOU DON'T FOLLOW THE INSTRUCTIONS GIVEN ABOVE, THIS SCRIPT WILL DISPLAY A WARNING MESSAGE AND ABORT THE CLONING PROCESS.

## Usage

Download it with the following command: `curl -L -O github.com/thiggy01/clone-ubuntu/raw/master/clone-ubuntu`, give it
execution permission with `chmod +x clone-ubuntu` and run it with root privileges as `sudo ./clone-ubuntu`

After starting the script, you will see a series of instructions on how to prepare your disk to run the script properly.

menu asking you to select your umounted target boot "/" ext4 partition.

<p align="center"><img width="460" height="312" src="https://i.imgur.com/2fUBIgr.png"></p>

If you have a separate /home partition, it will be detected by the script and you will be promped to select the target
/home partition.

<p align="center"><img width="460" height="312" src="https://i.imgur.com/be18MSl.png"></p>

After you selected the appropriate partitions, the script will mount your target boot partition and show a confirmation
screen with the source and target information, including size, used and available space, etc.

<p align="center"><img width="460" height="312" src="https://i.imgur.com/FEhgCp4.png"></p>

If you press Y or y to proceed, the script starts the cloning process and will show progress and some stats at the end.
When the copying is finished, the script will change the target fstab file in order to mount the corrent clone UUID.
It also changes the UUID from the target grub.cfg file to the clone one and update it to add the menu entry for the 
clone linux system, as shown below:

<p align="center"><img width="460" height="312" src="https://i.imgur.com/6cJnMC6.gif"></p>

As you could see on the image above, if you selected a target /home partition, a confirmation screen will be
showing information about the source and target home partitions and, if you press y or Y to proceed, it will carry out
almost the same process as before, with exception of not changing the grub configuration file.

<p align="center"><img width="460" height="312" src="https://i.imgur.com/4aBPyon.gif"></p>

Finally, the script will be unmounting your boot and home (if there is one) partitions and cleaning up all temporary files.
The next time you boot your computer, you should see a new grub menu entry for your clone linux distribution and boot it 
normally, as you would with the cloned one.
