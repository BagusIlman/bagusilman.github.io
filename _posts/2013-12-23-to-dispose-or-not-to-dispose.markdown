---
layout: post
title:  "To Dispose Or Not To Dispose"
date:   2013-12-23 00:55:37
categories: Article
---

Seperti yang kita tahu bahwa sebagian besar object di .net akan di dispose sendirinya oleh garbage collector sehingga secara umum kita tidak perlu secara eksplisit men-dispose object.

Namun ada beberapa class di .net yang tidak purely menggunakan komponen dot net, atau bahasa lainnya menggunakan unmanage resource. File handle, pinned memory, COM object, dan database connection adalah contoh-contoh class yang mengharuskan kita men-dispose sendiri object tersebut setelah kita tidak menggunakannya lagi.

Dalam SharePoint object model, terdapat beberapa class yang menggunakan unmanaged resource. SPWeb dan SPSite adalah contoh dari class yang menggunakan unmanaged resource. Contoh lain yang kurang terkenal namun menggunakan unmanaged resource adalah DataContext dalam LINQ to SharePoint.

Pertanyaannya adalah, apakah semua instance class yang menggunakan unmanaged class harus secara eksplisit di-dispose?

Ternyata, tidak semua instance dari class tersebut harus kita dispose.

Dalam mendispose object di SharePoint berlaku kaidah "Dia yang berbuat, dia juga yang harus bertanggung jawab". Maksudnya adalah jika kita sendiri yang meng-create object tersebut, maka kita juga yang harus men-dispose-nya. Namun jika kita hanya me-reference dari object lain, kita sebaiknya jangan men-dispose object tersebut.

{% highlight csharp %}
using (SPSite site = new SPSite(@"http://sitecollection/"))
{
    SPWeb web = site.RootWeb;
}
{% endhighlight %}

dalam contoh diatas, kita sendiri yang men-create object SPSite melalui perintah new SPSite(). Sehingga kita paham bahwa tidak ada orang lain yang menggunakan object tersebut selain kita dan SPSite tersebut dapat kita dispose kapanpun kita mau.

Lain halnya dengan contoh dibawah ini :

{% highlight csharp %}
private static void ItemUpdated(SPItemEventProperties properties)
{
    SPWeb web = properties.Web;
}
{% endhighlight %}

Disini kita hanya me-reference dari object yang sudah ada sebelumnya (properties.Web) sehingga pen-dispose-an dari object tersebut diluar tanggung jawab kita. Sebaiknya kita tidak mendispose onject SPWeb disini.

Akan ada possibility bahwa event receiver lain dalam list tersebut yang akan menggunakan object SPWeb. Ketika event receiver tersebut mencoba mengakses SPWeb yang telah terdispose sehingga akan menyebabkan memory leak, crash atau paling tidak performance issue.

So, ingat baik-baik : Siapa yang berbuat, dia juga yang harus bertanggung jawab. :P