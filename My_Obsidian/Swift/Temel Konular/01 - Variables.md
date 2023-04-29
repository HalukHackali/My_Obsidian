#swift #yazılım 

Ne zaman program oluştursanız, bazı verileri depolamak isteyeceksiniz. Belki az önce girdikleri kullanıcı adı, belki internetten indirdiğiniz bazı haberler veya az önce yaptığınız karmaşık bir hesabın sonucu olabilir.

Swift, verilerin zaman içinde değişmesini isteyip istemediğinize bağlı olarak bize verileri depolamanın iki yolunu sunar. İlk seçenek, yeni bir oyun alanı oluşturduğunuzda otomatik olarak kullanılır çünkü şu satırı içerecektir:

```swift
var greeting = "Hello, playground"
```

Bu, adında yeni bir değişken yaratır `greeting`ve bu bir değişken olduğu için değeri değişebilir _–_programımız çalışırken değişebilir.

**İpucu:** Bir macOS oyun alanındaki diğer satır `import Cocoa`, uygulama oluşturmayı kolaylaştırmak için Apple tarafından sağlanan büyük bir kod koleksiyonunu getiren . Bu, pek çok önemli işlevsellik içerir, bu nedenle lütfen onu silmeyin.

Orada gerçekten dört parça sözdizimi var:

-   Anahtar kelime `var`“yeni bir değişken oluştur” anlamına gelir; biraz yazarak tasarruf sağlar.
-   Değişkenimizi çağırıyoruz `greeting`. Değişkeninizi istediğiniz gibi arayabilirsiniz, ancak çoğu zaman onu tanımlayıcı yapmak isteyeceksiniz.
-   Eşittir işareti değişkenimize bir değer atar. İstemiyorsanız eşittir işaretinin her iki tarafında bu boşluklara sahip olmanıza gerek yoktur, ancak bu en yaygın biçimdir.
-   Atadığımız değer “Merhaba oyun alanı” metnidir. Metnin çift tırnak içine yazıldığına dikkat edin, böylece Swift metnin nerede başladığını ve nerede bittiğini görebilir.

Başka diller kullandıysanız, kodumuzun satırın sonunda noktalı virgüle gerek duymadığını fark etmişsinizdir. Swift, noktalı virgüllere _izin_ verir, ancak bunlar çok nadirdir - herhangi bir nedenle aynı satıra iki parça kod yazmak istiyorsanız onlara ihtiyacınız olacaktır.

Bir değişken yaptığınızda, onu zaman içinde değiştirebilirsiniz:

```swift
var name = "Ted"
name = "Rebecca"
name = "Keeley"
```

Bu, adında yeni bir değişken yaratır `name`ve ona "Ted" değerini verir. Daha sonra iki kez değiştirilir, önce "Rebecca" ve ardından "Keeley" olarak - `var`tekrar kullanmıyoruz çünkü yeni bir değişken oluşturmak yerine mevcut bir değişkeni değiştiriyoruz. Değişkenleri ihtiyacınız olduğu kadar değiştirebilirsiniz ve her seferinde eski değer atılır.

(Değişkenlerinize farklı metinler ekleyebilirsiniz, ancak ben Ted Lasso TV programının büyük bir hayranıyım, bu yüzden Ted ile gittim. Ve evet, sonraki bölümlerde başka Ted Lasso referansları ve daha fazlasını bekleyebilirsiniz.)

Bir değeri değiştirmek istemezseniz, bunun yerine bir _sabit_ kullanmanız gerekir . Bir sabit oluşturmak, bir değişken oluşturmakla neredeyse aynı şekilde çalışır, şu şekilde `let`yerine kullanmamız dışında:`var`

```swift
let character = "Daphne"
```

Şimdi, kullandığımızda , değişemeyecek bir değer olan bir _sabit_`let` yaparız . Swift kelimenin tam anlamıyla bize izin vermeyecek ve denersek büyük bir hata gösterecek.

Bana inanmıyor musun? Bunu Xcode'a koymayı deneyin:

```swift
let character = "Daphne"
character = "Eloise"
character = "Francesca"
```

