---
title: Yazılım güncelleştirmeleri için kullanılan simgeler
titleSuffix: Configuration Manager
description: Configuration Manager konsolu, eşitlenen güncelleştirme veya yazılım güncelleştirme grubu için bir durumu gösteren simgeler içerir.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0ca0509893ecadc4c54d06ca98c18531959fb941
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608417"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Configuration Manager 'de yazılım güncelleştirmeleri için kullanılan simgeler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Eşitlenen yazılım güncelleştirmeleri Configuration Manager konsolunda görüntülenir ve her yazılım güncelleştirmesinin ilk sütununda belirli bir durumu gösteren bir simge bulunur. Yazılım güncelleştirme grupları ayrıca grupta bulunan yazılım güncelleştirmelerinin durumu hakkında bilgi sağlayan bir simge ile temsil edilir. Bu bölümde yazılım güncelleştirme simgeleri ve her bir simgenin neyi temsil ettiği hakkında bilgi verilmiştir.  

## <a name="icons-for-software-updates"></a>Yazılım Güncelleştirme Simgeleri  
 Eşitlenen yazılım güncelleştirmeleri aşağıdaki simgelerden biriyle gösterilir.  

### <a name="normal-icon"></a>Normal Simgesi  
 ![Normal simge](../media/Normal.jpg) Yeşil oklu simge normal bir yazılım güncelleştirmesini ifade eder.  

 **Açıklama:**  

 Normal yazılım güncelleştirmeleri eşitlenmiştir ve yazılım dağıtımı için kullanılabilir.  

 **İşletimsel Sorunlar:**  

 İşletimsel bir sorun yoktur.  

### <a name="expired-icon"></a>Süresi Doldu Simgesi  
 ![Süre dolma simgesi ](../media/Expired.jpg) Siyah X olan simge, zaman aşımına uğradı bir yazılım güncelleştirmesini temsil eder. Ayrıca, Configuration Manager konsolunda görüntülendiğinde yazılım güncelleştirmesi için süre **dolma** sütununu görüntüleyerek zaman aşımına uğradı yazılım güncelleştirmelerini belirleyebilirsiniz.  

 **Açıklama:**  

 Süresi dolan yazılım güncelleştirmeleri dağa önce istemci bilgisayarlarına dağıtılabilir durumdadır, ancak yazılım güncelleştirmesinin süresi dolduktan sonra yazılım güncelleştirmeleri için artık yeni dağıtımlar oluşturulamaz. Zaman aşımına uğradı yazılım güncelleştirmeleri etkin dağıtımlardan kaldırılır ve artık istemciler için kullanılabilir duruma getirilmeyecektir.  

 **İşletimsel Sorunlar:**  

 İşletimsel bir sorun yoktur.

### <a name="superseded-icon"></a>Yenisiyle Değiştirildi Simgesi  
 ![Yenisiyle değiştirildi simgesi ](../media/Superseded.jpg) sarı yıldız içeren simge yenisiyle değiştirilen bir yazılım güncelleştirmesini temsil eder. Ayrıca, yazılım güncelleştirmesinin **yenisiyle değiştirilmiş** sütununu görüntüleyerek Configuration Manager konsolunda görüntülendiğinde yenisiyle değiştirilen yazılım güncelleştirmelerini belirleyebilirsiniz.  

 **Açıklama:**  

 Yenisiyle değiştirilmiş yazılım güncelleştirmeleri, yazılım güncelleştirmesinin yeni sürümleri ile değiştirilmiştir. Genellikle, başka bir yazılım güncelleştirmesinin yerine geçen bir yazılım güncelleştirmesi aşağıdaki işlemlerden birini veya birkaçını yapar:  

- Önceden sunulan bir veya daha fazla yazılım güncelleştirmesini geliştirir, iyileştirir veya sağladığı düzeltmeye ekler.  

- Yazlım güncelleştirmesi yükleme için onaylanırsa istemcinin yüklediği yazılım güncelleştirme dosyası paketinin verimliliğini artırır. Örneğin, yenisiyle değiştirilen yazılım güncelleştirmesi artık düzeltmeyle veya yeni yazılım güncelleştirmesinin desteklediği işletim sistemleriyle ilgili olmayan dosyalar içerebilir. bu nedenle, bu dosyalar yerine geçen yazılım güncelleştirmesinin dosya paketinde bulunmaz.  

