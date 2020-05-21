---
title: Intune için Windows Güvenlik deneyimi için Windows 10 Antivirus ilke ayarları | Microsoft Docs
description: Microsoft Intune 'de Windows güvenlik uygulaması için uç nokta güvenliği virüsten koruma ilkesi ayarları
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431332"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Microsoft Intune Windows Güvenlik deneyimi profili için ayarlar

Bir [uç nokta güvenlik ilkesinin](../protect/endpoint-security-policy.md)parçası olarak Microsoft Intune Windows 10 Için **Windows Güvenlik deneyimi** profili için yapılandırabileceğiniz virüsten koruma ilkesi ayarlarını görüntüleyin.

**Windows güvenliği**

- **Microsoft Defender 'ın devre dışı bırakılmasını engellemek için yetkisiz korumayı etkinleştirin**  
  [Güvenlik ayarlarında, yetkisiz koruma ile değişiklik yapılmasını engelle](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Yapılandırılmadı** (*varsayılan*)-Istemcide *etkinleştirme* veya *devre dışı bırakma* durumu varsa, dağıtımının *yapılandırılması* ayarı etkilemez. 
  - **Enable** -yetkisiz koruma kısıtlamasını etkinleştirin. Durumu etkin ya da devre dışı olarak değiştirmek için, ters ayarı devreye sahip olacak şekilde dağıtın.
  - **Disable** -etkin olmayan koruma kısıtlamalarını devre dışı bırakın. Durumu etkin ya da devre dışı olarak değiştirmek için, ters ayarı devreye sahip olacak şekilde dağıtın.

- **Windows Güvenlik uygulamasında virüs ve tehdit koruması alanını gizle**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki virüs ve tehdit koruması alanı son kullanıcılardan gizlenir. Virüs ve tehdit koruması ile ilgili bildirimler bastırılır.

  - **Windows Güvenlik uygulamasında fidye yazılımı veri kurtarma seçeneğini gizle**  
    'SINI[](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki fidye yazılımı veri kurtarma alanı son kullanıcılardan gizlenir. Fidye yazılımı ile ilgili bildirimler bastırılır.

- **Windows Güvenlik uygulamasında hesap koruma alanını gizle**  
  CSP: [Disableaccountprotectionuı](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki hesap koruma alanı, son kullanıcılardan gizlenir. Hesap koruması ile ilgili bildirimler bastırılır.

- **Windows Güvenlik uygulamasında güvenlik duvarı ve ağ koruması alanını gizle**  
  CSP: [Disablenetworkuı](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows güvenliği içindeki güvenlik duvarı ve ağ koruması alanı son kullanıcılardan gizlenir. Güvenlik Duvarı ve ağ koruması ile ilgili bildirimler bastırılır.

- **Windows Güvenlik uygulamasında uygulama ve tarayıcı denetim alanını gizle**  
  CSP: [Disableappbrowseruı](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows güvenliği içindeki uygulama ve tarayıcı denetim alanı son kullanıcılardan gizlenir. Uygulama ve tarayıcı denetimi ile ilgili bildirimler bastırılır.

- **Windows Güvenlik uygulamasında cihaz güvenlik alanını gizle**  
  CSP: [Disabledevicesecurityuı](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki donanım koruma alanı, son kullanıcılardan gizlenir. Donanımla koruma ile ilgili bildirimler bastırılır.
  
- **Windows Güvenlik uygulamasında cihaz performansı ve sistem durumu alanını gizle**  
  CSP: [Disablehealthuı](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki cihaz performansı ve sistem durumu alanı son kullanıcılardan gizlenir. Cihaz performansı ve sistem durumu ile ilgili bildirimler Ware gizlendi

- **Windows Güvenlik uygulamasında aile seçenekleri alanını gizle**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcı erişimine ve bildirimlere izin vermek olan istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki aile seçenekleri alanı son kullanıcılardan gizlenir. Ayrıca, Aile seçenekleriyle ilgili bildirimler bastırılır.

- **Windows güvenlik uygulaması bildirimleri**  
  'SINI[](https://go.microsoft.com/fwlink/?linkid=873675)

  Bu ayarı, önceki özellik ayarlarına yönelik olarak kullanıcılarınıza Windows Güvenlik bildirimlerini engellemek için kullanın. Alternatif olarak, devam ayarlarını kullanarak özellik başına Windows güvenlik uygulaması bildirimlerini yönetebilirsiniz.

  - **Yapılandırılmadı** (*varsayılan*)-başka bir ayar tarafından denetlenmeyen tüm Windows güvenlik uygulaması bildirimlerine izin verilir.
  - **Kritik olmayan bildirimleri engelle** -tam tarama tamamlama gibi bildirimler engellenir.
  - **Tüm bildirimleri engelle** -kritik ve kritik olmayan bildirimler tüm Windows güvenlik özellikleri için engellenir.

- **Bildirim alanından Windows Güvenlik simgesini gizle**  
  CSP: [Hidewindowssecuritynotificationareacontrol](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  Bu ayarın etkili olması için kullanıcının oturumu kapatıp yeniden oturum açması ya da bilgisayarı yeniden başlatması gerekir.
  - **Yapılandırılmadı** (*varsayılan*)-ayar, simgeyi göstermek için istemciyi varsayılana döndürür.
  - **Evet** -Windows Güvenlik simgesini kullanıcılar sistem tepsisinden gizleyin.
  
- **Windows Güvenlik uygulamasındaki TPM 'YI Temizle seçeneğini devre dışı bırakın**  
  CSP: [Disablecleartpmbutton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, düğmeye erişime izin veren istemci varsayılan değerini döndürür.
  - **Evet** -Windows Güvenlik uygulamasındaki TPM 'yi temizle düğmesine erişimi devre dışı bırakın.

- **Güvenlik açığı bulunursa kullanıcılardan TPM bellenimini güncelleştirmesini iste**  
  CSP: [Disabletpmfirmwareupdatewarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kullanıcılara sorulacak olan istemci varsayılan değerini döndürür.
  - **Evet** -TPM belleniminde olası bir güvenlik açığı bulunduğunda Windows 'un son kullanıcılara sormaya izin ver. Daha sonra bu güvenlik açığını gidermek için bellenim güncelleştirmelerini çalıştırmaları önerilir.

- **Kuruluşun destek iletişim bilgileri**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  BT kuruluş bilgilerinizin Windows güvenlik uygulaması ve bildirimlerinde görüntülenmesini istediğiniz yeri bildirin.
  - **Yapılandırılmadı** (*varsayılan*)
  - **Uygulamada ve bildirimlerde görüntüle**
  - **Yalnızca uygulamada görüntüle**
  - **Yalnızca bildirimlerde görüntüle**