Yine, ikinci ve üçüncü satırlarda hiç anahtar kelime yok `let`çünkü yeni sabitler oluşturmuyoruz, sadece elimizdekileri değiştirmeye çalışıyoruz. Ancak dediğim gibi bu işe yaramaz – bir sabiti değiştiremezsiniz, aksi halde sabit olmaz!

Merak ettiyseniz, "let" matematik dünyasından geliyor, burada "x 5'e eşit olsun" gibi şeyler söyleniyor.

**Önemli:** Lütfen hata gösteren iki kod satırını silin – sabitleri gerçekten değiştiremezsiniz!

Swift öğrenirken, Xcode'dan herhangi bir değişkenin değerini yazdırmasını isteyebilirsiniz. Kullanıcılar yazdırılanları göremediğinden gerçek uygulamalarda bu kadar fazla kullanmazsınız, ancak verilerinizin içinde ne olduğunu görmenin basit bir yolu olarak gerçekten yararlıdır.

Örneğin, her ayarlandığında bir değişkenin değerini yazdırabiliriz – bunu oyun alanınıza girmeyi deneyin:

```swift
var playerName = "Roy"
print(playerName)

playerName = "Dani"
print(playerName)

playerName = "Sam"
print(playerName)
```

**İpucu:** Solundaki mavi oynatma simgesine tıklayarak Xcode oyun alanınızda kod çalıştırabilirsiniz. O mavi şerit boyunca yukarı veya aşağı hareket ederseniz, oynat simgesinin de hareket ettiğini göreceksiniz - bu, isterseniz kodu belirli bir noktaya kadar çalıştırmanıza izin verir, ancak burada çoğu zaman sonuna kadar koşmak isteyeceksiniz. son satır

Değişkenimi , veya başka bir alternatif olarak `playerName`değil `playername`, olarak adlandırdığımı fark etmiş olabilirsiniz. Bu bir seçim: Swift , her yerde aynı şekilde atıfta bulunduğunuz sürece, sabitlerinizi ve değişkenlerinizi _ne olarak_`player_name` adlandırdığınızı gerçekten umursamıyor . Yani önce sonra sonra kullanamam – Swift bu ikisini farklı isimler olarak görüyor.`playerName``playername`

Swift, verilerimizi nasıl adlandırdığımızı umursamasa da, kullandığım adlandırma stili Swift geliştiricileri arasında standarttır - biz buna kural _diyoruz_ . Merak ediyorsanız, stile “camel case” denir, çünkü bir isimdeki ikinci ve sonraki kelimeler büyük harf için küçük bir çıkıntı ile başlar:

```swift
let managerName = "Michael Scott"
let dogBreed = "Samoyed"
let meaningOfLife = "How many roads must a man walk down?"
```

Yapabiliyorsanız, değişkenler yerine sabitleri kullanmayı tercih edin - bu, Swift'e kodunuzu biraz daha iyi hale getirme şansı vermekle kalmaz, aynı zamanda Swift'in bir sabitin değerini asla kazara değiştirmeyeceğinden emin olmasını da sağlar.

---

# Dizeler nasıl oluşturulur

Bir sabite veya değişkene metin atadığınızda, buna bir _dizi_ diyoruz - bir kelime oluşturmak için bir diziye dizilmiş bir grup Scrabble döşemesini düşünün.

Swift'in dizeleri çift tırnak ile başlar ve biter, ancak bu tırnakların içine ne koyacağınız size bağlıdır. Bunun gibi kısa alfabetik metin parçaları kullanabilirsiniz:

```swift
let actor = "Denzel Washington"
```

Noktalama işaretleri, emoji ve diğer karakterleri şu şekilde kullanabilirsiniz:

```swift
let filename = "paris.jpg"
let result = "⭐️ You win! ⭐️"
```

_Ayrıca, Swift'in bunların dizeyi bitirmek_ yerine dizenin _içinde_ olduğunu anlaması için önlerine ters eğik çizgi koymaya dikkat ettiğiniz sürece dizenizin içinde diğer çift tırnakları bile kullanabilirsiniz :

```swift
let quote = "Then he tapped a sign saying \"Believe\" and walked away."
```

Endişelenmeyin - eğer ters eğik çizgiyi kaçırırsanız, Swift kesinlikle kodunuzun tam olarak doğru olmadığını yüksek sesle haykıracaktır.

