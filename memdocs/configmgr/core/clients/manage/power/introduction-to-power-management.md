---
title: Güç yönetimine giriş
titleSuffix: Configuration Manager
description: Configuration Manager 'de güç yönetimine giriş alın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715224"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager güç yönetimi, birçok kuruluşun bilgisayarlarının güç tüketimini izlemek ve azaltmak için ihtiyaç duyduğu gereksinimi ortadan kaldırırlar. Bu özellik, kuruluştaki bilgisayarlara uygun ve tutarlı ayarlar uygulamak için yerleşik Windows güç yönetimi özelliklerinden yararlanır. Bilgisayarlara iş saatleri ve iş dışındaki saatler için farklı güç ayarları uygulayabilirsiniz. Örneğin, iş dışındaki saatlerde bilgisayarlara daha kısıtlayıcı bir güç planı uygulamak isteyebilirsiniz. Bilgisayarların her zaman açık kalması gereken durumlarda, güç yönetimi ayarlarının uygulanmasını engelleyebilirsiniz.  

 Configuration Manager güç yönetimi, kuruluşunuzda güç tüketimini ve bilgisayar güç ayarlarını çözümlemenize yardımcı olan çeşitli raporlar içerir. Raporları, güç yönetimi sorunlarını gidermenize yardımcı olması için de kullanabilirsiniz.  

 Güç yönetiminin nasıl yapılandırılacağı ve kullanılacağı hakkında ayrıntılı bir iş akışı için bkz. [güç yönetimi Için yönetici denetim listesi](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Configuration Manager güç yönetimi, sanal makinelerde desteklenmez. Sanal makinelere güç planları uygulayamaz ve sanal makinelere ilişkin güç verilerini raporlayamazsınız.  

## <a name="the-power-management-workflow"></a>Güç yönetimi iş akışı  
 Configuration Manager ' de güç yönetimini planlamak ve uygulamak için aşağıdaki üç aşamayı kullanın.  

### <a name="monitoring-and-planning-phase"></a>İzleme ve planlama aşaması  
 Güç yönetimi, sitedeki bilgisayarlar için bilgisayar kullanımı ve güç ayarları hakkında veri toplamak üzere Configuration Manager donanım envanterini kullanır. Bu verileri çözümlemek ve bilgisayarlara yönelik en iyi güç yönetimi ayarlarını belirlemek için kullanabileceğiniz çeşitli raporlar bulunur. Örneğin, güç yönetimi iş akışının izleme ve planlama aşamasında, **Güç Özellikleri** raporunda yer alan verileri temel alan koleksiyonlar oluşturabilir ve bu verileri güç yönetimi özelliği olmayan bilgisayarları belirlemek için kullanabilirsiniz. Daha sonra bu bilgisayarları güç yönetiminin dışında bırakabilirsiniz.  

> [!IMPORTANT]  
>  Güç planlarını sitenizdeki bilgisayarlara uygulamadan önce istemci bilgisayarlardan güç verilerini toplayıp çözümlemeniz gerekir. Bilgisayarlara yeni güç ayarlarını mevcut ayarları incelemeden uygularsanız, güç tüketiminde artışla karşılaşabilirsiniz.  

### <a name="enforcement-phase"></a>Zorlama aşaması  
 Güç yönetimi, sitenizdeki bilgisayar koleksiyonlarına uygulayabileceğiniz güç planları oluşturmanıza olanak sağlar. Bu güç planları, bilgisayarlarda Windows güç yönetimi ayarlarını yapılandırır. Configuration Manager bulunan güç planlarını kullanabilir veya kendi özel güç planlarınızı yapılandırabilirsiniz. Bilgisayarlara güç planı uyguladıktan sonra izleme ve planlama aşamasında toplanan güç verilerini, güç tasarrufunu değerlendirmek için bir temel olarak kullanabilirsiniz. Daha fazla bilgi için bkz. [güç yönetimi Için yönetici denetim listesi](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Uyumluluk aşaması  
 Uyumluluk aşamasında, kuruluşunuzdaki güç kullanımını ve güç maliyeti tasarrufunu değerlendirmenize yardımcı olan raporlar çalıştırabilirsiniz. Ayrıca, bilgisayarlar tarafından oluşturulan CO2 miktardaki iyileştirmeleri tanımlayan raporlar çalıştırabilirsiniz. Bunların yanı sıra güç ayarlarının bilgisayarlara doğru olarak uygulandığını doğrulamanıza ve güç yönetimi özelliğiyle ilgili sorunları gidermenize yardımcı olan raporlar da bulunur.  
