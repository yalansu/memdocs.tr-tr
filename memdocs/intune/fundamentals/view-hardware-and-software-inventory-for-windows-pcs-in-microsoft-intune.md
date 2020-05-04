---
title: Windows bilgisayarları için donanım ve yazılım envanterini görüntüleme
titleSuffix: Microsoft Intune
description: Intune yazılım istemcisi ile bilgisayar olarak yönettiğiniz Windows masaüstü cihazlar hakkında donanım ve yazılım bilgilerini görüntüleme.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3c10f4c9-520b-4864-92fc-a45a9f640ad4
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e2d5e3f1e5839040c3ffd2229c34f3063a3ce87
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330130"
---
# <a name="view-hardware-and-software-inventory-for-windows-pcs"></a>Windows bilgisayarları için donanım ve yazılım envanterini görüntüleme

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Bu konudaki bilgiler, yalnızca Intune yazılım istemcisini kullanarak bilgisayar olarak yönettiğiniz Windows masaüstü cihazlar için geçerlidir. Mobil cihaz olarak kaydedilen Windows bilgisayarlarının envanterini görüntülemek istiyorsanız, bkz. [Intune 'da cihaz ayrıntılarını görüntüleme](../remote-actions/device-inventory.md).

Intune, Intune yazılım istemcisini kullanarak bilgisayar olarak yönettiğiniz masaüstleri için donanım ve yazılım hakkında ayrıntılı bilgiler toplar. Şunları oluşturmak için aşağıdaki yordamlardaki bilgileri kullanın:

- Yönettiğiniz bilgisayarların donanım özellikleri hakkında bilgi listeleyen bir rapor.

- Her bir bilgisayarda yüklü olan yazılımı listeleyen bir rapor.

- Rapordaki verilerin güncel olduğundan emin olmak için bir BILGISAYARıN envanterini yenileme.

## <a name="to-display-information-about-pcs-you-manage"></a>Yönettiğiniz bilgisayarlar hakkında bilgi görüntülemek için

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/) **raporlar** &gt; **bilgisayar envanteri raporları**' nı seçin.

2. **Yeni rapor oluştur** sayfasında, varsayılan değerleri kabul edin veya rapor tarafından döndürülecek sonuçları filtreleyecek şekilde özelleştirin. Örneğin, raporda yalnızca Windows 8.1 çalıştıran bilgisayarların görüntülendiğini seçebilirsiniz.

3. **Bilgisayar Envanteri Raporu**'nu yeni bir pencerede açmak için **Raporu Görüntüle**'yi seçin.

    Her sütunun başlığını seçerek raporu **Ad**, **Kasa Türü** veya **Üretici** gibi sütunlara göre sıralayabilirsiniz.

## <a name="to-display-software-installed-on-pcs-you-manage"></a>Yönettiğiniz bilgisayarlarda yüklü yazılımı görüntülemek için

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/) **raporlar** &gt; **algılanan yazılım raporları**' nı seçin.

2. **Yeni rapor oluştur** sayfasında, varsayılan değerleri kabul edin veya rapor tarafından döndürülecek sonuçları filtreleyecek şekilde özelleştirin. Örneğin, raporda yalnızca Microsoft tarafından yayınlanan yazılımı görüntülemeyi seçebilirsiniz.

3. **Algılanan Yazılım Raporu**'nu yeni bir pencerede açmak için **Raporu Görüntüle**'yi seçin.

    Her sütunun başlığını seçerek raporu **Ad**, **Yayımcı** veya **Kategori** gibi sütunlara göre sıralayabilirsiniz. Liste öğesinin yanındaki yön okunu seçerek daha fazla ayrıntı (örneğin yüklü olduğu bilgisayarlar) görmek için listedeki güncelleştirmeleri genişletebilirsiniz.

## <a name="to-refresh-computer-inventory-to-ensure-it-is-current"></a>Bilgisayar envanterinin güncel olduğundan emin olmak üzere yenilemek için

1. [Microsoft Intune yönetim konsolunda](https://manage.microsoft.com/)**Gruplar** &gt; **Tüm Cihazlar**’ı (veya envanterini yenilemek istediğiniz bilgisayarı içeren başka bir grubu) seçin.

2. Bir bilgisayar seçin veya **Ctrl** tuşunu basılı tutarak birden çok bilgisayarı seçin.

3. Görev çubuğunda, **uzak görevler** &gt; **envanteri Yenile**' yi seçin.

4. Görev durumunu görüntülemek için, sayfanın sağ alt köşesinde **Uzak Görevler**'i seçin.

    **Görev Durumu** iletişim kutusu geçerli uzak görevler, görev durumu, cihaz adı ve bildirilen hataları gösterir ve sorun giderme bilgilerine bir bağlantı sağlar.

## <a name="see-also"></a>Ayrıca bkz.

[Intune yazılım istemcisi ile genel Windows bilgisayar yönetim görevleri](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
