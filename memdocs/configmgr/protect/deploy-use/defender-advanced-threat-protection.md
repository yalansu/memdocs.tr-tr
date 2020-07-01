---
title: Microsoft Defender Gelişmiş Tehdit Koruması
titleSuffix: Configuration Manager
description: Kuruluşların gelişmiş saldırılara yanıt vermesini sağlayan yeni bir hizmet olan Microsoft Defender Gelişmiş tehdit koruması 'nı yönetmeyi ve izlemeyi öğrenin.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613503"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Gelişmiş Tehdit Koruması

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Endpoint Protection, [Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) yönetmenize ve izlemenize yardımcı olabilir (eski adıyla WINDOWS Defender ATP olarak bilinir). Microsoft Defender ATP, kuruluşların ağlarında gelişmiş saldırıları algılamasına, araştırmasına ve yanıt vermesine yardımcı olur. Configuration Manager ilkeleri Windows 10 istemcilerini eklemenize ve izlemenize yardımcı olabilir.

Microsoft Defender ATP, Microsoft [Defender Güvenlik Merkezi](https://securitycenter.windows.com)'ndeki bir hizmettir. İstemci ekleme yapılandırma dosyası ekleyerek ve dağıtarak, Configuration Manager dağıtım durumunu ve Microsoft Defender ATP Aracısı sistem durumunu izleyebilir. Microsoft Defender ATP, Configuration Manager istemcisini çalıştıran veya [Microsoft Intune tarafından yönetilen](https://docs.microsoft.com/intune/protect/advanced-threat-protection)bilgisayarlarda desteklenir.

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
Configuration Manager sürüm 2002 ' den başlayarak, aşağıdaki işletim sistemlerini ekleyebilirsiniz:

- Windows 8.1
- Windows 10, sürüm 1607 veya üzeri
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, sürüm 1803 veya üzeri
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Configuration Manager ile ATP 'ye ekleme hakkında

Farklı işletim sistemlerinde ATP 'ye ekleme için farklı gereksinimler vardır. Windows 8.1 ve diğer alt düzey işletim sistemi cihazlarında, eklenecek **çalışma alanı anahtarı** ve **çalışma alanı kimliği** gerekir. Windows Server sürüm 1803 gibi yukarı düzey cihazların ekleme yapılandırma dosyasına ihtiyacı vardır. Configuration Manager ayrıca, eklendi cihazları için gerektiğinde Microsoft Monitoring Agent (MMA), ancak aracıyı otomatik olarak güncelleştirmez.

Yukarı düzey işletim sistemleri şunları içerir:
- Windows 10, sürüm 1607 ve üzeri
- Windows Server 2016, sürüm 1803 veya üzeri
- Windows Server 2019

Alt düzey işletim sistemleri şunları içerir:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, sürüm 1709 ve önceki sürümleri

Configuration Manager ile ATP 'ye cihaz eklediğinizde, ATP ilkesini bir hedef koleksiyona veya birden çok koleksiyona dağıtırsınız. Bazen hedef koleksiyon, desteklenen herhangi bir sayıda işletim sistemini çalıştıran cihazları içerir. Bu cihazları eklemeye yönelik yönergeler, yukarı düzey, alt düzey veya her ikisi de olan işletim sistemlerine sahip cihazları içeren bir koleksiyonu hedefliyorsanız temel alınarak değişir.

- Hedef koleksiyonunuz hem yukarı düzey hem de alt düzey cihazlar içeriyorsa, [desteklenen herhangi bir işletim sistemini çalıştıran cihazları](#bkmk_any_os) eklemek için yönergeleri kullanın (önerilir).
- Koleksiyonunuz yalnızca yukarı düzey cihazlar içeriyorsa, [en yüksek düzey ekleme yönergelerini](#bkmk_uplevel)kullanabilirsiniz.
- Koleksiyonunuz yalnızca alt düzey cihazlar içeriyorsa, [alt düzey ekleme yönergelerini](#bkmk_downlevel)kullanabilirsiniz.

> [!Warning]
> - Hedef koleksiyonunuz yukarı düzey cihazlar içeriyorsa ve alt düzey cihazlar için yönergeleri kullanırsanız, yukarı düzey cihazlar eklendi olmayacaktır.
> - Hedef koleksiyonunuz alt düzey cihazlar içeriyorsa ve yukarı düzey cihazlar için yönergeleri kullanırsanız, alt düzey cihazlar eklendi olmayacaktır.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a>Desteklenen işletim sistemlerini ATP 'ye içeren cihazları ekleme (önerilir)
 Configuration Manager için yapılandırma dosyasını, **çalışma alanı anahtarını**ve **çalışma alanı kimliğini** sağlayarak, [desteklenen işletim SISTEMLERINDEN](#bkmk_os) herhangi birini çalıştıran cihazları ATP 'ye ekleyebilirsiniz.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Yapılandırma dosyasını, çalışma alanı KIMLIĞINI ve çalışma alanı anahtarını al

1. [Microsoft Defender ATP çevrimiçi hizmetine](https://securitycenter.windows.com/) gidin ve oturum açın.
1. **Ayarlar**' ı seçin ve ardından **cihaz yönetimi** başlığı altında **ekleme** ' yi seçin.
1. İşletim sistemi için **Windows 10**' u seçin.
1. Dağıtım yöntemi için **geçerli dalı Configuration Manager ve daha sonra Microsoft uç noktası '** nı seçin.
1. **Paketi indir**' e tıklayın.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Yapılandırma dosyası indirmeyi ekleme" lightbox="media/5229962-onboarding-configuration.png":::
1. Sıkıştırılmış arşiv (. zip) dosyasını indirin ve içerikleri ayıklayın.
1. **Ayarlar**' ı seçin ve ardından **cihaz yönetimi** başlığı altında **ekleme** ' yi seçin.
1. İşletim sistemi için, listeden **Windows 7 SP1 ve 8,1** ya da **Windows Server 2008 r2 SP1, 2012 R2 ve 2016 '** i seçin.
   - **Çalışma alanı anahtarı** ve **çalışma alanı kimliği** , seçtiğiniz seçeneklerden bağımsız olarak aynı olacaktır.
1. **Bağlantı yapılandırma** bölümünden **çalışma alanı anahtarı** ve **çalışma alanı kimliği** değerlerini kopyalayın.

   > [!IMPORTANT]
   > Microsoft Defender ATP yapılandırma dosyası, güvenli tutulması gereken hassas bilgiler içerir.


### <a name="onboard-the-devices"></a>Cihazları ekleme

1. Configuration Manager konsolunda, **Assets and Compliance**  >  **Endpoint Protection**  >  **Microsoft Defender ATP ilkeleri**Endpoint Protection varlıklar ve uyum ' a gidin.
1. Microsoft Defender ATP Ilke Sihirbazı 'nı açmak için **Microsoft Defender ATP Ilkesi oluştur** ' u seçin. 
1. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **ekleme**' yi seçin.
1. İndirilen. zip dosyasından ayıkladığınız yapılandırma dosyasına **gidin** .
1. **Çalışma alanı anahtarını** ve **çalışma alanı kimliğini** girip **İleri**' ye tıklayın.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Microsoft Defender ATP Ilkesi oluşturma Sihirbazı" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Analiz edilmek üzere yönetilen cihazlardan toplanan ve paylaşılan dosya örneklerini belirtin.  
   - **Yok**
   - **Tüm dosya türleri**  
1. Özeti gözden geçirin ve Sihirbazı doldurun.  
1. Oluşturduğunuz ilkeye sağ tıkladıktan sonra, Microsoft Defender ATP ilkesini istemcilere hedeflemek için **Dağıt** ' ı seçin.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a>En yüksek düzeyde işletim sistemlerini ATP 'ye çalıştıran cihazlar ekleme

Yukarı düzey istemciler ATP 'ye ekleme için bir ekleme yapılandırma dosyası gerektirir. Yukarı düzey işletim sistemleri şunları içerir:
- Windows 10, sürüm 1607 ve üzeri 
- Windows Server 2016, sürüm 1803 ve üzeri
- Windows Server 2019

Hedef koleksiyonunuz hem yukarı düzey hem de alt düzey cihazlar içeriyorsa veya emin değilseniz, [desteklenen herhangi bir işletim sistemini çalıştıran cihazları](#bkmk_any_os)eklemek için yönergeleri kullanın (önerilir).

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Yukarı düzey cihazlar için bir ekleme yapılandırma dosyası alın

1. [Microsoft Defender ATP çevrimiçi hizmetine](https://securitycenter.windows.com/) gidin ve oturum açın.
1. **Ayarlar**' ı seçin ve ardından **cihaz yönetimi** başlığı altında **ekleme** ' yi seçin.
1. İşletim sistemi için **Windows 10**' u seçin.
1. Dağıtım yöntemi için **geçerli dalı Configuration Manager ve daha sonra Microsoft uç noktası '** nı seçin.
1. **Paketi indir**' e tıklayın.
1. Sıkıştırılmış arşiv (. zip) dosyasını indirin ve içerikleri ayıklayın.

> [!IMPORTANT]
> Microsoft Defender ATP yapılandırma dosyası, güvenli tutulması gereken hassas bilgiler içerir.


### <a name="onboard-the-up-level-devices"></a>Yukarı düzey cihazları ekleme

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**  >  **Endpoint Protection**  >  **Microsoft Defender ATP ilkeleri** ' ne gidin ve **Microsoft Defender ATP İlkesi Oluştur**' u seçin. Microsoft Defender ATP Ilkesi Sihirbazı açılır.  
1. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **ekleme**' yi seçin.
1. İndirilen. zip dosyasından ayıkladığınız yapılandırma dosyasına **gidin** .
   > [!Note]
   > Configuration Manager sürüm 2002 için, yalnızca yukarı düzey cihazlar ekleme olsanız bile **çalışma alanı anahtarı** ve **çalışma alanı kimliği** gerekir. **Settings**  >  **Onboarding**  >  [Microsoft Defender ATP çevrimiçi hizmeti](https://securitycenter.windows.com/)'nden**Windows 7 ve 8,1** ekleme ayarları ' nı seçerek bu değerleri alın. <!--7054188-->
1. Analiz edilmek üzere yönetilen cihazlardan toplanan ve paylaşılan dosya örneklerini belirtin.  
   - **Yok**
   - **Tüm dosya türleri**  
1. Özeti gözden geçirin ve Sihirbazı doldurun.  
1. Oluşturduğunuz ilkeye sağ tıkladıktan sonra, Microsoft Defender ATP ilkesini istemcilere hedeflemek için **Dağıt** ' ı seçin.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a>Alt düzey işletim sistemlerini ATP 'ye çalıştıran cihazlar ekleme

Alt düzey istemciler, ATP ekleme için **çalışma alanı anahtarı** ve **çalışma alanı kimliği** gerektirir. Alt düzey işletim sistemleri şunları içerir:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, sürüm 1709 ve önceki sürümleri

Hedef koleksiyonunuz hem yukarı düzey hem de alt düzey cihazlar içeriyorsa veya emin değilseniz, [desteklenen herhangi bir işletim sistemini çalıştıran cihazları](#bkmk_any_os)eklemek için yönergeleri kullanın (önerilir).

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>Alt düzey cihazlar için çalışma alanı KIMLIĞI ve çalışma alanı anahtarı al

1. [Microsoft Defender ATP çevrimiçi hizmetine](https://securitycenter.windows.com/) gidin ve oturum açın.
1. **Ayarlar**' ı seçin ve ardından **cihaz yönetimi** başlığı altında **ekleme** ' yi seçin.
1. İşletim sistemi için, listeden **Windows 7 SP1 ve 8,1** ya da **Windows Server 2008 r2 SP1, 2012 R2 ve 2016 '** i seçin.
   - **Çalışma alanı anahtarı** ve **çalışma alanı kimliği** , seçtiğiniz seçeneklerden bağımsız olarak aynı olacaktır.
1. **Bağlantı yapılandırma** bölümünden **çalışma alanı anahtarı** ve **çalışma alanı kimliği** değerlerini kopyalayın.

### <a name="onboard-the-down-level-devices"></a>Alt düzey cihazları ekleme

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**  >  **Endpoint Protection**  >  **Microsoft Defender ATP ilkeleri** ' ne gidin ve **Microsoft Defender ATP İlkesi Oluştur**' u seçin. Microsoft Defender ATP Ilkesi Sihirbazı açılır.  
1. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **ekleme**' yi seçin.
1. **Çalışma alanı anahtarını** ve **çalışma alanı kimliğini**sağlayın.
   > [!Note]
   > - Configuration Manager sürüm 2002 için, yalnızca alt düzey cihazları ekleme olsanız bile yapılandırma dosyası gerekir. **Settings**  >  **Onboarding**  >  [Microsoft Defender ATP çevrimiçi hizmeti](https://securitycenter.windows.com/)'nden**Windows 10** ' un eklenmesi seçeneklerini belirleyerek bu değerleri alın. <!--7054188--> 
   > - Microsoft Defender ATP yapılandırma dosyası, güvenli tutulması gereken hassas bilgiler içerir.
1. Analiz edilmek üzere yönetilen cihazlardan toplanan ve paylaşılan dosya örneklerini belirtin.  
   - **Yok**
   - **Tüm dosya türleri**  
1. Özeti gözden geçirin ve Sihirbazı doldurun.  
1. Oluşturduğunuz ilkeye sağ tıkladıktan sonra, Microsoft Defender ATP ilkesini istemcilere hedeflemek için **Dağıt** ' ı seçin.


## <a name="monitor"></a>İzleme

1. Configuration Manager konsolunda **izleme**  >  **güvenliği** ' ne gidin ve ardından **Microsoft Defender ATP**' yi seçin.  

1. Microsoft Defender Gelişmiş tehdit koruması panosunu gözden geçirin.  

    - **Microsoft Defender ATP Aracısı Ekleme durumu**: etkin MICROSOFT Defender ATP ilkesi eklendi uygun yönetilen istemci bilgisayarlarının sayısı ve yüzdesi  

    - **Microsoft Defender atp Aracı durumu**: MICROSOFT Defender ATP Aracısı için durum bildiren bilgisayar istemcilerinin yüzdesi  

        - **Sağlıklı** -düzgün çalışıyor  

        - **Etkin** olmayan-zaman aralığı boyunca hizmete veri gönderilmez  

        - **Aracı durumu** -Windows 'ta aracının sistem hizmeti çalışmıyor  

        - **Not eklendi** -ilke uygulandı, ancak aracı ilke üzerinde yer bildirmedi  

## <a name="create-an-offboarding-configuration-file"></a>Çıkarma yapılandırma dosyası oluşturma  

1. [Microsoft Defender ATP çevrimiçi hizmetinde](https://securitycenter.windows.com/)oturum açın.
1. **Ayarlar**' ı seçin ve ardından **cihaz yönetimi** başlığı altında **çıkarma** ' yı seçin.
1. İşletim sistemi için **Windows 10** ' u ve ardından dağıtım yöntemi için **geçerli dalı Configuration Manager Microsoft uç noktası** ' nı seçin.
   - **Windows 10** seçeneğinin kullanılması koleksiyondaki tüm cihazların offboarded olmasını sağlar ve gerektiğinde MMA kaldırılır.
1. Sıkıştırılmış arşiv (. zip) dosyasını indirin ve içerikleri ayıklayın. Dosyaları çıkarma işlemi 30 gün boyunca geçerlidir.

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**  >  **Endpoint Protection**  >  **Microsoft Defender ATP ilkeleri** ' ne gidin ve **Microsoft Defender ATP İlkesi Oluştur**' u seçin. Microsoft Defender ATP Ilkesi Sihirbazı açılır.  

1. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **çıkarma**seçeneğini belirleyin.

1. İndirilen. zip dosyasından ayıkladığınız yapılandırma dosyasına **gidin** .

1. Özeti gözden geçirin ve Sihirbazı doldurun.  

İstemcilere Microsoft Defender ATP ilkesini hedeflemek için **Dağıt** ' ı seçin.  

> [!IMPORTANT]
> Microsoft Defender ATP yapılandırma dosyaları, güvenli tutulması gereken hassas bilgiler içerir.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Defender Gelişmiş Tehdit Koruması](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Microsoft Defender Gelişmiş tehdit koruması ekleme sorunlarını giderme](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
