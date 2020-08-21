---
title: Site sistemi rolleri yükleme
titleSuffix: Configuration Manager
description: Site sistem rollerini sitedeki mevcut veya yeni bir site sistemi sunucusuna ekleyin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 30b57de75e637aa083070832783647b8ad35b4a7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700540"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Configuration Manager için site sistemi rollerini yükler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolunda, site sistemi rollerini yüklemek için iki yöntem vardır:

- **Site sistemi rolleri ekleme**: site sistem rollerini sitedeki mevcut bir site sistemi sunucusuna ekleyin.

- **Site sistemi sunucusu oluştur**: site sistemi sunucusu olarak yeni bir sunucu belirtin ve ardından bir veya daha fazla rol yükler. Bu yöntem, ilk sayfa hariç, **site sistemi rolleri ekleme**ile aynıdır. İlk olarak, sunucu adını ve yüklemek istediğiniz siteyi belirtmeniz gerekir.

> [!TIP]
> Uzak bilgisayara bir rol yüklediğinizde Configuration Manager, uzak bilgisayarın bilgisayar hesabını site sunucusundaki yerel bir gruba ekler.
>
> Siteyi bir etki alanı denetleyicisine yüklediğinizde, site sunucusundaki grup bir yerel Grup yerine bir etki alanı grubudur. Bu durumda, uzak site sistemi rolü hemen çalışmaz. Site sistemi sunucusunun yeniden başlatılması veya uzak sunucunun bilgisayar hesabı için Kerberos anahtarını yenilemeniz gerekir. Daha fazla bilgi için bkz. [kullanılan hesaplar](../../../plan-design/hierarchy/accounts.md).

Site sistemi rolünü yüklemeden önce, Configuration Manager seçili rollerin önkoşullarını karşıladığından emin olmak için hedef bilgisayarı denetler.

Varsayılan olarak, Configuration Manager bir site sistem rolü yüklediğinde, en fazla kullanılabilir boş disk alanına sahip, kullanılabilir ilk NTFS biçimli disk sürücüsüne dosya yüklenir. Configuration Manager, belirli sürücülere yüklenmesini engellemek için, site sistemi sunucusunu yüklemeden önce, sürücünün kökünde **no_sms_on_drive. SMS** adlı boş bir dosya oluşturun.

Configuration Manager, rolleri yüklemek için **site sistemi yükleme hesabını** kullanır. Rolü yüklerken bu hesabı belirtirsiniz. Varsayılan olarak, bu hesap, site sunucusu bilgisayarının yerel sistem hesabıdır. Site sistemi yükleme hesabı olarak bir etki alanı kullanıcı hesabı belirtebilirsiniz. Daha fazla bilgi için bkz. [hesaplar-site sistemi yükleme hesabı](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Var olan bir site sistemi sunucusuna roller yükler

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin. Yeni site sistem rollerini yüklemek istediğiniz var olan site sistem sunucusunu seçin.

1. Şeritte, **giriş** sekmesinde, **sunucu** grubunda, **site sistemi rolleri ekle**' yi seçin.

1. **Genel** sayfasında, ayarları gözden geçirin.

    > [!TIP]
    >  Site sistemi rolüne internet 'ten erişmek için, bir Internet tam etki alanı adı (FQDN) belirttiğinizden emin olun.

1. **Proxy** sayfasında, bu sunucudaki roller bir internet proxy 'si gerektiriyorsa, proxy sunucusu için ayarları belirtin. Daha fazla bilgi için bkz. [proxy sunucu desteği](../../../plan-design/network/proxy-server-support.md).

1. **Sistem rolü seçimi** sayfasında, eklemek istediğiniz site sistem rollerini seçin.

1. Sihirbazı tamamlayın. Belirli roller için ek sayfalar görünebilir. Daha fazla bilgi için bkz. [site sistemi rolleri Için yapılandırma seçenekleri](configuration-options-for-site-system-roles.md).

> [!TIP]
> **New-CMSiteSystemServer**Windows PowerShell cmdlet 'i Bu yordamla aynı işlevi gerçekleştirir. Daha fazla bilgi için bkz. [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Yeni bir site sistemi sunucusuna roller yükler

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin.

1. Şeritte, **giriş** sekmesinde, **Oluştur** grubunda, **site sistemi sunucusu oluştur**' u seçin.

1. **Genel** sayfasında, site sistemi için genel ayarları belirtin.

    > [!TIP]
    > Yeni site sistemi rolüne internet 'ten erişmek için bir Internet FQDN 'SI belirttiğinizden emin olun.

1. **Proxy** sayfasında, bu sunucudaki roller bir internet proxy 'si gerektiriyorsa, proxy sunucusu için ayarları belirtin. Daha fazla bilgi için bkz. [proxy sunucu desteği](../../../plan-design/network/proxy-server-support.md).

1. **Sistem rolü seçimi** sayfasında, eklemek istediğiniz site sistem rollerini seçin.

1. Sihirbazı tamamlayın. Belirli roller için ek sayfalar görünebilir. Daha fazla bilgi için bkz. [site sistemi rolleri Için yapılandırma seçenekleri](configuration-options-for-site-system-roles.md).

> [!TIP]
> **New-CMSiteSystemServer**Windows PowerShell cmdlet 'i Bu yordamla aynı işlevi gerçekleştirir. Daha fazla bilgi için bkz. [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="next-steps"></a>Sonraki adımlar

- [Site sistemi rolleri için yapılandırma seçenekleri](configuration-options-for-site-system-roles.md)

- [Rolü kaldır](../install/uninstall-sites-and-hierarchies.md#bkmk_role)