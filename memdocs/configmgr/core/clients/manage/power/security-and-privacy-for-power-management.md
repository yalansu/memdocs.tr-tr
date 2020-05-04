---
title: Güç yönetimi için güvenlik ve gizlilik
titleSuffix: Configuration Manager
description: Configuration Manager 'de güç yönetimi için güvenlik ve gizlilik bilgilerini alın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715182"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimi için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu bölüm Configuration Manager ' de güç yönetimi için güvenlik ve gizlilik bilgilerini içerir.  

## <a name="security-best-practices-for-power-management"></a>Güç yönetimi için önerilen güvenlik uygulamaları  
 Güç yönetimi için, güvenlikle ilgili önerilen uygulama bulunmamaktadır.  

## <a name="privacy-information-for-power-management"></a>Güç Yönetimi için Gizlilik Bilgileri  
 Güç yönetimi, güç kullanımını izlemek ve iş saatleri ile iş saatleri dışındaki saatler için güç ayarlarını bilgisayarlara uygulamak üzere yerleşik Windows özelliklerini kullanır. Configuration Manager, bir kullanıcının bilgisayar kullandığı zaman hakkında veri içeren bilgisayarlardan güç kullanım bilgilerini toplar. Configuration Manager her bir bilgisayar için değil, bir koleksiyon için güç kullanımını izlemeseler de, bir koleksiyon yalnızca bir bilgisayar içerebilir. Güç yönetimi varsayılan olarak etkinleştirilmez; bir yönetici tarafından yapılandırılması gerekir.  

 Güç kullanım bilgileri Configuration Manager veritabanında depolanır ve Microsoft 'a gönderilmez. Ayrıntılı bilgiler 31 gün boyunca veritabanında tutulur ve özet bilgiler 13 ay boyunca saklanır. Silme aralığını yapılandıramazsınız.  

 Güç yönetimini yapılandırmadan önce gizlilik gereksinimlerinizi gözden geçirin.  
