---
title: Mobil cihaz yönetimi yetkilisini ayarlayın
titleSuffix: Microsoft Intune
description: Intune’da mobil cihaz yönetimi yetkilisini ayarlayın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 676e7a4db54558eaea87ad2fa8efbe8af546f035
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996580"
---
# <a name="set-the-mobile-device-management-authority"></a>Mobil cihaz yönetimi yetkilisini ayarlayın

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Mobil cihaz yönetimi (MDM) yetkili ayarı, cihazlarınızı yönetme şeklinizi belirler. Kullanıcıların yönetilmek üzere cihaz kaydedebilmeleri için, BT yöneticisi olarak bir MDM yetkilisi ayarlamanız gerekir.

Olası yapılandırmalar şunlardır:

- **Intune Tek Başına** - Azure Portal’ı kullanarak yapılandırdığınız yalnızca bulut yönetimi. Intune’un sunduğu özelliklerin tamamını içerir. [MDM yetkilisini Intune konsolundan ayarlama](#set-mdm-authority-to-intune).

- **Intune ortak yönetim** -Intune bulut çözümünün Windows 10 cihazları için Configuration Manager ile tümleştirilmesi. Configuration Manager konsolunu kullanarak Intune’u siz yapılandırırsınız. [Cihazların otomatik kaydını Intune 'A yapılandırın](/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune). 

- **Microsoft 365 Için temel taşınabilirlik ve güvenlik** -bu yapılandırmayı ETKINLEŞTIRDIYSENIZ, MDM yetkilisi ' ni "Office 365" olarak ayarlanmış olacak şekilde görürsünüz. Intune 'u kullanmaya başlamak istiyorsanız, Intune lisansı satın almanız gerekir.

- **Microsoft 365 birlikte [bulunma](#coexistence) için temel taşınabilirlik ve güvenlik** -zaten temel hareketlilik ve güvenlik Microsoft 365 kullanıyorsanız ve yönetim yetkilisini her BIR kullanıcı için, MDM 'ye kayıtlı cihazları yönetmek için hangi hizmetin kullanılacağını dikte etmek üzere Intune veya temel taşınabilirlik ve güvenlik için Microsoft 365 olarak ayarlarsanız, kiracınıza Intune ekleyebilirsiniz. Her bir kullanıcının yönetim yetkilisi, kullanıcıya atanan lisansa göre tanımlanır: kullanıcının yalnızca bir Microsoft 365 temel veya standart lisansı varsa, cihazları Microsoft 365 için temel taşınabilirlik ve güvenlik tarafından yönetilecektir. Kullanıcının bir lisans entitling Intune 'u varsa, cihazları Intune tarafından yönetilir. Microsoft 365 için temel taşınabilirlik ve güvenlik tarafından daha önce yönetilen bir kullanıcıya Intune entitling bir lisans eklerseniz, cihazları Intune yönetimine geçiş yapılır. Kullanıcılara Intune 'a geçmeden önce Microsoft 365 için temel hareketliliği ve güvenliği değiştirmek üzere Intune yapılandırmalarına sahip olduğunuzdan emin olun, aksi halde, cihazları Microsoft 365 yapılandırma için temel taşınabilirlik ve güvenliği kaybeder ve Intune 'dan herhangi bir değişiklik almaz.

## <a name="set-mdm-authority-to-intune"></a>MDM yetkilisini Intune olarak ayarlama

1911 hizmet sürümünü ve daha yenisini kullanan kiracılar için MDM yetkilisi otomatik olarak Intune olarak ayarlanır.

Önceden 1911 hizmet sürümü kiracılar için MDM yetkilisini henüz ayarlamadıysanız aşağıdaki adımları izleyin.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde, **mobil cihaz yönetim yetkilisi** ayarını açmak için turuncu başlık ' ı seçin. Turuncu başlık, ancak henüz MDM yetkilisini ayarlamadıysanız görüntülenir.
2. **Mobil Cihaz Yönetimi Yetkilisi** altında, aşağıdakilerden birini MDM yetkiliniz olarak belirtin:
  - **Intune MDM Yetkilisi**
  - **Hiçbiri**

  ![Intune tarafından ayarlı mobil cihaz yönetim yetkilisi ekranının ekran görüntüsü](./media/mdm-authority-set/set-mdm-auth.png)

  MDM yetkilinizi başarıyla Intune olarak ayarladığınızı bildiren bir ileti görüntülenir.

### <a name="workflow-of-intune-administration-ui"></a>Intune Yönetim UI’si iş akışı
Android veya Apple cihaz yönetimi etkinleştirildiğinde Intune, ilgili cihazları yönetmek üzere bu üçüncü taraf hizmetleriyle tümleştirmek için cihaz ve kullanıcı bilgilerini gönderir.

Veri pencerelerini paylaşma onayı ekleyen senaryolar şu durumlarda eklenir:
- Android iş profillerini etkinleştirdiğinizde.
- Apple MDM anında iletme sertifikalarını etkinleştirdiğinizde ve karşıya yüklediğinizde.
- Aygıt Kayıt Programı, School Manager ve Volume Purchasing Program gibi Apple hizmetlerinden herhangi birini etkinleştirdiğinizde.

Bu durumların tamamında onay kesinlikle bir mobil cihaz yönetimi hizmetinin çalışmasıyla ilgilidir. Örneğin bir BT yöneticisinin Google veya Apple cihazların kaydını yetkilendirmesini onaylamak gibi. Yeni iş akışları yayınlandığında hangi bilgilerin paylaşıldığına ilişkin belgeler şu konumlarda bulunabilir:
- [Intune’un Google’a gönderdiği veriler](https://aka.ms/Data-intune-sends-to-google)
- [Intune’un Apple’a gönderdiği veriler](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Dikkat Edilmesi Gereken Önemli Noktalar
Yeni MDM yetkilisine geçtikten sonra cihazın iade edilmesi ve hizmetle eşitlenmesi için bir geçiş süresi (sekiz saate kadar) olması olasıdır. Kayıtlı cihazların değişiklikten sonra yönetilmeye ve korumaya devam edecağına emin olmak için yeni MDM yetkilisinde ayarları yapılandırmanız gerekir. 
- Yeni MDM yetkilisinden (tek başına Intune) gelen ayarların cihazdaki mevcut ayarların yerini alması için değişiklik sonrasında cihazların hizmete bağlanması gerekir.
- MDM yetkilisini değiştirdikten sonra önceki MDM yetkilisinden bazı temel ayarlar (örneğin, profiller) en fazla yedi güne kadar veya cihaz hizmete ilk kez bağlanana kadar cihazda kalır. Yeni MDM yetkilisindeki uygulama ve ayarları (ilkeler, profiller ve uygulamalar gibi) mümkün olan en kısa sürede yapılandırmanız ve ayarı, kayıtlı cihazları olan kullanıcıları içeren Kullanıcı gruplarına dağıtmanız önerilir. MDM yetkilisindeki değişiklikten sonra cihaz hizmete ilk bağlandığı zaman, yeni MDM yetkilisinden yeni ayarları alacaktır, böylece yönetim ve korumada boşluk oluşması önlenecektir.
- İlişkili kullanıcıları olmayan cihazlar (genellikle iOS/ıpados Aygıt Kayıt Programı veya toplu kayıt senaryolarında) yeni MDM yetkilisine geçirilmez. Bu cihazları yeni MDM yetkilisine taşımak için destek ile iletişime geçip yardım almanız gerekir.

## <a name="coexistence"></a>Birlikte

Birlikte bulunma özelliğinin etkinleştirilmesi, Intune 'U yeni bir kullanıcı kümesi için kullanmanızı sağlarken mevcut kullanıcılar için temel hareketliliği ve güvenliği kullanmaya devam etmenizi sağlar. Kullanıcı aracılığıyla hangi cihazların Intune tarafından yönetildiğini kontrol edersiniz. Bir kullanıcıya bir Intune lisansı atanırsa veya Configuration Manager ile Intune ortak yönetimi kullanılıyorsa, tüm kayıtlı cihazları Intune tarafından yönetilir. Aksi takdirde, Kullanıcı temel taşınabilirlik ve güvenlik tarafından yönetilir.

Birlikte bulunmasını olanaklı kılmak için üç önemli adım vardır:
1. Hazırlık
2. Intune MDM yetkilisi ekleme
3. Kullanıcı ve cihaz geçişi (isteğe bağlı).

### <a name="preparation"></a>Hazırlık

Temel taşınabilirlik ve güvenlikle birlikte bulundurmadan önce aşağıdaki noktaları göz önünde bulundurun:
- Intune ile yönetmek istediğiniz kullanıcılar için yeterli [Intune lisansına](licenses.md) sahip olduğunuzdan emin olun.
- Hangi kullanıcılara Intune lisansı atandığını gözden geçirin. Birlikte bulunmasını etkinleştirdikten sonra, Intune lisansı atanmış olan tüm kullanıcılar cihazlarını Intune 'a geçiş yapar. Beklenmedik cihaz anahtarlarından kaçınmak için, birlikte bulunmasını etkinleştirene kadar herhangi bir Intune lisansı atamamız önerilir.
- Başlangıçta Office 365 güvenlik & uyumluluk portalı aracılığıyla dağıtılan cihaz güvenlik ilkelerinin yerini almak için Intune ilkeleri oluşturun ve dağıtın. Bu değişiklik, temel taşınabilirlik ve güvenlik 'ten Intune 'a taşımayı düşündüğünüz tüm kullanıcılar için yapılmalıdır. Bu kullanıcılara atanmış Intune ilkesi yoksa, birlikte bulunma özelliğinin etkinleştirilmesi, temel taşınabilirlik ve güvenlik ayarlarını kaybetmesine neden olabilir. Bu ayarlar, yönetilen e-posta profilleri gibi değişiklik yapılmadan kaybolacaktır. Cihaz güvenlik ilkelerini Intune ilkeleriyle değiştirirken bile, cihaz Intune yönetimine taşındıktan sonra kullanıcıların e-posta profillerinin kimliklerini yeniden doğrulaması istenebilir.

### <a name="add-intune-mdm-authority"></a>Intune MDM yetkilisi ekleme

Birlikte bulunma özelliğini etkinleştirmek için, Intune 'U ortamınız için MDM yetkilisi olarak eklemeniz gerekir:

1. Azure AD Genel veya Intune Hizmet Yöneticisi haklarıyla endpoint.microsoft.com 'de oturum açın.
2. **Cihazlar**' a gidin.
3. **MDM yetkilisi Ekle dikey** penceresi görüntülenir.
4. MDM yetkilisini *Office 365* ' den *Intune* 'a geçirmek ve birlikte bulunmasını sağlamak için, **Intune MDM yetkilisi**  >  **Ekle**' yi seçin.
  ![MDM yetkilisi ekleme ekranının ekran görüntüsü](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>Kullanıcıları ve cihazları geçirme (isteğe bağlı)

Intune MDM yetkilisi etkinleştirildikten sonra, birlikte bulunma etkinleştirilir ve kullanıcıları Intune ile yönetmeye başlayabilirsiniz. İsteğe bağlı olarak, temel taşınabilirlik ve güvenlik tarafından daha önce yönetilen cihazları Intune tarafından yönetilmek üzere taşımak istiyorsanız, bu kullanıcılara bir Intune lisansı atayın. Kullanıcıların cihazları, bir sonraki MDM iadelerinde Intune 'a geçiş yapar. Temel taşınabilirlik ve güvenlik aracılığıyla bu cihazlara uygulanan ayarlar artık uygulanmayacaktır ve cihazlardan kaldırılacak.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>MDM sertifikası süre sonunda mobil cihazı temizleme

Mobil cihazlar Intune hizmetiyle iletişim kurduğunda MDM sertifikası otomatik olarak yenilenir. Mobil cihazlar silinir veya belirli bir süre boyunca Intune hizmetiyle iletişim kuramazlar, MDM sertifikası yenilenmez. MDM sertifikasının süre sonundan 180 gün sonra, cihaz Azure Portal’dan kaldırılır.

## <a name="remove-mdm-authority"></a>MDM yetkilisini kaldırma

MDM yetkilisi tekrar Bilinmeyen olarak değiştirilemez. MDM yetkilisi, hizmet tarafından hangi Portal kayıtlı cihazların (Microsoft 365 için Microsoft Intune veya temel taşınabilirlik ve güvenlik için) rapor olduğunu tespit etmek üzere kullanılır.

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>MDM yetkilisini değiştirdikten sonra ne olur

- Intune hizmeti bir kiracının MDM yetkilisinin değiştiğini algıladığında, hizmetine giriş yapmak ve hizmeti eşitlenmek üzere tüm kayıtlı cihazlara bir bildirim iletisi gönderir (Bu bildirim düzenli olarak zamanlanan iadinin dışında). Bu nedenle, kiracının MDM yetkilisi tek başına Intune 'dan değiştirildikten sonra, açık ve çevrimiçi olan cihazlar hizmete bağlanır, yeni MDM yetkilisini alır ve yeni MDM yetkilisi tarafından yönetilir. Bu cihazların yönetimi ve korumasına kesinti yoktur.
- MDM yetkilisindeki değişiklik sırasında (veya hemen sonrasında) açık ve çevrimiçi olan cihazlarda bile, cihazlar yeni MDM yetkilisi altında hizmete kaydolmadan önce sekiz saate kadar (bir sonraki zamanlanmış düzenli iadenin zamanına bağlı olarak) bir gecikme olur.  

 > [!IMPORTANT]  
 > MDM yetkilisini değiştirdiğiniz saat arasında ve yenilenen APNs sertifikası yeni yetkiliye yüklendiğinde, iOS/ıpados cihazları için yeni cihaz kayıtları ve cihaz denetimi başarısız olur. Bu nedenle MDM yetkilisindeki değişiklikten hemen sonra APNs sertifikasını gözden geçirmeniz ve yeni yetkiliye yüklemeniz önemlidir.

- Kullanıcılar, el ile cihazdan hizmete iadeyi başlatarak hızlıca yeni MDM yetkilisine geçebilir. Kullanıcılar Şirket Portalı uygulamasını kullanarak ve bir cihaz uyumluluk denetimi başlatarak bu değişikliği kolayca yapabilir.
- Cihazların, MDM yetkilisindeki değişiklikten sonra iade ettikten ve hizmetle eşitlendikten sonra düzgün çalıştığını doğrulamak için, yeni MDM yetkilisindeki cihazları arayın.
- MDM yetkilisindeki değişiklik sırasında bir cihaz çevrimdışı olduğunda ve bu cihaz hizmeti iade ettiğinde bir ara zaman vardır. Bu ara dönemde cihazın korunduğundan ve işlevsel olduğundan emin olmak için aşağıdaki profiller yedi güne kadar (veya cihaz yeni MDM yetkilisine bağlanıp mevcut ayarları yenileriyle değiştirene kadar) cihazda kalır:
   - E-posta profili
   - VPN profili
   - Sertifika profili
   - Wi-Fi profili
   - Yapılandırma profilleri
- Yeni MDM yetkilisine geçtikten sonra, Microsoft Intune yönetim konsolunda doğru uyumluluk verilerinin gösterilmesi bir haftayı bulabilir. Ancak Azure Active Directory’deki ve cihazdaki uyumluluk durumları doğru olacaktır, böylece cihaz korunmaya devam eder.
- Mevcut ayarların üzerine yazılması amaçlanan yeni ayarların, öncekilerle aynı ada sahip olduğundan emin olun. Aksi takdirde eski ayarların üzerine yazılmaz. Ve cihazlarda gereksiz profiller ve ilkeler ortaya çıkabilir.  

 > [!TIP]  
 > En iyi uygulama olarak, tüm yönetim ayarları ve yapılandırmaları ile dağıtımları, MDM yetkilisindeki değişiklik tamamlandıktan hemen sonra oluşturmalısınız. Böylece, ara dönemde cihazların korunduğundan ve etkin olarak yönetildiğinden emin olursunuz.

- MDM yetkilisini değiştirdikten sonra cihazların yeni yetkiliye başarılı bir şekilde kaydedildiğini doğrulamak için aşağıdaki adımları gerçekleştirin:  
 - Yeni cihaz kaydetme
 - Yeni kaydedilen cihazın yeni MDM yetkilisinde göründüğünden emin olun.
 - Yönetim konsolunu kullanarak cihazda Uzaktan Kilitleme gibi bir eylem gerçekleştirin. Bu eylem başarılı olursa cihaz, yeni MDM yetkilisi tarafından yönetiliyor demektir.
- Belirli cihazlarla sorun yaşıyorsanız bu cihazları kaldırıp yeniden kaydederek cihazların yeni yetkiliye bağlanması ve yönetilmeye devam etmesini sağlayabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

MDM yetkilisi ayarlandıktan sonra [cihazları kaydetmeye](../enrollment/device-enrollment.md) başlayabilirsiniz.