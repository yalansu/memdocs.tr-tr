---
title: Proxy sunucu desteği
titleSuffix: Configuration Manager
description: Configuration Manager site sistem sunucularının proxy sunucularını nasıl kullandığını öğrenin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5581214dd786bdefd29d0e4d2626de536ad26ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718717"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Configuration Manager 'de proxy sunucu desteği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bazı Configuration Manager site sistemi sunucuları Internet bağlantısı gerektirir. Ortamınız bir ara sunucu kullanmak için internet trafiği gerektiriyorsa, bu site sistem rollerini proxy kullanmak üzere yapılandırın.  

- Site sistemi sunucusunu barındıran bir bilgisayar, tek bir proxy sunucusu yapılandırmasını destekler. Bu bilgisayardaki tüm site sistem rolleri aynı ara sunucu yapılandırmasını paylaşır. Farklı roller veya bir rolün örnekleri için ayrı proxy sunucuları gerekirse, bu rolleri ayrı site sistemi sunucularına yerleştirin.  

- Zaten bir ara sunucu yapılandırması olan bir site sistemi sunucusu için yeni proxy sunucu ayarlarını yapılandırdığınızda özgün yapılandırmanın üzerine yazılır.  

- Varsayılan olarak, ara sunucu bağlantıları, site sistemi rolünü barındıran bilgisayarın **sistem** hesabını kullanır.  

- Bilgisayar hesabının kimliği doğrulanamadıysanız, site sistem sunucusu proxy sunucusuna bağlanmak için Kullanıcı kimlik bilgilerini saklayabilir. Bu kimlik bilgileri, **site sistemi proxy sunucu hesabıdır**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Proxy kullanan site sistem rolleri

Aşağıdaki site sistem rolleri internet 'e bağlanır ve gerekirse bir ara sunucu kullanabilir:  

### <a name="asset-intelligence-synchronization-point"></a>Varlık Yönetim Bilgileri eşitleme noktası

Bu site sistem rolü Microsoft 'a bağlanır ve Varlık Yönetim Bilgileri eşitleme noktasını barındıran bilgisayarda bir proxy sunucu yapılandırması kullanır.  

### <a name="cloud-distribution-point"></a>Bulut dağıtım noktası

Bulut dağıtım noktası rolü Microsoft Azure ' de çalışır. Bu site sistem rolünü bir ara sunucu kullanacak şekilde yapılandırmayın. Bulut dağıtım noktasını yöneten birincil site sunucusunda ara sunucu yapılandırmasını ayarlayın.  

Bu yapılandırma için birincil site sunucusu:  

- İçerik ayarlamak, izlemek ve bulut dağıtım noktasına dağıtmak için Microsoft Azure bağlanabilmelidir.  

- Varsayılan olarak, bağlantıyı kurmak için bilgisayarın **sistem** hesabını kullanır. Ayrıca, gerekirse, site sistemi proxy sunucusu hesabını da kullanabilir.  

- Windows Web tarayıcısı API 'Lerini kullanır.  

### <a name="distribution-point"></a>Dağıtım noktası

<!-- 5856396 -->

Sürüm 2002 ' den başlayarak, Microsoft bağlı önbelleği için bir Configuration Manager dağıtım noktası etkinleştirirseniz, internet erişimi için kimliği doğrulanmamış bir ara sunucu üzerinden iletişim kurabilir. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği](../hierarchy/microsoft-connected-cache.md).

### <a name="exchange-server-connector"></a>Exchange Server bağlayıcısı

Bu site sistemi rolü bir Exchange sunucusuna bağlanır. Exchange Server bağlayıcısını barındıran bilgisayarda bir proxy sunucu yapılandırması kullanır.  

### <a name="service-connection-point"></a>Hizmet bağlantı noktası

Bu site sistemi rolü, Configuration Manager sürüm güncelleştirmelerini indirmek için Configuration Manager bulut hizmetine bağlanır. Hizmet bağlantı noktasını barındıran bilgisayarda yapılandırılmış bir ara sunucu kullanır.  

### <a name="software-update-point"></a>Yazılım güncelleştirme noktası

