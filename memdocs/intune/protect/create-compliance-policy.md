---
title: Microsoft Intune-Azure 'da cihaz uyumluluk ilkeleri oluşturma | Microsoft Docs
description: Yetkisizkullanımsüresinde durumunu, koşullu erişim ile çalışma, atanmış bir ilke olmadan cihazları işleme ve Azure portal ile klasik portalda uyumluluk farklarını kullanarak cihaz uyumluluk ilkeleri oluşturun, durum ve önem düzeylerine genel bakış yapın Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad49651c7a9bd5b20aa7552f675f7dfe01be3b1c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820570"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Microsoft Intune’da uyumluluk ilkesi oluşturma

Intune’un kuruluşunuzun kaynaklarını korumaya yönelik kullanımında cihaz uyumluluk ilkeleri en önemli özelliklerdendir. Intune’da cihazların uyumlu olarak değerlendirilmesi için uyması gereken minimum işletim sistemi sürümü gibi kurallar ve ayarlar oluşturabilirsiniz. Cihaz uyumlu değilse, [koşullu erişim](conditional-access.md)kullanarak verilere ve kaynaklara erişimi engelleyebilirsiniz.

Ayrıca uyumsuzluğa yönelik olarak kullanıcıya bildirim gönderme gibi önlemler alabilirsiniz. Uyumluluk ilkelerinin işlevleri ve kullanım şekilleri hakkında genel bilgilere için bkz. [Cihaz uyumluluğuna başlama](device-compliance-get-started.md).

Bu makalede:

- Uyumluluk ilkesi oluşturmak için gerekli önkoşullar ve adımlar listelenmiştir.
- İlkeyi kullanıcı ve cihaz gruplarınıza atama adımları gösterilmiştir.
- İlkelerinizi "filtrelemek" için kullanabileceğiniz kapsam etiketleri gibi ek adımlar ve uyumlu olmayan cihazlarda gerçekleştirebileceğiniz işlemler anlatılmıştır.
- Cihazların ilke güncelleştirmelerini aldığı iade yenileme döngüsü süreleri listelenmiştir.

## <a name="before-you-begin"></a>Başlamadan önce

Cihaz uyumluluk ilkelerini kullanmak için aşağıdakilerden emin olun:

- Aşağıdaki abonelikleri kullanın:

  - Intune
  - Koşullu erişim kullanıyorsanız, Azure Active Directory (AD) Premium sürümü gerekir. [Azure Active Directory fiyatlandırması](https://azure.microsoft.com/pricing/details/active-directory/) sayfasında farklı sürümlerde sunulan özelliklere yer verilmiştir. Intune uyumluluğu için Azure AD gerekli değildir.

- Desteklenen bir platform kullanın:

  - Android cihaz yöneticisi
  - Android Kurumsal
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1

- Cihazları Intune'a kaydetme (uyumluluk durumunu görmek için gereklidir)

- Cihazları bir kullanıcıya kaydedin veya birincil kullanıcı olmadan kaydedin. Cihazların birden çok kullanıcıya kaydedilmesi desteklenmez.

## <a name="create-the-policy"></a>İlkeyi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **uyumluluk ilkeleri**  >  **ilkeleri**  >  **ilke oluştur**' u seçin.

3. Aşağıdaki seçeneklerden Bu ilke için bir **Platform** seçin:
   - *Android cihaz yöneticisi*
   - *Android Kurumsal*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows 8.1 ve üzeri*
   - *Windows 10 ve üzeri*

    *Android Enterprise*Için bir **ilke türü**de seçersiniz:
     - *Android tam olarak yönetilen, adanmış ve şirkete ait iş profili ilkesi*
     - *Android iş profili uyumluluk ilkesi*

    Ardından, **Oluştur** ' u seçerek **ilke yapılandırma oluştur** penceresini açın.

4. **Temel bilgiler** sekmesinde, daha sonra tanımanıza yardımcı olacak bir **ad** belirtin. Örneğin, iyi bir ilke adı **iOS/ıpados jailbreak uygulanmış cihazlarını uyumlu değil olarak işaretler**.

   Bir **Açıklama**belirtmeyi de tercih edebilirsiniz.
  
5. **Uyumluluk ayarları** sekmesinde, kullanılabilir Kategoriler ' i genişletin ve ilkenizin ayarlarını yapılandırın.  Aşağıdaki makaleler her platformun ayarlarını anlatmaktadır:
   - [Android cihaz yöneticisi](compliance-policy-create-android.md)
   - [Android Kurumsal](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows 8.1 ve üzeri](compliance-policy-create-windows-8-1.md)
   - [Windows 10 ve üzeri](compliance-policy-create-windows.md)  

6. **Konumlar** sekmesinde, cihazın konumuna göre uyumluluğu zorlayabilirsiniz. Mevcut konumlar arasından seçim yapın. Henüz kullanılabilir bir konumunuz yoksa, kılavuz için bkz. [konumları (ağ dilimini) kullanma](use-network-locations.md) .
   > [!TIP]
   > **Konumlar** yalnızca *Android Cihaz Yöneticisi* platformu için kullanılabilir.

7. **Uyumsuzluk eylemleri** sekmesinde, bu uyumluluk ilkesini karşılamayan cihazlara otomatik olarak uygulanacak bir eylem sırası belirtin.

   Bazı eylemler için birden çok eylem ekleyebilir ve zamanlamalar ve ek ayrıntılar yapılandırabilirsiniz. Örneğin, varsayılan eylem *işareti cihazının* bir gün sonra gerçekleşmeyecek şekilde zamanlamasını değiştirebilirsiniz. Daha sonra, cihaz bu durumu uyarmak üzere uyumlu olmadığında kullanıcıya e-posta göndermek için bir eylem ekleyebilirsiniz. Ayrıca uyumsuz kalan cihazları kilitleyen veya devre dışı bırakabilen eylemler ekleyebilirsiniz.

   Yapılandırabileceğiniz eylemler hakkında daha fazla bilgi için, bkz. kullanıcılarınıza göndermek için bildirim e-postaları oluşturma da dahil olmak üzere, [uyumlu olmayan cihazlar için eylem ekleme](actions-for-noncompliance.md).

   Başka bir örnek, bir Uyumluluk ilkesine en az bir konum eklediğiniz konumların kullanımını içerir. Bu durumda, en az bir konum seçtiğinizde uyumsuzluk için varsayılan eylem geçerlidir. Cihaz seçilen konumlardan herhangi birine bağlı değilse, uyumlu değil olarak kabul edilir. Kullanıcılarınıza bir gün gibi yetkisiz kullanım süresi vermek için zamanlamayı yapılandırabilirsiniz.

8. **Kapsam etiketleri** sekmesinde, ilkelerin veya gibi belirli gruplara filtre uygulamak için Etiketler ' i seçin `US-NC IT Team` `JohnGlenn_ITDepartment` . Uyumluluk ilkelerinize ayar ekledikten sonra bir kapsam etiketi de ekleyebilirsiniz. 

   Kapsam etiketlerini kullanma hakkında bilgi için bkz. [ilkeleri filtrelemek için kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

9. **Atamalar** sekmesinde, ilkeyi gruplarınızı atayın.  

   **Dahil edilecek + Select grupları** ' nı seçin ve ardından ilkeyi bir veya daha fazla gruba atayın. İlkeyi bir sonraki adımdan sonra kaydettiğinizde, ilke bu gruplar için de geçerlidir. 

10. **Gözden geçir + oluştur** sekmesinde ayarları gözden geçirin ve Uyumluluk ilkesini kaydetmeye hazırsanız **Oluştur** ' u seçin.  

    İlkenize göre hedeflenen kullanıcı veya cihazlar, Intune ile iade edildiğinde uyumluluk için değerlendirilir.

## <a name="refresh-cycle-times"></a>Yenileme döngü süreleri

Intune, uyumluluk ilkelerine yönelik güncelleştirmeleri denetlemek için farklı yenileme döngüleri kullanır. Cihaz yakın zamanda kaydedildiyse, iade etme daha sık çalışır. [İlke ve profil yenileme döngüleri](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) tahmini yenileme zamanlarını listeler.

Herhangi bir zamanda, kullanıcılar Şirket Portalı uygulamayı açabilir ve cihaz güncelleştirmelerini anında denetlemek için cihazı eşitleyebilir.

### <a name="assign-an-ingraceperiod-status"></a>InGracePeriod durumu atama

InGracePeriod durumu, uyumluluk ilkesi için bir değerdir. Bu değer, bir cihazın yetkisiz kullanım süresinin ve bu uyumluluk ilkesi için bir cihazın gerçek durumunun birleşimiyle belirlenir.

Yani bir cihazın atanmış bir uyumluluk ilkesi için Uyumsuz durumu varsa ve:

- Cihaza atanmış bir yetkisiz kullanım süresi yoksa, uyumluluk ilkesi için atanan değer uyumsuz
- Cihazda süresi geçen bir yetkisiz kullanım süresi varsa, uyumluluk ilkesi için atanan değer uyumsuz olur
- Cihazda daha sonra bir yetkisiz kullanım süresi varsa, uyumluluk ilkesi için atanan değer Yetkisizkullanımsüresinde olur

Aşağıdaki tabloda bu noktalar özetlenmektedir:

|Asıl uyumluluk durumu|Atanmış yetkisiz kullanım süresi değeri|Geçerli uyumluluk durumu|
|---------|---------|---------|
|NonCompliant |Bir yetkisiz kullanım süresi atanmamış |NonCompliant |
|NonCompliant |Dünün tarihi|NonCompliant|
|NonCompliant |Yarının tarihi|InGracePeriod|

Cihaz uyumluluk ilkelerini izleme hakkında daha fazla bilgi için bkz. [Intune Cihaz uyumluluk ilkelerini izleme](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Tek bir uyumluluk ilkesi durumu atama

Bir cihazda birden fazla uyumluluk ilkesi varsa ve cihazın bu atanmış uyumluluk ilkelerinden iki veya daha fazlası için farklı uyumluluk durumları varsa, cihaza tek bir uyumluluk durumu atanır. Bu atama, uyumluluk durumlarına atanan kavramsal önem derecesi düzeyine dayalı olarak yapılır. Uyumluluk durumlarının önem derecesi aşağıdaki gibidir:

|Durum  |Önem Derecesi  |
|---------|---------|
|Bilinmiyor     |1|
|NotApplicable     |2|
|Uyumlu|3|
|InGracePeriod|4|
|NonCompliant|5|
|Hata|6|

Bir cihazda birden fazla uyumluluk ilkesi varsa, bu ilkelerden en yüksek önem derecesine sahip olanı bu cihaza atanır.

Örneğin bir cihaza üç uyumluluk ilkesi atandığını düşünelim: biri Bilinmiyor durumunda (önem derecesi = 1), biri Uyumlu durumunda (önem derecesi = 3) ve biri InGracePeriod durumunda (önem derecesi = 4). InGracePeriod durumu en yüksek önem düzeyine sahiptir. Bu nedenle üç ilke de InGracePeriod uyumluluk durumuna sahip olur.

## <a name="next-steps"></a>Sonraki adımlar

[İlkelerinizi izleme](compliance-policy-monitor.md).
