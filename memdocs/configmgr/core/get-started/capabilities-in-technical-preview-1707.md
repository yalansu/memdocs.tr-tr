---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1707 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9ea860568d7f094588e628955f128e5b8a3aa154
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995424"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Configuration Manager için Technical Preview 1707 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1707 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Bu teknik önizlemede bilinen sorunlar:**
- **Pasif modda bir site sunucunuz varsa, Preview sürüm 1707 ' e güncelleştirme başarısız olur**. Önizleme sürümü 1706 ' i çalıştırdığınızda ve [pasif modda bir birincil site sunucusuna](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)sahip olduğunuzda, önizleme sitenizi sürüm 1707 ' ye başarıyla güncelleştirebilmeniz için Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz sürüm 1707 ' i çalıştırdıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
  2. **Site sistemi rolleri** bölmesinde, **site sunucusu** rolüne sağ tıklayın ve ardından **rolü kaldır**' ı seçin.
  3. Pasif mod site sunucusuna sağ tıklayın ve ardından **Sil**' i seçin.
  4. Site sunucusu kaldırıldıktan sonra, etkin birincil site sunucusunda hizmeti **CONFIGURATION_MANAGER_UPDATE**yeniden başlatın.



**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-microsoft-365"></a>Windows 10 ve Microsoft 365 için hızlı yükleme dosyaları için istemci eş önbelleği desteği
<!-- 1352486 -->
Bu sürümden itibaren, eş önbellek Windows 10 için içerik hızlı yükleme dosyalarının dağıtımını ve Microsoft 365 için güncelleştirme dosyalarını destekler. Ek yapılandırma gerekmez.

## <a name="surface-device-dashboard"></a>Surface cihaz panosu
<!--1355788-->
Surface cihaz panosu, ortamınızda bulunan yüzey cihazları hakkında bilgi sağlar. Konsolunda, **izleme**  >  **yüzeyi cihazları**' na gidin. Aşağıdakileri görebilirsiniz:
- Yüzey yüzdesi
- Yüzey modellerinin yüzdesi
- ilk beş işletim sistemi sürümü

Cihazların tüm listesi için **yüzey modelleri** grafiğinin bir bölümüne tıklayın.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Windows Defender Application Guard ilkelerini yapılandırma ve dağıtma
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) , güvenilir olmayan Web sitelerini işletim sisteminin diğer bölümleri tarafından erişilemeyen güvenli bir yalıtılmış kapsayıcıda açarak kullanıcılarınızı korumaya yardımcı olan yeni bir Windows özelliğidir. Bu Technical Preview sürümünde, yapılandırdığınız Configuration Manager uyumluluk ayarlarını kullanarak bu özelliği yapılandırmak ve ardından bir koleksiyona dağıtmak için destek ekledik. Bu özellik, Windows 10 Fall oluşturucusunun güncelleştirme 64 bit sürümü (kod adı: RS3) için önizleme aşamasında kullanıma sunulacaktır. Bu özelliği şimdi test etmek için bu güncelleştirmenin bir önizleme sürümünü kullanıyor olmanız gerekir.

### <a name="before-you-start"></a>Başlamadan önce

Windows Defender Application Guard ilkeleri oluşturup dağıtmak için, ilkeyi dağıttığınız Windows 10 cihazlarının bir ağ yalıtımı ilkesiyle yapılandırılması gerekir. Daha ayrıntılı bilgi için [Bu blog gönderisine](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)bakın. Bu özellik yalnızca geçerli Windows 10 Insider Derlemeleriyle birlikte kullanılabilir. Bunu test etmek için istemcileriniz son Windows 10 Insider derlemesini çalıştırıyor olmalıdır.

### <a name="try-it-out"></a>Deneyin!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Bir ilke oluşturmak ve kullanılabilir ayarlara gitmek için:

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**' i seçin.
2. **Varlıklar ve uyum** çalışma alanında, **Overview**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**Endpoint Protection genel bakış ' ı seçin.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Windows Defender Application Guard İlkesi Oluştur**' a tıklayın.
4. Blog gönderisini başvuru olarak kullanarak, özelliği denemek için kullanılabilir ayarları gözden geçirin ve yapılandırabilirsiniz.
5. Bu sürümde, sihirbaza yeni **ağ tanımı** sayfasını ekledik. Bu sayfada, kurumsal kimlik ' i belirtin ve kurumsal ağ sınırınızı tanımlayın.<br>Windows 10 bilgisayarları, istemcide yalnızca bir ağ yalıtımı listesini depolar. Bu sürümde, iki farklı türde ağ yalıtımı listesi (biri Windows Information Protection, diğeri Windows Defender Application Guard 'dan) oluşturabilir ve bunları istemciye dağıtabilirsiniz. Her iki ilkeyi de dağıtırsanız, bu ağ yalıtımı listelerinin eşleşmesi gerekir. Aynı istemciyle eşleşmeyen listeler dağıtırsanız, dağıtım başarısız olur.
[Windows Information Protection belgelerinde](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)ağ tanımlarını belirtme hakkında daha fazla bilgi edinebilirsiniz.

6. İşiniz bittiğinde Sihirbazı doldurun ve ilkeyi bir veya daha fazla Windows 10 cihazına dağıtın.

### <a name="further-reading"></a>Daha fazla bilgi
Windows Defender Application Guard hakkında daha fazla bilgi edinmek için [Bu blog gönderisine](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)bakın. Ayrıca, Windows Defender Application Guard tek başına modu hakkında daha fazla bilgi edinmek için [Bu blog gönderisine](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)bakın.

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Configuration Manager PowerShell betikleri dağıtırken parametreler ekleme

<!-- 1236459 --->

Son Technical Preview 'da, [Configuration Manager konsolundan PowerShell betikleri oluşturmanıza ve çalıştırmanıza](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)olanak sağlayan yeni bir özellik sunuyoruz.
Bu teknik önizlemede bu özelliği genişlettik. Configuration Manager artık PowerShell betiğini okur ve betik oluşturma sihirbazında tüm parametreleri görüntüler. Sihirbazda, komut dosyası çalıştırıldığında kullanılacak parametre için bir değer sağlayabilirsiniz. Alternatif olarak, parametresini boş bırakabilirsiniz. Bunu yaparsanız, komut dosyasını çalıştırdığınızda parametresi için bir değer sağlamanız gerekir.
Bu teknik önizlemede, bir betiğin gerektirdiği tüm parametreleri sağlamanız gerekir. Gelecekteki bir sürümde, komut dosyası parametrelerinin isteğe bağlı olarak kullanılmasını planlıyoruz.

### <a name="try-it-out"></a>Deneyin!

1. [Configuration Manager konsolundan PowerShell betikleri oluşturmak ve çalıştırmak](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)için yönergeleri izleyin.
2. **Betik oluşturma sihirbazının**yeni **betik parametreleri** sayfasında bir parametre seçin ve ardından **Düzenle**' ye tıklayın.
3. Seçili parametre için bir parametre değeri sağlayın ve ardından **Tamam**' a tıklayın.
4. Sihirbazı tamamlayın.

Betik çalıştırıldığında, yapılandırdığınız tüm parametre değerlerini kullanır.