Dizilerinizin uzunluğu için gerçekçi bir sınır yoktur, yani bir diziyi Shakespeare'in tüm eserleri gibi çok uzun bir şeyi saklamak için kullanabilirsiniz. Ancak, Swift'in dizelerinde satır sonlarını sevmediğini göreceksiniz. Bu nedenle, bu tür bir koda izin verilmez:

```swift
let movie = "A day in
the life of an
Apple engineer"
```

_Bu, birden çok satırda dizeler oluşturamayacağınız_ anlamına gelmez , yalnızca Swift'in bunları özel olarak ele almanıza ihtiyacı vardır: dizenizin her iki tarafında bir dizi tırnak yerine, şu şekilde üç tane kullanırsınız:

```swift
let movie = """
A day in
the life of an
Apple engineer
"""
```

Bu çok satırlı dizeler çok sık kullanılmaz, ancak en azından nasıl yapıldığını görebilirsiniz: başlangıçtaki ve sondaki üçlü tırnaklar kendi satırlarında, sizin dizeniz arasında.

Dizginizi oluşturduktan sonra, Swift'in bize içeriğiyle çalışmamız için bazı yararlı işlevler verdiğini göreceksiniz. Zamanla bu işlevsellik hakkında daha fazla şey öğreneceksiniz, ancak size burada üç şeyi tanıtmak istiyorum.

`.count`İlk olarak, bir dizgenin uzunluğunu değişkenin veya sabitin adından sonra yazarak okuyabilirsiniz :

```swift
print(actor.count)
```

Çünkü `actor`"Denzel Washington" metni vardır ve bu, addaki her harf için bir tane artı ortadaki boşluk olmak üzere 17 basacaktır.

İstemiyorsanız bir dizenin uzunluğunu doğrudan yazdırmanıza gerek yoktur - bunu başka bir sabite atayabilirsiniz, bunun gibi:

```swift
let nameLength = actor.count
print(nameLength)
```

İşlevselliğin ikinci yararlı parçası `uppercased()`, her harfinin büyük olması dışında aynı dizgiyi geri gönderen işlevidir:

```swift
print(result.uppercased())
```

Evet, aç ve kapat parantezleri burada gereklidir _,_ ancak `count`. Bunun nedeni, öğrendikçe daha net hale gelecektir, ancak Swift öğreniminizin bu erken aşamasında ayrım en iyi şekilde şu şekilde açıklanır: Swift'ten bazı verileri okumasını istiyorsanız parantezlere ihtiyacınız yoktur, ancak eğer ' Swift'den sizin _yaptığınız_ bazı işleri yapmasını istiyorsunuz . Daha sonra öğreneceğiniz üzere bu tamamen doğru değil, ancak şimdilik ilerlemenizi sağlamak için yeterli.

Yararlı dize işlevinin son parçasına denir `hasPrefix()`ve bir dizenin seçtiğimiz bazı harflerle başlayıp başlamadığını bize bildirir:

```swift
print(movie.hasPrefix("A day"))
```

`hasSuffix()`Bir dizenin bir metinle bitip bitmediğini kontrol eden bir karşılığı da vardır :

```swift
print(filename.hasSuffix(".jpg"))
```

**Önemli:** Dizeler Swift'te büyük/küçük harfe duyarlıdır; bu, `filename.hasSuffix(".JPG")`dizedeki harfler küçük olduğundan, kullanmanın false döndüreceği anlamına gelir.

Dizeler Swift'te gerçekten güçlüdür ve yapabileceklerinin yalnızca yüzeyini çizdik!

---

# tam sayılar nasıl saklanır

_3, 5, 50 veya 5 milyon gibi tam sayılarla çalışırken, Swift'in tamsayı_ dediği şeyle çalışıyorsunuz veya `Int`kısaca - "tamsayı" aslında "tam" anlamına gelen Latince bir kelimedir; meraklı.

Yeni bir tamsayı oluşturmak, tıpkı bir dize oluşturmak gibi çalışır: `let`veya kullanın `var`, bir sabit veya değişken isteyip istemediğinize bağlı olarak, bir ad girin, sonra ona bir değer verin. `score`Örneğin, şöyle bir sabit oluşturabiliriz :

