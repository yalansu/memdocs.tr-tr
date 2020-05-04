---
title: Linux ve UNIX için donanım envanteri
titleSuffix: Configuration Manager
description: Configuration Manager ' de Linux ve UNIX için donanım envanterini nasıl kullanacağınızı öğrenin.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1bdfb8c6d528c12581f05f86111a1a76d2259faa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714426"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Configuration Manager 'de Linux ve UNIX için donanım envanteri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Linux ve UNIX için Configuration Manager istemcisi donanım envanterini destekler. Donanım envanterini topladıktan sonra kaynak gezgininde veya Configuration Manager raporlarında envanteri çalıştırabilir ve bu bilgileri kullanarak aşağıdaki işlemleri etkinleştiren sorgular ve koleksiyonlar oluşturabilirsiniz:  

- Yazılım dağıtımı  

- Bakım pencerelerini zorlama  

- Özel istemci ayarlarını dağıtma  

Linux ve UNIX sunucuları için donanım envanteri, standartlara dayalı Genel Bilgi Modeli (CıM) sunucusu kullanır. CIM sunucusu bir yazılım hizmeti (veya arka plan programı) olarak çalışır ve Dağıtılmış Yönetim Araştırma Grubu (DMTF) standartlarını temel alan bir yönetim altyapısı sağlar. CIM sunucusu, Windows tabanlı bilgisayarlarda kullanılabilen Windows Yönetim Alt Yapısı (WMI) CIM özelliklerine benzer işlevsellik sağlar.  

Toplu güncelleştirme 1 ' den itibaren, Linux ve UNIX için istemcisi açık **gruptan**açık kaynaklı **omiserver** sürüm 1.0.6 kullanır. (Toplu güncelleştirme 1’den önce istemci CIM sunucusu olarak **nanowbem** kullanıyordu).  

