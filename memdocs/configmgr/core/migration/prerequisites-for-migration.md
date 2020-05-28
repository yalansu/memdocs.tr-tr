---
title: Geçiş önkoşulları
titleSuffix: Configuration Manager
description: Desteklenen Configuration Manager, desteklenen kaynak-site dillerinin ve geçiş için gereken yapılandırmaların sürümlerini anlayın.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36e62ea5198824a6b3466853cdbcfc3057d1829e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428736"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Configuration Manager geçiş önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Desteklenen bir kaynak hiyerarşisinden geçiş yapmak için, her bir geçerli Configuration Manager kaynak sitesine erişiminizin olması ve Configuration Manager hedef sitesindeki izinlerin geçiş işlemlerini yapılandırıp çalıştırması gerekir.  

 Geçiş için desteklenen Configuration Manager sürümlerini ve gerekli konfigürasyonları anlamanıza yardımcı olması için aşağıdaki bölümlerde yer alan bilgileri kullanın.  

-   [Geçiş için desteklenen Configuration Manager sürümleri](#BKMK_SupportedMigrationVersions)  

-   [Geçiş için desteklenen kaynak site dilleri](#BKMK_SorceSiteLanguage)  

-   [Geçiş için gerekli yapılandırmalar](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a>Geçiş için desteklenen Configuration Manager sürümleri  
 Aşağıdaki Configuration Manager sürümlerinden herhangi birini çalıştıran bir kaynak hiyerarşisinden veri geçirebilirsiniz:  

- Configuration Manager 2007 SP2 (geçiş amacıyla, kaynak sitedeki Configuration Manager 2007 R2 veya R3 bir göz önünde bulundurulmaz. Kaynak site SP2 çalıştırdığı sürece, R2 veya R3 eklentisinin yüklü olduğu siteler Configuration Manager geçerli dala geçiş için desteklenir.  

- System Center 2012 Configuration Manager SP2 veya System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Geçişe ek olarak, geçerli dalı Configuration Manager için System Center 2012 Configuration Manager çalıştıran sitelerin yerinde yükseltmesini kullanabilirsiniz.  

- Configuration Manager aynı veya daha az sürümünün Configuration Manager hiyerarşisi.  

  Örneğin, geçerli Configuration Manager dalı 1606 çalıştıran bir hedef hiyerarşiniz varsa, bu sürümü 1606 veya 1602 sürümünü çalıştıran bir kaynak hiyerarşisinden veri kopyalamak için geçiş kullanabilirsiniz. Ancak, 1610 çalıştıran bir kaynak hiyerarşisinden veri geçiremez.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a>Geçiş için desteklenen kaynak site dilleri  
 Configuration Manager hiyerarşileri arasında veri geçirdiğinizde, veriler hedef hiyerarşisinde Configuration Manager için dilden bağımsız biçimde depolanır. Configuration Manager 2007, verileri dilden bağımsız biçimde saklamadığı için, geçiş işlemi Configuration Manager 2007 ' den geçiş sırasında nesneleri bu biçime dönüştürmelidir. Bu nedenle, geçiş için yalnızca aşağıdaki dillerle yüklenen Configuration Manager 2007 kaynak sitesi desteklenir:  

-   İngilizce  

-   Fransızca  

-   Almanca  

-   Japonca  

-   Korece  

-   Rusça  

-   Basitleştirilmiş Çince  

-   Geleneksel Çince  

Bir System Center 2012 Configuration Manager veya Configuration Manager geçerli dal hiyerarşisinden veri geçirdiğinizde, kaynak site dil sınırlamaları yoktur. Kaynak site veritabanındaki nesneler zaten dil belirsiz biçiminde.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a>Geçiş için gerekli yapılandırma  
Aşağıda geçiş ve geçiş işlemleri kullanmak için gereken konfigürasyonlar verilmiştir:  

- **Configuration Manager konsolunda geçişi yapılandırmak, çalıştırmak ve izlemek için:**  

   Hedef sitede hesabınızın **Altyapı Yöneticisi**rol tabanlı yönetim güvenlik rolüne atanması gerekir. Bu güvenlik rolü, geçiş işlerinin oluşturulması, temizleme, izleme ve dağıtım noktalarını paylaşma ve güncelleştirme eylemlerini içeren tüm geçiş işlemlerini yönetme izinleri sağlar.  

- **Veri toplama:**  

   Hedef sitenin veri toplamasını etkinleştirmek üzere aşağıdaki iki kaynak site erişim hesabını her bir kaynak siteyle kullanım için yapılandırmanız gerekir:  

  -   **Kaynak Site Hesabı:** Bu hesap, kaynak siteye ait SMS Sağlayıcısı'na erişmek için kullanılır.  

      -   Configuration Manager 2007 SP2 kaynak sitesi için, bu hesabın tüm kaynak site nesneleri üzerinde **okuma** izni olması gerekir.  

      -   System Center 2012 Configuration Manager veya Configuration Manager geçerli dal kaynak sitesi için bu hesabın tüm kaynak site nesneleri üzerinde **okuma** izni olması gerekir, bu izni rol tabanlı yönetim kullanarak hesaba vermiş olursunuz. Rol tabanlı yönetimi kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Kaynak Site Veritabanı Hesabı:** Bu hesap, kaynak sitenin SQL Server veritabanına erişmek için kullanılır ve kaynak site veritabanı üzerinde **Bağlanma**, **Yürütme**ve **Seçme** izinleri gerektirir.  

  Yeni bir kaynak hiyerarşisi yapılandırırken, ek bir kaynak site için veri toplamayı yapılandırırken veya bir kaynak siteye ait kimlik bilgilerini yeniden yapılandırırken bu hesapları yapılandırabilirsiniz. Bu hesaplar bir etki alanı kullanıcı hesabı kullanabilir veya hedef hiyerarşisine ait en üst düzey sitenin bilgisayar hesabını belirtebilirsiniz.  

  > [!IMPORTANT]  
  >  Herhangi bir erişim hesabı için Configuration Manager bilgisayar hesabı kullanıyorsanız, bu hesabın kaynak sitenin bulunduğu etki alanındaki **Dağıtılmış com kullanıcıları** güvenlik grubunun bir üyesi olduğundan emin olun.  

  Veri toplama sırasında şu ağ protokolleri ve bağlantı noktaları kullanılır:  

  - NetBIOS/SMB-445 (TCP)  

  - RPC (WMı)-135 (TCP & UDP)  

  - Dinamik RPC. Dinamik bağlantı noktaları, işletim sistemi sürümü tarafından tanımlanan bir dizi bağlantı noktası numarası kullanır. Bu bağlantı noktaları, kısa ömürlü bağlantı noktaları olarak da bilinir. Varsayılan bağlantı noktası aralıkları hakkında daha fazla bilgi için, bkz. [Windows için ağ bağlantı noktası koşulları ve hizmete genel bakış](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).<!-- SCCMDocs#1053 -->

  - SQL Server - TCP bağlantı noktaları kaynak ve hedef site veritabanları tarafından kullanılıyor.  

- **Yazılım Güncelleştirmelerini geçir:**  

   Yazılım güncelleştirmelerini geçirmeden önce hedef hiyerarşisini bir yazılım güncelleştirme noktasıyla yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Yazılım güncelleştirmelerini geçirmeyi planlama](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Dağıtım noktalarını paylaş:**  

   Bir kaynak sitedeki herhangi bir dağıtım noktasını başarıyla paylaşmak için hedef hiyerarşisinde en az bir birincil site veya merkezi yönetim sitesi, istemci istekleri için kaynak siteyle aynı bağlantı noktası numaralarını kullanmalıdır. İstemci istek bağlantı noktaları hakkında bilgi için bkz. [istemci iletişim bağlantı noktalarını yapılandırma](../../core/clients/deploy/configure-client-communication-ports.md)  

   Her bir kaynak site için yalnızca bir FQDN ile yapılandırılan site sistem sunucularında yüklü olan dağıtım noktaları paylaşılır.  

   Ayrıca, bir System Center 2012 Configuration Manager Configuration Manager veya geçerli dal kaynak sitesinden bir dağıtım noktası paylaşmak için kaynak site **hesabı** (kaynak site sunucusu Için SMS sağlayıcısına erişir), kaynak sitedeki **site** nesnesi üzerinde **değiştirme** izinlerine sahip olmalıdır. Hesaba bu izni rol tabanlı yönetim kullanarak sağlarsınız. Rol tabanlı yönetimi kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Dağıtım noktalarını yükselt veya yeniden ata:**  

   Kaynak siteye ait SMS Sağlayıcısı'ndan veri toplamak üzere yapılandırılan **Kaynak Site Erişim Hesabı** 'nın şu izinlere sahip olması gerekir:  

  - Configuration Manager 2007 dağıtım noktasını yükseltmek için, hesabın Configuration Manager2007 site sunucusundaki **site** sınıfı üzerinde **okuma**, **yürütme**ve **silme** Izinleri olması gerekir ve bu da dağıtım noktasını Configuration Manager2007 kaynak sitesinden başarıyla kaldırır  

  - System Center 2012 Configuration Manager veya geçerli dal dağıtım noktasını Configuration Manager yeniden atamak için hesabın kaynak sitedeki **site** nesnesi üzerinde **değiştirme** iznine sahip olması gerekir. Hesaba bu izni rol tabanlı yönetim kullanarak sağlarsınız. Rol tabanlı yönetimi kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md).  

    Dağıtım noktasını yeni bir hiyerarşiye başarıyla yükseltmek veya yeniden atamak için kaynak hiyerarşisindeki dağıtım noktasını yöneten sitedeki istemci istekleri için yapılandırılan bağlantı noktaları, dağıtım noktasını yönetecek olan hedef sitedeki istemci istekleri için yapılandırılan bağlantı noktalarıyla eşleşmelidir. İstemci istek bağlantı noktaları hakkında bilgi için bkz. [istemci iletişim bağlantı noktalarını yapılandırma](../../core/clients/deploy/configure-client-communication-ports.md).  
