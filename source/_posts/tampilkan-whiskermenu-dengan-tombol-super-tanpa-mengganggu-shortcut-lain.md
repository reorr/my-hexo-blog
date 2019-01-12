---
title: Tampilkan Whiskermenu Dengan Tombol Super Tanpa Mengganggu Shortcut Lain
tags:
  - archlinux
  - xfce
categories:
  - Destop
  - Linux
featured_image: posts/xcape+whiskermenu.png
date: 2017-09-11 08:23:59
---

Ya, benar, saya menulis tulisan ini semata-mata sebagai reminder bagi diri sendiri. Sudah lama saya menggunakan cara ini, namun setiap kali sehabis instal ulang, saya selalu lupa dan harus mengubek-ubek internet lagi. Tombol super pastinya sangat penting bagi kamu yang terbiasa dengan shortcut pada sistem operasi windows seperti kombinasi ```w+e``` yang akan membuka explorer, ```w+r``` yang akan membuka program run, dan lain-lain. Pun setelah saya bermigrasi ke linux. Kebiasaan itu tidak akan hilang dengan mudah, banyak sekali shorcut yang saya gunakan menggunakan tombol modifier super.

Masalah muncul ketika saya menggunakan tombol super sebagai shotcut untuk membuka popup whiskermenu. Setiap saya menekan shortcut yang menggunakan tombol super, popup whiskermenu selalu muncul, dan itu sangat mengganggu. Jalan paling mudah adalah mengganti shortcut popup whiskermenu menjadi ```w+space``` atau dengan tambahan key lain, namun hal itu sangat tidak nyaman bagi saya. Bagi yang mengalami masalah serupa, tenang saja, ada solusi mudah dan praktis, yaitu dengan menggunakan [xcape](https://github.com/alols/xcape).

xcape mengizinkan key modifier digunakan sebagai key lain saat ditekan dan dilepaskan. Contohnya begini, dengan menggunakan xcape kamu dapat menekan tombol super, namun mesinmu akan membacanya sebagai kombinasi tombol ```ctrl+shift+alt+super```. Dengan begitu saat kamu menekan shortcut yang menggunakan kombinasi tombol super, whisker menu tidak akan keluar, karena whiskermenu di bind ke tombol ```ctrl+shift+alt+super```.

Kita langsung masuk ke prakteknya saja

1.  Instal xcape, bisa dari repo, aur maupun compil sendiri.
2.  Buka xfce4-keyboard-settings > klik application shortcuts > klik add > tulisakan "xfce4-popup-whiskermenu " > klik ok > tekan tombol ```Ctrl+Shift+Alt+Super```.
3.  Buka xfce4-session-settings > klik application autostart > klik add > beri nama semaumu > tuliskan ```xcape -e "Super\_L=Control\_L|Shift\_L|Alt\_L|Super_L"``` pada bagian command > klik ok.
4.  Logout dan login kembali, coba tekan tombol super, maka popup whiskermenu akan keluar.

Sekian dari saya, bila sempat nanti akan saya update dengan gambar, wassalamu'alaikum.