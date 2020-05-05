---
title: İşletim sistemi dağıtımına giriş
titleSuffix: Configuration Manager
description: Configuration Manager ortamınızda işletim sistemlerini dağıtmadan önce kavramları anlayın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720390"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Configuration Manager işletim sistemi dağıtımına giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İşletim sistemlerini çeşitli yollarla dağıtmak için Configuration Manager kullanabilirsiniz. İşletim sistemlerinin nasıl dağıtılacağını ve görevlerinin nasıl otomatikleştirildiğini anlamak için bu bölümdeki bilgileri kullanın. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a>İşletim sistemi dağıtım işlemi  
 Configuration Manager, bir işletim sistemini dağıtmak için kullanabileceğiniz çeşitli yöntemler sağlar. Kullandığınız dağıtım yönteminden bağımsız olarak yapmanız gereken çeşitli eylemler vardır:  

-   Önyükleme görüntüsünü başlatmak veya dağıtmanız gereken işletim sistemi görüntüsünü yüklemek için gerekli Windows cihaz sürücülerini belirleyin.  

-   Hedef bilgisayarı başlatmak için kullanmak istediğiniz önyükleme görüntüsünü belirleyin.  

-   Bir görev dizisi kullanarak, dağıtacağınız işletim sisteminin bir görüntüsünü yakalayın. Alternatif olarak, varsayılan bir işletim sistemi görüntüsü kullanabilirsiniz.  

-   Önyükleme görüntüsünü, işletim sistemi görüntüsünü ve ilgili herhangi bir içeriği bir dağıtım noktasına dağıtın.  

-   Önyükleme görüntüsünü ve işletim sistemi görüntüsünü dağıtma adımlarıyla bir görev dizisi oluşturun.  

-   Görev dizisini bir bilgisayar koleksiyonuna dağıtın.  

-   Dağıtımı izleyin.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> İşletim sistemi dağıtım senaryoları  
 Configuration Manager içinde ortamınıza ve işletim sistemi yüklemesinin amacına bağlı olarak seçebileceğiniz çok sayıda işletim sistemi dağıtım senaryosu vardır.  Örneğin, var olan bir bilgisayarı yeni bir Windows sürümüyle bölümleyip biçimlendirebilir veya Windows’u en son sürüme yükseltebilirsiniz. Gereksinimlerinizi karşılayan dağıtım yöntemini belirlemenize yardımcı olmak için, [Kurumsal işletim sistemlerini dağıtmaya yönelik senaryolar](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)konusunu gözden geçirin.  Aşağıdaki işletim sistemi dağıtım senaryolarından birini seçebilirsiniz:  

