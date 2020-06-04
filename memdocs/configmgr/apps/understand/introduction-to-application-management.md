---
title: Uygulama yönetimine giriş
titleSuffix: Configuration Manager
description: Configuration Manager içinde uygulama yönetmeniz ve dağıtmanız için ihtiyacınız olan temel bilgileri bulun.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b2fc0dfe37ad51ce1a549545c3eaa716395438d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347123"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Configuration Manager 'de uygulama yönetimine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager uygulamalarla çalışmaya başlamadan önce temel bilgileri öğreneceksiniz.  

> [!TIP]  
> Configuration Manager uygulamaların nasıl yönetileceğini zaten biliyorsanız, bu makaleye atlayın. Örnek uygulama oluşturmak için ilerleyin: [uygulama oluşturma ve dağıtma](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Uygulama nedir?

*Uygulama* veya *uygulama* bilgi işlem sırasında yaygın olarak kullanılan bir terim olsa da, Configuration Manager ' de belirli bir şey anlamına gelir. Uygulamayı bir kutu gibi düşünün. Bu kutu bir yazılım paketi ( *dağıtım türü*olarak bilinir) için bir veya daha fazla yükleme dosyası kümesi ve yazılımın nasıl dağıtılacağı hakkında yönergeler içerir.  

Uygulamayı cihazlara dağıtırken, hangi dağıtım türünün cihaza Configuration Manager yükleneceğine **gereksinim** vardır.  

Bir uygulamayla birçok şeyi yapabilirsiniz. Bu kılavuzu okurken bu şeyler hakkında bilgi edineceksiniz. Aşağıdaki bölümlerde, daha derin bir şekilde başlamadan önce bilmeniz gereken bazı kavramlar tanıtılmaktadır:  

### <a name="deployment-type"></a>Dağıtım türü

*Uygulama* kutu ise *dağıtım türü* , kutudaki içerik kümesidir. Uygulamanın, uygulamanın nasıl yükleneceğini belirlediği için en az bir dağıtım türü olması gerekir. Aynı uygulama için farklı içerik ve yükleme programını yapılandırmak için birden fazla dağıtım türü kullanın.

Örneğin, şirketiniz Astoria adlı bir iş kolu uygulamasına sahiptir. Uygulama geliştiricileri, uygulamayı yüklemek için aşağıdaki yolları sağlar:

- Windows 10 cihazlarında tam işlevsellik için Windows Installer paketi
- Terminal sunucu grubunda kullanılacak App-V paketi
- Mobil kullanıcılar için bir Web uygulaması  

Configuration Manager içinde Astoria için tek bir uygulama oluşturursunuz. Uygulama, tüm yükleme yöntemleri ve platformları genelinde ortak olan uygulama hakkında üst düzey meta verileri tanımlar. Ardından, kullanılabilir yükleme yöntemleri için üç dağıtım türü oluşturursunuz ve uygulamayı tüm kullanıcılara dağıtırsınız. Dağıtım türlerindeki gereksinimlere ve diğer yapılandırmalara göre Configuration Manager her kullanım durumunda doğru yöntemi belirler.

Daha fazla bilgi için bkz. [uygulama için dağıtım türleri oluşturma](../deploy-use/create-applications.md#bkmk_create-dt).

### <a name="requirements"></a>Gereksinimler

Önceki Configuration Manager sürümlerinde, uygulamayı dağıtmak için bir cihaz koleksiyonu oluşturacaksınız. Yine de bir koleksiyon oluşturabilirsiniz, ancak bir uygulama dağıtımı için daha ayrıntılı ölçütler belirtmek üzere *gereksinimleri* kullanın.

Örneğin, bir uygulamanın yalnızca Windows 10 çalıştıran cihazlara yüklenebileceği belirtin. Uygulamayı tüm cihazlarınıza dağıttığınızda, yalnızca Windows 10 çalıştıran cihazlara yüklenir.

Configuration Manager, bir uygulamayı ve onun dağıtım türlerinden birini yükleyip yüklememediğini belirlemede gereksinimleri değerlendirir. Ardından bir uygulamayı yükleyecek doğru dağıtım türünü belirler. Varsayılan olarak, Configuration Manager istemci, **dağıtımlar için yeniden değerlendirmeyi zamanla**istemci ayarına göre uyumluluğu belirlemede gereksinim kurallarını her yedi günde bir yeniden değerlendirmelidir.

Daha fazla bilgi için bkz. uygulama ve [dağıtım türü gereksinimleri](../deploy-use/create-applications.md#bkmk_dt-require) [oluşturma ve dağıtma](../get-started/create-and-deploy-an-application.md) .

### <a name="global-conditions"></a>Genel koşullar

Tek bir uygulamada belirli bir dağıtım türüyle gereksinimleri kullanırken, *genel koşullar*da oluşturabilirsiniz. Bu koşullar, herhangi bir uygulama ve dağıtım türüyle kullanabileceğiniz, önceden tanımlanmış gereksinimlerin bir kitaplığıdır. Configuration Manager yerleşik bir genel koşullar kümesini içerir veya kendi kendinize de oluşturabilirsiniz.

Daha fazla bilgi için bkz. [genel koşullar oluşturma](../deploy-use/create-global-conditions.md).

### <a name="simulated-deployment"></a>Sanal dağıtım

*Sanal dağıtım* , bir uygulama için gereksinimleri, algılama yöntemini ve bağımlılıkları değerlendirir. Bir istemci, uygulamayı gerçekten yüklemeden sonuçları raporlar.

Daha fazla bilgi için bkz. [uygulama dağıtımlarının benzetimini](../deploy-use/simulate-application-deployments.md)yapma.  

### <a name="deployment-action"></a>Dağıtım eylemi

*Dağıtım eylemi* , dağıttığınız uygulamayı yüklemek mi yoksa kaldırmak mı istediğinizi belirtir. Tüm dağıtım türleri kaldırma eylemini desteklemez.

Daha fazla bilgi için bkz. [uygulamaları dağıtma](../deploy-use/deploy-applications.md).  

### <a name="deployment-purpose"></a>Dağıtım amacı

*Dağıtım amacı* , dağıtım uygulamasının **gerekli** veya **kullanılabilir**olup olmadığını belirtir:  

- İstemci, ayarladığınız zamanlamaya göre *gerekli* bir dağıtımı otomatik olarak kurar. Uygulama gizli değilse, Kullanıcı dağıtım durumunu izleyebilir. Ayrıca, son tarihten önce uygulamayı yüklemek için yazılım merkezi 'ni de kullanabilirler.  

- Uygulamayı *kullanılabilir*olarak bir kullanıcıya dağıtırsanız, yazılım merkezi 'nde görür ve isteğe bağlı olarak talep edebilir.  

Daha fazla bilgi için bkz. [uygulamaları dağıtma](../deploy-use/deploy-applications.md).  

### <a name="revisions"></a>Düzeltmeler

Bir uygulama veya dağıtım türü üzerinde *düzeltmeler* yaptığınızda, Configuration Manager uygulamanın yeni bir sürümünü oluşturur. Configuration Manager konsolunda aşağıdaki işlemleri gerçekleştirin:

- Her uygulama düzeltmesinin geçmişini görüntüle
- Özelliklerini görüntüleyin
- Uygulamanın önceki bir sürümünü geri yükleme
- Eski sürümü Sil

Daha fazla bilgi için bkz. [uygulamaları gözden geçirme](../deploy-use/revise-and-supersede-applications.md#application-revisions).  

### <a name="detection-method"></a>Algılama yöntemi

Bir cihazın bir uygulamanın zaten yüklü olup olmadığını saptamak için *algılama yöntemlerini* kullanın. Algılama yöntemi uygulamanın yüklü olduğunu gösteriyorsa Configuration Manager yeniden yüklemeyi denemez.

Daha fazla bilgi için bkz. [dağıtım türü algılama yöntemi seçenekleri](../deploy-use/create-applications.md#bkmk_dt-detect).

### <a name="dependencies"></a>Bağımlılıklar

*Bağımlılıklar* , istemcinin bu dağıtım türünü yüklemeden önce yüklenmesi gereken başka bir uygulamadan bir veya daha fazla dağıtım türünü tanımlar.

Daha fazla bilgi için bkz. [dağıtım türü bağımlılıkları](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Yerine Geçme

Configuration Manager, bir *yerine geçme* ilişkisi kullanarak mevcut uygulamaları yükseltmenize veya değiştirmenize olanak sağlar. Bir uygulamayı yenisiyle değiştirdiğinizde, yerine geçilen uygulamanın dağıtım türünü değiştirmek için yeni bir dağıtım türü belirtirsiniz. Ayrıca, istemci yerine geçen uygulamayı yüklemeden önce yenisiyle değiştirilen uygulamayı yükseltip yükseltmemeye karar verebilirsiniz.

Daha fazla bilgi için bkz. [uygulama yerine geçme](../deploy-use/revise-and-supersede-applications.md#application-supersedence).  

### <a name="user-centric-management"></a>Kullanıcı merkezli yönetim

Configuration Manager uygulamalar, belirli kullanıcıları belirli cihazlarla ilişkilendirmenizi sağlayan *Kullanıcı merkezli yönetimi*destekler. Kullanıcı cihazının adını anımsamak yerine kullanıcıya ve cihaza uygulama dağıtın. Bu işlevsellik, kullanıcıların cihazlarının her birinde en önemli uygulamaların her zaman kullanılabilir olduğundan emin olmanıza yardımcı olur. Bir Kullanıcı yeni bir bilgisayar edindiğinde, Configuration Manager oturum açmadan önce uygulamalarını cihaza otomatik olarak yüklenir.

Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  

### <a name="application-group"></a>Uygulama grubu

Sürüm 1906 ' den başlayarak, bir kullanıcı veya cihaz koleksiyonuna tek bir dağıtım olarak gönderebilmeniz için bir uygulama grubu oluşturun. Uygulama grubu hakkında belirttiğiniz meta veriler yazılım merkezi 'nde tek bir varlık olarak görülür. Bu uygulamaları, istemcinin belirli bir sırada yüklemesi için Grup içindeki sıraya alabilirsiniz.

Daha fazla bilgi için bkz. [uygulama grupları oluşturma](../deploy-use/create-app-groups.md).

## <a name="what-application-types-can-you-deploy"></a>Hangi uygulama türlerini dağıtabilirsiniz?

Configuration Manager aşağıdaki uygulama türlerini dağıtmanıza olanak tanır:  

- Windows Installer (MSI)  

- Windows uygulama paketi ve uygulama paketleri (appx, appxdemeti, maltı, msıxdemeti)  

- Microsoft Store Windows uygulama paketi  

- Üçüncü taraf yükleyiciler ve betik sarmalayıcıları için betik yükleyici

- Microsoft App-V v4 ve v5  

- Mac OS  

- Karmaşık uygulamalar için işletim sistemi olmayan dağıtım görev dizisi

Ayrıca, Configuration Manager [Şirket içi cihaz yönetimi](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)aracılığıyla cihazları yönetirken, bu diğer uygulama türlerini yönetin:  

- Windows Phone uygulama paketi (xap)  

- Microsoft Store Windows Phone uygulama paketi  

- MDM üzerinden Windows Installer (MSI)  

- Web uygulaması

## <a name="state-based-applications"></a>Durum tabanlı uygulamalar  

Configuration Manager uygulamalar durum tabanlı izleme kullanır. Kullanıcılar ve cihazlar için son uygulama dağıtım durumunu izleyebilirsiniz. Durum iletileri ayrı aygıtlar hakkındaki bilgileri gösterir. Örneğin, bir uygulamayı bir kullanıcı koleksiyonuna dağıtırsanız, dağıtımın uyumluluk durumunu ve Configuration Manager konsolundaki dağıtım amacını görüntüleyebilirsiniz. Configuration Manager konsolundaki **izleme** çalışma alanından tüm yazılımların dağıtımını izleyin. Daha fazla bilgi için bkz. [uygulamaları izleme](../deploy-use/monitor-applications-from-the-console.md).  

Configuration Manager istemci, uygulama dağıtımlarını düzenli olarak yeniden değerlendirin. Örnek:  

- Kullanıcı dağıtılan bir uygulamayı kaldırır. Sonraki değerlendirme döngüsünün Configuration Manager uygulamanın mevcut olmadığını algılar. İstemci daha sonra uygulamayı otomatik olarak yeniden yükler.  

- Configuration Manager, gereksinimleri karşılayamadığı için bir cihaza uygulama yüklememedi. Sonra, cihaza bir değişiklik yapıldı ve cihaz artık gereksinimleri karşılıyor. Configuration Manager Bu değişikliği algılar ve istemci uygulamayı yüklerse.  

Uygulama dağıtımları için yeniden değerlendirme aralığı ayarlayabilirsiniz. **Yazılım dağıtım** grubundaki **dağıtımlar Için yeniden değerlendirmeyi zamanla** istemci ayarını kullanın. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#software-deployment).  

## <a name="get-started-creating-an-application"></a>Uygulama oluşturmaya başlayın  

Doğrudan bir uygulama oluşturmak istiyorsanız, [uygulama oluşturma ve dağıtma](../get-started/create-and-deploy-an-application.md) makalesindeki bir adım adım bulacaksınız.  

Temel bilgiler hakkında bilgi sahibiyseniz ve kullanılabilir tüm seçenekler hakkında daha ayrıntılı başvuru bilgileri arıyorsanız, [uygulamaları oluşturmaya](../deploy-use/create-applications.md)başlayın.  

## <a name="software-center"></a>Yazılım Merkezi  

Yazılım Merkezi, Configuration Manager istemcisiyle yüklenmiş bir Windows uygulamasıdır. Aşağıdaki eylemler için kullanın:  

- Cihaza veya kullanıcıya dağıtılan uygulamaları inceleyin ve isteyin
- Yazılım yüklemelerini yükleme ve zamanlama
- Uygulamalar, yazılım güncelleştirmeleri ve işletim sistemleri için yükleme durumunu görüntüleme
- Uzaktan denetim ayarlarını yapılandırma
- Güç yönetimini ayarlama

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [Uygulama yönetimini planlama ve yapılandırma](../plan-design/plan-for-and-configure-application-management.md)
- [Yazılım Merkezini planlama](../plan-design/plan-for-software-center.md)
- [Yazılım Merkezi kullanıcı kılavuzu](../../core/understand/software-center.md)

> [!Note]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Paketler ve programlar  

Configuration Manager, ürünün önceki sürümlerinde kullanılan paketleri ve programları desteklemeye devam eder.

Daha fazla bilgi için bkz. [paketler ve programlar](../deploy-use/packages-and-programs.md).  

## <a name="next-steps"></a>Sonraki adımlar

Configuration Manager ' de uygulama yönetiminin temel kavramlarını anladığınıza göre, aşağıdaki makalelere geçin:

- [Örnek uygulama oluşturma ve dağıtma](../get-started/create-and-deploy-an-application.md)
- [Uygulama yönetimini planlama ve yapılandırma](../plan-design/plan-for-and-configure-application-management.md)
- [Uygulama oluşturma](../deploy-use/create-applications.md)
