---
title: Ortak yönetim ile istemci durumu
titleSuffix: Configuration Manager
description: Azure portal Intune 'dan Configuration Manager istemci durumunun görünürlüğünü koruyun
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711199"
---
# <a name="client-health-with-co-management"></a>Ortak yönetim ile istemci durumu

Ağınızın sistem durumu, içindeki ve olmayan cihazların sistem durumuna doğrudan bağlanır. Intune, ağınızda olmasa bile sağlıksız bir istemciyle iletişim kurabilir. Bu özelliği, bilinen sağlıklı istemcilerin %98 ' ını geri bildirebilme olanağı Configuration Manager ile birleştirmek için ortak yönetimi kullanın. Böylece, gerçek zamanlı olarak tüm istemcileri tespit edebilir, değerlendirebilir ve görünürlük sağlayabilirsiniz. Intune, tüm bağlı istemciler arasında uyumluluk yükseltmeleri için gereken desteği de ekler.

Aşağıdaki videoda, üst düzey Program Yöneticisi ramiz York ve ürün pazarlama yöneticisi Locky Ainley tartışın ve ortak yönetim ile demo istemci sistem durumu:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Avantajlar

İstemci sistem durumunun değerlendirme bir üst önceliktir. System Center 2012 Configuration Manager **Ccmeval**ekledi. Bu yardımcı program Configuration Manager istemcisinin dışında. İstemci sistem durumu izleme ve otomatik düzeltme sağlar. Ancak, bu raporlama, iç ağınızdaki fiziksel veya neredeyse bir cihaza dayanır. Ortak yönetim, bu sorunu ele almanıza yardımcı olur.

Ortak yönetim sayesinde Intune, istemci sistem durumu hakkında rapor verebilir. Verilerin geçerliliği için zaman damgası bilgileri sağlar. Bu bilgiler, cihazlarınızın sağlıklı olup olmadığını, bağlanıp bağlanamadığını, uygulamaları yükleyebileceklerini veya gerekli işletim sistemi yapılarına güncelleştirme yapabileceklerini bildirir. 

Bu özelliğe ilişkin ayrıntılı bir genel bakış için bu videoyu, Ignite 2018 [Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) oturumdaki yenilikler bölümüne bakın.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Configuration Manager, istemcinin yüklü olduğu ancak cihaz durumunu sunmadığında, Intune istemciye bağlanmaya gerek kalmadan daha fazla bilgi sağlayabilir. Intune 'da cihaz sistem durumu bilgilerinin anlaşılması kolaydır. Durum **sağlıklı**olmayan bir şeydir, sorun gidermek ve çözmek için öneriler ve sonraki adımlar sağlar.

> [!Note]  
> Gelecekteki bir sürüm için aşağıdaki avantajlar planlanmaktadır:
> - Configuration Manager CCMeval 'e ek işlevsellik dahil edilecek  
> - Hem Configuration Manager hem de Intune 'da sağlıksız olabilecek makineleri belirlemek daha kolay olacaktır  
> - İstemci sistem durumu verilerini Intune 'da gruplandırabilirsiniz  



## <a name="value-proposition"></a>Değer teklifi

Bu özellik sayesinde artık Intune ile bir dış veri kaynağınız vardır. Büyük bir istemci sorunları dizisinde sorun gidermeye yönelik sonraki adımları belirlemenizi sağlar. Artık istemci verilerini geri çekmek için ek raporlar oluşturmanız veya diğer araçları kullanmanız gerekmez.

Sağlıklı istemcileriniz varsa, düzeltme eki uyumluluğunu daha önce güncelleştirmiş olursunuz. Daha iyi düzeltme eki uyumluluğu daha iyi güvenlik anlamına gelir.



## <a name="configure"></a>Yapılandırma

Bu özelliği kullanmaya başlamak için aşağıdaki adımları kullanın:

- Cihazları Windows 10, sürüm 1709 veya sonraki sürümlere güncelleştirme  

- [Ortak yönetimi etkinleştirme](how-to-enable.md)  
    - Herhangi bir iş yükünü Intune 'a geçmeniz gerekmez  

- Configuration Manager sitenizi ve istemcilerinizi *sürüm 1806* veya üzeri bir sürüme güncelleştirin  


### <a name="review-configuration-manager-client-health-in-intune"></a>Intune 'da Configuration Manager istemci durumunu gözden geçirme

1. [Azure Portal](https://portal.azure.com/)oturum açın.  

2. **Tüm hizmetler** > **Intune**' ı seçin. Intune, **İzleme + Yönetim** bölümünde bulunur.  

3. **Microsoft Intune** bölmesini açtıktan sonra **Yardım ve destek**altındaki menüde **sorun giderme** sayfasına gidin.  

4. **Kullanıcı Seç** seçeneğini kullanın, **cihazlar** listesinde belirli bir cihazı bulun ve cihaz sayfasını açmak için seçin.  

5. Ortak yönetim bilgileri, cihaz sayfasının alt kısmında gösterilir. Bu bilgiler, istemci sistem durumu için aşağıdaki alanları içerir:  
    - **Configuration Manager Aracı durumu**  
    - **Son Configuration Manager aracı denetimi zamanı**  

> [!Tip]  
> Intune 'a kayıtlı cihazlar, yaklaşık olarak her sekiz saatte bir günde üç kez bulut hizmetine bağlanır. 
