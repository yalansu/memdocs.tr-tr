---
title: Windows 10 için yapılandırma öğeleri oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager istemcisi tarafından yönetilen Windows 10 bilgisayarlarının ayarlarını yönetmek için Windows 10 yapılandırma öğesini kullanın.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: ade07cf23807d340ee5e0c7955a042a44f9031c5
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240448"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Windows 10 cihazları için yapılandırma öğeleri oluşturma

Configuration Manager istemcisi tarafından yönetilen Windows 10 bilgisayarlarının ayarlarını yönetmek için **Windows 10** Configuration Manager yapılandırma öğesini kullanın.  
  
> [!IMPORTANT]  
>  Bu sürümde, **Windows 10** türündeki bir yapılandırma öğesinin parçası olarak bir **parola** ayarı oluşturduysanız (Configuration Manager istemcisiyle yönetilen bir cihaz için), aşağıdaki sorunu unutmayın. Ayar zaten mevcut değilse veya Windows 10 cihazında yapılandırılmamışsa, yanlış şekilde uyumlu olarak değerlendirilir.  
>   
>  Geçici bir çözüm olarak, bu cihazlar için bir ayar oluşturduğunuzda Yapılandırma Öğesi Oluşturma sihirbazının ayarlar sayfasında **Uyumsuz ayarları düzelt** seçeneğinin belirlendiğinden emin olun. Ayrıca, parola ayarlarını içeren bir Windows 10 yapılandırma öğesi içeren bir yapılandırma temeli dağıttığınızda, **Desteklendiğinde uyumsuz kuralları düzelt**' i seçin. Bu seçimi yapılandırma temelleri Dağıt iletişim kutusunda yaparsınız. Bu geçici çözümü kullanarak, ayar izlenir ve uyumsuz olduğu bulunursa düzeltilebilir. Düzeltmeden sonra ayar doğru şekilde **uyumlu** olarak bildirilir (bir sorunla karşılaşılmadığı sürece, bu durumda **hatayı**raporlacaktır).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Bir Windows 10 yapılandırma öğesi oluşturmak için  
  
1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**' i seçin.  
  
2. **Varlıklar ve uyum** çalışma alanında, **Uyumluluk ayarları**' nı genişletin ve **yapılandırma öğeleri**' ni seçin.  
  
3. **Giriş** sekmesinde, **Oluştur** grubunda, **yapılandırma öğesi oluştur**' u seçin.  
  
4. **Yapılandırma öğesi oluşturma** Sihirbazı ' nın **genel** sayfasında, yapılandırma öğesi için bir ad ve isteğe bağlı bir açıklama belirtin.  
  
5. **Oluşturmak istediğiniz yapılandırma öğesi türünü belirtin**bölümünün altında, **Windows 10**seçeneğini belirleyin.  
  
6. Configuration Manager konsolundaki yapılandırma öğelerini aramanıza ve filtrelemenize yardımcı olacak kategoriler oluşturup atarsanız **Kategoriler**' i seçin.  
  
7. Sihirbazın **Desteklenen Platformlar** sayfasında, yapılandırma öğesini değerlendirecek belirli Windows 10 platformlarını seçin.  
  
