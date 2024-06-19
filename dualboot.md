well, in here i am gonna write about how to manage the instalation with archlinux and windows 11, without windows 11 being an asshole, i can't do anything to make Win11 less annoying
First of all, i am absolute non-expert but tech-savvy so, i am gonna just do it, fuck it and doing again


I dont like vanilla Windows, it so much bloatware, i love WinterOS by [Mauro Cerqueiro](https://www.youtube.com/@WinterOS/videos), in this Guide i am gonna install Rev12

First Boot Windows installer, make a 100GB Partition and install Windows in that partition, like a normal install
When Windows is installed, reboot and install archlinux from [installation.md](/installation-guide.md)

and that is, ITS NICE RIGHT

I like [this](https://www.youtube.com/watch?v=NxqU1G8hKWk) Guide

Microsoft need to be a monopoly because there are no reason to use Windows, screwing everything, there is no reason to blame linux, is a windows thing.

To solve cluster 0 and no kernel loading problems, atomic solution is
1. Boot Arch Live USB
2. Connect to internet
3. `lsblk`, detect your `/boot` partition
4. `cdisk /dev/your-disk`, and delete your old `/boot` partition and do again
5. `mkfs.vfat -F 32 -S 4096 /dev/your-disk-partition`
7. mount `/` disk in `/mnt` and `/boot` disk in `/mnt/boot`
8. `arch-chroot /mnt`
9. `blkid` and replace your old boot UUID with the new boot UUID 
10. `pacman -Syu grub linux linux-firmware linux-headers intel-ucode dkms systemd`
11. `grub-install --target=x86_64-efi --efi-directory=/boot/ --bootloader-id=GRUB --modules="tpm" --disable-shim-lock --removable --recheck`
12. `grub-mkconfig -o /boot/grub/grub.cfg`
13. `exit`
14. `umount -R /mnt`
15. `reboot`

EUFI Config, Note, my notebook is [Aspire575G](https://wiki.archlinux.org/title/Acer_Aspire_E5-575), so have boot problems
1. add password to access to bios
2. delete all .efi entries
3. exit bios, and enter again
4. enter grub.efi entry
5. delete password to access bios
6. Boot Arch

Now you can select Archlinux and boot right, now you can do `grub-mkconfig -o /boot/grub/grub.cfg` and discover Windows Partition

Its so frustating, i really hate windows