```swift
let score = 10
```

Tamsayılar gerçekten büyük olabilir - geçmiş milyarlar, geçmiş trilyonlar, geçmiş katrilyonlar ve hatta _kentilyonlar_ , ama gerçekten küçük de olabilirler - kentilyonlara kadar _negatif sayılar tutabilirler._

Rakamları elle yazarken, neler olup bittiğini tam olarak görmek zor olabilir. Örneğin, bu hangi sayıdır?

```swift
let reallyBig = 100000000
```

Bunu elle yazıyor olsaydık, muhtemelen “100.000.000” yazardık ve bu noktada sayının 100 milyon olduğu açıktır. `_`Swift'de buna benzer bir şey var: sayıları istediğiniz gibi ayırmak için alt çizgileri, , kullanabilirsiniz .

Böylece önceki kodumuzu şu şekilde değiştirebiliriz:

```swift
let reallyBig = 100_000_000
```

Swift aslında alt çizgileri umursamıyor, bu yüzden istersen onun yerine şunu yazabilirsin:

```swift
let reallyBig = 1_00__00___00____00
```

Sonuç aynıdır: `reallyBig`100.000.000 değerinde bir tamsayıya ayarlanır.

Elbette, okulda öğrendiğiniz aritmetik operatör türlerini kullanarak diğer tamsayılardan da tamsayılar oluşturabilirsiniz: `+`toplama, `-`çıkarma, `*`çarpma ve `/`bölme için.

Örneğin:

```swift
let lowerScore = score - 2
let higherScore = score + 10
let doubledScore = score * 2
let squaredScore = score * score
let halvedScore = score / 2
print(score)
```

Her seferinde yeni sabitler yapmak yerine, Swift'in bir tamsayıyı bir şekilde ayarlayan ve sonucu orijinal sayıya geri atayan bazı özel işlemleri vardır.

Örneğin, bu, `counter`10'a eşit bir değişken oluşturur ve ona 5 tane daha ekler:

```swift
var counter = 10
counter = counter + 5
```

Yazmak yerine , söz konusu tamsayıya doğrudan bir sayı ekleyen `counter = counter + 5`steno işlecini kullanabilirsiniz :`+=`

```swift
counter += 5
print(counter)
```

Bu tamamen aynı şeyi yapar, sadece daha az yazarak. _Bunlara bileşik atama işleçleri_ diyoruz ve başka biçimlerde geliyorlar:

```swift
counter *= 2
print(counter)
counter -= 10
print(counter)
counter /= 2
print(counter)
```

Tamsayılarla işimiz bitmeden önce, son bir şeyden bahsetmek istiyorum: tıpkı dizeler gibi, tamsayıların bazı kullanışlı işlevleri vardır. Örneğin, `isMultiple(of:)`başka bir tamsayının katı olup olmadığını öğrenmek için bir tamsayıyı arayabilirsiniz.

120'nin üçün katı olup olmadığını şu şekilde sorabiliriz:

```swift
let number = 120
print(number.isMultiple(of: 3))
```

Oradaki bir sabit numarayı arıyorum `isMultiple(of:)`, ancak isterseniz numarayı doğrudan kullanabilirsiniz:

```swift
print(120.isMultiple(of: 3))
```

---

# ondalık sayılar nasıl saklanır

3.1, 5.56 veya 3.141592654 gibi ondalık sayılarla çalışırken, Swift'in _kayan noktalı_ sayılar dediği şeyle çalışıyorsunuz. Adı, sayıların bilgisayarınızın şaşırtıcı derecede karmaşık bir şekilde saklanma biçiminden gelir: 123,456,789 gibi çok büyük sayıları, 0,0000000001 gibi çok küçük sayılarla aynı miktarda alanda depolamaya çalışır ve bunu yapabilmesinin tek yolu, sayının boyutuna göre ondalık noktayı hareket ettirmek.

Bu depolama yöntemi, ondalık sayıların programcılar için herkesin bildiği gibi sorunlu olmasına neden olur ve sadece iki satırlık Swift koduyla bunun tadına bakabilirsiniz:

```swift
let number = 0.1 + 0.2
print(number)
```

