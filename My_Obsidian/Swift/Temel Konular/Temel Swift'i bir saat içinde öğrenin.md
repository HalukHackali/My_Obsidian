#swift #yazılım 

Swift'i kullanmaya başlamak için bilmeniz gereken en az şey burada.

![](https://www.hackingwithswift.com/uploads/swift-evolution-5.jpg)

Bu makalede size yaklaşık bir saat içinde Swift programlama dilinin temellerini tanıtacağım.

Bu makale iki tür insana yöneliktir: 100 Günlük SwiftUI kursuma girişini tamamlayan ve hızlı bir inceleme arayan kişiler ve diğer dillerle deneyimli ve becerilerini Swift'e aktarmak isteyen kişiler.

Hızlı hareket edeceğiz çünkü bu bir astar olacak şekilde tasarlandı - kendinizi bir şeyi anlamakta zorlanırken bulursanız, orada daha uzun, daha ayrıntılı tanıtımı tamamlamak için [100 Günlük SwiftUI'yi](https://www.hackingwithswift.com/100/swiftui)ziyaret edin.

Hadi ona geçelim!

### Sabitler ve değişkenler oluşturma

Swift sabitler ve değişkenler oluşturabilir, ancak sabitler genellikle tercih edilir.

Bir değişken dizesi oluşturmak ve değiştirmek için bunu kullanın:

```swift
var name = "Ted"
name = "Rebecca"
```

Bir değeri değiştirmek istemiyorsanız, bunun yerine bir _sabit_ kullanın:

```swift
let user = "Daphne"
```

The `print()` function is helpful for learning and debugging, and shows some information about a variable:

```swift
print(user)
```

### Teller

Swift'in dizeleri çift tırnakla başlar ve biter:

```swift
let actor = "Tom Cruise"
```

Ve emoji ile de harika çalışıyorlar:

```swift
let actor = "Tom Cruise 🏃‍♂️"
```

Dizenizin içinde çift tırnak işareti istiyorsanız, önlerine bir ters eğik çizgi yerleştirin:

```swift
let quote = "He tapped a sign saying \"Believe\" and walked away."
```

Birden fazla satırı kapsayan bir dize istiyorsanız, aşağıdaki gibi üç çift tırnakla başlayın ve bitirin:

```swift
let movie = """
A day in
the life of an
Apple engineer
"""
```

Swift provides many useful properties and methods for strings, including `.count` to read how many letters it has:

```swift
print(actor.count)
```

There are also `hasPrefix()` and `hasSuffix()`, which lets us know whether a string starts or ends with specific letters:

```swift
print(quote.hasPrefix("He"))
print(quote.hasSuffix("Away."))
```

**Önemli:** Swift'te dizeler büyük/küçük harfe duyarlıdır, böylece ikinci kontrol false döndürür.

### Tamsayılar

Swift stores whole numbers using the type `Int`, which supports a range of standard mathematical operators: 

```swift
let score = 10
let higherScore = score + 10
let halvedScore = score / 2
```

Ayrıca, yerinde değişkenleri değiştiren bileşik atama operatörlerini de destekler:

```swift
var counter = 10
counter += 5
```

Integers come with their own useful functionality, such as the `isMultiple(of:)` method:

```swift
let number = 120
print(number.isMultiple(of: 3))
```

Bunun gibi belirli bir aralıkta rastgele tamsayılar da yapabilirsiniz:

```swift
let id = Int.random(in: 1...1000)
```

### Ondalık Sayılar

If you create a number with a decimal point, Swift will consider it a `Double`:

```swift
let score = 3.0
```

Swift, `Double`'ı `Int` tamamen farklı bir veri türü olarak görüyor ve bunları karıştırmanıza izin vermiyor.

### Booleanlar

Swift uses the type `Bool` to store true or false:

```swift
let goodDogs = true
let gameOver = false
```

You can flip a Boolean from true to false by calling its `toggle()` method:

```swift
var isSaved = false
isSaved.toggle()
```

### Birleştirme dizeleri

_Dize enterpolasyonunu_ kullanarak diğer verilerden dizeler oluşturabilirsiniz: dizenizin içine bir ters eğik çizgi yazın, ardından bir değişkenin veya sabitin adını parantez içine yerleştirin, şöyle:

```swift
let name = "Taylor"
let age = 26
let message = "I'm \(name) and I'm \(age) years old."
print(message)
```

Bu kod çalıştığında, "Ben Taylor ve 26 yaşındayım" yazacak.

### Diziler

Öğeleri şöyle bir dizide gruplandırabilirsiniz:

```swift
var colors = ["Red", "Green", "Blue"]
let numbers = [4, 8, 15, 16]
var readings = [0.1, 0.5, 0.8]
```

Each of those hold different kinds of data: one strings, one integers, and one decimals. When we read data from arrays we will get the appropriate type back - a `String`, an `Int`, or a `Double`:

```swift
print(colors[0])
print(readings[2])
```

**İpucu:** İstediğiniz dizinde bir öğenin bulunduğundan emin olun, aksi takdirde kodunuz çöker - uygulamanız çalışmayı durdurur.

If your array is variable, you can use `append()` to add new items:

```swift
colors.append("Tartan")
```

Eklediğiniz veri türü, zaten orada olanlarla eşleşmelidir.

Arrays have useful functionality, such as `.count` to read how many items are in an array, or `remove(at:)` to remove one item at a specific index:

```swift
colors.remove(at: 0)
print(colors.count)
```

You can check whether an array contains a particular item by using `contains()`, like this:

```swift
print(colors.contains("Octarine"))
```

### Sözlükler

Sözlükler, belirttiğimiz bir anahtara göre birden fazla değeri depolar. Örneğin, bir kişi hakkında bilgi depolamak için bir sözlük oluşturabiliriz:

```swift
let employee = [
    "name": "Taylor",
    "job": "Singer"
]
```

Sözlükten veri okumak için, oluştururken kullandığınız tuşları kullanın:

```swift
print(employee["name", default: "Unknown"])
print(employee["job", default: "Unknown"])
```

The `default` value will be used if the key we’ve asked for doesn’t exist.

### Setler

Kümeler dizilere benzer, ancak yinelenen öğeler ekleyemezsiniz ve öğeleri belirli bir sırayla saklamazlar.

Bu bir dizi sayı yapar:

```swift
var numbers = Set([1, 1, 3, 5, 7])
print(numbers)
```

Unutmayın, küme yinelenen değerleri yok sayar ve dizide kullanılan sırayı hatırlamaz.

Adding items to a set is done by calling its `insert()` method, like this:

```swift
numbers.insert(10)
```

Sets have one big advantage over arrays: using `contains()` on a set is effectively instant no matter how many items the set contains – even a set with 10,000,000 items will respond instantly.

### Enumlar

Enum, kodumuzu daha verimli ve daha güvenli hale getirmek için oluşturabileceğimiz ve kullanabileceğimiz bir dizi adlandırılmış değerdir. Örneğin, bunun gibi hafta içi enum yapabiliriz:

```swift
enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}
```

That calls the new enum `Weekday`, and provides five cases to handle the five weekdays.

Artık bu enum'un örneklerini yapabilir, ardından ona başka olası durumlar atayabiliriz:

```swift
var day = Weekday.monday
day = .friday
```

### Tip ek açıklamaları

Aşağıdaki gibi _tür ek açıklamasını_ kullanarak yeni bir değişken veya sabit için belirli bir türü zorlamayı deneyebilirsiniz:

```swift
var score: Double = 0
```

Without the `: Double` part Swift would infer that to be an `Int`, but we’re overriding that and saying it’s a `Double`.

İşte şimdiye kadar kapsanan türlere dayalı bazı tür ek açıklamaları:

```swift
let player: String = "Roy"
var luckyNumber: Int = 13
let pi: Double = 3.141
var isEnabled: Bool = true
var albums: Array<String> = ["Red", "Fearless"]
var user: Dictionary<String, String> = ["id": "@twostraws"]
var books: Set<String> = Set(["The Bluest Eye", "Foundation"])
```

Diziler ve sözlükler o kadar yaygındır ki, yazması daha kolay olan özel sözdizimine sahiptirler:

```swift
var albums: [String] = ["Red", "Fearless"]
var user: [String: String] = ["id": "@twostraws"]
```

Boş koleksiyonlar oluşturmak için tam olarak şey türlerini bilmek önemlidir. Örneğin, bunların her ikisi de boş dize dizileri oluşturur:

```swift
var teams: [String] = [String]()
var clues = [String]()
```

Bir enum'un değerleri, enum'un kendisiyle aynı türe sahiptir, bu nedenle şunu yazabiliriz:

```swift
enum UIStyle {
    case light, dark, system
}

var style: UIStyle = .light
```

### şartlar

Use `if`, `else`, and `else if` statements to check a condition and run some code as appropriate:

```swift
let age = 16

if age < 12 {
    print("You can't vote")
} else if age < 18 {
    print("You can vote soon.")
} else {
    print("You can vote now.")
}
```

We can use `&&` to combine two conditions, and the whole condition will only be true if the two parts inside are true:

```swift
let temp = 26

if temp > 20 && temp < 30 {
    print("It's a nice day.")
}
```

Alternatively, `||` will make a condition be true if _either_ subcondition is true.

### İfadeleri değiştir

Swift lets us check a value against multiple conditions using `switch`/`case` syntax, like this:

```swift
enum Weather {
    case sun, rain, wind
}

let forecast = Weather.sun

switch forecast {
case .sun:
    print("A nice day.")
case .rain:
    print("Pack an umbrella.")
default:
    print("Should be okay.")
}
```

`switch`ifadeler ayrıntılı olmalıdır: kazara birini kaçırmamak için tüm olası değerler ele alınmalıdır.

### Üçlü koşullu operatör

Üçlü operatör bir koşulu kontrol etmemize ve iki değerden birini döndürmemize izin verir: koşul doğruysa bir şey ve yanlışsa bir şey:

```swift
let age = 18
let canVote = age >= 18 ? "Yes" : "No"
```

When that code runs, `canVote` will be set to “Yes” because `age` is set to 18.

### Döngüler

Swift'in döngüleri, bir koleksiyondaki veya özel bir aralıktaki her öğe için bazı kodlar çalıştırır. Örneğin:

```swift
let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift works on \(os).")
}
```

Ayrıca bir dizi sayı üzerinde döngü yapabilirsiniz:

```swift
for i in 1...12 {
    print("5 x \(i) is \(5 * i)")
}
```

`1...12` contains the values 1 through 12 inclusive. If you want to exclude the final number, use `..<`instead:

```swift
for i in 1..<13 {
    print("5 x \(i) is \(5 * i)")
}
```

**Tip:** If you don’t need the loop variable, use `_`:

```swift
var lyric = "Haters gonna"

for _ in 1...5 {
    lyric += " hate"
}

print(lyric)
```

There are also `while` loops, which execute their loop body until a condition is false, like this:

```swift
var count = 10

while count > 0 {
    print("\(count)…")
    count -= 1
}

print("Go!")
```

You can use `continue` to skip the current loop iteration and proceed to the following one:

```swift
let files = ["me.jpg", "work.txt", "sophie.jpg"]

for file in files {
    if file.hasSuffix(".jpg") == false {
        continue
    }

    print("Found picture: \(file)")
}
```

Alternatif olarak, bir döngüden çıkmak ve kalan tüm yinelemeleri atlamak için `break` kullanın.

### Fonksiyonlar

To create a new function, write `func` followed by your function’s name, then add parameters inside parentheses:

```swift
func printTimesTables(number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(number: 5)
```

We need to write `number: 5` at the call site, because the parameter name is part of the function call.

To return data from a function, tell Swift what type it is, then use the `return` keyword to send it back. For example, this returns a dice roll:

```swift
func rollDice() -> Int {
    return Int.random(in: 1...6)
}

let result = rollDice()
print(result)
```

If your function contains only a single line of code, you can remove the `return` keyword:

```swift
func rollDice() -> Int {
    Int.random(in: 1...6)
}
```

### Fonksiyonlardan birden fazla değer döndürme

Demetler, bir işlevden birden fazla değer döndürmenin uygun bir yolu olan belirli türlerde sabit sayıda değer depolar:

```swift
func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}

let user = getUser()
print("Name: \(user.firstName) \(user.lastName)")
```

If you don’t need all the values from the tuple you can destructure the tuple to pull it apart into individual values, then `_` to tell Swift to ignore some:

```swift
let (firstName, _) = getUser()
print("Name: \(firstName)")
```

### Parametre etiketlerini özelleştirme

Bir işlevi çağırırken bir parametrenin adını iletmek istemiyorsanız, önüne bir alt çizgi yerleştirin:

```swift
func isUppercase(_ string: String) -> Bool {
    string == string.uppercased()
}

let string = "HELLO, WORLD"
let result = isUppercase(string)
```

Bir alternatif, ilkinden önce ikinci bir isim yazmaktır: biri harici olarak ve biri dahili olarak kullanılır:

```swift
func printTimesTables(for number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5)
```

In that code `for` is used externally, and `number` is used internally.

### Parametreler için varsayılan değerler sağlama

Türden sonra bir eşittir yazarak ve ardından aşağıdaki gibi bir değer sağlayarak varsayılan parametre değerleri sağlayabiliriz:

```swift
func greet(_ person: String, formal: Bool = false) {
    if formal {
        print("Welcome, \(person)!")
    } else {
        print("Hi, \(person)!")
    }
}
```

Now we can call `greet()` in two ways:

```swift
greet("Tim", formal: true)
greet("Taylor")
```

### Fonksiyonlardaki hataları işleme

İşlevlerdeki hataları işlemek için Swift'e hangi hataların olabileceğini söylemeniz, hata atabilecek bir işlev yazmanız, ardından onu çağırmanız ve herhangi bir sorunu çözmeniz gerekir.

İlk olarak, oluşabilecek hataları tanımlayın:

```swift
enum PasswordError: Error {
    case short, obvious
}
```

Next, write a function that can throw errors. This is done by placing `throws` into the function’s type, then by using `throw` to trigger specific errors:

```swift
func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }

    if password == "12345" {
        throw PasswordError.obvious
    }

    if password.count < 10 {
        return "OK"
    } else {
        return "Good"
    }
}
```

Now call the throwing function by starting a `do` block, calling the function using `try`, then catching errors that occur:

```swift
let string = "12345"

do {
    let result = try checkPassword(string)
    print("Rating: \(result)")
} catch PasswordError.obvious {
    print("I have the same combination on my luggage!")
} catch {
    print("There was an error.")
}
```

When it comes to catching errors, you must always have a `catch` block that can handle every kind of error. 

### Kapanışlar

İşlevselliği doğrudan aşağıdaki gibi bir sabite veya değişkene atayabilirsiniz:

```swift
let sayHello = {
    print("Hi there!")
}

sayHello()
```

In that code, `sayHello` is a closure – a chunk of code we can pass around and call whenever we want. If you want the closure to accept parameters, they must be written inside the braces:

```swift
let sayHello = { (name: String) -> String in
    "Hi \(name)!"
}
```

`in`, parametrelerin sonunu ve dönüş türünü işaretlemek için kullanılır - bundan sonraki her şey kapağın gövdesidir.

Closures are used extensively in Swift. For example, there’s an array method called `filter()` that runs all elements of the array through a test, and any that return true for the test get returned in a new array.

Bu testi bir kapatma kullanarak sağlayabiliriz, böylece bir diziyi yalnızca T ile başlayan adları içerecek şekilde filtreleyebiliriz:

```swift
let team = ["Gloria", "Suzanne", "Tiffany", "Tasha"]

let onlyT = team.filter({ (name: String) -> Bool in
    return name.hasPrefix("T")
})
```

Inside the closure we list the parameter `filter()` passes us, which is a string from the array. We also say that our closure returns a Boolean, then mark the start of the closure’s code by using `in` – after that, everything else is normal function code.

### Arka kapaklar ve kısaltma sözdizimi

Swift'in kapanışların okunmasını kolaylaştırmak için birkaç numarası var. İşte bir diziyi yalnızca "T" ile başlayan isimleri içerecek şekilde filtreleyen bazı kodlar:

```swift
let team = ["Gloria", "Suzanne", "Tiffany", "Tasha"]

let onlyT = team.filter({ (name: String) -> Bool in
    return name.hasPrefix("T")
})

print(onlyT)
```

Immediately you can see that the body of the closure has just a single line of code, so we can remove `return`:

```swift
let onlyT = team.filter({ (name: String) -> Bool in
    name.hasPrefix("T")
})
```

`filter()`dizisinden bir öğeyi kabul eden ve döndürülen dizide olması gerekiyorsa true döndüren bir işlev verilmelidir.

Geçtiğimiz işlev böyle davranmalı olduğundan, kapanışımızdaki türleri belirtmemize gerek yoktur. Yani, kodu şuna yeniden yazabiliriz:

```swift
let onlyT = team.filter({ name in
    name.hasPrefix("T")
})
```

Aşağıdaki gibi görünen _son kapatma sözdizimi_ adı verilen özel sözdizimini kullanarak daha da ileri gidebiliriz:

```swift
let onlyT = team.filter { name in
    name.hasPrefix("T")
}
```

Finally, Swift can provide short parameter names for us so we don’t even write `name in` any more, and instead rely on a specially named value provided for us: `$0`:

```swift
let onlyT = team.filter {
    $0.hasPrefix("T")
}
```

### Yapılar

Yapılar, kendi özellikleri ve yöntemleriyle tamamlanan kendi özel veri türlerimizi oluşturmamıza izin veriyor:

```swift
struct Album {
    let title: String
    let artist: String
    var isReleased = true

    func printSummary() {
        print("\(title) by \(artist)")
    }
}

let red = Album(title: "Red", artist: "Taylor Swift")
print(red.title)
red.printSummary()
```

Yapı örnekleri oluşturduğumuzda bunu bir _başlatıcı_ kullanarak yaparız - Swift, yapımıza bir işlev gibi davranmamıza izin verir ve özelliklerinin her biri için parametreler geçirir. Yapının özelliklerine göre bu _üye başlatıcıyı_ sessizce oluşturur.

Bir yapının yönteminin özelliklerinden birini değiştirmesini istiyorsanız, onu _mutasyona uğratıyor_ olarak işaretleyin:

```swift
mutating func removeFromSale() {
    isReleased = false
}
```

### Hesaplanan özellikler

A computed property calculates its value every time it’s accessed. For example, we could write an `Employee` struct that tracks how many days of vacation remained for that employee:

```swift
struct Employee {
    let name: String
    var vacationAllocated = 14
    var vacationTaken = 0

    var vacationRemaining: Int {
        vacationAllocated - vacationTaken
    }
}
```

To be able to write to `vacationRemaining` we need to provide both a _getter_ and a _setter_:

```swift
var vacationRemaining: Int {
    get {
        vacationAllocated - vacationTaken
    }

    set {
        vacationAllocated = vacationTaken + newValue
    }
}
```

`newValue`Swift tarafından sağlanır ve kullanıcının mülke atadığı değeri saklar.

### Mülk gözlemcileri

Property observers are pieces of code that run when properties change: `didSet` runs when the property just changed, and `willSet` runs _before_ the property changed.

We could demonstrate `didSet` by making a `Game` struct print a message when the score changes:

```swift
struct Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var game = Game()
game.score += 10
game.score -= 3
```

### Özel başlatıcılar

Başlatıcılar, kullanılacak yeni bir yapı örneği hazırlayan ve tüm özelliklerin bir başlangıç değerine sahip olmasını sağlayan özel işlevlerdir.

Swift, yapının özelliklerine göre bir tane oluşturur, ancak kendinizinkini oluşturabilirsiniz:

```swift
struct Player {
    let name: String
    let number: Int

    init(name: String) {
        self.name = name
        number = Int.random(in: 1...99)
    }
}
```

**Important:** Initializers don’t have `func` before them, and don’t explicitly return a value.

### Erişim kontrolü

Swift, yapılar içinde erişim kontrolü için çeşitli seçeneklere sahiptir, ancak dördü en yaygın olanlardır:

-   Use `private` for “don’t let anything outside the struct use this.”
-   Use `private(set)` for “anything outside the struct can read this, but don’t let them change it.”
-   Use `fileprivate` for “don’t let anything outside the current file use this.”
-   Use `public` for “let anyone, anywhere use this.”

Örneğin:

```swift
struct BankAccount {
    private(set) var funds = 0

    mutating func deposit(amount: Int) {
        funds += amount
    }

    mutating func withdraw(amount: Int) -> Bool {
        if funds > amount {
            funds -= amount
            return true
        } else {
            return false
        }
    }
}
```

Because we used `private(set)`, reading `funds` from outside the struct is fine but writing isn’t possible.

### Statik özellikler ve yöntemler

Swift, statik özellikleri ve yöntemleri destekleyerek, yapının bir örneğinden ziyade doğrudan yapının kendisine bir özellik veya yöntem eklemenize olanak tanır:

```swift
struct AppData {
    static let version = "1.3 beta 2"
    static let settings = "settings.json"
}
```

Bu yaklaşımı kullanarak, uygulamanın sürüm numarası gibi bir şeyi kontrol etmemiz veya görüntülememiz gereken her yerde `AppData.version` okuyabiliriz.

### Sınıflar

Sınıflar, özel veri türleri oluşturmamıza izin verir ve yapılardan beş şekilde farklıdır.

İlk fark, işlevselliği diğer sınıflardan miras alarak sınıflar oluşturabilmemizdir:

```swift
class Employee {
    let hours: Int

    init(hours: Int) {
        self.hours = hours
    }

    func printSummary() {
        print("I work \(hours) hours a day.")
    }
}

class Developer: Employee {
    func work() {
        print("I'm coding for \(hours) hours.")
    }
}

let novall = Developer(hours: 8)
novall.work()
novall.printSummary()
```

If a child class wants to change a method from a parent class, it must use `override`:

```swift
override func printSummary() {
    print("I spend \(hours) hours a day searching Stack Overflow.")
}
```

İkinci fark, başlatıcıların sınıflarla daha zor olmasıdır. Burada çok fazla karmaşıklık var, ancak üç kilit nokta var:

1.  Swift, sınıflar için üye olarak bir başlatıcı oluşturmaz.
2.  Bir alt sınıfın özel başlatıcıları varsa, kendi özelliklerini kurmayı bitirdikten sonra her zaman _üst_ öğenin başlatıcısını çağırmalıdır.
3.  Bir alt sınıfın herhangi bir başlatıcısı yoksa, üst sınıfının başlatıcılarını otomatik olarak devralır.

Örneğin:

```swift
class Vehicle {
    let isElectric: Bool

    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}

class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)
    }
}
```

`super`başlatıcısı gibi üst sınıfımıza ait yöntemleri çağırmamıza izin verir.

Üçüncü fark, bir sınıf örneğinin tüm kopyalarının verilerini paylaşmasıdır, bu da bir tanesinde yaptığınız değişikliklerin diğer kopyaları otomatik olarak değiştireceği anlamına gelir.

Örneğin:

```swift
class Singer {
    var name = "Adele"
}

var singer1 = Singer()
var singer2 = singer1
singer2.name = "Justin"
print(singer1.name)  
print(singer2.name)
```

Bu, her ikisi için de "Justin"i yazdıracak - sadece birini değiştirmiş olsak da, diğeri de değişti. Buna karşılık, yapı kopyaları verilerini paylaşmaz.

Dördüncü fark, sınıfların bir nesneye son başvuru yok edildiğinde çağrılan bir _başlatıcıya_ sahip olabileceğidir.

Böylece, oluşturulduğunda ve yok edildiğinde bir mesaj yazdıran bir sınıf oluşturabiliriz:

```swift
class User {
    let id: Int

    init(id: Int) {
        self.id = id
        print("User \(id): I'm alive!")
    }

    deinit {
        print("User \(id): I'm dead!")
    }
}

for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I'm in control!")
}
```

Son fark, sınıfların sınıfın kendisi sabit olsa bile değişken özelliklerini değiştirmemize izin vermesidir:

```swift
class User {
    var name = "Paul"
}

let user = User()
user.name = "Taylor"
print(user.name)
```

As a result of this, classes don’t need the `mutating` keyword with methods that change their data.

### Protokoller

Protokoller, bir veri türünün desteklemesini beklediğimiz işlevselliği tanımlar ve Swift, kodumuzun bu kurallara uymasını sağlar.

For example, we could define a `Vehicle` protocol like this:

```swift
protocol Vehicle {
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

Bu protokolün çalışması için gerekli yöntemleri listeler, ancak herhangi bir kod içermez - yalnızca yöntem adları, parametreler ve dönüş türleri belirtiriz.

Once you have a protocol you can make data types conform to it by implementing the required functionality. For example, we could make a `Car` struct that conforms to `Vehicle`:

```swift
struct Car: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }

    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }
}
```

`Vehicle` listelenen tüm yöntemler, aynı ad, parametreler ve dönüş türleriyle _tam olarak_ `Car`bulunmalıdır.

Now you can write a function that accepts any kind of type that conforms to `Vehicle`, because Swift knows it implements both `estimateTime()` and `travel()`:

```swift
func commute(distance: Int, using vehicle: Vehicle) {
    if vehicle.estimateTime(for: distance) > 100 {
        print("Too slow!")
    } else {
        vehicle.travel(distance: distance)
    }
}

