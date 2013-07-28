## Ruby on Rails Geliştiricileri için PostgreSQL

Bu belgede lab2023 - internet teknolojileri olarak özel projelerde ve SAAS ürünlerimizde kullandığımız PostgreSQL
veritabanını nasıl kullandığımızı dökümante edilmiştir. Aşağıdaki konuları içerir,

* Genel Bilgiler
* Kurulum
* DB Yaratma
* Kullanıcılar ve Roller
* Ayarlar
* Performans
* Partition
* Replikasyon
* Backup Restore
* Active Record ve PostgreSQL

Daha detaylı bilgi için  http://www.postgresql.org/files/documentation/pdf/9.2/postgresql-9.2-A4.pdf bakabilirsiniz.

## Genel Bilgiler

### Genel veritabanı bilgileri

* 1 TB altındaki veritabanları küçüktür. 
* Veritabanında hızdan çok stabil olması önemlidir.

### Genel PostgreSQL bilgileri

* PostgreSQL veritabanı dışındaki işlemleri işletim sistemine bırakır. Yani fazla bir kaynağa gerek yoktur.
* PostgreSQL 32 coredan fazlasını kullanamıyor. 64 core makine satın almaya gerek yoktur!
* Default 24 MB ile geliyor. 
* 8.4 versiyonuna kadar yavaş ancak stabil bir versiyonu var. 9.2 den sonra diğer veritabanlarından daha hızlı çalışır.
* 1975-85 yılında invest adıyla ilk yapılıyor. İlk yapım amacı veritabanlarının yeterli komplex işlemleri yapamıyor.
* 1995 yılında PostgreSQL yapılıyor. 10 kişilik bir developer ile yapılıyor.

### Limitler

* Veritabanında bir limit sınırımız yok.
* Bir tablo 32 TB olabilir.
* Bir satırın uzunluğun max 1.6 TB olabilir.
* Bir satırın bir columnu max 1 TB olabilir.
* Bir tabloda 250 den fazla index olmamalı fazlası sıkıntıdır.

### Süreçler

* Postmaster bütün işleri yapar.
* Her işlem bir process olarak olur.
* PostgreSQL i kurduktan bir cluster oluşur. Her cluster bir port kullanır, sistem kaynaklarını ayrıca tüketir.

## Kurulum

### Ubuntu Server 12.04

**Gerekli olan kütüphane**

```bash
sudo apt-get install libpq-dev
````

**Kurulum**

```bash
sudo add-apt-repository ppa:pitti/postgresql
sudo apt-get update
sudo apt-get install postgresql-9.2
````

**Güncelleme**

```bash
sudo apt-get upgrade
````

**Varsayılan ayar dosyaları**

```bash
/etc/postgresql/9.2/main
/var/lib/postgresql/9.2/main
````

### Ubuntu Server 12.10

Kuruluma başlamadan önce

```$ sudo apt-get update && sudo apt-get upgrade```

Ardından Aşağıdaki paket kuruluyor. Bu paketleri kurmamızın sebebi  ```add-apt-repository ppa:pitti/postgresql``` komutunu çalıştırabilmek içindir. Bu komut ubuntu 12.10 ile birlikte varsayılan olarak çalışmamakta.

```$ sudo apt-get install python-software-properties &&  sudo apt-get install software-properties-common```

Bu işlemlerin ardından postgresql 9.2 için gereken paketi repoya ekliyoruz. 

```$ sudo add-apt-repository ppa:pitti/postgresql```

Bu işlemlerden sonra aşağıdaki komutla repoları güncelliyoruz.

```$ sudo apt-get update```

Son olarak aşağıdaki komut ile postgresql 9.2 kurulumunu tamamlıyoruz. Ben kurulumu yaptıgım zamanda 9.2.4 kurulumunu yapmıştı.

```console
$ sudo apt-get install postgresql-9.2
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following extra packages will be installed:
  libpq5 libxml2 postgresql-client-9.2 postgresql-client-common postgresql-common sgml-base ssl-cert xml-core
Suggested packages:
  oidentd ident-server locales-all postgresql-doc-9.2 sgml-base-doc openssl-blacklist debhelper
The following NEW packages will be installed:
  libpq5 libxml2 postgresql-9.2 postgresql-client-9.2 postgresql-client-common postgresql-common sgml-base
  ssl-cert xml-core
0 upgraded, 9 newly installed, 0 to remove and 2 not upgraded.
Need to get 6,652 kB of archives.
After this operation, 26.3 MB of additional disk space will be used.
Do you want to continue [Y/n]? Y
.....
.....
.....
 * Starting PostgreSQL 9.2 database server                                                               [ OK ] 
Processing triggers for libc-bin ...
ldconfig deferred processing now taking place
Processing triggers for sgml-base ...
Updating the super catalog...
```

