#swift #yazılım 

# Enum nasıl oluşturulur ve kullanılır?

Enum - _enumeration_ kısaltması _-_ oluşturabileceğimiz ve kodumuzda kullanabileceğimiz bir dizi adlandırılmış değerdir. Swift için özel bir anlamları yoktur, ancak daha verimli ve daha güvenlidirler, dolayısıyla bunları kodunuzda çok kullanırsınız.

Sorunu göstermek için, kullanıcının haftanın bir gününü seçmesine izin verecek bir kod yazmak istediğinizi varsayalım. Şöyle başlayabilirsiniz:

```swift
var selected = "Monday"
```

Daha sonra kodunuzda şu şekilde değiştirirsiniz:

```swift
selected = "Tuesday"
```

Bu, çok basit programlarda işe yarayabilir, ancak şu koda bir bakın:

```swift
selected = "January"
```

Hata! Yanlışlıkla bir gün yerine bir ay yazdınız – kodunuz ne yapacak? Pekala, bir meslektaşınızın kodunuzu incelerken hatayı görmesini sağlayacak kadar şanslı olabilirsiniz, ama buna ne dersiniz:

```swift
selected = "Friday "
```

Cuma gününün sonunda boşluk olan ve boşluk olan “Friday”, Swift'in gözünde boşluk olmayan “Friday”den farklıdır. Yine, kodunuz ne yapardı?

Bu tür şeyler için dizeleri kullanmak çok dikkatli bir programlama gerektirir, ancak aynı zamanda oldukça verimsizdir - tek bir günü izlemek için "Cuma" nın tüm harflerini gerçekten saklamamız gerekiyor mu?

Sıralamaların devreye girdiği yer burasıdır: sahip olabileceği bir avuç belirli değerle yeni bir veri türü tanımlamamıza izin verirler. Yalnızca doğru veya yanlış olabilen bir Boole düşünün - bunu "belki" veya "muhtemelen" olarak ayarlayamazsınız çünkü bu onun anlayabileceği değerler aralığında değildir. Numaralandırmalar aynıdır: sahip olabileceği değer aralığını en baştan listeleriz ve Swift, bunları kullanırken asla hata yapmamanızı sağlar.

Böylece, hafta içi günlerimizi bunun gibi yeni bir listeye yeniden yazabiliriz:

```swift
enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
}
```

Bu, yeni numaralandırmayı çağırır `Weekday` ve haftanın beş gününü işlemek için beş vaka sağlar.

Şimdi dizeleri kullanmak yerine numaralandırmayı kullanırdık. Bunu oyun alanınızda deneyin:

```swift
var day = Weekday.monday
day = Weekday.tuesday
day = Weekday.friday
```

Bu değişiklikle birlikte yanlışlıkla “Cuma”yı fazladan boşluk bırakarak kullanamazsınız veya onun yerine bir ay adı koyamazsınız – her zaman numaralandırmada listelenen olası günlerden birini seçmelisiniz. Hatta yazdığınızda Swift'in olası tüm seçenekleri sunduğunu göreceksiniz `Weekday.`çünkü o, durumlardan birini seçeceğinizi biliyor.

Swift, numaralandırmaların kullanımını biraz daha kolaylaştıran iki şey yapar. İlk olarak, bir numaralandırmada birçok vakanız olduğunda, sadece bir kez yazabilir `case`, ardından her vakayı virgülle ayırabilirsiniz:

```swift
enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}
```

İkinci olarak, bir değişkene veya sabite bir değer atadığınızda veri türünün sabit hale geldiğini unutmayın; bir değişkeni önce bir dizgeye, ardından bir tamsayıya ayarlayamazsınız. 

Numaralandırmalar için bu, ilk atamadan sonra numaralandırma adını şu şekilde atlayabileceğiniz anlamına gelir:

```swift
var day = Weekday.monday
day = .tuesday
day = .friday
```

Swift, her zaman bir tür olması gerektiği için buna `.tuesday` atıfta bulunulması gerektiğini bilir . `Weekday.tuesday` `day` `Weekday`

