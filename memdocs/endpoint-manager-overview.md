---
title: Microsoft Endpoint Manager 'a genel bakış-Azure | Microsoft Docs
description: Endpoint Manager, şirket içi dahil olmak üzere tüm cihazları yönetmek için Intune, Configuration Manager, ortak yönetim, masaüstü analizi, Windows Autopilot ve yönetim merkezini içerir.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9e3d03211907f31008b31d68c4ed5cd11ae1a6e
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2020
ms.locfileid: "84262155"
---
# <a name="microsoft-endpoint-manager-overview"></a>Microsoft Endpoint Manager’a genel bakış

Microsoft Uç Nokta Yöneticisi, verilerinizi bulutta ve şirket içinde güvenli tutmak için modern çalışma alanı ve modern yönetimin sağlanmasına yardımcı olur. Endpoint Manager, mobil cihazları, masaüstü bilgisayarları, sanal makineleri, katıştırılmış cihazları ve sunucuları yönetmek ve izlemek için kullandığınız hizmet ve araçları içerir.

Endpoint Manager, Microsoft Intune, Configuration Manager, masaüstü analizi, ortak yönetim ve Windows Autopilot gibi bildiğiniz ve kullanmakta olduğunuz hizmetleri birleştirir. Bu hizmetler, erişimi güvenli hale getirmek, verileri korumak ve riski yanıtlamak ve yönetmek için Microsoft 365 yığınının bir parçasıdır.

Atacan Anderson, Microsoft Kurumsal Başkan Yardımcısı Microsoft 365 için aşağıdaki iki dakikalık videoyu izleyerek başlayın:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Ne alacaksınız

Endpoint Manager aşağıdaki hizmetleri içerir:

- **Microsoft Intune**: Intune, uygulamalarınız ve cihazlarınız için %100 bulut tabanlı bir mobil cihaz YÖNETIMI (MDM) ve mobil uygulama YÖNETIMI (MAM) sağlayıcısıdır. Android, Android Enterprise, iOS/ıpados, macOS ve Windows 10 cihazlarında özellikleri ve ayarları denetlemenize olanak tanır. Azure Active Directory (AD), mobil tehdit savunları, ADMX şablonları, Win32 ve özel LOB uygulamaları ve daha fazlasını içeren diğer hizmetlerle tümleştirilir.

  Exchange veya Active Directory gibi şirket içi altyapınız varsa, Intune bağlayıcıları da kullanılabilir:

  - **Active Directory Intune Bağlayıcısı** , Windows Autopilot kullanarak kaydeden bilgisayarlar için şirket içi Active Directory etki alanına girişler ekler. Daha fazla bilgi için bkz. [karma Azure AD 'ye katılmış cihazları dağıtma](/mem/intune/enrollment/windows-autopilot-hybrid).
  - **Intune Exchange Bağlayıcısı** , cihazların Intune 'a kaydolması ve ilkeleriniz ile uyumlu olması halinde Exchange sunucularınıza cihaz erişimine izin verir (veya engeller). Daha fazla bilgi için bkz. Şirket [Içi Intune Exchange bağlayıcısını ayarlama](/mem/intune/protect/exchange-connector-install).
  - **Intune sertifika Bağlayıcısı** , kimlik doğrulaması ve S/MIME e-posta şifrelemesi için sertifikaları kullanan cihazlardan gelen sertifika isteklerini işler. Daha fazla bilgi için bkz. [kimlik doğrulaması için sertifikaları kullanma](/mem/intune/protect/certificates-configure).

  Endpoint Manager 'ın bir parçası olarak, Intune 'u kullanarak uyumluluğu oluşturup denetleyin ve bulut kullanarak cihazlarınıza uygulamalar, Özellikler ve ayarlar dağıtın.

  Daha fazla bilgi için bkz. [Microsoft Intune nedir?](https://docs.microsoft.com/intune/fundamentals/what-is-intune).

- **Configuration Manager**: Configuration Manager, ağınızdaki veya internet tabanlı masaüstü bilgisayarları, sunucuları ve dizüstü bilgisayarları yönetmek için bir şirket içi yönetim çözümüdür. Bu uygulamayı Intune, Azure Active Directory (AD), Microsoft Defender ATP ve diğer bulut hizmetleriyle tümleştirilebilen bulut için etkinleştirebilirsiniz. Uygulamaları, yazılım güncelleştirmelerini ve işletim sistemlerini dağıtmak için Configuration Manager kullanın. Ayrıca uyumluluğu izleyebilir, istemcileri gerçek zamanlı olarak sorgulayabilir ve davranabilir ve çok daha fazlasını yapabilirsiniz.

  Endpoint Manager 'ın bir parçası olarak, her zaman sahip olduğunuz Configuration Manager kullanmaya devam edin. Bazı görevleri buluta taşımaya hazırsanız, [ortak yönetimi](https://docs.microsoft.com/configmgr/comanage/)göz önünde bulundurun.

  Daha fazla bilgi için bkz. [Configuration Manager nedir?](https://docs.microsoft.com/configmgr/core/understand/introduction).

- **Ortak yönetim**: ortak yönetim, Intune ve diğer Microsoft 365 bulut hizmetlerini kullanarak mevcut şirket içi Configuration Manager yatırımınızı buluta birleştirir. Configuration Manager veya Intune 'un yedi farklı iş yükü grubu için yönetim yetkilisi olup olmadığını seçersiniz.

  Endpoint Manager 'ın bir parçası olarak ortak yönetim, koşullu erişim de dahil olmak üzere bulut özelliklerini kullanır. Intune ile bulutta diğer görevleri çalıştırırken bazı görevleri şirket içinde saklayın.

  Daha fazla bilgi için bkz. [ortak yönetim nedir?](https://docs.microsoft.com/configmgr/comanage/overview).

- **Masaüstü Analizi**: Masaüstü analizi, Configuration Manager ile tümleşen bulut tabanlı bir hizmettir. Windows istemcilerinizin güncelleştirme hazırlığı hakkında daha bilinçli kararlar almanıza yardımcı olmak için içgörüler ve zeka sağlar. Hizmet, Microsoft bulutuna bağlı milyonlarca cihazdan toplanan verileri kuruluşunuzdaki verileri birleştirir. Kuruluşunuzdaki güvenlik güncelleştirmeleri, uygulamalar ve cihazlar hakkında bilgi sağlar ve uygulamalar ve sürücülerle ilgili uyumluluk sorunlarını belirler. Kuruluşunuzdaki varlıklar için en iyi öngörüleri sağlama olasılığı olan cihazlar için bir pilot oluşturun.

  Endpoint Manager 'ın bir parçası olarak, Windows 10 cihazlarının güncel kalmasını sağlamak için masaüstü analizinin bulut destekli öngörülerini kullanın.

  Daha fazla bilgi için bkz. [Masaüstü analizi nedir?](https://docs.microsoft.com/configmgr/desktop-analytics/overview).

- **Windows Autopilot**: Windows Autopilot yeni cihazları ayarlar ve önceden yapılandırır, kullanıma hazırlanıyor. Windows cihazlarının yaşam döngüsünü, hem BT hem de son kullanıcılar için yaşam süresi boyunca ilk dağıtımdan basitleştirmek üzere tasarlanmıştır.

  Endpoint Manager 'ın bir parçası olarak, cihazları önceden yapılandırmak ve cihazları Intune 'a otomatik olarak kaydetmek için Autopilot kullanın. Ayrıca, daha karmaşık cihaz yapılandırması (önizlemede) için Autopilot ile Configuration Manager ve ortak yönetim ile tümleştirilebilir.

  Daha fazla bilgi için bkz. [Windows Autopilot genel bakış](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) ve [Windows cihazlarını Intune 'a kaydetme](/mem/intune/enrollment/enrollment-autopilot).

- **Azure Active Directory (ad)**: Azure AD, Endpoint Manager tarafından cihazların, kullanıcıların, grupların ve çok faktörlü kimlik DOĞRULAMASıNıN (MFA) kimliğini kullanır. Ek bir maliyet olabilecek **Azure AD Premium**, dinamik gruplar, otomatik kayıt ve koşullu erişim dahil cihaz, uygulama ve verilerin korunmasına yardımcı olmak için [ek özelliklere](https://azure.microsoft.com/pricing/details/active-directory/) sahiptir.

  Daha fazla bilgi için bkz. [Kullanıcı ekleme](/mem/intune/fundamentals/users-add), [otomatik kayıt ayarlama](/mem/intune/enrollment/windows-enroll)ve [koşullu erişim hakkında](/mem/intune/protect/conditional-access).

- **Endpoint Manager Yönetim Merkezi**: [Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) , ilkeleri oluşturmak ve cihazlarınızı yönetmek için tek seferlik bir Web sitesidir. Bunlar, gruplar, güvenlik, koşullu erişim ve raporlama dahil olmak üzere diğer temel cihaz yönetim hizmetleri ile birlikte yer takar. Bu Yönetim Merkezi Ayrıca Configuration Manager ve Intune tarafından yönetilen cihazları gösterir (önizlemede).

## <a name="choose-whats-right-for-you"></a>Sizin için doğru olanları seçin

Kuruluşunuz için nelerin doğru olduğunu belirlemenin birkaç yolu vardır. Sonraki adımlarınız, kuruluşunuzun yaptığı işe göre değişir. Ne elde etmek istediğinizi göz önünde bulundurun.

Örneğin:

- Yeni cihazları sürekli temin ediyorsanız Windows Autopilot ile başlayın.
- Kullanıcılarınız, uygulamalarınız ve cihazlarınız için kurallar ve denetim ayarları ekleyip Intune ile başlayın.
- Şu anda uygulamaları dağıtmak için Configuration Manager kullanıyorsanız ve güvenlik gereksinimlerine göre koşullu erişimi kullanmak istiyorsanız ortak yönetim ile başlayın.
- Şu anda Configuration Manager kullanıyorsanız ve Windows 10 cihazlarının güncel tutulmasını sağlamaktan sorumluysanız, masaüstü analizi ile başlayın.
- MDM ve MAM ile çalışmaya başladıysanız veya Office, Microsoft Edge ve Windows ayarlarını denetlemek için ADMX şablonları kullanıyorsanız, Intune ile başlayın.

Endpoint Manager 'ı üç bölümden de düşünebilirsiniz: bulut, şirket içi ve bulut + şirket içi:

- **Bulut**: tüm veriler Azure 'da depolanır. Ve, daha fazla veri merkezi yoktur. Bu yaklaşım, bulutun taşınabilirlik avantajlarının yanı sıra Azure 'un güvenlik avantajlarından yararlanmanızı sağlar.

- **Şirket içi**: Configuration Manager içeren veya bulutu kullanmaya hazırlamış olan bir şirket içi altyapınız varsa, mevcut sistemlerinizi koruyabilirsiniz.

- **Bulut + şirket içi**: birçok ortam karmatı ve bulut iliştirme yaklaşımını kullanır. Bu, bulut ve şirket içi bir birleşimi kullandıkları anlamına gelir. Yeni cihazlarda, verilere erişmek ve verileri korumak için Intune 'un avantajlarını kullanın. Configuration Manager kullanıyorsanız, ek işlevsellik ve çözümlemeler için buluta bağlanın. Bazı iş yüklerini buluta taşımak istiyorsanız, ortak yönetim iyi bir seçenektir.

## <a name="what-you-need-to-get-started"></a>Başlamak için yapmanız gerekenler

Microsoft Uç Nokta Yöneticisi, birkaç teknolojiyi birleştiren bir çözüm platformudur. Yeni bir lisans değildir. Hizmetler, bireysel lisans koşullarına göre lisanslanır. Daha fazla bilgi için [ürün lisanslama koşullarına](https://www.microsoft.com/licensing/product-licensing/products)bakın.

Şu anda Configuration Manager kullanıyorsanız, Windows cihazlarınızı birlikte yönetmek için de Microsoft Intune alırsınız. İOS/ıpados ve Android gibi diğer platformlarda ayrı bir Intune lisansına sahip olmanız gerekir.

Çoğu senaryoda, Endpoint Manager ve Office 365 ' i verdiği için en iyi seçenek Microsoft 365 olabilir. Daha fazla bilgi için bkz. [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## <a name="next-steps"></a>Sonraki adımlar

[Bulut zekasını kullanarak BT 'yi basitleştirip hızlandırın ve modern bir çalışma alanına geçme](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Öğretici: Microsoft Endpoint Manager’da Intune için izlenecek yol](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Microsoft 365 nedir? Modül öğren](https://docs.microsoft.com/learn/modules/what-is-m365/index)
