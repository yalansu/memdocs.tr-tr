---
title: Bilinmeyen bilgisayar dağıtımlarına hazırlanma
titleSuffix: Configuration Manager
description: İşletim sistemlerini Configuration Manager ortamınızda Configuration Manager tarafından yönetilmeyen bilgisayarlara dağıtmayı öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724072"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Configuration Manager bilinmeyen bilgisayar dağıtımları için hazırlanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ortamınızdaki bilinmeyen bilgisayarlara işletim sistemi dağıtmak için bu konudaki bilgileri kullanın. Bilinmeyen bilgisayar, Configuration Manager tarafından yönetilmeyen bir bilgisayardır. Bu, Configuration Manager veritabanında bu bilgisayarların kaydı olmadığı anlamına gelir. Bilinmeyen bilgisayarlar aşağıdakileri içerir:  

- Configuration Manager istemcisinin yüklü olmadığı bir bilgisayar  

- Configuration Manager içine aktarılmayan bir bilgisayar  

- Configuration Manager tarafından bulunmayan bir bilgisayar  

  İşletim sistemlerini aşağıdaki dağıtım yöntemleriyle bilinmeyen bilgisayarlara dağıtabilirsiniz:  

- [Windows’u ağ üzerinden dağıtmak için PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Önyüklenebilir medya kullanarak işletim sistemini dağıtma](../deploy-use/create-bootable-media.md)  

- [Önceden hazırlanmış medya kullanarak işletim sistemini dağıtma](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Bilinmeyen bilgisayar dağıtımı iş akışı  
 Bilinmeyen bir bilgisayara işletim sistemi dağıtmaya yönelik temel iş akışı aşağıda verilmiştir:  

-   Dağıtımda kullanılacak bir bilinmeyen bilgisayar nesnesi seçin. İşletim sistemini **Tüm Bilinmeyen Bilgisayarlar** koleksiyonundaki bilinmeyen bilgisayar nesnelerinden birine dağıtabilir veya **Tüm Bilinmeyen Bilgisayarlar** koleksiyonundaki nesneleri başka bir koleksiyona ekleyebilirsiniz. Configuration Manager, **Tüm Bilinmeyen bilgisayarlar** koleksiyonunda iki bilinmeyen bilgisayar nesnesi sağlar. Nesnelerden biri x86 bilgisayarlar, diğeriyse x64 bilgisayarlar içindir.  

    > [!NOTE]  
    >  **x86 Bilinmeyen Bilgisayar** nesnesi yalnızca x86 özellikli bilgisayarlar içindir. **x64 Bilinmeyen Bilgisayar** nesnesi x86 ve x64 özellikli bilgisayarlar içindir. Diğer bir deyişle bu nesneler hedef bilgisayarın mimarisini tanımlar. Hedef bilgisayara dağıtmak istediğiniz işletim sistemini tanımlamaz.  

-   Bilinmeyen bilgisayar dağıtımlarını desteklemek üzere PXE özellikli bir dağıtım noktası yapılandırın veya medya oluşturun.  

-   İşletim sistemini dağıtmak için görev dizisini dağıtın.  

## <a name="unknown-computer-installation-process"></a>Bilinmeyen Bilgisayar Yükleme Süreci  
 Bir bilgisayar PXE 'den veya medyadan ilk kez başlatıldığında, Configuration Manager Configuration Manager veritabanında bu bilgisayar için bir kayıt olup olmadığını denetler. Bir kayıt varsa Configuration Manager, kayda dağıtılmış görev dizileri olup olmadığını kontrol eder. Kayıt yoksa, bilinmeyen bir bilgisayar nesnesine dağıtılmış görev dizileri olup olmadığını denetler Configuration Manager. Her iki durumda da Configuration Manager aşağıdaki eylemlerden birini gerçekleştirir:  

- Kullanılabilir bir görev sırası varsa Configuration Manager kullanıcıdan görev dizisini çalıştırmasını ister.  

- Gerekli bir görev sırası varsa, Configuration Manager görev dizisini otomatik olarak çalıştırır.  

- Kayıt için bir görev sırası dağıtılmamışsa, Configuration Manager hedef bilgisayar için dağıtılan bir görev sırası olmadığını belirten bir hata üretir.  

  Bilinmeyen bir bilgisayar başlatıldığında, bilgisayarı bilinmeyen bir bilgisayar yerine, sağlaması yapılmamış bir bilgisayar olarak tanır Configuration Manager. Buna göre, bilgisayar artık bilinmeyen bilgisayar nesnesine dağıtılmış görev dizilerini alabilir. Dağıtılan görev sırası daha sonra Configuration Manager istemcisini içermesi gereken bir işletim sistemi görüntüsü yüklüyor.  

  Configuration Manager istemcisi yüklendikten sonra, bilgisayar için bir kayıt oluşturulur ve bilgisayar uygun Configuration Manager koleksiyonunda listelenir. Bilgisayar işletim sistemi görüntüsünü veya Configuration Manager istemcisini yükleyemezse, bilgisayar için bir "Bilinmeyen" kaydı oluşturulur ve bilgisayar **Tüm sistemler** koleksiyonunda görünür.  

> [!NOTE]  
>  İşletim sistemi görüntüsünün yüklenmesi sırasında, görev dizisi bu bilgisayardan koleksiyon değişkenleri alabilir, ancak bilgisayar değişkenleri alamaz.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Bilinmeyen Bilgisayar Desteğini Etkinleştirme  
 Bir işletim sistemini PXE, önyüklenebilir medya ve önceden hazırlanmış medya kullanarak dağıttığınızda, bilinmeyen bilgisayar desteğini etkinleştirmek için aşağıdakileri kullanın.  

-   **PXE**  

     PXE için etkin olan bir dağıtım noktası için **PXE** sekmesinde **Bilinmeyen bilgisayar desteğini etkinleştir** onay kutusunu işaretleyin. Daha fazla bilgi için bkz. [PXE isteklerini kabul etmek için dağıtım noktaları yapılandırma](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Önyüklenebilir medya**  

     Görev Dizisi Medyası Oluşturma Sihirbazı'nın **Güvenlik** sayfasında **Bilinmeyen bilgisayar desteğini etkinleştir** onay kutusunu işaretleyin. Daha fazla bilgi için bkz. [PXE isteklerini kabul etmek için dağıtım noktalarını yapılandırma](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) ve [Configuration Manager Ile ağ üzerinden WINDOWS dağıtmak için PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Önhazırlığı yapılan medya**  

     Görev Dizisi Medyası Oluşturma Sihirbazı'nın **Güvenlik** sayfasında **Bilinmeyen bilgisayar desteğini etkinleştir** onay kutusunu işaretleyin. Daha fazla bilgi için bkz. [Configuration Manager ile önceden hazırlanmış medya oluşturma](../deploy-use/create-prestaged-media.md).  
