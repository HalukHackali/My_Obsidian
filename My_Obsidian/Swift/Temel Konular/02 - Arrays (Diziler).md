#swift #yazılım 

Diziler birçok değeri tek bir koleksiyonda gruplamanızı, ardından da koleksiyondaki yerini kullanarak bu değerlere ulaşmanızı sağlar. Swift, tip belirtecini kullanarak, dizinin ne tür bir veri tuttuğunu belirler. Yani şöyle:

```swift
var evenNumbers = [2, 4, 6, 8]
var songs = ["Shake it Off", "You Belong with Me", "Back to December"]
```

Gördüğünüz gibi, Swift dili bir dizinin başlangıcını ve sonunu belirlemek için köşeli parantez kullanır ve dizideki her bir eleman virgül ile birbirinden ayrılır.

***<mark style="background: #FFF3A3A6;">Bir dizinin içeriği okunmaya başladığında, dikkat etmelisiniz:</mark>*** Swift dili 0'dan (sıfırdan) saymaya başlar. Bu, ilk elemanın 0, ikinci elemanın 1, üçüncünün 2 ve böyle devam ettiği anlamına gelir. Oyun alanınıza şunu girmeyi deneyin:

```swift
var songs = ["Shake it Off", "You Belong with Me", "Back to December"]
songs[0]
songs[1]
songs[2]
```

Bu kodun sonuç panelindeki çıktısı "Shake it Off", "You Belong with Me" ve "Back to December" olacaktır.

Dizideki bir elemanın pozisyonu onun indeksi olarak anılır ve herhangi bir elemanı bu indeksi kullanarak okuyabilirsiniz. Ama tabi dikkatli olmalısınız, üç elemanlı dizimizin 0, 1 ve 2. indeksleri doğru çalışacaktır. Eğer `songs[3]`yazmayı denerseniz, oyun alanınız çalışmayı durduracaktır; eğer gerçek bir uygulamada denemiş olsaydınız, çökerdi!!

Üç tane String vererek diziyi oluşturduğunuz için, Swift bunun bir String dizisi olduğunu biliyor. Oyun alanında, herhangi bir değişkenin veri tipini yazdırıran özel bir komut kullanarak, bu sonucu onaylayabilirsiniz:

```swift
var songs = ["Shake it Off", "You Belong with Me", "Back to December"]
type(of: songs)
```

Bu komut, `songs` dizisinin String'lerden oluştuğunun Swift dili tarafından kabul edildiğini size söyleyerek, sonuç paneline `Array<String>.Type` yazdıracaktır.

Diyelim ki bir hata yaptınız ve kazara dizinin sonuna bir sayı girdiniz. Şunu deneyin ve sonuç panelinde ne yazdığına bakın:

```swift
var songs = ["Shake it Off", "You Belong with Me", "Back to December", 3]
type(of: songs)
```

Bu kez bir hata göreceksiniz. Bu hata, bu dizide olduğu gibi karışık veri tiplerini içeren dizilerle Swift dilinin aş edemediği için değil –bunun nasıl yapıldığını birazdan size göstereceğim!– aksine, Swift dilinin ne kadar yardımcı olduğu içindir. Gördüğünüz hata mesajı <mark style="background: #FF5582A6;">“heterogenous collection literal could only be inferred to '[Any]'; add explicit type annotation if this is intentional.”</mark> <mark style="background: #FFF3A3A6;">"(ayrı cinsten oluşan koleksiyonlar sadece '[Any]' olarak belirtildiğinde oluşturulur; eğer niyetiniz buysa açıkça tip belirtecinizi ekleyin.")</mark> Anlayacağımız şekilde söylersek, **"bu dizi birçok veri tipi için tasarlanmışa benziyor, eğer amacınız buysa, lütfen bunu açık seçik belirtin."**

Tip güvenliği önemlidir ve Swift dilindeki diziler her tür veriyi tutabilmesine rağmen, bu özel durum kazara olmuştu. Neyse ki, dizide tam olarak ne tür veri saklamak istediğinizi belirlemek için tip belirtimi kullanabileceğinizi size söylemiştim. Bir dizinin tipini belirlemek için, köşeli parantezlerin içine veri tipini şu şekilde yazabilirsin:

