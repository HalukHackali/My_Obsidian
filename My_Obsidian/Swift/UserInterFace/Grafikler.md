#swift #yazılım 

**Grafik, verileri grafiksel, ulaşılabilir bir şekilde iletmenize yardımcı olur.**

![  | 400 ](https://developer.apple.com/design/human-interface-guidelines/images/intro/components/charts-intro_2x.png) 

Etkili bir grafik, bir veri kümesindeki birkaç önemli bilgiyi vurgulayarak insanların içgörü kazanmasına ve karar vermesine yardımcı olur. Örneğin, insanlar aşağıdakiler için bir grafik kullanabilir:

- Yaklaşan hava koşullarının planlarını nasıl etkileyebileceğini öğrenin
- Geçmiş performansı anlamak ve eğilimleri keşfetmek için hisse senedi fiyatlarını analiz edin
- İlerlemelerini izlemek ve yeni hedefler belirlemek için fitness verilerini gözden geçirin

Deneyiminizi geliştirmek için grafik tasarlama hakkında bilgi edinmek için bkz. [Grafik verileri](https://developer.apple.com/design/human-interface-guidelines/patterns/charting-data); geliştirici rehberliği için bkz. [Swift Charts kullanarak grafik oluşturma](https://developer.apple.com/documentation/charts/creating-a-chart-using-swift-charts).

## anotomi

Grafik, bir veri kümesindeki değerleri gösteren ve onlar hakkında bilgi ileten birkaç grafik öğesi içerir.

![Eksenler, ızgara çizgileri, işaretler, onaylar, eksen değer etiketleri ve genel grafik alanı gibi grafik bileşenlerini tanımlayan işaretlere sahip bir çubuk grafiğin diyagramı.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/charts-anatomy_2x.png)

*İşaret*, bir veri değerinin görsel bir temsilidir. Her değeri bir işarete atayarak bir veya daha fazla veri değeri serisi sağlayarak bir grafik oluşturursunuz. Çubuk grafik, çizgi grafik veya dağılım grafiği gibi görüntülemek istediğiniz grafiğin stilini belirtmek için çubuk, çizgi veya nokta gibi bir işaret türü seçersiniz (rehberlik için bkz. [İşaretler](#marks)). Bir grafikte münferit veri değerlerini tasvir etme genel görevine *grafik*, işaretleri içeren alana ise *arsa alanı* denir.

Bir değeri göstermek için, her işaret türü, sayılar, tarihler veya kategoriler gibi veri değerlerini konum, renk veya yükseklik gibi görsel özelliklerle eşleştiren bir ölçek tarafından belirlenen görsel öznitelikleri kullanır. Örneğin, bir çubuk işareti, bir değerin büyüklüğünü temsil etmek için belirli bir yüksekliği ve değerin meydana geldiği zamanı temsil etmek için belirli bir konumu kullanabilir.

İnsanlara bir grafiğin görsel özelliklerini yorumlamaları için ihtiyaç duydukları bağlamı vermek için, birkaç farklı biçim alabilen açıklayıcı içerik sağlarsınız.

Bir dizi işaretle temsil edilen veriler için bir referans çerçevesi tanımlamaya yardımcı olması için bir *eksen* kullanabilirsiniz. Birçok grafik, çizim alanının kenarlarında bir çift eksen görüntüler - bir yatay ve bir dikey - burada her eksen zaman, miktar veya kategori gibi bir değişkeni temsil eder.

Bir eksen, insanların eksen boyunca 0, %50 ve %100 gibi önemli değerlerin konumunu görsel olarak bulmalarına yardımcı olan referans noktaları olan *onay işaretleri* içerebilir. Birçok grafik, insanların işareti bir eksene yakın olmadığında bir veri değerini görsel olarak tahmin etmelerine yardımcı olmak için her biri arsa alanı boyunca bir onay işaretinden uzanan *ızgara çizgilerini* görüntüler.

Ayrıca, insanların verileri yorumlamasına ve iletmek istediğiniz temel bilgileri vurgulamasına yardımcı olmak için grafik öğelerini tanımlamanın birden fazla yolu vardır. Örneğin, eksenler, ızgara çizgileri, onay işaretleri veya işaretler gibi öğeleri adlandıran *etiketler* ve yardımcı teknolojiler kullanan kişiler için grafik öğelerini tanımlayan *erişilebilirlik etiketleri* sağlayabilirsiniz. Bağlam ve ek ayrıntılar sağlamak için açıklayıcı başlıklar, altyazılar ve ek açıklamalar oluşturabilirsiniz. Gerektiğinde, farklı değer kategorilerini belirtmek için renk veya şekil kullanımı gibi bir işaretin konumuyla ilgili olmayan grafik özelliklerini açıklayan bir efsane de oluşturabilirsiniz.

Net, doğru açıklamalar, bir grafiği daha ulaşılabilir ve erişilebilir hale getirmeye yardımcı olabilir; grafiğinizin erişilebilirliğini iyileştirmenin ek yolları hakkında bilgi edinmek için bkz. [Bir grafiğin erişilebilirliğini artırma](#enhancing-the-accessibility-of-a-chart).

## İşaretler

**Veriler hakkında iletmek istediğiniz bilgilere göre bir işaret türü seçin.** En tanıdık işaret türlerinden bazıları çubuk, çizgi ve noktadır; bu ve diğer işaret türleri hakkında geliştirici rehberliği için bkz. [Swift Charts](https://developer.apple.com/documentation/charts).

*Çubuk* işaretleri, insanların farklı kategorilerdeki değerleri karşılaştırmasına veya bir bütün olarak çeşitli parçaların göreceli oranlarını görüntülemesine yardımcı olan grafiklerde iyi çalışır. İnsanların zaman içinde değişen verileri anlamalarına yardımcı olmak için kullanıldığında, çubuk grafikler özellikle her değer bir günde atılan toplam adım sayısı gibi bir toplamı temsil çildiğinde iyi çalışır.

![Ağustos ayında her gün için adım sayısını gösteren bir çubuk grafiğin diyagramı.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/bar-marks_2x.png)

*Çizgi* işaretleri, değerlerin zaman içinde nasıl değiştiğini de gösterebilir. Bir çizgi grafikte, bir çizgi tüm veri değerlerini bir veri serisinde birbirine bağlar. Çizginin eğimi, veri değerleri arasındaki değişimin büyüklüğünü ortaya çıkarır ve insanların genel eğilimleri görselleştirmesine yardımcı olabilir.

![Bir hisse senedinin beş yıllık bir süre boyunca performansını gösteren bir çizgi grafiğinin diyagramı.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/line-marks_2x.png)

*Nokta* işaretleri, tek tek veri değerlerini görsel olarak farklı işaretler olarak göstermenize yardımcı olur. Bir dizi nokta işareti, verilerinizin iki farklı özelliğinin birbiriyle nasıl ilişkili olduğunu gösterebilir ve insanların bireysel veri değerlerini incelemesine ve aykırı değerleri ve kümeleri tanımlamasına yardımcı olabilir.

![Beş-and-a-half-month dönemi boyunca dakika başına kalp atışlarının günlük okumalarını gösteren bir point-mark grafiğinin diyagramı.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/point-marks_2x.png)

**Grafiğinize netlik kattığında işaret türlerini birleştirmeyi düşünün.** Örneğin, zaman içinde bir değişiklik göstermek için bir çizgi grafiği kullanırsanız, tek tek veri noktalarını vurgulamak için satırın üstüne nokta işaretleri eklemek isteyebilirsiniz. Noktaları bir çizgiyle birleştirerek, insanların genel eğilimi anlamalarına yardımcı olurken aynı zamanda bireysel değerlere de dikkat çekebilirsiniz.

## Eksenler

**Grafiğinizin anlamına bağlı olarak sabit veya dinamik bir eksen aralığı kullanın.** *Sabit* bir aralıkta, eksenin üst ve alt sınırları asla değişmezken, *dinamik* bir aralıkta üst ve alt sınırlar mevcut verilere göre değişebilir. Belirli minimum ve maksimum değerler tüm olası veri değerleri için anlamlı olduğunda sabit bir aralık kullanmayı düşünün. Örneğin, insanlar bir pilin mevcut şarjının minimum %0 (tamamen boş) ve maksimum değeri %100 (tamamen dolu) olduğunu gösteren bir grafik bekler.

![Şarjın %0 ile %100 arasında sabit bir aralıkta değişebileceği, zaman içindeki pil şarjını göstermek için bir grafik kullanan iPhone'daki Pil Ayarları'nın kısmi bir ekran görüntüsü.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/fixed-range-axis_2x.png)
Şarjın %0 ile %100 arasında sabit bir aralıkta değişebileceği, zaman içindeki pil şarjını göstermek için bir grafik kullanan iPhone'daki Pil Ayarları'nın kısmi bir ekran görüntüsü.

Buna karşılık, olası veri değerleri büyük ölçüde değişebiliyorsa ve işaretlerin kullanılabilir çizim alanını doldurmasını istediğinizde dinamik bir aralık kullanmayı düşünün. Örneğin, Sağlık uygulamasının Adımlar tablosundaki Y ekseni aralığının üst sınırı değişir, böylece belirli bir zaman dilimindeki en fazla adım sayısı grafiğin en üstüne yakındır.

![Tek bir gün için toplam adım sayısını gösteren Sağlık uygulamasının Adımlar tablosunun kısmi bir ekran görüntüsü.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/dynamic-range-axis-large_2x.png)
Tek bir gün için toplam adım sayısını gösteren Sağlık uygulamasının Adımlar tablosunun kısmi bir ekran görüntüsü.

![Bir aylık dönemde günlük ortalama adım sayısını gösteren Sağlık uygulamasının Adımlar tablosunun kısmi bir ekran görüntüsü.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/bar-marks_2x.png)
Bir aylık dönemde günlük ortalama adım sayısını gösteren Sağlık uygulamasının Adımlar tablosunun kısmi bir ekran görüntüsü.

**İşaret türüne ve grafik kullanımına göre alt sınırın değerini tanımlayın.** Örneğin, Y ekseninin alt sınırı için sıfır kullandığınızda çubuk grafikler iyi çalışabilir, çünkü bunu yapmak, insanların değerlerinin makul bir tahminini elde etmek için tek tek çubukların göreceli yüksekliklerini görsel olarak karşılaştırmasına olanak tanır. Buna karşılık, sıfırın daha düşük bir sınırını tanımlamak bazen değerler arasındaki anlamlı farklılıkları ayırt etmeyi daha zor hale getirebilir. Örneğin, alt sınır için her zaman sıfır kullanan bir kalp atış hızı grafiği, dinlenme ve aktif okumalar arasındaki önemli farklılıkları gizleyabilir, çünkü farklılıklar sıfırdan uzak bir aralıkta meydana gelir.

**Bir eksen için onay işareti ve ızgara çizgisi etiketlerinde tanıdık değer dizilerini tercih edin.** Örneğin, 0, 5, 10 vb. gibi ortak bir sayı dizisi kullanırsanız, insanların bir bakışta her onay değerinin önceki değer artı beşe eşit olduğunu bilmesi muhtemeldir. 1, 6, 11 vb. gibi bir dizi aynı kuralı izlese de, bu yaygın değildir, bu nedenle çoğu insanın değerler arasındaki aralığı düşünmek için fazladan zaman harcaması muhtemeldir.

**Izgara çizgilerinin ve etiketlerin görünümünü bir grafiğin kullanım durumlarına göre uyarlayın.** Çok fazla ızgara çizgisi görsel olarak bunaltıcı olabilir ve insanları verilerden uzaklaştırabilir; çok az ızgara çizgisi bir işaretin değerini tahmin etmeyi zorlaştırabilir. Bu öğelerin uygun yoğunluğunu ve görsel ağırlığını belirlemenize yardımcı olmak için, arayüzdeki bir grafiğin bağlamını, desteklediğiniz etkileşimleri ve grafiğin etkinleştirdiğiniz görevleri göz önünde bulundurun. Örneğin, insanlar bir grafikle etkileşime girerek bireysel veri noktalarını inceleyebilirse, verilerin görsel olarak belirgin kalmasını sağlamak için daha az ızgara çizgisi ve açık etiket rengi kullanabilirsiniz.

## Açıklayıcı içerik

**İnsanların bir grafiği görüntülemeden önce ne yaptığını anlamalarına yardımcı olan açıklamalar yazın.** Bir grafiğin amacını ve işlevselliğini açıklayan bilgi açısından zengin başlıklar ve etiketler sağladığınızda, insanlara dalmadan ve ayrıntıları incelemeden önce ihtiyaç duydukları bağlamı verirsiniz. Bağlamı bu şekilde sağlamak, VoiceOver kullanıcıları ve belirli bilişsel engelli türleri olanlar için özellikle önemlidir, çünkü daha fazla araştırmaya karar vermeden önce çizelgenizin amacını ve birincil mesajını anlamak için açıklamalarınıza güvenirler.

**Herkes için ulaşılabilir ve kullanışlı olmasına yardımcı olmak için grafiğinizin ana mesajını özetleyin.** Bir grafiği kullanmanın birincil nedeni, ana mesajı destekleyen verileri görüntülemek olsa da, insanların onu hızlı bir şekilde kavrayabilmesi için temel bilgileri özetlemek önemlidir. Örneğin, Weather, önümüzdeki saat için beklenen yağışı kısaca tanımlayan bir başlık ve altyazı sağlayarak, insanlara grafiğin ayrıntılarını incelemelerine gerek kalmadan en önemli bilgileri verir.

![Önümüzdeki altmış dakika için tahmin edilen yağışı tanımlamak için kısa ve sade bir dil kullanan Hava Durumu uygulamasının kısmi bir ekran görüntüsü.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/descriptive-content_2x.png)
Önümüzdeki altmış dakika için tahmin edilen yağışı tanımlamak için kısa ve sade bir dil kullanan Hava Durumu uygulamasının kısmi bir ekran görüntüsü.

## En iyi uygulamalar

**Çeşitli grafik öğelerinin göreceli öneminin iletilmesine yardımcı olan tutarlı bir görsel hiyerarşi oluşturun.** Tipik olarak, açıklamaların ve eksenlerin verilerle rekabet etmeden ek bağlam sağlamasına izin verirken, verilerin kendisinin en belirgin olmasını istersiniz.

**Kompakt bir ortamda, insanlara bir grafiği rahatça incelemek için yeterli alan sağlamak için arsa alanının genişliğini en üst düzeye çıkarın.** Önemli verilerin belirli bir genişliğe iyi oturmasına yardımcı olmak için, dikey eksendeki etiketlerin netliği kaybetmeden mümkün olduğunca kısa olmasını sağlayın. Ayrıca, bir başlık gibi grafiğin diğer alanlarındaki birimleri tanımlamayı ve bunu yapmak önemli bilgileri gizlemediğinde, arsa alanının içine kategori adı gibi daha uzun bir eksen etiketi yerleştirmeyi düşünebilirsiniz.

**Uygulamanızdaki her grafiği erişilebilir hale getirin.** Grafiklerin — tüm infografikler gibi — içeriği nasıl algıladıklarına bakılmaksızın herkes tarafından tamamen erişilebilir olması gerekir. Örneğin, insanların ekranı görmelerine gerek kalmadan bilgi almasına ve gezinmesine yardımcı olmak için ekran içeriğini açıklayan VoiceOver'ı desteklemek önemlidir (SeOver hakkında daha fazla bilgi edinmek için bkz. [Vision](https://www.apple.com/accessibility/vision/)). Grafiğinizin bileşenlerini tanımlayan erişilebilirlik etiketleri sağlamanın yanı sıra, Ses Grafiklerini de kullanarak VoiceOver deneyimini geliştirebilirsiniz. [Audio Graphs,](https://developer.apple.com/documentation/accessibility/audio_graphs) bir grafiğin veri değerlerini ve eğilimlerini sesli olarak temsil eden bir dizi ton oluşturan VoiceOver'a grafik bilgileri sağlar; ayrıca ek bağlam sağlayan high-level metin özetleri sunmanıza olanak tanır. Rehberlik için bkz. [Grafiğin erişilebilirliğini artırma](#enhancing-the-accessibility-of-a-chart).

**İnsanların mantıklı olduğunda verilerle etkileşime girmesine izin verin, ancak kritik bilgileri ortaya çıkarmak için etkileşim gerektirmez.** Örneğin, hisse senetlerinde, insanlar genellikle bir hisse senedinin zaman içindeki performansıyla en çok ilgilenir, bu nedenle uygulama, insanların bir gün, üç ay veya beş yıl gibi seçtiği zaman dilimindeki performansı gösteren bir çizgi grafik görüntüler. İnsanlar ek ayrıntıları keşfetmek isterlerse, seçilen zamanda değeri ortaya çıkararak çizgi grafiğinde dikey bir göstergeyi sürükleyebilirler.

**Herkesin bir grafikle etkileşime girmesini kolaylaştırın.** Bazen, grafik işaretleri bir parmakla veya işaretçiyle hedeflenemeyecek kadar küçüktür, bu da grafiğinizi motor kontrolü azaltılmış ve herkes için rahatsız edici kişiler için kullanmayı zorlaştırır. Bu durumda, vurulan hedefi tüm arsa alanını içerecek şekilde genişletmeyi ve insanların çeşitli değerleri ortaya çıkarmak için bölgeyi fırçalamasına izin vermeyi düşünün.

**Klavye komutlarını (tam klavye erişimi dahil) veya Anahtar Kontrolü kullanırken etkileşimli bir grafikte gezinmeyi kolaylaştırın.** Varsayılan olarak, bu giriş türleri, bir veri dosyasındaki değerler dizisi gibi doğrusal bir dizideki tek tek ekran öğelerini ziyaret etme eğilimindedir. Grafiğinizde özel bir gezinme deneyimini etkinleştirmek istiyorsanız, bunu yapmanın iki ana yolu. İlk yol, grafiğinizin bilgileri aracılığıyla mantıklı ve öngörülebilir bir yol belirtmek için erişilebilirlik API'lerini ( [accessibilityRespondsToUserInteraction(_:)](https://developer.apple.com/documentation/swiftui/label/accessibilityrespondstouserinteraction%28_:%29/) gibi) kullanmaktır. Örneğin, insanların ileri geri atlamak yerine X ekseni boyunca gezinmesine izin vermek isteyebilirsiniz. İkinci yol — ki bu özellikle çok büyük bir veri kümesi sunmanız gerekiyorsa — insanların tüm bireysel veri noktalarında gezinmek yerine odak noktasını değerlerin alt kümeleri arasında hareket ettirmesine izin vermektir. Grafiğiniz etkileşimli olmasa bile, bu özelleştirmelerin her ikisinin de VoiceOver deneyimini geliştirebileceğini unutmayın. Rehberlik için bkz. [Erişilebilirlik > Gezinme](https://developer.apple.com/design/human-interface-guidelines/foundations/accessibility#navigation).

**İnsanların bir grafikteki önemli değişiklikleri fark etmelerine yardımcı olun.** Örneğin, insanlar işaretlerin veya eksenlerin ne zaman değiştiğini fark etmezlerse, bir grafiği yanlış okuyabilirler. Bu tür değişiklikleri canlandırma, insanların onları fark etmesine yardımcı olabilir, ancak VoiceOver kullanıcılarının ve animasyonları kapatan kişilerin onlar hakkında bilgi sahibi olmasını sağlamak için değişiklikleri başka şekillerde de vurgulamanız gerekir. Geliştirici rehberliği için bkz.[UIAccessibility.Notification](https://developer.apple.com/documentation/uikit/uiaccessibility/notification) (UIKit) veya [NSAccessibility.Notification](https://developer.apple.com/documentation/appkit/nsaccessibility/notification) (AppKit).

**Bir grafiği çevreleyen arayüz öğeleriyle hizalayın.** Örneğin, bir grafiğin ön kenarını bir ekrandaki diğer görünümlerin ön kenarıyla hizalamak genellikle iyi çalışır. Bir grafikte temiz bir ön kenarı korumanın bir yolu, her dikey ızgara çizgisinin etiketini arka tarafında görüntülemektir. Y eksenini grafiğin arka tarafına kaydırmayı da düşünebilirsiniz, böylece onay etiketleri grafiğin ön kenarını geçmez. Hiçbir şeyle ilişkili görünmeyen bir etiketle sonuçlanırsanız, onu bir ızgara çizgisine sabitlemek için bir onay işareti kullanabilirsiniz.

## Renk

Arayüzünüzün diğer tüm bölümlerinde olduğu gibi, bir grafikte renk kullanmak, bilgileri netleştirmenize, markanızı uyandırmanıza ve görsel süreklilik sağlamanıza yardımcı olabilir. Rengi herkesin takdir edebileceği şekillerde kullanma konusunda genel rehberlik için bkz. [Kapsayıcı renk](https://developer.apple.com/design/human-interface-guidelines/foundations/color#inclusive-color).

**Farklı veri parçalarını ayırt etmek veya bir grafikteki temel bilgileri iletmek için yalnızca renge güvenmekten kaçının.** Bir grafikte anlamlı renk kullanmak, farklılıkları vurgulamak ve önemli ayrıntıları yükseltmek için iyi çalışır, ancak bu bilgileri iletmek için alternatif yollar eklemek çok önemlidir, böylece insanlar renkleri ayırt edip edemediklerine bakılmaksızın grafiğinizi kullanabilirler. Rengi tamamlamanın bir yolu, verilerin farklı bölümlerini tasvir etmek için farklı şekiller veya desenler kullanmaktır. Örneğin, Kırmızı ve siyah renkler kullanmanın yanı sıra Sağlık, kan basıncının iki bileşenini temsil eden nokta işaretlerinde iki farklı şekil kullanır.

![Sistolik değerleri temsil etmek için kırmızı bir daire ve diyastolik değerleri temsil etmek için siyah bir elmas kullanan bir kan basıncı çizelgesinin diyagramı.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/chart-colors_2x.png)
Sistolik değerleri temsil etmek için kırmızı bir daire ve diyastolik değerleri temsil etmek için siyah bir elmas kullanan bir kan basıncı çizelgesinin diyagramı.

**Bitişik renk alanları arasında görsel ayrım ekleyerek anlamaya yardımcı olun.** Örneğin, işaretleri tek bir satırda veya sütunda istifleyen bir çubuk grafikte, her işarete farklı bir renk atamak yaygındır. Bu tasarımda, işaretler arasına ayırıcılar eklemek, insanların tek tek olanları ayırt etmesine yardımcı olabilir.

![Medya, uygulamalar ve fotoğraflar gibi öğeler tarafından alınan göreceli alanı göstermek için farklı renklerde birkaç parça içeren tek bir çubuk işareti kullanan iPhone Depolama Ayarları'nın kısmi bir ekran görüntüsü. Çubuk, her bir parça çifti arasında dar bir boş alan şeridi içerir.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/chart-colors-stacked_2x.png)
Medya, uygulamalar ve fotoğraflar gibi öğeler tarafından alınan göreceli alanı göstermek için farklı renklerde birkaç parça içeren tek bir çubuk işareti kullanan iPhone Depolama Ayarları'nın kısmi bir ekran görüntüsü. Çubuk, her bir parça çifti arasında dar bir boş alan şeridi içerir.

## Bir grafiğin erişilebilirliğini geliştirmek

Bir grafik oluşturmak için Swift Charts kullandığınızda, değerini açıklayan her işaret (veya işaret grubu) için varsayılan bir erişilebilirlik öğesine ek olarak varsayılan bir [Ses Grafikleri](https://developer.apple.com/documentation/accessibility/audio_graphs) uygulaması elde edersiniz.

**VoiceOver kullanıcılarına grafiğiniz hakkında daha fazla bilgi vermek için Ses Grafiklerini kullanmayı düşünün.** Swift Charts'ın sağladığı varsayılan Audio Graphs uygulamasını, insanların grafiğinizin amacını ve ana özelliklerini anlamalarına yardımcı olmak için VoiceOver'ın konuştuğu bir grafik başlığı ve açıklayıcı özet sağlayarak özelleştirebilirsiniz. Ses Grafikleri kullanmıyorsanız, grafiğin yapısına ve amacına genel bir bakış sağlamanız gerekir. Örneğin, grafiğin türünü tanımlamanız gerekir - çubuk veya çizgi gibi - her eksenin neyi temsil ettiğini açıklamanız ve üst ve alt eksen sınırları gibi ayrıntıları açıklamanız gerekir.

**ÖNEMLİ**Açıklayıcı bir erişilebilirlik etiketi gerektiren bir görüntünün aksine, bir grafiğin genellikle her önemli veya etkileşimli öğe için bir erişilebilirlik etiketi sunması gerekir. Grafiğinizin amacına ve işaretlerinin kapsamına ve yoğunluğuna bağlı olarak, her bir işareti tanımlamanın gerekli olup olmadığına veya işaret gruplarını tanımlamak için erişilebilirlik deneyimini iyileştirip iyileştirmediğine karar vermeniz gerekir. Bazı durumlarda, daha ayrıntılı bir sürümü ortaya çıkaran bir düğmede bir grafiğin küçük bir sürümünü kullandığınızda olduğu gibi, grafiğin kısa ve üst düzey bir açıklamasını sağlayan tek bir erişilebilirlik etiketi kullanmak mantıklı olabilir.

**Grafiğinizin amacını destekleyen erişilebilirlik etiketleri yazın.** Örneğin, Haritalar, her biri rotanın küçük bir bölümünün yüksekliğini temsil eden bir dizi ayrı çubuk kullanarak bir bisiklet rotası için yükseklik değişikliklerini gösterir. Grafiğin amacı, insanlara bireysel yükseklikler sağlamak değil, tüm rota için arazi hakkında bir fikir vermektir. Bu nedenle Haritalar, bir grup çubuktaki yükseklik değişikliklerini özetleyen erişilebilirlik etiketleri sağlar; çubuk başına bir erişilebilirlik etiketi sağlamaz. Buna karşılık, Sağlık, Adımlar tablosundaki her çubuk için bir erişilebilirlik etiketi sunar, çünkü grafiğin amacı insanlara her izleme dönemi için gerçek adım sayılarını vermektir.

![Haritalar'da, yolculuğun toplam mesafesi üzerindeki yükseklik aralığını gösteren bir çubuk grafiğin kısmi ekran görüntüsü. Grafiğin üstünde, toplam yükseklik değerlerinin yaklaşık beşte birini içeren bir VoiceOver odak göstergesi görülebilir.](https://developer.apple.com/design/human-interface-guidelines/components/content/charts/images/bar-chart-with-voiceover-focus_2x.png)
Haritalar'da, yolculuğun toplam mesafesi üzerindeki yükseklik aralığını gösteren bir çubuk grafiğin kısmi ekran görüntüsü. Grafiğin üstünde, toplam yükseklik değerlerinin yaklaşık beşte birini içeren bir VoiceOver odak göstergesi görülebilir.

Bu bisiklet yükseklik tablosunun odaklanmış bölümü için VoiceOver, "0,4 milden 0,7 mil arasında: 70 fit tırmanın" açıklamasını sağlar.

Aşağıdaki yönergeler, grafik öğeleri için yararlı erişilebilirlik etiketleri yazmanıza yardımcı olabilir.

- **Netliğe ve kapsamlılığa öncelik verin.** Genel olarak, onunla ilişkili tarih veya konum gibi insanların onu anlamasına yardımcı olacak bağlamı da dahil etmediğiniz sürece, yalnızca bir veri değerini bildirmek nadiren yeterlidir. Ses Grafiklerinin veya genel bakışınızın sağladığı bir eksen adı gibi, insanların başka şekillerde elde edebileceği bilgileri tekrarlamadan bir değerin bağlamını kısa bir şekilde tanımlamayı hedefleyin. Öğenin ayrıntılarının kısa bir açıklamasıyla bağlam belirleme bilgilerini takip edin.
- **Öznel terimler kullanmaktan kaçının.** Öznel kelimeler - hızlı, yavaş ve neredeyse olduğu gibi - verileri yorumlamanızı iletir. İnsanların kendi yorumlarını oluşturmalarına yardımcı olmak için açıklamalarınızda gerçek değerleri kullanın.
- **Potansiyel olarak belirsiz biçimlerden ve kısaltmalardan kaçınarak veri açıklamalarında netliği en üst düzeye çıkarın.** Örneğin, "6 Haziran" kullanmak "6/6" kullanmaktan daha nettir; benzer şekilde, "60 dakika" veya "60 metre" yazmak "60m" kısaltmasını kullanmaktan daha nettir.
- **Grafiğin ayrıntılarının neye benzediklerini değil, neyi temsil ettiğini açıklamaya odaklanın.** İnsanların iki farklı veri serisini görsel olarak ayırt etmelerine yardımcı olmak için kırmızı ve mavi renkleri kullanan bir grafik düşünün. Her serinin neyi temsil ettiğini tanımlayan erişilebilirlik etiketleri oluşturmak çok önemlidir, ancak onları görsel olarak temsil eden renkleri tanımlamak gereksiz bilgiler ekleyebilir ve dikkat dağıtıcı olabilir.
- **Belirli bir eksene atıfta bulunurken uygulamanız genelinde tutarlı olun.** Örneğin, her zaman önce X ekseninden bahsederseniz, insanlar bir açıklamada hangi eksenin alakalı olduğunu bulmak için daha az zaman harcayabilir.

**Yardımcı teknolojilerden eksenler ve onaylar için görünür metin etiketlerini gizleyin.** Eksen ve onay etiketleri, insanların bir grafikteki eğilimleri görsel olarak değerlendirmesine ve işaret değerlerini tahmin etmesine yardımcı olur. VoiceOver kullanıcıları, erişilebilirlik etiketleri ve Ses Grafikleri aracılığıyla işaret değerlerini ve trend bilgilerini alabilir, böylece genellikle görünür etiketlerdeki içeriğe ihtiyaç duymazlar.

## Platform değerlendirmeleri

*iOS, iPadOS, macOS veya tvOS için ek husus yok.*

### watchOS

**Genel olarak, watchOS uygulamanızda karmaşık grafik etkileşimleri gerektirmekten kaçının.** Mümkün olduğunca, insanların bir bakışta alabilecekleri odaklanmış, kullanışlı bilgileri görüntülemeyi ve değer kattıklarında basit etkileşimleri etkinleştirmeyi tercih edin. Uygulamanızın başka bir platformda bir sürümünü de sunuyorsanız, daha fazla ayrıntı görüntülemek ve grafiğinizle daha fazla etkileşim sağlamak için kullanmayı düşünün. Örneğin, watchOS'taki Kalp Atış Hızı, kullanıcının geçerli gün için kalp atış hızı verilerinin bir grafiğini görüntülerken, iPhone'daki Sağlık uygulaması birkaç farklı süre için kalp atış hızı verilerini görüntüler ve insanların bireysel işaretleri incelemesine olanak tanıyan etkileşimlere olanak tanır.

## kaynaklar

#### İlgili

- [Grafik verileri](https://developer.apple.com/design/human-interface-guidelines/patterns/charting-data)

#### Geliştirici belgeleri

- [Hızlı Grafikler](https://developer.apple.com/documentation/Charts)

#### Videolar

- [![](https://devimages-cdn.apple.com/wwdc-services/images/124/6694/6694_wide_250x141_2x.jpg)<br>Grafiklerle uygulama deneyimleri tasarlayın<br>WWDC22](https://developer.apple.com/videos/play/wwdc2022/110342/)
- [![](https://devimages-cdn.apple.com/wwdc-services/images/124/6692/6692_wide_250x141_2x.jpg)<br>Etkili bir grafik tasarlayın<br>WWDC22](https://developer.apple.com/videos/play/wwdc2022/110340/)
- [![](https://devimages-cdn.apple.com/wwdc-services/images/124/6633/6633_wide_250x141_2x.jpg)<br>Merhaba Swift Grafikleri<br>WWDC22](https://developer.apple.com/videos/play/wwdc2022/10136/)