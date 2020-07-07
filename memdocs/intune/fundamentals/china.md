---
title: Çin'de 21Vianet tarafından çalıştırılan Intune
titleSuffix: ''
description: Çin 'de 21Vianet tarafından işletilen Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: f82664cbc9f6970d494945cfdf6fc72e8d95ae8b
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.contentlocale: tr-TR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022356"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Çin'de 21Vianet tarafından çalıştırılan Intune  

21Vianet tarafından işletilen Intune, Çin 'de güvenli, güvenilir ve ölçeklenebilir bulut hizmetleri gereksinimlerini karşılayacak şekilde tasarlanmıştır. Hizmet olarak Intune, Microsoft Azure üzerine kurulmuştur. 21Vianet tarafından çalıştırılan Microsoft Azure, Çin 'de bulunan bulut hizmetleri 'nin fiziksel olarak ayrılmış bir örneğidir. Bu, 21Vianet tarafından bağımsız olarak çalıştırılır ve işlem yapılır. Bu hizmet, Microsoft 'un 21Vianet 'e lisansladığı teknolojide desteklenir.

Microsoft, hizmetin kendisini işlemez. 21Vianet, hizmetin teslimini sağlar, sağlar ve yönetir. 21Vianet, Çin 'deki bir Internet veri merkezi hizmetleri sağlayıcısıdır. Barındırma, yönetilen ağ hizmetleri ve bulut bilgi işlem altyapısı Hizmetleri sağlar. 21Vianet, Microsoft teknolojilerini lisanslayarak, verilerinizi Çin 'de tutarken Intune hizmetini kullanma olanağı sunmak için yerel veri merkezleri sunmaktadır. 21Vianet Ayrıca aboneliğiniz, faturalandırma ve destek hizmetlerinizi de sağlar.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>21Vianet tarafından işletilen Intune 'da özellik farklılıkları

Çin Hizmetleri, Çin 'nin içinden bir iş ortağı tarafından işletiğinden, Intune ile ilgili bazı özellik farklılıkları vardır. 

- 21Vianet tarafından işletilen Intune yalnızca tek başına dağıtımları destekler. System Center Configuration Manager ile ortak yönetim desteği şu anda geliştirme aşamasındadır.
- Genel bulutlardan bağımsız bulutlarına geçiş desteklenmez. 21Vianet tarafından işletilen Intune 'a geçmeyi ilgilenen müşterilerin el ile geçirilmesi gerekir.
- Kiracı iliştirme özelliği (bulut konsol senaryolarını desteklemek için kayıt olmadan cihazları Intune 'a eşitleme) Şu anda desteklenmiyor.
- 21Vianet tarafından işletilen Intune Intune aracısını desteklemez, bu nedenle eski PC yönetimini desteklemez.
- Windows 10 ' un yönetimi modern MDM kanalı kullanılarak desteklenir.
- 21Vianet tarafından işletilen Intune şirket içi Exchange bağlayıcısını desteklemez.
- Windows Autopilot ve Iş Mağazası özellikleri şu anda kullanılamıyor.
- Google Mobile Services Çin 'de kullanılamadığından, 21Vianet tarafından çalıştırılan Intune 'da müşteriler Google Mobile Services gerektiren özellikleri kullanamaz. Bu özellikler şunlardır:
  - SafetyNet cihaz kanıtlama gibi özellikleri koruma Google Play.
  - Google Play Store uygulamaları yönetme.
  - Android kurumsal özellikleri. Daha fazla bilgi için bu [Google belgelerine](https://support.google.com/work/android/answer/6270910?hl=en)bakın.
- Android için Intune Şirket Portalı uygulaması, Microsoft Intune hizmetiyle iletişim kurmak için Google Mobile Services kullanır. Çin 'de Google Play hizmetleri kullanılamadığından, bazı görevlerin tamamlanabilmesi için 8 saate kadar süre gerekebilir. Daha fazla bilgi için bu [makaleye](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable)bakın. 
- Yerel düzenlemeleri izlemek ve gelişmiş işlevsellik sağlamak için, Intune istemci deneyimi (Şirket Portalı uygulaması) Çin 'de farklılık gösterebilir.
- Sınırlama kullanılamıyor.
- Mobil uygulama yönetimi (MAM) kullanılabilirliği, Çin Halk Cumhuriyeti 'nde mevcut olan uygulamalar üzerinde şartlı bir uygulamadır.

## <a name="you-control-customer-data"></a>Müşteri verilerini kontrol edersiniz

Microsoft Azure, Intune, Office 365 ve 21Vianet tarafından çalıştırılan Power BI, verileriniz üzerinde tam denetime sahip olursunuz:
- Müşteri verilerinin nerede bulunduğunu bilirsiniz.
- Müşteri verilerinize erişimi kontrol edersiniz.
- Hizmeti bıraktığınızda müşteri verilerinizi denetlersiniz.
- Müşteri verilerinizin güvenliğini denetleme seçenekleriniz vardır.

Microsoft Azure, Intune, Office 365 ve 21Vianet tarafından çalıştırılan Power BI, verilerinizin sahibidir:
- 21Vianet, müşteri verilerini reklamcılık için kullanmaz.
- Müşteri verilerinize kimlerin erişebileceğini denetlersiniz.
- Her müşterinin verisini ayırmak için mantıksal yalıtım kullanıyoruz.
- Basit, saydam veri kullanımı ilkeleri sunuyoruz ve bağımsız denetimler ediniyoruz.
- Yüklenicimiz, gizlilik gereksinimlerinizi karşılamak için sözleşme aşamasındadır.

## <a name="data-subject-requests"></a>Veri konu istekleri

21Vianet tarafından işletilen Intune için Kiracı Yöneticisi rolü, veri konularıyla ilgili verileri aşağıdaki yollarla isteyebilir:

- Azure Active Directory Yönetim merkezini kullanarak bir Kiracı Yöneticisi, Azure Active Directory ve ilgili hizmetlerden bir veri konusunun kalıcı olarak silinmesine neden olabilir. Daha fazla bilgi için bkz. [Azure veri konu istekleri-silme](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- 21Vianet tarafından çalıştırılan Microsoft Hizmetleri için sistem tarafından oluşturulan Günlükler, veri günlüğü dışarı aktarma kullanılarak kiracı yöneticileri tarafından dışarı aktarılabilir. Daha fazla bilgi için bkz. [Azure veri konu istekleri-dışarı aktarma](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export).

## <a name="next-steps"></a>Sonraki adımlar

[Intune tarafından desteklenen konfigürasyonlar hakkında daha fazla bilgi edinin](supported-devices-browsers.md)