# Ruby Gems

## Client Side

### Twitter Bootstrap

#### bootstrap-saas
Twitter Bootstrap' ın Sass versiyonunu Rails' e entegre ediyor. 

* https://www.ruby-toolbox.com/categories/css_with_ruby#bootstrap-sass
* https://github.com/thomas-mcdonald/bootstrap-sass
* http://rubydoc.info/gems/bootstrap-sass/frames

#### bootstrap-wysihtml5-rails
Bootstrap temalı HTML5 wysing editör.

* https://www.ruby-toolbox.com/projects/bootstrap-wysihtml5-rails
* https://github.com/Nerian/bootstrap-wysihtml5-rails
* http://rubydoc.info/gems/bootstrap-wysihtml5-rails/frames

#### haml
Markup language.

* http://haml-lang.com
* https://www.ruby-toolbox.com/projects/haml
* https://github.com/haml/haml
* Ruby doc linki
* http://screencasts.org/episodes/introduction-to-haml
* http://www.youtube.com/watch?v=ILt6q_o2hts

#### haml-rails
Haml - Rails entegrasyonu yapar.

* https://www.ruby-toolbox.com/projects/haml-rails
* https://github.com/indirect/haml-rails
* Ruby doc linki
* http://screencasts.org/episodes/using-haml-with-rails-3

#### bootstrap-datepicker-rails
Bootstrap temalı date picker.

* ruby-toolbox linki
* https://github.com/Nerian/bootstrap-datepicker-rails
* Ruby doc linki

#### breadcrumbs_on_rails
Breadcrumb(ekmek kırıntısı) için kullanıyoruz.

* ruby-toolbox linki
* https://github.com/weppos/breadcrumbs_on_rails
* Ruby doc linki

#### client_side_validations
Modeldeki validasyonları alıp javascript ile client side' ta yapıyor.

* ruby-toolbox linki
* https://github.com/bcardarella/client_side_validations
* Ruby doc linki
* http://railscasts.com/episodes/263-client-side-validations

#### compass-rails
Sass mixin kütüphanesi.

* ruby-toolbox linki
* https://github.com/chriseppstein/compass
* Ruby doc linki
* http://railscasts.com/episodes/334-compass-css-sprites

#### simple_form
Form generator.

* ruby-toolbox linki
* https://github.com/plataformatec/simple_form
* Ruby doc linki
* http://railscasts.com/episodes/234-simple-form

