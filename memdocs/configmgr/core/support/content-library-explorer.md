---
title: Kitaplık Tarayıcı İçeriği
titleSuffix: Configuration Manager
description: Configuration Manager dağıtım noktasındaki içerik kitaplığını görüntülemek ve sorunlarını gidermek için Içerik kitaplığı gezginini kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aa92fb143815faf693f6c2629c3f6436546c5080
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078541"
---
# <a name="content-library-explorer"></a>Kitaplık Tarayıcı İçeriği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İçerik kitaplığı Gezgini [Configuration Manager araçlarından](tools.md)biridir. Aşağıdaki etkinlikler için aracı kullanın:  

- Belirli bir dağıtım noktasındaki içerik kitaplığını keşfet  

- İçerik kitaplığı sorunlarını giderme  

- Paket, içerik, klasör ve dosyaları içerik kitaplığından kopyalayın  

- Paketleri dağıtım noktasına yeniden Dağıt  

- Uzak dağıtım noktalarında paketleri doğrulama  



## <a name="requirements"></a>Gereksinimler

- Aracını yönetici erişimi olan bir hesap kullanarak çalıştırın:  

    - Hedef dağıtım noktası  

    - Site sunucusundaki WMI sağlayıcısı  

    - Configuration Manager sağlayıcı  

- Bu araçtaki tüm bilgileri görüntülemek için yalnızca **tam yönetici** ve **salt okunurdur analist** rollerinin hakları yeterlidir.  

    - **Uygulama Yöneticisi**gibi diğer roller kısmi bilgileri görüntüleyebilir. Daha fazla bilgi için bkz. [devre dışı paketler](#bkmk_disabled-packages).  

    - **Salt-okunurdur analist** , bu araçtan paketleri yeniden dağıtamaz.  

- Aracı, bağlanaldığı sürece herhangi bir bilgisayardan çalıştırın:  

    - Hedef dağıtım noktası  

    - Birincil site sunucusu  

    - Configuration Manager sağlayıcı  

- Dağıtım noktası site sunucusuyla birlikte bulunuyorsa, hala site sunucusuna yönetici erişiminin olması gerekir.  



## <a name="usage"></a>Kullanım 

**Contentlibraryexplorer. exe**' yi başlattığınızda, hedef dağıtım noktasının tam etki alanı adını (FQDN) girin. Daha sonra dağıtım noktasına bağlanır. Dağıtım noktası bir ikincil sitenin parçasıysa, birincil site sunucusunun FQDN 'sini ve birincil site kodunu sorar.

Sol bölmede, bu dağıtım noktasına dağıtılan paketleri görüntüleyin. Paketleri genişletin ve klasör yapısını keşfedebilirsiniz. Bu yapı, paketi oluşturduğunuz klasör yapısıyla eşleşir.

Bir klasör seçtiğinizde, klasör içindeki tüm dosyalar sağ bölmede görüntülenir. Bu görünüm aşağıdaki bilgileri içerir: 
- Dosya adı
- Dosya boyutu
- Bulunduğu sürücü
- Sürücüdeki aynı dosyayı kullanan diğer paketler
- Dağıtım noktasında dosyanın son değiştirildiği zaman

Araç ayrıca Configuration Manager sağlayıcısına da bağlanır. Bu bağlantı, dağıtım noktasına hangi paketlerin dağıtıldığını ve gerçekten dağıtım noktasının içerik kitaplığında olup olmadıklarını belirlemektir. Örneğin, dağıtım bekleyen bir paket, içerik kitaplığında henüz bulunmayabilir. Bu tür bir paket, araçta "beklıyor" olarak görünür ve bu paket için hiçbir eylem etkinleştirilmez.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a>Devre dışı paketler

Bazı paketler dağıtım noktasında bulunuyor ancak Configuration Manager konsolunda görünmüyor. Bu paketler bir yıldız işareti (\*) ile işaretlenir. Bu paketlerde hiçbir eylem gerçekleştirilemeyebilir. Diğer paketler da bir yıldız işaretiyle işaretlenebilir ve eylemleri devre dışı bırakabilir. 

Devre dışı bırakılan paketlerin başlıca üç nedeni vardır:  

- Paket Configuration Manager istemci yükseltirsiniz. Bu paket "CCMSetup. exe" içerir.  

- Kullanıcı hesabınız, büyük olasılıkla rol tabanlı yönetim nedeniyle pakete erişemez. Örneğin, **uygulama yazarı** rolü konsolundaki sürücü paketlerini göremez, bu nedenle dağıtım noktasındaki tüm sürücü paketleri devre dışı olarak işaretlenir.  

- Paket, dağıtım noktasında yalnız bırakılmış.  


### <a name="validate-packages"></a>Paketleri doğrula

Araç çubuğunda **paket** > **doğrulaması** ' nı kullanarak paketleri doğrulayın. Önce sol bölmedeki bir paket düğümünü seçin bir içerik veya klasör seçmeyin. Araç, bu eylem için dağıtım noktasındaki WMI sağlayıcısına bağlanır. Araç başlatıldığında, bir veya daha fazla içerik eksik olan paketler geçersiz olarak işaretlenir. Paketin doğrulanması, içeriğin eksik olduğunu gösterir. Tüm içerik mevcutsa, ancak veriler bozuksa, doğrulama bozulmayı algılar.


### <a name="redistribute-packages"></a>Paketleri yeniden Dağıt

Araç çubuğundaki **paket** > yeniden**dağıtma** kullanılarak paketleri yeniden dağıtın. Önce sol bölmedeki bir paket düğümünü seçin. Bu eylem, paketleri yeniden dağıtmak için izinler gerektirir.


### <a name="other-actions"></a>Diğer eylemler

Paket, içerik, klasör ve dosyaları içerik kitaplığından belirtilen bir klasöre kopyalamak için**kopyayı** **Düzenle** > ' yi kullanın. İçerik kitaplığının kendisini kopyalayamazsınız. Birden fazla dosya seçin, ancak birden çok klasör seçemezsiniz.

**Düzenleme** > **bul paketini**kullanarak paketleri arayın. Bu eylem, sorgunuzu paket adı ve paket KIMLIĞI içinde arar.



## <a name="limitations"></a>Sınırlamalar

- Araç, içerik kitaplığını hiçbir şekilde doğrudan işleyebilir. İçerik kitaplığındaki değişiklikler düzgün çalışmayabilir.  

- Araç paketleri yeniden dağıtabilir, ancak yalnızca hedef dağıtım noktasına.  

- Dağıtım noktasını site sunucusuyla birlikte bulundurdığınızda, paket verilerini doğrulayamazsınız. Bunun yerine Configuration Manager konsolunu kullanın. Araç yine de tüm içeriğin mevcut olduğundan emin olmak için paketi inceler.  

- Bu araçla içerik silemezsiniz.



## <a name="see-also"></a>Ayrıca bkz.

- [İçerik yönetimi için temel kavramlar](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [İçerik kitaplığı](../plan-design/hierarchy/the-content-library.md)
