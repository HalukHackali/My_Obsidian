#swift #yazılım   

Fonksiyonların nasıl oluşturulacağını ve bunlara nasıl parametre ekleneceğini gördünüz, ancak işlevler genellikle verileri de _geri_ gönderir - bazı hesaplamalar yaparlar, ardından bu çalışmanın sonucunu arama sitesine geri döndürürler.

Swift'de bu fonksiyonların birçoğu yerleşiktir ve Apple'ın çerçevelerinde on binlercesi daha vardır. Örneğin, oyun alanımız her zaman en tepede olmuştur ve bu , bir sayının karekökünü hesaplamak `import Cocoa`gibi çeşitli matematiksel fonksiyonları içerir .`sqrt()`

Fonksiyon, `sqrt()`karekökünü hesaplamak istediğimiz sayı olan bir parametreyi kabul eder ve devam eder ve işi yapar, ardından karekökü geri gönderir.

Örneğin, şunu yazabiliriz:

```swift
let root = sqrt(169)
print(root)
```

_Bir fonksiyondan kendi_ değerinizi döndürmek istiyorsanız iki şey yapmanız gerekir:

1.  Fonksiyonunuzun açılış parantezinden önce bir ok ve ardından bir veri türü yazın; bu, Swift'e ne tür verilerin geri gönderileceğini söyler.
2.   Verilerinizi geri göndermek için `return` anahtar kelimesini kullanın .

Örneğin, programınızın çeşitli bölümlerinde bir zar atmak isteyebilirsiniz, ancak zarı her zaman 6 kenarlı bir zar kullanmaya zorlamak yerine, bunu bir fonksiyon haline getirebilirsiniz:

```swift
func rollDice() -> Int {
    return Int.random(in: 1...6)
}

let result = rollDice()
print(result)
```

Bu, fonksiyonun bir tamsayı döndürmesi gerektiğini söyler ve gerçek değer, anahtar kelime ile geri gönderilir `return`.

`rollDice()` Bu yaklaşımı kullanarak , programınız boyunca birçok yeri arayabilirsiniz ve hepsi 6 kenarlı bir zar kullanır. Ancak gelecekte 20 kenarlı bir zar kullanmak istediğinize karar verirseniz, programınızın geri kalanının güncellenmesi için bu fonksiyonu değiştirmeniz yeterlidir.

**Önemli:** Fonksiyonunuzun an döndüreceğini söylediğinizde `Int`, Swift her zaman an döndürmesini sağlayacaktır `Int`- bir değer geri göndermeyi unutamazsınız, çünkü kodunuz oluşturulmayacaktır.

Daha karmaşık bir örnek deneyelim: iki dize, sıralarına bakılmaksızın aynı harfleri içeriyor mu? Bu işlev iki dizi parametresini kabul etmeli ve harfleri aynıysa true döndürmelidir - yani "abc" ve "cab", her ikisi de bir "a", bir "b" ve bir "c" içerdiğinden doğru döndürmelidir.

Aslında bu sorunu zaten kendi başınıza çözecek kadar bilgilisiniz, ancak şimdiden o kadar çok şey öğrendiniz ki, muhtemelen bu görevi bu kadar kolaylaştıran bir şeyi unuttunuz: herhangi bir diziyi çağırırsanız, tüm özellikleriyle birlikte yeni bir dizi alırsınız `sorted()`. harfler alfabetik sırayla. `==`Yani, bunu her iki dizi için yaparsanız, harflerinin aynı olup olmadığını görmek için bunları karşılaştırmak için kullanabilirsiniz .

Devam edin ve işlevi kendiniz yazmayı deneyin. Yine, mücadele ederseniz endişelenmeyin - sizin için hepsi çok yeni ve yeni bilgileri hatırlamak için mücadele etmek, öğrenme sürecinin bir parçasıdır. Çözümü birazdan göstereceğim ama lütfen önce kendiniz deneyin.

Hala burada? Tamam, işte bir örnek çözüm:

```swift
func areLettersIdentical(string1: String, string2: String) -> Bool {
    let first = string1.sorted()
    let second = string2.sorted()
    return first == second
}
```

Bunu parçalayalım:

