---
title: Endpoint Protection için planlama
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
description: Kötü amaçlı yazılımdan koruma ilkelerini ve Windows Güvenlik Duvarı güvenliğini planlayın
ms.openlocfilehash: 2e3904b7b7232e92fd4a246d2e0519ef32fb67f6
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606834"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager Endpoint Protection planlaması

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager Endpoint Protection, Configuration Manager hiyerarşinizdeki istemci bilgisayarlar için kötü amaçlı yazılımdan koruma ilkelerini ve Windows Güvenlik Duvarı güvenliğini yönetmenize olanak tanır.  

> [!IMPORTANT]  
>  Configuration Manager hiyerarşinizdeki istemcileri yönetmek için Endpoint Protection kullanmak üzere lisansa sahip olmanız gerekir.  

Configuration Manager Endpoint Protection kullandığınızda aşağıdaki avantajlara sahip olursunuz:  

-   Kötü amaçlı yazılımdan koruma ilkelerini, Windows Güvenlik Duvarı ayarlarını yapılandırın ve Microsoft Defender Gelişmiş tehdit korumasını seçili bilgisayar gruplarında yönetin  

-   İstemci bilgisayarları güncel tutmak üzere en son kötü amaçlı yazılımdan koruma tanım dosyalarını indirmek için Configuration Manager yazılım güncelleştirmelerini kullanın  

-   E-posta bildirimleri gönderin, konsol içi izlemeyi kullanın ve istemci bilgisayarlarda kötü amaçlı yazılım algılandığında yönetim kullanıcılarını bilgilendirmeye yönelik raporları görüntüleyin.  

Windows 10 bilgisayarları Endpoint Protection yönetimi için ek istemci gerektirmez. Windows 8.1 ve önceki bilgisayarlarda, Endpoint Protection Configuration Manager istemcisine ek olarak kendi istemcisini de yüklerse. Endpoint Protection istemcisi aşağıdaki özelliklere sahiptir:  

-   Kötü amaçlı yazılım ve casus yazılım algılama ve düzeltme.  

-   Rootkit algılama ve düzeltme  

-   Kritik güvenlik açığı değerlendirmesi ve otomatik tanım ve altyapı güncelleştirmeleri  

-   Ağ Denetleme Sistemi ile ağ güvenlik açığı algılama  

-   Kötü amaçlı yazılımları Microsoft 'a bildirmek için bulut koruma hizmeti ile tümleştirme. Bu hizmete katıladığınızda, Windows Defender veya Endpoint Protection istemcisi, bir bilgisayarda tanımlanmayan kötü amaçlı yazılım algılandığında kötü amaçlı yazılım koruma merkezinden en son tanımları indirebilir.  

> [!NOTE]  
>  Endpoint Protection istemcisi, Hyper-V çalıştıran bir sunucuya ve desteklenen işletim sistemlerine sahip konuk sanal makinelere yüklenebilir. Aşırı CPU kullanımını engellemek için Endpoint Protection eylemlerde yerleşik, rastgele bir gecikme vardır ve bu sayede hizmetler aynı anda çalıştırılmaz.  

  Ayrıca, Configuration Manager Endpoint Protection, Configuration Manager konsolundaki Windows Güvenlik Duvarı ayarlarını yönetmenizi sağlar.  

 [Örnek senaryo: bilgisayarları kötü amaçlı yazılımlardan korumak Için System Center Endpoint Protection kullanmak](../deploy-use/scenarios-endpoint-protection.md) Endpoint Protection ve Windows güvenlik duvarını nasıl yapılandırıp yönetebileceğinizi gösterir.  

## <a name="managing-malware-with-endpoint-protection"></a>Endpoint Protection ile Kötü Amaçlı Yazılımları Yönetme  

Configuration Manager Endpoint Protection Endpoint Protection istemci yapılandırmalarına yönelik ayarları içeren kötü amaçlı yazılımdan koruma ilkeleri oluşturmanıza olanak sağlar. Daha sonra, bu kötü amaçlı yazılımdan koruma ilkelerini istemci bilgisayarlara dağıtabilir ve **izleme** çalışma alanındaki **Endpoint Protection durum** düğümünde veya Configuration Manager raporları kullanarak izleyebilirsiniz.  

 Ek bilgiler:  

-   [Endpoint Protection için kötü amaçlı yazılımdan koruma Ilkeleri oluşturma ve dağıtma](../deploy-use/endpoint-antimalware-policies.md) -kötü amaçlı yazılımdan koruma ilkelerini, yapılandırabileceğiniz ayarların bir listesiyle oluşturun, dağıtın ve izleyin  

-   [Endpoint Protection](../deploy-use/monitor-endpoint-protection.md) izleme etkinlik raporlarını, virüslü istemci bilgisayarları ve daha fazlasını izleyin.   

