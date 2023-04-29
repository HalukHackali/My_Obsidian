#swift #yazılım 

Swift, karmaşık veri tipleri oluşturmak için Class (sınıf) adında bir başka yola daha sahiptir. Struct'lara (yapı) benzer, ama şunları da içeren bazı önemli farklılıkları vardır:

-   Class'larınızla birlikte otomatik bir üyelik başlatıcısı gelmez; kendiniz yazmanız gerekir.
-   İstediğiniz yeni şeyleri ekleyerek, başka bir Class'ı temel alan bir Class tanımlayabilirsiniz.
-   Bir Class'ın örneğini oluşturduğunuz zaman, artık o bir nesne (object) olarak anılır. Eğer bu nesneyi kopyalarsanız, ön tanımlı olarak ikisi de aynı veriyi kopyalar; birini değiştirirseniz, diğer kopya da değişir.

Bu üçü de büyük farklardır. Ben de devam etmeden önce, bunları derinlemesine ele alacağım.

## Bir nesneyi başlatma

Eğer bizim `Person` struct'ını `Person` class'ına döndürseydik, Swift şu şekilde yazmamıza izin vermezdi:

```swift
class Person {
    var clothes: String
    var shoes: String
}
```

Bunun sebebi, hatırlarsanız daha önce söylediğimiz gibi, mutlaka bir değere sahip olması gereken iki `String` tipinde değer tanımladığımız içindir. Struct için bir sorun yok, çünkü Swift bu iki özelliğe değer vermemiz için bizi zorlayarak, üyelik başlatıcıyı otomatik olarak üretiyor. Ama class'larda durum böyle değil, o yüzden Swift verilecek değerden emin olamıyor.

Bunun için üç tane çözüm var: İki değeri de optional String yapmak, veya onlara birer başlangıç değeri atamak, ya da kendi başlatıcımızı yazmak. İlk seçenek, tüm kod geneline gerek olmasa da optional'ları tanıtıyor. İkinci seçenek işe yarar, ama bu başlangıç değerleri gerçekten kullanılmadıkça ziyan edilmiş olurlar. Geriye kalan üçüncü seçenek, kesinlikle doğru olan: Kendi başlatıcımızı yazmak.

Bunu yapmak için, class içerisinde bizi ilgilendiren iki parametreyi alan ve `init()` adında bir metod oluşturun:

```swift
class Person {
    var clothes: String
    var shoes: String

    init(clothes: String, shoes: String) {
        self.clothes = clothes
        self.shoes = shoes
    }
}
```

Bu kodda dikkatinizi çekebilecek iki şey var: 

İlki, `init()` metodundan önce `func`yazmayacaksınız, çünkü bu özel bir metoddur. İkincisi ise, parametre adları ile atamak istediğiniz özellik adları aynı olduğu için `self.` kullanın. Kolayca kavramanız için şöyle söyleyebiliriz: "Bu nesnenin `clothes` özelliği, değerini aktaracağı `clothes` parametresiyle aynı olması gerekli". İstediğiniz isimleri verebilirsiniz onlara, tamamen size kalmış.

**Önemli:** Swift, başlatıcının sonuna kadar optional olmayan tüm özelliklerin bir değere sahip olmasını gerektirir veya o zamana kadar başlatıcı, herhangi bir diğer metodu çağırır; artık hangisi önce gelirse. 

## Class inheritance (Sınıf kalıtsallığı)

Struct'lar ve class'lar arasındaki ikinci önemli fark, _sınıf kalıtsallığı_ olarak da bilinen daha büyük şeyler üretmek için birbiri üzerine kurulabilir. Bu teknik, en basit programlarda bile yoğun bir şekilde Cocoa Touch içinde kullanılır, o yüzden iyi bir şekilde anlamanız gerekli.

Basit birşeyle başlayalım: name (isim) ve age (yaş) özellikleri olan bir `Singer` class'ı oluşturalım. Metodlar olarak, özelliklere değer atayabilmek için basit bir başlatıcı olacak, bir de birkaç sözcük yazdıracak olan `sing()` metodu:

```swift
class Singer {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func sing() {
        print("La la la la")
    }
}
```

Başlatıcıyı çağırarak bu nesnenin bir örneğini oluşturalım şimdi. Ardından da özelliklerini yazdıralım ve metodunu çağıralım:

```swift
var taylor = Singer(name: "Taylor", age: 25)
taylor.name
taylor.age
taylor.sing()
```

İşte bizim basit class'ımız, ama onun üzerinde çalışmaya devam edeceğiz: `Singer` class'ının yaptığı her şeyi yapan, ama `sing()` metodunu çağırdığımda "Trucks, guitars, and liquor" yazmasını istediğim bir `CountrySinger` sınıfı tanımlamak istiyorum.

Orjinal `Singer` class'ını yeni oluşturduğun `CountrySinger` class'ına tabiki de kopyalayabilirdin. Ama bu programlamanın tembel bir şekli. Hem sonrasında `Singer` class'ında bir değişiklik yapıp, diğerinde yapmayı unutursan bu değişiklikler geri gelip seni bulur. Bunun yerine, Swift'in daha akıllıca bir çözümü var: `Singer`class'ını baz alarak `CountrySinger` sınıfını oluşturabiliriz. Böylece oluşturmamız gereken tüm bu özellikler ve metodlar bize hazır gelmiş olur:

```swift
class CountrySinger: Singer {

}
```

Bu iki nokta üst üste sihrin oluştuğu şeydir: "`CountrySinger` class'ı `Singer` class'ını genişletir" anlamına gelir. Artık yeni `CountrySinger` class'ı (subclass –alt sınıf– olarak adlandırılır), `Singer` class'ına (parent class veya superclass –ana sınıf veya süper sınıf– olarak adlandırılır) hiçbir şey eklemez. Biz de zaten kendi has `sing()` metodu olsun istiyoruz, ama Swift dilinde yeni bir anahtar sözcük daha öğrenmeniz gerekli: `override`. Bunun anlamı "Bu metodun parent class'ımda tanımlandığını biliyorum, ama bu subclass için bunu değiştirmek istiyorum"dur.

`override` anahtar sözcağüne sahip olmak faydalı bir şey, çünkü ne yapmak istediğinizi açıklığa kavuşturuyor. Aynı zamanda Swift'in kodunuzu kontrol etmesini sağlıyor: Eğer `override`kullanmasaydınız, Swift superclass'ınızdan gelen metodu değiştirmenize izin vermeyecekti veya `override` kullansaydınız ama geçersiz kılacağınız (override) birşey olmasaydı, Swift hatanızı size işaret edecekti.

O yüzden, aşağıdaki gibi bir `override func`kullanmamız gerekiyor:

```swift
class CountrySinger: Singer {
    override func sing() {
        print("Trucks, guitars, and liquor")
    }
}
```

Şimdi `taylor` nesnesinin oluşturulma şeklini değiştirin:

```swift
var taylor = CountrySinger(name: "Taylor", age: 25)
taylor.sing()
```

Eğer `CountrySinger` nesnesini sadece `Singer`nesnesine değiştirirseniz, sonuç panelinde beliren farklı mesajları görebilmeniz gerekiyor.

Şimdi birşeyleri karmaşıklaştıralım ve `HeavyMetalSinger` adıyla yeni bir class tanımlayalım. Ama bu kez, heavy metal şarkıcının mikrofonundan geçen çığlığın ne kadar gürültülü olduğunu belirleyen `noiseLevel` (gürültü seviyesi) adını verdiğimiz bir özelliği saklayacağız.

