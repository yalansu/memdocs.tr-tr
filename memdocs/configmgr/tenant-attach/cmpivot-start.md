---
title: Kiracı ekli CMPivot Başlat (Önizleme)
titleSuffix: Configuration Manager
description: Microsoft Endpoint Manager kiracı ekli cihazlar için CMPivot 'i başlatın.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae6c0c83-2299-4463-958d-5555e3fcbdbe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 88fe50bd75fff73604c78125b0cd7599aa1afa4f
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564383"
---
# <a name="launch-cmpivot-from-the-admin-center-preview"></a><a name="bkmk_cmpivot"></a> Yönetim merkezinden CMPivot 'ı başlatın (Önizleme)

*Uygulama hedefi: Configuration Manager (geçerli dal)* 

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

<!--6024392-->
Şirket içi [CMPivot](../core/servers/manage/cmpivot.md) 'ın gücünü Microsoft Endpoint Manager yönetim merkezine taşıyın. Yardım masası gibi ek kişilerin buluttan, tek bir ConfigMgr tarafından yönetilen cihaza karşı gerçek zamanlı sorgular başlatabilmesini ve sonuçları yönetim merkezine geri döndürmesini sağlar. Bu, CMPivot 'in tüm geleneksel avantajlarından yararlanmanızı sağlar. Bu, BT yöneticilerinin ve diğer belirlenen kişilerin, ortamlarında cihazların durumunu hızlıca değerlendirebilme ve işlem yapması için sahip olduğu bir işlemdir.

## <a name="prerequisites"></a>Önkoşullar

Yönetim merkezinden CMPivot kullanmak için aşağıdaki öğeler gereklidir:

- [Kiracı iliştirme önkoşulları: ConfigMgr istemci ayrıntıları](client-details.md)
- [Güncelleştirme paketi](https://support.microsoft.com/help/4560496/) ve konsolun karşılık gelen sürümü yüklü olan en az sürüm 2002 Configuration Manager.
- Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.  
- Hedef istemciler en az PowerShell sürüm 4 gerektirir.
- Aşağıdaki varlıklar için veri toplamak üzere, hedef istemciler en az PowerShell sürüm 5,0 gerektirir:  
  - Yöneticiler
  - Bağlantı
  - Komutunu
  - SMBConfig

## <a name="permissions"></a>İzinler

Kullanıcı hesabının aşağıdaki izinleri olması gerekir:

- Configuration Manager içinde cihazın **koleksiyonu** için **okuma** izni.
- Configuration Manager **koleksiyondaki koleksiyonda** **CMPivot iznini Çalıştır**
- Azure AD 'de Configuration Manager Mikro hizmet uygulaması için **Yönetici Kullanıcı** rolü.
  - Azure AD 'deki rolü, **Enterprise applications**  >  **mikro hizmet**  >  **kullanıcıları ve grupları**  >  **Kullanıcı Ekle**' Configuration Manager kurumsal uygulamalardan ekleyin. Azure AD Premium varsa gruplar desteklenir.


## <a name="launch-cmpivot"></a><a name="bkmk_launch"></a> CMPivot Başlat

1. Bir tarayıcıda öğesine gidin [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. **Cihazlar** ve **tüm cihazlar**' ı seçin.
1. [Kiracı iliştirme](device-sync-actions.md)aracılığıyla Configuration Manager eşitlenen bir cihaz seçin.
1. **CMPivot (Önizleme)** öğesini seçin.
1. Komut dosyası bölmesine sorgunuzu yazın ve **Çalıştır**' ı seçin.

## <a name="close-cmpivot"></a>CMPivot kapat

CMPivot 'i kapatmak ve cihaz bilgilerine dönmek için, `X` CMPivot 'ın sağ üst köşesindeki simgeyi kullanın.

   :::image type="content" source="media/6024392-close-cmpivot.png" alt-text="Microsoft Endpoint Manager Yönetim Merkezi 'nde X simgesiyle CMPivot kapatma" lightbox="media/6024392-close-cmpivot.png":::

## <a name="next-steps"></a>Sonraki adımlar

- Sorgu örnekleri için bkz. [CMPivot Sample Scripts](cmpivot-samples-attached.md).
- CMPivot varlıkları, işleçleri ve işlevleri hakkında bilgi için bkz. [CMPivot Usage Overview](cmpivot-overview-attached.md).
- Yönetim merkezine yüklenen cihazlarda [CMPivot sorunlarını giderin](troubleshoot-cmpivot.md) .