---
title: Microsoft Intune reports
titleSuffix: Microsoft Intune
description: Intune, tutarlı ve zamanında veriler içeren odaklanmış görünümlerle belirli rapor türleri sağlar.
keywords: ''
author: erikre
ms.author: erikre
manager: dougeby
ms.date: 09/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d6c159f775ffbc169f2f91b9cf447f24eaf0df4
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813780"
---
# <a name="intune-reports"></a>Intune raporları
Microsoft Intune raporları, kuruluşunuzdaki uç noktaların sistem durumunu ve etkinliğini daha etkili ve verimli bir şekilde izlemenize olanak tanır ve ayrıca Intune genelinde diğer raporlama verileri sağlar. Örneğin, cihaz uyumluluğu, cihaz sistem durumu ve cihaz eğilimleri hakkındaki raporları görebileceksiniz. Ayrıca, daha belirli verileri almak için özel raporlar da oluşturabilirsiniz. 

> [!NOTE]
> Intune raporlama değişiklikleri, yeni yapıyı hazırlamaya ve uyarlanmanıza yardımcı olmak için bir süre içinde kademeli olarak zaman aşımına uğrar.

Rapor türleri aşağıdaki odak alanlarında düzenlenmiştir:
- **İşletimsel** -odaklanmanıza ve işlem yapmanıza yardımcı olacak, zamanında, hedeflenen verileri sağlar. Yöneticiler, konu uzmanları ve yardım masası bu raporları en yararlı bulacaktır.
- **Kuruluş** -cihaz yönetimi durumu gibi genel bir görünümün daha geniş bir özetini sağlar. Yöneticiler ve Yöneticiler bu raporları en yararlı bulacaktır.
- **Geçmiş** -bir süre boyunca desenler ve eğilimler sağlar. Yöneticiler ve Yöneticiler bu raporları en yararlı bulacaktır.
- **Uzman** -kendi özel raporlarınızı oluşturmak için ham verileri kullanmanıza olanak sağlar. Yöneticiler bu raporları en yararlı bulacaktır.

Raporlama çerçevesi, tutarlı ve daha kapsamlı bir raporlama deneyimi sağlar. Kullanılabilir raporlar aşağıdaki işlevleri sağlar:
- **Arama ve sıralama** : veri kümesinin ne kadar büyük olduğuna bakılmaksızın, her sütunda arama ve sıralama yapabilirsiniz.
- **Veri sayfalaması** : verileri sayfa sayfa veya belirli bir sayfaya atlayarak disk belleğine göre tarayabilirsiniz.
- **Performans** -büyük kiracılardan oluşturulan raporları hızlıca oluşturabilir ve görüntüleyebilirsiniz.
- **Dışarı aktar** – büyük kiracılardan oluşturulan raporlama verilerini hızlıca dışarı aktarabilirsiniz.

### <a name="who-can-access-the-data"></a>Verilere kimler erişebilir?

Aşağıdaki izinlere sahip kullanıcılar günlükleri gözden geçirebilir:

- Genel Yönetici
- Intune Hizmet Yöneticisi
- **Okuma** Izinleriyle bir Intune rolüne atanan yöneticiler

## <a name="non-compliant-devices-report-operational"></a>Uyumlu olmayan cihazlar raporu (Işletimsel)
Uyumlu olmayan cihazlar raporu, sorunları belirlemek ve sorunları düzeltmek için yardım masası veya yönetici rolleri tarafından genellikle kullanılan verileri sağlar. Bu raporda bulunan veriler zamanında, beklenmeyen davranışı çağırır ve eyleme geçmek üzere tasarlanmıştır. Rapor, iş yüküyle birlikte kullanılabilir ve uyumlu olmayan cihazların etkin iş akışlarından göz atarak erişilebilir hale getirilmesi sağlanır. Bu rapor filtreleme, arama, sayfalama ve sıralama özellikleri sağlar. Ayrıca, sorun gidermeye yardımcı olmak için ayrıntıya gidebilirsiniz.

**Uyumsuz cihazlar** raporunu aşağıdaki adımları kullanarak görebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Devices**  >  **Monitor**  >  **Uyumsuz cihazları**izlemek için cihazlar ' ı seçin.

    ![Uyumsuz cihaz raporu](./media/intune-reports/intune-reports-02.png)

    > [!TIP]
    > Intune 'u Azure Portal daha önce kullandıysanız, [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) 'da oturum açarak ve **cihaz uyumluluğu**  >  **uyumlu olmayan cihazlar**' ı seçerek yukarıdaki ayrıntıları Azure Portal bulabilirsiniz.