Bu bir soruna sebep olur ve çok özel bir şekilde çözülmeyi gerektirir:

-   Swift dili, tüm optional olmayan özelliklerin bir değere sahip olmasını ister.
-   `Singer` class'ımız `noiseLevel` özelliğine sahip değildir.
-   O yüzden, bu gürültü seviyesini kabul eden `HeavyMetalSinger` için ısmarlama bir başlatıcı oluşturmamız gerekiyor. 
-   Bu yeni başlatıcı aynı zamanda heavy metal şarkıcısının `name` ve `age` özelliklerini bilmeye ihtiyacı var. Bunu `Singer` superclass'ı aracılığıyla değer geçebilir.
-   Superclass'taki veriye değer geçmek metodun çağrılmasıyla yapılır ve özelliklerinizin hepsine değer verene kadar başlatıcıdaki metod çağrılarını yapamazsınız.
-   O yüzden, önce özelliğimizi ayarlamamız gerekiyor (`noiseLevel`), ardından da kullanılacağı superclass için diğer parametreleri geçersiniz.

Bu size korkunç bir şekilde karışık gelebilir, ama kodun içinde doğrudan oluyor. Burada `HeavyMetalSinger` class'ını, kendi `sing()`metoduyla tamamlayın:

```swift
class HeavyMetalSinger: Singer {
    var noiseLevel: Int

    init(name: String, age: Int, noiseLevel: Int) {
        self.noiseLevel = noiseLevel
        super.init(name: name, age: age)
    }

    override func sing() {
        print("Grrrrr rargh rargh rarrrrgh!")
    }
}
```

Başlatıcının nasıl üç parametre aldığına ve ardından `Singer` superclass'ındaki `name` ve `age`değişkenlerine değer geçmek için `super.init()`çağrısına dikkat edin; ama tabi sadece kendi özellikleri ayarlandıktan sonra. Nesnelerle çalışırken `super` ifadesini çoğu kez göreceksiniz. Bu sadece "türetiğim sınıfın metodunu çağır" anlamına geliyor. Genellikle "önce parent class'ımın ihtiyaç duyduğu her şeyi yapmasına izin ver, sonrasında ben fazladan birşeyler yapacağım" anlamında kullanılır.

Sınıf kalıtsallığı büyük bir konudur, o yüzden henüz tam olarak anlamadıysanız üzülmeyin. Zaten, bilmeniz gereken bir şey daha var: Sınıf kalıtsallığı sıklıkla birçok aşamaya yayılır. Örneğin A, B'den türemiş olabilir ve B ise C'den türemiş olabilir, hatta C de D'den türemiş olabilir. Bu böyle gider. Bu, yazdığınız kodun modüler ve anlamasının kolay olmasına yardımcı olan class'ları fonksiyonel bir şekilde kurmanıza ve yeniden kullanmanıza izin verir.

## Objective-C koduyla çalışmak

Eğer Swift class metodlarınızı çağıran Apple'ın işletim sisteminin bazı parçalarına sahip olmak istiyorsanız, özel bir nitelik ile onu işaretlemeniz gerekir: `@objc`. Bu, “Objective-C”nin kısaltmasıdır ve çoğunlukla tüm iOS, macOS, watchOS ve tvOs için olan daha eski Objective-C kodunu çalıştıran metodu etkin bir şekilde işaretleyen niteliktir. Örneğin, bir saniye geçtikten sonra metodunuzun çağrılmasını sisteme söylemek için, onu `@objc` ile işaretlemeniz gerekli.

Şimdilik `@objc` konusuna çok takılmayın; sadece devam eden konular içinde onu açıklamaya çalışmayacağım, aynı zamanda Xcode da her zaman bunu sana gerektiğinde söyleyecek. Alternatif olarak, eğer bireysel metodlar için `@objc`kullanmak istemezseniz, otomatik olarak Objective-C için class'ınız tüm metodlarını uygun hale getirmeden önce `@objcMembers`koyabilirsiniz.

## Değerler ve referanslar

Bir struct'ı kopyaladığınızda, tüm değerleriyle birlikte her şey çoğaltılır. Bu, bir struct'ın bir kopyasını değiştirerek, diğer kopyaların değiştiremeyeceğiniz anlamına gelir; hepsi bireyseldir. Class'larla, bir nesnenin her bir kopyası aynı orjinal nesneyi işaret eder. Yani birini değiştirirseniz, hepsini değiştirmiş olursunuz. Swift struct'ları "değer tipleri" olarak tanımlar, çünkü onlar sadece bir değeri işaret eder. Ama class'lar "referans tipleri"ndendir, çünkü nesneler gerçek değerlerin paylaşımlı referanslarıdır.

Bu önemli bir farktır ve struct'lar ile class'lar arasında seçimin önemli olduğu anlamına gelir:

-   Eğer, değer geçilmesi ve yerinde değiştirilmesi için paylaşımlı bir hale sahip olmak istiyorsanız, class'ları arıyorsunuz demektir. Fonksiyonların içine onları aktarırsınız veya dizilerde saklarsınız, orada değiştirirsiniz ve programın kalan kısmına bu değişiklikleri yansıtırsınız.
-   Eğer, bir kopya değiştiğinde diğerlerini etkilemesini istiyor ve paylaşımlı bir durumdan kaçınıyorsanız, o zaman struct'ları arıyorsunuz demektir. Fonksiyonların içine onları aktarırsınız veya dizilerde saklarsınız, orada değiştirirsiniz, ama referans olduğu başka hiçbir yerde değişmezler.

Struct'lar ve Class'lar arasındaki anahtar farkı özetlemem gerekseydi, şunu söylerdim: Class'lar daha esnek, ama struct'lar daha güvenli. Basit bir kural olarak, belirli bir neden dolayı ihtiyaç duyana kadar, her zaman struct'ları kullanmalısınız.

---

# Kendi sınıflarınızı nasıl oluşturabilirsiniz?

`String`Swift, , `Int`, `Double`ve dahil olmak üzere veri türlerinin çoğunu depolamak için yapıları kullanır , ancak özel veri türleri oluşturmanın _sınıflar adı verilen_ _başka bir_`Array` yolu vardır . Bunların yapılarla pek çok ortak noktası vardır, ancak kilit noktalarda farklıdırlar.

İlk olarak, sınıfların ve yapıların ortak noktaları şunlardır:

-   Onları yaratıp adlandırabilirsin.
-   Özellik gözlemcileri ve erişim denetimi dahil olmak üzere özellikler ve yöntemler ekleyebilirsiniz.
-   Yeni örnekleri istediğiniz gibi yapılandırmak için özel başlatıcılar oluşturabilirsiniz.

Ancak, sınıflar yapılardan beş temel noktada farklılık gösterir:

1.  Bir sınıfın başka bir sınıftaki işlevsellik üzerine inşa edilmesini sağlayabilir, tüm özelliklerini ve yöntemlerini başlangıç ​​noktası olarak alabilirsiniz. Bazı yöntemleri seçici olarak geçersiz kılmak istiyorsanız, bunu da yapabilirsiniz.
2.  Bu ilk noktadan dolayı, Swift otomatik olarak sınıflar için üye bazında bir başlatıcı oluşturmaz. Bu, kendi başlatıcınızı yazmanız veya tüm özelliklerinize varsayılan değerler atamanız gerektiği anlamına gelir.
3.  Bir sınıfın örneğini kopyaladığınızda, her iki kopya da aynı verileri paylaşır - bir kopyayı değiştirirseniz diğeri de değişir.
4.  _Bir sınıf örneğinin son kopyası yok edildiğinde, Swift isteğe bağlı olarak deinitializer_ adı verilen özel bir işlevi çalıştırabilir .
5.  Bir sınıfı sabit yapsanız bile, değişken oldukları sürece özelliklerini değiştirebilirsiniz.

