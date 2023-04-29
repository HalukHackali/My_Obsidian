#swift #yazılım 

Şimdiye kadar tam sayılarla, string'lerle, kesirli ve ondalıklı sayılarla, Boolean'larla, dizilerle, sözlüklerle, struct'larla ve class'larla karşılaştınız. Ama Swift dilinde geniş bir şekilde kullanılan bir veri tipi daha var ve closure olarak anılıyor. Bunlar karmaşıktır, ama aynı zamanda güçlü ve anlamlıdırlar öyle ki, Cocoa Touch içinde her tarafta yaygın bir şekilde kullanılırlar. O yüzden, onları anlamadan daha fazla ileriye gidemezsiniz.

Bir closure, kod içeren bir değişken olarak düşünülebilir. Yani 0 veya 500 tam sayısının tutulduğu yerde, bir closure Swift kodu satırları tutabilir. Bir fonksiyona göre farklıdır yine de, çünkü closure'lar kendi haklarına sahip veri tipleridirler: Bir closure'u parametre olarak geçebilir veya bir özellik olarak saklayabilirsiniz. Closure'lar aynı zamanda oluşturuldukları ortamı da yakalarlar. Bu, içlerinde kullanılan değerlerin bir kopyasını aldıkları anlamına gelir.

Kendi closure'unuzu tasarlamanız _asla_ gerekmez, o yüzden takip etmesini oldukça zor bulsanız da çekinmeyiniz. Zaten, hem Cocoa hem de Cocoa Touch ihtiyaçlarını karşılamak için sizden sık sık closure'lar yazmanızı isteyecek. O yüzden en azından nasıl çalıştıklarını bilmeniz gerekli. Şimdi ilk olarak bir Cocoa Touch örneği ele alalım:

```swift
let vw = UIView()

UIView.animate(withDuration: 0.5, animations: {
    vw.alpha = 0
})
```

`UIView`, kullanıcı arayüzü taşıyıcısının en temel türünü sunan UIKit içindeki bir iOS veri tipidir. Ne işe yaradığıyla şimdilik ilgilenmeyin, bütün olay temel kullanıcı arayüzü bileşeni olması. `UIView`, `animate()` adlı bir metoda sahip ve bununla animasyon kullanarak arayüzünüzü değiştirebilirsiniz; neyin değişeceğini ve ne kadar süreceğini siz tanımlarsınız, geri kalanını da Coca Touch halleder.

Bu kod içinde `animate()` metodu iki parametre alıyor: Animasyonun biteceği saniye ve animasyon parçası olarak çalıştırılacak olan kodu içeren bir closure. İlk parametreyi yarım saniye olarak tanımladım ve ikincisi ile de UIKit'in view'ün "tamamen saydam" anlamına gelen alfa 0'a (bu saydamlıktır) ayarlamasını istedim.

