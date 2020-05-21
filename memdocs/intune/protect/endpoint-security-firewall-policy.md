---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle güvenlik duvarı ayarlarını yönetme | Microsoft Docs
description: Microsoft Endpoint Manager 'daki Endpoint Security Güvenlik Duvarı ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırın ve dağıtın.
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
ms.openlocfilehash: f98d7a30d219aee63e38a63a74d8f1713deb198a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431296"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için güvenlik duvarı ilkesi

MacOS ve Windows 10 çalıştıran cihazlar için yerleşik bir güvenlik duvarı yapılandırmak üzere Intune 'daki uç nokta güvenliği güvenlik duvarı ilkesini kullanın. Yerleşik güvenlik duvarları, Windows cihazları için BitLocker ve macOS için dosya Kasası ' nı içerir.

Cihaz yapılandırması için Endpoint Protection profillerini kullanarak aynı güvenlik duvarı ayarlarını yapılandırabilmeniz da, cihaz yapılandırma profilleri ek ayar kategorileri içerir. Bu ek ayarlar güvenlik duvarları ile ilgisiz değildir ve ortamınız için yalnızca güvenlik duvarı ayarlarını yapılandırma görevini karmaşıklaştırabilir.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde *Yönet* bölümündeki güvenlik duvarları için uç nokta güvenlik ilkelerini bulun.

[Güvenlik duvarı profillerinin ayarlarını](../protect/endpoint-security-Firewall-profile-settings.md)görüntüleyin.

## <a name="prerequisites-for-firewall-profiles"></a>Güvenlik Duvarı profilleri için Önkoşullar

- Windows 10 veya üzeri
- Tüm desteklenen macOS sürümleri

## <a name="firewall-profiles"></a>Güvenlik Duvarı profilleri

**MacOS profilleri**:

- **MacOS güvenlik duvarı** – MacOS 'ta yerleşik güvenlik duvarının ayarlarını etkinleştirin ve yapılandırın.

**Windows 10 profilleri**:

- **Microsoft Defender güvenlik duvarı** – Gelişmiş Güvenlik Özellikli Windows Defender güvenlik duvarı ayarlarını yapılandırın. Windows Defender güvenlik duvarı, bir cihaz için ana bilgisayar tabanlı ve iki yönlü ağ trafiği filtrelemesi sağlar ve yerel cihazdan gelen veya giden yetkisiz ağ trafiğini engelleyebilir.

- **Microsoft Defender güvenlik duvarı kuralları** *(Önizleme)* -belirli bağlantı noktaları, protokoller, uygulamalar ve ağlar dahil olmak üzere ayrıntılı güvenlik duvarı kuralları tanımlayın ve ağ trafiğine izin verebilir veya bu trafiği engelleyin. Bu profilin her örneği en fazla 150 özel kuralı destekler.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Güvenlik duvarı kuralı birleşmeleri ve ilke çakışmaları

Yalnızca bir ilke kullanarak bir cihaza uygulanacak güvenlik duvarı ilkelerini planlayın. Tek bir ilke örneği ve ilke türü kullanımı, iki ayrı ilkenin aynı ayara farklı yapılandırmalara sahip olmasını önlemeye yardımcı olur ve bu da çakışmalar oluşturur. İki ilke örneği veya farklı değerlerle aynı ayarı yöneten ilke türleri arasında bir çakışma olduğunda, ayar cihaza gönderilmez.

- Bu ilke çakışması biçimi, diğer Microsoft Defender güvenlik duvarı profilleriyle çakışabilecek **Microsoft Defender güvenlik** duvarı profili veya cihaz yapılandırması gibi farklı bir ilke türü tarafından sunulan bir güvenlik duvarı yapılandırması için geçerlidir.

  Microsoft *Defender Güvenlik Duvarı profilleri* , *Microsoft Defender güvenlik duvarı kuralları* profilleriyle çakışmaz.

**Microsoft Defender güvenlik duvarı kuralları** profillerini kullandığınızda, aynı cihaza birden çok kural profili uygulayabilirsiniz. Ancak, farklı yapılandırmalara sahip aynı şey için farklı kurallar varsa, her ikisi de cihaza gönderilir ve bu cihazda bir çakışma oluşturur.

- Örneğin, bir kural güvenlik duvarı aracılığıyla *takımlar. exe* ' yi engelliyorsa ve ikinci bir kural *takımlar. exe*' ye izin veriyorsa, her iki kural de istemciye dağıtılır. Bu sonuç, güvenlik duvarı ayarları için diğer ilkeler kullanılarak oluşturulan çakışmalarla farklıdır.

Birden çok kural profilinden gelen kurallar birbirleriyle çakışmadığı zaman, cihazlar her bir profildeki kuralları birleştirerek cihazda birleştirilmiş bir güvenlik duvarı kuralı yapılandırması oluşturur. Bu davranış, her bir profilin bir cihaza desteklediği 150 kurallarından fazlasını dağıtmanıza olanak sağlar.

- Örneğin, iki Microsoft Defender güvenlik duvarı kuralı profilleriniz vardır. İlk profil, güvenlik duvarı üzerinden *takımlar. exe* ' ye izin verir. İkinci profil, güvenlik duvarı üzerinden *Outlook. exe* ' ye izin verir. Bir cihaz her iki profili de aldığında, cihaz her iki uygulama için de güvenlik duvarından geçmesine izin verecek şekilde yapılandırılır.

## <a name="next-steps"></a>Sonraki adımlar

[Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
