#yazılım #swift 

*Tarayıcı* olarak da adlandırılan sütun görünümü, insanların bir dizi dikey sütun kullanarak bir veri hiyerarşisini görüntülemesine ve gezinmesine olanak tanır.

![[Pasted image 20230416030045.png  | 500]]

Her sütun hiyerarşinin bir seviyesini temsil eder ve veri öğelerinin yatay satırlarını içerir. Bir sütunda, iç içe geçmiş alt öğeler içeren herhangi bir üst öğe bir üçgen simgesiyle işaretlenir. İnsanlar bir ebeveyn seçtiğinde, bir sonraki sütun çocuklarını görüntüler. İnsanlar çocuğu olmayan bir öğeye ulaşana kadar bu şekilde gezinmeye devam edebilir ve ayrıca diğer veri dallarını keşfetmek için hiyerarşide geri gezinebilirler.

## En iyi uygulamalar

İnsanların seviyeler arasında sık sık ileri geri gezinme eğiliminde olduğu derin bir veri hiyerarşiniz olduğunda ve bir [listenin veya tablonun](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/lists-and-tables) sağladığı sıralama yeteneklerine ihtiyacınız olmadığında bir sütun görünümü kullanmayı düşünün. Örneğin, Finder dizin yapılarında gezinmek için bir sütun görünümü (simge, liste ve galeri görünümlerine ek olarak) sunar.

**İlk sütunda veri hiyerarşinizin kök düzeyini gösterin.** İnsanlar, hiyerarşiyi tekrar üstten gezinmeye başlamak için hızlı bir şekilde ilk sütuna geri dönebileceklerini biliyorlar.

**Görüntülenecek iç içe öğe olmadığında seçili öğe hakkında bilgi göstermeyi düşünün.** Örneğin Finder, seçilen öğenin önizlemesini ve oluşturma tarihi, değişiklik tarihi, dosya türü ve boyut gibi bilgileri gösterir.

**İnsanların sütunları yeniden boyutlandırmasına izin verin.** Bu, özellikle bazı veri öğelerinin adları varsayılan sütun genişliğine sığamayacak kadar uzunsa önemlidir.

## Platform değerlendirmeleri

*iOS, iPadOS, tvOS veya watchOS'ta desteklenmez.*

### iPadOS

iPadOS'ta hiyerarşik içeriğin sunumunu yönetmeniz gerekiyorsa, [bölünmüş](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/split-views) bir [görünüm](https://developer.apple.com/design/human-interface-guidelines/components/layout-and-organization/split-views) kullanmayı düşünün.