---
title: Örnek doğrulama durumu geçişleri
titleSuffix: Configuration Manager
description: Configuration Manager Varlık Yönetim Bilgileri için doğrulama durumu geçişleri örneklerine bakın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2af9243d6720d5821c641e5c80589457a33b638e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714181"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>Varlık Yönetim Bilgileri için örnek doğrulama durumu geçişleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Varlık Yönetim Bilgileri doğrulama durumları statik değildir ve Varlık Yönetim Bilgileri kataloğunda depolanan verileri etkilemek için sizin yaptığınız yönetim eylemleriyle değiştirilebilir. Bu konu, olası doğrulama durumu geçişleri için örnekler sağlar.

##  <a name="uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a>Kategorilere ayrılmamış Katalog öğesi, yönetici kullanıcı tarafından kategorilere ayrılmıştır  

|**Durum geçişi**|**Durum geçişi açıklaması**|  
|--------------------------|--------------------------------------|  
|**Kategorilere ayrılmamış**|System Center Online tarafından önceden kategorilere ayrılmış veya yönetici kullanıcının Varlık Yönetim Bilgileri kataloğuna girdiği, envantere alınmamış bir yazılım|  
|**Kullanıcı tanımlı** olarak **kategorilere ayrılmamış**|Kategorilere ayrılmamış öğe, yönetici kullanıcı tarafından kategorilere ayrılır.|  

##  <a name="categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> Kategorilere ayrılmış katalog öğesi, yönetici kullanıcı tarafından yeniden kategorilere ayrılmıştır.  

|**Durum geçişi**|**Durum geçişi açıklaması**|  
|--------------------------|--------------------------------------|  
|**Doğrulanmış**|Katalog Öğesi System Center Online araştırmacıları tarafından tanımlanır ve Varlık Yönetim Bilgisi kataloğunda bulunur.|  
|**Doğrulanmış** ’tan **Kullanıcı Tanımlı**|Doğrulanmış kategori öğesi, yönetici kullanıcı tarafından yeniden kategorilere ayrılmıştır.|  

> [!NOTE]  
>  System Center Online’dan alınan kategorilere ayırma bilgileri veritabanında depolandığından ve silinemediğinden, yönetici kullanıcı daha sonra System Center Online kategorilerine geri dönebilir.  

##  <a name="user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a>Kullanıcı tanımlı Katalog öğesi System Center Online tarafından yeniden kategorilere ayrılmıştır  

|**Durum geçişi**|**Durum geçişi açıklaması**|  
|--------------------------|--------------------------------------|  
|**Kategorilere ayrılmamış**|Varlık Yönetim Bilgileri kataloğuna, daha önce System Center Online veya yönetici kullanıcı tarafından kategorilere ayrılmamış olan, envantere alınmış bir yazılım girilmiştir.|  
|**Kullanıcı Tanımlı**|Kategorilere ayrılmamış öğe, yönetici kullanıcı tarafından kategorilere ayrılır.|  
|**Kullanıcı Tanımlı** ’tan **Kullanıcı Tanımlı**|Varlık Yönetim Bilgileri kataloğunun el ile sıralı toplu güncelleştirmesi sırasında System Center Online tarafından farklı şekilde kategorilere ayrılmış olan, kullanıcı tanımlı bir katalog öğesi.<br /><br /> Yönetici kullanıcı, yeni kategori bilgilerinin veya önceki kullanıcı tanımlı değerlerin kullanılmasını belirlemek üzere **Yazılım Ayrıntıları Çakışması Çözümü** iletişim kutusunu kullanabilir.|  
|**Kullanıcı Tanımlı** ’tan **Doğrulanmış**|Yönetici kullanıcı, önceki katalog güncelleştirmesi sırasında System Center Online’dan alınan yeni kategori bilgilerini kullanmak için **Yazılım Ayrıntıları Çakışma Çözümü** iletişim kutusunu kullanabilir.|  
|or||  
|**Kullanıcı Tanımlı** ’tan **Kullanıcı Tanımlı**|Yönetici kullanıcı, önceki kullanıcı tanımlı değeri kullanmak için **Yazılım Ayrıntıları Çakışma Çözümü** iletişim kutusunu kullanabilir.|  

