---
title: Uyumluluk ayarlarını kullanmaya başlayın
titleSuffix: Configuration Manager
description: Temel kavramlar ve uyumluluk ayarlarının nasıl çalıştığı hakkında bilgi edinin
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f0a26d02770ff8460787ee9897bdc8f1218a2c12
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506171"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Configuration Manager uyumluluk ayarları ile çalışmaya başlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager uyumluluk ayarları oluşturmadan önce temel kavramlar hakkında bilgi edinin ve bunların nasıl çalıştığını anlayın.  



## <a name="how-compliance-settings-work"></a>Uyumluluk ayarları nasıl çalışır?  
Uyumluluk ayarları, kuruluşunuzdaki istemcilerin yapılandırmasını ve uyumluluğunu yönetmenizi sağlar.  

Yapılandırma öğeleri iki ana kategoriye ayrılır:  

- Cihazı yönetmenizi sağlamak için istemci yazılımını Configuration Manager yüklediğiniz **Configuration Manager istemcisiyle yönetilen cihazlara yönelik ayarlar** .  

- **Configuration Manager istemcisi olmadan yönetilen cihazların ayarları** -genellikle Microsoft Intune veya Configuration Manager Şirket içi cihaz yönetimi ile yönetilen cihazlar.  



## <a name="what-devices-are-supported"></a>Hangi cihazlar desteklenir?  

| Cihaz Türü | Daha fazla bilgi |  
|------------|----------------------|  
| Windows bilgisayarları (Configuration Manager istemcisi ile) | Kayıt defteri anahtarları, dosyalar ve Active Directory öznitelikleri gibi nesneleri değerlendirmek için özel yapılandırma öğeleri oluşturun.<br /><br /> Windows 10 yapılandırma öğesi türünü kullandığınızda önceden tanımlanmış bir listeden Ayarlar ' ı seçin. |  
| Windows bilgisayarları (Şirket içi MDM ile kayıtlı) | Önceden tanımlanmış bir listeden Ayarlar ' ı seçin. |  
| Windows Phone cihazlar (Şirket içi MDM ile kayıtlı) | Önceden tanımlanmış bir listeden Ayarlar ' ı seçin. |  
| Mac bilgisayarlar (Configuration Manager istemcisi ile) | MacOS tercihleri ve bir komut dosyası tarafından döndürülen sonuçlar gibi nesneleri değerlendirmek için özel yapılandırma öğeleri oluşturun. |  



## <a name="what-is-a-configuration-item"></a>Yapılandırma öğesi nedir?  
Yapılandırma öğesi, belirli bilgileri depolayan bir kapsayıcıdır. Yapılandırdığınız bilgiler yapılandırma öğesi türüne bağlıdır. Yapılandırma öğeleri aşağıdaki bilgileri içerebilir:

- **Algılama yöntemi bilgileri** yalnızca uygulama ayarlarını içeren Windows yapılandırma öğeleri içindir. Uygulamanın yüklenip yüklenmediğini algılar. Bu algılama, uygulama için Windows Installer dosyasını veya özel bir komut dosyası kullanarak kullanır.  

- **Ayarlar** , istemci cihazlarındaki uyumluluğu değerlendirmek için iş veya teknik koşulları temsil eder. Yeni bir ayar yapılandırın veya referans bilgisayarındaki mevcut bir ayara gidin.  

- **Uyumluluk kuralları** , yapılandırma öğesi ayarının uyumluluğunu tanımlayan koşulları belirtir. İstemci bir ayarı uyumluluk açısından değerlendirmadan önce en az bir uyumluluk kuralına sahip olmalıdır. Bazı ayarlar uyumsuz değerleri düzeltir. Yeni kurallar oluşturun veya herhangi bir yapılandırma öğesinde var olan bir ayara gidin ve içindeki kuralları seçin.  

- **Desteklenen platformlar** , istemcinin yapılandırma öğelerinin uyumluluğunu değerlendirirken tanımladığınız cihaz platformlarıdır. Bir yapılandırma öğesini desteklenen platformlar listesinde bulunmayan bir cihaza dağıtırsanız, uyumluluk değerlendirmesi yapmaz.  



## <a name="what-is-a-configuration-baseline"></a>Yapılandırma temel çizgisi nedir?  
Değerlendirilecek yapılandırma öğelerini içeren bir yapılandırma temeli tanımlayın. Ayrıca, gerekli uyumluluk düzeyini tanımlayan ayarları ve kuralları da içerir. Bu yapılandırma verilerini Configuration Manager yapılandırma paketlerinden içeri aktarın. Microsoft ve diğer satıcılar bu yapılandırma paketlerini tanımlar. Ya da yeni yapılandırma öğeleri ve yapılandırma temelleri oluşturun.  

