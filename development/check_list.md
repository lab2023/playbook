# Kontrol Listesi

Bir işi yapmadan önce yapılması gereken işlerin listesidir.

## Deploy

* Veritabanı yedeklerinin alınması.
* Yeni bir versiyon atılması. version.txt'nin güncellenmesi.
* Müşterinin projesi ise proje grubuna email atılması
* Açık kaynaklı bir proje ise şirket mail grubuna mail atılması ve konu ile ilgili tweet atılması

## Proje Başlangıcı

**Müşteri adına açılacak hesaplar**

* Gmail mail adresi
* Github hesabı açılması
* Mandrill hesabının açılması
* Amazon S3 hesabının açılması
* İletişim için email grubu açılması
* Facebook app gerekli ise facebook app açılması
* SSL sertifikası alınacak

**Müşteriye sorulacak sorular**

* Sosyal medya hesaplarını aldınız mı?
* Marka tescili yaptınız mı?
* Takımın gtalk, email, iletişim bilgileri sizde var mı?
* Sizin adınıza hollywood lansmanı yapalım mı?
 
**Ekibin yapması gerekenler**

* Proje yöneticisi sözleşme ek1′e göre github issuelardan iterasyonları ayarlar. Böylece huboard kullanılmaya başlanır.
* Müşteri ile github, huboard, çevik süreçler ile ilgili kaynaklar paylaşılır. Müşteriye kısa bir bilgi verilir.
* Stagging ve production için sunucu kurulur. Bu işlem daha ilk kod yazılması ile yapılır.

## Sunucu Kurulumu

* Firewall var mı?
* Periyodik yedek alınıyor mu?
* Sunucu şifreleri Keepass programına girildi mi?

## Siteye Makale Yazılması

* Yazan kişişi - Mail grubuna mail atmak
* Sosyal medya sorumlusu - Twitter ve Facebook hesabında paylaşılması

## Yeni Sürüm Çıkarılması

**Açık Kaynak Projelerde**

* VERSION.txt değişmeli
* CHANGELOG.md değişmeli
* Yeni etiket oluşturulmalı
* Yeni etiket, master ve develop branch push edilmeli
* lab2023-dev mail grubuna email atılmalı

Sonra

* Yeni versiyon ile ilgili lab2023'e makale yazılmalı.
* Blog yazısında versiyonda ne olduğu anlatılmalı ve rubygems, changelog gibi unsurlara link verilmeli
* Blog yazısı twitter ve facebook hesabından paylaşılmalı

NOT: Kendinize işkence yapmayın! Git-flow kullanın.

**Müşteri Projelerinde**

* VERSION.txt değişmeli
* CHANGELOG.md değişmeli
* Yeni etiket oluşturulmalı
* Yeni etiket, master ve develop branch push edilmeli
* Proje email grubuna email atılmalı
* Staging sunucusuna deploy edilmeli

NOT: Hotfix olmadıkça yeni sürümler cumadan cumaya çıkar.
