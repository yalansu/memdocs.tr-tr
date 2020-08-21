---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1710 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e408bbe7ea88d70c5a9d02368c2d820584cae2b8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694449"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Configuration Manager için Technical Preview 1710 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1710 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bu teknik önizlemede bilinen sorunlar:**
- **Windows 10, sürüm 1709 (Fall Creators Update olarak da bilinir) desteği**.  Bu Windows sürümünden itibaren, Windows Media birden çok sürüm içerir. Bir görev dizisini bir işletim sistemi yükseltme paketi veya işletim sistemi görüntüsü kullanacak şekilde yapılandırırken, [Configuration Manager tarafından kullanılmak üzere desteklenen bir sürüm](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)seçtiğinizden emin olun.
- **Pasif modda bir site sunucunuz varsa yeni bir önizleme sürümüne güncelleştirme başarısız olur**. [Pasif modda birincil site sunucusuna](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)sahip bir önizleme sürümü çalıştırdığınızda, önizleme sitenizi bu yeni önizleme sürümüne başarıyla güncelleştirebilmeniz için Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz güncelleştirmeyi tamamladıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
  2. **Site sistemi rolleri** bölmesinde, **site sunucusu** rolüne sağ tıklayın ve ardından **rolü kaldır**' ı seçin.
  3. Pasif mod site sunucusuna sağ tıklayın ve ardından **Sil**' i seçin.
  4. Site sunucusu kaldırıldıktan sonra, etkin birincil site sunucusunda hizmeti **CONFIGURATION_MANAGER_UPDATE**yeniden başlatın.

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Configuration Manager PowerShell betikleri dağıtmaya yönelik iyileştirmeler
Bu sürümle birlikte, dağıttığınız PowerShell betikleri artık aşağıdaki geliştirmelerin kullanımını desteklemektedir: 
- **Güvenlik kapsamları**.  Betikler artık komut dosyalarını yazma ve yürütmeyi denetlemek için güvenlik kapsamlarını kullanır. Bu, Kullanıcı gruplarını temsil eden Etiketler atanarak yapılır. Güvenlik kapsamlarını kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Gerçek zamanlı izleme**. Bir komut dosyasının çalıştırılmasını izlerken, betik çalıştığı için artık gerçek zamanlı olur.
- **Parametre doğrulaması**. Betiğinizdeki her parametrenin, bu parametre için doğrulama eklemeniz için bir **betik parametresi özellikleri** iletişim kutusu vardır. Doğrulama eklendikten sonra, doğrulamasını karşılamayan bir parametre için değer giriyorsanız hata almalısınız.

PowerShell betikleri dağıtımı ilk olarak Technical Preview [Teknik önizleme 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)' de kullanıma sunulmuştur. [Teknik önizleme 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) ve [Teknik Önizleme 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)ile ek iyileştirmeler yapılmıştır.


### <a name="try-it-out"></a>Deneyin!

