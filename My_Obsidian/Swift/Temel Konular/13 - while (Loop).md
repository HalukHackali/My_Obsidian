#swift #yazılım 

Durmasını söyleyinceye kadar kod bloğunu tekrar tekrar çalıştıran bir üçüncü tür döngüyü göreceksiniz. Oyunlar gibi, ne kadar süre sonra sonlanacağını bilmediğiniz yerlerde kullanılır. Sadece tekrar etmeye devam edersiniz; "dokunuşları kontrol, robotları hareketlendir, ekrana çiz, dokunuşları kontrol et..." gibi. ta ki, sonunda kullanıcının bir butona basıp oyundan çıkarak ana menüye geri dönene kadar.

Bu tür döngüler `while` döngüleri olarak anılır ve şuna benzerler:

```swift
var counter = 0

while true {
    print("Counter is now \(counter)")
    counter += 1

    if counter == 556 {
        break
    }
}
```

Bu kod, `break` adı verilen yeni bir anahtar sözcük sunuyor. İstediğiniz bir noktada `while` veya `for`döngüsünden çıkmak için kullanılır. Bu olmadan kod asla sonlanmaz çünkü durum kontrolünde sürekli "doğru" çıkar ve doğru her zaman doğrudur. `break` ifadesi olmaksızın, sonsuz bir döngüye girilir ki, bu da kötü birşeydir.

Bu `while` döngüleri, bilinmeyen bir veri kullandığınızda, internetten birşeyler indirdiğinizde, XML gibi bir dosya okuduğunuzda, kullanıcı girişi beklediğinizde veya bunun gibi bir durumda en iyi şekilde çalışır. Yani bu, yalnızca yeteri kadar çalıştıktan sonra döngünün ne zaman duracağınızı bildiğiniz içindir.

`break` ifadesinin tam karşıtı `continue` ifadesidir. Halbuki bir döngüyü kırmak, çalışmayı hemen durdurur ve döngüden sonrasına doğrudan devam eder. Döngü, sadece o andaki yinelemesinden çıkar. Sonrasında döngünün en başına sıçrar ve oradan başlar.

Örnek olarak aşağıdaki kodu inceleyin:

```swift
var songs = ["Shake it Off", "You Belong with Me", "Look What You Made Me Do"]

for song in songs {
    if song == "You Belong with Me" {
        continue
    }

    print("My favorite song is \(song)")
}
```

Bu döngü, Taylor Swift'in 3 şarkısı etrafındadır, ama sadece ikisinin ismini yazdırılacak. Bunun sebebi ise `continue` anahtar sözcüğüdür: Döngü "You Belong with Me" adlı şarkı adını kullanmayı denediğinde, `continue` çağırılacak, bu da döngünün hemen başlangıcına geri sıçramasına sebep olacak. Böylece `print()` asla çağırılmayacak ve bunun yerine doğrudan “Look What You Made Me Do” ile devam edilecek.

---

# Çalışmayı tekrarlamak için while döngüsü nasıl kullanılır?

Swift'in : ona bir koşul sağlayın adında ikinci bir döngü türü vardır `while`ve bir `while`döngü, koşul yanlış olana kadar döngü gövdesini sürekli olarak yürütür.

`while`Yine de zaman zaman döngüler görecek olsanız da , bunlar `for`döngüler kadar yaygın değildir. Sonuç olarak, var olduklarını bilesiniz diye bunları ele almak istiyorum ama üzerinde fazla durmayalım, olur mu?

İşte `while`başlamamız için temel bir döngü:

```swift
var countdown = 10

while countdown > 0 {
    print("\(countdown)…")
    countdown -= 1
}

print("Blast off!")
```

Bu, 10'dan başlayan bir tamsayı sayacı oluşturur, ardından `while`koşulla bir döngü başlatır `countdown > 0`. Böylece, döngü gövdesi - sayıyı yazdırıp 1'i çıkararak - 0'a eşit veya 0'ın altında olana kadar sürekli olarak çalışacak `countdown`, bu noktada döngü sona erecek ve son mesaj yazdırılacaktır.

`while`döngüler, döngünün kaç kez döneceğini bilmediğiniz zaman gerçekten kullanışlıdır. `Int`Bunu göstermek için, size her ikisinin de sahip olduğu , gerçekten yararlı bir işlevsellik parçasını tanıtmak istiyorum `Double`: `random(in:)`. `Int`Buna çalışmak için bir dizi sayı verin ve rastgele veya `Double`bu aralığın içinde bir yere geri gönderecektir .

Örneğin, bu 1 ile 1000 arasında yeni bir tamsayı oluşturur.

```swift
let id = Int.random(in: 1...1000)
```

Bu da 0 ile 1 arasında rastgele bir ondalık sayı oluşturur:

```swift
let amount = Double.random(in: 0...1)
```

`while`Bu işlevi, 20 taraflı sanal zarları tekrar tekrar atmak için bir döngü ile kullanabiliriz ve döngüyü yalnızca 20 atıldığında sonlandırabiliriz - siz tüm Dungeons & Dragons oyuncuları için kritik bir vuruş .

İşte bunu gerçekleştirmek için kod:

```swift
// create an integer to store our roll
var roll = 0

// carry on looping until we reach 20
while roll != 20 {
    // roll a new dice and print what it was
    roll = Int.random(in: 1...20)
    print("I rolled a \(roll)")
}

// if we're here it means the loop ended – we got a 20!    
print("Critical hit!")
```

Kendinizi hem `for` hem de `while` döngülerini  kodunuzda kullanırken bulacaksınız: `for` döngüleri, bir aralık veya dizi gibi sınırlı miktarda veriye sahip olduğunuzda daha yaygındır, ancak özel bir koşula ihtiyacınız olduğunda `while` döngüleri gerçekten yararlıdır. 