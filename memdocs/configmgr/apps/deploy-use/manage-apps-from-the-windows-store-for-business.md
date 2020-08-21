---
title: Microsoft Mağazası uygulamaları
titleSuffix: Configuration Manager
description: Configuration Manager ile Iş ve eğitim için Microsoft Store uygulamaları yönetin ve dağıtın.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8125f55215fd597d9611723e1d36629850bff44
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695231"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Configuration Manager ile Iş ve eğitim için Microsoft Store uygulamaları yönetin

[İş ve eğitimin Microsoft Store](/microsoft-store/) , kuruluşunuz için Windows uygulamalarını nerede bulabileceğinizi ve elde ettiğiniz yerdir. Mağazayı Configuration Manager bağladığınızda, elde ettiğiniz uygulamaların listesini eşitlemeniz gerekir. Bu uygulamaları Configuration Manager konsolunda görüntüleyin ve başka herhangi bir uygulamayı dağıttığınız gibi dağıtın.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a> Çevrimiçi ve çevrimdışı uygulamalar

Iş ve eğitimin Microsoft Store iki tür uygulamayı destekler:

- **Çevrimiçi**: Bu lisans türü, kullanıcıların ve cihazların bir uygulamayı ve lisansını almak için depoya bağlanmasını gerektirir. Windows 10 cihazları Azure Active Directory (Azure AD) ile Birleşik veya karma Azure AD 'ye katılmış olmalıdır.  

- **Çevrimdışı**: Bu tür, uygulamaları ve lisansları doğrudan şirket içi ağınızda dağıtmak üzere önbelleğe almanızı sağlar. Cihazların mağazaya bağlanması veya internet bağlantısı olması gerekmez.