1.  adlı yeni bir işlev oluşturur `areLettersIdentical()`.
2.  İşlev iki dize parametresini kabul eder `string1`ve `string2`.
3.  İşlev, a döndürdüğünü söylüyor `Bool`, bu nedenle bir noktada her zaman doğru veya yanlış döndürmeliyiz.
4.  İşlev gövdesinin içinde, her iki diziyi de sıralarız ve ardından dizeleri karşılaştırmak için kullanırız `==`- eğer aynı iseler true, aksi takdirde false döndürür.

Bu kod, hem `string1`ve hem de `string2`sıralanmış değerlerini yeni sabitlere atayarak sıralar `first`ve `second`. Ancak buna gerek yok – bu geçici sabitleri atlayabilir ve sonuçları `sorted()`doğrudan şu şekilde karşılaştırabiliriz:

```swift
func areLettersIdentical(string1: String, string2: String) -> Bool {
    return string1.sorted() == string2.sorted()
}
```

Bu daha az kod, ancak daha da iyisini yapabiliriz. Görüyorsunuz, Swift'e bu fonksiyonun bir Boole değeri döndürmesi gerektiğini söyledik ve fonksiyonda yalnızca bir kod satırı olduğu için Swift bunun veri döndürmesi gerektiğini biliyor. `return`Bu nedenle, bir işlev yalnızca bir kod satırına sahip olduğunda, anahtar kelimeyi şu şekilde tamamen kaldırabiliriz :

```swift
func areLettersIdentical(string1: String, string2: String) -> Bool {
    string1.sorted() == string2.sorted()
}
```

Geri dönüp aynısını fonksiyon için de yapabiliriz `rollDice()`:

```swift
func rollDice() -> Int {
    Int.random(in: 1...6)
}
```

Unutmayın, bu yalnızca işleviniz tek bir kod satırı içerdiğinde işe yarar ve özellikle bu kod satırının aslında geri getirmeye söz verdiğiniz verileri döndürmesi gerekir.

Üçüncü bir örnek deneyelim. Okuldan Pisagor teoremini hatırlıyor musun? İçinde bir dik açı olan bir üçgeniniz varsa, hipotenüsün uzunluğunu diğer kenarların karesini alıp toplayıp sonucun karekökünü hesaplayarak hesaplayabileceğinizi belirtir.

Nasıl kullanılacağını zaten öğrendiniz , böylece iki ondalık sayı kabul eden ve başka bir sayı döndüren `sqrt()`bir işlev oluşturabiliriz :`pythagoras()`

```swift
func pythagoras(a: Double, b: Double) -> Double {
    let input = a * a + b * b
    let root = sqrt(input)
    return root
}

let c = pythagoras(a: 3, b: 4)
print(c)
```

Bu, `pythagoras()`iki parametreyi kabul eden `Double`ve diğerini döndüren, adlı bir işlevdir `Double`. İçinde kareler `a`ve `b`, bunları bir araya toplar, sonra bunu içine aktarır `sqrt()`ve sonucu geri gönderir.

Bu işlev aynı zamanda tek bir satıra indirgenebilir ve `return`anahtar kelimesi kaldırılabilir - bir deneyin. Her zaman olduğu gibi daha sonra size kendi çözümümü göstereceğim ama denemeniz önemli.

Hala burada? Tamam, işte benim çözümüm:

```swift
func pythagoras(a: Double, b: Double) -> Double {
    sqrt(a * a + b * b)
}
```

`return`Devam etmeden önce bahsetmek istediğim son bir şey var: Eğer fonksiyonunuz bir değer döndürmezse, fonksiyonu erken çıkmaya zorlamak için yine de tek başına kullanabilirsiniz . Örneğin, girdinin beklediğinizle eşleşip eşleşmediğini kontrol edebilirsiniz ve eşleşmiyorsa devam etmeden hemen önce işlevden çıkmak isteyebilirsiniz.

---

# Fonksiyonlardan birden çok değer nasıl döndürülür?

Bir işlevden tek bir değer döndürmek istediğinizde, işlevinizin açılış parantezinden önce bir ok ve bir veri türü yazarsınız, bunun gibi:

```swift
func isUppercase(string: String) -> Bool {
    string == string.uppercased()
}
```

Bu, bir dizeyi kendisinin büyük harfli sürümüyle karşılaştırır. Dize zaten tamamen büyük harfliyse, hiçbir şey değişmemiş olacak ve iki dize aynı olacak, aksi takdirde farklı olacak ve `==`false gönderecekler.

_Bir işlevden iki veya daha fazla_ değer döndürmek istiyorsanız , bir dizi kullanabilirsiniz. Örneğin, bir kullanıcının ayrıntılarını geri gönderen bir tane var:

```swift
func getUser() -> [String] {
    ["Taylor", "Swift"]
}

let user = getUser()
print("Name: \(user[0]) \(user[1])") 
```

`user[0]`Bu sorunlu, çünkü neyin ne olduğunu hatırlamak zor `user[1]`ve eğer o dizideki verileri ayarlarsak o zaman `user[0]`ve `user[1]`sonunda başka bir şey olabilir veya belki de hiç var olmayabiliriz.

Bunun yerine bir sözlük kullanabiliriz, ancak bunun da kendi sorunları var:

```swift
func getUser() -> [String: String] {
    [
        "firstName": "Taylor",
        "lastName": "Swift"
    ]
}

let user = getUser()
print("Name: \(user["firstName", default: "Anonymous"]) \(user["lastName", default: "Anonymous"])") 
```

Evet, artık kullanıcı verilerimizin çeşitli bölümlerine anlamlı adlar verdik, ancak şu çağrıya bakın - her ikisini de _bilsek_ ve var olacak `print()`olsak da , her şeyin istediğimiz gibi olmaması ihtimaline karşı yine de varsayılan değerler sağlamamız gerekiyor. beklemek.`firstName``lastName`

_Bu çözümlerin ikisi de oldukça kötü, ancak Swift'in demetler_ şeklinde bir çözümü var . Diziler, sözlükler ve kümeler gibi, demetler de birden çok veri parçasını tek bir değişkene koymamıza izin verir, ancak diğer seçeneklerden _farklı olarak_ demetlerin sabit bir boyutu vardır ve çeşitli veri türlerine sahip olabilir.

Fonksiyonumuz bir demet döndürdüğünde şöyle görünür:

```swift
func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}

let user = getUser()
print("Name: \(user.firstName) \(user.lastName)")
```

Bunu parçalayalım…

1.  Dönüş tipimiz şimdi `(firstName: String, lastName: String)`, iki dize içeren bir demet.
2.  Tuple'ımızdaki her dizenin bir adı vardır. Bunlar tırnak içinde değil: sözlüklerde sahip olduğumuz rasgele anahtar türlerinin aksine, dizimizdeki her bir öğe için özel adlardır.
3.  İşlevin içinde, söz verdiğimiz tüm öğeleri içeren, adlara eklenmiş bir demet geri gönderiyoruz: `firstName`"Taylor" olarak ayarlanıyor, vb.
4.  çağırdığımızda , , , vb. `getUser()`anahtar isimlerini kullanarak tuple'ın değerlerini okuyabiliriz.`firstName``lastName`

Demetlerin sözlüklere çok benzediğini biliyorum, ancak bunlar farklı:

1.  Bir sözlükteki değerlere eriştiğinizde, Swift bunların mevcut olup olmadığını önceden bilemez. `user["firstName"]`Evet, bunun olacağını biliyorduk ama Swift emin olamıyor ve bu yüzden varsayılan bir değer sağlamamız gerekiyor.
2.  Bir demetteki değerlere eriştiğinizde, demet kullanılabilir olacağını _söylediği_ için Swift onun kullanılabilir olduğunu önceden _bilir_ .
3.  Şunu kullanarak değerlere erişiyoruz `user.firstName`: bu bir dize değil, dolayısıyla yazım hatası yapma şansı da yok.
4.  Sözlüğümüz yanında yüzlerce başka değer içerebilir `"firstName"`, ancak demetimiz içeremez - içereceği tüm değerleri listelemeliyiz ve sonuç olarak hepsini içermesi ve başka hiçbir şey içermemesi garanti edilir.

