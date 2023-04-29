Swift dilinde, `Access Control` (Erişim Kontrolü) bir öğenin (sınıf, yapı, özellik, fonksiyon vb.) diğer öğeler tarafından erişilebilirliğini kontrol etmek için kullanılır. Bu, Swift programlamasında gizlilik (encapsulation) ilkesinin uygulanmasına yardımcı olur.

`Access Control` dört seviyede uygulanabilir:

1.  `private`: Sadece tanımlandığı kapsamda erişilebilir. Örneğin, bir sınıfın özel bir fonksiyonu sadece o sınıfın diğer öğeleri tarafından erişilebilir.
    
2.  `fileprivate`: Sadece tanımlandığı dosyada erişilebilir. Örneğin, bir yapıda yerel bir değişkeni yalnızca o yapıda yer alan fonksiyonlar tarafından erişilebilir.
    
3.  `internal`: Sadece aynı modülde (proje) tanımlanan öğeler tarafından erişilebilir. Bu, varsayılan erişim seviyesidir.
    
4.  `public` ve `open`: Herhangi bir modülde erişilebilir. `public` seviyesi, başka modüller tarafından kullanılabilir, ancak kalıtım yoluyla değiştirilemez. `open` seviyesi, hem başka modüllerde kullanılabilir hem de kalıtım yoluyla değiştirilebilir.
    

Aşağıdaki örnek, erişim kontrolü seviyelerini göstermektedir:
```swift
public class Car {
    private var mileage: Int = 0
    
    public init() {}
    
    fileprivate func start() {
        print("The car has started.")
    }
    
    internal func drive() {
        print("The car is being driven.")
    }
    
    public func stop() {
        print("The car has stopped.")
    }
}

let car = Car()
car.start() // Fileprivate access, compile-time error.
car.drive() // Internal access, works fine.
car.mileage = 1000 // Private access, compile-time error.
car.stop() // Public access, works fine.
```

Bu örnekte:

`Car` sınıfı `public` olarak tanımlanmıştır, bu nedenle diğer modüller tarafından kullanılabilir. 

`mileage` özelliği `private` olarak tanımlanmıştır, bu nedenle sadece `Car` sınıfı içinde kullanılabilir. 

`start()` fonksiyonu `fileprivate` olarak tanımlanmıştır, bu nedenle yalnızca aynı dosya içindeki diğer öğeler tarafından erişilebilir. 

`drive()` fonksiyonu `internal` olarak tanımlanmıştır, bu nedenle aynı modüldeki diğer öğeler tarafından erişilebilir. 

`stop()` fonksiyonu `public` olarak tanımlanmıştır, bu nedenle diğer modüllerdeki öğeler tarafından erişilebilir ve sınıfın kalıtım yoluyla değiştirilmesine izin verilir.

---

`Access Control` seviyeleri, bir öğenin ne kadar gizli kalması gerektiğini belirleyen gizlilik ilkesi (encapsulation) gereği çok önemlidir. Özellikle büyük ölçekli projelerde, farklı modüller arasındaki iletişimde kullanılan öğelerin kontrol edilmesi ve sınıfların uygun bir şekilde korunması gerekmektedir. Ayrıca, doğru erişim seviyesi kullanarak hataları en aza indirmek ve programlama hatalarını önlemek de mümkündür.

---

`Access Control`'ün amacı, programlama hatalarını en aza indirgemek, sınıfların korunmasını sağlamak ve farklı modüller arasındaki iletişimi kontrol etmek gibi çeşitli amaçlarla kullanılır. Bu, yazılım geliştirme sürecinde önemli bir rol oynar, özellikle de büyük projelerde.

Ayrıca, `Access Control`'ü kullanarak bir sınıfın veya yapıların belirli özelliklerini gizleyerek, kullanıcıların sadece belirli bir arayüzle etkileşimde bulunmalarını sağlayabilirsiniz. Böylece, bir uygulamanın güvenliği arttırılabilir ve programlama hataları en aza indirilebilir.

`Access Control` seviyeleri, `internal` ve `public` olmak üzere ikiye ayrılır. `internal` varsayılan erişim seviyesidir ve yalnızca aynı modülde tanımlanan öğeler tarafından erişilebilir. `public` seviyesi ise herhangi bir modülde erişilebilir, ancak yalnızca başka bir modülde tanımlanan bir alt sınıf veya üye tarafından yeniden tanımlanamaz.

Bunun yanı sıra, Swift dilinde `open` erişim seviyesi de bulunur. `open`, `public` ile aynı seviyede olmasına rağmen, başka bir modülde tanımlanan bir alt sınıf veya üye tarafından yeniden tanımlanabilir. Bu, bir modülün başka bir modüle açık bir API sağlaması ve API'nin başka bir modül tarafından kullanılması amaçlanıyorsa, `open` kullanılabilir.

Aşağıdaki örnek, `Access Control`'ün temel kullanımını göstermektedir:
```swift
public class Vehicle {
    internal var speed: Int = 0
    
    fileprivate func startEngine() {
        print("Engine started.")
    }
    
    public func stopEngine() {
        print("Engine stopped.")
    }
}

class Car: Vehicle {
    private var mileage: Int = 0
    
    override init() {
        super.init()
        speed = 0
        mileage = 0
    }
    
    func drive() {
        print("Driving...")
    }
}

let car = Car()
car.drive()
car.startEngine() // Fileprivate access, compile-time error.
car.speed = 100 // Internal access, works fine.
car.mileage = 1000 // Private access, compile-time error.
car.stopEngine() // Public access, works fine.
```
