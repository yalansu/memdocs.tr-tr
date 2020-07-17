---
title: Kiracı iliştirme-Yönetim merkezinde ConfigMgr istemci ayrıntıları (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinden Configuration Manager cihazların istemci ayrıntılarını görüntüleyin.
ms.date: 07/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e8db4a7f877b5bd07f1aac76fc49b6efef31802e
ms.sourcegitcommit: 16bc2ed5b64eab7f5ae74391bd9d7b66c39d8ca6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86437435"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a>Kiracı iliştirme: Yönetim merkezinde ConfigMgr istemci ayrıntıları (Önizleme)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->

Artık Microsoft Endpoint Manager Yönetim Merkezi 'nde belirli bir cihaz için Koleksiyonlar, sınır grubu üyeliği ve gerçek zamanlı istemci bilgilerini içeren ConfigMgr istemci ayrıntılarını görebilirsiniz.

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.
> - Sınır grupları sekmesi yalnızca tek başına siteler için çalışır. Sekme, tek başına birincil site dışında herhangi bir şey için yönetim merkezinde boş olur.

## <a name="prerequisites"></a>Önkoşullar

- [Karşıya yüklenen cihazlara kiracı eklenmiş](device-sync-actions.md)bir ortam.
- Aşağıdaki tarayıcılardan biri:
  - Microsoft Edge, sürüm 77 ve üzeri
  - Google Chrome
- Kullanıcı hesabı hem [Azure Active Directory (Azure AD) Kullanıcı keşfi](https://docs.microsoft.com/mem/configmgr/core/servers/deploy/configure/about-discovery-methods#azureaddisc) hem de [Active Directory Kullanıcı keşfi](https://docs.microsoft.com/mem/configmgr/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)ile keşfedilmiştir.
  - Kullanıcı hesabının Azure 'da eşitlenmiş bir kullanıcı nesnesi olması gerektiği anlamına gelir.

## <a name="permissions"></a>İzinler

Kullanıcı hesabının aşağıdaki izinleri olması gerekir:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü.
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.

## <a name="view-configmgr-client-details"></a>ConfigMgr istemcisi ayrıntılarını görüntüle

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. **İstemci ayrıntılarını (Önizleme)** seçin.
   - Birincil site bir saat sonra aşağıdaki alanları güncelleştirir:
      - **Son ilke isteği**
      - **Son etkin saat**
      - **Son yönetim noktası**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Microsoft Endpoint Manager Yönetim Merkezi 'nde istemci ayrıntıları" lightbox="media/6024387-device-details.png":::

1. İstemcinin koleksiyonlarını listelemek için **koleksiyonları (Önizleme)** seçin.

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Microsoft Endpoint Manager Yönetim Merkezi 'nde istemci koleksiyonları" lightbox="media/6024387-device-collections.png":::

## <a name="next-steps"></a>Sonraki adımlar

[İstemci ayrıntıları sorunlarını giderme](troubleshoot-client-details.md)
