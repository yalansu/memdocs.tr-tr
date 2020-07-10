---
title: Microsoft Endpoint Manager kiracısı ekleme
titleSuffix: Configuration Manager
description: Configuration Manager cihazlarınızı bulut hizmetine yükleyin ve yönetim merkezinden işlem yapın.
ms.date: 07/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a9e97c74e4825dc49ce628b3ae176c55f4288966
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210292"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri
<!--3555758 live 3/4/2020-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir.

Configuration Manager sürüm 2002 ' den başlayarak, Configuration Manager cihazlarınızı bulut hizmetine yükleyebilir ve yönetim merkezindeki **cihazlar** dikey penceresinden eylemler gerçekleştirebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- Bu değişiklik uygulanırken oturum açmak için *genel yönetici* olan bir hesap. Daha fazla bilgi için bkz. [Azure Active Directory (Azure AD) yönetici rolleri](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Ekleme, Azure AD kiracınızda üçüncü taraf bir uygulama ve birinci taraf hizmet sorumlusu oluşturur.
- Azure genel bulut ortamı.
- Cihaz eylemlerini tetikleyen Kullanıcı hesapları aşağıdaki önkoşullara sahiptir:
   - [Azure Active Directory Kullanıcı bulma](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) ve [Active Directory Kullanıcı keşfi](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)ile birlikte keşfedilmiştir.
      - Bu, Kullanıcı hesabının Azure AD 'de eşitlenmiş bir kullanıcı nesnesi olması gerektiği anlamına gelir.
   - Microsoft Endpoint Manager Yönetim merkezinde **uzak görevler** altında **Configuration Manager eylemi Başlat** izni.


## <a name="internet-endpoints"></a>Internet uç noktaları

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>Cihaz yüklemeyi etkinleştir

