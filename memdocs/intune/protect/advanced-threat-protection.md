---
title: Microsoft Intune-Azure 'da Microsoft Defender ATP 'yi kullanma | Microsoft Docs
description: Kurulum ve yapılandırma dahil olmak üzere Intune ile Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) kullanın, Intune cihazlarınızı ATP ile ekleme ve ardından Intune cihaz uyumluluğuyla bir cihaz ATP risk değerlendirmesi ve ağ kaynaklarını korumak için koşullu erişim ilkeleri kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: beea54b7ca244190ec0821d4ce8364369797590a
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166629"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Intune 'da koşullu erişimle Microsoft Defender ATP için uyumluluğu zorlama

Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP), Microsoft Intune Mobile Threat Defense çözümü olarak tümleştirebilirsiniz. Tümleştirme, güvenlik ihlallerinin önlenmesine ve bir kuruluşun içindeki ihlallerinin etkilerini sınırlamanıza yardımcı olabilir. Microsoft Defender ATP, Windows 10 veya üzeri çalıştıran cihazlarla ve Android cihazlarla çalışır.

Başarılı olmak için Concert 'de aşağıdaki konfigürasyonları kullanın:

- **Intune Ile Microsoft Defender ATP arasında hizmetten hizmete bağlantı kurun**. Bu bağlantı, Microsoft Defender ATP 'nin Windows 10 ' dan makine riski ve Intune ile yönettiğiniz Android cihazları hakkında veri toplamasını sağlar.
- **Microsoft Defender ATP ile cihazları eklemek için bir cihaz yapılandırma profili kullanın**. Cihazları, Microsoft Defender ATP ile iletişim kuracak şekilde yapılandırmak ve risk düzeylerini değerlendirmeye yardımcı olan verileri sağlamak için kullanabilirsiniz.
- **İzin vermek istediğiniz risk düzeyini ayarlamak için bir cihaz uyumluluk Ilkesi kullanın**. Risk düzeyleri Microsoft Defender ATP tarafından raporlanır. İzin verilen risk düzeyini aşan cihazlar uyumlu değil olarak tanımlanır.
- Kullanıcıların, uyumlu olmayan cihazlardan şirket kaynaklarına erişmesini engellemek için **koşullu erişim Ilkesi kullanın** .

