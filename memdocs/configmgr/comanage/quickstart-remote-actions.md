---
title: Ortak yönetim ile uzak eylemler
titleSuffix: Configuration Manager
description: Ortak yönetilen cihazlar için Intune 'da uzak eylemleri çalıştırma
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075328"
---
# <a name="remote-actions-with-co-management"></a>Ortak yönetim ile uzak eylemler

Yönettiğiniz her cihazın, nerede olduğu, her bağlandığında emin olmak için erişilebilir olduğundan emin olmanız gerekir. Ayrıca, her kullanıcıya, uygulamaları ve verileri korurken üretken kalmak için ihtiyaç duydukları her şeyi sağlamanız gerekir. Intune tarafından desteklenen cihaz eylemleri sayesinde, bu kritik işlevleri uzaktan çözebilirsiniz.

Aşağıdaki videoda, sorumlu Program Yöneticisi Heidi Cheng ve Kıdemli Program Yöneticisi, ortak yönetim ile uzak eylemleri tartışır ve demo olarak uzaktan eylemler oluşturun:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Avantajlar

Uzak cihaz eylemleri, kişisel verilerle kesintiye uğramadan cihazda yönetim denetimleri sağlar. Bu uzak cihaz eylemleri şunları yapmanıza olanak sağlar: 
- Kaybolan veya çalınan cihazlarda şirket verilerini silme  
- Bir cihazı yeniden adlandırma  
- Cihazı yeniden başlatma  
- Cihaz envanterini gözden geçirme  
- Bir cihazı uzaktan denetleme  
- Önceden yüklenmiş OEM uygulamalarını baştan başlayarak temizleme yeniden başlatma  
- Herhangi bir Windows 10 cihazında fabrika sıfırlaması yapın  

Bu işlevler, e-posta veya OneDrive 'A bakılmaksızın bu cihazlarda depolanan kurumsal verileri korumanın önemli ve basit bir yoludur.

