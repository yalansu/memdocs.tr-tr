---
title: Microsoft Intune-Azure 'da ilke kullanarak cihaz özelliklerini kısıtlama | Microsoft Docs
description: Android Cihaz Yöneticisi, Android kurumsal, macOS, iOS, Idos, Windows Phone ve Windows 10 cihazlarındaki özellikleri Microsoft Intune kısıtlamak için bir cihaz profili ekleyin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 470ca47aa92b30acacc8a251c6d7d1741513bdf1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359223"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Microsoft Intune’da cihaz kısıtlama ayarlarını yapılandırma

Intune, yöneticilerin Android, iOS/ıpados, macOS ve Windows cihazlarını denetlemesine yardımcı olan cihaz kısıtlama ilkeleri içerir. Bu kısıtlamalar, kuruluşunuzun kaynaklarını korumak için çok çeşitli ayarları ve özellikleri denetlemenize olanak tanır. Örneğin, yöneticiler şunları yapabilir:

- Cihaz kamerasına izin verin veya kamerayı engelleyin.
- Google Play, uygulama mağazalarına erişimi denetleme, belgeleri ve oyunları görüntüleme.
- Yerleşik uygulamaları engelleyin veya izin verilen ya da yasaklanmış uygulamaların bir listesini oluşturun.
- Dosyaların bulut ve depolama hesaplarına yedeklenmesini sağlar veya engelleyin.
- En az parola uzunluğu ayarlayın ve basit parolaları engelleyin.

Bu özellikler Intune 'da kullanılabilir ve yönetici tarafından yapılandırılabilir. Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profile ekledikten sonra, profili kuruluşunuzdaki cihazlara gönderebilir veya dağıtabilirsiniz.

Bu makalede bir cihaz kısıtlama profili oluşturma yöntemi gösterilmektedir. Farklı platformlar için kullanılabilir tüm ayarları da görebilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:  

        - **Android Cihaz Yöneticisi**
        - **Android Kurumsal**
        - **iOS/ıpados**
        - **macOS**
        - **Windows 10 ve üzeri**
        - **Windows 8.1 ve üzeri**
        - **Windows Phone 8.1**

    - **Profil**: **cihaz kısıtlamalarını**seçin.

        Windows 10 Team cihazları için Surface Hub gibi bir cihaz kısıtlama profili oluşturmak için, **cihaz kısıtlamaları (Windows 10 ekibi)** öğesini seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **iOS/ıpados: cihazlarda kamera blok**' dır.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**'yi seçin.

7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android Cihaz Yöneticisi](device-restrictions-android.md)
    - [Android Kurumsal](device-restrictions-android-for-work.md)
    - [iOS/ıpados](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 ve üzeri](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. **İleri**'yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili `US-NC IT Team` veya `JohnGlenn_ITDepartment`gıbı belirli BT gruplarına filtrelemek için bir etiket atayın. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**'yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**'yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduktan sonra atanmak için hazırlanın. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
