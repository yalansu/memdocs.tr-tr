---
title: Topluluk hub 'ı ve GitHub
titleSuffix: Configuration Manager
description: Configuration Manager 'de topluluk hub 'ını etkinleştirme ve kullanma
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128180"
---
# <a name="community-hub-and-github"></a>Topluluk hub 'ı ve GitHub
<!--3555935, 3555936-->

BT Yöneticisi topluluğu, yıllar boyunca çok fazla bilgi geliştirmiştir. Komut dosyaları ve raporlar gibi öğeleri sıfırdan yeniden almak yerine, BT yöneticilerinin birbirleriyle paylaştığı bir **Configuration Manager Community hub 'ı** oluşturduk. Başkalarının çalışmasını izleyerek iş saatlerini tasarrufu sağlayabilirsiniz. Topluluk hub 'ı, diğerleri üzerinde oluşturma ve diğer kişilerin kendi üzerinde derlenme yoluyla yaratıcıkileri. GitHub zaten, paylaşım için tasarlanmış sektör genelinde işlemlere ve araçlara sahiptir. Artık topluluk hub 'ı, bu yeni topluluğu yönlendiren temel parçalar halinde doğrudan Configuration Manager konsolundaki bu araçlardan faydalanır. İlk sürüm için, topluluk hub 'ında kullanılabilir hale getirilen içerik yalnızca Microsoft tarafından karşıya yüklenir. Gelecekte, BT yöneticileri kendi GitHub hesaplarını kullanarak kendi kendilerine içerik yükleyebilecektir.

> [!Note]  
> Topluluk hub 'ı, isteğe bağlı bir bulut tabanlı özelliktir. İlk önce Haziran 2020 ' de kullanıma sunulmuştur. Topluluk hub 'ını kabul etme hakkında daha fazla bilgi için bkz. [Isteğe bağlı özellikler](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Topluluk Merkezi hakkında

Topluluk hub 'ı aşağıdaki nesneleri destekler:

- CMPivot sorguları
- Uygulamalar
- Görev dizileri
- Yapılandırma öğeleri
- PowerShell Betikleri
- Raporlar

## <a name="prerequisites"></a>Ön koşullar

- Topluluk hub 'ına erişmek için kullanılan Configuration Manager konsolunu çalıştıran cihaz aşağıdaki öğelere ihtiyaç duyuyor:
   - .NET Framework sürüm 4,6 veya üzeri
   - Windows 10 derleme 17110 veya üzeri
      - Windows Server desteklenmez, bu nedenle Configuration Manager konsolunun site sunucusundan ayrı bir Windows 10 cihazına yüklenmesi gerekir.
   - Oturum açan kullanıcı hesabı yerleşik yönetici hesabı olamaz

- Configuration Manager [Yönetim hizmetinin](../../../develop/adminservice/set-up.md) ayarlanması ve çalışması gerekir.

- Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, Configuration Manager konsolunun İnternet uç noktalarına erişmesine izin vermeniz gerekir. Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../plan-design/network/internet-endpoints.md#community-hub).

## <a name="permissions"></a>İzinler

- Bir betiği içeri aktarmak için: **SMS_Scripts** sınıfı Için izin **Oluştur** .
- Bir raporu içeri aktarmak için: tam yönetici güvenlik rolü.


## <a name="use-the-community-hub"></a>Topluluk hub 'ını kullanma

1. **Topluluk** çalışma alanındaki **topluluk hub** 'ı düğümüne gidin.
1. İndirilecek bir öğe seçin.
1. Hub 'dan nesneleri indirmek ve siteye içeri aktarmak için Configuration Manager sitenizde uygun izinlere sahip olmanız gerekir.
    - Bir betiği içeri aktarmak için: SMS_Scripts sınıfı için izin **Oluştur** .
    - Bir raporu içeri aktarmak için: tam yönetici güvenlik rolü.
1. İndirilen raporlar, Raporlama Hizmetleri noktasında **hub** adlı bir rapor klasörüne dağıtılır. İndirilen betikler **betikleri Çalıştır** düğümünde görülebilir.
1. **Topluluk hub** 'ı düğümünden **indirilekleriniz** ' a tıklayarak, kuruluşunuz tarafından indirilen tüm öğeleri görüntüleyin.

[![Topluluk hub 'ından indirilen tüm öğeler](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a>Topluluk hub 'ı öğelerine doğrudan bağlantılar
<!--4224406-->
*(Sürüm 2006 ' de tanıtılmıştır)* Doğrudan bağlantı ile Configuration Manager konsolu topluluk hub düğümündeki öğelere kolayca gidebilirsiniz ve başvurabilirsiniz. Bu özelliğin amacı, daha kolay işbirliği yapmak ve iş arkadaşlarınızla topluluk hub öğeleri bağlantılarını paylaşabiliyor. Bu derin bağlantılar Şu anda yalnızca konsolun topluluk hub düğümündeki öğeler için geçerlidir.

### <a name="prerequisites-for-direct-links"></a>Doğrudan bağlantılar için Önkoşullar

- Configuration Manager Konsolu sürüm 2006 veya üzeri
- Bir topluluk hub 'ı bağlantısını izleyerek yerel yerleşik yönetici hesabını kullanamazsınız.

### <a name="sharing-and-opening-direct-links"></a>Doğrudan bağlantıları paylaşma ve açma

Bir öğeyi paylaşmak için:
1. Hub 'daki öğeye gidip **paylaşma**' yı seçin.
1. Kopyalanmış bağlantıyı yapıştırın ve başkalarıyla paylaşabilirsiniz.

Paylaşılan bir bağlantıyı açmak için:
1. Configuration Manager konsolunun yüklü olduğu bir makineden bağlantıya tıklayın.
   - Örneğin, bu bağlantıyı kullanarak [kenar otomatik güncelleştirme betiğini](https://communityhub.microsoft.com/item/7200) ( `https://communityhub.microsoft.com/item/7200` ) paylaşabilirsiniz.
1. İstendiğinde **topluluk hub 'ını Başlat ' ı** seçin.
1. Konsol doğrudan topluluk merkezindeki komut dosyasına açılır.

## <a name="known-issues"></a><a name="bkmk_known"></a>Bilinen sorunlar

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>Konsol farklı bir kullanıcı olarak çalıştırılırken topluluk hub düğümüne erişilemiyor
<!--7826897-->
Daha düşük haklara sahip bir kullanıcı olarak oturum açtıysanız ve Configuration Manager konsolunu açmak için farklı bir Kullanıcı **olarak çalıştır** ' ı seçerseniz, **topluluk hub** düğümüne erişemeyebilirsiniz.

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>İndirilen raporlar indirmeler sayfasından kaldırılmaz
<!--7851305-->
İndirilen bir raporu **izleme**  >  **raporları** düğümünden silerseniz, rapor **topluluk hub 'ından**  >  **indirmeler** sayfasında silinmez ve raporu yeniden indiremez. 

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki nesneleri oluşturma ve kullanma hakkında daha fazla bilgi edinin:

- [PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md)
- [Raporlamaya giriş](introduction-to-reporting.md)
- [Görev dizileri oluşturma ve yönetme](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Uygulama oluşturma ve dağıtma](../../../apps/get-started/create-and-deploy-an-application.md)
- [Yapılandırma öğeleri oluşturma](../../../compliance/deploy-use/create-configuration-items.md)