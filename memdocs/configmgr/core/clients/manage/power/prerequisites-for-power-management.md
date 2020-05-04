---
title: Güç yönetimi için önkoşullar
titleSuffix: Configuration Manager
description: Configuration Manager ' de güç yönetimi önkoşullarını alın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715189"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimi önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager güç yönetimi, ürün içinde dış bağımlılıklara ve bağımlılıklara sahiptir.  

## <a name="dependencies-external-to-configuration-manager"></a>Bağımlılıklar dış Configuration Manager  
 Aşağıdaki tabloda, güç yönetiminin kullanımı için Configuration Manager dış bağımlılıkları listelenmektedir.  

|Bağımlılık|Daha fazla bilgi|  
|----------------|----------------------|  
|İstemci bilgisayarlar gerekli güç durumlarını destekleyebilmelidir|Güç yönetiminin tüm özelliklerini kullanmak için istemci bilgisayarların uyku, hazırda bekleme, uyku modundan uyandırma ve bekleme modundan uyandırma eylemlerini destekleyebilmesi gerekir. Bilgisayarların bu eylemleri destekleyip desteklemediğini belirlemek için **Güç Özellikleri** raporunu kullanabilirsiniz. Daha fazla bilgi için bkz. güç [Özellikleri raporu](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) , [güç yönetimini Izleme ve plan yapma](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları  
 Aşağıdaki tabloda güç yönetimi kullanımı için Configuration Manager içindeki bağımlılıklar listelenmektedir.  

|Bağımlılık|Daha Fazla Bilgi|  
|----------------|----------------------|  
|Güç planları oluşturup izleyebilmeniz için güç yönetiminin etkinleştirilmesi gerekir.|Güç yönetimini etkinleştirme ve yapılandırma hakkında daha fazla bilgi için bkz. [güç yönetimini yapılandırma](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Raporlama hizmetleri noktası|Güç yönetimi raporlarını görüntüleyebilmek için bir raporlama hizmetleri noktasını yapılandırmanız gerekir. Daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).|  
