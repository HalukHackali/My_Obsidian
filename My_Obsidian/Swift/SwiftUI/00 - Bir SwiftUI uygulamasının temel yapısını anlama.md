#swift #swiftui 

Yeni bir SwiftUI uygulaması oluşturduğunuzda, bir dizi dosya ve toplamda belki 20 satır kod alırsınız.

Xcode içinde, proje gezgini olarak adlandırılan soldaki alanda aşağıdaki dosyaları görmelisiniz:

-   WeSplitApp.swift, uygulamanızı başlatmak için kod içerir. Uygulama başladığında bir şey yaratır ve onu her zaman canlı tutarsanız, onu buraya koyarsınız.
-   ContentView.swift, programınız için ilk kullanıcı arabirimini (UI) içerir ve bu projedeki tüm işi burada yapacağız.
-   Assets.xcassets, uygulamanızda kullanmak istediğiniz resimlerden oluşan bir koleksiyon olan bir _varlık kataloğudur ._ Burada uygulama simgeleri, iMessage çıkartmaları ve daha fazlasıyla birlikte renkler de ekleyebilirsiniz.
-   İçeriği Önizleme, içinde Preview Assets.xcassets bulunan bir gruptur - bu başka bir varlık kataloğudur, bu sefer özellikle, kullanıcı arabirimlerinizi tasarlarken kullanmak istediğiniz örnek resimler için, size nasıl görünebilecekleri hakkında bir fikir vermek için. program çalışıyor.

**İpucu:** Xcode yapılandırmasına bağlı olarak, proje gezgininizde dosya uzantılarını görebilir veya görmeyebilirsiniz. Bunu, Xcode'un tercihlerine giderek, Genel sekmesini seçerek ve ardından Dosya Uzantıları seçeneğini ayarlayarak kontrol edebilirsiniz.

Bu proje için tüm çalışmalarımız, Xcode'un sizin için açmış olacağı ContentView.swift'te gerçekleşecek. En üstte bazı yorumlar var - başlangıçta iki eğik çizgi ile işaretlenen şeyler - ve bunlar Swift tarafından yok sayılır, böylece kodunuzun nasıl çalıştığına dair açıklamalar eklemek için bunları kullanabilirsiniz.

Yorumların altında on kadar kod satırı var:

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

Kendi kodumuzu yazmaya başlamadan önce, tüm bunların ne işe yaradığını gözden geçirmeye değer, çünkü birkaç şey yeni olacak.

İlk olarak `import SwiftUI`Swift'e, SwiftUI çerçevesi tarafından bize verilen tüm işlevleri kullanmak istediğimizi söyler. Apple, makine öğrenimi, ses oynatma, görüntü işleme ve daha fazlası gibi şeyler için bize birçok çerçeve sağlar, bu nedenle programımızın her şeyi kullanmak istediğini varsaymak yerine, yüklenebilmeleri için hangi parçaları kullanmak istediğimizi söyleriz.

İkincisi, protokole uygun olduğunu söyleyerek `struct ContentView: View`adında yeni bir yapı oluşturur . SwiftUI'den gelir ve ekranda çizmek istediğiniz her şey tarafından benimsenmesi gereken temel protokoldür - tüm metinler, düğmeler, resimler ve daha fazlası, diğer görünümleri birleştiren kendi düzenleriniz de dahil olmak üzere görünümlerdir.`ContentView``View``View`

Üçüncüsü, adında ilginç bir türü olan `var body: some View`yeni bir hesaplanmış özelliği tanımlar : . Bu, düzenimiz olan protokole uyan bir şey döndüreceği anlamına gelir . Perde arkasında bu, düzenimizdeki her şeye bağlı olarak çok karmaşık bir veri türünün döndürülmesine neden olacaktır, ancak bunun için endişelenmemize gerek olmadığı anlamına gelir.`body``some View``View``some View`

Protokolün yalnızca bir gereksinimi vardır, o da , döndürülen `View`adında hesaplanan bir özelliğe sahip olmanızdır . Görünüm yapılarınıza daha fazla özellik ve yöntem ekleyebilirsiniz (ve ekleyeceksiniz), ancak gerekli olan tek şey budur.`body``some View``body`

Dördüncüsü, `Text("Hello, world!")`“Merhaba dünya!” dizesini kullanarak bir metin görünümü oluşturur. Metin görünümleri, ekrana çizilen basit statik metin parçalarıdır ve gerektiğinde birden çok satıra otomatik olarak sarılır.

`padding()`Beşinci olarak, metin görünümünde yöntemin çağrıldığını göreceksiniz . _Bu, Swift'in değiştirici_ dediği şeydir , bunlar küçük bir farkla normal yöntemlerdir: her zaman hem orijinal verilerinizi hem de istediğiniz ekstra değişikliği içeren yeni bir görünüm döndürürler. Bizim durumumuzda bu, `body`yalnızca normal bir metin görünümü değil, dolgulu bir metin görünümü döndürecektir.

Yapının altında protokole uyan `ContentView`bir yapı göreceksiniz . Bu kod parçası aslında App Store'a giden son uygulamanızın bir parçasını oluşturmayacak, bunun yerine özellikle Xcode'un kullanması içindir, böylece kodunuzun yanında UI tasarımınızın bir önizlemesini gösterebilir.`ContentView_Previews``PreviewProvider`

Bu önizlemeler, tuval adı verilen ve genellikle doğrudan kodunuzun sağ tarafında görülebilen bir Xcode özelliğini kullanır. İsterseniz önizleme kodunu özelleştirebilirsiniz ve bunlar yalnızca tuvalin mizanpajlarınızı gösterme şeklini etkiler - çalıştırılan gerçek uygulamayı değiştirmez.

Kanvas, iPhone 13 Pro veya iPod touch gibi belirli bir Apple aygıtı kullanılarak otomatik olarak önizlenir. Bunu değiştirmek için mevcut cihaz için Xcode pencerenizin üst ortasına bakın, ardından üzerine tıklayın ve bir alternatif seçin. Bu, kodunuzun daha sonra sanal iOS simülatöründe nasıl çalıştırılacağını da etkiler.

**Önemli:** Xcode pencerenizde tuvali görmüyorsanız Düzenleyici menüsüne gidin ve Canvas'ı seçin.

Sıklıkla kodunuzdaki bir hatanın Xcode tuvalinin güncellenmesini durdurduğunu görürsünüz - "Otomatik önizleme güncellemesi duraklatıldı" gibi bir şey görürsünüz ve bunu düzeltmek için Sürdür'e basabilirsiniz. Bunu sık sık yapacağınız için size önemli bir kısayol önereyim: Option+Cmd+P, Devam Et'e tıklamakla aynı işlevi görür.