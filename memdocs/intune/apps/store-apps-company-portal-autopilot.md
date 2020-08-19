---
title: Autopilot tarafından sağlanan cihazlar için Windows 10 Şirket Portalı uygulaması ekleme ve atama
titleSuffix: Microsoft Intune
description: Autopilot tarafından sağlanan cihazlar için Windows 10 Şirket Portalı uygulamasını ekleyin ve Intune 'a atayın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559530"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Autopilot tarafından sağlanan cihazlar için Windows 10 Şirket Portalı uygulaması ekleme ve atama

Cihazları yönetmek ve uygulamaları yüklemek için kullanıcılarınız Şirket Portalı uygulamasını kullanabilir. Windows 10 Şirket Portalı uygulamasını doğrudan Intune 'dan atayabilirsiniz. 

## <a name="prerequisites"></a>Ön koşullar

Windows 10 Autopilot tarafından sağlanan cihazlarda, Microsoft Store for Business hesabınızı Intune ile ilişkilendirmeniz önerilir. Daha fazla bilgi için bkz. [Microsoft Intune Ile iş için Microsoft Store toplu satın alınan uygulamaları yönetme](windows-store-for-business.md).

**Şirket portalı (çevrimdışı)** uygulamayı aşağıdaki adımları kullanarak yüklemeyi seçebilirsiniz. Şirket Portalı uygulaması, Autopilot grubuna atandığında cihaz bağlamına yüklenir ve Kullanıcı oturum açmadan önce cihaza yüklenir.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>Mağaza ayarlarını çevrimdışı uygulamayı gösterecek şekilde yapılandırma

1. [İş için Microsoft Store](https://www.microsoft.com/business-store)’da yönetici hesabınızla oturum açın.
2. Pencerenin üst kısmında **Yönet** sekmesini seçin.
3. Sol bölmede **Ayarlar**’ı seçin.
4. **Alışveriş deneyimi** altında **Çevrimdışı uygulamaları göster** seçeneğini **Açık** olarak ayarlayın.  
   Çevrimdışı lisanslı uygulamalar görüntülenir.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>Mağazadan çevrimdışı Şirket Portalı uygulamasını al

1. **Şirket Portalı** uygulamasını arayın ve seçin.
2. **Lisans türü** olarak **Çevrimdışı** ayarlayın.
3. Çevrimdışı Şirket Portalı uygulamasını almak ve envanterinize eklemek için **Uygulamayı al**’ı seçin.
   Uygulamanın Intune 'da listelenmesini sağlamak için, eşitleme zamanlamasının tamamlanmasını beklemeniz veya Microsoft Endpoint Manager yönetim merkezinden el ile eşitleme yapmanız gerekir.

## <a name="manually-sync-company-portal-app-with-intune"></a>Şirket Portalı uygulamasını Intune ile el ile eşitleme

1. Yönetici hesabınızla [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın   .
2. İş için **kiracı yönetim**  >  **bağlayıcıları ve belirteçleri**  >  **Microsoft Store**seçin.
3. **Etkinleştir**' e tıklayın.
4. Henüz yapmadıysanız İş İçin Microsoft Mağazası'na kaydolma bağlantısına tıklayın ve daha önce ayrıntı olarak açıklandığı gibi hesabınızı ilişkilendirin.
5. **Dil** açılan listesinden İş için Microsoft Store’dan alınan uygulamaların Azure portalında görüntülendiği dili seçin. Uygulamalar, görüntülendikleri dilden bağımsız olarak, mevcut olması durumunda son kullanıcının dilinde yüklenir.
6. Microsoft Mağazası’ndan satın aldığınız uygulamaları Intune’a almak için **Eşitle**’ye tıklayın.

## <a name="assign-the-company-portal-app"></a>Şirket Portalı uygulamasını atama

1. Yönetici hesabınızla [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın   .
2. **Uygulamalar**  >  **pencerelerini**seçin.
3. Windows uygulamaları listesinden **Şirket portalı (çevrimdışı)** öğesini seçin.
4. Şirket Portalı uygulamasını seçtiğiniz Autopilot cihaz gruplarına gerekli bir uygulama olarak [atayın](apps-deploy.md) .

## <a name="next-steps"></a>Sonraki adımlar

- Uygulama atama hakkında daha fazla bilgi için bkz. [uygulamaları gruplara atama](apps-deploy.md).

