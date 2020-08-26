---
title: Ürün ve lisanslama hakkında SSS
titleSuffix: Configuration Manager
description: Configuration Manager için ortak ürün ve lisans sorularının yanıtlarını bulun.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f249c4ad981c289be33d364dcb4f5b8635faecb
ms.sourcegitcommit: e43e6e83e3b38137ceebc6d299eacd94a925db85
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88895901"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Configuration Manager dalları ve lisanslama hakkında sık sorulan sorular

*Uygulama hedefi: Configuration Manager (geçerli dal) & System Center Configuration Manager (uzun süreli bakım dalı)*

Bu SSS, Microsoft Toplu Lisanslama programları aracılığıyla kullanılabilen Configuration Manager geçerli dalı ve uzun süreli bakım dalı (LTSB) sürümleriyle ilgili genel lisanslama sorularını ele alır. Bu makale bilgilendirme amaçlıdır. Configuration Manager lisanslamayı kapsayan herhangi bir belgenin yerini almaz veya değiştirmez. Daha fazla bilgi için [Ürün koşullarına](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53)bakın. Ürün koşulları, toplu lisanslama 'de tüm Microsoft ürünleri için kullanım koşulları 'nı anlatmaktadır.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a> Geçerli dal nedir?

Geçerli dal, etkin bir hizmet modeli sağlayan Configuration Manager üretime yönelik olarak hazırlanmakta olan bir yapı. Bu hizmet modeli Windows 10 ' da deneyim gibidir. Bu yaklaşım, bir Cloud temposunda 'a taşınan ve daha hızlı yenilik yapın etmek isteyen müşterileri destekler. Geçerli dal bakım modeliyle yeni özellikler ve işlevler almaya devam edersiniz. Bu nedenle, yalnızca Configuration Manager lisanslarda etkin yazılım güvencesi olan veya eşdeğer abonelik haklarıyla olan müşteriler, geçerli Configuration Manager dalını yükleyip kullanabilir.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a> Uzun süreli bakım dalı (LTSB) nedir?  

