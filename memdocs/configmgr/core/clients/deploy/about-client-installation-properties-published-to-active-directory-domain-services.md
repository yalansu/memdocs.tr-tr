---
title: Active Directory istemci yükleme özellikleri
titleSuffix: Configuration Manager
description: Active Directory Domain Services Configuration Manager istemci yükleme özelliklerini yayımlayın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712074"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Active Directory Etki Alanı Hizmetlerine yayımlanan istemci yükleme özellikleri hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için Active Directory şemasını genişlettiğinizde ve site Active Directory Domain Services yayımlandığında, birçok istemci yükleme özelliği Active Directory Domain Services olarak yayımlanır. Bir bilgisayar bu istemci yükleme özelliklerini bulabiliyorsa, Configuration Manager istemci dağıtımı sırasında onları kullanabilir.  

 İstemci yükleme özelliklerini yayımlamak için Active Directory Etki Alanı Hizmetlerini kullanmanın avantajları şunlardır:  

-   Yazılım güncelleştirme noktası tabanlı istemci yüklemeleri ve grup ilkesi istemci yüklemeleri, her bilgisayarda kurulum parametrelerinin ayarlanmış olmasını gerektirmez.  

-   Bu bilgiler otomatik olarak oluşturulduğundan, yükleme özelliklerinin elle girilmesiyle ilişkili insan hatası riski ortadan kalkar.  

> [!NOTE]  
>  Configuration Manager için Active Directory şemasının nasıl genişletileceği ve bir sitenin nasıl yayımlanacağı hakkında daha fazla bilgi için bkz. [Configuration Manager Için şema uzantıları](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Active Directory Domain Services yayımlanan istemci yükleme özellikleri  
İstemci yükleme özelliklerinin listesi aşağıda verilmiştir. Aşağıda listelenen her öğe hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).  

- Configuration Manager site kodu.  

- Site sunucusu imzalama sertifikası.  

- Güvenilen kök anahtar.  

- HTTP ve HTTPS istemci iletişim bağlantı noktaları.  

- Geri dönüş durum noktası. Sitede birden çok geri dönüş durum noktası varsa, Active Directory Domain Services için yalnızca ilk yüklenen ad yayımlanır.  

- İstemcinin yalnızca HTTPS kullanarak iletişim kurması gerektiğini belirten bir ayar.  

- PKI sertifikalarıyla ilgili ayarlar:  

  -   İstemci PKI sertifikasının kullanılıp kullanılmayacağı.  

  -   Sertifika seçimi için seçim ölçütleri. Bu, istemcinin Configuration Manager için kullanılabilen birden fazla geçerli PKI sertifikası olduğundan, bu gerekli olabilir.  

  -   Sertifika seçim işleminden sonra istemcinin birden çok geçerli sertifikası olduğunda hangi sertifikanın kullanılacağını belirleyen bir ayar.  

  -   Güvenilen kök CA sertifikalarının listesini içeren sertifika verenler listesi.  

- **Client Push Yükleme Özellikleri** iletişim kutusunun **İstemci** sekmesinde belirtilen client.msi yükleme özellikleri.

İstemci yüklemesi (CCMSetup), yalnızca aşağıdakilerden biri kullanılarak başka hiçbir özellik belirtilmemişse Active Directory Domain Services yayımlanan özellikleri kullanır:  

-   El ile yükleme yöntemi (Bu makalenin ilerleyen kısımlarında açıklanmıştır)

-   Grup ilkesi yükleme yöntemi (Bu makalenin ilerleyen kısımlarında açıklanmıştır)

> [!NOTE]  
>  İstemci yükleme özellikleri istemciyi yüklemek için kullanılır. İstemci yüklendikten ve bir Configuration Manager sitesine başarıyla atandıktan sonra, atanan sitesindeki yeni ayarlarla bu özelliklerin üzerine yazılabilir.  

 İstemci yükleme özelliklerini almak için Active Directory Domain Services hangi Configuration Manager istemci yükleme yöntemlerinin kullandığını öğrenmek için aşağıdaki bölümlerdeki ayrıntıları kullanın.  

