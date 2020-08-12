---
title: Configuration Manager konsol bildirimleri
titleSuffix: Configuration Manager
description: Configuration Manager konsolundan bildirimler hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129687"
---
# <a name="configuration-manager-console-notifications"></a>Configuration Manager konsol bildirimleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3556016, fka 1318035-->
Configuration Manager sürüm 1902 ' den başlayarak, Configuration Manager konsolu size oluşan belirli olayları bildirir. Configuration Manager siteleriniz için bazı olay bildirimlerini yapılandırabilirsiniz.

- Yapılandırılamayan olay bildirimleri:
   - Configuration Manager için bir güncelleştirme kullanılabilir olduğunda
   - Ortamda yaşam döngüsü ve bakım olayları gerçekleştiğinde
- Yapılandırılabilir olay bildirimleri:
   - [Kritik olmayan site durumu değişiklikleri](#bkmk_noncrit)
   - [Microsoft 'Tan iletiler](#bkmk_msft) (sürüm 2006 ' den başlayarak)

Bu bildirim, şeridin altındaki konsol penceresinin en üstünde yer aldığı bir çubukdur. Configuration Manager güncelleştirmeler kullanılabilir olduğunda önceki deneyimin yerini alır. Bu konsol içi bildirimlerde hala kritik bilgiler görüntülenir, ancak konsolda çalışmalarınız kesintiye uğramaz. Kritik bildirimleri yok sayabilirsiniz. Konsol, tüm bildirimleri başlık çubuğunun yeni bir bildirim alanında görüntüler.

![Konsolda bildirim çubuğu ve bayrak](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a>Bir siteyi kritik olmayan bildirimleri gösterecek şekilde yapılandırma

Her bir siteyi, sitenin özelliklerinde kritik olmayan bildirimler gösterecek şekilde yapılandırabilirsiniz.

1. **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.
1. Kritik olmayan bildirimler için yapılandırmak istediğiniz siteyi seçin.
1. Şeritte **Özellikler**' i seçin.
1. **Uyarılar** sekmesinde, **kritik olmayan site sistem durumu değişiklikleri Için konsol bildirimlerini etkinleştirme**seçeneğini belirleyin.
   - Bu ayarı etkinleştirirseniz, tüm konsol kullanıcıları kritik, uyarı ve bilgi bildirimlerini görür. Bu ayar varsayılan olarak etkindir.  
   - Bu ayarı devre dışı bırakırsanız, konsol kullanıcıları yalnızca kritik bildirimleri görür.  

Çoğu konsol bildirimi oturum başına alınır. Konsol, bir kullanıcı tarafından başlatıldığında sorguları değerlendirir. Bildirimlerde değişiklikleri görmek için konsolunu yeniden başlatın. Bir kullanıcı kritik olmayan bir bildirimi geri alıyorsa, hala uygunsa konsol yeniden başlatıldığında yeniden bildirir.

Aşağıdaki bildirimler beş dakikada bir yeniden değerlendirmeye sahiptir:

- Site bakım modunda  
- Site kurtarma modunda  
- Site yükseltme modunda  

Bildirimler rol tabanlı yönetimin izinlerini izler. Örneğin, bir kullanıcının Configuration Manager güncelleştirmelerini görme izni yoksa, bu bildirimleri görmez.

Bazı bildirimlerin ilgili bir eylemi vardır. Örneğin, konsol sürümü site sürümüyle eşleşmiyorsa, **Yeni konsol sürümünü yükler**' i seçin. Bu eylem konsol yükleyicisini başlatır.

Sürüm 2006 ' den başlayarak, Azure hizmetleri 'ni buluta eklemek üzere yapılandırırsanız, [gizli anahtarı yenilemek](../deploy/configure/azure-services-wizard.md#bkmk_renew)için bir eylem içeren bildirimler görürsünüz.<!--6386392--> Site, aşağıdaki uyarıların durumunu saat başına bir kez değerlendirir:

- Bir veya daha fazla Azure AD uygulama gizli anahtarı yakında dolacak
- Bir veya daha fazla Azure AD uygulama gizli anahtarının geçerliliği bitti

Aşağıdaki bildirimler, en çok Technical Preview dalı için geçerlidir:  

- Değerlendirme sürümü süre sonu 30 gün içinde (uyarı): geçerli tarih, değerlendirme sürümünün son kullanma tarihinden itibaren 30 gün içinde  
- Değerlendirme sürümünün süresi doldu (kritik): geçerli tarih, değerlendirme sürümünün sona erme tarihinden geçti  
- Konsol sürümü uyumsuzluğu (kritik): konsol sürümü site sürümüyle eşleşmiyor  
- Site yükseltme kullanılabilir (uyarı): yeni bir güncelleştirme paketi var  

Daha fazla bilgi ve sorun giderme yardımı için konsol bilgisayarındaki **Smsadminuı. log** dosyasına bakın. Varsayılan olarak, bu günlük dosyası şu yolda olur: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log` .

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a>Bir siteyi Microsoft 'tan iletiler alacak şekilde yapılandırma
 <!--3953121-->

Sürüm 2006 ' den başlayarak, Microsoft 'tan Configuration Manager konsolunda bildirimleri almayı seçebilirsiniz. Bu bildirimler yeni veya güncelleştirilmiş özellikler, Configuration Manager ve ekli hizmetlerde yapılan değişiklikler ve Düzeltme eylemi gerektiren sorunlar hakkında bilgi almanıza yardımcı olur.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Microsoft iletileri için bildirim ayarlarını yapılandırma

1. **Yönetim**  >  **sitesi yapılandırma**  >  **siteleri**' ne gidin.
1. Siteye sağ tıklayıp **Özellikler**' i seçin.
1. **Uyarılar** sekmesinde, **Microsoft 'tan ileti al**' ı seçerek bildirimleri etkinleştirin. Bunları almamayı tercih ediyorsanız aşağıdaki bildirimlerin herhangi birini kaldırabilirsiniz:  
   - **Engelleme/çözme**: kuruluşunuzu etkileyen, işlem yapmanız gereken bilinen sorunlar.
   - **Değişiklik planı**: işlem yapmanız gereken Configuration Manager değişiklikler.
   - **Bilgilendirmeye**devam edin: yeni veya güncelleştirilmiş özellikleri size bildirir.

     [![Site özelliklerindeki Microsoft seçeneklerinin bildirimi](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Sonraki adımlar

- [Konsolu kullanma](admin-console.md)
- [Konsol ipuçları](admin-console-tips.md)
- [Erişilebilirlik özellikleri](../../understand/accessibility-features.md)
