---
title: Yazılım Merkezi kullanıcı kılavuzu
titleSuffix: Configuration Manager
description: Yazılım Merkezi 'nin özellikleri ve işlevleri hakkında bilgi edinin
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722665"
---
# <a name="software-center-user-guide"></a>Yazılım Merkezi kullanıcı kılavuzu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kuruluşunuzun BT Yöneticisi, uygulamaları, yazılım güncelleştirmelerini yüklemek ve Windows 'u yükseltmek için yazılım merkezi 'ni kullanır. Bu kullanıcı kılavuzunda, bilgisayar kullanıcıları için yazılım merkezi 'nin işlevleri açıklanmaktadır.

Software Center işleviyle ilgili genel notlar:

- Bu makalede, yazılım merkezi 'nin en son özellikleri açıklanmaktadır. Kuruluşunuz, yazılım merkezi 'nin daha eski ancak hala desteklenen bir sürümünü kullanıyorsa, tüm özellikler kullanılamaz. Daha fazla bilgi için BT yöneticinize başvurun.

- BT yöneticiniz, yazılım merkezi 'nin bazı yönlerini devre dışı bırakabilir. Belirli deneyiminiz farklılık gösterebilir.

- Birden fazla kullanıcı aynı anda bir cihaz kullanıyorsa, birden fazla uzak masaüstü oturumu aracılığıyla, en düşük oturum KIMLIĞINE sahip olan Kullanıcı, yazılım merkezi 'nde kullanılabilir tüm dağıtımları görmek için tek bir tane olur. Daha yüksek oturum kimliği olan kullanıcılar, yazılım merkezi 'nde dağıtımlardan bazılarını görmeyebilir. Örneğin, daha yüksek oturum kimliği olan kullanıcılar dağıtılan uygulamaları görebilir, ancak dağıtmayan paketleri veya görev dizilerini görebilirler. Bu sırada, en düşük oturum KIMLIĞINE sahip Kullanıcı dağıtılan tüm uygulamaları, paketleri ve görev dizilerini görür.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Yazılım Merkezi 'ni açma

Yazılım merkezini bir Windows 10 bilgisayarında başlatmak için en basit yöntem için **Başlat** ' a basın ve yazın `Software Center`. En iyi eşleşmeyi bulmak için Windows 'un tüm dizesini yazmanız gerekebilir.

Başlat menüsünde gezinirseniz, **Yazılım Merkezi** simgesi Için **Microsoft Uç Nokta Yöneticisi** grubunun altına bakın.

