# Capistrono

# Ubuntu Server 12.10

Ubuntu Server'ı kurup root kullanıcısı ile terminalden ssh bağlantısını oluşturduğunuzu varsayıyoruz. 
Aşağıdaki işlemleri sırasyıla takip edin;

## Varsayılan SSH Port Numarasını Değiştirin

```bash
$ nano /etc/ssh/sshd_config
# What ports, IPs and protocols we listen for
# Port 22 -> Bu satıra rasgele bir port numarası veriniz.
$ /etc/init.d/ssh restart
```

## Mevcut Paketleri Güncelleyin

```bash
$ apt-get update && apt-get upgrade
```

## Aşağıdaki Paketleri Kurun

Bu paketleri kurmamızın sebebi  ```add-apt-repository ppa:*/*``` gibi kanal ekleme komutunu çalıştırabilmek içindir. 
Bu komut ubuntu 12.10 ile birlikte varsayılan olarak çalışmamaktadır.

```bash
$ sudo apt-get install python-software-properties && sudo apt-get install software-properties-common
```

## Locale Uyarılarından Kurtulun

```bash
$ export LANGUAGE=en_US.UTF-8 && export LANG=en_US.UTF-8 && export LC_ALL=en_US.UTF-8 && locale-gen en_US.UTF-8 && sudo dpkg-reconfigure locales
```

## Eğer Sunucuda Apache2 ve MySQL gibi şu anda kullanmak istemeceğiniz paketler varsa kaldırın.

```
$ dpkg --get-selections # Size mevcut kurulu paketleri gösterir
$ sudo apt-get --purge remove apache2*
$ service apache2 stop
$ sudo apt-get remove --purge mysql-server mysql-client mysql-common
$ sudo apt-get autoremove
$ sudo apt-get autoclean
```

## Htop kurun (Bu bir tavsiyedir)

```bash
$ apt-get install htop
```

Sıradakı aşama olan Nginix kurulumuna başlayabilirisiniz...

# Nginx

## Stabil Güncel Sürüm İçin Nginx Kanalını Ekleyin

```bash
$ add-apt-repository ppa:nginx/stable
$ apt-get update
```

## Nginx'i Kurun

```bash
$ apt-get install nginx
```

Kurulmu tamamlandıktan sonra nginx'i ```service nginx start``` komutu ile konsoldan başlatın.

### DİKKAT: Ubuntu 12.10 da nginx 1.2.7 versiyonunu kurdugunuzda nginix'i başlatırken aşağıdaki gibi bir hata alırsanız:

```bash
* Starting nginx nginx
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] still could not bind()
   ...done.
   ...done.
```

Nano v.b. bir editör ile Nginx default site ayarlarını açın.

```bash
$ nano /etc/nginx/sites-available/default
```

Server ayarlarının olduğu satırdaki aşağıdakı kısmı bulun ve belirtildiği (```ipv6only=on``` kısmına dikkat!) 
şekilde değiştirip, dosyayı kaydedip kapatın.

** Önce **

```bash
server {
        listen 80;
        listen [::]:80 default_server;
        ...
```

** Sonra **

```bash
server {
        listen 80;
        listen [::]:80 ipv6only=on default_server;
        ...
```

Bu işlemi yaptıktan sonra konsoldan ```service nginx start``` komutunu koştuğunuzda nginx başlatılacaktır. 

## Nginx'i Başlatın

```bash
$ service nginx start
```

Sunucu ip'nizi yada domaini yazarak nginx start sayfasının geldiğinden emin olunuz.

# Git & Curl

Sunucunuzdaki kodları Capistrano aracılığı ile deploy edebilmemiz için Git kurulu olması gerekmektedir. 
Aynı zamadan sunucunuzda Curl da kurulu olmalıdır. Aşağıdakı paketleri kurun.

```bash
$ apt-get -y install curl git-core
```

## Sunucuya github proje reposundaki ssh key'i ekleyin ve github bağlantısını doğrulayın.

Bu işlemi yapmadan önce aşağıdakı komutu çalıştırın ve çıktıyı doğrulayın.

```bash
$ ssh git@github.com
# The authenticity of host 'github.com (207.97.227.239)' can't be established.
# RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
# Are you sure you want to continue connecting (yes/no)? yes
# Warning: Permanently added 'github.com,207.97.227.239' (RSA) to the list of known hosts.
# Permission denied (publickey).
```

Sunucuya GitHub reponuzda bulunan Settings > Deploy Keys sekmesine eklemek üzere bir public ssh_key oluşturun. 
Deploy sırasında GitHub'ın sormaması için herhangi bir şifre vermeyin. Böylelikle deploy süreci hızlanmış olacaktır.

```bash
$ ssh-keygen -t rsa -C "user@example.com"
# GitHub üyelik e-postanız veya herhangi bir e-posta adresi.
# Örneğin sunucuda barındırılacak ygulamanın info@... adresi olabilir.
```

Oluşturulan public ssh_key'in içeriğini kopyalayın ve GitHub'da belirtilen sekmeye gidip "Add Deploy Key" diyerek ekleyin.

```bash
$ cat ~/.ssh/id_rsa.pub
```

