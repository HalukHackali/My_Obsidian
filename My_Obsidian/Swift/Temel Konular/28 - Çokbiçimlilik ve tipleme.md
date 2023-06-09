#swift #yazılım 

Class'lar birbirinden türetilebildiği için (`Singer`sınıfından türetilen `CountrySinger` sınıfı gibi), bir class etkin bir şekilde diğerinin üstkümesidir: B class'ı birkaç fazlayla, A class'ının sahip olduğu her şeye sahiptir. Bu sonuçta, B class'ını B tipi veya A tipi olarak ihtiyacınıza göre işlemeniz demektir.

Alkınız mı karıştı? Hadi kod yazmaya çalışalım:

```swift
class Album {
    var name: String

    init(name: String) {
        self.name = name
    }
}

class StudioAlbum: Album {
    var studio: String

    init(name: String, studio: String) {
        self.studio = studio
        super.init(name: name)
    }
}

class LiveAlbum: Album {
    var location: String

    init(name: String, location: String) {
        self.location = location
        super.init(name: name)
    }
}
```

Bu, 3 class tanımlar: Albümler, stüdyo albümleri ve canlı albümler; son ikisi `Album` class'ından türetiliyor. `LiveAlbum` class'ının herhangi bir kopyası `Album`den türetildiği için, ya `Album` ya da `LiveAlbum` gibi işlenecektir; aynı anda ikisi de hem de. Buna çokbiçimlilik (polymorphism) denir ve aşağıdaki gibi bir kod yazabileceğin anlamına gelir:

```swift
var taylorSwift = StudioAlbum(name: "Taylor Swift", studio: "The Castles Studios")
var fearless = StudioAlbum(name: "Speak Now", studio: "Aimeeland Studio")
var iTunesLive = LiveAlbum(name: "iTunes Live from SoHo", location: "New York")

var allAlbums: [Album] = [taylorSwift, fearless, iTunesLive]
```

Burada, sadece albümleri tutan bir dizi oluşturduk, ama içine iki stüdyo albümü ve bir de canlı albüm yerleştirdik. Swift dili için bu son derece uygundur, çünkü hepsi `Album` class'ının soyundan geldi. Dolayısıyla aynı temel davranışı paylaşıyorlar.

Bunu bir adım daha öteye taşıyarak, çokbiçimliliğin aslında nasıl çalıştığını gösterelim. Bu üç class'a da `getPerformance()` metodunu ekleyelim:

```swift
class Album {
    var name: String

    init(name: String) {
        self.name = name
    }

    func getPerformance() -> String {
        return "The album \(name) sold lots"
    }
}

class StudioAlbum: Album {
    var studio: String

    init(name: String, studio: String) {
        self.studio = studio
        super.init(name: name)
    }

    override func getPerformance() -> String {
        return "The studio album \(name) sold lots"
    }
}

class LiveAlbum: Album {
    var location: String

    init(name: String, location: String) {
        self.location = location
        super.init(name: name)
    }

    override func getPerformance() -> String {
        return "The live album \(name) sold lots"
    }
}
```

`Album` class'ında `getPerformance()` metodu zaten var, ama iki child class da (türetilen class'lar) onu geçersiz kılıyor. `Album` değerlerini içeren bir dizi oluşturduğumuzda, aslında onu albümlerin subclass'larıyla (alt sınıflarıyla) doldurmuş oluyoruz: `LiveAlbum` ve `StudioAlbum`. `Album`sınıfından türetildikleri için bu dizinin içine girmelerinde bir sorun yok, çünkü zaten orjinal class'larını asla kaybetmezler. Dolayısıyla kodu şu şekilde yazabiliriz:

```swift
var taylorSwift = StudioAlbum(name: "Taylor Swift", studio: "The Castles Studios")
var fearless = StudioAlbum(name: "Speak Now", studio: "Aimeeland Studio")
var iTunesLive = LiveAlbum(name: "iTunes Live from SoHo", location: "New York")

var allAlbums: [Album] = [taylorSwift, fearless, iTunesLive]

for album in allAlbums {
    print(album.getPerformance())
}
```

