---
title: Microsoft Intune-Azure 'da güvenlik temellerinin başarısını veya başarısızlığını denetleyin | Microsoft Docs
description: Microsoft Intune MDM 'deki kullanıcılara ve cihazlara güvenlik temelleri dağıtımında hata, çakışma ve başarı durumunu denetleyin. Bkz. istemci günlüklerini kullanarak sorun giderme ve Intune 'daki rapor özellikleri.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ccf9801c7a5977485c6c1864a69be2e46a4af55
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914880"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Microsoft Intune 'de güvenlik temellerini ve profillerini izleme

Intune, güvenlik temellerinizi izlemek için çeşitli seçenekler sunar. Seçenekleriniz şunlardır:

- Bir güvenlik taban çizgisini ve önerilen değerler ile eşleşen (veya eşleşmeyen) cihazları izleyin.
- Kullanıcılarınız ve cihazlarınız için geçerli olan güvenlik temelleri profilini izleyin.
- Seçili bir profildeki ayarların seçili bir cihazda nasıl ayarlandığını görüntüleyin.

Ayrıca, güvenlik temellerini içeren tek tek cihazlar için uygulanan *uç nokta güvenlik yapılandırmalarının* da görüntüleyebilirsiniz.

Bu makalede, bu izleme seçeneklerinde izlenecek yol gösterilmektedir.

