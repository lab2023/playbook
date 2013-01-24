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

Ivar Jacobson söyle demiştir. "Her program görev süresince değişikliğe uğrar. Bu ilk sürümden ötesi düşünülen 
programların yazılımında göz önünde bulundurulmalıdır." Yani mutlaka ama mutlaka yazılımınız ileride gelen yeni 
istekleri karşılabilecek kapasitede olmalıdır. Sektörde müşterilerine yazılımları satıp yeni istekler gelince 
köşe bucak kaçan bir sürü yazılım firması vardır.

Bu prensibe göre programlar geliştirilmeye açık ama değiştirilmeye kapalı olmalıdır. Yani yeni bir istek geldiğinde
eski yazdığınız kodları değiştirmemeli yeni kodlar yazarak müşterinin yeni isteklerini karşılamalısınız. Kodlar
değişeme kapalı, geliştirilmeye açık olmalıdır. 

Basit bir örnek verelim. Müşterimiz bize AVEA ve Turkcell'den SMS atan bir program istedi diyelim. 

```ruby
class Sms
  send_sms number, msg
    if number is turkcell
      # Turkcell'den SMS gönder
    elsif number is avea
      # Avea'dan SMS gönder
    end
  end
end
```

Yukarıda kod tam bir beladır. İleride müşteriniz Vodofan'dan bir kampanya alırsanız. Yukarıda ki kodu switch'e çevirmeniz
gerekecektir. Yani eski yazdığınız kodu değiştirmeniz gerekecektir. Bunun yerine aşağıdaki kod daha kalitelidir.

```ruby
# Kadu yazalım

```

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
