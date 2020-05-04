---
title: İstemciler için site sistem rolleri
titleSuffix: Configuration Manager
description: Configuration Manager içindeki istemciler için site sistemi rollerini belirleme.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713250"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Configuration Manager istemcileri için site sistemi rollerini belirleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Configuration Manager istemcilerini dağıtmanız için ihtiyacınız olan site sistem rollerini belirlemenize yardımcı olabilir.

Bu rollerin hiyerarşide yükleneceği konum hakkında daha fazla bilgi için bkz. [site hiyerarşisi tasarlama](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

Bu rollerin nasıl yükleneceği ve yapılandırılacağı hakkında daha fazla bilgi için bkz. [site sistemi rollerini yüklemek](../../../servers/deploy/configure/install-site-system-roles.md).  

## <a name="management-point"></a>Yönetim noktası

Varsayılan olarak, tüm Windows istemci bilgisayarları Configuration Manager istemcisini yüklemek için bir dağıtım noktası kullanır. Bir dağıtım noktası kullanılamadığında bir yönetim noktasına geri dönebilirler. Ancak, CCMSetup komut satırı özelliğini `/source:<Path>`kullandığınızda, bilgisayarlara alternatif bir kaynaktan Windows istemcileri yükleyebilirsiniz. Örneğin, internet 'e istemcileri yüklüyorsanız bu eylemi gerçekleştirebilirsiniz. Diğer senaryo, istemci yüklemesi sırasında bilgisayar ve yönetim noktası arasında ağ paketleri gönderilmesini önlemek istediğinizde olur. Bu senaryo, bir güvenlik duvarının gerekli bağlantı noktalarını engellemesi veya düşük bant genişliğine sahip olmanız nedeniyle oluşur. Ancak, tüm istemcilerin bir siteye atanacak ve Configuration Manager tarafından yönetilmek üzere bir yönetim noktasıyla iletişim kurması gerekir.  

İstemci komut satırı özellikleri hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../about-client-installation-properties.md).  

Hiyerarşide birden fazla yönetim noktası yüklediğinizde istemciler, orman üyeliklerine ve ağ konumlarına göre tek bir noktaya otomatik olarak bağlanır. İkincil bir sitede birden fazla yönetim noktası yükleyemezsiniz.  

Configuration Manager ile kaydolmaettiğiniz Mac bilgisayar istemcileri ve mobil cihaz istemcileri, istemci yüklemesi için her zaman bir yönetim noktası gerektirir. Bu yönetim noktasının birincil sitede olması gerekir, mobil cihazları destekleyecek şekilde yapılandırılması ve Internet 'ten istemci bağlantılarını kabul etmesi gerekir. Bu istemciler ikincil sitelerdeki yönetim noktalarını kullanamaz veya diğer birincil sitelerdeki yönetim noktalarına bağlanabilir.  

## <a name="distribution-point"></a>Dağıtım noktası

Windows bilgisayarlarına Configuration Manager istemcileri yüklemek için bir dağıtım noktasına ihtiyacınız yoktur. Configuration Manager, varsayılan olarak, Windows bilgisayarlarına istemci kaynak dosyalarını yüklemek için bir dağıtım noktası kullanır. Bu dosyaları bir yönetim noktasından indirmeye geri dönebilirler. Dağıtım noktaları, Configuration Manager tarafından kaydedilen mobil cihaz istemcilerini yüklemek için kullanılmaz, ancak mobil cihaz eski istemcisini yüklerseniz kullanılır. Configuration Manager istemcisini bir işletim sistemi dağıtımının parçası olarak yüklerseniz, işletim sistemi görüntüsü bir dağıtım noktasından depolanır ve alınır.

Çoğu Configuration Manager istemcisini yüklemek için dağıtım noktalarına ihtiyaç duymasanız da, istemcilere uygulamalar ve yazılım güncelleştirmeleri gibi yazılımları yüklemek için bu istemcilere ihtiyacınız vardır.  

## <a name="fallback-status-point"></a>Geri dönüş durumu noktası

Windows bilgisayarlarına yönelik istemci dağıtımını izlemek için bir geri dönüş durum noktası kullanabilirsiniz. Ayrıca, bir yönetim noktasıyla iletişim kuramadığı için yönetilmeyen Windows bilgisayar istemcilerini de tanımlayabilirsiniz.

