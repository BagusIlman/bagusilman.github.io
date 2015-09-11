---
layout: post
title:  "Case Sensitive yang Kurang Sensitif"
date:   2012-09-23 00:55:37
categories: Article
---
Bagi gw sendiri yang sehari-hari pake C# ga akan kesulitan meng-convert kerjaan programmer laen yang nulis kodenya pake VB. Banyak situs situs di internet yang nyediain converter dari VB ke C#  dan biasanya berjalan dengan baik. Tapi kalo convert dari C #  ke VB? Eits.. belom tentu bisa, ada case sensitive yang bakal mbikin code yang dibuat pake C# jadi gagal diconvert ke VB.

Entah apa yang terbesit di dalam kepala Mbah Kernighan dan Mbah Ritchie ketika memutuskan kalo bahasa C adalah case sensitive, mungkin karena mereka keseringan chatting dan sebel sama orang yang nulis di chat-nya pake huruf capital semua. Atau mereka ketemu orang alay yang nulis nama doi dengan riTcHiE  .

Yang nggak abis pikir, kenapa semua bahasa turunan dari C ikut-ikutan menggunakan case sensitive juga, termasuk C# ini. And guess what? Gw ngabisin waktu sejam cuma buat nge-debug "SignOn" != "Signon". Sigh….

Tapi gw jadi mikir lagi. Untungnya gw kerja pake C# yang nota bene adalah compiler language, gimana kalo pake Phyton atau PHP? Keduanya punya identifier case-sensitive, scripting language yang nggak nge-resolve pas waktu parse. Bakal nggak ketauan errornya dimana, kalo nggak ditest dulu.

Intinya adalah, sejauh mungkin hindari penamaan yang sensitive terhadap besar kecilnya huruf. Kalo bener-bener perlu, kasih komen yang nerangin kalo ini ada pasangannya yang sama namanya cuma beda case.
