---
title: Kaynak Gezgini sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager kiracı iliştirme için kaynak Gezgini sorunlarını giderme
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 05829d36-2cbf-4921-bf4b-cfcdef4cfcc1
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a93127e28d451c74828c4362fa00418e35c6e56f
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564365"
---
# <a name="troubleshoot-resource-explorer-for-devices-uploaded-to-the-admin-center-preview"></a>Yönetim merkezine yüklenen cihazlar için kaynak Gezgini sorunlarını giderme (Önizleme)
<!--6479284-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Endpoint Manager Yönetim Merkezi 'nde ConfigMgr cihazları için kaynak Gezgini sorunlarını gidermek için aşağıdakileri kullanın:

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Microsoft Endpoint Manager Yönetim Merkezi 'ndeki yaygın hatalar

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> Gerekli Yapılandırma Azure Active Directory eksik

**Hata iletisi:** Gerekli Yapılandırma Azure Active Directory eksik. Configuration Manager sitesini Azure kiracınıza iliştirdiğinizden ve uygun Kullanıcı rolünü Azure AD 'ye atadığınızdan emin olun.

**Olası neden:** Kullanıcı hesabının Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü eksik olabilir. Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir. Bu izne yapılan değişikliklerin etkili olması bir saate kadar sürebilir.

### <a name="unable-to-get-resource-information"></a><a name="bkmk_noinfo"></a> Kaynak bilgisi alınamıyor

**Hata iletisi 1:** Kaynak bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

**Olası nedenler:** Genellikle, bu hataya yönetici hesabındaki bir sorun neden olur. Aşağıda, yönetim kullanıcı hesabıyla ilgili en yaygın sorunlar verilmiştir:

1. Yönetici merkezinde oturum açmak için aynı hesabı kullanın. Şirket içi kimliğin ile eşitlenmesi ve bulut kimliğiyle eşleşmesi gerekir.
1. Hesabın Configuration Manager, cihazın **koleksiyonu** için **okuma** iznine sahip olduğunu doğrulayın.
1. Configuration Manager, kullanmakta olduğunuz yönetim kullanıcı hesabını keşfettiği emin olun. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Kullanıcılar** düğümünü seçin ve kullanıcı hesabınızı bulun.

    Hesabınız **Kullanıcılar** düğümünde listelenmiyorsa, sitenin [Active Directory Kullanıcı bulmanın](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)yapılandırmasını denetleyin.

1. Bulma verilerini doğrulayın. Kullanıcı hesabınızı seçin. Şeritte, **giriş** sekmesinde **Özellikler**' i seçin. Özellikler penceresinde, aşağıdaki bulma verilerini onaylayın:

    - **Azure Active Directory KIRACı kimliği**: Bu değer, Azure AD kiracısı IÇIN bir GUID olmalıdır.
    - **Azure Active Directory Kullanıcı kimliği**: Bu değer, Azure AD 'de bu hesap IÇIN bir GUID olmalıdır.
    - **Kullanıcı asıl adı**: Bu değerin biçimi user@domain . Örneğin, `jqpublic@contoso.com`.

    Azure AD özellikleri boşsa, sitenin [Azure AD Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)yapılandırmasını denetleyin.

### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a> Site bilgileri henüz eşitlenmedi

**Hata iletisi:** Site bilgileri henüz Microsoft Endpoint Manager yönetim merkezine Configuration Manager ile eşitlenmemiş. 

**Olası nedenler:**
- Bu hata genellikle kiracı iliştirme 'ye yeni ekleme gerçekleştirildiğinde oluşur. Bilgilerin eşitlenmesi için bir saat bekleyin.
- Bu hata, merkezi yönetim sitesi yeni bir Configuration Manager sürümüne yükseltildiyse ancak bazı alt birincil siteler henüz yükseltilmemişse de görünebilir.

### <a name="unable-to-load-inventory-classes"></a><a name="bkmk_load"></a> Envanter sınıfları yüklenemiyor

**Hata iletisi:** Ortamınız için envanter sınıfları yüklenemiyor.

**Olası nedenler:**

- Varlıkların listesi Şirket içinden karşıya yüklenmemiş olabilir. Bir saat bekleyip hatanın devam edip etmediğini inceleyin.
- Geçersiz **KIRACı kimliği** veya **hiyerarşi kimliği** belirtilmiş olabilir. Hizmet bağlantı noktasını denetleyin ve çalıştığından emin olun.
- Sınıfları almak için sorgu başarıyla yürütülemedi. Hatanın devam edip etmediğini görmek için 15 dakika bekleyin.

### <a name="failed-to-get-inventory-classes-with-data"></a><a name="bkmk_get"></a> Envanter sınıfları verilerle alınamadı

**Hata iletisi:** Envanter sınıfları verilerle alınamadı. Şirket içi hatası 500.

**Olası nedenler:** Beklenmeyen hatalara genellikle [hizmet bağlantı noktası](../core/servers/deploy/configure/about-the-service-connection-point.md), [Yönetim hizmeti](../develop/adminservice/overview.md)veya bağlantı sorunları neden olmuş olabilir.

1. Hizmet bağlantı noktasının **Cmgatewaynotificationworker. log**kullanarak buluta bağlantı olduğunu doğrulayın.
1. Merkezi sitedeki site bileşeni izlemenin SMS_REST_PROVIDER bileşenini inceleyerek yönetim hizmetinin sağlıklı olduğunu doğrulayın.
1. IIS 'nin sağlayıcı makinesine yüklenmesi gerekir. Daha fazla bilgi için bkz. [Yönetim hizmeti önkoşulları](../develop/adminservice/overview.md#prerequisites).

### <a name="the-user-does-not-have-permissions"></a><a name="bkmk_user"></a> Kullanıcının izni yok

**Hata iletisi:** Envanter sınıfları verilerle alınamadı. Kullanıcının izni yok.

**Olası nedenler:** Kullanıcının cihazın parçası olduğu koleksiyona erişimi olmayabilir. Aşağıdaki öğeleri doğrulayın:

1. Yönetici merkezinde oturum açmak için aynı hesabı kullanın. Şirket içi kimliğin ile eşitlenmesi ve bulut kimliğiyle eşleşmesi gerekir.
1. Hesabın Configuration Manager, cihazın **koleksiyonu** için **okuma** iznine sahip olduğunu doğrulayın.
1. Configuration Manager, kullanmakta olduğunuz yönetim kullanıcı hesabını keşfettiği emin olun. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Kullanıcılar** düğümünü seçin ve kullanıcı hesabınızı bulun.

    Hesabınız **Kullanıcılar** düğümünde listelenmiyorsa, sitenin [Active Directory Kullanıcı bulmanın](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)yapılandırmasını denetleyin.

## <a name="known-issues"></a>Bilinen sorunlar

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Sonraki adımlar

[Kiracı eklemeyle ilgili sorunları giderme](troubleshoot.md)