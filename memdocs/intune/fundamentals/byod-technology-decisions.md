---
title: EMS ile KCG için teknoloji kararları
description: KCG'yi etkinleştirmeye ve şirket verilerini Microsoft Enterprise Mobility + Security ile korumaya yönelik önemli teknoloji kararları.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 12/8/2017
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 297926f6-c029-4003-bda4-9ee031d47dda
ms.reviewer: pfetty
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a264b9a3b8f0ba15debe7e7323c106f09fa12c6
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455251"
---
# <a name="technology-decisions-for-enabling-byod-with-microsoft-enterprise-mobility--security-ems"></a>KCG'yi Microsoft Enterprise Mobility + Security (EMS) ile etkinleştirmeye yönelik teknoloji kararları

Çalışanların uzaktan kendi cihazlarında çalışmalarını (BYOD) sağlama stratejinizi geliştirirken, KCG'yi etkinleştirme ve şirket verilerinizi koruma senaryolarında önemli kararlar vermeniz gerekir. Neyse ki, EMS kapsamlı bir çözüm kümesinde ihtiyacınız olan özelliklerin tümünü sunar.  

Bu konu başlığı altında, şirket e-postasına KCG erişimini etkinleştirme örneğini inceliyoruz. Tüm cihazı mı yoksa yalnızca tam olarak geçerli olan uygulamaları mı yönetmeniz gerektiği hakkında odaklanacağız.

## <a name="assumptions"></a>Varsayımlar
* Azure Active Directory ve Microsoft Intune hakkında temel bilgilere sahipsiniz
* E-posta hesaplarınız Exchange Online'da barındırılıyor

## <a name="common-reasons-to-manage-the-device-mdm"></a>Cihazı yönetmek için yaygın nedenler (MDM)
Exchange Online 'da [koşullu erişim](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) ilkesi dağıtarak, kullanıcıların cihazlarını cihaz yönetimine kaydetmelerini kolayca sağlayabilirsiniz. Aşağıdaki nedenlerle kişisel cihazları yönetmek isteyebilirsiniz:

**WiFi/VPN** – Kullanıcılarınızın üretken olmak için bir şirket bağlantı profiline ihtiyaçları varsa, bu rahatça yapılandırılabilir.

**Uygulamalar** – Kullanıcılarınızın cihazlarına gönderilecek bir dizi uygulamaya ihtiyaçları varsa, bu rahatça sağlanabilir. Mobile Threat Defense uygulaması gibi güvenlik amaçlarıyla ihtiyacınız olabilecek uygulamalar da bunlara dahildir.

**Uyumluluk** – Bazı kuruluşların belirli MDM denetimlerini çağıran yasal düzenleme ilkelerine veya başka ilkelere uyumlu olması gerekir. Örneğin, cihazın tamamını şifrelemek veya cihazdaki tüm uygulamaların raporunu oluşturmak için MDM gerekir.

## <a name="common-reasons-to-only-manage-the-apps-mam"></a>Yalnızca uygulamaları yönetmek için yaygın nedenler (MAM)
MDM olmadan MAM, KCG'yi destekleyen kuruluşlar arasında çok yaygındır. Exchange Online 'da koşullu erişim ilkesi dağıtarak, kullanıcıları Outlook Mobile 'dan (MAM korumalarını destekler) e-postaya erişmek için kullanabilirsiniz. Aşağıdaki nedenlerle yalnızca kişisel cihazlardaki uygulamaları yönetmek isteyebilirsiniz:

**Kullanıcı deneyimi** – MDM kaydı birçok uyarı istemi içerir (bunlar platform tarafından zorunlu tutulur) ve sonuçta çoğunlukla kullanıcı kendi kişisel cihazından e-postaya hiç erişmemeye karar verebilir. MAM kullanıcılara çok daha az uyarı verir; yalnızca bir kez açılan kutuyla MAM korumalarının yürürlükte olduğu bildirilir.

