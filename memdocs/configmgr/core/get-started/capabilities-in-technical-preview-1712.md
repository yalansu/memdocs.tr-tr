---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1712 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721279"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Configuration Manager için Technical Preview 1712 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1712 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. 

Technical Preview 'un bu sürümünü yüklemeden önce [Configuration Manager Için Teknik önizlemeyi](technical-preview.md) gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve teknik Önizlemedeki özelliklerle ilgili geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


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
  <!--sms489412-->


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Yenisiyle değiştirilen uygulamaları otomatik olarak yükseltme
<!-- 1351266 -->
Bu sürümde, [Kullanıcı sesli geri bildirimlerinize](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)göre, bir uygulama dağıtımını, yenisiyle değiştirilen sürümü otomatik olarak yükseltmeden yapılandırma seçeneğiniz vardır. Dağıtım oluştururken, **Yazılım Dağıtma Sihirbazı**'Nın **dağıtım ayarları** sayfasında, **kullanılabilir** veya **gerekli** Kurulum amacı Için, **Bu uygulamanın yenisiyle değiştirilen sürümlerini otomatik olarak yükseltme**seçeneğini etkinleştirebilir veya devre dışı bırakabilirsiniz.


## <a name="install-multiple-applications-in-software-center"></a>Yazılım Merkezi 'nde birden çok uygulama yükler
<!-- 1357126 -->
Bir son kullanıcının veya masaüstü teknisyenin bir cihaza birden çok uygulama yüklemesi gerekiyorsa, Yazılım Merkezi artık birden fazla seçili uygulamayı yüklemeyi desteklemektedir. Bu, bir sonraki başlatmadan önce bir yüklemenin bitmesini beklemirken kullanıcının daha verimli olmasını sağlar.

**Uygulamalar** sekmesinde Çoklu seçim modu kullanırken, yazılım merkezi 'nin çoklu seçim için hangi uygulamaların etkinleştirmesine ilişkin aşağıdaki ölçütler belirlenir:
- Uygulama kullanıcıya görünür
- Uygulama zaten yüklü değil
- Yönetici onayı gerekli değil veya zaten verilmiş
- Uygulama durumu kullanılabilir (örneğin, içerik indiriyorum)

### <a name="try-it-out"></a>Deneyin!
**Configuration Manager konsolunda:** Kullanılabilir veya gerekli olduğu gibi (gelecekteki son tarihte), yükleme için birden çok uygulamayı bir kullanıcıya veya cihaza dağıtın. Yönetici onayı gerekmez. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).

**Software Center 'da:**
 1. **Uygulamalar** sekmesi varsayılan olarak açılmalıdır. 
 2. Liste görünümünde çoklu seçim moduna girmek için yeni simgesine tıklayın ![Software Center çoklu seçim simgesi](media/software-center-multi-select-apps.png) sağ üst köşede.
 3. Listedeki uygulamaların sol tarafındaki onay kutusuna tıklayarak yüklemek üzere iki veya daha fazla uygulama seçin.
 4. **Seçili yüklensin** düğmesine tıklayın.

Uygulamalar normal olarak yüklenir ve yalnızca hemen birbirini ister.


## <a name="client-based-pxe-responder-service"></a>İstemci tabanlı PXE Yanıtlayıcı hizmeti
<!-- 1357148 -->
Müşteriler için yaygın bir zorluk, çok az sunucu altyapısı olan veya olmayan uzak/şube ofislerinde PXE hizmetleri sağlıyor. Dağıtım noktası rolü, istemci işletim sistemlerini destekler, ancak Windows Dağıtım Hizmetleri bağımlılığı nedeniyle PXE etkin olamaz.

Yeni istemci ayarları artık Configuration Manager istemcilerinde bir PXE Yanıtlayıcı hizmetini etkinleştirmek için kullanılabilir. PXE 'yi destekleyen bir önyükleme görüntüsü, PXE Yanıtlayıcının istemci önbelleğinde bulunmalıdır.

### <a name="try-it-out"></a>Deneyin!
Test ortamında bu istemci PXE Yanıtlayıcısı ile çakışabilecek PXE 'yi destekleyen mevcut dağıtım noktalarının veya diğer PXE sunucularının bulunmadığından emin olun.

Configuration Manager konsolunda:
1. **Yazılım kitaplığı** çalışma alanında, **işletim sistemleri**, **görev dizileri**: özel şablonu kullanarak bir görev dizisi oluşturun.
   1. **Ekle**' ye tıklayın, **genel**' i seçin ve ardından **görev sırası değişkenini ayarla** adımını belirleyin. Görev dizisi değişkeni olarak **SMSTSPersistContent seçeneğinin** girin ve **true**değerini girin.
   1. **Ekle**' ye tıklayın, **yazılım**' i ve ardından **paket içeriğini indir** adımını seçin. Altın yıldız işaretine tıklayıp PXE 'yi destekleyen bir önyükleme görüntüsü seçin. Hem x86 hem de x64 önyükleme görüntülerini dahil edin. **Configuration Manager istemci önbelleğine**yerleştirmek için adımı yapılandırın.
   1. **Ekle**' ye tıklayın, **genel**' i seçin ve ardından **görev sırası değişkenini ayarla** adımını belirleyin. Görev dizisi değişkeni olarak **SMSTSPreserveContent** girin ve **true**değerini girin.
