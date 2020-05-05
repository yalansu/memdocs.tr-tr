---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1711 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721293"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Configuration Manager için Technical Preview 1711 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1711 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bu teknik önizlemede bilinen sorunlar:**
- **Windows 10, sürüm 1709 (Fall Creators Update olarak da bilinir) desteği**.  Bu Windows sürümünden itibaren, Windows Media birden çok sürüm içerir. Bir görev dizisini bir işletim sistemi yükseltme paketi veya işletim sistemi görüntüsü kullanacak şekilde yapılandırırken, [Configuration Manager tarafından kullanılmak üzere desteklenen bir sürüm](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)seçtiğinizden emin olun.
- **Pasif modda bir site sunucunuz varsa yeni bir önizleme sürümüne güncelleştirme başarısız olur**. [Pasif modda birincil site sunucusuna](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)sahip bir önizleme sürümü çalıştırdığınızda, önizleme sitenizi bu yeni önizleme sürümüne başarıyla güncelleştirebilmeniz için Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz güncelleştirmeyi tamamladıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Konsolunda **Yönetim** > **genel bakış** > **Site yapılandırması** > **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
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

## <a name="improvements-to-run-task-sequence"></a>Görev dizisi çalıştırma geliştirmeleri
<!-- 1261338 -->

Bu Technical Preview, görev dizisi Çalıştır adımını geliştirir. Geliştirmeler aşağıdaki öğeleri içerir:

- Yazılım Merkezi, PXE ve medyadan tüm işletim sistemi dağıtım senaryoları için destek.
- Nesne silme sırasında kopyalama, içeri aktarma, dışarı aktarma ve uyarı gibi konsol eylemlerine yönelik geliştirmeler.
- **Önceden hazırlanan Içerik oluşturma** Sihirbazı desteği.
- Dağıtım doğrulama ile tümleştirme.
- Görev sırasını Çalıştır adımı artık yalnızca tek bir üst-alt ilişkisi değil birden çok görev dizisi düzeyinde kullanılabilir. Çok düzeyli ilişkiler karmaşıklığı artırır, bu nedenle dikkatli olun. Bu ilişkiler hala döngüsel başvurular için denetlenir.

### <a name="try-it-out"></a>Deneyin!  

Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için şeridin **giriş** sekmesinden bize **geri bildirim** gönderin:

1. Görev sırası düzenleyicisinde, **Ekle**' ye tıklayın, **genel**' i seçin ve **görev sırasını Çalıştır**' a tıklayın.
2. Alt görev sırasını seçmek için, **Araştır** ' a tıklayın.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Uygulama yüklenirken kullanıcı etkileşimine izin ver <!-- 1356976 -->

Bu önizleme ile, son kullanıcının görev dizisinin çalıştırılması sırasında bir uygulama yüklemesiyle etkileşime girmesine izin verebilirsiniz. Örneğin, son kullanıcıya çeşitli seçenekler için istemde bulunan bir kurulum işlemi çalıştırın. Bazı uygulama yükleyicilerinin Kullanıcı istemlerinin susuyor olması veya yükleme işleminin yalnızca Kullanıcı tarafından bilinen belirli yapılandırma değerlerinin olması gerekebilir. Bu özellik, bu yükleme senaryolarını idare etmenizi sağlar.

### <a name="try-it-out"></a>Deneyin!

Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin:

1.  Bir uygulama oluşturun veya düzenleyin. Daha fazla bilgi için bkz. [Configuration Manager uygulama oluşturma](../../apps/deploy-use/create-applications.md).

    a. **Windows Installer (\*MSI dosyası) özelliklerindeki** **Kullanıcı deneyimi** sekmesini seçin.

    b. Yüklenecek **sistem** **davranışı**için yüklemeyi seçin.

    c. Kullanıcının **oturum açma gereksinimi**için **oturum açıp açmamadığını** seçin.

    d. **Yükleme programı görünürlüğü**için **normal** ' i seçin. Üç seçenekten istediğinizi seçebilirsiniz: **küçültülmüş**, **normal**veya **ekranı kaplamış**.

    e. **Kullanıcıların program yüklemesiyle etkileşime girmesine Izin ver** kutusunu seçin.

2.  Uygulamayı **Install** adımını kullanarak uygulamayı yüklemek için bir görev dizisi oluşturun veya düzenleyin. Daha fazla bilgi için bkz. [görev dizisi adımlarında](../../osd/understand/task-sequence-steps.md) [uygulamayı yüklemeyi](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) .

    a. Windows 'U ve Configuration Manager adımından sonra görüntüleme görevi sırası.

    b. Son Işleme grubundaki yerinde yükseltme görev sırası.

3.  Görev sırasını bir istemciye dağıtın.
4.  Görev sırasını yazılım merkezi 'nden yükler.

Görev sırası ilerlemesi sırasında, uygulama yükleme arabirimi hedef Son Kullanıcı cihazında görüntülenir. Görev sırası ilerlemesi, son kullanıcı uygulama yüklemesi iş akışını tamamlayana kadar duraklatılır.

### <a name="install-using-the-wizard"></a>Sihirbazı kullanarak yüklemeyi

Bu özelliği Sihirbazı kullanarak bir uygulama dağıttığınızda de kullanabilirsiniz.

1. Bir uygulama oluşturun veya düzenleyin.
2. Uygulamayı bir istemciye dağıtın.
3. Uygulamayı Yazılım Merkezi ' nden yükler. Uygulama yükleme arabirimi görüntülenmelidir. Son Kullanıcı uygulama yükleme Sihirbazı 'nı izlemelidir ve uygulama başarıyla yüklenir.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Sonraki Adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
