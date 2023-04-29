#yazılım #swift 

Bir kutu, mantıksal olarak ilgili bilgi ve bileşenlerden oluşan görsel olarak farklı bir grup oluşturur.

![[boxes.png   | 500]]

Varsayılan olarak, bir kutu içeriğini arayüzün geri kalanından ayırmak için görünür bir kenarlık veya arka plan rengi kullanır. Bir kutu ayrıca bir başlık içerebilir.

## En iyi uygulamalar

**Bir kutuyu içeren görünümüne kıyasla nispeten küçük tutmayı tercih edin.** Bir kutunun boyutu, içeren pencerenin veya ekranın boyutuna yaklaştıkça, gruplandırılmış içeriğin ayrılmasını iletmede daha az etkili hale gelir ve diğer içeriği kalabalık hale getirebilir.

**Bir kutu içinde ek gruplamayı iletmek için dolgu ve hizalama kullanmayı düşünün.** Bir kutunun kenarlığı ayrı bir görsel öğedir - alt grupları tanımlamak için iç içe kutular eklemek, arayüzünüzü meşgul ve kısıtlı hissettirebilir.

## İçerik

**Kutunun içeriğini netleştirmeye yardımcı oluyorsa, kısa ve öz bir tanıtım başlığı sağlayın.** Bir kutunun görünümü, insanların içeriğinin ilişkili olduğunu anlamalarına yardımcı olur, ancak ilişki hakkında daha fazla ayrıntı sağlamak mantıklı olabilir. Ayrıca, bir başlık VoiceOver kullanıcılarının kutuda karşılaştıkları içeriği tahmin etmelerine yardımcı olabilir.

**Bir başlığa ihtiyacınız varsa, içeriği açıklayan kısa bir ifade yazın.** Cümle tarzı büyük harf kullanın. Başlığa iki nokta üst üste eklediğiniz ayarlar bölmesinde bir kutu kullanmadığınız sürece noktalama işaretlerini sonlandırmaktan kaçının.

## Platform değerlendirmeleri

*tvOS veya watchOS'ta desteklenmez.*

### iOS, iPadOS

Varsayılan olarak, iOS ve iPadOS kutulardaki ikincil ve üçüncül arka plan [renklerini](https://developer.apple.com/design/human-interface-guidelines/foundations/color) kullanır.

### macOS

Varsayılan olarak, macOS üzerinde bir kutunun başlığını görüntüler.