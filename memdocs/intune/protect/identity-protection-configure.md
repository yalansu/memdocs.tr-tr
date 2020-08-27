---
title: Microsoft Intune-Azure kullanarak Windows 10 cihazlarda oturum açmak için PIN kullanma | Microsoft Docs
description: Kullanıcıların bir PIN, parmak izi ve daha fazlasını kullanarak cihazlarda oturum açmalarına olanak tanımak için Iş için Windows Hello 'Yu kullanın. Bu ayarlarla Windows 10 cihazları için Intune 'da bir kimlik koruması yapılandırma profili oluşturun ve profili Kullanıcı gruplarına ve cihaz gruplarına atayın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 233ef8ce9c4ebd8ce5efe91715d653feaba2e88a
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909151"
---
# <a name="use-windows-hello-for-business-on-windows-10-devices-with-microsoft-intune"></a>Microsoft Intune ile Windows 10 cihazlarda Iş için Windows Hello 'Yu kullanma

Iş için Windows Hello, parolaları, akıllı kartları ve sanal akıllı kartları değiştirerek Windows cihazlarda oturum açmaya yönelik bir yöntemdir. Intune, yöneticilerin Iş için Windows Hello 'Yu yapılandırıp kullanabilmesi için yerleşik ayarları içerir. Örneğin, bu ayarları kullanarak şunları yapabilirsiniz:

- Cihazlar ve kullanıcılar için Iş için Windows Hello 'Yu etkinleştir
- Minimum veya maksimum PIN uzunluğu dahil cihaz PIN gereksinimlerini ayarla
- Kullanıcıların cihazlarda oturum açmasını sağlayan (veya kullanabilecek) parmak izi gibi hareketlere izin ver

Bu özellik şunları çalıştıran cihazlarda geçerlidir:

- Windows 10 ve üzeri
- Windows 10 Holographic for Business

Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profilde ekledikten sonra bu ayarları kuruluşunuzdaki Kullanıcı ve cihaz gruplarına gönderin veya dağıtın.

Bu makalede bir cihaz yapılandırma profili oluşturma konusu gösterilmektedir. Tüm ayarların bir listesi ve ne yapacaklarınız için Windows 10 cihaz ayarları ' na bakın ve [iş Için Windows Hello 'yu etkinleştirin](identity-protection-windows-settings.md).

## <a name="create-the-device-profile"></a>Cihaz profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. Aşağıdaki özellikleri girin:

   - **Ad**: Yeni profil için açıklayıcı bir ad girin.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
   - **Platform**: **Windows 10 ve üstünü**seçin. İş İçin Windows Hello, yalnızca Windows 10 ve üzeri çalıştıran cihazlarda desteklenir.
   - **Profil türü**: **kimlik koruması**' nı seçin.

4. *İş Için Windows Hello* bölmesinde, aşağıdaki seçenekleri yapılandırın:

   - **İş Için Windows Hello 'Yu Yapılandır**: Iş Için Windows Hello 'yu nasıl yapılandırmak istediğinizi seçin:

     - **Yapılandırılmadı** (varsayılan): cihazda [Iş Için Windows Hello 'yu hazırlar](/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning) . Kimlik koruma profillerini yalnızca kullanıcılara atarken cihaz bağlamı varsayılan olarak **Yapılandırılmadı** olur.

     - **Devre dışı**: Iş Için Windows Hello 'yu kullanmak istemiyorsanız, bu seçeneği seçin. Bu seçenek tüm kullanıcılar için Iş için Windows Hello 'Yu devre dışı bırakır.

     - **Etkin**: Intune 'da Iş Için Windows Hello ayarlarını [sağlamak](/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning)ve yapılandırmak için bu seçeneği belirleyin. Yapılandırmak istediğiniz ayarları girin. Tüm ayarların bir listesi ve ne yaptıkları gibi, bkz. [iş Için Windows Hello 'yu etkinleştirmek Için Windows 10 cihaz ayarları](identity-protection-windows-settings.md).

   - **Oturum açma için güvenlik anahtarlarını kullan**: Windows Hello güvenlik anahtarını Kiracıdaki tüm bilgisayarlar için oturum açma kimlik bilgileri olarak etkinleştirin.

     - **Etkinleştirme**
     - **Yapılandırılmadı**  (varsayılan)

5. İşiniz bittiğinde, değişikliklerinizi kaydetmek için **Tamam**  >  **Oluştur** ' u seçin.

Profil oluşturulur ve profiller listesinde görüntülenir. Daha sonra, gereksinimlerinizi karşılamak için bu profili Kullanıcı ve cihaz gruplarına [atayın](../configuration/device-profile-assign.md) .

> [!IMPORTANT]
> Bir cihaza birden çok kullanıcının sağlanmasını sağlamak için, Iş için Windows Hello ilkesinin cihazlara uygulanacağını belirtin. İlke yalnızca kullanıcılara uygulanmışsa, bir cihaza yalnızca bir Kullanıcı sağlanabilir.

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/identity-protection-configure/disable-android-camera.png)

-->

## <a name="next-steps"></a>Sonraki adımlar

- Tüm ayarların bir listesini [ve ne yaptığını](identity-protection-windows-settings.md)görün.
- [Profili atama](../configuration/device-profile-assign.md) ve [durumunu izleme](../configuration/device-profile-monitor.md).