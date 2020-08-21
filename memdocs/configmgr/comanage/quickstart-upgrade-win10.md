---
title: Windows 10 ' a yükseltme
titleSuffix: Configuration Manager
description: Cihazları, ortak yönetim için gerekli olan Windows 10 sürüm 1709 veya sonraki sürümlere yükseltin
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d41a0806a33ac627eceaafab54c73c31ea013365
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694840"
---
# <a name="upgrade-windows-10-for-co-management"></a>Ortak yönetim için Windows 10 ' a yükseltme

Kuruluşunuzu ortak yönetime ekleme konusunda çalışırken, geçerli olan bazı müşteriler için önemli bir aceye sahip olursunuz. Ortak yönetim [Windows 10 sürüm 1709](/windows/whats-new/whats-new-windows-10-version-1709) veya üstünü gerektirir. Windows 'u güncelleştirdiğinizde ve otomatik kaydı yapılandırdıktan sonra, istemcileriniz otomatik olarak ortak yönetime kaydedilir.

Aşağıdaki videoda, üst düzey Program Yöneticisi ramiz York ve ürün pazarlama yöneticisi Locky Ainley, ortak yönetim için Windows 10 ' a yükseltmeyi ve tanıtımı sağlar:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Neden yükseltirsiniz?

Diğer Platform geliştirmeleri arasında Windows 10 sürüm 1709 ve üzeri otomatik kaydı destekler. Bu davranış, bir cihazın Azure Active Directory (Azure AD) katıldığında otomatik olarak Intune 'a kaydolmasını sağlar. 

Daha fazla bilgi için bkz. [Windows 10 otomatik kaydını etkinleştirme](/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Nasıl yapılır?

İşte binlerce müşterinin güncel hızla yararlanmasına yardımcı olmak için öğrendiğimiz bazı ipuçları:

- Bu yükseltmeyi doğru zamanlarda doğru kişilere almak için aşamalı dağıtımları kullanın. Daha fazla bilgi için bkz. [aşamalı dağıtımlar oluşturma](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Kullanıcı bekleme sürelerini azaltmak için ön önbelleğe alma özelliğini kullanın. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../osd/deploy-use/configure-precache-content.md).  

- Varsayılan yerinde yükseltme görev sırası şablonunu kullanın. Ardından, adımlarınızı ön ve yükseltme sonrası ve tüm hata eylemleri için yapılandırın. Daha fazla bilgi için, bkz. [işlem sonrası Için önerilen görev dizisi adımları](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- Ortamınızda yüksek düzeyde bir mobil iş gücü varsa, Configuration Manager bulut yönetimi ağ geçidi (CMG) üzerinden yerinde yükseltmeyi destekler. Bu özellik, internet tabanlı olduklarında Windows 10 istemcilerinizi yükseltmenize olanak tanır. CMG hakkında daha fazla bilgi için bkz. [CMG aracılığıyla Windows 10 yerinde yükseltme dağıtımı](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Erken benimseme yapmak isteyen kullanıcılar için ortak yönetim için bir katılım sunun. Bu yaklaşım ilk benimsemeyi hızlandırır. Bu kişileri önceden tanımlayarak, bir piyasaya çıkmanın erken günlerinde iyi tedarik sağlayabilirsiniz. Ayrıca, değişiklik için memnun olan ve daha sık kullanılan sürümlerde ilgilendiği kullanıcılardan doğrulama ve geri bildirim alırsınız. Erken benimseyen programları yeni teknolojilerde ilgi oluşturur ve zaman içinde boyut olarak büyür.  


## <a name="case-studies"></a>Örnek olay incelemeleri

Microsoft BT Microsoft 'un Windows 10 ' a 96.000 dağıtılmış kullanıcılarına dağıttı. Dağıtım hem uzak kullanıcıları hem de şirket ağındaki kullanıcıları içerir. Dağıtım dokuz hafta içinde tamamlandı. Deneyimi hakkında daha fazla bilgi için bkz. [Microsoft 'Ta Windows 10 ' u yerinde yükseltme olarak dağıtma](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

Büyük Avrupa yazılım üreticisi, erken benimseyen grubunu başarıyla kullanır. İlk test ve pilot gruplardan sonra, yaklaşık 2.000 çalışan ilk güncelleştirme, yükseltmeler ve yazılımları alır. Bu grup BT personelini ve tercih edilen gönüllü teers 'ı içerir. Kullanıcıları ile bu katılım düzeyi, test sırasında daha fazla güvenilirlik sağlar ve toplu piyasaya çıkarma başlamadan daha fazla güvenilirlik sağlar.



## <a name="contact-fasttrack"></a>FastTrack 'e başvurun

İşlemin herhangi bir noktasında Windows 10 yükseltmeniz ile ilgili yardıma ihtiyacınız varsa [Microsoft FastTrack](https://Microsoft.com/FastTrack/), oturum açın ve yardım isteyin. 

Daha fazla bilgi için bkz. [FastTrack 'ten yardım alın](quickstart-fasttrack.md).