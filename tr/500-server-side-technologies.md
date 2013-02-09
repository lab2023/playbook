# Ruby ekosistemi

## Ruby

* http://www.ruby-lang.org
* https://www.ruby-toolbox.com

### Kaynaklar

**İnteraktif**

* http://tryruby.org/levels/1/challenges/0
* http://www.codeschool.com/courses/tag/ruby
* http://rubymonk.com/learning/books

**Videolar**

* http://www.lynda.com/Ruby-tutorials/essential-training/47905-2.html
* https://cooperpress.com/19walkthrough

**Kitaplar**

* http://www.amazon.com/Programming-Ruby-1-9-Pragmatic-Programmers/dp/1934356085
* http://www.amazon.com/Metaprogramming-Ruby-Program-Like-Pros/dp/1934356476/ref=pd_sim_b_9
* http://www.amazon.com/Practical-Object-Oriented-Design-Ruby-Addison-Wesley/dp/0321721330/ref=pd_sim_b_13
* http://www.amazon.com/Design-Patterns-Ruby-Russ-Olsen/dp/0321490452/ref=pd_sim_b_20

## Rack
## Rake
## Bundler Gemfile
## Rails
## Gems
* [to_xls](https://github.com/arydjmal/to_xls) Excel export yapar.
* [state_machine](https://github.com/pluginaweek/state_machine) Durum yönetimi yapıyor.
* [savon](https://github.com/savonrb/savon) SOAP client.
* [ransack](https://github.com/ernie/ransack) Arama ve sıralama.
* [whenever](https://github.com/javan/whenever) Zamanlanmış görevler.
* [resque](https://github.com/defunkt/resque) Arkaplan işlerini yönetir.
* [better_errors](https://github.com/charliesome/better_errors) - Rails' in standart error sayfasını daha kullanışlı bir sayafa ile değiştiriyor.
* [cancan](https://github.com/ryanb/cancan) - Kullanıcı yetkilendirmesi yapıyor.
* [client_side_validations](https://github.com/bcardarella/client_side_validations) - Modeldeki validasyonları alıp javascript ile client side' ta yapıyor.
* [compass-rails](https://github.com/chriseppstein/compass) - Sass mixin kütüphanesi.
* [devise](https://github.com/plataformatec/devise) - Kullanıcı authentication.
* [friendly_id](https://github.com/norman/friendly_id) - İnsancıl url üretir.
* [haml-rails](https://github.com/indirect/haml-rails) - Haml - Rails entegrasyonu yapar.
* [haml](http://haml-lang.com) - Markup language.
* [simple_form](https://github.com/plataformatec/simple_form) - Form generator.
* [bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass) Twitter Bootstrap' ın Sass versiyonunu Rails' e entegre ediyor.
* [bootstrap-wysihtml5-rails](https://github.com/Nerian/bootstrap-wysihtml5-rails) Bootstrap temalı HTML5 wysing editör.
* [bootstrap-datepicker-rails](https://github.com/Nerian/bootstrap-datepicker-rails) Bootstrap temalı date picker.
* [breadcrumbs_on_rails](https://github.com/weppos/breadcrumbs_on_rails) Breadcrumb(ekmek kırıntısı) için kullanıyoruz.
* [globalize3](https://github.com/svenfuchs/globalize3) Model katmanına çoklu dil desteği eklemek için kullanıyoruz.
* [devise_invitable](https://github.com/scambra/devise_invitable) Kullanıcı davet sistemi için kullanıyoruz. İsmindende anlaşılacağı gibi devise gemi ile birlikte çalışıyor.
* [sextant](https://github.com/schneems/sextant) Geliştirme sürecinde route' ları veiwde gösteren bir gem. rails 4 ile birlikte varsayılan olarak geliyor.
* [rails_panel](https://github.com/dejan/rails_panel) Geliştirme sürecinde sql sürelerini ve sayfa yüklenme sürelerini gösteriyor. Gemi kullanabilmek için [RailsPanel](https://chrome.google.com/webstore/detail/railspanel/gjpfobpafnhjhbajcjgccbbdofdckggg) chrome eklentisine iytiyacımız var.
* [rails_config](https://github.com/railsjedi/rails_config) Projeye config ayarları eklememizi sağlıyor.

# Background jobs
Kullancıyı süre olarak bekletecek işlemleri arkaplan işlerine alıyoruz.
## Resque
[resque](https://github.com/defunkt/resque) Arkaplan işlerini yönetir.
## resque_mailer
[resque_mailer](https://github.com/zapnap/resque_mailer) mailleri arkaplan işlerine alıyor.
# Full text search
Proje başlangıcında full text search kullanmıyoruz. Projenin ilerleyen aşamalarında durumuna göre entegre ediyoruz.
## Sphinx
Rails' te [thinking-sphinx](https://github.com/pat/thinking-sphinx) gem' i ile kullanıyoruz. Detaylı döküman http://pat.github.com/ts/en/
