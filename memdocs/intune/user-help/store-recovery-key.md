---
title: Şirket Portalı Web sitesi aracılığıyla Intune 'da bir kurtarma anahtarı depolama
description: Şirket Portalı Web sitesinden cihaz kurtarma anahtarınızı karşıya yükleyin ve saklayın.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f0a674753ff23fca509bd21e6b52101104a6803f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910800"
---
# <a name="store-your-personal-filevault-key"></a>Kişisel dosya Kasası anahtarınızı depolayın 

Kişisel olarak şifrelenen macOS cihazınız için bir Filekasa anahtarı depolayın. Şifreleme gereksinimlerinin karşılamanın yanı sıra, anahtarınızı Intune 'da depolamak şunları yapmanıza olanak sağlar: 

* Her cihazdan kolayca ve hızlı bir şekilde anahtar alabilir veya döndürün. 
* Anahtarı almanız veya döndürmenize gerek yoksa uygulama veya Web sitesine kendiniz erişebilmek için destek sorumlunuza yardım isteyin.


## <a name="retrieve-or-rotate-the-key"></a>Anahtarı alma veya döndürme

Cihazınızı kilitlediyseniz, anahtarınızı aşağıdaki konumlardan alabilirsiniz:
   
- Şirket Portalı web sitesi
- İOS için Şirket Portalı App/ıpados 
- Android için Şirket Portalı uygulaması
- Intune uygulaması
 
 Intune 'a yönetici erişimi olan kişilerin cihazınızı kilitlediyseniz, kişisel kurtarma anahtarınızı sizin için döndürebilir. Anahtarlar, yalnızca şirkete ait cihazlara ait olanlar da görüntülenebilir. BT, kişileri kişisel cihazlara ait olan kurtarma anahtarlarını görüntüleyemez.   


## <a name="do-i-need-to-store-my-key"></a>Anahtarımı depolamam gerekiyor mu?  
BT destek sorumlusu, kişisel bir kurtarma anahtarını karşıya yüklemeniz gerektiğini size sağlar. Kuruluşunuzun BT departmanı normalde sizinle iletişim kuruyorsa iOS/ıpados veya Android için Şirket Portalı uygulamalarından bir bildirim alabilirsiniz. 

Yalnızca aşağıdaki kategorilerden birine düşiyorsanız bir kurtarma anahtarı yüklemeniz önerilir:
* Cihazınızı kuruluşunuza kaydetmeden önce şifrelemiş olursunuz. 
* MacOS sistem tercihleri aracılığıyla cihazınızı el ile şifrelemiş olursunuz.   

Kuruluşunuzun ilkelerine bağlı olarak, anahtarınızı karşıya yükleyene kadar cihazınızdaki kurumsal kaynaklara erişiminizi engellemiş olabilirsiniz.  

## <a name="upload-personal-recovery-key"></a>Kişisel kurtarma anahtarını karşıya yükle 
Şifrelenmiş Mac cihazınız için kişisel dosya Kasası anahtarını kaydetmek için bu adımları uygulayın.  


