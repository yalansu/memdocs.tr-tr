---
title: Windows dağıtmak için tek başına medya kullanma
titleSuffix: Configuration Manager
description: Bilgisayar yenileme, yükleme veya yükseltme seçeneği olarak bant genişliğinin sınırlı olduğu Windows 'u dağıtmak için Configuration Manager tek başına medyayı kullanın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124661"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Ağı kullanmadan Windows dağıtmak için tek başına medya kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager tek başına medya, bir işletim sistemini bir bilgisayara dağıtmak için gereken her şeyi içerir. Medya, önyükleme görüntüsü, işletim sistemi görüntüsü, görev sırası ilkesi, uygulamalar, sürücüler ve daha fazlasını içerir. Tek başına medya dağıtımları, aşağıdaki durumlarda işletim sistemlerini dağıtmanızı sağlar:

- Bir işletim sistemi görüntüsünün veya başka büyük paketlerin ağ üzerinden kopyalanması pratik olmayan ortamlarda.

- Ağ bağlantısı olmayan ortamlarda veya düşük bant genişliğine sahip ağ bağlantısı.

Aşağıdaki işletim sistemi dağıtım senaryolarında tek başına medyayı kullanın:

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)

- [Windows’u en yeni sürüme yükseltme](upgrade-windows-to-the-latest-version.md)

Bu işletim sistemi dağıtım senaryolarından birindeki adımları doldurun. Ardından, tek başına medyayı hazırlamak ve oluşturmak için aşağıdaki bölümleri kullanın.

## <a name="unsupported-task-sequence-actions"></a>Desteklenmeyen görev sırası eylemleri

Tek başına medyayı kullandığınızda Configuration Manager, görev dizisinde aşağıdaki eylemleri desteklemez:

- [Sürücüleri otomatik olarak Uygula](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı. Aygıt sürücülerinin sürücü kataloğundan otomatik uygulaması desteklenmez. Windows Kurulumu için belirli bir sürücü kümesini kullanılabilir hale getirmek için, [sürücü paketini Uygula](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) adımını kullanın.

- Yazılım güncelleştirmelerinin yüklenmesi.

- İşletim sistemini dağıtmaya başlamadan önce yazılım yükleme.

- Kullanıcı cihaz benzeşimi için kullanıcıları hedef bilgisayarla ilişkilendirme.

- Dinamik paket, [paketi yükleme](../understand/task-sequence-steps.md#BKMK_InstallPackage) adımı ile yüklenir.

- Dinamik uygulama, [uygulama yükleme](../understand/task-sequence-steps.md#BKMK_InstallApplication) adımı ile yüklenir.

> [!NOTE]
> Bir işletim sistemini dağıtmaya yönelik görev diziniz **paket yükleme** adımını içeriyorsa ve tek başına medyayı merkezi yönetim SITESINDE (CAS) oluşturursanız bir hata oluşabilir. CA 'LAR, görev dizisi çalıştırıldığında yazılım dağıtım aracısını etkinleştirmek için gerekli istemci yapılandırma ilkelerine sahip değildir. **CreateTsMedia. log** dosyasında aşağıdaki hata görünebilir:
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> **Paket yükleme** adımını içeren tek başına medya için, tek başına medyayı yazılım dağıtım Aracısı etkinleştirilmiş bir birincil sitede oluşturun
>
> Alternatif olarak, [Windows 'u ve ConfigMgr 'Yi Kur](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) adımından sonra [komut satırı Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı eklemek için görev dizisini düzenleyin. Bu **komut satırını Çalıştır** adımı, Ilk **paketi Kur** adımı çalıştırılmadan önce yazılım dağıtım ARACıSıNı etkinleştirmek için aşağıdaki WMI komutunu çalıştırır:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma

İşletim sistemi dağıtım işlemini başlatmak üzere tek başına medya kullandığınızda, işletim sistemini medya tarafından kullanılabilir hale getirmek için dağıtımı yapılandırın. Dağıtımın **dağıtım ayarları** sayfasında, **aşağıdaki için kullanılabilir yap** ayarı için aşağıdaki seçeneklerden birini belirleyin:

- İstemcileri, medyayı ve PXE 'yi Configuration Manager

- Yalnızca medya ve PXE

- Yalnızca medya ve PXE (gizli)

## <a name="create-the-standalone-media"></a>Tek başına medyayı oluşturma

Tek başına medyanın bir USB flash sürücü veya CD/DVD seti olup olmadığını belirtebilirsiniz. Medyayı başlatacak bilgisayar önyüklenebilir sürücü olarak belirlediğiniz seçeneği desteklemelidir. Daha fazla bilgi için bkz. [tek başına medya oluşturma](create-stand-alone-media.md).

## <a name="install-the-os-from-standalone-media"></a>Tek başına medyadan işletim sistemini yükleme

İşletim sistemini yüklemek için, tek başına medyayı bilgisayara yerleştirin ve ardından üzerine gidin.

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemi dağıtımı için kullanıcı deneyimleri](../understand/user-experience.md#task-sequence-wizard)
