---
title: Cihaz yeniden başlatma bildirimleri
titleSuffix: Configuration Manager
description: Configuration Manager içindeki çeşitli istemci ayarları için yeniden başlatma bildirimi davranışı.
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b326c4dd8112a72555239f2c3eda078ebf47bf82
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347228"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager cihaz yeniden başlatma bildirimleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kullanıcının bekleyen bir cihaz yeniden başlatması için aldığı bildirimler [bilgisayarın istemci ayarlarını yeniden başlatması](#client-settings) ve hangi Configuration Manager sürümünü kullandığınıza bağlı olarak farklılık gösterebilir. Bu makale, bekleyen cihaz yeniden başlatma bildirimleri için Kullanıcı deneyimini yapılandırmanıza yardımcı olur.

## <a name="deployment-types-for-restart-notifications"></a>Yeniden başlatma bildirimleri için dağıtım türleri

[Bilgisayar yeniden başlatma istemci ayarları](#client-settings) , aşağıdaki türlerin yeniden başlatılmasını gerektiren tüm gerekli dağıtımlar için Kullanıcı deneyimini değiştirir:

- [Uygulama](../../../apps/deploy-use/deploy-applications.md)
- [Görev dizisi](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Yazılım güncelleştirmesi](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Bildirim türlerini yeniden Başlat

Bir cihaz yeniden başlatma gerektirdiğinde, istemci yaklaşan yeniden başlatmanın son kullanıcısına bir bildirim gösterir. Kullanıcıların alabileceği dört genel bildirim vardır.

### <a name="toast-notification"></a>Bildirim

Windows bildirim bildirimi, kullanıcıya cihazın yeniden başlatılması gerektiğini bildirir. Bildirim bildiriminde bulunan bilgiler, çalıştırdığınız Configuration Manager sürümüne bağlı olarak farklı olabilir. Bu tür bir bildirim Windows işletim sistemi için yereldir. Üçüncü taraf yazılımları bu tür bir bildirim kullanarak da görebilirsiniz.

![Bekleyen yeniden başlatmanın bildirim bildirimi](media/3555947-restart-toast.png)

### <a name="software-center-notification-with-snooze"></a>Ertelele yazılım merkezi bildirimi

Yazılım Merkezi, bir erteleme seçeneği ve cihazları yeniden başlamaya zormadan önce kalan süre ile bir bildirim gösterir. İleti, Configuration Manager sürümünüze bağlı olarak farklı olabilir.

![Yeniden başlatma için bekleyen yazılım merkezi bildirimi bekleniyor düğmesi](media/3976435-snooze-restart-countdown.png)

### <a name="software-center-final-countdown-notification"></a>Software Center son geri sayım bildirimi

Yazılım Merkezi, kullanıcının kapatımda veya geri erermesine yönelik bu son geri sayım bildirimini gösterir.

![Software Center son geri sayım bildirimi](media/3976435-final-restart-countdown.png)

Sürüm 1906 ' den başlayarak, bekleyen yeniden başlatma işlemi 24 saatten daha az olana kadar Kullanıcı yeniden başlatma bildiriminde bir ilerleme çubuğu görmez.

### <a name="software-center-notification-before-deadline"></a>Son tarihten önce yazılım merkezi bildirimi

Kullanıcı son tarihten önce gerekli yazılımları önceden yüklerse ve yeniden başlatma gerektiriyorsa, farklı bir bildirim görür. Aşağıdaki bildirim, hem Kullanıcı deneyimi ayarı bildirimlere izin veriyorsa hem de dağıtım için bildirim kullanmadan oluşur. Bu ayarları yapılandırma hakkında daha fazla bilgi için bkz. [dağıtım **Kullanıcı deneyimi** ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) ve [Gerekli dağıtımlar için Kullanıcı bildirimleri](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Önceden yüklenmiş yazılım bildirimi](media/3976435-proactive-user-restart-notification.png)

#### <a name="available-apps"></a>Kullanılabilir uygulamalar

Bildirim kullanmıyorsanız, **kullanılabilir** olarak işaretlenen yazılımın iletişim kutusu, önceden yüklenmiş yazılım ile benzerdir. **Kullanılabilir** yazılımlar için, bildirimin yeniden başlatma için son tarih yoktur ve Kullanıcı kendi erteleme aralığını seçebilir. Daha fazla bilgi için bkz. [onay ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

!["Kullanılabilir" olarak işaretlenen yazılımın, bildirimde yeniden başlatma için son tarih yok.](media/3555947-deployment-marked-available-restart.png)

## <a name="client-settings"></a>İstemci ayarları

İstemci yeniden başlatma davranışlarını denetlemek için **bilgisayar yeniden başlatma** grubunda aşağıdaki cihaz istemci ayarlarını yapılandırın. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](configure-client-settings.md).

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Bir cihazın yeniden başlatılmasından önceki son tarihten sonra geçen süreyi belirtin (dakika)

Bu ayar, bilgisayara uygulanan en kısa bakım penceresinden daha kısa bir süre içinde olmalıdır. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../manage/collections/use-maintenance-windows.md).

Varsayılan değer 90 dakikadır. Sürüm 1906 ' den başlayarak, en yüksek değer 1440 dakika (24 saat) ile 20160 dakikaya (iki hafta) artar.

> [!NOTE]
> Bu ayar daha önce **, kullanıcıya Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki aralığı belirten geçici bir bildirim görüntüler (dakika)**.

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Bir cihaz yeniden başlatılmadan önce kullanıcıya son geri sayım bildirimi sunulırken geçen süreyi belirtin (dakika)

Bu ayar, bilgisayara uygulanan en kısa bakım penceresinden daha kısa bir süre içinde olmalıdır. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../manage/collections/use-maintenance-windows.md).

