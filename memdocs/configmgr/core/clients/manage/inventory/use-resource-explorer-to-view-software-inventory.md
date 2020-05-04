---
title: Kaynak Gezgini ile yazılım envanterini görüntüleme
titleSuffix: Configuration Manager
description: Configuration Manager ' de yazılım envanterini görüntülemek için Kaynak Gezgini kullanın.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710660"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Configuration Manager ' de yazılım envanterini görüntülemek için Kaynak Gezgini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hiyerarşinizdeki bilgisayarlardan toplanan yazılım envanteri hakkındaki bilgileri görüntülemek için Configuration Manager Kaynak Gezgini kullanın.  

> [!NOTE]  
>  Kaynak Gezgini, istemcide yazılım envanteri çevrimi çalıştırılıncaya kadar herhangi bir envanter verisi görüntülemez.  

 Kaynak Gezgini aşağıdaki yazılım envanteri bilgilerini sağlar:  

-   **Yazılım**:  

    -   **Toplanan dosyalar** -yazılım envanteri sırasında toplanan dosyalar.  

    -   **Dosya ayrıntıları** -yazılım envanteri sırasında envantere alınan ve belirli bir ürün veya üretici ile ilişkilendirilmemiş dosyalar.  

    -   **Son yazılım taraması** -istemci bilgisayar için son yazılım envanterinin ve dosya koleksiyonunun tarih ve saati.  

    -   **Ürün ayrıntıları** -yazılım envanteri tarafından stoğa alınan yazılım ürünleri, üreticiye göre gruplandırılır.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Kaynak Gezgini’ni Configuration Manager konsolundan çalıştırmak için  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** ' i seçin.

2.  **Varlıklar ve uyum** çalışma alanında, **cihazlar** ' ı seçin veya cihazları görüntüleyen herhangi bir koleksiyonu açın.  

3.  Görüntülemek istediğiniz envanteri içeren bilgisayarı seçin ve sonra **giriş** sekmesinde > **cihazlar** grubunda **Başlat** > **Kaynak Gezgini**' ı seçin.

4.  Kaynak Gezgini penceresinin sağ bölmesindeki herhangi bir öğeye sağ tıklayıp **Özellikler** ' i seçerek toplanan envanter bilgilerini daha okunabilir bir biçimde görüntüleyebilirsiniz.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Toplanan tanılama dosyalarını görüntüleyin ve yönetin

Configuration Manager sürüm 2002 ' den başlayarak, [istemci günlüklerini toplamak](../client-notification.md#client-diagnostics)için istemci bildirimini kullandığınızda toplanan dosyaları görüntülemek ve yönetmek için kaynak Gezgini kullanın. 

1. **Cihazlar** düğümünden, günlüklerini görüntülemek istediğiniz cihaza sağ tıklayın.
1. **Başlat**' ı ve ardından **Kaynak Gezgini**' yi seçin.
1. **Kaynak Gezgini**, **Tanılama dosyaları**' na tıklayın.
1. **Tanılama dosyaları** listesinde, dosyalar için koleksiyon tarihini görebilirsiniz. İstemci günlüklerinin ad biçimi `Support_<guid>.zip`.
1. ZIP dosyasına sağ tıklayın ve aşağıdaki seçeneklerden birini belirleyin:
    - **Destek merkezini açın**: [destek merkezini](../../../support/support-center.md)başlatır.
    - **Kopyala**: satır bilgilerini kaynak Gezgini kopyalar.
    - **Dosyayı görüntüle**: ZIP dosyasının dosya Gezgini ile bulunduğu klasörü açar.
    - **Kaydet**: seçili dosya Için dosya Kaydet iletişim kutusunu açar.
    - **Dışarı aktar**: **tanılama dosyalarında**gösterilen kaynak Gezgini sütunlarını kaydeder.
    - **Yenile**: dosya listesini yeniler.
    - **Özellikler**: seçili dosyadaki özellikleri döndürür. 

[![Kaynak Gezgini istemci günlüklerini gözden geçirin ve kaydedin](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Sonraki adımlar

Toplanan tanılama dosyalarını görüntülemek için [destek merkezini kullanın](../../../support/support-center.md) .
