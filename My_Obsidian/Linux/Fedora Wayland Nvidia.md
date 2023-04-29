#linux #fedora
# Fedora Wayland Nvidia Ekran Kartı Sürücüsünü Yükleme

Wayland, Nvidia ekran kartları için resmi bir sürücü sağlamaz, ancak açık kaynaklı Nouveau sürücüsü ile çalışır. Ancak, Nvidia'nın kendi kapalı kaynaklı sürücüsü, Nvidia Graphics Driver, daha iyi performans ve uyumluluk sağlayabilir.

Nvidia Graphics Driver'ın yüklenmesi için aşağıdaki adımları izleyebilirsiniz:

1.  Nvidia'nın web sitesine gidin ve son sürüm Nvidia Graphics Driver'ı indirin. Dosya genellikle **.run** uzantılıdır.
2.  Terminal açın ve root kullanıcısı olarak oturum açın:

`su -`
3.  İndirdiğiniz .run dosyasını çalıştırın:
`sh /path/to/NVIDIA-Linux-x86_64-xxx.xx.run`


```ad-warning
title: NOT : 
`/path/to/` kısmını indirdiğiniz dosyanın gerçek konumu ile değiştirin ve `xxx.xx` kısmını indirdiğiniz sürüm numarası ile değiştirin.
```

4.  Kurulum sihirbazını takip edin ve sürücüyü kurun.
5.  Kurulum tamamlandıktan sonra, **xorg.conf** dosyasını düzenleyin:

`nano /etc/X11/xorg.conf`

6.  Dosyanın sonuna aşağıdaki satırları ekleyin:
    
```Bash
Section "OutputClass" 
    Identifier "nvidia" 
    MatchDriver "nvidia-drm" 
    Driver "nvidia" 
    Option "AllowEmptyInitialConfiguration" 
    Option "SLI" "Auto" 
    Option "BaseMosaic" "on" 
EndSection
```
    
7.  Kaydedin ve çıkın.
8.  Bilgisayarınızı yeniden başlatın.

```ad-warning
title: NOT : 
Nvidia sürücüsü, bazı kullanıcıların yaşadığı önyükleme sorunlarına neden olabilir. Bu nedenle, kurulumdan önce yedekleme yapmanız önerilir.
```

Bu adımları izledikten sonra, Nvidia ekran kartınız Wayland'da kullanılabilir olacaktır.