1. [Şirket portalı Web sitesine](https://portal.manage.microsoft.com) gidin ve okul veya iş hesabınızla oturum açın. 
2. Şifrelenmiş cihazınızı seçin.
3. **Mağaza kurtarma anahtarını**seçin.  
4. 24 karakterlik, alfasayısal dosya Kasası anahtarınızı girin.  
5. Anahtarı yeniden girin. Sonra **Kaydet**'i seçin.
6. Şirket Portalı kişisel kurtarma anahtarınızı doğrulamaya, döndürmeye ve kaydetmeye çalışacaktır. Anahtar kaydedildikten sonra başka bir eylem gerekmez. Karşıya yükleme tamamlanmadan önce Web sitesini bırakırsanız, bir sonraki oturum açışınızda cihaz ayrıntıları sayfasında durumunu görüntüleyebilirsiniz.  

Bu işlem sırasında görebileceğiniz iletiler hakkında daha fazla bilgi için bkz. [Şirket portalı iletileri](store-recovery-key.md#company-portal-messages).  

## <a name="company-portal-messages"></a>Şirket Portalı iletileri

|İleti  |Anlamı  |
|---------|---------|
|Anahtarların eşleşmesi gerekir. Anahtarları denetleyin ve yeniden deneyin.     | Anahtarlarınızı birbirleriyle eşleşmediğini bildirmek için **Kurtarma anahtarını onayla** altında görünür. Anahtarları her iki alana da yeniden yazın ve tekrar kaydetmeyi deneyin.        |
|Cihazın kurtarma anahtarı güncelleştirilemedi.| Şirket Portalı, sizin için bir kurtarma anahtarı depolayamediğini bildirmek için ekranın üst kısmında bir bildirim bildirimi olarak görünür. Daha fazla ayrıntı için, Şifrelenmiş cihazınızı seçin. Ardından sonraki adımlar için sayfanın üst kısmındaki iletiyi okuyun. |
|Kurtarma anahtarınızı karşıya yükleyemedik. Doğru anahtarı girdiğinizden emin olun ve yeniden deneyin. Sorun devam ederse, anahtarınızı el ile döndürmeyi deneyin. Daha fazla bilgi için dokunun.     | Cihaz ayrıntıları sayfasında görünür ve birkaç şey anlamına gelebilir: Ilk olarak, girdiğiniz anahtar yanlış olduğundan Şirket Portalı anahtarınızı kaydedemedi. Doğru anahtara sahip olduğunuzu doğrulayın ve yeniden deneyin. İkinci olasılık, cihazınızın kuruluşunuzda bir süredir birlikte iade edilmedi olması. Kuruluşunuzdaki en son güncelleştirmeleri eşitlemek için cihazınızı seçin > **durum**  >  **denetimi erişimi**. Sonra kurtarma anahtarını depolamayı yeniden deneyin. Son olarak, sorun devam ederse kuruluşunuzun dosya kasasını tarafında etkinleştirmemiş olması anlamına gelebilir. BT destek sorumlunuza başvurun ve cihazınızı eşitlebildiğinizi, ancak yine de dosya Kasası anahtarınızı depolayalım.         |
|Kurtarma anahtarınız güncelleştirildi. Cihazınızı kilitlediyseniz ve anahtarınızı almanız gerekiyorsa, Şirket Portalı oturum açın ve **Kurtarma anahtarı al**' ı seçin.    | Cihaz ayrıntıları sayfasında görünür. Kaydettiğiniz anahtar başarıyla döndürüldü ve yeni kişisel kurtarma anahtarınız depolanıyor.    |



## <a name="it-pro-support"></a>BT uzmanı desteği

BT destek sorumlunuza sahipseniz ve kuruluşunuzdaki Mac cihazları için dosya Kasası şifrelemesini yapılandırmak ve yönetmek istiyorsanız, bkz. [Intune Ile macOS Için filekasası disk şifrelemeyi kullanma](../protect/encrypt-devices-filevault.md).  

## <a name="next-steps"></a>Sonraki adımlar

Anahtarınızı her zaman Şirket Portalı Web sitesinden, Intune uygulamasından ve iOS ve Android için Şirket Portalı uygulamalarla alabilir ve Mac cihazınıza erişmek için kullanabilirsiniz. Kurtarma anahtarınızı alma hakkında bilgi edinmek için bkz. [Kurtarma anahtarını alma](get-recovery-key-cpweb.md).

Şirket Portalı Web sitesinde yapabileceğiniz diğer şeyleri öğrenin. Eylemlerin listesi için [Intune şirket portalı Web sitesini kullanma](using-the-intune-company-portal-website.md) konusuna bakın.  

Bu bilgiler yardımcı olmadı mı? BT destek sorumlunuza başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.