`Weekday.monday` Burada görünmese de, numaralandırmaların en büyük faydalarından biri, Swift'in bunları optimize edilmiş bir biçimde saklamasıdır - Swift'in bunu 0 gibi tek bir tamsayı kullanarak saklayacağını söylediğimizde, depolamak ve kontrol etmek, depolamak ve kontrol etmekten çok daha verimlidir. M, o, n, d, a, y harfleri.

---
Enumerations, Swift içinde kullanılmak üzere kendi veri tipinizi oluşturmanızın bir yoludur; genellikle kısaca "enum" olarak bahsedilir ve "inam" olarak okunur. Bazı programlama dillerinde sadece basit işler için kullanılırlar, ama temelin ötesine geçmek isterseniz, Swift'in onlara verdiği büyük miktardaki gücü kullanabilirsiniz.

Daha önceki basit örnekle başlayalım:

```swift
func getHaterStatus(weather: String) -> String? {
    if weather == "sunny" {
        return nil
    } else {
        return "Hate"
    }
}
```

Bu fonksiyon şu andaki hava durumunu anlatan bir String kabul ediyor. Sorun, bu String'in verdiği bilgi açısından çok yetersiz kalmasıdır: "Yağmurlu" mu, "yağıyor" mu, "yağışlı" mı? Ya da "sağanak", "çisil çisil" veya "fırtınalı" mı? Daha da kötüsü, ya birisi "Rain" (yağmur) sözcüğünü büyük harfle başlatırken, bir diğeri ne yazdğına bakmadan yazdığı için onu "Ran" olarak yazarsa?

Enum'lar, yeni bir veri tipi belirleyip, olası değerleri tutması için yeni bir veri tipi belirlemenize izin vererek bu problemi çözer. Örneğin, beş tür hava durumu var diyelim: Sun, cloud, rain, wind ve snow (sırasıyla güneşli, bulutlu, yağmurlu, rüzgarlı ve karlı). Eğer biz bunlarla bir enum oluşturursak, Swift sadece bu beş değeri kabul edecek demektir; bunun dışındakiler hataya sebep olacak. Ayrıca enums, bilgisayarların String'lerden daha hızlı çalıştığı genellikle basit sayılardır.

Şunu kodunuza ekleyin:

```swift
enum WeatherType {
    case sun, cloud, rain, wind, snow
}

func getHaterStatus(weather: WeatherType) -> String? {
    if weather == WeatherType.sun {
        return nil
    } else {
        return "Hate"
    }
}

getHaterStatus(weather: WeatherType.cloud)
```

İlk üç satıra bir bakın: Birinci satırda veri tipimize `WeatherType` adını verdik. Bu, kodunuzda `String` veya `Int` yerine kullanacağınız şeydir. İkinci satırda ise yukarıda çerçevesini çizdiğim enum'ın olabileceği 5 olası değer belirleniyor. Geneleksen olarak bunlar küçük harfle başlıyor; "sun," "cloud", vs. Üçüncü satırda da enum tanımını bitiren süslü parantezi kapatıyoruz.

Şimdi nasıl kullanıldığına bir bakalım: `getHaterStatus()` fonksiyonunu `WeatherType` değeri kullanacak şekilde değiştirdim. Şartlı ifadeyi, `WeatherType.sun`değerimizle karşılaştırması için yeniden yazdım. Unutmayın, bu kontrol arka planda ışık hızında gerçekleşen bir sayıdır sadece.

Şimdi geri dönün ve kodu tekrar okuyun, çünkü iki önemli değişiklik yapmak üzere yeniden yazacağım. Herkes hazır mı?

```swift
enum WeatherType {
    case sun
    case cloud
    case rain
    case wind
    case snow
}

func getHaterStatus(weather: WeatherType) -> String? {
    if weather == .sun {
        return nil
    } else {
        return "Hate"
    }
}

getHaterStatus(weather: .cloud)
```

