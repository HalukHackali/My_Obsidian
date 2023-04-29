#yazılım #swift 

Bir koleksiyon, sıralı bir içerik kümesini yönetir ve onu özelleştirilebilir ve son derece görsel bir düzende sunar.

<img src="https://developer.apple.com/design/human-interface-guidelines/images/intro/components/collection-view-intro_2x.png" alt="" width="319" height="179"> 

Genel olarak konuşursak, koleksiyonlar image- tabanlı içerik göstermek için idealdir.

## En iyi uygulamalar

**Mümkün olduğunda standart satır veya ızgara düzenini kullanın.** Koleksiyonlar, içeriği varsayılan olarak yatay bir satırda veya bir ızgarada görüntüler; bunlar, insanların beklediği basit, etkili görünümlerdir. İnsanların kafasını karıştırabilecek veya kendisine gereksiz yere dikkat çekebilecek özel bir düzen oluşturmaktan kaçının.

**Metin için koleksiyon yerine tablo kullanmayı düşünün.** Kaydırılabilir bir listede görüntülendiğinde metinsel bilgileri görüntülemek ve sindirmek genellikle daha basit ve daha verimlidir.

**Bir öğe seçmeyi kolaylaştırın.** Koleksiyonunuzdaki bir öğeye ulaşmak çok zorsa, insanlar istedikleri içeriğe ulaşmadan önce hayal kırıklığına uğrayacak ve ilgilerini kaybedeceklerdir. Odağı net tutmak ve içeriğin üst üste gelmesini önlemek için görüntülerin etrafında yeterli dolgu kullanın.

**Gerektiğinde özel etkileşimler ekleyin.** Varsayılan olarak, insanlar seçmek için dokunabilir, düzenlemek için dokunup basılı tutabilir ve kaydırmak için kaydırabilir. Uygulamanız gerektiriyorsa, özel eylemler gerçekleştirmek için daha fazla hareket ekleyebilirsiniz.

**Kişiler öğeleri eklerken, silerken veya yeniden sıralarken geri bildirim sağlamak için animasyonları kullanmayı düşünün.** Koleksiyonlar bu eylemler için standart animasyonları destekler ve ayrıca özel animasyonlar da kullanabilirsiniz.

## Platform değerlendirmeleri

*macOS veya tvOS için ek husus yok. WatchOS'ta desteklenmez.*

### iOS, iPadOS

**Dinamik düzen değişiklikleri yaparken dikkatli olun.** Bir koleksiyonun düzeni dinamik olarak değişebilir. Herhangi bir değişikliğin mantıklı olduğundan ve izlenmesinin kolay olduğundan emin olun. Mümkünse, açık bir eyleme yanıt vermediği sürece, insanlar onu görüntülerken ve onunla etkileşimde bulunurken düzeni değiştirmekten kaçınmaya çalışın.