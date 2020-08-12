---
title: Sağlama modu
titleSuffix: Configuration Manager
description: Configuration Manager görev sırası sırasında istemci sağlama modu hakkında bilgi edinin.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0039648c6f444efdbbaeb16f55d29b630ee7f16
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124279"
---
# <a name="provisioning-mode"></a>Sağlama modu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir işletim sistemi dağıtımı görev sırası sırasında, Configuration Manager istemciyi sağlama moduna koyar. (Bir işletim sistemi dağıtımı görev dizisi, Windows 10 ' a yerinde yükseltme içerir.) Bu durumda, istemci ilkeyi siteden işlemez. Bu davranış, istemci üzerinde çalışan ek dağıtımlar risk olmadan görev dizisinin çalışmasına izin verir. Görev dizisi tamamlandığında, başarılı veya işlenmiş hata oluştuğunda, istemci sağlama modundan çıkar.

Görev sırası beklenmedik bir şekilde başarısız olursa, istemci sağlama modunda kalabilir. Örneğin, cihaz görev dizisi işlemenin ortasında yeniden başlarsa ve kurtarılamazsa. Bir yöneticinin bu durumdaki istemcileri el ile tanımlaması ve çözmesi gerekir.


## <a name="manually-remove-provisioning-mode"></a>Sağlama modunu el ile kaldır

İstemci sağlama modunda bırakılırsa, istemciyi normal işleme döndürmek için bu el ile işlemi kullanın.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Bu WMI yöntemi tarafından yapılan değişikliklerden biri bir kayıt defteri değeri ayarlıyor, ancak başka değişiklikler de yapar. Kayıt defteri değerinin değiştirilmesi, istemciyi sağlama modundan tamamen almaz. Kayıt defterini el ile düzenlerseniz, istemci beklenmeyen davranışlar gösterebilir.  


## <a name="client-provisioning-mode-timeout"></a>İstemci sağlama modu zaman aşımı

Sürüm 1902 ' den başlayarak, görev dizisi istemciyi sağlama moduna koyarken bir zaman damgası ayarlar. Sağlama modundaki bir istemci her 60 dakikada bir zaman damgasından bu yana süreyi denetler. 48 saatten uzun bir süredir sağlama modundayken istemci, sağlama modundan otomatik olarak çıkar ve işlemini yeniden başlatır.

48 saat, varsayılan sağlama modu zaman aşımı değeridir. Aşağıdaki kayıt defteri anahtarında **Provisioningmaxminutes** değerini ayarlayarak bir cihazda bu zamanlayıcıyı ayarlayabilirsiniz: `HKLM\Software\Microsoft\CCM\CcmExec` . Bu değer yoksa veya ise `0` , istemci varsayılan 48 saati kullanır.

Zaman damgası **Provisioningenabledtime** şu kayıt defteri anahtarında bulunuyor: `HKLM\Software\Microsoft\CCM\CcmExec` . Zaman damgası, makinenin en son sağlama moduna girdiği bir değere sahiptir. Biçim, dönem (Unix zaman damgası) ve UTC biçimindedir.

Bu zaman damgası Ayrıca, aşağıdaki komutu kullanarak makineyi sağlama moduna el ile yerleştirdiğinizde geçerli saate sıfırlanır:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>İşlem akış diyagramları

Bu diyagramlar görev dizisi ve istemcisi için işlem akışını gösterir.

### <a name="task-sequence"></a>Görev dizisi

Aşağıdaki diyagramda, görev dizisinin sağlama modunun nasıl ayarladığı gösterilmektedir:

![Görev sırası ayarı sağlama modunun akış diyagramı](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>İstemci düzeltme

Aşağıdaki diyagramda istemcinin sağlama modundan nasıl çıkış olduğu gösterilmektedir:

![Kaynak sağlama modundan çıkmadan istemci akış diyagramı](media/3197824-client-flow.png)


## <a name="see-also"></a>Ayrıca bkz.

[Windows'u ve ConfigMgr'yi Kur](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[İşletim Sistemini Yükselt](task-sequence-steps.md#BKMK_UpgradeOS)
