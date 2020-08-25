---
title: Windows cihazınızı el ile eşitleme | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820689"
---
# <a name="sync-your-windows-device-manually"></a>Windows cihazınızı el ile eşitleme

Uygulama yükleme hızı ideal olduğunda, el ile bir cihaz eşitlemesi başlatın. El ile eşitlemeler, cihazınızı en son güncelleştirmeler ve iletişimler için Intune 'a bağlanmaya zorlar. Cihaz eşitlemesi tamamlandıktan sonra yükleme hızı artabilir.

Intune; Şirket Portalı uygulamasından, masaüstü görev çubuğu ve Başlat menüsünden ve cihazın Ayarlar uygulamasından el ile eşitlemeyi destekler. Şirket Portalı uygulaması işlevselliği, Creator’s Update (1703) ve üzerini çalıştıran Windows 10 cihazlarda desteklenir. 

Aşağıdakiler dahil olmak üzere tüm Windows cihazlar, cihazın Ayarlar uygulamasından eşitlenebilir:

* [Windows 10 Masaüstü](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Windows için Şirket Portalı uygulamasından doğrudan eşitleme
Oluşturan güncelleştirme (sürüm 1709) veya sonraki sürümü çalıştıran Windows 10 cihazlarını el ile eşitlemek için bu adımları uygulayın.

1. Cihazınızda Şirket Portalı uygulamasını açın.

2. **Ayarları**  >  **eşitleme**' yi seçin.

    ![Şirket Portalı uygulamasının Ayarlar bölümünün vurgulandığı giriş sayfasının ekran görüntüsü](./media/RS1_homePage_settings_04.png)  
    
    ![Şirket Portalı uygulamasının Eşitle düğmesinin vurgulandığı ayarlar sayfasının ekran görüntüsü](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Cihaz görev çubuğundan veya Başlat menüsünden eşitleme   

Eşitleme denetimine uygulama dışında, cihazınızın masaüstünden de erişebilirsiniz. Uygulamayı doğrudan görev çubuğunuza veya Başlat menünüze sabitlediyseniz ve hızla eşitleme yapmak istiyorsanız bu yol kullanışlı olacaktır.  

1. Görev çubuğunuzda veya Başlat menünüzde Şirket Portalı uygulaması simgesini bulun.  
2. Uygulama simgesine sağ tıklayın, böylece uygulamanın menüsü (atlama listesi olarak da bilinir) açılır.  

    ![Bir cihazın masaüstünde Windows görev çubuğunun ekran görüntüsü. Şirket Portalı App Icon seçildi ve "görev çubuğuna sabitle," "pencereyi kapat" ve "Bu cihazı Eşitle" eylemini içeren bir menü gösteriliyor.](./media/sync-device-from-start-menu-1807.png)  

3. **Bu cihazı eşitle**’yi seçin. Şirket Portalı uygulaması, **Ayarlar** sayfasında açılır ve eşitlemenizi başlatır.  

## <a name="sync-from-settings-app"></a>Ayarlar Uygulamasından eşitleme 
Microsoft HoloLens ve Windows 10 Masaüstü cihazlarınızı ayarlar uygulamasıyla el ile eşitlemek için bu adımları uygulayın.  

### <a name="windows-10-desktop"></a>Windows 10 masaüstü
1. Cihazınızda ayarları **Başlat**' ı seçin  >  **Settings**.

2. **Hesaplar**’ı seçin.

    ![Ayarlar sayfasında Hesapları seçme](./media/win10pc-sync-2-settings-accounts.png)  

3. Masaüstü cihazlar için Windows 10’un birden çok sürümü vardır. Hangi adımlar dizisini takip etmeniz gerektiğini belirlemek için ekranınızı aşağıdaki ekran görüntüleriyle karşılaştırın. 

    * Ekranınızda **İş veya okula erişme** yazıyorsa [İş veya okula erişme](#access-work-or-school-steps) adımlarına atlayın.

    ![Ayarlar uygulamasında iş veya okula erişme seçeneği](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Ekranınızda **İş erişimi** yazıyorsa [İş erişimi](#work-access-steps) adımlarına atlayın.  

    ![Hesap türü olarak iş yeri erişimini seçme](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Bu yönergeler, Windows 10 Yıldönümü Güncelleştirmesi (RS1 olarak da bilinir) çalıştıran HoloLens cihazlarda geçerlidir.  

1. Cihazınızda Ayarlar uygulamasını açın.  

2. **Hesapların**  >  **iş erişimini**seçin.  

    ![Hesaplar bağlantısının vurgulandığı HoloLens ayarlar uygulamasının ekran görüntüsü](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Bağlı hesabınızı ve ardından **Eşitle**’yi seçin.  

    ![Eşitle düğmesinin vurgulandığı HoloLens ayarlar uygulamasının ekran görüntüsü](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>İş veya okula erişme adımları  

1. **İşe veya okula erişim**' i seçin.

    ![İş veya okula erişme seçeneğini gösteren ekran görüntüsü](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Yanında evrak çantası simgesi bulunan hesabı seçin. Bu hesabı görmüyorsanız şirketiniz ayarlarınızı farklı yapılandırmış olabilir. Bunun yanında bir Microsoft logosu olan hesabı seçin.

     ![Evrak çantası veya Microsoft logosu yanındaki hesabınızın adını seçin](./media/win10pc-rs1-sync-info-button.png)

3. **Bilgi**' yi seçin. 

4. **Eşitle**’yi seçin. 

#### <a name="work-access-steps"></a>İş erişimi adımları

1. **İş erişimi**’ni seçin.

    ![Hesap türü olarak iş yeri erişimini seçme](./media/win10pc-sync-3-work-access.png)

2. **Cihaz yönetimine kaydol**’un altında şirketinizin adını seçin.

    ![Cihaz yönetimi için şirket adı seçme](./media/win10pc-sync-4-tap-com-name.png)

3. **Eşitle**' yi seçin. Eşitleme tamamlanana kadar düğme devre dışı kalır.

    ![Eşitleme düğmesini seçme](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>Sonraki adımlar  

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.
