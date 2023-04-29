#linux 

Tek bir statik IP adresi ile iki farklı fiziksel sunucuda barınan iki farklı web sitesi (farklı domainlerle) dış dünyaya açmak için aşağıdaki adımları takip edebilirsiniz:

1.  İlk olarak, her bir web sitesi için ayrı bir web sunucusu kurmanız gerekiyor. Apache veya Nginx gibi popüler web sunucusu yazılımları, bu amaçla kullanılabilir.
    
2.  Ardından, her bir web sunucusunu yapılandırmanız gerekiyor. Yapılandırma işlemi, web sunucusu yazılımınızın belgelerinde ayrıntılı olarak açıklanmaktadır. Her web sunucusu, kendisine ait bir kök dizinindeki web sayfalarını sunacaktır.
    
3.  İkinci olarak, bir yük dengeleyici (load balancer) kurmanız gerekiyor. Bu, gelen istekleri farklı web sunucularına yönlendirecektir. HAProxy veya Nginx gibi bir yük dengeleyici yazılımı kullanılabilir.
    
4.  Yük dengeleyiciyi yapılandırırken, her bir web sunucusunun IP adresini ve port numarasını belirtmelisiniz. Bu, gelen trafik yükünün doğru şekilde yönlendirilmesini sağlar. Örneğin, web sitesi 1 için 10.0.0.1:80 ve web sitesi 2 için 10.0.0.2:80 gibi.
    
5.  Yük dengeleyicinin aynı zamanda, gelen trafik için doğru web sunucusuna yönlendirilmesi için, HTTP host headerlarını kontrol etmesi gerekiyor. Bu, her isteğin hangi web sitesine ait olduğunu belirlemek için kullanılır. Örneğin, web sitesi 1 için "Host: site1.com" ve web sitesi 2 için "Host: site2.com" gibi.
    
6.  Son olarak, her bir alan adı için DNS kaydı oluşturmanız gerekiyor. Bu, her bir alan adının IP adresinin yük dengeleyici IP adresine yönlendirilmesini sağlar.
    

Yukarıdaki adımları takip ederek, aynı IP adresi kullanarak iki farklı web sitesini farklı domainlerle dış dünyaya açabilirsiniz. Ancak, bu işlem biraz karmaşık ve teknik olduğundan, tecrübeli bir sistem yöneticisi veya konu hakkında bilgi sahibi biri tarafından yardım almanız önerilir.

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

* * *

**Evde Linux için bir web çiftliği kurmak, yüksek kullanılabilirlik ve performans sağlayan birkaç sunucuyu birden yönetmek anlamına gelir. Bu işlemi gerçekleştirmek için aşağıdaki adımları takip edebilirsiniz:**

1.  İlk olarak, hangi Linux dağıtımını kullanacağınıza karar verin. Web çiftliğinizi yönetmek için genellikle Debian, Ubuntu, CentOS veya Fedora gibi yaygın dağıtımlar kullanılır. Dağıtımınızı seçin ve yükleyin.
    
2.  Ardından, web sunucusu yazılımınızı seçin. Apache veya Nginx, Linux için en popüler web sunucularından ikisidir. İkisi arasındaki seçim, ihtiyaçlarınıza ve tercihlerinize bağlıdır. Her ikisi de yüksek performans ve güvenilirlik sağlayabilir.
    
3.  Web çiftliği için bir yük dengeleyici seçin. Yük dengeleyici, gelen trafik yükünü birden fazla sunucu arasında dağıtmak için kullanılır. HAProxy veya Nginx gibi birçok yük dengeleyici yazılımı vardır.
    
4.  Sunucularınız arasında veri senkronizasyonunu sağlamak için bir dosya senkronizasyon yazılımı kullanın. Bu, aynı verilerin her sunucuda mevcut olmasını ve bir sunucuda yapılan değişikliklerin diğer sunuculara yansıtılmasını sağlar. Bu amaçla, rsync veya unison gibi yazılımlar kullanılabilir.
    
