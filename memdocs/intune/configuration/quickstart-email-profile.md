---
title: Hızlı başlangıç-iOS/ıpados cihazları için bir e-posta cihaz profili oluşturma
titleSuffix: Microsoft Intune
description: İOS/ıpados cihazlarının şirket e-postasına güvenli bir şekilde bağlanabilmesi için bir e-posta cihaz profili oluşturmak üzere Microsoft Intune nasıl kullanacağınızı öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af7657eb89df14e8429a81616e76d81a5a9ac5c1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327434"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Hızlı başlangıç: iOS/ıpados için bir e-posta cihaz profili oluşturma

Bu hızlı başlangıçta iOS/ıpados cihazları için bir e-posta cihaz profili oluşturma hakkında bilgi edineceksiniz. Bu profil, şirket e-postasına bağlanmak için iOS/ıpados cihazında yerleşik e-posta uygulaması için gerekli olan ayarları belirtir. E-posta cihaz profilleri cihaz ayarlarını standartlaştırır ve son kullanıcıların kişisel cihazlarında şirket e-postasına bir kurulum yapmaları gerekmeden erişmelerini sağlar. E-postanızı daha fazla korumak için bir e-posta profili kullanarak cihazların uyumlu olup olmadığını belirleyebilir ve sonra yalnızca uyumlu cihazların e-postaya erişmesine izin vermek üzere koşullu erişim ayarlayabilirsiniz. E-posta profilleri hakkında bilgi için bkz. [Microsoft Intune'da e-posta ayarlarını yapılandırma](email-settings-configure.md)

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Intune'da oturum açma

[Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) genel yönetici veya Intune Hizmet Yöneticisi olarak oturum açın. Intune Deneme aboneliği oluşturduysanız aboneliği oluşturduğunuz hesap Genel yönetici rolüne sahip olur.

## <a name="create-an-iosipados-email-profile"></a>İOS/ıpados e-posta profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. Seçin ve **cihazlar** > **yapılandırma profilleri** > **Profil oluştur**' a gidin.
   ![Intune 'da iOS/ıpados için bir e-posta profili oluşturma](./media/quickstart-email-profile/ios-create-profile.png)

3. Aşağıdaki özellikleri girin:
   - **Platform**: **IOS/ıpados** seçin
   - **Profil**: **e-posta** Seç
  
4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:
   - **Ad**: Yeni profil için açıklayıcı bir ad girin. Bu örnekte **iOS iş e-postası iste** girin.
   - **Açıklama**: **IOS/ıpados cihazlarının iş e-postasını kullanmasını gerektir** yazın


        ![Intune 'da iOS/ıpados cihazları ile kullanmak için bir e-posta profili oluşturma](./media/quickstart-email-profile/ios-email-profile-name.png)

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, aşağıdaki ayarları girin (diğer ayarlar için varsayılan değerleri bırakın):
   - **E-posta sunucusu**: Bu hızlı başlangıç için **outlook.office365.com** girin. Bu ayar, iOS/ıpados posta uygulamasının e-postaya bağlanmak için kullanacağı e-posta sunucusunun Exchange konumunu (URL) belirtir.
   - **Hesap adı**: girin **şirket e-posta**.
   - **AAD'den kullanıcı adı özniteliği**: Bu ad, Intune'un Azure Active Directory'den (Azure AD) aldığı özniteliktir. Intune, bu profilin kullanıcı adını bu adı kullanarak dinamik olarak oluşturur. Bu hızlı başlangıçta, **Kullanıcı asıl adının** profile (örneğin, user1@contoso.com) Kullanıcı adı olarak kullanılmasını istediğinizi varsayacağız.
   - **AAD'den e-posta adresi özniteliği**: Bu ayar Exchange'de oturum açmak için kullanılacak Azure AD e-posta adresidir. Bu hızlı başlangıçta **Kullanıcı Asıl Adı**'nı seçin.
   - **Kimlik doğrulama yöntemi**: Bu hızlı başlangıçta **Kullanıcı adı ve parola**'yı seçin. (Intune için zaten bir sertifika ayarladıysanız, **sertifika** da seçebilirsiniz.)

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** içinde (isteğe bağlı) **Ileri**' yi seçin. Bu profil için kapsam etiketi kullanmayacağız.

10. **Atamalar**' da, **ata** için açılan eklentiyi kullanın ve **tüm kullanıcılar ve tüm cihazlar '** ı seçin.  Ardından **İleri**' yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Ek öğreticiler veya test için oluşturduğunuz profili kullanmayı düşünmüyorsanız, şimdi silebilirsiniz.

1. Intune ' da**cihazlar** > **cihaz yapılandırması**' nı seçin.
2. Oluşturduğunuz test profilini ve **iOS/ıpados iş e-postası gerektir**' i seçin ve **Sil**' i seçin. 

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta iOS/ıpados cihazları için bir e-posta profili oluşturdunuz. Artık bu profili, bir iOS/ıpados cihazının profille eşleşmeyen tüm iOS/ıpados aygıtlarını işaret eden bir uyumluluk ilkesi oluşturarak uyumlu olup olmadığını anlamak için kullanabilirsiniz. Daha fazla koruma için, uyumsuz iOS/ıpados cihazlarının e-postaya erişimini engelleyen bir koşullu erişim ilkesi oluşturabilirsiniz. Cihaz uyumluluk ilkeleri hakkında daha fazla bilgi için bkz. [Intune’da cihaz uyumluluk ilkelerini kullanmaya başlama](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Öğretici: Yönetilen cihazlarda Exchange Online e-postalarını koruma](../protect/tutorial-protect-email-on-enrolled-devices.md)
