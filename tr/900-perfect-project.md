Bir uygulamanın müşterinin istediği şekilde tam ve eksiksiz çalışması onu mükemmel yapmaz! Çünkü müşterilerimiz bizim
kadar ne **pazarlama** ne de **teknik** bilgiye sahip değildir. Bir uygulamanın mükemmel olması için o uygulamanın 
müşterinin hayallerini gerçekleştirmesine yardımcı olması lazım.

Eğer müşterinin hayali sahibinden.com gibi bir siteye sahip olması ise bizim müşterimize o istemese bile aşağıdaki 
maddeleri tek tek anlatmamız ve projeye eklememiz gerekmektedir. Aksi halde uygulama müşterinin isteklerini gerçekleştirse
de hayallerini gerçekleştirmeyeceğinden mükemmel bir uygulama olmayacaktır.

# Uygulamanın Performansı ve Ölçeklenmesi

İyi bir yazılım performanslı ve ölçeklenebilir olması gerekir.

## Veritabanı

* Veritabanınında replikasyon
* Veritabanı tablolarında partition

## Statik içerikler

* Uygulamaların CDN desteği olmalıdır.

## Web server

* Uygulama birden fazla web servera dağıtılabilmelidir. Nginx load-blance

# Uygulamanın Pazarlama Stratejisine Uygunluğu

Bütün uygulamalarda pazarlama unsuru olacak diye bir kaide yok ancak startupların bir çoğunda pazarlama 
hatta internet üzerinden pazarlama vardır. Bir çok müşteri fikrine çok inanır ancak fikirler istedikleri 
kadar özgün olursa olsun pazarlama olmadan olmaz! Bizler müşterilerimize pazarlama konusunda da yardımcı
olmak zorundayız.

* Yapılan uygulamada bir pazarlama unsuru olacak mı? 
* Eğer olacaksa internet üzerinden tanıtım ve satış yapılacak mı?
* Müşterinin daha önce kullandığı bir CRM var mı?

## AARRR 

AARRR, [Dave McClure](https://twitter.com/davemcclure) tarafından internet projelerinin başarılarının ölçülmesini sağlayan beş aşamadan oluşan bir yöntemdir. 

Bizler yazılımlarmızı [AARRR](https://github.com/lab2023/playbook/blob/master/tr/901-AARRR.md) süreçlerini destekleyecek şekilde yazmaya özen gösteriyoruz.

## Satış Ortaklığı

## Davetiye Sistemi

## Widgets

# Uygulamanın Diğer Uygulamalar ile Entegrasyonu

## API

Her uygulamanın API'ye ihtiyacı yoktur ancak API'si olan uygulamalar ticari açıdan daha başarılıdırlar.

* https://github.com/applicake/doorkeeper

## JSON Response type

* Web uygulamalarına sadece kullanıcılar değil, mobil ve diğer web uygulamalarıda erişir. Eğer bir veri public ise bunun rahat bir şekilde kullanılabilmesi için JSON formatında da döndürülmesi gerekmektedir.

# Destek ve Geribildirim Servisler

Bir uygulama yapması gereken işleri yapmalıdır. Uygulama için destek, geri bildirim gibi ihtiyaçlar 3. parti servisler 
tarafından karşılanmalıdır.

Bizler destek için http://www.desk.com u öneriyoruz. Basitçe özellikleri

* Bilgi Havuzu
* Twitter, facebook, email ile gelen soruların bir yerde toplanması
* Canlı destek
* Özelleştirilebilmesi
* Esnek ödeme seçenekleri, 1. kullanıcı ücretsiz

Geri bildirim süreçleri için eğer desk.com çok fazla gelirse http://www.userreport.com/ servisini öneriyoruz. Bu serviste
ücretsizdir.