LTSB, Configuration Manager üretime hazırlamış bir derleme. Yazılım Güvencesi veya eşdeğer abonelik haklarının sona erme süresini aşan müşterilere yöneliktir. LTSB, geçerli dala kıyasla [işlevselliği düşürür](introduction-to-the-ltsb.md#features-that-arent-available). Yazılım Güvencesi veya eşdeğer abonelik haklarının son kullanım süresini aşan müşterilerin geçerli Configuration Manager dalını kaldırması gerekir. Configuration Manager için kalıcı lisans hakları olan müşteriler, süresi dolma sırasında geçerli olan Configuration Manager sürümünün LTSB derlemesini yükleyip kullanabilir.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a>*Kısaltmalar ve* *L&sa* , Configuration Manager açısından ne anlama geliyor?

Hem **yazılım güvencesi** (SA) hem de **Lisans ve yazılım güvencesi** (L&sa), Configuration Manager kullanma hakları veren lisans seçeneklerdir. SA, bir müşterinin önceki bir anlaşmadan SA kapsamını yenileyen bir seçenektir. L&SA, müşterinin yeni bir lisans ve SA kapsamı satın aldığı bir seçenektir.

- **Yazılım güvencesi (SA)**: müşteriler, Configuration Manager geçerli dal seçeneğini yüklemek ve kullanmak için Configuration Manager lisanslarında veya eşdeğer abonelik HAKLARıYLA etkin sa 'ya sahip olmalıdır.

  SA, bazı Microsoft ürünleri için isteğe bağlı olsa da, geçerli dalı Configuration Manager kullanma haklarını almanın tek yolu, SA *veya eşdeğer abonelik haklarına*sahiptir. Daha fazla bilgi için bkz. [yazılım GÜVENCESI SSS](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Microsoft lisans ve yazılım güvencesi (L&sa)**: müşteriler, Configuration Manager için yeni lisanslar satın alarak, L&sa (LISANS ve sa kapsamı) almalıdır.

  - SA, geçerli dalı kullanma hakkı verir.

  - SA 'nın süresi dolarsa ve hala Configuration Manager lisansınız varsa, geçerli dalı artık kullanamazsınız. Daha fazla bilgi için bkz. [SA 'nın süresi dolarsa ve L&SA, ne edinebilirim?](#bkmk_sa-expires)

Lisans teklifleri hakkında daha fazla bilgi için bkz. [ürün koşulları](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64) [satın alma](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) ve lisanslama yolları.  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a>*Eşdeğer abonelikler*nelerdir?

Eşdeğer abonelikler [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) veya [Microsoft 365 Kurumsal](https://www.microsoft.com/microsoft-365/enterprise)gibi programlara başvurur. Başkaları olabilir, ancak bu programlar en sık kullanılan programlardır. Microsoft Toplu Lisanslama Ürün Koşulları, bu programları Yönetim Lisansı eşdeğer lisanslar olarak ifade eder.

Configuration Manager aşağıdaki planlara dahil edilir:

- Intune kullanıcı aboneliği lisansı (USL)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F3 (eski adıyla F1 Microsoft 365)

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager [Microsoft 365 iş](https://www.microsoft.com/microsoft-365/business) planına dahil değildir.

### <a name="what-changes-with-licensing-for-co-management-in-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Manager 'da ortak yönetim için lisanslamayla ilgili değişiklikler nelerdir?

<!-- 7202432 -->

Ortak Yönetim Lisansı, Yazılım Güvencesine sahip müşterilerin kullanıcılara bireysel Intune lisansları satın alıp atamak zorunda kalmadan Intune bılgısayar yönetim haklarına sahip Configuration Manager sağlar. Bu lisans, Microsoft Endpoint Manager ile Windows cihazlarını yönetmenizi kolaylaştırır.

- Ortak yönetim için Intune 'a kaydolmamış Configuration Manager tarafından zaten yönetilen cihazların, tek başına Intune ile yönetilen bir bılgısayarla neredeyse aynı haklara sahip olması gerekir. Bu cihazda Windows 'u sıfırlarsanız, Windows Autopilot ile sağlayamazsınız. Autopilot tam bir Intune lisansı gerektirir.

- Bir Windows 10 cihazını Intune 'a başka yollarla kaydederseniz, bunun yine de tam bir Intune lisansı gerekir. Örneğin, bir cihaz sağlamak için Autopilot kullandığınızda veya bir Kullanıcı self servis kaydını el ile yapar.

- Mevcut Configuration Manager yönetilen cihazların, Kullanıcı etkileşimi olmadan ortak yönetim için Intune 'a kaydedilmesi için, ortak yönetim, Windows 10 otomatik kaydı adlı bir Azure Active Directory (Azure AD) özelliği kullanır. Ortak yönetimiyle otomatik kayıt, hem Azure AD Premium (AADP1) hem de Intune için lisanslar gerektirir. 1 Aralık 2019 ' den itibaren, bu senaryo için ayrı ayrı Intune lisansları atamanız gerekmez. Microsoft Uç Nokta Yöneticisi artık ortak yönetim için Intune lisanslarını içerir. Ayrı AADP1 lisanslama gereksinimi, bu senaryonun çalışması için aynı kalır. Diğer kayıt senaryoları için yine de Intune lisansları atamanız gerekir.

- İOS, Android veya macOS cihazlarını yönetmek için Intune 'u kullanmak istiyorsanız, tek başına bir Intune lisansı, Enterprise Mobility + Security (EMS) veya Microsoft 365 aracılığıyla uygun Intune aboneliğine ihtiyacınız vardır.

- Intune ile ilgili herhangi bir abonelik planınız yoksa, ortak yönetimi desteklemek için en az bir Intune lisansı satın almanız gerekir. Bu lisans, bir yöneticinin abonelik planını etkinleştirmesi ve Microsoft Endpoint Manager yönetim merkezine erişimi alması içindir.

- Microsoft 365 yerleşik [temel taşınabilirlik ve güvenliği](https://support.microsoft.com/office/capabilities-of-built-in-mobile-device-management-for-microsoft-365-a1da44e5-7475-4992-be91-9ccec25905b0)kullanıyorsanız, temel taşınabilirlik ve güvenlik tarafından yönetilen cihazlara sahip olan bir kullanıcı için yeni ortak yönetim lisansını kullanamazsınız. Kullanıcının Configuration Manager tarafından yönetilen cihaz için ortak yönetim lisansını kullanmak için aşağıdaki eylemlerden birini yapın:

  - Kullanıcıya tam bir Intune lisansı atayın ve cihazlarını Intune aracılığıyla yönetin.
  - Temel taşınabilirlik ve güvenlik aygıtlarından cihazların kaydını kaldırın.

- Daha önce System Center Configuration Manager sahip olduğunuz lisanslama, Microsoft uç nokta Configuration Manager için de geçerlidir. Yeni bir site yüklüyorsanız, mevcut ürün anahtarlarını kullanın.

|Özellik | Ortak Yönetim Lisansı | Tam Intune lisansı |
|---------|---------|---------|
|Windows 10 kaydı|Evet (yalnızca var olan ConfigMgr tarafından yönetilen cihazlar için)|Evet|
|iOS, Android, macOS kaydı|Hayır|Evet|
|Otomatik Pilot|Hayır|Evet|
|Mobil uygulama yönetimi (MAM)|Hayır|Evet|
|Koşullu erişim<br>(ek AADP1 gerekir)|Evet|Evet|
|Cihaz profilleri|Evet|Evet|
|Yazılım güncelleştirme yönetimi|Evet|Evet|
|Envanter|Evet|Evet|
|Uygulama yönetimi|Evet|Evet|
|Uzaktan tam/seçmeli silme|Evet|Evet|
|Uzaktan yardım<br>(TeamViewer lisansı gereklidir)|Evet|Evet|
|Masaüstü Analizi<br>(Windows Abonelik lisansları gereklidir|Evet|Yok|
|Kiracı ekleme|Evet|Yok|
|Uç nokta analizi|Evet|Evet|

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Ortak yönetim önkoşulları](../../comanage/overview.md#prerequisites)
- [Windows Autopilot gereksinimleri](/windows/deployment/windows-autopilot/windows-autopilot-requirements)
- [Masaüstü Analizi önkoşulları](../../desktop-analytics/overview.md#prerequisites)
- [Kiracı iliştirme önkoşulları](../../tenant-attach/device-sync-actions.md#prerequisites)
- [Endpoint Analytics lisanslama önkoşulları](../../../analytics/overview.md#licensing-prerequisites)
- [Intune ile koşullu erişim kullanma](../../../intune/protect/conditional-access.md#use-conditional-access-with-intune)
- [TeamViewer önkoşulları](../../../intune/remote-actions/teamviewer-support.md#prerequisites)

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a> Enterprise Mobility + Security ve bu süre doldum, şimdi ne yapmam gerekir?  

EMS, geçerli dalı ve uzun süreli hizmet dalı Configuration Manager kullanma hakkı verir. Bu hakların süreleri dolduğunda, her iki dalı kullanma haklarınız yoktur ve kaldırması gerekir.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a> SA 'nın süresi dolarsa ve L&SA, ne edinebilirim?

SA 'nın, 1 Ekim 2016 ' den sonra süresi dolmuşsa, altında San&elde ettiğiniz programa bağlı olarak, LTSB 'yi kullanmak için kalıcı bir lisans tutabilirsiniz. Şu anda geçerli dalı kullanıyorsanız, onu kaldırmanız ve ardından LTSB 'yi kurmanız gerekir. Geçerli daldan LTSB 'ye geçiş veya dönüştürme desteği yoktur.

SA 'nız 1 Ekim 2016 ' den önce dolmuşsa ve Configuration Manager için kalıcı bir lisans elde ediyorsanız, sürekli kullanım için tek seçeneğiniz System Center 2012 R2 Configuration Manager ve kullanılabilir hizmet paketlerini yüklemek ve kullanmak içindir. SA 'nın süresi dolmuşsa geçerli dalı kaldırmanız ve ürünün önceki sürümünü yeniden yüklemeniz gerekir. Güncel dalı Configuration Manager önceki Configuration Manager sürümüne geçirme veya bu sürümlere düşürme desteği yoktur.

System Center Endpoint Protection kullanıyorsanız ve SA 'nın süresi dolarsa, kaldırmanız gerekir. System Center Endpoint Protection, *L (Lisans)* hakları ve kalıcı haklar gerektirmez.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a> Geçerli dala "sahip" misiniz?

Hayır. Etkin SA 'yı kullandığınızda geçerli dalı kullanma lisansına sahipsiniz. Örneğin, *l&sa*ile *sa* süresi dolmuşsa, geçerli dalı kullanma haklarını Içermeyen yalnızca *l (Lisans)* haklarına sahip olursunuz. L 'niz kalıcı haklar sağlıyorsa, geçerli dalın yerine LTSB Configuration Manager kullanabilirsiniz. SA 'nız 1 Ekim 2016 ' den önce dolmuşsa, System Center 2012 R2 Configuration Manager de kullanabilirsiniz.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a> SA olmadan tek başına Configuration Manager satın alabilir miyim?

Hayır. Configuration Manager kullanma haklarını almanın tek yolu, SA ile veya eşdeğer bir abonelikle lisans alma yöntemidir. Geliştirme ve test amaçları için Configuration Manager sunulur, ancak üretim kullanımı değil, MSDN gibi geliştirici programları vardır.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> Test veya geliştirme için üretim dışı bir ortam açık bir lisans gerektiriyor mu?

<!-- SCCMDocs#1848 -->

- Üretim ortamınız olarak aynı anki dal yazılımını kullanıyorsanız açık bir lisansa sahip olmanız gerekir. Belirli lisans sözleşmenizin birden fazla ortamda birden çok örneği kapsamadığını öğrenmek için hesap ekibinize başvurun.

- MSDN gibi bazı geliştirici programları, geliştirme ve test için Configuration Manager gibi ürünler sunar, ancak üretim kullanımı değildir.

- Geçici bir ortam için [değerlendirme sürümünü](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) 180 gün boyunca kullanabilirsiniz.

- Laboratuvar ortamında, [Technical Preview dalını](../get-started/technical-preview.md)kullanabilirsiniz. Technical Preview, geçerli Dalla aynı işlevselliğe sahiptir, ancak ölçek ve desteklenen platformlar açısından bazı sınırlamalar içerir.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> Configuration Manager konsolunda herhangi bir güncelleştirmeyi yüklemek için haklara sahip mıyım?

Etkin *sa*'nız varsa haklarınız vardır.

Etkin SA yoksa, geçerli dalı kaldırın ve ardından Configuration Manager LTSB ' yi yükleme. LTSB, Configuration Manager artımlı sürümleri için güncelleştirmeleri almaz, ancak destek yaşam döngüsüne göre güvenlik güncelleştirmelerini alır.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a> Bir bulut çözüm sağlayıcısı (CSP) aracılığıyla EMS veya Microsoft 365 satın aldım, Configuration Manager kullanma haklarım var mı?

Evet, EMS lisansı kapsamındaki istemcileri yönetmek için Configuration Manager kullanma haklarınız vardır. İlk olarak [değerlendirme yazılımını](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)indirin ve yükleyin. Ardından lisans anahtarını almak için Microsoft Desteği başvurun.<!--issue472--> Microsoft Desteği ile konuşurken iç Makale No 4033838 ' ye başvurmalarını isteyin.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a> Aboneliğimin bitiş tarihi bir SA sona erme tarihi ile aynı mı?

*Sa* veya aboneliğiniz etkinse, geçerli Configuration Manager dalı için kullanım haklarına sahip olursunuz. Etkin bir abonelik, etkin *sa*'ya sahip olma, ancak kalıcı olmayan *"L" (Lisans)* ile eşdeğerdir. Aboneliğiniz bittikten sonra, geçerli dalı kaldırın. Şu anda LTSB 'yi kullanma haklarınız yok.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a> Configuration Manager ile birlikte sunulan SQL teknolojisiyle ilişkili kullanım hakları nelerdir?

Configuration Manager SQL Server teknolojisini içerir. Microsoft 'un bu ürüne yönelik lisans koşulları, SQL Server teknolojiden yalnızca Configuration Manager bileşenleri desteklemek için kullanılmasına olanak tanır. SQL Server istemci erişim lisansları Bu kullanım için gerekli değildir.

Configuration Manager ile SQL özellikleri için onaylanan kullanım hakları şunlardır:

- Site veritabanı rolü
- Yazılım güncelleştirme noktası rolü için Windows Server Update Services (WSUS)
- Raporlama noktası rolü için SQL Server Reporting Services (SSRS)
- Veri ambarı hizmet noktası rolü
- Yönetim noktası rolleri için veritabanı çoğaltmaları

Configuration Manager eklenen SQL Server Lisansı, Configuration Manager için bir veritabanı barındırmak üzere yüklediğiniz her bir SQL Server örneğini destekler. Ancak, bu lisansı kullandığınızda yalnızca yukarıdaki listedeki Configuration Manager veritabanları bu SQL Server çalıştırılabilir. Ek Microsoft veya üçüncü taraf ürün için bir veritabanı SQL Server paylaşıyorsa, bu SQL Server örneği için ayrı lisansa sahip olmanız gerekir.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a> Şirket içi mobil cihaz yönetimi (MDM) bir Intune aboneliği gerektiriyor mu?

1806 ve önceki sürümlerde, şirket içi MDM kullanmaya başlamak için bir Microsoft Intune aboneliğine sahip olmanız gerekir. Abonelik yalnızca cihazların lisansını izlemek için gereklidir ve cihazların yönetim bilgilerini yönetmek ya da depolamak için kullanılmaz. Tüm yönetim verileri kuruluşunuzda şirket içi Configuration Manager altyapısı kullanılarak depolanır.  

Sürüm 1810 ' den başlayarak, yeni şirket içi MDM dağıtımları için bir Intune bağlantısı artık gerekli değildir.<!--3607730, fka 1359124--> Kuruluşunuz hala bu özelliği kullanmak için Intune lisansları istiyor. Daha fazla bilgi için bkz. [Intune destek blog gönderisi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).
