---
title: Bir cihaza uygulama yükleme
titleSuffix: Configuration Manager
description: Bir uygulamayı bir koleksiyon olmadan hemen bir cihaza yüklemek için Configuration Manager kullanın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710226"
---
# <a name="install-applications-for-a-device"></a>Bir cihaza uygulama yükleme

<!--4402180-->

Sürüm 1906 ' den başlayarak, Configuration Manager konsolundan, uygulamaları bir cihaza gerçek zamanlı olarak yükleyebilirsiniz. Bu özellik, her uygulama için ayrı koleksiyonlar gereksinimini azaltmaya yardımcı olabilir.

## <a name="prerequisites"></a>Önkoşullar

- [İsteğe bağlı özelliği](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **cihaz başına Kullanıcı için uygulama isteklerini Onayla**' yı etkinleştirin.  

- [Uygulamayı](deploy-applications.md) bir cihaz koleksiyonuna *kullanılabilir* olarak dağıtın.  

    - Dağıtım sihirbazının **dağıtım ayarları** sayfasında, aşağıdaki seçeneği belirleyin: **bir yöneticinin cihazdaki bu uygulama için bir isteği onaylaması gerekir**.  

        > [!Note]  
        > Bu dağıtım ayarlarıyla, istemciye hiçbir ilke gönderilmez. Uygulama, yazılım merkezi 'nde kullanılabilir olarak gösterilmez ve Kullanıcı uygulamayı Bu dağıtıma yükleyemez. Uygulamayı yüklemek için bu eylemi kullandıktan sonra Kullanıcı onu çalıştırabilir ve yazılım merkezi 'nde yükleme durumunu görebilirler.

- Kullanıcı hesabınız için aşağıdaki izinler gerekir:

    - **Uygulama**: okuma, onaylama

    - **Koleksiyon**: oku, kaynağı oku, kaynağı değiştir, toplanan dosyayı görüntüle

    Örneğin, **Uygulama Yöneticisi** yerleşik rolü bu izinlere sahiptir.

> [!TIP]
> Hiyerarşide, uygulama ve dağıtım bilgilerinin hedef istemcinin atandığı birincil siteye çoğaltılmasını bekleyin.<!-- SCCMDocs#2113 -->

## <a name="process"></a>İşleme

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Hedef cihazı seçin ve ardından şeritte **uygulamayı Install** eylemini seçin.

1. Listeden bir veya daha fazla uygulama seçin. Liste yalnızca önkoşul ayarlarıyla zaten dağıttığınız uygulamaları gösterir.

Bu eylem, seçili önceden dağıtılan uygulamaların yüklenmesini cihazda tetikler.

Onay isteğinin durumunu görmek için, **yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **Uygulama istekleri** düğümünü seçin.

Uygulama yüklemesini, **izleme** çalışma alanının **dağıtımlar** düğümündeki her zamanki gibi izleyin.


## <a name="see-also"></a>Ayrıca bkz.

[Uygulamaları onaylama](app-approval.md)
