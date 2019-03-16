---
title: "Keamanan PTS Online"
date: 2019-03-16T17:40:46+07:00
draft: false
tags:
- security
---
{{< lazyimg src="/img/525141.png" >}}
Ya, habis ganti tampilan dan dengan <s>bodohnya</s> tidak sengaja ngehapus artikel2 sebelumnya, kali ini mau membahas soal PTS (Penilaian Tengah Semester) Online yang baru saja dilaksanakan di sekolahan saya untuk pertama kalinya. Awalnya saya sendiri sudah curiga akan PTS Online ini mengingat jumlah laptop/pc yang ada di sekolan tidak banyak dibandingkan dengan jumlah peserta PTS.

# Zambro + Google Formulir = ....WTF!?

Dan yah, sekitar 1 minggu sebelum PTS Online dimulai sekolah memberi tahu soal aplikasi apa yang harus diinstall dan dibuatkan juga video panduannya tentang tata cara pengerjaan saat PTS Online.

{{< lazyimg src="/img/7347357.png" >}}

Gampangnya seperti ini sekolah membuat google formulir berisi soal lalu dimasukan ke url shortener bit.ly lalu diberikan ke siswa untuk dibuka dengan aplikasi [zambro](https://play.google.com/store/apps/details?id=id.sch.smkn2cikbar.exambrowser&hl=in) di handphonenya masing-masing.

Pertama-tama mari membahas soal kegunaan aplikasi zambro, intinya aplikasi ini unutuk meng-_Lock_ handphone kalian agar saat mengakses website yang kalian masukan kalian tidak akan bisa pindah aplikasi,screenshot,split screen. Jujur saja aplikasinya berjalan dengan baik dan cukup untuk mengamankan siswa-siswa Nakal.

Tapi, sekarang mari kita lihat disisi website untuk PTS Online yang dikasus sekolah saya menggunakan **GOOGLE <s>FUCKING</s> FORMULIR**. Sebenarnnya tidak ada masalah dengan penggunaan google formulir untuk PTS Online, tapi sekarang yang mau saya tanyakan adalah bagaimana sekolah tau kalau siswa memang benar-benar menggunakan Zambro untuk mengakses google formulir itu?

Mungkin kalian berpikir _**"Lah,kan ada pengawas?"**_. Iya, tentu saja pengawas bisa berjalan bolak-balik seperti orang thawaf untuk memastikan siswa tidak mengerjakan di chrome,firefox dan browser lainnya.. tapi bagaimana dengan fake zambro?

# HAH!? Zambro fake?

Saya tidak anggap ini celah dari aplikasi zambro maupun google formulir karena zambro memang tidak dibuat untuk google formulir dan sebaliknya, celahnya berasal dari keyakinan bahwa siswa akan mengakses google formulir tersebut dengan zambro. Contoh simplenya (Contoh lo ya...), saya membuat aplikasi mirip seperti zambro mulai dari tampilan dan fitur locknya tapi saya juga tambahkan tombol rahasia yang bisa mengaktifkan dan mematikan fitur _lock_ tersebut, yang berarti saya bisa membuka browser, whatsapp dll untuk mencari jawaban. Lalu bagaimana pengawas bisa membedakan antara zambro asli dan yang palsu?

{{< lazyimg src="/img/73238.png" >}}

tentu saja sangat sulit untuk pengawas membedakan aplikasi zambro asli dan yang palsu, seharusnya hal seperti ini bisa diminimalisir kalau website PTS Online memiliki pengecheckan browser/aplikasi yang digunakan, jadi website hanya bisa diakses dengan user-agent tertentu yang dimana fitur ini tidak ada di google formulir (setahu saya..), yang membuat Soal PTS Online ini bisa diakses dengan aplikasi apa saja.

# Kisah dari sekolah lain

Kebetulan teman saya, sekolahnya juga untuk pertama kali melakukan PTS Online. Dan jujur saja walaupun sama-sama pertama kali melaksanakan PTS Online, sekolah teman saya bisa dibilang lebih serius mulai dari aplikasi exambro yang _"Sepertinya"_ dibuat oleh sekolah sendiri dan website pelaksanaan PTS Online juga milik sekolah sendiri.

Jadi sistem aplikasi dan website adalah seperti ini, aplikasi secara otomatis membuka subdomain website sekolah untuk PTS Online dan juga memiliki user-agent tertentu, jadi website PTS Online hanya bisa diakses lewat aplikasi tersebut.

Ini yang saya sebut dengan koneksi antara aplikasi dan website yang bagus untuk PTS Online, karena Website tidak mau diakses dengan aplikasi lain dan aplikasi hanya akses website PTS. Walaupun pada akhirnya berhasil kami bikin kloningannya (Mungkin bakal saya jadikan postingan). 

# Akhir Kata

Saya sih berharap jika sistem PTS Online ini masih dilanjutkan, tolong pikirkan tentang keamanannya, saya tahu kalau ini pertama kalinya sekolah saya melaksanakan jadi agak maklum juga. Mungkin sistem yang digunakan sekolah teman saya bisa dijadikan contoh dan ditingkatkan keamanannya. Sekian Terimakasih.