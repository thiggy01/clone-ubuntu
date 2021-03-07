# clone-ubuntu

This is a tool to clone your linux root "/" system and your separate home "/home" partition, if there is one, to 
another disk in a seamlessly and safely way. You may use it to move your data to a Solid State Drive (SSD) when upgrading your computer or to create an isolated environment for testing purposes.

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

### Prerequisites and Warnings

* The script must be ran in a terminal running bash shell and whiptail package has to be installed.

* You must be cloning from inside your mounted root system and mounted home partition.
 
* Your target clone partitions must not be mounted and have to be using an ext4 file system.

* When you are recloning, any new data on the previous clone partition will be deleted.

* Don't use your computer while it's being cloned because you may end up with inconsistent data between your cloned source and clone target.

* IF YOU DON'T FOLLOW THE INSTRUCTIONS GIVEN ABOVE, THIS SCRIPT WILL DISPLAY A WARNING MESSAGE AND ABORT THE CLONING PROCESS.

## Usage

Download the script with the following command: `wget github.com/thiggy01/clone-ubuntu/raw/master/clone-ubuntu`, make it executable with `chmod +x clone-ubuntu` and run it with root privileges as `sudo ./clone-ubuntu`

After starting the script, you will see instructions on how to prepare your disk to clone your system properly. Then, a menu will be asking you to select your umounted target root "/" ext4 partition and, if you have a separate /home partition, it will be detected by the script and you will be promped to select the target /home partition. 

After you selected the appropriate partitions, the script will mount your target root partition and ask you to proceed. If you type Y or y, the script will start the cloning process, showing the progress and some stats. Then, when the cloning process is finished, the script will change the target fstab file in order to mount the correct clone UUID. It will also change the target grub.cfg file to include the clone's UUID, install the proper grub in the new disk and update it so you can have the appropriate boot menu. 

If you have a separate /home partitionf the script will also ask you if you want to proceed with the process of cloning your home partition.

Finally, the script will unmount your root and home (if there is one) partitions and clean up all temporary files. Then, when you boot from your new device, you should see a new grub menu entry for your clone linux distribution to boot it as you would with the cloned disk.
