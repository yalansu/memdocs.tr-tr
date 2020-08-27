---
title: LAN 'da uyandırma 'yı yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager LAN'da Uyandırma ayarları ' nı seçin.
ms.date: 08/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 33283b13bc28c7d102f014ac3cb4048681343ac2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907856"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Configuration Manager 'da LAN 'da uyandırma 'yı yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bilgisayarları uyku durumundan çıkarmak istediğinizde Configuration Manager için LAN 'da uyandırma ayarlarını belirtin.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a> Sürüm 1810 ' den başlayarak LAN 'da uyandırma
<!--3607710-->
Configuration Manager 1810 ' den başlayarak, Uyuyan makineleri uyandırmaya yönelik yeni bir yol vardır. İstemci, site sunucusuyla aynı alt ağda olmasa bile Configuration Manager konsolundan istemcileri uyandırabilirsiniz. Bakım veya sorgu cihazları yapmanız gerekiyorsa, uykuda olan uzak istemcilerle sınırlı değilsiniz. Site sunucusu aynı uzak alt ağda açık olan diğer istemcileri tanımlamak için istemci bildirim kanalını kullanır ve ardından bu istemcileri LAN 'da uyandırma isteği (Sihirli paket) gönderecek şekilde kullanır. İstemci bildirim kanalının kullanılması, MAC flakandan kaçınmaya yardımcı olur ve bu da bağlantı noktasının yönlendirici tarafından kapatılmasını sağlayabilir. LAN 'da uyandırma 'nın yeni sürümü, [eski sürümle](#bkmk_wol-previous)aynı anda etkinleştirilebilir.

### <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar
<!--7323898, 7363492-->
- Hedef alt ağdaki en az bir istemci uyanık olmalıdır.
- Bu özellik aşağıdaki ağ teknolojilerini desteklemez:
   - IPv6
   - 802.1 x ağ kimlik doğrulaması
    >[!NOTE]
    > 802.1 x ağ kimlik doğrulaması, donanıma ve yapılandırmasına bağlı olarak ek yapılandırma ile çalışabilir.
- Makineler yalnızca **uyandırma** istemci bildirimi aracılığıyla onlara bildirimde bulunduğunda uyanma yapılır.
    - Son Tarih gerçekleştiğinde Uyandırma için LAN 'da uyandırma 'nın eski sürümü kullanılır.
    -  Eski sürüm etkinleştirilmemişse, istemci uyandırma ayarları, **Gerekli dağıtımlar için istemcileri uyandırma** veya **uyandırma PAKETLERI göndermek**için LAN 'da uyandırma 'yı kullanır.  
- DHCP kira süreleri sonsuz olarak ayarlanamaz. <!--8018584-->
   - SleepAgent_ &lt; *etki alanının* \> @SYSTEM_0.log çok büyük ve muhtemelen DHCP kiralamaları sonsuz olarak ayarlandığı ortamlarda bir yayın fırtınası olduğunu görebilirsiniz.  

### <a name="security-role-permissions"></a>Güvenlik rolü izinleri

- Koleksiyon kategorisi altındaki **kaynağı bilgilendir**

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>İstemcileri 1810 sürümünden itibaren LAN 'da uyandırma kullanacak şekilde yapılandırma

Daha önce ağ bağdaştırıcısının özelliklerinde LAN 'da Uyandırma için istemciyi el ile etkinleştirmeniz gerekiyordu. Configuration Manager 1810, **ağ uyandırma Için Izin ver**adlı yeni bir istemci ayarı içerir. Ağ bağdaştırıcısının özelliklerini değiştirmek yerine bu ayarı yapılandırın ve dağıtın.

1. **Yönetim**altında **istemci ayarları**' na gidin.
1. Düzenlemek istediğiniz istemci ayarlarını seçin veya dağıtmak için yeni özel istemci ayarları oluşturun. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](configure-client-settings.md).
1. **Güç yönetimi** istemci ayarları altında, **ağ uyandırma ayarlarına izin ver** ayarı için **Etkinleştir** ' i seçin. Bu ayar hakkında daha fazla bilgi için bkz. [istemci ayarları hakkında](about-client-settings.md#power-management).

