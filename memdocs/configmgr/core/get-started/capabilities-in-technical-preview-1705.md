---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1705 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0a10726062d679666d14cbbb0b87510af5dfe30c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078813"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Configuration Manager için Technical Preview 1705 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1705 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.    

**Bu teknik önizlemede bilinen sorunlar:**
-   **Operations Manager Suite Bağlayıcısı yükseltmez**. OMS Bağlayıcısı yapılandırılmış olan Technical Preview 'ın önceki bir sürümünden yükselttiğinizde, bu bağlayıcı yükseltilmemiştir ve konsolda artık kullanılamaz. Yükseltmeden sonra, [Azure Hizmetleri Sihirbazı 'nı kullanmanız](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) ve OMS çalışma alanınıza yeniden bağlantı kurmanız gerekir.
-   **Yüzey sürücüleri başarıyla eşitlenmez**. Surface sürücüleri için destek, Technical Preview için Configuration Manager konsolundaki **Yenilikler bölümünde listelense de,** bu özellik henüz beklendiği gibi çalışmaz.
-   **İş erteleme ilkeleri için Windows Update**oluşturulamıyor. Iş erteleme ilkeleri için Windows Update yapılandırma özelliği, Technical Preview için Configuration Manager konsolundaki **Yenilikler bölümünde listelense de,** sihirbaz açılmaz ve herhangi bir ilkeyi yapılandıraamamış olursunuz.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Sıfırlama aracını güncelleştirme  
Konsol içi güncelleştirmelerin indirme veya çoğaltma sorunları olduğunda sorunları gidermek için **Cmupdatereset. exe**Configuration Manager güncelleştirme sıfırlama aracını kullanabilirsiniz. Bu araç, Technical Preview sürüm 1705 ' ye eklenmiştir. Önizlemeyi, \CD.exe ' ye yükledikten sonra Technical Preview sitenizin site sunucusunda, \ \. ***Latest\smssetup\tools*** klasörüne bulabilirsiniz.

Bu aracı Teknik Önizleme sürümleri 1606 veya sonrası ile birlikte kullanabilirsiniz. Bu geriye doğru destek, aracın bir dizi teknik önizleme güncelleştirme senaryolarıyla kullanılabilmesi ve sonraki Teknik Önizleme kullanılabilir hale gelene kadar beklemeniz gerekmeden sağlanır.

Konsol içi bir güncelleştirme henüz yüklenmemişse ve hatalı durumdaysa bu aracı kullanabilirsiniz. Hatalı bir durum, güncelleştirme indirmenin devam ediyor, ancak takılı ve çok uzun sürebileceği anlamına gelebilir, bu da benzer boyuttaki güncelleştirme paketlerine ait geçmiş beklentilerinden daha uzun sürebilir. Güncelleştirme, alt birincil sitelere çoğaltılmak için de bir hata olabilir.  

Aracı çalıştırdığınızda, belirttiğiniz güncelleştirmede karşı çalışır. Araç, varsayılan olarak, başarıyla yüklenen veya indirilen güncelleştirmeleri silmez.  

### <a name="prerequisites"></a>Önkoşullar
Aracı çalıştırmak için kullandığınız hesap aşağıdaki izinleri gerektirir:
-   Merkezi yönetim sitesinin ve hiyerarşinizdeki her birincil sitenin site veritabanı için **okuma** ve **yazma** izinleri. Bu izinleri ayarlamak için, Kullanıcı hesabını **db_datawriter** bir üyesi olarak ekleyebilir ve her bir sitenin Configuration Manager veritabanına **db_datareader** [sabit veritabanı rolleri](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) ekleyebilirsiniz. Araç ikincil sitelerle etkileşime girmiyor.
-   Hiyerarşinizin en üst düzey sitesinde **yerel yönetici** .
-   Hizmet bağlantı noktasını barındıran bilgisayarda **yerel yönetici** .