2. **Istemci ayarları**altındaki **Yönetim** çalışma alanında: özel bir istemci cihaz ayarları ilkesi oluşturun.
   1. **Istemci önbelleği ayarları** grubunu seçin.
   1. **Tam işletim sisteminde içerik paylaşmak için Configuration Manager Istemcisini etkinleştir** ayarını **Evet**olarak ayarlayın.
   1. **PXE Yanıtlayıcı hizmetini etkinleştir** ayarını **Evet**olarak ayarlayın.
   1. Otomatik olarak **imzalanan sertifika oluşturma veya BIR PKI istemci sertifikası alma** ayarı için, **sertifika sağla**' ya tıklayın. Test ortamınızda PKI varsa **sertifikayı Içeri aktar** ' ı seçin, aksi takdirde otomatik olarak imzalanan sertifika oluşturmak için **Tamam** ' a tıklayın. 
   1. Geri kalan ayarları test ortamınız için gerektiği şekilde yapılandırın. (Belirli bir ağ veya güvenlik gereksinimi olmadıkça varsayılan ayarlar çalışmalıdır.)
3. Görev sırasını ve özel istemci ayarlarını, hedef istemciler koleksiyonuna PXE Yanıtlayıcıları olacak şekilde dağıtın. İlkelerin uygulanmasını ve görev dizisinin çalışmasını bekleyin.
4. Aynı alt ağdaki başka bir istemciyi PXE/ağ önyüklemesinde normal olarak başlatın.

### <a name="known-issues"></a>Bilinen sorunlar
- Görev sırası Düzenleyicisi, bir önyükleme görüntüsü eklediğinizde **paket Içeriğini indir** adımının kırmızı hata simgesini görüntüler, ancak görev dizisi başarıyla kaydedilir. Bu görev sırasını düzenleyicide tekrar açmak, başvurulan nesnelerin bulunamadığını belirten zararsız bir uyarı da gösterir. <!-- sms427542 -->
- Paket Içeriğini Indir adımındaki önyükleme görüntüsü, özel görev dizisinin başvuru listesinde gösterilmez. Ayrıca **Içerik dağıtma** eylemi kullanılamaz. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager istemci yüklemede değişiklik  
Kullanıcı sesli geri bildirimlerinizin bir sonucu olarak, [Silverlight artık istemcilere otomatik olarak yüklenmez.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Surface cihaz panosuna değiştirme
Surface panosu artık işletim sistemi sürümü yerine yüzey cihazları için bellenim sürümlerini görüntüler. Konsolunda, **izleme** > **yüzeyi cihazları**' na gidin. Aşağıdaki öğeleri görüntüleyebilirsiniz:
- Yüzey yüzdesi
- Yüzey modellerinin yüzdesi
- En popüler beş bellenim sürümü
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Office 365 Istemci yönetimi panosundaki geliştirmeler 
Office 365 Istemci yönetimi panosu artık grafik bölümleri seçildiğinde ilgili cihazların bir listesini görüntüler. Konsolunda, **yazılım kitaplığı** >**'na genel bakış** >**Office 365 istemci yönetimi**' ne gidin. Pano sağda görüntülenir. Grafikten ölçüt seçme, cihazların listesini gösterir.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager konsolundaki geliştirmeler 
Configuration Manager konsolunda, kullanıcı sesli geri bildirimlerinizin bir sonucu olan aşağıdaki geliştirmeleri yaptık.

- [Cihaz listesinde birincil Kullanıcı görüntülenir](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): varlıklar ve uyumluluk altındaki cihaz listeleri, artık birincil kullanıcı varsayılan olarak görüntülenir. Oturum açan Son Kullanıcı, isteğe bağlı bir sütun olarak da eklenebilir. <!-- 1357280 -->
- [Yeniden adlandırılan koleksiyonlar var olan koleksiyon üyeliği kurallarında görüntülenir](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): bir koleksiyon başka bir koleksiyonun üyesiyse ve yeniden adlandırıldığında, yeni ad Üyelik kuralları altında güncelleştirilir.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>İşletim sistemi dağıtımı geliştirmeleri
İşletim sistemi dağıtımı için, bazıları Kullanıcı sesli geri bildirimlerinizin sonucu olan aşağıdaki geliştirmeleri yaptık.
- [Önyükleme görüntüsündeki varsayılan günlük Görüntüleyicisi](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): Windows PE 'de, CMTrace. exe ' yi başlatırken, bu programın günlük dosyaları için varsayılan görüntüleyici yapıp yapmayacağını seçmeniz istenmez. <!-- SMS 500897 -->
- Paket Içeriğini indirme adımı: artık bu görev dizisi adımına önyükleme görüntüleri ekleyebilirsiniz.


## <a name="windows-10-feedback-hub-app-integration"></a>Windows 10 Geri Bildirim Hub 'ı uygulama tümleştirmesi

Windows 10 ' da yerleşik olarak bulunan [geri bildirim Merkezi uygulaması](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) aracılığıyla geri bildirimde bulunduğumuz için geri bildirimde bulunmak istiyoruz. **Yeni geri bildirim eklediğinizde** **Kurumsal Yönetim** kategorisini seçtiğinizden emin olun ve ardından aşağıdaki alt kategorilerinden birini seçin:
- Configuration Manager İstemcisi
- Configuration Manager Konsolu
- Configuration Manager işletim sistemi dağıtımı
- Configuration Manager sunucusu

Configuration Manager yeni özellik fikirlerini Oylamak için [Kullanıcı ses](https://configurationmanager.uservoice.com/) sayfamızı kullanmaya devam edin.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
