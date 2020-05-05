---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1708 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721335"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Configuration Manager için Technical Preview 1708 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1708 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bu teknik önizlemede bilinen sorunlar:**
- **Pasif modda bir site sunucunuz varsa, Preview sürüm 1708 ' e güncelleştirme başarısız olur**. Önizleme sürümü 1706 veya 1707 ' i çalıştırdığınızda ve [pasif modda bir birincil site sunucusuna](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)sahipseniz, önizleme sitenizi sürüm 1708 ' ye başarıyla güncelleştirebilmeniz için Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz sürüm 1708 ' i çalıştırdıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Konsolunda **Yönetim** > **genel bakış** > **Site yapılandırması** > **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
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

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Configuration Manager PowerShell betikleri dağıtırken betik parametrelerini belirtme iyileştirmeleri
<!-- 1236459 -->

Configuration Manager 1706 ve sonraki sürümlerde, [PowerShell betiklerini Configuration Manager konsolundan oluşturup çalıştırabilirsiniz](../../apps/deploy-use/create-deploy-scripts.md).

[Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)' de, komut dosyasından parametre okuma Configuration Manager izin vermek için bu özelliği genişlettik.

Bu Technical Preview 'da, hangi parametrelerin zorunlu olduğunu ve isteğe bağlı olduğunu tespit etmek için komut dosyası parametreleri özelliğini genişlettik ve bunları girmenizi ister.

### <a name="try-it-out"></a>Deneyin!

1. [Configuration Manager konsolundan PowerShell betikleri oluşturmak ve çalıştırmak](../../apps/deploy-use/create-deploy-scripts.md)için yönergeleri izleyin.
2. **Betik oluşturma sihirbazının**yeni **betik parametreleri** sayfasında bir parametre seçin ve ardından değerlerini düzenleyin.
Sihirbaz zorunlu olan ve isteğe bağlı olan parametreleri görüntüler.
4. Parametreleri düzenlemenizi bitirdiğinizde Sihirbazı doldurun.

Betik çalıştırıldığında, yapılandırdığınız tüm parametre değerlerini kullanır. Zorunlu bir parametre yapılandırmadıysanız, komut dosyası çalıştırıldığında son kullanıcıdan parametresini sağlaması istenir.

## <a name="management-insights"></a>Yönetim içgörüleri
<!-- 1353967 -->
Artık, site veritabanındaki verilerin analizine dayalı olarak ortamınızın geçerli durumu hakkında öngörüler elde edebilirsiniz. Öngörüler, ortamınızı daha iyi anlamanıza ve öngörülere göre işlem yapmanıza yardımcı olur. **Yönetim** > **yönetimi öngörülerinin** > **Tüm öngörülerini**Configuration Manager konsolundaki yönetim öngörülerini inceleyin. Bu sürümde, aşağıdaki Öngörüler artık kullanılabilir:

- **Dağıtımsız uygulamalar**: ortamınızda etkin dağıtımlar bulunmayan uygulamaları listeler. Bu, konsolunda görünen uygulamaların listesini basitleştirmek için kullanılmayan uygulamaları bulmanıza ve silmeye yardımcı olur.
- **Boş Koleksiyonlar**: ortamınızda üyesi olmayan koleksiyonları listeler. Bu koleksiyonları, örneğin nesneleri dağıtıldığında görüntülenecek koleksiyonların listesini basitleştirmek için silebilirsiniz.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Configuration Manager konsolundan bilgisayarları yeniden başlatma   
<!-- 1356283 -->
Bu sürümden itibaren, yeniden başlatma gerektiren istemci cihazlarını belirlemek için Configuration Manager konsolunu kullanabilir ve sonra yeniden başlatmak için bir istemci bildirim eylemi kullanabilirsiniz.

Yeniden başlatma bekleyen cihazları tanımlamak için **varlıklar ve uyumluluk** > **cihazları** ' na gidin ve yeniden başlatma gerektirebilecek cihazlara sahip bir koleksiyon seçin. Bir koleksiyon seçtikten sonra, Ayrıntılar bölmesinde her bir cihazın durumunu, **bekleyen yeniden başlatma**adlı yeni bir sütunda görüntüleyebilirsiniz. Her aygıtın değeri **Evet**veya **Hayır**.

