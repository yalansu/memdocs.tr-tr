---
title: Bağlı önbellek sorunlarını giderme
titleSuffix: Configuration Manager
description: Sorunları gidermenize yardımcı olmak üzere Microsoft bağlı önbelleği için teknik ayrıntılar.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a8c975798c506339a981e8648003387dc1e9838
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878110"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Configuration Manager 'de Microsoft bağlı önbelleği sorunlarını giderme

Bu makalede, Configuration Manager 'de Microsoft bağlı önbelleği hakkında teknik ayrıntılar sağlanmaktadır. Ortamınızda bulunan sorunları gidermeye yardımcı olması için bu uygulamayı kullanın. Nasıl çalıştığı ve nasıl kullanılacağı hakkında daha fazla bilgi için, bkz. [Microsoft bağlı önbelleği Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> Sürüm 1910 ' den başlayarak, bu özellik artık **Microsoft bağlı önbelleği**olarak adlandırılmaktadır. Daha önce teslim Iyileştirmesi-ağ önbelleği olarak bilinirdi.

## <a name="verify"></a>Doğrulama

Teslim Iyileştirme önbellek sunucusunu doğru şekilde yüklediğinizde ve istemcileri doğru şekilde yapılandırdığınızda, internet yerine dağıtım noktanmda yüklü olan önbellek sunucusundan indirirler.

