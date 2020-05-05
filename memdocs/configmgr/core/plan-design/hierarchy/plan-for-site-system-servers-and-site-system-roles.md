---
title: Site sistem rollerini planlayın
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşinizi planlarken, site sistem sunucularını ve site sistem rollerini göz önünde bulundurun.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722448"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Site sistem sunucularını ve site sistem rollerini Configuration Manager için planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yüklediğiniz her bir Configuration Manager site **sistem sunucusu**olan bir site sunucusu içerir. Site, ayrıca, site sunucusundan uzakta olan bilgisayarlardaki ek site sistem sunucularını da içerebilir. Site sistem sunucuları (site sunucusu veya uzak site sistem sunucusu) **site sistem rollerini**destekler.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a>Site sistemi sunucuları  

Bir bilgisayara site sistem rolü yüklediğinizde, o bilgisayar bir site sistem sunucusu olur. Her sitede, bir veya daha fazla ek site sistem sunucusu yükleyebilirsiniz. Ek site sistemi sunucuları yüklemek zorunda değilsiniz ve tüm site sistem rollerini doğrudan site sunucusu bilgisayarında çalıştırmayı tercih edebilirsiniz. Her site sistem sunucusu bir veya daha fazla site sistemi rolünü destekler. Ek sunucular, site sistem rollerinin bir sunucuda yer aldığı işleme yükünü paylaşarak sitenin özelliklerini ve kapasitesini genişletmesine yardımcı olabilir.  

Bir site sistem sunucusunun eklenmesini değerlendirirken sunucunun amaçlanan kullanım için önkoşulları karşıladığından emin olun. Ayrıca, beklenen uç noktalarla iletişim kurmak için yeterli bant genişliğine sahip bir ağ konumuna ekleyin. Bu uç noktalar site sunucusu, etki alanı kaynakları, bulut tabanlı konum, site sistem sunucuları ve istemciler içerir.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a>Site sistemi rolleri  

Siteye ek yetenekler sağlamak için site sistemi rollerini bir sunucuya yükler. Örneklere şunlar dahildir:  

- Sitenin desteklenen kapasitesine kadar daha fazla cihaz destekleyebilmesi için ek yönetim noktaları.  

- İçerik altyapınızı genişlettirecek ek dağıtım noktaları, cihazlara yönelik içerik dağıtımlarının performansını geliştirir.  

- Özelliğe özgü bir veya daha fazla site sistemi rolü. Örneğin, bir yazılım güncelleştirme noktası, yönetilen cihazlar için yazılım güncelleştirmelerini yönetmenizi sağlar. Bir raporlama hizmetleri noktası, ortamınız hakkındaki bilgileri izlemek, anlamak ve paylaşmak için raporları çalıştırmanızı sağlar.  

Farklı Configuration Manager siteleri, farklı site sistem rolü kümelerini destekleyebilir. Desteklenen site sistemi rolleri kümesi, sitenin türüne bağlıdır. (Site türleri bir merkezi yönetim sitesi, birincil siteler veya ikincil siteler içerir.) Hiyerarşinizin topolojisi belirli site türlerindeki bazı rollerin yerleşimini sınırlayabilir. Örneğin, hizmet bağlantı noktası yalnızca hiyerarşinin üst katman sitesinde desteklenir. Üst katman site bir merkezi yönetim sitesi veya tek başına birincil site olabilir. Bu rol bir alt birincil sitede veya ikincil sitelerde desteklenmez.  

Bir site yüklendikten sonra bazı site sistem rollerinin konumunu site sunucusundaki varsayılan konumlarından başka bir sunucuya taşıyabilirsiniz. Örneğin, yönetim noktası veya dağıtım noktası rolleri bir birincil veya ikincil site sunucusuna varsayılan olarak yüklenir. Ayrıca, sitenizin yeteneklerini genişletmek ve iş gereksinimlerinizi karşılamak için bazı site sistem rollerinin ek örneklerini de yükler. Bazı roller gerekir, diğerleri isteğe bağlıdır.  

### <a name="configuration-manager-site-server"></a>Configuration Manager site sunucusu

