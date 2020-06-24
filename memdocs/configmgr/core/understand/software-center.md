---
title: Yazılım Merkezi kullanıcı kılavuzu
titleSuffix: Configuration Manager
description: Yazılım Merkezi 'nin özellikleri ve işlevleri hakkında bilgi edinin
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715559"
---
# <a name="software-center-user-guide"></a>Yazılım Merkezi kullanıcı kılavuzu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kuruluşunuzun BT Yöneticisi, uygulamaları, yazılım güncelleştirmelerini yüklemek ve Windows 'u yükseltmek için yazılım merkezi 'ni kullanır. Bu kullanıcı kılavuzunda, bilgisayar kullanıcıları için yazılım merkezi 'nin işlevleri açıklanmaktadır.

Yazılım Merkezi, BT kuruluşunuzun yönettiği Windows cihazlarına otomatik olarak yüklenir. Başlamak için bkz. [Yazılım Merkezi 'ni açma](#bkmk_open).

Software Center işleviyle ilgili genel notlar:

- Bu makalede, yazılım merkezi 'nin en son özellikleri açıklanmaktadır. Kuruluşunuz, yazılım merkezi 'nin daha eski ancak hala desteklenen bir sürümünü kullanıyorsa, tüm özellikler kullanılamaz. Daha fazla bilgi için BT yöneticinize başvurun.

- BT yöneticiniz, yazılım merkezi 'nin bazı yönlerini devre dışı bırakabilir. Belirli deneyiminiz farklılık gösterebilir.

- Birden fazla kullanıcı aynı anda bir cihaz kullanıyorsa, en düşük oturum KIMLIĞINE sahip kullanıcı yazılım merkezindeki kullanılabilir tüm dağıtımları görmek için tek bir Kullanıcı olur. Örneğin, uzak masaüstü ortamında birden çok kullanıcı. Daha yüksek oturum kimliği olan kullanıcılar, yazılım merkezi 'nde dağıtımlardan bazılarını görmeyebilir. Örneğin, daha yüksek oturum kimliği olan kullanıcılar dağıtılan uygulamaları görebilir, ancak dağıtmayan paketleri veya görev dizilerini görebilirler. Bu sırada, en düşük oturum KIMLIĞINE sahip Kullanıcı dağıtılan tüm uygulamaları, paketleri ve görev dizilerini görür. Windows Görev Yöneticisi 'nin **Kullanıcılar** sekmesi tüm kullanıcıları ve bunların oturum kimliklerini gösterir.

- BT yöneticiniz, yazılım merkezi 'nin rengini değiştirebilir ve kuruluşunuzun logosunu ekleyebilir.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Yazılım Merkezi 'ni açma

Yazılım Merkezi, BT kuruluşunuzun yönettiği Windows cihazlarına otomatik olarak yüklenir. Yazılım merkezini bir Windows 10 bilgisayarında başlatmak için en basit yöntem için **Başlat** ' a basın ve yazın `Software Center` . En iyi eşleşmeyi bulmak için Windows 'un tüm dizesini yazmanız gerekebilir.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Başlat menüsünde Software Center en iyi eşleşme":::

Başlat menüsünde gezinmek için, **Yazılım Merkezi** simgesi Için **Microsoft Uç Nokta Yöneticisi** grubunun altına bakın.

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Microsoft Uç Nokta Yöneticisi başlangıç menüsü simgeleri":::

> [!NOTE]
> Yukarıdaki başlangıç menüsü yolu, Kasım 2019 (sürüm 1910) veya sonraki sürümlere yöneliktir. Önceki sürümlerde, klasör adı **Microsoft System Center**' dır.

Yazılım Merkezi 'ni Başlat menüsünde bulamıyorsanız BT yöneticinize başvurun.

## <a name="applications"></a>Uygulamalar

:::image type="content" source="media/software-center-apps.png" alt-text="Software Center uygulamaları sekmesi" lightbox="media/software-center-apps.png":::

BT yöneticinizin size veya bu bilgisayara dağıttığı uygulamaları bulmak ve yüklemek için **uygulamalar** sekmesini (1) seçin.

- **Tümü** (2): yükleyebilmeniz için tüm kullanılabilir uygulamaları gösterir.

- **Gerekli** (3): BT yöneticiniz bu uygulamaları zorluyor. Bu uygulamalardan birini kaldırırsanız, yazılım merkezi onu yeniden yükler.

- **Filtreler** (4): BT yöneticiniz, uygulama kategorileri oluşturabilir. Varsa, görünümü yalnızca belirli bir kategorideki uygulamalarla filtrelemek için açılan listeyi seçin. Tüm uygulamaları göstermek için **Tümü** ' nü seçin.

- **Sıralama ölçütü** (5): uygulama listesini yeniden düzenleyin. Varsayılan olarak bu liste **en güncel**olanı sıralar. Son kullanılabilir uygulamalar yedi gün boyunca görünür **Yeni** bir başlık ile görüntülenir.

- **Arama** (6): hala aradığınızı bulamıyor musunuz? Bulmak için arama kutusuna anahtar sözcükleri girin!

- Görünümü (7) değiştirin: görünümü liste görünümü ve kutucuk görünümü arasında değiştirmek için simgeleri seçin. Varsayılan olarak, uygulamalar listesi grafik kutucukları olarak gösterilir.

|Simge|Görünüm|Description|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Çoklu seçim modu**|Aynı anda birden fazla uygulama yükler. Daha fazla bilgi için bkz. [birden çok uygulama yüklemesi](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**Liste görünümü**|Bu görünüm uygulama simgesini, adını, yayımcıyı, sürümünü ve durumunu görüntüler.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Kutucuk görünümü**|BT yöneticiniz, simgeleri özelleştirebilir. Her kutucukta uygulama adı, yayımcı ve sürüm görüntülenir.|

### <a name="install-an-application"></a>Uygulama yükleme

Hakkında daha fazla bilgi için listeden bir uygulama seçin. Yüklemek için **yüklemeyi** seçin. Bir uygulama zaten yüklüyse, **kaldırma**seçeneğiniz olabilir.

Bazı uygulamalar, yüklemeden önce onay gerektirebilir.

- Yüklemeyi denediğinizde, bir açıklama girip uygulamayı **isteyebilirsiniz** .

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Yazılım Merkezi uygulama yüklemesi onayı isteği":::

- Yazılım Merkezi istek geçmişini gösterir ve isteği iptal edebilirsiniz.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Yazılım Merkezi uygulama yüklemesi istendi":::

- Bir yönetici isteğinizi onayladığında, uygulamayı yükleyebilirsiniz. Beklerseniz, yazılım merkezi iş dışı saatleriniz sırasında uygulamayı otomatik olarak yüklenir.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Yazılım Merkezi uygulama yüklemesi onaylandı":::

### <a name="install-multiple-applications"></a>Birden çok uygulama yükler

<!-- 1357126 -->
Bir sonraki başlatmadan önce bir defa daha fazla uygulama için bir kez daha yüklemeyi beklemek yerine. Seçilen uygulamaların uygun olması gerekir:

- Uygulama size görünebilir
- Uygulama zaten indirilmedi veya yüklü değil
- BT yöneticiniz uygulamayı yüklemek için onay gerektirmez

Tek seferde birden fazla uygulama yüklemek için:

1. Sağ üst köşedeki çoklu seçim simgesini seçin::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. Yüklemek için iki veya daha fazla uygulama seçin. Listedeki her uygulamanın solundaki onay kutusunu seçin.

3. Başlamak için **Seçileni yüklensin** düğmesini seçin.

Uygulamalar normal olarak yüklenir ve yalnızca hemen birbirini ister.

### <a name="share-an-application"></a>Uygulama paylaşma

Bir bağlantıyı belirli bir uygulamayla paylaşmak için, uygulamayı seçtikten sonra sağ üst köşedeki **paylaşma** simgesini seçin::::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Yazılım Merkezi 'nden uygulama paylaşma":::

Dizeyi **kopyalayın** ve bir e-posta iletisi gibi başka bir yere yapıştırın. Örneğin, `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`. Software Center ile kuruluşunuzdaki diğer kullanıcılar aynı uygulamayı açmak için bağlantıyı kullanabilir.

## <a name="updates"></a>Güncelleştirmeler

:::image type="content" source="media/software-center-updates.png" alt-text="Yazılım Merkezi Güncelleştirmeler sekmesi" lightbox="media/software-center-updates.png":::

BT yöneticinizin bu bilgisayara dağıttığı yazılım güncelleştirmelerini görüntülemek ve yüklemek için **güncelleştirmeler** sekmesini (1) seçin.  

- **Tümü** (2): yükleyebileceğiniz tüm güncelleştirmeleri gösterir

- **Gerekli** (3): BT yöneticiniz bu güncelleştirmeleri zorluyor.

- **Sıralama ölçütü** (4): güncelleştirme listesini yeniden düzenleyin. Varsayılan olarak, bu liste **uygulama adına göre sıralar: a-Z**.

- **Arama** (5): hala aradığınızı bulamıyor musunuz? Bulmak için arama kutusuna anahtar sözcükleri girin!

Güncelleştirmeleri yüklemek için **Tümünü yüklensin** (6) seçeneğini belirleyin.

Yalnızca belirli güncelleştirmeleri yüklemek için, çoklu seçim moduna (7) girmek üzere simgeyi seçin::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Yüklenecek güncelleştirmeleri kontrol edin ve ardından **Seçileni yüklensin**' i seçin.

## <a name="operating-systems"></a>İşletim Sistemleri

:::image type="content" source="media/software-center-os.png" alt-text="Software Center Işletim sistemleri sekmesi" lightbox="media/software-center-os.png":::

BT yöneticinizin bu bilgisayara dağıttığı Windows sürümlerini görüntülemek ve yüklemek için **Işletim sistemleri** sekmesini (1) seçin.  

- **Tümü** (2): yükleyebileceğiniz tüm Windows sürümlerini gösterir

- **Gerekli** (3): BT yöneticiniz bu yükseltmeleri zorluyor.

- **Sıralama ölçütü** (4): güncelleştirme listesini yeniden düzenleyin. Varsayılan olarak, bu liste **uygulama adına göre sıralar: a-Z**.

- **Arama** (5): hala aradığınızı bulamıyor musunuz? Bulmak için arama kutusuna anahtar sözcükleri girin!

## <a name="installation-status"></a>Yükleme durumu

Uygulamaların durumunu görüntülemek için **yükleme durumu** sekmesini seçin. Aşağıdaki durumları görebilirsiniz:

- **Yüklü**: Software Center bu uygulamayı bu bilgisayarda zaten yüklü.

- **İndiriliyor**: Software Center, yazılımı bu bilgisayara yüklemek için indiriyor.

- **Başarısız**: Yazılım Merkezi yazılımı yükleyemedi.

- **Sonrasında yüklenmek üzere zamanlandı**: yaklaşan yazılımları yüklemek için cihazın bir sonraki bakım penceresinin tarihini ve saatini gösterir. Bakım pencereleri BT yöneticiniz tarafından tanımlanır.<!--1358131-->

  - Durum **Tümü** ve **yaklaşan** sekmesinde görülebilir.

  - **Şimdi yüklensin** düğmesini seçerek bakım penceresi zamanından önce yükleyebilirsiniz.

## <a name="device-compliance"></a>Cihaz uyumluluğu

Bu bilgisayarın uyumluluk durumunu görüntülemek için **cihaz uyumluluğu** sekmesini seçin.

BT yöneticiniz tarafından tanımlanan güvenlik ilkelerine karşı bu cihazın ayarlarını değerlendirmek için **uyumluluğu denetle** ' yi seçin.

## <a name="options"></a>Seçenekler

Bu bilgisayarın ek ayarlarını görüntülemek için **Seçenekler** sekmesini seçin.

### <a name="work-information"></a>İş bilgileri

Genellikle çalıştığınız saatleri belirtin. BT yöneticiniz, yazılım yüklemelerini iş saatleriniz dışında zamanlayabilir. Sistem bakım görevleri için her gün en az dört saate izin verin. BT yöneticiniz, iş saatleri boyunca kritik uygulamaları ve yazılım güncelleştirmelerini yüklemeye devam edebilir.

- Bu bilgisayarı kullandığınız en erken ve en son saatleri seçin. Varsayılan olarak, bu değerler **5:00** Ile **10:00 PM**arasında.

- Bu bilgisayarı genellikle kullandığınız haftanın günlerini seçin. Varsayılan olarak, yazılım merkezi yalnızca haftanın günlerini seçer.

İşinizi yapmak için düzenli olarak bu bilgisayarı kullanıp kullanmayacağınızı belirtin. Yöneticiniz uygulamaları otomatik olarak kurabilir veya birincil bilgisayarların kullanımına ek uygulamalar sağlayabilir.<!--3485366--> Kullandığınız bilgisayar birincil bir bilgisayar ise, **işlerim için düzenli olarak bu bilgisayarı**kullanıyorum ' ı seçin.

### <a name="power-management"></a>Güç yönetimi

BT yöneticiniz, güç yönetimi ilkelerini ayarlayabilir. Bu ilkeler, bu bilgisayar kullanımda olmadığında kuruluşunuzun elektrik tasarrufu sağlanmasına yardımcı olur.

Bu bilgisayarın bu ilkelerden muaf olmasını sağlamak için, **BT departmanımın bu bilgisayara güç ayarlarını uygulama**' yı seçin. Varsayılan olarak bu ayar devre dışıdır ve bilgisayar güç ayarlarını uygular.

### <a name="computer-maintenance"></a>Bilgisayar Bakımı

Software Center 'ın son tarihten önce yazılım değişikliklerini nasıl uygulayacağını belirtin.

- **Gerekli yazılımları otomatik olarak yükleme veya kaldırma ve bilgisayarı yalnızca belirtilen iş saatleri dışında yeniden başlatma**: Bu ayar varsayılan olarak devre dışıdır.

- **Bilgisayarım sunu modundayken Software Center etkinliklerini askıya al**: Bu ayar varsayılan olarak etkindir.

BT yöneticiniz tarafından sorulduğunda, **eşitleme ilkesi**' ni seçin. Bu bilgisayar, uygulamalar, yazılım güncelleştirmeleri veya işletim sistemleri gibi yeni bir şey için sunucuları kontrol eder.

### <a name="remote-control"></a>Uzaktan Denetim

Bilgisayarınız için uzaktan erişim ve Uzaktan denetim ayarlarını belirtin.

**BT departmanınızdan uzaktan erişim ayarlarını kullanın**: varsayılan olarak, BT departmanınız size uzaktan yardım eden ayarları tanımlar. Bu bölümdeki diğer ayarlar, BT departmanınızın tanımladığı ayarların durumunu gösterir. Herhangi bir ayarı değiştirmek için, önce bu seçeneği devre dışı bırakın.

- **İzin verilen uzaktan erişim düzeyi**
  - **Uzaktan erişime izin verme**: BT yöneticileri size yardımcı olmak için bu bilgisayara uzaktan erişemez.
  - **Yalnızca görüntüleme**: bir BT Yöneticisi, ekranınızı yalnızca uzaktan görüntüleyebilir.
  - **Tam**: bir BT Yöneticisi, bu bilgisayarı uzaktan denetleyebilir. Bu ayar varsayılan seçenektir.

- **Uzakta olduğumu yönetici tarafından bu bilgisayarın uzaktan denetimine Izin ver**. Bu ayar varsayılan olarak **Evet** ' tir.

- **Bir yönetici bu bilgisayarı uzaktan denetlemeye çalıştığında**
  - **Her seferinde Izin iste**: Bu ayar varsayılan seçenektir.
  - **İzin sorma**

- **Uzaktan Denetim sırasında şunu göster**: Bu görsel bildirimler, bir yöneticinin cihaza uzaktan eriştiğini bildirmek için varsayılan olarak etkindir.
  - **Bildirim alanında durum simgesi**
  - **Masaüstünde bir oturum bağlantı çubuğu**

- **Ses çal**: Bu sesli bildirim, bir yöneticinin cihaza uzaktan erişimi olduğunu bilmenizi sağlar.
  - **Oturum başladığında ve sona erdiğinde**: Bu ayar varsayılan seçenektir.
  - **Oturum sırasında defalarca**
  - **Hiçbir zaman**

## <a name="custom-tabs"></a>Özel sekmeler

BT yöneticiniz varsayılan sekmeleri kaldırabilir veya yazılım merkezi 'ne ek sekmeler ekleyebilir. Özel sekmeler yöneticiniz tarafından adlandırılır ve yöneticinin belirttiği bir Web sitesini açar. Örneğin, BT kuruluşunuzun yardım masası Web sitesini açan "yardım masası" adlı bir sekmeye sahip olabilirsiniz. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>BT yöneticileri hakkında daha fazla bilgi

BT yöneticileri için aşağıdaki makalelerde yazılım merkezi 'nin nasıl planlanacağı ve yapılandırılacağı hakkında daha fazla bilgi bulabilirsiniz:

- [Yazılım Merkezini planlama](../../apps/plan-design/plan-for-software-center.md)
- [Yazılım Merkezi istemci ayarları](../clients/deploy/about-client-settings.md#software-center)
- [Cihaz yeniden başlatma bildirimleri](../clients/deploy/device-restart-notifications.md)
- [Uzaktan denetime giriş](../clients/manage/remote-control/introduction-to-remote-control.md)
