---
title: Sistem durumunu izleme
titleSuffix: Configuration Manager
description: Sistem durumu izlemenin masaüstü Analizi 'nde nasıl çalıştığı hakkında bilgi edinin.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 119f787f15b8c907d0c760a12b973ca984f4348c
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268547"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Masaüstü Analizi 'nde sistem durumu izleme

[Bir güncelleştirmeyi üretime dağıtırken](deploy-prod.md), cihazlarınızın sistem durumunu izlemeye yardımcı olmak Için masaüstü Analizi ' ni kullanın. Bu makalede Sistem durumu izlemenin nasıl çalıştığı ayrıntılı bilgiler açıklanmaktadır.

Bu özelliğin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [güncelleştirilmiş cihazların sistem durumunu izleme](deploy-prod.md#bkmk_monitor).

![Masaüstü analizinin sistem durumunu Izle sayfasının ekran görüntüsü](media/monitor-health.png)

> [!NOTE]  
> Masaüstü analizi, yalnızca paydası olarak kullanabileceği kullanım verileri sağlayan cihazlardan sistem durumu verilerini toplar. Bu, Gelişmiş (sınırlı) düzeyde tanılama verilerini paylaşmak üzere ayarlanmamış Windows 7 ve Windows 10 çalıştıran cihazları içermediği anlamına gelir. Windows 10 çalıştıran cihazların %10 ' dan fazlası, tanılama verilerini Gelişmiş (sınırlı) dışındaki düzeylerde paylaşmak üzere ayarlandıysa, **durumu izle** sayfası başlık alanında bir uyarı görüntüler.  

Belirli bir uygulama hakkında daha fazla bilgi görüntülemek için listeden seçin.

## <a name="apps"></a>Uygulamalar

### <a name="health-status-factors"></a>Sağlık durumu faktörleri

![Masaüstü Analizi 'nde bir uygulama için sistem durumu faktörleri](media/monitor-health-status-factors.png)

Masaüstü analizi, uygulamalar için aşağıdaki sistem durumu faktörlerini izler:

- **% Çökme olan cihazlar**: son iki hafta için, bu uygulamanın üzerinde üzerinde çalıştığı cihaz sayısı, uygulamanın kullanıldığı cihaz sayısına göre bölünür. Bu görünüm, yeni işletim sistemi sürümünde uygulama kararlığının arttığını veya azalmadığını görmenizi sağlar. Masaüstü Analizi aşağıdaki kümeler için bu yüzdeyi hesaplar:  

  - **Güncelleştirme sonrasında**: dağıtım planında belirtilen hedef işletim sistemi sürümüne güncelleştirilmiş cihazlar. Yeterli veri içeren varlık sayısını azaltmak için, masaüstü analizi bu verileri güncelleştirilmiş cihazlarınızın tamamına göre toplar. Bu küme, dağıtım planında bulunmayan cihazları içerir.  

  - **Güncelleştirmeden önce**: işletim sistemi sürümünde, dağıtım planında belirtilenden daha önce olan cihazlar. Bu liste Windows 7 çalıştıran cihazları içermez.  

  - **Ticari ort**: tüm ticari cihazlarda ortalama (ort) kilitlenme oranı. Bu ortalama, uygulamanın *Tüm* sürümleri arasında hesaplanır. Sürümünüz ticari ortalamanın üzerinde bir kilitlenme oranı gösteriyorsa, daha kararlı bir sürüm bulunabilir.  

- **Kilitlenmelere sahip% oturum**sayısı: önceki verilerle benzerdir ancak son iki hafta içinde çökmelere sahip oturumların yüzdesini sayar.  

Bir uygulamanın sistem durumunu öğrenmek için, masaüstü analizi en az 20 cihazdan veri gerektirir. Aksi takdirde, uygulama için **yetersiz veri** bildirir. Hizmet, bu cihazlardan gelen *oturum kilitlenme oranına* göre sistem durumunu hesaplar. Cihaz kilitlenme ücreti yalnızca bilgi için sağlanır. Sistem durumu hesaplamasında kullanılmaz.

### <a name="usage"></a>Kullanım

<!-- 5533890 -->

- **Etkin cihazlar**: Bu değer, bir kullanıcının son iki hafta içinde seçili uygulamayı başlattı olan cihazların sayısıdır. Windows 10 ' un hedeflenen sürümünü çalıştıran seçili dağıtım planındaki cihazlara dayalıdır.

- **Oturumlar**: Bu değer, bir kullanıcının hedeflenen Windows sürümünde seçili uygulamayı başlatanın toplam sayısıdır.

### <a name="additional-tabs"></a>Ek sekmeler

Uygulama Ayrıntıları sayfasının en altında, aşağıdaki üç sekme sorunu gidermenize yardımcı olabilir:

- **Diğer sürümler**: Bu uygulamanın alternatif sürümlerinin bir listesi. Her sürüm için, kuruluşunuzda çökme hızlarındaki ve ticari ortadaki ilgili değişiklikleri gösterir. Uygulamanın daha düşük kilitlenme oranına sahip daha sonraki bir sürümünü bulursanız, uygulamanın güncelleştirilmesi yardımcı olabilir.  

    Ayrıca, sürümün gelişmiş öngörülere sahip olup olmadığını gösterir. Daha fazla bilgi için bkz. [Uyumluluk değerlendirmesi](compat-assessment.md).  

- **Popüler sorunlar**: örnek sayısına göre en sık karşılaşılan hata kimliklerinin listesi. Bir hata KIMLIĞI, kilitlenmeyle ilişkili yığın izlemesini tanımlar. Destek için uygulama satıcısı ' nı çağırdığınızda bu KIMLIĞI kullanabilirsiniz.  

- Son kilitlenmeler: uygulamanın yakın zamanda **çöktüğü**cihazların listesi. Hata KIMLIĞI ve diğer ölçütlere göre filtreleyebilirsiniz. Daha geniş bir dağıtım denemeden önce belirli cihazlarda günlükleri toplayıp veya düzeltmeleri deneyerek sorunu gidermek için bu bilgileri kullanın.  

Çözemezseniz önemli bir durum gerileme bulursanız, uygulamanın **yükseltme kararını** **yapılamadı**olarak değiştirin. Bu eylem, güncelleştirmenin bu varlıkla birlikte cihazlara daha sonra dağıtılmasını engeller.

## <a name="see-also"></a>Ayrıca bkz.

- [Masaüstü Analizi 'nde uyumluluk değerlendirmesi](compat-assessment.md)  

- [Masaüstü analizi ile üretime dağıtım](deploy-prod.md)  
