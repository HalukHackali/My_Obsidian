
#swift #yazılım 

### <mark style="background: #FFF3A3A6;"> Birden çok koşul nasıl kontrol edilir?</mark>

Kullandığımızda, `if`Swift'e değerlendirildikten sonra doğru ya da yanlış olacak bir tür koşul sağlamalıyız. Birkaç farklı değeri kontrol etmek istiyorsanız, bunları şu şekilde arka arkaya yerleştirebilirsiniz:

```swift
let age = 16

if age >= 18 {
    print("You can vote in the next election.")
}

if age < 18 {
    print("Sorry, you're too young to vote.")
}
```

Ancak, düşünürseniz bu çok verimli değil: iki koşulumuz birbirini dışlıyor, çünkü eğer biri 18'den büyük veya ona eşitse (ilk koşul), o zaman 18'den (ikinci koşul) küçük olamaz ve tersi de doğrudur. Swift'e ihtiyaç duyulmayan işleri yaptırıyoruz.

`else`Bu durumda, Swift bize kodumuza bir blok eklememize izin veren daha gelişmiş bir koşul sağlar - koşul doğru _değilse_ çalıştırılacak bazı kodlar .

Bunu kullanarak `else`önceki kodumuzu şu şekilde yeniden yazabiliriz:

```swift
let age = 16

if age >= 18 {
    print("You can vote in the next election.")
} else {
    print("Sorry, you're too young to vote.")
}
```

Şimdi Swift'in yalnızca bir kez kontrol etmesi gerekiyor `age`: 18'den büyük veya ona eşitse ilk `print()`kod çalıştırılır, ancak 18'den _küçük_ herhangi bir değerse ikinci `print()`kod çalıştırılır.

Yani, şimdi durumumuz şöyle görünüyor:

```swift
if someCondition {
    print("This will run if the condition is true")
} else {
    print("This will run if the condition is false")
}
```

İlki başarısız olursa yeni bir kontrol yapmanızı sağlayan _daha_ da gelişmiş bir koşul vardır . `else if`İsterseniz bunlardan yalnızca birine sahip olabilir veya birden fazla olabilir `else if`ve hatta gerekirse `else if`bir ile birleştirebilirsiniz. `else`Ancak, yalnızca bir tanesine sahip olabilirsiniz `else`, çünkü bu, "diğer tüm koşullar yanlışsa" anlamına gelir.

İşte böyle görünüyor:

```swift
let a = false
let b = true

if a {
    print("Code to run if a is true")
} else if b {
    print("Code to run if a is false but b is true")
} else {
    print("Code to run if both a and b are false")
}
```

İsterseniz daha fazla koşul eklemeye devam edebilirsiniz `else if`, ancak kodunuzun çok karmaşık hale gelmemesine dikkat edin!

`else`Daha gelişmiş koşullar oluşturmak için ve'yi kullanmanın yanı sıra `else if`, birden fazla şeyi de kontrol edebilirsiniz. Örneğin, “bugünkü sıcaklık 20 derecenin üzerinde ve 30'un altındaysa mesaj yazdırın” demek isteyebiliriz.

Bunun iki koşulu var, dolayısıyla şunu yazabiliriz:

```swift
let temp = 25

if temp > 20 {
    if temp < 30 {
        print("It's a nice day.")
    }
}
```

Bu yeterince işe yarasa da, Swift daha kısa bir alternatif sunuyor: iki koşulu birleştirmek için kullanabiliriz `&&`ve tüm koşul ancak koşulun içindeki iki kısım doğruysa doğru olacaktır.

Böylece kodumuzu şu şekilde değiştirebiliriz:

```swift
if temp > 20 && temp < 30 {
    print("It's a nice day.")
}
```

“ve” olarak okumalısınız `&&`, yani tüm koşullarımız “temp 20'den büyükse ve temp 30'dan küçükse bir mesaj yazdırın” şeklindedir. _Mantıksal operatör_ olarak adlandırılır çünkü Boolean'ları yeni bir Boolean oluşturmak için birleştirir.

