# Kali Linux Live USB Persistence

Kali Linux "Live" has two options in the default boot menu which enable persistencs— the preservation of data on the “Kali Live” USB drive — across reboots of “Kali Live”. This can be an extremely useful enhancement, and enables you to retain documents, collected testing results, configurations, etc., when running Kali Linux “Live” from the USB drive, even across different systems. The persistent data is stored in its own partition on the USB drive, which can also be optionally LUKS-encrypted.

![](https://i.loli.net/2019/04/07/5ca951194f475.png)

## DD Live OS

```
dd if=kali-linux-2019.1a-amd64.iso of=/dev/sdc bs=512k
```

## Live USB Persistence

```
# select USB partitions
fdisk -l

# create and format an additional partition on the USB drive
# it'll auto calculate the space of USB Image, about 3gb
# and then $start will be start
end=26gb
read start _ < <(du -bcm kali-linux-2019.1a-amd64.iso | tail -1); echo $start
parted /dev/sdc mkpart primary $start $end


# create an ext3 file system in the partition and label it “persistence
mkfs.ext3 -L persistence /dev/sdc3
e2label /dev/sdc3 persistence

# create a mount point
mkdir -p /mnt/my_usb
mount /dev/sdc3 /mnt/my_usb
echo "/ union" > /mnt/my_usb/persistence.conf
umount /dev/sdc3
```

## Live USB Persistence with LUKS Encryption

```
end=7gb
read start _ < <(du -bcm kali-linux-2019.1a-amd64.iso | tail -1); echo $start
parted /dev/sdc mkpart primary $start $end

cryptsetup --verbose --verify-passphrase luksFormat /dev/sdc3
cryptsetup luksOpen /dev/sdc3 my_usb

mkfs.ext3 -L persistence /dev/mapper/my_usb
e2label /dev/mapper/my_usb persistence

mkdir -p /mnt/my_usb
mount /dev/mapper/my_usb /mnt/my_usb
echo "/ union" > /mnt/my_usb/persistence.conf
umount /dev/mapper/my_usb

# if want to close the encrypted channel to our persistence partition
cryptsetup luksClose /dev/mapper/my_usb
```