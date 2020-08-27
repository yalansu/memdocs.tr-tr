---
title: Mobil cihazınıza mobil tehdit savunması 'nı yükler
description: Mobile Threat Defense uygulamalarının ne olduğunu ve bir tanesi ayarlamayı öğrenin.
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
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 9ac83ce840d4a43de98791d6b116bb373a018a7d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914200"
---
# <a name="install-mobile-threat-defense-app"></a>Mobil tehdit savunması uygulamasını yükleme  

> [!TIP]
> Pazardaki çeşitli MTD uygulamaları vardır. Kuruluşunuzun hangisini kullanacağınızı söylemiş olması gerekir. Bir MTD uygulaması yüklemek isteyip istemediğiniz sorulursa uygulamayı ayarlamaya veya yüklemeye hemen yönlendirilmezseniz yardım için BT destek sorumlunuza başvurun.  

Kuruluşunuzun güvenlik gereksinimlerinin bir parçası olarak, bir Mobile Threat Defense (MTD) satıcı uygulaması yüklemenize gerek duyabilirsiniz. Bu tür bir uygulama, cihazınızdaki şüpheli uygulamalar, ağlar veya işletim sistemi güvenlik açıkları gibi tehditleri algılar ve sizi uyarır.  

Gerekli MTD uygulamanız yoksa, iş veya okul hesabınızla korumalı, yönetilen uygulamalarda (Microsoft Excel veya OneDrive gibi) oturum açmanız engellenir. Bu makalede, [BIR MTD uygulamasını ayarlamayı](set-up-mobile-threat-defense.md#set-up-mtd-app) ve yeniden erişim elde etme hakkında bilgi edineceksiniz.    

## <a name="mtd-apps-for-ios"></a>İOS için MTD uygulamaları
Aşağıdaki MTD uygulamaları genellikle iOS cihazlarında kullanılır. Uygulama mağazasındaki listesini açmak için bir uygulama seçin.   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>Android için MTD uygulamaları 
Aşağıdaki MTD uygulamaları genellikle Android cihazlarda kullanılır. Google Play listesini açmak için bir uygulama seçin.  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zyium mobil IP 'leri (ZIP 'ler)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>Kuruluşunuzun görebileceği bilgiler   

Kuruluşunuz, kişisel uygulamalarınızda metin, e-posta ve resim gibi verileri göremez. MTD uygulaması, uygulamalarınız hakkında ad ve sürüm gibi bilgileri kuruluşunuza bildirir. Bildirilen gerçek bilgiler, şirketinizin kullandığı MTD satıcısına bağlıdır. Kuruluşunuz şunları görebilir:   

* Uygulama adı  
* Uygulama KIMLIĞI: Google Play içinde uygulamayı tanımlayan benzersiz ad.  
* Uygulama sürümü ve kısa sürüm numarası: bir uygulama için belirli sürüm numaraları.  
* Uygulama paketi ve dinamik Boyut: bir uygulamanın cihazınızda kullandığı alan miktarı. 


## <a name="set-up-mtd-app"></a>MTD uygulamasını ayarlama 
Korumalı bir uygulamada oturum açtığınızda, bir MTD uygulaması kurmanız istenir. Yüklemeyi tamamlayıp korumalı uygulamaya erişim kazanmak için ekrandaki adımları izleyin. 

