---
title: Microsoft Intune-Azure 'da paylaşılan veya çok kullanıcılı cihaz ayarları | Microsoft Docs
description: Microsoft Intune ' de birden çok kullanıcı tarafından paylaşılan veya kullanılan Windows 10 ve Windows holographic for Business cihazlarını ekleyin ve kullanın. Microsoft HoloLens dahil olmak üzere tüm ayarların ve cihazlarda ne yaptıkları hakkında bir liste görürsünüz. Konuk hesaplarını denetleme, hesapları yönetme ve etkin olmayan hesapları silme, yerel depolama alanına kaydetmeye izin verme veya bunu engelleme, güç ve uyku seçeneklerini ayarlama, güncelleştirmelerin ne zaman yükleneceğini seçme ve cihaz yapılandırma profilindeki eğitim ortamlarında cihazları kullanma.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1a11d9b41d17935d9c74490aabb5b983d04b4e1
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401515"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Intune kullanarak paylaşılan bılgısayar veya çok kullanıcılı cihazlarda erişimi, hesapları ve güç özelliklerini denetleme

Birden çok kullanıcısı olan cihazlara paylaşılan cihaz denir ve mobil cihaz yönetimi (MDM) çözümlerinin yaygın bir parçasıdır. Microsoft Intune kullanarak, aşağıdaki platformları çalıştıran paylaşılan cihazları özelleştirebilirsiniz:

- Windows 10 Professional ve üzeri
- Windows 10 Enterprise ve daha yeni
- Windows holographic for Business, HoloLens gibi

Örneğin, okulların genellikle birçok öğrenci tarafından kullanılan cihazları vardır. Bu ayar ile, okul Intune Yöneticisi paylaşılan bılgısayar özelliğini açıp tek seferde bir kullanıcıya izin verebilir. Öğrenciler cihazdaki farklı oturum açma hesapları arasında geçiş yapamıyor. Öğrenci oturumu kapattığında, kullanıcıya özgü tüm ayarları da kaldırmayı tercih edersiniz.

Son kullanıcılar, bu paylaşılan cihazlarda Konuk hesabıyla oturum açabilirler. Kullanıcılar oturum açtıktan sonra, kimlik bilgileri önbelleğe alınır. Cihaz kullandıkları için, son kullanıcılar yalnızca izin verilen özelliklere erişim sağlar. Örneğin, kullanıcıların dosyaları yerel olarak görüp kaydedebilen, güç yönetimi ayarlarını etkinleştirebilen veya devre dışı bırakabilen, cihazın uyku moduna geçme ve daha fazlasını tercih edebilirsiniz. Ayrıca, bir eşiğe ulaşıldığında, Konuk hesabının kullanıcı oturumunu kapattığında veya etkin olmayan hesapları sildiğinden de kontrol edersiniz.

Bu makalede bir yapılandırma profili oluşturma ve açıklamalarını içeren kullanılabilir ayarların bağlantılarını ekleme işlemlerinin nasıl yapılacağı gösterilir.

Profil Intune 'da oluşturulduğunda, profilinizi kuruluşunuzdaki cihaz gruplarına dağıtır veya atarsınız. Bu profili Ayrıca, karma cihaz türleri ve işletim sistemi (OS) sürümleriyle cihaz gruplarına da atayabilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

   - **Platform**: **Windows 10 ve üstünü**seçin.
   - **Profil**: **paylaşılan çok kullanıcılı cihaz**' ı seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

   - **Ad**: Yeni profil için açıklayıcı bir ad girin.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Windows 10 ve üzeri](shared-user-device-settings-windows.md)
    - [Windows 10 Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak cihazlar grubunu seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

    > [!NOTE]
    > Profili kuruluşunuzdaki cihaz gruplarına atadığınızdan emin olun.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Her cihazın bir sonraki denetimi sırasında ilke uygulanır.

## <a name="next-steps"></a>Sonraki adımlar

- [Windows 10 ve daha yeni](shared-user-device-settings-windows.md) ve [Windows holographic for Business](shared-user-device-settings-windows-holographic.md)için tüm ayarları görüntüleyin.
- [Profil atandıktan](device-profile-assign.md)sonra [durumunu izleyin](device-profile-monitor.md).
