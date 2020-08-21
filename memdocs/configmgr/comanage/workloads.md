---
title: Ortak yönetim iş yükleri
titleSuffix: Configuration Manager
description: Configuration Manager 'ten Microsoft Intune geçiş yapmak için kullanabileceğiniz iş yükleri hakkında bilgi edinin.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: e44576401d601c8c510aaf50b28e5924f5c4d6db
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694874"
---
# <a name="co-management-workloads"></a>Ortak yönetim iş yükleri

İş yüklerini değiştirmek zorunda değilsiniz veya hazırsanız tek tek yapabilirsiniz. Configuration Manager, Intune 'a geçiş gerçekleştirmeyen iş yükleri ve ortak yönetimin desteklemediği diğer tüm Configuration Manager özellikleri de dahil tüm diğer iş yüklerini yönetmeye devam eder.

Bir iş yükünü Intune 'a geçerseniz, ancak daha sonra fikrinizi değiştirirseniz, tekrar Configuration Manager dönebilirsiniz.

Ortak yönetim aşağıdaki iş yüklerini destekler:

- [Uyumluluk ilkeleri](#compliance-policies)  

- [Windows Update ilkeleri](#windows-update-policies)  

- [Kaynak erişim ilkeleri](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Cihaz yapılandırması](#device-configuration)  

- [Office Tıkla-Çalıştır uygulamaları](#office-click-to-run-apps)  

- [İstemci uygulamaları](#client-apps)  

## <a name="compliance-policies"></a>Uyumluluk ilkeleri

Uyumluluk ilkeleri, bir cihazın koşullu erişim ilkeleriyle uyumlu kabul edilmesi için uyması gereken kuralları ve ayarları tanımlar. Uyumluluk ilkelerini, koşullu erişimden bağımsız olarak cihazlarla ilgili uyumluluk sorunlarını izlemek ve düzeltmek için de kullanın. Configuration Manager sürüm 1910 ' den başlayarak, uyumluluk ilkesi değerlendirme kuralı olarak özel yapılandırma temellerinin değerlendirmesini ekleyebilirsiniz. Daha fazla bilgi için bkz. [Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temelleri ekleme](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Intune özelliği hakkında daha fazla bilgi için bkz. [cihaz uyumluluk ilkeleri](/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Windows Update ilkeleri

Iş ilkeleri için Windows Update, Windows 10 özellik güncelleştirmeleri için erteleme ilkelerini veya doğrudan Iş Windows Update tarafından yönetilen Windows 10 cihazları için kalite güncelleştirmelerini yapılandırmanızı sağlar.

Intune özelliği hakkında daha fazla bilgi için bkz. [iş erteleme ilkelerini Windows Update yapılandırma](/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Kaynak erişim ilkeleri

Kaynak erişim ilkeleri cihazlarda VPN, Wi-Fi, e-posta ve sertifika ayarlarını yapılandırır.

Intune özelliği hakkında daha fazla bilgi için bkz. [kaynak erişim profillerini dağıtma](/intune/device-profiles).

> [!Note]  
> Kaynak erişimi iş yükü Ayrıca cihaz yapılandırmasının bir parçasıdır. Bu ilkeler, [cihaz yapılandırması](#device-configuration) iş yükünü değiştirdiğinizde Intune tarafından yönetilir.

## <a name="endpoint-protection"></a>Uç Nokta Koruma

<!--1357365-->

Endpoint Protection iş yükü Windows Defender 'ın kötü amaçlı yazılımdan koruma özellikleri paketini içerir:

- Windows Defender kötü amaçlı yazılımdan koruma
- Windows Defender Application Guard  
- Windows Defender Güvenlik Duvarı  
- Windows Defender SmartScreen  
- Windows Şifreleme
- Windows Defender Exploit Guard  
- Windows Defender Uygulama Denetimi  
- Windows Defender Güvenlik Merkezi  
- Windows Defender Gelişmiş tehdit koruması (şimdi Microsoft Defender tehdit koruması olarak bilinirdi)

Intune özelliği hakkında daha fazla bilgi için bkz. [Microsoft Intune Endpoint Protection](/intune/endpoint-protection-windows-10).

> [!Note]  
> Bu iş yükünü değiştirdiğinizde, Intune ilkeleri üzerlerine gelene kadar Configuration Manager ilkeleri cihazda kalır. Bu davranış, cihazın geçiş sırasında koruma ilkelerine hala sahip olduğundan emin olur.
>
> Endpoint Protection iş yükü Ayrıca cihaz yapılandırmasının bir parçasıdır. [Cihaz yapılandırma](#device-configuration) iş yükünü değiştirdiğinizde aynı davranış geçerlidir.<!-- SCCMDocs.nl-nl issue #4 --> Cihaz yapılandırma iş yükünü değiştirdiğinizde, ayrıca Endpoint Protection iş yüküne dahil olmayan Windows Information Protection özelliğine yönelik ilkeler de bulunur.<!-- 4184095 -->
>
> Intune cihaz yapılandırması için cihaz kısıtlamaları profil türünün parçası olan Microsoft Defender virüsten koruma ayarları, Endpoint Protection kaydırıcısının kapsamına dahil edilmez. Endpoint Protection kaydırıcısının etkin olduğu ortak yönetilen cihazlar için Microsoft Defender virüsten koruma 'yı yönetmek üzere **Microsoft Endpoint Manager Yönetim Merkezi**  >  **uç nokta güvenlik**  >  **Virüsten**koruma ' daki yeni virüsten koruma ilkelerini kullanın. Yeni ilke türü yeni ve geliştirilmiş seçeneklere sahiptir ve cihaz kısıtlamaları profilinde sunulan tüm ayarları destekler. <!--6609171-->
>
> Windows şifreleme özelliği BitLocker yönetimini içerir. Bu özelliğin ortak yönetim ile davranışı hakkında daha fazla bilgi için bkz. deploy The [BitLocker Management](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Cihaz yapılandırması

<!--1357903-->

Cihaz yapılandırma iş yükü, kuruluşunuzdaki cihazlar için yönettiğiniz ayarları içerir. Bu iş yükünü değiştirmek, **kaynak erişimini** ve **Endpoint Protection** iş yüklerini de taşıdıkça.

Intune 'un cihaz yapılandırma yetkilisi olmasına rağmen Configuration Manager ayarları ortak yönetilen cihazlara dağıtmaya devam edebilirsiniz. Bu özel durum, kuruluşunuzun gerektirdiği ancak henüz Intune 'da kullanılamadığı ayarları yapılandırmak için kullanılabilir. Bu özel durumu bir [Configuration Manager yapılandırma temeli](../compliance/deploy-use/create-configuration-baselines.md)üzerinde belirtin. Temeli oluştururken **ortak yönetilen istemciler için bu temeli her zaman Uygula** seçeneğini etkinleştirin. Daha sonra varolan bir taban çizgisinin özelliklerinin **genel** sekmesinde değiştirebilirsiniz.  

Intune özelliği hakkında daha fazla bilgi için, bkz. [Microsoft Intune bir cihaz profili oluşturma](/intune/device-profile-create).  

> [!NOTE]
> Cihaz yapılandırma iş yükünü değiştirdiğinizde, ayrıca Endpoint Protection iş yüküne dahil olmayan Windows Information Protection özelliğine yönelik ilkeler de bulunur.<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Office Tıkla-Çalıştır uygulamaları

<!--1357841-->

Bu iş yükü, ortak yönetilen cihazlarda Microsoft 365 uygulamalarını yönetir.

- İş yükünü taşıdıktan sonra, uygulama cihazda **Şirket portalı** görüntülenir  

- Office güncelleştirmelerinin, cihazlar yeniden başlatılana kadar istemcinin gösterilmesi 24 saat sürebilir  

- Yeni bir genel koşul mevcuttur, **cihazda Intune tarafından yönetilen Office 365 uygulamaları vardır**. Bu koşul, varsayılan olarak yeni Office 365 uygulamalarına bir gereksinim olarak eklenir. Bu iş yükünü geçiş yaparken, ortak yönetilen istemciler uygulamadaki gereksinimi karşılamıyor. Ardından, Configuration Manager aracılığıyla dağıtılan Office 365 ' i yüklemez.  

Intune özelliği hakkında daha fazla bilgi için bkz. [Microsoft Intune Ile Office 365 uygulamalarını Windows 10 cihazlarına atama](/intune/apps-add-office365).

## <a name="client-apps"></a>İstemci uygulamaları

<!--1357892-->

Ortak yönetilen Windows 10 cihazlarında istemci uygulamalarını ve PowerShell betiklerini yönetmek için Intune 'U kullanın. Bu iş yükünü geçirdikten sonra, Intune 'dan dağıtılan kullanılabilir uygulamalar Şirket Portalı kullanılabilir. Configuration Manager 'ten dağıttığınız uygulamalar yazılım merkezi 'nde kullanılabilir.

Intune özelliği hakkında daha fazla bilgi için bkz. [uygulama yönetimi Microsoft Intune nedir?](/intune/app-management).

> [!Tip]  
> Bu özellik ilk olarak sürüm 1806 ' de [yayın öncesi özelliği](../core/servers/manage/pre-release-features.md)olarak sunulmuştur. Sürüm 2002 ' den başlayarak, artık yayın öncesi bir özellik değildir.  
>
> Bu özellik, **ortak yönetilen cihazlar Için mobil uygulamalar**olarak özellik listesinde bulunabilir.<!-- 5849669 -->

Sürüm 1910 ' den başlayarak, Microsoft bağlı önbelleği Configuration Manager dağıtım noktalarınız üzerinde etkinleştirdiğinizde, bu kişiler artık Microsoft Intune Win32 uygulamalarını ortak yönetilen istemcilere sunabilir. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Uygulama iş yükleri için diyagram

:::image type="content" source="media/co-management-apps.svg" alt-text="Ortak yönetim uygulama iş yüklerinin diyagramı" lightbox="media/co-management-apps.svg":::

> [!TIP]
> Sürüm 2006 ' den başlayarak, Şirket Portalı Configuration Manager uygulamaları da gösterecek şekilde yapılandırabilirsiniz. Bu uygulama portalı deneyimini değiştirirseniz, Yukarıdaki diyagramda açıklanan davranışları değiştirir. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](company-portal.md).<!--CMADO-3601237,INADO-4297660-->

## <a name="known-issues"></a>Bilinen sorunlar

Endpoint Protection iş yükü Intune 'a taşındığında, istemci yine de Configuration Manager ve Microsoft Defender tarafından ayarlanan ilkeleri kabul edebilir. <!--5024559-->

Bu sorunu geçici olarak çözmek için, aşağıdaki adımları kullanarak, Intune ilkeleri istemci tarafından alındıktan sonra ConfigSecurityPolicy.exe kullanarak CleanUpPolicy.xml uygulayın:

1. Aşağıdaki metni kopyalayın ve olarak kaydedin `CleanUpPolicy.xml` .

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```

1. İçin yükseltilmiş bir komut istemi açın `ConfigSecurityPolicy.exe` . Genellikle bu yürütülebilir dosya aşağıdaki dizinlerden biridir:
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft güvenlik Istemcisi

1. Komut isteminden, ilkeyi temizlemek için XML dosyasını geçirin. Örneğin, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Sonraki adımlar

[İş yüklerini değiştirme](how-to-switch-workloads.md)