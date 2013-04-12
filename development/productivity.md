# GIT, GITHUB, GITFLOW

## Git

## Github

## Git-flow

Git-flow [Vincent Driessen](http://nvie.com/) tarafından etkili dallanma (branching) yapmak için geliştirilmiştir.

Aşağıdaki dökümanlarda git-flow'un basit kullanımı anlatılmıştır. Daha detaylı kullanım için kaynakçada ki makale ve videoları izleyebilirsiniz.

### Temel İpuçları

* git-flow mükemmel bir komut satırı yardıma ve çıktısına sahiptir. Lütfen okuyun!
* [Sourcetree](http://www.sourcetreeapp.com/) ürünü git-flow için gui sağlıyor. Eğer komut satırı ile aranız yoksa değerlendirebilirsiniz.

### Kurulum

Kurulum esnasında git-flow dal (branch), yayım (release), etiket (tag) ön ekleri ile ilgili size sorular sorar. Bunların hepsini boş bırakırak enter tuşuna başıyoruz.

**OSX**

`brew install git-flow`

**Linux**

`apt-get install git-flow`

**Windows**

Şaka yapıyorsunuz... *nix çekirdekli bir makine kullanın.

### Başlayalım

Havuza (repository) git-flow'un kurulması için  `git flow init` kodu koşuyoruz. Unutmayın git-flow için sizin önceden git havuzunuz olmalıdır.

### Özellikler (Features)

* Yeni gelen release için geliştiricilerin eklediği yeni özellikler için
* Sadece mevcut develop havuzuna uygulanır.

#### Yeni özellik ekleme

* Diyelim ki size yeni bir görev verildi programa yeni bir özellik ekleyeceksiniz. O zaman develop dalından 

`git flow feature start NEW_FEATURE` 

kodunu çalıştıracaksınız. Bu kod size develop branchtan türemiş yeni bir dal varecektir.

#### Yeni özelliğin bitirilmesi

Yeni özelliği bitirilmesi

* NEW_FEATURE dalını develop dalına birleştirir (merge)
* NEW_FEATURE dalını kaldırır
* Varsayılan dalı develop yapar

`git flow feature finish NEW_FEATURE`

#### Yeni özelliği yayınlama

Eğer bu yeni özelliği birden fazla developer ile geliştiriyorsanız uzak sunucuyada göndermeniz gerekmektedir. Eğer sadece siz kodluyorsanız yapmayınız.

`git flow feature publish NEW_FEATURE`

#### Yayınlanmış bir özelliği alma

Eğer bir geliştiricinin yayınladığı özelliği almanız gerekiyorsa

`git flow feature pull NEW_FEATURE`

yapmalısınız.

### Yayım (release) yapma

* Yeni ürünüzün producta hazırlamanızı sağlar.
* Bu yapı ile ürünlerinize hotfix imkanı gelir ve yayım olunca otomatik etiketlenir.

#### Yayıma başlama

Yeni bir yayıma başlamak için git-flow'un `release` kodunu kullanırız. 

`git flow release start RELEASE` 

Örneğin `git flow release start 0.1.0` gibi

Eğer aynı özellik gibi yayımıda yayınlamak isterseniz 

`git flow release publish RELEASE` 

yapmanız gerekmektedir.

#### Yayımı bitirme

Bir yayımın bitmesi git-flow için büyük bir iştir. Aşağıdakileri yapar.

* release dalını master dalına birleştirir (merge)
* master dalını etiketler (tag)
* release dalını develop dalı ile birleştirir
* ilgili release dalını siler

### Düzeltmeler (Hotfixes)

* Kullanılmakta olan bir uygulamada beklenmeyen hatalar oluşabilir. Bunların hızlı bir şekilde düzenlenmesi gerekmektedir.
* Bu düzelmeler yeni bir versiyon ile tekrer sunucuya gönderilmelidir.

#### Düzenlemeye başlama

`git flow hotfix start VERSION`

#### Düzenlemeyi bitirme

`git flow hotfix finish VERSION` 

### Komutlar

* git flow init
* git flow feature start NEW_FEATURE
* git flow feature finish NEW_FEATURE
* git flow feature publish NEW_FEATURE
* git flow feature pull NEW_FEATURE
* git flow release start RELEASE
* git flow release publish RELEASE
* git flow release finish RELEASE
* git flow hotfix start VERSION
* git flow hotfix finish VERSION

**Kaynaklar**

* https://github.com/nvie/gitflow
* http://nvie.com/posts/a-successful-git-branching-model/
* http://danielkummer.github.com/git-flow-cheatsheet/
* http://buildamodule.com/video/change-management-and-version-control-deploying-releases-features-and-fixes-with-git-how-to-use-a-scalable-git-branching-model-called-gitflow
* http://vimeo.com/16018419
* http://vimeo.com/37408017