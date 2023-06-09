#swift #yazılım 

Swift çok güvenli bir dildir. Yani sürpriz bir şekilde kodunuzun asla hata yapmamasını garantilemek için çok sıkı çalışır.

Kodun hata vermesinin en yaygın yollarından biri yanlış veya eksik bir veri kullanmaya çalışmasıdır. Örneğin, şöyle bir fonksiyon düşünün:

```swift
func getHaterStatus() -> String {
    return "Hate"
}
```

Bu fonksiyon herhangi bir parametre almıyor ve bir String döndürüyor: "Hate" (nefret). Peki ya bugün özellikle güneşli bir gün olsaydı ve bu nefret dolu olanlar, kötü hissetmeseydiler; ne olurdu o zaman? Belki o zaman hiçbir şey geri döndüremezdik: Bu nefret dolu olanları bugün hiçbir şey kötü hissettirmeyecek çünkü.

String'e gelince, boş bir String'in iletişim kurmamak için iyi bir yol olduğunu düşünebilirsiniz. Bu bazen doğru olabilir. Ama ya sayılarda? 0 (sıfır) "boş bir sayı" mıdır? Ya da -1?

Kendi kendinize hayali kurallar yaratmaya başlamadan önce, Swift dilinde bunun için bir çözüm olduğunu söyleyeyim: Optionals (seçimliler). Optional bir değişken, bir değer içerebilir de, içermeyebilir de. Çoğu kişi optional'ları anlamakta zorlanır. Sorun yok, çeşitli yollarla bunu açıklamaya çalışacağım. Umarım biri işe yarar.

Şimdilik, "Taylor Swift'in ne kadar muhteşem olduğunu hakkında 1'den 5'e kadar bir değerlendirme aralığı" vererek birine soru sorabileceğiniz bir anket yaptığınızı düşünün. İlk kez duyduğu biri hakkında herhangi biri nasıl cevap verebilir? 1 haksız bir şekilde onu cezalandırmak, 5 ise Taylor Swift hakkında hiçbir fikri olmayan birisi tarafından ödüllendirilmek olurdu. Çözüm optional'larda: "Herhangi bir rakam vermek istemiyorum."

`-> String` ifadesini kullandığımızda, "kesinlikle bir String döndürülecektir" anlamına gelir. Yani bu fonksiyon bir değer _döndüremez_ değildir. Dolayısıyla güvenli olacaktır çünkü kullanabileceğin bir String değer elde edeceğinin bilincinde olursun. Eğer Swift'e bu fonksiyonun bir değer döndürebileceğini veya belki de döndüremeyeceğini söylemek istersek, şu şekilde kullanmamız gerekir:

```swift
func getHaterStatus() -> String? {
    return "Hate"
}
```

Fazladan bir soru işareti var, dikkat ettiniz mi? `String?` ifadesi "optional string" (seçimli String) anlamına gelir. Bizim örneğimizde şimdi, ne olursa olsun "Hate" değeri döndürülecektir. Ama gelin bu fonksiyonu değiştirip bir adım daha öteye götürelim: Eğer hava güneşliyse, nefret dolu olanlar yeni bir sayfa açsınlar ve nefret dolu hayatlarını bıraksınlar; biz de herhangi bir değer geri döndürmeyelim. Swift dilinde bu "herhangi bir değer döndürmeyelim"in özel bir karşılığı var: `nil`.

Fonksiyonu aşağıdaki gibi değiştirin:

```swift
func getHaterStatus(weather: String) -> String? {
    if weather == "sunny" {
        return nil
    } else {
        return "Hate"
    }
}
```

Bu fonksiyon sadece bir String parametre (weather) kabul ediyor ve geriye bir String (nefret durumu) döndürüyor. Ama bu dönen değer orada olabilir de, olmayabilir de; yani "nil" durumu. Dönüş olarak ya bir String alacağız veya "nil" değerini alacağız.

Şimdi sıra önemli kısımda: Swift, yazdığınız kodun gerçekten güvenli olmasını ister, bu yüzden "nil" değerini kullanmaya çalışmak iyi bir fikir değil. Kodunuzu çökertebilir, uygulamanızın tüm mantığını yok edebilir veya kullanıcı arayüzünde yanlış şeyler gösterilmesine sebep olabilir. Sonuç olarak, bir değeri seçimli olarak belirttiyseniz, Swift güvenli bir şekilde onunla baş etmenizi sağlayacaktır.

Şimdi şunu deneyelim. Oyun alanınızdaki koda şu satırları ekleyin:

```swift
var status: String
status = getHaterStatus(weather: "rainy")
```

İlk satır String bir değişken oluşturur, ikincisi ise `getHaterStatus()` fonksiyonundan dönecek olan değeri atar. Bugün de hava yağışlı, yani bu nefret dolu olanlar kesinlikle kötü hissedecekler.

Yukarıdaki kod çalışmayacak, çünkü `status`değişkeni bir değer gerektiren `String` tipinde. Ama `getHaterStatus()` fonksiyonu optional String olduğu için bu değeri sağlamayabilir. Bu şu anlama gelir: `status` değişkeninde _kesinlikle_ bir String olacağını söyledik, ama `getHaterStatus()` fonksiyonu herhangi birşey döndürmeyebilir. Swift dili haliyle sizi bu hataya düşürmeyecek. Bu son derece faydalı birşey, çünkü etkili bir şekilde tüm genel hata sınıfını durduruyor.

Bu sorunu çözmek için, `status` değişkenine `String?` atamamız gerekli veya tip belirtimini tamamen silip, Swift'in tip çıkarsamasını kullanmasına izin vermemiz yeterli. İlk seçenek aşağıdaki gibi görünecek:

```swift
var status: String?
status = getHaterStatus(weather: "rainy")
```

İkinci seçenek ise şu şekilde olacak:

```swift
var status = getHaterStatus(weather: "rainy")
```

Hangisini seçerseniz seçin, bu değer orada olabilir de, olmayabilir de. Swift bunu tehlikeli bir şekilde kullanmanıza izin vermeyecek. Örnek olarak aşağıdaki gibi bir fonksiyon düşünün:

```swift
func takeHaterAction(status: String) {
    if status == "Hate" {
        print("Hating")
    }
}
```

Bu fonksiyon bir String alır ve içeriğine bağlı olarak bir mesaj yazdırır. Bu fonksiyon `String` bir değer alır, `String?` bir değer _değil_. Burada bir optional değer geçemezsiniz; `status` değişkenini kullanarak onu çağıramayacağı için gerçek bir String istiyor çünkü.

Swift'in iki çözümü var. İkisi de kullanıldı, ama biri diğerine tercih edilecek kesinlikle. İlk çözüm, "optional unwrapping" (optional'ı açma) olarak adlandırılır ve özel bir sözdizimi kullanılarak içerisindeki şartlı ifadelerle yapılır. Aynı anda iki şey yapar: Optional'ın bir değere sahip olup olmadığını kontrol eder ve eğer bir değeri varsa, onu "non-optional" (optional olmayan) bir veri tipi olarak açar, ardından da kod bloğunu çalıştırır.

Bahsettiğimiz sözdizimi şunun gibidir:

```swift
if let unwrappedStatus = status {
    // unwrappedStatus, optional olmayan bir değer içeriyor!
} else {
    // Bir else bloğu olmasını istiyorsanız, buyrun...
}
```

Bu `if let` ifadeleri kontrol eder ve onları daha ortak hale getiren kısa bir kod satırı içinde açar. Bu yöntemi kullanarak, `getHaterStatus()`fonksiyonundan dönen değeri güvenli bir şekilde açabilir ve geçerli, optional olmayan bir String'le sadece `takeHaterAction()` fonksiyonunu çağırdığımızdan emin olabiliriz. Kodun tamamı aşağıdadır:

```swift
func getHaterStatus(weather: String) -> String? {
    if weather == "sunny" {
        return nil
    } else {
        return "Hate"
    }
}

func takeHaterAction(status: String) {
    if status == "Hate" {
        print("Hating")
    }
}

if let haterStatus = getHaterStatus(weather: "rainy") {
    takeHaterAction(status: haterStatus)
}
```

**Eğer bu kavramı anladıysanız, "Optional'ları zorla açma" başlığına atlayabilirsiniz** Eğer optional'lar konusunu tam olarak anlayıp anlamadığınıza emin değilseniz, okumaya devam.

Hala buradaysanız, yukarıdaki açıklamanın sizin için ya bir anlamı yok, ya da anladınız sayılır ama muhtemelen biraz daha netleştirmeye ihtiyacınız var demektir bu. Optional'lar Swift dilinde yoğun bir şekilde kullanılırlar, o yüzden onları gerçekten onlamanız gerekli. Başka bir yoldan tekrar açıklamaya çalışacağım. Umarım bu yardımcı olur!

Işte size yeni bir fonksiyon:

