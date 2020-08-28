---
title: Intune ile iOS ve Android için Office 'i yönetme
titleSuffix: ''
description: İOS ve Android için Office ile Intune uygulama koruma ve yapılandırma ilkelerini kullanarak, işbirliği deneyimlerinin yerinde korumalar için her zaman erişilebilir olmasını sağlayın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 06d53789bb80475528bd413d14015e30d09fca64
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996665"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>İOS ve Android için Office kullanarak işbirliği deneyimlerini Microsoft Intune ile yönetin

İOS ve Android için Office aşağıdakiler dahil çeşitli önemli avantajlar sunar:

- Word, Excel ve PowerPoint 'i, indirme veya aralarında geçiş yapmak için daha az uygulama deneyimini kolaylaştıran bir biçimde birleştirme. Zaten bildiğiniz ve kullandıkları mevcut mobil uygulamaların neredeyse tüm özelliklerini koruyarak, tek tek uygulamaları yüklemekten çok daha az telefon depolama alanı gerektirir.
- Görüntüyü düzenlenebilir Word ve Excel belgelerine dönüştürme, PDF 'Leri tarama ve içeriği daha kolay okunabilir hale getirmek için otomatik dijital geliştirmeler ile beyaz tahtaların yakalanması gibi yetenekler sayesinde, Office Lens teknolojisini tümleştirme.
- Genellikle bir telefonda çalışırken karşılaştığı yaygın görevler için yeni işlevsellik ekleme; hızlı not oluşturma, PDF imzalama, QR kodlarını tarama ve cihazlar arasında dosya aktarma gibi şeyler.

Microsoft 365 verilerine yönelik zengin ve en geniş koruma özellikleri, koşullu erişim gibi Microsoft Intune ve Azure Active Directory Premium özellikleri içeren Enterprise Mobility + Security Suite 'e abone olduğunuzda kullanılabilir. En azından, mobil cihazlardan iOS ve Android için Office bağlantısına izin veren bir koşullu erişim ilkesi ve işbirliği deneyiminin korunmasını sağlayan bir Intune uygulama koruma ilkesi dağıtmanız gerekir.

## <a name="apply-conditional-access"></a>Koşullu erişim Uygula
Kuruluşlar, kullanıcıların yalnızca iOS ve Android için Office kullanarak iş veya okul içeriğine erişebildiğinden emin olmak için Azure AD koşullu erişim ilkelerini kullanabilir. Bunu yapmak için tüm olası kullanıcıları hedefleyen bir koşullu erişim ilkesine ihtiyacınız olacaktır. Bu ilkeyi oluşturma hakkındaki ayrıntılar, [bulut uygulaması Için koşullu erişimle uygulama koruma Ilkesi iste](/azure/active-directory/conditional-access/app-protection-based-conditional-access)' de bulunabilir.

1. "Adım 1: Office 365 için Azure AD koşullu erişim ilkesi yapılandırma" yı izleyin. [Senaryo 1: office 365 uygulamaları](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), IOS ve Android için Office 'e izin veren ve üçüncü taraf OAuth özellikli mobil cihaz istemcilerinin Office 365 uç noktalarına bağlanmasını engelleyen uygulama koruma ilkeleriyle onaylanan uygulamalar gerektirir.

   >[!NOTE]
   > Bu ilke, mobil kullanıcıların tüm Office uç noktalarına ilgili uygulamaları kullanarak erişmesini sağlar.

## <a name="create-intune-app-protection-policies"></a>Intune uygulama koruma ilkeleri oluşturma

Uygulama koruma Ilkeleri (uygulama) hangi uygulamalara izin verileceğini ve kuruluşunuzun verileriyle alabilecekleri eylemleri tanımlar. UYGULAMADA kullanılabilen seçimler, kuruluşların korumayı özel gereksinimlerine uyarlamalarını sağlar. Bazıları için, bir bütün senaryoyu uygulamak için hangi ilke ayarlarının gerekli olduğu açık olmayabilir. Microsoft, kuruluşların mobil istemci uç noktası sağlamlaştırma için öncelik vermesini sağlamak üzere iOS ve Android mobil uygulama yönetimi için uygulama veri koruma çerçevesi için Taksonomi sunmuştur.

UYGULAMA veri koruma çerçevesi, her düzey bir önceki düzeyin üzerinde oluşturulmasıyla birlikte üç ayrı yapılandırma düzeyi halinde düzenlenmiştir:

