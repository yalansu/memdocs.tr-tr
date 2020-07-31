---
title: Surface sürücü güncelleştirmelerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager Surface cihazlarına dağıtım için yüzey sürücü güncelleştirmelerini eşitler.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: f276db618a2e67832ffa5575622e00eea02c7422
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438623"
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

Aşağıdaki tablo, Configuration Manager sürücüleri yükleyebilecekleri Windows 10 ' un yüzey modellerini ve sürümlerini içerir. Surface sürücü güncelleştirmeleri, Microsoft Update kataloğunda yayımlandıkları gün Configuration Manager kullanılamaz. Configuration Manager, hangi yüzey sürücülerinin içeri aktarılacağını kendi listesini tutar. Windows 10 S ürünleri gerektiren cihazlar belirtilmiştir. Microsoft amaçlar, yüzey sürücülerinin ikinci Salı günü, Configuration Manager eşitlemeye uygun hale getirmek için her ay Salı ve daha sonra izin verilenler listesine eklenmesini sağlar. Daha fazla bilgi için bkz. [sık sorulan sorular](#bkmk_faq).

</br>

|Yüzey modeli|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Yes| Yes| Yes |Yes|Yes|
|Surface Pro 4|Yes| Yes| Yes |Yes|Yes|
|Surface Pro 6|Yok| Yes| Yes |Yes|Yes|
|Surface Pro 7|Yok| Yok| Yok |Yes|Yes|
|Surface Pro X|Yok| Yok| Yok |Yes|Yes|
|Surface Book|Yes| Yes| Yes |Yes|Yes|
|Surface Book 2|Yes| Yes| Yes |Yes|Yes|
|Surface Book 3|Yok| Yok| Yok |Yes|Yes|
|Yüzey dizüstü bilgisayar|Evet, "Windows 10 S sürüm 1709 ve üzeri bakım sürücüleri" seçiliyken seçili| Evet, "Windows 10 S sürüm 1803 ve üzeri bakım sürücüleri" seçiliyken seçili|Evet, "Windows 10 S sürüm 1809 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|
|Yüzey dizüstü 2|Yok| Yes |Yes|Yes|Yes|
|Yüzey dizüstü 3|Yok| Yok|Yok|Yes |Yes|
|Yüzey go|Yok| Evet, "Windows 10 S sürüm 1803 ve üzeri bakım sürücüleri" seçiliyken seçili|Evet, "Windows 10 S sürüm 1809 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|
|Yüzey git 2|Yok| Yok| Yes |Yes|Evet, "Windows 10 S sürüm 1903 ve sonraki sürümleri & hizmet sürücülerini yükseltme" seçiliyken|
|Surface Studio|Yes| Yes| Yes |Yes|Yes|
|Surface Studio 2|Yok| Yes| Yes |Yes|Yes|

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

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Sık sorulan sorular (SSS)

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Bu makaledeki adımları izledikten sonra yüzey Sürücülerim hala eşitlenmedi. Neden?

Microsoft Update yerine yukarı akış Windows Server Update Services (WSUS) sunucusundan eşitlerseniz, yukarı akış WSUS sunucusunun yüzey sürücü güncelleştirmelerini destekleyecek ve eşitleyeceği şekilde yapılandırıldığından emin olun. Tüm aşağı akış sunucuları, yukarı akış WSUS sunucu veritabanında bulunan güncelleştirmelerle sınırlıdır.

WSUS 'de sürücü olarak sınıflandırılan 68.000 'den fazla güncelleştirme vardır. Surface olmayan ilgili sürücülerin Configuration Manager eşitlenmesini engellemek için, Microsoft, sürücü eşitlemesini izin verilenler listesine göre filtreler. Yeni izin verilenler listesi yayımlandıktan ve Configuration Manager ' ye eklendikten sonra, yeni sürücüler sonraki eşitlemeden sonra konsola eklenir. Microsoft amaçlar, yüzey sürücülerinin ikinci Salı günü, Configuration Manager eşitlemeye uygun hale getirmek için her ay Salı ve daha sonra izin verilenler listesine eklenmesini sağlar.

Configuration Manager ortamınız çevrimdışıysa, [bakım güncelleştirmelerini](../../core/servers/manage/use-the-service-connection-tool.md) Configuration Manager her içeri aktardığınızda yeni bir izin verilenler listesi içeri aktarılır. Ayrıca, güncelleştirmeler Configuration Manager konsolunda görüntülenmeden önce sürücüleri içeren [Yeni BIR WSUS kataloğunu](../get-started/synchronize-software-updates-disconnected.md) içeri aktarmanız gerekir. Tek başına bir WSUS ortamı Configuration Manager SUP 'den daha fazla sürücü içerdiğinden, çevrimiçi yeteneklere sahip bir Configuration Manager ortamı oluşturmanızı ve bunu yüzey sürücülerini eşitleyecek şekilde yapılandırmanızı öneririz. Bu, çevrimdışı ortama benzeyen daha küçük bir WSUS dışarı aktarımı sağlar.

Configuration Manager ortamınız çevrimiçiyse ve yeni güncelleştirmeleri algılayabiliyorsa, listedeki güncelleştirmeleri otomatik olarak alırsınız. Beklenen sürücüleri görmüyorsanız, lütfen tüm eşitleme hatalarıyla ilgili WCM. log ve WsyncMgr. log ' u gözden geçirin.

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>Configuration Manager ortamım çevrimdışı, Surface sürücülerini el ile WSUS 'a aktarabilir miyim?

Hayır. Güncelleştirme WSUS 'e aktarılsa bile, güncelleştirme izin verilenler listesinde listelenmemişse dağıtım için Configuration Manager konsoluna aktarılmaz. İzin verilenler listesini güncelleştirmek için [hizmet bağlantı aracını](../../core/servers/manage/use-the-service-connection-tool.md) , Configuration Manager hizmet güncelleştirmelerini içeri aktarmak üzere kullanmanız gerekir.

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>Surface sürücü ve üretici yazılımı güncelleştirmelerini hangi alternatif yöntemlerle dağıtmalıyım?

Farklı kanallar aracılığıyla yüzey sürücüsü ve bellenim güncelleştirmelerinin nasıl dağıtılacağı hakkında bilgi için bkz. [Surface sürücü ve bellenim güncelleştirmelerini yönetme](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates). . Msi veya. exe dosyasını indirmek ve sonra geleneksel yazılım dağıtım kanalları aracılığıyla dağıtmak istiyorsanız, bkz. [Surface üretici yazılımının Configuration Manager Ile güncelleştirilmesini koruma](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager).

## <a name="next-steps"></a>Sonraki adımlar

Yüzey sürücüleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Yüzey ve System Center Configuration Manager ilgili konular](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Yüzey güncelleştirme geçmişi](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Surface cihazları için en son bellenim ve sürücüleri indirin](/surface/manage-surface-driver-and-firmware-updates)
