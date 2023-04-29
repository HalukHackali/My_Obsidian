#swift #yazılım 

Giriş kontrolü, struct ve class'ların içinde olan ve dış dünyaya sunulacak ne tür veri olduğunu belirlemenize izin verir. Bunun için şu 4 değiştiriciyi seçersiniz:

-   Açık (Public): O özelliği herkesin okuyabileceği ve yazabileceği anlamına gelir.
-   Dahili (Internal): O özelliği sadece Swift kodunuzun okuyabileceği ve yazabileceği anlamına gelir. Eğer kodunuzu diğerlerinin kullanımı için bir çerçeve olarak hazırlarsanız, özelliği kimse okuyamaz.
-   Dosyaya Özel (File Private): Tür olarak sadece aynı dosyada bulunan Swift kodu o özelliği okuyup yazabilir.
-   Özel (Private): Bu en kısıtlayıcı seçenektir. O özelliğin sadece tipe ait metodları veya genişletmeleri içinde kullanılabileceği anlamına gelir.

Çoğu zaman giriş kontrolü tanımlamanıza gerek yoktur, ama bazen başkalarının doğrudan ulaşmasını engellemek için bir özelliği açıkça özel olarak ayarlamak istersiniz. Bu, kendi metodunuzun o özellikle çalışabileceği, ama diğerlerinin çalışamayacağı için faydalıdır. Böylece, belirli eylemler yapan kodunuzu incelemek için onları zorlarsınız.

Bir özelliği, özel kılmak için sadece şunu yapın:

```swift
class TaylorFan {
    private var name: String!
}
```

Eğer "dosyaya özel" giriş kontrolünü kullanmak isterseniz, şu şekilde bir sözcük yazın: `fileprivate`. Ama yine de şunu söylemeliyim ki, `fileprivate` kullanımı çok nadirdir!


---
# Cccess Control kullanılarak dahili verilere erişim nasıl sınırlanır?


Varsayılan olarak, Swift'in yapıları, özelliklerine ve yöntemlerine serbestçe erişmemize izin verir, ancak genellikle istediğiniz bu değildir - bazen bazı verileri harici erişimden gizlemek istersiniz. Örneğin, belki özelliklerinize dokunmadan önce uygulamanız gereken bir mantığınız vardır veya belki bazı yöntemlerin belirli bir şekilde veya sırayla çağrılması gerektiğini ve bu nedenle dışarıdan dokunulmaması gerektiğini biliyorsunuzdur.

Problemi örnek bir yapı ile gösterebiliriz:

```swift
struct BankAccount {
    var funds = 0

    mutating func deposit(amount: Int) {
        funds += amount
    }

    mutating func withdraw(amount: Int) -> Bool {
        if funds >= amount {
            funds -= amount
            return true
        } else {
            return false
        }
    }
}
```

Bir banka hesabına para yatırmak ve çekmek için yöntemleri vardır ve şu şekilde kullanılmalıdır:

```swift
var account = BankAccount()
account.deposit(amount: 100)
let success = account.withdraw(amount: 200)

if success {
    print("Withdrew money successfully")
} else {
    print("Failed to get the money")
}
```

Ancak `funds`mülk bize sadece dışsal olarak maruz kalıyor, peki bizi ona doğrudan dokunmaktan alıkoyan nedir? Cevap _hiçbir şeydir_ - bu tür kodlara izin verilir:

```swift
account.funds -= 1000
```

Bu, insanların sahip olduklarından daha fazla para almasını engellemek için uyguladığımız mantığı tamamen atlıyor ve şimdi programımız tuhaf şekillerde davranabilir.

Bunu çözmek için, Swift'e bunun yalnızca yapı içinde erişilebilir olması gerektiğini söyleyebiliriz `funds`- yapıya ait yöntemlerle ve ayrıca herhangi bir hesaplanmış özellik, özellik gözlemcisi vb.

Bu sadece bir fazladan kelime alır:

```swift
private var funds = 0
```

Ve artık `funds`struct'ın dışından erişim mümkün değildir, ancak hem ve hem de içinde _mümkündür_ . Yapının dışından okumaya veya yazmaya çalışırsanız, Swift kodunuzu oluşturmayı reddedecektir.`deposit()``withdraw()``funds`

_Buna erişim kontrolü_ denir , çünkü bir yapının özelliklerine ve yöntemlerine yapının dışından nasıl erişilebileceğini kontrol eder.

Swift bize birkaç seçenek sunar, ancak öğrenirken yalnızca birkaçına ihtiyacınız olacak:

-   `private`“Yapı dışında hiçbir şeyin bunu kullanmasına izin verme” için kullanın .
-   `fileprivate`"Geçerli dosyanın dışında hiçbir şeyin bunu kullanmasına izin verme" için kullanın .
-   `public`"Herkesin, her yerde bunu kullanmasına izin ver" için kullanın .

Öğrenciler için bazen faydalı olan fazladan bir seçenek daha vardır, o da şudur: `private(set)`. Bu, "herkesin bu özelliği okumasına izin verin, ancak yalnızca benim yöntemlerimin yazmasına izin verin" anlamına gelir. Bunu ile kullanmış olsaydık , bu , yapının dışına `BankAccount`yazdırabileceğimiz anlamına gelirdi , ancak yalnızca ve değeri gerçekten _değiştirebilirdik ._`account.funds``deposit()``withdraw()`

Bu durumda, fonlar için en iyi seçim olduğunu düşünüyorum `private(set)`: cari banka hesap bakiyesini istediğiniz zaman okuyabilirsiniz, ancak benim mantığımdan geçmeden değiştiremezsiniz.

Düşünürseniz, erişim kontrolü gerçekten sizin ve ekibinizdeki diğer geliştiricilerin yapabileceklerini sınırlamakla ilgilidir ve bu mantıklıdır! Swift'in bizi hata yapmaktan alıkoymasını sağlayabilirsek, bu her zaman akıllıca bir hareket olur.

**Önemli:** Bir veya daha fazla özellik için erişim kontrolü kullanıyorsanız `private`, muhtemelen kendi başlatıcınızı oluşturmanız gerekecektir.