```swift
func yearAlbumReleased(name: String) -> Int {
    if name == "Taylor Swift" { return 2006 }
    if name == "Fearless" { return 2008 }
    if name == "Speak Now" { return 2010 }
    if name == "Red" { return 2012 }
    if name == "1989" { return 2014 }

    return 0
}
```

Bu fonksiyon, Taylor Swift albüm adlarını alır ve yayınlandığı yılı geri döndürür. Ama Hudson Mohawke ile Taylor Swift'i karıştırdığımız "Lantern" adlı albümü çağırırsak (basit bir hata değil mi?), o zaman geriye 0 döndürür, çünkü bu bir Taylor Swift albümü değil.

Peki 0'ın burada bir anlamı var mı? Eğer albüm Caesar Augustus'un Roma İmparatoru olduğu zaman olan MS 0'da yayınlandıysa, 0'ın elbette bir anlamı var. Ama burası biraz kafa karıştırıcı. "Tanımlanamadı" anlamına gelen 0'ın, önceki bir zaman olduğunu bilmeleri gerekli.

Bu fonksiyonu yeniden yazmak çok daha iyi bir fikir, öyle ki, ya bir tam sayı dönsün (bir yıl değeri bulunduğunda) veya nil dönsün (hiçbir şey bulamadığında). İşte burada optional'lara teşekkür ediyoruz. İşte yeni fonksiyon:

```swift
func yearAlbumReleased(name: String) -> Int? {
    if name == "Taylor Swift" { return 2006 }
    if name == "Fearless" { return 2008 }
    if name == "Speak Now" { return 2010 }
    if name == "Red" { return 2012 }
    if name == "1989" { return 2014 }

    return nil
}
```

Artık geriye nil değerini döndürüyor. Herhangi bir değer içerip içermediğini kontrol etmek için `if let` yapısını kullanarak, sonucu açmamız gerekiyor.

**Eğer kavramı artık anladıysanız, "Optional'ları zorla açma" başlığına atlayabilirsiniz** Eğer optional'lar konusunu tam olarak anlayıp anlamadığınıza emin değilseniz, okumaya devam.

Evet, hala burada olduğunuza göre, gerçekten optional'ları anlamaya çabalıyorsunuz. O zaman ben de onları açıklamayı son bir kez daha deneyeceğim.

Burada isimlerden oluşan bir dizi var:

```swift
var items = ["James", "John", "Sally"]
```

Eğer diziye bakıp, belirli bir adın indeksini bize söyleyen bir fonksiyon yazmak isteseydik, muhtemelen şöyle birşey yazardık:

```swift
func position(of string: String, in array: [String]) -> Int {
    for i in 0 ..< array.count {
        if array[i] == string {
            return i
        }
    }

    return 0
}
```

Bu döngü dizideki tüm elemanlara bakar, eğer bir eşleşme bulursa onun pozisyonunu döndürür, bulamazsa 0 döndürür.

Şimdi şu dört satırlık kodu çalıştırmayı deneyin:

```swift
let jamesPosition = position(of: "James", in: items)
let johnPosition = position(of: "John", in: items)
let sallyPosition = position(of: "Sally", in: items)
let bobPosition = position(of: "Bob", in: items)
```

Bunların çıktısı 0, 1, 2, 0 olacak; birisi dizide olup, diğeri olmamasına rağmen James ve Bob'un pozisyonları aynı. Çünkü 0'ı "bulunamadı" anlamında kullandım. Basit bir düzeltme ile -1 olarak değiştirilebilir, ama ister 0, ister -1 olsun, hala sorun devam ediyor, çünkü "bulunamadı" anlamına gelen bu özel rakamı hatırlamak zorundasın.

Çözüm optional'lardır: Eğer bir eşleşme bulunursa, bir tam sayı döndür, bulunamazsa nil döndür. Aslında Swift dilinde dahili olarak bulunan "find in array" (dizinin içinde ara) metodunun yaklaşımıyla bu tamamamen aynıdır:

`someArray.index(of: someValue)`.

Bu "orada olabilir de, olmayabilir de" değerleri ile çalışırken, onları kullanmadan önce bir değer taşıyıp taşımadıkları bilgisine ulaşabilmek adına Swift sizi onları açmaya zorlar. `if let`kullanımının yaptığı şey budur: Eğer optional bir değere sahipse, onu aç ve kullan, değilse onu sakın kullanma. Dolayısıyla olası boş değerleri kazaen kullanamazsın; Swift buna izin vermeyecektir.

