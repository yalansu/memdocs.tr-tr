---
title: Microsoft Intune-Azure 'da Windows ve holographic cihazları için bilgi noktası ayarları | Microsoft Docs
description: Windows 10 (ve üzeri) ve Windows holographic for Business cihazlarınızı tek uygulamayla ve çok kullanıcılı bilgi olarak yapılandırın, Başlat menüsünü özelleştirin, uygulamalar ekleyin, görev çubuğunu görüntüleyin ve Microsoft Intune bir Web tarayıcısı yapılandırın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 778ce3e6d069347522a98977da65d651e059e41c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327392"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Intune kullanarak adanmış bir bilgi noktası olarak çalışacak Windows 10 ve Windows holographic for Business cihaz ayarları

Windows 10 cihazlarında, cihazları bir bilgi noktası olarak çalıştırmak için Intune 'u kullanın, bazen adanmış bir cihaz olarak bilinir. Bilgi noktası modundaki bir cihaz bir uygulama çalıştırabilir veya birçok uygulama çalıştırabilir. Bir başlangıç menüsünü gösterebilir ve özelleştirebilir, Win32 uygulamaları dahil farklı uygulamalar ekleyebilir, bir Web tarayıcısına belirli bir giriş sayfası ekleyebilir ve daha fazlasını yapabilirsiniz. 

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri
- Windows 10 Holographic for Business

Diğer platformlar için bilgi noktası profilleri oluşturmak için bkz. [Android Cihaz Yöneticisi](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings)ve [iOS/ıpados](device-restrictions-ios.md#kiosk).

Intune, cihaz başına bir bilgi noktası profili destekler. Tek bir cihazda birden fazla bilgi noktası profiline ihtiyacınız varsa bir [Özel OMA-URI](custom-settings-windows-10.md) kullanabilirsiniz.

Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profilde ekledikten sonra bu ayarları kuruluşunuzdaki gruplara gönderin veya dağıtın.

Bu makalede bir cihaz yapılandırma profili oluşturma konusu gösterilmektedir. Tüm ayarların bir listesi ve ne yapacaklarınız için bkz. [Windows 10 bilgi noktası ayarları](kiosk-settings-windows.md) ve [Windows holographic for Business bilgi noktası ayarları](kiosk-settings-holographic.md).

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

   - **Ad**: Yeni profil için açıklayıcı bir ad girin.
   - **Açıklama**: Profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
   - **Platform**: **Windows 10 ve üzeri**’ni seçin
   - **Profil türü**: **bilgi noktası** seçin

4. **Ayarlar**' da bir **bilgi noktası modu**seçin. **Bilgi noktası modu**, ilke tarafından desteklenen bilgi noktası modu türünü belirler. Şu seçenekler mevcuttur:

    - **Yapılandırılmamış** (varsayılan): İlke, bilgi noktası modunu etkinleştirmez.
    - **Tekli uygulama, tam ekran bilgi noktası**: Cihaz tek kullanıcı hesabı olarak çalışır ve tek bir Mağaza uygulamasına kilitlenir. Dolayısıyla kullanıcı oturum açtığında belirli bir uygulama başlar. Bu mod ayrıca kullanıcının yeni uygulamalar açmasını veya çalışan uygulamayı değiştirmesini önler.
    - **Çoklu uygulama bilgi noktası**: Cihaz, Uygulama Kullanıcı Modeli Kimliği (AUMID) kullanarak birden fazla Store, Win32 veya Windows uygulaması çalıştırır. Cihazda yalnızca eklediğiniz uygulamalar kullanılabilir.

        Çok uygulamalı bilgi noktasının veya sabit amaçlı cihazın yararı, yalnızca ihtiyaç duyulan uygulamalara erişim sağlayarak kullanıcılara anlaşılması kolay bir deneyim sunmasıdır. Ayrıca, Ayrıca, kullanıcıların ihtiyaç duydukları uygulamaları görüntüleyebilecekleri şekilde kaldırabilirsiniz.

    Tüm ayarların bir listesi ve ne yapacaklarınız için, bkz.:
      - [Windows 10 bilgi noktası ayarları](kiosk-settings-windows.md)
      - [Windows holographic for Business bilgi noktası ayarları](kiosk-settings-holographic.md)

5. İşiniz bittiğinde **Tamam** > **Oluştur**’u seçerek değişikliklerinizi kaydedin.

Profil oluşturulur ve profiller listesinde gösterilir. Sonra, profili [atayın](device-profile-assign.md) .

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

Aşağıdaki platformları çalıştıran cihazlar için bilgi noktası profilleri oluşturabilirsiniz:

- [Android Cihaz Yöneticisi](device-restrictions-android.md#kiosk)
- [Android Kurumsal](device-restrictions-android-for-work.md#dedicated-device-settings)
- [iOS/ıpados](device-restrictions-ios.md#kiosk)
- [Windows 10 ve üzeri](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
