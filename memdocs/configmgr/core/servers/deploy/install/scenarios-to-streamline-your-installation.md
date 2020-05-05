---
title: Yükleme senaryoları
titleSuffix: Configuration Manager
description: Bir siteyi güncelleştirirken veya yükseltirken yeni bir Configuration Manager hiyerarşi yükleme tekniklerini öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718101"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Configuration Manager yüklemenizin kolaylaştırılmasına yönelik senaryolar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme sürümleri yayınlanmasıyla, yeni bir hiyerarşinin güncelleştirme sürümüne (güncelleştirme 1610 gibi) yüklenmesini ve Microsoft System Center 2012 Configuration Manager yükseltmesini kolaylaştırmak için yeni senaryolar vardır.

Desteklenen senaryolar:  

Bir güncelleştirme sürümü çalıştıran **Yeni bir Configuration Manager geçerli dal hiyerarşisi yükler** .  

-   Yalnızca üst katman siteyi yükler ve ardından bu siteyi kullanacağınız güncelleştirme sürümüyle güncel hale getirmek için hemen bir güncelleştirme yükleyebilirsiniz. Daha sonra, bu güncelleştirme sürümüne doğrudan ek siteler yükleyebilirsiniz.  
-   Bu senaryoda, ek siteleri bir temel düzeyine yükleme işlemini atlar ve sonra bunları kullanmak istediğiniz güncelleştirme sürümüne güncelleştirebilirsiniz.  
-   Bu senaryoda, bir temel sürüme istemci yükleme işlemini atlar ve daha sonra bu sürüme güncelleştirdiğinizde bunları yeniden yükleyebilirsiniz.  

**Bir Microsoft System Center 2012 Configuration Manager** altyapısını Configuration Manager güncelleştirme sürümüne yükseltin.  

-   Bir güncelleştirme sürümü (sürüm 1610 gibi) yüklemeden önce Merkezi Yönetim sitenizi ve her birincil siteyi bir temel sürüme (sürüm 1606 gibi) el ile yükseltin.  
-   Birincil siteleriniz kullanacağınız güncelleştirme sürümünü çalıştırana kadar, Microsoft System Center 2012 Configuration Manager ikincil siteleri yükseltmeyin.  
-   Birincil siteleriniz kullanacağınız güncelleştirme sürümünü çalıştırana kadar, Microsoft System Center 2012 Configuration Manager istemcileri yükseltmeyin.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Senaryo: bir güncelleştirme sürümüne yeni bir hiyerarşi yükler  
Bu örnek senaryoda, bir hiyerarşinin ilk sitesini sürüm 1610 gibi Configuration Manager temel bir sürümünü kullanarak yüklersiniz. Daha sonra, ek siteleri veya istemcileri dağıtmadan önce 1610 güncelleştirmesini yükleyebilirsiniz.  

-   Bir güncelleştirme sürümü (sürüm 1610 gibi) kullanmayı planlıyorsunuz ve temel bir sürümde (sürüm 1606 gibi) kalmadığından, ek siteler yüklemeniz ve sonra bunları yükseltmeniz gerekmez. Bu, istemciler için de geçerlidir.  
-   Sürüm 1606 ile ikincil siteleri yüklemeyin ve ardından bunları 1610 sürümüne yükseltin. Bunun yerine, birincil siteleriniz sürüm 1610 ' i çalıştırdıktan sonra ikincil siteleri yüklemelisiniz.  

Bu sırayı izleyin:  

1. Temel medyayı kullanarak **Yeni hiyerarşiniz için en üst düzey bir site yükler** .  

   -   Temel medyayı yalnızca yeni bir hiyerarşinin ilk sitesini yüklemek için kullanabilirsiniz.  
   -   Örneğin, 1606 temel sürümünü kullanarak en üst düzey bir site yükler. Daha fazla bilgi için bkz. [siteleri yüklemek Için Kurulum Sihirbazı 'Nı kullanma](use-the-setup-wizard-to-install-sites.md).  

   Bu adımdan sonra, en üst düzey siteniz 1606 sürümünü çalıştırır.  

2. **En üst düzey sitenizi daha sonraki bir sürüme güncelleştirmek için konsol içi güncelleştirmeleri kullanın.**  

   -   Herhangi bir alt site veya istemci yüklemeden önce en üst düzey sitenizi kullanmayı planladığınız güncelleştirme sürümüne güncelleştirin.  
   -   Örneğin, 1606 sürümünü çalıştıran en üst düzey sitenizi 1610 sürümüne güncelleştirebilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../../../../core/servers/manage/updates.md).  

   Bu adımdan sonra, en üst düzey siteniz 1610 sürümünü çalıştırır.  

