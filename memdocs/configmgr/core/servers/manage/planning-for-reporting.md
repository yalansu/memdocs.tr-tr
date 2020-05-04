---
title: Raporlama planı
titleSuffix: Configuration Manager
description: Yükleme ayrıntılarından güvenlik ve ağ bant genişliğine sahip olmak üzere Configuration Manager raporlamak için plan yapmanız önemlidir.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713684"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Configuration Manager raporlamak için plan yapın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager raporlama, SQL Server Reporting Services veya Power BI Rapor Sunucusu gelişmiş raporlama özelliklerini kullanmanıza yardımcı olan bir araç ve kaynak kümesi sağlar. Configuration Manager ' de raporlama planlaması yapmanıza yardımcı olması için aşağıdaki bölümleri kullanın.

## <a name="where-to-install-the-reporting-services-point"></a>Raporlama Hizmetleri noktasının nereye yükleneceği

Bir sitede Configuration Manager raporları çalıştırdığınızda, raporların bağlandığı site veritabanındaki bilgilere erişimi vardır. Raporlama hizmetleri noktasının nereye yükleneceğini ve hangi veri kaynağının kullanılacağını belirlemenize yardımcı olmak üzere aşağıdaki bölümleri kullanın.

> [!NOTE]
> Configuration Manager site sistemlerini planlama hakkında daha fazla bilgi için bkz. [site sistemi rolleri ekleme](../deploy/configure/add-site-system-roles.md).

### <a name="supported-site-system-servers"></a> Desteklenen site sistemi sunucuları

Raporlama Hizmetleri noktasını merkezi yönetim sitesine (CAS) ve birincil sitelere yükleyebilirsiniz. Bir sitedeki birden fazla site sisteminde ve hiyerarşideki diğer sitelerde çalışmaktadır. Configuration Manager, ikincil sitelerdeki raporlama hizmetleri noktasını desteklemez. Bir sitedeki ilk raporlama hizmetleri noktası, varsayılan rapor sunucusu olarak ayarlanır. Bir siteye daha fazla raporlama hizmetleri noktası ekleyebilirsiniz, ancak Configuration Manager raporları her sitede varsayılan rapor sunucusunu etkin bir şekilde kullanır. Raporlama Hizmetleri noktasını site sunucusuna veya uzak bir site sistemine yükler. En iyi performans için, uzak bir site sistem sunucusunda SQL Server Reporting Services kullanın.

### <a name="data-replication-considerations"></a> Veri çoğaltma konuları

Raporlama hizmetleri noktanızı nereye yükleyeceğinizi belirlemenize yardımcı olması için aşağıdaki etkenleri göz önünde bulundurun:

- Raporlama veri kaynağı olarak CAS veritabanı olan bir raporlama hizmetleri noktası, Configuration Manager hiyerarşisindeki tüm genel ve site verilerine erişebilir. Bir hiyerarşideki birden fazla site için site verisi içeren raporlara ihtiyacınız varsa, raporlama hizmetleri noktasını CA 'larda bir site sistemine yüklemeyi düşünün. Sonra veritabanını raporlama veri kaynağı olarak kullanın.

- Raporlama veri kaynağı olarak alt birincil site veritabanı olan bir raporlama hizmetleri noktası, yalnızca yerel birincil site ve tüm alt ikincil siteler için genel verilere ve site verilerine erişim sağlar. Configuration Manager hiyerarşisindeki diğer birincil sitelerin site verileri bu birincil siteye çoğaltılmaz. Raporlama Hizmetleri diğer birincil siteler için site verilerine erişemez. Belirli bir birincil site veya genel veriler için site verileri içeren raporlara ihtiyacınız varsa ve kullanıcının diğer birincil sitelerden site verilerine erişimi olmasını istemiyorsanız, birincil sitedeki site sistemine bir raporlama hizmetleri noktası yükleyebilirsiniz. Ardından, birincil sitenin veritabanını raporlama veri kaynağı olarak kullanın.

