---
title: Technical Preview 1603 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1603 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73e3e19df4ce545e4cbb36109da2710e848f1159
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076229"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Configuration Manager için Technical Preview 1603 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1603 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Alternatif olarak, System Center Technical Preview 5 ' i kullandığınızda, bu sürüm Configuration Manager Technical Preview 'ın temel sürümü olarak yüklenir. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).  

 **Bu Technical Preview için bilinen sorunlar:**  

- Bu sürüm, daha önce yayımlanmış özellikler için güncelleştirmeleri içerir ancak yeni özellikler sunmaz. Bu nedenle, daha önce 1602 sürümüne yükselttiyseniz ve 1602 ' de bulunan tüm özellikleri etkinleştirdiyseniz güncelleştirme sihirbazının Özellikler sayfası boş olur.  

- Site sunucunuz Technical Preview 1603 ' e yükselttikten sonra, istemciler ayrıca 1603 sürümüne güncelleştirene kadar herhangi bir uzaktan denetim özelliğini kullanamazlar.  

  **Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a>Yazılım Merkezi geliştirmeleri  

### <a name="new-tiled-view-for-apps"></a>Uygulamalar için yeni döşeli görünüm  
 Son kullanıcılar artık yazılım merkezi 'nin **uygulamalar** sekmesinde bir uygulama listesi veya bir uygulama döşeli görünümü arasından seçim yapabilir.  

### <a name="select-multiple-updates-in-software-center"></a>Yazılım Merkezi 'nde birden çok güncelleştirme seçin  
 Yazılım Merkezi 'nin **güncelleştirmeler** sekmesinde, artık birden çok güncelleştirme seçebilir veya birden çok güncelleştirmeyi aynı anda yüklemeye başlamak Için **Tümünü Güncelleştir** ' i seçebilirsiniz.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a>Uzaktan Denetim geliştirmeleri  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Uzaktan denetim oturumunda paylaşılan Pano erişimini sınırlandırma  
 Artık, uzaktan denetim oturumunda paylaşılan panoya erişimi sınırlandırmak için **kullanıcıyı paylaşılan Pano dosya aktarımı Için iste** yeni uzak Araçlar istemci ayarını etkinleştirebilirsiniz.  

 Etkinleştirildiğinde, uzak bir oturumu paylaşan son kullanıcının, paylaşılan Pano aracılığıyla oturumdan dosyaları yerel makinesine aktarabilmesi için, bu oturumun görüntüleyicisine izin vermesi gerekir.  

 Bu, daha önce son kullanıcı için bir koruma katmanı ekler. Bu, görüntüleyiciye son kullanıcının bilgisayarında tam denetim verildiyse, paylaşılan panoyu kullanarak oturumları, son kullanıcıya tamamen saydam bir şekilde yerel bilgisayarlarına aktarabilir.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a>PXE 'yi destekleyen dağıtım noktalarında RamDisk TFTP blok boyutunu ve pencere boyutunu özelleştirme  
 1603 Technical Preview sürümünde, PXE 'yi destekleyen dağıtım noktaları için RamDisk TFTP blok boyutunu ve pencere boyutunu özelleştirebilirsiniz. Ağınızı özelleştirdiyseniz önyükleme görüntüsünün indirilmesi, blok veya pencere boyutu çok büyük olduğundan zaman aşımı hatası vererek başarısız olabilir. RamDisk TFTP blok boyutu ve pencere boyutu özelleştirmesi, PXE kullanırken belirli ağ gereksinimlerinizi karşılayacak şekilde TFTP trafiğini iyileştirmenize olanak tanır.   
En verimli ayarları belirlemek için, özelleştirilmiş ayarları ortamınızda test etmeniz gerekir.  

-   **TFTP blok boyutu**: Blok boyutu, sunucu tarafından dosyayı indiren istemciye gönderilen veri paketlerinin boyutudur (RFC 2347’de açıklandığı gibi). Daha büyük bir blok boyutu, sunucunun daha az paket göndermesine olanak tanıyarak sunucu ve istemci arasındaki gidiş dönüş gecikmelerini azaltır. Ancak büyük blok boyutları, çoğu PXE istemci uygulaması tarafından desteklenmeyen parçalanmış paketlere yol açar.  

-   **TFTP pencere boyutu**: TFTP, gönderilen her veri bloğu için bir onay (ACK) paketi gerektirir. Sunucu, önceki blok için ACK paketini alıncaya kadar sırada sonraki bloğu göndermez. TFTP pencereleme, bir pencereyi doldurmak için kaç veri bloğu gerektiğinizi tanımlamanıza olanak sağlayan bir Windows Dağıtım Hizmetleri özelliğidir. Sunucu, pencere doldurulana kadar veri bloklarını arka arkaya gönderir ve sonra istemci bir ACK paketi gönderir. Bu pencere boyutunun artırılması, istemci ve sunucu arasındaki gidiş dönüş gecikmelerini azaltır ve bir önyükleme görüntüsünü indirmek için gereken toplam süreyi düşürür.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için bu konunun en üstündeki geri bildirim bilgilerini kullanın:  

-   PXE 'yi destekleyen dağıtım noktasındaki RamDisk TFTP pencere boyutunu özelleştirebiliyorum.  

-   PXE 'yi destekleyen dağıtım noktasındaki RamDisk TFTP blok boyutunu özelleştirebiliyorum.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>RamDisk TFTP pencere boyutunu değiştirmek için  

- RamDisk TFTP pencere boyutunu özelleştirmek için, PXE'yi destekleyen dağıtım noktalarında aşağıdaki kayıt defteri anahtarını ekleyin:  

   **Konum**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Ad: RamDiskTFTPWindowSize  

   **Tür**: REG_DWORD  

   **Değer**: &lt;özelleştirilmiş pencere boyutu\>  

  Varsayılan değer, 1'dir (1 veri bloğu pencereyi doldurur).  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>RamDisk TFTP blok boyutunu değiştirmek için  

- RamDisk TFTP pencere boyutunu özelleştirmek için, PXE'yi destekleyen dağıtım noktalarında aşağıdaki kayıt defteri anahtarını ekleyin:  

   **Konum**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Ad: RamDiskTFTPBlockSize  

   **Tür**: REG_DWORD  

   **Değer**: &lt;özelleştirilmiş blok boyutu\>  

  Varsayılan değer, 4096’dır (4k).  