Dolayısıyla, demetlerin sözlüklere göre önemli bir avantajı vardır: tam olarak hangi değerlerin var olacağını ve hangi türlere sahip olduğunu belirtiriz, oysa sözlükler istediğimiz değerleri içerebilir veya içermeyebilir.

Demetleri kullanırken bilinmesi gereken üç şey daha vardır.

İlk olarak, bir işlevden bir demet döndürüyorsanız, Swift zaten demetteki her bir öğeye verdiğiniz adları bilir, bu nedenle kullanırken bunları tekrarlamanız gerekmez `return`. Yani, bu kod önceki demetimizle aynı şeyi yapar:

```swift
func getUser() -> (firstName: String, lastName: String) {
    ("Taylor", "Swift")
}
```

İkincisi, bazen size öğelerin isimlerinin olmadığı demetler verildiğini göreceksiniz. Bu olduğunda, 0'dan başlayan sayısal indeksleri kullanarak demetin öğelerine şu şekilde erişebilirsiniz:

```swift
func getUser() -> (String, String) {
    ("Taylor", "Swift")
}

let user = getUser()
print("Name: \(user.0) \(user.1)")
```

Bu sayısal indeksler, öğeleri adlandıran demetlerde de mevcuttur, ancak ben her zaman adları kullanmayı tercih etmişimdir.

Son olarak, eğer bir işlev bir demet döndürürse, isterseniz demeti ayrı değerlere ayırabilirsiniz.

Bununla ne demek istediğimi anlamak için önce şu koda bir göz atın:

```swift
func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}

let user = getUser()
let firstName = user.firstName
let lastName = user.lastName

print("Name: \(firstName) \(lastName)")
```

Bu, adlı sürümüne geri döner `getUser()`ve demet çıktığında, öğeleri kullanmadan önce oradan ayrı içeriklere kopyalarız. Burada yeni bir şey yok; sadece verileri biraz hareket ettiriyoruz.

Bununla birlikte, tuple'ı öğesine atamak ve ardından tek tek değerleri oradan kopyalamak yerine , ilk adımı atlayabiliriz - dönüş değerini şu şekilde iki ayrı sabite `user`ayırabiliriz :`getUser()`

```swift
let (firstName, lastName) = getUser()
print("Name: \(firstName) \(lastName)")
```

Bu sözdizimi ilk başta canınızı sıkabilir, ancak daha önce sahip olduğumuz şey için gerçekten sadece kısa yol: geri aldığımız iki öğenin demetini `getUser()`iki ayrı sabite dönüştürmek.

Aslında, demetteki tüm değerlere ihtiyacınız yoksa, kullanarak bir adım daha ileri giderek `_`Swift'e demetin o kısmını yoksaymasını söyleyebilirsiniz:

```swift
let (firstName, _) = getUser()
print("Name: \(firstName)")
```

---
# Parametre etiketleri nasıl özelleştirilir

Swift geliştiricilerinin fonksiyon parametrelerini nasıl isimlendirmeyi sevdiklerini gördünüz çünkü bu, fonksiyon çağrıldığında ne yaptıklarını hatırlamayı kolaylaştırıyor. Örneğin, zarın kenar sayısını ve zar sayısını kontrol etmek için parametreleri kullanarak, bir zarı belirli sayıda atmak için bir fonksiyon yazabiliriz:

```swift
func rollDice(sides: Int, count: Int) -> [Int] {
    // Start with an empty array
    var rolls = [Int]()

    // Roll as many dice as needed
    for _ in 1...count {
        // Add each result to our array
        let roll = Int.random(in: 1...sides)
        rolls.append(roll)
    }

    // Send back all the rolls
    return rolls
}

let rolls = rollDice(sides: 6, count: 4)
```

`rollDice(sides: 6, count: 4)`Altı ay sonra bu kurala geri dönseniz bile, bunun oldukça açıklayıcı olduğundan eminim .

Harici kullanım için bu parametreleri adlandırma yöntemi Swift için o kadar önemlidir ki, hangi yöntemin çağrılacağını bulmak söz konusu olduğunda aslında adları kullanır. Bu, diğer birçok dilden oldukça farklıdır, ancak bu, Swift'te mükemmel bir şekilde geçerlidir:

```swift
func hireEmployee(name: String) { }
func hireEmployee(title: String) { }
func hireEmployee(location: String) { }
```

Evet, bunların hepsi adı verilen işlevlerdir `hireEmployee()`, ancak bunları çağırdığınızda Swift, sağladığınız parametre adlarına göre hangisini kastettiğinizi bilir. Çeşitli seçenekler arasında ayrım yapmak için, belgelerin her işleve parametreleri dahil olmak üzere atıfta bulunduğunu görmek çok yaygındır, örneğin: `hireEmployee(name:)`veya `hireEmployee(title:)`.

Ancak bazen, bu parametre adları _daha az_ yardımcı oluyor ve bakmak istediğim iki yol var.

`hasPrefix()`İlk olarak, daha önce öğrendiğiniz işlevi düşünün :

```swift
let lyric = "I see a red door and I want it painted black"
print(lyric.hasPrefix("I see"))
```

Aradığımızda, doğrudan kontrol etmek için ön eki iletiriz - ya da daha kötüsü `hasPrefix()`demeyiz . Nasıl olur?`hasPrefix(string:)``hasPrefix(prefix:)`

_Bir fonksiyonun parametrelerini tanımlarken aslında iki_ isim ekleyebiliriz : biri fonksiyonun çağrıldığı yerde kullanım için, diğeri ise fonksiyonun içinde kullanım için. bunu , Swift'in "bunu yoksay" deme şekli olan ve bu parametre için harici bir etiket olmamasına neden olan parametresinin harici adı olarak `hasPrefix()`belirtmek için kullanır .`_`

Daha iyi okunacağını düşünüyorsanız, aynı tekniği kendi fonksiyonlarımızda da kullanabiliriz. Örneğin, daha önce bu işleve sahiptik:

```swift
func isUppercase(string: String) -> Bool {
    string == string.uppercased()
}

let string = "HELLO, WORLD"
let result = isUppercase(string: string)
```

Buna bakıp tam olarak doğru olduğunu düşünebilirsiniz, ancak buna bakıp `string: string`can sıkıcı tekrarlar da görebilirsiniz. Ne de olsa, oraya bir ipten başka ne geçireceğiz?

Parametre adından önce bir alt çizgi eklersek, harici parametre etiketini şu şekilde kaldırabiliriz:

```swift
func isUppercase(_ string: String) -> Bool {
    string == string.uppercased()
}

let string = "HELLO, WORLD"
let result = isUppercase(string)
```

`append()`Bu, Swift'de bir diziye öğe eklemek veya `contains()`bir öğenin bir dizinin içinde olup olmadığını kontrol etmek gibi çok kullanılır - her iki yerde de bir etiket olmadan da parametrenin ne olduğu oldukça açıktır.

Harici parametre adlarıyla ilgili ikinci sorun, tam olarak doğru olmadıkları zamandır - onlara sahip olmak istiyorsunuz, bu yüzden `_`iyi bir fikir değil, ancak işlevin çağrı sitesinde doğal olarak okunmuyorlar.

Örnek olarak, daha önce incelediğimiz başka bir işlevi burada bulabilirsiniz:

```swift
func printTimesTables(number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(number: 5)
```

Bu kod geçerli Swift ve onu olduğu gibi bırakabiliriz. Ancak arama sitesi iyi okumuyor: `printTimesTables(number: 5)`. Şöyle çok daha iyi olur:

```swift
func printTimesTables(for: Int) {
    for i in 1...12 {
        print("\(i) x \(for) is \(i * for)")
    }
}

printTimesTables(for: 5)
```

Bu, çağrı sitesinde çok daha iyi okunuyor - kelimenin tam anlamıyla yüksek sesle "5 için çarpım tablosunu yazdır" diyebilirsiniz ve bu mantıklıdır. Ama şimdi geçersiz Swift'e sahibiz: `for`arama sitesinde izin verilmesine ve harika okunmasına rağmen, işlev içinde buna izin _verilmez ._

