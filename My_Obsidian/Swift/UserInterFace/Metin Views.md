#yazılım #swift 

Metin görünümü, isteğe bağlı olarak düzenlenebilir olan çok satırlı, biçimli metin içeriğini görüntüler.

 <img src="https://developer.apple.com/design/human-interface-guidelines/images/intro/components/text-view-intro-dark_2x.png" alt="" width="460,8" height="259,2">

Metin görünümleri herhangi bir yükseklikte olabilir ve içerik görünümün dışına çıktığında kaydırmayı etkinleştirebilir. Varsayılan olarak, bir metin görünümündeki içerik ön kenarla hizalanır ve sistem etiketi rengini kullanır. iOS veya iPadOS'ta, bir metin görünümü düzenlenebilirse, insanlar görünümü seçtiğinde bir klavye görünür.

## En iyi uygulamalar

**Uzun, düzenlenebilir veya özel bir biçimde metin görüntülemeniz gerektiğinde bir metin görünümü kullanın.** Metin görünümleri, özel metni görüntülemek ve metin girdisi almak için en fazla seçeneği sağlamaları bakımından [metin alanlarından](https://developer.apple.com/design/human-interface-guidelines/components/selection-and-input/text-fields) ve [etiketlerden](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/labels) farklıdır. Az miktarda metin görüntülemeniz gerekiyorsa, bunun yerine bir etiket veya metin düzenlenebilirse bir metin alanı kullanmak daha kolaydır.

**Metni okunaklı tutun.** Birden fazla yazı tipini, rengi ve hizalamayı yaratıcı yollarla kullanabilseniz de, içeriğinizin okunabilirliğini korumak çok önemlidir. Dinamik Türü benimsemek iyi bir fikirdir, böylece insanlar cihazlarında metin boyutunu değiştirirse metniniz hala iyi görünür. İçeriğinizi kalın metin gibi erişilebilirlik seçenekleri etkinken de test etmelisiniz. Rehberlik için bkz. [Erişilebilirlik](https://developer.apple.com/design/human-interface-guidelines/foundations/accessibility) ve [Tipografi](https://developer.apple.com/design/human-interface-guidelines/foundations/typography).

**Yararlı metni seçilebilir hale getirin.** Bir metin görünümü hata mesajı, seri numarası veya IP adresi gibi yararlı bilgiler içeriyorsa, insanların başka bir yere yapıştırmak için seçmesine ve kopyalamasına izin vermeyi düşünün.

## Platform değerlendirmeleri

*macOS için ek husus yok.*

### iOS, iPadOS

**Uygun klavye türünü göster.** Her biri farklı bir giriş türünü kolaylaştırmak için tasarlanmış birkaç farklı klavye türü mevcuttur. Veri girişini kolaylaştırmak için, bir metin görünümünü düzenlerken görüntülediğiniz klavye içerik türüne uygun olmalıdır. Rehberlik için bkz. [Ekran klavyeleri](https://developer.apple.com/design/human-interface-guidelines/components/selection-and-input/onscreen-keyboards).

### tvOS

Metin görünümü kullanarak tvOS'ta metin görüntüleyebilirsiniz. tvOS'taki metin girişi tasarım gereği minimum olduğundan, tvOS bunun yerine düzenlenebilir metin için [metin alanları](https://developer.apple.com/design/human-interface-guidelines/components/selection-and-input/text-fields) kullanır.

### watchOS

WatchOS'ta metinleri WatchKit'te etiket olarak veya SwiftUI'de metin görünümüyle görüntüleyebilirsiniz. Rehberlik için bkz. [Etiketler](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/labels).