Bu eylemler hakkında daha fazla bilgi için bkz. [kullanılabilir uzak eylemler](#available-remote-actions). 



## <a name="case-studies"></a>Örnek olay incelemeleri

Küresel danışmanlık firması Avanade düzenli olarak, 30.000 çalışanları tarafından kullanılan cihazları yönetmek için uzak eylemleri kullanır. Yeni bir [blog gönderisine](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), AVANAıN CIO, belirtilen:

> *Intune işlevselliğine sahip olmanın hemen ardından, bir makinede Windows 'u uzaktan sıfırlama yeteneği vardı. Bu, son derece mobil iş gücümüzde daha yaygın olan kayıp veya çalınmış makineler için bizim için önemlidir.* 
>  *Bu, başka türlü özel bir ConfigMgr paketinde derlemek ve bakımını yapmak zorunda kaldığımız işlevsellikdir.*

Bu uzak eylemlerin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [kullanılabilir cihaz eylemleri](../../intune/remote-actions/device-management.md#available-device-actions).


## <a name="value-proposition"></a>Değer teklifi

Bir Configuration Manager cihaz birlikte yönetildiğinde, Configuration Manager yerel olarak sahip olmayan bu işlevleri hemen ekler. Artık Intune tarafından desteklenen herhangi bir uzak eylemi yapabilirsiniz. 

Ortak yönetim sayesinde Configuration Manager cihazları artık diğer Intune tarafından yönetilen tüm cihazlarda olduğu gibi. Örneğin, bulutta tam bir varlığına sahiptir ve internet erişimi olduğu sürece bunlara ulaşabilirsiniz. Bu eylemlerin tümünü, ortak yönetimi etkinleştirmenin ötesinde hiçbir ek adım uygulamadan yapabilirsiniz.

Otomatik kayıt işlemi kullanıcı tarafından saydam olduğundan, verimliliğine hiçbir etkisi yoktur. Kullanıcının herhangi bir şey yapması gerekmez.


### <a name="available-remote-actions"></a>Kullanılabilir uzak eylemler

Configuration Manager içinde [ortak yönetimi etkinleştirdikten](how-to-enable.md) sonra bu uzak eylemleri Intune 'dan kullanın.

#### <a name="remove-devices"></a>Cihazları kaldırma
- **Devre dışı bırak**: Bu eylem, söz konusu cihaza atanmış yönetilen uygulamaları ve verileri (uygun olduğunda), ayarlarını ve e-posta profillerini kaldırır. Cihaz daha sonra Intune yönetiminden kaldırılır. Bu işlem, cihazın bir sonraki denetlemesi sırasında gerçekleşir ve uzaktan devre dışı bırakma eylemini alır. Devre dışı bırakma işlevi, kullanıcının kişisel verilerini cihazda bırakır.  

- **Temizleme**: Bu eylem, bir cihazı fabrika varsayılan ayarlarına geri yükler. **Kayıt durumunu ve Kullanıcı hesabını tutma**seçeneğini belirlerseniz, Kullanıcı verileri tutulur. Aksi halde sürücü güvenli bir şekilde silinir.  

- **Sil**: Azure Portal Intune 'dan cihazları kaldırmak istiyorsanız, ilgili cihaz bölmesinden silin. Cihaz bir dahaki sefer iade ettiğinde, üzerinde depolanan tüm kurumsal verileri kaldırır.  

Daha fazla bilgi için bkz. [cihazı silme, devre dışı bırakma veya el ile silmeyi kaldırma kullanarak cihazları kaldırma](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Seçmeli temizleme
<!--SCCMDocs issue 973-->
Bir **uygulamayı seçmeli silme**seçtiğinizde, kişisel verileri kaldırmadan şirket uygulama verilerini kaldırır. Bir cihaz kayıp veya çalınmış olarak bildirildiğinde bu eylemi kullanın. 

Daha fazla bilgi için bkz. [Intune tarafından yönetilen uygulamalardan yalnızca şirket verilerini temizleme] (.. /.. /Intune/Apps/Apps-Selective-Wipe.exe.

#### <a name="sync"></a>Sync
Cihazı **Eşitle** eylemi, seçili cihazı Intune’a hemen giriş yapmaya zorlar. Bir cihaz iade edildiğinde, kendisine atadığınız bekleyen eylemleri veya ilkeleri hemen alır.

Bu özellik, atadığınız ilkeleri bir sonraki zamanlanmış iadeyi beklemeden anında doğrulamanızı ve sorunlarını gidermenize yardımcı olabilir.

Daha fazla bilgi için bkz. [Intune ile en son ilkeleri ve eylemleri almak için cihazları eşitleme](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Yeniden Başlatma
Cihazı **Yeniden Başlat** eylemi, seçtiğiniz cihazın yeniden başlatılmasını sağlar. Bu eylem, bekleyen bir yeniden başlatma işlemi olduğunda faydalıdır, ancak kullanıcı bunu yapmak için kullanılabilir değildir.

Daha fazla bilgi için bkz. [Intune ile cihazları uzaktan yeniden başlatma](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Yeni Başlangıç
**Yeni başlangıç** cihaz eylemi, Windows 10, sürüm 1703 veya sonraki sürümleri çalıştıran bir cihazda yüklü tüm uygulamaları kaldırır. Yeni başlatma, genellikle yeni bir cihazla yüklenen önceden yüklenmiş (OEM) uygulamaların kaldırılmasına yardımcı olur.

Kullanıcı verilerini korumamalıdır ' ı seçerseniz, cihaz hazır durumuna geri yükler. Azure AD ve MDM 'den kaydını kaldırır.

Cihazda hangi uygulamaların olması gerektiğine ilişkin önceden tanımlı standartlarınız varsa, bu eylem ölçütlerinizi karşılamayan olanları ortadan kaldırır.

Daha fazla bilgi için bkz. [Windows 10 cihazlarını Intune ile sıfırlamak Için yeni başlangıç kullanma](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Uzaktan denetim
Intune tarafından yönetilen cihazlar [TeamViewer](https://www.teamviewer.com/) kullanarak uzaktan yönetilebilir. TeamViewer, ayrı olarak elde ettiğiniz üçüncü taraf bir programdır.

Daha fazla bilgi için bkz. [Intune cihazlarını uzaktan yönetmek Için TeamViewer kullanma](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Yapılandırma

TeamViewer aracılığıyla uzak denetim dışında, bu uzak cihaz eylemlerini Intune 'da kullanmaya başlamak için, [ortak yönetimi etkinleştirdikten](how-to-enable.md)sonra ek kurulum gerekmez.

Uzaktan denetim için TeamViewer kullanma hakkında daha fazla bilgi için bkz. [Intune cihazlarını uzaktan yönetmek Için TeamViewer kullanma](../../intune/remote-actions/teamviewer-support.md).
