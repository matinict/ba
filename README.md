# BlackArch  Repo


## Booting into BlackArch Live ISO


  
  #check the available disks and partitions:
  lsblk
  df -h /
  #cfdisk /dev/sda
  sudo mkfs.fat -F32 /dev/sda1   # EFI Partition 1GB
  sudo mkfs.ext4 /dev/sda2       # Root Partition 60Gb
  sudo mkfs.ext4 /dev/sda3       # Home Partition 50GB
  
 #Dont Format & Partiion again During Instal 
 blackarch-install

 Boot partition is usually an EFI  sda1, with a size of 100–500 MB.

sudo lsblk -f /dev/sda2
sudo e2fsck -f /dev/sda2

sudo e2fsck -f /dev/sda2
sudo resize2fs /dev/sda2
df -h /

sudo blkid
sudo dumpe2fs /dev/sda2 | grep -i "block count"
sudo blockdev --getsize64 /dev/sda2