Bu metod bir closure kullanmayı gerektiriyor, çünkü UIKit başlayacak animasyon için hazırlanacak her tür işi yapmak zorunda. Böylece olan şey, UIKit süslü parantez içindeki (işte bu bizim closure'muz) kodun kopyasını alıyor, bir yerde depoluyor, tüm hazırlıkları yapıyor, ardından da hazır olduğunda kodumuzu çalıştırıyor. Eğer kodumuzu doğrudan çalıştırsaydık, bu mümkün olmazdı.

Yukarıdaki kod aynı zamanda closure'ların ortamlarını nasıl yakaladıklarını da gösteriyor: `vw`adında closure'un dışında bir sabit tanımladım, sonra onu içerisinde kullandım. Swift bunu tespit etti ve verinin closure'un içinde de kullanılabilir olmasını sağladı.

Swift'in, bir closure'un ortamı otomatik olarak yakalama sistemi çok yardımcıdır, ama nadiren de olsa sizi şaşırtır: Eğer bir A nesnesi özellik olarak bir closure tutuyorsa, bu özellik aynı zamanda A nesnesine gönderir. Bu da güçlü referans döngüsü adında bir şeye sahip olmanız demektir ki, kullanıcıları mutsuz edersiniz. Bu, şu anda bilmeniz gerekenden büyük ölçüde daha gelişmiş bir konudur. O yüzden şimdilik üzerinde fazla durmayın.

## Trailing closures (Takip eden closure'lar)

Closure'lar çok sık bir şekilde kullanıldığı için, Swift kodunuzu daha kolay okunabilir hale getirmek için sözdizimsel bir güzellik uygulayabilir. Kural şöyle: Bir metodun son parametresi bir closure alıyorsa, bu parametreyi silebilir ve yerine süslü parantezler içindeki kodu sağlayabilirsin. Örneğin daha önceki kodu şu şekilde dönüştürebiliriz:

```swift
let vw = UIView()

UIView.animate(withDuration: 0.5) {
    vw.alpha = 0
}
```

Bu, kodunuzu daha kısa ve okuması daha kolay hale getirir. O yüzden sözdizimsel şekli –takip eden closure sözdizimi olarak bilinir– tercih edilir.

---

# Closures nasıl oluşturulur ve kullanılır?

Fonksiyonlar Swift'te güçlü şeylerdir. Evet, onları nasıl arayabileceğinizi, değerleri iletebileceğinizi ve veri döndürebileceğinizi gördünüz, ancak bunları değişkenlere atayabilir, işlevlere işlevler iletebilir ve hatta işlevlerden işlevler döndürebilirsiniz.

Örneğin:

```swift
func greetUser() {
    print("Hi there!")
}

greetUser()

var greetCopy = greetUser
greetCopy()
```

Bu, önemsiz bir işlev oluşturur ve onu çağırır, ancak daha sonra bu işlevin bir _kopyasını_ oluşturur ve kopyayı çağırır. Sonuç olarak, aynı mesajı iki kez yazdıracaktır.

**Önemli:** Bir işlevi kopyalarken, ondan sonra parantez yazmazsınız - bu `var greetCopy = greetUser`ve değil `var greetCopy = greetUser()`. Parantezleri oraya koyarsanız, işlevi _çağırıyor_ve dönüş değerini başka bir şeye atamış oluyorsunuz.

_Ancak, ayrı bir işlev oluşturmayı atlamak_ ve işlevi doğrudan bir sabite veya değişkene atamak isterseniz ne olur ? Görünüşe göre bunu da yapabilirsin:

```swift
let sayHello = {
    print("Hi there!")
}

sayHello()
```

Swift buna görkemli bir ad _kapatma ifadesi_ veriyor , bu da bir kapatma oluşturduğumuzu söylemenin süslü bir yolu - etrafta dolaşabileceğimiz ve istediğimiz zaman arayabileceğimiz bir kod yığını. Bunun bir adı yoktur, ancak bunun dışında etkin bir şekilde hiçbir parametre almayan ve bir değer döndürmeyen bir işlevdir.

Kapatmanın parametreleri kabul etmesini istiyorsanız, bunların özel bir şekilde yazılması gerekir. Görüyorsunuz, kapatma parantezlerle başlar ve biter, bu da parametreleri kontrol etmek veya değer döndürmek için bu parantezlerin dışına kod koyamayacağımız anlamına gelir. _Yani, Swift'in temiz bir geçici çözümü var: Aynı bilgiyi parantez içine_ koyabiliriz , şöyle:

```swift
let sayHello = { (name: String) -> String in
    "Hi \(name)!"
}
```

Oraya fazladan bir anahtar kelime ekledim - fark ettiniz mi? Bu anahtar kelimedir `in`ve doğrudan kapatmanın parametrelerinden ve dönüş türünden sonra gelir. Yine, düzenli bir işlevde parametreler ve dönüş tipi parantezlerin _dışına_ çıkar , ancak bunu kapatmalarla yapamayız. Bu nedenle, `in`parametrelerin sonunu ve dönüş tipini işaretlemek için kullanılır - bundan sonraki her şey, kapatmanın kendisinin gövdesidir. Bunun bir nedeni var ve bunu yakında kendiniz de göreceksiniz.

Bu arada, daha temel bir sorunuz olabilir: "Bunlara neden ihtiyacım olsun ki?" Biliyorum, kapanışlar çok belirsiz görünüyor. _Daha da kötüsü, anlaşılmaz ve_ karmaşık görünüyorlar - pek çok insan, onlarla ilk karşılaştıklarında gerçekten kapanışlarla mücadele ediyor, çünkü bunlar karmaşık canavarlar ve hiçbir zaman yararlı olmayacak gibi görünüyorlar.

Ancak, göreceğiniz gibi bu, Swift'te ve SwiftUI'nin hemen hemen _her yerinde_ _yaygın olarak kullanılıyor._ _Cidden, onları yazdığınız her SwiftUI uygulamasında, bazen yüzlerce kez kullanacaksınız - belki yukarıda gördüğünüz biçimde olmayabilir, ancak onu çok_ kullanacaksınız .

_Kapanışların neden bu kadar yararlı olduğu hakkında bir fikir edinmek için, önce sizi işlev türleriyle_tanıştırmak istiyorum . Tamsayıların `Int`ve ondalık sayıların , vb. tipine sahip olduğunu gördünüz `Double`ve şimdi fonksiyonların da nasıl tipleri olduğunu düşünmenizi istiyorum.

Daha önce yazdığımız fonksiyonu ele alalım `greetUser()`: parametre kabul etmez, değer döndürmez ve hata vermez. Bunu bir tip ek açıklaması olarak yazacak olsaydık `greetCopy`, şunu yazardık:

```swift
var greetCopy: () -> Void = greetUser
```

Bunu parçalayalım…

1.  Boş parantezler, parametre almayan bir işlevi işaretler.
2.  Ok, bir işlev oluştururken tam olarak ne anlama geldiğini ifade eder: işlevin dönüş türünü bildirmek üzereyiz.
3.  `Void`"hiçbir şey" anlamına gelir - bu işlev hiçbir şey döndürmez. Bazen bunun şeklinde yazıldığını görebilirsiniz `()`, ancak boş parametre listesiyle karıştırılabileceği için genellikle bundan kaçınırız.

Her işlevin türü, aldığı ve geri gönderdiği verilere bağlıdır. Kulağa basit gelebilir, ancak önemli bir noktayı gizler: aldığı verilerin _adları_ , işlevin türünün bir parçası _değildir ._

Bunu biraz daha kodla gösterebiliriz:

```swift
func getUserData(for id: Int) -> String {
    if id == 1989 {
        return "Taylor Swift"
    } else {
        return "Anonymous"
    }
}

let data: (Int) -> String = getUserData
let user = data(1989)
print(user)
```

Bu, yeterince kolay başlar: bir tamsayı kabul eden ve bir dize döndüren bir işlevdir. _Ancak fonksiyonun bir kopyasını_ aldığımızda, fonksiyonun türü harici parametre adını içermez `for`, bu nedenle kopya çağrıldığında `data(1989)`yerine kullanırız `data(for: 1989)`.

Kurnazca aynı kural tüm kapatmalar için geçerlidir – aslında daha önce yazdığımız kapatmayı _kullanmadığımı_ fark etmişsinizdir `sayHello`ve bunun nedeni sizi çağrı sitesinde bir parametre adı eksikliğini sorgulamak istemememdir. Şimdi arayalım:

```swift
sayHello("Taylor")
```

Bu, tıpkı işlevleri kopyaladığımızda olduğu gibi parametre adı kullanmaz. Yani, yine: harici parametre adları, yalnızca bir işlevi doğrudan çağırdığımızda önemlidir, bir kapatma oluşturduğumuzda veya önce işlevin bir kopyasını aldığımızda değil.

Muhtemelen hala tüm bunların neden önemli olduğunu merak ediyorsunuz ve her şey netleşmek üzere. `sorted()`Öğelerini sıralamak için bir dizi ile kullanabileceğimizi söylediğimi hatırlıyor musun ?

Bunun anlamı şöyle bir kod yazabiliriz:

```swift
let team = ["Gloria", "Suzanne", "Piper", "Tiffany", "Tasha"]
let sortedTeam = team.sorted()
print(sortedTeam)
```

Bu gerçekten harika, ama ya bu sıralamayı _kontrol etmek isteseydik – ya her zaman bir kişinin takım kaptanı olduğu için birinci olmasını ve geri kalanının alfabetik olarak sıralanmasını isteseydik?_

Aslında, `sorted()`tam olarak bunu kontrol etmek için özel bir sıralama işlevine geçmemize izin veriyor. Bu işlev iki dizgiyi kabul etmeli ve birinci dizge ikinciden önce sıralanacaksa true, birinci dizge ikinciden _sonra_ sıralanacaksa false döndürmelidir .

Suzanne kaptan olsaydı, fonksiyon şöyle görünürdü:

```swift
func captainFirstSorted(name1: String, name2: String) -> Bool {
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}
```

Bu nedenle, ilk ad Suzanne ise, `name1`önce sıralanacak şekilde true döndürün `name2`. Öte yandan, Suzanne ise , _sonra_ sıralanması `name2`için false döndürün . _İsimlerden hiçbiri_ Suzanne değilse , normal bir alfabetik sıralama yapmak için kullanın .`name1` `name2``<`

Dediğim gibi, `sorted()`özel bir sıralama düzeni oluşturmak için bir işlev iletilebilir ve bu işlev a) iki dizeyi kabul ettiği ve b) bir Boolean döndürdüğü sürece `sorted()`onu kullanabilir.

