---
title: Yazılım Merkezini planlama
titleSuffix: Configuration Manager
description: Kullanıcıların Configuration Manager etkileşimde bulunmak için yazılım merkezi 'ni nasıl yapılandırmak ve marka eklemek istediğinize karar verin.
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 802dbaa4188199e555a5cc0143ed599ad454e27e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695180"
---
# <a name="plan-for-software-center"></a>Yazılım Merkezini planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kullanıcılar ayarları değiştirebilir, uygulamalara gözatabilir ve yazılım merkezi 'nden uygulama yükler. Configuration Manager istemcisini bir Windows cihazına yüklediğinizde, yazılım merkezi de otomatik olarak yüklenir.

Yazılım Merkezi 'nin diğer özellikleri hakkında daha fazla bilgi için bkz. [Software Center Kullanıcı Kılavuzu](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Yazılım merkezini yapılandırma  

Yazılım Merkezi 'nin en son özelliklerinden yararlanmak için Configuration Manager sitelerinizi ve istemcilerinizi sürüm 1906 veya sonraki bir sürüme güncelleştirin.

> [!IMPORTANT]
> Yazılım Merkezi ve yönetim noktası için bu yinelemeli geliştirmeler, uygulama kataloğu rollerinin devre dışı bırakılması.
>
> - Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez.
> - Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz.
> - Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.

- **Bilgisayar Aracısı** grubundaki **yeni yazılım merkezini kullan** istemci ayarı varsayılan olarak etkindir. Yazılım Merkezi 'nin önceki sürümü artık desteklenmiyor. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

- Yazılım Merkezi 'nin **yükleme durumu** sekmesinde Uygulama Kataloğu web sitesi bağlantısının görünürlüğünü belirtin. Daha fazla bilgi için bkz. [Software Center](../../core/clients/deploy/about-client-settings.md#software-center) istemci ayarları.

