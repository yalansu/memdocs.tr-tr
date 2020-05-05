---
title: Site sistemleri için Web siteleri
titleSuffix: Configuration Manager
description: Configuration Manager 'de site sistem sunucuları için varsayılan ve özel Web siteleri hakkında bilgi edinin.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 344ba7f6a6b0ee7683c3ac7661338f01be601a10
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718696"
---
# <a name="websites-for-site-system-servers-in-configuration-manager"></a>Configuration Manager'da site sistemi sunucuları için web siteleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Birçok Configuration Manager site sistem rolü, Microsoft Internet Information Services (IIS) kullanımını gerektirir ve site sistem hizmetlerini barındırmak için varsayılan IIS Web sitesini kullanır. Aynı sunucuda diğer Web uygulamalarını çalıştırmanız gerektiğinde ve ayarlar Configuration Manager uyumlu değilse, Configuration Manager için özel bir Web sitesi kullanmayı düşünün.  

> [!TIP]  
>  En iyi güvenlik uygulaması, IIS gerektiren Configuration Manager site sistemleri için bir sunucu ayırmayı kullanmaktır. Configuration Manager bir site sisteminde diğer uygulamaları çalıştırdığınızda, o bilgisayarın saldırı yüzeyini artırırsınız.  




##  <a name="what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a>Özel Web sitelerini kullanmayı seçmeden önce bilmeniz gerekenler  
 Site sistem rolleri varsayılan olarak IIS’teki **Varsayılan Web Sitesi**’ni kullanır. Bu, site sistemi rolü yüklediğinde otomatik olarak ayarlanır. Ancak, birincil sitelerde bunun yerine özel web siteleri kullanmayı seçebilirsiniz. Özel web siteleri kullanırken:  

-   Özel Web siteleri, bireysel site sistem sunucuları veya rolleri yerine tüm site için etkinleştirilir.  

-   Birincil sitelerde, uygulanabilir bir site sistem rolünü barındıracak her bilgisayar **SMSWEB**adlı özel bir Web sitesi ile ayarlanmalıdır. Bu Web sitesini oluşturup bu bilgisayarda özel Web sitesini kullanmak üzere site sistem rolleri ayarlamadan, istemciler ilgili bilgisayardaki site sistem rolleriyle iletişim kuramamayabilir.  

-   İkincil siteler, birincil üst siteleri olarak ayarlandığı sırada özel bir Web sitesi kullanmak üzere otomatik olarak ayarlandığı için, IIS gerektiren her bir ikincil site sistemi sunucusunda IIS 'de özel Web siteleri de oluşturmanız gerekir.  


  **Özel web siteleri kullanma önkoşulları:**  

 Bir sitede özel web siteleri kullanma seçeneğini etkinleştirmeden önce aşağıdakileri yapmalısınız:  

-   IIS gerektiren her site sistem sunucusunda **SMSWEB** adlı özel bir web sitesi oluşturun. Bunu birincil sitede ve tüm alt ikincil sitelerde yapın.  

-   Configuration Manager istemci iletişimi (istemci isteği bağlantı noktası) için ayarladığınız aynı bağlantı noktasına yanıt vermek üzere özel Web sitesini ayarlayın.  

