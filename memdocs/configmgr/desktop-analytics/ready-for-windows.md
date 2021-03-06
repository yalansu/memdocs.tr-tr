---
title: Windows için hazırlanıyor
titleSuffix: Configuration Manager
description: Windows için hazırlanma Web sitesinin kullanımdan kaldırılması hakkında
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 2d431f744ab09aeb938a7961ebf713f71c0f8015
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193691"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Modern masaüstü kullanımdan kaldırma hakkında SSS

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Windows benimseme durumu için hazırlanma

Benimseme durumu, Microsoft ile veri paylaşan ticari cihazlardan gelen bilgileri temel alır. Durum, yazılım satıcılarından destek deyimleriyle tümleşiktir.

Masaüstü analizi, ticari cihazlarda bulunan bir varlığın her sürümü için benimseme durumu sağlar. Bu durum, tüketici cihazlarından veya veri paylaşmeyen cihazlardan veri içermez. Durum, tüm Windows 10 cihazlarında benimseme oranını temsil edemeyebilir.

Olası kategoriler şunlardır:

- **Son derece benimseme**: en az 100.000 ticari Windows 10 cihaz bu uygulamayı yükledi.

- **Benimseme**: en az 10.000 ticari Windows 10 cihaz bu uygulamayı yükledi.

- **Yetersiz veri**: çok az sayıda ticari Windows 10 cihaz, Microsoft 'un benimsemesi için bu uygulamayla ilgili bilgileri paylaşıyor.

- **Geliştiriciye başvurun**: uygulamanın bu sürümünde uyumluluk sorunları olabilir. Microsoft daha fazla bilgi edinmek için yazılım sağlayıcısına başvurmayı önerir.

- **Bilinmiyor**: Bu uygulamanın bu sürümü için kullanılabilir bilgi yok. Bilgiler, uygulamanın diğer sürümleri için kullanılabilir olabilir.

## <a name="general"></a>Genel

### <a name="what-happened-to-the-ready-for-windows-website"></a>Windows için hazırlanma Web sitesine ne oldu?

Birçok müşteri, Windows 10 ve Enterprise için Microsoft 365 uygulamaları ile alma ve güncel kalma konularında zorluk sahibi olabilir. Bu işlem genellikle el ile olduğundan, birincil zorluk uygulamaları test ediyor. BT yöneticileri ve uygulama sahiplerinin, mevcut uygulamaları sürekli olarak analiz etmesine ve sonra ortaya çıkan sorunları gidermesine zaman alıcı bir işlemdir.

Windows 10 ve Enterprise için Microsoft 365 uygulamaları çalıştıran ticari cihazlarda desteklenen ve kullanımda olan *modern Masaüstü dizinine yönelik* listelenen yazılım çözümleri. Dizin, BT yöneticilerine Windows 10 ' un en son sürümlerini ve dağıtımlarına yönelik Microsoft 365 göz önünde bulundurmalarına yardımcı olur.

BT yöneticileriyle ilgili geri bildirimler, bu öngörüleri, dağıtım planlarını planlamak için kullandıkları araçlarla tümleştirirler. Windows 10 ve Microsoft 365 uygulamalarınızı kurumsal yükseltme projelerine yönelik olarak planlamak ve yönetmek için Configuration Manager ' de [Masaüstü Analizi](https://aka.ms/dadocs) ve [Microsoft 365 uygulamaları hazır olma özellikleri](/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) ' ni kullanın. 

> [!Note]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

### <a name="what-is-desktop-analytics"></a>Desktop Analytics nedir?

