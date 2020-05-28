---
title: Veri paylaşımını etkinleştirme
titleSuffix: Configuration Manager
description: Masaüstü analizi ile tanılama verilerini paylaşmaya yönelik bir başvuru kılavuzu.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0811c695acba4859bf32de535a28ea55cf8eee07
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268751"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Masaüstü analizi için veri paylaşımını etkinleştirme

Cihazları masaüstü analizine kaydetmek için Microsoft 'a Tanılama verileri gönderilmesi gerekir. Ortamınız bir ara sunucu kullanıyorsa, proxy 'yi yapılandırmaya yardımcı olması için bu bilgileri kullanın.

## <a name="diagnostic-data-levels"></a>Tanılama veri düzeyleri

![Masaüstü analizi için tanılama veri düzeyleri diyagramı](media/diagnostic-data-levels.png)

Configuration Manager masaüstü analizi ile tümleştirdiğinizde, cihazlarda tanılama veri düzeyini yönetmek için de kullanabilirsiniz. En iyi deneyim için Configuration Manager kullanın.

> [!Important]  
> Çoğu durumda bu ayarları yapılandırmak için yalnızca Configuration Manager kullanın. Bu ayarları etki alanı Grup İlkesi nesnelerinde da uygulamayın. Daha fazla bilgi için bkz. [çakışma çözümü](enroll-devices.md#conflict-resolution).

Masaüstü analizinin temel işlevselliği **temel** [Tanılama veri düzeyinde](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)çalışmaktadır. **Gelişmiş (sınırlı)** düzeyi Configuration Manager ' de yapılandırmazsanız, masaüstü analizinin aşağıdaki özelliklerini almazsınız:

- Uygulama kullanımı
- [Ek uygulama öngörüleri](compat-assessment.md#additional-insights)
- Dağıtım durumu verileri
- Sistem durumu izleme verileri

Microsoft, bundan elde edeceğiniz avantajları en üst düzeye çıkarmak için, **Gelişmiş (sınırlı)** tanılama veri düzeyini masaüstü analiziyle etkinleştirmenizi önerir.

> [!Tip]
> Configuration Manager **Gelişmiş (sınırlı)** ayarı, gelişmiş tanılama verilerini Windows 10, sürüm 1709 ve üstünü çalıştıran cihazlarda kullanılabilen **Windows Analytics ilkesi için gereken en düşük düzeyde sınırlayan** aynı ayardır.
>
> Windows 10, sürüm 1703 ve önceki sürümleri, Windows 8.1 veya Windows 7 çalıştıran cihazlarda Bu ilke ayarı yoktur. Configuration Manager ' de **Gelişmiş (sınırlı)** ayarı yapılandırdığınızda, bu cihazlar **temel** düzeye geri döner.
>
> Windows 10, sürüm 1709 çalıştıran cihazlarda Bu ilke ayarı vardır. Ancak, Configuration Manager ' de **Gelişmiş (sınırlı)** ayarı yapılandırdığınızda, bu cihazlar da **temel** düzeye geri döner.

**Gelişmiş (sınırlı)** ile Microsoft ile paylaşılan Tanılama verileri hakkında daha fazla bilgi için bkz. [Windows 10 gelişmiş tanılama verileri olayları ve alanları](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]
> Microsoft 'un gizliliğinizi denetim altına alan araçlar ve kaynakları sağlamaya yönelik güçlü bir taahhüt vardır. Sonuç olarak, masaüstü Analizi Windows 8.1 cihazları destekleirken, Microsoft, Avrupa ülkelerinde (EEA ve Isviçre) bulunan Windows 8.1 cihazlardan Windows Tanılama verileri toplamaz.

Daha fazla bilgi için bkz. [Masaüstü Analizi gizliliği](privacy.md).

Windows tanılama veri düzeylerini daha iyi anlamak için aşağıdaki makaleler de iyi kaynaklardır:

- [Windows 10 ve BT karar mekanizmaları için GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Gelişmiş tanılama verilerini sınırlamak üzere yapılandırılan istemciler, ilk tam taramada Microsoft bulutuna yaklaşık 2 MB veri gönderecek. Günlük Delta, günde 250-400 KB arasında değişir.
>
> Günlük Delta taraması 3:00 (cihaz yerel saati) saatinde gerçekleşir. Bazı olaylar, gün boyunca ilk kullanılabilir zamanda gönderilir. Bu süreler yapılandırılamaz.
>
> Daha fazla bilgi için bkz. [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Uç Noktalar

Veri paylaşımını etkinleştirmek için Proxy sunucunuzu aşağıdaki Internet uç noktalarına izin verecek şekilde yapılandırın.

> [!Important]  
> Gizlilik ve veri bütünlüğü için Windows, tanılama veri uç noktaları ile iletişim kurarken bir Microsoft SSL sertifikası (sertifika sabitleme) olup olmadığını denetler. SSL yakalamasyonu ve incelemesi mümkün değildir. Masaüstü analizlerini kullanmak için bu uç noktaları SSL incelemeden hariç tutun.<!-- BUG 4647542 -->

Sürüm 2002 ' den başlayarak, Configuration Manager site bir bulut hizmeti için gerekli uç noktalara bağlanamazsa, kritik bir durum ileti KIMLIĞI 11488 oluşturur. Hizmete bağlanamadığınızda SMS_SERVICE_CONNECTOR bileşen durumu kritik olarak değişir. Configuration Manager konsolunun [Bileşen durumu](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) düğümünde ayrıntılı durumu görüntüleyin.<!-- 5566763 -->

> [!NOTE]
> Microsoft IP adresi aralıkları hakkında daha fazla bilgi için bkz. [Microsoft genel IP alanı](https://www.microsoft.com/download/details.aspx?id=53602). Bu adresler düzenli olarak güncelleştirin. Hizmete göre ayrıntı düzeyi yoktur, bu aralıklardaki IP adresleri kullanılabilir.

### <a name="server-connectivity-endpoints"></a>Sunucu bağlantısı uç noktaları

Hizmet bağlantı noktasının aşağıdaki uç noktalarla iletişim kurması gerekir:

| Uç Nokta  | İşlev  |
|-----------|-----------|
| `https://aka.ms` | Hizmeti bulmak için kullanılır |
| `https://graph.windows.net` | Hiyerarşinizi masaüstü analizine (Configuration Manager sunucu rolünde) eklerken ticari kimlik gibi ayarları otomatik olarak almak için kullanılır. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Masaüstü analizi ile cihaz koleksiyonu üyeliklerini, dağıtım planlarını ve cihaz hazırlık durumunu eşitleme (yalnızca Configuration Manager sunucu rolü) için kullanılır. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Kullanıcı deneyimi ve tanılama bileşeni uç noktaları

İstemci cihazların aşağıdaki uç noktalarla iletişim kurması gerekir:

| Uç Nokta  | İşlev  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 10, sürüm 1809 veya sonraki sürümleri çalıştıran cihazlarda veya sürüm 1803 ' nin, 2018-09 toplu güncelleştirmesi veya sonraki sürümlerde yüklü olduğu cihazlar tarafından kullanılır. |
| `https://v10.events.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 10, sürüm 1803 çalıştıran cihazlar tarafından 2018-09 toplu güncelleştirmesi yüklü _olmadığında_ kullanılır. |
| `https://v10.vortex-win.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 10, sürüm 1709 veya önceki sürümleri çalıştıran cihazlar tarafından kullanılır. |
| `https://vortex-win.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 7 ve Windows 8.1 çalıştıran cihazlar tarafından kullanılır |

### <a name="client-connectivity-endpoints"></a>İstemci bağlantı uç noktaları

İstemci cihazların aşağıdaki uç noktalarla iletişim kurması gerekir:

| Dizin oluşturma | Uç Nokta  | İşlev  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Uyumluluk güncelleştirmesinin Microsoft 'a veri göndermesini sağlar. |
| 2 | `http://adl.windows.com` | Uyumluluk güncelleştirmesinin Microsoft 'un en son uyumluluk verilerini almasına izin verir. |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1803 veya önceki sürümlerde dağıtım sistem durumunu izlemek için gereklidir. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde cihaz sistem durumu raporları için gereklidir. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows hata bildirimi (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Çevrimiçi Kilitlenme Analizi (Oca)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Windows 10, sürüm 1809 veya sonraki sürümlerde cihaz sistem durumu raporları için gereklidir. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Çevrimiçi Kilitlenme Analizi (Oca)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Windows 10, sürüm 1803 veya önceki sürümlerde dağıtım sistem durumunu izlemek için gereklidir. |
| 13 | `https://login.live.com` | Masaüstü analizi için daha güvenilir bir cihaz kimliği sağlamak için gereklidir. <br> <br>Son Kullanıcı Microsoft hesabı erişimini devre dışı bırakmak için, bu uç noktayı engellemek yerine ilke ayarlarını kullanın. Daha fazla bilgi için bkz. [enterprise Microsoft hesabı](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. |

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
> Kullanıcı proxy kimlik doğrulama yaklaşımı, Microsoft Defender Gelişmiş tehdit koruması kullanımıyla uyumlu değildir. Bu davranış, bu kimlik doğrulamanın **Disableenterpriseauthproxy** kayıt defteri anahtarını olarak ayarlanmış olması `0` , Microsoft Defender ATP 'nin olarak ayarlanmasını gerektirmesidir `1` . Daha fazla bilgi için bkz. [Microsoft Defender ATP 'de makine proxy ve internet bağlantısı ayarlarını yapılandırma](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Cihaz proxy kimlik doğrulaması

Bu yaklaşım aşağıdaki senaryoları destekler:

- Kullanıcının oturum açtığı veya cihazın kullanıcılarının internet erişimi olmayan, gözetimsiz cihazlar

- Windows tümleşik kimlik doğrulaması kullanmayan kimliği doğrulanmış proxy 'ler

- Microsoft Defender Gelişmiş tehdit koruması 'nı da kullanıyorsanız

Bu yaklaşım en karmaşıktır çünkü aşağıdaki yapılandırmalarda gereklidir:

- Cihazların yerel sistem bağlamında WinHTTP aracılığıyla proxy sunucusuna ulaşabildiğinizden emin olun. Bu davranışı yapılandırmak için aşağıdaki seçeneklerden birini kullanın:

  - Komut satırı`netsh winhttp set proxy`

  - Web proxy otomatik bulma (WPAD) protokolü

  - Saydam proxy

  - Aşağıdaki Grup İlkesi ayarını kullanarak cihaz genelinde Winınet proxy yapılandırın: **makine başına proxy ayarları yap (Kullanıcı başına değil)** (proxysettingsperuser = `1` )

  - Yönlendirilmiş bağlantı veya ağ adresi çevirisi (NAT) kullanan

- Proxy sunucularını, Active Directory ' deki bilgisayar hesaplarının tanılama veri uç noktalarına erişmesine izin verecek şekilde yapılandırın. Bu yapılandırma, proxy sunucularının Windows tümleşik kimlik doğrulamasını desteklemesini gerektirir.  