Eğer _hala_ optional'ların nasıl çalıştığından emin değilsen, en iyisi Twitter'dan bana sor: [@twostraws](http://twitter.com/twostraws)

## Force unwrapping optionals (Optional'ları zorla açma)

Swift, `!` ünlem işareti kullanarak, güvenliğini geçersiz kılmana izin verir. Eğer bir optional'ın kesinlikle bir değere sahip olduğunu biliyorsan, ardına bir ünlem işareti koyarak onu açmaya zorlayabilirsin. 

**Yine de lütfen dikkat edin: Eğer bunu bir değere sahip olmayan bir değişken üzerinde denerseniz, yazdığınız kod çökecektir.**

Çalışan bir örneği kullanarak, diğerlerini ekleyelim:

```swift
func yearAlbumReleased(name: String) -> Int? {
    if name == "Taylor Swift" { return 2006 }
    if name == "Fearless" { return 2008 }
    if name == "Speak Now" { return 2010 }
    if name == "Red" { return 2012 }
    if name == "1989" { return 2014 }

    return nil
}

var year = yearAlbumReleased(name: "Red")

if year == nil {
    print("There was an error")
} else {
    print("It was released in \(year)")
}
```

Bu, albümün yayınlandığı yılı getirir. Eğer albüm bulunamazsa, `year` değişkeni nil olarak ayarlanır ve bir hata mesajı yazdırılır. Aksi taktirde, yıl yazdırılacaktır.

Ya da öyle mi olacak? `yearAlbumReleased()`fonksiyonu optional bir tam sayı döndürür ve kod bu optional'ı açmak için `if let` yapısını kullanmaz. Sonuç olarak, şu mesaj yazdırılır: "It was released in Optional(2012)" (Yayınlandığı tarih Optional(2012)). Muhtemelen istediğimiz bu değil!

Kodun bu noktasında, geçerli bir değerimiz olduğunu zaten kontrol ettik, yani optional'ı güvenli bir şekilde açmak için başka bir `if let` kullanmak biraz anlamsız olacak. O yüzden, Swift bize bir çözüm sunuyor: İkinci `print()` çağrısını, aşağıdaki şekilde değiştirin:

```swift
print("It was released in \(year!)")
```

Ünlem işaretine dikkat edin: Bu "kesinlikle bir değer içeriyorum, şimdi onu açmaya zorlaya" anlamına geliyor.

## Implicitly unwrapped optionals (Dolaylı olarak açılan seçimliler)

Ünlem işaretini dolaylı olarak açılan optional'ları oluşturmak için de kullanabilirsiniz. Bu kavram bazı insanların gerçekten kafasını karıştırıyor. O yüzden lütfen dikkatle okuyun!

-   Sıradan bir değişken bir değer içerir. Örneğin: `String` bir String içermelidir; `""` şeklinde boş olsa bile. Ama _asla_ nil olamaz.
-   _Optional_ bir değişken bir değer içerebilir de, içermeyebilir de. Kullanılmadan önce açılmak zorundadır. Örneğin: `String?` bir String içerebilir veya nil değerini içerebilir. Bunu bilmenin tek yolu onu açmaktır.
-   Dolaylı olarak açılan bir optional, bir değer içerebilir de, içermeyebilir de. Ama kullanılmadan önce açılmasına gerek _yoktur_. Swift sizin için bunu kontrol etmeyecektir, o yüzden daha dikkatli olmalısınız. Örneğin: `String!` bir String içerebilir veya nil değerini içerebilir; uygun bir şekilde kullanmak size kalmış. Sıradan bir optional gibidir, ama Swift güvenli bir şekilde açılmadan doğrudan değere ulaşmanıza izin verir. Eğer bunu yapmayı denerseniz, bu orada bir değer olduğunu bildiğiniz anlamına gelir. Ama eğer yanılıyorsanız, uygulamanız çökecektir.

Dolaylı olarak açılmış optional'larla, iOS üzerindeki UIKit veya macOS üzerindeki AppKit içindeki kullanıcı arayüzü elemanları ile çalışırken tanışacaksınız asıl. Önde bunları tanımlanız gerekiyor, ama oluşturulana kadar onları kullanamazsınız. Zaten Apple da, gereksiz iş yapmaktan kaçınmak için olası en son anlarda kullanıcı arayüzü elemanların oluşturulmasını sever. Sürekli olarak değerleri açmanın, bir zaman sonra sıkıcı hale geleceğini kesinlikle biliyorsunuz, o yüzden bunlar dolaylı olarak açılanlardan yapıldı.

Eğer dolaylı olarak açılan optional'ları kavramayı biraz zor bulduysan, dert etme sakın. Dille çalıştıkça, daha anlaşılır hale gelecek.