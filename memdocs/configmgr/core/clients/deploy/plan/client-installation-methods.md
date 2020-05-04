---
title: İstemci yükleme yöntemleri
titleSuffix: Configuration Manager
description: Configuration Manager istemcisini yükleme yöntemleri hakkında bilgi edinin.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713313"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Configuration Manager istemci yükleme yöntemleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemci yazılımını yüklemek için farklı yöntemler kullanabilirsiniz. Bir yöntem veya yöntemlerin birleşimini kullanın. Bu makalede her bir yöntemi açıklanmakta ve bu sayede kuruluşunuz için en iyi şekilde hangisinin hangisi olduğunu öğrenebilirsiniz.  

## <a name="client-push-installation"></a>Client push yüklemesi  

**Desteklenen istemci platformu**: Windows  

#### <a name="advantages"></a>Yararları  

-   İstemciyi tek bir bilgisayara, bilgisayar topluluğuna veya bir sorgunun sonuçlarına göre yüklemek için kullanılabilir.  

-   İstemciyi bulunan tüm bilgisayarlara otomatik olarak yüklemek için kullanılabilir.  

-   **İstemciye Göndererek Yükleme Özellikleri** iletişim kutusundaki **İstemci** sekmesinde tanımlanan istemci yükleme özelliklerini otomatik olarak kullanır.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Büyük topluluklara gönderirken yüksek ağ trafiğine neden olabilir.  

-   Yalnızca Configuration Manager tarafından keşfedilen bilgisayarlarda kullanılabilir.  

-   Bir çalışma grubuna istemci yüklemek için kullanılamaz.  

-   Amaçlanan istemci bilgisayarda yönetici haklarına sahip olan istemci gönderme yükleme hesabı belirtilmelidir  

-   Windows Güvenlik Duvarı, istemci bilgisayarlarda özel durumlarla yapılandırılmalıdır.   

-   İstemci gönderme yüklemesini iptal edemezsiniz. Configuration Manager, istemciyi bulunan tüm kaynaklara yüklemeye çalışır. Yedi güne kadar olan tüm sorunları yeniden dener.  

Daha fazla bilgi için bkz. [Client Push ile istemcileri yükleme](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Yazılım güncelleştirme noktası tabanlı yükleme  

**Desteklenen istemci platformu**: Windows  

#### <a name="advantages"></a>Yararları  

-   İstemci yazılımını yönetmek için mevcut yazılım güncelleştirme altyapısını kullanabilir.  

-   Active Directory Domain Services Windows Server Update Services (WSUS) ve Grup İlkesi ayarları doğru yapılandırılmışsa, istemci yazılımını yeni bilgisayarlara otomatik olarak yükleyebilir.  

-   İstemcinin yüklenebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

-   Bilgisayarlar Active Directory Etki Alanı Hizmetlerine yayımlanmış istemci yükleme özelliklerini okuyabilirler.  

-   İstemci kaldırılırsa, bu yöntem yeniden yükler.  

-   , Amaçlanan istemci bilgisayar için bir yükleme hesabı yapılandırmanızı ve bakımını gerektirmez.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Önkoşul olarak işleyen bir yazılım güncelleştirme altyapısı gerektirir.  

-   İstemci yüklemesi ve yazılım güncelleştirmeleri için aynı sunucuyu kullanmanız gerekir. Bu sunucunun bir birincil sitede bulunması gerekir.  

-   Yeni istemcileri yüklemek için Active Directory Domain Services içinde bir Grup İlkesi nesnesini istemcinin etkin yazılım güncelleştirme noktası ve bağlantı noktasıyla yapılandırmanız gerekir.  

-   Active Directory şeması Configuration Manager için genişletilmemişse, istemci yükleme özelliklerine sahip bilgisayarları sağlamak için Grup İlkesi ayarlarını kullanmanız gerekir.  

Daha fazla bilgi için bkz. [yazılım güncelleştirmesi tabanlı yükleme ile istemcileri yükleme](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Grup ilkesi yüklemesi  

**Desteklenen istemci platformu**: Windows  

#### <a name="advantages"></a>Yararları  

-   İstemcinin yüklenebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

-   Yeni istemci yüklemelerinde veya yükseltmelerde kullanılabilir.  

-   Bilgisayarlar Active Directory Etki Alanı Hizmetlerine yayımlanmış istemci yükleme özelliklerini okuyabilirler.  

-   , Amaçlanan istemci bilgisayar için bir yükleme hesabı yapılandırmanızı ve bakımını gerektirmez.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Çok sayıda istemci yükleniyorsa yüksek ağ trafiğine neden olabilir.  

-   Active Directory şeması Configuration Manager uzatılmazsa, sitenizdeki bilgisayarlara istemci yükleme özellikleri eklemek için Grup İlkesi ayarlarını kullanmanız gerekir.  

Daha fazla bilgi için bkz. [Grup İlkesi ile istemci yüklemesi](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Oturum açma betiği yüklemesi  

**Desteklenen istemci platformu**: Windows  

#### <a name="advantages"></a>Yararları  

-   İstemcinin yüklenebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

-   CCMSetup için komut satırı özelliklerini kullanmayı destekler.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Kısa bir süre içinde çok sayıda istemci yükleniyorsa yüksek ağ trafiğine neden olabilir.  

-   Kullanıcılar ağda sık oturum açık değilse, tüm istemci bilgisayarlara yüklenmesi uzun zaman alabilir.  

Daha fazla bilgi için bkz. [oturum açma betiklerine sahip Istemcileri nasıl yüklenir](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>El ile yükleme  

**Desteklenen istemci platformu**: WINDOWS, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Yararları  

-   İstemcinin yüklenebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

-   Sınama amacıyla yararlı olabilir.  

-   CCMSetup için komut satırı özelliklerini kullanmayı destekler.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Otomasyon olmadığından zaman alıcıdır.  

İstemcisinin her platforma el ile nasıl yükleneceği hakkında daha fazla bilgi için aşağıdaki makalelere bakın:  

-   [İstemcileri Windows bilgisayarlara dağıtma](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [UNIX ve Linux sunuculara istemci dağıtma](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Mac bilgisayarlara istemci dağıtma](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>MDM yüklemesini Microsoft Intune

**Desteklenen istemci platformları**: Windows 10

#### <a name="advantages"></a>Yararları  

-   İstemcinin yüklenebilmesi için bilgisayarların keşfedilmesini gerektirmez.  

-   , Amaçlanan istemci bilgisayar için bir yükleme hesabı yapılandırmanızı ve bakımını gerektirmez.  

-   Azure Active Directory ile modern kimlik doğrulaması kullanabilir.  

-   İnternet 'te bilgisayar yükleyebilir ve atayabilir.  

-   , Ortak yönetim için Windows AutoPilot ve Microsoft Intune otomatikleştirebilir.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Configuration Manager dışında ek teknolojiler gerektirir.  

-   İnternet tabanlı olmasa bile cihazın İnternet erişimine sahip olmasını gerektirir.  

Daha fazla bilgi için aşağıdaki makalelere bakın:  

-   [İstemcileri Intune MDM ile yönetilen Windows cihazlarına nasıl yükleyebilirim?](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Kimlik doğrulaması için Azure AD 'yi kullanarak Configuration Manager Windows 10 istemcileri yükleyip atama](../deploy-clients-cmg-azure.md)  

