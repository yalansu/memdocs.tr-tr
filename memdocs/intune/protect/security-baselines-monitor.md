---
title: Microsoft Intune-Azure 'da güvenlik temellerinin başarısını veya başarısızlığını denetleyin | Microsoft Docs
description: Microsoft Intune MDM 'deki kullanıcılara ve cihazlara güvenlik temelleri dağıtımında hata, çakışma ve başarı durumunu denetleyin. Bkz. istemci günlüklerini kullanarak sorun giderme ve Intune 'daki rapor özellikleri.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
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
ms.openlocfilehash: 6623afcce55c6598ed69fdb78d35235e0fd39dc5
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815383"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Microsoft Intune 'de güvenlik temellerini ve profillerini izleme

Intune, güvenlik temellerini izlemek için çeşitli seçenekler sağlar. Seçenekleriniz şunlardır:

- Bir güvenlik taban çizgisini ve önerilen değerler ile eşleşen (veya eşleşmeyen) cihazları izleyin.
- Kullanıcılarınız ve cihazlarınız için geçerli olan güvenlik temelleri profilini izleyin.
- Seçili bir profildeki ayarların seçili bir cihazda nasıl ayarlandığını görüntüleyin.

Ayrıca, güvenlik temellerini içeren tek tek cihazlar için uygulanan *uç nokta güvenlik yapılandırmalarının* da görüntüleyebilirsiniz.