5.  Son olarak, web çiftliğinizin her bir sunucusunu yapılandırın. Sunucuları yapılandırırken, yük dengeleyiciyi yapılandırın ve her sunucu için dosya senkronizasyonunu ayarlayın. Web sunucusunu ayarlayın ve belirli bir sunucunun yanıt verememesi durumunda diğer sunucuların nasıl tepki vereceğini belirleyin.
    

Yukarıdaki adımları takip ederek, evde Linux için bir web çiftliği kurabilir ve yüksek kullanılabilirlik ve performans sağlayabilirsiniz. Ancak bu işlem, biraz karmaşık ve teknik olduğundan, tecrübeli bir Linux kullanıcısı olmanız veya konu hakkında bilgi sahibi biri tarafından yardım almanız önerilir.

* * *

**İki farklı Raspberry Pi'ye kurulu ve farklı web siteleri barındıran Nginx sunucuları için modem/router ayarları şu şekilde yapılabilir:**

1.  Her Raspberry Pi için bir dahili IP adresi yapılandırın. Bu adresler, Raspberry Pi'lerin ağ yapılandırma dosyaları (örneğin, /etc/network/interfaces dosyası) aracılığıyla yapılandırılabilir. Dahili IP adresleri, Raspberry Pi'lerin bulunduğu ağ alt ağına uygun olmalıdır.
    
2.  Her Raspberry Pi'de Nginx web sunucusu yapılandırın. Her sunucu için farklı bir HTTP port numarası ayarlayın. Örneğin, birinci Raspberry Pi için 80 numaralı HTTP portu ve ikinci Raspberry Pi için 8080 numaralı port gibi. HTTP port numaraları Nginx yapılandırma dosyasında belirtilebilir.
    
3.  Modem/router'ın port yönlendirme ayarları yapılandırılmalıdır. Her Raspberry Pi için, Nginx HTTP port numarası belirli bir dış IP adresine yönlendirerek, trafiği ilgili Raspberry Pi'ye iletecektir.
    
4.  Her Raspberry Pi'de barındırılan web siteleri için ayrı ayrı sanal ana bilgisayar yapılandırması yapılmalıdır. Nginx için, bu yapılandırma /etc/nginx/sites-available/default dosyasında yapılabilir. Her sanal ana bilgisayar, ilgili Raspberry Pi'nin HTTP port numarasına atanan IP adresini kullanarak tanımlanmalıdır.
    
5.  DNS ayarları yapılandırılmalıdır. Her web sitesi için farklı bir alan adı belirleyin ve DNS kayıtlarını, her alan adı için doğru dış IP adresine yönlendirerek yapılandırın.
    

Bu yapılandırmalar tamamlandıktan sonra, her Raspberry Pi'nin web sunucusu, ayrı bir web sitesi olarak dış dünyaya açılacak ve modem/router, gelen trafiği doğru Raspberry Pi'ye yönlendirecektir. Port çakışmalarını önlemek için her Raspberry Pi için farklı bir HTTP port numarası kullanılması önemlidir.

* * *

**H298A V9. modem/router için iki farklı Raspberry Pi server port yönlendirme ve DMZ s**

**H298A V9 modem/router için iki farklı Raspberry Pi sunucu için port yönlendirme ve DMZ ayarlamak için şu adımları izleyebilirsiniz:**

1.  Raspberry Pi'lerinize statik IP adresleri verin. Raspberry Pi'lerinize IP adresleri vermek için ağ yapılandırma dosyalarını değiştirebilirsiniz. Bu dosyaların yolu Raspberry Pi'nin kullandığı işletim sistemine göre değişebilir. Örneğin, Raspbian işletim sistemi kullanan bir Raspberry Pi için /etc/dhcpcd.conf dosyasını değiştirebilirsiniz.
    
2.  Raspberry Pi'lerinizde çalışan web sunucularının port numaralarını belirleyin. Örneğin, birinci Raspberry Pi için 80 numaralı HTTP portu ve ikinci Raspberry Pi için 8080 numaralı port gibi.
    
3.  H298A V9 modem/router arayüzüne erişin ve Ayarlar bölümüne gidin.
    
4.  Sol menüden NAT ve DMZ seçeneğini seçin.
    
