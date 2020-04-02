---
title: Microsoft Intune-Azure 'da macOS cihazlarına tercih dosyası ayarları ekleme | Microsoft Docs
titleSuffix: ''
description: Uygulamanız hakkında önemli bilgileri içeren bir XML veya plist dosyası ekleyin. Özellik Listesi dosyasındaki anahtar bilgilerini değiştirmek ve macOS cihazlarınıza atamak için bir tercih dosyası cihaz yapılandırma profili kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9cb8cea30b53c5619580b289f73529668d71e909
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551500"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Microsoft Intune kullanarak macOS cihazlarına bir özellik listesi dosyası ekleyin

Microsoft Intune kullanarak, macOS cihazları için bir özellik listesi dosyası (. plist) veya macOS cihazlarındaki uygulamalar ekleyebilirsiniz.

Bu özellik şu platformlarda geçerlidir:

- macOS 10,7 ve üzeri

Özellik listesi dosyaları, macOS uygulamalarıyla ilgili bilgileri içerir. Daha fazla bilgi için bkz. [bilgi özellik listesi dosyaları](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apple 'ın Web sitesi) ve [özel yük ayarları](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1)hakkında.

Bu makalede, macOS cihazlarına ekleyebileceğiniz farklı özellik listesi dosyası ayarları listelenir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, uygulama paketi KIMLIĞINI (`com.company.application`) eklemek ve uygulamanın. plist dosyasını eklemek için bu ayarları kullanın.

Bu ayarlar, Intune'da bir cihaz yapılandırma profiline eklenir ve daha sonra macOS cihazlarınıza atanır veya dağıtılır.

## <a name="what-you-need-to-know"></a>Bilmeniz gerekenler

- Bu ayarlar doğrulanmaz. Profili cihazlarınıza atamadan önce değişikliklerinizi test ettiğinizden emin olun.
- Uygulama anahtarı girme konusunda emin değilseniz, uygulama içindeki ayarı değiştirin. Ardından, ayarın nasıl yapılandırıldığını görmek için [Xcode](https://developer.apple.com/xcode/) kullanarak uygulamanın tercih dosyasını gözden geçirin. Apple, dosyayı içeri aktarmadan önce Xcode kullanılarak yönetilebilir olmayan ayarların kaldırılmasını önerir.
- Yalnızca bazı uygulamalar yönetilen tercihlerle çalışır ve tüm ayarları yönetmenize izin verebilir.
- Kullanıcı kanalı ayarlarını değil cihaz kanalı ayarlarını hedef alan özellik listesi dosyalarını karşıya yüklediğinizden emin olun. Özellik listesi dosyaları tüm cihazı hedefleyin.

> [!NOTE]
> Intune kullanıcı arabirimi (UI) tam ekran deneyimine sahiptir ve birkaç hafta sürebilir. Kiracınız bu güncelleştirmeyi alıncaya kadar, bu makalede açıklanan ayarları oluştururken veya düzenlerken biraz farklı bir iş akışına sahip olursunuz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **MacOS** seçin
    - **Profil**: **tercih dosyasını**seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **MacOS: cihazlarda Microsoft Defender ATP 'yi yapılandıran tercih dosyası Ekle**' dir.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**'yi seçin.

7. **Yapılandırma ayarları**' nda ayarlarınızı yapılandırın:

    - **Tercih etki alanı adı**: özellik listesi dosyaları genellikle Web tarayıcıları (Microsoft Edge), [Microsoft Defender Gelişmiş tehdit koruması](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)ve özel uygulamalar için kullanılır. Bir tercih etki alanı oluşturduğunuzda, bir paket KIMLIĞI de oluşturulur. `com.company.application`gibi paket KIMLIĞINI girin. Örneğin `com.Contoso.applicationName`, `com.Microsoft.Edge`veya `com.microsoft.wdav`girin.
    - **Özellik listesi dosyası**: uygulamanızla ilişkili özellik listesi dosyasını seçin. Bir `.plist` veya `.xml` dosyası olduğundan emin olun. Örneğin, bir `YourApp-Manifest.plist` veya `YourApp-Manifest.xml` dosyası yükleyin.
    - **Dosya içeriği**: Özellik Listesi dosyasındaki önemli bilgiler gösterilir. Anahtar bilgilerini değiştirmeniz gerekiyorsa, liste dosyasını başka bir düzenleyicide açın ve ardından dosyayı Intune 'A yeniden yükleyin.

    Dosyanızın doğru biçimlendirildiğinden emin olun. Dosya yalnızca anahtar değer çiftlerine sahip olmalı ve `<dict>`, `<plist>`veya `<xml>` etiketlerinde sarmalanmamalıdır. Örneğin, özellik listesi dosyanız aşağıdaki dosyaya benzer olmalıdır:

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. **İleri**'yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili `US-NC IT Team` veya `JohnGlenn_ITDepartment`gıbı belirli BT gruplarına filtrelemek için bir etiket atayın. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**'yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**'yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulur ancak henüz herhangi bir işlem gerçekleştirmez. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

Microsoft Edge için tercih dosyaları hakkında daha fazla bilgi için bkz. [macOS 'Ta Microsoft Edge ilke ayarlarını yapılandırma](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
