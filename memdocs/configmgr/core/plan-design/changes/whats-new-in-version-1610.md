---
title: Yeni sürüm 1610
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1610 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d23880def99fd12bffe83efffe9768f94481d07e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993565"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Sürüm 1610 ' deki yenilikler&#39;Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli dalın Configuration Manager güncelleştirme 1610, daha önce yüklü olan ve 1511, 1602 veya 1606 sürümlerini çalıştıran sitelerde konsol içi bir güncelleştirme olarak sunulmaktadır.


> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanmanız gerekir.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Sitelere güncelleştirme yükleme](../../servers/manage/updates.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Aşağıdaki bölümlerde, Configuration Manager sürüm 1610 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Güncelleştirme yükleme durumunu konsol içi izleme  
Sürüm 1610 ' den başlayarak, bir güncelleştirme paketi yüklediğinizde ve yüklemeyi konsolda izlerken, yeni bir aşama vardır: **yükleme sonrası**. Bu aşama, önemli hizmetleri yeniden başlatma ve çoğaltma izlemenin başlatılması gibi görevlerin durumunu içerir. (Bu aşama, siteniz sürüm 1610 ' e güncellene kadar konsolda kullanılamaz.) Güncelleştirme yükleme durumu hakkında daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yükleme](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>İstemcileri otomatik yükseltmeden hariç tut
Windows istemcilerinin, istemci yazılımının yeni sürümleriyle yükseltilmesinden de dışlayabilirsiniz. Bunu yapmak için, istemci bilgisayarlarını, yükseltmenin dışında belirtilen bir koleksiyona dahil edersiniz. Dışlanan koleksiyondaki istemciler, istemci yazılımını güncelleştirme isteklerini yoksayar.  Daha fazla bilgi için bkz. [Windows istemcilerini yükseltmelerden dışlama](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Sınır grupları geliştirmeleri
Sürüm 1610, sınır gruplarında önemli değişiklikleri ve bunların dağıtım noktalarıyla nasıl çalıştığını tanıtır. Bu değişiklikler, içerik altyapınızın tasarımını basitleştirecek ve istemciler içerik kaynak konumları olarak ek dağıtım noktalarında arama yapmak için nasıl ve ne zaman geri dönüş konusunda daha fazla denetim sağlar. Bu, hem şirket içi hem de bulut tabanlı dağıtım noktaları içerir.
Bu geliştirmeler, bildiğiniz kavramların ve davranışların yerini alır (dağıtım noktalarını hızlı veya yavaş olacak şekilde yapılandırmak gibi). Yeni modelin ayarlanması ve bakımını yapmak daha kolay olmalıdır. Bu değişiklikler Ayrıca, sınır gruplarıyla ilişkilendirdiğiniz diğer site sistem rollerini iyileştirecek sonraki değişiklikler için ön hazırlıkları başlattık ' i de oluşturur.

Sürüm 1610 ' e güncelleştirdiğinizde güncelleştirme, geçerli sınır grubu yapılandırmalarınızı yeni modele uyacak şekilde dönüştürür, böylece bu değişiklikler mevcut içerik dağıtım yapılandırmalarınızı rahatsız etmez.

Daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>İstemcilere içerik dağıtımı için eş önbellek
Sürüm 1610 ' den başlayarak, istemci **Eş Önbelleği** uzak konumlardaki istemcilerin içerik dağıtımını yönetmenize yardımcı olur. Eş önbellek, istemcilerin diğer istemcilerle doğrudan yerel Önbelleklerinden içerik paylaşmasına yönelik yerleşik bir Configuration Manager çözümüdür.

Bir koleksiyona eş önbelleği etkinleştiren istemci ayarlarını dağıttıktan sonra, bu koleksiyonun üyeleri aynı sınır grubundaki diğer istemciler için eş içerik kaynağı olarak davranabilir.

Ortamınızdaki eş önbellek içerik kaynaklarının kullanımını anlamak için yeni **Istemci veri kaynakları** panosunu de kullanabilirsiniz.

> [!TIP]  
> Sürüm 1610 ile eş önbellek ve Istemci veri kaynakları panosu, yayın öncesi özelliklerdir. Bunları etkinleştirmek için bkz. [güncelleştirmelerden yayın öncesi özellikleri kullanma](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Daha fazla bilgi için bkz. [Configuration Manager istemcileri Için eş önbellek](../hierarchy/client-peer-cache.md)ve [istemci veri kaynakları panosu](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Birden çok paylaşılan dağıtım noktasını aynı anda geçirme
Artık, 50 paylaşılan dağıtım noktasının aynı anda yeniden atanması için dağıtım noktasını paralel olarak Configuration Manager işleme sahip olacak şekilde **yeniden atama** seçeneğini kullanabilirsiniz. Bu sürümden önce, yeniden atanmış dağıtım noktaları tek seferde işlendi. Daha fazla bilgi için, [aynı anda birden fazla paylaşılan dağıtım noktasını geçirme](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time)bölümüne bakın.

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Internet tabanlı istemcileri yönetmek için bulut yönetimi ağ geçidi

Bulut yönetimi ağ geçidi, Internet 'teki Configuration Manager istemcilerini yönetmek için basit bir yol sağlar. Microsoft Azure dağıtılan ve bir Azure aboneliği gerektiren bulut yönetimi ağ geçidi hizmeti, bulut yönetimi ağ geçidi bağlantı noktası adlı yeni bir rol kullanarak şirket içi Configuration Manager altyapınıza bağlanır. Tamamen dağıtıldıktan ve yapılandırıldıktan sonra istemciler, iç özel ağa veya Internet 'e bağlı olup olmadıklarına bakılmaksızın şirket içi Configuration Manager site sistem rolleriyle ve bulut tabanlı dağıtım noktalarıyla iletişim kurabilir. Bulut yönetimi ağ geçidi 'nin Internet tabanlı istemci yönetimiyle nasıl Karşılaştırıldığı hakkında daha fazla bilgi edinmek ve bkz. [İnternet 'te Istemcileri yönetme](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Windows 10 Sürüm Yükseltme İlkesindeki Geliştirmeler
Bu sürümde, bu ilke türü için aşağıdaki iyileştirmeler yapılmıştır:

- Artık, Microsoft Intune kayıtlı Windows 10 bilgisayarlarının yanı sıra Configuration Manager istemcisini çalıştıran Windows 10 bilgisayarlarıyla sürüm yükseltme ilkesini kullanabilirsiniz.
- Windows 10 Professional 'dan donanımınızla uyumlu olan sihirbazda herhangi bir platforma yükseltebilirsiniz.

## <a name="manage-hardware-identifiers"></a>Donanım tanımlayıcılarını yönetme
Artık Configuration Manager, PXE önyüklemesi ve istemci kaydı amacıyla yoksayması gereken donanım kimliklerinin bir listesini sağlayabilirsiniz. Bu sorunun ele sağlanmasına yardımcı olan iki yaygın sorun vardır:

1. Surface Pro 3 gibi birçok cihaz, yerleşik bir Ethernet bağlantı noktası içermez. Bir USB-Ethernet bağdaştırıcısı, genellikle bir işletim sistemi dağıtma amacıyla kablolu bağlantı kurmak için kullanılır. Bununla birlikte, maliyet ve genel kullanılabilirlik nedeniyle genellikle paylaşılan bağdaştırıcılardır. Bu bağdaştırıcının MAC adresi cihazı tanımlamak için kullanıldığından, bağdaştırıcının yeniden kullanılması her dağıtım arasında ek yönetici eylemleri olmadan sorunlu olur. Şimdi Configuration Manager sürüm 1610 ' de, bu senaryoda kolayca yeniden kullanılabilmesi için bu bağdaştırıcının MAC adresini dışlayabilirsiniz.
2. SMBıOS KIMLIĞININ benzersiz bir donanım tanımlayıcısı olması gerekir, ancak bazı özel donanım cihazları yinelenen kimliklerle oluşturulmuştur. Bu sorun, yalnızca açıklanan USB-Ethernet bağdaştırıcı senaryosu kadar yaygın olmayabilir, ancak dışlanan donanım kimlikleri listesini kullanarak bu sorunu ele alabilirsiniz.

Ayrıntılar için bkz. [yinelenen donanım tanımlayıcılarını yönetme](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Iş için Windows Mağazası 'nda Configuration Manager ile tümleştirme geliştirmeleri
Bu sürümdeki değişiklikler:
- Daha önce Iş için Windows Mağazası 'ndan ücretsiz uygulamalar dağıtabilirsiniz. Artık Configuration Manager, ücretli çevrimiçi lisanslanmış uygulamalar (yalnızca Intune 'A kayıtlı cihazlar için) dağıtılmasını da desteklemektedir.
- Artık Iş için Windows Mağazası ve Configuration Manager arasında anında eşitleme başlatabilirsiniz.
- Artık Azure Active Directory aldığınız istemci gizli anahtarını değiştirebilirsiniz.
- Mağaza aboneliğini silebilirsiniz.

Ayrıntılar için bkz. [iş Için Windows Mağazası 'ndan uygulamaları Configuration Manager yönetme](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Intune 'a kayıtlı cihazlar için ilke eşitleme
Artık, Intune 'a kayıtlı bir cihaz için Configuration Manager konsolundan bir ilke eşitlemesi isteğinde bulunabilir ve bunun yerine cihazın kendisindeki Şirket Portalı uygulamasından eşitleme istemeniz gerekir. Eşitleme isteği durum bilgileri, **uzak eşitleme durumu**adlı cihaz görünümlerinde yeni bir sütun olarak kullanılabilir. Bilgiler ayrıca her bir cihaz için **Özellikler** iletişim kutusunun bulma verileri bölümünde de bulunur.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Uyumluluk ayarlarını kullanarak Windows Defender ayarlarını yapılandırma
Artık Configuration Manager konsolundaki yapılandırma öğelerini kullanarak Intune 'a kayıtlı Windows 10 bilgisayarlarında Windows Defender istemci ayarlarını yapılandırabilirsiniz.
Ayrıntılar için, [Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları için yapılandırma öğeleri oluşturma](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)konusunun **Windows Defender** bölümüne bakın.



## <a name="general-improvements-to-software-center"></a>Software Center 'da genel iyileştirmeler
- Kullanıcılar artık yazılım merkezi 'nden ve Uygulama Kataloğu uygulama isteyebilirler.
- Kullanıcıların hangi yazılımların yeni ve ilgili olduğunu anlamasına yardımcı olacak geliştirmeler.

## <a name="new-columns-in-device-collection-views"></a>Cihaz koleksiyonu görünümlerindeki yeni sütunlar
Artık cihaz koleksiyonu görünümlerinde **IMEI** ve **seri numarası** (iOS cihazları için) sütunlarını görüntüleyebilirsiniz.

## <a name="customizable-branding-for-software-center-dialogs"></a>Yazılım Merkezi iletişimleri için özelleştirilebilir marka
Yazılım Merkezi için özel marka Configuration Manager sürüm 1602 ' de kullanıma sunulmuştur. Sürüm 1610 ' de, bu marka artık Yazılım Merkezi kullanıcılarına daha tutarlı bir deneyim sunmak için ilişkili tüm iletişim kutularına genişletilir.

Yazılım Merkezi için özel marka aşağıdaki kurallara göre uygulanır:

- Uygulama Kataloğu web sitesi noktası site sunucusu rolü yüklü değilse, Yazılım Merkezi, **Bilgisayar Aracısı** Istemci ayarı **Yazılım Merkezi 'nde görüntülenen kuruluş adı**' nda belirtilen kuruluş adını görüntüler. Yönergeler için bkz. [istemci ayarlarını yapılandırma](../../clients/deploy/configure-client-settings.md).

- Uygulama Kataloğu web sitesi noktası site sunucusu rolü yüklüyse, Yazılım Merkezi Uygulama Kataloğu web sitesi noktası site sunucusu rolü özelliklerinde belirtilen kuruluş adını ve rengini görüntüler. Daha fazla bilgi için bkz. [Uygulama Kataloğu web sitesi noktası Için yapılandırma seçenekleri](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

- Microsoft Intune bir abonelik yapılandırılıp Configuration Manager ortamına bağlanırsa, Yazılım Merkezi, Intune Abonelik özelliklerinde belirtilen kuruluş adını, rengini ve Şirket logosunu görüntüler.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Gerekli uygulama ve yazılım güncelleştirme dağıtımları için zorlama yetkisiz kullanım süresi
Bazı durumlarda, gerekli uygulama dağıtımlarını veya yazılım güncelleştirmelerini ayarladığınız tüm son tarihlerden sonra yüklemek için kullanıcılara daha fazla zaman vermek isteyebilirsiniz. Örneğin, bir bilgisayar uzun bir süre kapatılmış ve çok sayıda uygulama veya güncelleştirme dağıtımı yüklemesi gerektiğinde bu gerekli olabilir. Örneğin, bir son kullanıcı tatilden yeni döndürülürse, süresi geçmiş uygulama dağıtımları yüklenirken uzun süredir beklemek zorunda kalabilir. Bu sorunu çözmeye yardımcı olmak için artık Configuration Manager istemci ayarlarını bir koleksiyona dağıtarak bir zorlama yetkisiz kullanım süresi tanımlayabilirsiniz. 

Yetkisiz kullanım süresini yapılandırmak için aşağıdaki işlemleri gerçekleştirin:
1. İstemci ayarları ' nın **Bilgisayar Aracısı** sayfasında, **dağıtım son tarihi (saat) sonra** , **1** ila **120** saat arasında bir değere sahip zorlama için yeni özellik yetkisiz kullanım süresini yapılandırın.
2. Yeni bir gerekli uygulama dağıtımında veya var olan bir dağıtımın özelliklerinde, **zamanlama** sayfasında, **istemci ayarlarında tanımlanan yetkisiz kullanım süresine kadar bu dağıtımın uygulanmasını, kullanıcı tercihlerine göre geciktir**onay kutusunu seçin. Bu onay kutusunun seçili olduğu ve istemci ayarını dağıttığınız cihazlara hedeflenmiş tüm dağıtımlar, zorlama yetkisiz kullanım süresini kullanır.

Bir zorlama yetkisiz kullanım süresi yapılandırır ve onay kutusunu seçerseniz, uygulama yükleme son tarihine ulaşıldığında, kullanıcının bu yetkisiz kullanım süresine yapılandırdığı ilk iş dışı penceresine yüklenir. Ancak, Kullanıcı hala yazılım merkezini açabilir ve uygulamayı istedikleri zaman yükleyebilir. Yetkisiz kullanım süresi dolduktan sonra, zorlama süresi dolan dağıtımlar için normal davranışa geri döner. Yazılım güncelleştirmeleri dağıtım sihirbazına, otomatik dağıtım kuralları sihirbazına ve özellikler sayfalarına benzer seçenekler eklenmiştir.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Gerekli yazılımlarla ilgili iletişim kutularındaki gelişmiş işlevler
Bir kullanıcı gerekli yazılımları aldığında, **yeniden anımsat ve bana anımsat:** ayarı aşağıdaki açılan değer listesinden seçim yapabilir: 
- **Daha sonra**. Bildirimlerin, Istemci Aracısı ayarlarında yapılandırılan bildirim ayarlarına bağlı olarak zamanlandığını belirtir.
- **Sabit zaman**. Bildirimin seçili zamandan sonra yeniden görüntülenmek üzere zamanlanacağını belirtir (örneğin, 30 dakika).

![Istemci Aracısı ayarlarındaki bilgisayar Aracısı sayfası](media/client-notification-settings.png)

Maksimum erteleme süresi, Istemci Aracısı ayarlarında yapılandırılan bildirim değerlerine göre belirlenir. Örneğin, **dağıtım son tarihi 24 saatten fazlaysa, bilgisayar Aracısı sayfasında kullanıcıları her (saat)** , 10 saat için de uyar ve son tarihten önce 24 saatten fazla olursa Kullanıcı, en fazla 10 saat boyunca bir erteleme seçeneği görür. Son Tarih yaklaşırsa, dağıtım zaman çizelgesinin her bileşeni için ilgili Istemci Aracısı ayarları ile tutarlı, daha az seçenek mevcuttur.

Ek olarak, bir işletim sistemini dağıtan görev dizisi gibi yüksek riskli bir dağıtım için Kullanıcı bildirim deneyimi artık daha zorlayıcıdır. Geçici bir görev çubuğu bildirimi yerine, kullanıcıya kritik yazılım bakımının gerekli olduğu her bildirimde bulunulduğundan, kullanıcının bilgisayarında aşağıdaki gibi bir iletişim kutusu görüntülenir:

![Gerekli yazılım iletişim kutusu](media/client-toast-notification.png)


Daha fazla bilgi için:
- [Yüksek riskli dağıtımları yönetme ayarları](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [İstemci ayarlarını yapılandırma](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Yazılım güncelleştirmeleri panosu
Kuruluşunuzdaki cihazların geçerli uyumluluk durumunu görüntülemek için yeni yazılım güncelleştirmeleri panosunu kullanın ve hangi cihazların risk altında olduğunu görmek için verileri hızlıca çözümleyin. Panoyu görüntülemek için **izleme**  >  **genel bakış**  >  **güvenlik**  >  **yazılım güncelleştirmeleri panosuna**gidin.

Ayrıntılar için bkz. [yazılım güncelleştirmelerini izleme](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Uygulama isteği işlemindeki geliştirmeler
Bir uygulamayı yükleme için onayladıktan sonra, Configuration Manager konsolunda **Reddet** ' e tıklayarak isteği reddetmeyi tercih edebilirsiniz. Daha önce, bu düğme onay sonrasında gri renkte.

Bu eylem, uygulamanın herhangi bir cihazdan kaldırılmasına neden olmaz. Ancak, kullanıcıların yazılım merkezi 'nden uygulamanın yeni kopyalarını yüklemesini durdurur.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Otomatik dağıtım kurallarında içerik boyutuna göre filtrele
Artık otomatik dağıtım kurallarında yazılım güncelleştirmeleri için içerik boyutuna filtre uygulayabilirsiniz. Örneğin, yalnızca 2 MB 'tan küçük yazılım güncelleştirmelerini indirmek için, **Içerik boyutu (KB)** filtresini **< 2048**olarak ayarlayabilirsiniz. Bu filtrenin kullanılması, büyük yazılım güncelleştirmelerinin otomatik olarak indirilmesini engeller, bu da ağ bant genişliği sınırlı olduğunda Basitleştirilmiş Windows alt düzey bakımını daha iyi destekler. Ayrıntılar için bkz.
- [Alt düzey Işletim sistemlerinde Configuration Manager ve Basitleştirilmiş Windows Bakımı](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056)
- [Yazılım güncelleştirmelerini otomatik dağıtma](../../../sum/deploy-use/automatically-deploy-software-updates.md)

**Içerik boyutu (KB)** alanını yapılandırmak için aşağıdakilerden birini yapın:
- Bir otomatik dağıtım kuralı oluşturduğunuzda, otomatik dağıtım kuralı oluşturma Sihirbazı ' nda, **yazılım güncelleştirmeleri** sayfasına gidin.
- Mevcut bir otomatik dağıtım kuralının Özellikler bölümünde, **yazılım güncelleştirmeleri** sekmesine gidin.

## <a name="office-365-client-management-dashboard"></a>Office 365 Istemci yönetimi panosu
Office 365 Istemci yönetimi panosu artık Configuration Manager konsolunda kullanılabilir. Panoyu görüntülemek için, **yazılım kitaplığı**  >  **'na genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.

Panoda aşağıdakiler için grafikler görüntülenir:

- Office 365 istemcilerinin sayısı
- Office 365 istemci sürümleri
- Office 365 istemci dilleri
- Office 365 istemci kanalları

Ayrıntılar için bkz. [Microsoft 365 Apps güncelleştirmelerini yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS’tan UEFI’ye dönüştürmeyi yönetmek için görev sırası adımları
Artık, **Bilgisayarı yeniden Başlat** adımının UEFI 'ye geçiş için sabit SÜRÜCÜDEKI bir FAT32 bölümünü hazırlayabilmesi Için TSUEFIDrive adlı yeni bir değişkenle bir işletim sistemi dağıtımı görev dizisini özelleştirebilirsiniz. Aşağıdaki yordam, BIOS 'TAN UEFı 'ye dönüştürme için sabit sürücüyü hazırlamak üzere görev dizisi adımlarını nasıl oluşturabileceğiniz hakkında bir örnek sağlar. Ayrıntılar için bkz.  [BIOS 'TAN UEFI dönüştürmeyi yönetmeye yönelik görev dizisi adımları](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Görev dizisi adımındaki geliştirmeler: ConfigMgr Istemcisini yakalamaya hazırlama  
ConfigMgr Istemcisini hazırla adımı yalnızca anahtar bilgilerini kaldırmak yerine Configuration Manager istemcisini tamamen kaldırır. Görev dizisi yakalanan işletim sistemi görüntüsünü dağıttığında, her seferinde yeni bir Configuration Manager istemci yükler. Ayrıntılar için bkz. [görev dizisi adımları](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Intune uyumluluk ilkesi grafikleri
Artık Configuration Manager konsolundaki **izleme** çalışma alanı altındaki yeni grafikleri kullanarak, cihazların genel uyumluluğuna ve uyumsuzluk için en önemli nedenler hakkında hızlı bir bakış edinebilirsiniz. Bu kategorideki cihazların listesine gitmek için grafikteki bir bölüme tıklayabilirsiniz. Ayrıntılar için bkz. [Uyumluluk Ilkesini izleme](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>İOS ve Android cihazlarını korumak için karma uygulamalar için gevleme tümleştirmesi
Microsoft, cihazlarda kötü amaçlı yazılım, riskli uygulamalar ve daha fazlasını algılayarak iOS ve Android mobil cihazlarını korumak için gereken mobil tehdit koruması çözümünü tümleştiriyor. GEVME çözümü, yapılandırılabilir olan tehdit düzeyini belirlemenize yardımcı olur. Configuration Manager ' de bir uyumluluk ilkesi kuralı oluşturabilirsiniz. Bu durumda cihaz uyumluluğunu, riske göre risk değerlendirmesine göre belirleyebilirsiniz. Koşullu erişim ilkelerini kullanarak, cihaz uyumluluk durumuna göre şirket kaynaklarına erişime izin verebilir veya erişimi reddedebilirsiniz.

Uyumsuz iOS cihazlarının kullanıcılarına kaydolması istenir. Lookout for Work uygulamasını cihazlara yüklemek, uygulamayı etkinleştirmek ve şirket verilerine erişim kazanmak için Lookout for Work uygulamada bildirilen tehditleri düzeltmek için bu uygulamalar gerekecektir.


## <a name="new-compliance-settings-for-configuration-items"></a>Yapılandırma öğeleri için yeni uyumluluk ayarları
Çeşitli cihaz platformları için yapılandırma öğelerinde kullanabileceğiniz birçok yeni ayar vardır. Bunlar, bir tek başına yapılandırmada Microsoft Intune daha önce var olan ve Intune 'U Configuration Manager ile kullandığınızda kullanılabilir olan ayarlardır.
Ayrıntılar için bkz. [Configuration Manager istemcisi olmadan yönetilen cihazlar Için yapılandırma öğeleri](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Android cihazları için yeni ayarlar
#### <a name="password-settings"></a>Parola ayarları
- **Parola geçmişini anımsa**
- **Parmak izi ile kilit açmaya izin ver**

#### <a name="security-settings"></a>Güvenlik ayarları
- **Depolama kartlarında şifreleme iste**
- **Ekran yakalamaya izin ver**
- **Tanılama verilerinin gönderimine izin ver**

#### <a name="browser-settings"></a>Tarayıcı ayarları
- **Web tarayıcısına izin ver**
- **Otomatik doldurmaya izin ver**
- **Açılır pencere engelleyicisine izin ver**
- **Tanımlama bilgilerine izin ver**
- **Etkin betik yazmaya izin ver**

#### <a name="app-settings"></a>Uygulama ayarları
- **Google Play mağazasına izin ver**

#### <a name="device-capability-settings"></a>Cihaz özelliği ayarları
- **Çıkarılabilir depolama birimine izin ver**
- **Wi-Fi İnternet paylaşımına izin ver**
- **Coğrafi konuma izin ver**
- **NFC'ye izin ver**
- **Bluetooth'a izin ver**
- **Ses dolaşımına izin ver**
- **Veri dolaşımına izin ver**
- **SMS/MMS iletilerine izin ver**
- **Sesli yardıma izin ver**
- **Sesli aramaya izin ver**
- **Kopyalama ve yapıştırmaya izin ver**

### <a name="new-settings-for-ios-devices"></a>İOS cihazları için yeni ayarlar
#### <a name="password-settings"></a>Parola ayarları
- **Parolada gerekli karmaşık karakter sayısı**
- **Basit parolalara izin ver**
- **Parola gerekmeden önce etkin olmama süresi (dakika)**
- **Parola geçmişini anımsa**

### <a name="new-settings-for-mac-os-x-devices"></a>Mac OS X cihazları için yeni ayarlar
#### <a name="password-settings"></a>Parola ayarları
- **Parolada gerekli karmaşık karakter sayısı**
- **Basit parolalara izin ver**
- **Parola geçmişini anımsa**
- **Ekran koruyucu etkinleştirilmeden önce işlem yapılmadan geçen süre**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Windows 10 Masaüstü ve mobil cihazlar için yeni ayarlar
#### <a name="password-settings"></a>Parola ayarları
- **Minimum karakter kümesi sayısı**
- **Parola geçmişini anımsa**
- **Cihaz boş bir durumdan döndürüldüğünde parola iste**

#### <a name="security-settings"></a>Güvenlik ayarları
- **Cihazda şifrelemeyi gerektir**
- **Elle kayıt kaldırmaya izin ver**

#### <a name="device-capability-settings"></a>Cihaz özelliği ayarları
- **Hücresel veri üzerinden VPN'ye izin ver**
- **Hücresel veri üzerinden VPN dolaşımına izin ver**
- **Telefon sıfırlamaya izin ver**
- **USB bağlantısına izin ver**
- **Cortana’ya izin ver**
- **İşlem merkezi bildirimlerine izin ver**

### <a name="new-settings-for-windows-10-team-devices"></a>Windows 10 Team cihazları için yeni ayarlar
#### <a name="device-settings"></a>Cihaz ayarları
- **Azure Operasyonel İçgörüler'i etkinleştir**
- **Miracast kablosuz projektörü etkinleştir**
- **Karşılama ekranında görüntülenen toplantı bilgilerini seçin**
- **Kilit ekranı arka plan görüntüsü URL'si**

### <a name="new-settings-for-windows-81-devices"></a>Windows 8.1 cihazları için yeni ayarlar
#### <a name="applicability-settings"></a>Uygulanabilirlik ayarları
- **Tüm yapılandırmaları Windows 10'a uygula**

#### <a name="password-settings"></a>Parola ayarları
- **Gerekli parola türü**
- **Minimum karakter kümesi sayısı**
- **Minimum parola uzunluğu**
- **Cihaz silinmeden önce izin verilen yinelenen oturum açma hatası sayısı**
- **Ekran kapanmadan önce işlem yapılmadan geçen dakika sayısı**
- **Parola geçerlilik süresi (gün)**
- **Parola geçmişini anımsa**
- **Önceki parolaların yeniden kullanılmasını engelleme**
- **Resimli parolaya veya PIN’e izin ver**

#### <a name="browser-settings"></a>Tarayıcı ayarları
- **İntranet ağının otomatik algılanmasına izin ver**

### <a name="new-settings-for-windows-phone-81-devices"></a>Windows Phone 8,1 cihazları için yeni ayarlar
#### <a name="applicability-settings"></a>Uygulanabilirlik ayarları
- **Tüm yapılandırmaları Windows 10'a uygula**

#### <a name="password-settings"></a>Parola ayarları
- **Minimum karakter kümesi sayısı**
- **Basit parolalara izin ver**
- **Parola geçmişini anımsa**

#### <a name="device-capability-settings"></a>Cihaz özelliği ayarları
- **Ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmaya izin ver**
