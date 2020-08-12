---
title: Uygulama yüklemesinde sorun giderme
titleSuffix: Configuration Manager
description: Configuration Manager kiracı iliştirme için uygulama yüklemesinde sorun giderme
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 75f47456-cd8d-4c83-8dc5-98b336a7c6c8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 93b793dfbc6d7d0b5f4b24db65588ee1390604e9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129289"
---
# <a name="troubleshoot-application-installation-for-devices-uploaded-to-the-admin-center-preview"></a>Yönetim merkezine yüklenen cihazlar için uygulama yüklemesinde sorun giderme (Önizleme)
<!--6374854, 6521921-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Endpoint Manager Yönetim Merkezi 'nde Configuration Manager uygulamalarda sorun gidermek için aşağıdakileri kullanın:

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Microsoft Endpoint Manager Yönetim Merkezi 'ndeki yaygın hatalar

Microsoft Endpoint Manager Yönetim Merkezi 'nden uygulamaları görüntülerken veya yüklerken, bu hatalardan biri üzerinde çalıştırabilirsiniz.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a>Gerekli Yapılandırma Azure Active Directory eksik

**Hata iletisi:** Gerekli Yapılandırma Azure Active Directory eksik. Configuration Manager sitesini Azure kiracınıza iliştirdiğinizden ve uygun Kullanıcı rolünü Azure AD 'ye atadığınızdan emin olun.

**Olası neden:** Kullanıcı hesabının Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü eksik olabilir. Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir. Bu izne yapılan değişikliklerin etkili olması bir saate kadar sürebilir.

### <a name="unable-to-get-application-information"></a><a name="bkmk_noinfo"></a>Uygulama bilgileri alınamıyor

**Hata iletisi 1:** Uygulama bilgileri alınamıyor. Azure AD ve AD Kullanıcı bulmanın yapılandırıldığından ve kullanıcının her ikisiyle de bulunduğundan emin olun. Kullanıcının Configuration Manager uygun izinlere sahip olduğunu doğrulayın.

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

### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a>Beklenmeyen bir hata oluştu

**Hata iletisi:** Beklenmeyen bir hata oluştu

#### <a name="error-code-500-with-an-unexpected-error-occurred-message"></a>Hata kodu 500, beklenmeyen bir hata oluştu iletisi

