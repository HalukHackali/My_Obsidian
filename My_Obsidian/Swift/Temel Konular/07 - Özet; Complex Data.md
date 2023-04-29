#swift #yazılım 

Artık basit veri türlerinin ötesine geçtik ve bunları birlikte gruplandırmanın ve hatta numaralandırmaları kullanarak kendi veri türlerimizi oluşturmanın yollarını aramaya başladık. Öyleyse özetleyelim:

-   Diziler, birçok değeri tek bir yerde saklamamıza ve ardından tamsayı indekslerini kullanarak okumamıza izin verir. Diziler her zaman özelleştirilmelidir, böylece belirli bir tür içerirler ve `count`, `append()`ve gibi yararlı işlevlere sahiptirler `contains()`.
-   Sözlükler ayrıca birçok değeri tek bir yerde saklamamıza izin verir, ancak belirttiğimiz anahtarları kullanarak bunları okumamıza izin verir. `contains()`Anahtar için belirli bir türe ve değer için başka bir türe sahip olacak şekilde uzmanlaşmaları ve ve gibi dizilere benzer işlevselliğe sahip olmaları gerekir `count`.
-   _Kümeler, birçok değeri tek bir yerde depolamanın üçüncü_ bir yoludur, ancak bu öğeleri depoladıkları sırayı seçemiyoruz. Setler, belirli bir öğeyi içerip içermediklerini bulmada gerçekten etkilidir.
-   Numaralandırmalar, Swift'te kendi basit türlerimizi oluşturmamıza izin verir, böylece kullanıcının gerçekleştirebileceği eylemler listesi, yazabileceğimiz dosya türleri veya gönderilecek bildirim türleri gibi bir dizi kabul edilebilir değer belirtebiliriz. kullanıcı
-   Swift, bir sabit veya değişken içindeki veri türünü her zaman bilmelidir ve atadığımız verilere dayanarak bunu anlamak için çoğunlukla _tür çıkarımını kullanır._ _Ancak, belirli bir türü zorlamak için tür açıklamasını_ kullanmak da mümkündür .

Diziler, sözlükler ve kümeler arasında açık ara en çok dizileri kullanacağınızı söylemek yanlış olmaz. Bundan sonra sözlükler gelir ve kümeler uzak bir üçüncü sırada gelir. Bu, setlerin kullanışlı olmadığı anlamına gelmez, ancak onlara ne zaman ihtiyacınız olduğunu bileceksiniz!