Aşağıdaki istemci türleri geri dönüş durumu noktası kullanmaz:

- Mac bilgisayarlar
- Configuration Manager tarafından kaydedilen mobil cihazlar
- Exchange Server bağlayıcısı kullanılarak yönetilen mobil cihazlar

İstemci etkinliğini ve istemci sistem durumunu izlemek için bir geri dönüş durum noktası gerekli değildir.  

Geri dönüş durum noktası her zaman, kimliği doğrulanmamış bağlantıları kullanan HTTP üzerinden istemcilerle iletişim kurar ve verileri şifresiz metin olarak gönderir. Bu davranış, özellikle de internet tabanlı istemci yönetimiyle kullanıldığında geri dönüş durum noktasının saldırıya açık olmasını sağlar. Saldırı yüzeyini azaltmaya yardımcı olmak için her zaman bir sunucuyu geri dönüş durum noktasını çalıştırmaya ayırabilirsiniz. Diğer site sistemi rollerini bir üretim ortamında aynı sunucuya yüklemeyin.  

Aşağıdaki koşulların tümü geçerliyse, bir geri dönüş durum noktası yükler:  

- Bu istemci bilgisayarlar bir yönetim noktasıyla iletişim kuramasa bile, Windows bilgisayarlarından gelen istemci iletişim hatalarının siteye gönderilmesini istersiniz.  

- Geri dönüş durum noktası tarafından gönderilen verileri görüntüleyen Configuration Manager istemci dağıtım raporlarını kullanmak istiyorsunuz.  

- Bu site sistem rolü için adanmış bir sunucunuz vardır ve sunucunun saldırıya karşı korunmasına yardımcı olmak için ek güvenlik önlemleri vardır.  

- Geri dönüş durum noktası kullanmanın avantajları, kimliği doğrulanmamış bağlantılarla ilişkili güvenlik risklerini ve HTTP trafiği üzerinden şifresiz metin aktarımlarını kapsar.  

Kimliği doğrulanmamış bağlantıları olan bir Web sitesini çalıştırmanın ve şifresiz metin aktarımlarının güvenlik riskleri, istemci iletişim sorunlarının tanımlanmasından faydalanır olursa geri dönüş durum noktası yüklemeyin.  

## <a name="reporting-services-point"></a>Raporlama hizmetleri noktası

Configuration Manager, istemcilerin yükleme, atama ve yönetimini Configuration Manager konsolunda izlemenize yardımcı olacak birçok rapor sağlar. İstemci dağıtım raporlarının bazıları istemcilerin bir geri dönüş durum noktasına atanmasını gerektirir.  

İstemcilerin dağıtılması için raporlara gerek yoktur. Configuration Manager konsolunda bazı dağıtım bilgilerini görebilir veya ayrıntılı bilgi için istemci günlük dosyalarını kullanabilirsiniz. Ancak, istemci raporları istemci dağıtımını izlemeye ve sorunlarını gidermenize yardımcı olmak için değerli bilgiler sağlar.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Kayıt noktası ve kayıt proxy noktası

Configuration Manager, kayıt noktasının ve kayıt proxy noktasının mobil cihazları kaydetmesini ve Mac bilgisayarlar için sertifikaları kaydetmesini gerektirir. Aşağıdaki durumlarda bu site sistem rollerine ihtiyacınız yoktur:

- Mobil cihazları Exchange Server bağlayıcısını kullanarak yönetmeyi planlarsınız
- Mobil cihaz eski istemcisini (örneğin, Windows CE) yüklersiniz
- Mac bilgisayarlara istemci sertifikasını Configuration Manager bağımsız olarak isteyin ve yüklersiniz

## <a name="application-catalog"></a>Uygulama Kataloğu

> [!Important]  
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Bulut yönetimi ağ geçidi bağlayıcı noktası

[Internet 'te istemcileri yönetmek](../../manage/manage-clients-internet.md)için bir [bulut yönetimi ağ geçidi](../../manage/cmg/plan-cloud-management-gateway.md) ayarlıyorsanız bir bulut yönetimi ağ geçidi bağlayıcı noktası gerekir.
