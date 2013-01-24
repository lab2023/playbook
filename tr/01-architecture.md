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

Bu daha doğru bir yaklaşım emaili Email sınıfının, login logout işlemlerini Session sınıfının, hatta kullanıcının kaydedilip,
silinmesi işlemlerine DAO sınıfının bakması gerekmektedir. Eğer bir sınıfın birden fazla sorumluluğu olursa o sınıfın ileride
modifiye edilmesi yüksek bir olasılıktır ki buda açık kapalı prensibine aykırıdır.

## OCP	- Açık Kapalı Prensibi (Open/closed principle)
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
