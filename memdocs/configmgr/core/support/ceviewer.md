---
title: Koleksiyon Değerlendirme Görüntüleyicisi
titleSuffix: Configuration Manager
description: Configuration Manager 'de koleksiyon değerlendirme işlemini görüntülemek ve sorunlarını gidermek için koleksiyon değerlendirme görüntüleyicisini kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723421"
---
# <a name="collection-evaluation-viewer"></a>Koleksiyon Değerlendirme Görüntüleyicisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Koleksiyon değerlendirme Görüntüleyicisi [Configuration Manager araçlarından](tools.md)biridir. Birincil site sunucusunda koleksiyon değerlendirme işlemini görüntülemek ve sorunlarını gidermek için kullanın.

Araç aşağıdaki bilgileri görüntüler:  

- Tam ve artımlı koleksiyon değerlendirmeleri için hem geçmiş hem de canlı bilgiler  

- Değerlendirme kuyruğu durumu  

- Koleksiyon değerlendirmelerinin tamamlanma zamanı  

- Şu anda hangi koleksiyonlar değerlendirilemekte  

- Bir koleksiyon değerlendirmesinin başlayacağı ve tamamlayabaşlayacağı tahmini süre  



## <a name="about-collection-evaluation"></a>Koleksiyon değerlendirmesi hakkında

Koleksiyon değerlendirme işlemi, üyelerini güncelleştirmek için bir koleksiyonun Üyelik kuralları değerlendirilirken çalışır. Site, değerlendirme yaptığı bir koleksiyonu dört farklı kuyruktan birinde koyar:  

- **El Ile kuyruk**: bir yöneticinin, konsolundan değerlendirme için el ile seçtiği koleksiyonlar için  

- **Yeni kuyruk**: yeni oluşturulan koleksiyonlar için  

- **Tam sıra**: tam değerlendirme nedeniyle koleksiyonlar için  

- **Artımlı kuyruk**: artımlı değerlendirmede koleksiyonlar için  

Yukarıdaki kuyruklardaki koleksiyonları değerlendirmek için çalışan dört iş parçacığı vardır. Her sıra bir dizi dizi içerir ve her dizi değerlendirilecek koleksiyonları içerir. Sıra için çalışan iş parçacığı diziden bir koleksiyon seçer ve değerlendirmeyi çalıştırır. Kuyruk uzunluğu kuyruktaki dizi dizilerini gösterir.



## <a name="requirements"></a>Gereksinimler

- Aracı site sunucusunda çalıştırın  

- Aracı, en azından **salt okunurdur analist** rolüyle Yönetici Kullanıcı tarafından çalıştırın  

- Kullanıcı ayrıca, SQL 'de site veritabanı için **okuma** izni gerektirir



## <a name="usage"></a>Kullanım

**Ceviewer. exe**' yi çalıştırın. Aracının ana menüsü aşağıdaki sekmeleri içerir: 

