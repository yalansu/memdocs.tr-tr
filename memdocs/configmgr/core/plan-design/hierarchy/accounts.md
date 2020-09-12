---
title: Kullanılan hesaplar
titleSuffix: Configuration Manager
description: Configuration Manager ' de kullanılan Windows gruplarını, hesaplarını ve SQL nesnelerini tanımlayabilir ve yönetin.
ms.date: 05/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fff07351725e6606a49804bba79f226a9042c349
ms.sourcegitcommit: f575b13789185d3ac1f7038f0729596348a3cf14
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2020
ms.locfileid: "90039355"
---
# <a name="accounts-used-in-configuration-manager"></a>Configuration Manager kullanılan hesaplar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, kullanıldıkları ve tüm gereksinimlerin kullanıldığı Windows gruplarını, hesaplarını ve SQL nesnelerini belirlemek için aşağıdaki bilgileri kullanın.  

- [Configuration Manager’ın oluşturduğu ve kullandığı Windows grupları](#bkmk_groups)  
  - [Yapılandırma Manager_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [Yapılandırma Manager_DViewAccess](#configmgr_dviewaccess)  
  - [Uzaktan denetim kullanıcılarını Configuration Manager](#configmgr_rcusers)  
  - [SMS Yöneticileri](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_ &lt; sitekodu\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; sitekodu\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_ &lt; sitekodu\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_ &lt; sitekodu\>](#bkmk_filerepl)  

- [Configuration Manager'ın kullandığı hesaplar](#bkmk_accounts)
  - [Active Directory grubu bulma hesabı](#active-directory-group-discovery-account)  
  - [Active Directory sistem bulma hesabı](#active-directory-system-discovery-account)  
  - [Kullanıcı keşfi hesabını Active Directory](#active-directory-user-discovery-account)  
  - [Active Directory orman hesabı](#active-directory-forest-account)  
  - [Sertifika kayıt noktası hesabı](#certificate-registration-point-account)  
  - [İşletim sistemi görüntüsü hesabı yakala](#capture-os-image-account)  
  - [Client Push yükleme hesabı](#client-push-installation-account)  
  - [Kayıt noktası bağlantı hesabı](#enrollment-point-connection-account)  
  - [Exchange Server bağlantı hesabı](#exchange-server-connection-account)  
  - [Yönetim noktası bağlantı hesabı](#management-point-connection-account)  
  - [Çok noktaya yayın bağlantı hesabı](#multicast-connection-account)  
  - [Ağ erişim hesabı](#network-access-account)  
  - [Paket erişim hesabı](#package-access-account)  
  - [Raporlama Hizmetleri noktası hesabı](#reporting-services-point-account)  
  - [Uzak araçlara izin verilen Görüntüleyici hesapları](#remote-tools-permitted-viewer-accounts)  
  - [Site yükleme hesabı](#site-installation-account)
  - [Site sistemi yükleme hesabı](#site-system-installation-account)  
  - [Site sistemi proxy sunucusu hesabı](#site-system-proxy-server-account)  
  - [SMTP sunucusu bağlantı hesabı](#smtp-server-connection-account)  
  - [Yazılım güncelleştirme noktası bağlantı hesabı](#software-update-point-connection-account)  
  - [Kaynak site hesabı](#source-site-account)  
  - [Kaynak site veritabanı hesabı](#source-site-database-account)  
  - [Görev sırası etki alanına katılacak hesap](#task-sequence-domain-join-account)  
  - [Görev dizisi ağ klasörü bağlantı hesabı](#task-sequence-network-folder-connection-account)  
  - [Görev sırası farklı çalıştır hesabı](#task-sequence-run-as-account)  

- [Configuration Manager SQL 'de kullanan kullanıcı nesneleri](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Configuration Manager SQL 'de kullanan veritabanı rolleri](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Configuration Manager oluşturduğu ve kullandığı Windows grupları  

Configuration Manager otomatik olarak oluşturulur ve birçok durumda aşağıdaki Windows gruplarını otomatik olarak korur:  

> [!NOTE]  
> Configuration Manager, etki alanı üyesi olan bir bilgisayarda bir grup oluşturduğunda, Grup bir yerel güvenlik grubudur. Bilgisayar bir etki alanı denetleyicisiyse, Grup bir etki alanı yerel grubudur. Bu grup türü, etki alanındaki tüm etki alanı denetleyicileri arasında paylaşılır.  


### <a name="configuration-manager_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> Yapılandırma Manager_CollectedFilesAccess

Configuration Manager, yazılım envanteri tarafından toplanan dosyaları görüntülemeye erişim vermek için bu grubu kullanır.  

Daha fazla bilgi için bkz. [yazılım envanterine giriş](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, birincil site sunucusunda oluşturulan yerel bir güvenlik grubudur.

Bir siteyi kaldırdığınızda, bu grup otomatik olarak kaldırılmaz. Bir siteyi kaldırdıktan sonra el ile silin.

#### <a name="membership"></a>Üyelik
Configuration Manager, Grup üyeliğini otomatik olarak yönetir. Üyelik, atanmış bir güvenlik rolünden **Koleksiyon** güvenliği sağlanabilir nesnesine **Toplanan Dosyaları Görüntüleme** izni verilen yönetici kullanıcıları içerir.

#### <a name="permissions"></a>İzinler
Varsayılan olarak, bu grubun site sunucusundaki şu klasörde **okuma** izni vardır: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configuration-manager_dviewaccess"></a><a name="configmgr_dviewaccess"></a>Yapılandırma Manager_DViewAccess  

Bu grup, bir alt birincil sitenin site veritabanı sunucusunda veya veritabanı çoğaltma sunucusunda Configuration Manager oluşturduğu bir yerel güvenlik grubudur. Site, bir hiyerarşideki siteler arasında veritabanı çoğaltması için dağıtılmış görünümleri kullandığınızda onu oluşturur. Bu, merkezi yönetim sitesinin site sunucusunu ve SQL Server bilgisayar hesaplarını içerir.

Daha fazla bilgi için bkz. [siteler arasındaki veri aktarımları](data-transfers-between-sites.md).


### <a name="configuration-manager-remote-control-users"></a><a name="configmgr_rcusers"></a> Uzaktan denetim kullanıcılarını Configuration Manager  

Configuration Manager uzak Araçlar, **Izin verilen görüntüleyiciler** listesinde ayarladığınız hesapları ve grupları depolamak için bu grubu kullanır. Site bu listeyi her bir istemciye atar.  

Daha fazla bilgi için bkz. [uzaktan denetime giriş](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, istemci uzak araçlara izin veren bir ilke aldığında Configuration Manager istemcisinde oluşturulan yerel bir güvenlik grubudur.

Bir istemci için uzak araçları devre dışı bıraktıktan sonra, bu grup otomatik olarak kaldırılmaz. Uzak araçları devre dışı bıraktıktan sonra el ile silin.

#### <a name="membership"></a>Üyelik
Varsayılan olarak, bu grupta bir üye yoktur. **Izin verilen görüntüleyiciler** listesine kullanıcılar eklediğinizde, bunlar otomatik olarak bu gruba eklenir.

Kullanıcıları veya grupları doğrudan bu gruba eklemek yerine, bu grubun üyeliğini yönetmek için **Izin verilen görüntüleyiciler** listesini kullanın.

Bir yönetim kullanıcısının, izin verilen bir Görüntüleyici olmanın yanı sıra, **koleksiyon** nesnesi Için **uzak denetim** iznine sahip olması gerekir. Bu izni, **Uzak Araçlar işleci** güvenlik rolünü kullanarak atayın.  

#### <a name="permissions"></a>İzinler
Varsayılan olarak, bu grubun bilgisayardaki herhangi bir konuma izni yoktur. Yalnızca **Izin verilen görüntüleyiciler** listesini tutmak için kullanılır.  


### <a name="sms-admins"></a>SMS Yöneticileri  

Configuration Manager, WMI aracılığıyla SMS Sağlayıcısına erişim vermek için bu grubu kullanır. Configuration Manager konsolundaki nesneleri görüntülemek ve değiştirmek için SMS Sağlayıcısına erişim gerekir.  

> [!NOTE]  
> Bir yönetim kullanıcısının rol tabanlı yönetim yapılandırması, Configuration Manager konsolunu kullanırken hangi nesneleri görüntüleyebileceklerini ve yönetebileceklerini belirler.  

Daha fazla bilgi için bkz. [plan for SMS Provider](plan-for-the-sms-provider.md).

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, SMS sağlayıcısı olan her bilgisayarda oluşturulan yerel bir güvenlik grubudur. 

Bir siteyi kaldırdığınızda, bu grup otomatik olarak kaldırılmaz. Bir siteyi kaldırdıktan sonra el ile silin.

#### <a name="membership"></a>Üyelik
Configuration Manager, Grup üyeliğini otomatik olarak yönetir. Varsayılan olarak, bir hiyerarşideki ve site sunucusu bilgisayar hesabındaki her yönetici kullanıcı, bir sitedeki her bir SMS sağlayıcısı bilgisayarında **SMS yöneticileri** grubunun üyesidir.

#### <a name="permissions"></a>İzinler
SMS yöneticileri grubu için hakları ve izinleri **WMI denetimi** MMC ek bileşeninde görüntüleyebilirsiniz. Varsayılan olarak, bu gruba WMI ad alanında **hesabı etkinleştir** ve **Uzaktan Etkinleştir** izni verilir `Root\SMS` . Kimliği doğrulanmış kullanıcıların **çalıştırma yöntemleri**, **sağlayıcı yazma**ve **etkinleştirme hesabı**vardır.

Uzak bir Configuration Manager konsolu kullandığınızda, hem site sunucusu bilgisayarında hem de SMS sağlayıcısında **Uzaktan etkinleştirme** DCOM izinlerini yapılandırın. Bu hakları **SMS yöneticileri** grubuna verin. Bu eylem, bu hakları doğrudan kullanıcılara veya gruplara vermek yerine yönetimi basitleştirir. Daha fazla bilgi için bkz. [uzaktan Configuration Manager konsolları IÇIN DCOM Izinlerini yapılandırma](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_ &lt; sitekodu\>  
 
Site sunucusundan uzakta olan yönetim noktaları, site veritabanına bağlanmak için bu grubu kullanır. Bu grup, site sunucusunda ve site veritabanındaki gelen kutusu klasörlerine bir yönetim noktası erişimi sağlar.  

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, SMS sağlayıcısı olan her bilgisayarda oluşturulan yerel bir güvenlik grubudur.

Bir siteyi kaldırdığınızda, bu grup otomatik olarak kaldırılmaz. Bir siteyi kaldırdıktan sonra el ile silin.

#### <a name="membership"></a>Üyelik
Configuration Manager, Grup üyeliğini otomatik olarak yönetir. Varsayılan olarak, üyelik, site için bir yönetim noktasına sahip uzak bilgisayarların bilgisayar hesaplarını içerir.

#### <a name="permissions"></a>İzinler
Varsayılan olarak, bu grubun site sunucusundaki şu klasörde **okuma**, **okuma & yürütme**ve **klasör içeriğini listeleme** izni vardır: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Bu grup, yönetim noktasının istemci verilerini yazdığı **gelen kutularındaki**alt klasörlere **yazma** ek iznine sahiptir.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; sitekodu\>  
 
Uzak SMS sağlayıcısı bilgisayarları, site sunucusuna bağlanmak için bu grubu kullanır.  

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, site sunucusunda oluşturulan yerel bir güvenlik grubudur.

Bir siteyi kaldırdığınızda, bu grup otomatik olarak kaldırılmaz. Bir siteyi kaldırdıktan sonra el ile silin.

#### <a name="membership"></a>Üyelik
Configuration Manager, Grup üyeliğini otomatik olarak yönetir. Varsayılan olarak, üyelik bilgisayar hesabı veya bir etki alanı kullanıcı hesabı içerir. Her bir uzak SMS sağlayıcısından site sunucusuna bağlanmak için bu hesabı kullanır.

#### <a name="permissions"></a>İzinler
Varsayılan olarak, bu grubun site sunucusundaki şu klasörde **okuma**, **okuma & yürütme**ve **klasör içeriğini listeleme** izni vardır: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Bu grup, gelen kutularının altındaki alt klasörlere **yazma** ve **değiştirme** ek izinlerine sahiptir. SMS sağlayıcısının bu klasörlere erişmesi gerekir.

Bu grubun Ayrıca, aşağıdaki site sunucusundaki alt klasörlerde **okuma** izni vardır `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` . 

Ayrıca aşağıdaki alt klasörler için aşağıdaki izinlere sahiptir `C:\Program Files\Microsoft Configuration Manager\OSD\boot` :
- **Okuyamaz**  
- **& yürütmeyi oku**  
- **Klasör içeriğini Listele**  
- **Yazarken**  
- **Değiştir**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_ &lt; sitekodu\>  

Configuration Manager uzak site sistem bilgisayarları üzerindeki dosya gönderme Yöneticisi bileşeni, site sunucusuna bağlanmak için bu grubu kullanır.  

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, site sunucusunda oluşturulan yerel bir güvenlik grubudur.

Bir siteyi kaldırdığınızda, bu grup otomatik olarak kaldırılmaz. Bir siteyi kaldırdıktan sonra el ile silin.

#### <a name="membership"></a>Üyelik
Configuration Manager, Grup üyeliğini otomatik olarak yönetir. Varsayılan olarak, üyelik bilgisayar hesabını veya etki alanı kullanıcı hesabını içerir. Dosya gönderme Yöneticisi 'ni çalıştıran her bir uzak site sisteminden site sunucusuna bağlanmak için bu hesabı kullanır.

#### <a name="permissions"></a>İzinler
Varsayılan olarak, bu grubun site sunucusundaki şu klasörde ve alt klasörlerinde **okuma**, **okuma & yürütme**ve **klasör içeriğini listeleme** izni vardır: `C:\Program Files\Microsoft Configuration Manager\inboxes` . 

Bu grup, site sunucusunda aşağıdaki klasöre **yazma** ve **değiştirme** ek izinlerine sahiptir: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box` .


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_ &lt; sitekodu\>  
Configuration Manager, bir hiyerarşideki siteler arasında dosya tabanlı çoğaltmayı etkinleştirmek için bu grubu kullanır. Bu siteye doğrudan dosya aktaran her bir uzak site için, bu grubun bir **dosya çoğaltma hesabı**olarak ayarlanmış hesapları vardır.  

#### <a name="type-and-location"></a>Tür ve konum
Bu grup, site sunucusunda oluşturulan yerel bir güvenlik grubudur.

#### <a name="membership"></a>Üyelik
Yeni bir siteyi başka bir sitenin alt öğesi olarak yüklediğinizde, Configuration Manager otomatik olarak yeni site sunucusunun bilgisayar hesabını üst site sunucusundaki bu gruba ekler. Configuration Manager ayrıca, ana sitenin bilgisayar hesabını yeni site sunucusundaki gruba ekler. Dosya tabanlı aktarımlar için başka bir hesap belirtirseniz, o hesabı hedef site sunucusunda bu gruba ekleyin.

Bir siteyi kaldırdığınızda, bu grup otomatik olarak kaldırılmaz. Bir siteyi kaldırdıktan sonra el ile silin.

#### <a name="permissions"></a>İzinler
Varsayılan olarak, bu grup aşağıdaki klasöre **tam denetime** sahiptir: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive` .



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Configuration Manager kullanılan hesaplar  

Configuration Manager için aşağıdaki hesapları ayarlayabilirsiniz.  

> [!TIP]
> `%`Configuration Manager konsolunda belirttiğiniz hesaplara ilişkin parolada yüzde karakterini () kullanmayın. Hesap kimlik doğrulaması başarısız olur.<!-- SCCMDocs#1032 -->

### <a name="active-directory-group-discovery-account"></a>Active Directory grubu bulma hesabı  

Site, belirttiğiniz Active Directory Domain Services konumlardan aşağıdaki nesneleri bulmak için **Active Directory grubu bulma hesabını** kullanır:
- Yerel, genel ve Evrensel güvenlik grupları
- Bu gruplar içindeki üyelik
- Dağıtım grupları içindeki üyelik
  - Dağıtım grupları, grup kaynakları olarak keşfedilmez

Bu hesap, bulmayı çalıştıran site sunucusunun bilgisayar hesabı ya da bir Windows kullanıcı hesabı olabilir. Bulma için belirttiğiniz Active Directory konumlarına **okuma** erişimi izni olması gerekir.  

Daha fazla bilgi için [Active Directory grubu bulma](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)bölümüne bakın.


### <a name="active-directory-system-discovery-account"></a>Active Directory sistem bulma hesabı  

Site, belirttiğiniz Active Directory Domain Services konumlardan bilgisayarları bulmak için **Active Directory sistem bulma hesabını** kullanır.  

Bu hesap, bulmayı çalıştıran site sunucusunun bilgisayar hesabı ya da bir Windows kullanıcı hesabı olabilir. Bulma için belirttiğiniz Active Directory konumlarına **okuma** erişimi izni olması gerekir.  

Daha fazla bilgi için bkz. [sistem keşfi Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Kullanıcı keşfi hesabını Active Directory  
 
Site, belirttiğiniz Active Directory Domain Services konumlardan Kullanıcı hesaplarını bulmak için **Active Directory Kullanıcı keşfi hesabını** kullanır.  

Bu hesap, bulmayı çalıştıran site sunucusunun bilgisayar hesabı ya da bir Windows kullanıcı hesabı olabilir. Bulma için belirttiğiniz Active Directory konumlarına **okuma** erişimi izni olması gerekir.  

Daha fazla bilgi için bkz. [Kullanıcı keşfi Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Active Directory orman hesabı  

Site, Active Directory ormanlarından ağ altyapısını saptamak için **Active Directory orman hesabını** kullanır. Merkezi yönetim siteleri ve birincil siteler, site verilerini bir orman için Active Directory Domain Services yayımlamak için de kullanır.  

> [!NOTE]  
> İkincil siteler, Active Directory'e yayımlamak için daima ikincil site sunucusu bilgisayar hesabını kullanır.  

Güvenilmeyen ormanları bulup yayımlamak için Active Directory orman hesabı bir genel hesap olmalıdır. Site sunucusunun bilgisayar hesabını kullanmıyorsanız, yalnızca genel bir hesap seçebilirsiniz.  

Bu hesabın, ağ altyapısını keşfetmek istediğiniz her bir Active Directory ormanına **Okuma** izinlerini bulunmalıdır.  

Bu hesabın, site verilerini yayımlamak istediğiniz her bir Active Directory ormanında **sistem yönetimi** kapsayıcısı ve tüm alt nesneleri Için **tam denetim** izinlerine sahip olması gerekir. Daha fazla bilgi için bkz. [site yayımlama için Active Directory hazırlama](../network/extend-the-active-directory-schema.md).  

Daha fazla bilgi için bkz. [Active Directory orman keşfi](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Sertifika kayıt noktası hesabı  

Sertifika kayıt noktası, Configuration Manager veritabanına bağlanmak için **sertifika kayıt noktası hesabını** kullanır. Varsayılan olarak bilgisayar hesabını kullanır, ancak bunun yerine bir kullanıcı hesabı yapılandırabilirsiniz. Sertifika kayıt noktası site sunucusundan güvenilir olmayan bir etki alanında olduğunda, bir kullanıcı hesabı belirtmeniz gerekir. Durum iletisi sistemi yazma görevlerini işlediği için bu hesabın yalnızca site veritabanına **okuma** erişimi olması gerekir.  

Daha fazla bilgi için bkz. [sertifika profillerine giriş](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>İşletim sistemi görüntüsü hesabı yakala  

Bir işletim sistemi görüntüsünü yakaladığınızda, Configuration Manager yakalanan görüntüleri depoladığınız klasöre erişmek için **işletim sistemi görüntüsünü yakala hesabını** kullanır. **İşletim sistemi görüntüsünü yakala** adımını bir görev dizisine eklerseniz, bu hesap gereklidir.  

Hesabın, yakalanan görüntüleri depoladığınız ağ paylaşımında **okuma** ve **yazma** izinlerine sahip olması gerekir.  

Windows 'da hesabın parolasını değiştirirseniz, görev dizisini yeni parolayla güncelleştirin. Configuration Manager istemcisi, bir sonraki istemci ilkesini indirdiğinde yeni parolayı alır.  

Bu hesabı kullanmanız gerekiyorsa, bir etki alanı kullanıcı hesabı oluşturun. Gerekli ağ kaynaklarına erişmek için en az izinleri verin ve tüm yakalama görev dizileri için bunu kullanın.  

> [!IMPORTANT]  
> Bu hesaba etkileşimli oturum açma izinleri atamayın.  
>   
> Bu hesap için ağ erişim hesabı kullanmayın.  

Daha fazla bilgi için bkz. bir [işletim sistemini yakalamak için görev dizisi oluşturma](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Client Push yükleme hesabı  

İstemcileri Client Push yükleme yöntemini kullanarak dağıttığınızda, site bilgisayarlara bağlanmak ve Configuration Manager istemci yazılımını yüklemek için **istemci anında yükleme hesabını** kullanır. Bu hesabı belirtmezseniz, site sunucusu bilgisayar hesabını kullanmayı dener.  

Bu hesap, hedef istemci bilgisayarlarındaki yerel **Yöneticiler** grubunun bir üyesi olmalıdır. Bu hesap, **etki alanı yönetici** hakları gerektirmez.  

Birden fazla istemci anında yükleme hesabı belirtebilirsiniz. Configuration Manager her birini, her biri başarılı olana kadar dener.  

> [!TIP]  
> Büyük bir Active Directory ortamınız varsa ve bu hesabı değiştirmeniz gerekiyorsa, bu hesap güncelleştirmesini daha etkin bir şekilde koordine etmek için aşağıdaki işlemi kullanın: 
> 1. Farklı bir ada sahip yeni bir hesap oluşturun   
> 2. Yeni hesabı Configuration Manager içindeki istemci anında yükleme hesapları listesine ekleyin  
> 3. Active Directory Domain Services yeni hesabı çoğaltması için yeterli zamana izin ver  
> 4. Ardından Configuration Manager eski hesabı kaldırın ve Active Directory Domain Services  

> [!IMPORTANT]  
> **Yerel olarak oturum açmaya izin**vermek üzere Windows kullanıcı hakkını atamak için etki alanı veya yerel Grup İlkesi kullanın. Yöneticiler grubunun bir üyesi olarak, bu hesap yerel olarak oturum açma hakkına sahip olur ve bu gerekli değildir. Daha iyi güvenlik için, bu hesabın hakkını açık olarak reddedin. Reddetme hakkı, izin verme hakkı 'nın yerini alır.<!--MEMDocs#744-->

Daha fazla bilgi için bkz. [Client Push yüklemesi](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Kayıt noktası bağlantı hesabı  

Kayıt noktası Configuration Manager site veritabanına bağlanmak için **kayıt noktası bağlantı hesabını** kullanır. Varsayılan olarak bilgisayar hesabını kullanır, ancak bunun yerine bir kullanıcı hesabı yapılandırabilirsiniz. Kayıt noktası site sunucusundan güvenilir olmayan bir etki alanında olduğunda, bir kullanıcı hesabı belirtmeniz gerekir. Bu hesap, site veritabanına **okuma** ve **yazma** erişimi gerektirir.  

Daha fazla bilgi için bkz. Şirket [ıçı MDM için site sistemi rolleri yüklemesi](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).


### <a name="exchange-server-connection-account"></a>Exchange Server bağlantı hesabı  

Site sunucusu, belirtilen Exchange Server 'a bağlanmak için **Exchange Server bağlantı hesabını** kullanır. Exchange Server 'a bağlanan mobil cihazları bulmak ve yönetmek için bu bağlantıyı kullanır. Bu hesap, Exchange Server bilgisayarına gerekli izinleri sağlayan Exchange PowerShell cmdlets gerektirir. Cmdlet 'ler hakkında daha fazla bilgi için bkz. [Exchange bağlayıcısını yükleyip yapılandırma](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Yönetim noktası bağlantı hesabı  

Yönetim noktası Configuration Manager site veritabanına bağlanmak için **Yönetim noktası bağlantı hesabını** kullanır. İstemciler için bilgi göndermek ve almak üzere bu bağlantıyı kullanır. Yönetim noktası varsayılan olarak bilgisayar hesabını kullanır, ancak bunun yerine bir kullanıcı hesabı yapılandırabilirsiniz. Yönetim noktası site sunucusundan güvenilir olmayan bir etki alanında olduğunda, bir kullanıcı hesabı belirtmeniz gerekir.  

Hesabı, Microsoft SQL Server çalıştıran bilgisayarda düşük haklara sahip yerel bir hesap olarak oluşturun.  

> [!IMPORTANT]  
> Bu hesaba etkileşimli oturum açma hakları vermeyin.  


### <a name="multicast-connection-account"></a>Çok noktaya yayın bağlantı hesabı  

Çok noktaya yayın özellikli dağıtım noktaları, site veritabanından bilgileri okumak için **çok noktaya yayın bağlantı hesabını** kullanır. Sunucu, varsayılan olarak bilgisayar hesabını kullanır, ancak bunun yerine bir kullanıcı hesabı yapılandırabilirsiniz. Site veritabanı güvenilmeyen bir ormanda olduğunda, bir kullanıcı hesabı belirtmeniz gerekir. Örneğin, veri merkezinizde, site sunucusu ve site veritabanı dışında bir ormanda bir çevre ağı varsa, bu hesabı site veritabanından çok noktaya yayın bilgilerini okumak için kullanın.  

Bu hesaba ihtiyacınız varsa, Microsoft SQL Server çalıştıran bilgisayarda düşük haklara sahip yerel bir hesap olarak oluşturun.  

> [!IMPORTANT]  
> Bu hesaba etkileşimli oturum açma hakları vermeyin.  

Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Ağ erişim hesabı  

İstemci bilgisayarları, dağıtım noktalarındaki içeriğe erişmek için yerel bilgisayar hesaplarını kullanamazlar, **ağ erişim hesabını** kullanır. Bu, genellikle güvenilmeyen etki alanlarından gelen çalışma grubu istemcileri ve bilgisayarları için geçerlidir. Bu hesap, işletim sistemini yükleyen bilgisayarda henüz etki alanında bir bilgisayar hesabı olmadığında, işletim sistemi dağıtımı sırasında da kullanılır.  

> [!Important]  
> Ağ erişim hesabı, programları çalıştırmak, yazılım güncelleştirmeleri yüklemek veya görev dizilerini çalıştırmak için güvenlik bağlamı olarak hiçbir şekilde kullanılmaz. Yalnızca ağdaki kaynaklara erişmek için kullanılır.  

Bir Configuration Manager istemci, ilk olarak içerik indirmek için bilgisayar hesabını kullanmayı dener. Başarısız olursa, ağ erişim hesabını otomatik olarak dener.  

Siteyi HTTPS veya [GELIŞMIŞ http](enhanced-http.md)için yapılandırırsanız, bir çalışma grubu veya Azure AD 'ye katılmış istemci, ağ erişim hesabına gerek olmadan dağıtım noktalarından içeriğe güvenli bir şekilde erişebilir. Bu davranış, önyükleme medyasından, PXE 'den veya yazılım merkezi 'nden çalışan bir görev sırası ile işletim sistemi dağıtım senaryolarını içerir.<!--1358228,1358278--> Daha fazla bilgi için bkz. [istemciden yönetim noktası iletişimi](communications-between-endpoints.md#bkmk_client2mp).<!-- SCCMDocs#1345 -->

> [!Note]  
> Ağ erişim hesabı gerektirmeyen **GELIŞMIŞ http** 'yi etkinleştirirseniz, dağıtım noktasının Windows Server 2012 veya sonraki bir sürümü çalıştırması gerekir. <!--SCCMDocs-pr issue #2696-->
>  
> Bu işlevselliği etkinleştirmeden önce istemcileri en az sürüm 1806 ' e yükseltin. Yalnızca **GELIŞMIŞ http** bağlantılarına izin verirseniz, eski istemciler bu yöntemi kullanarak kimlik doğrulaması yapamaz, bu nedenle istemci yükseltme paketini bir dağıtım noktasından indiremez. <!--vso2841213-->   

#### <a name="permissions"></a>İzinler

Bu hesaba, istemcinin yazılıma erişim gerektirdiği içeriğe uygun en az izini verin. Hesabın bu bilgisayara dağıtım noktasındaki **ağ üzerinden erişimi** olmalıdır. Site başına en fazla 10 ağ erişim hesabı yapılandırabilirsiniz.  

Hesabı, kaynaklara gerekli erişimi sağlayan herhangi bir etki alanında oluşturun. Ağ erişim hesabı her zaman bir etki alanı adı içermelidir. Bu hesap için doğrudan geçiş güvenliği desteklenmez. Birden çok etki alanında dağıtım noktalarınız varsa, hesabı güvenilir bir etki alanında oluşturun.  

> [!TIP]  
> Hesap kilitlenmelerini önlemek için, mevcut ağ erişim hesabında parolayı değiştirmeyin. Bunun yerine, yeni bir hesap oluşturun ve Configuration Manager yeni hesabı ayarlayın. Tüm istemcilerin yeni hesap ayrıntılarını alması için yeterli süre geçtiğinde, eski hesabı ağın paylaşılan klasörlerinden kaldırın ve hesabı silin.  

> [!IMPORTANT]  
> Bu hesaba etkileşimli oturum açma hakları vermeyin.  
>   
> Bu hesaba bilgisayarları etki alanına ekleme hakkı vermeyin. Bir görev dizisi sırasında bilgisayarları etki alanına katdıysanız, [görev sırası etki alanına ekleme hesabı](#task-sequence-domain-join-account)' nı kullanın.  

#### <a name="configure-the-network-access-account"></a>Ağ erişim hesabını yapılandırma  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Ardından siteyi seçin.  

2.  Şeridin **Ayarlar** grubunda **site bileşenlerini Yapılandır**' ı seçin ve **yazılım dağıtımı**' nı seçin.  

3.  **Ağ erişim hesabı** sekmesini seçin. Bir veya daha fazla hesap ayarlayın ve **Tamam**' ı seçin.  


### <a name="package-access-account"></a>Paket erişim hesabı  

Bir **paket erişim hesabı** , dağıtım noktalarında paket içeriğine erişebilen kullanıcıları ve Kullanıcı gruplarını BELIRTMEK için NTFS izinleri ayarlamanıza olanak sağlar. Varsayılan olarak, Configuration Manager yalnızca genel erişim hesapları **kullanıcısına** ve **yöneticisine**erişim izni verir. İstemci bilgisayarlara erişimi, ek Windows hesapları veya grupları kullanarak denetleyebilirsiniz. Mobil cihazlar paket içeriğini her zaman anonim olarak alır, bu nedenle bir paket erişim hesabı kullanmaz.  

Varsayılan olarak, Configuration Manager içerik dosyalarını bir dağıtım noktasına kopyaladığında, yerel **Kullanıcılar** grubuna **okuma** erişimi ve yerel **Yöneticiler** grubuna **tam denetim** izni verir. Gerekli olan gerçek izinler, pakete bağlıdır. Çalışma gruplarında veya güvenilmeyen ormanlarda istemcileriniz varsa, bu istemciler paket içeriğine erişmek için ağ erişim hesabını kullanırlar. Ağ erişim hesabının, tanımlı paket erişim hesaplarını kullanarak pakete yönelik izinlere sahip olduğundan emin olun.  

Bir etki alanındaki, dağıtım noktalarına erişebilen hesapları kullanın. Paketi oluşturduktan sonra hesabı oluşturur veya değiştirirseniz, paketi yeniden dağıtmanız gerekir. Paketin güncelleştirilmesi, paketteki NTFS izinlerini değiştirmez.  

Ağ erişim hesabını bir paket erişim hesabı olarak eklemeniz gerekmez, çünkü **Kullanıcılar** grubunun üyeliği onu otomatik olarak ekler. Paket erişim hesabını yalnızca ağ erişim hesabı olarak kısıtlamak, istemcilerin pakete erişmesini engellemez.  

#### <a name="manage-package-access-accounts"></a>Paket erişim hesaplarını yönetme  

1.  Configuration Manager konsolunda **yazılım kitaplığı**' nı seçin.  

2.  **Yazılım kitaplığı** çalışma alanında, erişim hesaplarını yönetmek istediğiniz içerik türünü saptayın ve belirtilen adımları izleyin:  

    - **Uygulama**: **uygulama yönetimi**' ni genişletin, **uygulamalar**' ı seçin ve ardından erişim hesaplarını yönetmek istediğiniz uygulamayı seçin.  

    - **Paket**: **uygulama yönetimi**' ni genişletin, **paketler**' i seçin ve ardından erişim hesaplarını yönetmek istediğiniz paketi seçin.  

    - **Yazılım güncelleştirme dağıtım paketi**: **yazılım güncelleştirmeleri**' ni genişletin, **dağıtım paketleri**' ni seçin ve ardından erişim hesaplarını yönetmek istediğiniz dağıtım paketini seçin.  

    - **Sürücü paketi**: **işletim sistemleri**' ni genişletin, **sürücü paketleri**' ni seçin ve ardından erişim hesaplarını yönetmek istediğiniz sürücü paketini seçin.  

    - İşletim sistemleri **görüntüsü**: **işletim sistemleri**' ni genişletin, **işletim sistemi görüntüleri**' ni seçin ve ardından erişim hesaplarını yönetmek istediğiniz işletim sistemi görüntüsünü seçin.  

    - İşletim sistemi **yükseltme paketi**: **işletim sistemleri**' ni genişletin, **işletim sistemi yükseltme paketleri**' ni seçin ve ardından erişim hesaplarını yönetmek istediğiniz işletim sistemi yükseltme paketini seçin.  

    - **Önyükleme görüntüsü**: **işletim sistemleri**' ni genişletin, **önyükleme görüntüleri**' ni seçin ve ardından erişim hesaplarını yönetmek istediğiniz önyükleme görüntüsünü seçin.  

3.  Seçili nesneye sağ tıklayın ve ardından **erişim hesaplarını yönet**' i seçin.  

4.  **Hesap Ekle** iletişim kutusunda, içeriğe erişim verilecek hesap türünü belirtin ve ardından hesapla ilişkili erişim haklarını belirtin.  

    > [!NOTE]  
    > Hesap için bir Kullanıcı adı eklediğinizde ve bu ada sahip bir yerel kullanıcı hesabı ve etki alanı kullanıcı hesabı Configuration Manager Configuration Manager, etki alanı kullanıcı hesabı için erişim haklarını ayarlar.  


### <a name="reporting-services-point-account"></a>Raporlama Hizmetleri noktası hesabı  
 
SQL Server Reporting Services, site veritabanından Configuration Manager raporların verilerini almak için **Raporlama Hizmetleri noktası hesabını** kullanır. Belirttiğiniz Windows kullanıcı hesabı ve parolası, SQL Server Raporlama Hizmetleri veritabanında şifrelenir ve depolanır.  

> [!NOTE]  
> Belirttiğiniz hesabın, SQL Raporlama Hizmetleri veritabanını barındıran bilgisayarda **yerel oturum** açma izinlerine sahip olması gerekir.

> [!NOTE]  
> Hesaba, Configuration Manager veritabanındaki smsschm_users SQL veritabanı rolüne eklendikten sonra tüm gerekli haklar otomatik olarak verilir.

Daha fazla bilgi için bkz. [raporlamaya giriş](../../servers/manage/introduction-to-reporting.md).


### <a name="remote-tools-permitted-viewer-accounts"></a>Uzak araçlara izin verilen Görüntüleyici hesapları  

Uzaktan denetim için **İzin Verilen Görüntüleyiciler** olarak belirttiğiniz hesaplar, istemcilerde uzak araçlar işlevselliğini kullanmasına izin verilen kullanıcıların bir listesidir.  

Daha fazla bilgi için bkz. [uzaktan denetime giriş](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Site yükleme hesabı
<!--SCCMDocs issue #572-->
Configuration Manager kurulumunu çalıştırdığınız sunucuda oturum açmak ve yeni bir site yüklemek için bir etki alanı kullanıcı hesabı kullanın.

Bu hesap için aşağıdaki haklar gereklidir:  

- Aşağıdaki sunucularda **yönetici** :
    - Site sunucusu  
    - Site veritabanını barındıran her sunucu  
    - Site için SMS sağlayıcısı 'nın her örneği  

- Site veritabanını barındıran SQL Server örneğinde **sysadmin**  

Configuration Manager Kurulum, bu hesabı otomatik olarak [SMS yöneticileri](#sms-admins) grubuna ekler.

Yükleme sonrasında, bu hesap Configuration Manager konsolu için haklara sahip tek kullanıcı olur. Bu hesabı kaldırmanız gerekiyorsa, önce başka bir kullanıcıya haklarını eklediğinizden emin olun.

Tek başına siteyi bir merkezi yönetim sitesi içerecek şekilde genişletirken, bu hesap tek başına birincil sitede **tam yönetici** veya **Altyapı Yöneticisi** rol tabanlı yönetim hakları gerektirir.


### <a name="site-system-installation-account"></a>Site sistemi yükleme hesabı  

Site sunucusu site sistemlerini yüklemek, yeniden yüklemek, kaldırmak ve ayarlamak için **site sistemi yükleme hesabını** kullanır. Site sistemini site sunucusunun bu site sistemine yönelik bağlantıları başlatmasını gerektirecek şekilde ayarlarsanız, Configuration Manager, site sistemini ve tüm rolleri yükledikten sonra site sisteminden veri çekmek için de bu hesabı kullanır. Her site sisteminde farklı bir yükleme hesabı bulunabilir, ancak o site sistemindeki tüm rolleri yönetmek için yalnızca bir yükleme hesabı ayarlayabilirsiniz.  

Bu hesabın hedef site sistemlerinde yerel yönetim izinleri olması gerekir. Ayrıca, bu hesabın hedef site sistemlerindeki güvenlik ilkesinde **Bu bilgisayara ağ üzerinden erişmesi** gerekir.  

> [!TIP]  
> Birçok etki alanı denetleyiciniz varsa ve bu hesaplar etki alanları genelinde kullanılıyorsa, site sistemini ayarlamadan önce Active Directory bu hesapları çoğaltmış olduğunu denetleyin.  
>   
> Yönetilecek her site sisteminde bir yerel hesap belirttiğinizde, bu yapılandırma etki alanı hesaplarının kullanılmasıyla daha güvenlidir. Hesap tehlikeye girerse, saldırganların yapabilirler. Ancak, etki alanı hesaplarının yönetilmesi daha kolaydır. Güvenlik ve etkili yönetim arasındaki dengelemeyi göz önünde bulundurun.  


### <a name="site-system-proxy-server-account"></a>Site sistemi proxy sunucusu hesabı
<!--SCCMDocs issue #648-->
Aşağıdaki site sistem rolleri, kimlik doğrulamalı erişim gerektiren bir proxy sunucusu veya güvenlik duvarı üzerinden İnternet 'e erişmek için **site sistemi proxy sunucusu hesabını** kullanır:

- Varlık Yönetim Bilgileri eşitleme noktası
- Exchange Server bağlayıcısı
- Hizmet bağlantı noktası
- Yazılım güncelleştirme noktası

> [!IMPORTANT]  
> Gerekli proxy sunucusu veya güvenlik duvarı için olabilecek en az sayıda izne sahip bir hesap belirtin.  

Daha fazla bilgi için bkz. [proxy sunucu desteği](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>SMTP sunucusu bağlantı hesabı  

Site sunucusu, SMTP sunucusu kimlik doğrulamalı erişim gerektirdiğinde e-posta uyarıları göndermek için **SMTP sunucusu bağlantı hesabını** kullanır.  

> [!IMPORTANT]  
> E-posta göndermek için olabilecek en az izine sahip bir hesap belirtin.  

Daha fazla bilgi için bkz. [uyarıları ve durum sistemini kullanma](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Yazılım güncelleştirme noktası bağlantı hesabı  

Site sunucusu, aşağıdaki iki yazılım güncelleştirme hizmeti için **yazılım güncelleştirme noktası bağlantı hesabını** kullanır:  

- Ürün tanımları, sınıflandırmalar ve yukarı akış ayarları gibi ayarları ayarlayan Windows Server Update Services (WSUS).  

- Bir yukarı akış WSUS sunucusuna veya Microsoft Update'e eşitleme isteyen WSUS Eşitleme Yöneticisi.  

[Site sistemi yükleme hesabı](#site-system-installation-account) , yazılım güncelleştirmeleri için bileşenleri yükleyebilir, ancak yazılım güncelleştirme noktasında yazılım güncelleştirmesine özgü işlevleri gerçekleştiremez. Yazılım güncelleştirme noktası güvenilmeyen bir ormanda olduğundan, bu işlevsellik için site sunucusu bilgisayar hesabını kullanamıyoruz, site sistemi yükleme hesabına ek olarak bu hesabı belirtmeniz gerekir.  

Bu hesap, WSUS 'u yüklediğiniz bilgisayarda bir yerel yönetici olmalıdır. Ayrıca yerel **WSUS yöneticileri** grubunun bir parçası olmalıdır.  

Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).


### <a name="source-site-account"></a>Kaynak site hesabı  

Geçiş işlemi kaynak sitenin SMS sağlayıcısına erişmek için **kaynak site hesabını** kullanır. Geçiş işleri için veri toplamak üzere bu hesap, kaynak sitedeki site nesneleri için **Okuma** izinlerini gerektirir.  

Birlikte bulunan dağıtım noktaları olan Configuration Manager 2007 dağıtım noktanız veya ikincil siteniz varsa, bunları Configuration Manager (geçerli dal) dağıtım noktalarına yükselttiğinizde, bu hesabın da **site** sınıfı için **silme** izinlerine sahip olması gerekir. Bu izin, yükseltme sırasında dağıtım noktasını Configuration Manager 2007 sitesinden başarıyla kaldırmak için kullanılır.  

> [!NOTE]  
> Kaynak site hesabı ve [kaynak site veritabanı hesabı](#source-site-database-account) , Configuration Manager konsolundaki **Yönetim** çalışma alanının **hesaplar** düğümünde **geçiş Yöneticisi** olarak tanımlanır.  

Daha fazla bilgi için bkz. [hiyerarşiler arasında veri geçirme](/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Kaynak site veritabanı hesabı  

Geçiş işlemi kaynak sitenin SQL Server veritabanına erişmek için **kaynak site veritabanı hesabını** kullanır. Kaynak sitenin SQL Server veritabanından veri toplamak için, kaynak site veritabanı hesabının, kaynak sitenin SQL Server veritabanı için **okuma** ve **yürütme** izinlerine sahip olması gerekir.  

Configuration Manager (geçerli dal) bilgisayar hesabını kullanıyorsanız, aşağıdakilerin bu hesap için doğru olduğundan emin olun:  
  
- Configuration Manager 2007 sitesiyle aynı etki alanında **Dağıtılmış com kullanıcıları** güvenlik grubunun bir üyesidir  
- **SMS yöneticileri** güvenlik grubunun bir üyesi  
- Tüm Configuration Manager 2007 nesneleri için **okuma** izni vardır  

> [!NOTE]  
> Kaynak site hesabı ve [kaynak site veritabanı hesabı](#source-site-database-account) , Configuration Manager konsolundaki **Yönetim** çalışma alanının **hesaplar** düğümünde **geçiş Yöneticisi** olarak tanımlanır.  

Daha fazla bilgi için bkz. [hiyerarşiler arasında veri geçirme](/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Görev sırası etki alanına katılacak hesap 

Windows Kurulumu, yeni bir görüntü oluşturulan bilgisayarı etki alanına katmak için **görev dizisi etki alanına katılımı hesabını** kullanır. Bu hesap, **etki alanına Katıl seçeneği Ile** [etki alanı veya çalışma grubuna katıl](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) görev dizisi adımı için gereklidir. Bu hesap, [ağ ayarlarını uygula](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı ile de ayarlanabilir, ancak gerekli değildir.  

Bu hesap, hedef etki alanında **etki alanına katılmayı** gerektirir.  

> [!TIP]  
> Etki alanına katmak için en az izinlerle bir etki alanı kullanıcı hesabı oluşturun ve tüm görev dizileri için kullanın.  

> [!IMPORTANT]  
> Bu hesaba etkileşimli oturum açma izinleri atamayın.  
>   
> Bu hesap için ağ erişim hesabı kullanmayın.  


### <a name="task-sequence-network-folder-connection-account"></a>Görev dizisi ağ klasörü bağlantı hesabı  

Görev dizisi altyapısı, ağdaki paylaşılan bir klasöre bağlanmak için **görev dizisi ağ klasörü bağlantı hesabını** kullanır. Bu hesap, [ağ klasörüne Bağlan](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) görev dizisi adımı için gereklidir.  

Bu hesap, belirtilen paylaşılan klasöre erişmek için izinler gerektirir. Bu bir etki alanı kullanıcı hesabı olmalıdır.  

> [!TIP]  
> Gerekli ağ kaynaklarına erişmek için en az izinlerle bir etki alanı kullanıcı hesabı oluşturun ve tüm görev dizileri için kullanın.  

> [!IMPORTANT]  
> Bu hesaba etkileşimli oturum açma izinleri atamayın.  
>   
> Bu hesap için ağ erişim hesabı kullanmayın.  


### <a name="task-sequence-run-as-account"></a>Görev sırası farklı çalıştır hesabı  

Görev dizisi altyapısı, komut satırlarını veya PowerShell betiklerini yerel sistem hesabı dışındaki kimlik bilgileriyle çalıştırmak için **görev sırası farklı çalıştır hesabını** kullanır. Bu hesap [komut satırını Çalıştır](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) ve [PowerShell Betiği Çalıştır](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) görev dizisi adımlarını, **Bu adımı seçilen hesap olarak çalıştır** seçeneğiyle gerektirir.  

Hesabı, görev dizisinde belirttiğiniz komut satırını çalıştırmak için gereken en düşük izinlere sahip olacak şekilde ayarlayın. Hesap, etkileşimli oturum açma hakları gerektirir. Genellikle yazılım yüklemek ve ağ kaynaklarına erişmek için gereklidir. PowerShell Betiği Çalıştır görevi için bu hesap yerel yönetici izinleri gerektirir. 

> [!IMPORTANT]  
> Bu hesap için ağ erişim hesabı kullanmayın.  
>   
> Hesabı hiçbir şekilde etki alanı yöneticisi yapmayın.  
>   
> Bu hesap için hiçbir şekilde dolaşım profili ayarlama. Görev sırası çalıştırıldığında, hesap için dolaşım profilini indirir. Bu, profilin yerel bilgisayara erişimine açık kalmasını sağlar.  
>   
> Hesabın kapsamını sınırlandırın. Örneğin, her bir görev dizisi için farklı görev dizisi farklı çalıştır hesapları oluşturun. Daha sonra, bir hesap tehlikeye girerse, yalnızca bu hesabın erişimi olan istemci bilgisayarlarının güvenliği aşılmış olur.  
>   
> Komut satırı bilgisayarda yönetim erişimi gerektiriyorsa, görev dizisini çalıştıran tüm bilgisayarlarda yalnızca bu hesap için bir yerel yönetici hesabı oluşturmayı düşünün. Artık ihtiyaç kalmadığında hesabı silin.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Configuration Manager SQL 'de kullanan kullanıcı nesneleri 
<!--SCCMDocs issue #1160-->
Configuration Manager, SQL 'de aşağıdaki kullanıcı nesnelerini otomatik olarak oluşturur ve korur.  Bu nesneler güvenlik/kullanıcılar altında Configuration Manager veritabanı içinde bulunur.  

> [!IMPORTANT]  
>  Bu nesneleri değiştirme veya kaldırma Configuration Manager ortamda çok fazla soruna neden olabilir.  Bu nesnelerde değişiklik yapmanızı öneririz.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Bu nesne, salt okuma bağlamı altındaki sorguları çalıştırmak için kullanılır.  Bu nesne, birkaç saklı yordam ile yararlanılabilir.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Bu nesne, dinamik SQL deyimlerine yönelik izinler sağlamak için kullanılır.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Bu nesne, SQL Raporlama yürütmelerini çalıştırmak için kullanılır.  Şu saklı yordam bu işlevle kullanılır: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Configuration Manager SQL 'de kullanan veritabanı rolleri
<!--SCCMDocs issue #1160-->
Configuration Manager, SQL 'de aşağıdaki rol nesnelerini otomatik olarak oluşturur ve korur. Bu roller, verileri almak veya Configuration Manager veritabanına veri eklemek için her rolün gerekli eylemlerini gerçekleştirmek üzere belirli saklı yordamlara, tablolara, görünümlere ve işlevlere erişim sağlar. Bu nesneler, güvenlik/roller/veritabanı rolleri altındaki Configuration Manager veritabanı içinde bulunur.

> [!IMPORTANT]  
> Bu nesneleri değiştirme veya kaldırma Configuration Manager ortamda çok fazla soruna neden olabilir. Bu nesneleri değiştirmeyin. Aşağıdaki liste yalnızca bilgi amaçlıdır.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Varlık Yönetim Bilgileri toplu lisanslar içeri aktarma. Configuration Manager, RBA erişimini temel alan kullanıcı hesaplarına, Varlık Yönetim Bilgileri birlikte kullanılacak toplu lisansı içeri aktarabilecek şekilde izin verir.  Bu hesap, tam yönetici rolü veya bir varlık Yöneticisi rolü tarafından eklenebilir.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Güncelleştirme eşitlemesini Varlık Yönetim Bilgileri. Configuration Manager, Varlık Yönetim Bilgileri proxy verilerini almak ve karşıya yüklenmek üzere bekleyen AI verilerini görüntülemek için Varlık Yönetim Bilgileri eşitleme noktası hesabı erişimini barındıran bilgisayar hesabına izin verir.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Bant dışı yönetim. Bu rol, Intel AMT 'yi destekleyen cihazlarda verileri almak için Configuration Manager AMT rolü tarafından kullanılır.

> [!NOTE]  
> Bu rol Configuration Manager daha yeni sürümlerinde kullanımdan kaldırılmıştır.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Basit Sertifika Kayıt Protokolü (SCEP) desteklemek için sertifika kayıt noktası. Configuration Manager, sertifika imzalama ve yenileme için SCEP desteği için sertifika kayıt noktasını destekleyen site sisteminin bilgisayar hesabına izin verir.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

Sertifika kayıt noktası PFX desteği. Configuration Manager, imzalama ve yenileme için PFX desteği için yapılandırılmış sertifika kayıt noktasını destekleyen site sisteminin bilgisayar hesabına izin verir.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Cihaz yönetim noktası. Configuration Manager, "mobil cihazların ve Mac bilgisayarın bu yönetim noktasını kullanmasına Izin ver" seçeneğini içeren bir yönetim noktası için bilgisayar hesabına izin verir, MDM kaydı yapılmış cihazlara destek sağlama olanağı sunar.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Hizmet bağlantı noktası. Configuration Manager, telemetri verilerini almak ve sağlamak, bulut hizmetlerini yönetmek ve hizmet güncelleştirmelerini almak için hizmet bağlantı noktasını barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Dağıtılmış görünümler. Configuration Manager, çoğaltma bağlantısı özelliklerinde SQL Server dağıtılmış görünümler seçeneği belirlendiğinde, CA 'larda birincil site sunucularının bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Veri ambarı. Configuration Manager, veri ambarı rolünü barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Kayıt noktası. Configuration Manager, MDM aracılığıyla cihaz kaydına izin vermek için kayıt noktasını barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Tüm genişletilmiş şema görünümlerine erişim sağlar.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Hiyerarşi Yöneticisi hizmeti. Configuration Manager, bu hesabın yük devretme durum iletilerini ve SQL Server Aracı işlemlerini, bir hiyerarşideki siteler arasında yönetmesine izin verir.

> [!NOTE]  
> Smdbrole_WebPortal rolü, varsayılan olarak bu rolün bir üyesidir.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Çok noktaya yayın hizmeti. Configuration Manager, bu izni çok noktaya yayını destekleyen dağıtım noktasının bilgisayar hesabına verir.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Yönetim noktası. Configuration Manager, Configuration Manager istemcileri için destek sağlamak üzere yönetim noktası rolünü barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Yönetim noktası Microsoft BitLocker Yönetimi ve Izleme. Configuration Manager, bir ortam için MBAD 'yi yöneten yönetim noktasını barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Yönetim noktası uygulama Isteği. Configuration Manager, Kullanıcı tabanlı uygulama isteklerini desteklemek için yönetim noktasını barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

SMS sağlayıcısı. Configuration Manager, SMS sağlayıcısı rolünü barındıran bilgisayar hesabına bu izni verir.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Site sunucusu. Configuration Manager, birincil veya CAS sitesini barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Yazılım güncelleştirme noktası. Configuration Manager, üçüncü taraf güncelleştirmeleriyle çalışmak için yazılım güncelleştirme noktasını barındıran bilgisayar hesabına bu izni verir.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Uygulama Kataloğu web sitesi noktası. Configuration Manager, Kullanıcı tabanlı uygulama dağıtımı sağlamak için Uygulama Kataloğu web sitesi noktasını barındıran bilgisayar hesabına izin verir.

### <a name="smsschm_users"></a>smsschm_users

Kullanıcı raporlama erişimi. Configuration Manager, Raporlama Hizmetleri noktası hesabı için kullanılan hesaba, Configuration Manager raporlama verilerinin görüntülenmesini sağlamak üzere SMS raporlama görünümlerine erişim izni verir.  Veriler RBA kullanımıyla daha fazla kısıtlanmıştır.

## <a name="elevated-permissions"></a>Yükseltilmiş izinler

<!-- SCCMDocs#405 -->

Configuration Manager, bazı hesapların devam eden işlemler için yükseltilmiş izinlere sahip olmasını gerektirir. Örneğin, [birincil site yükleme önkoşulları](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri)konusuna bakın. Aşağıdaki liste, bu izinleri ve bunların neden gerekli oldukları nedenleri özetler.

- Birincil site sunucusunun bilgisayar hesabı ve merkezi yönetim site sunucusu şunları gerektirir:

  - Tüm site sistemi sunucularındaki yerel yönetici hakları. Bu izin, sistem hizmetlerini yönetmek, yüklemek ve kaldırmak için kullanılır. Ayrıca, site sunucusu rolleri eklediğinizde veya kaldırdığınızda site sistemindeki yerel grupları da güncelleştirir.

  - Site veritabanının SQL örneğine sysadmin erişimi. Bu izin, site için SQL 'i yapılandırmak ve yönetmek içindir. SQL ile sıkı bir şekilde tümleşen Configuration Manager, yalnızca bir veritabanı değil.

- Tam yönetici rolündeki Kullanıcı hesapları şunları gerektirir:

  - Tüm site sunucularındaki yerel yönetici hakları. Bu izin, sistem hizmetlerini, kayıt defteri anahtarlarını ve değerlerini ve WMI nesnelerini görüntüleme, düzenleme, kaldırma ve yüklemeye yönelik izindir.

  - Site veritabanının SQL örneğine sysadmin erişimi. Bu izin, kurulum veya kurtarma sırasında veritabanını yüklemek ve güncellemek için kullanılır. SQL bakım ve işlemler için de gereklidir. Örneğin, yeniden dizin oluşturma ve istatistikleri güncelleştirme.

    > [!NOTE]
    > Bazı kuruluşlar sysadmin erişimini kaldırmayı seçebilir ve yalnızca gerektiğinde bu izni verebilir. Bu davranış bazen "tam zamanında (JıT) erişim" olarak adlandırılır. Bu durumda, tam yönetici rolüne sahip kullanıcılar, Configuration Manager veritabanında saklı yordamları okumak, güncelleştirmek ve yürütmek için hala erişime sahip olmalıdır. Bu izinler, tam sysadmin erişimi olmadan çoğu sorunu gidermelerine izin verir.
