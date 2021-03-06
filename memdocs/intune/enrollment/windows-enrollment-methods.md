---
title: Windows cihazları için Intune kayıt yöntemleri
titleSuffix: Microsoft Intune
description: Windows cihazlarını Intune 'A kaydedebilmeniz için kullanabileceğiniz farklı yolları öğrenin
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: ''
ms.openlocfilehash: c91c0f776ee46ddebbbb7bc27895b0f8795ae975
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911599"
---
# <a name="intune-enrollment-methods-for-windows-devices"></a>Windows cihazları için Intune kayıt yöntemleri

Intune 'da cihazları yönetmek için önce cihazların Intune hizmetine kaydolması gerekir. Kişisel ve şirkete ait cihazlar, Intune yönetimi için kaydedilebilir. 

Intune 'a kayıtlı cihazları almanın iki yolu vardır:
- Kullanıcılar, Windows bilgisayarlarını kendi kendilerine kaydedebilir 
- Yöneticiler, Kullanıcı katılımı olmadan otomatik kaydı zorlamak için ilkeleri yapılandırabilir

## <a name="user-self-enrollment-in-intune"></a>Intune 'da Kullanıcı kendini kaydetme

Kullanıcılar, aşağıdaki yöntemlerden herhangi birini kullanarak Windows cihazlarını kendi kendilerine kaydedebilir:

- [Kendi cihazını getir (](../user-help/enroll-windows-10-device.md)KCG): kullanıcılar, bu Işlemi **Şirket portalı uygulamayı** indirip yükleyerek kendi kişisel cihazlarını kaydetmeleri:
  - E-posta gibi kurumsal kaynağa erişim kazanmak için cihazı Azure Active Directory kaydeder.
  - Cihazı Intune 'A bir kişiye ait cihaz (KCG) olarak kaydeder.
Bir yönetici otomatik kaydı yapılandırmışsa (Azure AD Premium abonelikleri ile kullanılabilir), kullanıcının kimlik bilgilerini yalnızca bir kez girmesi gerekir. Aksi takdirde, yalnızca MDM kaydı aracılığıyla ayrı olarak kaydolmaları ve kimlik bilgilerini yeniden girmeniz gerekir.  
- **Yalnızca MDM kaydı** , kullanıcıların var olan bir çalışma grubunu, Active Directory veya Azure Active Directory 'ye KATıLMıŞ bir bilgisayarı Intune 'a kaydetmelerini sağlar. Kullanıcılar, mevcut Windows bilgisayarındaki ayarlardan kaydolmasını ister. Bu yöntem, cihazı Azure Active Directory 'ye kaydetmediği için önerilmez. Koşullu erişim gibi özelliklerin kullanılmasını da engeller.
- [Azure Active Directory (Azure AD) katılma](/azure/active-directory/user-help/user-help-join-device-on-network) -cihazı Azure Active Directory ile birleştirir ve KULLANıCıLARıN Azure AD kimlik bilgileriyle Windows 'da oturum açmasını sağlar. Otomatik kayıt etkinse cihaz otomatik olarak Intune 'A kaydedilir. Otomatik kayıt 'nin avantajı, Kullanıcı için tek adımlı bir işlemdir. Aksi takdirde, yalnızca MDM kaydı aracılığıyla ayrı olarak kaydolmaları ve kimlik bilgilerini yeniden girmeniz gerekir. Kullanıcılar bu şekilde, ilk Windows OOBE veya ayarlardan bu şekilde kaydolmalarını ister. Cihaz, Intune 'da şirkete ait cihaz olarak işaretlenir.
- [Autopilot](../../autopilot/enrollment-autopilot.md) -Azure AD JOIN 'i otomatikleştirir ve şirkete ait yeni cihazları Intune 'a kaydeder. Bu yöntem, kullanıma hazır deneyimi basitleştirir ve cihazlara özel işletim sistemi görüntüleri uygulama gereksinimini ortadan kaldırır. Yöneticiler, Autopilot cihazlarını yönetmek için Intune 'u kullanırken, ilkeler, profiller, uygulamalar ve daha fazlasını kaydolduktan sonra yönetebilir.  Dört tür Autopilot dağıtımı vardır: [kendi kendine dağıtım modu](/windows/deployment/windows-autopilot/self-deploying) (kiosks, dijital imza, veya paylaşılan bir cihaz için), [Kullanıcı odaklı mod](/windows/deployment/windows-autopilot/user-driven) (geleneksel KULLANıCıLAR için) ve BT personelinin, tam olarak yapılandırılması ve [mevcut cihazlara yönelik](/windows/deployment/windows-autopilot/existing-devices) olarak Windows 10 ' un en son sürümünü kolayca dağıtmanıza olanak sağlamak için bir Windows 10 PC 'nin ön [sağlamasını sağlar.](/windows/deployment/windows-autopilot/white-glove)

## <a name="administrator-based-enrollment-in-intune"></a>Intune 'da yönetici tabanlı kayıt

Yöneticiler, Kullanıcı etkileşimi gerektirmeyen kayıt için aşağıdaki yöntemleri ayarlayabilir:

- [Karma Azure AD katılım](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) , yöneticilerin karma Azure AD 'ye katılmış cihazları otomatik olarak kaydetmesi için Active Directory Grup İlkesi 'ni yapılandırmalarına olanak tanır.
- [Configuration Manager ortak yönetimi](/configmgr/comanage/overview) , yöneticilerin, ıntune ve Configuration Manager 'nin iki avantajına sahip olan mevcut Configuration Manager yönetilen cihazlarını Intune 'a kaydetmelerini sağlar.
- [Cihaz Kayıt Yöneticisi](device-enrollment-manager-enroll.md) (DEM) özel bir hizmet hesabıdır. DEM hesaplarının, yetkili kullanıcıların birden çok şirkete ait cihazı kaydetmesine ve yönetmesine izin veren izinleri vardır. Bu tür cihazlar örneğin satış noktası veya yardımcı uygulamalara uygundur ancak e-postaya veya şirket kaynaklarına erişmesi gereken kullanıcılar için uygun değildir. Bu yöntem, koşullu erişim gibi özelliklerin kullanılmasına izin vermez. 
- [Toplu kayıt](windows-bulk-enroll.md) , yetkili bir kullanıcının çok sayıda yeni şirkete ait cihazı Azure Active Directory ve Intune 'a katılılabilmesi için izin verir. Windows yapılandırma Tasarımcısı (WCD) uygulamasıyla bir sağlama paketi oluşturun. Daha sonra, ilk Windows OOBE deneyimi sırasında veya mevcut Windows PC 'den USB medyası kullanarak cihazları Intune 'a otomatik olarak kaydetmek için sağlama paketini yüklersiniz. Bu yöntem Koşullu erişimin kullanılmasına izin vermez.
- Windows [IoT çekirdek cihazlarını](/windows/iot-core/manage-your-device/intunedeviceenrollment) kaydetmek, Windows IoT çekirdek Panosu kullanılarak, cihazı hazırlamak için ve ardından Windows yapılandırma Tasarımcısı kullanılarak bir sağlama paketi oluşturmak için gerçekleştirilir. Ardından, ilk önyükleme sırasında SD kart medyasını kullanarak cihazları Intune 'a otomatik olarak kaydetmek için sağlama paketini yükler.

## <a name="next-steps"></a>Sonraki adımlar

[Windows kayıt yöntemlerinin yeteneklerini öğrenin](enrollment-method-capab.md)