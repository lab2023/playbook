# Capistrono

# Ubuntu server

# Nginx

# Unicorn

# Rbenv

# Backup
Backup işlemleri için [backup](https://github.com/meskyanichi/backup) gemini kullanıyoruz. Veritabanı yedeği, assets(resim, video) yedekleri ve log yedeklerini almamız yeterli. Uygulamalarımızı githubda geliştirdiğimiz için uygulamanın yedeğini alma ihtiyacı duymuyoruz. Yedeği hem locale hemde yedek işlemleri için ayırdığımız sunucuya alıyoruz.

# Monitoring
## Exception Notification (Hata Bildirici)
Sunucudaki 500 hatalrından haberdar olmak için [exception_notification](https://github.com/smartinez87/exception_notification) gemini kulanıyoruz. Gem sunucu 500 verirse anında bize mail atıyor. Gemin kullanımı ile ilgili şu yazıyı http://www.muhammetdilek.com/blog/2013/04/04/exception-notification-hata-bildirici/ okuyabilirsiniz.

# Heroku
