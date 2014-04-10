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
$ git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
$ git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
$ rbenv install 2.0.0-p247
$ rbenv rehash
$ rbenv global 2.0.0-p247
$ ruby -v
# ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-linux]
```

Eğer yukarıdakı adımları izleyip ruby versiyonunu doğruladıysanız işlem tamamlanmış demektir. 
Artık Rbenv aktif ve ilgili ruby versiyonu sunucunuza kurulmuş demektir.

# RubyGems

Kurulumlara başlamadan önce rubygems'i güncellemek önerilir. Aşağıdaki komutu çalıştırın.

```bash
$ gem update --system
```

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
$ sudo add-apt-repository ppa:chris-lea/node.js
$ sudo apt-get update
$ sudo apt-get install nodejs
```

Evet. Deploy için gereken tüm temel bileşenleri sunucuya kurduk. Bu aşamadan sonra size bir veritabanı sunucusu gerekmekte.
Bunun için 2 yöntem tercih edebilirsiniz. 1. halihazırda kurduğunuz sunucunun üzerine bir veritabanı yönetim sistemi kurabilir
veya 2. bir veritabanı sunucusu oluşturabilirsiniz. Biz genellikle veritabanı ile application sunucusunu ayırmayı
tercih ettiğimizden bu sunucunun üzerine postgresql kurmuyoruz.

