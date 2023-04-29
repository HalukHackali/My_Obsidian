#swift #yazılım 

`@dynamicMemberLookup`, Swift dilinde bir özelliktir ve bir türün dinamik olarak üyelerine erişimini sağlar. Bu özellik, bir türün üyelerine nokta (.) notasyonuyla erişilebilmesini sağlar ve üyelerin adı çalışma zamanında belirlenebilir.

Bu özellik, bir türün `subscript(dynamicMember:)` metodu ile sağlanır. Bu metot, bir üye erişimi yapılacağı zaman çağrılır ve erişilecek üyenin adı parametre olarak geçirilir. `subscript(dynamicMember:)` metodu, erişilecek üyeyi döndürür.

Örneğin, aşağıdaki örnek, `Person` adında bir tür tanımlar ve `@dynamicMemberLookup` özelliği kullanarak bir üye erişimini sağlar:
```swift
@dynamicMemberLookup
struct Person {
    var name: String
    var age: Int
    
    subscript(dynamicMember member: String) -> String {
        switch member {
        case "description":
            return "\(name), age \(age)"
        case "uppercaseName":
            return name.uppercased()
        default:
            fatalError("Unknown member: \(member)")
        }
    }
}
```


Bu örnekte, `Person` türü `@dynamicMemberLookup` özelliği ile işaretlenir ve `subscript(dynamicMember:)` metodu tanımlanır. Bu sayede, `Person` örneği, nokta (.) notasyonu ile üyelerine erişilebilir hale gelir. Örneğin:
```swift
let person = Person(name: "John", age: 30)
let description = person.description // "John, age 30"
let uppercaseName = person.uppercaseName // "JOHN"
```


Bu örnekte, `person` örneğinin `description` ve `uppercaseName` üyelerine nokta (.) notasyonu ile erişilir. `subscript(dynamicMember:)` metodu, ilgili üyenin adını alarak, ilgili işlemi yapar ve sonucu döndürür.

`@dynamicMemberLookup` özelliği, özellikle API'lerin oluşturulması gibi durumlarda yararlıdır. Bu özellik, türleri daha dinamik hale getirerek, kod yazımını daha esnek hale getirir.