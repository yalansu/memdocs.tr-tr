---
title: Şirket Portalı’ndaki uygulamalar
titleSuffix: Configuration Manager
description: Şirket Portalı uygulamasını kullanmak için ortak yönetilen cihazlar için tutarlı bir kullanıcı deneyimi sağlayın.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd49546e49d6964cfe37b0b13e1abe9175f4aa0e
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432566"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Ortak yönetilen cihazlarda Şirket Portalı uygulamasını kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--CMADO-3601237,INADO-4297660-->

Sürüm 2006 ' den başlayarak Şirket Portalı, artık Microsoft Endpoint Manager için platformlar arası uygulama portalı deneyimidir. Ortak yönetilen cihazları Şirket Portalı de kullanacak şekilde yapılandırarak tüm cihazlarda tutarlı bir kullanıcı deneyimi sağlayabilirsiniz.

Şirket Portalı aşağıdaki eylemleri destekler:

- Şirket Portalı uygulamasını birlikte yönetilen cihazlarda başlatın ve Azure Active Directory (Azure AD) çoklu oturum açma (SSO) ile oturum açın.
- Intune uygulamalarıyla birlikte Şirket Portalı Configuration Manager ve yüklü uygulamaları görüntüleyin.
- Şirket Portalı Configuration Manager uygulamaları yükleme ve yükleme durum bilgilerini alma.

:::image type="content" source="media/3601237-company-portal.png" alt-text="Configuration Manager uygulama ile Şirket Portalı" lightbox="media/3601237-company-portal.png":::

Şirket Portalı davranışı ortak yönetim iş yükü yapılandırmanıza bağlıdır:

