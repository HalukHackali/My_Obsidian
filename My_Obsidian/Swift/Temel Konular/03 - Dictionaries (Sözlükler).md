#swift #yazılım 

Gördüğünüz gibi, Swift dizileri `songs[0]` gibi sayısal indekslerini kullanarak ulaşılabilen koleksiyonlardır. Sözlükler ise bir diğer yaygın koleksiyon tipidir. Ama dizilerden farklı olarak, belirlediğiniz anahtar (key) temelli olarak üzerindeki değere (value) ulaşabilirsiniz.

Örnek olarak, bir kişi hakkındaki verileri bir dizi içine nasıl sakladığımızı düşünelim:

```swift
var person = ["Taylor", "Alison", "Swift", "December", "taylorswift.com"]
```

Kişinin ikinci adını elde edebilmek için `person[1]`, doğduğu yıl için ise `person[3]` yazarız. Aslında bu bazı sorunları içerir; dizi içindeki her değerin atandığı indeksini hatırlamak çok zor! Peki ya kişinin ikinci adı yoksa? Yazdığın kodda kaos oluşturacak bir alta kayma söz konusu olur o zaman.

Sözlüklerle çok daha duyarlı bir şekilde tekrardan yazabiliriz, çünkü rastgele seçeceğiniz sayılardan ziyade, belirlediğiniz bir anahtarı kullanarak değeri okuyabilir ve yazabilirsiniz. Örneğin:

```swift
var person = ["first": "Taylor", "middle": "Alison", "last": "Swift", "month": "December", "website": "taylorswift.com"]
person["middle"]
person["month"]
```

Daha fazla boşluk kullanarak, sözlüğün ekranınızda kesilmeden görüntülemek daha iyi anlamanıza yardımcı olabilir:

```swift
var person = [
                "first": "Taylor",
                "middle": "Alison",
                "last": "Swift",
                "month": "December",
                "website": "taylorswift.com"
            ]

person["middle"]
person["month"]
```

Gördüğünüz gibi, bir sözlük oluşturduğunuzda önce anahtarı, ardından iki nokta üst üsteyi, sonra da değeri yazarsınız. Böylece üzerinde çalışmayı çok daha kolaylaştıran sadece anahtarı yazarak, sözlükteki herhangi bir değeri okuyabilirsiniz.

Dizilerde olduğu gibi, anahtarları çoğunlukla String olmalasına rağmen, çeşitli değerleri sözlük içesine saklayabilirsiniz.

---

# Dictionari'lerde veri nasıl saklanır ve bulunur

Dizilerin, haftanın günleri veya bir şehir için sıcaklıklar gibi belirli bir sıraya sahip verileri depolamanın nasıl harika bir yolu olduğunu gördünüz. Diziler, öğelerin onları eklediğiniz sırayla saklanması gerektiğinde veya orada yinelenen öğeleriniz olduğunda harika bir seçimdir, ancak çoğu zaman verilere dizideki konumuna göre erişmek can sıkıcı ve hatta tehlikeli olabilir.

Örneğin, işte bir çalışanın ayrıntılarını içeren bir dizi:

```swift
var employee = ["Taylor Swift", "Singer", "Nashville"]
```

Verilerin bir çalışanla ilgili olduğunu söylemiştim, bu nedenle çeşitli bölümlerin ne yaptığını tahmin edebilirsiniz:

```swift
print("Name: \(employee[0])")
print("Job title: \(employee[1])")
print("Location: \(employee[2])")
```

Ama bunun birkaç sorunu var. İlk olarak, `employee[2]` konumunun olduğundan tam olarak emin olamazsınız - bu onların şifresi olabilir. İkincisi, özellikle diziyi bir değişken yaptığımız için, 2. öğenin orada olduğunun garantisi yoktur. Bu tür bir kod ciddi sorunlara neden olur:

```swift
print("Name: \(employee[0])")
employee.remove(at: 1)
print("Job title: \(employee[1])")
print("Location: \(employee[2])")    
```

Bu, artık Nashville'i iş unvanı olarak yazdırıyor, bu yanlış ve kodumuzun `employee[2]` okuduğunda çökmesine neden olacak, ki bu sadece _bad_.

Swift'in her iki sorun için de _sözlük_ adı verilen bir çözümü var. Sözlükler, öğeleri dizilerin yaptığı gibi konumlarına göre saklamaz, bunun yerine öğelerin nerede saklanması gerektiğine karar vermemize izin verin.

