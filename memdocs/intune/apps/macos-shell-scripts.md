---
title: Microsoft Intune adresindeki macOS cihazlarında kabuk betikleri kullanın | Microsoft Docs
description: Microsoft Intune 'de macOS cihazları için kabuk betikleri oluşturun, atayın, izleyin ve sorun giderin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
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
ms.openlocfilehash: c8d290e038529a85a01de3bdb890b9f131ef8442
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83430042"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune"></a>Intune 'da macOS cihazlarında kabuk betikleri kullanma

Intune 'da, macOS işletim sisteminin desteklendiklerinin ötesinde cihaz yönetim özelliklerini genişletmek için kabuk betikleri kullanın. 

## <a name="prerequisites"></a>Ön koşullar
Kabuk betikleri oluştururken ve bunları macOS cihazlarına atarken aşağıdaki önkoşulların karşılandığından emin olun. 
 - Cihazlar macOS 10,12 veya üstünü çalıştırıyor.
 - Cihazlar, Intune tarafından yönetilir. 
 - Kabuk betikleri ile başlar `#!` ve, veya gibi geçerli bir konumda olmalıdır `#!/bin/sh` `#!/usr/bin/env zsh` .
 - Uygulanabilir kabuklar için komut satırı yorumlayıcıları yüklenir.

