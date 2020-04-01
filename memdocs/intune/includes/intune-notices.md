---
title: dosya ekle
description: dosya ekle
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438724"
---
Bu bildirimler, gelecekteki Intune değişiklik ve özelliklerine hazırlanmanıza yardımcı olabilecek önemli bilgiler sağlar.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Windows 10 Mobile bitiş için Microsoft Intune desteği<!--3544938-->
Windows 10 Mobile için Microsoft temel desteği Aralık 2019 ' de sona erdi. Bu destek bildiriminde bahsedildiği gibi, Windows 10 Mobile kullanıcıları artık yeni güvenlik güncelleştirmeleri, güvenlikle ilgili olmayan düzeltmeler, ücretsiz yardımlı destek seçenekleri veya Microsoft 'un çevrimiçi teknik içerik güncelleştirmeleri almak için uygun olmayacaktır. Microsoft Intune, tüm mobil işletim sistemi desteğine göre, artık 11 Mayıs 2020 ' de Windows 10 Mobile uygulaması ve Windows 10 mobil Işletim sistemi için Şirket Portalı desteğini sona erdirmek üzere.

#### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek?
Kuruluşunuzda dağıtılmış Windows 10 Mobile cihazları varsa, şu an ve 11 Mayıs 2020 arasında yeni cihazlar kaydedebilir, ilke ve uygulamaları ekleyebilir veya kaldırabilir ya da herhangi bir yönetim ayarını güncelleştirebilirsiniz. 11 Mayıs 'tan sonra yeni kayıtları durduracağız ve sonuç olarak Windows 10 Mobile yönetimini Intune kullanıcı arabiriminden kaldıracağız. Cihazlar artık Intune hizmetini denetmayacak ve cihaz ve ilke verilerini silecağız.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Bu değişikliğe hazırlanmak için ne yapmam gerek?
Hangi cihazların veya kullanıcıların etkilendiğini görmek için Intune raporlamayı kontrol edebilirsiniz. **Tüm cihazlar** > **cihazlar** ' a gidin ve işletim sistemine göre filtreleyin. Kuruluşunuzun Windows 10 Mobile çalıştıran cihazlara sahip olduğunu belirlemenize yardımcı olması için ek sütunlar ekleyebilirsiniz. Son kullanıcılarınızın cihazlarını yükseltmesini isteyin veya şirket erişimi için cihazları kullanmaya devam edin.


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>' Intune için Adobe Acrobat Reader ' mobil uygulaması için destek özeti güncelleştirildi<!--5746776-->
Ağustos ayının sonunda MC188653 ' de paylaşıyoruz. Bu, Intune mobil uygulaması için Adobe Acrobat Reader 'ın 1 Aralık 2019 ' de sona erecek ve Adobe uygulamasının, ana Acrobat Reader uygulaması içinde Intune 'un uygulama koruma ilkelerini desteklemeyi planlıyor olması. Bundan sonra, BT yöneticilerinin hedeflemesini sağlamak için daha fazla zaman sunduğumuz ve son kullanıcıların Intune için Adobe Acrobat Reader kullanmaya başlamasını sağlayan müşteri geri bildirimi aldık. Son Kullanıcı cihazlarında Intune için Adobe Acrobat Reader 'ın yüksek kullanımı ve kurumsal senaryolarda önem derecesi verildiğinde, tüm deneyimin kuruluşunuzun uygulama koruma ihtiyaçlarını karşıladığından emin olmak istiyoruz. 

Acrobat Reader mobil uygulaması uygulama koruma Ilkelerini desteklediğinden ve Intune SDK ile tümleştirildiği için ilkelerinizde genel Acrobat Reader mobil uygulamasını hedeflemek öneriyoruz, ancak Intune için Adobe Acrobat Reader uygulaması desteklenmeye devam edecek 31 Mart 2020 tarihine kadar. 

#### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek?
Bu iletiyi, raporumuz kuruluşunuzdaki bir veya daha fazla ilkeyi Intune için Adobe Acrobat Reader uygulamasını hedeflediğinden ve/veya önceki EOL iletişimimizi almış olabilirsiniz. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Bu değişikliğe hazırlanmak için ne yapmam gerek?
Son kullanıcılarınıza ve yardım masasına bu değişikliğin haberdar olmasına izin verin. Intune ile ilgili sorulara yönelik bir kanal oluşturmak için [Şirket portalı destek bilgileri işlevselliğini](../apps/company-portal-app.md#support-information) kullanabilirsiniz.

#### <a name="additional-information"></a>Ek Bilgiler
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>Işlem yapın: korumalı Intune tarayıcı deneyiminiz için Microsoft Edge kullanın<!--5728447-->
Geçen yıl içinde paylaşım yaptığımız gibi, Microsoft Edge Mobile, çok daha iyi bir son kullanıcı deneyimi sağlarken Managed Browser aynı yönetim özellikleri kümesini destekler. Microsoft Edge 'de sunulan güçlü deneyimlere yönelik bir yöntem oluşturmak için Intune Managed Browser devre dışı bırakılacağız. 27 Ocak 2020 tarihinden itibaren Intune artık Intune Managed Browser desteklemezler.  

#### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek? 
1 Şubat 2020 ' den itibaren, Intune Managed Browser artık Google Play Store veya iOS App Store 'da kullanılamayacak. Bu noktada yeni uygulama koruma ilkelerini Intune Managed Browser hedefleyebilirsiniz, ancak yeni kullanıcılar Intune Managed Browser uygulamasını indiremezler. Ayrıca, iOS 'ta, MDM 'ye kayıtlı cihaza gönderilen yeni web klipleri Intune Managed Browser yerine Microsoft Edge 'de açılır.  

Mart 31 2020 ' de Intune Managed Browser Azure konsolundan kaldırılacak. Bu, artık Intune Managed Browser için yeni ilkeler oluşturamayacak anlamına gelir. Mevcut Intune Managed Browser ilkeleri varsa, bunlar etkilenmez. Intune Managed Browser konsolunda, hiçbir simge olmadan bir LOB uygulaması olarak görünür ve mevcut ilkeler uygulamaya hala hedeflenmiş olarak görünür. Bu noktada, uygulama koruma ilkelerinin veri koruma bölümünde yer alan Intune Managed Browser Web içeriğini yönlendirme seçeneğini de kaldıracağız.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Bu değişikliğe hazırlanmak için ne yapmam gerek? 
Intune Managed Browser Microsoft Edge 'e kesintisiz geçiş sağlamak için aşağıdaki adımları önceden gerçekleştirmeniz önerilir: 

1. İOS ve Android için Microsoft Edge 'i uygulama koruma ilkesiyle (MAM olarak da bilinir) ve uygulama yapılandırma ayarlarına hedefleyin. Mevcut ilkeleri Microsoft Edge 'de hedefleyerek Microsoft Edge için Intune Managed Browser ilkelerini yeniden kullanabilirsiniz.  
2. Ortamınızdaki tüm MAM korunan uygulamaların "diğer uygulamalarla Web içeriği aktarımını kısıtla" ayarı "Ilkeyle yönetilen tarayıcılar" olarak ayarlanmış Uygulama koruma ilkesi ayarına sahip olduğundan emin olun. 
3. Tüm MAM korumalı uygulama yapılandırma ayarı "com. Microsoft. Intune. useEdge" değeri true olarak ayarlandı. Sonraki ay 1911 sürümü ile başlayarak, uygulama koruma ilkelerinizin veri koruma bölümünde "diğer uygulamalarla Web içeriği aktarımını kısıtla" ayarını "Microsoft Edge" olarak yapılandırarak adım 2 ve 3 ' ü tek yapmanız mümkün olacaktır. . 

İOS ve Android 'de web klipleri için destek geliyor. Bu destek yayınlandığında, Managed Browser yerine Microsoft Edge 'de açıldıklarından emin olmak için önceden mevcut web kliplerini yeniden hedeflemeniz gerekir. 

#### <a name="additional-information"></a>Ek bilgiler
Daha fazla bilgi için [Microsoft Edge 'i uygulama koruma ilkeleriyle birlikte kullanarak](../apps/manage-microsoft-edge.md) belgelerimizi ziyaret edin veya [destek blog gönderimizi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269)görüntüleyin.

### <a name="end-of-support-for-legacy-pc-management"></a>Eski PC yönetimi için destek sonu

Eski PC yönetimi, 15 Ekim 2020 ' de destek altına geçiyor. Cihazları Windows 10 ' a yükseltin ve Intune tarafından yönetilmek üzere bunları mobil cihaz yönetimi (MDM) cihazları olarak yeniden kaydedin.

[Daha fazlasını öğrenin](https://go.microsoft.com/fwlink/?linkid=2107122)


