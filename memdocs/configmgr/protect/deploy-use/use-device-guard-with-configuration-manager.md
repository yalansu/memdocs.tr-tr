---
title: Windows Defender uygulama denetimini yönetme
titleSuffix: Configuration Manager
description: Windows Defender uygulama denetimini yönetmek için Configuration Manager nasıl kullanacağınızı öğrenin.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f9aff29d2773c4994272317d5fcd486b83cba8d7
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210188"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Configuration Manager ile Windows Defender uygulama denetimi yönetimi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

## <a name="introduction"></a>Giriş
Windows Defender uygulama denetimi bilgisayarları kötü amaçlı yazılımlara ve diğer güvenilmeyen yazılımlara karşı korumak için tasarlanmıştır. Yalnızca onaylanan kodun çalıştırılabilmesini sağlayarak kötü amaçlı kodun çalışmasını önler.

Windows Defender uygulama denetimi, bir bılgısayarda çalışmasına izin verilen yazılımın açık bir listesini zorlayan, yazılım tabanlı bir güvenlik katmanıdır. Uygulama denetiminde herhangi bir donanım veya bellenim önkoşulu yoktur. İle dağıtılan uygulama denetim ilkeleri, bu makalede özetlenen en düşük Windows sürümü ve SKU gereksinimlerini karşılayan hedeflenen koleksiyonlardaki bilgisayarlarda bir ilkeyi etkinleştirmek Configuration Manager. İsteğe bağlı olarak, Configuration Manager aracılığıyla dağıtılan uygulama Denetim ilkelerinin hiper yönetici tabanlı koruması, uyumlu donanımda grup ilkesi aracılığıyla etkinleştirilebilir.

Windows Defender uygulama denetimi hakkında daha fazla bilgi edinmek için, [Windows Defender uygulama denetimi dağıtım kılavuzu](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)' nu okuyun.

   > [!NOTE]
   > - Windows 10, sürüm 1709 ' den başlayarak, yapılandırılabilir kod bütünlüğü ilkeleri Windows Defender uygulama denetimi olarak bilinir.
   > - Configuration Manager sürüm 1710 ' den başlayarak, Device Guard ilkeleri Windows Defender uygulama denetim ilkeleri olarak yeniden adlandırıldı.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Configuration Manager ile Windows Defender uygulama denetimini kullanma

Windows Defender uygulama denetimi ilkesini dağıtmak için Configuration Manager kullanabilirsiniz. Bu ilke, Windows Defender uygulama denetimi 'nin bir koleksiyondaki bilgisayarlarda çalıştığı modu yapılandırmanızı sağlar. 

Aşağıdaki modlardan birini yapılandırabilirsiniz:

1. **Zorlama etkin** -yalnızca güvenilir yürütülebilir dosyaların çalıştırılmasına izin verilir.
2. **Yalnızca denetim** -tüm yürütülebilir dosyaların çalışmasına izin verir, ancak yerel istemci olay günlüğünde çalışan güvenilmeyen yürütülebilir dosyaları günlüğe kaydeder.

> [!Tip]  
> Bu özellik ilk olarak sürüm 1702 ' de [yayın öncesi özelliği](../../core/servers/manage/pre-release-features.md)olarak sunulmuştur. Sürüm 1906 ' den başlayarak, artık yayın öncesi bir özellik değildir.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Windows Defender uygulama denetimi ilkesini dağıtırken ne çalıştırılabilir?

Windows Defender uygulama denetimi, yönettiğiniz bilgisayarlarda nelerin çalışacağını kesin olarak denetlemenize olanak tanır. Bu özellik, yüksek güvenlikli departmanlardaki bilgisayarlar için yararlı olabilir; burada istenmeyen yazılımın çalıştırılabilmesi çok önemlidir.

Bir ilkeyi dağıttığınızda, genellikle aşağıdaki yürütülebilir dosyalar çalıştırılabilir:

- Windows işletim sistemi bileşenleri
- Donanım geliştirme merkezi sürücüleri (Windows Hardware Quality Labs imzaları vardır)
- Windows Mağazası uygulamaları
- Configuration Manager istemcisi 
- Windows Defender uygulama denetimi ilkesinden sonra bilgisayarları yükleyen Configuration Manager aracılığıyla dağıtılan tüm yazılımlar işlenir. 
- Windows bileşenlerine yönelik güncelleştirmeler:
    - Windows Update
    - İş İçin Windows Update
    - Windows Server Update Services
    - Configuration Manager
    - İsteğe bağlı olarak, Microsoft Intelligent Security Graph (ıSG) tarafından belirlendiği şekilde iyi bir saygınlığa sahip yazılım. ISG, Windows Defender SmartScreen ve diğer Microsoft hizmetlerini içerir. Bu yazılımın güvenilir olması için cihazın Windows Defender SmartScreen ve Windows 10 sürüm 1709 veya sonraki bir sürümü çalıştırması gerekir.

>[!IMPORTANT]
>Bu öğeler, Internet veya üçüncü taraf yazılım güncelleştirmelerinden, daha önce bahsedilen veya Internet 'ten bahsedilen güncelleştirme mekanizmalarından herhangi biri aracılığıyla yüklenip yüklenmediğini otomatik olarak güncelleştiren hiçbir *yazılım içermez.* Yalnızca Configuration Manager istemcisi çalıştırılabilir ancak dağıtılan yazılım değişiklikleri.

## <a name="before-you-start"></a>Başlamadan önce

Windows Defender uygulama denetim ilkelerini yapılandırmadan veya dağıtmadan önce, aşağıdaki bilgileri okuyun:

- Windows Defender uygulama denetimi yönetimi, Configuration Manager için yayın öncesi bir özelliktir ve değiştirilebilir.
- Windows Defender uygulama denetimi 'ni Configuration Manager ile kullanmak için yönettiğiniz bilgisayarların Windows 10 Enterprise sürüm 1703 veya üstünü çalıştırıyor olması gerekir.
- Bir ilke istemci bilgisayarında başarılı bir şekilde işlendikten sonra, Configuration Manager Bu istemcide yönetilen bir yükleyici olarak yapılandırılır. İlke işlemlerinden sonra, bu aracılığıyla dağıtılan yazılımlar otomatik olarak güvenilirdir. Windows Defender uygulama denetimi ilke işlemlerinden önce Configuration Manager tarafından yüklenen yazılımlar otomatik olarak güvenilir değildir.
- Dağıtım sırasında yapılandırılabilen uygulama denetim ilkelerine yönelik varsayılan uyumluluk değerlendirmesi zamanlaması, her gün bir gündür. İlke işlemede sorunlar gözlemleniyorsa, uyumluluk değerlendirme zamanlamasının örneğin her saat daha kısa olması için yapılandırılması faydalı olabilir. Bu zamanlama, bir hata oluşursa istemcilerin bir Windows Defender uygulama denetimi ilkesini işlemeye ne sıklıkta yanıt göndereceğini belirler.
- Seçtiğiniz zorlama modundan bağımsız olarak, bir Windows Defender Uygulama Denetim İlkesi dağıttığınızda, istemci bilgisayarlar HTML uygulamalarını. hta uzantısıyla çalıştıramaz.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Windows Defender uygulama denetim ilkesi oluşturma
1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.
2. **Varlıklar ve uyum** çalışma alanında **Endpoint Protection**' ı genişletin ve ardından **Windows Defender uygulama denetimi**' ne tıklayın.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Uygulama Denetim İlkesi Oluştur**' a tıklayın.
4. **Uygulama denetim Ilkesi oluşturma Sihirbazı**' nın **genel** sayfasında, aşağıdaki ayarları belirtin:
    - **Ad** -bu Windows Defender uygulama denetim ilkesi için benzersiz bir ad girin. 
    - **Açıklama** -isteğe bağlı olarak, ilke için Configuration Manager konsolunda tanımanıza yardımcı olacak bir açıklama girin.
    - **Bu ilkenin tüm işlemlerde zorlanabilmesi için cihazların yeniden başlatılmasını zorunlu kıl** -ilke BIR istemci bilgisayarda işlendikten sonra, **bilgisayar yeniden başlatma**için **istemci ayarlarına** göre istemcide yeniden başlatma zamanlanır.
        - Windows 10 sürüm 1703 veya öncesini çalıştıran cihazlar her zaman otomatik olarak yeniden başlatılır.
        - Windows 10 sürüm 1709 ' den başlayarak, cihazda çalışmakta olan uygulamalara yeni uygulama denetim ilkesi, yeniden başlatmadan sonra bu uygulamalara uygulanmaz. Ancak, ilke uygulandıktan sonra başlatılan uygulamalar yeni uygulama denetimi ilkesini kabul eder. 
    - **Zorlama modu** -Istemci bilgisayarda Windows Defender uygulama denetimi için aşağıdaki zorlama yöntemlerinden birini seçin.
        - **Zorlama etkin** -yalnızca güvenilir yürütülebilirlerin çalışmasına izin verilir.
        - **Yalnızca denetim** -tüm yürütülebilir dosyaların çalışmasına izin verir, ancak yerel istemci olay günlüğünde çalışan güvenilmeyen yürütülebilir dosyaları günlüğe kaydeder.
