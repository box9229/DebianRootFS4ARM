DebianRootFS4ARM
================

This script can create a ARM Debian Root FileSystem image file automatically.


## Prepare

Before you start, Some packets must be installed in you environment.

    # apt-get install binfmt-support qemu qemu-user-static debootstrap kpartx lvm2 dosfstools

## How to use

    # ./build_debian_arm_rootfs_img.sh img  your_image_file

After run this script, you also need to merge uboot and linux kernel into this image for a bootable image in ARM system.

***

## Note

Here are some things you need to know when you first booting by this image.

- The password for root is "123456"

- Please modify the /etc/network/interface for network settings

- Run 'dpkg-reconfigure locales' to set your language.

- Run 'dpkg-reconfigure tzdata' to set your timezone.

https://blog.haostudio.net/hwp/動手打造debian-root-filesystem-for-arm-2/

動手打造Debian root filesystem for ARM
Posted on 2014-11-06 by hao

一切動力皆來自於 why ?

每次都使用別人做好的image file 來用在自己的ARM 開發板上. 對於別人是如何做出這樣的image file 感到好奇.
於是花了一些時間, 想要動手打造自己開發板上專屬的image file. 上網找了一下, 原本是想從Linux From Scratch著手. 覺得LFS 才是真正從底部打造起, 但是後來想想, 若某個軟體有bug, 想要更新時, 還得從souce code 抓下來, 一個個補上去, 我似乎沒辦法整天都在盯著軟體的漏洞跑. 最後決定採用Debian Distribution, 因為感覺他比較自由. 有漏洞時, 只要用apt 去更新套件就好. 因此動手打造Debian 的Root File System 就成了第一個目標.


後續

但是別太興奮的將這個檔燒到SD Card 或TF Card. 因為這樣還不能夠將 ARM 系統正常開機.

他還缺2的東西, uboot 及kernel. 由於這兩的東西跟你的ARM 開發板有絕對的關係, 因此不同家的板子, 其作法都有些不同
下次有機會, 再來討論如何將uboot 及kernel 整合到這個rootfs.img 檔中, 使它能夠真正的在ARM 板子上開機起來.
關於如何建立Cubieboard 的uboot, 及linux kernel 請參考這篇文章

自動化建立root filesystem 的script

做了上面那麼多的動作後, 應該會覺得很累了. 因此我寫了一個自動化的script 讓上面的所有步驟一氣呵成.可以讓省下許多時間去喝杯咖啡吧.

請到這裡抓取這個自動化的script.


box9229 says:
2016-05-25 at 22:31:03

1 #./update_kernel_to_disk_images.sh img ../DebianRootFS4ARM/rootfs.img output_cb3/kernel/
2 #./update_uboot_to_disk_images.sh img ../DebianRootFS4ARM/rootfs.img output_cb3/uboot/

看了一下 兩個script 試燒到SD Card可以開機了
