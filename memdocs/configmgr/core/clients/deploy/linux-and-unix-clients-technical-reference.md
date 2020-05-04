---
title: UNIX/Linux istemci Bileşen Hizmetleri ve komutları
titleSuffix: Configuration Manager
description: Configuration Manager ' de Linux ve UNIX istemcilerinde Bileşen Hizmetleri ve komutları hakkında bilgi edinin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713348"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Linux ve UNIX istemcileri Bileşen Hizmetleri ve Configuration Manager için komutlar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.


 Aşağıdaki tabloda, Linux ve UNIX için Configuration Manager istemcisinin istemci Bileşen Hizmetleri tanımlanmaktadır.  

|Dosya adı|Daha fazla bilgi|  
|---------------|----------------------|  
|ccmexec.bin|Bu hizmet, Windows tabanlı bir istemcide ccmexc hizmetine benzer. Configuration Manager site sistem rollerine sahip tüm iletişimlerden sorumludur ve ayrıca yerel bilgisayardan donanım envanteri toplamak için omiserver. bin hizmeti ile iletişim kurar.<br /><br /> Desteklenen komut satırı bağımsız değişkenlerinin listesi için şunu çalıştırın`ccmexec -h`|  
|omiserver.bin|Bu hizmet CIM sunucusudur. CIM sunucusu, sağlayıcı olarak adlandırılan eklenebilir yazılım modülleri için bir çerçeve sağlar. Sağlayıcılar Linux ve UNIX bilgisayar kaynakları ile etkileşim kurar ve donanım envanteri verilerini toplar. Örneğin, bir Linux bilgisayar için **işlem sağlayıcısı** , Linux işletim sistemi işlemleriyle ilişkili verileri toplar.|  

 Aşağıdaki tabloda her bir Linux ve UNIX sürümündeki istemci hizmetlerini (ccmexec.bin ve omiserver.bin) başlatmak, durdurmak veya yeniden başlatmak için kullanabileceğiniz komutlar listelenmektedir. Ccmexec hizmetini başlattığınızda veya durdurduğunuzda omiserver hizmeti de başlatılır veya durdurulur.  

|İşletim sistemi|Komutlar|  
|----------------------|--------------|  
|Evrensel Aracı<br /><br /> RHEL 4 ve SLES 9|Başından`/etc/init d/ccmexecd start`<br /><br /> Durdurulması`/etc/init d/ccmexecd stop`<br /><br /> Uygulamasını`/etc/init d/ccmexecd restart`|  
|Solaris 9|Başından`/etc/init d/ccmexecd start`<br /><br /> Durdurulması`/etc/init d/ccmexecd stop`<br /><br /> Uygulamasını`/etc/init d/ccmexecd restart`|  
|Solaris 10|Başlat:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Durdur:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Başlat:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Durdur:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Başlat:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Durdur:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Başından`/sbin/init.d/ccmexecd start`<br /><br /> Durdurulması`/sbin/init.d/ccmexecd stop`<br /><br /> Uygulamasını`/sbin/init.d/ccmexecd restart`|  
