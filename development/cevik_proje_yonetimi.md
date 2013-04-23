# Çevik Süreçler

Proje yönetimi için çevik süreçler kullanılır.

* [Çevik Manifesto](http://agilemanifesto.org/iso/tr/)
* [Çevik İlkeler](http://agilemanifesto.org/iso/tr/principles.html)
* [Kanban](http://kanban.lab2023.com) için huboard programını kullanıyoruz.
* Sürüm kontrolü için [semver](http://semver.org/) kullanıyoruz.

# Huboard

Huboard' un proje üzerinde uygulanması için github'da aşağıdaki 5 etiket açılır:

* 0 – Backlog
* 1 – Ready
* 2 – In Progress
* 3 – Done
* 4 – Reviewed

Etiketlerin anlamları:

* 0 – **Backlog** : Müşteri ile görüşülmeye devam eden veya görüşülmüş, detaylandırılması sonuçlanmamış, yani henüz analizi tamamlanmamış iş birimi.
* 1 – **Ready** : Analizi tamamlanmış, detaylandırılması yapılmış, geliştirilmeye hazır iş birimi
* 2 – **In Progress** : Geliştirici iş birimini geliştirmeye başlamış, yani geliştiricini hali hazırda üzerinde çalıştığı iş birimi
* 3 – **Done** : Geliştirici iş birimini geliştirmeyi tamamlamış, geliştirme ortamında çalışan iş birimi.
* 4 – **Reviewed** : Geliştiricinin tamamladığı iş birimi kontrol edilmiş, yazım standartlarına uygun olduğu, istenilen işlevi yaptığı ve çalışır olduğu doğrulanmış iş birimi. Üretim ortamına atılabilir, yayınlamaya hazır işe birimi.

## Github ve Etiketler

lab2023 projelerinde github'da 4 adet etiket açılır.

* **Bug** - Hata bildirimleri için kullanılır.
* **Enhancement** - Programdaki bir özelliği veya arayüzü iyileştirmek için kullanılır.
* **Question** - Soru sormak, öneride bulunmak veya tartışmak için kullanılır.
* **Future** - Proje süresince müşterinin aklına gelen ancak anlaşmadığımız gelecekte yapılması planlanan işlerdir. Bunlar yapılmaz ancak fikirler unutulmasın diye future etiketi ile etiketlenir.

NOT: 

1. wontfix, dublicate, invalid gibi etiketler kullanılmaz. 
2. Eğer yeni iş istek varsa buna etiket yapılmaz. 

# Semantik Versiyonlama

lab2023 olarak www.semver.org adresinde ki standartlara göre versiyonlama yapıyoruz. Bu reponun Türkçesini https://github.com/lab2023/semver/blob/tr_translation/locales/semver.tr.md adresinde bulabilirsiniz.

**Kurallar**

* X.Y.Z şeklinde ifade edilecen bir versiyonlama da X -> Major, Y -> Minor, Z -> Patchi ifade eder.
* Z -> Uygulamaya yapılan hotfix ve typo düzeltmelerinden de yapılır. Yani uygulamaya yeni bir özellik eklemediyseniz, belli bir yerdeki bir hatayı veya yazıyı değiştirdiyseniz Z sayısı değişir.
* Y -> Uygulamaya eklenen yeni özellikler, iyileştirmeler sonucunda değişir. Y deki değişiklikler eski kullanıcıları eklemez. Y de ki değişiklikler **GERİYE UYUMLU**dur.
* X -> Uygulamada yapılan büyük değişikliklerdir. Örneğin yapının komple değişmesi, teknolojinin değişmesi gibi gibi. X de yapılan bir değişiklik **GERİYE UYUMLULUĞU** desteklemez.
* Bir uygulama 0.1.0 versiyonu ile başlar. 
* Bir uygulama product olunca 1.0.0 olmalıdır. 
* Eğer X = 0 ise o uygulama stable değildir. Yani her an her şeyi değişebilir. Hala develop aşamasındadır.
* Her uygulmanın versiyonunu gösteren bir API si olmalıdır. Yani kullancılar, diğer developerlar mutlaka hangi sürümü kullandıklarını bilmelidir! **Bu programcının birinci ve en önemli görevidir.**
* Versiyonlamada [0-9A-Za-z-] ifadelerini kullanabilirsiniz.
* 1.0.0-alpha.1 gibi prepatchleri kullanmanızı biz lab2023 olarak önermiyoruz. Hayat zaten yeterince karışık!

# Üretkenlik

Bu bölümde geliştiricilerin üretkenliğini artırmaya yönelik kurallar vardır.

* Gelişticiler ile toplantılar günde bir alınır. Bu toplantılar günlük 5 dakikayı geçemez.
* Geliştiricilere işler iteratif olarak haftalık verilir.
* Geliştirici aynı anda iki projeye de çalışmaz. Bir proje bitmeden başka projeye geçemez.
* Mümkün olduğunca iki geliştirici bir projede çalışır.
* Geliştiriciler sorularını mail grubunda sorarlar. Böylece sorular kayıt altına alınır. Aynı sorular iki defa sorulmaz.
* İletişim aracı olarak sırasıyla 1. mail, 2. gtalk, 3. cep telefonu tercih edilir. Böylece geliştiriciler bir birlerini rahatsız etmez.
* lab2023 geliştiricilerine donanım, lisans vb unsurları alması için kredi verir, bu konuda maddi olarak destekler.