-   [Windows’u en yeni sürüme yükseltme](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Mevcut bir bilgisayarı değiştirme ve ayarları aktarma](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a>İşletim sistemlerini dağıtma yöntemleri  
 Configuration Manager istemci bilgisayarlara işletim sistemlerini dağıtmak için kullanabileceğiniz çeşitli yöntemler vardır.  

- **PXE tarafından başlatılan dağıtımlar**: PXE tarafından başlatılan dağıtımlar, istemci bilgisayarlarının ağ üzerinde bir dağıtım talep etmesini sağlar. Bu dağıtım yönteminde, işletim sistemi görüntüsü ve bir Windows PE önyükleme görüntüsü, PXE başlatma taleplerini kabul etmek üzere yapılandırılmış bir dağıtım noktasına gönderilir. Daha fazla bilgi için bkz. [Configuration Manager ile ağ üzerinden Windows dağıtmak IÇIN PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **İşletim sistemlerini Yazılım Merkezi’nde kullanılabilir yap**: Bir işletim sistemini dağıtabilir ve Yazılım Merkezi’nde kullanılabilir hale getirebilirsiniz. Configuration Manager istemcileri, işletim sistemi yüklemesini Yazılım Merkezi 'nden başlatabilir. Daha fazla bilgi için bkz. [var olan bir bilgisayarı değiştirme ve ayarları aktarma](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Çok noktaya yayın dağıtımları**: Çok noktaya yayın dağıtımları, verilerin bir kopyasını ayrı bir bağlantı üzerinden her bir istemciye göndermek yerine, verileri birden çok istemciye eş zamanlı olarak göndererek, ağ bant genişliği tasarrufu yapar. Bu dağıtım yönteminde, işletim sistemi görüntüsü bir dağıtım noktasına gönderilir. Bu ardından, istemci bilgisayarları dağıtımı talep ettiğinde, görüntüyü dağıtır. Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Önyüklenebilir medya dağıtımları**: Önyüklenebilir medya dağıtımları, hedef bilgisayar başladığında işletim sistemini dağıtmanızı sağlar. Hedef bilgisayar başladığında, görev dizisini, işletim sistemi görüntüsünü ve gerekli herhangi diğer içeriği ağdan alır. İçerik medyada yer almadığından, medyayı yeniden oluşturmaya gerek olmadan içeriği güncelleştirebilirsiniz. Daha fazla bilgi için bkz. [önyüklenebilir medya oluşturma](../deploy-use/create-bootable-media.md).  

- **Tek başına medya dağıtımları**: Tek başına medya dağıtımları aşağıdaki durumlarda işletim sistemlerini dağıtmanızı sağlar:  

  - Bir işletim sistemi görüntüsünün veya başka büyük paketlerin ağ üzerinden kopyalanması uygun olmayan ortamlarda.  

  - Ağ bağlantısı olmayan veya düşük bant genişliğine sahip ağ bağlantısı olan ortamlarda.  

    Daha fazla bilgi için bkz. [tek başına medya oluşturma](../deploy-use/create-stand-alone-media.md).  

- **Önceden hazırlanmış medya dağıtımları**: Önceden hazırlanmış medya dağıtımları bir işletim sistemini tam olarak sağlanmamış bir bilgisayara dağıtmanızı sağlar. Önceden hazırlanmış medya, üretici tarafından veya Configuration Manager ortamına bağlı olmayan bir kuruluş hazırlama merkezinde çıplak bir bilgisayara yüklenebilen bir Windows Imaging Format (WıM) dosyasıdır.  

   Daha sonra Configuration Manager ortamında, bilgisayar, medya tarafından sağlanan önyükleme görüntüsünü kullanarak başlar ve ardından indirme işlemini tamamlayan kullanılabilir görev dizileri için site yönetim noktasına bağlanır. Önyükleme görüntüsü ve işletim sistemi görüntüsü zaten hedef bilgisayarda olduğundan, bu dağıtım yöntemi ağ trafiğini azaltabilir. Önceden hazırlanmış medyanın dahil edileceği uygulamaları, paketleri ve sürücü paketlerini belirtebilirsiniz. Daha fazla bilgi için bkz. [önceden hazırlanmış medya oluşturma](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a>Önyükleme görüntüleri  
 Configuration Manager bir önyükleme görüntüsü, işletim sistemi dağıtımı sırasında kullanılan bir Windows PE (WinPE) görüntüsüdür. Önyükleme görüntüleri, hedef bilgisayarı Windows yüklemesine hazırlayan sınırlı bileşen ve hizmetlere sahip en yalın işletim sistemi olan WinPE’de bilgisayarı başlatmak için kullanılır. Configuration Manager iki önyükleme görüntüsü sağlar: biri x86 platformlarını ve diğeri de x64 platformlarını destekler. Bunlar varsayılan önyükleme görüntüsü olarak kabul edilir. Oluşturduğunuz ve Configuration Manager ekleyeceğiniz önyükleme görüntüleri özel görüntüler olarak kabul edilir. Configuration Manager güncelleştirdiğinizde varsayılan önyükleme görüntüleri otomatik olarak değiştirilebilir. Önyükleme görüntüleri hakkında daha fazla bilgi için bkz. [Önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a>İşletim sistemi görüntüleri  
 Configuration Manager içindeki işletim sistemi görüntüleri Windows Imaging File (WIM) dosya biçiminde depolanır ve bir işletim sistemini bilgisayara başarıyla yüklemek ve yapılandırmak için gereken başvuru dosya ve klasörlerinden oluşan sıkıştırılmış bir koleksiyonu temsil ederler. Tüm işletim sistemi dağıtım senaryoları için bir işletim sistemi görüntüsü seçmeniz gerekir. Varsayılan işletim sistemi görüntüsünü kullanabilir veya yapılandırdığınız bir başvuru bilgisayarından işletim sistemi görüntüsünü oluşturabilirsiniz. Daha fazla bilgi için bkz. [işletim sistemi görüntülerini yönetme](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a>İşletim sistemi yükseltme paketleri  
 İşletim sistemi yükseltme paketleri bir işletim sistemini yükseltmek için kullanılır ve kurulumla başlatılan işletim sistemi dağıtımlarıdır. İşletim sistemi yükseltme paketlerini bir DVD veya bağlı ISO dosyasından Configuration Manager içeri aktarırsınız. Daha fazla bilgi için bkz. [işletim sistemi yükseltme paketlerini yönetme](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a>İşletim sistemlerini dağıtmak için medya  
 İşletim sistemlerini dağıtmak için kullanılabilecek çeşitli türlerde medya oluşturabilirsiniz. Bu, işletim sistemi görüntülerini yakalamak için kullanılan yakalama medyasını, bir işletim sistemini dağıtmak için kullanılan önyüklenebilir ve önceden hazırlanmış medyayı içerir. Medya kullanarak, işletim sistemlerini, bir ağ bağlantısı olmayan veya Configuration Manager sitenize düşük bant genişliğine sahip bir bağlantısı olan bilgisayarlara dağıtabilirsiniz. Medyanın nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [görev dizisi medyası oluşturma](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Cihaz sürücüleri  
 Cihaz sürücülerini dağıtılmakta olan işletim sistemi görüntüsüne eklemeden hedef bilgisayarlara yükleyebilirsiniz. Configuration Manager, Configuration Manager içine aktardığınız tüm cihaz sürücülerine yönelik başvuruları içeren bir sürücü kataloğu sağlar. Sürücü kataloğu, **Yazılım Kitaplığı** çalışma alanında bulunur ve iki düğümden oluşur: **Sürücüler** ve **Sürücü Paketleri**. **Sürücüler** düğümü, sürücü kataloğu içine aktardığınız tüm sürücüleri listeler. Bu düğümü, her bir içe aktarılan sürücü hakkında ayrıntıları keşfetmek, bir sürücünün hangi sürücü paketi veya önyükleme görüntüsüne ait olduğunu değiştirmek, bir sürücüyü etkinleştirmek ya da devre dışı bırakmak ve başka şeyler için kullanabilirsiniz. Daha fazla bilgi için bkz. [sürücüleri yönetme](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> Kullanıcı durumunu kaydetme ve geri yükleme  
 İşletim sistemlerini dağıttığınızda, hedef bilgisayardan kullanıcı durumunu kaydedebilir, işletim sistemini dağıtabilir ve ardından işletim sistemi dağıtıldıktan sonra kullanıcı durumunu geri yükleyebilirsiniz. Bu işlem, genellikle işletim sistemini bir Configuration Manager istemci bilgisayarına yüklediğinizde kullanılır.  

 Kullanıcı durumu bilgisi, görev dizileri kullanılarak yakalanır ve geri yüklenir. Kullanıcı durumu bilgisi yakalandığında, bilgiler aşağıdaki yöntemlerin biri kullanılarak depolanabilir:  

- Kullanıcı durumu verilerini, bir durum geçiş noktası yapılandırarak uzaktan depolayabilirsiniz. Yakala görev sırası, verileri durum geçiş noktasına gönderir. Ardından, işletim sistemi dağıtıldıktan sonra, Geri yükle görev sırası, verileri alır ve kullanıcı durumunu hedef bilgisayarda geri yükler.  

- Kullanıcı durumu verilerini, yerel olarak belirli bir konuma depolayabilirsiniz. Bu senaryoda, Yakala görev sırası, kullanıcı verilerini hedef bilgisayardaki belirli bir konuma kopyalar. Ardından, işletim sistemi dağıtıldıktan sonra, Geri yükle görev sırası, kullanıcı verilerini o konumdan alır.  

- Kullanıcı verilerini orijinal konumuna geri yüklemek üzere kullanılabilecek sabit bağlantılar belirtebilirsiniz. Bu senaryoda, kullanıcı durumu verileri, eski işletim sistemi kaldırıldığında sürücüde kalır. Ardından, işletim sistemi dağıtıldıktan sonra, Geri yükle görev sırası, kullanıcı durumu verilerini orijinal konumuna geri yüklemek için sabit bağlantıları kullanır.  

  Daha fazla bilgi için [Kullanıcı durumunu yönetin](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Bilinmeyen bilgisayarlara dağıtma  
 Bir işletim sistemini, Configuration Manager tarafından yönetilmeyen bilgisayarlara dağıtabilirsiniz. Configuration Manager veritabanında bu bilgisayarların kaydı yoktur. Bu bilgisayarlar bilinmeyen bilgisayarlar olarak adlandırılır. Bilinmeyen bilgisayarlar aşağıdakileri içerir:  

- Configuration Manager istemcisinin yüklü olmadığı bir bilgisayar  

- Configuration Manager içine aktarılmayan bir bilgisayar  

- Configuration Manager tarafından bulunmayan bir bilgisayar  

  Daha fazla bilgi için bkz. [bilinmeyen bilgisayar dağıtımları Için hazırlanma](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a>Kullanıcıları bir bilgisayarla ilişkilendirme  
 Bir işletim sistemini dağıttığınızda, kullanıcı aygıtı benzeşimi eylemlerini desteklemek için kullanıcıları hedef bilgisayarla ilişkilendirebilirsiniz. Bir kullanıcıyı hedef bilgisayarla ilişkilendirdiğinizde, yönetim kullanıcısı daha sonra, o kullanıcıyla ilişkili herhangi bir bilgisayarda, belirli bir kullanıcının bilgisayarına bir uygulama dağıtmak gibi eylemleri yapabilir. Ancak, bir işletim sistemi dağıttığınızda, işletim sistemini belirli bir kullanıcının bilgisayarına dağıtamazsınız. Daha fazla bilgi için bkz. [kullanıcıları bir hedef bilgisayarla ilişkilendirme](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> Adımları otomatikleştirmek için görev dizilerini kullanma  
 Configuration Manager ortamınızda çeşitli görevleri gerçekleştirmek için görev dizileri oluşturabilirsiniz. Görev dizisinin eylemleri, dizinin tek tek adımlarında tanımlanır. Görev dizisi çalıştırıldığında, her bir adımın eylemleri, kullanıcı müdahalesi gerektirmeden, komut satırı düzeyinde gerçekleştirilir. Görev dizilerini aşağıdaki amaçlarla kullanabilirsiniz:  

-   [İşletim sistemini yüklemek için görev dizisi oluşturma](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [İşletim sistemi dışı dağıtımlar için görev dizisi oluşturma](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [İşletim sistemini yakalamak için görev dizisi oluşturma](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Kullanıcı durumunu yakalamak ve geri yüklemek için görev dizisi oluşturma](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Özel bir görev sırası oluşturma](../deploy-use/create-a-custom-task-sequence.md)  
