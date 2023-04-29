#swift #yazılım 

### <mark style="background: #FFF3A3A6;">Birden çok koşulu kontrol etmek için switch ifadeleri nasıl kullanılır?</mark>

`if` Koşulları tekrar tekrar kontrol etmek için ve tuşlarını istediğiniz kadar kullanabilirsiniz `else if`, ancak okunması biraz zorlaşır. Örneğin, bir listeden bir hava durumu tahminimiz olsaydı, aşağıdaki gibi bir dizi koşula dayalı olarak hangi mesajın yazdırılacağını seçebilirdik:

```swift
enum Weather {
    case sun, rain, wind, snow, unknown
}

let forecast = Weather.sun

if forecast == .sun {
    print("It should be a nice day.")
} else if forecast == .rain {
    print("Pack an umbrella.")
} else if forecast == .wind {
    print("Wear something warm")
} else if forecast == .rain {
    print("School is cancelled.")
} else {
    print("Our forecast generator is broken!")
}
```

Bu işe yarıyor, ancak sorunları var:

1.  `forecast`Her seferinde aynı şeyi kontrol etmemize rağmen yazmak zorunda kalıyoruz .
2.  Yanlışlıkla iki kez kontrol ettim `.rain`, ikinci kontrol asla doğru olamaz çünkü ikinci kontrol yalnızca ilk kontrol başarısız olursa yapılır.
3.  Hiç kontrol etmedim `.snow`, bu yüzden işlevsellik eksik.

Bu sorunların üçünü de koşulları kontrol etmenin farklı bir yolunu kullanarak çözebiliriz `switch`. Bu aynı zamanda bireysel vakaları tek tek kontrol etmemizi sağlar, ancak artık Swift yardımcı olabilir. Bir numaralandırma durumunda, sıralamanın sahip olabileceği tüm olası durumları bilir, bu nedenle birini kaçırırsak veya iki kez kontrol edersek şikayet eder.

`if`Böylece, tüm bunları ve `else if`kontrolleri bununla değiştirebiliriz :

```swift
switch forecast {
case .sun:
    print("It should be a nice day.")
case .rain:
    print("Pack an umbrella.")
case .wind:
    print("Wear something warm")
case .snow:
    print("School is cancelled.")
case .unknown:
    print("Our forecast generator is broken!")
}
```

Bunu parçalayalım:

1.  ile başlıyoruz `switch forecast`, bu da Swift'e kontrol etmek istediğimiz değerin bu olduğunu söylüyor.
2.  `case`Daha sonra , her biri karşılaştırmak istediğimiz değerler olan bir ifade dizimiz var `forecast`.
3.  Vakalarımızın her biri bir hava tipini listeliyor ve açıldığı için `forecast`yazmamıza gerek yok `Weather.sun`vs. `Weather.rain`- Swift bunun bir çeşit olması gerektiğini biliyor `Weather`.
4.  Her durumdan sonra, bu durum eşleşirse çalıştırılacak kodun başlangıcını işaretlemek için iki nokta üst üste yazarız.
5.  İfadeyi sonlandırmak için kapanış parantezini kullanırız `switch`.

`.snow`için değiştirmeyi denerseniz `.rain`, Swift'in yüksek sesle şikayet ettiğini göreceksiniz: bir kez `.rain`iki kez kontrol ettiğimizden ve yine ifademizin _ayrıntılı_`switch` olmadığından – tüm olası durumları ele almadığından.

Daha önce başka programlama dilleri kullandıysanız, Swift'in `switch`ifadesinin iki yerde farklı olduğunu fark etmiş olabilirsiniz:

1.  Tüm `switch`ifadeler kapsamlı _olmalıdır_ , yani kazara bir tanesini atlamamanız için olası tüm değerlerin burada işlenmesi gerekir.
2.  Swift, kontrol ettiğiniz koşulla eşleşen ilk durumu yürütecek, ancak daha fazlasını değil. Diğer diller genellikle sonraki tüm durumlardan başka kodlar yürütmeye devam eder ve bu genellikle tamamen yanlış varsayılan şeydir.

Bu ifadelerin her ikisi de doğru olsa da, ihtiyacımız olursa Swift bize biraz daha fazla kontrol sağlıyor.

İlk olarak, _evet_ , tüm `switch`ifadeler kapsamlı _olmalıdır_ : olası tüm değerlerin kapsandığından emin olmalısınız. Bir diziyi etkinleştiriyorsanız, o zaman sonsuz bir sayı olduğu için tüm olası dizilerin kapsamlı bir kontrolünü yapmak açıkça mümkün değildir, bu nedenle bunun yerine varsayılan bir durum sağlamamız gerekir - diğer durumlardan hiçbiri eşleşmezse çalışacak _kod_ .

Örneğin, bir yer adı içeren bir diziyi değiştirebiliriz:

```swift
let place = "Metropolis"

switch place {
case "Gotham":
    print("You're Batman!")
case "Mega-City One":
    print("You're Judge Dredd!")
case "Wakanda":
    print("You're Black Panther!")
default:
    print("Who are you?")
}
```

Bu, `default:`sonunda, tüm vakaların eşleşmemesi durumunda çalıştırılacak olan varsayılan vakadır.

**Unutmayın: Swift kasalarını sırayla kontrol eder ve ilk eşleşeni çalıştırır.** Başka bir durumun önüne koyarsanız `default`, bu durum işe yaramaz çünkü asla eşleştirilmeyecek ve Swift kodunuzu oluşturmayı reddedecektir.

