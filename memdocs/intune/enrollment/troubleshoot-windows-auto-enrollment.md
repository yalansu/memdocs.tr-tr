---
title: Intune 'da Windows 10 otomatik kaydı sorunlarını giderme
titleSuffix: Microsoft Intune
description: Otomatik kayıt sorunlarını giderme hakkında bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd84d50fb7e1ad9d67cd106d6da2b187dfd6adb4
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87528220"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Intune 'da Windows 10 Grup İlkesi tabanlı otomatik kayıt sorunlarını giderme

Active Directory (AD) etki alanına katılmış cihazlar için otomatik kaydı MDM 'ye tetikleyebilmeniz için Grup İlkesi kullanabilirsiniz. Bu özellik hakkında daha fazla bilgi için bkz. [Grup İlkesi kullanarak Windows 10 cihazını otomatik olarak kaydetme](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

## <a name="verify-the-configuration"></a>Yapılandırmayı doğrulama

Sorun gidermeye başlamadan önce, her şeyin doğru şekilde yapılandırıldığını doğrulamanız en iyisidir. Sorun doğrulama sırasında çözülenemediğinde, bazı önemli günlük dosyalarını denetleyerek sorun gidermeye devam edebilirsiniz.

1. Cihazı kaydetmeye çalışan kullanıcıya geçerli bir Intune lisansı atandığını doğrulayın.

   ![Intune lisansını doğrulama](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

2. Cihazların Intune 'A kaydolabileceği tüm kullanıcılar için otomatik kaydın etkinleştirildiğini doğrulayın. Daha fazla bilgi için bkz. [Azure AD ve Microsoft Intune: yeni portalda OTOMATIK MDM kaydı](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal).

   ![Otomatik kaydı doğrulama](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Tüm kullanıcıların Intune 'a cihaz kaydetmesine izin vermek için **MDM Kullanıcı kapsamının** **Tümü** olarak ayarlandığını doğrulayın.
   - **Mam Kullanıcı kapsamının** **none**olarak ayarlandığını doğrulayın. Aksi takdirde, bu ayar MDM kapsamına göre önceliğe sahip olur ve sorunlara yol açabilir.
   - **MDM bulma URL 'sinin** olarak ayarlandığını doğrulayın **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** .

3. Cihazın Windows 10, sürüm 1709 veya sonraki bir sürümünü çalıştırdığından emin olun.

4. Cihazların **karma Azure AD 'ye katılmış**olarak ayarlandığını doğrulayın. Bu ayar, cihazların hem etki alanına katılmış hem de Azure AD 'ye katılmış olduğu anlamına gelir.

   Ayarları doğrulamak için, komut satırında **dsregcmd/Status** komutunu çalıştırın. Sonra çıktıda aşağıdaki durum değerlerini doğrulayın:

   - Cihaz Durumu
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - SSO durumu

     ```asciidoc
     AzureAdPrt: YES
     ```

   Aynı bilgileri Azure AD 'ye katılmış cihazlar listesinde bulabilirsiniz:

   ![Azure AD 'ye katılmış cihazların listesi](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

5. Hem **Microsoft Intune**hem de    **Microsoft Intune kayıt** Azure AD dikey PENCERESINDE **Mobility (MDM ve MAM)** altında listelenebilir   . Her ikisi de varsa, **Microsoft Intune**' nin altındaki otomatik kayıt ayarlarını yapılandırmadığınızdan emin olun.

6. Aşağıdaki grup ilkesi ilkesi ayarının Intune 'a kaydedilmesi gereken tüm cihazlara başarıyla dağıtıldığını doğrulayın:

   **Bilgisayar yapılandırması**  >  **İlkeler**  >  **Yönetim Şablonları**  >  **Windows bileşenleri**  >  **MDM**  >  **Varsayılan Azure AD kimlik bilgilerini kullanarak OTOMATIK MDM kaydını etkinleştirme**

   Grup ilkesi ilkesi ayarının başarıyla dağıtıldığını doğrulamak için etki alanı yöneticilerinizle iletişime geçin.

7. Cihazın, klasik bılgısayar Aracısı kullanılarak Intune 'A kayıtlı olmadığından emin olun.
8. Azure AD ve Intune 'da aşağıdaki ayarları doğrulayın:

   **Azure AD cihaz ayarları 'nda:**

   ![Azure AD cihaz ayarları](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - **Kullanıcılar cihazları Azure AD ayarlarına katabilir** ve **Tümü**olarak ayarlanır.
   - Bir kullanıcının Azure AD 'deki cihaz sayısı, **Kullanıcı kotası başına maksimum cihaz sayısını** aşamaz.
   
   **Intune kayıt kısıtlamaları:**

   - Windows cihazlarının kaydına izin veriliyor.

     ![Windows cihazlarının izin verilen kaydı](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Sorun giderme

Sorun devam ederse, Olay Görüntüleyicisi aşağıdaki konumda bulunan MDM günlüklerini cihazda inceleyin:

**Uygulama ve hizmet günlükleri**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-kuruluş-tanılama-sağlayıcı**  >  **Yönetici**

Olay KIMLIĞI 75 ' i arayın (olay iletisi "otomatik MDM kaydı: başarılı"). Bu olay otomatik kaydın başarılı olduğunu gösterir.

Olay KIMLIĞI 75, aşağıdaki durumlarda günlüğe kaydedilmez:

- Kayıt başarısız olur.

  Bu hatayı doğrulamak için olay KIMLIĞI 76 (olay iletisi: otomatik MDM kaydı: başarısız (bilinmeyen Win32 hata kodu: 0x8018002b) bölümüne bakın. Bu olay, başarısız bir otomatik kaydı gösterir.

  Bu hatayla ilgili bir çözüm için bkz. [Microsoft Intune Windows cihaz kaydı sorunlarını giderme](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors).

- Kayıt, hiç tetiklenmedi.Bu durumda, olay KIMLIĞI 75 ve olay KIMLIĞI 76 günlüğe kaydedilmez.
  
  Otomatik kayıt işlemi, **Microsoft**Görev Zamanlayıcı ' de Microsoft Windows EnterpriseMgmt altında bulunan "**AAD 'den MDM 'ye otomatik olarak kaydolma için kayıt istemcisi tarafından oluşturulan zamanlama**" görevinin tarafından tetiklenir  >  **Windows**  >  **EnterpriseMgmt** .

  ![Kayıt tetiklenmedi](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Bu görev, **varsayılan Azure AD kimlik bilgileri kullanılarak OTOMATIK MDM kaydını etkinleştir** Grup İlkesi ilke ayarı başarıyla hedef cihaza dağıtıldığında oluşturulur. Görev, 1 gün içinde 5 dakikada bir çalışacak şekilde zamanlanır.

  Görevin başlatıldığını doğrulamak için Olay Görüntüleyicisi içinde aşağıdaki konumda bulunan Görev Zamanlayıcı olay günlüklerini kontrol edin:

  **Uygulama ve hizmet günlükleri Microsoft > Windows > Görev Zamanlayıcı > Işletimsel >**

  Görev Zamanlayıcı üzerinde tetiklendiğinde, 107 olay KIMLIĞI günlüğe kaydedilir.

  Görev tamamlandığında 102 olay KIMLIĞI günlüğe kaydedilir. Olay, otomatik kayıt işleminin başarılı olup olmadığını günlüğe kaydedilir.

  > [!NOTE]
  > Otomatik kaydın tetiklenip tetiklenmediğini denetlemek için Görev Zamanlayıcısı günlüğünü kullanabilirsiniz. Ancak, otomatik kaydın başarılı olup olmadığını anlamak için günlüğü kullanamazsınız.

  Aşağıdaki durum, kayıt istemcisi tarafından oluşturulan zamanlamanın AAD 'den MDM 'ye otomatik olarak kaydedilmesini sağlamak üzere kayıt istemcisi tarafından oluşturulmasına neden olabilir:

  - Cihaz zaten başka bir MDM çözümüne kayıtlı. Bu durumda, 7016 hata 2149056522 kodu ile birlikte olay kimliği, **uygulama ve hizmet günlükleri**  >  **Microsoft**  >  **Windows**  >  **Görev Zamanlayıcı**  >  **işletimsel** olay günlüğünü günlüğe kaydeder.

    Bu sorunu onarmak için, cihazın MDM 'den kaydını kaldırın.

  - Grup ilkesi bir sorun var. Bu durumda, aşağıdaki komutu çalıştırarak grup ilkesi ayarlarının güncelleştirilmesini zorlayın:

    **gpupdate/Force**

    Sorun devam ederse, Active Directory ek sorun giderme yapın.