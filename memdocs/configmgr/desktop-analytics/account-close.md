---
title: Hesabınızı kapatma
titleSuffix: Configuration Manager
description: Azure hesabınızdan masaüstü Analizi 'ni kaldırma
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e24c2ee19093dd12af6e87280a31851a1f593782
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268479"
---
# <a name="how-to-close-your-account"></a>Hesabınızı kapatma

Ortamınızda masaüstü analizlerini ayarlayıp kaldırmanız gerekiyorsa, hesabınızı kapatmak için bu işlemi kullanın.

## <a name="prerequisites"></a>Ön koşullar

Azure portal hesabı yalnızca bir **genel yönetici** kapatabilir veya yeniden etkinleştirebilir.

## <a name="process-to-offboard"></a>İşlem kapalı

1. [Masaüstü Analizi portalını](https://aka.ms/desktopanalytics) Microsoft 365 cihaz yönetimi ' nde, **genel yönetici** rolüne sahip bir kullanıcı olarak açın.

1. **Genel ayarlar** menüsünde **bağlı hizmetler**' i seçin. Cihazları Kaydet bölümünde, **çıkarma**seçeneğini belirleyin.

1. Devam etmeye karar verirseniz hesabınız kapalı olur.

> [!Important]
> Bu makalenin geri kalanını 90 gün sonra veya yeniden etkinleştirmezseniz devam edin.
>
> Hesabınızı 90 gün beklemek zorunda kalmadan tamamen kapatmak istiyorsanız, önce hesabınızı [sıfırlayın](account-reset.md) .

## <a name="reactivate"></a>Yeniden etkinleştirme

Sonraki 90 gün boyunca, masaüstü Analizi portalına erişen kuruluşunuzdaki tüm yöneticiler, boşaltmanız gerektiğini belirten bir bildirim görür.

Genel yönetici, hesabı 90 gün içinde yeniden etkinleştirebilir. Kuruluşunuzun masaüstü analizlerini geri yüklemek için **beni geri alma**seçeneğini belirleyin.

## <a name="delete-the-solution"></a>Çözümü silme

> [!Warning]
> Bu makalenin geri kalanını 90 gün sonra veya yeniden etkinleştirmezseniz devam edin. Bu diğer bileşenleri silip keserseniz, yeniden etkinleştirmeyi denemeyin.

1. [Azure Portal](https://portal.azure.com) , **genel yönetici** rolüne sahip bir kullanıcı olarak oturum açın.

1. Masaüstü Analizi çalışma alanınızın adı için **tüm kaynaklarda** arama yapın. Bu ad, hizmete kaydolurken oluşturduğunuz şeydir.

1. `Microsoft365Analytics(YourWorkspaceName)` **Çözüm**türü silme.

Masaüstü Analizi verileri çalışma alanı için veri bekletme ilkenize göre yaşılır. Aynı çalışma alanında diğer çözümleri kullanmaya devam edebilirsiniz.

> [!Important]  
> Log Analytics çalışma alanını diğer çözümlerle kullanıyorsanız, çalışma alanını silmeyin.

## <a name="remove-user-and-app-access"></a>Kullanıcı ve uygulama erişimini kaldırma

1. [Azure Portal](https://portal.azure.com) , **genel yönetici** rolüne sahip bir kullanıcı olarak oturum açın. **Azure Active Directory**gidin.

1. **Roller ve yöneticiler**' de **Masaüstü Analizi yönetici** rolünü aratın. Üyelerini kaldırın.

1. **Gruplar**' da, aşağıdaki grupların üyelerini kaldırın:

    - **M365 Analytics Istemci yöneticileri (Log Analytics sahipleri)**
    - **M365 Analytics Istemci yöneticileri (Log Analytics katkıda bulunanlar)**

1. **Kurumsal uygulamalarda**, aşağıdaki uygulamalar için erişim izinlerini silin veya iptal edin:

    - `MaLogAnalyticsReader`

    - ConfigMgr uygulaması. Bu uygulamanın adını bulmak için Configuration Manager konsoluna gidin. **Yönetim** çalışma alanında **Cloud Services**' ı genişletin ve **Azure hizmetleri** düğümünü seçin. **Masaüstü Analizi** hizmetinin özelliklerini açın ve **uygulamalar** sekmesine geçin. **Web uygulaması** bu Azure uygulamasıdır.

        > [!Important]  
        > Azure AD 'de bu uygulamada değişiklik yapmadan önce, Configuration Manager ' deki başka bir hizmetle yeniden kullandığınızdan emin olun.

## <a name="disconnect-configuration-manager"></a>Configuration Manager bağlantısını kes

1. Configuration Manager konsolunu, **tam yönetici** rolüne sahip bir kullanıcı olarak açın.

1. **Yönetim** çalışma alanına gidin, **Cloud Services**öğesini genişletin ve **Azure hizmetleri** düğümünü seçin.

1. Masaüstü Analizi hizmetini silin.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Pilot ve üretim dağıtımları için koleksiyonları silme

1. Configuration Manager konsolunda, **varlıklar ve uyum** çalışma alanında **Cihaz Koleksiyonları** ' nı seçin.

1. Artık kullanmadığınız koleksiyonları silin. Varsayılan olarak, Koleksiyonlar **dağıtım planları** klasörünün altında bulunur.  

## <a name="reconfigure-clients"></a>İstemcileri yeniden yapılandırın

### <a name="unenroll-devices"></a>Cihazların kaydını kaldır

Kayıtlı cihazlarda, aşağıdaki Windows kayıt defteri anahtarlarından ticari kimlik değerini kaldırın:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows tanılama veri yapılandırması

Cihazların tanılama verilerini göndermeye devam etmesini istemiyorsanız:

- Windows 10: tanılama veri düzeyini **güvenlik** olarak ayarlayın
- Windows 7 SP1 veya 8,1: **ticari veri katılımı anahtarını** devre dışı bırakma

Aşağıdaki yöntemlerden birini kullanarak bu değerleri ayarlayın:

- Grup ilkesi, **bilgisayar yapılandırması**  >  **Yönetim Şablonları**  >  **Windows bileşenleri**  >  **veri toplama ve önizleme yapıları**
- [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry) gibi mobil cihaz YÖNETIMI (MDM)

Daha fazla bilgi için bkz. [Kuruluşunuzda Windows tanılama verilerini yapılandırma](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Bu değişiklikleri uyguladığınızda, cihazlar tanılama verilerini göndermeyi hemen durdurur. Microsoft 'un, çalışma alanınız için öngörüleri işlemeyi durdurması 24-48 saat sürebilir. Microsoft bu verileri, bulut hizmetlerinden 30 gün içinde veya daha az bir süre içinde siler.
