---
title: Microsoft Intune Endpoint Security 'yi yönetme | Microsoft Docs
description: Güvenlik yöneticilerinin cihaz güvenliğini yönetmek ve Microsoft Endpoint Manager 'daki cihazların sorunlarını gidermek için uç nokta güvenlik düğümünü nasıl kullanabileceğinizi öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 99ac1e069386c69011543ac40878dd62a0d50527
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990833"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Microsoft Intune uç nokta güvenliğini yönetme

Güvenlik Yöneticisi olarak, cihaz güvenliğini yapılandırmak ve bu cihazlar risk altında olduğunda cihazların güvenlik görevlerini yönetmek için Intune 'daki *Endpoint Security* düğümünü kullanın. Uç nokta güvenlik ilkeleri, cihazlarınızın güvenliğine odaklanmanız ve riski azaltmaya yardımcı olmak için tasarlanmıştır. Kullanılabilir görevler, risk altında olan cihazları belirlemenize, bu cihazları düzeltmeye ve bunları uyumlu veya daha güvenli bir duruma geri yüklemenize yardımcı olur.

Uç nokta güvenlik düğümü, Intune aracılığıyla cihazları güvenli tutmak için kullanabileceğiniz araçları gruplandırır:

- **Tüm yönetilen cihazlarınızın durumunu gözden geçirin**. Cihaz uyumluluğunu yüksek bir düzeyden görüntüleyebileceğiniz [tüm cihazlar](#manage-devices) görünümünü kullanın ve ardından bunları çözebilmeniz için hangi uyumluluk ilkelerinin karşılanmadığını anlamak üzere belirli cihazlara gidebilirsiniz.

- **Cihazlar için en iyi yöntem güvenlik yapılandırmalarının temelini oluşturan güvenlik temellerini dağıtın**. Intune, Windows cihazlarına yönelik [güvenlik temellerini](#manage-security-baselines) ve Microsoft Defender Gelişmiş tehdit koruması (Defender ATP) ve Microsoft Edge gibi büyüyen bir uygulamalar listesi içerir. Güvenlik temelleri, bilinen bir ayar grubunu ve ilgili güvenlik ekiplerinin önermediği varsayılan değerleri uygulamanıza yardımcı olan önceden yapılandırılmış Windows ayarları gruplarıdır.

- **Cihazlarda sıkı odaklı ilkeler aracılığıyla güvenlik yapılandırmalarının yönetimini yönetin**.  Her [uç nokta güvenlik ilkesi](#use-policies-to-manage-device-security) , virüsten koruma, disk şifreleme, güvenlik duvarları ve Defender ATP ile tümleştirme aracılığıyla kullanılabilir hale getirilen çeşitli alanlarla ilgili cihaz güvenliğinin yönlerine odaklanır.

- **Uyumluluk ilkesi aracılığıyla cihaz ve Kullanıcı gereksinimleri oluşturun**. [Uyumluluk ilkeleriyle](../protect/device-compliance-get-started.md), cihazların ve kullanıcıların uyumlu kabul edilmesi için uyması gereken kuralları ayarlarsınız. Kurallar, işletim sistemi sürümlerini, parola gereksinimlerini, cihaz tehdit düzeylerini ve daha fazlasını içerebilir.

  Uyumluluk ilkelerini zorlamak için Azure Active Directory (Azure AD) [koşullu erişim ilkeleriyle](#configure-conditional-access) tümleştirdiğinizde, hem yönetilen cihazların hem de yönetilmeyen cihazların şirket kaynaklarına erişmesini sağlayabilirsiniz.

- **Intune 'U Microsoft Defender ATP ekibiniz Ile tümleştirin**. [Defender ATP ile tümleştirerek](#set-up-integration-with-defender-atp) [güvenlik görevlerine](#review-security-tasks-from-defender-atp)erişim elde edersiniz. Güvenlik görevleri, güvenlik takımınızın risk altında olan cihazları tanımlamasına ve daha sonra işlem yapacak olan Intune yöneticilerine yönelik ayrıntılı düzeltme adımlarını belirlemesine yardımcı olmak için, Defender ATP ve Intune 'U birbirine yakından bağlayın.

Bu makalenin aşağıdaki bölümlerinde, Yönetim Merkezi 'nin uç nokta güvenlik düğümünden gerçekleştirebileceğiniz farklı görevler ve bunları kullanmak için gereken rol tabanlı erişim denetimi (RBAC) izinleri ele alınmaktadır.

## <a name="manage-devices"></a>Cihazları yönetme

Uç nokta güvenlik düğümü, Azure AD 'nizden Microsoft Endpoint Manager 'da bulunan tüm cihazların listesini görüntüleyebileceğiniz *tüm cihazlar* görünümünü içerir.

Bu görünümden, bir cihazın hangi ilkeleri ile uyumlu olmadığı hakkında daha fazla bilgi için detaya gitmek üzere cihazları seçebilirsiniz. Ayrıca, bir cihazın sorunlarını gidermek, bir cihazı yeniden başlatmak, kötü amaçlı yazılım taraması başlatmak veya bir Windows 10 cihazında BitLocker anahtarlarını döndürmek için bu görünümden erişimi de kullanabilirsiniz.

Daha fazla bilgi için bkz. [Microsoft Intune uç nokta güvenliği olan cihazları yönetme](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Güvenlik temellerini yönetme

Intune 'daki güvenlik temelleri, ürün için ilgili Microsoft Güvenlik ekiplerinden en iyi yöntem önerileri olan önceden yapılandırılmış ayarlar gruplarıdır. Intune, Windows 10 cihaz ayarları, Microsoft Edge, Microsoft Defender Gelişmiş tehdit koruması ve daha fazlası için güvenlik temellerini destekler.

Kullanıcılarınızın ve cihazlarınızın korunması için cihaz ve uygulama ayarlarının *en iyi yöntem* yapılandırmasını hızla dağıtmak üzere güvenlik temellerini kullanabilirsiniz. Güvenlik temelleri Windows 10 sürüm 1809 ve üstünü çalıştıran cihazlar için desteklenir.

Daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarını yapılandırmak için güvenlik temellerini kullanma](../protect/security-baselines.md).

Güvenlik temelleri, cihazlarda ayarları yapılandırmak için Intune 'daki çeşitli yöntemlerden biridir. Ayarları yönetirken, ortamınızda hangi diğer yöntemlerin kullanımda olduğunu anlamak önemlidir. böylece, çakışmaları önlemek için cihazlarınızı yapılandırabilirler. Bu makalenin ilerleyen kısımlarında [İlke çakışmalarını önleyin](#avoid-policy-conflicts) bölümüne bakın.

## <a name="review-security-tasks-from-defender-atp"></a>Defender ATP 'den güvenlik görevlerini gözden geçirme

Intune 'u Microsoft Defender Gelişmiş tehdit koruması (Defender ATP) ile tümleştirdiğinizde, Intune 'da risk altında olan cihazları belirleyen ve bu riski azaltmak için gereken adımları sağlayan *güvenlik görevlerini* gözden geçirebilirsiniz. Daha sonra bu riskler başarıyla azaltıldığında Defender ATP 'ye geri raporlamak için görevleri kullanabilirsiniz.

- Defender ATP ekibi, hangi cihazların risk altında olduğunu ve bu bilgileri Intune ekibinize bir güvenlik görevi olarak geçitirsiniz. Birkaç tıklamayla, Intune için risk altındaki cihazları tanımlayan bir güvenlik görevi ve güvenlik açığı oluşturur ve bu riski hafifletmek için yönergeler sağlar.

- Intune yöneticileri güvenlik görevlerini gözden geçirdikten sonra bu görevleri düzeltmek için Intune içinde hareket ederler. Bu durum azaltıldıktan sonra, bu durumu Defender ATP ekibine geri ileten görevi tamamlanmış olarak ayarlar.

Güvenlik görevleri aracılığıyla her iki takım da risk altında olan cihazlar ve bu risklerin nasıl ve ne zaman düzeltildiğinde eşitlenmiş olarak kalır.

Güvenlik görevlerini kullanma hakkında daha fazla bilgi için bkz. [Microsoft Defender ATP tarafından tanımlanan güvenlik açıklarını düzeltmek Için Intune kullanma](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Cihaz güvenliğini yönetmek için ilkeleri kullanma

Güvenlik Yöneticisi olarak, uç nokta güvenlik düğümünde *Yönet* altında bulunan güvenlik ilkelerini kullanın. Bu ilkelerle, cihaz yapılandırma profilleri ve güvenlik temellerinden daha büyük gövdeye ve ayarların aralığına gidilmeden cihaz güvenliğini yapılandırabilirsiniz.

![İlkeleri yönetme](./media/endpoint-security/endpoint-security-policies.png)

Bu güvenlik ilkelerini kullanma hakkında daha fazla bilgi için bkz. [Endpoint Security ilkeleriyle cihaz güvenliğini yönetme](../protect/endpoint-security-policy.md).

Uç nokta güvenlik ilkeleri, cihazlarda ayarları yapılandırmak için Intune 'daki çeşitli yöntemlerden biridir. Ayarları yönetirken, ortamınızda, cihazlarınızı yapılandırabileceği ve çakışmalardan kaçınacak diğer yöntemlerin ne olduğunu anlamak önemlidir. Bu makalenin ilerleyen kısımlarında [İlke çakışmalarını önleyin](#avoid-policy-conflicts) bölümüne bakın.

*Yönet* altında bulunan *cihaz uyumluluğu* ve *koşullu erişim* ilkeleri de bulunur. Bu ilke türleri, uç noktaları yapılandırmaya yönelik odaklanmış bir güvenlik ilkesi değildir, ancak cihazları yönetmeye ve şirket kaynaklarınıza erişime yönelik önemli araçlardır.

## <a name="use-device-compliance-policy"></a>Cihaz Uyumluluk ilkesini kullanma

Cihazların ve kullanıcıların ağınıza ve şirket kaynaklarına erişmesine izin verilen koşulları oluşturmak için cihaz Uyumluluk ilkesini kullanın.

[Kullanılabilir uyumluluk ayarları](../protect/device-compliance-get-started.md#next-steps) , kullandığınız platforma bağlıdır, ancak ortak ilke kuralları şunları içerir:

- Cihazların en düşük veya belirli bir işletim sistemi sürümünü çalıştırmasını isteme
- Parola gereksinimlerini ayarlama
- Defender ATP veya başka bir mobil tehdit savunma iş ortağı tarafından belirlendiği şekilde izin verilen en fazla cihaz tehdit düzeyini belirtme

İlke kurallarına ek olarak, uyumluluk ilkeleri şunları destekler:

- Intune 'da tanımladığınız [konumlar](../protect/use-network-locations.md) . Bir uyumluluk ilkesiyle konum kullandığınızda, ilke cihazların uyumlu olması için bir iş ağına bağlı olduğundan emin olabilir.
- [Uyumsuzluk Için eylemler](../protect/actions-for-noncompliance.md). Bu eylemler, uyumlu olmayan cihazlara uygulanacak zaman sıralı bir dizi eylemlerdir. Eylemler cihaz kullanıcılarına uyumsuzluk, uzaktan cihazları kilitleme, hatta uyumlu olmayan cihazları devre dışı bırakma ve şirket verilerini kaldırma hakkında uyarı göndermek için e-posta veya bildirimler göndermeyi içerir.

Uyumluluk ilkelerini zorlamak için Intune 'U Azure AD [koşullu erişim ilkeleriyle](#configure-conditional-access) tümleştirdiğinizde, koşullu erişim, yönetilen cihazlar ve yönetmeyecek cihazlardan şirket kaynaklarına erişmek için uyumluluk verilerini kullanabilir.

Daha fazla bilgi edinmek için bkz. [Intune kullanarak kuruluşunuzdaki kaynaklara erişime izin vermek için cihazlardaki kuralları ayarlama](../protect/device-compliance-get-started.md).

Cihaz uyumluluk ilkeleri, cihazlarda ayarları yapılandırmak için Intune 'daki çeşitli yöntemlerden biridir. Ayarları yönetirken, ortamınızda, cihazlarınızı yapılandırabileceği ve çakışmaları önlemek için diğer yöntemlerin ne olduğunu anlamak önemlidir. Bu makalenin ilerleyen kısımlarında [İlke çakışmalarını önleyin](#avoid-policy-conflicts) bölümüne bakın.

## <a name="configure-conditional-access"></a>Koşullu erişim yapılandırma

Cihazlarınızı ve kurumsal kaynaklarınızı korumak için Intune ile Azure Active Directory (Azure AD) koşullu erişim ilkelerini kullanabilirsiniz.

Intune, cihaz uyumluluk ilkelerinizin sonuçlarını Azure AD 'ye geçirir ve bu da, hangi cihazların ve uygulamaların şirket kaynaklarınıza erişebileceğini zorlamak için koşullu erişim ilkeleri kullanır. Koşullu erişim ilkeleri, Intune tarafından yönetilmeyen cihazlara erişimi geçit 'e yardımcı olabilir. Intune ile tümleştirilen [Mobile Threat Defense iş ortaklarının](../protect/mobile-threat-defense.md) uyumluluk ayrıntılarını bile kullanabilirsiniz.

Intune ile koşullu erişim kullanmanın iki yaygın yöntemi aşağıda verilmiştir:

- Yalnızca yönetilen ve uyumlu cihazların ağ kaynaklarına erişebildiğinden emin olmak için **cihaz tabanlı koşullu erişim**.
- Intune ile yönetmezseniz cihazlarda kullanıcılara ağ kaynaklarına erişimi yönetmek için uygulama koruma ilkelerini kullanan **uygulama tabanlı koşullu erişim**.

Intune ile koşullu erişim kullanma hakkında daha fazla bilgi edinmek için bkz. [koşullu erişim ve Intune hakkında bilgi edinin](../protect/conditional-access.md).

## <a name="set-up-integration-with-defender-atp"></a>Defender ATP ile tümleştirmeyi ayarlama

Microsoft Defender Gelişmiş tehdit koruması 'nı (Defender ATP) Intune ile tümleştirdiğinizde, riskleri tanımanıza ve bunlara yanıt vermeye yönelik bir özellik geliştirebilirsiniz.

Intune çeşitli [Mobile Threat Defense ortaklarıyla](../protect/mobile-threat-defense.md)tümleştirilmesine karşın, Defender ATP kullandığınızda, Defender ATP ve Intune arasında derin cihaz koruma seçeneklerine erişimi olan ve aşağıdakiler dahil sıkı bir tümleştirme elde edersiniz:

- Güvenlik görevleri: ATP ve Intune yöneticileri arasında, risk altındaki cihazlar ve bu riskler azaltıldığında yapılan onay ile sorunsuz iletişim.
- İstemcilerde Defender ATP için kolaylaştırılmış ekleme.
- Intune uyumluluk ilkelerinde ATP cihaz risk sinyalleri kullanımı.
- Yetkisiz *koruma* özelliklerine erişim.

 Intune ile Defender ATP kullanma hakkında daha fazla bilgi edinmek için bkz. [Intune 'Da koşullu erişimle Microsoft Defender ATP için uyumluluğu zorlama](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Rol tabanlı erişim denetimi gereksinimleri

Microsoft Endpoint Manager Yönetim Merkezi 'nin uç nokta güvenlik düğümündeki görevleri yönetmek için bir hesabın olması gerekir:

- Intune için bir lisans atanması.
- Rol tabanlı erişim denetimi (RBAC) izinlerinin **Endpoint Security Manager**'ın yerleşik Intune rolü tarafından belirtilen izinlere eşit olması gerekir. *Endpoint Security Manager* rolü Microsoft Endpoint Manager yönetim merkezine erişim izni verir. Bu rol, güvenlik temelleri, cihaz uyumluluğu, koşullu erişim ve Microsoft Defender ATP dahil olmak üzere güvenlik ve uyumluluk özelliklerini yöneten kişiler tarafından kullanılabilir.

Daha fazla bilgi için bkz. [rol tabanlı erişim denetimi (RBAC) Microsoft Intune ile](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>*Endpoint Security Manager* rolü tarafından verilen izinler

Microsoft Endpoint Manager Yönetim merkezinde aşağıdaki izin listesini, **kiracı yönetim**  >  **rolleri**  >  **tüm roller**' e giderek görüntüleyebilirsiniz, **Endpoint Security Manager**  >  **özellikleri**' ni seçin.

**İzinleri**

- **Android for Work**
  - Okuma
- **Denetim verileri**
  - Okuma
- **Kurumsal cihaz tanımlayıcıları**
  - Okuma
- **Cihaz uyumluluğu ilkeleri**
  - Ata
  - Oluştur
  - Sil
  - Okuma
  - Güncelleştir
  - Raporları görüntüle
- **Cihaz yapılandırmaları**
  - Okuma
- **Cihaz kaydı yöneticileri**
  - Okuma
- **Endpoint Protection raporları**
  - Okuma
- **Kayıt programları**
  - Cihazı oku
  - Profili oku
  - Belirteci oku
- **Intune veri ambarı**
  - Okuma
- **Yönetilen uygulamalar**
  - Okuma
- **Yönetilen cihazlar**
  - Sil
  - Okuma
  - Birincil kullanıcıyı ayarla
  - Güncelleştir
- **Mobil uygulamalar**
  - Okuma
- **Kuruluş**
  - Okuma
- **PolicySets**
  - Okuma
- **Uzaktan yardım**
  - Okuma
- **Uzak görevler**
  - Filekasa anahtarını alın.
- **Roller**
  - Okuma
- **Güvenlik temelleri**
  - Ata
  - Oluştur
  - Sil
  - Okuma
  - Güncelleştir
- **Güvenlik görevleri**
  - Okuma
  - Güncelleştir
- **Telekom giderleri**
  - Okuma
- **Hüküm ve koşullar**
  - Okuma

## <a name="avoid-policy-conflicts"></a>İlke çakışmalarını önleyin

Cihazlar için yapılandırabileceğiniz ayarların birçoğu, Intune 'daki farklı özelliklerle yönetilebilir. Bu özellikler şunları içerir ancak bunlarla sınırlı değildir:

- Uç nokta güvenlik ilkeleri
- Güvenlik temelleri
- Cihaz yapılandırma ilkeleri
- Windows 10 kayıt ilkeleri

Örneğin, uç nokta güvenlik ilkelerinde bulunan ayarlar, *uç nokta koruma* ve cihaz yapılandırma ilkesindeki *cihaz kısıtlama* profillerinde bulunan ve ayrıca çeşitli güvenlik temelleri aracılığıyla yönetilen ayarların bir alt kümesidir.

Çakışmaların oluşmaması için bir yol, bir cihazdaki aynı ayarları yönetmek için farklı taban çizgileri, aynı taban çizgisi örnekleri veya farklı ilke türleri ve örnekleri kullanmamalıdır. Bu, farklı cihazlara yapılandırma dağıtmak için kullanacağınız yöntemlerin planlanmasını gerektirir. Aynı ayarı yapılandırmak için birden çok yöntem veya örnek kullandığınızda, farklı metotlarınızın aynı cihazlara sahip olduğundan veya dağıtılmadığından emin olun.

Çakışmalar meydana geliyorsa, bu çakışmaların kaynağını belirlemek ve çözümlemek için Intune 'un yerleşik araçlarını kullanabilirsiniz. Daha fazla bilgi için bkz.

- [Intune'da ilke ve profil sorunları giderme](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Güvenlik temellerinizi izleyin](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Sonraki adımlar

Yapılandırma

- [Güvenlik temelleri](../protect/security-baselines.md)
- [Uyumluluk ilkeleri](../protect/device-compliance-get-started.md)
- [Koşullu erişim ilkeleri](#configure-conditional-access)
- [Defender ATP ile tümleştirme](../protect/advanced-threat-protection.md)