Intune 'u Microsoft Defender ATP ile tümleştirdiğinizde, ATPs tehdidi & güvenlik açığı yönetimi (TVM) avantajlarından yararlanabilir ve [TVM tarafından tanımlanan uç nokta zayıflılığını düzeltmek Için Intune 'u kullanabilirsiniz](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Intune ile Microsoft Defender ATP kullanma örneği

Aşağıdaki örnek, kuruluşunuzun korunmasına yardımcı olmak için bu çözümlerin birlikte nasıl çalıştığını açıklamanıza yardımcı olur. Bu örnek için, Microsoft Defender ATP ve Intune zaten tümleşiktir.

Birisinin kuruluşunuzdaki bir kullanıcıya katıştırılmış kötü amaçlı kod içeren bir sözcük eki gönderdiği bir olay düşünün.

- Kullanıcı eki açar ve içeriği etkinleştirir.
- Yükseltilmiş bir ayrıcalık saldırısı başlar ve uzak bir makineden bir saldırganın, kurban cihazında yönetici hakları vardır.
- Daha sonra saldırgan, kullanıcının diğer cihazlarına uzaktan erişir. Bu güvenlik ihlali tüm kuruluşu etkileyebilir.

Microsoft Defender ATP, bu senaryo gibi güvenlik olaylarının çözümlenmesine yardımcı olabilir.

- Örneğimizde, Microsoft Defender ATP cihazın anormal kod yürütüldüğünü, bir işlem ayrıcalık yükseltme yükseltmesi, eklenen kötü amaçlı kod ve şüpheli bir uzak kabuk vermiş olduğunu algılar.
- Microsoft Defender ATP cihazdan bu eylemlere bağlı [olarak, cihazı yüksek riskli olarak sınıflandırır](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) ve Microsoft Defender Güvenlik Merkezi portalındaki şüpheli etkinlik hakkında ayrıntılı bir rapor içerir.

Cihazları uyumlu olmayan bir *Orta* veya *yüksek* düzeyde riske göre sınıflandırmak için bir Intune cihaz uyumluluk ilkeniz olduğundan, güvenliği aşılmış bir cihaz uyumlu değil olarak sınıflandırılmıştır. Bu sınıflandırma, koşullu erişim ilkenizin, bu cihazdan kurumsal kaynaklarınıza erişimi başlatmanıza ve erişimini engellemeye olanak tanır.

## <a name="prerequisites"></a>Önkoşullar

Microsoft Defender ATP 'yi Intune ile birlikte kullanmak için, aşağıdakilerin yapılandırıldığından ve kullanıma hazırlandığınızdan emin olun:

- Enterprise Mobility + Security E3 ve Windows E5 (veya Microsoft 365 Kurumsal E5) için lisanslı kiracı
- Microsoft Intune ortamı, [Intune ile yönetilen](../enrollment/windows-enroll.md) Windows 10 veya aynı zamanda Azure AD 'ye katılmış Android cihazları
- Microsoft [Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) ve Microsoft Defender güvenlik MERKEZI (ATP portalı) erişimi

> [!NOTE]
> Microsoft Defender ATP, iOS/ıpados ve Android Intune uygulama koruma ilkeleriyle desteklenmez.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Intune 'da Microsoft Defender ATP 'yi etkinleştirme

İlk adım, Intune ile Microsoft Defender ATP arasında hizmetten hizmete bağlantı kurmak için kullanılır. Bu, hem Microsoft Defender Güvenlik Merkezi 'ne hem de Intune 'a yönetici erişimi gerektirir.

### <a name="to-enable-defender-atp"></a>Defender ATP 'yi etkinleştirmek için

Yalnızca her kiracı için Defender ATP 'yi tek bir kez etkinleştirmeniz gerekir.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security** > **Microsoft Defender ATP**' yi seçin ve ardından **Microsoft Defender Güvenlik Merkezi 'ni aç**' ı seçin.

   ![Microsoft Defender Güvenlik Merkezi 'ni açmak için seçin](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. **Microsoft Defender Güvenlik Merkezi**'nde:
   1. **Ayarlar** > **Gelişmiş Özellikler**' i seçin.
   2. **Microsoft Intune bağlantısı** için **Açık** seçeneğini belirleyin:

      ![Intune bağlantısını etkinleştirme](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. **Tercihleri kaydet**’i seçin.

4. Microsoft Endpoint Manager Yönetim merkezinde **Microsoft Defender ATP** 'ye dönün. **MDM uyumluluk Ilkesi ayarları**altında kuruluşunuzun ihtiyaçlarına bağlı olarak:
   - **Windows cihazları 10.0.15063 ve üzeri sürümlerini Microsoft Defender ATP** 'yi **Açık** ve/veya üzerine bağla ayarı yapın
   - **6.0.0 ve üzeri sürüm Android cihazlarını açık olarak Microsoft Defender ATP 'ye bağlayın** . **On**

5. **Kaydet**’i seçin.

> [!TIP]
> Yeni bir uygulamayı Intune mobil tehdit savunması ile tümleştirdiğinizde ve Intune bağlantısını etkinleştirdiğinizde, Intune Azure Active Directory içinde klasik bir koşullu erişim ilkesi oluşturur. [Defender ATP](advanced-threat-protection.md) veya ek [MTD iş ortaklarından](mobile-threat-defense.md#mobile-threat-defense-partners)herhangi biri dahil olmak üzere tümleştirilen her MTD uygulaması yeni bir klasik koşullu erişim ilkesi oluşturur. Bu ilkeler yoksayılabilir, ancak düzenlenmemelidir, silinmemelidir veya devre dışı bırakılmalıdır.
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
> Klasik koşullu erişim ilkelerini görüntülemek için [Azure](https://portal.azure.com/#home)'da **Azure Active Directory** > **koşullu erişim** > **Klasik ilkeleri**' ne gidin.

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Yapılandırma profili kullanarak Windows cihazları ekleme 

Windows platformu için, Intune ile Microsoft Defender ATP arasında hizmet-hizmet bağlantısı kurduktan sonra, risk düzeyiyle ilgili verilerin toplanabilmesi ve kullanılabilmesi için Intune yönetilen cihazlarınızı ATP 'ye ekleyin. Cihazları eklemek için, Microsoft Defender ATP için bir cihaz yapılandırma profili kullanırsınız.

Microsoft Defender ATP bağlantısı kurduktan sonra Intune, Microsoft Defender ATP 'den bir Microsoft Defender ATP ekleme yapılandırma paketi aldı. Bu paket cihaz yapılandırma profiliyle cihazlara dağıtılır. Yapılandırma paketi, cihazları taramak, tehditleri algılamak ve riski Microsoft Defender ATP 'ye bildirmek üzere [Microsoft Defender ATP hizmetleriyle](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) iletişim kuracak şekilde yapılandırır. Yapılandırma paketini kullanarak bir cihaz ekledikten sonra, bunu tekrar yapmanız gerekmez. Ayrıca, bir [Grup İlkesi veya Microsoft uç noktası Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints)kullanarak da cihaz ekleyebilirsiniz.

### <a name="create-the-device-configuration-profile"></a>Cihaz yapılandırma profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
3. Bir **Ad** ve **Açıklama** girin.
4. **Platform**için **Windows 10 ve üzeri** ' i seçin 
5. **Profil türü**Için **Microsoft Defender ATP (Windows 10 Masaüstü)** öğesini seçin.
6. Şu ayarları yapılandırın:

   - **Microsoft Defender ATP istemci yapılandırma paketi türü**: yapılandırma paketini profile **eklemek için Ekle** ' yi seçin. Yapılandırma paketini profilden çıkarmak için **Çıkar**’ı seçin.
  
     > [!NOTE]
     > Microsoft Defender ATP ile düzgün bir şekilde bağlantı oluşturduysanız, **Intune otomatik olarak yapılandırma profilini,** **Microsoft Defender ATP istemci yapılandırma paketi türü** ayarını de kullanıma sunulacaktır.
  
   - **Tüm dosyalar Için örnek paylaşımı**: **Etkinleştir** , örneklerin toplanmasına ve Microsoft Defender ATP ile paylaşılmasına olanak tanır. Örneğin, şüpheli bir dosya görürseniz, ayrıntılı analiz için Microsoft Defender ATP 'ye gönderebilirsiniz. **Yapılandırılmadı** , MICROSOFT Defender ATP 'ye herhangi bir örnek paylaşmaz.
   - **Telemetri raporlama sıklığını**hızlandırın: yüksek riskli olan cihazlar için bu ayarı **etkinleştirin** ve bu AYARı, Microsoft Defender ATP hizmetine daha sık telemetri rapor eder.

     [Microsoft uç noktası Configuration Manager kullanarak Windows 10 makineleri](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) eklemek, bu MICROSOFT Defender ATP ayarları hakkında daha fazla bilgi içerir.

7. **Tamam**’ı ve **Oluştur**’u seçerek değişikliklerinizi kaydedin, böylece profil oluşturulur.
8. [Cihaz yapılandırma profilini,](../configuration/device-profile-assign.md) MICROSOFT Defender ATP ile değerlendirmek Istediğiniz cihazlara atayın.

## <a name="create-and-assign-the-compliance-policy"></a>Uyumluluk ilkesi oluşturma ve atama

Hem Windows hem de Android cihazlarda, uyumluluk ilkesi bir cihaz için kabul edilebilir olarak düşünmeniz gereken risk düzeyini belirler.

Uyumluluk ilkesi oluşturma konusunda bilgi sahibi değilseniz, *Microsoft Intune ' de uyumluluk ilkesi oluşturma bölümünde* [ilke oluşturma](../protect/create-compliance-policy.md#create-the-policy) yordamına başvurun. Aşağıdaki bilgiler, bir uyumluluk ilkesinin parçası olarak Defender ATP yapılandırmasına özgüdür.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz** > **uyumluluk ilkeleri** > **Policies**ilkeleri > **ilke oluştur**' u seçin.

3. **Platform** için *Windows 10 ve üzeri*, **Android Cihaz Yöneticisi**ve/veya **Android Enterprise**' u seçin. Ardından, **Oluştur** ' u seçerek **ilke yapılandırma oluştur** penceresini açın.

4. Daha sonra tanımanıza yardımcı olacak bir **ad** belirtin. Bir **Açıklama**belirtmeyi de tercih edebilirsiniz.
  
5. **Uyumluluk ayarları** sekmesinde, **Microsoft Defender ATP** grubunu genişletin ve cihazın tercih edilen düzeyinize **veya makine risk puanı altında olmasını gerektir** seçeneğini belirleyin.

   Tehdit düzeyi sınıflandırmaları, [Microsoft Defender ATP tarafından belirlenir](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Temiz**: En güvenli düzeydir. Cihazda mevcut tehditler bulunamaz ve şirket kaynaklarına erişmeye devam edin. Herhangi bir tehdit bulunursa cihaz uyumsuz olarak değerlendirilir. (Microsoft Defender ATP, *güvenli*değeri kullanır.)
   - **Düşük**: Cihaz, yalnızca düşük düzeydeki tehditler varsa uyumludur. Orta veya yüksek tehdit düzeylerine sahip cihazlar uyumlu değildir.
   - **Orta**: Cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumludur. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
   - **Yüksek**: Bu düzey en az güvenlidir ve tüm tehdit düzeylerine izin verir. Yüksek, orta veya düşük tehdit düzeylerine sahip cihazlar uyumlu kabul edilir.

6. İlkenin geçerli gruplara atanması dahil olmak üzere ilkenin yapılandırmasını doldurun.

## <a name="create-a-conditional-access-policy"></a>Koşullu erişim ilkesi oluşturma

Koşullu erişim ilkesi, uyumluluk ilkenizde ayarladığınız tehdit düzeyini aşan cihazlar için kaynaklara erişimi engeller. Cihazdan SharePoint veya Exchange Online gibi şirket kaynaklarına erişimi engelleyebilirsiniz.

> [!TIP]
> Koşullu Erişim, bir Azure Active Directory (Azure AD) teknolojisidir. Microsoft Endpoint Manager yönetim merkezinden erişilen koşullu erişim düğümü, *Azure AD*'den erişilen aynı düğümdür.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security** > **koşullu erişim** > **Yeni ilke**' yi seçin.

3. İlke için bir **Ad** girin ve **Kullanıcılar ve gruplar**’ı seçin. İlke için grupları eklemek üzere Dahil Et veya Hariç Tut seçeneklerini kullanın ve **Bitti**’yi seçin.

4. **Bulut uygulamaları**’nı ve ardından hangi uygulamaların korunacağını seçin. Örneğin **Uygulama seçin**’e tıklayın, **Office 365 SharePoint Online** ve **Office 365 Exchange Online**’ı seçin.

   Değişikliklerinizi kaydetmek için **Bitti**’yi seçin.

5. İlkeyi uygulamalara ve tarayıcılara uygulamak için **koşullar** > **istemci uygulamaları** ' nı seçin. Örneğin **Evet**’i seçin ve ardından **Tarayıcı** ve **Mobil uygulamalar ve masaüstü istemciler**’i etkinleştirin.

   Değişikliklerinizi kaydetmek için **Bitti**’yi seçin.

6. Cihaz uyumluluğuna göre koşullu erişim uygulamak için **Izin ver** ' i seçin. Örneğin, **erişim** > ver**cihazın uyumlu olarak işaretlenmesini gerektir**' i seçin.

    Değişikliklerinizi kaydetmek için **Seçin**’e tıklayın.

7. **İlkeyi etkinleştir**’i ve **Oluştur**’u seçerek değişikliklerinizi kaydedin.

## <a name="monitor-device-compliance"></a>Cihaz uyumluluğunu izleme

Ardından, Microsoft Defender ATP Uyumluluk ilkesine sahip cihazların durumunu izleyin.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazları** > seçin**ilke uyumluluğunu****izleyin** > .

3. Listede Microsoft Defender ATP ilkenizi bulun ve hangi cihazların uyumlu veya uyumsuz olduğunu görün.

Aynı konumdaki uyumsuz cihazlar için *işletimsel* raporu da kullanabilirsiniz:

1. **Uyumsuz cihazları****izlemek** > için **cihazlar** > ' ı seçin.

Raporlar hakkında daha fazla bilgi için bkz. [Intune raporları](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Ekleme durumunu görüntüle

Tüm Intune tarafından yönetilen Windows 10 cihazlarının ekleme durumunu görüntülemek için **Kiracı Yönetimi** > **Microsoft Defender ATP**'ye gidebilirsiniz. Bu sayfadan, Microsoft Defender ATP 'ye daha fazla cihaz ekleme için bir cihaz yapılandırma profili oluşturmayı da başlatabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

[Microsoft Defender ATP koşullu erişimi](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Microsoft Defender ATP risk panosu](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Cihazların sorunlarını gidermek Için ATPs güvenlik açığı yönetimi ile güvenlik görevlerini kullanın](atp-manage-vulnerabilities.md).

[Cihaz uyumluluk ilkelerini kullanmaya başlama](device-compliance-get-started.md)
