---
title: Microsoft Intune-Azure 'da Windows 10 için etki alanına ekleme profili ayarları | Microsoft Docs
description: Karma Azure AD 'ye katılmış cihazlar için bir etki alanına katılma cihaz yapılandırma profili oluşturun. Windows Autopilot ve Microsoft Intune ile sağlanan cihazlara şirket içi Active Directory etki alanı bilgilerini dağıtmak için bu profili kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/31/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8285b15a3fd7d473641ce9480fe1e6522b54e814
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281107"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Microsoft Intune 'de karma Azure AD 'ye katılmış cihazlar için yapılandırma etki alanına katılma ayarları

Birçok ortam şirket içi Active Directory (AD) kullanır. AD etki alanına katılmış cihazlar aynı zamanda Azure AD 'ye katıldığında, karma Azure AD 'ye katılmış cihazlar olarak adlandırılırlar. Windows Autopilot kullanarak, [karma Azure AD 'ye katılmış cihazları](../../autopilot/windows-autopilot-hybrid.md) Intune 'a kaydedebilirsiniz. Kaydolmak için bir **etki alanına katılması** yapılandırma profiline de ihtiyacınız vardır.

**Etki alanına katılması** yapılandırma profili şirket içi Active Directory etki alanı bilgilerini içerir. Cihazlar sağlanırken (ve genellikle çevrimdışı), bu profil, cihazların hangi şirket içi etki alanına katılabileceklerini bilmesi için AD etki alanı ayrıntılarını dağıtır. Etki alanına ilişkin bir profil oluşturmazsanız bu cihazların dağıtımı başarısız olabilir.

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri
- Hibrit Azure AD’ye katılmış cihazlar
- Autopilot + Intune ile karma dağıtım

Bu makalede, karma Autopilot dağıtımı için bir etki alanı ekleme profili oluşturma gösterilmektedir. Kullanılabilir ayarları da görebilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **Windows 10 ve üstünü**seçin.
    - **Profil**: **etki alanına katılmayı (Önizleme)** seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **Windows 10: karma ad 'ye katılmış cihazları Windows Autopilot 'e kaydetmek için şirket içi etki alanı bilgilerini Içeren etki alanına katılma profilidir**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda, aşağıdaki özellikleri girin:

    - **Bilgisayar adı ön eki**: Cihaz adı için bir ön ek girin. Bilgisayar adları 15 karakter uzunluğundadır. Ön ek sonrasında, kalan 15 karakter rastgele oluşturulur.
    - **Etki alanı adı**: cihazların katılabileceği tam etki alanı adını (FQDN) girin. Örneğin, şunu girin `americas.corp.contoso.com.`
    - **Kuruluş birimi** (isteğe bağlı): bilgisayar hesaplarının oluşturulacağı kuruluş BIRIMI (OU) için tam yolu ([ayırt edici ad](/windows/win32/ad/object-names-and-identities#distinguished-name)) girin. Örneğin, `"CN=Users,DC=Contoso,DC=com"` girin. Değer girmezseniz, iyi bilinen bir bilgisayar nesne kapsayıcısı kullanılır.

      Bu ayar hakkında daha fazla bilgi ve öneri için bkz. [karma Azure AD 'ye katılmış cihazları dağıtma](../../autopilot/windows-autopilot-hybrid.md).

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak cihaz gruplarını seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    Cihazları farklı etki alanlarına veya OU 'Lara katılmanız gerekirse farklı cihaz grupları oluşturun.

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Artık [Intune ve Windows Autopilot kullanarak karma Azure AD 'ye katılmış cihazları dağıtmanıza](../../autopilot/windows-autopilot-hybrid.md)hazırdır.

## <a name="next-steps"></a>Sonraki adımlar

Profil [atandıktan](device-profile-assign.md)sonra [durumunu izleyin](device-profile-monitor.md).

[Intune ve Windows Autopilot kullanarak karma Azure AD 'ye katılmış cihazları dağıtın](../../autopilot/windows-autopilot-hybrid.md).
