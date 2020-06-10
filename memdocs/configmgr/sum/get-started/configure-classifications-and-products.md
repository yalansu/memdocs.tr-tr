---
title: Sınıflandırmaları ve ürünleri yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager konsolunda eşitlenmek üzere yazılım güncelleştirme sınıflandırmalarını ve ürünlerini yapılandırmak için aşağıdaki adımları izleyin.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 4f13ff305ba5fc2b5c5080bafb6fed2412ff8366
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614075"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Sınıflandırmaları ve eşitlenmek üzere ürünleri yapılandırma  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yazılım güncelleştirme meta verileri, yazılım güncelleştirme noktası bileşen özelliklerinde belirttiğiniz ayarlara göre Configuration Manager eşitleme işlemi sırasında alınır. Yazılım güncelleştirmelerini ilk kez eşitledikten veya yeni ürün ve sınıflandırmalar yayınlandıktan sonra, yeni öğeleri seçmek için özelliklere gitmeniz gerekir. Eşitlenecek sınıflandırmaları ve ürünleri yapılandırmak için aşağıdaki prosedürü kullanın.  

> [!NOTE]  
> Bu bölümdeki prosedürü sadece üst düzey sitede kullanın.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Eşitlenecek sınıflandırmaları ve ürünleri yapılandırmak için  

1. **Configuration Manager** konsolunda, **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin.

2. Merkezi yönetim sitesini veya tek başına birincil siteyi seçin.  

3. **Giriş** sekmesindeki **Ayarlar** grubunda **Site Bileşenlerini Yapılandır**’a, ardından da **Yazılım Güncelleştirme Noktası**’na tıklayın.

