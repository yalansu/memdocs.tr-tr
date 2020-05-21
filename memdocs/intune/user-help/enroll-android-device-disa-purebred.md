---
title: Microsoft Intune App ve DıŞA üfle bir Android cihazı kaydetme
description: Bir Android cihazını kaydetmeyi ve birlikte bulunan kimlik bilgisi kimlik doğrulamasını, DıŞA purebred ile ayarlamayı öğrenin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f92a23b117582ef40d236fe257917018431128e
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633409"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Microsoft Intune App ve DıŞA Üflerle Android cihazı ayarlama

Kuruluşunuzun e-postasına, dosyalarına ve uygulamalarına güvenli, mobil erişim kazanmak için cihazınızı Microsoft Intune uygulamasına kaydedin. Cihazınız kaydedildikten sonra, *yönetilen*hale gelir. Kuruluşunuz, Intune gibi bir mobil cihaz yönetimi (MDM) sağlayıcısı aracılığıyla cihaza ilkeler ve uygulamalar atayabilir.  

Kayıt sırasında, bir türetilmiş kimlik bilgisini cihazınıza de yüklersiniz. Kuruluşunuz, kaynaklara erişirken veya e-postaları imzalama ve şifreleme için türetilmiş kimlik bilgilerini bir kimlik doğrulama yöntemi olarak kullanmanızı gerektirebilir.

Şunları yapmak için bir akıllı kart kullanıyorsanız, büyük olasılıkla türetilmiş bir kimlik bilgisi ayarlamanız gerekir:

* Okul veya iş uygulamalarında oturum açma, Wi-Fi ve sanal özel ağlar (VPN)
* Okul veya iş e-postalarını S/MIME sertifikaları kullanarak imzalama ve şifreleme

Bu makalede şunları yapacaksınız:

* Intune uygulamasıyla bir mobil Android cihaz kaydetme
* Kuruluşunuzun türetilmiş kimlik bilgisi sağlayıcısından türetilmiş bir kimlik bilgisi yükleyerek akıllı kartınızı ayarlama, [dışa purebred](https://public.cyber.mil/pki-pke/purebred/)

## <a name="what-are-derived-credentials"></a>Türetilmiş kimlik bilgileri nelerdir?

Türetilmiş kimlik bilgileri, akıllı kart kimlik bilgilerinizle derlenen ve cihazınızda yüklü olan bir sertifikadır. Bu, iş kaynaklarına uzaktan erişim izni verir, ancak yetkisiz kullanıcıların hassas bilgilere erişmesini önler.

Türetilmiş kimlik bilgileri şu şekilde kullanılır:

* Okul veya iş uygulamalarında, Wi-Fi ve VPN 'de oturum açan öğrencilerin ve çalışanların kimliklerini doğrulama
* Okul veya iş e-postalarını S/MIME sertifikaları ile imzalama ve şifreleme

Türetilmiş kimlik bilgileri, özel yayın (SP) 800-157 kapsamında türetilmiş kişisel kimlik doğrulama (PıV) kimlik bilgileri için ulusal standartlar ve Teknoloji Enstitüsü (NıST) kuralları uygulamasıdır.

## <a name="prerequisites"></a>Ön koşullar

Kaydı tamamlayabilmeniz için, şunları yapmanız gerekir:

* Okulunuz veya iş tarafından sağlanmış akıllı kartınız
* Akıllı kartınızla oturum açabileceğiniz bir bilgisayar veya bilgi noktası erişimi
* Android 7,0 veya üzerini çalıştıran yeni veya fabrika ayarlarına sahip bir cihaz 
* Cihazınızda yüklü Microsoft Intune uygulaması
* Cihazınıza yüklenmiş purebred uygulaması (uygulama cihaz kurulumundan kısa bir süre sonra otomatik olarak yüklenmelidir. Bu yoksa BT destek sorumlunuza başvurun.)

Ayrıca, kurulum sırasında purebred Aracısı veya temsilcisiyle iletişim kurmanız gerekecektir.

## <a name="enroll-device"></a>Cihaz kaydetme  

1. Yeni veya fabrika ayarlarına sıfırlama cihazınızı açın.  
2. **Hoş Geldiniz** ekranında dili seçin. QR kodu veya NFC ile kayıt yapmanız istenirse, yöntemiyle eşleşen aşağıdaki adımları izleyin.  
     * NFC: kuruluşunuzun ağına bağlanmak için bir programcı cihazında NFC ile desteklenen cihazınıza dokunun. Ekrandaki istemleri izleyin. Chrome 'un hizmet koşulları ekranına ulaştığınızda, 5. adıma geçin.  

     * QR kodu: [QR kod kaydı](#qr-code-enrollment)'Ndaki adımları doldurun.  

     Başka bir yöntem kullanmanız istenirse adım 3 ' e geçin.    

3. Wi-Fi ' e bağlanın ve **İleri**' ye dokunun. Kayıt yönteminiz ile eşleşen adımı izleyin. 

    * Belirteç: Google oturum açma ekranına geldiğinizde, [belirteç kaydı](#token-enrollment)'ndaki adımları doldurun.  
    * Google sıfırı Touch: Wi-Fi ' a Bağlandıktan sonra cihazınız kuruluşunuz tarafından tanınacaktır. 4. adıma geçin ve kurulum tamamlanana kadar ekrandaki istemleri izleyin.    
 
       ![Google of Touch kullanıyorsanız gördüğünüz Google terimleri ekranının örnek görüntüsü, & devam et ' i vurgulama düğmesi.](./media/google-zero-touch-intune-app-01.png)   
   
4. Google 'ın şartlarını gözden geçirin. Sonra **& devam et**' e dokunun.  

      ![Google terms ekranının örnek görüntüsü, kabul & devam et düğmesine vurgu.](./media/fully-managed-intune-app-04.png)   

5. Chrome 'un hizmet koşullarını gözden geçirin. Sonra **& devam et**' e dokunun.  

   ![Chrome hizmet koşulları ekranının örnek görüntüsü, & devam et düğmesine vurgu.](./media/fully-managed-intune-app-06.png)   

6. Oturum açma ekranında, **oturum açma seçenekleri** ' ne tıklayın ve ardından **başka bir cihazdan oturum açın**. 

7. Ekrandaki kodu yazın.  

8. Akıllı kart etkin cihazınıza geçin ve ekranınızda gösterilen web adresine gidin. 

9. Daha önce yazdığınız kodu girin.

   > [!div class="mx-imgBorder"]
   > ![Şirket Portalı Web sitesinin ekran görüntüsü "kod girin" istemi.](./media/enter-code-intercede.png)

10. Oturum açmak için akıllı kartınızı ekleyin. 

11. Oturum açma ekranında iş veya okul hesabınızı seçin. Ardından mobil cihazınıza geri dönün. 

12. Kuruluşunuzun gereksinimlerine bağlı olarak, ekran kilitleme veya şifreleme gibi ayarları güncelleştirmeniz istenebilir. Bu istemler görürseniz **Ayarla** ' ya dokunun ve ekrandaki yönergeleri izleyin.  

       ![İş telefonunuzu ayarlama ekranınızın örnek görüntüsü, küme oluştur düğmesi.](./media/fully-managed-intune-app-10.png)   

13. Cihazınıza iş uygulamaları yüklemek için, **yükler**' e dokunun. Yükleme tamamlandıktan sonra **İleri**' ye dokunun.  

       ![İş telefonunuzu ayarlama ekranınızın örnek görüntüsü, Install düðmesini vurgulaması.](./media/fully-managed-intune-app-11.png)   

14. Microsoft Intune uygulamasını açmak için **Başlat** ' a dokunun. 

    ![İş telefonunuzu ayarlama ekranınızın örnek görüntüsü, Başlat düğmesini vurguladır.](./media/fully-managed-intune-app-17.png)   

15. Mobil cihazınızda Intune uygulamasına dönün ve kayıt tamamlanana kadar ekrandaki yönergeleri izleyin. 

    ![Erişim ayarlama, cihaz ekranınızı kaydetme, bitti düğmesi gibi örnek görüntü.](./media/fully-managed-intune-app-19.png)   

16. Cihazınızı ayarlamayı bitirmeden bu makaledeki [akıllı kartınızı ayarlama](enroll-android-device-disa-purebred.md#set-up-smart-card) bölümüne ilerleyin.  

### <a name="qr-code-enrollment"></a>QR kod kaydı  
Bu bölümde, şirketinizin sağladığı QR kodunuzu taracaksınız.  İşiniz bittiğinde cihaz kayıt adımlarına geri yönlendiriyoruz.     
  
1. **Karşılama** EKRANıNDA, QR kodu kurulumu 'nu başlatmak için ekrana beş kez dokunun.  

   ![Cihaz kurulumu hoş geldiniz ekranının örnek görüntüsü, ekrana dokunarak görüntülenecek yönergeleri vurgular.](./media/qr-code-intune-app-01.png)  

2. Wi-Fi ' a bağlanmak için ekrandaki yönergeleri izleyin.  
3. Cihazınızın bir QR kodu tarayıcısı yoksa, kurulum ekranları bir tarayıcı yüklendiği için ilerlemeyi gösterir. Yüklemenin tamamlanmasını bekleyin.  
4. İstendiğinde, kuruluşunuzun size verdiği kayıt profili QR kodunu tarayın.  
5. [Cihaza kaydet](#enroll-device)'e dönün, kuruluma devam etmek için 4. adımı izleyin.  

### <a name="token-enrollment"></a>Belirteç kaydı  
Bu bölümde, şirketinizin sunduğu belirteci girersiniz. İşiniz bittiğinde cihaz kayıt adımlarına geri yönlendiriyoruz.  

1. Google oturum açma ekranında, **e-posta veya telefon** kutusuna **AFW # kurulum**yazın. **İleri**' ye dokunun. 

   ![Google oturum açma ekranının örnek görüntüsü, "AFW # kurulum" ın alana yazılmış olduğunu gösterir.](./media/token-intune-app-01.png)   

2. **Android cihaz ilkesi** uygulaması için **yüklemeyi** seçin. Yükleme işlemine devam edin. Cihazınıza bağlı olarak, ek koşulları gözden geçirmeniz ve kabul etmeniz gerekebilir.    

3. **Bu cihazı kaydet** ekranında **İleri**' yi seçin.  

4. **Kodu girin**' i seçin.  

5. **Tarama veya kod girme** ekranında, kuruluşunuzun size verdiği kodu yazın.  Ardından **İleri**’ye tıklayın.  

   ![Taramanın örnek görüntüsü veya kod girme, Ileri vurgu düğmesi.](./media/token-intune-app-04.png)  

6. [Cihaza kaydet](#enroll-device)'e dönün, kuruluma devam etmek için 4. adımı izleyin.


## <a name="set-up-smart-card"></a>Akıllı kart ayarlama  

> [!NOTE]
> Purebred uygulamasının bu adımları tamamlaması gerekir ve kayıt sonrasında cihazınıza otomatik olarak yüklenir. Kısa süre bekledikten sonra uygulamaya hala sahip değilseniz BT destek sorumlunuza başvurun.  

1. Kayıt tamamlandıktan sonra, Intune uygulaması akıllı kartınızı ayarlamanıza yönelik bildirim gönderir. Bildirime dokunun. Bildirim alamazsanız, e-postanızı kontrol edin.

   > [!div class="mx-imgBorder"]
   > ![Cihaz giriş ekranında Intune uygulama anında iletme bildirimi ekran görüntüsü.](./media/action-required-in-app-android.png)

2. **Akıllı kart ayarla** ekranında:

   1. Kuruluşunuzun kurulum yönergelerinin bağlantısına dokunun ve bunları gözden geçirin. Kuruluşunuz ek yönergeler sağlamıyorsa, bu makaleye gönderilir.

   2. **Başlat**' a dokunun.   

   > [!div class="mx-imgBorder"]
   > ![Intune uygulamasının ekran görüntüsü, akıllı kart ekranı ayarlama.](./media/smart-card-open-disa-purebred-android.png)

3. **Sertifika al** ekranında purebred 'yi **Başlat** ' a dokunarak purebred uygulamasını açın. (Uygulama cihazınıza otomatik olarak yüklenmiş olmalıdır. Bu yoksa, destek sorumlunuza başvurun.)  

   > [!div class="mx-imgBorder"]
   > ![Bulunan DıŞA Üfte bred uygulamasını açmak için Intune uygulama isteminin ekran görüntüsü.](./media/open-app-prompt-disa-purbred-android.png)  

4. Purebred uygulamasının düzgün çalışması için ek izinler gerekebilir. **Izin ver** ' e dokunun veya istendiğinde **Tüm saate izin verin** . Bu izinlerin neden gerekli olduğu hakkında daha fazla bilgi için destek sorumlunuza veya purebred aracısıyla konuşun.  

5. Purebred uygulamasında olduktan sonra, iş veya okul kaynaklarına erişmeniz gereken sertifikaları indirip yüklemek için kuruluşunuzun purebred aracısıyla birlikte çalışın.

    > [!IMPORTANT]
    > Bu işlem sırasında, istendiğinde **Tamam** ' a veya **yüklensin** ' e dokunun. Yüklenmesi istenen herhangi bir sertifika yetkilisi (CA) veya sertifika adını değiştirmeyin.    

6. Yükleme tamamlandıktan sonra, sertifikalarınızın hazırlanmaya yönelik bir bildirim alırsınız. Intune uygulamasına geri dönmek için bildirime dokunun.

    > [!div class="mx-imgBorder"]
    > !["Sertifikalara erişime Izin ver" ekranının ekran görüntüsü](./media/certificates-ready-prompt-disa-purbred-android.png)

7. **Sertifikalara erişime Izin ver** ekranında, Intune UYGULAMASıNA, dışa yönelik olarak bulunan türetilmiş kimlik bilgilerine erişim izni verirsiniz. Bu adım, korumalı iş veya okul kaynaklarına her eriştiğinizde kuruluşunuzun kimliğinizi doğrulayabilmesini sağlar.  

    1. **İleri**' ye dokunun.

       > [!div class="mx-imgBorder"]
       > !["Sertifikalar hazırlanıyor" isteminin ekran görüntüsü](./media/certificates-access-disa-purbred-android.png)

    2. **Sertifika seçmeniz**istendiğinde seçimi değiştirmeyin. Doğru sertifika zaten seçili olduğundan, yalnızca **Seç** veya **Tamam**' a dokunun.  

       > [!div class="mx-imgBorder"]
       > !["Sertifika Seç" isteminin ekran görüntüsü](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. Türetilmiş kimlik bilgileriniz birden çok sertifikadan oluşur, bu nedenle **sertifika seçme** isteğini birden çok kez görebilirsiniz. Daha fazla istem görünene kadar önceki adımı tekrarlayın.  

8. Tüm sertifikalar işlendikten sonra, Intune uygulamasının cihazınızı ayarlamayı tamamlamasını bekleyin. **Her şey ayarlamış** olduğunuzu gördüğünüzde kurulumun tamamlandığını bilirsiniz! etkileşime geçebilirsiniz.  

    > [!div class="mx-imgBorder"]
    > !["Tüm hazırsınız" ekranının ekran görüntüsü](./media/all-set-android.png)

## <a name="next-steps"></a>Sonraki adımlar

Kayıt tamamlandıktan sonra e-posta, Wi-Fi ve kuruluşunuzun kullanabildiği tüm uygulamalar gibi iş kaynaklarına erişebilirsiniz. Intune uygulamasında uygulama alma, arama, yükleme ve kaldırma hakkında daha fazla bilgi için bkz.:

* [Cihazınızdaki yönetilen uygulamaları kullanma](use-managed-apps-on-your-device-android.md)  
* [Şirket Portalı Web sitesinden uygulamaları yönetme](manage-apps-cpweb.md)  


Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.
