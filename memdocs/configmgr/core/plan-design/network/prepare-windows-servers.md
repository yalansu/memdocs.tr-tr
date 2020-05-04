---
title: Windows Sunucularını hazırlama
titleSuffix: Configuration Manager
description: Bir bilgisayarın Configuration Manager için bir site sunucusu veya site sistem sunucusu olarak kullanım önkoşullarını karşıladığından emin olun.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8889c0ee306eaaf682563b2e8e72d5482054d1c7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710793"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Windows Server'ı, Configuration Manager’ı destekleyecek şekilde hazırlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için bir Windows bilgisayarını site sistem sunucusu olarak kullanabilmeniz için, bilgisayarın site sunucusu veya site sistem sunucusu olarak amaçlanan kullanımı için önkoşulları karşılaması gerekir.  

- Bu Önkoşullar genellikle Sunucu Yöneticisi bilgisayarları kullanılarak etkinleştirilen bir veya daha fazla Windows özelliğini veya rolünü içerir.  

- Windows özelliklerini ve rollerini etkinleştirme yöntemi işletim sistemi sürümleri arasında farklılık yaptığından, kullandığınız işletim sistemini ayarlama hakkında ayrıntılı bilgi için işletim sistemi sürümünüze yönelik belgelere bakın.  

Bu makaledeki bilgiler, Configuration Manager site sistemlerini desteklemek için gereken Windows yapılandırmalarının türlerine genel bir bakış sağlar. Belirli site sistem rollerinin yapılandırma ayrıntıları için bkz. [site ve site sistemi önkoşulları](../configs/site-and-site-system-prerequisites.md).

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a>Windows özellikleri ve rolleri  
Bir bilgisayarda Windows özelliklerini ve rollerini ayarlarken, bu yapılandırmayı gerçekleştirmek için bilgisayarı yeniden başlatmanız gerekebilir. Bu nedenle, bir Configuration Manager sitesini veya site sistem sunucusunu yüklemeden önce belirli site sistem rollerini barındıracak bilgisayarları belirlemek iyi bir fikirdir.

### <a name="features"></a>Özellikler  
Aşağıdaki Windows özellikleri, belirli site sistem sunucularında gereklidir ve söz konusu bilgisayara bir site sistem rolü yüklemeden önce ayarlanmalıdır.  

- **.NET Framework**: Aşağıdakiler dahil  

    - ASP.NET  
    - HTTP Etkinleştirmesi  
    - HTTP olmayan etkinleştirme  
    - Windows Communication Foundation (WCF) Hizmetleri  

    Farklı site sistemi rolleri .NET Framework farklı sürümlerini gerektirir.  

    .NET Framework 4,0 ve üzeri sürümleri, 3,5 ve önceki sürümlerin yerini alacak şekilde geriye dönük olarak uyumlu olmadığından, farklı sürümler gerekli olarak listelendiğinde, aynı bilgisayardaki her sürümü etkinleştirmeyi planlayın.  

- **Arka plan Akıllı Aktarım Hizmetleri (BITS)**: yönetim noktaları, yönetilen cihazlarla iletişimi desteklemek için BITS (ve otomatik olarak belirlenen seçenekler) gerektirir.  

- **BranchCache**: dağıtım noktaları, BranchCache kullanan istemcileri desteklemek için BranchCache ile ayarlanabilir.  

- **Yinelenen verileri kaldırma**: dağıtım noktaları, ile ayarlanabilir ve yinelenen verileri kaldırma özelliğinden yararlanabilir.  

- **Uzaktan değişiklikleri sıkıştırma (RDC)**: bir site sunucusu veya dağıtım noktası barındıran her bilgisayar RDC gerektirir. RDC, paket imzaları üretmek için kullanılır ve imza karşılaştırmaları gerçekleştirir.  

### <a name="roles"></a>Roller  
Aşağıdaki Windows rolleri, yazılım güncelleştirmeleri ve işletim sistemi dağıtımları gibi belirli işlevleri desteklemek için gereklidir, ancak IIS en sık kullanılan site sistemi rolleri için gereklidir.  

- **Ağ aygıtı kayıt hizmeti** (Active Directory Sertifika Hizmetleri altında): Bu Windows rolü, Configuration Manager Sertifika profillerinin kullanılması için önkoşuldur.  

