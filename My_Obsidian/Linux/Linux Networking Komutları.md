#linux 

| **Command**       | **Description**                                                                                                   |
| ------------- | ------------------------------------------------------------------------------------------------------------- |
| ip            | Ağ parametrelerini atamak ve yapılandırmak için yönlendirmeyi değiştirme                                      |
| traceroute    | Ana bilgisayara ulaşmak için paketlerin izlediği rotayı tanımlayın                                            |
| tracepath     | Ağ ana bilgisayarına giden yolu izlerken maksimum iletim birimini alır                                        |
| ping          | Genellikle ana bilgisayar ve sunucu arasındaki bağlantıyı kontrol etmek için kullanılır                       |
| ss            | Ağ soketleriyle ilgili ayrıntıları alır                                                                       |
| dig           | DNS ad sunucusu hakkında gerekli tüm bilgileri verir                                                          |
| host          | Belirli bir etki alanının ve iç organların IP adresini yazdırır                                               |
| hostname      | Çoğunlukla ana bilgisayar adını yazdırmak ve değiştirmek için kullanılır.                                     |
| curl          | Çeşitli protokolleri destekleyerek ağ üzerinden veri aktarır                                                  |
| mtr           | Ağı teşhis etmek için bir ping ve traceroute kombinasyonu kullanılır                                          |
| whois         | Kayıtlı etki alanları, IP adresleri, ad sunucuları ve daha fazlası hakkında bilgi alır                        |
| ifplugstatus  | Yerel bir Ethernet cihazının bağlantı durumunu algılar                                                        |
| iftop         | Bant genişliği ile ilgili istatistikleri izler                                                                |
| tcpdump       | Ağ trafiğini yakalamak, analiz etmek ve filtrelemek için kullanılan paket dinleme ve analiz yardımcı programı |
| ethtool       | Kullanıcıların Ethernet cihazlarını yapılandırmasına izin verir                                               |
| nmcli         | Ağ bağlantıları için sorun giderme yardımcı programı                                                          |
| nmap          | Öncelikle ağ güvenliğini denetlemek için kullanılır                                                           |
| bmon          | Gerçek zamanlı bant genişliğini izlemek için açık kaynaklı bir yardımcı program                               |
| firewalld     | Güvenlik Duvarı kurallarını yapılandırmak için CLI aracı                                                      |
| iperf         | Ağ performansını ve ayarlamayı ölçmek için yardımcı program                                                   |
| speedtest-cli | İnternet hızlarını kontrol etmek için speedtest.net'in CLI yardımcı programı                                  |
| vnstat        | Çoğunlukla ağ trafiğini ve bant genişliği tüketimini izlemek için kullanılır                                  |

* * *

### 1\. IP komutu

IP (İnternet Protokolü), sistem yöneticileri tarafından sıklıkla kullanıldığını görebileceğiniz en temel ancak yeterince önemli olanlardan biridir ve kullanım durumları, yönlendirmeyi değiştirmekten ağ parametrelerini atamaya ve yapılandırmaya kadar değişebilir.

Kullanım durumları sonsuz olsa da, size Ip komutunun en temel kullanım durumunu (bir IP adresi bulma) göstereyim:

```bash
ip address

```

