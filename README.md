# clone-linux

This is a tool to clone your linux boot "/" system and your separate home "/home" partition, if there is one, into 
another partition or device in a seamlessly and safely way.

## Credits 
 
This script is a fork of the code posted by WinEunuuchs2Unix at [askubuntu.com](https://bit.ly/34RNGbv) as a tool to avoid
losing the whole system when upgrading from Ubuntu 16.04, 17.04 or 17.10 LTS to 18.04 LTS.

## Changings

I removed some functionalities like changing release-upgrades file, moving your cron jobs to a hold folder, among other
things. I also added the ability to detect and clone, not just the root partition, but the /home partition too, among 
other coding tweaks to turn the cloning process safer.

## Preparation

Imortant notes to consider:

* Your boot loader must be grub and the script must be ran in a terminal with bash shell and whiptail dialog boxes.

* You must be cloning from your mounted (live) boot system and mounted home partition.

* You must create empty ext4 partitions large enough to hold your boot and home partitions.

* Your target (clone) partitions must not be mounted before calling the `clone-linux` script.

* When you are recloning, any new data on the previous clone partition will be deleted.

* Before cloning, a confirmation screen is displayed with information about source and target partitions.

## Usage

Download it with the following command: `curl -L -O github.com/thiggy01/clone-linux/raw/master/clone-linux`, give it
execution permission with `chmod +x clone-linux` and run it with root privileges as `sudo ./clone-linux`

After starting the script, you will see a menu asking you to selecte your umounted target boot "/" ext4 partition.

<p align="center"><img src="https://i.imgur.com/X7MVELD.png"></p>

If you have a separate /home partition, it will be detected by the script and you will be promped to select the target
/home partition.

<p align="center"><img src="https://i.imgur.com/p8gpJCw.png"></p>

After you selected the appropriate partitions, the script will mount your target boot partition and show a confirmation
screen with the source and target information, including size, used and available space, etc.

<p align="center"><img src="https://i.imgur.com/JfYyIal.png"></p>

If you press Y or y to proceed, the script starts the cloning process and will show progress and some stats at the end.
When the copying is finished, the script will change the target fstab file in order to mount the corrent clone UUID.
It also changes the UUID from the target grub.cfg file to the clone one and update it to add the menu entry for the 
clone linux system, as shown below:

<p  aligh="center"><img src="https://i.imgur.com/i3QcTXb.gif"></p>

As you could see on the image above, if you selected a target /home partition, a confirmation screen will be
showing information about the source and target home partitions and, if you press y or Y to proceed, it will carry out
almost the same process as before, with exception of not changing the grub configuration file.

Finally, the script will be unmounting your boot and home (if there is one) partitions and cleaning up all temporary files.
The next time you boot your computer, you should see a new grub menu entry for your clone linux distribution and boot it 
normally, as you would with the cloned one.
