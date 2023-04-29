#swift #yazılım 

Swift dili, bir tipin örneklerinden ziyade, bir tipe ait özellikler ve metodlar oluşturmanıza izin verir. Bu, paylaşımlı veriyi tutarak verinizi anlamlı bir şekilde organize etmenize yardımcı olur.

Bu paylaşımlı özellikler Swiift dilinde "sabit özellikler" olarak adlandırılır ve `static` anahtar sözcüğünü kullanarak bir tane oluşturursunuz. Bir kez bu yapıldığında, tipin tam adını kullanarak özelliğe ulaşabilirsiniz. İşte basit bir örnek:

```swift
struct TaylorFan {
    static var favoriteSong = "Look What You Made Me Do"

    var name: String
    var age: Int
}

let fan = TaylorFan(name: "James", age: 25)
print(TaylorFan.favoriteSong)
```

Bu şekilde, bir Taylor Swift hayranın kendine ait bir "name" (isim) ve "age" (yaş) özelliği oluyor, ama hepsi aynı en sevilen şarkıya sahip (favorite song).

Sabit metodu, struct'ın diğer kopyalarından çok kendi struct'ına ait olduğu için, struct'tan herhangi bir sabit olmayan özelliğe giriş yapmak için onu kullanamazsınız.

---

Yapılara özellikleri ve yöntemleri nasıl ekleyebileceğimizi ve her yapının bu özelliklerin kendi benzersiz kopyasına sahip olduğunu gördünüz, böylece yapı üzerinde bir yöntem çağrıldığında aynı türden farklı bir yapının özellikleri okunmaz.

Eh, bazen - sadece bazen - yapının belirli bir örneğine değil, doğrudan kullanmanıza izin veren yapının kendisine bir özellik veya yöntem eklemek istersiniz. Bu tekniği SwiftUI ile iki şey için çok kullanıyorum: örnek veriler oluşturmak ve çeşitli yerlerde erişilmesi gereken sabit verileri depolamak.

İlk olarak, statik özelliklerin ve yöntemlerin nasıl oluşturulup kullanılacağına ilişkin basitleştirilmiş bir örneğe bakalım:

```swift
struct School {
    static var studentCount = 0

    static func add(student: String) {
        print("\(student) joined the school.")
        studentCount += 1
    }
}
```

`static`Buradaki anahtar kelimeye dikkat edin ; bu, hem `studentCount`özelliğin hem de yöntemin yapının bireysel örneklerinden ziyade yapının kendisine `add()`ait olduğu anlamına gelir.`School`

Bu kodu kullanmak için aşağıdakileri yazardık:

```swift
School.add(student: "Taylor Swift")
print(School.studentCount)
```

Bir örneğini yaratmadım – kelimenin tam anlamıyla ve doğrudan yapı üzerinde `School`kullanabiliriz . Bunun nedeni, her ikisinin de statik olmasıdır, yani yapı örneklerinde benzersiz olarak var olmazlar.`add()``studentCount`

`studentCount`Bu aynı zamanda , yöntemi şu şekilde işaretlemeden özelliği neden değiştirebildiğimizi de açıklamalıdır `mutating`– bu yalnızca normal struct işlevlerinde, bir struct örneğinin sabit olarak oluşturulduğunda ve çağrılırken hiçbir örneğin _olmadığı_`add()` zamanlar için gereklidir .

Statik ve statik olmayan özellikleri ve yöntemleri karıştırmak ve eşleştirmek istiyorsanız iki kural vardır:

1.  Statik koddan statik olmayan koda erişmek için… şansınız kalmadı: statik özellikler ve yöntemler, statik olmayan özelliklere ve yöntemlere atıfta bulunamaz çünkü bu bir anlam ifade etmez – hangi örneğine atıfta bulunursunuz `School`?
2.  Statik olmayan koddan statik koda erişmek için her zaman türünüzün adını kullanın, örneğin `School.studentCount`. `Self`Geçerli türe başvurmak için de kullanabilirsiniz .

Şimdi elimizde `self` _ve_ `Self` var ve farklı anlamlara geliyorlar: `self`yapının geçerli değerini ifade eder ve `Self`geçerli _türü_ ifade eder .

**İpucu:**`self` ve arasındaki farkı unutmak kolaydır `Self`, ancak bunu düşünürseniz, Swift'in geri kalan adlandırmalarına benzer - tüm veri türlerimizi büyük harfle ( `Int`, `Double`, , vb.) başlatırız, bu nedenle başlamak `Bool`mantıklıdır `Self`hem de büyük harfle.

Şimdi, duyabileceğiniz o ses, "buna neden ihtiyaç duyuluyor?" Ve anlıyorum - bu ilk başta oldukça gereksiz bir özellik gibi görünebilir. Bu yüzden size statik verileri kullandığım iki ana yolu göstermek istiyorum.

İlk olarak, uygulamalarımdaki ortak verileri düzenlemek için statik özellikler kullanıyorum. `AppData`Örneğin, birçok yerde kullandığım birçok paylaşılan değeri depolamak gibi bir yapıya sahip olabilirim :

```swift
struct AppData {
    static let version = "1.3 beta 2"
    static let saveFilename = "settings.json"
    static let homeURL = "https://www.hackingwithswift.com"
}
```

Bu yaklaşımı kullanarak, uygulamamın sürüm numarası gibi bir şeyi kontrol etmem veya görüntülemem gereken her yerde - hakkında ekranı, hata ayıklama çıktısı, günlük bilgileri, destek e-postaları vb. - okuyabilirim `AppData.version`.

Statik verileri yaygın olarak kullanmamın ikinci nedeni, yapılarımdan örnekler oluşturmaktır. Daha sonra göreceğiniz gibi, SwiftUI en iyi, siz geliştirirken uygulamanızın önizlemelerini gösterebildiğinde çalışır ve bu önizlemeler genellikle örnek veriler gerektirir. Örneğin, bir çalışanın verilerini görüntüleyen bir ekran gösteriyorsanız, çalışırken her şeyin doğru göründüğünü kontrol edebilmeniz için önizleme ekranında örnek bir çalışan gösterebilmek isteyeceksiniz.

`example`Bu en iyi şekilde , yapı üzerinde aşağıdaki gibi statik bir özellik kullanılarak yapılır :

```swift
struct Employee {
    let username: String
    let password: String

    static let example = Employee(username: "cfederighi", password: "hairforceone")
}
```

`Employee`Ve şimdi , tasarım önizlemelerinizde çalışmak için bir örneğe ihtiyacınız olduğunda , kullanabilirsiniz `Employee.example`ve işiniz bitti.

Başta söylediğim gibi, statik bir özelliğin veya yöntemin anlamlı olduğu çok az durum vardır, ancak bunlar yine de kullanışlı araçlardır.