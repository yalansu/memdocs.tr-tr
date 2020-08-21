---
title: Veri paylaşımını etkinleştirme
titleSuffix: Configuration Manager
description: Masaüstü analizi ile tanılama verilerini paylaşmaya yönelik bir başvuru kılavuzu.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 999d8441e8c97f0a4b7ad4a92c8175300dcc4ead
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696455"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Masaüstü analizi için veri paylaşımını etkinleştirme

Cihazları masaüstü analizine kaydetmek için Microsoft 'a Tanılama verileri gönderilmesi gerekir. Ortamınız bir ara sunucu kullanıyorsa, proxy 'yi yapılandırmaya yardımcı olması için bu bilgileri kullanın.

## <a name="diagnostic-data-levels"></a>Tanılama veri düzeyleri

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Masaüstü analizi için tanılama veri düzeyleri diyagramı":::

Configuration Manager masaüstü analizi ile tümleştirdiğinizde, cihazlarda tanılama veri düzeyini yönetmek için de kullanabilirsiniz. En iyi deneyim için Configuration Manager kullanın.

> [!IMPORTANT]
> Çoğu durumda bu ayarları yapılandırmak için yalnızca Configuration Manager kullanın. Bu ayarları etki alanı Grup İlkesi nesnelerinde da uygulamayın. Daha fazla bilgi için bkz. [çakışma çözümü](enroll-devices.md#conflict-resolution).

Masaüstü analizinin temel işlevselliği, **gerekli** [Tanılama veri düzeyinde](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)çalışmaktadır. Configuration Manager 'de **Isteğe bağlı (sınırlı)** düzeyi yapılandırmazsanız, masaüstü analizinin aşağıdaki özelliklerini almazsınız:

- Uygulama kullanımı
- [Ek uygulama öngörüleri](compat-assessment.md#additional-insights)
- [Dağıtım durumu verileri](deploy-prod.md#address-deployment-alerts)
- [Sistem durumu izleme verileri](health-status-monitoring.md)

Microsoft, sizin alacağınız avantajları en üst düzeye çıkarmak için, **Isteğe bağlı (sınırlı)** tanılama veri düzeyini masaüstü analiziyle etkinleştirmenizi önerir.

> [!TIP]
> Configuration Manager **Isteğe bağlı (sınırlı)** ayarı, gelişmiş tanılama verilerini Windows 10, sürüm 1709 ve üstünü çalıştıran cihazlarda bulunan **Windows Analytics ilkesi için gereken en düşük düzeyde sınırlandırarak** aynı ayardır.
>
> Windows 10, sürüm 1703 ve önceki sürümleri, Windows 8.1 veya Windows 7 çalıştıran cihazlarda Bu ilke ayarı yoktur. Configuration Manager 'de **Isteğe bağlı (sınırlı)** ayarı yapılandırdığınızda, bu cihazlar **gerekli** düzeye geri döner.
>
> Windows 10, sürüm 1709 çalıştıran cihazlarda Bu ilke ayarı vardır. Ancak, Configuration Manager ' de **Isteğe bağlı (sınırlı)** ayarı yapılandırdığınızda, bu cihazlar da **gerekli** düzeye geri döner.
>
> Configuration Manager sürüm 2002 ve önceki sürümlerde, ayarlarda farklı adlar vardı:<!-- 7363467 -->
>
> | Sürüm 2006 ve üzeri | Sürüm 2002 ve öncesi |
> |---------|---------|
> | Gerekli | Temel |
> | İsteğe bağlı (sınırlı) | Gelişmiş (sınırlı) |
> | N/A | Gelişmiş |
> | İsteğe Bağlı | Tam |
>
> Daha önce **Gelişmiş** düzeyde herhangi bir cihaz yapılandırdıysanız, sürüm 2006 ' e yükselttiğinizde bu kullanıcılar **isteğe bağlı (sınırlı)** olarak döndürülür. Böylece daha az veri Microsoft 'a gönderilir. Bu değişiklik, masaüstü analizinden gördüklerinizi etkilemez.

**Isteğe bağlı (sınırlı)** ile Microsoft ile paylaşılan Tanılama verileri hakkında daha fazla bilgi için bkz. [Windows 10 gelişmiş tanılama verileri olayları ve alanları](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Microsoft 'un gizliliğinizi denetim altına alan araçlar ve kaynakları sağlamaya yönelik güçlü bir taahhüt vardır. Sonuç olarak, masaüstü Analizi Windows 8.1 cihazları destekleirken, Microsoft, Avrupa ülkelerinde (EEA ve Isviçre) bulunan Windows 8.1 cihazlardan Windows Tanılama verileri toplamaz.

Daha fazla bilgi için bkz. [Masaüstü Analizi gizliliği](privacy.md).

Windows tanılama veri düzeylerini daha iyi anlamak için aşağıdaki makaleler de iyi kaynaklardır:

- [Windows 10 ve BT karar mekanizmaları için GDPR](/windows/privacy/gdpr-it-guidance)  

- [Kuruluşunuzda Windows tanılama verilerini yapılandırma](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> **Isteğe bağlı (sınırlı)** Tanılama verileri gönderecek şekilde yapılandırılan istemciler, ilk tam taramada Microsoft bulutuna YAKLAŞıK 2 MB veri gönderecek. Günlük Delta, günde 250-400 KB arasında değişir.
>
> Günlük Delta taraması 3:00 (cihaz yerel saati) saatinde gerçekleşir. Bazı olaylar, gün boyunca ilk kullanılabilir zamanda gönderilir. Bu süreler yapılandırılamaz.
>
> Daha fazla bilgi için bkz. [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Uç Noktalar

Veri paylaşımını etkinleştirmek için Proxy sunucunuzu aşağıdaki Internet uç noktalarına izin verecek şekilde yapılandırın.

> [!IMPORTANT]
> Gizlilik ve veri bütünlüğü için Windows, tanılama veri uç noktaları ile iletişim kurarken bir Microsoft SSL sertifikası (sertifika sabitleme) olup olmadığını denetler. SSL yakalamasyonu ve incelemesi mümkün değildir. Masaüstü analizlerini kullanmak için bu uç noktaları SSL incelemeden hariç tutun.<!-- BUG 4647542 -->

Sürüm 2002 ' den başlayarak, Configuration Manager site bir bulut hizmeti için gerekli uç noktalara bağlanamazsa, kritik bir durum ileti KIMLIĞI 11488 oluşturur. Hizmete bağlanamadığınızda SMS_SERVICE_CONNECTOR bileşen durumu kritik olarak değişir. Configuration Manager konsolunun [Bileşen durumu](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) düğümünde ayrıntılı durumu görüntüleyin.<!-- 5566763 -->

> [!NOTE]
> Microsoft IP adresi aralıkları hakkında daha fazla bilgi için bkz. [Microsoft genel IP alanı](https://www.microsoft.com/download/details.aspx?id=53602). Bu adresler düzenli olarak güncelleştirin. Hizmete göre ayrıntı düzeyi yoktur, bu aralıklardaki IP adresleri kullanılabilir.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

## <a name="proxy-server-authentication"></a>Proxy sunucusu kimlik doğrulaması

Kuruluşunuz internet erişimi için proxy sunucu kimlik doğrulamasını kullanıyorsa, kimlik doğrulaması nedeniyle tanılama verilerini engellemediğinden emin olun. Proxy 'niz cihazların bu verileri göndermesini izin vermezse, masaüstü Analizi 'nde gösterilmez.

### <a name="bypass-recommended"></a>Atla (önerilir)

Proxy sunucularınızı tanılama veri uç noktalarına giden trafik için proxy kimlik doğrulaması gerektirecek şekilde yapılandırın. Bu seçenek en kapsamlı çözümdür. Tüm Windows 10 sürümleri için geçerlidir.  

### <a name="user-proxy-authentication"></a>Kullanıcı proxy kimlik doğrulaması

Cihazları, oturum açmış kullanıcının proxy kimlik doğrulaması bağlamını kullanacak şekilde yapılandırın. Bu yöntem aşağıdaki konfigürasyonları gerektirir:

- Cihazların desteklenen bir Windows sürümü için geçerli kalite güncelleştirmesi var

- Windows ayarları 'nın Internet & ağ **Ara sunucu ayarları** 'nda Kullanıcı düzeyi proxy 'Yi (Winınet proxy) yapılandırın. Eski Internet seçenekleri denetim masasını da kullanabilirsiniz.

- Kullanıcıların tanılama veri uç noktalarına erişmek için proxy iznine sahip olduğundan emin olun. Bu seçenek, cihazların proxy izinlerine sahip konsol kullanıcılarına sahip olmasını gerektirir, bu nedenle bu yöntemi gözetimsiz cihazlarla kullanamazsınız.

> [!IMPORTANT]
> Kullanıcı proxy kimlik doğrulama yaklaşımı, Microsoft Defender Gelişmiş tehdit koruması kullanımıyla uyumlu değildir. Bu davranış, bu kimlik doğrulamanın **Disableenterpriseauthproxy** kayıt defteri anahtarını olarak ayarlanmış olması `0` , Microsoft Defender ATP 'nin olarak ayarlanmasını gerektirmesidir `1` . Daha fazla bilgi için bkz. [Microsoft Defender ATP 'de makine proxy ve internet bağlantısı ayarlarını yapılandırma](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Cihaz proxy kimlik doğrulaması

Bu yaklaşım aşağıdaki senaryoları destekler:

- Kullanıcının oturum açtığı veya cihazın kullanıcılarının internet erişimi olmayan, gözetimsiz cihazlar

- Windows tümleşik kimlik doğrulaması kullanmayan kimliği doğrulanmış proxy 'ler

- Microsoft Defender Gelişmiş tehdit koruması 'nı da kullanıyorsanız

Bu yaklaşım en karmaşıktır çünkü aşağıdaki yapılandırmalarda gereklidir:

- Cihazların yerel sistem bağlamında WinHTTP aracılığıyla proxy sunucusuna ulaşabildiğinizden emin olun. Bu davranışı yapılandırmak için aşağıdaki seçeneklerden birini kullanın:

  - Komut satırı `netsh winhttp set proxy`

  - Web proxy otomatik bulma (WPAD) protokolü

  - Saydam proxy

  - Aşağıdaki Grup İlkesi ayarını kullanarak cihaz genelinde Winınet proxy yapılandırın: **makine başına proxy ayarları yap (Kullanıcı başına değil)** (proxysettingsperuser = `1` )

  - Yönlendirilmiş bağlantı veya ağ adresi çevirisi (NAT) kullanan

- Proxy sunucularını, Active Directory ' deki bilgisayar hesaplarının tanılama veri uç noktalarına erişmesine izin verecek şekilde yapılandırın. Bu yapılandırma, proxy sunucularının Windows tümleşik kimlik doğrulamasını desteklemesini gerektirir.