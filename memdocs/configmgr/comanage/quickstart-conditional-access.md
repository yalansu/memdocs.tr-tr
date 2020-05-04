---
title: Ortak yönetim ile koşullu erişim
titleSuffix: Configuration Manager
description: Intune 'dan uyumluluk kurallarına göre kurumsal kaynaklara Kullanıcı erişimini denetleme
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711507"
---
# <a name="conditional-access-with-co-management"></a>Ortak yönetim ile koşullu erişim

Koşullu erişim, güvenilen uygulamaları kullanarak yalnızca güvenilen kullanıcıların güvenilen cihazlarda kuruluş kaynaklarına erişebilmesini sağlar. Bulutta sıfırdan oluşturulmuştur. Cihazları Intune ile yönetseniz veya Configuration Manager dağıtımınızı ortak yönetime genişleterek aynı şekilde çalışmaktadır.

Aşağıdaki videoda, üst düzey Program Yöneticisi Joey Glocke ve Product Marketing Manager Locky Ainley ile ortak yönetim ile koşullu erişim:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Ortak yönetim sayesinde Intune, ne kadar güvenilir olduğunu öğrenmek için ağınızdaki her cihazı değerlendirir. Bu değerlendirmeyi aşağıdaki iki şekilde yapar:

1. Intune, bir cihazın veya uygulamanın yönetilip ve güvenli bir şekilde yapılandırıldığından emin olmanızı sağlar. Bu denetim, kuruluşunuzun uyumluluk ilkelerini nasıl ayarlayadiğinize bağlıdır. Örneğin, tüm cihazların şifreleme özelliğinin etkinleştirildiğinden ve jailbreak uygulanmış olmadığından emin olun.  

    - Bu değerlendirme ön güvenlik ihlali ve yapılandırma tabanlıdır  

    - Ortak yönetilen cihazlar için Configuration Manager ayrıca yapılandırma tabanlı değerlendirme da yapmaz. Örneğin, gerekli güncelleştirmeler veya uygulamalar uyumluluğu. Intune bu değerlendirmeyi kendi değerlendirmesiyle birlikte birleştirir.  

