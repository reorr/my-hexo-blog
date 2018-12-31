---
title: Flash TL-MR3420 v2 Dengan Openwrt Chaos Calmer
tags:
  - chaos calmer
  - mr3420
  - openwrt
  - router
categories:
  - tutorial
date: 2017-07-13 10:38:04
---
<div align="center">
![header post](/images/posts/flash_mr3420.png)
</div>
Pertama-tama kita siapkan dulu alat dan bahannya

1.  Router TP-LINK TL-MR3420 V2
2.  Komputer/Laptop/Smartphone
3.  Firmware openwrt chaos calmer (jika sudah punya)
4.  Kopi/Teh/Sirup sisa lebaran kemarin (opsional)
5.  Cemilan (opsional)

  Jika semua hal di atas sudah disiapkan, mari kita langsung eksekusi cara flash openwrt pada perangkat TL-MR3420 V2.

6.  Jika belum punya firmware openwrt chaos calmer, bisa anda unduh di [sini](https://wiki.openwrt.org/toh/tp-link/tl-mr3420), pilih yang openwrt-15.05.1-ar71xx-generic-tl-mr3420-v2-squashfs-factory.bin. jangan pilih yang sysupgrade.bin, nanti saya kasih tahu alasannya.
7.  Sambungkan komputer dengan router.
8.  Pastikan sambungan terhubung dengan baik, dengan cara ping ke 192.168.0.1
9.  Buka browser favorit anda, lalu masuk ke router dengan mengetikkan 192.168.0.1 pada address bar dan tekan enter.
10.  Masuk ke bagian system tools > firmware upgrade, pilih firmware yang sudah diunduh tadi.

![screenshot_2017-07-10_14-23-35.png](/images/posts/screenshot_2017-07-10_14-23-35.png)

![screenshot_2017-07-10_14-24-17.png](/images/posts/screenshot_2017-07-10_14-24-17.png)

11.  Klik tombol upgrade dan tunggu sampai router restart.

![screenshot_2017-07-10_14-24-24.png](/images/posts/screenshot_2017-07-10_14-24-24.png)

12.  Untuk mengecek apakah sudah terpasang openwrt coba ping ke 192.168.1.1, jika sukses berarti anda berhasil.
13.  Taraa… router anda telah terpasang openwrt, selamat mengoprek.

P: Lo… kok… hmmm… perasaan di langkah ke lima ada yang salah deh, kok yang dipilih malah yang upgrade, bukan factory?

S: Nah, ini pertanyaan yang saya tunggu dari jaman batu. Entah lagi ngantuk atau kesambet, saya salah flash yang sysupgrade, seharusnya jika masih memakai firmware original, maka kita harus menggunakan yang factory. Image sysupgrade digunakan bila router sudah dalam posisi terpasang openwrt/ddwrt.

P: Terus, itu routernya nggak papa? Nggak ngebrik?

S: Tenang saja, kalo salah firmware seperti saya masih bisa diakses kok routernya, coba masuk ke 192.168.1.1 lewat browser, nanti bakalan masuk ke LuCI. Masalahnya adalah setelah router direstart, semua settingan akan kembali ke default, mau dioprek gimana aja ya bakalan balik lagi ke awal.

P: Nah lo, cara benerinnya gimana tuh?

S: Gampil bgt deh, caranya masuk ke LuCI dulu, habis itu di menu System pilih Backup/Flash Firmware. Nah kita browse file yang sysupgrade, karena router kita sudah terpasang openwrt. Klik tombol Flash Image, dan tunggu sampai router reboot. Insyaallah router kita sudah sehat dan sudah terpasang openwrt dengan semestinya. 

P: Wuih… otw flash openwrt gan!!!

S: Monggo, bila ada keluhan silahkan hubungi dokter terdekat saya melalui komentar/pm akun facebook saya.   Keterangan P = Penanya (tokoh fiktif) S= Saya (aku, ingsung, kula, abdi, me, boku, ore, watashi)