Yeni fonksiyonumuzun yaptığı da tam olarak bu `captainFirstSorted()`, yani onu hemen kullanabiliriz:

```swift
let captainFirstTeam = team.sorted(by: captainFirstSorted)
print(captainFirstTeam)
```

`["Suzanne", "Gloria", "Piper", "Tasha", "Tiffany"]`Bu çalıştığında , tam olarak istediğimiz gibi yazdıracaktır .

Şimdi görünüşte çok farklı iki şeyi ele aldık. İlk olarak, sabitler ve değişkenler içinde saklayarak anonim işlevler olarak kapanışlar oluşturabiliriz:

```swift
let sayHello = {
    print("Hi there!")
}

sayHello()
```

Ayrıca, işlevleri diğer işlevlere de geçirebiliriz, tıpkı şuna geçtiğimiz `captainFirstSorted()`gibi `sorted()`:

```swift
let captainFirstTeam = team.sorted(by: captainFirstSorted)
```

Kapanışların gücü, bu ikisini bir araya getirebilmemizdedir: `sorted()`iki dizgiyi kabul edecek ve bir Boole değeri döndürecek bir işlev istiyor ve bu işlevin resmi olarak kullanılarak mı oluşturulduğu yoksa bir `func`kapatma kullanılarak mı sağlandığı umurunda değil.