Varsayılan değer 15 dakikadır.

> [!NOTE]
> Bu ayar daha önce, Kullanıcı **Oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki geri sayım aralığını görüntüleyen kullanıcının kapatamayacağı bir iletişim kutusu görüntüler (dakika)**.

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Son tarihten sonra, bir cihaz yeniden başlatılmadan önce kullanıcıya sunulan anımsatıcı bildirimlerinin sıklığını belirtin (dakika)
<!--3976435-->
_1906 sürümünden başlayarak_

Bu sıklık süresi değeri, **bir cihazın yeniden başlatılmasından önceki son tarihten sonra geçecek süreyi belirtin (dakika)** eksi bir **cihaz yeniden başlatılmadan önce bir kullanıcıya son geri sayım bildirimi (dakika) Için bir değer belirtin**. Aksi takdirde, anımsatıcı bildirimleri çalışmaz.

Varsayılan değer 240 dakikadır.

> [!NOTE]
> Bu ayar daha önce **, bilgisayar yeniden başlatma geri sayım bildirimleri (dakika) için erteleme süresini belirtin**.

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>Bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin
<!--3555947-->
Sürüm 1902 ' den başlayarak, bu ayarı **Evet** olarak yapılandırmak, Kullanıcı deneyimini daha zormak üzere değiştirir. Bu ayar tüm uygulamaların, Görev sıralarının ve yazılım güncelleştirmelerinin tüm dağıtımları için geçerlidir. Daha fazla bilgi için bkz. [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> Configuration Manager 1902 ' de, bazı durumlarda iletişim kutusu bildirim bildirimlerini değiştirmez. Bu sorunu çözmek için [Configuration Manager sürüm 1902 için güncelleştirme paketini](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)yükledikten sonra. <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Cihaz yeniden başlatma bildirimleri (sürüm 1906)
<!--3976435-->
Bazı müşteriler sık yeniden başlatma bildirimlerini tercih eder ve kullanıcılara kısa bir zaman çerçevesinin erteleyebilmesine izin verir. Diğerleri, kullanıcıların yeniden başlatma işlemini daha uzun süreler boyunca erteleyebilsin ve kullanıcıların bekleyen yeniden başlatma işlemini seyrek olarak bilgilendirmesini sağlar. Configuration Manager sürüm 1906 ' den başlayarak, yeniden başlatma bildirimlerinin zamanlaması ve sıklığı üzerinde ek denetime sahip olursunuz.

### <a name="install-required-software-at-or-after-the-deadline"></a>Son tarihe veya sonra gerekli yazılımları yükler

Son tarihte veya sonrasında gerekli yazılım yüklendiğinde, kullanıcılarınız seçtiğiniz istemci ayarlarına bağlı olarak bildirimleri görürler.

**Dağıtım için yeniden başlatma gerektiren ayar, bildirim yerine kullanıcıya bir iletişim kutusu penceresi göster** :

