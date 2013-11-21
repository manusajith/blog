---
layout: post
title: Restore/recover grub2 after reinstalling Windows XP/Vista/7
tags:
- codingarena
- grub
- Linux
- manu
- neo
- server
- ubuntu
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
After reinstalling Windows in the computer dual boot with both Windows and Ubuntu Linux,you need restore grub because mbr has been rewritten. This tutorial shows how to restore grub 2.

##1).Using grub4dos##
First download grub4dos from <a title="click to download grub4dos" href="http://download.gna.org/grub4dos/" target="_blank">here</a>.<br>

1. For XP user,<br>
copy the file grldr (without quotes) from grub4dos package to 
C:\ <br>
Edit boot.ini  (hidden file in C:\ ) and add this line to the file:
<pre>C:\grldr="grub4dos"</pre>
For Vista/win7 user,copy the file grldr,grldr.mbr to C:\.Create boot.ini file in the root directory of C:\,copy and paste following into this file.
<pre>[boot loader]
timeout=0
default=c:\grldr.mbr
[operating systems]
C:\grldr.mbr="Grub4Dos"</pre>
2.Now,create menu.lst in root directory of C:,its content:
<pre>timeout 0
default 0
title grub2
find --set-root /boot/grub/core.img
kernel /boot/grub/core.img
boot</pre>
Restart computer,and select boot from Grub4Dos.Then select boot up Ubuntu in grub menu.
Once login,use this command to install grub into mbr:
<pre>sudo grub-install /dev/sda</pre>
##2).Using Ubuntu 9.10 livecd or higher##
Here assuming the Ubuntu partition is sda7,and /boot partition is sda6 (if you have a separate /boot partition).
Boot up ubuntu from the livecd,open terminal and run:
<pre>sudo -i
mount /dev/sda7 /mnt
mount /dev/sda6 /mnt/boot  #skip this one if not have a separate /boot partition
grub-install --root-directory=/mnt/ /dev/sda</pre>
If you miss grub.cfg file,use following to recreate:
<pre>mount --bind /proc /mnt/proc
mount --bind /dev /mnt/dev
mount --bind /sys /mnt/sys
chroot /mnt update-grub
umount /mnt/sys
umount /mnt/dev
umount /mnt/proc
exit</pre>
##3).Using the cd/usb boot up with grub##
Boot up the cd/usb,press c in grub menu.Type:
<pre>grub&gt;find /boot/grub/core.img
grub&gt;root (hdx,y)   (previous command will output the x,y)
grub&gt;kernel /boot/grub/core.img
grub&gt;boot</pre>
After the boot command,you'll go into grub2 menu.Select to boot up ubuntu,and run this command to restore grub:
<pre>sudo grub-install /dev/sda</pre>
--

<a title="Neo" href="http://facebook.com/manusajith" target="_blank">Manu</a>

<a title="Codingarena" href="http://codingarena.in" target="_blank">http://codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>