İki değişiklik yaptım. İlki, her bir hava durumu tipi şimdi kendi satırında. Bu küçük bir değişiklik gibi görünebilir ki, bu örnek için gerçekten de öyledir, ama sonrasında önemli hale gelecek. Yaptığım ikinci değişiklik, `if weather == .sun` ifadesini yazmaktı; `WeatherType.sun` demek istediğimi tekrardan hecelememe gerek yok, çünkü Swift tip çıkarsamasını kullanarak, bir `WeatherType`değişkeni ile karşılaştırma yaptığımı böylece biliyor.

Enum'lar özellikle `switch/case` blokları içinde çok kullanışlıdır, çünkü Swift enum içindeki tüm değerleri biliyor. Böylece onların hepsini kapsamanı garantiliyor. Örneğin, `getHaterStatus()`metodunu şu şekilde yeniden yazabiliriz:

```swift
func getHaterStatus(weather: WeatherType) -> String? {
    switch weather {
    case .sun:
        return nil
    case .cloud, .wind:
        return "dislike"
    case .rain:
        return "hate"
    }
}
```

Evet, "haters gonna dislike" (kinciler hiç hoşlanmayacak) gerçekten de harika bir söz, ama yine de akademik, çünkü bu kod çalışmayacak: `.snow` durumunu ele alamıyor, ama Swift bütün durumları kapsamayı ister. Ya bu durum için bir "case" daha ekleyeceksiniz, ya da "default case" ekleyeceksiniz.

## İlave değerlerle Enum'lar

Swift dilinin en güçlü özelliklerinden biri de, belirlediğiniz durumlara değerler verebilmenizdir. Gittikçe belirsizliği artan örneğimizi biraz daha öteye taşırsak, `.wind` (rüzgar) durumuna bir değer ekleyeceğim, böylece rüzgarın ne kadar hızlı olduğunu söyleyebileceğiz. Kodunuzu aşağıdaki gibi değiştirin:

```swift
enum WeatherType {
    case sun
    case cloud
    case rain
    case wind(speed: Int)
    case snow
}
```

Gördüğünüz gibi, diğer durumlar bir hız değerine gerek duymuyorlar, o yüzden sadece `wind`durumuna uyguladım. İşte şimdi gerçek sihir geliyor: Swift `switch/case` bloğumuza, sadece bu şartların doğru olduğu zaman eşleyeceği ekstra şartlar durumlar izin veriyor. Bu, bir durum içerisindeki değere ulaşacak `let` anahtar sözcüğünü, ardından da eşleşme deseni için `where` anahtar sözcüğünü kullanıyor.

İşte yeni fonksiyon:

```swift
func getHaterStatus(weather: WeatherType) -> String? {
    switch weather {
    case .sun:
        return nil
    case .wind(let speed) where speed < 10:
        return "meh"
    case .cloud, .wind:
        return "dislike"
    case .rain, .snow:
        return "hate"
    }
}

getHaterStatus(weather: WeatherType.wind(speed: 5))
```

Burada `.wind` durumunun iki kez belirdiğini görebilirsiniz. Ama ilki sadece hızın saatte 10 kilometrenin altında olduğu zamanlarda doğru olacak. Eğer rüzgar hızı 10 veya daha üzerindeyse, eşleşmeyecek. `let` ile oluşturduğunuz anahtar (kullanabileceğiniz bir sabit tanımlamak için) enum içesindeki değeri tutar, ardından kontrol etmek için de `where` şartını kullanır.

Swift dili, `switch/case` bloklarını yukarıdan aşağıya doğru değerlendirir ve bir eşleşme bulur bulmaz durur. Bu, eğer `case .cloud, .wind:`durumları, `case .wind(let speed) where speed < 10:` durumundan önce belirirse, daha önce çalıştırılacağı anlamına gelir ve çıktıyı değiştirir.

O yüzden, durumları nasıl sıralayacağınız konusunda dikkatli olun!

**Ek bilgi:** Swift dilindeki seçimliler aslında beraberinde değerleri olan enum'lar kullanılarak oluşturulmuştur. İki durum vardır: `none` ve `some`; `some`, seçimli içesinde herhangi bir değere sahip olma durumudur.

Bitti!