Örneğin, önceki örneğimizi her bir öğenin ne olduğu hakkında daha açık olacak şekilde yeniden yazabiliriz:

```swift
let employee2 = ["name": "Taylor Swift", "job": "Singer", "location": "Nashville"]
```

Bunu ayrı satırlara ayırırsak, kodun ne yaptığı hakkında daha iyi bir fikir edineceksiniz:

```swift
let employee2 = [
    "name": "Taylor Swift",
    "job": "Singer", 
    "location": "Nashville"
]
```

Gördüğünüz gibi, şimdi gerçekten net davranıyoruz: adı Taylor Swift, iş Singer ve konum Nashville. Swift soldaki dizeleri çağırır - ad, iş ve konum - sözlüğün _anahtarlarını_ ve sağdaki dizeler _değerlerdir_.

Sözlükten veri okumaya gelince, onu oluştururken kullandığınız tuşları kullanırsınız:

```swift
print(employee2["name"])
print(employee2["job"])
print(employee2["location"])
```

If you try that in a playground, you’ll see Xcode throws up various warnings along the lines of “Expression implicitly coerced from 'String?' to 'Any’”. Worse, if you look at the output from your playground you’ll see it prints `Optional("Taylor Swift")` rather than just `Taylor Swift` – what gives?

Pekala, şunu bir düşünün:

```swift
print(employee2["password"])
print(employee2["status"])
print(employee2["manager"])
```

