---
title: Microsoft Intune-Azure kullanarak Zeköşeli cihazlara çok sayıda OEMConfig profili dağıtma | Microsoft Docs
description: Android Enterprise çalıştıran Zeköşeli cihazlarda birden çok OEMConfig cihaz yapılandırma profili oluşturmak ve dağıtmak için Microsoft Intune kullanın. Profillerinizi sıralamak için Zeköşeli eylemleri ve adımları kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988683"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Microsoft Intune 'de birden çok OEMConfig profilini Zeköşeli cihazlara dağıtma

Microsoft Intune 'de, Android Kurumsal cihazları için OEM 'e özgü ayarları özelleştirmek üzere OEMConfig ' i kullanın. Bu ayarlar cihaz üreticisine özeldir ve Intune 'da yapılandırma profilleri kullanılarak dağıtılır.

Zeköşeli cihazlarda, aynı cihaza birden çok profil dağıtabilir veya atayabilirsiniz. Mevcut OEMConfig profilleri, cihazların Intune ile bir sonraki eşitlenebilmesi durumunda bu özelliği kullanabilir.

Bu özellik şu platformlarda geçerlidir:

- Android Enterprise çalıştıran zeköşeli cihazlar

OEMConfig hakkında daha fazla bilgi edinmek için neler yaptığı ve nasıl kullanılacağı dahil olmak üzere, bkz. [oemconfig yapılandırma profili](android-oem-configuration-overview.md).

Bu makalede, Zeköşeli cihazlara OEMConfig birden çok profili dağıtma, sıralamayı açıklar ve Microsoft Intune içindeki raporlama özellikleri kullanılarak açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar

Bir [Oemconfig yapılandırma profili](android-oem-configuration-overview.md)oluşturun.

## <a name="use-multiple-profiles"></a>Birden çok profil kullanma

Zeköşeli cihazlarda, her cihazda aynı anda birçok profil bulunabilir. Bu özellik, Zeköşeli OEMConfig ayarlarınızı daha küçük profillere böetmenize olanak tanır. Ze, OEMConfig şeması da **eylemleri**kullanır. Eylemler, cihazda çalışan işlemlerdir. Ayarları yapılandırmaz. Dosya indirmeyi tetiklemek, Panoyu temizlemek ve daha fazlasını yapmak için bu eylemleri kullanın. Desteklenen eylemlerin tam listesi için bkz. [zeköşeli belgeleri](https://techdocs.zebra.com/oemconfig/10-0/about/) (zetaya 'nın Web sitesini açar).

Örneğin, cihaza bazı ayarlar uygulayan bir Zeköşeli OEMConfig profili oluşturursunuz. Başka bir Zeköşeli OEMConfig profili, Panoyu temizleyen bir eylem içerir. İlk profili bir Zeköşeli cihazlar grubuna atarsınız. Daha sonra bu cihazlarda panoyu temizlemeniz gerekir. İkinci profili, ilk profili değiştirmeden aynı aygıtlar grubuna atarsınız. Cihaz panosu, ilk profilde oluşturulan yapılandırma ayarlarını yeniden göndermeden veya etkilemeden temizlenir.

Başka bir örnekte, bazı Zeköşeli cihaz ayarlarını yapılandıran bir OEMConfig profili atadınız. Son olarak, kullanıcılar belirli bir uygulamayla ilgili sorunları bildiriyor ve uygulamanın önbelleğini temizlemek istiyorsunuz. Yalnızca "Önbelleği Temizle" eylemini içeren yeni bir OEMConfig profili oluşturun. Profili, ihtiyaç duyulan cihazlara atayın.

## <a name="ordering"></a>Sıralama

Her cihazda birden fazla profille, profillerin dağıtıldığı sıra garanti edilmez. Bu davranış Google Play kısıtlamadır. İşlemleri sırayla çalıştırmak için [Zeköşeli işlem özelliğini](https://techdocs.zebra.com/oemconfig/9-1/mc/) kullanabilirsiniz (Zela 'nın Web sitesini açar). Şimdi örneği inceleyelim.

İki profil vardır:

- **Profil 1**: Bluetooth 'u açar. Bu profil Pazartesi günü **tüm cihazlar** grubuna atanır.
- **Profil 2**: başka bir ayar yapılandırır. Bu profil, **tüm cihazlar** grubuna Salı günü atanır.

Diğer ayar yapılandırıldıktan sonra Bluetooth 'un açık olması gerekir.

Çarşamba 'da, Intune ile 10 yeni Zeköşeli cihaz kaydeder. Profil 1 ve profil 2 **tüm cihazlar** grubuna atanır. Yeni cihazlar Intune ile eşitlendikten sonra profilleri alırlar. Bu cihazlar profil 1 ' den önce profil 2 alabilir.

İşlemlerin sırayla çalıştırıldığını onaylamak için Zeköşeli şeması 'ndaki **adımlar** özelliğini kullanın. Bu durumda, iki Işlem adımını içeren bir profil oluşturursunuz. İlk adım Bluetooth ayarlarını içerir ve ikinci adım diğer ayarı yapılandırır. Zeucin OEMCong uygulaması profili aldığında, bu adımları, Zeköşeli tarafından garanti edilen sırayla çalıştırır.

Daha fazla bilgi için bkz. [zeköşeli işlem adımları](https://techdocs.zebra.com/oemconfig/9-1/mc/) (Zela 'nın Web sitesini açar).

## <a name="enhanced-reporting"></a>Gelişmiş raporlama

Bir profil dağıtırsınız ve cihazdaki Zeköşeli OEMConfig uygulaması tarafından yürütülür. Zeköşeli OEMConfig uygulaması, profil durumunu Intune olarak bildirir. Endpoint Manager Yönetim merkezinde, dağıtılan OEMConfig profillerinin durumunu ve hata ya da uyarıları görebilirsiniz.

1. [Microsoft Endpoint Manager yönetim merkezini](https://go.microsoft.com/fwlink/?linkid=2109431)açın.
2. **Monitor**  >  **Cihaz durumunu**izlemek > zeköşeli oemconfig profilinizi seçin. Bu seçenek, OEMConfig profilinizin atandığı cihazları gösterir.
3. Cihaz **yapılandırma** > bir cihaz seçin > Zeköşeli oemconfig profilinizi seçin. Bu seçenek, başarılı veya başarısız olan profil ayarlarını gösterir.

    Hatalı bir satır seçin. Ayrıntıları neden başarısız olduğuna ilişkin daha fazla bilgi içeren ayrıntılar gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Oemconfig yapılandırma profilleri](android-oem-configuration-overview.md)hakkında daha fazla bilgi edinin.
- Android Cihaz Yöneticisi 'nde [Mobility uzantıları 'nı (MX)](android-zebra-mx-overview.md)yapılandırın.
- [Profil durumunu izleyin](device-profile-monitor.md).