Yüzeyde bunlar muhtemelen oldukça rastgele görünüyor ve zaten yapılarımız varken sınıflara neden ihtiyaç duyulduğunu merak ediyor olabilirsiniz.

Bununla birlikte, SwiftUI, sınıfları, özellikle 3. nokta için kapsamlı bir şekilde kullanır: bir sınıfın tüm kopyaları aynı verileri paylaşır. Bu, uygulamanızın birçok bölümünün aynı bilgileri paylaşabileceği anlamına gelir, böylece kullanıcı bir ekranda adını değiştirirse diğer tüm ekranlar bu değişikliği yansıtacak şekilde otomatik olarak güncellenir.

Diğer noktalar _önemlidir_ , ancak kullanımları farklıdır:

1.  Bir sınıfı diğerine göre oluşturabilmek, Apple'ın eski UI çerçevesi UIKit'te gerçekten önemlidir, ancak SwiftUI uygulamalarında çok daha az yaygındır. UIKit'te, A sınıfının B sınıfı üzerine, C sınıfı üzerine, D sınıfı üzerine vb. inşa edildiği uzun sınıf hiyerarşilerine sahip olmak yaygındı.
2.  Üye bazında bir başlatıcının olmaması can sıkıcıdır, ancak bir sınıfın diğerine dayanabileceği göz önüne alındığında uygulamanın neden zor olduğunu anlayabilirsiniz - eğer C sınıfı fazladan bir özellik eklerse, C, B ve A için tüm başlatıcıları bozar.
3.  Sabit bir sınıfın değişkenlerini değiştirebilmek, sınıfların çoklu kopyalama davranışına bağlanır: sabit bir sınıf, kopyamızın işaret ettiği potu değiştiremeyeceğimiz anlamına gelir, ancak özellikler değişkense, yine de potun _içindeki_ verileri değiştirebiliriz. Bu, bir yapının her bir kopyasının benzersiz olduğu ve kendi verilerini tuttuğu yapılardan farklıdır.
4.  Bir sınıfın bir örneğine birkaç yerde başvurulabileceğinden, son kopyanın ne zaman yok edildiğini bilmek önemli hale gelir. Başlatma kaldırıcının devreye girdiği yer burasıdır: son kopya kaybolduğunda ayırdığımız tüm özel kaynakları temizlememizi sağlar.

Bitirmeden önce, bir sınıf oluşturan ve kullanan küçük bir kod dilimine bakalım:

```swift
class Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var newGame = Game()
newGame.score += 10
```

`class`Evet, bununla bir yapı arasındaki tek fark, bunun yerine kullanılarak oluşturulmuş olmasıdır `struct`– geri kalan her şey aynıdır. Bu, derslerin gereksiz görünmesine neden olabilir, ancak bana güvenin: Aralarındaki beş farkın tümü önemlidir.

Sonraki bölümlerde sınıflar ve yapılar arasındaki beş fark hakkında daha fazla ayrıntıya gireceğim, ancak şu anda bilinmesi gereken en önemli şey şudur: yapılar önemlidir ve sınıflar da önemlidir - SwiftUI kullanırken her ikisine de ihtiyacınız olacak _._

---

# Bir sınıfın diğerinden miras alması nasıl sağlanır?

_Swift, kalıtım_ olarak bilinen bir süreç olan mevcut sınıfları temel alarak sınıflar oluşturmamıza izin verir . Bir sınıf, başka bir sınıftan (“ebeveyn” veya “süper” sınıf) işlevsellik devraldığında, Swift, yeni sınıfa (“alt sınıf” veya “alt sınıf”) o üst sınıfın özelliklerine ve yöntemlerine erişim verir. yeni sınıfın davranış biçimini özelleştirmek için küçük eklemeler veya değişiklikler yapmak.

Bir sınıfın diğerinden miras almasını sağlamak için alt sınıfın adından sonra iki nokta üst üste koyun ve ardından üst sınıfın adını ekleyin. Örneğin, burada `Employee`bir özelliği ve bir başlatıcısı olan bir sınıf var:

```swift
class Employee {
    let hours: Int

    init(hours: Int) {
        self.hours = hours
    }
}
```

`Employee`Her biri özelliği ve başlatıcıyı kazanacak iki alt sınıfı oluşturabiliriz `hours`:

```swift
class Developer: Employee {
    func work() {
        print("I'm writing code for \(hours) hours.")
    }
}

class Manager: Employee {
    func work() {
        print("I'm going to meetings for \(hours) hours.")
    }
}
```

Bu iki alt sınıfın nasıl doğrudan atıfta bulunabileceğine dikkat edin `hours`- sanki bu özelliği kendileri eklemişler gibi, kendimizi tekrarlamak zorunda kalmamamız dışında.

Bu sınıfların her biri öğesinden miras alır `Employee`, ancak daha sonra her biri kendi özelleştirmesini ekler. Dolayısıyla, her birinin bir örneğini oluşturup çağırırsak `work()`, farklı bir sonuç elde ederiz:

```swift
let robert = Developer(hours: 8)
let joseph = Manager(hours: 10)
robert.work()
joseph.work()
```

Özellikleri paylaşmanın yanı sıra, daha sonra alt sınıflardan çağrılabilen yöntemleri de paylaşabilirsiniz. Örnek olarak, bunu sınıfa eklemeyi deneyin `Employee`:

```swift
func printSummary() {
    print("I work \(hours) hours a day.")
}
```

`Developer`öğesinden miras aldığı için , bunun gibi örneklerini `Employee`hemen çağırmaya başlayabiliriz :`printSummary()``Developer`

```swift
let novall = Developer(hours: 8)
novall.printSummary()
```

Miras aldığınız bir yöntemi değiştirmek istediğinizde işler biraz _daha karmaşıklaşıyor._ `printSummary()`Örneğin, içine koyduk `Employee`, ama belki bu alt sınıflardan biri biraz farklı davranış istiyor.

`override`Burası Swift'in basit bir kuralı uyguladığı yerdir: Bir alt sınıf, bir üst sınıftan bir yöntemi değiştirmek istiyorsa, alt sınıfın sürümünde kullanmalısınız . Bu iki şey yapar:

1.  Kullanmadan bir yöntemi değiştirmeye çalışırsanız `override`, Swift kodunuzu oluşturmayı reddedecektir. Bu, yanlışlıkla bir yöntemi geçersiz kılmanızı engeller.
2.  Kullanırsanız `override`, ancak yönteminiz aslında üst sınıftan bir şeyi geçersiz kılmazsa, muhtemelen bir hata yaptığınız için Swift kodunuzu oluşturmayı reddedecektir.

Dolayısıyla, geliştiricilerin benzersiz bir yöntemi olmasını isteseydik `printSummary()`, bunu sınıfa eklerdik `Developer`:

```swift
override func printSummary() {
    print("I'm a developer who will sometimes work \(hours) hours a day, but other times spend hours arguing about whether code should be indented using tabs or spaces.")
}
```

Swift, yöntem geçersiz kılma işlemlerinin nasıl çalıştığı konusunda akıllıdır: üst sınıfınız `work()`hiçbir şey döndürmeyen bir yönteme sahipse, ancak alt sınıfınız, `work()`işin nerede yapıldığını belirtmek için bir dize kabul eden bir yönteme sahipse, bu gerekli _değildir_`override` çünkü değiştirmiyorsunuz ana yöntem.

