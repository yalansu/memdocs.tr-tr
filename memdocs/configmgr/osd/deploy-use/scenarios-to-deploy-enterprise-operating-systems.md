---
title: Kurumsal işletim sistemlerini dağıtma senaryoları
titleSuffix: Configuration Manager
description: Configuration Manager ile kurumsal işletim sistemlerini dağıtmaya yönelik çeşitli senaryolar hakkında bilgi edinin.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723771"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Configuration Manager ile kurumsal işletim sistemlerini dağıtma senaryoları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' de aşağıdaki işletim sistemi dağıtım senaryoları kullanılabilir:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Windows’u en yeni sürüme yükseltme
Bu senaryo, işletim sistemini Şu anda Windows 7, Windows 8.1 veya Windows 10 çalıştıran bilgisayarlarda yükseltir. Yükseltme işlemi, bilgisayardaki uygulamaları, ayarları ve Kullanıcı verilerini tutar. Windows ADK gibi dış bağımlılıklar yoktur. Bu işlem geleneksel işletim sistemi dağıtımlarından daha hızlı ve daha esnek olabilir.  

Daha fazla bilgi için bkz. [Windows 'u en son sürüme yükseltme](upgrade-windows-to-the-latest-version.md).


#### <a name="windows-autopilot-for-existing-devices"></a>Mevcut cihazlar için Windows Autopilot
<!--3607717, fka 1358333-->
Sürüm 1810 ' den başlayarak, mevcut cihazlar için Windows Autopilot, Windows 10 sürüm 1809 veya sonraki sürümlerde kullanılabilir. Bu özellik, tek bir Configuration Manager görev sırası kullanarak Windows Autopilot Kullanıcı odaklı mod için bir Windows 7 cihazını yeniden görüntünüzü ve sağlamanızı sağlar.

Daha fazla bilgi için bkz. [Mevcut cihazlar için Windows Autopilot](windows-autopilot-for-existing-devices.md).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme
Bu senaryo, var olan bir bilgisayarı bölümler ve biçimlendirir (siler) ve bilgisayara yeni bir işletim sistemi yüklenir. İşletim sistemi yüklendikten sonra ayarları ve Kullanıcı verilerini geçirebilirsiniz.  

Daha fazla bilgi için bkz. [var olan bir bilgisayarı yeni bir Windows sürümü Ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)
Bu senaryo yeni bir bilgisayara bir işletim sistemi yüklüyor. Bu, işletim sisteminin yeni bir yüklemesidir ve herhangi bir ayar veya Kullanıcı verisi geçişi içermez.  

Daha fazla bilgi için bkz. [Yeni bir bilgisayara yeni bir Windows sürümü (çıplak)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Mevcut bir bilgisayarı değiştirme ve ayarları aktarma
Bu senaryo yeni bir bilgisayara bir işletim sistemi yüklüyor. İsteğe bağlı olarak, eski bilgisayardaki ayarları ve kullanıcı verilerini yeni bilgisayara geçirebilirsiniz.  

Daha fazla bilgi için bkz. [var olan bir bilgisayarı değiştirme ve ayarları aktarma](replace-an-existing-computer-and-transfer-settings.md).