```swift
var songs: [String] = ["Shake it Off", "You Belong with Me", "Back to December", 3]
```

Şimdi biz, Swift diline bu dizinin içine sadece String saklamak istediğimizi söyledik, ama 3 rakamı String olmadığı için kodumuzun çalışması reddedilecektir.

Eğer dizinin herhangi bir tür veri tipini tutmasını istiyorsak gerçekten, o zaman özel `Any` veri tipini kullanacağız:

```swift
var songs: [Any] = ["Shake it Off", "You Belong with Me", "Back to December", 3]
```

## Dizi oluşturmak

Yukarıda gösterilen sözdizimini kullanarak bir dizi oluşturmak istersek, Swift diziyi oluşturur ve belirlediğimiz değerlerle içini doldurur. Ama önce diziyi oluşturup, içini sonra doldurmak isterseniz, bu öyle basitçe olmaz; bu sözdizimi işe yaramaz:

```swift
var songs: [String]
songs[0] = "Shake it Off"
```

Sebep ilk bakışta gereksiz bir detaycılık olarak görünecek, ama biraz derinlemesine bakınca altında yatan performans konuları olduğunu anlayacaksınız. Galiba siz buraya takıldınız. Basitçe `var songs: [String]` yazmak, `songs` değişkeninin String'lerden oluşan bir diziyi saklayacağını Swift'e söylemiş oluruz, ama _aslında bu diziyi oluşturmuş olmaz_. RAM'de herhangi bir alan kaplamaz veya Swift dizisini oluşturan herhangi bir iş yapılmış olmaz. Sadece bir dizi oluşturulacağını ve bu dizinin String veri tiplerini saklayacağını söyler.

Bunu doğru bir şekilde ifade edebilmenin birkaç yolu var ve şu anda en anlamlı olanı da muhtemelen bu:

```swift
var songs: [String] = []
```

String'lerden oluşan bir dizi oluşturacağımızı açıklığa kavuşturan ve ona içi boş bir dizi atayan (yani şöyle `[]`) tip belirtimini kullanılıyor.

Aynı zamanda yaygın olarak kullanılan bu yapıyı da göreceksiniz:

```swift
var songs = [String]()
```

Aynı anlama geliyorlar: `()` şeklindeki kullanım, tip çıkarsamasını kullanarak `songs` değişkenine atanacak olan söz konusu diziyi oluşturacağımızı Swift'e söyler. Bu seçenek iki karakter daha kısadır, dolayısıyla programcıların bu kullanımı tercih edecekleri şaşırtıcı olmaz!

## Dizi operatörleri

Diziler üzerinde sınırlı bir operatör serisi kullanabilirsiniz. Örneğin, aşağıdaki gibi iki diziyi + operatörünü kullanarak birleştirebilirsiniz:

```swift
var songs = ["Shake it Off", "You Belong with Me", "Love Story"]
var songs2 = ["Today was a Fairytale", "Welcome to New York", "Fifteen"]
var both = songs + songs2
```

Eklemek ve atamak için de şu şekilde += operatörünü kullanabilirsiniz:

```swift
both += ["Everything has Changed"]
```
---
# Sıralı veriler dizilerde nasıl saklanır?

İster haftanın günleri, ister bir sınıftaki öğrencilerin listesi, bir şehrin son 100 yıldaki nüfusu veya sayısız başka örnek olsun, çok sayıda verinin tek bir yerde olmasını istemek son derece yaygındır.

Swift'te bu gruplamayı bir _dizi_ kullanarak yaparız . `String`Diziler , `Int`, ve gibi kendi veri türleridir `Double`, ancak yalnızca bir dizi tutmak yerine sıfır dizi, bir dizi, iki dizi, üç, elli, elli milyon veya hatta daha fazla dizi tutabilirler - otomatik olarak şu şekilde tutmaya uyum sağlayabilirler: istediğiniz kadar çok ve verileri her zaman eklediğiniz sırada tutun.

Dizi oluşturmaya ilişkin bazı basit örneklerle başlayalım:

