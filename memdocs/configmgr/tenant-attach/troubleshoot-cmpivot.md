---
title: Yönetim merkezine yüklenen cihazlar için CMPivot sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager kiracı iliştirme için sorun giderme CMPivot
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 86f97154-c9fc-4efd-9d49-4a253cef5953
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 7b7e8b347dee46e42f9fe9d9cb89332a3ee1bef5
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643385"
---
# <a name="troubleshoot-cmpivot-preview-for-devices-uploaded-to-the-admin-center"></a>Yönetim merkezine yüklenen cihazlar için CMPivot (Önizleme) sorunlarını giderme
<!--6024392-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Endpoint Manager Yönetim Merkezi 'nde CMPivot sorunlarını gidermek için aşağıdakileri kullanın:

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

## <a name="common-issues"></a>Genel sorunlar

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> Gerekli Yapılandırma Azure Active Directory eksik

**Hata iletisi:** Gerekli Yapılandırma Azure Active Directory eksik. Configuration Manager sitesini Azure kiracınıza iliştirdiğinizden ve uygun Kullanıcı rolünü Azure AD 'ye atadığınızdan emin olun.

**Olası neden:** Kullanıcı hesabının Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü eksik olabilir. Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir. Bu izne yapılan değişikliklerin etkili olması bir saate kadar sürebilir.

### <a name="unable-to-get-device-information"></a><a name="bkmk_noinfo"></a> Cihaz bilgisi alınamıyor

**Hata iletisi 1:** Cihaz bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

**Olası nedenler:** Genellikle, bu hataya yönetici hesabındaki bir sorun neden olur. Aşağıda, yönetim kullanıcı hesabıyla ilgili en yaygın sorunlar verilmiştir:

1. Yönetici merkezinde oturum açmak için aynı hesabı kullanın. Şirket içi kimliğin ile eşitlenmesi ve bulut kimliğiyle eşleşmesi gerekir.
1. Hesabın Configuration Manager, cihazın **koleksiyonu** için **okuma** iznine sahip olduğunu doğrulayın.
1. Configuration Manager, Microsoft Endpoint Manager Yönetim Merkezi 'ndeki kiracı iliştirme özelliklerine erişmek için kullanmakta olduğunuz yönetim kullanıcı hesabını bulduğundan emin olun. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Kullanıcılar** düğümünü seçin ve kullanıcı hesabınızı bulun.

    Hesabınız **Kullanıcılar** düğümünde listelenmiyorsa, sitenin [Active Directory Kullanıcı bulmanın](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)yapılandırmasını denetleyin.

1. Bulma verilerini doğrulayın. Kullanıcı hesabınızı seçin. Şeritte, **giriş** sekmesinde **Özellikler**' i seçin. Özellikler penceresinde, aşağıdaki bulma verilerini onaylayın:

    - **Azure Active Directory KIRACı kimliği**: Bu değer, Azure AD kiracısı IÇIN bir GUID olmalıdır.
    - **Azure Active Directory Kullanıcı kimliği**: Bu değer, Azure AD 'de bu hesap IÇIN bir GUID olmalıdır.
    - **Kullanıcı asıl adı**: Bu değerin biçimi user@domain . Örneğin, `jqpublic@contoso.com`.

    Azure AD özellikleri boşsa, sitenin [Azure AD Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)yapılandırmasını denetleyin.


### <a name="not-authorized-to-view-query-results"></a><a name="bkmk_rbac"></a> Sorgu sonuçlarını görüntüleme yetkisi yok

**Hata iletisi:** Sorgu sonuçlarını görüntüleme yetkisi yok. Configuration Manager 'de CMPivot için izin verildiğini doğrulayın

**Olası nedenler:** Kullanıcı hesabının CMPivot için izinlere sahip olduğunu doğrulayın. Daha fazla bilgi için bkz. [CMPivot Için izinler](cmpivot-start.md#permissions).

#### <a name="other-possible-causes-of-unexpected-errors"></a><a name="bkmk_other"></a> Beklenmeyen hataların diğer olası nedenleri

Beklenmeyen hatalara genellikle [hizmet bağlantı noktası](../core/servers/deploy/configure/about-the-service-connection-point.md), [Yönetim hizmeti](../develop/adminservice/overview.md)veya bağlantı sorunları neden olmuş olabilir.

1. Hizmet bağlantı noktasının **Cmgatewaynotificationworker. log**kullanarak buluta bağlantı olduğunu doğrulayın.
1. Merkezi sitedeki site bileşeni izlemenin SMS_REST_PROVIDER bileşenini inceleyerek yönetim hizmetinin sağlıklı olduğunu doğrulayın.
1. IIS 'nin sağlayıcı makinesine yüklenmesi gerekir. Daha fazla bilgi için bkz. [Yönetim hizmeti önkoşulları](../develop/adminservice/overview.md#prerequisites).

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="inconsistent-results-for-some-operators-with-configuration-manager-version-2002"></a>Configuration Manager sürüm 2002 ile bazı işleçler için tutarsız sonuçlar
<!--7784718, 7884272-->
Microsoft Endpoint Manager Yönetim Merkezi 'ndeki Configuration Manager sürüm 2002 ile CMPivot kullanırken, aşağıdaki işleçler için tutarsız sonuçlar alabilirsiniz:

- Özetleme ölçütü
- Take
- Sıralama ölçütü
- Üst
- Count
- Distinct

**Çözüm**: [KB4578123-CMPivot sorguları Install geçerli Configuration Manager dalı, sürüm 2002 ' de beklenmeyen sonuçlar döndürüyor](https://support.microsoft.com/help/4578123).

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> SMS sağlayıcısı CA 'lardan uzak olduğunda, Yönetici konsolundan bir iç sunucu hatasıyla karşılaşabilirsiniz

**Hata iletisi:** Şirket içi hata kodu: 500 iç sunucu hatası

**Senaryo 1:** Configuration Manager sürüm 2002 çalıştırılırken ve CA 'LAR için uzak bir sağlayıcı varsa, Yönetici konsolundan bir iç sunucu hatasıyla karşılaşabilirsiniz.

**Senaryo 2:** Configuration Manager sürüm 2006 ' i çalıştırırken, hizmet bağlantı noktası birincil sitede sağlayıcıya bağlanamazsa ve CA 'lara geri dönmek için bu hatayla karşılaşabilirsiniz. 

**Senaryo 3:** CA 'LAR sürüm 2006 ' e yükseltildiyse ancak birincil site henüz yükseltilmemişse, istekler CAS sağlayıcısı aracılığıyla yönlendirilir. Sağlayıcı uzak ise, yönetim konsolundan bir iç sunucu hatasıyla karşılaşabilirsiniz. 

**Geçici çözüm:** Bu "çift atlama" senaryosuna geçici çözüm için CMPivot makalesinde bulunan [CA 'ların uzak sağlayıcı](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) senaryosuna yönelik yönergeleri izleyin.


[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Sonraki adımlar

[Kiracı eklemeyle ilgili sorunları giderme](troubleshoot.md)
