---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Configuration Manager ile tümleştirilmiş masaüstü Analizi hizmetine genel bakış.
ms.date: 06/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 09f829bd1695426211ff94381a63b8f23d1b4fe8
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411023"
---
# <a name="what-is-desktop-analytics"></a>Desktop Analytics nedir?

Masaüstü analizi, Configuration Manager ile tümleşen bulut tabanlı bir hizmettir. Hizmet, Windows istemcilerinizin güncelleştirme hazırlığı hakkında daha bilinçli kararlar almanıza yardımcı olmak için Öngörüler ve zeka sağlar. Microsoft bulut hizmetlerine bağlı milyonlarca cihazdan toplanan verilerle kuruluşunuzdaki verileri birleştirir.

Configuration Manager ile birlikte masaüstü analizlerini kullanın:  

- Kuruluşunuzda çalışan uygulamaların envanterini oluşturma  

- En son Windows 10 özellik güncelleştirmeleriyle uygulama uyumluluğunu değerlendirin  

- Uyumluluk sorunlarını belirlemek ve bulut özellikli veri içgörüleri temelinde risk azaltma önerilerini almak  

- Minimum cihaz kümesi genelinde uygulamanın ve sürücünün tamamını temsil eden pilot grupları oluşturun  

- Pilot ve üretime yönetilen cihazlara Windows 10 dağıtma  

![Azure portal masaüstü Analizi giriş sayfasının ekran görüntüsü](media/portal-home.png)

Aşağıdaki videoda, masaüstü analizi hakkında daha fazla bilgi içeren bir Ignite 2019 oturumu bulunmaktadır:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Yönetim, bakım ve destek için veri odaklı Öngörüler aracılığıyla Windows TCO 'yu azaltmak için masaüstü analizlerini ve Configuration Manager kullanma](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Derinlemesine bir demo için 10:00 'e atlayın.

> [!Note]  
> Masaüstü analizi, 31 Ocak 2020 tarihinde kullanımdan kaldırılan Windows Analytics 'in bir ardıldır.
>
> Windows Analytics 'in özellikleri, masaüstü Analizi hizmetinde birleştirilir. Ayrıca, masaüstü Analizi Configuration Manager ile daha sıkı bir şekilde tümleşiktir. Daha fazla bilgi için bkz. [Windows Analytics müşterileri Için SSS](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Avantajlar

Birçok müşteri, Windows 10 ' da mevcut olan ve güncel bir sorun ile karşılaşıyor. Birincil zorluk, uygulamaları test ediyor. Bu işlem genellikle el ile yapılır. BT yöneticileri ve uygulama sahiplerinin mevcut uygulamaları sürekli analiz etmesine yönelik zaman alıcı bir işlemdir. Sonra ortaya çıkan tüm sorunları düzeltin.

Masaüstü Analizi aşağıdaki avantajları sağlar:

- **Cihaz ve yazılım envanteri**: uygulamalar ve Windows sürümleri gibi önemli faktörlerin envanterini çıkarın.  

- **Pilot kimlik**: faktörlerin en geniş kapsamını sağlayan en küçük cihaz kümesinin kimliği. Windows yükseltmelerinde ve güncelleştirmelerinde yapılan bir pilot için en önemli etkenlere odaklanır. Pilot uygulamanın daha başarılı olduğundan emin olmak, üretimde çok daha hızlı ve güvenle çalışmaya devam etmenizi sağlar.  

- **Sorun kimliği**: toplu pazar verilerini ortamınızdaki verilerle birlikte kullanarak, hizmet, mevcut sorunları Windows ile alma ve kullanmaya yönelik olası sorunları tahmin eder. Daha sonra potansiyel azaltmaları önerir.  

- **Configuration Manager tümleştirme**: hizmet bulutu-mevcut şirket içi altyapınızı mümkün. Windows 'u cihazlarınızda dağıtmak ve yönetmek için bu verileri ve çözümlemeyi kullanın.  

## <a name="prerequisites"></a>Önkoşullar

Masaüstü analizlerini kullanmak için ortamınızın aşağıdaki önkoşulları karşıladığından emin olun.

### <a name="technical"></a>Teknik

- [Genel yönetici](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) izinlerine sahip etkin bir genel Azure aboneliği. [Microsoft hesapları](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) desteklenmez.  

    > [!IMPORTANT]
    > Masaüstü analizi, Azure genel 'de barındırılan ve Windows tanılama verilerini kullanan bir Windows hizmetidir. Masaüstü analizi, ABD kamu müşterileri tarafından kullanılabilen bir Azure küresel hizmettir. Bu, [ABD kamu Community uyumluluk (GCC)](https://docs.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) özniteliklerini karşılamıyor. Microsoft ürün ve hizmetlerinin uyumluluk tekliflerinin bir listesi için bkz. [Microsoft Güven Merkezi](https://docs.microsoft.com/microsoft-365/compliance/offering-home?view=o365-worldwide). Masaüstü analizi, GCC High veya ABD Savunma Bakanlığı (DOD) müşterileri için kullanılamaz. Masaüstü Analizi çalışma alanlarını barındırmak için Azure Kamu aboneliklerinin kullanılması desteklenmez.

    - Çalışma alanınızı ve aşağıdaki rolleri **ayarlamak**Için **çalışma alanı sahibi** izinleri:  

      - [**Masaüstü Analizi yönetici**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) rolü.

      - Mevcut bir çalışma alanını kullanmak veya var olan bir kaynak grubunda yeni bir çalışma alanı oluşturmak için kaynak grubundaki katkıda bulunan ve [**Kullanıcı erişimi yöneticisi**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) [**Log Analytics**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) .

      - Yeni bir kaynak grubunda çalışma alanı oluşturmak için abonelikte [**sahip**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)veya [**katkıda bulunan**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) ve [**Kullanıcı erişimi Yöneticisi**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) izinleri.  

    - Ekleme işleminden sonra portala erişmek için şunlar gerekir:

      - Log Analytics çalışma alanında [**Masaüstü Analizi yönetici**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) rolü ve [**sahibi**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)ya da [**katkıda bulunan**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) izinleri.

