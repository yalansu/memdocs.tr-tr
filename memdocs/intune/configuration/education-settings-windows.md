---
title: Microsoft Intune-Azure 'da Windows 10 eğitim ayarları | Microsoft Docs
description: Windows 10 cihazları için tüm eğitim ayarlarının listesini görüntüleyin. Bu ayarları, test alma uygulaması ile bir cihaz yapılandırma profilinde kullanın, kullanıcıların veya öğrencilerin oturum açmasını, test sırasında ekranı nasıl izleyeceğinizi ve Intune 'da daha fazlasını yapın.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39f881b05c9698a8560fe009331fac3389b35bde
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333082"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Intune kullanarak Windows 10 cihazlarda bir test alma uygulaması yapılandırma

Bir test al uygulaması, dersin Windows 10 cihazlarında çevrimiçi testleri güvenli bir şekilde yönetmenizi sağlar. Test al uygulamasını ayarlamak için, Intune 'da bir cihaz yapılandırma profili oluşturmanız ve güvenli değerlendirme ayarlarını yapılandırmanız gerekir. Bu makalede, test alma uygulaması için bulacağınız ayarlar açıklanmaktadır. 

Profili yapılandırdıktan sonra öğrencilerinize atayıp dağıtın. 

[Intune 'da bir test uygulaması alma](education-settings-configure.md) bu özellik hakkında daha fazla bilgi sağlar.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Test ayarları yapın
Bir cihaz yapılandırma profili oluşturduktan sonra, **profil türü** ' ne gidin ve **güvenli değerlendirme (eğitim)** seçeneğini belirleyin. Aşağıdaki bir test uygulaması ayarlarını yapın. 


- **Hesap türü**: kullanıcıların testte oturum açmasını seçin. Seçenekleriniz şunlardır:
  - Azure AD hesabı
  - Etki alanı hesabı
  - Yerel hesap
  - Yerel Konuk hesabı: yalnızca Windows 10, sürüm 1903 ve üzeri sürümleri çalıştıran cihazlarda kullanılabilir.    
- **Hesap Kullanıcı adı**: bir test alma uygulamasıyla kullanılan hesabın kullanıcı adını girin. Hesapları aşağıdaki biçimde girebilirsiniz:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Hesap adı**: bir yerel Konuk hesap türü ayarlamak Için, test alma uygulaması ile kullanılan hesabın adını girin. Hesap adı, oturum açma ekranında bir kutucuk olarak görüntülenir. Öğrenciler, testi başlatmak için kutucuğa tıklayın.  
- **Değerlendirme URL 'si**: kullanıcıların geçirmesine istediğiniz testin URL 'sini girin. URL 'YI alma hakkında daha fazla bilgi için [test alma belgelerine](https://docs.microsoft.com/education/windows/take-tests-in-windows-10)bakın.
- **Yazıcı bağlantısı**: bir yazıcıya bağlı cihazlardan yalnızca bir test alma uygulaması erişimine izin vermek için **gerektir** ' i seçin. Bu ayar ayrıca uygulamanın Yazdır düğmesini test çiciler için kullanılabilir hale getirir. **Yapılandırılmadı** , öğrenciler, bir yazıcıya bağlı olmayan cihazlardan uygulamaya erişmesine izin verir.  
- **Ekran izleme**: kullanıcılar bir test alırken ekran etkinliğini Izlemeye **izin ver** ' i seçin. **Yapılandırılmadı** , sınama sırasında ekranı izlemekten engel olur.
- **Metin önerileri**: **izin ver** ' i seçin, böylece test takiciler metin önerilerini görüntüleyebilir. **Yapılandırılmadı** , kullanıcılar bir test sunarken metin önerilerini engeller.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atadığınızdan](device-profile-assign.md)emin olun ve [durumunu izleyin](device-profile-monitor.md).