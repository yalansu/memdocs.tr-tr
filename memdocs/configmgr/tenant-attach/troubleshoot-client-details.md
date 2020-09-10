---
title: İstemci ayrıntıları sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager kiracı iliştirme için istemci ayrıntıları sorunlarını giderme
ms.date: 07/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 2555d933d3ed19c83de02dca1c672031343836fa
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643511"
---
# <a name="troubleshoot-configmgr-client-details-in-the-admin-center-preview"></a>Yönetim merkezinde ConfigMgr istemci ayrıntıları sorunlarını giderme (Önizleme)
<!--6374854, 6521921-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Endpoint Manager Yönetim Merkezi 'nde ConfigMgr istemci ayrıntılarına sorun gidermek için aşağıdakileri kullanın:

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Microsoft Endpoint Manager Yönetim Merkezi 'ndeki yaygın hatalar

ConfigMgr istemci ayrıntılarını görüntülerken, bu hatalardan biri üzerinde çalıştırabilirsiniz.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> Gerekli Yapılandırma Azure Active Directory eksik

**Hata iletisi:** Gerekli Yapılandırma Azure Active Directory eksik. Configuration Manager sitesini Azure kiracınıza iliştirdiğinizden ve uygun Kullanıcı rolünü Azure AD 'ye atadığınızdan emin olun.

**Olası neden:** Kullanıcı hesabının Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü eksik olabilir. Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir. Bu izne yapılan değişikliklerin etkili olması bir saate kadar sürebilir.

### <a name="unable-to-get-device-or-collection-information"></a><a name="bkmk_noinfo"></a> Cihaz veya koleksiyon bilgisi alınamıyor

**Hata iletisi 1:** İstemci ayrıntıları (veya koleksiyon) bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

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


### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a> Beklenmeyen bir hata oluştu

**Hata iletisi:** Beklenmeyen bir hata oluştu

**Olası nedenler:** Beklenmeyen hatalara genellikle [hizmet bağlantı noktası](../core/servers/deploy/configure/about-the-service-connection-point.md), [Yönetim hizmeti](../develop/adminservice/overview.md)veya bağlantı sorunları neden olmuş olabilir.

1. Hizmet bağlantı noktasının **Cmgatewaynotificationworker. log**kullanarak buluta bağlantı olduğunu doğrulayın.
1. Merkezi sitedeki site bileşeni izlemenin SMS_REST_PROVIDER bileşenini inceleyerek yönetim hizmetinin sağlıklı olduğunu doğrulayın.
1. IIS 'nin sağlayıcı makinesine yüklenmesi gerekir. Daha fazla bilgi için bkz. [Yönetim hizmeti önkoşulları](../develop/adminservice/overview.md#prerequisites).
1. Hizmet bağlantı noktasındaki saatin eşitlenmiş olduğunu doğrulayın. Hizmet bağlantı noktasının saati biraz geride olursa, [Configuration Manager sürüm 2002 kiracı iliştirme sorunları Için KB4563473-Update paketini](https://support.microsoft.com/help/4563473)uygulayın. Hatalar için sağlayıcı makinesinde **Adminservice. log dosyasına** bakın.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="gettingresultstimedout"></a>Sonuçların alınması zaman aşımına uğradı

**Senaryo:** Bir uzak hizmet bağlantı noktanız varsa ve 30 Mart 2020 tarihinden önce 2002 erken güncelleştirme halkası yüklediyseniz, Yönetim merkezinde bir zaman aşımı hatası görürsünüz.

**Hata iletisi:** Sonuçların alınması zaman aşımına uğradı. Configuration Manager hizmet bağlantı noktasının çalışır durumda olduğundan ve buluta bir bağlantı bulunduğundan emin olun.

**Geçici çözüm:** `Microsoft.ConfigurationManagement.ManagementProvider.dll` Site sunucusunun `bin\x64` klasöründen uzak hizmet bağlantı noktasının `bin\x64` klasörüne kopyalayın.  Hizmeti, `SMS_EXECUTIVE` hizmet bağlantı noktası sunucusunda yeniden başlatın.

### <a name="boundary-groups-list-is-empty"></a>Sınır grupları listesi boş

**Hata iletisi**: sınır grubu bulunamadı veya kullanıcının sınır grubu bilgilerini görüntüleme izni olmayabilir.

Boş liste, Configuration Manager siteleri hiyerarşiniz olduğunda Configuration Manager sürüm 2002 için bilinen bir sorundur.

:::image type="content" source="media/6024387-known-issue-device-details.png" alt-text="Sınır grubu listesi boş" lightbox="media/6024387-known-issue-device-details.png":::

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Sonraki adımlar

[Kiracı eklemeyle ilgili sorunları giderme](troubleshoot.md)
