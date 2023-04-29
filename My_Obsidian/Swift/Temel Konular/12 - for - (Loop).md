#swift #yazılım 

###  <mark style="background: #FFF3A3A6;">Çalışmayı tekrarlamak için bir for döngüsü nasıl kullanılır?</mark>

Bilgisayarlar tekrarlayan işler yapmakta gerçekten harikalar ve Swift, bazı kodları sabit sayıda veya bir dizideki, sözlükteki veya kümedeki her öğe için bir kez tekrarlamayı kolaylaştırıyor.

Basit bir şeyle başlayalım: eğer bir dizge dizimiz varsa, her bir dizgiyi şu şekilde yazdırabiliriz:

```swift
let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift works great on \(os).")
}
```

Bu, içindeki tüm öğelerin üzerinden geçerek `platforms`onları birer birer içine yerleştirir `os`. Başka bir yerde yaratmadık `os`; bizim için döngünün bir parçası olarak yaratıldı ve yalnızca açılış ve kapanış parantezlerinin içinde kullanıma sunuldu.

Köşeli ayraçların içinde, dizideki her öğe için çalıştırmak istediğimiz kod bulunur, bu nedenle yukarıdaki kod, her döngü öğesi için bir tane olmak üzere dört satır yazdırır. Buraya önce “iOS” yazıp ardından arama yapıyor `print()`, ardından “macOS” yazıp arama yapıyor `print()`, ardından “tvOS” ve ardından “watchOS”.

İşlerin anlaşılmasını kolaylaştırmak için bu şeylere ortak adlar veriyoruz:

-   _Parantez içindeki koda döngü gövdesi_ diyoruz.
-   Döngü gövdesindeki bir döngüye _döngü yinelemesi_ diyoruz .
-   `os`Döngü _değişkeni_ diyoruz . Bu yalnızca döngü gövdesi içinde bulunur ve sonraki döngü yinelemesinde yeni bir değere değişir.

Adın özel olmadığını söylemeliyim `os`- onun yerine şunu yazabilirdik:

```swift
for name in platforms {
    print("Swift works great on \(name).")
}
```

Hatta bu:

```swift
for rubberChicken in platforms {
    print("Swift works great on \(rubberChicken).")
}
```

Kod yine tamamen aynı şekilde çalışacaktır.

Aslında, Xcode burada gerçekten akıllıdır: yazarsanız, `for plat`adlı bir dizi olduğunu fark eder `platforms`ve hepsini otomatik tamamlamayı önerir `for platform in platforms`- bunun çoğul olduğunu anlar `platforms`ve döngü değişkeni için tekil bir ad önerir. Xcode'un önerisinin göründüğünü gördüğünüzde, onu seçmek için Geri Dön'e basın.

Bir dizi (veya küme veya sözlük - sözdizimi aynıdır!) üzerinde döngü yapmak yerine, sabit bir sayı aralığında da döngü yapabilirsiniz. Örneğin, 1'den 12'ye kadar olan 5 çarpım tablosunu şu şekilde yazdırabiliriz:

```swift
for i in 1...12 {
    print("5 x \(i) is \(5 * i)")
}
```

Orada birkaç şey yeni, o yüzden durup inceleyelim:

-   `i`"Saydığınız sayı" için yaygın bir kodlama kuralı olan döngü değişkenini kullandım . İkinci bir sayı sayıyorsanız kullanırsınız `j`ve üçte bir sayıyorsanız kullanırsınız `k`, ancak dördüncü sayıyorsanız belki daha iyi değişken adları seçmelisiniz.
-   Parça `1...12`bir _aralıktır_ ve "1 ile 12 arasındaki tüm tamsayıların yanı sıra 1 ile 12'nin kendisi" anlamına gelir. Aralıklar, Swift'de kendi benzersiz veri türleridir.

Yani, bu döngü ilk çalıştığında `i`1 olacak, sonra 2, sonra 3, vb. olacak, 12'ye kadar, ardından döngü sona erecek.

_İç içe döngüler_ adı verilen döngülerin içine de döngüler koyabilirsiniz , bunun gibi:

```swift
for i in 1...12 {
    print("The \(i) times table:")

    for j in 1...12 {
        print("  \(j) x \(i) is \(j * i)")
    }

    print()
}
```

Bu, birkaç yeni şeyi daha gösteriyor, bu yüzden tekrar duralım ve daha yakından bakalım:

-   Artık iç içe bir döngü var: 1'den 12'ye kadar sayıyoruz ve buradaki her sayı için tekrar 1'den 12'ye kadar sayıyoruz.
-   `print()`Hiçbir metin veya değer iletilmeden kendi başına kullanmak , yeni bir satır başlatacaktır. Bu, çıktımızın ekranda daha güzel görünmesi için parçalanmasına yardımcı olur.

Böylece, bildiğinizi gördüğünüzde, hangi sayıda olursa olsun başlayan ve o sayıya kadar sayan ve bu sayıyı içeren `x...y`bir aralık oluşturur .`x``y`

