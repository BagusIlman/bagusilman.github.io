---
layout: post
title:  "Mendapatkan List Service dengan Credential Tertentu"
date:   2013-05-09 00:55:37
categories: Article
---
Gw hari ini dapet kasus dimana user ingin mengganti password system account di Sharepoint, namun account system account juga dipakai untuk menjalankan service. Masalah yang terjadi ketika password system account diubah adalah service yang memakai account system account tidak akan berfungsi.

Yang pertama yang ingin gw ketahui adalah bagaimana caranya mem-populate user system account itu dipake di service mana aja. Pas gw utak atik powershell ketemu command yang kayaknya menjanjikan yg namanya Get-Service. Tanpa banyak basa basi gw coba aja tuh command dan hasilnya dy mempopulate service yg ada di server tapi nggak ada kolom credential disana. Gw coba pipe sama Format-List tapi hasilnya tetep gak muncul tuh kolom credential.

Setelah mencoba dengan Get-Service dan gagal, gw coba dengan Get-WmiObject. Prtama sich ga ketemu juga tuh kolom tapi dengan format-list disitu keliatan kalo dy jga punya kolom yang menjelaskan credential yg ipake service tersebut. Nama kolom tsb adalah start name. Nam yang cukup aneh...

Finally gw pipe Get-WmiObject dengan Format-Table dan gw specify kolom-kolom apa aja yang mau ditampilkan dan akhir kata scrip gw jadi sbb:

{% highlight PowerShell %}
Get-WMIObject Win32_Service
| Where-Object{$_.StartName -eq 'LocalSystem'}
| Sort-Object -Property StartName
| Format-Table Name, StartName
{% endhighlight %}
