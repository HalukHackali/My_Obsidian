#linux 
## Önyükleme Sırasını Değiştirme

**İlk olarak, geçerli önyükleme sırasını kopyalayın. Örneğin, önyükleme sıralamam:**

`BootOrder:0012,0011,0010,0005,0000,000E,0003,0004,0001,0002,001D,000A,000C,000D`

```bash
[haluk@lenovo ~]$ efibootmgr
BootCurrent: 0012
Timeout: 2 seconds
BootOrder: 0012,0011,0010,0005,0000,000E,0003,0004,0001,0002,001D,000A,000C,000D,001E,000B,001F
```

**İlk olarak, geçerli önyükleme sırasını kopyalayın. Örneğin, önyükleme sıralamam:**

0013,0012,0014,0000,0001,0002,0003,000D,0011,0007,0008,0009,000A,000B,000C,000E

Ardından aşağıdaki komutu yazın

```baash
sudo efibootmgr -o
```

Ve önyükleme sırasını yukarıdaki komuta ekleyin.

```bash
sudo efibootmgr -o 0013,0012,0014,0000,0001,0002,0003,000D,0011,0007,0008,0009,000A,000B,000C,000E
```

Mesela  **`0012`** 'nin ilk önyükleme girişi olmasını istiyoruz. İlk olarak, geçerli önyükleme sırasını kopyalayın. Tek yapmanız gereken onu sola kaydırmak **`0013`** ve **Enter**'a basın.

`sudo efibootmgr -o 0012,0013,0014,0000,0001,0002,0003,000D,0011,0007,0008,0009,000A,000B,000C,000E`

* * *

`[haluk@lenovo ~]$ efibootmgr`

```bash
BootCurrent: 0012
Timeout: 2 seconds
BootOrder: 0012,0011,0010,0005,0000,000E,0003,0004,0001,0002,001D,000A,000C,000D,001E,000B,001F
Boot0000* Windows Boot Manager  HD(1,MBR,0x36ecdf4a,0xac,0x5cfc)/File(\EFI\Microsoft\Boot\bootmgfw.efi)57494e444f5753000100000088000000780000004200430044004f0042004a004500430054003d007b00390064006500610038003
600320063002d0035006300640064002d0034006500370030002d0061006300630031002d006600330032006200330034003400640034003700390035007d00000064000100000010000000040000007fff0400
Boot0001* Manjaro       HD(1,GPT,eb0fc6ec-49ca-4012-b229-c137e35dd00b,0x800,0x32000)/File(\EFI\Manjaro\grubx64.efi)
Boot0002* Archcraft     HD(1,GPT,4990e1db-e7d7-40c5-a09a-149c51d5d3ac,0x800,0x32000)/File(\EFI\Archcraft\grubx64.efi)
Boot0003* Fedora        HD(1,GPT,c2d61a4a-2286-41ae-bba1-ef334663b749,0x800,0xf4240)/File(\EFI\fedora\shimx64.efi)
Boot0004* Pop!_OS 22.04 LTS     HD(1,GPT,60cc6354-26f7-4cd9-ad19-0adf43d2c9cd,0x14fc4000,0x12bfff)/File(\EFI\systemd\systemd-bootx64.efi)
Boot0005* nobara        HD(1,GPT,9648abd1-3625-ea47-8601-b96011b95c5d,0x1000,0x12c000)/File(\EFI\fedora\shimx64.efi)
Boot0006  Setup FvFile(721c8b66-426c-4e86-8e99-3457c46ab0b9)
Boot0007  Boot Menu     FvFile(86488440-41bb-42c7-93ac-450fbf7766bf)
Boot0008  Diagnostic Splash     FvFile(a7d8d9a6-6ab0-4aeb-ad9d-163e59a7a380)
Boot0009  OilDiagApp    FvFile(f8397897-e203-4a62-b977-9e7e5d94d91b)
Boot000A* USB FDD:      VenMsg(bc7838d2-0f82-4d60-8316-c068ee79d25b,6ff015a28830b543a8b8641009461e49)
Boot000B* ATAPI CD:     VenMsg(bc7838d2-0f82-4d60-8316-c068ee79d25b,aea2090adfde214e8b3a5e471856a354)
Boot000C* USB CD:       VenMsg(bc7838d2-0f82-4d60-8316-c068ee79d25b,86701296aa5a7848b66cd49dd3ba6a55)
Boot000D* PCI LAN: EFI Network (IPv4)   PciRoot(0x0)/Pci(0x1c,0x5)/Pci(0x0,0x0)/MAC(54ee75aa5ec1,0)/IPv4(0.0.0.00.0.0.0,0,0){af4aa878-2a2b-4efc-a79c-f5cc8f3d3803}
Boot000E* NVMe: SAMSUNG MZVLV256HCHP-000L2              PciRoot(0x0)/Pci(0x1d,0x0)/Pci(0x0,0x0)/NVMe(0x1,00-00-00-00-00-00-00-00){99191c00-d932-4e4c-ae9a-a0b6e98eb8a4}
Boot000F* Lenovo Recovery System        File(\EFI\Microsoft\Boot\lrsBootMgr.efi)
Boot0010* ubuntu        HD(1,GPT,2c155f0e-a90f-4561-bf32-25aec3fc5fc8,0x1000,0x1e747f)/File(\EFI\ubuntu\shimx64.efi)
Boot0011* cachyos       HD(1,GPT,455df286-27ad-7048-9f8c-dc09b174b3c4,0x1000,0x96000)/File(\EFI\cachyos\grubx64.efi)
Boot0012* nobara        HD(1,GPT,a930087c-8f07-3a42-8dff-26e421abc8ee,0x1000,0x12c000)/File(\EFI\fedora\shimx64.efi)
Boot001D* USB HDD:      VenMsg(bc7838d2-0f82-4d60-8316-c068ee79d25b,33e821aaaf33bc4789bd419f88c50803)
Boot001E* ATA HDD:      VenMsg(bc7838d2-0f82-4d60-8316-c068ee79d25b,91af625956449f41a7b91f4f892ab0f600)
Boot001F* PCI LAN: EFI Network (IPv6)   PciRoot(0x0)/Pci(0x1c,0x5)/Pci(0x0,0x0)/MAC(54ee75aa5ec1,0)/IPv6([::]:<->[::]:,0,0){af4aa878-2a2b-4efc-a79c-f5cc8f3d3803}
```

