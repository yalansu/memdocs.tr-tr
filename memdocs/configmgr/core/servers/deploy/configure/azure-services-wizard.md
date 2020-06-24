---
title: Azure hizmetlerini yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager ortamınızı bulut yönetimi, Iş için Microsoft Store ve Log Analytics Azure hizmetleriyle bağlayın.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6ca5307de5c7df54c3cf7924bc91b0175b1bfa39
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715331"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Azure hizmetlerini Configuration Manager ile kullanım için yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ile kullandığınız Azure bulut hizmetlerini yapılandırma işlemini basitleştirmek için **Azure Hizmetleri Sihirbazı 'nı** kullanın. Bu sihirbaz Azure Active Directory (Azure AD) Web uygulaması kayıtlarını kullanarak ortak bir yapılandırma deneyimi sağlar. Bu uygulamalar, abonelik ve yapılandırma ayrıntılarını sağlar ve Azure AD ile iletişimin kimliğini doğrular. Uygulama, Azure ile yeni bir Configuration Manager bileşeni veya hizmeti her ayarlarken aynı bilgilerin girilmesini yerine koyar.

## <a name="available-services"></a>Kullanılabilir hizmetler

Bu Sihirbazı kullanarak aşağıdaki Azure hizmetlerini yapılandırın:  

