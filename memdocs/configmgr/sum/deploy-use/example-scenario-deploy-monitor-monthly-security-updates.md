---
title: Güncelleştirmeleri dağıtmak ve izlemek için örnek senaryo
titleSuffix: Configuration Manager
description: Aylık yazılım güncelleştirmelerini dağıtmak ve izlemek için Configuration Manager ' de yazılım güncelleştirmelerini kullanma.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714916"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Aylık yazılım güncelleştirmelerini dağıtmak ve izlemek için örnek senaryo

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konuda, Microsoft 'un aylık olarak çalıştığı güvenlik yazılım güncelleştirmelerini dağıtmak ve izlemek için Configuration Manager ' de yazılım güncelleştirmelerini nasıl kullanabileceğinizi gösteren örnek bir senaryo sunulmaktadır.  

 Bu senaryoda, Woodgrove Bank konumundaki Configuration Manager yöneticisinin eylemlerini izliyoruz. Yöneticinin aşağıdaki koşullar ve gereksinimlerle bir yazılım güncelleştirme dağıtımı stratejisi oluşturması gerekir:  

- Etkin yazılım güncelleştirme dağıtımı, Microsoft tarafından her ayın ikinci Salı günü yayınlanan güvenlik yazılımı güncelleştirmelerinden bir hafta sonra gerçekleşir. Bu olay genellikle Salı Düzeltme Eki olarak adlandırılır.  

- Yazılım güncelleştirmeleri indirilir ve dağıtım noktalarında hazırlanır. Daha sonra, ConfigMgr Yöneticisi, yazılım güncelleştirmelerini üretim ortamında tamamen dağıtmadan önce bir dağıtım istemci alt kümesiyle test edilir.  

- Yöneticinin, yazılım güncelleştirmelerinin uyumluluğunu aya veya yıla göre izleyebilmesi gerekir.  

  Bu senaryo, yazılım güncelleştirme noktası altyapısının zaten uygulanmış olduğunu varsayar. Configuration Manager ' de yazılım güncelleştirmelerini planlamak ve yapılandırmak için aşağıdaki bilgileri kullanın.  

|İşleme|Başvuru|  
|-------------|---------------|  
|Yazılım güncelleştirmeleri için anahtar kavramları gözden geçirin.|[Yazılım güncelleştirmelerine giriş](../understand/software-updates-introduction.md)|  
|Yazılım güncelleştirmelerini planlayın. Bu bilgiler, kapasiteyle alakalı durumlar için planlama yapmanıza; yazılım güncelleştirmeleri için yazılım güncelleştirme noktası altyapısını, yazılım güncelleştirme noktası yüklemesini ve eşitleme ayarlarını belirlemenize yardımcı olur.|[Yazılım güncelleştirmelerini planlama](../plan-design/plan-for-software-updates.md)|  
|Yazılım güncelleştirmelerini yapılandırın. Bu bilgi, hiyerarşinizdeki yazılım güncelleştirmelerini yüklemenize ve yapılandırmanıza yardımcı olur ve yazılım güncelleştirmelerinizi yapılandırmanızı ve eşitlemenizi sağlar.<br /><br /> Bu senaryoda ConfigMgr yöneticiniz, yazılım güncelleştirmeleri eşitleme zamanlamasını her ayın ikinci Çarşamba günü gerçekleşecek şekilde yapılandırır ve bu da Microsoft 'un en son güvenlik yazılım güncelleştirmelerini aldığından emin olabilir.|[Yazılım güncelleştirmelerini eşitleme](../get-started/synchronize-software-updates.md)|  

 Bu konudaki aşağıdaki bölümlerde, kuruluşunuzda Configuration Manager güvenlik yazılımı güncelleştirmelerini dağıtmanıza ve izlemenize yardımcı olacak örnek adımlar sağlanmaktadır.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a>1. Adım: yıllık uyumluluk için yazılım güncelleştirme grubu oluşturma  
 Configuration Manager yöneticisi, 2016 içinde yayıntıkları tüm güvenlik yazılımı güncelleştirmeleri için uyumluluğu izlemek üzere kullanılabilecek bir yazılım güncelleştirme grubu oluşturur. Yönetici aşağıdaki tablodaki adımları gerçekleştirir.  

