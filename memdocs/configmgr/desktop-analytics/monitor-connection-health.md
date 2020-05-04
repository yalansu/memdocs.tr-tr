---
title: Bağlantı durumunu izleme
titleSuffix: Configuration Manager
description: Configuration Manager ' de masaüstü analizine yönelik bağlantı durumunun ve cihaz durumlarının nasıl izleneceği hakkında ayrıntılar.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 37555c6b60b0d2c18096c2778e9a077baeb9143f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714545"
---
# <a name="monitor-connection-health"></a>Bağlantı durumunu izleme

Cihaz sistem durumu kategorilerine göre detaya gitmek için Configuration Manager 'deki **bağlantı sistem durumu** panosunu kullanın. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Masaüstü Analizi bakım** düğümünü genişletin ve **bağlantı sistem durumu** panosunu seçin.  

[![Configuration Manager bağlantı durumu panosunun ekran görüntüsü](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

Masaüstü analizlerini ilk kez ayarlarken, bu grafikler tüm verileri gösteremeyebilir. Etkin cihazların masaüstü Analizi hizmetine Tanılama verileri gönderebilmesi, verileri işlemek için hizmeti ve sonra Configuration Manager sitesiyle eşitlenmesi 2-3 gün sürebilir.<!-- 4098037 -->

## <a name="connection-details"></a>Bağlantı ayrıntıları

Bu kutucuk, Configuration Manager ile masaüstü Analizi arasında bağlantı hakkında aşağıdaki temel bilgileri görüntüler:

- **Kiracı adı**: **Azure hizmetleri** düğümündeki masaüstü Analizi bağlantısının adı

- **Hedef koleksiyon**: Configuration Manager masaüstü analizine bağlarken belirttiğiniz *hedef koleksiyon* aynı. Bu koleksiyon, ticari KIMLIĞINIZ ve tanılama veri ayarlarınızla Configuration Manager yapılandırdığı tüm cihazları içerir. Bu, Configuration Manager masaüstü Analizi hizmetine bağlanan cihazların eksiksiz kümesidir.

- **Hedeflenen cihazlar**: hedef koleksiyondaki tüm cihazlar, aşağıdaki cihaz türlerinden oluşur:

  - Yetkisi alınmış
  - Geçersiz
  - Etkin değil
  - Yönetilmeyen
  - Windows 10 ' un uzun süreli bakım kanalı (LTSC) sürümlerini çalıştıran cihazlar
  - Windows Server çalıştıran cihazlar

    Bu cihaz durumları hakkında daha fazla bilgi için bkz. [istemci durumu hakkında](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager, hedef koleksiyondaki tüm cihazların istemci analizine, Kullanımdan kaldırılmış ve kullanımdan kalkmış istemcilere yüklenmesini.

- **Da uygun olan cihazlar**: Masaüstü analizine uygun olmayan cihaz sayısı. Örneğin, hedef koleksiyondaki, Windows Server veya Windows 10 uzun süreli bakım kanalı (LTSC) çalıştıran cihazlar.

## <a name="last-sync-details"></a>Son eşitleme ayrıntıları

Bu kutucuk, Configuration Manager masaüstü Analizi bulut hizmeti ile ne zaman eşitlendiği ve kaç cihaz eşitlendiği gösterir.

- **Eşitlenen cihazlar**: Configuration Manager masaüstü analizine gönderilen uygun cihaz sayısı. Hizmet şu anda görünür olan anlık görüntüde bu cihazları içerir.

- **Son hizmet eşitleme**: Masaüstü Analizi portalındaki **Son güncelleme** zamanı ile aynı.

- **Sonraki hizmet eşitleme**: Masaüstü analizinden bir sonraki günlük anlık görüntüyü beklemeniz için.

> [!Note]  
> Cihazları masaüstü Analizi 'ne ilk kez kaydettiğinizde verilerin karşıya yüklenmesi ve işlenmesi birkaç gün sürebilir. Bu süre boyunca, **son eşitleme ayrıntıları** kutucuğu boş görünebilir.
> Ayrıca, isteğe bağlı bir anlık görüntü istediğinizde, bu kutucuktaki değerlerden hiçbiri otomatik olarak günceldir. Daha fazla bilgi için bkz. [veri gecikmesi](troubleshooting.md#data-latency).

Bazı cihazların masaüstü Analizi 'nde gösterilmediğini düşünüyorsanız cihazların masaüstü Analizi tarafından desteklendiğinden emin olun. Daha fazla bilgi için bkz. [Önkoşullar](overview.md#prerequisites).

## <a name="connection-health"></a>Bağlantı sistem durumu

**Bağlantı sistem durumu** grafiği, aşağıdaki sistem durumundaki cihaz sayısını görüntüler:  

- [Düzgün şekilde kaydedildi](#properly-enrolled): cihaz, tam envanterle birlikte masaüstü Analizi 'nde görüntülenir
- [Kayıt yapılamıyor](#unable-to-enroll): cihaz kaydını engelleyen bir engelleme sorunu var
- [Yapılandırma Uyarısı](#configuration-alert): cihaz masaüstü analizinde görünmüyor veya tamamlanmamış bir stokla görünüyor. Configuration Manager ayrıca cihaz kaydında bir sorun belirledi.
- [Kayıt bekleniyor](#awaiting-enrollment): cihaz Configuration Manager yapılandırıldı, ancak henüz masaüstü Analizi 'nde görünmüyor
- [Durum bekliyor](#status-pending): Configuration Manager hala bu cihazı yapılandırıyor ya da cihazın durumunu öğrenmek için cihazda yeterli veri yok
- [Eksik veri](#missing-data): Configuration Manager cihaz yapılandırdı, ancak masaüstü analizinin yalnızca kısmi verileri vardır

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Bu grafikteki cihazların toplam sayısı, bağlantı ayrıntıları kutucuğunda DA aynı şekilde bulunan **cihazlarla** aynı olmalıdır.

Bu duruma sahip cihazların listesine gitmek için grafikteki dilimi seçin. Daha fazla bilgi için bkz. [cihaz listesi](#device-list).

Listeden kaldırmak veya grafikten eklemek için kategori adını seçin. Bu eylem, daha küçük parçaların göreli boyutlarını görebilmeniz için grafiği yakınlaştırmanıza yardımcı olur.

### <a name="properly-enrolled"></a>Düzgün şekilde kaydedildi

Cihaz aşağıdaki özniteliklere sahiptir:

- Configuration Manager istemci sürümü 1902 veya üzeri  
- Yapılandırma hatası yok  
- Masaüstü analizi, bu cihazdan geçen 28 gün içinde tüm tanılama verilerini aldı  
- Masaüstü analizi, cihazın yapılandırmasının ve yüklü uygulamalarının tamamen envanterini içerir  

### <a name="unable-to-enroll"></a>Kayıt yapılamıyor

Configuration Manager, cihaz kaydını engelleyen bir veya daha fazla engelleyici sorunu algılar. Daha fazla bilgi için [Configuration Manager Içindeki masaüstü Analizi cihaz özellikleri](#bkmk_config-issues)listesine bakın.  

Örneğin, Configuration Manager istemcisi en az sürüm 1902 (5.0.8790) değil. İstemciyi en son sürüme güncelleştirin. Configuration Manager sitesi için otomatik istemci yükseltmesini etkinleştirmeyi düşünün. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

Sürüm 2002 ' den başlayarak, istemci proxy yapılandırma sorunlarını iki alanda daha kolay bir şekilde tanımlayabilirsiniz:

- **Uç nokta bağlantısı denetimleri**: istemciler gerekli bir uç noktaya ulaşamazsa, panoda bir yapılandırma uyarısı görürsünüz. Proxy yapılandırma sorunları nedeniyle istemcilerin bağlanamadıkları uç noktaları görmek için kaydedemeyecek istemcilerde detaya gidin. Daha fazla bilgi için bkz. [Endpoint bağlantı denetimleri](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Bağlantı durumu**: Istemcileriniz, masaüstü analizine erişmek için bir proxy sunucusu kullanıyorsa, Configuration Manager istemcilerden proxy kimlik doğrulama sorunlarını görüntüler. Proxy kimlik doğrulama sorunları nedeniyle kaydedemeyecek istemcileri görmek için detaya gidin. Daha fazla bilgi için bkz. [bağlantı durumu](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Yapılandırma Uyarısı

Cihaz, masaüstü Analizi 'nde görünmez veya tamamlanmamış bir stokla birlikte görüntülenir. Configuration Manager ayrıca cihaz kaydında bir sorun belirledi. Daha fazla bilgi için [Configuration Manager Içindeki masaüstü Analizi cihaz özellikleri](#bkmk_config-issues)listesine bakın.

Örneğin, cihazın hizmete bağlantısı yoktur. Daha fazla bilgi için bkz. [Windows Tanılama uç noktası bağlantısı](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Kayıt bekleniyor

Masaüstü analizlerinin bu cihaz için tanılama verileri yok. Bu sorun, son zamanlarda cihazı hedef koleksiyona eklediğiniz ve henüz veri gönderilmemiş olmasından kaynaklanır. Ayrıca cihazın hizmetle düzgün bir şekilde iletişim kurmadığı anlamına gelir ve en son Tanılama verileri 28 günden daha eski olabilir.

Cihazın hizmetle iletişim kurabildiğinden emin olun. Daha fazla bilgi için bkz. [uç noktalar](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Durum bekliyor

Configuration Manager, bu cihazı hala yapılandırıyor veya durumunu öğrenmek için cihazdan yeterli veri yok.

### <a name="missing-data"></a>Eksik veri

Configuration Manager cihazı başarıyla yapılandırdı, ancak masaüstü Analizi bir uyumluluk değerlendirmesi oluşturamaz. Cihazın yapılandırması (Census) veya yüklü uygulamalar (envanter) için bir veri kümesine sahip değildir.

Bu sorun genellikle cihaz yeniden denendiğinde otomatik olarak düzeltilir. Devam ederse, cihazın hizmetle iletişim kurabildiğinden emin olun. Daha fazla bilgi için bkz. [uç noktalar](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Cihaz listesi

Cihazların duruma göre belirli bir listesini görmek için **bağlantı durumu** panosu ile başlayın. **Bağlantı durumu** kutucuğunun segmentlerinden birini seçin ve bu durumdaki cihazların listesine gidin. Bu özel cihaz görünümü aşağıdaki masaüstü Analizi sütunlarını varsayılan olarak görüntüler:

- Ticari KIMLIK yapılandırması
- En düşük uyumluluk güncelleştirmesi
- Windows tanılama verilerini kabul etme
- Windows ticari veri katılımı
- Windows Tanılama uç noktası bağlantısı
- Bağlantı durumu (sürüm 2002 ' den başlayarak)
- Uç nokta bağlantı denetimleri (sürüm 2002 ' den başlayarak)

Bu sütunlar, cihazların masaüstü analiziyle iletişim kurması için temel [önkoşullara](overview.md#prerequisites) karşılık gelir.

[![Cihaz listesinin kaydı yapılamadı ekran görüntüsü](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Ayrıntı bölmesinde kullanılabilir özelliklerin tam listesini görmek için bir cihaz seçin. Ayrıca, bu özelliklerden herhangi birini, cihaz listesine sütun olarak ekleyebilirsiniz.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a>Cihaz özellikleri

Aşağıdaki masaüstü Analizi cihaz özellikleri Configuration Manager cihaz listesinde sütunlar olarak kullanılabilir:

- [Uç nokta bağlantı denetimleri](#endpoint-connectivity-checks) (sürüm 2002 ' den başlayarak)
- [Bağlantı durumu](#connectivity-status) (sürüm 2002 ' den başlayarak)
- [Appraiser yapılandırması](#appraiser-configuration)  
- [En düşük uyumluluk güncelleştirmesi](#minimum-compatibility-update)  
- [Appraiser sürümü](#appraiser-version)  
- [Son başarılı tam Appraiser çalıştırması](#last-successful-full-run-of-appraiser)  
- [Appraiser veri toplama](#appraiser-data-collection)  
- [Census 'in son başarılı tam çalışması](#last-successful-full-run-of-census)  
- [Census veri toplama](#census-data-collection)  
- [Windows Tanılama uç noktası bağlantısı](#windows-diagnostic-endpoint-connectivity)  
- [Son Kullanıcı tanılama verilerini denetle](#check-end-user-diagnostic-data)  
- [Kullanıcı ara sunucusunu denetle](#check-user-proxy)  
- [Ticari KIMLIK yapılandırması](#commercial-id-configuration)  
- [Windows ticari veri katılımı](#windows-commercial-data-opt-in)  
- [Tanılama verilerinde cihaz adını denetle](#check-device-name-in-diagnostic-data)  
- [DiagTrack hizmeti yapılandırması](#diagtrack-service-configuration)  
- [DiagTrack sürümü](#diagtrack-version)  
- [SQM KIMLIĞI alımı](#sqm-id-retrieval)  
- [Benzersiz cihaz tanımlayıcısı alımı](#unique-device-identifier-retrieval)  
- [Windows tanılama verilerini kabul etme](#windows-diagnostic-data-opt-in)  

Bağlantı sistem durumu panosunun **en sık kayıt engelleyiciler ve yapılandırma uyarıları** kutucuğunda, cihazların en sık bir sorun olarak rapor veren özellikleri görüntülenir.

### <a name="endpoint-connectivity-checks"></a>Uç nokta bağlantı denetimleri

Sürüm 2002 ' den başlayarak,<!-- 4963230 --> proxy kimlik doğrulama sorunlarını algılamak için istemciler gerekli uç noktalara göre bağlantı denetimleri gerçekleştirir. İstemci gerekli bir uç noktaya ulaşamadıysanız, bu özellik proxy yapılandırma sorunları nedeniyle bağlanamadıkları uç noktaların numaralandırılmış bir listesini gösterir. Bu listeyi, [gerekli uç noktaların](enable-data-sharing.md#endpoints)yayımlanmış listesiyle karşılaştırın.

### <a name="connectivity-status"></a>Bağlantı durumu

Sürüm 2002 ' den başlayarak,<!-- 4963383 --> istemcileriniz, masaüstü analizine erişmek için bir proxy sunucusu kullanıyorsa, bu özellik proxy kimlik doğrulama sorunlarını gösterir. Proxy kimlik doğrulamasıyla ilgili aşağıdaki ayrıntıları içerir:

- Durum kodu
- Dönüş kodu

Günlük dosyasında aşağıdakine benzer hatalar görürsünüz:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

`%s` , Gerekli bir uç noktanın URL 'sidir.

Ayrıca, cihazlar kayıt sorunlarıyla karşılaşana kadar dikkat gerektirmeyen belirleyici olmayan hata iletileri de görebilirsiniz. Örneğin:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Ara sunucuları masaüstü analizi ile kullanılmak üzere yapılandırma hakkında daha fazla bilgi için bkz. [proxy sunucusu kimlik doğrulaması](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Appraiser yapılandırması

<!--20,21-->
Appraiser, [Uyumluluk güncelleştirmelerine](enroll-devices.md#update-devices)karşılık gelen Windows bileşenidir. Windows 'un en son sürümüyle uyumluluk için cihazdaki uygulamalar ve sürücüler değerlendirir.

Bu denetim başarılı olursa, Appraiser bileşeni cihazda düzgün şekilde yapılandırılır.

Aksi takdirde, aşağıdaki hatalardan birini gösterebilir:

- Cihaz uygulama uyumluluk verileri koleksiyonu yapılandırılamıyor (Setrequestallappraerversions). Özel durum ayrıntıları için günlükleri denetleyin  

- Cihaz uygulama uyumluluk verileri koleksiyonu yapılandırılamıyor (Setrequestallappraerversions). Özel durum ayrıntıları için günlükleri denetleyin  

- Requestallappraerversions kayıt defteri anahtarına `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`yazılamıyor. İzinleri denetle  

Bu kayıt defteri anahtarındaki izinleri denetleyin. Yerel sistem hesabının, Configuration Manager istemcisinin ayarlaması için bu anahtara erişebildiğinizden emin olun.  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

### <a name="minimum-compatibility-update"></a>En düşük uyumluluk güncelleştirmesi

<!--18,19,32-->
Uyumluluk Güncelleştirmesi (Appraiser. dll), cihazda yüklü değil veya güncel değil. Masaüstü analizi, 10.0.17763 için en düşük gereksinimden daha eski.

En son uyumluluk güncelleştirmesini yükler. Daha fazla bilgi için bkz. [Uyumluluk güncelleştirmeleri](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Appraiser sürümü

Bu özellik cihazdaki Appraiser bileşeninin geçerli sürümünü görüntüler. Üzerinde `%windir%\System32\appraiser.dll`, ondalık noktaları olmadan dosya sürümü gösterilir. Örneğin, dosya sürümü 10.0.17763 10017763 olarak görüntülenir.

### <a name="last-successful-full-run-of-appraiser"></a>Son başarılı tam Appraiser çalıştırması

Bu özellik, cihazın en son başarıyla çalıştırıldığı tarihi ve saati gösterir Appraiser.

### <a name="appraiser-data-collection"></a>Appraiser veri toplama

<!--Appraiser run status-->
<!--22,33-->
Bu özellik, Appraiser bileşenini çalıştıran Windows 'un en son sonucunu gösterir.

Başarılı olmazsa, aşağıdaki hatalardan birini gösterebilir:

- Uygulama uyumluluğu verileri toplanamıyor (RunAppraiser). Ayrıntılar için günlüklere bakın  

- Uygulama uyumluluğu veri toplama (CompatTelRunner. exe) bir hata koduyla sona erdi  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.

Şu dosyayı denetleyin: `%windir%\System32\CompatTelRunner.exe`. Mevcut değilse, gerekli [uyumluluk güncelleştirmelerini](enroll-devices.md#update-devices)yeniden yükleyin. Grup İlkesi veya kötü amaçlı yazılımdan koruma hizmeti gibi başka bir sistem bileşeninin bu dosyayı kaldırmakta olmadığından emin olun.

İstemcideki M365AHandler. log dosyası aşağıdaki hatalardan birini içeriyorsa:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Bu hataları düzeltmeye yardımcı olması için etkilenen istemcide yükseltilmiş bir Windows PowerShell konsolundan aşağıdaki komutları çalıştırın:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Census 'in son başarılı tam çalışması

Bu özellik, cihazın Census 'i son çalıştırdığı tarihi ve saati görüntüler.

### <a name="census-data-collection"></a>Census veri toplama

<!-- Census run status -->
<!--51,52-->
Census, cihazı izleyen Windows bileşenidir. Bu envanter verileri, cihazı ve yapılandırmasını anlamak için kullanılır.

Bu özellik, görselleştirmenizdeki bileşenini çalıştıran Windows 'un en son sonucunu gösterir.

Başarılı olmazsa, aşağıdaki hatalardan birini gösterebilir:

- Cihaz ve yapılandırması (RunCensus) hakkında veri toplanamıyor. Özel durum ayrıntıları için günlükleri denetleyin  

- Cihaz ve yapılandırma verileri toplama aracı (devicecensus. exe) bulunamadı  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.

Şu dosyayı denetleyin: `%windir%\System32\DeviceCensus.exe`. Mevcut değilse, gerekli [uyumluluk güncelleştirmelerini](enroll-devices.md#update-devices)yeniden yükleyin. Grup İlkesi veya kötü amaçlı yazılımdan koruma hizmeti gibi başka bir sistem bileşeninin bu dosyayı kaldırmakta olmadığından emin olun.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows Tanılama uç noktası bağlantısı

<!--12,15-->
Bu denetim başarılı olursa cihaz, bağlı kullanıcı deneyimine ve telemetri uç noktasına (Vortex) bağlanabilir.

Aksi takdirde, aşağıdaki hatalardan biri gösterilebilir:  

- Bağlı kullanıcı deneyimi ve telemetri uç noktası (Vortex) ile bağlantı kurulamadı. Ağ/proxy ayarlarınızı denetleyin  

- Bağlı kullanıcı deneyimi ve telemetri uç noktası (CheckVortexConnectivity) bağlantısı denetlenemiyor. Özel durum ayrıntıları için günlükleri denetleyin  

Cihazlar işletim sistemi sürümüne bağlı olarak aşağıdaki uç noktaya bir GET isteğiyle bağlantıyı doğrular:

| İşletim sistemi sürümü | Uç Nokta |
|------------|----------|
| -Windows 10, sürüm 1809 veya üzeri<br/>-Windows 10, sürüm 1803, 2018-09 toplu güncelleştirmesi veya sonrası | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, sürüm 1803, 2018-09 veya üzeri toplu güncelleştirme *olmadan* | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, sürüm 1709 veya öncesi | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 veya Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Cihazın hizmetle iletişim kurabildiğinden emin olun. Bu denetim, gerekli tüm uç noktaların tümünü değil bazılarını doğrular. Daha fazla bilgi için bkz. [uç noktalar](enable-data-sharing.md#endpoints).  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

### <a name="check-end-user-diagnostic-data"></a>Son Kullanıcı tanılama verilerini denetle

<!--1004-->
Bu denetim başarılı olmazsa, bir Kullanıcı cihazda daha düşük bir Windows tanılama verisi seçti. Ayrıca, çakışan bir Grup İlkesi nesnesi de oluşabilir. Daha fazla bilgi için bkz. [Windows ayarları](enroll-devices.md#windows-settings).

İş gereksinimlerinize bağlı olarak, Grup İlkesi aracılığıyla Kullanıcı seçimini devre dışı bırakabilirsiniz. **Telemetri katılım ayarı Kullanıcı arabirimini yapılandırmak**için bu ayarı kullanın. Daha fazla bilgi için bkz. [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Kullanıcı ara sunucusunu denetle

<!--30,35-->
DisableEnterpriseAuthProxy ayarı, Windows 7 için varsayılan olarak etkindir. Windows 8.1 bilgisayarlar için, Configuration Manager DisableEnterpriseAuthProxy ayarını 0 (devre dışı değil) olarak ayarlar.

Bu özellik aşağıdaki hataları gösterebilir:

- Kimlik doğrulama proxy 'si etkin. DisableEnterpriseAuthProxy 'yi içinde 0 olarak ayarla`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Kimlik doğrulama proxy 'si durumu denetlenemiyor. Özel durum ayrıntıları için günlükleri denetleyin

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

Bu kayıt defteri anahtarındaki izinleri denetleyin. Yerel sistem hesabının, Configuration Manager istemcisinin ayarlaması için bu anahtara erişebildiğinizden emin olun. Ayrıca, çakışan bir Grup İlkesi nesnesi de oluşabilir. Daha fazla bilgi için bkz. [Windows ayarları](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Ticari KIMLIK yapılandırması

<!--9, 11, 53-->
Microsoft, cihazlarındaki bilgileri masaüstü Analizi çalışma alanınıza eşlemek için benzersiz bir ticari KIMLIK kullanır. Configuration Manager masaüstü analizi ile tümleştirdiğinizde, bu KIMLIK için hizmeti otomatik olarak sorgular. Configuration Manager, bu KIMLIĞI masaüstü Analizi ayarlarını hedeflediğiniz istemcilere otomatik olarak uygulamalıdır.

Bu denetim başarılı olursa cihaz, ticari KIMLIK ile düzgün şekilde yapılandırılır.

Aksi takdirde, aşağıdaki hatalardan biri gösterilebilir:

- Ticari kimlik kayıt defteri anahtarına `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`yazılamıyor. İzinleri denetle  

- Kayıt defteri anahtarındaki `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`ticari kimlik güncelleştirilemez. Özel durum ayrıntıları için günlükleri denetleyin  

- Doğru ticari kimlik değerini sağlayın`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

Bu kayıt defteri anahtarındaki izinleri denetleyin. Yerel sistem hesabının, Configuration Manager istemcisinin ayarlaması için bu anahtara erişebildiğinizden emin olun. Ayrıca, çakışan bir Grup İlkesi nesnesi de oluşabilir. Daha fazla bilgi için bkz. [Windows ayarları](enroll-devices.md#windows-settings).  

Cihaz için farklı bir KIMLIK vardır. Bu kayıt defteri anahtarı Grup İlkesi tarafından kullanılır. Configuration Manager tarafından belirtilen KIMLIĞE göre önceliklidir.  

<a name="bkmk_ViewCommercialID"></a>Masaüstü Analizi portalındaki ticari KIMLIĞI görüntülemek için aşağıdaki yordamı kullanın:

1. Masaüstü Analizi portalına gidin ve genel ayarlar grubunda **bağlı hizmetler** ' i seçin.  

2. **Bağlı hizmetler** bölmesinde, **cihazları kaydet** bölmesi varsayılan olarak seçilidir. Cihazları kaydet bölmesinde bilgi bölümünde ticari KIMLIK anahtarınız görüntülenir.  

[![Masaüstü Analizi portalındaki ticari KIMLIK ekran görüntüsü](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Geçerli olanı kullanamıyoruz yalnızca **yenı kimlik anahtarı alın** . Ticari KIMLIĞI yeniden oluşturursanız, [cihazlarınızı yeni kimliğe yeniden kaydedin](enroll-devices.md#device-enrollment). Bu işlem, geçiş sırasında tanılama verilerinin kaybedilmesine neden olabilir.  

### <a name="windows-commercial-data-opt-in"></a>Windows ticari veri katılımı

<!--64-->
Bu özellik Windows 7 veya Windows 8.1 çalıştıran cihazlara özgüdür. Benzer testleri, ticari veri OptIn değeri dışında [Windows Tanılama verileri katılımı](#windows-diagnostic-data-opt-in)olarak çalıştırır.

### <a name="check-device-name-in-diagnostic-data"></a>Tanılama verilerinde cihaz adını denetle

<!--56,58-->
Bu denetim başarılı olursa cihaz, cihaz adını paylaşacak şekilde düzgün şekilde yapılandırılır.

Aksi takdirde, aşağıdaki hatalardan biri gösterilebilir:

- Windows Tanılama verilerinin bir parçası olarak Microsoft 'a gönderilecek cihaz adı denetlenemiyor. Özel durum ayrıntıları için günlükleri denetleyin  

- AllowDeviceNameInTelemetry kayıt defteri anahtarına `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`yazılamıyor. İzinleri denetle  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

Bu kayıt defteri anahtarındaki izinleri denetleyin. Yerel sistem hesabının, Configuration Manager istemcisinin ayarlaması için bu anahtara erişebildiğinizden emin olun. Ayrıca, çakışan bir Grup İlkesi nesnesi de oluşabilir. Daha fazla bilgi için bkz. [Windows ayarları](enroll-devices.md#windows-settings).  

Grup İlkesi gibi başka bir ilke mekanizmasının bu ayarı devre dışı bıraktığınızdan emin olun.

### <a name="diagtrack-service-configuration"></a>DiagTrack hizmeti yapılandırması

<!--44,45,50-->
Bu denetim başarılı olursa, DiagTrack bileşeni cihazda düzgün şekilde yapılandırılır. Masaüstü analizi için gereken en düşük sürüm 10010586 ' dir (10.0.10586).

Aksi takdirde, aşağıdaki hatalardan birini gösterebilir:

- Bağlı kullanıcı deneyimi ve telemetri (diagtrack. dll) bileşeni güncel değil. Gereksinimleri denetle  

- Bağlı kullanıcı deneyimi ve telemetri (diagtrack. dll) bileşeni bulunamıyor. Gereksinimleri denetle  

- Microsoft 'a veri göndermek için bağlı kullanıcı deneyimlerini ve telemetri hizmetini etkinleştirin ve başlatın  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

En son güncelleştirmeleri yükler. Daha fazla bilgi için bkz. [cihaz güncelleştirmeleri](enroll-devices.md#update-devices).

Cihazdaki **bağlı kullanıcı deneyimlerinin ve telemetri** hizmetinin çalıştığından emin olun.

### <a name="diagtrack-version"></a>DiagTrack sürümü

Bu özellik, cihazda bağlı kullanıcı deneyiminin ve telemetri bileşeninin geçerli sürümünü görüntüler. Üzerinde `%windir%\System32\diagtrack.dll`, ondalık noktaları olmadan dosya sürümü gösterilir. Örneğin, dosya sürümü 10.0.10586 10010586 olarak görüntülenir.

### <a name="sqm-id-retrieval"></a>SQM KIMLIĞI alımı

<!--38-->
Bu özellik öncelikli olarak Windows 7 cihazlarına yöneliktir. Bu, daha sonraki işletim sistemi sürümleri tarafından cihaz için bir geri dönüş tanımlayıcısı olarak kullanılabilir.

Başarılı olmazsa, şu hata görüntülenebilir:

- Eski cihaz telemetri tanımlayıcısı alınamıyor (SQM KIMLIĞI)

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

Ortamınızda yinelenen kimliklere sahip olmadığınızdan emin olun. Örneğin, cihazlar Genelleştirilmiş olmayan bir işletim sistemi görüntüsüyle dağıtıldıysa.

### <a name="unique-device-identifier-retrieval"></a>Benzersiz cihaz tanımlayıcısı alımı

<!--54-->
Masaüstü analizi, daha güvenilir bir cihaz kimliği için Microsoft hesabı hizmetini kullanır.

**Microsoft hesabı oturum açma Yardımcısı** hizmetinin devre dışı olmadığından emin olun. Başlangıç türü **el ile (tetikleyici başlatma)** olmalıdır.

Son Kullanıcı Microsoft hesabı erişimini devre dışı bırakmak için, bu uç noktayı engellemek yerine ilke ayarlarını kullanın. Daha fazla bilgi için bkz. [enterprise Microsoft hesabı](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Windows tanılama verilerini kabul etme

<!--8,40,55,62-->
Bu özellik, Windows 'un tanılama verilerine izin verecek şekilde düzgün yapılandırıldığını denetler. Aşağıdaki kayıt defteri anahtarlarında Allowtelemetri değerini denetler:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Bu kayıt defteri anahtarlarındaki izinleri denetleyin. Yerel sistem hesabının, Configuration Manager istemcisinin ayarlaması için bu anahtarlara erişebildiğinizden emin olun. Ayrıca, çakışan bir Grup İlkesi nesnesi de oluşabilir. Daha fazla bilgi için bkz. [Windows ayarları](enroll-devices.md#windows-settings).  

Daha fazla bilgi için istemcide M365AHandler. log dosyasına bakın.  

## <a name="see-also"></a>Ayrıca bkz.

[Desktop Analytics sorunlarını giderme](troubleshooting.md)