- **Bulut yönetimi**: Bu hizmet, site ve ISTEMCILERIN Azure ad kullanarak kimlik doğrulaması yapmasına olanak sağlar. Bu kimlik doğrulaması, aşağıdaki gibi diğer senaryolara izin vermez:  

  - [Kimlik doğrulaması için Azure AD 'yi kullanarak Configuration Manager Windows 10 istemcileri yükleyip atama](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Azure AD Kullanıcı bulmayı yapılandırma](configure-discovery-methods.md#azureaadisc)  

  - [Azure AD Kullanıcı grubu bulmayı yapılandırma](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Belirli [bulut yönetimi ağ geçidi senaryolarını](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios) destekleme  

  - [Uygulama onayı e-postası bildirimleri](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics Bağlayıcısı**: [Azure Log Analytics 'a bağlanın](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Koleksiyon verilerini Log Analytics ile eşitleyin.  

    > [!Note]  
    > Bu makale, daha önce *OMS Bağlayıcısı*olarak adlandırılan *Log Analytics bağlayıcıya*başvurur. İşlevsel farklılık yoktur. Daha fazla bilgi için bkz. [Azure yönetim-izleme](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics).  

- **İş için Microsoft Store**: [iş için Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)bağlanın. Kuruluşunuz için Configuration Manager ile dağıtabileceğiniz mağaza uygulamalarını alın.  

### <a name="service-details"></a>Hizmet Ayrıntıları

Aşağıdaki tabloda her bir hizmetin ayrıntıları listelenmektedir.  

- **Kiracılar**: yapılandırabilmeniz için hizmet örneklerinin sayısı. Her örnek ayrı bir Azure AD kiracısı olmalıdır.  

- **Bulutlar**: tüm hizmetler küresel Azure bulutunu destekler, ancak tüm HIZMETLER Azure ABD kamu bulutu gibi özel bulutları desteklemez.  

- **Web uygulaması**: hizmetin *Web uygulaması/API*türünde bir Azure AD uygulaması kullanıp kullanmadığını da Configuration Manager ' de bir sunucu uygulaması olarak da bilinir.  

- **Yerel uygulama**: hizmetin, Configuration Manager ' de istemci uygulaması olarak da adlandırılan *Yerel*türdeki bir Azure AD uygulaması kullanıp kullanmadığını belirtir.  

- **Eylemler**: bu uygulamaları Configuration Manager Azure hizmetleri sihirbazında içeri veya dışarı aktarıp oluşturamayacağını belirtir.  

|Hizmet  |Kiracılar  |Bulutlar  |Web uygulaması  |Yerel uygulama  |Eylemler  |
|---------|---------|---------|---------|---------|---------|
|İle bulut yönetimi<br>Azure AD bulma | Birden çok | Ortak, özel | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | İçeri aktarma, oluşturma |
|Log Analytics Bağlayıcısı | Bir | Ortak, özel | ![Destekleniyor](media/green_check.png) | ![Desteklenmiyor](media/Red_X.png) | İçeri Aktar |
|İçin Microsoft Store<br>İş | Bir | Ortak | ![Destekleniyor](media/green_check.png) | ![Desteklenmiyor](media/Red_X.png) | İçeri aktarma, oluşturma |

### <a name="about-azure-ad-apps"></a>Azure AD uygulamaları hakkında

Farklı Azure Hizmetleri, Azure portal yaptığınız ayrı konfigürasyonlar gerektirir. Ayrıca, her bir hizmetin uygulamaları Azure kaynakları için ayrı izinler gerektirebilir.  

Birden fazla hizmet için tek bir uygulama kullanabilirsiniz. Configuration Manager ve Azure AD 'de yönetilecek yalnızca bir nesne vardır. Uygulamadaki güvenlik anahtarının süresi dolmuşsa yalnızca bir anahtarı yenilemeniz gerekir.

Sihirbazda ek Azure hizmetleri oluşturduğunuzda, hizmetler arasında ortak olan bilgileri yeniden kullanmak için Configuration Manager tasarlanmıştır. Bu davranış, aynı bilgileri birden çok kez girmenize gerek duymanıza yardımcı olur.

Her hizmet için gerekli uygulama izinleri ve yapılandırma hakkında daha fazla bilgi için, [kullanılabilir hizmetler](#available-services)' de ilgili Configuration Manager makalesine bakın.

Azure uygulamaları hakkında daha fazla bilgi için aşağıdaki makalelerle başlayın:

- [Azure App Service’de kimlik doğrulaması ve yetkilendirme](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Web Apps genel bakış](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [Azure AD 'de uygulama kaydetmenin temelleri](/azure/active-directory/develop/authentication-scenarios)  
- [Uygulamanızı Azure Active Directory kiracınızla kaydetme](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Başlamadan önce

Bağlanmak istediğiniz hizmete karar verdikten sonra, [Hizmet Ayrıntıları](#service-details)' nda tabloya bakın. Bu tablo, Azure hizmet Sihirbazı 'Nı tamamlaması için gereken bilgileri sağlar. Azure AD yöneticinizle birlikte önceden bir tartışma yapın. Aşağıdaki eylemlerden hangisini kullanacağınıza karar verin:

- Uygulamaları Azure portal önceden el ile oluşturun. Sonra uygulama ayrıntılarını Configuration Manager içine aktarın.  

- Azure AD 'de uygulamaları doğrudan oluşturmak için Configuration Manager kullanın. Azure AD 'den gerekli verileri toplamak için, bu makalenin diğer bölümlerindeki bilgileri gözden geçirin.  

Bazı hizmetler, Azure AD uygulamalarının belirli izinlere sahip olmasını gerektirir. Tüm gerekli izinleri öğrenmek için her hizmet için bilgileri gözden geçirin. Örneğin, bir Web uygulamasını içeri aktarabilmeniz için önce bir Azure Yöneticisi tarafından [Azure Portal](https://portal.azure.com)oluşturmanız gerekir.

Log Analytics bağlayıcısını yapılandırırken, ilgili çalışma alanını içeren kaynak grubunda yeni kayıtlı Web uygulamasına *katkıda* bulunan izin verin. Bu izin, Configuration Manager Bu çalışma alanına erişmesine izin verir. İzin atarken, Azure portal **Kullanıcı Ekle** alanında uygulama kaydı adını arayın. Bu işlem, [Log Analytics izinlerle Configuration Manager sağlamaya](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics)benzer. Uygulamayı Configuration Manager içeri aktarmadan önce bir Azure Yöneticisi bu izinleri atamalıdır.

## <a name="start-the-azure-services-wizard"></a>Azure Hizmetleri Sihirbazı 'nı başlatma

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Azure hizmetleri** grubunda **Azure hizmetlerini yapılandır**' ı seçin.  

3. Azure Hizmetleri Sihirbazı 'nın **Azure hizmetleri** sayfasında:  

    1. Configuration Manager nesne için bir **ad** belirtin.  

    2. Hizmeti tanımlamanızı sağlayacak isteğe bağlı bir **Açıklama** belirtin.  

    3. Configuration Manager bağlamak istediğiniz Azure hizmetini seçin.  

4. Azure hizmetleri sihirbazının [Azure uygulama özellikleri](#azure-app-properties) sayfasına devam etmek için **İleri ' yi** seçin.  

## <a name="azure-app-properties"></a>Azure uygulama özellikleri

Azure Hizmetleri Sihirbazı 'nın **uygulama** sayfasında, önce listeden **Azure ortamı** ' nı seçin. Hizmetin Şu anda hizmette kullanılabildiği [Hizmet Ayrıntıları](#service-details) ' nın tablosuna bakın.

Uygulama sayfasının geri kalanı, belirli bir hizmete bağlı olarak değişir. Hizmetin kullandığı uygulama türü ve kullanabileceğiniz eylem için [Hizmet Ayrıntıları](#service-details) ' nda tabloya bakın.

- Uygulama hem içeri aktarma hem de işlem eylemlerini destekliyorsa, **Araştır**' ı seçin. Bu eylem [sunucu uygulaması iletişim kutusunu](#server-app-dialog) veya [istemci uygulaması iletişim kutusunu](#client-app-dialog)açar.  

- Uygulama yalnızca içeri aktarma eylemini destekliyorsa, **Içeri aktar**' ı seçin. Bu eylem, [uygulamaları Içeri Aktar iletişim kutusunu (sunucu)](#import-apps-dialog-server) veya [Uygulamaları İçeri Aktar iletişim kutusunu (istemci)](#import-apps-dialog-client)açar.

Bu sayfadaki uygulamaları belirttikten sonra, Azure hizmetleri sihirbazının [yapılandırma veya bulma](#configuration-or-discovery) sayfasına devam etmek için **İleri** ' yi seçin.

### <a name="web-app"></a>Web uygulaması

Bu uygulama, Configuration Manager bir sunucu uygulaması olarak da adlandırılan Azure AD türü *Web uygulaması/API*'sidir.

#### <a name="server-app-dialog"></a>Sunucu uygulaması iletişim kutusu

Azure Hizmetleri Sihirbazı 'nın uygulama sayfasında **Web uygulamasına** **Araştır** ' ı seçtiğinizde, sunucu uygulaması iletişim kutusunu açar. Mevcut Web uygulamalarının aşağıdaki özelliklerini gösteren bir liste görüntüler:

- Kiracı kolay adı
- Uygulama kolay adı
- Hizmet Türü

Sunucu uygulaması iletişim kutusundan kullanabileceğiniz üç eylem vardır:

- Var olan bir Web uygulamasını yeniden kullanmak için listeden seçin.
- **İçeri** Aktar ' ı seçerek [Uygulamaları İçeri Aktar iletişim kutusunu](#import-apps-dialog-server)açın.
- [Sunucu uygulaması oluştur iletişim kutusunu](#create-server-application-dialog)açmak için **Oluştur** ' u seçin.

Bir Web uygulaması seçtikten, aldıktan veya oluşturduktan sonra, sunucu uygulaması iletişim kutusunu kapatmak için **Tamam** ' ı seçin. Bu eylem, Azure hizmetleri sihirbazının [uygulama sayfasına](#azure-app-properties) döner.

#### <a name="import-apps-dialog-server"></a>Uygulamaları İçeri Aktar iletişim kutusu (sunucu)

Sunucu uygulaması iletişim kutusundan veya Azure hizmetleri sihirbazının uygulama sayfasında **Içeri aktar** ' ı seçtiğinizde, uygulamaları içeri aktar iletişim kutusunu açar. Bu sayfa, Azure portal zaten oluşturulmuş bir Azure AD Web uygulaması hakkında bilgi girmenize olanak sağlar. Bu Web uygulaması hakkındaki meta verileri Configuration Manager içine aktarır. Aşağıdaki bilgileri belirtin:

- **Azure AD kiracı adı**: Azure AD kiracınızın adı.
- **Azure AD KIRACı kimliği**: Azure AD KIRACıNıZıN GUID 'si.
- **Uygulama adı**: uygulamanın kolay adı, uygulama kaydında görünen ad.
- **ISTEMCI kimliği**: uygulama kaydının **uygulama (istemci) kimliği** değeri. Biçim standart bir GUID 'dir.
- **Gizli anahtar**: uygulamayı Azure AD 'ye kaydettiğinizde gizli anahtarı kopyalamanız gerekir.
- **Gizli anahtar süre sonu**: takvimden gelecek bir tarih seçin.
- **Uygulama kimliği URI 'si**: Bu DEĞERIN Azure AD kiracınızda benzersiz olması gerekir. Hizmete erişim istemek için Configuration Manager istemcisi tarafından kullanılan erişim simgesindeki. Değer, Azure AD portalındaki uygulama kayıt girişinin **uygulama kimliği URI 'sidir** . Biçimi ile benzerdir `https://ConfigMgrService` .

Bilgileri girdikten sonra **Doğrula**' yı seçin. Ardından **Tamam** ' ı seçerek Uygulamaları İçeri Aktar iletişim kutusunu kapatın. Bu eylem, Azure hizmetleri sihirbazının [uygulama sayfasına](#azure-app-properties) veya [sunucu uygulaması iletişim kutusuna](#server-app-dialog)geri döner.

> [!TIP]
> Uygulamayı Azure AD 'ye kaydettiğinizde, aşağıdaki **yeniden YÖNLENDIRME URI**'sini el ile belirtmeniz gerekebilir: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>` . Uygulamanın istemci KIMLIĞI GUID 'sini belirtin, örneğin: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49` .<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Sunucu uygulaması oluştur iletişim kutusu

Sunucu uygulaması iletişim kutusunda **Oluştur** ' u seçtiğinizde sunucu uygulaması oluştur iletişim kutusunu açar. Bu sayfa, Azure AD 'de bir Web uygulaması oluşturulmasını otomatikleştirir. Aşağıdaki bilgileri belirtin:

- **Uygulama adı**: uygulama için kolay bir ad.
- **Giriş sayfası URL 'si**: bu değer Configuration Manager tarafından kullanılmaz, ancak Azure AD tarafından gerekli değildir. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.  
- **Uygulama kimliği URI 'si**: Bu DEĞERIN Azure AD kiracınızda benzersiz olması gerekir. Hizmete erişim istemek için Configuration Manager istemcisi tarafından kullanılan erişim simgesindeki. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.  
- **Gizli anahtar geçerlilik süresi**: açılan listeden **1 yıl** veya **2 yıl** seçeneklerinden birini belirleyin. Bir yıl, varsayılan değerdir.

Azure 'da yönetici kullanıcı olarak kimlik doğrulaması gerçekleştirmek için **oturum aç '** ı seçin. Bu kimlik bilgileri Configuration Manager tarafından kaydedilmez. Bu kişi Configuration Manager izinleri gerektirmez ve Azure Hizmetleri Sihirbazı 'Nı çalıştıran aynı hesapla aynı olmalıdır. Azure 'da başarıyla kimlik doğrulamasından geçtikten sonra, sayfada başvuru için **Azure AD kiracı adı** gösterilir.

Azure AD 'de Web uygulaması oluşturmak için **Tamam** ' ı seçin ve sunucu uygulaması oluştur iletişim kutusunu kapatın. Bu eylem [sunucu uygulaması iletişim kutusuna](#server-app-dialog)geri döner.

> [!NOTE]
> Tanımlanmış bir Azure AD koşullu erişim ilkeniz varsa ve **tüm bulut uygulamalarına** geçerliyse, oluşturulan sunucu uygulamasını bu ilkeden hariç bırakmanız gerekir. Belirli uygulamaları dışarıda bırakma hakkında daha fazla bilgi için bkz. [Azure AD koşullu erişim belgeleri](https://docs.microsoft.com/azure/active-directory/conditional-access/).

### <a name="native-client-app"></a>Yerel Istemci uygulaması

Bu uygulama, Configuration Manager ' de istemci uygulaması olarak da adlandırılan Azure AD türü *yereldir*.

#### <a name="client-app-dialog"></a>İstemci uygulaması iletişim kutusu

Azure hizmetleri sihirbazının uygulama sayfasında **yerel istemci uygulaması** için **Araştır** ' ı seçtiğinizde, istemci uygulaması iletişim kutusunu açar. Mevcut yerel uygulamaların aşağıdaki özelliklerini gösteren bir liste görüntüler:

- Kiracı kolay adı
- Uygulama kolay adı
- Hizmet Türü

Istemci uygulaması iletişim kutusundan kullanabileceğiniz üç eylem vardır:

- Mevcut bir yerel uygulamayı yeniden kullanmak için listeden seçin. 
- **İçeri** Aktar ' ı seçerek [Uygulamaları İçeri Aktar iletişim kutusunu](#import-apps-dialog-client)açın.
- **Oluştur** ' u seçerek [istemci uygulaması oluştur iletişim kutusunu](#create-client-application-dialog)açın.

Yerel bir uygulamayı seçip içeri aktardıktan veya oluşturduktan sonra, Istemci uygulaması iletişim kutusunu kapatmak için **Tamam** ' ı seçin. Bu eylem, Azure hizmetleri sihirbazının [uygulama sayfasına](#azure-app-properties) döner.

#### <a name="import-apps-dialog-client"></a>Uygulamaları İçeri Aktar iletişim kutusu (istemci)

Istemci uygulaması iletişim kutusundan **Içeri aktar** ' ı seçtiğinizde, uygulamaları içeri aktar iletişim kutusunu açar. Bu sayfa, Azure portal zaten oluşturulmuş bir Azure AD yerel uygulaması hakkında bilgi girmenize olanak sağlar. Bu yerel uygulamayla ilgili meta verileri Configuration Manager içine aktarır. Aşağıdaki bilgileri belirtin:

- **Uygulama adı**: uygulama için kolay bir ad.
- **ISTEMCI kimliği**: uygulama kaydının **uygulama (istemci) kimliği** değeri. Biçim standart bir GUID 'dir.

Bilgileri girdikten sonra **Doğrula**' yı seçin. Ardından **Tamam** ' ı seçerek Uygulamaları İçeri Aktar iletişim kutusunu kapatın. Bu eylem, [Istemci uygulaması iletişim kutusuna](#client-app-dialog)geri döner.

#### <a name="create-client-application-dialog"></a>Istemci uygulaması oluştur iletişim kutusu

Istemci uygulaması iletişim kutusundan **Oluştur** ' u seçtiğinizde, Istemci uygulaması oluştur iletişim kutusunu açar. Bu sayfa, Azure AD 'de yerel bir uygulamanın oluşturulmasını otomatikleştirir. Aşağıdaki bilgileri belirtin:

- **Uygulama adı**: uygulama için kolay bir ad.
- **Yanıt URL 'si**: bu değer Configuration Manager tarafından kullanılmaz, ancak Azure AD tarafından gerekli değildir. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.

Azure 'da yönetici kullanıcı olarak kimlik doğrulaması gerçekleştirmek için **oturum aç '** ı seçin. Bu kimlik bilgileri Configuration Manager tarafından kaydedilmez. Bu kişi Configuration Manager izinleri gerektirmez ve Azure Hizmetleri Sihirbazı 'Nı çalıştıran aynı hesapla aynı olmalıdır. Azure 'da başarıyla kimlik doğrulamasından geçtikten sonra, sayfada başvuru için **Azure AD kiracı adı** gösterilir.

Azure AD 'de yerel uygulamayı oluşturmak için **Tamam** ' ı seçin ve Istemci uygulaması oluştur iletişim kutusunu kapatın. Bu eylem, [Istemci uygulaması iletişim kutusuna](#client-app-dialog)geri döner.

## <a name="configuration-or-discovery"></a>Yapılandırma veya bulma

Uygulamalar sayfasında Web ve yerel uygulamaları belirttikten sonra, bağlandığınız hizmete bağlı olarak Azure Hizmetleri Sihirbazı bir **yapılandırma** ya da **keşif** sayfasına ilerler. Bu sayfanın ayrıntıları hizmetten hizmete değişir. Daha fazla bilgi için aşağıdaki makalelerden birine bakın:  

- **Bulut yönetimi** hizmeti, **bulma** sayfası: [Azure AD Kullanıcı bulmayı yapılandırma](configure-discovery-methods.md#azureaadisc)  

- **Log Analytics Bağlayıcısı** hizmeti, **yapılandırma** sayfası: [bağlantıyı Log Analytics yapılandırma](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- **İş hizmetleri için Microsoft Store** yapılandırma **sayfası:** [iş için Microsoft Store yapılandırma](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Son olarak, Azure Hizmetleri Sihirbazı ' nı Özet, Ilerleme ve tamamlama sayfalarından tamamlayabilirsiniz. Configuration Manager ' de bir Azure hizmeti yapılandırmasını tamamladınız. Diğer Azure hizmetlerini yapılandırmak için bu işlemi tekrarlayın.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a>Gizli anahtarı Yenile

### <a name="renew-key-for-created-app"></a>Oluşturulan uygulama için anahtarı Yenile

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure Active Directory kiracılar** düğümünü seçin.

1. Ayrıntılar bölmesinde, uygulamanın Azure AD kiracısı ' ni seçin.

1. Şeritte **gizli anahtarı Yenile**' yi seçin. Uygulama sahibinin ya da bir Azure AD yöneticisinin kimlik bilgilerini girin.

### <a name="renew-key-for-imported-app"></a>İçeri aktarılan uygulama için anahtarı Yenile

Azure uygulamasını Configuration Manager içeri aktardıysanız yenilemek için Azure portal kullanın. Yeni gizli anahtar ve sona erme tarihini dikkate alın. Bu bilgileri **gizli anahtarı Yenile** sihirbazına ekleyin.  

> [!NOTE]
> Azure uygulama özellikleri **anahtar** sayfasını kapatmadan önce gizli anahtarı kaydedin. Sayfayı kapattığınızda bu bilgiler kaldırılır.

## <a name="view-the-configuration-of-an-azure-service"></a>Azure hizmetinin yapılandırmasını görüntüleme

Kullanım için yapılandırdığınız bir Azure hizmetinin özelliklerini görüntüleyin. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri**' ni seçin. Görüntülemek veya düzenlemek istediğiniz hizmeti seçin ve ardından **Özellikler**' i seçin.

Bir hizmet seçip Şeritteki **Sil** ' i seçerseniz, bu eylem Configuration Manager bağlantıyı siler. Azure AD 'de uygulamayı kaldırmaz. Azure yöneticinizden uygulamayı artık gerekli olmadığında silmesini isteyin. Ya da uygulamayı içeri aktarmak için Azure hizmet Sihirbazı 'Nı çalıştırın.<!--483440-->

## <a name="cloud-management-data-flow"></a>Bulut yönetimi veri akışı

Aşağıdaki diyagramda Configuration Manager, Azure AD ve bağlı bulut hizmetleri arasındaki etkileşime yönelik kavramsal bir veri akışı bulunur. Bu belirli örnek, bir Windows 10 istemcisi ve hem sunucu hem de istemci uygulamaları içeren **bulut yönetimi** hizmetini kullanır. Diğer hizmetlerin akışları benzerdir.

![Azure AD ve bulut yönetimiyle Configuration Manager yönelik veri akışı diyagramı](media/aad-auth.png)

1. Configuration Manager yöneticisi, Azure AD 'de istemci ve sunucu uygulamalarını içeri aktarır veya oluşturur.  

2. Configuration Manager Azure AD Kullanıcı keşfi yöntemi çalışır. Site, Kullanıcı nesneleri için Microsoft Graph sorgulamak için Azure AD Server uygulama belirtecini kullanır.  

3. Site, Kullanıcı nesneleri hakkındaki verileri depolar. Daha fazla bilgi için bkz. [Azure AD Kullanıcı keşfi](about-discovery-methods.md#azureaddisc).  

4. Configuration Manager istemcisi, Azure AD kullanıcı belirtecini ister. İstemci, Azure AD istemci uygulamasının uygulama KIMLIĞINI ve hedef kitle olarak sunucu uygulamasını kullanarak talebi yapar. Daha fazla bilgi için bkz. [Azure AD güvenlik belirteçlerinde talepler](/azure/active-directory/develop/authentication-scenarios#security-tokens).  

5. İstemci, Azure AD belirtecini bulut yönetimi ağ geçidine ve şirket içi HTTPS özellikli yönetim noktasına sunarak sitesiyle kimliğini doğrular.  

Daha ayrıntılı bilgi için bkz. [Azure AD kimlik doğrulaması iş akışı](../../../clients/manage/azure-ccmsetup.md).
