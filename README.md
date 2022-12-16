# DDE
This is instructions for how to set up your Linux machine with Deniable Disk Encryption (DDE). In order to do this, we will use plain mode encryption on the whole disk and store grub on a seperate flash drive. Normal grub doesn't support decrypting plain mode so we will need to use a fork of Grub.

## Step 1: Grub with support for plain mode

Years ago, we could simply use [GrubCrypt](http://grub.johnlane.ie/) as it supported plain mode. Unfortunately, it is no longer being updated and doesnt compile so instead we will patch Grub with the following [patch](https://lists.nongnu.org/archive/html/grub-devel/2022-12/msg00046.html).

To do this, first clone Grub (At the time of writing Grub is on commit 7259d55ffcf124e32eafb61aa381f9856e98a708)

```
git clone https://git.savannah.gnu.org/git/grub.git
```

Next, download (or copy/paste) the patch mentioned above and run

```
git apply [filename].patch
```