Sıfırlamak istediğiniz güncelleştirme paketinin GUID 'sine ihtiyacınız olacak. GUID 'yi almak için:
-   Konsolunda, **Yönetim** > **güncelleştirmeleri ve bakım** ' a gidin ve ardından görüntü bölmesinde sütunlardan birinin başlığına ( **durum**gibi) sağ tıklayın ve ardından **paket GUID**' yi seçin. Bu sütun, görüntülenecek sütunu ekler ve sütunda güncelleştirme paketi GUID 'SI gösterilir.

> [!TIP]  
> GUID 'yi kopyalamak için, sıfırlamak istediğiniz güncelleştirme paketinin satırını seçin ve ardından CTRL + C tuşlarını kullanarak bu satırı kopyalayın. Kopyalanmış seçiminizi bir metin düzenleyicisine yapıştırırsanız, aracı çalıştırdığınızda yalnızca bir komut satırı parametresi olarak kullanılacak GUID 'yi kopyalayabilirsiniz.

### <a name="run-the-tool"></a>Aracı çalıştırma    
Aracın hiyerarşinin en üst düzey sitesinde çalıştırılması gerekir.

Aracı çalıştırdığınızda, hiyerarşide en üst katman sitesinde, site veritabanı adından ve sıfırlamak istediğiniz güncelleştirme paketinin GUID 'sinin SQL Server belirtmek için komut satırı parametrelerini kullanırsınız. Araç daha sonra, güncelleştirmelerin durumuna göre erişmesi gereken ek sunucuları tanımlar.   

Güncelleştirme paketi *karşıdan yükleme sonrası* durumundaysa, araç paketi temizlemez. Bir seçenek olarak, başarıyla indirilen bir güncelleştirmenin zorla silmeyi zorla parametresini kullanarak kaldırmayı zorlayabilirsiniz (Bu konunun ilerleyen kısımlarında komut satırı parametrelerine bakın).

Araç çalıştıktan sonra:
-   Bir paket silinmişse, en üst katman siteleri SMS_Executive hizmeti 'ni yeniden başlatın ve sonra paketi indirmek için güncelleştirmeleri denetleyin.
-   Bir paket silinmediği takdirde, güncelleştirme yeniden başlatılır ve çoğaltma veya yükleme yeniden başlatılır.

**Komut satırı parametreleri:**  


|                        Parametre                         |                                                            Açıklama                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;en üst katman sitenizin SQL Server FQDN 'si>** | *Gerekli* <br> Hiyerarşinizin üst katman sitesi için site veritabanını barındıran SQL Server FQDN belirtmeniz gerekir. |
|                **-D &lt;veritabanı adı>**                 |                             *Gerekli* <br> Üst katman siteleri veritabanının adını belirtmeniz gerekir.                             |
|                 **-P &lt;paketi GUID>**                 |                        *Gerekli* <br> Sıfırlamak istediğiniz güncelleştirme paketi için GUID 'YI belirtmeniz gerekir.                        |
|           **-I &lt;SQL Server örnek adı>**           |                   *İsteğe Bağlı* <br> Site veritabanını barındıran SQL Server örneğini tanımlamak için bunu kullanın.                   |
|                       **-FDELETE**                       |                      *İsteğe Bağlı* <br> Başarıyla indirilen bir güncelleştirme paketinin silinmesini zorlamak için bunu kullanın.                      |

 **Örnekler**  
 Tipik bir senaryoda, indirme sorunları olan bir güncelleştirmeyi sıfırlamak istersiniz. SQL Server FQDN 'niz *server1.fabrikam.com*, site veritabanı *CM_XYZ*ve paket GUID 'si *61F16b3c-f1f6-4f9f-8647-2a524b0c802c*olur.  Şunu çalıştırırsınız: ***Cmupdatereset. exe-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 Daha Extreme bir senaryoda sorunlu güncelleştirme paketinin silinmesini zorlamak isteyebilirsiniz. SQL Server FQDN 'niz *server1.fabrikam.com*, site veritabanı *CM_XYZ*ve paket GUID 'si *61F16b3c-f1f6-4f9f-8647-2a524b0c802c*olur.  Şunu çalıştırırsınız: ***Cmupdatereset. exe-FDELETE-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Teknik Önizleme ile aracı test edin  