- **Kurumsal temel veri koruması** (düzey 1), uygulamaların PIN ile korunmasını ve şifreli silme işlemleri gerçekleştirmesini sağlar. Android cihazlar için bu düzey, Android cihaz kanıtlamasını doğrular. Bu, Exchange Online posta kutusu ilkelerinde benzer veri koruma denetimi sağlayan ve bunu ve Kullanıcı popülasyonu uygulamayı sunan bir giriş düzeyi yapılandırmadır.
- **Kurumsal gelişmiş veri koruması** (düzey 2), uygulama veri sızıntısı önleme mekanizmalarını ve en düşük işletim sistemi gereksinimlerini tanıtır. Bu, iş veya okul verilerine erişen mobil kullanıcıların çoğu için geçerli olan yapılandırmadır.
- **Kurumsal yüksek veri koruma** (düzey 3) gelişmiş veri koruma mekanizmaları, gelişmiş PIN YAPıLANDıRMASı ve uygulama mobil tehdit savunması sağlar. Bu yapılandırma, yüksek riskli verilere erişen kullanıcılar için istenir.

Her yapılandırma düzeyi ve korunması gereken en düşük uygulamalar için belirli önerilere bakmak için, [Uygulama koruma ilkelerini kullanarak Data Protection Framework 'ü](app-protection-framework.md)inceleyin.

Cihazın birleştirilmiş bir uç nokta yönetimi (UEM) çözümüne kaydolmasından bağımsız olarak, [Uygulama koruma ilkeleri oluşturma ve atama](app-protection-policies.md)bölümündeki adımları kullanarak hem iOS hem de Android Uygulamaları Için bir Intune uygulama koruma ilkesi oluşturulması gerekir. En azından bu ilkelerin aşağıdaki koşullara uyması gerekir:

1. Bu kişiler, Edge, Outlook, OneDrive, Office veya takımlar gibi tüm mobil uygulamaları Microsoft 365, böylece kullanıcıların herhangi bir Microsoft uygulamasındaki iş veya okul verilerine güvenli bir şekilde erişebilmesini ve bunları işleyebilmesini sağlar.

2. Bunlar tüm kullanıcılara atanır. Bu, iOS veya Android için Office 'i kullanıp kullanmadıklarından bağımsız olarak tüm kullanıcıların korunmasını sağlar.

3. Gereksinimlerinizi karşılayan çerçeve düzeyini saptayın. Çoğu kuruluş, veri koruma ve erişim gereksinimleri denetimlerine izin veren şekilde **Kurumsal gelişmiş veri koruması** 'nda (düzey 2) tanımlanan ayarları uygulamalıdır.

Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Android uygulama koruma ilkesi ayarları](app-protection-policy-settings-android.md) ve [iOS uygulama koruma ilkesi ayarları](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Intune uygulama koruma ilkelerini Intune 'a kayıtlı olmayan Android cihazlarda uygulamalara uygulamak için, kullanıcının da Intune Şirket Portalı yüklemesi gerekir. Daha fazla bilgi için bkz. [Android uygulamanız uygulama koruma ilkeleriyle yönetildiğinde beklemeniz gerekenler](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Uygulama yapılandırmasını kullanma

İOS ve Android için Office, Microsoft Endpoint Manager gibi yöneticilerin uygulamanın davranışını özelleştirmesini sağlayan uygulama ayarlarını destekler.

Uygulama yapılandırması, kayıtlı cihazlarda mobil cihaz yönetimi (MDM) işletim sistemi kanalı aracılığıyla (iOS için[yönetilen uygulama yapılandırma](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) kanalı veya Android için [kuruluş kanalında android](https://developer.android.com/work/managed-configurations) ) veya Intune uygulama koruması ilkesi (uygulama) kanalı aracılığıyla teslim edilebilir. İOS ve Android için Office aşağıdaki yapılandırma senaryolarını destekler:

- Yalnızca iş veya okul hesaplarına izin ver
- Veri koruma ayarları

> [!IMPORTANT]
> Android 'de cihaz kaydı gerektiren yapılandırma senaryolarında cihazların Android Enterprise 'a kayıtlı olması ve Android için Office 'in yönetilen Google Play deposu aracılığıyla dağıtılması gerekir. Daha fazla bilgi için bkz. [Android kurumsal iş profili cihazlarının kaydını ayarlama](../enrollment/android-work-profile-enroll.md) ve [yönetilen Android Kurumsal cihazları için uygulama yapılandırma ilkeleri ekleme](app-configuration-policies-use-android.md).

Her yapılandırma senaryosunda belirli gereksinimler vurgulanmıştır. Örneğin, yapılandırma senaryosunun cihaz kaydı gerektirip gerektirmediğini ve bu nedenle herhangi bir UıEM sağlayıcısıyla çalışıp çalışmadığını veya Intune Uygulama Koruması Ilke gerektirip gerektirmediğini belirtir.

> [!NOTE]
> Microsoft Endpoint Manager ile, MDM işletim sistemi kanalı üzerinden sunulan uygulama yapılandırması, **yönetilen cihazlar** uygulama yapılandırma IlkesI (ACP) olarak adlandırılır; Uygulama koruma Ilkesi kanalı üzerinden sunulan uygulama yapılandırması, **yönetilen uygulamalar** uygulama yapılandırma ilkesi olarak adlandırılır.

## <a name="only-allow-work-or-school-accounts"></a>Yalnızca iş veya okul hesaplarına izin ver

En büyük ve yüksek oranda düzenlenen müşterilerinin veri güvenliği ve uyumluluk ilkeleri, Microsoft 365 değerine göre önemli bir değerdir. Bazı şirketlerin kurumsal ortamlarında tüm iletişim bilgilerini yakalama gereksinimi vardır ve ayrıca cihazların yalnızca kurumsal iletişimler için kullanıldığından emin olun. Bu gereksinimleri desteklemek için, kayıtlı cihazlarda Android için Office, yalnızca tek bir şirket hesabının uygulama içinde sağlanmasını sağlayacak şekilde yapılandırılabilir.

Aşağıdaki kuruluş izin verilen hesaplar modu ayarını yapılandırma hakkında daha fazla bilgi edinebilirsiniz:

- [Android ayarı](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Bu yapılandırma senaryosu yalnızca kayıtlı cihazlarla birlikte kullanılabilir. Ancak, herhangi bir UıEM sağlayıcısı desteklenir. Microsoft Endpoint Manager kullanmıyorsanız, bu yapılandırma anahtarlarının nasıl dağıtılacağı konusunda UEM belgelerinize danışmanız gerekir.

> [!NOTE]
> Şu anda yalnızca Android için Office, kuruluş izin verilen hesaplar modunu destekler.

## <a name="data-protection-app-configuration-scenarios"></a>Veri koruma uygulaması yapılandırma senaryoları

İOS ve Android için Office, uygulama Microsoft Uç Nokta Yöneticisi tarafından uygulamada oturum açan iş veya okul hesabına uygulanan bir Intune Uygulama Koruması Ilkesiyle yönetildiğinde aşağıdaki veri koruma ayarları için uygulama yapılandırma ilkelerini destekler:

- Dosya aktarma eylemi aracılığıyla dosya aktarımlarını yönetme
- Dosya aktarımlarını yakında paylaşma eylemiyle yönetin

Bu ayarlar, cihaz kayıt durumundan bağımsız olarak uygulamaya dağıtılabilir.

### <a name="manage-file-transfers"></a>Dosya aktarımlarını yönetme

Varsayılan olarak, iOS ve Android için Office, kullanıcıların çeşitli mekanizmalar kullanarak içerik paylaşmasını sağlar:

- Dosya OneDrive veya SharePoint 'te barındırılıyorsa, kullanıcılar doğrudan dosya içinde bir Share isteği başlatabilir.
- Kullanıcılar dosyaları **aktarma** eylemini kullanarak masaüstü sistemlerine dosya aktarabilir.
- Kullanıcılar **yakında paylaşma** eylemini kullanarak yakındaki mobil cihazlara dosya paylaşabilir.

**Dosya aktarma** ve **yakın işlemleri paylaşma** yalnızca medya, yerel dosyalar ve bir uygulama koruma ilkesi tarafından korunmayan dosyalarla çalışır. 

|    Anahtar    |    Değer    |
|-------------------------------------------------------------------|-------------|
|    com. Microsoft. Office. ShareNearby. IsAllowed. ıntunemamonly    |    **true** (varsayılan) iş veya okul hesabı Için yakında paylaşma özelliğini sunar<br>**false** , iş veya okul hesabı Için yakın paylaşılan özelliği devre dışı bırakır    |
|    com. Microsoft. Office. TransferFiles. IsAllowed. ıntunemamonly    |    **true** (varsayılan) iş veya okul hesabı Için dosya aktarma özelliğini sunar<br>**false** , iş veya okul hesabı Için dosya aktarma özelliğini devre dışı bırakır    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Microsoft Uç Nokta Yöneticisi ile uygulama yapılandırma senaryolarını dağıtma

Mobil uygulama yönetimi sağlayıcınız olarak Microsoft Uç Nokta Yöneticisi 'ni kullanıyorsanız, veri koruma uygulaması yapılandırma senaryoları için yönetilen uygulamalar uygulama yapılandırma ilkesi oluşturma hakkında [cihaz kaydı olmadan yönetilen uygulamalar için uygulama yapılandırma Ilkeleri ekleme](app-configuration-policies-managed-app.md) bölümüne bakın. Yapılandırma oluşturulduktan sonra ilkeyi Kullanıcı gruplarına atayabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama koruma ilkeleri nelerdir?](app-protection-policy.md) 
- [Microsoft Intune için uygulama yapılandırma ilkeleri](app-configuration-policies-overview.md)