[Masaüstü Analizi](https://aka.ms/dadocs) , Configuration Manager ile tümleşen bulut tabanlı bir hizmettir. Hizmet, Windows uç noktalarınızın güncelleştirme hazırlığı hakkında daha bilinçli kararlar almanıza yardımcı olmak için Öngörüler ve zeka sağlar. Microsoft 'un bulut hizmetlerine bağlı milyonlarca Windows cihazınızdan toplanan öngörülerle kuruluşunuza özgü verileri birleştirir.

-    Kuruluşunuzda yönetim altındaki uç noktalar, uygulamalar ve sürücüler hakkında kapsamlı bir görünüm alın.

-    En son Windows özellik güncelleştirmeleriyle uygulama ve sürücü uyumluluğunu değerlendirin. İş kolu uygulamalarına yönelik gelişmiş Öngörüler ve bilinen sorunların risk azaltma önerilerini alın.

-    Genel ortamınızı yeterince temsil eden pilot cihaz kümesini iyileştirmek için Microsoft bulutundaki yapay zeka (AI) kullanın.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Windows Dağıtım planlarım için neden masaüstü Analizi kullanmalıyım?

Masaüstü Analizi aşağıdaki avantajları sağlar:

-    **Cihaz ve yazılım envanteri**: uygulamalar ve Windows sürümleri gibi önemli faktörlerin envanterini çıkarın.

-    **Pilot kimlik**: faktörlerin en geniş kapsamını sağlayan en küçük cihaz kümesinin kimliği. Windows yükseltmelerinde ve güncelleştirmelerinde yapılan bir pilot için en önemli etkenlere odaklanır. Pilot uygulamanın daha başarılı olduğundan emin olmak, üretimde çok daha hızlı ve güvenli bir şekilde devam etmenize olanak tanır.

-    **Sorun kimliği**: toplu pazar verilerini ortamınızdaki verilerle birlikte kullanarak, hizmet, mevcut sorunları Windows ile alma ve kullanmaya yönelik olası sorunları tahmin eder. Daha sonra potansiyel azaltmaları önerir.

-    **Configuration Manager tümleştirme**: BT bulutu-mevcut şirket içi altyapınızı mümkün kılar. Windows 'u cihazlarınızda dağıtmak ve yönetmek için bu verileri ve çözümlemeyi kullanın.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Masaüstü analizinden *Windows Için hazırlanma* durumu ne anlama geliyor?

**Benimseme durumu** , Microsoft ile veri paylaşan ticari cihazlardan gelen bilgileri temel alır. Durum, yazılım satıcılarından destek deyimleriyle tümleşiktir.

Masaüstü analizi, ticari cihazlarda bulunan bir varlığın her sürümü için benimseme durumu sağlar. Bu durum, tüketici cihazlarından veya veri paylaşmeyen cihazlardan veri içermez. Durum, tüm Windows 10 cihazlarında benimseme oranını temsil edemeyebilir.

Daha fazla bilgi için bkz. [Uyumluluk değerlendirmesi](compat-assessment.md).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Masaüstü Analizi 'nde *Windows Için hazırlanma* durumu hangi varlıkları alır? 

Varlıklar, şu durumlarda masaüstü analizinden *Windows Için hazırlanma* durumuna sahiptir:

-    Yazılım sağlayıcısı çözüm için destek bildirir.
-    Müşteriler, Microsoft ile bilgi paylaşan önemli sayıda ticari Windows 10 cihazına dağıtmıştır.
-    Varlık, ticari kullanıcılarla ilgilidir.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Masaüstü analizine hangi ek Öngörüler alabilirim?

Masaüstü analizi, [cihazların ve yüklü uygulamalarının envanterini ve](about-assets.md)iş kolu uygulamalarına yönelik [Gelişmiş öngörüleri](compat-assessment.md#advanced-insights) sağlar. 

## <a name="software-providers"></a>Yazılım sağlayıcıları

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>Yazılım çözümmi masaüstü Analizte listeme yine de listeleyebilir miyim?

Ürününüzün 32-bit veya 64 bit Windows 10 veya Enterprise için Microsoft 365 uygulamalarla birlikte çalıştığına yönelik bir destek bildirisi yayımlayın. Çözümlerinizi masaüstü Analizi 'nde göstermek için Microsoft kişinizle görüşün.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Çözümlerimi kullanım açısından nasıl Listelerim?

Binlerce BT yöneticileri Configuration Manager ve Masaüstü analiziyle milyonlarca cihazı yönetir. Bu araçları, kuruluşlarını Windows 10 ' un en son sürümüne ve kurumsal Microsoft 365 uygulamalarına yönelik olarak planlamak ve yükseltmek için kullanır. Bunlar, yazılım çözümleri için satın alma kararları almak için de kullanılır.

Microsoft, yazılım satıcılarından, ticari cihazlardan aldıkları benimseme bilgilerine sahip destek deyimlerini tümleştirir. Dünyanın dört bir yanındaki kuruluşlar bu verileri masaüstü Analizi ve Office hazırlık araçları 'nda kullanır. 

Destek deyimleriniz, varlıklarla doğru şekilde ilişkilendirilmemişse, Microsoft kişinizle konuşun.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Varlıklarım üzerinde ayrıntılı performans ölçümleri görebilir miyim?

Geliştirici Merkezi aracılığıyla sistem durumu ve ölçüm raporlarıyla çözümlerinizi performansını değerlendirin: 

- [Windows Store](/windows/uwp/publish/health-report)
- [Masaüstü](/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office Eklentileri](/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-microsoft-365-apps-for-enterprise"></a>Windows 10 için uyumlu varlıkları ve kurumsal için Microsoft 365 uygulamaları nasıl geliştirebilirim?

Masaüstü uygulamalarınızın şimdi uyumlu olduğundan emin olun ve gelecekte Windows 10 ile uyumlu kalın. Daha fazla bilgi için bkz. [geliştiriciler Için uygulama uyumluluğu](https://developer.microsoft.com/windows/desktop/app-compatibility).

Enterprise için Microsoft 365 uygulamalar için çözümler geliştirirseniz, bkz. [Office 'TEKI com, VSTO ve VBA eklentileri Için geliştirme en iyi yöntemleri](/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).