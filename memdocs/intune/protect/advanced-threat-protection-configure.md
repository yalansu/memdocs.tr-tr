---
title: Microsoft Intune-Azure 'da Microsoft Defender ATP 'yi yapılandırma | Microsoft Docs
description: ATP 'ye bağlanma, cihazları ekleme, risk düzeyleri için uyumluluk atama ve koşullu erişim ilkeleri de dahil olmak üzere Intune 'da Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) yapılandırın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9c3e456722d0b747a07c3f7040edc2cdf28f264
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909593"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Intune 'da Microsoft Defender ATP 'yi yapılandırma

Bu makaledeki bilgiler ve yordamlar, Microsoft Defender ATP 'yi Intune ile tümleştirmeyi yapılandırmanıza yardımcı olur. Yapılandırma aşağıdaki genel adımları içerir:

- Kiracınız için Microsoft Defender ATP 'yi etkinleştirin
- Windows ve Android çalıştıran cihazları ekleme
- Uyumluluk ilkelerini kullanarak cihaz risk düzeylerini ayarlama
- Beklenen risk düzeylerinizi aşan cihazları engellemek için koşullu erişim ilkelerini kullanın

Başlamadan önce ortamınızın, Microsoft Defender ATP 'yi Intune ile kullanma [önkoşullarını](../protect/advanced-threat-protection.md#prerequisites) karşılaması gerekir.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Intune 'da Microsoft Defender ATP 'yi etkinleştirme

İlk adım, Intune ile Microsoft Defender ATP arasında hizmetten hizmete bağlantı kurmak için kullanılır. Kurulumu, hem Microsoft Defender güvenlik merkezi hem de Intune için yönetici erişimi gerektirir.

Yalnızca Microsoft Defender ATP 'yi her kiracı için tek bir kez etkinleştirmeniz gerekir.

