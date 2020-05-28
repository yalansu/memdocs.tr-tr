---
title: Günlük dosyaları hakkında
titleSuffix: Configuration Manager
description: Configuration Manager istemcileri ve site sistemleriyle ilgili sorunları gidermek için günlük dosyalarını kullanın.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588bccc533909f2438dc61d6f25b39c3a582c71b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879020"
---
# <a name="about-log-files-in-configuration-manager"></a>Configuration Manager 'de günlük dosyaları hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, istemci ve site sunucusu bileşenleri işlem bilgilerini ayrı günlük dosyalarına kaydeder. Ortaya çıkabilecek sorunları gidermenize yardımcı olması için bu günlük dosyalarındaki bilgileri kullanabilirsiniz. Varsayılan olarak, Configuration Manager istemci ve sunucu bileşenleri için günlüğe kaydetmeye izin vermez.

Bu makalede Configuration Manager günlük dosyaları hakkında genel bilgiler sağlanmaktadır. Kullanılacak araçları, günlükleri yapılandırmayı ve bunların nerede bulunacağını içerir. Belirli günlük dosyaları hakkında daha fazla bilgi için bkz. [günlük dosyaları başvurusu](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a>Nasıl çalıştığı

Configuration Manager çoğu işlem, işletimsel bilgileri bu işleme ayrılmış bir günlük dosyasına yazar. Günlük dosyaları **. log** veya **. LO_** dosya uzantıları tarafından tanımlanır. Configuration Manager, günlük en büyük boyutuna erişene kadar bir. log dosyasına yazar. Günlük dolduğunda,. log dosyası aynı ada sahip olan, ancak. lo_ uzantılı bir dosyaya kopyalanır ve işlem ya da bileşen. log dosyasına yazmaya devam eder. . Log dosyası yeniden en büyük boyutuna ulaştığında,. lo_ dosyasının üzerine yazılır ve işlem yinelenir. Bazı bileşenler, günlük dosyası adına bir tarih ve saat damgası ekleyerek ve. log uzantısını koruyarak bir günlük dosyası geçmişi oluştururlar.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a>Günlük Görüntüleyicisi araçları

Tüm Configuration Manager günlük dosyaları düz metinlerdir, böylece bunları not defteri gibi herhangi bir metin okuyucu ile görüntüleyebilirsiniz. Günlükler, aşağıdaki özelleştirilmiş araçlardan biriyle en iyi şekilde görüntülenen benzersiz biçimlendirmeyi kullanır:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Destek Merkezi günlük Görüntüleyici](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Günlükleri görüntülemek için Configuration Manager günlük Görüntüleyici aracı **CMTrace**' i kullanın. `\SMSSetup\Tools`Configuration Manager kaynak ortamının klasöründe bulunur. CMTrace Aracı, yazılım kitaplığı 'na eklenen tüm önyükleme görüntülerine eklenir. CMTrace günlük görüntüleme aracı, Configuration Manager istemcisiyle birlikte otomatik olarak yüklenir.<!--1357971--> Daha fazla bilgi için bkz. [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

Sürüm 1906 ' den başlayarak **Onetrace** , Destek Merkezi 'nin bulunduğu yeni bir günlük görüntüleyicisine sahiptir. Geliştirme ile CMTrace 'e benzer şekilde çalışır. Daha fazla bilgi için bkz. [Destek Merkezi OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Destek Merkezi günlük Görüntüleyici

**Destek Merkezi** , modern bir günlük Görüntüleyici içerir. Bu araç CMTrace 'in yerini alır ve sekmeler ve yerleştirilebilir Windows desteğiyle özelleştirilebilir bir arabirim sağlar. Bu, hızlı bir sunu katmanına sahiptir ve büyük günlük dosyalarını Saniyeler içinde yükleyebilir. Daha fazla bilgi için bkz. [Destek Merkezi günlük Görüntüleyici başvurusu](../../support/support-center-ui-reference.md#bkmk_log-viewer).

> [!Note]  
> Destek Merkezi ve OneTrace Windows Presentation Foundation (WPF) kullanır. Bu bileşen Windows PE 'de kullanılamaz. Görev sırası dağıtımlarıyla önyükleme görüntülerinde CMTrace 'i kullanmaya devam edin.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a>Günlüğe kaydetme seçeneklerini yapılandırma

Ayrıntılı düzey, boyut ve geçmiş gibi günlük dosyalarının yapılandırmasını değiştirebilirsiniz. Bu ayarları değiştirmek için birkaç yol vardır:

- [İstemci yüklemesi sırasında](#bkmk_logoptions-clientprop)
- [Configuration Manager Service Manager kullanma](#bkmk_logoptions-sm)
- [Windows kayıt defteri 'ni kullanma](#bkmk_logoptions-registry)
- [Configuration Manager konsolunda](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a>İstemci yüklemesi sırasında günlüğe kaydetme seçeneklerini yapılandırma

Yükleme sırasında istemci günlük dosyalarının yapılandırmasını ayarlayabilirsiniz. Aşağıdaki özellikleri kullanın:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Daha fazla bilgi için bkz. [istemci yükleme özellikleri](../../clients/deploy/about-client-installation-properties.md#clientMsiProps).

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a>Configuration Manager Service Manager kullanarak günlüğe kaydetme seçeneklerini yapılandırma

Günlük dosyalarını ve bunların boyutunu Configuration Manager nerede depoladığını değiştirebilirsiniz.  

Günlük dosyalarının boyutunu değiştirmek için, günlük dosyasının adını ve konumunu değiştirin veya birden çok bileşeni tek bir günlük dosyasına yazmaya zorlamak için aşağıdaki adımları uygulayın:  

#### <a name="modify-logging-for-a-component"></a>Bir bileşen için günlük kaydını değiştirme  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **sistem durumu**' nu genişletin ve ardından **Site durumu** veya **Bileşen durumu** düğümünü seçin.  

2. Şeritte **Başlat**' ı ve ardından **Configuration Manager Service Manager**' yı seçin.  

3. Configuration Manager Service Manager açıldığında, yönetmek istediğiniz siteye bağlanın. Yönetmek istediğiniz site gösterilmemişse, **site**' yi seçin, **Bağlan**' ı seçin ve ardından doğru sitenin site sunucusunun adını girin.  

4. Siteyi genişletin ve yönetmek istediğiniz bileşenlerin bulunduğu yere göre **Bileşenler** veya **sunucular**' a gidin.  

5. Sağ bölmede bir veya daha fazla bileşen seçin.  

6. **Bileşen** menüsünde **günlüğe**Kaydet ' i seçin.  

7. **Configuration Manager Bileşen Günlüğü** iletişim kutusunda, seçiminize yönelik mevcut yapılandırma seçeneklerini tamamlayın.  

8. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a>Windows kayıt defteri 'ni kullanarak günlüğe kaydetme seçeneklerini yapılandırma

<!-- SCCMDocs#992 -->
Aşağıdaki günlük seçeneklerini değiştirmek için sunucularda veya istemcilerde Windows kayıt defteri 'ni kullanın:

- Ayrıntı düzeyi
- Maksimum geçmiş
- Maksimum boyut

Bir sorunu giderirken, günlük dosyalarında ek ayrıntılar yazmak üzere Configuration Manager için ayrıntılı günlük kaydını etkinleştirebilirsiniz.

> [!Warning]
> Bu ayarların yanlış yapılandırılması Configuration Manager, büyük miktarlarda bilgileri günlüğe kaydedebilir veya hiç hiçbirini hiç açmaz. Bu veriler sorun giderme için yararlı olsa da, üretim sitelerinde bu değerleri değiştirirken dikkatli olun. Bu değişiklikleri her zaman önce bir laboratuar ortamında test edin. Aşırı günlük kaydı gerçekleşebilir, bu durum günlük dosyalarındaki ilgili bilgileri bulmayı zorlaştırır.

Bu kayıt defteri ayarlarında değişiklik yaptıktan sonra, bileşeni yeniden başlatın:

- İstemci ayarlarını değiştirirseniz, **SMS Aracısı ana bilgisayar** hizmeti 'Ni (Ccmexec) yeniden başlatın.
- Sunucu ayarlarını değiştirirseniz, **SMS Executive** hizmetini yeniden başlatın.

Kayıt defteri ayarları bileşene bağlı olarak değişir:

- [İstemci ve yönetim noktası](#bkmk_reg-client)
- [Site sunucusu](#bkmk_reg-site)
- [Site sistemi rolü](#bkmk_reg-role)
- [Configuration Manager konsolu](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a>İstemci ve yönetim noktası günlüğe kaydetme seçenekleri

İstemci veya yönetim noktası site sistemindeki tüm bileşenlerin günlük seçeneklerini yapılandırmak için, bu **REG_DWORD** değerlerini aşağıdaki Windows kayıt defteri anahtarı altında yapılandırın:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Name  |Değerler  |Açıklama  |
|---------|---------|---------|
|LogLevel|`0`: Verbose<br>`1`: Varsayılan<br>`2`: Uyarılar ve hatalar<br>`3`: Yalnızca hatalar|Günlük dosyalarına yazılacak ayrıntı düzeyi.|
|LogMaxHistory|Sıfırdan büyük veya sıfıra eşit herhangi bir tamsayı, örneğin:<br>`0`: Geçmiş yok<br>`1`: Varsayılan|Bir günlük dosyası en büyük boyuta ulaştığında, istemci onu bir yedekleme olarak yeniden adlandırır ve yeni bir günlük dosyası oluşturur. Kaç tane eski sürümü tutulacağını belirtin.|
|LogMaxSize|10.000 değerinden büyük veya buna eşit bir tamsayı, örneğin:<br>250000|Bayt cinsinden en büyük günlük dosyası boyutu. Bir günlük belirtilen boyuta büyüdükçe, istemci onu bir geçmiş dosyası olarak yeniden adlandırır ve yeni bir dosya oluşturur. Varsayılan değer 250.000 bayttır.|

> [!Note]  
> Bu kayıt defteri anahtarında mevcut olabilecek diğer değerleri değiştirmeyin.

Gelişmiş hata ayıklama için bu **REG_SZ** değerini aşağıdaki Windows kayıt defteri anahtarı altına da ekleyebilirsiniz:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Name  |Değerler  |Açıklama  |
|---------|---------|---------|
|Etkin | `True`: hata ayıklama günlüklerini etkinleştir<br>`False`: hata ayıklama günlüklerini devre dışı bırak |Sorun giderme amacıyla günlüğe hata ayıklama desteği sunar.|

Bu ayar, istemcinin sorun giderme için düşük düzey bilgileri kaydetmesine neden olur. Bu ayarı üretim sitelerinde kullanmaktan kaçının. Aşırı günlük kaydı gerçekleşebilir, bu durum günlük dosyalarındaki ilgili bilgileri bulmayı zorlaştırır. Sorunu çözdükten sonra bu ayarı etkinleştirdiğinizden emin olun.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a>Site sunucusu günlük seçenekleri

Ayarları genel olarak veya Configuration Manager site sunucusundaki belirli bir bileşen için yapılandırabilirsiniz.

Aşağıdaki Windows kayıt defteri anahtarı altında bu değerleri yapılandırın:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Name  |Değerler  |Tür  |Açıklama
|---------|---------|---------|---------|
|SqlEnabled| `1`: SQL izlemeyi etkinleştir<br> `0`: SQL izlemeyi devre dışı bırak |REG_DWORD|Tüm site sunucusu günlüklerine SQL izleme günlüğü ekleyin.|
|ArchiveEnabled| `1`: günlük arşivlerini etkinleştir<br> `0`: günlük arşivlerini devre dışı bırak | REG_DWORD |Site sunucusu günlüklerini geçmiş koruma için ayrı bir konuma arşivleyebilirsiniz.|
|ArchivePath| Geçerli bir klasör yolu, örneğin`C:\Logs\Archive` | REG_SZ |Site sunucusu günlüklerinin arşivleneceği yol.|

Yalnızca, sorun giderme amacıyla SQL izlemeyi etkinleştirin. Üretim sitelerinde kullanmaktan kaçının. Aşırı günlük kaydı gerçekleşebilir, bu durum günlük dosyalarındaki ilgili bilgileri bulmayı zorlaştırır. Sorunu çözdükten sonra bu ayarı etkinleştirdiğinizden emin olun.

> [!Note]  
> Bu kayıt defteri anahtarında mevcut olabilecek diğer değerleri değiştirmeyin.

Belirli bir sunucu bileşeni için günlük seçeneklerini yapılandırmak için, aşağıdaki Windows kayıt defteri anahtarı altında bu **REG_DWORD** değerleri yapılandırın:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Name  |Değerler  |Açıklama  |
|---------|---------|---------|
|LoggingLevel|`0`: Verbose<br>`1`: Varsayılan<br>`2`: Uyarılar ve hatalar<br>`3`: Yalnızca hatalar|Günlük dosyalarına yazılacak ayrıntı düzeyi.|
|LogMaxHistory|Sıfırdan büyük veya sıfıra eşit herhangi bir tamsayı, örneğin:<br>`0`: Geçmiş yok<br>`1`: Varsayılan|Günlük dosyası en büyük boyuta ulaştığında, sunucu onu bir yedekleme olarak yeniden adlandırır ve yeni bir günlük dosyası oluşturur. Kaç tane eski sürümü tutulacağını belirtin.|
|MaxFileSize|10.000 değerinden büyük veya buna eşit bir tamsayı, örneğin:<br>250000|Bayt cinsinden en büyük günlük dosyası boyutu. Bir günlük belirtilen boyuta büyüdükçe, istemci onu bir geçmiş dosyası olarak yeniden adlandırır ve yeni bir dosya oluşturur. Varsayılan değer 250.000 bayttır.|
|DebugLogging| `1`: hata ayıklama günlüklerini etkinleştir<br>`0`: hata ayıklama günlüklerini devre dışı bırak |Sorun giderme amacıyla günlüğe hata ayıklama desteği sunar.|

DebugLogging ayarı, sunucuda sorun giderme için düşük düzey bilgileri günlüğe kaydetmesine neden olur. Bu ayarı üretim sitelerinde kullanmaktan kaçının. Aşırı günlük kaydı gerçekleşebilir, bu durum günlük dosyalarındaki ilgili bilgileri bulmayı zorlaştırır. Sorunu çözdükten sonra bu ayarı etkinleştirdiğinizden emin olun.

> [!Note]  
> Bu kayıt defteri anahtarında mevcut olabilecek diğer değerleri değiştirmeyin.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a>Site sistemi rol günlüğü seçenekleri

Ayarları, genel olarak veya Configuration Manager sunucu rolü barındıran bir site sisteminde belirli bir bileşen için yapılandırabilirsiniz.

Belirli bir sunucu bileşeni için günlük seçeneklerini yapılandırmak için, aşağıdaki Windows kayıt defteri anahtarı altında bu **REG_DWORD** değerleri yapılandırın:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Örneğin, dağıtım noktası rolü için:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Name  |Değerler  |Açıklama  |
|---------|---------|---------|
|LogLevel|`0`: Verbose<br>`1`: Varsayılan<br>`2`: Uyarılar ve hatalar<br>`3`: Yalnızca hatalar|Günlük dosyalarına yazılacak ayrıntı düzeyi.|
|LogMaxHistory|Sıfırdan büyük veya sıfıra eşit herhangi bir tamsayı, örneğin:<br>`0`: Geçmiş yok<br>`1`: Varsayılan|Günlük dosyası en büyük boyuta ulaştığında, sunucu onu bir yedekleme olarak yeniden adlandırır ve yeni bir günlük dosyası oluşturur. Kaç tane eski sürümü tutulacağını belirtin.|
|LogMaxSize|10.000 değerinden büyük veya buna eşit bir tamsayı, örneğin:<br>250000|Bayt cinsinden en büyük günlük dosyası boyutu. Bir günlük belirtilen boyuta büyüdükçe, sunucu onu bir geçmiş dosyası olarak yeniden adlandırır ve yeni bir dosya oluşturur. Varsayılan değer 250.000 bayttır.|

> [!Note]  
> Bu kayıt defteri anahtarında mevcut olabilecek diğer değerleri değiştirmeyin.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a>Konsol günlüğü seçeneklerini Configuration Manager

Configuration Manager konsolunun AdminUI. log öğesinin ayrıntı düzeyini değiştirmek için aşağıdaki yordamı kullanın:

1. **Microsoft. ConfigurationManagement. exe. config**konsol yapılandırma dosyasını Not defteri gıbı bir XML düzenleyicisinde açın. Varsayılan yapılandırma dosyası şu konumdadır:`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

    > [!IMPORTANT]
    > Sürüm 1910 ' den başlayarak, bu yol klasörü kullanacak şekilde değiştirilmiştir `Microsoft Endpoint Manager` . Dosyanın başka bir klasörde mevcut olabilecek eski bir sürümünü kullandığınızdan emin olun.

1. **System. Diagnostics**  >  **kaynakları**  >  **kaynak** öğesi altında **switchValue** özniteliğini `Error` olarak değiştirin `Verbose` . Örneğin:

    Özgün: `<source name="SmsAdminUISnapIn" switchValue="Error">` Yeni:`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Dosyayı kaydedin ve konsolunu yeniden başlatın.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a>Configuration Manager konsolundaki günlük seçeneklerini yapılandırma

<!-- 4433455 -->

Sürüm 1910 ' den başlayarak, konsolundan bir istemcide veya koleksiyonda ayrıntılı günlük kaydını etkinleştirin veya devre dışı bırakın:

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **cihazlar** düğümünü seçin ve bir hedef cihaz seçin.

1. Şeritte, **giriş** sekmesinde, **cihaz** grubunda, **istemci tanılama**' yı seçin. Kullanılabilir eylemlerden birini seçin.

Daha fazla bilgi için bkz. [istemci tanılama](../../clients/manage/client-notification.md#client-diagnostics).

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a>Günlük dosyalarını bulma

Configuration Manager ve bağımlı bileşenler günlük dosyalarını çeşitli konumlarda depolar. Bu konumlar, günlük dosyasını ve ortamınızın yapılandırmasını oluşturan işleme göre değişir.

Aşağıdaki konumlar varsayılan değerdir. Ortamınızda yükleme dizinlerini özelleştirdiyseniz gerçek yollar farklılık gösterebilir.

- İstemcilerinin`C:\Windows\CCM\logs`
- Server`C:\Program Files\Microsoft Configuration Manager\Logs`
- Yönetim noktası:`C:\SMS_CCM\Logs`
- Configuration Manager konsolu:`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog`
- ISS`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Görev sırası günlük konumları

Görev dizisi günlük dosyası **Smsts. log** dosyasının konumu, görev dizisinin aşamasına bağlı olarak değişir:

- [Biçimlendirme ve disk bölümleme](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) adımından önce Windows PE 'de: `X:\Windows\temp\smstslog\smsts.log` (X, Windows PE RAM sürücüsüdür)
- **Biçim ve Bölüm diski** adımından sonra Windows PE 'de: `X:\smstslog\smsts.log` , sürücü için `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- İstemci yüklenmeden önce yeni Windows işletim sistemi:`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- İstemci yüklendikten sonra Windows 'ta:`C:\Windows\CCM\Logs\smstslog\smsts.log`
- Görev dizisi tamamlandıktan sonra Windows 'ta:`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) salt okunurdur görev dizisi değişkeni her zaman geçerli günlük dosyasının yolunu içerir.


## <a name="see-also"></a>Ayrıca bkz.

- [Günlük dosyaları başvurusu](log-files.md)

- [Destek Merkezi OneTrace](../../support/support-center-onetrace.md)

- [Destek Merkezi günlük dosyası Görüntüleyici](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
