---
title: Bilgisayarları kötü amaçlı yazılımlardan koruyun
titleSuffix: Configuration Manager
description: Bilgisayarları kötü amaçlı yazılım saldırılarına karşı korumak için Configuration Manager Endpoint Protection nasıl uygulayacağınızı öğrenin.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722392"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Örnek senaryo: bilgisayarları kötü amaçlı yazılımlardan korumak için Endpoint Protection kullanın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, kuruluşunuzdaki bilgisayarları kötü amaçlı yazılımlara karşı korumak için Configuration Manager Endpoint Protection uygulayabileceğiniz örnek senaryo sunulmaktadır.  



## <a name="scenario-overview"></a>Senaryoya genel bakış

 Configuration Manager, Woodgrove Bank 'ta yüklenir ve kullanılır. Banka şu anda, bilgisayarları kötü amaçlı yazılım saldırılarına karşı korumak için System Center Endpoint Protection kullanıyor. Ayrıca, banka şirketteki tüm bilgisayarlarda Windows Güvenlik Duvarı’nın etkin olduğundan ve Windows Güvenlik Duvarı yeni bir programı engellediğinde kullanıcıların bildirim aldığından emin olmak için Windows Grup İlkesi kullanmaktadır.  

Configuration Manager yöneticileri, en son kötü amaçlı yazılımdan koruma özelliklerinden faydalanabilmesi ve kötü amaçlı yazılımdan koruma çözümünü Configuration Manager konsolundan merkezi olarak yönetebilmek için Woodgrove Bank kötü amaçlı yazılımdan koruma yazılımını System Center Endpoint Protection sürümüne yükseltmelidir. 


## <a name="business-requirements"></a>İş gereksinimleri

Bu uygulama aşağıdaki gereksinimlere sahiptir:  

- Şu anda grup ilkesi tarafından yönetilen Windows Güvenlik Duvarı ayarlarını yönetmek için Configuration Manager kullanın.  

- Bilgisayarlara kötü amaçlı yazılım tanımları indirmek için Configuration Manager yazılım güncelleştirmelerini kullanın. Yazılım güncelleştirmeleri yoksa (örneğin, bilgisayar şirket ağına bağlı değilse), bilgisayarlar Microsoft Update tanım güncelleştirmelerini indirmelidir.  

- Kullanıcıların bilgisayarları her gün hızlı bir kötü amaçlı yazılım taraması gerçekleştirmelidir. Ancak, sunucular her Cumartesi gecesi iş saatleri dışında saat 1’de tam tarama gerçekleştirmelidir.  

- Aşağıdaki olaylardan herhangi biri oluştuğunda e-posta uyarısı gönderin:  

  -   Herhangi bir bilgisayarda kötü amaçlı yazılım algılandığında  

  -   Aynı kötü amaçlı yazılım tehdidi bilgisayarların yüzde 5'inden fazlasında algılandığında  

  -   Aynı kötü amaçlı yazılım tehdidi herhangi bir 24 saatlik dönemde 5 ' ten fazla kez algılanır  

  -   24 saatlik bir dönemde 3 ' ten fazla farklı türde kötü amaçlı yazılım algılandı  

  Yöneticiler daha sonra Endpoint Protection uygulamak için aşağıdaki adımları uygulayın:  



##  <a name="steps-to-implement-endpoint-protection"></a> Endpoint Protection uygulama adımları  

