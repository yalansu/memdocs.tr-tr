---
title: Microsoft Intune - Azure ile uyumsuzluk iletisi ve eylemleri | Microsoft Docs
description: Uyumlu olmayan cihazlara gönderilmek üzere bir bildirim e-postası oluşturun. Cihaz uyumlu değil olarak işaretlendikten sonraki eylemleri ekleyin. Örneğin uyumluluğu sağlamak için bir yetkisiz kullanım süresi ekleyebilir veya cihaz uyumlu duruma gelene kadar erişimi engellemek için bir zamanlama oluşturabilirsiniz. Bunu yapmak için Azure'da Microsoft Intune’u kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8b8bde6b7979cfe3b936a08630e23e19fc7e5a0
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81615055"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Intune 'da uyumsuz cihazlar için eylemleri yapılandırma

Uyumluluk ilkelerinizi veya kurallarınızı karşılamayan cihazlarda **uyumsuzluk Için eylemler**ekleyebilirsiniz. Bu özellik, son kullanıcıya e-posta gönderme ve daha fazlası gibi zaman sıralı bir eylem dizisi yapılandırır.

## <a name="overview"></a>Genel Bakış

Varsayılan olarak, her uyumluluk ilkesi, sıfır gün (**0**) zamanlamasıyla **uyumsuz olarak işaretle cihaz** uyumsuzluğu için eylemi içerir. Bu varsayılan değer, Intune 'un bir cihazın uyumlu olmadığını algıladığında, Intune 'un cihazı uyumsuz olarak işaretlediği bir sonucudur. Daha sonra, Azure Active Directory (AD) [koşullu erişim](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) cihazı engelleyebilir.

**Uyumsuzluk Için eylemler** yapılandırarak, uyumlu olmayan cihazlarla ilgili ne yapacağınıza karar verme esnekliği elde edersiniz ve ne zaman yapılacağını belirleyin. Örneğin, cihazı hemen engellememeyi ve kullanıcıya uyumlu hale gelmesi için bir yetkisiz kullanım süresi vermenizi tercih edebilirsiniz.

Ayarlayabileceğiniz her bir eylem için, cihazın uyumsuz olarak işaretlenme gün sayısına göre ne zaman geçerli olacağını belirleyen bir zamanlama yapılandırabilirsiniz. Ayrıca, bir eylemin birden çok örneğini yapılandırabilirsiniz. Bir ilkede bir eylemin birden çok örneğini ayarladığınızda, cihaz uyumsuz olarak kalırsa eylem daha sonra zamanlanan saatte yeniden çalışır.

Tüm platformlar için tüm eylemler kullanılamaz.

## <a name="available-actions-for-noncompliance"></a>Uyumsuzluk için kullanılabilir eylemler

Uyumsuzluk için kullanılabilir eylemler aşağıda verilmiştir. Aksi belirtilmedikçe, her bir eylem Intune tarafından desteklenen tüm platformlar için kullanılabilir:

- **Cihazı uyumsuz olarak işaretle**: varsayılan olarak, bu eylem her uyumluluk ilkesi için ayarlanır ve cihazları hemen uyumsuz olarak işaretleyerek sıfır (**0**) gün zamanlamalarına sahiptir.

  Varsayılan zamanlamayı değiştirdiğinizde, kullanıcının sorunları düzeltebileceği veya uyumsuz olarak işaretlenmeden uyumlu hale gelebileceği bir yetkisiz kullanım süresi sağlarsınız.

