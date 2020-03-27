---
title: Hızlı Başlangıç - Windows 10 Masaüstü cihazınızı Microsoft Intune’a kaydetme
description: Hızlı Başlangıç - Windows 10 Masaüstü cihazınızı Microsoft Intune’a kaydetmek için Şirket Portalı’nı kullanın.
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f70c8487d9cb30b2a7cced63e6e019541f73704
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327046"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>Hızlı Başlangıç: Windows 10 cihazınızı kaydetme

Bu hızlı başlangıçta önce bir Intune kullanıcısı rolünü üstlenecek ve Windows 10 cihazınızı Microsoft Intune’a kaydedeceksiniz. Ardından, Intune 'a geri dönüp cihazın kaydolduğunu onaylamanız gerekir.

Cihazlarınızı Microsoft Intune 'ye kaydetmek, Windows 10 cihazlarınızın e-posta, dosyalar ve diğer kaynaklar dahil, kuruluşunuzun güvenli verilerine erişmesini sağlar. Bu durum hem Windows 10 masaüstü hem de Windows 10 Mobile cihazlar için geçerlidir. Cihazlarınızı kaydetmeniz hem sizin hem de kuruluşunuz için güvenli erişim sağlamanıza ve iş verilerinizi kişisel verilerinizden ayırmanıza yardımcı olur.

> [!TIP]
> [Cihazınızı Intune'a kaydettiğinizde](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md) neler olacağını ve [cihazınızdaki bilgilerin](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) nasıl etkileneceğini öğrenin.

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Önkoşullar

- Microsoft Intune aboneliği - [ücretsiz deneme hesabına kaydolun](../fundamentals/free-trial-sign-up.md)
- Bu hızlı başlangıcı tamamlamak için [Intune’da otomatik kayıt kurulumu](quickstart-setup-auto-enrollment.md) adımlarını tamamlamanız gerekir.

## <a name="confirm-your-windows-10-desktop-version"></a>Windows 10 Masaüstü sürümünüzü onaylayın

Windows 10 Masaüstü cihazınızı kaydetmeden önce yüklü olan Windows sürümünü onaylamanız gerekir.

1. Windows Ayarları seçeneklerini görüntülemek için Windows’un **Başlat** simgesine sağ tıklayın ve **Ayarlar**’ı seçin.

   ![Windows Ayarları - Sistem ekran görüntüsü](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. **Sistem** > **Hakkında**’yı seçin. 

   ![Sistem ayarlarınızın ekran görüntüsü](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > Ayrıca **arama çubuğuna** “Bilgisayarınız hakkında” yazıp **Bilgisayarınız hakkında**’yı seçebilirsiniz.

3. **Ayarlar** penceresinde bilgisayarınız için bir **Windows belirtimleri** listesi göreceksiniz. Bu listede **Sürüm**'ü bulun.

4. Windows 10’un **Sürüm** bölümünün **1607 veya üzeri** olduğunu onaylayın.

    > [!IMPORTANT]
    > Bu hızlı başlangıçta sunulan adımlar Windows 10 **1607 veya üzeri** sürümler içindir, **1511 veya daha düşük** sürüme sahipseniz [şu adımları](../user-help/enroll-windows-10-device.md) izleyin.  

## <a name="enroll-windows-10-desktop"></a>Windows 10 Masaüstü’nü kaydetme

1. Windows Ayarları’na dönün ve **Hesaplar**’ı seçin.

   ![Sistem ayarları - Hesaplar ekranınızın ekran görüntüsü](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. **İş veya okula erişim** > **Bağlan**’ı seçin.

    ![İş veya okul hesabına erişimi seçme](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. İş veya okul hesabınızla Intune’da oturum açın ve daha sonra **Sonraki**’ne tıklayın. [Kullanıcı oluştur ve lisans ata](../fundamentals/quickstart-create-user.md) hızlı başlangıç ' yı izlediyseniz, oluşturduğunuz kullanıcı hesabıyla oturum açabilirsiniz.

    > [!NOTE]
    > Bir “.onmicrosoft.com” hesabı ayarlıyorsanız, kullanıcı hesabında adresin bir parçası olarak **.onmicrosoft.com** görünür. 

   ![İş veya okul hesabınızı girme](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    Şirketinizin veya okulunuzun cihazınızı kaydettiğini belirten bir ileti görürsünüz.

4. **Her şey hazırsınız!** ekranını görünce **Bitti**’yi seçin. İşiniz bitti.

5. Eklenen hesabı artık Windows Masaüstü cihazınızdaki **İş veya okula erişim** ayarlarında görebilirsiniz.

   ![Yeni eklenen hesabın ekran görüntüsü](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    Önceki adımları izlediyseniz, ancak iş veya okul e-posta hesabınıza ve dosyalarınıza erişemiyorsanız, [işe veya okula erişim görüyorsanız Izlenecek sorun giderme adımları](../user-help/troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-access-work-or-school)bölümündeki adımları izleyin.

## <a name="confirm-your-device-enrollment-in-intune"></a>Intune’da cihaz kaydınızı onaylama

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) genel yönetici veya Intune Hizmet Yöneticisi olarak oturum açın.
2. Intune 'da kayıtlı cihazları görüntülemek için **tüm cihazlar** > **cihazları** seçin.
3. Intune’a kayıtlı bir ek cihazınız olduğunu doğrulayın.

   ![Intune’a kayıtlı cihazların ekran görüntüsü](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

Windows cihazınızın kaydını silmek için bkz. [Windows cihazınızı yönetimden kaldırma](../user-help/unenroll-your-device-from-intune-windows.md).

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta Windows 10 cihazları Intune’a kaydetmeyi öğrendiniz. Tüm platformlar genelinde cihaz kaydetmenin başka yolları hakkında bilgi edinebilirsiniz. Cihazları Intune ile kullanma hakkında daha fazla bilgi için bkz. [İşlerinizi tamamlamak için yönetilen cihazlar kullanma](../user-help/use-managed-devices-to-get-work-done.md).

Bu Intune hızlı başlangıç serisini takip etmek için bir sonraki hızlı başlangıca ilerleyin.

> [!div class="nextstepaction"]
> [Hızlı Başlangıç: Android cihazlar için gerekli parola uzunluğunu ayarlama](../protect/quickstart-set-password-length-android.md)
