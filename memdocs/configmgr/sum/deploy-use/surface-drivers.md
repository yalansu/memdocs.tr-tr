---
title: Surface sürücü güncelleştirmelerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager Surface cihazlarına dağıtım için yüzey sürücü güncelleştirmelerini eşitler.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: 6428b6e1992af6dbb1f6d49b9ef1eac3010dd833
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614986"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Configuration Manager ile yüzey sürücülerini yönetme

*Uygulama hedefi: System Center Configuration Manager (Güncel Dalı)*

System Center Configuration Manager Surface cihazları için sürücüleri eşitlemenize ve bunları bir yazılım güncelleştirmesi gibi dağıtmanıza olanak tanır. Bu işlevsellik, Surface cihazlarınızın kullanılabilir en son sürücüleri çalıştırdığından emin olmanızı sağlar. Bu eşitleme ilk olarak sürüm 1706 ' de yayın öncesi özelliği olarak sunulmuştur ve 1710 ' de bir özellik haline geldi. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Yüzey sürücülerini eşitleme önkoşulları

- İnternet 'e bağlı bir en üst düzey yazılım güncelleştirme noktası.
- Tüm yazılım güncelleştirme noktaları, toplu güncelleştirme KB4025339 veya üzeri yüklü Windows Server 2016 ' i çalıştırmalıdır.
- Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Kullanmadan önce bu özelliği etkinleştirin. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Surface sürücüleri için eşitlemeyi etkinleştir

Surface sürücülerinin eşitlenmesini etkinleştirmek için aşağıdaki adımları uygulayın:

1. Yapılandırma Yöneticisi konsolunu en üst düzey site sunucusuna bağlayın.
1. **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin ve en üst düzey sitenize tıklayın.
1. Şeritte, **Ayarlar**  >  **site bileşenlerini Yapılandır**  >  **yazılım güncelleştirme noktası**' nı seçin.
1. **Sınıflandırmalar** sekmesine tıklayın, ardından **Microsoft Surface sürücülerini ve bellenim güncelleştirmelerini dahil et** onay kutusuna tıklayın ve **Uygula**' ya tıklayın.

     ![Yazılım güncelleştirme noktası özelliklerinden yüzey sürücülerini etkinleştir](media/enable-surface-driver-sync.png)

1. Yazılım güncelleştirme noktası bileşen özellikleri ' nde, **Ürünler** sekmesine tıklayın. Daha fazla bilgi için bkz. [Surface Drivers](#bkmk_prod) ve [Surface modeller](#bkmk_models) bölümlerine yönelik ürünler.
1. Surface sürücülerini desteklemek istediğiniz her Windows 10 sürümü için ürünleri seçin. Sürücüler için her bir ürünün iki farklı sürümü olduğunu fark edeceksiniz:

   - Windows 10 *Sürüm* **güncelleştirmesi ve üzeri bakım sürücüleri**
   - Windows 10 *Sürüm* **güncelleştirmesi ve sonraki sürümler & hizmet sürücülerini yükseltme**.

     ![Windows 10 sürümleri sürücü ürün listesi](media/surface-driver-products-sup.png)

1. Ürünleri seçmeyi tamamladığınızda **Tamam**' a tıklayın.
1. Surface sürücüleri Configuration Manager ' ye getirmek için [yazılım güncelleştirme noktanızı eşitler](../get-started/synchronize-software-updates.md) .
1. Yüzey sürücüleri eşitlendikten sonra, diğer güncelleştirmeleri dağıtırken aynı şekilde dağıtın.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a>Surface sürücüleri için ürünler

Çoğu sürücü aşağıdaki ürün gruplarına aittir:

