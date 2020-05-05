---
title: LTSB 'yi güncel dala yükseltme
titleSuffix: Configuration Manager
description: Uzun süreli bakım dalı (LTSB) sitesini güncel bir dal sitesine dönüştürmeyi öğrenin.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722959"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Uzun süreli bakım dalını geçerli dala yükseltme

*Uygulama hedefi: System Center Configuration Manager (uzun süreli bakım dalı)*

Uzun süreli bakım dalı (LTSB) çalıştıran bir siteyi ve hiyerarşiyi Güncel Dalı Configuration Manager yükseltmeyi öğrenmek için bu konuyu kullanın.

Güncel Dalı kullanma hakkı veren geçerli bir yazılım güvencesi anlaşmanız (veya benzer lisanslama haklarınız) varsa, yüklemenizi LTSB 'den Güncel Dalı dönüştürebilirsiniz.  Bu tek yönlü bir dönüştürmedir çünkü bir Güncel Dalı sitesini LTSB 'ye dönüştürmeye yönelik destek yoktur.

Birden çok siteniz varsa, yalnızca hiyerarşinizin üst katman sitesini dönüştürmeniz gerekir. Üst katman sitesi dönüştürüldükten sonra:
- Alt birincil siteler otomatik olarak dönüştürülür.
- İkincil siteleri Configuration Manager konsolunun içinden el ile güncelleştirmeniz gerekir.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Uzun süreli bakım dalını dönüştürmek için kurulumu çalıştırın
Hiyerarşinizin üst katman sitesinde, uygun taban medyasından Configuration Manager kurulumu çalıştırabilir ve **Site Bakımı**' nı seçebilirsiniz.  Daha sonra, lisanslama sayfasıyla birlikte Güncel Dalı seçeneğini belirleyin ve Sihirbazı doldurun.

Siteniz Güncel Dalı dönüştürüldüğünde, önceden kullanılamayan özellikler ve özellikler kullanıma sunulacaktır.

> [!NOTE]  
> Uygun temel medya, LTSB yüklemenize eşit veya ondan daha yeni bir sürüme sahip olan bir ortamdır.

Örneğin, LTSB sürümü 1606 ' i temel oluşturduğundan, Güncel Dalı dönüştürmek için Baseline 1511 medyasını kullanamazsınız. Bunun yerine, kurulum 'u LTSB sitesini yüklemek için kullandığınız sürüm 1606 temel medyasından çalıştırın ve Güncel Dalı için lisans seçeneğini belirleyin.  Alternatif olarak, Güncel Dalı sonraki bir taban çizgisi yayımlanmışsa, kurulum 'u bu ana hat medyasından çalıştırabilirsiniz.

Temel sürümlerin bir listesi için bkz. [Configuration Manager güncelleştirmelerde](../servers/manage/updates.md) **temel ve güncelleştirme sürümleri** .

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Uzun süreli bakım dalını dönüştürmek için Configuration Manager konsolunu kullanın
Siteniz LTSB 'yi çalıştırıyorsa, Güncel Dalı dönüştürmek için Configuration Manager konsolundaki aşağıdaki seçeneği kullanabilirsiniz:

 1. Konsolunda, **Yönetim** > **Site yapılandırması** > **siteler**' e gidin ve ardından **Hiyerarşi ayarları**' nı açın.  

 2. **Hiyerarşi ayarları**' nda **lisanslama** sekmesine geçin. **güncel dalı dönüştürme**seçeneğini belirleyin ve ardından **Uygula**' yı seçin.  

Siteniz Güncel Dalı dönüştürüldüğünde, önceden kullanılamayan özellikler ve özellikler kullanıma sunulacaktır.