CIM sunucusu Linux ve UNIX istemcisinin bir parçası olarak yüklenir. Linux ve UNIX için istemcisi, CıM sunucusu ile doğrudan iletişim kurar ve CıM sunucusunun WS-MAN arabirimini kullanmaz. İstemci yüklendiğinde CIM sunucusu üzerindeki WS-MAN bağlantı noktası devre dışı bırakılır. Microsoft şu anda Açık Yönetim Altyapısı (OMI) projesi yoluyla açık kaynak olarak kullanılabilen CIM sunucusunu geliştirmiştir. Açık Yönetim Altyapısı projesi hakkında daha fazla bilgi için [Açık Grup](https://www.opengroup.org/) web sitesine bakın.  

Linux ve UNIX sunucuları üzerindeki Donanım Envanteri, var olan Win32 WMI sınıflarını ve özelliklerini Linux ve UNIX sunucularının eşdeğer sınıf ve özellikleriyle eşleyerek çalışır. Sınıfların ve özelliklerin bu bire bir eşlemesi, Linux ve UNIX donanım envanterinin Configuration Manager tümleştirilmesine olanak sağlar. Linux ve UNIX sunucularından alınan envanter verileri, Configuration Manager konsolu ve raporlarında Windows tabanlı bilgisayarlardan envanter ile birlikte görüntülenir. Bu davranış tutarlı bir heterojen yönetim deneyimi sağlar.  

> [!TIP]  
>  Sorgu ve koleksiyonlarda farklı Linux ve UNIX işletim sistemlerini tanımlamak üzere **İşletim Sistemi** sınıfının **Resim Yazısı** değerini kullanabilirsiniz.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Linux ve UNIX sunucuları için donanım envanterini yapılandırma  
 Varsayılan istemci ayarlarını kullanabilir veya özel istemci cihaz ayarları oluşturarak donanım envanterini yapılandırabilirsiniz. Özel istemci cihaz ayarlarını kullandığınızda yalnızca Linux ve UNIX sunucularınızdan toplamak istediğiniz sınıfları ve özellikleri yapılandırabilirsiniz. Ayrıca Linux ve UNIX sunucularınızdan tam ve delta envanterlerin ne zaman toplanacağına ilişkin özel zamanlamalar belirtebilirsiniz.  

 Linux ve UNIX istemcisi, Linux ve UNIX sunucularında kullanılabilen aşağıdaki donanım envanteri sınıflarını destekler:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Bu envanter sınıflarının tüm özellikleri, Configuration Manager Linux ve UNIX bilgisayarlar için etkin değildir.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Donanım envanteri işlemleri  
 Linux ve UNIX sunucularınızdan donanım envanterini topladıktan sonra, bu bilgileri diğer bilgisayarlardan topladığınız envanteri görüntülediğiniz şekilde görüntüleyip kullanabilirsiniz:  

- Linux ve UNIX sunucularından donanım envanteri hakkında ayrıntılı bilgi görüntülemek için Kaynak Gezgini’ni kullanın  

- Belirli donanım yapılandırmalarını temel alan sorgular oluşturun  

- Belirli donanım yapılandırmalarını temel alan, sorgu tabanlı koleksiyonlar oluşturun  

- Donanım yapılandırmalarının belirli ayrıntılarını görüntüleyen raporlar çalıştırın  

Bir Linux veya UNIX sunucusundaki donanım envanteri, istemci ayarlarında yapılandırdığınız zamanlamaya göre çalışır. Varsayılan olarak, bu zamanlama her yedi günde bir olur. Linux ve UNIX istemcisi hem tam envanter döngülerini hem de delta envanter döngülerini destekler.  

Ayrıca, bir Linux veya UNIX sunucusu üzerindeki istemciyi donanım envanterini hemen çalıştırmaya zorlayabilirsiniz. Donanım envanterini çalıştırmak için bir istemcide **kök** kimlik bilgilerini kullanarak bir donanım envanteri döngüsünü başlatmak üzere aşağıdaki komutu çalıştırın:`/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

Donanım envanteri eylemleri **scxcm.log**adlı istemci günlük dosyasına girilir.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Özel donanım envanteri oluşturmak için Açık Yönetim Altyapısı kullanma  
 Linux ve UNIX istemcisi, Açık Yönetim Altyapısı (OMI) kullanarak oluşturabileceğiniz özel donanım envanterini destekler. Bunu yapmak için aşağıdaki adımları kullanın:  

1.  OMI kaynağını kullanarak özel bir envanter sağlayıcısı oluşturma  

2.  Envanteri raporlamak üzere yeni sağlayıcıyı kullanmak için bilgisayarları yapılandırın  

3.  Yeni sağlayıcıyı desteklemek için Configuration Manager etkinleştir  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Linux ve UNIX bilgisayarlar için özel bir donanım envanteri oluşturun:  
 Linux ve UNIX için Configuration Manager istemcisi için özel bir donanım envanteri sağlayıcısı oluşturmak için **OMI kaynağı-v. 1.0.6** kullanın ve OMI Başlangıç Kılavuzu 'ndaki yönergeleri izleyin. Bu işlem yeni sağlayıcının şemasını tanımlayan bir Yönetilen Nesne Biçimi (MOF) dosyası oluşturmayı içerir. Daha sonra, yeni özel envanter sınıfının desteğini etkinleştirmek için Configuration Manager MOF dosyasını içeri aktarırsınız.  

 Hem OMI Kaynağı - v.1.0.6 hem de OMI Başlangıç Kılavuzu [Açık Grup](https://github.com/microsoft/omi/blob/master/README.md) web sitesinden indirilebilir. Bu indirmeleri OpenGroup.org web sitesinde aşağıdaki web sayfasında bulunan **Belgeler** sekmesine yerleştirebilirsiniz: [Açık Yönetim Altyapısı (OMI)](https://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Özel donanım envanteri sağlayıcısı ile Linux veya UNIX çalıştıran her bilgisayarı yapılandırın:  
 Özel bir envanter sağlayıcısı oluşturduktan sonra, toplanacak envanteri içeren her bir bilgisayarda sağlayıcı kitaplık dosyasını kopyalamanız ve ardından kaydetmeniz gerekir.  

1.  Sağlayıcı kitaplığını, envanteri toplamak istediğiniz her Linux ve UNIX bilgisayarına kopyalayın. Sağlayıcı kitaplığının adı şu ada benzer: **XYZ_MyProvider. bu nedenle**  

2.  Ardından, her bir Linux ve UNIX bilgisayarında sağlayıcı kitaplığını OMI sunucusuna kaydedin. Linux ve UNIX için Configuration Manager istemcisini yüklediğinizde OMı sunucusu bilgisayara yüklenir, ancak özel sağlayıcıları elle kaydetmeniz gerekir. Sağlayıcıyı kaydetmek için aşağıdaki komut satırını kullanın:`/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  Yeni sağlayıcıyı kaydettikten sonra **omicli** aracını kullanarak sağlayıcıyı test edin. Linux ve UNIX için Configuration Manager istemcisini yüklediğinizde **omicli** aracı her bir LINUX ve UNIX bilgisayara yüklenir. Örneğin, **XYZ_MyProvider** öğesinin oluşturduğunuz sağlayıcının adı olduğu aşağıdaki komutu bilgisayarda çalıştırın: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     **Omicli** ve test özel sağlayıcılar hakkında daha fazla bilgi için bkz. OMI Başlangıç Kılavuzu.  

> [!TIP]  
>  Özel sağlayıcıları dağıtmak ve özel sağlayıcıları her bir Linux ve UNIX istemci bilgisayarına kaydetmek için yazılım dağıtımını kullanın.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Configuration Manager’da yeni envanter sınıfını etkinleştirin:  
 Configuration Manager, Linux ve UNIX bilgisayarlarda yeni sağlayıcı tarafından bildirilen envanterde raporlanması için, özel sağlayıcınızın şemasını tanımlayan Yönetilen Nesne Biçimi (MOF) dosyasını içeri aktarmanız gerekir.  

 Özel bir MOF dosyasını Configuration Manager içine aktarmak için bkz. [donanım envanterini yapılandırma](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