`&&`"veya" anlamına gelen iki boru simgesi olan bir karşılığı vardır `||`. Halbuki `&&`, yalnızca her iki alt koşul da doğruysa bir koşulu doğru yapar, alt koşullardan _biri_ doğruysa `||`bir koşulu doğru yapar .

Örneğin, bir kullanıcı en az 18 yaşındaysa oyun satın alabilir veya 18 yaşından küçükse bir ebeveyninden izin almalıdır diyebiliriz. `||`Bunu şöyle kullanarak yazabiliriz :

```swift
let userAge = 14
let hasParentalConsent = true

if userAge >= 18 || hasParentalConsent == true {
    print("You can buy the game")
}
```

Bu, "Oyunu satın alabilirsiniz" yazdıracaktır, çünkü koşulumuzun ilk yarısı başarısız olsa da - kullanıcı en az 18 yaşında _değildir_ - ikinci yarısı geçer, çünkü ebeveyn izni vardır _._

Bir koşulda kullanmanın `== true`kaldırılabileceğini unutmayın, çünkü zaten bir Boole değerini kontrol ediyoruz. Yani, bunun yerine şunu yazabiliriz:

```swift
if userAge >= 18 || hasParentalConsent {
    print("You can buy the game")
}
```

Birden çok koşulu kontrol etmeyi bitirmek için, , `if`, ve tümünü aynı anda birleştiren ve hatta sıralamaların koşullara nasıl uyduğunu gösteren daha karmaşık bir örnek deneyelim .`else if``else``||`

Bu örnekte, adında beş durum içeren bir sıralama oluşturacağız `TransportOption`: uçak, helikopter, bisiklet, araba ve scooter. Daha sonra bir sabite örnek bir değer atayacağız ve bazı kontroller yapacağız:

-   Uçakla veya helikopterle bir yere gidiyorsak “Haydi uçalım!”
-   Bisikletle gidiyorsak “Umarım bisiklet yolu vardır…” yazdırırız.
-   Arabayla gidiyorsak, “Trafikte takılma zamanı” yazdıracağız.
-   Aksi takdirde “Şimdi bir scooter kiralayacağım!” Yazacağız.

İşte bunun için kod:

```swift
enum TransportOption {
    case airplane, helicopter, bicycle, car, scooter
}

let transport = TransportOption.airplane

if transport == .airplane || transport == .helicopter {
    print("Let's fly!")
} else if transport == .bicycle {
    print("I hope there's a bike path…")
} else if transport == .car {
    print("Time to get stuck in traffic.")
} else {
    print("I'm going to hire a scooter now!")
}
```

Bu kodun birkaç bölümünü seçmek istiyorum:

1.  için değeri ayarladığımızda, `transport`atıfta bulunduğumuzu açıkça belirtmemiz gerekir `TransportOption.airplane`. `.airplane`Swift sıralamayı kastettiğimizi anlamadığı için öylece yazamayız `TransportOption`.
2.  Bu bir kez gerçekleştiğinde, `TransportOption`artık yazmamıza gerek yok çünkü Swift `transport`bir çeşit olması gerektiğini biliyor `TransportOption`. `.airplane`Böylece, yerine eşit olup olmadığını kontrol edebiliriz `TransportOption.airplane`.
3.  Eşit olup olmadığını _kontrol_`||` etmek için kullanılan kod ve bunlardan _herhangi biri_ doğruysa , koşul doğrudur ve “Hadi uçalım!” yazdırılır.`transport``.airplane` `.helicopter`
4.  İlk koşul başarısız olursa – taşıma modu `.airplane`veya değilse `.helicopter`– o zaman ikinci koşul çalıştırılır: taşıma modu mu `.bicycle`? Eğer öyleyse, “Umarım bir bisiklet yolu vardır…” yazdırılır.
5.  Bisikletle de gitmiyorsak araba ile gidip gitmediğimize bakarız. Biz ise, “Trafikte takılma zamanı.” yazdırılır.
6.  Son olarak, önceki tüm koşullar başarısız olursa, `else`blok çalıştırılır ve bu, scooter ile gidiyoruz anlamına gelir.