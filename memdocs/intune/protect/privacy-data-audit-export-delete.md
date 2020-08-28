---
title: Kişisel verileri denetleme, dışarı aktarma veya silme
titleSuffix: Microsoft Intune
description: Kişisel verileri denetleme, dışarı aktarma veya silme hakkında bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 96990be0-eb1e-43a4-a0e4-09c7dbdc2bf4
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2bdf057893ff24cd4bc5b671d53fbb5c75f597f5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996002"
---
# <a name="audit-export-or-delete-personal-data-in-intune"></a>Intune’da kişisel verileri denetleme, dışarı aktarma veya silme

Intune yöneticileri, denetim günlükleriyle ilgili kişisel verileri etkinlik izlemek için kullanabilir. Yöneticiler ayrıca kişisel verileri dışarı aktarabilir ve silebilir.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## <a name="audit-personal-data"></a>Kişisel verileri denetleme

Denetim günlükleri, kiracı yöneticilerine Microsoft Intune’da değişiklik yaratan etkinliklerin kaydını sağlar. Denetim günlükleri, birçok yönetim etkinliği için mevcuttur ve genellikle eylem oluşturur, güncelleştirir (düzenler), siler ve atar. Denetim olayları oluşturan kaldırma görevleri de gözden geçirilebilir. Bu denetim günlükleri, cihazları Intune’da kayıtlı olan kullanıcıların kişisel verilerini içerebilir.  

Intune, güvenlik nedeniyle kullanıcı ve cihaz eylemleri için denetim günlüklerini bir yıllık bir süre boyunca tutabilir. Bu günlükler, bir yıllık saklama döneminden sonra otomatik olarak silinir.

Denetim günlüklerini gözden geçirmek için bkz. [Intune etkinlikleri için denetim günlükleri](../fundamentals/monitor-audit-logs.md). 

Yöneticiler denetim günlüklerini silemiyor.

Bu denetim olayları, bir yıl boyunca saklanır. Kiracı yöneticileri, [bu destek isteği formunu](https://privacy.microsoft.com/en-US/privacy-questions?) kullanarak denetim günlüklerini isteyebilir.

## <a name="export-personal-data"></a>Kişisel verileri dışarı aktarma

Yöneticiler; hesaplar, hizmet verileri ve ilişkili günlükler dahil olmak üzere son kullanıcı kişisel verilerini Veri Sahibi Hakları istekleri doğrultusunda dışarı aktarabilir. Bu, siz ve kuruluşunuza, verileri kişisel verilerin bir kopyası ile mi sağlayacağınıza, yoksa bunu vermeyle ilgili yasal bir iş nedeniniz mi olduğunu belirlemek için de kullanabilirsiniz. Verileri sağlamaya karar verirseniz asıl belgenin bir kopyasını, uygun şekilde redakte edilmiş halini veya paylaşmaya uygun gördüğünüz kısımların ekran görüntüsünü veri sahibiyle paylaşabilirsiniz.

Bir kullanıcının kişisel verilerini dışarı aktarmak için şunu kullanabilirsiniz: 
- Cihazlar listesini dışarı aktarmak için Intune MDM Cihaz dikey penceresi. Cihaz verilerini doğrudan da kopyalayabilirsiniz.
- [Export-IntuneData.ps1 betiği](https://aka.ms/intunedataexport).

## <a name="delete-end-user-personal-data"></a>Son kullanıcı kişisel verilerini silme

Kişisel verileri Intune yönetiminden kaldırmanın üç yolu vardır:
- Azure Active Directory’den kullanıcıyı silme
- Cihazı fabrika ayarlarına sıfırlamak
- Kullanıcının kendisini kaldırması

### <a name="delete-a-user-from-intune"></a>Intune’dan kullanıcı silmek

Son kullanıcının Intune 'daki kişisel verilerini silmek için bir yöneticinin [kullanıcıyı Azure Active Directory (AAD) ' dan silmesi](/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user)gerekir. Kullanıcı AAD 'den (kalıcı olarak silindi) silindiğinde, Intune, AAD 'den silme sinyali alır ve bu kullanıcının tüm kişisel verilerini Intune hizmetinden temizlemeyi otomatik olarak başlatır. Kullanıcının bilgileri, kaldırma eyleminin 30 gün içinde Intune hizmetinden silinir.

### <a name="reset-device-to-factory-settings"></a>Cihazı fabrika ayarlarına sıfırlama
Fabrika ayarlarına sıfırlama, tüm şirkete ait ve kişisel veri ve ayarlar yerine orijinal fabrika ayarlarını geri yükler. Bu, cihazı yeni bir çalışana vermek için kullanışlıdır. Kullanıcı dosyaları, kullanıcının yüklediği uygulamalar ve varsayılan olmayan ayarlar kaldırılır ve bu veriler kaldırma eylemini izleyen 30 gün içerisinde Intune hizmetinden silinir.

### <a name="user-self-removal-from-intune-management"></a>Kullanıcının kendisini Intune yönetiminden kaldırması
Kullanıcılar, yönetici yardımı olmadan kendi [Android, Apple veya Windows](../user-help/unenroll-your-device-from-intune-android.md) cihazlarını Intune’dan kaldırabilir.   

### <a name="retire"></a>Devre Dışı Bırakma
**Kullanımdan kaldırma** eylemi; şirket uygulamaları, Intune'un yönettiği uygulamalara ilişkin veriler, ilke ayarları ve Intune yoluyla sağlanan e-posta profilleri gibi Intune tarafından sağlanan verileri kaldırır. Bu eylem, kullanıcının kişisel verilerini cihazda bırakır.

### <a name="delete-a-tenant-from-microsoft-intune"></a>Microsoft Intune’dan kiracı silme

Bir Intune kiracısı Intune hesabını iptal ederse, Intune hesabının kapatılmasını izleyen 180 gün içerisinde tüm kiracı verileri silinir. Azure AD kiracısı diğer Microsoft Enterprise abonelikleri (Azure, Microsoft 365) ile ilişkiliyse, yalnızca Intune müşteri verileri silinir. Azure AD kiracı kaynağı diğer abonelikler tarafından kullanılmak üzere tutulur. Intune hesabı Azure AD kiracısı ile ilişkilendirilen tek abonelik ise, kiracı silinir ve tüm kaynaklar ve müşteri verileri de silinir.

## <a name="next-steps"></a>Sonraki adımlar

Intune’da kişisel verileri [denetleme, dışarı aktarma ve silme](privacy-data-audit-export-delete.md) hakkında bilgi edinin.