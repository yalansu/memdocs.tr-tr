---
title: Windows özellikleri için destek
titleSuffix: Configuration Manager
description: Configuration Manager hangi Windows ve ağ özelliklerinin desteklediğini öğrenin.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4f9266668a488b6331857bf860d874a48161fcd0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700223"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Configuration Manager 'da Windows özellikleri ve ağları için destek

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, yaygın Windows ve ağ özellikleri için Configuration Manager desteği tanımlanmaktadır.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  

Dağıtım noktalarında etkin hale geldiğinde Configuration Manager Windows BranchCache kullanın ve istemcileri dağıtılmış önbellek modunda kullanacak şekilde yapılandırın.

Uygulamalar için dağıtım türündeki BranchCache ayarlarını, bir paket için dağıtımda ve görev dizileri için yapılandırın. Sürüm 1802 ' den başlayarak BranchCache varsayılan olarak etkindir.

BranchCache için gereksinimler karşılandığında, bu özellik uzak konumlardaki istemcilerin, içeriğin geçerli bir önbelleğine sahip olan yerel istemcilerden içerik almasına olanak sağlar.  

Örneğin, ilk BranchCache etkin istemci, BranchCache sunucusu olarak yapılandırılmış bir dağıtım noktasından içerik istediğinde, istemci içeriği indirir ve önbelleğe alır. Bu içerik daha sonra bu içeriği isteyen aynı alt ağdaki istemciler için kullanılabilir hale getirilir.

Bu istemciler de içeriği önbelleğe alarak. Aynı alt ağdaki diğer istemciler, dağıtım noktasından içerik indirmek zorunda kalmaz. İçerik, gelecekteki aktarımlar için birden fazla istemciye dağıtılır.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Configuration Manager ile BranchCache destekleme gereksinimleri

#### <a name="configure-distribution-points"></a>Dağıtım noktalarını yapılandırma

**Windows BranchCache** özelliğini, dağıtım noktası olarak yapılandırılan site sistemi sunucusuna ekleyin.

- BranchCache 'i destekleyecek şekilde yapılandırılan sunuculardaki dağıtım noktaları, ek yapılandırma gerektirmez.
- Windows BranchCache 'i bulut tabanlı bir dağıtım noktasına ekleyemezsiniz. Bulut tabanlı dağıtım noktaları, Windows BranchCache için yapılandırılan istemciler tarafından içerik indirilmesini destekler.  

#### <a name="configure-clients"></a>İstemcileri yapılandırma

- BranchCache 'i destekleyebilen istemcilerin BranchCache dağıtılmış önbellek modu için yapılandırılmış olması gerekir.  
- BranchCache 'i desteklemek için BITS istemci ayarları için işletim sistemi ayarı etkinleştirilmelidir.  

Bilgi için bkz. Windows belgelerindeki [Istemcileri BranchCache için yapılandırma](/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) .

Desteklenen Configuration Manager tüm Windows sürümleri, varsayılan olarak BranchCache ' i destekler.

Daha fazla bilgi için Windows Server belgelerindeki [Windows Için BranchCache](/windows-server/networking/branchcache/branchcache) konusuna bakın.  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Çalışma gruplarındaki bilgisayarlar  

Configuration Manager, çalışma gruplarındaki istemciler için destek sağlar.  

- Configuration Manager, bir istemcinin çalışma grubundan etki alanına veya etki alanından bir çalışma grubuna taşınmasını destekler. Daha fazla bilgi için bkz. [Configuration Manager istemcileri çalışma grubu bilgisayarlarına nasıl yüklenir](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]
> Çalışma gruplarındaki istemciler desteklense de, tüm site sistemleri desteklenen bir Active Directory etki alanının üyesi olmalıdır.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a> Yinelenen verileri kaldırma

Configuration Manager, Windows Server 2012 veya üzeri sürümlerde dağıtım noktalarıyla yinelenen verileri kaldırma özelliğinin kullanımını destekler.

> [!IMPORTANT]  
> Paket kaynak dosyalarını barındıran birim yinelenen verileri kaldırma için işaretlenemez. Bu sınırlama, yinelenen verileri kaldırma işleminin yeniden ayrıştırma noktalarını kullanması nedeniyle oluşur. Configuration Manager, yeniden ayrıştırma noktalarında depolanan dosyalarla içerik kaynak konumu kullanımını desteklemez.  

Daha fazla bilgi için aşağıdaki gönderilere bakın:

- Configuration Manager ekibi blogda [dağıtım noktaları ve Windows Server 2012 yinelenen verileri kaldırma Configuration Manager](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385)