- Windows 10 ve üzeri sürüm sürücüleri
- Windows 10 ve sonrası yükseltme & bakım sürücüleri
- Windows 10 yıldönümü güncelleştirmesi ve üzeri bakım sürücüleri
- Windows 10 yıldönümü güncelleştirmesi ve sonraki sürümler & bakım sürücüleri
- Windows 10 Creators Update ve üzeri bakım sürücüleri
- Windows 10 Creators Update ve üzeri Upgrade & bakım sürücüleri
- Windows 10 Fall Creators Update ve üzeri bakım sürücüleri
- Windows 10 Fall Creators Update ve üzeri Upgrade & hizmet sürücüleri
- Windows 10 S ve üzeri bakım sürücüleri
- Test için Windows 10 S sürüm 1709 ve üzeri bakım sürücüleri
- Windows 10 S sürüm 1709 ve sonraki sürümler & test için bakım sürücülerini yükseltme
- Windows 10 S sürüm 1803 ve üzeri bakım sürücüleri
- Windows 10 S sürüm 1803 ve sonraki sürümler & hizmet sürücülerini yükseltme
- Windows 10 S sürüm 1809 ve üzeri, bakım sürücüleri
- Windows 10 S sürüm 1809 ve üzeri, & hizmet sürücülerini yükseltme
- Windows 10 S sürüm 1903 ve üzeri, bakım sürücüleri
- Windows 10 S sürüm 1903 ve üzeri, & hizmet sürücülerini yükseltme
- Windows 10 sürüm 1803 ve üzeri bakım sürücüleri
- Windows 10 sürüm 1803 ve sonraki sürümler & hizmet sürücülerini yükseltme
- Windows 10 sürüm 1809 ve üzeri, bakım sürücüleri
- Windows 10 sürüm 1809 ve üzeri, yükseltme & bakım sürücüleri
- Windows 10 sürüm 1903 ve üzeri, bakım sürücüleri
- Windows 10 sürüm 1903 ve üzeri, yükseltme & bakım sürücüleri

> [!NOTE]
> Birçok yüzey sürücüsü birden çok Windows 10 ürün grubuna aittir. Burada listelenen tüm ürünleri seçmeniz gerekebilir. Güncelleştirme kataloğunuzun doldurulmasına yönelik ürünlerin sayısını azaltmaya yardımcı olmak için yalnızca eşitleme için ortamınız için gereken ürünleri seçmenizi öneririz.

## <a name="surface-models"></a><a name="bkmk_models"></a>Yüzey modelleri

Aşağıdaki tablo, Configuration Manager sürücüleri yükleyebilecekleri Windows 10 ' un yüzey modellerini ve sürümlerini içerir. Surface sürücü güncelleştirmeleri, Microsoft Update kataloğunda yayımlandıkları gün Configuration Manager kullanılamaz. Configuration Manager, hangi yüzey sürücülerinin içeri aktarılacağını kendi listesini tutar. Bu liste düzenli aralıklarla yayımlanır ve belirli bir tarihte veya bu tarihten önce yayımlanan sürücüleri içerir. Windows 10 S ürünleri gerektiren cihazlar belirtilmiştir.

**9 haziran 2020 ' de veya daha önce yayınlanan yüzey sürücüleri Configuration Manager ' de kullanılabilir**. 


|Yüzey modeli|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Yes| Yes| Yes |Yes|Yes|
|Surface Pro 4|Yes| Yes| Yes |Yes|Yes|
|Surface Pro 6|YOK| Yes| Yes |Yes|Yes|
|Surface Pro 7|YOK| YOK| YOK |Yes|Yes|
|Surface Pro X|YOK| YOK| YOK |Yes|Yes|
|Surface Book|Yes| Yes| Yes |Yes|Yes|
|Surface Book 2|Yes| Yes| Yes |Yes|Yes|
|Surface Book 3|YOK| YOK| YOK |YOK|Yes|
|Yüzey dizüstü bilgisayar|Evet, "Windows 10 S sürüm 1709 ve üzeri bakım sürücüleri" seçiliyken seçili| Evet, "Windows 10 S sürüm 1803 ve üzeri bakım sürücüleri" seçiliyken seçili|Evet, "Windows 10 S sürüm 1809 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|
|Yüzey dizüstü 2|Yes| Yes |Yes|Yes|Yes|
|Yüzey dizüstü 3|YOK| YOK|YOK|Yes |Yes|
|Yüzey go|YOK| Evet, "Windows 10 S sürüm 1803 ve üzeri bakım sürücüleri" seçiliyken seçili|Evet, "Windows 10 S sürüm 1809 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|
|Yüzey git 2|YOK| Yes| Yes |Yes|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|
|Surface Studio|Yes| Yes| Yes |Yes|Yes|
|Surface Studio 2|YOK| Yes| Yes |Yes|Yes|