#### chosen-rails
[chosen](https://github.com/harvesthq/chosen) javascript kütüphanesini projeye entegre etmemizi sağlıyor. Chosen uzun ve hantal select box' ları güzelleştiriyor.

* ruby-toolbox linki
* https://github.com/tsechingho/chosen-rails
* Ruby doc linki

#### cocoon
Nested formları yönetmemizi sağlıyor. Form generator için gem kullanıyorsanız Gemfile' da hemen o gemin altına ekleyiniz. Böyle olmadığı zaman production' da çalışmıyor. Alternatif olarak  https://github.com/ryanb/nested_form kullanılabilir. Fakat client side validasyonlarda sıkıntı çıkarıyor.

* ruby-toolbox linki
* https://github.com/nathanvda/cocoon
* http://rubydoc.info/gems/cocoon/1.1.2/frames

## Server Side

#### rails_config
Projeye config ayarları eklememizi sağlıyor.

* ruby-toolbox linki
* https://github.com/railsjedi/rails_config
* Ruby doc linki

#### to_xls
Excel export yapar.

* ruby-toolbox linki
* https://github.com/arydjmal/to_xls
* Ruby doc linki

#### state_machine
Durum yönetimi yapıyor.

* ruby-toolbox linki
* https://github.com/pluginaweek/state_machine
* Ruby doc linki
* http://railscasts.com/episodes/392-a-tour-of-state-machines

#### savon
SOAP client.

* ruby-toolbox linki
* https://github.com/savonrb/savon
* Ruby doc linki
* http://railscasts.com/episodes/290-soap-with-savon

#### ransack
Arama ve sıralama.

* ruby-toolbox linki
* https://github.com/ernie/ransack
* Ruby doc linki
* http://railscasts.com/episodes/370-ransack

#### whenever
Zamanlanmış görevler.

* ruby-toolbox linki
* https://github.com/javan/whenever
* Ruby doc linki
* http://railscasts.com/episodes/164-cron-in-ruby-revised

#### resque
Arkaplan işlerini yönetir.

* ruby-toolbox linki
* https://github.com/defunkt/resque
* Ruby doc linki
* http://railscasts.com/episodes/271-resque

#### cancan
Kullanıcı yetkilendirmesi yapıyor.

* ruby-toolbox linki
* https://github.com/ryanb/cancan
* Ruby doc linki
* http://railscasts.com/episodes/192-authorization-with-cancan

#### friendly_id
İnsancıl url üretir.

* ruby-toolbox linki
* https://github.com/norman/friendly_id
* Ruby doc linki
* http://railscasts.com/episodes/314-pretty-urls-with-friendlyid

#### devise
Kullanıcı authentication.

* ruby-toolbox linki
* https://github.com/plataformatec/devise
* Ruby doc linki
* http://railscasts.com/episodes/235-devise-and-omniauth-revised
* http://railscasts.com/episodes/209-devise-revised
* http://railscasts.com/episodes/209-introducing-devise
* http://railscasts.com/episodes/210-customizing-devise
* http://railscasts.com/episodes/233-engage-with-devise
* http://railscasts.com/episodes/235-omniauth-part-1
* http://railscasts.com/episodes/236-omniauth-part-2

#### globalize3
Model katmanına çoklu dil desteği eklemek için kullanıyoruz.

* ruby-toolbox linki
* https://github.com/svenfuchs/globalize3
* Ruby doc linki
* http://railscasts.com/episodes/338-globalize3


#### devise_invitable
Kullanıcı davet sistemi için kullanıyoruz. İsmindende anlaşılacağı gibi devise gemi ile birlikte çalışıyor.

* ruby-toolbox linki
* https://github.com/scambra/devise_invitable
* Ruby doc link

#### wice_grid
Twitter bootstrap tema uyumlu grid generator. Filtreleme, excel export, sayfalama mevcut.
* ruby-toolbox linki
* https://github.com/leikind/wice_grid
* http://rubydoc.info/gems/wice_grid/3.2.1/frames

#### enumerize
ActiveRecord ve i18n destekli enum türünde veri oluşturmamızı sağlıyor. Örneğin `homes` tablosundaki `home_type` alanı için model katmanında enumları belirleyerek kullanabiliriz. Simple Form desteği mevcut.
* ruby-toolbox linki
* https://github.com/brainspec/enumerize
* http://rubydoc.info/gems/enumerize/0.5.1/frames

#### validates_timeliness
Tarih validasyonları için kullanıyoruz.

* https://github.com/adzap/validates_timeliness

## Development Tools

#### sextant
Geliştirme sürecinde route' ları veiwde gösteren bir gem. rails 4 ile birlikte varsayılan olarak geliyor.

* ruby-toolbox linki
* https://github.com/schneems/sextant
* Ruby doc linki

#### better_errors
Rails' in standart error sayfasını daha kullanışlı bir sayafa ile değiştiriyor.

* ruby-toolbox linki
* https://github.com/charliesome/better_errors
* Ruby doc linki
* http://railscasts.com/episodes/402-better-errors-railspanel

#### binding_of_caller
Better errors için hata veren instancelerin inpectionlarının görünmesini sağlar.
Better Errors' advanced features(REPL, local/instance variable inspection, pretty stack frame names)

#### rails_panel & meta_request
Google chrome ile rails'ın debug edilmesine yarıyor.

* https://github.com/dejan/rails_panel
* https://www.ruby-toolbox.com/gems/meta_request
* http://railscasts.com/episodes/402-better-errors-railspanel

#### bullet
Uygulamadaki N+1 problemlerini tespit ediyor. 

* https://github.com/flyerhzm/bullet
* http://railscasts.com/episodes/372-bullet

#### annotate
Modellerin başlarına gerekli açıklamalari koyuyor.

* https://github.com/ctran/annotate_models
* http://rubydoc.info/gems/annotate/2.5.0/frames

## i18n Data

#### rails-i18n
Rails için bir çok dilde tarih, saat, pluralization vb i18n dosyalarını barındırır.

* https://github.com/svenfuchs/rails-i18n/

#### devise-i18n
Devise geminin bir çok dilde i18n dasyalarını barındırır.

* https://github.com/tigrish/devise-i18n

#### i18n_generators
Modellerin locale dosyalarını oluşturur ve eski dosyalar ile senkronize eder.

* http://github.com/amatsuda/i18n_generators
* 