5. **Uygulama denetim Ilkesi oluşturma Sihirbazı**'nın **içermeler** sekmesinde, **Intelligent Security Graph tarafından güvenilen yazılımları yetkilendirmek**istediğinizi seçin.
6. Bilgisayarlarda belirli dosyalar veya klasörler için güven eklemek istiyorsanız **Ekle** ' ye tıklayın. **Güvenilen dosya veya klasör ekle** iletişim kutusunda, güvenilecek yerel bir dosya veya klasör yolu belirtebilirsiniz. Ayrıca, bağlanmak için izninizin olduğu uzak bir cihazda bir dosya veya klasör yolu belirtebilirsiniz. Belirli dosyalar veya klasörler için bir Windows Defender uygulama denetimi ilkesinde güven eklediğinizde şunları yapabilirsiniz:
    - Yönetilen yükleyici davranışları ile ilgili sorunları aşmak
    - Configuration Manager ile dağıtılabilecek iş kolu uygulamalarına güvenin
    - Bir işletim sistemi dağıtım görüntüsüne dahil olan uygulamalara güvenin. 
8. Sihirbazı tamamladıktan **sonra ileri**' ye tıklayın.

>[!IMPORTANT]
>Güvenilen dosyaların veya klasörlerin eklenmesi yalnızca Configuration Manager istemcisinin 1706 veya sonraki bir sürümünü çalıştıran istemci bilgisayarlarda desteklenir. Bir Windows Defender uygulama denetim ilkesine ekleme kuralları varsa ve ilke daha sonra Configuration Manager istemcisinde daha önceki bir sürümü çalıştıran bir istemci BILGISAYARA dağıtılırsa, ilke uygulanmaz. Bu eski istemcileri yükseltmek bu sorunu çözmeyecektir. Ekleme kuralları içermeyen ilkeler, Configuration Manager istemcisinin eski sürümlerine de uygulanabilir.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Windows Defender uygulama denetim ilkesi dağıtma
1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.
2. **Varlıklar ve uyum** çalışma alanında **Endpoint Protection**' ı genişletin ve ardından **Windows Defender uygulama denetimi**' ne tıklayın.
3. İlke listesinden, dağıtmak istediğiniz birini seçin ve ardından **giriş** sekmesinde, **dağıtım** grubunda, **uygulama denetim ilkesini dağıt**' ı tıklatın.
4. **Uygulama denetim Ilkesini dağıt** iletişim kutusunda, ilkeyi dağıtmak istediğiniz koleksiyonu seçin. Ardından, istemcilerin ilkeyi değerlendirmesi için bir zamanlama yapılandırın. Son olarak, istemcinin ilkeyi yapılandırılmış herhangi bir bakım penceresi dışında değerlendiremeyeceğini seçin.
5. İşiniz bittiğinde, ilkeyi dağıtmak için **Tamam** ' ı tıklatın. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Windows Defender uygulama denetimi ilkesini izleme

