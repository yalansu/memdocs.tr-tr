---
title: PowerShell betiği güvenliği hakkında daha fazla bilgi edinin
titleSuffix: Configuration Manager
description: PowerShell betiği güvenliği hakkında bilgi edinmenize yardımcı olacak kaynaklar.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075872"
---
# <a name="learn-more-about-powershell-script-security"></a>PowerShell betiği güvenliği hakkında daha fazla bilgi edinin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu, ortamınızdaki önerilen PowerShell ve PowerShell parametre kullanımını doğrulamak için yöneticinin sorumluluğundadır. Yöneticiler ve potansiyel risk yüzeyleri hakkında yöneticileri eğitmenize yardımcı olmak için bazı faydalı kaynaklar aşağıda verilmiştir. Bu, olası riskli yüzeyleri azaltmaya ve güvenli betiklerin kullanılmasına izin vermeyi sağlar.

## <a name="powershell-script-security"></a>PowerShell betiği güvenliği
Çalıştırma betiklerine yerleşik olarak, ortamda çalıştırılması istenen betikleri görsel olarak gözden geçirip onaylamaya yönelik bir özelliktir. Yöneticiler, kötü amaçlı betik olabilir ve betik onaylama işlemi sırasında görsel incelemeden algılanmak üzere kötü ve zor olan komut dosyası olabilir. En iyi uygulama olarak, PowerShell betiklerini görsel olarak gözden geçirmeye ek olarak, belirli denetim araçlarını kullanarak, şüpheli betiklerin sorunlarını algılamaya yardımcı olur. Bu araçlar, her zaman PowerShell yazarının amacını belirleyemez, bu nedenle şüpheli bir betiğe dikkat edebilir. Ancak, Araçlar yöneticinin kötü amaçlı veya isteyerek betik söz dizimi olduğunu kararlaştırmak için gerekli olacaktır.

## <a name="recommendations"></a>Öneriler
- Aşağıda başvurulan çeşitli bağlantıları kullanarak PowerShell güvenlik en iyi uygulamaları hakkında bilgi edinin.
- **Betiklerinizi imzalayın**: betikleri güvenli tutmak için başka bir yöntem, kullanım için içeri aktarmadan önce bunları daha sonra ve imzalanmış olacak.
- Gizli dizileri (parolalar gibi) PowerShell betiklerine depolamayın ve gizli dizileri işleme hakkında daha fazla bilgi edinin.


## <a name="general-information-about-powershell-security-best-practices"></a>PowerShell güvenlik en iyi uygulamaları hakkında genel bilgiler

Bu bağlantı koleksiyonu, PowerShell betiği güvenlik en iyi uygulamaları hakkında bilgi edinmek için Configuration Manager yöneticilerine bir başlangıç noktası vermek üzere seçilmiştir.  

[PowerShell güvenlik En Iyi uygulamalarına giriş](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell güvenlik En Iyi uygulamaları PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[PowerShell saldırılarına karşı savunma, PowerShell ekip blogu](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Bir Microsoft PowerShell ve güvenlik danışmanı eser Holmes ile PowerShell saldırılarına karşı savunma](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Kötü amaçlı kod eklenmesine karşı koruma](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[PowerShell mavi ekibi, derin betik bloğu günlüğü, korumalı olay günlüğü, kötü amaçlı yazılımdan koruma tarama arabirimi, güvenli kod oluşturma API 'Leri açıklanmaktadır](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Windows 10 için, kötü amaçlı yazılımdan koruma taraması arabirimi için bir API vardır](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>PowerShell parametreleri güvenliği
Parametreleri geçirme, betiklerle esneklik elde etmenin ve çalışma zamanına kadar kararların ertelenmesi için bir yoldur. Ayrıca, başka bir risk yüzeyi de açar. Kötü amaçlı parametreleri veya betiği ekleme işlemini engellemek için en iyi uygulamalar şunlardır:

- Yalnızca önceden tanımlanmış parametrelerin kullanılmasına izin verin.
- İzin verilen parametreleri doğrulamak için normal ifade özelliğini kullanın.
    - Örnek: yalnızca belirli bir değer aralığına izin veriliyorsa, yalnızca aralığı oluşturan karakterleri veya değerleri denetlemek için normal bir ifade kullanın.
    - Parametrelerin doğrulanması, kullanıcıların, tırnak işaretleri gibi belirli karakterleri kullanmaya çalışmasını önlemeye yardımcı olabilir. Birden çok tırnak türü olduğunu unutmayın. bu nedenle, hangi karakterlerin izin vermekte olduğunu doğrulamak için normal ifadeler kullanılması, izin verilmeyen tüm girdileri tanımlamaya çalışmaktan genellikle daha kolaydır.
- PowerShell Galerisi ["ekleme Hunter"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) PowerShell modülünden yararlanın.
    - Yanlış pozitif sonuçlar olabilir. bu nedenle, gerçek bir sorun olup olmadığını tespit etmek için bir şeyin şüpheli olarak işaretlenme amacını göz atın. 
- Microsoft Visual Studio, PowerShell söz dizimini denetlemeye yardımcı olabilecek bir betik Çözümleyicisi içerir.
- Bu video: "DEF CON 25-eser Holmes-Get $pwnd: saldırmayı sağlamlaştırılmış Windows Server", güvenlik altına alabileceğiniz sorun türlerine genel bir bakış sunar (özellikle 12:20 ile 17:50 arası bölüm):    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Ortam önerileri
PowerShell yöneticileri için genel öneriler.
1. Windows 10 ' da yerleşik olarak bulunan sürüm 5 veya üstü gibi en son PowerShell sürümünü dağıtın. Alternatif olarak, [Windows Management Framework 'ü](https://www.microsoft.com/download/details.aspx?id=54616)dağıtabilirsiniz. 
2. İsteğe bağlı olarak korumalı olay günlüğü dahil olmak üzere PowerShell günlüklerini etkinleştirin ve toplayın. Bu günlükleri imzalara, hunme ve olay yanıtı iş akışlarınıza ekleyin.
3. Yüksek değerli sistemlere, bu sistemlere kısıtlı yönetici erişimini ortadan kaldırmak veya azaltmak için yeterli yönetim uygulayın.
4. Önceden onaylanmış yönetim görevlerinin PowerShell dilinin tam yeteneklerini kullanmasına izin vermek için Windows Defender uygulama denetim ilkeleri dağıtın; etkileşimli ve onaylanmamış kullanımı, PowerShell dilinin sınırlı bir alt kümesiyle sınırlandırılmıştır.
5. Windows 10 ' un PowerShell 'i de içeren Windows Scripting konakları tarafından işlenen tüm içerik (çalışma zamanında oluşturulan veya devre dışı) ile tüm içeriğe tam erişim sağlamak için Windows 10 ' un dağıtımını yapın.