Ayrı bir sunucuda (veya bu sunucuda) jasıl Postgresql kurmanız gerektiğii öğrenmek istiyorsanız 
[PostgreSQL Veritabanı Kurulumu](https://github.com/lab2023/playbook/blob/master/development/database.md#kurulum) 
kaynağını ziyaret edebilirsiniz.

Veritabanı sunucunuz da hazırlandıktan sonra artık rails application'ununuz Capistrano ile deploy edebilirsiniz...

# Capistrano & Unicorn

`gem install capistrano`

Gemleri kurduktan sonra `capify .` komutunu çalıştıralım. Oluşan `config/deploy.rb` dosyasını aşağıdaki gibi düzenleyelim.

```ruby
require "bundler/capistrano"
#require "whenever/capistrano"

set :stages, %w(staging production)
set :default_stage, "production"
require 'capistrano/ext/multistage'

default_run_options[:pty] = true

set :whenever_command, "bundle exec whenever"

set :application, "project_name"
set :user, "deployer"
set :deploy_to, "/home/#{user}/apps/#{application}"

set :deploy_via, :remote_cache
set :use_sudo, false

set :scm, "git"
set :repository, "git@github.com:UserName/#{application}.git"
set :branch, "master"

default_run_options[:pty] = true
ssh_options[:forward_agent] = true

after "deploy", "deploy:cleanup" # keep only the last 5 releases


after "deploy:symlink", "deploy:update_crontab"

namespace :deploy do

  task :precompile, :role => :app do
    run "cd #{release_path}/ && rake assets:precompile"
  end

  after "deploy:finalize_update", "deploy:precompile"

  %w[start stop restart].each do |command|
    desc "#{command} unicorn server"
    task command, roles: :app, except: {no_release: true} do
      run "/etc/init.d/unicorn_#{application} #{command}"
    end
  end

  after "deploy:setup", "deploy:setup_config"

  task :symlink_config, roles: :app do
    run "ln -nfs #{shared_path}/config/database.yml #{release_path}/config/database.yml"
  end
  after "deploy:finalize_update", "deploy:symlink_config"

  desc "Make sure local git is in sync with remote."
  task :check_revision, roles: :web do
    unless `git rev-parse HEAD` == `git rev-parse origin/master`
      puts "WARNING: HEAD is not the same as origin/master"
      puts "Run `git push` to sync changes."
      exit
    end
  end
  before "deploy", "deploy:check_revision"

  task :install_bundler, :roles => :app do
    run "type -P bundle &>/dev/null || { gem install bundler --no-rdoc --no-ri; }"
  end
  before "deploy:cold", "deploy:install_bundler"

  desc "Update the crontab file"
  task :update_crontab, :roles => :db do
    #run "cd #{release_path} && whenever --update-crontab #{application}"
  end
  after "deploy:update_crontab", "deploy:resque_setup"

  desc "Resque QUEUE Start"
  task :resque_setup, :roles => :db do
    #run "cd #{release_path} && resque:work QUEUE='*'"
  end
end

# Production
set :default_environment, {
    'PATH' => "$HOME/.rbenv/shims:$HOME/.rbenv/bin:$PATH"
}

after "deploy", "deploy:cleanup"
```

`config/deploy/production.rb` ve `config/deploy/staging.rb` dosyalarını oluşturalım.

```ruby
server "2.2.2.2", :web, :app, :db, primary: true
set :port, 2222
set :rails_env, 'production'

namespace :deploy do
  task :setup_config, roles: :app do
    # Production
    sudo "ln -nfs #{current_path}/config/nginx.#{rails_env}.conf /etc/nginx/sites-enabled/#{application}"
    sudo "ln -nfs #{current_path}/config/unicorn_init_#{rails_env}.sh /etc/init.d/unicorn_#{application}"
    run "mkdir -p #{shared_path}/config"
    put File.read("config/database.example.#{rails_env}.yml"), "#{shared_path}/config/database.yml"
    puts "Now edit the config files in #{shared_path}."
  end
end
```

```ruby
server "1.1.1.1", :web, :app, :db, primary: true
set :port, 1111
set :rails_env, 'staging'

namespace :deploy do
  task :setup_config, roles: :app do
    # Staging
    sudo "ln -nfs #{current_path}/config/nginx.#{rails_env}.conf /etc/nginx/sites-enabled/#{application}"
    sudo "ln -nfs #{current_path}/config/unicorn_init_#{rails_env}.sh /etc/init.d/unicorn_#{application}"
    run "mkdir -p #{shared_path}/config"
    put File.read("config/database.example.#{rails_env}.yml"), "#{shared_path}/config/database.yml"
    puts "Now edit the config files in #{shared_path}."
  end
end
```

Gemfile a `gem 'unicorn'` ekleyelim. Öncelikle `config/unicorn.rb` dosyasını oluşturup Unicorn ayarlarını yapalım.

```ruby
@shared_dir = "/home/deployer/apps/project_name/shared/"
@working_dir = "/home/deployer/apps/project_name/current/"

worker_processes 2
working_directory @working_dir
timeout 30

listen "/tmp/sockets/unicorn_project_name.sock", :backlog => 64

pid_file = "#{@shared_dir}pids/unicorn.pid"
old_pid = "#{pid_file}.oldbin"

pid pid_file

stderr_path "#{@shared_dir}log/unicorn.stderr.log"
stdout_path "#{@shared_dir}log/unicorn.stdout.log"

preload_app true

# combine Ruby 2.0.0dev or REE with "preload_app true" for memory savings
# http://rubyenterpriseedition.com/faq.html#adapt_apps_for_cow
preload_app true
GC.respond_to?(:copy_on_write_friendly=) and
  GC.copy_on_write_friendly = true

check_client_connection false

before_fork do |server, worker|
  # the following is highly recomended for Rails + "preload_app true"
  # as there's no need for the master process to hold a connection
  defined?(ActiveRecord::Base) and
    ActiveRecord::Base.connection.disconnect!
end

after_fork do |server, worker|
  # the following is *required* for Rails + "preload_app true",
  defined?(ActiveRecord::Base) and
    ActiveRecord::Base.establish_connection
end

```

Daha sonra `config/unicorn_init_production.sh` ve `config/unicorn_init_staging.sh` 
dosyalarını oluşturalım. Dosyaları şu şekilde güncelleyelim.

* https://gist.github.com/muhammetdilek/d45a30d5fd26889ef5ea
* https://gist.github.com/muhammetdilek/d37e6b31d1b02e652255

Bu dosyalarda `project_name` kısmını proje ismiyle değiştirmeyi unutmayınız.

Ardından yukarıdaki dosyaları çalıştırılabilir hale getirmek için, aşağıdakı komutu konsoldan çalıştırın.

```bash
$ chmod +x config/unicorn_init_production.sh && chmod +x config/unicorn_init_staging.sh
```
Ardından;

`config/database.example.staging.yml` ve `config/database.example.production.yml` dosyalarını oluşturup 
staging ve production sunucu için kullancağınız veritabanı bilgilerini ilgili environment değerleri ile oluşturunuz.

`config/nginx.staging.conf` ve `config/nginx.production.conf` dosyasını oluşturup aşağıdaki gibi güncelleyiniz.
Bu aşamada eğer staging ve production sunucularında farklı nginx ayarları yapmak isterseniz dosyaları modifiye edebilirsiniz.
Örneğin. Staging sunucu cicin domain sadece ```stage.example.com``` şeklinde kullanılabilir.

```shell
 upstream project_name {
   server unix:/tmp/unicorn.project_name.sock fail_timeout=0;
 }

 server {
   listen 80;
   server_name *.example.com example.com;
   root /home/deployer/apps/project_name/current/public;

   location ^~ /assets/ {
     gzip_static on;
     expires max;
     add_header Cache-Control public;
   }

   try_files $uri/index.html $uri @project_name;
   location @project_name {
     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
     proxy_set_header Host $http_host;
     proxy_redirect off;
     proxy_pass http://project_name;
   }

   error_page 500 502 503 504 /500.html;
   client_max_body_size 4G;
   keepalive_timeout 10;
 }
```

`project_name` olan yerleri proje ismi ile değiştirmeyi unutmayınız.

Artık deploy için hazırız.

Proje dizininde;

*Staging deploy için*

`cap staging deploy:setup`
`cap staging deploy:cold`

*Production deploy için*

`cap deploy:setup`
`cap deploy:cold`

komutlarını çalıştırarak ilk deployumuzu yapıyoruz. Bundan sonraki deploylar için `cap staging deploy` 
veya `cap deploy` komutunu çalıştırmak yeterli olacaktır.

# Backup
Backup işlemleri için [backup](https://github.com/meskyanichi/backup) gemini kullanıyoruz. 
Veritabanı yedeği, assets(resim, video) yedekleri ve log yedeklerini almamız yeterli. 
Uygulamalarımızı githubda geliştirdiğimiz için uygulamanın yedeğini alma ihtiyacı duymuyoruz. 
Yedeği hem locale hemde yedek işlemleri için ayırdığımız sunucuya alıyoruz.

### Capistrano ile deploydan önce yedek almak

Deploydan önce yedek alacak komutu çalıştırtmalıyız. Tabi bunun için backup geminin kurulu olması gerekmektedir. Backup kurulum işleminide capistranoya yaptıralım.

Aşağıdaki task' i `deploy.rb` nin içine ekleyelim.

```ruby
namespace :deploy do
  task :configure_backup do
    on_rollback do
      puts 'I can not install backup gem.'
    end
    puts "Create backup model"
    run "backup generate:model -t #{application} --storages='local' --compressors='gzip' --databases='postgresql'"
    puts "Now edit ~/Backup/models/#{application}.rb"
  end
end
```

`cap deploy:cold` işleminden sonra bu task' i calıştırmak için şu satırı ekleyelim.

```ruby
after 'deploy:cold', 'deploy:configure_backup'
```
Sunucuda backup modelinizin bilgilerini değiştirmeyi unutmayın. `~/Backup/models/project_name.rb`

Şimdi de her deployan önce yedek alcak bir task yazalım.

```ruby
namespace :deploy do
  task :backup do
    transaction do
      on_rollback do
        puts 'I can not backup.'
      end
      run "backup perform --trigger #{application}"
    end

  end
end
```

Bunuda `deploy.rb` dosyasına ekleyelim. Her `cap deploy`işleminden önce bu task' i çalıştırmak için aşağıdaki satırı ekleyelim
```ruby
before 'deploy', 'deploy:backup'
```

### Log Yedekleri ve Log rotation
Log dosyalarının çok şişmesi genel problemimiz. Biz bunu nasıl çözüyoruz ? Linux logrotate kullanıyoruz. 
Logrotate log dosyalarını rotate ederek şişmesini önler.
Öncelikle kurulu değilse `sudo apt-get install logrotate` komutu ile log ratator'ı kuruyoruz.
Logrotate kullanmak için `/etc/logrotate.conf` dosyasına aşağıdaki kodları ekliyoruz.

```bash
# Rotate Rails application logs
/home/deployer/apps/project/current/log/*.log {
  daily #Bu işlemi günlük yap
  missingok # İşlem yapılacak log dosyaları eksik ise hata verme
  rotate 7 # 7 tane dosya tut
  compress # Sıkıştır gzip varsayılan
  delaycompress # Bir sonraki log ortasyonuna kadar sıkıştırmayı beklet. Yani sıkıştırma
  notifempty # Log dosyası boş ise rotate etme
  copytruncate # O anki yazılan log dosyasını rotate ederken rotate anında yazılan verile kaybetmemek için
  size 1024M # Magabayt olarak boyut 1024 olsun
}
```
Ardından logrotator günlük olarak çalışıp yedekleme işlemlerini yapacaktır
Eğer daha önceki log dosyalarını o an sıkıştırmak istersek

```bash
sudo logrotate -f /etc/logrotate.conf
```

komutuyla logrotator'ı çalıştırabiliriz.

Ayrıca log rotatorda işlenecek log dosyalarını görmek için

```bash
cat /var/lib/logrotate/status
```
komutunu kullanabiliriz.

Sıkıştırılmış log dosyalarının backup gemi ile yedeğini alıyoruz.

# Monitoring
## Exception Notification (Hata Bildirici)
Sunucudaki 500 hatalrından haberdar olmak için 
[exception_notification](https://github.com/smartinez87/exception_notification) gemini kulanıyoruz. 
Gem sunucu 500 verirse anında bize mail atıyor. 
Gemin kullanımı ile ilgili şu yazıyı http://www.muhammetdilek.com/blog/2013/04/04/exception-notification-hata-bildirici/ 
okuyabilirsiniz.

# Heroku

Hazırlanıyor...