Böylece, tekrar arayabiliriz `sorted()`, ancak işlevi iletmek yerine `captainFirstTeam()`, bunun yerine yeni bir kapatma başlatın: açık bir parantez yazın, parametrelerini listeleyin ve türü döndürün, yazın ve `in`ardından standart işlev kodumuzu koyun.

**Bu ilk başta beyninize zarar verecek.** Kapanışları anlayacak kadar akıllı olmadığın veya Swift programlama için uygun olmadığın için değil, sadece kapanışlar _gerçekten zor_ . Endişelenmeyin - bunu kolaylaştırmanın yollarına bakacağız!

`sorted()`Tamam, bir kapatma kullanarak çağıran yeni bir kod yazalım :

```swift
let captainFirstTeam = team.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
})
```

Bu aynı anda büyük bir sözdizimi yığını ve yine bunun daha kolay olacağını söylemek istiyorum – bir sonraki bölümde, neler olup bittiğini daha kolay görebilmek için kod miktarını azaltmanın yollarına bakacağız.

Ama önce orada neler olduğunu özetlemek istiyorum:

1.  İşlevi daha önce olduğu gibi çağırıyoruz `sorted()`.
2.  Bir fonksiyonda geçmek yerine, bir kapanışı geçiyoruz – sonraki açılış parantezinden `by:`son satırdaki kapanış parantezine kadar her şey kapanışın bir parçasıdır.
3.  Doğrudan kapatmanın içinde listelediğimiz iki parametre `sorted()`bize geçecektir, bunlar iki dizgedir. Ayrıca kapanışımızın bir Boole döndüreceğini söylüyoruz, ardından kapanış kodunun başlangıcını kullanarak işaretliyoruz `in`.
4.  Diğer her şey sadece normal fonksiyon kodudur.