Özelliği hakkında daha fazla bilgi için bkz. [Intune 'Da güvenlik temelleri](security-baselines.md).

## <a name="monitor-the-baseline-and-your-devices"></a>Taban çizgisini ve cihazlarınızı izleyin

Bir taban çizgisini izlerken, Microsoft 'un önerilerine bağlı olarak cihazlarınızın güvenlik durumu hakkında öngörüler elde edersiniz. Bu öngörüleri görüntülemek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın, **uç nokta güvenlik**  >  **güvenliği temelleri** ' ne gidin ve *MDM güvenlik temeli*gibi bir güvenlik temeli türü seçin. Ardından, *sürümler* bölmesinden, ayrıntılarını görüntülemek istediğiniz profil örneğini seçin ve *genel bakış* bölmesini açın. 

*Genel bakış* bölmesinde seçili taban çizgisi için iki durum görünümü görüntülenir:

- **Güvenlik temeli duruşunu** grafiği-bu grafik, taban çizgisi sürümü için cihaz durumuyla ilgili üst düzey ayrıntıları görüntüler. Kullanılabilir Ayrıntılar:
  - **Varsayılan taban çizgisiyle eşleşir** – bu durum, bir cihaz yapılandırmasının varsayılan (değiştirilmemiş) taban çizgisi yapılandırmasıyla ne zaman eşleştiğini tanımlar.
  - **Özel ayarlarla eşleşir** – bu durum, bir cihaz yapılandırmasının dağıttığınız taban çizgisinin özelleştirilmiş sürümüyle eşleşip eşleşmediğini tanımlar. 
  - **Yanlış yapılandırılmış** – bu durum, bir cihazdan üç durum koşullarını temsil eden bir toplu hatadır: *hata*, *bekleyen*veya *Çakışma*. Bu ayrı durumlar, bu grafiğin altında görüntülenen bir liste görünümü olan *kategoriye göre güvenlik temeli*geri görüntüsü gibi diğer görünümlerde kullanılabilir.
  - **Uygulanamaz** -bu durum, ilkeyi alamayacak bir cihazı temsil eder. Örneğin, ilke Windows 'un en son sürümüne özgü bir ayarı güncelleştirir, ancak cihaz bu ayarı desteklemeyen daha eski (eski) bir sürümünü çalıştırır. 

- **Kategoriye göre güvenlik temeli** gözden hakkı-cihaz durumunu kategoriye göre görüntüleyen bir liste görünümüdür. Bu liste görünümünde, *güvenlik temeli duruşunu* grafiğiyle aynı Ayrıntılar mevcuttur. Bununla birlikte, yanlış yapılandırılan durum durumları için, *yanlış yapılandırılmış* bir yerine üç sütun görürsünüz:

  - **Hata**: ilke uygulanamadı. Bu ileti, genellikle bir açıklamaya bağlantı veren bir hata kodu görüntüler.
  - **Çakışma**: aynı cihaza iki ayar uygulanır ve Intune çakışmayı sıralayamazsınız. Yöneticinin gözden geçirmesi gerekir.
  - **Bekliyor**: cihaz, ilkeyi henüz alacak şekilde Intune ile iade edilmedi.
 
Önceki iki görünümde ayrıntıya indığınızda, ayar durumu ve cihaz durum listesi görünümleri için aşağıdaki ayrıntıları görüntüleyebilirsiniz:

- **Başarılı**: ilke uygulandı.
- **Hata**: ilke uygulanamadı. Bu ileti, genellikle bir açıklamaya bağlantı veren bir hata kodu görüntüler.
- **Çakışma**: aynı cihaza iki ayar uygulanır ve Intune çakışmayı sıralayamazsınız. Yöneticinin gözden geçirmesi gerekir.
- **Bekliyor**: cihaz, ilkeyi henüz alacak şekilde Intune ile iade edilmedi.
- **Uygulanamaz**: cihaz ilkeyi alamıyor. Örneğin, ilke Windows 'un en son sürümüne özgü bir ayarı güncelleştirir, ancak cihaz bu ayarı desteklemeyen daha eski (eski) bir sürümünü çalıştırır.

*Sürüm* görünümünden **cihaz durumu**' nu seçebilirsiniz. Cihaz durumu görünümü bu temeli alan cihazların listesini görüntüler ve aşağıdaki ayrıntıları içerir:
- *Kullanıcı asıl adı* -bu, cihazdaki taban çizgisiyle ilişkili kullanıcı profilini görüntüler. 
- *GÜVENLIK temelı POSTURE* -bu sütunda cihazların durumu görüntülenir:
  - **Başarılı**: ilke uygulandı.
  - **Hata**: ilke uygulanamadı. Bu ileti, genellikle bir açıklamaya bağlantı veren bir hata kodu görüntüler.
  - **Çakışma**: aynı cihaza iki ayar uygulanır ve Intune çakışmayı sıralayamazsınız. Yöneticinin gözden geçirmesi gerekir.
  - **Bekliyor**: cihaz, ilkeyi henüz alacak şekilde Intune ile iade edilmedi.
  - **Uygulanamaz**: cihaz ilkeyi alamıyor. Örneğin, ilke Windows 'un en son sürümüne özgü bir ayarı güncelleştirir, ancak cihaz bu ayarı desteklemeyen daha eski (önceki) bir sürümünü çalıştırır
- *Son Iade etme* durumu cihazdan en son alındığı zaman.

> [!TIP]  
> İlk olarak bir taban çizgisi atadıktan sonra verilerin görünmesi 24 saate kadar sürer. Sonraki değişikliklerin görünmesi altı saate kadar sürer.

## <a name="monitor-the-profile"></a>Profili izleme

Profili izlemek, cihazlarınızın dağıtım durumuna ilişkin öngörüler sağlar, ancak temel önerilere göre güvenlik durumunu etkilemez.

1. Intune 'da, **uç nokta güvenlik**  >  **güvenliği temelleri**' ni seçin, *MDM güvenlik temeli gibi bir güvenlik taban çizgisi türü seçin*,  >  *Bu taban çizgisi özelliklerinin bir örneğini seçin*  >  **Properties**.

2. Taban çizgisinin *özelliklerinde* , detaya git ' i **genişletin ve** temel çizgi için bu örnek için yapılandırma dahil olmak üzere tüm ayarlar kategorilerini ve tek tek ayarları görüntüleyin.

   ![Ayarlar görünümünü gösteren ekran görüntüsü](./media/security-baselines-monitor/manage-settings.png)

3. Her bir cihazda profilin dağıtım durumunu, her bir kullanıcının durumunu ve taban çizgisinin örneğinden ayarların durumunu görüntülemek için **izleyici** seçeneklerini kullanın:

   ![Güvenlik temelleri profili için farklı izleyici seçeneklerine bakın](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="resolve-conflicts-for-security-baselines"></a>Güvenlik temelleri için çakışmaları çözme

Güvenlik taban çizgisi profillerinizin veya uç nokta Güvenlik ilkelerinizin ayarları için bir çakışmayı veya sorunu çözmeye yardımcı olması için, bir cihazın **uç nokta güvenlik yapılandırmasını** görüntüleyin.  Bu cihaz tabanlı görünüm, profillerinizin ve ilkelerinizin, çakışma veya hata durumunu belirten ayarları içerdiğini belirlemenize yardımcı olur. 

Microsoft Endpoint Manager Yönetim Merkezi 'nin içinden iki yol aracılığıyla çakışma veya hata içindeki ayarlar hakkında bilgi alabilirsiniz:

- **Uç nokta güvenliği**  >  **Güvenlik temelleri**  >  *bir taban çizgisi türü seçin*  >  **Profiller**  >  *bir taban çizgisi örneği seçin*  >  **Cihaz durumu**  >  **Uç nokta güvenlik yapılandırması**  >  *bir çakışmayı veya hataları gösteren ayarlar*.
- **Cihazlar**  >  *bir cihaz seçin*  >  **Uç nokta güvenlik yapılandırması**  >  *bir profil veya taban çizgisi seçin*  >  *bir çakışma veya hata gösteren ayarlar listesinden bir ayar seçin*.

Bir cihazın **uç nokta güvenlik yapılandırması** görünümünde, Intune her bir temel profilini ve bu cihaza atanan uç nokta güvenliği ilkesini görüntüler. Bu görünüm Ayrıca, her giriş için ilişkili kullanıcı asıl adını ve temel profil ya da ilkenin durumunu tanımlar. Bir profil veya ilke, onunla ilişkilendirilen her farklı Kullanıcı asıl adı için bir cihazda birden çok kez görünebilir. 

<!-- pending
The **Baseline status** represents the worst available status from any applicable setting in that profile or policy. For example, if on the device a single setting from a profile is found to be in conflict while the rest of the baselines’ settings are successful, the *Baseline status* is set to *Conflict*. 

The available status from best to worst:

- **Success** - The setting on the device matches the value as configured in the profile, and there are no conflicting configurations. This is either a default and recommended value, or a custom value specified by an administrator when the profile was configured.
- **Error** - The profile and settings failed to apply.
- **Conflict** - The setting conflicts with another instance of the setting from another policy, has an error, or is pending an update. This setting isn’t sent to the device until the conflict is resolved.
--> 

### <a name="drill-in-to-identify-and-resolve-conflicts"></a>Çakışmaları belirlemek ve çözmek için detaya git

1. Bir cihazın uç nokta güvenlik yapılandırmasını görüntülerken, çakışma veya hata durumuyla sonuçlanan sorun hakkında daha fazla bilgi edinmek için detaya gitmeyi istediğiniz bir profil seçin.

   Detaya gitme sırasında, Intune, *yapılandırılmamış*olarak ayarlanmamış her ayarı ve bu ayarın durumunu içeren bu profil için ayarların bir listesini görüntüler. Görüntü kategoriye, ayar adına veya duruma göre düzenlenebilir. Durum üzerinde filtrelemeniz durumunda yalnızca hata veya çakışma olan ayarlara hızlıca odaklanırsınız.  

2. Belirli bir ayar hakkındaki ayrıntıları görüntülemek için, **ayarları seçerek ayarlar Ayrıntılar** bölmesini açın. Bu bölmede şunları göreceksiniz:
   - Ayar: ayarın adı.
   - Durum: cihazdaki ayarın durumu. 
   - Kaynak profili: Bu, aynı ayarı ve farklı bir değerle yapılandıran her bir uç nokta Güvenlik profilinin veya güvenlik temelinin bir listesidir.

   > [!TIP]  
   > Cihaz yapılandırma profillerinin aksine, uç nokta güvenlik profilleri hata kodları veya ilgili ayrıntıları sağlamaz.

3. Çakışan profilleri yeniden yapılandırmak için, profil yapılandırmasının bir görünümünü açmak üzere **kaynak profili** listesinden bir kayıt seçin. Profilin yapılandırma görünümünden, çakışmayı kaldırmak için bu profildeki ayarları gözden geçirebilir ve düzenleyebilirsiniz.

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Bir cihaza uygulanan profillerdeki ayarları görüntüleyin

Bir güvenlik temeli için bir profil seçebilir ve bu profildeki ayarların bir listesini, tek bir cihaza uygulanan şekilde görüntülemek için detaya gidebilirsiniz.  Bu listeyi görüntülemek için **uç nokta güvenlik**  >  **güvenliği temellerine**detaya git  >  *güvenlik temeli türünü seçin*  >  *select the Profile you want to view*  >  **cihaz durumunu**görüntülemek istediğiniz profili seçin. Ayrıca, **uç nokta güvenliği**  >  **tüm cihazlar**  >  *cihaz Seç*  >  **uç noktası güvenlik yapılandırması**' na giderek listeyi görüntüleyebilirsiniz  >  *bir temel sürüm seçin*.

Bir cihaz seçildikten sonra, Microsoft Endpoint Manager Yönetim Merkezi, bu profildeki ayarların bulunduğu kategoriyi ve cihazdaki yapılandırma durumunu içeren ayarların bir listesini görüntüler. Yapılandırma durumları aşağıdaki değerleri içerir:

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


