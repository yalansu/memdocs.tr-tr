---
title: Dosya tabanlı çoğaltma
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşinizdeki siteler arasında veri aktarmak için dosya tabanlı çoğaltmayı nasıl kullandığını öğrenin
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720173"
---
# <a name="file-based-replication"></a>Dosya tabanlı çoğaltma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager hiyerarşinizdeki siteler arasında dosya tabanlı verileri aktarmak için dosya tabanlı çoğaltmayı kullanır. Bu veriler, alt sitelerdeki dağıtım noktalarına dağıtmak istediğiniz uygulamaları ve paketleri içerir. Ayrıca, sitenin üst sitesine aktardığı işlenmemiş bulma verisi kayıtlarını işler ve sonra işler.  

Siteler arasındaki dosya tabanlı iletişim TCP/IP bağlantı noktası 445 üzerinde *sunucu ileti bloğu* (SMB) protokolünü kullanır. Sitenin ağ üzerinden aktardığı veri miktarını denetlemek için bant genişliği azaltma ve darbe modunu belirtin. Ağ üzerinden ne zaman veri gönderileceğini denetlemek için zamanlamalar kullanın.  

## <a name="routes"></a><a name="bkmk_routes"></a>Yolların

Aşağıdaki bilgiler, dosya çoğaltma yolları ayarlamanıza ve kullanmanıza yardımcı olabilir.  

### <a name="file-replication-route"></a>Dosya çoğaltma yolu

Her dosya çoğaltma yolu, bir sitenin dosya tabanlı verileri aktardığı bir hedef siteyi tanımlar. Her site belirli bir hedef siteye yönelik bir dosya çoğaltma yolunu destekler.  

Bir dosya çoğaltma yolunu yönetmek için **Yönetim** çalışma alanına gidin. **Hiyerarşi Yapılandırması** düğümünü genişletin ve ardından **dosya çoğaltma**' yı seçin.  

Dosya çoğaltma yolları için aşağıdaki ayarları değiştirebilirsiniz:  

#### <a name="file-replication-account"></a>Dosya çoğaltma hesabı

Bu hesap hedef siteye bağlanır ve verileri bu sitenin **SMS_Site** paylaşımıyla yazar. Alan site, bu paylaşıma yazılan verileri işler. Varsayılan olarak, hiyerarşiye bir site eklediğinizde, Configuration Manager yeni site sunucusunun bilgisayar hesabını dosya çoğaltma hesabı olarak atar. Daha sonra bu hesabı hedef sitenin `SMS_SiteToSiteConnection_<sitecode>` grubuna ekler. Bu grup, SMS_Site paylaşımının erişimine izin veren bilgisayar için yereldir. Bu hesabı bir Windows kullanıcı hesabı olarak değiştirebilirsiniz. Hesabı değiştirirseniz, yeni hesabı hedef sitenin `SMS_SiteToSiteConnection_<sitecode>` grubuna eklediğinizden emin olun.  

> [!NOTE]  
> İkincil siteler **Dosya Çoğaltma Hesabı**olarak her zaman ikincil site sunucusunun bilgisayar hesabını kullanır.  

#### <a name="schedule"></a>Zamanlama

Her dosya çoğaltma yolu için zamanlamayı ayarlayın. Bu eylem, verilerin hedef siteye aktarabilmesi için veri türünü ve saati kısıtlar.  

#### <a name="rate-limits"></a>Hız sınırları

Her dosya çoğaltma yolu için oran sınırlarını belirtin. Bu eylem, sitenin hedef siteye veri aktarırken kullandığı ağ bant genişliğini denetler:  

- **Darbe modu**: sitenin hedef siteye gönderdiği veri bloklarının boyutunu belirtin. Ayrıca gönderilen her veri öbeği arasındaki gecikme süresini de belirtebilirsiniz. Hedef siteye düşük bant genişliğine sahip bir ağ bağlantısı üzerinden veri göndermeniz gerektiğinde bu seçeneği kullanın.

    Örneğin, her beş saniyede bir 1 KB veri gönderme kısıtlamalarına sahip olursunuz, ancak üç saniyede bir 1 KB değil. Bu kısıtlama, bağlantının hızına veya belirli bir zamanda kullanılmasına bakılmaksızın olur.