Gerektiğinde subclass'a bağlı olan `getPerformance()` versiyonuna göre otomatik olarak override'ı (geçersiz kılmayı) kullanacak. İşte bu çokbiçimliliğin davranış şekli: Bir nesne onun sınıfı ve parent class'ı olarak çalışabilir; hepsi aynı anda.

## Tipleme ile veri tipi dönüştürme

Sıklıkla kendinizi, belirli tipte bir nesye sahip ama aslında onun farklı bir tipte olduğunu biliyor olarak bulursunuz. Ne üzücüdür ki, bildiğiniz şeyi Swift bilmiyorsa, kodunuzu derlemeyecektir. Bunun için bir çözüm var ve ismi de tipleme (typecasting): Belirli bir tipteki nesneyi, bir diğerine dönüştürme.

Muhtemelen bunun neden gerekli olacağını düşünüp çabalıyorsunuz, ama size basit bir örnek verebilirim:

```swift
for album in allAlbums {
    print(album.getPerformance())
}
```

Bu bizim birkaç dakika önceki döngümüzdü. `allAlbums` adlı dizi, `Album` tipini tutyor, ama biz aslında subclass'larından birini tuttuğunu biliyoruz: `StudioAlbum` veya `LiveAlbum`. Swift bunu bilmiyor, o yüzden `print(album.studio)` gibi birşey yazmayı denerseniz, derlemeyi reddedecektir, çünkü sadece `StudioAlbum`nesneleri bu özelliğe sahip.

Swift dilinde tipleme üç şekilde gelir, ama çoğunlukla sadece ikisiyle karşılaşacaksın: `as?` ve `as!`. Bunlar optional downcasting (seçimli indirgeme) ve forced downcasting (zorla indirgeme) olarak bilinirler. İlki, "bu dönüşümün doğru olduğunu sanıyorum, ama hata verebilir", ikincisi ise "bu dönüşümün doğru olduğunu biliyorum ve eğer yanılıyorsam uygulamam çökeceği için mutluyum" anlamına gelir.

**Not:** "Dönüşüm" derken, nesnenin harfiyen değiştirileceğini kastetmiyorum. Daha çok, Swift'in nesneye nasıl davranacağını anlatmaya çalışıyorum; Swift'e bir nesnenin A tipinde olduğunu sandığını, ama aslında E tipinde olduğunu söylüyorsunuz.

Neler olduğu hakkında soru ve ünlem işaretleri bir ipucu verebilir, çünkü optional alanına çok benzerdir. Örneğin, şöyle yazarsanız:

```swift
for album in allAlbums {
    let studioAlbum = album as? StudioAlbum
}
```

Swift, `studioAlbum`ü `StudioAlbum?` veri tipine sahip bir sabit haline getirecek. Bu, stüdyo albüm için bir seçimdir: Dönüşüm, birlikte çalıştığınız stüdyo albümüne sahip olduğunuz bu durumda bir ihtimal işe yarayabilir veya nil değerine sahip olduğunuz durum da hata verebilir.

Optional sonuçları otomatik olarak açmak için en genel kullanım şekli `if let` ile olanıdır. Şunun gibi:

```swift
for album in allAlbums {
    print(album.getPerformance())

    if let studioAlbum = album as? StudioAlbum {
        print(studioAlbum.studio)
    } else if let liveAlbum = album as? LiveAlbum {
        print(liveAlbum.location)
    }
}
```

Bu her albüme bakacak ve onun performans detaylarını yazdıracak, çünkü bu hem `Album`class'ında hem de onun tüm subclass'larında ortaktır. Sonrasında `album` değerini `StudioAlbum` class'ına dönüştürüp dönüştüremeyeceğini kontrol eder ve eğer dönüştürebilecekse, stüdyo adını yazdırır. Aynı şey dizideki `LiveAlbum` için de geçerlidir.

Zorla indirgeme ise, bir nesnenin tipinin başka bir tip gibi davranabildiğinden gerçekten emin olduğunuzda yapılır. Ama eğer hatalıysanız, program çöker. Dönüşümün kesinlikle işe yarayacağını söylediğiniz için, zorla indirgemenin optional bir değer döndürmesi gerekmez. Ama eğer yanılıyorsanız, kodu yanlış yazıyorsunuz demektir.

