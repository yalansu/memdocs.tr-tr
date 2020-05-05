---
title: Microsoft Defender Gelişmiş Tehdit Koruması
titleSuffix: Configuration Manager
description: Kuruluşların gelişmiş saldırılara yanıt vermesini sağlayan yeni bir hizmet olan Microsoft Defender Gelişmiş tehdit koruması 'nı yönetmeyi ve izlemeyi öğrenin.
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a635ae36875984537c18c4850a3526d57ffceb31
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210154"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Gelişmiş Tehdit Koruması

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Endpoint Protection, [Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) yönetmenize ve izlemenize yardımcı olabilir (eski adıyla WINDOWS Defender ATP olarak bilinir). Microsoft Defender ATP, kuruluşların ağlarında gelişmiş saldırıları algılamasına, araştırmasına ve yanıt vermesine yardımcı olur. Configuration Manager ilkeleri Windows 10 istemcilerini eklemenize ve izlemenize yardımcı olabilir.

Microsoft Defender ATP, [Windows Defender Güvenlik Merkezi](https://securitycenter.windows.com)'ndeki bir hizmettir. İstemci ekleme yapılandırma dosyası ekleyerek ve dağıtarak, Configuration Manager dağıtım durumunu ve Microsoft Defender ATP Aracısı sistem durumunu izleyebilir. Microsoft Defender ATP, Configuration Manager istemcisini çalıştıran veya [Microsoft Intune tarafından yönetilen](https://docs.microsoft.com/intune/protect/advanced-threat-protection)bilgisayarlarda desteklenir.

## <a name="prerequisites"></a>Önkoşullar

- Microsoft Defender Gelişmiş tehdit koruması çevrimiçi hizmetine abonelik  
- Configuration Manager istemcisini çalıştıran istemci bilgisayarlar
- Aşağıdaki [desteklenen istemci işletim sistemleri](#bkmk_os) bölümünde listelenen bir işletim sistemini kullanan istemciler.

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a>Desteklenen istemci işletim sistemleri
Çalıştırmakta olduğunuz Configuration Manager sürümüne bağlı olarak, aşağıdaki istemci işletim sistemleri eklendi olabilir:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager sürüm 1910 ve öncesi

- Windows 10, sürüm 1607 ve üzeri çalıştıran istemci bilgisayarlar

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager sürüm 2002 ve üzeri
<!--5229962-->
- Windows 7 SP1
- Windows 8.1
- Windows 10, sürüm 1607 veya üzeri
- Windows Server 2008 R2 SP1
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, sürüm 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Ekleme yapılandırma dosyası oluşturma

1. [Microsoft Defender ATP çevrimiçi hizmetine](https://securitycenter.windows.com/) gidin ve oturum açın.
1. **Ayarlar**altında **makine yönetimi** ' ni seçin ve ardından **ekleme**' yi seçin.
1. Listeden eklemek istediğiniz işletim sistemlerini seçin.
   - Windows 10, Windows Server 1803 ve Windows Server 2019 ' i oluşturuyorsanız:
      1. **Configuration Manager (geçerli dal) sürüm 1606** ' i seçin ve **paketi indir**' i seçin.
      1. Sıkıştırılmış arşiv (. zip) dosyasını indirin ve içerikleri ayıklayın.
   - Başka bir Windows işletim sistemi oluşturuyorsanız: 
      1. Listeden eklemek istediğiniz işletim sistemlerini seçin. Örneğin, **Windows 7 ve 8,1** ya da **Windows Server 2008 r2 SP1, 2012 R2 ve 2016**seçeneklerinden birini belirleyin.
      1. **Çalışma alanı anahtarı** ve **çalışma alanı kimliği** değerlerini, Işlem tamamlandıktan sonra **Bağlantıyı Yapılandır** bölümünden kopyalayın.

> [!IMPORTANT]
> - Microsoft Defender ATP yapılandırma dosyası, güvenli tutulması gereken hassas bilgiler içerir.

## <a name="onboard-devices"></a>Yerleşik cihazlar

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Endpoint Protection** > **Windows Defender ATP ilkeleri** ' ne gidin ve **Windows Defender ATP İlkesi Oluştur**' u seçin. Microsoft Defender ATP Ilkesi Sihirbazı açılır.  
1. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **ekleme**' yi seçin.
1. Kuruluşunuzun Microsoft Defender ATP bulut hizmeti kiracısı tarafından sunulan yapılandırma dosyasına **gidin** .
   - **Windows 7 ve 8,1** ya da **Windows Server 2008 r2 SP1, 2012 R2 ve 2016**için **çalışma alanı anahtarını** ve **çalışma alanı kimliğini**belirtin.
   - Configuration Manager sürüm 2002 için, yalnızca Windows Server 2019 ve Windows Server 1803 veya üzeri cihazları ekleme olsanız bile **çalışma alanı anahtarı** ve **çalışma alanı kimliği** gerekir. [Microsoft Defender ATP çevrimiçi hizmeti](https://securitycenter.windows.com/)'nden**Windows 7 ve 8,1** **ekleme** >  **ayarları** > ' nı seçerek bu değerleri alın. <!--7054188-->
1. Analiz edilmek üzere yönetilen cihazlardan toplanan ve paylaşılan dosya örneklerini belirtin.  

   - **Yok**

   - **Tüm dosya türleri**  
1. Özeti gözden geçirin ve Sihirbazı doldurun.  

İstemcilere Microsoft Defender ATP ilkesini hedeflemek için **Dağıt** ' ı seçin.

## <a name="monitor"></a>İzleme

1. Configuration Manager konsolunda **izleme** > **güvenliği** ' ne gidin ve ardından **Windows Defender ATP**' yi seçin.  

1. Microsoft Defender Gelişmiş tehdit koruması panosunu gözden geçirin.  

    - **Windows Defender Aracısı dağıtım durumu**: etkin MICROSOFT Defender ATP ilkesi eklendi uygun yönetilen istemci bilgisayarlarının sayısı ve yüzdesi  

    - **Windows Defender atp Aracı durumu**: MICROSOFT Defender ATP Aracısı için durum bildiren bilgisayar istemcilerinin yüzdesi  

        - **Sağlıklı** -düzgün çalışıyor  

        - **Etkin** olmayan-zaman aralığı boyunca hizmete veri gönderilmez  

        - **Aracı durumu** -Windows 'ta aracının sistem hizmeti çalışmıyor  

        - **Not eklendi** -ilke uygulandı, ancak aracı ilke üzerinde yer bildirmedi  

## <a name="create-an-offboarding-configuration-file"></a>Çıkarma yapılandırma dosyası oluşturma  

1. [Microsoft Defender ATP çevrimiçi hizmetinde](https://securitycenter.windows.com/)oturum açın.

1. **Ayarlar**altında **makine yönetimi** ' ni seçin ve ardından **ekleme**' yi seçin.  

1. **Configuration Manager (geçerli dal) sürüm 1606** ' i seçin ve **uç nokta çıkarma**seçeneğini belirleyin.  

1. Sıkıştırılmış arşiv (. zip) dosyasını indirin ve içerikleri ayıklayın. Dosyaları çıkarma işlemi 30 gün boyunca geçerlidir.

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Endpoint Protection** > **Windows Defender ATP ilkeleri** ' ne gidin ve **Windows Defender ATP İlkesi Oluştur**' u seçin. Microsoft Defender ATP Ilkesi Sihirbazı açılır.  

1. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **çıkarma**seçeneğini belirleyin.

1. Kuruluşunuzun Microsoft Defender ATP bulut hizmeti kiracısı tarafından sunulan yapılandırma dosyasına **gidin** .

1. Özeti gözden geçirin ve Sihirbazı doldurun.  

İstemcilere Microsoft Defender ATP ilkesini hedeflemek için **Dağıt** ' ı seçin.  

> [!IMPORTANT]
> Microsoft Defender ATP yapılandırma dosyaları, güvenli tutulması gereken hassas bilgiler içerir.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Defender Gelişmiş Tehdit Koruması](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Microsoft Defender Gelişmiş tehdit koruması ekleme sorunlarını giderme](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
