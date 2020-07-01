---
title: Sürüm 1606 ' de yeni
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1606 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 070c616ed8411bcd90b2d3edb12b04edd57241e1
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590482"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Sürüm 1606 ' deki yenilikler&#39;Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için güncelleştirme 1606, daha önce yüklü olan ve 1511 veya 1602 sürümlerini çalıştıran sitelerde konsol içi bir güncelleştirme olarak sunulmaktadır. Sürüm 1511, yeni Configuration Manager siteleri yüklemek için kullandığınız ilk temel sürümdür.
> [!TIP]  
> Aşağıdakiler hakkında daha fazla bilgi edinin:  
>   
> - [Yeni siteler yükleme](../../servers/deploy/install/prepare-to-install-sites.md) (1511 gibi bir temel sürüm kullanarak)  
> - [Güncelleştirmeleri sitelere yükleme](../../servers/manage/updates.md) (güncelleştirme 1602 veya 1606 gibi)  

 Aşağıdaki bölümlerde, Configuration Manager sürüm 1606 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Güncelleştirmeler ve bakım

### <a name="changes-for-the-updates-and-servicing-node"></a>Güncelleştirmeler ve bakım düğümü için değişiklikler
Configuration Manager konsolundaki güncelleştirmeler ve bakım düğümündeki değişiklikler aşağıda verilmiştir:
> [!NOTE]
> Sürüm 1606 ' i yükleyene kadar bu değişiklikler kullanılamaz.

- **Düğüm adı değişikliği:**

    **İzleme** çalışma alanında, **site bakım durumu** düğümü **güncelleştirmeler ve bakım durumu**olarak yeniden adlandırıldı.
- **Daha fazla yükleme durumu ayrıntıları:**

    Bir sitenin güncelleştirme yükleme durumunu görüntülediğinizde, konsol artık aşağıdaki eylemler için ayrı Ayrıntılar görüntüler:
    - **İndir** (Bu yalnızca hizmet bağlantı noktası site sistemi rolünün yüklü olduğu en üst katman sitesi için geçerlidir.)
    - **Çoğaltma**
    - **Önkoşul Denetimi**
    - **Yükleme**

  Ayrıca, daha fazla bilgi için hangi günlük dosyasını görüntüleyebileceği da dahil olmak üzere her bir adımla ilgili daha ayrıntılı bilgiler de mevcuttur.  