```BASH
[haluk@lenovo lib]$ ip address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 54:ee:75:aa:5e:c1 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.109/24 brd 192.168.1.255 scope global dynamic noprefixroute enp3s0
       valid_lft 3401sec preferred_lft 3401sec
    inet6 fe80::1ccd:24c5:889c:aee3/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 68:07:15:51:dc:d1 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.107/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp2s0
       valid_lft 3522sec preferred_lft 3522sec
    inet6 fe80::923e:8a84:a51c:9fab/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

Benzer şekilde, Ip komutunu kullanarak cihazların durumunu sürekli olarak izlemek için de kullanabilirsiniz. `monitor`yerine seçenek `address`daha önce IP adreslerini almak için kullandığımız.

```
`ip monitor` 
```

* * *

## 2\. traceroute

traceroute komutunu kullanarak, paketlerin ana bilgisayara ulaşmak için izlediği yolu belirleyebilirsiniz. Ve veri paketlerinin iletimini ve paketler tarafından alınan atlamaları sorgulamak istediğinizde oldukça yararlı olabilir.

Varsayılan olarak, sisteminizde traceroute kurulu olmayabilir ve Debian türevi kullanıyorsanız (Ubuntu dahil), kurulum tek komut ileridedir:

```
sudo apt install traceroute
```

Örneğin, paketleri google.com'a yönlendiriyor olurdum

```
traceroute google.com
```

Varsayılan olarak traceroute, IPv4'ü kullanır, ancak bu davranışı kullanarak değiştirebilirsiniz. `-6`traceroute'un IPv6'yı kullanacağını belirten seçenek. Size nasıl olduğunu göstereyim:

* * *

## 3\. tracepath

Tracepath komutu, ağ ana bilgisayarına giden yolu izlerken MTU'yu (Maksimum İletim Birimi) keşfetmek için kullanılır. Yukarıda tartıştığım şeye oldukça benzer, ancak sudo ayrıcalıkları gerektirir ve ayrıca traceroute gibi hiçbir gerçek işlevi yoktur.

Ama her şeyden önce MTU nedir?

MTU, ağ üzerinden iletilebilen veya alınabilen en büyük çerçeve veya paketten başka bir şey değildir.

Şimdi google.com ile temel tracepath örneğine bir göz atalım.

```
tracepath google.com
```

Benzer şekilde, kullanarak hem IP adresini hem de ana bilgisayar adını yazdırabilirsiniz. `-b`seçenek.

```
tracepath -b google.com
```

* * *

## 4\. ping

[Ana bilgisayar ve sunucu arasındaki bağlantıyı kontrol etmenin en yaygın yolu olduğundan , ping (Paket İnternet Groper) komutu,](https://linuxhandbook.com/ping-command-ubuntu/) ağınızdaki sorunları giderirken en önemli komutlardan biri olarak kabul edilebilir.

Örneğin, google'a ping atıyor olurdum:

```
ping google.com
```

Burada son satır (min/avg/max), belirtilen sunucudan yanıt alma süresini gösterir.

şeklinde bir hata alıyorsanız **Ve "bash: ping: komut bulunamadı"** ile ilgili kılavuzumuza göz atabilirsiniz [, Ping'in Ubuntu'ya nasıl kurulacağı](https://linuxhandbook.com/ping-command-ubuntu/) .

* * *

## 5.ss

ss (soket istatistikleri) komutu, ağ soketi (ağ üzerinden veri göndermek ve almak için uç nokta) hakkında ayrıntılı bilgi vermek için kullanılır.

Dinleyen ve dinlemeyen tüm TCP bağlantılarını listelemek için şunu kullanmalısınız: `-at`aşağıda gösterildiği gibi seçenek:

```
ss -at
```

Benzer şekilde, aynısını kullanarak UDP bağlantı noktalarıyla da yapabilirsiniz. `-au`seçenek:

```
ss -au
```

* * *

## 6\. dig

Dig [(Domain Information Groper) komutu,](https://linuxhandbook.com/dig-command/) DNS ad sunucusu hakkında gerekli tüm bilgileri almak için kullanılır.

Dig yardımcı programını Ubuntu tabanlı dağıtımlara yüklemek için verilen komutu izleyin:

```
sudo apt install dnsutils
```

Şimdi, size belirli bir DNS'den nasıl bilgi alacağınızı göstereyim ve bu örnek için, Itsfoss.com'u DNS olarak kullanacağım.

```
dig itsfoss.com
```

* * *

## 7\. host

Host komutu esas olarak belirli bir alanın IP adresini almak için kullanılır veya alan adını belirli bir IP adresinden alabilirsiniz. Başka bir deyişle, yalnızca bir DNS arama aracıdır.

Alan adının IP'sini bulmak için, alan adını host komutuyla eklemeniz yeterlidir. Size nasıl olduğunu göstereyim:

```
host itsfoss.com
```

Benzer şekilde, alan adını almak için bir IP adresi kullanabilirsiniz:

```
host 8.8.4.4
```

* * *

## 8\. hostname

Bir süredir Linux kullanıyorsanız bu komuta aşina olmalısınız, çünkü bu çoğunlukla [sisteminizin ana bilgisayar adını](https://itsfoss.com/change-hostname-ubuntu/) ve NIS (Ağ Bilgi Sistemi) alan adını değiştirmek için kullanılır.

Herhangi bir seçenek olmadan kullanıldığında, sistemin geçerli ana bilgisayar adını alır:

```
hostname
```

[<img src=":/af2c2942a0544b5aaa667f016a8a637b" class="kg-image jop-noMdConv" alt=" ana bilgisayar adı" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/hostname.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/hostname.png 900w" sizes="(min-width: 720px) 720px" width="900" height="270">](https://itsfoss.com/content/images/wordpress/2022/08/hostname.png)

Ana bilgisayar adını, istenen ana bilgisayar adını içeren bir dosyadan değiştirmek, bu yardımcı programın bir başka ilginç özelliğidir.

```
sudo hostname -F <filename>
```

* * *

## 9\. curl

Curl (İstemci URL'si) komutu çoğunlukla ağ üzerinden veri aktarmak için kullanılır ve HTTP, FTP, IMAP ve diğerleri dahil olmak üzere çeşitli protokolleri destekler.

Bu araç, herhangi bir insan etkileşimi olmadan çalışacak şekilde oluşturulduğundan ve ayrıca uç nokta testi, Hata ayıklama ve hata günlüğünde kullanılabileceği için otomasyonda tercih edilir.

curl yardımcı programı önceden yüklenmiş olarak gelmez ve herhangi bir Debian türevi kullanıyorsanız, kurulum için aşağıdaki komutu kullanmanız yeterlidir:

```
sudo apt install curl
```

dosyaları indirmek oldukça kolaydır [curl komutunu kullanarak](https://linuxhandbook.com/curl-command-examples/) , sadece kullanmanız gerekir. `-O`seçeneği ve gitmekte fayda var!

```
curl -O [URL]
```

[<img src=":/159e94261fda4f78bb05835defb50164" class="kg-image jop-noMdConv" alt=" curl veya url" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/curl-o-url.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/curl-o-url.png 800w" sizes="(min-width: 720px) 720px" width="800" height="352">](https://itsfoss.com/content/images/wordpress/2022/08/curl-o-url.png)

Büyük dosyaları indirirken, ilerleme çubuğu oldukça kullanışlı olabilir ve aynısını curl kullanarak yapabilirsiniz. `-#`seçenek.