Bu aracı Teknik Önizleme sürümleri 1606 veya sonrası ile birlikte kullanabilirsiniz. Bu geriye doğru destek, aracın daha fazla sayıda teknik önizleme güncelleştirme senaryolarıyla kullanılabilmesi için, sonraki Technical Preview sürümü kullanılabilir olana kadar beklemek zorunda kalmadan sağlanır.

Bu güncelleştirme önkoşul denetimini tamamlamadan önce teknik önizleme için bir güncelleştirme paketinde aracı çalıştırın. Tamamlanmış bir önkoşul denetimi durumu, **Yönetim** > **güncelleştirmeleri ve bakımı**'ndaki paket için aşağıdaki durum ile tanımlanır:  
-   **Önkoşul denetimi başarılı**
-   **Önkoşul denetimi uyarıyla geçti**
-   **Önkoşul denetimi başarısız oldu**


## <a name="high-dpi-console-support"></a>Yüksek DPı konsol desteği

Bu sürümle birlikte, Configuration Manager konsolunun, yüksek DPı cihazlarda (yüzey defteri gibi) görüntülendiğinde, Kullanıcı arabiriminin farklı kısımlarını ölçeklendirdiği ve gösterdiği sorunlar düzeltilmelidir.


## <a name="peer-cache-improvements"></a>Eş önbellek geliştirmeleri
Bu Technical Preview sürümünden itibaren, eş önbellek artık eşlerden gelen indirme isteklerinin kimliğini doğrulamak için [ağ erişim hesabını kullanmaz](../plan-design/hierarchy/client-peer-cache.md) .


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>SQL Server Always on kullanılabilirlik gruplarında iyileştirmeler  
Bu sürümle birlikte, artık Configuration Manager kullandığınız SQL Server Always on kullanılabilirlik gruplarında zaman uyumsuz tamamlama çoğaltmaları kullanabilirsiniz.  Bu, site dışı (uzak) yedeklemeler olarak kullanmak üzere kullanılabilirlik gruplarınıza ek çoğaltmalar ekleyebileceğiniz ve sonra bunları bir olağanüstü durum kurtarma senaryosunda kullanabileceğiniz anlamına gelir.  

