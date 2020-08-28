---
title: Intune uygulama koruma İlkesi dağıtımı sorunlarını giderme
description: Intune uygulama koruma ilkelerini dağıtırken karşılaşabileceğiniz sorunları nasıl giderebileceğinizi açıklar.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.subservice: apps
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 9aceb4d2b8b0b67af297fa5d15cdf66ae04a83f4
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996631"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Intune 'da uygulama koruma İlkesi dağıtımı sorunlarını giderme

## <a name="introduction"></a>Giriş

Bu makale, Microsoft Intune ' de uygulama koruma ilkeleri uyguladığınızda sorunları anlamanıza ve gidermenize yardımcı olur. Durumunuza uygulanan bölümleri izleyin.

## <a name="basic-steps"></a>Temel adımlar

### <a name="collect-initial-data"></a>İlk verileri topla

Sorun gidermeye başlamadan önce, sorunu daha iyi anlamanıza ve çözüm bulma süresini azaltmanıza yardımcı olabilecek bazı temel bilgileri toplamanız gerekir.

Aşağıdaki bilgileri toplayın:

- Hangi ilke ayarı uygulanmadı? Herhangi bir ilke uygulandı mı?
- Kullanıcı deneyimi nedir? Kullanıcıların hedeflenen uygulamayı yükleyip başlatsın mı?
- Sorun ne zaman başladı? Uygulama koruması hiç çalıştı mı?
- Hangi platform (Android veya iOS) soruna sahip?
- Kaç Kullanıcı etkilendi? Tüm cihazlar veya yalnızca bazı cihazlar etkileniyor mu?
- Kaç cihaz etkilendi? Tüm cihazlar veya yalnızca bazı cihazlar etkileniyor mu?
- Intune uygulama koruma ilkesi bir mobil cihaz yönetimi (MDM) hizmeti gerektirmese de, Intune veya üçüncü taraf EMM kullanan kullanıcılar etkileniyor mu?
- Tüm yönetilen uygulamalar veya yalnızca belirli uygulamalar etkileniyor mu? Örneğin, [Intune uygulama SDK 'sı](../developer/app-sdk-get-started.md) etkilenen LOB uygulamaları, ancak Mağaza uygulamaları değil mi?

Şimdi, bu soruların yanıtlarına göre sorun gidermeye başlayabilirsiniz.

### <a name="verify-prerequisites"></a>Önkoşulları doğrulama

Sorun gidermede bir sonraki adım, tüm önkoşulların karşılanıp karşılanmadığını denetmamız.

Intune uygulama koruma ilkelerini herhangi bir MDM çözümüyle bağımsız olarak kullanabilseniz de, aşağıdaki önkoşulların karşılanması gerekir:

- Kullanıcıya bir Intune lisansı atanmış olmalıdır.
- Kullanıcı, uygulama koruma ilkesi tarafından hedeflenen bir güvenlik grubuna ait olmalıdır. Aynı uygulama koruma ilkesi, kullanılan belirli bir uygulamayı hedeflemelidir.
- Android cihazlarda, uygulama koruma ilkelerini almak için Şirket Portalı uygulaması gereklidir.
- [Word, Excel veya PowerPoint](https://products.office.com/business/office) uygulamaları kullanıyorsanız, aşağıdaki ek gereksinimlerin karşılanması gerekir:
    - Kullanıcının, [iş için Microsoft 365](https://products.office.com/business/compare-more-office-365-for-business-plans) bir lisansa ve kullanıcının Azure Active Directory (Azure AD) hesabına bağlı olan kuruluşa sahip olması gerekir. Aboneliğin mobil cihazlarda Office uygulamalarını içermesi gerekir ve [OneDrive İş](https://onedrive.live.com/about/business/)’te bir bulut depolama hesabını içerebilir. Microsoft 365 lisansları, [Bu yönergeleri](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc)izleyerek [Microsoft 365 Yönetim merkezinde](https://admin.microsoft.com) atanabilir.
    - Kullanıcının ayrıntılı **farklı kaydet** işlevi kullanılarak yapılandırılmış bir yönetilen konumu olmalıdır. Bu komut, kuruluş verilerini uygulama koruma ilkesinin **kopyalarını kaydet** ilkesinin altında bulunur. Örneğin, yönetilen konum [OneDrive](https://onedrive.live.com/about/)Ise, OneDrive uygulaması kullanıcının Word, Excel veya PowerPoint uygulamasında yapılandırılmalıdır.
    - Yönetilen konum OneDrive ise, uygulamanın kullanıcıya dağıtılan uygulama koruma ilkesi tarafından hedeflenmelidir.

  > [!NOTE]
  > Office mobil uygulamaları şu anda yalnızca SharePoint Online 'ı destekler ve şirket içi SharePoint 'i desteklemez.

- Intune uygulama koruma ilkelerini şirket içi kaynaklarla birlikte kullanıyorsanız (Microsoft Skype Kurumsal ve Microsoft Exchange Server), [Skype Kurumsal ve Exchange Için karma modern kimlik doğrulamasını (HMA)](/office365/enterprise/hybrid-modern-auth-overview)etkinleştirmeniz gerekir.

Intune uygulama koruma ilkeleri, Kullanıcı kimliğinin uygulama ile [Intune uygulama SDK 'sı](../developer/app-sdk-get-started.md)arasında tutarlı olmasını gerektirir. Bu tutarlılığı güvence altına almanın tek yolu modern kimlik doğrulamadır. Uygulamaların modern kimlik doğrulaması olmadan şirket içi yapılandırmada çalışma senaryosu vardır. Ancak, sonuçlar tutarlı veya garanti edilmez.

Skype Kurumsal karma ve şirket içi yapılandırmalarda HMA 'yı etkinleştirme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- **Hibrit**<br>
[SfB ve Exchange için karma modern kimlik doğrulaması GA 'ye gidiyor](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **On-premises (Şirket içi)** <br>
[Azure AD ile SfB Onpred için modern kimlik doğrulama](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Uygulama koruma ilkesi durumunu denetleme

Uygulama koruma durumunuzu denetlemek için şu adımları izleyin:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Apps**  >  **Monitor**  >  **Uygulama koruma durumunu**izlemek için uygulamalar ' ı seçin ve ardından **atanan kullanıcılar** kutucuğunu seçin.
3. **Uygulama raporlama** sayfasında **Kullanıcı seçin**'i belirterek kullanıcı ve grupların bulunduğu listeyi açın.
4. Listeden etkilenen kullanıcılardan birini arayıp seçin, sonra **Kullanıcı Seç**' i seçin. Uygulama raporlama bölmesinin üst kısmında, kullanıcının uygulama koruması için lisanslı olup olmadığını ve Microsoft 365 için bir lisansa sahip olup olmadığını görebilirsiniz. Ayrıca, tüm kullanıcı cihazları için uygulama durumunu görebilirsiniz.
5. Hedeflenen uygulamalar, cihaz türleri, ilkeler, cihaz iade durumu ve son eşitleme zamanı gibi önemli bilgilere dikkat edin.

> [!NOTE]
> Uygulama koruma ilkeleri yalnızca uygulamalar iş bağlamında kullanıldığında uygulanır. Örneğin, Kullanıcı uygulamalara bir iş hesabı kullanarak erişirken.

Daha fazla bilgi için bkz. [Microsoft Intune 'de uygulama koruma ilkesi kurulumunuzu doğrulama](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Uygulama ile Intune uygulama SDK 'Sı arasında Kullanıcı kimliğinin tutarlı olduğunu doğrulama

Çoğu senaryoda, kullanıcılar kendi hesaplarında Kullanıcı asıl adını (UPN) kullanarak oturum açabilirler. Ancak, bazı ortamlarda (Şirket içi senaryolar gibi), kullanıcılar başka bir oturum açma kimlik bilgisi biçimini kullanabilir. Bu durumlarda, uygulamada kullanılan UPN 'nin Azure AD 'deki UPN nesnesiyle eşleşmemesi fark edebilirsiniz. Bu sorun oluştuğunda, uygulama koruma ilkeleri beklendiği gibi uygulanmaz.

Microsoft 'un önerilen en iyi yöntemleri, UPN 'yi birincil SMTP adresi ile eşleşmedir. Bu uygulama, kullanıcıların tutarlı bir kimliğe sahip olarak yönetilen uygulamalarda, Intune uygulama korumasında ve diğer Azure AD kaynaklarında oturum açmasını sağlar. Daha fazla bilgi için bkz. [Azure AD userPrincipalName popülasyonu](/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Ortamınız alternatif oturum açma yöntemleri gerektiriyorsa bkz. alternatif [oturum açma kimliğini yapılandırma](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), özellikle de [alternatif kimlik Ile karma modern kimlik doğrulama](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Kullanıcının hedeflendiğini doğrulama

Intune uygulama koruma ilkelerinin kullanıcıları hedeflemeli olması gerekir. Bir kullanıcı veya kullanıcı grubuna uygulama koruma ilkesi atamadıysanız, ilke uygulanmaz.

İlkenin hedeflenen kullanıcıya uygulandığını doğrulamak için şu adımları izleyin:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Apps**  >  **Monitor**  >  **Uygulama koruma durumunu**izleme uygulamaları ' nı seçin ve ardından **Kullanıcı durumu** kutucuğunu (cihaz işletim sistemi platformuna göre) seçin.
Açılan **uygulama raporlama** bölmesinde, Kullanıcı aramak Için **Kullanıcı Seç** ' i seçin.
3. Listeden kullanıcı seçin. Bu kullanıcının ayrıntılarını görebilirsiniz.

İlkeyi bir kullanıcı grubuna atadığınızda, kullanıcının kullanıcı grubunda olduğundan emin olun. Bunu yapmak için şu adımları uygulayın:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Grupları > tüm gruplar**' ı seçin ve ardından uygulama koruma ilkesi atamalarınız için kullanılan grubu arayıp seçin.
3. **Yönet** bölümünün altında **Üyeler**' i seçin.
4. Etkilenen Kullanıcı listede yoksa, Azure Active Directory grupları ve grup üyeliği kurallarınızı [kullanarak uygulama ve kaynak erişimini yönetme](/azure/active-directory/fundamentals/active-directory-manage-groups) konusunu gözden geçirin. Etkilenen kullanıcının gruba eklendiğinden emin olun.
5. Etkilenen kullanıcının ilke için hariç tutulan gruplardan hiçbirinde bulunmadığından emin olun.

> [!IMPORTANT]
> - Intune uygulama koruma ilkesinin, cihaz gruplarına değil Kullanıcı gruplarına atanması gerekir.
> - Etkilenen cihaz Apple Aygıt Kayıt Programı (DEP) kullanıyorsa, **Kullanıcı benzeşimi** ' nin etkinleştirildiğinden emin olun. Kullanıcı Benzeşimi, DEP altında kullanıcı kimlik doğrulaması gerektiren tüm uygulamalar için gereklidir.
> - Etkilenen cihaz Android Enterprise kullanıyorsa, yalnızca iş profilleri uygulama koruma ilkelerini destekleyecektir.


### <a name="verify-that-the-managed-app-is-targeted"></a>Yönetilen uygulamanın hedeflenmiş olduğunu doğrulama

Intune uygulama koruma ilkelerini yapılandırdığınızda, hedeflenen uygulamalar [Intune uygulama SDK 'sını](../developer/app-sdk-get-started.md)kullanmalıdır. Aksi takdirde, uygulama koruma ilkeleri doğru çalışmayabilir.

Hedeflenen uygulamanın [Microsoft Intune korunan uygulamalarda](../apps/apps-supported-intune-apps.md)listelendiğinden emin olun. LOB veya özel uygulamalar için, uygulamaların [Intune uygulama SDK 'sının](../developer/app-sdk-get-started.md)en son sürümünü kullanbildiğini doğrulayın. Şunlara dikkat edin:

İOS için, her sürüm bu ilkelerin nasıl uygulandığını ve nasıl çalıştığını etkileyen düzeltmeler içerdiğinden, bu uygulama önemlidir. Daha fazla bilgi için bkz. [Intune uygulama SDK 'Sı iOS sürümleri](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
Android için bu uygulama önemli değildir. Ancak, Şirket Portalı Uygulama İlke Aracısı Aracısı olarak çalışacağından, kullanıcıların Şirket Portalı uygulamasının en son sürümü yüklü olmalıdır.

> [!NOTE]
> Intune, Eylül 2019 ' den itibaren Intune uygulama SDK 'Sı 8.1.1 ve sonraki sürümlere sahip iOS uygulamalarını destekleyecek şekilde hareket edecektir. 8.1.1 'den önceki SDK sürümleri kullanılarak oluşturulan uygulamalar artık desteklenmeyecektir. 

## <a name="more-information"></a>Daha fazla bilgi

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Intune MDM ile yönetilen cihazlar için özel gereksinimler

Bir uygulama koruma ilkesi oluşturduğunuzda, bunu tüm uygulama türlerine veya aşağıdaki uygulama türlerine hedefleyebilirsiniz:

- Yönetilmeyen cihazlardaki uygulamalar
- Intune tarafından yönetilen cihazlarda uygulamalar
- Android Iş profilindeki uygulamalar

> [!NOTE] 
> Uygulama türlerini belirtmek için, **hedefi tüm uygulama türlerine** **Hayır**olarak ayarlayın ve ardından **uygulama türleri** listesinden seçin.

İOS için, uygulama koruma ilkesi (uygulama) ayarlarını Intune 'a kayıtlı cihazlardaki uygulamalara hedeflemek için aşağıdaki ek [uygulama yapılandırma ayarları](../apps/app-configuration-policies-use-ios.md) gerekir:

- **Intunemamupn** tüm MDM (Intune veya üçüncü taraf EMM) tarafından yönetilen uygulamalar için yapılandırılmalıdır. Daha fazla bilgi için bkz. Microsoft Intune veya üçüncü taraf EMM için Kullanıcı UPN ayarını yapılandırma.
- **Intunemamdeviceıd** , tüm üçüncü taraf ve LOB MDM ile yönetilen uygulamalar için yapılandırılmalıdır.
- **Intunemamdeviceıd** , cihaz kimliği belirteci olarak yapılandırılmalıdır. Örneğin, Key = ıntunemamdeviceıd, değer = {{DeviceID}}. Daha fazla bilgi için bkz. [Yönetilen iOS cihazlar için uygulama yapılandırma ilkeleri ekleme](../apps/app-configuration-policies-use-ios.md).
- Yalnızca **ıntunemamdeviceıd** değeri yapılandırılırsa, Intune uygulaması cihazı yönetilmeyen olarak kabul eder.

### <a name="scenario-policy-changes-are-not-working"></a>Senaryo: Ilke değişiklikleri çalışmıyor
[Intune uygulama SDK 'sı](../developer/app-sdk-get-started.md) , ilke değişikliklerini düzenli olarak denetler. Ancak, bu işlem aşağıdaki nedenlerden herhangi biri için gecikebilir:

- Uygulama, hizmetle iade edilmedi.
- Şirket Portalı uygulama cihazdan kaldırılmıştır.

Intune uygulama koruma İlkesi Kullanıcı kimliğini kullanır. Bu nedenle, uygulamaya yönelik bir iş veya okul hesabı kullanan geçerli bir oturum ve hizmetle tutarlı bir bağlantı gerekir. Kullanıcı uygulamada oturum açmadıysa veya Şirket Portalı uygulama cihazdan kaldırılmışsa, ilke güncelleştirmeleri uygulanmaz.

Ayrıca, uygulama koruma ilkesinde yapılan değişikliklerin ve güncelleştirmelerin uygulanması 8 saate kadar sürebilir. Uygulanabiliyorsa, tüm uygulamaları kapatma ve cihazı yeniden başlatma, genellikle ilke güncelleştirmesini daha erken uygulanmaya zorlar.

Uygulama koruma durumunu denetlemek için şu adımları izleyin:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Apps**  >  **Monitor**  >  **Uygulama koruma durumunu**izlemek için uygulamalar ' ı seçin ve ardından **atanan kullanıcılar** kutucuğunu seçin.
3. Uygulama Raporlama sayfasında, **Kullanıcı Seç** ' i seçerek kullanıcılar ve gruplar listesini açın.
4. Listeden etkilenen kullanıcılardan birini arayıp seçin, sonra **Kullanıcı Seç**' i seçin.
5. Durum ve son eşitleme saati dahil olmak üzere, şu anda uygulanmış olan ilkeleri gözden geçirin.
6. Durum **Iade edilmez**veya görüntü yakın zamanda eşitleme olmadığını gösteriyorsa, kullanıcının tutarlı bir ağ bağlantısına sahip olup olmadığını denetleyin. Android kullanıcıları için Şirket Portalı uygulamasının en son sürümünün yüklü olduğundan emin olun.

> [!IMPORTANT]
> [Intune uygulama SDK 'sı](../developer/app-sdk-get-started.md) seçmeli Temizleme için her 30 dakikada bir denetler. Ancak, zaten oturum açmış olan kullanıcılar için mevcut ilkede yapılan değişiklikler 8 saate kadar görünmeyebilir. Bu işlemi hızlandırmak için, kullanıcının uygulamayı oturum açmasını ve sonra yeniden oturum açıp cihazlarını yeniden başlatmasını sağlayabilirsiniz.

Intune uygulama koruma ilkesi, çoklu kimlik desteği içerir. Intune, uygulama koruma ilkelerini yalnızca uygulamada oturum açan iş veya okul hesabına uygulayabilir. Ancak, cihaz başına yalnızca bir iş veya okul hesabı desteklenir.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Senaryo: ilke uygulandı, ancak iOS kullanıcıları iş dosyalarını yine de yönetilmeyen uygulamalara aktarmaya devam edebilir
İOS cihazları için **açma yönetimi** ( ![ Aç düğmesi ](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg) ) özelliği, MDM kanalı aracılığıyla dağıtılan uygulamalar arasında dosya aktarımlarını sınırlayabilir. Kullanıcı, yapılandırmaya bağlı olarak OneDrive ve Exchange gibi yönetilen konumlardan iş dosyalarını, yönetilmeyen uygulamalara veya konumlara aktarabilir. İOS **Açık yönetim** özelliği diğer veri aktarımı yöntemlerinin dışında çalışmaktadır. Bu nedenle, **farklı kaydet** ve **Kopyala/Yapıştır** ayarları bundan etkilenmez.

Şirket verilerini aşağıdaki şekilde korumak için Intune uygulama koruma ilkelerini iOS birlikte **açma yönetimi** özelliğiyle birlikte kullanabilirsiniz:

- **BIR MDM çözümü tarafından yönetilmeyen çalışana ait cihazlar**: uygulama koruma ilkesi ayarlarını, **uygulamanın yalnızca ilkeyle yönetilen uygulamalara veri aktarmasına izin**verecek şekilde ayarlayabilirsiniz. Bu şekilde yapılandırıldığında, ilkeyle yönetilen bir uygulamadaki **Açık** davranış, paylaşım seçenekleri olarak yalnızca diğer ilkeyle yönetilen uygulamalar sağlar. Örneğin, bir kullanıcı yerel posta uygulamasında OneDrive 'dan korumalı bir dosyayı bir ek olarak göndermeyi denediğinde bu dosya okunamaz.

- **MDM çözümleri tarafından yönetilen cihazlar**: Intune veya üçüncü taraf MDM çözümlerine kayıtlı cihazlar için uygulama koruma ilkelerini kullanarak uygulamalar arasında veri PAYLAŞıMı ve MDM aracılığıyla dağıtılan diğer yönetilen iOS uygulamaları, Intune uygulaması ve iOS **Açık yönetim** özelliği tarafından denetlenir.<br/><br/>
Bir MDM çözümünü kullanarak dağıttığınız uygulamaların de Intune uygulama koruma ilkeleriniz ile ilişkili olduğundan emin olmak için Kullanıcı UPN ayarını [Kullanıcı UPN 'Sini yapılandırma](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm)bölümünde anlatıldığı şekilde yapılandırın.<br/><br/>Diğer uygulamalara veri aktarımına nasıl izin vermek istediğinizi belirtmek için, **diğer uygulamalara kuruluş verisi gönder**' i etkinleştirin ve tercih ettiğiniz paylaşım düzeyini seçin.<br/><br/>Bir uygulamanın diğer uygulamalardan veri almasına nasıl izin vermek istediğinizi belirtmek için, **diğer uygulamalardan veri al**seçeneğini etkinleştirin ve tercih edilen veri alma düzeyini seçin.

Uygulama verilerini alma ve paylaşma hakkında daha fazla bilgi için bkz. [veri değiştirme ayarları](../apps/app-protection-policy-settings-ios.md#data-protection).

Daha fazla bilgi için bkz. [Microsoft Intune’da iOS uygulamaları arasında veri aktarımını yönetme](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Başvurular

Hala ilgili bir soruna çözüm arıyorsanız veya Intune hakkında daha fazla bilgi için [Microsoft Intune forumumuza](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)soru gönderin. Birçok destek mühendisi, MVP ve geliştirme ekibimizin üyeleri forumları ziyaret edebilir. Bu nedenle, ihtiyacınız olan bilgileri içeren birini bulmanın iyi bir olasılığı vardır.

Microsoft Intune ürün desteği ekibine yönelik destek isteği açmak için bkz. [Microsoft Intune için destek alma](../fundamentals/get-support.md).

Intune uygulama koruma ilkesi hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Mobil uygulama yönetimi sorunlarını giderme](../apps/troubleshoot-mam.md)
- [MAM ve uygulama koruma hakkında sık kullanılan sorular](../apps/mam-faq.md)
- [Destek Ipucu: yerel cihazlarda günlük dosyalarını kullanarak Intune uygulama koruma İlkesi sorunlarını giderme](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

En son haberler, bilgiler ve teknik ipuçları için resmi bloglarımıza gidin:

- [Microsoft Intune destek ekibi blogu](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Microsoft Enterprise Mobility ve Security blogu](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Sonraki adımlar

- Ek Intune sorun giderme bilgileri için bkz. [Şirketinizdeki kullanıcılara yardımcı olmak için sorun giderme portalını kullanma](../fundamentals/help-desk-operators.md). 
- Microsoft Intune’daki tüm bilinen sorunlar hakkında bilgi edinin. Daha fazla bilgi için bkz. [Intune müşteri başarısı](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Ek yardım mı gerekiyor? Bkz. [Microsoft Intune için destek alma](../fundamentals/get-support.md).