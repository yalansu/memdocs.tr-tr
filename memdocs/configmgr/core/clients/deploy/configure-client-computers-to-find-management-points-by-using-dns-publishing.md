---
title: İstemcileri DNS yayımlaması kullanacak şekilde yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager istemci bilgisayarlarını, DNS yayımlaması kullanarak yönetim noktalarını bulacak şekilde yapılandırın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713103"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>İstemci bilgisayarlarını, DNS yayımlaması kullanarak yönetim noktalarını bulacak şekilde yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içindeki istemciler, site atamasını tamamlamaya yönelik bir yönetim noktası ve yönetilmeye devam etmek için bir devam eden işlem olarak bulunmalıdır. Active Directory Etki Alanı Hizmetleri, intranetteki istemcilerin yönetim noktaları bulması için en güvenli yöntemi sağlar. Ancak, istemciler bu hizmet konumu yöntemini kullanamazlarsa (örneğin, Active Directory şemasını genişletmediniz veya istemciler bir çalışma grubundan), tercih edilen alternatif servis konumu yöntemi olarak DNS yayınlamayı kullanın.  

> [!NOTE]  
>  İstemciyi Linux ve UNIX için yüklediğinizde, iletişimin başlangıç noktası olarak kullanmak üzere bir yönetim noktası belirleyin. Linux ve UNIX için istemcinin nasıl yükleneceği hakkında bilgi için bkz. [ISTEMCILERI UNIX ve Linux sunucularına dağıtma](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Yönetim noktaları için DNS yayınlaması kullanmadan önce intranetteki DNS sunucularının, sitenin yönetim noktaları için hizmet konumu kaynak kayıtlarına (SRV RR) ve ilgili konak (A veya AAA) kaynak kayıtlarına sahip olduğundan emin olun. Hizmet konumu kaynak kayıtları, DNS 'deki kayıtları oluşturan DNS Yöneticisi tarafından Configuration Manager veya el ile otomatik olarak oluşturulabilir.  

 Configuration Manager istemcileri için hizmet konumu olarak DNS yayımlama hakkında daha fazla bilgi için bkz. [İstemcilerin site kaynaklarını ve hizmetleri nasıl bulduklarını anlama Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Varsayılan olarak, istemciler kendi DNS etki alanlarındaki yönetim noktaları için DNS arar. Ancak, istemcinin etki alanında yayımlanmış bir yönetim noktası yoksa, istemcileri bir yönetim noktası DNS soneki ile el ile yapılandırmanız gerekir. İstemcilerdeki bu DNS sonekini, istemci yüklemesi sırasında veya sonrasında yapılandırabilirsiniz.  

-   İstemci yüklemesi sırasında bir yönetim noktası sonekine ait istemcileri yapılandırmak için CCMSetup Client.msi özelliklerini yapılandırın.  

-   İstemci yüklemesinden sonra bir yönetim noktası sonekine ait istemcileri yapılandırmak için Denetim Masası'nda **Configuration Manager Özellikleri**'ni yapılandırın.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>İstemci yüklemesi sırasında bir yönetim noktası sonekine ait istemcileri yapılandırmak için  

- İstemciyi aşağıdaki CCMSetup Client.msi özelliğiyle yükleyin:  

  - **DnsSuffix =** * &lt;yönetim noktası etki alanı\>*  

     Site birden fazla yönetim noktasına sahipse ve bunlar birden fazla etki alanındaysa yalnızca bir etki alanı belirtin. İstemciler bu etki alanında bir yönetim noktasına bağlandığında, diğer etki alanlarından yönetim noktalarını içeren kullanılabilir yönetim noktalarının bir listesini indirir.  

    CCMSetup komut satırı özellikleri hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>İstemci yüklemesinden sonra bir yönetim noktası sonekine ait istemcileri yapılandırmak için  

1.  İstemci bilgisayarın Denetim Masası'nda **Configuration Manager**'a gidin ve **Özellikler**'i çift tıklatın.  

2.  **Site** sekmesinde bir yönetim noktasına ait DNS sonekini belirtin ve daha sonra **Tamam**'ı tıklatın.  

     Site birden fazla yönetim noktasına sahipse ve bunlar birden fazla etki alanındaysa yalnızca bir etki alanı belirtin. İstemciler bu etki alanında bir yönetim noktasına bağlandığında, diğer etki alanlarından yönetim noktalarını içeren kullanılabilir yönetim noktalarının bir listesini indirir.