- **Hayır**: Windows, dağıtım son geri sayım bildirimine ulaşıncaya kadar bildirim bildirimlerini gösterir.

- **Evet**: yazılım merkezi bir bildirim gösterir:

  - Yeniden başlatma, 24 saatten fazlaysa tahmini bir yeniden başlatma süresi gösterir. Bu bildirimin zamanlaması, ayarı temel alır: **bir cihazın yeniden başlatılmasından önceki son tarihten sonraki süreyi belirtin (dakika)**.

    ![Yeniden başlatma zamanı, 24 saatten fazla kaldı](media/3976435-notification-greater-than-24-hours.png)

  - Yeniden başlatma işlemi 24 saatten azsa, bir ilerleme çubuğu gösterir. Bu bildirimin zamanlaması, ayarı temel alır: **bir cihazın yeniden başlatılmasından önceki son tarihten sonraki süreyi belirtin (dakika)**.

    ![Yeniden başlatma zamanı, 24 saatten az kaldı](media/3976435-notification-less-than-24-hours.png)

Kullanıcı **erteleme**seçerse, erteleme dönemi dolduktan sonra başka bir geçici bildirim gösterilir. Bu davranış, son geri sayıma henüz ulaşmadığını varsayar. Sonraki bildirimin zamanlaması, ayarı temel alır: **kullanıcıya sunulan, son tarihten sonra, bir cihaz yeniden başlatılmadan önce (dakika) anımsatıcı bildirimlerinin sıklığını belirtin**. Kullanıcı **erteleme**seçeneğini seçerse ve erteleme aralığı bir saat Ise, yazılım merkezi kullanıcıya 60 dakika içinde yeniden bildirim gönderir. Bu davranış, son geri sayıma henüz ulaşmadığını varsayar.

Son geri sayıma ulaştığında, yazılım merkezi kullanıcıya kapanmadıkları bir bildirim gösterir. İlerleme çubuğu kırmızıdır ve **Kullanıcı bunu yeniden** görüntüleyemez.

![1906 sürümündeki yazılım merkezi son geri sayım bildirimi](media/3976435-1906-final-restart-countdown.png)

### <a name="proactively-install-required-software-before-the-deadline"></a>Son tarihten önce gerekli yazılımları proaktif olarak yükler

