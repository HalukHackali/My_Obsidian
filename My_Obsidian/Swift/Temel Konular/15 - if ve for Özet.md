#swift #yazılım 

Önceki bölümlerde koşullar ve döngüler hakkında çok şey ele aldık, o yüzden özetleyelim:

-   `if`Bir koşulun doğru olup olmadığını kontrol etmek için ifadeler kullanırız . İstediğiniz herhangi bir koşulda geçebilirsiniz, ancak sonuçta bir Boolean değerine indirgenmesi gerekir.
-   `else`İsterseniz, diğer koşulları kontrol etmek için bir blok ve/veya birden fazla `else if`blok ekleyebilirsiniz . Swift bunları sırayla yürütür.
-   Koşulları kullanarak birleştirebilirsiniz `||`; bu, alt koşullardan biri doğruysa tüm koşulun doğru olduğu anlamına gelir veya `&&`her iki alt koşul da doğruysa tüm koşulun doğru olduğu anlamına gelir.
-   Aynı türden kontrolleri çok tekrarlıyorsanız, `switch`bunun yerine bir ifade kullanabilirsiniz. Bunlar her zaman ayrıntılı olmalıdır, bu da varsayılan bir servis talebi eklemek anlamına gelebilir.
-   Vakalarınızdan biri `switch`kullanıyorsa `fallthrough`, bu, Swift'in daha sonra aşağıdaki vakayı yürüteceği anlamına gelir. Bu yaygın olarak kullanılmaz.
-   Üçlü koşul operatörü, WTF'yi kontrol etmemizi sağlar: Ne, Doğru, Yanlış. İlk başta okuması biraz zor olsa da bunun SwiftUI'de _çok_ kullanıldığını göreceksiniz .
-   `for`döngüler diziler, kümeler, sözlükler ve aralıklar üzerinde döngü yapmamızı sağlar. `_`Öğeleri bir döngü değişkenine atayabilir ve döngü içinde kullanabilirsiniz veya döngü değişkenini yok saymak için alt çizgi, , kullanabilirsiniz .
-   `while`döngüler, bir koşul yanlış olana kadar çalışmaya devam edecek özel döngüler oluşturmamızı sağlar.
-   `continue`Sırasıyla veya kullanarak döngü öğelerinin bazılarını veya tümünü atlayabiliriz `break`.

Bu da başka bir devasa yeni malzeme yığını, ancak koşullar ve döngülerle artık gerçekten yararlı yazılımlar oluşturmak için yeterince bilginiz var – bir deneyin!