`_`Harici bir parametre adı yazmamıza gerek kalmaması için parametre adının önüne nasıl koyabileceğimizi zaten gördünüz . Diğer seçenek, oraya ikinci bir ad yazmaktır: biri harici olarak, diğeri dahili olarak kullanmak için.

İşte böyle görünüyor:

```swift
func printTimesTables(for number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5)
```

Orada yakından bakmanız gereken üç şey var:

1.  Şunu yazıyoruz `for number: Int`: harici isim `for`, dahili isim `number`, ve tipinde `Int`.
2.  İşlevi çağırdığımızda, parametre için harici adı kullanırız: `printTimesTables(for: 5)`.
3.  İşlevin içinde, parametre için dahili adı kullanırız: `print("\(i) x \(number) is \(i * number)")`.

`_`Böylece, Swift bize parametre adlarını kontrol etmek için iki önemli yol sunuyor: Kullanılmaması için harici parametre adını kullanabiliriz veya hem harici hem de dahili parametre adlarına sahip olmamız için oraya ikinci bir ad ekleyebiliriz .

**İpucu: Daha önce, bir işleve** _ilettiğiniz_ teknik değerlere "argümanlar" ve işlev içinde aldığınız değerlere de _parametreler_ dendiğinden daha önce bahsetmiştim . İşlerin biraz karıştığı yer burasıdır, çünkü artık her ikisi de işlev tanımında bağımsız değişken etiketlerimiz ve parametre adlarımız yan yana var. Dediğim gibi, her ikisi için de "parametre" terimini kullanacağım ve ayrım önemli olduğunda, "harici parametre adı" ve "dahili parametre adı" kullanarak ikisini birbirinden ayırdığımı göreceksiniz.

---

# Parametreler için varsayılan değerler nasıl sağlanır?

Fonksiyonlara parametre eklemek, özelleştirme noktaları eklememizi sağlar, böylece fonksiyonlar ihtiyaçlarımıza bağlı olarak farklı veriler üzerinde çalışabilir. Bazen kodumuzu esnek tutmak için bu özelleştirme noktalarını kullanıma sunmak isteriz, ancak diğer zamanlarda bunu düşünmek istemezsiniz - on seferden dokuzunda aynı şeyi istersiniz.

Örneğin, daha önce bu fonksiyona baktık:

```swift
func printTimesTables(for number: Int, end: Int) {
    for i in 1...end {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5, end: 20)
```

Bu, sayının 1 katından başlayarak herhangi bir bitiş noktasına kadar herhangi bir çarpım tablosunu yazdırır. Bu sayı, istediğimiz çarpım tablosuna bağlı olarak her zaman değişecektir, ancak bitiş noktası makul bir varsayılan sağlamak için harika bir yer gibi görünüyor - çoğu zaman 10 veya 12'ye kadar saymak isteyebiliriz, yine de açık bırakıyoruz. bazen farklı bir değere gitme olasılığı.

Bu sorunu çözmek için Swift, parametrelerimizin herhangi biri veya tümü için varsayılan değerler belirlememize izin verir. Bu durumda, varsayılan değeri 12 olarak ayarlayabiliriz `end`, yani bunu belirtmezsek otomatik olarak 12 kullanılacaktır.

İşte kodda nasıl göründüğü:

```swift
func printTimesTables(for number: Int, end: Int = 12) {
    for i in 1...end {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5, end: 20)
printTimesTables(for: 8)
```

Şimdi nasıl iki farklı şekilde arayabileceğimize dikkat edin `printTimesTables()`: her iki parametreyi de istediğimiz zamanlar için sağlayabiliriz, ancak yapmazsak – sadece yazarsak `printTimesTables(for: 8)`– o zaman için varsayılan değer olan 12 kullanılacaktır `end`.

Aslında, daha önce kullandığımız bazı kodlarda varsayılan bir parametreyi çalışırken gördük:

```swift
var characters = ["Lana", "Pam", "Ray", "Sterling"]
print(characters.count)
characters.removeAll()
print(characters.count)
```

Bu, bir diziye bazı dizeler ekler, sayısını yazdırır, ardından hepsini kaldırır ve sayımı yeniden yazdırır.

