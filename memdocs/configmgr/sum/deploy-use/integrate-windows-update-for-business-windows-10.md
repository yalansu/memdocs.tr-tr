---
title: Windows Update Iş için tümleştirin
titleSuffix: Configuration Manager
description: Windows Update hizmetine bağlı cihazlar için Windows 10 ' un güncel kalmasını sağlamak için Windows Update for Business (WUfB) kullanın.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 62f5059ef02d7b2594a506135abf332a8b6c0def
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083905"
---
# <a name="integrate-with-windows-update-for-business"></a>Iş için Windows Update tümleştirin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows Update for Business (WUfB), bu cihazlar doğrudan Windows Update (WU) hizmetine bağlandıklarında en son güvenlik savunmaları ve Windows özellikleriyle Kuruluşunuzda Windows 10 tabanlı cihazların her zaman güncel kalmasını sağlar. Configuration Manager, yazılım güncelleştirmelerini almak için WUfB ve WSUS kullanan Windows 10 bilgisayarları birbirinden ayırt edebilir.  

> [!WARNING]
> Cihazlarınız için ortak yönetim kullanıyorsanız ve [Windows Update Ilkelerini](../../comanage/workloads.md#windows-update-policies) Intune 'a taşıdıysanız, cihazlarınız [Intune 'dan Windows Update iş ilkelerini](/intune/windows-update-for-business-configure)alır.
> - Configuration Manager istemcisi birlikte yönetilen cihazda hala yüklüyse, toplu güncelleştirmeler ve özellik güncelleştirmelerinin ayarları Intune tarafından yönetilir. Ancak, [**Istemci ayarlarında**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)etkinleştirildiyse, üçüncü taraf düzeltme eki uygulama Configuration Manager tarafından yönetilmeye devam eder.  

 Configuration Manager istemcileri, WUfB veya Windows Insiders içeren WU 'dan güncelleştirmeleri alacak şekilde yapılandırıldığında bazı Configuration Manager özellikleri artık kullanılamaz:  

- Windows Update uyumluluk raporu:  
  - Configuration Manager, WU 'ye yayımlanan güncelleştirmelerin farkında olmaz. WU güncelleştirmelerini almak üzere yapılandırılan Configuration Manager istemcileri, Configuration Manager konsolunda bu güncelleştirmeler için **bilinmiyor** olarak görüntülenir.  

  - **Bilinmeyen** durum yalnızca tarama durumunu WSUS 'ten geri bildirmemiş istemciler için olduğundan genel uyumluluk durumunun giderilmesi zordur. Şimdi de WU 'den güncelleştirme alan Configuration Manager istemcileri de içerir.  

  - Tanım güncelleştirmeleri uyumluluğu, genel güncelleştirme uyumluluğu raporlamasının bir parçasıdır ve beklenen şekilde çalışmaz.

- Güncelleştirme uyumluluk durumuna dayalı Defender için genel Endpoint Protection raporlaması, eksik tarama verileri nedeniyle doğru sonuçlar döndürmez.  

- Configuration Manager, güncelleştirmeleri almak için WUfB 'ye bağlı istemcilere Microsoft 365 uygulamalar, IE ve Visual Studio gibi Microsoft güncelleştirmelerini dağıtabmayacak.  

- Configuration Manager, WSUS 'e yayınlanan ve Configuration Manager üzerinden yönetilen 3. taraf güncelleştirmelerini, güncelleştirmeleri almak için WUfB 'ye bağlı istemcilere dağıtabilir. WUfB 'e bağlanan istemcilerde üçüncü taraf güncelleştirmelerinin yüklenmesini istemiyorsanız, [istemcilerde yazılım güncelleştirmelerini etkinleştir](../../core/clients/deploy/about-client-settings.md#software-updates)adlı istemci ayarını devre dışı bırakın.

- Yazılım güncelleştirmeleri altyapısını kullanan Configuration Manager tam istemci dağıtımı, güncelleştirmeleri almak için WUfB 'ye bağlanan istemciler için çalışmaz.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Windows 10 güncelleştirmeleri için WUfB kullanan istemcileri tanımla

Windows 10 güncelleştirmelerini ve yükseltmelerini almak için WUfB kullanan istemcileri tanımlamak için aşağıdaki yordamı kullanın. Ardından bu istemcileri güncelleştirmeleri almak üzere WSUS kullanmayı durduracak şekilde yapılandırın ve bu istemciler için yazılım güncelleştirmeleri iş akışını devre dışı bırakmak üzere bir istemci Aracısı ayarı dağıtın.  

### <a name="prerequisites-for-wufb"></a>WUfB önkoşulları

- Windows 10 Desktop Pro veya Windows 10 Enterprise Edition sürüm 1511 veya sonraki sürümleri çalıştıran istemciler

- [İş için Windows Update](/windows/deployment/update/waas-manage-updates-wufb) dağıtılır ve istemciler Windows 10 güncelleştirmelerini ve yükseltmelerini almak için WUfB kullanır.  

### <a name="to-identify-clients-that-use-wufb"></a>WUfB kullanan istemcileri tanımlamak için  

1. Daha önce etkinleştirildiyse Windows Update aracısının WSUS 'ye karşı tarandığından emin olun. Aşağıdaki kayıt defteri anahtarı bilgisayarın WSUS veya Windows Update karşı tarama yapıp yapamadığını belirtmek için kullanılabilir. Kayıt defteri anahtarı yoksa, WSUS 'ye karşı tarama yapmaz.
    - **HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Configuration Manager Kaynak Gezgini **Windows Update** düğümü altında **UseWUServer**adlı yeni bir öznitelik vardır.
1. Güncelleştirmeler ve yükseltmeler için WUfB üzerinden bağlı tüm bilgisayarlarda **UseWUServer** özniteliğini temel alan bir koleksiyon oluşturun. Aşağıdakine benzer bir sorgu temel alınarak bir koleksiyon oluşturabilirsiniz:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Yazılım güncelleştirme iş akışını devre dışı bırakmak için bir istemci Aracısı ayarı oluşturun. Ayarı doğrudan WUfB 'ye bağlı olan bilgisayar koleksiyonuna dağıtın.
1. WUfB üzerinden yönetilen bilgisayarların uyumluluk durumunda **bilinmiyor** görüntülenir ve genel uyumluluk yüzdesinin bir parçası olarak sayılmaz.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Iş erteleme ilkeleri için Windows Update yapılandırma
<!-- 1290890 -->
Configuration Manager sürüm 1706 ' den başlayarak, Windows 10 için Windows 10 özellik güncelleştirmeleri veya kalite güncelleştirmeleri için erteleme ilkelerini, doğrudan Iş Windows Update tarafından yönetilen Windows 10 cihazları için yapılandırabilirsiniz. **Yazılım kitaplığı**Windows 10 bakımı altındaki **iş için yeni Windows Update ilke** düğümünde erteleme ilkelerini yönetebilirsiniz  >  **Windows 10 Servicing**.

> [!NOTE]
> Configuration Manager sürüm 1802 ' den başlayarak, Windows Insider için erteleme ilkelerini ayarlayabilirsiniz. <!--507201-->  
Windows Insider programı hakkında daha fazla bilgi için bkz. [iş Için Windows Insider programı ile çalışmaya](/windows/deployment/update/waas-windows-insider-for-business)başlama.

### <a name="prerequisites-for-deferral-policies"></a>Erteleme ilkeleri için Önkoşullar

- Windows 10 sürüm 1703 veya üzeri
- Iş için Windows Update tarafından yönetilen Windows 10 cihazlarının Internet bağlantısı olmalıdır

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Iş erteleme ilkesi için Windows Update oluşturmak için

1. **Yazılım kitaplığı**'nda  >  iş ilkeleri için**Windows 10 Bakımı**  >  **Windows Update**
1. Iş için Windows Update oluşturma Sihirbazı 'Nı açmak için **Oluştur** grubunun **giriş** sekmesinde **iş ilkesi Windows Update oluştur** ' u seçin.
1. **Genel** sayfasında, ilke için bir ad ve açıklama girin.
1. Erteleme Ilkeleri sayfasında, özellik güncelleştirmelerini **ertelemeyi** veya duraklatmayı yapılandırın. Özellik Güncelleştirmeleri genellikle Windows’un yeni özellikleridir. **Dal hazırlık düzeyi** ayarını yapılandırdıktan sonra, özellik güncelleştirmelerini Microsoft 'un kullanılabilirliğine göre ertelemek için ne kadar süre ertelemenizi istediğinizi tanımlayabilirsiniz.
    - **Dal hazırlık düzeyi**: cihazın Windows güncelleştirmelerini alacağı dalı ayarlayın. Yarı yıllık kanal (hedefli), yarı yıllık kanal veya Windows Insider derlemesi seçin.

        > [!NOTE]
        > **Yarı yıllık kanal** için Windows 10, *Sürüm 1903 veya sonraki bir sürüme*ilke dağıtın. **Yarı yıllık kanal (hedefli)** için Windows 10, *Sürüm 1809 veya önceki bir sürümü*için ilkeler dağıtın.
        >
        > Windows 10, sürüm 1903 veya üzeri bir **yarı yıllık kanal (hedefli)** ilkesi için bir ilke dağıtırsanız, dağıtım **0x8004100C**hatası ile başarısız olur.<!-- 5593139 -->

    - **Erteleme süresi (gün)**: Özellik güncelleştirmelerinin ertelenmesi gereken gün sayısını belirtin. Bu özellik güncelleştirmelerini almayı, yayınlarından 365 güne kadar erteleyebilirsiniz.
    - **Özellik güncelleştirmelerini duraklatma başlatılıyor**: cihazların güncelleştirmeleri duraklatmadan 35 güne kadar olan özellik güncelleştirmelerini almasını isteyip istemediğinizi seçin. En fazla gün sayısı kadar bir süre geçtikten sonra duraklatma işlevi otomatik olarak sona erer ve cihaz, kullanılabilecek güncelleştirmeleri bulmak için Windows Güncelleştirmelerini tarar. Bu taramanın ardından güncelleştirmeleri yeniden duraklatabilirsiniz. Onay kutusunu temizleyerek Özellik güncelleştirmelerinin duraklamasını geri alabilirsiniz.
1. Kalite güncelleştirmelerini ertelemenizi veya duraklatmayı seçin. Kalite Güncelleştirmeleri, genellikle mevcut Windows işlevselliğine yönelik düzeltme ve iyileştirmelerdir. Normal olarak her ayın ilk salı günü yayımlanırlar ancak Microsoft tarafından herhangi bir zamanda yayımlanmaları mümkündür. Kullanıma sunulduktan sonra Kalite Güncelleştirmelerinin alınmasını ertelemek isteyip istemediğinizi ve ne kadar süreyle erteleyeceğinizi tanımlayabilirsiniz.
    - **Erteleme süresi (gün)**: kalite güncelleştirmelerinin ertelenmesi gereken gün sayısını belirtin. Bu kalite güncelleştirmelerini almayı, sürümünden 30 güne kadar erteleyebilirsiniz.
    - **Kalite güncelleştirmelerini duraklatma başlangıcı**: cihazların, güncelleştirmeleri duraklatmadan 35 güne kadar kalite güncelleştirmeleri almasını isteyip istemediğinizi seçin. En fazla gün sayısı kadar bir süre geçtikten sonra duraklatma işlevi otomatik olarak sona erer ve cihaz, kullanılabilecek güncelleştirmeleri bulmak için Windows Güncelleştirmelerini tarar. Bu taramanın ardından güncelleştirmeleri yeniden duraklatabilirsiniz. Onay kutusunu temizleyerek kalite güncelleştirmelerinin duraklamasını geri alabilirsiniz.
1. Microsoft Update için geçerli olan ve Windows güncelleştirmelerinin yanı sıra **diğer Microsoft ürünlerinden güncelleştirme yüklemeyi** seçin.
1. Sürücüleri Windows güncelleştirmelerinden otomatik olarak güncelleştirmek için **Windows Update sürücüleri dahil et** ' i seçin. Bu ayarı temizlerseniz, sürücü güncelleştirmeleri Windows güncelleştirmelerinden indirilmez.
1. Yeni erteleme ilkesini oluşturmak için Sihirbazı doldurun.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Windows Update Iş erteleme ilkesini dağıtmak için

1. **Yazılım kitaplığı**'nda  >  iş ilkeleri için**Windows 10 Bakımı**  >  **Windows Update**
1. **Giriş** sekmesinde, **dağıtım** grubunda, **Windows Update iş ilkesi için dağıt**' ı seçin.
1. Aşağıdaki ayarları yapılandırın:
    - **Dağıtılacak yapılandırma ilkesi**: dağıtmak istediğiniz iş ilkesi Windows Update seçin.
    - **Koleksiyon**: ilkeyi dağıtmak istediğiniz koleksiyonu seçmek Için, **Araştır** ' a tıklayın.
    - **Bakım süresi dışında düzeltmeye Izin ver**: ilkeyi dağıtmakta olduğunuz koleksiyon için bir bakım penceresi yapılandırıldıysa, ilke ayarlarının bakım penceresi dışındaki değeri düzeltmesine izin vermek için bu seçeneği etkinleştirin. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).
    - **Zamanlama**: dağıtılan ilkenin istemci bilgisayarlarda değerlendirildiği uyumluluk değerlendirmesi zamanlamasını belirtin. Bu zamanlama basit veya özel bir zamanlama olabilir.
1. İlkeyi dağıtmak için Sihirbazı doldurun.