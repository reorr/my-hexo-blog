---
title: How To Enable Fingerprint Scanner on Thinkpad Laptop in Archlinux
tags:
  - archlinux
  - fingerprint
  - t430s
categories:
  - Linux
  - Thinkpad
  - tutorial
featured_image: posts/thinkpad_fingerprint.jpg
date: 2018-08-07 23:00:47
---

Yeah, as a linux user i know how tiring is typing a password each we run command as super user or simply login. Not again, i've purchased Thinkpad T430s with fingerprint scanner, but without setting it up it wont do anything. This is a very brief tutorial how to enable fingerprint scanner in Archlinux system.

1.  Install `fingerprint-gui` from AUR

1.  Make `/lib/udev/rules.d/40-libfprint0-custom.rules` as follows


<pre>
ATTRS{idVendor}=="147e", ATTRS{idProduct}=="2020", MODE="0664", GROUP="plugdev"
</pre>


3.  Add yourself to the plugdev group

<pre>
$ sudo usermod -a -G plugdev username
</pre>

4.  Reboot
5.  Open fingerprint-gui to do the enrolment
6.  Add this line to `/etc/pam.d/sudo`, `/etc/pam.d/su`, `/etc/pam.d/login` and `/etc/pam.d/polkit-1`

<pre>
auth		sufficient		pam_fingerprint-gui.so
</pre>

7.  Try do `$ sudo something` in terminal, you should be able to use your fingerprint for authentication
8.  You can also login in tty with your fingerprint