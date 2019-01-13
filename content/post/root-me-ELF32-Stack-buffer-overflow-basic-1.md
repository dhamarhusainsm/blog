---
title: "[Root Me] ELF32 Stack Buffer Overflow Basic 1"
date: 2019-01-08T22:01:07+07:00
draft: false
image: img/root-me-elf32-Stack-buffer-overflow-basic-1/thumb.png
tags:
    - root me
    - Binary hacking
---
Halo, Dhamar here ...

cuman mau berbagi cara nyelesaiin challenge [Root Me](https://www.root-me.org/en/Challenges/App-System/ELF32-Stack-buffer-overflow-basic-1), challenge ini sangat mudah. Oke jadi di challenge ini kita dikasih source code nya.

![](/img/root-me-elf32-Stack-buffer-overflow-basic-1/source-code.png)

Oke dari Source code diatas bisa diketahui kalau goals kita adalah overwrite variable check sehingga menjadi **0xdeadbeef** dengan buffer overflow, Oke sekarang seperti yang terlihat di line 16 kita perlu memasukan string ke variable buf dan buf sendiri memiliki alokasi 40 karakter mari kita coba run filenyadan memasukin 40 karakter.

![](/img/root-me-elf32-Stack-buffer-overflow-basic-1/step-1.png)

oke bagus, karena alokasi variable buf hanya 40 berarti jika kita masukan data melebihi 40 akan meng-overwrite variable check , oke langsung aja eksekusi..

![](/img/root-me-elf32-Stack-buffer-overflow-basic-1/step-2.png)

dan variable check ter-overwrite, oke kita sudah bisa mengkontrol variable check step selanjutnya yang perlu kita lakukan berarti mengubah isinya menjadi **0xdeadbeef**, **0xdeadbeef** berarti menjadi **\xef\xbe\xad\xde** dan langsung saja kita inputkan.

![](/img/root-me-elf32-Stack-buffer-overflow-basic-1/step-3.png)

Dan Booom!! kita berhasil mengubah variable check, tapi terus selanjutnya apa? kita enggak dapet flagnya... dari source code ditunjukan kalau kita berhasil mengubah checkmenjadi 0xdeadbeef maka akan membukakan shell, tapi shell langsung tertutup saat program juga selesai... kita hanya perlu menambahkan **cat -** agar shell code tetap terbuka.

![](/img/root-me-elf32-Stack-buffer-overflow-basic-1/step-4.png)

setelah shell terbuka kita bisa ketik **ls -a** untuk melihat seluruh file di folder tersebut dan bisa kita lihat ada file bernama **.passwd** setelah kita cat dan akhirnya kita mendapatkan flagnya....