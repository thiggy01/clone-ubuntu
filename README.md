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

* The script must be ran in a terminal with bash shell and have the whiptail package installed.

* You must be cloning from your mounted (live) boot system and mounted home partition.

* You must create empty ext4 partitions large enough to hold your boot and home partitions.

* Your target (clone) partitions must not be mounted before calling the `clone-linux` script.

* When you are recloning, any new data on the previous clone partition will be deleted.

* Before cloning, a confirmation screen is displayed with information about source and target partitions.

## Usage

Download it with the following command: `curl -L -O github.com/thiggy01/clone-linux/raw/master/clone-linux`, give it
execution permission with `chmod +x clone-linux` and run it with root privileges as `sudo ./clone-linux`

After starting the script, you will see a menu asking you to selecte your umounted target boot "/" ext4 partition, as
seen below.
![clone-linux menu](https://i.imgur.com/OY71spK.png)

If you have a separate /home partition, it will be detected by the script and you will be promped to select the target
/home partitiona, as seen below.
![Imgur](https://i.imgur.com/nmAatyQ.png)
