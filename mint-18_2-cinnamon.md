Procedure to prepare and install Mint 18.2 (Cinnamon 64 bit) on a scrubbed HDD

Using a USB drive containing Mint 18.2 (preferably without persistence) boot into a live session and open a terminal.

|Steps|Action|Comment|
|--------|--------|--------|
| 1.|in a terminal, type `sudo -i` ;<br> press Enter|*CTRL + ALT +T* opens terminal <br>`sudo -i` creates an instance of superuser|
|2.|`lsblk`|to view existing paritions|
|3.|`fdisk /dev/sda`| |
|4.|`o`|to create DOS tables|
|5.|`w`|to write to disk and exit|
|6.|`parted /dev/sda`|to edit partition|
|7.|`unit GiB`|set units to gigabytes|
|8.|`mkpart primary 0 2`|make 2 GB partition at start of sda|
|9.|`mkpart primary 2 100%`|make one partition of the rest of sda|
|10.|`print`|to see parition created|
|11.|`quit`|to leave parition editor|
|12.|`mkfs -t ext2 /dev/sda1`|to create file system on sda1|
|13.|`pvcreate /dev/sda2`|to create virtual HDD on sda2|
|14.|`vgcreate mint18.2cinn64 /dev/sda2`|to create volume group|
|15.|`lvcreate -L 20G -n root mint18.2cinn64`|to create root partition|
|16.|`lvcreate -L 4G -n swap mint18.2cinn64`|to create swap partition|
|17.|`lvcreate -l 100%FREE -n home mint18.2cinn64`|to create home parition|
|18.|`lsblk`|to view partition created|
|19.|`mkfs -t ext4 /dev/mint18.2cinn64/root`|to create root file system|
|20.|`mkfs -t ext4 /dev/mint18.2cinn64/home`|to create home file system|
|21.|`mkswap /dev/mint18.2cinn64/swap`|to create swap file|
|22.|`dmidecode | grep “Serial Number”`|to list serial number in BIOS|
|23.|select, highlight and copy a serial number|to be a unique computer identifier|
|24.|double click on *Install* icon|**Start Mint Installation**|
|25.|set English language and Continue| |
|26.|select third party software for installation|Ensure ethernet cable is connected to the computer|
|27.|select *Something Else*|start partition editor|
|28.|check for expected boot loader location (HDD) near bottom of window|usually on sda; <br>avoid installation to USB device|
|29.|select boot partition for *sda1* and use *Change* button to select parameters<br>use as: *ext2*<br>mount point: */boot*|assign file system and mount point, continue through warnings and observe mount point listed|
|30.|select root partition and use Change button to select parameters<br>use as: *ext4*<br>mount point: */*|assign file system and mount point, continue through warnings & observe mount point listed|
|31.|select home partition and use Change button to select parameters<br>use as: *ext4*<br>mount point: */home*|assign file system and mount point, continue through warnings & observe mount point listed|
|32.|do nothing for swap partition| |
|33.|select *Install Now*| |
|34.|type `Toronto` & *Continue*|to enter location for time zone|
|35.|select English US keyboard & *Continue*| |
|36.|type `Owner`|to identify computer user|
|37.|clear & paste serial number into computer name|to uniquely identify computer|
|38.|type password `1Password!`|to assign password|
|39.|check *Password required to login* & *Continue*|to require password at login|
|40.|wait for installation to complete| |
|41.|Select *Restart* & follow prompt to remove USB drive|to restart computer using newly installed operating system on HDD|
