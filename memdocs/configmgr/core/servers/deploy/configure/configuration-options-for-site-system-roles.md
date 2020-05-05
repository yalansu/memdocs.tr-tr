---
title: Site sistemi rolü seçenekleri
titleSuffix: Configuration Manager
description: Kendine açıklayıcı olmayan Configuration Manager site sistem rolleri hakkında daha fazla bilgi için bu makaleye bakın.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721090"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configuration Manager 'de site sistemi rolleri için yapılandırma seçenekleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager site sistem rollerinin çoğu yapılandırma seçeneği kendi kendine açıklayıcıdır veya yapılandırdığınızda, sihirbazda veya iletişim kutularında açıklanmaktadır. Aşağıdaki bölümlerde, ayarları ek bilgi gerektirebilecek site sistem rolleri açıklanmaktadır.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a>Uygulama Kataloğu web sitesi noktası  

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Uygulama Kataloğu web sitesi noktasını ayarlama hakkında daha fazla bilgi için bkz. [uygulama yönetimini planlayın ve yapılandırın](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a>Uygulama Kataloğu Web hizmet noktası  

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Uygulama Kataloğu Web hizmeti noktasının nasıl ayarlanacağı hakkında daha fazla bilgi için bkz. [uygulama yönetimini planlayın ve yapılandırın](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a>Sertifika kayıt noktası  

Sertifika kayıt noktasını ayarlama hakkında daha fazla bilgi için bkz. [sertifika profillerine giriş](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a>Dağıtım noktası  

Dağıtım noktasının içerik dağıtımı için nasıl ayarlanacağı hakkında daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](manage-content-and-content-infrastructure.md).  

PXE dağıtımları için dağıtım noktasının nasıl ayarlanacağı hakkında daha fazla bilgi için, bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

Dağıtım noktasının çok noktaya yayın dağıtımları için nasıl ayarlanacağı hakkında daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Configuration Manager gerekliyse IIS 'yi yükleyip yapılandırın

Daha önce yüklenmemişse, site sisteminde IIS 'nin yüklenmesini ve kurulumunu Configuration Manager izin vermek için bu seçeneği belirleyin. IIS 'nin tüm dağıtım noktalarında yüklü olması gerekir ve sihirbazda devam etmek için bu ayarı seçmeniz gerekir.  

### <a name="site-system-installation-account"></a>Site sistemi yükleme hesabı

Site sunucusuna yüklenen dağıtım noktaları için, site sistemi yükleme hesabı olarak kullanılmak üzere yalnızca site sunucusunun bilgisayar hesabı desteklenir. Daha fazla bilgi için bkz. [hesaplar](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a>Kayıt noktası  

Kayıt noktaları, macOS bilgisayarlarını yüklemek ve şirket içi mobil cihaz yönetimi ile yönettiğiniz cihazları kaydetmek için kullanılır. Daha fazla bilgi için aşağıdaki makalelere bakın:  

- [Mac bilgisayarlara istemci dağıtma](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Kullanıcıların cihazları şirket içi MDM ile kaydetme şekli](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>İzin verilen bağlantılar

HTTPS ayarı otomatik olarak seçilir ve kayıt proxy noktası için sunucu kimlik doğrulaması ve SSL üzerinden verilerin şifrelenmesi için sunucuda bir PKI sertifikası gerektirir. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

Sunucu sertifikasının örnek dağıtımı ve IIS 'de nasıl yapılandırılacağı hakkında bilgi için bkz. [IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a>Kayıt proxy noktası  

Mobil cihazlar için bir kayıt proxy noktası ayarlama hakkında daha fazla bilgi için bkz. [kullanıcıların cihazları şirket ıçı MDM ile kaydetme şekli](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

### <a name="client-connections"></a>İstemci bağlantıları

HTTPS ayarı otomatik olarak seçilir. Sunucusunda aşağıdaki PKI sertifikalarının olması gerekir:

- Configuration Manager ile kaydolmalarınızın mobil cihazlara ve Mac bilgisayarlara sunucu kimlik doğrulaması için
- Güvenli Yuva Katmanı (SSL) üzerinden verilerin şifrelenmesi için

Sertifika gereksinimleri hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

Sunucu sertifikasının örnek dağıtımı ve IIS 'de nasıl yapılandırılacağı hakkında bilgi için bkz. [IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a>Geri dönüş durum noktası  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Durum iletilerinin sayısı ve kısıtlama aralığı (saniye)

Bu seçenekler için varsayılan ayarlar, 10.000 durum mesajlardır ve kısıtlama aralığı için 3.600 saniyedir. Bu ayarlar çoğu durumda yeterli olmakla birlikte, aşağıdaki koşulların her ikisi de doğru olduğunda bunları değiştirmeniz gerekebilir:  

- Geri dönüş durum noktası yalnızca intranetten gelen bağlantıları kabul eder.  

- Birçok bilgisayar için bir istemci dağıtımı dağıtımı sırasında geri dönüş durum noktasını kullanırsınız.  

Bu senaryoda sürekli bir durum iletileri akışı, site sunucusunda sürekli bir süre boyunca yüksek işlemci kullanımına neden olan bir durum iletileri biriktirme listesi oluşturabilir. Ayrıca, Configuration Manager konsolunda ve istemci dağıtım raporlarında istemci dağıtımı hakkında güncel bilgiler göremeyebilirsiniz.  

Bu geri dönüş durum noktası ayarları, istemci dağıtımı sırasında oluşturulan durum iletileri için ayarlanacak şekilde tasarlanmıştır. Internet üzerindeki istemciler Internet tabanlı yönetim noktasına bağlanamadığında olduğu gibi, ayarlar istemci iletişim sorunları için ayarlanacak şekilde tasarlanmamıştır. Geri dönüş durum noktası bu ayarları yalnızca istemci dağıtımı sırasında oluşturulan durum iletilerine uygulayamadığından, geri dönüş durum noktası internet 'ten gelen bağlantıları kabul ettiğinde bu ayarları yapılandırmayın.  

Configuration Manager istemcisini başarıyla yükleyen her bilgisayar, geri dönüş durum noktasına aşağıdaki dört durum iletisini gönderir:  

- İstemci dağıtımı başlatıldı  

- İstemci dağıtımı başarılı oldu  

- İstemci ataması başlatıldı  

- İstemci ataması başarılı oldu  

Yüklenemediği veya istemci Configuration Manager atayan bilgisayarlar ek durum iletileri gönderir.  

Örneğin, Configuration Manager istemcisini 20.000 bilgisayarlara dağıtırsanız, dağıtım geri dönüş durum noktasına 80.000 durum iletileri gönderebilir. Varsayılan azaltma yapılandırması 10.000 durum iletilerinin her 3.600 saniye (1 saat) geri dönüş durum noktasına gönderilmesine izin sağladığından, durum iletileri geri dönüş durum noktasında geri alınabilir duruma gelebilir. Ayrıca, geri dönüş durum noktası ve site sunucusu arasındaki kullanılabilir ağ bant genişliğini ve çok sayıda durum iletisini işlemek için site sunucusunun işlem gücünü göz önünde bulundurun.  

Bu sorunları önlemeye yardımcı olmak için durum iletilerinin sayısında bir artış ve kısıtlama aralığındaki bir azalma düşünün.  

Aşağıdaki koşullardan biri doğru olduğunda geri dönüş durum noktası için azaltma değerlerini sıfırlayın:  

- Geri dönüş durum noktasından durum iletilerini işlemek için geçerli kısıtlama değerlerinin gerekenden daha yüksek olduğunu hesaplayabilirsiniz.  

- Geçerli kısıtlama ayarlarının site sunucusunda yüksek işlemci kullanımı oluştur, olduğunu fark edersiniz.  

Sonuçları anlamadığınız müddetçe geri dönüş durum noktası kısıtlama ayarlarının ayarlarını değiştirmeyin. Örneğin, kısıtlama ayarlarını yüksek olarak artırdığınızda, site sunucusundaki işlemci kullanımı yüksek ve tüm site işlemlerini yavaşlamış olabilir.  
