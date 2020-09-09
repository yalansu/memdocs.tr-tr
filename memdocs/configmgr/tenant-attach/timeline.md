---
title: Kiracı iliştirme-cihaz zaman çizelgesi (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinden Configuration Manager cihazların zaman çizelgesini görüntüleyin.
ms.date: 09/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: b2d914d8-6714-4fa1-9e14-0046b77e6b40
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5065e893a8670911c055910889e8fbae472bfc4c
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564391"
---
# <a name="tenant-attach-device-timeline-in-the-admin-center-preview"></a><a name="bkmk_timeline"></a> Kiracı iliştirme: Yönetim merkezinde cihaz zaman çizelgesi (Önizleme)
<!--CM7141381, IN7552762 pubpreview Sept 8, 2020-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Configuration Manager, kiracı iliştirme aracılığıyla bir cihazı Microsoft Uç Nokta Yöneticisi ile eşitlediğinde, olayların zaman çizelgesini görebilirsiniz. Bu zaman çizelgesi, cihazdaki sorunları gidermenize yardımcı olabilecek geçmiş etkinlikleri gösterir.

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

## <a name="prerequisites"></a>Önkoşullar

Yönetim merkezinde zaman çizelgesini kullanmak için aşağıdaki öğeler gereklidir:

- [Kiracı iliştirme önkoşulları: ConfigMgr istemci ayrıntıları](client-details.md#prerequisites).
- [Güncelleştirme paketi](https://support.microsoft.com/help/4560496/) ve konsolun karşılık gelen sürümü yüklü olan en az sürüm 2002 Configuration Manager.
- Configuration Manager 'de Endpoint Analytics veri toplamayı etkinleştir:
   1. Configuration Manager konsolunda, **Yönetim**  >  **istemci ayarları**  >  **varsayılan istemci ayarları**' na gidin.
   1. Sağ tıklayın ve **Özellikler** ' i seçin ve ardından **Bilgisayar Aracısı** ayarları ' nı seçin.
   1. **Endpoint Analytics veri toplamayı etkinleştir** ayarını **Evet**olarak belirleyin.
      - Yalnızca istemci bu ilkeyi aldıktan sonra toplanan olaylar Yönetim merkezinde görünür olur. İlkeyi almadan önce olaylara erişilemez.

## <a name="permissions"></a>İzinler

Kullanıcı hesabının aşağıdaki izinleri olması gerekir:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Configuration Manager içinde **koleksiyon** altında **kaynağı oku** izni.
- Configuration Manager içinde **koleksiyon** altında **kaynağı bilgilendir** izni. <!--7984188-->
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü.
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.

## <a name="generate-events"></a>Olay oluşturma

Cihazlar, olayları günde bir kez yönetim merkezine gönderir. Yalnızca istemci, **Endpoint Analytics verilerini etkinleştirme** ilkesini aldıktan sonra toplanan olaylar Yönetim merkezinde görünür. Configuration Manager bir uygulama veya güncelleştirme yükleyerek test olaylarını kolayca oluşturun veya cihazı yeniden başlatın. Olaylar 30 gün boyunca tutulur. Toplanan olayları görüntülemek için [grafiği](#collected-events) kullanın.

## <a name="collected-events"></a>Toplanan olaylar

|Olay adı|Sağlayıcı adı|Olay Kimliği|
|---|---|---|
|Uygulama hatası|Uygulama hatası|1000|
|Uygulama askıda kalıyor|Uygulama askıda kalıyor|1002|
|Çekirdek kilitlenme|Microsoft-Windows-WER-SystemErrorReporting|1001|
|Uygulama kilitlenmesi|Windows Hata Bildirimi|1001|
|Windows Update Aracısı – yüklemeyi Güncelleştir|Microsoft-Windows-WindowsUpdateClient|19|
|Bilinmeyen kapalı|Önyükleme|0|
|Başlatılan kapatmalar|Önyükleme|1074|
|Olağan dışı kapatmalar|Önyükleme|41|
|Sınır grubu değişikliği|Microsoft-ConfigMgr|20000|
|Uygulama Dağıtımı|Microsoft-ConfigMgr|20001|
|Configuration Manager – yüklemeyi Güncelleştir|Microsoft-ConfigMgr|20002|
|Üretici yazılımı sürümü değişikliği|Microsoft-ConfigMgr|20003|

## <a name="view-the-timeline"></a>Zaman çizelgesini görüntüleme

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. **Zaman çizelgesini**seçin. Varsayılan olarak, son 24 saatin olayları gösterilir.
   - **Zaman aralığını**, **olay düzeylerini**ve **sağlayıcı adını**değiştirmek için **filtre** düğmesini kullanın.
   - Bir olayda seçerseniz, bunun ayrıntılı iletisini görürsünüz.
   - İstemcide oluşturulan son verileri getirmek için **Eşitle** ' yi seçin. Cihaz, varsayılan olarak bir gün sonra yönetim merkezine olayları gönderir. <!--7984188-->
   - Sayfayı yeniden yüklemek ve yeni toplanan olayları görmek için **Yenile** ' yi seçin.

   :::image type="content" source="./media/7141381-timeline.png" alt-text="Bir cihaz için olay zaman çizelgesi" lightbox="./media/7141381-timeline.png":::

## <a name="next-steps"></a>Sonraki adımlar

[Cihaz zaman çizelgesinde sorun giderme](troubleshoot-timeline.md)