-   Özel bir klasör kullanan her özel veya varsayılan Web sitesi için, kullandığınız varsayılan belge türünün bir kopyasını Web sitesini barındıran kök klasörde yerleştirin. Örneğin, varsayılan yapılandırmalara sahip bir Windows Server 2008 R2 bilgisayarında **iisstart. htm** , kullanılabilir olan birkaç varsayılan belge türünden biridir. Bu dosyayı varsayılan Web sitesinin kökünde bulabilir ve ardından SMSWEB özel Web sitesini barındıran kök klasörde bu dosyanın bir kopyasını (veya kullandığınız varsayılan belge türünün bir kopyasını) yerleştirebilirsiniz. Varsayılan belge türleri hakkında daha fazla bilgi için bkz. [IIS Için varsayılan &lt;belge defaultDocument\> ](https://www.iis.net/configreference/system.webserver/defaultdocument).  

**IIS gereksinimleri hakkında:**
**aşağıdaki site sistem rolleri, site sistem hizmetlerini barındırmak için IIS ve bir Web sitesi gerektirir:**  

-   Uygulama Kataloğu web hizmet noktası  

-   Uygulama Kataloğu web sitesi noktası  

-   Dağıtım noktası  

-   Kayıt noktası  

-   Kayıt proxy noktası  

-   Geri dönüş durumu noktası  

-   Yönetim noktası  

-   Yazılım güncelleştirme noktası  

-   Durum Geçiş noktası  

Ek hususlar:  

-   Birincil sitede özel Web siteleri etkinken, bu siteye atanan istemciler, geçerli site sistemi sunucularındaki varsayılan Web siteleri yerine özel web siteleriyle iletişim kurmaya yönlendirilir  

-   Bir birincil site için özel Web siteleri kullanıyorsanız, istemcilerin hiyerarşide başarıyla dolaşabildiklerinden emin olmak için hiyerarşinizdeki tüm birincil siteler için özel Web sitelerini göz önünde bulundurun. (Bir istemci bilgisayar, farklı bir site tarafından yönetilen yeni bir ağ kesimine taşındığında dolaşım gerçekleşir. Dolaşım, bir istemcinin WAN bağlantısı yerine yerel olarak erişebileceği kaynakları etkileyebilir.  

-   IIS kullanan ancak istemci bağlantılarını kabul etmeyen, ancak raporlama hizmetleri noktası gibi site sistem rolleri, varsayılan Web sitesi yerine SMSWEB web sitesini de kullanır.  

-   Özel Web siteleri, bilgisayarın varsayılan Web sitesinin kullandığı ayarlardan farklı bağlantı noktası numaraları atamanızı gerektirir. Varsayılan web sitesi ve özel web sitesi TCP/IP bağlantı noktalarını aynı anda kullanmaya çalışırsa, her iki site aynı anda çalıştırılamaz.  

-   Özel Web sitesi için IIS 'de ayarladığınız TCP/IP bağlantı noktaları, site için istemci istek bağlantı noktalarıyla eşleşmelidir.  

## <a name="switch-between-default-and-custom-websites"></a>Varsayılan ve özel Web siteleri arasında geçiş yap  
Birincil sitede özel Web sitelerini kullanmaya ilişkin kutuyu dilediğiniz zaman denetleyebilir veya işaretini kaldırabilirsiniz (Bu kutu, sitenin özelliklerinin genel sekmesindedir), bu değişikliği yapmadan önce dikkatle planlayın. Bu yapılandırma değiştiğinde, birincil sitedeki ve alt ikincil sitelerdeki tüm ilgili site sistem rollerinin kaldırılması ve yeniden yüklenmesi gerekir:  

Aşağıdaki roller **otomatik olarak yeniden yüklenir**:  

-   Yönetim noktası  

-   Dağıtım noktası  

-   Yazılım güncelleştirme noktası  

-   Geri dönüş durumu noktası  

-   Durum Geçiş noktası  

Aşağıdaki roller **el ile yeniden yüklenmelidir**:  

-   Uygulama Kataloğu web hizmet noktası  

-   Uygulama Kataloğu web sitesi noktası  

-   Kayıt noktası  

-   Kayıt proxy noktası  

Ek olarak:  

-   Varsayılan Web sitesinden özel bir Web sitesi kullanmak üzere değişiklik yaptığınızda, Configuration Manager eski sanal dizinleri kaldırmaz. Configuration Manager kullanılan dosyaları kaldırmak istiyorsanız, varsayılan Web sitesi altında oluşturulan sanal dizinleri el ile silmeniz gerekir.  

-   Siteyi özel Web siteleri kullanacak şekilde değiştirirseniz, siteye zaten atanmış istemciler özel Web siteleri için yeni istemci isteği bağlantı noktalarını kullanacak şekilde yeniden yapılandırılmalıdır. Bkz. [istemci iletişim bağlantı noktalarını yapılandırma](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Özel Web sitelerini ayarlama  
Özel web sitesi oluşturma adımları farklı işletim sistemi sürümlerinde farklılık gösterdiğinden, tam adımlar için işletim sistemi sürümünüze ilişkin belgelere bakın, ancak uygun olduğunda aşağıdaki bilgileri kullanın:  

-   Web sitesi adı şu olmalıdır: **SMSWEB**.  

-   HTTPS 'yi ayarlarken, yapılandırmayı kaydedebilmeniz için önce bir SSL sertifikası belirtmeniz gerekir.  

-   Özel Web sitesini oluşturduktan sonra, IIS 'deki diğer Web sitelerinden kullandığınız özel Web sitesi bağlantı noktalarını kaldırın:  

    1.  **SMSWEB** Web sitesine atananlarla eşleşen bağlantı noktalarını kaldırmak için diğer web sitelerinin **bağlamalarını** düzenleyin.  

    2.  **SMSWEB** Web sitesini başlatın.  

    3.  Sitenin site sunucusunda **SMS_SITE_COMPONENT_MANAGER** hizmetini yeniden başlatın.  