## <a name="windows-10-unhealthy-endpoints-report-operational"></a>Windows 10 sağlıksız uç noktalar raporu (Işletimsel)
**Windows 10 sağlıksız uç noktalar** , sorunları belirlemek ve sorunları düzeltmeye yardımcı olmak üzere yardım masası veya yönetici rolleri tarafından genellikle kullanılan yüzey verilerini rapor eder. Bu raporda bulunan veriler zamanında, sağlıksız cihaz, birincil kullanıcı asıl adı (UPN) ve bir dizi ayarların durumunu çağırır. Rapor, birincil **Virüsten koruma** iş yükü içinde bir sekme olarak kullanılabilir. Bu rapor filtreleme, arama, sayfalama ve sıralama sağlar. 

**Windows 10 sağlıksız uç noktaları** raporunu aşağıdaki adımları kullanarak görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Endpoint Security**  >  **Virüsten koruma**  >  **Windows 10 sağlıksız uç noktaları**' nı seçin.

## <a name="windows-10-detected-malware-report-operational"></a>Windows 10 algılanan kötü amaçlı yazılım raporu (Işletimsel)
**Windows 10 algılanan kötü amaçlı yazılım** raporu, cihazları kötü amaçlı yazılım sorunlarıyla tanıtmak ve sorunları düzeltmeye yardımcı olmak için veri sağlar. Bu raporda bulunan veriler zamanında, sağlıksız cihaz, Kullanıcı adı ve önem derecesi ' ni çağırır. Rapor, birincil **Virüsten koruma** iş yükü içinde bir sekme olarak kullanılabilir. Bu rapor filtreleme, arama, sayfalama ve sıralama sağlar. 

Aşağıdaki adımları kullanarak, **Windows 10 algılanan kötü amaçlı yazılım** raporunu görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Endpoint Security**  >  **Virüsten koruma**  >  **Windows 10 algılanan kötü amaçlı yazılımları**seçin.

### <a name="bulk-actions-for-devices"></a>Cihazlar için toplu eylemler
**Windows 10 algılanan kötü amaçlı yazılım** raporu, rapor içinde seçilen cihazlar için geçerli olan toplu eylemler sağlar. Toplu bir eylem kullanmak için, her bir cihaza karşılık gelen bir satır seçer (aynı anda en fazla 100 cihaz) ve eylemi seçersiniz. Kullanılabilir eylemler şunlardır:
- **Yeniden Başlat** -bu eylem seçilen cihazların yeniden başlatılmasını gerçekleştirir.
- **Hızlı tarama** -bu eylem, seçilen cihazlarda bir Windows Defender hızlı taraması gerçekleştirir. 
- **Tam tarama** -bu eylem, seçilen cihazların Windows Defender tam taramasını gerçekleştirir. 

*Hızlı tarama* ve *tam tarama*arasındaki fark hakkında daha fazla bilgi için bkz. [Zamanlanmış hızlı veya tam Microsoft Defender virüsten koruma taramaları yapılandırma](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/scheduled-catch-up-scans-microsoft-defender-antivirus).

## <a name="feature-update-failures-report-operational"></a>Özellik Güncelleştirme hatalarının raporu (Işletimsel)
**Özellik güncelleştirme hataları** işlem raporu, bir **Windows 10 özellik güncelleştirmeleri** ilkesiyle hedeflenen ve bir güncelleştirmeyi denemeyen cihazlara yönelik hata ayrıntıları sağlar. Bu raporda bulunan veriler zamanında ve hatalı cihaz sayısını çağırır. Sorun gidermeye yardımcı olmak için ayrıntıya gidebilirsiniz. Bu rapor filtreleme, arama, sayfalama ve sıralama sağlar. 

Aşağıdaki adımları kullanarak **özellik güncelleştirme arızaları** raporunu görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**seçme  >  **Monitor**  >  **özelliği güncelleştirme başarısızlıklarını**seçin.

## <a name="device-compliance-report-organizational"></a>Cihaz uyumluluk raporu (kuruluş)

