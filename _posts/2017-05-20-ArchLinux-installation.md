---
title               : "ArchLinux 설치"
excerpt             : "ArchLinux 배포판을 가상머신 도구인 VMware를 사용하여 설치하는 법에 대해서 알아봅니다."
last_modifieat_at   : 2017-05-21 09:19:50

toc 				: true
toc_sticky			: true

categories:
 - Linux
---

{: .notice--danger }
**Disclaimer!** 이번에 리눅스 사용해 보는 것이 처음이기 때문에 아직 잘 모르는 부분이 많아 불필요한 패키지도 설치할 가능성이 높습니다.

## 사전 준비

-	가상 데스크톱 환경을 구성하기위해 [VMware workstation player](http://www.vmware.com/products/player/playerpro-evaluation.html)를 설치합니다.
-	[ArchLinux Download](https://www.archlinux.org/download/)에서 iso 미디어 파일을 받아 놓습니다.

## 가상 머신 설정

-	OS 이미지파일을 등록하고 다음을 누른다.

![Step 01]({{ site.imgurl }}posts/archlinux/installation/create-vm-01.png){: .align-center }

-	Linux를 선택하고 버전은 `Other Linux 3.x kernel 64-bit`를 선택한다.

![Step 02]({{ site.imgurl }}posts/archlinux/installation/create-vm-02.png){: .align-center }

-	이름을 설정하고 저장소를 설정해준다.

![Step 03]({{ site.imgurl }}posts/archlinux/installation/create-vm-03.png){: .align-center }

-	사용할 하드 용량을 설정해준다.

![Step 04]({{ site.imgurl }}posts/archlinux/installation/create-vm-04.png){: .align-center }

-	하드웨어를 설정해준다.

![Step 05]({{ site.imgurl }}posts/archlinux/installation/create-vm-05.png){: .align-center }

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

`ArchLinux`는 필수적인 기능을 제외하고는 모두 Mirror site에서 웹으로 다운받아 설치한다. 따라서 더 진행하기 전에 Mirror 리스트를 업데이트 하는 것을 권장한다. 원래는 설치중 `arch.nimukaito.net` 에서 해당 파일을 찾을 수 없다는 오류 메세지가 자꾸 출력되어 이를 없애기 위해서 찾아본 정보이지만 설치 전 Mirror 리스트를 업데이트 해주는 것이 좋다.

```bash
# nano /etc/pacman.d/mirrorlist
```

해당 파일에서 가장 첫번째 항목인 프랑스쪽에서 `arch.nimukaito.net` 부분을 주석처리 해준다.

{: .notice--info}
**Note:** 주석은 # 으로 처리한다.

```bash
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist
```

원본 파일을 복사 후 가장 빠른 6개의 서버만 남겨준다. 해당 명령어를 수행시키면 완료되기까지 오래걸리니 느긋하게 기다려준다.

원본 파일만 복사 후 다음의 내용으로 `mirrorlist`의 내용을 바꿔 주어도 된다. 스크린샷은 `rankmirrors` 명령이 완료된 결과이다.

![Mirror list]({{ site.imgurl }}posts/archlinux/installation/mirrorlist.png){: .align-center}

## ArchLinux 설치

/dev/sda3 파티션에 /mnt 디렉토리를 `mount`시켜준다. `mount`란 어떠한 디렉토리를 디바이스에 올린다는 뜻이다. 다시말하면, /mnt 디렉토리는 /dev/sda3/ 의 물리적 하드디스크 드라이브 장치에 있는 내용으로 채워진다는 뜻이다. 그 후 /mnt 내부에 3개의 디렉토리를 만들어준다.

-	/mnt/boot : 부팅 관련 파일들의 공간. 처음에 파티션을 `bootable`로 나눈 것에 마운트 시킨다.
-	/mnt/var  : 환경 변수에 관련된 공간으로 생각한다.
-	/mnt/home : 사용자의 파일시스템의 최상위 디렉토리가 되는 공간이다.

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

### User 설정

루트 계정에 대해서 비밀번호를 설정해주고 추가로 사용계정을 만들고 `sudoer`로 추가시켜준다. `sudoer`는 `sudo` 명령을 통해 사용자 계정에서 루트권한을 잠시 가질 수 있는 계정이다. 흔히 보는 관리자 계정을 생각하면 될 것 같다.

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

### Grub bios 설치

```bash
# grub-install /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg
```

이후 `exit` 를 입력하여 `bash`를 나간 뒤 `reboot` 으로 재부팅한다.

## 네트워크 설정

```bash
# hostnamectl set-hostname archlinux
# systemctl enable dhcpcd
# systemctl start dhcpcd
// SSH 설치 스킵해도 무방함.
# pacman -S openssh
```

이후 `ip addr`로 확인해보면 ip 가 잡혀있는 것을 확인할 수 있다.

## X packages 설치

```bash
# pacman -S xorg xterm xorg-xclock xorg-twm 
# pacman -S xorg-xinit 
# pacman -S xorg-drivers
```

{: .notice--info }
**Note:** 자료를 찾아보면 `xorg-server-utils`도 설치하라 나와있지만 막상 해당 패키지가 존재하지 않는다고 나온다.

## Open Vm tools 설치

VMware 유틸리티 관련 패키지이다. 해당 패키지를 설치하면 클립보드 공유나 가상머신에 파일을 드래그 앤 드롭으로 넣을 수 있다.

```bash
# pacman -S net-tools gtkmm open-vm-tools
```

## Desktop Environment 설치

### KDE Plasma 5

서비스를 켜주고 재부팅하면 이후 Desktop Environment를 통한 GUI로 부팅된다.

```bash
# pacman -Sy plasma-meta kdebase
# pacman -Sy ttf-freefont
# systemctl enable sddm.service
# reboot
```

### Gnome 3

WaylandEnable=false 부분 주석을 해제하고 재부팅하면 이후 Desktop Environment를 통한 GUI로 부팅된다.

```bash
# pacman -Sy gnome gnome-extra gnome-tweak-tool
# systemctl enable gdm
# nano /etc/gdm/custom.conf
# systemctl enable gdm.service
# reboot
```

## References

-	[How To Quickly: Install Arch Linux 2017 With Gnome in VMWare (3 Minute Tutorial)](https://www.youtube.com/watch?v=m28veKzJcQ4)
-	[ArchLinux Wiki - Mirrors](https://wiki.archlinux.org/index.php/Mirrors#List_by_speed)
-	[Arch Linux 2017.03 Installation + GNOME + Apps + VMware Tools + Review on VMware Workstation [2017]](https://www.youtube.com/watch?v=Nojq2Ihy_3s&t=172s)
-	[Arch Linux 2017 Installation + KDE Plasma 5 + Apps + VMware Tools on VMware Workstation [2017]](https://www.youtube.com/watch?v=L-fNv9QqFfA)