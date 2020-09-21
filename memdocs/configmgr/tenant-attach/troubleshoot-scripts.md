---
title: Yönetim merkezine yüklenen cihazlar için betiklerin sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager kiracı iliştirme için betikler sorunlarını giderme
ms.date: 09/18/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: a0eb1e8f-2c85-4f48-a0b5-945b3e5f63f3
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: b42663e649f50d1a785bf929d0b03fb4d2eb0632
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90803304"
---
# <a name="troubleshoot-scripts-preview-for-devices-uploaded-to-the-admin-center"></a>Yönetim merkezine yüklenen cihazlar için betiklerin (Önizleme) sorunlarını giderme
<!--6024392-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Endpoint Manager Yönetim Merkezi 'ndeki betiklerin sorunlarını gidermek için aşağıdakileri kullanın:

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

## <a name="common-issues"></a>Genel sorunlar

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> Gerekli Yapılandırma Azure Active Directory eksik

**Hata iletisi:** Gerekli Yapılandırma Azure Active Directory eksik. Configuration Manager sitesini Azure kiracınıza iliştirdiğinizden ve uygun Kullanıcı rolünü Azure AD 'ye atadığınızdan emin olun.

**Olası neden:** Kullanıcı hesabının Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü eksik olabilir. Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir. Bu izne yapılan değişikliklerin etkili olması bir saate kadar sürebilir.

### <a name="configuration-manager-doesnt-meet-the-minimum-version-prerequisite"></a><a name="bkmk_version"></a> Configuration Manager en düşük sürüm önkoşullarını karşılamıyor

**Hata iletisi:** Configuration Manager en düşük sürüm önkoşullarını karşılamıyor.

