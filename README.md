# clone-linux

This is a tool to clone your mounted boot system "/" and your mounted home "/home" partition, if there is one, into 
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

* You must create empty ext4 partitions large enough to hold your linux distro partitions.

* Your target (clone) partitions must not be mounted before calling the `clone-linux` script.

* When you are recloning, any new data on the previous clone partition will be deleted.

* Before cloning, a confirmation screen is displayed with information about source and target partitions.