- **Saate göre maksimum aktarım hızlarıyla sınırlı**: site yalnızca belirttiğiniz sürenin yüzdesini kullanarak bir hedef siteye veri gönderir. Configuration Manager, ağın kullanılabilir bant genişliğini tanımlamaz. Veri göndereme süresini zaman dilimlerine böler. Daha sonra verileri kısa bir zaman bloğunda gönderir ve bu, verileri göndermediği zaman blokları izler.

    Örneğin, en yüksek oranı **%50**olarak ayarlarsınız. Configuration Manager, verileri göndermeyen bir süre ve ardından eşit bir süre boyunca veri iletir. Bu, gönderdiği veri bloğunun gerçek boyutunu yönetmez. Site yalnızca veri gönderdiği süreyi yönetir.  

    > [!CAUTION]  
    > Varsayılan olarak, bir site, bir hedef siteye veri aktarmak için en çok üç **eş zamanlı gönderme** kullanabilir. Bir dosya çoğaltma yolu için oran sınırlarını etkinleştirdiğinizde, bu siteye yönelik **eşzamanlı teslimeleri** bir ile sınırlandırır. **Kullanılabilir bant genişliğini sınırla (%)** ayarı **%100**olarak ayarlandığında bu davranış geçerlidir. Örneğin, gönderen için varsayılan ayarları kullanırsanız, bu durum hedef siteye aktarım hızını varsayılan kapasitenin üçte biri olacak şekilde azaltır.  

#### <a name="routes-between-secondary-sites"></a>İkincil siteler arasındaki rotalar

İki ikincil site arasında dosya tabanlı içerikleri yönlendirmek için bu siteler arasında bir dosya çoğaltma yolu yapılandırın.  


### <a name="sender"></a>Gönderen

Her sitenin bir göndereni vardır. Gönderici bir siteden hedef siteye ağ bağlantısını yönetir. Aynı anda birden fazla siteye bağlantı kurabilir. Gönderen, bir siteye bağlanmak için, siteye dosya çoğaltma yolunu kullanır ve ağ bağlantısını kurmak için kullandığı hesabı tanımlar. Gönderen Ayrıca, hedef sitenin SMS_Site paylaşımıyla veri yazmak için bu hesabı kullanır.  

Varsayılan olarak, gönderici birden çok **eş zamanlı gönderme**veya bir *iş parçacığı*kullanarak verileri bir hedef siteye yazar. Her iş parçacığı, hedef siteye farklı bir dosya tabanlı nesne aktarabilir. Gönderen bir nesneyi gönderilmeye başladığında, nesnenin tamamını gönderene kadar bu nesne için veri blokları yazmaya devam eder. Nesne için tüm verileri gönderdikten sonra, yeni bir nesne o iş parçacığına gönderilmeye başlayabilir.  

Bir sitenin gönderisini yönetmek için, **Yönetim** çalışma alanına gidin ve **site yapılandırma** düğümünü genişletin. **Siteler** düğümünü seçin ve ardından yönetmek Istediğiniz sitenin **Özellikler** ' i seçin. Gönderici ayarlarını değiştirmek için **gönderici** sekmesine geçin.  

Bir gönderici için aşağıdaki ayarları değiştirebilirsiniz:  

#### <a name="maximum-concurrent-sendings"></a>En fazla eşzamanlı gönderme

Varsayılan olarak, her site beş eşzamanlı gönderme (iş parçacığı) kullanır. Her bir hedef siteye veri gönderdiğinde kullanabileceğiniz üç iş parçacığı vardır. Bu sayıyı artırdığınızda, siteler arasında verilerin verimini artırabilirsiniz. Daha fazla iş parçacığı Configuration Manager aynı anda daha fazla dosya aktarabileceği anlamına gelir. Bu sayının artırılması aynı zamanda siteler arasındaki ağ bant genişliği talebini artırır.  

#### <a name="retry-settings"></a>Yeniden deneme ayarları

Varsayılan olarak, her site bağlantı denemeleri arasında tek dakikalık bir gecikmeyle bir sorun bağlantısını iki kez yeniden dener. Sitenin yaptığı bağlantı girişimlerinin sayısını ve denemeler arasında ne kadar bekleneceğini değiştirebilirsiniz.  


## <a name="next-steps"></a>Sonraki adımlar

[Veritabanı çoğaltması](database-replication.md)
