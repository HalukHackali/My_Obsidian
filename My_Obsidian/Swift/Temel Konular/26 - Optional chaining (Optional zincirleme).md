#swift #yazılım 

Optional'larla çalışırken kendimizi biraz acemi hissederiz bazen ve açmalar (unwrapping), kontrol etmeler o kadar büyük bir yük haline gelir ki, çalışmaya devam edebilmek için birkaç tane ünlem işareti fırlatmak gelir içimizden. Siz yine de dikkatli olun: Eğer bir değer içermeyen bir optional'ı açmaya zorlarsanız, yazdığınız kod çöker.

Swift dili, kodunuzdaki karmaşayı azaltmaya yardım etmek için iki tekniğe sahiptir. İlkinin adı, sadece optional'ınızın bir değeri varsa kodunuzun çalışmasına izin veren Optional Chaining'tir. Alttaki kodu oyun alanınıza girin ve başlayalım:

```swift
func albumReleased(year: Int) -> String? {
    switch year {
    case 2006: return "Taylor Swift"
    case 2008: return "Fearless"
    case 2010: return "Speak Now"
    case 2012: return "Red"
    case 2014: return "1989"
    default: return nil
    }
}

let album = albumReleased(year: 2006)
print("The album is \(album)")
```

Bu kod sonuç paneline "The album is Optional("Taylor Swift")" yazdıracaktır.

Eğer `albumReleased()` fonksiyonunun döndürdüğü değeri büyük harf olarak ("Taylor Swift" yerine "TAYLOR SWIFT") değiştirmek isteseydik, bu String'in `uppercased()` metodunu çağırırdık. Örneğin:

```swift
let str = "Hello world"
print(str.uppercased())
```

Sorun ise, `albumReleased()` fonksiyonunun optional bir String döndürmesidir: Bir String döndürebilir de, hiçbir şey döndürmeyebilir de. Söylemek istediğimiz şey şu: "Eğer bir String dönüyorsa büyük harflere dönüştür, aksi taktirde birşey yapma." İşte burada söze optional chaining giriyor, çünkü kendisi tam da bu şekilde davranıyor.

Kodunuzun son iki satırını, aşağıdaki gibi değiştirmeyi deneyin:

```swift
let album = albumReleased(year: 2006)?.uppercased()
print("The album is \(album)")
```

Optional chaining yapan soru işaretine dikkat edin: Bu soru işaretinden sonra gelen her şey çalışacak, ama tabi soru işaretinden öncekiler bir değer içeriyorsa. Bu, `album` değişkeninin veri tipini etkilemez, çünkü bu kod satırı ya nil değerini döndürecek, ya da albümün adının büyük harfli versiyonunu; sonuçta hala optional bir String.

Optional chaining istediğiniz kadar uzun olabilir. Örneğin:

```swift
let album = albumReleased(year: 2006)?.someOptionalValue?.someOtherOptionalValue?.whatever
```

Swift, bir noktada duracağı nil değerini bulana kadar soldan sağa hepsini kontrol eder.

## nil değeri birleştirme operatörü (nil coalescing operator)

Swift'in bu özelliği basit görünmesine rağmen, kodunuzu daha basit ve daha güvenli hale getirir. Bakmayın siz birçok insanı korkutan görkemli ismine. Bu bir ayıptır, çünkü ne olduğunu anlamak için zaman ayırırsanız, nil değeri birleştirme operatörünün hayatınızı ne kadar çok kolaylaştıracağını göreceksiniz!

Yaptığı şey hakkında şöyle söyleyebiliriz: "Mümkünse A değerini kullan, ama A değeri nil ise, o zaman B değerini kullan." Bu kadar işte. Özellikle optional'larla birlikte çok kullanışlıdır, çünkü non-optional (seçimli olmayan) B değerini verdiğiniz için, onları optional olmaktan etkili bir şekilde kurtarır. Yani, eğer A bir optional ise ve bir değere sahipse, onu kullanacaktır (çünkü bir değerimiz var). Ama eğer A kendisi varken ama bir değere sahip değilse, B kullanılacaktır (hala bir değere sahibiz). Her halükarda, kesinlikle bir değere sahibiz.

Daha gerçekçi bir durum vermek için, aşağıdaki kodu oyun alanınızda deneyin:

```swift
let album = albumReleased(year: 2006) ?? "unknown"
print("The album is \(album)")
```