Bu çalıştığında 0.3 yazdırmaz. Bunun yerine, 0,30000000000000004 yazdıracak – bu 0,3, sonra 15 sıfır, sonra 4 çünkü… dediğim gibi, bu karmaşık.

_Neden_ karmaşık olduğunu birazdan daha fazla açıklayacağım ama önce neyin önemli olduğuna odaklanalım.

İlk olarak, bir kayan noktalı sayı oluşturduğunuzda, Swift bunu bir `Double`. Bu, "çift kesinlikli kayan noktalı sayı"nın kısaltması, bunun oldukça garip bir isim olduğunun farkındayım - kayan noktalı sayıları ele alma şeklimiz yıllar içinde çok değişti ve Swift bunu basitleştirme konusunda iyi bir iş çıkarsa da bazen daha karmaşık olan bazı eski kodlarla karşılaşabilirsiniz. Bu durumda, Swift'in bazı eski dillerin yaptığı gibi iki kat daha fazla depolama alanı tahsis ettiği anlamına gelir, bu da bir kutunun `Double`kesinlikle çok büyük sayıları depolayabileceği anlamına gelir.

İkincisi, Swift, ondalık sayıların tamsayılardan tamamen farklı bir veri türü olduğunu düşünür, bu da onları bir araya getiremeyeceğiniz anlamına gelir. Ne de olsa, tamsayılar her zaman %100 doğrudur, oysa ondalıklar değildir, bu nedenle Swift, özellikle olmasını istemediğiniz sürece ikisini bir araya getirmenize izin vermez.

Pratikte bu, ondalık sayıya tamsayı eklemek gibi şeyler yapamayacağınız anlamına gelir, dolayısıyla bu tür kodlar bir hata üretir:

```swift
let a = 1
let b = 2.0
let c = a + b
```

Evet, bunun gerçekten sadece 2 tamsayısının ondalık sayı gibi göründüğünü görebiliyoruz _,_`b` ancak Swift yine de bu kodun çalışmasına izin vermiyor. _Buna tür güvenliği_ denir : Swift, farklı veri türlerini kazara karıştırmamıza izin vermez.

`Double`Bunun olmasını istiyorsanız, Swift'e ya içini `b`şöyle ele alması gerektiğini açıkça söylemelisiniz `Int`:

```swift
let c = a + Int(b)
```

Veya `Int`içini `a`şu şekilde ele alın `Double`:

```swift
let c = Double(a) + b
```

`Double`Üçüncüsü, Swift, sağladığınız sayıya göre a mı yoksa an mı oluşturmak istediğinize karar verir `Int`- orada bir nokta varsa, a'nız vardır `Double`, aksi takdirde a'dır `Int`. Evet, noktadan sonraki sayılar 0 olsa bile.

Bu yüzden:

```swift
let double1 = 3.1
let double2 = 3131.3131
let double3 = 3.0
let int1 = 3
```

Tip güvenliği ile birleştiğinde bu, Swift'in bir sabitin veya değişkenin hangi veri tipini tuttuğuna karar verdiğinde, her zaman aynı veri tipini tutması gerektiği anlamına gelir. Bu, bu kodun iyi olduğu anlamına gelir:

```swift
var name = "Nicolas Cage"
name = "John Travolta"
```

Ancak bu tür bir kod değildir:

```swift
var name = "Nicolas Cage"
name = 57
```

Bu, Swift'in `name`bir dize saklayacağını söyler, ancak bunun yerine oraya bir tamsayı koymaya çalışır.

Son olarak, ondalık sayılar, tamsayılarla aynı operatör aralığına ve bileşik atama operatörlerine sahiptir:

```swift
var rating = 5.0
rating *= 2
```

Birçok eski API, ondalık sayıları depolamak için biraz farklı bir yol kullanır `CGFloat`. `Double`Neyse ki Swift, a'nın beklendiği her yerde normal sayıları kullanmamıza izin veriyor `CGFloat`, bu nedenle zaman zaman göründüğünü görseniz `CGFloat`de onu görmezden gelebilirsiniz.

