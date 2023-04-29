#swift #swiftui 


SwiftUI'nin `@State`özellik sarmalayıcısı, görünüm yapılarımızı özgürce değiştirmemize izin verir; bu, programımız değiştikçe görünüm özelliklerimizi eşleşecek şekilde güncelleyebileceğimiz anlamına gelir.

Ancak, kullanıcı arabirimi kontrolleriyle işler biraz daha karmaşıktır. Örneğin, kullanıcıların yazabileceği düzenlenebilir bir metin kutusu oluşturmak istiyorsanız, bunun gibi bir SwiftUI görünümü oluşturabilirsiniz:

```swift
struct ContentView: View {
    var body: some View {
        Form {
            TextField("Enter your name")
            Text("Hello, world!")
        }
    }
}
```

Bu, bir metin alanı ve bir metin görünümü içeren bir form oluşturmaya çalışır. Ancak, SwiftUI metnin metin alanında nerede saklanacağını bilmek istediğinden bu kod derlenmeyecektir.

Görünümlerin durumlarının bir işlevi olduğunu unutmayın; bu metin alanı, yalnızca programınızda saklanan bir değeri yansıtıyorsa bir şeyler gösterebilir. SwiftUI'nin istediği, yapımızda metin alanı içinde gösterilebilen ve ayrıca metin alanına kullanıcı ne yazarsa yazsın depolayacak bir dize özelliğidir.

Böylece kodu şu şekilde değiştirebiliriz:

```swift
struct ContentView: View {
    var name = ""

    var body: some View {
        Form {
            TextField("Enter your name", text: name)
            Text("Hello, world!")
        }
    }
}
```

Bu, bir `name`özellik ekler, ardından bunu metin alanını oluşturmak için kullanır. Bununla birlikte, bu kod _yine de_ çalışmaz çünkü Swift'in özelliği, kullanıcının metin alanına yazdığı her şeyle eşleşecek şekilde güncelleyebilmesi gerekir , bu nedenle şu şekilde `name`kullanabilirsiniz :`@State`

```swift
@State private var name = ""
```

Ancak bu yine de yeterli değil ve kodumuz yine de derlenmeyecek.

Sorun, Swift'in "bu özelliğin değerini burada göster" ile "bu özelliğin değerini burada göster, _ancak tüm değişiklikleri özelliğe geri yaz_ " arasında ayrım yapmasıdır.

Metin alanımız söz konusu olduğunda, Swift'in metindeki her şeyin aynı zamanda mülkte olduğundan emin olması gerekir `name`, böylece görüşlerimizin durumlarının bir işlevi olduğu - kullanıcının görebileceği her şeyin yalnızca olduğu - sözünü yerine getirebilir. kodumuzdaki yapıların ve özelliklerin görünür temsili.

Buna _iki yönlü bağlama_ denir: metin alanını özelliğimizin değerini gösterecek şekilde bağlarız, ancak aynı zamanda metin alanında yapılan herhangi bir değişikliğin özelliği güncellemesi için de bağlarız.

Swift'de, bu iki yönlü bağlamaları özel bir sembolle işaretleriz, böylece göze çarparlar: önlerine bir dolar işareti yazarız. Bu, Swift'e özelliğin değerini okuması gerektiğini ama aynı zamanda herhangi bir değişiklik olduğunda geri yazmasını söyler.

Yani, yapımızın doğru versiyonu şudur:

```swift
struct ContentView: View {
    @State private var name = ""

    var body: some View {
        Form {
            TextField("Enter your name", text: $name)
            Text("Hello, world!")
        }
    }
}
```

Bu kodu şimdi çalıştırmayı deneyin - beklendiği gibi metin alanına dokunabileceğinizi ve adınızı girebileceğinizi görmelisiniz.

Devam etmeden önce, metin görünümünü kullanıcının adını doğrudan metin alanlarının altında gösterecek şekilde değiştirelim:

```swift
Text("Your name is \(name)")
```

`name`Bunun yerine nasıl kullanıldığına dikkat edin `$name`? Bunun nedeni, burada iki yönlü bir bağlama istemiyoruz – değeri _okumak_ istiyoruz , evet, ancak bir şekilde geri yazmak istemiyoruz çünkü bu metin görünümü değişmeyecek.

Bu nedenle, bir özellik adından önce bir dolar işareti gördüğünüzde, bunun iki yönlü bir bağ oluşturduğunu unutmayın: özelliğin değeri okunur, aynı zamanda yazılır.