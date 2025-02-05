Setting up a M2 SSD to your raspberry pi 5

Setup used in writing this:
- Raspberry Pi 5 with Kali Linux
- Geekworm X1001 PCIe to M2 Hate (key-m)
- Patriot P320 256GB NVMe PCIe Gen 3x4 - M.2 2280



Enable PCIe on the Raspberry Pi 5
1. Edit the Configuration File
  -	Open a terminal on your Raspberry Pi.
  -	Edit the config.txt file in the /boot directory:
      sudo nano /boot/config.txt
2. Add PCIe Parameters
  -	Add the following line to enable the PCIe interface:
      dtparam=pciex1
  -	To force PCIe Gen 3 speeds, add:
      dtparam=pciex1_gen=3
  -	Save the file and exit the editor:
      In Nano, press Ctrl+X, then Y, and Enter.
3. Reboot the Raspberry Pi
  - Reboot your device to apply the changes:
     sudo reboot

Mount the M.2 SSD
1. Identify the SSD
  - After rebooting, verify the SSD is recognized by listing connected storage devices:
   lsblk
  - Look for your SSD, which might appear as /dev/nvme0n1 or similar.
2. Create a Mount Point
  - Create a directory to mount the SSD:
    sudo mkdir /mnt/ssd

Reformatting the M.2 SSD
1. Create a New Filesystem
  - Format the SSD with the desired filesystem. For ext4:
    sudo mkfs.ext4 /dev/nvme0n1p1
  - For other filesystems like NTFS or FAT32, replace ext4 with ntfs or vfat.
2. Mount the Reformatted Partition
  - Ensure a mount point exists (if not already created):
    sudo mkdir /mnt/ssd
3. Mount the newly formatted partition:
    sudo mount /dev/nvme0n1p1 /mnt/ssd

Automate Mounting on Boot
1. Edit the fstab file to enable automatic mounting:
    sudo nano /etc/fstab
2. Add this line:
   /dev/nvme0n1p1 /mnt/ssd ext4 defaults 0 2
3. Save and exit the editor.


Verify the Setup
1. Reboot your Raspberry Pi:
   sudo reboot
2. After reboot, confirm the SSD is mounted:
   df -h
