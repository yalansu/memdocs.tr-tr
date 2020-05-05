---
title: İlke Gözetleme
titleSuffix: Configuration Manager
description: Configuration Manager istemcilerinde ilke sistemini görüntülemek ve sorunlarını gidermek için Ilke Spy kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723183"
---
# <a name="policy-spy"></a>İlke Gözetleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İlke Spy [Configuration Manager araçlarından](tools.md)biridir. Configuration Manager istemcilerinde ilke sistemini görüntülemek ve sorunlarını gidermek için bir araçtır. Kullanıcı arabirimini açmak için **Policyspy. exe** ' yi çalıştırın. Komut satırı kullanımı hakkında daha fazla bilgi için bkz. [komut satırı sözdizimi](#bkmk_policyspy-syntax).

> [!Important]  
> Ilkeyi bir yönetici olarak çalıştırın. **Yönetici olarak çalıştırmazsanız**, istemci bilgilerinde aşağıdaki hatayı görürsünüz:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a>Komut satırı sözdizimi

İlke Spy öncelikle Kullanıcı arabirimi aracılığıyla kullanılmak üzere tasarlanmıştır. Otomasyon ve toplu işlemeyi desteklemek için sınırlı komut satırı seçenekleri sağlar.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Seçeneği`/export`
Bu seçenek yerel veya uzak bilgisayarın ilkesini sessizce dışarı aktarır. `<ExportFilename>`, aracın XML olarak içe aktarılmış ilkesini kaydettiği dosya adıdır. `<computername>` Seçeneğini belirtirseniz, ilke Spy yerel bilgisayar yerine bu bilgisayarın ilkesini dışarı aktarır.

> [!Note]  
> Bu komut satırı seçeneği, Kullanıcı kimlik bilgilerini belirtmek için bir yol sağlamaz. Uzak bir bilgisayara erişmek için alternatif kimlik bilgilerini kullanmak için **runas** komutunu kullanarak gerekli güvenlik bilgileriyle yeni bir komut istemi açın.  


## <a name="usage"></a>Kullanım

### <a name="tools-menu"></a>Araçlar menüsü

**Araçlar** menüsünde aşağıdaki eylemler mevcuttur:  

- **Açık uzak**: uzak bilgisayardaki Configuration Manager istemci ilkesine bağlanır. Uzak bilgisayarın adını ve isteğe bağlı kullanıcı kimlik bilgilerini almak için Bağlan iletişim kutusunu kullanın. Bağlantı başarısız olursa, Istemci bilgileri bölmesinde hata bilgilerini görüntüler. Bağlantı yeniden başarısız olursa, **düzenleme** menüsünde **Yenile** ' yi seçerek veya F5 tuşuna basarak bağlanmayı deneyin.  

- **Dosya Aç**: **dışa aktarma ilkesi** seçeneği tarafından oluşturulan bir ilke DıŞA aktarma dosyası (XML) açar. Araç, aktarılmış ilkeyi canlı ilkeyle tam olarak aynı şekilde görüntüler. Yalnızca gerçek bir istemciye bağlandığınızda uygulanan bazı özellikleri devre dışı bırakır.  

- **Istek makinesi atamaları**: hedef bilgisayarda makine ilkesi atamaları için bir istek tetikler. Bu özellik, içe aktarılmış ilke görüntülenirken devre dışıdır.  

- **Makine Ilkesini değerlendir**: hedef bilgisayarda bir makine ilkesi değerlendirmesi tetikler. Bu özellik, dışarıya aktarılmış bir ilke görüntülenirken devre dışıdır.  

- **Kullanıcı atamalarını iste**: Şu anda oturum açmış olan kullanıcı için Kullanıcı ilkesi atamaları için bir istek tetikler. Bu özellik yalnızca yerel bilgisayarda bir ilke görüntülenirken kullanılabilir.  

- **Kullanıcı Ilkesini değerlendir**: Şu anda oturum açmış olan kullanıcı için bir Kullanıcı ilkesi değerlendirmesi tetikler. Bu özellik yalnızca yerel bilgisayarda bir ilke görüntülenirken kullanılabilir.  

- **Ilkeyi Sıfırla**: varsayılan olmayan tüm ilkeleri kaldırır ve sitenin ilke tanımlama bilgilerini sıfırlar. Daha sonra makine ilkesi atamaları için bir istek tetikler. Bu özellik, dışarıya aktarılmış bir ilke görüntülenirken devre dışıdır.  

- **Ilkeyi dışarı aktar**: hedef bilgisayarın ILKESINI bir XML dosyasına aktarır. Bu dosyayı Ilke Spy ile herhangi bir bilgisayarda görüntüleyin. Dışarı aktarma dosyasını açmak için **Araçlar** menüsünden **Dosya Aç** ' ı seçin. Bu özellik, dışarıya aktarılmış bir ilke görüntülenirken devre dışıdır.  


### <a name="edit-menu"></a>Düzenle menüsü

**Düzenleme** menüsünde aşağıdaki eylemler mevcuttur:  

- **Sil**: sonuçlar bölmesinde seçilen örneği siler. Bu eylem yalnızca ilke örnekleri için desteklenir. İlke örnekleri dışında bir şeyi silmeye çalışırsanız, araç bir hata mesajı görüntüler. Bu özellik, dışarıya aktarılmış bir ilke görüntülenirken devre dışıdır.  

- **Yenile**: en son bilgileri görüntülemek için tüm sonuçları yeniler. Yenilemeden önce genişletilen tüm ağaç düğümleri daha sonra otomatik olarak genişletilir. Ilke Spy, hedef bilgisayarın ilkesine başarıyla bağlanmamışsa, bağlanmayı yeniden dener. Bu özellik, dışarıya aktarılmış bir ilke görüntülenirken devre dışıdır.  

