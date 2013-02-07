# Redis

## Ubuntu Server Kurulum Talimatları

## OSX Kurulum Talimatları

Redis'i OSX ortamına kurmanın en kolay yolu homebrew kullanmaktır. Homebrew OSX için hazırlanmış daha ziyade geliştiricilere yönelik hazırlanmış paketlerin bulunduğu bir repo'dur diyebiliriz.

Kurulum için aşağıdaki komutu terminalden çalıştırmanız yeterlidir.

```bash
$ brew install
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
