---
title: Site hatası etkileri
titleSuffix: Configuration Manager
description: Configuration Manager sitesindeki çeşitli hataların etkilerini anlayın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723897"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Configuration Manager 'de site hatası etkileri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Site sunucusu ve diğer site sistemleri başarısız olabilir ve düzenli olarak sağladığı hizmetlerin kaybına neden olabilir. Aynı bilgisayara birden fazla site sistemi yüklerseniz ve bu bilgisayar başarısız olursa, bu site sistemleri tarafından düzenli olarak sağlanan tüm hizmetler artık kullanılamaz.

Planlama işleminizin bir parçası, kuruluşunuzu sağladığınız hizmette etkileri anlamak içermelidir. Sitedeki her bir site sistemi farklı işlevsellik sağladığından, başarısız olan site sisteminin rolüne bağlı olarak sitedeki bir hatanın etkisi farklılık gösterir. 

Tek bir sistemin başarısızlığını azaltmaya yardımcı olmak için [yüksek kullanılabilirlik seçenekleri](../deploy/configure/high-availability-options.md) kullanın. Ayrıca, hizmetin kullanılamayan süreyi azaltmak için bir [yedekleme ve kurtarma](backup-and-recovery.md) stratejisi planlayın ve yapın.

Aşağıdaki bölümler, belirtilen site sistemi işlemsel olmadığında etkisini anlatmaktadır:


### <a name="site-server"></a>Site sunucusu

- Site yönetimi mümkün değildir. Konsolu siteye bağlanamazsınız.  

- Yönetim noktası istemci bilgilerini toplar ve site sunucusu yeniden çevrimiçi olana kadar önbelleğe alır.  

- Kullanıcılar mevcut dağıtımları çalıştırabilir ve istemciler dağıtım noktalarından içerik indirebilir.  


### <a name="site-database"></a>Site veritabanı

- Site yönetimi mümkün değildir.  

- Configuration Manager istemcisinde zaten yeni ilkeler içeren bir ilke ataması varsa ve yönetim noktası ilke gövdesini önbelleğe alıyorsa, istemci ilke gövdesi isteği yapabilir ve ilke gövdesi yanıtı alabilir. Ancak, site yeni ilke atama isteklerine hizmet vermez.  

- İstemciler yalnızca ilkeyi zaten almış olmaları durumunda dağıtımları çalıştırabilir ve ilişkili kaynak dosyaları zaten istemcide yerel olarak önbelleğe alınır.  


### <a name="management-point"></a>Yönetim noktası

- Yeni dağıtımlar oluşturabilseniz de, istemciler bir yönetim noktası çevrimiçi olana kadar bunları almaz.  

- İstemciler envanter, yazılım kullanım ölçümü ve durum bilgilerini yine de toplar. Bu veriler, yönetim noktası kullanılabilir olana kadar yerel olarak depolanır.  

- İstemciler yalnızca ilkeyi zaten almış olmaları durumunda dağıtımları çalıştırabilir ve ilişkili kaynak dosyaları zaten istemcide yerel olarak önbelleğe alınır.  


### <a name="distribution-point"></a>Dağıtım noktası

- Configuration Manager istemcileri, yalnızca ilişkili kaynak dosyaları zaten yerel olarak indirildiyse veya bir eş kaynakta varsa dağıtımları çalıştırabilir.

