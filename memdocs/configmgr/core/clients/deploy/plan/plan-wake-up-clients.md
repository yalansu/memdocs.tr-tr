---
title: İstemcileri uyandırma
titleSuffix: Configuration Manager
description: LAN'da Uyandırma (WOL) kullanarak Configuration Manager istemcileri uyandırmayı planlayın.
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713264"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Configuration Manager 'da istemcilerin nasıl Uyandırılacağını planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Configuration Manager, yazılım güncelleştirmeleri ve uygulamalar gibi gerekli yazılımları yüklemek istediğinizde bilgisayarları uyku modunda Uyandırma için geleneksel uyandırma paketlerini destekler.

> [!NOTE]
> Bu makalede, LAN 'da uyandırma işlevinin daha eski bir sürümünün nasıl yapılacağı açıklanır. Bu işlevsellik, zaten LAN 'da uyanma 'nin daha yeni bir sürümünü de içeren Configuration Manager sürüm 1810 ' de mevcuttur. LAN 'da uyandırma 'nın her iki sürümü de olabilir ve birçok durumda aynı anda etkinleştirilebilir. LAN 'da uyandırma işlevleri 1810 ' de başlayan ve ya da her iki sürümü de etkinleştiren yeni sürümü hakkında daha fazla bilgi için bkz. [LAN 'Da uyandırma 'yı yapılandırma](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Configuration Manager 'da istemcileri uyandırma

 Configuration Manager, yazılım güncelleştirmeleri ve uygulamalar gibi gerekli yazılımları yüklemek istediğinizde bilgisayarları uyku modunda Uyandırma için geleneksel uyandırma paketlerini destekler.  

Uyandırma proxy 'si istemci ayarlarını kullanarak geleneksel uyandırma paketi yöntemini tamamlayabilirsiniz. Uyandırma proxy 'si, alt ağdaki diğer bilgisayarların uyanık olup olmadığını denetlemek ve gerekirse onları uyandırmak için eşler arası Protokolü ve seçili bilgisayarları kullanır. Site LAN'da Uyandırma yapılandırıldığında ve istemciler uyandırma proxy 'si için yapılandırıldığında, işlem aşağıdaki gibi çalışır:  

1. Configuration Manager istemcisi yüklü olan ve alt ağda uyku modunda olmayan bilgisayarlar, alt ağdaki diğer bilgisayarların uyanık olup olmadığını denetler. Bu denetim, her beş saniyede bir TCP/IP ping komutunu göndererek bu denetimi yapar.  

2. Başka bilgisayarlardan yanıt yoksa, uyku modunda olduğu varsayılır. Uyanık olan bilgisayarlar alt ağ için *yönetici bilgisayar* haline gelir.  

    Bir bilgisayarın uykudan başka bir nedenden dolayı yanıt vermeyebileceğinden (örneğin, kapatılmış, ağdan kaldırıldığı veya proxy uyandırma istemci ayarı artık uygulanmadığı için), bilgisayarlara her gün 2 P.M. bir uyandırma paketi gönderilir Yerel Saat. Yanıt vermeyen bilgisayarlar artık uykuda olacak şekilde kabul edilmez ve uyandırma proxy 'si tarafından uyandırılmaz.  

    Uyandırma proxy 'sini desteklemek için, her alt ağ için en az üç bilgisayarın uyanık olması gerekir. Bu gereksinime ulaşmak için, alt ağ için *koruyucu bilgisayarlar* olmak üzere üç bilgisayar belirleyici olmayan bir şekilde seçilebilir. Bu durum, herhangi bir süre etkinlik dışı kaldıktan sonra uyku veya hazırda bekleme moduna geçme gibi yapılandırılmış güç ilkesine rağmen uydukları kalabileceği anlamına gelir. Koruyucu bilgisayarlar, bakım görevlerinin sonucu olarak kapalı veya yeniden başlatma komutlarını kabul etmek. Bu eylem oluşursa, alt ağın üç koruyucu bilgisayara sahip olmaya devam edebilmesi için, kalan koruyucu bilgisayarlar alt ağda başka bir bilgisayarı uyandırır.  

3. Yönetici bilgisayarlar ağ anahtarından, Uyuyan bilgisayarlar için ağ trafiğini kendilerine yeniden yönlendirilmesini ister.  

    Yeniden yönlendirme, kaynak adres olarak uyuyan bilgisayarın MAC adresini kullanan bir Ethernet çerçevesini yayımlayan yönetici bilgisayar tarafından gerçekleştirilir. Bu davranış, ağ anahtarının, Uyuyan bilgisayar, Yönetici bilgisayarın açık olduğu bağlantı noktasına taşınmış gibi davranmasını sağlar. Yönetici bilgisayar Ayrıca, girişi ARP önbelleğinde yeni tutmak için uyuyan bilgisayarlar için ARP paketleri gönderir. Yönetici bilgisayar Ayrıca, Uyuyan bilgisayar adına ARP isteklerine yanıt verir ve uyuyan bilgisayarın MAC adresiyle yanıt verir.  

   > [!WARNING]  
   >  Bu işlem sırasında, Uyuyan bilgisayar için IP-MAC eşlemesi aynı kalır. Uyandırma proxy 'si, ağ anahtarını farklı bir ağ bağdaştırıcısı tarafından başka bir ağ bağdaştırıcısı tarafından kaydedilen bağlantı noktasını kullandığı konusunda bilgilendirerek çalışır. Ancak, bu davranış MAC Flap olarak bilinir ve standart ağ işlemleri için olağan dışı bir işlemdir. Bazı ağ izleme araçları bu davranışı arar ve bir şeyin yanlış olduğunu varsayabilir. Sonuç olarak, bu izleme araçları, uyandırma proxy 'si kullandığınızda uyarı oluşturabilir veya bağlantı noktalarını kapatabilir.  
   >   
   >  Ağ izleme araçlarınız ve hizmetleriniz MAC flaps 'ye izin vermediğinden uyandırma proxy 'si kullanmayın.  

4. Bir yönetici bilgisayar, Uyuyan bir bilgisayar için yeni bir TCP bağlantı isteği gördüğünde ve istek uyku moduna geçmeden önce dinlediği bilgisayarın dinlediği bir bağlantı noktasına geldiğinde, yönetici bilgisayar uyuyan bilgisayara bir uyandırma paketi gönderir ve ardından bu bilgisayar için trafiği yeniden yönlendirmeyi durduruyor.  

5. Uyuyan bilgisayar uyandırma paketini alır ve uyandırır. Gönderen bilgisayar bağlantıyı otomatik olarak yeniden dener ve bu kez, bilgisayar uyanık ve yanıt verebilir.  

   Uyandırma proxy 'si aşağıdaki Önkoşullara ve sınırlamalara sahiptir:  

> [!IMPORTANT]  
>  Ağ altyapısı ve ağ hizmetlerinden sorumlu ayrı bir ekibiniz varsa, değerlendirme ve test döneminde bu ekibi bilgilendirin ve dahil edin. Örneğin, 802.1 X ağ erişim denetimi kullanan bir ağda, uyandırma proxy 'si çalışmaz ve ağ hizmetini kesintiye uğratabilir. Ayrıca, uyandırma proxy 'si, araçlar diğer bilgisayarları uyandırma trafiğini tespit edildiğinde bazı ağ izleme araçlarına uyarı oluşturulmasına neden olabilir.  

-   [İstemciler ve cihazlar için desteklenen işletim sistemlerinde](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) desteklenen istemciler olarak listelenen tüm Windows işletim sistemleri LAN'da Uyandırma desteklenir.  

-   Bir sanal makinede çalışan konuk işletim sistemleri desteklenmez.  

-   İstemci ayarları kullanılarak, uyandırma proxy 'si için istemcilerin etkinleştirilmiş olması gerekir. Uyandırma proxy 'si işlemi donanım envanterine bağlı olmasa da, istemciler donanım envanteri için etkinleştirilmedikleri ve en az bir donanım envanteri göndermedikleri için uyandırma proxy 'si hizmetinin yüklenmesini raporlamaz.  

-   Ağ bağdaştırıcılarının (ve büyük olasılıkla BIOS) etkinleştirilmesi ve uyandırma paketleri için yapılandırılması gerekir. Ağ bağdaştırıcısı Uyandırma paketleri için yapılandırılmamışsa veya bu ayar devre dışıysa, Configuration Manager, uyandırma proxy 'sini etkinleştirmek üzere istemci ayarını aldığında bir bilgisayar için otomatik olarak yapılandırılır ve etkinleştirir.  

-   Bir bilgisayarda birden fazla ağ bağdaştırıcısı varsa, uyandırma proxy 'si için hangi bağdaştırıcının kullanılacağını yapılandıramazsınız; seçim belirleyici değildir. Ancak, seçilen bağdaştırıcı SleepAgent_<etki alanı\> @SYSTEM_0.log dosyasına kaydedilir.  

-   Ağ, ıCMP yankı isteklerine (en azından alt ağ içinde) izin vermelidir. ICMP ping komutlarını göndermek için kullanılan beş saniyelik aralığı yapılandıramazsınız.  

-   İletişim şifrelenmemiş ve kimliği doğrulanmamış ve IPSec desteklenmez.  

-   Aşağıdaki ağ konfigürasyonları desteklenmez:  

    -   bağlantı noktası kimlik doğrulaması ile 802.1 x  

    -   Kablosuz ağlar  

    -   MAC adreslerini belirli bağlantı noktalarına bağlayan ağ anahtarları  

    -   Yalnızca IPv6 ağları  

    -   24 saatten az DHCP kira süreleri  

Zamanlanmış Yazılım yüklemesi için bilgisayarları uyandırmak istiyorsanız, her birincil siteyi uyandırma paketlerini kullanacak şekilde yapılandırmanız gerekir.  

 Uyandırma proxy 'sini kullanmak için, birincil siteyi yapılandırmanın yanı sıra güç yönetimi uyandırma proxy 'si istemci ayarlarını dağıtmanız gerekir.  

Alt ağa yönelik yayın paketlerinin veya tek noktaya yayın paketlerinin kullanılıp kullanılmayacağını ve kullanılacak UDP bağlantı noktası numarasını belirleyin. Varsayılan olarak, geleneksel Uyandırma paketleri UDP bağlantı noktası 9 kullanılarak iletilir, ancak güvenliği artırmaya yardımcı olmak için, bu alternatif bağlantı noktası aradaki yönlendiriciler ve güvenlik duvarları tarafından destekleniyorsa site için alternatif bir bağlantı noktası seçebilirsiniz.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>LAN 'da Uyandırma için tek noktaya yayın ve alt ağa yönelik yayın arasında seçim yapın  
 Bilgisayarları geleneksel Uyandırma paketleri göndererek uyandırmayı seçerseniz, tek noktaya yayın paketleri mi yoksa alt ağ doğrudan yayın paketleri mi aktaracağınıza karar vermeniz gerekir. Uyandırma proxy 'si kullanırsanız, tek noktaya yayın paketlerini kullanmanız gerekir. Aksi takdirde, hangi iletim yönteminin seçleyeceğini belirlemenize yardımcı olması için aşağıdaki tabloyu kullanın.  

|İletim yöntemi|Avantaj|Dezavantaj|  
|-------------------------|---------------|------------------|  
|Tekli|Paket, bir alt ağ üzerindeki tüm bilgisayarlar yerine doğrudan bir bilgisayara gönderildiğinden, alt ağa yönelik yayınlarla daha güvenli çözüm.<br /><br /> Yönlendiricilerin yeniden yapılandırılmasını gerektirmeyebilir (ARP önbelleğini yapılandırmanız gerekebilir).<br /><br /> Alt ağa yönelik yayın aktarımlarına kıyasla daha az ağ bant genişliği kullanır.<br /><br /> IPv4 ve IPv6 ile desteklenir.|Uyandırma paketleri, son donanım envanteri zamanlamadan sonra alt ağ adreslerini değiştiren hedef bilgisayarları bulamaz.<br /><br /> Anahtarların UDP paketlerini iletmek için yapılandırılması gerekebilir.<br /><br /> Bazı ağ bağdaştırıcıları, tek noktaya yayın 'yi iletim yöntemi olarak kullandıklarında tüm uyku durumundaki uyandırma paketlerine yanıt vermeyebilirler.|  
|Alt ağa yönelik yayın|Aynı alt ağdaki IP adreslerini sıklıkla değiştiren bilgisayarlarınız varsa, tek noktaya göre daha yüksek başarı oranı.<br /><br /> Anahtar yeniden yapılandırması gerekli değildir.<br /><br /> Tüm uyku durumları için bilgisayar bağdaştırıcılarıyla yüksek uyumluluk oranı alt ağa yönelik yayınlar, Uyandırma paketleri göndermek için özgün iletim yöntemidir.|Saldırgan, tek noktaya yayın kullanmaktan daha az güvenli bir çözümdür, çünkü bir saldırgan, bir hatalı kaynak adresinden yönlendirilmiş yayın adresine ıCMP yankı isteklerinin sürekli akışını gönderebilir. Bu, tüm konaklarının bu kaynak adrese yanıt vermesine neden olur. Yönlendiriciler alt ağa yönelik yayınlara izin verecek şekilde yapılandırıldıysa, güvenlik nedenleriyle ek yapılandırma önerilir:<br /><br /> -Belirli bir UDP bağlantı noktası numarası kullanarak, yönlendiricileri yalnızca Configuration Manager site sunucusundan gelen IP 'ye yönelik yayınlara izin verecek şekilde yapılandırın.<br />-Configuration Manager belirtilen varsayılan olmayan bağlantı noktası numarasını kullanacak şekilde yapılandırın.<br /><br /> Alt ağa yönelik yayınları etkinleştirmek için tüm Aradaki yönlendiricilerin yeniden yapılandırılması gerekebilir.<br /><br /> Tek noktaya yayın aktarımından daha fazla ağ bant genişliği tüketir.<br /><br /> Yalnızca IPv4 ile desteklenir; IPv6 desteklenmiyor.|  

> [!WARNING]  
>  Alt ağa yönelik yayınlarla ilişkili güvenlik riskleri vardır: bir saldırgan, bir hatalı kaynak adresinden alınan Internet Denetim Iletisi Protokolü (ıCMP) yankı isteklerinin sürekli akışını, tüm ana bilgisayarların bu kaynak adrese yanıt vermesine neden olan yönlendirilmiş yayın adresine gönderebilir. Bu tür bir hizmet reddi saldırısı genellikle Smurf saldırısı olarak adlandırılır ve alt ağa yönelik yayınlar etkinleştirilmemekle genellikle azaltılmaktadır.
