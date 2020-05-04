---
title: Intune için Android cihazını şifreleme | Microsoft Docs
description: Intune için gerektiğinde Android cihaz şifrelemesini açma adımları
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
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
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696270"
---
# <a name="encrypting-your-android-device"></a>Android cihazınızı şifreleme

Cihazınız kaybolur veya çalınırsa, cihaz şifreleme, dosyalarınızı ve klasörlerinizi yetkisiz erişimden korur. Bu, cihazınızdaki verilerin geçiş kodu olmayan kişiler tarafından erişilemez ve okunamaz olmasını sağlar. 

Okul veya iş kaynaklarına erişebilmek için kuruluşunuz şunları yapmanız gerekebilir:

* [Cihazınızı şifreleme](#encrypt-device)
* [Güvenli başlatmayı etkinleştir](#enable-secure-startup)
* [Başlangıç geçiş kodu, PIN veya diğer kimlik doğrulama yöntemi ayarlama](#set-startup-passcode)  

> [!Note]
> Huawei, vivo ve OPPO 'dan gelen belirli Android cihazları şifrelenemez. Daha fazla bilgi için bkz. [cihaz şifreli ancak uygulama aksini söylüyor](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Cihazı şifreleme

Cihazınızı şifrelemek için aşağıdaki adımları izleyin. Cihazınız birkaç kez yeniden başlayabilir. 

Şifreleme seçeneğinin adı ve konumu, cihaz üreticinize ve Android sürümüne bağlı olarak değişir. 

1. **Ayarlar** uygulamasını başlatın.
2. İlgili ayarları bulmak için uygulamanın arama çubuğuna **güvenlik** veya **şifreleme** yazın.
3. Cihazınızı şifrelemek için seçeneğe dokunun. Ekrandaki yönergeleri takip edin.  
4. İstendiğinde, bir kilit ekranı parolası, PIN veya başka bir kimlik doğrulama yöntemi (kuruluşunuz tarafından izin verildiyse) ayarlayın. 
5. Ayarları yeniden denetlemek için Şirket Portalı veya Microsoft Intune uygulamasını açın.
    * Şirket Portalı kullanıcılar: cihazınızı seçin ve **cihaz ayarlarını denetle**' ye dokunun. 
    * Microsoft Intune kullanıcılar: sayfa güncellene kadar beklemeniz gerekir, ancak bunu yaparken şifreleme durumunuz uyumlu olarak değiştirilmelidir. 

## <a name="enable-secure-startup"></a>Güvenli başlatmayı etkinleştir

Kuruluşunuz, şifreleme ilkelerinin bir parçası olarak güvenli başlatmayı etkinleştirmenizi isteyebilir. Bu özellik, telefon başlamadan önce bir parola veya PIN girilmesini isteyerek cihazınızı daha da korur. Birçok ek kimlik doğrulama seçeneğiniz vardır ancak kuruluşunuzun izin verdiği seçeneğe göre farklılık gösterir. 

Güvenli Başlatma seçeneğinin adı ve konumu, cihaz üreticinize ve Android sürümüne bağlı olarak değişir. Bazı cihazlarda bu ayar **güçlü koruma**olarak adlandırılabilir. 

1. **Ayarlar** uygulamasını başlatın.
2. Uygulamanın arama çubuğunda **güvenli başlangıç** yazın.
3. Cihaz açıldığında **güvenli başlatma** > **PIN gerektir**' e dokunun.
4. İstendiğinde, cihazınızın PIN 'inizi girin.   
5. Ayarları yeniden denetlemek için Şirket Portalı veya Microsoft Intune uygulamasını açın.
    * Şirket Portalı kullanıcılar: cihazınızı seçin ve **cihaz ayarlarını denetle**' ye dokunun. 
    * Microsoft Intune kullanıcılar: sayfa güncellene kadar beklemeniz gerekir, ancak bunu yaparken şifreleme durumunuz uyumlu olarak değiştirilmelidir.  


## <a name="set-startup-passcode"></a>Başlangıç geçiş kodunu ayarla   
[Cihazınızı şifreleyip](#encrypt-device) [güvenli başlatmayı etkinleştirdiğinizde](#enable-secure-startup), cihazınızın PIN 'ini, parolasını veya diğer kimlik doğrulama yöntemini (kuruluşunuz tarafından izin verildiyse) ayarlamanız istenir. Başka bir adım gerekmez. 

Kilit ekranı türünü seçmek veya değiştirmek için:

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
