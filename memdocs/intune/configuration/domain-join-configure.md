---
title: Microsoft Intune-Azure 'da Windows 10 için etki alanına ekleme profili ayarları | Microsoft Docs
description: Karma Azure AD 'ye katılmış cihazlar için bir etki alanına katılma cihaz yapılandırma profili oluşturun. Windows Autopilot ve Microsoft Intune ile sağlanan cihazlara şirket içi Active Directory etki alanı bilgilerini dağıtmak için bu profili kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333114"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Microsoft Intune 'de karma Azure AD 'ye katılmış cihazlar için yapılandırma etki alanına katılma ayarları

Birçok ortam şirket içi Active Directory (AD) kullanır. AD etki alanına katılmış cihazlar aynı zamanda Azure AD 'ye katıldığında, karma Azure AD 'ye katılmış cihazlar olarak adlandırılırlar. Windows Autopilot kullanarak, [karma Azure AD 'ye katılmış cihazları](../enrollment/windows-autopilot-hybrid.md) Intune 'a kaydedebilirsiniz. Kaydolmak için bir **etki alanına katılması** yapılandırma profiline de ihtiyacınız vardır.

**Etki alanına katılması** yapılandırma profili şirket içi Active Directory etki alanı bilgilerini içerir. Cihazlar sağlanırken (ve genellikle çevrimdışı), bu profil, cihazların hangi şirket içi etki alanına katılabileceklerini bilmesi için AD etki alanı ayrıntılarını dağıtır. Etki alanına ilişkin bir profil oluşturmazsanız bu cihazların dağıtımı başarısız olabilir.

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri
- Hibrit Azure AD’ye katılmış cihazlar
- Autopilot + Intune ile karma dağıtım

Bu makalede, karma Autopilot dağıtımı için bir etki alanı ekleme profili oluşturma gösterilmektedir. Kullanılabilir ayarları da görebilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **Windows 10: karma ad 'ye katılmış cihazları Windows Autopilot 'e kaydetmek için şirket içi etki alanı bilgilerini Içeren etki alanına katılma profilidir**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: **Windows 10 ve üstünü**seçin.
    - **Profil türü**: **etki alanına katılmayı (Önizleme)** seçin.

4. **Ayarlar**' ı seçin. Aşağıdaki özellikleri girin:

    - **Bilgisayar adı ön eki**: Cihaz adı için bir ön ek girin. Bilgisayar adları 15 karakter uzunluğundadır. Ön ek sonrasında, kalan 15 karakter rastgele oluşturulur.
    - **Etki alanı adı**: cihazların katılabileceği tam etki alanı adını (FQDN) girin. Örneğin, şunu girin`americas.corp.contoso.com.`
    - **Kuruluş birimi** (isteğe bağlı): bilgisayar hesaplarının oluşturulacağı kuruluş BIRIMI (OU) için tam yolu ([ayırt edici ad](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) girin. Örneğin, `"CN=Users,DC=Contoso,DC=com"` girin. Değer girmezseniz, iyi bilinen bir bilgisayar nesne kapsayıcısı kullanılır.

      Bu ayar hakkında daha fazla bilgi ve öneri için bkz. [karma Azure AD 'ye katılmış cihazları dağıtma](../enrollment/windows-autopilot-hybrid.md).

5. İşiniz bittiğinde, değişikliklerinizi kaydetmek için **Tamam** > **Oluştur** ' u seçin.

Profil oluşturulur ve profiller listesinde gösterilir. Artık [Intune ve Windows Autopilot kullanarak karma Azure AD 'ye katılmış cihazları dağıtmanıza](../enrollment/windows-autopilot-hybrid.md)hazırdır.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduktan sonra atanmak için hazırlanın. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

[Intune ve Windows Autopilot kullanarak karma Azure AD 'ye katılmış cihazları dağıtın](../enrollment/windows-autopilot-hybrid.md).
