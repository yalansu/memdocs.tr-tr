---
title: Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşıma
titleSuffix: Microsoft Intune
description: Android cihazlarını cihaz yöneticisinden Intune 'da iş profili yönetimine taşıyın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33e4f36afce9b8a2f296697623cd7031edf0fa74
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791776"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşıma

**Cihazların cihaz yöneticisiyle yönetilen cihazları engellemek**için uyumluluk ayarını kullanarak Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşımasına yardımcı olabilirsiniz. Bu ayar cihaz yöneticisiyle yönetiliyorsa cihazların uyumsuz olmasını sağlar. 

Kullanıcılar bu nedenle uyumsuz olduklarını görtiklerinde, **Çözümle**' ye dokunabilirler. Bunlar, bunlara göre kılavuzluk edecek bir denetim listesine alınırlar:
1. Cihaz Yöneticisi yönetiminden kaydı geri al
2. İş profili yönetimine kaydolma
3. Tüm uyumluluk sorunlarını çözme. 

## <a name="prerequisites"></a>Ön koşullar

- Kullanıcıların Android Şirket Portalı Version 5.0.4720.0 veya üzeri bir sürümü olan [Android Cihaz Yöneticisi 'ne kayıtlı cihazları](android-enroll-device-administrator.md) olmalıdır.
- [Intune kiracı Hesabınızı Android Kurumsal hesabınıza bağlayarak](connect-intune-android-enterprise.md)Android iş profili yönetimini ayarlayın.
- Android iş profiline taşınan Kullanıcı grubu için [Android kurumsal iş profili kaydını ayarlayın](android-work-profile-enroll.md) .
- Kullanıcı cihaz limitlerinizi artırmayı göz önünde bulundurun. Cihazların cihaz yöneticisi yönetiminden kaydı kaldırıldığında, cihaz kayıtları hemen kaldırılmayabilir. Bu süre boyunca Cushion sağlamak için, kullanıcıların iş profili yönetimine kaydolabilmesi için cihaz sınırı kapasitesini artırmanız gerekebilir.
  - Kullanıcı başına en fazla cihaz sayısı için [Azure Active Directory cihaz ayarlarını yapılandırın](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) .
  - Cihaz sınırını ayarlayarak [Intune cihaz sınır kısıtlamalarını](enrollment-restrictions-set.md#create-a-device-limit-restriction) ayarlayın. 

## <a name="create-device-compliance-policy"></a>Cihaz uyumluluk ilkesi oluştur

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihaz**  >  **uyumluluk ilkeleri**  >  **ilkeleri**  >  **ilke oluştur**' u seçin.

    ![İlke oluşturma](./media/android-move-device-admin-work-profile/create-policy.png)

2. **İlke oluştur** sayfasında, **platformu** **Android Cihaz Yöneticisi**  >  **Oluştur**olarak ayarlayın.
3. **Temel bilgiler** sayfasında, bir sonraki **adı** ve açıklamayı yazın **Description**  >  **Next**.

    ![Temel bilgiler sayfası](./media/android-move-device-admin-work-profile/basics.png)
    
4. **Uyumluluk ayarları** sayfasında, **cihaz durumu** bölümünde, **cihaz yöneticisiyle yönetilen blok cihazların** ileri ' ye Evet ' i belirleyin **Yes**  >  **Next**.

    ![Cihazları engelle](./media/android-move-device-admin-work-profile/block-devices.png)

5. **Konumlar** sayfasında, bir **sonraki**> isterseniz konum ekleyebilirsiniz.

6. **Uyumsuzluğa yönelik eylemler**' de, bu akış için son kullanıcı deneyimini özelleştirmek üzere [uyumsuzluk için kullanılabilir eylemleri](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) yapılandırabilirsiniz. Göz önünde bulundurulması gereken bazı eylemler vardır.

- **Cihazı uyumsuz olarak işaretle**: varsayılan olarak, bu eylem sıfır (0) güne ayarlanır ve cihazları hemen uyumsuz olarak işaretler. Bunu daha fazla güne değiştirmek, kullanıcılara henüz uyumsuz olarak işaretlenmeksizin iş profili yönetimine geçiş yapmak için akışı görebilecekleri bir yetkisiz kullanım süresi sağlar. Örneğin, bunu 14 gün olarak ayarlamak, kullanıcılara, kaynaklara erişimi kaybetme riski olmadan cihaz yöneticisinden iş profili yönetimine geçiş yapmak için iki hafta daha verebilir.
- **Son kullanıcıya anında iletme bildirimi gönder**: bunu, Cihaz Yöneticisi cihazlarına anında iletme bildirimleri gönderecek şekilde yapılandırın. Bir Kullanıcı bildirimi seçtiğinde, **cihaz ayarlarını Güncelleştir** sayfasında iş profili yönetimine geçiş yapmak için akışı başlatabilecekleri Android şirket portalı başlatılır.
- **Son kullanıcıya e-posta gönder**: bunu, cihaz yöneticisinden iş profili yönetimine taşıma hakkında kullanıcılara e-posta gönderecek şekilde yapılandırın. E-postada aşağıdaki URL 'YI ekleyebilirsiniz. Bu işlem, seçildiğinde, iş profili yönetimine geçmek üzere akışı başlatabilecekleri cihaz ayarlarını Güncelleştir sayfasında Android Şirket Portalı başlatacak.
    - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
    - ABD kamu için bu bağlantıyı şu şekilde kullanabilirsiniz: `https://portal.manage.microsoft.us/UpdateSettings.aspx` .
  
    > [!NOTE]
    > - Tabii ki, kullanıcılarla iletişiminizdeki bağlantılar için Kullanıcı dostu hiper metin kullanabilirsiniz. Ancak, bu şekilde değiştirildiyse bağlantılar çalışamadığı için URL-kısa kullanım belirteçleri kullanmayın.
    > - Android Şirket Portalı açıksa ve arka planda, Kullanıcı bağlantıya dokunduğunda bunun yerine açıldıkları son sayfaya gidebilirler.
    > - Kullanıcılar bir Android cihazında bağlantıya dokunmalıdır. Bunun yerine bir tarayıcıya yapıştırdıysanız, Android Şirket Portalı başlatılmaz. 

    **İleri**’yi seçin.

7. **Kapsam etiketleri** sayfasında, dahil etmek istediğiniz tüm kapsam etiketlerini seçin.
8. **Atamalar** sayfasında, ilkeyi Cihaz Yöneticisi yönetimi ile kaydedilmiş cihazlara sahip bir gruba **atayın >.**
9. **Gözden geçir + oluştur** sayfasında, tüm ayarlarınızı doğrulayın ve ardından **Oluştur**' u seçin.

## <a name="troubleshooting"></a>Sorun giderme

[Yeni cihaz yönetimi kurulumuna geçmek için Son Kullanıcı akışı](../user-help/move-to-new-device-management-setup.md) , kullanıcıların Cihaz Yöneticisi yönetiminden kaydını kaldırarak ve iş profili yönetimine göre kurulumunu yaparken kullanıcılara kılavuzluk eder. Kullanıcıların Android Şirket Portalı Version 5.0.4720.0 veya üzeri bir sürümü olan [Android Cihaz Yöneticisi 'ne kayıtlı cihazları](android-enroll-device-administrator.md) olmalıdır.

### <a name="user-sees-an-error-after-tapping-resolve"></a>Kullanıcı Çözümle ' ye dokunduktan sonra bir hata görür
Kullanıcılar **Çözümle** düğmesine dokunduktan sonra bir hata görüyor, bunun nedeni aşağıdakilerden biri olabilir:
- İş profili kaydı doğru ayarlanmadı (bir Android kurumsal hesabı bağlı değil veya kayıt kısıtlamaları iş profili kaydını engelleyecek şekilde ayarlanmış).
- Cihaz, iş profili kaydını desteklemeyen Android 4,4 veya daha önceki bir sürümü çalıştırıyor. 
- Cihaz üreticisi, cihaz modelinde iş profili kaydını desteklememektedir.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>Çözümle düğmesi kullanıcının cihazında görünmüyor
Kullanıcı, yukarıda açıklanan cihaz uyumluluk ilkesiyle hedeflendikten sonra cihaz yönetici yönetimine kaydederse, **Çözümle** düğmesi kullanıcının cihazında görünmez.

**Çözümle** düğmesinin görüntülenmesini sağlamak için, kullanıcının kurulumu erteleyip işlemi bildirimden yeniden başlatması gerekir.

Bu koşuldan kaçınmak için kayıt kısıtlamalarını kullanarak cihaz yöneticisi yönetimine kaydı engelleyin.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>Kullanıcı, cihaz ayarları sayfasını güncelleştirmek için URL 'ye dokunduktan sonra bir hata görüyor
Kullanıcılar, Android Şirket Portalı **cihaz ayarlarını Güncelleştir SAYFASıNDA** URL 'ye dokunduğunda tarayıcıda bir hata sayfası görebilirler. Bu hatanın nedeni aşağıdakilerden biri olabilir:
- Cihaz bir Android değil.
- Android cihazda Şirket Portalı uygulaması yok.
- Android Şirket Portalı sürümü 5.0.4720.0 'den daha eski.
- Android cihaz Android 6 veya daha önceki bir sürümünü kullanır. 

## <a name="next-steps"></a>Sonraki adımlar
[Son Kullanıcı akışına bakın](../user-help/move-to-new-device-management-setup.md) 
 [Android iş profili cihazlarını Intune Ile yönetme](android-enterprise-overview.md)
