---
title: Microsoft Intune-Azure 'da Microsoft Defender ATP 'yi kullanma | Microsoft Docs
description: Kurulum ve yapılandırma dahil olmak üzere Intune ile Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) kullanın, Intune cihazlarınızı ATP ile ekleme ve ardından Intune cihaz uyumluluğuyla bir cihaz ATP risk değerlendirmesi ve ağ kaynaklarını korumak için koşullu erişim ilkeleri kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f54bf7f281fca65e01d839e926200bc68c49765
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663456"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Intune 'da koşullu erişimle Microsoft Defender ATP için uyumluluğu zorlama

Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP), Microsoft Intune Mobile Threat Defense çözümü olarak tümleştirebilirsiniz. Tümleştirme, güvenlik ihlallerinin önlenmesine ve bir kuruluşun içindeki ihlallerinin etkilerini sınırlamanıza yardımcı olabilir.

Microsoft Defender ATP, Windows 10 veya üzeri çalıştıran cihazlarla ve Android cihazlarla çalışır.

Başarılı olmak için Concert ' de aşağıdaki konfigürasyonları kullanacaksınız:

- **Intune Ile Microsoft Defender ATP arasında hizmetten hizmete bağlantı kurun**. Bu bağlantı, Microsoft Defender ATP 'yi Intune ile yönettiğiniz desteklenen cihazlardan makine riski hakkında veri toplamasına olanak sağlar.
- **Microsoft Defender ATP ile cihazları eklemek için bir cihaz yapılandırma profili kullanın**. Cihazları, Microsoft Defender ATP ile iletişim kuracak şekilde yapılandırmak ve risk düzeylerini değerlendirmeye yardımcı olan verileri sağlamak için kullanabilirsiniz.
- **İzin vermek istediğiniz risk düzeyini ayarlamak için bir cihaz uyumluluk Ilkesi kullanın**. Risk düzeyleri Microsoft Defender ATP tarafından raporlanır. İzin verilen risk düzeyini aşan cihazlar uyumsuz olarak tanımlanır.
- Kullanıcıların uyumlu olmayan cihazlardan şirket kaynaklarına erişmesini engellemek için **koşullu erişim Ilkesi kullanın** .

Intune 'u Microsoft Defender ATP ile tümleştirdiğinizde, Microsoft Defender ATPs tehdit & güvenlik açığı yönetimi (TVM) avantajlarından yararlanabilir ve [TVM tarafından tanımlanan uç nokta zayıflılığını düzeltmek Için Intune 'u kullanabilirsiniz](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Intune ile Microsoft Defender ATP kullanma örneği

Aşağıdaki örnek, kuruluşunuzun korunmasına yardımcı olmak için bu çözümlerin birlikte nasıl çalıştığını açıklamanıza yardımcı olur. Bu örnek için, Microsoft Defender ATP ve Intune zaten tümleşiktir.

Birisinin kuruluşunuzdaki bir kullanıcıya katıştırılmış kötü amaçlı kod içeren bir sözcük eki gönderdiği bir olay düşünün.

- Kullanıcı eki açar ve içeriği etkinleştirir.
- Yükseltilmiş bir ayrıcalık saldırısı başlar ve uzak bir makineden bir saldırganın, kurban cihazında yönetici hakları vardır.
- Daha sonra saldırgan, kullanıcının diğer cihazlarına uzaktan erişir. Bu güvenlik ihlali tüm kuruluşu etkileyebilir.

Microsoft Defender ATP, bu senaryo gibi güvenlik olaylarının çözümlenmesine yardımcı olabilir.

- Örneğimizde, Microsoft Defender ATP cihazın anormal kod yürütüldüğünü, bir işlem ayrıcalık yükseltme yükseltmesi, eklenen kötü amaçlı kod ve şüpheli bir uzak kabuk vermiş olduğunu algılar.
- Microsoft Defender ATP cihazdan bu eylemlere bağlı [olarak, cihazı yüksek riskli olarak sınıflandırır](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) ve Microsoft Defender Güvenlik Merkezi portalındaki şüpheli etkinlik hakkında ayrıntılı bir rapor içerir.

Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP), Microsoft Intune Mobile Threat Defense çözümü olarak tümleştirebilirsiniz. Tümleştirme, güvenlik ihlallerinin önlenmesine ve bir kuruluşun içindeki ihlallerinin etkilerini sınırlamanıza yardımcı olabilir.

Cihazları *Orta* veya *yüksek* düzeyde risk uyumlu olmayan şekilde sınıflandırmak için bir Intune cihaz uyumluluk ilkeniz olduğundan, güvenliği aşılmış cihaz uyumsuz olarak sınıflandırılmıştır. Bu sınıflandırma, koşullu erişim ilkenizin, bu cihazdan kurumsal kaynaklarınıza erişimi başlatmanıza ve erişimini engellemeye olanak tanır.

Android çalıştıran cihazlar için, Android 'de Microsoft Defender ATP yapılandırmasını değiştirmek üzere Intune ilkesini kullanabilirsiniz. Daha fazla bilgi için bkz. [Microsoft Defender ATP Web koruması](../protect/advanced-threat-protection-manage-android.md).

## <a name="prerequisites"></a>Ön koşullar

Microsoft Defender ATP 'yi Intune ile birlikte kullanmak için, aşağıdakilerin yapılandırıldığından ve kullanıma hazırlandığınızdan emin olun:

- Enterprise Mobility + Security E3 ve Windows E5 (veya Microsoft 365 Kurumsal E5) için lisanslı kiracı
- Microsoft Intune ortamı, [Intune ile yönetilen](../enrollment/windows-enroll.md) Windows 10 veya aynı zamanda Azure AD 'ye katılmış Android cihazları
- Microsoft Defender Güvenlik Merkezi 'ne (ATP portalı) erişmenizi sağlayacak [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) ortamı

> [!NOTE]
> Microsoft Defender ATP, iOS/ıpados ve Android Intune uygulama koruma ilkeleriyle desteklenmez.

## <a name="next-steps"></a>Sonraki adımlar

- Microsoft Defender ATP 'yi Intune 'a bağlamak, cihazları eklemek ve koşullu erişim ilkelerini yapılandırmak için bkz. [Intune 'Da Microsoft Defender ATP 'Yi yapılandırma](../protect/advanced-threat-protection-configure.md).

Intune belgelerinden daha fazla bilgi edinin:

- [Cihazların sorunlarını gidermek için ATPs güvenlik açığı yönetimi ile güvenlik görevlerini kullanma](atp-manage-vulnerabilities.md)
- [Cihaz uyumluluk ilkelerini kullanmaya başlama](device-compliance-get-started.md)

Microsoft Defender ATP belgelerinden daha fazla bilgi edinin:

- [Microsoft Defender ATP koşullu erişimi](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP risk panosu](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
