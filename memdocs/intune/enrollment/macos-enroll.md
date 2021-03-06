---
title: macOS cihazların kaydını ayarlama
titleSuffix: Microsoft Intune
description: Intune’da macOS cihazların kaydının nasıl ayarlandığını öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f2b2826e8eaf1cf1c1c8680743b582203199aed
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906846"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Intune’da macOS cihazların kaydını ayarlama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune, kullanıcılara şirket e-postasına ve uygulamalarına erişim vermek için macOS cihazlarını yönetmenize olanak tanır.

Intune yöneticisi olarak, şirkete ait macOS cihazları ile kişilere ait macOS cihazları ("kendi cihazını getir" veya KCG) için kaydı ayarlayabilirsiniz. 

## <a name="prerequisites"></a>Önkoşullar

macOS cihaz kaydını ayarlamadan önce, aşağıdaki önkoşulları tamamlayın:

- [Cihazınızın Apple cihaz kaydına uygun olduğundan emin olun](https://support.apple.com/en-us/HT204142#eligibility).
- [Etki alanlarını yapılandırma](../fundamentals/custom-domain-name-configure.md)
- [MDM yetkilisini ayarlama](../fundamentals/mdm-authority-set.md)
- [Grup oluşturma](../fundamentals/groups-add.md)
- [Şirket Portalı’nı yapılandırma](../apps/company-portal-app.md)
- [Microsoft 365 yönetim merkezinde](https://go.microsoft.com/fwlink/p/?LinkId=698854) kullanıcı lisanslarını atama
- [Apple MDM anında iletme sertifikası alın](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>Kullanıcıya ait macOS cihazları (KCG)

Kullanıcıların kendi kişisel cihazlarını Intune yönetimine kaydetmelerini sağlayabilirsiniz. Bu, "kendi cihazını getir" veya KCG olarak bilinir. Önkoşulları ve atanan kullanıcı lisanslarını tamamladıktan sonra, kullanıcılarınız cihazlarını şu şekilde kaydedebilir:
- [Şirket portalı Web sitesine](https://portal.manage.microsoft.com) veya
- [Aka.MS/EnrollMyMac](https://aka.ms/EnrollMyMac)adresindeki Mac Şirket portalı uygulaması indiriliyor.

Kullanıcılarınıza çevrimiçi kayıt adımları için bir bağlantı da gönderebilirsiniz: [macOS cihazınızı Intune 'A kaydetme](../user-help/enroll-your-device-in-intune-macos-cp.md).

Diğer son kullanıcı görevleri hakkında daha fazla bilgi için şu makalelere bakın:

- [Microsoft Intune’da son kullanıcı deneyimi hakkında kaynaklar](../fundamentals/end-user-educate.md)
- [macOS cihazınızı Intune ile kullanma](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>Şirkete ait macOS cihazları
Kullanıcılarına cihaz sağlayan kuruluşlar için Intune, aşağıdaki şirkete ait macOS cihazı kayıt yöntemlerini destekler:
- [Apple 'ın otomatik cihaz kaydı (ade)](device-enrollment-program-enroll-macos.md): kuruluşlar MacOS cihazlarını Ade aracılığıyla satın alabilir. ADE, cihazları yönetime getirmek için bir kayıt profilini "hava üzerinden" dağıtmanızı sağlar.
- [Cihaz kayıt yöneticisi (DEM)](device-enrollment-manager-enroll.md): En çok 1.000 cihazı kaydetmek için DEM hesabı kullanabilirsiniz.
- [Doğrudan kayıt](device-enrollment-direct-enroll-macos.md): doğrudan kayıt, cihazı temizlemez.

## <a name="block-macos-enrollment"></a>macOS kaydını engelleme
Varsayılan olarak, Intune macOS cihazlarının kaydına izin verir. macOS cihazlarının kaydedilmesini engellemek için bkz. [Cihaz türü kısıtlamaları ayarlama](enrollment-restrictions-set.md).

## <a name="enroll-virtual-macos-machines-for-testing"></a>Sanal macOS makineleri sınama için kaydetme

> [!NOTE]
> macOS sanal makinelerin yalnızca sınama desteği vardır. macOS sanal makineleri son kullanıcılarınız için üretim cihazları olarak kullanmamalısınız. 

macOS sanal makineleri, Parallels Desktop veya VMware Fusion kullanarak sınama için kaydedebilirsiniz. 

Parallels Desktop kullanırsanız, Intune’un sanal makineleri tanıyabilmesi için bunların donanım türü ve seri numaralarını ayarlamanız gerekir. Sınama için gerekli ayarları yapmak üzere Parallels’in donanım türünü ve [seri numarasını ayarlama](http://kb.parallels.com/123455) yönergelerini izleyin. Sanal makineleri çalıştıran cihazın donanım türünü, oluşturduğunuz sanal makinelerin donanım türüyle eşleştirmenizi öneririz. Bu donanım türünü, **Apple menu**  >  **Bu Mac**  >  **Sistem rapor**  >  **modeli tanımlayıcısı**hakkında Apple menüsünde bulabilirsiniz. 

VMware Fusion kullanırsanız, sanal makinenin donanım türü ve seri numarasını ayarlamak için [.vmx dosyasını düzenlemeniz](https://kb.vmware.com/s/article/1014782) gerekir. Sanal makineleri çalıştıran cihazın donanım türünü, oluşturduğunuz sanal makinelerin donanım türüyle eşleştirmenizi öneririz. Bu donanım türünü, **Apple menu**  >  **Bu Mac**  >  **Sistem rapor**  >  **modeli tanımlayıcısı**hakkında Apple menüsünde bulabilirsiniz. 

## <a name="user-approved-enrollment"></a>Kullanıcı Onaylı kayıt

Kullanıcı Onaylı MDM kaydı, güvenlik açısından hassas bazı ayarları yönetmek için kullanabileceğiniz bir macOS kayıt türüdür. Daha fazla bilgi için [Apple'ın destek belgelerine](https://support.apple.com/HT208019) bakın.  
 
Haziran 2020 itibariyle, otomatik cihaz kaydı (ADE) üzerinden yapılmalanlar da dahil olmak üzere Intune 'daki tüm yeni macOS MDM kayıtları Kullanıcı onaylı olarak kabul edilir. Son Kullanıcı, yönetim profilini **Sistem Tercihleri**  >  **profillerine**el ile yüklemelidir ve bu nedenle yönetim profili onayını sağlamalıdır. Sistem Tercihleri, KCG macOS kullanıcıları için Şirket Portalı uygulamasından otomatik olarak başlatılır. [Yönetim profilini yüklemeye yönelik yönergeler](../user-help/enroll-your-device-in-intune-macos-cp.md) Şirket portalı uygulamasında sunulmaktadır.     

Haziran 2020 ' den önceki BYOD MacOS MDM kayıtları, Son Kullanıcı **Sistem Tercihleri**profillerindeki yönetim profilini el ile onaylamadıysa Kullanıcı onaylı olmayabilir  >  **Profiles**. Haziran 2020 ' den sonra BYOD kayıtları için Şirket Portalı uygulaması kullanıcı için **sistem tercihlerini** başlatır ve kullanıcının yüklemeyi seçmesini gerekir. Kullanıcı kayıt sırasında yönetim profilini onaylamadıysanız, Kullanıcı **Sistem Tercihleri**  >  **profilleri**' ne gidebilir, yönetim profilini seçebilir ve daha sonraki bir noktada profili onaylamak için **Onayla** ' yı seçin.

### <a name="find-out-if-a-device-is-user-approved"></a>Bir cihazın Kullanıcı tarafından onaylanmış olup olmadığını bulma
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar**  >  **tüm cihazlar** ' ı seçin> cihazı > **donanımı**seçin.
3. **Kullanıcının onayladığı kayıt** alanını denetleyin.


## <a name="next-steps"></a>Sonraki adımlar

macOS cihazları kaydedildikten sonra, [macOS cihazları için özel ayarlar oluşturabilirsiniz](../configuration/custom-settings-macos.md).