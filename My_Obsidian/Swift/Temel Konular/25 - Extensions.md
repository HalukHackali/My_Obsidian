# Extensions nasıl oluşturulur ve kullanılır?

#swift #yazılım 

Uzantılar, ister biz oluşturalım ister başkası oluştursun, herhangi bir türe, hatta Apple'ın kendi türlerinden birine bile işlevsellik eklememize izin verir.

Bunu göstermek için, sizi dizeler üzerinde kullanışlı bir yöntemle tanıştırmak istiyorum `trimmingCharacters(in:)`. Bu, alfasayısal harfler, ondalık basamaklar veya en yaygın olarak boşluk ve yeni satırlar gibi belirli karakter türlerini bir dizenin başından veya sonundan kaldırır.

Boşluk, boşluk karakterinin, sekme karakterinin ve bu ikisinin diğer çeşitli varyantlarının genel terimidir. Yeni satırlar, metindeki satır sonlarıdır, bu _kulağa_ basit gelebilir, ancak pratikte elbette bunları yapmanın tek bir yolu yoktur, bu nedenle yeni satırları kesmemizi istediğimizde, bizim için tüm varyantları otomatik olarak halledecektir.

Örneğin, burada her iki yanında boşluk bulunan bir dize var:

```swift
var quote = "   The truth is rarely pure and never simple   "
```

Her iki taraftaki boşlukları ve yeni satırları kırpmak istiyorsak, bunu şu şekilde yapabiliriz:

```swift
let trimmed = quote.trimmingCharacters(in: .whitespacesAndNewlines)
```

Değer `.whitespacesAndNewlines`, Apple'ın Foundation API'sinden gelir ve aslında öyledir `trimmingCharacters(in:)`- bu kursun başında söylediğim gibi, Foundation gerçekten yararlı kodlarla doludur!

Her seferinde aramak zorunda olmak `trimmingCharacters(in:)`biraz endişe verici, o yüzden kısaltmak için bir uzantı yazalım:

```swift
extension String {
    func trimmed() -> String {
        self.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}
```

Bunu parçalayalım…

1.  `extension`Swift'e varolan bir türe işlevsellik eklemek istediğimizi söyleyen anahtar sözcükle başlıyoruz .
2.  Hangi tür? Sırada bu var: `String`.
3.  Şimdi bir parantez açıyoruz ve son kapanış parantezine kadar olan tüm kod dizelere eklenecek.
4.  `trimmed()`Yeni bir dize döndüren adında yeni bir yöntem ekliyoruz .
5.  `trimmingCharacters(in:)`İçeride , sonucunu geri göndererek önceki yöntemin aynısını çağırırız: .
6.  Burada nasıl kullanabileceğimize dikkat edin `self`- bu otomatik olarak mevcut dizgeye atıfta bulunur. Bu mümkündür çünkü şu anda bir dizi uzantısındayız.

Ve şimdi boşlukları ve yeni satırları kaldırmak istediğimiz her yerde aşağıdakileri yazabiliriz:

```swift
let trimmed = quote.trimmed()
```

Daha kolay!

Bu biraz yazma tasarrufu sağladı, ancak normal bir işlevden çok daha iyi _mi ?_

Gerçek şu ki, şöyle bir fonksiyon yazabilirdik:

```swift
func trim(_ string: String) -> String {
    string.trimmingCharacters(in: .whitespacesAndNewlines)
}
```

Sonra şu şekilde kullandı:

```swift
let trimmed2 = trim(quote)
```

Bu, hem işlevi oluşturma hem de kullanma açısından bir uzantı kullanmaktan daha az koddur. _Bu tür bir işleve global_ işlev denir , çünkü projemizin her yerinde kullanılabilir.

Bununla birlikte, uzantının, genel işleve göre aşağıdakiler de dahil olmak üzere bir dizi avantajı vardır:

1.  Xcode yazdığınızda `quote.`, uzantılara eklediğimiz tüm yöntemler de dahil olmak üzere dizedeki yöntemlerin bir listesini getirir. Bu, ekstra işlevselliklerimizin bulunmasını kolaylaştırır.
2.  Genel işlevler yazmak, kodunuzu oldukça dağınık hale getirir; bunları organize etmek ve takip etmek zordur. Öte yandan, uzantılar doğal olarak genişlettikleri veri türüne göre gruplandırılır.
3.  Uzantı yöntemleriniz orijinal türün tam bir parçası olduğundan, türün dahili verilerine tam erişim elde ederler. `private`Bu, örneğin erişim kontrolü ile işaretlenmiş özellikleri ve yöntemleri kullanabilecekleri anlamına gelir .

Dahası, uzantılar, değerleri yerinde değiştirmeyi, yani yeni bir değer döndürmek yerine bir değeri doğrudan değiştirmeyi kolaylaştırır.

Örneğin, daha önce boşlukları ve yeni satırları kaldırılmış yeni bir dize döndüren bir yöntem yazdık , ancak dizeyi _doğrudan_`trimmed()` değiştirmek istiyorsak, bunu uzantıya ekleyebiliriz:

```swift
mutating func trim() {
    self = self.trimmed()
}
```

Dize `quote`bir değişken olarak oluşturulduğundan, onu şu şekilde yerinde kırpabiliriz:

```swift
quote.trim()
```

Yöntemin şimdi biraz farklı adlandırmaya sahip olduğuna dikkat edin: yeni bir değer döndürdüğümüzde kullandık `trimmed()`, ancak dizeyi doğrudan değiştirdiğimizde kullandık `trim()`. `ed`Bu kasıtlıdır ve Swift'in tasarım yönergelerinin bir parçasıdır: Eğer onu yerinde değiştirmek yerine yeni bir değer döndürüyorsanız, veya `ing`gibi kelime sonları kullanmalısınız `reversed()`.

**İpucu:** Daha önce size diziler üzerindeki yöntemi tanıtmıştım `sorted()`. `sort()`Artık bu kuralı biliyorsunuz, bir değişken dizisi oluşturursanız , yeni bir kopya döndürmek yerine diziyi yerinde sıralamak için kullanabileceğinizi anlamalısınız .

Tiplere _özellikler_ eklemek için uzantıları da kullanabilirsiniz , ancak bir kural vardır: bunlar yalnızca _hesaplanmış_ özellikler olmalıdır, depolanmış özellikler olmamalıdır. Bunun nedeni, yeni saklanan özelliklerin eklenmesinin veri türlerinin gerçek boyutunu etkilemesidir - bir tamsayıya bir grup saklı özellik eklersek, o zaman her tamsayı her yerdeki bellekte daha fazla yer kaplamak zorunda kalır ve bu da her türden veri türüne neden olur. sorunların

Neyse ki, hesaplanan özellikleri kullanarak hala çok şey yapabiliriz. Örneğin, dizelere eklemek istediğim bir özellik `lines`, dizeyi tek tek satırlardan oluşan bir diziye bölen özellik olarak adlandırılır. `components(separatedBy:)`Bu , diziyi bizim seçtiğimiz bir sınırda bölerek bir dizi dizisine bölen, adı verilen başka bir dize yöntemini sarar . Bu durumda, bu sınırın yeni çizgiler olmasını isteriz, dolayısıyla bunu dize uzantımıza ekleriz:

```swift
var lines: [String] {
    self.components(separatedBy: .newlines)
}
```

`lines`Bununla birlikte , artık herhangi bir dizgenin özelliğini şu şekilde okuyabiliriz :

```swift
let lyrics = """
But I keep cruising
Can't stop, won't stop moving
It's like I got this music in my mind
Saying it's gonna be alright
"""

print(lyrics.lines.count)
```

İster tek satırlık ister karmaşık işlevsellik parçaları olsun, uzantıların her zaman aynı amacı vardır: kodunuzu daha kolay yazmak, daha kolay okumak ve uzun vadede daha kolay bakım yapmak.

Bitirmeden önce, uzantılarla çalışırken size gerçekten faydalı bir numara göstermek istiyorum. Daha önce Swift'in yapılar için üye bazında bir başlatıcıyı nasıl otomatik olarak oluşturduğunu gördünüz, bunun gibi:

```swift
struct Book {
    let title: String
    let pageCount: Int
    let readingHours: Int
}

let lotr = Book(title: "Lord of the Rings", pageCount: 1178, readingHours: 24)
```

Ayrıca, kendi başlatıcınızı oluşturmanın, Swift'in artık bizim için üye bazında sağlamayacağı anlamına geldiğinden de bahsetmiştim. Bu kasıtlıdır, çünkü özel bir başlatıcı, aşağıdaki gibi bazı özel mantığa dayalı olarak veri atamak istediğimiz anlamına gelir:

```swift
struct Book {
    let title: String
    let pageCount: Int
    let readingHours: Int

    init(title: String, pageCount: Int) {
        self.title = title
        self.pageCount = pageCount
        self.readingHours = pageCount / 50
    }
}
```

Swift, bu örnekte üye bazında başlatıcıyı tutarsa, yaklaşık okuma süresini hesaplama mantığımızı atlar.

Bununla birlikte, _bazen_ ikisini de istersiniz - özel bir başlatıcı kullanma becerisine sahip olmak, ancak aynı zamanda Swift'in otomatik üye bazında başlatıcısını da korumak istersiniz. Bu durumda, Swift'in tam olarak ne yaptığını bilmeye değer: eğer _yapımızın içine_ özel bir başlatıcı uygularsak , o zaman Swift, otomatik üye bazında başlatıcıyı devre dışı bırakır.

_Bu fazladan küçük ayrıntı, bundan sonra ne olacağı konusunda size bir ipucu verebilir: eğer bir extension_içinde özel bir başlatıcı uygularsak , Swift, otomatik üye bazında başlatıcıyı devre dışı _bırakmaz ._ Düşünürseniz bu mantıklıdır: Bir uzantının içine yeni bir başlatıcı eklemek varsayılan başlatıcıyı da devre dışı bırakırsa, bizden yapacağınız küçük bir değişiklik diğer tüm Swift kodlarını bozabilir.

Dolayısıyla, yapımızın varsayılan üye başlatıcıya ve özel başlatıcımıza sahip olmasını istiyorsak `Book`, özel olanı şöyle bir uzantıya yerleştiririz:

```swift
extension Book {
    init(title: String, pageCount: Int) {
        self.title = title
        self.pageCount = pageCount
        self.readingHours = pageCount / 50
    }
}
```

---

# Protokol Extensions nasıl oluşturulur ve kullanılır?

Protokoller, uygun türlerin uyması gereken sözleşmeleri tanımlamamıza izin verir ve uzantılar, mevcut türlere işlevsellik eklememize izin verir. _Ancak protokollere_ uzantılar yazabilseydik ne olurdu ?

Artık merak etmeyin çünkü Swift, uygun şekilde adlandırılmış _protokol uzantılarını_ kullanarak tam olarak bunu destekliyor : yöntem uygulamaları eklemek için tüm bir protokolü genişletebiliriz, yani o protokole uyan herhangi bir tür bu yöntemleri alır.

Önemsiz bir örnekle başlayalım. Bir dizinin herhangi bir değeri olup olmadığını kontrol eden bir koşul yazmak çok yaygındır, bunun gibi:

```swift
let guests = ["Mario", "Luigi", "Peach"]

if guests.isEmpty == false {
    print("Guest count: \(guests.count)")
}
```

`!`Bazı insanlar Boole operatörünü şu şekilde kullanmayı tercih eder :

```swift
if !guests.isEmpty {
    print("Guest count: \(guests.count)")
}
```

Bu yaklaşımlardan herhangi birinin gerçekten büyük bir hayranı değilim, çünkü bana doğal olarak "bazı diziler boş değilse" gibi gelmiyorlar?

Bunu, bunun gibi gerçekten basit bir uzantıyla düzeltebiliriz `Array`:

