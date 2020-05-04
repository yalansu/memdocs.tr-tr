---
title: Güç yönetimi için yönetici denetim listesi
titleSuffix: Configuration Manager
description: Configuration Manager ' de güç yönetimini planlayıp uygulamanıza yardımcı olması için yönetici denetim listesini kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715287"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimi için yönetici denetim listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu yönetici denetim listesi, kuruluşunuzda Configuration Manager güç yönetimi kullanmak için önerilen adımları sağlar.  

## <a name="configuring-power-management"></a>Güç yönetimini yapılandırma  
 İstemci bilgisayarlardan güç yönetimi bilgilerini toplamak üzere hiyerarşi yapılandırmanıza yardımcı olması için aşağıdaki adımları kullanın.  

> [!IMPORTANT]  
>  İstemci bilgisayarlardan güç verilerini toplayıp çözümleyinceye kadar güç planlarını hiyerarşinizdeki bilgisayarlara uygulamayın. Bilgisayarlara yeni güç ayarlarını mevcut ayarları incelemeden uygularsanız, güç tüketiminde artış oluşabilir.  

|Görev|Ayrıntılar|  
|----------|-------------|  
|Configuration Manager belge kitaplığındaki güç yönetimi kavramlarını gözden geçirin.|Bkz. [güç yönetimine giriş](introduction-to-power-management.md).|  
|Configuration Manager belge kitaplığındaki güç yönetimi önkoşullarını gözden geçirin.|Bkz. [güç yönetimi önkoşulları](prerequisites-for-power-management.md).|  
|Güç yönetimi için en iyi yöntem bilgilerini gözden geçirin.|Bkz. [güç yönetimi Için en iyi uygulamalar](best-practices-for-power-management.md).|  
|Koleksiyonlarınızı Ortamınızdaki bilgisayarlardan güç tüketimini yönetecek şekilde yapılandırın.|**Taban çizgisi verilerinin raporlanması**, **taban çizgisi verilerinin raporlanması için**koleksiyon, **güç yönetimi özelliğine sahip bilgisayarların toplanması**, güç planlarının uygulanacağı bilgisayar **koleksiyonları**, **güç planlarının uygulanacağı**bilgisayar koleksiyonları ve **Windows Server çalıştıran bilgisayar** koleksiyonları, hiyerarşinizdeki bilgisayarların güç ayarlarını yönetmenize yardımcı olmak için kullanın. Birden çok koleksiyon oluşturabilir ve her koleksiyona farklı güç planları uygulayabilirsiniz.|  
|Güç yönetimini etkinleştirin.|Güç yönetimini kullanmaya başlayabilmeniz için etkinleştirmeniz ve gerekli istemci ayarlarını yapılandırmanız gerekir. Daha fazla bilgi için bkz. [güç yönetimini yapılandırma](configuring-power-management.md).|  
|İstemci bilgisayarlardan güç yönetimi bilgilerini toplayın.|Güç yönetimi verileri istemciler tarafından Configuration Manager donanım envanteri aracılığıyla bildirilir. Yapılandırdığınız donanım envanteri zamanlamasına bağlı olarak, tüm istemci bilgisayarlardan envanter alınması biraz zaman alabilir.|  

## <a name="monitoring-and-planning-phase"></a>İzleme ve planlama aşaması  

|Görev|Ayrıntılar|  
|----------|-------------|  
|**Bilgisayar Etkinliği** raporunu çalıştırın.|**Bilgisayar Etkinliği** raporu, belirtilen süre boyunca belirtilen bir koleksiyon için monitör, bilgisayar ve kullanıcı etkinliğini gösteren grafiği görüntüler. Bu rapor, belirtilen koleksiyondaki bilgisayarların uyku ve uyandırma özelliklerini gösteren **Bilgisayar Etkinliği Ayrıntıları** raporuna bağlanır. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Enerji Tüketimi** veya **Günlük Enerji Tüketimi**raporunu çalıştırın.|**Enerji Tüketimi** ve **Günlük Enerji Tüketimi** raporları belirli bir süre içinde belirtilen bir koleksiyon için toplam aylık güç tüketimini saat başına kilowatt (kWh) cinsinden görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Çevre Etkisi** veya  **Günlük Çevre Etkisi**raporunu çalıştırın.|**Çevre Etkisi** ve **Günlük Çevre Etkisi** raporları belirli bir süre için belirtilen bir bilgisayar koleksiyonu tarafından tasarruf edilen karbon dioksit (CO2) emisyonlarını gösteren bir grafiği görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Enerji Maliyeti** veya **Günlük Enerji Maliyeti**raporunu çalıştırın.|**Enerji Maliyeti** ve **Günlük Enerji Maliyeti** raporları belirli bir süre için toplam güç tüketimi maliyetini görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Güç Özellikleri**raporunu çalıştırın.|**Güç Özellikleri** raporu, belirtilen koleksiyondaki bilgisayarların güç yönetimi özelliklerini görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Güç Ayarları**raporunu çalıştırın.|**Güç Ayarları** raporu, belirli bir koleksiyondaki bilgisayarlar tarafından kullanılan geçerli güç ayarlarının toplu listesini görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|Tüm zorunlu bilgisayar koleksiyonlarını güç yönetiminin dışında bırakın.|Bkz. [güç yönetimini yapılandırma](configuring-power-management.md).|  

