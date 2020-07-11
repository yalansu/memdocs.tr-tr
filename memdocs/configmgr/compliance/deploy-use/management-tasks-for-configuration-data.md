---
title: Yapılandırma verilerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager ' de yapılandırma öğeleri ve temelleri oluşturduktan sonra, çeşitli eylemler gerçekleştirmek için diğer komutları kullanabilirsiniz.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: c375b5d773775e1be89f1e9dda38ee04e7f9f63f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240261"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Configuration Manager yapılandırma verilerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' de yapılandırma öğeleri ve yapılandırma temelleri oluşturduktan sonra, çeşitli eylemler gerçekleştirmenize yardımcı olmak için daha fazla komut kullanılabilir.  

## <a name="manage-configuration-items"></a>Yapılandırma öğelerini yönetme  

-   **Varlıklar ve uyum** çalışma alanında, **Uyumluluk ayarları**  >  **yapılandırma öğeleri**' ni genişletin, yönetilecek yapılandırma öğesini seçin ve ardından bir yönetim görevi seçin.  

|Yönetim görevi|Ayrıntılar|  
|---------------------|-------------|  
|**Alt Yapılandırma Öğesi Oluşturma**|Seçili yapılandırma öğesi için bir alt yapılandırma öğesi oluşturabileceğiniz **Alt Yapılandırma Öğesi Oluşturma Sihirbazı** ’nı açar.<br /><br /> Bir mobil cihaz yapılandırma öğesinden alt yapılandırma öğesi oluşturamazsınız.<br /><br /> Ayrıntılar için bkz. [alt yapılandırma öğeleri oluşturma](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Değişiklik Geçmişi**|Seçili yapılandırma öğesinin önceki düzeltmelerini görüntüleyip yönetebileceğiniz **Yapılandırma Öğesi Düzeltme Geçmişi** iletişim kutusunu açar.|  
|**XML Tanımını Görüntüle**|Seçili yapılandırma öğesinin XML tanım dosyasını yeni bir pencerede açar. Bu bilgiler yapılandırma verilerini el ile oluşturmak istediğinizde yararlı olabilir.|  
|**Dışarı Aktarma**|İlgili sitede oluşturulması koşuluyla dolap (.cab) dosya biçiminde bir yapılandırma öğesini dışarı aktarır. Daha sonra bunu aynı veya farklı bir Configuration Manager sitesine içeri aktarabilirsiniz. Yapılandırma verileri DCM Özetine dönüştürülür.|  
|**Kopyala**|Seçili yapılandırma öğesi için belirttiğiniz adla bir kopya oluşturur. Yeni yapılandırma öğesi özgün yapılandırma öğesi ile herhangi bir ilişki sürdürmez. Bu durum, yinelenen yapılandırma öğesinin özgün yapılandırma öğesinden yapılandırma bilgilerini devralmaya devam etmediği anlamına gelir.|  
|**Sil**|Bu yapılandırma öğesinin tüm başvurularını gözden geçirebileceğiniz **Yapılandırma Öğesini Sil** iletişim kutusunu açar.<br /><br /> Yapılandırma öğesini silmeden önce yapılandırma öğesinin tüm başvurularını kaldırmanız gerekir.|  

## <a name="manage-configuration-baselines"></a>Yapılandırma temellerini yönetme  

-   **Varlıklar ve uyum** çalışma alanında, **Uyumluluk ayarları**  >  **yapılandırma temelleri**' ni genişletin, yönetilecek Yapılandırma temelini seçin ve ardından bir yönetim görevi seçin.  


|Yönetim görevi|Ayrıntılar|  
|---------------------|-------------|  
|**Üyeleri Göster**|Yapılandırma temeli tarafından başvurulan tüm yapılandırma öğelerini görüntüler.|  
|**Özetlemeyi Zamanla**|Configuration Manager konsolundaki **yapılandırma temelleri** düğümünde gösterilen verilerin, site veritabanındaki en son bilgilerle güncelleştirildiği zamanlamayı yapılandırır.|  
|**Özetlemeyi Çalıştır**|Özetleme, **Yapılandırma Temelleri** düğümündeki verilerin site veritabanındaki en son verilerle yenilenmesine neden olur. Bu işlemin tamamlanması birkaç dakika sürebilir. Konsolda en son verileri görebilmek için **Yenile** ’ye tıklamanız gerekebilir.|  
|**XML Tanımını Görüntüle**|Seçili yapılandırma temelinin XML tanım dosyasını yeni bir pencerede açar. Bu bilgiler yapılandırma verilerini el ile oluşturmak istediğinizde yararlı olabilir.|  
|**Etkinleştir**|Uyumluluk izlemesi için bir yapılandırma temelini etkinleştirir.|  
|**Devre Dışı Bırak**|İstemci bilgisayarlarda uyumluluğunun bundan böyle değerlendirilmemesi için yapılandırma temelini devre dışı bırakır. Bu yapılandırma temeline başvuran yapılandırma temelleri de devre dışı bırakılır.|  
|**Dışarı Aktarma**|İlgili sitede oluşturulması koşuluyla dolap (.cab) dosya biçiminde bir yapılandırma temelini dışarı aktarır. Daha sonra bunu aynı veya farklı bir Configuration Manager sitesine içeri aktarabilirsiniz. Yapılandırma verileri DCM Özetine dönüştürülür.<br /><br /> Yapılandırma verilerini içeri aktarma hakkında daha fazla bilgi için bkz. [yapılandırma verilerini Içeri aktarma](../../compliance/deploy-use/import-configuration-data.md).|  
|**Kopyala**|Seçili yapılandırma temeli için belirttiğiniz adla bir kopya oluşturur. Yeni yapılandırma temeli özgün yapılandırma temeli ile herhangi bir ilişki sürdürmez.|  
|**Sil**|Bu yapılandırma Temelinin tüm başvurularını gözden geçirebileceğiniz **Yapılandırma Temelini Sil** iletişim kutusunu açar.<br /><br /> Yapılandırma temelini silmeden önce yapılandırma temelinin tüm başvurularını kaldırmanız gerekir.|  
|**Dağıtma**|Hiyerarşinizdeki cihazlara bir veya daha fazla yapılandırma temeli dağıtabileceğiniz **Yapılandırma Temeli Dağıt** iletişim kutusunu açar.<br /><br /> Ayrıntılar için bkz. [yapılandırma temellerini dağıtma](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
