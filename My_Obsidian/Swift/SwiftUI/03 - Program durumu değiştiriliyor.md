#swift #swiftui 

SwiftUI geliştiricileri arasında "görüşlerimizin durumlarının bir işlevi olduğu" şeklinde bir söz vardır, ancak bu yalnızca bir avuç sözcük olsa da, ilk başta sizin için oldukça anlamsız gelebilir.

Bir dövüş oyunu oynuyor olsaydınız, birkaç can kaybedebilir, biraz puan toplayabilir, biraz hazine toplayabilir ve belki de bazı güçlü silahlar edinebilirdiniz. Programlamada bunlara _durum_ diyoruz - oyunun şu anda nasıl olduğunu açıklayan aktif ayarlar koleksiyonu.

SwiftUI'nin görüşlerinin durumlarının bir işlevi olduğunu söylediğimizde, kullanıcı arabiriminizin görünümünün - insanların görebildikleri ve etkileşimde bulunabilecekleri şeylerin - programınızın durumu tarafından belirlendiğini kastediyoruz. Örneğin, adlarını bir metin alanına girene kadar Devam'a dokunamazlar.

Bunu, SwiftUI'de bir başlık dizesi ve düğmeye dokunulduğunda çalıştırılan bir eylem kapatma ile oluşturulabilen bir düğme ile uygulamaya koyalım:

```swift
struct ContentView: View {
    var tapCount = 0

    var body: some View {
        Button("Tap Count: \(tapCount)") {
            tapCount += 1
        }
    }
}
```

Bu kod yeterince makul görünüyor: "Dokunma Sayısı" artı düğmeye dokunma sayısı yazan bir düğme oluşturun, ardından `tapCount`düğmeye her dokunulduğunda 1 ekleyin.

Ancak inşa etmeyecek; bu geçerli bir Swift kodu değil. Gördüğünüz gibi, `ContentView`sabit olarak yaratılabilecek bir yapıdır. Yapıları öğrendiğiniz zamanları düşünürseniz, bunun _değişmez olduğu_ anlamına gelir - değerlerini özgürce değiştiremeyiz.

Özellikleri değiştirmek isteyen yapı yöntemleri oluştururken, örneğin `mutating`: anahtar kelimesini eklememiz gerekir. `mutating func doSomeWork()`Ancak Swift, mutasyona uğramış hesaplanmış özellikler yapmamıza izin vermiyor, bu da yazamayacağımız anlamına geliyor `mutating var body: some View`- buna izin verilmiyor.

Bu, bir çıkmaza girmiş gibi görünebilir: programımız çalışırken değerleri değiştirebilmek istiyoruz, ancak görüşlerimiz yapılar olduğu için Swift bize izin vermiyor.

Neyse ki, Swift bize _mülk sarmalayıcı_ adı verilen özel bir çözüm sunuyor : mülklerimizin önüne yerleştirebileceğimiz ve onlara etkili bir şekilde süper güçler veren özel bir nitelik. Bir düğmeye dokunulma sayısı gibi basit program durumunun saklanması durumunda, SwiftUI'den `@State`şu şekilde adlandırılan bir özellik sarmalayıcı kullanabiliriz:

```swift
struct ContentView: View {
    @State var tapCount = 0

    var body: some View {
        Button("Tap Count: \(tapCount)") {
            self.tapCount += 1
        }
    }
}
```

Bu küçük değişiklik, programımızın çalışması için yeterlidir, böylece şimdi onu oluşturabilir ve deneyebilirsiniz.

`@State`yapıların sınırlamaları üzerinde çalışmamıza izin verir: Yapılar sabit olduğu için özelliklerini değiştiremeyeceğimizi biliyoruz, ancak bu değerin _değiştirilebilen_`@State` bir yerde SwiftUI tarafından ayrı olarak depolanmasına izin verir .

Evet, biraz hile gibi geliyor ve bunun yerine neden sınıfları kullanmadığımızı merak edebilirsiniz - bunlar serbestçe değiştirilebilir _._ Ama inanın bana, buna değer: ilerledikçe SwiftUI'nin yapılarınızı sık sık yok ettiğini ve yeniden yarattığını öğreneceksiniz, bu nedenle onları küçük ve basit tutmak performans için önemlidir.

**İpucu:** SwiftUI'de program durumunu saklamanın birkaç yolu vardır ve hepsini öğreneceksiniz. `@State`tek bir görünümde saklanan basit özellikler için özel olarak tasarlanmıştır. Sonuç olarak, Apple `private`bu özelliklere erişim denetimi eklememizi önerir, örneğin: `@State private var tapCount = 0`.
