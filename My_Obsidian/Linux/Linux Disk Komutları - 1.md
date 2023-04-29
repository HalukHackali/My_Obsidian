#linux 

## **Dizin/Klasör Listele ve Boyutuna Bak**


```
du -sh * | sort -h
```


* * *

## **Diskleri Listele**

`
```
lsblk
```
`

* * *

## Disk Silme - Bölme - Yeniden Oluşturma

Diski biçimlendir:

`
```
fdisk /dev/YOUR_DISK
```
`

`yeni bir bölüm oluşturmak için` ard arda, `p`, `1`, `Enter`, `Enter`, ve `w` .

* * *

Biçimlendirme için:

`
```
mkfs.ext4 /dev/YOUR_DISK1
```
`

* * *

## Disk Bağla

Dizini oluşturarak başlayalım:

`
```
mkdir /mnt/hdd
```
`

Ardından diski manuel olarak monte edebiliriz:

`
```
mount /dev/YOUR_DISK1 /mnt/hdd
```
`

* * *

## Verileri taşımak istersek klasörlerden birine /mnt/hdd klasörü bağlayın

Burada `/home/yunohost.app`' teki uygulamaların büyük verilerini ve sabit diskinizdeki postaları taşımak istediğinizi düşüneceğiz.

### [Diskte alt klasörler oluşturma](https://yunohost.org/en/external_storage#5-1-creating-subfolders-o)

Başlangıç olarak, sabit sürücüde bir klasör oluşturuyoruz

```
mkdir -p /mnt/hdd/home/yunohost.app
mkdir -p /mnt/hdd/var/mail
```

* * *

## Mount Noktalarının Oluşturulması

Ardından, orijinal klasörü yeniden adlandıracağız ve boş bir isimsiz klasör oluşturacağız.

```
mv /home/yunohost.app /home/yunohost.app.bkp
mkdir /home/yunohost.app
mv /var/mail /var/mail.bkp
mkdir /var/mail
```

Daha sonra, sabit sürücümüzdeki klasörü ağaçtaki yeni boş konuma bağlamak için `mount --bind` komutunu kullanabiliriz.

```
mount --bind /mnt/hdd/home/yunohost.app /home/yunohost.app
mount --bind /mnt/hdd/var/mail /var/mail
```

* * *

## Verilerin Kopyalanması

Ardından, tüm klasör ve dosya özelliklerini koruyarak verileri kopyalıyoruz. Bu işlem biraz zaman alabilir, başka bir terminalle, montaj noktasıyla ilişkili ağırlığı gözlemleyerek evrimi kontrol edebilirsiniz.`df -h`

```
cp -a /home/yunohost.app.bkp/. /home/yunohost.app/
cp -a /var/mail.bkp/. /var/mail/
```

Bu yapıldıktan sonra, içeriğin orada olduğunu `ls` ile kontrol edin:

```
ls -la /home/yunohost.app/
ls -la /var/mail/
```

* * *

## Önyüklemede Otomatik Olarak Monte Edin[](https://yunohost.org/en/external_storage#6-automatically-mount-on-)[](https://yunohost.org/en/external_storage#6-automatically-mount-on-)

Başlangıç olarak, diskimizin UUID'sini (evrensel tanımlayıcı) şu şekilde bulalım:

```
blkid | grep "/dev/YOUR_DISK1:"
# Returns something like :
# /dev/sda1:UUID="cea0b7ae-2fbc-4f01-8884-3cb5884c8bb7" TYPE="ext4" PARTUUID="34e4b02c-02"
```

`/etc/fstab` dosyasına önyükleme sırasında disklerin bağlanmasını işleyen bir satır ekleyelim. Bu yüzden dosyayı `nano` ile açıyoruz:

```
nano /etc/fstab
```

Ardından dosyanın sonuna şu satırları ekleyin:

```
UUID="cea0b7ae-2fbc-4f01-8884-3cb5884c8bb7" /mnt/hdd ext4 defaults,nofail 0 0
/mnt/hdd/home/yunohost.app /home/yunohost.app none defaults,bind 0 0
/mnt/hdd/var/mail /var/mail none defaults,bind 0 0
```

(bu satır önceki bilgi ve seçimlere göre uyarlanmalıdır)

Use Ctrl+X then `y` to save.

Daha sonra diskin ve alt klasörlerin otomatik olarak bağlanıp bağlanmadığını kontrol etmek için sistemi yeniden başlatmayı deneyebilirsiniz.

* * *

## Eski verileri Temizle
`
```
rm -Rf /home/yunohost.app.bkp rm -Rf /var/mail.bkp
```