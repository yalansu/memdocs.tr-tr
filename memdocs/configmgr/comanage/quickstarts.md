---
title: Ortak yönetim ile bulut bağlantısı
titleSuffix: Configuration Manager
description: Ortak yönetim, bunu etkinleştirdiğinizde anında değer sağlar.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ca960ddd6a4057da10341063f0b14a7f1d104d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075821"
---
# <a name="cloud-connecting-with-co-management"></a>Ortak yönetim ile bulut bağlantısı

![Blastoff serisi başlığı](media/blastoff-banner.png)

Ortak yönetim, mevcut Configuration Manager dağıtımınıza daha önce nasıl çalışabilmeniz gerekmeden yeni işlevsellik ekler. Ortak yönetimi etkinleştirdiğinizde, buluttan hemen faydalanmasını başlayabilirsiniz. Bu değeri, var olan yönetim altyapınıza ve süreçlerinize uygulayabilirsiniz.

Bu ortak yönetim hızlı başlangıç serisinde, nasıl hızlı bir şekilde yeni yönetim değeri sürücünüzü kullanabileceğinizi öğrenin. Ortak yönetim, şu anda kullanabileceğiniz özellik ve araçlar oluşturmak için oluşturulmuştur.

Aşağıdaki videoda, Microsoft Kurumsal Başkan Yardımcısı atacan Anderson bu ortak yönetim serisini tanıtır:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| Anlık değer | Başlarken |
|-----------------|-----------------|
| - [Koşullu erişim](#bkmk_ca)<br> - [Intune 'da uzak eylemler](#bkmk_remote)<br> - [İstemci sistem durumu](#bkmk_client-health)<br> - [Karma Azure AD](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Ortak yönetime yönelik yollar](#bkmk_paths)<br> - [Karma Azure AD ayarlama](#bkmk_setup-hybrid-aad)<br> - [Windows 10 ' a yükseltme](#bkmk_upgrade-win10)<br> - [FastTrack 'ten yardım alın](#bkmk_fasttrack) |

## <a name="immediate-value"></a>Anlık değer

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Cihaz uyumluluğuyla koşullu erişim** | Intune 'dan uyumluluk kurallarına göre şirket kaynaklarına Kullanıcı erişimini denetleme | [![Koşullu erişim videosunun küçük resmi](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**Intune 'da uzak eylemler** | Ortak yönetilen cihazlar için Intune 'da uzak eylemleri çalıştırın. Örneğin, bir cihazı silme ve sıfırlama ve kaydı ve hesabı koruma | [![Uzak eylemler videosu küçük resmi](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Configuration Manager istemci sistem durumu** | Azure portal Intune 'dan Configuration Manager istemci durumunun görünürlüğünü koruyun | [![İstemci sistem durumu videosunu küçük resmi](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Azure AD ile, hem bulutta hem de şirket içi ortamlarda, kaynaklarınız için kullanıcılarınıza ve güvenliğine yönelik geliştirilmiş verimliliğin avantajlarından yararlanabilirsiniz. | [![Karma Azure AD videonun küçük resmi](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Cihazları dağıtma, yönetme ve devre dışı bırakma veya geri dönüştürme ile ilişkili zamanı, kaynakları ve karmaşıklığı azaltın. Autopilot, son kullanıcılar için daha iyi bir deneyim da oluşturur. | [![Windows Autopilot video küçük resmi](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>Başlarken

Ortak yönetimi etkinleştirmek istiyorsanız, karşılaşabileceğiniz teknik kaygıları ortadan kaldırmak için Buradan başlayın.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Ortak yönetime yönelik yollar** | Ortak yönetimi ayarlamanıza yönelik iki temel yol vardır ve her bir yolun önkoşullarını anlamak önemlidir.  Her yol, Azure AD, ConfigMgr, Intune ve Windows istemcisinin bazı birleşimini gerektirir. | [![Ortak yönetim yollarının slaydının küçük resmi](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**Karma Azure AD ayarlama** | Ortamınızda Şu anda etki alanına katılmış Windows 10 cihazları varsa, ortak yönetimi etkinleştirebilmeniz için karma Azure AD 'yi ayarlayın | [![Karma Azure AD 'nin küçük resmi video kurulumu](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**Windows 10 ' a yükseltme** | Ortak yönetim için Windows 10 sürüm 1709 veya üzeri gereklidir | [![Windows 10 ' un yükseltme videosu küçük resmi](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**FastTrack 'ten yardım alın** | FastTrack organizasyonu, ortak yönetimi ayarlama da dahil olmak üzere tüm kuruluş türlerinin Microsoft 365 uygulamaları dağıtmasına yardımcı olmak için uzmanlaşan büyük bir Microsoft mühendisleri grubudur. | [![FastTrack videosunun küçük resmi](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