Yine, orada çok fazla sözdizimi var ve baş ağrınızın yaklaştığını hissederseniz sizi suçlamam ama umarım kapatmanın faydasını en azından biraz görebilirsiniz: nasıl yapılacağını ayarlamak için özel kod girmemize izin ver gibi `sorted()`işlevler çalışırlar ve bunu doğrudan yaparlar - yalnızca bu kullanım için yeni bir işlev yazmamıza gerek yoktur.

Artık kapanışların ne olduğunu anladınız, bakalım onları daha kolay okunabilir hale getirebilecek miyiz…

---

# Trailing Closures ve Shorthand Syntax nasıl kullanılır?

Swift'in kapanışlarla birlikte gelen sözdizimi miktarını azaltmak için birkaç hilesi var, ama önce kendimize sorunu hatırlatalım. İşte bir önceki bölümün sonunda elde ettiğimiz kod:

```swift
let team = ["Gloria", "Suzanne", "Piper", "Tiffany", "Tasha"]

let captainFirstTeam = team.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
})

print(captainFirstTeam)
```

Hatırlarsanız, `sorted()`özel sıralama yapmak için herhangi bir işlevi tek bir kuralla kabul edebilirsiniz: bu işlev, söz konusu diziden iki öğe kabul etmelidir (burada iki dize vardır) ve ilk dize olması gerekiyorsa bir Boolean kümesini true olarak döndürmelidir. saniyeden önce sıralanır.

Açık olmak gerekirse, işlev şu şekilde _davranmalıdır_ - hiçbir şey döndürmezse veya yalnızca bir dize kabul ederse, Swift kodumuzu oluşturmayı reddeder.

İyice düşünün: Bu kodda, sağladığımız işlev `sorted()`iki dize sağlamalı ve bir Boole döndürmelidir, öyleyse kapanışta neden kendimizi tekrar etmemiz gerekiyor?

Cevap: _yapmıyoruz_ . _Dize olmaları gerektiğinden_ iki parametremizin türlerini belirtmemize gerek yok ve bir Boolean olması _gerektiğinden_ bir dönüş türü belirtmemize gerek yok . Böylece kodu şu şekilde yeniden yazabiliriz:

```swift
let captainFirstTeam = team.sorted(by: { name1, name2 in
```

Bu, koddaki dağınıklığı zaten azalttı, ancak bir adım daha ileri gidebiliriz: bir işlev diğerini parametresi olarak kabul ettiğinde, tıpkı yaptığı gibi, `sorted()`Swift _sondaki kapanış sözdizimi_ adı verilen özel sözdizimine izin verir . Şuna benziyor:

```swift
let captainFirstTeam = team.sorted { name1, name2 in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}
```

Kapatmayı bir parametre olarak iletmek yerine, devam edip kapatmayı doğrudan başlatırız ve bunu yaparken `(by:`baştan ve sondaki bir kapatma parantezini kaldırırız. Umarız artık neden parametre listesini görebilir ve kapatmanın _içine_`in` girebilirsiniz , çünkü dışarıda olsalardı daha da tuhaf görünürdü!

_Swift'in kapanışları daha az karmaşık hale getirmesinin son bir yolu var: Swift, kestirme sözdizimini_kullanarak bizim için otomatik olarak parametre adları sağlayabilir . Bu sözdizimi ile artık yazmıyoruz bile `name1, name2 in`ve bunun yerine Swift'in bize sağladığı özel olarak adlandırılmış değerlere güveniyoruz: `$0`ve `$1`, sırasıyla birinci ve ikinci dizeler için.

Bu sözdizimini kullanarak kodumuz daha da kısalır:

```swift
let captainFirstTeam = team.sorted {
    if $0 == "Suzanne" {
        return true
    } else if $1 == "Suzanne" {
        return false
    }

    return $0 < $1
}
```

