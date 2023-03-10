# Deniable Disk Encryption (DDE)
This is instructions for how to set up your Linux machine with Deniable Disk Encryption. In order to do this, we will use plain mode encryption on the whole disk and store grub on a seperate flash drive. Normal grub doesn't support decrypting plain mode so we will need to use a fork of Grub.

## Step 1: Prepare the USB drive

To make your encryption more deniable, it's recommended to store Grub elsewhere (such as a removeable USB drive). To do this, wipe your USB drive and create a single EFI parition for UEFI systems or a single "BIOS boot" parition for BIOS systems. For very optimized setups, this parition can be as small as 10mb however since my USB drive is only for Grub, I will make my pariton this size of the entire drive. If you're unsure what size to use, I recommend the whole drive or at least 512 MiB.

Next format as FAT 32 like so:

```
mkfs.fat -F 32 /dev/sdxY
```
where x is the drive letter and Y is the parition number (likely 1).

## Step 2: Install Grub on the system

Next we need to install grub on our system to get the tool grub-install. The fork of Grub we will use that supports plain mode encryption is [GrubCrypt](http://grub.johnlane.ie/) (There exists other forks and patches one could use however GrubCrypt is what Libreboot uses so that is what we will use). To install GrubCrypt, you can install it from source and compile it or, if you're using an Arch based system, you can install the following [package](https://aur.archlinux.org/packages/grub-luks-keyfile) from the AUR manually or via a AUR-helper like paru:

```
paru -S grub-luks-keyfile
```

## Step 3: Install Grub on the USB drive

Now that we've prepared a USB drive and installed grub, it's time to install Grub on the USB drive. 

To do this, first mount the drive:

```
mount /dev/sdxY /mnt
```

And then run grub-install with the following parameters for UEFI systems:

```
grub-install --efi-directory=/mnt --removable
```

Or with the following paramters for BIOS systems:

```
grub-install --boot-directory=/mnt /dev/sdy
```

For more infomation on this see the Arch Wiki page [GRUB/Tips and Trick](https://wiki.archlinux.org/title/GRUB/Tips_and_tricks#Alternative_installation_methods)
