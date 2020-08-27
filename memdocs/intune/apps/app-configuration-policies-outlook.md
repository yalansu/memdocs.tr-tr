---
title: Intune ile iOS ve Android için Outlook 'U yönetme
description: İOS ve Android için Outlook ile Intune uygulama koruma ve yapılandırma ilkelerini kullanarak, ekip işbirliği deneyimlerinin yerinde korumalar için her zaman erişilebilir olmasını sağlayın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90bbc3bfbe4f7e6120359f86ad9cb1c55b2ed500
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907795"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>İOS ve Android için Outlook 'U kullanarak mesajlaşma işbirliği erişimini yönetme Microsoft Intune

İOS ve Android için Outlook uygulaması, kuruluşunuzdaki kullanıcıların e-posta, takvim, kişiler ve diğer dosyaları bir araya getirerek mobil cihazlarından daha fazlasını gerçekleştirmelerine olanak tanımak üzere tasarlanmıştır.

Office 365 verileri için zengin ve en geniş koruma özellikleri, koşullu erişim gibi Microsoft Intune ve Azure Active Directory Premium özellikleri de içeren Enterprise Mobility + Security Suite 'e abone olduğunuzda kullanılabilir. En azından, mobil cihazlardan iOS ve Android için Outlook 'a bağlantı sağlayan bir koşullu erişim ilkesi ve işbirliği deneyiminin korunmasını sağlayan bir Intune uygulama koruma ilkesi dağıtmanız gerekir.

## <a name="apply-conditional-access"></a>Koşullu erişim Uygula
Kuruluşlar, kullanıcıların yalnızca iOS ve Android için Outlook 'U kullanarak iş veya okul içeriğine erişebildiğinden emin olmak için Azure AD koşullu erişim ilkelerini kullanabilir. Bunu yapmak için tüm olası kullanıcıları hedefleyen bir koşullu erişim ilkesine ihtiyacınız olacaktır. Bu ilkeyi oluşturma hakkındaki ayrıntılar, [bulut uygulaması Için koşullu erişimle uygulama koruma Ilkesi iste](/azure/active-directory/conditional-access/app-protection-based-conditional-access)' de bulunabilir.

1. "Adım 1: Office 365 için Azure AD koşullu erişim ilkesi yapılandırma" yı izleyin [. Senaryo 1: office 365 uygulamaları](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), IOS ve Android için Outlook 'a izin veren ve OAuth özellikli Exchange ActiveSync Istemcilerinin Exchange Online 'a bağlanmasını engelleyen uygulama koruma ilkeleriyle onaylanan uygulamalar gerektirir.

   > [!NOTE]
   > Bu ilke, mobil kullanıcıların tüm Office uç noktalarına ilgili uygulamaları kullanarak erişmesini sağlar.

2. "2. Adım: bir Azure AD koşullu erişim ilkesini ActiveSync (EAS) ile Exchange Online için yapılandırma" adlı [Senaryo 1: Office 365 uygulamaları, uygulama koruma ilkeleriyle onaylanan uygulamalar gerektirir](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies). Bu, temel kimlik doğrulaması kullanan Exchange ActiveSync Istemcilerinin Exchange Online 'a bağlanmasını engeller.

   Yukarıdaki ilkeler, erişim izni vermeden önce iOS ve Android için Outlook 'Ta ilişkili hesaba bir Intune Uygulama Koruması Ilkesinin uygulanmasını sağlayan [uygulama koruması gerektir Ilkesi gerektirir](/azure/active-directory/active-directory-conditional-access-technical-reference). Kullanıcı bir Intune Uygulama Koruması Ilkesine atanmamışsa, Intune için lisanslı değildir veya uygulama Intune Uygulama Koruması Ilkesine dahil edilmemişse, ilke kullanıcının bir erişim belirteci almasını ve mesajlaşma verilerine erişim sağlamasını önler.