> [!NOTE]  
>  System Center Online’dan alınan kategorilere ayırma bilgileri veritabanında depolandığından ve silinemediğinden, yönetici kullanıcı daha sonra System Center Online kategorilerine geri dönebilir.  

##  <a name="uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a>Kategorilere ayrılmamış Katalog öğesi, kategorilere ayrılması için System Center Online 'a gönderilir  

|**Durum geçişi**|**Durum geçişi açıklaması**|  
|--------------------------|--------------------------------------|  
|**Kategorilere ayrılmamış**|Varlık Yönetim Bilgileri veritabanına daha önce System Center Online veya yönetici kullanıcı tarafından kategorilere ayrılmamış envantere alınmış bir yazılım girilmiştir.|  
|**Kategorilere ayrılmamış** ’tan **Bekleniyor**|Kategorilere ayrılmamış öğe, yönetici kullanıcı tarafından kategorilere ayrılması için System Center Online’a gönderilmiştir.|  
|**Bekleniyor** ’tan **Doğrulanmış**|Öğe, System Center Online tarafından kategorilere ayrılmıştır. Yönetici kullanıcı, toplu katalog güncelleştirmesi veya Varlık Yönetim Bilgileri kataloğu eşitleme kullanarak öğeyi Varlık Yönetim Bilgileri kataloğuna aktarır. İki seçenek de Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolüyle kullanılabilir.|  

##  <a name="user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a>Kullanıcı tanımlı Katalog öğesi, kategorilere ayrılması için System Center Online 'a gönderilir  

|**Durum geçişi**|**Durum geçişi açıklaması**|  
|--------------------------|--------------------------------------|  
|**Kategorilere ayrılmamış**|Varlık Yönetim Bilgileri veritabanına daha önce yönetici kullanıcı veya System Center Online tarafından kategorilere ayrılmamış olan, envantere alınmış bir yazılım girilmiştir.|  
|**Kullanıcı Tanımlı**|Kategorilere ayrılmamış öğeyi kategorilere ayırdınız.|  
|**Kullanıcı Tanımlı** ’tan **Bekleniyor**|Kullanıcı tanımlı öğeyi kategorilere ayrılması için System Center Online’a gönderdiniz.|  
|**Bekleniyor** ’tan **Kullanıcı Tanımlı**|Sıralı katalog eşitlemesi sırasında System Center Online tarafından farklı şekilde kategorilere ayrılmış olan, kullanıcı tanımlı bir katalog öğesi. Yeni kategori bilgilerinin veya önceki Kullanıcı tanımlı değerin kullanılıp kullanılmayacağını belirlemek için **çakışmayı çözümle** eylemini kullanabilirsiniz. Çakışmaları giderme hakkında daha fazla bilgi için [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)konusuna bakın.|  
|**Kullanıcı Tanımlı** ’tan **Doğrulanmış**|**Çakışmayı Gider** eylemini kullanarak önceki katalog güncelleştirmesi sırasında System Center Online’dan alınan yeni kategorilere ayırma bilgilerini seçebilirsiniz. Çakışmaları giderme hakkında daha fazla bilgi için [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)konusuna bakın.|  
|or||  
|**Kullanıcı Tanımlı** ’tan **Kullanıcı Tanımlı**|**Çakışmayı Gider** eylemini kullanarak önceki kullanıcı tanımlı değeri kullanmayı seçersiniz. Çakışmaları giderme hakkında daha fazla bilgi için [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)konusuna bakın.|  

> [!NOTE]  
>  System Center Online’dan alınan kategorilere ayırma bilgileri veritabanında depolandığından ve silinemediğinden, daha sonra System Center Online kategorilerine geri dönebilirsiniz.  
