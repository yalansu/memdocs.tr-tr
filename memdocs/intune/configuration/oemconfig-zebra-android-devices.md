---
title: Microsoft Intune-Azure kullanarak Zeköşeli cihazlara çok sayıda OEMConfig profili dağıtma | Microsoft Docs
description: Android Enterprise çalıştıran Zeköşeli cihazlarda birden çok OEMConfig cihaz yapılandırma profili oluşturmak ve dağıtmak için Microsoft Intune kullanın. Profillerinizi sıralamak için Zeköşeli eylemleri ve adımları kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
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
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311192"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Microsoft Intune 'de birden çok OEMConfig profilini Zeköşeli cihazlara dağıtma

Microsoft Intune 'de, Android Kurumsal cihazları için OEM 'e özgü ayarları özelleştirmek üzere OEMConfig ' i kullanın. Bu ayarlar cihaz üreticisine özeldir ve Intune 'da yapılandırma profilleri kullanılarak dağıtılır.

Zeköşeli cihazlarda, aynı cihaza birden çok profil dağıtabilir veya atayabilirsiniz. Mevcut OEMConfig profilleri, cihazların Intune ile bir sonraki eşitlenebilmesi durumunda bu özelliği kullanabilir.

Bu özellik şu platformlarda geçerlidir:

- Android Enterprise çalıştıran zeköşeli cihazlar

OEMConfig hakkında daha fazla bilgi edinmek için neler yaptığı ve nasıl kullanılacağı dahil olmak üzere, bkz. [oemconfig yapılandırma profili](android-oem-configuration-overview.md).

Bu makalede, Zeköşeli cihazlara OEMConfig birden çok profili dağıtma, sıralamayı açıklar ve Microsoft Intune içindeki raporlama özellikleri kullanılarak açıklanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

Bir [Oemconfig yapılandırma profili](android-oem-configuration-overview.md)oluşturun.

## <a name="use-multiple-profiles"></a>Birden çok profil kullanma

Zeköşeli cihazlarda, her cihazda aynı anda birçok profil bulunabilir. Bu özellik, Zeköşeli OEMConfig ayarlarınızı daha küçük profillere böetmenize olanak tanır. Örneğin, tüm cihazları etkileyen bir temel profil oluşturun. Daha sonra, bir cihaza özgü ayarları yapılandıran daha fazla profil oluşturun.

Ze, OEMConfig şeması da **eylemleri**kullanır. Eylemler, cihazda çalışan işlemlerdir. Ayarları yapılandırmaz. Dosya indirmeyi tetiklemek, Panoyu temizlemek ve daha fazlasını yapmak için bu eylemleri kullanın. Desteklenen eylemlerin tam listesi için bkz. [zeköşeli belgeleri](https://techdocs.zebra.com/oemconfig/10-0/about/) (zetaya 'nın Web sitesini açar).

Örneğin, cihaza bazı ayarlar uygulayan bir Zeköşeli OEMConfig profili oluşturursunuz. Başka bir Zeköşeli OEMConfig profili, Panoyu temizleyen bir eylem içerir. İlk profili bir Zeköşeli cihazlar grubuna atarsınız. Daha sonra bu cihazlarda panoyu temizlemeniz gerekir. İkinci profili, ilk profili değiştirmeden aynı aygıtlar grubuna atarsınız. Cihaz panosu, ilk profilde oluşturulan yapılandırma ayarlarını yeniden göndermeden veya etkilemeden temizlenir.

Başka bir örnekte, bazı Zeköşeli cihaz ayarlarını yapılandıran bir OEMConfig profili atadınız. Son olarak, kullanıcılar belirli bir uygulamayla ilgili sorunları bildiriyor ve uygulamanın önbelleğini temizlemek istiyorsunuz. Yalnızca "Önbelleği Temizle" eylemini içeren yeni bir OEMConfig profili oluşturun. Profili, ihtiyaç duyulan cihazlara atayın.

## <a name="ordering"></a>Sıralama

Her cihazda birden fazla profille, profillerin dağıtıldığı sıra garanti edilmez. Bu davranış Google Play kısıtlamadır. İşlemleri sırayla çalıştırmak için [zeköşeli 'ın Işlem adımı özelliğini](https://techdocs.zebra.com/oemconfig/10-0/mc/) kullanabilirsiniz (Zela 'nın Web sitesini açar). 

Özetlemek gerekirse, Eğer önemli bir sıralama ise [Zeköşeli Işlem adımı özelliğini](https://techdocs.zebra.com/oemconfig/10-0/mc/) kullanın (Zela 'nın Web sitesini açar). Sıralama ne olursa olsun, birden çok Intune profili kullanın. 

Bazı örneklere bakalım:

- Bu cihazlarda başka bir ayarı yapılandırmadan önce, tüm yeni kaydedilmiş Zeköşeli cihazlar için Bluetooth 'u açmak istiyorsunuz. İşlemleri sırayla çalıştırmak için Zeköşeli şeması 'ndaki **adımlar** özelliğini kullanın.

  İki Işlem adımını içeren bir Intune profili oluşturun. İlk adım Bluetooth ayarlarını içerir ve ikinci adım diğer ayarı yapılandırır. Zeucin OEMConfig uygulaması profili aldığında, adımları sırasıyla çalıştırır.

  Daha fazla bilgi için bkz. [zeköşeli işlem adımları](https://techdocs.zebra.com/oemconfig/10-0/mc/) (Zela 'nın Web sitesini açar).

- Tüm Zeköşeli cihazların saati 24 saat biçiminde görüntülemesini istiyorsunuz. Bu cihazların bazıları için kamerayı devre dışı bırakmak istiyorsunuz. Zaman ve kamera ayarları birbirlerine bağlı değildir.

  İki Intune profili oluşturun:

  - **Profil 1**: saati 24 saat biçiminde görüntüler. Pazartesi günü, bu profil **Tüm Zeköşeli AE cihazları** grubuna atanır.
  - **Profil 2**: kamerayı kapatır. Salı günü, bu profil **Zeköşeli AE Factory cihazları** grubuna atanır.

  Çarşamba 'da, Intune ile 10 yeni Zeköşeli cihaz kaydeder. Profil 1 ve profil 2 atanır. Yeni cihazlar Intune ile eşitlendikten sonra profilleri alırlar. Cihazlar profil 1 ' i almadan önce profil 2 alabilir.

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
