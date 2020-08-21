---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 2ae953f6fb01f42c8140407c551ddeb3a9f39c70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692697"
---
### <a name="server-connectivity-endpoints"></a>Sunucu bağlantısı uç noktaları

Hizmet bağlantı noktasının aşağıdaki uç noktalarla iletişim kurması gerekir:

| Uç Noktası  | İşlev  |
|-----------|-----------|
| `https://aka.ms` | Hizmeti bulmak için kullanılır |
| `https://graph.windows.net` | Hiyerarşinizi masaüstü analizine (Configuration Manager sunucu rolünde) eklerken ticari kimlik gibi ayarları otomatik olarak almak için kullanılır. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Masaüstü analizi ile cihaz koleksiyonu üyeliklerini, dağıtım planlarını ve cihaz hazırlık durumunu eşitleme (yalnızca Configuration Manager sunucu rolü) için kullanılır. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | Şirket içi hizmet bağlayıcısından gelen Tanılama verileri için, buluta bağlı hizmetlerin sistem durumu hakkında öngörüler elde edin.<!--7541816--> |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Kullanıcı deneyimi ve tanılama bileşeni uç noktaları

İstemci cihazların aşağıdaki uç noktalarla iletişim kurması gerekir:

| Uç Noktası  | İşlev  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 10, sürüm 1809 veya sonraki sürümleri çalıştıran cihazlarda veya sürüm 1803 ' nin, 2018-09 toplu güncelleştirmesi veya sonraki sürümlerde yüklü olduğu cihazlar tarafından kullanılır. |
| `https://v10.events.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 10, sürüm 1803 çalıştıran cihazlar tarafından 2018-09 toplu güncelleştirmesi yüklü _olmadığında_ kullanılır. |
| `https://v10.vortex-win.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 10, sürüm 1709 veya önceki sürümleri çalıştıran cihazlar tarafından kullanılır. |
| `https://vortex-win.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. Windows 7 ve Windows 8.1 çalıştıran cihazlar tarafından kullanılır |

### <a name="client-connectivity-endpoints"></a>İstemci bağlantı uç noktaları

İstemci cihazların aşağıdaki uç noktalarla iletişim kurması gerekir:

| Dizin oluşturma | Uç Noktası  | İşlev  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Uyumluluk güncelleştirmesinin Microsoft 'a veri göndermesini sağlar. |
| 2 | `http://adl.windows.com` | Uyumluluk güncelleştirmesinin Microsoft 'un en son uyumluluk verilerini almasına izin verir. |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1803 veya önceki sürümlerde dağıtım sistem durumunu izlemek için gereklidir. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde cihaz sistem durumu raporları için gereklidir. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows hata bildirimi (WER)](/windows/win32/wer/windows-error-reporting). Windows 10, sürüm 1809 veya sonraki sürümlerde dağıtım durumunu izlemek için gereklidir. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Çevrimiçi Kilitlenme Analizi (Oca)](/windows/win32/dxtecharts/crash-dump-analysis). Windows 10, sürüm 1809 veya sonraki sürümlerde cihaz sistem durumu raporları için gereklidir. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Çevrimiçi Kilitlenme Analizi (Oca)](/windows/win32/dxtecharts/crash-dump-analysis). Windows 10, sürüm 1803 veya önceki sürümlerde dağıtım sistem durumunu izlemek için gereklidir. |
| 13 | `https://login.live.com` | Masaüstü analizi için daha güvenilir bir cihaz kimliği sağlamak için gereklidir. <br> <br>Son Kullanıcı Microsoft hesabı erişimini devre dışı bırakmak için, bu uç noktayı engellemek yerine ilke ayarlarını kullanın. Daha fazla bilgi için bkz. [enterprise Microsoft hesabı](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Bağlı kullanıcı deneyimi ve tanılama bileşeni uç noktası. |