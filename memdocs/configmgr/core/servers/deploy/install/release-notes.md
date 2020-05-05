---
title: Sürüm notları
titleSuffix: Configuration Manager
description: Üründe henüz düzeltilmeyen veya Microsoft Desteği Bilgi Bankası makalesinde kapsanan acil sorunlar hakkında bilgi edinin.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: da0b9fc5600a957680ad22e54edc176c892527a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718136"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager için sürüm notları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, ürün sürüm notları acil sorunlarla sınırlıdır. Bu sorunlar henüz üründe düzeltilmemiştir veya Microsoft Desteği Bilgi Bankası makalesinde ayrıntılı olarak açıklanmıştır.  

Özelliğe özgü belgeler, temel senaryoları etkileyen bilinen sorunlar hakkında bilgiler içerir.  

Bu makale, Configuration Manager geçerli dalı için sürüm notlarını içerir. Technical Preview dalı hakkında daha fazla bilgi için bkz. [Technical Preview](../../../get-started/technical-preview.md)  

Farklı sürümlerle sunulan yeni özellikler hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Sürüm 2002’deki yenilikler](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Sürüm 1910’daki yenilikler](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Sürüm 1906’daki yenilikler](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [Sürüm 1902’deki yenilikler](../../../plan-design/changes/whats-new-in-version-1902.md)

> [!Tip]  
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın:`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Kurulum ve yükseltme  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>İstemci otomatik yükseltmesi tüm istemciler için hemen gerçekleşir

<!-- 6040412 -->

*Sürüm 1910 için geçerlidir*

Siteniz [otomatik istemci yükseltmesini](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)kullanıyorsa, siteyi sürüm 1910 ' e güncelleştirdiğinizde tüm istemciler, site başarıyla güncelleştirildikten sonra anında yükseltilir. Tek Rastgele seçim, istemcilerin ilkeyi aldıkları zaman, varsayılan olarak her saat ' tir. Çok sayıda istemcisi olan büyük bir site için, bu davranış önemli miktarda ağ trafiği ve stres dağıtım noktası kullanabilir.

Etkilenen sürümler hakkında daha fazla bilgi için bkz. [geçerli Configuration Manager dalı Için istemci güncelleştirmesi, sürüm 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Pasif modda site sunucusu Configuration. mof ' i güncelleştirmez

<!-- 5787848 -->

*Sürüm 1910 için geçerlidir*

Siteniz [pasif modda bir site sunucusu](../configure/site-server-high-availability.md)içeriyorsa, siteyi güncelleştirdiğinizde envanter özelleştirmelerini kaybedebilirsiniz. Site sunucularının yükünü devretmek için site şu anda Configuration. mof ' i eşitlemez.

Bu sorunu geçici olarak çözmek için sitenin Configuration. mof ' i el ile yedekleyin ve geri yükleyin.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Sunucu 2019 üzerinde etki alanı işlev düzeyinde önkoşul uyarısını ayarla

<!-- 4904376 -->

*Sürüm 1906 için geçerlidir*

Windows Server 2019 çalıştıran etki alanı denetleyicileri içeren bir ortamda sürüm 1906 için güncelleştirme yüklenirken, etki alanı işlev düzeyi için önkoşul denetimi aşağıdaki uyarıyı döndürür:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Bu sorunu geçici olarak çözmek için, uyarıyı yoksayın.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>Azure AD Kullanıcı keşfi ve koleksiyon grubu eşitleme, site genişletmesinden sonra çalışmıyor

<!-- 4797313 -->
*Sürüm 1906 için geçerlidir*

Aşağıdaki özelliklerden birini yapılandırdıktan sonra:

- Kullanıcı grubu bulmayı Azure Active Directory
- Koleksiyon üyeliği sonuçlarını Azure Active Directory gruplarıyla eşitler

Bir tek başına birincil siteyi merkezi yönetim sitesi içeren bir hiyerarşiye genişletirseniz, SMS_AZUREAD_DISCOVERY_AGENT. log dosyasında şu hatayı görürsünüz:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Bu sorunu geçici olarak çözmek için, Azure AD 'de uygulama kaydıyla ilişkili anahtarı yenileyin. Daha fazla bilgi için bkz. [gizli anahtarı yenileme](../configure/azure-services-wizard.md#bkmk_renew).

## <a name="role-based-administration"></a>Rol tabanlı yönetim

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Belirli klasörler için güvenlik kapsamları, CA 'lardan birincil sitelere çoğaltılmaz
<!--6306759-->
*Sürüm 1910 için geçerlidir*

Sürüm 1910 ' e yükselttikten sonra, Kullanıcı koleksiyonlarında ve cihaz koleksiyonlarında bulunan [Klasörler için güvenlik KAPSAMLARı](../configure/configure-role-based-administration.md#bkmk_config-folder) CA 'lardan birincil sitelere çoğaltılmaz.

## <a name="application-management"></a>Uygulama yönetimi

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Microsoft Edge, sürüm 77 ve üzeri dağıtımı sırasında PowerShell hatası için sertifika alınamıyor
<!--5769384-->
*Uygulama hedefi: Configuration Manager sürüm 1910*

Configuration Manager konsolunu dilin Isveççe, Macarca veya Japonca olan bir IŞLETIM sisteminde çalıştırıyorsanız, Microsoft Edge, sürüm 77 ve üstünü dağıttığınızda aşağıdaki hatayı alırsınız:

`Unable to get certificate for Powershell`

Bu hata, bir `scripts` klasör Isveççe, Macarca veya Japonca `AdminConsole\bin` diller için dizin altında bulunmadığından oluşur. Betikler klasörü bu işletim sistemi dillerinde yerelleştirilir.

Bu sorunu geçici olarak çözmek için `scripts` `AdminConsole\bin` dizinde adlı bir klasör oluşturun. Yerelleştirilmiş klasörünüzdeki dosyaları yeni oluşturulan `scripts` klasöre kopyalayın. Dosyalar kopyalandıktan sonra Microsoft Edge, sürüm 77 ve üstünü dağıtın.

## <a name="os-deployment"></a>İşletim sistemi dağıtımı

### <a name="task-sequences-cant-run-over-cmg"></a>Görev dizileri CMG üzerinden çalıştırılamaz

*Uygulama hedefi: Configuration Manager sürüm 2002*

Bir bulut yönetimi ağ geçidi (CMG) aracılığıyla iletişim kuran bir cihazda görev dizilerinin üzerinde çalışacağı iki örnek vardır:

- Siteyi gelişmiş HTTP için yapılandırırsınız ve yönetim noktası HTTP 'dir.<!-- 6358851 -->

    Bu sorunu geçici olarak çözmek için, HTTPS için yönetim noktasını yapılandırın.

- İstemciyi, kimlik doğrulaması için bir toplu kayıt belirteciyle yükleyip kaydettiniz.<!-- 6377921 -->

    Bu sorunu geçici olarak çözmek için aşağıdaki kimlik doğrulama yöntemlerinden birini kullanın:

  - Cihazı iç ağa ön kaydetme
  - Cihazı istemci kimlik doğrulama sertifikasıyla yapılandırma
  - Cihazı Azure AD 'ye ekleme

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Pasif site sunucusu yükseltildikten sonra, varsayılan önyükleme görüntüsü paketleri hala önceki etkin sunucuda paket kaynağına sahip olur

<!--3453224, SCCMDocs-pr issue 3097-->
*Uygulama hedefi: Configuration Manager sürüm 1810*

Pasif modda (sunucu B) bir site sunucunuz varsa, onu etkin olarak yükselttiğinizde, varsayılan önyükleme görüntülerinin içerik konumu daha önce etkin olan sunucuya (sunucu A) başvurmaya devam eder. Sunucu A 'nın bir donanım hatası varsa, varsayılan önyükleme görüntülerini güncelleştiremez veya değiştiremezsiniz.

Bu sorun için geçici çözüm yoktur.

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="security-roles-are-missing-for-phased-deployments"></a>Aşamalı dağıtımlar için güvenlik rolleri eksik

<!--3479337, SCCMDocs-pr issue 3095-->
*Uygulama hedefi: Configuration Manager sürümler 1810, 1902*

Yerleşik güvenlik rolü **Dağıtım Yöneticisi Işletim sistemi** [aşamalı dağıtımlar](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)için izinlere sahiptir. Şu rollerin bu izinleri yoktur:  

- **Uygulama Yöneticisi**  
- **Uygulama Dağıtım Yöneticisi**  
- **Yazılım Güncelleştirme Yöneticisi**  

**Uygulama yazarı** rolü, aşamalı dağıtımlar için bazı izinlere sahip gibi görünebilir, ancak dağıtım oluşturmamalıdır.

Bu rollere sahip bir Kullanıcı, aşamalı dağıtım oluşturma Sihirbazı 'nı başlatabilir ve bir uygulama veya yazılım güncelleştirmesi için aşamalı dağıtımlar görebilir. Sihirbaz tamamlanamazlar veya var olan bir dağıtımda herhangi bir değişiklik yapamaz.

Bu sorunu geçici olarak çözmek için özel bir güvenlik rolü oluşturun. Mevcut bir güvenlik rolünü kopyalayın ve **aşamalı dağıtım** nesne sınıfına aşağıdaki izinleri ekleyin:

- Oluştur  
- Sil  
- Değiştir  
- Okuma  

Daha fazla bilgi için bkz. [özel güvenlik rolleri oluşturma](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Dağıtılmış görünümler için donanım envanteri kullanıyorsanız, masaüstü analizine ekleyemezsiniz

<!-- 4950335 -->
*Uygulama hedefi: güncelleştirme paketi ile Configuration Manager sürüm 1902 ve sürüm 1906*

Bir hiyerarşiniz varsa ve herhangi bir site çoğaltma bağlantısı üzerinde [Dağıtılmış görünümler](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) için **donanım envanteri** site verilerini etkinleştirirseniz, Configuration Manager ' de masaüstü Analizi bağlantısını yapılandırdıktan sonra, M365UploadWorker. log dosyasında şu hatayı görürsünüz:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Bu sorunu geçici olarak çözmek için, her site çoğaltma bağlantısında dağıtılmış görünümler için **donanım envanteri** site verilerini devre dışı bırakın.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>Koleksiyonlar kaldırılırken konsol beklenmedik şekilde kapanıyor

<!-- 4749443 -->
*Uygulama hedefi: güncelleştirme paketi ile Configuration Manager sürüm 1902*

Siteyi [Masaüstü](../../../../desktop-analytics/connect-configmgr.md)analizine bağlandıktan sonra, **Masaüstü analiziyle eşitlenmek üzere belirli koleksiyonlar seçebilirsiniz**. Bir koleksiyonu kaldırır ve değişiklikleri uygularsanız, hemen yeni bir koleksiyon eklemek işlenmeyen bir özel duruma neden olur. Konsol beklenmedik şekilde kapanır.

Bu sorunu geçici olarak çözmek için, bir koleksiyonu kaldırdığınızda, Özellikler penceresini kapatmak için **Tamam** ' ı seçin. Ardından, **Masaüstü Analizi bağlantı** sekmesine yeni bir koleksiyon eklemek için özellikleri tekrar açın.

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>Pilot durum kutucuğu bazı cihazları ' tanımsız ' olarak gösteriyor

<!-- 4547783 -->
*Uygulama hedefi: güncelleştirme paketi ile Configuration Manager sürüm 1902*

Pilot dağıtım durumunuzu izlemek için Configuration Manager konsolunu kullandığınızda, bu dağıtım planı için Windows 'un hedef sürümünde güncel olan pilot cihazlar pilot durum kutucuğunda **tanımsız** olarak gösterilir.  

Bu **tanımsız** cihazlar, o dağıtım planına ait hedef işletim sistemi **sürümü ile güncel** değildir. Başka bir eylem gerekmez.

## <a name="cloud-services"></a>Bulut hizmetleri

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>ABD kamu bulutunda Azure hizmeti genel bulut olarak gösteriliyor

<!-- 6036748 -->

*Sürüm 1910 için geçerlidir*

Azure hizmetine bir bağlantı oluşturur ve **Azure ortamını** kamu bulutuna ayarlarsanız bağlantının özellikleri, ortamı Azure genel bulutu olarak gösterir. Bu sorun, konsolda yalnızca bir görüntüleme sorunudur ve hizmet, kamu bulutunda. Yapılandırmayı onaylamak için, site veritabanında aşağıdaki SQL sorgusunu çalıştırın:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

Kamu Bulutu için, bu sorgunun `2` sonucu belirli bir kiracıya yöneliktir.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>TLS 1,2 için etkinleştirilen bir bulut yönetimi ağ geçidiyle içerik indirilemiyor

<!-- 5771680 -->

*Sürüm 1906, 1910 erken güncelleştirme halkası için geçerlidir*

Bulut yönetimi ağ geçidini (CMG) **bulut dağıtım noktası olarak çalışır ve Azure Storage 'dan içerik sunabilir** ve **TLS 1,2 ' i zorlayabiliyorsanız**, içerik indirmelerinin başarısız olduğunu görebilirsiniz.

Aşağıdaki hatalar, istemcideki DataTransferService. log dosyasında gösterilmektedir:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Aşağıdaki hatalar sunucuda CMGContentService. log dosyasında gösterilmektedir:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Bu soruna geçici bir çözüm olarak:

- Siteyi 20 Aralık 2019 tarihinde yayınlanan Küresel olarak kullanılabilir 1910 sürümüne güncelleştirin. (Daha önce 1910 erken güncelleştirme halkasını güncelleştirdiyseniz, kullanılabilir olduğunda bu yapıya güncelleştirmeniz gerekir.)

- Alternatif olarak, geleneksel bir [bulut dağıtım noktası](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)kullanın. Bu rol TLS 1,2 ' i zorlamaz, ancak TLS 1,2 gerektiren istemcilerle uyumludur.

## <a name="protection"></a>Koruma

### <a name="bitlocker-management-appears-in-version-1906"></a>1906 sürümünde BitLocker Yönetimi görünür

*Sürüm 1906 için geçerlidir*

<!-- 5984688 -->

21 Kasım 2019 ' den sonra, sürüm 1902 veya daha önceki sürümden 1906 sürümüne güncelleştirirseniz BitLocker yönetim özelliği açılır ve kullanılabilir olur. Bu özellik 1910 sürümünden itibaren isteğe bağlı bir özelliktir. Sürüm 1906 ' de desteklenmez. Sürüm 1906 ' de kullanmayı denerseniz beklenmedik sonuçlarla karşılaşabilirsiniz. Özelliği kullanmıyorsanız, hiçbir etkisi yoktur.

[BitLocker yönetim özelliğini](../../../../protect/plan-design/bitlocker-management.md)kullanmak için 1910 sürümüne güncelleştirin.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