| İş Yükü | Ayar | Davranış |
|----------|---------|----------|
| İstemci uygulamaları | **Configuration Manager** | Yalnızca Configuration Manager istemci uygulamalarını görebilirsiniz |
| İstemci uygulamaları | **Pilot Intune** veya **Intune** | Hem Configuration Manager hem de Intune istemci uygulamalarını görebilirsiniz |
| Office Tıkla-Çalıştır uygulamaları | **Configuration Manager** | Yalnızca Office Tıkla-Çalıştır uygulamaları Configuration Manager görebilirsiniz |
| Office Tıkla-Çalıştır uygulamaları | **Pilot Intune** veya **Intune** | Yalnızca Intune Office Tıkla-Çalıştır uygulamalarını görebilirsiniz |

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Uygulama iş yükleri için diyagram](workloads.md#diagram-for-app-workloads)

- [Configuration Manager iş yüklerini Intune 'a değiştirme](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Önkoşullar

- Geçerli dal sürümü 2006 veya üstünü Configuration Manager <sup>([bkz. SSS](#bkmk_ver-prereq))</sup>

- Şirket Portalı App Version 11.0.8980.0 veya üzeri

- Windows 10, sürüm 1803 veya üzeri:

  - [Ortak yönetime](how-to-enable.md) kaydolmuş

  - [Intune için Internet uç noktalarına](../../intune/fundamentals/intune-endpoints.md) erişim

- Bu cihazlarda oturum açmak için gereken kullanıcı hesapları aşağıdaki konfigürasyonları gerektirir:

  - Bir Azure AD kimliği

  - Bir Intune lisansı atandı

## <a name="configure-and-deploy"></a>Yapılandırma ve dağıtma

### <a name="configuration-manager-client-settings"></a>Configuration Manager istemci ayarları

Kullanıcıların yalnızca Şirket Portalı bildirimler aldığından emin olmak için Configuration Manager istemci ayarlarını yapılandırın. Cihaz ayarları ' nın **Yazılım Merkezi** grubunda, **Şirket portalı**için **Kullanıcı Portalı** ' nı seçin.

İstemci ayarları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [İstemci ayarlarını yapılandırma](../core/clients/deploy/configure-client-settings.md)
- [İstemci ayarları hakkında](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Şirket Portalı uygulamasını dağıtma

- Kullanıcılar Şirket Portalı uygulamayı [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab)el ile yükleyebilir.

- Ortak yönetilen cihazlarda uygulamayı gerektirmek için dağıtım işlemi, [istemci uygulamalarının](workloads.md#client-apps) ortak yönetim iş yükünün durumuna bağlıdır:

  - İstemci uygulamaları iş yükü Configuration Manager, [Configuration Manager bir uygulama oluşturun ve dağıtın](../apps/get-started/create-and-deploy-an-application.md). Çevrimdışı Şirket Portalı uygulamasını [iş Microsoft Store](https://www.microsoft.com/business-store)indirin.

  - İstemci uygulamaları iş yükü Intune ile varsa, Configuration Manager aracılığıyla dağıtabilir veya [Microsoft Intune kullanarak Windows 10 Şirket Portalı uygulamasını ekleyebilirsiniz](../../intune/apps/store-apps-company-portal-app.md).

Kuruluşunuzun Şirket Portalı marka hakkında daha fazla bilgi için, bkz. [Intune şirket portalı uygulamasını özelleştirme](../../intune/apps/company-portal-app.md).

## <a name="use-the-company-portal"></a>Şirket Portalı kullanın

1. Başlat menüsünden Şirket Portalı başlatın. Şu anda oturum açmış olan Kullanıcı Azure AD kimliğine göre Şirket Portalı otomatik olarak oturum açtı.

1. **Uygulamalar** sayfasını seçin. Listede Configuration Manager uygulamalar görmeniz gerekir.

1. Configuration Manager dağıtılan uygulamalardan birini seçin.

    - **Genel bakış** sekmesi, uygulamayla ilgili boyut, sürüm ve Yayımlanma tarihi gibi ayrıntıları gösterir.

    - Configuration Manager Bu uygulama için yönetim hizmeti olduğunu görmek için **ek bilgi** sekmesine geçin.

    - Uygulamayı yüklemek için, **yüklensin**' i seçin. Şirket Portalı, yükleme durumunu gösterir ve tamamlandığında bir bildirim görürsünüz.

    - Uygulama zaten yüklüyse, uygulamayı kaldırmak için **Kaldır** ' ı seçin.

    - `...` **Onarma** ve **paylaşma**gibi ek eylemler için üç nokta () simgesini seçin.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Şirket Portalı ayrıntılarla Configuration Manager uygulama" lightbox="media/3601237-company-portal-app-details.png":::

    - Bir Configuration Manager Web uygulaması yükledikten sonra, üç nokta menüsünü seçin ve ardından **tarayıcıda aç** ' ı seçerek Web uygulamasını başlatın.

    - Bir Configuration Manager uygulaması bilinen bir hata koduyla yüklenemediğinde, hata kodu üzerinde arama yapmak için başarısız durum bağlantısını seçin.

Şirket Portalı istemci ayarını değiştirirseniz, bir Kullanıcı Configuration Manager bildirimi seçtiğinde Şirket Portalı başlatır. Bildirim, Şirket Portalı desteklemediği bir senaryo için ise bildirim, yazılım merkezini başlatır.

Configuration Manager uygulamalarının yüklenmesiyle ilgili sorunları gidermeye yardımcı olmak için Şirket Portalı **yardım & destek** bölümüne gidin. **Yardım al** seçeneğini kullandığınızda, isteğin bir parçası olarak Configuration Manager günlük dosyaları gönderebilirsiniz.

## <a name="frequently-asked-questions-faq"></a>Sık sorulan sorular (SSS)

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Configuration Manager sürüm 2002 kullanıyorum, neden yeni Şirket Portalı Configuration Manager uygulamaları gösteriyor?

Şirket Portalı sürüm 11.0.8980.0 veya üzeri, kendisini kullanan tüm ortak yönetilen istemciler için Configuration Manager dağıtılan uygulamaları gösterir. Configuration Manager sürüm 2006, istemci ayarını bildirimleri denetlemek için eklediği için önkoşuldur. Daha önceki bir sürümün ortak yönetilen cihazına Şirket Portalı yüklerseniz veya istemci ayarını yapılandırmazsanız kullanıcılar her iki portaldan gelen bildirimleri görür. Bu deneyim, kullanıcılar için kafa karıştırıcı olabilir.

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Configuration Manager yazılım güncelleştirmeleri olarak dağıtılan uygulamaları Şirket Portalı destekler mi?

Evet. Yazılım güncelleştirmeleri özelliğini kullanarak bir uygulama dağıtırsanız, istemci bunu kullanıcı deneyiminin Şirket Portalı veya yazılım merkezi olup olmadığına bakılmaksızın aynı şekilde değerlendirir.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>Kullanıcılar Şirket Portalı Configuration Manager uygulamaları onarabilir, kaldırabilir ve güncelleştirebilir miyim?

Evet. Configuration Manager uygulamasını bu ek eylemleri destekleyecek şekilde yapılandırırsanız, Şirket Portalı Onar, kaldır ve Güncelleştir ' i destekler.

## <a name="known-issues"></a>Bilinen sorunlar

Yazılım Merkezi 'nin aşağıdaki özellikleri Şirket Portalı Şu anda kullanılamıyor:

- Bazı uygulama bilgileri, örneğin, bir yeniden başlatma gerekirse veya tahmini yüklenmeye süresi

- [Uygulama grupları](../apps/deploy-use/create-app-groups.md)

Diğer bilinen sorunlar:

- Aynı uygulamayı hem Configuration Manager hem de Intune 'dan dağıtırsanız, Şirket Portalı iki kez görünür.

- Şirket Portalı aradığınızda, Intune uygulamaları Configuration Manager uygulamalardan önce her zaman görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar

[Configuration Manager iş yüklerini Intune 'a değiştirme](how-to-switch-workloads.md)

[Intune Şirket Portalı uygulamasını özelleştirme](../../intune/apps/company-portal-app.md)