Bu bir çift soru işareti, nil birleştirme operatörüdür ve buradaki anlamı "`albumReleased()`fonksiyonu bir değer döndürürse, onu `album`değişkenine yerleştir. Ama eğer `albumReleased()` fonksiyonu herhangi bir değer döndürmezse, dönen nil değeri yerine 'unknown' (bilinmeyen) değerini kullan."

Eğer şimdi sonuç paneline bakarsanız, "The album is Taylor Swift" yazdığını göreceksiniz; artık Optional ifadesi yok. Bu şekilde yazdırmasının sebebi, Swift'in artık fonksiyonun döndüreceği ister bir değer olsun, isterse 'unknown' olsun, gerçek bir şey alabileceğinden emin olmasıdır. Bunun anlamı, herhangi bir şeyi açmanıza gerek olmadığı, dolayısıyla da çökme riskinin olmadığıdır. Kodunuzu daha güvenli ve çalışması daha kolay bir hale getiren gerçek bir veriye sahip olduğunuz artık kesin.

---

# Opsiyonel seçeneklerle eksik veriler nasıl işlenir?

Swift öngörülebilir olmayı sever, bu da bizi mümkün olduğunca güvenli ve beklediğimiz gibi çalışacak kodlar yazmaya teşvik eder. Fırlatma işlevleriyle zaten tanıştınız, ancak Swift'in öngörülebilirliği sağlamanın başka bir önemli yolu var _-_ "bu şeyin bir değeri olabilir veya olmayabilir" anlamına gelen bir sözcük - isteğe bağlılar.

İsteğe bağlı seçenekleri iş başında görmek için aşağıdaki kodu düşünün:

```swift
let opposites = [
    "Mario": "Wario",
    "Luigi": "Waluigi"
]

let peachOpposite = opposites["Peach"]
```

`[String: String]`Orada iki tuşlu bir sözlük oluşturuyoruz : Mario ve Luigi. Daha sonra "Şeftali" anahtarına iliştirilmiş, var olmayan değeri okumaya çalışırız ve eksik verilerin yerine geri göndermek için varsayılan bir değer sağlamadık _._

`peachOpposite`Bu kod çalıştıktan sonra ne olacak? Bu bir `[String: String]`sözlük, yani anahtarlar dizgiler ve değerler dizgeler, ama biz sadece var olmayan bir anahtarı okumaya çalıştık - orada bir değer yoksa bir dizgeyi geri almanın bir anlamı olmaz .

Swift'in çözümü , mevcut olabilecek veya olmayabilecek veriler anlamına gelen _options opsiyonel olarak adlandırılır._ Öncelikle veri türünüzden sonra bir soru işareti koyarak temsil edilirler, bu nedenle bu durumda a yerine a `peachOpposite`olur .`String?``String`

Opsiyonlar, içinde bir şey olan ya da olmayan bir kutu gibidir. Yani, a, `String?`içimizde bizi bekleyen bir dizi olabilir veya hiçbir şey olmayabilir - `nil`"değer yok" anlamına gelen özel bir değer adı verilen bir anlam ifade eder. `Int`, `Double`, ve `Bool`, numaralandırma, yapı ve sınıf örnekleri dahil olmak üzere her türlü veri isteğe bağlı olabilir .

Muhtemelen “peki… burada gerçekte ne değişti? Eskiden bir a vardı `String`ve şimdi bir a var `String?`, ama bu aslında yazdığımız kodu nasıl değiştirir?

İşin püf noktası şu: Swift, kodumuzun öngörülebilir olmasını seviyor, bu da orada olmayabilecek verileri kullanmamıza izin vermeyeceği anlamına geliyor. Opsiyonlar söz konusu olduğunda, bu, opsiyonel olanı kullanmak için _açmamız gerektiği anlamına gelir - bir değer olup olmadığını görmek için kutunun içine bakmamız ve varsa onu çıkarıp kullanmamız gerekir._

Swift bize opsiyonları açmanın iki temel yolunu veriyor, ama en çok göreceğiniz yol şuna benziyor:

```swift
if let marioOpposite = opposites["Mario"] {
    print("Mario's opposite is \(marioOpposite)")
}
```

Bu `if let`sözdizimi Swift'de _çok_`if` yaygındır ve bir koşul ( ) oluşturmayı bir sabit ( ) oluşturmayla birleştirir `let`. Birlikte, üç şey yapar:

1.  Sözlükten isteğe bağlı değeri okur.
2.  İsteğe bağlı içinde bir dize varsa, açılır _-_ bu, içindeki dizenin sabitin içine yerleştirildiği anlamına gelir `marioOpposite`.
3.  Koşul başarılı oldu - isteğe bağlı paketi açabildik - yani koşulun gövdesi çalıştırıldı.

