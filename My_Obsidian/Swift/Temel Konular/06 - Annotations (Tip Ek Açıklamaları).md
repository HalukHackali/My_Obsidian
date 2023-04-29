
#swift #yazılım 

Swift, ona atadığımız şeye bağlı olarak bir sabitin veya değişkenin ne tür verileri tuttuğunu anlayabilir. Ancak bazen hemen bir değer atamak istemiyoruz veya bazen Swift'in tip seçimini geçersiz kılmak istiyoruz ve işte burada tip ek açıklamaları devreye giriyor.

Şimdiye kadar bunun gibi sabitler ve değişkenler oluşturuyoruz:

```swift
let surname = "Lasso"
var score = 0
```

Bu, _tür çıkarımını_ kullanır : Swift, `surname` ona metin atadığımız için bunun bir string olduğu çıkarımını yapar ve sonra `score` ona bir tam sayı atadığımız için bunun bir _integer_ olduğu çıkarımını yapar.  

Tür ek açıklamaları, hangi veri türlerini istediğimiz konusunda net olmamızı sağlar ve şöyle görünür:

```swift
let surname: String = "Lasso"
var score: Int = 0
```

Şimdi açık konuşuyoruz: `surname` bir string olmalı ve `score` bir tamsayı olmalıdır. Bu tam olarak Swift'in tür çıkarımının zaten yapacağı şeydi, ama bazen öyle değil - bazen farklı bir tür seçmek isteyeceksiniz.

Örneğin, belki `score` bir ondalıktır, çünkü kullanıcı yarım puan alabilir, dolayısıyla şunu yazarsınız:

```swift
var score: Double = 0
```

Kısım olmadan `: Double`Swift bunun bir tamsayı olduğu sonucuna varırdı, ama biz bunu geçersiz kılıyoruz ve kesinlikle bir ondalık sayı olduğunu söylüyoruz.

Şimdiye kadar birkaç tür veriye baktık ve gerektiğinde doğru tür açıklamasını kullanabilmeniz için adlarını bilmeniz önemlidir.

`String`metni tutar:

```swift
let playerName: String = "Roy"
```

`Int`tam sayıları tutar:

```swift
var luckyNumber: Int = 13
```

`Double`ondalık sayıları tutar:

```swift
let pi: Double = 3.141
```

`Bool`true veya false tutar:

```swift
var isAuthenticated: Bool = true
```

`Array` eklediğiniz sırayla birçok farklı değeri tutar. Bu, aşağıdaki gibi uzmanlaşmış olmalıdır `[String]`:

```swift
var albums: [String] = ["Red", "Fearless"]
```

`Dictionary` verilere nasıl erişilmesi gerektiğine karar verdiğiniz birçok farklı değere sahiptir. Bu, aşağıdaki gibi uzmanlaşmış olmalıdır `[String: Int]`:

```swift
var user: [String: String] = ["id": "@twostraws"]
```

`Set` qbirçok farklı değeri tutar, ancak bunları, içerdiğini kontrol etmek için optimize edilmiş bir sırada saklar. Bu, aşağıdaki gibi uzmanlaşmış olmalıdır `Set<String>`:

```swift
var books: Set<String> = Set(["The Bluest Eye", "Foundation", "Girl, Woman, Other"])
```

Tüm bu türleri bilmek, başlangıç ​​değerleri vermek istemediğiniz zamanlar için önemlidir. Örneğin, bu bir dizi dizi oluşturur:

```swift
var soda: [String] = ["Coke", "Pepsi", "Irn-Bru"]
```

Burada tip ek açıklamasına gerek yoktur, çünkü Swift sizin bir dizi dizge atadığınızı görebilir. _Ancak, boş_bir dize dizisi oluşturmak istiyorsanız , türü bilmeniz gerekir:

```swift
var teams: [String] = [String]()
```

