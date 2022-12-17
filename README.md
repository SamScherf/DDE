# DDE
This is instructions for how to set up your Linux machine with Deniable Disk Encryption (DDE). In order to do this, we will use plain mode encryption on the whole disk and store grub on a seperate flash drive. Normal grub doesn't support decrypting plain mode so we will need to use a fork of Grub.

## Step 1: Grub with support for plain mode

The fork of Grub we will use for decrypting the drive is [GrubCrypt](http://grub.johnlane.ie/) (There exists other forks and patches one could use however GrubCrypt is what Libreboot uses so that is what we will use). To install GrubCrypt, you can install it from source and compile it or, if you're using an Arch based system, you can install the following [package](https://aur.archlinux.org/packages/grub-luks-keyfile) from the AUR manually or via a AUR-helper like paru:

```
paru -S grub-luks-keyfile
```
