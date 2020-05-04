---
title: Linux/UNIX istemcilerini izleme
titleSuffix: Configuration Manager
description: Linux ve UNIX sunucularındaki istemcileri Configuration Manager izleyin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715364"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Configuration Manager 'da Linux ve UNIX sunucuları için istemcileri izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Configuration Manager konsolundaki Linux ve UNIX sunucularından gelen bilgileri, Windows tabanlı istemcilerden bilgileri görüntülemek için kullandığınız yöntemlerin aynısını kullanarak görüntüleyebilirsiniz.  

 Görüntüleyebileceğiniz bilgiler şunları içerir:  

- Configuration Manager konsolu panolarında, istemcilerden gelen durum ayrıntıları  

- Varsayılan Configuration Manager raporlardaki istemcilerle ilgili ayrıntılar  

- Kaynak Gezgini’ndeki stok ayrıntıları  

  Aşağıdaki bölümlerde, bu ayrıntıların kaynak Gezgini ve raporlardan nasıl alınacağı açıklanır.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a>Linux ve UNIX sunucularının envanterini görüntülemek için kaynak Gezgini 'ni kullanma  

 Bir Configuration Manager istemcisi Configuration Manager sitesine donanım envanterini gönderdikten sonra, bu bilgileri görüntülemek için Kaynak Gezgini kullanabilirsiniz. Linux ve UNIX için Configuration Manager istemcisi, Kaynak Gezgini envanter için yeni sınıflar veya görünümler eklemez. Linux ve UNIX envanter verileri var olan WMI sınıflarıyla eşleşir. Kaynak Gezgini'ni kullanarak Windows tabanlı sınıflandırmalardaki Linux ve UNIX sunucularının envanter ayrıntılarını görüntüleyebilirsiniz.  

 Örneğin, Linux ve UNIX sunucularınızda bulunan yerel olarak yüklenmiş tüm programların listesini toplayabilirsiniz. Linux içindeki **.rpms** veya Solaris içindeki **.pkgs** , yerel olarak yüklenmiş program örnekleri arasında bulunur. Envanter bir Linux veya UNIX istemcisi tarafından gönderildikten sonra, Configuration Manager konsolundaki Kaynak Gezgini yerel olarak yüklenmiş tüm Linux veya UNIX programlarının listesini görüntüleyebilirsiniz.  

 Kaynak Gezgini kullanma hakkında daha fazla bilgi için bkz. [Kaynak Gezgini kullanarak donanım envanterini görüntüleme](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Linux ve UNIX Sunucuların Bilgilerini Görüntülemek İçin Raporları Kullanma  
 Configuration Manager raporları, Linux ve UNIX sunucularından gelen bilgileri ve Windows tabanlı bilgisayarlardan gelen bilgileri içerir. Linux ve UNIX verilerini raporlarda tümleştirmek için hiçbir ek yapılandırmaya gerek yoktur.  

 Örneğin, İşletim Sistemi Sürümleri Sayısı adlı raporu çalıştırırsanız rapor, farklı işletim sistemlerinin listesini ve her bir işletim sistemini çalıştıran istemcilerin sayısını görüntüler. Rapor, farklı işletim sistemleri üzerinde çalışan farklı Configuration Manager istemcileri tarafından gönderilen donanım envanteri bilgilerine dayanır.  

 Ayrıca, Linux ve UNIX sunucu verilerine özgü özel raporlar oluşturmak da mümkündür. Donanım envanteri sınıfı **İşletim Sistemi** ’nin **Resim Yazısı** özelliği, rapor sorgusundaki belirli İşletim Sistemleri’ni tanımlamak için kullanabileceğiniz yararlı bir özniteliktir.  

 Configuration Manager raporları hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../servers/manage/introduction-to-reporting.md).  
