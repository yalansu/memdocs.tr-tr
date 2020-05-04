---
title: Cihaz durumu kanıtlama
titleSuffix: Configuration Manager
description: Configuration Manager konsolunda görüntülenebilen Cihaz Sistem Durumu Kanıtlama işlevselliği hakkında bilgi edinin.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9917ec8a1ed2072903276de438f49d3f783a1284
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712452"
---
# <a name="health-attestation-for-configuration-manager"></a>Configuration Manager için durum kanıtlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yöneticiler, Configuration Manager konsolunda [Windows 10 Cihaz Durumu Kanıtlama](https://technet.microsoft.com/library/mt592023.aspx)’nın durumunu görebilir.  Cihaz durumu kanıtlama, yöneticinin istemci bilgisayarlarda aşağıdaki güvenilir BIOS, TPM ve önyükleme yazılım yapılandırmalarının etkin olduğundan emin olmasını sağlar:  

-   Erken başlatılan kötü amaçlı yazılımdan koruma - Erken başlatılan kötü amaçlı yazılımdan koruma (ELAM), bilgisayarınızı başlarken ve üçüncü taraf sürücüleri başlamadan önce korur. [ELAM nasıl açılır](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Windows BitLocker Sürücü Şifrelemesi, Windows işletim sistemi birimde depolanan tüm verileri şifrelemenizi sağlayan bir yazılımdır.  [BitLocker 'ı açma](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Güvenli Önyükleme - Güvenli Önyükleme, bilgisayarınızın yalnızca bilgisayar üreticisinin güvendiği yazılımla önyüklendiğinden emin olmaya yardımcı olmak için bilgisayar sektörünün geliştirdiği bir güvenlik standardıdır. [Güvenli Önyükleme hakkında daha fazla bilgi edinin](https://technet.microsoft.com/library/hh824987.aspx)  
-   Kod Bütünlüğü - Kod Bütünlüğü, bir sürücünün veya sistem dosyasının belleğe her yüklendiğinde bütünlüğünü doğrulayarak işletim sisteminin güvenliğini arttıran bir özelliktir. [Kod Bütünlüğü hakkında daha fazla bilgi edinin](https://technet.microsoft.com/library/dd348642.aspx)  

Bu işlevsellik, Configuration Manager tarafından yönetilen PC’lerle şirket içi kaynaklarında ve Microsoft Intune tarafından yönetilen mobil cihazlarda kullanılabilir. Yöneticiler, raporlamanın bulut veya şirket içi altyapısı aracılığıyla yapılacağını belirtebilir. Şirket içi cihaz sistem durumu kanıtlama izlemesi, yöneticinin internet erişimi olmadan istemci bilgisayarlarını izlemesini sağlar.

## <a name="enable-health-attestation"></a>Sistem durumu kanıtlamasını etkinleştir

 **Gereklilik**  

-   [Cihaz sistem durumu kanıtlama etkinken](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)Windows 10 sürüm 1607 veya windows Server 2016 sürüm 1607 çalıştıran istemci cihazları.
-   TPM 1,2 veya TPM 2 etkin cihazlar.
-   Bulut yönetimi kullanılırken, Configuration Manager istemci Aracısı ile yönetim noktası arasında *has.spserv.Microsoft.com* (bağlantı noktası 443) sistem durumu kanıtlama hizmeti (bulut yönetimi) ile iletişim. Şirket içinde, istemcinin cihaz sistem durumu kanıtlama etkin yönetim noktasıyla iletişim kurabilmesi gerekir.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager istemci bilgisayarlarında Cihaz Durumu Kanıtlama hizmet iletişimi nasıl etkinleştirilir

İnternet 'e bağlanan cihazlar için cihaz sistem durumu kanıtlama izlemeyi etkinleştirmek üzere bu yordamı kullanın.

1.  Configuration Manager konsolunda **Yönetim** > **genel bakış** > **istemci ayarları**' nı seçin.  **Bilgisayar Aracısı** ayarlarının sekmesini seçin.  
2.  **Varsayılan Ayarlar** iletişim kutusunda, **Bilgisayar Aracısı**’nı seçin, sonra **Cihaz Durumu Kanıtlama Hizmeti ile iletişimi etkinleştir**’e ilerleyin  
3.  **Cihaz Durumu Kanıtlama Hizmeti ile iletişimi etkinleştir** ’i **Evet**olarak ayarlayın, sonra **Tamam**’a tıklayın.  
4. Cihaz sistem durumunu rapor etmesi gereken cihaz koleksiyonlarını hedefleyin.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager istemci bilgisayarlarında şirket içi Cihaz Durumu Kanıtlama hizmet iletişimi nasıl etkinleştirilir
İnternet 'e bağlı olmayan şirket içi cihazlar için cihaz sistem durumu kanıtlama izlemeyi etkinleştirmek üzere bu yordamı kullanın.

Configuration Manager 1702 ' den itibaren, şirket içi cihaz durumu kanıtlama hizmeti URL 'SI yönetim noktasında internet erişimi olmayan istemci cihazlarını desteklemek için yapılandırılabilir.

1. Configuration Manager konsolunda, **Yönetim** > **genel bakış** > **Site yapılandırması** > **siteler**' e gidin.
2. Şirket içi cihaz sistem durumu kanıtlama istemcilerini destekleyen yönetim noktasıyla birincil veya ikincil siteye sağ tıklayın ve **site bileşenleri** > **yönetim noktasını**Yapılandır ' ı seçin. **Yönetim noktası bileşen özellikleri** sayfası açılır.
3. **Gelişmiş Seçenekler** sekmesinde, **Ekle** ' yi seçin ve geçerli bir şirket içi cihaz sistem durumu kanıtlama hizmeti URL 'si belirtin. Birden çok URL ekleyebilirsiniz. Birden çok şirket içi URL belirtilirse, istemciler tam kümesi alır ve hangisinin kullanılacağını rastgele seçer.
4.  Configuration Manager konsolunda **Yönetim** > **genel bakış** > **istemci ayarları**' nı seçin.  **Bilgisayar Aracısı** ayarlarının sekmesini seçin.  
5.  **Sistem durumu kanıtlama hizmeti ile Iletişimi etkinleştirmek**için aşağı kaydırın ve **Evet**olarak ayarlayın.
7.  Şirket **Içi sağlık Attestaion hizmeti kullan** seçeneğine tıklayın ve **Evet**olarak ayarlayın.
8. Cihaz sistem durumu kanıtlama raporlamasını etkinleştirmek için istemci Aracısı ayarları ile cihaz durumunu raporlamak zorunda olan cihaz koleksiyonlarını hedefleyin.

Ayrıca, cihaz durumu kanıtlama hizmeti URL 'Lerini **düzenleyebilir** veya **kaldırabilirsiniz** .

> [!NOTE]
> Configuration Manager 1702 ' e yükseltmeden önce cihaz sistem durumu kanıtlama kullandıysanız, istemci Aracısı ayarlarında belirtilen şirket içi URL 'Ler yükseltme sırasında yönetim noktası özelliklerinde önceden doldurulur. Şirket içi istemciler, yükseltilene kadar istemci Aracısı ayarlarında belirtilen URL 'YI kullanmaya devam eder. Daha sonra yönetim noktasında belirtilen URL 'Lerden birine geçiş yapar.

## <a name="monitor-device-health-attestation"></a>Cihaz durumu kanıtlamasını izleme

1.  Cihaz durumu kanıtlamayı görüntülemek için, Configuration Manager konsolunda **İzleme** , **Güvenlik** düğümüne tıklayın ve sonra da **Durumu Kanıtlama**’ya tıklayın.  
2.  Cihaz Durumu Kanıtlama görüntülenir.  

Configuration Manager Cihaz Durumu Kanıtlama şunları görüntüler:  

-   **Sistem Kanıtlama Durumu** - Uyumlu, uyumsuz, hatalı ve bilinmeyen durumlardaki cihazların paylarını gösterir  
-   **Sistem Durumu Kanıtlama Rapor Eden Cihazlar** - Cihaz Durumu Kanıtlama durumu rapor eden cihazların yüzdesini gösterir  
-   **İstemci Türüne Göre Uyumsuz Cihazlar** - Uyumsuz olan cihazların ve bilgisayarların payını gösterir  
-   **Cihaz Durumu Kanıtlama Ayarları Eksik Olan İlkler** - Cihaz durumu kanıtlama ayarı eksik olan cihazların sayısını, ayar göre listeler