Bir performans optimizasyonu olarak Swift, dizilere öğelerini tutacak kadar bellek artı biraz fazladan zaman içinde biraz büyüyebilecekleri bellek verir. Diziye daha fazla öğe eklenirse, Swift otomatik olarak giderek daha fazla bellek ayırır, böylece olabildiğince az israf olur.

öğesini çağırdığımızda `removeAll()`, Swift dizideki tüm öğeleri otomatik olarak kaldıracak ve ardından diziye atanan tüm belleği boşaltacaktır. Genellikle isteyeceğiniz şey budur, çünkü sonuçta nesneleri bir nedenle kaldırıyorsunuz. Ancak bazen – sadece bazen – diziye pek çok yeni öğe eklemek üzere olabilirsiniz ve bu nedenle bu işlevin, önceki kapasiteyi korurken öğeleri kaldıran ikinci bir biçimi vardır:

```swift
characters.removeAll(keepingCapacity: true)
```

Bu, varsayılan bir parametre değeri kullanılarak gerçekleştirilir: varsayılan false değerine sahip bir Boolean'dır, böylece varsayılan olarak mantıklı olanı yapar ve aynı zamanda dizinin mevcut kapasitesini korumak istediğimiz zamanlar için `keepingCapacity`geçiş yapma seçeneğimizi de açık bırakır.`true`

Gördüğünüz gibi, varsayılan parametre değerleri, çoğu zaman aramayı can sıkıcı hale getirmeden işlevlerimizde esnekliği korumamıza izin verir - yalnızca alışılmadık bir şeye ihtiyacınız olduğunda bazı parametreleri göndermeniz gerekir.

---

# Fonksiyonlardaki hatalar nasıl ele alınır?

Okumak istediğiniz dosyanın olmaması veya indirmeye çalıştığınız verinin ağ kapalı olduğu için başarısız olması gibi şeyler her zaman ters gider. Hataları incelikle ele almasaydık, kodumuz çökerdi, bu yüzden Swift, hataları ele almamızı veya en azından ne zaman olabileceğini kabul etmemizi sağlar.

Bu üç adım alır:

1.  Swift'e olabilecek olası hataları anlatmak.
2.  Olursa hataları işaretleyebilecek bir işlev yazmak.
3.  Bu işlevi çağırmak ve oluşabilecek hataları işlemek.

Eksiksiz bir örnek üzerinde çalışalım: Kullanıcı bizden şifresinin ne kadar güçlü olduğunu kontrol etmemizi isterse, şifre çok kısa veya barizse ciddi bir hata işaretleyeceğiz.

Bu nedenle, olabilecek olası hataları tanımlayarak başlamalıyız. Bu, Swift'in mevcut `Error`türünü temel alan yeni bir numaralandırma yapmak anlamına gelir, bunun gibi:

```swift
enum PasswordError: Error {
    case short, obvious
}
```

Bu, şifreyle ilgili iki olası hata olduğunu söylüyor: `short`ve `obvious`. _Bunların ne anlama geldiğini_ değil , sadece var olduklarını tanımlar.

İkinci adım, bu hatalardan birini tetikleyecek bir işlev yazmaktır. Bir hata tetiklendiğinde - veya Swift'te _atıldığında_ - işlevde önemli bir şeylerin ters gittiğini ve normal şekilde devam etmek yerine herhangi bir değer geri göndermeden hemen sona erdiğini söylüyoruz.

Bizim durumumuzda, bir parolanın gücünü kontrol eden bir işlev yazacağız: eğer gerçekten kötüyse – 5 karakterden azsa veya çok iyi biliniyorsa – hemen bir hata atarız, ancak diğer tüm dizeler için "Tamam", "İyi" veya "Mükemmel" derecelerini döndürür.

İşte Swift'de nasıl göründüğü:

```swift
func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }

    if password == "12345" {
        throw PasswordError.obvious
    }

    if password.count < 8 {
        return "OK"
    } else if password.count < 10 {
        return "Good"
    } else {
        return "Excellent"
    }
}
```

Bunu parçalayalım…

