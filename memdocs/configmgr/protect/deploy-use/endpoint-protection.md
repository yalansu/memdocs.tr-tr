---
title: Uç Nokta Koruma
titleSuffix: Configuration Manager
description: Kötü amaçlı yazılımdan koruma ilkelerini ve Windows Güvenlik Duvarı güvenliğini istemciler için yönetmeyi öğrenin.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b74a8c1daff31a8ffca8a38e6449aeeef1bb9b2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715651"
---
# <a name="endpoint-protection"></a>Uç Nokta Koruma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Endpoint Protection, Configuration Manager hiyerarşinizdeki istemci bilgisayarlar için kötü amaçlı yazılımdan koruma ilkelerini ve Windows Güvenlik Duvarı güvenliğini yönetir.  

> [!IMPORTANT]  
>  Configuration Manager hiyerarşinizdeki istemcileri yönetmek için Endpoint Protection kullanmak üzere lisansa sahip olmanız gerekir.  

 Configuration Manager Endpoint Protection kullandığınızda aşağıdaki avantajlara sahip olursunuz:  

-   Kötü amaçlı yazılımdan koruma ilkelerini, Windows Güvenlik Duvarı ayarlarını yapılandırın ve Microsoft Defender Gelişmiş tehdit korumasını seçili bilgisayar gruplarında yönetin  
-   İstemci bilgisayarları güncel tutmak üzere en son kötü amaçlı yazılımdan koruma tanım dosyalarını indirmek için Configuration Manager yazılım güncelleştirmelerini kullanın  
-   E-posta bildirimleri gönderin, konsol içi izlemeyi kullanın ve raporları görüntüleyin. Bu eylemler, istemci bilgisayarlarda kötü amaçlı yazılım algılandığında yönetici kullanıcıları bilgilendirir.  

Windows 10 ve Windows Server 2016 bilgisayarlarıyla başlayarak, Windows Defender zaten yüklüdür. Bu işletim sistemleri için, Configuration Manager istemcisi yüklediğinde Windows Defender için bir yönetim istemcisi yüklenir. Windows 8.1 ve önceki bilgisayarlarda, Endpoint Protection istemcisi Configuration Manager istemcisiyle yüklenir. Windows Defender ve Endpoint Protection istemcisi aşağıdaki yeteneklere sahiptir:  

-   Kötü amaçlı yazılım ve casus yazılım algılama ve düzeltme.  
-   Rootkit algılama ve düzeltme  
-   Kritik güvenlik açığı değerlendirmesi ve otomatik tanım ve altyapı güncelleştirmeleri  
-   Ağ Denetleme Sistemi ile ağ güvenlik açığı algılama  
-   Kötü amaçlı yazılımları Microsoft 'a bildirmek için bulut koruma hizmeti ile tümleştirme. Bu hizmete katıladığınızda, Endpoint Protection istemcisi veya Windows Defender, bir bilgisayarda tanımlanmayan kötü amaçlı yazılım algılandığında kötü amaçlı yazılım koruma merkezi 'ndeki en son tanımları indirir.  

> [!NOTE]  
>  Endpoint Protection istemcisi, Hyper-V çalıştıran bir sunucuya ve desteklenen işletim sistemlerine sahip konuk sanal makinelere yüklenebilir. Aşırı CPU kullanımını engellemek için, Endpoint Protection eylemlerin yerleşik rastgele bir gecikmesi vardır, böylece koruma hizmetleri aynı anda çalıştırılmaz.  

 Ayrıca, Windows Güvenlik Duvarı ayarlarını Configuration Manager konsolundaki Endpoint Protection yönetirsiniz.  

 [Örnek senaryo: bilgisayarları kötü amaçlı yazılımlardan korumak Için System Center Endpoint Protection kullanma](scenarios-endpoint-protection.md) Endpoint Protection ve Windows güvenlik duvarı.  


## <a name="managing-malware-with-endpoint-protection"></a>Endpoint Protection ile Kötü Amaçlı Yazılımları Yönetme  
 Configuration Manager Endpoint Protection Endpoint Protection istemci yapılandırmalarına yönelik ayarları içeren kötü amaçlı yazılımdan koruma ilkeleri oluşturmanıza olanak sağlar. Bu kötü amaçlı yazılımdan koruma ilkelerini istemci bilgisayarlara dağıtın. Ardından, **izleme** çalışma alanında **güvenlik** altındaki **Endpoint Protection durumu** düğümünde uyumluluğu izleyin. Ayrıca **Raporlama** düğümündeki Endpoint Protection raporlarını kullanın.  

 Ek bilgiler:  

-   [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md) -kötü amaçlı yazılımdan koruma ilkelerini, yapılandırabileceğiniz ayarların bir listesi ile oluşturma, dağıtma ve izleme  

-   [Endpoint Protection](monitor-endpoint-protection.md) izleme etkinlik raporlarını, virüslü istemci bilgisayarları ve daha fazlasını izleme.  

