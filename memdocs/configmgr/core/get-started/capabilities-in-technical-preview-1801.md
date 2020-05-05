---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1801 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074223"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Configuration Manager için Technical Preview 1801 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1801 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. 

Technical Preview 'un bu sürümünü yüklemeden önce [Configuration Manager Için Teknik önizlemeyi](technical-preview.md) gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Bu teknik önizlemede bilinen sorunlar:**
- **Pasif modda bir site sunucunuz varsa yeni bir önizleme sürümüne güncelleştirme başarısız olur**. [Pasif modda bir birincil site sunucunuz](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)varsa, bu yeni önizleme sürümüne güncelleştirmeden önce Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz güncelleştirmeyi tamamladıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Configuration Manager konsolunda **Yönetim** > **genel bakış** > **Site yapılandırması** > **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
  2. **Site sistemi rolleri** bölmesinde, **site sunucusu** rolüne sağ tıklayın ve ardından **rolü kaldır**' ı seçin.
  3. Pasif mod site sunucusuna sağ tıklayın ve ardından **Sil**' i seçin.
  4. Site sunucusu kaldırıldıktan sonra, etkin birincil site sunucusunda hizmeti **CONFIGURATION_MANAGER_UPDATE**yeniden başlatın.
  <!--sms 489412-->


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Aşamalı dağıtımlar oluşturma
<!-- 1357405 -->
Aşamalı dağıtımlar, birden çok dağıtım oluşturmadan, düzenli ve sıralı bir yazılım dağıtımını otomatik hale getirir. Bu Technical Preview sürümünde, yönetim konsolundaki görev dizileri için aşamalı dağıtım Sihirbazı tamamlanabilir. Ancak, dağıtımlar oluşturulmaz. 

### <a name="try-it-out"></a>Deneyin!  
  Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.
 
**Görev dizisi için aşamalı dağıtım oluşturma** </br>
1. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.
2. Var olan bir görev dizisine sağ tıklayın ve **aşamalı dağıtım oluştur**' u seçin. 
3. **Genel** sekmesinde, aşamalı dağıtıma bir ad, açıklama (isteğe bağlı) verin ve **otomatik olarak varsayılan pilot ve üretim aşamaları oluştur**' u seçin. 
4. **Pilot koleksiyon** ve **Üretim koleksiyonu** alanlarını doldurun. **İleri**’yi seçin.
5. **Ayarlar** sekmesinde, zamanlama ayarlarının her biri için bir seçenek belirleyin ve tamamlandığında **İleri ' yi** seçin. 
6. **Aşamalar** sekmesinde, gerekirse aşamaların birini düzenleyin ve ardından **İleri**' ye tıklayın.
7. **Özet** sekmesinde seçimlerinizi onaylayın ve devam etmek için **İleri** ' ye tıklayın.

## <a name="co-management-reporting"></a>Ortak yönetim raporlaması
<!-- 1356648 -->
[Ortak yönetim](../../comanage/overview.md) yeteneklerini kullanıyorsanız, artık ortamınızda ortak yönetim hakkında bilgi içeren bir pano görüntüleyebilirsiniz. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **yükseltme hazırlığı**' i genişletin ve **ortak yönetim** panosunu seçin. Pano aşağıdaki kutucukları içerir:
- **Ortak yönetilen cihazlar**: ortamınızda ortak yönetim için etkinleştirdiğiniz cihazların yüzdesi
- **Işletim sistemi dağıtımı**: işletim SISTEMLERININ (OS) sürüme göre dökümünü. Bu grafik aşağıdaki gruplandırmaları kullanır:
  - Windows 7 & 8. x
  - 1709 'den düşük Windows 10
  - Windows 10 1709 ve üzeri
    > [!NOTE] 
    > Windows 10, sürüm 1709 ve üzeri, ortak yönetim için bir önkoşuldur
- **Ortak yönetim durumu**: aşağıdaki kategorilerde cihaz başarısı veya başarısızlığı dökümü:
   - Başarılı, karma Azure AD 'ye katılmış
   - Başarılı, Azure AD 'ye katılmış
   - Hata: otomatik kayıt başarısız oldu
- **Iş yükü geçişi**: kullanılabilir üç iş yükü için Microsoft Intune geçiş yaptığınız cihazların sayısını gösteren bir çubuk grafik: 
   - Uyumluluk İlkeleri
   - Kaynak erişimi
   - İş İçin Windows Update

