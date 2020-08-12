---
title: Microsoft Endpoint Manager kiracısı ekleme
titleSuffix: Configuration Manager
description: Configuration Manager cihazlarınızı bulut hizmetine yükleyin ve yönetim merkezinden işlem yapın.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 784a287176066ce34c3499ecdc91a450e2d6160c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127554"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri
<!--3555758 live 3/4/2020-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir.

Configuration Manager sürüm 2002 ' den başlayarak, Configuration Manager cihazlarınızı bulut hizmetine yükleyebilir ve yönetim merkezindeki **cihazlar** dikey penceresinden eylemler gerçekleştirebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

- Bu değişiklik uygulanırken oturum açmak için *genel yönetici* olan bir hesap. Daha fazla bilgi için bkz. [Azure Active Directory (Azure AD) yönetici rolleri](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Ekleme, Azure AD kiracınızda üçüncü taraf bir uygulama ve birinci taraf hizmet sorumlusu oluşturur.
- Azure genel bulut ortamı.
- Cihaz eylemlerini tetikleyen Kullanıcı hesapları aşağıdaki önkoşullara sahiptir:
   - [Azure Active Directory Kullanıcı bulma](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) ve [Active Directory Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)ile birlikte keşfedilmiştir.
      - Bu, Kullanıcı hesabının Azure AD 'de eşitlenmiş bir kullanıcı nesnesi olması gerektiği anlamına gelir.
   - Microsoft Endpoint Manager Yönetim merkezinde **uzak görevler** altında **Configuration Manager eylemi Başlat** izni.


## <a name="internet-endpoints"></a>Internet uç noktaları

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a>Ortak yönetim zaten etkin olduğunda cihaz yüklemeyi etkinleştir

Şu anda ortak yönetim 'i etkinleştirdiyseniz, cihaz yüklemeyi etkinleştirmek için ortak yönetim özelliklerini kullanacaksınız. Ortak yönetim zaten etkin olmadığında, bunun yerine cihaz yüklemeyi etkinleştirmek için [ **ortak yönetim yapılandırma** Sihirbazı 'nı kullanın](#bkmk_config) .

Ortak yönetim zaten etkin olduğunda, aşağıdaki yönergeleri kullanarak cihaz karşıya yüklemeyi etkinleştirmek için ortak yönetim özelliklerini düzenleyin:

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
1. Şeritte, ortak yönetim üretim ilkenize yönelik **Özellikler** ' i seçin.
1. **Karşıya yüklemeyi Yapılandır** sekmesinde, **Microsoft Endpoint Manager yönetim merkezine yükle**' yi seçin. **Uygula**’yı seçin.
   - Cihaz yükleme için varsayılan ayar, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm cihazlardır**. Gerekirse, karşıya yüklemeyi tek bir cihaz koleksiyonuna sınırlayabilirsiniz.
1. [Endpoint](../../analytics/overview.md)Analytics 'te Son Kullanıcı deneyimini Iyileştirmek Istiyorsanız **Microsoft Endpoint Manager 'A yüklenen cihazlarda Endpoint Analytics 'i etkinleştirme** seçeneğini işaretleyin.

   [![Cihazları Microsoft Endpoint Manager yönetim merkezine yükleme](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. İstendiğinde *genel yönetici* hesabınızla oturum açın.
1. **AAD uygulaması oluştur** bildirimini kabul etmek için **Evet** ' i seçin. Bu eylem, bir hizmet sorumlusu sağlar ve eşitlemeyi kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.
1. Değişiklik yapmayı tamamladıktan sonra ortak yönetim özelliklerinden çıkmak için **Tamam ' ı** seçin.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a>Ortak yönetim etkin olmadığında cihaz yüklemeyi etkinleştir

Ortak yönetim özelliği etkinleştirilmemişse, cihaz yüklemeyi etkinleştirmek için **ortak yönetim yapılandırma** Sihirbazı 'nı kullanırsınız. Ortak yönetim için otomatik kayıt veya Intune 'a geçiş iş yüklerini etkinleştirmek zorunda kalmadan cihazlarınızı karşıya yükleyebilirsiniz. **İstemci** sütununda **Evet** olan Configuration Manager tarafından yönetilen tüm cihazlar karşıya yüklenir. Gerekirse, karşıya yüklemeyi tek bir cihaz koleksiyonuna sınırlayabilirsiniz. Ortak yönetim ortamınızda zaten etkinleştirilmişse, bunun yerine cihaz yüklemeyi etkinleştirmek için [ortak yönetim özelliklerini düzenleyin](#bkmk_edit) .

Ortak yönetim etkin olmadığında, cihaz yüklemeyi etkinleştirmek için aşağıdaki yönergeleri kullanın:

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
1. Şeritte, Sihirbazı açmak için **ortak yönetimi Yapılandır** ' ı seçin.
1. **Kiracı ekleme** sayfasında, ortamınız için **AzurePublicCloud** ' yi seçin. Azure Kamu bulutu ve Azure Çin 21Vianet desteklenmez.
1. **Oturum aç '** ı seçin. Oturum açmak için *genel yönetici* hesabınızı kullanın.
1. **Kiracı ekleme** sayfasında **Microsoft Endpoint Manager Yönetim Merkezi 'ne yükle** seçeneğinin seçili olduğundan emin olun.
   - Ortak yönetimi şimdi etkinleştirmek istemiyorsanız **ortak yönetim için otomatik istemci kaydını etkinleştir** seçeneğinin işaretli olmadığından emin olun. Ortak yönetimi etkinleştirmek istiyorsanız, seçeneğini belirleyin.
   - Ortak yönetimi cihaz karşıya yükleme ile birlikte etkinleştirirseniz, sihirbazın tamamlaması için ek sayfalar vermiş olursunuz. Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](../comanage/how-to-enable.md).

   [![Ortak yönetim Yapılandırma Sihirbazı](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. **AAD uygulaması oluştur** bildirimini kabul etmek için **İleri** ' yi ve ardından **Evet** ' i seçin. Bu eylem, bir hizmet sorumlusu sağlar ve eşitlemeyi kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.
     - İsteğe bağlı olarak, kiracı ekleme ekleme sırasında (sürüm 2006 ' den başlayarak) önceden oluşturulmuş bir Azure AD uygulamasını içeri aktarabilirsiniz. Daha fazla bilgi için, [önceden oluşturulmuş bir Azure AD uygulamasını Içeri aktarma](#bkmk_aad_app) bölümüne bakın.
1. **Karşıya yüklemeyi Yapılandır** sayfasında, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm Cihazlarım**için önerilen cihaz karşıya yükleme ayarını seçin. Gerekirse, karşıya yüklemeyi tek bir cihaz koleksiyonuna sınırlayabilirsiniz.
1. [Endpoint](../../analytics/overview.md) Analytics 'te Son Kullanıcı deneyimini Iyileştirmek Istiyorsanız **Microsoft Endpoint Manager 'a yüklenen cihazlar için Endpoint Analytics 'i etkinleştirme** seçeneğini işaretleyin
1. Seçiminizi gözden geçirmek için **Özet** ' i seçin ve ardından **İleri**' yi seçin.
1. Sihirbaz tamamlandığında **Kapat**' ı seçin.  

## <a name="perform-device-actions"></a>Cihaz eylemlerini gerçekleştirme

1. Bir tarayıcıda şuraya gidin`endpoint.microsoft.com`
1. Yüklenen cihazları görmek için **cihazlar** ' ı ve ardından **tüm cihazlar** ' ı seçin. **ConfigMgr** 'yi karşıya yüklenen cihazlar Için **tarafından yönetilen** sütununda görürsünüz.
   [![Microsoft Endpoint Manager Yönetim Merkezi 'ndeki tüm cihazlar](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. **Genel bakış** sayfasını yüklemek için bir cihaz seçin.
1. Aşağıdaki eylemlerden birini seçin:
   - **Makine Ilkesini Eşitle**
   - **Kullanıcı Ilkesini eşitleme**
   - **Uygulama değerlendirme çevrimi**

   [![Microsoft Endpoint Manager Yönetim Merkezi 'nde cihaza genel bakış](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a>Önceden oluşturulmuş bir Azure AD uygulamasını içeri aktarma (isteğe bağlı)
<!--6479246-->
*(Sürüm 2006 ' de tanıtılmıştır)*

Yeni bir [ekleme](#bkmk_config)sırasında, yönetici Kiracı ekleme sırasında daha önce oluşturulmuş bir uygulama belirtebilir. Azure AD uygulamalarını birden çok hiyerarşilerde paylaşma veya yeniden kullanma. Birden çok hiyerarşsahipseniz, her biri için ayrı Azure AD uygulamaları oluşturun.

**Ortak yönetim Yapılandırma Sihirbazı**'ndaki **kiracı ekleme** sayfasında, **Configuration Manager istemci verilerini Microsoft Endpoint Manager Yönetim Merkezi Ile eşleştirmek için isteğe bağlı olarak ayrı bir Web uygulaması içeri aktar**' ı seçin. Bu seçenek, Azure AD uygulamanız için aşağıdaki bilgileri belirtmenizi ister:

- Azure AD kiracı adı
- Azure AD kiracı kimliği
- Uygulama adı
- İstemci Kimliği
- Gizli anahtar
- Gizli anahtar süre sonu
- Uygulama Kimliği URI'si

### <a name="azure-ad-application-permissions-and-configuration"></a>Azure AD uygulama izinleri ve yapılandırması

Kiracı iliştirme 'ye ekleme sırasında önceden oluşturulmuş bir uygulamanın kullanılması için aşağıdaki izinler gerekir:

- Configuration Manager Mikro hizmet izinleri:
   - CmCollectionData. Read
   - CmCollectionData. Write

- Microsoft Graph izinleri:
   - Directory. Read. tüm [uygulamalar izni](https://docs.microsoft.com/graph/permissions-reference#application-permissions)
   - Directory. Read. tüm [temsilci Dizin izni](https://docs.microsoft.com/graph/permissions-reference#directory-permissions)

- Azure AD uygulaması için **kiracı için yönetici onayı izninin** seçildiğinden emin olun. Daha fazla bilgi için bkz. [uygulama kayıtları yönetici onayı verme](https://docs.microsoft.com/azure/active-directory/manage-apps/grant-admin-consent).

- İçeri aktarılan uygulamanın aşağıdaki şekilde yapılandırılması gerekir:
   - **Yalnızca bu kuruluş dizinindeki hesaplar**için kaydedilir. Daha fazla bilgi için bkz. [uygulamanıza kimlerin erişebileceğini değiştirme](https://docs.microsoft.com/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Geçerli bir uygulama KIMLIĞI URI 'SI ve gizli anahtarı vardır



## <a name="next-steps"></a>Sonraki adımlar

- [Configuration Manager cihazlarını Endpoint Analytics 'e kaydetme](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Kiracı iliştirme günlük dosyaları hakkında daha fazla bilgi için bkz. [kiracı Iliştirme sorunlarını giderme](troubleshoot.md).
