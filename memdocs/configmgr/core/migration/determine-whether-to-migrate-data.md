---
title: Geçirilecek öğeleri seçin
titleSuffix: Configuration Manager
description: Hangi verileri geçirebileceğinizi ve geçerli dala Configuration Manager geçiremeyeceğiniz verileri öğrenin.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718920"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Geçerli dala Configuration Manager veri geçirilip geçirmeyeceğinizi belirleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalda, geçiş Configuration Manager desteklenen sürümlerinden oluşturduğunuz verileri ve konfigürasyonları yeni hiyerarşinize aktarmaya yönelik bir işlem sağlar.  Bunu kullanarak şunları yapabilirsiniz:  

-   Birden çok hiyerarşiyi bir içinde birleştirin.  

-   Verileri ve konfigürasyonları bir laboratuvar dağıtımından üretim dağıtımınıza taşıyın.

-   Güncel Configuration Manager 2012 dala Configuration Manager yükseltme yolu olmayan Configuration Manager 2007 gibi Configuration Manager önceki bir sürümünden veri ve yapılandırma taşıyın (Bu, geçerli dala Configuration Manager yükseltme yolunu destekler).  

Dağıtım noktası site sistem rolü ve dağıtım noktalarını barındıran bilgisayarlar hariç olmak üzere (siteleri, site sistem rollerini veya bir site sistem rolü barındıran bilgisayarları içeren) hiçbir altyapı, hiyerarşiler arasında geçirilemez, aktarılamaz veya paylaşılamaz.  

 Sunucu altyapısını geçiremeseniz de, hiyerarşiler arasında Configuration Manager istemcileri geçirebilirsiniz. İstemci geçişi, istemcilerin kullandığı verilerin kaynak hiyerarşisinden hedef hiyerarşisine geçirilmesini ve daha sonra istemcinin yeni hiyerarşiye rapor vermesi için istemci yazılımının yüklenmesini veya yeniden atanmasını içerir.

Yeni hiyerarşiye bir istemci yükledikten ve istemci verilerini gönderdikten sonra, benzersiz Configuration Manager KIMLIĞI, Configuration Manager daha önce her bir istemci bilgisayarıyla geçirdiğiniz verileri ilişkilendirmenize yardımcı olur.  

 Geçiş tarafından sağlanan işlevler, yapılandırma ve dağıtımlarda yaptığınız yatırımları korumanıza yardımcı olmakla birlikte, ilk olarak üründeki temel değişikliklerden tam olarak yararlanmanızı sağlar (ilk olarak System Center 2012 Configuration Manager eklenmiştir ve Configuration Manager devam eder). Bu değişiklikler, daha az site ve kaynak kullanan Basitleştirilmiş bir Configuration Manager hiyerarşisini ve 64 bit donanımda çalışan yerel 64 bit kodu kullanmaktan gelen gelişmiş işlemleri içerir.  

 Geçişin desteklediği Configuration Manager sürümleri hakkında bilgi için bkz. [geçiş önkoşulları](../../core/migration/prerequisites-for-migration.md).  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a>Geçerli dala Configuration Manager geçirebileceğiniz veriler

Geçiş, Desteklenen Configuration Manager hiyerarşileri arasında çoğu nesneyi geçirebilir. Configuration Manager 2007 ' in desteklenen bir sürümünden bazı nesnelerin geçirilmiş örnekleri System Center 2012 Configuration Manager şeması ve nesne biçimine uyacak şekilde değiştirilmelidir.

Bu değişiklikler, kaynak site veritabanındaki verileri etkilemez. System Center 2012 Configuration Manager veya Configuration Manager geçerli dalının desteklenen bir sürümünden geçirilen nesneler değişiklik gerektirmez.  

