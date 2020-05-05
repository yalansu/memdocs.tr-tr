---
title: Rol tabanlı yönetim temelleri
titleSuffix: Configuration Manager
description: Yönettiğiniz Configuration Manager ve nesnelere yönelik yönetici erişimini denetlemek için rol tabanlı yönetimi kullanın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 62faf2fd736f9751e8b33e821cb814f527a1197c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722861"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Configuration Manager için rol tabanlı yönetimin temelleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Configuration Manager yönetmek için gereken erişimin güvenliğini sağlamak üzere rol tabanlı yönetimi kullanırsınız. Ayrıca, yönettiğiniz nesneler için Koleksiyonlar, dağıtımlar ve siteler gibi erişimi de güvenli hale getirin. Bu makalede tanıtılan kavramları anladıktan sonra, [Configuration Manager için rol tabanlı yönetim yapılandırabilirsiniz](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Rol tabanlı yönetim modeli, aşağıdaki öğeleri kullanarak tüm siteler ve site ayarları için hiyerarşi genelindeki güvenlik erişim ayarlarını merkezi olarak tanımlar ve yönetir:  

- *Güvenlik rolleri* , farklı Configuration Manager nesnelerine bu kullanıcılara (veya Kullanıcı gruplarına) izin vermek üzere yönetici kullanıcılara atanır. Örneğin, istemci ayarlarını oluşturma veya değiştirme izni.  

- *Güvenlik kapsamları* , 2010 Microsoft Office yükleyen bir uygulama gibi bir yönetici kullanıcının yönetmekle sorumlu olduğu nesnelerin belirli örneklerini gruplandırmak için kullanılır.  

- *Koleksiyonlar* , yönetici kullanıcının yönetebileceği kullanıcı gruplarını ve cihaz kaynaklarını belirtmek için kullanılır.  

  Güvenlik rolleri, güvenlik kapsamları ve koleksiyonların birleşimi sayesinde, kuruluşunuzun gereksinimlerini karşılayan yönetim atamalarını ayırt edersiniz. Birlikte kullanıldığında, bir kullanıcının yönetim kapsamını tanımlar, bu, kullanıcının Configuration Manager dağıtımınızda görüntüleyebileceği ve yönetebilecekleri şeydir.  

## <a name="benefits-of-role-based-administration"></a>Rol tabanlı yönetimin avantajları  

- Siteler, yönetim sınırları olarak kullanılmaz.  
- Yönetici kullanıcıları bir hiyerarşi için oluşturursunuz ve bu kullanıcılara yalnızca bir kez güvenlik atamanız gerekir.  
- Tüm güvenlik atamaları çoğaltılır ve hiyerarşi genelinde kullanılabilir.  
- Tipik yönetim görevlerini atamak için kullanılan yerleşik güvenlik rolleri vardır. Belirli iş gereksinimlerinizi destekleyecek kendi özel güvenlik rollerinizi oluşturun.  
- Yönetici kullanıcılar yalnızca yönetme iznine sahip oldukları nesneleri görür.  
- Yönetici güvenlik eylemlerini denetleyebilirsiniz.  

Configuration Manager için yönetim güvenliği tasarlayıp uyguladığınızda, yönetici kullanıcı için *Yönetim kapsamı* oluşturmak üzere aşağıdakileri kullanın:  

