---
title: Hizmet bağlantı noktası
titleSuffix: Configuration Manager
description: Bu Configuration Manager site sistem rolü hakkında bilgi edinin ve bunların kullanım aralığını anlayın ve planlayın.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721188"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Configuration Manager hizmet bağlantı noktası hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hizmet bağlantı noktası, hiyerarşi için birkaç önemli işlev sağlayan bir site sistem rolüdür. Hizmet bağlantı noktasını ayarlamadan önce, kullanım aralığını anlayın ve planlayın. Kullanım planlaması, bu site sistemi rolünü ayarlamayı etkileyebilir:

- Configuration Manager altyapınıza uygulanan güncelleştirmeleri indirin. Yalnızca altyapınız için ilgili güncelleştirmeler karşıya yüklediğiniz kullanım verilerine göre kullanılabilir hale getirilir.

- Configuration Manager altyapınızdan kullanım verilerini karşıya yükleyin. Karşıya yüklediğiniz ayrıntı düzeyini veya miktarını kontrol edebilirsiniz. Daha fazla bilgi için bkz. [kullanım veri düzeyleri ve ayarları](../install/setup-reference.md#bkmk_usage).

- Azure 'da bir [bulut yönetimi ağ geçidi](../../../clients/manage/cmg/plan-cloud-management-gateway.md) dağıtma

- [İş ve eğitim için Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) uygulamaları eşitler

- [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc) içinde kullanıcıları ve grupları bulma

- Windows 10 güncelleştirme ve uygulama hazırlığı hakkında öngörüler edinmek için [Masaüstü Analizi](../../../../desktop-analytics/overview.md) 'ni kullanma

Her hiyerarşi bu rolün tek bir örneğini destekler. Yalnızca hiyerarşinizin bir merkezi yönetim sitesi (CAS) veya tek başına birincil site olan üst katman sitesine yüklenebilir. Bağımsız bir birincil siteyi daha büyük bir hiyerarşiye genişletirseniz, bu rolü birincil siteden kaldırın ve ardından CA 'lardan yükleme yapın.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a>İşlem modları

Hizmet bağlantı noktası iki çalışma modunu destekler:

- **Çevrimiçi**: hizmet bağlantı noktası güncelleştirmeleri her 24 saatte bir otomatik olarak denetler. Geçerli altyapınız ve ürün sürümünüz için mevcut olan yeni güncelleştirmeleri, Configuration Manager konsolunda kullanılabilir hale getirmek üzere indirir.

- **Çevrimdışı**: hizmet bağlantı noktası Microsoft bulut hizmetine bağlanmıyor. Kullanılabilir güncelleştirmeleri el ile içeri aktarmak için [hizmet bağlantı aracını](../../manage/use-the-service-connection-tool.md)kullanın.

### <a name="change-mode"></a>Modu Değiştir

Hizmet bağlantı noktasını yükledikten sonra çevrimiçi veya çevrimdışı modlar arasında geçiş yaparsanız, SMS_Executive hizmetinin **SMS_DMP_DOWNLOADER** iş parçacığını yeniden başlatın. Bu iş parçacığını yeniden başlatmak, değişikliğin geçerli hale gelmesini sağlar. Bu iş parçacığını yeniden başlatmak için Configuration Manager Service Manager kullanın.

> [!TIP]
> Ayrıca, çoğu site bileşenini yeniden başlatan Configuration Manager için SMS_Executive hizmetini yeniden başlatabilirsiniz. Alternatif olarak, SMS_Executive hizmeti durdurup yeniden başlatan bir site yedeklemesi gibi zamanlanmış bir görevi bekleyin.

SMS_DMP_DOWNLOADER iş parçacığını yeniden başlatmak için Configuration Manager Service Manager kullanmak için:

1. Configuration Manager konsolunda **izleme** çalışma alanına gidin, **sistem durumu**' nu genişletin ve **Bileşen durumu** düğümünü seçin. Şeritte **Başlat**' ı seçin ve ardından **Configuration Manager Service Manager**' yı seçin.

1. Service Manager gezinti bölmesinde, siteyi genişletin, **Bileşenler**' i genişletin ve sonra yeniden başlatmak istediğiniz bileşeni seçin: **SMS_DMP_DOWNLOADER**.

1. **Bileşen** menüsüne gidin ve **sorgu**' yı seçin.

1. Bileşenin geçerli durumunu onaylayın. Sonra **bileşen** menüsüne gidin ve **Durdur**' u seçin.  

1. Durdurulan olduğunu onaylamak için bileşeni tekrar **sorgulayın** . Sonra yeniden başlatmak için bileşen **Başlat** eylemini seçin.

## <a name="remote-site-system-requirements"></a>Uzak site sistem gereksinimleri

Hizmet bağlantı noktasını site sunucusundan uzak bir site sistem sunucusuna yüklediğinizde, aşağıdaki gereksinimleri yapılandırın:

- Site sunucusunun bilgisayar hesabı, uzak hizmet bağlantı noktasını barındıran bilgisayarda bir yerel yönetici olmalıdır.

- Bu rolü barındıran site sistemi sunucusunu bir [site sistemi yükleme hesabıyla](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)ayarlayın. Site sunucusundaki dağıtım Yöneticisi, güncelleştirmeleri hizmet bağlantı noktasından aktarmak için site sistemi yükleme hesabını kullanır.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a>Internet erişimi gereksinimleri

Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, hizmet bağlantı noktasının İnternet uç noktalarına erişmesine izin vermeniz gerekir.

Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../../plan-design/network/internet-endpoints.md#bkmk_scp).

## <a name="install"></a>Yükleme

Bir hiyerarşinin üst katman sitesini yüklemek için **Kurulum 'u** çalıştırdığınızda, hizmet bağlantı noktasını yükleyebilirsiniz.

Kurulum çalıştıktan sonra veya rolü yeniden yüklüyorsanız, **site sistemi rolleri ekleme** Sihirbazı ' nı veya **site sistemi sunucusu oluşturma** Sihirbazı ' nı kullanın. (Hizmet bağlantı noktasını yalnızca hiyerarşinizin üst katman sitesine yükler.) Daha fazla bilgi için bkz. [site sistemi rollerini yüklemeyi](install-site-system-roles.md).

## <a name="move-the-role"></a><a name="bkmk_move"></a>Rolü taşı

<!-- SCCMDocs#922 -->
Hizmet bağlantı noktasını başka bir sunucuya taşımanız gerekebilecek birkaç senaryo vardır:

- [Kurtarma](../../manage/recover-sites.md)
- [Site sunucusu yüksek kullanılabilirliği](site-server-high-availability.md)
- [Site genişletmesi](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Hizmet bağlantı noktasını taşıdıktan sonra tüm site işlevlerini kontrol edin. Örneğin, Azure Active Directory (Azure AD) kiracılarına yönelik bağlantıların gizli anahtarını yenilemeniz gerekebilir. Daha fazla bilgi için bkz. [gizli anahtarı yenileme](azure-services-wizard.md#bkmk_renew).

## <a name="log-files"></a>Günlük dosyaları

Microsoft 'a yükleme hakkında bilgi görüntülemek için, hizmet bağlantı noktasını çalıştıran sunucuda **Dmpuploader. log dosyasına** bakın. Güncelleştirmelerin İndirilme ilerlemesi için **DMPDownloader. log dosyasına**bakın. Hizmet bağlantı noktasıyla ilgili günlüklerin tam listesi için bkz. [günlük dosyaları-hizmet bağlantı noktası](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog).

## <a name="next-steps"></a>Sonraki adımlar

İşlem akışını ve anahtar günlüğü girdilerini anlamak için aşağıdaki akış çizelgeleriyle kullanın. Bu işlem, güncelleştirme indirmeleri ve diğer sitelere yapılan güncelleştirmelerin çoğaltılmasını içerir.

- [Akış Grafiği - Güncelleştirmeleri indir](../../manage/download-updates-flowchart.md)

- [Akış Çizelgesi - Çoğaltmayı güncelleştirme](../../manage/update-replication-flowchart.md)
