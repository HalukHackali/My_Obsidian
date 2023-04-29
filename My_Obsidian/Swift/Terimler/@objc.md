`@objc`, Swift dilinde bir özelliktir ve bir türün veya üyenin Objective-C tarafından erişilebilir olmasını sağlar. Bu özellik, bir tür veya üye Objective-C tarafından kullanılacaksa eklenir.

Objective-C, Swift ile tam uyumlu bir dil değildir ve Objective-C kodu ile Swift kodu arasında bazı farklılıklar vardır. `@objc` özelliği, bu farklılıkları telafi etmek için kullanılır ve Swift kodunu Objective-C tarafından erişilebilir hale getirir.

Örneğin, aşağıdaki örnek, `Person` adında bir sınıf tanımlar ve `@objc` özelliği kullanarak Objective-C tarafından erişilebilir hale getirir:
```swift
@objc class Person: NSObject {
    @objc var name: String
    @objc var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    @objc func sayHello() {
        print("Hello, my name is \(name) and I am \(age) years old.")
    }
}
```


Bu örnekte, `Person` sınıfı `@objc` özelliği ile işaretlenir ve `@objc` özellikleri ile etiketlenen `name`, `age` ve `sayHello()` üyeleri Objective-C tarafından erişilebilir hale getirilir.

Objective-C, özellikle iOS veya macOS gibi Apple platformlarında birçok API'nin yazıldığı bir dildir. Bu nedenle, Swift kodunun Objective-C tarafından erişilebilir olması, Swift ile Objective-C kodu arasındaki entegrasyonu kolaylaştırır ve uygulama geliştirme sürecini hızlandırır.