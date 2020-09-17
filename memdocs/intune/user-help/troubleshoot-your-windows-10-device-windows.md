---
title: Okul veya iş için Windows 10 cihaz erişiminin sorunlarını giderme | Microsoft Intune
description: Kayıtlı bir Windows 10 cihazının erişimini veya hesap bağlantı sorunlarını çözün.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 268ef3b9931c86a73ccf4e681240e4d2333c8026
ms.sourcegitcommit: 2339c927b6576db8878f34f167a9a45c5dc9f58d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90689404"
---
# <a name="troubleshoot-windows-10-device-access"></a>Windows 10 cihaz erişimi sorunlarını giderme
Bu makalede, kayıtlı bir Windows 10 cihazına yönelik erişim sorunlarının nasıl çözümleneceği açıklanır. 

## <a name="check-wi-fi-connection"></a>Wi-Fi bağlantısını denetle  

İş veya okul kaynaklarına erişmek için Wi-Fi bağlantısı gerekir. Wi-Fi ' a bağlı olduğunuzdan emin olun ve ardından kaynaklara erişmeyi yeniden deneyin.  

## <a name="add-work-or-school-account-in-settings-app"></a>Ayarlar uygulamasında iş veya okul hesabı ekle  
Bu adımlar, cihazınızı kaydetmek için kullandığınız aynı. Ancak, hesabınız **Ayarlar** uygulamasında görüntülenmiyorsa, bu adımları bir kez daha çalıştırmanız gerekir.  

1. **Ayarlar** uygulamasını başlatın. 
2. **Hesaplar**’ı seçin.
3. Bu sonraki adım, kullanmakta olduğunuz Windows 10 sürümüne bağlı olarak farklılık gösterir. 
    * Sürüm 1607 ve sonrası: **işe veya okula erişim**' i seçin.
    * Sürüm 1511 ve önceki sürümler: **iş erişimi**' ni seçin.  
4. Hesabınızı kontrol edin. Listede yoksa, eklemek için **Bağlan** artı imzala düğmesini seçin. 
5. İş veya okul kimlik bilgilerinizle oturum açın. 
6. Bağlantıyı tamamlaması için ekrandaki istemleri izleyin.  
7. İşlem tamamlandığında, hesabınız bağlantı olarak eklenir. Kuruluşunuzun kullanılabilir hale getiren kaynaklara erişebilirsiniz.   

## <a name="contact-it-support-for-access-requirements"></a>Erişim gereksinimleri için BT desteğiyle iletişime geçin  
Ayarlar uygulamasında iş veya okul hesabınızı görürseniz, cihazınız ve hesabınız zaten bağlı demektir. Erişim sorunlarıyla ilgili daha fazla yardım için BT destek sorumlunuza başvurun. Belirli kaynaklara erişmenizi engelleyen kısıtlamalar veya gereksinimler olabilir.  

## <a name="error-messages"></a>Hata iletileri  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>Girilen kullanıcı adıyla eşleşen bir yönetim uç noktası otomatik olarak bulunamadı. lütfen kullanıcı adınızı kontrol edin ve oturum açmayı yeniden deneyin. Yönetim uç noktanızın URL 'sini biliyorsanız lütfen girin.

**Neden**: hesabınız, girilen URL 'nin yanı sıra (Yönetim uç noktası olarak da anılır) doğrulanamadı.  

#### <a name="resolution"></a>Çözüm
1. Kullanıcı adınızı ve parolanızı yeniden girin. 
2. Hala çalışmazsa, doğru URL 'YI almak için BT destek sorumlunuza başvurun (örnek: <code>www.yourcompany.onmicrosoft.com</code> ). 
3. İstendiğinde, belirtilen URL 'YI girin. 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>Bağlı değilsiniz gibi görünüyor. Ağa bağlı olduğunuzdan emin olun.

**Neden**: Cihazınız Wi-Fi ' y e bağlı değildir ve bir iş veya okul hesabı eklemek için bir bağlantı gerekir.     

#### <a name="resolution"></a>Çözüm
1. Cihaz araç çubuğınızdan veya ayarlarınızda **ağ durumu** küre simgesini seçin.
2. **Connect**> bir Wi-Fi ağı seçin.  
3. Hesabınızı yeniden bağlamayı deneyin.  


## <a name="next-steps"></a>Sonraki adımlar  

Bu bilgiler yardımcı olmadı mı? BT destek sorumlunuza başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.
