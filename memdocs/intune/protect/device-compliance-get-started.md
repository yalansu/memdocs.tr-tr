---
title: Microsoft Intune - Azure’da cihaz uyumluluk ilkeleri | Microsoft Docs
description: Uyumluluk ilkesi ayarları ve Microsoft Intune yönelik cihaz uyumluluk ilkeleri de dahil olmak üzere uyumluluk ilkelerini kullanmaya başlayın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ae39f91c4daa67c40c42022f63137f0b23daf80
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911072"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Intune ile yönettiğiniz cihazların kurallarını ayarlamak için uyumluluk ilkelerini kullanma

Intune gibi mobil cihaz yönetimi (MDM) çözümleri, kullanıcıların ve cihazların bazı gereksinimleri karşılamasına gerek kalmadan kurumsal verilerin korunmasına yardımcı olabilir. Intune 'da bu özelliğe *uyumluluk ilkeleri*adı verilir.

Intune 'da uyumluluk ilkeleri:

- Kullanıcıların ve cihazların uyumlu olması için uyması gereken kuralları ve ayarları tanımlayın.
- Uyumsuz cihazlara uygulanan eylemleri dahil edin. Uyumsuzluğa yönelik eylemler, kullanıcılara uyumsuz cihazlarda uyumsuzluk ve verileri koruma koşullarına göre uyarı verebilir.
- , Kuralları karşılamayan kullanıcıları ve cihazları engelleyebilen [koşullu erişimle birleştirilebilir](#integrate-with-conditional-access).

Intune 'da uyumluluk ilkelerinin iki bölümü vardır:

- **Uyumluluk ilkesi ayarları** – her cihazın aldığı yerleşik uyumluluk ilkesi gibi kiracı genelindeki ayarlar. Uyumluluk ilkesi ayarları, herhangi bir cihaz uyumluluk ilkesi almamış cihazların uyumlu veya uyumsuz olup olmadığı dahil olmak üzere, uyumluluk ilkesinin Intune ortamınızda nasıl çalıştığı için bir taban çizgisi ayarlar.

- **Cihaz uyumluluk ilkesi** – Kullanıcı veya cihaz gruplarına yapılandırıp dağıtabileceğiniz platforma özgü kurallar.  Bu kurallar, en düşük işletim sistemleri veya disk şifrelemesi kullanımı gibi cihazlara yönelik gereksinimleri tanımlar. Cihazların uyumlu kabul edilmesi için bu kuralları karşılaması gerekir.

Diğer Intune ilkeleri gibi, cihaz için uyumluluk ilkesi değerlendirmeleri, cihaz Intune ile iade edildiğinde ve [ilke ve profil yenileme döngülerine](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)bağlı olarak değişir.

## <a name="compliance-policy-settings"></a>Uyumluluk ilkesi ayarları

*Uyumluluk ilkesi ayarları* , Intune 'un uyumluluk hizmeti 'nin cihazlarınızla nasıl etkileşime gireceğini sağlayan kiracı genelindeki bir ayarlardır. Bu ayarlar, bir cihaz uyumluluk ilkesinde yapılandırdığınız ayarlardan farklıdır.

Uyumluluk ilkesi ayarlarını yönetmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **uç nokta güvenlik**  >  **cihaz uyumluluğu**  >  **Uyumluluk ilkesi ayarları**' na gidin.

Uyumluluk ilkesi ayarları aşağıdaki ayarları içerir:

- **Uyumluluk ilkesi atanmamış cihazları işaretle**

  Bu ayar, Intune 'un cihaz uyumluluk ilkesi atanmamış cihazlara nasıl davrandığını belirler. Bu ayar iki değere sahiptir:
  - **Uyumlu** (*varsayılan*): Bu güvenlik özelliği kapalıdır. Bir cihaz uyumluluk ilkesi gönderilmemiş cihazlar *uyumlu*kabul edilir.
  - **Uyumlu değil**: Bu güvenlik özelliği açık. Bir cihaz uyumluluk ilkesi almamış cihazlar uyumsuz olarak kabul edilir.

  Cihaz uyumluluk ilkelerinizle koşullu erişim kullanırsanız, yalnızca uyumlu olarak onaylanan cihazların kaynaklarınıza erişebildiğinden emin olmak için bu ayarı **uyumlu değil** olarak değiştirmeniz önerilir.

  Bir ilke kendisine atanmadığı için bir son kullanıcı uyumlu değilse, [Şirket portalı uygulama](../apps/company-portal-app.md) hiçbir uyumluluk ilkesi atanmadığını gösterir.

- **Gelişmiş jailbreak algılama** (*yalnızca IOS/ıpados için geçerlidir*)

  Bu ayar yalnızca jailbreak uygulanmış cihazlarını engelleyen bir cihaz uyumluluk ilkesiyle hedeflediğiniz cihazlarla kullanılabilir.  (Bkz. iOS/ıpados için [cihaz durumu](compliance-policy-create-ios.md#device-health) ayarları).

  Bu ayar iki değere sahiptir:

  - **Devre dışı** (*varsayılan*): Bu güvenlik özelliği kapalıdır. Bu ayarın, jailbreak uygulanmış cihazlarını engelleyen cihaz Uyumluluk ilkesini alan cihazlarınızda hiçbir etkisi yoktur.
  - **Etkin**: Bu güvenlik özelliği açık. Jailbreak uygulanmış cihazlarını engellemek için cihaz uyumluluk ilkesi alan cihazlar, gelişmiş jailbreak algılamayı kullanır.

  Geçerli bir iOS/ıpados cihazında etkinleştirildiğinde cihaz:

  - İşletim sistemi düzeyinde konum hizmetleri 'ni sunar.
  - Her zaman Şirket Portalı konum hizmetlerini kullanmasına izin verir.
  - , Arka planda jailbreak algılamasını daha sık tetiklemek için konum hizmetlerini kullanır. Kullanıcı konum verileri, Intune tarafından depolanmaz.

  Gelişmiş jailbreak algılama, şu durumlarda bir değerlendirme çalıştırır:

  - Şirket Portalı uygulama açılır
  - Cihaz, yaklaşık olarak 500 ölçüm veya daha fazla olan önemli bir mesafeyi büyük ölçüde taşımıştır. Intune, denetimin bir cihazın ağ bağlantısına bağlı olması halinde, her önemli konum değişikliğinin bir jailbreak algılama denetimi ile sonuçlanabileceğini garanti edemez.

  İOS 13 ve üzerinde, bu özellik, cihazın arka planda konumunu kullanmasına izin Şirket Portalı vermeye devam etmek için kullanıcıların *her zaman Izin vermeyi* seçmesini gerektirir. Kullanıcılar her zaman konum erişimine izin vermediğinde ve bu ayarı yapılandırılmış bir ilkeye sahip değilse, cihazları uyumsuz olarak işaretlenir.

- **Uyumluluk durumu geçerlilik süresi (gün)**

  Cihazların tüm alınan uyumluluk ilkelerine başarıyla rapor alması gereken bir süre belirtin. Bir cihaz geçerlilik süresi dolmadan bir ilkenin uyumluluk durumunu raporlamazsa, cihaz uyumsuz olarak kabul edilir.

  Varsayılan olarak, dönem 30 gün olarak ayarlanır. 1 ile 120 gün arasında bir dönem yapılandırabilirsiniz.

  Geçerlilik süresi ayarı ile cihaz uyumluluğuyla ilgili ayrıntıları görüntüleyebilirsiniz. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **cihazlar**  >  **izleyici**  >  **ayarı uyumluluğu**' na gidin. Bu ayar, *ayar* sütununda **etkin** bir ada sahiptir.  Bu ve ilgili uyumluluk durumu görünümleri hakkında daha fazla bilgi için bkz. [Cihaz uyumluluğunu izleme](compliance-policy-monitor.md).

## <a name="device-compliance-policies"></a>Cihaz uyumluluğu ilkeleri

Intune cihaz uyumluluk ilkeleri:

- Kullanıcıların ve yönetilen cihazların uyumlu olması için uyması gereken kuralları ve ayarları tanımlayın. Kuralların örnekleri şunlardır: cihazların en düşük işletim sistemi sürümünü çalıştırmasını, caıl olmayan veya kökü belirtilmemiş olduğunu ve Intune ile tümleştirmiş olduğunuz tehdit yönetimi yazılımıyla belirtilen *tehdit düzeyinde* ya da bu düzeyin altında olmasını gerektirir.
- Uyumluluk kurallarınızı karşılamayan cihazlar için uygulanan işlemleri destekler. Eylemlere örnek olarak uzaktan kilitleme veya cihaz durumu hakkında cihaz Kullanıcı e-postası gönderme dahil olmak üzere, bunları çözebilmeleri gerekir.
- Cihaz gruplarındaki Kullanıcı gruplarında veya cihazlarda kullanıcılara dağıtın. Bir uyumluluk ilkesi bir kullanıcıya dağıtıldığında tüm kullanıcı cihazlarının uyumluluk denetimi yapılır. Bu senaryoda cihaz gruplarını kullanmak, uyumluluk raporlamasına yardımcı olur.

Koşullu erişim kullanırsanız, koşullu erişim ilkeleriniz, uyumsuz cihazlardan kaynaklara erişimi engellemek için cihaz uyumluluk sonuçlarınızı kullanabilir.

Bir cihaz uyumluluk ilkesinde belirtebileceğiniz kullanılabilir ayarlar, ilke oluştururken seçtiğiniz platform türüne bağlıdır. Farklı cihaz platformları farklı ayarları destekler ve her platform türü ayrı bir ilke gerektirir.  

Aşağıdaki konular, cihaz yapılandırma ilkesinin farklı yönleri için adanmış makalelere bağlantı sağlar.

- [**Uyumsuzluk eylemleri**](actions-for-noncompliance.md) -her cihaz uyumluluk ilkesi, uyumsuzluk için bir veya daha fazla eylem içerir. Bu eylemler, ilkede ayarladığınız koşullara uymayan cihazlara uygulanan kurallardır.

  Varsayılan olarak, her cihaz uyumluluk ilkesi bir ilke kuralına uyamazsa cihazı uyumsuz olarak işaretleme eylemini içerir. İlke daha sonra, bu eylemler için ayarladığınız zamanlamalara göre, daha sonra yapılandırdığınız uyumsuzluğa yönelik ek eylemler için geçerlidir.

  Uyumsuzluğa yönelik eylemler, cihazları cihaz uyumlu olmadığında veya bir cihazda olabilecek verileri korumak için kullanıcılara uyarı verebilir. Eylemlere örnek olarak şunlar verilebilir:

  - Uyumlu olmayan cihazla ilgili ayrıntılarla kullanıcılara ve gruplara **e-posta uyarıları gönderme** . İlkeyi, uyumsuz olarak işaretlendikten hemen sonra bir e-posta gönderecek şekilde yapılandırabilir ve ardından, cihaz uyumlu olana kadar düzenli aralıklarla bir e-posta gönderilir.
  - Bir süredir uyumsuz olan **cihazları uzaktan kilitleyin** .
  - Cihazları bir süre uyumsuz olduktan sonra **devre dışı bırakın** . Bu eylem, cihazı Intune yönetiminden kaldırır ve cihazdaki tüm şirket verilerini kaldırır.

- [**Ağ konumlarını yapılandırma**](use-network-locations.md) -Android cihazlar tarafından desteklenen *ağ konumlarını* yapılandırabilir ve ardından bu konumları cihaz uyumluluk kuralı olarak kullanabilirsiniz. Bu tür bir kural, belirtilen bir ağın dışında veya ayrıldığında bir cihazı uyumsuz olarak işaret edebilir. Bir konum kuralı belirlemeden önce, ağ konumlarını yapılandırmanız gerekir.

- [**Ilke oluşturma**](create-compliance-policy.md) – bu makaledeki bilgilerle önkoşulları gözden geçirebilir, kuralları yapılandırmak için seçenekler aracılığıyla çalışabilir, uyumsuzluk için Eylemler belirtebilir ve ilkeyi gruplara atayabilirsiniz. Bu makale ayrıca ilke yenileme süreleri hakkında bilgiler içerir.

  Farklı cihaz platformları için cihaz uyumluluk ayarlarını görüntüleyin:

  - [Android](compliance-policy-create-android.md)
  - [Android Kurumsal](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows 10 Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows 8.1 ve üzeri](compliance-policy-create-windows-8-1.md)
  - [Windows 10 ve üzeri](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Uyumluluk durumunu izleme

Intune, cihazların uyumluluk durumunu izlemek ve daha fazla bilgi için ilkeler ve cihazlarda detaya gitmek üzere kullandığınız bir cihaz uyumluluk panosu içerir. Bu Pano hakkında daha fazla bilgi edinmek için bkz. [Cihaz uyumluluğunu izleme](compliance-policy-monitor.md).

## <a name="integrate-with-conditional-access"></a>Koşullu erişimle tümleştirin

Koşullu erişim kullandığınızda, koşullu erişim ilkelerinizi, hangi cihazların kurumsal kaynaklarınıza erişebileceğini belirleyebilmek için cihaz uyumluluk ilkelerinizin sonuçlarını kullanacak şekilde yapılandırabilirsiniz. Bu erişim denetimi, cihaz uyumluluk ilkelerine dahil ettiğiniz uyumsuzluğa ek olarak ve eylemlerden ayrı olarak yapılır.

Bir cihaz Intune 'A kaydedildiğinde Azure AD 'ye kaydolur. Cihazların uyumluluk durumu Azure AD 'ye bildirilir. Koşullu erişim ilkeleriniz, *cihazın uyumlu olarak Işaretlenmesini gerektir*olarak ayarlanmış erişim denetimlerine sahipseniz, koşullu erişim, e-postaya ve diğer kuruluş kaynaklarına erişim izni verip vermeyeceğinizi öğrenmek için bu uyumluluk durumunu kullanır.

Koşullu erişim ilkeleriyle cihaz uyumluluk durumunu kullanacaksanız, kiracınızın, uyumluluk ilkesi [ayarları](#compliance-policy-settings)altında yönettiğiniz *Uyumluluk Ilkesi atanmamış şekilde işaretleme cihazlarını*nasıl yapılandırdığınıza bakın.

Cihaz uyumluluk ilkelerinizle koşullu erişimi kullanma hakkında daha fazla bilgi için bkz. [cihaz tabanlı koşullu erişim](conditional-access-intune-common-ways-use.md#device-based-conditional-access)

Azure AD belgelerinde koşullu erişim hakkında daha fazla bilgi edinin:

- [Koşullu erişim nedir?](/azure/active-directory/conditional-access/overview)
- [Cihaz kimliği nedir?](/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Farklı platformlarda uyumsuzluk ve koşullu erişim için başvuru

Aşağıdaki tabloda, bir uyumluluk ilkesi koşullu erişim ilkesi ile kullanıldığında uyumlu olmayan ayarların nasıl yönetildiği açıklanır.

- **Düzeltildi**: cihaz işletim sistemi uyumluluğu zorluyor. Örneğin, kullanıcı bir PIN ayarlamaya zorlanır.

- **Karantinaya alındı**: cihaz işletim sistemi uyumluluğu zorlamaz. Örneğin Android ve Android Kurumsal cihazlar kullanıcıyı cihazı şifrelemeye zorlamaz. Cihaz uyumsuz olduğunda aşağıdaki işlemler yapılır:
  - Kullanıcı için bir koşullu erişim ilkesi geçerliyse cihaz engellenir.
  - Şirket Portalı uygulaması, tüm uyumluluk sorunları hakkında kullanıcıya bildirim gönderir.

---------------------------

|**İlke ayarı**| **Platform** |
| --- | ----|
| **PIN veya parola yapılandırması** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı  <br>  <br>- **iOS 8,0 ve üzeri**: düzeltildi<br>- **MacOS 10,11 ve üzeri**: düzeltildi  <br>  <br>- **Windows 8.1 ve üzeri**: düzeltildi|
| **Cihaz şifrelemesi** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı<br><br>- **iOS 8,0 ve üzeri**: DÜZELTILEN (PIN ayarlanarak)<br>- **MacOS 10,11 ve üzeri**: DÜZELTILEN (PIN ayarlanarak)<br><br>- **Windows 8.1 ve üzeri**: geçerli değil|
| **Güvenliği kırılmış veya kökü belirtilen cihaz** | - **Android 4,0 ve üzeri**: karantinaya alındı (ayar değil)<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı (ayar değil)<br>- **Android Enterprise**: karantinaya alındı (ayar değil)<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı (ayar değil)<br>- **MacOS 10,11 ve üzeri**: geçerli değil<br><br>- **Windows 8.1 ve üzeri**: geçerli değil |
| **E-posta profili** | - **Android 4,0 ve üzeri**: uygulanamaz<br>- **Samsung KNOX Standard 4,0 ve üzeri**: uygulanamaz<br>- **Android Enterprise**: uygulanamaz<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı<br>- **MacOS 10,11 ve üzeri**: karantinaya alındı<br><br>- **Windows 8.1 ve üzeri**: geçerli değil |
| **En düşük işletim sistemi sürümü** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı<br>- **MacOS 10,11 ve üzeri**: karantinaya alındı<br><br>- **Windows 8.1 ve üzeri**: karantinaya alındı|
| **En yüksek işletim sistemi sürümü** | - **Android 4,0 ve üzeri**: karantinaya alındı<br>- **Samsung KNOX Standard 4,0 ve üzeri**: karantinaya alındı<br>- **Android Enterprise**: karantinaya alındı<br><br>- **iOS 8,0 ve üzeri**: karantinaya alındı<br>- **MacOS 10,11 ve üzeri**: karantinaya alındı<br><br>- **Windows 8.1 ve üzeri**: karantinaya alındı |
| **Windows durum kanıtlama** | - **Android 4,0 ve üzeri**: uygulanamaz<br>- **Samsung KNOX Standard 4,0 ve üzeri**: uygulanamaz<br>- **Android Enterprise**: uygulanamaz<br><br>- **iOS 8,0 ve üzeri**: uygulanamaz<br>- **MacOS 10,11 ve üzeri**: geçerli değil<br><br>- **Windows 10**: karantinaya alındı<br>- **Windows 8.1 ve üzeri**: karantinaya alındı |

---------------------------

## <a name="next-steps"></a>Sonraki adımlar

- Android cihazlarla kullanılmak üzere [konumları yapılandırma](../protect/use-network-locations.md)
- [Ilke oluşturma ve dağıtma](../protect/create-compliance-policy.md) ve önkoşulları gözden geçirme
- [Cihaz uyumluluğunu izleme](../protect/compliance-policy-monitor.md)
- [Microsoft Intune 'deki cihaz ilkeleri ve profillerle ilgili yaygın sorular, sorunlar ve çözümler](../configuration/device-profile-troubleshoot.md)
- [İlke varlıkları Için başvuru](../developer/reports-ref-policy.md) , Intune veri ambarı ilke varlıkları hakkında bilgiler içerir