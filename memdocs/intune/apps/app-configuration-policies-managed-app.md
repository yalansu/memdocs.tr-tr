---
title: Cihaz kaydı olmadan yönetilen uygulamalar için uygulama yapılandırma ilkeleri
titleSuffix: Microsoft Intune
description: Cihaz kaydı olmadan yönetilen uygulamalar için ilkeleri yapılandırmayı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b493443a86d7cd1769ce6f66c77acc87063521f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461649"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>Cihaz kaydı olmadan yönetilen uygulamalar için uygulama yapılandırma ilkeleri ekleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune App SDK’sını destekleyen yönetilen uygulamalarla uygulama yapılandırma ilkelerini, kayıtlı olmayan cihazlarda dahi kullanabilirsiniz. 

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen uygulamalar**Ekle ' yi seçin.
3. **Temel bilgiler** sayfasında, aşağıdaki ayrıntıları ayarlayın:
    - **Ad**: Azure Portal görünecek profilin adı.
    - **Açıklama**: Azure Portal görüntülenecek profil açıklaması.
    - **Cihaz kayıt türü**: yönetilen uygulamalar seçilidir.
4. Yapılandırmak istediğiniz uygulamayı seçmek için **ortak uygulamaları seçin** ya da **özel uygulamalar** ' ı seçin. Onayladığınız ve Intune ile eşitlenmiş uygulamalar listesinden uygulamayı seçin.
5. **İleri** ' ye tıklayarak **Ayarlar** sayfasını görüntüleyin.
6. **Ayarlar sayfası** , yapılandırdığınız uygulamaya göre görüntülenen seçenekleri sağlar:

    - **Genel yapılandırma ayarları** -uygulamanın desteklediği her genel yapılandırma ayarı için **adı** ve **değeri**yazın. 
 
        Intune Uygulama SDK’sı özellikli uygulamalar, anahtar/değer çiftlerinde yapılandırmaları destekler. Hangi anahtar-değer yapılandırmalarının desteklendiğini öğrenmek için uygulamaların kendi belgelerine bakın. Uygulama tarafından oluşturulan verilerle dinamik olarak doldurulacak belirteçler kullanabileceğinizi unutmayın. Genel bir yapılandırma ayarını silmek için üç nokta (**...**) simgesini seçin ve **Sil**' i seçin. Daha fazla bilgi için bkz. [belirteçleri kullanmak Için yapılandırma değerleri](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens). 

    - **Outlook yapılandırma ayarları** -IOS ve Android için Outlook, yöneticilere birçok uygulama içi ayar için varsayılan yapılandırmayı özelleştirme olanağı sunar. Daha fazla bilgi için bkz. [iOS ve Android Için Outlook-genel uygulama yapılandırma senaryoları](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios).
   
    - **S/MIME** güvenli çok amaçlı Internet posta uzantıları (s/MIME), kullanıcıların dijital imzalı ve şifrelenmiş e-posta gönderip almasına izin veren bir belirtimdir.
        - **S/MIME 'Yi etkinleştir** -e-posta oluştururken s/MIME denetimlerinin etkinleştirilip etkinleştirilmeyeceğini belirtin. Varsayılan değer: **Yapılandırılmadı**.
        - **Kullanıcının ayarı değiştirmesine Izin ver** -kullanıcının ayarı değiştirmesine izin verilip verilmediğini belirtin. S/MIME etkin olmalıdır. Varsayılan değer: **Evet**.
        
    Outlook uygulama yapılandırma ilkesi ayarları hakkında daha fazla bilgi için bkz. [iOS ve Android Için Outlook uygulama yapılandırma ayarları](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

7. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.
8. **Dahil edilecek grupları seç ' e**tıklayın.
9. **Dahil edilecek grupları seçin** bölmesinde bir grup seçin ve **Seç**' e tıklayın.
10. İlgili bölmeyi görüntülemek için **Dışlanacak grupları seçin**’e tıklayın.
11. Dışlamak istediğiniz grupları seçin ve **Seç**’e tıklayın.

    >[!NOTE]
    >Bir grup eklerken, herhangi bir atama türü için başka bir grup önceden dahil edilmişse bu grup, diğer dahil etme atama türleri için önceden seçili ve değiştirilemez bir biçimde görüntülenir. Dolayısıyla bu grup zaten kullanılmıştır ve dışlanmış bir grup olarak kullanılamaz.

12. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin.
13. Uygulama yapılandırma ilkesini Intune 'a eklemek için **Oluştur** ' a tıklayın.

## <a name="configuration-values-for-using-tokens"></a>Belirteç kullanmak için yapılandırma değerleri

Intune bazı belirteçleri oluşturabilir ve yönetilen uygulamaya gönderebilir. Örneğin uygulama yapılandırmanız bir e-posta ayarı kullanabiliyorsa, bir belirteç kullanarak dinamik bir e-posta ekleyebilirsiniz. **Ad** alanına uygulama tarafından beklenen adı yazıp **Değer** alanına `\{\{mail\}\}` yazın.

Intune, yapılandırma ayarlarında aşağıdaki belirteç türlerini destekler. Diğer özel anahtar/değer çiftleri desteklenmez.

- \{\{userprincipalname\}\}: örneğin John@contoso.com
- \{\{mail\}\}: örneğin John@contoso.com
- \{\{partialupn\}\}: örneğin John
- \{\{accountid\}\}: örneğin fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\}: örneğin 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\}: örneğin John Doe
- \{\{PrimarySMTPAddress\}\}: örneğin testuser@ad.domain.com

> [!Note]  
> \{\{ ve \}\} karakterleri yalnızca belirteç türleri tarafından kullanılır ve başka bir amaçla kullanılmamalıdır.

## <a name="next-steps"></a>Sonraki adımlar

Normal yollarla, uygulamayı [atama](apps-deploy.md) ve [izleme](apps-monitor.md) işlemlerine devam edin.
