---
title: Koşullu erişim senaryoları
titleSuffix: Microsoft Intune
description: Intune Koşullu erişimin cihaz tabanlı ve uygulama tabanlı koşullu erişim için yaygın olarak nasıl kullanıldığını öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52c8be7556fac2cf06d244fc8640a0ed7d173481
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992951"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Intune ile koşullu erişim kullanmanın yaygın yolları nelerdir?

Intune ile kullanılan iki tür koşullu erişim vardır: Cihaz tabanlı koşullu erişim ve uygulama tabanlı koşullu erişim. Kuruluşunuzda koşullu erişim uyumluluğunu sağlamak için ilgili uyumluluk ilkelerini yapılandırmanız gerekir. Koşullu erişim, Exchange 'e erişime izin verme veya erişimi engelleme, ağa erişimi denetleme veya bir mobil tehdit savunması çözümü ile tümleştirme gibi işlemleri yapmak için yaygın olarak kullanılır.
 
Bu makaledeki bilgiler, Intune mobil *cihaz* uyumluluk özelliklerini ve Intune mobil *uygulama* yönetimi (MAM) yeteneklerini nasıl kullanacağınızı anlamanıza yardımcı olabilir. 

> [!NOTE]
> Koşullu erişim, bir Azure Active Directory Premium lisansıyla birlikte sunulan bir Azure Active Directory özelliğidir. Intune, çözüme mobil cihaz uyumluluğu ve mobil uygulama yönetimi ekleyerek bu özelliği geliştirir. *Intune* 'Dan erişilen koşullu erişim düğümü, *Azure AD*'den erişilen aynı düğümdür.  

## <a name="device-based-conditional-access"></a>Cihaz tabanlı koşullu erişim

Intune ve Azure Active Directory, yalnızca yönetilen ve uyumlu cihazların e-postaya, Microsoft 365 hizmetlere, hizmet olarak yazılım (SaaS) uygulamalarına ve [Şirket içi uygulamalara](/azure/active-directory/active-directory-application-proxy-get-started)erişmesine emin olmak için birlikte çalışır. Ayrıca, Azure Active Directory ' de bir ilkeyi yalnızca, etki alanına katılmış bilgisayarları veya Intune 'a kaydedilen mobil cihazları yalnızca Microsoft 365 hizmetlerine erişmesi için ayarlayabilirsiniz.

Intune, cihazların uyumluluk durumunu değerlendiren cihaz uyumluluk ilkesi özellikleri sunar. Uyumluluk durumu, Kullanıcı şirket kaynaklarına erişmeye çalıştığında Azure Active Directory oluşturulan koşullu erişim ilkesini zorlamak için onu kullanan Azure Active Directory bildirilir.

Exchange Online ve diğer Microsoft 365 ürünleri için cihaz tabanlı koşullu erişim ilkeleri [Azure Portal](../fundamentals/what-is-intune.md)aracılığıyla yapılandırılır.

