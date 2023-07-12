# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar

`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]

##### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın.

MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
#ilk 3 soruyu join kullanmadan yazın.

    1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.




    2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.


    3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.

    #join ile yazın
    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    SELECT ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih FROM ogrenci INNER JOIN islem ON ogrenci.ogrno=islem.ogrno

    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    SELECT t.turadi k.kitapadi FROM tur as t INNER JOIN kitap AS k ON t.turno= k.turno WHERE turadi="Fıkra" OR turadi="Hikaye"


    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

    SELECT o.ogrno,o.ograd,o.ogrsoyad,k.kitapadi FROM ogrenci AS o INNER JOIN islem ON islem.ogrno=o.ogrno INNER JOIN kitap AS k ON islem.kitapno = k.kitapno WHERE o.sinif in("10B","10C")


    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.

    Select o.ograd,o.ogrsoyad,o.ogrno,o.sinif,i.atarih from ogrenci as o
    	   Left Join islem as i On i.ogrno=o.ogrno


    8) Kitap almayan öğrencileri listeleyin.

    Select o.ograd,o.ogrsoyad,o.ogrno,o.sinif,i.atarih from ogrenci as o
    	   Left Join islem as i On i.ogrno=o.ogrno
    	   WHERE i.atarih is null


    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

    Select COUNT(k.kitapno) AS Toplam, k.kitapadi, k.kitapno FROM kitap AS k LEFT JOIN islem as i ON k.kitapno=i.kitapno GROUP BY k.kitapno

    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

    Select COUNT(k.kitapno) AS Toplam, k.kitapadi, k.kitapno FROM kitap AS k LEFT JOIN islem as i ON k.kitapno=i.kitapno GROUP BY k.kitapno


    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.

    Select o.ograd,o.ogrsoyad,k.kitapadi FROM ogrenci AS o INNER JOIN islem as i ON i.ogrno = o.ogrno INNER JOIN kitap as k ON k.kitapno = i.kitapno


    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.

    Select o.ograd,o.ogrsoyad,k.kitapadi,y.yazarad,y.yazarsoyad,t.turadi,i.atarih From ogrenci as o LEFT JOIN islem as i ON i.ogrno= o.ogrno LEFT JOIN kitap as k ON i.kitapno = k.kitapno LEFT JOIN yazar as y ON k.yazarno = y.yazarno LEFT JOIN tur as t ON k.turno = t.turno

    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.

     SELECT o.ograd,o.ogrsoyad, COUNT(k.kitapno) as "Okuduğu Kitap" FROM ogrenci AS o INNER JOIN islem as i ON i.ogrno = o.ogrno INNER JOIN kitap as k ON k.kitapno = i.kitapno GROUP BY o.ogrno


    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG

    select AVG(sayfasayisi) from kitap

    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.

    select * from kitap WHERE (sayfasayisi > (SELECT AVG(sayfasayisi) from kitap ))

    16) Öğrenci tablosundaki öğrenci sayısını gösterin

    SELECT COUNT(ogrno) as "Öğrenci Sayısı" FROM ogrenci


    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.

       SELECT COUNT(ogrno) as "Öğrenci Sayısı" FROM ogrenci


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

    select count(ograd) from ogrenci


    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    Select MAX(sayfasayisi)  from kitap


    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

     Select kitapadi,sayfasayisi  from kitap
    	   Where sayfasayisi=(Select MAX(sayfasayisi)  from kitap)


    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

     Select MIN(sayfasayisi) from kitap

    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    Select kitapadi,sayfasayisi from kitap
    	   Where sayfasayisi =(Select MIN(sayfasayisi) from kitap)


    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.

    Select * from kitap as k,
           tur as t where t.turno = k.turno and t.turadi = 'Dram' and sayfasayisi =(Select MAX(sayfasayisi) from kitap)


    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.

    Select Sum(sayfasayisi) from ogrenci as o
    	   Left Join islem as i On o.ogrno=i.ogrno
    	   Left Join kitap as k On i.kitapno= k.kitapno
    	   Where o.ogrno=15



    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

     Select CONCAT(Count(ograd),'   adet'),ograd from ogrenci
    	   Group by ograd


    26) Her sınıftaki öğrenci sayısını bulunuz.

Select COUNT(ogrno),sinif from ogrenci
Group by sinif

    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz

     Select CONCAT(COUNT(ogrno),'    adet'),cinsiyet,sinif from ogrenci
    	   Group by sinif,cinsiyet



    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.

     Select o.ogrno,o.ograd,o.ogrsoyad,SUM(k.sayfasayisi) as Toplam from ogrenci as o
    	   Left Join islem as i  On o.ogrno= i.ogrno
    	   Left Join kitap as k On k.kitapno=i.kitapno
    	   Group by o.ogrno
    	   order by Toplam DESC


    29) Her öğrencinin okuduğu kitap sayısını getiriniz.

Select Count(k.kitapno), o.ograd,o.ogrsoyad from ogrenci as o
Left Join islem as i On o.ogrno= i.ogrno
Left Join kitap as k On k.kitapno=i.kitapno
Group by o.ogrno
