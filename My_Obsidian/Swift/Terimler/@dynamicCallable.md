#swift #yazılım 

`@dynamicCallable`, Swift dilinde bir özelliktir ve bir türün işlevsel bir çağrılabilir olarak davranmasını sağlar. Bu özellik, bir türün örneğinin fonksiyon olarak çağrılabilmesini ve argümanlarını alabilmesini sağlar.

Bu özellik, bir türün `callAsFunction` metodu ile sağlanır. Bu metot, bir fonksiyon olarak türün örneği çağrıldığında çalıştırılır. `callAsFunction` metodu, bir veya daha fazla parametre alabilir ve bir değer döndürür.

Örneğin, aşağıdaki örnek, `CallableType` adında bir tür tanımlar ve `callAsFunction` metodu kullanarak bir fonksiyon olarak çağrılabilmesini sağlar:
```swift
@dynamicCallable 
struct CallableType {     
	func callAsFunction(_ x: Int, _ y: Int) -> Int {         
	return x + y     
	} 
}
```


Bu örnekte, `CallableType` türü `@dynamicCallable` özelliği ile işaretlenir ve `callAsFunction` metodu tanımlanır. Bu sayede, `CallableType` örneği, bir fonksiyon olarak çağrılabilir hale gelir. Örneğin:
```swift
let callable = CallableType() 
let result = callable(3, 4) 
// 7
```


Bu örnekte, `callable` örneği bir fonksiyon olarak çağrılır ve `callAsFunction` metodu 3 ve 4 argümanlarını alarak çalıştırılır. Sonuç olarak, 7 döndürülür.

`@dynamicCallable` özelliği, özellikle DSL'ler (Domain-Specific Languages) gibi alan özelleştirilmiş dillerin oluşturulmasında yararlıdır. Bu özellik, türleri bir dilin doğal ifadesine yakın hale getirerek, daha okunaklı ve anlaşılır bir kod yazımı sağlar.