```swift
var beatles = ["John", "Paul", "George", "Ringo"]
let numbers = [4, 8, 15, 16, 23, 42]
var temperatures = [25.3, 28.2, 26.4]
```

Bu, üç farklı dizi oluşturur: biri insan isimlerini tutan diziler, biri önemli sayıların tamsayıları ve biri de Santigrat cinsinden ondalık sıcaklıkları tutan. Her öğe arasında virgül bulunan köşeli parantezler kullanarak dizileri nasıl başlattığımıza ve bitirdiğimize dikkat edin.

_Bir diziden_ değerleri okumaya gelince , değerleri dizide göründükleri konuma göre isteriz. Bir dizideki bir öğenin konumu genellikle dizini olarak _adlandırılır_ .

Bu, yeni başlayanların biraz kafasını karıştırır, ancak Swift aslında bir öğenin dizinini birden değil sıfırdan sayar -  örneğin `beatles[0]`, ilk öğedir ve `beatles[1]`ikincisidir.

Böylece, dizilerimizden bazı değerleri şu şekilde okuyabiliriz:

```swift
print(beatles[0])
print(numbers[1])
print(temperatures[2])
```

**İpucu:** İstediğiniz dizinde bir öğe olduğundan emin olun, aksi takdirde kodunuz çöker - uygulamanız çalışmayı durdurur.

Diziniz değişken ise, onu oluşturduktan sonra değiştirebilirsiniz. `append()`Örneğin, yeni öğeler eklemek için şunları kullanabilirsiniz :

```swift
beatles.append("Adrian")
```

Ve sizi birden fazla öğe eklemekten alıkoyan hiçbir şey yok:

```swift
beatles.append("Allen")
beatles.append("Adrian")
beatles.append("Novall")
beatles.append("Vivian")
```

