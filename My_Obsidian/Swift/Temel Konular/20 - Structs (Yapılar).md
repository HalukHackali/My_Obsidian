#swift #yazılım 

Struct'lar, çoklu değerlerden oluşturulan karmaşık veri tipleridir. Bir struct örneği oluşturup, içini verilerle doldur, ardından tek bir değer olarak kodunda kullan. Örneğin, `clothes` ve `shoes` adlı iki değişken içeren `Person` adında bir struct tipi belirleyebiliriz.

```swift
struct Person {
    var clothes: String
    var shoes: String
}
```

Bir struct'ı tanımladığınızda, Swift onları oluşturmayı çok kolaylaştırır çünkü üyelik başlatıcı olarak anılan şeyi otomatik olarak üretir. Daha basit konuşmak gerekirse, aşağıda gösterildiği gibi, içinde tanımlı olan iki niteliğe birer başlangıç değeri geçerek struct oluşturursunuz:

```swift
let taylor = Person(clothes: "T-shirts", shoes: "sneakers")
let other = Person(clothes: "short skirts", shoes: "high heels")
```

Bir struct örneği oluşturduğunuz anda, onun niteliklerini struct'ın önce adını, ardından bir nokta, sonra da talep ettiğiniz niteliğin adını yazarak okuyabilirsiniz:

```swift
print(taylor.clothes)
print(other.shoes)
```

Eğer bir struct'ı diğerine atarsanız, Swift arka planda onu kopyalar, böylece tam ve bağımsız bir çoğaltaması oluşur. Aslında bu tavizsiz bir şekilde doğru değildir: Swift, aslında değiştirmeye çalıştığınız zaman verinizin kopyalanması anlamına gelen "yazarak kopyala" adlı bir tekniği kullanır.

Struct kopyalarının nasıl çalıştığını anlamanıza yardımcı olması için, şu kodu oyun alanınıza yazın:

```swift
struct Person {
    var clothes: String
    var shoes: String
}

let taylor = Person(clothes: "T-shirts", shoes: "sneakers")
let other = Person(clothes: "short skirts", shoes: "high heels")

var taylorCopy = taylor
taylorCopy.shoes = "flip flops"

print(taylor)
print(taylorCopy)
```

Bu, iki tane `Person` struct'ı oluşturur. Ardından `taylor`ın bir kopyası olarak `taylorCopy` isminde bir üçüncüsünü oluşturur. Sonrasında olan ise ilginç kısmıdır: Kod, `taylorCopy` versiyonunu değiştirir ve hem onu, hem de `taylor`ı yazdırır. Eğer sonuç paneline bakarsanız (sığdırabilmek için ekranı yeniden ölçülendirmeniz gerekebilir), kopyanın orjinaline göre farklı bir değere sahip olduğunu görürsünüz: Birini değiştirmek, diğerini de değiştirmek anlamına gelmez.

## Struct'ların içindeki fonksiyonlar

Struct'ların içine fonksiyon koyabilirsiniz ve aslında struct'ın içindeki veriyi okumak veya değiştirmek için fonksiyonları kullanmak iyi bir fikirdir. Örneğin, `Person` adlı struct'ımıza ne giydiklerini tanımlayan bir fonksiyonu şu şekilde ekleyebilirdik:

```swift
struct Person {
    var clothes: String
    var shoes: String

    func describe() {
        print("I like wearing \(clothes) with \(shoes)")
    }
}
```

Bu kodda göremeyeceğiniz, ama bilmenizin iyi olduğunu düşündüğüm bir şey daha var: Bir struct'ın içine bir fonksiyon koyduğunuzda, ismi _metod_ olur. Swift dilinde, ister fonksiyon, ister metod olsun her halükarda `func` ile yazarsınız, ama fark onlar hakkında konuşurken korunur.

---
# Kendi struct yapınızı nasıl oluşturabilirsiniz?

Swift'in yapıları, kendi değişkenleri ve kendi işlevleriyle birlikte kendi özel, karmaşık veri türlerimizi oluşturmamıza izin verir.

Basit bir yapı şöyle görünür:

```swift
struct Album {
    let title: String
    let artist: String
    let year: Int

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}
```

Bu, ve `Album`adı verilen iki dize sabiti ve adı verilen bir tamsayı sabiti ile adında yeni bir tür oluşturur . Üç sabitimizin değerlerini özetleyen basit bir fonksiyon da ekledim.`title``artist``year`

`Album`Büyük A ile nasıl başladığına dikkat edin ? Swift'de standart budur ve biz onu başından beri kullanıyoruz - `String`, `Int`, `Bool`, `Set`, vb. Bir veri türünden bahsederken, ilk harfin büyük olduğu deve durumunu kullanırız, ancak bir değişken veya işlev gibi tür içindeki bir şeye atıfta bulunduğunuzda, ilk harfin küçük olduğu deve durumunu kullanırız. . Unutmayın, çoğunlukla bu bir kuraldan ziyade yalnızca bir gelenektir, ancak buna bağlı kalmanız yararlı olacaktır.

Bu noktada, `Album`tıpkı `String`veya gibi `Int`– bunları oluşturabilir, değerler atayabilir, kopyalayabilir vb. Örneğin, birkaç albüm yapabilir, ardından bazı değerlerini yazdırabilir ve işlevlerini çağırabiliriz:

```swift
let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
let wings = Album(title: "Wings", artist: "BTS", year: 2016)

print(red.title)
print(wings.artist)

red.printSummary()
wings.printSummary()
```