**Olası nedenler:** Configuration Manager siteleriniz [, Configuration Manager geçerli dalı için sürüm 2006 ' nin yüklü olduğu Configuration Manager KB4580678-Tenant iliştirme toplamasına](https://support.microsoft.com/help/4580678) sahip en düşük 2006 sürümünü çalıştırmıyor. Aşağıdakileri doğrulayın:
 - Configuration Manager sürüm 2006 veya üzeri yüklendi.
 - Configuration Manager sürüm 2006 çalıştıran sitelerde bu [KB4580678](https://support.microsoft.com/help/4580678) .
 - Hiyerarşideki her site yukarıda listelenen en az UMS karşılıyor.

### <a name="unable-to-get-scripts-information"></a><a name="bkmk_403"></a> Betikler bilgisi alınamıyor

**Hata iletisi:** Betiklerin bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve Microsoft Endpoint Manager yönetim merkezinden kiracı iliştirme özelliklerine erişen kullanıcı hesabının her ikisi tarafından keşfedildiğini doğrulayın. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

**Olası nedenler:** Genellikle, bu hataya yönetici hesabındaki bir sorun neden olur. Aşağıda, yönetim kullanıcı hesabıyla ilgili en yaygın sorunlar verilmiştir:

1. Yönetici merkezinde oturum açmak için aynı hesabı kullanın. Şirket içi kimliğin ile eşitlenmesi ve bulut kimliğiyle eşleşmesi gerekir.
1. Hesabın Configuration Manager, cihazın **koleksiyonu** için **okuma** iznine sahip olduğunu doğrulayın.
1. Hesabın Configuration Manager içindeki **koleksiyon** Için **kaynak okuma** iznine sahip olduğunu doğrulayın.
1. Configuration Manager, Microsoft Endpoint Manager Yönetim Merkezi 'ndeki kiracı iliştirme özelliklerine erişmek için kullanmakta olduğunuz yönetim kullanıcı hesabını bulduğundan emin olun. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Kullanıcılar** düğümünü seçin ve kullanıcı hesabınızı bulun.

    Hesabınız **Kullanıcılar** düğümünde listelenmiyorsa, sitenin [Active Directory Kullanıcı bulmanın](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)yapılandırmasını denetleyin.

1. Bulma verilerini doğrulayın. Kullanıcı hesabınızı seçin. Şeritte, **giriş** sekmesinde **Özellikler**' i seçin. Özellikler penceresinde, aşağıdaki bulma verilerini onaylayın:

    - **Azure Active Directory KIRACı kimliği**: Bu değer, Azure AD kiracısı IÇIN bir GUID olmalıdır.
    - **Azure Active Directory Kullanıcı kimliği**: Bu değer, Azure AD 'de bu hesap IÇIN bir GUID olmalıdır.
    - **Kullanıcı asıl adı**: Bu değerin biçimi user@domain . Örneğin, `jqpublic@contoso.com`.

    Azure AD özellikleri boşsa, sitenin [Azure AD Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)yapılandırmasını denetleyin.


### <a name="unable-to-get-device-information"></a><a name="bkmk_noinfo"></a> Cihaz bilgisi alınamıyor

**Hata iletisi:** Cihaz bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

**Olası neden:** Configuration Manager, Microsoft Endpoint Manager Yönetim Merkezi 'ndeki kiracı iliştirme özelliklerine erişmek için kullanmakta olduğunuz yönetim kullanıcı hesabını bulduğundan emin olun. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Kullanıcılar** düğümünü seçin ve kullanıcı hesabınızı bulun.

   Hesabınız **Kullanıcılar** düğümünde listelenmiyorsa, sitenin [Active Directory Kullanıcı bulmanın](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)yapılandırmasını denetleyin.

1. Bulma verilerini doğrulayın. Kullanıcı hesabınızı seçin. Şeritte, **giriş** sekmesinde **Özellikler**' i seçin. Özellikler penceresinde, aşağıdaki bulma verilerini onaylayın:

    - **Azure Active Directory KIRACı kimliği**: Bu değer, Azure AD kiracısı IÇIN bir GUID olmalıdır.
    - **Azure Active Directory Kullanıcı kimliği**: Bu değer, Azure AD 'de bu hesap IÇIN bir GUID olmalıdır.
    - **Kullanıcı asıl adı**: Bu değerin biçimi user@domain . Örneğin, `jqpublic@contoso.com`.

    Azure AD özellikleri boşsa, sitenin [Azure AD Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)yapılandırmasını denetleyin.


### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a> Beklenmeyen bir hata oluştu

**Hata iletisi:** Beklenmeyen bir hata oluştu

#### <a name="possible-cause"></a>Olası nedeni

Hesabın Configuration Manager içindeki **koleksiyon** Için **kaynak okuma** iznine sahip olduğunu doğrulayın.

#### <a name="error-code-500-with-an-unexpected-error-occurred-message"></a>Hata kodu 500, beklenmeyen bir hata oluştu iletisi

`System.Security.SecurityException` **Adminservice. log**dosyasında görüyorsanız, [Active Directory Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) tarafından KEŞFEDILEN Kullanıcı asıl adınızın (UPN) Şirket ıçı UPN yerine bir bulut UPN olarak ayarlandığını doğrulayın. Boş bir UPN değeri de kabul edilebilir çünkü Active Directory bulunan etki alanı adının kullanıldığı anlamına gelir. Geçerli bir etki alanı UPN (contoso.com) olmayan yalnızca bulutta bulunan UPN (örnek: onmicrosoft.com) görürseniz, bir sorununuz vardır ve [ACTIVE DIRECTORY UPN sonekini ayarlamanız](/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them)gerekebilir.


#### <a name="other-possible-causes-of-unexpected-errors"></a>Beklenmeyen hataların diğer olası nedenleri

Beklenmeyen hatalara genellikle [hizmet bağlantı noktası](../core/servers/deploy/configure/about-the-service-connection-point.md), [Yönetim hizmeti](../develop/adminservice/overview.md)veya bağlantı sorunları neden olmuş olabilir.

1. Hizmet bağlantı noktasının **Cmgatewaynotificationworker. log**kullanarak buluta bağlantı olduğunu doğrulayın.
1. Merkezi sitedeki site bileşeni izlemenin SMS_REST_PROVIDER bileşenini inceleyerek yönetim hizmetinin sağlıklı olduğunu doğrulayın.
1. IIS 'nin sağlayıcı makinesine yüklenmesi gerekir. Daha fazla bilgi için bkz. [Yönetim hizmeti önkoşulları](../develop/adminservice/overview.md#prerequisites).

## <a name="known-issues"></a>Bilinen sorunlar

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]