Cihaz uyumluluk raporlarının doğası gereği, toplanan ölçümleri tanımlamak üzere verilerin daha geleneksel bir raporlama görünümünü sağlaması amaçlanmıştır. Bu rapor, tam cihaz uyumluluk resmi almak için büyük veri kümeleriyle çalışmak üzere tasarlanmıştır. Örneğin, cihaz uyumluluğuna yönelik cihaz uyumluluk raporu, veri kümesinin ne kadar büyük olduğuna bakılmaksızın, cihazların daha geniş bir görünümünü sağlamak için cihazlara yönelik tüm uyumluluk durumlarını gösterir. Bu rapor, toplu ölçümlerin uygun bir görselleştirmesine ek olarak kayıtların tam dökümünü gösterir. Bu rapor, üzerine filtre uygulanarak ve "rapor oluştur" düğmesi seçilerek oluşturulabilir. Bu işlem, toplanan verileri oluşturan tek tek kayıtları görüntüleme yeteneği ile en son durumu göstermek için verileri yeniler. Yeni çerçevede bulunan çoğu rapor gibi, bu kayıtlar, ihtiyacınız olan bilgilere odaklanmak için sıralanabilir ve aranabilir.

Cihaz durumunun oluşturulmuş bir raporunu görmek için aşağıdaki adımları kullanabilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. Raporların özetini görüntülemek için **raporlar** ' ı seçin.
3. **Cihaz uyumluluğu**'nu seçin.
4. Raporunuzu iyileştirmek için **uyumluluk durumu**, **Işletim sistemi**ve **sahiplik** filtrelerini seçin.
5. Geçerli verileri almak için **rapor oluştur** (veya **yeniden oluştur**) seçeneğine tıklayın.

    ![Cihaz uyumluluk raporu](./media/intune-reports/intune-reports-02a.png)

    > [!NOTE]
    > Bu **cihaz uyumluluk** raporu, raporun en son ne zaman oluşturulduğu zaman damgasını sağlar. 