- Configuration Manager, sürüm 1902 güncelleştirme paketi (4500571) veya üzeri. Daha fazla bilgi için bkz. [güncelleştirme Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    - Configuration Manager [**tam yönetici**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) rolü  

    > [!NOTE]
    > Masaüstü analizi, tek bir Azure AD kiracısına rapor veren birden çok Configuration Manager hiyerarşiyi destekler.<!-- 4814075 --> Ortamınızda birden çok hiyerarşinizi varsa, aşağıdaki seçeneklere sahip olursunuz:
    >
    > - Farklı ticari kimlikler ve Azure AD kiracılarını kullanın.
    > - Her iki hiyerarşiyi de Azure AD kiracısı ve Masaüstü Analizi örneğini paylaşmak için aynı ticari KIMLIĞI kullanacak şekilde yapılandırın. Her hiyerarşiyi bağlamak için [farklı uygulamalar](connect-configmgr.md#bkmk_connect) kullanın. Portalın değişiklikleri yansıtması için bir hiearchy bağlantısı kesildikten sonra 30 güne kadar zaman alabilir. 

- Windows 7, Windows 8.1 veya Windows 10 çalıştıran cihazlar  

    - En son güncelleştirmeleri yükler. Daha fazla bilgi için bkz. [cihazları güncelleştirme](enroll-devices.md#update-devices).  

    - Cihazların Ayrıca Configuration Manager Client, sürüm 1902 güncelleştirme paketi (4500571) veya sonraki bir sürüme sahip olması gerekir. Daha fazla bilgi için bkz. [güncelleştirme Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    > [!Note]  
    > Masaüstü analizi, Windows 10 uzun süreli bakım kanalına (LTSC) veya bu bilgisayardan yükseltmeleri desteklemez. Daha fazla bilgi için bkz. [hizmet olarak Windows 'a genel bakış](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Masaüstü analizi, yerinde yükseltme senaryosunu en iyi şekilde destekleyecek şekilde tasarlanmıştır. 32 bitlik mimari-64-bit mimarisine gibi büyük değişiklikler yapmanız gerekiyorsa, bir görüntüleme senaryosu kullanın. Bu klasik işletim sistemi dağıtım senaryolarında masaüstü Analizi öngörüleri hâlâ değerlidir, ancak yerinde yükseltmeye özgü Kılavuzu yoksayabilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager ile kurumsal işletim sistemlerini dağıtma senaryoları](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Windows Tanılama verileri. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

    - [Tanılama veri düzeyleri](enable-data-sharing.md#diagnostic-data-levels)  

    - [Masaüstü Analizi gizliliği](privacy.md)  

- Cihazlardan Microsoft genel bulutuna ağ bağlantısı. Daha fazla bilgi için bkz. [veri paylaşımını etkinleştirme](enable-data-sharing.md)  

> [!Important]
> Microsoft 'un gizliliğinizi denetim altına alan araçlar ve kaynakları sağlamaya yönelik güçlü bir taahhüt vardır. Sonuç olarak, Microsoft, Avrupa ülkelerinde (EEA ve Isviçre) bulunan cihazlardan aşağıdaki verileri toplamaz:
>
> - Windows 8.1 cihazlarından Windows Tanılama verileri
> - Windows 7 için uygulama kullanım verileri

### <a name="licensing-and-costs"></a>Lisanslama ve maliyetler

- Etkin bir genel Azure aboneliği.

    > [!NOTE]
    > Configuration Manager için eşdeğer aboneliklerin çoğu ayrıca Azure AD ' i de içerir. Örneğin, bkz. [Microsoft 365 planları](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) ve [Enterprise Mobility + Security lisanslama](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Masaüstü analizine kayıtlı cihazların geçerli bir Configuration Manager lisansı olması gerekir. Daha fazla bilgi için bkz. [Configuration Manager lisanslama](../core/understand/product-and-licensing-faq.md).

- Cihazın kullanıcıları aşağıdaki lisanslardan birine gerek duyar:

  - Windows 10 Enterprise E3 veya E5 (Microsoft 365 F3, E3 veya E5 'e dahildir)

  - Windows 10 eğitim a3 veya a5 (Microsoft 365 a3 veya a5 'e dahildir)

  - Windows sanal masaüstü erişimi E3 veya E5  

> [!NOTE]
> Bu lisans aboneliklerinin maliyetinin ötesinde, Azure Log Analytics 'da masaüstü analizinin kullanılmasına yönelik ek ücret alınmaz. Masaüstü Analizi tarafından alınan veri türleri Log Analytics veri alımı ve bekletme ücretlerinden ücretsizdir. Bu veriler, faturalandırılamayan veri türleri olarak Log Analytics, günlük veri alma Cap 'e de tabi değildir. Daha fazla bilgi için bkz. [Log Analytics kullanımı ve maliyetleri](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki öğreticide, masaüstü analizine ve Configuration Manager kullanmaya başlamak için adım adım kılavuz sunulmaktadır:
  
> [!div class="nextstepaction"]
> [Windows 10’u pilotta dağıtma](tutorial-windows10.md)