3. Son olarak, iOS ve Android cihazlarda diğer Exchange protokolleri için eski kimlik doğrulamasını engellemek üzere [koşullu erişim Ile Azure AD 'de eski kimlik doğrulamasını engelleme](/azure/active-directory/conditional-access/block-legacy-authentication) konusuna uyun; Bu ilke yalnızca Office 365 Exchange Online Cloud App ve iOS ve Android cihaz platformlarını hedeflemelidir. Bu, Exchange Web Hizmetleri, ıMAP4 veya POP3 protokollerini temel kimlik doğrulaması ile kullanan mobil uygulamaların Exchange Online 'a bağlanamamasını sağlar.

## <a name="create-intune-app-protection-policies"></a>Intune uygulama koruma ilkeleri oluşturma

Uygulama koruma Ilkeleri (uygulama) hangi uygulamalara izin verileceğini ve kuruluşunuzun verileriyle alabilecekleri eylemleri tanımlar. UYGULAMADA kullanılabilen seçimler, kuruluşların korumayı özel gereksinimlerine uyarlamalarını sağlar. Bazıları için, bir bütün senaryoyu uygulamak için hangi ilke ayarlarının gerekli olduğu açık olmayabilir. Microsoft, kuruluşların mobil istemci uç noktası sağlamlaştırma için öncelik vermesini sağlamak üzere iOS ve Android mobil uygulama yönetimi için uygulama veri koruma çerçevesi için Taksonomi sunmuştur.

UYGULAMA veri koruma çerçevesi, her düzey bir önceki düzeyin üzerinde oluşturulmasıyla birlikte üç ayrı yapılandırma düzeyi halinde düzenlenmiştir:

- **Kurumsal temel veri koruması** (düzey 1), uygulamaların PIN ile korunmasını ve şifreli silme işlemleri gerçekleştirmesini sağlar. Android cihazlar için bu düzey, Android cihaz kanıtlamasını doğrular. Bu, Exchange Online posta kutusu ilkelerinde benzer veri koruma denetimi sağlayan ve bunu ve Kullanıcı popülasyonu uygulamayı sunan bir giriş düzeyi yapılandırmadır.
- **Kurumsal gelişmiş veri koruması** (düzey 2), uygulama veri sızıntısı önleme mekanizmalarını ve en düşük işletim sistemi gereksinimlerini tanıtır. Bu, iş veya okul verilerine erişen mobil kullanıcıların çoğu için geçerli olan yapılandırmadır.
- **Kurumsal yüksek veri koruma** (düzey 3) gelişmiş veri koruma mekanizmaları, gelişmiş PIN YAPıLANDıRMASı ve uygulama mobil tehdit savunması sağlar. Bu yapılandırma, yüksek riskli verilere erişen kullanıcılar için istenir.

Her yapılandırma düzeyi ve korunması gereken en düşük uygulamalar için belirli önerilere bakmak için, [Uygulama koruma ilkelerini kullanarak Data Protection Framework 'ü](app-protection-framework.md)inceleyin.

Cihazın birleştirilmiş bir uç nokta yönetimi (UEM) çözümüne kaydolmasından bağımsız olarak, [Uygulama koruma ilkeleri oluşturma ve atama](app-protection-policies.md)bölümündeki adımları kullanarak hem iOS hem de Android Uygulamaları Için bir Intune uygulama koruma ilkesi oluşturulması gerekir. En azından bu ilkelerin aşağıdaki koşullara uyması gerekir:

1. Bu kişiler, Edge, Outlook, OneDrive, Office veya takımlar gibi tüm mobil uygulamaları Microsoft 365, böylece kullanıcıların herhangi bir Microsoft uygulamasındaki iş veya okul verilerine güvenli bir şekilde erişebilmesini ve bunları işleyebilmesini sağlar.

2. Bunlar tüm kullanıcılara atanır. Bu, iOS veya Android için Outlook kullanıp kullanmadıklarından bağımsız olarak tüm kullanıcıların korunmasını sağlar.

3. Gereksinimlerinizi karşılayan çerçeve düzeyini saptayın. Çoğu kuruluş, veri koruma ve erişim gereksinimleri denetimlerine izin veren şekilde **Kurumsal gelişmiş veri koruması** 'nda (düzey 2) tanımlanan ayarları uygulamalıdır.

Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Android uygulama koruma ilkesi ayarları](app-protection-policy-settings-android.md) ve [iOS uygulama koruma ilkesi ayarları](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Intune uygulama koruma ilkelerini Intune 'a kayıtlı olmayan Android cihazlarda uygulamalara uygulamak için, kullanıcının da Intune Şirket Portalı yüklemesi gerekir. Daha fazla bilgi için bkz. [Android uygulamanız uygulama koruma ilkeleriyle yönetildiğinde beklemeniz gerekenler](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Uygulama yapılandırmasını kullanma

İOS ve Android için Outlook, Microsoft Endpoint Manager, yöneticilerin uygulamanın davranışını özelleştirmesini sağlamak gibi Birleşik uç nokta yönetimine izin veren uygulama ayarlarını destekler.

Uygulama yapılandırması, kayıtlı cihazlarda mobil cihaz yönetimi (MDM) işletim sistemi kanalı aracılığıyla (iOS için[yönetilen uygulama yapılandırma](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) kanalı veya Android için [kuruluş kanalında android](https://developer.android.com/work/managed-configurations) ) veya Intune uygulama koruması ilkesi (uygulama) kanalı aracılığıyla teslim edilebilir. İOS ve Android için Outlook aşağıdaki yapılandırma senaryolarını destekler:

- Yalnızca iş veya okul hesaplarına izin ver
- Genel uygulama yapılandırma ayarları
- S/MIME ayarları
- Veri koruma ayarları

İOS ve Android için Outlook uygulama yapılandırma ayarları hakkında belirli yordamsal adımlar ve ayrıntılı belgeler için, bkz. [iOS ve Android Için Outlook dağıtımı yapılandırma ayarları](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama koruma ilkeleri nelerdir?](app-protection-policy.md) 
- [Microsoft Intune için uygulama yapılandırma ilkeleri](app-configuration-policies-overview.md)