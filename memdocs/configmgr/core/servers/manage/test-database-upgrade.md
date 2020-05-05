---
title: Veritabanı güncelleştirmesini test et
titleSuffix: Configuration Manager
description: Configuration Manager güncelleştirmelerini yüklerken site veritabanını yükseltin.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719984"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Güncelleştirme yüklerken veritabanı yükseltmesini test etme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konudaki bilgiler, geçerli Configuration Manager dalı için konsol içi bir güncelleştirmeyi yüklemeden önce bir test veritabanı yükseltmesini çalıştırmanıza yardımcı olabilir. Ancak, test yükseltmesi artık gerekli değildir veya veritabanınız şüpheli olmadığı veya Configuration Manager tarafından açıkça desteklenmeyen özelleştirmeler tarafından değiştirilmediği takdirde adım adım önerilmez.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Bir test yükseltmesi çalıştıralmam gerekiyor mu?
Configuration Manager geçerli Dalla tanıtılan değişiklikler nedeniyle bu yükseltme testinin kullanımdan kaldırılması mümkün hale getirilir. Bu değişiklikler, bir üretim ortamının daha yeni sürümlere güncelleştirilemeyebilir işlemini ve hızını basitleştirir. Bu yeniden tasarımı, müşterilerin yeni bir güncelleştirme yüklerken daha az risk ve daha az işletimsel ek yük ile güncel kalmasına yardımcı olmak için gerçekleştirildi.

Değişiklikler, bir Site Recovery 'yi çalıştırmaya gerek kalmadan otomatik olarak başarısız bir güncelleştirmeyi geri kaydeden mantığı dahil güncelleştirmelerin nasıl yükleneceğine göre yapılır. Bu değişiklikler, güncelleştirme yüklemelerini yönetmek için konsolun kullanımını etkinleştirir ve [başarısız bir güncelleştirmenin yüklenmesini yeniden deneme](install-in-console-updates.md#bkmk_retry)seçeneği içerir.

> [!TIP]
> System Center 2012 Configuration Manager gibi eski ürünlerden güncel dala Configuration Manager yükselttiğinizde, [test veritabanı yükseltmeleri önerilen bir adım olarak kalır](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test).

Konsol içi bir güncelleştirme yüklerken bir site veritabanının yükseltmesini test etmek istiyorsanız, aşağıdaki bilgiler [konsol içi bir güncelleştirmeyi yükleme ile ilgili yönergeler](install-in-console-updates.md#bkmk_install)de sağlar.

## <a name="prepare-to-run-a-test-database-upgrade"></a>Test veritabanı yükseltmesini çalıştırmaya hazırlanma  
Hiyerarşinize güncelleştirme 1702 gibi yeni bir güncelleştirme yüklemeden önce, site veritabanınızın yükseltmesini test edebilirsiniz.

Yükseltme testini çalıştırmak için CD 'deki kaynak dosyalardan Configuration Manager kurulumunu kullanın [. ](the-cd.latest-folder.md)Güncelleştirdiğiniz Configuration Manager sürümünü çalıştıran bir sitenin en son klasörü. Bu gereksinim, 1702 güncelleştirmesi için veritabanı güncelleştirmesini test etmek için gereken anlamına gelir:
-   Bu CD 'yi alabilmeniz için 1702 sürümünü çalıştıran en az bir siteniz olmalıdır. En son klasör.
-   Gerekli sürümü çalıştıran bir siteniz yoksa, bir siteyi laboratuvar ortamına yüklemeyi ve ardından bu siteyi yeni sürüme güncelleştirmeyi düşünün. Bu, CD 'yi oluşturur. Kaynak dosyalarının doğru sürümüne sahip en son klasör.

Yükseltme testi, site veritabanınızın ayrı bir SQL Server örneğine geri yüklediğiniz yedeğine karşı çalıştırılır.  Kurulum 'U CD 'den çalıştırırsınız **. ** **TESTDBUPGRADE** komut satırı anahtarına sahip en son klasör, veritabanının kopyasını geri yükleyen test yükseltmesine. Test yükseltmesi tamamlandıktan sonra, yükseltilen veritabanı atılır. Configuration Manager bir site tarafından kullanılamaz.

Bir güncelleştirme yüklemesi başarısız olursa, siteyi kurtarmanız gerekmez. Bunun yerine, güncelleştirme yüklemesini konsolunun içinden tekrar deneyebilirsiniz.

##  <a name="run-the-test-upgrade"></a>Test yükseltmesini Çalıştır    
1. CD 'deki Configuration Manager Kurulum ve kaynak dosyalarını kullanın **. **Güncelleştirmeyi planladığınız sürümü çalıştıran bir sitenin en son klasörü.  

2. **CD 'yi kopyalayın. **Test veritabanı yükseltmesini çalıştırmak için kullanacağınız SQL Server örneğindeki bir konuma en son klasör.

3. Yükseltmeyi test etmek istediğiniz site veritabanının bir yedeğini oluşturun. Sonra, bu veritabanının bir kopyasını bir Configuration Manager sitesi barındırmayan bir SQL Server örneğine geri yükleyin. SQL Server örnek, site veritabanınız ile aynı SQL Server sürümünü kullanmalıdır.  

4. Veritabanı kopyasını geri yükledikten sonra, **Kurulum 'U** CD 'den çalıştırın. Güncelleştirdiğiniz sürümden kaynak dosyalarını içeren en son klasör. Kurulum'u çalıştırdığınızda, **/TESTDBUPGRADE** komut satırı seçeneğini kullanın. Veritabanı kopyasını barındıran SQL Server örneği varsayılan örnek değilse, site veritabanı kopyasını barındıran örneği tanımlamak için komut satırı bağımsız değişkenlerini belirtin.   

   Örneğin, *SMS_ABC*veritabanı adına sahip bir site veritabanınız vardır. Bu site veritabanının bir kopyasını, örnek adı *dbtest*olan desteklenen bir SQL Server örneğine geri yükleyin. Site veritabanının bu kopyasının yükseltmesini test etmek için şu komut satırını kullanın: **Setup. exe/TESTDBUPGRADE DBtest \ CM_ABC**.  

   Setup. exe ' yi Configuration Manager kaynak medyada şu konumda bulabilirsiniz: **Smssetup\bin\x64**.  

5. Yükseltme testini çalıştırdığınız SQL Server örneğinde, sistem sürücüsünün kökündeki *ConfigMgrSetup. log* dosyasında ilerleme ve başarı durumunu izleyin.  

    Test yükseltmesi başarısız olursa, site veritabanı yükseltme hatasıyla ilgili sorunları giderin. Ardından, site veritabanının yeni bir yedeğini oluşturun ve veritabanının yeni kopyasının yükseltmesini test edin.  



## <a name="next-steps"></a>Sonraki adımlar
Test veritabanı güncelleştirmesi başarıyla tamamlandıktan sonra, güncelleştirilmiş veritabanını atın. Configuration Manager bir site tarafından kullanılamaz. Ardından etkin sitenize geri dönüp [güncelleştirme yüklemesine başlayabilirsiniz](install-in-console-updates.md).
