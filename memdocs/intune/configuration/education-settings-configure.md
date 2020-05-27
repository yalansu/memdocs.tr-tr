---
title: Microsoft Intune-Azure 'da eğitim ayarları ekleme veya yapılandırma | Microsoft Docs
description: Microsoft Intune Windows 10 ve üzeri cihazlarda bir cihaz yapılandırma profilinde bir test yap uygulamasını kullanın. Eğitim ayarlarını kullanarak bir yapılandırma profili oluşturun ve bir test uygulaması URL 'SI girin, kullanıcıların oturum açma biçimini seçin, test sırasında ekranı izleyin ve test sırasında metin önerilerine izin verin veya bu önerileri önleyin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52eae65e6735ad655c2e8db53e34383ccc5e3b30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988392"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Microsoft Intune 'da Windows 10 cihazlarda bir test alma uygulaması kullanın

Intune 'da eğitim profilleri, öğrenciler için cihazlarda bir test veya sınava yönelik olarak tasarlanmıştır. Bu özellik bir test URL 'SI eklemek için **bir test** uygulaması ve ayarlar alma, son kullanıcıların teste nasıl oturum açmasını ve daha fazlasını içerir. Bu özellik aşağıdaki platformu destekler:

- Windows 10 ve üzeri

Kullanıcı oturum açtığında, bir test al uygulaması girdiğiniz test ile otomatik olarak açılır. Test devam ederken cihazda başka hiçbir uygulama çalıştırılamaz. [Windows 10 ' da testleri al](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) test alma uygulaması hakkında daha fazla bilgi sağlar.

Bu makalede Microsoft Intune ' de bir cihaz yapılandırma profili oluşturma adımları listelenir. Ayrıca, Windows 10 cihazlarınıza yönelik kullanılabilir eğitim ayarları hakkında bilgi almak ve bunları öğrenmek için bilgileri de içerir.

## <a name="create-a-device-profile"></a>Bir cihaz profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **Windows 10 ve üstünü**seçin.
    - **Profil**: **güvenli değerlendirme (eğitim)** seçeneğini belirleyin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: Yeni profil için açıklayıcı bir ad girin.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda, yapılandırmak istediğiniz ayarları girin:

    - [Windows 10 ve üzeri](education-settings-windows.md)

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya kullanıcı grubunu seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Her cihazın bir sonraki denetimi sırasında ilke uygulanır.

## <a name="next-steps"></a>Sonraki adımlar

[Windows 10 eğitim ayarlarının](education-settings-windows.md) ve açıklamalarının listesini görüntüleyin.

[Profil atandıktan](device-profile-assign.md)sonra [durumunu izleyin](device-profile-monitor.md).
