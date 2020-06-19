---
title: Microsoft Intune-Azure 'da macOS cihazları için 802.1 x kablolu ağ ayarlarını yapılandırma | Microsoft Docs
titleSuffix: ''
description: MacOS masaüstü bilgisayar cihazları için kablolu ağ cihazı yapılandırma profili oluşturun veya ekleyin. Farklı ayarları görüntüleyin, sertifika ekleyin, bir EAP türü seçin ve Microsoft Intune bir kimlik doğrulama yöntemi seçin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095725"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Microsoft Intune içindeki macOS cihazlarınıza kablolu ağ ayarlarını ekleyin ve kullanın

Kablolu ağlar, masaüstü bilgisayarlara ağ erişimi sağlamak için birçok kuruluş tarafından kullanılır. Microsoft Intune, kuruluşunuzdaki macOS kullanıcıları ve cihazlarına dağıtılabilecek yerleşik ayarları içerir. Bu ayar grubuna "profil" adı verilir. Profilinizde, ağ arabirimi, kabul edilen EAP türleri ve sunucu güven ayarları gibi ortak ayarları ekleyebilirsiniz.

Profil hazırlanıyor, farklı kullanıcılara ve gruplara atanabilir. Atandıktan sonra kullanıcılarınız, kuruluşunuzun kablolu ağına kendi kendilerini yapılandırmadan erişim kazanın.

Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, kablolu ağları yönetmek için 802.1 x profilleri oluşturmak üzere bu özelliği kullanın. Ardından, bu kablolu ağları macOS cihazlarınıza dağıtın.

Bu özellik şu platformlarda geçerlidir:

- Mac OS

Örneğin, **contoso kablolu ağ**adlı bir kablolu ağınız vardır. Tüm macOS masaüstlerini bu ağa bağlanacak şekilde ayarlamak istiyorsunuz. İşlem şöyledir:

1. **Contoso kablolu ağına**bağlanan ayarları içeren bir kablolu ağ profili oluşturun.
2. Profili tüm kullanıcılar macOS masaüstü bilgisayarları içeren bir gruba atayın. Grup türlerini kullanma ile ilgili öneriler için bkz. [Kullanıcı grupları ve cihaz grupları](device-profile-assign.md#user-groups-vs-device-groups).
3. Kullanıcılar, masaüstlerinde, ağ listesinde **contoso kablolu ağını** bulur. Daha sonra seçtiğiniz kimlik doğrulama yöntemini kullanarak ağa bağlanabilirler.

Bu makalede kablolu ağ profili oluşturma adımları listelenir. Ayrıca, farklı ayarları açıklayan bir bağlantı da içerir.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **MacOS**' u seçin.
    - **Profil**: **kablolu ağ**' ı seçin.

4. **Oluştur**'u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, **macOS cihazlarındaki tüm şirket Için kablolu ağ profilidir**.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda ağın ağ arabirimini seçin ve Genişletilebilir Kimlik Doğrulama Protokolü (EAP) türünü seçin. Tüm ayarların bir listesi ve ne yapacaklarınız için, bkz.:

    - [macOS](wired-network-settings-macos.md)

8. **İleri**’yi seçin.
9. **Atamalar**' da, profilinizi alacak Kullanıcı gruplarını veya cihaz gruplarını seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

10. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

> [!TIP]
> Kablolu ağ profiliniz için sertifika tabanlı kimlik doğrulaması kullanıyorsanız, kablolu ağ profilini, sertifika profilini ve güvenilen kök profilini aynı gruplara dağıtın. Bu dağıtım, her cihazın sertifika yetkilinizin yasallığını tanıyabileceği şekilde sağlar. Daha fazla bilgi için bkz. [Microsoft Intune sertifikaları yapılandırma](../protect/certificates-configure.md).

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak herhangi bir şey olmayabilir. [Bu profili atadığınızdan](device-profile-assign.md)emin olun ve [durumunu izleyin](device-profile-monitor.md).
