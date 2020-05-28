---
title: Desktop Analytics sorunlarını giderme
titleSuffix: Configuration Manager
description: Masaüstü analiziyle ilgili sorunları gidermenize yardımcı olacak teknik ayrıntılar.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 69694fa39375daf436abf59fcd48edda41a9fc62
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268258"
---
# <a name="troubleshoot-desktop-analytics"></a>Desktop Analytics sorunlarını giderme

Configuration Manager ile tümleştirilmiş masaüstü analiziyle ilgili sorunları gidermenize yardımcı olması için bu makaledeki ayrıntıları kullanın.

## <a name="confirm-prerequisites"></a>Önkoşulları Onayla

Yaygın olarak karşılaşılan çoğu sorun eksik önkoşullardan kaynaklanır. Önce aşağıdaki konfigürasyonları onaylayın:

- [Önkoşullar](overview.md#prerequisites)  

- [Windows bileşen güncelleştirmeleri](enroll-devices.md#update-devices)  

- Aşağıdaki konuları kapsayan [veri paylaşımını etkinleştirme](enable-data-sharing.md):  

  - İstemcilerin bağlanması gereken Internet uç noktaları  

  - Proxy sunucusu kimlik doğrulaması  

  - Tanılama veri düzeyleri  

## <a name="monitor-connection-health"></a>Bağlantı durumunu izleme

Cihaz sistem durumu kategorilerine göre detaya gitmek için Configuration Manager 'deki **bağlantı sistem durumu** panosunu kullanın. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Masaüstü Analizi bakım** düğümünü genişletin ve **bağlantı sistem durumu** panosunu seçin.  

Daha fazla bilgi için bkz. [bağlantı durumunu izleme](monitor-connection-health.md).

> [!NOTE]
> Masaüstü analizine Configuration Manager bağlantısı, hizmet bağlantı noktası üzerine bağımlıdır. Bu site sistemi rolündeki değişiklikler, bulut hizmetiyle eşitlemeyi etkileyebilir. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

Sürüm 2002 ' den başlayarak, Configuration Manager site bir bulut hizmeti için gerekli uç noktalara bağlanamazsa, kritik bir durum ileti KIMLIĞI 11488 oluşturur. Hizmete bağlanamadığınızda SMS_SERVICE_CONNECTOR bileşen durumu kritik olarak değişir. Configuration Manager konsolunun [Bileşen durumu](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) düğümünde ayrıntılı durumu görüntüleyin.<!-- 5566763 -->

## <a name="log-files"></a>Günlük dosyaları

Daha fazla bilgi için bkz. [Masaüstü Analizi Için günlük dosyaları](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

Configuration Manager sürüm 1906 ' den başlayarak, Configuration Manager install dizininden masaüstü Analizi sorunlarını gidermeye yardımcı olması için **DesktopAnalyticsLogsCollector. ps1** aracını kullanın. Bazı temel sorun giderme adımlarını çalıştırır ve ilgili günlükleri tek bir çalışma dizininde toplar. Daha fazla bilgi için bkz. [Günlükler toplayıcısı](log-collector.md).

### <a name="enable-verbose-logging"></a>Ayrıntılı günlük kaydını etkinleştir

1. Hizmet bağlantı noktasında aşağıdaki kayıt defteri anahtarına gidin:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. **LoggingLevel** değerini olarak ayarlayın`0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a>Azure AD uygulamaları

Masaüstü Analizi aşağıdaki uygulamaları Azure AD 'nize ekler:

- **Configuration Manager Mikro hizmeti**: Configuration Manager, masaüstü analiziyle bağlanır. Bu uygulamanın erişim gereksinimi yok.  

- **MALogAnalyticsReader**: günlük anlık görüntünün başarıyla kopyalandığından emin olmak için Azure Log Analytics çalışma alanınızı izler. Daha fazla bilgi için bkz. [MALogAnalyticsReader uygulama rolü](#bkmk_MALogAnalyticsReader).  

- **Office365 Istemci Yöneticisi**: Masaüstü analizinden dağıtım planı bilgilerinin ve cihaz hazırlık durumunun Configuration Manager alınmasına izin vermez.

Kurulumu tamamladıktan sonra bu uygulamaları sağlamanız gerekiyorsa, **bağlı hizmetler** bölmesine gidin. **Kullanıcılar ve uygulamalar erişimini yapılandır**' ı seçin ve uygulamaları sağlayın.  

- **Configuration Manager Için Azure AD uygulaması**. Kurulumu tamamladıktan sonra bağlantı sorunlarını sağlamanız veya sorun gidermeniz gerekiyorsa, bkz. [Configuration Manager için uygulama oluşturma ve içeri aktarma](#create-and-import-app-for-configuration-manager). Bu uygulama, **Configuration Manager Service** API 'SINDEKI **Write cm koleksiyon VERISI** ve **okuma cm koleksiyon verilerini** gerektirir.  

### <a name="create-and-import-app-for-configuration-manager"></a>Configuration Manager için uygulama oluşturma ve içeri aktarma

Azure hizmetlerini Yapılandırma Sihirbazı 'ndan Configuration Manager için Azure AD uygulamasını oluşturamaz veya mevcut bir uygulamayı yeniden kullanmak istiyorsanız, el ile oluşturmanız ve içeri aktarmanız gerekir. Masaüstü Analizi portalında [ilk ekleme](set-up.md#initial-onboarding) işlemini tamamladıktan sonra aşağıdaki adımları kullanın:

#### <a name="create-app-in-azure-ad"></a>Azure AD 'de uygulama oluşturma

1. [Azure Portal](https://portal.azure.com) , *genel yönetici* izinlerine sahip bir kullanıcı olarak açın, **Azure Active Directory**' e gidin ve **uygulama kayıtları**' yı seçin. Sonra **Yeni kayıt**' ı seçin.  

2. **Oluştur** panelinde aşağıdaki ayarları yapılandırın:  

    - **Ad**: uygulamayı tanımlayan benzersiz bir ad, örneğin:`Desktop-Analytics-Connection`  

    - **Desteklenen hesap türleri**: **yalnızca bu kuruluş dizinindeki hesaplar (contoso)**

    - **Yeniden yönlendirme URI 'si (isteğe bağlı)**: **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    **Kaydol**’u seçin.  

3. Uygulamayı seçin, **uygulamanın (istemci) kimliğini** ve **Dizin (kiracı) kimliğini**aklınızda yapın. Değerler, Configuration Manager bağlantısını yapılandırmak için kullanılan GUID 'lerdir.  

4. **Yönet** menüsünde **Sertifikalar & parolaları**' nı seçin. **Yeni istemci gizli dizisi**’ni seçin. Bir **Açıklama**girin, bir sona erme süresi belirtin ve ardından **Ekle**' yi seçin. Configuration Manager bağlantısını yapılandırmak için kullanılan anahtarın **değerini** kopyalayın.

    > [!Important]  
    > Bu, anahtar değerini kopyalamak için tek fırsattır. Şimdi kopyalayamazsınız, başka bir anahtar oluşturmanız gerekir.  
    >
    > Anahtar değerini güvenli bir konuma kaydedin.  

5. **Yönet** menüsünde, **API izinleri**' ni seçin.  

    1. **API izinleri** panelinde **izin Ekle**' yi seçin.  

    2. **API Izinleri iste** panelinde **Kuruluşumun kullandığı API**'lere geçin.  

    3. **Configuration Manager Mikro hizmet** API 'sini arayın ve seçin.  

    4. **Uygulama izinleri** grubunu seçin. **Cmcollectiondata**öğesini genişletin ve şu izinlerden her ikisini de SEÇIN: **cm koleksiyon VERILERINI yazın** ve **cm koleksiyon verilerini okuyun**.  

    5. **Izin Ekle**' yi seçin.  

6. **API izinleri** panelinde **yönetici izni ver...** seçeneğini belirleyin. **Evet**' i seçin.  

#### <a name="import-app-in-configuration-manager"></a>Uygulamayı Configuration Manager içeri aktar

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin. Şeritte **Azure hizmetlerini yapılandır** ' ı seçin.  

2. Azure Hizmetleri Sihirbazı 'nın **Azure hizmetleri** sayfasında, aşağıdaki ayarları yapılandırın:  

    - Configuration Manager nesne için bir **ad** belirtin.  

    - Hizmeti tanımlamanızı sağlayacak isteğe bağlı bir **Açıklama** belirtin.  

    - Kullanılabilir hizmetler listesinden **Masaüstü Analizi** ' ni seçin.  
  
   **İleri**’yi seçin.  

3. **Uygulama** sayfasında, uygun **Azure ortamını**seçin. Ardından Web uygulaması için **Içeri aktar** ' ı seçin. **Uygulamaları Içeri aktar** penceresinde aşağıdaki ayarları yapılandırın:  

    - **Azure AD kiracı adı**: Bu ad, Configuration Manager nasıl adlandırıldığını  

    - **Azure AD KIRACı kimliği**: Azure AD 'Den KOPYALADıĞıNıZ **dizin kimliği**  

    - **ISTEMCI kimliği**: Azure AD uygulamasından KOPYALADıĞıNıZ **uygulama kimliği**  

    - **Gizli anahtar**: Azure AD uygulamasından kopyaladığınız anahtar **değeri**  

    - **Gizli anahtar süre sonu**: anahtarın aynı süre sonu tarihi  

    - **Uygulama kimliği URI 'si**: Bu ayar otomatik olarak aşağıdaki değerle doldurulur:`https://cmmicrosvc.manage.microsoft.com/`  
  
   **Doğrula**' yı seçin ve ardından **Tamam** ' ı seçerek uygulamaları içeri aktar penceresini kapatın. Azure hizmetleri sihirbazının uygulama sayfasında **İleri ' yi** seçin.  

Sihirbazın geri kalanını **Tanılama verileri** sayfasında devam ettirmek için bkz. [hizmete bağlanma](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Configuration Manager 'de uygulama sorunlarını giderme

Uygulamayı oluştururken veya içeri aktarırken sorun yaşıyorsanız, önce belirli bir hata için **Smsadminuı. log dosyasına** bakın. Ardından aşağıdaki konfigürasyonları kontrol edin:

- Kiracıyı masaüstü Analizi hizmetine başarıyla kaydettiniz. Daha fazla bilgi için bkz. [Masaüstü analizlerini ayarlama](set-up.md).

- Tüm gerekli uç noktalara erişilebilir. Daha fazla bilgi için bkz. [uç noktalar](enable-data-sharing.md#endpoints).

- Oturum açan kullanıcının doğru izinlere sahip olduğundan emin olun. Daha fazla bilgi için bkz. [Önkoşullar](overview.md#prerequisites).

- Kullanıcının Azure 'da genel olarak oturum açmasını sağlayın. Bu eylem, genel Azure AD kimlik doğrulama sorunları olup olmadığını belirler.

- **SMS_SERVICE_CONNECTOR** bileşeni Için *Masaüstü Analizi çalışanıyla*ilgili durum iletilerini denetleyin.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a>MALogAnalyticsReader uygulama rolü

Masaüstü analizlerini ayarlarken, kuruluşunuzun adına onay vermiş olursunuz. Bu izin, MALogAnalyticsReader uygulamasını çalışma alanı için Log Analytics okuyucu rolü atamak içindir. Bu uygulama rolü masaüstü analizi için gereklidir.

Kurulum sırasında bu işlemle ilgili bir sorun varsa, bu izni el ile eklemek için aşağıdaki işlemi kullanın:

1. [Azure Portal](https://portal.azure.com)gidin ve **tüm kaynaklar**' ı seçin. **Log Analytics**türünde çalışma alanını seçin.  

2. Çalışma alanı menüsünde **erişim denetimi (IAM)** öğesini seçin ve ardından **Ekle**' yi seçin.  

3. **Izin Ekle** panelinde aşağıdaki ayarları yapılandırın:  

    - **Rol**: **okuyucu**  

    - **Azure AD kullanıcısına, grubuna veya uygulamasına** **erişim atama**  

    - Şunu **seçin**: **MALogAnalyticsReader**  

4. **Kaydet**’i seçin.

Portal, rol atamasını eklediği bir bildirim gösterir.

## <a name="data-latency"></a>Veri gecikme süresi

<!-- 3846531 -->
Masaüstü analizlerini ilk kez ayarladığınızda, yeni istemcileri Kaydet veya yeni dağıtım planlarını yapılandırdığınızda, Configuration Manager ve Masaüstü Analizi portalındaki Raporlar, verilerin tamamını hemen göstermez. Aşağıdaki adımların gerçekleşmesi 2-3 gün sürebilir:

- Etkin cihazlar, tanılama verilerini masaüstü Analizi hizmetine gönderiyor
- Hizmet, verileri işler
- Hizmet Configuration Manager sitesiyle eşitlenir

Cihaz koleksiyonlarını Configuration Manager hiyerarşinizden masaüstü analizine eşitlerken, bu koleksiyonların masaüstü Analizi portalında görünmesi bir saate kadar sürebilir. Benzer şekilde, masaüstü Analizi 'nde bir dağıtım planı oluşturduğunuzda, dağıtım planıyla ilişkili yeni koleksiyonların Configuration Manager hiyerarşinizde görünmesi bir saate kadar sürebilir. Birincil siteler, koleksiyonları oluşturur ve merkezi yönetim sitesi masaüstü analizi ile eşitlenir. Configuration Manager, koleksiyon üyeliğini değerlendirmek ve güncelleştirmek için 24 saate kadar sürebilir. Bu işlemi hızlandırmak için koleksiyon üyeliğini el ile güncelleştirin.<!-- 4984639 -->

> [!Note]
> Değişiklikleri yansıtacak şekilde el ile koleksiyon güncelleştirmeleri için SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker bileşenin ilk eşitlenmesi gerekir. Bu işlemin çalışması bir saate kadar sürebilir. Daha fazla bilgi için **M365ADeploymentPlanWorker. log dosyasına**bakın.

Masaüstü Analizi portalı 'nda iki tür veri vardır: **yönetici verileri** ve **Tanılama verileri**:

- **Yönetici verileri** , çalışma alanı yapılandırmanızda yaptığınız tüm değişiklikleri ifade eder. Örneğin, bir varlığın **yükseltme kararını** veya **önemini** değiştirdiğinizde, yönetici verilerini değiştirirsiniz. Bu değişiklikler genellikle, söz konusu varlığın yüklendiği bir cihazın hazırlık durumunu değiştirebilecek şekilde Birleşik bir etkiye sahiptir.

- **Tanılama verileri** , istemci cihazlarından Microsoft 'a yüklenen sistem meta verilerini ifade eder. Bu veri, masaüstü analizlerini güçlendirir. Cihaz envanteri ve güvenlik ve özellik güncelleştirme durumu gibi öznitelikleri içerir.

Varsayılan olarak, masaüstü Analizi portalındaki tüm veriler her gün otomatik olarak yenilenir. Bu yenileme, tanılama verilerinde ve yapılandırmada yaptığınız değişikliklerle (Yönetici verileri) yapılan değişiklikleri içerir. Bu, masaüstü Analizi portalında her gün 08:00 saat UTC 'ye kadar görünür olmalıdır.

Yönetici verilerinde değişiklik yaptığınızda, çalışma alanınızdaki yönetici verilerinin talep üzerine yenilenmesini tetikleyebilirsiniz. Masaüstü Analizi portalındaki herhangi bir sayfadan, veri para birimi açılır öğesini açın:

![Masaüstü Analizi portalındaki veri para birimi açılır pencere sekmesinin ekran görüntüsü](media/data-currency-flyout.png)

Sonra **Değişiklikleri Uygula**' yı seçin:

![Masaüstü Analizi portalında genişletilmiş veri para birimi açılır ekranının ekran görüntüsü](media/data-currency-flyout-expand.png)

Bu işlem genellikle 15-60 dakika arasında sürer. Zamanlama, çalışma alanınızın boyutuna ve işlem gerektiren değişikliklerin kapsamına bağlıdır. İsteğe bağlı bir veri yenileme isteğinde bulunduğunda, tanılama verilerinde hiçbir değişikliğe neden olmaz.  Daha fazla bilgi için bkz. [Masaüstü ANALIZI SSS](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Yukarıda belirtilen zaman kareleri içinde güncelleştirilmiş değişiklikleri görmüyorsanız, bir sonraki günlük yenileme için 24 saat bekleyin. Daha uzun gecikmeler görürseniz hizmet durumu panosunu kontrol edin. Hizmet sağlıklı olarak bildirirse, Microsoft destek 'e başvurun.<!-- 3896921 -->

> [!IMPORTANT]
> **Son verileri görüntülemek** Için masaüstü Analizi seçeneği kullanım dışıdır. Bu eylem, daha sonraki bir masaüstü Analizi hizmeti sürümünde kaldırılacaktır. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  
