# Capistrono

# Ubuntu server

# Nginx

# Unicorn

# Rbenv

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