3. **Bir merkezi yönetim sitesinin altına yeni alt birincil siteleri yükleyin.**  

   - Alt birincil siteleri yüklemek için merkezi yönetim site sunucusunda bulunan CD.Latest klasöründeki yükleme medyasını kullanın. Daha fazla bilgi için [CD 'ye bakın. Configuration Manager için en son klasör](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Bu kaynak medya, yeni alt birincil sitelerin merkezi yönetim sitesiyle eşleştiğinden emin olmak için gereklidir.  

   Bu adımdan sonra yeni alt birincil siteleriniz 1610 sürümünü çalıştırır.  

4. **Her birincil sitede, yeni ikincil siteleri yüklemek için konsol içi seçeneğini kullanın.**  

   -   Birincil siteler sürüm 1606 ' de iken ikincil siteleri yüklememiş olduğunuzdan, ikincil siteleri yükseltmeniz gerekmez.  
   -   Bunun yerine 1610 sürümünü çalıştıran yeni ikincil siteleri yükler. Daha fazla bilgi için, [Siteleri yüklemek için Kurulum Sihirbazı’nı kullanma](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) konu başlığı altındaki [İkincil siteyi yükleme](use-the-setup-wizard-to-install-sites.md) bölümüne bakın.  

   Bu adımdan sonra yeni ikincil siteler yüklenir ve 1610 sürümünü çalıştırır.  

5. **Birincil siteye yeni istemcileri yükler.**  

   -   Birincil siteler sürüm 1606 ' de olan istemcileri yüklememiş olduğunuzdan, istemcileri 1606 sürümünden sürüm 1610 sürümüne yükseltmeniz gerekmez.  
   -   Bunun yerine 1610 sürümünü çalıştıran yeni istemciler yüklersiniz. Daha fazla bilgi için bkz. [Istemcileri dağıtma](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Bu adımdan sonra 1610 sürümünü çalıştıran yeni istemciler yüklenir.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Senaryo: System Center 2012 Configuration Manager Configuration Manager, geçerli dalın bir güncelleştirme sürümüne yükseltin  

Bu örnek senaryoda, System Center 2012 Configuration Manager altyapınızı, sürüm 1610 gibi Configuration Manager geçerli dalın bir güncelleştirme sürümüne yükseltin.  

-   Merkezi Yönetim sitesi ve tüm birincil siteler, 1610 sürümüne yönelik güncelleştirmeyi yüklemeden önce temel 1606 sürümüne yükseltilmelidir.  
-   İkincil siteler ve istemciler 1606 sürümünü yükseltmez ve yüklemez. Bunun yerine, doğrudan System Center 2012 Configuration Manager Configuration Manager geçerli dal sürümü 1610 ' e taşınır.  

Bu sırayı izleyin:  

1. **En üst düzey System Center 2012 Configuration Manager sitenizi** , Configuration Manager için kaynak medyayı (sürüm 1606 gibi) kullanarak geçerli dalın temel bir sürümüne yükseltin. Daha fazla bilgi için bkz. [Configuration Manager yükseltme](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Geleneksel yükseltme senaryolarında olduğu gibi, önce hiyerarşinin en üst düzey sitesini her zaman yükseltmeniz ve ardından alt siteleri yükseltmeniz gerekir.  

   Bu adımdan sonra, en üst düzey siteniz 1606 sürümünü çalıştırır.  

2. **Hiyerarşinizdeki** alt birincil siteleri aynı temel sürüme yükseltin.  

   -   Microsoft System Center 2012 Configuration Manager yükselttiğinizde, her birincil siteyi geçerli dalın temel bir sürümüne elle yükseltmeniz gerekir.  
   -   Bu noktada ikincil siteleri yükseltmeyecektir.  

   Bu adımdan sonra her birincil site 1606 sürümünü çalıştırır.  

3. **Alt birincil sitelerde bakım pencereleri ayarlayın.** Tüm birincil sitelerinizi temel sürüme yükselttikten sonra, bu sitelerin altyapı güncelleştirmelerini ne zaman yükleyeceğini denetlemek için bakım pencerelerini yapılandırmayı planlayın. Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Bakım pencereleri 1606 sürümündeki *hizmet pencereleri* olarak adlandırılır.)  

   -   Bir alt birincil site bir merkezi yönetim sitesine yüklediğiniz güncelleştirmelerin aynısını otomatik yükler.  
   -   İkincil slikler yeni sürümleri otomatik olarak yüklemez. Bunları konsolunun içinden el ile yükseltmeniz gerekir.  

   Bu adımdan sonra, merkezi yönetim sitesinde güncelleştirme yüklediğinizde, alt birincil siteler bakım pencereleri izin verdiğinde yalnızca o güncelleştirmeleri yükler.  

4. **Güncelleştirme sürümünü en üst düzey sitenize yükler.** Bu, en üst düzey sitenizi güncelleştirir. Bir merkezi yönetim sitesi güncelleştirme sürümünü yükledikten sonra, yükleme bir bakım penceresi tarafından engellenmediği takdirde her bir alt birincil site güncelleştirmeyi otomatik olarak yüklenir.  

   -   Örneğin, en üst düzey sitenizi 1606 sürümünden 1610 sürümüne güncelleştirebilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../../../../core/servers/manage/updates.md).  

   Bu adımdan sonra merkezi yönetim siteniz ve birincil siteler 1610 sürümünü çalıştırır.  

5. **İkincil siteleri yükseltin.** Bir birincil site güncelleştirmeyi yükledikten ve 1610 sürümünü çalıştırdıktan sonra ikincil siteleri yükseltmek için konsol içi seçeneğini kullanın.  

   -   Bu, ikincil siteleri doğrudan Microsoft System Center 2012 Configuration Manager 'den birincil siteye yüklediğiniz güncelleştirme sürümüne yükseltir.  
   -   İkincil bir siteyi yükseltme hakkında daha fazla bilgi için, [Configuration Manager yükseltme](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) Içindeki [siteleri yükseltme](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) konusuna bakın.  

6. **İstemcileri yükseltin.** İstemcileri yükseltmek için, [Windows bilgisayarları için istemcileri yükseltme](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)bölümündeki bilgileri kullanın.  

   -   Bu, istemcileri doğrudan Microsoft System Center 2012 Configuration Manager 'den birincil siteye yüklediğiniz güncelleştirme sürümüne yükseltir.  

   Bu adımdan sonra istemciler, önce 1606 sürümüne yükseltmeden önce sürüm 1610 ' e yükseltilir.
