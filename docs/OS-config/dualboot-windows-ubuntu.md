# Dual-boot Windows and Ubuntu
This is a guide for installing Ubuntu on a separate drive from Windows with each OS having their own EFI partition. It assumes Windows 11 is already installed.

Despite choosing a drive to install Ubuntu (and other distros) on, the installer may write EFI data to another drive, such as the drive where Windows is installed. This is problematic because Windows is known to overwrite any boot information that isn't Windows, making booting into Linux impossible. To avoid this, we do a few things to make sure that Ubuntu gets its own EFI partition on its own disk, separate from the Windows EFI partition.

## Preliminary steps
### UEFI settings
Make sure that these features are disabled:

- Fast boot: disabled
- Any option related to booting to Windows: disabled or "Other OS"

### Windows settings
Windows has a feature called "fast startup" which can cause issues with other operating systems present. To disable this:

In Power Options :material-arrow-right: "Choose what the power buttons do" :material-arrow-right: "Change settings that are currently unavailable"

- "Turn on Fast startup": disabled

Windows and Linux have different ways of measuring time, which can cause Windows have the wrong time after a Linux session. One way fix this is syncing with the time servers shortly after login:

Run `services.msc`

- For service: Windows Time (`w32time`), set Startup type: Automatic

## Installing Ubuntu on a separate drive with its own EFI partition

Step 1: Flash Ubuntu to USB drive and boot into it

Step 2: Run terminal with `CTRL+ALT+T`

Step 3: Login as root
 ```
 sudo su -
 ```

Step 4: List disks. Find the disk where Windows is installed, e.g. `/dev/nvme1n1`
```
fdisk -l
```

Step 5: Run `parted` on Windows disk, e.g. `nvme1n1`

```
parted /dev/nvme1n1
```

Step 6: Print partitions. Find the Windows EFI partition. This is likely the only one with `fat32` file system, e.g. partition number `1` or `/dev/nvme1n1p1`. This partition should have the `boot` flag enabled
```
p
```

Step 7: Remove the `boot` flag in the Windows EFI partition
```
set 1 boot off
```

Step 8: Print partitions again to confirm the flag is absent from partition number `1`'s list of flags
```
p
```

Step 9: Quit `parted` and close the terminal
```
q
exit
```
Step 10: Install Ubuntu on other disk, e.g. `nvme0n1`

- Disk setup: Erase disk and install Ubuntu
- Installation disk: `nvme0n1`
- Applications: Default selection
- Proprietary software: Codecs & drivers

If you didn't manually create any partitions, the automatically created ones should be something like:

- partition `nvme0n1p1` formatted as `fat32` used for `boot/efi`
- partition `nvme0n1p2` formatted as `ext4` used for `/`

Step 11: Login to Ubuntu and run terminal with `CTRL+ALT+T`

Step 12: Login as root
 ```
 sudo su -
 ```

Step 13: Run `parted` on Windows disk, e.g. `nvme1n1`

```
parted /dev/nvme1n1
```

Step 14: Print partitions. Find the Windows EFI partition. This is likely the only one with `fat32` file system, e.g. partition number `1` or `/dev/nvme1n1p1`. This partition should have the `boot` flag disabled
```
p
```

Step 15: Re-enable the `boot` flag in the Windows EFI partition
```
set 1 boot on
```

Step 16: Print partitions again to confirm the flag is present in partition number `1`'s list of flags
```
p
```

Step 17: Quit `parted`
```
q
```

Step 18: Restart. In your UEFI boot order, set Windows to be first priority and Ubuntu to be second (or whichever you prefer)

Step 19: Login to either OS by using the UEFI boot menu and making a selection

## Enabling GRUB (recommended)
It's a good idea to have a bootloader. In the event of a broken install, you can easily access a live recovery partition already on your disk (if your distro does this, it appears that Ubuntu doesn't) via GRUB without needing to create another live ISO.

Step 1: While logged in as root, edit this file
```
nano /etc/default/grub
```
Step 2: Uncomment or add the line
```
GRUB_DISABLE_OS_PROBER=false
```
and `CTRL+O` to write and then `CTRL+X` to exit

Step 3: Run the prober. It should recognize the Windows Boot Manager on your Windows disk, e.g. `nvme1n1`
```
os-prober
```

Step 4: Make the grub configuration file. It should find the Linux images and the Windows Boot Manager
```
grub-mkconfig -o /boot/grub/grub.cfg
```

Step 5: Confirm bootloader information was installed on the other drive, e.g. `nvme0n1`. Check that filesystem `/dev/nvme0n1p1` is mounted on `/boot/efi`
```
df
```
Step 6: You should see directories `BOOT` and `ubuntu`
in `/boot/efi/EFI/`
```
cd /boot/efi/EFI
ls -la
```
Step 7: In your UEFI boot order, set Windows to be first priority and Ubuntu to be second (or whichever you prefer)

Step 8: Login to either OS by using the UEFI boot menu and making a selection

## Credit
Separate EFI info adapted from KMDTech's excellent [video guide](https://youtu.be/KX85vZ3ANVk?si=LgnHuwgjv6mnfiCW)