5.  Port Yönlendirme bölümüne gidin ve "Yeni Port Yönlendirme Kuralı" düğmesini tıklayın.
    
6.  İlk Raspberry Pi için bir port yönlendirme kuralı oluşturmak için aşağıdaki bilgileri girin:
    
    - Servis Adı: Bir isim belirleyin (örneğin, "Raspberry Pi 1").
    - Protokol: HTTP veya TCP gibi bir protokol seçin.
    - Dış Port: Dış IP adresi üzerinden gelen trafik için bir port numarası belirleyin (örneğin, 80).
    - İç IP Adresi: İlk Raspberry Pi'nin statik IP adresini girin.
    - İç Port: İlk Raspberry Pi'nin web sunucusunda kullanılan HTTP port numarasını girin (örneğin, 80).
7.  İkinci Raspberry Pi için bir port yönlendirme kuralı oluşturmak için aşağıdaki bilgileri girin:
    
    - Servis Adı: Bir isim belirleyin (örneğin, "Raspberry Pi 2").
    - Protokol: HTTP veya TCP gibi bir protokol seçin.
    - Dış Port: Dış IP adresi üzerinden gelen trafik için bir port numarası belirleyin (örneğin, 8080).
    - İç IP Adresi: İkinci Raspberry Pi'nin statik IP adresini girin.
    - İç Port: İkinci Raspberry Pi'nin web sunucusunda kullanılan HTTP port numarasını girin (örneğin, 8080).
8.  DMZ bölümüne gidin ve "DMZ Hedefi Ekle" düğmesini tıklayın.
    
9.  DMZ Hedefi Ekleme bölümünde, "DMZ Hedefi Ekle" düğmesini tıklayın.
    
10. İlk Raspberry Pi'nin IP adresini girin.
    
11. "Değişiklikleri Kaydet" düğmesini tıklayın.
    
12. Bu işlemleri
    

**Öncelikle, DMZ'yi etkinleştirmek için aşağıdaki adımları izleyebilirsiniz:**

1.  Modem/router'ınızın yönetim arayüzüne giriş yapın. Tarayıcınızın adres çubuğuna modeminizin IP adresini yazarak yönetim arayüzüne erişebilirsiniz. H298A V9 modem/router'ın varsayılan IP adresi 192.168.1.1'dir.
    
2.  Yönetim arayüzüne girdikten sonra, "Gelişmiş Ayarlar" sekmesini açın.
    
3.  "NAT" bölümüne gidin ve "DMZ" seçeneğini seçin.
    
4.  DMZ'yi etkinleştirmek için "DMZ Durumu" seçeneğini "Açık" olarak seçin.
    
5.  DMZ'de kullanmak istediğiniz Raspberry Pi server'ın IP adresini girin ve "Kaydet" düğmesine tıklayın.
    
**Port yönlendirmesi için aşağıdaki adımları izleyebilirsiniz:**

1.  Yönetim arayüzüne giriş yapın ve "Gelişmiş Ayarlar" sekmesini açın.
    
2.  "NAT" bölümüne gidin ve "Port Yönlendirme" seçeneğini seçin.
    
3.  Raspberry Pi server'larınız için port yönlendirmesi yapmak istediğiniz portları seçin ve Raspberry Pi server'ların IP adreslerini girin.

4.  "Kaydet" düğmesine tıklayarak port yönlendirmesi ayarlarınızı kaydedin.
    

Bu adımları tamamladıktan sonra, her Raspberry Pi server için ayrı ayrı port yönlendirme ayarlarını yapabilirsiniz ve DMZ'de bir Raspberry Pi server'ı seçerek, o server'a gelen tüm gelen bağlantılar doğrudan o server'a yönlendirilir.

Ancak, unutmayın ki DMZ'yi etkinleştirdiğinizde, seçtiğiniz Raspberry Pi server'a yönlendirilen tüm gelen bağlantılar doğrudan o server'a gider. Bu da güvenlik açısından bir risk oluşturabilir. Bu nedenle, mümkünse port yönlendirme ile istediğiniz erişimi sağlamaya çalışın ve DMZ'yi mümkün olduğunca kullanmamaya özen gösterin.