- [Bağlan](#bkmk_connect): birincil site sunucusuyla ilk bağlantıyı kurun ve SQL Server  

- [Tam değerlendirme](#bkmk_full-eval): tüm geçmiş tam değerlendirmelere ilişkin ayrıntılı bilgileri listeler   

- [Artımlı değerlendirme](#bkmk_incremental-eval): tüm geçmiş artımlı değerlendirmelere ilişkin ayrıntılı bilgileri listeler  

- [Tüm kuyruklar](#bkmk_all-q): dört kuyruk için geçerli koleksiyon değerlendirmelerini özetler  

- [El Ile kuyruk](#bkmk_manual-q): el ile kuyruktaki geçerli koleksiyon değerlendirmesiyle ilgili ayrıntılı bilgileri listeler  

- [Yeni kuyruk](#bkmk_new-q): yeni kuyruktaki geçerli koleksiyon değerlendirmesiyle ilgili ayrıntılı bilgileri listeler  

- [Tam sıra](#bkmk_full-q): tam kuyruktaki geçerli koleksiyon değerlendirmesiyle ilgili ayrıntılı bilgileri listeler  

- [Artımlı kuyruk](#bkmk_incremental-q): artımlı kuyruktaki geçerli koleksiyon değerlendirmesiyle ilgili ayrıntılı bilgileri listeler  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Bağlan sekmesi

Bu sekme, birincil site sunucusuna ilk bağlantıyı ayarlamanıza olanak sağlar. Araç ayrıca, site veritabanını barındıran SQL Server ile bağlantı kurar.

Birincil site sunucusu ve SQL Server bağlantıları, geçerli oturum açmış kullanıcı kimlik bilgilerini kullanır. Merkezi yönetim sitesine veya ikincil bir siteye bağlantılar desteklenmez. Bu sitelerde hiçbir koleksiyon değerlendirme işlemi çalıştıryok.

Araç başarıyla bir bağlantı kurduktan sonra, koleksiyon değerlendirme görüntüleyicisinin altındaki, aracın SQL Server bağlantısını doğrulayan bir bildirime bakın. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a>Tam değerlendirme sekmesi

Geçmiş tam koleksiyon değerlendirmeleri hakkında ayrıntılı bilgileri gösterir. Sekiz sütun vardır:  

- **Koleksiyon adı**: koleksiyonun adı  

- **SITE kimliği**: KOLEKSIYONUN site kimliği   

- **Çalışma zamanı**: son toplama değerlendirmesinin ne kadar süreceğine (saniye cinsinden)  

- **Son değerlendirme tamamlanma zamanı**: son toplama değerlendirmesi tamamlandığında  

- **Sonraki değerlendirme zamanı**: bir sonraki tam değerlendirme başladığında  

- **Üye değişiklikleri**: Son koleksiyon değerlendirmesinde üye değişiklikleri. Bu değişiklikler artı (Üyeler eklendi) veya eksi (kaldırılan Üyeler).  

- **Son üye değiştirme zamanı**: koleksiyon değerlendirmesinde üyelik değişikliği olan en son zaman  

- **Yüzde**: Toplam (tüm koleksiyonlar) değerlendirme süresi üzerinde bu koleksiyon için değerlendirme süresinin yüzdesi  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a>Artımlı değerlendirme sekmesi

Son artımlı koleksiyon değerlendirmeleri hakkında ayrıntılı bilgileri gösterir. Yedi sütun vardır:  

- **Koleksiyon adı**: koleksiyonun adı  

- **SITE kimliği**: KOLEKSIYONUN site kimliği   

- **Çalışma zamanı**: son toplama değerlendirmesinin ne kadar süreceğine (saniye cinsinden)  

- **Son değerlendirme tamamlanma zamanı**: son toplama değerlendirmesi tamamlandığında  

- **Üye değişiklikleri**: Son koleksiyon değerlendirmesinde üye değişiklikleri. Bu değişiklikler artı (Üyeler eklendi) veya eksi (kaldırılan Üyeler).  

- **Son üye değiştirme zamanı**: koleksiyon değerlendirmesinde üyelik değişikliği olan en son zaman  

- **Yüzde**: Toplam (tüm koleksiyonlar) değerlendirme süresi üzerinde bu koleksiyon için değerlendirme süresinin yüzdesi  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a>Tüm kuyruklar sekmesi

Dört kuyruk için canlı koleksiyon değerlendirmeleri özetler. Altı bölüm vardır:  

- **Özet**: dört kuyruktaki tüm koleksiyonlar için toplam koleksiyon numarasını ve sıra uzunluğunu listeler  

- **Değerlendirme çalıştırılıyor**: her sırada hangi koleksiyonun değerlendirileceğini ve ne kadar süreyle çalıştığını listeler  

- **El Ile güncelleştirme**: değerlendirilen koleksiyonların kısa bir özetini, tahmini tamamlanma süresini ve değerlendirme sırasını el ile sıraya göre gösterir  

- **Yeni koleksiyon**: değerlendirilen koleksiyonların kısa bir özetini, tahmini tamamlanma süresini ve değerlendirme sırasını yeni koleksiyon kuyruğunda gösterir  

- **Tam değerlendirme**: değerlendirilmekte olan koleksiyonların kısa bir özetini, tahmini tamamlanma süresini ve değerlendirmenin tam değerlendirme kuyruğundaki sırasını gösterir  

- **Artımlı değerlendirme**: değerlendirilmekte olan koleksiyonların kısa bir özetini, tahmini tamamlanma süresini ve değerlendirme sırasını artımlı değerlendirme kuyruğunda gösterir  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a>El ile kuyruk sekmesi

Şu anda değerlendirilen el ile toplama değerlendirmesi hakkındaki bilgileri gösterir. Listedeki sıra, koleksiyonun değerlendirileceği sıradır. Dört sütun vardır:  

- **Koleksiyon adı**: koleksiyonun adı  

- **SITE kimliği**: KOLEKSIYONUN site kimliği   

- **Tahmini tamamlanma süresi**: değerlendirmenin tamamlanması tahmin edildiğinde  

- **Tahmini çalışma süresi**: değerlendirmenin ne kadar süre çalıştırılacağı tahmini, gün: Saat: dakika: ikinci biçim  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a>Yeni kuyruk sekmesi

Değerlendirilmekte olan yeni koleksiyon değerlendirmesiyle ilgili canlı bilgileri gösterir. Listedeki sıra, koleksiyonun değerlendirileceği sıradır. Dört sütun vardır:  

- **Koleksiyon adı**: koleksiyonun adı  

- **SITE kimliği**: KOLEKSIYONUN site kimliği   

- **Tahmini tamamlanma süresi**: değerlendirmenin tamamlanması tahmin edildiğinde  

- **Tahmini çalışma süresi**: değerlendirmenin ne kadar süre çalıştırılacağı tahmini, gün: Saat: dakika: ikinci biçim  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a>Tam sıra sekmesi

Şu anda değerlendirilen tam koleksiyon değerlendirmesi hakkındaki bilgileri gösterir. Listedeki sıra, koleksiyonun değerlendirileceği sıradır. Dört sütun vardır:  

- **Koleksiyon adı**: koleksiyonun adı  

- **SITE kimliği**: KOLEKSIYONUN site kimliği   

- **Tahmini tamamlanma süresi**: değerlendirmenin tamamlanması tahmin edildiğinde  

- **Tahmini çalışma süresi**: değerlendirmenin ne kadar süre çalıştırılacağı tahmini, gün: Saat: dakika: ikinci biçim  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a>Artımlı kuyruk sekmesi

Şu anda değerlendirilen artımlı koleksiyon değerlendirmesi hakkındaki bilgileri gösterir. Listedeki sıra, koleksiyonun değerlendirileceği sıradır. Dört sütun vardır:  

- **Koleksiyon adı**: koleksiyonun adı  

- **SITE kimliği**: KOLEKSIYONUN site kimliği   

- **Tahmini tamamlanma süresi**: değerlendirmenin tamamlanması tahmin edildiğinde  

- **Tahmini çalışma süresi**: değerlendirmenin ne kadar süre çalıştırılacağı tahmini, gün: Saat: dakika: ikinci biçim  



