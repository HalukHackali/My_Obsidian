#swift #yazılım 

Fonksiyonlar, belirli fonksiyonellikleri olan parçaları işleten yeniden kullanılabilen kod parçaları tanımlamanızı sağlar. Genellikle fonksiyonlar, çalıştıkları şekli değiştiren bazı değerler kabul edebilirler, ama bu gerekli değil.

Basit bir fonksiyonla başlayalım:

```swift
func favoriteAlbum() {
    print("My favorite is Fearless")
}
```

Eğer bu kodu oyun alanınıza koyarsanız, hiçbir şey yazdırılmaz. Evet, fonksiyonda herhangi bir yanlışlık yok. İçerisinde "My favorite is Fearless" mesajı bulunan `favoriteAlbum()` adındaki bu fonksiyonun hiçbir şey yazdırmamasının sebebi, bu fonksiyonun çağırılmamasıdır. Fonksiyonu çalıştırmak için alt satıra şu kodu ekleyin:

```swift
favoriteAlbum()
```

Bu şekilde fonksiyon çalıştırılır (veya "çağırılır"), böylece biz de "My favorite is Fearless" çıktısını görebiliriz.

Gördüğünüz gibi, bir fonksiyon `func` yazarak tanımlanır, ardından fonksiyonun adı ve parantezler açılır ve kapanır, parantezlerin içine de kod bloğu yerleştirilir. Fonksiyonun adını takip eden parantezler konularak çağırılır.

Tabi bu budalaca bir örnek; bu fonksiyon ne olursa olsun aynı şeyi yapar, yani varoluşunun bir anlamı yoktur. Ama ya her defasında farklı bir albümü yazmasını isteseydik? bu durumda, Swift'e fonksiyonumuz her çağrıldığında bir değer kabul etmesini, ardından da bu değeri kullanmasını isteyebilirdik.

Hadi şimdi bunu yapalım:

```swift
func favoriteAlbum(name: String) {
    print("My favorite is \(name)")
}
```

Bu, bir String olması gereken ve "name" olarak adlandırılan (parametre de denebilir) bir değer kabul eden fonksiyon istediğimizi Swift'e söyler. That tells Swift we want the function to accept one value (called a "parameter"), named "name", that should be a string. Sonra biz de çıktı mesajımızın içine doğrudan sevdiğimiz albümümüzün adını yazmak için String eklemesini (interpolasyon) kullanırız. Şimdi fonksiyonu çağırmak için, şunu yazabilirsiniz:

```swift
favoriteAlbum(name: "Fearless")
```

Hala amacın ne olduğunu merak ediyor olabilirsiniz; sonuçta verilen tek satırlık bir kod. Şöyle düşünün: Biz bu fonksiyonu büyük bir uygulamanın 20 farklı yerinde kullandık. Sonra baş tasarımcı geldi ve mesajı "I love Fearless so much – it's my favorite!" ile değiştirmenizi söyledi. Kodunuzdaki tüm bu 20 fonksiyonu tek tek bulup değiştirmeyi gerçekten ister misiniz? Muhtemelen hayır. İşte, fonksiyonla bunu bir kez değiştirirsiniz ve her şey güncellenir.

Fonksiyonunuzu istediğiniz kadar parametre kabul edecek şekilde oluşturabilirsiniz. Bu fonksiyonu bir name (isim) ve year (yıl) kabul edecek şekilde yapalım:

```swift
func printAlbumRelease(name: String, year: Int) {
    print("\(name) was released in \(year)")
}

printAlbumRelease(name: "Fearless", year: 2008)
printAlbumRelease(name: "Speak Now", year: 2010)
printAlbumRelease(name: "Red", year: 2012)
```

Bu fonksiyon parametre isimleri önemlidir ve aslında fonksiyonun kendisinin parçalarıdır. Bazen aynı adla bir çok fonksiyon görürsünüz; örneğin `handle()`, ama farklı eylemleri ayıracak olan şey farklı parametre isimleridir.

## Dahili ve harici parametre isimleri

Bazen fonksiyon çağrıldığı zaman kullanmak için parametreleri isimlendirirsin, bazen de fonksiyonun içinde kullanılması için isimlendirirsin. Bu, bir fonksiyonu çağırdığında çoğunlukla doğal İngilizce kullandığı anlamına gelir, ama fonksiyonun içinde parametreler duyarlı isimlere sahiptir. Bu teknik Swift dilinde çok sık kullanılır, o yüzden şimdi anlamaya değer bir konudur.

Bunu göstermek için, bir String'deki harf sayısını veren bir fonksiyon yazalım. String'lerin özelliklerinden olan `count` ifadesini kullanalım. Dolayısıyla şu şekilde yazabiliriz:

```swift
func countLettersInString(string: String) {
    print("The string \(string) has \(string.count) letters.")
}
```

Bu fonksiyonu şu şeklide çağırabiliriz:

```swift
countLettersInString(string: "Hello")
```

Çalışmasında bir sorun olmamasına rağmen, biraz sözcükvari oldu bu şekliyle. Ayrıca "count letters in string string hello" (hello stringi stringindeki harfleri say) ifadesini sesli olarak söylemek de kulağa hoş gelmeyecek.

Swift dilinin çözümü, parametre için bir ismi çağrıldığında kullanmak için, diğerini de metodun içinde kullanmak için tanımlamanıza izin vermek olacaktır. Bunu kullanmak için, parametre adını bir harici, bir de dahili olmak üzere iki kez yazmak yeterli.

Örneğin parametre adını, çağrıldığı zaman kullanmak için `myString`, metodun içinde kullanmak için ise `str` olarak verebiliriz:

```swift
func countLettersInString(myString str: String) {
    print("The string \(str) has \(str.count) letters.")
}

countLettersInString(myString: "Hello")  
```

Harici parametre adını `_` alttan çizgi olarak da tanımlayabilirsiniz. Bu şekilde kullanım, Swift diline harici ismin çok da önemli olmadığını söyler. Örneğin:

```swift
func countLettersInString(_ str: String) {
    print("The string \(str) has \(str.count) letters.")
}

countLettersInString("Hello")
```

Gördüğünüz gibi bu, kodu İngilizce bir tümce okuyormuş gibi yapar: “count letters in string hello" (hello String'indeki harfleri say". 

Alttan çizgi `_` kullanımının doğru bir seçim olduğu bir çok durum olduğu halde, Swift programcıları genellikle parametrelerini isimlendirmeyi tercih ederler. Şöyle düşünün: Neden fonksiyondaki "String" sözcüğüne ihtiyacımız olsun ki? Biz harfleri saymaktan başka birşey istemiyoruz ki.

O yüzden genellikle harici parametre isimleri olarak "in", "for" ve "ile" ve dahili isimler için de daha anlamlı sözcükler görürüz. Bu fonksiyonun daha Swiftvari versiyonu şu şekilde olacaktır:

```swift
func countLetters(in string: String) {
    print("The string \(string) has \(string.count) letters.")
}
```