Daha fazla bilgi için bkz. [iş ve eğitime genel bakış Microsoft Store](/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Yeteneklerin Özeti

Configuration Manager, Configuration Manager istemcisiyle Windows 10 cihazlarında ve ayrıca Microsoft Intune kayıtlı Windows 10 cihazlarında Iş ve eğitim uygulamalarına yönelik Microsoft Store yönetmeyi destekler. Configuration Manager çevrimiçi ve çevrimdışı uygulamalar için aşağıdaki özellikleri sunar:

|Özellik|Çevrimdışı uygulamalar|Çevrimiçi uygulamalar|
|------------|------------|------------|
|Uygulama verilerini Configuration Manager ile eşitler<br>(eşitleme 24 saatte bir gerçekleşir)|Evet|Evet|
|Mağaza uygulamalarından Configuration Manager uygulamalar oluşturma|Evet|Evet|
|Mağazadan ücretsiz uygulamalar için destek|Evet|Evet|
|Mağazadan ücretli uygulamalar için destek|Hayır|Evet<sup>[1](#bkmk_note1)</sup>|
|Kullanıcı veya cihaz koleksiyonlarına gereken dağıtımları destekleme|Evet|Evet|
|Kullanıcı veya cihaz koleksiyonlarına sunulan dağıtımları destekleme|Evet|Evet|
|Mağazadan iş kolu uygulamalarını destekleme|Evet|Evet|
|Cihazdaki tüm kullanıcılar için bir mağaza uygulaması sağlama<sup>[notunda 2](#bkmk_note2)</sup><!--1358310-->|Evet|Evet|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a> Note 1: çevrimiçi lisanslı uygulamalar sürüm gereksinimi

Çevrimiçi lisanslı uygulamaları Configuration Manager istemcisiyle Windows 10 cihazlarına dağıtmak için, Windows 10, sürüm 1703 veya sonraki bir sürümü çalıştırmalıdır.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a> 2. Note: en düşük Configuration Manager sürümü

1806 sürümünden başlayarak. Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../get-started/creating-windows-applications.md#bkmk_provision).  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Configuration Manager istemcisini çalıştıran cihazlara Iş ve eğitim Microsoft Store kullanarak çevrimiçi uygulamalar dağıtma

Tüm Configuration Manager istemcisini çalıştıran cihazlara Iş ve eğitim uygulamaları için Microsoft Store dağıtılmadan önce aşağıdaki noktaları göz önünde bulundurun:

- Tüm işlevler için cihazların Windows 10, sürüm 1703 veya üstünü çalıştırması gerekir.  

- Cihazları bir yönetim aracı olarak Iş ve eğitim için Microsoft Store kaydettiğiniz Azure AD kiracısına kaydedin veya birleştirin.  

- Yerel yönetici hesabı cihazda oturum açtığında, Iş ve eğitim uygulamalarına yönelik Microsoft Store erişemez.  

- Cihazların Iş ve eğitim için Microsoft Store canlı bir internet bağlantısı olması gerekir. Ara sunucu yapılandırması dahil daha fazla bilgi için bkz. [Önkoşullar](/microsoft-store/prerequisites-microsoft-store-for-business).  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Windows 10 ' un önceki sürümlerini çalıştıran cihazların notları

Configuration Manager istemcisi olan ve Windows 10 sürüm 1607 veya öncesini çalıştıran cihazlarda aşağıdaki işlevler geçerlidir:  

Aşağıdaki yöntemlerden birini izleyerek, uygulamanın cihaza yüklenmesini zorunlu kılabilirsiniz:  

- Kullanıcı uygulamayı yüklüyor  

- Dağıtım, yükleme son tarihine ulaştı

- Gerekli dağıtımlar için yükleme sonrası yeniden değerlendirme  

Ardından aşağıdaki davranışlar oluşur:  

- Configuration Manager istemcisi, Microsoft Store uygulamayı başlatarak uygulamayı "zorunlu tutar"  

- Kullanıcının mağazadan yüklemeyi tamamlaması gerekir  

- Configuration Manager konsolunda, uygulama dağıtım durumu şu hata nedeniyle hata bildiriyor: "Microsoft Store uygulama istemci bılgısayarda açıldı ve kullanıcının yüklemeyi tamamlamasını bekliyor."  

Sonraki uygulama değerlendirme döngüsünün:  

- Kullanıcı uygulamayı mağazadan yükle,, uygulama durumu **başarılı** olarak bildiriyor  

- Kullanıcı uygulamayı mağazadan yüklemeyi denemediyse:  

  - Gerekli dağıtımlar için Configuration Manager istemcisi mağaza uygulamasını yeniden başlatmaya çalışır  

  - Configuration Manager, kullanılabilir dağıtımları yeniden zorlamaz

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Windows 10 ' un önceki sürümlerini çalıştıran cihazlar

- İş kolu uygulamalarını Iş ve eğitim için Microsoft Store dağıtamazsınız

- Mağaza 'dan ücretli uygulamalar dağıttığınızda, kullanıcıların mağazada oturum açması ve uygulamayı almaları gerekir  

- Microsoft Store tüketici sürümüne erişimi devre dışı bırakmak için bir grup ilkesi dağıtırsanız, Microsoft Store Iş ve eğitim için olan dağıtımlar çalışmaz. Bu davranış, Iş ve eğitim için Microsoft Store etkinleştirseniz bile meydana gelir.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a> Eşitlemeyi ayarla

Kuruluşunuzun elde ettiği Iş ve eğitim uygulamalarının Microsoft Store listesini eşitlediğinizde, bu uygulamaları Configuration Manager konsolunda görürsünüz.

Configuration Manager sitenizi Azure AD 'ye bağlayın ve Iş ve eğitim için Microsoft Store. Bu işlemin daha fazla bilgi ve ayrıntılarını görmek için bkz. [Azure hizmetlerini yapılandırma](../../core/servers/deploy/configure/azure-services-wizard.md). **İş için Microsoft Store** hizmetine bir bağlantı oluşturun.

Hizmet bağlantı noktasının ve hedeflenen cihazların bulut hizmetine erişebildiğinden emin olun. Daha fazla bilgi için bkz. [iş ve eğitim için Microsoft Store önkoşulları-proxy yapılandırması](/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a> Ek bilgi ve yapılandırma

Azure Hizmetleri Sihirbazı 'nın **uygulama** sayfasında, önce **Azure ortamını** ve **Web uygulamasını**yapılandırın. Ardından sayfanın alt kısmındaki **daha fazla bilgi** bölümünü okuyun. Bu bilgiler Iş ve eğitim portalı için Microsoft Store aşağıdaki ek eylemleri içerir:  

- Mağaza yönetim aracı olarak Configuration Manager yapılandırın. Daha fazla bilgi için bkz. [Yönetim sağlayıcısını yapılandırma](/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Çevrimdışı lisanslı uygulamalar için desteği etkinleştirin. Daha fazla bilgi için bkz. [çevrimdışı uygulamaları dağıtma](/microsoft-store/distribute-offline-apps).  

- En az bir uygulama edinin. Daha fazla bilgi için bkz. [uygulamaları bulma ve alma](/microsoft-store/find-and-acquire-apps-overview).  

Azure hizmetleri sihirbazının **Konfigürasyonlar** sayfasında, aşağıdaki bilgileri belirtin:  

- **Microsoft Store iş uygulaması içerik depolaması Için yol**: bir klasör dahil olmak üzere paylaşılan ağ yolunu belirtin. Örneğin, `\\server\share\folder`. Site sunucusu mağaza ile eşitlendikten sonra bu konumdaki içeriği önbelleğe alır. Configuration Manager ' de bir uygulama oluşturduğunuzda, site sunucusu bu yerel önbellekteki uygulama içeriğini sitenin içerik kitaplığına kopyalar.  

- **Seçilen diller**: mağazadan eşitlenecek dilleri seçin ve yazılım merkezi 'nde kullanıcılara görüntüleyin. Örneğin, Kullanıcı Almanca için Windows 'u yapılandırırsa, yazılım merkezi mağaza uygulaması için Almanya dizelerini gösterir. Bu davranış, dilin eşitlenmesini ve belirli bir uygulama için var olmasını gerektirir.

- **Varsayılan dil**: kullanıcının dili kullanılamıyorsa, kullanılacak varsayılan dili seçin.  

> [!NOTE]
> Configuration Manager uygulama simgesini depodan eşitlemez. Yazılım Merkezi 'nde bu uygulama için görüntülenecek simgeye ihtiyacınız varsa, uygulamayı uygulama özelliklerine el ile ekleyin. Daha fazla bilgi için bkz. [uygulama bilgilerini el ile belirtme](create-applications.md#bkmk_manual-app).<!-- 2837053 -->

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a> Uygulama oluşturma ve dağıtma

Eşitlemeden sonra, diğer Configuration Manager uygulamalarına benzer Iş ve eğitim uygulamaları için Microsoft Store oluşturun ve dağıtın.

1. Configuration Manager konsolunun **yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **Mağaza uygulamaları için lisans bilgileri** düğümünü seçin.  

2. Dağıtmak istediğiniz uygulamayı seçin, ardından şeritte **uygulama oluştur** ' u seçin.  

Site, Iş ve eğitim uygulaması için Microsoft Store içeren bir Configuration Manager uygulaması oluşturur.

Daha sonra bu uygulamayı diğer Configuration Manager uygulamaları gibi dağıtın ve izleyin. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [Uygulamaları dağıtma](deploy-applications.md)
- [Uygulamaları konsoldan izleme](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Sonraki adımlar

**Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **Mağaza uygulamaları için lisans bilgileri** düğümünü seçin.

Yönettiğiniz her mağaza uygulaması için uygulamayla ilgili aşağıdaki bilgileri görüntüleyin:

- Uygulama adı
- Uygulama platformu
- Sahip olduğunuz uygulama için lisans sayısı
- Kullanılabilir lisansların sayısı

Çevrimiçi uygulamalar dağıttıktan sonra, bu uygulamaya yönelik tüm güncelleştirmeler doğrudan Microsoft Store gelir. Ayrıca, Configuration Manager çevrimiçi uygulamaların sürüm uyumluluğunu denetetmez, yalnızca Windows uygulamayı yüklendi olarak bildirir.  

Configuration Manager istemcisi ile Windows 10 cihazlarına çevrimdışı uygulamalar dağıttığınızda, kullanıcıların Configuration Manager dağıtımlar dışındaki uygulamaları güncelleştirmesine izin vermez. Çevrimdışı uygulamalardaki güncelleştirmelerin denetimi, özellikle sınıfsallar gibi çok kullanıcılı ortamlarda önemlidir. Microsoft Store devre dışı bırakmak için bir seçenek, [Grup İlkesi](/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy)kullanmaktır.

Iş ve eğitim yöneticisi için Microsoft Store, çevrimdışı bir uygulama elde ettikten sonra, uygulamayı mağaza aracılığıyla kullanıcılara yayımlamayın. Bu yapılandırma, kullanıcıların çevrimiçi olarak yüklenip güncelleştirebir şekilde emin olmanızı sağlar. Kullanıcılar, Configuration Manager aracılığıyla yalnızca çevrimdışı uygulama güncelleştirmelerini alırlar.

## <a name="see-also"></a>Ayrıca bkz.

[Configuration Manager ile Iş ve eğitim tümleştirmesi Microsoft Store sorunlarını giderin](troubleshoot-microsoft-store-for-business-integration.md)