## <a name="client-push-installation"></a>Client push yüklemesi  
 Client push yüklemesi, yükleme özelliklerini almak için Active Directory Etki Alanı Hizmetlerini kullanmaz.  

 Bunun yerine Client **push yükleme özellikleri** Iletişim kutusunun **yükleme özellikleri** sekmesinde istemci yükleme özelliklerini belirtebilirsiniz. Bu seçenekler ve istemci ile ilgili site ayarları istemci yükleme sırasında istemcinin okuduğu dosyaya depolanır.  

> [!NOTE]  
>  Client push yüklemesi için herhangi bir CCMSetup özelliği veya geri dönüş durumu noktası ya da **yükleme özellikleri** sekmesinde Güvenilen kök anahtarı belirtmeniz gerekmez. Bu ayarlar, istemcilere client push yüklemesi kullanılarak yüklendiklerinde otomatik olarak sağlanır.
CCMSetup, Client. msi özelliklerine ek olarak şu parametreleri destekler:/forcereboot,/skipprereq,/Logon,/Bitspriınlık,/DownloadTimeout,/forceinstall

 Site Active Directory Domain Services yayımlandıysa, **yükleme özellikleri** sekmesinde belirttiğiniz tüm özellikler Active Directory Domain Services yayımlanır. Bu ayarlar, CCMSetup'ın bir yükleme özelliği olmadan çalıştırıldığı istemci yüklemeleri tarafından okunur.  

## <a name="software-update-point-based-installation"></a>Yazılım güncelleştirme noktası tabanlı yükleme  
 Yazılım güncelleştirme noktası tabanlı yükleme yöntemi, yükleme özelliklerinin CCMSetup komut satırına eklenmesini desteklemez.  

 İstemci bilgisayarda Grup İlkesi kullanılarak bir komut satırı özelliği sağlanmamışsa CCMSetup, yükleme özellikleri için Active Directory Etki Alanı Hizmetlerini arar.  

## <a name="group-policy-installation"></a>Grup İlkesi yüklemesi  
 Grup İlkesi yüklemesi yöntemi, yükleme özelliklerinin CCMSetup komut satırına eklenmesini desteklemez.  

 İstemci bilgisayarda bir komut satırı özelliği sağlanmamışsa CCMSetup yükleme özellikleri için Active Directory Etki Alanı Hizmetlerini arar.  

## <a name="manual-installation"></a>El ile yükleme  
 CCMSetup, aşağıdaki koşullarda yükleme özellikleri için Active Directory Etki Alanı Hizmetleri'ni arar:  

-   CCMSetup.exe komutundan sonra hiçbir komut satırı özelliği belirtilmez.  

-   Bilgisayar, Grup İlkesi kullanılarak yükleme özellikleriyle sağlanmamıştır.  

## <a name="logon-script-installation"></a>Oturum açma betiği yüklemesi  
 CCMSetup, aşağıdaki koşullarda yükleme özellikleri için Active Directory Etki Alanı Hizmetleri'ni arar:  

-   CCMSetup.exe komutundan sonra hiçbir komut satırı özelliği belirtilmez.  

-   Bilgisayar, Grup İlkesi kullanılarak yükleme özellikleriyle sağlanmamıştır.  

## <a name="software-distribution-installation"></a>Yazılım dağıtım yüklemesi  
 CCMSetup, aşağıdaki koşullarda yükleme özellikleri için Active Directory Etki Alanı Hizmetleri'ni arar:  

-   CCMSetup.exe komutundan sonra hiçbir komut satırı özelliği belirtilmez.  

-   Bilgisayar, Grup İlkesi kullanılarak yükleme özellikleriyle sağlanmamıştır.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Active Directory Domain Services erişeolmayan istemciler için Yüklemeler  
Bu istemci bilgisayarlar Active Directory Domain Services yayımlanan yükleme özelliklerini okuyamıyor veya erişemez.

 Bu istemciler şunları içerir:  

-   Çalışma grubu bilgisayarları.  

-   Active Directory Domain Services yayımlanmayan bir Configuration Manager sitesine atanan istemciler.  

-   Internet 'te olduklarında yüklü olan istemciler.  