- Bir ürünün daha yeni sürümlerini güncelleştirir veya diğer bir deyişle, bir ürünün daha eski sürümleri ya da yapılandırmaları için artık geçerli değildir. Yazılım güncelleştirmeleri ayrıca dil desteğini genişletmek için değişiklikler yapılmışsa başka güncelleştirmelerin de yerini alabilir. Örneğin, Microsoft 365 uygulamalar için bir ürün güncelleştirmesinin daha sonraki bir düzeltmesi, daha eski bir işletim sistemi için desteği kaldırabilir, ancak ilk yazılım güncelleştirme sürümünde yeni diller için ek destek ekleyebilir.  

  Yazılım Güncelleştirme Noktası Bileşeni özelliklerindeki Yenisiyle Değiştirme Kuralları sekmesinde, yenisiyle değiştirilen yazılım güncelleştirmelerinin nasıl yönetileceğini belirtebilirsiniz. Daha fazla bilgi için, bkz. [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **İşletimsel Sorunlar:**  

  Mümkün olduğunda, yerine geçen yazılım güncelleştirmesini yenisiyle değiştirilen yazılım güncelleştirmesinin yerine istemci bilgisayara dağıtın. Yazılım güncelleştirmesinin yerine geçen yazılım güncelleştirmeleri listesini, yazılım güncelleştirmesi özelliklerindeki **Yenileriyle Değiştirme Bilgileri** sekmesinde görüntüleyebilirsiniz.  

### <a name="invalid-icon"></a>Geçersiz Simgesi  
 ![Geçersiz simge](../media/Invalid.jpg) Kırmızı X içeren simge, geçersiz bir yazılım güncelleştirmesini temsil eder.  

 **Açıklama:**  

 Geçersiz yazılım güncelleştirmeleri etkin bir dağıtımda, ancak bazı nedenlerle içerik (yazılım güncelleştirme dosyaları) kullanılamaz. Bu durumun oluşabileceği senaryolar aşağıda verilmiştir:  

- Yazılım güncelleştirmesini başarıyla dağıtırsınız, ancak yazılım güncelleştirme dosyası dağıtım paketinden kaldırılır ve artık kullanılamaz.  

- Bir sitede yazılım güncelleştirme dağıtımı oluşturursunuz ve dağıtım nesnesi bir alt siteye başarıyla çoğaltılır, ancak dağıtım paketi alt siteye başarıyla çoğaltılmamıştır.  

  **İşletimsel Sorunlar:**  

  Bir yazılım güncelleştirmesi için içerik eksik olduğunda içerik bir dağıtım noktasında kullanılabilir olana kadar istemciler yazılım güncelleştirmesini yükleyemez. **Yeniden dağıtma** eylemini kullanarak içeriği dağıtım noktalarına yeniden dağıtabilirsiniz. Bir üst sitede oluşturulan dağıtımda yazılım güncelleştirmesi için içerik eksik olduğunda, yazılım güncelleştirmesi alt siteye çoğaltılması ya da yeniden dağıtılması gerekir. İçerik yeniden dağıtımı hakkında daha fazla bilgi için bkz. [dağıttığınız Içeriği yönetme](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Yalnızca Meta Veri Simgesi
 ![Yalnızca meta veri simgesi](../media/MetadataOnly.png) Mavi oklu simge, yalnızca meta veri yazılım güncelleştirmesini ifade eder.

 **Açıklama:**  

 Yalnızca meta veri yazılım güncelleştirmeleri raporlama için Configuration Manager konsolunda kullanılabilir. Yazılım güncelleştirme meta verileriyle ilişkili bir yazılım güncelleştirme dosyası olmadığından yalnızca meta veri yazılım güncelleştirmelerini dağıtırsınız veya indiremez.  

 **İşletimsel Sorunlar:**  

 Yalnızca meta veri yazılım güncelleştirmeleri raporlama amacıyla kullanılabilir ve yazılım güncelleştirme dağıtımına yönelik değildir.  

## <a name="icons-for-software-update-groups"></a>Yazılım Güncelleştirme Gruplarına Yönelik Simgeler  
 Yazılım güncelleştirmeleri aşağıdaki simgelerden biriyle gösterilir.  

### <a name="normal-icon"></a>Normal Simgesi  
 ![Yazılım güncelleştirme grupları-normal simge](../media/Normal.jpg) Yeşil oklu simge yalnızca normal yazılım güncelleştirmelerini içeren bir yazılım güncelleştirme grubunu ifade eder.  

 **İşletimsel Sorunlar:**  

 İşletimsel bir sorun yoktur.  

### <a name="expired-icon"></a>Süresi Doldu Simgesi  
 ![Yazılım güncelleştirme grupları-süre sonu simgesi](../media/Expired.jpg) Siyah X içeren simge bir veya daha fazla süresi dolmuş yazılım güncelleştirmesi içeren bir yazılım güncelleştirme grubunu ifade eder.  

 **İşletimsel Sorunlar:**  

 Mümkün olduğunda yazılım güncelleştirme grubunda süresi dolmuş yazılım güncelleştirmelerini kaldırın ya da değiştirin.  

### <a name="superseded-icon"></a>Yenisiyle Değiştirildi Simgesi  
 ![Yazılım güncelleştirme grupları-yenisiyle değiştirildi simgesi](../media/Superseded.jpg) Sarı yıldız içeren simge bir veya daha fazla yenisiyle değiştirilmiş yazılım güncelleştirmesi içeren bir yazılım güncelleştirme grubunu ifade eder.  

 **İşletimsel Sorunlar:**  

 Yazılım güncelleştirme paketinde yenisiyle değiştirilmiş yazılım güncelleştirmesini, mümkün olduğunda yerine geçen yazılım güncelleştirmesiyle değiştirin.  

### <a name="invalid-icon"></a>Geçersiz Simgesi  
 ![Yazılım güncelleştirme grupları-geçersiz simge](../media/Invalid.jpg) Kırmızı X içeren simge bir veya daha fazla geçersiz yazılım güncelleştirmesi içeren bir yazılım güncelleştirme grubunu ifade eder.  

 **İşletimsel Sorunlar:**  

 Bir yazılım güncelleştirmesi için içerik eksik olduğunda içerik bir dağıtım noktasında kullanılabilir olana kadar istemciler yazılım güncelleştirmesini yükleyemez. **Yeniden dağıtma** eylemini kullanarak içeriği dağıtım noktalarına yeniden dağıtabilirsiniz. Bir üst sitede oluşturulan dağıtımda yazılım güncelleştirmesi için içerik eksik olduğunda, yazılım güncelleştirmesinin çoğaltılması veya alt siteye yeniden dağıtılması gerekir. İçerik yeniden dağıtımı hakkında daha fazla bilgi için bkz. [dağıttığınız Içeriği yönetme](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Sonraki adımlar 

[Yazılım güncelleştirmelerini planlama](../plan-design/plan-for-software-updates.md)