Bu rol, bir site yüklemek için Configuration Manager Kurulum 'un çalıştırıldığı sunucuyu veya ikincil bir site yüklediğiniz sunucuyu tanımlar. Site kaldırılana kadar bu rolü taşıyamaz veya kaldıramazsınız.  

### <a name="configuration-manager-site-system"></a>Configuration Manager site sistemi

Bu rol, bir site yüklediğiniz veya bir site sistem rolü yüklediğiniz tüm bilgisayarlara atanır. Son site sistem rolünü bilgisayardan kaldırana kadar bu rolü taşıyamaz veya kaldıramazsınız.  

### <a name="configuration-manager-component-site-system-role"></a>Bileşen site sistemi rolü Configuration Manager

Bu rol **SMS Executive** hizmetinin bir örneğini çalıştıran bir site sistemini tanımlar. Yönetim noktaları gibi diğer rolleri desteklemek için gereklidir. Son geçerli site sistem rolünü bilgisayardan kaldırana kadar bu rolü taşıyamaz veya kaldıramazsınız.  

### <a name="configuration-manager-site-database-server"></a>Configuration Manager site veritabanı sunucusu

Site, bu rolü site veritabanının bir örneğini tutan site sistem sunucularına atar. Siteyi site veritabanını barındırmak için farklı bir SQL Server örneğini kullanacak şekilde değiştirmek için, bu rolü yalnızca kurulum 'u çalıştırarak yeni bir sunucuya taşıyın.  

### <a name="sms-provider"></a>site veritabanı

Site, bu rolü SMS sağlayıcısı 'nın bir örneğini barındıran her bilgisayara atar. Sağlayıcı, bir Configuration Manager konsolu ve site veritabanı arasındaki arabirimdir. Bu rol, varsayılan olarak bir merkezi yönetim sitesinin ve birincil sitelerin site sunucusuna otomatik olarak yüklenir. Ek yönetim kullanıcılarına veya yedekliliğe erişim sağlamak için her siteye ek örnekler yükler.  

