---
title: İçerik Kitaplığı Aktarma Aracı
titleSuffix: Configuration Manager
description: İçeriği bir Configuration Manager dağıtım noktasında bir disk sürücüsünden diğerine aktarmak için Içerik kitaplığı aktarma aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720089"
---
# <a name="content-library-transfer-tool"></a>İçerik Kitaplığı Aktarma Aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Içerik kitaplığı aktarma aracı [Configuration Manager araçlarından](tools.md)biridir. İçeriği bir disk sürücüsünden diğerine aktarır. Araç, dağıtım noktası site sistemlerinde çalışmak üzere tasarlanmıştır. Bir site veya uzak site sistemleriyle birlikte bulunan dağıtım noktalarını destekler.  

Araç, içerik kitaplığını barındıran disk sürücüsü dolduğunda senaryo için yararlı olur. İlk olarak, içerik kitaplığını barındırmak için yeterli alana sahip başka bir sabit disk ekleyin veya bunu yapın. Daha sonra eski doldurulmuş sabit diskten yeni, boş sürücüye içerik aktarmak için **Contentlibrarytransfer. exe** ' yi kullanın.
 
Aktarım tamamlandıktan sonra, içerik istemci bilgisayarlar tarafından yeni konumdan erişilebilir.



## <a name="usage"></a>Kullanım 

Dağıtım noktasında yönetim izinlerine sahip bir kullanıcı olarak **Contentlibrarytransfer. exe** ' yi çalıştırın. 

#### <a name="syntax"></a>Sözdizimi 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Örnek
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Sınırlamalar

- Aracı dağıtım noktasında yerel olarak çalıştırın. Uzak bir bilgisayardan çalıştıramazsınız.  

- Yalnızca istemciler dağıtım noktasına etkin bir şekilde erişmemişse kullanın. İstemci içeriğe erişirken aracı çalıştırırsanız, hedef sürücüdeki içerik kitaplığında eksik veriler olabilir. Veri aktarımı, kullanılamayan bir içerik kitaplığına tamamen başa çıkabilir.  

- Aracı çalıştırdığınızda içeriği dağıtım noktasına dağıtmayın. İçerik dağıtım noktasına yazılırken aracı çalıştırırsanız, hedef sürücüdeki içerik kitaplığında eksik veriler olabilir. Veri aktarımı, kullanılamayan bir içerik kitaplığına tamamen başa çıkabilir.



## <a name="see-also"></a>Ayrıca bkz.

- [İçerik yönetimi için temel kavramlar](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [İçerik kitaplığı](../plan-design/hierarchy/the-content-library.md)
