---
title: Android cihazınızı şifreleme-Microsoft Intune | Microsoft Docs
description: Intune için gerektiğinde Android cihaz şifrelemesini açmayı öğrenin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/22/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 98950a6907db0ac6869b55ae26718a2919048154
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002656"
---
# <a name="encrypting-your-android-device"></a>Android cihazınızı şifreleme

Cihazınız kaybolur veya çalınırsa, cihaz şifreleme, dosyalarınızı ve klasörlerinizi yetkisiz erişimden korur. Bir geçiş kodu olmayan kişilerin verileri erişilemez ve okunamaz hale getirir. 

Okul veya iş kaynaklarına erişebilmek için kuruluşunuz şunları yapmanız gerekebilir:

* [Cihazınızı şifreleme](#encrypt-device)
* [Güvenli başlatmayı etkinleştir](#enable-secure-startup)
* [Başlangıç geçiş kodu, PIN veya diğer kimlik doğrulama yöntemi ayarlama](#set-startup-passcode)  

> [!Note]
> Huawei, vivo ve OPPO 'dan gelen belirli Android cihazları şifrelenemez. Daha fazla bilgi için bkz. [cihaz şifreli ancak uygulama aksini söylüyor](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Cihazı şifreleme

Cihazınızı şifrelemek için aşağıdaki adımları izleyin. Cihazınız birkaç kez yeniden başlayabilir. Şifreleme seçeneğinin adı ve konumu, cihaz üreticinize ve Android sürümüne bağlı olarak değişir. 

1. **Ayarlar** uygulamasını başlatın.
2. İlgili ayarları bulmak için arama çubuğuna **güvenlik** veya **şifreleme** yazın.  
3. Cihazınızı şifrelemek için seçeneğe dokunun. Ekrandaki yönergeleri takip edin.  
4. İstendiğinde, bir kilit ekranı parolası, PIN veya başka bir kimlik doğrulama yöntemi (kuruluşunuz tarafından izin verildiyse) ayarlayın. 
5. Ayarları yeniden denetlemek için Şirket Portalı veya Microsoft Intune uygulamasını açın.
    * Şirket Portalı kullanıcılar: cihazınızı seçin ve **cihaz ayarlarını denetle**' ye dokunun. 
    * Microsoft Intune kullanıcılar: sayfa güncellene kadar beklemeniz gerekir, ancak bunu yaparken şifreleme durumunuz uyumlu olarak değiştirilmelidir. 

## <a name="enable-secure-startup"></a>Güvenli başlatmayı etkinleştir

Kuruluşunuz, *güvenli başlatmayı*etkinleştirmenizi gerektirebilir. Güvenli başlatma, cihazın her açılışında bir parola veya PIN isteyerek cihazınızı korur. Kuruluşunuzun izin verdiği seçeneğe bağlı olarak kullanabileceğiniz diğer kimlik doğrulama seçenekleri olabilir. 

Güvenli Başlatma seçeneğinin adı ve konumu, cihaz üreticinize ve Android sürümüne göre de değişir. Bazı cihazlarda, bu ayar **güçlü koruma**olarak adlandırılır. 

1. **Ayarlar** uygulamasını başlatın.
2. Uygulamanın arama çubuğunda **güvenli başlangıç** yazın.
3. Cihaz açıldığında **güvenli başlatma**  >  **PIN gerektir**' e dokunun.
4. İstendiğinde, cihazınızın PIN 'inizi girin.   
5. Ayarları yeniden denetlemek için Şirket Portalı veya Microsoft Intune uygulamasını açın.
    * Şirket Portalı kullanıcılar: cihazınızı seçin ve **cihaz ayarlarını denetle**' ye dokunun. 
    * Microsoft Intune kullanıcılar: sayfa güncellene kadar beklemeniz gerekir, ancak bunu yaparken şifreleme durumunuz uyumlu olarak değiştirilmelidir.  


## <a name="set-startup-passcode"></a>Başlangıç geçiş kodunu ayarla   
Cihazınızı şifreledikten ve güvenli başlatmayı etkinleştirdikten sonra, cihazınızın PIN 'ini, parolasını veya diğer kimlik doğrulama yöntemini (kuruluşunuz tarafından izin verildiyse) ayarlamanız istenir. Bu adım, başlangıç geçiş kodu gereksinimini karşılaacaktır. 

Cihazınızda bir kilit ekranı ayarlamak veya şu anda kullandığınız türü değiştirmek için:  

1. **Ayarlar** uygulamasını başlatın.
2. Uygulamanın arama çubuğuna **ekran kilidi** yazın.
3. **Ekran kilidi türü**' ne dokunun.
4. Kullanmak istediğiniz ekran kilidi türüne dokunun ve onaylamak için ekrandaki yönergeleri izleyin.  

## <a name="troubleshoot"></a>Sorun giderme    
**Sorun**: şifreleme düğmesi devre dışı bırakıldı.   

**Deneyebileceğiniz şey**: 
* Cihazınızın tam olarak ücretlendirildiği ve fişe takılı olduğundan emin olun. Şifreleme biraz zaman alabilir ve tam bir pil gerektirir.   

**Sorun**: hala cihazınızı şifrelemeniz gerektiğini söyleyen bir ileti görürsünüz.  

**Deneyebileceğiniz şeyler**:
   *  Cihazınızda [bir kilit ekranı ayarlayın](#set-startup-passcode) . 
   * [Güvenli başlatmayı etkinleştirin](#enable-secure-startup).

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek birimine başvurun (iletişim bilgileri için [Şirket Portalı web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın) veya <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android ekibine</a> yazın.  
