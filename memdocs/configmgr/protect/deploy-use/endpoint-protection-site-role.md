---
title: Endpoint Protection noktası site sistemi rolü oluştur
titleSuffix: Configuration Manager
description: Configuration Manager istemci bilgisayarlarındaki güvenlik ve kötü amaçlı yazılımları yönetmek için Endpoint Protection yapılandırmayı öğrenin.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710835"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Endpoint Protection noktası site sistemi rolü oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Endpoint Protection’ı kullanabilmeniz için Endpoint Protection noktası site sistemi rolü yüklenmelidir. Yalnızca bir site sistemi sunucusuna yüklenmelidir ve bir merkezi yönetim sitesinde veya bağımsız bir birincil sitede hiyerarşinin en üstüne yüklenmelidir.

Endpoint Protection için yeni bir site sistemi sunucusu yüklemek veya var olan bir site sistemi sunucusunu kullanmak istediğinize bağlı olarak aşağıdaki yordamlardan birini kullanın:
- [Yeni bir site sistemi sunucusuna yükler](#new-site-system-server)
- [Var olan bir site sistemi sunucusuna yükler](#existing-site-system-server)

> [!IMPORTANT]
>  Bir Endpoint Protection noktası yüklediğinizde, Endpoint Protection noktasını barındıran sunucuya Endpoint Protection istemci yüklenir. Sunucuya yüklenmiş var olan kötü amaçlı yazılımdan koruma çözümleriyle bir arada bulunabilmesi için bu istemcideki hizmetler ve taramalar devre dışı bırakılır. Bu sunucuyu daha sonra Endpoint Protection tarafından yönetim için etkinleştirir ve herhangi bir üçüncü taraf kötü amaçlı yazılımdan koruma çözümünü kaldırma seçeneğini belirlerseniz, üçüncü taraf ürün kaldırılmaz. Bu ürünü elle kaldırmanız gerekir.

## <a name="new-site-system-server"></a>Yeni site sistemi sunucusu

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.

2.  **Yönetim** çalışma alanında, **Site Yapılandırması**'nı genişletin ve **Sunucu ve Site Sistemi Rolleri**'ne tıklayın.

3.  **Oluştur** grubunun **Giriş** sekmesinde, **Site Sistemi Sunucusu Oluştur**'a tıklayın.

4.  **Genel** sayfasında, site sisteminin genel ayarlarını belirleyin ve **İleri**'yi tıklatın.

5.  **Sistem Rolü Seçimi** sayfasında, kullanılabilir roller listesinden **Endpoint Protection noktası** 'nı seçin ve ardından **İleri**'ye tıklayın.

6.  **Endpoint Protection** sayfasında **Endpoint Protection lisans koşullarını kabul ediyorum** onay kutusunu seçin ve ardından **İleri**’ye tıklayın.

    > [!IMPORTANT]
    >  Lisans koşullarını kabul etmediğiniz takdirde Configuration Manager Endpoint Protection kullanamazsınız.

7.  **Bulut koruma hizmeti** sayfasında, yeni tanımlar geliştirmeye yardımcı olmak için Microsoft 'a göndermek istediğiniz bilgi düzeyini seçin ve ardından **İleri**' ye tıklayın.

    > [!NOTE]
    >  Bu seçenek, varsayılan olarak kullanılan bulut koruma hizmeti (eski adıyla Microsoft Etkin Koruma Hizmeti veya HARITALAR) ayarlarını yapılandırır. Bundan sonra, oluşturduğunuz her bir kötü amaçlı yazılımdan koruma ilkesi için özel ayarlar yapılandırabilirsiniz. Microsoft 'un kötü amaçlı yazılımdan koruma tanımlarını daha güncel tutmasına yardımcı olabilecek kötü amaçlı yazılım örnekleri sunarak bilgisayarlarınızı daha güvenli tutmaya yardımcı olmak için bulut koruma hizmeti 'ne katın. Ayrıca, bulut koruma hizmeti 'ne katılırsanız Endpoint Protection istemcisi, Windows Update yayımlanmadan önce yeni tanımları indirmek için dinamik imza hizmetini kullanabilir. Daha fazla bilgi için bkz. [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md).

8.  Sihirbazı tamamlayın.


## <a name="existing-site-system-server"></a>Mevcut site sistemi sunucusu

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.

2.  **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin, **sunucular ve site sistemi rolleri**' ne tıklayın ve ardından Endpoint Protection için kullanmak istediğiniz sunucuyu seçin.

3.  **Sunucu** grubunun **Giriş** sekmesinde, **Site Sistemi Rolleri Ekle**'yi tıklatın.

4.  **Genel** sayfasında, site sisteminin genel ayarlarını belirleyin ve **İleri**'yi tıklatın.

5.  **Sistem Rolü Seçimi** sayfasında, kullanılabilir roller listesinden **Endpoint Protection noktası** 'nı seçin ve ardından **İleri**'ye tıklayın.

6.  **Endpoint Protection** sayfasında **Endpoint Protection lisans koşullarını kabul ediyorum** onay kutusunu seçin ve ardından **İleri**’ye tıklayın.

    > [!IMPORTANT]
    >  Lisans koşullarını kabul etmediğiniz takdirde Configuration Manager Endpoint Protection kullanamazsınız.

7.  **Bulut koruma hizmeti** sayfasında, yeni tanımlar geliştirmeye yardımcı olmak için Microsoft 'a göndermek istediğiniz bilgi düzeyini seçin ve ardından **İleri**' ye tıklayın.

    > [!NOTE]
    >  Bu seçenek, varsayılan olarak kullanılan bulut koruma hizmeti ayarlarını (eski adıyla HARITALAR) yapılandırır. Yapılandırdığınız her bir kötü amaçlı yazılımdan koruma ilkesi için özel ayarlar yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md).

8.  Sihirbazı tamamlayın.
