---
title: Coding di Ponsel Android? Kenapa Tidak!
tags:
  - programming
  - termux
  - vim
categories:
  - Alat
  - Android
  - tutorial
featured_image: posts/termux-header.png
date: 2017-12-31 20:55:34
---

Hmmm ... Jadi gini, laptop saya yang biasa saya gunakan nampaknya sudah terlampau tua dan harus dipensiunkan, sedangkan saya belum ada rencana (baca: duit) dalam waktu dekat ini untuk membeli penggantinya. Masalahnya adalah saya kuliah di jurusan IT dan mau tidak mau harus ngoding. Selama ini saya ngoding memanfaatkan fasilitas yang diberikan kampus, bisa di lab. RPL maupun di Student Lounge. Btw, komputer di Student Lounge minimal berspesifikasi prosessor i5 dengan RAM 16 GB. Namun tentu lab. dan Student Lounge tidak buka sampai malam, pun di akhir pekan. Apalagi sekarang musim libur semester, ya saya pasti pulang dong.

Nah, satu-satunya gawai yang saya punya selain laptop ya cuman ponsel Oukitel K6000 yang selalu saya tenteng ke mana-mana ini. Spesifikasinya juga lumayan kalo cuma buat ngoding. Pertanyaannya, gimana cara ngoding di ponsel Android? Banyak cara sebenarnya untuk ngoding di Android, salah satunya yang akan saya tuliskan di bawah ini. Saya mau bercerita dulu sebentar.

Beberapa waktu lalu saya membaca blog milik pendiri IDRAILS. Di sana beliau bercerita tentang pengalaman menggunakan editor vim sebagai editor utama, yang sebelumnya menggunakan Sublime Text. Saya jadi penasaran juga ingin mencobanya. Dulu sih pernah juga mencoba, tapi keluarnya itu lo, susah! Heheheh .... Ternyata eh ternyata, vim itu bisa diatur sesuka pengguna. Sak udele dewe! Jadi konon katanya vim bisa digunakan sebagai IDE yang powerfull. Sekarang pasti sudah tau saya mau menggunakan apa untuk coding di Android. Vim tidak dapat dijalankan langsung di perangkat Android, maka dari itu saya menggunakan Termux dan menginstallnya di sana.

Termux dapat diinstall melalui Play Store maupun F-droid. Selanjutnya langsung saja kita install vim

```$ pkg update && pkg install vim```

Nah, seharusnya vim telah terpasang di Termux. Coba jalankan perintah vim di Termux. Untuk keluar dari vim, ketikkan ```:q``` diikuti dengan enter. Mudah bukan? Sekarang saatnya kita atur vim sehingga menjadi IDE yang nyaman digunakan. Pastikan saat perintah-perintah di bawah dijalankan, kamu berada di direktori Home.

<pre>
$ git clone https://github.com/souravchk/dotfiles.git
$ cat dotfiles/vimrc > ~/.vimrc
$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
$ pkg install ctags $ echo "set encoding=utf-8 nobomb" >> ~/.vimrc
$ vim +PluginInstall +qall
</pre>

Jika perintah-perintah di atas berhasil dieksekusi dengan lancara, maka kamu telah berhasil mengatur vim sebagai IDE. Coba jalankan kembali vim, seharusnya tampilan akan menjadi ini.

<div align="center">
![](/images/posts/termux-1.png)
</div>

Kita coba mengetikkan sesuatu. Untuk masuk ke mode INSERT kita tekan dulu tombol Insert di keyboard.

<div align="center">
![](/images/posts/termux-2.png)
</div>

Untuk menyimpan filekita haris keluar dulu dari mode INSERT dengan menekan tombol Esc. Setelahnya kita ketikkan perintah :w nama_file. Nah, codingan kita sudah menjadi berwarna-warni, itu tandanya vim mengenali bahasa tersebut dan mengaktifkan autocomplete. Kita tambahin dikit codingan kita dan rasakan perbedaannya.

<div align="center">
![](/images/posts/termux-3.png)
</div>

Jika ingin menyimpannya kembali, cukup keluar dari mode insert dan ketikkan :w diikuti dengan enter. Nah, sekian perkenalan dengan vim sebagai IDE di Termux Android. Nanti mungkin akan saya bahas kemampuan lain dari vim maupun Termux yang tidak kalah menarik. Sumber rujukan: https://souravchk.github.io/blog/2017/04/20/configure-vim