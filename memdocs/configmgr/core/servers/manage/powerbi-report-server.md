---
title: Power BI Rapor Sunucusu ile tümleştirme
titleSuffix: Configuration Manager
description: Modern görselleştirme ve daha iyi performans için Power BI Rapor Sunucusu Configuration Manager raporlama ile tümleştirin.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f4089f52d912491b3b1396906fe391c5c334e061
ms.sourcegitcommit: 02635469d684d233fef795d2a15615658e62db10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84814898"
---
# <a name="integrate-with-power-bi-report-server"></a>Power BI Rapor Sunucusu ile tümleştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3721603-->

Sürüm 2002 ' den başlayarak, [Power BI Rapor Sunucusu](https://docs.microsoft.com/power-bi/report-server/get-started) Configuration Manager raporlama ile tümleştirebilirsiniz. Bu tümleştirme size modern görselleştirme ve daha iyi performans sağlar. Bu, SQL Server Reporting Services zaten mevcut olana benzer Power BI raporlar için konsol desteği ekler.

Power BI Desktop rapor dosyalarını Kaydet (. PBIX) ve Power BI Rapor Sunucusu dağıtın. Bu işlem, SQL Server Reporting Services rapor dosyalarıyla benzerdir (. RDL). Raporları tarayıcıda doğrudan Configuration Manager konsolundan da başlatabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

- Power BI Rapor Sunucusu Lisansı. Daha fazla bilgi için bkz. [lisanslama Power BI rapor sunucusu](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server).

- [Microsoft Power BI rapor sunucusu-eylül 2019](https://www.microsoft.com/download/details.aspx?id=57270)veya sonraki bir sürümü indirin.

    > [!NOTE]
    > Power BI Rapor Sunucusu hemen yüklemeyin. Ortamınıza bağlı olarak uygun işlem için bkz. [Reporting Services noktasını yapılandırma](#configure-the-reporting-services-point).

- [Microsoft Power BI Desktop (Power BI rapor sunucusu-eylül 2019 Için iyileştirilmiş)](https://www.microsoft.com/download/details.aspx?id=57271)veya üzeri indirin.

    > [!IMPORTANT]
    > - Yalnızca [Microsoft Indirme merkezi](https://www.microsoft.com/download/)'ndeki Power BI Desktop sürümlerini kullanın, Microsoft Store bir sürüm kullanmayın.
    > - Yalnızca [ **Power BI rapor sunucusu Için iyileştirildiğini**belirten Power BI Desktop](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop)bir sürümünü kullanın.

- Power BI tümleştirme, raporlama için aynı rol tabanlı yönetimi kullanır.
    > [!NOTE]
    > Power BI Rapor Sunucusu RBAC özellikli raporları desteklemez Bu nedenle, kendilerine atanan kapsamlarından bağımsız olarak, raporların tüm görüntüleyicilerinin aynı sonuçları görür.

## <a name="configure-the-reporting-services-point"></a>Raporlama Hizmetleri noktasını yapılandırma

Bu işlem, sitede bu rolün zaten mevcut olup olmadığına bağlı olarak farklılık gösterir.

### <a name="you-have-a-reporting-services-point"></a>Bir Raporlama Hizmetleri noktanız var

Bu işlemi yalnızca sitede bir Raporlama Hizmetleri noktanız zaten varsa kullanın. Bu işlemin tüm adımlarını aynı sunucuda yapın:

1. **Raporlama sunucusu Configuration Manager**, **şifreleme anahtarlarını**yedekleyin. Daha fazla bilgi için bkz. [SSRS şifreleme anahtarları-şifreleme anahtarlarını yedekleme ve geri yükleme](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Bu adımı atlarsanız SQL Server Reporting Services özel raporlara erişiminizi kaybedersiniz.

1. Raporlama Hizmetleri noktası rolünü siteden kaldırın.

1. SQL Server Reporting Services kaldırın, ancak veritabanını koruyun.

1. Power BI Rapor Sunucusu'nu yükleyin.

1. Power BI Rapor Sunucusu Yapılandırma

    1. Önceki rapor sunucusu veritabanını kullanın.

    1. **Şifreleme anahtarlarını**geri yüklemek Için **Raporlama sunucusu Configuration Manager** kullanın.

1. Configuration Manager ' de raporlama hizmetleri noktası rolünü ekleyin.

### <a name="you-dont-have-a-reporting-services-point"></a>Bir Raporlama Hizmetleri noktanız yok

Bu işlemi yalnızca sitede bir Raporlama Hizmetleri noktanız yoksa kullanın. Bu işlemin tüm adımlarını aynı sunucuda yapın:

1. Power BI Rapor Sunucusu'nu yükleyin.

2. Configuration Manager ' de raporlama hizmetleri noktası rolünü ekleyin. Daha fazla bilgi için bkz. [raporlamayı yapılandırma](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Configuration Manager konsolunu yapılandırma

1. Configuration Manager konsolunun bulunduğu bir bilgisayarda, Configuration Manager konsolunu en son sürüme güncelleştirin.

1. Power BI Desktop 'i yükler. Dilin aynı olduğundan emin olun.

1. Yüklendikten sonra, Configuration Manager konsolunu açmadan önce en az bir kez Power BI Desktop başlatın.

## <a name="create-power-bi-reports"></a>Power BI raporları oluşturma

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve yeni **Power BI raporları** düğümünü seçin.

1. Şeritte **rapor oluştur**' u seçin. Bu eylem Power BI Desktop açar.

1. Power BI Desktop bir rapor oluşturun.

    - Power BI Desktop, bir veri kaynağına bağlandığınızda, bağlantı ayarları için **DirectQuery** ' yi seçin.

    - Bu raporlarda yalnızca desteklenen SQL görünümlerini kullanın. Daha fazla bilgi için bkz. [Configuration Manager SQL Server görünümlerini kullanarak özel raporlar oluşturma](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Rapor kaydedilmeye hazırsa **Dosya** menüsüne gidin, **farklı kaydet**' i seçin ve ardından **Power BI rapor sunucusu**' yi seçin.

1. **Power BI rapor sunucusu seçim** penceresinde, Raporlama Hizmetleri noktasının URL 'sini **Yeni rapor sunucusu adresi**olarak girin. Örneğin, `https://rsp.contoso.com/Reports`.

Configuration Manager konsolunda, yeni raporu, Power BI raporları listesinde görürsünüz.

## <a name="next-steps"></a>Sonraki adımlar

Bir rapor oluşturduktan sonra, Configuration Manager konsolunda aşağıdaki eylemleri kullanın:

- **Tarayıcıda Çalıştır**: Power BI raporunu Web tarayıcısında açar. Bu URL 'YI başkalarıyla paylaşma, örneğin:`https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Web tarayıcısında yalnızca bu raporları görüntüleyebilirsiniz.

- **Düzenle**: Power BI Desktop raporda değişiklik yapın. Mevcut bir rapor için, değişiklikleri rapor sunucusuna geri kaydetmek için **Kaydet** seçeneğini kullanın.

Raporlama için kullanılacak günlük dosyaları hakkında daha fazla bilgi için bkz. [günlük dosyası başvurusu-raporlama](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
