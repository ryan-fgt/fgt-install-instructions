Procedure to prepare and install Mint 18.2 (Cinnamon 64 bit) on a scrubbed HDD

Using a USB drive containing Mint 18.2 (preferably without persistence) boot into a live session and open a terminal.

|Steps|Action|Comment|
|--------|--------|--------|
|1.|in a terminal, type `sudo -i` ;<br> press Enter|*CTRL + ALT +T* opens terminal <br>`sudo -i` creates an instance of superuser|
|2.|`lsblk`|to view existing paritions|
|3.|`fdisk /dev/sda`| |
| |`o`|to create DOS table|
| |`w`|to write to disk and exit|
| |`parted /dev/sda`|to edit partition|
| |`unit GiB`|set units to gigabytes|
| |`mkpart primary 0 2`|make 2 GB partition at start of sda|
| |`mkpart primary 2 100%`|make one partition of the rest of sda|
| |`print`|to see parition created|
| |`quit`|to leave parition editor|
|4.|`mkfs -t ext2 /dev/sda1`|to create file system on sda1|
|5.|`pvcreate /dev/sda2`|to create virtual HDD on sda2|
|6.|`vgcreate mint18.2cinn64 /dev/sda2`|to create volume group|
|7.|`lvcreate -L 20G -n root mint18.2cinn64`|to create root partition|
|8.|`lvcreate -L 4G -n swap mint18.2cinn64`|to create swap partition|
|9.|`lvcreate -l 100%FREE -n home mint18.2cinn64`|to create home parition|
|10.|`lsblk`|to view partition created|
|11.|`mkfs -t ext4 /dev/mint18.2cinn64/root`|to create root file system|
|12.|`mkfs -t ext4 /dev/mint18.2cinn64/home`|to create home file system|
|13.|`mkswap /dev/mint18.2cinn64/swap`|to create swap file|
|14.|`dmidecode \| grep "Serial Number"`|to list serial number in BIOS|
| |select, highlight and copy a serial number|to be a unique computer identifier|
|15.|double click on *Install* icon|**Start Mint Installation**|
| |set English language and Continue| |
| |select third party software for installation|Ensure ethernet cable is connected to the computer|
| |select *Something Else*|start partition editor|
| |check for expected boot loader location (HDD) near bottom of window|usually on sda; <br>avoid installation to USB device|
| |select boot partition for *sda1* and use *Change* button to select parameters<br>use as: *ext2*<br>mount point: */boot*|assign file system and mount point, continue through warnings and observe mount point listed|
| |select root partition and use Change button to select parameters<br>use as: *ext4*<br>mount point: */*|assign file system and mount point, continue through warnings & observe mount point listed|
| |select home partition and use Change button to select parameters<br>use as: *ext4*<br>mount point: */home*|assign file system and mount point, continue through warnings & observe mount point listed|
| |do nothing for swap partition| |
| |select *Install Now*| |
| |type `Toronto` & *Continue*|to enter location for time zone|
| |select English US keyboard & *Continue*| |
| |type `Owner`|to identify computer user|
| |clear & paste serial number into computer name|to uniquely identify computer|
| |type password|to assign password|
| |check *Password required to login* & *Continue*|to require password at login|
| |wait for installation to complete| |
| |Select *Restart* & follow prompt to remove USB drive|to restart computer using newly installed operating system on HDD|