- [Azure Active Directory 'de koşullu erişim ile yönetilen cihazlar gerektirme](/azure/active-directory/conditional-access/require-managed-devices)hakkında daha fazla bilgi edinin.

- [Intune cihaz uyumluluğu](device-compliance-get-started.md) hakkında daha fazla bilgi edinin.

- [Azure Active Directory 'de koşullu erişim Ile desteklenen tarayıcılar](/azure/active-directory/conditional-access/technical-reference#supported-browsers)hakkında daha fazla bilgi edinin.

> [!NOTE]
> Android cihazlarda, SharePoint Online 'a cihaz tabanlı erişimi veya Exchange Online 'a tarayıcı tabanlı erişim 'i etkinleştirdiğinizde, kullanıcılar kayıtlı cihazda **tarayıcı erişimini etkinleştir** seçeneğini şu şekilde etkinleştirmelidir:
> 1. **Şirket Portalı uygulamasını**başlatın.
> 2. Üçlü noktalar (...) veya donanım menü düğmesinden **Ayarlar** sayfasına gidin.
> 3. **Tarayıcı Erişimini Etkinleştir** düğmesine basın. 
> 4. Chrome tarayıcısında Microsoft 365 oturumunuzu kapatın ve Chrome 'u yeniden başlatın.

### <a name="conditional-access-based-on-network-access-control"></a>Ağ erişim denetimine bağlı koşullu erişim

Intune, Intune kaydına ve cihaz uyumluluk durumuna göre erişim denetimleri sağlamak için Cisco ıSE, Aruba Clear Pass ve Citrix NetScaler gibi iş ortaklarıyla tümleştirilir.

Kullanıcılar, kullandıkları cihazın Intune cihaz uyumluluk ilkeleriyle yönetilip yönetilmediğine bağlı olarak şirket Wi-Fi veya VPN kaynaklarına erişim izni verebilir veya erişimi reddedilebilir.

- [Intune ile NAC tümleştirmesi](network-access-control-integrate.md) hakkında daha fazla bilgi edinin.

### <a name="conditional-access-based-on-device-risk"></a>Cihaz riskine bağlı olarak koşullu erişim

Intune; mobil cihazlardaki kötü amaçlı yazılımı, Truva atlarını ve diğer tehditleri algılamak için güvenlik çözümleri sağlayan Mobil Tehdit Savunması satıcılarıyla iş ortaklıkları kurar.

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Intune ve Mobil Tehdit Savunması Tümleştirmesi nasıl çalışır

Mobil cihazlarda Mobile Threat Defense Aracısı yüklüyse, mobil cihazın kendisinde bir tehdit bulunduğunda Aracı, uyumluluk durumu iletilerini Intune bildirimine geri gönderir.

Intune ve mobil tehdit savunması tümleştirmesi, cihaz riskine bağlı olarak koşullu erişim kararlarında bir faktör oynar.

- [Intune mobil tehdit savunması](mobile-threat-defense.md) hakkında daha fazla bilgi edinin.

### <a name="conditional-access-for-windows-pcs"></a>Windows Bilgisayarlar için koşullu erişim

Bilgisayarlar için koşullu erişim, mobil cihazlarda bulunanlara benzer yetenekler sağlar. Intune ile bilgisayarları yönetirken koşullu erişimi kullanma yollarınız hakkında konuşalım.

#### <a name="corporate-owned"></a>Şirkete ait

- **Karma Azure AD 'ye katılmış:** Bu seçenek genellikle bilgisayarlarını zaten AD Grup ilkeleri veya Configuration Manager ile yönetme konusunda makul ölçüde rahat olan kuruluşlar tarafından kullanılır.

- **Azure AD etki alanına katılmış ve Intune yönetimi:** Bu senaryo, bulutu ilk kez yapmak isteyen kuruluşlar içindir (yani, birincil olarak bulut hizmetleri 'ni kullanarak, şirket içi bir altyapının kullanımını azaltmaya yönelik bir hedefle birlikte) veya salt bulut (Şirket içi altyapı olmadan). Azure AD JOIN, karma bir ortamda çalışarak hem buluta hem de şirket içi uygulamalara ve kaynaklara erişimi etkinleştirir. Cihaz Azure AD 'ye katılır ve şirket kaynaklarına erişirken koşullu erişim ölçütü olarak kullanılabilecek Intune 'a kaydedilir.

#### <a name="bring-your-own-device-byod"></a>Kendi cihazını getir (KCG)

- **Çalışma alanına katılma ve Intune yönetimi:** Burada kullanıcı kişisel cihazlarına ve kurumsal kaynak ve hizmetlere erişebilir. Koşullu erişim ölçütlerini değerlendirmek için başka bir seçenek olan cihaz düzeyinde ilkeler almak üzere çalışma alanına katılma ve cihazları Intune MDM 'ye kaydetme kullanabilirsiniz.

[Azure Active Directory 'de cihaz yönetimi](/azure/active-directory/devices/overview)hakkında daha fazla bilgi edinin.

## <a name="app-based-conditional-access"></a>Uygulamaya bağlı koşullu erişim

Intune ve Azure Active Directory, kurumsal e-postaya veya diğer Microsoft 365 hizmetlerine yalnızca yönetilen uygulamaların erişebildiğinizden emin olmak için birlikte çalışır.

- [Intune ile uygulama tabanlı koşullu erişim hakkında](app-based-conditional-access-intune.md) daha fazla bilgi edinin.

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Şirket içi Exchange için Intune koşullu erişimi

Koşullu erişim, cihaz uyumluluk ilkelerine ve kayıt durumuna bağlı olarak **şirket içi Exchange**'e erişim izin vermek veya erişim engellemek için kullanılabilir. Koşullu erişim bir cihaz uyumluluk ilkesiyle birlikte kullandığınızda, yalnızca uyumlu cihazların şirket içi Exchange'e erişmesine izin verilir.

Koşullu erişimdeki gelişmiş ayarları aşağıdaki gibi daha ayrıntılı denetim için yapılandırabilirsiniz:

- Belirli platformlara izin verme veya bunları engelleme.

- Intune tarafından yönetilmeyen cihazları hemen engelleyin.

Cihaz uyumluluğu ve koşullu erişim ilkeleri uygulandığında, şirket için Exchange'e erişmek için kullanılan tüm cihazların uyumlu olup olmadığı denetlenir.

Cihazlar koşullar kümesini karşılamıyorsa, Son Kullanıcı cihazı kaydetme işlemi boyunca aygıtı uyumsuz hale getiren sorunu düzeltir.

> [!NOTE]
> Haziran 2020 ' den başlayarak Exchange Connector için destek kullanım dışıdır ve Exchange [karma modern kimlik doğrulaması](/office365/enterprise/hybrid-modern-auth-overview) (HMA) ile değiştirilmiştir. HMA kullanımı, Intune 'un Exchange bağlayıcısını kurulumunu ve kullanmasını gerektirmez. Bu değişiklik ile, aboneliğiniz ile bir Exchange Bağlayıcısı kullanmıyorsanız, Intune için Exchange bağlayıcısını yapılandırmak ve yönetmek için kullanılan Kullanıcı arabirimi Microsoft Endpoint Manager yönetim merkezinden kaldırılmıştır.
>
> Ortamınızda ayarlanmış bir Exchange Bağlayıcısı varsa, Intune kiracınız kullanım için desteklenir ve yapılandırmasını destekleyen Kullanıcı arabirimine erişime sahip olmaya devam edersiniz. Daha fazla bilgi için bkz. [Şirket Içi Exchange bağlayıcısını yüklemeye](../protect/exchange-connector-install.md) . Bağlayıcıyı kullanmaya devam edebilir veya HMA 'yı yapılandırabilir ve ardından bağlayıcınızı kaldırabilirsiniz.
>
> Karma modern kimlik doğrulaması, Intune için Exchange Connector tarafından daha önce sağlanan işlevselliği sağlar: bir cihaz kimliğini Exchange kaydıyla eşleme.  Bu eşleme artık, Intune 'da yaptığınız bir yapılandırmanın veya Intune bağlayıcısının Intune ve Exchange 'e köprü oluşturma gereksiniminin dışında gerçekleşir. HMA ile, ' Intune ' öğesine özgü yapılandırmayı (bağlayıcı) kullanma gereksinimi kaldırılmıştır.


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Intune rolü nedir?

Intune cihaz durumunu değerlendirir ve yönetir.

#### <a name="whats-the-exchange-server-role"></a>Exchange Server rolü nedir?

Exchange Server, cihazları karantinaya almak için API ve altyapı sağlar.

> [!IMPORTANT]
> Cihazın uyumluluk açısından değerlendirilebilmesi için, cihazı kullanan kullanıcıya bir uyumluluk profili ve Intune lisansı atanmış olması gerektiğini aklınızda bulundurun. Kullanıcıya hiçbir uyumluluk ilkesi dağıtılmadıysa, cihaz uyumlu olarak kabul edilir ve hiçbir erişim kısıtlaması uygulanmaz.

## <a name="next-steps"></a>Sonraki adımlar

[Azure Active Directory 'de koşullu erişimi yapılandırma](/azure/active-directory/active-directory-conditional-access-azure-portal)

[Uygulama tabanlı koşullu erişim ilkeleri ayarlama](app-based-conditional-access-intune-create.md)

[Şirket içi Exchange için koşullu erişim ilkesi oluşturma](conditional-access-exchange-create.md)