---
title: Samsung Knox için uygulamalara izin veren veya uygulamaları engelleyen Microsoft Intune ilkesi
titleSuffix: ''
description: Samsung Knox Standard cihazlarında uygulamalara izin vermek veya uygulama engellemek için bir özel profil oluşturun.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ee2e89dcfd7ab963dae3b14b5e7d53daaa07ff4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695996"
---
# <a name="use-custom-policies-in-microsoft-intune-to-allow-and-block-apps-for-samsung-knox-standard-devices"></a>Microsoft Intune’da özel ilkeler kullanarak Samsung Knox Standard cihazları için uygulamalara izin verme veya bunları engelleme 

Bu makaledeki yordamı kullanarak, aşağıdakilerden birini oluşturan bir Microsoft Intune özel ilkesi oluşturun:

- Cihazda çalışması engellenmiş uygulamaların listesi. İlke uygulandığı sırada zaten yüklenmiş durumda olsalar bile, bu listede yer alan uygulamaların çalışması engellenir.
- Cihaz kullanıcılarının Google Play mağazasından yüklemesine izin verilen uygulamaların listesi. Yalnızca listelediğiniz uygulamalar yüklenebilir. Mağazadan başka hiçbir uygulama yüklenemez.

Bu ayarlar yalnızca Samsung Knox Standard çalıştıran cihazlar tarafından kullanılabilir.

## <a name="create-an-allowed-or-blocked-app-list"></a>izin verilen veya engellenen uygulama listesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki ayarları girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı **Android özel profilidir**.
    - **Açıklama**: Ayara genel bir bakış sağlayan ve diğer önemli ayrıntıları veren bir açıklama girin.
    - **Platform**: **Android**' i seçin.
    - **Profil türü**: **özel**' i seçin.

4. **Özel OMA-URI Ayarları**’nda **Ekle**’yi seçin. Aşağıdaki ayarları girin:

    Cihazda çalıştırılması engellenen uygulamalar listesi için:

    - **Ad**: **preventstartpackages**girin.
    - **Açıklama**: Ayara genel bir bakış sağlayan ve profili bulmanıza yardımcı olacak diğer ek bilgileri içeren bir açıklama girin. Örneğin, **çalışması engellenen uygulamaların listesini**girin.
    - **OMA-URI** (büyük/küçük harfe duyarlı): **./Vendor/MSFT/PolicyManager/My/ApplicationManagement/preventstartpackages**girin.
    - **Veri türü**: **dize**seçin.
    - **Değer**: izin vermek istediğiniz uygulama paket adlarının bir listesini girin. `;`, `:` Veya `|` ayırıcı olarak kullanabilirsiniz. Örneğin, `package1;package2;` girin.

   Diğer tüm uygulamaları hariç tutarak, kullanıcıların Google Play mağazasından yüklemesine izin verilen uygulamaların listesi için:

    - **Ad**: **Allowınstallpackages**girin.
    - **Açıklama**: ayara genel bir bakış sağlayan bir açıklama ve profili bulmanıza yardımcı olacak diğer ilgili bilgileri girin. Örneğin, **kullanıcıların Google Play yükleye, uygulamaların listesini**girin.
    - **OMA-URI** (büyük/küçük harfe duyarlı): **./Vendor/MSFT/PolicyManager/My/ApplicationManagement/allowınstallpackages**yazın.
    - **Veri türü**: **dize**seçin.
    - **Değer**: izin vermek istediğiniz uygulama paket adlarının bir listesini girin. `;`, `:` Veya `|` ayırıcı olarak kullanabilirsiniz. Örneğin, `package1;package2;` girin.

5. Değişikliklerinizi kaydetmek için **Tamam**’ı seçin.
6. İşiniz bittiğinde, **OK**  >  Intune profilini oluşturmak için Tamam**Oluştur** ' u seçin. Bu tamamlandığında, profiliniz **cihazlar-yapılandırma profilleri** listesinde gösterilir.

>[!TIP]
> Uygulamanın paket kimliğini, Google Play mağazasında uygulamaya göz atarak bulabilirsiniz. Paket kimliği, uygulanın sayfasının URL’sinde yer alır. Örneğin, Microsoft Word uygulamasının paket kimliği **com.microsoft.office.word**’dür.

Her hedeflenen cihaz bir sonraki sefer iade ettiğinde, uygulama ayarları uygulanır.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulur ancak henüz herhangi bir işlem gerçekleştirmez. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).
