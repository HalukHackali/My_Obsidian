##  Döngü öğeleri break ile nasıl atlanır ve devam edilir?

#swift #yazılım 

  
Swift, bir döngüdeki bir veya daha fazla öğeyi atlamamız için bize iki yol sunar: `continue`geçerli döngü yinelemesini atlar ve `break`kalan tüm yinelemeleri atlar. Döngüler gibi `while`bunlar _bazen_ kullanılır, ancak pratikte düşündüğünüzden çok daha az.

ile başlayarak ayrı ayrı inceleyelim `continue`. Bir veri dizisi üzerinde döngü yaparken, Swift diziden bir öğe alır ve onu kullanarak döngü gövdesini yürütür. Bu döngü gövdesinin içini çağırırsanız `continue`, Swift geçerli döngü yinelemesini yürütmeyi hemen durduracak ve normal olarak devam edeceği döngüdeki bir sonraki öğeye atlayacaktır. Bu genellikle, seçtiğiniz bir testi geçemeyen döngü değişkenlerini ortadan kaldırdığınız döngülerin başlangıcına yakın yerlerde kullanılır.

İşte bir örnek:

```swift
let filenames = ["me.jpg", "work.txt", "sophie.jpg", "logo.psd"]

for filename in filenames {
    if filename.hasSuffix(".jpg") == false {
        continue
    }

    print("Found picture: \(filename)")
}
```

Bu, bir dizi dosya adı dizesi oluşturur, ardından her birinin üzerinden geçer ve “.jpg” son ekine sahip olduğundan, bunun bir resim olduğundan emin olmak için kontrol eder. `continue`bu testi geçemeyen tüm dosya adlarıyla birlikte kullanılır, böylece döngü gövdesinin geri kalanı atlanır.

, bir döngüden hemen `break`çıkar ve kalan tüm yinelemeleri atlar. Bunu göstermek için, iki sayı için 10 ortak katı hesaplayan bir kod yazabiliriz:

```swift
let number1 = 4
let number2 = 14
var multiples = [Int]()

for i in 1...100_000 {
    if i.isMultiple(of: number1) && i.isMultiple(of: number2) {
        multiples.append(i)

        if multiples.count == 10 {
            break
        }
    }
}

print(multiples)
```

Bu oldukça fazla şey yapar:

1.  İki sayıyı tutmak için iki sabit oluşturun.
2.  İki sayımızın ortak katlarını saklayacak bir tamsayı dizisi değişkeni oluşturun.
3.  1'den 100.000'e kadar sayın, her döngü değişkenini `i`.
4.  If, `i`hem birinci hem de ikinci sayıların katıysa, onu tamsayı dizisine ekleyin.
5.  10 çarpana ulaştığımızda, `break`döngüden çıkmak için arayın.
6.  Ortaya çıkan diziyi yazdırın.

Dolayısıyla, `continue`geçerli döngü yinelemesinin geri kalanını atlamak istediğinizde kullanın ve `break`kalan tüm döngü yinelemelerini atlamak istediğinizde kullanın.