**İpucu:** Sınıfınızın mirası desteklememesi gerektiğinden eminseniz, bunu olarak işaretleyebilirsiniz `final`. _Bu, sınıfın kendisinin başka şeylerden miras alabileceği, ancak miras_ almak için kullanılamayacağı anlamına gelir - hiçbir alt sınıf, ebeveyni olarak son bir sınıfı kullanamaz.

---

# sınıflar için başlatıcılar nasıl eklenir

Swift'deki sınıf başlatıcıları, yapı başlatıcılarından daha karmaşıktır, ancak biraz kurnazlıkla gerçekten önemli olan kısma odaklanabiliriz: bir alt sınıfın herhangi bir özel başlatıcısı varsa, kendi ayarını bitirdikten sonra her zaman _ebeveynin_ başlatıcısını çağırmalıdır. varsa özellikleri.

Daha önce söylediğim gibi, Swift otomatik olarak sınıflar için üye bazında bir başlatıcı oluşturmayacak. Bu, kalıtım olsa da olmasa da geçerlidir - sizin için hiçbir zaman üye bazında bir başlatıcı oluşturmaz. Bu nedenle, ya kendi başlatıcınızı yazmanız ya da sınıfın tüm özellikleri için varsayılan değerler sağlamanız gerekir.

Yeni bir sınıf tanımlayarak başlayalım:

```swift
class Vehicle {
    let isElectric: Bool

    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}
```

Bu, tek bir Boole özelliğine ve bu özelliğin değerini ayarlamak için bir başlatıcıya sahiptir. Unutmayın, burada kullanmak, parametreyi aynı ada sahip özelliğe `self`atadığımızı açıkça gösterir .`isElectric`

`Car`Şimdi, miras alan bir sınıf yapmak istediğimizi varsayalım `Vehicle`- şöyle bir şey yazmaya başlayabilirsiniz:

```swift
class Car: Vehicle {
    let isConvertible: Bool

    init(isConvertible: Bool) {
        self.isConvertible = isConvertible
    }
}
```

Ancak Swift bu kodu oluşturmayı reddedecek: sınıfın bunun elektrikli olup olmadığını bilmesi gerektiğini söyledik `Vehicle`, ancak bunun için bir değer sağlamadık.

Swift'in bizden yapmamızı istediği, hem ve hem de `Car`içeren bir başlatıcı sağlamak , ancak kendimizi depolamaya çalışmak yerine onu aktarmamız gerekiyor - süper sınıftan kendi başlatıcısını çalıştırmasını istememiz gerekiyor.`isElectric``isConvertible``isElectric`

İşte böyle görünüyor:

```swift
class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)
    }
}
```

`super`Swift'in bizim için otomatik olarak sağladığı değerlerden bir diğeri, şuna benzer `self`: başlatıcısı gibi üst sınıfımıza ait yöntemleri çağırmamıza izin verir. Dilerseniz diğer yöntemlerle de kullanabilirsiniz; başlatıcılarla sınırlı değildir.

`Car`Artık her iki sınıfımızda da geçerli bir başlatıcımız olduğuna göre, şöyle bir örnek oluşturabiliriz :

```swift
let teslaX = Car(isElectric: true, isConvertible: false)
```

**İpucu:** Bir alt sınıfın kendi başlatıcılarından hiçbiri yoksa, üst sınıfının başlatıcılarını otomatik olarak devralır.

---
# sınıflar nasıl kopyalanır

Swift'te, bir sınıf örneğinin tüm kopyaları aynı verileri paylaşır, yani bir kopyada yaptığınız herhangi bir değişiklik otomatik olarak diğer kopyaları da değiştirir. Bunun nedeni, sınıfların Swift'te _referans türleri_olmasıdır; bu, bir sınıfın tüm kopyalarının hepsinin aynı temel veri kabına geri _gönderme yaptığı anlamına gelir._

Bunu çalışırken görmek için şu basit sınıfı deneyin:

```swift
class User {
    var username = "Anonymous"
}
```

Bunun yalnızca bir özelliği vardır, ancak bir sınıf içinde depolandığı için sınıfın tüm kopyalarında paylaşılacaktır.

Böylece, o sınıfın bir örneğini oluşturabiliriz:

```swift
var user1 = User()
```

Daha sonra bir kopyasını alıp değeri `user1`değiştirebiliriz `username`:

```swift
var user2 = user1
user2.username = "Taylor"
```

Umarım bunun nereye gittiğini görürsünüz! Şimdi kopyanın özelliğini değiştirdik, `username`ardından her farklı kopyadan aynı özellikleri yazdırabiliriz:

```swift
print(user1.username)  
print(user2.username)
```

…ve bu her ikisi için de “Taylor” yazacak – örneklerden yalnızca birini değiştirsek de diğeri de değişti.

Bu bir hata gibi görünebilir, ancak aslında bir özelliktir ve aynı zamanda gerçekten önemli bir özelliktir çünkü bu, uygulamamızın tüm bölümlerinde ortak verileri paylaşmamızı sağlayan şeydir. Göreceğiniz gibi, SwiftUI, özellikle çok kolay paylaşılabildikleri için, verileri için büyük ölçüde sınıflara güvenir.

Karşılaştırıldığında, yapılar verilerini kopyalar arasında _paylaşmazlar_`class User` , yani kodumuzda olarak değiştirirsek `struct User`farklı bir sonuç alırız: "Anonim" sonra "Taylor" yazdırır, çünkü kopyayı değiştirmek orijinali de ayarlamaz.

Bir sınıf örneğinin _benzersiz bir kopyasını (bazen_ _derin kopya_ olarak adlandırılır) oluşturmak istiyorsanız , yeni bir örnek oluşturmayı ele almanız ve tüm verilerinizi güvenli bir şekilde kopyalamanız gerekir.

Bizim durumumuzda bu çok basit:

```swift
class User {
    var username = "Anonymous"

    func copy() -> User {
        let user = User()
        user.username = username
        return user
    }
}
```

Artık aynı başlangıç ​​verilerine sahip bir nesneyi güvenle arayabiliriz `copy()`, ancak gelecekteki herhangi bir değişiklik orijinali etkilemeyecektir.

---

# Bir sınıf için bir deinitializer nasıl oluşturulur

_Swift'in sınıflarına isteğe bağlı olarak bir başlatıcıyı kaldıran_ verilebilir ; bu, başlatıcının tersi gibidir, çünkü nesne yaratıldığında _değil_ , _yok_ edildiğinde çağrılır .

Bu, birkaç küçük şartla birlikte gelir:

1.  Tıpkı başlatıcılar gibi, başlatıcı kaldırıcılarla kullanmazsınız `func`- onlar özeldir.
2.  Başlatmayanlar hiçbir zaman parametre alamaz veya veri döndüremez ve sonuç olarak parantez içinde bile yazılmaz.
3.  Başlatma gidericiniz, bir sınıf örneğinin son kopyası yok edildiğinde otomatik olarak çağrılacaktır. Bu, örneğin şu anda biten bir işlevin içinde yaratıldığı anlamına gelebilir.
4.  Başlatma gidericileri asla doğrudan aramayız; sistem tarafından otomatik olarak işlenirler.
5.  Yapıların başlatıcıları yoktur, çünkü onları kopyalayamazsınız.

