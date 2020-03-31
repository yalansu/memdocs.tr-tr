---
title: Microsoft Intune adresindeki macOS cihazlarında kabuk betikleri kullanın | Microsoft Docs
description: Microsoft Intune 'de macOS cihazları için kabuk betikleri oluşturun, atayın, izleyin ve sorun giderin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36936976528b5ea9c3fff1f77ec11223a4e4e63d
ms.sourcegitcommit: e7fb8cf2ffce29548b4a33b2a0c33a3a227c6bc4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80401773"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Intune 'da macOS cihazlarında kabuk betikleri kullanma (Genel Önizleme)

> [!NOTE]
> MacOS cihazları için kabuk betikleri Şu anda önizleme aşamasındadır. Bu özelliği kullanmadan önce [önizlemede bulunan bilinen sorunların](macos-shell-scripts.md#known-issues) listesini gözden geçirin.

Intune 'da, macOS işletim sisteminin desteklendiklerinin ötesinde cihaz yönetim özelliklerini genişletmek için kabuk betikleri kullanın. 

## <a name="prerequisites"></a>Önkoşullar
Kabuk betikleri oluştururken ve bunları macOS cihazlarına atarken aşağıdaki önkoşulların karşılandığından emin olun. 
 - Cihazlar macOS 10,12 veya üstünü çalıştırıyor.
 - Cihazlar, Intune tarafından yönetilir. 
 - Kabuk betikleri `#!` başlar ve `#!/bin/sh` veya `#!/usr/bin/env zsh`gibi geçerli bir konumda olmalıdır.
 - Uygulanabilir kabuklar için komut satırı yorumlayıcıları yüklenir.

## <a name="important-considerations-before-using-shell-scripts"></a>Kabuk betikleri kullanmadan önce önemli noktalar
 - Kabuk betikleri, Microsoft Intune MDM aracısının macOS cihazında başarıyla yüklenmesini gerektirir. Daha fazla bilgi için bkz. [macOS IÇIN MDM aracısı Microsoft Intune](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
 - Kabuk betikleri cihazlarda ayrı süreçler olarak paralel çalışır.
 - Oturum açmış kullanıcı olarak çalıştırılan kabuk betikleri, çalıştırma sırasında cihazdaki tüm oturum açmış kullanıcı hesapları için çalıştırılır.
 - Bir son kullanıcının, oturum açmış bir kullanıcı olarak çalışan betikleri yürütmek için cihazda oturum açması gerekir.
 - Komut dosyası standart bir kullanıcı hesabının değişiklik yapmasını gerektiriyorsa kök kullanıcı ayrıcalıkları gerekir.
 - Kabuk betikleri, diskin dolu olması gibi belirli koşullar için seçilen betik sıklığından daha sık çalıştırmayı dener. Örneğin, depolama konumu ile oynanmışsa, yerel önbellek silinirse veya Mac cihazı yeniden başlatılırsa.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Kabuk betik ilkesi oluşturma ve atama
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Ekle** > **MacOS** > **betiklerinin** > **cihazları** seçin.
3. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin ve **İleri**' yi seçin:
   - **Ad**: kabuk betiği için bir ad girin.
   - **Açıklama**: kabuk betiği için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
4. **Betik ayarları**' nda aşağıdaki özellikleri girin ve **İleri**' yi seçin:
   - **Betiği karşıya yükle**: kabuk betiğine gidin. Betik dosyası boyutu 200 KB 'tan az olmalıdır.
   - **Betiği oturum açmış kullanıcı olarak çalıştır**: betiği kullanıcının cihazdaki kimlik bilgileriyle çalıştırmak için **Evet** ' i seçin. Betiği kök kullanıcı olarak çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin. 
5. **Kapsam etiketleri**' nde, isteğe bağlı olarak betik için kapsam etiketleri ekleyin ve **İleri**' yi seçin. Intune 'da betikleri kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).
6. **Atamaları** seçin > **Eklenecek grupları**seçin. Mevcut bir Azure AD grupları listesi gösteriliyor. MacOS cihazları betiği almak için olan kullanıcıları içeren bir veya daha fazla cihaz grubu seçin. **Seçin** öğesini belirleyin. Seçtiğiniz gruplar listede gösterilir ve betik ilkenize gönderilir.
   > [!NOTE]
   > - Intune 'daki kabuk betikleri yalnızca Azure AD cihaz güvenlik gruplarına atanabilir. Önizleme aşamasında Kullanıcı grubu ataması desteklenmez. 
   > - Kabuk betikleri için atamaları güncelleştirme, [macOS için MICROSOFT INTUNE MDM aracısına](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos)yönelik atamaları da güncelleştirir.
7. **İnceleme + Ekle**' de, yapılandırdığınız ayarların bir özeti gösterilir. Betiği kaydetmek için **Ekle** ' yi seçin. **Ekle**' yi seçtiğinizde, komut dosyası ilkesi seçtiğiniz gruplara dağıtılır.

Oluşturduğunuz betik artık betikler listesinde görünür. 

## <a name="monitor-a-shell-script-policy"></a>Kabuk betik ilkesini izleme
Aşağıdaki raporlardan birini seçerek, kullanıcılar ve cihazlar için atanan tüm betiklerin çalışma durumunu izleyebilirsiniz:
- **Betikler** >  > **cihaz durumunu** **izlemek için betiği seçin**
- **Betikler** >  > **Kullanıcı durumunu** **izlemek için betiği seçin**

>[!IMPORTANT]
> Seçilen **betik sıklığından**bağımsız olarak, komut dosyası çalıştırma durumu yalnızca bir komut dosyası ilk kez çalıştırıldığında raporlanır. Betik çalıştırma durumu sonraki çalışmalarda güncelleştirilmedi. Ancak, güncelleştirilmiş betikler yeni komut dosyaları olarak kabul edilir ve çalışma durumunu yeniden rapor eder.

Bir komut dosyası çalıştıktan sonra, aşağıdaki durumlardan birini döndürür:
- Betik çalıştırma durumu **başarısız oldu** , betiğin sıfır olmayan bir çıkış kodu döndürmediğini veya betiğin yanlış biçimli olduğunu gösterir. 
- Işlemin betiği çalıştırma durumu, betiğin çıkış kodu olarak sıfır döndürdüğünden emin **oldu** . 

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Neden kabuk betikleri cihazda çalışmıyor?
Birkaç nedenden dolayı şunlar olabilir:
* Aracının yeni veya güncelleştirilmiş betikleri alması için iade etme gerekebilir. Bu iade süreci her 8 saatte bir gerçekleşir ve MDM iadeden farklıdır. Cihazın açık olduğundan ve başarılı bir aracı iade etme işlemi için bir ağa bağlı olduğundan emin olun ve aracının iade olmasını bekleyin.
* Aracı yüklenmemiş olabilir. Aracının macOS cihazında `/Library/Intune/Microsoft Intune Agent.app` yüklenip yüklenmediğini denetleyin.
* Aracı sağlıklı bir durumda olmayabilir. Aracı 24 saat boyunca kurtarmayı dener, kendisini kaldırır ve kabuk betikleri hala atanmışsa yeniden yükler.

### <a name="how-frequently-is-script-run-status-reported"></a>Betik çalıştırma durumu ne sıklıkta raporlanır?
Betik çalıştırma durumu, komut dosyası çalıştırması tamamlandıktan hemen sonra Microsoft Endpoint Manager Yönetici Konsolu 'na bildirilir. Bir betik bir ayarlama sıklığında düzenli olarak çalışacak şekilde zamanlanırsa, yalnızca ilk çalıştırıldığında durumu bildirir.

### <a name="when-are-shell-scripts-run-again"></a>Kabuk betikleri ne zaman yeniden çalıştırılır?
Betiği yalnızca, **komut dosyası başarısız olursa en fazla yeniden deneme sayısı** ayarı yapılandırılmışsa ve betik çalıştırmada başarısız olursa, bir komut dosyası yeniden çalıştırılır. Komut dosyası başarısız olursa ve bir betik çalıştırmada başarısız olursa **en fazla yeniden deneme sayısı** yapılandırılmamışsa, yeniden çalıştırılmaz ve çalıştırma durumu **başarısız**olarak bildirilir. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Kabuk betikleri için hangi Intune rolü izinleri gereklidir?
Atanmış Intune rolünüz, kabuk betiklerini silmek, atamak, oluşturmak, güncelleştirmek veya okumak için **cihaz yapılandırması** izinleri gerektirir.

## <a name="microsoft-intune-mdm-agent-for-macos"></a>MacOS için MDM Aracısı Microsoft Intune
 ### <a name="why-is-the-agent-required"></a>Aracı neden gereklidir?
 Yerel macOS işletim sistemi tarafından desteklenmeyen gelişmiş cihaz yönetimi özelliklerini etkinleştirmek için, Microsoft Intune MDM aracısının yönetilen macOS cihazlarına yüklenmesi gerekir.
 
 ### <a name="how-is-the-agent-installed"></a>Aracı nasıl yüklenir?
 Aracı, Microsoft Endpoint Manager Yönetim merkezinde en az bir kabuk betiği atadığınız Intune tarafından yönetilen macOS cihazlarına otomatik olarak ve sessizce yüklenir. Aracı, uygulanabilir olduğunda `/Library/Intune/Microsoft Intune Agent.app` yüklenir ve macOS cihazlarındaki **Finder** > **uygulamalarda** görünmez. Aracı, macOS cihazlarında çalışırken **etkinlik Izleyicisinde** `IntuneMdmAgent` olarak görünür.

### <a name="what-does-the-agent-do"></a>Aracı ne yapar?
 - Aracı, macOS cihazı için atanmış kabuk betikleri almak üzere iade etmeden önce Intune hizmetleriyle sessizce kimlik doğrular.
 - Aracı atanmış kabuk betikleri alır ve yapılandırılmış zamanlama, yeniden deneme girişimleri, bildirim ayarları ve yönetici tarafından ayarlanan diğer ayarlar temelinde betikleri çalıştırır.
 - Aracı, Intune hizmetleriyle genellikle her 8 saatte bir yeni veya güncelleştirilmiş betikleri denetler. Bu iade işlemi, MDM iadeden bağımsızdır. 

 >[!NOTE]
 > Şirket Portalı **ayarları denetle** EYLEMI yalnızca MDM iadelerini zorlar. Aracı iade etme işlemi için el ile gerçekleştirilen eylem yok.

 ### <a name="when-is-the-agent-removed"></a>Aracı ne zaman kaldırılır?
 Aracının cihazdan kaldırılmasına neden olabilecek çeşitli koşullar vardır:
 - Kabuk betikleri artık cihaza atanmaz. 
 - MacOS cihazı artık yönetilmez.
 - Aracı, 24 saatten uzun bir süredir kurtarılabilir durumda (cihaz-uyanık süresi).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Kabuk betikleri için Microsoft 'a gönderilen kullanım verilerini devre dışı bırakma
 Intune MDM aracısından Microsoft 'a gönderilen kullanım verilerini devre dışı bırakmak için Şirket Portalı açın ve **menü** > **tercihleri** ' ni seçin >  *' Microsoft 'un kullanım verilerini toplamasına izin ver ' seçeneğinin işaretini kaldırın*. Bu, hem Intune MDM Aracısı hem de Şirket Portalı için gönderilen kullanım verilerini devre dışı bırakır.

## <a name="known-issues"></a>Bilinen sorunlar
- **Kullanıcı grubu ataması:** Kullanıcı gruplarına atanan kabuk betikleri cihazlara uygulanmaz. Kullanıcı grubu ataması Şu anda önizlemede desteklenmiyor. Betik atamak için cihaz grubu atamasını kullanın.
- **Günlükleri topla:** "Günlükleri topla" eylemi görünür. Ancak günlük toplama denendiğinde, "bir hata oluştu" ve günlükleri yakalamaz. Günlük koleksiyonu şu anda önizlemede desteklenmiyor.
- **Betik çalıştırma durumu yok:** Aygıtta bir betiğin alındığı ve çalışma durumunun bildirilmesinden önce cihazın çevrimdışı olduğu olası bir olayda, cihaz yönetim konsolundaki betik için çalışma durumunu raporlamaz.
- **Kullanıcı durumu raporu:** Boş bir rapor sorunu var. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) **izleyici**' yi seçin. Kullanıcı durumu boş bir rapor gösterir.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune bir uyumluluk ilkesi oluşturma](..\protect\create-compliance-policy.md)
