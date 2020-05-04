---
title: İstemcileri engelleme
titleSuffix: Configuration Manager
description: Configuration Manager kullanarak sistem güvenliği için istemci erişimini engelleyin.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713243"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Configuration Manager istemcilerin engellenip engellenmeyeceğini belirleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemci bilgisayara veya istemci mobil cihaza artık güvenilmiyorsa, System Center 2012 Configuration Manager konsolundaki istemciyi engelleyebilirsiniz. Engellenen istemciler, ilke indirmek, envanter verileri yüklemek veya durum mesajları göndermek üzere site sistemleriyle iletişim kurabilmesi için Configuration Manager altyapısı tarafından reddedilir.  

 İstemciyi ikincil bir siteden veya merkezi yönetim sitesinden değil atandığı siteden engellemeniz ya da engelini kaldırmanız gerekir.  

> [!IMPORTANT]  
>  Configuration Manager engelleme, Configuration Manager sitesinin güvenliğini sağlamaya yardımcı olabilse de, engellenen bir istemci siteye otomatik olarak imzalanan yeni bir sertifika ve donanım KIMLIĞIYLE yeniden katılabildiğinden, istemcilerin HTTP kullanarak site sistemleriyle iletişim kurmasına izin verirseniz, siteyi güvenilmeyen bilgisayarlardan veya mobil cihazlardan korumak için bu özelliğe güvenmeyin. Onun yerine, işletim sistemlerini dağıtmak için kullandığınız kayıp veya güvenliği aşılmış önyükleme medyasını engellemek için ve site sistemleri HTTPS istemci bağlantılarını kabul ediyorsa engelleme özelliğini kullanın.  

 Siteye ISV Proxy sertifikasını kullanarak erişen istemciler engellenemez. ISV proxy sertifikası hakkında daha fazla bilgi için Configuration Manager yazılım geliştirme kiti 'Ne (SDK) bakın.  

 Site sistemleriniz HTTPS istemci bağlantılarını kabul ediyor ve ortak anahtar altyapınız (PKI) sertifika iptal listesini (CRL) destekliyorsa sertifika iptalini daima, riskli olabilecek sertifikalara karşı birincil savunma hattı olarak değerlendirin. Configuration Manager istemcilerin engellenmesi, hiyerarşinizi korumak için ikinci bir savunma hattı sunar.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> İstemcileri engellemede göz önüne alınacaklar  

-   Bu seçenek, HTTP ve HTTPS istemci bağlantılarında kullanılabilir, ancak istemciler site sistemlerine HTTP kullanarak bağlandığında güvenliği sınırlıdır.  

-   Configuration Manager yönetici kullanıcıların bir istemciyi engelleme yetkisi vardır ve bu eylem Configuration Manager konsolunda gerçekleştirilir.  

-   İstemci iletişimi yalnızca Configuration Manager hiyerarşisinden reddedilir.  

    > [!NOTE]  
    >  Aynı istemci farklı bir Configuration Manager hiyerarşisine kaydoar.  

-   İstemci Configuration Manager sitesinden hemen engellenir.  

-   Site sistemlerini riskli olabilecek bilgisayarlardan ve mobil cihazlardan korumaya yardımcı olur.  

## <a name="considerations-for-using-certificate-revocation"></a>Sertifika iptalinde göz önüne alınacaklar  

-   Bu seçenek, ortak anahtar altyapısı (PKI) bir sertifika iptal listesini (CRL) destekliyorsa, HTTPS Windows istemci bağlantılarında kullanılabilir.  

     Mac istemcileri her zaman CRL denetimi yapar ve bu işlev devre dışı bırakılamaz.  

     Mobil cihaz istemcileri site sistemlerine yönelik sertifikaları denetlemek için sertifika iptal listelerini kullanmasa da, sertifikaları Configuration Manager tarafından iptal edilebilir ve denetlenebilir.  

-   Ortak anahtar altyapısı yöneticilerinin bir sertifikayı iptal etme yetkisi vardır ve bu eylem Configuration Manager konsolunun dışında gerçekleştirilir.  

-   İstemci iletişimi, bu istemci sertifikasını gerektiren herhangi bir bilgisayardan veya mobil cihazdan reddedilebilir.  

-   Bir sertifikayı iptal etme ile değiştirilmiş sertifika iptal listesini (CRL) site sistemlerinin indirmesi arasında bir gecikme olması muhtemeldir.  

-   Birçok PKI dağıtımında, bu gecikme bir gün veya daha uzun sürebilir. Örneğin, Active Directory Sertifika Hizmetlerinde, varsayılan sona erme süresi tam CRL için bir hafta, fark CRL'si için ise bir gündür.  

-   Site sistemlerini ve istemcileri riskli olabilecek bilgisayarlardan ve mobil cihazlardan korumaya yardımcı olur.  

    > [!NOTE]  
    >  Ayrıca, IIS'de sertifika güven listesi (CTL) yapılandırarak IIS çalıştıran site sistemlerini bilinmeyen istemcilerden koruyabilirsiniz.  