## Bir Deployer kullanıcısı ekleyin

Bunun için öncesinde bir admin grubu oluşturmalısınız ve ardından deployer adında bir kullanıcıyı bu gruba ekleyin.

```bash
$ groupadd admin && adduser deployer --ingroup admin
```

Kullanıcı şifresini ve verilen soruları cevaplayın. Artık deployer kullanıcımız oluşturuldu. 
Bu kullanıcıya daha sonra ruby rbenv ve diper deploy süreçlerinde ihtiyaç duyacağız.

# Rbenv

Sunucumuza Rbenv kurabilmek için öncesinde deployer olarak ssh bağlantısı oluşturmalıyız.

```bash
$ ssh deployer@127.0.0.1 -p xxxx
```

Yada eğer root olarak bağlı iseniz

```bash
$ su - deployer
```


Bu işlemden sonra aşlağıdaki paketleri kurun. Bu paketlerden daha önceden mevcut kurulu olanlar olabilir.

```bash
$ sudo apt-get install zlib1g-dev openssl libopenssl-ruby1.9.1 libssl-dev libruby1.9.1 libreadline-dev git-core make make-doc
```

Deployer kullanıcısının home dizinine gidin. Rbenv'i GitHub reposundan klonlayın vekabuk ve konsol 
ayarlarını yapıp tekrar başlatın.

```bash
$ cd ~
$ git clone git://github.com/sstephenson/rbenv.git .rbenv
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
$ exec $SHELL
```

Rbenv kurulumunu ```which rbenv``` komutu ile konsoldan doğrulayın. 
Herşey yolunda gidiyorsa şu şekilde bir çıktı almalısınız: ```/home/deployer/.rbenv/bin/rbenv```

Şimdi gerekli pluginleri kurmak için aşağıdaki adımları takip edin.

```bash
$ mkdir -p ~/.rbenv/plugins
$ cd ~/.rbenv/plugins
$ git clone git://github.com/sstephenson/ruby-build.git
$ git clone git://github.com/sstephenson/rbenv-gem-rehash.git
$ rbenv install 2.0.0-p0
$ rbenv rehash
$ rbenv global 2.0.0-p0
$ ruby -v
# ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-linux]
```

Eğer yukarıdakı adımları izleyip ruby versiyonunu doğruladıysanız işlem tamamlanmış demektir. 
Artık Rbenv aktif ve ilgili ruby versiyonu sunucunuza kurulmuş demektir.

# Bundler

Rbenv kurumulundan hemen sonra sisteme bundler gem'i kurmamız gerekmekte. Aşağıdaki komutları çalıştırın.

```bash
$ gem install bundler --no-ri --no-rdoc
$ rbenv rehash
$ bundle -v

```

# Node.js

En temel haliyle Rails projelerinde assets-precompile işlemleri için node.js'in de sunucuda kurulu olması gerekmektedir.

```bash
$ add-apt-repository ppa:chris-lea/node.js
$ apt-get update
$ apt-get install nodejs
```

# Unicorn

# Backup
Backup işlemleri için [backup](https://github.com/meskyanichi/backup) gemini kullanıyoruz. Veritabanı yedeği, assets(resim, video) yedekleri ve log yedeklerini almamız yeterli. Uygulamalarımızı githubda geliştirdiğimiz için uygulamanın yedeğini alma ihtiyacı duymuyoruz. Yedeği hem locale hemde yedek işlemleri için ayırdığımız sunucuya alıyoruz.

### Log Yedekleri
Log dosyalarının çok şişmesi genel problemimiz. Biz bunu nasıl çözüyoruz ? Linux logrotate kullanıyoruz . Logrotate log dosyalarını rotate ederek şişmesini önler.
Logrotate kullanmak için `/etc/logrotate.conf` dosyasına aşağıdaki kodları ekliyoruz.

```bash
# Rotate Rails application logs
/home/deployer/apps/birekmek/current/log/*.log {
  daily #Bu işlemi günlük yap
  missingok # İşlem yapılacak log dosyaları eksik ise hata verme
  rotate 7 # 7 tane dosya tut
  compress # Sıkıştır gzip varsayılan
  delaycompress # Bir sonraki log ortasyonuna kadar sıkıştırmayı beklet. Yani sıkıştırma
  notifempty # Log dosyası boş ise rotate etme
  copytruncate # O anki yazılan log dosyasını rotate ederken rotate anında yazılan verile kaybetmemek için
  sizem 1024 # Magabayt olarak boyut 1024 olsun
}
```
Sıkıştırılmış log dosyalarının backup gemi ile yedeğini alıyoruz.
# Monitoring
## Exception Notification (Hata Bildirici)
Sunucudaki 500 hatalrından haberdar olmak için [exception_notification](https://github.com/smartinez87/exception_notification) gemini kulanıyoruz. Gem sunucu 500 verirse anında bize mail atıyor. Gemin kullanımı ile ilgili şu yazıyı http://www.muhammetdilek.com/blog/2013/04/04/exception-notification-hata-bildirici/ okuyabilirsiniz.

# Heroku


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
* Bir starın uzunluğun max 1.6 TB olabilir.
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