Bunların hepsi geçerli Swift kodu, ancak bunlara eklenmiş bir değeri olmayan sözlük anahtarlarını okumaya çalışıyoruz. Elbette, Swift burada tıpkı var olmayan bir dizi dizini okursanız çökeceği gibi çökebilir, ancak bu çalışmayı çok zorlaştıracaktır - en azından 10 öğeli bir diziniz varsa, 0'dan 9'a kadar olan endeksleri okumanın güvenli olduğunu bilirsiniz. ("Emin olmadığınız takdirde, "indeks"in çoğul halidir.)

Swift bir alternatif sunuyor: bir sözlüğün içindeki verilere eriştiğinizde, bize "bir değeri geri alabilirsiniz, ancak hiçbir şeyi geri alamıyor olabilirsiniz" diyecektir. Swift bu _isteğe bağlıları_ çağırır çünkü verilerin varlığı isteğe bağlıdır - orada olabilir veya olmayabilir.

Swift, kodu yazdığınızda, oldukça belirsiz bir şekilde de olsa sizi uyaracak - "İfade dolaylı olarak 'Dize'den zorlandı mı?' diyecek. 'Herhangi bir'ye", ama bu gerçekten "bu veriler aslında orada olmayabilir - yazdırmak istediğinizden emin misiniz?" anlamına gelecektir.

İsteğe bağlı olanlar, daha sonra ayrıntılı olarak ele alacağımız oldukça karmaşık bir konudur, ancak şimdilik size daha basit bir yaklaşım göstereceğim: bir sözlükten okurken, anahtar yoksa kullanmak için _varsayılan_ bir değer sağlayabilirsiniz.

İşte böyle görünüyor:

```swift
print(employee2["name", default: "Unknown"])
print(employee2["job", default: "Unknown"])
print(employee2["location", default: "Unknown"])
```

Tüm örnekler hem anahtarlar hem de değerler için dizeler kullandı, ancak her ikisi için de diğer veri türlerini kullanabilirsiniz. Örneğin, hangi öğrencilerin okuldan mezun olduğunu isimler için dizeler ve mezuniyet durumları için Booleans kullanarak takip edebiliriz:

```swift
let hasGraduated = [
    "Eric": false,
    "Maeve": true,
    "Otis": false,
]
```

Ya da Olimpiyatların gerçekleştiği yılları konumlarıyla birlikte takip edebiliriz:

```swift
let olympics = [
    2012: "London",
    2016: "Rio de Janeiro",
    2021: "Tokyo"
]

print(olympics[2012, default: "Unknown"])
```

Ayrıca saklamak istediğiniz açık türleri kullanarak boş bir sözlük oluşturabilir, ardından anahtarları tek tek ayarlayabilirsiniz:

```swift
var heights = [String: Int]()
heights["Yao Ming"] = 229
heights["Shaquille O'Neal"] = 216
heights["LeBron James"] = 206
```

Anahtarları için dizeler ve değerleri için tamsayılar içeren bir sözlük anlamına gelmek için şimdi `[String: Int]` yazmamız gerektiğine dikkat edin.

Her sözlük öğesinin belirli bir anahtarda bulunması gerektiğinden, sözlükler yinelenen anahtarların var olmasına izin vermez. Bunun yerine, zaten var olan bir anahtar için bir değer ayarlarsanız, Swift önceki değerin üzerine yazacaktır.

Örneğin, bir arkadaşınızla süper kahramanlar ve süper kötüler hakkında sohbet ediyorsanız, bunları şöyle bir sözlükte saklayabilirsiniz:

```swift
var archEnemies = [String: String]()
archEnemies["Batman"] = "The Joker"
archEnemies["Superman"] = "Lex Luthor"
```

Arkadaşınız Joker'in Batman'in baş düşmanı olduğuna katılmıyorsa, aynı anahtarı kullanarak bu değeri yeniden yazabilirsiniz:

```swift
archEnemies["Batman"] = "Penguin"
```

Son olarak, şu ana kadar gördüğümüz diziler ve diğer veri türleri gibi, sözlükler de gelecekte kullanmak isteyeceğiniz bazı yararlı işlevlerle birlikte gelir. tıpkı diziler için yaptıkları gibi, `count` and `removeAll()`.

---

# Sözlüklerde veri nasıl saklanır ve bulunur?

Dizilerin, haftanın günleri veya bir şehrin sıcaklıkları gibi belirli bir sıraya sahip verileri depolamanın harika bir yolu olduğunu gördünüz. Diziler, öğelerin eklediğiniz sırayla saklanması gerektiğinde veya orada yinelenen öğeleriniz olduğunda harika bir seçimdir, ancak çoğu zaman dizideki konumuna göre verilere erişmek can sıkıcı ve hatta tehlikeli olabilir.

Örneğin, işte bir çalışanın ayrıntılarını içeren bir dizi:

```swift
var employee = ["Taylor Swift", "Singer", "Nashville"]
```

Size verilerin bir çalışanla ilgili olduğunu söyledim, bu nedenle çeşitli bölümlerin ne işe yaradığını tahmin edebilirsiniz:

```swift
print("Name: \(employee[0])")
print("Job title: \(employee[1])")
print("Location: \(employee[2])")
```

Ama bunun birkaç sorunu var. İlk olarak, konumlarının bu olduğundan gerçekten emin olamazsınız `employee[2]`- belki de şifreleri budur. İkincisi, özellikle diziyi bir değişken yaptığımız için, 2. öğenin orada olduğunun garantisi yoktur. Bu tür bir kod ciddi sorunlara neden olur:

```swift
print("Name: \(employee[0])")
employee.remove(at: 1)
print("Job title: \(employee[1])")
print("Location: \(employee[2])")    
```

Bu, Nashville'i iş unvanı olarak yazdırıyor, bu yanlış ve okunduğunda kodumuzun çökmesine neden olacak ki `employee[2]`bu çok _kötü_ .

_Swift'in bu sorunların her ikisi için de sözlükler_ adı verilen bir çözümü var . Sözlükler, diziler gibi öğeleri konumlarına göre saklamaz, bunun yerine öğelerin nerede depolanacağına _biz karar veririz._

Örneğin, her bir öğenin ne olduğu konusunda daha açık olmak için önceki örneğimizi yeniden yazabiliriz:

```swift
let employee2 = ["name": "Taylor Swift", "job": "Singer", "location": "Nashville"]
```

Bunu ayrı satırlara ayırırsak, kodun ne yaptığı hakkında daha iyi bir fikir edinirsiniz:

```swift
let employee2 = [
    "name": "Taylor Swift",
    "job": "Singer", 
    "location": "Nashville"
]
```

Gördüğünüz gibi, artık gerçekten açık konuşuyoruz: isim Taylor Swift, iş Singer ve mekan Nashville. Swift soldaki dizeleri - ad, iş ve konum - sözlüğün _anahtarlarını çağırır ve sağdaki dizeler_ _değerlerdir_ .

Sözlükten veri okumak söz konusu olduğunda, onu oluştururken kullandığınız tuşları kullanırsınız:

```swift
print(employee2["name"])
print(employee2["job"])
print(employee2["location"])
```

Bunu bir oyun alanında denerseniz, Xcode'un "'String?'den dolaylı olarak zorlanan ifade?" 'Herhangi birine'”. Daha da kötüsü, oyun alanınızdaki çıktıya bakarsanız, bunun `Optional("Taylor Swift")`yalnızca `Taylor Swift`- ne verir?

Pekala, şunu düşün:

```swift
print(employee2["password"])
print(employee2["status"])
print(employee2["manager"])
```

Bunların hepsi geçerli Swift kodu, ancak kendilerine eklenmiş bir değere sahip olmayan sözlük anahtarlarını okumaya çalışıyoruz. Elbette, Swift burada tıpkı var olmayan bir dizi dizini okursanız çökeceği gibi _çökebilir_ , ancak bu, onunla çalışmayı çok zorlaştırır - en azından güvenli olduğunu bildiğiniz 10 öğeli bir diziniz varsa 0'dan 9'a kadar olan indeksleri okuyun. (“Endeksler”, emin olmamanız durumunda, “indeks”in çoğul halidir.)

Bu nedenle, Swift bir alternatif sunuyor: Bir sözlük içindeki verilere eriştiğinizde, bize "bir değeri geri alabilirsiniz, ancak hiçbir şey geri alamayabilirsiniz" diyecektir. Swift, verilerin varlığı isteğe bağlı olduğu için bu _isteğe bağlıları_ çağırır - orada olabilir veya olmayabilir.

Oldukça belirsiz bir şekilde de olsa, Swift, kodu yazdığınızda sizi uyaracaktır. "Herhangi biri" olarak, ancak bu gerçekten "bu veriler aslında orada olmayabilir - onu yazdırmak istediğinizden emin misiniz?" anlamına gelir.

İsteğe bağlı seçenekler, daha sonra ayrıntılı olarak ele alacağımız oldukça karmaşık bir konudur, ancak şimdilik size daha basit bir yaklaşım göstereceğim: Bir sözlükten okurken, anahtar yoksa kullanmak için _varsayılan_ bir değer sağlayabilirsiniz. .

İşte böyle görünüyor:

```swift
print(employee2["name", default: "Unknown"])
print(employee2["job", default: "Unknown"])
print(employee2["location", default: "Unknown"])
```

Tüm örneklerde hem anahtarlar hem de değerler için dizeler kullanılmıştır, ancak bunlardan herhangi biri için diğer veri türlerini kullanabilirsiniz. Örneğin, hangi öğrencilerin okuldan mezun olduğunu adlar için dizeler ve mezuniyet durumları için Boolean'lar kullanarak takip edebiliriz:

```swift
let hasGraduated = [
    "Eric": false,
    "Maeve": true,
    "Otis": false,
]
```

Ya da olimpiyatların yapıldığı yılları, konumları ile birlikte takip edebiliriz:

```swift
let olympics = [
    2012: "London",
    2016: "Rio de Janeiro",
    2021: "Tokyo"
]

print(olympics[2012, default: "Unknown"])
```

Ayrıca saklamak istediğiniz açık türleri kullanarak boş bir sözlük oluşturabilir, ardından anahtarları birer birer ayarlayabilirsiniz:

```swift
var heights = [String: Int]()
heights["Yao Ming"] = 229
heights["Shaquille O'Neal"] = 216
heights["LeBron James"] = 206
```

`[String: Int]`Anahtarları için dizeleri ve değerleri için tamsayıları olan bir sözlük anlamına gelmek için şimdi nasıl yazmamız gerektiğine dikkat edin .

Her sözlük öğesinin belirli bir anahtarda bulunması gerektiğinden, sözlükler yinelenen anahtarların var olmasına izin vermez. Bunun yerine, zaten var olan bir anahtar için bir değer ayarlarsanız, Swift önceki değerin üzerine yazacaktır.

Örneğin, bir arkadaşınızla süper kahramanlar ve süper kötüler hakkında sohbet ediyorsanız, onları şu şekilde bir sözlükte saklayabilirsiniz:

```swift
var archEnemies = [String: String]()
archEnemies["Batman"] = "The Joker"
archEnemies["Superman"] = "Lex Luthor"
```

Arkadaşınız Joker'in Batman'in baş düşmanı olduğu konusunda hemfikir değilse, aynı anahtarı kullanarak bu değeri yeniden yazabilirsiniz:

```swift
archEnemies["Batman"] = "Penguin"
```

Son olarak, şimdiye kadar gördüğümüz diziler ve diğer veri türleri gibi, sözlükler de gelecekte kullanmak isteyeceğiniz bazı yararlı işlevlerle gelir ve her ikisi de `count`sözlükler `removeAll()`için mevcuttur ve tıpkı diziler için yaptıkları gibi çalışır.