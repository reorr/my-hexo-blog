---
title: Warnai Desktop Otomatis dengan xfcolorizer
tags:
  - gtk
  - pyhon
  - Ricing
  - xfwm
categories:
  - Alat
  - Destop
  - Linux
featured_image: posts/xfcolorizer-01.png
date: 2017-06-06 09:12:57
---

Ceritanya saya suka modding desktop, tapi lama kelamaan bosen tema yang ada cuma itu-itu saya. Saya menggunakan lingkungan destop xfce yang tidak mendukung perubahan warna jendela otomatis sesuai dengan warna latar belakang. Setelah saya menjelah, saya menemukan tema yang enak untuk tampilah sehari-hari, namun, ya itu tadi, hanya ada beberapa fork dari tema tersebut, sehingga kurang mendukung warna dari latar belakang. Jalan satu-satunya adalah dengan mengedit file tema yang sudah ada, dan jika setiap ganti latar belakang haru mengedit lagi, pastilah tidak efisien. Terpikirlah ide untuk membuat alat yang memudahkan untuk menyesuaikan warna tema gtk dan xfwm dengan skema warna latar belakang, maka rilis lah xfcolorizer.

Xfcolorizer merupakan alat berbasis bahasa python dan bash yang secara otomatis menyesuaikan warna tema sesuai warna gambar pilihan. Xfcolorizer akan mengubah tema xfcolorize yang merupakan fork dari adapta. Dengan menggunakan alat ini, maka kita tidak usah susah-susah mengedit file tema, sehingga orang awam pun bisa menggunakannya. Ada beberapa dependensi yang harus dipasang sebelum menggunakan alat ini, yaitu:

1. Inkscape
2. python3
3. colorthief
 
Inkscape dan python3 dapat dipasang dari repo masing-masing distro, sedangkan untuk color thief, dapat dipasang menggunakan perintah

```
$ pip install colorthief
```

Perintah yang digunakan untuk menjalankan xfcolorizer adalah

```
$ python3 xfcolorizer -i /direktori/menuju/gambar.jpg
```

Selain itu, jika kita ingin menggunakan warna pilihan kita untuk warna jendela dan panel, dapat menggunakan perintah

```
$ python3 xfcolorizer -i /direktori/menuju/gambar.jpg/png -w "hex warna pilihan"
```

Setelah itu alat ini akan berjalan untuk mengubah warna dan menerapkan tema dan latar belakang secara otomatis, tunggu sebentar karena saat mengubah tema gtk perlu dilakukan perenderan aset-aset.

Taraaa!!! Destopmu sudah terwarnai sesuai dengan warna latar belakang.

### Tangkapan Layar

<div align="center">
![01](/images/posts/xfcolorizer-01.png)
![01](/images/posts/xfcolorizer-02.png)
![01](/images/posts/xfcolorizer-03.png)
![01](/images/posts/xfcolorizer-04.png)
![01](/images/posts/xfcolorizer-05.png)
![01](/images/posts/xfcolorizer-06.png)
</div>

Xfcolorizer bisa diunduh dari github saya [di sini](https://github.com/reorr/xfcolorizer).

### Edit
Tertanggal tanggal 29 Desember 2018, lumbung xfcolorizer saya _archive_-kan. Saya tidak ada niatan untuk me-_maintenance_ proyek tersebut. Namun jangan sedih, saya punya proyek baru yang bernama "warnai" yang fungsinya lebih yahud daripada xfcolorizer.

warnai dapat diunduh dari tautan [ini](https://github.com/reorr/warnai).