Aşağıda, kaynak hiyerarşisindeki Configuration Manager sürümüne göre geçirebilen nesneler verilmiştir. Sorgu gibi bazı nesneler geçirilmez. Bu nesneleri kullanmaya devam etmek istiyorsanız, bunları yeni hiyerarşide yeniden oluşturmanız gerekir. Bazı istemci verileri de dahil diğer nesneler, söz konusu hiyerarşideki istemcileri yönetirken yeni hiyerarşide otomatik olarak yeniden oluşturulur.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>System Center 2012 Configuration Manager veya geçerli dalı Configuration Manager geçirebileceğiniz nesneler

-   System Center 2012 Configuration Manager ve sonraki sürümleri için uygulamalar  

-   System Center 2012 Configuration Manager ve sonraki sürümlerinden App-V sanal ortamı  

-   Varlık Yönetim Bilgileri özelleştirmeleri  

-   Sınırlar  

-   Koleksiyonlar: System Center 2012 Configuration Manager veya geçerli dalı Configuration Manager desteklenen bir sürümünden koleksiyonları geçirmek Için bir nesne geçiş işi kullanırsınız.  

-   Uyumluluk ayarları:  

    -   Yapılandırma temelleri  

    -   Yapılandırma öğeleri  

-   Dağıtımlar  

-   İşletim sistemi dağıtımı:  

    -   Önyükleme görüntüleri  

    -   Sürücü paketleri  

    -   Sürücüler  

    -   Görüntüler  

    -   Paketler  

    -   Görev dizileri  

-   Arama sonuçları: kayıtlı arama ölçütleri  

-   Yazılım güncelleştirmeleri:  

    -   Dağıtımlar  

    -   Dağıtım paketleri  

    -   Şablonlar  

    -   Yazılım güncelleştirmesi listeleri  

-   Yazılım dağıtım paketleri  

-   Yazılım kullanım ölçümü kuralları  

-   Sanal uygulama paketleri  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Configuration Manager 2007 SP2 'den geçirebileceğiniz nesneler

-   Reklamlar  

-   System Center 2012 Configuration Manager ve sonraki sürümleri için uygulamalar  

-   System Center 2012 Configuration Manager ve sonraki sürümlerinden App-V sanal ortamı  

-   Varlık Yönetim Bilgileri özelleştirmeleri  

-   Sınırlar  

-   Koleksiyonlar: bir koleksiyon geçiş işini kullanarak koleksiyonları Configuration Manager 2007 ' nin desteklenen bir sürümünden geçirmiş olursunuz.  

-   Uyumluluk ayarları (Configuration Manager 2007’de istenen yapılandırma yönetimi olarak bilinir):  

    -   Yapılandırma temelleri  

    -   Yapılandırma öğeleri  

-   İşletim sistemi dağıtımı:  

    -   Önyükleme görüntüleri  

    -   Sürücü paketleri  

    -   Sürücüler  

    -   Görüntüler  

    -   Paketler  

    -   Görev dizileri  

-   Arama sonuçları: arama klasörleri  

-   Yazılım güncelleştirmeleri:  

    -   Dağıtımlar  

    -   Dağıtım paketleri  

    -   Şablonlar  

    -   Yazılım güncelleştirmesi listeleri  

-   Yazılım dağıtım paketleri  

-   Yazılım kullanım ölçümü kuralları  

-   Sanal uygulama paketleri  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a>Geçerli dala Configuration Manager geçiremeyeceğiniz veriler

Aşağıdaki nesne türlerini geçiremezsiniz:  

-   AMT istemcisi sağlama bilgileri  

-   İstemcilerde aşağıdakiler dahil olmak üzere dosyalar:  

    -   İstemci envanter ve geçmiş verileri  

    -   İstemci önbelleğindeki dosyalar  

-   Sorgular  

-   Site ve nesneler için 2007 güvenlik hakları ve örnekleri Configuration Manager  

-   SQL Server Reporting Services Configuration Manager 2007 raporu  

-   Configuration Manager 2007 Web raporları  

-   System Center 2012 Configuration Manager ve Configuration Manager güncel dal raporları  

-   System Center 2012 Configuration Manager ve Configuration Manager geçerli dalı rol tabanlı yönetim:  

    -   Güvenlik rolleri  

    -   Güvenlik kapsamları  
