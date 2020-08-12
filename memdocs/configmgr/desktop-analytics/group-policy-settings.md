---
title: Grup ilkesi ayarları
titleSuffix: Configuration Manager
description: Configuration Manager ve Masaüstü Analizi tarafından kullanılan Windows 'da yerel ve Grup İlkesi ayarlarını anlayın
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 2ee472b89f45e744e43915e51e98f11841208b73
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125816"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Masaüstü analizi için Grup İlkesi ayarları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Windows 'da Configuration Manager ve Masaüstü analizinin kullandığı yerel ve Grup İlkesi ayarları ayrıntılı olarak açıklanır.

Configuration Manager, cihazları masaüstü analizine kaydettiğinde, cihazı yapılandırmak için Windows ilkelerini ayarlar. Çoğu durumda bu ayarları yapılandırmak için yalnızca Configuration Manager kullanın.

## <a name="windows-settings"></a>Windows ayarları

Configuration Manager, aşağıdaki kayıt defteri anahtarlarının birindeki veya her ikisinde Windows ilkelerini ayarlar:

- Grup İlkesi nesnesi (**GPO**):`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **Yerel** ilke tercihi:`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| İlke | Yol | Şunlara uygulanır | Değer |
|--------|------|------------|-------|
| **Commercialıd** | Yerel | Tüm Windows sürümleri | Cihazın masaüstü analizinde görünmesi için kuruluşunuzun ticari KIMLIĞIYLE yapılandırın. |
| **Allowtelemetri**  | GPO | Windows 10 | `1` **Temel** (gerekli), `2` **Gelişmiş**veya `3` **tam** (isteğe bağlı) tanılama verileri için ayarlayın. Masaüstü analizi için en az temel Tanılama verileri gerekir. Microsoft, masaüstü analizi ile **Isteğe bağlı (sınırlı)** (Gelişmiş (sınırlı)) düzeyi kullanmanızı önerir. Daha fazla bilgi için bkz. [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, sürüm 1803 ve üzeri | Bu ayar yalnızca Allowtelemetri ayarı olduğunda geçerlidir `2` . Microsoft 'a gönderilen gelişmiş tanılama veri olaylarını yalnızca masaüstü analizinin gerektirdiği olaylarla sınırlandırır. Daha fazla bilgi için bkz. [Windows 10 Tanılama verileri olayları ve gelişmiş tanılama verilerini sınırla ilkesi aracılığıyla toplanan alanlar](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10, sürüm 1803 ve üzeri | Cihazların cihaz adını göndermesini etkinleştirin. Cihaz adı varsayılan olarak Microsoft 'a gönderilmez. Cihaz adını göndermezseniz, masaüstü analizlerinin "Unknown" olarak görünmesi gerekir. Daha fazla bilgi için bkz. [Cihaz adı](enroll-devices.md#device-name). |
| **Ticari veri OptIn** | Yerel | Windows 8.1 ve önceki sürümler | Masaüstü Analizi bir değeri gerektirir `1` . Daha fazla bilgi için bkz. [Windows 7 ' de ticari veri katılımı](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **Requestallappraerversions** | Her İkisi | Windows 8.1 ve önceki sürümler | Masaüstü analizi, `1` veri toplamanın doğru şekilde çalışması için bir değer gerektirir. |
| **DisableEnterpriseAuthProxy** | GPO | Tüm Windows sürümleri | Ortamınız internet erişimi için Windows tümleşik kimlik doğrulaması ile Kullanıcı kimliği doğrulanmış bir ara sunucu gerektiriyorsa, masaüstü analizi, `0` veri toplamanın doğru bir şekilde çalışması için bir değer gerektirir. Daha fazla bilgi için bkz. [proxy sunucusu kimlik doğrulaması](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> Çoğu durumda bu ayarları yapılandırmak için yalnızca Configuration Manager kullanın. Bu ayarları etki alanı Grup İlkesi nesnelerinde da uygulamayın. Daha fazla bilgi için bkz. [çakışma çözümü](enroll-devices.md#conflict-resolution).

### <a name="settings-from-upgrade-readiness"></a>Yükseltme Hazırlığı ayarlar

Windows Analytics, Yükseltme Hazırlığı betiği aracılığıyla aşağıdaki ilkeleri de ayarlar:

- Commercialıd
- AllowDeviceNameInTelemetry
- Ticari veri OptIn
- Requestallappraerversions

Bir cihazda Yükseltme Hazırlığı ekleme betiğini çalıştırdıysanız, bu ilke ayarları yine de mevcut olabilir. Eski betiği kullanmayın. Cihazı masaüstü Analizi 'ne kaydetmeden önce, bu önceki ilke ayarlarını kaldırın.

## <a name="group-policy-settings"></a>Grup ilkesi ayarları

Genel olarak, masaüstü Analizi ayarlarını ve kaydını hedeflemek için Configuration Manager koleksiyonları kullanın. Cihazları koleksiyona dahil etmek veya hariç tutmak için doğrudan üyeliği veya sorguları kullanın. Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](../core/clients/manage/collections/create-collections.md).

Configuration Manager, hedef koleksiyonunuzda ticari KIMLIK ve Tanılama verileri ayarlarını yapılandırır. Farklı cihaz grupları için farklı Tanılama verileri ayarları yapılandırmanız gerekiyorsa, Configuration Manager ayarlarını geçersiz kılmak için Grup İlkesi ayarlarını kullanın. Örneğin, bazı cihazlar için **Isteğe bağlı (sınırlı)** düzey ayarlamanız ve diğerleri için **gerekli** olması gerekir. Bazı cihazlarda [Ara sunucu kimlik doğrulama](enable-data-sharing.md#proxy-server-authentication) ayarları farklı olabilir.

İlgili Grup İlkesi ayarları şu yoldur: **bilgisayar yapılandırması**  >  **Yönetim Şablonları**  >  **Windows bileşenleri**  >  **veri toplama ve önizleme yapıları**.

Grup İlkesi ayarları yalnızca aşağıdaki anahtardaki kayıt defteri ayarlarını değiştirir:`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Karmaşık senaryoları etkinleştirmek için Grup İlkesi ayarlarını kullandığınızda, yapılandırma çakışmalarına neden olabilecek ilke ayarlarına özel dikkat edin. Configuration Manager yalnızca *değer yoksa* [Windows ayarlarını](#windows-settings) yapılandırır. Grup İlkesi ayarları Configuration Manager ayarlarından önceliklidir. bu nedenle, bazı Grup İlkesi yapılandırmalarının masaüstü analiziyle sorun oluşmasına neden olabilir.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Masaüstü analizi için Configuration Manager ayarlarıyla çakışabilecek Grup İlkesi ayarları

Aşağıdaki tabloda yer alan Grup İlkesi ayarları, masaüstü analizine kaydettiği cihazlarda Configuration Manager ayarlanan Windows ayarlarıyla çakışmasına neden olabilecek en büyük potansiyeli sahiptir:

| Görünen ad | Kayıt defteri değeri | Masaüstü analizine kayıtlı cihazlarda etki |
|--------------|----------------|-------------------------------------------------|
| **Ticari KIMLIĞI yapılandırma** | Commercialıd | Bu ilkeyi farklı bir değere ayarlarsanız, Configuration Manager tarafından ayarlanan ticari KIMLIĞI geçersiz kılar. Aynı KIMLIK yoksa, yapılandırılmış cihazlar masaüstü Analizi 'nde görünmeyebilir. |
| **Telemetriye izin ver** | Allowtelemetri | Bu ilkeyi farklı bir değere ayarlarsanız, hedef koleksiyon için Configuration Manager ayarladığınız genel tanılama veri düzeyini geçersiz kılar. |
| **Gelişmiş tanılama verilerini Windows Analytics için gereken en düşük düzeyde sınırlayın** | LimitEnhancedDiagnosticDataWindowsAnalytics | Bu ilke, önceki Allowtelemetri ayarına bağımlıdır. Configuration Manager veya Grup İlkesi ile ayarladığınız düzeye bağlı olarak, bu ilke cihazdaki tanılama veri düzeyini **Gelişmiş** veya **Gelişmiş (sınırlı)** olarak değiştirebilir. Bu ilke yalnızca Allowtelemetri `2` (**Gelişmiş**) olarak ayarlandıysa geçerlidir. |
| **Windows Tanılama verilerinde cihaz adının gönderilmesine izin ver** | AllowDeviceNameInTelemetry | Configuration Manager cihaz adlarını göndermeyi tercih ederseniz, bu ilkeyi devre dışı olarak yapılandırarak geçersiz kılabilirsiniz. Bu ayarı devre dışı bıraktığınızda, masaüstü analizinden cihaz adları "bilinmiyor" olarak görünür. Daha fazla bilgi için bkz. [Cihaz adı](enroll-devices.md#device-name). |
| **Bağlı kullanıcı deneyimi ve telemetri hizmeti için kimliği doğrulanmış ara sunucu kullanımını yapılandırma** | DisableEnterpriseAuthProxy | Configuration Manager cihazlarını Kullanıcı tarafından kimliği doğrulanmış ara sunucu () kullanmak üzere yapılandırırsanız `0` , bu Ilkeyi **kimliği doğrulanmış proxy kullanımını devre dışı bırakacak** şekilde yapılandırırsanız, `1` Cihaz kullanıcının bağlamı yerine sistem bağlamında Tanılama verileri gönderir. Cihazı sistem bağlamında bir ara sunucu ile yapılandırmazsanız veya cihaz ara sunucuda kimlik doğrulayamıyorsanız, Windows, tanılama verilerini masaüstü Analizi 'ne gönderemez. |

> [!NOTE]
> **Bağlı kullanıcı deneyimlerini ve Telemetriyi yapılandırma** (TelemetryProxy) Ilkesi, Windows 'un tanılama verilerini Kullanıcı (Winınet) veya cihaz (WinHTTP) proxy 'sini kullanmak yerine adanmış bir ara sunucuya iletmesini sağlar. Bazı Windows bileşenleri bu ilkeyi desteklemez. Bu ilkeyi kullanırsanız, masaüstü analizinden veri kalitesi sorunlarına neden olabilir.

#### <a name="behavior-of-disabled-settings"></a>Devre dışı bırakılan ayarların davranışı

Bu Grup İlkesi ayarlarını **devre dışı**olarak yapılandırırsanız, sistem davranışında farklı etkileri vardır.

- **Ticari kimlik** ilkesini devre dışı bıraktığınızda Windows, kayıt defteri değerini kaldırır. Yerel ilke kayıt defteri yolunda ayarlanan ticari KIMLIK Configuration Manager ayarı, ardından cihaz için geçerlidir.

- Grup İlkesi ile aynı kayıt defteri konumunda Configuration Manager ayarlayan ilkeler için, Grup İlkesi ayarını devre dışı bıraktığınızda Windows, kayıt defteri değerini kaldırır. Configuration Manager, bir sonraki ilke işleme döngüsüyle yeniden ayarlanır ve sonra Windows bunu bir sonraki Grup İlkesi yenilemesinde kaldırır. Yapılandırmada bu sabit değişiklik, masaüstü analiziyle istenmeyen davranışlara neden olabilir.

  - Bu Grup İlkesi ayarlarını **Yapılandırılmadı**olarak ayarlarsanız, Windows değeri bir kez kaldırır ancak kaldırmaya devam etmez. Bu yapılandırma, Configuration Manager değerlerinin beklendiği gibi uygulanmasını sağlar.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Kullanıcı deneyimini özelleştirmek için Grup İlkesi ayarları

Bu Grup İlkesi ayarları Configuration Manager veya masaüstü Analizi tarafından gerekli değildir. Kullanıcıları, Windows Tanılama verileriyle kullanıcılarınızın deneyimini yapılandırmak için Grup İlkesi 'nde yapılandırabilirsiniz.

| Görünen ad | Kayıt defteri değeri | Masaüstü analizine kayıtlı cihazlarda etki |
|--------------|----------------|-------------------------------------------------|
| **Telemetri katılım değişikliği bildirimlerini yapılandırma** | DisableTelemetryOptInChangeNotification | Windows 10, sürüm 1803 ' den itibaren Windows, tanılama veri düzeyi değiştiğinde kullanıcıları bilgilendirir. Bildirimleri devre dışı bırakmak için bu ilkeyi kullanın. |
| **Telemetri katılım ayarlarını yapılandırma kullanıcı arabirimi** | DisableTelemetryOptInSettingsUx | Tanılama veri düzeyini yapılandırırken, cihazın üst sınırını ayarlarsınız. Windows 10, sürüm 1803 ' den başlayarak, kullanıcılar daha düşük bir düzey ayarlayabilir. Kullanıcıların tanılama düzeyini değiştirmesini engellemek için bu ilkeyi kullanın. Daha fazla bilgi için bkz. [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Tanılama verilerini silmeyi devre dışı bırak** | DisableDeviceDelete | Kullanıcılar, Windows 10, sürüm 1809 ' den başlayarak tanılama verilerini **tanılama & geri bildirim** ayarları sayfasından silebilir. Microsoft 'un cihazdan topladığı tanılama verilerinin silinmesini engellemek için bu ilkeyi kullanın. |
| **Tanılama veri görüntüleyicisini devre dışı bırak** | DisableDiagnosticDataViewer | Windows 10, sürüm 1809 ' den başlayarak, kullanıcılar tanılama **& geri bildirim** ayarları sayfasından tanılama veri görüntüleyicisini etkinleştirip açabilir. Windows ayarlarındaki tanılama veri görüntüleyicisini devre dışı bırakmak ve Microsoft 'un cihazdan topladığı tanılama verilerini göstermesini engellemek için bu ilkeyi kullanın.|
