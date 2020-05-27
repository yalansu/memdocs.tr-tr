---
title: Microsoft Intune-Azure 'da Windows ve holographic cihazları için bilgi noktası ayarları | Microsoft Docs
description: Windows 10 (ve üzeri) ve Windows holographic for Business cihazlarınızı tek uygulamayla ve çok kullanıcılı bilgi olarak yapılandırın, Başlat menüsünü özelleştirin, uygulamalar ekleyin, görev çubuğunu görüntüleyin ve Microsoft Intune bir Web tarayıcısı yapılandırın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9be644a47a361cf29e7b7132b2c87a4921553ea
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989436"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Intune kullanarak adanmış bir bilgi noktası olarak çalışacak Windows 10 ve Windows holographic for Business cihaz ayarları

Windows 10 cihazlarında, cihazları bir bilgi noktası olarak çalıştırmak için Intune 'u kullanın, bazen adanmış bir cihaz olarak bilinir. Bilgi noktası modundaki bir cihaz bir uygulama çalıştırabilir veya birçok uygulama çalıştırabilir. Bir başlangıç menüsünü gösterebilir ve özelleştirebilir, Win32 uygulamaları dahil farklı uygulamalar ekleyebilir, bir Web tarayıcısına belirli bir giriş sayfası ekleyebilir ve daha fazlasını yapabilirsiniz. 

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri
- Windows 10 Holographic for Business

Diğer platformlar için bilgi noktası profilleri oluşturmak için bkz. [Android Cihaz Yöneticisi](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)ve [iOS/ıpados](device-restrictions-ios.md#kiosk).

Intune, cihaz başına bir bilgi noktası profili destekler. Tek bir cihazda birden fazla bilgi noktası profiline ihtiyacınız varsa bir [Özel OMA-URI](custom-settings-windows-10.md) kullanabilirsiniz.

Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profilde ekledikten sonra bu ayarları kuruluşunuzdaki gruplara gönderin veya dağıtın.

Bu makalede bir cihaz yapılandırma profili oluşturma konusu gösterilmektedir. Tüm ayarların bir listesi ve ne yapacaklarınız için bkz. [Windows 10 bilgi noktası ayarları](kiosk-settings-windows.md) ve [Windows holographic for Business bilgi noktası ayarları](kiosk-settings-holographic.md).

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

   - **Platform**: **Windows 10 ve üstünü**seçin.
   - **Profil**: **bilgi noktası**seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

   - **Ad**: Yeni profil için açıklayıcı bir ad girin.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda  >  **bir bilgi noktası modu seçin**, ilke tarafından desteklenen bilgi noktası modu türünü seçin. Seçeneklere şunlar dahildir:

    - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. İlke bilgi noktası modunu etkinleştirmez.
    - **Tekli uygulama, tam ekran bilgi noktası**: Cihaz tek kullanıcı hesabı olarak çalışır ve tek bir Mağaza uygulamasına kilitlenir. Dolayısıyla kullanıcı oturum açtığında belirli bir uygulama başlar. Bu mod ayrıca kullanıcının yeni uygulamalar açmasını veya çalışan uygulamayı değiştirmesini önler.
    - **Çoklu uygulama bilgi noktası**: Cihaz, Uygulama Kullanıcı Modeli Kimliği (AUMID) kullanarak birden fazla Store, Win32 veya Windows uygulaması çalıştırır. Cihazda yalnızca eklediğiniz uygulamalar kullanılabilir.

        Çok uygulamalı bilgi noktasının veya sabit amaçlı cihazın yararı, yalnızca ihtiyaç duyulan uygulamalara erişim sağlayarak kullanıcılara anlaşılması kolay bir deneyim sunmasıdır. Ayrıca, Ayrıca, kullanıcıların ihtiyaç duydukları uygulamaları görüntüleyebilecekleri şekilde kaldırabilirsiniz.

    Tüm ayarların bir listesi ve ne yapacaklarınız için, bkz.:

      - [Windows 10 kiosk ayarları](kiosk-settings-windows.md)
      - [Windows holographic for Business bilgi noktası ayarları](kiosk-settings-holographic.md)

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya kullanıcı grubunu seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Her cihazın bir sonraki denetimi sırasında ilke uygulanır.

## <a name="next-steps"></a>Sonraki adımlar

[Profil atandıktan](device-profile-assign.md)sonra [durumunu izleyin](device-profile-monitor.md).

Aşağıdaki platformları çalıştıran cihazlar için bilgi noktası profilleri oluşturabilirsiniz:

- [Android cihaz yöneticisi](device-restrictions-android.md#kiosk)
- [Android Kurumsal](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 ve üzeri](kiosk-settings-windows.md)
- [Windows 10 Holographic for Business](kiosk-settings-holographic.md)