Ek sağlayıcılar yüklemek için [SMS sağlayıcısı 'Nı yönetmek](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)üzere Configuration Manager kurulumunu çalıştırın. Daha sonra ek bilgisayarlara ek sağlayıcılar yükler. Bir bilgisayara yalnızca bir SMS sağlayıcısı örneği yükler. Bu bilgisayar, site sunucusuyla aynı etki alanında olmalıdır.  

### <a name="application-catalog-web-service-point"></a>Uygulama Kataloğu Web hizmet noktası

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Yazılım Kitaplığı 'ndan Uygulama Kataloğu Web sitesine yazılım bilgileri sağlayan bir site sistemi rolü. Yalnızca birincil sitelerde desteklenmesine karşın, bir siteye veya aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükleyebilirsiniz.  

### <a name="application-catalog-website-point"></a>Uygulama Kataloğu web sitesi noktası

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Kullanıcılara uygulama kataloğu 'ndan kullanılabilir yazılımların listesini sağlayan bir site sistemi rolü. Yalnızca birincil sitelerde desteklenmesine karşın, bir siteye veya aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükleyebilirsiniz.  

### <a name="asset-intelligence-synchronization-point"></a>Varlık Yönetim Bilgileri eşitleme noktası

Varlık Yönetim Bilgileri kataloğu için bilgi indirmek üzere Microsoft 'a bağlanan bir site sistemi rolü. Bu rol kategorilere ayrılmamış başlıkları da yükler, böylece Microsoft bunları kataloğa eklemek için bunları düşünebilirler. Hiyerarşi, hiyerarşinizin üst katman sitesinde bu rolün yalnızca tek bir örneğini destekler. Tek başına bir birincil siteyi daha büyük bir hiyerarşiye genişletirseniz, bu rolü birincil siteden kaldırın. Daha sonra merkezi yönetim sitesine yükleyemezsiniz.

Daha fazla bilgi için [Configuration Manager varlık yönetim bilgileri](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)bakın.  

### <a name="certificate-registration-point"></a>Sertifika kayıt noktası

Ağ aygıtı kayıt hizmeti 'ni (NDES) çalıştıran bir sunucuyla iletişim kuran bir site sistemi rolü. Bu rol, Basit Sertifika Kayıt Protokolü (SCEP) kullanan cihaz sertifika isteklerini yönetir. Bu rol yalnızca birincil sitelerde ve merkezi yönetim sitesinde desteklenir.

Tek bir sertifika kayıt noktası tüm bir hiyerarşiye işlevsellik sağlayabilse de, bir siteye ve aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yüklemek isteyebilirsiniz. Bu tasarım yük dengelemeye yardımcı olur. Bir hiyerarşide birden fazla örnek varsa, istemciler sertifika kayıt noktalarından birine rastgele olarak atanır.  

Her sertifika kayıt noktası ayrı bir NDES örneğine erişim gerektirir. Aynı NDES örneğini kullanmak için iki veya daha fazla sertifika kayıt noktasını yapılandıramazsınız. Ayrıca, sertifika kayıt noktasını NDES çalıştıran sunucuya yüklemeyin.  

### <a name="cloud-management-gateway-connection-point"></a>Bulut yönetimi ağ geçidi bağlantı noktası

[Bulut yönetimi ağ geçidi](../../clients/manage/cmg/plan-cloud-management-gateway.md)ile iletişim kurmak için bir site sistemi rolü.  

### <a name="data-warehouse-service-point"></a>Veri ambarı hizmet noktası

Configuration Manager ortamınızda uzun süreli geçmiş verileri depolamak ve raporlamak için veri ambarı hizmet noktasını kullanın. Daha fazla bilgi için bkz. [veri ambarı](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Dağıtım noktası

İstemcilerin indirileceği kaynak dosyaları içeren bir site sistemi rolü (örneğin:

- Uygulama içeriği
- Yazılım paketleri
- Yazılım güncelleştirmeleri
- İşletim sistemi görüntüleri
- Önyükleme görüntüleri  

Bu rol, varsayılan olarak, yeni bir birincil veya ikincil site yüklediğinizde site sunucusuna yüklenir. Bu rol bir merkezi yönetim sitesinde desteklenmez. Desteklenen bir siteye ve aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükler. Daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](fundamental-concepts-for-content-management.md)ve [içeriği ve içerik altyapısını yönetme](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="endpoint-protection-point"></a>Uç Nokta Koruma noktası

Configuration Manager Endpoint Protection lisans koşullarını kabul etmek ve bulut koruma hizmeti için varsayılan üyeliği yapılandırmak için kullanılan bir site sistemi rolü. Bir hiyerarşi yalnızca bu rolün tek bir örneğini destekler ve bu, en üst katman sitesinde olmalıdır. Tek başına bir birincil siteyi daha büyük bir hiyerarşiye genişletirseniz, bu rolü birincil siteden kaldırın ve merkezi yönetim sitesine yükleyebilirsiniz. Daha fazla bilgi için [Configuration Manager Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)bakın.  

### <a name="enrollment-point"></a>Kayıt noktası

Mobil cihazları ve macOS bilgisayarlarını kaydetmek için Configuration Manager için PKI sertifikalarını kullanan bir site sistemi rolü. Yalnızca birincil sitelerde desteklenmesine karşın, bir siteye veya aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükleyebilirsiniz.  

Bir Kullanıcı Configuration Manager kullanarak mobil cihazları kaydederse ve kullanıcının Active Directory hesabı site sunucusunun ormanı tarafından güvenilmeyen bir ormandaysa, kullanıcının ormanına bir kayıt noktası yükler. Configuration Manager kullanıcının kimliğini doğrulayabilirler.  

### <a name="enrollment-proxy-point"></a>Kayıt proxy noktası

Mobil cihazlardan ve macOS bilgisayarlarından Configuration Manager kayıt isteklerini yöneten bir site sistemi rolü. Yalnızca birincil sitelerde desteklenmesine karşın, bir siteye veya aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükleyebilirsiniz.  

Internet üzerindeki mobil cihazları desteklediğimde, bir çevre ağına bir kayıt proxy noktası yükleyip intranete bir tane yükleyebilirsiniz.

### <a name="exchange-server-connector"></a>Exchange Server bağlayıcısı

Bu rol hakkında daha fazla bilgi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Geri dönüş durumu noktası

İstemci yüklemesini izlemenize yardımcı olan bir site sistemi rolü. Yönetim noktasıyla iletişim kuramadığı için yönetilmeyen istemcileri tanımlar. Bu rol yalnızca birincil sitelerde desteklenmesine karşın, bir siteye ve aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükleyebilirsiniz.

### <a name="management-point"></a>Yönetim noktası

İstemcilere ilke ve hizmet konum bilgileri sağlayan bir site sistemi rolü. Ayrıca istemcilerden yapılandırma verilerini alır.  

Bu rol, varsayılan olarak, yeni bir birincil veya ikincil site yüklediğinizde site sunucusuna yüklenir. Birincil siteler bu rolün birden çok örneğini destekler. İkincil siteler tek bir yönetim noktasını destekler. Proxy yönetim noktası olarak da adlandırılan bu rol, bir ikincil sitedeki bu rol, istemcilerin bilgisayar ve kullanıcı ilkeleri alması için yerel bir iletişim noktası sağlar.  

Yönetim noktalarını HTTP ya da HTTPs destekleyecek şekilde ayarlayın. Ayrıca, Configuration Manager Şirket içi mobil cihaz yönetimi (MDM) ile yönettiğiniz mobil cihazları da destekleyebilir. İstemcilerden gelen istekleri hizmet ettiği için yönetim noktaları tarafından site veritabanı sunucusuna yerleştirilmiş işleme yükünü azaltmaya yardımcı olmak için, [Yönetim noktaları Için veritabanı çoğaltmaları](../../servers/deploy/configure/database-replicas-for-management-points.md)kullanın.  

### <a name="reporting-services-point"></a>Raporlama hizmetleri noktası

Configuration Manager raporları oluşturmak ve yönetmek için SQL Server Reporting Services ile tümleşen bir site sistemi rolü. Bu rol birincil sitelerde ve merkezi yönetim sitesinde desteklenir ve desteklenen bir siteye bu rolün birden çok örneğini yükleyebilirsiniz. Daha fazla bilgi için bkz. [Raporlama planlaması](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Hizmet bağlantı noktası

Sitenizdeki kullanım verilerini yükleyen ve konsolunda kullanılabilir Configuration Manager güncelleştirmeleri yapmak için gerekli olan bir site sistemi rolü. Bir hiyerarşi yalnızca bu rolün tek bir örneğini destekler ve bu, hiyerarşinizin üst katman sitesinde olmalıdır. Tek başına bir birincil siteyi daha büyük bir hiyerarşiye genişletirseniz, bu rolü birincil siteden kaldırın ve merkezi yönetim sitesine yükleyebilirsiniz. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Yazılım güncelleştirme noktası

Configuration Manager istemcilere yazılım güncelleştirmeleri sağlamak üzere Windows Server Update Services (WSUS) ile tümleşen bir site sistemi rolü. Bu rol, tüm sitelerde desteklenir:  

- Bu site sistemini, WSUS ile eşitlenmek üzere merkezi yönetim sitesine yükler.  

- Bu rolün tüm örneklerini alt birincil sitelerde merkezi yönetim sitesiyle eşitlenmek üzere ayarlayın.  

- Ağ üzerinden veri aktarımı yavaş olduğunda, ikincil sitelere bir yazılım güncelleştirme noktası yüklemeyi göz önünde bulundurun.  

Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Durum Geçiş noktası

Bir bilgisayarı yeni bir işletim sistemine geçirdiğinizde, bu site sistem rolü Kullanıcı durumu verilerini depolar. Bu rol birincil sitelerde ve ikincil sitelerde desteklenir. Bir siteye ve aynı hiyerarşideki birden fazla siteye bu rolün birden çok örneğini yükler. Bir işletim sistemini dağıtırken Kullanıcı durumunu depolama hakkında daha fazla bilgi için bkz. [Manage user State](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Sonraki adımlar

Bazı Configuration Manager site sistem rolleri Internet bağlantısı gerektirir. Ortamınız bir ara sunucu kullanmak için internet trafiği gerektiriyorsa, bu site sistem rollerini proxy kullanmak üzere yapılandırın. Daha fazla bilgi için bkz. [proxy sunucu desteği](../network/proxy-server-support.md).  
