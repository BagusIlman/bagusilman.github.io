---
layout: post
title:  "Return Void"
date:   2013-04-16 00:55:37
categories: Article
---
Salah satu return type dari fungsi yang dibuat pake c# (dan bahasa turunan c lainnya) adalah void. Simpelnya fungsi yang returrn void tidak mengembalikan nilai apapun. Mirip-mirip kayak subroutine atau prochedure kalo pembaca dulu pernah main-main di bahasa Pascal.

Sebenernya ga ada yang salah dengan fungsi yang return void, tapi  kayaknya sayang aja kalo kita manggil fungsi tapi fungsinya ga ngembaliin apa-apa. Mungkin perumpamaan kasarnya kayak kita ngasi perintah ke orang dan perintah kita ga direspon apa-apa (pastinya orang tsb tau kalo kita manggil, tapi karena dy ga bs respon, kt jadi ga tau apakah dy ngerti apa yg kita mau apa nggak).

Return boolean bisa jadi salah satu alternatif kalo kita butuh respon dari fungsi yang kita panggil. Dengan hal tersebut kita tidak perlu lagi mengecek apakah suatu proses berhasil atau tidak dari object-nya, cukup dari return value nilai fungsinya saja.

{% highlight charp %}
    public class Sample
    {
        public int Hasil { get; set; }
        public bool DoSomething()
        {
            try
            {
                var someProxy = new SomeProxy();
                Hasil = someProxy.SomeMethod; //isi hasil dengan nilai dari fungsi lain
            }
            catch (Exception)
            {
                return false;
            }
            return true;
        }
    }
    var sample = new Sample();

    if (sample.DoSomething()) // cukup periksa dari hasil fungsi
    {
              // code yang lain disini
    }

{% endhighlight %}

Tapi bagaimana kalau memang kita benar-benar ga perlu nilai balikan fungsi? Benar benar ga perlu walaupun hanya sekedar boolean? Mungkin bisa dicoba dengan memberi balikan object-nya saja sehingga bisa di chain. Lebih lengkapnya bisa dilihat contoh dibawah:

{% highlight charp %}
public class Operasi {

    public int Hasil { get;set; }

    public void Tambah(int number) {
        Hasil += number;
    }

    public void Kurang(int number) {
        Hasil -= number;
    }
}

var operasi = new Operasi();
operasi.Tambah(10);
operasi.Tambah(20);
operasi.Kurang(10);
System.Console.WriteLine(operasi.Hasil);

{% endhighlight %}

Disini gw terus-terusan nulis kata operasi kalo pengen manggil Tambah atau Kurang karena memang fungsi Tambah dan Kurang-nya return void. bandingkan kalo kita return object operasi-nya, bukan hanya void:

{% highlight charp %}
public class Operasi {

    public int Hasil { get;set; }

    public Operasi Tambah(int number) {
        Hasil += number;
    }

    public Operasi Kurang(int number) {
        Hasil -= number;
    }
}

System.Console.WriteLine(
     new Operasi().Tambah(10)
                  .Tambah(20)
                  .Kurang(10)
                  .Hasil);
{% endhighlight %}

Lebih ringkas dan simple kan? Well, at least menurut gw gitu :)

So kesimpulannya, return void memutuskan kemampuan untuk melakukan chain call. Kalo emang nggak perlu ngembaliin apa-apa, bisa di coba untuk return objectnya aja.