Bunu sona bıraktım çünkü diğerleri kadar net değil – bazı insanlar bu sözdizimini görüyor ve daha az net olduğu için ondan nefret ediyor ve sorun değil.

Şahsen ben burada _kullanmazdım_ çünkü her bir değeri bir kereden fazla kullanıyoruz, ama aramamız `sorted()`daha basit olsaydı – örneğin, sadece ters sıralama yapmak isteseydik – o zaman şunu yapardım:

```swift
let reverseTeam = team.sorted {
    return $0 > $1
}
```

Bu nedenle, `in`parametrelerin sonunu ve dönüş tipini işaretlemek için kullanılır - bundan sonraki her şey, kapatmanın kendisinin gövdesidir. Bunun bir nedeni var ve bunu yakında kendiniz de göreceksiniz.

`<`Orada karşılaştırmayı to'dan to'ya çevirdim, `>`böylece ters bir sıralama elde ettik, ama artık tek bir kod satırına indiğimize göre the'yi kaldırabilir `return`ve neredeyse sıfıra indirebiliriz:

```swift
let reverseTeam = team.sorted { $0 > $1 }
```

Steno sözdiziminin ne zaman kullanılacağı ve ne zaman kullanılmayacağına dair sabit kurallar yoktur, ancak yardımcı olması durumunda, aşağıdakilerden herhangi biri doğru olmadığı sürece steno sözdizimi kullanırım:

1.  Kapanış kodu uzun.
2.  `$0`ve arkadaşlar birden fazla kez kullanılır.
3.  Üç veya daha fazla parametre alırsınız (örn `$2`. , `$3`, vb.).

Kapatmaların gücü konusunda hala ikna olmadıysanız, iki örneğe daha göz atalım.

İlk olarak, `filter()`işlev, dizideki her öğe üzerinde bazı kodlar çalıştırmamıza izin verir ve işlev için doğru olan her öğeyi içeren yeni bir dizi geri gönderir. Böylece, adı T ile başlayan tüm takım oyuncularını şu şekilde bulabiliriz:

```swift
let tOnly = team.filter { $0.hasPrefix("T") }
print(tOnly)
```

Yazılacak `["Tiffany", "Tasha"]`, çünkü adı T ile başlayan tek iki ekip üyesi bunlar.

İkincisi, `map()`işlev, dizideki her öğeyi, seçtiğimiz bazı kodları kullanarak dönüştürmemize izin verir ve dönüştürülen tüm öğelerin yeni bir dizisini geri gönderir:

```swift
let uppercaseTeam = team.map { $0.uppercased() }
print(uppercaseTeam)
```

`["GLORIA", "SUZANNE", "PIPER", "TIFFANY", "TASHA"]`Bu , her adı büyük harfle yazdığı ve sonuçtan yeni bir dizi ürettiği için yazdıracaktır .

**İpucu:** ile çalışırken `map()`, döndürdüğünüz türün başladığınız türle aynı olması gerekmez; örneğin, bir tamsayı dizisini bir dizi dizisine dönüştürebilirsiniz.

Dediğim gibi, SwiftUI ile kapanışları _çok_ kullanacaksınız :

1.  Ekranda bir veri listesi oluşturduğunuzda, SwiftUI sizden listeden bir öğeyi kabul eden ve ekranda görüntüleyebileceği bir şeye dönüştüren bir işlev sağlamanızı isteyecektir.
2.  Bir düğme oluşturduğunuzda, SwiftUI sizden düğmeye basıldığında yürütülecek bir işlev ve düğmenin içeriğini oluşturmak için başka bir işlev sağlamanızı isteyecektir - bir resim veya bir metin vb.
3.  Sadece istiflenen metin parçalarını dikey olarak koymak bile bir kapatma kullanılarak yapılır.

Evet, SwiftUI bunu her yaptığında bireysel işlevler oluşturabilirsiniz, ancak bana güvenin: yapmayacaksınız. Kapatmalar bu tür kodları tamamen doğal hale getirir ve bence SwiftUI'nin bunları son derece basit, temiz kod üretmek için nasıl kullandığına şaşıracaksınız.