> [!IMPORTANT]  
>  İzleme ve planlama aşaması sırasında oluşturulan güç yönetimi raporlarından bilgileri kaydettiğinizden emin olun. Bu verileri, hiyerarşinizdeki bilgisayarlara bir güç planı uygulama sonucundaki güç kullanımı, güç maliyeti ve çevre etkisi tasarruflarını değerlendirmenize yardımcı olması için zorlama ve uyumluluk aşamaları sırasında oluşturulan güç yönetimi bilgileriyle karşılaştırabilirsiniz.  

## <a name="enforcement-phase"></a>Zorlama aşaması  

|Görev|Ayrıntılar|  
|----------|-------------|  
|Kuruluşunuzdaki bilgisayarların koleksiyonları için var olan güç planlarını seçin veya yeni güç planları oluşturun.|Bkz. [güç planları oluşturma ve uygulama](create-and-apply-power-plans.md).|  
|Bu güç planlarını bilgisayarlara uygulayın.|Bkz. [güç planları oluşturma ve uygulama](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Uyumluluk aşaması  

|Görev|Ayrıntılar|  
|----------|-------------|  
|**Bilgisayar Etkinliği** raporunu çalıştırın.|**Bilgisayar Etkinliği** raporu, belirtilen süre boyunca belirtilen bir koleksiyon için monitör, bilgisayar ve kullanıcı etkinliğini gösteren grafiği görüntüler. Bu rapor, belirtilen koleksiyondaki bilgisayarların uyku ve uyandırma özelliklerini gösteren **Güç Bilgisayar Etkinliği Ayrıntıları** raporuna bağlanır. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Enerji Tüketimi** veya **Günlük Enerji Tüketimi**raporunu çalıştırın.|**Enerji Tüketimi** ve **Günlük Enerji Tüketimi** raporları belirli bir süre içinde belirtilen bir koleksiyon için toplam aylık güç tüketimini saat başına kilowatt (kWh) cinsinden görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Çevre Etkisi** veya **Günlük Çevre Etkisi**raporunu çalıştırın.|**Çevre Etkisi** ve **Günlük Çevre Etkisi** raporları belirli bir süre için belirtilen bir bilgisayar koleksiyonu tarafından tasarruf edilen karbon dioksit (CO2) emisyonlarını gösteren bir grafiği görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|**Enerji Maliyeti** veya **Günlük Enerji Maliyeti**raporunu çalıştırın.|**Enerji Maliyeti** ve **Günlük Enerji Maliyeti** raporları belirli bir süre için toplam güç tüketimi maliyetini görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Sorun giderme  

|Görev|Ayrıntılar|  
|----------|-------------|  
|Hiyerarşinizdeki bilgisayarlar uyku veya hazırda bekleme moduna girmediyse, olası nedenleri görüntülemek için **Uyku Moduna Geçmeme Raporu** ’nu çalıştırın.|**Uyku Moduna Geçmeme Raporu** , bilgisayarların uyku moduna geçmesini veya hazırda beklemesini engelleyen temel nedenlerin listesini ve belirtilen süre boyunca her bir nedenden etkilenen bilgisayar sayısını görüntüler. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md).|  
|Bir bilgisayara birden çok güç planı uygulanırsa en az kısıtlayıcı güç planı uygulanır. Birden çok güç planının uygulandığı bilgisayarları görmek için **Birden Çok Güç Planına Sahip Bilgisayarlar** raporunu çalıştırın.|[Güç yönetimini izleme ve planlama konusunda](monitor-and-plan-for-power-management.md) **birden çok güç planına sahip olan bilgisayarlara** bakın.|  