- Şu anda ortak yönetim 'i etkinleştirdiyseniz, cihaz yüklemeyi etkinleştirmek için [ortak yönetim özelliklerini düzenleyin](#bkmk_edit) .
- Ortak yönetim özelliği etkinleştirilmemişse, cihaz yüklemeyi etkinleştirmek için [ **ortak yönetim yapılandırma** Sihirbazı 'nı kullanın](#bkmk_config) .
   - Ortak yönetim için otomatik kayıt veya Intune 'a geçiş iş yüklerini etkinleştirmek zorunda kalmadan cihazlarınızı karşıya yükleyebilirsiniz.
- **İstemci** sütununda **Evet** olan Configuration Manager tarafından yönetilen tüm cihazlar karşıya yüklenir. Gerekirse, karşıya yüklemeyi tek bir cihaz koleksiyonuna sınırlayabilirsiniz.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Cihaz yüklemeyi etkinleştirmek için ortak yönetim özelliklerini düzenleyin

Ortak yönetim Şu anda etkinleştirilmişse, aşağıdaki yönergeleri kullanarak cihaz karşıya yüklemeyi etkinleştirmek için ortak yönetim özelliklerini düzenleyin:

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
1. Ortak yönetim ayarlarınıza sağ tıklayıp **Özellikler**' i seçin.
1. **Karşıya yüklemeyi Yapılandır** sekmesinde, **Microsoft Endpoint Manager yönetim merkezine yükle**' yi seçin. **Uygula**'ya tıklayın.
   - Cihaz yükleme için varsayılan ayar, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm cihazlardır**. Gerekirse, karşıya yüklemeyi tek bir cihaz koleksiyonuna sınırlayabilirsiniz.
1. [Endpoint](../../analytics/overview.md)Analytics 'te Son Kullanıcı deneyimini Iyileştirmek Istiyorsanız **Microsoft Endpoint Manager 'A yüklenen cihazlarda Endpoint Analytics 'i etkinleştirme** seçeneğini işaretleyin.

   [![Cihazları Microsoft Endpoint Manager yönetim merkezine yükleme](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. İstendiğinde *genel yönetici* hesabınızla oturum açın.
1. **AAD uygulaması oluştur** bildirimini kabul etmek için **Evet** ' e tıklayın. Bu eylem, bir hizmet sorumlusu sağlar ve eşitlemeyi kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.
1. Değişiklik yapmayı tamamladıktan sonra ortak yönetim özelliklerinden çıkmak için **Tamam** ' ı tıklatın.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Cihaz yüklemeyi etkinleştirmek için ortak yönetim Yapılandırma Sihirbazı 'nı kullanın
Ortak yönetim özelliği etkinleştirilmemişse, cihaz yüklemeyi etkinleştirmek için **ortak yönetim yapılandırma** Sihirbazı 'nı kullanın. Ortak yönetim için otomatik kayıt veya Intune 'a geçiş iş yüklerini etkinleştirmek zorunda kalmadan cihazlarınızı karşıya yükleyebilirsiniz. Aşağıdaki yönergeleri kullanarak cihaz karşıya yüklemeyi etkinleştirin:

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
1. Şeritte, Sihirbazı açmak için **ortak yönetimi yapılandırma** ' ya tıklayın.
1. **Kiracı ekleme** sayfasında, ortamınız için **AzurePublicCloud** ' yi seçin. Azure Kamu Bulutu desteklenmez.
1. **Oturum aç**' a tıklayın. Oturum açmak için *genel yönetici* hesabınızı kullanın.
1. **Kiracı ekleme** sayfasında **Microsoft Endpoint Manager Yönetim Merkezi 'ne yükle** seçeneğinin seçili olduğundan emin olun.
   - Ortak yönetimi şimdi etkinleştirmek istemiyorsanız **ortak yönetim için otomatik istemci kaydını etkinleştir** seçeneğinin işaretli olmadığından emin olun. Ortak yönetimi etkinleştirmek istiyorsanız, seçeneğini belirleyin.
   - Ortak yönetimi cihaz karşıya yükleme ile birlikte etkinleştirirseniz, sihirbazın tamamlaması için ek sayfalar vermiş olursunuz. Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](../comanage/how-to-enable.md).

   [![Ortak yönetim Yapılandırma Sihirbazı](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. **AAD uygulaması oluştur** bildirimini kabul etmek için **İleri** ' ye ve ardından **Evet** ' e tıklayın. Bu eylem, bir hizmet sorumlusu sağlar ve eşitlemeyi kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.
1. **Karşıya yüklemeyi Yapılandır** sayfasında, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm Cihazlarım**için önerilen cihaz karşıya yükleme ayarını seçin. Gerekirse, karşıya yüklemeyi tek bir cihaz koleksiyonuna sınırlayabilirsiniz.
1. [Endpoint](../../analytics/overview.md) Analytics 'te Son Kullanıcı deneyimini Iyileştirmek Istiyorsanız **Microsoft Endpoint Manager 'a yüklenen cihazlar için Endpoint Analytics 'i etkinleştirme** seçeneğini işaretleyin
1. Seçiminizi gözden geçirmek için **Özet** ' e tıklayın ve ardından **İleri**' ye tıklayın.
1. Sihirbaz tamamlandığında **Kapat**' a tıklayın.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Karşıya yüklemeyi gözden geçirin

1. ConfigMgr yükleme dizininden **Cmgatewaysyncuploadworker. log** &lt; dosyasını açın> \logs.
1. Sonraki eşitleme zamanı, şuna benzer günlük girdileri tarafından belirtilir `Next run time will be at approximately: 02/28/2020 16:35:31` .
1. Cihaz yüklemeleri için şuna benzer günlük girdilerine bakın `Batching N records` . **N** , buluta yüklenen cihazların sayısıdır. 
1. Karşıya yükleme, değişiklikler için 15 dakikada bir gerçekleşir. Değişiklikler karşıya yüklendikten sonra, istemci değişikliklerinin **Microsoft Endpoint Manager Yönetim merkezinde**görünmesi 5 ila 10 dakika sürebilir.

## <a name="perform-device-actions"></a>Cihaz eylemlerini gerçekleştirme

1. Bir tarayıcıda şuraya gidin`endpoint.microsoft.com`
1. Yüklenen cihazları görmek için **cihazlar** ' ı ve ardından **tüm cihazlar** ' ı seçin. **ConfigMgr** 'yi karşıya yüklenen cihazlar Için **tarafından yönetilen** sütununda görürsünüz.
   [![Microsoft Endpoint Manager Yönetim Merkezi 'ndeki tüm cihazlar](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. **Genel bakış** sayfasını yüklemek için bir cihaza tıklayın.
1. Aşağıdaki eylemlerden birine tıklayın:
   - **Makine Ilkesini Eşitle**
   - **Kullanıcı Ilkesini eşitleme**
   - **Uygulama değerlendirme çevrimi**

   [![Microsoft Endpoint Manager Yönetim Merkezi 'nde cihaza genel bakış](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="specific-devices-dont-synchronize"></a>Belirli cihazlar eşitlenmez

<!--7099564-->
Configuration Manager istemci olan belirli cihazların hizmete yüklenmeyeceği olasıdır.

**Etkilenen cihazlar:** Bir cihaz hem dağıtım noktası işlevselliği hem de onun istemci Aracısı için aynı PKI sertifikasını kullanan bir dağıtım noktasıdır, bu durumda cihaz kiracı iliştirme cihaz eşitlemesine dahil değildir.

**Davranış:** Oluşturma aşamasında kiracı ekleme gerçekleştirirken, ilk kez tam eşitleme gerçekleştirilir. Sonraki eşitleme döngüleri, Delta eşitlelerdir. Etkilenen cihazlara yapılan herhangi bir güncelleştirme, cihazın eşitlemeden kaldırılmasına neden olur.

## <a name="log-files"></a>Günlük dosyaları
Hizmet bağlantı noktasında bulunan aşağıdaki günlükleri kullanın:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

## <a name="next-steps"></a>Sonraki adımlar

Kiracı iliştirme günlük dosyaları hakkında daha fazla bilgi için bkz. [kiracı Iliştirme sorunlarını giderme](troubleshoot.md).