- Configuration Manager, zaman uyumlu çoğaltmanızı kurtarmak için zaman uyumsuz tamamlama çoğaltmasını kullanmayı destekler.  Bunun nasıl yapılacağını öğrenmek için yedekleme ve kurtarma konusundaki [site veritabanı kurtarma seçenekleri](../servers/manage/recover-sites.md#site-database-recovery-options) bölümüne bakın.

- Bu sürüm, site veritabanınız olarak zaman uyumsuz tamamlama çoğaltmasını kullanmak için yük devretmeyi desteklemez.
  > [!CAUTION]  
  > Configuration Manager, zaman uyumsuz tamamlama çoğaltmasının durumunu doğrulamak için geçerli olduğundan emin olmak için, bu [tür bir çoğaltma eşitlenmemiş](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes)olabilir ve site veritabanı, site veritabanının bütünlüğünü ve verilerinizi riske koyabildiğinden zaman uyumsuz bir çoğaltma çoğaltmasının kullanımını eşzamanlı hale getirebilirsiniz.  

- Bir kullanılabilirlik grubunda, kullandığınız SQL Server sürümü tarafından desteklenen aynı sayıda ve türde çoğaltmaları kullanabilirsiniz.   (Önceki destek iki eşzamanlı kayıt çoğaltmalarıyla sınırlandırılmıştır.)

### <a name="configure-an-asynchronous-commit-replica"></a>Zaman uyumsuz bir kayıt çoğaltması yapılandırma
[Configuration Manager ile kullandığınız bir kullanılabilirlik grubuna](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)zaman uyumsuz bir çoğaltma eklemek için, zaman uyumlu çoğaltma yapılandırmak için gereken yapılandırma betiklerini çalıştırmanız gerekmez. (Bunun nedeni, site veritabanı olarak o zaman uyumsuz çoğaltmanın kullanılması desteklenmez.) Kullanılabilirlik gruplarına ikincil çoğaltmalar ekleme hakkında bilgi edinmek için [SQL Server belgelerine](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) bakın.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Sitenizi kurtarmak için zaman uyumsuz çoğaltmayı kullanın
Site veritabanınızı kurtarmak için zaman uyumsuz bir çoğaltma kullanmadan önce, site veritabanına ek yazmaları engellemek için etkin birincil siteyi durdurmanız gerekir. Siteyi durdurduktan sonra, [el ile kurtarılan bir veritabanını](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered)kullanmak yerine zaman uyumsuz bir çoğaltma kullanabilirsiniz.

Siteyi durdurmak için, site sunucusundaki önemli hizmetleri durdurmak için [Hiyerarşi Bakımı aracını](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) kullanabilirsiniz. Komut satırını kullanın: **Preinst. exe/STOPSITE**   

Siteyi durdurma, site sunucusundaki SMS_Executive hizmeti tarafından izlenen Site Bileşen Yöneticisi hizmeti 'nin (Sitecomp) durdurulmasına eşdeğerdir.


## <a name="improved-user-notifications-for-office-365-updates"></a>Office 365 güncelleştirmeleri için geliştirilmiş Kullanıcı bildirimleri
Bir istemci Office 365 güncelleştirmesi yüklediğinde Office Tıkla-Çalıştır Kullanıcı deneyiminden yararlanmak için geliştirmeler yapılmıştır. Bu, açılır ve uygulama içi bildirimleri ve geri sayım deneyimini içerir. Bu sürümden önce, bir istemciye Office 365 güncelleştirmesi gönderildiğinde, açık olan Office uygulamaları uyarı vermeden otomatik olarak kapatılır. Bu güncelleştirmeden sonra Office uygulamaları artık beklenmedik şekilde kapanmayacaktır.

### <a name="prerequisites"></a>Önkoşullar
Bu güncelleştirme, Office 365 ProPlus istemcileri için geçerlidir.

### <a name="known-issues"></a>Bilinen sorunlar
Bir istemci Office 365 güncelleştirme atamasını ilk kez değerlendirirken ve güncelleştirmenin geçmişte zamanlanan, hemen zamanlanan veya 30 dakika içinde zamanlanan bir son tarih olduğunda, Office 365 kullanıcı deneyimi tutarsız olabilir. Örneğin, istemci güncelleştirme için 30 dakikalık bir geri sayım iletişim kutusu alabilir, ancak gerçek uygulama geri sayım sonundan önce başlayabilir. Bu davranışı önlemek için aşağıdakileri göz önünde bulundurun:
- Office 365 güncelleştirmesini, geçerli zamandan önce 60 dakikadan daha fazla süreyle zamanlanan bir son tarihle dağıtın.
- Koleksiyonda iş dışı saatlerde bir bakım penceresi yapılandırın veya dağıtımda bir zorlama yetkisiz kullanım süresi yapılandırın.

### <a name="try-it-out"></a>Deneyin!
Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için şeridin **giriş** sekmesinden bize **geri bildirim** gönderin:
- Son tarihi geçerli zamandan önce en az 60 dakika sonra ayarlanmış bir istemciye Office 365 güncelleştirmesi olan bir istemciye dağıtın. İstemcideki yeni davranışı gözlemleyin.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Windows Defender Application Guard ilkelerini yapılandırma ve dağıtma

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) , güvenilir olmayan Web sitelerini işletim sisteminin diğer bölümleri tarafından erişilemeyen güvenli bir yalıtılmış kapsayıcıda açarak kullanıcılarınızı korumaya yardımcı olan yeni bir Windows özelliğidir. Bu Technical Preview sürümünde, yapılandırdığınız Configuration Manager uyumluluk ayarlarını kullanarak bu özelliği yapılandırmak ve ardından bir koleksiyona dağıtmak için destek ekledik.
Bu özellik, Windows 10 Creator güncelleştirmesinin 64 bit sürümü için önizleme aşamasında kullanıma sunulacaktır. Bu özelliği şimdi test etmek için bu güncelleştirmenin bir önizleme sürümünü kullanıyor olmanız gerekir.