Bu davranışı [bir istemcide](#bkmk_verify-client) veya [sunucuda](#bkmk_verify-server)doğrulayın.

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a>İstemci üzerinde doğrulama

1. Windows 10, sürüm 1809 veya sonraki sürümleri çalıştıran istemcide, bulutta yönetilen içeriği indirin. Bağlı önbelleğin desteklediği içerik türleri hakkında daha fazla bilgi için bkz. [bağlı önbelleği doğrulama](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. PowerShell 'i açın ve aşağıdaki komutu çalıştırın:`Get-DeliveryOptimizationStatus`

Örneğin:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Özniteliğin sıfır olmadığına dikkat edin `BytesFromCacheServer` .

İstemci doğru yapılandırılmamışsa veya önbellek sunucusu doğru şekilde yüklenmemişse, teslim Iyileştirme istemcisi özgün bulut kaynağına geri döner. Sonra BytesFromCacheServer özniteliği sıfır olur.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a>Sunucuda doğrulama

İlk olarak, kayıt defteri özelliklerinin doğru şekilde yapılandırıldığını doğrulayın: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache` . Örneğin, sürücü önbelleği konumu, burada gibi `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294` `PrimaryDrivesInput` birden çok sürücü olabilir `C,D,E` .

Ardından, zorunlu üstbilgiler ile sunucuya bir istemci indirme isteğinin benzetimini yapmak için aşağıdaki yöntemi kullanın.

1. Yönetici olarak 64 bitlik bir PowerShell penceresi açın.
2. Aşağıdaki komutu çalıştırın ve sunucunuzun adını veya IP adresini değiştirin `<DoincServer>` :

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

Çıktı aşağıdaki örneğe benzer şekilde görünür:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Aşağıdaki öznitelikler başarıyı gösterir:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Günlük dosyaları

- ARR kurulum günlüğü:`%temp%\arr_setup.log`

- Önbellek sunucusu kurulum günlüğü: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` dağıtım noktasında ve `DistMgr.log` site sunucusunda

- IIS işletimsel Günlükler: varsayılan olarak,`%SystemDrive%\inetpub\logs\LogFiles`

- Önbellek sunucusu işletimsel günlüğünü yap:`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Diğer kullanımlar arasında bu günlük, Microsoft bulutuyla ilgili bağlantı sorunlarını belirlemenize yardımcı olabilir.

## <a name="setup-error-codes"></a>Kurulum hata kodları

Configuration Manager bağlı önbellek bileşenini dağıtım noktasına yüklediğinde, aşağıdaki tabloda oluşabilecek olası hata kodları listelenmektedir:

| Hata kodu | Hata açıklaması |
|------------|-------------------|
| 0x00000000 | Başarılı |
| 0x00000BC2 | Başarılı, yeniden başlatma gerekiyor |
| 0x00000643 | Genel yüklemesi hatası |
| 0x00D00001 | Bağlı önbellek kurulumu yalnızca Internet Information Services (IIS) yüklenmişse çalıştırılabilir |
| 0x00D00002 | Bağlı önbellek kurulumu yalnızca sunucuda bir ' varsayılan Web sitesi ' varsa çalıştırılabilir |
| 0x00D00003 | Uygulama Isteği yönlendirme (ARR) zaten yüklüyse bağlı önbellek yükleyemezsiniz |
| 0x00D00004 | Bağlı önbellek kurulumu yalnızca uygulama Isteği yönlendirme (ARR), Install. ps1 betiği tarafından yüklendiyse çalıştırılabilir |
| 0x00D00005 | Bağlı önbellek kurulumu yönetici olarak çalışan bir PowerShell oturumu gerektiriyor |
| 0x00D00006 | Bağlı önbellek kurulumu yalnızca 64 bitlik bir PowerShell ortamından çalıştırılabilir |
| 0x00D00007 | Bağlı önbellek kurulumu yalnızca bir Windows Server 'da çalıştırılabilir |
| 0x00D00008 | Hata: belirtilen önbellek sürücüsü sayısı belirtilen önbellek sürücü boyutu yüzdeleri ile aynı olmalıdır |
| 0x00D00009 | Hata: geçerli bir önbellek düğümü KIMLIĞI sağlanmalıdır |
| 0x00D0000A | Hata: geçerli bir önbellek sürücüsü kümesi sağlanmalıdır |
| 0x00D0000B | Hata: geçerli bir önbellek sürücüsü boyut yüzdesi kümesi sağlanmalıdır |
| 0x00D0000C | Hata: geçerli bir önbellek sürücüsü boyutu yüzdesi kümesi veya GB cinsinden önbellek sürücüsü boyutu sağlanmalıdır |
| 0x00D0000D | Hata: geçerli bir önbellek sürücüsü boyutu yüzdesi kümesi ve önbellek sürücüsü boyutu her ikisi de sağlanamaz |
| 0x00D0000E | Hata: belirtilen önbellek sürücüsü sayısı, belirtilen GB cinsinden önbellek sürücü boyutu sayısıyla aynı olmalıdır |
| 0x00D0000F | Hata: ApplicationHost. config dosyası $AppHostConfig ' dan yedeklenme $AppHostConfigDestinationName |
| 0x00D00010 | Hata: varsayılan Web sitesi Web. config dosyası $WebsiteConfigFilePath 'den $WebConfigDestinationName geri yüklenemedi |
| 0x00D00011 | Hata: SetupARRWebFarm. ps1 içinde bir özel durum oluştu |
| 0x00D00012 | Hata: SetupARRWebFarmRewriteRules. ps1 içinde bir özel durum oluştu |
| 0x00D00013 | Hata: SetupARRWebFarmProperties. ps1 içinde bir özel durum oluştu |
| 0x00D00014 | Hata: SetupAllowableServerVariables. ps1 içinde bir özel durum oluştu |
| 0x00D00015 | Hata: SetupFirewallRules. ps1 içinde bir özel durum oluştu |
| 0x00D00016 | Hata: SetupAppPoolProperties. ps1 içinde bir özel durum oluştu |
| 0x00D00017 | Hata: SetupARROutboundRules. ps1 içinde bir özel durum oluştu |
| 0x00D00018 | Hata: SetupARRDiskCache. ps1 içinde bir özel durum oluştu |
| 0x00D00019 | Hata: SetupARRProperties. ps1 içinde bir özel durum oluştu |
| 0x00D0001A | Hata: SetupARRHealthProbes. ps1 içinde bir özel durum oluştu |
| 0x00D0001B | Hata: VerifyIISSItesStarted. ps1 içinde bir özel durum oluştu |
| 0x00D0001C | Hata: SetDrivesToHealthy. ps1 içinde bir özel durum oluştu |
| 0x00D0001D | Hata: VerifyCacheNodeSetup. ps1 içinde bir özel durum oluştu |
| 0x00D0001E | Varsayılan Web sitesi 80 bağlantı noktasında değilse bağlı önbellek yükleyemezsiniz |
| 0x00D0001F | Hata: yüzde cinsinden önbellek sürücüsü ayırma 100 ' i aşamaz |
| 0x00D00020 | Hata: GB cinsinden önbellek sürücüsü ayırma, sürücünün boş alanını aşamaz |
| 0x00D00021 | Hata: yüzde cinsinden önbellek sürücüsü ayırma 0 ' dan büyük olmalıdır |
| 0x00D00022 | Hata: GB cinsinden önbellek sürücüsü ayırma 0 ' dan büyük olmalıdır |
| 0x00D00023 | Hata: RegisterScheduledTask_CacheNodeKeepAlive bir özel durum oluştu |
| 0x00D00024 | Hata: RegisterScheduledTask_Maintenance bir özel durum oluştu |
| 0x00D00025 | Hata: HTTPS grubu için yeniden yazma kuralları ayarlanırken bir özel durum oluştu: $FarmName |
| 0x00D00026 | Hata: HTTP grubu için yeniden yazma kuralları ayarlanırken bir özel durum oluştu: $FarmName |
| 0x00D00027 | Bağımlı "uygulama Isteği yönlendirme (ARR)" yazılımı yüklenemediğinden bağlı önbellek yükleyemezsiniz. % Temp% \ arr_setup. log konumunda bulunan günlük dosyasına bakın |

## <a name="iis-configurations"></a>IIS yapılandırması

DO Cache Server yüklemesi, dağıtım noktasındaki IIS yapılandırmasında çeşitli değişiklikler yapar.

### <a name="application-request-routing"></a>Uygulama isteği yönlendirme

DO Cache Server, IIS [uygulama Isteği yönlendirme (ARR) uygulamasını](https://www.iis.net/downloads/microsoft/application-request-routing)yüklüyor ve yapılandırır. Olası çakışmaları önlemek için, dağıtım noktasında bu bileşen zaten yüklü olamaz.

### <a name="allowed-server-variables"></a>İzin verilen sunucu değişkenleri

DO Cache sunucusunu yükledikten sonra, varsayılan Web sitesi aşağıdaki *Yerel* sunucu değişkenlerine sahiptir:

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CıD
- X-DOıNC-GIDEN

### <a name="rewrite-rules"></a>Yeniden yazma kuralları

DO Cache Server aşağıdaki yeniden yazma kurallarını ekler:

#### <a name="inbound-rewrite-rules"></a>Gelen yeniden yazma kuralları

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Giden yeniden yazma kuralları

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Sunucu kaynaklarını yönetme

Her DO önbellek sunucusu için gereken disk alanı, kuruluşunuzun güncelleştirme gereksinimlerine bağlı olarak değişiklik gösterebilir. 100 GB, aşağıdaki içeriği önbelleğe almak için yeterli alan olmalıdır:

- Bir özellik güncelleştirmesi
- Kaliteli ve Office güncelleştirmelerinin iki ile üç ayı
- Microsoft Intune uygulamalar ve Windows gelen kutusu uygulamaları

DO Cache Server çok fazla sistem belleği veya işlemci zamanı tüketmemelidir. DO Cache Server 'ı yükledikten sonra, önemli işlem veya bellek kaynak tüketimine dikkat etmeniz durumunda IIS ve ARR günlük dosyalarını çözümleyin.

IIS ve ARR günlük dosyaları sunucuda çok fazla alan kaplasa, günlük dosyalarını yönetmek için kullanabileceğiniz çeşitli yöntemler vardır. Daha fazla bilgi için bkz. [IIS günlük dosyası depolamayı yönetme](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Ayrıca bkz.

[Configuration Manager 'de Microsoft bağlı önbelleği](../../../plan-design/hierarchy/microsoft-connected-cache.md)