Ek bağlam için, bu bölümdeki [iOS](set-up-mobile-threat-defense.md#ios-setup) veya [Android](set-up-mobile-threat-defense.md#android-setup) yönergelerine bakın. Bu adımlar, ekranda gösterilen yönergelerin yerini alacak ve bu adımların değiştirilmesini amaçlıyordu. 

Bir MTD uygulaması yüklemek isteyip istemediğiniz konusunda emin değilseniz, yardım için BT destek sorumlunuza başvurun.  

### <a name="device-registration"></a>Cihaz kaydı  
Kimlik doğrulamak ve okul veya iş hesabınızı cihazınıza bağlamak için cihaz kaydı gereklidir. Cihazınız kayıtlı değilse, MTD uygulamasını yüklemeden önce bu adımlarla ekranda otomatik olarak gezinirsiniz.   

Cihaz kaydı hakkında daha fazla bilgi için bkz. [kuruluşunuzun ağına kişisel cihazınızı kaydetme](/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>iOS kurulumu  
Bu adımlar, korumalı bir uygulamada oturum açtıktan sonra görünen **erişim al** ekranında başlar.  

1. **Erişim al** ekranında, kuruluşunuzun gerektirdiği MTD uygulamasını yüklemek için yönergeleri izleyin.   
2. **Erişim al** ekranına dönün ve **Aç**' ı seçin.  
3. MTD uygulaması Microsoft Authenticator açmak için izin ister. **Aç**’ı seçin. 
4. Oturum açmak için iş hesabınızı seçin. 
5. MTD uygulaması cihazınızı güvenlik tehditleri için taradığında bekleyin. 
6. İlk olarak erişmeye çalıştığınız okul veya iş uygulamasına geri dönün. Bu noktada, kuruluşunuz PIN oluşturma gibi diğer uygulama güvenlik gereksinimlerini yapılandırmanızı isteyebilir.   
7. Artık uygulamaya erişiminizin olması gerekir. Hala bloke ediyorsanız:  
    * **Erişim al** ekranında yeniden **Denetle**' yi seçin.  
    * MTD uygulamasına gidin ve mevcut tehditleri denetleyin. Tehdidi çözümlemek ve erişimi yeniden kazanmak için önerilen adımları izleyin.    

### <a name="android-setup"></a>Android kurulumu 
Bu adımlar, korumalı bir uygulamada oturum açtıktan sonra görünen **erişim al** ekranında başlar.  

1. **Erişim al** ekranında, kuruluşunuzun gerektirdiği MTD uygulamasını yüklemek için yönergeleri izleyin.  
2. **Erişim al** ekranına dönün ve **Aç**' ı seçin.  
3. MTD uygulaması, cihazınızın belirli alanlara erişmesi için izin ister. Bu uygulamanın düzgün çalışması için kişilere erişime **Izin vermeniz** gerekir. İstenen izinler, MTD satıcıları genelinde farklılık gösterir.  
4. Oturum açmak için iş hesabınızı seçin.  
5. MTD uygulaması cihazınızı güvenlik tehditleri için taradığında bekleyin.  
6. İlk olarak erişmeye çalıştığınız okul veya iş uygulamasına geri dönün. Bu noktada, kuruluşunuz PIN oluşturma gibi diğer uygulama güvenlik gereksinimlerini yapılandırmanızı isteyebilir.  
7. Artık uygulamaya erişiminizin olması gerekir. Hala bloke ediyorsanız:  
    * **Erişim al** ekranında yeniden **Denetle**' yi seçin.  
    * MTD uygulamasına gidin ve mevcut tehditleri denetleyin. Tehdidi çözümlemek ve erişimi yeniden kazanmak için önerilen adımları izleyin.  


## <a name="resolving-a-threat"></a>Tehdidi çözme
Bir tehdit algılanırsa ve kuruluşunuzun tanımlı tehdit düzeyini aşarsa, kuruluşunuz şu şekilde olur:  
   
* Erişimi engelle: iş veya okul hesabınızda oturum açtığınızda kuruluşunuzun korunan uygulamalarını kullanmanızı engeller.  
* Verileri silme: kuruluşunuzun korunan uygulamalarından bir veya daha fazla iş veya okul verilerini siler.  

Bir tehdidi çözümlemek ve korunan uygulamalara erişimi yeniden kazanmak için:  

1. Cihazınızda MTD uygulamasını açın.     
2. Tehdit ayrıntılarını uygulamada okuyun. Bu, tehdidi çözülmedi ve çözümlenmezse tehdidin cihazınızı nasıl etkileyebileceğini açıklar. 
3. Cihazınızda gerekli değişiklikleri yaptıktan sonra, MTD uygulamasına dönün ve yeni bir tarama başlatın. Tüm tehditler çözümlenene kadar bu adımları tekrarlayın. Değişikliklerinizin kuruluşunuzla eşitlenmesi birkaç dakika sürebilir. Bu değişiklikler eşitlendikten sonra korunan uygulamaya yeniden erişim elde edersiniz. 

## <a name="get-support"></a>Destek alma
Kuruluşunuzun iletişim bilgilerini bulmak için [Şirket portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) gidin. Hakkında yardım almak için onlara başvurun:

* Hangi MTD uygulamasının kullanılacağını belirleme  
* Yükleme  
* Yükleme başarısız  
* Tehdidi algılama/çözme  
* MTD uygulamasını kaldırma   
 

### <a name="share-app-logs-with-it-support"></a>Uygulama günlüklerini BT desteğiyle paylaşma  
Uygulama günlüklerinizi, başarısız bir yükleme hakkında daha fazla bağlam sağlamak için BT destek sorumlunuza da gönderebilirsiniz.  
* Android kullanıcıları: Şirket Portalı [günlüklerinizi karşıya yükleyin ve e-posta ile gönderin](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) .   

* iOS cihaz kullanıcıları: iOS için Microsoft Edge 'ten [günlüklerinizi alın ve gönderin](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) .  


## <a name="next-steps"></a>Sonraki adımlar  

Yönetilen uygulamaların nasıl çalıştığı, nasıl alınacağı ve bir tane kullandığınızı nasıl anlayacağınız hakkında daha fazla bilgi edinmek için aşağıdaki makalelere bakın.  

* [Android cihazınızdaki yönetilen uygulamaları kullanma](use-managed-apps-on-your-device-android.md)
* [iOS cihazınızdaki yönetilen uygulamaları kullanma](use-managed-apps-on-your-device-ios.md)  

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.

