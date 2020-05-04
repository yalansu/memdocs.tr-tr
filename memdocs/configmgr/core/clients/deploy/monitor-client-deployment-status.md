---
title: İstemci dağıtım durumunu izleme
titleSuffix: Configuration Manager
description: Configuration Manager istemci dağıtım durumunu izleme.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713320"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Configuration Manager istemci dağıtım durumunu izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Siteniz genelinde istemciler dağıtmak zaman alıcıdır ve bazı yüklemeler ilk seferde başarılı olmaz. Configuration Manager konsolu, istemci dağıtım durumunu gerçek zamanlı olarak bildirerek bir koleksiyondaki istemci dağıtımlarını göz önünde tutmanız için bir yol sağlar.  

> [!NOTE]  
>  İstemci dağıtımını izlemenin en iyi ve en güvenilir yolu Configuration Manager konsoludur (Bu makalede açıklandığı gibi). Konsoldaki **İzleme** çalışma alanının **İstemci Durumu** bölümü, istemci dağıtım durumunu gerçek zamanda doğru olarak sunar. İstemci dağıtımlarını Windows Server veya System Center Operations Manager’daki Server Manager gibi başka araçlarla da izleyebilirsiniz, ancak normal yükleme etkinliğinden uyarılar alabilirsiniz. İstemci yükleme programının (CCMSetup.exe) değişik ortamlardaki çalışma şekli nedeniyle bu diğer araçlar, istemci dağıtımlarının durumunu doğru yansıtmayan yanlış uyarılar oluşturabilir.  

 Konsolun **İzleme** çalışma alanında, belirttiğiniz bir koleksiyon içinde gerçekleşen istemci dağıtımlarının aşağıdaki durumlarını izleyebilirsiniz:  

- Uyumlu  

- Devam ediyor  

- Uyumlu değil  

- Başarısız  

- Bilinmiyor  

  Configuration Manager, üretim istemcilerinin veya üretim öncesi istemcilerinin dağıtımlarını raporlar. Configuration Manager konsolu, ayrıca, dağıtımlardaki sorunları çözmek için yaptığınız işlemlerin zaman içinde istemci dağıtım başarısını artırıp artırmadığını belirlemenize yardımcı olmak için belirli bir süre içinde başarısız olan istemci dağıtımlarının da bir grafiğini sunar.  

## <a name="to-monitor-client-deployments"></a>İstemci dağıtımlarını izlemek için  

- Configuration Manager konsolunda, **izleme** > **istemci durumu**' nu tıklatın.  

- İzlemek istediğiniz istemci sürümüne bağlı olarak **Üretim İstemci Dağıtımı**’na veya **Üretim Öncesi İstemci Dağıtımı**’na tıklayın.  

- İstemci dağıtım durumu ve istemci dağıtım başarısızlığı grafiklerini inceleyin.  

- Raporun kapsamını değiştirmek istiyorsanız, **araştır...** ' a tıklayın ve farklı bir koleksiyon seçin.  

  Ön üretim istemci dağıtımları hakkında daha fazla bilgi edinmek için bkz. [bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../../core/clients/manage/upgrade/test-client-upgrades.md).

  > [!NOTE]
  > Bir ön üretim koleksiyonundaki site sistem rollerini barındıran bilgisayarlardaki dağıtım durumu, istemci başarıyla dağıtıldığında bile **uyumlu değil** olarak bildirilebilir. İstemciyi üretime yükselttiğinizde dağıtım durumu doğru şekilde bildirilir.   

  Dağıtılan istemcilerin durumunu izlemek için bkz. [istemcileri izleme](../../../core/clients/manage/monitor-clients.md)  

  Sitenizdeki istemcilerin durumu hakkında daha fazla bilgi edinmek için Configuration Manager raporları kullanabilirsiniz. Raporların nasıl çalıştırılacağı hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../servers/manage/introduction-to-reporting.md).  
