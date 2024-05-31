well, in here i am gonna write about how to manage the instalation with archlinux and windows 11, without windows 11 being an asshole
First of all, i am absolute non-expert but tech-savvy so, i am gonna just do it, fuck it and doing again


I dont like vanilla Windows, it so much bloatware, i love WinterOS by [Mauro Cerqueiro](https://www.youtube.com/@WinterOS/videos), in this Guide i am gonna install Rev12

First, boot archlinux liveiso, delete all, and make uefi partition with CFDISK, with 200gb, next, shutdown, boot Windows installer and choose that partition, with this i make shure that is booted next in UEFI, i dont trust windows, you know

When Windows is installed, reboot and install archlinux from [installation.md](/installation-guide.md)

and that is, ITS NICE RIGHT

I like [this](https://www.youtube.com/watch?v=NxqU1G8hKWk) Guide

Windows tend to monopoly, so need to screw everything that not even control, that is grub, for me is "Recheck Disk Countdown" from Windows 11, i need to boot live iso, connect to internet, mount /mnt and /mnt/boot/.
Next 'arch-chroot /mnt', and update the system, next execute instalation of grub and redo mkinitcpio