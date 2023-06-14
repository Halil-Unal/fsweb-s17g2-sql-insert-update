# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

# Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#Tablolar 
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]



# Görevler
Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın. 



	1) ÖRNEK SORU: Yazar tablosunu KEMAL UYUMAZ isimli yazarı ekleyin.
	
 INSERT INTO yazar(yazarad,yazarsoyad) VALUES('kemal','ÖZKAYA')
	
	2) Biyografi türünü tür tablosuna ekleyiniz.
	
	insert into tur(turadi) values(biyoloji35)

	3) 10A sınıfı olan ÇAĞLAR ÜZÜMCÜ isimli erkek, sınıfı 9B olan LEYLA ALAGÖZ isimli kız ve sınıfı 11C olan Ayşe Bektaş isimli kız öğrencileri tek sorguda ekleyin. 
	INSERT INTO ogrenciler ( ograd, ogrsoyad, cinsiyet)
VALUES
('Hülya', 'Yiğit', 'K', , '10A'),
( 'Niyazi', 'Sevinç','E','9B');

	
	4) Öğrenci tablosundaki rastgele bir öğrenciyi yazarlar tablosuna yazar olarak ekleyiniz.
	
	INSERT INTO yazar(yazarad,yazarsoyad)  


	5) Öğrenci numarası 10 ile 30 arasındaki öğrencileri yazar olarak ekleyiniz.
	
	
	6) Nurettin Belek isimli yazarı ekleyip yazar numarasını yazdırınız.
	(Not: Otomatik arttırmada son arttırılan değer @@IDENTITY değişkeni içinde tutulur.)
	
	
	7) 10B sınıfındaki öğrenci numarası 3 olan öğrenciyi 10C sınıfına geçirin.
	
	
	8) 9A sınıfındaki tüm öğrencileri 10A sınıfına aktarın
	
	
	9) Tüm öğrencilerin puanını 5 puan arttırın.
	
	update ogrenci set puan=puan+5
	
	10) 25 numaralı yazarı silin.

delete from yazar where yazarno=25

	11) Doğum tarihi null olan öğrencileri listeleyin. (insert sorgusu ile girilen 3 öğrenci listelenecektir)
	
	
	12) Doğum tarihi null olan öğrencileri silin. 
	delet from ogrenci where dtarih=NULL
	
	13) Kitap tablosunda adı a ile başlayan kitapların puanlarını 2 artırın.
	
	UPDATE kitap set puan=puan+2 where kitapadi LIKE 'A%'
	
	14) Kişisel Gelişim isimli bir tür oluşturun.
	İNSERT İNTO tur(turadi) values('Kişisel Gelişim') 
	
	15) Kitap tablosundaki Başarı Rehberi kitabının türünü bu tür ile değiştirin.
	
	update kitap set kitapadi='Kişisel Gelişim' where kitapadi='Başarı Rehberi'

	16) Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir prosedür oluşturun.
	
CREATE PROCEDURE ogrencilistesi()
LANGUAGE 'SQL'
AS $BODY$
    SELECT * FROM ogrenciler;
AS $BODY$
CALL ogrencilistesi();
	
	17) Öğrenci tablosuna yeni öğrenci eklemek için "ekle" adında bir prosedür oluşturun.
	CREATE PROCEDURE ekle(IN p_ograd VARCHAR(255), IN p_ogrsoyad VARCHAR(255), IN p_sinif VARCHAR(255), IN p_ogrno INT, IN p_puan INT)
LANGUAGE 'SQL'
AS $BODY$
    INSERT INTO ogrenciler (ograd, ogrsoyad, sinif, ogrno, puan)
    VALUES (p_ograd, p_ogrsoyad, p_sinif, p_ogrno, p_puan);
AS $BODY$

CALL ekle('Öğrenci Adı', 'Öğrenci Soyadı', 'Sınıf', 12345, 85);
	
	18) Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.
	
		CREATE PROCEDURE sil( IN p_ogrno INT)
LANGUAGE 'SQL'
AS $BODY$
   delete from ogrenci where ogrno='p_ogrno'
    
AS $BODY$
	
	19) Öğrenci numarasını kullanarak kolay bir biçimde öğrencinin sınıfını değiştirebileceğimiz bir prosedür oluşturun.
	
	
	20) Öğrenci adı ve soyadını "Ad Soyad" olarak birleştirip, ad soyada göre kolayca arama yapmayı sağlayan bir prosedür yazın.
	
	
	21) Daha önceden oluşturduğunu tüm prosedürleri silin.
	
	
	#Esnek görevler (Esnek görevlerin hepsini Select in Select ile gerçekleştirmeniz beklenmektedir.)
	22) Select in select yöntemiyle dram türündeki kitapları listeleyiniz.
	
	  select * from kitap where turno=(select turno from tur where turno=1)
	
	23) Adı e harfi ile başlayan yazarların kitaplarını listeleyin.
	 SELECT * FROM kitap WHERE yazarno = (SELECT yazarno FROM yazar WHERE yazarad LIKE 'A%');
	
	24) Kitap okumayan öğrencileri listeleyiniz.
	
	
	25) Okunmayan kitapları listeleyiniz

	
	26) Mayıs ayında okunmayan kitapları listeleyiniz.