### <a name="before-you-start"></a>Başlamadan önce

Windows Defender Application Guard ilkeleri oluşturup dağıtmak için, ilkeyi dağıttığınız Windows 10 cihazlarının bir ağ yalıtımı ilkesiyle yapılandırılması gerekir. Daha fazla ayrıntı için, daha sonra başvurulan blog gönderisine bakın.
Bu özellik yalnızca geçerli Windows 10 Insider Derlemeleriyle birlikte kullanılabilir. Bunu test etmek için istemcileriniz son Windows 10 Insider derlemesini çalıştırıyor olmalıdır.

### <a name="try-it-out"></a>Deneyin!

Windows Defender Application Guard hakkındaki temel bilgileri anlamak için blog gönderisini okuduğunuzdan emin olun.

Bir ilke oluşturmak ve kullanılabilir ayarlara gitmek için:

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk**' i seçin.
2.  **Varlıklar ve uyum** çalışma alanında,**Windows Defender Application Guard****Endpoint Protection** >  **genel bakış** > ' ı seçin.
3.  **Giriş** sekmesinde, **Oluştur** grubunda, **Windows Defender Application Guard İlkesi Oluştur**' a tıklayın.
4.  Blog gönderisini başvuru olarak kullanarak, özelliği denemek için kullanılabilir ayarları gözden geçirin ve yapılandırabilirsiniz.
5.  İşiniz bittiğinde Sihirbazı doldurun ve ilkeyi bir veya daha fazla Windows 10 cihazına dağıtın.

### <a name="further-reading"></a>Daha fazla bilgi

Windows Defender Application Guard hakkında daha fazla bilgi edinmek için [Bu blog gönderisine]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)bakın.
Ayrıca, Windows Defender Application Guard tek başına modu hakkında daha fazla bilgi edinmek için [Bu blog gönderisine](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)bakın.




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Azure AD ve bulut yönetimi için yeni yetenekler

Bu sürümde, aşağıdaki senaryoyu desteklemek için bulut hizmetleri 'ni Azure AD kullanacak şekilde yapılandırabilirsiniz:

- Configuration Manager istemcisini Internet 'ten el ile yüklemek ve bir Configuration Manager sitesine atamasını sağlamak.
- Configuration Manager istemcisini Internet 'teki cihazlara dağıtmak için Intune 'U kullanın.

### <a name="advantages"></a>Yararları

Cloud Services ve Azure AD 'nin kullanılması, istemci kimlik doğrulama sertifikalarını kullanma gereksinimini ortadan kaldırır.

Azure AD kullanıcılarını, koleksiyonlarda ve diğer Configuration Manager işlemlerinde kullanmak üzere sitenizde bulabilirsiniz.

### <a name="before-you-start"></a>Başlamadan önce