- **Olayları Temizle**: olaylar sekmesindeki tüm öğeleri temizler.  



## <a name="results-pane"></a>Sonuçlar bölmesi

Sonuçlar bölmesinde, hedef bilgisayardaki ilke sisteminin farklı görünümleri görüntülenir. Aşağıdaki dört sekmeden birine tıklayarak bu görünümlere erişin: 
- [Gerçek](#bkmk_policyspy-actual)
- [İstekte bulunan](#bkmk_policyspy-requested)
- [Varsayılan](#bkmk_policyspy-default)
- [Olaylar](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a>Varolan

Bu sekme, istemcinin geçerli ilkesini görüntüler. Geçerli ilke, bir istemcinin davranışını ve yazılım dağıtımı ve envanteri gibi istemci aracılarının davranışını belirler. Bu sekme, sonuçları bilgisayar ad alanı ve kullanıcıya özgü her ad alanı için kök düğümü olan bir ağaç biçiminde görüntüler. Sınıf listesini göstermek için bir ad alanı düğümünü genişletin. Örneklerinin listesini göstermek için bir sınıfı genişletin. Sınıf listesi yalnızca örnekleri olan sınıfları içerir.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a>İstenen

Bu sekme, istemcinin atanan sitesinden aldığı ilke atamalarını görüntüler. Bu sekme, sonuçları makine ad alanı ve kullanıcıya özgü her ad alanı için kök düğümü olan ağaç biçiminde görüntüler. Bir ad alanı düğümü genişletildiğinde aşağıdaki düğümler görüntülenir:  

- **Yapılandırma**: ilke nesnesini, atamaları ve diğerlerini içeren CCM_Policy_Config türetilen yapılandırma sınıflarının bir listesini görüntüler.  

- **Ayarlar**: ilkeler tarafından oluşturulan tüm etkin ayarları görüntüler. Ayarlar yapılandırma düğümünün altında görüntülenir. 

> [!Note]   
> İstemci bu ayarları son sonuç kümesinde birleştirmediği için aynı ada sahip birden çok örnek bulunabilir. İlke Spy, doğru ilke anahtarları yerine RealKey özelliklerini kullanarak bu düğüm altındaki örnekleri görüntüler. Bu örneklerin gerçek sekmede görüntülenecek sonuç kümesi ile ilişkilendirilmesi.  


### <a name="default"></a><a name="bkmk_policyspy-default"></a>Varsayılanını

Bu sekme, **istenen** sekmeyle aynı bilgileri görüntüler. DefaultMachine ve DefaultUser ad alanlarının içeriğini de içerir.


### <a name="events"></a><a name="bkmk_policyspy-events"></a>Olayları

Bu sekmede, ilke aracısı olayları olduğu gibi görüntülenir. Görünüm, CCM_PolicyAgent_Event türetilen tüm olaylar için bir WMI olay aboneliği oluşturur. Görünüm en fazla 200 olay gösterir. Gerektiğinde, listenin en eski olaylarını kaldırır. Listedeki son öğeyi seçerseniz, yeni olaylar eklediğinden liste otomatik olarak aşağı kayar. Aksi takdirde, Görünüm geçerli konumunu korur ve yeni olayları görüntülemek için aşağı kaydırmanız veya bitiş tuşuna basmanız gerekir. Bu görünüm, bir verdiğiniz ilke görüntülenirken her zaman boştur.



## <a name="client-info-pane"></a>İstemci bilgileri bölmesi
Istemci bilgileri bölmesi, hedef bilgisayar için özelliklerin bir listesini görüntüler. Varsa, aşağıdaki özellikleri görüntüler:  
- Adı
- Kimlik
- Sürüm
- Site
- Atanan MP
- Yerleşik MP
- Proxy MP
- Ara sunucu durumu



## <a name="details-pane"></a>Ayrıntılar bölmesi
Ayrıntılar bölmesi, geçerli seçimle ilgili ayrıntılı bilgileri görüntüler. Hiçbir seçim etkin değilse, sürüm de dahil olmak üzere, Ilke Spy ile ilgili bilgileri görüntüler. Aksi takdirde, seçili öğenin nesne biçimini Yönet (MOF) gösterimini görüntüler.

İlke Spy, WMI tarafından oluşturulan düz metin MOF 'den daha kolay bir HTML görüntüsü oluşturmak için kendi MOF oluşturma yordamını kullanır. Bu davranış, MOF 'nin daha okunaklı olması için Ilke Spy 'un aşağıdaki özellikleri eklemesini sağlar:  

- Söz dizimi vurgulama  

- Girintili nesneler ve diziler  

- Özellikler sistem, devralınan ve yerel gruplar halinde düzenlenir. Varsayılan olarak, sistemi ve devralınan grupları daraltır. Örneğin hangi özelliklerin gerçekten kullandığını hemen görebilirsiniz.  

- MOF 'yi kopyalayın veya düz metin MOF 'yi panoya kopyalayın. Bu özellik, MofComp aracını doğrudan çağırarak MOF 'yi diğer uygulamalara yapıştırmak için yararlıdır.  

CCM_Policy_Policy türetilen Ilke nesnelerinin örnekleri için, Ayrıntılar bölmesinde görüntülenen MOF 'nin altındaki ilke gövdesi görüntülenir. İstemci, ilke gövdesini indirmemişse, Ilke Spy bir köprü görüntüler. İlke gövdesini doğrudan istemcinin yönetim noktasından indirmek için bağlantıya tıklayın. Araç, ilke gövdesini başarıyla indirdiğinde, köprünün, yanıtın içeriğiyle yerini alır. Aksi takdirde, Ilke Spy, isteğin başarısız olduğunu belirten ekranı güncelleştirir.