8. Sihirbazın **Cihaz Ayarları** sayfasında, yapılandırmak istediğiniz ayar grubunu seçin. (Ayrıntılar için bu makaledeki [Windows 10 yapılandırma öğesi ayarları başvurusu](#BKMK_Ref) ' na bakın.) Ardından **İleri**' yi seçin.  
  
   > [!TIP]  
   >  İstediğiniz ayar listelenmemişse **varsayılan ayar gruplarında olmayan ek ayarları Yapılandır onay kutusunu**seçin.  
  
9. Her ayar sayfasında, ihtiyacınız olan ayarları ve cihazlarla uyumlu olmadığında (desteklendiğinde) düzeltmek isteyip istemediğinizi yapılandırın.  
  
10. Her ayar grubu için bir yapılandırma öğesi uyumsuz olarak bulunduğunda bildirilen önem derecesini de yapılandırabilirsiniz:  
  
    -   **Hiçbiri**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için bir hata önem derecesi raporlamaz.  
  
    -   **Bilgi**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için **bilgi** hata önem derecesi raporlar.  
  
    -   **Uyarı**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için **Uyarı** hata önem derecesi raporlar.  
  
    -   **Kritik**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar.  
  
    -   **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar. Bu önem düzeyi ayrıca uygulama olay günlüğünde bir Windows olayı olarak kaydedilir.  
  
11. Sihirbazın **Platform uygulanabilirliği** sayfasında, daha önce seçtiğiniz desteklenen platformlarla uyumlu olmayan tüm ayarları gözden geçirin. Geri giderek bu ayarları kaldırabilir veya devam edebilirsiniz.  
  
    > [!TIP]  
    >  Desteklenmeyen ayarlar uyumluluk açısından değerlendirilmez.  
  
12. Sihirbazı tamamlayın.  
  
    Yeni yapılandırma öğesini, **Varlıklar ve Uyumluluk** çalışma alanındaki **Yapılandırma Öğeleri** düğümünde görüntüleyebilirsiniz.  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Parola  
  
|Ayar|Ayrıntılar|  
|-------------|-------------|  
|**Cihazlarda parola ayarlarını iste**|Desteklenen cihazlarda bir parola gerektirir.|  
|**Minimum parola uzunluğu (karakter)**|Parola için karakter cinsinden minimum uzunluk.|  
|**Gün olarak parola geçerlilik süresi**|Parolanın değiştirilmesi gerekmeden önce geçmesi gereken gün sayısı.|  
|**Anımsanan parola sayısı**|Önceki parolaların yeniden kullanılmasını önler.|  
|**Cihazın silinmesine neden olacak başarısız oturum açma girişimi sayısı**|Bu sayıda oturum açma işlemi başarısız olursa cihazı temizler.|  
|**Cihaz kilitlenmeden önce boşta geçen süre**|Otomatik olarak kilitlenmeden önce cihazın kaç dakika devre dışı olması gerektiğini belirtir.|  
|**Parola karmaşıklığı**|' 1234 ' gibi bir PIN belirtip belirtmeyeceğinizi ya da güçlü bir parola sağlamanız gerekip gerekmediğini seçin.|
|**Parolada gereken karmaşık karakter kümesi sayısı**|**Güçlü** bir parola seçtiyseniz, gereken karmaşık karakter kümesi sayısını yapılandırmak için bu ayarı kullanın. Güçlü bir parola için, bu ayar en az **3**olarak ayarlanmalıdır, bu da hem harflerin hem de sayıların gerekli olduğu anlamına gelir. Ek olarak **(% $** gibi) özel karakterler gerektiren bir parola zorlamak istiyorsanız **4** ' ü seçin.<br>(Yalnızca Windows 10)  |
  
###  <a name="device"></a>Cihaz  
  
|Ayar adı|Ayrıntılar|  
|------------------|-------------|  
|**Bluetooth**|Cihazda Bluetooth özelliğinin kullanımına izin verir.|  
  
### <a name="cloud"></a>Bulut  
  
|Ayar adı|Ayrıntılar|  
|------------------|-------------|  
|**Ayarları eşitleme**|Cihazlar arasında ayarların eşitlenmesine izin verir.|  
|**Kimlik bilgilerini eşitleme**|Cihazlar arasında kimlik bilgilerinin eşitlenmesine izin verir.|  
|**Tarifeli bağlantı üzerinden ayar eşitleme**|Internet bağlantısı tarifeli olduğunda ayarların eşitlenmesine izin verir.|  
  
### <a name="roaming"></a>Gezici  
  
|Ayar adı|Ayrıntılar|  
|------------------|-------------|  
|**Veri dolaşımı**|Verilere erişirken ağlar arasında dolaşıma izin verir.|  
  
### <a name="encryption"></a>Şifreleme  
  
|Ayar adı|Ayrıntılar|  
|------------------|-------------|  
|**Cihazda dosya şifreleme**|Cihazdaki dosyaların şifrelenmesini gerektirir.|  
  
### <a name="system-security"></a>Sistem güvenliği  
  
|Ayar adı|Ayrıntılar|  
|------------------|-------------|  
|**Kullanıcı Hesap Denetimi**|Cihazda Windows Kullanıcı Hesabı Denetimini’nin çalışmasını yapılandırır.<br />Örneğin, denetimi devre dışı bırakabilir veya size bildirim yapılacak düzeyi ayarlayabilirsiniz.|  
|**Ağ güvenlik duvarı**|Windows Güvenlik Duvarı’nı etkinleştirir veya devre dışı bırakır.|  
|**SmartScreen**|Windows SmartScreen 'i etkinleştirilir veya devre dışı bırakır.|  
|**Virüs koruması**|Virüsten koruma yazılımının yüklenmiş ve yapılandırılmış olmasını gerektirir.|  
|**Virüs koruması imzaları güncel**|Cihazdaki virüsten koruma yazılımının imza dosyalarının güncel olması gerekir.|  
  
### <a name="windows-information-protection"></a>Windows Bilgi Koruması

Kuruluştaki çalışana ait cihazların artması sayesinde, e-posta, sosyal medya ve genel bulut gibi uygulamalar ve hizmetler aracılığıyla yanlışlıkla veri sızıntılarının artması riski da vardır. Bunlar, kuruluşun denetiminin dışındadır. Çalışanların ne zaman bir çalışanı vardır:

- En son mühendislik resimlerini kişisel e-posta hesabından gönderir.
- Ürün bilgilerini kopyalar ve bir tweet öğesine yapıştırır.
- Devam eden satış raporunu genel bulut depolamaya kaydeder.

Windows Information Protection (WıP, eskiden kurumsal veri koruma) bu olası veri sızıntılarına karşı korunmaya yardımcı olur. WıP ayrıca kurumsal uygulama ve verileri, çalışanların çalışmaya getirmelerini sağlayan şirkete ait cihazlarda ve kişisel cihazlarda yanlışlıkla veri sızıntılarına karşı korumanıza yardımcı olur. WıP, ortamınızda veya diğer uygulamalarda değişiklik yapılmasını gerektirmez.

Configuration Manager Windows Information Protection yapılandırma öğeleri şunları yönetir:

- WıP tarafından korunan uygulamaların listesi
- Kurumsal ağ konumları
- Koruma düzeyi
- Şifreleme ayarları
  
WıP 'i Configuration Manager ile yapılandırma hakkında daha fazla bilgi için bkz.:

- [Windows Information Protection (WıP) kullanarak kurumsal verilerinizi koruma](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Configuration Manager kullanarak bir Windows Information Protection (WıP) ilkesi oluşturma ve dağıtma](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Windows Information Protection (WıP) kullanılırken Sınırlamalar](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Ayrıca bkz.  
[Configuration Manager istemcisiyle yönetilen cihazlar için yapılandırma öğeleri](../../compliance/deploy-use/create-configuration-items.md)
