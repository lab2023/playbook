# SOLID

## SRP	- Tek Sorumluluk Prensibi (Single responsibility principle)

Bir sınıfın tek bir sorumluluğu olmalıdır. Örneğin aşağıdaki `User` sınıfında kullanıcının yaratılması, silinmesi, 
kayıttan sonra email atılması, login logout olması gibi çok fazla sorumluluk vardır.

```ruby

class User
  attr_accessor :username, :password, :email
 
  def create username, password, email
    # Kodlar
  end
  
  def delete username
    # Kodlar
  end
  
  def send_register_email email
    # Kodlar
  end
  
  def login email, password
    # Kodlar
  end
  
  def logout email
    # Kodlar
  end
  
end
```

Daha doğru bir yaklaşım emaili Email sınıfının, login logout işlemlerini Session sınıfının, hatta kullanıcının kaydedilip,
silinmesi işlemlerine DAO sınıfının bakması gerekmektedir. Eğer bir sınıfın birden fazla sorumluluğu olursa o sınıfın ileride
modifiye edilmesi yüksek bir olasılıktır ki buda açık kapalı prensibine aykırıdır.


```ruby
class User
  attr_accessor :username, :password, :email
end
```


```ruby
class UserDao
  def create username, password, email
    # Kodlar
  end
  
  def delete username
    # Kodlar
  end
end
```


```ruby
class SendEmail
  def send_register_email user
    # Kodlar
  end
end
```


```ruby
class Session
  def login user, password
    # Kodlar
  end
  
  def logout user
    # Kodlar
  end
end
```

## OCP	- Açık Kapalı Prensibi (Open/closed principle)

Bu prensibe göre programlar geliştirilmeye açık ama değiştirilmeye kapalı olmalıdır.

Programcının görevi müşterisinin ihtiyacını çözmektir ancak müşterinin ihtiyaçları sürekli değişmektedir. Hiç bir
program zaman için müşterisinin ihtiyacını karşılamaya yetmeyecektir. Çevremizde müşterilerine eski programları 
satıp, yeni talepler gelince köşe bucak kaçan yazılım firmaları vardır.

Yazılımlara yeni talep gelmesi <b>doğal bir süreç</b>tir. Ivar Jacobson söyle demiştir. "Her program görev süresince
değişikliğe uğrar. Bu ilk sürümden ötesi düşünülen programların yazılımında göz önünde bulundurulmalıdır." Yani iyi bir 
yazılım kolay geliştirilebilen, projenin ilerleyen aşamalarında müşterinin diğer isteklerine destek verebilen bir 
yazılımdır.

Açık kapalı prensibine göre bir yazılıma yeni talepler geldiğinde, programcı yeni kodlar yazarak bunları karşılabilmelidir.
Eğer istenen yeni talep eski yazılan kodları değiştirmeyi gerekiyorsa eski kodlar açık kapalı prensibine uygun yazılmamış
demektir.

## LSP	- Liskov substitution principle
## ISP	- Interface segregation principle
## DIP	- Dependency inversion principle

# Design patterns

http://en.wikipedia.org/wiki/Design_pattern_(computer_science)

## Oluşturucu

### Factory
### Abstract Factory
### Singleton
### Builder
### Prototype

## Yapısal

### Adapter
### Bridge
### Facede
### Composite
### Decorator
### Proxy
### Flyweight

## Davranışsal

### Command
### Iterator
### Memento
### State
### Observer
### Strategy
### Chain of responsibility
### Mediator
### Visitor
### Template Method
