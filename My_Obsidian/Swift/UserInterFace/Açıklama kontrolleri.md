#yazılım #swift 

Açıklama kontrolleri, belirli kontroller veya görünümlerle ilgili bilgileri ve işlevleri ortaya çıkarır ve gizler.

 ![   | 400](https://developer.apple.com/design/human-interface-guidelines/images/intro/components/disclosure-control-intro-dark_2x.png)

## En iyi uygulamalar

**İlgili olana kadar ayrıntıları gizlemek için bir açıklama kontrolü kullanın.** İnsanların kullanma olasılığı en yüksek olan kontrolleri açıklama hiyerarşisinin en üstüne yerleştirin, böylece varsayılan olarak gizlenmiş daha gelişmiş işlevlerle her zaman görünür olurlar. Bu organizasyon, insanların çok fazla ayrıntılı seçenekle onları bunaltmadan önce en temel bilgilere odaklanmalarına yardımcı olur.

## Açıklama üçgenleri

Bir açıklama üçgeni, bir görünüm veya öğe listesiyle ilişkili bilgileri ve işlevleri gösterir ve gizler. Örneğin, Keynote, bir sunuyu dışa aktarırken gelişmiş seçenekleri göstermek için bir açıklama üçgeni kullanır ve Finder, liste görünümünde bir klasör yapısında gezinirken hiyerarşiyi aşamalı olarak ortaya çıkarmak için açıklama üçgenlerini kullanır.

- [Çöktü](#)
- [Genişletilmiş](#)

- ![Kapalı bir açıklama üçgenini gösteren bir ekran görüntüsü.](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/disclosure-controls/images/disclosure-triangle-before_2x.png)
    

Bir açıklama üçgeni, içeriği gizlendiğinde ön kenardan içe ve içeriği görünür olduğunda aşağı doğru işaret eder. Açıklama üçgenine tıklamak veya dokunmak bu iki durum arasında geçiş yapar ve görünüm içeriği barındırmak için buna göre genişler veya daralır.

**Açıklama üçgeni kullanırken tanımlayıcı bir etiket sağlayın.** Etiketlerinizin "Gelişmiş Seçenekler" gibi neyin ifşa edildiğini veya gizlendiğini gösterdiğinden emin olun.

Geliştirici rehberliği için [NSBezelStyleDisclosure'a](https://developer.apple.com/documentation/appkit/nsbezelstyle/nsbezelstyledisclosure) bakın.

## Açıklama düğmeleri

Bir açıklama düğmesi, belirli bir denetimle ilişkili işlevselliği gösterir ve gizler. Örneğin, macOS Kaydet sayfası Farklı Kaydet metin alanının yanında bir açıklama düğmesi gösterir. İnsanlar bu düğmeyi tıklattığında veya dokunduğunda, Kaydet iletişim kutusu, belgeleri için bir çıktı konumu seçmek üzere gelişmiş gezinme seçenekleri sunmak üzere genişler.

- [Çöktü](#)
- [Genişletilmiş](#)

- ![Bir metin alanını takip eden kapalı bir açıklama düğmesini gösteren bir ekran görüntüsü.](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/disclosure-controls/images/disclosure-button-before_2x.png)
    

Bir açıklama düğmesi, içeriği gizlendiğinde aşağı ve içeriği görünür olduğunda yukarıyı gösterir. Açıklama düğmesine tıklamak veya dokunmak bu iki durum arasında geçiş yapar ve görünüm içeriği barındırmak için buna göre genişler veya daralır.

**Gösterdiği ve gizlediği içeriğin yanına bir açıklama düğmesi yerleştirin.** Kontrol ile bir kişi bir düğmeyi tıkladığında veya dokunduğunda görünen genişletilmiş seçenekler arasında net bir ilişki kurun.

**Tek bir görünümde birden fazla açıklama düğmesi kullanmayın.** Birden fazla açıklama düğmesi karmaşıklık ekler ve kafa karıştırıcı olabilir.

Geliştirici rehberliği için [NSBezelStyleRoundedDisclosure'a](https://developer.apple.com/documentation/appkit/nsbezelstyle/nsbezelstyleroundeddisclosure) bakın.

## Platform değerlendirmeleri

*macOS için ek husus yok. tvOS veya watchOS'ta desteklenmez.*

### iOS, iPadOS

Açıklama kontrolleri, SwiftUI [DisclosureGroup](https://developer.apple.com/documentation/swiftui/disclosuregroup) görünümüyle iOS ve iPadOS'ta mevcuttur.