`[String]`Yine, tür ek açıklaması gerekli değildir, ancak yine de şeyi yapabilmeniz için bir dizge dizisinin as olarak yazıldığını bilmeniz gerekir . Unutmayın, boş diziler, sözlükler ve kümeler oluştururken aç ve kapat parantezlerini eklemeniz gerekir, çünkü Swift burada bunların oluşturulma şeklini özelleştirmemize izin verir.

Bazı insanlar tip ek açıklamasını kullanmayı tercih eder, ardından buna şu şekilde boş bir dizi atar:

```swift
var cities: [String] = []
```

Mümkün olduğunca tür çıkarımı kullanmayı tercih ediyorum, bu yüzden şunu yazarım:

```swift
var clues = [String]()
```

Tüm bunların yanı sıra, _numaralandırmalar_ da var . Numaralandırmalar diğerlerinden biraz farklıdır çünkü haftanın günlerini içeren bir numaralandırma, kullanıcının istediği UI temasını içeren bir numaralandırma veya hatta şu anda hangi ekranın gösterildiğini içeren bir numaralandırma gibi kendi yeni türlerimizi oluşturmamıza izin verirler. bizim uygulamamız

Bir enum'un değerleri, enum'un kendisiyle aynı türdedir, dolayısıyla şöyle bir şey yazabiliriz:

```swift
enum UIStyle {
    case light, dark, system
}

var style = UIStyle.light
```

Bu, Swift'in gelecekteki atamalar için enum adını kaldırmasına izin veren şeydir, böylece yazabiliriz `style = .dark`- for için herhangi bir yeni değerin `style`bir tür olması gerektiğini bilir`UIStyle`

_Şimdi, büyük olasılıkla tür ek açıklamalarını ne zaman_ kullanmanız gerektiğini soracaksınız , bu nedenle mümkün olduğunca tür çıkarımını kullanmayı tercih ettiğimi, yani bir sabite veya bir değere bir değer atadığımı bilmeniz sizin için yararlı olabilir. değişken ve Swift doğru türü otomatik olarak seçer. Bazen bu, `var score = 0.0`bir `Double`.

Bunun en yaygın istisnası, henüz bir değere sahip olmadığım sabitlerdir. Görüyorsunuz, Swift gerçekten akıllı: Henüz bir değeri olmayan bir sabit oluşturabilirsiniz, daha sonra bu değeri _sağlayın_ ve Swift, bir değer mevcut olana kadar onu yanlışlıkla kullanmamamızı sağlayacaktır. Ayrıca, değeri sabit kalması için yalnızca bir kez ayarlamanızı sağlar.

Örneğin:

```swift
let username: String
// lots of complex logic
username = "@twostraws"
// lots more complex logic
print(username)
```

Bu kod yasaldır: bir noktada bir dize içerecek diyoruz `username`ve kullanmadan önce bir değer veriyoruz. Atama satırı – `username = "@twostraws"`– eksik olsaydı, Swift bir değeri olmayacağı için kodumuzu oluşturmayı reddederdi ve benzer şekilde, ikinci kez `username`bir değer ayarlamaya çalışırsak Swift de şikayet ederdi.`username`

Bu tür bir kod, bir tür ek açıklaması _gerektirir_`username` , çünkü atanan bir başlangıç ​​değeri olmadan Swift, ne tür verilerin içereceğini bilemez .

Tip çıkarımı veya tip ek açıklaması kullanmanızdan bağımsız olarak, bir altın kural vardır: Swift, sabitlerinizin ve değişkenlerinizin hangi veri tiplerini içerdiğini her zaman bilmelidir. Bu, tip-güvenli bir dil olmanın özüdür ve benzeri `5 + true`veya benzeri saçma sapan şeyler yapmamızı engeller.

**Önemli:** Tür ek açıklaması, Swift'in tür çıkarımını bir dereceye kadar geçersiz kılmamıza izin verse de, bitmiş kodumuz yine de mümkün olmalıdır. Örneğin, buna izin verilmez:

```swift
let score: Int = "Zero"
```

Swift, "Sıfır"ı bizim için bir tamsayıya dönüştüremez, bunu talep eden bir tür ek açıklaması olsa bile, bu nedenle kod oluşturulmaz.