1.  Bir işlev, kendisi işlemeden hata atabiliyorsa, işlevi `throws`dönüş türünden önce olduğu gibi işaretlemeniz gerekir.
2.  Fonksiyon tarafından tam olarak ne tür bir hata atıldığını belirtmiyoruz, sadece hata atabiliyor.
3.  ile işaretlenmiş olması, `throws`işlevin hata vermesi _gerektiği_ anlamına gelmez , sadece verebileceği anlamına gelir.
4.  Bir hata atma zamanı geldiğinde, `throw`vakalarımızdan birini takip ederek yazarız `PasswordError`. Bu, işlevden hemen çıkar, yani bir dize döndürmez.
5.  Hiçbir hata atılmazsa, işlev normal gibi davranmalıdır - bir dize döndürmesi gerekir.

Bu, hata atma işleminin ikinci adımını tamamlar: olabilecek hataları tanımladık, ardından bu hataları kullanarak bir fonksiyon yazdık.

Son adım, işlevi çalıştırmak ve oluşabilecek hataları ele almaktır. Swift Playgrounds, hata işleme konusunda oldukça esnektir, çünkü çoğunlukla öğrenme amaçlıdırlar, ancak gerçek Swift projeleriyle çalışmaya gelince, üç adım olduğunu göreceksiniz:

1.  . `do`_
2.  kullanarak bir veya daha fazla fırlatma işlevini çağırma `try`.
3.  . `catch`_

Sözde kodda şöyle görünür:

```swift
do {
    try someRiskyWork()
} catch {
    print("Handle errors here")
}
```

Mevcut fonksiyonumuzu kullanarak bunu deneyin yazmak isteseydik `checkPassword()`, şunu yazabilirdik:

```swift
let string = "12345"

do {
    let result = try checkPassword(string)
    print("Password rating: \(result)")
} catch {
    print("There was an error.")
}
```

İşlev `checkPassword()`düzgün çalışıyorsa, içine bir değer döndürür `result`ve ardından yazdırılır. Ancak herhangi bir hata atılırsa (ki bu durumda olacaktır), parola derecelendirme mesajı asla yazdırılmayacaktır - yürütme hemen bloğa atlayacaktır `catch`.

Bu kodun tartışmayı hak eden birkaç farklı bölümü var ama ben en önemlisine odaklanmak istiyorum: `try`. Bu, hata oluşturabilecek tüm işlevler çağrılmadan önce yazılmalıdır ve geliştiricilere, bir hata olması durumunda normal kod yürütmenin kesintiye uğrayacağına dair görsel bir işarettir.

kullandığınızda `try`, bir bloğun içinde olmanız `do`ve `catch`herhangi bir hatayı işleyebilecek bir veya daha fazla bloğunuz olduğundan emin olmanız gerekir. Bazı durumlarda, ve `try!`gerektirmeyen , ancak bir hata atılırsa kodunuzu çökertecek şekilde yazılmış bir alternatif kullanabilirsiniz - bunu nadiren ve yalnızca _bir_ hatanın atılamayacağından kesinlikle eminseniz kullanmalısınız.`do``catch`

`catch`Hataları yakalamak söz konusu olduğunda, her zaman her türlü hatayı işleyebilecek bir bloğa sahip olmalısınız . Ancak, isterseniz belirli hataları da yakalayabilirsiniz:

```swift
let string = "12345"

do {
    let result = try checkPassword(string)
    print("Password rating: \(result)")
} catch PasswordError.short {
    print("Please use a longer password.")
} catch PasswordError.obvious {
    print("I have the same combination on my luggage!")
} catch {
    print("There was an error.")
}
```

İlerledikçe, fırlatma işlevlerinin Apple'ın kendi çerçevelerinin çoğunda nasıl yapıldığını göreceksiniz, bu nedenle, bunları kendiniz çok fazla oluşturamasanız da en azından bunları güvenli bir şekilde nasıl _kullanacağınızı_ bilmeniz gerekecek.

**İpucu:** Apple tarafından atılan çoğu hata, gerekirse kullanıcınıza sunabileceğiniz anlamlı bir mesaj sağlar. `error`Swift bunu bloğunuz içinde otomatik olarak sağlanan bir değer kullanarak sağlar ve tam olarak ne olduğunu görmek için `catch`okumak yaygın bir uygulamadır .`error.localizedDescription`