Swift, son sayıya kadar sayılan ancak _hariç olan_ benzer ama farklı bir aralığa sahiptir : `..<`. Bu en iyi kodda görülür:

```swift
for i in 1...5 {
    print("Counting from 1 through 5: \(i)")
}

print()

for i in 1..<5 {
    print("Counting 1 up to 5: \(i)")
}
```

Bu çalıştığında, ilk döngüde 1, 2, 3, 4, 5 sayıları için, ikinci döngüde yalnızca 1, 2, 3 ve 4 sayıları için yazdıracaktır. Ben `1...5`"birden beşe" ve `1..<5`"birden beşe kadar" olarak telaffuz ediyorum ve Swift'in başka yerlerinde de benzer ifadeler göreceksiniz.

**İpucu:** `..<` 0'dan saydığımız ve genellikle dizideki öğe sayısına kadar saymak istediğimiz dizilerle çalışmak için gerçekten yararlıdır.

Döngülerle işimiz bitmeden `for`, bahsetmek istediğim bir şey daha var: Bazen bir aralığı kullanarak bazı kodları belirli sayıda çalıştırmak istersiniz, ancak aslında döngü değişkenini istemezsiniz – istemezsiniz. `i`veya `j`, çünkü kullanmazsınız.

Bu durumda, döngü değişkenini aşağıdaki gibi bir alt çizgi ile değiştirebilirsiniz:

```swift
var lyric = "Haters gonna"

for _ in 1...5 {
    lyric += " hate"
}

print(lyric)
```