Koşulun gövdesi, yalnızca isteğe bağlı içinde bir değer varsa çalıştırılacaktır. Tabii ki, bir blok eklemek istiyorsanız `else`- bu sadece normal bir durumdur, bu nedenle bu tür kodlar uygundur:

```swift
var username: String? = nil

if let unwrappedName = username {
    print("We got a user: \(unwrappedName)")
} else {
    print("The optional was empty.")
}
```

Opsiyonları biraz Schrödinger'in veri tipi gibi düşünün: kutunun içinde bir değer olabilir ya da olmayabilir, ancak öğrenmenin tek yolu kontrol etmektir.

Bu, şimdiye kadar oldukça akademik görünebilir, ancak isteğe bağlı seçenekler, daha iyi yazılım üretmemize yardımcı olmak için gerçekten çok önemlidir. Görüyorsunuz, aynı şekilde, isteğe bağlılar, verilerin mevcut olabileceği veya olmayabileceği anlamına gelir, isteğe bağlı _olmayanlar_ - normal dizeler, tamsayılar, vb. - verilerin mevcut olması _gerektiği anlamına gelir._

Bir düşünün: Eğer bir isteğe bağlı olmayanımız varsa, `Int`bu, içinde mutlaka bir sayı olduğu anlamına gelir, her zaman. 1 milyon veya 0 gibi bir şey olabilir ama yine de bir sayıdır ve var olması garantidir. Karşılaştırıldığında, isteğe bağlı bir `Int`kümenin `nil`hiçbir değeri yoktur - 0 veya başka bir sayı değildir, hiçbir şeydir.

Benzer şekilde, isteğe bağlı olmayan bir dizemiz varsa `String`, bu kesinlikle orada bir dize olduğu anlamına gelir: "Merhaba" veya boş bir dize gibi bir şey olabilir, ancak bunların her ikisi de olarak ayarlanan isteğe bağlı bir dizeden farklıdır `nil`.

`Array`Gerekirse, ve gibi koleksiyonlar da dahil olmak üzere her veri türü isteğe bağlı olabilir `Dictionary`. Yine, bir tamsayı dizisi bir veya daha fazla sayı içerebilir veya hiç sayı içermeyebilir, ancak bunların her ikisi de olarak ayarlanan isteğe bağlı dizilerden farklıdır `nil`.

Açık olmak gerekirse, olarak ayarlanan isteğe bağlı bir tamsayı , 0'ı tutan isteğe bağlı olmayan bir tamsayı ile aynı _değildir_`nil` , olarak ayarlanan isteğe bağlı bir dize , şu anda boş bir dizeye ayarlanan isteğe bağlı olmayan bir dize ve isteğe bağlı bir dizi ile aynı değildir olarak ayarlamak, şu anda hiç öğe içermeyen isteğe bağlı olmayan bir dizi ile aynı değildir - boş veya başka herhangi bir verinin olmamasından bahsediyoruz.`nil``nil`

