---
title: Microsoft Intune - Azure’da Windows 10 cihazlar için özel ayarlar ekleme | Microsoft Docs
description: Microsoft Intune’da Windows 10 çalıştıran cihazlar için OMA-URI ayarlarını kullanmak üzere özel bir profil ekleyin veya oluşturun. Özel ayarları eklemek için özel bir profil kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96074f4bea22b7468b1f210d631f0912eeafe7b5
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428984"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Intune’da Windows 10 cihazlar için özel ayarlar kullanma

Bu makalede, Windows 10 ve daha yeni cihazlarda denetleyebilmeniz için tüm farklı özel ayarlar listelenir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Intune 'da yerleşik olmayan ayarları yapılandırmak için bu ayarları kullanın.

Özel profiller hakkında daha fazla bilgi için bkz. [özel ayarlarla profil oluşturma](custom-settings-configure.md).

Bu ayarlar, Intune 'da bir cihaz yapılandırma profiline eklenir ve ardından Windows 10 cihazlarınıza atanır veya dağıtılır.

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri

Windows 10 özel profilleri, Open Mobile Alliance Tekdüzen Kaynak Tanımlayıcısı (OMA-URI) ayarlarını kullanarak farklı özellikleri yapılandırır. Bu ayarlar normalde mobil cihaz üreticileri tarafından cihazdaki özellikleri denetlemek için kullanılır.

Windows 10, [İlke Yapılandırma Hizmet Sağlayıcısı (İlke CSP’si)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers) gibi pek çok Yapılandırma Hizmeti Sağlayıcısı (CSP) ayarını kullanıma sunar.

Belirli bir ayarı arıyorsanız [Windows 10 cihaz kısıtlama profilinde](device-restrictions-windows-10.md) yerleşik olarak pek çok ayar bulunduğunu unutmayın. Bu sayede, özel değerler girmeniz gerekmeyebilir.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows 10 özel profili oluşturun](custom-settings-configure.md#create-the-profile).

## <a name="oma-uri-settings"></a>OMA-URI ayarları

**Ekle**: aşağıdaki ayarları girin:

- **Ad**: Ayarlar listesinde tanımanıza yardımcı olması için OMA-URI ayarına benzersiz bir ad girin.
- **Açıklama**: Ayara genel bir bakış sağlayan ve diğer önemli ayrıntıları veren bir açıklama girin.
- **OMA-URI ** (büyük/küçük harfe duyarlı): Ayar olarak kullanmak istediğiniz OMA-URI’yi girin.
- **Veri türü**: Bu OMA-URI ayarı için kullanacağınız veri türünü seçin. Seçenekleriniz şunlardır:

  - Base64 (dosya)
  - Boole
  - Dize (XML dosyası)
  - Tarih ve saat
  - Dize
  - Kayan nokta
  - Tamsayı

- **Değer**: Girdiğiniz OMA-URI ile ilişkilendirmek istediğiniz veri değerini girin. Değer, seçtiğiniz veri türüne bağlıdır. Örneğin, **Tarih ve saat**' i seçerseniz, bir tarih seçicisinden değeri seçin.

Bazı ayarları ekledikten sonra **Dışarı Aktar**’ı seçebilirsiniz. **Dışarı Aktar**, virgülle ayrılmış değerler (.csv) dosyasına eklediğiniz tüm değerlerin listesini oluşturur.

## <a name="find-the-policies-you-can-configure"></a>Yapılandırabileceğiniz ilkeleri bulma

[Yapılandırma hizmet sağlayıcısı başvurusu](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) konusunda, Windows 10’un desteklediği tüm yapılandırma hizmet sağlayıcılarının (CSP) tam listesi bulunur.

Tüm ayarlar, Windows 10 sürümlerinin tümüyle uyumlu değildir. [Yapılandırma hizmet sağlayıcısı başvurusu](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference), her bir CSP için hangi sürümlerin desteklendiğini açıklar.

Ayrıca Intune, [Yapılandırma hizmet sağlayıcısı başvurusu](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) konusundaki tüm ayarları desteklemez. İstediğiniz ayarı Intune’un destekleyip desteklemediğini öğrenmek için ilgili ayarın makalesini açın. Her ayar sayfası, desteklediği işlemi gösterir. Intune ile çalışmak için, ayarın **Add**, **Replace**ve **Get** işlemlerini desteklemesi gerekir. **Get** işlemi tarafından döndürülen değer **ekleme** veya **değiştirme** Işlemleri tarafından sağlanan değerle eşleşmiyorsa, Intune bir uyumluluk hatası bildirir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Intune 'da özel profiller hakkında daha fazla bilgi edinin](custom-settings-configure.md).
