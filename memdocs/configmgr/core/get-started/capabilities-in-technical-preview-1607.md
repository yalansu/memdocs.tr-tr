---
title: Technical Preview 1607 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1607 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 73aac9e1bfb7b902a7db28ba4be00a2a02277324
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905691"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Configuration Manager için Technical Preview 1607 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1607 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>Windows 10 Sürüm Yükseltme İlkesindeki Geliştirmeler

Bu sürümde, bu ilkede aşağıdaki iyileştirmeler yapılmıştır:

* Artık Windows 10 bilgisayarlarının yanı sıra Configuration Manager istemcisini çalıştıran Windows 10 bilgisayarlarıyla sürüm yükseltme ilkesini kullanabilirsiniz Microsoft Intune.
* Windows 10 Professional 'dan donanımınızla uyumlu olan sihirbazda herhangi bir platforma yükseltebilirsiniz.

[Windows 10 sürüm yükseltme Ilkesi hakkında daha fazla bilgi edinin](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>Deneyin!

1. Sürüm yükseltme ilkesi oluşturmak için [Mevcut sürüm yükseltme ilkesi konusundaki](../../compliance/deploy-use/upgrade-windows-version.md) bilgileri kullanın.
2. Bu ilkeyi Configuration Manager istemcisini çalıştıran bir Windows 10 BILGISAYARıNA dağıtın.
İlke, hedeflenen bir Windows PC’ye ulaştığında, yükseltmenin uygulanması için PC iki saat içinde yeniden başlatılır. Şu anda bu yeniden başlatmayı gizlenemez. İlkeyi dağıttığınız kullanıcıları bilgilendirdiğinizden emin olun veya ilkeyi Kullanıcı çalışma saatleri dışında çalışacak şekilde zamanlayın.

### <a name="known-issue-with-this-release"></a>Bu sürümde bilinen sorun
Configuration Manager istemci ayarları ' nda, **sürüm yükseltme**için ayarları görebilirsiniz. Bu sürümde, bu ayarlar işlevsel değildir. Windows 10 ' un daha yeni bir sürüme yükseltilmesi için yukarıda verilen yönergeleri kullanın.

## <a name="customizable-branding-for-software-center-dialogs"></a>Yazılım Merkezi İletişimleri için Özelleştirilebilir Markalama

Yazılım Merkezi için özel marka Configuration Manager sürüm 1602 ' de kullanıma sunulmuştur. Technical Preview sürüm 1607 ' de, bu marka artık Yazılım Merkezi kullanıcılarına daha tutarlı bir deneyim sağlamak amacıyla ilişkili tüm iletişim kutularına ve görev çubuğu bildirimlerine genişletilir.

### <a name="try-it-out"></a>Deneyin!

Yazılım Merkezi için özel marka aşağıdaki kurallara göre uygulanır:

1. Uygulama Kataloğu Web sitesi noktası site sunucusu rolü yüklü değilse, Yazılım Merkezi, **Bilgisayar Aracısı** istemci ayarı **Yazılım Merkezi'nde görüntülenen kuruluş adı**’nda belirtilen kuruluş adını görüntüler. Yönergeler için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).

2. Uygulama Kataloğu web sitesi noktası site sunucusu rolü yüklüyse, Yazılım Merkezi Uygulama Kataloğu web sitesi noktası site sunucusu rolü özelliklerinde belirtilen kuruluş adını ve rengini görüntüler. Daha fazla bilgi için bkz. [Uygulama Kataloğu web sitesi noktası Için yapılandırma seçenekleri](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Microsoft Intune bir abonelik yapılandırılıp Configuration Manager ortamına bağlanırsa, Yazılım Merkezi, Intune Abonelik özelliklerinde belirtilen kuruluş adını, rengini ve Şirket logosunu görüntüler.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Birden çok PXE tarafından başlatılan dağıtımlar için aynı ağ bağdaştırıcısını kullan
Technical Preview sürüm 1607 ' de, birden çok cihazı (örneğin, birden çok cihazda kullandığınız USB Ethernet bağdaştırıcısı gibi) görüntülemek için bir Ethernet bağdaştırıcısı kullandığınızda, Ethernet bağdaştırıcıları için donanım tanımlayıcıları girmenize izin veren yeni bir ayarı etkinleştirebilirsiniz. Configuration Manager, PXE yüklemesi gerçekleştirirken ve istemci kaydı için listedeki donanım tanımlayıcılarını yoksayar.

Bu sorun hakkında daha fazla bilgi için bkz. [OSD destek ekibi blogu Configuration Manager](https://techcommunity.microsoft.com/t5/configuration-manager-archive/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in/ba-p/273721).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Yinelenen donanım tanımlayıcılarını yönetmek için özelliği etkinleştirin  
1. Configuration Manager konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **güncelleştirmeler ve bakım**  >  **özellikleri**' ne gidin.
2. Görüntü bölmesinde, **yinelenen donanım tanımlayıcılarını Yönet**' i seçin.
3. **Giriş** sekmesinde, **Özellikler** grubunda, **Aç**' a tıklayın.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Yoksayılacak Configuration Manager için donanım tanımlayıcıları ekleyin  
1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. **Giriş** sekmesinde, **Siteler** grubunda, **Hiyerarşi Ayarları**'nı tıklatın.
3. **Istemci onayı ve çakışan kayıtlar** sekmesine gidin.
4. Yeni donanım tanımlayıcıları eklemek için **yinelenen donanım tanımlayıcıları** bölümünde **Ekle** ' ye tıklayın.
