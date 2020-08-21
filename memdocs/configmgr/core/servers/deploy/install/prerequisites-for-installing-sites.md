---
title: Siteler için Önkoşullar
titleSuffix: Configuration Manager
description: Farklı türlerde Configuration Manager siteleri yüklemeye yönelik önkoşullar hakkında bilgi edinin.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bf9ad15266c4e6615ba100d5ea5270e23b93ece7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699135"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Configuration Manager siteleri yükleme önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir site yüklemesine başlamadan önce, farklı türlerde Configuration Manager siteleri yüklemeye yönelik önkoşullar hakkında bilgi edinin.


## <a name="primary-sites-and-the-central-administration-site"></a>Birincil siteler ve merkezi yönetim sitesi

Aşağıdaki önkoşullar aşağıdaki türlerden birini yüklemek için geçerlidir:

- Bir hiyerarşinin ilk sitesi olarak bir merkezi yönetim sitesi
- Tek başına birincil site
- Bir alt birincil site

Bir merkezi yönetim sitesini bir hiyerarşi genişletmesinin parçası olarak yüklüyorsanız, bkz. [tek başına birincil siteyi genişletme](#bkmk_expand).

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Birincil site veya merkezi yönetim sitesi yükleme önkoşulları  

- Gerekli Windows Server rolleri, özellikleri ve Windows bileşenleri yüklü olmalıdır. Daha fazla bilgi için bkz. [site sistemi önkoşulları](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq)  

- Siteyi yükleyen kullanıcı hesabı aşağıdaki haklara sahip olmalıdır:  

    - Aşağıdaki sunucularda **yönetici** :  
        - Site sunucusu  
        - **Site veritabanını** barındıran her sunucu  
        - Site için **SMS sağlayıcısı** 'nın her örneği  

    - Site veritabanını barındıran SQL Server örneğinde **sysadmin**  

        > [!IMPORTANT]  
        > Configuration Manager Kurulum tamamlandığında, site sunucusu bilgisayar hesabı, SQL Server için sysadmin haklarını korumalıdır. Bu hesaptan SQL sysadmin haklarını kaldırmayın.  

    > [!NOTE]
    > Kurulum tamamlandıktan sonra bu izinlerin ihtiyacı hakkında daha fazla bilgi için bkz. [yükseltilmiş izinler](../../../plan-design/hierarchy/accounts.md#elevated-permissions).

- Birincil site yüklüyorsanız, aşağıdaki ek haklara sahip olmanız gerekir:  

    - Site sunucusunda değilse, ilk yönetim noktasını ve dağıtım noktasını yüklediğiniz ek sunucularda **yönetici**  

- Bir merkezi yönetim sitesinin altına yeni bir alt birincil site yüklüyorsanız, aşağıdaki ek haklara sahip olmanız gerekir:  

    - Merkezi yönetim sitesini barındıran sunucuda **yönetici**  

    - Configuration Manager içinde, **Altyapı Yöneticisi** veya **tam yönetici** güvenlik rolüne eşdeğer rol tabanlı yönetim hakları  

- Doğru yükleme kaynak dosyalarını kullanın ve kurulum 'u bu konumdan çalıştırın. Farklı türlerde siteleri yüklemek için kullanılacak doğru kaynak dosyaları hakkında daha fazla bilgi için bkz. [farklı site türlerini yükleme seçenekleri](prepare-to-install-sites.md#bkmk_options).  

- Site sunucusunun, Microsoft 'tan güncelleştirilmiş Kurulum dosyalarına aşağıdaki yollarla erişimi olmalıdır:  

    - Yükleme işlemine başlamadan önce, bu dosyaların bir kopyasını yerel ağınıza indirip saklayın. Daha fazla bilgi için bkz. [Kurulum Yükleyici](setup-downloader.md).  

    - Bu dosyanın yerel bir kopyası yoksa, site sunucusunun İnternet erişimi olmalıdır. Yükleme sırasında bu dosyaları Microsoft 'tan indirir.  

- Site sunucusu ve site veritabanı sunucusu tüm önkoşul yapılandırmalarının yerine getirmelidir. Configuration Manager kurulumunu başlatmadan önce, sorunları belirlemek ve onarmak için [önkoşul denetleyicisi 'ni el ile çalıştırın](prerequisite-checker.md) .  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Tek başına birincil siteyi genişletme önkoşulları

Tek başına birincil site, merkezi yönetim sitesi olan bir hiyerarşiye genişletebilmeniz için aşağıdaki önkoşulları karşılamalıdır:

#### <a name="source-file-version-matches-site-version"></a>Kaynak dosya sürümü site sürümüyle eşleşiyor

Yeni Merkezi yönetim sitesini bir CD 'den medyayı kullanarak yükler. Tek başına birincil sitenin sürümü ile eşleşen en son klasör. Sürümlerin eşleştiğinden emin olmak için CD 'de bulunan kaynak dosyalarını kullanın [. ](../../manage/the-cd.latest-folder.md) Tek başına birincil sitede en son klasör.

Farklı siteleri yüklemek için kullanılacak doğru kaynak dosyaları hakkında daha fazla bilgi için bkz. [farklı site türlerini yükleme seçenekleri](prepare-to-install-sites.md#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Başka bir hiyerarşiden etkin geçişi durdur

Tek başına birincil siteyi başka bir Configuration Manager hiyerarşisinden veri geçirmek üzere yapılandıramazsınız. Diğer Configuration Manager hiyerarşilerinden tek başına birincil siteye etkin geçişi durdurun ve geçiş için tüm konfigürasyonları kaldırın. Bu yapılandırmalara şunlar dahildir:

- Tamamlanmamış geçiş işleri  
- Veri toplama  
- Etkin kaynak hiyerarşisinin yapılandırması  

Bu yapılandırma gereklidir çünkü Configuration Manager hiyerarşinin üst düzey sitesinden verileri geçirir. Bağımsız bir birincil siteyi genişlettiğinizde geçiş için yapılandırma merkezi yönetim sitesine aktarılmaz.  

Tek başına birincil siteyi genişlettikten sonra, birincil sitede geçişi yeniden yapılandırırsanız, merkezi yönetim sitesi geçiş işlemlerini gerçekleştirir.

Geçişin nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [geçiş için kaynak hiyerarşileri ve kaynak siteleri yapılandırma](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

#### <a name="computer-account-as-administrator"></a>Yönetici olarak bilgisayar hesabı

Yeni Merkezi yönetim sitesini barındıran sunucunun bilgisayar hesabı, tek başına birincil site sunucusunda **yönetici** grubunun bir üyesi olmalıdır.

Tek başına birincil siteyi başarılı bir şekilde genişletmek için, yeni merkezi yönetim sitesinin bilgisayar hesabı tek başına birincil sitede **yönetici** haklarına sahip olmalıdır. Bu yalnızca site genişletmesi sırasında gereklidir. Site genişletmesi tamamlandığında, hesabı birincil sitedeki Kullanıcı grubundan kaldırabilirsiniz.  

#### <a name="installation-account-permissions"></a>Yükleme hesabı izinleri

Yeni Merkezi yönetim sitesini yüklemek için Configuration Manager Kurulumu çalıştıran kullanıcı hesabı, tek başına birincil sitede rol tabanlı yönetim haklarına sahip olmalıdır.

Bir merkezi yönetim sitesini bir site genişletmesinin parçası olarak yüklemek için, merkezi yönetim sitesini yüklemek için Kurulumu çalıştıran kullanıcı hesabının, tek başına birincil sitede **tam yönetici** veya **Altyapı Yöneticisi**olarak rol tabanlı yönetimde tanımlanması gerekir.

Gerekli izinlerin tümünü içeren liste hakkında daha fazla bilgi için bkz. [site yükleme hesabı](../../../plan-design/hierarchy/accounts.md#site-installation-account).

#### <a name="top-level-site-roles"></a>Üst düzey site rolleri

Siteyi genişlettikten önce, tek başına birincil siteden aşağıdaki site sistem rollerini kaldırın:

- Varlık Yönetim Bilgileri eşitleme noktası  
- Uç Nokta Koruma noktası  
- Hizmet bağlantı noktası  

Configuration Manager, yalnızca hiyerarşinin en üst düzey sitesinde bu rolleri destekler. Tek başına birincil siteyi genişlettikten önce bu site sistem rollerini kaldırın. Siteyi genişlettikten sonra, merkezi yönetim sitesinde bu site sistem rollerini yeniden yükleyin.  

Diğer tüm site sistem rolleri birincil sitede yüklü kalabilir.  

#### <a name="open-the-sql-server-service-broker-port"></a>SQL Server Hizmet Aracısı bağlantı noktasını açın

Tek başına birincil site ile merkezi yönetim sitesinin sunucusu arasındaki SQL Server Hizmet Aracısı (SSB) için ağ bağlantı noktası açık olmalıdır.  

Bir merkezi yönetim sitesi ile birincil site arasında başarıyla veri çoğaltmak için Configuration Manager SSB 'nin kullanması için iki site arasında açık bir bağlantı noktası gerektirir. Bir merkezi yönetim sitesi yüklediğinizde ve tek başına bir birincil siteyi genişlettiğinizde, önkoşul denetimi SSB için belirttiğiniz bağlantı noktasının birincil sitede açık olduğunu doğrulamaz.  

#### <a name="known-issues-with-azure-services"></a>Azure hizmetleriyle ilgili bilinen sorunlar

Siteyi genişlettikten sonra, aşağıdaki Azure hizmetlerini Configuration Manager ile yeniden yapılandırmanız gerekir:

- [Log Analytics](/azure/azure-monitor/platform/collect-sccm)  
- [Iş için Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Bulut yönetimi ağ geçidi](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

En kolay yöntem Azure Active Directory kiracı gizli anahtarını yenilemeyecektir. Daha fazla bilgi için bkz. [gizli anahtarı yenileme](../configure/azure-services-wizard.md#bkmk_renew).

Alternatif olarak, bu hizmete bağlantıyı kaldırıp yeniden oluşturun:

1. Configuration Manager konsolunda Azure hizmetini **Azure hizmetleri** düğümünden silin.  

2. Azure portal, hizmetle ilişkili kiracıyı Azure Active Directory kiracılar düğümünden silin. Bu eylem ayrıca hizmetle ilişkili Azure AD Web uygulamasını da siler.  

3. Configuration Manager ile kullanmak üzere Azure hizmetine bağlantıyı yeniden yapılandırın.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a> İkincil siteler

İkincil siteleri yüklemek için Önkoşullar aşağıda verilmiştir:  

- Gerekli Windows Server rolleri, özellikleri ve Windows bileşenleri yüklü olmalıdır. Daha fazla bilgi için bkz. [site sistemi önkoşulları](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq)  

- Configuration Manager konsolundaki ikincil sitenin yüklemesini yapılandıran yöneticinin, **Altyapı Yöneticisi** veya **tam yönetici**güvenlik rolüyle eşdeğer rol tabanlı yönetim haklarına sahip olması gerekir.  

- Üst birincil sitenin bilgisayar hesabı, ikincil site sunucusunda bir **yönetici** olmalıdır.  

- İkincil site, ikincil site veritabanını barındırmak için SQL Server önceden yüklenmiş bir örneğini kullandığında:  

    - Üst birincil sitenin bilgisayar hesabı, ikincil site sunucusundaki SQL Server örneğinde **sysadmin** haklarına sahip olmalıdır.  

    - İkincil site sunucusu bilgisayarının **yerel sistem** hesabı, ikincil site sunucusundaki SQL Server örneğinde **sysadmin** haklarına sahip olmalıdır.  

        > [!IMPORTANT]  
        > Configuration Manager Kurulum tamamlandığında, her iki hesap da SQL Server için sysadmin haklarını korumalıdır. Sysadmin haklarını bu hesaplardan kaldırmayın.  

- İkincil site sunucusu tüm önkoşul yapılandırmalarının yerine gelmelidir. Bu yapılandırma SQL Server ve yönetim noktası ve dağıtım noktasının varsayılan site sistem rollerini içerir.  


## <a name="next-steps"></a>Sonraki adımlar

Önkoşulları onayladıktan sonra kurulum 'u çalıştırmaya hazırsınız demektir. Daha fazla bilgi için bkz. [Configuration Manager siteleri yüklemek Için Kurulum Sihirbazı 'Nı kullanma](use-the-setup-wizard-to-install-sites.md).