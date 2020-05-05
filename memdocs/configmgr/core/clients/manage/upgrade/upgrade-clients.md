---
title: İstemcileri yükseltin
titleSuffix: Configuration Manager
description: Configuration Manager ' de istemcilerin nasıl yükseltileceğiyle ilgili bilgiler alın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076688"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Configuration Manager istemcileri yükselt

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows bilgisayarlarda, UNIX ve Linux sunucularda ve Mac bilgisayarlarda Configuration Manager istemci yazılımını yükseltmek için farklı yöntemler kullanabilirsiniz. Her yöntemin avantajları ve dezavantajları aşağıda verilmiştir.  

> [!TIP]  
>  Sunucu altyapınızı Configuration Manager’ın önceki bir sürümünden yükseltiyorsanız \(Configuration Manager 2007 veya System Center 2012 Configuration Manager gibi\), Configuration Manager istemcilerini yükseltmeden önce tüm geçerli dal güncelleştirmeleri de içinde olmak üzere sunucu yükseltmelerini tamamlamanızı öneririz. Bu şekilde, istemci yazılımının en son sürümüne de sahip olacaksınız.  

## <a name="group-policy-installation"></a>Grup İlkesi yüklemesi  
 **Desteklenen istemci platformu:** Windows  

#### <a name="advantages"></a>Yararları  

- İstemcinin yükseltilebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

- Yeni istemci yüklemelerinde veya yükseltmelerde kullanılabilir.  

- Bilgisayarlar Active Directory Etki Alanı Hizmetlerine yayımlanmış istemci yükleme özelliklerini okuyabilirler.  

- Amaçlanan istemci bilgisayar için bir yükleme hesabı yapılandırıp bulundurmanızı gerektirmez.  

#### <a name="disadvantages"></a>Dezavantajlar  

- Çok sayıda istemciyi yükseltiyorsanız yüksek ağ trafiğine neden olabilir.  

- Active Directory şeması Configuration Manager uzatılmazsa, sitenizdeki bilgisayarlara istemci yükleme özellikleri eklemek için [Grup İlkesi ayarlarını](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) kullanmanız gerekir.  


## <a name="logon-script-installation"></a>Oturum açma betiği yüklemesi  
 **Desteklenen istemci platformu:** Windows  

#### <a name="advantages"></a>Yararları  

- İstemcinin yüklenebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

- Yeni istemci yüklemelerinde veya yükseltmelerde kullanılabilir.  

- CCMSetup için komut satırı özelliklerini kullanmayı destekler.  

#### <a name="disadvantages"></a>Dezavantajlar  

- Kısa bir süre içinde çok sayıda istemciyi yükseltiyorsanız yüksek ağ trafiğine neden olabilir.  

- Kullanıcılar ağda sık oturum açıp tüm istemci bilgisayarlarını yükseltmek uzun zaman alabilir.  

  Daha fazla bilgi için bkz. [Configuration Manager İstemcilerini Grup İlkesi Kullanarak Yükleme](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>El ile yükleme  
 **Desteklenen istemci platformu:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Yararları  

- İstemcinin yükseltilebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

- Sınama amacıyla yararlı olabilir.  

- CCMSetup için komut satırı özelliklerini kullanmayı destekler.  

#### <a name="disadvantages"></a>Dezavantajlar  

- Otomasyon olmadığından zaman alıcıdır.  

  Daha fazla bilgi edinmek için aşağıdaki kaynaklara bakın:  

- [Configuration Manager İstemcilerini El İle Yükleme](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Linux ve UNIX sunucuları için istemcileri yükseltme](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Mac bilgisayarlarda istemcileri yükseltme](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Yüklemeyi yükseltme (uygulama yönetimi)  
 **Desteklenen istemci platformu:** Windows  

> [!NOTE]  
>  Bu yöntemle Configuration Manager 2007 istemcilerini yükseltemezsiniz. Bu senaryoda, Configuration Manager istemcisini Configuration Manager 2007 sitesinden bir paket olarak dağıtabilir veya istemcinin en son sürümünü içeren bir paketi otomatik olarak oluşturup dağıtan otomatik istemci yükseltmesini kullanabilirsiniz.  

#### <a name="advantages"></a>Yararları  

- CCMSetup için komut satırı özelliklerini kullanmayı destekler.  

#### <a name="disadvantages"></a>Dezavantajlar  

- İstemcisini büyük koleksiyonlara dağıtırsanız yüksek ağ trafiğine neden olabilir.  

- Yalnızca bulunarak siteye atanmış bilgisayarlardaki istemci yazılımları yükseltmek için kullanılabilir.  

  Daha fazla bilgi için bkz. [Configuration Manager İstemcilerini Paket ve Program Kullanarak Yükleme](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Otomatik istemci yükseltmesi  

> [!NOTE]  
> , Geçerli şube istemcilerine Configuration Manager Configuration Manager 2007 istemcilerini yükseltmek için kullanılabilir. Configuration Manager 2007 istemcisi bir Configuration Manager sitesine atayabilir, ancak otomatik istemci yükseltmesinin yanında herhangi bir işlem gerçekleştiremez.  

 **Desteklenen istemci platformu:** Windows  

#### <a name="advantages"></a>Yararları  

- Belirtilen süre boyunca rastgele seçim nedeniyle, yalnızca otomatik yükseltme, büyük ölçekli istemci yükseltmeleri için uygundur. Diğer yöntemler büyük ölçekte çok yavaş ya da rastgele seçim içermez. 

    > [!Note]
    > İstemci pilot çalışması, hiç rastgele olmadığı için büyük ölçekte iyi değildir.  
- Sitenizdeki istemcileri otomatik olarak en son sürümde tutmak için kullanılabilir.  

- En az yönetim gerektirir.  

#### <a name="disadvantages"></a>Dezavantajlar  

- Yalnızca istemci yazılımı yükseltmek için kullanılabilir, yeni istemci yüklemek için kullanılamaz.  

- Hiyerarşideki siteye atanmış tüm istemciler için geçerlidir. Topluluğa göre kapsamı daraltılamaz.  

- Sınırlı zamanlama seçenekleri.  

  Daha fazla bilgi için bkz. [Windows bilgisayarları için istemcileri yükseltme](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>İstemci testi  
 **Desteklenen istemci platformu:** Windows  

#### <a name="advantages"></a>Yararları  

- Daha küçük bir üretim öncesi koleksiyonunda yeni istemci sürümlerini test etmek için kullanılabilir.  

- Test tamamlandığında, ön üretim içindeki istemciler üretime yükseltilir ve Configuration Manager sitesinde otomatik olarak yükseltilir.  

#### <a name="disadvantages"></a>Dezavantajlar  

- Yalnızca istemci yazılımı yükseltmek için kullanılabilir, yeni istemci yüklemek için kullanılamaz.  

  [Bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
