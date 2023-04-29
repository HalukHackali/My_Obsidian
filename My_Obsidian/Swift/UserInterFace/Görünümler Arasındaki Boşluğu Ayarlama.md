#yazılım #swift 

**İçeriğinizin hizalamasını ve aralığını belirtin.**

Bilgileri görüntüleyen görünümleri tanımlarken fazladan alanın nereye gitmesi gerektiğini bildirerek düzeni ayarlayabilirsiniz. Mizanpajınızın nasıl uyum sağlamasını istediğinize bağlı olarak farklı araçlar seçebilirsiniz. Görünümler arasındaki boşluğu yönetmek için kullanılan araçlardan bazıları görünümlerdir, örneğin [`Spacer`](https://developer.apple.com/documentation/SwiftUI/Spacer). Bir görünüme bitişik alanı etkileyen görünüm değiştiriciler de vardır, örneğin . Bazı durumlarda, bir görünümün veya değiştiricinin parametresi olarak varsayılan olmayan bir değer sağlayarak bir düzeni etkilersiniz. [`padding(_:_:)`](https://developer.apple.com/documentation/SwiftUI/View/padding%28_:_:%29)

Görünümler arasındaki aralığı değiştirmeye yönelik bazı farklı stratejileri göstermek için bu örnekte bir dizi tren vagonu kullanılmaktadır. [Her trenin üç görünümü vardır — ön, orta ve arka bölüm — ve SF](https://developer.apple.com/design/resources/#sf-symbols) Symbols'deki tren vagonu simgelerini kullanır . Bu örnekler, [`HStack`](https://developer.apple.com/documentation/SwiftUI/HStack)yatay aralığı göstermek için bir kullanır. Aynı ilkeler, SwiftUI'deki dikey eksen ve diğer yığın ve ızgara görünümleri için geçerlidir.

Bu kapsayıcı görünümlerinin birçoğu varsayılan olarak bir miktar negatif boşluk içerir, bu nedenle içeriğinizi ayarlayın ve aralığı özelleştirmeden önce varsayılanların nasıl göründüğünü görmek için bir ilk yapın.[`PreviewProvider`](https://developer.apple.com/documentation/SwiftUI/PreviewProvider)

Aşama 1

Bu özel görünüm, [`Image`](https://developer.apple.com/documentation/SwiftUI/Image)görünümün kapsamını göstermek için pembe bir arka planla birlikte bir tren vagonunun SF Sembolünü görüntüleyen bir görünümü tanımlar.

Her yerde aynı değiştiricileri ve parametreleri belirtmek zorunda kalmadan birden çok yerde benzer görünümlere sahip olabilmek için kendi özel görünümlerinizi tanımlayabilirsiniz.

Adım 2

Kullanımdaki bu özel görünümün bir örneğini burada bulabilirsiniz . Bu görünüm bildirimi, yalnızca trenin hangi bölümünü temsil ettiğini belirtir. Yapı, görünümü karşılık gelen sembolle tanımlar ve bir arka plan ekler.`TrainCar`

`TrainCar`

`Image`

Aşama 3

Bu, bir tren oluşturmak için ön, orta ve arka olmak üzere [`HStack`](https://developer.apple.com/documentation/SwiftUI/HStack)üç görünüm içerir . Kod, görünümlere herhangi bir özel boşluk veya dolgu eklemez , ancak tren vagonlarının çerçeveleri arasında hala biraz boşluk vardır.`TrainCar`

`HStack`

`TrainCar`

`HStack`SwiftUI'nin yerleşik koleksiyon görünümlerinin çoğu gibi bir , varsayılan olarak alt görünümleri arasına biraz boşluk koyar.

TrainCar.swift

```swift
import SwiftUI 

struct DefaultSpacing: View { var body: some View { Text("Default Spacing") HStack { TrainCar(.rear) TrainCar(.middle) TrainCar(.front) } TrainTrack() } } 

struct DefaultSpacing_Previews: PreviewProvider { static var previews: some View { VStack { DefaultSpacing() } } }
```
![[Pasted image 20230416031855.png  | 600]]


[Bölüm 2](https://developer.apple.com/tutorials/swiftui-concepts/adjusting-the-space-between-views#Customize-a-containers-spacing)

## Bir kapsayıcının aralığını özelleştirme

an öğesinin varsayılan aralığı `HStack`tüm düzenler için doğru değildir. Yığının alt görünümleri arasında sabit bir boşluk, Dinamik Tür ile ölçeklenen boşluk veya hiç boşluk belirtemezsiniz.

Aşama 1

`spacing`an parametresi, görünümleri `HStack`arasındaki aralığı özelleştirir. Bu değer, varsayılan aralık yerine `20`ön ve orta görünümler arasına 20 nokta ve orta ve arka görünümler arasına 20 nokta boşluk koyar.`TrainCar`

`TrainCar`

Adım 2

Bu tren vagonları SF sembolleri olduğundan, akım değiştiğinde boyutları değişir . Bu trenin mesafesi orantılı olarak ayarlanır. Bunda , parametrenin değeri görünümün özelliğidir .[`dynamicTypeSize`](https://developer.apple.com/documentation/SwiftUI/EnvironmentValues/dynamicTypeSize)

`HStack`

`spacing`

`trainCarSpace`

`ScaledSpacing`

Aşama 3

Özellik sarmalayıcı , özelliği geçerli yazı tipi boyutuyla orantılı olarak değişecek şekilde yapılandırır .[`ScaledMetric`](https://developer.apple.com/documentation/SwiftUI/ScaledMetric)

`trainCarSpace`

[`body`](https://developer.apple.com/documentation/SwiftUI/Font/body)

Adım 4

`0`Burada parametre için değerinin kullanılması, `spacing`görünümler arasındaki tüm boşluğu kaldırır. Bunda `HStack`tren vagonları yan yana duruyor.

ÖzelAralık.swift

```
 import SwiftUI 

  struct ScaledSpacing: View { @ScaledMetric var trainCarSpace = 5 

 

 var body: some View { Text("Scaled Spacing") HStack(spacing:trainCarSpace) { TrainCar(.rear) TrainCar(.middle) TrainCar(.front) } TrainTrack() } } 

  struct ScaledSpacing_Previews: PreviewProvider { static var previews: some View { VStack { ScaledSpacing() } } }
```

![[Pasted image 20230416031950.png  | 600]]

[Bölüm 3](https://developer.apple.com/tutorials/swiftui-concepts/adjusting-the-space-between-views#Add-padding-around-subviews)

## Alt görünümlerin çevresine dolgu ekleyin

Bir görünümün dış kenarlarına, o görünüm ile komşu görünümler arasına veya bir pencerenin veya sahnenin kenarına biraz boşluk bırakmak için dolgu ekleyebilirsiniz.

Aşama 1

[`padding(_:_:)`](https://developer.apple.com/documentation/SwiftUI/View/padding%28_:_:%29)herhangi bir parametre olmadan dört kenarın çevresine boşluk koyar. Varsayılan dolgunun boyutu, görünümün özniteliklerine ve görünümün göründüğü ortama bağlı olarak değişir.

Aşama 3

Bu örnek, parametrede belirli bir dolgu miktarını tanımlar `length`.

Yazı tipi değişikliklerine yanıt olarak aralığı ayarlamak için a öğesini de kullanabilirsiniz .`ScaledMetric`

Adım 4

Dolgu değiştiricinin etkisi, değiştirdiği görünüme bağlıdır.

Görünümleri içeren yığına değiştiricinin uygulanması, dolguyu tren vagonları yerine yığının kenarlarına yerleştirir.[`padding(_:_:)`](https://developer.apple.com/documentation/SwiftUI/View/padding%28_:_:%29)

`TrainCar`

VarsayılanPadding.swift

```
 import SwiftUI 

  struct SpecificPadding: View { var body: some View { Text("Specific Padding") HStack { TrainCar(.rear) TrainCar(.middle) .padding(5) .background(Color("customBlue")) TrainCar(.front) } TrainTrack() } } 

  struct SpecificPadding_Previews: PreviewProvider { static var previews: some View { VStack { SpecificPadding() } } }
```

![[Pasted image 20230416032026.png  | 600]]

[Bölüm 4](https://developer.apple.com/tutorials/swiftui-concepts/adjusting-the-space-between-views#Add-a-view-to-create-space)

## Alan oluşturmak için bir görünüm ekleyin

Alan oluşturmak için bir içerik görünümünü değiştirmenin yanı sıra, herhangi bir içerik görüntülemeden düzeninizi değiştiren görünmez bir görünüm ekleyerek de alan oluşturabilirsiniz.

Aşama 1

Görünümler arasındaki bu, `Spacer()`içerik görünümlerini olabildiğince birbirinden uzaklaştırır.

Her biri için bir minimum genişlik belirtebilir `Spacer`veya bitişik içeriğin tüm alana ihtiyacı varsa sıfıra kadar sıkıştırmasına izin verebilirsiniz.

Adım 2

`opacity`Bu düzen , doğru miktarda alan kaplamak için o görünümün görünmez bir sürümünü oluşturmak üzere değiştiriciyi kullanarak bir görünümün boyutuna bağlı olan bir alan miktarını belirtir .

Aşama 3

A, `ZStack`en büyük görünümünün boyutuna uyum sağlar, böylece bu yığındaki görünmez görünüm, orta tren vagonunun etrafında dolgu gibi bir görsel görünüm oluşturur.

Spacer.swift ekleniyor

```
 import SwiftUI 

  struct AddingPlaceholder: View { var body: some View { Text("Spacing with a Placeholder") HStack { TrainCar(.rear) TrainCar(.middle) .opacity(0) .background(Color("customBlue")) TrainCar(.front) 

 

 } TrainTrack() } } 

  struct AddingPlaceholder_Previews: PreviewProvider { static var previews: some View { VStack { AddingPlaceholder() } } }
```

![[Pasted image 20230416032053.png | 600]]

Sonraki

## Durum ve bağlamalarla kullanıcı arayüzünüzdeki değişiklikleri yönlendirme

Durumu kullanarak bir görünümde veri bağımlılıklarını belirtin ve bu bağımlılıkları bağlamaları kullanarak diğer görünümlerle paylaşın.

[Başlamak](https://developer.apple.com/tutorials/swiftui-concepts/driving-changes-in-your-ui-with-state-and-bindings)