### <a name="prerequisites"></a>Önkoşullar
- Configuration Manager konsolunu çalıştıran bilgisayar Internet Explorer 9 veya üstünü gerektirir.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Otomatik dağıtım kuralı değerlendirme zamanlaması geliştirmeleri
<!-- 1357133 -->
[Kullanıcı sesinize geri bildirimde bulunarak](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), artık otomatik dağıtım KURALı (ADR) değerlendirmesini bir temel günden ötede olacak şekilde zamanlayabilirsiniz. Örneğin, ayın ikinci Salı gününe geçen iki günün bir boşluğu, kuralı Perşembe günü değerlendirir. 

### <a name="try-it-out"></a>Deneyin!  
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin. <br/>

**Temel bir günden oluşan ve ADR sapmasını değerlendiren özel bir zamanlama oluşturma** </br>
1.  **Yazılım kitaplığı** çalışma alanında **yazılım güncelleştirmeleri**' ni genişletin ve **Otomatik dağıtım kuralları**' nı seçin.
2. **Otomatik dağıtım kuralları** ' na sağ tıklayın ve **Otomatik dağıtım kuralı oluştur**' u seçin. 
3. **Genel**, **dağıtım ayarları**ve **yazılım güncelleştirmeleri** sekmelerini tamamlamaya yönelik yönergeleri izleyin. 
4. **Değerlendirme zamanlaması** sekmesinde, **kuralı bir zamanlamaya göre Çalıştır** ve **Özelleştir**' i seçin.
5. Özel zamanlama için **aylık** ' ı seçin ve ikinci Salı gibi bir temel güne koyun. 
6. Sapmayı **(gün)** ve gün sayısını denetleyin ve tamamlandığında **Tamam** ' a tıklayın.  
7. **Otomatik dağıtım kuralı oluşturma Sihirbazı**' nın kalanını tamamlayın. 



## <a name="reassign-distribution-point"></a>Dağıtım noktasını yeniden ata
<!-- 1306937 -->
Birçok müşterinin büyük Configuration Manager altyapıları vardır ve bunların ortamlarını basitleştirmek için birincil veya ikincil siteleri azaltmaktadır. Ayrıca, yönetilen istemcilere içerik sağlamak için şube konumlarında dağıtım noktalarını korumaları gerekir. Bu dağıtım noktaları genellikle birden çok terabayt veya daha fazla içerik içerir. Bu içerik, bu uzak sunuculara dağıtılacak zaman ve ağ bant genişliği açısından maliyetlidir. 

Bu özellik, içeriği yeniden dağıtmadan bir dağıtım noktasını başka bir birincil siteye yeniden atamanıza olanak tanır. Bu eylem, sunucudaki tüm içeriği kalıcı hale yaparken site sistem atamasını güncelleştirir. Birden çok dağıtım noktasını yeniden atamanız gerekiyorsa, önce bu eylemi tek bir dağıtım noktasında gerçekleştirin ve ardından aynı anda ek sunucularla devam edin.

> [!IMPORTANT]
> Site sistemi sunucusu yalnızca dağıtım noktası rolünü barındırabilirler. Site sistemi sunucusu durum geçiş noktası gibi başka bir Configuration Manager sunucu rolü barındırıyorsa, dağıtım noktasını yeniden atayamazsınız. Bir bulut dağıtım noktasını yeniden atayamazsınız. 

Tek bir birincil sitenin Technical Preview sınırı nedeniyle bu sürümde bu seçenek kullanılamaz. Senaryoyu değerlendirin ve bu eylemin özellikleri ile ilgili olarak şeridin **giriş** sekmesinden **geri bildirim** gönderin.
1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin.
2. Hedef dağıtım noktasına sağ tıklayın ve **dağıtım noktasını yeniden ata**' yı seçin. 
  ![Dağıtım noktasını yeniden ata](media/1306937-reassign-dp.png)
