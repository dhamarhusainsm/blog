---
title: "Memanfaatkan Celah LFI Dengan PHP Filters"
date: 2019-01-10T08:27:56+07:00
draft: false
image: img/memanfaatkan-celah-lfi-dengan-php-filters/thumb.png
tags:
    - root me
    - pentest
    - web
---

Halo, Dhamar here...
kali ini saya mau menunjukan bagaiman menggunakan php filters pada celah LFI, untuk contohnya saya akan menggunakan [root me - PHP filters](https://www.root-me.org/en/Challenges/Web-Server/PHP-filters).

## Apa itu LFI ?

**Local File Inclusion Vulnerability** adalah sebuah kelemahan aplikasi web yang menyebabkan seorang Attacker dapat mengeksploitasi Server dengan mengakses direktori dan mengeksekusi command di luar root web server.

## Root Me - PHP filters

Oke, jadi di Challenges ini kita mendapatkan url ini : http://challenge01.root-me.org/web-serveur/ch12/, langsung saja kita akses..

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-1.png)

Jadi ada 2 pilihan yaitu home dan login, saat saya coba akses login...

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-2.png)

bisa dilihat di linknya ada perameter **inc=login.php**, hmm.... coba ubah menjadi **inc=** saja dan ...

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-3.png)

ya, parameter **inc** adalah nama file yang dilempar ke fuction **include()** untuk dipanggil. Nah disini kita akan menggunakan `php://filter/convert.base64-encode/resource=login.php` yang funsinya akan encode file login.php menjadi base64 oke langsung saja...

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-4.png)

setelah berhasil dapatkan source code login.php yang ter encode, kita hanya perlu decode dengan terminal

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-5.png)

dan kita dapat source code nya 

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-6.png)

bisa dilihat ada pengecheckan username dan password yang kita masukan dengan variable **$username** dan **$password**,dan ada file **config.php** yang di include. sekarang coba kita akses **config.php** dengan `php://filter/convert.base64-encode/resource=config.php`

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-7.png)

lalu kita decode agar dapat source codenya..

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-8.png)

dan........

![](/img/memanfaatkan-celah-lfi-dengan-php-filters/step-9.png)

yes!, kita dapat username dan passwordnya.