- Bir Azure AD kiracısına sahip olmanız gerekir.
- Cihazlarınız Windows 10 çalıştırmalıdır ve Azure AD 'ye katılmış olmalıdır.  İstemciler ayrıca, Azure AD 'ye katılmış olarak etki alanına katılmış olabilir.
- Yönetim noktası site sistemi rolü için [mevcut önkoşullara](../plan-design/configs/site-and-site-system-prerequisites.md) ek olarak, bu site sistem rolünü barındıran bilgisayarda **ASP.NET 4,5** (ve bu ile otomatik olarak seçilen tüm seçenekler) seçeneklerinin de etkinleştirildiğinden emin olmanız gerekir.
- Configuration Manager istemcisini dağıtmak üzere Microsoft Intune kullanmak için:
    - Çalışan bir Intune kiracısına sahip olmanız gerekir (Configuration Manager ve Intune 'un bağlı olması gerekmez).
    - Intune 'da, Configuration Manager istemcisini içeren bir uygulama oluşturdunuz ve dağıttınız. Bunun nasıl yapılacağı hakkında ayrıntılı bilgi için bkz. Intune MDM ile yönetilen Windows cihazlarına istemci yüklemesi.
- İstemciyi dağıtmak için Configuration Manager kullanmak için:
    - En az bir yönetim noktasının HTTPS modu için yapılandırılması gerekir.
    - Bir Bulut Yönetimi Ağ Geçidi ayarlamanız gerekir.


### <a name="set-up-the-cloud-management-gateway"></a>Bulut Yönetimi Ağ Geçidi ayarlama

İstemcilerin, sertifikaları kullanmadan Configuration Manager sitenize internet 'ten erişmesine izin vermek için Bulut Yönetimi Ağ Geçidi ayarlayın.

Aşağıdaki konularda bunun nasıl yapılacağı hakkında yardım bulacaksınız:

- [Configuration Manager 'de bulut yönetimi ağ geçidini planlayın](../clients/manage/cmg/plan-cloud-management-gateway.md).
- [Configuration Manager için bulut yönetimi ağ geçidini ayarlayın](../clients/manage/cmg/setup-cloud-management-gateway.md).
- [Configuration Manager 'de bulut yönetimi ağ geçidini izleyin](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configuration Manager Cloud Services Azure Hizmetleri uygulamasını ayarlama

Bu, Configuration Manager sitenizi Azure AD 'ye bağlar ve bu bölümdeki tüm diğer işlemler için bir önkoşuldur. Bunu yapmak için:

1. Configuration Manager konsolunun **Yönetim** çalışma alanında **Cloud Services**' i genişletin ve ardından **Azure hizmetleri**' ne tıklayın.
2. **Giriş** sekmesinde, **Azure hizmetleri** grubunda, **Azure hizmetlerini yapılandır**' ı tıklatın.
3. Azure Hizmetleri Sihirbazı 'nın Azure **Hizmetleri** sayfasında, ISTEMCILERIN Azure AD 'yi kullanarak hiyerarşiyle kimlik doğrulamasına izin vermek Için **bulut yönetimi** ' ni seçin.
4. Sihirbazın **genel** sayfasında, bir ad ve Azure hizmetiniz için bir açıklama belirtin.
5. Sihirbazın **uygulama** sayfasında, listeden Azure ortamınızı seçin ve ardından, Azure hizmetini yapılandırmak için kullanılacak sunucu ve istemci uygulamalarını seçmek üzere **Araştır** ' a tıklayın:
   - **Sunucu uygulaması** penceresinde, kullanmak istediğiniz sunucu uygulamasını seçin ve ardından **Tamam**' a tıklayın. Sunucu uygulamaları, kiracı KIMLIĞINIZ, Istemci KIMLIĞINIZ ve istemciler için gizli anahtar dahil olmak üzere Azure hesabınıza yönelik yapılandırmaların bulunduğu Azure Web Apps ' dir. Kullanılabilir bir sunucu uygulamanız yoksa, aşağıdakilerden birini kullanın:
       - **Oluştur**: yeni bir sunucu uygulaması oluşturmak için **Oluştur**' a tıklayın. Uygulama ve kiracı için kolay bir ad sağlayın. Ardından, Azure 'da oturum açtıktan sonra, Web uygulaması ile kullanmak üzere Istemci KIMLIĞI ve gizli anahtar dahil olmak üzere Azure 'da Web uygulaması oluşturur Configuration Manager. Daha sonra, bunları Azure portal görüntüleyebilirsiniz.
       - **Içeri aktar**: Azure aboneliğinizde zaten mevcut olan bir Web uygulamasını kullanmak Için **içeri aktar**' a tıklayın. Uygulama ve kiracı için kolay bir ad sağlayın ve ardından Configuration Manager kullanmak istediğiniz Azure Web uygulaması için kiracı KIMLIĞINI, Istemci KIMLIĞINI ve gizli anahtarı belirtin. Bilgileri doğruladıktan sonra, devam etmek için **Tamam** ' ı tıklatın. Bu seçenek şu anda bu Technical Preview sürümünde kullanılamaz.
   - İstemci uygulaması için aynı işlemi tekrarlayın.

   Portalda doğru izinleri ayarlamak için uygulama Içeri aktarma kullandığınızda *Dizin verilerini oku* uygulama iznini vermeniz gerekir. Uygulama oluşturmayı kullanıyorsanız, izinler uygulamayla otomatik olarak oluşturulur, ancak yine de Azure portal uygulamaya onay vermeniz gerekir.
6. Sihirbazın **bulma** sayfasında isteğe bağlı olarak **Azure Active Directory Kullanıcı bulmayı etkinleştirin**ve ardından **Ayarlar**' a tıklayın.
   **Azure AD Kullanıcı keşfi ayarları** iletişim kutusunda bulma işleminin gerçekleştiği zaman için bir zamanlama yapılandırın. Ayrıca, Azure AD 'de yalnızca yeni veya değiştirilmiş hesapları denetleyen Delta Keşfi de etkinleştirebilirsiniz.
7. Sihirbazı tamamlayın.

Bu noktada, Configuration Manager sitenizi Azure AD 'ye bağladınız.


### <a name="install-the-cm-client-from-the-internet"></a>CM istemcisini Internet 'ten yükler

Başlamadan önce, istemci yükleme kaynak dosyalarının istemcisini yüklemek istediğiniz cihazda yerel olarak depolandığından emin olun.
Ardından, aşağıdaki yükleme komut satırını kullanarak [Istemcileri Windows bilgisayarlarına dağıtma](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) bölümündeki yönergeleri kullanın (örnekteki değerleri kendi değerlerinizle değiştirin):

**CCMSetup. exe/NoCrlCheck/Source: C:\CLIENT CCMHOSTNAME = SCCMPROXYCONTOSO. CLOUDAPP. NET/CCM_Proxy_ServerAuth/72457598037527932 Smssitekodu = HEC AADTENANTıD = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPıD =\<GUID> AADRESOURCEURI =<https://contososerver>**

- **/NoCRLCheck**: yönetim noktanız veya bulut yönetimi ağ geçidiniz ortak olmayan bir sunucu sertifikası kullanıyorsa, istemci CRL konumuna ulaşamayacak olabilir.
- **/Source**: yerel klasör: istemci yükleme dosyalarının konumu.
- **CCMHOSTNAME**: Internet yönetim noktasının adı. Bunu, yönetilen istemcideki bir komut isteminden **gwmi ad alanı root\ccm\locationservices-class SMS_ActiveMPCandidate** çalıştırarak bulabilirsiniz.
- **SMSMP**: arama yönetim noktanağınızın adı – bu, intranetinizde olabilir.
- **Smssitekodu**: Configuration Manager sitenizin site kodudur.
- **Aadtenantıd**, **aadtenantname**: Configuration Manager bağladığınız Azure AD kiracının kimliği ve adı. Bunu, Azure AD 'ye katılmış bir cihazdaki komut isteminden dsregcmd. exe/status komutunu çalıştırarak bulabilirsiniz.
- **Aadclientappıd**: Azure AD ISTEMCI uygulama kimliği. Bu konuda yardım almak için bkz. [kaynaklara erişebilen Azure Active Directory uygulaması ve hizmet sorumlusu oluşturmak için portalı kullanma](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
- **Aadresourceuri**: EKLENDI Azure AD Server uygulamasının tanımlayıcı URI 'si.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>OMS bağlantısını yapılandırmak için Azure Hizmetleri Sihirbazı 'Nı kullanma
1705 Technical Preview sürümünden başlayarak, Configuration Manager bağlantınızı Operations Management Suite (OMS) bulut hizmetine yapılandırmak için **Azure Hizmetleri Sihirbazı 'nı** kullanın. Sihirbaz, bu bağlantıyı yapılandırmak için önceki iş akışlarının yerini alır.

-   Bu sihirbaz, OMS, Iş için Windows Mağazası (WSfB) ve Azure Active Directory (Azure AD) gibi Configuration Manager için bulut hizmetlerini yapılandırmak üzere kullanılır.  

-   Configuration Manager, Log Analytics veya Yükseltme Hazırlığı gibi özellikler için OMS 'ye bağlanır.

### <a name="prerequisites-for-the-oms-connector"></a>OMS Bağlayıcısı için Önkoşullar
OMS bağlantısını yapılandırma önkoşulları [, güncel dalı sürüm 1702 ' de belgelenenlerden](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)değiştirilmez. Bu bilgiler burada yinelenir:  

-   OMS 'ye Configuration Manager izni sağlanıyor.

-   OMS bağlayıcısının [çevrimiçi modda](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)olan bir [hizmet bağlantı noktasını](../servers/deploy/configure/about-the-service-connection-point.md) barındıran bilgisayara yüklenmesi gerekir.

-   OMS bağlayıcısıyla birlikte hizmet bağlantı noktasına yüklenmiş OMS için bir Microsoft Monitoring Agent yüklemelisiniz. Aracı ve OMS bağlayıcısının aynı **OMS çalışma alanını**kullanacak şekilde yapılandırılması gerekir. Aracıyı yüklemek için bkz. OMS belgelerindeki [aracıyı indirme ve yükleme](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) .
-   Bağlayıcıyı ve aracıyı yükledikten sonra, OMS 'yi Configuration Manager verileri kullanacak şekilde yapılandırmanız gerekir. Bunu yapmak için, OMS portalında [Configuration Manager koleksiyonlarını Içeri aktarabilirsiniz](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>OMS bağlantısını yapılandırmak için Azure Hizmetleri Sihirbazı 'Nı kullanın

1.  Konsolunda, **Yönetim** > **genel bakış** > **Cloud Services** > **Azure hizmetleri**' ne gidin ve ardından Şeritteki **giriş** sekmesinden **Azure hizmetlerini yapılandır** ' ı seçerek **Azure Hizmetleri Sihirbazı 'nı**başlatın.

2.  **Azure hizmetleri** sayfasında, Operation Management Suite Bulut hizmetini seçin. **Azure hizmet adı** ve isteğe bağlı bir açıklama için kolay bir ad girin ve ardından **İleri**' ye tıklayın.

3.  **Uygulama** sayfasında, Azure ortamınızı belirtin (Technical Preview yalnızca genel bulutu destekler). Ardından, **Araştır** ' a tıklayarak sunucu uygulaması penceresini açın.

4.  Bir Web uygulaması seçin:

    -   **Içeri aktar**: Azure aboneliğinizde zaten mevcut olan bir Web uygulamasını kullanmak Için **içeri aktar**' a tıklayın. Uygulama ve kiracı için kolay bir ad sağlayın ve ardından Configuration Manager kullanmak istediğiniz Azure Web uygulaması için kiracı KIMLIĞINI, Istemci KIMLIĞINI ve gizli anahtarı belirtin. Bilgileri **doğruladıktan** sonra, devam etmek için **Tamam** ' ı tıklatın.   

    > [!NOTE]   
    > OMS 'yi bu önizleme ile yapılandırdığınızda, OMS yalnızca bir Web uygulamasının *içeri aktarma* işlevini destekler. Yeni bir Web uygulaması oluşturmak desteklenmez. Benzer şekilde, OMS için mevcut bir uygulamayı yeniden kullanamazsınız.

5.  Diğer tüm yordamları başarıyla gerçekleştirdiniz, **OMS bağlantı yapılandırma** ekranındaki bilgiler bu sayfada otomatik olarak görüntülenir. **Azure aboneliğiniz**, **Azure Kaynak grubunuz**ve **Operations Management Suite çalışma alanınız**için bağlantı ayarları bilgisi görüntülenmelidir.

6.  Sihirbaz, giriş yaptığınız bilgileri kullanarak OMS hizmetine bağlanır. OMS ile eşitlemek istediğiniz cihaz koleksiyonlarını seçin ve ardından **Ekle**' ye tıklayın.

7.  **Özet** ekranında bağlantı ayarlarınızı doğrulayın ve sonra **İleri**' yi seçin. **İlerleme** ekranı, bağlantı durumunu gösterir ve ardından **tamamlanmalıdır**.

8.  Sihirbaz tamamlandıktan sonra, Configuration Manager konsolu, **Operation Management Suite** 'ı bir **bulut hizmeti türü**olarak yapılandırdığınıza göre gösterir.