Merak ettiyseniz, kayan noktalı sayıların karmaşık olmasının nedeni, bilgisayarların karmaşık sayıları depolamak için ikili (binary) kullanmaya çalışmasıdır. Örneğin, 1'i 3'e bölerseniz 1/3 elde edeceğinizi biliyoruz, ancak bu ikili olarak saklanamaz, bu nedenle sistem çok yakın tahminler oluşturmak üzere tasarlanmıştır. Son derece verimli ve hata o kadar küçük ki genellikle alakasız, ama en azından Swift'in neden karıştırmamıza `Int`ve `Double`kazara izin vermediğini biliyorsun!

---
# Booleans ile True/False nasıl saklayabilirim?

Şimdiye kadar dizilere, tamsayılara ve ondalık sayılara baktık, ancak aynı anda ortaya çıkan dördüncü bir veri türü daha var: Boolean adı verilen ve doğru ya da yanlışı saklayan çok basit bir tür. Merak ediyorsanız Boolean'lar, mantık hakkında araştırma yapmak ve yazmak için çok zaman harcayan İngiliz matematikçi George Boole'un adını almıştır.

Boolean'ların gizlice girdiğini söylüyorum çünkü onları zaten birkaç kez gördünüz:

```swift
let filename = "paris.jpg"
print(filename.hasSuffix(".jpg"))

let number = 120
print(number.isMultiple(of: 3))
```

Her ikisi `hasSuffix()`de `isMultiple(of:)`kontrollerine göre yeni bir değer döndürür: dizede sonek vardır veya yoktur ve 120, 3'ün katıdır veya değildir. Her iki yerde de her zaman basit bir doğru veya yanlış yanıtı vardır, Boolean'lar burada devreye girer - sadece onu saklarlar, başka bir şey saklamazlar.

Bir Boole değeri oluşturmak, diğer veri türlerini oluşturmak gibidir, yalnızca true veya false şeklinde bir başlangıç ​​değeri atamanız gerekir, bunun gibi:

```swift
let goodDogs = true
let gameOver = false
```

Sonunda doğru veya yanlış olduğu sürece, başka bir koddan bir Boolean'ın başlangıç ​​değerini de atayabilirsiniz:

```swift
let isMultiple = 120.isMultiple(of: 3)
```

`+`Diğer veri türlerinden farklı olarak, Boolean'lar ve gibi aritmetik işleçlere sahip değildir `-`- sonuçta, true + true neye eşit olur? Ancak, Boolean'ların "değil" anlamına gelen bir özel işleci vardır `!`. Bu, bir Boole değerini doğrudan yanlışa veya yanlıştan doğruya çevirir.

Örneğin, bir Boole değerini şu şekilde çevirebiliriz:

```swift
var isAuthenticated = false
isAuthenticated = !isAuthenticated
print(isAuthenticated)
isAuthenticated = !isAuthenticated
print(isAuthenticated)
```

Bu, çalıştığında önce "doğru" sonra "yanlış" yazacaktır, çünkü yanlış olarak başladı ve onu yanlış _değil_`isAuthenticated` olarak ayarladık , ki bu doğruydu, sonra tekrar yanlışa dönmesi için ters çevirin.

Boolean'lar yararlı olabilecek biraz ekstra işlevselliğe sahiptir _._ Özellikle, bir Boolean'ı çağırırsanız, `toggle()`true değerini false'a ve false değerini true'ya çevirir. Bunu denemek için, `gameOver`bir değişken oluşturmayı ve şu şekilde değiştirmeyi deneyin:

```swift
var gameOver = false
print(gameOver)

gameOver.toggle()
print(gameOver)
```

Bu önce false yazdıracak, ardından çağrıldıktan sonra `toggle()`true yazdıracaktır. Evet, bu biraz daha az kod kullanmakla aynı şeydir `!`, ancak karmaşık kodlarla uğraşırken şaşırtıcı derecede kullanışlıdır!

---
# Stringleri nasıl birleştirirsiniz?

Swift bize dizeleri birleştirmek için iki yol sunuyor: kullanarak bunları birleştirmek `+`ve herhangi bir türdeki değişkenleri doğrudan dizelerin içine yerleştirebilen _dize enterpolasyonu adı verilen özel bir teknik._

