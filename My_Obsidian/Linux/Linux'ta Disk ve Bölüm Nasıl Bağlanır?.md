#linux 

# Linux'ta disk ve bölüm nasıl takılır

Kullanmak istediğiniz diskleri veya bölümleri, içindeki verilere erişmeden önce bir klasöre veya bağlama noktasına bağlamanız gerekir. Oradan dosya sisteminde gezinebilecek ve okuma veya yazma işlemlerini gerçekleştirebileceksiniz.

![[f38831d5e654493c86a811670b831dba.png]]


Diskleri ve bölümleri her kullanmanız gerektiğinde manuel olarak bağlayabilir veya */etc/fstab* içine bir giriş ekleyebilirsiniz, böylece sisteminiz her önyüklendiğinde otomatik olarak bağlanır. Bu sürücüleri aygıt adı, etiketi veya **UUID** aracılığıyla bağlayabilirsiniz.

İlişkili: [How to mount disk partition using UUID in Linux](https://www.simplified.guide/linux/disk-mount-uuid "linux:disk-mount-uuid")

## Linux'ta disk veya bölüm bağlama adımları:

1.  Terminali başlatın.
    
2.  Takmak istediğiniz disk veya bölüm adını alın.
    
```bash
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0    7:0    0  55.4M  1 loop /snap/core18/1944
loop1    7:1    0  55.4M  1 loop /snap/core18/1932
loop2    7:2    0 217.9M  1 loop /snap/gnome-3-34-1804/60
loop3    7:3    0   219M  1 loop /snap/gnome-3-34-1804/66
loop4    7:4    0  64.8M  1 loop /snap/gtk-common-themes/1514
loop5    7:5    0    51M  1 loop /snap/snap-store/518
loop6    7:6    0  62.1M  1 loop /snap/gtk-common-themes/1506
loop7    7:7    0    51M  1 loop /snap/snap-store/498
loop8    7:8    0  31.1M  1 loop /snap/snapd/10707
loop9    7:9    0  31.1M  1 loop /snap/snapd/10492
sda      8:0    0    20G  0 disk 
├─sda1   8:1    0     1M  0 part 
├─sda2   8:2    0   513M  0 part /boot/efi
└─sda3   8:3    0  19.5G  0 part /
sdb      8:16   0    20G  0 disk 
└─sdb1   8:17   0    20G  0 part 
sr0     11:0    1  1024M  0 rom
 ```
    
3.  Diskin veya bölümün dosya sistemi türünü kontrol edin.
    
```
$ blkid /dev/sdb1
/dev/sdb1: UUID="ccab0f8d-3b5b-4189-9da3-23c49159c318" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="c088a647-01"
```
    
4.  Eğer mevcut değilse, bağlama noktası için bir dizin oluşturun.
    
```bash
$ mkdir disk
```
    
5.  **mount** kullanarak bölümü manuel olarak monte edin.
    
    ```
    $ sudo mount -t ext4 /dev/sdb1 disk
    [sudo] password for user:
    ```
    
6.  Sürücünün başarıyla monte edilip edilmediğini kontrol edin.
    
    ```bash
    $ df -h
    Filesystem      Size  Used Avail Use% Mounted on
    tmpfs           391M  1.8M  389M   1% /run
    /dev/sda3        20G  7.1G   12G  39% /
    tmpfs           2.0G     0  2.0G   0% /dev/shm
    tmpfs           5.0M     0  5.0M   0% /run/lock
    tmpfs           4.0M     0  4.0M   0% /sys/fs/cgroup
    /dev/sda2       512M  7.8M  505M   2% /boot/efi
    tmpfs           391M  112K  391M   1% /run/user/1000
    /dev/sdb1        20G   45M   19G   1% /home/user/disk
    ```
    
7.  Önceden monte edilmiş sürücüyü çıkarın.
    
    ```
    $ sudo umount /dev/sdb1
    ```
    
8.  Tercih ettiğiniz metin düzenleyiciyi kullanarak **/etc/fstab** dosyasını açın.
    
    ```
    $ sudo vi /etc/fstab
    ```
    
9.  Yeni bir bağlama noktası için bir giriş ekleyin.
    
    ```
    /dev/sdb1 /home/user/disk ext4 defaults 00
    ```
    
10. Tüm dosya sistemlerini **/etc/fstab** içine bağlayın.
    
    ```
    $ sudo mount -a
    ```
    
11. Sürücünün veya dosya sisteminin başarıyla monte edilip edilmediğini kontrol edin.
    
    ```
    $ df -h
    Filesystem      Size  Used Avail Use% Mounted on
    tmpfs           391M  1.8M  389M   1% /run
    /dev/sda3        20G  7.1G   12G  39% /
    tmpfs           2.0G     0  2.0G   0% /dev/shm
    tmpfs           5.0M     0  5.0M   0% /run/lock
    tmpfs           4.0M     0  4.0M   0% /sys/fs/cgroup
    /dev/sda2       512M  7.8M  505M   2% /boot/efi
    tmpfs           391M  112K  391M   1% /run/user/1000
    /dev/sdb1        20G   45M   19G   1% /home/user/disk
    ```