_Ancak Swift, eklemeye çalıştığınız veri türünü_ izler ve dizinizin her seferinde yalnızca bir tür veri içerdiğinden emin olur. Dolayısıyla, bu tür bir koda [izin verilmez](https://translate.google.com/website?sl=auto&tl=tr&hl=tr&u=https://twitter.com/MuseumShuffle/status/1444267345103532032?s%3D20) :

```swift
temperatures.append("Chris")
```

Bu aynı zamanda diziden veri okumak için de geçerlidir - Swift, dizinin `beatles`dizeler içerdiğini bilir, bu nedenle bir değeri okuduğunuzda her zaman bir dize alırsınız. Aynısını ile yapmaya çalışırsanız `numbers`, her zaman bir tamsayı alırsınız. Swift, bu iki farklı türü birlikte karıştırmanıza izin vermez, bu nedenle bu tür kodlara izin verilmez:

```swift
let firstBeatle = beatles[0]
let firstNumber = numbers[0]
let notAllowed = firstBeatle + firstNumber
```

Bu tür güvenliğidir, tıpkı Swift'in daha derin bir düzeye götürülmesi dışında tamsayıları ve ondalık sayıları karıştırmamıza izin vermemesi gibi. Evet, hepsi `beatles`ve `numbers`her ikisi de dizidir, ancak bunlar özel dizi türleridir: biri bir dizi dizisidir ve biri bir tamsayılar dizisidir.

Boş bir dizi ile başlayıp ona tek tek öğeler eklemek istediğinizde bunu daha net görebilirsiniz. Bu çok kesin bir sözdizimi ile yapılır:

```swift
var scores = Array<Int>()
scores.append(100)
scores.append(80)
scores.append(85)
print(scores[1])
```

Son dört satırı zaten ele aldık, ancak bu ilk satır nasıl özel bir dizi tipine sahip olduğumuzu gösteriyor – bu herhangi bir dizi değil, tamsayıları tutan bir dizi. Bu, Swift'in bunun her zaman bir dizge olması gerektiğini kesin olarak bilmesini sağlayan `beatles[0]`ve aynı zamanda bizi bir dizge dizisine tamsayılar eklemekten alıkoyan şeydir.

Ardından gelen açma ve kapama parantezleri `Array<Int>`oradadır, çünkü gerekirse dizinin oluşturulma şeklini özelleştirmek mümkündür. Örneğin, daha sonra gerçek verileri eklemeden önce diziyi çok sayıda geçici veriyle doldurmak isteyebilirsiniz.

Farklı şekillerde özelleştirerek başka türden diziler oluşturabilirsiniz, bunun gibi:

```swift
var albums = Array<String>()
albums.append("Folklore")
albums.append("Fearless")
albums.append("Red")
```

Yine, bunun her zaman dize içermesi gerektiğini söyledik, bu yüzden oraya bir tamsayı koymaya çalışamayız.

Diziler Swift'te o kadar yaygındır ki onları oluşturmanın özel bir yolu vardır: yazmak yerine `Array<String>`yazabilirsiniz `[String]`. Dolayısıyla, bu tür bir kod öncekiyle tamamen aynıdır:

```swift
var albums = [String]()
albums.append("Folklore")
albums.append("Fearless")
albums.append("Red")
```

Swift'in tür güvenliği, bir dizinin ne tür veri depoladığını her zaman bilmesi gerektiği anlamına gelir. `albums`Bu, is an diyerek açık olmak anlamına gelebilir `Array<String>`, ancak bazı başlangıç ​​değerleri sağlarsanız Swift bunu kendi başına çözebilir:

```swift
var albums = ["Folklore"]
albums.append("Fearless")
albums.append("Red")
```

Bitirmeden önce, dizilerle birlikte gelen bazı kullanışlı işlevlerden bahsetmek istiyorum.

`.count`İlk olarak, tıpkı dizelerde yaptığınız gibi, bir dizide kaç öğe olduğunu okumak için kullanabilirsiniz :

```swift
print(albums.count)
```

`remove(at:)`İkinci olarak, belirli bir dizindeki bir öğeyi kaldırmak veya `removeAll()`her şeyi kaldırmak için öğesini kullanarak bir diziden öğeleri kaldırabilirsiniz :

```swift
var characters = ["Lana", "Pam", "Ray", "Sterling"]
print(characters.count)

characters.remove(at: 2)
print(characters.count)

characters.removeAll()
print(characters.count)
```

Bu, karakterler kaldırıldıkça 4, ardından 3 ve ardından 0 yazdıracaktır.

`contains()`Üçüncü olarak, şunun gibi kullanarak bir dizinin belirli bir öğe içerip içermediğini kontrol edebilirsiniz :

```swift
let bondMovies = ["Casino Royale", "Spectre", "No Time To Die"]
print(bondMovies.contains("Frozen"))
```

`sorted()`Dördüncüsü, şunun gibi kullanarak bir diziyi sıralayabilirsiniz :

```swift
let cities = ["London", "Tokyo", "Rome", "Budapest"]
print(cities.sorted())
```

Bu, öğeleri artan düzende sıralanan yeni bir dizi döndürür; bu, dizeler için alfabetik olarak ancak sayılar için sayısal olarak anlamına gelir - orijinal dizi değişmeden kalır.

Son olarak, bir diziyi çağırarak tersine çevirebilirsiniz `reversed()`:

```swift
let presidents = ["Bush", "Obama", "Trump", "Biden"]
let reversedPresidents = presidents.reversed()
print(reversedPresidents)
```

**İpucu:** Bir diziyi tersine çevirdiğinizde, Swift çok zekidir - aslında tüm öğeleri yeniden düzenleme işini yapmaz, bunun yerine öğelerin tersine çevrilmesini istediğinizi kendi kendine hatırlar. Bu nedenle, çıktısını aldığınızda `reversedPresidents`, bunun artık basit bir dizi olmadığını görünce şaşırmayın!

Diziler Swift'te son derece yaygındır ve ilerledikçe onlar hakkında daha fazla şey öğrenmek için birçok fırsatınız olacak. Dizeler için daha da iyisi `sorted()`, `reversed()`, ve diğer pek çok dizi işlevi de mevcuttur - `sorted()`orayı kullanmak dizenin harflerini alfabetik sıraya koyar ve "swift" gibi bir şeyi "fistw"ye dönüştürür.

---
