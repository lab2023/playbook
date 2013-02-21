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

## AARRR Metrics

* https://github.com/paulasmuth/fnordmetric

## Satış Ortaklığı

## Davetiye Sistemi

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



