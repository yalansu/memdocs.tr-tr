---
title: Windows için istemci yükseltmelerini hariç tut
titleSuffix: Configuration Manager
description: Windows istemcilerinin Configuration Manager 'den yükseltilme 'den nasıl dışlanacağını öğrenin.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715420"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Configuration Manager ' de istemcileri yükseltmeden dışlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemcilerin bir koleksiyonunu, güncelleştirilmiş istemci sürümlerini otomatik olarak yükleyerek dışlayabilirsiniz. İstemciyi yükseltirken daha fazla dikkatli olması gereken bir bilgisayar koleksiyonu için bu dışlamayı kullanın. Dışlanan bir koleksiyonda bulunan bir istemci, güncelleştirilmiş istemci yazılımını yüklemek için istekleri yoksayar.

Bu dışlama aşağıdaki yöntemler için geçerlidir:

- Otomatik yükseltme
- Yazılım güncelleştirmesi tabanlı yükseltme
- Oturum açma betikleri
- Grup İlkesi

> [!NOTE]
> Kullanıcı arabirimi istemcilerin herhangi bir yöntem aracılığıyla yükseltmeyeceği durumlara karşın, bu ayarları geçersiz kılmak için kullanabileceğiniz iki yöntem vardır. Bu yapılandırmayı geçersiz kılmak için istemci gönderme veya el ile istemci yükleme kullanın. Daha fazla bilgi için bkz. [Dışlanan istemciyi yükseltme](#bkmk_override).

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a>Dışlamayı yapılandırma

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin, **siteler** düğümünü seçin ve ardından şeritte **Hiyerarşi ayarları** ' nı seçin.

2. **Istemci yükseltme** sekmesine geçin.

3. **Belirtilen istemcileri yükseltmeden dışlama**seçeneğini belirleyin. Sonra dışlamak istediğiniz **dışlama koleksiyonunu** seçin. Yalnızca dışlama için tek bir koleksiyon seçebilirsiniz.

4. Kapatmak ve yapılandırmayı kaydetmek için **Tamam ' ı** seçin.

![Otomatik yükseltme dışlama ayarları](media/automatic_upgrade_exclusion.png)

Dışlanan koleksiyon güncelleştirme ilkesindeki istemciler, istemci güncelleştirmelerini otomatik olarak yüklemez. Daha fazla bilgi için bkz. [Windows bilgisayarları için istemcileri yükseltme](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Dışlanan istemciler hala CCMSetup 'ı indirir ve çalıştırır, ancak yükseltmeyin.

Bir istemciyi dışlama koleksiyonundan kaldırdığınızda, sonraki otomatik yükseltme döngüsüne kadar otomatik olarak yükseltilmez.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a>Dışlanan bir istemciyi yükseltme

Bir cihaz, yükseltmeden hariç tutulan bir koleksiyonun üyesiyse, aşağıdaki yöntemlerden birini kullanarak istemciyi yine de yükseltebilirsiniz:

- **Client Push yüklemesi**: CCMSetup, doğrudan sizin amacınızı sağladığından Client Push yüklemesine izin verir. Bu yöntem, bir istemciyi koleksiyondan kaldırmadan yükseltmenizi veya tüm koleksiyonu dışlamadan kaldırmayı sağlar.

- **El ile istemci yüklemesi**: aşağıdaki CCMSetup komut satırı parametresini kullanarak dışlanan bir istemciyi el ile yükseltin: **/IgnoreSkipUpgrade**

    Dışlanan koleksiyonun üyesi olan bir istemciyi el ile yükseltmeye çalışırsanız ve bu parametreyi kullanmıyorsanız, istemci yükseltmez. Daha fazla bilgi için bkz. [Configuration Manager istemcilerini El Ile nasıl yüklenir](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## <a name="see-also"></a>Ayrıca bkz.

- [İstemcileri yükseltin](upgrade-clients.md)

- [İstemcileri Windows bilgisayarlara dağıtma](../../deploy/deploy-clients-to-windows-computers.md)

- [Genişletilmiş birlikte çalışabilirlik istemcisi](../../../understand/interoperability-client.md)
