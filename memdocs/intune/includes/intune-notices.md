---
title: include dosyası
description: include dosyası
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183066"
---
Bu bildirimler, gelecekteki Intune değişiklik ve özelliklerine hazırlanmanıza yardımcı olabilecek önemli bilgiler sağlar.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Windows 10 Mobile bitiş için Microsoft Intune desteği<!--3544938-->
Windows 10 Mobile için Microsoft temel desteği Aralık 2019 ' de sona erdi. Bu destek bildiriminde bahsedildiği gibi, Windows 10 Mobile kullanıcıları artık yeni güvenlik güncelleştirmeleri, güvenlikle ilgili olmayan düzeltmeler, ücretsiz yardımlı destek seçenekleri veya Microsoft 'un çevrimiçi teknik içerik güncelleştirmeleri almak için uygun olmayacaktır. Microsoft Intune, tüm mobil işletim sistemi desteğine bağlı olarak, Windows 10 Mobile uygulaması için Şirket Portalı ve 10 Ağustos 2020 ' de Windows 10 Mobile Işletim sistemi için destek sona acaktır.

#### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek?
Kuruluşunuzda dağıtılmış Windows 10 Mobile cihazları varsa, şu anda ve 10 Ağustos 2020 arasında yeni cihazlar kaydedebilir, ilke ve uygulamaları ekleyebilir veya kaldırabilir ya da herhangi bir yönetim ayarını güncelleştirebilirsiniz. 10 Ağustos 'tan sonra yeni kayıtları durduracağız ve sonuç olarak Windows 10 Mobile yönetimini Intune kullanıcı arabiriminden kaldıracağız. Cihazlar artık Intune hizmetini denetmayacak ve cihaz ve ilke verilerini silecağız.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Bu değişikliğe hazırlanmak için ne yapmam gerek?
Hangi cihazların veya kullanıcıların etkilendiğini görmek için Intune raporlamayı kontrol edebilirsiniz. **Cihazlar** > **tüm cihazlar** ' a gidin ve işletim sistemine göre filtreleyin. Kuruluşunuzun Windows 10 Mobile çalıştıran cihazlara sahip olduğunu belirlemenize yardımcı olması için ek sütunlar ekleyebilirsiniz. Son kullanıcılarınızın cihazlarını yükseltmesini isteyin veya şirket erişimi için cihazları kullanmaya devam edin.


### <a name="end-of-support-for-legacy-pc-management"></a>Eski PC yönetimi için destek sonu

Eski PC yönetimi, 15 Ekim 2020 ' de destek altına geçiyor. Cihazları Windows 10 ' a yükseltin ve Intune tarafından yönetilmek üzere bunları mobil cihaz yönetimi (MDM) cihazları olarak yeniden kaydedin.

[Daha fazlasını öğrenin](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Android Cihaz Yöneticisi desteğini azaltma<!--5857738-->
Android Cihaz Yöneticisi (bazen "eski" Android yönetimi ve Android 2,2 ile kullanıma sunulan) Android cihazlarını yönetmenin bir yoludur. Ancak, geliştirilmiş yönetim işlevselliği artık [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (Android 5,0 ile yayımlanmıştır) ile kullanılabilir. Modern, daha zengin ve daha güvenli cihaz yönetimine geçiş çabasında, Google yeni Android sürümlerindeki Cihaz Yöneticisi desteğini düşürdüğünde.

#### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek?
Google tarafından yapılan bu değişiklikler nedeniyle Intune kullanıcıları aşağıdaki yollarla etkilenecektir:  
- Intune, yalnızca S2 CY2020 aracılığıyla Android 10 ve üzeri çalıştıran cihaz yönetici tarafından yönetilen Android cihazları için tam destek sağlayabilecektir. Cihaz Yöneticisi-bu süre sonunda Android 10 veya sonraki sürümleri çalıştıran yönetilen cihazlar tamamen yönetilemez. Özellikle, etkilenen cihazlar yeni parola gereksinimleri almaz.
    - Bu zaman diliminde, Intune 'un Knox platformuyla tümleştirilmesi aracılığıyla genişletilmiş destek sağlandığı için Samsung KNOX cihazları etkilenmez. Bu, daha fazla zaman Cihaz Yöneticisi yönetimi 'nin geçişini planlamak için daha fazla zaman sağlar.    
- Android 10 ' un altında kalan Android sürümlerinde kalan Cihaz Yöneticisi ile yönetilen Android cihazları etkilenmez ve cihaz yöneticisiyle tamamen yönetilmeye devam edebilir.    
- Android 10 ve üzeri çalıştıran tüm cihazlarda, Google, Şirket Portalı gibi cihaz yönetici yönetim aracılarının cihaz tanımlayıcı bilgilerine erişmesine olanak sağlar. Bu kısıtlama, bir cihaz Android 10 veya sonraki bir sürüme güncelleştirildikten sonra aşağıdaki Intune özelliklerini etkiler:  
    - VPN için ağ erişim denetimi artık çalışmayacak.   
    - Cihazların ıMEı veya seri numarası ile şirkete ait olarak tanımlanması cihazları şirkete ait olarak otomatik olarak işaretlemez.  
    - IMEı ve seri numarası artık Intune 'da BT yöneticileri için görünür olmayacaktır. 
        > [!NOTE]
        > Bu, yalnızca Android 10 ve üzeri cihazlarda cihaz yöneticisi tarafından yönetilen cihazları etkiler ve Android Enterprise olarak yönetilmekte olan cihazları etkilemez. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Bu değişikliğe hazırlanmak için ne yapmam gerek?
S3 CY2020 ' de gelen işlevselliğin azalmasını önlemek için şunları yapmanızı öneririz:
- Cihaz Yöneticisi yönetimine yeni cihaz eklemeyin.
- Bir cihazın Android 10 güncelleştirmesi alması bekleniyorsa, cihazı Cihaz Yöneticisi yönetiminden Android kurumsal yönetim ve/veya uygulama koruma ilkelerine geçirin.

#### <a name="additional-information"></a>Ek bilgiler
- [Google 'ın cihaz yöneticisinden Android kuruluşa geçiş kılavuzu](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google 'ın Cihaz Yöneticisi API 'sini kullanımdan kaldırma planına yönelik belgeleri](https://developers.google.com/android/work/device-admin-deprecation)