[Intune 'Daki güvenlik temelleri](security-baselines.md) Microsoft Intune içindeki güvenlik temelleri özelliği hakkında daha fazla bilgi sağlar.

## <a name="monitor-the-baseline-and-your-devices"></a>Taban çizgisini ve cihazlarınızı izleyin

Bir taban çizgisini izlerken, Microsoft 'un önerilerine bağlı olarak cihazlarınızın güvenlik durumu hakkında öngörüler elde edersiniz. Bu öngörüleri görüntülemek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın, **uç nokta güvenlik**  >  **güvenliği temelleri** ' ne gidin ve *MDM güvenlik temeli*gibi bir güvenlik temeli türü seçin. Ardından, *profil* bölmesinde, ayrıntılarını görüntülemek istediğiniz profil örneğini seçin. Bu, daha sonra *izleyici* bölümünde profil raporlarının hiçbirini seçebileceğiniz profiller *Özellikler* Bölmesi ' ni açar. 

İlk olarak bir taban çizgisi atadıktan sonra verilerin görünmesi 24 saate kadar sürer. Sonraki değişikliklerin görünmesi altı saate kadar sürer.

Raporların ve cihazların detayına göre, çeşitli ayrıntılar mevcuttur.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Profili izleme

Profili izlemek, cihazlarınızın dağıtım durumuna ilişkin öngörüler sağlar, ancak temel önerilere göre güvenlik durumunu etkilemez.

1. Intune 'da **güvenlik temelleri** ' ni seçin > *profiller* bölmesini açmak için bir taban çizgisi seçin.

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. Özellikleri **Yönet**altında  >  **Properties**, taban çizgisinde tüm ayarların bir listesi gösterilir. Ayrıca, bu ayarlardan herhangi birini değiştirebilirsiniz:

   ![Güvenlik temelleri profilindeki ayarları görme ve güncelleştirme](./media/security-baselines-monitor/manage-settings.png)

4. **İzleyici**' de, her bir cihazda profilin dağıtım durumunu, her bir kullanıcının durumunu ve her bir ayarın durumunu Baseline olarak görebilirsiniz:

   ![Güvenlik temelleri profili için farklı izleyici seçeneklerine bakın](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Bir cihaza uygulanan profillerdeki ayarları görüntüleyin

Bir güvenlik temeli için bir profil seçebilir ve bu profildeki ayarların bir listesini, tek bir cihaza uygulanan şekilde görüntülemek için detaya gidebilirsiniz.  Bu listeyi görüntülemek için **uç nokta güvenlik**  >  **güvenliği temellerine**detaya git  >  *güvenlik temeli türünü seçin*  >  *select the Profile you want to view*  >  **cihaz durumunu**görüntülemek istediğiniz profili seçin. Ayrıca, **uç nokta güvenliği**  >  **tüm cihazlar**  >  *cihaz Seç*  >  **uç noktası güvenlik yapılandırması**' na giderek listeyi görüntüleyebilirsiniz  >  *bir temel sürüm seçin*.

Bir cihaz seçildikten sonra, Microsoft Endpoint Manager Yönetim Merkezi, ayarın kimden olduğu kategori ve cihazdaki yapılandırma durumu dahil olmak üzere bu profildeki ayarların bir listesini görüntüler. Yapılandırma durumları aşağıdaki değerleri içerir:

- **Başarılı** – cihazdaki ayar, profilde yapılandırılan değerle eşleşir. Bu, varsayılan temel değer ve önerilen değer ya da profil yapılandırıldığında yönetici tarafından belirtilen özel bir değerdir.
- **Çakışma** – Bu ayar başka bir ilkeyle çakışıyor, bir hata içeriyor veya güncelleştirme bekliyor.
- **Uygulanamaz** – ayar profil tarafından uygulanmaz.

> [!NOTE]
> Daha ayrıntılı bilgiler sağlamak için, ayarlar için durum değerleri gelecek bir sürümde güncellenecektir.

## <a name="view-endpoint-security-configurations-per-device"></a>Cihaz başına uç nokta güvenlik yapılandırmasını görüntüle

Tek bir cihaza uygulanan güvenlik yapılandırmalarının ayrıntılarını görüntüleyin ve bu, yanlış yapılandırılmış ayarları yalıtmanıza yardımcı olabilir.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazlar**  >  **tüm cihazlar** ' a gidin ve görüntülemek istediğiniz cihazı seçin.

3. *İzleyici* kategorisinde, bu cihaza uygulanan güvenlik yapılandırmalarının listesini görüntülemek Için **uç nokta güvenlik yapılandırması** ' nı seçin.

4. Detaya gitmek için bir uç nokta güvenlik yapılandırması seçebilir ve cihazdaki bu güvenlik yapılandırmasının değerlendirmesiyle ilgili ek ayrıntıları görüntüleyebilirsiniz.

## <a name="troubleshoot-using-per-setting-status"></a>Ayar başına durumu kullanarak sorun giderme

Bir güvenlik temeli dağıttıysanız, ancak dağıtım durumu bir hata gösterir. Aşağıdaki adımlar, hatayı gidermeye yönelik bazı yönergeler sağlar.

1. Intune 'da **güvenlik temelleri** ' ni seçin > bir temel > **profili**seçin.

2. **Monitor**  >  **Ayar başına ayarla durumu**altında bir profil > seçin.

3. Tabloda tüm ayarlar ve her ayarın durumu gösterilmektedir. Hataya neden olan ayarı görmek için **hata** sütununu veya **Çakışma** sütununu seçin.

### <a name="mdm-diagnostic-information"></a>MDM tanılama bilgileri

Artık sorunlu ayarı öğrenmiş oldunuz. Bir sonraki adım, bu ayarın neden bir hata veya çakışmaya neden olduğunu bulmadır.

Windows 10 cihazlarında, yerleşik bir MDM tanılama bilgileri raporu vardır. Bu rapor varsayılan değerleri, geçerli değerleri, ilkeyi listeler, cihaza veya kullanıcıya dağıtılıp dağıtılmadığını gösterir ve daha fazlasını içerir. Ayarın bir çakışmaya veya hataya neden neden olduğunu belirlemenize yardımcı olması için bu raporu kullanın.

1. Cihazda **Ayarlar**  >  **hesaplar**  >  **iş veya okul erişimi**' ne gidin.

2. > **bilgi**  >  **Gelişmiş tanılama raporu**  >  **rapor oluştur**hesabını seçin.

3. **Dışarı aktar**' ı seçin ve oluşturulan dosyayı açın.

4. Raporda, raporun farklı bölümlerinde hata veya çakışma ayarını bulun.

  Örneğin, **kayıtlı yapılandırma kaynakları ve hedef kaynaklar** bölümüne veya **yönetilmeyen ilkeler** bölümüne bakın. Neden bir hata veya çakışmaya neden olduğuna ilişkin bir fikir alabilirsiniz.

[Windows 10 ' da MDM başarısızlıklarını tanılama](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) bu yerleşik rapor hakkında daha fazla bilgi sağlar.

> [!TIP]
>
> - Bazı ayarlar GUID 'YI de listeler. Herhangi bir küme değeri için yerel kayıt defterinde (regedit) Bu GUID için arama yapabilirsiniz.
> - Olay Görüntüleyicisi Günlükler, sorunlu ayara (**Olay Görüntüleyicisi**  >  **Uygulamaları ve hizmet günlükleri**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostics-Provider**  >  **admin**) ilişkin bazı hata bilgilerini de içerebilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Güvenlik temelleri hakkında bilgi edinin](security-baselines.md)
- [Çakışmaları önleyin](security-baselines.md#avoid-conflicts)
- [Cihaz profillerini izleme](../configuration/device-profile-monitor.md) 
- [Yaygın sorunlar ve çözümleri](../configuration/device-profile-troubleshoot.md).
- [Intune'da ilke ve profil sorunları giderme](../configuration/troubleshoot-policies-in-microsoft-intune.md)