[<img src=":/e3854fad27a64e2fab2672cac8de603e" class="kg-image jop-noMdConv" alt="kıvırmak # o" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/curl-o.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/curl-o.png 900w" sizes="(min-width: 720px) 720px" width="900" height="285">](https://itsfoss.com/content/images/wordpress/2022/08/curl-o.png)

* * *

## [](https://itsfoss.com/content/images/wordpress/2022/08/curl-o.png)10\. mtr

Ping ve traceroute yardımcı programlarının bir birleşimidir ve esas olarak ağ teşhisi için kullanılır ve ağ yanıtı ile bağlantıya canlı bir bakış sağlar.

mtr kullanmanın en basit yolu, buna bir alan adı veya IP adresi eklemektir ve canlı bir traceroute raporu verecektir.

```
mtr [URL/IP]
```

[<img src=":/6e5070b3c0bd4fa0ac68f4aa06f15a1f" class="kg-image" alt=" mtr google.com" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/mtr-google.com_.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/mtr-google.com_.png 900w" sizes="(min-width: 720px) 720px" width="900" height="369">](https://itsfoss.com/content/images/wordpress/2022/08/mtr-google.com_.png)

Ve mtr'nin hem ana bilgisayar adlarını hem de IP adreslerini göstermesini istiyorsanız, mtr ile eşleştirebilirsiniz. `-b`aşağıda gösterildiği gibi seçenek:

```
mtr -b [URL]
```

[<img src=":/261684264c244af88fe3a1ce9ed374a2" class="kg-image" alt="mtr b" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/mtr-b.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/mtr-b.png 900w" sizes="(min-width: 720px) 720px" width="900" height="370">](https://itsfoss.com/content/images/wordpress/2022/08/mtr-b.png)

* * *

## 11\. whois

Whois, whois dizin hizmetinin istemcisi olduğu için kayıtlı alan adları, IP adresleri, ad sunucuları ve çok daha fazlası hakkında bilgi bulmanıza yardımcı olabilir.

Bu yardımcı program cihazınıza önceden yüklenmemiş olabilir ve Ubuntu tabanlı dağıtıma kurulum için verilen komutu kullanabilirsiniz:

```
sudo apt install whois
```

Genel olarak, whois komutu, verilen alan adıyla eşleştirilir:

```
whois [DomainName]
```

[<img src=":/1323b4547afb44b0b32a58f1c6862b89" class="kg-image" alt=" whois google.com" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/whois-google.com_.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/whois-google.com_.png 800w" sizes="(min-width: 720px) 720px" width="800" height="532">](https://itsfoss.com/content/images/wordpress/2022/08/whois-google.com_.png)

Alternatif olarak, alan adı yerine bir IP adresi de kullanabilirsiniz ve aynı ayrıntıları alırsınız.

* * *

## 12\. ifplugstatus

ifplugstatus, bağlantı sorunlarını temel düzeyde gidermek için en temel ancak yeterince kullanışlı olanlardan biridir. Ve yerel bir ethernetin bağlantı durumunu algılamak için kullanılır ve API'leri 3.x'ün tümü için destekleyerek mii-diag, mii-tool ve ethtool'a benzer şekilde çalışır.

Ubuntu tabanlı dağıtımlara kurulum için verilen komutu takip edebilirsiniz:

```
sudo apt install ifplugd
```

Bu yardımcı programın herhangi bir fantezi seçeneği yoktur ve genellikle herhangi biriyle eşleştirilmeden kullanılır:

```
ifplugstatus
```

## [<img src=":/c19ce5f2577647cdbcf2615f602870df" class="kg-image" alt=" ifplugstatus" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/ifplugstatus.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/ifplugstatus.png 900w" sizes="(min-width: 720px) 720px" width="900" height="223">](https://itsfoss.com/content/images/wordpress/2022/08/ifplugstatus.png)

* * *

## [](https://itsfoss.com/content/images/wordpress/2022/08/ifplugstatus.png)13\. iftop

iftop (Arayüz TOP), genellikle yöneticiler tarafından bant genişliği ile ilgili istatistikleri izlemek için kullanılır ve ağ ile ilgili sorunlarınız olduğunda bir teşhis aracı olarak da kullanılabilir.

Bu yardımcı program manuel kurulum gerektirir ve verilen komutla Ubuntu çalıştıran makinelere kolayca kurulabilir:

```
sudo apt install iftop
```

iftop herhangi bir seçenek olmadan kullanıldığında, varsayılan arayüzün bant genişliği istatistiklerini gösterir:

```
sudo iftop
```

[<img src=":/ab83730a39844579b69de4382847abf2" class="kg-image" alt="iftop" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/iftop.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/iftop.png 900w" sizes="(min-width: 720px) 720px" width="900" height="599">](https://itsfoss.com/content/images/wordpress/2022/08/iftop.png)

Ayrıca, cihaz adını sonuna ekleyerek ağ cihazını belirtebilirsiniz. `-i`seçenek.

```
sudo iftop -i <DeviceName>
```

benim durumumda, `enp1s0`bu yüzden çıktım aşağıdaki gibi olacak:

[<img src=":/cf1cfe7c85584003a9cbd0f88dbbd6a7" class="kg-image" alt="sudo iftop ve enp1s0" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-iftop-i-enp1s0.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-iftop-i-enp1s0.png 900w" sizes="(min-width: 720px) 720px" width="900" height="599">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-iftop-i-enp1s0.png)

* * *

### 14\. tcpdump

tcpdump, ağ trafiğini yakalamak, analiz etmek ve filtrelemek için kullanılan bir paket koklama ve analiz aracıdır. pcap dosyasına kaydettiği için bir güvenlik aracı olarak da kullanılabilir [Yakalanan verileri Wireshark aracılığıyla erişilebilen](https://itsfoss.com/install-wireshark-ubuntu/) .

Diğer birçok araç gibi, tcpdump önceden kurulu olarak gelmez ve Ubuntu tabanındaysanız, kurulum için verilen komutu takip edebilirsiniz.

```
sudo apt install tcpdump
```

Kurulumu tamamladıktan sonra, mevcut arayüz için aşağıda verilen yakalama paketlerini alabilirsiniz:

```
sudo tcpdump
```

[<img src=":/30475d62efd24255a47d4ade7054a3e7" class="kg-image" alt="sudo tcpdump" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-tcpdump.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-tcpdump.png 900w" sizes="(min-width: 720px) 720px" width="900" height="653">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-tcpdump.png)

Peki yakalanan paketleri pcap dosyasına kaydetmeye ne dersiniz? Size nasıl olduğunu göstereyim:

```
sudo tcpdump -w Captured_Packets.pcap -i <networkdevice>
```

[<img src=":/ed02dfc5d1d64fb4ad45e0bf55d05702" class="kg-image" alt="sudo tcpdump w" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-tcpdump-w-.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-tcpdump-w-.png 900w" sizes="(min-width: 720px) 720px" width="900" height="260">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-tcpdump-w-.png)

Kaydedilen dosyaya erişmek için şunu kullanmanız gerekir: `-r`dosya adını ekleyerek seçenek:

```
sudo tcpdump -r Captured_Packets.pcap
```

[<img src=":/bbd47e47a6ca4cfd97619f0564ec892b" class="kg-image" alt="sudo tcpdump r dosya adı" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-tcpdump-r-filename.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-tcpdump-r-filename.png 800w" sizes="(min-width: 720px) 720px" width="800" height="684">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-tcpdump-r-filename.png)

### 15\. ettool

Adından da anlaşılacağı gibi, ethtool yardımcı programı öncelikle ethernet cihazlarının yönetimi ile ilgilidir. Bu yardımcı programı kullanmak, ağ kartı hızını, otomatik anlaşmayı ve çok daha fazlasını değiştirmenize olanak tanır.

Ancak, makinenize önceden yüklenmemiş olabilir ve verilen komut kullanılarak Ubuntu ile çalışan bir makineye kurulabilir:

```
sudo apt install ethtool
```

Arayüz ayrıntılarını almak için, cihaz adını aşağıda gösterildiği gibi komutla eklemeniz yeterlidir:

```
sudo ethtool <InterfaceName>
```

[<img src=":/aa812fd28f0b4475b4293ff6b8754131" class="kg-image" alt="sudo ethtool enp1s0" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-ethtool-enp1s0.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-ethtool-enp1s0.png 900w" sizes="(min-width: 720px) 720px" width="900" height="490">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-ethtool-enp1s0.png)

### 16\. nmcli

Basit ama güçlü bir ağ sorun giderme aracı olarak, herhangi bir sistem yöneticisinin ağ sorunlarını gidermek için kullanacağı ilk yardımcı programlardan biridir ve komut dosyalarında da kullanılabilir.

Cihazların bağlantı durumunu izlemek için verilen nmcli komutunu kullanabilirsiniz:

```
nmcli dev status
```

[<img src=":/d5c2b572e66d4145b1a76b1bb2fe4c8f" class="kg-image" alt="nmcli geliştirme durumu" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/nmcli-dev-status.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/nmcli-dev-status.png 900w" sizes="(min-width: 720px) 720px" width="900" height="229">](https://itsfoss.com/content/images/wordpress/2022/08/nmcli-dev-status.png)

Herhangi bir seçenek olmadan kullanıldığında, sisteminizde bulunan tüm cihazlar hakkında bilgi getirecektir.

```
nmcli
```

[<img src=":/280403bcb8324a02b110f606741aec93" class="kg-image" alt="nmcli" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/nmcli.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/nmcli.png 900w" sizes="(min-width: 720px) 720px" width="900" height="666">](https://itsfoss.com/content/images/wordpress/2022/08/nmcli.png)

### 17\. nmap

Nmap, ağ güvenliğini keşfetmek ve denetlemek için bir araçtır. Ağ hakkında gerçek zamanlı bilgi, ağınıza bağlı IP'leri detaylı bir şekilde almanıza, port taramaya ve çok daha fazlasına olanak sağladığı için bilgisayar korsanları ve güvenlik meraklıları tarafından sıklıkla kullanılır.

Ubuntu tabanlı dağıtımlarda nmap yardımcı programının kurulumu için verilen komutu kullanın:

```
sudo apt install nmap
```

Ana bilgisayar adıyla taramaya başlayalım:

```
nmap itsfoss.com
```

[<img src=":/f97704dd92884babacc70f7777f4ceae" class="kg-image" alt="nmap itsfoss.com" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/nmap-itsfoss.com_.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/nmap-itsfoss.com_.png 900w" sizes="(min-width: 720px) 720px" width="900" height="408">](https://itsfoss.com/content/images/wordpress/2022/08/nmap-itsfoss.com_.png)

### 18\. bmon

bmon, istatistikleri daha insan dostu bir şekilde sunarak gerçek zamanlı bant genişliğini izlemek ve sorunları ayıklamak için açık kaynaklı bir yardımcı programdır. Bu aracın en iyi yanı grafik sunumudur ve çıktınızı HTML olarak bile alabilir!

bmon, popüler Linux dağıtımlarının varsayılan depolarında bulunduğu ve Ubuntu'yu da içerdiği için kurulum oldukça basittir.

```
sudo apt install bmon
```

Şimdi, sadece bmon'u başlatmanız gerekiyor ve bant genişliğini göze hoş gelen bir şekilde izleyebileceksiniz:

```
bmon
```

[<img src=":/ebc9182f4bea4f9989826b94d12911a2" class="kg-image" alt="bmon" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/bmon-800x591.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/bmon-800x591.png 800w" sizes="(min-width: 720px) 720px" width="800" height="591">](https://itsfoss.com/content/images/wordpress/2022/08/bmon-800x591.png)

### 19\. firewalld

Güvenlik duvarlarını yönetmek, ağ güvenliğinin temel parçası olarak kabul edilebilir ve bu araç, güvenlik duvarına kurallar eklemenize, yapılandırmanıza ve kaldırmanıza olanak tanır.

Ancak güvenlik duvarı manuel kurulum gerektirir ve Ubuntu tabanlı bir dağıtım kullanıyorsanız kurulum için verilen komutu kullanabilirsiniz:

```
sudo apt install firewalld
```

Örneğin, genel bölge için 80 numaralı bağlantı noktasını kalıcı olarak nasıl açabileceğinizi size gösterirdim:

```
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
```

[<img src=":/6c1f3930e69346b798dc4eb133d40f49" class="kg-image" alt="sudo güvenlik duvarı cmd kalıcı bölge = genel" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-firewall-cmd-permanent-zonepublic.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-firewall-cmd-permanent-zonepublic.png 900w" sizes="(min-width: 720px) 720px" width="900" height="241">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-firewall-cmd-permanent-zonepublic.png)

Benzer şekilde, son eklenen kuralı kaldırmak için şunu kullanmalısınız: `-remove`aşağıda gösterildiği gibi seçenek:

```
sudo firewall-cmd --zone=public --remove-port=80/tcp
```

[<img src=":/af8f5baa8d2c428db8d485f700f012bd" class="kg-image" alt="sudo güvenlik duvarı cmd bölgesi = genel kaldır" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/sudo-firewall-cmd-zonepublic-remove.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/sudo-firewall-cmd-zonepublic-remove.png 900w" sizes="(min-width: 720px) 720px" width="900" height="190">](https://itsfoss.com/content/images/wordpress/2022/08/sudo-firewall-cmd-zonepublic-remove.png)

### 20\. iperf

İperf, C ile yazılmış, kullanıcıların ağ performansı ölçümü ve ayarı yapmasına izin veren açık kaynaklı bir yardımcı programdır.

Bu araç, Ubuntu'nun varsayılan deposunda bulunur ve verilen komuttan kurulabilir:

```
sudo apt install iperf
```

Ağı izlemeye başlamak için, kullanıcıların verilen komutla bu istemciyi sunucuda başlatması gerekir:

```
iperf -s -u
```

Nerede, `-s`seçenek sunucuyu gösterir ve `-u`seçenek UDP formatı içindir.

[<img src=":/707ab028691e47b6889ae5d447d23378" class="kg-image" alt="iperf su" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/iperf-s-u.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/iperf-s-u.png 900w" sizes="(min-width: 720px) 720px" width="900" height="276">](https://itsfoss.com/content/images/wordpress/2022/08/iperf-s-u.png)

Artık sunucunuza bağlanabilirsiniz (kullanarak `-c`istemci tarafını gösteren seçenek), tercih edilen protokol için bir IP adresi yükü sağlayarak. Bu örnek için UDP ile gittim (kullanarak `-u`seçenek) 100 yük ile.

```
iperf -c 10.0.2.15 -u 100
```

[<img src=":/3966dec9eb694770991fc52fd549968f" class="kg-image" alt="iperf-c" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/iperf-c-.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/iperf-c-.png 900w" sizes="(min-width: 720px) 720px" width="900" height="430">](https://itsfoss.com/content/images/wordpress/2022/08/iperf-c-.png)

### 21\. speedtest-cli

Adından da anlaşılacağı gibi bu, speedtest.net web sitesi için CLI yardımcı programıdır. kontrol etmek için güvenilir bir kaynak istediğinizde oldukça yardımcı olabilir . [Apache 2.0 lisansı altında yayınlanan bu açık kaynaklı yardımcı program , internet hızlarını](https://itsfoss.com/network-speed-monitor-linux/) cli'den

Kurulum oldukça basittir ve bir Ubuntu tabanındaysanız, verilen komut kullanılarak kolayca kurulabilir:

```
sudo apt install speedtest-cli
```

Kurulum bölümünü tamamladığınızda, hızlarınızı test ettirmek için tek bir komut kullanmanız yeterlidir:

```
speedtest-cli
```

[<img src=":/9d28a234f12043f7babfd6bc65a607cb" class="kg-image" alt="en hızlı cli" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/speedtest-cli.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/speedtest-cli.png 900w" sizes="(min-width: 720px) 720px" width="900" height="379">](https://itsfoss.com/content/images/wordpress/2022/08/speedtest-cli.png)

### 22\. vnstat

vnstat yardımcı programı çoğunlukla sistem yöneticileri tarafından ağ trafiğini ve bant genişliği tüketimini (çoğunlukla) izlemek için kullanılır, çünkü bu araç sisteminizin ağ arabirimlerindeki trafiği izler.

Diğer herhangi bir ağ aracında olduğu gibi, vnstat'ı varsayılan depolarda bulabilirsiniz ve eğer Ubuntu'daysanız, kurulum verilen komutla yapılabilir:

```
sudo apt install vnstat
```

Herhangi bir seçenek olmadan vnstat komutunu kullanabilirsiniz ve sisteminizin mevcut tüm arayüzlerinin temel istatistiklerini getirecektir:

```
vnstat
```

[<img src=":/242731f0ecfd4c89936a8a578585a610" class="kg-image" alt="vnstate" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/vnstat.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/vnstat.png 900w" sizes="(min-width: 720px) 720px" width="900" height="360">](https://itsfoss.com/content/images/wordpress/2022/08/vnstat.png)

Canlı izleme için vnstat komutunu şununla eşleştirebilirsiniz: `-l`seçenek:

man sayfalarından en iyi şekilde nasıl yararlanılır

[<img src=":/57cbf7041a7240e59449af17c25e8972" class="kg-image" alt="vnstat" loading="lazy" srcset="https://itsfoss.com/content/images/size/w600/wordpress/2022/08/vnstat-l.png 600w, https://itsfoss.com/content/images/wordpress/2022/08/vnstat-l.png 900w" sizes="(min-width: 720px) 720px" width="900" height="260">](https://itsfoss.com/content/images/wordpress/2022/08/vnstat-l.png)