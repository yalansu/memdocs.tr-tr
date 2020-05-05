---
title: Site bileşenleri
titleSuffix: Configuration Manager
description: Site sistem rolleri ve site durumu raporlama davranışını değiştirmek için site bileşenlerini nasıl yapılandıracağınızı öğrenin.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718332"
---
# <a name="site-components-for-configuration-manager"></a>Configuration Manager için site bileşenleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Her bir Configuration Manager sitesi için site sistemi rolleri ve site durumu raporlama davranışını değiştirmek üzere site bileşenlerini yapılandırabilirsiniz. Site bileşeni yapılandırması bir site için ve sitedeki geçerli bir site sistem rolünün her örneği için geçerlidir.  

Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Bir site seçin. Şeridin **Ayarlar** grubunda **site bileşenlerini Yapılandır**' ı seçin. Aşağıdaki seçeneklerden birini belirtin:

- [Yazılım dağıtımı](#software-distribution)  
- [Yazılım güncelleştirme noktası](#software-update-point) 
- [İşletim sistemi dağıtımı](#operating-system-deployment)
- [Yönetim noktası](#management-point)  
- [Durum bildirimi](#status-reporting)  
- [E-posta bildirimi](#email-notification)
- [Koleksiyon üyeliği değerlendirmesi](#bkmk_colleval)


## <a name="about-site-components"></a>Site bileşenleri hakkında  

 Çeşitli site bileşenlerine yönelik birçok seçenek, Configuration Manager konsolunda görüntülendiklerinde kendi kendine açıklayıcıdır. Ancak, aşağıdaki Ayrıntılar daha karmaşık yapılandırmaların bazılarını açıklamaya yardımcı olabilir veya sizi ek içeriğe yönlendirebilir.  

> [!Note]  
> Bazı bileşenler için kullanılabilen seçenekler, merkezi yönetim sitesini, birincil siteyi veya ikincil bir siteyi seçip seçmeyeceğinizi farklılık gösterir. Bazı bileşenler belirli site türleri için kullanılamaz.  



### <a name="software-distribution"></a>Yazılım dağıtımı  

#### <a name="content-distribution-settings"></a>İçerik dağıtım ayarları
**Genel** sekmesinde, site sunucusunun içeriği dağıtım noktalarına nasıl aktardığından emin olan ayarları belirtin. Eşzamanlı dağıtım ayarları için kullandığınız değerleri artırdığınızda, içerik dağıtımı daha fazla ağ bant genişliği kullanabilir.  

#### <a name="pull-distribution-point"></a>Çekme dağıtım noktası
Daha fazla bilgi için bkz. [çekme dağıtım noktası kullanma](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

#### <a name="network-access-account"></a>Ağ erişim hesabı
Daha fazla bilgi için bkz. [ağ erişim hesabı](../../../plan-design/hierarchy/accounts.md#network-access-account).  


### <a name="software-update-point"></a>Yazılım güncelleştirme noktası  

Daha fazla bilgi için bkz. [yazılım güncelleştirme noktası yüklemesi](../../../../sum/get-started/install-a-software-update-point.md).  


### <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı

Daha fazla bilgi için bkz. [çevrimdışı işletim sistemi görüntüsü bakımı için sürücüyü belirtme](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive).


### <a name="management-point"></a>Yönetim noktası  

**Genel** sekmesinde, Active Directory Domain Services için yönetim noktaları hakkında bilgi yayımlamak üzere siteyi ayarlayın.  

Configuration Manager istemcileri hizmetleri bulmak ve sınır grubu üyeliği ve PKI sertifikası seçme seçenekleri gibi site bilgilerini bulmak için yönetim noktalarını kullanır. İstemciler ayrıca, sitedeki diğer yönetim noktalarını bulmak için yönetim noktalarını ve yazılımın indirileceği dağıtım noktalarını da kullanır. Yönetim noktaları Ayrıca istemcilerin site atamasını tamamlamasını ve istemci ilkesini indirmesini ve istemci bilgilerini karşıya yüklemeyi sağlar.  

İstemcilerin yönetim noktalarını bulması için en güvenli yöntem, Active Directory Domain Services içinde yayımlamaktır. Bu hizmet konumu yöntemi, aşağıdakilerin doğru olmasını gerektirir:

- Şema Configuration Manager için genişletilir.
- Site sunucusunun bu kapsayıcıya yayımlaması için uygun güvenlik izinlerine sahip bir **sistem yönetimi** kapsayıcısı vardır.
- Configuration Manager site, Active Directory Domain Services yayımlanacak şekilde ayarlanır.
- İstemciler, site sunucusunun ormanıyla aynı Active Directory ormanına aittir.  

İntranetteki istemciler yönetim noktalarını bulmak için Active Directory Domain Services kullanbulamadığında [DNS yayımlaması](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns)' nı kullanın.  

Hizmet konumu hakkında genel bilgi için bkz. [İstemcilerin site kaynaklarını ve hizmetleri nasıl bulduklarını anlama](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Seçili intranet yönetim noktalarını DNS 'de Yayımla
İntranetteki istemciler Active Directory Domain Services yönetim noktalarını bulamadığında bu seçeneği belirtin. Bunun yerine, atanmış sitelerinde bir yönetim noktası bulmak için bir DNS hizmeti konum kaynak kaydı (SRV RR) kullanabilirler.  

İntranet yönetim noktalarını DNS 'ye yayımlamak için Configuration Manager için aşağıdaki koşulların tümü sağlanmalıdır:  

-   DNS sunucularınızda BIND 8.1.2 veya üzeri bir sürümün olması.  

-   DNS sunucularınız otomatik güncelleştirmeler için ayarlanır ve hizmet konumu kaynak kayıtlarını destekler.  

-   Configuration Manager içindeki yönetim noktaları için belirtilen tam etki alanı adları (FQDN), DNS 'de konak girişlerine (A veya AAA kayıtları) sahiptir.  

> [!WARNING]  
>  İstemcilerin DNS 'de yayınlanan yönetim noktalarını bulması için, istemcileri belirli bir siteye atamanız gerekir (otomatik site atamasını kullanmak yerine). Site kodunu, yönetim noktalarının etki alanı sonekiyle birlikte kullanmak için bu istemcileri ayarlayın. Daha fazla bilgi için bkz. [yönetim noktalarını bulma](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points).  

Configuration Manager istemciler intranet üzerindeki yönetim noktalarını bulmak için Active Directory Domain Services veya DNS kullanamazlar, [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins)kullanırlar. Site için yüklenen ilk yönetim noktası, intranet üzerindeki HTTP istemci bağlantılarını kabul etmek üzere ayarlandığında WINS 'e otomatik olarak yayımlanır.  


### <a name="status-reporting"></a>Durum bildirimi  

Bu ayarlar, siteler ve istemcilerden gelen durum raporlarına dahil edilen ayrıntı düzeyini doğrudan ayarlar.  


### <a name="email-notification"></a>E-posta ile bildirim  

Configuration Manager uyarılar için e-posta bildirimleri göndermesini sağlamak üzere hesap ve e-posta sunucusu ayrıntılarını belirtin.  

Daha fazla bilgi için bkz. [uyarıları ve durum sistemini kullanma](../../manage/use-alerts-and-the-status-system.md).


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a>Koleksiyon üyeliği değerlendirmesi  

Koleksiyon üyeliğinin artımlı olarak ne sıklıkta değerlendirildiğini ayarlamak için bu bileşeni kullanın. Artımlı değerlendirme, bir koleksiyon üyeliğini yalnızca yeni veya değiştirilmiş kaynaklarla güncelleştirir.  

Daha fazla bilgi için bkz. [koleksiyonlar Için en iyi uygulamalar](../../../clients/manage/collections/best-practices-for-collections.md).



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Configuration Manager Service Manager kullanarak site bileşenlerini yönetme  

Configuration Manager hizmetlerini denetlemek ve herhangi bir Configuration Manager hizmetinin veya çalışan iş parçacığının durumunu görüntülemek için Configuration Manager Service Manager kullanabilirsiniz. Bu hizmetler ve iş parçacıkları topluca Configuration Manager bileşenleri olarak adlandırılır. Configuration Manager bileşenleri hakkında aşağıdaki deyimleri anlayın:  

-   Bileşenler, herhangi bir site sisteminde çalışabilir.  

-   Bileşenler Windows 'taki Hizmetleri yönettiğiniz şekilde yönetilir. Configuration Manager bileşenlerini başlatabilir, durdurabilir, duraklatabilir, sürdürebilir veya sorgulayabilirsiniz.  

Bir Configuration Manager hizmeti, kendisi için bir şey olduğunda çalışır. Bu eylem, genellikle bir yapılandırma dosyası bir bileşenin gelen kutusuna yazıldığında olur. 


### <a name="use-the-configuration-manager-service-manager"></a>Configuration Manager kullanın Service Manager  

1.  Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **sistem durumu**' nu genişletin ve **Bileşen durumu** düğümünü seçin.  

2.  Şeridin **bileşen** grubunda **Başlat**' ı ve ardından **Configuration Manager Service Manager**' yı seçin.  

3.  Configuration Manager Service Manager açıldığında yönetmek istediğiniz siteye bağlanın.  

     Yönetmek istediğiniz siteyi görmüyorsanız, **site** menüsüne gidin ve **Bağlan**' ı seçin. Ardından doğru sitenin site sunucusunun adını girin.  

4.  Siteyi genişletin ve yönetmek istediğiniz bileşenlerin bulunduğu yere göre **Bileşenler** veya **sunucular**' a gidin.  

5.  Sağ bölmede bir veya daha fazla bileşen seçin. Ardından, **bileşen** menüsünde, seçiminizin durumunu güncelleştirmek için **sorgu** ' yı seçin.  

6.  Bileşenin durumu güncelleştirildikten sonra bileşenin işlemini değiştirmek için **bileşen** menüsündeki dört eylem tabanlı seçenekten birini kullanın. Bir eylem istedikten sonra bileşenin yeni durumunu göstermek için bileşeni sorgulamanız gerekir.  

7.  Bileşenlerin işletimsel durumunu değiştirmeyi tamamladığınızda Configuration Manager Service Manager kapatın.  