Betikleri Çalıştır özelliğini kullanmayı denemek için bkz. [betikleri oluşturma ve çalıştırma](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Windows 10 geliştirilmiş verilerini yalnızca Windows Analytics ile ilgili verileri gönderecek şekilde sınırlayın Cihaz Durumu
<!-- 1356148 -->

Bu sürümle birlikte, artık Windows 10 tanılama veri toplama düzeyini **Gelişmiş (sınırlı)** olarak ayarlayabilirsiniz. Bu ayar, ortamınızdaki cihazlar hakkında, Windows 10 sürüm 1709 veya sonraki bir sürümü ile **Gelişmiş** düzeydeki tüm verileri raporlayan cihazlar hakkında eyleme dönüştürülebilir Öngörüler elde etmenizi sağlar.

Gelişmiş (sınırlı) düzey, temel düzeydeki ölçümleri ve Windows Analytics ile ilgili **Gelişmiş** düzeyden toplanan verilerin bir alt kümesini içerir.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Yazılım Merkezi artık 250x250 ' dan büyük simgeleri bozar  
<!-- 1356194 -->

Bu sürümle birlikte, Yazılım Merkezi artık 250x250 ' dan büyük simgeleri bozmayacaktır. Yazılım Merkezi bu tür simgeler bulanık bir şekilde görünür. Artık 512x512 ' ye kadar piksel boyutlarına sahip bir simge ayarlayabilirsiniz ve bozulma olmadan görüntülenir.

### <a name="try-it-out"></a>Deneyin!
Yazılım Merkezi 'nde uygulamanız için bir simge ekleyin. Denemek için bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Ortak yönetilen cihazlar için yazılım merkezi 'nden uyumluluğu denetle
<!-- 1356374 -->
Bu sürümde, kullanıcılar, koşullu erişim Intune tarafından yönetilse bile, ortak yönetilen Windows 10 cihazlarının uyumluluğunu denetlemek için yazılım merkezi 'ni kullanabilir. Ayrıntılar için bkz. [Windows 10 cihazlar Için ortak yönetim](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Exploit Guard desteği
Bu sürüm, Windows Defender Exploit Guard için destek ekler. Tüm dört Exploit Guard bileşenini yöneten ilkeleri yapılandırabilir ve dağıtabilirsiniz. Bu bileşenler şunlardır:
-   Saldırı Yüzeyini Azaltma
-   Denetlenen klasör erişimi
-   Exploit protection
-   Ağ koruması

Exploit Guard ilke dağıtımına yönelik uyumluluk verileri Configuration Manager konsolundan kullanılabilir.

Exploit Guard ve belirli bileşenler ve kurallar hakkında daha fazla bilgi için Windows belge kitaplığı 'nda [Windows Defender Exploit Guard](/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) bölümüne bakın.

### <a name="prerequisites"></a>Ön koşullar
Yönetilen cihazların Windows 10 1709 Fall Creators Update veya sonrasını çalıştırması ve yapılandırılan bileşenlere ve kurallara bağlı olarak aşağıdaki gereksinimleri karşılamalıdır:

|Exploit Guard bileşeni |Ek önkoşullar|
|------------------------|------------------------|
| Saldırı Yüzeyini Azaltma  | Cihazlarda [Windows Defender av gerçek zamanlı korumanın]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) etkinleştirilmiş olması gerekir.  |
| Denetlenen klasör erişimi  | Cihazlarda [Windows Defender av gerçek zamanlı korumanın]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) etkinleştirilmiş olması gerekir.   |
| Exploit protection  | Hiçbiri  |
| Ağ koruması  |  Cihazlarda [Windows Defender av gerçek zamanlı korumanın]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) etkinleştirilmiş olması gerekir.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Exploit Guard ilkesi oluşturma  <!--1355468 -->
1. Configuration Manager konsolunda **varlıklar ve uyumluluk**  >  **Endpoint Protection**' ne gidin ve ardından **Windows Defender Exploit Guard**' ı tıklatın.
2. **Giriş** sekmesinde, **Oluştur** grubunda, **Exploit İlkesi Oluştur**' a tıklayın.
3. **Yapılandırma Öğesi Oluştur Sihirbazı** ’nın **Genel**sayfasında, yapılandırma öğesi için bir ad ve isteğe bağlı bir açıklama belirtin.
4. Ardından, bu ilkeyle yönetmek istediğiniz Exploit Guard bileşenlerini seçin. Seçtiğiniz her bir bileşen için, daha sonra ek ayrıntılar yapılandırabilirsiniz.
   - **Saldırı yüzeyi azaltma:** Engellemek veya denetlemek istediğiniz Office tehdidi, komut dosyası tehditleri ve e-posta tehditlerini yapılandırın. Ayrıca, belirli dosyaları veya klasörleri bu kuraldan dışlayabilirsiniz.
   - **Denetlenen klasör erişimi:** Engellemeyi veya denetimini yapılandırın ve ardından bu ilkeyi atlayabileceği uygulamalar ekleyin.  Ayrıca, varsayılan olarak korunmayan ek klasörler de belirtebilirsiniz.
   - **Exploit koruması:**  Sistem işlemlerine ve uygulamalarına yönelik güvenlik açıklarını azaltmaya yönelik ayarları içeren bir XML dosyası belirtin. Bu ayarları Windows 10 cihazındaki Windows Defender Güvenlik Merkezi uygulamasından dışarı aktarabilirsiniz.
   - **Ağ koruması:** Şüpheli etki alanlarına erişimi engellemek veya denetlemek için ağ koruması ayarlayın.
5. Daha sonra cihazlara dağıtabileceğiniz ilkeyi oluşturmak için Sihirbazı doldurun.

### <a name="deploy-an-exploit-guard-policy"></a>Exploit Guard İlkesi dağıtma     
Exploit Guard ilkeleri oluşturduktan sonra, bunları dağıtmak için Exploit Guard Koruma Ilkesini Dağıtma Sihirbazı 'nı kullanın. Bunu yapmak için Configuration Manager konsolunu **varlıklar ve uyum**  >  **Endpoint Protection**açın ve ardından **Exploit Guard ilkesini dağıt**' a tıklayın.