### <a name="to-enable-microsoft-defender-atp"></a>Microsoft Defender ATP 'yi etkinleştirmek için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **Microsoft Defender ATP**' yi seçin ve ardından **Microsoft Defender Güvenlik Merkezi 'ni aç**' ı seçin.

   ![Microsoft Defender Güvenlik Merkezi 'ni açmak için seçin](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. **Microsoft Defender Güvenlik Merkezi**'nde:
   1. **Ayarlar**  >  **Gelişmiş Özellikler**' i seçin.
   2. **Microsoft Intune bağlantısı** için **Açık** seçeneğini belirleyin:

      ![Intune bağlantısını etkinleştirme](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

   3. **Tercihleri kaydet**’i seçin.

4. Microsoft Endpoint Manager Yönetim merkezinde **Microsoft Defender ATP** 'ye dönün. **MDM uyumluluk Ilkesi ayarları**altında kuruluşunuzun ihtiyaçlarına bağlı olarak:
   - **Windows cihazları 10.0.15063 ve sonraki sürümlerini Microsoft Defender ATP** 'yi **Açık** olarak ayarla
   - **6.0.0 ve üzeri sürüm Android cihazlarını açık olarak Microsoft Defender ATP 'ye bağlama** **On**

5. **Kaydet**’i seçin.

> [!TIP]
> Yeni bir uygulamayı Intune mobil tehdit savunması ile tümleştirdiğinizde ve Intune bağlantısını etkinleştirdiğinizde, Intune Azure Active Directory içinde klasik bir koşullu erişim ilkesi oluşturur. [Microsoft Defender ATP](advanced-threat-protection.md) veya ek [MTD iş ortaklarından](mobile-threat-defense.md#mobile-threat-defense-partners)herhangi biri dahil olmak üzere tümleştirilen her MTD uygulaması yeni bir klasik koşullu erişim ilkesi oluşturur. Bu ilkeler yoksayılabilir, ancak düzenlenmemelidir, silinmemelidir veya devre dışı bırakılmalıdır.
>
> Klasik ilke silinirse, oluşturulduktan sorumlu olan Intune bağlantısını silmeniz ve sonra yeniden ayarlamanız gerekecektir. Bu, klasik ilkeyi yeniden oluşturur. , MTD uygulamaları için klasik ilkelerin, koşullu erişim için yeni ilke türüne geçirilmesi desteklenmez.
>
> MTD uygulamaları için klasik koşullu erişim ilkeleri:
>
> - , Cihazların Azure AD 'ye kaydolmasını gerektirmek için, MTD iş ortaklarıyla iletişim kurmadan önce cihaz KIMLIĞI olması için Intune MTD tarafından kullanılır. KIMLIK, cihazların ve durumlarını Intune 'a başarıyla bildirebileceği şekilde gereklidir.
> - Diğer bulut uygulamaları veya kaynakları üzerinde hiçbir etkisi yoktur.
> - , MTD 'leri yönetmeye yardımcı olmak için oluşturabileceğiniz koşullu erişim ilkelerinden farklıdır.
> - Varsayılan olarak, değerlendirme için kullandığınız diğer koşullu erişim ilkeleriyle etkileşime geçin.
>
> Klasik koşullu erişim ilkelerini görüntülemek için [Azure](https://portal.azure.com/#home)'da **Azure Active Directory**  >  **koşullu erişim**  >  **Klasik ilkeleri**' ne gidin.

## <a name="onboard-devices"></a>Yerleşik cihazlar

Intune 'da Microsoft Defender ATP desteğini etkinleştirdiğinizde, Intune ile Microsoft Defender ATP arasında bir hizmetten hizmete bağlantı kurarsınız. Daha sonra Intune ile yönettiğiniz cihazları, cihaz risk düzeyleriyle ilgili veri toplamayı sağlayan Microsoft Defender ATP 'ye ekleyebilirsiniz.

### <a name="onboard-windows-devices"></a>Windows cihazları ekleme

Intune ile Microsoft Defender ATP arasında bağlantı kurduktan sonra Intune, Microsoft Defender ATP 'den bir Microsoft Defender ATP ekleme yapılandırma paketi aldı. Bu yapılandırma paketini, Microsoft Defender ATP için bir cihaz yapılandırma profili ile Windows cihazlarınıza dağıtırsınız.

Yapılandırma paketi, cihazları taramak ve tehditleri algılamak için [Microsoft Defender ATP hizmetleriyle](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) iletişim kuracak cihazları yapılandırır. Cihaz ayrıca, oluşturacağınız uyumluluk ilkelerine bağlı olarak cihaz risk düzeyini Microsoft Defender ATP 'ye bildirmek üzere de yapılandırılır.

Yapılandırma paketini kullanarak bir cihaz ekledikten sonra, bunu tekrar yapmanız gerekmez. Ayrıca, bir [Grup İlkesi veya Microsoft uç noktası Configuration Manager](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints)kullanarak da cihaz ekleyebilirsiniz.

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Windows cihazlarını eklemek için cihaz yapılandırma profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. **Platform**için **Windows 10 ve üzeri** ' i seçin
4. **Profil türü**Için, **Microsoft Defender ATP (Windows 10 Masaüstü)** öğesini seçin ve ardından **Oluştur**' u seçin.
5. **Temel bilgiler** sayfasında, profil Için bir *ad* ve *Açıklama* (Isteğe bağlı) girin ve ardından **İleri**' yi seçin.
6. **Yapılandırma ayarları** sayfasında, aşağıdakileri yapılandırın:

   - **Microsoft Defender ATP istemci yapılandırma paketi türü**: yapılandırma paketini profile **eklemek için Ekle** ' yi seçin. Yapılandırma paketini profilden çıkarmak için **Çıkar**’ı seçin.
  
     > [!NOTE]
     > Microsoft Defender ATP ile düzgün bir şekilde bağlantı oluşturduysanız, **Intune otomatik olarak yapılandırma profilini,** **Microsoft Defender ATP istemci yapılandırma paketi türü** ayarını de kullanıma sunulacaktır.
  
   - **Tüm dosyalar Için örnek paylaşımı**: **Etkinleştir** , örneklerin toplanmasına ve Microsoft Defender ATP ile paylaşılmasına olanak tanır. Örneğin, şüpheli bir dosya görürseniz, ayrıntılı analiz için Microsoft Defender ATP 'ye gönderebilirsiniz. **Yapılandırılmadı** , MICROSOFT Defender ATP 'ye herhangi bir örnek paylaşmaz.
   - **Telemetri raporlama sıklığını**hızlandırın: yüksek riskli olan cihazlar için bu ayarı **etkinleştirin** ve bu AYARı, Microsoft Defender ATP hizmetine daha sık telemetri rapor eder.

     [Microsoft uç noktası Configuration Manager kullanarak Windows 10 makineleri](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) eklemek, bu MICROSOFT Defender ATP ayarları hakkında daha fazla bilgi içerir.

7. **Kapsam etiketleri** sayfasını açmak için **İleri ' yi** seçin. Kapsam etiketleri isteğe bağlıdır. Devam etmek için **İleri** seçeneğini belirleyin.

8. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

   **İleri**’yi seçin.

9. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.
 **Tamam**' a tıklayın ve ardından profil oluşturan değişikliklerinizi kaydetmek için **oluşturun** .

### <a name="onboard-android-devices"></a>Android cihazları ekleme

Intune ile Microsoft Defender ATP arasında hizmetten hizmete bağlantı kurduktan sonra, Android cihazlarını Microsoft Defender ATP 'ye ekleyebilirsiniz. Ekleme cihazları Defender ATP ile iletişim kuracak şekilde yapılandırır, bu da cihazların risk düzeyiyle ilgili verileri toplar.

Windows cihazlarından farklı olarak, Android çalıştıran cihazlar için bir yapılandırma paketi yoktur. Bunun yerine, Android için Microsoft Defender ATP belgelerindeki Android için Microsoft Defender ATP belgelerine [genel bakış](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) ve Android için ekleme yönergeleri için bkz..

Android çalıştıran cihazlar için, Android 'de Microsoft Defender ATP 'yi değiştirmek üzere Intune ilkesini de kullanabilirsiniz. Daha fazla bilgi için bkz. [Microsoft Defender ATP Web koruması](../protect/advanced-threat-protection-manage-android.md).

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Cihaz risk düzeyini ayarlamak için uyumluluk ilkesi oluşturma ve atama

Hem Windows hem de Android cihazlarda, uyumluluk ilkesi bir cihaz için kabul edilebilir olarak düşünmeniz gereken risk düzeyini belirler.

Uyumluluk ilkesi oluşturma konusunda bilgi sahibi değilseniz *Microsoft Intune ' de uyumluluk ilkesi oluşturma bölümünde* [ilke oluşturma](../protect/create-compliance-policy.md#create-the-policy) yordamına başvurun. Aşağıdaki bilgiler, uyumluluk ilkesinin bir parçası olarak Microsoft Defender ATP 'yi yapılandırmaya özgüdür.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **uyumluluk ilkeleri**  >  **ilkeleri**  >  **ilke oluştur**' u seçin.

3. **Platform**için açılan kutuyu kullanarak aşağıdaki seçeneklerden birini belirleyin:
   - **Windows 10 ve üzeri**
   - **Android cihaz yöneticisi**
   - **Android Kurumsal**

   Ardından, **Oluştur** ' u seçerek **ilke yapılandırma oluştur** penceresini açın.

4. Bu ilkeyi daha sonra tanımanıza yardımcı olacak bir **ad** belirtin. Bir **Açıklama**belirtmeyi de tercih edebilirsiniz.
  
5. **Uyumluluk ayarları** sekmesinde, **Microsoft Defender ATP** grubunu genişletin ve **cihazın makine risk puanı altında veya altında olmasını gerektir** seçeneğini tercih ettiğiniz düzeye ayarlayın.

   Tehdit düzeyi sınıflandırmaları, [Microsoft Defender ATP tarafından belirlenir](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Temiz**: En güvenli düzeydir. Cihazda mevcut tehditler bulunamaz ve şirket kaynaklarına erişmeye devam edin. Herhangi bir tehdit bulunursa cihaz uyumsuz olarak değerlendirilir. (Microsoft Defender ATP, *güvenli*değeri kullanır.)
   - **Düşük**: Cihaz, yalnızca düşük düzeydeki tehditler varsa uyumludur. Orta veya yüksek tehdit düzeylerine sahip cihazlar uyumlu değildir.
   - **Orta**: Cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumludur. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
   - **Yüksek**: Bu düzey en az güvenlidir ve tüm tehdit düzeylerine izin verir. Yüksek, orta veya düşük tehdit düzeylerine sahip cihazlar uyumlu kabul edilir.

6. İlkenin geçerli gruplara atanması dahil olmak üzere ilkenin yapılandırmasını doldurun.


## <a name="create-a-conditional-access-policy"></a>Koşullu erişim ilkesi oluşturma

Koşullu erişim ilkeleri, ayarladığınız tehdit düzeyini aşan cihazların kaynaklarına erişimi engellemek için Microsoft Defender ATP 'den verileri kullanabilir. Cihazdan SharePoint veya Exchange Online gibi şirket kaynaklarına erişimi engelleyebilirsiniz.

> [!TIP]
> Koşullu erişim bir Azure Active Directory (Azure AD) teknolojisidir. Microsoft Endpoint Manager Yönetim merkezinde bulunan *koşullu erişim* düğümü, *Azure AD*'deki düğümdür.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **koşullu erişim**  >  **Yeni ilke**' yi seçin.

3. İlke için bir **Ad** girin ve **Kullanıcılar ve gruplar**’ı seçin. İlke için grupları eklemek üzere Dahil Et veya Hariç Tut seçeneklerini kullanın ve **Bitti**’yi seçin.

4. **Bulut uygulamaları**’nı ve ardından hangi uygulamaların korunacağını seçin. Örneğin **Uygulama seçin**’e tıklayın, **Office 365 SharePoint Online** ve **Office 365 Exchange Online**’ı seçin.

   Değişikliklerinizi kaydetmek için **Bitti**’yi seçin.

5. **Conditions**  >  İlkeyi uygulamalara ve tarayıcılara uygulamak için koşullar**istemci uygulamaları** ' nı seçin. Örneğin **Evet**’i seçin ve ardından **Tarayıcı** ve **Mobil uygulamalar ve masaüstü istemciler**’i etkinleştirin.

   Değişikliklerinizi kaydetmek için **Bitti**’yi seçin.

6. Cihaz uyumluluğuna göre koşullu erişim uygulamak için **Izin ver** ' i seçin. Örneğin, **erişim ver**  >  **cihazın uyumlu olarak işaretlenmesini gerektir**' i seçin.

    Değişikliklerinizi kaydetmek için **Seçin**’e tıklayın.

7. **İlkeyi etkinleştir**’i ve **Oluştur**’u seçerek değişikliklerinizi kaydedin.

## <a name="next-steps"></a>Sonraki adımlar

- [Android 'de Microsoft Defender ATP ayarlarını yapılandırma](../protect/advanced-threat-protection-manage-android.md)
- [Risk düzeyleri için uyumluluğu izleme](../protect/advanced-threat-protection-monitor.md)

Intune belgelerinden daha fazla bilgi edinin:

- [Cihazların sorunlarını gidermek için ATPs güvenlik açığı yönetimi ile güvenlik görevlerini kullanma](atp-manage-vulnerabilities.md)
- [Cihaz uyumluluk ilkelerini kullanmaya başlama](device-compliance-get-started.md)

Microsoft Defender ATP belgelerinden daha fazla bilgi edinin:

- [Microsoft Defender ATP koşullu erişimi](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP risk panosu](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)