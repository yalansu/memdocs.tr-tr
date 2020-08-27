---
title: Microsoft Intune - Azure’daki yenilikler | Microsoft Docs
titleSuffix: ''
description: Intune Azure portalındaki yenilikleri keşfedin
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34c69a8263a76b83f81470c214e05a5e02dc873c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88916070"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune'daki yenilikler

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde Microsoft Intune her hafta yenilikleri öğrenin. Ayrıca, [önemli bildirimler](#notices), [Geçmiş yayınlar](whats-new-archive.md)ve [Intune hizmet güncelleştirmelerinin nasıl yayımlandığına](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)ilişkin bilgileri de bulabilirsiniz. 

> [!Note]
> Her [aylık güncelleştirmenin](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) piyasaya çıkma üç güne kadar sürebilir ve şu sırada olacaktır:
>
> - Gün 1: Asya Pasifik (APAC)
> - Gün 2: Avrupa, Orta Doğu, Afrika (EMEA)
> - Gün 3: Kuzey Amerika
> - Gün 4 +: kamu için Intune
>
> Bazı özelliklerin piyasaya çıkması birkaç haftayı bulabilir ve tüm özellikler ilk hafta bütün müşterilerimize sunulmamış olabilir.
>
> Bir sürümdeki yaklaşan özelliklerin bir listesi için [geliştirme sayfasını](in-development.md) inceleyin.

**RSS akışı**: aşağıdaki URL 'yi kopyalayıp akış okuyucunuzun içine yapıştırarak Bu sayfa güncelleştirildikten sonra bildirim alın: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts

<!-- ########################## -->
## <a name="week-of-august-24-2020-2008-service-release"></a>24 Ağustos 2020 (2008 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322----"></a>Apple VPP belirtecinin silinmesinden önce ilişkili lisanslar iptal edildi<!--6195322  -->
Microsoft Endpoint Manager 'da bir Apple VPP belirtecini sildiğinizde, bu belirteçle ilişkilendirilen tüm Intune tarafından atanan lisanslar silinmeden önce otomatik olarak iptal edilir.

#### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-shows-descriptions----7414768-wnstaged---"></a>Android için Şirket Portalı App 'teki cihaz ayarlarını güncelleştirme iyileştirmesi açıklamaları gösterir <!-- 7414768 wnstaged -->
Android cihazlarda Şirket Portalı uygulamasında, **cihaz ayarlarını Güncelleştir** sayfası, güncelleştirilmesi gereken ayarları listeler. Kullanıcılar daha fazla bilgi görmek için sorunu genişletir ve **Çözümle** düğmesine bakın.

Bu Kullanıcı deneyimi geliştirilmiştir. Listelenen ayarlar, açıklamayı göstermek için varsayılan olarak genişletilir ve uygunsa **Çözümle** düğmesini gösterir. Daha önce, sorunlar varsayılan olarak daraltılıydı. Bu varsayılan davranış, kullanıcıların sorunları daha hızlı çözümleyebilmeleri için tıklama sayısını azaltır.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631-----"></a>İOS/ıpados ve macOS cihazları için VPN bağlantı türü olarak NetMotion kullanma<!-- 1333631   -->
Bir VPN profili oluşturduğunuzda netmotion, bir VPN bağlantı türü olarak kullanılabilir (**cihazlar**  >  **cihaz yapılandırması**  >  **Create profile**  >  **iOS/ıpados** veya **MacOS** for platform > **VPN** for platform > bağlantı türü için **netmotion** ).

Intune 'da VPN profilleri hakkında daha fazla bilgi için bkz. VPN [sunucularına bağlanmak IÇIN VPN profilleri oluşturma](../configuration/vpn-settings-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS
- Mac OS

#### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024----"></a>Windows 10 Wi-Fi profilleri için daha fazla korunan Genişletilebilir Kimlik Doğrulama Protokolü (PEAP) seçenekleri<!-- 3805024  -->
Windows 10 cihazlarında, Wi-Fi bağlantılarının kimliğini doğrulamak için Genişletilebilir Kimlik Doğrulama Protokolü (EAP) kullanarak Wi-Fi profilleri oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Windows 10 and later** profil > **Enterprise**için **Wi-Fi** >.

Korumalı EAP (PEAP) seçeneğini belirlediğinizde kullanılabilir yeni ayarlar vardır:
- **PEAP aşamasında sunucu doğrulaması gerçekleştirme 1**: PEAP anlaşma aşaması 1 ' de, sunucu sertifika doğrulaması tarafından doğrulanır.
  - **PEAP aşaması 1 ' de sunucu doğrulaması için Kullanıcı Istemlerini devre dışı bırak**: PEAP anlaşma aşaması 1 ' de, Kullanıcı tarafından güvenilen sertifika yetkilileri IÇIN yeni PEAP sunucularının yetkilendirilmesini isteyen istemler gösterilmez.
- **Şifreleme bağlaması gerektir**: PEAP anlaşması sırasında şifre tabanlı bağlama kullanmayan PEAP sunucularıyla bağlantıları engeller.

Yapılandırabileceğiniz ayarları görmek için [Windows 10 ve üzeri cihazlar Için Wi-Fi ayarları ekle](../configuration/wi-fi-settings-windows.md)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir: 
- Windows 10 ve üzeri

#### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576--idstaged---"></a>MacOS Microsoft Enterprise SSO eklentisini yapılandırma<!-- 5627576  idstaged -->
Microsoft Azure AD ekibi, macOS 10.15 + kullanıcılarına Microsoft uygulamalarına, kuruluş uygulamalarına ve Apple 'ın SSO özelliğini destekleyen ve Azure AD 'yi kullanarak kimlik doğrulaması yapan, tek bir oturum açma işlemiyle erişim elde etmesine izin vermek için bir yeniden yönlendirme çoklu oturum açma (SSO) uygulama uzantısı oluşturdu. Microsoft Enterprise SSO eklentisi sürümü sayesinde, SSO uzantısını yeni Microsoft Azure AD uygulama uzantısı türüyle**yapılandırabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  profil için**MacOS** for platform > **cihaz özellikleri** > **Çoklu oturum açma uygulama** uzantısı > SSO uygulama uzantısı türü > **Microsoft Azure AD**).

Microsoft Azure AD SSO uygulama uzantısı türüyle SSO sağlamak için, kullanıcıların macOS cihazlarındaki Şirket Portalı uygulamasını yüklemesi ve üzerinde oturum açması gerekir. 

