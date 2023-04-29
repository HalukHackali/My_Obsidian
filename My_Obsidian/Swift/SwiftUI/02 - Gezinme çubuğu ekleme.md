#swift #swiftui 

iOS, istersek, üstteki sistem saati ve alttaki ana sayfa göstergesi dahil olmak üzere ekranın herhangi bir yerine içerik yerleştirmemize izin verir. Bu harika görünmüyor, bu nedenle varsayılan olarak SwiftUI, bileşenlerin sistem kullanıcı arayüzü veya yuvarlatılmış köşeler tarafından kapatılamayacakları bir alana - güvenli alan olarak bilinen bir alana - yerleştirilmesini _sağlar_ .

Bir iPhone 13'te güvenli alan, çentiğin hemen altındaki alanı ev göstergesinin hemen üstüne kadar kapsar. Bunun gibi bir kullanıcı arayüzü ile çalışırken görebilirsiniz:

```swift
struct ContentView: View {
    var body: some View {
        Form {
            Section {
                Text("Hello, world!")
            }
        }
    }
}
```

Bunu iOS simülatöründe çalıştırmayı deneyin - Xcode penceresinin sol üst köşesindeki Yürüt düğmesine veya Cmd+R tuşlarına basın.

Formun çentiğin altında başladığını göreceksiniz, bu nedenle varsayılan olarak formumuzdaki satır tamamen görünür durumdadır. Bununla birlikte, formlar da kaydırılabilir, bu nedenle simülatörde kaydırırsanız, satırı yukarı taşıyabileceğinizi göreceksiniz, böylece saatin altına girecek ve bu da her ikisinin de okunmasını zorlaştıracaktır.

Bunu düzeltmenin yaygın bir yolu, ekranın üst kısmına bir gezinme çubuğu yerleştirmektir. Gezinme çubuklarının başlıkları ve düğmeleri olabilir ve SwiftUI'de ayrıca kullanıcı bir eylem gerçekleştirdiğinde bize yeni görünümler gösterme yeteneği verir.

Düğmelere ve yeni görünümlere daha sonraki bir projede geleceğiz, ancak en azından size nasıl bir gezinme çubuğu ekleyeceğinizi ve ona bir başlık vereceğinizi göstermek istiyorum, çünkü bu, formumuzu kaydırırken daha iyi görünmesini sağlar.

Metin görünümünün etrafına ekleyerek bir bölümün içine metin görünümü yerleştirebileceğimizi ve benzer şekilde `Section`bölümü a içine yerleştirebileceğimizi gördünüz . `Form`Aynı şekilde bir gezinme çubuğu ekliyoruz, ancak burada adı `NavigationView`.

```swift
var body: some View {
    NavigationView {
        Form {
            Section {
                Text("Hello, world!")
            }
        }
    }
}
```

Bu kodu Xcode tuvalinde gördüğünüzde, kullanıcı arayüzünüzün üst kısmında büyük bir gri alan olduğunu fark edeceksiniz. Bu bizim hareket halindeki gezinme çubuğumuz ve simülatörde kodunuzu çalıştırırsanız, ekranın üst kısmına doğru hareket ederken formun çubuğun altında kaydığını göreceksiniz.

Genellikle gezinme çubuğuna bir tür başlık koymak isteyeceksiniz ve bunu, içine yerleştirdiğiniz her şeye bir _değiştirici_ ekleyerek yapabilirsiniz .

Formumuz için gezinme başlığını ayarlamak üzere bir değiştirici eklemeyi deneyelim:

```swift
NavigationView {
    Form {
        Section {
            Text("Hello, world!")
        }
    }
    .navigationTitle("SwiftUI")
}
```

`.navigationTitle()`Değiştiriciyi formumuza eklediğimizde , Swift aslında bir gezinme başlığı artı sağladığınız tüm mevcut içeriklere sahip yeni bir form oluşturur.

Gezinme çubuğuna bir başlık eklediğinizde, o başlık için büyük bir yazı tipi kullanıldığını fark edeceksiniz. Başka bir değiştirici ekleyerek küçük bir yazı tipi elde edebilirsiniz:

```swift
.navigationBarTitleDisplayMode(.inline)
```

Apple'ın bu büyük ve küçük başlıkları nasıl kullandığını Ayarlar uygulamasında görebilirsiniz: ilk ekranda büyük metinle "Ayarlar" yazar ve sonraki ekranlarda başlıkları küçük metinle gösterir.