1. `System.Security.SecurityException` **Adminservice. log**dosyasında görüyorsanız, [Active Directory Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) tarafından KEŞFEDILEN Kullanıcı asıl adınızın (UPN) Şirket ıçı UPN yerine bir bulut UPN olarak ayarlandığını doğrulayın. Boş bir UPN değeri de kabul edilebilir çünkü Active Directory bulunan etki alanı adının kullanıldığı anlamına gelir. Geçerli bir etki alanı UPN (contoso.com) olmayan yalnızca bulutta bulunan UPN (örnek: onmicrosoft.com) görürseniz, bir sorununuz vardır ve [ACTIVE DIRECTORY UPN sonekini ayarlamanız](https://docs.microsoft.com/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them)gerekebilir.
1. **Adminservice. log**dosyasında aşağıdaki hatayı görürseniz, [Microsoft Endpoint Manager Yönetim Merkezi 'Nde KB4576782-Application dikey penceresini zaman aşımına uğruyor](https://support.microsoft.com/help/4576782) :
   ```log 
   System.Data.Entity.Core.EntityCommandExecutionException: An error occurred while executing the command definition. See the inner exception for details.
   System.Data.SqlClient.SqlException: Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.
   System.ComponentModel.Win32Exception: The wait operation timed out
   ```

#### <a name="error-code-3-with-an-unexpected-error-occurred-message"></a>Beklenmeyen bir hata oluştu iletisi ile hata kodu 3

Yönetici hizmeti çalışmıyor veya IIS yüklü değil. IIS 'nin sağlayıcı makinesine yüklenmesi gerekir. Daha fazla bilgi için bkz. [Yönetim hizmeti önkoşulları](../develop/adminservice/overview.md#prerequisites).

#### <a name="other-possible-causes-of-unexpected-errors"></a>Beklenmeyen hataların diğer olası nedenleri

Beklenmeyen hatalara genellikle [hizmet bağlantı noktası](../core/servers/deploy/configure/about-the-service-connection-point.md), [Yönetim hizmeti](../develop/adminservice/overview.md)veya bağlantı sorunları neden olmuş olabilir.

1. Hizmet bağlantı noktasının **Cmgatewaynotificationworker. log**kullanarak buluta bağlantı olduğunu doğrulayın.
1. Merkezi sitedeki site bileşeni izlemenin SMS_REST_PROVIDER bileşenini inceleyerek yönetim hizmetinin sağlıklı olduğunu doğrulayın.
1. IIS 'nin sağlayıcı makinesine yüklenmesi gerekir. Daha fazla bilgi için bkz. [Yönetim hizmeti önkoşulları](../develop/adminservice/overview.md#prerequisites).


### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a>Site bilgileri henüz eşitlenmedi

**Hata iletisi:** Site bilgileri henüz Microsoft Endpoint Manager yönetim merkezine Configuration Manager ile eşitlenmemiş. Siteyi Azure kiracınıza iliştirdikten 15 dakikaya kadar bekleyin.

**Olası nedenler:**
- Bu hata genellikle kiracı iliştirme 'ye yeni ekleme gerçekleştirildiğinde oluşur. Bilgilerin eşitlenmesi 15 dakika bekleyin.
- Bu hata, merkezi yönetim sitesi yeni bir Configuration Manager sürümüne yükseltildiyse ancak bazı alt birincil siteler henüz yükseltilmemişse de görünebilir.

### <a name="application-shows-as-installed-after-creating-a-new-deployment"></a><a name="bkmk_installed"></a>Uygulama yeni bir dağıtım oluşturduktan sonra yüklendi olarak gösteriliyor

**Belirti:** Kullanılabilir yeni bir cihaz oluşturulduktan sonra bir uygulama, Microsoft Endpoint Manager Yönetim Merkezi 'nde yüklü olarak gösterilir.

**Olası neden:** Bu cihaz için gösterilen uygulama durumu, başka bir etkin veya geçmiş dağıtımından yapılır.

### <a name="errors-when-searching-or-retrying-an-installation"></a><a name="bkmk_hfru"></a>Bir yüklemeyi ararken veya yeniden denemeden oluşan hatalar

**Belirti:** Aşağıdaki eylemler gerçekleştirilirken hatalar oluşur:
- Aramayı Kullanma
- **Yüklemeyi yeniden dene 'yi** seçin

**Olası neden:**  [Microsoft uç noktası Configuration Manager sürüm 2002 Için güncelleştirme toplamasının](https://support.microsoft.com/help/4560496/) ve konsolun karşılık gelen sürümünün yüklü olduğundan emin olun. Daha fazla bilgi için bkz. [Yönetim merkezinden uygulama yükleme önkoşulları](applications.md#prerequisites).

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="application-installation-times-out-if-application-requires-restart"></a>Uygulama yeniden başlatma gerektiriyorsa uygulama yüklemesi zaman aşımına uğrar

**Senaryo:** Configuration Manager sürüm 2002 çalıştırıyorsanız ve uygulama yükleme işlemini tamamlaması için yeniden başlatma gerektiriyorsa, yükleme zaman aşımına uğrar.

**Belirtiler:** Kullanıcı `restart pending` bildirimleri ve yazılım merkezi 'nde görüntülenir. Microsoft Endpoint Manager yönetim merkezinden uygulama `Installing` durumunda kalır.  

**Geçici çözüm:** Kullanıcı cihazı yeniden başlattıktan sonra, yönetici merkezinde doğru durum görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar

[Kiracı eklemeyle ilgili sorunları giderme](troubleshoot.md)