Fonksiyonun içerisinde bir anlamı olmayan, ama "in" adlı parametreyle fonksiyonu çağırabileceğin anlamına gelir bu. Zaten fonksiyonun _içerisinde_"string" adıyla aynı parametrereyi çağırmak, daha kullanışlı olacaktır. Dolayısıyla fonksiyon şu şekilde çağırılabilir: 

```swift
countLetters(in: "Hello")
```

İşte _bu_ gerçek bir Swiftvari kod şekli: Doğal İngilizce gibi okunur "count letters in hello" (hello'daki harfleri say) ve kodunuzu daha açık ve öz hale getirir.

## Döndürülen değerler

Swift fonksiyonları, parametre listesinden sonra `->`işareti ve veri tipi yazılarak bir değer döndürebilir. Bunu yaptığınızda, Swift, fonksiyonunuzun her halükarda bir değer döndüreceğini garantiler. İşte bu, kodunuzun yapacağı şey konusunda bir vaatte bulunmaktır.

Örnek olarak, bir albüm adı Taylor Swift'e aitse doğru, başka birine aitse yanlış değerini döndürecek bir fonksiyon yazalım. Fonksiyon bir parametre kabul edecek (kontrol edilecek albüm adı) ve geriye bir Boolean değeri döndürecek. İşte kodumuz:

```swift
func albumIsTaylor(name: String) -> Bool {
    if name == "Taylor Swift" { return true }
    if name == "Fearless" { return true }
    if name == "Speak Now" { return true }
    if name == "Red" { return true }
    if name == "1989" { return true }

    return false
}
```

Eğer yeni öğrendiğiniz `switch/case` ifadesini kullanmak isterseniz, bu fonksiyon uygun bir yer olacaktır.

Albüm adlarını geçerek, fonksiyonu çağırıp sonucu görebilirsiniz:

```swift
if albumIsTaylor(name: "Red") {
    print("That's one of hers!")
} else {
    print("Who made that?!")
}

if albumIsTaylor(name: "Blue") {
    print("That's one of hers!")
} else {
    print("Who made that?!")
}
```

---
# Fonksiyonlar 2 

#swift #yazılım 

Fonksiyonları tanımlayın ve çağırın, bağımsız değişkenlerini etiketleyin ve dönüş değerlerini kullanın.

*Fonksiyonlar*, belirli bir görevi gerçekleştiren bağımsız kod parçalarıdır. Bir fonksiyona ne yaptığını tanımlayan bir ad verirsiniz ve bu ad, gerektiğinde görevini yerine getirmesi için fonksiyonu "*çağırmak*" için kullanılır.

Swift'in birleştirilmiş fonksiyon sözdizimi, parametre adları olmayan basit bir C stili fonksiyondan, her parametre için adlar ve bağımsız değişken etiketleri içeren karmaşık Objective-C stili bir yönteme kadar her şeyi ifade edecek kadar esnektir. Parametreler, fonksiyon çağrılarını basitleştirmek için varsayılan değerler sağlayabilir ve fonksiyon yürütmeyi tamamladıktan sonra iletilen bir değişkeni değiştiren giriş-çıkış parametreleri olarak iletilebilir.

Swift'deki her fonksiyonun, fonksiyonun parametre türleri ve dönüş türünden oluşan bir türü vardır. Bu türü Swift'deki diğer türler gibi kullanabilirsiniz, bu da fonksiyonları diğer fonksiyonlara parametre olarak geçirmeyi ve fonksiyonlardan fonksiyon döndürmeyi kolaylaştırır. Fonksiyonlar, kullanışlı işlevselliği iç içe geçmiş bir fonksiyon kapsamı içinde kapsüllemek için diğer fonksiyonların içinde de yazılabilir.

### [Fonksiyonları Tanımlama ve Çağırma](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Defining-and-Calling-Functions)

Bir fonksiyon tanımladığınızda, isteğe bağlı olarak, fonksiyonun girdi olarak aldığı, parametreler olarak bilinen bir veya daha fazla adlandırılmış, yazılı değer tanımlayabilirsiniz . İsteğe bağlı olarak, fonksiyonun bittiğinde çıktı olarak geri ileteceği, dönüş türü olarak bilinen bir değer türü de tanımlayabilirsiniz .

Her fonksiyonun, fonksiyonun gerçekleştirdiği görevi açıklayan bir fonksiyon adı vardır. Bir fonksiyonu kullanmak için, o fonksiyonu adıyla “çağırırsınız” ve fonksiyonun parametre türleriyle eşleşen girdi değerlerini ( argümanlar olarak bilinir) iletirsiniz. Bir fonksiyonun bağımsız değişkenleri her zaman fonksiyonun parametre listesiyle aynı sırada sağlanmalıdır.

Aşağıdaki örnekteki fonksiyon  `greet(person:)` olarak adlandırılır , çünkü yaptığı budur — girdi olarak bir kişinin adını alır ve o kişi için bir selamlama döndürür. `String` bunu başarmak için, bir giriş parametresi ( adlandırılan bir değer ) ve o kişi için bir selamlama içerecek `person` bir dönüş türü `:String` tanımlarsınız.

Aşağıdaki örnekteki fonksiyona `greet(person:)` denir, çünkü yaptığı şey budur — bir kişinin adını girdi olarak alır ve o kişi için bir selamlama döndürür. Bunu başarmak için, bir giriş parametresi — `person` adı verilen bir `String` değeri — ve o kişi için bir selamlama içerecek bir `String` dönüş türü tanımlarsınız:

```swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}
```

Tüm bu bilgiler, `func` anahtar sözcüğünün öneki olan fonksiyonun (*definition*)/*tanımına* toplanır. Fonksiyonun dönüş türünü *dönüş oku* `->` (kısa çizgi ve ardından dik açılı ayraç) ile belirtirsiniz, ardından döndürülecek türün adı gelir.

Tanım, fonksiyonun ne yaptığını, ne almayı beklediğini ve bittiğinde ne döndürdüğünü açıklar. Tanım, fonksiyonun kodunuzun herhangi bir yerinden açık bir şekilde çağrılmasını kolaylaştırır:

```swift
print(greet(person: "Anna"))
// Prints "Hello, Anna!"
print(greet(person: "Brian"))
// Prints "Hello, Brian!"
```

Fonksiyonu, bağımsız değişken etiketinden sonra greet(person:)bir değer ileterek çağırırsınız , örneğin . Fonksiyon bir değer döndürdüğü için, yukarıda gösterildiği gibi bu dizeyi yazdırmak ve dönüş değerini görmek için fonksiyona yapılan bir çağrıya sarılabilir `.Stringpersongreet(person: "Anna")Stringgreet(person:)`

`Greet(person: "Anna")` gibi `person` bağımsız değişken etiketinden sonra bir `String` değeri geçirerek `great(person:)` fonksiyonunu çağırırsınız. Fonksiyon bir `String` değeri döndürdüğünden, `greet(person:)`, bu dizeyi yazdırmak ve yukarıda gösterildiği gibi dönüş değerini görmek için `print(_:separator:terminator:)` fonksiyonuna yapılan bir çağrıya sarılabilir.

```swift
print(_:separator:terminator:)
```

````ad-warning
title: NOT :

`Print(_:separator:terminator:)` fonksiyonunun hatayı ilk bağımsız değişkeni için bir etiketi yoktur ve diğer bağımsız değişkenleri varsayılan bir değere sahip oldukları için isteğe bağlıdır. Fonksiyon sözdizimindeki bu varyasyonlar aşağıda 
[Function Argument Labels and Parameter Names](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Argument-Labels-and-Parameter-Names) ve [Default Parameter Values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Default-Parameter-Values).
````

Fonksiyonun gövdesi, `greet(person:)` adında yeni bir sabit  tanımlayarak ve onu basit bir karşılama mesajı olarak ayarlayarak başlar. Bu selamlama daha sonra key word kullanılarak fonksiyondan geri geçirilir . Yazan kod satırında , fonksiyon yürütmesini bitirir ve geçerli değerini döndürür .`Stringgreetingreturnreturn greetinggreeting`

greet(person:) Fonksiyonu farklı giriş değerleriyle birden çok kez çağırabilirsiniz . "Anna" Yukarıdaki örnek, bir giriş değeri ve bir giriş değeri ile çağrıldığında ne olacağını gösterir "Brian". Fonksiyon, her durumda özel bir selamlama döndürür.

`greet(person:)` fonksiyonunun gövdesi, `greeting` adı verilen yeni bir `String` sabiti tanımlayarak ve onu basit bir selamlama mesajına ayarlayarak başlar. Bu selamlama daha sonra `return` anahtar sözcüğü kullanılarak fonksiyondan geri aktarılır. `return greeting` yazan kod satırında, fonksiyon yürütülmesini tamamlar ve `greeting` geçerli değerini döndürür.

Bu fonksiyonun gövdesini kısaltmak için mesaj oluşturma ve dönüş ifadesini tek bir satırda birleştirebilirsiniz:
```swift
func greetAgain(person: String) -> String {
	return "Hello again, " + person + "!"
	}
print(greetAgain(person: "Haluk"))
// Prints "Hello again, Haluk!"
```

---

#### [Fonksiyon Parametreleri ve Dönüş Değerleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Parameters-and-Return-Values)

Swift'te fonksiyon parametreleri ve dönüş değerleri son derece esnektir. Tek bir isimsiz parametreye sahip basit bir yardımcı program fonksiyonundan, etkileyici parametre adlarına ve farklı parametre seçeneklerine sahip karmaşık bir fonksiyona kadar her şeyi tanımlayabilirsiniz.

#####  [Parametresiz Fonksiyonlar](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Functions-Without-Parameters)

Giriş parametrelerini tanımlamak için fonksiyonlara gerek yoktur. İşte giriş parametresi olmayan, çağrıldığında her zaman aynı `String` mesajını döndüren bir fonksiyon:
```swift
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// Prints "hello, world"
```

Fonksiyon tanımı, herhangi bir parametre almasa bile, fonksiyon adından sonra parantezlere ihtiyaç duyar. Fonksiyon çağrıldığında fonksiyon adından sonra boş bir parantez çifti gelir. 

---

#### [Çoklu Parametrelere Sahip Fonksiyonlar](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Functions-With-Multiple-Parameters)
 
Fonksiyonlar, fonksiyonun parantezleri içinde virgülle ayrılmış şekilde yazılan birden çok giriş parametresine sahip olabilir.

Bu fonksiyon, bir kişinin adını ve daha önce karşılanıp karşılanmadığını girdi olarak alır ve o kişi için uygun bir karşılama döndürür:

```swift
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))
// Prints "Hello again, Tim!"
```

`Great(person:already Greeted:)` fonksiyonunu, hem `person` etiketli bir `String` bağımsız değişken değerini hem de virgülle ayrılmış parantez içinde `alreadyGreeted` etiketli bir `Bool` bağımsız değişken değerini ileterek çağırırsınız. Bu fonksiyonun önceki bir bölümde gösterilen `greet(person:)` fonksiyonundan farklı olduğunu unutmayın. Her iki fonksiyonun da  `greet` ile başlayan adları olmasına rağmen, `greet(person:alreadyGreeted:)` fonksiyonu iki argüman alır, ancak `greet(person:)` fonksiyonu yalnızca bir argüman alır.

---
### [Dönüş Değerleri Olmayan Fonksiyonlar](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Functions-Without-Return-Values)

Bir dönüş türü tanımlamak için fonksiyonlar gerekli değildir. İşte fonksiyonun , kendi değerini döndürmek yerine `greet(person:)` kendi değerini yazdıran bir  `:String` versiyonu; 
```swift
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")
// Prints "Hello, Dave!"
```

Bir değer döndürmesi gerekmediğinden, fonksiyonun tanımı dönüş okunu ( ->) veya dönüş türünü içermez.
```ad-warning
title: NOT :
`greet(person:)` Açıkça söylemek gerekirse, fonksiyonun bu sürümü, dönüş değeri tanımlanmasa bile yine de bir değer döndürür . Tanımlanmış bir dönüş türü olmayan fonksiyonlar, özel bir tür değeri döndürür Void. Bu sadece olarak yazılan boş bir `tuple()`'dır.
```
Bir fonksiyonun dönüş değeri, çağrıldığında göz ardı edilebilir:
```swift
func printAndCount(string: String) -> Int {
    print(string)
    return string.count
}
func printWithoutCounting(string: String) {
    let _ = printAndCount(string: string)
}
printAndCount(string: "hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting(string: "hello, world")
// prints "hello, world" but doesn't return a value
```

İlk fonksiyon olan `printAndCount (string:)` bir string yazdırır ve ardından karakter sayısını `Int` olarak döndürür. İkinci fonksiyon, `printWithoutCounting(string:)`, ilk fonksiyonu çağırır, ancak dönüş değerini yok sayar. İkinci fonksiyon çağrıldığında, mesaj yine de ilk fonksiyon tarafından yazdırılır, ancak döndürülen değer kullanılmaz.

**<mark style="background: #FFB8EBA6;">Not :</mark>** Dönüş değerleri yok sayılabilir, ancak bir değer döndüreceğini söyleyen bir fonksiyon her zaman bunu yapmalıdır. Tanımlı bir dönüş türüne sahip bir fonksiyon, bir değer döndürmeden kontrolün fonksiyonun altından düşmesine izin veremez ve bunu yapmaya çalışmak derleme zamanı hatasına neden olur.

---

#### [Çoklu Dönüş Değerlerine Sahip Fonksiyonlar](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Functions-with-Multiple-Return-Values)

Bir fonksiyonun tek bir bileşik dönüş değerinin parçası olarak birden çok değer döndürmesi için dönüş türü olarak bir demet türü kullanabilirsiniz.

Aşağıdaki örnek, `Int` değerleri dizisindeki en küçük ve en büyük sayıları bulan `minMax(array:)` adlı bir fonksiyonu tanımlar:
```swift
func min Max(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < current Min {
            current Min = value
        } } else if value > current Max {
            current Max = value
        }
    }
    return (currentMin, currentMax)
}
```

`minMax(array:)` fonksiyonu, iki `Int` değeri içeren bir demet döndürür. Bu değerler, fonksiyonun dönüş değerini sorgularken ada göre erişilebilmeleri için `min` ve `maks` olarak etiketlenir.

`minMax(array:)` fonksiyonunun gövdesi, `currentMin` ve `currentMax` adlı iki çalışma değişkenini dizideki ilk tamsayının değerine ayarlayarak başlar. Fonksiyon daha sonra dizideki kalan değerler üzerinde yinelenir ve sırasıyla `currentMin` ve `currentMax` değerlerinden daha küçük veya daha büyük olup olmadığını görmek için her değeri kontrol eder. Son olarak, toplam minimum ve maksimum değerler iki Int değerinden oluşan bir demet olarak döndürülür.

Grubun üye değerleri, fonksiyonun dönüş türünün bir parçası olarak adlandırıldığından, bulunan minimum ve maksimum değerleri almak için bunlara nokta sözdizimi ile erişilebilir:
```swift
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// Prints "min is -6 and max is 109"
```

Tuple üyelerinin, tuple'ın fonksiyondan döndürüldüğü noktada adlandırılması gerekmediğini unutmayın, çünkü adları zaten fonksiyonun dönüş türünün bir parçası olarak belirtilmiştir.

---
#### [Optional Tuple Dönüş Türleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Optional-Tuple-Return-Types)

Bir fonksiyondam döndürülecek tuple türü, tüm tuple için “no value” olma potansiyeline sahipse, tüm tuple'ın `nil` olabileceği gerçeğini yansıtmak için bir *optional tupl* dönüş türü kullanabilirsiniz. Tuple türünün kapanış parantezinden sonra `(Int, Int)?` veya `(String, Int, Bool)?` gibi bir soru işareti koyarak isteğe bağlı bir demet dönüş türü yazarsınız.

```ad-warning
title: NOT :
icon: pin
`(Int, Int)` ? gibi optional types bir tuple türü, `(Int?, Int?)` gibi optional types türler içeren bir tuple'dan farklıdır. Optional tuple type, yalnızca tuple içindeki her bir değer değil, tüm tuple optional'dır.
```

Yukarıdaki `minMax(array:)` fonksiyonu, iki `Int` değeri içeren bir tuple döndürür. Ancak fonksiyon, iletildiği dizide herhangi bir güvenlik denetimi gerçekleştirmez. `array` bağımsız değişkeni boş bir array içeriyorsa, yukarıda tanımlandığı gibi `minMax(dizi:)` fonksiyonu, `array[0]` erişmeye çalışırken bir çalışma zamanı hatasını tetikler.

Boş bir array safely bir şekilde işlemek için, `minMax(array:)` fonksiyonunu optional bir tuple dönüş türüyle yazın ve tuple boşken  `nil` değerini döndürün:
```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

`minMax(array:)` fonksiyonunun bu sürümünün gerçek bir tuple değeri mi yoksa `nil` m, döndürdüğünü kontrol etmek için  optional binding(bağlayıcı) kullanabilirsiniz:
```swift
if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("min is \(bounds.min) and max is \(bounds.max)")
}
// Prints "min is -6 and max is 109"

```

---
### [Örtük Dönüşlü Fonksiyonlar](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Functions-With-an-Implicit-Return)

Fonksiyonun tüm gövdesi tek bir ifade ise, fonksiyon örtük olarak bu ifadeyi döndürür. Örneğin, aşağıdaki her iki fonksiyon de aynı davranışa sahiptir:
```swift
func greeting(for person: String) -> String {
    "Hello, " + person + "!"
}
print(greeting(for: "Dave"))
// Prints "Hello, Dave!"

func anotherGreeting(for person: String) -> String {
    return "Hello, " + person + "!"
}
print(anotherGreeting(for: "Dave"))
// Prints "Hello, Dave!"

```

- `greeting(for:)` fonksiyonunun tüm tanımı, döndürdüğü karşılama mesajıdır, yani bu daha kısa biçimi kullanabilir.
- `anotherGreeting(for:)` fonksiyonu, daha uzun bir fonksiyon gibi `return` anahtar sözcüğünü kullanarak aynı karşılama iletisini döndürür. Yalnızca bir `return` satırı olarak yazdığınız herhangi bir fonksiyon, dönüşü atlayabilir.

[Shorthand Getter Beyanında](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Shorthand-Getter-Declaration) 'da göreceğiniz gibi, mülk alıcıları aynı zamanda örtük bir getiri de kullanabilir.


```ad-warning
title: NOT :
icon: pin

Örtük bir dönüş değeri olarak yazdığınız kodun bir değer döndürmesi gerekir. Örneğin, örtülü bir dönüş değeri olarak `print(13)` kullanamazsınız. Ancak, asla `fatalError("Oh no!")` örtük bir dönüş değeri olarak, çünkü Swift örtük dönüşün gerçekleşmediğini bilir.

```
---
### [Fonksiyon Argüman Etiketleri ve Parametre Adları](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Argument-Labels-and-Parameter-Names)

Her fonksiyon parametresinin hem bir *argüman etiketi* hem de bir *parametre adı* vardır. Bağımsız değişken etiketi, fonksiyonu çağırırken kullanılır; her argüman, fonksiyon çağrısına, ondan önce bağımsız değişken etiketiyle yazılır. Parametre adı fonksiyonun uygulanmasında kullanılır. Varsayılan olarak, parametreler argüman etiketi olarak parametre adlarını kullanır.

```swift
func someFunction(first Parameter Name: Int, second Parameter Name: Int) {
    // İşlev gövdesinde, first Parameter Name ve second Parameter Name
    // bfirst and second parameter'lerin bağımsız değişken değerlerine bakın.
}
some Function(first Parameter Name: 1, second Parameter Name: 2)
```

Tüm parametrelerin benzersiz isimleri olmalıdır. Birden fazla parametrenin aynı argüman etiketine sahip olması mümkün olsa da, benzersiz bağımsız değişken etiketleri kodunuzu daha okunabilir hale getirmeye yardımcı olur.

----
### [Bağımsız Değişken Etiketlerini Belirleme](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Specifying-Argument-Labels)

Parametre adından önce bir boşlukla ayrılmış bir bağımsız değişken etiketi yazarsınız:
```swift
func someFunction(argument Label parameterName: Int) {
// Fonksiyon gövdesinde parameterName, o parametrenin bağımsız değişken değerini ifade eder.
}
```

İşte bir kişinin adını ve memleketini alan ve bir selamlama döndüren `greet(person:)` fonksiyonunun bir varyasyonu:
```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}
print(great(person: "Bill", from: "Cupertino"))
// Prints "Hello Bill!  Glad you could visit from Cupertino."

```

Argüman etiketlerinin kullanılması, bir fonksiyonun etkileyici, cümle benzeri bir şekilde çağrılmasına izin verirken, yine de amaç olarak okunabilir ve net bir fonksiyon gövdesi sağlayabilir.

---
### [Bağımsız Değişken Etiketlerini Atlamak](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Omitting-Argument-Labels)

Bir parametre için bağımsız değişken etiketi istemiyorsanız, bu parametre için açık bir bağımsız değişken etiketi yerine bir alt çizgi/underscore (`_`) yazın.
```swift
func someFunction(_ first Parameter Name: Int, second Parameter Name: Int) {
	// İşlev gövdesinde, firstParameterName ve secondParameterName, first ve second parametrelerin bağımsız değişken değerlerine başvurur.
}
some Function(1, second Parameter Name: 2)
```

Bir parametrenin bağımsız değişken etiketi varsa, fonksiyonu çağırdığınızda argümanın etiketlenmesi *gerekir*.

---
### [Varsayılan Parametre Değerleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Default-Parameter-Values)

Bu parametrenin türünden sonra parametreye bir değer atayarak bir fonksiyondaki herhangi bir parametre için *varsayılan* bir *değer* tanımlayabilirsiniz. Varsayılan bir değer tanımlanırsa, fonksiyonu çağırırken bu parametreyi atlayabilirsiniz.

```swift
func someFunction(parameter Without Default: Int, parameter With Default: Int = 12) {
	// Bu fonksiyonu çağırırken ikinci bağımsız değişkeni atlarsanız, fonksiyon gövdesi içindeki parameterWithDefault değeri 12'dir.
}
some Function(parameter Without Default: 3, parameter With Default: 6) // varsayılan parametre 6'dır
some Function(parameter Without Default: 4) // varsayılan parametre 12'dir
```

Varsayılan değerleri olmayan parametreleri, bir fonksiyonun parametre listesinin başına, varsayılan değerleri olan parametrelerin önüne yerleştirin. Varsayılan değerlere sahip olmayan parametreler genellikle fonksiyonun anlamı için daha önemlidir — önce bunları yazmak, herhangi bir varsayılan parametrenin atlanıp atlanmadığına bakılmaksızın aynı fonksiyonun çağrıldığını tanımayı kolaylaştırır.

---
### [Değişken Parametreler](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Variadic-Parameters)

*Değişken* bir *parametre,* belirli bir türde sıfır veya daha fazla değeri kabul eder. Fonksiyon çağrıldığında parametrenin değişen sayıda giriş değeri iletilebileceğini belirtmek için değişken bir parametre kullanırsınız. Parametrenin tür adından sonra üç nokta karakteri `(...)` ekleyerek değişken parametreler yazın.

Değişken bir parametreye geçirilen değerler, fonksiyonun gövdesinde uygun türde bir array olarak kullanılabilir hale getirilir. Örneğin, ``numbers``  ve type'ı `Double...` olan değişken bir parametre, fonksiyonun gövdesi içinde `[Double]` türünde `numbers` adı verilen sabit/constant bir array olarak kullanılabilir hale getirilir.

Aşağıdaki örnek, herhangi bir uzunluktaki sayıların bir listesi için *aritmetik ortalamayı* (*ortalama* olarak da bilinir) hesaplar:

Bu Swift fonksiyonu, değişen sayıda bağımsız değişkenleri olan bir ortalama hesaplama fonksiyonu gerçekleştirir. Fonksiyonun imzası şu şekildedir:
```swift
func arithmetic Mean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmetic Mean(1, 2, 3, 4, 5)
// bu beş sayının aritmetik ortalaması olan 3.0'ı döndürür
arithmetic Mean(3, 8.25, 18.75)
// bu üç sayının aritmetik ortalaması olan 10.0'ı döndürür

```

Burada, `_ numbers` ifadesi, fonksiyonun alacağı değişen sayıda (0'dan fazla) `Double` türünden bağımsız değişkenleri temsil eder.

Fonksiyon, aldığı tüm sayıları toplamak için bir döngü kullanır ve toplamı `total` adlı bir değişkende saklar. Daha sonra, `numbers` dizisinin eleman sayısına bölerek sayıların aritmetik ortalamasını hesaplar ve bu değeri geri döndürür.

`arithmeticMean(1, 2, 3, 4, 5)

Fonksiyona 5 sayıyı argüman olarak geçirir ve sonuç olarak 3.0 (1+2+3+4+5=15, 15/5=3) değerini döndürür.

Benzer şekilde, şu kod örneği:

`arithmeticMean(3, 8.25, 18.75)`

Bir fonksiyon birden fazla değişken parametreye sahip olabilir. Değişken bir parametreden sonra gelen ilk parametrenin bir argüman etiketi olmalıdır. Argüman etiketi, hangi argümanların değişken parametreye geçirildiğini ve hangi argümanların değişken parametreden sonra gelen parametrelere geçirildiğini açık hale getirir.

---
### [Giriş-Çıkış Parametreleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#In-Out-Parameters)

Swift dilinde <mark style="background: #D2B3FFA6;">in-out parameters</mark> (içeri-dışarı parametreleri), bir fonksiyona argüman olarak geçirilen değerlerin fonksiyon içinde değiştirilip dışarıda kullanılabilmesini sağlar.

Bir fonksiyon, içeri-dışarı parametrelerle çağrıldığında, parametreler `in-out` olarak belirtilir. Bu tür bir parametre, `"&"` işaretiyle öne eklenerek tanımlanır. Örneğin:
```swift
func swapInts(_ a: inout Int, _ b: inout Int) {
    let temp = a
    a = b
    b = temp
}
```

Bu fonksiyon, "a" ve "b" adlı iki tamsayı içeri-dışarı parametreleri alır ve bunları birbirleriyle değiştirir. Fonksiyon, "temp" adlı geçici bir değişken kullanarak "a" ve "b" değerlerini değiştirir.

Bu fonksiyonu kullanmak için, bir fonksiyon çağrısı yapılırken, "&" işaretiyle öne eklenerek "a" ve "b" parametreleri işaret edilir:
```swift
var x = 10
var y = 20
swapInts(&x, &y)
print("x: \(x), y: \(y)") // prints "x: 20, y: 10"
```

Bu örnekte, `x` ve y adlı iki değişken, "swapInts" fonksiyonuna argüman olarak geçilir. Fonksiyon, `x` ve `y` değişkenlerinin değerlerini değiştirir, bu nedenle sonuç olarak `x` 20 ve `y` 10 olarak yazdırılır.

İçeri-dışarı parametreleri kullanmak, özellikle büyük veri yapıları veya nesnelerle çalışırken, daha verimli bir programlama yöntemi olabilir. Bununla birlikte, içeri-dışarı parametrelerin kullanımı, fonksiyonların doğrudan etkilemesi gereken veriler üzerinde kontrollü bir şekilde çalışmak için biraz daha fazla dikkat gerektirebilir.

Fonksiyon parametreleri varsayılan olarak sabittir. Bir fonksiyon parametresinin değerini o fonksiyonun gövdesinden değiştirmeye çalışmak, bir derleme zamanı hatasına neden olur. Bu, bir parametrenin değerini yanlışlıkla değiştiremeyeceğiniz anlamına gelir. Bir fonksiyonun, bir parametrenin değerini değiştirmesini istiyorsanız ve fonksiyon çağrısı sona erdikten sonra bu değişikliklerin devam etmesini istiyorsanız, bunun yerine bu parametreyi bir *in-out parametresi* olarak tanımlayın.

`Inout` anahtar sözcüğünü bir parametrenin türünden hemen önce yerleştirerek bir in-out parametresi yazarsınız. Bir ın-out parametresi, fonksiyona *in* geçirilen, fonksiyon tarafından değiştirilen ve orijinal değeri değiştirmek için fonksiyondan *out* geri geçirilen bir değere sahiptir. Çıkış parametrelerinin davranışı ve ilişkili derleyici optimizasyonları hakkında ayrıntılı bir tartışma için bkz. [Çıkış Parameters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations#In-Out-Parameters).

Bir değişkeni yalnızca bir in-out parametresi için argüman olarak geçirebilirsiniz. Argüman olarak bir sabit veya değişmez bir değer geçiremezsiniz, çünkü sabitler ve değişmezler değiştirilemez. Fonksiyon tarafından değiştirilebileceğini belirtmek için bir in-out parametresine argüman olarak ilettiğinizde, bir değişkenin adının hemen önüne bir ampersand (`&`) yerleştirirsiniz.


```ad-warning
title: NOT :
icon: pin

In-out parametreleri varsayılan değerlere sahip olamaz ve değişken parametreler `inout` olarak işaretlenemez.
```

İşte `a` ve `b` olarak adlandırılan iki  in-out tamsayı parametresine sahip `swapTwoInts(_:_:)` adlı bir fonksiyona bir örnek:
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporary
}
```

`swapTwoİnts(_:_:)` fonksiyonu, `b`'nin değerini `a`'ya ve `a`'nın değerini `b`'ye değiştirir. Fonksiyon, `a`'nın değerini geçici olarak adlandırılan geçici bir sabitte depolayarak, `b`'nin değerini `a`'ya atayarak ve ardından geçici değeri `b`'ye atayarak bu takası gerçekleştirir.

Değerlerini değiştirmek için `Int` türünde iki değişkenle `swapTwoInts(_:_:)` fonksiyonunu çağırabilirsiniz. `swapTwoInts(_:_:)` fonksiyonuna iletildiklerinde `someInt` ve `anotherInt` adlarının bir ve işareti ile öneklendiğini unutmayın:
```swift
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// Prints "someInt şimdi 107 ve anotherInt şimdi 3"
```

Yukarıdaki örnek, `someInt` ve `anotherInt` orijinal değerlerinin, orijinal olarak fonksiyonun dışında tanımlanmış olsalar bile `swapTwoInts(_:_:)` fonksiyonu tarafından değiştirildiğini göstermektedir.


```ad-warning
title: NOT :
icon: pin

In-ou parametreleri, bir fonksiyondan bir değer döndürmekle aynı şey değildir. Yukarıdaki `swapTwoInts` örneği bir dönüş türü tanımlamaz veya bir değer döndürmez, ancak yine de `someInt` ve `anotherInt' değerlerini değiştirir. In-out parametreleri, bir fonksiyonun fonksiyon gövdesinin kapsamı dışında bir etkiye sahip olmasının alternatif bir yoludur.
```

---
## [İşlev Türleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Types)

Her fonksiyonun, parametre türlerinden ve fonksiyonun dönüş türünden oluşan belirli bir *fonksiyon türü* vardır.

Örneğin:
```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}
func multiplyTwoInt(_ a: Int, _ b: Int) -> Int {
    return a * b
}
print(addTwoInts(2, 3))       // 5
print(multiplyTwoInt(2, 3))   // 6
```

Bu örnek, `addTwoInts` ve `multiplyTwoInts` adı verilen iki basit matematiksel fonksiyonu tanımlar. Bu fonksiyonların her biri iki `Int` değeri alır ve uygun bir matematiksel işlemin gerçekleştirilmesinin sonucu olan bir `Int` değeri döndürür.

Bu fonksiyonların her ikisinin de türü `(Int, Int) -> Int`. Bu şu şekilde okunabilir:
```ad-hint
title: 
Her ikisi de `Int` türünde iki parametreye sahip olan ve `Int` türünde bir değer döndüren bir fonksiyon.
```

`addTwoInts(_:_:)`  fonksiyonu, `mathFunction` değişkeniyle aynı türe sahiptir ve bu nedenle bu atamaya Swift'in tür denetleyicisi tarafından izin verilir.

Artık atanan fonksiyonu `mathFunction` adıyla çağırabilirsiniz`:
```swift
 print("Result: \(mathFunction(2, 3))") 
 // Prints "Result: 5"
```

Aynı eşleşen türe sahip farklı bir fonksiyon, aynı değişkene, fonksiyonsuz türlerde olduğu gibi atanabilir:
```swift
 mathFunction = multiplyTwoInts 
 print("Result: \(mathFunction(2, 3))") 
 // Prints "Result: 6"
```

Diğer herhangi bir türde olduğu gibi, bir sabite veya değişkene bir fonksiyon atadığınızda fonksiyon türünü çıkarmak için Swift'e bırakabilirsiniz:
```swift
 let anotherMathFunction = addTwoInts 
 // anotherMathFunction türünde olduğu sonucuna varılır (Int, Int) -> Int
```

---
### [Parametre Türleri Olarak Fonksiyon Türleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Types-as-Parameter-Types)

`(Int, Int) -> Int` gibi bir fonksiyon tipini başka bir fonksiyon için parametre tipi olarak kullanabilirsiniz. Bu, bir fonksiyonun uygulamasının bazı yönlerini, fonksiyon çağrıldığında sağlaması için fonksiyon arayan kişiye bırakmanıza olanak tanır.

İşte matematik fonksiyonlarının sonuçlarını yukarıdan yazdırmak için bir örnek
```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
	return a + b
}

func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
	print("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)
```

Bu örnek, üç parametresi olan  `printMathResult(_:_:_:)` adlı bir fonksiyonu tanımlar. İlk parametre `mathFunction` olarak adlandırılır ve `(Int, Int) -> Int` türündedir. Bu türdeki herhangi bir fonksiyonu bu ilk parametre için bağımsız değişken olarak iletebilirsiniz. İkinci ve üçüncü parametreler `a` ve `b` olarak adlandırılır ve her ikisi de `Int` türündedir. Bunlar, sağlanan matematik fonksiyonu için iki giriş değeri olarak kullanılır.

`printMathResult(_:_:_:)` çağrıldığında,  `addTwoInts(_:_:)` fonksiyonu ve `3` ve `5` tamsayı değerleri iletilir. Sağlanan fonksiyonu `3` ve `5` değerleriyle çağırır ve `8` sonucunu yazdırır.
```ad-hint
title: 
`printMathResult(_:_:_:)` fonksiyonu, uygun türde bir matematik fonksiyonuna yapılan çağrının sonucunu yazdırmaktır. Bu fonksiyonun uygulamasının gerçekte ne yaptığı önemli değil - yalnızca fonksiyonun doğru türde olması önemlidir. Bu, `printMathResult(_:_:_:)` fonksiyonunun bir kısmını fonksiyonun çağıranına tür açısından güvenli bir şekilde devretmesini sağlar.
```

---
### [Dönüş Türleri Olarak Fonksiyon Türleri](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Types-as-Return-Types)

Başka bir fonksiyonun dönüş türü olarak bir fonksiyon türü kullanabilirsiniz. Bunu, dönen fonksiyonun dönüş okundan (`->`) hemen sonra tam bir fonksiyon türü yazarak yaparsınız.

Bir sonraki örnek, `stepForward(_:)` ve `stepBackward(_:)` olarak adlandırılan iki basit fonksiyonu tanımlar. `stepForward(_:)`  fonksiyonu, input değerinden bir değer daha döndürür ve `stepBackward(_:)` fonksiyonu, input değerinden bir değer daha az döndürür. Her iki fonksiyonun da bir türü vardır `(Int) -> Int`:
```swift
func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}
```

İşte dönüş türü `(Int) -> Int` olan `chooseStepFunction(backward:)` adlı bir fonksiyon. `chooseStepFunction(backward:)` fonksiyonu, `stepForward(_:)`  adlı bir Boole parametresine dayalı olarak `stepForward(_:)` fonksiyonunu veya `stepBackward(_:)` fonksiyonunu döndürür:
```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int { 
	return backward ? stepBackward : stepForwar
}
```

Artık bir yöne veya diğerine adım atacak bir fonksiyon elde etmek için `chooseStepFunction(backward:)` fonksiyonunu kullanabilirsiniz:
```swift
var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero now refers to the stepBackward() function
```

Yukarıdaki örnek, `currentValue` adlı bir değişkeni aşamalı olarak sıfıra yaklaştırmak için pozitif veya negatif bir adımın gerekli olup olmadığını belirler. `currentValue` `3` başlangıç değerine sahiptir, yani `currentValue> 0` `true` değerini döndürür ve `chooseStepFunction(backward:)` fonksiyonunun `stepBackward(_:)` fonksiyonunu döndürmesine neden olur. Döndürülen fonksiyona yapılan bir başvuru, `moveNearerToZero` adlı bir sabitte saklanır.

Artık `moveNearerToZero` doğru fonksiyona atıfta bulunduğuna göre, sıfıra saymak için kullanılabilir:
```swift
print("Counting to zero:")
// Counting to zero:
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// 3...
// 2...
// 1...
// zero!
```

---
## [İç İçe Fonksiyonlar](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Nested-Functions)

Bu bölümde şimdiye kadar karşılaştığınız tüm fonkasiyonlar, küresel kapsamda tanımlanan *genel fonksiyonlara* örnek olmuştur. *İç içe fonksiyonlar* olarak bilinen diğer fonksiyonların gövdelerinin içindeki fonksiyonları da tanımlayabilirsiniz.

İç içe geçmiş fonksiyonlar varsayılan olarak dış dünyadan gizlenir, ancak yine de çevreleyen fonksiyonları tarafından çağrılabilir ve kullanılabilir. Bir çevreleyen fonksiyon, iç içe geçmiş fonksiyonun başka bir kapsamda kullanılmasına izin vermek için iç içe geçmiş fonksiyonlardan birini de döndürebilir.

İç içe geçmiş fonksiyonları kullanmak ve döndürmek için yukarıdaki `chooseStepFunction(backward:)` örneğini yeniden yazabilirsiniz:


```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// // moveNearerToZero şimdi iç içe geçmiş stepForward()) fonksiyonunu ifade ediyor
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```

----
🔚   🔚   🔚   🔚   🔚   🔚 🔚    🔚   🔚   🔚   🔚   🔚   🔚   🔚   🔚   🔚   🔚   🔚   🔚   🔚    🔚   🔚   🔚   🔚  🔚

---
# Fonksiyonlarla kod nasıl yeniden kullanılır ? 

Gerçekten beğendiğiniz bir kod yazdığınızda ve tekrar tekrar kullanmak istediğinizde, onu bir _function_içine koymayı düşünmelisiniz . İşlevler, programınızın geri kalanından ayırdığınız ve onlara kolayca başvurabilmeniz için bir ad verdiğiniz kod parçalarıdır.

Örneğin, bu güzel ve basit kodumuz olduğunu varsayalım:

```swift
print("Welcome to my app!")
print("By default This prints out a conversion")
print("chart from centimeters to inches, but you")
print("can also set a custom range if you want.")
```

Bu, bir uygulama için hoş geldiniz mesajıdır ve uygulama başlatıldığında veya belki de kullanıcı yardım istediğinde yazdırılmasını isteyebilirsiniz.

_Ama ya her iki_ yerde de olmasını istersen ? Evet, bu dört satırı kopyalayıp her iki yere de koyabilirsiniz , ama ya bu metni _on_`print()` yerde istiyorsanız ? Ya da daha sonra ifadeyi değiştirmek isteseydiniz - kodunuzda göründüğü her yerde değiştirmeyi gerçekten hatırlar mıydınız?

Fonksiyonların devreye girdiği yer burasıdır: bu kodu çıkarabilir, ona bir isim verebilir ve ihtiyaç duyduğumuz her an ve her yerde çalıştırabiliriz. Bu, tüm `print()`hatların tek bir yerde kalması ve başka bir yerde yeniden kullanılması anlamına gelir.

İşte böyle görünüyor:

```swift
func showWelcome() {
    print("Welcome to my app!")
    print("By default This prints out a conversion")
    print("chart from centimeters to inches, but you")
    print("can also set a custom range if you want.")
}
```

Bunu parçalayalım…

1.  `func`Bir fonksiyonun başlangıcını işaret eden anahtar kelime ile başlar .
2.  Fonksiyonu adlandırıyoruz `showWelcome`. Bu, istediğiniz herhangi bir isim olabilir, ancak onu akılda kalıcı kılmaya çalışın –  `printInstructions()`, `displayHelp()`, vb. Hepsi iyi seçimlerdir.
3.  Fonksiyonun gövdesi, tıpkı döngülerin gövdesi ve koşulların gövdesi gibi, açık ve kapalı parantezlerin içinde yer alır.

`()`Orada fazladan bir şey daha var ve bunu şu ana kadarki çalışmalarımızdan hatırlayabilirsiniz: `showWelcome`. `count`İlk kez bu şekilde dizelere baktığımızda, ondan sonrası yok dediğimde tanıştık `()`ama `uppercased()`var.

Pekala, şimdi nedenini öğreniyorsunuz: bunlar `()`işlevlerle kullanılır. Yukarıda görebileceğiniz gibi, işlevi oluşturduğunuzda ve aynı zamanda işlevi _çağırdığınızda_ - Swift'den kodunu çalıştırmasını istediğinizde kullanılırlar. Bizim durumumuzda, fonksiyonumuzu şu şekilde çağırabiliriz:

```swift
showWelcome()
```

Bu , "işlevin çağrıldığı yer" anlamına gelen süslü bir ad olan işlevin _çağrı sitesi olarak bilinir._

Peki parantezler _aslında ne yapıyor_ ? Burası, fonksiyonlarımız için konfigürasyon seçeneklerini eklediğimiz yer - fonksiyonun çalışma şeklini özelleştiren verileri iletiyoruz, böylece fonksiyon daha esnek hale geliyor.

Örnek olarak, zaten böyle bir kod kullandık:

```swift
let number = 139

if number.isMultiple(of: 2) {
    print("Even")
} else {
    print("Odd")
}
```

`isMultiple(of:)`tamsayılara ait bir fonksiyondur. Herhangi bir özelleştirmeye izin vermeseydi, mantıklı olmazdı - _neyin_ katı mı ? Elbette, Apple bunu şunun gibi bir şey yapabilirdi `isOdd()`ya da `isEven()`bu yüzden hiçbir zaman yapılandırma seçeneklerine sahip olmaya gerek duymadı, ancak aniden yazabilmek `(of: 2)`işlev daha güçlü hale geliyor çünkü artık 2, 3, 4, 5, 50'nin katlarını kontrol edebiliyoruz. , veya başka herhangi bir numara.

Benzer şekilde, daha önce sanal zar atarken şöyle bir kod kullandık:

```swift
let roll = Int.random(in: 1...20)
```

Yine, `random()`bir fonksiyondur ve `(in: 1...20)`kısım yapılandırma seçeneklerini işaretler – bu olmadan rastgele sayılarımızın aralığı üzerinde hiçbir kontrolümüz olmazdı, bu da çok daha az kullanışlı olurdu.

Fonksiyonumuzu oluştururken parantezlerin arasına ekstra kod koyarak konfigürasyona açık kendi fonksiyonlarımızı yapabiliriz. Buna 8 gibi tek bir tamsayı verilmeli ve bunun için 1'den 12'ye kadar olan çarpım tabloları hesaplanmalıdır.

İşte kodda şu:

```swift
func printTimesTables(number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(number: 5)
```

`number: Int`Parantezlerin içine nasıl yerleştirdiğime dikkat ettiniz mi ? _Buna parametre_ denir ve bu bizim özelleştirme noktamızdır. _Bu işlevi kim çağırırsa buraya bir tamsayı girmesi gerektiğini_ ve Swift'in bunu uygulayacağını söylüyoruz . İşlevin içinde, `number`diğer sabitler gibi kullanılabilir, bu nedenle çağrının içinde görünür `print()`.

Gördüğünüz gibi, çağrıldığında `printTimesTables()`açıkça yazmamız gerekiyor `number: 5`– işlev çağrısının bir parçası olarak parametre adını yazmamız gerekiyor. Bu, diğer dillerde yaygın değildir, ancak her parametrenin ne yaptığını hatırlatması açısından Swift'te gerçekten yararlı olduğunu düşünüyorum.

_Birden çok_ parametreniz olduğunda, parametrelerin bu şekilde adlandırılması daha da önemli hale gelir . Örneğin, çarpım tablolarımızın ne kadar yüksek olduğunu özelleştirmek istersek, aşağıdaki gibi ikinci bir parametre kullanarak aralığımızın sonunu ayarlayabiliriz:

```swift
func printTimesTables(number: Int, end: Int) {
    for i in 1...end {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(number: 5, end: 20)
```

Şimdi bu _iki_ parametre alır: adlı bir tamsayı `number`ve adı verilen bir bitiş noktası `end`. Çalıştırıldığında bunların her ikisinin de özel olarak adlandırılması gerekir `printTablesTable()`ve umarım şimdi neden önemli olduklarını anlayabilirsiniz - kodumuzun bunun yerine şöyle olup olmadığını hayal edin:

```swift
printTimesTables(5, 20)
```

Hangi sayının hangisi olduğunu hatırlayabiliyor musunuz? Belki. Ama bundan altı ay sonrasını hatırlar mısın? Muhtemelen değil.

_Şimdi, teknik olarak veri göndermek_ ve veri _almak_ için biraz farklı isimler veriyoruz ve birçok kişi (ben dahil) bu ayrımı görmezden gelse de, daha sonra hazırlıksız yakalanmamanız için en azından sizi haberdar edeceğim.

Bu koda bir göz atın:

```swift
func printTimesTables(number: Int, end: Int) {
```

Her ikisi de vardır `number`ve _parametreler_ : bunlar, işlev çağrıldığında değerlerle doldurulacak yer tutucu adlardır, böylece işlev içinde bu değerler için bir adımız olur.`end`

Şimdi şu koda bakın:

```swift
printTimesTables(number: 5, end: 20)
```

5 ve 20 bağımsız değişkenlerdir _:_ bunlar, çalışmak için işleve gönderilen, doldurmak için kullanılan gerçek değerlerdir `number`ve `end`.

_Yani, hem parametrelerimiz_ hem de _bağımsız değişkenlerimiz_ var : biri _yer tutucu_ , diğeri _gerçek değer_ , yani hangisinin hangisi olduğunu unutursanız, Parametre/Yer Tutucu, Bağımsız Değişken/Gerçek Değer'i hatırlayın.

Bu isim ayrımı önemli mi? Pek değil: Her ikisi için de "parametre" kullanıyorum ve her ikisi için de "argüman" kullanan başka insanlar tanıdım ve dürüst olmak gerekirse, kariyerimde bir kez bile en ufak bir soruna neden olmadı. Aslında, birazdan Swift'te göreceğiniz gibi, ayrım _fazladan_ kafa karıştırıcı, bu yüzden üzerinde düşünmeye değmez.

**Önemli:** Girilen veriler için "argüman" ve alınan veriler için "parametre" kullanmayı tercih ederseniz, bu size kalmış, ancak ben gerçekten her ikisi için de "parametre" kullanıyorum ve bu kitap boyunca ve sonrasında da öyle yapacağım. .

Onlara "bağımsız değişkenler" veya "parametreler" demenizden bağımsız olarak, Swift'ten işlevi çağırmasını istediğinizde, parametreleri her zaman işlevi oluşturduğunuzda listelendikleri sırayla iletmelisiniz.

Yani, bu kod için:

```swift
func printTimesTables(number: Int, end: Int) {
```

Bu geçerli bir kod _değil_ , çünkü şunun `end`önüne koyuyor `number`:

```swift
printTimesTables(end: 20, number: 5)
```

**İpucu:** Bir işlev içinde oluşturduğunuz tüm veriler, işlev bittiğinde otomatik olarak yok edilir.