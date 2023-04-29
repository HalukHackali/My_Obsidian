#swift #swiftui 

Birçok uygulama, kullanıcıların bir tür girdi girmesini gerektirir - bu, onlardan bazı tercihler belirlemelerini isteyebilir, bir arabanın onları nereden almasını istediklerini onaylamalarını isteyebilir, bir menüden yemek sipariş etmek veya herhangi bir şey olabilir. benzer.

SwiftUI, bu amaç için bize `Form`. Formlar, metin ve resimler gibi statik denetimlerin kayan listeleridir, ancak metin alanları, geçiş anahtarları, düğmeler ve daha fazlası gibi kullanıcı etkileşimli denetimlerini de içerebilir.

Yalnızca varsayılan metin görünümünü içine sararak temel bir form oluşturabilirsiniz `Form`, bunun gibi:

```swift
var body: some View {
    Form {
        Text("Hello, world!")
            .padding()
    }
}
```

Xcode'un tuvalini kullanıyorsanız, oldukça çarpıcı bir şekilde değiştiğini göreceksiniz: Hello World'den önce beyaz bir ekranda ortalanmıştı, ancak şimdi ekran açık gri ve Hello World sol üstte beyaz olarak görünüyor.

Dolguyu da kaldırabilirsiniz – buna daha sonra geri döneceğiz:

```swift
Form {
    Text("Hello, world!")
}
```

Burada gördüğünüz, tıpkı Ayarlar uygulamasında göreceğiniz gibi bir veri listesinin başlangıcıdır. Verilerimizde Merhaba Dünya metni olan bir satır var, ancak daha fazlasını özgürce ekleyebilir ve hemen formumuzda görünmesini sağlayabiliriz:

```swift
Form {
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
}
```

Aslında, bir formun içinde istediğiniz kadar çok şey olabilir, ancak 10'dan fazla eklemeyi düşünüyorsanız SwiftUI, sorunları önlemek için nesneleri gruplara yerleştirmenizi gerektirir.

Örneğin, bu kod on satırlık metni gayet iyi gösterir:

```swift
Form {
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
}
```

Ancak bu, izin verilmeyen 11'i göstermeye çalışır:

```swift
Form {
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
}
```

**İpucu:** Neden 10 satıra izin verildiği halde 11'e izin verilmediğini merak ediyorsanız, bu SwiftUI'deki bir sınırlamadır: bir forma nasıl bir şey ekleneceğini, bir forma nasıl iki şey ekleneceğini, nasıl ekleneceğini anlamak için kodlanmıştır. üç şey, dört şey, beş şey ve daha fazlası, 10'a kadar, ama ötesine değil - bir yere bir çizgi çekmeleri gerekiyordu. Bir ebeveyn içindeki bu 10 çocuk sınırı aslında SwiftUI'de her yerde geçerlidir.

Formun içinde 11 şey olmasını istiyorsanız, a içine bazı satırlar koymalısınız `Group`:

```swift
Form {
    Group {
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
    }

    Group {
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
        Text("Hello, world!")
    }
}
```

Gruplar aslında kullanıcı arayüzünüzün görünüşünü değiştirmezler, sadece SwiftUI'nin bir ebeveyn içindeki on alt görünüm sınırlamasını aşmamıza izin verirler - bu, bu örnekte bir form içindeki metin görünümleridir.

_Öğeleri parçalara ayırırken formunuzun farklı görünmesini istiyorsanız_ , bunun yerine görünümü kullanmalısınız `Section`. Bu, tıpkı Ayarlar uygulamasının yaptığı gibi, formunuzu ayrı görsel gruplara ayırır:

```swift
Form {
    Section {
        Text("Hello, world!")
    }

    Section {
        Text("Hello, world!")
        Text("Hello, world!")
    }
}
```

Bir formu bölümlere ayırmanız gerektiğinde kesin ve hızlı bir kural yoktur - yalnızca ilgili öğeleri görsel olarak gruplandırmak için vardır.