İkinci olarak, Swift'in sonraki vakaları yürütmeye devam etmesini açıkça istiyorsanız _,_`fallthrough` . Bu yaygın olarak _kullanılmaz_ , ancak bazen - sadece bazen - işi tekrarlamaktan kaçınmanıza yardımcı olabilir.

Örneğin, The Twelve Days of Christmas adlı ünlü bir Noel şarkısı vardır ve şarkı devam ettikçe, yaklaşık altıncı günde evi oldukça dolu olan talihsiz bir kişiye giderek daha fazla hediye yığılır.

kullanarak bu şarkının basit bir tahminini yapabiliriz `fallthrough`. İlk olarak, kodun aşağıdakiler _olmadan_ `fallthrough` nasıl görüneceği aşağıda açıklanmıştır :

```swift
let day = 5
print("My true love gave to me…")

switch day {
case 5:
    print("5 golden rings")
case 4:
    print("4 calling birds")
case 3:
    print("3 French hens")
case 2:
    print("2 turtle doves")
default:
    print("A partridge in a pear tree")
}
```

Bu, tam olarak doğru olmayan “5 altın yüzük” yazdıracaktır. 1. gün sadece “Armut ağacında keklik”, 2. gün “2 kumru” ardından _“_ Armut ağacında keklik”, 3. gün “3 Fransız tavuğu”, “Armut ağacında keklik” yazılmalıdır. 2 kumru” ve… pekala, fikri anladınız.

`fallthrough`Tam olarak bu davranışı elde etmek için kullanabiliriz :

```swift
let day = 5
print("My true love gave to me…")

switch day {
case 5:
    print("5 golden rings")
    fallthrough
case 4:
    print("4 calling birds")
    fallthrough
case 3:
    print("3 French hens")
    fallthrough
case 2:
    print("2 turtle doves")
    fallthrough
default:
    print("A partridge in a pear tree")
}
```

Bu, ilk durumla eşleşir ve "5 altın yüzük" yazdırır, ancak `fallthrough`satır aracı `case 4`"4 çağıran kuş"u çalıştırır ve yazdırır, bu da `fallthrough`"3 Fransız tavuğu"nun yazdırılması için tekrar kullanır ve bu böyle devam eder. Şarkıyla mükemmel bir eşleşme değil, ama en azından işlevselliği çalışırken görebilirsiniz!

---

##  Switch case 2

Daha önce `if` ifadesini, ardından da döngüleri gördünüz. Ama Swift `switch/case` olarak anılan başka bir akış kontrol tipine daha sahiptir. Bunu en kolay şekliyle `if` ifadesinin gelişmiş bir formu olarak düşünün, çünkü birçok eşleşmeye sahip olabilirsiniz ve Swift doğru olanını çalıştıracak.

`switch/case` ifadesinin en temel formuyla, Swift'e hangi değişkeni kontrol etmek istediğinizi söyler, ardından bu değişken için olası durumları belirtirsiniz. Swift değişkeninize uyan ilk durumu bulur ve kod bloğunu çalıştırır. Bu blok bittiğinde Swift, `switch/case` bloğundan çıkar.

İşte size basit bir örnek:

```swift
let liveAlbums = 2

switch liveAlbums {
case 0:
    print("You're just starting out")

case 1:
    print("You just released iTunes Live From SoHo")

case 2:
    print("You just released Speak Now World Tour")

default:
    print("Have you done something new?")
}
```

Bunu `if` ve `else if` bloklarını kullanarak da pekala yazabilirdik, ama bu yöntem daha açık; önemli olan da bu.

`switch/case` kullanımının bir avantajı da, Swift yazdığınız durumların ayrıntılı olmasını sağlamasıdır. Bununla, kontrol etmediğiniz bir değere sahip değişkeninizin olma ihtimali varsa, Xcode uygulamanızı derlemeyi reddedecektir.

Etkili bir şekilde açık uçlu değişkenlerin olduğu durumlarda, tıpkı bizim `liveAlbums` tamsayısındaki gibi, bu olası değerleri yakalayacak `default` durum içermesine ihtiyacınız var. Evet, verinizin sadece belirli bir aralığa düştüğünü "bilseniz" bile, Swift tamamen emin olmak ister.

Swift, değişkenlere karşı eşleme yapabilmek için durum ifadelerinize bazı değerlendirmeler yapmaya başvurabilir. Örneğin, olası değerlerin aralığını kontrol etmek isterseniz, aşağıdaki şekilde kapalı aralık operatörünü kullanabilirsiniz:

```swift
let studioAlbums = 5

switch studioAlbums {
case 0...1:
    print("You're just starting out")

case 2...3:
    print("You're a rising star")

case 4...5:
    print("You're world famous!")

default:
    print("Have you done something new?")
}
```

Swift'teki `switch/case` blokları, bildiğiniz diğer dillerdeki gibi fos çıkmayacağını bilmelisiniz. Eğer `case` bloklarınızda `break` yazmaya alışkınsanız, Swift dilinde buna gerek olmadığını da bilmelisiniz.

Bunun yerine, bir durumun diğerine doğru akmasını sağlayan `fallthrough` anahtar sözcüğünü kullanın; etkili bir şekilde tam zıttıdır bu. Tabi bunun ne anlama geldiği hakkında herhangi bir fikriniz yoksa, bu daha iyi: Buna takılmayın!