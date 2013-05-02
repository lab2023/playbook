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
