#yazılım #swift 


* * *

Bir görüntü görünümü, şeffaf veya opak bir arka plan üzerinde tek bir görüntü (veya bazı durumlarda animasyonlu bir görüntü dizisi) görüntüler.

<img src="https://developer.apple.com/design/human-interface-guidelines/images/intro/components/image-view-intro_2x.png" alt="" width="308" height="173"> 

Bir görüntü görünümünde, görüntüyü belirli bir konuma sığdırmak için genişletebilir, ölçeklendirebilir, boyutlandırabilir veya sabitleyebilirsiniz. Görüntü görünümleri genellikle etkileşimli değildir.

## En iyi uygulamalar

**Görünümün birincil amacı sadece bir görüntüyü görüntülemek olduğunda bir görüntü görünümü kullanın.** Bir görüntünün etkileşimli olmasını isteyebileceğiniz nadir durumlarda, bir görüntü görünümüne düğme davranışları eklemek yerine görüntüyü görüntülemek için sistem tarafından sağlanan bir [düğme](https://developer.apple.com/design/human-interface-guidelines/components/menus-and-actions/buttons) yapılandırın.

**Arayüzünüzde bir simge görüntülemek istiyorsanız, resim görünümü yerine bir sembol veya arayüz simgesi kullanmayı düşünün.** [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/foundations/sf-symbols), çeşitli renkler ve opaklıklarla oluşturabileceğiniz geniş bir aerodinamik, vektör tabanlı görüntüler kitaplığı sağlar. Bir [arayüz simgesi](https://developer.apple.com/design/human-interface-guidelines/foundations/icons) (glif veya şablon görüntüsü olarak da adlandırılır), tipik olarak şeffaf olmayan piksellerin renk alabileceği bir bitmap görüntüsüdür. Hem semboller hem de arayüz simgeleri, insanların seçtiği vurgu renklerini kullanabilir.

## İçerik

Görüntü görünümü, PNG, JPEG ve PDF gibi çeşitli biçimlerde zengin görüntü verileri içerebilir. Daha fazla rehberlik için bkz. [Görüntüler](https://developer.apple.com/design/human-interface-guidelines/foundations/images).

**Görüntülere metin bindirirken dikkatli dikkatli olmak.** Metni görüntülerin üzerine birleştirmek hem görüntünün netliğini hem de metnin okunabilirliğini azaltabilir. Sonuçları iyileştirmeye yardımcı olmak için metnin görüntüyle iyi kontrast oluşturduğundan emin olun ve bir metin gölgesi veya arka plan katmanı eklemek gibi metin nesnesini öne çıkarmanın yollarını düşünün.

**Animasyonlu bir dizideki tüm görüntüler için tutarlı bir boyut kullanmayı hedefleyin.** Görüntüleri görünüme uyacak şekilde önceden ölçeklendirdiğde, sistemin herhangi bir ölçeklendirme yapması gerekmez. Sistemin ölçeklendirmeyi yapması gereken durumlarda, tüm görüntüler aynı boyut ve şekilde olduğunda performans genellikle daha iyidir.

## Platform değerlendirmeleri

*iOS veya iPadOS için ek husus yok.*

### macOS

**Uygulamanızın düzenlenebilir bir resim görünümüne ihtiyacı varsa, bir görüntü kuyusu kullanın.** [Görüntü kuyusu](https://developer.apple.com/design/human-interface-guidelines/components/selection-and-input/image-wells), içeriğini temizlemek için Sil tuşunu kopyalamayı, yapıştırmayı, sürüklemeyi ve kullanmayı destekleyen bir görüntü görünümüdür.

**Tıklanabilir bir görüntü yapmak için görüntü görünümü yerine resim düğmesi kullanın.** Bir [resim düğmesi](https://developer.apple.com/design/human-interface-guidelines/components/menus-and-actions/buttons/#image-buttons) bir resim veya simge içerir, bir görünümde görünür ve anında uygulamaya özgü bir eylem başlatır.

### tvOS

Birçok tvOS görüntüsü, derinlik hissi yaratmak için birden fazla katmanı şeffaflıkla birleştirir. Rehberlik için bkz. [Katmanlı Görüntüler](https://developer.apple.com/design/human-interface-guidelines/foundations/images/#layered-images).

### watchOS

**Mümkün olduğunda animasyonlar oluşturmak için SwiftUI'yi kullanın.** Gerekirse, bir görüntü öğesi içindeki bir görüntü dizisini canlandırmak için WatchKit'i kullanabilirsiniz. Geliştirici rehberliği için bkz. [WKImageAnimatable](https://developer.apple.com/documentation/watchkit/wkimageanimatable).