Bir yapılandırma temeli tanımladıktan sonra, Kullanıcı ve cihaz koleksiyonlarına dağıtın. İstemci daha sonra bir zamanlamaya göre uyumluluk için taban çizgisi ayarlarını değerlendirir. Cihazlara birden fazla yapılandırma temeli dağıtabilirsiniz. Bu ayrıntı düzeyi, uyumluluk üzerinde daha fazla denetim sağlar. 

İstemci cihazlar, dağıtılan her bir yapılandırma temeline göre uyumluluklarını değerlendirir ve durum iletileri kullanarak sonuçları siteye hemen bildirir. Bir cihazın Şu anda ağla bağlantısı kesilirse ancak yapılandırma temelini indirdiyse yapılandırma öğelerinin uyumluluğunu yine de değerlendirir. Yeniden bağlandığında uyumluluk bilgilerini gönderir.  

### <a name="monitoring-configuration-baselines"></a>Yapılandırma temelleri izleniyor
- Configuration Manager konsolundaki uyumluluk değerlendirmesinin sonuçlarını, **dağıtımlar** düğümündeki **izleme** çalışma alanı altında izleyin. Örneğin:
  - Uyumsuzluğun yaygın nedenleri
  - Hatalar
  - Etkilenen Kullanıcı ve cihaz sayısı
- Uyumluluk ayarları raporlarını ek ayrıntılarla çalıştırın. Örneğin:
  - Uyumlu veya uyumlu olmayan cihazlar
  - Yapılandırma temelinin hangi öğesi bir bilgisayarın uyumsuz olmasına neden oluyor
- Configuration Manager istemcisini çalıştıran Windows bilgisayarlarından uyumluluk değerlendirmesi sonuçlarını görüntüleyin. **Configuration Manager** Denetim Masası ' nı açın ve **Konfigürasyonlar** sekmesine geçin.  



## <a name="user-data-and-profiles-configuration-items"></a>Kullanıcı verileri ve profilleri yapılandırma öğeleri  
Kullanıcı verileri ve profilleri için yapılandırma öğeleri, Windows 8 ve sonraki sürümlerini çalıştıran bilgisayarlardaki kullanıcıların nasıl yönetileceğini denetleyen ayarları içerir:  
- Klasör yeniden yönlendirme
- Çevrimdışı dosyalar
- Dolaşım profilleri  

Bu yapılandırma öğelerini Kullanıcı koleksiyonlarına dağıtın. Configuration Manager konsolunun **izleme** düğümünden uyumluluğunu izleyin. Diğer yapılandırma öğelerinden farklı olarak, bunları dağıtmadan önce yapılandırma temellerine eklemeyin. Şeritteki **Dağıt** ' a tıklayarak bunları doğrudan dağıtın.  

Daha fazla bilgi için bkz. [Kullanıcı verileri ve profilleri yapılandırma öğeleri oluşturma](../deploy-use/create-user-data-and-profiles-configuration-items.md).  



## <a name="remote-connection-profiles"></a>Uzak bağlantı profilleri  
Uzak bağlantı profilleri, uzaktan bağlantı ayarlarını oluşturmanıza, dağıtmanıza ve izlemenize yardımcı olacak birtakım araçlar ve kaynaklar sağlar. Bu ayarları cihazlara dağıtarak, son kullanıcıların bilgisayarlarını kurumsal ağa bağlamak için ihtiyaç duyduğu çabayı en aza indirmiş olursunuz.  

Daha fazla bilgi için bkz. [uzak bağlantı profilleri oluşturma](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Windows sürüm yükseltme
Sürüm yükseltme ilkesi, belirli Windows 10 sürümlerini çalıştıran cihazları otomatik olarak yeni bir sürüme yükseltir. Bu ilke, cihazın yükseltmek için kullandığı yeni bir ürün anahtarı veya lisans dosyası sağlar.

Daha fazla bilgi için bkz [. Windows cihazlarını sürüm yükseltme Ilkesiyle yükseltme](../deploy-use/upgrade-windows-version.md)

## <a name="microsoft-edge-legacy-browser-profiles"></a>Microsoft Edge eski tarayıcı profilleri
<!-- 1357310 -->
Windows 10 istemcilerinde [Microsoft Edge eski](https://docs.microsoft.com/microsoft-edge/deploy/) Web tarayıcısını kullanan müşteriler için, tarayıcı ayarlarını yapılandırmak üzere bir Configuration Manager uyumluluk ilkesi oluşturun.

Daha fazla bilgi için bkz. [Microsoft Edge eski tarayıcı profilleri](../deploy-use/browser-profiles.md).