Bu site sistem rolü, düzeltme eklerini indirmek ve güncelleştirmelerle ilgili bilgileri eşleştirmek için Microsoft Update bağlandığı zaman proxy 'yi kullanır. Diğer tüm site sistem rolleri gibi, önce site sistemi ara sunucu ayarlarını yapılandırın. Ardından, yazılım güncelleştirme noktasına özgü aşağıdaki seçenekleri yapılandırın:  

- **Yazılım güncelleştirmelerini eşitlerken proxy sunucusu kullan**  

- **Otomatik dağıtım kuralları kullanarak içerik indirirken proxy sunucu kullan**  

    > [!NOTE]
    > Bu ayar kullanıma hazır olsa da, ikincil sitelerdeki yazılım güncelleştirme noktaları tarafından kullanılmaz.  

Bu ayarlar, yazılım güncelleştirme noktası özellikleri 'nin **proxy ve hesap ayarları** sekmesindedir.  

> [!NOTE]
> Varsayılan olarak, otomatik dağıtım kuralları çalıştırıldığında, internet 'e bağlanmak ve yazılım güncelleştirmelerini indirmek için otomatik dağıtım kuralının oluşturulduğu sitenin site sunucusundaki **sistem** hesabı kullanılır. Alternatif olarak, site sistemi proxy sunucusu hesabını yapılandırın ve kullanın. 
>
> Bu hesap internet 'e erişemeyebilir, yazılım güncelleştirmeleri indirilemez. **RuleEngine. log**dosyasına aşağıdaki giriş kaydedilir:  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a>Bir site sistemi sunucusu için proxy kullanan diğer özellikler

*(Sürüm 2002 ' de tanıtılmıştır)*

Configuration Manager sürüm 2002 ' den başlayarak, aşağıdaki özellikler [hizmet bağlantı noktası](#service-connection-point) rolünü barındıran site sisteminin ara sunucusunu kullanır: <!--5913817-->

- [Azure Active Directory (Azure AD) Kullanıcı keşfi](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Azure AD Kullanıcı grubu bulma](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Koleksiyon üyeliği sonuçlarını Azure Active Directory gruplarıyla eşitleme](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>Bir site sistemi sunucusu için proxy 'yi yapılandırma  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve ardından **sunucular ve site sistemi rolleri** düğümünü seçin.  

2. Düzenlemek istediğiniz site sistem sunucusunu seçin. Ayrıntılar bölmesinde, **site sistemi** rolüne sağ tıklayın ve **Özellikler**' i seçin.  

3. Site Sistem Özellikleri ' nde **proxy** sekmesine geçin. aşağıdaki proxy ayarlarını yapılandırın:  

    - **İnternet 'ten bilgi eşitlerken proxy sunucusu kullan**: site sistem sunucusunun bir ara sunucu kullanmasını sağlamak için bu seçeneği belirleyin.  

    - **Proxy sunucu adı**: ortamınızda proxy sunucusunun ana bilgisayar adını veya FQDN 'sini belirtin.  

    - **Bağlantı noktası**: ara sunucu ile iletişim kurmak için kullanılacak ağ bağlantı noktasını belirtin. Varsayılan olarak **80**numaralı bağlantı noktasını kullanır.  

    - **Proxy sunucusuna bağlanmak için kimlik bilgilerini kullan**: birçok proxy sunucusu, bir kullanıcının kimlik doğrulamasını gerektirir. Varsayılan olarak, site sistem sunucusu, proxy sunucusuna bağlanmak için bilgisayar hesabını kullanır. Gerekirse, bu seçeneği etkinleştirin, **Ayarla**' yı tıklatın ve ardından mevcut bir **hesabı** seçin veya yeni bir **Hesap**belirtin. Bu kimlik bilgileri, **site sistemi proxy sunucu hesabıdır**.  Daha fazla bilgi için bkz. [Configuration Manager kullanılan hesaplar](../hierarchy/accounts.md).  

4. Yeni proxy sunucusu yapılandırmasını kaydetmek için **Tamam ' ı** seçin.  