Dağıtılan ilkenin tüm bilgisayarlara doğru şekilde uygulandığını izlemenize yardımcı olması için [Uyumluluk ayarlarını izle](../../compliance/deploy-use/monitor-compliance-settings.md) makalesindeki bilgileri kullanın.

Bir Windows Defender uygulama denetim ilkesinin işlenmesini izlemek için, istemci bilgisayarlarda aşağıdaki günlük dosyasını kullanın:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Engellenen veya denetlenen belirli yazılımların doğrulanması için aşağıdaki yerel istemci olay günlüklerine bakın:

1. Yürütülebilir dosyaların engellenmesi ve denetlenmesi için, **uygulama ve hizmet günlükleri** > **Microsoft** > **Windows** > **kod bütünlüğü** > **işletimsel**' i kullanın.
2. Windows Installer ve betik dosyalarının engellenmesi ve denetlenmesi için, **uygulama ve hizmet günlükleri** > **Microsoft** > **Windows** > **AppLocker** > **MSI ve betiği**kullanın.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Windows Defender uygulama denetimi için güvenlik ve gizlilik bilgileri

- Bu yayın öncesi sürümünde, Windows Defender uygulama denetim ilkelerini **yalnızca** bir üretim ortamında zorlama modu denetimiyle dağıtmayın. Bu mod, özelliği yalnızca bir laboratuvar ayarında test etmenize yardımcı olmaya yöneliktir.
- İlke zorlamak için **yalnızca Audit** veya **zorlama etkinleştirilmiş** modda dağıtılan bir ilkeye sahip olan cihazlar, yüklü güvenilir olmayan yazılımlarla savunmasızdır.
Bu durumda, cihaz yeniden başlatıldığında veya **zorlama etkinleştirilmiş** modda bir ilke alırsa yazılımın çalıştırılmasına izin verilmeye devam edebilir.
- Windows Defender uygulama denetimi ilkesinin etkin olduğundan emin olmak için cihazı laboratuvar ortamında hazırlayın. Ardından, **zorlama etkin** ilkesini dağıtın ve son olarak, cihazı son kullanıcıya vermeden önce cihazı yeniden başlatın.
- **Zorlama etkin**bir ilke dağıtmayın ve daha sonra **yalnızca** aynı cihaza sahip bir ilkeyi bir ilke ile dağıtın. Bu yapılandırma, güvenilmeyen yazılımın çalıştırılmasına izin verilmesini sağlayabilir.
- İstemci bilgisayarlarda Windows Defender uygulama denetimi 'ni etkinleştirmek için Configuration Manager kullandığınızda, ilke yerel yönetici haklarına sahip kullanıcıların uygulama denetim ilkelerini atlamasını veya aksi takdirde Güvenilmeyen yazılım yürütmesini engellemez. 
- Yerel yönetici haklarına sahip kullanıcıların uygulama denetimini devre dışı bırakmasına engel olmanın tek yolu, imzalı ikili bir ilke dağıtmaktır. Bu dağıtım grup ilkesi aracılığıyla yapılabilir ancak şu anda Configuration Manager desteklenmiyor.
- İstemci bilgisayarlarda yönetilen bir yükleyici olarak Configuration Manager ayarlama, AppLocker İlkesi kullanır. AppLocker yalnızca yönetilen yükleyicileri tanımlamak için kullanılır ve tüm zorlama Windows Defender uygulama denetimi ile gerçekleştirilir. 

## <a name="next-steps"></a>Sonraki adımlar

 [Kötü amaçlı yazılımdan koruma ilkelerini ve güvenlik duvarı ayarlarını yönetme](endpoint-antimalware-firewall.md)