![Microsoft Uç Nokta Yöneticisi başlangıç menüsü simgeleri](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Sürüm 1910 ' de Başlat menüsü yolu değişti. Sürüm 1906 ve önceki sürümlerde klasör adı **Microsoft System Center**' dır. Configuration Manager sürüm 1910 veya üzeri sürümüne güncelleştirdiğinizde, bu yeni konumu dahil etmek için tuttuğunuz tüm dahili belgeleri güncelleştirdiğinizden emin olun.

## <a name="applications"></a>Uygulamalar

BT yöneticinizin size veya bu bilgisayara dağıttığı uygulamaları bulmak ve yüklemek için **uygulamalar** sekmesini seçin.

- **Tümü**: yükleyebileceğiniz tüm uygulamaları gösterir
- **Gerekli**: BT yöneticiniz bu uygulamaları zorluyor. Bu uygulamalardan birini kaldırırsanız, yazılım merkezi onu yeniden yükler.
- **Filtreler**: BT yöneticiniz, uygulama kategorileri oluşturabilir. Varsa, görünümü yalnızca belirli bir kategorideki uygulamalarla filtrelemek için açılan listeyi seçin. Tüm uygulamaları göstermek için **Tümü** ' nü seçin.
- **Sıralama ölçütü**: uygulama listesini yeniden düzenleyin. Varsayılan olarak bu liste **en güncel**olanı sıralar. Son kullanılabilir uygulamalar 7 gün boyunca görünür **Yeni** bir etiketle listelenir.
- **Arama**: hala aradığınızı bulamıyor musunuz? Bulmak için arama kutusuna anahtar sözcükleri girin!
- **Görünümü değiştirin**: görünümü liste görünümü ve kutucuk görünümü arasında değiştirmek için simgeleri seçin. Varsayılan olarak, uygulamalar listesi grafik kutucukları olarak gösterilir.
    - Kutucuk görünümü: BT yöneticiniz simgeleri özelleştirebilir. Her kutucukta uygulama adı, yayımcı ve sürüm görüntülenir.
    - Liste görünümü: Bu görünümde uygulama simgesi, ad, Yayımcı, sürüm ve durum görüntülenir.

### <a name="install-multiple-applications"></a>Birden çok uygulama yükler

<!-- 1357126 -->
Bir sonraki başlatmadan önce bir defa daha fazla uygulama için bir kez daha yüklemeyi beklemek yerine. Tüm uygulamalar uygun değildir:

- Uygulama size görünebilir
- Uygulama zaten indirilmedi veya yüklü değil
- BT yöneticiniz uygulamayı yüklemek için onay gerektirmez

Tek seferde birden fazla uygulama yüklemek için:

1. Liste görünümünde çoklu seçim moduna girmek için çoklu seçim simgesini seçin. ![Software Center çoklu seçim simgesi](media/software-center-multi-select-apps.png) sağ üst köşede.
2. Listedeki uygulamaların solundaki onay kutusunu seçerek yüklemek için iki veya daha fazla uygulama seçin.
3. **Seçili yüklemeyi** Seç düğmesini seçin.

Uygulamalar normal olarak yüklenir ve yalnızca hemen birbirini ister.


## <a name="updates"></a>Güncelleştirmeler

BT yöneticinizin bu bilgisayara dağıttığı yazılım güncelleştirmelerini görüntülemek ve yüklemek için **güncelleştirmeler** sekmesini seçin.  

- **Tümü**: yükleyebileceğiniz tüm güncelleştirmeleri gösterir
- **Gerekli**: BT yöneticiniz bu güncelleştirmeleri zorluyor.
- **Sıralama ölçütü**: güncelleştirme listesini yeniden düzenleyin. Varsayılan olarak, bu liste **uygulama adına göre sıralar: a-Z**.

Güncelleştirmeleri yüklemek için **Tümünü yüklensin**' i seçin.

Yalnızca belirli güncelleştirmeleri yüklemek için, çoklu seçim moduna girmek üzere simgesini seçin. Yüklenecek güncelleştirmeleri kontrol edin ve ardından **Seçileni yüklensin**' i seçin.


## <a name="operating-systems"></a>İşletim Sistemleri

BT yöneticinizin bu bilgisayara dağıttığı Windows sürümlerini görüntülemek ve yüklemek için **Işletim sistemleri** sekmesini seçin.  

- **Tümü**: yükleyebileceğiniz tüm Windows sürümlerini gösterir
- **Gerekli**: BT yöneticiniz bu yükseltmeleri zorluyor.
- **Sıralama ölçütü**: güncelleştirme listesini yeniden düzenleyin. Varsayılan olarak, bu liste **uygulama adına göre sıralar: a-Z**.


## <a name="installation-status"></a>Yükleme durumu

Uygulamaların durumunu görüntülemek için **yükleme durumu** sekmesini seçin. Aşağıdaki durumları görebilirsiniz:

- **Yüklü**: Software Center bu uygulamayı bu bilgisayarda zaten yüklü.
- **İndiriliyor**: Software Center, yazılımı bu bilgisayara yüklemek için indiriyor.
- **Başarısız oldu**: Software Center yazılımı yüklemeye çalışırken bir hatayla karşılaştı.
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

- Bu bilgisayarı kullandığınız en erken ve en son saatleri seçmek için açılan listeleri seçin. Varsayılan olarak, bu değerler **5** Ile **10 PM** arasında

- Bu bilgisayarı genellikle kullandığınız haftanın günlerinin yanındaki onay kutusunu işaretleyin. Software Center varsayılan olarak yalnızca hafta içi günleri seçer.  

İşinizi yapmak için düzenli olarak bu bilgisayarı kullanıp kullanmayacağınızı belirtin. Yöneticiniz uygulamaları otomatik olarak kurabilir veya birincil bilgisayarların kullanımına ek uygulamalar sağlayabilir. <!--3485366-->

- Kullanmakta olduğunuz bilgisayar birincil bir bilgisayar ise **çalışmalarımı yapmak için düzenli olarak bu bilgisayarı** kullanıyorum seçeneğini belirleyin.

### <a name="power-management"></a>Güç yönetimi

BT yöneticiniz, güç yönetimi ilkelerini ayarlayabilir. Bu ilkeler, bu bilgisayar kullanımda olmadığında kuruluşunuzun elektrik tasarrufu sağlanmasına yardımcı olur.

Bu bilgisayarın bu ilkelerden muaf olmasını sağlamak için, **BT departmanımın bu bilgisayara güç ayarlarını uygulama**onay kutusunu seçin. Bu ayar varsayılan olarak devre dışıdır; bilgisayar güç ayarlarını uygular.

### <a name="computer-maintenance"></a>Bilgisayar Bakımı

Software Center 'ın son tarihten önce yazılım değişikliklerini nasıl uygulayacağını belirtin

- **Gerekli yazılımları otomatik olarak yükleme veya kaldırma ve bilgisayarı yalnızca belirtilen iş saatleri dışında yeniden başlatma**: Bu ayar varsayılan olarak devre dışıdır.
- **Bilgisayarım sunu modundayken Software Center etkinliklerini askıya al**: Bu ayar varsayılan olarak etkindir.
- **Eşitleme ilkesi**: BT yöneticiniz tarafından sorulduğunda bu düğmeyi seçin. Bu bilgisayar, uygulamalar, yazılım güncelleştirmeleri veya işletim sistemleri gibi yeni bir şey için sunucuları kontrol eder.

### <a name="remote-control"></a>Uzaktan Denetim

Bilgisayarınız için uzaktan erişim ve Uzaktan denetim ayarlarını belirtin

- **BT departmanınızdan uzaktan erişim ayarlarını kullanın**: Bu onay kutusu varsayılan olarak seçilidir.
- **İzin verilen uzaktan erişim düzeyi**: aşağıdaki 3 seçenekten birini seçin
    - **Uzaktan erişime izin verme**
    - **Yalnızca görünüm**
    - **Tam**: Bu düzey varsayılan olarak etkindir.
- **Uzakta olduğumu yönetici tarafından bu bilgisayarın uzaktan denetimine Izin ver**. Bu ayar varsayılan olarak **Evet** olarak ayarlanır.
- **Bir yönetici bu bilgisayarı uzaktan denetlemeye çalıştığında**: Bu ayar iki seçeneğe sahiptir
    - **Her seferinde Izin iste**: Bu seçenek varsayılan olarak seçilidir.
    - **İzin sorma**
- **Uzaktan Denetim sırasında şunu göster**: her iki seçenek de varsayılan olarak seçilidir
    - **Bildirim alanında durum simgesi**
    - **Masaüstünde bir oturum bağlantı çubuğu**
- **Ses çal**: Bu ayar üç seçeneğe sahiptir
    - **Oturum başladığı ve bittiği zaman**: Bu ayar varsayılan olarak seçilidir.
    - **Oturum sırasında defalarca**
    - **Hiçbir zaman**

    Daha fazla bilgi için bkz. [uzaktan denetime giriş](../clients/manage/remote-control/introduction-to-remote-control.md)
    

## <a name="custom-tab-in-software-center"></a>Yazılım Merkezi 'nde özel sekme

BT yöneticiniz, yazılım merkezi 'ne ek bir sekme eklemiş olabilir. Bu sekme, yöneticiniz tarafından adlandırılır ve belirttikleri bir Web sitesine yönlendirir. Örneğin, kuruluşunuzun yardım masası Web sitesine yol gösteren "yardım masası" adlı bir sekmeye sahip olabilirsiniz. <!--1358132-->
