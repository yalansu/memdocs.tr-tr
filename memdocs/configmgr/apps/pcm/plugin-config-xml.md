---
title: Eklenti yapılandırması XML
titleSuffix: Configuration Manager
description: Paket Dönüştürme Yöneticisi eklentisinin XML öğeleri için teknik başvuru.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9178b595ba67723c623979b4c29290e42fe5f6ac
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877745"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Paket Dönüştürme Yöneticisi eklenti yapılandırması XML 'SI için teknik başvuru

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357861-->

Bu makalede, Paket Dönüştürme Yöneticisi eklentisinin çalışmasını denetleyen Configuration Manager yapılandırma dosyasında (Microsoft. ConfigurationManagement. exe. config) XML öğeleri açıklanmaktadır. Bu eklentinin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [Package Conversion Manager eklentisini kullanma](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>XML yapılandırma öğeleri

Aşağıdaki tabloda, Paket Dönüştürme Yöneticisi eklentisiyle ilgili Configuration Manager yapılandırma dosyasındaki XML öğeleri açıklanmaktadır.

|Öğe  |Tür  |Açıklama  |
|---------|---------|---------|
|**PcmPlugIn**|Dize|Paket Dönüştürme Yöneticisi eklentisi olarak kullanılacak betiğin veya yürütülebilir dosyanın adı.|
|**PcmPlugInTimeoutMilliseconds**|Tamsayı|Paket Dönüştürme Yöneticisi eklenti betiği veya yürütülebilir bir paketin işlenmesini tamamlaması için beklenecek en uzun süre (milisaniye cinsinden).|
|**PcmPluginExitCode**|Tamsayı|Eklenti işleminden beklenen çıkış kodu. Bu değer başarıyı gösterir. Diğer tüm kodlar hata olarak kabul edilir.|
|**ForceRequirementsExtraction**|Boole|Otomatik dönüştürmenin bir paket ile ilişkili koleksiyon gereksinimlerini kullanmasına izin verin. Bu, hangi gereksinimlerin kullanılacağı hakkında kararlar vermek için tasarlanan bir paket dönüştürme Yöneticisi eklentisiyle çalışırken yalnızca true olarak ayarlanmalıdır.|



## <a name="sample-configuration-xml"></a>Örnek yapılandırma XML 'i

Bu bölüm, **Microsoft. ConfigurationManagement. exe. config**Configuration Manager yapılandırma dosyasında paket dönüştürme YÖNETICISI yapılandırma XML öğelerine bir örnek sağlar. Varsayılan olarak, bu dosya şu yolda bulunur:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

> [!IMPORTANT]
> Sürüm 1910 ' den başlayarak, bu yol klasörü kullanacak şekilde değiştirilmiştir `Microsoft Endpoint Manager` . Dosyanın başka bir klasörde mevcut olabilecek eski bir sürümünü kullandığınızdan emin olun. 

Örnekte, Paket Dönüştürme Yöneticisi ile ilgili öğeler aşağıdaki öğenin içindedir:`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