**Uyumluluk** – Bazı kuruluşların, kişisel cihazlarda daha az yönetim özelliği gerektiren ilkelerle uyumlu olması gerekir. Örneğin, MDM cihazdan tüm verileri kaldırabilirken MAM yalnızca uygulamalardan şirket verilerini kaldırabilir.

![Mobil cihazlarda cihaz yönetimiyle uygulama yönetimini karşılaştıran resim](./media/byod-technology-decisions/byod-app-device-mgmt.png)

[Cihaz yönetimi ve uygulama yönetimi yaşam döngüleri](device-lifecycle.md) hakkında daha fazla bilgi edinin.

## <a name="mdm-vs-mam-capability-comparison"></a>MDM ile MAM özellik karşılaştırması
Daha önce belirtildiği gibi, koşullu erişim bir kullanıcıyı cihazlarını kaydetmek veya Outlook Mobile gibi yönetilen bir uygulama kullanmak için kullanabilir. Her iki durumda birçok başka koşul da uygulanabilir, örneğin:

* Erişmeye çalışan kullanıcı
* Konumun güvenilir olup olmadığı
* Oturum açma riski düzeyi
* Cihaz platformu

Yine de birçok kuruluşun ilgilendikleri belirli riskleri vardır.  Aşağıdaki tabloda yaygın endişeler ve MDM ile MAM'nin bunlara yanıtı listelenir.

| Endişe   |   MDM  |   MAM  |
|------------|--------|--------|
|Verilere yetkisiz erişim | grup üyeliği gerektirme | grup üyeliği gerektirme |
|Verilere yetkisiz erişim | Cihaz kaydı gerektirme | Korumalı uygulama gerektirme |
|Verilere yetkisiz erişim | Belirli bir konum gerektirme | Belirli bir konum gerektirme |
| | | |
|Ele geçirilen kullanıcı hesabı| MFA gerektirme | MFA gerektirme|
|Ele geçirilen kullanıcı hesabı | Yüksek riskli kullanıcıları engelleme | Yüksek riskli kullanıcıları engelleme |
|Ele geçirilen kullanıcı hesabı | Cihaz PIN'i | Uygulama PIN'i |
| | | |
| Güvenliği aşılmış cihaz veya uygulama | Uyumlu cihaz gerektirir | Uygulama başlatıldığında jailbreak/kök denetimi |
| Güvenliği aşılmış cihaz veya uygulama | Cihaz verilerini şifreleme | Uygulama verilerini şifreleme |
| | | |
|Kayıp veya çalınan cihaz | Tüm cihaz verilerini kaldırma | Tüm uygulama verilerini kaldırma|
| | | |
| Verileri yanlışlıkla paylaşma veya güvenli olmayan konumlara kaydetme | Cihaz verileri yedeklemesini kısıtlama | Kuruluş verilerinin yedeklemelerini kısıtla |
| Verileri yanlışlıkla paylaşma veya güvenli olmayan konumlara kaydetme | Farklı kaydetme işlemini kısıtlama | Farklı kaydetme işlemini kısıtlama |
|Verileri yanlışlıkla paylaşma veya güvenli olmayan konumlara kaydetme | Yazdırmayı devre dışı bırak | Kuruluş verilerinin yazdırılmasını devre dışı bırak |

## <a name="next-steps"></a>Sonraki adımlar
Artık cihaz yönetimine, uygulama yönetimine veya ikisinin birleşimine odaklanarak kuruluşunuzda BYOD 'yi etkinleştirip etkinleştirmemeye karar vereceğiz. Nasıl hayata geçireceğiniz konusunda kararı siz verirsiniz ve bu arada da Azure AD'de sağlanan kimlik ve güvenlik özelliklerinin yine sağlanacağından emin olabilirsiniz.  

Planlamanızda bir sonraki düzeyi belirlemek için Intune [Planlama Kılavuzu](planning-guide.md)'nu kullanın.
