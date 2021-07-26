# B1: Tạo phân vùng ổ cứng
```sh
lsblk
fdisk /dev/sda
```
Nhập n để tạo phân vùng mới, chọn mặc định đến option thứ 4  
Nhập kích thước cho phân vùng: +nG, n là kích thước , G là gigabyte  
# B2 : Phân vùng ổ cứng
* Phân vùng hệ thống
```sh
mkfs.ext4 /dev/sda1  # tạo phân vùng hệ thống
```
* phân vùng swap
```sh
swapoff -a
mkswap /dev/sda2
swapon /dev/sda2
```

# B3 : cài đặt base linux:
```sh
mount /dev/sda1 /mnt
pacstrap /mnt base linux linux-firmware nano dhcp networkmanager
```
# B4: Config hệ thống arch
```sh
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt
```
# B5: cấu hình thời gian, múi giờ, ngôn ngữ
```sh
ln -sf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime  
hwclock --systohc --utc
# Cấu hình system locale
locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
export LANG=en_US.UTF-8
```
# B6: Cấu hình hostname, password, grub
```sh
# hostname
echo 'huuvuot' > /etc/hostname
echo '127.0.0.1 localhost' > /etc/hosts
# cấu hình password
passwd
# cấu hình grub
pacman -S grub
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
exit
reboot
```

# B7: cài đặt MATE desktop enviroment
* Cấu hình mạng
```sh
systemctl enable NetworkManager.service
systemctl enable dhcp.service
```
* cài đặt môi trường
```sh
pacman -S xorg xorg-server
pacman -S mate mate-extra
pacmam -S lightdm
pacman -S lightdm-gtk-greeter
systemctl enable lightdm.service
reboot
```