- **Son kullanıcıya e-posta gönder**: Bu eylem kullanıcıya bir e-posta bildirimi gönderir.
Bu eylemi etkinleştirdiğinizde:

  - Bu eylemin gönderdiği bir *bildirim iletisi şablonu* seçin. Bu eyleme bir tane atayabilmeniz için önce [bir bildirim iletisi şablonu oluşturmanız](#create-a-notification-message-template) gerekir. Özel bildirimi oluşturduğunuzda, konuyu, ileti gövdesini özelleştirip şirket logosu, şirket adı ve ek iletişim bilgilerini de ekleyebilirsiniz.
  - Azure AD gruplarınızı bir veya daha fazla seçerek iletiyi ek alıcılara göndermek için seçin.

E-posta gönderildiğinde, Intune e-posta bildiriminde uyumsuz cihaz hakkındaki ayrıntıları içerir.

- **Uyumsuz cihazı uzaktan kilitleme**: Bu eylemi, bir cihazın uzak kilidini vermek için kullanın. Bunun ardından cihazın kilidini açmak için kullanıcıdan PIN veya parola istenir. [Uzaktan Kilitleme](../remote-actions/device-remote-lock.md) özelliğinde daha fazla bilgi bulabilirsiniz.

- **Uyumsuz cihazı devre dışı bırak**: Bu eylem tüm şirket verilerini cihazdan kaldırır ve cihazı Intune yönetiminden kaldırır. Bir cihazın yanlışlıkla silinmesini engellemek için, bu eylem en az **30** günlük zamanlamayı destekler.

  Aşağıdaki platformlar bu eylemi destekler:
  - Android
  - iOS
  - Mac OS
  - Windows 10 Mobile
  - Windows Phone 8.1 ve üzeri

  [Cihazları devre dışı bırakma](../remote-actions/devices-wipe.md#retire)hakkında daha fazla bilgi edinin.

- **Son kullanıcıya anında iletme bildirimi gönder**: cihazdaki Şirket portalı uygulama veya Intune uygulaması aracılığıyla bir cihaza uyumsuzluk hakkında anında iletme bildirimi göndermek için bu eylemi yapılandırın.

  Aşağıdaki platformlar bu eylemi destekler:
  - Android:
    - Android cihaz yöneticisi
    - Android kurumsal cihaz sahibi
    - Android kurumsal Iş profili
  - iOS/iPadOS

  Anında iletme bildirimi, cihaz Intune ile ilk kez iade ettiğinde ve uyumluluk ilkesiyle uyumlu olmadığı bulunduğunda gönderilir. Kullanıcı bildirimi seçtiğinde Şirket Portalı uygulaması veya Intune uygulaması açılır ve neden uyumsuz oldukları hakkında bilgi görüntüler. Kullanıcı daha sonra sorunu çözmek için işlem gerçekleştirebilir. Uyumsuz ile ilgili ileti ayrıntıları Intune tarafından oluşturulur ve özelleştirilemiyor.

  > [!IMPORTANT]
  > Intune, Şirket Portalı uygulaması ve Microsoft Intune uygulaması, anında iletme bildiriminin teslimini garanti edemez. Bildirimler, her birinde birkaç saatlik gecikmeden sonra gösterilebilir. Bu, kullanıcıların anında iletme bildirimlerini kapatmış olduğu zaman dahildir.
  >
  > Acil iletilerde bu bildirim yöntemine güvenmeyin.

  Eylemin her örneği tek bir bildirim gönderir. Aynı bildirimi bir ilkeden yeniden göndermek için, bu ilkede, her biri farklı bir zamanlamaya sahip eylemin ek örneklerini yapılandırın.
  
  Örneğin, ilk eylemi sıfır gün boyunca zamanlayabilir ve sonra bir eylem kümesinin ikinci bir örneğini üç güne ekleyebilirsiniz. İkinci bildirimden önceki bu gecikme, kullanıcıya sorunu çözmek için birkaç gün ve ikinci bildirimden kaçının.

  Çok sayıda yinelenen ileti içeren kullanıcıların istenmeyen harcamasını engellemek için, uyumsuzluk için bir anında iletme bildirimi içeren uyumluluk ilkelerini gözden geçirin ve kolaylaştırın ve aynı sorun için çok sık gönderilen bildirimleri ortadan kaldırmak üzere zamanlamaları gözden geçirin.

  Aşağıdakileri dikkate alın:
  - Aynı gün için bir anında iletme bildirimi kümesinin birden çok örneğini içeren tek bir ilke için, o gün için yalnızca tek bir bildirim gönderilir.

  - Birden çok uyumluluk ilkesi aynı uyumluluk koşullarını içerir ve aynı zamanlamaya sahip anında iletme bildirimi eylemini dahil ettiğinizde, aynı günde aynı cihaza birden çok bildirim gönderilir.

## <a name="before-you-begin"></a>Başlamadan önce

Cihaz Uyumluluk ilkesini yapılandırırken veya daha sonra ilkeyi düzenleyerek [uyumsuzluk için eylemler ekleyebilirsiniz](#add-actions-for-noncompliance) . İhtiyaçlarınızı karşılamak için her ilkeye ek eylemler ekleyebilirsiniz. Her uyumluluk ilkesinin, cihazları uyumsuz olarak işaretleyen, bir zamanlama sıfır güne ayarlanmış şekilde, uyumsuzluk için varsayılan eylemi otomatik olarak içerdiğine dikkat edin.

Cihaz uyumluluk ilkelerini, cihazları kurumsal kaynaklardan engellemek üzere kullanmak için Azure AD koşullu erişiminin ayarlanmış olması gerekir. Rehberlik için [Intune Ile koşullu erişim kullanmanın Azure Active Directory veya genel yollarla](conditional-access-intune-common-ways-use.md) [koşullu erişim](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) bölümüne bakın.

Bir cihaz uyumluluk ilkesi oluşturmak için platforma özgü aşağıdaki kılavuza bakın:

- [Android](compliance-policy-create-android.md)
- [Android iş profilleri](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [Mac OS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Bildirim iletisi şablonu oluşturma

Kullanıcılarınıza e-posta göndermek için bir bildirim iletisi şablonu oluşturun. Cihazın uyumsuz olması durumunda, şablona girdiğiniz ayrıntılar kullanıcılarınıza gönderilen e-postada görüntülenir.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **uyumluluk ilkeleri** > **Notifications**bildirimleri > **Oluştur bildirim oluştur**' u seçin.
3. *Temel bilgiler*altında, aşağıdaki bilgileri belirtin:

   - **Adı**
   - **Konu**
   - **İleti**

4. Ayrıca, *temel bilgiler*altında, tüm varsayılan olarak *etkinleştirilecek*olan bildirim için aşağıdaki seçenekleri yapılandırın:

   - **E-posta üst bilgisi – Şirket logosunu ekleyin**
   - **E-posta alt bilgisi – Şirket adını ekleyin**
   - **E-posta alt bilgisi – İletişim bilgilerini ekleyin**

   Şirket Portalı markasının bir parçası olarak karşıya yüklediğiniz logo, e-posta şablonları için kullanılır. Şirket Portalı markası hakkında daha fazla bilgi için bkz. [Şirket kimliği marka özelleştirme](../apps/company-portal-app.md#customizing-the-user-experience).

   ![Intune'da örnek uyumluluk bildirimi iletisi](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Devam etmek için **İleri**’yi seçin.

5. **Gözden geçir + oluştur**altında, bildirim iletisi şablonunun kullanıma hazırsa emin olmak için yapılandırmalarınızı gözden geçirin. Bildirim oluşturmayı tamamladıktan sonra **Oluştur** ' u seçin.

> [!NOTE]
> Ayrıca, daha önce oluşturduğunuz mevcut bir bildirim şablonunu seçebilir ve şablonu güncelleştirmek için bilgilerini **düzenleyebilirsiniz** .

## <a name="add-actions-for-noncompliance"></a>Uyumsuzluğa yönelik eylemler ekleme

Cihaz uyumluluğu ilkesi oluşturduğunuzda, Intune uyumsuzluk için otomatik olarak bir eylem oluşturur. Bir cihaz uyumluluk ilkenizi karşımıyorsa, bu eylem cihazı uyumlu değil olarak işaretler. Cihazın ne kadar süreyle uyumsuz olarak işaretleneceğini ayarlayabilirsiniz. Bu eylem kaldırılamaz.

Bir uyumluluk ilkesi oluşturduğunuzda veya mevcut bir ilkeyi güncelleştirdiğinizde isteğe bağlı eylemler ekleyebilirsiniz.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz** > **uyumluluk ilkeleri** > **ilkeleri**' ni seçin, ilkelerinizin birini seçin ve ardından **Özellikler**' i seçin.

   Henüz bir ilkeniz yok mu? [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) veya başka bir platform ilkesi oluşturun.

   > [!NOTE]
   > JAMF cihazlar ve cihaz grupları tarafından hedeflenen cihazlar, şu anda uyumluluk eylemleri alamaz.

3. **Uyumsuzluk** > **Ekle**için Eylemler ' i seçin.

4. İstediğiniz **Eylem**’i seçin:

   - **Son kullanıcıya e-posta gönder**: Cihaz uyumsuz olduğunda kullanıcıya e-posta göndermek için bunu seçin. Ayrıca:
     - Daha önce oluşturduğunuz **İleti şablonunu** seçin
     - Grupları seçerek **Ek alıcılar** girin

   - **Uyumsuz cihazları uzaktan kilitle**: Cihaz uyumsuz olduğunda cihazı kilitleyin. Bu eylem, kullanıcının cihazın kilidini açmak için bir PIN veya geçiş kodu girmesini zorlar.

   - **Uyumsuz cihazı devre dışı bırak**: cihaz uyumsuzsa, cihazdaki tüm şirket verilerini kaldırın ve cihazı Intune yönetiminden kaldırın. Bir cihazın yanlışlıkla silinmesini engellemek için, bu eylem en az **30** günlük zamanlamayı destekler.

   - **Son kullanıcıya anında iletme bildirimi gönder**: cihazdaki Şirket portalı uygulama veya Intune uygulaması aracılığıyla bir cihaza uyumsuzluk hakkında anında iletme bildirimi göndermek için bu eylemi yapılandırın.

5. **Zamanlama**yapılandırma: kullanıcıların cihazlarında eylemi tetiklemek için uyumsuzluktan sonra geçen gün sayısını (0-365) girin. (*Uyumsuz cihazı devre dışı bırakma* en az 30 gün destekler.) Bu yetkisiz kullanım süresinden sonra [koşullu erişim](conditional-access-intune-common-ways-use.md) ilkesini zorunlu kılabilirsiniz. **0** (sıfır) gün sayısı girerseniz, koşullu erişim **hemen**yürürlüğe girer. Örneğin, bir cihaz uyumsuzsa, e-posta, SharePoint ve diğer kuruluş kaynaklarına erişimi doğrudan engellemek için koşullu erişimi kullanın.

   Bir uyumluluk ilkesi oluşturduğunuzda, **cihaz uyumsuz olarak işaretle** eylemi otomatik olarak oluşturulur ve otomatik olarak **0** güne ayarlanır (hemen). Bu eylemle cihaz iade edildiğinde cihaz hemen uyumlu değil olarak değerlendirilir. Koşullu erişim de kullanılıyorsa, koşullu erişim hemen açılır. Yetkisiz kullanım süresine izin vermek istiyorsanız, **cihazı uyumsuz olarak işaretle** eyleminde **zamanlamayı** değiştirin.

   Uyumluluk ilkenizde, örneğin, kullanıcıya bildirme de isteyebilirsiniz. **Son kullanıcıya e-posta gönder** eylemini ekleyebilirsiniz. Bu **e-posta gönder** eyleminde **zamanlamayı** iki güne ayarlarsınız. Cihaz veya son kullanıcı hala ikinci gün uyumlu değil olarak değerlendiriliyorsa, e-postanız ikinci gün gönderilir. Uyumsuzluğu 5. günde bir kez daha e-postayla gönderin ve sonra başka bir eylem ekleyin ve **zamanlamayı** beş güne ayarlayın.

  Uyumluluk ve yerleşik eylemler hakkında daha fazla bilgi için bkz. [uyumluluğa genel bakış](device-compliance-get-started.md).

6. İşiniz bittiğinde, değişikliklerinizi kaydetmek için**Tamam** **Ekle** > ' yi seçin.

## <a name="next-steps"></a>Sonraki adımlar

[İlkelerinizi izleme](compliance-policy-monitor.md).
