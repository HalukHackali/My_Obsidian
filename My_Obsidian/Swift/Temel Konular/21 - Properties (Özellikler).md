#swift #yazılım 

Struct'lar ve sınıflar (ortaklaşa: "tipler") kendilerine has değişkenlere ve sabitlere sahip olabilirlir ve bunlar özellik olarak adlandırılır. Bunlar, onları eşsiz bir şekilde temsil edecek olan tiplerinize değerler iliştirmenize izin verir, ama tiplerin de metodları olduğu için, onları kendilerine has verilere göre davranmalarını sağlayabilirsiniz.

Hadi şimdi aşağıdaki örneğe bir göz atalım:

```swift
struct Person {
    var clothes: String
    var shoes: String

    func describe() {
        print("I like wearing \(clothes) with \(shoes)")
    }
}

let taylor = Person(clothes: "T-shirts", shoes: "sneakers")
let other = Person(clothes: "short skirts", shoes: "high heels")
taylor.describe()
other.describe()
```

Gördüğünüz gibi, bir metod içerisinde bir özellik kullandığınızda, aynı nesneye ait olan değeri otomatik olarak kullanacaktır.

## Özellik gözleyiciler

Swift dili, bir özellik değişmek üzere olduğunda veya değiştiğinde çalıştırılacak kodu eklemene izin verir. Bu, örneğin bir değer değiştiğinde kullanıcı arayüzünün güncellenmesi için, sıklıkla iyi bir yoldur.

İki tür özellik gözleyici vardır: `willSet` ve `didSet`. Bunlar bir özellik değişmeden önce veya sonra çağırılırlar. `willSet` ile Swift, `newValue` adı verilen özel bir değerle kodunuzun sahip olacağı yeni özellik değerini sağlar. `didSet` ile de bir önceki değeri temsil eden `oldValue` verilir.

Bu iki özellik gözleyiciyi, `Person` struct'ının bir özelliği `clothes` değişkenine ekleyelim:

```swift
struct Person {
    var clothes: String {
        willSet {
            updateUI(msg: "I'm changing from \(clothes) to \(newValue)")
        }

        didSet {
            updateUI(msg: "I just changed from \(oldValue) to \(clothes)")
        }
    }
}

func updateUI(msg: String) {
    print(msg)
}

var taylor = Person(clothes: "T-shirts")
taylor.clothes = "short skirts"
```

Bu çıktısı "I'm changing from T-shirts to short skirts" (Tişörtleri kısa eteklerle değiştiriyorum) ve "I just changed from T-shirts to short skirts." (Az önce tişörtleri kısa eteklerle değiştirdim) mesajları olacaktır.

## Computed properties Hesaplanmış özellikler

Arka plandaki gerçek kod olan özellikler yapmam mümkün. Örneğin daha önce string metodu olan `uppercased()` kullanmıştık, ama aynı zamanda her zaman kendisinin büyük harfli versiyonunu saklayan her string'dense, gerektiğinde hesaplanan ve `capitalized` adı verilen bir özellik daha var.

Hesaplanmış bir özellik yapmak için, özellikten sonra bir süslü parantez açın ve uygun bir zamanda eyleme geçmesi için `get` veya `set`kullanın. Örneğin, kişinin yaşını yedi ile çarpıp otomatik olarak döndüren `ageInDogYears`adında bir özellik eklemek isteseydik, şu şekilde yapardık:

```swift
struct Person {
    var age: Int

    var ageInDogYears: Int {
        get {
            return age * 7
        }
    }
}

var fan = Person(age: 25)
print(fan.ageInDogYears)
```

Hesaplanmış özellikler, Apple'ın kodlarında gittikçe yaygınlaşıyor, ama kullanıcı kodlarında daha az yaygın.

**Not:** Eğer onları sadece *okunan" veri olarak kullanmayı düşünüyorsan, `get` kısmını aşağıdaki gibi tamamen silebilirsin:

```swift
var ageInDogYears: Int {
    return age * 7
}
```

