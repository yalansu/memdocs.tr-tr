---
title: Microsoft Intune - Azure’da Windows Phone 8.1 cihazlara özel ayarlar ekleme | Microsoft Docs
titleSuffix: ''
description: Microsoft Intune’da Windows Phone 8.1 çalıştıran cihazlar için OMA-URI ayarlarını kullanmak üzere özel bir profil ekleyin veya oluşturun.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0adb573dbb40f00a1b43b9fb356cdc20b97b669
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910086"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Intune’da Windows Phone 8.1 cihazlar için özel ayarlar kullanma

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Microsoft Intune’u kullanarak, “özel profiller” kullanan Windows Phone 8.1 cihazlarınız için özel ayarlar ekleyebilir veya oluşturabilirsiniz. Özel profiller, bir Intune özelliğidir. Intune’da yerleşik olarak bulunmayan cihaz ayarları ve özelliklerini eklemek için tasarlanmıştır.

Windows Phone 8.1 özel profilleri, Open Mobile Alliance Tekdüzen Kaynak Tanımlayıcısı (OMA-URI) ayarlarını kullanarak farklı özellikleri yapılandırır. Bu ayarlar normalde mobil cihaz üreticileri tarafından cihazdaki özellikleri denetlemek için kullanılır. [Windows Phone 8,1 MDM Protokolü belgeleri](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) ayarları listeler.

Bu makale, Windows Phone 8.1 cihazlar için özel profil oluşturma işlemini gösterir. 

## <a name="before-you-begin"></a>Başlamadan önce

[Windows Phone 8,1 özel profili oluşturun](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Özel OMA-URI ayarları

- **OMA-URI ayarları**: aşağıdaki ayarları **ekleyin** :

  - **Ad**: Ayarlar listesinde tanımanıza yardımcı olması için OMA-URI ayarına benzersiz bir ad girin.
  - **Açıklama**: Ayara genel bir bakış sağlayan ve profili bulmanıza yardımcı olacak diğer ek bilgileri içeren bir açıklama girin.
  - **OMA-URI ** (büyük/küçük harfe duyarlı): Ayar olarak kullanmak istediğiniz OMA-URI’yi girin.
  - **Veri türü**: Bu OMA-URI ayarı için kullanacağınız veri türünü seçin. Seçenekleriniz şunlardır:

    - Dize
    - Dize (XML dosyası)
    - Tarih ve saat
    - Tamsayı
    - Kayan nokta
    - Boole
    - Base64 (dosya)

  - **Değer**: Girdiğiniz OMA-URI ile ilişkilendirmek istediğiniz veri değerini girin. Değer, seçtiğiniz veri türüne bağlıdır. Örneğin, **Tarih ve saat**' i seçerseniz, bir tarih seçicisinden değeri seçin.

  Bazı ayarları ekledikten sonra **Dışarı Aktar**’ı seçebilirsiniz. **Dışarı Aktar**, virgülle ayrılmış değerler (.csv) dosyasına eklediğiniz tüm değerlerin listesini oluşturur.

## <a name="example"></a>Örnek

Aşağıdaki örnekte, Windows 8.1 telefon cihazlarının taşıyıcı kapsam alanı dışına geçiş yaparken hücresel ağların değiştirilmesi engellenir.

- **Ad**: hücresel veri dolaşımına izin ver
- **Açıklama**: hücresel veri dolaşımına izin ver veya izin verme
- **OMA-URI** (büyük/küçük harfe duyarlı):./Vendor/MSFT/PolicyManager/My/connectivity/AllowCellularDataRoaming
- **Veri türü**: tamsayı
- **Değer**: 0

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Windows 10 cihazlarında özel bir profil](custom-settings-windows-10.md)oluşturun.