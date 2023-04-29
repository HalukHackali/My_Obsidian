#swift #yazılım 

Swift'de koşulları kontrol etmenin son bir yolu var.

Örneğin, birinin yaşını saklayan `age` adında bir sabit oluşturabiliriz , ardından `canVote` o kişinin oy kullanıp kullanamayacağını saklayacak ikinci bir sabit adında ikinci bir sabit oluşturabiliriz:

```swift
let age = 18
let canVote = age >= 18 ? "Yes" : "No"
```

Bu kod çalıştığında, `age` 18 olarak ayarlandığı `canVote` için “Evet” olarak ayarlanacaktır .

Gördüğünüz gibi, üçlü operatör üç kısma ayrılmıştır: bir kontrol ( `age >= 18`), koşul doğru olduğunda ("Evet") ve koşul yanlış olduğunda ("Hayır"). Bu , aynı zamamda, tam olarak normal `if` ve `else` blok gibi çalışır.

Yardımcı olursa, [Scott Michaud](https://translate.google.com/website?sl=auto&tl=tr&hl=tr&u=https://twitter.com/scottmichaud/status/1087510756634083330) yararlı bir anımsatıcı önerdi: WTF. "What, true, false" anlamına gelir ve kodumuzun sırası ile eşleşir:

-   Durumumuz nedir? Bu `age >= 18`.
-   Koşul doğru olduğunda ne yapmalı? "Evet" olarak geri gönderin, böylece `canVote`.
-   Ve koşul yanlışsa? "Hayır" geri gönderin.

Diğer bazı örneklere bakalım, 24 saat biçiminde bir saati okuyan ve iki mesajdan birini yazdıran kolay bir örnekle başlayalım:

```swift
let hour = 23
print(hour < 12 ? "It's before noon" : "It's after noon")
```

Bunun sonucu herhangi bir yere atamadığına dikkat edin - değerine bağlı olarak doğru veya yanlış durumu yazdırılır `hour`.

`count`Veya bir dizinin durumunu koşulunun bir parçası olarak okuyan ve ardından iki diziden birini geri gönderen bir dizi :

```swift
let names = ["Jayne", "Kaylee", "Mal"]   
let crewCount = names.isEmpty ? "No one" : "\(names.count) people"
print(crewCount)
```

Burada görebileceğiniz gibi, durumunuz eşitliği kontrol etmek için kullanıldığında okumak _biraz_ zorlaşıyor :`==`

```swift
enum Theme {
    case light, dark
}

let theme = Theme.dark

let background = theme == .dark ? "black" : "white"
print(background)
```

Bu `= theme ==`kısım genellikle insanların okumakta zorlandıkları kısımlardır, ancak parçalamayı unutmayın:

-   Ne ? `theme == .dark`
-   Doğru: "siyah"
-   Yanlış: “beyaz”

Bu nedenle, tema "Siyah" döndürmek için eşitse `.dark`, aksi takdirde "Beyaz" döndürmek için bunu atayın `background`.

Şimdi, üçlü operatörün neden yararlı olduğunu merak ediyor olabilirsiniz, özellikle de bizim için uygun düzenli `if`/ `else`koşullarımız varken. Bunun harika bir cevap olmadığının farkındayım, ancak bu konuda bana güvenmeniz gerekecek: Bazı zamanlar, özellikle SwiftUI ile, başka seçeneğimiz olmadığında ve bir üçlü kullanmamız _gerektiğinde ._

Saatleri kontrol etme kodumuzla ilgili sorunun kabaca ne olduğunu görebilirsiniz:

```swift
let hour = 23
print(hour < 12 ? "It's before noon" : "It's after noon")
```

Bunu kullanarak yazmak isteseydik `if`ve `else`bu geçersiz kodu yazmamız gerekirdi:

```swift
print(
    if hour < 12 {
        "It's before noon"
    } else {
        "It's after noon"
    }
)
```

Veya `print()`şu şekilde iki kez çalıştırın:

```swift
if hour < 12 {
    print("It's before noon")
} else {
    print("It's after noon")
}
```

Bu ikincisi burada iyi çalışıyor, ancak daha sonra göreceğiniz gibi SwiftUI'de neredeyse imkansız hale geliyor. Dolayısıyla, üçlü operatöre bakıp onu neden kullandığınızı merak ediyor olsanız bile, lütfen bana güvenin: önemli!