## <a name="limited-support-for-cng-certificates"></a>CNG sertifikaları için sınırlı destek
<!-- 1356191 -->
Bu sürümden itibaren, artık aşağıdaki senaryolar için [şifreleme API 'si: yeni nesil (CNG)](/windows/win32/seccng/cng-features) sertifika şablonları kullanabilirsiniz:

- Bir HTTPS yönetim noktasıyla istemci kaydı ve iletişim.   
- Bir HTTPS dağıtım noktasıyla yazılım dağıtımı ve uygulama dağıtımı.   
- İşletim sistemi dağıtımı.  
- İstemci mesajlaşma SDK 'Sı (en son güncelleştirme ile) ve ISV proxy.   
- Bulut Yönetimi Ağ Geçidi yapılandırma.  

CNG sertifikalarını kullanmak için, sertifika yetkilinizin (CA) hedef makineler için CNG sertifika şablonları sağlaması gerekir.  Şablon Ayrıntıları senaryoya göre farklılık gösterir; Ancak, aşağıdaki özellikler gereklidir:

- **Uyumluluk** sekmesi

    - **Sertifika yetkilisi** Windows Server 2008 veya sonraki bir sürümü olmalıdır. (Windows Server 2012 önerilir.)

    - **Sertifika alıcısı** Windows Vista/sunucu 2008 veya sonraki bir sürümü olmalıdır. (Windows 8/Windows Server 2012 önerilir.)

- **Şifreleme** sekmesi

    - **Sağlayıcı kategorisi** , **anahtar depolama sağlayıcısı**olmalıdır.  Istenir

En iyi sonuçlar için, Active Directory bilgilerden konu adının oluşturulmasını öneririz.  **Konu adı biçimi** Için DNS adını kullanın ve diğer konu adına DNS adını ekleyin.  Aksi takdirde, cihaz sertifika profiline kaydedildiğinde bu bilgileri sağlamanız gerekir.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Bekleyen bilgisayar yeniden başlatmaları için geliştirilmiş açıklamalar   <!--1356283 -->
[Technical preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)' de, Configuration Manager konsolunun içinden yeniden başlatma bekleyen cihazları tanımlamak için özelliği ekledik.

Bu Technical Preview sürümünden itibaren konsol, yeniden başlatmayı isteyen işlem veya eylem hakkında bilgi sağlayan ek ayrıntılar görüntüler.

## <a name="device-guard-policy-changes----1355092---"></a>Device Guard ilke değişiklikleri <!-- 1355092 -->
1710 Technical Preview derlemesi sayesinde, Device Guard ilkeleriyle ilgili olarak aşağıdaki üç değişiklik yapılmıştır:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Windows Defender uygulama denetim ilkelerine yeniden adlandırılan cihaz koruyucu ilkeleri
Device Guard ilkeleri Windows Defender uygulama denetimi ilkeleriyle yeniden adlandırıldı. Bu nedenle, örneğin, **Device Guard Ilke oluşturma Sihirbazı** artık **Windows Defender uygulama denetim ilkesi oluşturma Sihirbazı**olarak adlandırılmaktadır.

### <a name="restart-is-not-required-to-apply-policies"></a>İlkeleri uygulamak için yeniden başlatma gerekli değildir
Windows sürüm 1709 için Fall Creators Update ile başlayarak, Windows 'un yeni sürümünü kullanan cihazların Windows Defender uygulama denetim ilkelerini uygulamak için yeniden başlatılması gerekmez.

Varsayılan değer yeniden başlatılıyor.

#### <a name="try-it-out"></a>Deneyin!  

Yeniden başlatmaları devre dışı bırakmak istiyorsanız aşağıdaki adımları izleyin:

1.  **Windows Defender uygulama denetim Ilkesi oluşturma** Sihirbazı 'nı açın.
2.  **Genel** sayfasında, **Bu ilkenin tüm işlemlerde zorlanabilmesi için cihazların yeniden başlatılmasını zorla**onay kutusunun işaretini kaldırın.
3.  Sihirbaz tamamlanana kadar **İleri** ' ye tıklayın.

Windows 'un eski sürümlerinde otomatik yeniden başlatma yine de zorlanır.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Intelligent Security Graph tarafından güvenilen yazılımı otomatik olarak çalıştır

Yöneticiler artık, kilitlenmiş cihazların Microsoft Intelligent Security Graph (ıSG) tarafından belirlenen iyi bir saygınlığa sahip güvenilir yazılımları çalıştırmasına izin verme seçeneğine sahiptir. ISG, Windows Defender SmartScreen ve diğer Microsoft hizmetlerinden oluşur.

Yazılımın güvenilir olması için cihazların Windows Defender SmartScreen çalıştırması gerekir.

#### <a name="try-it-out"></a>Deneyin!  

Windows Defender SmartScreen çalıştıran bir cihazın güvenilir yazılım çalıştırmasına izin vermek için aşağıdaki adımları izleyin:

1.  **Windows Defender uygulama denetim Ilkesi oluşturma Sihirbazı 'nı**açın.
2.  **İçermeler** sayfasında, **Intelligent Security Graph tarafından güvenilen Yetkilendir yazılımının**kutusunu işaretleyin.
3.  **Güvenilen dosyalar veya klasör** kutusunda, güvenilir olmasını istediğiniz dosya ve klasörleri ekleyin.
4.  Sihirbaz tamamlanana kadar **İleri** ' ye tıklayın.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Windows Defender Application Guard ilkelerini yapılandırma ve dağıtma <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) , güvenilir olmayan Web sitelerini işletim sisteminin diğer bölümleri tarafından erişilemeyen güvenli bir yalıtılmış kapsayıcıda açarak kullanıcılarınızı korumaya yardımcı olan yeni bir Windows özelliğidir. Bu Technical Preview sürümünde, yapılandırdığınız Configuration Manager uyumluluk ayarlarını kullanarak bu özelliği yapılandırmak ve ardından bir koleksiyona dağıtmak için destek ekledik. Bu özellik, Windows 10 Creator güncelleştirmesinin 64 bit sürümü için önizleme aşamasında kullanıma sunulacaktır. Bu özelliği şimdi test etmek için bu güncelleştirmenin bir önizleme sürümünü kullanıyor olmanız gerekir.

### <a name="before-you-start"></a>Başlamadan önce
Windows Defender Application Guard ilkeleri oluşturup dağıtmak için, ilkeyi dağıttığınız Windows 10 cihazlarının bir ağ yalıtımı ilkesiyle yapılandırılması gerekir. Daha fazla bilgi için, daha sonra başvurulan blog gönderisine bakın. Bu özellik yalnızca geçerli Windows 10 Insider Derlemeleriyle birlikte kullanılabilir. Bunu test etmek için istemcileriniz son Windows 10 Insider derlemesini çalıştırıyor olmalıdır.

### <a name="try-it-out"></a>Deneyin!

Windows Defender Application Guard hakkındaki temel bilgileri anlamak için [blog gönderisini](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)okuyun.

Bir ilke oluşturmak ve kullanılabilir ayarlara gitmek için:
1. **Configuration Manager** konsolunda, **varlıklar ve uyumluluk**' i seçin.
2. **Varlıklar ve uyum** çalışma alanında, **Overview**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**Endpoint Protection genel bakış ' ı seçin.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **Windows Defender Application Guard İlkesi Oluştur**' a tıklayın.
4. Blog gönderisini başvuru olarak kullanarak, özelliği denemek için kullanılabilir ayarları gözden geçirin ve yapılandırabilirsiniz.
5. Bu sürümde, sihirbaza yeni ağ tanımı sayfasını ekledik. Burada, kurumsal kimlik ' i belirtin ve kurumsal ağ sınırınızı tanımlayın.

    > [!NOTE]
    > Windows 10 bilgisayarları, istemcide yalnızca bir ağ yalıtımı listesini depolar. Bu sürümde, iki farklı türde ağ yalıtımı listesi (biri Windows Information Protection, diğeri Windows Defender Application Guard 'dan) oluşturabilir ve bunları istemciye dağıtabilirsiniz. Her iki ilkeyi de dağıtırsanız, bu ağ yalıtımı listelerinin eşleşmesi gerekir. Aynı istemciyle eşleşmeyen listeler dağıtırsanız, dağıtım başarısız olur.

    Ağ tanımlarının nasıl belirtilme hakkında daha fazla bilgiyi [Windows Information Protection belgeleri]- [windows Information Protection (WIP) kullanarak kurumsal verilerinizi koruma](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)hakkında daha fazla bilgi edinebilirsiniz.

6. İşiniz bittiğinde Sihirbazı doldurun ve ilkeyi bir veya daha fazla Windows 10 cihazına dağıtın.

### <a name="further-reading"></a>Daha fazla bilgi

Windows Defender Application Guard hakkında daha fazla bilgi edinmek için [Bu blog gönderisine](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)bakın. Ayrıca, Windows Defender Application Guard tek başına modu hakkında daha fazla bilgi edinmek için [Bu blog gönderisine](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)bakın.

## <a name="next-steps"></a>Sonraki Adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).