## <a name="verify-the-configuration"></a>Yapılandırmayı doğrulama

Yazılım güncelleştirme noktasının doğru şekilde yapılandırıldığını doğrulamak için **WsyncMgr. log** ve **WCM. log**' u kullanın.

1. WsyncMgr. log ' i açın ve aşağıdaki günlük girişini denetleyin:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Aşağıdaki girdilerden biri **WsyncMgr. log**dosyasında günlüğe kaydedildiğinde, yazılım güncelleştirme noktasının özelliklerinde **Microsoft Surface sürücülerini ve bellenim güncelleştirmelerini dahil et** seçeneğini seçtiğinizden emin olun:
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. **WCM. log** ' i açın ve aşağıdaki girişlere benzer öğeleri arayın:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Bu giriş, şu anda yazılım güncelleştirme noktası sunucunuz tarafından eşitlenmiş olan her ürün grubunu ve sınıflandırmayı listeleyen bir XML öğesidir. Seçtiğiniz ürünleri bulamıyorsanız, yazılım güncelleştirme noktasının ürünleri, Çift denetimi kaydedilir.
1. Bir sonraki eşitleme bitene kadar de bekleyebilirsiniz. Daha sonra yüzey sürücüsü ve bellenim güncelleştirmelerinin Configuration Manager konsolundaki yazılım güncelleştirmelerinde listelenip listelenmediğini denetleyin. Örneğin, konsol şu bilgileri görüntüleyebilir: ![ Configuration Manager konsolunda eşitlenmiş yüzey sürücüleri](media/synchronized-surface-drivers.png)

## <a name="frequently-asked-questions-faq"></a>Sık sorulan sorular (SSS)

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Bu makaledeki adımları izledikten sonra yüzey Sürücülerim hala eşitlenmedi. Neden mi?

Microsoft Update yerine yukarı akış Windows Server Update Services (WSUS) sunucusundan eşitlerseniz, yukarı akış WSUS sunucusunun yüzey sürücü güncelleştirmelerini destekleyecek ve eşitleyeceği şekilde yapılandırıldığından emin olun. Tüm aşağı akış sunucuları, yukarı akış WSUS sunucu veritabanında bulunan güncelleştirmelerle sınırlıdır.

### <a name="after-i-follow-the-steps-in-this-article-some-surface-drivers-are-synchronized-but-not-the-expected-drivers-why"></a>Bu makaledeki adımları izledikten sonra bazı yüzey sürücüleri eşitlenir, ancak beklenen sürücüler desteklenmez. Neden mi?

Sürücüleri test etmek ve WSUS ve Configuration Manager ile dağıtım için bunları onaylamak için işleme süresi değişir. Bu nedenle, Surface sürücü güncelleştirmeleri hem el ile yükleme hem de Configuration Manager konsol dağıtımı için aynı günde kullanılabilir değildir.

Ayrıca, WSUS 'de sürücü olarak sınıflandırılan 68.000 'den fazla güncelleştirme vardır. Surface olmayan ilgili sürücülerin Configuration Manager eşitlenmesini engellemek için, Microsoft, sürücü eşitlemesini izin verilenler listesine göre filtreler. Yüzey sürücüleri, bu listeye eklenmeden önce ek testlerin ardından gelmelidir. Yeni izin verilenler listesi yayımlandıktan ve Configuration Manager ' ye eklendikten sonra, yeni sürücüler sonraki eşitlemeden sonra konsola eklenir.