---
 
#  Properties değerleri dinamik olarak nasıl hesaplanır ? 

Yapıların iki tür özelliği olabilir: _saklı_ bir özellik, yapının bir örneğinin içinde bir veri parçasını tutan bir değişken veya sabittir ve _hesaplanmış_ bir özellik, her erişildiğinde özelliğin değerini dinamik olarak hesaplar. Bu, hesaplanan özelliklerin hem depolanan özelliklerin hem de işlevlerin bir karışımı olduğu anlamına gelir: bunlara depolanmış özellikler gibi erişilir, ancak işlevler gibi çalışır.

Örnek verecek olursak daha önce `Employee`o çalışanın kaç gün izin kaldığını takip eden bir yapımız vardı. İşte basitleştirilmiş bir versiyon:

```swift
struct Employee {
    let name: String
    var vacationRemaining: Int
}

var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.vacationRemaining -= 5
print(archer.vacationRemaining)
archer.vacationRemaining -= 3
print(archer.vacationRemaining)
```

Bu önemsiz bir yapı olarak çalışıyor, ancak değerli bilgileri kaybediyoruz – bu çalışana 14 günlük tatil atıyoruz ve ardından alınan günleri gün olarak çıkarıyoruz, ancak bunu yaparken başlangıçta kaç gün verildiğini kaybediyoruz.

Hesaplanan özelliği kullanmak için bunu şu şekilde ayarlayabiliriz:

```swift
struct Employee {
    let name: String
    var vacationAllocated = 14
    var vacationTaken = 0

    var vacationRemaining: Int {
        vacationAllocated - vacationTaken
    }
}
```

Şimdi doğrudan atayabileceğimiz bir şey yapmak yerine `vacationRemaining`, ne kadar izin verildiğinden ne kadar izin aldıkları çıkarılarak hesaplanıyor.

'dan okurken `vacationRemaining`, normal bir depolanmış özellik gibi görünür:

```swift
var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
print(archer.vacationRemaining)
archer.vacationTaken += 4
print(archer.vacationRemaining)
```

Bu gerçekten güçlü bir şey: bir mülk gibi görünen şeyleri okuyoruz, ancak perde arkasında Swift her seferinde değerini hesaplamak için bazı kodlar çalıştırıyor.

Yine de ona yazamıyoruz çünkü Swift'e _bunun_ nasıl ele alınması gerektiğini söylemedik. Bunu düzeltmek için, sırasıyla "okuyan kod" ve "yazan kod" için hem _alıcı_ hem de _ayarlayıcı_ - süslü isimler sağlamamız gerekiyor .

Bu durumda alıcı yeterince basit, çünkü bu sadece bizim mevcut kodumuz. Ancak _ayarlayıcı_ daha ilginçtir - bir çalışan için ayarlarsanız , değerlerinin artırılmasını veya azaltılmasını `vacationRemaining`mı istiyorsunuz yoksa aynı kalması ve onun yerine bizim değişmemiz mi gerektiğini kastediyorsunuz ?`vacationAllocated``vacationAllocated``vacationTaken`

Bu ikisinden ilkinin doğru olduğunu varsayacağım, bu durumda özellik şu şekilde görünür:

```swift
var vacationRemaining: Int {
    get {
        vacationAllocated - vacationTaken
    }

    set {
        vacationAllocated = vacationTaken + newValue
    }
}
```

Bir değeri okurken veya yazarken ayrı ayrı kod parçalarının nasıl çalıştırılacağına `get`ve işaretlendiğine dikkat edin. `set`Daha da önemlisi, dikkat edin `newValue`- bu bize Swift tarafından otomatik olarak sağlanır ve kullanıcının mülke atamaya çalıştığı değeri saklar.

Hem alıcı hem de ayarlayıcı yerinde olduğunda, artık şunları değiştirebiliriz `vacationRemaining`:

```swift
var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
archer.vacationRemaining = 5
print(archer.vacationAllocated)
```

