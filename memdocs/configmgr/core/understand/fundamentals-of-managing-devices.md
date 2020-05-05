---
title: Cihaz yönetmenin temel ilkeleri
titleSuffix: Configuration Manager
description: Configuration Manager kullanarak cihazları yönetme hakkında bilgi edinin.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722847"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Configuration Manager ile cihazları yönetmenin temelleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, iki geniş cihaz kategorisini yönetebilir:

- *İstemciler* , Configuration Manager istemci yazılımını yüklediğiniz iş istasyonları, dizüstü bilgisayarlar, sunucular ve mobil cihazlar gibi cihazlardır. Donanım envanteri gibi bazı yönetim işlevleri için bu istemci yazılımı gerekir.  

- *Yönetilen cihazlar* *istemcileri*içerebilir, ancak genellikle Configuration Manager istemci yazılımının yüklü olmadığı bir mobil cihazlardır. Bu tür bir cihazda, Configuration Manager ' de yerleşik şirket içi mobil cihaz yönetimini kullanarak yönetirsiniz.

Ayrıca, yalnızca istemci türünü değil, kullanıcıyı temel alan cihazları gruplandırabilir ve tanımlayabilirsiniz.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Configuration Manager istemcisiyle cihaz yönetme

Bir cihazı yönetmek için Configuration Manager istemci yazılımını kullanmanın iki yolu vardır. İlk yöntem, ağınızdaki cihazı keşfetmenin yanı sıra istemci yazılımını bu cihaza dağıtmaktır. Diğer yöntem, istemci yazılımını yeni bir bilgisayara el ile yüklemek ve ardından ağınıza katıldığında bu bilgisayarın sitenize katılmasını sağlamak için kullanılır. İstemci yazılımının yüklü olmadığı cihazları bulmak için, yerleşik bulma yöntemlerinden birini veya birkaçını çalıştırın. Bir cihaz bulunana sonra, istemci yazılımını yüklemek için birkaç yöntemden birini kullanın. Keşfi kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager bulmayı çalıştırma](../servers/deploy/configure/run-discovery.md).  

Configuration Manager istemci yazılımını çalıştırmak için desteklenen cihazları bulduktan sonra, yazılımı yüklemek için çeşitli yöntemlerden birini kullanabilirsiniz. Yazılım yüklendikten ve istemci birincil bir siteye atandıktan sonra cihazı yönetmeye başlayabilirsiniz. Yaygın yükleme yöntemleri şunları içerir:

- Client push yüklemesi

- Yazılım güncelleştirmesi tabanlı yükleme

- Grup İlkesi

- Bir bilgisayara el ile yükleme

- İstemciyi dağıttığınız bir işletim sistemi görüntüsünün parçası olarak dahil etme  

İstemci yüklendikten sonra, cihazları yönetme görevini koleksiyonlar kullanarak basitleştirebilirsiniz. Koleksiyonlar, bunları bir grup olarak yönetebilmeniz için oluşturduğunuz cihaz veya kullanıcı gruplarıdır. Örneğin, Configuration Manager kaydeder tüm mobil cihazlara bir mobil cihaz uygulaması yüklemek isteyebilirsiniz. Bu durumda, tüm mobil cihazlar koleksiyonunu kullanabilirsiniz.  

Daha fazla bilgi için şu makalelere bakın:  

- [Cihaz yönetim çözümü seçme](../plan-design/choose-a-device-management-solution.md)  

- [İstemci yükleme yöntemleri](../clients/deploy/plan/client-installation-methods.md)  

- [Koleksiyonlara giriş](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>İstemci ayarları

Configuration Manager ilk yüklediğinizde, hiyerarşideki tüm istemciler, değiştirebileceğiniz varsayılan istemci ayarları kullanılarak yapılandırılır. İstemci ayarları şu yapılandırma seçeneklerini içerir:

- Cihazların siteyle ne sıklıkla iletişim kurduğu.

- İstemcinin yazılım güncelleştirmeleri ve diğer yönetim işlemleri için ayarlanmış olup olmadığı.

- Kullanıcıların mobil cihazlarını Configuration Manager tarafından yönetilmek üzere kaydedebilecekleri.  

Özel istemci ayarları oluşturabilir ve bunları koleksiyonlara atayabilirsiniz. Koleksiyonun üyeleri özel ayarları olacak şekilde yapılandırılır ve belirttiğiniz sırada uygulanan birden çok özel istemci ayarı oluşturabilirsiniz (sayısal sıraya göre). Çakışan ayarlar varsa, en düşük sayısal sırada olan ayar diğer ayarları geçersiz kılar.  

Aşağıdaki diyagramda özel istemci ayarlarını nasıl oluşturup uygulayacağınızı gösteren bir örnek gösterilmektedir.  

![İstemci ayarları](media/ClientSettings.gif)  

İstemci ayarları hakkında daha fazla bilgi edinmek için aşağıdaki makalelere bakın:

- [İstemci ayarlarını yapılandırma](../clients/deploy/configure-client-settings.md)
- [İstemci ayarları hakkında](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Configuration Manager istemcisi olmadan cihaz yönetme

Configuration Manager, istemci yazılımını yüklememiş ve Intune tarafından yönetilmeyen bazı cihazların yönetimini destekler. Daha fazla bilgi için bkz. [Şirket içi altyapıyla mobil cihazları yönetme Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) ve [mobil cihazları Configuration Manager ve Exchange ile yönetme](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Kullanıcı tabanlı yönetim

Configuration Manager, Azure Active Directory ve Active Directory Domain Services kullanıcı koleksiyonlarını destekler. Bir kullanıcı koleksiyonu kullandığınızda, yazılım, koleksiyonun kullandığı tüm bilgisayarlara yüklenebilir. Dağıttığınız yazılımın yalnızca kullanıcının birincil cihazı olarak belirtilen cihazlara yüklendiğinden emin olmak için, Kullanıcı cihaz benzeşimini ayarlayın. Bir kullanıcının bir veya daha fazla birincil cihazı olabilir.  

Kullanıcıların yazılım dağıtım deneyimlerini denetleyebilme yöntemlerinden biri, **Yazılım Merkezi** istemci arabirimini kullanmaktır. **Yazılım Merkezi** istemci bilgisayarlara otomatik olarak yüklenir ve Windows **Başlat** menüsünden çalıştırılır. **Yazılım Merkezi** , kullanıcıların kendi yazılımlarını yönetmesine ve aşağıdaki görevleri uygulamasına olanak tanır:  

- Yazılımı yükleme  

- Yazılımları çalışma saatleri dışında otomatik olarak yüklenmeye zamanlama  

- Configuration Manager bir cihaza yazılım yükleyebilirim yapılandırma  

- Uzaktan denetim Configuration Manager içinde ayarlandıysa, uzaktan denetim için erişim ayarlarını yapılandırın  

- Yönetici bu seçeneği ayarlarsa, güç yönetimi seçeneklerini yapılandırın  

- Yazılım için tarama, yüklemeye ve isteme

- Tercih ayarlarını yapılandırma

- Ayarlandığında, Kullanıcı cihaz benzeşimi için bir birincil cihaz belirtin

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Yazılım Merkezini planlama](../../apps/plan-design/plan-for-software-center.md)
- [Kullanıcı cihaz benzeşimi ile kullanıcıları ve cihazları bağlama](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Yazılım Merkezi kullanıcı kılavuzu](software-center.md)