### Mac geliştirme (homebrew)

## Cluster yaratma

## Dizin yapısı

## Kullanıcı ve Roller

## Tablespace

## Ayarları 

## DB İşlemleri

**Create DB**

* Serverin locale si ayarlanması
* ENCODING'ı unutmayın!

```sql
CREATE DATABASE xxxx_production OWNER xxxx ENCODING 'UTF8' LC_COLLATE = 'en_US.UTF-8' LC_CTYPE = 'en_US.UTF-8' TEMPLATE template0;
````

**DROP DB**

```sql
DROP DATABASE xxxx_production;
````

**Can't Drop Db Sorunsali**

DB yi kullanan sessionlarin olmasi durumu.

```sql
SELECT pid FROM pg_stat_activity where pid <> pg_backend_pid();
SELECT pg_terminate_backend(pid);
````

### Bağlantı ve Yetkilendirme

* http://www.postgresql.org/docs/9.2/interactive/runtime-config-connection.html

### Kaynak Tüketimi

* http://www.postgresql.org/docs/9.2/interactive/runtime-config-resource.html

### Logların yazımı

* http://www.postgresql.org/docs/9.2/interactive/runtime-config-wal.html

### Log Ayarları

* http://www.postgresql.org/docs/9.2/interactive/runtime-config-logging.html

### Auto Vacum ve Analiz

* http://www.postgresql.org/docs/9.2/interactive/routine-vacuuming.html#AUTOVACUUM
* http://www.postgresql.org/docs/9.2/interactive/runtime-config-autovacuum.html

## Partition

## Replikasyon

* http://www.postgresql.org/docs/9.2/static/runtime-config-replication.html

## Backup - Restore

* http://www.postgresql.org/docs/9.2/interactive/backup.html
* http://www.muhammetdilek.com/blog/2013/01/21/postgresql-yedek-alma-ve-geri-yukleme/
* https://github.com/tayfunoziserikan/articles/blob/master/PostgreSQL%20AB2013%20Eg%CC%86itim%20Notlar%C4%B1%20-%20I.md#yedekleme--geri-ykleme-backup--restore

# Redis

## Ubuntu Server Kurulum Talimatları

## OSX Kurulum Talimatları

Redis'i OSX ortamına kurmanın en kolay yolu [Homebrew](http://mxcl.github.com/homebrew/) kullanmaktır. Homebrew OSX için hazırlanmış daha ziyade geliştiricilere yönelik hazırlanmış paketlerin bulunduğu bir repo'dur diyebiliriz.

Kurulum için aşağıdaki komutu terminalden çalıştırmanız yeterlidir.

```bash
$ brew install redis
```

Kurulum işleminiz tamamlandıktan sonra konsola aşağıdaki komutu yazın ve hemen altındakine benzer bir çıktı aldığınızdan emin olun.

```bash
$ redis-server
[13193] 07 Jul 21:34:25 # Warning: no config file specified, using the default config. In 
order to specify a config file use 'redis-server /path/to/redis.conf'
[13193] 07 Jul 21:34:25 * Server started, Redis version 2.4.15
[13193] 07 Jul 21:34:25 * The server is now ready to accept connections on port 6379
[13193] 07 Jul 21:34:25 - 0 clients connected (0 slaves), 922304 bytes in use
```

Güzel, şimdi yukarıdaki konsol çıktılarını aldığınıza göre redis varsayılan ayarlarla çalışmaya başladı demektir. Eğer redis'in ayarlarını değiştirip kendi belirlediğiniz ayarlarla çalışmasını istiyorsanız aşağıdaki yöntemi deneyin.

```bash
$ redis-server /path/to/redis.conf
```

Bunun dısında genellikle tercih edilen bir yöntem de redis config dosyasını ~/.redis dizinine kopyalamanızdır. Böylelikle redis-server başlarken default ayarlarını buradan okuyarak ayaklanacaktır.

```bash
$ mkdir ~/.redis
$ cp /usr/local/src/redis-x.x.x/redis.conf
```

