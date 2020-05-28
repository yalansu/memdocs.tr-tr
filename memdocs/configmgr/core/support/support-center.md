---
title: Destek Merkezi
titleSuffix: Configuration Manager
description: Destek Merkezi ile Configuration Manager istemcilerin sorunlarını giderin.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: da2fe2ad66617ffb5ad3058011f111b0aaf9e9ae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903904"
---
# <a name="support-center-for-configuration-manager"></a>Configuration Manager için destek merkezi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357489-->
Sürüm 1810 ' den başlayarak, istemci sorunlarını giderme, gerçek zamanlı günlük görüntüleme veya Configuration Manager istemci bilgisayarının durumunu daha sonra analiz edilmek üzere yakalama için destek merkezini kullanın. Destek Merkezi, birçok yönetici sorun giderme aracını birleştiren tek bir araçtır.


## <a name="about"></a>Hakkında

Configuration Manager istemci bilgisayarlarda sorun giderirken sorunları ve sorunları azaltmak için destek merkezi amaçlar. Daha önce, Configuration Manager istemcilerde bir sorunu gidermeye yönelik destekle çalışırken, sorun gidermeye yardımcı olmak için günlük dosyalarını ve diğer bilgileri el ile toplamanız gerekir. Önemli bir günlük dosyasını yanlışlıkla unutmak kolaydır. Bu, siz ve üzerinde çalıştığınız destek personeli için ek yığınlar sağlar.

Destek deneyimini kolaylaştırmak için destek merkezini kullanın. Şunları yapmanızı sağlar:

- Configuration Manager istemci günlük dosyalarını içeren bir sorun giderme paketi (. zip dosyası) oluşturun. Daha sonra destek personeline göndermek için tek bir dosyanız vardır.  

- İstemci günlük dosyalarını, sertifikaları, kayıt defteri ayarlarını, hata ayıklama dökümlerini, istemci ilkelerini Configuration Manager görüntüleyin.  

