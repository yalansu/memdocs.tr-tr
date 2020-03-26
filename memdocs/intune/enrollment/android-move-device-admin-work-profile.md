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
ms.openlocfilehash: 7126d3d3a8567a2567afc116037d67ffa1a6c8b2
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80274703"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşıma

**Cihazların cihaz yöneticisiyle yönetilen cihazları engellemek**için uyumluluk ayarını kullanarak Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşımasına yardımcı olabilirsiniz. Bu ayar cihaz yöneticisiyle yönetiliyorsa cihazların uyumsuz olmasını sağlar. 

Kullanıcılar bu nedenle uyumsuz olduklarını görtiklerinde, **Çözümle**' ye dokunabilirler. Bunlar, bunlara göre kılavuzluk edecek bir denetim listesine alınırlar:
1. Cihaz Yöneticisi yönetiminden kaydı geri al
2. İş profili yönetimine kaydolma
3. Tüm uyumluluk sorunlarını çözme. 

## <a name="prerequisites"></a>Önkoşullar

- Kullanıcıların Android Şirket Portalı Version 5.0.4720.0 veya üzeri bir sürümü olan [Android Cihaz Yöneticisi 'ne kayıtlı cihazları](android-enroll-device-administrator.md) olmalıdır.
- [Intune kiracı Hesabınızı Android Kurumsal hesabınıza bağlayarak](connect-intune-android-enterprise.md)Android iş profili yönetimini ayarlayın.
- Android iş profiline taşınan Kullanıcı grubu için [Android kurumsal iş profili kaydını ayarlayın](android-work-profile-enroll.md) .
- Kullanıcı cihaz limitlerinizi artırmayı göz önünde bulundurun. Cihazların cihaz yöneticisi yönetiminden kaydı kaldırıldığında, cihaz kayıtları hemen kaldırılmayabilir. Bu süre boyunca Cushion sağlamak için, kullanıcıların iş profili yönetimine kaydolabilmesi için cihaz sınırı kapasitesini artırmanız gerekebilir.
  - Kullanıcı başına en fazla cihaz sayısı için [Azure Active Directory cihaz ayarlarını yapılandırın](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) .
  - Cihaz sınırını ayarlayarak [Intune cihaz sınır kısıtlamalarını](enrollment-restrictions-set.md#create-a-device-limit-restriction) ayarlayın. 

## <a name="create-device-compliance-policy"></a>Cihaz uyumluluk ilkesi oluştur

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde, **cihaz** > **Uyumluluk Ilkeleri** > **ilkeler** > **ilke oluştur**' u seçin.

    ![İlke oluştur](./media/android-move-device-admin-work-profile/create-policy.png)

2. **Ilke oluştur** sayfasında, **platformu** **Android Cihaz Yöneticisi** olarak ayarlayın > **oluşturun**.
3. **Temel bilgiler** sayfasında, **ad** ve **Açıklama** > **İleri**' ye yazın.

    ![Temel bilgileri sayfası](./media/android-move-device-admin-work-profile/basics.png)
    
4. **Uyumluluk ayarları** sayfasında, **cihaz durumu** bölümünde, **cihaz yöneticisiyle yönetilen blok cihazların** **İleri**' ye > ' i **Evet** olarak ayarlayın.

    ![Cihazları engelle](./media/android-move-device-admin-work-profile/block-devices.png)

5. **Konumlar** sayfasında, bir **sonraki**> isterseniz konum ekleyebilirsiniz.
6. **Uyumsuzluğa yönelik eylemler**' de, **son kullanıcıya e-posta gönder** eylemini ayarlayabilirsiniz.

    ![E-posta gönder](./media/android-move-device-admin-work-profile/send-email.png)


    E-postada, aşağıdaki URL 'YI kullanıcılara iletilerinize ekleyebilirsiniz. URL, **cihaz ayarlarını Güncelleştir** sayfasında Android şirket portalı başlatacaktır. Bu sayfa iş profili yönetimine geçmek için akışını başlatır.
    - [https://portal.manage.microsoft.com/UpdateSettings.aspx](https://portal.manage.microsoft.com/UpdateSettings.aspx).
    - ABD kamu için bu bağlantıyı şu şekilde kullanabilirsiniz: [https://portal.manage.microsoft.us/UpdateSettings.aspx](https://portal.manage.microsoft.us/UpdateSettings.aspx).
  
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
[Intune Ile Android iş profili cihazlarını yönetme](android-enterprise-overview.md)
[Son Kullanıcı akışına bakın](../user-help/move-to-new-device-management-setup.md)