Başlatma gidericilerinizin tam olarak ne _zaman_ çağrılacağı, ne yaptığınıza bağlıdır, ancak gerçekte bu, _kapsam_ adı verilen bir kavrama bağlıdır . Kapsam aşağı yukarı “bilginin mevcut olduğu bağlam” anlamına gelir ve şimdiden pek çok örnek gördünüz:

1.  Bir fonksiyonun içinde bir değişken oluşturursanız, ona fonksiyonun dışından erişemezsiniz.
2.  Bir koşul içinde bir değişken oluşturursanız `if`, bu değişken koşulun dışında kullanılamaz.
3.  Döngü değişkeninin kendisi de dahil olmak üzere bir döngü içinde bir değişken oluşturursanız `for`, onu döngü dışında kullanamazsınız.

Büyük resme bakarsanız, bunların her birinin kapsamlarını oluşturmak için parantez kullandığını göreceksiniz: koşullar, döngüler ve işlevlerin tümü yerel kapsamlar oluşturur.

Bir değer _kapsamdan çıktığında_ , içinde yaratıldığı bağlamın uzaklaştığını kastediyoruz. Verilerin yok edildiği anlamına gelen yapılar söz konusu olduğunda, ancak sınıflar söz konusu olduğunda bu, temel alınan verilerin yalnızca bir kopyasının gittiği anlamına gelir - başka yerlerde hala başka kopyalar olabilir. Ancak son kopya kaybolduğunda, yani bir sınıf örneğini işaret eden son sabit veya değişken yok edildiğinde, altta yatan veriler de yok edilir ve kullandığı bellek sisteme geri döner.

Bunu göstermek için, bir başlatıcı ve başlatıcı kaldırıcı kullanarak oluşturulduğunda ve yok edildiğinde bir mesaj yazdıran bir sınıf oluşturabiliriz:

```swift
class User {
    let id: Int

    init(id: Int) {
        self.id = id
        print("User \(id): I'm alive!")
    }

    deinit {
        print("User \(id): I'm dead!")
    }
}
```

Artık bir döngü kullanarak bunun örneklerini hızlı bir şekilde oluşturabilir ve yok edebiliriz - döngü içinde bir örnek oluşturursak `User`, döngü yinelemesi bittiğinde bu örnek yok edilir:

```swift
for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I'm in control!")
}
```

Bu kod çalıştığında, her bir kullanıcıyı ayrı ayrı oluşturup yok ettiğini, biri daha oluşturulmadan önce tamamen yok edildiğini göreceksiniz.

Unutmayın, başlatıcıyı kaldırıcı yalnızca bir sınıf örneğine yapılan son kalan başvuru yok edildiğinde çağrılır. Bu, sakladığınız bir değişken veya sabit olabilir veya bir dizide bir şey saklamış olabilirsiniz.

Örneğin, örneklerimizi oluşturuldukları gibi ekliyor olsaydık `User`, bunlar yalnızca dizi temizlendiğinde yok edilirdi:

```swift
var users = [User]()

for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I'm in control!")
    users.append(user)
}

print("Loop is finished!")
users.removeAll()
print("Array is clear!")
```

---
# Sınıfların içindeki değişkenlerle nasıl çalışılır?

Swift'in sınıfları biraz tabelalar gibi çalışır: Elimizdeki bir sınıf örneğinin her kopyası aslında aynı temel veri parçasını işaret eden bir tabeladır. Çoğunlukla bu, bir kopyayı değiştirmenin diğerlerini değiştirme şekli nedeniyle önemlidir, ancak aynı zamanda sınıfların değişken özellikleri nasıl ele aldığı nedeniyle de önemlidir.

Bu küçük kod örneği, işlerin nasıl yürüdüğünü gösterir:

```swift
class User {
    var name = "Paul"
}

let user = User()
user.name = "Taylor"
print(user.name)
```

Bu, sabit bir örnek oluşturur `User`, ancak daha sonra onu değiştirir - sabit değeri değiştirir. Bu kötü, değil mi?

Bunun dışında sabit değeri hiç değiştirmez. Evet, sınıfın içindeki veriler değişti, ancak sınıf örneğinin kendisi - yarattığımız nesne - değişmedi _ve_ aslında onu sabit yaptığımız için değiştirilemez _._

Şöyle düşünün: bir kullanıcıyı işaret eden sabit bir tabela oluşturduk ama o kullanıcının isim etiketini sildik ve farklı bir isim yazdık. Söz konusu kullanıcı değişmedi - kişi hala var - ancak dahili verilerinin bir kısmı _değişti_ .

`name`Şimdi, özelliği kullanarak _sabit_ yapsaydık `let`, değiştirilemezdi - bir kullanıcıyı işaret eden sabit bir tabelamız var, ancak silinmemesi için adını kalıcı mürekkeple yazdık.

`user`Aksine, hem örneği hem de özellik değişkenlerini yaparsak ne olur `name`? `User`Şimdi özelliği değiştirebileceğiz, ancak istersek tamamen yeni bir örneğe de geçebileceğiz . Tabela benzetmesine devam edecek olursak, tabelayı tamamen farklı bir kişiyi gösterecek şekilde çevirmek gibi olur.

Bu kodla deneyin:

```swift
class User {
    var name = "Paul"
}

var user = User()
user.name = "Taylor"
user = User()
print(user.name)
```

Bu, sonunda "Paul" yazdıracaktı, çünkü "Taylor" olarak değiştirmiş olsak bile, daha sonra tüm nesnenin üzerine yeni bir tane `name`yazdık ve onu "Paul" olarak sıfırladık.`user`

Son varyasyon, değişken bir örneğe ve sabit özelliklere sahip olmaktır, bu, istersek yeni bir tane oluşturabileceğimiz anlamına gelir `User`, ancak bir kez yapıldığında özelliklerini değiştiremeyiz.

Yani, dört seçenekle sonuçlanıyoruz:

1.  Sabit örnek, sabit özellik – her zaman aynı ada sahip olan aynı kullanıcıyı gösteren bir tabela.
2.  Sabit örnek, değişken özellik – her zaman aynı kullanıcıyı işaret eden, ancak adı değişebilen bir tabela.
3.  Değişken örneği, sabit özellik – farklı kullanıcılara işaret edebilen, ancak adları asla değişmeyen bir tabela.
4.  Değişken örneği, değişken özelliği - farklı kullanıcıları işaret edebilen bir tabela ve bu kullanıcılar da isimlerini değiştirebilir.

Bu son derece kafa karıştırıcı ve hatta bilgiççe görünebilir. Ancak, sınıf örneklerinin paylaşılma şekli nedeniyle önemli bir amaca hizmet eder.

Diyelim ki size bir örnek verildi `User`. Örneğiniz sabittir, ancak içindeki özellik bir değişken olarak bildirilmiştir. Bu size sadece isterseniz o özelliği değiştirebileceğinizi söylemekle kalmaz, daha da önemlisi özelliğin başka bir yerde değiştirilme olasılığının olduğunu söyler - sahip olduğunuz sınıf başka bir yerden bir kopya olabilir ve özellik değişken olduğu için o kodun başka bir bölümünün onu sürpriz bir şekilde değiştirebileceği anlamına gelir.

Sabit özellikleri gördüğünüzde, ne mevcut kodunuzun ne de programınızın başka bir bölümünün onu değiştiremeyeceğinden emin olabilirsiniz, ancak değişken özelliklerle uğraşır ilgilenmez – sınıf örneğinin kendisinin sabit olup olmadığına bakılmaksızın – verilerin ayaklarınızın altında değişebileceği ihtimalini açar.