MacOS SSO uygulama uzantıları hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısı](../configuration/device-features-configure.md#single-sign-on-app-extension).

Aşağıdakiler cihazlar için geçerlidir:
- macOS 10,15 ve üzeri

#### <a name="prevent-users-from-unlocking-android-enterprise-work-profile-devices-using-face-and-iris-scanning--6069759-idmiss---"></a>Kullanıcıların yüz ve Iris taramasını kullanarak Android kurumsal iş profili cihazlarını kilidini kullanmalarını engelleyin<!--6069759 idmiss -->
Artık kullanıcıların yüz veya Iris taramasını kullanmasını engelleyebilirsiniz. Bu, cihaz düzeyinde veya iş profili düzeyinde iş profili Yönetilen cihazlarının kilidini açabilir. Bu **, cihaz**  >  **yapılandırma profilleri**  >  için**profil oluşturma**  >  **Android Enterprise** for platform > **iş > profili** , profil > **iş profili ayarları** ve **parola** bölümleri için cihaz kısıtlamaları oluşturabilir ' de ayarlanabilir.

Daha fazla bilgi için bkz. [Intune kullanarak özelliklere izin vermek veya bunları kısıtlamak için Android Kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Aşağıdakiler cihazlar için geçerlidir: 
- Android kurumsal iş profili

#### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991----"></a>Microsoft Enterprise SSO eklentisiyle diğer iOS/ıpados uygulamalarında SSO uygulama uzantılarını kullanın<!-- 7369991  -->
[Apple cihazları Için Microsoft ENTERPRISE SSO eklentisi](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) , SSO uygulama uzantılarını destekleyen tüm uygulamalarla birlikte kullanılabilir. Intune 'da bu özellik, eklentinin Apple cihazları için Microsoft kimlik doğrulama kitaplığı 'nı (MSAL) kullanmayan Mobile iOS/ıpados uygulamalarıyla birlikte çalışacağı anlamına gelir. Uygulamaların MSAL kullanması gerekmez, ancak Azure AD uç noktalarında kimlik doğrulaması yapması gerekir.

İOS/ıpados uygulamalarınızı eklentiyle birlikte SSO 'yu kullanacak şekilde yapılandırmak için bir iOS/ıpados yapılandırma profiline uygulama paketi tanımlayıcıları**ekleyin (cihaz**  >  **yapılandırma**  >  **Create profile**  >  **iOS/iPadOS** > > profilleri, **Device features** SSO uygulama uzantısı türü > uygulama paketi kimlikleri) için **Çoklu oturum açma uygulama uzantısı**  >  **Microsoft Azure AD** **App bundle IDs**

Yapılandırabileceğiniz geçerli SSO uygulama uzantısı ayarlarını görmek için [Çoklu oturum açma uygulaması uzantısına](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="deploy-endpoint-security-antivirus-policy-to-tenant-attached-devices-preview---5475441----"></a>Kiracı ekli cihazlarına Endpoint Security virüsten koruma ilkesini dağıtma (Önizleme)<!-- 5475441  -->
Önizleme olarak, Configuration Manager ile yönettiğiniz cihazlara [Virüsten koruma için](../protect/endpoint-security-antivirus-policy.md) uç nokta güvenlik ilkesi dağıtabilirsiniz. Bu senaryo, desteklenen bir Configuration Manager sürümü ve Intune aboneliğiniz arasında bir kiracı iliştirme yapılandırması yapılandırmanızı gerektirir. Aşağıdaki Configuration Manager sürümleri desteklenir:

- Geçerli dalı Configuration Manager 2006

Daha fazla bilgi için, kiracı eklemeyi desteklemek üzere [Intune uç nokta güvenlik ilkelerine yönelik gereksinimlere](../protect/tenant-attach-intune.md#specific-requirements-for-intune-endpoint-security-policies) bakın.

#### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119------"></a>Endpoint Security virüsten koruma ilkesi dışlamaları için değişiklikler<!--5583940, 6018119    -->
[Endpoint Security virüsten koruma ilkesinin](../protect/endpoint-security-antivirus-policy.md)bir parçası olarak yapılandırdığınız Microsoft Defender virüsten koruma dışlama listelerini yönetmek için iki değişiklik yaptık. Değişiklikler, farklı ilkeler arasındaki çakışmaları önlemenize ve önceden dağıtılan ilkeleriniz üzerinde mevcut olabilecek dışlama listesi çakışmalarını çözmenize yardımcı olur.

Her iki değişiklik de aşağıdaki [Microsoft Defender virüsten koruma yapılandırma hizmeti sağlayıcılarının](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) (CSP 'ler) ilke ayarları için geçerlidir:

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

Değişiklikler şunlardır:

- Yeni profil türü: **Microsoft Defender virüsten koruma dışlamaları** -yalnızca virüsten koruma dışlamalarıyla odaklanan bir ilke tanımlamak için Windows 10 ve üzeri için bu yeni profil türünü kullanın. Bu profil, diğer ilke yapılandırmalarından ayırarak dışlama listelerinizin yönetimini basitleştirmeye yardımcı olur.

  Yapılandırabileceğiniz Dışlamalar, Defender *süreçlerini*, *dosya uzantılarını*ve Microsoft Defender 'ın tarayabilmesi istemediğiniz *Dosya* ve *klasörleri* içerir.

- **İlke birleştirme** – Intune artık ayrı profillerde tanımladığınız dışlamaları listesini her bir cihaza veya kullanıcıya uygulanacak tek bir dışlamaları listesine birleştirir. Örneğin, üç ayrı ilke ile bir kullanıcıyı hedefliyorsanız, bu üç ilkenin dışlama listeleri *Microsoft Defender virüsten koruma dışlamalarının*tek bir üst kümesi ile birleştirilir ve bu da bu kullanıcı için geçerlidir.


<!-- ########################## -->
## <a name="week-of-august-17-2020"></a>17 Ağustos 2020 haftası

### <a name="intune-apps"></a>Intune uygulamaları

#### <a name="custom-brand-image-now-displayed-in-the-windows-company-portal-profile-page---4280187---"></a>Özel marka resmi artık Windows Şirket Portalı profili sayfasında görüntüleniyor<!-- 4280187 -->
Microsoft Intune Yöneticisi olarak, Intune 'a, Windows Şirket Portalı uygulamasındaki kullanıcının profil sayfasında bir arka plan görüntüsü olarak görüntülenecek özel bir marka resmi yükleyebilirsiniz. Daha fazla bilgi için bkz. [uygulamaları, Şirket portalı Web sitesini ve Intune uygulamasını özelleştirme Intune şirket portalı](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Şirket Portalı Configuration Manager uygulama desteği ekler<!-- 4297660 -->
Şirket Portalı artık Configuration Manager uygulamalarını desteklemektedir. Bu özellik, son kullanıcıların ortak yönetilen müşteriler için Şirket Portalı hem Configuration Manager hem de Intune tarafından dağıtılan uygulamaları görmesini sağlar. Bu destek, yöneticilerin farklı Son Kullanıcı Portalı deneyimlerini birleştirmesine yardımcı olur. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](/mem/configmgr/comanage/company-portal). 

### <a name="device-security"></a>Cihaz güvenliği

#### <a name="set-device-compliance-state-from-third-party-mdm-providers---6361689---"></a>Üçüncü taraf MDM sağlayıcılarından cihaz uyumluluk durumunu ayarla<!-- 6361689 -->

Intune artık [cihaz uyumluluk ayrıntıları kaynağı olarak üçüncü taraf MDM çözümlerini](../protect/device-compliance-partners.md)desteklemektedir. Bu üçüncü taraf uyumluluk verileri, Microsoft Intune tümleştirmesi aracılığıyla iOS ve Android üzerinde Microsoft 365 uygulamalar için koşullu erişim ilkelerini zorlamak üzere kullanılabilir.  Intune, bir cihazın güvenilir olup olmadığını anlamak için üçüncü taraf sağlayıcıdan uyumluluk ayrıntılarını değerlendirir ve ardından Azure AD 'de koşullu erişim özniteliklerini ayarlar.  Azure AD koşullu erişim ilkelerinizi Microsoft Endpoint Manager yönetim merkezi veya Azure AD portalı içinden oluşturmaya devam edersiniz.

Aşağıdaki üçüncü taraf MDM sağlayıcıları, genel önizleme olarak bu yayında desteklenir:

- VMware çalışma alanı BIR UEM (daha önce AirWatch olarak biliniyordu)

*Bu güncelleştirme, müşterilere küresel olarak gönderilir. Bu özelliği bir sonraki hafta içinde görmeniz gerekir.*

<!-- ########################## -->
## <a name="week-of-august-10-2020"></a>10 Ağustos 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="tenant-attach-install-an-application-from-the-admin-center----in7220536-cm6024389--"></a>Kiracı iliştirme: yönetim merkezinden bir uygulama yükler <!-- IN7220536 CM6024389-->
Artık Microsoft Endpoint Manager yönetim merkezinden bir kiracıya bağlı cihaz için bir uygulamayı gerçek zamanlı olarak yüklemeyi başlatabilirsiniz. Daha fazla bilgi için bkz. [kiracı iliştirme: yönetim merkezinden uygulama yüklemesi](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## <a name="week-of-july-27-2020"></a>27 Temmuz 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="power-bi-compliance-report-template-v20---636958---"></a>Power BI uyumluluk raporu şablonu V 2.0<!-- 636958 -->
Power BI şablon uygulamaları, Power BI iş ortaklarının çok az kodlamaya sahip Power BI uygulamalar oluşturmasına ve bunları herhangi bir Power BI müşteriye dağıtmalarına olanak tanır. Yöneticiler, Power BI uyumluluk raporu şablonunun sürümünü V 1.0 'dan V 2.0 'a güncelleştirebilir. V 2.0, gelişmiş bir tasarım, Ayrıca, şablonun bir parçası olarak ortaya çıkacak hesaplamalarda ve verilerde yapılan değişiklikleri içerir. Daha fazla bilgi için bkz. [Power BI Ile veri ambarına bağlanma](../developer/reports-proc-get-a-link-powerbi.md) ve [bir şablon uygulamasını güncelleştirme](/power-bi/service-template-apps-install-distribute#update-a-template-app). Ayrıca, [Intune veri ambarı ile Power BI uyumluluk raporunun yeni bir sürümünü duyuran](https://aka.ms/new_compliance_report)blog gönderisine bakın.

<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>13 Temmuz 2020 (2007 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Exchange şirket Içi bağlayıcı desteği<!-- 7138486  -->
Intune, 2007 (Temmuz) sürümünden itibaren Intune hizmetinden şirket Içi Exchange Bağlayıcı özelliği desteğini kaldırıyor. Etkin bağlayıcı içeren mevcut müşteriler şu anda geçerli işlevselliğe devam edebilir. Etkin Bağlayıcısı olmayan yeni müşteriler ve mevcut müşteriler, artık yeni bağlayıcılar oluşturamaz veya Intune 'dan Exchange ActiveSync (EAS) cihazlarını yönetemez. Bu müşteriler için, Microsoft şirket içi Exchange 'e erişimi korumak için Exchange [karma modern kimlik doğrulamasının (HMA)](/office365/enterprise/hybrid-modern-auth-overview) kullanılmasını önerir. HMA hem Intune Uygulama Koruması Ilkelerini (MAM olarak da bilinir) hem de şirket içi Exchange için Outlook Mobile aracılığıyla koşullu erişim imkanı sunar.

#### <a name="smime-for-outlook-on-ios-and-android-devices-without-enrollment---6517155---"></a>Kayıt olmadan iOS ve Android cihazlarda Outlook için S/MIME<!-- 6517155 -->
Artık, yönetilen uygulamalar için bir uygulama yapılandırma ilkesi kullanarak iOS ve Android cihazlarda Outlook için S/MIME 'yi etkinleştirebilirsiniz. Bu, cihaz kayıt durumundan bağımsız olarak ilke teslimine izin verir. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen uygulamalar**Ekle ' yi seçin. Ayrıca, kullanıcıların Outlook 'ta bu ayarı değiştirmesine izin verip vermeyeceğinizi de seçebilirsiniz. Ancak, S/MIME sertifikalarını iOS ve Android için Outlook 'a otomatik olarak dağıtmak için cihazın kayıtlı olması gerekir. S/MIME hakkında genel bilgi için bkz. [Intune 'da e-postayı imzalamak ve şifrelemek Için s/MIME 'ye genel bakış](../protect/certificates-s-mime-encryption-sign.md). Outlook yapılandırma ayarları hakkında daha fazla bilgi için bkz. [Microsoft Outlook yapılandırma ayarları](../apps/app-configuration-policies-outlook.md) ve [cihaz kaydı olmadan yönetilen uygulamalar için uygulama yapılandırma ilkeleri ekleme](../apps/app-configuration-policies-managed-app.md). İOS ve Android S/MIME bilgileri için Outlook için bkz. [s/MIME senaryoları](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) ve [yapılandırma anahtarları-S/MIME ayarları](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Windows 10 ve daha yeni cihazlar için yeni VPN ayarları<!-- 6602122   -->

Ikev2 bağlantı türünü kullanarak bir VPN profili oluşturduğunuzda yapılandırabileceğiniz yeni ayarlar vardır (**cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **Windows 10 ve sonrası** için platform > **VPN** > **temel VPN**):

- **Cihaz tüneli**: cihazların Kullanıcı oturumu açma da dahil olmak üzere herhangi bir Kullanıcı ETKILEŞIMI gerekmeden VPN 'ye otomatik olarak bağlanmasına izin verir. Bu özellik **her zaman açık**' i etkinleştirmenizi ve **makine sertifikalarını** kimlik doğrulama yöntemi olarak kullanmanızı gerektirir.
- Şifreleme paketi ayarları: istemci ve sunucu ayarlarını eşleştirmeye izin veren ıKE ve alt güvenlik ilişkilerinin güvenliğini sağlamak için kullanılan algoritmaları yapılandırın.

Yapılandırabileceğiniz ayarları görmek için, [Intune kullanarak VPN bağlantıları eklemek üzere Windows cihaz ayarları](../configuration/vpn-settings-windows-10.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:

- Windows 10 ve üzeri

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Android kurumsal cihazlarda (COBO) cihaz kısıtlamaları profilinde daha fazla Microsoft Başlatıcı ayarı yapılandırma<!-- 6285001  -->

Android kurumsal tam olarak yönetilen cihazlarda, bir cihaz kısıtlamaları profili kullanarak daha fazla Microsoft başlatıcısı ayarı**yapılandırabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  platform için bir**profil**  >  **Android Enterprise** > **cihaz sahibi yalnızca**  >  **cihaz kısıtlamaları**cihaz  >  **deneyimi**  >  **tam olarak yönetilir**). 

Bu ayarları görmek için [Android kurumsal cihaz ayarları ' na giderek özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-android-for-work.md#device-experience).

Ayrıca, Microsoft Başlatıcı ayarlarını bir [uygulama yapılandırma profili](../apps/configure-microsoft-launcher.md)kullanarak da yapılandırabilirsiniz.

Aşağıdakiler cihazlar için geçerlidir:

- Android kurumsal cihaz sahibi tam olarak yönetilen cihazlar (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Android kurumsal cihaz sahibi adanmış cihazlarda (COSU) yönetilen giriş ekranı için yeni özellikler<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

Android kurumsal cihazlarda Yöneticiler, birden çok uygulama bilgi noktası modunu kullanarak adanmış cihazlarda yönetilen giriş ekranını özelleştirmek için cihaz yapılandırma profillerini kullanabilir (**cihazlar**  >  **yapılandırma profilleri**, cihaz  >  **Create profile**  >  **Android Enterprise** sahibi > cihaz **sahibine yalnızca**  >  **Device Restrictions** profil > cihaz için **Device experience**  >  **ayrılmış**cihaz  >  **Çoklu uygulaması**) cihaz kısıtlamalarına sahip olabilir.

Özellikle şunları yapabilirsiniz:

- Simgeleri özelleştirme, ekran yönünü değiştirme ve rozet simgelerinde uygulama bildirimlerini gösterme <!--7414175-->
- Yönetilen ayarlar kısayolunu gizle <!--7133328-->
- Hata ayıklama menüsüne daha kolay erişim <!--7133720-->
- Wi-Fi ağlarının izin verilen bir listesini oluşturma <!-- 7134873-->
- Cihaz bilgilerine daha kolay erişin <!-- 7135184-->

Daha fazla bilgi için bkz. [Android kurumsal cihaz ayarları, özelliklere izin vermek veya](../configuration/device-restrictions-android-for-work.md) [Bu blogu](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060)kısıtlamak için.

Aşağıdakiler cihazlar için geçerlidir:

- Android kurumsal cihaz sahibi, adanmış cihazlar (COSU)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>Microsoft Edge 84 için güncelleştirilmiş Yönetim Şablonları<!--7722068-->
Microsoft Edge için kullanılabilen ADMX ayarları güncelleştirildi. Son kullanıcılar artık Edge 84 ' de eklenen yeni ADMX ayarlarını yapılandırabilir ve dağıtabilir. Daha fazla bilgi için bkz. [Edge 84 sürüm notları](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>Şirkete ait, kişisel olarak etkinleştirilen cihazlar (Önizleme)<!--4442275  -->
Intune artık Android 8 ve üzeri işletim sistemi sürümleri için iş profiliyle iOS kurumsal şirkete ait cihazları desteklemektedir. İş profiline sahip şirkete ait cihazlar, Android kurumsal çözüm kümesindeki kurumsal yönetim senaryolarından biridir. Bu senaryo, kurumsal ve kişisel kullanım için tasarlanan tek Kullanıcı cihazlarına yöneliktir. Şirkete ait, kişisel olarak etkinleştirilen bu (COPE) senaryo şunları sunar:

- çalışma ve kişisel profil kapsayıcılama
- Yöneticiler için cihaz düzeyi denetimi
- Son kullanıcılara kişisel verilerinin ve uygulamalarının özel olarak kalacağı garantisi

İlk genel önizleme sürümü, genel olarak kullanılabilir sürüme dahil edilecek özelliklerin bir alt kümesini içerir. Ek özellikler, toplama temelinde eklenecektir. İlk önizlemede kullanılabilir olacak özellikler şunlardır:

- Kayıt: Yöneticiler, son tarihi olmayan benzersiz belirteçlerle birden çok kayıt profili oluşturabilir. Cihaz kaydı NFC, Token entry, QR Code, Zero Touch veya Knox Mobile kaydı aracılığıyla yapılabilir.
- Cihaz yapılandırması: mevcut, tam olarak yönetilen ve ayrılmış cihaz ayarlarının bir alt kümesi.
- Cihaz Uyumluluğu: Şu anda tam olarak yönetilen cihazlar için kullanılabilen uyumluluk ilkeleri.
- Cihaz eylemleri: cihazı silme (fabrika sıfırlaması), cihazı yeniden başlatma ve cihazı kilitleme.  
- Uygulama Yönetimi: uygulama atamaları, uygulama yapılandırması ve ilişkili raporlama özellikleri 
- Koşullu Erişim

Şirkete ait iş profili önizlemesi hakkında daha fazla bilgi için bkz. [destek blogu](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>MacOS cihazları için uzaktan kilitleme eylemine yönelik güncelleştirmeler<!--7032805   -->
MacOS cihazları için uzaktan kilitleme eyleminde yapılan değişiklikler şunları içerir:
- Kurtarma PIN 'i silinmeden önce 30 gün boyunca görüntülenir (7 gün yerine).
- Bir yöneticinin açık ikinci bir tarayıcısı varsa ve komutu farklı bir sekmeden ya da tarayıcıdan yeniden tetiklemeyi denediğinde, Intune komutun geçmesine izin verir. Ancak raporlama durumu, yeni bir PIN oluşturmak yerine başarısız olarak ayarlanır.
- Önceki komut hala beklenirse veya cihaz geri ayarlanmamışsa, yöneticinin başka bir uzaktan kilitleme komutu vermesine izin verilmez.
Bu değişiklikler, birden çok uzaktan kilitleme komutlarından sonra doğru PIN 'in üzerine yazılmasını engellemek için tasarlanmıştır.

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>Cihaz eylemleri silme ve korumalı silme arasındaki farklılıklar<!--7118901 -->
**Cihaz eylemleri** raporu artık silme ve korumalı silme eylemleri arasında farklılaştırır. Raporu görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **Monitor**  >  **cihaz eylemlerini** izleme ( **diğer**altında) bölümüne gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Microsoft Defender güvenlik duvarı kuralı geçiş aracı önizlemesi<!-- 6423187   -->
Genel önizleme olarak, Microsoft Defender güvenlik duvarı kurallarını geçiren bir PowerShell tabanlı araç üzerinde çalışıyoruz. Aracı yükleyip çalıştırdığınızda, Windows 10 istemcisinin geçerli yapılandırmasına dayalı olarak Intune için uç nokta güvenliği Güvenlik Duvarı kural ilkelerini otomatik olarak oluşturur. Daha fazla bilgi için bkz. [Endpoint Security güvenlik duvarı kuralı geçiş aracına genel bakış](../protect/endpoint-security-firewall-rule-tool.md).

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>Kiracı ekli cihazlarını MDADTP 'ye ekleme için uç nokta algılama ve yanıt ilkesi genel kullanıma sunuldu<!-- 7303816   -->
Intune 'daki Endpoint Security 'nin bir parçası olarak, [Configuration Manager tarafından yönetilen cihazlarla kullanılmak üzere uç nokta algılama ve yanıt (EDR) ilkeleri](../protect/endpoint-security-edr-policy.md) artık *Önizleme* aşamasındadır ve *genel kullanıma sunulmuştur*.

EDR ilkesini Configuration Manager desteklenen bir sürümünden cihazlarla kullanmak için, [Configuration Manager Için kiracı eklemeyi](../../configmgr/tenant-attach/device-sync-actions.md)yapılandırın. Kiracı ekleme yapılandırmasını tamamladıktan sonra, Microsoft Defender Gelişmiş tehdit koruması 'na (Microsoft Defender ATP) Configuration Manager tarafından yönetilen cihazları eklemek için EDR ilkeleri dağıtabilirsiniz.

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>Endpoint Security saldırı yüzeyi Azaltma ilkesi için cihaz denetim profillerinde Bluetooth ayarları bulunur <!--7032084   -->
Windows 10 cihazlarında Bluetooth 'u, *uç nokta güvenliği saldırı yüzeyi Azaltma ilkesi*için [cihaz denetim profiline](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) ekledik.  Bunlar, cihaz *yapılandırması*için cihaz kısıtlama profillerinde kullanılabilir olanlarla aynı ayarlardır.

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Windows 10 cihazları için Endpoint Security virüsten koruma ilkesiyle birlikte tanım güncelleştirmelerinin kaynak konumlarını yönetme<!-- 6347801   -->  
[Windows 10 cihazları için Endpoint Security virüsten koruma Ilkesinin](../protect/antivirus-microsoft-defender-settings-windows.md#updates) *güncelleştirmeler* kategorisine, cihazların güncelleştirme tanımlarını alma biçimini yönetmenize yardımcı olabilecek iki yeni ayar ekledik:

- *Tanım güncelleştirmelerini indirmek için dosya paylaşımlarını tanımlayın*
- *Tanım güncelleştirmelerini indirmek için kaynak sırasını tanımlayın*

Yeni ayarlarla, tanım güncelleştirmeleri için kaynak konumları indirme olarak UNC dosya paylaşımları ekleyebilir ve farklı kaynak konumlarına hangi sırada bağlantı kurulacağınızı tanımlayabilirsiniz.

#### <a name="improved-security-baselines-node---7433136------"></a>Geliştirilmiş güvenlik temelleri düğümü<!-- 7433136    -->
Microsoft Endpoint Manager Yönetim merkezinde [güvenlik temeli düğümünün](../protect/security-baselines.md) kullanılabilirliğini geliştirmek için bazı değişiklikler yaptık. Artık **uç nokta güvenlik**  >  **güvenliği temelleri** detayına gidin ve ardından, **profiller** bölmesi ile sunulan MDM güvenlik temeli gibi bir güvenlik taban çizgisi türü seçin. Profiller bölmesinde, bu taban çizgisi türü için oluşturduğunuz profilleri görüntüleyin.  Daha önce konsol, her zaman ayrı profiller için raporlarda bulunan ayrıntılarla eşleşen bir toplam veri toplamasını içeren bir genel bakış bölmesi sundu.

Değiştirilmeden, profiller bölmesinden, bu profil özelliklerinin yanı sıra *izleyici*altında bulunan çeşitli raporları görüntülemek için detaya gitme için bir profil seçebilirsiniz.  Benzer şekilde, profillerle aynı düzeyde, dağıttığınız bu profil türünün çeşitli sürümlerini görüntülemek için hala **sürümler** ' i seçebilirsiniz. Bir sürümde detaya gitme yaptığınızda, profil raporlarına benzer şekilde raporlara de erişebilirsiniz. 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Windows için türetilmiş kimlik bilgileri desteği<!-- 4886090   -->
Artık Windows cihazlarınızla türetilmiş kimlik bilgilerini kullanabilirsiniz. Bu, iOS/ıpados ve Android için mevcut desteğe genişletilir ve aynı türetilmiş kimlik bilgileri sağlayıcıları için kullanılabilir olacaktır:
- Entrust Datacard
- Intercede
- DıŞA purebred

Tek başına desteği, Wi-Fi veya VPN profillerinin kimliğini doğrulamak için türetilmiş bir kimlik bilgisinin kullanımını içerir. Windows cihazlarında, türetilmiş kimlik bilgileri, kullandığınız türetilmiş kimlik bilgisi sağlayıcısı tarafından verilen istemci uygulamasından verilir.

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Intune tarafından değil, cihaz kullanıcısı tarafından şifrelenen cihazlar için dosya Kasası şifrelemesini yönetme<!--5239424  -->
Intune artık, Intune ilkesi tarafından değil [cihaz kullanıcısı tarafından şifrelenen bir macOS cihazında dosya Kasası disk şifrelemesi yönetimini varsayabilir](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices).  Bu senaryo şunları gerektirir:
- Intune 'dan, dosya kasasını sağlayan disk şifreleme ilkesini alacak olan cihaz.
- Cihaz kullanıcısı, şifreli cihaz için kişisel kurtarma anahtarını Intune 'a yüklemek üzere Şirket Portalı Web sitesini kullanır. Anahtarı karşıya yüklemek için şifrelenmiş macOS cihazı için *Mağaza kurtarma anahtarı* seçeneğini seçeceğiz.

Kullanıcı kurtarma anahtarını karşıya yükledikten sonra, Intune geçerli olduğunu doğrulamak için anahtarı döndürür. Intune artık, cihazı doğrudan şifrelemek için ilkeyi kullandığımıza göre anahtarı ve şifrelemeyi yönetebilir. Bir kullanıcının cihazını kurtarmaları gerekir, bu, aşağıdaki konumlardan herhangi bir cihaz kullanarak kurtarma anahtarına erişebilirler:   
- Şirket Portalı web sitesi
- İOS için Şirket Portalı App/ıpados 
- Android için Şirket Portalı uygulaması
- Intune uygulaması

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>MacOS Filekasası disk şifrelemesi sırasında bir cihaz kullanıcısının kişisel kurtarma anahtarını gizle<!--  5475632-->
MacOS Filekasası disk şifrelemesini yapılandırmak için uç nokta güvenlik ilkesi kullandığınızda, cihaz şifrelenirken *kişisel kurtarma anahtarının* görüntülenmesini engellemek için [**Kurtarma anahtarını Gizle**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) ayarını kullanın. Şifreleme sırasında anahtarı gizleyerek, kullanıcıların cihaz şifrelemesini beklerken daha sonra yazamayacak kadar güvenli kalmasına yardımcı olabilirsiniz. 

Daha sonra, kurtarma gerekliyse, Kullanıcı Intune Şirket Portalı Web sitesi, iOS/ıpados Şirket Portalı, Android Şirket Portalı veya Intune uygulaması aracılığıyla kişisel kurtarma anahtarını görüntülemek için her zaman herhangi bir cihazı kullanabilir.

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>Cihazlar için güvenlik temeli ayrıntılarının geliştirilmiş görünümü<!-- 5536846  -->
Artık, cihaza uygulanan güvenlik temellerine yönelik ayar ayrıntılarını görüntülemek için bir cihazın ayrıntılarında ayrıntıya gidebilirsiniz. Ayarlar, ayarı kategorisi, ayar adı ve durumu içeren basit, düz bir liste içinde görüntülenir. Daha fazla bilgi için bkz. [cihaz başına Endpoint Security yapılandırmasını görüntüleme](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>Cihaz uyumluluk günlükleri artık Ingilizce olarak<!--6014904  -->
Intune Devicekarmaşık kuruluş günlükleri daha önce yalnızca Karmaşıkstate, OwnerType ve DeviceHealthThreatLevel için numaralandırmalar içeriyordu. Artık bu günlüklerde sütunlarda Ingilizce bilgiler vardır.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-----"></a>Profil ata ve profili Güncelleştir izin değişiklikleri<!--7177586   -->
Otomatik cihaz kayıt akışı için profil atama ve güncelleştirme profili için rol tabanlı erişim denetimi izinleri değişti:

Profil ata: Yöneticiler bu izinle profiller ve otomatik cihaz kaydı için bir belirtece varsayılan bir profil atar.

Güncelleştirme profili: Bu izne sahip yöneticiler, yalnızca otomatik cihaz kaydı için mevcut profilleri güncelleştirebilir.

Bu rolleri görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **kiracı yönetim**  >  **rolleri**  >  **tüm roller**  >  **Create**  >  **izin**  >  **rolleri**oluşturma ' ya gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Betik Oluşturma

#### <a name="additional-data-warehouse-v10-properties---6125732----"></a>Ek veri ambarı v 1.0 özellikleri<!-- 6125732  -->
Intune veri ambarı v 1.0 kullanılarak ek özellikler mevcuttur. Aşağıdaki özellikler artık [cihazlar](../developer/reports-ref-devices.md#devices) varlığı aracılığıyla kullanıma sunulmuştur:
- `ethernetMacAddress` -Bu cihazın benzersiz ağ tanımlayıcısı.
- `office365Version` -Cihaza yüklü Office 365 sürümü.

Aşağıdaki özellikler artık [Devicepropertygeçmişin](../developer/reports-ref-devices.md#devicepropertyhistories) varlığı aracılığıyla kullanıma sunulmuştur:
- `physicalMemoryInBytes` -Bayt cinsinden fiziksel bellek.
- `totalStorageSpaceInBytes` -Bayt cinsinden toplam depolama kapasitesi.

Daha fazla bilgi için bkz. [Microsoft Intune veri ambarı API 'si](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>06 Temmuz 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Android 'de Şirket Portalı ve Intune uygulamalarında cihaz simgelerine güncelleştirme<!-- 6057023 -->
Android cihazlarda Şirket Portalı ve Intune uygulamalarındaki cihaz simgelerini, daha modern bir görünüm oluşturmak ve Microsoft 'un akıcı tasarım sistemiyle uyum sağlamak için güncelleştirdik. İlgili bilgiler için bkz. [iOS/ıpados ve macOS için şirket portalı App 'teki simgelere güncelleştirme](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>iOS Şirket Portalı, Apple 'ın Kullanıcı benzeşimi olmadan otomatik cihaz kaydını destekleyecektir<!-- 7282707 --> 
İOS Şirket Portalı, artık Apple 'ın otomatik cihaz kaydı kullanılarak kaydedilmiş cihazlarda atanmış bir Kullanıcı gerekmeden desteklenmektedir. Son Kullanıcı iOS Şirket Portalı, cihaz benzeşimi olmadan kaydedilen bir iOS/ıpados cihazında birincil kullanıcı olarak kurmak için oturum açabilir. Otomatik cihaz kaydı hakkında daha fazla bilgi için bkz. [Apple 'ın otomatik cihaz kaydı Ile iOS/ıpados cihazlarını otomatik olarak kaydetme](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Kiracı iliştirme: Yönetim merkezinde ConfigMgr istemci ayrıntıları (Önizleme)<!-- 7552762 -->

Artık Microsoft Endpoint Manager Yönetim Merkezi 'nde belirli bir cihaz için Koleksiyonlar, sınır grubu üyeliği ve gerçek zamanlı istemci bilgilerini içeren ConfigMgr istemci ayrıntılarını görebilirsiniz. Daha fazla bilgi için bkz. [kiracı iliştirme: ConfigMgr istemci ayrıntıları Yönetim Merkezi (Önizleme)](../../configmgr/tenant-attach/client-details.md).

## <a name="week-of-june-22-2020"></a>22 Haziran 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Intune için yeni kullanılabilir korumalı uygulamalar<!-- 7248952 -->
Aşağıdaki korumalı uygulamalar artık kullanılabilir:
- BlueJeans görüntülü konferans
- Intune için Cisco Jabber
- Intune için Tableau Mobile
- Intune için sıfır

Korumalı uygulamalar hakkında daha fazla bilgi için bkz. [Microsoft Intune korumalı uygulamalar](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Kullanıcı üretkenliğini artırmak ve BT destek maliyetlerini azaltmak için Endpoint Analytics 'i kullanın<!-- 5653063 --> 
Sonraki hafta boyunca bu özellik kullanıma sunulacaktır. Kullanıcı üretkenliğini geliştirmek ve Kullanıcı deneyimine yönelik Öngörüler sunarak BT destek maliyetlerini azaltmak için Endpoint Analytics amaçlar. İçgörüler, BT 'nin son kullanıcı deneyimini öngörülü destekle en uygun hale getirmesine ve yapılandırma değişikliklerinin Kullanıcı etkisini değerlendirerek Kullanıcı deneyimine yönelik gerilemeleri algılamasına olanak tanır. Daha fazla bilgi için bkz. [Endpoint Analytics önizlemesi](https://aka.ms/uea).

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Komut dosyası paketlerini kullanarak Son Kullanıcı cihaz sorunlarını önceden düzelt<!-- 5933328 -->
Kuruluşunuzdaki en önemli destek sorunlarını önceden bulmak ve gidermek için, Son Kullanıcı cihazlarında betik paketleri oluşturup çalıştırabilirsiniz. Betik paketlerinin dağıtımı, destek çağrılarını azaltmanıza yardımcı olur. Kendi betik paketlerinizi oluşturmayı seçin veya yazdığımız ve destek biletlerini azaltmak için ortamımızda kullandığımız komut dosyası paketlerinden birini dağıtın. Intune, dağıtılan betik paketlerinizin durumunu görmenizi ve algılama ve düzeltme sonuçlarını izlemenizi sağlar. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **raporlar**  >  **Endpoint Analytics**  >  **proaktif**düzeltmeler ' i seçin. Daha fazla bilgi için bkz. [proaktif](https://aka.ms/uea_prs)düzeltmeler.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Android için uyumluluk ilkelerinde Microsoft Defender ATP kullanma<!-- 4425686  -->

Artık Intune 'U [Android cihazları Microsoft Defender Gelişmiş tehdit koruması](../protect/advanced-threat-protection-configure.md#onboard-devices) (MICROSOFTDEFENDER ATP) uygulamasına eklemek için kullanabilirsiniz. Kayıtlı cihazlarınız eklendi olduktan sonra, Android için uyumluluk ilklarınız Microsoft Defender ATP 'den *tehdit düzeyi* sinyallerini kullanabilir. Bunlar, daha önce Windows 10 cihazlarında kullanabileceğiniz sinyallerdir.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Android cihazlar için Defender ATP Web korumasını yapılandırma<!-- 6185563  -->

Android cihazlar için Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) kullandığınızda, [Microsoft Defender ATP Web koruması](../protect/advanced-threat-protection-manage-android.md) 'nı, kimlik avı taraması özelliğini devre dışı bırakmak için yapılandırabilir veya taramanın VPN kullanmasını engelleyebilirsiniz.

Android cihazınızın Intune 'a nasıl oluşturulduğuna bağlı olarak, aşağıdaki seçenekler kullanılabilir:

- Android Cihaz Yöneticisi-Web Koruması özelliğini devre dışı bırakmak veya taramalar sırasında yalnızca VPN 'lerin kullanımını devre dışı bırakmak için özel OMA-URI ayarlarını kullanın.
- Android kurumsal iş profili-tüm Web koruması yeteneklerini devre dışı bırakmak için bir uygulama yapılandırma profili ve yapılandırma Tasarımcısı kullanın.

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>15 Haziran 2020 (2006 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Yönetilen uygulamalar için telekomünikasyon veri aktarımı koruması<!-- 6884491  -->
Korumalı bir uygulamada köprülü telefon numarası algılandığında, Intune, sayının bir çevirici uygulamasına aktarılmasını sağlayan bir koruma ilkesinin uygulanıp uygulanmadığı kontrol eder. İlke ile yönetilen bir uygulamadan başlatıldığında bu tür bir içerik aktarımını nasıl işleyebileceğini seçebilirsiniz. Microsoft Endpoint Manager 'da bir uygulama koruma ilkesi oluştururken, **Kuruluş verilerini diğer uygulamalara gönder**' den yönetilen bir uygulama seçeneği belirleyin ve ardından Iletişim **verilerini aktarma**seçeneğini belirleyin. Bu veri koruma ayarı hakkında daha fazla bilgi için, Microsoft Intune ve [iOS uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-ios.md) ['nda Android uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-android.md) bölümüne bakın. 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Şirket Portalı Azure AD kurumsal ve Office Online uygulamalarının birleştirilmiş teslimi<!-- 7414033  -->
Intune 'un **Özelleştirme** bölmesinde Şirket portalı hem **Azure AD kurumsal uygulamalarını** hem de **Office Online uygulamalarını** **gizleme** veya **gösterme** seçeneğini belirleyebilirsiniz. Her Son Kullanıcı tüm uygulama kataloglarını seçilen Microsoft hizmetinden görürler. Varsayılan olarak, her bir ek uygulama kaynağı **gizleyecek**şekilde ayarlanır. Bu özellik ilk olarak Şirket Portalı Web sitesinde, izlenmesi beklenen Windows Şirket Portalı desteğiyle etkili olacaktır. Bu yapılandırma ayarını bulmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **Kiracı Yönetimi**  >  **özelleştirmesi** ' nı seçin. İlgili bilgiler için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>MacOS kayıt deneyimi için Şirket Portalı geliştirmeleri<!-- 6444452  -->
MacOS kayıt deneyiminin Şirket Portalı, iOS kayıt deneyimi için Şirket Portalı daha yakından hizalanan daha basit bir kayıt işlemine sahiptir. Cihaz kullanıcıları şunları görür:  
- Bir uyleyici Kullanıcı arabirimi.  
- İyileştirilmiş bir kayıt denetim listesi.  
- Cihazlarını nasıl kaydedebileceğinize ilişkin daha net yönergeler.  
- Gelişmiş sorun giderme seçenekleri.  

Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>İOS/ıpados ve macOS şirket portallarının cihazlar sayfasında geliştirmeler<!-- 6055001 -->
İOS/ıpados ve Mac kullanıcıları için uygulama deneyimini geliştirmek üzere Şirket Portalı **cihazları** sayfasında değişiklikler yaptık. Daha modern bir görünüm oluşturmaya ek olarak, kullanıcıların cihaz durumunu görebilmesi daha kolay olması için, tanımlı bölüm üst bilgilerine sahip tek bir sütun altındaki cihaz ayrıntılarını yeniden güncelleştirdik. Ayrıca, cihazları uyumsuz olan kullanıcılar için daha net mesajlaşma ve sorun giderme adımları ekledik. Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md). Bir cihazı el ile eşitlemek için bkz. [iOS cihazınızı El Ile eşitleme](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>İOS/ıpados Şirket Portalı uygulaması için bulut ayarı<!-- 7071303  -->
İOS/ıpados Şirket Portalı için yeni bir **bulut** ayarı, kullanıcıların kimlik doğrulamasını kuruluşunuz için uygun buluta yönlendirmelerini sağlar. Varsayılan olarak, ayar **Otomatik**olarak yapılandırılır, bu da kimlik doğrulaması otomatik olarak kullanıcının cihazı tarafından algılanır. Kuruluşunuzun kimlik doğrulaması otomatik olarak algılanan buluttan başka bir buluta yönlendirilmelidir (örneğin, kamu veya kamu), kullanıcılarınız > **Şirket portalı**Cloud **Settings** uygulamasını seçerek uygun bulutu el ile seçebilir  >  **Cloud**. Kullanıcılarınız yalnızca başka bir cihazdan oturum açtıklarında **bulut** ayarını **Otomatik** olarak değiştirmeli ve uygun bulut cihaz tarafından otomatik olarak algılanmaz. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Yinelenen Apple VPP belirteçleri<!-- 7101606  -->
Aynı **belirteç konumuna** sahıp Apple VPP belirteçleri artık **yinelenen** olarak işaretlenir ve yinelenen belirteç kaldırıldığında yeniden eşitlenebilir. Hala yinelenen olarak işaretlenmiş belirteçler için lisans atayabilir ve iptal edebilirsiniz. Ancak, bir belirteç yinelenen olarak işaretlendikten sonra satın alınan yeni uygulamalar ve Kitaplar için lisanslar yansıtılmayabilir. Kiracınız için Apple VPP belirteçlerini bulmak için, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nden **kiracı yönetim**bağlayıcıları ' nı seçin  >  **ve**  >  **Apple VPP belirteçlerini**belirteçler yapın. VPP belirteçleri hakkında daha fazla bilgi için bkz. [Microsoft Intune ile Apple Volume Purchase program aracılığıyla satın alınan iOS ve macOS uygulamalarını yönetme](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>MacOS cihazlarında Wi-Fi profillerindeki EAP-TLS kimlik doğrulaması için birden çok kök sertifika ekleme<!-- 2077871  -->

MacOS cihazlarında, bir Wi-Fi profili oluşturabilir ve Genişletilebilir Kimlik Doğrulama Protokolü (EAP) kimlik doğrulama türünü seçebilirsiniz (**cihaz**  >  **yapılandırma profilleri**for  >  **Create profile**  >  **macOS** platform > **Wi-> Fi** **Wi-Fi type** ' y i seçin.

EAP **türünü** **EAP-TLS**, **EAP-TTLS**veya **PEAP** kimlik doğrulaması olarak ayarladığınızda, birden çok kök sertifika ekleyebilirsiniz. Daha önce yalnızca bir kök sertifika ekleyebilirsiniz.

Yapılandırabileceğiniz ayarlar hakkında daha fazla bilgi için, bkz. [Microsoft Intune macOS cihazları Için Wi-Fi ayarları ekleme](../configuration/wi-fi-settings-macos.md).

Aşağıdakiler cihazlar için geçerlidir:
- Mac OS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Windows 10 ve daha yeni cihazlarda Wi-Fi profilleriyle PKCS sertifikaları kullanma<!-- 3246388   -->
Windows Wi-Fi profillerinin kimlik doğrulaması için SCEP sertifikaları (**cihaz yapılandırma**  >  **profilleri**  >  **Create profile**  >  **Windows 10 ve üzeri** için profil oluşturma > **Wi-Fi** for platform > **Enterprise**  >  **EAP Type**). Şimdi, Windows Wi-Fi profilleriniz ile PKCS sertifikaları kullanabilirsiniz. Bu özellik, kiracınızdaki yeni veya mevcut PKCS sertifika profillerini kullanarak Wi-Fi profillerinin kimlik doğrulamasından geçmesini sağlar. 

Yapılandırabileceğiniz Wi-Fi ayarları hakkında daha fazla bilgi için, bkz. [Intune 'Da Windows 10 ve üzeri cihazlar Için Wi-Fi ayarları ekleme](../configuration/wi-fi-settings-windows.md).

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>MacOS cihazları için kablolu ağ cihaz yapılandırma profilleri<!-- 3508686  -->
Kablolu ağları yapılandıran yeni bir MacOS cihaz yapılandırma profili vardır (**cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  platform için**MacOS profil oluşturma MacOS** for profile için **kablolu ağ** >). Kablolu ağları yönetmek için 802.1 x profilleri oluşturmak ve bu kablolu ağları macOS cihazlarınıza dağıtmak için bu özelliği kullanın.

Bu özellik hakkında daha fazla bilgi için bkz. [macOS cihazlarda kablolu ağlar](../configuration/wired-networks-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- Mac OS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Tam olarak yönetilen Android Kurumsal cihazları için varsayılan başlatıcı olarak Microsoft başlatıcısı 'nı kullanın<!-- 4927976   -->
Android kurumsal cihaz sahibi cihazlarda, Microsoft başlatıcısı 'nı tam olarak yönetilen cihazlar için varsayılan başlatıcı olarak**ayarlayabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Android Enterprise** profil > **Device owner**  >  **cihaz deneyimi**için cihaz sahibi**cihaz kısıtlamalarına** >). Diğer tüm Microsoft Başlatıcı ayarlarını yapılandırmak için [uygulama yapılandırma ilkelerini](../apps/configure-microsoft-launcher.md)kullanın. 

Ayrıca, **cihaz deneyimine**yeniden adlandırılmakta olan **adanmış cihazlar** dahil bazı farklı Kullanıcı Arabirimi güncelleştirmeleri de vardır.

Kısıtlayabilecek tüm ayarları görmek için bkz. [Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak Için Android kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md). 

Aşağıdakiler cihazlar için geçerlidir:
- Android kurumsal cihaz sahibi tam olarak yönetilen cihazlar (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>İOS Şirket Portalı uygulamasını bir oturum açma/kapatma uygulaması olacak şekilde yapılandırmak için otonom tek uygulama modu ayarlarını kullanın<!-- 7055619   -->
İOS/ıpados cihazlarında, uygulamaları otonom tek uygulama modunda (ASAM) çalışacak şekilde yapılandırabilirsiniz. Artık Şirket Portalı uygulama ASAM 'yi destekliyor ve "oturum aç/oturumu Kapat" uygulaması olacak şekilde yapılandırılabilir. Bu modda, kullanıcıların cihazdaki diğer uygulamaları ve ana ekran düğmesini kullanabilmesi için Şirket Portalı uygulamada oturum açması gerekir. Şirket Portalı uygulamasında oturum açtıklarında, cihaz tek uygulama moduna geri döner ve Şirket Portalı uygulamasındaki kilitler.

Şirket portalı, Asam içinde olacak şekilde yapılandırmak için, bkz. **cihaz**  >  **yapılandırma profilleri**  >  **profil oluşturma**  >  **iOS/ıpados** , **tek uygulama modu**> profil için **cihaz kısıtlamaları > cihaz kısıtlamaları** .

Daha fazla bilgi için bkz. [otonom tek uygulama modu (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) ve [tek uygulama modu](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (Apple 'ın Web sitesini açar).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>MacOS cihazlarında içerik önbelleğe almayı yapılandırma<!-- 7106872   -->
MacOS cihazlarında, içerik önbelleğe almayı yapılandıran bir yapılandırma profili**oluşturabilirsiniz (cihaz**  >  **yapılandırma profilleri**profil  >  için MacOS**profili oluşturma**  >  **MacOS** > for profile için **cihaz özellikleri** ). Önbelleği silmek, paylaşılan önbelleğe izin vermek, diskte önbellek sınırı ayarlamak ve daha fazlasını yapmak için bu ayarları kullanın.

İçerik önbelleğe alma hakkında daha fazla bilgi için bkz. [contentcaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (Apple 'ın Web sitesini açar).

Yapılandırabileceğiniz ayarları görmek için [Intune 'Da MacOS cihaz özelliği ayarları](../configuration/macos-device-features-settings.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:
- Mac OS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Android Enterprise üzerinde OEMConfig kullanarak yeni şema ayarları ekleme ve mevcut şema ayarlarını arama<!-- 6394386   -->
Intune 'da, Android kurumsal cihazlarındaki ayarları yönetmek için oemconfig kullanabilirsiniz (**cihaz**  >  **yapılandırma profilleri**Intune için bir  >  **profil**  >  **Android Enterprise** for platform > **için bkz** .). **Yapılandırma tasarımcısını**kullandığınızda, uygulama şemasındaki özellikler gösterilir. Şimdi, **yapılandırma tasarımcısında**şunları yapabilirsiniz:

- Uygulama şemasına yeni ayarlar ekleyin.
- Uygulama şemasında yeni ve var olan ayarları arayın.

Intune 'daki OEMConfig profilleri hakkında daha fazla bilgi için, bkz. [Microsoft Intune 'de oemconfig Ile Android Kurumsal cihazları kullanma ve yönetme](../configuration/android-oem-configuration-overview.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android Kurumsal

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Paylaşılan iPad cihazlarda paylaşılan iPad geçici oturumlarını engelle<!-- 6613794  -->
Intune 'da, paylaşılan iPad cihazlarında geçici oturumları engelleyen, paylaşılan yeni bir **iPad geçici oturumları** ayarı**vardır (cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **iOS/ıpados** > profil türü > **paylaşılan iPad**için **cihaz kısıtlamaları** ). Etkinleştirildiğinde, son kullanıcılar Konuk hesabını kullanamaz. Yönetilen Apple KIMLIĞI ve parolasıyla cihazda oturum açması gerekir. 

Daha fazla bilgi için bkz. [iOS ve ıpados cihaz ayarları, özelliklere izin vermek veya erişimi kısıtlamak](../configuration/device-restrictions-ios.md).

Aşağıdakiler cihazlar için geçerlidir:
- İOS/ıpados 13,4 ve daha yeni çalıştıran paylaşılan iPad cihazları

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>Kendi cihazlarını getir, dağıtmak için VPN kullanabilir<!--5015344  -->
Yeni Autopilot profili **etki alanı bağlantısını atla onay** geçişi, üçüncü taraf Win32 VPN istemcinizi kullanarak kurumsal ağınıza erişim olmadan karma Azure AD JOIN cihazlarını dağıtmanıza olanak tanır. Yeni geçişi görmek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**   >  **Windows**  >  **Windows kayıt**  >  **dağıtım profilleri**  >  **profil oluşturma**öncesi  >  **deneyim (OOBE)** bölümüne gidin.

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Kayıt durumu sayfası profilleri, cihaz gruplarına ayarlanabilir<!--3952138 -->
Daha önce, kayıt durumu sayfası (ESP) profilleri yalnızca Kullanıcı gruplarını hedefleyebilir. Artık, bunları hedef cihaz gruplarına da ayarlayabilirsiniz. Daha fazla bilgi için bkz. [kayıt durumu sayfası ayarlama](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Otomatik cihaz kaydı Eşitleme hataları<!-- 6988214 -->
İOS/ıpados ve macOS cihazları dahil olmak üzere yeni hatalar raporlanır
- Telefon numarasında geçersiz karakterler veya bu alan boş. 
- Profil için geçersiz veya boş yapılandırma adı. 
- Geçersiz/zaman aşımına uğradı imleç değeri veya imleç bulunamadı.
- Reddedilen veya süre dolma belirteci. 
- Departman alanı boş veya uzunluk çok uzun. 
- Profil Apple tarafından bulunmadı ve yeni bir tane oluşturulması gerekiyor. 
- Cihazların durumunu gördüğünüz genel bakış sayfasına, kaldırılan bir Apple Business Manager cihazı sayısı eklenecektir.

#### <a name="shared-ipads-for-business--6367326-----"></a>Iş için paylaşılan IPad 'ler<!--6367326   -->
Birden çok çalışanın cihaz paylaşabilmesi için, Intune ve Apple Business Manager 'ı kullanarak paylaşılan iPad 'i kolayca ve güvenli bir şekilde ayarlayabilirsiniz. Apple 'ın [paylaşılan iPad](https://developer.apple.com/education/shared-ipad/) 'i, Kullanıcı verilerini korurken birden çok kullanıcı için kişiselleştirilmiş bir deneyim sağlar. Yönetilen bir Apple KIMLIĞI kullanarak, kullanıcılar kuruluşlarındaki paylaşılan iPad 'de oturum açtıktan sonra uygulamalarına, verilerine ve ayarlarına erişebilirler. Paylaşılan iPad, Federasyon kimlikleriyle birlikte çalışmaktadır.

Bu özelliği görmek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **iOS**  >  **iOS kaydı**  >  **kayıt programı belirteçleri**' ne gidin  >  **bir belirteç**  >  **profilleri**seçin  >  **iOS profili oluştur**  >  **iOS**. **Yönetim ayarları** sayfasında, **Kullanıcı benzeşimi olmadan kaydet** ' i seçin ve **paylaşılan iPad** seçeneğini görürsünüz.

Şunları gerektirir: ıpados 13,4 ve üzeri. Bu sürüm, kullanıcıların yönetilen bir Apple KIMLIĞI olmadan bir cihaza erişebilmeleri için paylaşılan iPad ile geçici oturumlar için destek ekledi. Oturum kapatma sonrasında cihaz tüm Kullanıcı verilerini siler, böylece cihaz kullanıma hemen kullanılabilir hale gelir ve cihaz temizleme gereksinimini ortadan kaldırır. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Apple 'ın otomatik cihaz kaydı için güncelleştirilmiş Kullanıcı arabirimi<!--7430322 -->
Kullanıcı arabirimi Apple 'ın Aygıt Kayıt Programı Apple terminolojisini yansıtacak şekilde otomatik cihaz kaydına değiştirecek şekilde güncelleştirilmiştir.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>MacOS için cihaz uzaktan kilitleme PIN 'i kullanılabilir<!--7281557   -->
MacOS cihaz uzaktan kilitleme PIN 'lerinin kullanılabilirliği 7 günden 30 güne yükselmiştir.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Ortak yönetilen cihazlarda birincil kullanıcıyı değiştirme<!--7319183  -->
Bir cihazın birincil kullanıcısını, ortak yönetilen Windows cihazları için değiştirebilirsiniz. Bunu bulma ve değiştirme hakkında daha fazla bilgi için bkz. [Intune cihazının birincil kullanıcısını bulma](../remote-actions/find-primary-user.md). Bu özellik önümüzdeki birkaç hafta içinde kademeli olarak kullanıma sunulacaktır.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Intune birincil kullanıcı ayarı da Azure AD Owner özelliğini ayarlar<!--7319227 -->
Bu yeni özellik, yeni kaydedilen karma Azure AD 'ye katılmış cihazlarda sahip özelliğini Intune birincil kullanıcısının ayarlandığı anda otomatik olarak ayarlar. Birincil Kullanıcı hakkında daha fazla bilgi için bkz. [Intune cihazının birincil kullanıcısını bulma](../remote-actions/find-primary-user.md).

Bu, kayıt işlemine yapılan bir değişiklik ve yalnızca yeni kaydedilen cihazlar için geçerlidir. Mevcut karma Azure AD 'ye katılmış cihazlar için Azure AD Owner özelliğini el ile güncelleştirmeniz gerekir. Bunu yapmak için [birincil Kullanıcı Değiştir özelliğini](../remote-actions/find-primary-user.md#change-a-devices-primary-user) veya [bir komut dosyasını](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)kullanabilirsiniz.

Windows 10 cihazları karma Azure Azure dizini 'ne katıldığında, cihazın ilk kullanıcısı Endpoint Manager 'da birincil Kullanıcı olur.  Şu anda Kullanıcı ilgili Azure AD cihaz nesnesinde ayarlanmadı. Bu, *sahip* özelliğini Microsoft Endpoint Manager Yönetim Merkezi 'ndeki *birincil Kullanıcı* ÖZELLIĞI ile bir Azure AD portalından karşılaştırırken tutarsızlığa neden olur. Azure AD Owner özelliği, BitLocker Kurtarma anahtarlarına erişimin güvenliğini sağlamak için kullanılır. Özelliği, karma Azure AD 'ye katılmış cihazlarda doldurulmamış. Bu sınırlama, Azure AD 'den BitLocker kurtarma 'nın self servis kurulumunu engeller. Yakında sunulacak olan bu özellik bu kısıtlamayı çözer.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>MacOS cihazları için dosya Kasası 2 şifrelemesi sırasında, kurtarma anahtarını kullanıcılardan gizle<!-- 5459801  -->
[MacOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) şablonu Içindeki *filekasası* kategorisine yeni bir ayar ekledik: **Kurtarma anahtarını gizleyin**. Bu ayar, Filekasa2 şifrelemesi sırasında son kullanıcıdan kişisel anahtarı gizler. 

Şifrelenmiş bir macOS cihazının kişisel kurtarma anahtarını görüntülemek için, cihaz kullanıcısı aşağıdaki konumlardan birine gidebilir ve macOS cihazı için *Kurtarma anahtarını al* ' a tıklayabilirsiniz: 

- İOS/ıpados Şirket portalı uygulaması
- Intune uygulaması
- Şirket portalı web sitesi
- Android şirket portalı uygulaması

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Android 'de tam olarak yönetilen ve Outlook ile S/MIME imzalama ve şifreleme sertifikaları desteği<!--5896415   -->
Artık Android kurumsal tam olarak yönetilen cihazlarda Outlook ile S/MIME imzalama ve şifreleme için sertifikaları kullanabilirsiniz.

Bu, diğer Android sürümleri (Android 'de Outlook ile S/MIME imzalama ve şifreleme sertifikaları desteği) için geçen aya eklenen desteğe genişletilir. Bu sertifikaları SCEP ve PKCS içeri aktarılan sertifika profillerini kullanarak sağlayabilirsiniz.

Bu destek hakkında daha fazla bilgi için Exchange belgelerindeki [iOS ve Android Için Outlook 'Ta duyarlılık etiketleme ve koruma](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) bölümüne bakın.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Uyumsuzluk için e-postalara Şirket Portalı Destek Web sitenizin bağlantısını ekleyin<!-- 7225498    -->
Uyumsuzluk için e-posta bildirimleri göndermek üzere [bir bildirim iletisi şablonu yapılandırdığınızda](../protect/actions-for-noncompliance.md#create-a-notification-message-template) , Şirket portalı Web sitenizin bağlantısını otomatik olarak eklemek için yeni ayar **Şirket portalı Web sitesi bağlantısını** kullanın. Bu seçenek *etkin*olarak ayarlandığında, bu şablona dayalı e-posta alan uyumlu olmayan cihazlara sahip kullanıcılar, cihazlarının neden uyumlu olmadığı hakkında daha fazla bilgi edinmek için bir Web sitesi açmak üzere bağlantıyı kullanabilir. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Lisanslama

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Yöneticiler artık Microsoft Endpoint Manager Yönetici konsoluna erişmek için bir Intune lisansı gerektirmez<!--1335430 -->
Artık, yöneticilerin MEM Yönetici Konsolu ve sorgu grafiği API 'Lerine erişmesi için Intune lisans gereksinimini kaldıran kiracı genelinde bir geçiş ayarlayabilirsiniz. Lisans gereksinimini kaldırdıktan sonra, bunu hiçbir şekilde yeniden devreye sokmanız gerekir. 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Betikler 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>MacOS cihazlarında kabuk betiklerinin kullanılabilirliği<!-- 7134839  -->
MacOS cihazları için kabuk betikleri artık kamu bulutu ve Çin müşterileri tarafından kullanılabilir. Kabuk betikleri hakkında daha fazla bilgi için bkz. [Intune 'Da macOS cihazlarında Shell betikleri kullanma](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>8 Haziran 2020 haftası   

### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>İOS/ıpados için Şirket Portalı bilgi ekranı güncelleştirmeleri <!--7032452 -->
İOS/ıpados için Şirket Portalı bir bilgilendirici ekran, yöneticinin cihazları neleri görebileceğini ve ne yapabileceğini daha iyi açıklamak için güncelleştirilmiştir. Bu açıklamalar yalnızca şirkete ait cihazlar içindir. Yalnızca metin güncelleştirildi, yöneticinin Kullanıcı cihazlarını neleri görebileceklerini veya yapabileceğini hiçbir gerçek değişiklik yapılmadı. Güncelleştirilmiş ekranları görmek için [Intune son kullanıcı uygulamaları Için Kullanıcı Arabirimi güncelleştirmeleri](./whats-new-app-ui.md)' ne gidin.

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Güncelleştirilmiş Android UYGULAMASı koşullu başlatma Son Kullanıcı deneyimi<!-- 5736084 -->
Android Şirket Portalı 2006 sürümünde, 2005 sürümündeki güncelleştirmelerde derleme yapan değişiklikler vardır. 2005 ' de, bir uygulama koruma ilkesi tarafından uyarı veren, blok veya temizleme yapan son Android cihaz kullanıcılarının, uyarı, blok veya silme nedeninizi ve sorunları düzeltmek için gereken adımları açıklayan bir tam sayfa mesajı görürsünüz. 2006 ' de, uygulama erişiminin engellenmesine neden olan sorunları düzeltmek için bir uygulama koruma ilkesi atanan Android uygulamalarının ilk kullanıcıları, kılavuzlu bir akış aracılığıyla alınacaktır. 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>25 Mayıs 2020 haftası

### <a name="app-management"></a>Uygulama yönetimi

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>ARM64 cihazlarda Windows 32-bit (x86) uygulamaları<!-- 5477661 -->
ARM64 cihazlara sunulan olarak dağıtılan Windows 32-bit (x86) uygulamaları artık Şirket Portalı görüntülenecektir. Windows 32-bit uygulamaları hakkında daha fazla bilgi için bkz. [Win32 uygulama yönetimi](../apps/apps-win32-app-management.md).

#### <a name="windows-company-portal-app-icon---7114635---"></a>Windows Şirket Portalı uygulaması simgesi<!-- 7114635 -->
Windows Şirket Portalı uygulamasının simgesi güncelleştirildi. Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>18 Mayıs 2020 haftası

### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>İOS/ıpados ve macOS için Şirket Portalı App 'teki simgelere güncelleştirme<!--6057697 -->
Çift ekran cihazlarda desteklenen ve Microsoft akıcı tasarım sistemiyle hizalanan daha modern bir görünüm oluşturmak için Şirket Portalı simgeleri güncelleştirdik. Güncelleştirilmiş simgeleri görmek için [Intune son kullanıcı uygulamaları Için Kullanıcı Arabirimi güncelleştirmeleri](./whats-new-app-ui.md)' ne gidin. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Cihazları Defender ATP 'ye eklemek için uç nokta algılama ve yanıt ilkesini kullanın<!-- 7130165  -->

Microsoft Defender Gelişmiş tehdit koruması (Defender ATP) dağıtımınız için cihaz eklemek ve yapılandırmak üzere [uç nokta algılama ve yanıt](../protect/endpoint-security-edr-policy.md) (EDR) için uç nokta güvenlik ilkesi kullanın. EDR, Intune (MDM) tarafından yönetilen Windows cihazları için ilkeyi ve Configuration Manager tarafından yönetilen Windows cihazları için ayrı bir ilkeyi destekler. 

Configuration Manager cihazlar için ilkeyi kullanmak üzere, [EDR ilkesini desteklemek için Configuration Manager ayarlamanız](../protect/tenant-attach-intune.md)gerekir. Kurulum şunları içerir:

- *Kiracı iliştirme*için Configuration Manager 'ı yapılandırın.
- EDR ilkeleri desteğini etkinleştirmek için Configuration Manager için konsol içi bir güncelleştirme yükler. Bu güncelleştirme yalnızca *kiracı iliştirme*'yi etkinleştirilen Hiyerarşiler için geçerlidir.
- Cihaz koleksiyonlarınızı, hiyerarşinizi Microsoft Uç Nokta Yöneticisi Yönetim Merkezi olarak bir biçimde eşitler.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>11 Mayıs 2020 (2005 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Şirket Portalı self servis cihaz eylemlerini özelleştirme<!--4393379 -->
Şirket Portalı uygulamasında ve Web sitesinde son kullanıcılara gösterilen kullanılabilir self servis cihaz eylemlerini özelleştirebilirsiniz. İstenmeyen cihaz eylemlerini önlemeye yardımcı olmak için, **Kiracı Yönetimi**özelleştirmesi ' nı seçerek bu ayarları Şirket portalı uygulama için yapılandırabilirsiniz  >  **Customization**. Aşağıdaki eylemler kullanılabilir:
- Kurumsal Windows cihazında **Kaldır** düğmesini gizleyin.
- Kurumsal Windows cihazlarında **sıfırlama** düğmesini gizleyin.
- Kurumsal iOS cihazlarında **sıfırlama** düğmesini gizleyin.
- Kurumsal iOS cihazlarda **Kaldır** düğmesini gizleyin.
Daha fazla bilgi için, [Şirket portalı Kullanıcı self servis cihaz eylemleri](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)bölümüne bakın.

#### <a name="auto-update-vpp-available-apps---3640511----"></a>VPP ile kullanılabilen uygulamaları otomatik güncelleştirme<!-- 3640511  -->
Toplu satın alma programı (VPP) kullanılabilir uygulamalar olarak yayımlanan uygulamalar, **otomatik uygulama GÜNCELLEŞTIRMELERI** VPP belirteci için etkinleştirildiğinde otomatik olarak güncelleştirilir. Daha önce, VPP 'nin kullanabildiği uygulamalar otomatik olarak güncelleştirmedi. Bunun yerine, son kullanıcıların Şirket Portalı gitmesi ve daha yeni bir sürüm varsa uygulamayı yeniden yüklemesi gerekiyordu. Gerekli uygulamalar otomatik güncelleştirmeleri desteklemeye devam eder.




#### <a name="android-company-portal-user-experience---5736084----"></a>Android Şirket Portalı Kullanıcı deneyimi<!-- 5736084  -->
Android Şirket Portalı 2005 sürümünde, bir uygulama koruma ilkesi tarafından uyarı veren, blok veya temizleme yapan Android cihazların son kullanıcıları yeni bir kullanıcı deneyimi görür. Son kullanıcılar, geçerli iletişim kutusu deneyimi yerine, uyarı, blok veya silme nedeninizi ve sorunu düzeltmek için gereken adımları açıklayan bir tam sayfa mesajı görür. Daha fazla bilgi için, bkz. Microsoft Intune [Android cihazları Için uygulama koruma deneyimi](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) ve [Android uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>MacOS için Şirket Portalı birden çok hesap desteği<!-- 5779449  -->
MacOS cihazlarındaki Şirket Portalı artık Kullanıcı hesaplarını önbelleğe alır, oturum açma daha kolay hale getirir. Kullanıcıların, uygulamayı her başlattığında artık Şirket Portalı oturum açması gerekmez. Ayrıca, birden çok kullanıcı hesabı önbelleğe alınmışsa, kullanıcıların kullanıcı adını girmesi gerekmiyorsa Şirket Portalı bir hesap seçici görüntülenir. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Yeni kullanılabilir korumalı uygulamalar<!-- 7060934   -->
Aşağıdaki korumalı uygulamalar artık kullanılabilir:
- Pano Incelemeleri
- Intune için Breezy
- Diyelim ki Intune Ile Ilgili
- Intune için ISEC7 mobil Exchange temsilcisi
- Intune için Lexmark
- Meetio Enterprise
- Microsoft beyaz tahta
- Şimdi Mobile-Intune®
- Qlik Sense Mobile 
- ServiceNow® Aracısı-Intune
- ServiceNow® ekleme-Intune
- Intune için smartcrypt
- Intune için kişi
- Avukatlar için sıfır e-posta

Korumalı uygulamalar hakkında daha fazla bilgi için bkz. [Microsoft Intune korumalı uygulamalar](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Şirket Portalı Intune belgelerini arama<!-- 1736480   -->
Artık doğrudan macOS uygulamasındaki Şirket Portalı Intune belgelerini arayabilirsiniz. Menü çubuğunda **Yardım**  >  **Ara** ' yı seçin ve sorularınızın yanıtlarını hızlı bir şekilde bulmak için aramanızın anahtar sözcüklerini girin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Zeköşeli Technologies cihazları için OEMConfig desteği geliştirmeleri<!-- 4184154 -->
Intune, Zeköşeli OEMConfig tarafından sunulan tüm özellikleri tam olarak destekler. Zeköşeli teknolojileri cihazlarını Android Enterprise ve OEMConfig ile yöneten müşteriler, birden çok OEMConfig profilini tek bir cihaza dağıtabilir. Müşteriler, Zeköşeli OEMConfig profillerinin durumu hakkında zengin raporlamayı da görüntüleyebilir.

Daha fazla bilgi için, bkz. [Microsoft Intune Zeköşeli cihazlara birden çok OEMConfig profili dağıtma](../configuration/oemconfig-zebra-android-devices.md).

Diğer OEM 'Ler için OEMConfig davranışında değişiklik yapılmaz.

Aşağıdakiler cihazlar için geçerlidir:
- Android Kurumsal
- OEMConfig 'i destekleyen zeköşeli teknolojiler cihazları. Destek ile ilgili belirli Ayrıntılar için Zeköşeli bağlantı kurun.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>MacOS cihazlarında sistem uzantılarını yapılandırma<!-- 6255624 -->
MacOS cihazlarında, çekirdek düzeyinde ayarları yapılandırmak için bir çekirdek uzantıları profili oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **macOS** for platform > Platform **uzantıları** for profile). Apple, çekirdek uzantılarını kullanımdan kaldırır ve gelecekteki sürümlerde sistem uzantıları ile değiştirmektir.

Sistem uzantıları Kullanıcı alanında çalışır ve çekirdeğe erişemez. Amaç, güvenliği artırmak ve daha fazla Son Kullanıcı denetimi sağlamak, ancak saldırıları çekirdek düzeyinde sınırlandırmaktır. Her iki çekirdek uzantısı ve sistem uzantısı, kullanıcıların işletim sisteminin yerel yeteneklerini genişleten uygulama uzantılarını yüklemelerine izin verir.

Intune 'da, hem çekirdek uzantılarını hem de sistem uzantılarını yapılandırabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **MacOS** for platform >, profil için **sistem uzantıları** ). Çekirdek uzantıları, 10.13.2 ve üzeri için geçerlidir. Sistem uzantıları 10,15 ve üzeri sürümler için geçerlidir. MacOS 10,15 ' den macOS 10.15.4, çekirdek uzantıları ve sistem uzantıları yan yana çalışabilir. 

MacOS cihazlarında bu uzantılar hakkında bilgi edinmek için bkz. [MacOS uzantıları ekleme](../configuration/kernel-extensions-overview-macos.md).

Aşağıdakiler cihazlar için geçerlidir:
- macOS 10,15 ve üzeri

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>MacOS cihazlarında uygulama ve işlem gizlilik tercihlerini yapılandırma<!-- 2934232   --> 
MacOS Catalina 10,15 sürümü sayesinde, Apple yeni güvenlik ve gizlilik iyileştirmeleri ekledi. Varsayılan olarak, uygulamalar ve süreçler Kullanıcı izni olmadan belirli verilere erişemez. Kullanıcılar onay sağlamıyorsa, uygulamalar ve süreçler çalışmayabilir. Intune, macOS 10,14 ve üstünü çalıştıran cihazlarda son kullanıcılar adına, BT yöneticilerinin veri erişimine izin vermesini veya bu izni vermemeyi sağlayan ayarlar için destek ekliyor. Bu ayarlar, uygulamaların ve işlemlerin düzgün şekilde çalışmaya devam etmesini ve istem sayısını azaltmasını sağlar. 

Yönetebileceğiniz ayarlar hakkında daha fazla bilgi için bkz. [MacOS Gizlilik Tercihleri](../configuration/device-restrictions-macos.md#privacy-preferences).

Aşağıdakiler cihazlar için geçerlidir:
- macOS 10,14 ve üzeri

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Kayıt kısıtlamaları kapsam etiketlerini destekler<!--4209550  -->
Artık, kayıt kısıtlamalarına kapsam etiketleri atayabilirsiniz. Bunu yapmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **Kayıt kısıtlamaları**  >  **oluşturma kısıtlaması**' na gidin. Her iki kısıtlama türünü de oluşturun ve **kapsam etiketleri** sayfasını görürsünüz. Daha fazla bilgi için bkz. [kayıt kısıtlamalarını ayarlama](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>HoloLens 2 cihazları için Autopilot desteği<!--6305220  -->
Windows Autopilot artık HoloLens 2 cihazlarını desteklemektedir. HoloLens için Autopilot kullanma hakkında daha fazla bilgi için bkz. [HoloLens 2 Için Windows Autopilot](/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>İOS için toplu olarak uzak eylemi Eşitle kullan<!--6440956  idmiss-->
Artık aynı anda en fazla 100 iOS cihazda Uzaktan eşitleme işlemini kullanabilirsiniz. Bu özelliği görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **tüm cihazlar**  >  **toplu cihaz eylemleri**' ne gidin. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Otomatik cihaz eşitleme aralığı, 12 saate kadar<!--3077535  -->
Apple 'ın otomatik cihaz kaydı için, Intune ile Apple Business Manager arasındaki otomatik cihaz eşitleme aralığı, 24 saatten 12 saate kadar azaltılır. Eşitleme hakkında daha fazla bilgi için bkz. [yönetilen cihazları eşitleme](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Android cihazlarda DıŞA ınpurebred için türetilmiş kimlik bilgileri desteği<!-- 6939073     -->
Artık Android kurumsal tam olarak yönetilen cihazlarda bulunan bir [türetilmiş kimlik bilgileri](../protect/derived-credentials.md) sağlayıcısı olarak, *Reberkred* 'yi kullanabilirsiniz. Destek, DıŞA Üfli Rebred için türetilmiş bir kimlik bilgisi almayı içerir. Uygulama kimlik doğrulaması, Wi-Fi, VPN veya S/MIME imzalama ve/veya şifrelemeyi destekleyen uygulamalarla şifreleme için türetilmiş bir kimlik bilgisi kullanabilirsiniz. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Uyumsuzluk için eylem olarak anında iletme bildirimleri gönder <!-- 1733150   -->
Artık, cihazları bir uyumluluk ilkesinin koşullarını karşılamadığında, kullanıcıya anında iletme bildirimi gönderen [uyumsuzluğa yönelik bir eylem](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) yapılandırabilirsiniz. Yeni eylem, **son kullanıcıya anında iletme bildirimi gönderiyor**ve Android ve iOS cihazlarında destekleniyor.

Kullanıcılar cihazlarından anında iletme bildirimini seçerken, neden uyumsuz oldukları hakkında ayrıntıları göstermek için Şirket Portalı veya Intune uygulaması açılır.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Uç nokta güvenlik içeriği ve yeni özellikler<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Intune [Endpoint Security](../protect/endpoint-security.md) belgeleri artık kullanılabilir. Microsoft Endpoint Manager Yönetim Merkezi 'nin uç nokta güvenlik düğümünde şunları yapabilirsiniz:

- Yönetilen cihazlarınıza odaklanmış güvenlik ilkeleri oluşturun ve dağıtın
- Microsoft Defender Gelişmiş tehdit koruması ile tümleştirmeyi yapılandırın ve güvenlik görevlerini yönetin ATP ekibiniz tarafından tanımlandığı şekilde risk altındaki cihazlarda riskleri düzeltmeye yardımcı olur
- Güvenlik temellerini yapılandırma
- Cihaz uyumluluğunu ve koşullu erişim ilkelerini yönetme
- Hem Intune hem de Configuration Manager istemci iliştirme için yapılandırıldığında Configuration Manager tüm cihazlarınızın uyumluluk durumunu görüntüleyin.

İçeriğin kullanılabilirliğine ek olarak, bu ay Endpoint Security için aşağıdakiler de yenidir:

- [**Uç nokta güvenlik ilkeleri**](../protect/endpoint-security-policy.md) **are out of** ***Önizleme*** aşamasındadır ve artık iki özel durum dışında, *genel kullanıma sunulan*üretim ortamlarında kullanıma hazırdır:

  - Yeni bir *genel önizlemede*, Windows 10 güvenlik duvarı Ilkesi Için [ **Microsoft Defender güvenlik duvarı kuralları** profili](../protect/endpoint-security-firewall-policy.md#firewall-profiles) ' ni kullanabilirsiniz. Bu profilin her örneğiyle, Microsoft Defender güvenlik duvarı profillerinizi karmaşıklama etmek için en fazla 150 güvenlik duvarı kuralı yapılandırabilirsiniz. 
  - Hesap koruması güvenlik ilkesi önizlemede kalır. 

- Artık [**bir uç nokta güvenlik ilkesi yinelemesi oluşturabilirsiniz**](../protect/endpoint-security-policy.md#duplicate-a-policy). Yinelemeler, özgün ilkenin ayarlar yapılandırmasını tutar, ancak yeni bir ad alır. Sonra yeni ilke örneği, yeni ilke örneğini eklemek üzere düzenlemeye kadar gruplara atamalar içermez. Aşağıdaki ilkeleri çoğaltabilirsiniz:
  - Virüsten Koruma
  - Disk şifrelemesi
  - Güvenlik duvarı
  - Uç nokta algılama ve yanıt
  - Saldırı yüzeyini azaltma
  - Hesap koruması

- Artık [**bir güvenlik taban çizgisi yinelemesi oluşturabilirsiniz**](../protect/security-baselines.md#duplicate-a-security-baseline). Yinelemeler özgün taban çizgisinin ayarlar yapılandırmasını tutar, ancak yeni bir ad alır. Yeni temel örnek, yeni temel örneği eklemek için düzenlenene kadar gruplara atamalar içermez.

- Endpoint Security virüsten koruma ilkesi için yeni bir rapor kullanılabilir: [**Windows 10 sağlıksız uç noktalar**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Bu rapor, uç nokta güvenlik virüsten koruma ilkenizi görüntülerken seçebileceğiniz yeni bir sayfasıdır. Rapor, MDM ile yönetilen Windows 10 cihazlarınızın virüsten koruma durumunu görüntüler.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Android 'de Outlook ile S/MIME imzalama ve şifreleme sertifikaları desteği<!-- 7207474  -->
Artık Android 'de Outlook ile S/MIME imzalama ve şifreleme için sertifikaları kullanabilirsiniz. Bu destek sayesinde, SCEP, PKCS ve PKCS içeri aktarılan sertifika profillerini kullanarak bu sertifikaları sağlayabilirsiniz. Aşağıdaki Android platformları desteklenir:

- Android kurumsal Iş profili
- Android Cihaz Yöneticisi

Android kurumsal tam olarak yönetilen cihazlar için destek yakında kullanıma sunulacak.

Bu destek hakkında daha fazla bilgi için Exchange belgelerindeki [iOS ve Android Için Outlook 'Ta duyarlılık etiketleme ve koruma](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) bölümüne bakın.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="device-reports-ui-update---6269408---"></a>Cihaz raporları Kullanıcı arabirimi güncelleştirmesi<!-- 6269408 -->
Raporlara genel bakış bölmesi şimdi bir **Özet** ve **rapor** sekmesi sağlar. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **raporlar**' ı seçin ve ardından **raporlar** sekmesini seçerek kullanılabilir rapor türlerini görüntüleyin. İlgili bilgiler için bkz. [Intune raporları](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Betik Oluşturma

#### <a name="macos-script-support---6376978----"></a>macOS betik desteği<!-- 6376978  -->
MacOS için betik desteği genel kullanıma sunuldu. Ayrıca, Apple 'ın otomatik cihaz kaydına (eski adıyla Aygıt Kayıt Programı) kaydedilmiş Kullanıcı tarafından atanan betikler ve macOS cihazları için destek ekledik. Daha fazla bilgi için bkz. [Intune 'Da macOS cihazlarında Shell betikleri kullanma](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>4 Mayıs 2020 haftası  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Android için Şirket Portalı, iş profili kaydından sonra kullanıcıların uygulamaları almasını sağlar <!-- 6103999 -->
Kullanıcıların uygulamaları bulmasını ve yüklemesini kolaylaştırmak için Şirket Portalı 'teki uygulama içi Kılavuzu geliştirdik. Kullanıcılar, iş profili yönetimine kaydolduktan sonra, Google Play 'in hatalı sürümünde önerilen uygulamaları nasıl bulabileceğinizi açıklayan bir ileti alır. [Android profili ile cihaz kaydetme](../user-help/enroll-device-android-work-profile.md) bölümündeki son adım yeni iletiyi gösterecek şekilde güncelleştirilmiştir. Kullanıcılar ayrıca soldaki Şirket Portalı çekmecede yeni bir **uygulamalar al** bağlantısı görür. Bu yeni ve geliştirilmiş deneyimlere yönelik bir yöntem oluşturmak için, **uygulamalar** sekmesi kaldırılmıştır. Güncelleştirilmiş ekranları görmek için [Intune son kullanıcı uygulamaları Için Kullanıcı Arabirimi güncelleştirmeleri](./whats-new-app-ui.md)' ne gidin. 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>20 Nisan 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri<!-- 6317104, CM3555758  -->
Microsoft Uç Nokta Yöneticisi tek bir konsolda Configuration Manager ve Intune 'U bir araya getiriyor. Configuration Manager sürüm 2002 ' den başlayarak, Configuration Manager cihazlarınızı bulut hizmetine yükleyebilir ve bunların Yönetim merkezinde üzerinde işlem yapabilirsiniz. Daha fazla bilgi için bkz. [Microsoft Endpoint Manager kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Microsoft Office 365 ProPlus yeniden adlandır<!-- 6368143 -->
Microsoft Office 365 ProPlus, **enterprise Microsoft 365 Apps**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Belgelerimizde, yaygın olarak Microsoft 365 uygulamalar olarak başvuracağız. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde uygulamalar Windows Ekle ' **yi seçerek uygulamalar**paketini bulabilirsiniz  >  **Windows**  >  **Add**. Uygulama ekleme hakkında daha fazla bilgi için bkz. [Microsoft Intune uygulama ekleme](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>13 Nisan 2020 (2004 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Android kurumsal cihazlarda Outlook için S/MIME ayarlarını yönetme<!-- 6517085   -->
Android Enterprise çalıştıran cihazlarda Outlook için S/MIME ayarını yönetmek üzere uygulama yapılandırma ilkelerini kullanabilirsiniz. Ayrıca, cihaz kullanıcılarının Outlook ayarları 'nda S/MIME 'yi etkinleştirmesine veya devre dışı bırakmasına izin verip vermeyeceğinizi de seçebilirsiniz. Android için uygulama yapılandırma ilkelerini kullanmak için, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) 'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen cihazlar**Ekle ' ye gidin. Outlook ayarlarını yapılandırma hakkında daha fazla bilgi için bkz. [Microsoft Outlook yapılandırma ayarları](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Yönetilen Google Play uygulamaları için yayın öncesi test<!-- 2681933  -->
[Uygulama ön sürümü testi için Google Play kapalı test izlerini](https://support.google.com/googleplay/android-developer/answer/3131213) kullanan kuruluşlar, bu parçaları Intune ile yönetebilir. Test yapmak için Google Play 'in ön üretim izlerine yayımlanan uygulamaları, pilot gruplara seçerek atayabilirsiniz. Intune 'da, bir uygulamanın kendisine yayımlanmış bir üretim öncesi derleme testi izlemesine sahip olup olmadığını ve bu izlemeyi Azure AD Kullanıcı veya cihaz grupları ' na atayabilmesini sağlayabilirsiniz. Bu özellik, şu anda desteklenen Android kurumsal senaryolarımız (iş profili, tam olarak yönetilen ve adanmış) için kullanılabilir. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar**  >  **Android**  >  **Ekle**' yi seçerek yönetilen bir Google Play uygulaması ekleyebilirsiniz. Daha fazla bilgi için bkz. [yönetilen Google Play kapatılan test parçalarıyla çalışma](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft ekipleri artık macOS için Office 365 Suite 'e eklenmiştir<!-- 5903936  -->
Microsoft Endpoint Manager 'da macOS için Microsoft Office atanan kullanıcılar artık mevcut Microsoft Office uygulamalarına (Word, Excel, PowerPoint, Outlook ve OneNote) ek olarak Microsoft ekipleri alacak. Intune, diğer Office macOS uygulamaları yüklü olan mevcut Mac cihazlarını algılar ve cihaz Intune ile bir dahaki sefer iade ettiğinde Microsoft ekipleri yüklemeye çalışır. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, MacOS için **Office 365 paketini** , **Apps**  >  **MacOS**  >  **Add**uygulamaları ' nı seçerek bulabilirsiniz. Daha fazla bilgi için bkz. [Microsoft Intune Ile macOS cihazlarına Office 365 atama](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Android uygulama yapılandırma ilkelerine güncelleştirme<!-- 6113334  -->
Android uygulama yapılandırma ilkeleri, yöneticilerin uygulama yapılandırma profili oluşturmadan önce cihaz kayıt türünü seçmesine izin verecek şekilde güncelleştirilmiştir. İşlev, kayıt türü (Iş profili veya cihaz sahibi) tabanlı sertifika profillerinin hesabına ekleniyor.  Bu güncelleştirme aşağıdakileri sağlar:

1. Yeni bir profil oluşturulduysa ve cihaz kayıt türü için Iş profili ve cihaz sahibi profili seçilirse, bir sertifika profilini uygulama yapılandırma ilkesiyle ilişkilendiremezsiniz.
2. Yeni bir profil oluşturulup Iş profili yalnızca seçili ise, cihaz yapılandırması altında oluşturulan Iş profili sertifika ilkeleri kullanılabilir.
3. Yeni bir profil oluşturulduysa ve yalnızca cihaz sahibi seçilirse, cihaz yapılandırması altında oluşturulan cihaz sahibi sertifika ilkeleri kullanılabilir. 

> [!IMPORTANT]
> Bu özelliğin yayınlanmasından önce oluşturulan mevcut ilkeler (2020 Nisan sürümü-2004) ilke kayıt türü için varsayılan olarak Iş profili ve cihaz sahibi profili olur. Ayrıca, bu özellik ile ilişkili sertifika profillerinin bulunduğu bu özelliğin yayınlanmasından önce oluşturulan mevcut ilkeler, varsayılan olarak yalnızca Iş profili ' dir.

Ayrıca, her iki e-posta yapılandırma türünde Sertifika profillerinin kullanılması da dahil olmak üzere hem Iş profili hem de cihaz sahibi kayıt türleri için çalışacak Gmail ve dokuz e-posta yapılandırma profilleri ekliyoruz.  Iş profillerinin cihaz yapılandırması altında oluşturduğunuz Gmail veya dokuz ilke cihaza uygulanmaya devam eder ve bunları uygulama yapılandırma ilkelerine taşımak gerekli değildir.

[Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar**  >  **uygulama yapılandırma ilkeleri**' ni seçerek uygulama yapılandırma ilkelerini bulabilirsiniz. Uygulama yapılandırma ilkeleri hakkında daha fazla bilgi için bkz. [Microsoft Intune Için uygulama yapılandırma ilkeleri](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Cihaz sahiplik türü değiştirildiğinde anında iletme bildirimi<!-- 5575875 -->
Hem Android hem de iOS Şirket Portalı kullanıcılarınıza, cihaz sahipliği türü kişisel olarak bir gizlilik özelliği olarak değiştirildiğinde, bu kullanıcılara göndermek üzere bir anında iletme bildirimi yapılandırabilirsiniz. Bu anında iletme bildirimi varsayılan olarak off olarak ayarlanmıştır. Bu ayar, **Kiracı Yönetimi**özelleştirmesi seçilerek Microsoft Uç Nokta Yöneticisi ' nde bulunabilir  >  **Customization**. Cihaz sahipliğinin son kullanıcılarınızı nasıl etkilediği hakkında daha fazla bilgi edinmek için bkz. [cihaz sahipliğini değiştirme](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Özelleştirme bölmesi için Grup hedefleme desteği<!-- 4722837  -->
**Özelleştirme** bölmesindeki ayarları Kullanıcı grupları ' na hedefleyebilirsiniz. Bu ayarları Intune 'da bulmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' ne gidin, **Kiracı Yönetimi**  >  **özelleştirmesi**' nı seçin. Özelleştirme hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>İOS, ıpados ve macOS 'ta desteklenen isteğe bağlı VPN kuralları birden çok "her bağlantı denemesini değerlendir"<!-- 6424615  -->
Intune kullanıcı deneyimi, **her bağlantı denemesini değerlendir** eylemiyle aynı VPN profilinde birden çok isteğe bağlı VPN kuralına izin verir (**cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  isteğe bağlı **Otomatik VPN**> profil için iOS > için **VPN** oluşturma**iOS/ıpados** veya **MacOS**  >  **On-demand**).

Yalnızca listedeki ilk kurala göre kabul edilir. Bu davranış sabittir ve Intune listedeki tüm kuralları değerlendirir. Her kural, isteğe bağlı kurallar listesinde göründüğü sırada değerlendirilir.

> [!NOTE]
> Bu isteğe bağlı VPN kurallarını kullanan mevcut VPN profilleriniz varsa, bu değişiklik VPN profilini bir sonraki değiştirişinizde geçerli olur. Örneğin, adı bağlantıyı değiştir gibi küçük bir değişiklik yapın ve ardından profili kaydedin.
>
> Kimlik doğrulaması için SCEP sertifikaları kullanıyorsanız bu değişiklik, bu VPN profiline yönelik sertifikaların yeniden verilmesine neden olur.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS
- Mac OS

VPN profilleri hakkında daha fazla bilgi için bkz. [VPN profilleri oluşturma](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>İOS/ıpados cihazlarında SSO ve SSO uygulama uzantısı profillerindeki ek seçenekler<!-- 6504155   -->

İOS/ıpados cihazlarında şunları yapabilirsiniz:
- SSO profillerinde (**cihazlar**  >  **yapılandırma profilleri**  >  **profil oluşturma**  >  **iOS/ıpados** for platform > **cihaz özellikleri** > **Çoklu oturum açma**) için, Kerberos asıl adını SSO profillerindeki güvenlik hesabı Yöneticisi (Sam) hesap adı olacak şekilde ayarlayın. 
- SSO uygulama uzantısı profillerinde (**cihazlar**  >  **yapılandırma profilleri**  >  **profil oluşturma**  >  **iOS/ıpados** for platform > **cihaz > özellikleri** **Çoklu oturum açma uygulama uzantısı**) için iOS/ıpados Microsoft Azure ad uzantısını, yeni bir SSO uygulama uzantısı türü kullanarak daha az tıklamayla yapılandırın. Paylaşılan cihaz modundaki cihazlar için Azure AD uzantısını etkinleştirebilir ve uzantıya özgü verileri uzantıya gönderebilirsiniz.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 13.0 +

İOS/ıpados cihazlarında çoklu oturum açma kullanma hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısına genel bakış](../configuration/device-features-configure.md#single-sign-on-app-extension) ve [Çoklu oturum açma ayarları listesi](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Varsayılan profil mevcut olduğunda Apple otomatik cihaz kayıt belirtecini Sil<!--6393220 -->
Daha önce, bir varsayılan profili silemdiniz, bu, bununla ilişkili otomatik cihaz kayıt belirtecini silememeyi amaçlıyordu. Şimdi, şu durumlarda belirteci silebilirsiniz:
- belirtece hiçbir cihaz atanmadı
- Varsayılan bir profil vardır, varsayılan profili silin ve ardından ilişkili belirteci silin.
Daha fazla bilgi için bkz. [Intune 'dan BIR Ade belirtecini silme](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Apple otomatik cihaz kaydı ve Apple Configurator 2 cihazları, profilleri ve belirteçleri için ölçekli destek<!--3542402 -->
Intune, BT departmanlarına ve kuruluşlara yardımcı olmak için, belirteç başına 1000 adede kadar kayıt profilini, her Intune hesabı için 2000 otomatik cihaz kaydı (eski adıyla DEP) belirteçlerini ve belirteç başına 75.000 cihazlarını desteklemektedir. Kayıt profili başına cihazlar için, belirteç başına en fazla cihaz sayısı altında belirli bir sınır yoktur.

Intune artık 1000 adede kadar Apple Configurator 2 profilini desteklemektedir.

Daha fazla bilgi için bkz. [desteklenen birim](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Tüm cihazlar sayfa sütun girdisi değişiklikleri<!--6967616 -->
**Tüm cihazlar** sayfasında, **yönetilen** sütunun girdileri değiştirilmiştir:
- *Intune* artık *MDM* yerine gösteriliyor
- *Ortak yönetilen* artık *MDM/ConfigMgr Aracısı* yerine görüntülendi

Dışarı aktarma değerleri değiştirilmez.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Güvenilen Platform Yöneticisi (TPM) sürüm bilgileri artık cihaz donanımı sayfasında<!--6224914 idmiss -->
Artık bir cihazın donanım sayfasında TPM sürüm numarasını görebilirsiniz ([Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazları** > bir cihaz > bir cihaz seçin > **sistem kasası**altına bakın). **Hardware**

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>MacOS cihazlarına atanan betiklerin daha iyi giderilmesine yönelik Günlükler toplayın<!-- 6359853  -->
Artık macOS cihazlarına atanan betiklerin daha iyi sorun giderme için günlük toplayabilirsiniz. En çok 60 MB (sıkıştırılmış) veya 25 dosya olan günlükleri toplayabilirsiniz (hangisi önce gerçekleşirse). Daha fazla bilgi için bkz. [günlük toplama kullanarak macOS kabuğu betik Ilkelerine sorun giderme](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Güvenlik

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Android kurumsal tam olarak yönetilen cihazları sertifikalarla sağlamak için türetilmiş kimlik bilgileri<!--4839592    -->
Intune artık, bir Android cihazları için kimlik doğrulama yöntemi olarak [türetilmiş kimlik bilgilerinin](../protect/derived-credentials.md) kullanımını desteklemektedir. Türetilmiş kimlik bilgileri, cihazlara sertifika dağıtmaya yönelik ulusal standartlar ve Teknoloji Enstitüsü (NıST) 800-157 standardının bir uygulamasıdır. Android desteğiniz iOS/ıpados çalıştıran cihazlara yönelik desteğimize genişletilir.

Türetilmiş kimlik bilgileri, akıllı kart gibi kişisel kimlik doğrulama (PıV) veya ortak erişim kartı (CAC) kartının kullanımına dayanır. Mobil cihazlarının türetilmiş bir kimlik bilgilerini almak için, kullanıcılar Microsoft Intune uygulamasında başlar ve kullandığınız sağlayıcıya özgü bir kayıt iş akışını takip edin. Tüm sağlayıcılar için ortak, türetilmiş kimlik bilgisi sağlayıcısında kimlik doğrulaması yapmak için bir bilgisayarda akıllı kart kullanma gereksinimidir. Bu sağlayıcı daha sonra kullanıcının akıllı kartından derlenen cihaza bir sertifika yayınlar.

VPN ve WiFi için cihaz yapılandırma profillerinin kimlik doğrulama yöntemi olarak türetilmiş kimlik bilgilerini kullanabilirsiniz. Bunları destekleyen uygulamalar için uygulama kimlik doğrulaması ve S/MIME imzalama ve şifreleme için de kullanabilirsiniz.

Intune artık Android ile aşağıdaki türetilmiş kimlik bilgisi sağlayıcılarını desteklemektedir:
- Entrust Datacard
- Intercede

Daha sonraki sürümlerde Android için bir üçüncü sağlayıcı (DıŞA purebred) kullanıma sunulacaktır.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Microsoft Edge güvenlik temeli artık genel kullanıma sunuldu<!--6586139 -->

Yeni bir [Microsoft Edge güvenlik temeli](../protect/security-baselines.md#available-security-baselines) sürümü kullanıma sunuldu ve genel kullanıma açık (GA) olarak yayımlandı. Önceki kenar taban çizgisi önizlemededir.  Yeni temel sürüm 2020 Nisan (Edge sürüm 80 ve üzeri). 

Bu yeni temelin yayınlanmasıyla birlikte, önceki temel sürümlere göre profil oluşturamayacak, ancak bu sürümlerle oluşturduğunuz profilleri kullanmaya devam edebilirsiniz. Ayrıca [, mevcut profillerinizi en son temel sürümü kullanacak şekilde güncelleştirmeyi](../protect/security-baselines.md#change-the-baseline-version-for-a-profile)de tercih edebilirsiniz. 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>6 Nisan 2020 haftası

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>MacOS cihazları için yeni kabuk betik ayarları<!-- 6884363 -->
MacOS cihazları için kabuk betikleri yapılandırılırken, artık aşağıdaki yeni ayarları yapılandırabilirsiniz: 
- Cihazlarda betik bildirimlerini gizle
- Betik sıklığı
- Betik başarısız olursa en fazla yeniden deneme sayısı

Daha fazla bilgi için bkz. [Intune 'Da macOS cihazlarında Shell betikleri kullanma](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>30 Mart 2020 haftası

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Microsoft Endpoint Manager Yönetim Merkezi için yeni URL<!-- 3704810 -->
Son yılda Microsoft Endpoint Manager duyurusunu ile hizalamak için Microsoft Endpoint Manager yönetim merkezinin (eski Microsoft 365 adıyla cihaz yönetimi) URL 'sini olarak değiştirdik [https://endpoint.microsoft.com](https://endpoint.microsoft.com) . Eski Yönetim Merkezi URL 'SI ( [https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com) ) çalışmaya devam eder, ancak yeni URL 'yi kullanarak Microsoft Endpoint Manager yönetim merkezine erişmeye başlamanız önerilir.

Daha fazla bilgi için bkz. [Microsoft Endpoint Manager yönetim merkezini kullanarak BT görevlerini basitleştirme](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>İOS için Şirket Portalı yatay modunu destekler<!--6048329  -->   
Kullanıcılar artık cihazlarını kaydedebilir, uygulama bulabilir ve tercih ettikleri ekran yönünü kullanarak BT desteği alabilir. Kullanıcılar ekranı dikey modda kilitlemedikleri takdirde uygulama ekranları dikey veya yatay moda uyacak şekilde otomatik olarak algılar ve ayarlar.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>MacOS cihazları için betik desteği (Genel Önizleme)<!-- 4280361  -->
MacOS cihazlarına komut dosyaları ekleyebilir ve dağıtım yapabilirsiniz. Bu destek, MacOS cihazlarındaki yerel MDM yeteneklerini kullanarak, macOS cihazlarını mümkün olduğunca fazla yapılandırma yeteneğinizi genişletmektedir. Daha fazla bilgi için bkz. [Intune 'Da macOS cihazlarında Shell betikleri kullanma](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>24 Mart 2020 haftası

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Android ve Android kurumsal cihazlarda cihaz kısıtlama profilleri oluştururken Geliştirilmiş kullanıcı arabirimi deneyimi<!-- 5841361 -->
Android veya Android Kurumsal cihazları için bir profil oluşturduğunuzda, uç nokta yönetimi Yönetim Merkezi 'ndeki deneyim güncellenir. Bu değişiklik, aşağıdaki**cihaz yapılandırma profillerini etkiler (cihaz**  >  **yapılandırma profilleri**  >  **profil oluşturma**  >  **Android Cihaz Yöneticisi** veya platform için **Android Enterprise** ):

- Cihaz kısıtlamaları: Android Cihaz Yöneticisi
- Cihaz kısıtlamaları: Android kurumsal cihaz sahibi
- Cihaz kısıtlamaları: Android kurumsal iş profili

Yapılandırabileceğiniz cihaz kısıtlamaları hakkında daha fazla bilgi için bkz. [Android Cihaz Yöneticisi](../configuration/device-restrictions-android.md) ve [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>İOS/ıpados ve macOS cihazlarında yapılandırma profilleri oluştururken Geliştirilmiş kullanıcı arabirimi deneyimi<!-- 5569002 5568997 -->
İOS veya macOS cihazları için bir profil oluşturduğunuzda, uç nokta yönetimi Yönetim Merkezi 'ndeki deneyim güncellenir. Bu değişiklik, aşağıdaki**cihaz yapılandırma profillerini etkiler (cihaz**  >  **yapılandırma profilleri**  >  **Create profile**  >  **iOS/ıpados** veya platform için **MacOS** ):

- Özel: iOS/ıpados, macOS
- Cihaz özellikleri: iOS/ıpados, macOS
- Cihaz kısıtlamaları: iOS/ıpados, macOS
- Endpoint Protection: macOS
- Uzantılar: macOS
- Tercih dosyası: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>MacOS cihazlarındaki cihaz özelliklerinde Kullanıcı yapılandırma ayarından gizle<!-- 6524869 -->

MacOS cihazlarında bir cihaz özellikleri yapılandırma profili oluşturduğunuzda, yeni bir **Kullanıcı yapılandırma** ayarı (**cihazlar**  >  **yapılandırma profilleri**,  >  **Create profile**  >  profil > **oturum açma öğeleri**için cihaz için**MacOS** > **cihaz özelliklerini** oluşturur) vardır.

Bu özellik, macOS cihazlarında **kullanıcı & grupları** oturum açma öğeleri uygulama listesinde bir uygulamanın gizleme onay işaretini ayarlar. Mevcut profiller listede bu ayarı yapılandırılmamış olarak gösterir. Yöneticiler, bu ayarı yapılandırmak için mevcut profilleri güncelleştirebilir.

**Gizle**olarak ayarlandığında, uygulama için gizleme onay kutusu işaretlenir ve kullanıcılar bunu değiştiremezler. Kullanıcılar cihazlarında oturum açtıktan sonra da uygulamayı kullanıcılardan gizler.

> [!div class="mx-imgBorder"]
> ![Kullanıcılar Microsoft Intune ve uç nokta yöneticisinde cihazda oturum açtıktan sonra macOS cihazlarındaki uygulamaları gizleyin](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Yapılandırabileceğiniz ayar hakkında daha fazla bilgi için bkz. [MacOS cihaz özelliği ayarları](../configuration/macos-device-features-settings.md).

Bu özellik şu platformlarda geçerlidir:

- Mac OS

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>16 Mart 2020 haftası (2003 hizmet sürümü)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS ve iOS Şirket Portalı güncelleştirmeleri<!-- 5779439, 5780234  -->
MacOS ve iOS Şirket Portalı profil bölmesi, oturum kapatma düğmesini içerecek şekilde güncelleştirilmiştir. Ayrıca, macOS Şirket Portalı profil bölmesinde UI geliştirmeleri yapılmıştır. Şirket Portalı hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Web kliplerini iOS cihazlarında Microsoft Edge 'e yeniden hedefle<!-- 5455276   -->
Korunan bir tarayıcıda açılması gereken iOS cihazlarında yeni dağıtılan web klipleri (sabitlenmiş Web uygulamaları) Intune Managed Browser yerine Microsoft Edge 'de açılır. Managed Browser yerine Microsoft Edge 'de açıldıklarından emin olmak için önceden mevcut web kliplerini yeniden hedeflemeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Edge kullanarak Web erişimini yönetme Microsoft Intune](../apps/manage-microsoft-edge.md) ve [Microsoft Intune Web uygulamaları ekleme](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Android için Microsoft Edge ile Intune Tanılama aracını kullanma<!-- 4735244  -->
Android için Microsoft Edge artık Intune Tanılama aracı ile tümleşiktir. İOS için Microsoft Edge deneyiminden benzer şekilde, cihazdaki Microsoft Edge 'in URL çubuğuna "about: ıntunehelp" girilmesi, Intune Tanılama aracını başlatacak. Bu araç ayrıntılı Günlükler sağlar. Kullanıcılar bu günlükleri kendi BT departmanlarına toplayıp göndermek veya belirli uygulamalar için MAM günlüklerini görüntülemek için Kılavuzlu olabilir.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Intune marka ve özelleştirme güncelleştirmeleri<!-- 5236032  -->
"Marka ve özelleştirme" adlı Intune bölmesini, geliştirmeler de dahil olmak üzere güncelleştirdik:

- Bölmeyi **özelleştirmek**için yeniden adlandırma.
- Kuruluş ve ayarların tasarımını geliştirme.
- Ayarlar metin ve araç ipuçlarını geliştirme.

Bu ayarları Intune 'da bulmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' ne gidin, **Kiracı Yönetimi**  >  **özelleştirmesi**' nı seçin. Varolan özelleştirme hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Kullanıcının kişisel şifreli kurtarma anahtarı<!-- 6273943  -->
Kullanıcıların, Android Şirket Portalı uygulaması veya Android Intune uygulaması aracılığıyla Mac cihazları için kişisel şifreli **Filekasasını** kurtarma anahtarını almasına olanak sağlayan yeni bir Intune özelliği vardır. Hem Şirket Portalı uygulaması hem de Intune uygulamasında, kullanıcının Mac cihazlarına erişmek için gereken **Filekasasını** kurtarma anahtarını görebildiği Web şirket portalı bir Chrome tarayıcısı açacak bir bağlantı vardır. Şifreleme hakkında daha fazla bilgi için bkz. [Intune ile cihaz şifrelemesini kullanma](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>İyileştirilmiş ayrılmış cihaz kaydı <!-- 6114580  -->
Android kurumsal adanmış cihazları için kaydı iyileştirmekte ve Wi-Fi ile ilişkili SCEP sertifikalarının, 22 Kasım 2019 ' den önce kaydedilen adanmış cihazlara uygulanması daha kolay hale getiriyoruz. Yeni kayıtlar söz konusu olduğunda, Intune uygulaması yüklenmeye devam eder, ancak son kullanıcıların kayıt sırasında **Intune Aracısını Etkinleştir** adımını gerçekleştirmesi artık gerekmez. Taksit arka planda otomatik olarak gerçekleşir ve Wi-Fi ile ilişkili SCEP sertifikaları, son kullanıcı etkileşimi olmadan dağıtılabilir ve ayarlanabilir.  

Bu değişiklikler, Intune hizmet arka ucu dağıttığı için Mart ayının her gününde aşamalı olarak kullanıma sunulacaktır. Tüm kiracıların bu yeni davranışı Mart sonuna kadar olacak. İlgili bilgiler için bkz. [Android kurumsal adanmış CIHAZLARDA SCEP sertifikaları Için destek](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Windows cihazlarında Yönetim Şablonları oluştururken yeni kullanıcı deneyimi<!--5096036 -->
Müşteri geri bildirimlerine göre ve yeni Azure tam ekran deneyimine geçtiğimiz için, Yönetim Şablonları profili deneyimini bir klasör görünümüyle yeniden oluşturduk. Herhangi bir ayarlarda veya mevcut profillerde değişiklik yapmadık. Bu nedenle, mevcut profilleriniz aynı kalır ve yeni görünümde kullanılabilir. **Tüm ayarlar ' ı**seçip ara ' yı kullanarak tüm ayarlar seçeneklerinde gezinmeye devam edebilirsiniz. Ağaç görünümü bilgisayar ve Kullanıcı yapılandırmalarına göre bölünür. Windows, Office ve Edge ayarlarını ilişkili klasörlerinde bulacaksınız.  

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>IKEv2 VPN bağlantılarına sahip VPN profilleri, her zaman iOS/ıpados cihazlarıyla birlikte kullanılabilir<!-- 1947932   -->
İOS/ıpados cihazlarında, Ikev2 bağlantısı kullanan bir VPN profili oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**profil  >  **Oluştur**  >  **iOS/ıpados** for platform > bağlantı türü için **VPN** ). Şimdi, Ikev2 ile her zaman açık yapılandırma yapabilirsiniz. Yapılandırıldığında, IKEv2 VPN profilleri otomatik olarak bağlanır ve VPN 'ye bağlı (veya hızlı bir şekilde yeniden bağlantı) kalır. Ağlar arasında hareket etmekle veya cihazları yeniden başlatırken bile bağlı kalır.

İOS/ıpados 'da, her zaman VPN Ikev2 profilleriyle sınırlıdır.

Yapılandırabileceğiniz Ikev2 ayarlarını görmek için [Microsoft Intune iOS CIHAZLARıNDA VPN ayarları ekle](../configuration/vpn-settings-ios.md#ikev2-settings)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Android kurumsal cihazlarda OEMConfig cihaz yapılandırma profillerindeki paketleri ve paket dizilerini silme<!-- 5550355   -->
Android kurumsal cihazlarda, oemconfig profilleri oluşturur ve güncelleştirir (**cihaz**  >  **yapılandırma profilleri**  >  **Create profile**  >  platform için**Android Enterprise** > profil türü için **oemconfig** ). Kullanıcılar artık Intune 'daki **yapılandırma tasarımcısını** kullanarak demeti ve paket dizilerini silebilir.

OEMConfig profilleri hakkında daha fazla bilgi için bkz. [Microsoft Intune 'de oemconfig Ile Android Kurumsal cihazları kullanma ve yönetme](../configuration/android-oem-configuration-overview.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android Kurumsal

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>İOS/ıpados Microsoft Azure AD SSO uygulama uzantısını yapılandırma<!-- 5672534   -->
Microsoft Azure AD ekibi, iOS/ıpados 13.0 + kullanıcılarına tek bir oturum açma ile Microsoft uygulamalarına ve Web sitelerine erişim elde etmesine izin vermek için bir yeniden yönlendirme çoklu oturum açma (SSO) uygulama uzantısı oluşturdu. Daha önce Microsoft Authenticator uygulama ile aracılı kimlik doğrulaması yapmış olan tüm uygulamalar, yeni SSO uzantısıyla SSO almaya devam edecektir. Azure AD SSO uygulama uzantısı sürümü ile, SSO uzantısını yeniden yönlendirme SSO uygulama uzantısı türüyle**yapılandırabilirsiniz (cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **iOS/ıpados** > cihaz için Platform **cihaz özellikleri** > **Çoklu oturum açma uygulama uzantısı**).

Aşağıdakiler cihazlar için geçerlidir:
- iOS 13,0 ve üzeri
- ıpados 13,0 ve üzeri

İOS SSO uygulama uzantıları hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısı](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Kurumsal uygulama güven ayarları değiştirme ayarı iOS/ıpados cihaz kısıtlama profillerden kaldırılır<!-- 6225131   -->
İOS/ıpados cihazlarında, bir cihaz kısıtlamaları profili**oluşturursunuz (cihaz**  >  **yapılandırma profilleri**profil  >  **Oluştur**  >  **iOS/ıpados** for platform > profil türü için **cihaz kısıtlamaları** ). **Kurumsal uygulama güven ayarları değiştirme** ayarı Apple tarafından kaldırılır ve Intune 'dan kaldırılır. Şu anda bu ayarı bir profilde kullanıyorsanız, hiçbir etkisi yoktur ve mevcut profillerden kaldırılır. Bu ayar ayrıca Intune 'daki herhangi bir raporlamadan kaldırılır.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

Kısıtlayacakları ayarları görmek için [iOS ve ıpados cihaz ayarları ' na giderek özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Sorun giderme: bekleyen MAM ilkesi bildirimi bilgilendirici simgesine değiştirildi<!--6348954 -->
Sorun giderme dikey penceresinde bekleyen bir MAM ilkesi için bildirim simgesi bir bilgilendirme simgesine değiştirilmiştir.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Uyumluluk ilkesini yapılandırırken kullanıcı arabirimi güncelleştirmesi<!-- 3961639    -->

Microsoft Endpoint Manager 'da [uyumluluk ilkeleri oluşturmak](../protect/create-compliance-policy.md#create-the-policy) için Kullanıcı arabirimini güncelleştirdik (**cihaz**  >  **uyumluluk ilkeleri**  >  **ilkeleri**  >  **ilke oluştur**). Daha önce kullandığınız ayarların ve ayrıntıların aynısını içeren yeni bir kullanıcı deneyimi sunuyoruz. Yeni deneyim, Uyumluluk ilkesini oluşturmak için sihirbaza benzer bir süreç izler ve ilke için *atamalar* ekleyebileceğiniz bir sayfa ve ilkeyi oluşturmadan önce yapılandırmanızı gözden geçirebileceğiniz bir *İnceleme + oluştur* sayfası içerir.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Uyumsuz cihazları devre dışı bırak<!-- 1827291       -->
Uyumsuz cihazlara ekleyebileceğiniz uyumlu olmayan cihazlar için,  [uyumsuz cihazı devre dışı](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)bırakmak üzere yeni bir eylem ekledik.  Yeni eylem, **uyumsuz cihazı devre dışı bırakma**, cihazdaki tüm şirket verilerinin kaldırılmasına neden olur ve ayrıca cihazın Intune tarafından yönetilmesini kaldırır.  Bu eylem, gün cinsinden yapılandırılan değere ulaşıldığında ve bu noktada cihaz kullanımdan kalkmaya uygun hale geldiğinde çalışır. Minimum değer 30 gündür.  Yöneticilerin uygun olan tüm cihazları devre dışı bırakabileceği *uyumlu olmayan cihazları devre* dışı bırak bölümü kullanılarak cihazları devre dışı bırakmak IÇIN açık BT yöneticisi onayı gerekecektir.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>İOS Enterprise Wi-Fi profillerinde WPA ve WPA2 desteği<!--6215273   -->
[İOS Için Enterprise Wi-Fi profilleri](../configuration/wi-fi-settings-ios.md#enterprise-profiles) artık *güvenlik türü* alanını destekliyor. *Güvenlik türü*Için, **WPA Enterprise** veya **WPA/WPA2 kurumsal**seçeneklerinden birini seçebilir ve ardından *EAP türü*için bir seçim belirtebilirsiniz.  (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluşturun** ve *Platform* Için **iOS/ıpados** ' ı seçin ve ardından *profil*için **Wi-Fi** ' i seçin. 

Yeni kurumsal seçenekler, iOS için temel bir Wi-Fi profili için kullanılabilir olanlar gibidir.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Sertifika, e-posta, VPN ve Wi-Fi, VPN profilleri için yeni kullanıcı deneyimi<!-- 5615208   -->
[user experience](../configuration/device-profile-create.md) **Devices**  >  **Configuration profiles**  >  Aşağıdaki profil türlerini oluşturmak ve değiştirmek için uç nokta yönetimi Yönetim merkezinde (cihaz yapılandırma profilleri**profil oluşturma**) Kullanıcı deneyimini güncelleştirdik. Yeni deneyim, daha önce olduğu gibi aynı ayarları sunar, ancak çok yatay kaydırma gerektirmeyen sihirbaza benzer bir deneyim kullanır. Mevcut konfigürasyonları yeni deneyimle değiştirmeniz gerekmez.

- Türetilmiş kimlik bilgileri
- E-posta
- PKCS sertifikası
- PKCS içeri aktarılmış sertifikası
- SCEP sertifikası
- Güvenilir sertifika
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Şirket Portalı, Android ve iOS için kayıt için kullanılabilir olup olmadığını yapılandırın<!-- 4260128  -->
Android ve iOS cihazlarındaki Şirket Portalı cihaz kaydının, istemler olmadan veya kullanıcılar tarafından kullanılamayan istemlerle kullanılabilir olup olmadığını yapılandırabilirsiniz. Bu ayarları Intune 'da bulmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' ne gidin ve **Kiracı Yönetimi**  >  **özelleştirmesi**  >  **Edit**  >  **cihaz kaydını**Düzenle ' yi seçin.  

Cihaz kayıt ayarı için destek, son kullanıcıların bu Şirket Portalı sürümlerine sahip olmasını gerektirir:
-    İOS üzerinde Şirket Portalı: sürüm 4,4 veya üzeri
-    Android üzerinde Şirket Portalı: sürüm 5.0.4715.0 veya üzeri

Varolan Şirket Portalı özelleştirmesi hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Android cihazlarına yeni Android raporuna genel bakış sayfası<!-- 5435435   -->
Her bir cihaz yönetimi çözümüne kaç tane Android cihaz kaydedildiğini gösteren Android cihazlara Genel Bakış sayfasında Microsoft Endpoint Manager yönetim konsoluna bir rapor ekledik. Bu grafik (Azure konsolunda aynı grafik gibi), iş profilini, tam olarak yönetilen, adanmış ve Cihaz Yöneticisi kayıtlı cihaz sayısını gösterir. Raporu görmek için **cihazlar**  >  **Android**  >  **genel bakış**' ı seçin.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Android Cihaz Yöneticisi yönetiminden iş profili yönetimine kadar Kullanıcı Kılavuzu<!--5857738   -->
Android Cihaz Yöneticisi platformu için yeni bir uyumluluk ayarı yayınlıyoruz. Bu ayar cihaz yöneticisiyle yönetiliyorsa bir cihazı uyumsuz hale getirme olanağı sağlar.

Uyumlu olmayan bu cihazlarda, **cihaz ayarlarını Güncelleştir** sayfasında kullanıcılar **yeni cihaz yönetimi kurulum** iletisi ' ne git ' i görür. **Çözümle** düğmesine dokunduklarında, bunlara göre kılavuzluk edilecek:

1. Cihaz Yöneticisi yönetiminden kaydı geri al
2. İş profili yönetimine kaydolma
3. Uyumluluk sorunlarını çözme 
 
Google, Android Enterprise ile modern, daha zengin ve daha güvenli cihaz yönetimine geçme çabasında yeni Android sürümlerindeki Cihaz Yöneticisi desteğini düşürdüğünde.  Intune, yalnızca S2 CY2020 aracılığıyla Android 10 ve üzeri çalıştıran cihaz yönetici tarafından yönetilen Android cihazları için tam destek sağlayabilir. Android 10 veya sonraki sürümleri çalıştıran Cihaz Yöneticisi tarafından yönetilen cihazlar (Samsung hariç), tamamen yönetilemez. Özellikle, etkilenen cihazlar yeni parola gereksinimleri almaz.

Bu ayar hakkında daha fazla bilgi için bkz. [Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşıma](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Veri ambarı artık MAC adresini sağlıyor<!-- 6123680  -->
Intune veri ambarı, `EthernetMacAddress` `device` yöneticilerin Kullanıcı ve ana bilgisayar MAC adresi arasında ilişkilendirip ilişkilendirilmesi için varlık içinde yeni bir Özellik () olarak sağlar. Bu özellik belirli kullanıcılara ulaşmaya ve ağda gerçekleşen olay sorunlarını gidermenize yardımcı olur. Yöneticiler daha zengin raporlar oluşturmak için bu özelliği [Power BI raporlarında](../developer/reports-proc-get-a-link-powerbi.md) da kullanabilir. Daha fazla bilgi için bkz. Intune veri ambarı [cihaz](../developer/intune-data-warehouse-collections.md#devices) varlığı.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Ek veri ambarı cihaz envanteri özellikleri<!-- 6125732  -->
Intune veri ambarı kullanılarak ek cihaz envanteri özellikleri kullanılabilir. Aşağıdaki özellikler artık [cihazlar](../developer/reports-ref-devices.md#devices) Beta koleksiyonu aracılığıyla kullanıma sunulmuştur:
- `ethernetMacAddress` -Bu cihazın benzersiz ağ tanımlayıcısı.
- `model` -Cihaz modeli.
- `office365Version` -Cihaza yüklü Office 365 sürümü.
- `windowsOsEdition` -Işletim sistemi sürümü.

Aşağıdaki özellikler artık [Devicepropertyhistory](../developer/reports-ref-devices.md#devicepropertyhistories) Beta koleksiyonu aracılığıyla kullanıma sunulmuştur:
- `physicalMemoryInBytes` -Bayt cinsinden fiziksel bellek.
- `totalStorageSpaceInBytes` -Bayt cinsinden toplam depolama kapasitesi.

Daha fazla bilgi için bkz. [Microsoft Intune veri ambarı API 'si](../developer/reports-nav-intune-data-warehouse.md).

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Ek hizmetleri desteklemek için yardım ve destek iş akışı güncelleştirmesi<!-- 5654170   -->
Microsoft Endpoint Manager Yönetim Merkezi 'ndeki yardım ve destek sayfasını, artık [kullandığınız yönetim türünü seçtiğiniz](../fundamentals/get-support.md#options-to-access-help-and-support)şekilde güncelleştirdik. Bu değişiklik ile aşağıdaki yönetim türlerinden seçim yapabilirsiniz:

- Configuration Manager (Masaüstü analizlerini içerir)
- Intune
- Ortak yönetim

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Güvenlik

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Endpoint Security 'nin bir parçası olarak güvenlik yöneticisi odaklı ilkelerinin önizlemesini kullanın<!--6131401  -->
Genel önizleme olarak, Microsoft uç nokta yönetimi Yönetim Merkezi 'nde uç nokta güvenlik düğümü altına birçok yeni ilke grubu ekledik. Güvenlik Yöneticisi olarak, bu yeni ilkeleri cihaz güvenliğinin belirli yönlerine odaklanmak için, daha büyük cihaz yapılandırma ilkesi gövdesinin ek yükü olmadan farklı ilgili ayarları yönetmek üzere kullanabilirsiniz.

*Microsoft Defender virüsten koruma için yeni virüsten koruma ilkesi* dışında (aşağıda bkz.), bu yeni önizleme ilkelerinin ve profillerinin her bir sürümündeki ayarlar şu anda [cihaz yapılandırma profilleri](../configuration/device-profile-create.md) aracılığıyla yapılandırdığınız ayarların aynısıdır.

Aşağıda, önizleme aşamasında olan yeni ilke türleri ve bunların kullanılabilir profil türleri verilmiştir:

- **Virüsten koruma (Önizleme)**:
  - MacOS
    - **Virüsten koruma** - [Mac IÇIN Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)'Yi yönetmek üzere MacOS için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-macos.md) yönetin.

  - Windows 10 ve üzeri:
    - **Microsoft Defender virüsten koruma** -bulut koruması, virüsten koruma dışlamaları, düzeltme, tarama seçenekleri ve daha fazlası Için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-windows.md) yönetin.

      *Microsoft Defender virüsten koruma* Için virüsten koruma profili, cihaz kısıtlama profilinin bir parçası olarak bulunan ayarların yeni bir örneğini tanıtan bir özel durumdur. Bu yeni virüsten koruma ayarları:

        - , Cihaz kısıtlamalarında bulunan ayarlardır, ancak cihaz kısıtlaması olarak yapılandırıldığında kullanılamayan yapılandırma için üçüncü bir seçeneği destekler.
        - Endpoint Protection için [ortak yönetim iş yükü kaydırıcısının](/configmgr/comanage/how-to-switch-workloads) Intune olarak ayarlandığı durumlarda Configuration Manager ile birlikte yönetilen cihazlara uygulanır.

     Yeni *Virüsten koruma*  >  *Microsoft Defender virüsten koruma* profilini bir cihaz kısıtlama profili aracılığıyla yapılandırma yerine kullanmayı planlayın.

  - **Windows Güvenlik deneyimi** -son kullanıcıların Microsoft Defender Güvenlik Merkezi 'nde görüntüleyebilecekleri Windows güvenlik ayarlarını ve aldıkları bildirimleri yönetin. Bu ayarlar, cihaz yapılandırma Endpoint Protection profili olarak kullanılabilenlerden değiştirilmez.

- **Disk şifrelemesi (Önizleme)**:
  - MacOS
    - **FileVault**
  - Windows 10 ve üzeri:
    - **BitLocker**
- **Güvenlik Duvarı (Önizleme)**:
  - MacOS
    - **macOS güvenlik duvarı**
  - Windows 10 ve üzeri:
    - **Microsoft Defender güvenlik duvarı**
- **Uç nokta algılama ve yanıt (Önizleme)**:
  - Windows 10 ve üzeri: - **Windows 10 Intune**
- **Saldırı yüzeyi azaltma (Önizleme)**:
  - Windows 10 ve üzeri:
    - **Uygulama ve tarayıcı yalıtımı**
    - **Web koruması**
    - **Uygulama denetimi**
    - **Saldırı yüzeyi azaltma kuralları**
    - **Cihaz denetimi**
    - **Exploit protection**
- **Hesap koruması (Önizleme)**:
  - Windows 10 ve üzeri:
    - **Hesap koruması**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>9 Mart 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Win32 uygulama içeriğini indirirken teslim Iyileştirme aracısını yapılandırma<!-- 5410945 -->

Teslim Iyileştirme aracısını, atamaya göre arka planda veya ön plan modunda Win32 uygulama içeriğini indirmek için yapılandırabilirsiniz. Mevcut Win32 uygulamaları için içerik arka plan modunda indirilmeye devam edecektir. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **uygulamalar**  >  **tüm uygulamalar**' ı seçin  >  *Win32 uygulama*  >  **özellikleri**' ni seçin. **Atamalar**' ın yanındaki **Düzenle** ' yi seçin.  **Gerekli** bölümde **mod** altında **Ekle** seçeneğini belirleyerek atamayı düzenleyin.  Yeni ayarı, **uygulama ayarları** bölümünde bulabilirsiniz. Teslim Iyileştirme hakkında daha fazla bilgi için bkz. [Win32 uygulama yönetimi-teslim iyileştirmesi](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Windows cihazları için birincil kullanıcıyı değiştirme<!-- 3794742   -->
Birincil kullanıcıyı Windows hibrit ve Azure AD 'ye katılmış cihazlar için değiştirebilirsiniz. Bunu yapmak için, **Intune**  >  **cihazlar**  >  **tüm cihazlar** > bir cihaz > **Özellikler**  >  **birincil Kullanıcı**seçin. Daha fazla bilgi için bkz. [bir cihazın birincil kullanıcısını değiştirme](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Bu görev için yeni bir RBAC izni (yönetilen cihazlar/set birincil kullanıcı) de oluşturuldu. Bu izin, yardım masası operatörü, Okul Yöneticisi ve uç nokta güvenlik Yöneticisi dahil yerleşik rollere eklenmiştir.

Bu özellik, genel olarak önizleme aşamasında müşterilere gönderilir. Sonraki birkaç hafta içinde özelliği görmeniz gerekir.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>2 Mart 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri<!-- 6317104, CM3555758-->
Microsoft Uç Nokta Yöneticisi tek bir konsolda Configuration Manager ve Intune 'U bir araya getiriyor. Configuration Manager Technical Preview sürüm 2002,2 ' den başlayarak, Configuration Manager cihazlarınızı bulut hizmetine yükleyebilir ve yönetici merkezinde bu işlemler üzerinde işlem yapabilirsiniz. Daha fazla bilgi için [Configuration Manager Technical Preview sürüm 2002,2 ' deki Özellikler](/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach)bölümüne bakın.

Bu güncelleştirmeyi yüklemeden önce [Configuration Manager Technical Preview makalesini](/configmgr/core/get-started/technical-preview) gözden geçirin. Bu makale, Technical Preview kullanma, sürümler arasında güncelleştirme ve geri bildirim sağlama ile ilgili genel gereksinimleri ve sınırlamaları tamamladığınızda tercihinize.

#### <a name="bulk-remote-actions--4576882--"></a>Toplu uzak eylemler<!--4576882-->
Artık şu uzak eylemler için toplu komutlar verebilirsiniz: yeniden başlatma, yeniden adlandırma, Autopilot sıfırlama, silme ve silme. Yeni toplu eylemleri görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **tüm cihazlar**  >  **toplu eylemleri**' ne gidin.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Tüm cihazlar için geliştirilmiş arama, sıralama ve filtreleme listeleri<!--6179023-->
Tüm cihazlar listesi, daha iyi performans, arama, sıralama ve filtreleme için geliştirilmiştir. Daha fazla bilgi için [Bu destek ipucunu](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946)inceleyin.  

### <a name="app-management"></a>Uygulama yönetimi  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Android için Şirket Portalı 'de geliştirilmiş oturum açma deneyimi    
Daha modern, basit ve kullanıcılar için temiz bir deneyim sunmak amacıyla Android için Şirket Portalı uygulamasındaki çeşitli oturum açma ekranlarının yerleşimini güncelleştirdik. Geliştirmelere göz atmak için bkz. [uygulama kullanıcı arabirimindeki](./whats-new-app-ui.md)yenilikler.

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>24 Şubat 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>macOS Şirket Portalı Kullanıcı deneyimi geliştirmeleri<!-- 5568987 -->
MacOS cihaz kayıt deneyimlerine ve Mac için Şirket Portalı uygulamasına yönelik iyileştirmeler yaptık. Aşağıdaki geliştirmeleri görürsünüz:
- Kayıt sırasında, kullanıcılarınızın Şirket Portalı en son sürümüne sahip olmasını sağlayacak daha iyi bir Microsoft **Otomatik güncelleştirme** deneyimi.
- Kayıt sırasında gelişmiş bir uyumluluk denetimi adımı.
- Kopyalanmış olay kimlikleri için destek, kullanıcılarınız cihazlarından Şirket destek ekibine daha hızlı bir şekilde hata gönderebilir.

Mac için kayıt ve Şirket Portalı uygulaması hakkında daha fazla bilgi için bkz. [Şirket Portalı uygulamasını kullanarak macOS cihazınızı kaydetme](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Daha Iyi mobil için uygulama koruma ilkeleri artık iOS ve ıpados 'yi destekliyor<!-- 6224512  -->

Ekim 2019 ' de Intune uygulama koruma ilkesi, Microsoft tehdit savunma iş ortaklarımızın verilerini kullanma özelliğini ekledi. Bu güncelleştirmeyle, artık iOS ve ıpados üzerinde daha Iyi bir mobil uygulama kullanarak kullanıcıların şirket verilerini engellemek veya seçmeli olarak silmek için bir uygulama koruma İlkesi kullanabilirsiniz.  Daha fazla bilgi için bkz. [Intune Ile mobil tehdit savunma uygulama koruma Ilkesi oluşturma](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Tüm cihazlar listesinden Şimdi daraltılmış CSV biçiminde dışarı aktarır<!--6343117-->
Cihazlardan dışarı aktarmalar **Devices**  >  **tüm cihazlar** sayfası artık daraltılmış CSV biçimindedir.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>17 Şubat 2020 (2002 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>MacOS için Microsoft Defender Gelişmiş tehdit koruması (ATP) uygulaması<!-- 5424618 -->
Intune, macOS için Microsoft Defender Gelişmiş tehdit koruması (ATP) uygulamasını yönetilen Mac cihazlarına dağıtmanın kolay bir yolunu sunar. Daha fazla bilgi için bkz. [Mac için Microsoft Intune ve Microsoft Defender Gelişmiş tehdit koruması](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) [kullanarak MacOS CIHAZLARıNA Microsoft Defender ATP ekleme](../apps/apps-advanced-threat-protection-macos.md) .  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>İOS cihazlarında Cisco AnyConnect VPN ile ağ erişim denetimi 'ni (NAC) etkinleştirme<!-- 4860111  -->
İOS cihazlarında, bir VPN profili oluşturabilir ve Cisco AnyConnect gibi farklı bağlantı türleri kullanabilirsiniz (**cihaz yapılandırma**  >  **profilleri,**  >  **Create profile**  >  **iOS** bağlantı türü için **Cisco AnyConnect** for platform > **VPN** >

Cisco AnyConnect ile ağ erişim denetimi 'ni (NAC) etkinleştirebilirsiniz. Bu özelliği kullanmak için:

1. [Cisco kimlik hizmetleri altyapısı yönetici kılavuzunda](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html), Azure 'Da Cisco Identity Services altyapısını (ISE) YAPıLANDıRMAK Için **MDM sunucusu olarak Microsoft Intune yapılandırma** bölümündeki adımları kullanın.
2. Intune cihaz yapılandırma profilinde **ağ Access Control etkinleştir (NAC)** ayarını seçin.

Tüm kullanılabilir VPN ayarlarını görmek için [iOS CIHAZLARıNDA VPN ayarlarını yapılandırma](../configuration/vpn-settings-ios.md)bölümüne gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Apple MDM anında Iletme sertifikası sayfasındaki seri numarası<!--5947765  -->
Apple MDM anında Iletme sertifikası sayfasında artık seri numarası görüntülenir. Sertifikayı oluşturan Apple KIMLIĞINE erişim kaybolursa, Apple MDM anında Iletme sertifikasına erişimi yeniden kazanmak için seri numarası gereklidir. Seri numarasını görmek için **cihazlar**  >  **iOS**  >  **iOS kaydı**  >  **Apple MDM anında iletme sertifikası**' na gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Kayıtlı iOS/ıpados cihazlarına işletim sistemi güncelleştirmelerini göndermek için yeni güncelleştirme zamanlaması seçenekleri<!--5879689  -->
İOS/ıpados cihazları için işletim sistemi güncelleştirmelerini zamanlarken aşağıdaki seçenekler arasından seçim yapabilirsiniz. Bu seçenekler, Apple Business Manager veya Apple Okul Yöneticisi kayıt türlerini kullanan cihazlar için geçerlidir.
- Sonraki iadede Güncelleştir
- Zamanlanan süre içinde güncelleştirme
- Zamanlanan sürenin dışında güncelleştirme

İkinci iki seçenek için birden çok zaman penceresi oluşturabilirsiniz.

Yeni seçenekleri görmek için mem > **cihazlar**  >  **iOS**  >  **güncelleştirme ilkeleri iOS/ıpados**  >  **Create profile**bölümüne gidin.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Kayıtlı cihazlara hangi iOS/ıpados güncelleştirmelerinin göndermek istediğinizi seçin<!--5879689  -->
Apple Business Manager veya Apple Okul Yöneticisi kullanılarak kaydedilmiş cihazlara gönderim yapmak için belirli bir iOS/ıpados Güncelleştirmesi (en son güncelleştirme dışında) seçebilirsiniz. Bu tür cihazlarda, yazılım güncelleştirme görünürlüğünü birkaç gün boyunca geciktirmek için bir cihaz yapılandırma ilkesi ayarlanmış olmalıdır. Bu özelliği görmek için mem > **cihazlar**  >  **iOS**  >  **güncelleştirme ilkeleri iOS/ıpados**  >  **Create profile**bölümüne gidin.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="improved-intune-reporting-experience---3791418-----"></a>İyileştirilmiş Intune raporlama deneyimi<!-- 3791418   -->
Intune artık yeni rapor türleri, daha iyi rapor organizasyonu, daha odaklanmış görünümler, geliştirilmiş rapor işlevselliği ve daha tutarlı ve zamanında veriler de dahil olmak üzere gelişmiş bir raporlama deneyimi sunmaktadır. Raporlama deneyimi, genel önizlemeden GA 'ye (genel kullanılabilirlik) geçmeyecektir. Ayrıca, GA sürümü, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'ndeki kutucuklar üzerinde yerelleştirme desteği, hata düzeltmeleri, tasarım iyileştirmeleri ve cihaz uyumluluk verileri toplama sağlar.

Yeni rapor türleri aşağıdaki bilgilere odaklanmaktadır:

- **İşletimsel** -negatif bir sistem durumu odaklı yeni kayıtlar sağlar. 
- **Kuruluş** -genel durumun daha geniş bir özetini sağlar.
- **Geçmiş** -bir süre boyunca desenler ve eğilimler sağlar.
- **Uzman** -kendi özel raporlarınızı oluşturmak için ham verileri kullanmanıza olanak sağlar.

Yeni raporların ilk kümesi cihaz uyumluluğuna odaklanır. Daha fazla bilgi için bkz. [blog-Microsoft Intune raporlama çerçevesi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) ve [Intune raporları](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Kullanıcı arabirimindeki güvenlik temellerinin konumu birleştirildi<!-- 6177074   -->
Çeşitli kullanıcı arabirimi konumlarından *güvenlik temellerini* kaldırarak Microsoft Endpoint Manager Yönetim merkezinde [güvenlik temellerini](../protect/security-baselines.md) bulmak için yolları birleştiriyoruz. Güvenlik temellerini bulmak için şu yolu kullanın: **uç nokta güvenlik**  >  **güvenliği temelleri**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>İçeri aktarılan PKCS sertifikaları için genişletilmiş destek<!-- 6044197  -->
*Android kurumsal tam olarak yönetilen cihazları*desteklemek için [içeri aktarılan PKCS sertifikalarını](../protect/certificates-imported-pfx-configure.md#supported-platforms) kullanma desteğini genişlettik. Genellikle, PFX sertifikalarını içeri aktarma işlemi, e-posta şifrenin gerçekleşebilmesi için bir kullanıcının tüm cihazlarında gerekli olduğu S/MIME şifreleme senaryolarında kullanılır.

Aşağıdaki platformlar PFX sertifikalarının içeri aktarımını destekler:

- Android-Cihaz Yöneticisi
- Android kurumsal-tam yönetilen
- Android kurumsal Iş profili
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Cihazlar için uç nokta güvenlik yapılandırmasını görüntüleme<!-- 6206460  -->
[Belirli bir cihaza uygulanan Endpoint Security yapılandırmalarının](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)görüntülenmesi Için Microsoft Endpoint Manager Yönetim Merkezi ' nde seçeneğin adını güncelleştirdik. Bu seçenek, uygun güvenlik temellerini ve güvenlik temelleri dışında oluşturulan ek ilkeleri gösterdiği için **uç nokta güvenlik yapılandırması** olarak yeniden adlandırılır. Daha önce Bu seçenek *güvenlik temelleri*olarak adlandırılmıştı.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Intune rolleri Kullanıcı arabirimi değişiklikleri geliyor<!--5801612   -->
[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **kiracı yönetim**rolleri için Kullanıcı arabirimi,  >  **Roles** daha kolay ve sezgisel bir tasarıma geliştirilmiştir. Bu deneyim, şimdi kullandığınız ayarların ve ayrıntıların aynısını sağlar, ancak yeni deneyim sihirbaz benzeri bir işlem kullanır.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>17 Şubat 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsofts-new-office-app---5859926---"></a>Microsoft 'un yeni Office uygulaması<!-- 5859926 -->
Microsoft 'un yeni Office uygulaması artık indirme ve kullanım için genel kullanıma sunulmuştur. Office uygulaması, kullanıcılarınızın tek bir uygulama içinde Word, Excel ve PowerPoint 'te çalışabilecekleri birleştirilmiş bir deneyimdir. Erişilmekte olan verilerin korunduğundan emin olmak için uygulamayı bir uygulama koruma ilkesiyle hedefleyebilirsiniz.

Daha fazla bilgi için bkz. [Office mobil önizleme uygulamasıyla Intune uygulama koruma ilkelerini etkinleştirme](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>10 Şubat 2020 haftası

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 genişletilmiş desteği sonlandırır<!--3042987 -->
Windows 7, 14 Ocak 2020 ' de Genişletilmiş desteğin sonuna ulaştı. Intune, Windows 7 çalıştıran cihazlar için aynı anda kullanım dışı desteği. BILGISAYARıNıZı korumaya yardımcı olan teknik yardım ve otomatik güncelleştirmeler artık kullanılamaz. Windows 10 ' a yükseltmeniz gerekir. Daha fazla bilgi için bkz. [değişiklik için blog gönderisi planı](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Windows 10 cihazlarda Microsoft Edge sürüm 77 ve üzeri<!-- 5843584 -->
Intune artık Windows 10 cihazlarda Microsoft Edge sürüm 77 ve üstünü kaldırmayı desteklemektedir. Daha fazla bilgi için bkz. [Windows 10 Için Microsoft Edge 'i Microsoft Intune 'e ekleme](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Şirket Portalı, Android iş profili kaydından kaldırılan ekran<!--6103987 -->
**Sonraki nedir?** ekranı, Kullanıcı deneyimini kolaylaştırmak Için Şirket portalı Android iş profili kayıt akışından kaldırılmıştır. Güncelleştirilmiş Android iş profili kayıt akışını görmek için [Android iş profiline kaydol](../user-help/enroll-device-android-work-profile.md) ' a gidin.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Şirket Portalı Uygulama performansı geliştirildi<!-- 6178652 -->
Şirket Portalı uygulaması, Surface Pro X gibi ARM64 işlemciler kullanan cihazlar için iyileştirilmiş performansı destekleyecek şekilde güncelleştirilmiştir. daha önce, öykünülmüş bir ARM32 modunda çalıştırılan Şirket Portalı. Artık sürüm 10.4.7080.0 ve üzeri sürümlerde Şirket Portalı uygulaması, ARM64 için yerel olarak derlenir. Şirket Portalı uygulaması hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

## <a name="whats-new-archive"></a>Yenilikler arşivi
Önceki aylar için bkz. yenilikler [Arşivi](whats-new-archive.md).

## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]