### <a name="is-the-driver-allow-list-published-is-it-downloadable"></a>Sürücü izin verilenler listesi yayımlanmış mi? İndirimidir?

Surface sürücü izin verilenler listesi çevrimiçi olarak yayınlanmıyor. Bu liste, güncelleştirme ve bakım kanalları aracılığıyla Configuration Manager teslim edilir. Configuration Manager ortamınız çevrimiçiyse ve yeni güncelleştirmeleri algılayabiliyorsa, listedeki güncelleştirmeleri otomatik olarak alırsınız.

Configuration Manager ortamınız çevrimdışıysa, bakım güncelleştirmelerini Configuration Manager her içeri aktardığınızda yeni bir izin verilenler listesi içeri aktarılır. Ayrıca, güncelleştirmeler Configuration Manager konsolunda görüntülenmeden önce sürücüleri içeren yeni bir WSUS kataloğunu içeri aktarmanız gerekir. Tek başına bir WSUS ortamı Configuration Manager yazılım güncelleştirme noktasına göre daha fazla sürücü içerdiğinden, çevrimiçi yeteneklere sahip bir Configuration Manager ortamı oluşturmanızı ve bunu yüzey sürücülerini eşitleyecek şekilde yapılandırmanızı öneririz. Bu, çevrimdışı ortama benzeyen daha küçük bir WSUS dışarı aktarımı sağlar.

Başka bir çözüm de Surface sürücü ve bellenim güncelleştirmelerini dağıtmak için [Alternatif Yöntemler](#bkmk_alt) kullanmaktır.

### <a name="i-require-the-latest-firmware-update-and-i-cant-wait-for-it-to-be-approved-for-import-into-configuration-manager-can-i-manually-import-the-driver-into-wsus"></a>En son üretici yazılımı güncelleştirmesine ihtiyacım yok ve bu işlemin Configuration Manager içeri aktarmaya yönelik onaylanmıyorum. Sürücüyü el ile WSUS 'e aktarabilir miyim? 

Hayır. Güncelleştirme WSUS 'e aktarılsa bile, güncelleştirme izin verilenler listesinde listelenmemişse dağıtım için Configuration Manager konsoluna aktarılmaz.

Başka bir çözüm de Surface sürücü ve bellenim güncelleştirmelerini dağıtmak için [Alternatif Yöntemler](#bkmk_alt) kullanmaktır.

### <a name="can-i-manually-add-a-driver-to-the-allow-list"></a>İzin verilenler listesine el ile bir sürücü ekleyebilir miyim? 

Hayır. Liste Configuration Manager veritabanında depolanır. CAB dosyası bir sonraki işlendiği sırada listedeki tüm değişikliklerin üzerine yazılır.


### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a><a name="bkmk_alt"></a>Surface sürücü ve üretici yazılımı güncelleştirmelerini hangi alternatif yöntemlerle dağıtmalıyım?

Farklı kanallar aracılığıyla yüzey sürücüsü ve bellenim güncelleştirmelerinin nasıl dağıtılacağı hakkında bilgi için bkz. [Surface sürücü ve bellenim güncelleştirmelerini yönetme](https://docs.microsoft.com/surface/manage-surface-pro-3-firmware-updates).

. Msi veya. exe dosyasını indirmek ve sonra geleneksel yazılım dağıtım kanalları aracılığıyla dağıtmak istiyorsanız, bkz. [Surface üretici yazılımının Configuration Manager Ile güncelleştirilmesini koruma](https://blogs.technet.microsoft.com/thejoncallahan/2016/06/20/keeping-surface-firmware-updated-with-configuration-manager/).

## <a name="next-steps"></a>Sonraki adımlar

Yüzey sürücüleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Yüzey ve System Center Configuration Manager ilgili konular](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Yüzey güncelleştirme geçmişi](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Surface cihazları için en son bellenim ve sürücüleri indirin](https://docs.microsoft.com/surface/deploy-the-latest-firmware-and-drivers-for-surface-devices)