* * *

## Önyükleme Girişi Ekleme

Bilgisayarınıza birden çok Linux dağıtımı yüklediyseniz ancak Linux dağıtımlarından birinin UEFI önyükleme girişi yoksa, manuel olarak ekleyebilirsiniz.

UFEI önyükleme girişi olmayan Linux dağıtımına önyükleme yapın. Ardından, GRUB önyükleyicinin EFI sürümünün kurulu olduğundan emin olun

***Fedora***

```
sudo dnf install grub2-efi-modules
```

Ardından EFI sistem bölümünü (ESP) /boot/efi/ dizini altına bağlayın. Bu örnekte, /dev/sda7 ESP'dir.

```BASH
sudo mount /dev/sda7 /boot/efi/
```

Ardından Grub önyükleme yükleyicisini ESP'ye kurun.

```
sudo grub-install /dev/sda --target=x86_64-efi --efi-directory=/boot/efi/
```

x86_64-efi, UEFI üretici yazılımı için Grub'u kuracağımız anlamına gelir. Varsayılan hedef, geleneksel BIOS üretici yazılımı için olan i386-pc'dir.

Şimdi, UEFI önyükleme menüsünde bootmgr komutuyla yeni bir giriş görmelisiniz. Donanımın altında, Grub yükleyici önce /boot/efi/EFI/&lt;label&gt;/ dizinine bir .efi booloader dosyası kurar. Genellikle grubx64.efi olarak adlandırılır. Ardından, UEFI önyükleme menüsüne yeni bir giriş eklemek için aşağıdaki komutu çalıştırır.

```
efibootmgr -c -d /dev/sda -p 7 -L <label> -l \EFI\<label>\grubx64.efi
```

Yeni eklenen giriş, önyükleme sırasında ilk olacaktır.

* * *

## Önyükleme Girişini Silme

Diyelim ki bir sabit diske birden çok Linux dağıtımı yüklediniz, bu nedenle yukarıdaki ekran görüntüsündeki gibi birden çok önyükleme girişiniz var. Ve şimdi bir Linux dağıtımını sildiniz, ancak önyükleme girişi hala orada. İlgili önyükleme girişini kaldırmak için şunu çalıştırın:

```BASH
sudo efibootmgr -b <bootnum> -B
```

Örneğin:

```bash
sudo efibootmgr -b 0014 -B
```

`-b` seçeneği önyükleme numarasını belirtir. `-B` seçeneği bu önyükleme numarasını siler.

* * *

## Önyükleme Girişini Etkin veya Etkin Değil olarak Ayarlama

Ardından yıldız işareti gelen bir önyükleme girdisi etkin olduğunu gösterir. Aksi halde pasiftir. Etkin bir önyükleme girdisi ayarlamak için şunu çalıştırın:

```
sudo efibootmgr -b <bootnum> -a
```

Bir önyükleme girişini devre dışı bırakmak için şunu çalıştırın:

```
sudo efibootmgr -b <bootnum> -A
```

Diğer bilgisayarımda Linux Mint, ne denersem deneyeyim GRUB önyükleme menüsünü her zaman gizler.
Bazen Fedora gibi başka bir Linux dağıtımı kullanmam gerekiyor.
Bu yüzden UEFI önyükleme menüsünden Linux Mint önyükleme girişini devre dışı bırakıyorum.
Artık Grub önyükleme menüsünü gizlemeyen Fedora önyükleme menüsünü kullanıyor.
Ancak, Linux Mint'i yeni bir sürüme yükselttiğinizde, sistem yükseltme prosedüründe Linux Mint önyükleme girişi geri yüklenecektir.
Linux Mint önyükleme girişini otomatik olarak devre dışı bırakmak için bir systemd hizmet dosyası ayarlayabilirim.

```
sudo nano /etc/systemd/system/disable-boot-entry.service
```

```service
[Unit]
  Description=disable Linux Mint Boot Entry
  After=multi-user.target

[Service]
  Type=oneshot
  ExecStart=/bin/bash -c '/usr/bin/efibootmgr -b 0008 -A'

[Install]
  WantedBy=multi-user.target
```

Dosyayı kaydedip kapatın. Ardından bu hizmeti etkinleştirin.

```
sudo systemctl enable disable-boot-entry.service
```

> **systemd'nin nasıl kullanılacağı hakkında daha fazla bilgi için lütfen aşağıdaki makaleyi okuyun.**
> 
> **[Systemd on Linux – Manage Services, Run Levels and](https://www.linuxbabe.com/command-line/systemd-services-run-levels-logs)**

**Umarım bu eğitim, Linux efibootmgr komutunda ustalaşmanıza yardımcı olmuştur. Canlı bir USB veya canlı CD oluşturmadan bir ISO dosyasını başlatıp açamayacağınızı hiç merak ettiniz mi? Lütfen aşağıdaki öğreticiyi okuyun:**

[**Grub2 Önyükleme Yükleyicisinden ISO Dosyalarını Önyükleme**](https://www.linuxbabe.com/desktop-linux/boot-from-iso-files-using-grub2-boot-loader)