Bunu çökmeyen bir yolla göstermek için, dizide sadece stüdyo albümü kalacak şekilde, canlı albümü çıkaralım:

```swift
var taylorSwift = StudioAlbum(name: "Taylor Swift", studio: "The Castles Studios")
var fearless = StudioAlbum(name: "Speak Now", studio: "Aimeeland Studio")

var allAlbums: [Album] = [taylorSwift, fearless]

for album in allAlbums {
    let studioAlbum = album as! StudioAlbum
    print(studioAlbum.studio)
}
```

Bu açıkça yapmacık bir örnek, çünkü eğer gerçek olsaydı, sadece `allAlbums` değişkenini değiştirerek, veri tipinin `[StudioAlbum]` olmasını olmasını sağlayabilirdik. Ama yine de zorla ingirgemenin nasıl çalıştığını gösteriyor ve örnek kod çökmeyecek çünkü doğru varsayımlarla yaptım.

Swift, dizi döngüsünün bir parçası olarak indirgemene izin verir ki, bizim örneğimizde daha verimli olurdur. Eğer zorla indirgemeyi dizi seviyesinde yapmak isterseniz, şu şekilde yazarsınız:

```swift
for album in allAlbums as! [StudioAlbum] {
    print(album.studio)
}
```

Böylece döngü içerisindeki her bir elemanın indirgenmesi gerekmez, çünkü daha döngü başlarken bu yapılmış oluyor. Tekrar söyleyelim, dizideki tüm elemanların `StudioAlbums`olduğunu doğrulamak en iyisi olacaktır, aksi taktirde kodunuz çöker.

Swift aynı zamanda, biraz daha oyunbaz olsa da, dizi seviyesinde seçimli indirgemeye de izin verir; çünkü döngü için her zaman bir değerin olduğunu garantileyecek bir nil birleştirme operatörüne ihtiyacınız vardır. İşte bir örnek:

```swift
for album in allAlbums as? [LiveAlbum] ?? [LiveAlbum]() {
    print(album.location)
}
```

Bu şu anlama gelir: "`allAlbums` değişkenini `LiveAlbum` nesnesinin bir dizisi olacak şekilde dönüştürmeyi dene, ama eğer başarısız olursa, hemen canlı albümler için boş bir dizi oluştur ve örneğin hiçbir şey yapmamak yerine bunu kullan."

## Başlatıcılarla ortak tipleri dönüştürme

Swift'in bilmediği bir şeyi bildiğinde tipleme faydalı birşeydir. Örneğin `A` tipinde bir nesneniz varken, Swift bunun `B` tipinde olduğunu sanır. Her ne kadar tipleme gerçekten sadece bu tipler söylediğiniz gibi olduğunda faydalıysa da, bir `A` tipini bir `Z` tipine dönüşmeye zorlayamazsınız; tabi eğer gerçekten ilgisi yoksa.

Örneğin, `number` adında bir tam sayınız varsa, onu String yapmak için şöyle bir kod yazamazsınız:

```swift
let number = 5
let text = number as! String
```

Bu, bir tam sayıyı bir string'e dönüşmeye zorlayamazsınız demektir, çünkü ikisi birbirlerinden tamamen farklıdır. Bunun yerine, tam sayı ile beslenen yeni bir string oluşturmanız gerekli ki, Swift bu ikisini nasıl dönüştüreceğini bilsin. Fark inceliklidir: Aynı değerin yeniden yorumlanmasından ziyade, bu _yeni_ bir değerdir.

Dolayısıyla kod şu şekilde yeniden yazılabilir:

```swift
let number = 5
let text = String(number)
print(text)
```

Bu, Swift dilinin sadece belirli dahili veri tipleri için işe yarar: Tam sayıları veya ondalıklı sayıları string'e ve tekrar geriye çeviremezsiniz. Örneğin isteğe göre hazırlanmış iki struct oluşturursanız, Swift birini diğerine sihirli bir şekilde dönüştüremez; bu kodu kendiniz yazmalısınız.