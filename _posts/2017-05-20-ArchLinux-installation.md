---
layout: single
title: "ArchLinux 설치"
excerpt: "ArchLinux 배포판을 가상머신 도구인 VMware를 사용하여 설치하는 법에 대해서 알아봅니다."
last_modifieat_at: 2017-05-20 08:58:18

tags:
 - Linux
---

{% include toc %}

{: .notice--danger }
**Disclaimer!** 이번에 리눅스 사용해 보는 것이 처음이기 때문에 아직 잘 모르는 부분이 많아 불필요한 패키지도 설치할 가능성이 높습니다.

## 사전 준비

-	가상 데스크톱 환경을 구성하기위해 [VMware workstation player](http://www.vmware.com/products/player/playerpro-evaluation.html)를 설치합니다.
-	[ArchLinux Download](https://www.archlinux.org/download/)에서 iso 미디어 파일을 받아 놓습니다.

## 가상 머신 설정

-	OS 이미지파일을 등록하고 다음을 누른다.

![Step 01]({{ site.url }}{{ site.imgurl }}ArchLinux/Installation/create-vm-01.PNG){: .align-center }

-	Linux를 선택하고 버전은 `Other Linux 3.x kernel 64-bit`를 선택한다.

![Step 02]({{ site.url }}{{ site.imgurl }}ArchLinux/Installation/create-vm-02.PNG){: .align-center }

-	이름을 설정하고 저장소를 설정해준다.

![Step 03]({{ site.url }}{{ site.imgurl }}ArchLinux/Installation/create-vm-03.PNG){: .align-center }

-	사용할 하드 용량을 설정해준다.

![Step 04]({{ site.url }}{{ site.imgurl }}ArchLinux/Installation/create-vm-04.PNG){: .align-center }

-	하드웨어를 설정해준다.

![Step 05]({{ site.url }}{{ site.imgurl }}ArchLinux/Installation/create-vm-05.PNG){: .align-center }

## Partition 설정

가상 머신을 켜고 파티션 설정부터 해준다.

```bash
// 파티션 정보 확인
# fdisk -l
// 파티션 설정
# cfdisk /dev/sda
```

총 3개의 파티션으로 나눈다.

1.	1G 크기의 Bootable 파티션
2.	2G 크기의 swap 타입 파티션
3.	남은 크기의 파티션

파티션 설정이 끝나면 변경사항을 저장하고 나간다.

다음의 명령어를 입력하여 포맷한다.

```bash
# mkfs.ext4 /dev/sda1
# mkswap /dev/sda2
# swapon /dev/sda2
# mkfs.ext4 /dev/sda3
```

## Mirrorlist 수정

설치중 `arch.nimukaito.net` 에서 해당 파일을 찾을 수 없다는 오류 메세지가 자꾸 출력된다. 이를 방지하기 위해서 다음의 명령어로 mirrorlist 를 수정해준다.

```bash
# nano /etc/pacman.d/mirrorlist
```

해당 파일에서 `arch.nimukaito.net` 부분을 주석처리 해준다.
당연하지만 한국 기준으로는 카이스트쪽 서버가 가장 빠르다.

```bash
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist
```

원본 파일을 복사 후 가장 빠른 6개의 서버만 남겨준다.

## ArchLinux 설치

```bash
# mount /dev/sda3 /mnt
# mkdir /mnt/boot /mnt/var /mnt/home
# mount /dev/sda1 /mnt/boot
# pacstrap /mnt base base-devel
```

## 바이오스 설치

```bash
# pacstrap /mnt grub-bios
# genfstab -p /mnt >> /mnt/etc/fstab
# arch-chroot /mnt
# hwclock --systohc --utc
# mkinitcpio -p linux
```

## User 설정

```bash
# passwd root
# useradd -m -g users -G wheel -s /bin/bash username
# nano /etc/sudoers

##
## User privilege specification
##
root ALL=(ALL) ALL
username ALL=(ALL) ALL
```

## Grub bios 설치

```bash
# grub-install /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg
```

이후 `exit` 를 두 번 입력하여 나간 뒤 `reboot` 으로 재부팅한다.

## 네트워크 설정

```bash
# hostnamectl set-hostname archlinux
# ip addr
# systemctl enable dhcpcd
# systemctl start dhcpcd
# pacman -S openssh
```

## X packages 설치

```bash
# pacman -S xorg xterm xorg-xclock xorg-twm 
# pacman -S xorg-xinit 
# pacman -S xorg-drivers net-tools gtkmm open-vm-tools
```

{: .notice--info }
**Note:** 자료를 찾아보면 `xorg-server-utils`도 설치하라 나와있지만 막상 해당 패키지가 존재하지 않는다고 나온다.

```bash
# systemctl enable gdm
# nano /etc/gdm/custom.conf
```

WaylandEnable=false 부분 주석 해제.

## Gnome 설치

```bash
# pacman -Sy gnome gnome-extra gnome-tweak-tool
```

## 기본적인 어플 설치

```bash
# pacman -Sy firefox qt4 vlc gimp libreoffice flashplugin
```

## 마무리

```bash
# systemctl enable gdm.service
# reboot
```

이후 Gnome을 이용한 GUI로 부팅된다.

## References

-	[How To Quickly: Install Arch Linux 2017 With Gnome in VMWare (3 Minute Tutorial)](https://www.youtube.com/watch?v=m28veKzJcQ4)
-	[ArchLinux Wiki - Mirrors](https://wiki.archlinux.org/index.php/Mirrors#List_by_speed)
-	[Arch Linux 2017.03 Installation + GNOME + Apps + VMware Tools + Review on VMware Workstation [2017]](https://www.youtube.com/watch?v=Nojq2Ihy_3s&t=172s)