`Album`Sanki bir fonksiyon çağırıyormuşuz gibi yeni bir fonksiyonu nasıl oluşturabileceğimize dikkat edin – sadece tanımlandıkları sırayla her bir sabit için değer sağlamamız gerekiyor.

Gördüğünüz gibi, her ikisi `red`de `wings`aynı yapıdan geliyor `Album`, ancak onları oluşturduğumuzda, tıpkı iki dizi oluşturmak gibi ayrılar.

Her yapıyı çağırdığımızda bunu eylem halinde görebilirsiniz `printSummary()`, çünkü bu işlev `title`, `artist`ve `year`. Her iki durumda da her yapı için doğru değerler yazdırılır: `red`“Red (2012) by Taylor Swift” yazdırır ve `wings`“Wings (2016) by BTS” yazdırır – Swift `printSummary()`çağrıldığında `red`, `title`, `artist`ve `year`da ait olan sabitler `red`.

İşlerin daha ilginç hale geldiği yer, değişebilen değerlere sahip olmak istediğiniz zamandır. `Employee`Örneğin, gerektiğinde tatil yapabilen bir yapı oluşturabiliriz :

```swift
struct Employee {
    let name: String
    var vacationRemaining: Int

    func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("I'm going on vacation!")
            print("Days remaining: \(vacationRemaining)")
        } else {
            print("Oops! There aren't enough days remaining.")
        }
    }
}
```

Ancak bu gerçekten işe yaramayacak – Swift kodu oluşturmayı reddedecek.

Görüyorsunuz, kullanarak bir çalışanı sabit olarak yaratırsak `let`, Swift çalışanı _ve tüm verilerini_ sabit yapar - işlevleri gayet iyi çağırabiliriz, ancak bu işlevlerin yapının verilerini değiştirmesine izin verilmemelidir çünkü onu sabit yaptık.

Sonuç olarak, Swift fazladan bir adım atmamızı sağlıyor: Yalnızca veri okuyan tüm işlevler oldukları gibi gayet iyi, ancak yapıya ait verileri _değiştiren_ herhangi bir özel anahtar sözcükle işaretlenmelidir `mutating`, bunun gibi:

```swift
mutating func takeVacation(days: Int) {
```

`takeVacation()`Şimdi kodumuz gayet iyi inşa edilecek, ancak Swift sabit yapılardan arama yapmamızı engelleyecek .

Kodda buna izin verilir:

```swift
var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.takeVacation(days: 5)
print(archer.vacationRemaining)
```

`var archer`Ancak olarak değiştirirseniz, `let archer`Swift'in kodunuzu yeniden oluşturmayı reddettiğini göreceksiniz - sabit bir yapı üzerinde mutasyona uğrayan bir işlev çağırmaya çalışıyoruz, buna izin verilmez.

Önümüzdeki birkaç bölümde yapıları ayrıntılı olarak keşfedeceğiz, ama önce bazı şeylere isimler vermek istiyorum.

-   Yapılara ait değişkenler ve sabitler _özellikler_ olarak adlandırılır .
-   _Yapılara ait olan işlevlere yöntemler_ denir .
-   Bir yapıdan bir sabit veya değişken oluşturduğumuzda buna _örnek_`Album` diyoruz - örneğin yapının bir düzine benzersiz örneğini oluşturabilirsiniz .
-   Yapı örnekleri oluşturduğumuzda, bunu şunun gibi bir _başlatıcı_`Album(title: "Wings", artist: "BTS", year: 2016)` kullanarak yaparız: .

Bu sonuncusu başta biraz garip gelebilir, çünkü yapımıza bir fonksiyon gibi davranıyoruz ve parametreleri geçiyoruz. Bu biraz _sözdizimsel şeker_`init()` denen şeyin bir parçasıdır - Swift , yapının tüm özelliklerini parametre olarak kullanarak, yapının içinde sessizce özel bir işlev yaratır . Daha sonra otomatik olarak bu iki kod parçasına aynıymış gibi davranır:

```swift
var archer1 = Employee(name: "Sterling Archer", vacationRemaining: 14)
var archer2 = Employee.init(name: "Sterling Archer", vacationRemaining: 14)
```

Aslında daha önce bu davranışa güveniyorduk. İlk kez tanıttığımda , bir ve a `Double`ekleyemeyeceğinizi ve bunun yerine şöyle bir kod yazmanız gerektiğini açıklamıştım:`Int``Double`

```swift
let a = 1
let b = 2.0
let c = Double(a) + b
```

Artık burada gerçekte ne olduğunu görebilirsiniz: Swift'in kendi `Double`türü bir yapı olarak uygulanır ve bir tamsayı kabul eden bir başlatıcı işlevi vardır.

Swift, kendi başlatıcısını oluşturma biçiminde akıllıdır, hatta özelliklerimize atarsak varsayılan değerleri ekler.

Örneğin, yapımızda bu iki özellik varsa

```swift
let name: String
var vacationRemaining = 14
```

Ardından Swift sessizce varsayılan değeri 14 olan bir başlatıcı oluşturacak `vacationRemaining`ve bunların her ikisini de geçerli kılacaktır:

```swift
let kane = Employee(name: "Lana Kane")
let poovey = Employee(name: "Pam Poovey", vacationRemaining: 35)
```

**İpucu:** Sabit bir özelliğe varsayılan bir değer atarsanız, bu, başlatıcıdan tamamen kaldırılacaktır. _Bir varsayılan_ atamak ancak gerektiğinde geçersiz kılma olasılığını açık bırakmak için bir değişken özelliği kullanın.