#swift #yazılım 

# nil birleştirme ile isteğe bağlı seçenekler nasıl açılır?

Bir dakika... Swift'in opsiyonları açmanın _üçüncü bir yolu var mı?_ Evet! Ayrıca gerçekten kullanışlıdır: _sıfır birleştirme işleci_ olarak adlandırılır ve bir isteğe bağlı paketi açmamıza ve isteğe bağlı boşsa varsayılan bir değer sağlamamıza izin verir.

Biraz geri saralım:

```swift
let captains = [
    "Enterprise": "Picard",
    "Voyager": "Janeway",
    "Defiant": "Sisko"
]

let new = captains["Serenity"]
```

Bu, sözlüğümüzde var olmayan bir anahtarı okur `captains`; bu, `new`olarak ayarlanacak isteğe bağlı bir dize olacağı anlamına gelir `nil`.

nil birleştirme işleci ile yazılmış `??`, herhangi bir isteğe bağlı için varsayılan bir değer sağlayabiliriz, bunun gibi:

```swift
let new = captains["Serenity"] ?? "N/A"
```

Bu, değeri sözlükten okuyacak `captains`ve paketini açmaya çalışacaktır. İsteğe bağlı içinde bir değer varsa, geri gönderilecek ve içinde saklanacak `new`, ancak değilse, bunun yerine “N/A” kullanılacaktır.

Bu, isteğe bağlı olanın - bir değer veya `nil`- ne içerdiğinden bağımsız olarak, bunun `new`isteğe bağlı değil gerçek bir dize olacağı anlamına gelir. Bu, değerin içindeki dize olabilir `captains`veya "N/A" olabilir.

Şimdi, ne düşündüğünüzü biliyorum: sözlükten okurken bir varsayılan değer belirleyemez miyiz? Kesinlikle haklı olduğunuzu düşünüyorsanız:

```swift
let new = captains["Serenity", default: "N/A"]
```

Bu, tamamen aynı sonucu verir, bu da sıfır birleştirme operatörünün anlamsız gibi görünmesine neden olabilir. Ancak, nil birleştirme operatörü yalnızca sözlüklerle çalışmaz, aynı zamanda _herhangi bir_ isteğe bağlı seçenekle de çalışır.

Örneğin, `randomElement()`dizilerdeki yöntem diziden rastgele bir öğe döndürür, ancak onu boş bir dizide çağırıyor olabileceğiniz için isteğe bağlı bir öğe döndürür. Dolayısıyla, bir varsayılan sağlamak için nil birleştirme kullanabiliriz:

```swift
let tvShows = ["Archer", "Babylon 5", "Ted Lasso"]
let favorite = tvShows.randomElement() ?? "None"
```

Veya isteğe bağlı özelliği olan bir yapınız var ve eksik olduğu zamanlar için mantıklı bir varsayılan sağlamak istiyorsunuz:

```swift
struct Book {
    let title: String
    let author: String?
}

let book = Book(title: "Beowulf", author: nil)
let author = book.author ?? "Anonymous"
print(author)
```

Dönüştürme başarısız olabileceğinden , aslında bir isteğe bağlı değeri geri aldığınız bir dizeden bir tamsayı oluşturursanız bile kullanışlıdır `Int?`- "Merhaba" gibi geçersiz bir tamsayı sağlamış olabilirsiniz. Burada varsayılan bir değer sağlamak için nil birleştirme kullanabiliriz, bunun gibi:

```swift
let input = ""
let number = Int(input) ?? 0
print(number)
```

Gördüğünüz gibi, nil birleştirme operatörü, isteğe bağlı bir değere sahip olduğunuz ve içindeki değeri kullanmak veya eksikse varsayılan bir değer sağlamak istediğiniz her yerde kullanışlıdır.

---

# İsteğe bağlı zincirleme kullanılarak birden çok isteğe bağlı nasıl işlenir?

İsteğe bağlı zincirleme, isteğe bağlı öğelerin içindeki seçenekleri okumak için basitleştirilmiş bir sözdizimidir. Bu, nadiren kullanmak isteyeceğiniz bir şey gibi gelebilir, ancak size bir örnek gösterirsem, bunun neden yararlı olduğunu göreceksiniz.

Bu koda bir göz atın:

```swift
let names = ["Arya", "Bran", "Robb", "Sansa"]

let chosen = names.randomElement()?.uppercased() ?? "No one"
print("Next in line: \(chosen)")
```

Bu, aynı anda iki isteğe bağlı özelliği kullanır: nil birleştirme operatörünün, bir isteğe bağlı boşsa varsayılan bir değer sağlamaya nasıl yardımcı olduğunu zaten gördünüz, ancak ondan önce , bir soru işaretinin ardından daha fazla kodun geldiği _isteğe bağlı zincirleme_ görüyorsunuz.

Opsiyonel zincirleme, “eğer opsiyonelin içinde bir değer varsa, aç o zaman…” dememizi sağlar ve daha fazla kod ekleyebiliriz. Bizim durumumuzda "diziden rastgele bir öğe almayı başardıysak, onu büyük harfle yazalım" diyoruz. Unutmayın, `randomElement()`dizi boş olabileceğinden isteğe bağlı döndürür.