|İşleme|Başvuru|  
|-------------|---------------|  
|Yöneticiler Configuration Manager Endpoint Protection temel kavramlarıyla ilgili mevcut bilgileri gözden geçirir.|Endpoint Protection hakkında genel bilgi için bkz. [Endpoint Protection](endpoint-protection.md).|  
|Yöneticiler Endpoint Protection kullanmak için gereken önkoşulları gözden geçirir ve uygular.|Endpoint Protection önkoşulları hakkında daha fazla bilgi için bkz. [Endpoint Protection planlama](../plan-design/planning-for-endpoint-protection.md).|  
|Yöneticiler Endpoint Protection site sistemi rolünü, Woodgrove Bank hiyerarşisinin en üstünde yalnızca bir site sistemi sunucusuna yükler.|Endpoint Protection site sistemi rolünün nasıl yükleneceği hakkında daha fazla bilgi için bkz. [Configure Endpoint Protection](endpoint-protection-configure.md)"Önkoşullar".|  
|Yöneticiler e-posta uyarılarını göndermek için bir SMTP sunucusunu kullanmak üzere Configuration Manager yapılandırır.<br /><br /> **Note:** Bir SMTP sunucusunu yalnızca Endpoint Protection bir uyarı oluşturulduğunda e-posta ile bildirim almak istiyorsanız yapılandırmanız gerekir.|Daha fazla bilgi için bkz. [Endpoint Protection uyarıları yapılandırma](endpoint-configure-alerts.md).|  
|Yöneticiler, Endpoint Protection istemcisini yüklemek için tüm bilgisayarları ve sunucuları içeren bir cihaz koleksiyonu oluşturur. Bu koleksiyona, **Endpoint Protection tarafından korunan tüm bilgisayarlar**adı vardır.<br /><br /> **İpucu:** Kullanıcı koleksiyonları için uyarıları yapılandıramazsınız.|Koleksiyonların nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. [koleksiyonlar oluşturma](../../core/clients/manage/collections/create-collections.md)|  
|Yöneticiler, koleksiyon için aşağıdaki uyarıları yapılandırır: <br /><br />1) **kötü amaçlı yazılım algılandı**: Yöneticiler **kritik**bir uyarı önem derecesi yapılandırır. <br /><br />2) çok **sayıda bilgisayarda aynı türde kötü amaçlı yazılım algılanır**: Yöneticiler **kritik** bir uyarı önem derecesi yapılandırır ve bilgisayarların yüzde 5 ' inden fazla kötü amaçlı yazılım algılandığında uyarının oluşturulacağını belirtir. <br /><br />3) **bir bilgisayardaki belirtilen aralıkta aynı türde kötü amaçlı yazılım sürekli olarak algılanır**: Yöneticiler kritik bir uyarı önem derecesi yapılandırır ve bir kötü amaçlı yazılım 24 saatlik bir dönemde 5 kereden fazla algılandığında uyarının oluşturulacağını belirtir. <br /><br />4) **belirtilen aralıkta aynı bilgisayar üzerinde birden çok türde kötü amaçlı yazılım algılanır**: Yöneticiler kritik bir uyarı önem derecesi yapılandırır ve 24 saatlik bir dönemde 3 ' ten fazla kötü amaçlı yazılımdan üretilmeden uyarının oluşturulacağını belirtir.<br /><br /> **Uyarı önem derecesi** değeri, Configuration Manager konsolunda ve bir e-posta iletisinde aldıkları uyarılarda görüntülenecek olan uyarı düzeyini gösterir.<br /><br /> Bunlara ek olarak, Configuration Manager konsolundaki uyarıları izleyebilmek için **Bu koleksiyonu Endpoint Protection panosunda görüntüle** seçeneğini belirleyin.|[Endpoint Protection yapılandırma](endpoint-configure-alerts.md)bölümünde "Endpoint Protection uyarılarını yapılandırma" konusuna bakın.|  
|Yöneticiler, otomatik dağıtım kuralı kullanarak tanım güncelleştirmelerini günde üç kez indirmek ve dağıtmak üzere yazılım güncelleştirmelerini Configuration Manager yapılandırır.|Daha fazla bilgi için, [tanım güncelleştirmelerini iletmek için yazılım güncelleştirmelerini Configuration Manager kullanma](endpoint-definitions-configmgr.md)konusunun "tanım güncelleştirmelerini sağlamak Için Configuration Manager yazılım güncelleştirmelerini kullanma" bölümüne bakın.|  
|Yöneticiler, Microsoft 'un önerilen güvenlik ayarlarını içeren varsayılan kötü amaçlı yazılımdan koruma ilkesindeki ayarları inceler. Bilgisayarların her gün için hızlı tarama gerçekleştirmesi için aşağıdaki ayarları değiştirir:<br /><br /> 1) **istemci bilgisayarlarda günlük hızlı tarama Çalıştır**: **Evet**.<br /><br /> 2) **günlük Hızlı Tarama zamanlaması saati**: **9:00 ÖÖ**.<br /><br /> Yöneticiler, Microsoft Update tarafından **dağıtılan güncelleştirmelerin** tanım güncelleştirme kaynağı olarak varsayılan olarak seçili olduğunu unutmayın. Bu, Configuration Manager yazılım güncelleştirmelerini almadıklarında bilgisayarların Microsoft Update tanımları indirdikleri iş gereksinimini karşılar.|[Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md)bölümüne bakın.|  
|Yöneticiler, yalnızca **Woodgrove Bank sunucuları**adlı Woodgrove Bank sunucularını içeren bir koleksiyon oluşturur.|Bkz. [koleksiyon oluşturma](../../core/clients/manage/collections/create-collections.md)|  
|Yöneticiler **Woodgrove Bank sunucu ilkesi**adlı özel bir kötü amaçlı yazılımdan koruma ilkesi oluşturur. Yalnızca **Zamanlanmış taramaların** ayarlarını ekler ve aşağıdaki değişiklikleri yapar:<br /><br /> **Tarama türü**:  **Tam**<br /><br /> **Tarama günü**:  **Cumartesi**<br /><br /> **Tarama saati**: **1:00**<br /><br /> **İstemci bilgisayarlarda günlük hızlı tarama çalıştır**:  **Hayır**.|[Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md)bölümüne bakın.|  
|Yöneticiler **Woodgrove Bank sunucu ilkesi** özel kötü amaçlı yazılımdan koruma Ilkesini **Woodgrove Bank sunucuları** koleksiyonuna dağıtır.|[Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md) makalesine bakın.|  
|Yöneticiler Endpoint Protection için yeni bir özel istemci cihaz ayarları kümesi oluşturur ve bu **Woodgrove Bank Endpoint Protection ayarlarını**adlandırır.<br /><br /> **Note:** Hiyerarşinizdeki tüm istemcilerde Endpoint Protection yüklemek ve etkinleştirmek istemiyorsanız, istemci **bilgisayarlarda Endpoint Protection Istemcisini Yönet** ve istemci **bilgisayarlara Endpoint Protection istemcisinin yüklenmesi** seçeneklerinin her ikisi de varsayılan istemci ayarlarında **Hayır** olarak yapılandırıldığından emin olun.|Daha fazla bilgi için bkz. [Endpoint Protection Için özel Istemci ayarlarını yapılandırma](endpoint-protection-configure-client.md).|  
|Endpoint Protection için aşağıdaki ayarları yapılandırır:<br /><br /> **İstemci bilgisayarlarda Endpoint Protection Istemcisini Yönet**: **Evet**<br /><br /> Bu ayar ve değer, yüklü olan mevcut Endpoint Protection istemcisinin Configuration Manager tarafından yönetilmesini sağlar.<br /><br /> **İstemci bilgisayarlara Endpoint Protection istemcisini yükle**:  **Evet**.</br></br>**Göz önünde** Configuration Manager 1802 ' den başlayarak, Windows 10 cihazlarının Endpoint Protection aracısının yüklü olması gerekmez. Windows 10 cihazlarında zaten yüklüyse, Configuration Manager kaldırmaz. Yöneticiler, en az 1802 istemci sürümünü çalıştıran Windows 10 cihazlarında Endpoint Protection aracısını kaldırabilir.|Daha fazla bilgi için bkz. [Endpoint Protection Için özel Istemci ayarlarını yapılandırma](endpoint-protection-configure-client.md).|  
|Yöneticiler, **Woodgrove Bank Endpoint Protection ayarları** istemci ayarlarını **Endpoint Protection koleksiyonu tarafından korunan tüm bilgisayarlara** dağıtır.|[Configuration Manager Endpoint Protection yapılandırma](endpoint-antimalware-policies.md)içindeki "Endpoint Protection Için özel Istemci ayarlarını yapılandırma" bölümüne bakın.|  
|Yöneticiler, etki alanı profili için aşağıdaki ayarları yapılandırarak bir ilke oluşturmak üzere Windows Güvenlik Duvarı Ilkesi oluşturma Sihirbazı 'Nı kullanır:<br /><br /> 1) **Windows güvenlik duvarını etkinleştir**: **Evet**<br /><br /> iki<br />                    **Windows Güvenlik Duvarı yeni bir programı engellediğinde kullanıcıya bildir**: **Evet**|[Endpoint Protection Için Windows Güvenlik Duvarı ilkeleri oluşturma ve dağıtma](../../protect/deploy-use/create-windows-firewall-policies.md) bölümüne bakın|  
|Yöneticiler, yeni güvenlik duvarı ilkesini daha önce oluşturdukları **Endpoint Protection korunan tüm bilgisayarlar** koleksiyonuna dağıtır.|[Endpoint Protection Için Windows Güvenlik Duvarı ilkeleri oluşturma ve dağıtma](create-windows-firewall-policies.md) bölümünde "Windows Güvenlik Duvarı Ilkesi dağıtmak için" bölümüne bakın|  
|Yöneticiler, kötü amaçlı yazılımdan koruma ve Windows Güvenlik Duvarı ilkelerini yönetmek, gerektiğinde bilgisayarlarda talep üzerine taramalar gerçekleştirmek, bilgisayarları en son tanımları indirmeye zorlamak ve kötü amaçlı yazılım algılandığında yapılması gereken diğer işlemleri belirtmek üzere Endpoint Protection için kullanılabilir yönetim görevlerini kullanır.|[Endpoint Protection için kötü amaçlı yazılımdan koruma ilkelerini ve güvenlik duvarı ayarlarını yönetme](endpoint-antimalware-firewall.md) bölümüne bakın|  
|Yöneticiler, Endpoint Protection durumunu ve Endpoint Protection tarafından gerçekleştirilen eylemleri izlemek için aşağıdaki yöntemleri kullanır:<br /><br /> 1) **izleme** çalışma alanında **güvenlik** altında **Endpoint Protection durum** düğümünü kullanarak.<br /><br /> 2) **varlıklar ve uyum** çalışma alanındaki **Endpoint Protection** düğümünü kullanarak.<br /><br /> 3) yerleşik Configuration Manager raporlarını kullanarak.|Bkz. [izleme Endpoint Protection](monitor-endpoint-protection.md)|  

 Yöneticiler, Endpoint Protection başarılı bir şekilde uygulanmasını bildirir ve ayrıca, Woodgrove Bank ' daki bilgisayarların, verilen iş gereksinimlerine göre artık kötü amaçlı yazılımdan korunduğunu onaylar. 

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz. [yapılandırma Endpoint Protection](endpoint-protection-configure.md)