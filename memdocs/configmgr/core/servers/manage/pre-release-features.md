---
title: Yayın öncesi özellikler
titleSuffix: Configuration Manager
description: Yayın öncesi özellikler, bir üretim ortamında erken test için geçerli dalda olan özelliklerdir.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720159"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager yayın öncesi Özellikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yayın öncesi özellikler, bir üretim ortamında erken test için geçerli dalda olan özelliklerdir. Bu özellikler tam olarak desteklenir, ancak hala etkin geliştirme aşamasındadır. Yayın öncesi kategorisinden taşınana kadar değişiklikler alabilir.

## <a name="give-consent"></a>Onay verme  

Yayın öncesi özellikleri kullanmadan önce yayın öncesi özellikleri kullanmak için izin verin. İzin verme, geri alamazsınız hiyerarşi başına tek seferlik bir eylemdir. İzin verene kadar, güncelleştirmelerde bulunan yeni yayın öncesi özellikleri etkinleştiremezsiniz. Yayın öncesi özelliğini etkinleştirdikten sonra devre dışı bırakabilirsiniz.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Şeritte **Hiyerarşi ayarları** ' na tıklayın.  

3. Hiyerarşi ayarları özelliklerinin **genel** sekmesinde, **yayın öncesi özellikleri kullanma onay**seçeneğini etkinleştirin. **Tamam**'a tıklayın.  

## <a name="enable-pre-release-features"></a>Yayın öncesi özellikleri etkinleştir

Yayın öncesi özellikleri içeren bir güncelleştirme yüklediğinizde, bu özellikler güncelleştirmeler ve Bakım Sihirbazı 'nda, güncelleştirmede bulunan düzenli özelliklerle görünür.

### <a name="if-you-have-given-consent"></a>İzin verildiyse

Güncelleştirmeler ve Bakım Sihirbazı 'nda yayın öncesi özellikleri etkinleştirin. Başka herhangi bir özellik gibi yayın öncesi özellikleri seçin.

İsteğe bağlı olarak, **Yönetim** çalışma alanındaki **güncelleştirmeler ve bakım** altındaki **Özellikler** düğümünden daha sonra yayın öncesi özellikleri etkinleştirmeyi bekleyin. Bir özellik seçin ve ardından şeritte **Aç** ' a tıklayın. İzin verene kadar bu seçenek kullanılamaz.

### <a name="if-you-havent-given-consent"></a>İzin verilmemişse

Güncelleştirmeler ve Bakım Sihirbazı 'nda yayın öncesi özellikler görünür ancak bunları etkinleştiremezsiniz. Güncelleştirme yüklendikten sonra, bu özellikler **Özellikler** düğümünde görünür. Ancak, izin verip vermeene kadar etkinleştiremezsiniz.

> [!IMPORTANT]  
> Çok siteli bir hiyerarşide, merkezi yönetim sitesinden yalnızca isteğe bağlı veya yayın öncesi özellikleri etkinleştirebilirsiniz. Bu davranış, hiyerarşide çakışma olmamasını sağlar. <!--507197-->  
>
> Tek başına bir birincil sitede onay vermiş ve sonra yeni bir merkezi yönetim sitesi yükleyerek hiyerarşiyi genişlettikten sonra, merkezi yönetim sitesinde tekrar onay vermeniz gerekir.  

Yayın öncesi özelliğini etkinleştirdiğinizde, bu özellik kullanılabilir hale gelmeden önce Configuration Manager hiyerarşi Yöneticisi (HMAN) değişikliği işlemesi gerekir. Değişikliğin işlenmesi genellikle anında gerçekleşir. HMAN işleme döngüsüne bağlı olarak, tamamlanması 30 dakika kadar sürebilir. Değişiklik işlendikten sonra, özelliği kullanmadan önce konsolunu yeniden başlatın.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a>Yayın öncesi özellikler listesi

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Özellik          | Yayın öncesi olarak eklendi | Tam özellik olarak eklendi |
|------------------|----------------------|-------------------------|
| [Düzenleme grupları](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Sürüm 2002 | ![Henüz değil](media/red_x.png) |
| [Görev sırası dağıtım türü](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Sürüm 2002 | ![Henüz değil](media/red_x.png) |
| [Merkezi yönetim sitesini kaldırma](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Sürüm 2002 | ![Henüz değil](media/red_x.png) |
| [Görev sırası hata ayıklayıcısı](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Sürüm 1906 | ![Henüz değil](media/red_x.png) |
| [Uygulama grupları](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Sürüm 1906 | ![Henüz değil](media/red_x.png) |
| [Kullanıcı grubu bulmayı Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Sürüm 1906 | Sürüm 2002 |
| [Koleksiyon üyeliği sonuçlarını Azure Active Directory ile eşitler](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Sürüm 1906| Sürüm 2002 |
| [Tek başına CMPivot](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Sürüm 1906 | Sürüm 2002 |
| [SMS Sağlayıcısı yönetim hizmeti](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Sürüm 1810 | Sürüm 1906 |
| [Gelişmiş HTTP sitesi sistemi](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Sürüm 1806 | Sürüm 1810 |
| [Ortak yönetilen cihazlar için istemci uygulamaları](../../../comanage/workloads.md#client-apps) <br/> (daha önce *ortak yönetilen cihazlar Için mobil uygulamalar*olarak biliniyordu) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Sürüm 1806 | Sürüm 2002 |
| [Paket Dönüştürme Yöneticisi](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Sürüm 1806 | Sürüm 1810 |
| [Aşamalı dağıtımlar](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Sürüm 1802 | Sürüm 1806 |
| [Windows Defender Uygulama Denetimi yönetimi](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Sürüm 1702 | Sürüm 1906 |
| [Küme durumunu algılayan bir koleksiyona hizmet verme (sunucu grupları)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Sürüm 1602 | ![Henüz değil](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> İlk olarak etkinleştirmeniz gereken yayın öncesi olmayan özellikler hakkında daha fazla bilgi için bkz. [güncelleştirmelerden isteğe bağlı özellikleri etkinleştirme](install-in-console-updates.md#bkmk_options).  
>
> Yalnızca Technical Preview dalında bulunan özellikler hakkında daha fazla bilgi için bkz. [Technical Preview](../../get-started/technical-preview.md).  