İsteğe bağlı zincirlemenin büyüsü, isteğe bağlı boşsa sessizce hiçbir şey yapmamasıdır - sadece daha önce sahip olduğunuz aynı isteğe bağlıyı, hala boş olarak geri gönderir. Bu, isteğe bağlı bir zincirin dönüş değerinin her zaman isteğe bağlı olduğu anlamına gelir; bu nedenle, varsayılan bir değer sağlamak için hala sıfır birleştirmeye ihtiyacımız var.

İsteğe bağlı zincirler istediğiniz kadar uzayabilir ve herhangi bir parça geri gönderir göndermez `nil`kodun geri kalanı dikkate alınmaz ve geri gönderilir `nil`.

İsteğe bağlı zincirlemeyi daha da zorlaştıran bir örnek vermek gerekirse, şunu hayal edin: kitapları yazar adlarına göre alfabetik olarak sıralamak istiyoruz. Bunu hemen parçalara ayırırsak, o zaman:

-   İsteğe bağlı bir yapı örneğine sahibiz `Book`- sıralayacak bir kitabımız olabilir veya olmayabilir.
-   Kitabın bir yazarı olabilir veya anonim olabilir.
-   Bir yazar dizesi varsa, boş bir dize olabilir veya metin içerebilir, bu nedenle her zaman ilk harfin orada olduğuna güvenemeyiz.
-   İlk harf varsa, büyük harf olduğundan emin olun, böylece çan kancaları gibi küçük adlara sahip yazarların doğru sıralanması sağlanır.

İşte bunun nasıl görüneceği:

```swift
struct Book {
    let title: String
    let author: String?
}

var book: Book? = nil
let author = book?.author?.first?.uppercased() ?? "A"
print(author)
```

Yani “bir kitabımız varsa ve kitabın bir yazarı varsa ve yazarın baş harfi varsa onu büyük harfle yazıp geri gönderin, yoksa A'yı geri gönderin” yazıyor.

_Kuşkusuz, opsiyonel seçenekler arasında bu_ kadar derine inmeniz pek olası değil , ama umarım sözdiziminin ne kadar hoş bir şekilde kısa olduğunu görebilirsiniz!

---

# İsteğe bağlı seçeneklerle işlev hatası nasıl ele alınır?

Hata atabilecek bir işlevi çağırdığımızda, ya onu kullanarak çağırır `try`ve hataları uygun şekilde ele alırız ya da işlevin başarısız olmayacağından eminsek, `try!`yanlış yaparsak kodumuzun çökeceğini kullanır ve kabul ederiz. (Spoiler: Çok nadiren kullanmalısınız `try!`.)

Ancak bir alternatif daha var: Tek umursadığımız işlevin başarılı olup olmadığıysa, işlevin isteğe bağlı bir değer döndürmesi için _isteğe bağlı_ bir try kullanabiliriz . İşlev herhangi bir hata vermeden çalıştıysa, isteğe bağlı dönüş değerini içerir, ancak herhangi bir hata atılırsa, işlev sıfır döndürür. Bu, tam olarak hangi hatanın atıldığını bilemeyeceğimiz anlamına gelir, ancak çoğu zaman sorun olmaz - işlevin çalışıp çalışmadığına bakabiliriz.

İşte nasıl göründüğü:

```swift
enum UserError: Error {
    case badID, networkFailed
}

func getUser(id: Int) throws -> String {
    throw UserError.networkFailed
}

if let user = try? getUser(id: 23) {
    print("User: \(user)")
}
```

İşlev `getUser()`her zaman bir hata atar , bu bizim test amaçlarımız için uygundur, ancak aslında _hangi_`networkFailed` hatanın atıldığı umurumuzda değildir - tek umursadığımız, çağrının bir kullanıcıyı geri gönderip göndermediğidir.

Bu, yardımcı olduğu yerdir `try?`: `getUser()`herhangi bir hata atılırsa sıfır olacak isteğe bağlı bir dize döndürür. _Tam olarak hangi hatanın olduğunu bilmek istiyorsanız_ , bu yaklaşım yararlı olmayacaktır, ancak çoğu zaman umursamıyoruz.

İsterseniz `try?`“bu fonksiyondan dönüş değeri almaya çalışın, başarısız olursa bunun yerine bu varsayılan değeri kullanın” anlamına gelen nil birleştirme ile birleştirebilirsiniz.

Yine de dikkatli olun: nil birleşiminden önce bazı parantezler eklemeniz gerekir, böylece Swift tam olarak ne demek istediğinizi anlar. Örneğin, şunu yazarsınız:

```swift
let user = (try? getUser(id: 23)) ?? "Anonymous"
print(user)
```

`try?`Esas olarak üç yerde kullanıldığını göreceksiniz :

1.  İle kombinasyon halinde çağrı dönerse `guard let`mevcut işlevden çıkmak için .`try?``nil`
2.  Bir şeyi denemek veya başarısızlık durumunda varsayılan bir değer sağlamak için nil birleştirme ile birlikte.
3.  Dönüş değeri olmayan herhangi bir fırlatma işlevini çağırırken, başarılı olup olmadığını gerçekten umursamadığınızda - örneğin, bir günlük dosyasına yazıyor veya bir sunucuya analitik gönderiyor olabilirsiniz.

