#swift #yazılım 

`@escaping`, Swift dilinde bir özelliktir ve bir fonksiyon parametresinin, fonksiyonun çağrısının tamamlanmasından sonra da kullanılabileceğini belirtir. Bu özellik, bir fonksiyonun bir kapatma (closure) olarak kullanılmasını sağlar.

Normalde, bir fonksiyon parametresi, fonksiyonun çağrısının tamamlanmasından sonra hemen yok olur. Ancak, `@escaping` özelliği kullanılarak, bir fonksiyon parametresinin hayatta kalmasına izin verilebilir. Böylece, fonksiyonun çağrısının tamamlanmasından sonra da kapatma fonksiyonu çalışabilir.

Örneğin, aşağıdaki örnek, `perform` adında bir fonksiyon tanımlar ve bir `completionHandler` parametresi alır. `completionHandler` parametresi, `@escaping` özelliği ile işaretlenir ve fonksiyonun çağrısının tamamlanmasından sonra da kullanılabilir:

swiftCopy code

`func perform(completionHandler: @escaping () -> Void) {     DispatchQueue.main.asyncAfter(deadline: .now() + 1) {         completionHandler()     } }  perform {     print("Completed!") }`

Bu örnekte, `perform` fonksiyonu, `completionHandler` adında bir kapatma fonksiyonu parametresi alır ve `@escaping` özelliği ile işaretlenir. Fonksiyon, 1 saniye sonra `completionHandler` fonksiyonunu çağırarak tamamlanır. `perform` fonksiyonu çağrısı, bir kapatma fonksiyonu ile yapılır ve bu kapatma fonksiyonu, `Completed!` yazısını konsola yazdırır.

`@escaping` özelliği, özellikle asenkron işlemlerle uğraşırken yararlıdır. Bu özellik, asenkron fonksiyonlar için geri çağırma fonksiyonları yazarken kullanılabilir.