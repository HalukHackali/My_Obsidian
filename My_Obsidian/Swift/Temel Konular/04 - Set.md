#swift #yazılım 

# Hızlı veri arama için set'ler nasıl kullanılır?


Şimdiye kadar Swift'te veri toplamanın iki yolunu öğrendiniz: diziler ve sözlükler. Verileri gruplandırmanın _küme_ adı verilen çok yaygın üçüncü bir yolu vardır - dizilere benzerler, ancak yinelenen öğeler ekleyemezsiniz ve öğelerini belirli bir sırada saklamazlar.

Bir küme oluşturmak, bir dizi oluşturmak gibi çalışır: Swift'e ne tür verileri depolayacağını söyleyin, sonra devam edin ve bir şeyler ekleyin. Yine de iki önemli fark vardır ve bunlar en iyi şekilde bazı kodlar kullanılarak gösterilir.

İlk olarak, aktör isimlerini nasıl yapacağınız aşağıda açıklanmıştır:

```swift
let people = Set(["Denzel Washington", "Tom Cruise", "Nicolas Cage", "Samuel L Jackson"])
```

Bunun aslında önce bir dizi oluşturduğunu, ardından bu diziyi kümeye koyduğunu fark ettiniz mi? Bu kasıtlıdır ve sabit verilerden bir küme oluşturmanın standart yoludur. Kümenin yinelenen değerleri otomatik olarak kaldıracağını ve dizide kullanılan tam sırayı hatırlamayacağını unutmayın.

Setin verileri nasıl sıraladığını merak ediyorsanız, çıktısını almayı deneyin:

```swift
print(people)
```

İsimleri orijinal sırayla görebilirsiniz , ancak tamamen farklı bir sıra da alabilirsiniz - set _,_ öğelerinin hangi sırayla geldiğini umursamaz.

Bir kümeye öğe eklerken ortaya çıkan ikinci önemli fark, öğeleri tek tek eklediğinizde görünür. İşte kod:

```swift
var people = Set<String>()
people.insert("Denzel Washington")
people.insert("Tom Cruise")
people.insert("Nicolas Cage")
people.insert("Samuel L Jackson")
```

Nasıl kullandığımıza dikkat edin `insert()`? Bir dizgi dizimiz olduğunda, öğeleri çağırarak ekledik `append()`, ancak bu ad burada bir anlam ifade etmiyor - kümenin sonuna bir öğe eklemiyoruz çünkü küme, öğeleri istediği sırayla saklayacaktır. .

Şimdi, kümelerin kulağa basitleştirilmiş diziler gibi geldiğini düşünebilirsiniz - sonuçta, kopyalarınız yoksa ve öğelerinizin sırasını kaybederseniz, neden sadece dizileri kullanmıyorsunuz? Eh, bu kısıtlamaların ikisi de aslında bir avantaja dönüşüyor.

İlk olarak, kopyaları saklamamak bazen tam olarak istediğiniz şeydir. Önceki örnekte oyuncuları seçmemin bir nedeni var: Screen Actors Guild, karışıklığı önlemek için tüm üyelerinin benzersiz bir sahne adına sahip olmasını şart koşuyor, bu da tekrarlara asla izin verilmemesi gerektiği anlamına geliyor. Örneğin, aktör Michael Keaton'ın (Örümcek Adam Eve Dönüş, Oyuncak Hikayesi 3, Batman ve daha fazlası) aslında adı Michael Douglas'tır, ancak loncada _zaten_ bir Michael Douglas olduğu için (Avengers, Falling Down, Romancing the Stone ve dahası), benzersiz bir isme sahip olması gerekiyordu.

İkincisi, setler öğelerinizi tam olarak sizin belirlediğiniz sırada depolamak yerine, öğeleri bulmayı çok hızlı hale getiren oldukça optimize edilmiş bir sırada depolar. Ve fark küçük değil: 1000 film adından oluşan bir diziniz varsa ve `contains()`"Kara Şövalye" içerip içermediğini kontrol etmek gibi bir şey kullanıyorsanız, Swift'in eşleşen bir tane bulana kadar her öğeyi gözden geçirmesi gerekir - bu, hepsini kontrol etmek anlamına gelebilir Kara Şövalye dizide olmadığı için yanlış döndürmeden önce 1000 film adı.

Karşılaştırıldığında, `contains()`bir seti çağırmak o kadar hızlı çalışır ki, onu anlamlı bir şekilde ölçmek için mücadele edersiniz. Heck, sette bir milyon, hatta 10 milyon öğeniz olsa bile, yine de anında çalışır, oysa bir dizinin aynı işi yapması dakikalar veya daha uzun sürebilir.

Çoğu zaman kendinizi kümeler yerine dizileri kullanırken bulacaksınız, ancak bazen - sadece bazen - bir kümenin belirli bir sorunu çözmek için tam olarak doğru seçim olduğunu göreceksiniz ve aksi halde kodun çok kısa sürede yavaş çalışmasına neden olacaktır. hiç.

**İpucu: öğesinin** yanı sıra , bir kümedeki öğe sayısını okumayı ve kümenin öğelerini içeren sıralanmış bir dizi döndürmeyi `contains()`de bulacaksınız .`count``sorted()`