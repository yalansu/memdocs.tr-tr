---
title: İstemci iletişim bağlantı noktalarını yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager 'de istemci iletişim bağlantı noktalarını ayarlayın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713117"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Configuration Manager 'de istemci iletişim bağlantı noktalarını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcilerinin, iletişim için HTTP ve HTTPS kullanan site sistemleriyle iletişim kurmak için kullandığı istek bağlantı noktası numaralarını değiştirebilirsiniz. HTTP veya HTTPS 'nin güvenlik duvarları için zaten yapılandırılmış olmasına rağmen, HTTP veya HTTPS kullanan istemci bildirimi, yönetim noktası bilgisayarında özel bir bağlantı noktası numarası kullanmasından daha fazla CPU kullanımı ve bellek gerektirir. Ayrıca, istemcileri geleneksel uyandırma paketlerini kullanarak uyandırıyorsanız kullanılacak site bağlantı noktası numarasını da belirtebilirsiniz.  

 HTTP ve HTTPS istek bağlantı noktalarını belirttiğinizde, hem varsayılan bağlantı noktası numarasını hem de alternatif bağlantı noktası numarasını belirtebilirsiniz. Varsayılan bağlantı noktası ile iletişim başarısız olduktan sonra istemciler otomatik olarak alternatif bağlantı noktasını dener. HTTP ve HTTPS veri iletişimine yönelik ayarları belirtebilirsiniz.  

 İstemci istek bağlantı noktaları için varsayılan değerler, HTTP trafiği için **80** , HTTPS trafiği için **443** ' dir. Bu varsayılan değerleri kullanmak istemiyorsanız onları değiştirin. Özel bağlantı noktalarını kullanmak için tipik bir senaryo, varsayılan Web sitesi yerine IIS 'de özel bir Web sitesi kullanmaktır. IIS 'de varsayılan Web sitesinin varsayılan bağlantı noktası numaralarını değiştirirseniz ve diğer uygulamalar da varsayılan Web sitesini kullanıyorsa, bunlar başarısız olabilir.  

> [!IMPORTANT]
>  Configuration Manager ' deki bağlantı noktası numaralarını, sonuçları anlamak zorunda kalmadan değiştirmeyin. Örnekler:  
> 
> - İstemci istek Hizmetleri için bağlantı noktası numaralarını bir site yapılandırması olarak değiştirirseniz ve mevcut istemciler yeni bağlantı noktası numaralarını kullanacak şekilde yeniden yapılandırılmadığından, bu istemciler yönetilmez hale gelir.  
>   -   Varsayılan olmayan bir bağlantı noktası numarası yapılandırmadan önce, güvenlik duvarlarının ve tüm araya eklenen ağ cihazlarının bu yapılandırmayı destekleyebileceği ve bunları gerektiği şekilde yeniden yapılandırdığınızdan emin olun. Internet üzerindeki istemcileri yöneteceksiniz ve varsayılan HTTPS bağlantı noktası numarası olan 443 ' i değiştirirseniz, Internet üzerindeki yönlendiriciler ve güvenlik duvarları bu iletişimi engelleyebilir.  

 İstek bağlantı noktası numaralarını değiştirdikten sonra istemcilerin yönetilmeyen hale gelmediğinden emin olmak için, istemcilerin yeni istek bağlantı noktası numaralarını kullanacak şekilde yapılandırılması gerekir. Birincil sitedeki istek bağlantı noktalarını değiştirdiğinizde, tüm bağlı ikincil siteler aynı bağlantı noktası yapılandırmasını otomatik olarak alır. Birincil sitedeki istek bağlantı noktalarını yapılandırmak için bu konudaki yordamı kullanın.  

> [!NOTE]  
>  Linux ve UNIX çalıştıran bilgisayarlarda istemciler için istek bağlantı noktalarını yapılandırma hakkında daha fazla bilgi için bkz. [Linux ve UNIX Için istemci Için Istek bağlantı noktalarını yapılandırma](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Configuration Manager site Active Directory Domain Services yayımlandığında, bu bilgilere erişebilen yeni ve mevcut istemciler, site bağlantı noktası ayarlarıyla otomatik olarak yapılandırılır ve başka bir işlem yapmanız gerekmez. Active Directory Etki Alanı Hizmetlerine yayımlanan bu bilgilere erişemeyen istemciler içinde çalışma grubu istemcileri, başka bir Active Directory ormanından gelen istemciler, yalnızca İnternet için yapılandırılmış istemciler ve halen İnternet'te olan istemciler vardır. Bu istemciler yüklendikten sonra varsayılan bağlantı noktası numaralarını değiştirirseniz, aşağıdaki yöntemlerden birini kullanarak bunları yeniden yükleyin ve yeni istemcileri yükleyin:  

- Istemci anında Yükleme Sihirbazı 'nı kullanarak istemcileri yeniden yükleyin. Client push yüklemesi, istemcileri geçerli site bağlantı noktası yapılandırmasıyla otomatik olarak yapılandırır. Istemci anında Yükleme Sihirbazı 'nı kullanma hakkında daha fazla bilgi için bkz. [Client Push kullanarak Configuration Manager Istemcileri yükleme](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

- CCMSetup. exe ' yi ve CCMHTTPPORT ve CCMHTTPSPORT Client. msi yükleme özelliklerini kullanarak istemcileri yeniden yükleyin. Bu özellikler hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).  

- Active Directory Etki Alanı Hizmetlerinde Configuration Manager istemci yükleme özelliklerini arayan bir yöntemi kullanarak istemcileri yeniden yükleyin. Daha fazla bilgi için bkz. [Active Directory Domain Services yayımlanan istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  Mevcut istemcilerin bağlantı noktası numaralarını yeniden yapılandırmak için, komut dosyası PORTSWITCH ' i de kullanabilirsiniz. Yükleme medyası SMSSETUP\Tools\PortConfiguration klasöründe belirtilen VBS.  

> [!IMPORTANT]  
>  Halen Internet 'te olan mevcut ve yeni istemciler için, CCMSetup. exe Client. msi özelliklerini CCMHTTPPORT ve CCMHTTPSPORT kullanarak varsayılan olmayan bağlantı noktası numaralarını yapılandırmanız gerekir.  

 Sitedeki istek bağlantı noktalarını değiştirdikten sonra, site genelinde Client Push yükleme yöntemi kullanılarak yüklenen yeni istemciler, sitenin geçerli bağlantı noktası numaralarıyla otomatik olarak yapılandırılır.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Bir sitenin istemci iletişim bağlantı noktası numaralarını yapılandırmak için  

1. Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2. **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin, **siteler**' e tıklayın ve yapılandırılacak birincil siteyi seçin.  

3. **Giriş** sekmesinde, **Özellikler**' e ve ardından **bağlantı noktaları** sekmesine tıklayın.  

4. Öğelerin birini seçin ve **bağlantı noktası ayrıntısı** iletişim kutusunu göstermek için özellikler simgesine tıklayın.  

5. **Bağlantı noktası ayrıntısı** iletişim kutusunda öğe için bağlantı noktası numarasını ve açıklamasını belirtip **Tamam**' a tıklayın.  

6. IIS çalıştıran site sistemleri için **SMSWEB** 'in özel Web sitesi adını kullanacaksanız **özel Web sitesi kullan** ' ı seçin.  

7. Sitenin Özellikler iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.  

   Hiyerarşideki tüm birincil siteler için bu yordamı yineleyin.