4. **Sınıflandırma** sekmesinde, yazılım güncelleştirmelerini eşitlemek istediğiniz yazılım güncelleştirme sınıflandırmalarını belirtin.  

    Her yazılım güncelleştirmesi, farklı güncelleştirme türlerinin düzenlenmesine yardımcı olan bir güncelleştirme sınıflandırmasıyla tanımlanır. Eşitleme işlemi sırasında belirtilen sınıflandırmaların yazılım güncelleştirmeleri üst verileri eşitlenir. Configuration Manager, yazılım güncelleştirmelerini aşağıdaki güncelleştirme sınıflandırmalarıyla eşitlemeye olanak sağlar:  

     - **Kritik güncelleştirmeler**: kritik, güvenlikle ilgili olmayan bir hatayı gideren belirli bir sorun için yaygın olarak yayımlanmış bir düzeltme belirtir.  
     - **Tanım güncelleştirmeleri**: bir ürünün tanım veritabanına eklemeler içeren, yaygın olarak yayınlanan ve sık görülen bir yazılım güncelleştirmesini belirtir.  
     - **Özellik paketleri**: ilk olarak bir ürün sürümünün dışında dağıtılan ve tipik olarak bir sonraki tam ürün sürümüne dahil edilen yeni ürün işlevlerini belirtir.  
     - **Güvenlik güncelleştirmeleri**: ürüne özgü, güvenlikle ilgili bir güvenlik açığı için yaygın olarak yayımlanmış bir düzeltme belirtir.  
     - **Hizmet paketleri**: bir ürüne uygulanan tüm düzeltmeler, güvenlik güncelleştirmeleri, kritik güncelleştirmeler ve güncelleştirmelerin test edilmiş, toplu bir kümesini belirtir. Ayrıca, hizmet paketleri, ürünün yayımlanmasından bu yana dahili olarak bulunan sorunlara yönelik ek düzeltmeler de içerebilir.  
     - **Araçlar**: bir veya daha fazla görevi tamamlamaya yardımcı olan bir yardımcı programı veya özelliği belirtir.  
     - **Güncelleştirme paketleri**: kolay dağıtım için bir test edilmiş, toplu düzeltmeler, güvenlik güncelleştirmeleri, kritik güncelleştirmeler ve birlikte paketlenmiş güncelleştirmeleri belirtir. Güncelleştirme paketi genellikle güvenlik veya ürün bileşeni gibi belirli bir alana yöneliktir.  
     - **Güncelleştirmeler**: belirli bir sorun için yaygın olarak yayınlanan bir sorunu belirtir. Güncelleştirme, kritik olmayan ve güvenlikle ilgili olmayan bir hataya yöneliktir.  
     - **Yükseltme**: Windows 10 özellikleri ve işlevselliği için bir yükseltme belirtir. **Yükseltme** sınıflandırmasını almak için yazılım güncelleştirme noktalarınız ve siteleriniz, [3095113 düzeltmesini](https://support.microsoft.com/kb/3095113) içeren en az WSUS 6,2 çalıştırmalıdır. Bu güncelleştirmeyi ve **yükseltmeler**için diğer güncelleştirmeleri yükleme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri için Önkoşullar](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).
    
    > [!NOTE]
    > Microsoft Surface sürücülerini eşleştirmek için **Microsoft Surface sürücülerini ve bellenim güncelleştirmelerini dahil et** onay kutusunu seçebilirsiniz.<!--1098490--> Surface sürücülerini başarıyla eşitlemeniz için tüm yazılım güncelleştirme noktalarının Windows Server 2016 veya üstünü çalıştırması gerekir. Windows Server 2012 çalıştıran bir bilgisayarda bir yazılım güncelleştirme noktasını etkinleştirirseniz yüzey sürücülerini etkinleştirdikten sonra, sürücü güncelleştirmelerinin tarama sonuçları doğru olmaz. Bu, Configuration Manager konsolunda ve Configuration Manager raporlarında, yanlış uyumluluk verilerinin görüntülenmesine neden olur. Daha fazla bilgi için bkz. [Configuration Manager yüzey sürücülerini yönetme](../deploy-use/surface-drivers.md).

5. **Ürünler** sekmesinde, yazılım güncelleştirmelerini eşitlemek istediğiniz ürünleri belirtin ve ardından **Kapat**’a tıklayın.  

    - Configuration Manager, yazılım güncelleştirme noktasını ilk yüklediğinizde aralarından seçim yapabileceğiniz ürünlerin ve ürün ailelerinin listesini depolar. Configuration Manager yayımlandıktan sonra yayınlanan ürünler ve ürün aileleri, kullanılabilir ürünlerin ve ürün ailelerinin listesini güncelleştiren yazılım güncelleştirmeleri eşitlemesini tamamlayana kadar seçemeyebilir.  

    - Her yazılım güncelleştirmesinin meta verileri, güncelleştirmenin mevcut olduğu ürünleri tanımlar. Bir ürün, Windows Server 2012 gibi bir işletim sistemi veya uygulamanın belirli bir sürümüdür. Bir ürün ailesi, tek tek ürünlerin türetildiği temel işletim sistemi veya uygulamadır. Ürün ailesine örnek Windows’dur; Windows Server 2012 bunun bir üyesidir. Bir ürün ailesini veya bir ürün ailesi içinde tek tek ürünleri belirtebilirsiniz. Ne kadar çok ürün seçerseniz, yazılım güncelleştirmelerini eşitlemeniz o kadar uzun sürer.  

    - Yazılım güncelleştirmeleri birden fazla ürün için geçerli olduğunda ve ürünlerden en az biri eşitleme için seçildiyse, bazı ürünler seçilmese bile tüm ürünler Configuration Manager konsolunda görünür. Örneğin, seçtiğiniz tek işletim sistemi Windows Server 2012 ise ve Windows 8 ve Windows Server 2012 için bir yazılım güncelleştirmesi geçerliyse, her iki ürün de Configuration Manager konsolunda görüntülenir.  

    > [!NOTE]  
    > **Windows 10, sürüm 1903 ve üzeri,** **Windows 10** ürününün önceki sürümleri gibi bir parçası olmak yerine kendi ürünü olarak Microsoft Update eklenmiştir. Bu değişiklik, istemcilerinizin bu güncelleştirmeleri görmesini sağlamak için birkaç el ile adım uygulamanızı sağlar. Configuration Manager sürüm 1906 ' de yeni ürün için gerçekleştirmeniz gereken el ile adım sayısını azaltmaya yardımcı oluyoruz. <!--4682946-->
    >
    > Configuration Manager sürüm 1906 ' e güncelleştirdiğinizde ve eşitleme için **Windows 10** ürününün seçili olması halinde, aşağıdaki eylemler otomatik olarak gerçekleşir:
    > - Eşitleme için **Windows 10, sürüm 1903 ve sonraki** bir ürün eklenmiştir.
    > - **Windows 10** ürününü Içeren [Otomatik dağıtım kuralları](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) **, Windows 10, sürüm 1903 ve üstünü**içerecek şekilde güncelleştirilecektir.
    > - [Bakım planları](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) , **Windows 10, sürüm 1903 ve sonraki** bir ürünü içerecek şekilde güncelleştirilir.


## <a name="configuring-products-for-versions-of-windows-10"></a>Windows 10 sürümleri için ürünleri yapılandırma

### <a name="windows-10-version-1909"></a>Windows 10, sürüm 1909

Windows 10, sürüm 1909, Windows 10, sürüm 1903 ile ortak bir çekirdek işletim sistemini paylaşır. Bu sürümlerin her ikisine de aynı toplu güncelleştirmelerle bakım yapılır. Windows 10, sürüm 1909 hakkında daha fazla bilgi için [Windows 10, sürüm 1909 teslim seçenekleri](https://aka.ms/1909mechanics) blog gönderisine bakın.

Hem Windows 10 sürüm 1909 ve Windows 10 ' un, sürüm 1903 istemcilerinin Configuration Manager güncelleştirmeleri yüklemesini sağlamak için:

- Windows 10 ' un 1909 ve 1903 sürümleri için güncelleştirmeleri onaylayın.
  - Güncelleştirmelerin her bir işletim sistemi sürümü için farklı başlıkları ve Uygulanabilirlik kuralları vardır.
  - İşletim sisteminin sürümü ve mimarisi başına her güncelleştirme onaylanmak, Yöneticiler için normal onay işlemini korur.
- Toplu güncelleştirme yükleme dosyaları, Windows 10 ' un 1909 ve 1903 sürümleri için aynıdır.
  - Configuration Manager güncelleştirme kaynak dosyalarını yalnızca bir kez indirir.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Windows 10, sürüm 1909 için özellik güncelleştirmeleri

Windows 10, sürüm 1909 için özellik güncelleştirmelerini onayladığınızda, göreceğiniz birkaç farklı seçenek vardır:

- Windows 10, sürüm 1903 istemcilerine 12 Kasım 2019 ' de yayınlanan bir [etkinleştirme paketi](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)sunuluyor.
  - Etkinleştirme paketi, Windows 10, sürüm 1909 özelliklerini etkinleştiren ve cihazı yeniden başlatan küçük ve hızlı bir dosya yüklemeye yönelik bir dosyadır.
  - Etkinleştirme paketinin önkoşulları şunlardır:
    - 8 Ekim 2019 ' de yayınlanan en düşük toplu [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389)güncelleştirmesi.
    - 24 Eylül 2019 ' de yayınlanan [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390)'in en düşük bakım yığını güncelleştirmesi.
  - Bu güncelleştirme, diğer tüm özellik güncelleştirmeleri gibi, ' den içeri aktarma için kullanılamaz `https:\\catalog.update.microsoft.com` .
  - Eşitleme için **Windows 10, sürüm 1903 ve sonraki** ürün ve **yükseltmeler** SıNıFLANDıRMASıNA sahipseniz güncelleştirme WSUS ile otomatik olarak eşitlenir.
  - Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Windows 10 Bakımı**' nı genişletin ve **tüm Windows 10 güncelleştirmeleri** düğümünü seçin. "Etkinleştirme" veya "4517245" terimlerini arayın.

    > [!TIP]
    > Bunlar özellik güncelleştirmeleri olduğundan, **tüm yazılım güncelleştirmeleri** düğümünde değiller.

- Windows 10, sürüm 1809 ve önceki istemciler tek bir doğrudan Özellik güncelleştirmesiyle yükseltilir.
  - Bu, Windows 10 ' da yapmış olduğunuz özellik güncelleştirmelerine yönelik diğer tüm önceki yüklemelerin olduğu gibidir.

> [!NOTE]
> Hem etkinleştirme paketi hem de Windows 10 için geleneksel Özellik Güncelleştirmesi, sürüm 1909, bu uygulamayı yüklemek için kullanılan yolun ne olursa olsun, raporlama 'da "yüklü" olarak gösterilir.

### <a name="windows-10-version-1903-and-later"></a>Windows 10, sürüm 1903 ve üzeri

**Windows 10, sürüm 1903 ve üzeri,** **Windows 10** ürününün önceki sürümleri gibi bir parçası olmak yerine kendi ürünü olarak Microsoft Update eklenmiştir. Bu değişiklik, istemcilerinizin bu güncelleştirmeleri görmesini sağlamak için birkaç el ile adım uygulamanızı sağlar. Configuration Manager sürüm 1906 ' de yeni ürün için gerçekleştirmeniz gereken el ile adım sayısını azaltmaya yardımcı oluyoruz. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, sürüm 1903 ve üzeri Configuration Manager sürüm 1906
Configuration Manager sürüm 1906 ' e güncelleştirdiğinizde ve eşitleme için **Windows 10** ürününün seçili olması halinde, aşağıdaki eylemler otomatik olarak gerçekleşir:
- Eşitleme için **Windows 10, sürüm 1903 ve sonraki** bir ürün eklenmiştir.
- **Windows 10** ürününü Içeren [Otomatik dağıtım kuralları](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) **, Windows 10, sürüm 1903 ve üstünü**içerecek şekilde güncelleştirilecektir.
- [Bakım planları](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) , **Windows 10, sürüm 1903 ve sonraki** bir ürünü içerecek şekilde güncelleştirilir.

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, sürüm 1903 ve üzeri Configuration Manager sürüm 1902
Windows 10, sürüm 1903 istemcilerinde Configuration Manager 1902 kullanıyorsanız şunları yapmanız gerekir:
- Eşitleme için **Windows 10, sürüm 1903 ve sonraki** bir ürünü seçin.
- Windows 10, sürüm 1903 istemcileri için tüm [Otomatik dağıtım kurallarını](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) güncelleştirin.
- Windows 10, sürüm 1903 istemcileri için [bakım planlarını](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) güncelleştirme.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a>Windows Insider programı
<!--3556023-->
2019 Eylül 'den başlayarak, Windows Insider Preview derlemelerini çalıştıran cihazlara Configuration Manager ile hizmet verebilir ve güncelleştirebilirsiniz. Bu değişiklik, bu cihazları normal işlemlerinizi değiştirmeden veya Iş için Windows Update etkinleştirmeden yönetebileceğiniz anlamına gelir. Windows Insider Preview derlemeleri için özellik güncelleştirmelerini ve toplu güncelleştirmeleri, diğer Windows 10 güncelleştirme veya yükseltme gibi Configuration Manager içine indirebilirsiniz. Daha fazla bilgi için bkz. [Windows 10 özellik GÜNCELLEŞTIRMELERINI WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) blog gönderisine yayımlama.

Configuration Manager 'de Windows Insider desteği hakkında daha fazla bilgi için bkz. [Windows 10 Için destek](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Önkoşullar

- Configuration Manager sürüm 1906 veya üzeri, [yazılım güncelleştirme yönetimi](../plan-design/plan-for-software-updates.md)için yapılandırıldı.
- [Windows Insider Preview derlemesi](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started)çalıştıran Windows 10 cihazları.
- Windows Insider cihazlarını içeren bir koleksiyon.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Windows Insider yükseltmelerini ve güncelleştirmelerini etkinleştir

Windows Insider yükseltmeleri ve güncelleştirmeleri için ürünleri ve sınıflandırmaları etkinleştirmeniz gerekir. Windows Insider için özellik güncelleştirmeleri, toplu güncelleştirmeler ve diğer güncelleştirmeler **Windows Insider ön sürüm** ürün kategorisidir.

1. **Configuration Manager** konsolunda, **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. Merkezi yönetim sitesini veya tek başına birincil siteyi seçin.  
3. **Giriş** sekmesindeki **Ayarlar** grubunda **Site Bileşenlerini Yapılandır**’a, ardından da **Yazılım Güncelleştirme Noktası**’na tıklayın.
4. **Ürünler** sekmesinde, aşağıdaki ürünlerin eşitleme için seçildiğinden emin olun:
    - Windows Insider ön sürümü
    - Windows 10, sürüm 1903 ve üzeri
5. **Sınıflandırmalar** sekmesinde, eşitleme için aşağıdaki sınıflandırmaların seçildiğinden emin olun:
    - Güncelleştirmelerini
    - Güvenlik Güncelleştirmeleri
    - Güncelleştirmeler (isteğe bağlı)
6. **Yazılım güncelleştirme noktası bileşen özelliklerini**kapatmak için **Tamam** ' ı tıklatın.

### <a name="upgrading-windows-insider-devices"></a>Windows Insider cihazlarını yükseltme

Windows Insider 'lar için yükseltmeler eşitlendikten sonra, bunları **yazılım kitaplığı**  >  **Windows 10**' dan  >  **tüm Windows 10 güncelleştirmelerine**hizmet olarak görebilirsiniz.

![Windows 10 bakımı için Windows Insiders özelliği güncelleştirmeleri](media/3556023-windows-insiders-pre-release-feature-update.png)

Windows Insider için özellik güncelleştirmelerini, diğer tüm yükseltmelerle tıpkı hedef koleksiyonunuzda dağıtın. Ancak, bu özellik güncelleştirmelerini dağıttığınızda aşağıdaki öğeleri aklınızda bulundurmanız gerekir:

- Bu yükseltmeler, eşleşen mimari, sürüm ve dil ile tüm Windows 10 istemcileri 1903 veya önceki sürümleri için geçerli olacaktır.
- Lisans koşulları varsa, dağıtımınızın yüklenmek üzere koşulları kabul etmesi gerekir.
- [İstemci ayarlarında iş parçacığı önceliğini](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)kullanmayı göz önünde bulundurun.
- Dinamik güncelleştirme, en son toplu güncelleştirme de dahil olmak üzere kritik güncelleştirmeleri doğrudan Microsoft Update otomatik olarak yüklüyor. Bu davranış, Windows 10 sürüm 1903 için özellik güncelleştirmeleriyle başlatıldı. 
  - [İstemci ayarlarında dinamik güncelleştirmeyi](../../core/clients/deploy/about-client-settings.md#bkmk_du) veya bir [setupconfig. ini dosyası](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)ile açıkça devre dışı bırakabilirsiniz. 
  - Daha fazla bilgi için [Windows 10 dinamik güncelleştirme](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) blog gönderisine bakın.

Yükseltmeleri dağıtma hakkında daha fazla bilgi için bkz. [Windows 'u hizmet olarak yönetme](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Insider cihazlarını güncel tutma

Windows Insider için toplu güncelleştirmeler, Configuration Manager için WSUS ve uzantıya göre sunulacaktır. Bu toplu güncelleştirmeler Windows 10 sürüm 1903 toplu güncelleştirmelerine benzer bir sıklıkta yayınlanacaktır. Windows Insider toplu güncelleştirmeleri, **Windows Insider ön sürümü** ürün kategorisinde ve **güvenlik güncelleştirmeleri** ya da **güncelleştirmeler**olarak sınıflandırılmaktadır. Windows Insider için toplu güncelleştirmeleri, [Otomatik dağıtım kuralları](../deploy-use/automatically-deploy-software-updates.md) veya [aşamalı dağıtımlar](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)gibi normal yazılım güncelleştirme işleminizi kullanarak dağıtabilirsiniz.

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Genişletilmiş güvenlik güncelleştirmeleri ve Configuration Manager

[Genişletilmiş güvenlik güncelleştirmeleri (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) programı, destek sonunun ötesinde belirli eski Microsoft ürünlerini çalıştırması gereken müşteriler için son çare bir seçenektir. Ürünün genişletilmiş destek tarihine kadar olan en fazla üç yıl sonra kritik ve/veya önemli güvenlik güncelleştirmelerini ( [Microsoft Güvenlik Yanıt Merkezi (MSRC)](https://www.microsoft.com/msrc)tarafından tanımlandığı şekilde) içerir.

Destek yaşam döngüsünün ötesinde ürünlerin Configuration Manager kullanımı desteklenmez. Bu, ESU programının kapsamında kapsanan tüm ürünleri içerir. Örneğin, Windows 7. ESU programı altında yayınlanan güvenlik güncelleştirmeleri Windows Server Update Services (WSUS) hizmetine yayımlanacak. Bu güncelleştirmeler Configuration Manager konsolunda görünür. ESU programının kapsamında yer alan ürünler Configuration Manager ile kullanım için artık desteklenirken, [Configuration Manager geçerli dalın en son yayınlanan sürümü](../../core/servers/manage/updates.md#version-details) program altında Yayınlanan Windows güvenlik güncelleştirmelerini dağıtmak ve yüklemek için kullanılabilir. Windows 7 çalıştıran cihazlara Windows 10 dağıtmak için en son yayınlanan sürüm de kullanılabilir.

Windows yazılım güncelleştirme yönetimi veya işletim sistemi dağıtımıyla ilgili olmayan istemci yönetimi özellikleri artık ESU programının kapsamında yer alan işletim sistemlerinde sınanmayacak ve çalışmaya devam edeceğini garanti etmeyiz. İstemci yönetimi desteğini almak için en kısa sürede işletim sistemlerinin güncel bir sürümüne yükseltilmesi veya geçirilmesi önerilir.


## <a name="next-steps"></a>Sonraki adımlar

Yeni ölçütlere göre yazılım güncelleştirmelerini almak için yazılım güncelleştirmeleri eşitlemesini başlatın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini Synchronize](synchronize-software-updates.md).