SwiftUI, hesaplanan özellikleri kapsamlı bir şekilde kullanır - bunları oluşturduğunuz ilk projede göreceksiniz!

---

# Bir Properties değiştiğinde nasıl önlem alınır?

Swift , özellikler değiştiğinde çalışan özel kod parçaları olan _özellik gözlemcileri_ oluşturmamıza izin verir . Bunlar iki biçim alır: `didSet`özellik yeni değiştiğinde çalışacak bir gözlemci ve özellik değişmeden _önce_`willSet` çalışacak bir gözlemci .

Özellik gözlemcilerine neden ihtiyaç duyulabileceğini görmek için şuna benzer bir kod düşünün:

```swift
struct Game {
    var score = 0
}

var game = Game()
game.score += 10
print("Score is now \(game.score)")
game.score -= 3
print("Score is now \(game.score)")
game.score += 1
```

Bu bir `Game`yapı oluşturur ve puanını birkaç kez değiştirir. Puan her değiştiğinde, `print()`değişiklikleri takip edebilmemiz için onu bir çizgi izler. Ancak bir hata var: sonunda puan yazdırılmadan değişti _,_ bu bir hatadır.

`print()`Özellik gözlemcileri ile bu sorunu , aramayı kullanarak doğrudan özelliğe ekleyerek çözebiliriz `didSet`, böylece ne zaman değişirse – nerede değişirse değişsin – her zaman bazı kodlar çalıştıracağız.

İşte aynı örnek, şimdi yerinde bir özellik gözlemcisi ile:

```swift
struct Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var game = Game()
game.score += 10
game.score -= 3
game.score += 1
```

İsterseniz, değiştirdiğiniz şeye bağlı olarak özel işlevselliğe ihtiyacınız olması durumunda Swift otomatik olarak `oldValue`inside sabitini sağlar. _Ayrıca, özellik değişmeden önce_ bazı kodları çalıştıran ve buna bağlı olarak farklı bir işlem yapmak istemeniz durumunda atanacak yeni değeri sağlayan `didSet`bir varyant da vardır .`willSet`

Kod çalıştırıldığında akışı görebilmeniz için değerler değiştikçe mesajları yazdıracak tek bir kod örneğini kullanarak tüm bu işlevselliği uygulamalı olarak gösterebiliriz:

```swift
struct App {
    var contacts = [String]() {
        willSet {
            print("Current value is: \(contacts)")
            print("New value will be: \(newValue)")
        }

        didSet {
            print("There are now \(contacts.count) contacts.")
            print("Old value was \(oldValue)")
        }
    }
}

var app = App()
app.contacts.append("Adrian E")
app.contacts.append("Allen W")
app.contacts.append("Ish S")
```

`willSet`Evet, bir diziye ekleme hem ve hem de tetikler `didSet`, böylece kod çalıştırıldığında çok sayıda metin yazdırır.

Uygulamada, `willSet`'dan çok daha az kullanılır `didSet`, ancak yine de zaman zaman görebilirsiniz, bu nedenle var olduğunu bilmeniz önemlidir. Hangisini seçerseniz seçin, lütfen mülk gözlemcilerine çok fazla iş yüklemekten kaçının - yoğun çalışmayı tetiklemek gibi önemsiz görünen bir şey `game.score += 1`sizi düzenli olarak yakalar ve her türlü performans sorununa neden olur.

---

# Özel Properties nasıl oluşturulur?

Başlatıcılar, kullanılacak yeni bir yapı örneği hazırlamak için tasarlanmış özel yöntemlerdir. Swift'in bir yapı içine yerleştirdiğimiz özelliklere dayanarak bizim için nasıl sessizce bir tane oluşturduğunu zaten gördünüz, ancak bir altın kuralı takip ettiğiniz sürece kendinizinkini de oluşturabilirsiniz: başlatıcı sona erene kadar tüm özellikler bir değere sahip olmalıdır. .

Yapılar için Swift'in varsayılan başlatıcısına tekrar bakarak başlayalım:

```swift
struct Player {
    let name: String
    let number: Int
}

let player = Player(name: "Megan R", number: 15)
```

`Player`Bu , iki özelliği için değerler sağlayarak yeni bir örnek oluşturur . Swift buna , tanımlandığı sırayla her özelliği kabul eden bir başlatıcı söylemenin süslü bir yolu olan _üyeler için başlatıcı adını verir._

Dediğim gibi, bu tür bir kod mümkündür çünkü Swift sessizce bu iki değeri kabul eden bir başlatıcı oluşturur, ancak aynı şeyi yapmak için kendimizinkini yazabiliriz. Buradaki tek nokta, gelen parametrelerin adları ile atanan özelliklerin adlarını birbirinden ayırmaya dikkat etmeniz gerektiğidir.

İşte bunun nasıl görüneceği:

```swift
struct Player {
    let name: String
    let number: Int

    init(name: String, number: Int) {
        self.name = name
        self.number = number
    }
}
```

Bu, önceki kodumuzla aynı şekilde çalışır, ancak artık başlatıcı bize aittir, bu nedenle gerekirse oraya ekstra işlevsellik ekleyebiliriz.

Ancak, dikkatinizi çekmenizi istediğim birkaç şey var:

1.  Anahtar kelime yok `func`. Evet, bu sözdizimi açısından bir işleve benziyor, ancak Swift başlatıcıları özel olarak ele alıyor.
2.  Bu, yeni bir örnek oluştursa da `Player`, başlatıcıların hiçbir zaman açıkça bir dönüş türü yoktur - her zaman ait oldukları veri türünü döndürürler.
3.  "Parametreyi mülküme `self`ata" demek istediğimizi açıklığa kavuşturmak için özelliklere parametreler atardım .`name``name`

Bu son nokta özellikle önemlidir, çünkü olmasaydı `self`yapardık `name = name`ve bu bir anlam ifade etmez – özelliği parametreye mi, parametreyi kendisine mi atıyoruz yoksa başka bir şey mi yapıyoruz? Yazarak, başka herhangi bir şeyin aksine `self.name`“mevcut durumuma ait olan özelliği” kastettiğimizi açıklığa kavuşturuyoruz .`name`

Tabii ki, özel başlatıcılarımızın Swift'in bize sağladığı varsayılan üye bazında başlatıcı gibi çalışması gerekmez. Örneğin, bir oyuncu adı vermeniz gerektiğini söyleyebiliriz, ancak forma numarası rastgeledir:

```swift
struct Player {
    let name: String
    let number: Int

    init(name: String) {
        self.name = name
        number = Int.random(in: 1...99)
    }
}

let player = Player(name: "Megan R")
print(player.number)
```

Sadece altın kuralı unutmayın: başlatıcı sona erene kadar tüm özellikler bir değere sahip olmalıdır. Başlatıcı içinde için bir değer sağlamamış _olsaydık_ , `number`Swift kodumuzu oluşturmayı reddederdi.

**Önemli:** Yapınızın diğer yöntemlerini başlatıcınız içinde çağırabilseniz de, tüm özelliklerinize değerler atamadan bunu yapamazsınız – Swift'in başka bir şey yapmadan önce her şeyin güvenli olduğundan emin olması gerekir _._

İsterseniz yapılarınıza birden fazla başlatıcı ekleyebilir, ayrıca harici parametre adları ve varsayılan değerler gibi özelliklerden yararlanabilirsiniz. Ancak, kendi özel başlatıcılarınızı uygular uygulamaz, onu korumak için ekstra adımlar atmazsanız, Swift'in oluşturduğu üyeler bazında başlatıcıya erişiminizi kaybedersiniz. Bu bir tesadüf değildir: Eğer özel bir başlatıcınız varsa, Swift bunun nedeninin, özelliklerinizi başlatmak için özel bir yolunuz olduğunu varsayar, bu da varsayılanın artık mevcut olmaması gerektiği anlamına gelir.