- Windows Server belgelerinde [yinelenen verileri kaldırma 'ya genel bakış](/windows-server/storage/data-deduplication/overview)

## <a name="directaccess"></a><a name="bkmk_DA"></a> 'In  

Configuration Manager istemciler ve site sunucusu sistemleri arasındaki iletişim için DirectAccess özelliğini destekler.  

- DirectAccess 'in tüm gereksinimleri karşılandığında, Internet 'teki Configuration Manager istemcilerinin, intranette oldukları gibi, kendilerine atanan siteleri ile iletişim kurmasına olanak sağlar.  

- Uzaktan denetim ve client push yüklemesi gibi sunucu tarafından başlatılan eylemler için, başlatan bilgisayar IPv6 çalıştırıyor olmalıdır. Bu protokol, tüm aradaki ağ cihazlarında desteklenmelidir.  

Configuration Manager, DirectAccess üzerinde aşağıdaki işlevleri desteklemez:  

- İşletim sistemi dağıtımı

- Configuration Manager siteleri arasındaki iletişim  

- Site içindeki Configuration Manager site sistem sunucuları arasındaki iletişim  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a> Çift önyükleme bilgisayarları  

Configuration Manager, tek bir bilgisayarda birden fazla işletim sistemini yönetemez. Yönetmek üzere bir bilgisayarda birden fazla işletim sistemi varsa, Configuration Manager istemcisinin yalnızca yönetilmesi gereken işletim sistemine yüklendiğinden emin olmak için sitenin bulma ve istemci yükleme yöntemlerini ayarlayın.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a> IPv6  

Internet Protokolü sürüm 4 ' ün (IPv4) yanı sıra, Configuration Manager aşağıdaki özel durumlarla birlikte Internet Protokolü sürüm 6 ' yı (IPv6) destekler:  

|İşlev| IPv6 desteği için özel durum|  
|--------------|-------------------------------|  
|Bulut tabanlı dağıtım noktaları|Microsoft Azure ve bulut tabanlı dağıtım noktalarının desteklenmesi için IPv4 gereklidir.|  
|Bulut yönetimi ağ geçidi|Microsoft Azure ve bulut yönetimi ağ geçidini desteklemek için IPv4 gereklidir.|  
|Microsoft Intune ve Microsoft Hizmet Bağlayıcısı tarafından kaydedilen mobil cihazlar|Microsoft Intune ve Microsoft Hizmet Bağlayıcısı tarafından kaydedilen mobil cihazların desteklenmesi için IPv4 gereklidir.|  
|Ağ Bulma|Ağ Bulma’da arama yapmak üzere bir DHCP sunucusu yapılandırmak için IPv4 gereklidir.|  
|İşletim sistemi dağıtımı|Sürüm 1802 ve önceki sürümlerinde, işletim sistemi dağıtımını desteklemek için IPv4 gereklidir.  </br> </br> Sürüm 1806 ' den başlayarak, Windows dağıtım hizmeti olmadan bir dağıtım noktasındaki PXE Yanıtlayıcı 'yı etkinleştirin. Bu yeni PXE Yanıtlayıcı hizmeti IPv6 'Yı destekler. Görev sırası sırasında statik IP adreslerini yakalama veya ayarlama gibi işletim sistemi dağıtımı özelliğinin diğer yönleri, IPv4 gerektirmeye devam eder. |  
|Uyandırma ara sunucusu iletişimi|İstemci uyandırma proxy’si paketlerinin desteklenmesi için IPv4 gereklidir.|  
|Windows CE|Windows CE cihazlarda Configuration Manager istemcisini desteklemek için IPv4 gereklidir.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a> Ağ adresi çevirisi  

Site Internet 'te olan istemcileri desteklemediği ve istemci internet 'e bağlı olduğunu algıladığı müddetçe, ağ adresi çevirisi (NAT) Configuration Manager desteklenmez. Internet tabanlı istemci yönetimi hakkında daha fazla bilgi için bkz. [Internet tabanlı istemcileri yönetmeyi planlayın](../../clients/manage/plan-internet-based-client-management.md).  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a> Özel depolama teknolojisi  

Configuration Manager, Configuration Manager bileşeninin yüklü olduğu işletim sistemi sürümü için Windows Donanım uyumluluğu listesi 'nde sertifikalanmış tüm donanımlarla birlikte kullanılabilir.

Site sunucusu rolleri, Configuration Manager dizin ve dosya izinlerini ayarlayabilmesi için NTFS gerektirir. Configuration Manager, mantıksal bir sürücünün sahip olduğu varsayılmaktadır. Ayrı bilgisayarlarda çalışan site sistemleri herhangi bir depolama teknolojisinden mantıksal bir bölümü paylaşamaz. Ancak her bilgisayar, paylaşılan depolama cihazının aynı fiziksel bölümünde ayrı bir mantıksal bölüm kullanabilir.  

### <a name="support-considerations"></a>Destek konuları

- **Depolama alanı ağı**: desteklenen bir Windows tabanlı sunucu, San tarafından barındırılan birime doğrudan eklendiği zaman bir depolama alanı ağı (San) desteklenir.  

- **Tek örnekli depolama**: Configuration Manager tek örnekli depolama (SIS) özellikli bir birimde dağıtım noktası paketinin ve imza klasörlerinin yapılandırılmasını desteklemez.  

     Ayrıca, bir Configuration Manager istemcisinin önbelleği SIS özellikli bir birimde desteklenmez.  

- **Çıkarılabilir disk sürücüsü**: Configuration Manager çıkarılabilir disk sürücüsüne Configuration Manager site sistemlerinin veya istemcilerinin yüklenmesini desteklemez.