4. Configuration Manager 1902 ' den başlayarak, LAN 'da uyandırma 'nın yeni sürümü, **LAN'da Uyandırma bağlantı noktası numarası (UDP)** [istemci ayarı](about-client-settings.md#power-management)için belirttiğiniz özel UDP bağlantı noktasını alır. Bu ayar, LAN 'da uyandırma 'nin hem yeni hem de eski sürümü tarafından paylaşılır.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>1810 ' den başlayarak istemci bildirimini kullanarak bir istemciyi uyandırma
 
Bir koleksiyondaki tek bir istemciyi veya uyuyan istemcileri uyandırabilirsiniz. Koleksiyonda zaten açık olan cihazlarda, bunlar için herhangi bir işlem yapılmaz. Yalnızca uyku modunda olan istemciler bir LAN 'da uyandırma isteği göndermeyecektir. İstemciye uyandırmayı bildirme hakkında daha fazla bilgi için bkz. [İstemci bildirimi](../manage/client-notification.md).

- **Tek bir istemciyi uyandırmak için:** İstemciye sağ tıklayın, **Istemci bildirimi**' ne gidin ve ardından **uyandırma**' ı seçin.

   ![Konsolda istemci bildirimini uyandırma](media/wol-wake-up-client-notification.png)

- **Bir koleksiyondaki tüm uyuyan istemcileri uyandırmak için:** Cihaz koleksiyonuna sağ tıklayın, **Istemci bildirimi**' ne gidin ve ardından **uyandırma**' ı seçin.
   - Bu eylem yerleşik koleksiyonlar üzerinde çalıştırılamaz.
   - Bir koleksiyonda uyku ve uyuyan istemcileri karıştırdığınızda, yalnızca uyku modunda olan istemciler bir LAN 'da uyandırma isteği göndermiştir.
   - Configuration Manager 2002 ' den itibaren bu eylem, merkezi yönetim sitesine, tek başına siteye veya alt birincil siteye bağlı bir konsolundan kullanılabilir.
   - 1910 ve önceki sürümlerde bu eylem yalnızca Configuration Manager konsolu tek başına veya alt birincil siteye bağlıyken etkindir. Bir merkezi yönetim sitesine bağlanıldığında eylem kullanılamaz.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>LAN 'da uyandırma 'nın yalnızca yeni sürümü etkinleştirildiğinde beklemeniz gerekenler

LAN 'da uyandırma 'nın yalnızca yeni sürümü etkinse, yalnızca **uyandırma** istemci bildirimi etkindir. Görev dizileri, yazılım dağıtımı veya yazılım güncelleştirmeleri yüklemesi gibi dağıtımlarda istemciler bir son tarih alındığında bildirim gönderilmez. Uyuyan bir makine yeniden çevrimiçi olduktan sonra yönetim noktası ile iade edildiğinde konsola yansıtılır.

Configuration Manager sürüm 1902 ' den başlayarak, LAN 'da uyandırma bağlantı noktasını belirtebilirsiniz. Bu ayar, LAN 'da uyandırma 'nin hem yeni hem de eski sürümü tarafından paylaşılır.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>LAN 'da uyandırma 'nın her iki sürümü de etkinleştirildiğinde beklemeniz gerekenler

LAN 'da uyandırma 'nın her iki sürümü de etkinse, **uyandırma** istemci bildirimini kullanabilir ve son tarih üzerinde uyanma yapabilirsiniz. İstemci bildirimi, LAN 'da geleneksel uyandırma 'dan biraz farklı çalışır. İstemci bildiriminin nasıl çalıştığına ilişkin kısa bir açıklama için [sürüm 1810 ' den başlayarak lan 'Da uyandırma](#bkmk_wol-1810) bölümüne bakın. **Ağ uyandırma Için Izin ver** yeni istemci AYARı, NIC özelliklerini lan 'da uyandırmaya izin verecek şekilde değiştirecek. Artık ortamınıza eklenen yeni makinelerde el ile değişiklik yapmanız gerekmez. LAN 'da uyandırma işlevinin diğer tüm işlevleri değişmemiştir.

Sürüm 1902 ' den başlayarak, **uyandırma** istemci bildirimi, mevcut **LAN'da Uyandırma bağlantı noktası numarası (UDP)** ayarını geliştirir.


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a>  Sürüm 1806 ve önceki sürümlerde LAN 'da uyandırma

Yazılım güncelleştirmeleri, uygulamalar, görev dizileri ve programlar gibi gerekli yazılımları yüklemek için bilgisayarları uyku durumundan çıkarmak istediğinizde Configuration Manager için LAN 'da uyandırma ayarlarını belirtin.

Uyandırma proxy 'si istemci ayarlarını kullanarak LAN 'da uyandırma 'yı tamamlayabilirsiniz. Ancak, uyandırma proxy 'sini kullanmak için önce site için LAN 'da uyandırma 'yı etkinleştirmeniz ve **yalnızca Uyandırma paketleri kullan** ve LAN 'da uyandırma Iletimi Için **tek noktaya** ayarla seçeneğini belirtmeniz gerekir. Bu uyandırma çözümü, Uzak Masaüstü bağlantısı gibi geçici bağlantıları da destekler.

Bir birincil siteyi LAN 'da Uyandırma için yapılandırmak üzere ilk yordamı kullanın. Ardından, uyandırma proxy 'si istemci ayarlarını yapılandırmak için ikinci yordamı kullanın. Bu ikinci yordam, uyandırma proxy 'si ayarları için varsayılan istemci ayarlarını, hiyerarşideki tüm bilgisayarlara uygulanacak şekilde yapılandırır. Bu ayarların yalnızca seçili bilgisayarlara uygulanmasını istiyorsanız özel bir cihaz ayarı oluşturun ve bu ayarı, uyandırma proxy 'si için yapılandırmak istediğiniz bilgisayarları içeren bir koleksiyona atayın. Özel istemci ayarları oluşturma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../../core/clients/deploy/configure-client-settings.md).

Uyandırma proxy 'si istemci ayarlarını alan bir bilgisayar büyük olasılıkla 1-3 saniye boyunca ağ bağlantısını duraklatacaktır. Bu durum, istemcinin uyandırma proxy sürücüsünü etkinleştirmek üzere ağ arabirimi kartını sıfırlaması gerektiği için oluşur.

> [!WARNING]
> Ağ hizmetlerinize beklenmeyen kesintiden kaçınmak için, önce yalıtılmış ve temsili bir ağ altyapısında uyandırma proxy 'sini değerlendirin. Daha sonra özel istemci ayarlarını kullanarak testinizi birkaç alt ağdaki seçili bir bilgisayar grubuna genişletin. Uyandırma proxy 'sinin nasıl çalıştığı hakkında daha fazla bilgi için bkz. [istemcileri nasıl uyandırmayı planlayın](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Sürüm 1806 ve önceki sürümleri için bir site için LAN 'da uyandırma 'yı yapılandırmak için

 LAN 'da uyandırma 'yı kullanmak için, hiyerarşideki her site için etkinleştirmeniz gerekir.

1. Configuration Manager konsolunda **yönetim > site yapılandırması > siteleri**' ne gidin.
2. Yapılandırılacak birincil siteye tıklayın ve ardından **Özellikler**' e tıklayın.
3. **LAN 'Da uyandırma** sekmesine tıklayın ve bu site için ihtiyaç duyduğunuz seçenekleri yapılandırın. Uyandırma proxy 'sini desteklemek için **yalnızca Uyandırma paketleri kullan** ve **tek noktaya yayın**' ı seçtiğinizden emin olun. Daha fazla bilgi için bkz. [istemcileri uyandırmayı planlayın](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. **Tamam** ' a tıklayın ve hiyerarşideki tüm birincil siteler için yordamı tekrarlayın.

![Site özelliklerinde LAN'da Uyandırma etkinleştir](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Uyandırma proxy 'si istemci ayarlarını yapılandırmak için

1. Configuration Manager konsolunda **yönetim > Istemci ayarları**' na gidin.
2. **Varsayılan Istemci ayarları**' na ve ardından **Özellikler**' e tıklayın.
3. **Güç yönetimi** ' ni seçin ve ardından **uyandırma proxy 'Sini etkinleştir**için **Evet** ' i seçin.
4. Gözden geçirin ve gerekirse, diğer uyandırma proxy ayarlarını yapılandırın. Bu ayarlar hakkında daha fazla bilgi için bkz. [güç yönetimi ayarları](../../../core/clients/deploy/about-client-settings.md#power-management).
5. **Tamam** ' a tıklayarak iletişim kutusunu kapatın ve ardından varsayılan istemci ayarları iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.

Uyandırma proxy 'sinin yükleme ve yapılandırmasını izlemek için aşağıdaki LAN'da Uyandırma raporlarını kullanabilirsiniz:

- Uyandırma Proxy'si Dağıtım Durumu Özeti
- Uyandırma Proxy'si Dağıtım Durumu Ayrıntıları

> [!TIP]
> Uyandırma proxy 'sinin çalışıp çalışmadığını sınamak için, Uyuyan bir bilgisayara bir bağlantıyı test edin. Örneğin, bu bilgisayardaki paylaşılan bir klasöre bağlanın veya Uzak Masaüstü kullanarak bilgisayara bağlanmayı deneyin. Doğrudan erişim kullanıyorsanız, halen Internet 'te olan uyuyan bir bilgisayar için aynı testleri deneyerek IPv6 öneklerinin çalıştığını denetleyin.
