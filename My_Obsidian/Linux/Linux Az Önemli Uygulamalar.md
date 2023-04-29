#linux 
## jp2a: Görüntüleri ASCII sanatına dönüştürün

bir komut satırı aracıdır [jp2a , görüntüleri Linux terminalinde ASCII sanatına dönüştüren](https://itsfoss.com/ascii-image-converter/) . JPEG ve PNG dosyalarıyla çalışır. Ayrıca renkli çıktının ve seçtiğiniz karakter kümesinin ASCII görüntüsü olarak görünmesini sağlar.

<img decoding="async" loading="lazy" src=":/dfdc54f0236f43a6a1260482cc6fa03c" alt="jp2a" class="wp-image-99225 jop-noMdConv" srcset="https://itsfoss.com/content/images/wordpress/2022/07/jp2a.png 800w, https://itsfoss.com/content/images/wordpress/2022/07/jp2a-300x158.png 300w, https://itsfoss.com/content/images/wordpress/2022/07/jp2a-768x404.png 768w" sizes="(max-width: 800px) 100vw, 800px" width="800" height="421">

Aşağıdaki komutu kullanarak kurabilirsiniz:

```bash
sudo apt install jp2a
```

Renkli çıktıyı alabilir ve ASCII metnini şu şekilde kaydedebilirsiniz:

```bash
jp2a --output=ascii.txt --colors input.png
```

Bu türden tek program değil. Ascii-image-converter ve aynı amaç için kullanılabilecek birkaç başka araç var. Bu listede hepsini tartışmayacağım.

## lolcat: Terminalinize renk ekleyin

Peki! lolcat'in ASCII sanatıyla hiçbir ilgisi yoktur. En azından doğrudan değil.

Yine de diğer ASCII araçlarını lolcat ile birleştirebileceğiniz için bu yazının başına dahil ettim.

Peki ne yapar? cat komutuna benzer, ancak çıktısına rastgele degrade renkler ekler.

<img decoding="async" loading="lazy" src=":/e3f3178d800e473dba7e6c2ea8bafaa3" alt=" lolcat" class="wp-image-99294 jop-noMdConv" srcset="https://itsfoss.com/content/images/wordpress/2022/07/lolcat.png 734w, https://itsfoss.com/content/images/wordpress/2022/07/lolcat-300x156.png 300w" sizes="(max-width: 734px) 100vw, 734px" width="734" height="382">

Şu anda kullanışlı görünmeyebilir, ancak diğer ASCII araçlarının çıktıları lolcat aracılığıyla aktarıldığında etkisini göreceksiniz.

apt komutuyla lolcat'i kurun:

```bash
sudo apt install lolcat
```

* * *

## Terminalden Ses Kontrolü


```bash
haluk@lenovo ~$ alsamixer
```


```
┌───────────────────────────── AlsaMixer v1.2.8 ───────────────────────────────┐
│ Card: PipeWire                                       F1:  Help               │
│ Chip: PipeWire                                       F2:  System information |
│ View: F3:[Playback] F4: Capture  F5: All             F6:  Select sound card  │
│ Item: Master                                         Esc: Exit               │
│                                                                              │
│                                      ┌──┐                                    │
│                                      │  │                                    │
│                                      │  │                                    │
│                                      │  │                                    │
│                                      │  │                                    │
│                                      │  │                                    │
│                                      │  │                                    │
│                                      │▒▒│                                    │
│                                      │▒▒│                                    │
│                                      │▒▒│                                    |
│                                      │▒▒│                                    │
│                                      │▒▒│                                    │
│                                      ├──┤                                    │
│                                      │OO│                                    │
│                                      └──┘                                    │
│                                     50<>50                                   │
│                                   < Master >                                 │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

* * *