Bu, yapılardan farklıdır, çünkü sabit yapılar, özellikler değişken yapılsa bile özelliklerini değiştiremezler. Umarız bunun neden olduğunu şimdi anlamışsınızdır: yapılar tüm yol tabelası olayına sahip değildir, verilerini doğrudan tutarlar. Bu, yapının içindeki bir değeri değiştirmeye çalışırsanız, yapının kendisini de dolaylı olarak değiştirdiğiniz anlamına gelir, bu sabit olduğu için mümkün değildir.

`mutating`Tüm bunların bir avantajı, sınıfların anahtar kelimeyi verilerini değiştiren yöntemlerle kullanmasına gerek olmamasıdır . Bu anahtar kelime, yapılar için gerçekten önemlidir, çünkü nasıl yaratıldıklarına bakılmaksızın sabit yapıların özellikleri değiştirilemez, bu nedenle Swift, sabit bir yapı örneğinde bir yöntemi çağırdığımızı gördüğünde _buna_`mutating` izin verilmemesi gerektiğini bilir.

Sınıflar söz konusu olduğunda, örneğin kendisinin nasıl yaratıldığı artık önemli değildir - bir özelliğin değiştirilip değiştirilemeyeceğini belirleyen tek şey, özelliğin kendisinin bir sabit olarak yaratılıp yaratılmadığıdır. Swift, özelliği nasıl yaptığınıza bakarak bunu kendisi görebilir, bu nedenle yöntemi özel olarak işaretlemeye artık gerek yoktur.

---
# Protokoller nasıl oluşturulur ve kullanılır?

Protokoller biraz Swift'teki sözleşmelere benzer: bir veri türünden ne tür işlevselliklerin desteklenmesini beklediğimizi tanımlamamıza izin verirler ve Swift, kodumuzun geri kalanının bu kurallara uymasını sağlar.

Evinden ofisine gidip gelen birini simüle etmek için nasıl bazı kodlar yazabileceğimizi düşünün. Küçük bir yapı oluşturabilir `Car`, ardından şöyle bir işlev yazabiliriz:

```swift
func commute(distance: Int, using vehicle: Car) {
    // lots of code here
}
```

Elbette, trenle de gidip gelebilirler, bu yüzden şunu da yazarız:

```swift
func commute(distance: Int, using vehicle: Train) {
    // lots of code here
}
```

Veya otobüsle seyahat edebilirler:

```swift
func commute(distance: Int, using vehicle: Bus) {
    // lots of code here
}
```

Veya bisiklet, e-scooter, ortak araç veya herhangi bir sayıda başka ulaşım seçeneği kullanabilirler.

Gerçek şu ki, bu seviyede altta yatan yolculuğun nasıl gerçekleştiğini gerçekten umursamıyoruz. Bizim ilgilendiğimiz konu çok daha geniş: Kullanıcının her bir seçeneği kullanarak işe gidip gelmesi ne kadar sürebilir ve yeni konuma gerçek taşınma işlemini nasıl gerçekleştirebilir.

Protokollerin devreye girdiği yer burasıdır: kullanmak istediğimiz bir dizi özelliği ve yöntemi tanımlamamıza izin verirler. Bu özellikleri ve yöntemleri uygulamıyorlar - aslında arkasına herhangi bir kod koymuyorlar - sadece özelliklerin ve yöntemlerin var olması gerektiğini söylüyorlar, biraz plan gibi _._

`Vehicle`Örneğin, şöyle yeni bir protokol tanımlayabiliriz :

```swift
protocol Vehicle {
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

Bunu parçalayalım:

-   `protocol`Yeni bir protokol oluşturmak için protokol adının ardından yazıyoruz . Bu yeni bir tür, bu yüzden büyük harfle başlayan camel case kullanmamız gerekiyor.
-   Protokolün içinde, bu protokolün beklediğimiz gibi çalışması için ihtiyaç duyduğumuz tüm yöntemleri listeliyoruz.
-   Bu yöntemler içinde herhangi bir kod içermez - burada sağlanan işlev gövdesi yoktur. Bunun yerine, yöntem adlarını, parametreleri ve dönüş türlerini belirliyoruz. Gerekirse yöntemleri fırlatma veya mutasyona uğratma olarak da işaretleyebilirsiniz.

Böylece bir protokol oluşturduk - bu bize nasıl yardımcı oldu?

Artık o protokolle çalışan tipler tasarlayabiliriz. Bu, o protokolün gereksinimlerini uygulayan yeni yapılar, sınıflar veya numaralandırmalar oluşturmak anlamına gelir; bu, protokolü _benimseme_ veya _ona uyma_dediğimiz bir süreçtir .

Protokol, olması gereken tüm işlevsellik yelpazesini belirtmez, yalnızca minimum düzeydedir. Bu, protokole uyan yeni türler oluşturduğunuzda, gereken her türlü başka özelliği ve yöntemi ekleyebileceğiniz anlamına gelir.

Örneğin, aşağıdaki gibi `Car`uygun bir yapı yapabiliriz :`Vehicle`

```swift
struct Car: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }

    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }

    func openSunroof() {
        print("It's a nice day!")
    }
}
```

Bu kodda özellikle dikkat çekmek istediğim birkaç şey var:

1.  Swift'e, alt sınıfları işaretlediğimiz gibi, adından sonra iki nokta üst üste kullanarak `Car`uygun olduğunu söyleriz .`Vehicle``Car`
2.  Listelediğimiz tüm yöntemler _tam_`Vehicle` olarak . Biraz farklı isimlere sahiplerse, farklı parametreleri kabul ediyorlarsa, farklı dönüş tiplerine sahiplerse vb., o zaman Swift bizim protokole uymadığımızı söyleyecektir.`Car`
3.  Buradaki yöntemler, `Car`protokolde tanımladığımız yöntemlerin gerçek uygulamalarını sağlar. Bu durumda, bu, yapımızın belirli bir mesafeyi kaç dakika sürdüğüne dair kabaca bir tahmin sağladığı ve çağrıldığında bir mesaj yazdırdığı anlamına gelir `travel()`.
4.  Yöntem `openSunroof()`protokolden gelmiyor `Vehicle`ve orada pek bir anlam ifade etmiyor çünkü birçok araç tipinde açılır tavan yok. Ancak sorun değil, çünkü protokol yalnızca uyumlu türlerin sahip olması gereken _minimum_ işlevselliği açıklar ve gerektiğinde kendi işlevlerini ekleyebilirler.

Böylece, şimdi bir protokol oluşturduk ve `Car`protokole uygun bir yapı oluşturduk.

`commute()`Bitirmek için, işlevi daha önce eklediğimiz yeni yöntemleri kullanacak şekilde güncelleyelim `Car`:

```swift
func commute(distance: Int, using vehicle: Car) {
    if vehicle.estimateTime(for: distance) > 100 {
        print("That's too slow! I'll try a different vehicle.")
    } else {
        vehicle.travel(distance: distance)
    }
}