|İşleme|Başvuru|  
|-------------|---------------|  
|Configuration Manager yöneticisi, Configuration Manager konsolundaki **tüm yazılım güncelleştirmeleri** düğümünden, aşağıdaki ölçütlere uyan 2015 yılında yayınlanan veya düzeltilen güvenlik yazılımı güncelleştirmelerini göstermek için ölçütler ekler:<br /><br /><ul><li>**Ölçüt**: Yayınlandığı veya Gözden Geçirildiği Tarih</li><li>**Koşul**: belirli tarihten büyük veya eşittir<br />**Değer**: 1/1/2015</li><li>**Ölçüt**: Güncelleştirme Sınıflandırması<br />**Değer**: Güvenlik Güncelleştirmeleri</li><li>**Ölçüt**: Süresi dolan <br />**Değer**: Hayır</li></ul>|Ek bilgi yok|
|ConfigMgr Yöneticisi, filtrelenmiş yazılım güncelleştirmelerinin tümünü yeni bir yazılım güncelleştirme grubuna aşağıdaki gereksinimlere ekler:<br /><br /><ul><li>**Ad**: Uyumluluk Grubu - Microsoft Güvenlik Güncelleştirmeleri 2015</li><li>**Açıklama**: Yazılım güncelleştirmeleri|[Yazılım güncelleştirmelerini güncelleştirme grubuna ekleme](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a>2. Adım: geçerli ay için bir otomatik dağıtım kuralı oluşturma  
 Configuration Manager yöneticisi, Microsoft tarafından geçerli ay için yayınlanan güvenlik yazılımı güncelleştirmeleri için bir otomatik dağıtım kuralı oluşturur. Yönetici aşağıdaki tablodaki adımları gerçekleştirir.  

|İşleme|Başvuru|  
|-------------|---------------|  
|ConfigMgr Yöneticisi, aşağıdaki gereksinimlere sahip bir otomatik dağıtım kuralı oluşturur:<br /><br /><ol><li>**Genel** sekmesinde ConfigMgr Yöneticisi aşağıdakileri yapılandırır:<br /> <ul><li>Ad için **aylık güvenlik güncelleştirmelerini** belirtir.</li><li>Sınırlı istemcilerle bir test koleksiyonu seçer.</li><li>**Yeni yazılım güncelleştirme grubu oluştur ' a**seçer.</li><li>**Bu kural çalıştırıldıktan sonra dağıtımı etkinleştir** ' in seçili olmadığını doğrular.</li></ul></li><li>**Dağıtım ayarları** sekmesinde ConfigMgr Yöneticisi varsayılan ayarları seçer.</li><li>ConfigMgr Yöneticisi, **yazılım güncelleştirmeleri** sayfasında aşağıdaki özellik filtrelerini ve arama ölçütlerini yapılandırır:<br /><ul><li>Yayınlandığı veya Gözden Geçirildiği Tarih **Son 1 ay**.</li><li>Güncelleştirme Sınıflandırması **Güvenlik Güncelleştirmeleri**.</li></ul></li><li>**Değerlendirme** sayfasında ConfigMgr Yöneticisi, kuralın her **ayın** **ikinci Perşembe günü** için bir zamanlamaya göre çalışmasını sağlar.  ConfigMgr Yöneticisi aynı zamanda eşitleme zamanlamasının her **ayın** **ikinci Çarşamba** günü çalışacak şekilde ayarlandığını doğrular.</li><li>ConfigMgr Yöneticisi dağıtım zamanlaması, Kullanıcı deneyimi, uyarılar ve yükleme ayarları sayfalarında varsayılan ayarları kullanır.</li><li>**Dağıtım paketi** sayfasında, ConfigMgr Yöneticisi yeni bir dağıtım paketi belirtir.</li><li>ConfigMgr Yöneticisi, Indirme konumu ve dil seçimi sayfalarında varsayılan ayarları kullanır.</li></ol>|[Yazılım güncelleştirmelerini otomatik dağıtma](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a>3. Adım: yazılım güncelleştirmelerinin dağıtıma hazırlık olduğunu doğrulama  
 ConfigMgr Yöneticisi, her ayın ikinci Perşembe günü yazılım güncelleştirmelerinin dağıtıma hazırlandığını doğrular. Yönetici aşağıdaki adımı gerçekleştirir.  

|İşleme|Başvuru|  
|-------------|---------------|  
|ConfigMgr Yöneticisi yazılım güncelleştirmeleri eşitlemesinin başarıyla tamamlandığını doğrular.|[Yazılım güncelleştirme eşitleme durumu](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a>4. Adım: yazılım güncelleştirme grubunu dağıtma  
 ConfigMgr Yöneticisi yazılım güncelleştirmelerinin dağıtmaya hazırlanma olduğunu doğruladıktan sonra, yazılım güncelleştirmelerini dağıtır. Yönetici aşağıdaki tablodaki adımları gerçekleştirir.  

|İşleme|Başvuru|  
|-------------|---------------|  
|ConfigMgr Yöneticisi, yeni yazılım güncelleştirme grubu için iki test dağıtımı oluşturur. Yönetici her dağıtım için aşağıdaki ortamları dikkate alır:<br /><br /> **Iş istasyonu test dağıtımı**: ConfigMgr Yöneticisi, iş istasyonu test dağıtımı için aşağıdakileri göz önünde bulundurur:<br /><br /><ul><li>Dağıtımı doğrulamak için iş istasyonu istemcilerinin bir alt kümesini içeren bir dağıtım koleksiyonu belirtir.</li><li>Ortamındaki iş istasyonu istemcilerine uygun olan dağıtım ayarlarını yapılandırır.</li></ul><br />**Sunucu sınama dağıtımı**: ConfigMgr Yöneticisi, sunucu sınama dağıtımı için aşağıdakileri göz önünde bulundurur:<br /><br /><ul><li>Dağıtımı doğrulamak için sunucu istemcilerinin bir alt kümesini içeren bir dağıtım koleksiyonu belirtir.</li><li>Ortamındaki sunucu istemcilerine uygun olan dağıtım ayarlarını yapılandırır.</li></ul>|[Yazılım güncelleştirmelerini dağıtma](deploy-software-updates.md)|  
|ConfigMgr Yöneticisi test dağıtımlarının başarıyla dağıtıldığını doğrular.|[Yazılım güncelleştirmeleri dağıtım durumu](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|ConfigMgr Yöneticisi iki dağıtımı, üretim iş istasyonlarını ve sunucularını içeren yeni koleksiyonlarla güncelleştirir.|Ek bilgi yok|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a>5. Adım: dağıtılan yazılım güncelleştirmeleri için uyumluluğu Izleme  
 ConfigMgr Yöneticisi, yazılım güncelleştirme dağıtımlarının uyumluluğunu izler. Yönetici aşağıdaki tabloda adımı gerçekleştirir.  

|İşleme|Başvuru|  
|-------------|---------------|  
|ConfigMgr Yöneticisi, Configuration Manager konsolundaki yazılım güncelleştirmeleri dağıtım durumunu izler ve konsolundan kullanılabilen yazılım güncelleştirme dağıtım raporlarını denetler.|[Yazılım güncelleştirmelerini izleme](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a>Adım 6: yıllık güncelleştirme grubuna aylık yazılım güncelleştirmeleri ekleme  
 ConfigMgr Yöneticisi, aylık yazılım güncelleştirme grubundaki yazılım güncelleştirmelerini yıllık yazılım güncelleştirme grubuna ekler. Yönetici aşağıdaki tabloda adımı gerçekleştirir.  

|İşleme|Başvuru|  
|-------------|---------------|  
|ConfigMgr Yöneticisi, aylık yazılım güncelleştirme grubundaki yazılım güncelleştirmelerini seçer ve yazılım güncelleştirmelerini yıllık uyumluluk için oluşturulan yazılım güncelleştirmeleri grubuna ekler. Yönetici, yazılım güncelleştirme uyumluluğunu izler ve yönetimi için çeşitli raporlar oluşturur.|[Yazılım güncelleştirmelerini dağıtılan bir güncelleştirme grubuna ekle](add-software-updates-to-an-update-group.md)|  

ConfigMgr Yöneticisi, güvenlik yazılımı güncelleştirmeleri için aylık dağıtımını başarıyla tamamladı. Yönetici, ortamındaki istemcilerin kabul edilebilir uyumluluk düzeylerinde yer aldığından emin olmak için yazılım güncelleştirme uyumluluğunu izlemeye ve raporlara devam eder.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a>Yazılım güncelleştirmelerini dağıtmak için yinelenen aylık işlem  
 ConfigMgr yöneticimizin yazılım güncelleştirmelerini dağıttığı ilk aydan sonra, yönetici, Microsoft tarafından yayınlanan aylık güvenlik yazılımı güncelleştirmelerini dağıtmak için üç ile 6 arasındaki adımları gerçekleştirir.  