- **Web sunucusu (IIS)**: aşağıdakiler dahil:  
    - Ortak HTTP Özellikleri  
          - HTTP Yeniden Yönlendirme  
    - Uygulama Geliştirme  
          - .NET Genişletilebilirliği  
          - ASP.NET  
          - ISAPI Uzantıları  
          - ISAPI Filtreleri  
    - Yönetim Araçları  
          - IIS 6 Yönetimi Uyumluluğu  
          - IIS 6 Metatabanı Uyumluluğu  
          - IIS 6 Windows Yönetim Araçları (WMI) uyumluluğu  
    - Güvenlik  
          - İstek Filtreleme  
          - Windows Kimlik Doğrulaması  

  Aşağıdaki site sistem rolleri listelenen IIS yapılandırmalarından birini veya birkaçını kullanır:  
  - Uygulama Kataloğu web hizmet noktası  
  - Uygulama Kataloğu web sitesi noktası  
  - Dağıtım noktası  
  - Kayıt noktası  
  - Kayıt proxy noktası  
  - Geri dönüş durumu noktası  
  - Yönetim noktası  
  - Yazılım güncelleştirme noktası  
  - Durum Geçiş noktası     

  Gereken en düşük IIS sürümü, site sunucusunun işletim sistemi ile birlikte sağlanan sürümdür.  

  Bu IIS yapılandırmalarına ek olarak, [dağıtım noktaları Için IIS Istek filtrelemeyi](#BKMK_IISFiltering)ayarlamanız gerekebilir.  

- **Windows Dağıtım Hizmetleri**: Bu rol, işletim sistemi dağıtımı ile kullanılır.  

- **Windows Server Update Services**: Bu rol, yazılım güncelleştirmeleri için gereklidir.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a>Dağıtım noktaları için IIS istek filtreleme  
Varsayılan olarak IIS, çeşitli dosya adı uzantılarına ve klasör konumlarına HTTP veya HTTPS iletişimleri aracılığıyla erişimi engellemek için istek filtreleme kullanır. Dağıtım noktasında bu, istemcilerin engellenen uzantıları veya klasör konumlarını içeren paketleri indirmelerini engeller.  

Paket kaynak dosyalarınız, istek filtreleme yapılandırmanız tarafından IIS 'de engellenen uzantılara sahip olduğunda, izin vermek için istek filtrelemeyi ayarlamanız gerekir. Bu, dağıtım noktası bilgisayarlarınızdaki IIS Yöneticisi 'nde [istek filtreleme özelliği düzenlenerek](https://technet.microsoft.com/library/hh831621.aspx) yapılır.  

Ayrıca, aşağıdaki dosya adı uzantıları, paketler ve uygulamalar için Configuration Manager tarafından kullanılır. İstek filtreleme yapılandırmalarınızın bu dosya uzantılarını engellemediğinden emin olun:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Örneğin, bir yazılım dağıtımına ait kaynak dosyaları **bin** adlı bir klasör içerebilir veya **. mdb** dosya adı uzantısına sahip bir dosyaya sahip olabilir.  

- Varsayılan olarak IIS istek filtreleme, bu öğelere erişimi engeller (**bin** gizli kesim olarak engellenir ve **. mdb** dosya adı uzantısı olarak engellenir).  

- Dağıtım noktasında varsayılan IIS yapılandırmasını kullandığınızda, BITS kullanan istemciler bu yazılım dağıtımını dağıtım noktasından indiremez ve içerikleri beklediğini belirtir.  

- İstemcilerin bu içeriği indirmesini sağlamak için, her ilgili dağıtım noktasında, dağıttığınız paketlerdeki ve uygulamalardaki dosya uzantılarına ve klasörlere erişime izin vermek üzere IIS Yöneticisi 'ndeki **Istek filtrelemesini** düzenleyin.  

> [!IMPORTANT]  
> İstek filtresindeki düzenlemeler, bilgisayarın saldırı yüzeyini artırabilir.  
> 
> - Sunucu düzeyinde yaptığınız düzenlemeler, sunucudaki tüm Web siteleri için geçerlidir.   
>     - Ayrı Web sitelerinde yaptığınız düzenlemeler yalnızca o Web sitesi için geçerlidir.  
> 
> En iyi güvenlik uygulaması, Configuration Manager adanmış bir Web sunucusunda çalıştırıldır. Web sunucusunda başka uygulamalar çalıştırmanız gerekiyorsa, Configuration Manager için özel bir Web sitesi kullanın. Bilgi için bkz. [site sistemi sunucuları Için Web siteleri](websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>HTTP fiilleri
**Yönetim noktaları:** İstemcilerin bir yönetim noktasıyla başarılı bir şekilde iletişim kurabildiğinden emin olmak için, yönetim noktası sunucusunda aşağıdaki HTTP fiillerine izin verildiğinden emin olun:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Dağıtım noktaları:** Dağıtım noktaları, aşağıdaki HTTP fiillerinin izin verilen şekilde olmasını gerektirir:
- GET
- HEAD
- PROPFIND

Daha fazla bilgi için bkz. [IIS 'de istek filtrelemeyi yapılandırma](https://technet.microsoft.com/library/hh831621.aspx#Verbs). 