Kullanıcı son tarihten önce yeniden başlatılması gereken gerekli yazılımları önceden yüklerse, farklı bir bildirim görür. Bu ayarları yapılandırma hakkında daha fazla bilgi için bkz. [dağıtım **Kullanıcı deneyimi** ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) ve [Gerekli dağıtımlar için Kullanıcı bildirimleri](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

Aşağıdaki bildirim, hem Kullanıcı deneyimi ayarı bildirimlere izin veriyorsa hem de dağıtım için bildirim kullanmadan oluşur:

![Önceden yüklenmiş yazılım bildirimi](media/3976435-proactive-user-restart-notification.png)

Dağıtım son tarihine ulaştığında, Yazılım Merkezi, [gerekli yazılımı son tarihte veya sonrasında yüklemek](#install-required-software-at-or-after-the-deadline)için davranışı izler.

## <a name="example-configurations"></a>Örnek yapılandırma

Aşağıdaki örneklerde, istemci ayarlarının belirli davranışları elde etmek üzere nasıl yapılandırılacağı açıklanır.

### <a name="reminders-are-off"></a>Anımsatıcılar kapalı

| Ayar | Değer |
|---------|---------|
|Bir cihazın yeniden başlatılmasından önceki son tarihten sonra geçen süreyi belirtin (dakika)|180|
|Bir cihaz yeniden başlatılmadan önce kullanıcıya son geri sayım bildirimi sunulırken geçen süreyi belirtin (dakika)|60|
|Son tarihten sonra, bir cihaz yeniden başlatılmadan önce kullanıcıya sunulan anımsatıcı bildirimlerinin sıklığını belirtin (dakika)|240|
|Bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin|No|

Bu cihaz, dağıtım son tarihinden sonra üç saat (**180** dakika) yeniden başlatılır. Bir saat (**60** dakika) yeniden başlatılmadan önce, Kullanıcı kapamayabileceği veya geri erteledikleri bir geri sayım görür. İlk anımsatıcı bildirimi, yeniden başlatmanın ardından olan son tarihten sonra dört saat (**240** dakika) başlayacak şekilde ayarlanır. Böylece Kullanıcı herhangi bir anımsatıcı görmez.

### <a name="low-reminder-frequency"></a>Düşük anımsatma sıklığı

| Ayar | Değer |
|---------|---------|
|Bir cihazın yeniden başlatılmasından önceki son tarihten sonra geçen süreyi belirtin (dakika)|7200|
|Bir cihaz yeniden başlatılmadan önce kullanıcıya son geri sayım bildirimi sunulırken geçen süreyi belirtin (dakika)|120|
|Son tarihten sonra, bir cihaz yeniden başlatılmadan önce kullanıcıya sunulan anımsatıcı bildirimlerinin sıklığını belirtin (dakika)|900|
|Bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin|Yes|

Bu cihaz, dağıtım son tarihinden sonra beş gün (**7200** dakika) yeniden başlatılır. İki saat (**120** dakika) yeniden başlatılmadan önce, Kullanıcı kapatılamadıklarında veya uyku bir geri sayım görür. Bu yapılandırma, 118 saatin anımsatıcıları () göstermesini sağlar `(7200 - 120) / 60` . 15 saat (**900** dakika) son tarihten sonra, yazılım merkezi ilk anımsatıcıyı görüntüler. 15 saatte bir en fazla 6 ek anımsatıcı görüntüler (**900 dakika**). Kullanıcı, anımsatıcıyı birkaç saniye içinde bir bildirim yerine ekranda bir pencere olarak görür.

### <a name="high-reminder-frequency"></a>Yüksek anımsatıcı sıklığı

| Ayar | Değer |
|---------|---------|
|Bir cihazın yeniden başlatılmasından önceki son tarihten sonra geçen süreyi belirtin (dakika)|2880|
|Bir cihaz yeniden başlatılmadan önce kullanıcıya son geri sayım bildirimi sunulırken geçen süreyi belirtin (dakika)|60|
|Son tarihten sonra, bir cihaz yeniden başlatılmadan önce kullanıcıya sunulan anımsatıcı bildirimlerinin sıklığını belirtin (dakika)|30|
|Bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin|Yes|

Cihaz, dağıtım son tarihinden sonra iki günü (**2880** dakika) yeniden başlatır. Bir saat (**60** dakika) yeniden başlatılmadan önce, Kullanıcı kapamayabileceği veya geri erteledikleri bir geri sayım görür. Bu yapılandırma, 47 saatin anımsatıcıları () göstermesini sağlar `(2880 - 60) / 60` . son tarihten **30** dakika sonra yazılım merkezi ilk anımsatıcıyı görüntüler. Her **30 dakikada**bir en fazla 92 ek anımsatıcı görüntüler. Kullanıcı, anımsatıcıyı birkaç saniye içinde bir bildirim yerine ekranda bir pencere olarak görür.

## <a name="device-restart-notifications-version-1902"></a>Cihaz yeniden başlatma bildirimleri (sürüm 1902)

<!--3555947-->
Bazen kullanıcılar, bir yeniden başlatma veya gerekli dağıtım hakkındaki Windows bildirim bildirimini görmez. Ardından, anımsatıcıyı erteleme deneyimini görmez. Bu davranış, istemci son tarihe ulaştığında kötü bir kullanıcı deneyimine yol açabilir.

Sürüm 1902 ' den başlayarak, yazılım değişiklikleri gerektiğinde veya dağıtımların yeniden başlatılması gerektiğinde, daha zorlayıcı bir iletişim kutusu penceresi kullanma seçeneğiniz vardır.

[Bilgisayar yeniden başlatma](#client-settings) istemci ayarları grubunda, aşağıdaki seçeneği etkinleştirin: **bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin**.  

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

## <a name="log-files"></a>Günlük dosyaları

Cihaz yeniden başlatmalarının sorunlarını gidermek için istemcideki **Rebootcoordinator. log** ve **SCNotify. log** dosyalarını kullanın. Belirli dağıtım türüne göre, ek istemci [günlük dosyalarını](../../plan-design/hierarchy/log-files.md)da kullanmanız gerekebilir.

## <a name="next-steps"></a>Sonraki adımlar

- [İstemci ayarlarını yapılandırma](configure-client-settings.md)
- [Uygulama dağıtımı **Kullanıcı deneyimi** ayarları](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Gerekli uygulama dağıtımları için Kullanıcı bildirimleri](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
