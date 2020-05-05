---
title: Rol tabanlı yönetim aracı
titleSuffix: Configuration Manager
description: Configuration Manager ' deki güvenlik rollerini ve kapsamları modellemek ve denetlemek için rol tabanlı yönetim ve denetim aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723190"
---
# <a name="role-based-administration-and-auditing-tool"></a>Rol Tabanlı Yönetim ve Denetim Aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Rol tabanlı yönetim ve Denetim Aracı [Configuration Manager araçlarından](tools.md)biridir. Aşağıdaki görevler için bu aracı kullanın:

- Belirli izinlere sahip güvenlik rollerini modelleyin  

- Diğer kullanıcıların sahip olduğu güvenlik kapsamlarını ve güvenlik rollerini denetleyin



## <a name="requirements"></a>Gereksinimler

- Configuration Manager konsolu ile aynı bilgisayarda çalıştır  

- **Tam yönetici**, **salt okuma analist**veya **Güvenlik Yöneticisi** rolüne sahipsiniz  

- Hesabınızı **Tüm** güvenlik kapsamına ve tüm koleksiyonlara atayın  

- (*Isteğe bağlı*) Rapor klasörü güvenliğini çözümlemek için, SQL erişiminizin olması gerekir  

- (*Isteğe bağlı*) Rapor detaylanmasını çözümlemek için, bu aracı site sistemi sunucusunda Raporlama noktası rolüyle çalıştırın



## <a name="procedures"></a>Yordamlar


### <a name="model-permissions-for-a-new-role"></a>Yeni bir rol için model izinleri

Oluşturmak istediğiniz yeni bir rol için izinleri modellemek üzere aşağıdaki yordamı kullanın: 

1. **Rbaviewer. exe**' yi çalıştırın.  

2. Üzerinde derlemek istediğiniz temel güvenlik rollerini seçin veya boş bir izin kümesinden başlayın. Gerekli izinleri seçin.  

3. Bu özel rolün göreceği Kullanıcı arabirimini görmek için **Çözümle** ' ye tıklayın.  

    > [!Note]  
    > Gereksinimlerinizi karşılayan mevcut bir güvenlik rolünün olup olmadığını görmek için, **benzerlik** sekmesine geçin.  

4. Rolü bir XML dosyası olarak kaydetmek için **dışarı aktar** ' a tıklayın. Ardından Configuration Manager konsoluna aktarın. Daha fazla bilgi için bkz. [özel güvenlik rolleri oluşturma](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Mevcut güvenlik kapsamlarını denetleme

Configuration Manager ' deki tüm mevcut yönetici kullanıcılarını, koleksiyonları ve güvenlik kapsamlarını denetlemek için aşağıdaki yordamı kullanın:

1. **Rbaviewer. exe**' yi çalıştırın.  

2. Araç çubuğundan **Denetim RBA** düğmesini seçin.  

    1. Koleksiyon sınırlı ilişkilerini bir ağaç görünümünde görüntülemek için, **koleksiyon Özeti** sekmesine geçin.  

    2. Bir güvenlik rolüne atanan nesneleri görüntülemek için, **kapsam Özeti** sekmesine geçin.  


### <a name="audit-a-specific-user"></a>Belirli bir kullanıcıyı denetleme

Belirli bir kullanıcı için rol tabanlı yönetim yapılandırmasını denetlemek için aşağıdaki yordamı kullanın:

1. **Rbaviewer. exe**' yi çalıştırın.  

2. Araç çubuğundaki **Farklı Çalıştır** düğmesini seçin.  

3. Bu hesabın izinlerini denetlemek için belirli kullanıcı adını girin.  

4. Araç, kullanıcıya veya kullanıcının ait olduğu güvenlik grubuna atanmış olan güvenlik rollerini görüntüler. Ayrıca, bu kullanıcının görebilecekleri nesneleri ve konsolunda gerçekleştirebileceği eylemleri de görüntüler.  



## <a name="see-also"></a>Ayrıca bkz.

- [Rol tabanlı yönetimin temelleri](../understand/fundamentals-of-role-based-administration.md)
- [Rol tabanlı yönetimi yapılandırma](../servers/deploy/configure/configure-role-based-administration.md)