İlk olarak, dizeleri birleştirmek için kullanmak olan daha kolay seçenekle başlayalım `+`: iki diziniz olduğunda, bunları kullanarak yeni bir dizede birleştirebilirsiniz `+`, bunun gibi:

```swift
let firstPart = "Hello, "
let secondPart = "world!"
let greeting = firstPart + secondPart
```

Aşağıdakileri yapmanız gerekiyorsa bunu birçok kez yapabilirsiniz:

```swift
let people = "Haters"
let action = "hate"
let lyric = people + " gonna " + action
print(lyric)
```

Bu çalıştığında, "Nefret edenler nefret edecek" yazacak - evet, Taylor Swift'in büyük bir hayranıyım ve bence onun sözleri, Swift programlama hakkında bir eğitim için doğal bir uyum sağlıyor!

İki diziyi birleştirmek için nasıl kullandığımıza dikkat edin `+`, ancak ne zaman kullandık `Int`ve `Double`sayıları bir araya topladık? _Buna operatörün aşırı yüklenmesi_ denir - `+`nasıl kullanıldığına bağlı olarak bir operatörün farklı anlamlara gelme yeteneği . `+=`Dizeler için, bir dizeyi doğrudan diğerine ekleyen için de geçerlidir .

Bu teknik küçük şeyler için harika çalışıyor, ancak bunu çok fazla yapmak istemezsiniz. Görüyorsunuz, Swift iki dizginin onu kullanarak birleştirildiğini her gördüğünde, `+`devam etmeden önce bunlardan yeni bir dizi yapmak zorunda kalıyor ve eğer birleştirilen çok şey varsa, bu oldukça israf.

Örneğin şunu düşünün:

```swift
let luggageCode = "1" + "2" + "3" + "4" + "5"
```

Swift, tüm bu dizeleri tek seferde birleştiremez. Bunun yerine, "12"yi oluşturmak için ilk ikiye katılacak, ardından "123"ü oluşturmak için "12" ve "3"ü birleştirecek, ardından "1234"ü oluşturmak için "123" ve "4"ü birleştirecek ve son olarak "1234"ü oluşturacaktır. ve "5" "12345" yapmak için - kod bittiğinde nihai olarak kullanılmasalar bile "12", "123" ve "1234" tutmak için geçici dizeler yapar.

Swift'in _string interpolation_ adlı daha iyi bir çözümü var ve diğer dizgilerden, aynı zamanda tamsayılardan, ondalık sayılardan ve daha fazlasından verimli bir şekilde dizeler oluşturmamıza izin veriyor.

Hatırlarsanız, daha önce önlerinde ters eğik çizgi olduğu sürece dizelerin içine çift tırnak ekleyebileceğinizi söylemiştim, böylece Swift onlara özel davranması gerektiğini bilir:

```swift
let quote = "Then he tapped a sign saying \"Believe\" and walked away."
```

Dize enterpolasyonunda çok benzer bir şey kullanılır: dizenizin içine bir ters eğik çizgi yazarsınız, ardından bir değişkenin veya sabitin adını parantez içine alırsınız.

Örneğin, bir dizi sabiti ve bir tamsayı sabiti oluşturabilir, ardından bunları yeni bir dizide birleştirebiliriz:

```swift
let name = "Taylor"
let age = 26
let message = "Hello, my name is \(name) and I'm \(age) years old."
print(message)
```

Bu kod çalıştığında, "Merhaba, benim adım Taylor ve 26 yaşındayım" yazacaktır.

Dize enterpolasyonu, dizeleri birer birer birleştirmek için kullanmaktan çok daha etkilidir `+`, ancak başka bir önemli yararı daha vardır: tamsayıları, ondalık sayıları ve daha fazlasını fazladan çalışma yapmadan çekebilirsiniz.

Görüyorsunuz, kullanmak, `+`dizelere dizeler, tamsayılara tamsayılar ve ondalık sayılara ondalık sayılar eklememize izin verir, ancak dizelere tamsayılar eklememize izin _vermez ._ Bu nedenle, bu tür bir koda izin verilmez:

```swift
let number = 11
let missionMessage = "Apollo " + number + " landed on the moon."
```

İsterseniz, Swift'den sayıyı bir dizge gibi ele almasını isteyebilirsiniz, _şöyle_ :