## <a name="important-considerations-before-using-shell-scripts"></a>Kabuk betikleri kullanmadan önce önemli noktalar
 - Kabuk betikleri, Microsoft Intune yönetim aracısının macOS cihazında başarıyla yüklenmesini gerektirir. Daha fazla bilgi için bkz. [macOS için yönetim aracısı Microsoft Intune](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Kabuk betikleri cihazlarda ayrı süreçler olarak paralel çalışır.
 - Oturum açmış kullanıcı olarak çalıştırılan kabuk betikleri, çalıştırma sırasında cihazdaki tüm oturum açmış kullanıcı hesapları için çalıştırılır.
 - Bir son kullanıcının, oturum açmış bir kullanıcı olarak çalışan betikleri yürütmek için cihazda oturum açması gerekir.
 - Komut dosyası standart bir kullanıcı hesabının değişiklik yapmasını gerektiriyorsa kök kullanıcı ayrıcalıkları gerekir.
 - Kabuk betikleri, diskin dolu olması gibi belirli koşullar için seçilen betik sıklığından daha sık çalıştırmayı dener. Örneğin, depolama konumu ile oynanmışsa, yerel önbellek silinirse veya Mac cihazı yeniden başlatılırsa.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Kabuk betik ilkesi oluşturma ve atama
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **MacOS**  >  **betikleri**  >  **Ekle**' yi seçin.
3. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin ve **İleri**' yi seçin:
   - **Ad**: kabuk betiği için bir ad girin.
   - **Açıklama**: kabuk betiği için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
4. **Betik ayarları**' nda aşağıdaki özellikleri girin ve **İleri**' yi seçin:
   - **Betiği karşıya yükle**: kabuk betiğine gidin. Betik dosyası boyutu 200 KB 'tan az olmalıdır.
   - **Betiği oturum açmış kullanıcı olarak çalıştır**: betiği kullanıcının cihazdaki kimlik bilgileriyle çalıştırmak için **Evet** ' i seçin. Betiği kök kullanıcı olarak çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin. 
   - **Cihazlarda betik bildirimlerini gizle:** Varsayılan olarak, komut dosyası bildirimleri çalıştırılan her komut için gösterilir. Son kullanıcılar, macOS cihazlarında Intune 'dan *bilgisayar bildirimini yapılandırıyor* .
   - **Betik sıklığı:** Betiğin ne sıklıkla çalıştırılacağını seçin. Bir betiği yalnızca bir kez çalıştırmak için **Yapılandırılmadı** (varsayılan) seçeneğini belirleyin.
   - **Betik başarısız olursa en fazla yeniden deneme sayısı:** Sıfır olmayan bir çıkış kodu döndürürse betiğin kaç kez çalışacağını seçin (sıfır başarı anlamına gelir). Bir komut dosyası başarısız olduğunda yeniden denenmemelidir **(varsayılan** ) seçeneğini belirleyin.
5. **Kapsam etiketleri**' nde, isteğe bağlı olarak betik için kapsam etiketleri ekleyin ve **İleri**' yi seçin. Intune 'da betikleri kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).
6. **Atamaları**seçin  >  **dahil edilecek grupları seçin**. Mevcut bir Azure AD grupları listesi gösteriliyor. Betiği alacak bir veya daha fazla Kullanıcı veya cihaz grubu seçin. **Seç**’i seçin. Seçtiğiniz gruplar listede gösterilir ve betik ilkenize gönderilir.
   > [!NOTE]
   > - Kullanıcı gruplarına atanan kabuk betikleri, Mac 'te oturum açan tüm kullanıcılar için geçerlidir.  
   > - Kabuk betikleri için atamaları güncelleştirme, [macOS için MICROSOFT INTUNE MDM aracısına](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos)yönelik atamaları da güncelleştirir.

7. **İnceleme + Ekle**' de, yapılandırdığınız ayarların bir özeti gösterilir. Betiği kaydetmek için **Ekle** ' yi seçin. **Ekle**' yi seçtiğinizde, komut dosyası ilkesi seçtiğiniz gruplara dağıtılır.

Oluşturduğunuz betik artık betikler listesinde görünür. 

## <a name="monitor-a-shell-script-policy"></a>Kabuk betik ilkesini izleme
Aşağıdaki raporlardan birini seçerek, kullanıcılar ve cihazlar için atanan tüm betiklerin çalışma durumunu izleyebilirsiniz:
- **Betikler**  >  **izlenecek**  >  betiği seçin **Cihaz durumu**
- **Betikler**  >  **izlenecek**  >  betiği seçin **Kullanıcı durumu**

>[!IMPORTANT]
> Seçilen **betik sıklığından**bağımsız olarak, komut dosyası çalıştırma durumu yalnızca bir komut dosyası ilk kez çalıştırıldığında raporlanır. Betik çalıştırma durumu sonraki çalışmalarda güncelleştirilmedi. Ancak, güncelleştirilmiş betikler yeni komut dosyaları olarak kabul edilir ve çalışma durumunu yeniden rapor eder.

Bir komut dosyası çalıştıktan sonra, aşağıdaki durumlardan birini döndürür:
- Betik çalıştırma durumu **başarısız oldu** , betiğin sıfır olmayan bir çıkış kodu döndürmediğini veya betiğin yanlış biçimli olduğunu gösterir. 
- Işlemin betiği çalıştırma durumu, betiğin çıkış kodu olarak sıfır döndürdüğünden emin **oldu** . 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Günlük toplama kullanarak macOS kabuğu betik ilkelerine sorun giderme

MacOS cihazlarındaki betik sorunlarını gidermeye yardımcı olmak için cihaz günlüklerini toplayabilirsiniz. 

### <a name="requirements-for-log-collection"></a>Günlük toplama gereksinimleri
MacOS cihazında günlüklerin toplanması için aşağıdaki öğeler gereklidir:
- Tam mutlak günlük dosyası yolunu belirtmeniz gerekir.
- Dosya yollarının yalnızca noktalı virgül (;) ile ayrılması gerekir.
- Karşıya yüklenecek en fazla günlük toplama boyutu 60 MB (sıkıştırılmış) veya 25 dosya (hangisi önce gerçekleşirse).
- Günlük toplama için izin verilen dosya türleri şu uzantıları içerir: *. log,. zip,. gz,. tar,. txt,. xml,. kilitlenme,. rtf*

#### <a name="collect-device-logs"></a>Cihaz günlüklerini toplama
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz durumu** veya **Kullanıcı durumu** raporu ' nda bir cihaz seçin.
3. **Günlükleri topla**' yı seçin, günlük dosyalarının klasör yollarını yalnızca noktalı virgülle ayırarak belirtin (;) yollar arasında boşluk veya newlines olmadan.<br>Örneğin, birden çok yolun olarak yazılması gerekir `/Path/to/logfile1.zip;/Path/to/logfile2.log` . 

   >[!IMPORTANT]
   > Boşluk ile veya boşluk olmadan tırnak işareti, nokta, yeni satır veya tırnak işaretleri kullanılarak ayrılan birden çok günlük dosyası yolu, günlük toplama hatasına neden olur. Boşluklar, yollar arasında ayırıcı olarak da kullanılamaz.

4. **Tamam**’ı seçin. Günlükler, cihaz üzerinde Intune yönetim aracısının Intune ile birlikte denetleyeceği bir sonraki sefer toplanır. Bu iade genellikle her 8 saatte bir gerçekleşir.

   >[!NOTE]
   > 
   > - Toplanan Günlükler cihazda şifrelenir, aktarılan ve 30 gün boyunca Microsoft Azure depolama alanında depolanır. Depolanmış günlüklerin, isteğe bağlı olarak şifresi çözülür ve Microsoft Endpoint Manager Yönetim Merkezi kullanılarak indirilir.
   > - Yönetici tarafından belirtilen günlüklere ek olarak, Intune Yönetim Aracısı günlükleri de şu klasörlerden toplanır: `/Library/Logs/Microsoft/Intune` ve `~/Library/Logs/Microsoft/Intune` . Aracı günlük dosyası adları `IntuneMDMDaemon date--time.log` ve ' dir `IntuneMDMAgent date--time.log` . 
   > - Herhangi bir yönetici tarafından belirtilen dosya eksikse veya dosya uzantısı yanlış ise, ' de listelenen bu dosya adlarını görürsünüz `LogCollectionInfo.txt` .     

### <a name="log-collection-errors"></a>Günlük toplama hataları
Aşağıdaki tabloda belirtilen nedenlerden herhangi biri nedeniyle günlük koleksiyonu başarılı olmayabilir. Bu hataları gidermek için düzeltme adımlarını izleyin.

| Hata kodu (onaltılık) | Hata kodu (Dec) | Hata iletisi | Düzeltme adımları |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Günlük dosyası boyutu 60 MB 'ı aşamaz. | Sıkıştırılmış günlüklerin boyutunun 60 MB 'tan az olduğundan emin olun. |
| 0X87D300D1 | 2016214831 | Belirtilen günlük dosyası yolu mevcut olmalıdır. Sistem Kullanıcı klasörü, günlük dosyaları için geçersiz bir konum. | Belirtilen dosya yolunun geçerli ve erişilebilir olduğundan emin olun. |
| 0X87D300D2 | 2016214830 | Karşıya yükleme URL 'sinin süre sonu nedeniyle günlük toplama dosyası karşıya yüklenemedi. | **Günlükleri topla** eylemini yeniden deneyin. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Günlük toplama dosyası yükleme, şifreleme hatası nedeniyle başarısız oldu. Günlüğü karşıya yüklemeyi yeniden deneyin. | **Günlükleri topla** eylemini yeniden deneyin. |
| | 2016214828 | Günlük dosyası sayısı 25 dosya için izin verilen sınırı aştı. | Tek seferde en fazla 25 günlük dosyası toplanabilir. |
| 0X87D300D6 | 2016214826 | Günlük toplama dosyası karşıya yükleme, ZIP hatası nedeniyle başarısız oldu. Günlüğü karşıya yüklemeyi yeniden deneyin. | **Günlükleri topla** eylemini yeniden deneyin. |
| | 2016214740 | Sıkıştırılmış Günlükler bulunamadığı için Günlükler şifrelenmedi. | **Günlükleri topla** eylemini yeniden deneyin. |
| | 2016214739 | Günlükler toplandı, ancak depolanamadı. | **Günlükleri topla** eylemini yeniden deneyin. |

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Neden kabuk betikleri cihazda çalışmıyor?
Birkaç nedenden dolayı şunlar olabilir:
* Aracının yeni veya güncelleştirilmiş betikleri alması için iade etme gerekebilir. Bu iade süreci her 8 saatte bir gerçekleşir ve MDM iadeden farklıdır. Cihazın açık olduğundan ve başarılı bir aracı iade etme işlemi için bir ağa bağlı olduğundan emin olun ve aracının iade olmasını bekleyin. Ayrıca son kullanıcıyı Mac üzerinde Şirket Portalı açmasını isteyebilir, cihazı seçip **ayarları denetle**' ye tıklayın.
* Aracı yüklenmemiş olabilir. Aracının macOS cihazında yüklü olduğundan emin olun `/Library/Intune/Microsoft Intune Agent.app` .
* Aracı sağlıklı bir durumda olmayabilir. Aracı 24 saat boyunca kurtarmayı dener, kendisini kaldırır ve kabuk betikleri hala atanmışsa yeniden yükler.

### <a name="how-frequently-is-script-run-status-reported"></a>Betik çalıştırma durumu ne sıklıkta raporlanır?
Betik çalıştırma durumu, komut dosyası çalıştırması tamamlandıktan hemen sonra Microsoft Endpoint Manager Yönetici Konsolu 'na bildirilir. Bir betik bir ayarlama sıklığında düzenli olarak çalışacak şekilde zamanlanırsa, yalnızca ilk çalıştırıldığında durumu bildirir.

### <a name="when-are-shell-scripts-run-again"></a>Kabuk betikleri ne zaman yeniden çalıştırılır?
Betiği yalnızca, **komut dosyası başarısız olursa en fazla yeniden deneme sayısı** ayarı yapılandırılmışsa ve betik çalıştırmada başarısız olursa, bir komut dosyası yeniden çalıştırılır. Komut dosyası başarısız olursa ve bir betik çalıştırmada başarısız olursa **en fazla yeniden deneme sayısı** yapılandırılmamışsa, yeniden çalıştırılmaz ve çalıştırma durumu **başarısız**olarak bildirilir. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Kabuk betikleri için hangi Intune rolü izinleri gereklidir?
Atanmış Intune rolünüz, kabuk betiklerini silmek, atamak, oluşturmak, güncelleştirmek veya okumak için **cihaz yapılandırması** izinleri gerektirir.

## <a name="microsoft-intune-management-agent-for-macos"></a>MacOS için Yönetim Aracısı Microsoft Intune
 ### <a name="why-is-the-agent-required"></a>Aracı neden gereklidir?
Yerel macOS işletim sistemi tarafından desteklenmeyen gelişmiş cihaz yönetimi özelliklerini etkinleştirmek için Microsoft Intune yönetim aracısının yönetilen macOS cihazlarına yüklenmesi gerekir.
 
 ### <a name="how-is-the-agent-installed"></a>Aracı nasıl yüklenir?
 Aracı, Microsoft Endpoint Manager Yönetim merkezinde en az bir kabuk betiği atadığınız Intune tarafından yönetilen macOS cihazlarına otomatik olarak ve sessizce yüklenir. Aracı, `/Library/Intune/Microsoft Intune Agent.app` uygulanabilir olduğunda yüklenir ve **Finder**  >  MacOS cihazlarındaki Bulucu**uygulamalarında** görünmez. Aracı, `IntuneMdmAgent` macOS cihazlarında çalışırken **etkinlik izleyicisinde** olarak görünür.

### <a name="what-does-the-agent-do"></a>Aracı ne yapar?
 - Aracı, macOS cihazı için atanmış kabuk betikleri almak üzere iade etmeden önce Intune hizmetleriyle sessizce kimlik doğrular.
 - Aracı atanmış kabuk betikleri alır ve yapılandırılmış zamanlama, yeniden deneme girişimleri, bildirim ayarları ve yönetici tarafından ayarlanan diğer ayarlar temelinde betikleri çalıştırır.
 - Aracı, Intune hizmetleriyle genellikle her 8 saatte bir yeni veya güncelleştirilmiş betikleri denetler. Bu iade işlemi, MDM iadeden bağımsızdır. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Bir Mac 'ten bir aracı denetimini el ile nasıl başlatabilirim?
Aracının yüklü olduğu yönetilen bir Mac üzerinde **Şirket portalı**açın, yerel cihazı seçin, **ayarları denetle**' ye tıklayın. Bu, bir MDM iadesinin yanı sıra bir aracı iade etme işlemini başlatır.

Alternatif olarak, **terminali**açın, `sudo killall IntuneMdmAgent` işlemi sonlandırmak için komutunu çalıştırın `IntuneMdmAgent` . `IntuneMdmAgent`İşlem hemen yeniden başlatılır ve bu işlem, Intune ile bir iade başlatılır.

> [!NOTE]
> Microsoft Endpoint Manager Yönetici konsolundaki cihazlar için **eşitleme** EYLEMI bir MDM iade etme işlemini başlatır ve bir aracı iade etme işlemini zorlamaz.

 ### <a name="when-is-the-agent-removed"></a>Aracı ne zaman kaldırılır?
 Aracının cihazdan kaldırılmasına neden olabilecek çeşitli koşullar vardır:
 - Kabuk betikleri artık cihaza atanmaz. 
 - MacOS cihazı artık yönetilmez.
 - Aracı, 24 saatten uzun bir süredir kurtarılabilir durumda (cihaz-uyanık süresi).

 ### <a name="why-are-scripts-running-even-though-the-mac-is-no-longer-managed"></a>Mac artık yönetilmese de betikler neden çalışıyor?
 Atanmış betiklerle bir Mac artık yönetilmediğinde, aracı hemen kaldırılmaz. Aracı, Mac 'in bir sonraki aracı iadede (genellikle her 8 saatte bir) yönetilip yönetilmediğini algılar ve zamanlanmış komut dosyası çalıştırmalarını iptal eder. Bu nedenle, bir sonraki zamanlanmış aracı iadeden daha sık çalışmak üzere zamanlanmış yerel olarak depolanmış betikler çalışır. Aracı iade etmediği zaman, 24 saate kadar iade etmeyi yeniden dener (cihaz için uyanık süresi) ve sonra kendisini Mac 'ten kaldırır.
 
 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Kabuk betikleri için Microsoft 'a gönderilen kullanım verilerini devre dışı bırakma
 Intune yönetim aracısından Microsoft 'a gönderilen kullanım verilerini devre dışı bırakmak için, Şirket Portalı açın ve **menü**  >  **tercihleri**  >  *' ne ' Microsoft kullanım verilerini toplamasına izin ver ' onay kutusunu*işaretleyin. Bu, hem aracı hem de Şirket Portalı için gönderilen kullanım verilerini devre dışı bırakır.

## <a name="known-issues"></a>Bilinen sorunlar
- **Betik çalıştırma durumu yok:** Aygıtta bir betiğin alındığı ve çalışma durumunun bildirilmesinden önce cihazın çevrimdışı olduğu olası bir olayda, cihaz yönetim konsolundaki betik için çalışma durumunu raporlamaz.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune’da uyumluluk ilkesi oluşturma](..\protect\create-compliance-policy.md)