-   [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkelerini ve güvenlik duvarı ayarlarını yönetme](../deploy-use/endpoint-antimalware-firewall.md) - [kötü amaçlı yazılımdan koruma](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) veya [güvenlik duvarı](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies)ilke önceliğini değiştirebilir, [istemci bilgisayarlarda bulunan kötü amaçlı yazılımları](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)düzeltebilir ve diğer görevler

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Windows Güvenlik Duvarı’nı Endpoint Protection ile yönetme  
 Configuration Manager Endpoint Protection, istemci bilgisayarlarda Windows Güvenlik Duvarı 'nın temel yönetimini sağlar. Her ağ profili için aşağıdaki ayarları yapılandırabilirsiniz:  

-   Windows Güvenlik Duvarı’nı etkinleştirme veya devre dışı bırakma.  

-   İzin verilen programlar listesindekiler dahil gelen bağlantıları engelleme.  

-   Windows Güvenlik Duvarı yeni bir programı engellediğinde kullanıcıya bildirme.  

> [!NOTE]  
>  Endpoint Protection yalnızca Windows Güvenlik Duvarının yönetilmesini destekler.  

  Endpoint Protection için Windows Güvenlik Duvarı ilkeleri oluşturma ve dağıtma hakkında daha fazla bilgi için bkz. [Endpoint Protection Için Windows Güvenlik Duvarı ilkeleri oluşturma ve dağıtma](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Gelişmiş Tehdit Koruması

Configuration Manager (geçerli dal) sürüm 1606 ' den başlayarak, Endpoint Protection daha önce Windows Defender ATP olarak bilinen Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP) yönetmenize ve izlemenize yardımcı olabilir. Microsoft Defender ATP, kuruluşların ağlarında gelişmiş saldırıları algılamasına, araştırmasına ve yanıt vermesine yardımcı olacak bir hizmettir. Bkz. [Microsoft Defender Gelişmiş tehdit koruması](../deploy-use/defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection İş Akışı  
 Configuration Manager hiyerarşinizde Endpoint Protection uygulamak üzere iş akışını anlamanıza yardımcı olması için aşağıdaki diyagramı kullanın.  

 ![Endpoint Protection İş Akışı](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Mac Bilgisayarlar ve Linux Sunucuları için Endpoint Protection İstemcisi  
 System Center, Linux ve Mac bilgisayarlar için bir Endpoint Protection istemcisi içerir. Bu istemciler Configuration Manager ile sağlanmaz; Bunun yerine, [Microsoft Toplu Lisanslama Hizmet Merkezi](https://www.microsoft.com/licensing/servicecenter/default.aspx)' nden aşağıdaki ürünleri indirmeniz gerekir.  

> [!IMPORTANT]  
>  Linux ve Mac için Endpoint Protection yükleme dosyalarını indirebilmeniz için bir Microsoft Toplu Lisanslama müşterisi olmanız gerekir.  

 Bu ürünler Configuration Manager konsolundan yönetilemez. Ancak, yükleme dosyaları ile birlikte, Operations Manager kullanarak Linux istemcisini yönetmenizi sağlayan bir System Center Operations Manager yönetim paketi sağlanır.  

 Linux ve Mac bilgisayarlar için Endpoint Protection’ı yükleme ve yönetme hakkında daha fazla bilgi için bu ürünlerle birlikte verilip **Belgeler** klasöründe bulunan belgeleri kullanın.

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager'da Endpoint Protection En İyi Yöntemleri  
 System Center 2012 Configuration Manager'da Endpoint Protection için aşağıdaki en iyi yöntemleri kullanın.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Endpoint Protection’a yönelik özel istemci ayarlarını yapılandırma  
 Endpoint Protection için istemci ayarlarını yapılandırırken, varsayılan istemci ayarlarını, hiyerarşinizdeki tüm bilgisayarlara ayarlar uygulamadıklarından kullanmayın. Bunun yerine, özel istemci ayarlarını yapılandırın ve bu ayarları hiyerarşinizdeki bilgisayar koleksiyonlarına atayın.  

 Özel istemci ayarlarını yapılandırırken aşağıdakileri yapabilirsiniz:  

-   Kuruluşunuzun farklı bölümleri için kötü amaçlı yazılımdan koruma ve güvenlik ayarlarını özelleştirin.  
-   Tüm hiyerarşiye dağıtmadan önce küçük bir bilgisayar grubunda Endpoint Protection çalıştırmanın etkilerini test edin.  
-   Endpoint Protection istemcisinin dağıtımını aşamalandırmak için zaman içinde koleksiyona daha fazla istemci ekleyin.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Yazılım güncelleştirmelerini kullanarak tanım güncelleştirmelerini dağıtma  
 Tanım güncelleştirmelerini dağıtmak için Configuration Manager yazılım güncelleştirmelerini kullanıyorsanız, tanım güncelleştirmelerini diğer yazılım güncelleştirmelerini içermeyen bir pakete yerleştirmeyi göz önünde bulundurun. Bunun yapılması, tanım güncelleştirme paketinin boyutunu küçük tutmaya ve dolayısıyla dağıtım noktalarına daha hızlı çoğaltılmasına imkan tanır.