let car = Car()
commute(distance: 100, using: car)
```

Bu kodun tümü çalışır, ancak burada protokol aslında herhangi bir değer katmaz. Evet, içinde çok özel iki yöntem uygulamamızı sağladı `Car`, ancak bunu protokolü eklemeden de yapabilirdik, öyleyse neden zahmet edelim?

İşin zekice kısmı burada: Swift, uyumlu herhangi bir türün `Vehicle`hem `estimateTime()`ve yöntemlerini uygulaması gerektiğini biliyor ve bu nedenle aslında parametremizin türü olarak yerine `travel()`kullanmamıza izin veriyor . Fonksiyonu şu şekilde yeniden yazabiliriz:`Vehicle``Car`

```swift
func commute(distance: Int, using vehicle: Vehicle) {
```

Şimdi, bu tür protokole uygun olduğu sürece, bu işlevin herhangi bir veri türüyle çağrılabileceğini söylüyoruz `Vehicle`. Fonksiyonun gövdesinin değişmesi gerekmez çünkü Swift, `estimateTime()`ve `travel()`yöntemlerinin var olduğundan emindir.

_Hala_ bunun neden yararlı olduğunu merak ediyorsanız , aşağıdaki yapıyı göz önünde bulundurun:

```swift
struct Bicycle: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 10
    }

    func travel(distance: Int) {
        print("I'm cycling \(distance)km.")
    }
}

