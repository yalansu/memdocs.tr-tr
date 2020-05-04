---
title: Cihaz yeniden başlatma bildirimleri
titleSuffix: Configuration Manager
description: Configuration Manager içindeki çeşitli istemci ayarları için yeniden başlatma bildirimi davranışı.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713397"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager cihaz yeniden başlatma bildirimleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kullanıcının bekleyen bir cihaz yeniden başlatması için aldığı bildirimler [bilgisayar yeniden başlatma istemci ayarlarına](about-client-settings.md#computer-restart) ve hangi Configuration Manager sürümünün kullanılmakta olduğuna göre farklılık gösterebilir. Bu makale, yöneticilerin, bekleyen cihaz yeniden başlatma bildirimleri için kullanıcı deneyiminin ne olduğunu belirlemesine yardımcı olur.

>[!NOTE]
> - Bu makale, Configuration Manager sürüm 1902 ve sürüm 1906 ' de bulunan istemci ayarlarına odaklanır.


## <a name="deployment-types-for-restart-notifications"></a>Yeniden başlatma bildirimleri için dağıtım türleri

[Bilgisayar yeniden başlatma istemci ayarları](about-client-settings.md#computer-restart) , aşağıdaki türlerin yeniden başlatılmasını gerektiren tüm gerekli dağıtımlar için Kullanıcı deneyimini değiştirir:

- [Uygulama](../../../apps/deploy-use/deploy-applications.md)
- [Görev dizisi](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Yazılım güncelleştirmesi](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Bildirim türlerini yeniden Başlat

Yeniden başlatma gerektiğinde, son kullanıcıya yaklaşan yeniden başlatma bildirimi verilir. Kullanıcıların alaalabileceği dört genel bildirim vardır:

Bir yeniden başlatma gerektiğini bildiren **bildirim bildirimi** gerekir. Bildirim bildiriminde bulunan bilgiler, çalıştırdığınız Configuration Manager sürümüne bağlı olarak farklı olabilir. Bu tür bir bildirim Windows işletim sistemine yereldir ve bu tür bir bildirim kullanarak üçüncü taraf yazılımları da görebilirsiniz.

![Bekleyen yeniden başlatmanın bildirim bildirimi](media/3555947-restart-toast.png)

Yeniden başlatma uygulanmadan önce kalan süreyi gösteren bir erteleme seçeneği olan yazılım merkezi bildirimi. İleti, Configuration Manager sürümünüze bağlı olarak farklı olabilir.

![Yeniden başlatma için bekleyen yazılım merkezi bildirimi bekleniyor düğmesi](media/3976435-snooze-restart-countdown.png)

Yazılım Merkezi son geri sayım bildirimi Kullanıcı tarafından kapatılamıyor. Erteleme düğmesi gri olur.

![Software Center son geri sayım bildirimi](media/3976435-final-restart-countdown.png)

Kullanıcı, son tarih gerçekleşmeden önce yeniden başlatılması gereken gerekli yazılımları önceden yüklerse, farklı bir bildirim görür. Aşağıdaki bildirim, hem Kullanıcı deneyimi ayarı bildirimlere izin veriyorsa hem de dağıtım için bildirim kullanmadan oluşur. Bu ayarları yapılandırma hakkında daha fazla bilgi için bkz. [dağıtım **Kullanıcı deneyimi** ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) ve [Gerekli dağıtımlar için Kullanıcı bildirimleri](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Önceden yüklenmiş yazılım bildirimi](media/3976435-proactive-user-restart-notification.png)

- Bildirim kullanmıyorsanız, **kullanılabilir** olarak işaretlenen yazılımın iletişim kutusu, önceden yüklenmiş yazılım ile benzerdir.

  - **Kullanılabilir** yazılımlar için, bildirimin yeniden başlatma için son tarih yoktur ve Kullanıcı kendi erteleme aralığını seçebilir. Daha fazla bilgi için bkz. [onay ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

    !["Kullanılabilir" olarak işaretlenen yazılımın, bildirimde yeniden başlatma için son tarih yok.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Sürüm 1902 ' de cihaz yeniden başlatma bildirimleri

<!--3555947-->
Bazen kullanıcılar, bir yeniden başlatma veya gerekli dağıtım hakkındaki Windows bildirim bildirimini görmez. Ardından, anımsatıcıyı erteleme deneyimini görmez. Bu davranış, istemci son tarihe ulaştığında kötü bir kullanıcı deneyimine yol açabilir.

Sürüm 1902 ' den başlayarak, yazılım değişiklikleri gerektiğinde veya dağıtımların yeniden başlatılması gerektiğinde, daha zorlayıcı bir iletişim kutusu penceresi kullanma seçeneğiniz vardır.

[Bilgisayar yeniden başlatma](about-client-settings.md#computer-restart) istemci ayarları grubunda, aşağıdaki seçeneği etkinleştirin: **bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin**.  

Bu istemci ayarı yapılandırıldığında, bildirim bildirimleri ' nden yeniden başlatma gerektiren tüm gerekli dağıtımlar için Kullanıcı deneyimi değişir:

![Yeniden başlatmanın gerekli bildirimi](media/3555947-restart-toast-initial.png)  

Daha zorlayıcı Yazılım Merkezi iletişim penceresine:

![Bilgisayarınızı yeniden başlatmak için iletişim kutusu penceresi](media/3976435-proactive-user-restart-notification.png)

Yükleme sonrasında Kullanıcı cihazını yeniden başlatmadıysa, anımsatıcı olarak bir bildirim alır. Bu geçici anımsatıcı, kullanıcıya istemci ayarına bağlı olarak görünür: Kullanıcı **Oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki aralığı belirten kullanıcıya geçici bir bildirim görüntüler (dakika)**. Bu ayar, bir yeniden başlatma zorlanmadan önce kullanıcının makineyi yeniden başlatması gereken genel süredir.

- Bildirimler kullandığınızda geçici bildirim:

  ![Bekleyen yeniden başlatmanın bildirim bildirimi](media/3555947-restart-toast.png)

- Bildirim değil, Yazılım Merkezi iletişim kutusu penceresini kullandığınızda geçici bildirim:

  ![Yeniden başlatma için bekleyen yazılım merkezi bildirimi bekleniyor düğmesi](media/3555947-1902-hide-notification.png)

Kullanıcı geçici bildirimden sonra yeniden başlamazsa, kapanmadıkları son geri sayım bildirimi verilir. Son bildirimin görüneceği zaman, istemci ayarına göre belirlenir: kullanıcının **kapatılmadığı bir iletişim kutusu görüntüler; bu, Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önce geri sayım aralığını gösterir (dakika)**. Örneğin, ayar 60 ise, yeniden başlatma zorlanmadan önce bir saat, son bildirim kullanıcıya görünür:

![Software Center son geri sayım bildirimi](media/3555947-1902-final-countdown.png)

Aşağıdaki ayarlar, bilgisayara uygulanan en kısa [bakım penceresinden](../manage/collections/use-maintenance-windows.md) daha kısa sürede olmalıdır:

- **Kullanıcıya, Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki aralığı belirten geçici bir bildirim göster (dakika)**
- **Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki geri sayım aralığını gösteren, kullanıcının kapatamayacağı bir iletişim kutusu görüntüler (dakika)**

> [!IMPORTANT]
> Configuration Manager 1902 ' de, bazı durumlarda iletişim kutusu bildirim bildirimlerini değiştirmez. Bu sorunu çözmek için [Configuration Manager sürüm 1902 için güncelleştirme paketini](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)yükledikten sonra. <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>Sürüm 1906 ' de cihaz yeniden başlatma bildirimleri başlatılıyor
<!--3976435-->
Bazı yöneticiler sık yeniden başlatma bildirimlerini ve yeniden başlatmanın ertelenmesi için kısa bir zaman çerçevesini tercih eder. Diğer yöneticiler, kullanıcıların yeniden başlatma işlemini daha uzun süreler boyunca erteleyeve kullanıcılara bekleyen yeniden başlatma hakkında bilgi gönderilmesini ister. Configuration Manager sürüm 1906, yeniden başlatma bildirimlerinin zamanlaması ve sıklığı üzerinde yönetici ek denetimi sağlar. Aşağıdaki öğeler, yöneticiye daha fazla denetim sağlamak için 1906 ' de sunulmuştur:

- Bilgisayar **yeniden başlatma geri sayım bildirimleri için erteleme süresini belirtin (dakika)** [bilgisayarın yeniden başlatma istemci ayarlarına](about-client-settings.md#computer-restart)eklendi.
- En büyük değeri, kullanıcıya **Kullanıcı oturumu kapatmadan önceki aralığı belirten veya bilgisayar yeniden başlatılmadan (dakika)** 1440 dakikadan (24 saat) 20160 dakikaya (iki hafta) artırılan geçici bir bildirim görüntüler.
- Bekleyen yeniden başlatma işlemi 24 saatten daha az olana kadar Kullanıcı yeniden başlatma bildiriminde bir ilerleme çubuğu görmez.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Son tarihte veya sonrasında gerekli yazılımın yüklendiği zaman bildirimleri

Son tarihte veya sonrasında gerekli yazılım yüklendiğinde, kullanıcılarınız seçtiğiniz istemci ayarlarına bağlı olarak bildirimleri görürler.

**Dağıtım için yeniden başlatma gerektiren ayar, bildirim yerine kullanıcıya bir iletişim kutusu penceresi göster** :

- **No** Son geri sayım bildirimine ulaşılana kadar bildirim alınmaz.
- **Evet** -yazılım merkezi bildirimi görülür.
  - Yeniden başlatma, 24 saatten fazlaysa tahmini bir yeniden başlatma süresi görülür. Bu bildirimin zamanlaması ayarı temel alır: kullanıcıya, **Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki aralığı belirten geçici bir bildirim göster (dakika)**.

     ![Yeniden başlatma zamanı, 24 saatten fazla kaldı](media/3976435-notification-greater-than-24-hours.png)

  - Yeniden başlatma işlemi 24 saatten azsa, bir ilerleme çubuğu görülür. Bu bildirimin zamanlaması ayarı temel alır: kullanıcıya **, Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki aralığı belirten geçici bir bildirim göster (dakika)**

     ![Yeniden başlatma zamanı, 24 saatten az kaldı](media/3976435-notification-less-than-24-hours.png)

Kullanıcı **erteleme** düğmesini seçerse, geri erteleme süresi dolduktan sonra, son geri sayıma ulaşmamaları kabul edildiğinde başka bir geçici bildirim oluşur. Sonraki bildirimin zamanlaması ayarı temel alır: **bilgisayar yeniden başlatma geri sayım bildirimleri (saatler) için erteleme süresini belirtin**. Kullanıcı **erteleme** seçeneğini seçerse ve erteleme aralığı bir saat ise, Kullanıcı son geri sayıma henüz ulaşılmadığını varsayarak 60 dakika içinde yeniden bildirilir.

Son geri sayıma ulaşıldığında, kullanıcıya kapanmadığını bir bildirim verilir. İlerleme çubuğu kırmızıdır ve Kullanıcı **uyku**durumuna vurmaktadır.

![1906 sürümündeki yazılım merkezi son geri sayım bildirimi](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>Kullanıcı son tarihten önce proaktif olarak yükleniyor

Kullanıcı, son tarih gerçekleşmeden önce yeniden başlatılması gereken gerekli yazılımları önceden yüklerse, farklı bir bildirim görür. Bu ayarları yapılandırma hakkında daha fazla bilgi için bkz. [dağıtım **Kullanıcı deneyimi** ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) ve [Gerekli dağıtımlar için Kullanıcı bildirimleri](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

Aşağıdaki bildirim, hem Kullanıcı deneyimi ayarı bildirimlere izin veriyorsa hem de dağıtım için bildirim kullanmadan oluşur:

![Önceden yüklenmiş yazılım bildirimi](media/3976435-proactive-user-restart-notification.png)

Yazılımın son tarihine ulaşıldığında, [gerekli yazılımın son tarih davranışına veya sonrasında yüklendiği zaman bildirimleri](#notifications-when-required-software-is-installed-at-or-after-the-deadline) izlenir.

## <a name="log-files"></a>Günlük dosyaları

Cihaz yeniden başlatmaları sorunlarını gidermek için **Rebootcoordinator. log** ve **SCNotify. log** ' i kullanın. Ayrıca, kullanılan dağıtım türüne göre ek istemci [günlük dosyalarını](../../plan-design/hierarchy/log-files.md) da kullanmanız gerekebilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama yönetimini karşılama](../../../apps/understand/introduction-to-application-management.md)
- [İşletim sistemi dağıtımına giriş](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Yazılım güncelleştirme yönetimine giriş](../../../sum/understand/software-updates-introduction.md)