Genel ve site verileri hakkında daha fazla bilgi için bkz. [veri türleri](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Ağ bandı genişliği ile ilgili dikkat edilmesi gerekenler

Siteyi nasıl yapılandırdığınıza bağlı olarak, aynı sitedeki site sistemleri, sunucu ileti bloğu (SMB), HTTP veya HTTPS kullanarak birbirleriyle iletişim kurar. Configuration Manager bu iletişimi yönetmez. Ağ bant genişliği denetimi olmadan herhangi bir zamanda meydana gelebilir. Raporlama Hizmetleri noktası rolünü bir site sistemine yüklemeden önce kullanılabilir ağ bant genişliğinizi gözden geçirin.

Site sistemlerini planlama hakkında daha fazla bilgi için bkz. [site sistemi rolleri ekleme](../deploy/configure/add-site-system-roles.md).

## <a name="plan-for-role-based-administration"></a>Rol tabanlı yönetimi planlayın

Raporlama güvenliği, yönetici kullanıcılara güvenlik rolleri ve izinleri atayabileceğiniz Configuration Manager diğer nesnelere çok benzer. Yönetici kullanıcılar, ilgili güvenlik hakları olan raporları yalnızca çalıştırabilir ve değiştirebilirler. Configuration Manager konsolunda raporları çalıştırmak için, kullanıcıların **site** izni ve belirli nesneler için yapılandırılan Izinler için **Oku** hakkına ihtiyacı vardır.

Configuration Manager diğer nesnelerden farklı olarak, Configuration Manager konsolundaki yönetici kullanıcılar için ayarladığınız güvenlik hakları da Raporlama Hizmetleri 'nde yapılandırılır. Configuration Manager konsolunda güvenlik haklarını yapılandırdığınızda raporlama hizmetleri noktası Raporlama Hizmetleri 'ne bağlanır ve raporlar için uygun izinleri ayarlar.

Örneğin, **Yazılım Güncelleştirme Yöneticisi** güvenlik rolü, **Raporu Çalıştır** ve **Raporu Değiştir** izinlerine sahiptir. **Yazılım Güncelleştirme Yöneticisi** rolüne sahip kullanıcılar yalnızca yazılım güncelleştirmeleri için raporları çalıştırabilir ve değiştirebilir. Configuration Manager konsolu bu role yönelik diğer nesnelere ilişkin raporları görüntülemez. Bu davranışın istisnası, bazı raporların belirli Configuration Manager güvenli kılınabilir nesnelerle ilişkilendirilmediği durumdur. Bu raporlarda yönetici kullanıcıların, **Site** izninin raporları çalıştırması için **Oku** hakkına ve **Site** izninin raporları değiştirmesi için **Değiştir** hakkına sahip olması gerekir.  

> [!IMPORTANT]
> Raporları başarılı bir şekilde çalıştırmak için Raporlama Hizmetleri noktası hesabından farklı bir etki alanından kullanıcılar için iki etki alanı arasında iki yönlü bir güven oluşturun.

Raporlar rol tabanlı yönetim için tamamen etkinleştirilmiştir. Configuration Manager, raporu çalıştıran kullanıcının izinlerine bağlı olarak dahil edilen tüm raporların verilerini filtreler. Belirli rollere sahip kullanıcılar yalnızca kendi rolleri için tanımlanan bilgileri görüntüleyebilir.

Raporlama için güvenlik hakları hakkında daha fazla bilgi için bkz. [raporlamayı yapılandırma](configuring-reporting.md).

Configuration Manager ' de rol tabanlı yönetim hakkında daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Raporlama önerileri

Configuration Manager raporlama için aşağıdaki önerileri ve ipuçlarını göz önünde bulundurun:

- En iyi performans için raporlama hizmetleri noktasını uzak bir site sistemine yükler. Site sunucusuna yükleyebilirsiniz, ancak raporlama hizmetleri noktası, uzak bir site sistemine yüklediğinizde en iyi şekilde çalışır. Bu rol arka plan işlemi yaparken, diğer rollerle sistem kaynakları için rekabet edebilir. Site ve rol performansına göz önünde bulundurmanız gereken birçok değişken vardır, ancak genel olarak bu yapılandırma raporlamayı ve genel site performansını geliştirir.

- SQL Server Reporting Services sorgularını iyileştirin. Genellikle, tüm raporlama gecikmeleri, sorguları çalıştırmak ve sonuçları almak için geçen süredir. Sorgu Çözümleyicisi ve profil oluşturucu gibi Microsoft SQL Server araçları, sorguları iyileştirmenize yardımcı olabilir.

- Rapor aboneliği işlemini standart ofis saatleri dışında çalışacak şekilde zamanlayın. Mümkün olduğunda, abonelikleri çalışma saatleri dışında işlemek Configuration Manager site veritabanı sunucusundaki CPU işlemini en aza indirebilir. Aynı zamanda bu yöntem, beklenmeyen rapor istekleri için kullanılabilirliği geliştirir.

- Site güncelleştirmeleri yerleşik raporları korur. Bir standart raporu değiştirirseniz, site güncelleştirildiğinde, raporu alt çizgi öneki (`_`) ile yeniden adlandırır. Bu davranış, site güncelleştirmesinin standart rapor tarafından değiştirilen raporun üzerine yazılmayacağı şekilde emin olur.

## <a name="security-and-privacy"></a>Güvenlik ve gizlilik

Configuration Manager rapor, standart Configuration Manager yönetim işlemleri sırasında topladığı bilgileri görüntüler. Örneğin, Configuration Manager bulma veya envanterden toplanan bilgilerin raporunu görüntüleyebilirsiniz. Raporlar, yazılım dağıtımı ve uyumluluk denetimi gibi istemci yönetim işlemleriyle ilgili geçerli durum bilgilerini de içerebilir.

Raporlarda görüntüleyebileceğiniz verileri oluşturabilen Configuration Manager işlemlerine yönelik güvenlik önerileri ve gizlilik bilgileri hakkında daha fazla bilgi için bkz. [güvenlik ve gizlilik Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Sonraki adımlar

[Raporlama için önkoşullar](prerequisites-for-reporting.md)