[Zev Eisenberg'in dediği](https://translate.google.com/website?sl=auto&tl=tr&hl=tr&u=https://twitter.com/ZevEisenberg/status/1413107000867794950?s%3D20) gibi , “Swift isteğe bağlı seçenekler sunmadı. İsteğe bağlı olmayanları tanıttı.

İsteğe bağlı bir tamsayıyı isteğe bağlı olmayan bir tamsayı gerektiren bir işleve geçirmeye çalışırsanız, bunun gibi eylemde görebilirsiniz:

```swift
func square(number: Int) -> Int {
    number * number
}

var number: Int? = nil
print(square(number: number))
```

İsteğe bağlı tamsayı paketinin açılması gerektiğinden Swift bu kodu oluşturmayı reddedecek - isteğe bağlı olmayan bir değerin gerekli olduğu yerde isteğe bağlı bir değer kullanamayız, çünkü içinde bir değer olmasaydı bir sorunla karşılaşırdık.

Bu nedenle, isteğe bağlı kullanmak için önce onu şu şekilde _açmalıyız :_

```swift
if let unwrappedNumber = number {
    print(square(number: unwrappedNumber))
}
```

Bitirmeden önce, son bir şeyden bahsetmek istiyorum: opsiyonelleri açarken, onları aynı isimde bir sabite açmak çok yaygındır. Buna Swift'te tamamen izin verilir ve adlandırma sabitlerini veya benzerlerini tutmamız gerekmediği anlamına gelir `unwrappedNumber`.

Bu yaklaşımı kullanarak, önceki kodu şu şekilde yeniden yazabiliriz:

```swift
if let number = number {
    print(square(number: number))
}
```

Bu tarz, ilk okuduğunuzda biraz kafa karıştırıcı, çünkü artık kuantum fiziği gibi geliyor - aynı anda `number`gerçekten hem isteğe bağlı _hem de isteğe bağlı olmayan olabilir mi?_ Hayır.

Burada olan şey, geçici olarak, yalnızca koşulun gövdesi içinde mevcut olan, aynı ada sahip ikinci bir sabiti yaratmamızdır. _Buna gölgeleme_ denir ve çoğunlukla yukarıda gördüğünüz gibi isteğe bağlı açma işlemleriyle kullanılır.

Bu nedenle, koşulun gövdesinin _içinde,_ üzerinde çalışabileceğimiz açık bir değere sahibiz - `Int`isteğe bağlı değil gerçek `Int?`- ama _dışarıda_ hala isteğe sahibiz.

---

# Opsiyonel seçenekler koruma ile nasıl açılır?

  

Swift'in opsiyonelleri açmak için nasıl kullandığını zaten gördünüz `if let`ve bu, opsiyonelleri kullanmanın en yaygın yolu. Ancak hemen hemen aynı şeyi yapan ve neredeyse bir o kadar yaygın olan ikinci bir yol daha vardır: `guard let`.

Şuna benziyor:

```swift
func printSquare(of number: Int?) {
    guard let number = number else {
        print("Missing input")
        return
    }

    print("\(number) x \(number) is \(number * number)")
}
```

Like `if let`, `guard let`bir isteğe bağlı içinde bir değer olup olmadığını kontrol eder ve varsa değeri alır ve onu bizim seçtiğimiz bir sabite yerleştirir.

Ancak, bunu yapma _şekli_ işleri tersine çevirir:

```swift
var myVar: Int? = 3

if let unwrapped = myVar {
    print("Run if myVar has a value inside")
}

guard let unwrapped = myVar else {
    print("Run if myVar doesn't have a value inside")
}
```

Bu nedenle, `if let`isteğe bağlı bir değere sahipse kodu parantez içinde çalıştırır ve isteğe bağlı bir değere sahip _değilse_`guard let` kodu parantez içinde çalıştırır . Bu, şu koddaki kullanımını açıklar : "isteğe bağlı paketi açıp açamayacağımızı kontrol edin, ancak yapamazsak..."`else`

Bunun küçük bir fark gibi göründüğünün farkındayım, ancak önemli sonuçları var. Görüyorsunuz, `guard`program durumumuzun beklediğimiz gibi olup olmadığını kontrol etme yeteneği ve kurtarma değilse - örneğin mevcut işlevden çıkmak için.

Buna bazen _erken geri dönüş_ denir: işlev başlar başlamaz işlevin tüm girdilerinin geçerli olup olmadığını kontrol ederiz ve herhangi biri geçerli değilse bazı kodlar çalıştırıp hemen çıkarız. Tüm kontrollerimiz başarılı olursa, fonksiyonumuz tam olarak istendiği gibi çalışabilir.

`guard`tam olarak bu tarz programlama için tasarlanmıştır ve aslında yardımcı olacak iki şey vardır:

1.  Bir fonksiyonun girişlerinin geçerli olup olmadığını kontrol etmek için kullanırsanız , kontrol başarısız olursa `guard`Swift her zaman kullanmanızı isteyecektir .`return`
2.  Kontrol başarılı olursa ve paketini açtığınız isteğe bağlı değerin içinde bir değer varsa, bunu kod bittikten _sonra_ kullanabilirsiniz `guard`.

`printSquare()`İşleve daha önce bakarsanız, bu noktaların her ikisini de çalışırken görebilirsiniz :

```swift
func printSquare(of number: Int?) {
    guard let number = number else {
        print("Missing input")

        // 1: We *must* exit the function here
        return
    }

    // 2: `number` is still available outside of `guard`
    print("\(number) x \(number) is \(number * number)")
}
```

Yani: `if let`bir şekilde işleyebilmek için seçenekleri açmak için kullanın ve `guard let`seçeneklerin içinde bir şey olmasını sağlamak ve aksi halde çıkmak için kullanın.

**İpucu:** Korumayı, isteğe bağlı seçenekleri açmayanlar da dahil olmak üzere her koşulda kullanabilirsiniz. Örneğin, kullanabilirsiniz `guard someArray.isEmpty else { return }`.