-   **Önkoşul başarısızlıklarını yeniden deneme için yeni seçenek:**

    Hem **Yönetim** hem de **izleme** çalışma alanlarında, **güncelleştirmeler ve bakım** düğümü, şeritte **Önkoşul uyarılarını yoksay**adlı yeni bir düğme içerir.

    Önkoşul uyarılarını yok say (güncelleştirmeler Sihirbazı 'ndan) seçeneğini kullanmadan güncelleştirmeleri yüklediğinizde ve bu güncelleştirme yüklemesi bir uyarı nedeniyle durursa, bundan sonra şeritten **Önkoşul uyarılarını yoksay** ' ı seçebilirsiniz. Bu, güncelleştirme yüklemesinin otomatik devamlılığını tetikler.  



- **Güncelleştirmelerin temizleyici görünümü:**

    **Güncelleştirmeler ve bakım** düğümünde, artık yalnızca en son yüklenen güncelleştirmeyi ve yükleyebileceğiniz yeni güncelleştirmeleri görürsünüz. Daha önce yüklenen güncelleştirmeleri görüntülemek için şeritte görüntülenen yeni **Geçmiş** düğmesine tıklayın.  

-   **Ön üretim için yeniden adlandırılan seçenek:**

    **Güncelleştirmeler ve bakım** düğümünde, **istemci seçenekleri** düğmesi artık **üretim öncesi istemcisini Yükselt**olarak adlandırılmaktadır.


###  <a name="pre-release-features"></a>Yayın öncesi özellikler
1606 ' den başlayarak, kullanımlarını seçmeden ve etkinleştirebilmeniz için önce Configuration Manager ' deki yayın öncesi özellikleri kullanma onayı sağlamanız gerekir. Daha fazla bilgi için bkz. [Güncelleştirmelerden yayın öncesi sürüm özelliklerini kullanma](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Yeni dağıtım noktası güncelleştirme davranışı
Güncelleştirme 1606, gelecekteki güncelleştirmeleri yüklerken dağıtım noktalarının kullanılabilirliğini artıran değişiklikler sunar.

Güncelleştirme 1606 yüklendikten sonra, standart ve çekme dağıtım noktası site sistemi rollerinin otomatik olarak yeniden yüklenmesini gerektiren bu sitede bir güncelleştirmeyi daha sonra yüklediğinizde, tüm dağıtım noktaları artık aynı anda güncelleştirme için çevrimdışı duruma geçmez. Bunun yerine, site sunucusu, güncelleştirmeyi belirli bir zamanda bir dağıtım noktaları alt kümesine dağıtmak için sitenin içerik dağıtım ayarlarını kullanır. Sonuç olarak, güncelleştirmeyi yüklemek için yalnızca bazı dağıtım noktaları çevrimdışı olur. Bu, henüz güncelleştirmeye başlamış olmayan veya güncelleştirmeyi tamamlamış olan dağıtım noktalarının çevrimiçi kalması ve istemcilere içerik sağlayabilmesi için izin verir.



## <a name="accessibility"></a><a name="accessibility"></a>Larınızdaki
Bir çalışma alanının farklı düğümleri arasında gezinmek için artık bir düğümün adının ilk harfini girebilirsiniz. Her tuş basma imleci bu harfle başlayan bir sonraki düğüme taşıtir. Ekran okuyucusu olan kullanıcılar için okuyucu bu düğümün adını okur. Erişilebilirlik seçenekleri hakkında daha fazla bilgi için bkz. [erişilebilirlik özellikleri](../../../core/understand/accessibility-features.md).

## <a name="administration"></a><a name="administration"></a>Yönetim
Configuration Manager konsolundaki yönetim değişiklikleri aşağıda verilmiştir:
### <a name="oms-connector"></a>OMS Bağlayıcısı

Artık, Configuration Manager Configuration Manager koleksiyon olarak [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/)olarak bağlanabilirsiniz. Bu, Configuration Manager dağıtımınızdan Koleksiyonlar gibi verileri OMS 'de görünür hale getirir. Daha fazla bilgi edinmek için bkz. [Configuration Manager verileri buradan Microsoft Operations Management Suite eşitleme](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

OMS Bağlayıcısı, yayın öncesi bir özelliktir. Etkinleştirmek için, bkz. [güncelleştirmelerden yayın öncesi özellikleri kullanma](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Istemci ayarlarında önbellek boyutu desteği

Artık, istemci bilgisayarlardaki önbellek klasörünün boyutunu Configuration Manager konsolundaki **Istemci ayarları** ile yapılandırabilirsiniz. Daha önce, istemci yazılımını yüklerken veya yeniden yüklerken yalnızca istemci önbellek boyutunu ayarlayabilirsiniz. Artık önbellek boyutunu istemci ayarı olarak belirtebilirsiniz (varsayılan veya özel) ve ardından istemci üzerindeki bir sonraki ilke güncelleştirmesiyle istemci yeniden yüklemesi gerekmeden bu ayarların uygulanmasını sağlayabilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager İstemcileri İçin İstemci Önbelleğini Yapılandırma](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Şirket içi mobil cihaz yönetimi

### <a name="support-for-multiple-device-management-points"></a>Birden çok cihaz yönetim noktası desteği

Şirket içi mobil cihaz yönetimi (MDM) artık, kayıtlı bir cihazı, kullanılabilir birden fazla cihaz yönetim noktasına sahip olacak şekilde otomatik olarak yapılandıran Windows 10 yıldönümü güncelleştirmesi 'nin yeni bir özelliğini desteklemektedir. Bu yetenek, cihazın normalde kullandığı bir cihaz yönetim noktasına geri dönmesine izin verir. Bu özellik yalnızca Windows 10 yıldönümü güncelleştirmesi yüklü olan bilgisayarlar ve cihazlar için geçerlidir.


## <a name="application-management"></a>Uygulama yönetimi

### <a name="manage-apps-from-the-windows-store-for-business"></a>İş İçin Windows Mağazası uygulamalarını yönetme

[İş Için Windows Mağazası](https://www.microsoft.com/business-store) , kuruluşunuz için tek tek veya toplu olarak Windows uygulamaları bulabileceğiniz ve satın alabileceğiniz yerdir. Mağazayı Configuration Manager 'e bağlayarak Configuration Manager satın aldığınız uygulamaların listesini eşitleyebilir, bunları Configuration Manager konsolunda görüntüleyebilir ve diğer uygulamalar gibi dağıtabilirsiniz.

Ayrıntılar için bkz. [iş Için Windows Mağazası 'ndan uygulamaları Configuration Manager yönetme](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Toplu satın alınan iOS uygulamalarını yönetme

Toplu satın alınan iOS uygulamalarını yönetmek ve bunları Configuration Manager ile dağıtmak için iş akışı geliştirilmiştir.


### <a name="software-center-user-interface"></a>Yazılım Merkezi kullanıcı arabirimi

Yazılım Merkezi kullanıcı arabirimi daha kolay bulma için kolaylaştırılmıştır.
*  **Yükleme durumu** ve **yüklü yazılım** sekmeleri tek bir **yükleme durumu** sekmesinde birleştirilmiştir.
*  **Güncelleştirmeler**, **Işletim sistemleri**ve **uygulamalar** üç ayrı sekmeye ayrılmıştır.
* Aynı anda birden çok güncelleştirme yüklenmek üzere seçilebilir veya tümünü **yükleme**öğesine tıklayarak tüm güncelleştirmeler bir kez yüklenebilir.

### <a name="content-status-links"></a>İçerik durumu bağlantıları
Bir uygulama veya paketin özelliklerinde, sizi bu nesnenin durumuna götüren bir bağlantı vardır.

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Office 365 istemci Aracısı 'nı yönetmek için istemci ayarı
Artık Office 365 istemci aracısını yönetmek için bir Configuration Manager istemci ayarı kullanabilirsiniz. Office 365 güncelleştirmelerini ayarlayıp dağıttıktan sonra, Configuration Manager istemci Aracısı Office 365 istemci aracısında çalışarak bir dağıtım noktasından Office 365 güncelleştirmelerini indirip yükler.

Ayrıntılar için bkz. [Configuration Manager Ile Office 365 ProPlus güncelleştirmelerini yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>İstemcileri el ile yeni bir yazılım güncelleştirme noktasına değiştirme
Artık, etkin yazılım güncelleştirme noktasıyla ilgili sorunlar olduğunda Configuration Manager istemcilerinin yeni bir yazılım güncelleştirme noktasına geçiş yapmanızı sağlayan bir seçeneği etkinleştirebilirsiniz. Etkinleştirildiğinde, istemciler bir sonraki taramada başka bir yazılım güncelleştirme noktası arar.

Ayrıntılar için bkz. [Configuration Manager yazılım güncelleştirmelerini planlayın](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Windows 10 istemcileri için yazılım güncelleştirme yüklemesinden sonra yeniden başlatma seçenekleri
Yeniden başlatma gerektiren bir yazılım güncelleştirmesi Configuration Manager kullanılarak dağıtıldığında ve bir bilgisayara yüklendiğinde, bekleyen bir yeniden başlatma zamanlanır. Yeniden başlatma iletişim kutusu da görüntülenir. Configuration Manager sürüm 1606 ' den başlayarak, Configuration Manager yazılım güncelleştirmesi için bekleyen bir yeniden başlatma olduğunda **güncelleştirme ve yeniden başlatma** ve **güncelleştirme ve kapatmayla** ilgili seçenekler kullanılabilir. Bunlar Windows 10 bilgisayarlarının Windows güç seçeneklerinde bulunur. Bu seçeneklerden birini kullandıktan sonra, bilgisayar yeniden başlatıldıktan sonra yeniden başlatma iletişim kutusu görüntülenmez.

Ayrıntılar için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Bir istemci yazılım güncelleştirmelerini yükledikten ve yeniden başlatıldıktan sonra yazılım güncelleştirmeleri uyumluluk taramasını çalıştırın
Artık bir istemci yazılım güncelleştirmelerini yükledikten ve yeniden başlattıktan hemen sonra bir uyumluluk taraması çalıştırabilirsiniz. Bunu bir dağıtıma ayarlamak için, yazılım güncelleştirmelerini dağıtma Sihirbazı 'nın **Kullanıcı deneyimi** sayfasında, **Bu dağıtımdaki herhangi bir güncelleştirme sistemin yeniden başlatılmasını gerektiriyorsa, yeniden başlatmadan sonra güncelleştirmeleri dağıtım değerlendirme döngüsünü Çalıştır '** ı seçin. Bu, istemcinin yeniden başlatıldıktan sonra geçerli hale gelen ek yazılım güncelleştirmelerini denetlemesini ve aynı bakım penceresi sırasında bunları yükleyip uyumlu hale gelmesini sağlar. Ayrıntılar için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../../sum/deploy-use/automatically-deploy-software-updates.md) veya [yazılım güncelleştirmelerini el ile dağıtma](../../../sum/deploy-use/manually-deploy-software-updates.md).

## <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Görev dizisi adımındaki geliştirmeler: yazılım güncelleştirmelerini yükler
Yeni bir ayar, **önbelleğe alınmış tarama sonuçlarından yazılım güncelleştirmelerini değerlendir**, önbelleğe alınmış tarama sonuçlarını kullanmak yerine yazılım güncelleştirmeleri için tam tarama yapmanız için size bir seçenek sunar. Ayrıntılar için bkz. [görev dizisi adımları](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Ayrıca, yeni bir görev dizisi değişkeni olan **SMSTSSoftwareUpdateScanTimeout**, kullanılabilir. Bu değişken, yazılım güncelleştirmelerini yükler görev dizisi adımı sırasında yazılım güncelleştirmeleri taraması için zaman aşımını denetlemenizi sağlar. Varsayılan değer 30 dakikadır. Ayrıntılar için bkz. [görev dizisi yerleşik değişkenleri](../../../osd/understand/task-sequence-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>OSDPreserveDriveLetter görev dizisi değişkeni kullanım dışı bırakıldı
OSDPreserveDriveLetter görev dizisi değişkeni kullanım dışı bırakıldı. Configuration Manager sürüm 1606 ' den başlayarak, Windows Kurulumu kullanılacak en iyi sürücü harfini belirler (genellikle C:) bir işletim sistemi dağıtımı sırasında varsayılan olarak.

Ayrıntılar için bkz. [görev dizisi yerleşik değişkenleri](../../../osd/understand/task-sequence-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>PXE 'yi destekleyen dağıtım noktaları için RamDisk TFTP pencere boyutunu özelleştirme
Artık PXE 'yi destekleyen dağıtım noktaları için RamDisk pencere boyutunu özelleştirebilirsiniz. Ağınızı özelleştirdiyseniz, pencere boyutu çok büyük olduğundan önyükleme görüntüsü indirmenin bir zaman aşımı hatası vererek başarısız olmasına neden olabilir. RamDisk Önemsiz Dosya Aktarım Protokolü (TFTP) pencere boyutu özelleştirmesi, PXE 'yi kullanarak belirli ağ gereksinimlerinizi karşılayacak şekilde TFTP trafiğini iyileştirmenize olanak tanır.

Ayrıntılar için bkz. [Configuration Manager ile işletim sistemi dağıtımları için site sistemi rollerini hazırlama](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Uyumluluk ayarları

### <a name="smart-lock-setting-for-android-devices"></a>Android cihazları için Akıllı Kilit ayarı
Android ve Samsung KNOX Standard yapılandırma öğesine Akıllı Kilit yeni bir ayar, **Izin verme ve diğer güven aracılarına**eklenmiştir.

Bu ayar uyumlu Android cihazlarda Akıllı Kilit özelliğini denetlemenize olanak tanır. "Güven aracıları" olarak da bilinen bu telefon özelliği, cihaz güvenilir bir konumdayken cihaz kilidi ekran parolasını devre dışı bırakmanıza veya atlamanıza izin verir. Örneğin, güvenilir bir konum belirli bir Bluetooth cihazına bağlandığında veya bir NFC etiketinin yakınında olabilir. Bu ayarı kullanıcıların Akıllı Kilitleme’yi yapılandırmasını önlemek için kullanabilirsiniz.


## <a name="device-configuration-and-protection"></a>Cihaz yapılandırması ve koruması

### <a name="product-name-changes"></a>Ürün adı değişiklikleri

* İş için Microsoft Passport artık **iş Için Windows Hello**olarak bilinir.
* Kurumsal veri koruma artık **Windows Bilgi Koruması** olarak adlandırılıyor.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Iş için Windows Hello (Iş için Passport) dağıtımı

Artık Configuration Manager istemcisi tarafından yönetilen etki alanına katılmış Windows 10 cihazlarına Iş için Windows Hello ilkeleri dağıtabilirsiniz.

Configuration Manager konsolu bu değişiklikleri yansıtacak şekilde güncelleştirilmiştir.

### <a name="ios-activation-lock"></a>iOS Etkinleştirme Kilidi
Configuration Manager, iOS 7,1 ve üzeri cihazlar için iPhone 'Umu bul uygulamasının bir özelliği olan iOS Etkinleştirme Kilidi yönetmenize yardımcı olabilir. Etkinleştirme Kilidi etkinleştirildiğinde, aşağıdakilerin yapılabilmesi için önce kullanıcının Apple Kimliği ve parolasının girilmesi gerekir:
* İPhone 'Umu bul seçeneğini devre dışı bırakın.
* Cihazı silin.
* Cihazı yeniden etkinleştirin.

Configuration Manager, Etkinleştirme Kilidi’ni yönetmenize iki şekilde yardımcı olabilir:

- Denetimli cihazlarda Etkinleştirme Kilidi’ni etkinleştirme.
- Denetimli cihazlarda Etkinleştirme Kilidi’ni atlama.


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Gelişmiş Tehdit Koruması

Endpoint Protection, Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP) yönetmenize ve izlemenize yardımcı olabilir. Microsoft Defender ATP, kuruluşların ağlarında gelişmiş saldırıları algılamasına, araştırmasına ve yanıt vermesine yardımcı olacak yeni bir hizmettir. Configuration Manager ilkeleri, Windows 10, sürüm 1607 (derleme 14328) veya sonraki sürümleri çalıştıran yönetilen bilgisayarları eklemenize ve izlemenize yardımcı olabilir.

Ayrıntılar için bkz. [Microsoft Defender Gelişmiş tehdit koruması](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Cihaz kategorileri
Microsoft Intune ile Configuration Manager kullanırken cihazları cihaz koleksiyonlarına otomatik olarak yerleştirmek için kullanılabilecek cihaz kategorileri oluşturabilirsiniz. Daha sonra kullanıcıların Intune 'A cihaz kaydettiğinde bir cihaz kategorisi seçmesi gerekir. Ayrıca, Configuration Manager konsolundan bir cihazın kategorisini de değiştirebilirsiniz.

Ayrıntılar için bkz. [Configuration Manager cihazları otomatik olarak koleksiyonlar halinde kategorilere ayırma](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>IMEı veya iOS seri numaralarıyla cihazları önceden bildirin

Şirketin sahip olduğu cihazları, uluslararası istasyon mobil ekipman kimliği (ıMEı) numaralarını veya iOS seri numaralarını içeri aktararak tanımlayabilirsiniz. Cihaz ıMEı numaralarını içeren bir virgülle ayrılmış değerler (. csv) dosyasını karşıya yükleyebilir veya cihaz bilgilerini el ile girebilirsiniz. İçeri aktarılan bilgiler, cihaz listelerinde "Şirket" olarak kayıt yapan cihazların sahipliğini ayarlar. Hizmete erişen her kullanıcı için bir Intune lisansı hala gereklidir.

### <a name="on-premises-health-attestation-service-communication"></a>Şirket içi sistem durumu kanıtlama hizmeti iletişimi

Artık, Internet erişimi olmayan bilgisayarların Cihaz Sistem Durumu Kanıtlama (DHA) bildirebilmesi için yalnızca şirket içi altyapıyı kullanarak Windows 10 bilgisayarları için durum kanıtlama Hizmetleri izlemesini etkinleştirebilirsiniz.

Ayrıntılar için bkz. [Configuration Manager Için durum kanıtlama](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Uzaktan Denetim
Kullanıcılarınızın uzak denetim oturumunda paylaşılan panodan içerik aktarmadan önce dosya aktarımlarını kabul etme veya reddetme olanağı sağlar. Kullanıcıların, oturum başına yalnızca bir kez izin vermesi gerekir ve Görüntüleyici, dosya aktarımına devam etmek için kendilerine izin verme olanağına sahip değildir. Bu yeni ayarı **Yönetim** çalışma alanında bulabilirsiniz. **Istemci ayarları**' na gidin ve **varsayılan ayarlar**' da, **Uzak Araçlar** panelini açın.