(Evet, bu Shake It Off'tan Swift dilinde yazılmış bir Taylor Swift sözü.)

---

Siz bu tümceyi okurken harcadığınız zaman içerisinde, bilgisayarlar milyonlarca kez sıkıcı görevleri yapmakta harikalar. Sıra kod içindeki görevlerin tekrarına geldiğinde, istersen kodu defalarca kopyala yapıştır yapabilirsin; veya, bir durum doğru olduğu sürece tekrar edecek olan kod blokları olan basit programcılık yapılarını, yani _döngüleri_ kullanabilirsin.

Bunu kanıtlamak için, `print()` olarak anılan özel derleme fonksiyonunu tanıtmak istiyorum: Ona, yazdırması için bir metin verirsiniz, o da yazdırır. Bizim gibi siz de bir oyun alanında çalışıyorsanız, metninizin sonuç penceresinde belirdiğini göreceksiniz. Eğer Xcode'da gerçek bir uygulama çalıştırıyorsanız, metninizi Xcode'un log (günlük) penceresinde göreceksiniz. Her şekilde de, bir değişkenin içeriğinin ön görüntüsünü almak için `print()` harika bir yol.

Şu koda bir göz atın:
```swift
print("1 x 10 is \(1 * 10)")
print("2 x 10 is \(2 * 10)")
print("3 x 10 is \(3 * 10)")
print("4 x 10 is \(4 * 10)")
print("5 x 10 is \(5 * 10)")
print("6 x 10 is \(6 * 10)")
print("7 x 10 is \(7 * 10)")
print("8 x 10 is \(8 * 10)")
print("9 x 10 is \(9 * 10)")
print("10 x 10 is \(10 * 10)")
```

Çalışması bittiğinde, oyun alanınızın sonuç panelindeki tabloda 10'un katlarını yazdığını göreceksiniz. Ama tabi bu pek yeterli bir kod değil. Aslında <mark style="background: #FFF3A3A6;">closed range operator</mark> <mark style="background: #FF5582A6;">(kapalı aralık operatörü)</mark> adı verilen ve yan yana 3 noktadan oluşan `...` bir rakam aralığı üzerinde döngü yapmak daha temiz bir yoldur.

Kapalı aralık operatörünü kullanarak, tüm bu kodu 3 satırda yeniden yazabiliriz:

```swift
for i in 1...10 {
    print("\(i) x 10 is \(i * 10)")
}
```

Sonuç paneli şimdi, 10 kez çalışan döngümüzdeki "(10'un katları)"nı gösteriyor. Eğer döngünün aslında ne yaptığını bilmek isterseniz, 10'un katlarının sağındaki kareye hemen tıklayın. İçinde "10 x 10 is 100" yazan bir kutu göreceksiniz ve eğer sağ tıklarsanız "Value History" (Değer Tarihçesi) seçeneğini göreceksiniz. Şimdi ona tıklayın ve aşağıdaki resmi görün:

![Bir Swift oyun alanı bir döngü çalıştırdığında, döngünün sadece kaç kez çalıştığını gösterir. Eğer değerleri daha yakından incelemek isterseniz, sonuç bölümündeki kutuya tıklayın.](https://www.hackingwithswift.com/img/books/hws/0-5.png)

1 ve 10'u da içermek üzere, 1'den 10'a kadar sayan döngüde, sayı `i` sabitine atanıyor ve ardından süslü parantezlerin içindeki kod bloğu çalıştırılıyor.

Eğer sayının ne olduğunun önemi yoksa, sabit yerine bir altçizgi kullanabilirsiniz. Örneğin, şu şekilde Taylor Swift'in şarkı sözlerinden bazılarını yazdırmak istiyoruz:

```swift
var str = "Fakers gonna"

for _ in 1 ... 5 {
    str += " fake"
}

print(str)
```

Bu kod bloğu, döngü devam ettiği sürece metni ekleyecek ve ekrana "Fakers gonna fake fake fake fake fake" yazdıracak.

Eğer Swift her bir sayıyı döngü devam ettiği sürece bir değişkene atamak zorunda değilse, yazdığınız kod biraz daha hızlı çalışır. Sonuç olarak, eğer `for i in…` yazıyorsanız ve sonrasında `i`kullanmıyorsanız, Xcode `_` ile değiştirmeyi önerecek.

<mark style="background: #FFF3A3A6;">"Half open range operator"</mark> <mark style="background: #FF5582A6;">(yarı açık aralık operatörü)</mark> olarak anılan bir kapalı aralık operatörü çeşidi daha var ve kolayca kafa karışıklığına yol açabilir. Yarı açık aralık operatörü `..<` şeklinde gösterilir ve ilk sayıdan başlayıp, ikinci sayıyı _içermeden_ sonlanır. Örneğin `1 ..< 5` ifadesi, 1, 2, 3, 4'e kadar sayacaktır.

## Diziler üzerinde döngü yapma

Swift, dizideki tüm elemanlar üzerinde döngü yapabilmek için basit bir yol sunar. Çünkü Swift, dizinin zaten ne tür bir veri tuttuğunu bilir ve dizideki her bir elemanın üzerinden geçer, isimlendirdiğiniz sabite atar ve sonrasında kod bloğunuzu çalıştırır. Örneğin, aşağıdaki gibi harika şarkılardan oluşan listeyi yazdırabiliriz:

```swift
var songs = ["Shake it Off", "You Belong with Me", "Look What You Made Me Do"]

for song in songs {
    print("My favorite song is \(song)")
}
```

Burada dizi üzerinde isterseniz `for i in`şeklinde bir döngü de kullanabilirsiniz, çünkü dizinin içindeki indeksi sabit olarak kullanıyorsunuz. Hatta aşağıda gösterildiği gibi, iki ayrı dizideki indeks üzerinde de kullanabiliriz bu sabiti:

```swift
var people = ["players", "haters", "heart-breakers", "fakers"]
var actions = ["play", "hate", "break", "fake"]

for i in 0 ... 3 {
    print("\(people[i]) gonna \(actions[i])")
}
```

Yarı açık aralık operatörlerinin ne için kullanıldığını merak ediyor olabilirsiniz, ama sıfırdan başladıkları için dizilerle çalışmak oldukça kullanışlıdır. Dolayısıyla 0'dan başlayıp 3'e kadar (3 dahil) saymaktansa, 0'dan başlayıp dizi içindeki eleman sayısını _hariç_ bırakarak sayabiliriz.

**<mark style="background: #FF5582A6;">Unutmayın :</mark> Diziler sıfırdan başlar, o yüzden 4 elemanlı bir dizinin indeksi en fazla 3 olabilir; bu da bir döngüde neden _hariç_ bırakarak kullanmamız gerektiğidir.**

Bir dizideki elemanları saymak için, `someArray.count` ifadesini kullanın. Kodumuzu böylece şu şekilde tekrar yazabiliriz:

```swift
var people = ["players", "haters", "heart-breakers", "fakers"]
var actions = ["play", "hate", "break", "fake"]

for i in 0 ..< people.count {
    print("\(people[i]) gonna \(actions[i])")
}
```

## Dahili döngüler

İsterseniz, döngüler içine döngüler koyabilirsiniz; hatta o döngülerin içine de döngüler konabilir. Tabi birden kendinizi birşeyi 10 milyon kez yapıyor bulabilirsiniz, o yüzden dikkatli olun!

Şunu oluşturmak için önceki iki döngüyü birleştirebiliriz:

```swift
var people = ["players", "haters", "heart-breakers", "fakers"]
var actions = ["play", "hate", "break", "fake"]

for i in 0 ..< people.count {
    var str = "\(people[i]) gonna"

    for _ in 1 ... 5 {
        str += " \(actions[i])"
    }

    print(str)
}
```

Bu bize "players gonna play play play play play", ardından da "haters gonna…" çıktısını verir. Ana fikri anladınız sanırım.

Önemli bir not: Programcılar geleneksel olarak döngülerde `i`, `j` ve hatta `k` sabitlerini kullanırlar. İstediğiniz ismi verebilirsiniz, ama lütfen kendini anlatan bir isim olsun: `for personNumber in 0 ..< people.count` şeklinde olması kesinlikle daha doğru.

