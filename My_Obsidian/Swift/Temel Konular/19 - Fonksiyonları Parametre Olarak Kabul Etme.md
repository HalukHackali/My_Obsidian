#swift #yazılım 

Bakmak istediğim kapanışla ilgili son bir konu var, o da diğer fonksiyonları parametre olarak kabul eden fonksiyonların nasıl yazılacağıdır. Bu, takip eden kapatma söz dizimi nedeniyle özellikle kapatmalar için önemlidir, ancak ne olursa olsun sahip olunması yararlı bir beceridir.

Daha önce bu koda baktık:

```swift
func greetUser() {
    print("Hi there!")
}

greetUser()

var greetCopy: () -> Void = greetUser
greetCopy()
```

Tür ek açıklamasını kasıtlı olarak oraya ekledim, çünkü işlevleri parametre olarak belirtirken tam olarak bunu kullanıyoruz: Swift'e işlevin hangi parametreleri kabul ettiğini ve dönüş türünü söylüyoruz.

Bir kez daha kendinizi hazırlayın: Bunun sözdizimi ilk başta göze biraz zor geliyor! İşte bir işlevi belirli sayıda tekrarlayarak bir tamsayı dizisi oluşturan bir işlev:

```swift
func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    var numbers = [Int]()

    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }

    return numbers
}
```

Bunu parçalayalım…

1.  fonksiyon denir `makeArray()`. Biri istediğimiz tamsayı sayısı olmak üzere iki parametre alır ve ayrıca bir tamsayı dizisi döndürür.
2.  İkinci parametre bir fonksiyondur. Bu, kendi başına hiçbir parametre kabul etmez, ancak her çağrıldığında bir tamsayı döndürür.
3.  İçinde `makeArray()`yeni bir boş tamsayı dizisi oluşturuyoruz, ardından istendiği kadar döngü yapıyoruz.
4.  Döngü her döndüğünde, `generator`parametre olarak iletilen işlevi çağırırız. Bu, yeni bir tamsayı döndürecek, bu yüzden onu diziye koyuyoruz `numbers`.
5.  Sonunda bitmiş dizi döndürülür.

Gövdesi `makeArray()`çoğunlukla basittir: bir tamsayı oluşturmak için bir işlevi tekrar tekrar çağırın, her değeri bir diziye ekleyin ve ardından hepsini geri gönderin.

Karmaşık _kısım_ ilk satırdır:

```swift
func makeArray(size: Int, using generator: () -> Int) -> [Int] {
```

Orada iki takım parantezimiz ve iki takım dönüş tipimiz var, bu yüzden ilk başta biraz karışık olabilir. Bölürseniz, doğrusal olarak okuyabilmeniz gerekir:

1.  Yeni bir fonksiyon yaratıyoruz.
2.  fonksiyon denir `makeArray()`.
3.  İlk parametre, adı verilen bir tamsayıdır `size`.
4.  İkinci parametre `generator`, kendisi hiçbir parametre kabul etmeyen ve bir tamsayı döndüren adı verilen bir işlevdir.
5.  Her şey – `makeArray()`– bir tamsayı dizisi döndürür.

Sonuç olarak, artık her sayıyı oluşturmak için kullanılması gereken bir işleve geçerek keyfi boyutta tamsayı dizileri yapabiliriz:

```swift
let rolls = makeArray(size: 50) {
    Int.random(in: 1...20)
}

print(rolls)
```

Ve unutmayın, aynı işlevsellik özel işlevlerle de çalışır, böylece şöyle bir şey yazabiliriz:

```swift
func generateNumber() -> Int {
    Int.random(in: 1...20)
}

let newRolls = makeArray(size: 50, using: generateNumber)
print(newRolls)
```

`generateNumber()`Diziyi doldurmak için 50 kez arayacak .

Swift ve SwiftUI'yi öğrenirken, işlevleri parametre olarak nasıl kabul edeceğinizi bilmeniz gereken yalnızca birkaç kez olacak, ancak en azından artık nasıl çalıştığına ve neden önemli olduğuna dair bir fikriniz var.

Devam etmeden önce son bir şey daha var: İsterseniz fonksiyonunuzun _birden fazla_ fonksiyon parametresini kabul etmesini sağlayabilirsiniz , bu durumda birden fazla sondaki kapanış belirtebilirsiniz. Buradaki sözdizimi SwiftUI'de çok yaygındır, bu yüzden en azından burada onun tadına bakmanız önemlidir.

Bunu göstermek için burada, her biri parametre kabul etmeyen ve hiçbir şey döndürmeyen üç işlev parametresini kabul eden bir işlev var:

```swift
func doImportantWork(first: () -> Void, second: () -> Void, third: () -> Void) {
    print("About to start first work")
    first()
    print("About to start second work")
    second()
    print("About to start third work")
    third()
    print("Done!")
}
```

`print()`Arasında yapılan belirli bir işi simüle etmek ve çağrılmak için oraya fazladan `first`aramalar ekledim .`second``third`

Bunu çağırmaya gelince, ilk sondaki kapanış zaten kullandığımızla aynıdır, ancak ikinci ve üçüncü farklı formattadır: ayracı önceki kapanıştan bitirirsiniz, ardından harici parametre adını ve iki nokta üst üste yazarsınız, ardından başka bir parantez başlat.

İşte böyle görünüyor:

```swift
doImportantWork {
    print("This is the first work")
} second: {
    print("This is the second work")
} third: {
    print("This is the third work")
}
```

Üç takip eden kapanışa sahip olmak, beklediğiniz kadar nadir değildir. Örneğin, SwiftUI'de bir içerik bölümü oluşturmak, üç takip eden kapatma ile yapılır: biri içeriğin kendisi için, biri yukarıya konulacak bir başlık için ve biri aşağıya konacak bir altbilgi için.