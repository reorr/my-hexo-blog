---
title: 'Saya, Pulpstone, dan LUCI'
tags:
  - deadline
  - openwrt
  - pulpstone
categories:
  - Kisah
  - Linux
date: 2017-12-15 22:24:08
---

Pernah suatu hari, saat mengutak-atik _router_ saya, saya me-_flashnya_ dengan Pulpstone LEDE yang tanpa LUCI karena sebelumnya saya bosan dengan Chaos Chalmer dan wifi tak dapat digunakan. Seperti biasa _router_ yang telah di-flash otomatis _reboot_.

Nah, sehabis _reboot_ saya ingin menghubungkannya ke internet lewat wifi tethering dari ponsel. Saya pun membuka browser dan langsung menuju ke 192.168.1.1. Lhadalah, kok ndak ada LUCI? Saya coba cari di situs resmi pulpstone, ternyata harus menginstalnya lewat gigi. Saya unduh file LUCI dan coba untuk _upload_ ke _router_. Ternyata koneksi sftp dari laptop ke router tidak jalan. Setelah saya cari tahu penyebabnya, ternyata paket openssh belum terpasang pada _router_.

Lha terus piye iki? Saat itu saya sedang dikejar deadline, sedangkan laptop saya _port_ usbnya tidak dapat digunakan, sehingga koneksi hanya bisa dengan kabel LAN yang biasanya saya ambil dari _router_. Kepikiran mencoba mem-_flash_ OpenWRT lewat tftpd, namun di laptop saya tidak terpasang paket tersebut, waduh. Jalan lain adalah dengan mengkoneksikan router lewat kabel LAN di Lab. komputer kampus yang tidak mungkin dilakukan karena libur akhir pekan. Akhirnya setelah memeras otak saya menemukan ide brilian. Saya letakkan _image_ Pulpstone CC yang ada LUCI-nya di localhost lalu di-wget oleh router lewat SSH dan di-_flash_. Alhamdulillah, walau agak puyeng karena masih mikir tugas yang belum selesai, akhirnya router bisa berfungsi seperti sebelumnya.