---
title: Sorguları Yönet
titleSuffix: Configuration Manager
description: Sorgularınızı yönetme hakkında bilgi edinin. Ayrıntılı başvuru için bir tablo içerir.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713754"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Configuration Manager sorguları yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Configuration Manager sorguları yönetmenize yardımcı olabilir.  

 Sorgu oluşturma hakkında daha fazla bilgi için bkz. [sorgu oluşturma](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Sorguları Yönet
 **İzleme** çalışma alanında **Sorgular**’ı, yönetilecek sorguyu ve ardından bir yönetim görevini seçin.  

 Aşağıdaki tabloda yönetim görevleri hakkında bilgi verilmektedir.  

|Yönetim görevi|Ayrıntılar| 
|---------------------|-------------|
|**Çalışmaz**|Seçili sorguyu çalıştırır ve sonuçları Configuration Manager konsolunda görüntüler.|
|**İstemci Yükle**|Configuration Manager istemcisini seçili sorgu tarafından döndürülen bilgisayarlara yüklemenizi sağlayan **Istemci yüklemesi Sihirbazı**' nı açar.<br /><br /> Bu seçenek mobil cihazlar, kullanıcılar veya Kullanıcı grupları döndüren sorgular için kullanılamaz. <br /><br /> İstemci gönderimi kullanarak Configuration Manager istemcilerini yükleme hakkında daha fazla bilgi için bkz. [Windows bilgisayarlarına Istemci dağıtma](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Dışarı aktar**|**Nesneleri dışarı aktarma Sihirbazı**' nı açar. Bu sihirbaz, sorguyu daha sonra başka bir sitede içeri aktarabileceğiniz bir Yönetilen Nesne Biçimi (MOF) dosyasına aktarmanıza olanak tanır.
|**Taşı**|**Seçili öğeleri taşı** iletişim kutusunu açar. Bu iletişim kutusu seçili sorguyu **sorgular** düğümü altında daha önce oluşturduğunuz bir klasöre taşımanızı sağlar.|

## <a name="next-steps"></a>Sonraki adımlar 
 [Sorgu oluştur](../../../core/servers/manage/create-queries.md)
