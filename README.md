# BlackArch  Repo


##Enable networking:

    systemctl enable dhcpcd
    systemctl enable NetworkManager
    # Restart Networking Services
    systemctl restart NetworkManager
    ping -c 4 google.com
    ping -c 4 8.8.8.8



## Booting into BlackArch Live ISO TO HDD
  
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

  ## Create Bash
    sudo nano bau.sh
    
    #!/bin/bash

    # Update package database first
    sudo pacman -Syy

    # Get the full package list
    pkg_list=$(pacman -Qq)
    total_pkgs=$(echo "$pkg_list" | wc -l)

    # Loop through packages in batches of 100
    for i in $(seq 0 100 $total_pkgs); do
        batch=$(echo "$pkg_list" | sed -n "$((i+1)),$((i+100))p")
        if [[ -n "$batch" ]]; then
            sudo pacman -Syu --overwrite='*' --noconfirm --needed $batch
        fi
    done


    chmod +x batch_update.sh
    sudo ./batch_update.sh
    chmod +x bau.sh
    sudo ./bau.sh



## Ref



