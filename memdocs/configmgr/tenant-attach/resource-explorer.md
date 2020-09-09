---
title: Kiracı iliştirme-kaynak Gezgini Yönetim Merkezi (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinde kaynak Gezgini 'ni kullanarak karşıya yüklenen Configuration Manager cihazları için donanım envanterini görüntüleyin.
ms.date: 09/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: fabd91df79945580005e1c56893e78dec00d0202
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564358"
---
# <a name="tenant-attach-resource-explorer-in-the-admin-center-preview"></a><a name="bkmk_hinv"></a> Kiracı iliştirme: Yönetim merkezinde kaynak Gezgini (Önizleme)
<!--cm 6479284 in 7220536 pubpreview Sept 8, 2020-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Microsoft uç nokta Yönetimi yönetim merkezinden, kaynak Gezgini 'ni kullanarak karşıya yüklenen Configuration Manager cihazları için donanım envanterini görüntüleyebilirsiniz.

   :::image type="content" source="media/6479284-resource-explorer.png" alt-text="Microsoft Endpoint Manager Yönetim merkezinde kaynak Gezgini" lightbox="media/6479284-resource-explorer.png":::

## <a name="prerequisites"></a>Önkoşullar

Yönetim merkezinden kaynak Gezginini kullanmak için aşağıdaki öğeler gereklidir:

- [Kiracı iliştirme önkoşulları: ConfigMgr istemci ayrıntıları](client-details.md).
- En az Configuration Manager sürüm 2006 ve konsolun ilgili sürümü yüklü.
- Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.

## <a name="permissions"></a>İzinler

Kullanıcı hesabının aşağıdaki izinleri olması gerekir:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Configuration Manager içinde cihaz **koleksiyonu** Için **kaynak oku** izni.
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü.
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.

## <a name="launch-resource-explorer"></a><a name="bkmk_launch"></a> Kaynak Gezginini Başlat

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. Donanım envanterini görüntülemek için **Kaynak Gezgini 'ni (Önizleme)** seçin.
1. İstemciden bilgi almak için bir sınıf arayın veya seçin.

   :::image type="content" source="media/6479284-resource-explorer-details.png" alt-text="Ana kart sınıfı seçili kaynak Gezgini" lightbox="media/6479284-resource-explorer-details.png":::

## <a name="close-resource-explorer"></a>Kaynak Gezginini kapat

Kaynak Gezginini kapatmak ve cihaz bilgilerine dönmek için, `X` Kaynak Gezgini 'nin sağ üst köşesindeki simgeyi kullanın.

   :::image type="content" source="media/6479284-close-resource-explorer.png" alt-text="Kaynak Gezginini Microsoft Endpoint Manager Yönetim Merkezi 'nde x simgesiyle kapatma" lightbox="media/6479284-close-resource-explorer.png":::

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak Gezgini sorunlarını giderme](troubleshoot-resource-explorer.md)