- Envanterin gerçek zamanlı tanılaması (ContentSpy 'ın yerini alır), ilke (PolicySpy yerini alır) ve istemci önbelleği.  

### <a name="support-center-viewer"></a>Destek Merkezi Görüntüleyicisi

Destek Merkezi, personeli destek merkezi 'ni kullanarak oluşturduğunuz dosya paketini açmak için kullanımı destekleyen bir araç olan Destek Merkezi Görüntüleyicisi 'ni içerir. Destek Merkezi 'nin veri toplayıcısı, tanılama günlüklerini yerel veya uzak Configuration Manager istemcisinden toplar ve paketler. Veri toplayıcı paketleri 'ni görüntülemek için görüntüleyici uygulamasını kullanın.

### <a name="support-center-log-file-viewer"></a>Destek Merkezi günlük dosyası Görüntüleyici

Destek Merkezi, modern bir günlük Görüntüleyici içerir. Bu araç CMTrace 'in yerini alır ve sekmeler ve yerleştirilebilir Windows desteğiyle özelleştirilebilir bir arabirim sağlar. Bu, hızlı bir sunu katmanına sahiptir ve büyük günlük dosyalarını Saniyeler içinde yükleyebilir.

### <a name="support-center-onetrace-preview"></a>Destek Merkezi OneTrace (Önizleme)

<!--3555962-->
Sürüm 1906 ' den başlayarak **Onetrace** , Destek Merkezi 'nin bulunduğu yeni bir günlük görüntüleyicisine sahiptir. Geliştirme ile CMTrace 'e benzer şekilde çalışır. Daha fazla bilgi için bkz. [Destek Merkezi OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>PowerShell cmdlet'leri

Destek Merkezi, [PowerShell cmdlet 'lerini](https://docs.microsoft.com/powershell/sccm/overview?view=sccm-ps)de içerir. Bu cmdlet 'leri, başka bir Configuration Manager istemcisine uzak bağlantı oluşturmak, veri toplama seçeneklerini yapılandırmak ve veri toplamayı başlatmak için kullanın.


## <a name="prerequisites"></a>Ön koşullar

Aşağıdaki bileşenleri, Destek Merkezi 'ni yüklediğiniz sunucu veya istemci bilgisayara yükleyebilirsiniz:

- Configuration Manager tarafından desteklenen bir işletim sistemi sürümü. Daha fazla bilgi için bkz. [istemciler Için desteklenen işletim sistemi sürümleri](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). Destek Merkezi, mobil cihazları desteklemez.  

- Destek merkezini ve bileşenlerini çalıştırdığınız bilgisayarda .NET Framework 4.5.2 gereklidir.  


## <a name="install"></a>Yükleme

Site sunucusunda aşağıdaki yolda bulunan destek merkezi yükleyicisini bulun: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Yükledikten sonra, **Microsoft System Center** grubundaki Başlat menüsünde aşağıdaki öğeleri bulun:  

- Destek Merkezi (ConfigMgrSupportCenter. exe)  
- Destek Merkezi günlük dosyası Görüntüleyicisi (CMLogViewer. exe)  
- Destek Merkezi Görüntüleyicisi (ConfigMgrSupportCenterViewer. exe)  


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>Daha eski bir sürüm zaten yüklüyse en son sürümü yükleyemezsiniz

<!--SCCMDocs-pr issue #3090-->
*1810 ve 1902 sürümleri için geçerlidir*

Zaten Destek Merkezi 'nin daha eski bir sürümü yüklüyse, yeni yükleyici başarısız olur. Bu sorun, dosyaların orijinal sürüm ile en son sürümü arasında nasıl sürümlendirileledir. Bu sorunu geçici olarak çözmek için, önce destek merkezi 'nin eski sürümünü kaldırın. Ardından en son sürümü yükler.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Uzak bağlantılar, Kullanıcı adının bir parçası olarak bilgisayar adı veya etki alanı içermelidir

Destek Merkezi 'nden bir uzak istemciye bağlanırsanız, bağlantıyı kurarken Kullanıcı hesabı için makine adını veya etki alanı adını sağlamanız gerekir. Bir toplu bilgisayar adı veya etki alanı adı (gibi `.\administrator` ) kullanırsanız, bağlantı başarılı olur ancak destek merkezi istemciden veri toplamaz.

Bu sorundan kaçınmak için, uzak bir istemciye bağlanmak üzere aşağıdaki Kullanıcı adı biçimlerini kullanın:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Uzak istemcilere betikleştirilmiş sunucu ileti bloğu bağlantıları kaldırma gerekebilir

[New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) PowerShell cmdlet 'ini kullanarak uzak istemcilere bağlanırken, destek merkezi her bir uzak istemciye bir sunucu ileti bloğu (SMB) bağlantısı oluşturur. Veri toplamayı tamamladıktan sonra bu bağlantıları korur. Windows için en fazla uzak bağlantı sayısını aşmamak için, `net use` Şu anda etkin olan uzak bağlantı kümesini görmek için komutunu kullanın. Ardından, aşağıdaki komutu kullanarak gereksiz tüm bağlantıları devre dışı bırakın:`net use <connection_name> /d`
`<connection_name>`Uzak bağlantının adıdır.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>Uygulama dağıtımı değerlendirme çevrimi isteği uzak makinelere doğru şekilde gönderilmedi

<!--2849356-->
*Sürüm 1810 için geçerlidir*

Destek Merkezi 'nde, **içerik** sekmesinde **tetikleyici çağırma** eyleminden **uygulama dağıtımı değerlendirmesi** ' ni seçerseniz, bu eylem dağıtılan uygulamaları değerlendiren bir görevi başlatır. Yerel bir istemciye bağlıysanız, hem makine hem de Kullanıcı uygulama dağıtımlarını değerlendirir. Ancak, uzak bir istemciye bağlıysanız yalnızca makine uygulama dağıtımlarını değerlendirir.


## <a name="next-steps"></a>Sonraki adımlar

[Destek Merkezi hızlı başlangıç](support-center-quickstart.md)