```swift
let missionMessage = "Apollo " + String(number) + " landed on the moon."
```

Dize enterpolasyonunu kullanmak hem daha hızlı hem de okunması daha kolaydır:

```swift
let missionMessage = "Apollo \(number) landed on the moon."
```

**İpucu:** İsterseniz dize enterpolasyonunun içine hesaplamalar koyabilirsiniz. Örneğin, bu "5 x 5, 25'tir" yazdıracaktır:

```swift
print("5 x 5 is \(5 * 5)")
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

# Özet: Basit veriler

Önceki bölümlerde verilerin temelleri hakkında çok şey ele aldık, o yüzden özetleyelim:

-   `let`Swift kullanarak sabitler ve kullanarak değişkenler oluşturmamıza izin verir `var`.
-   Bir değeri değiştirmeyi düşünmüyorsanız, `let`Swift'in hatalardan kaçınmanıza yardımcı olabilmesi için kullandığınızdan emin olun.
-   Swift'in dizeleri, kısa dizilerden tüm romanlara kadar metin içerir. Emoji ve herhangi bir dünya diliyle harika çalışırlar ve `count`ve gibi yararlı işlevlere sahiptirler `uppercased()`.
-   Dizeleri, başında ve sonunda çift tırnak kullanarak oluşturursunuz, ancak dizenizin birkaç satırdan geçmesini istiyorsanız, başında ve sonunda üç çift tırnak kullanmanız gerekir.
-   Swift, tam sayılarını _tamsayı_ olarak adlandırır ve bunlar pozitif veya negatif olabilir. Ayrıca, `isMultiple(of:)`.
-   Swift'de ondalık sayılar `Double`, çift uzunluktaki kayan noktalı sayının kısaltması olarak adlandırılır. Bu, gerektiğinde çok büyük sayıları tutabilecekleri anlamına gelir, ancak aynı zamanda %100 doğru değildirler; parayla uğraşırken olduğu gibi %100 kesinlik gereken durumlarda bunları kullanmamalısınız.
-   Değişkenleri doğrudan değiştiren özel bileşik atama işleçlerinin yanı sıra `+`, , ve gibi birçok yerleşik aritmetik işleç vardır `-`.`*``/``+=`
-   `!`Operatör kullanılarak veya çağrılarak ters çevrilebilen bir Boole değeri kullanarak basit bir doğru veya yanlış durumu temsil edebilirsiniz `toggle()`.
-   Dize enterpolasyonu, sabitleri ve değişkenleri dizelerimize akıcı ve verimli bir şekilde yerleştirmemizi sağlar.

Çok fazla, değil mi? Ve sorun değil - uygulamaları oluştururken o listedeki her şeyi tekrar tekrar kullanacaksınız, ta ki sonunda buraya geri dönmenize gerek kalmadan her şeyi anlayana kadar.

### eng

We’ve covered a lot about the basics of data in the previous chapters, so let’s recap:

-   Swift lets us create constants using `let`, and variables using `var`.
-   If you don’t intend to change a value, make sure you use `let` so that Swift can help you avoid mistakes.
-   Swift’s strings contain text, from short strings up to whole novels. They work great with emoji and any world language, and have helpful functionality such as `count` and `uppercased()`.
-   You create strings by using double quotes at the start and end, but if you want your string to go over several lines you need to use three double quotes at the start and end.
-   Swift calls its whole numbers _integers_, and they can be positive or negative. They also have helpful functionality, such as `isMultiple(of:)`.
-   In Swift decimal numbers are called `Double`, short for double-length floating-point number. That means they can hold very large numbers if needed, but they also aren’t 100% accurate – you shouldn’t use them when 100% precision is required, such as when dealing with money.
-   There are lots of built-in arithmetic operators, such as `+`, `-`, `*`, and `/`, along with the special compound assignment operators such as `+=` that modify variables directly.
-   You can represent a simple true or false state using a Boolean, which can be flipped using the `!`operator or by calling `toggle()`.
-   String interpolation lets us place constants and variables into our strings in a streamlined, efficient way.

It’s a lot, right? And that’s okay – you’ll be using everything from that list time and time again as you build apps, until eventually you’ll understand it all without needing to refer back here.