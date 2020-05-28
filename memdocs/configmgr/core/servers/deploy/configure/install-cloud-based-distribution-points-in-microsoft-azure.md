---
title: Bulut dağıtım noktalarını yükler
titleSuffix: Configuration Manager
description: Configuration Manager bir bulut dağıtım noktası ayarlamak için bu adımları kullanın.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35379aed71544a25a98ec4dfa421be70c1bae851
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427699"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Configuration Manager için bulut dağıtım noktası yükler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Azure 'dan içerik paylaşmaya yönelik uygulama değişti. **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verme ve Azure depolama 'dan içerik**sunma seçeneğini etkinleştirerek, içerik özellikli bir bulut yönetimi ağ geçidi kullanın. Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Gelecekte geleneksel bir bulut dağıtım noktası oluşturamayacak. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

Bu makalede Microsoft Azure bir Configuration Manager bulut dağıtım noktası yüklemek için gereken adımlar ayrıntılı olarak açıklanır. Aşağıdaki bölümleri içerir:

- [Başlamadan önce](#bkmk_before)
- [Kurulum](#bkmk_setup)
- [DNS yapılandırma](#bkmk_dns)
- [Site sunucusu ara sunucusunu ayarlama](#bkmk_proxy)
- [İçerik dağıtma ve istemcileri yapılandırma](#bkmk_client)
- [Yönetme ve izleme](#bkmk_monitor)
- [Değiştir](#bkmk_modify)
- [Gelişmiş sorun giderme](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a>Başlamadan önce

Başlayın [bir bulut dağıtım noktası kullanın](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)makalesini okuyun. Bu makale, bulut dağıtım noktalarınızı planlayıp tasarlamanıza yardımcı olur.

Bulut dağıtım noktası oluşturmak için gerekli bilgilere ve önkoşullara sahip olduğunuzdan emin olmak için aşağıdaki denetim listesini kullanın:  

- Site sunucusu Azure 'a bağlanabilir. Ağınız bir proxy kullanıyorsa, [site sistemi rolünü yapılandırın](#bkmk_proxy).  

- Kullanılacak **Azure ortamı** . Örneğin, Azure genel bulutu veya Azure ABD kamu bulutu.  

- Sürüm 1806 ' den başlayarak ve *önerilen* **Azure Resource Manager dağıtımı**' nı kullanın. Aşağıdaki gereksinimler yerine getirilmelidir:<!--1322209-->  

    - **Bulut yönetimi**için [Azure Active Directory](azure-services-wizard.md) ile tümleştirme. Azure AD Kullanıcı keşfi gerekli değildir.  

    - Azure **ABONELIK kimliği**.  

    - Azure **kaynak grubu**.  

    - Sihirbaz sırasında bir **Abonelik Yöneticisi hesabının** oturum açması gerekir.  

- Bir **sunucu kimlik doğrulama sertifikası**, bir olarak olarak verildi. PFX dosyası.  

- Bulut dağıtım noktası için genel olarak benzersiz bir **hizmet adı** .  

    > [!TIP]  
    > Bu hizmet adını kullanan sunucu kimlik doğrulama sertifikasını istenmeden önce, istenen Azure etki alanı adının benzersiz olduğunu doğrulayın. Örneğin, *WallaceFalls.cloudapp.net*.
    >
    > 1. [Azure portalında](https://portal.azure.com) oturum açın.
    > 1. **Tüm kaynaklar**' ı ve ardından **Ekle**' yi seçin.
    > 1. **Bulut hizmeti**araması yapın. **Oluştur**’u seçin.
    > 1. **DNS adı** alanına istediğiniz öneki yazın, örneğin *Wallacedüşerse*. Arabirim, etki alanı adının kullanılabilir olduğunu veya başka bir hizmet tarafından zaten kullanımda olduğunu yansıtır.
    >
    > Hizmeti portalda oluşturma bu işlemi, adın kullanılabilirliğini denetlemek için kullanmanız yeterlidir.

- Bu dağıtım için Azure **bölgesi** .  

- Hala Configuration Manager sürüm 1810 veya önceki sürümlerde **Klasik Azure hizmet dağıtımını** kullanmanız gerekiyorsa, aşağıdaki gereksinimlere ihtiyacınız vardır:  

    > [!Important]  
    > Sürüm 1810 ' den başlayarak, Azure 'da klasik hizmet dağıtımları Configuration Manager kullanım dışıdır. Bulut dağıtım noktası için Azure Resource Manager dağıtımlarını kullanmaya başlayın. Daha fazla bilgi için bkz. [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > Configuration Manager sürüm 1902 ' den başlayarak, Azure Resource Manager bulut dağıtım noktasının yeni örnekleri için tek dağıtım mekanizmasıdır.<!-- 3605704 -->

    - Azure **ABONELIK kimliği**.  

    - Bir Azure **Yönetim sertifikası**, her ikisi de olarak verildi. CER ve. PFX dosyaları. Bir Azure aboneliği yöneticisinin eklemesi gerekir. [Azure Portal](https://portal.azure.com)ABONELIK için cer yönetim sertifikası.  

### <a name="branchcache"></a>BranchCache

Bir bulut dağıtım noktasını Windows BranchCache kullanmak üzere etkinleştirmek için, site sunucusuna BranchCache özelliğini yükler.<!-- SCCMDocs-pr#4054 -->

- Site sunucusunda bir şirket içi dağıtım noktası site sistemi rolü varsa, **BranchCache 'ı etkinleştirmek ve yapılandırmak**için bu rolün özelliklerinde seçeneğini yapılandırın. Daha fazla bilgi için bkz. [dağıtım noktası yapılandırma](install-and-configure-distribution-points.md#bkmk_config-general).

- Site sunucusunun bir dağıtım noktası rolü yoksa, Windows 'da BranchCache özelliğini yükler. Daha fazla bilgi için bkz. [BranchCache özelliğini yükler](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Zaten bir bulut dağıtım noktasına içerik dağıtdıysanız ve sonra BranchCache 'i etkinleştirmeye karar verirseniz, önce özelliği yüklemeniz gerekir. Ardından içeriği bulut dağıtım noktasına yeniden dağıtın.

> [!NOTE]  
> Configuration Manager sürüm 1810 ve önceki sürümlerde, birden fazla bulut dağıtım noktanız varsa BranchCache anahtar parolasını el ile ayarlamanız gerekir. Daha fazla bilgi için bkz. [MICROSOFT DESTEĞI KB 4458143](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a>Ayarla  

Bu yordamı, bu bulut dağıtım noktasını [tasarımınız](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology)tarafından belirlendiği şekilde barındırmak için bu yordamı gerçekleştirin.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **bulut dağıtım noktaları**' nı seçin. Şeritte, **bulut dağıtım noktası oluştur**' u seçin.  

2. Bulut dağıtım noktası oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki ayarları yapılandırın:  

    1. Önce **Azure ortamını**belirleyin.  

    2. Sürüm 1806 ' den başlayarak dağıtım yöntemi olarak **Azure Resource Manager dağıtım** *' ı seçin*. Azure aboneliği yönetici hesabıyla kimlik doğrulamak için **oturum aç '** ı seçin. Sihirbaz, kalan alanları Azure AD tümleştirme önkoşulu sırasında depolanan bilgilerden otomatik olarak doldurur. Birden çok aboneliğiniz varsa, kullanılacak istenen aboneliğin **ABONELIK kimliğini** seçin.  

    > [!Note]  
    > Sürüm 1810 ' den başlayarak, Azure 'da klasik hizmet dağıtımları Configuration Manager kullanım dışıdır.
    >
    > Klasik hizmet dağıtımı kullanmanız gerekiyorsa, bu sayfada bu seçeneği belirleyin. İlk olarak Azure **ABONELIK kimliğinizi**girin. Ardından, **Araştır** ' ı seçin ve öğesini seçin. Azure Yönetim sertifikası için PFX dosyası.  

3. **İleri**’yi seçin. Site Azure bağlantısını test etmek için bekleyin.  

4. **Ayarlar** sayfasında, aşağıdaki ayarları belirtin ve ardından **İleri**' yi seçin:  

    - **Bölge**: bulut dağıtım noktasını oluşturmak istediğiniz Azure bölgesini seçin.  

    - **Kaynak grubu** (yalnızca Azure Resource Manager dağıtım yöntemi)  

        - **Mevcut olanı kullan**: açılan listeden var olan bir kaynak grubunu seçin.  

        - **Yeni oluştur**: Azure aboneliğinizde oluşturulacak yeni kaynak grubu adını girin.  

    - **Birincil site**: Bu dağıtım noktasına içerik dağıtılacak birincil siteyi seçin.

    - **Sertifika dosyası**: **Araştır** ' ı seçin ve öğesini seçin. Bu bulut dağıtım noktasının sunucu kimlik doğrulama sertifikası için PFX dosyası. Bu sertifikadaki ortak ad, gerekli **hizmet FQDN 'si** ve **hizmet adı** alanlarını doldurur.  

        > [!NOTE]  
        > Bulut dağıtım noktası sunucu kimlik doğrulama sertifikası joker karakterleri destekler. Joker karakter sertifikası kullanıyorsanız, `*` **hizmet FQDN 'si** alanındaki yıldız işaretini () hizmet için istenen ana bilgisayar adıyla değiştirin.  

5. **Uyarılar** sayfasında, depolama kotaları, aktarım kotaları ve bu kotaların ne yüzdesinden Configuration Manager uyarı oluşturmasını istediğinizi belirleyin. Ardından **İleri**' yi seçin.  

6. Sihirbazı tamamlayın.  

### <a name="monitor-installation"></a>Yükleme izleme  

Site, bulut dağıtım noktası için yeni bir barındırılan hizmet oluşturmaya başlar. Sihirbazı kapattıktan sonra, Configuration Manager konsolundaki bulut dağıtım noktasının yükleme ilerlemesini izleyin. Ayrıca birincil site sunucusundaki **CloudMgr. log** dosyasını da izleyin. Gerekirse, bulut hizmetinin Azure portal sağlama işlemini izleyin.  

> [!NOTE]  
> Azure 'da yeni bir dağıtım noktası sağlanması 30 dakika kadar sürebilir. **CloudMgr. log** dosyası, depolama hesabı sağlanana kadar Şu iletiyi yineler:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Depolama hesabı sağlamasını gerçekleştirdikten sonra hizmet oluşturulup yapılandırılır.  

### <a name="verify-installation"></a>Yüklemeyi doğrula

Aşağıdaki yöntemleri kullanarak bulut dağıtım noktası yüklemesinin tamamlandığını doğrulayın:  

- Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Cloud Services**öğesini genişletin ve **bulut dağıtım noktaları** düğümünü seçin. Yeni bulut dağıtım noktasını listede bulun. Durum sütunu, **Ready**olmalıdır.  

- Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Sistem durumu**' nu genişletin ve **Bileşen durumu** düğümünü seçin. **SMS_CLOUD_SERVICES_MANAGER** bileşeninden tüm iletileri gösterin ve durum iletisi kimliği **9409**' i arayın.  

- Gerekirse Azure portal gidin. Bulut dağıtım noktası **dağıtımı** için **hazırlık**durumu görüntülenir.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a>DNS yapılandırma  

İstemcilerin bulut dağıtım noktasını kullanabilmesi için, bulut dağıtım noktasının adını Azure tarafından yönetilen bir IP adresine çözebilmeleri gerekir. Yönetim noktası, bulut dağıtım noktasının **HIZMET FQDN** 'sini verir. Bulut dağıtım noktası, **hizmet adı**olarak Azure 'da bulunur. Bulut dağıtım noktası özelliklerinin **Ayarlar** sekmesinde bu değerlere bakın.

> [!Note]  
> Konsolundaki **bulut dağıtım noktaları** düğümü, **hizmet adı**adlı bir sütun Içerir, ancak gerçekte **hizmet FQDN 'si** değerini gösterir. Her iki değeri de görmek için, bulut dağıtım noktasının **özelliklerini** açın ve **Ayarlar** sekmesine geçin.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Sunucu kimlik doğrulama sertifikası ortak adı, etki alanı adınızı içermelidir. Bu ad, bir ortak sağlayıcıdan bir sertifika satın aldığınızda gereklidir. Bu sertifika, PKI 'ınızdan yayınlandığınızda önerilir. Örneğin, `WallaceFalls.contoso.com`. Bu sertifikayı bulut dağıtım noktası oluşturma Sihirbazı 'nda belirttiğinizde, ortak ad **HIZMET FQDN** özelliğini ( `WallaceFalls.contoso.com` ) doldurur. **Hizmet adı** aynı ana bilgisayar adını ( `WallaceFalls` ) alır ve Azure etki alanı adına ekler `cloudapp.net` . Bu senaryoda istemcilerin, etki alanının **HIZMET FQDN** 'sini () `WallaceFalls.contoso.com` Azure **hizmet adı** () olarak çözümlemesi gerekir `WallaceFalls.cloudapp.net` . Bu adları eşlemek için bir CNAME diğer adı oluşturun.

### <a name="create-cname-alias"></a>CNAME diğer adı oluştur

Kuruluşunuzun genel, internet 'e yönelik DNS 'de kurallı bir ad kaydı (CNAME) oluşturun. Bu kayıt, istemcilerin aldığı bulut dağıtım noktasının **HIZMET FQDN** özelliği Için Azure **hizmet adına**bir diğer ad oluşturur. Örneğin, için için yeni bir CNAME kaydı oluşturun `WallaceFalls.contoso.com` `WallaceFalls.cloudapp.net` .  

### <a name="client-name-resolution-process"></a>İstemci adı çözümleme işlemi

Aşağıdaki işlem, bir istemcinin bulut dağıtım noktasının adını nasıl çözdüğünü gösterir:  

1. İstemci, içerik kaynakları listesinde bulut dağıtım noktasının **HIZMET FQDN** 'sini alır. Örneğin, `WallaceFalls.contoso.com`.  

2. CNAME diğer adını kullanarak hizmet FQDN 'sini Azure **hizmet adına**çözümleyen DNS 'i sorgular. Örneğin, `WallaceFalls.cloudapp.net`.  

3. Azure hizmet adını Azure genel IP adresine çözümleyen DNS 'i yeniden sorgular.  

4. İstemci bu IP adresini, bulut dağıtım noktasıyla iletişimi başlatmak için kullanır.  

5. Bulut dağıtım noktası, sunucu kimlik doğrulama sertifikasını istemciye gösterir. İstemci, doğrulanacak sertifikanın güven zincirini kullanır.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a>Site sunucusu ara sunucusunu ayarlama  

Bulut dağıtım noktasını yöneten birincil site sunucusunun Azure ile iletişim kurması gerekir. Kuruluşunuz internet erişimini denetlemek için bir proxy sunucusu kullanıyorsa, birincil site sunucusunu bu proxy 'yi kullanacak şekilde yapılandırın.  

Daha fazla bilgi için bkz. [proxy sunucu desteği](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a>İçerik dağıtma ve istemcileri yapılandırma

İçeriği bulut dağıtım noktasına diğer şirket içi dağıtım noktasıyla aynı şekilde dağıtın. Yönetim noktası, istemcilerin talep aldığı içeriğe sahip olmadığı müddetçe, içerik konumları listesinde bulut dağıtım noktasını içermez. Daha fazla bilgi için bkz. [Içeriği dağıtma ve yönetme](deploy-and-manage-content.md).

Bulut dağıtım noktasını diğer şirket içi dağıtım noktasıyla aynı şekilde yönetin. Bu eylemler, bir dağıtım noktası grubuna atamayı ve içerik paketlerini yönetmeyi içerir. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](install-and-configure-distribution-points.md).

Varsayılan istemci ayarları, istemcilerin bulut dağıtım noktalarını kullanmasını otomatik olarak etkinleştirir. Aşağıdaki istemci ayarıyla hiyerarşinizdeki tüm bulut dağıtım noktalarına erişimi denetleyin:  

- **Bulut ayarları** grubunda, **bulut dağıtım noktalarına erişime izin ver**ayarını değiştirin.  

    - Varsayılan olarak, bu ayar **Evet**olarak ayarlanır.  

    - Bu ayarı hem kullanıcılar hem de cihazlar için değiştirin ve dağıtın.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a>Yönetme ve izleme  

Bulut dağıtım noktasına dağıttığınız içeriği diğer şirket içi dağıtım noktalarıyla aynı şekilde izleyin. Daha fazla bilgi için bkz. [Içeriği izleme](monitor-content-you-have-distributed.md).

Konsolunda bulut dağıtım noktalarının listesini görüntülediğinizde, listeye ek sütunlar ekleyebilirsiniz. Örneğin, **veri çıkış** sütunu, son 30 gün içinde hizmetten indirilen veri istemcilerinin miktarını gösterir.<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a>Larınız  

Configuration Manager Azure hizmetini düzenli olarak denetler. Hizmet etkin değilse ya da abonelik veya sertifika sorunları varsa Configuration Manager bir uyarı oluşturur.

Bulut dağıtım noktasında depolamak istediğiniz veri miktarı ve istemcilerin dağıtım noktasından indirme veri miktarı için eşikler yapılandırın. Bulut hizmetini ne zaman durdurulacağı veya sileceğine karar vermenize, bulut dağıtım noktasında depoladığınız içeriği ayarlamanıza veya hizmeti hangi istemcilerin kullanacağınızı değiştirmenize yardımcı olması için bu eşiklere yönelik uyarıları kullanın.

- **Depolama uyarı eşiği**: depolama uyarı eşiği, bulut dağıtım noktasında depolamak istediğiniz veri veya içerik MIKTARı üzerinden GB cinsinden bir üst sınır ayarlar. Bu eşik, varsayılan olarak 2.000 GB 'tır. Configuration Manager, kalan boş alan belirttiğiniz düzeylere ulaştığında uyarı ve kritik uyarılar üretir. Varsayılan olarak, bu uyarılar eşiğin %50 ve %90 ' de oluşur.  

- **Aylık aktarım uyarısı eşiği**: aylık aktarım uyarısı eşiği, 30 günlük sürede dağıtım noktasından istemcilere aktarılan içerik miktarını izlemenize yardımcı olur. Bu eşik, varsayılan olarak 10.000 GB 'tır. Bu site, aktarımlar tanımladığınız değerlere ulaştığında uyarı ve kritik uyarılar oluşturur. Varsayılan olarak, bu uyarılar eşiğin %50 ve %90 ' de oluşur.  

    > [!IMPORTANT]  
    > Configuration Manager, verilerin aktarımını izler, ancak belirtilen aktarım uyarısı eşiğini aşan veri aktarımını durdurmaz.  

Yükleme sırasında her bir bulut dağıtım noktası için eşikler belirtin veya bulut dağıtım noktası özelliklerinin **Uyarılar** sekmesini kullanın.  

> [!NOTE]  
> Bulut dağıtım noktası uyarıları, Azure 'un kullanım istatistiklerine bağlıdır ve bu da kullanılabilir hale gelir ve 24 saat sürebilir. Azure Depolama Analizi hakkında daha fazla bilgi için bkz. [depolama Analizi](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

Saatlik bir döngüde, bulut dağıtım noktasını izleyen birincil site işlem verilerini Azure 'dan indirir. Bu işlem verilerini `CloudDP-<ServiceName>.log` site sunucusundaki dosyasında depolar. Configuration Manager, bu bilgileri her bir bulut dağıtım noktası için depolama ve aktarım kotalarıyla karşılaştırarak değerlendirir. Verilerin aktarımı, uyarılar veya kritik uyarılar için belirtilen birime ulaştığında ya da bu verileri aştığında, uygun uyarıyı üretir Configuration Manager.  

> [!WARNING]  
> Site, Azure 'dan her saat veri aktarımlarıyla ilgili bilgileri indirdiği için, Configuration Manager verilere erişebilmeleri ve bir uyarı oluşturmadan önce kullanım bir uyarı veya kritik eşiği aşabilir.  


## <a name="modify"></a><a name="bkmk_modify"></a>Değiştirebilirler

Configuration Manager konsolunun **Yönetim** çalışma alanındaki **Cloud Services** altında bulunan **bulut dağıtım noktaları** düğümünde dağıtım noktasıyla ilgili üst düzey bilgileri görüntüleyin. Daha fazla ayrıntı görmek için bir dağıtım noktası seçin ve **Özellikler** ' i seçin.  

Bir bulut dağıtım noktasının özelliklerini düzenlediğinizde, aşağıdaki sekmelerde düzenlenecek ayarlar bulunur:  

#### <a name="settings"></a>Ayarlar

- **Açıklama**  

- **Sertifika dosyası**: sunucu kimlik doğrulama sertifikasının süresi dolmadan önce aynı ortak ada sahip yeni bir sertifika verin. Ardından, hizmetin kullanmaya başlaması için yeni sertifikayı buraya ekleyin. Sertifikanın süresi dolarsa, istemciler güvenmez ve hizmeti kullanmaz.  

#### <a name="alerts"></a>Uyarılar

Depolama ve aylık aktarım uyarıları için veri eşiklerini ayarlayın.  

#### <a name="content"></a>İçerik

İçeriği şirket içi dağıtım noktasıyla aynı şekilde yönetin.  

### <a name="redeploy-the-service"></a>Hizmeti yeniden dağıtın

Aşağıdaki yapılandırma gibi daha önemli değişiklikler, hizmetin yeniden dağıtılmasını gerektirir:

- Azure Resource Manager için klasik dağıtım yöntemi
- Abonelik
- Hizmet adı
- Genel PKI 'ya özel
- Azure bölgesi

Sürüm 1806 ' den başlayarak, klasik dağıtım yönteminde mevcut bir bulut dağıtım noktanız varsa, Azure Resource Manager dağıtım yöntemini kullanmak için yeni bir bulut dağıtım noktası dağıtmanız gerekir. İki seçenek vardır:

- Aynı hizmet adını yeniden kullanmak istiyorsanız:  

    1. Önce klasik bulut dağıtım noktasını silin. Başka bir bulut dağıtım noktası yoksa istemciler içerik alamıyor olabilir.  

    2. Kaynak Yöneticisi dağıtımı kullanarak yeni bir bulut dağıtım noktası oluşturun. Aynı sunucu kimlik doğrulama sertifikasını yeniden kullanın.  

    3. Gerekli yazılım paketi içeriğini yeni bulut dağıtım noktasına dağıtın.  

- Yeni bir hizmet adı kullanmak istiyorsanız:  

    1. Kaynak Yöneticisi dağıtımı kullanarak yeni bir bulut dağıtım noktası oluşturun. Yeni bir sunucu kimlik doğrulama sertifikası kullanın.  

    2. Gerekli yazılım paketi içeriğini yeni bulut dağıtım noktasına dağıtın.  

    3. Klasik bulut dağıtım noktasını silin.

> [!Tip]  
> Bir bulut dağıtım noktasının geçerli dağıtım modelini öğrenmek için:<!--SCCMDocs issue #611-->  
>
> 1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **bulut dağıtım noktaları** düğümünü seçin.  
> 2. **Dağıtım modeli** özniteliğini liste görünümüne bir sütun olarak ekleyin. Kaynak Yöneticisi dağıtımı için bu öznitelik **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Bulut hizmetini isteğe bağlı olarak durdurun veya başlatın

Configuration Manager konsolunda dilediğiniz zaman bulut dağıtım noktasını durdurun. Bu eylem, istemcilerin hizmetten ek içerik indirmelerini anında önler. İstemcilere erişimi geri yüklemek için Configuration Manager konsolundan bulut hizmetini yeniden başlatın. Örneğin, bir veri eşiğine ulaştığında bir bulut hizmetini durdurun.  

Bir bulut dağıtım noktasını durdurduğunuzda, bulut hizmeti içeriği depolama hesabından silmez. Ayrıca, site sunucusunun bulut dağıtım noktasına ek içerik aktarmasına engel olmaz. Yönetim noktası hala bulut dağıtım noktasını istemcilere geçerli bir içerik kaynağı olarak döndürür.

Bir bulut dağıtım noktasını durdurmak için aşağıdaki yordamı kullanın:  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Cloud Services**öğesini genişletin ve **bulut dağıtım noktaları** düğümünü seçin.  

2. Bulut dağıtım noktasını seçin. Azure 'da çalışan bulut hizmetini durdurmak için Şeritteki **hizmeti Durdur** ' u seçin.  

3. Bulut dağıtım noktasını yeniden başlatmak için **Hizmeti Başlat** ' ı seçin.  

### <a name="delete-a-cloud-distribution-point"></a>Bulut dağıtım noktasını silme

Bir bulut dağıtım noktasını kaldırmak için Configuration Manager konsolundaki dağıtım noktasını seçin ve **Sil**' i seçin.  

Bir hiyerarşiden bulut dağıtım noktasını sildiğinizde Configuration Manager, Azure 'daki bulut hizmetinden içeriği kaldırır.

Azure 'daki tüm bileşenleri el ile kaldırmak sistemin tutarsız olmasına neden olur. Bu durum yalnız bırakılmış bilgileri bırakır ve beklenmeyen davranışlar ortaya çıkabilir.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a>Gelişmiş sorun giderme

Bulut dağıtım noktanınızdan sorunları gidermeye yardımcı olmak üzere Azure VM 'lerinden tanılama günlüğü toplamanız gerekiyorsa, abonelik için hizmet tanılama uzantısını etkinleştirmek üzere aşağıdaki PowerShell örneğini kullanın:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

Aşağıdaki örnek, yukarıdaki PowerShell betiğindeki **public_config** değişkeninde başvurulan örnek bir **Diagnostics. wadcfgx** dosyasıdır. Daha fazla bilgi için bkz. [Azure tanılama uzantısı yapılandırma şeması](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
