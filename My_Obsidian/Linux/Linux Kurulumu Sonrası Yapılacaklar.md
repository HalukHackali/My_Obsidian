#linux 

## **Fedora İçin;**

### 1\. MS Fontlarını Ekle:

```bash
sudo dnf upgrade --refresh
```

```bash
sudo dnf install curl cabextract xorg-x11-font-utils fontconfig
```

```bash
sudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

### Remove Microsoft Fonts

```bash
sudo dnf autoremove msttcore-fonts-installer
```

* * *

### 2\. Distrobox Kurulumu:

Link: [Yusuf İPEK - YouTube - Distrobox İncelemsi](https://www.youtube.com/watch?v=VT40wGY6zCE "Yusuf İPEK - Distrobox İncelemsi")

* * *

### 3\. Disk Swap Alanını Küçültme:

Takas alnını değiştirmene gerek yok. Zaten zram kullanıyor. Silme istersen aşağıdaki adımları uygula:

KDE Bölümlendrme Yöneticisi Aç > zram0 > Takas Alanını Devre Dışı Bırak > Sil

* * *

### 4\. Multimedya Eklentilerini Kurun

**Ortam codec bileşenlerini yüklemek istiyorsanız, aşağıdaki komutları kullanın:**

```bash
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel

sudo dnf install lame\* --exclude=lame-devel

sudo dnf group upgrade --with-optional Multimedia

sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin

# Bu komut, ses ve video paketlerinin ihtiyaç duyduğu paketleri kuracaktır:

sudo dnf groupupdate sound-and-video
```

### 5\. SSD Disk Optimizasyonu (trim) 

```bash
[haluk@lenovo ~]$ sudo systemctl status fstrim.timer
[sudo] password for haluk: 
● fstrim.timer - Discard unused blocks once a week
     Loaded: loaded (/usr/lib/systemd/system/fstrim.timer; enabled; preset: enabled)
     Active: active (waiting) since Sun 2023-03-05 15:07:40 +03; 4h 10min ago
      Until: Sun 2023-03-05 15:07:40 +03; 4h 10min ago
    Trigger: Mon 2023-03-06 00:36:20 +03; 5h 18min left
   Triggers: ● fstrim.service
       Docs: man:fstrim

Mar 05 15:07:40 lenovo systemd[1]: Started fstrim.timer - Discard unused blocks once a week.
```

**`sudo systemctl start fstrim.timer`**

* * *

### 6\. Libraries to control, scan and zap on Digital TV channel

**libdvbv5-1.22.1-4.fc37.x86_64**  sLibraries to control, scan and zap on Digital TV channel 
**v4l-utils-1.22.1-4.fc37.x86_64** Utilities for video4linux and DVB devices

**\[haluk@lenovo ~\]$ v4l2-ctl --list-devices**

* * *

### 7\. Codec Install

`[haluk@lenovo ~]$ sudo dnf install a52dec faac faad2 flac jasper lame libdca libdv libmad libmpeg2 libtheora libvorbis opus wavpack x264 xvidcore`

* * *

### 8.