- Sürüm 1906 ' den başlayarak, yazılım merkezi 'ne beş adede kadar özel sekme ekleyebilirsiniz. Daha fazla bilgi için bkz. [Software Center istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

- Kullanıcılar, yazılım merkezi 'nde Kullanıcı cihaz benzeşimini yapılandırabilir. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

- Sürüm 2006 ' den başlayarak, birlikte yönetilen cihazları hem Intune hem de Configuration Manager uygulamalar için Şirket Portalı kullanacak şekilde yapılandırabilirsiniz. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](../../comanage/company-portal.md).<!--CMADO-3601237,INADO-4297660-->

> [!IMPORTANT]
> Yeni Configuration Manager özelliklerinden yararlanmak için önce istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

### <a name="software-center-and-user-available-applications"></a>Yazılım Merkezi ve Kullanıcı tarafından kullanılabilir uygulamalar

- Uygulama Kataloğu rollerinin, yazılım merkezi 'nde Kullanıcı tarafından kullanılabilen uygulamaları görüntülemesi gerekmez. Bu davranış, kullanıcılara uygulama sunmak için gereken sunucu altyapısını azaltmanıza yardımcı olur. Yazılım Merkezi, bu bilgileri almak için yönetim noktasına dayanır, bu da daha büyük ortamların [sınır gruplarına](../../core/servers/deploy/configure/boundary-groups.md#management-points)atayarak daha iyi ölçeklendirilmesine yardımcı olur.<!--1358309-->

- Kullanıcılar, Azure Active Directory (Azure AD) ile birleştirilmiş cihazlarda Kullanıcı tarafından kullanılabilen uygulamalara gözatıp yükleyebilir. Sürüm 2006 ' den başlayarak, internet tabanlı, etki alanına katılmış cihazlarda Kullanıcı tarafından kullanılabilir uygulamalar alabilirler. Daha fazla bilgi için bkz. [Kullanıcı tarafından kullanılabilen uygulamaları dağıtma](../deploy-use/deploy-applications.md#deploy-user-available-applications).

- Sürüm 1906 ' den başlayarak, yazılım merkezi kullanıcılara hedeflenen uygulamalar için bir yönetim noktasıyla iletişim kurar. Artık uygulama kataloğunu kullanmaz. Bu değişiklik, uygulama kataloğunu siteden kaldırmanızı kolaylaştırır.

- Daha önce yazılım merkezi, kullanılabilir sunucular listesinden ilk yönetim noktasını çekildi. Sürüm 1906 ' den başlayarak, istemcinin kullandığı yönetim noktasını kullanır. Bu değişiklik, yazılım merkezi 'nin istemci olarak atanan birincil siteden aynı yönetim noktasını kullanmasına olanak sağlar.

## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a> Bildirim bildirimlerini iletişim kutusu penceresiyle değiştirme

<!--3555947-->
Bazen kullanıcılar, bir yeniden başlatma veya gerekli dağıtım hakkındaki Windows bildirim bildirimini görmez. Ardından, anımsatıcıyı erteleme deneyimini görmez. Bu davranış, istemci son tarihe ulaştığında kötü bir kullanıcı deneyimine yol açabilir.

Sürüm 1902 ' den başlayarak, [yazılım değişiklikleri gerektiğinde](#software-changes-are-required) veya dağıtımların [yeniden başlatılması gerektiğinde](#restart-required), daha zorlayıcı bir iletişim kutusu penceresi kullanma seçeneğiniz vardır.

### <a name="software-changes-are-required"></a>Yazılım değişiklikleri gerekiyor

Gelecekte bir son tarihe kadar [bir uygulamayı dağıtırken](../deploy-use/deploy-applications.md) , Yazılım Dağıtma Sihirbazı 'Nın **Kullanıcı deneyimi** sayfasında, aşağıdaki Kullanıcı bildirimi seçeneklerini belirleyin:

- **Yazılım Merkezi 'nde görüntüle ve tüm bildirimleri göster**
- **Yazılım değişiklikleri gerektiğinde kullanıcıya bildirim yerine bir iletişim kutusu penceresi gösterin**

Bu dağıtım ayarı yapılandırıldığında, bu senaryonun Kullanıcı deneyimi değişir.

Aşağıdaki bildirim:

![Yazılım değişikliklerinin gerekli olduğunu bildirme](media/3555947-required-toast.png)  

Aşağıdaki iletişim penceresine:

![Gerekli yazılım değişiklikleri için iletişim kutusu penceresi](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Yeniden başlatma gerekiyor

[Bilgisayar yeniden başlatma](../../core/clients/deploy/about-client-settings.md#computer-restart) istemci ayarları grubunda, aşağıdaki seçeneği etkinleştirin: **bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin**.  

Bu istemci ayarı yapılandırıldığında, aşağıdaki türlerin yeniden başlatılmasını gerektiren tüm gerekli dağıtımlar için Kullanıcı deneyimi değişir:

- [Uygulama](../deploy-use/deploy-applications.md)
- [Görev dizisi](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Yazılım güncelleştirmesi](../../sum/deploy-use/deploy-software-updates.md)

Aşağıdaki bildirim:

![Yeniden başlatmanın gerekli bildirimi](media/3555947-restart-toast.png)  

Aşağıdaki iletişim penceresine:

![Bilgisayarınızı yeniden başlatmak için iletişim kutusu penceresi](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> Configuration Manager 1902 ' de, bazı durumlarda iletişim kutusu bildirim bildirimlerini değiştirmez. Bu sorunu çözmek için [Configuration Manager sürüm 1902 için güncelleştirme paketini](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)yükledikten sonra. <!--4404715-->

## <a name="brand-software-center"></a>Marka yazılım merkezi

Yazılım Merkezi 'nin görünümünü kuruluşunuzun marka gereksinimlerini karşılayacak şekilde değiştirin. Bu yapılandırma, kullanıcıların yazılım merkezine güvenmesine yardımcı olur.

### <a name="configure-software-center-branding"></a>Software Center markasını yapılandırma

<!-- 1351224 -->
Kuruluşunuzun marka öğelerini ekleyerek ve sekmelerin görünürlüğünü belirterek yazılım merkezi 'nin görünümünü özelleştirin.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- İstemci ayarları [Yazılım Merkezi](../../core/clients/deploy/about-client-settings.md#software-center) grubu  
- [İstemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Marka öncelikleri

Configuration Manager, yazılım merkezi için aşağıdaki önceliklere göre özel marka uygular:  

1. **Yazılım Merkezi** istemci ayarları. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#software-center).  

2. **Bilgisayar Aracısı** grubundaki **kuruluş adı** istemci ayarı. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#computer-agent).  

#### <a name="application-catalog-branding-priorities"></a>Uygulama Kataloğu markalama öncelikleri

> [!IMPORTANT]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  

Uygulama Kataloğu kullanıyorsanız, marka şu öncelikleri izler:  

1. **Yazılım Merkezi** istemci ayarları. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#software-center).  

2. Uygulama Kataloğu web sitesi noktası özelliklerinde belirttiğiniz *kuruluş adı* ve *rengi* . Daha fazla bilgi için bkz. [Uygulama Kataloğu web sitesi noktası Için yapılandırma seçenekleri](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).  

3. **Bilgisayar Aracısı** grubundaki **kuruluş adı** istemci ayarı. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#computer-agent).  

## <a name="see-also"></a>Ayrıca bkz.

- [Yazılım Merkezi kullanıcı kılavuzu](../../core/understand/software-center.md)

- [Uygulama yönetimini planlama ve yapılandırma](plan-for-and-configure-application-management.md)

- [Ortak yönetilen cihazlarda Şirket Portalı uygulamasını kullanma](../../comanage/company-portal.md)