3. Bu dağıtım noktasını yeniden atamak istediğiniz site sunucusunu ve site kodunu seçin. 
  ![Site sunucusu seçin](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Donanım envanterinde iyileştirmeler
<!-- 1357389 -->
Yeni eklenen sınıflar için 255 karakterden büyük dize uzunlukları, anahtar olmayan donanım Envanter özellikleri için belirtilebilir.

### <a name="try-it-out"></a>Deneyin!  
Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.<br/>

1. **Yönetim** çalışma alanında, **istemci ayarları** ' na tıklayın, düzenlemek için istemci cihaz ayarını vurgulayın, sağ tıklayın ve ardından **Özellikler**' i seçin. 
2. **Donanım envanterini**seçin, sonra **sınıfları ayarlayın**ve **ekleyin**.
3. **Bağlan** düğmesine tıklayın.
4. **Bilgisayar adı**, **WMI ad alanı**' nı doldurup gerekirse **özyinelemeli** ' i seçin. Bağlanmak gerekirse kimlik bilgilerini sağlayın. Ad alanı sınıflarını görüntülemek için **Bağlan** ' a tıklayın.
5. Yeni bir sınıf seçin ve ardından **Düzenle**' ye tıklayın.
6. Anahtar dışındaki bir dize olan en az bir özelliğin **uzunluğunu** 255 ' den büyük olacak şekilde değiştirin. **Tamam**'a tıklayın. 
7. **Donanım envanteri sınıfı Ekle** için düzenlenmiş özelliğin seçildiğinden emin olun ve **Tamam**' a tıklayın. 
8. Yeni eklenen sınıfla 255 karakterden daha büyük bir özellik içeren donanım envanterini toplayın. 



## <a name="improvements-to-client-settings-for-software-center"></a>Yazılım Merkezi için istemci ayarları geliştirmeleri
<!-- 1351224 & 1355146 -->
Technical Preview 'un bu sürümünde, istemci ayarları altında yazılım merkezi özelleştirmesi için geliştirmeler yapılmıştır. 

1. Software Center istemci ayarları 'nda artık bir **Özelleştirme** düğmesi var.
2. Software Center başlığının nasıl göründüğünü göstermek için bir önizleme eklenmiştir.<!--1351224-->
    - Bir logo seçilmezse, önizleme şirket adı metnini ve rengini gösterir.
    - Bir logo seçilirse önizleme, logo ve şirket adı metnini gösterir.  
3.  Yazılım **merkezindeki onaylanmamış uygulamaları Gizle** , yazılım merkezi için yeni bir ayardır. Bu seçenek etkinleştirildiğinde, onay gerektiren Kullanıcı kullanılabilir uygulamaları yazılım merkezi 'nde gizlenir.<!--1355146-->

### <a name="try-it-out"></a>Deneyin!  
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. **Yönetim** çalışma alanında **istemci ayarları**' na tıklayın. Düzenlemek için bir istemci cihaz ayarı seçin. Sağ tıklayın ve ardından **Özellikler** sonra **Yazılım Merkezi**' ni seçin.
2.  **Özelleştir** düğmesine tıklayın. Önizleme dahil farklı özelleştirme ayarlarını deneyin.
3. **Yazılım merkezindeki onaylanmamış uygulamaları Gizle**ayarını etkinleştirin. Yazılım merkezindeki değişiklikleri gözlemleyin. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Windows Defender Application Guard için yeni ayarlar
<!-- 1356256 -->
Windows 10 sürüm 1709 ve üzeri cihazlarda, [Windows Defender Application Guard](../../protect/deploy-use/create-deploy-application-guard-policy.md)için iki yeni ana bilgisayar etkileşimi ayarı vardır. 
1. Web sitelerine, konağın sanal grafik işlemcisine erişim verilebilir. 
2. Kapsayıcı içinde indirilen dosyalar konakta kalıcı olabilir. </br>



## <a name="improvements-to-run-scripts"></a>Betikleri çalıştırma geliştirmeleri
<!-- 1236459 -->
[ **Betikleri Çalıştır** özelliği](../../apps/deploy-use/create-deploy-scripts.md) artık imzalı PowerShell betiklerini içeri aktarmanızı ve çalıştırmanızı sağlar. 
- Betik bütünlüğünü sağlamak için, imzalanmış betikler kopyalama/yapıştırma kullanmak yerine içeri aktarılmalıdır. 
- İçeri aktarılan imzalı betikler içeri aktarma işleminden sonra düzenlenemez.
    
>[!IMPORTANT]
>Bu Technical Preview sürümünde iki geçici kısıtlama vardır.
>- Betikler yalnızca komut dosyalarını çalıştır özelliğinde içeri aktarılabilir ve doğrudan konsolundan düzenlenemez.
>- Unicode olmayan bir kodlama ile içeri aktarılan betikler konsolda yanlış görüntülenebilir. Betiği başlangıçta yazıldığı gibi yürütülmeye devam edecektir.





## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
