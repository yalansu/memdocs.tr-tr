---
title: Endpoint Protection durumunu izleme
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşinizde izleme Endpoint Protection öğrenin.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722280"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Endpoint Protection durumunu izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Configuration Manager hiyerarşinizdeki Endpoint Protection, **izleme** çalışma alanındaki **güvenlik** altında bulunan **Endpoint Protection durum** düğümünü, **varlıklar ve uyum** çalışma alanındaki **Endpoint Protection** düğümünü ve raporları kullanarak izleyebilirsiniz.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a>Endpoint Protection durum düğümünü kullanarak Endpoint Protection Izleme  

1. Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2. **İzleme** çalışma alanında, **güvenlik** ' i genişletin ve ardından **Endpoint Protection durum**' a tıklayın.  

3. **Koleksiyon** listesinde, durum bilgilerini görüntülemek istediğiniz koleksiyonu seçin.  

   > [!IMPORTANT]
   >  Koleksiyonlar aşağıdaki durumlarda seçilebilir:  
   > 
   > - **Endpoint Protection panosunda bu koleksiyonu görüntüle '** yi seçtiğinizde <em><koleksiyonu\>adı</em>**Özellikler** iletişim kutusunun **Uyarılar** sekmesinde.  
   >   -   Koleksiyona bir Endpoint Protection kötü amaçlı yazılımdan koruma İlkesi dağıttığınızda.  
   >   -   Endpoint Protection istemci ayarlarını etkinleştirir ve koleksiyona dağıttığınızda.  

4. **Güvenlik durumu** ve **işletimsel durum** bölümlerinde görüntülenen bilgileri gözden geçirin. **Varlıklar ve Uyumluluk** çalışma alanının **Cihazlar** düğümünde geçici bir koleksiyon oluşturmak için herhangi bir durum bağlantısına tıklayabilirsiniz. Geçici koleksiyon seçili duruma sahip bilgisayarları içerir.  

   > [!IMPORTANT]  
   >  **Endpoint Protection durumu** düğümünde görüntülenen bilgiler, Configuration Manager veritabanından özetlenen son verileri temel alır ve geçerli olmayabilir. En son verileri almak istiyorsanız **Giriş** sekmesinde **Özetlemeyi Çalıştır**’a tıklayın veya **Özetlemeyi Zamanla** ’ya tıklayarak özetleme aralığını ayarlayın.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a>Varlıklar ve uyum çalışma alanında Endpoint Protection Izleme  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve uyum** çalışma alanında aşağıdaki eylemlerden birini gerçekleştirin:  

    -   **Cihazlar**’a tıklayın. **Varlıklar ve Uyumluluk** listesinde bir bilgisayar seçin ve ardından **Kötü Amaçlı Yazılım Ayrıntısı** sekmesine tıklayın.  

    -   **Cihaz Koleksiyonları**' na tıklayın. **Cihaz Koleksiyonları** listesinde, izlemek istediğiniz bilgisayarı içeren koleksiyonu seçin ve ardından **giriş** sekmesindeki **koleksiyon** grubunda **üyeleri göster**' e tıklayın.  

3.  *<koleksiyonu adı\> * listesinde bir bilgisayar seçin ve ardından **kötü amaçlı yazılım ayrıntısı** sekmesine tıklayın.  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a>Raporları kullanarak Endpoint Protection Izleme  
 Hiyerarşinizdeki Endpoint Protection hakkındaki bilgileri görüntülemenize yardımcı olması için aşağıdaki raporları kullanın. Bu raporları, Endpoint Protection sorunları gidermeye yardımcı olması için de kullanabilirsiniz. Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md) ve [günlük dosyaları](../../core/plan-design/hierarchy/log-files.md). Endpoint Protection raporları Endpoint Protection klasöründedir.  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Kötü Amaçlı Yazılımdan Koruma Etkinlik Raporu**|Belirtilen koleksiyon için kötü amaçlı yazılımdan koruma etkinliğine genel bakışı gösterir.|  
|**Etkilenen Bilgisayarlar**|Belirtilen tehdidin algılandığı bilgisayarların listesini gösterir.|  
|**Tehditlere göre İlk Kullanıcılar**|En fazla algılanan tehdide sahip kullanıcıların listesini görüntüler.|  
|**Kullanıcı Tehdit Listesi**|Belirtilen kullanıcı hesabı için bulunan tehditlerin listesini görüntüler.|  

## <a name="malware-alert-levels"></a>Kötü amaçlı yazılım uyarı düzeyleri  
 Raporlarda veya Configuration Manager konsolunda görüntülenebilen farklı Endpoint Protection uyarı düzeylerini tanımlamak için aşağıdaki tabloyu kullanın.  

|Uyarı düzeyi|Açıklama|  
|-----------------|-----------------|  
|**Başaramadı**|Endpoint Protection kötü amaçlı yazılımı düzeltemedi. Hatanın ayrıntıları için günlüklerinizi denetleyin.<br /><br /> **Note:** Configuration Manager ve Endpoint Protection günlük dosyalarının listesi için [günlük dosyaları](../../core/plan-design/hierarchy/log-files.md) konusunun "Endpoint Protection" bölümüne bakın.|  
|**Kaldırıldı**|Endpoint Protection kötü amaçlı yazılımı başarıyla kaldırdı.|  
|**Karantinaya Alındı**|Endpoint Protection kötü amaçlı yazılımı güvenli bir konuma taşıdı ve siz kaldırana veya çalışmasına izin verene kadar çalışmasını engelledi.|  
|**Temizlendi**|Kötü amaçlı yazılım, etkilenen dosyadan temizlendi.|  
|**İzin verildi**|Bir yönetim kullanıcısı, kötü amaçlı yazılımı içeren yazılımın çalışmasına izin vermeyi seçti.|  
|**Eylem Yok**|Endpoint Protection kötü amaçlı yazılım üzerinde hiçbir işlem gerçekleştirmesiz. Kötü amaçlı yazılım algılandıktan sonra bilgisayar yeniden başlatılır ve kötü amaçlı yazılım artık algılanmazsa bu durum oluşabilir; örneğin, kötü amaçlı yazılımın algılandığı eşlenen bir ağ sürücüsü, bilgisayar yeniden başlatıldığında yeniden bağlantı kurmaz.|  
|**Engellendi**|Endpoint Protection kötü amaçlı yazılımın çalışmasını engelledi. Bu durum, bilgisayardaki bir işlemin kötü amaçlı yazılım içerdiği bulunursa ortaya çıkabilir.|