let bike = Bicycle()
commute(distance: 50, using: bike)
```

Şimdi, aynı zamanda uyumlu olan ikinci bir yapıya sahibiz `Vehicle`ve protokollerin gücünün ortaya çıktığı yer burasıdır: artık işleve a veya `Car`a'yı geçirebiliriz . Dahili olarak işlev, istediği tüm mantığa sahip olabilir ve aradığında veya Swift otomatik olarak uygun olanı kullanır - bir arabada geçersek "Sürüyorum" der, ancak bisikletle geçersek şunu söyler "Bisiklete biniyorum".`Bicycle``commute()``estimateTime()``travel()`

Bu nedenle protokoller, tam türlerden ziyade birlikte çalışmak istediğimiz işlevsellik türü hakkında konuşmamıza izin verir. “Bu parametre bir araba olmalı” demek yerine, “bu parametre herhangi bir şey olabilir, yeter ki yolculuk süresini tahmin edebilsin ve yeni bir yere taşınabilsin” diyebiliriz.

Yöntemlerin yanı sıra, uyumlu türlerde bulunması gereken _özellikleri_ açıklayan protokoller de yazabilirsiniz . Bunu yapmak için, `var`ardından bir özellik adı yazın ve okunabilir ve/veya yazılabilir olup olmayacağını listeleyin.

`Vehicle`Örneğin, uyan tüm tiplerin kaç koltukları olduğunu ve şu anda kaç yolcuları olduğunu belirtmesi gerektiğini şu şekilde belirtebiliriz :

```swift
protocol Vehicle {
    var name: String { get }
    var currentPassengers: Int { get set }
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

Bu iki özellik ekler:

1.  `name`Okunabilir olması gereken adında bir dize . Bu, onun bir sabit olduğu anlamına gelebilir, ancak alıcısı olan hesaplanmış bir özellik de olabilir.
2.  `currentPassengers`Okuma-yazma olması gereken adında bir tamsayı . Bu, onun bir değişken olduğu anlamına gelebilir, ancak alıcı ve ayarlayıcı içeren hesaplanmış bir özellik de olabilir.

Tip ek açıklaması her ikisi için de gereklidir, çünkü tıpkı protokollerin yöntemler için uygulamaları sağlayamaması gibi, bir protokolde varsayılan bir değer sağlayamayız.

`Car`Bu iki ekstra gereksinim yerine getirildiğinde, Swift, her ikisinin de `Bicycle`özellikleri eksik olduğu için artık protokole uymadığı konusunda bizi uyaracaktır . Bunu düzeltmek için aşağıdaki özellikleri ekleyebiliriz `Car`:

```swift
let name = "Car"
var currentPassengers = 1
```

Ve bunlar `Bicycle`:

```swift
let name = "Bicycle"
var currentPassengers = 1
```

Yine de, kurallara uyduğunuz sürece bunları hesaplanan özelliklerle değiştirebilirsiniz - kullanırsanız, `{ get set }`sabit bir özellik kullanarak protokole uyamazsınız.

Yani artık protokolümüz iki yöntem ve iki özellik gerektiriyor, bu da kodumuzun çalışması için tüm uyumlu türlerin bu dört şeyi uygulaması gerektiği anlamına geliyor. Bu da Swift'in işlevselliğin mevcut olduğundan emin olduğu anlamına gelir, böylece ona dayanarak kod yazabiliriz.

Örneğin, bir dizi aracı kabul eden ve bunu bir dizi seçenek üzerinden tahminleri hesaplamak için kullanan bir yöntem yazabiliriz:

```swift
func getTravelEstimates(using vehicles: [Vehicle], distance: Int) {
    for vehicle in vehicles {
        let estimate = vehicle.estimateTime(for: distance)
        print("\(vehicle.name): \(estimate) hours to travel \(distance)km")
    }
}
```

Umarım bu size protokollerin gerçek gücünü gösterir - tüm protokol dizisini kabul ediyoruz , bu da a , a veya uyumlu herhangi bir yapıyı `Vehicle`geçebileceğimiz anlamına gelir ve otomatik olarak çalışır:`Car``Bicycle``Vehicle`

```swift
getTravelEstimates(using: [car, bike], distance: 150)
```

Protokolleri parametre olarak kabul etmenin yanı sıra, gerekirse bir işlevden protokolleri de döndürebilirsiniz.

**İpucu:** Yalnızca virgülle ayırarak tek tek listeleyerek ihtiyaç duyduğunuz kadar çok protokole uyabilirsiniz. _Bir şeyi alt sınıfa ayırmanız ve_ bir protokole uymanız gerekirse , önce ana sınıfın adını yazmalı, ardından protokollerinizi daha sonra yazmalısınız.

---

# Opaque return türleri nasıl kullanılır?

Swift , kodumuzdaki karmaşıklığı ortadan kaldırmamıza izin veren , opak dönüş türleri adı verilen gerçekten belirsiz, gerçekten karmaşık ama gerçekten _önemli bir özellik sağlar._ Dürüst olmak gerekirse, çok önemli bir gerçek olmasaydı, bunu bir başlangıç ​​kursunda ele almazdım: İlk SwiftUI projenizi oluşturur oluşturmaz bunu hemen göreceksiniz.

**Önemli:** Opak dönüş türlerinin nasıl çalıştığını ayrıntılı olarak anlamanız gerekmez, yalnızca var olduklarını ve çok özel bir iş yaptıklarını bilmeniz gerekir. Burayı takip ederken, bu özelliğin neden yararlı olduğunu merak etmeye başlayabilirsiniz, ancak bana güvenin: bu _önemli_ ve _yararlıdır_ , bu yüzden gücünüzü deneyin!

İki basit işlevi uygulayalım:

```swift
func getRandomNumber() -> Int {
    Int.random(in: 1...6)
}

func getRandomBool() -> Bool {
    Bool.random()
}
```

**İpucu:** `Bool.random()` true veya false döndürür. Rastgele tamsayılar ve ondalık sayılardan farklı olarak, herhangi bir özelleştirme seçeneği olmadığı için herhangi bir parametre belirtmemize gerek yoktur.

Yani, `getRandomNumber()`rasgele bir tamsayı döndürür ve `getRandomBool()`rasgele bir Boole değeri döndürür.

Her ikisi `Int`de ve "eşitlik için karşılaştırılabilir" anlamına `Bool`gelen ortak bir Swift protokolüne uygundur . `Equatable`Protokol , şu şekilde `Equatable`kullanmamıza izin veren şeydir :`==`

```swift
print(getRandomNumber() == getRandomNumber())
```

Bu türlerin her ikisi de ile uyumlu olduğundan , işlevimizi aşağıdaki gibi `Equatable`bir değer döndürecek şekilde değiştirmeyi deneyebiliriz :`Equatable`

```swift
func getRandomNumber() -> Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> Equatable {
    Bool.random()
}
```

Ancak, bu kod çalışmayacak ve Swift, Swift kariyerinizin bu noktasında pek yardımcı olmayacak bir hata mesajı verecektir: "'Equatable' protokolü yalnızca genel bir kısıtlama olarak kullanılabilir çünkü Self veya ilişkili tip gereksinimleri”. Swift'in hatasının anlamı, geri dönüşün `Equatable`mantıklı olmadığı ve bunun _neden_ anlamsız olduğunu anlamak, opak dönüş türlerini anlamanın anahtarıdır.

İlk olarak: evet, işlevlerden protokolleri _döndürebilirsiniz_ ve genellikle bu gerçekten yararlı bir şeydir. Örneğin, kullanıcılar için araç kiralama bulan bir işleviniz olabilir: taşıması gereken yolcu sayısını ve ne kadar bagaj istediklerini kabul eder, ancak birkaç yapıdan birini geri gönderebilir: , ‌ , ,`Compact` ve yakında.`SUV``Minivan`

Bunu, tüm bu yapılar tarafından benimsenen bir protokol döndürerek halledebiliriz ve böylece işlevi çağıran kişi , tüm araba çeşitlerini işlemek için 10 farklı işlev yazmamıza gerek kalmadan, isteklerine uyan _bir_`Vehicle` tür arabayı geri alır . Bu araba türlerinin her biri , 'nin tüm yöntemlerini ve özelliklerini uygulayacaktır , bu da bunların değiştirilebilir olduğu anlamına gelir - kodlama açısından hangi seçeneği geri aldığımız umurumuzda değil.`Vehicle`

`Int`Şimdi bir veya bir geri göndermeyi düşünün `Bool`. Evet, ikisi de uyumludur `Equatable`, ancak birbirlerinin yerine _kullanılamazlar_ - a ve a'yı `==`karşılaştırmak için kullanamayız , çünkü hangi protokollere uygun olurlarsa olsunlar Swift bize izin vermez.`Int``Bool`

Bir işlevden protokol döndürmek, bilgileri gizlememize izin verdiği için yararlıdır: döndürülen tam türü belirtmek yerine, döndürülen _işlevselliğe_ odaklanırız . Bir protokol söz konusu olduğunda `Vehicle`bu, koltuk sayısını, yaklaşık yakıt kullanımını ve bir fiyatı bildirmek anlamına gelebilir. Bu, kodumuzu daha sonra hiçbir şeyi bozmadan değiştirebileceğimiz anlamına gelir: tarafından istenen özellikleri ve yöntemleri uyguladıkları sürece a `RaceCar`, a , vb. döndürebiliriz .`PickUpTruck``Vehicle`

Bilgileri bu şekilde gizlemek gerçekten yararlıdır, ancak iki farklı şeyi `Equatable`karşılaştırmak mümkün olmadığı için mümkün değildir. `Equatable`İki tamsayı elde etmek için iki kez arasak bile `getRandomNumber()`, tam veri türlerini gizlediğimiz için onları karşılaştıramayız – aslında karşılaştırılabilecek iki tamsayı oldukları gerçeğini gizledik.

Opak dönüş türlerinin devreye girdiği yer burasıdır: kodumuzdaki bilgileri gizlememize izin verirler, ancak Swift derleyicisinden _değil ._ Bu, gelecekte farklı şeyler döndürebilmemiz için kodumuzu dahili olarak esnek hale getirme hakkını saklı tuttuğumuz anlamına gelir, ancak Swift, döndürülen _gerçek veri türünü her zaman anlar ve uygun şekilde kontrol eder._

İki işlevimizi opak dönüş türlerine yükseltmek için, anahtar kelimeyi `some`dönüş türlerinin önüne şu şekilde ekleyin:

```swift
func getRandomNumber() -> some Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> some Equatable {
    Bool.random()
}
```

Ve şimdi iki kez arayabilir _ve_`getRandomNumber()` sonuçları kullanarak karşılaştırabiliriz `==`. Bizim bakış açımızdan hala sadece bazı `Equatable`verilerimiz var, ancak Swift perde arkasında bunların aslında iki tamsayı olduğunu biliyor.

Opak bir dönüş türü döndürmek, belirli tür yerine döndürmek istediğimiz işlevselliğe odaklanabileceğimiz anlamına gelir; bu da gelecekte kodumuzun geri kalanını bozmadan fikrimizi değiştirmemize olanak tanır. Örneğin, `getRandomNumber()`kullanmaya geçebilir `Double.random(in:)`ve kod yine de harika çalışır.

Ancak buradaki avantaj, Swift'in her zaman gerçek temel veri türünü bilmesidir. Bu ince bir ayrım, ancak geri dönüş `Vehicle`"herhangi bir Araç türü ama ne olduğunu bilmiyoruz" anlamına gelirken, geri dönüş `some Vehicle`"belirli bir tür `Vehicle`ama hangisi olduğunu söylemek istemiyoruz" anlamına gelir.

Bu noktada başınızın dönmesini bekliyorum, bu yüzden size SwiftUI'de bunun neden önemli olduğuna dair gerçek bir örnek vereyim. SwiftUI'nin ekranda ne tür bir düzen göstermek istediğinizi tam olarak bilmesi gerekiyor ve bu yüzden onu açıklamak için kod yazıyoruz.

İngilizce olarak şöyle bir şey söyleyebiliriz: “üstte bir araç çubuğu, altta bir sekme çubuğu olan bir ekran var ve ortada, her birinin altında ne olduğunu söyleyen bir etiket bulunan, renkli simgelerden oluşan kayan bir ızgara var. simgesi, kalın yazı tipiyle yazılmış anlamına gelir ve bir simgeye dokunduğunuzda bir mesaj görünür.”

SwiftUI düzenimizi istediğinde, bu açıklama - her şey - düzen için dönüş türü olur. Konumlar, renkler, yazı tipi boyutları ve daha fazlası dahil olmak üzere ekranda göstermek istediğimiz her şey hakkında açık olmalıyız. Bunu dönüş türünüz olarak yazmayı hayal edebiliyor musunuz? Bir mil uzunluğunda olurdu! Ve düzeninizi oluşturmak için kodu her değiştirdiğinizde, dönüş türünü eşleşecek şekilde değiştirmeniz gerekir.

Bu, opak dönüş türlerinin imdada yetiştiği yerdir: türü döndürebiliriz `some View`, bu da bir tür görüntüleme ekranının döndürüleceği anlamına gelir, ancak onun mil uzunluğundaki türünü yazmak zorunda kalmak istemiyoruz. Aynı zamanda Swift, gerçek altta yatan türü bilir çünkü opak dönüş türleri bu şekilde çalışır: Swift, geri gönderilen verilerin tam türünü her zaman bilir ve SwiftUI, mizanpajlarını oluşturanları kullanır.

Başlangıçta söylediğim gibi, opak dönüş türleri gerçekten belirsiz, gerçekten karmaşık ama gerçekten _önemli_ bir özelliktir ve SwiftUI'de yaygın olarak kullanılmaları gerçeği olmasaydı bunları bir başlangıç ​​​​kursunda ele almazdım.

Dolayısıyla, SwiftUI kodunuzda gördüğünüzde `some View`, Swift'e etkili bir şekilde "bu, düzenlenmesi için bir tür görünümü geri gönderecek, ancak tam olarak yazmak istemiyorum - kendiniz anlıyorsunuz" diyoruz. ”