2. Intune, bir cihazdaki etkin güvenlik olaylarını algılar. [Microsoft Defender Gelişmiş tehdit koruması](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (eski adıyla WINDOWS Defender ATP) ve diğer [Mobil tehdit savunma sağlayıcılarının](https://www.lookout.com/about/partners/microsoft)akıllı güvenliğini kullanır. Bu iş ortakları cihazlarda devam eden davranış analizini çalıştırır. Bu analiz etkin olayları algılar ve gerçek zamanlı uyumluluk değerlendirmesi için bu bilgileri Intune 'a geçirir.  

    - Bu değerlendirme, güvenlik sonrası ihlal ve olay tabanlı  

Microsoft Kurumsal Başkan Yardımcısı atacan Anderson, Ignite 2018 Keynote sırasında canlı tanıtımlar halinde koşullu erişimi ele alır. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Koşullu erişim Ayrıca, ağa bağlı tüm cihazların sistem durumunu görmek için size merkezi bir yer sağlar. Bulut ölçeğinden faydalanır, bu da özellikle Configuration Manager üretim örneklerinin test edilmesine önem taşır.


## <a name="benefits"></a>Avantajlar

Her BT ekibi, ağ güvenliği ile sorunsuz hale gelir. Ağınıza erişmeden önce her cihazın güvenlik ve iş gereksinimlerinizi karşıladığından emin olmak zorunludur. Koşullu erişimle aşağıdaki faktörleri belirleyebilirsiniz: 
- Her cihaz şifrelendiyse  
- Kötü amaçlı yazılım yüklenmişse  
- Ayarları güncelleştirilirse  
- Jailbreak uygulanmış veya kökü belirtilmişse  

Koşullu erişim, her yerden herhangi bir cihazdaki çalışan üretkenliğini en üst düzeye çıkaran bir kullanıcı deneyimiyle, Kurumsal veriler üzerinde ayrıntılı denetimi birleştirir.

Aşağıdaki videoda, [Gelişmiş Iş parçacığı korumasının](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) düzenli olarak karşılaşabileceğiniz yaygın senaryolarla nasıl tümleştirildiği gösterilmektedir:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Ortak yönetim sayesinde Intune, gerekli güncelleştirmeler veya uygulamalar için güvenlik standartları uyumluluğunuzu değerlendirmek üzere Configuration Manager sorumluluklarını birleştirebilirler. Bu davranış, karmaşık uygulama ve düzeltme eki yönetimi için Configuration Manager kullanmaya devam etmek isteyen herhangi bir BT kuruluşu için önemlidir.

Koşullu erişim Ayrıca, [sıfır güven ağ](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) mimarinizi geliştirmenin önemli bir parçasıdır. Koşullu erişim ile uyumlu cihaz erişim denetimleri, sıfır güven ağının temel katmanlarını kapsar. Bu işlevsellik, daha sonra kuruluşunuzun güvenliğini nasıl güvence altına alma işlemlerinin büyük bir parçasıdır.

Daha fazla bilgi için, [Microsoft Defender Gelişmiş tehdit koruması 'ndaki makine riski verileriyle koşullu erişimi geliştirmeyle](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559)ilgili blog gönderisine bakın.



## <a name="case-studies"></a>Örnek olay incelemeleri

BT danışmanlık firması, tüm 91.000 çalışanları tarafından kullanılan cihazları korumak ve yönetmek için koşullu erişim kullanır. Son bir örnek olarak, bu BT 'nin Başkan Yardımcısı, belirtilen Wipro 'de belirtilmiştir:

> *Koşullu erişimi elde etmek, Wipro için büyük bir kazandır. Şimdi tüm çalışanlarınızın isteğe bağlı bilgilere mobil erişimi vardır.* 
>  *Güvenlik sonrası ve çalışan üretkenliğinizi geliştirdik. Artık 91.000 çalışan, herhangi bir cihazdan, her yerden 100 ' ten fazla uygulamaya yüksek düzeyde güvenli erişimden faydalanır.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Diğer örnekler şunlardır: 

- 150.000 ' den fazla çalışan için uygulama tabanlı koşullu erişim kullanan Nestlé  

- Artık "yalnızca yönetilen cihazların takımlar ve şirketin intraneti gibi Office 365 uygulamalarına erişimi olduğundan" Otomasyon yazılım şirketi, temposunda. Ayrıca, iş gücünün "iş günü ve Salesforce gibi diğer bulut tabanlı uygulamalara daha güvenli erişimi" de sunabilir. " Temposunda 'ın Intune deneyimi hakkında daha fazla bilgi için, bkz. [temposunda Microsoft 365 ' deki mobil işbirliği araçlarıyla iş hızını artırır](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune ayrıca Cisco ıSE, Aruba Clear Pass ve Citrix NetScaler gibi iş ortaklarıyla tamamen tümleşiktir. Bu iş ortaklarıyla, Intune kaydına ve cihaz uyumluluk durumuna göre erişim denetimlerini bu platformlar arasında koruyabilirsiniz.

Daha fazla bilgi için aşağıdaki videoları inceleyin:
- [Atacan Anderson gösterileri koşullu erişimi ayrıntılı olarak](https://youtu.be/8321obNofgM?t=547)  
- [Uç nokta bölgesinden ek ayrıntılar 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Değer teklifi

Koşullu erişim ve ATP tümleştirmesi sayesinde, her BT kuruluşunun temel bir bileşenini yasakladığınızı görürsünüz: güvenli bulut erişimi.

Tüm veri ihlallerinin %63 ' inden fazlası, saldırganlar, zayıf, varsayılan veya çalınan Kullanıcı kimlik bilgileri aracılığıyla kuruluşun ağına erişim elde edebilir. Koşullu erişim, Kullanıcı kimliğini güvenli hale getirmek için odaklandığından, kimlik bilgisi hırsızlığını kısıtlar. Koşullu erişim ayrıcalıklı veya ayrıcalıksız olarak kimliklerinizi yönetir ve korur. Cihazları ve içerdikleri verileri korumanın daha iyi bir yolu yoktur.

Koşullu erişim Enterprise Mobility + Security (EMS) temel bileşeni olduğundan, şirket içi kurulum veya mimari gerekli değildir. Intune ve Azure Active Directory (Azure AD) ile, bulutta koşullu erişimi hızlıca yapılandırabilirsiniz. Şu anda Configuration Manager kullanıyorsanız, ortamınızı ortak yönetim ile kolayca buluta genişletebilir ve hemen kullanmaya başlayabilirsiniz.

ATP tümleştirmesi hakkında daha fazla bilgi için bkz. [Microsoft Defender ATP cihaz risk puanı yeni cybersaldýrı kullanıma sunuyor, ağları korumak Için koşullu erişim sağlar](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Gelişmiş bir korsan grubunun, görülmeyen araçlarla hiçbir şekilde nasıl kullanıldığını ayrıntılarıyla açıklamaktadır. Hedeflenen kullanıcıların koşullu erişimi olduğundan, Microsoft bulutu tespit etti ve durdurdu. Yetkisiz giriş, cihazın risk tabanlı koşullu erişim ilkesini etkinleştirdi. Saldırgan ağda zaten bir othold kurdu olsa da, yukarıda belirtilen makinelerin kurumsal hizmetlere ve Azure AD tarafından yönetilen verilere erişimi otomatik olarak kısıtlıdır.



## <a name="configure"></a>Yapılandırma

[Ortak yönetimi etkinleştirdiğinizde](how-to-enable.md)Koşullu erişimin kullanımı kolaydır. **Uyumluluk ilkeleri** Iş yükünü Intune 'a taşımayı gerektirir. Daha fazla bilgi için bkz. [Configuration Manager iş yüklerini Intune 'a değiştirme](how-to-switch-workloads.md). 

Koşullu erişimi kullanma hakkında daha fazla bilgi için aşağıdaki makalelere bakın: 

- [Azure AD’de koşullu erişim](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Intune cihaz uyumluluk ilkeleri](https://docs.microsoft.com/intune/device-compliance)  

- [Intune ile uygulama tabanlı koşullu erişim](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Koşullu erişim özellikleri, hibrit Azure AD 'ye katılmış cihazlar için hemen kullanılabilir hale gelir. Bu özellikler Multi-Factor Authentication ve hibrit Azure AD JOIN erişim denetimini içerir. Bu davranış, Azure AD özelliklerini temel alır. Intune ve Configuration Manager yapılandırma tabanlı değerlendirmede yararlanmak için ortak Yönetimi etkinleştirin. Bu yapılandırma, uyumlu cihazlar için doğrudan Intune 'dan erişim denetimi sağlar. Ayrıca Intune 'un uyumluluk ilkeleri değerlendirme özelliğini de sağlar.  

