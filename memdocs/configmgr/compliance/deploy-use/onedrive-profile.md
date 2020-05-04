---
title: OneDrive İş Profilleri
titleSuffix: Configuration Manager
description: Configuration Manager ' de bir OneDrive Iş profili kullanarak Windows bilinen klasörlerini OneDrive Iş 'e yönlendirin.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 47d44c96e0ae63504278c58a5838c54648665505
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712242"
---
# <a name="onedrive-for-business-profiles"></a>OneDrive İş Profilleri

Configuration Manager sürüm 1902 ' den başlayarak, Windows bilinen klasörlerini OneDrive Iş 'e taşımak için OneDrive Iş profilleri oluşturabilirsiniz. Bu klasörler Masaüstü, belgeler ve resimleri içerir. Her profilde, Windows bilinen klasörlerini taşımaya yönelik ayarları belirtebilirsiniz. OneDrive Iş hakkında daha fazla bilgi için bkz. [yeniden yönlendirme ve Windows bilinen klasörlerini OneDrive 'a taşıma](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Önkoşullar

- [Office 365 Kiracı KIMLIĞINIZI bulun](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- OneDrive Sync Client sürüm 18.111.0603.0004 veya üstünü dağıtın. Daha fazla bilgi için bkz. [Configuration Manager kullanarak OneDrive uygulamaları dağıtma](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a>Windows bilinen klasörlerini OneDrive 'a taşı
<!--3556021-->
Windows bilinen klasörlerini OneDrive Iş 'e taşımak için Configuration Manager kullanın. Bu klasörler Masaüstü, belgeler ve resimleri içerir. Windows 10 yükseltmelerinizi basitleştirmek için, bir görev dizisini dağıtmadan önce bu ayarları Windows 7 istemcilerine dağıtın. 

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **OneDrive iş profilleri** düğümünü seçin.  

   ![OneDrive Iş profilleri düğümü](media/onedrive-for-business-profiles-node.png)
2. Şeritte **OneDrive Iş profili oluştur**' u seçin.  

3. Bu ilkeyi tanımlayacak bir ad belirtin ve **İleri**' yi seçin.  

4. OneDrive Iş profili ile hazırlanacak platformları seçin. Platformları seçmeyi tamamladığınızda **İleri**' ye tıklayın.

    ![OneDrive Iş profili için platformları seçin](media/onedrive-for-business-profile-select-platforms.png) 

5. **Ayarlar** sayfasında:

    1. Office 365 Kiracı KIMLIĞINIZI belirtin.  

    2. Bilinen klasörleri OneDrive 'a taşımak için aşağıdaki seçeneklerden birini belirleyin:  

        - **Kullanıcılardan Windows bilinen klasörlerini OneDrive 'a taşımasını iste**: Bu seçenekle Kullanıcı, dosyalarını taşımak için bir sihirbaz görür. Klasörlerin taşınmasını ertelemeyi veya reddetmeyi tercih ederseniz, OneDrive düzenli olarak bunları hatırlatır.  

        - **Windows bilinen klasörlerini sessizce OneDrive 'a taşıyın**: Bu ilke cihaz Için geçerliyse OneDrive istemcisi, bilinen klasörleri otomatik olarak OneDrive iş 'e yönlendirir.  

            - **Klasörler yeniden yönlendirildikten sonra kullanıcılara bildirim göster**: Bu seçeneği etkinleştirirseniz OneDrive istemcisi, kendi klasörlerini taşıdıktan sonra kullanıcıyı bilgilendirir.  

    3. **Kullanıcıların Windows bilinen KLASÖRLERINI bilgisayarına geri yönlendirmesini engelle**: Bu klasörü, kullanıcıların bu klasörleri yeniden cihaza taşımasını sağlamak Için Istemcideki OneDrive iş 'te devre dışı bırakır.  

       ![OneDrive Iş için bilinen klasör taşıma ayarları](media/onedrive-for-business-profile-move-folder-settings.png)

6. Sihirbazı tamamlayıp ilkeyi dağıtın.  


## <a name="deploy-the-onedrive-for-business-profile"></a>OneDrive Iş profilini dağıtma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **OneDrive iş profilleri** düğümünü seçin.  


2. Profili seçin ve şeritte **Dağıt** ' ı seçin.

3. Dağıtımınız için aşağıdaki ayarları belirtin:

   1. **Koleksiyon**: **gözatıp...** öğesine tıklayın ve ardından profili dağıtmak istediğiniz koleksiyonu seçin.  
   1. **Uyarı oluştur**:

      - **Uyumluluk şu oranın altında**: devam etmek için en düşük istemci uyumluluğu yüzdesi, aksi takdirde bir uyarı oluşturulur.
      -  **Tarih ve saat**: Tarih uyarıları ilk olarak profil uyumluluğuna göre üretilme başlar.
      - **System Center Operations Manager uyarı oluştur**: System Center Operations Manager için bir uyumluluk uyarısı gönderin.
   1. **Zamanlama**:

      - **Basit zamanlama**: Bu ayar, varsayılan olarak her yedi günde bir uyumluluk değerlendirmesi başlatmak için basit bir zamanlama kullanır.
      - **Özel zamanlama**: uyumluluk değerlendirmesinin ne zaman çalıştırılacağını tanımlayın. Başlangıç saati, zamanlamayı oluştururken Configuration Manager konsolunu çalıştıran bilgisayar için yerel saate dayalıdır veya UTC 'yi kullanabilirsiniz.
 
      ![OneDrive Iş profilini dağıtma](media/onedrive-for-business-deploy-profile.png)

4. OneDrive Iş profilini dağıtmak için **Tamam** ' ı tıklatın.


## <a name="next-steps"></a>Sonraki adımlar

[Uzak bağlantı profilleri oluşturma](create-remote-connection-profiles.md)