-   [Kötü amaçlı yazılımdan koruma ilkelerini ve güvenlik duvarı ayarlarını yönetme Endpoint Protection](endpoint-antimalware-firewall.md) -istemci bilgisayarlarda bulunan kötü amaçlı yazılımları Düzeltme  

-   [Endpoint Protection için günlük dosyaları](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Windows Güvenlik Duvarı’nı Endpoint Protection ile yönetme  
 Configuration Manager Endpoint Protection, istemci bilgisayarlarda Windows Güvenlik Duvarı 'nın temel yönetimini sağlar. Her ağ profili için aşağıdaki ayarları yapılandırabilirsiniz:  

-   Windows Güvenlik Duvarı’nı etkinleştirme veya devre dışı bırakma.  

-   İzin verilen programlar listesindekiler dahil gelen bağlantıları engelleme.  

-   Windows Güvenlik Duvarı yeni bir programı engellediğinde kullanıcıya bildirme.  

> [!NOTE]  
>  Endpoint Protection yalnızca Windows Güvenlik Duvarının yönetilmesini destekler.  


 Daha fazla bilgi için bkz. [Endpoint Protection Için Windows Güvenlik Duvarı ilkeleri oluşturma ve dağıtma](create-windows-firewall-policies.md).  


## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Gelişmiş Tehdit Koruması

Endpoint Protection, önceden Windows Defender ATP olarak bilinen Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP) yönetip izler. Microsoft Defender ATP hizmeti, kuruluşların kurumsal ağdaki gelişmiş saldırıları algılamasına, araştırmasına ve yanıt vermesine yardımcı olur. Daha fazla bilgi için bkz. [Microsoft Defender Gelişmiş tehdit koruması](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection İş Akışı  
 Configuration Manager hiyerarşinizde Endpoint Protection uygulamak üzere iş akışını anlamanıza yardımcı olması için aşağıdaki diyagramı kullanın.  

 ![Endpoint Protection İş Akışı](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Mac Bilgisayarlar ve Linux Sunucuları için Endpoint Protection İstemcisi  

> [!Important]  
> Mac ve Linux için System Center Endpoint Protection (SCEP) desteği (tüm sürümler) 31 Aralık 2018 tarihinde sona erer. Mac için SCEP için yeni virüs tanımlarının kullanılabilirliği ve Linux için SCEP, destek sonuna kadar sonlandırılabilir. Daha fazla bilgi için bkz. [Destek Web günlüğü gönderisinin sonu](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection, Linux ve Mac bilgisayarlar için bir Endpoint Protection istemcisi içerir. Bu istemciler Configuration Manager ile sağlanmaz. [Microsoft Toplu Lisanslama Hizmet Merkezi](https://www.microsoft.com/licensing/servicecenter/default.aspx)' nden aşağıdaki ürünleri indirin:  

-   Mac için System Center Endpoint Protection  

-   Linux için System Center Endpoint Protection  


> [!Note]  
>  Linux ve Mac için Endpoint Protection yükleme dosyalarını indirebilmeniz için bir Microsoft Toplu Lisanslama müşterisi olmanız gerekir.  

 Bu ürünler Configuration Manager konsolundan yönetilemez. Linux için istemcisini yönetmenizi sağlayan yükleme dosyaları ile birlikte System Center Operations Manager bir yönetim paketi sağlanır.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Mac bilgisayarlar ve Linux sunucuları için Endpoint Protection istemcisini alma

Mac bilgisayarlar ve Linux sunucuları için Endpoint Protection istemci yazılımı ve belgelerinin bulunduğu görüntü dosyasını indirmek için aşağıdaki adımları kullanın.
1. [Microsoft Toplu Lisanslama hizmeti Merkezi](https://www.microsoft.com/licensing/servicecenter/default.aspx)' nde oturum açın.
2. Web sitesinin en üstündeki **indirmeler ve anahtarlar** sekmesini seçin.
3. Ürün **System Center Endpoint Protection (geçerli dal)** üzerine filtreleyin.
4. **İndirmek** için bağlantıyı tıklatın
5. **Devam**’a tıklayın. **LINUX OS ve MACINTOSH OS Multilanguage 32/64 bit 1878 MB ISO Için System Center Endpoint Protection (geçerli dal-sürüm 1606)** dahil olmak üzere birkaç dosya görmeniz gerekir.
6. Dosyayı indirmek için ok simgesine tıklayın. Dosya adı **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO**.

Ocak 2018 Güncelleştirmesi (X21-67050) aşağıdaki sürümleri içerir:

- Mac için System Center Endpoint Protection 4.5.32.0 (macOS 10,13 High Sierra desteği)
- Linux için System Center Endpoint Protection 4.5.20.0 

  Linux ve Mac bilgisayarlar için Endpoint Protection istemcilerinin nasıl yükleneceği ve yönetileceği hakkında daha fazla bilgi için, bu ürünlere eşlik eden belgeleri kullanın. Bu ürün belgeleri, uygulamasının **belge** klasörüdür. ISO dosyası.