let car = Car()
commute(distance: 100, using: car)
```

Protokoller ayrıca mülk gerektirebilir, bu nedenle araçların kaç koltuklu olduğu ve şu anda kaç yolcuya sahip oldukları için özellikler isteyebiliriz:

```swift
protocol Vehicle {
    var name: String { get }
    var currentPassengers: Int { get set }
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

That adds two properties: one marked with `get` that might be a constant or computed property, and one marked with `get set` that might be a variable or a computed property with a getter and setter.

Now all conforming types must add implementations of those two properties, like this for `Car`:

```swift
let name = "Car"
var currentPassengers = 1
```

**İpucu:** Sadece virgülle ayrılmış olarak listeleyerek ihtiyacınız olduğu kadar protokole uyabilirsiniz.

### Uzantılar

Uzantılar, herhangi bir türe işlevsellik eklememize izin verir. Örneğin, Swift'in dizelerinin boşlukları ve yeni satırları kırpmak için bir yöntemi vardır, ancak oldukça uzundur, bu yüzden onu bir uzantıya dönüştürebiliriz:

```swift
extension String {
    func trimmed() -> String {
        self.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}

var quote = "   The truth is rarely pure and never simple   "
let trimmed = quote.trimmed()
```

If you want to change a value directly rather than returning a new value, mark your method as `mutating`like this:

```swift
extension String {
    mutating func trim() {
        self = self.trimmed()
    }
}

quote.trim()
```

Uzantılar, bunun gibi türlere hesaplanmış özellikler de ekleyebilir:

```swift
extension String {
    var lines: [String] {
        self.components(separatedBy: .newlines)
    }
}
```

The `components(separatedBy:)` method splits a string into an array of strings using a boundary of our choosing, which in this case is new lines.

Artık bu özelliği tüm dizelerle kullanabiliriz:

```swift
let lyrics = """
But I keep cruising
Can't stop, won't stop moving
"""

print(lyrics.lines.count)
```

### Protokol uzantıları

Protokol uzantıları, hesaplanan özellikler ve yöntem uygulamaları eklemek için tüm bir protokolü genişletir, böylece bu protokole uygun herhangi bir tür bunları alır.

For example, `Array`, `Dictionary`, and `Set` all conform to the `Collection` protocol, so we can add a computed property to all three of them like this:

```swift
extension Collection {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

Şimdi onu kullanabiliriz:

```swift
let guests = ["Mario", "Luigi", "Peach"]

if guests.isNotEmpty {
    print("Guest count: \(guests.count)")
}
```

Bu yaklaşım, bir protokolde gerekli yöntemleri listeleyebileceğimiz ve ardından bir protokol uzantısı içindekilerin varsayılan uygulamalarını ekleyebileceğimiz anlamına gelir. Tüm uyumlu türler daha sonra bu varsayılan uygulamaları kullanabilir veya gerektiğinde kendi uygulamalarını sağlar.

### İsteğe bağlı

İsteğe bağlılar, verilerin yokluğunu temsil eder - örneğin, 0 değerine sahip bir tamsayı ile hiç değeri olmayan bir tamsayayıyı ayırt ederler.

İsteğe bağlı olanları çalışırken görmek için bu kodu düşünün:

```swift
let opposites = [
    "Mario": "Wario",
    "Luigi": "Waluigi"
]

let peachOpposite = opposites["Peach"]
```

Bu, var olmayan "Şeftali" anahtarına eklenen değeri okumaya çalışır, bu nedenle bu normal bir dize olamaz. Swift'in çözümüne _isteğe bağlı_ denir, bu da mevcut olabilecek veya olmayabilecek veriler anlamına gelir.

An optional string might have a string waiting inside for us, or there might be nothing at all – a special value called `nil`, that means “no value”. Any kind of data can be optional, including `Int`, `Double`, and `Bool`, as well as instances of enums, structs, and classes.

Swift isteğe bağlı verileri doğrudan kullanmamıza izin vermez, çünkü boş olabilir. Bu, onu kullanmak için isteğe bağlı olanı _açmamız_ gerektiği anlamına gelir - bir değer olup olmadığını görmek için içeriye bakmamız ve varsa çıkarmamız ve kullanmamız gerekir.

Swift bize isteğe bağlı olarak açmanın birkaç yolunu sunar, ancak en çok göreceğiniz şuna benzer:

```swift
if let marioOpposite = opposites["Mario"] {
    print("Mario's opposite is \(marioOpposite)")
}
```

That reads the optional value from the dictionary, and if it has a string inside it gets _unwrapped_ – the string inside gets placed into the `marioOpposite` constant, and isn’t optional any more. Because we were able to unwrap the optional, the condition is a success so the `print()` code is run.

### İsteğe bağlı malzemeleri koruma ile açmak

Swift has a second way of unwrapping optionals, called `guard let`, which is very similar to `if let`except it flips things around: `if let` runs the code inside its braces if the optional had a value, and `guard let` runs the code if the optional _didn’t_ have a value.

Şöyle görünüyor:

```swift
func printSquare(of number: Int?) {
    guard let number = number else {
        print("Missing input")
        return
    }

    print("\(number) x \(number) is \(number * number)")
}
```

If you use `guard` to check a function’s inputs are valid, Swift requires you to use `return` if the check fails. However, if the optional you’re unwrapping has a value inside, you can use it _after_ the `guard` code finishes.

**İpucu:** İsteğe bağlı olarak açmayanlar da dahil olmak üzere her koşulda koruma kullanabilirsiniz.

### Nil birleşme

Swift, _nil birleştirme operatörü_ olarak adlandırılan isteğe bağlıları açmanın üçüncü bir yoluna sahiptir - isteğe bağlı bir paketi açar ve isteğe bağlı boşsa varsayılan bir değer sağlar:

```swift
let tvShows = ["Archer", "Babylon 5", "Ted Lasso"]
let favorite = tvShows.randomElement() ?? "None"
```

The nil coalescing operator is useful in many places optionals are created. For example, creating an integer from a string returns an optional `Int?` because the conversion might have failed. Here we can use nil coalescing to provide a default value:

```swift
let input = ""
let number = Int(input) ?? 0
print(number)
```

### İsteğe bağlı zincirleme

İsteğe bağlı zincirleme, isteğe bağlı olanların içindeki isteğe bağlıları şöyle okur:

```swift
let names = ["Arya", "Bran", "Robb", "Sansa"]
let chosen = names.randomElement()?.uppercased()
print("Next in line: \(chosen ?? "No one")")
```

İsteğe bağlı zincirleme 2. satırdadır: bir soru işareti ve ardından daha fazla kod gelir. "İsteğe bağlı olanın içinde bir değeri varsa, o zaman açın..." dememize ve daha fazla kod eklememize olanak tanır. Bizim durumumuzda "diziden rastgele bir öğemiz varsa, büyük harfle" diyoruz.

### İsteğe bağlı deneme?

When calling a function that might throw errors, we can use `try?` to convert its result into an optional containing a value on success, or `nil` otherwise.

İşte nasıl göründüğü:

```swift
enum UserError: Error {
    case badID, networkFailed
}

func getUser(id: Int) throws -> String {
    throw UserError.networkFailed
}

if let user = try? getUser(id: 23) {
    print("User: \(user)")
}
```

The `getUser()` function will always throw `networkFailed`, but we don’t care _what_ was thrown – all we care about is whether the call sent back a user or not.