```swift
extension Array {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

**İpucu:** Xcode'un oyun alanları, kodlarını yukarıdan aşağıya çalıştırır, bu nedenle bu uzantıyı kullanıldığı yerin _önüne koyduğunuzdan emin olun._

Artık anlaşılmasının daha kolay olduğunu düşündüğüm bir kod yazabiliriz:

```swift
if guests.isNotEmpty {
    print("Guest count: \(guests.count)")
}
```

Ama daha iyisini yapabiliriz. Görüyorsunuz, `isNotEmpty`dizilere yeni ekledik, peki ya kümeler ve sözlükler? Elbette, kendimizi tekrarlayabilir ve kodu uzantılara kopyalayabiliriz, ancak daha iyi bir çözüm var: `Array`, `Set`ve tümü , , , ve daha fazlası gibi işlevler elde ettikleri , `Dictionary`adlı yerleşik bir protokole uygundur .`Collection``contains()``sorted()``reversed()`

Bu önemlidir, çünkü aynı zamanda mülkiyetin var olmasını `Collection`da gerektirir . `isEmpty`Dolayısıyla, üzerine bir uzantı yazarsak , gerekli olduğu için `Collection`yine erişebiliriz . Bu, bunu elde etmek için kodumuzda olarak `isEmpty`değiştirebileceğimiz anlamına gelir :`Array``Collection`

```swift
extension Collection {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

Bu tek sözcük değişikliği ile artık `isNotEmpty`dizilerde, kümelerde ve sözlüklerde ve ayrıca `Collection`. İster inanın ister inanmayın, bu küçük uzantı binlerce Swift projesinde var çünkü pek çok kişi okumayı daha kolay buluyor.

Daha da önemlisi, protokolü genişleterek, normalde bireysel yapılar içinde yapılması gereken işlevsellik ekliyoruz. _Bu gerçekten güçlüdür ve Apple'ın protokol yönelimli programlama_ dediği bir tekniğe yol açar - bir protokolde gerekli bazı yöntemleri listeleyebilir, ardından bunların varsayılan uygulamalarını bir protokol uzantısı içine ekleyebiliriz. Tüm uyumlu türler daha sonra bu varsayılan uygulamaları kullanır veya gerektiğinde kendi uygulamalarını sağlar.

Örneğin, bunun gibi bir protokolümüz olsaydı:

```swift
protocol Person {
    var name: String { get }
    func sayHello()
}
```

Bu, tüm uyumlu türlerin bir yöntem eklemesi gerektiği anlamına gelir `sayHello()`, ancak bunun gibi bir uzantı olarak bunun varsayılan bir uygulamasını da ekleyebiliriz:

```swift
extension Person {
    func sayHello() {
        print("Hi, I'm \(name)")
    }
}
```

Ve artık uyumlu türler isterlerse kendi yöntemlerini ekleyebilirler _, ancak buna gerek yoktur - protokol uzantımızda sağlanan yönteme her zaman güvenebilirler._`sayHello()`

Böylece, yöntem olmadan bir çalışan oluşturabiliriz `sayHello()`:

```swift
struct Employee: Person {
    let name: String
}
```

Ancak uyumlu olduğundan `Person`, uzantımızda sağladığımız varsayılan uygulamayı kullanabiliriz:

```swift
let taylor = Employee(name: "Taylor Swift")
taylor.sayHello()
```

Swift, protokol uzantılarını _çok_ kullanır , ancak dürüst olmak gerekirse, bunları henüz çok ayrıntılı bir şekilde anlamanıza gerek yok - hiç bir protokol uzantısı kullanmadan harika uygulamalar oluşturabilirsiniz. Bu noktada onların var olduğunu biliyorsunuz ve bu kadarı yeter!

---

# Protokol Extensions'dan en iyi şekilde nasıl yararlanılır?

Protokol uzantıları, Swift'in güçlü bir özelliğidir ve bunları kendi uygulamalarınızda kullanabilmek için zaten yeterince şey öğrendiniz. Ancak, merak ettiyseniz ve biraz zamanınız varsa, biraz teğet geçip onları daha fazla keşfedebiliriz.

**Not:** Bu kesinlikle başlangıç ​​seviyesindeki Swift'in ötesine geçiyor, bu yüzden lütfen devam etmek için herhangi bir baskı altında hissetmeyin - herhangi bir noktada bir sonraki bölüme geçebilirsiniz!

Hala burada? Tamam, başka bir protokol uzantısı deneyelim, bu sefer biraz daha karmaşık. İlk olarak, üzerine basit bir uzantı olarak yazacağız `Int`:

```swift
extension Int {
    func squared() -> Int {
        self * self
    }
}

let wholeNumber = 5
print(wholeNumber.squared())
```

Bu `squared()`, kareyi elde etmek için sayıyı kendisiyle çarpan bir yöntem ekler, böylece yukarıdaki kodumuz 25 yazdırır.

Aynı yöntemi a'da sadece kodu kopyalamadan istiyorsak `Double`, yaptığımız kalıbın aynısını izleyebilirdik : hem hem de benimseyen `Collection`bir protokol bulabilir ve bunu genişletebilirdik.`Int``Double`

Burada her iki tür de protokolü paylaşır `Numeric`, çünkü ikisi de sayıdır, bu yüzden bunu genişletmeye çalışabiliriz:

```swift
extension Numeric {
    func squared() -> Int {
        self * self
    }
}
```

Ancak, bu kod artık çalışmaz, çünkü `self * self`artık herhangi bir sayı olabilir, dahil , ve a'yı a ile `Double`çarparsanız kesinlikle bir geri dönüş alamazsınız .`Double``Double``Int`

Bunu çözmek için sadece anahtar kelimeyi kullanabiliriz `Self`– bunu kısaca statik özelliklere ve yöntemlere atıfta bulunduğumuzda tanıttım, çünkü mevcut veri tipine atıfta bulunmamıza izin veriyor. Burada kullanışlıdır, çünkü "bu yöntemin gerçekte çağrıldığı uyumlu tür ne olursa olsun" anlamına gelir ve şöyle görünür:

```swift
extension Numeric {
    func squared() -> Self {
        self * self
    }
}
```

Unutmayın `self`ve `Self`farklı şeyler ifade edin: `self`geçerli değeri ifade eder ve `Self`geçerli _türü_ ifade eder . Dolayısıyla, 5'e ayarlanmış bir tamsayımız olsaydı, fonksiyonumuz `squared()`etkin bir şekilde şöyle çalışırdı:

```swift
func squared() -> Int {
    5 * 5
}
```

`Self`Etkili bir şekilde var ve `Int`etkili `self`bir şekilde 5'tir. Veya 3.141'e ayarlanmış bir ondalık sayıya sahip olsaydık, `squared()`şöyle çalışırdı:

```swift
func squared() -> Double {
    3.141 * 3.141
}
```

## Daha ileri gitmek ister misin?

Hâlâ buradaysanız, protokol uzantılarını daha da fazla keşfetmeye devam etmek istediğinizi söylemenin güvenli olduğunu düşünüyorum ve ben kimim ki hayal kırıklığına uğratayım? Bu kesinlikle çok meraklı insanlar içindir - SwiftUI ile uygulama oluşturmaya başlamak için aşağıdakileri gerçekten bilmenize gerek _yoktur ._

Hala burada? Pekala, Swift'in ve `Equatable`kullanarak iki nesneyi karşılaştırmak için kullandığı yerleşik bir protokolle başlayalım .`==``!=`

Yapımızı şu şekilde `User`uyumlu hale getirebiliriz :`Equatable`

```swift
struct User: Equatable {
    let name: String
}
```

Ve şimdi iki kullanıcıyı karşılaştırabiliriz:

```swift
let user1 = User(name: "Link")
let user2 = User(name: "Zelda")
print(user1 == user2)
print(user1 != user2)
```

Burada herhangi bir özel çalışma yapmamıza gerek yok, çünkü Swift `Equatable`bizim için uygunluk sağlayabilir - bir nesnenin tüm özelliklerini diğer nesnedeki aynı özelliklerle karşılaştırır.

Daha da ileri gidebiliriz: `Comparable`Swift'in bir nesnenin diğerinden önce sıralanması gerekip gerekmediğini görmesini sağlayan adında bir Swift protokolü vardır. Swift bunu özel türlerimizde otomatik olarak uygulayamaz, ancak bu zor değildir: `<`yapınızın iki örneğini parametresi olarak kabul eden ve ilk örneğin ikinciden önce sıralanması gerekiyorsa true değerini döndüren bir işlev yazmanız gerekir.

Yani, şunu yazabiliriz:

```swift
struct User: Equatable, Comparable {
    let name: String
}

func <(lhs: User, rhs: User) -> Bool {
    lhs.name < rhs.name
}
```

**İpucu:** Swift hakkında daha fazla şey öğrendikçe, fonksiyonun kodunuzu biraz daha düzenli tutmanıza yardımcı olan _statik_`<` bir fonksiyon olarak uygulanabileceğini öğreneceksiniz .

`User`Kodumuz, iki örnek oluşturmamıza ve bunları `<`aşağıdaki gibi kullanarak karşılaştırmamıza izin vermek için yeterlidir :

```swift
let user1 = User(name: "Taylor")
let user2 = User(name: "Adele")
print(user1 < user2)
```

Bu çok güzel, ama gerçekten zekice olan şey, Swift'in aşağıdakileri de çalıştırmak için protokol uzantılarını kullanması:

```swift
print(user1 <= user2)
print(user1 > user2)
print(user1 >= user2)
```

Bu kod mümkündür, çünkü eşittir olup olmadığını `Equatable`bilmemize izin verir ve daha önce sıralanması gerekip gerekmediğini bilmemize izin verir ve bu iki parça ile Swift gerisini otomatik olarak çözebilir.`user1``user2``Comparable``user1``user2`

Daha da iyisi, işe başlamak `Equatable`için yapımıza ekleme yapmamıza bile gerek yok . `==`Yalnız bu iyi:

```swift
struct User: Comparable {
    let name: String
}
```

Sahne arkasında, Swift _protokol kalıtımını_ kullanır , böylece `Comparable`otomatik olarak aynı zamanda `Equatable`. Bu, sınıf mirasına benzer şekilde çalışır, dolayısıyla `Comparable`ondan miras alındığında `Equatable`tüm gereksinimlerini de devralır.

Her neyse, bu çok büyük bir teğet oldu - başınızı biraz döndürdüyse endişelenmeyin, sadece merak için ve Swift yolculuğunuza devam ettiğinizde daha anlamlı olacak!

---

# Özet: Protokoller ve uzantılar

Bu bölümlerde Swift'in bazı karmaşık ama güçlü özelliklerini ele aldık, ancak biraz uğraşırsanız üzülmeyin - bunları ilk başta kavramak gerçekten zor ve ancak zamanınız olduğunda gerçekten anlayacaklar. bunları kendi kodunuzda denemek için.

Öğrendiklerimizi tekrar özetleyelim:

-   Protokoller, kod sözleşmeleri gibidir: ihtiyaç duyduğumuz işlevleri ve yöntemleri belirleriz ve uygun türler bunları uygulamalıdır.
-   Opak dönüş türleri, kodumuzdaki bazı bilgileri gizlememize izin verir. Bu, gelecekte değişiklik yapma esnekliğini korumak istediğimiz anlamına gelebilir, ancak aynı zamanda devasa getiri türlerini yazmamıza gerek olmadığı anlamına da gelir.
-   Uzantılar, kendi özel türlerimize veya Swift'in yerleşik türlerine işlevsellik eklememize izin verir. Bu, bir yöntem eklemek anlamına gelebilir, ancak hesaplanmış özellikler de ekleyebiliriz.
-   Protokol uzantıları, aynı anda birçok türe işlevsellik eklememize izin verir - bir protokole özellikler ve yöntemler ekleyebiliriz ve uyumlu tüm türler bunlara erişebilir.

Kısaca özetlediğimizde bu özellikler kolay görünüyor, ama değiller. _Onlar hakkında_ bilgi sahibi olmanız, var olduklarını bilmeniz gerekir , ancak öğrenme yolculuğunuza devam etmek için bunları yalnızca yüzeysel olarak kullanmanız gerekir.