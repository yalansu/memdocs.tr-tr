---
title: Windows 10 için destek
titleSuffix: Configuration Manager
description: Configuration Manager ile istemci veya OSD için desteklenen Windows 10 sürümleri hakkında bilgi edinin
ms.date: 05/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a67a22f788af39dacb9f3a39e91e0f28444c6988
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879069"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Configuration Manager 'de Windows 10 için destek  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager desteklediği Windows 10 sürümleri hakkında bilgi edinin, şunlar dahil:

- [Configuration Manager istemcisi olarak Windows 10](#windows-10-as-a-client)
- [Windows 10 için Windows değerlendirme ve Dağıtım Seti (ADK)](#windows-10-adk)

> [!Tip]
> İstemci olarak Windows Server derlemeleri, ilişkili Windows 10 sürümüyle aynı şekilde desteklenir. Örneğin, Windows Server 2016, Windows 10 LTSB 2016 ile aynı derleme sürümüdür ve Windows Server sürüm 1803, Windows 10 sürüm 1803 ile aynı derleme sürümüdür.
>
> Site sistemi olarak Windows Server hakkında daha fazla bilgi için bkz. [Configuration Manager site sistemi sunucuları Için desteklenen işletim sistemleri](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>İstemci olarak Windows 10

Configuration Manager, her yeni Windows 10 sürümü için kullanılabilir hale geldikten hemen sonra destek sağlamaya çalışır. Ürünlerin ayrı geliştirme ve sürüm zamanlamalarına sahip olduğu için Configuration Manager desteği, her biri kullanılabilir hale geldiğinde ' ı sağlar.

Configuration Manager sürüm, [Bu sürüm için destek](../../servers/manage/current-branch-versions-supported.md) sona erdikten sonra matris üzerinden düşecektir. Benzer şekilde, Kurumsal 2015 LTSB veya 1511 gibi Windows 10 sürümleri için destek, destek 'ten kaldırıldığında matrisin dışında bırakılır.

- Güncel dalın Configuration Manager en son sürümü, güvenlik ve kritik güncelleştirmeleri alır ve bu, Windows 10 sürümleriyle ilgili sorunları gidermeye yönelik düzeltmeler içerir. Microsoft Configuration Manager geçerli dalın yeni bir sürümünü yayımlarsa, önceki sürümler yalnızca güvenlik güncelleştirmelerini alırlar. Daha fazla bilgi için bkz. [Configuration Manager geçerli dal sürümleri Için destek](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > Windows 10 ile güncel kalabilmek için en iyi yol Configuration Manager ile güncel kalmanız. Daha fazla bilgi için bkz. [hizmet olarak Configuration Manager ve Windows](../../understand/configuration-manager-and-windows-as-service.md).  

- Bu bilgiler [, istemciler ve cihazlar Için desteklenen işletim sistemlerini](supported-operating-systems-for-clients-and-devices.md)tamamlar.  

- Configuration Manager uzun süreli bakım dalını kullanıyorsanız, bkz. [uzun süreli bakım dalı Için desteklenen konfigürasyonlar](../../understand/supported-configurations-for-ltsb.md).  

Aşağıdaki tabloda, farklı Configuration Manager sürümleriyle istemci olarak kullanabileceğiniz Windows 10 sürümleri listelenmiştir.

| Windows 10 sürümü | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Kurumsal 2015 LTSB** <!--10/14/2025-->   | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **Kurumsal 2016 LTSB** <!--10/13/2026-->   | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **Kurumsal LTSC 2019** <!--01/09/2029-->   | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--10/13/2020-->   | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Desteklenmiyor](media/Red_X.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/10/2022-->   | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **2004**<br>(10.0.19041)   <!--??/??/2021-->   | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Destekleniyor](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Windows yaşam döngüsü hakkında daha fazla bilgi için bkz. [Windows yaşam döngüsü olgu sayfası](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

| Anahtar |
|--|
| ![Desteklenen ](media/green_check.png)  =  **Supported** destekleniyor  |
| ![Desteklenmeyen desteklenmez ](media/Red_X.png)  =  **Not supported** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a>Windows 10 istemci destek notları

- Windows 10 yarı yıllık kanal sürümleri için destek aşağıdaki sürümleri içerir: Enterprise, Pro, eğitim ve Pro eğitim.  

- Sürüm 1906 ' den başlayarak, Configuration Manager Iş Istasyonu için Windows 10 Pro 'Yu destekler.

- Windows 10, sürüm 1909 için, işletim sistemi dağıtımı medyası sürümü 10.0.18362.418 olarak gösterir.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a>ARM64 üzerinde Windows 10

Configuration Manager, Windows 10 ARM64 cihazlarında istemciyi destekler. İşletim sistemi dağıtımı desteklenmiyor.<!-- 1353704 -->

Sürüm 2002 ' den başlayarak,<!--5954175--> **tüm Windows 10 (ARM64)** platformu, gereksinim kuralları veya uygulanabilirlik listeleri olan nesnelerde desteklenen işletim sistemi sürümleri listesinde bulunur.

> [!NOTE]
> En üst düzey **Windows 10** platformunu daha önce seçtiyseniz, bu eylem hem **tüm windows 10 (64-bit)** hem de **tüm Windows 10 (32-bit)**' i otomatik olarak seçti. Bu yeni platform otomatik olarak seçilmedi. **Tüm Windows 10 (ARM64)** eklemek istiyorsanız, listeden el ile seçin.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a>Windows Insider desteği

Configuration Manager sürüm 1906 ' den başlayarak, [Windows Insider derlemelerini güncelleştirebilir ve hizmet](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) verebilirsiniz. Bu özellik, müşterilerimize kolaylık sağlaması olarak sunulmaktadır. Bu işlevselliğin çalışması gerektiği sürece, için destek en iyi çabadır. Configuration Manager, bu işlevin işlevine başlanmasıyla ilgili bir düzeltme yayınmayabilir.  

Windows Insider hakkında geri bildirim sağlamak için [Geri Bildirim Hub 'ını](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback)kullanın.

## <a name="windows-10-adk"></a>Windows 10 ADK

İşletim sistemlerini Configuration Manager dağıtırken, Windows ADK gerekli bir dış bağımlılığıdır. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [İşletim sistemi dağıtımı için altyapı gereksinimleri](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Windows 10 için Windows ADK’yi indirin](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Windows 10 sürüm 1809 ' den itibaren, Windows PE ayrı bir yükleyicidir. Aksi takdirde işlevsel farklılık yoktur.
    >
    > ADK için hem Windows **10 Için WINDOWS ADK** hem de **Windows PE eklentisi**' ni indirdiğinizden emin olun.

Aşağıdaki tabloda, farklı Configuration Manager sürümleriyle kullanabileceğiniz Windows 10 ADK 'nin sürümleri listelenmektedir.

| Windows 10 ADK sürümü  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Desteklenmiyor](media/Red_X.png)   | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Geriye dönük uyumlu](media/blue_compat.png) | ![Geriye dönük uyumlu](media/blue_compat.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Geriye dönük uyumlu](media/blue_compat.png) | ![Geriye dönük uyumlu](media/blue_compat.png) | ![Desteklenmiyor](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Desteklenmiyor](media/Red_X.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) | ![Destekleniyor](media/green_check.png) |
| **2004**<br>(10.1.19041) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Desteklenmiyor](media/Red_X.png) | ![Destekleniyor](media/green_check.png) |

|Anahtar|
|--|
| ![Desteklenen ](media/green_check.png)  =  **Supported** destekleniyor <br/> Bu tabloda yalnızca Configuration Manager sürümüyle ilgili olarak Windows ADK desteklenebilirliği gösterilmektedir. Microsoft, dağıttığınız Windows sürümüyle eşleşen Windows ADK kullanılmasını önerir. En son Windows 10 sürümünü dağıttığınızda en son Windows ADK sürümünü kullanın. En son Windows ADK sürümü, Windows 8.1 gibi eski işletim sistemi sürümlerinin dağıtımını destekleyebilir.<!-- SCCMDocs issue 1229 --> Windows ADK bileşeni desteklenebilirliği hakkında daha fazla bilgi için bkz. [DISM desteklenen platformlar](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) ve [USMT gereksinimleri](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Geriye dönük uyumlu ](media/blue_compat.png)   =  **geriye dönük uyumlu** <br/> Bu bileşim test değildir ancak çalışmalıdır. Bilinen tüm sorunları veya uyarıları belgeliyoruz. |
| ![Desteklenmeyen desteklenmez ](media/Red_X.png)  =  **Not supported** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a>Windows 10 ADK destek notları

- Configuration Manager yalnızca Windows 10 ADK 'nin x86 ve AMD64 bileşenlerini destekler. Bu, şu anda ARM veya ARM64 bileşenlerini desteklememektedir.

- Windows Server derlemeleri, ilişkili Windows 10 sürümü ile aynı Windows ADK gereksinimine sahiptir. Örneğin, Windows Server 2016, Windows 10 LTSB 2016 ile aynı derleme sürümüdür.
