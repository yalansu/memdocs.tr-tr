---
title: Geçişi tamamlama
titleSuffix: Configuration Manager
description: Kaynak hiyerarşisinin artık verileri yoksa, Configuration Manager geçerli dal hedefi hiyerarşisine geçişi nasıl tamamlayacağınızı öğrenin.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76cf6b57a4bc1439f2aa9c2e0484271987f85748
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713012"
---
# <a name="plan-to-complete-migration-in-configuration-manager"></a>Configuration Manager geçişi tamamlamayı planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, bir kaynak hiyerarşisi hedef hiyerarşinize geçirmek istediğiniz verileri artık olmadığında geçiş işlemini tamamlayabilirsiniz. Geçişin tamamlanması aşağıdaki genel adımları içerir:  

-   İhtiyacınız olan verilerin geçirildiğinden emin olun. Kaynak hiyerarşiden geçişi tamamlamadan önce, hedef hiyerarşisinde gerekli olan kaynak hiyerarşisinden tüm kaynakları başarıyla geçirdiğinizden emin olun. Bu, veri ve istemcileri içerebilir.  

-   Kaynak sitelerden veri toplamayı durdurun. Bir kaynak hiyerarşisinden geçişi tamamlayabilmeniz için öncelikle kaynak sitelerden veri toplamayı durdurmanız gerekir.  

-   Geçiş verilerini temizleyin. Kaynak hiyerarşisindeki tüm kaynak sitelerden veri toplamayı durdurduktan sonra, geçiş işlemi ve kaynak hiyerarşisi hakkındaki verileri hedef hiyerarşisinin veritabanından kaldırabilirsiniz.  

-   Kaynak hiyerarşisinin yetkisini alın. Bir kaynak hiyerarşisinden geçişi tamamladıktan ve bu hiyerarşinin artık yönettiğiniz kaynakları yoksa, kaynak hiyerarşisindeki sitelerin yetkisini alabilir ve ilgili altyapıyı ortamınızdan kaldırabilirsiniz. Sitelerin ve kaynak hiyerarşilerinin yetkisini alma hakkında daha fazla bilgi için, bu Configuration Manager sürümü için belgelere başvurun.  

Veri toplamayı durdurup geçiş verilerini temizleyerek bir kaynak hiyerarşisinden geçişi tamamlamayı planlamaya yardımcı olması için aşağıdaki bölümleri kullanın:  

-   [Veri toplamayı durdurmayı planlayın](#Plan_to_Stop_Data_Gath)  

-   [Geçiş verilerini temizlemeyi planlayın](#Plan_to_clean_up)  

##  <a name="plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a>Veri toplamayı durdurmayı planlayın  
 Geçişi tamamlayıp geçiş verilerini temizlemeden önce, kaynak hiyerarşisindeki her kaynak siteden veri toplamayı durdurmanız gerekir. Her kaynak siteden veri toplamayı durdurmak için, en alt katman kaynak sitelerde **veri toplamayı durdur** komutunu gerçekleştirmeniz ve ardından her üst sitede işlemi tekrarlamanız gerekir. Kaynak hiyerarşisinin en üst düzeydeki sitesi, veri toplamayı durdurduğunuz son site olmalıdır. Bir üst sitede bu komutu gerçekleştirmeden önce her bir alt sitede veri toplamayı durdurmanız gerekir. Genellikle, yalnızca geçiş işlemini bitirmeye hazırsanız verileri toplamayı durdurursunuz.  

 Kaynak siteden veri toplamayı durdurduktan sonra, bu siteden paylaşılan dağıtım noktaları artık hedef hiyerarşideki istemciler için içerik konumları olarak kullanılamaz. Bu nedenle, hedef hiyerarşideki istemcilerin erişim gerektirdiğinden, aşağıdaki seçeneklerden birini kullanarak kullanılabilir olmaya devam ettiğinden emin olun:  

-   Hedef hiyerarşisinde, içeriği en az bir dağıtım noktasına dağıtın.  

-   Bir kaynak siteden veri toplamayı durdurmadan önce, gerekli içeriğe sahip paylaşılan dağıtım noktalarını yükseltin veya yeniden atayın. Paylaşılan dağıtım noktalarını yükseltme veya yeniden atama hakkında daha fazla bilgi için, [içerik dağıtımı geçiş stratejisi planlama](../../core/migration/planning-a-content-deployment-migration-strategy.md)konusundaki ilgili bölümlere bakın.  

Kaynak hiyerarşisindeki her kaynak siteden veri toplamayı durdurduktan sonra, geçiş verilerini temizleyebilirsiniz. Geçiş verilerini temizleyene kadar, çalışan veya çalıştırmaya zamanlanan her geçiş işi Configuration Manager konsolunda erişilebilir durumda kalır.  

Kaynak siteleri ve veri toplama hakkında daha fazla bilgi için bkz. [kaynak hiyerarşi stratejisi planlama](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a>Geçiş verilerini temizlemeyi planlayın  
 Geçişi tamamlaması için gereken son adım, geçiş verilerini temizleyelim. Kaynak hiyerarşisindeki her bir kaynak site için veri toplamayı durdurduktan sonra **geçiş verilerini temizle** komutunu kullanabilirsiniz. Bu isteğe bağlı eylem, geçerli kaynak hiyerarşisiyle ilgili verileri hedef hiyerarşinin veritabanından kaldırır.  

 Geçiş verilerini temizlediğinizde, geçiş hakkındaki verilerin çoğu hedef hiyerarşinin veritabanından kaldırılır. Ancak, geçirilen nesnelerle ilgili ayrıntılar korunur. Bu ayrıntılarla, **geçiş** çalışma alanını, geçirilen verilerin bulunduğu kaynak hiyerarşisini yeniden yapılandırmak veya daha önce geçirilen nesnelerin nesne ve site sahipliğini gözden geçirmek için kullanabilirsiniz.  