İlgili bilgiler için bkz. [Intune 'Da koşullu erişimle Microsoft Defender ATP için uyumluluğu zorlama](../protect/advanced-threat-protection.md).

## <a name="reports-summary"></a>Rapor Özeti 

Cihaz uyumluluk raporu, **raporlar** iş yükünde Özet rapor olarak kullanılabilir. Cihaz uyumluluk raporunu görüntülemek için aşağıdaki adımları kullanın:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. Raporların özetini görüntülemek için **raporlar** ' ı seçin.

    ![Intune raporları Özeti](./media/intune-reports/intune-reports-01.png)

## <a name="antivirus-agent-status-report-organizational"></a>Virüsten koruma Aracısı durum raporu (kuruluş)
**Virüsten koruma Aracısı durum** raporu, kuruluşunuzun cihazlarının aracı durumunu sağlar. Bu rapor, hangi cihazların gerçek zamanlı veya ağ korumasına sahip olduğunu ve bunların durumunu gösterir. Bu raporda bulunan veriler zamanında, sağlıksız cihaz, Kullanıcı adı ve önem derecesi ' ni çağırır. Bu rapor, birincil **Microsoft Defender virüsten koruma** iş yükünde kullanılabilir. Bu rapor filtreleme, arama, sayfalama ve sıralama sağlar. 

Aşağıdaki adımları kullanarak **Virüsten koruma Aracısı durum** raporunu görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Raporları**  >  **Microsoft Defender virüsten**koruma  >  **Aracısı durumu**' nu seçin.

## <a name="detected-malware-report-organizational"></a>Algılanan kötü amaçlı yazılım raporu (Kurumsal)
**Algılanan kötü amaçlı yazılım** raporu, kuruluşunuzun cihazlarının kötü amaçlı yazılım durumunu sağlar. Bu rapor, kötü amaçlı yazılım ve kötü amaçlı yazılım ayrıntılarının algılanan cihaz sayısını gösterir. Bu raporda bulunan veriler zamanında, cihaz adını ve önem derecesini ve diğer kötü amaçlı yazılımla ilgili ayrıntıları çağırır. Bu rapor, birincil **Microsoft Defender virüsten koruma** iş yükünde kullanılabilir. Bu rapor ayrıca filtreleme, arama, sayfalama ve sıralama sağlar. 

**Algılanan kötü amaçlı yazılım** raporunu aşağıdaki adımları kullanarak görebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Raporları**seçin  >  **Microsoft Defender virüsten koruma**  >  **kötü amaçlı yazılım algıladı**.

## <a name="windows-10-feature-updates-organizational"></a>Windows 10 özellik güncelleştirmeleri (Kurumsal)
**Windows 10 özellik güncelleştirmeleri** raporu, bir **Windows 10 özellik güncelleştirmeleri** ilkesiyle hedeflenen cihazlar için uyumluluk genel görünümünü sağlar. Bu rapor, güncelleştirme durumuna göre güncelleştirme durumunu sağlar. Ayrıca, belirli cihaz güncelleştirme ayrıntılarını da görebilirsiniz. Bu raporlarda bulunan veriler zamanında, cihaz adı ve durumunun yanı sıra diğer güncelleştirmeyle ilgili ayrıntıları da çağırır. **Windows güncelleştirmeleri** iş yükünde özet raporu kullanılabilir. Bu rapor ayrıca filtreleme, arama, sayfalama ve sıralama sağlar. 

Aşağıdaki adımları kullanarak **Windows 10 özellik güncelleştirmeleri** raporunu görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Reports**  >  Özet raporunu görüntülemek için rapor**Windows güncelleştirmeleri** ' ni seçin.
3. **Windows 10 özellik güncelleştirmeleri** raporunu görmek için **raporlar** sekmesini seçin ve **Windows Feature Update raporuna** tıklayın.

## <a name="device-compliance-trend-report-historical"></a>Cihaz uyumluluk eğilimi raporu (geçmiş)

Cihaz uyumluluğu eğilimi raporlarının, cihaz uyumluluğuyla ilgili uzun süreli eğilimleri belirlemek için Yöneticiler ve mimarlar tarafından kullanılma olasılığı yüksektir. Toplanan veriler bir süre içinde görüntülenir ve gelecekteki yatırım kararları vermek, işlem geliştirmelerini gerçekleştirmek veya herhangi bir anormalde araştırma istemek için yararlıdır. Ayrıca, belirli eğilimleri görmek için filtreler uygulanabilir. Bu rapor tarafından belirtilen veriler, geçerli kiracı durumunun anlık görüntüsüdür (gerçek zamanlı). 

Cihaz uyumluluk eğilimleri için bir cihaz uyumluluk eğilimi raporu, cihaz uyumluluk durumlarının bir süre boyunca eğilimini gösterebilir. Uyumluluğun nerede oluştuğunu tanımlayabilir ve zaman ve çabalarınızı uygun şekilde odakla azaltabilirsiniz.

Aşağıdaki adımları kullanarak **eğilimler** raporunu görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Reports**  >  Cihaz uyumluluğunu 60 günlük bir eğilim üzerinden görüntülemek için rapor**eğilimlerini** seçin.

    ![Intune eğilim raporu](./media/intune-reports/intune-reports-03.png)

## <a name="azure-monitor-integration-reports-specialist"></a>Azure Izleyici tümleştirme raporları (uzman)
İstediğiniz verileri almak için kendi raporlarınızı özelleştirebilirsiniz. Raporlarınızdaki veriler, [Log Analytics](reports.md#log-analytics) ve [Azure izleyici çalışma kitaplarını](reports.md#workbooks)kullanarak [Azure izleyici](/azure/azure-monitor/overview) aracılığıyla isteğe bağlı olarak kullanılabilir. Bu çözümler, özel sorgular oluşturmanıza, uyarıları yapılandırmanıza ve cihaz uyumluluk verilerini istediğiniz şekilde göstermeye yönelik panolar yapmanıza olanak sağlar. Ayrıca, Azure Depolama hesabınızdaki etkinlik günlüklerini koruyabilir, [güvenlik bilgileri ve olay yönetimi (SıEM) araçlarını](/microsoft-365/security/office-365-security/siem-server-integration)kullanarak raporlarla tümleştirebilir ve RAPORLARıN Azure ad etkinlik günlükleriyle ilişkilendirilmesi sağlayabilirsiniz. Azure Izleyici çalışma kitapları, özel raporlama ihtiyaçları için panoları içeri aktarmaya ek olarak kullanılabilir.

> [!NOTE]
> Karmaşık raporlama işlevselliği, bir Azure aboneliği gerektirir.

Örnek bir uzman raporu, cihaz sahipliği verilerini özel bir rapordaki platform kayıt verileriyle birlikte ilişkilendirir. Ardından, bu özel rapor Azure Active Directory portalındaki mevcut bir panoda görüntülenebilir.

Aşağıdaki adımları kullanarak özel raporlar oluşturabilir ve görüntüleyebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Rapor**  >  **Tanılama ayarları** [Tanılama ayarı](reports.md#diagnostic-settings)Ekle ' yi seçin.

    ![Intune raporları-tanılama ayarı ekleme](./media/intune-reports/intune-reports-04.png)

3. Tanılama **ayarları** bölmesini göstermek için **Tanılama ayarı Ekle** ' ye tıklayın. 
4. Tanılama ayarları için bir **ad** ekleyin. 
5. **Log Analytics gönder** ve **Devicekarmaşıkanceorg** ayarlarını seçin.

    ![Intune raporları-Tanılama ayarları](./media/intune-reports/intune-reports-04a.png)

6. **Kaydet**’e tıklayın.
7. Sonra, [Log Analytics](reports.md#log-analytics)kullanarak yeni bir günlük sorgusu oluşturmak ve çalıştırmak için **Log Analytics** ' i seçin.

   ![Log Analytics-günlük sorgusu](./media/intune-reports/intune-reports-05.png)

8. [Azure izleyici çalışma kitaplarını](reports.md#workbooks)kullanarak etkileşimli bir rapor oluşturmak veya açmak Için **çalışma kitaplarını** seçin.

   ![Çalışma kitapları-etkileşimli raporlar](./media/intune-reports/intune-reports-07.png)

### <a name="diagnostic-settings"></a>Tanılama ayarları
Her Azure kaynağı kendi tanılama ayarını gerektirir. Tanılama ayarı bir kaynak için aşağıdakileri tanımlar:

- Ayarda tanımlanan hedeflere gönderilen günlük kategorileri ve ölçüm verileri. Kullanılabilir Kategoriler farklı kaynak türleri için farklılık gösterir.
- Günlükleri göndermek için bir veya daha fazla hedef. Geçerli hedeflere Log Analytics çalışma alanı, Event Hubs ve Azure Storage dahildir.
- Azure depolama 'da depolanan veriler için bekletme ilkesi.

Tek bir tanılama ayarı, hedeflerin her birinden birini tanımlayabilir. Belirli bir hedef türünden birine (örneğin, iki farklı Log Analytics çalışma alanı) birden fazla veri göndermek istiyorsanız, daha sonra birden çok ayar oluşturun. Her kaynak en fazla 5 tanılama ayarlarına sahip olabilir.

Tanılama ayarları hakkında daha fazla bilgi için bkz. [Azure 'da platform günlüklerini ve ölçümlerini toplamak için tanılama ayarı oluşturma](/azure/azure-monitor/platform/diagnostic-settings).

### <a name="log-analytics"></a>Log Analytics
Log Analytics, günlük sorgularını yazmak ve sorguların sonuçlarını etkileşimli olarak çözümlemek için Azure portal birincil araçtır. Günlük sorgusu Azure Izleyici 'de başka bir yerde kullanılsa bile, genellikle Log Analytics kullanarak sorguyu yazın ve test edersiniz. Log Analytics kullanma ve günlük sorguları oluşturma hakkında ayrıntılar için bkz. [Azure izleyici 'de günlük sorgularına genel bakış](/azure/azure-monitor/log-query/log-query-overview). 

### <a name="workbooks"></a>Çalışma Kitapları
Çalışma kitapları metin, analiz sorguları, Azure ölçümleri ve parametreleri zengin etkileşimli raporlarla birleştirir. Çalışma kitapları aynı Azure kaynaklarına erişimi olan diğer takım üyeleri tarafından düzenlenebilir. Çalışma kitapları hakkında daha fazla bilgi için bkz. [Azure izleyici çalışma kitapları](/azure/azure-monitor/app/usage-workbooks). Ayrıca, ile çalışarak çalışma kitabı şablonlarına katkıda bulunabilirsiniz. Daha fazla bilgi için bkz. [Azure Izleyici çalışma kitabı şablonları](https://go.microsoft.com/fwlink/?linkid=867045).

## <a name="next-steps"></a>Sonraki adımlar 

Aşağıdaki teknolojiler hakkında daha fazla bilgi edinin:
- [Blog-Microsoft Intune raporlama çerçevesi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553)
- [Azure İzleyici](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor)
- [Log Analytics nedir?](/azure/azure-monitor/log-query/log-query-overview#what-is-log-analytics)
- [Günlük sorguları](/azure/azure-monitor/log-query/log-query-overview)
- [Azure Izleyici 'de Log Analytics kullanmaya başlama](/azure/azure-monitor/log-query/get-started-portal)
- [Azure Izleyici çalışma kitapları](/azure/azure-monitor/app/usage-workbooks)
- [Güvenlik bilgileri ve olay yönetimi (SıEM) araçları](/microsoft-365/security/office-365-security/siem-server-integration)