Bir cihazı yeniden başlatmak üzere istemci bildirimi oluşturmak için:
1. Konsolunun cihazlar düğümünde yeniden başlatmak istediğiniz cihazı bulun.
2. Cihaza sağ tıklayın, **Istemci bildirimi**' ni seçin ve ardından **Yeniden Başlat**' ı seçin. Bu, yeniden başlatma ile ilgili bir bilgi penceresi açar. Yeniden başlatma isteğini onaylamak için **Tamam** ' ı tıklatın.

Bildirim bir istemci tarafından alındığında, kullanıcıyı yeniden başlatma hakkında bilgilendirmek için bir **Yazılım Merkezi** bildirim penceresi açılır. Yeniden başlatma işlemi varsayılan olarak 90 dakika sonra gerçekleşir. [İstemci ayarlarını](../clients/deploy/configure-client-settings.md)yapılandırarak yeniden başlatma süresini değiştirebilirsiniz. Yeniden başlatma davranışı ayarları, varsayılan ayarların [bilgisayar yeniden başlatma](../clients/deploy/about-client-settings.md#computer-restart) sekmesinde bulunur.


### <a name="try-it-out"></a>Deneyin!
Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için şeridin **giriş** sekmesinden bize **geri bildirim** gönderin:
1. Yüklemeyi tamamlamaya yönelik cihazın yeniden başlatılmasını gerektiren bir cihaza uygulama veya güncelleştirme dağıtın.
2. Cihazı, konsolunun **varlıklar ve uyumluluk** > **cihazları** düğümünde bulun ve **bekleyen yeniden başlatma** sütununda **Evet** ' i görüntülendiğini onaylayın. Bekleyen yeniden başlatma durumunun konsolda yansıtılması 20 dakikaya kadar sürebilir.
3. Yazılım Merkezi bildiriminin açıldığını ve cihazın başarıyla yeniden başlatıldıklarını onaylamak için cihazı izleyin.


## <a name="software-center-customization"></a>Yazılım Merkezi özelleştirmesi
<!-- 1351224 -->
Kurumsal marka öğeleri ekleyebilir ve yazılım merkezi 'ndeki sekmelerin görünürlüğünü belirtebilirsiniz. Yazılım merkezine özgü şirket adınızı ekleyebilir, bir yazılım merkezi yapılandırma renk teması ayarlayabilir, bir şirket logosu ayarlayabilir ve istemci cihazları için görünür sekmeleri ayarlayabilirsiniz.

### <a name="customize-software-center"></a>Yazılım merkezini özelleştirme

Yazılım merkezini değiştirmek için:

1. **Configuration Manager** konsolunda **Yönetim** > **istemci ayarları**' nı seçin. İstediğiniz istemci ayarı örneğine tıklayın.
2. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.
3. **Varsayılan ayarlar** Iletişim kutusunda **Yazılım Merkezi**' ni seçin.
4. Yazılım Merkezi özelleştirmesi ayarlarınızı etkinleştirmek üzere **Şirket bilgilerini belirtmek için yeni ayarları seçmek** üzere **Evet** ' i seçin.
5. **Şirketinizin adını**yazın.
6. **Yazılım Merkezi Için renk düzeninizi**seçin.
7. Yazılım Merkezi için logonuz gitmek üzere, **Araştır** ' a tıklayın. Logo, en fazla 750 KB boyutundaki 400 x 100 piksellik bir JPEG veya PNG olmalıdır.
8. Sekmeleri istemci cihazlar için yazılım merkezi 'nde görünür hale getirmek için **Evet** ' i seçin. En az bir sekme görünür olmalıdır:

    -  Uygulamaları etkinleştir sekmesi
    -  Güncelleştirmeleri etkinleştir sekmesi
    -  Işletim sistemleri sekmesini etkinleştir
    -  Yükleme durumu sekmesini etkinleştir
    -  Cihaz uyumluluğu sekmesini etkinleştir
    -  Seçenekler sekmesini etkinleştir

### <a name="next-steps"></a>Sonraki adımlar

Configuration Manager 'de uygulama yönetimi hakkında daha fazla bilgi edinmek için bkz. [uygulama yönetimine giriş](../../apps/understand/introduction-to-application-management.md).