- [Güvenlik rolleri](#bkmk_Planroles)  

- [Koleksiyonlar](#bkmk_planCol)  

- [Güvenlik kapsamları](#bkmk_PlanScope)  

 Yönetim kapsamı, bir yönetici kullanıcının Configuration Manager konsolunda yaptığı nesneleri denetler ve kullanıcının bu nesneler üzerinde sahip olduğu izinleri denetler. Rol tabanlı yönetim yapılandırmaları hiyerarşideki her siteye global veri olarak çoğaltılır ve sonra tüm yönetim bağlantılarına uygulanır.  

> [!IMPORTANT]  
> Siteler arası çoğaltma gecikmeleri bir sitenin rol tabanlı yönetimle ilgili değişiklikleri almasını engelleyebilir. Siteler arası veritabanı çoğaltmasını izleme hakkında daha fazla bilgi için, [siteler arasındaki veri aktarımları](../plan-design/hierarchy/data-transfers-between-sites.md) konusuna bakın.  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a>Güvenlik rolleri

 Yönetim kullanıcılarına güvenlik izinleri vermek için güvenlik rollerini kullanın. Güvenlik rolleri, yönetim görevlerini gerçekleştirebilmeleri için yönetim kullanıcılarına atadığınız güvenlik izinleri gruplarıdır. Bu güvenlik izinleri bir yönetim kullanıcısının gerçekleştirebileceği yönetim eylemlerini ve belirli nesne türleri için verilen izinleri tanımlar. Bir güvenlik en iyi yöntemi olarak, en az izinleri sağlayan güvenlik rollerini atayın.  

 Configuration Manager, yönetim görevlerinin tipik gruplamalarını desteklemek için birkaç yerleşik güvenlik rolüne sahiptir ve belirli iş gereksinimlerinizi destekleyecek kendi özel güvenlik rollerinizi de oluşturabilirsiniz. Yerleşik güvenlik rollerine örnekler:  

- *Tam yönetici* Configuration Manager tüm izinleri verir.  

- *Varlık yöneticisi* varlık yönetim bilgileri eşitleme noktası, varlık yönetim bilgileri raporlama sınıfları, yazılım envanteri, donanım envanteri ve ölçüm kurallarını yönetme izinleri verir.  

- *Yazılım Güncelleştirme Yöneticisi* , yazılım güncelleştirmelerini tanımlama ve dağıtma izinleri verir. Bu rolle ilişkili yönetici kullanıcılar koleksiyonlar, yazılım güncelleştirme grupları, dağıtımlar ve şablonlar oluşturabilir.  

- *Güvenlik Yöneticisi* , yönetim kullanıcılarını ekleme ve kaldırma ve yönetici kullanıcılarını güvenlik rolleri, koleksiyonlar ve güvenlik kapsamları ile ilişkilendirme izinleri verir. Bu rolle ilişkili yönetici kullanıcılar ayrıca güvenlik rollerini ve bunların kendilerine atanmış güvenlik kapsamlarını ve koleksiyonlarını oluşturabilir, değiştirebilir ve silebilir.

> [!TIP]  
> Yerleşik güvenlik rollerinin listesini ve oluşturduğunuz özel güvenlik rollerini, açıklamalarıyla birlikte Configuration Manager konsolunda görüntüleyebilirsiniz. Rolleri görüntülemek için, **Yönetim** çalışma alanında, **güvenlik**' i genişletin ve **güvenlik rolleri**' ni seçin.  

 Her güvenlik rolünün farklı nesne türleri için belirli izinleri vardır. Örneğin, *uygulama yazarı* güvenlik rolünde uygulamalar için şu izinler bulunur: onaylama, oluşturma, silme, değiştirme, klasör değiştirme, nesne taşıma, okuma, rapor çalıştırma ve güvenlik kapsamını ayarlama.

 Yerleşik güvenlik rollerinin izinlerini değiştiremezsiniz, ancak bu rolü kopyalayabilir, değişiklikler yapabilir ve sonra bu değişiklikleri yeni bir özel güvenlik rolü olarak kaydedebilirsiniz. Ayrıca, başka bir hiyerarşiden dışarı aktardığınız güvenlik rollerini (örneğin, bir test ağından) içeri aktarabilirsiniz. Yerleşik güvenlik rollerini mi kullanacağınızı, yoksa kendi özel güvenlik rollerinizi mi oluşturmanız gerektiğini öğrenmek için güvenlik rollerini ve izinlerini gözden geçirin.  

### <a name="to-help-you-plan-for-security-roles"></a>Güvenlik rollerini planlamaya yardımcı olması için  

1. Yönetici kullanıcıların Configuration Manager ' de gerçekleştirdiği görevleri belirler. Bu görevler uygulama ve paket dağıtma, işletim sistemleri ve uyumluluk ayarları dağıtma, siteleri ve güvenliği yapılandırma, denetleme, bilgisayarları uzaktan kontrol etme ve envanter verilerini toplama gibi bir veya daha fazla yönetim görev gruplarıyla ilgili olabilir.  

2. Bu yönetim görevlerini yerleşik güvenlik rollerinden bir veya birkaçıyla eşleştirin.  

3. Yönetici kullanıcılardan bazıları birden fazla güvenlik rolü görevlerini gerçekleştirçalışıyorsa, görevleri birleştiren yeni bir güvenlik rolü oluşturmak yerine bu yönetici kullanıcılara birden fazla güvenlik rolü atayın.  

4. Belirlediğiniz görevler yerleşik güvenlik rolleriyle eşlenmezseniz, yeni güvenlik rolleri oluşturun ve test edin.  

Rol tabanlı yönetim için güvenlik rolleri oluşturma ve yapılandırma hakkında bilgi için, [Configuration Manager için rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md) makalesinde [özel güvenlik rolleri oluşturma](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) ve [güvenlik rollerini yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) bölümüne bakın.  

##  <a name="collections"></a><a name="bkmk_planCol"></a>Koleksiyonlarıyla

 Koleksiyonlar bir yönetici kullanıcının görüntüleyebileceği veya yönetebileceği kullanıcı ve bilgisayar kaynaklarını tanımlar. Örneğin, yönetici kullanıcıların uygulama dağıtmaları veya uzaktan kumandayı çalıştırabilmeleri için, bu kaynakları içeren bir koleksiyona erişim veren bir güvenlik rolüne atanmaları gerekir. Kullanıcı ve cihaz koleksiyonları seçebilirsiniz.  

 Koleksiyonlar hakkında daha fazla bilgi için bkz. [koleksiyonlara giriş](../../core/clients/manage/collections/introduction-to-collections.md).  

 Rol tabanlı yönetimi yapılandırmadan önce, aşağıdakilerden herhangi biri nedeniyle yeni koleksiyonlar oluşturmanız gerekip gerekmediğini kontrol edin.  

- İşlevsel organizasyon. Örneğin, sunucu ve iş istasyonlarından oluşan ayrı koleksiyonlar.  
- Coğrafi yerleşim. Örneğin, Kuzey Amerika ve Avrupa için ayrı koleksiyonlar.  
- Güvenlik gereksinimleri ve iş gereksinimleri. Örneğin, üretim ve test bilgisayarları için ayrı koleksiyonlar.  
- Organizasyon yerleşimi. Örneğin, her iş birimi için ayrı koleksiyonlar.  

Rol tabanlı yönetim için koleksiyonları yapılandırma hakkında daha fazla bilgi için, [Configuration Manager için rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md) makalesinde [güvenlik yönetimi için koleksiyonları Yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) konusuna bakın.  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a>Güvenlik kapsamları

 Yönetici kullanıcılara güvenli kılınabilir nesneler için erişim sağlamak için güvenlik kapsamlarını kullanın. Güvenlik kapsamı, yönetici kullanıcılara bir grup olarak atanan, güvenli kılınabilir nesnelerin adlandırılmış bir kümesidir. Güvenliği sağlanabilen tüm nesneler, bir veya daha fazla güvenlik kapsamına atanmalıdır. Configuration Manager iki yerleşik güvenlik kapsamına sahiptir:  

- *Tüm* yerleşik güvenlik kapsamları tüm kapsamlara erişim izni verir. Bu güvenlik kapsamına nesne atayamazsınız.  

- Varsayılan *yerleşik güvenlik* kapsamı, varsayılan olarak tüm nesneler için kullanılır. Configuration Manager ilk kez yüklediğinizde, tüm nesneler bu güvenlik kapsamına atanır.  

Yönetici kullanıcıların görebileceği ve yönetebileceği nesneleri sınırlamak isterseniz, kendi özel güvenlik kapsamlarınızı oluşturup kullanmanız gerekir. Güvenlik kapsamları hiyerarşik bir yapıyı desteklemez ve iç içe geçemez. Güvenlik kapsamları, aşağıdaki öğeleri içeren bir veya daha fazla nesne türü içerebilir:  

- Uyarı abonelikleri  
- Uygulamalar  
- Önyükleme görüntüleri  
- Sınır grupları  
- Yapılandırma öğeleri  
- Özel istemci ayarları  
- Dağıtım noktaları ve dağıtım noktası grupları  
- Sürücü paketleri
- Klasörler (sürüm 1906 ' den başlayarak) <!--3600867-->
- Genel koşullar  
- Geçiş işleri
- İşletim sistemi görüntüleri
- İşletim sistemi yükleme paketleri  
- Paketler  
- Sorgular  
- Siteler  
- Yazılım kullanım ölçümü kuralları  
- Yazılım güncelleştirme grupları  
- Yazılım güncelleştirmeleri paketleri  
- Görev sırası paketleri  
- Windows CE aygıt ayarı öğeleri ve paketleri  

Yalnızca güvenlik rolleri tarafından güvenliği sağlandıklarından güvenlik kapsamlarına dahil olmadığınız bazı nesneler de vardır. Bu nesnelere yönetim erişimi kullanılabilir nesnelerin bir alt kümesiyle sınırlı olamaz. Örneğin, belirli bir site için kullanılan sınır grupları oluşturan bir yönetici kullanıcınız olabilir. Sınır nesnesi güvenlik kapsamlarını desteklemediğinden, bu kullanıcıya yalnızca ilgili siteyle ilişkilendirilmiş olabilecek sınırlara erişim sağlayan bir güvenlik kapsamı atayamazsınız. Sınır nesnesi bir güvenlik kapsamıyla ilişkilendirilemediğinden, bir kullanıcıya sınır nesnelerine erişimi içeren bir güvenlik rolü atadığınızda, bu kullanıcı hiyerarşideki her sınıra erişebilir.  

Güvenlik kapsamları ile sınırlı olmayan nesneler aşağıdaki öğeleri içerir:  

- Active Directory ormanları  
- Yönetici kullanıcılar  
- Uyarılar  
- Kötü amaçlı yazılımdan koruma ilkeleri  
- Sınırlar  
- Bilgisayar ilişkilendirmeleri  
- Varsayılan istemci ayarları  
- Dağıtım şablonları  
- Aygıt sürücüleri  
- Exchange Server bağlayıcısı  
- Siteden siteye eşlemeleri geçişi  
- Mobil aygıt kayıt profilleri  
- Güvenlik rolleri  
- Güvenlik kapsamları  
- Site adresleri  
- Site sistemi rolleri  
- Yazılım başlıkları  
- Yazılım güncelleştirmeleri  
- Durum iletileri  
- Kullanıcı aygıtı benzeşimleri  

Nesnelerin ayrı örneklerine erişimi sınırlamanız gerektiğinde güvenlik kapsamları oluşturun. Örneğin:  

- Üretim uygulamalarını görmesi gereken, ancak test uygulamalarını görmemesi gereken bir grup yönetici kullanıcınız var. Üretim uygulamaları için bir güvenlik kapsamı ve test uygulamaları için başka bir güvenlik kapsamı oluşturun.  

- Farklı yönetici kullanıcılar bir nesnenin bazı örnekleri için farklı erişime gereksinim duyar. örneğin, bir grup yönetici kullanıcı belirli yazılım güncelleştirme grupları için Okuma izni ve başka bir grup yönetici kullanıcı diğer yazılım güncelleştirme grupları için Değiştirme ve Silme izinlerine gereksinim duyar. Bu yazılım güncelleştirme grupları için farklı güvenlik kapsamları oluşturun.  

Rol tabanlı yönetim için güvenlik kapsamlarını yapılandırma hakkında bilgi için, [Configuration Manager için rol tabanlı yönetim yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md) içindeki [bir nesne Için güvenlik kapsamlarını yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) bölümüne bakın.  

## <a name="next-steps"></a>Sonraki adımlar

[Configuration Manager için rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md)
