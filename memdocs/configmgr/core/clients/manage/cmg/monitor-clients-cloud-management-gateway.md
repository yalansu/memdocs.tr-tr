---
title: Bulut yönetimi ağ geçidini izleme
titleSuffix: Configuration Manager
description: Bulut yönetimi ağ geçidi (CMG) üzerinden istemcileri ve ağ trafiğini izleyin.
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714230"
---
# <a name="monitor-cloud-management-gateway"></a>Bulut yönetimi ağ geçidini izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bulut yönetimi ağ geçidi (CMG) çalışmaya başladıktan ve istemciler üzerinden bağlantı kurulduktan sonra, hizmetin nasıl çalıştığını bildiğinize emin olmak için istemcileri ve ağ trafiğini izleyebilirsiniz.


## <a name="monitor-clients"></a>İstemcileri izleme

CMG aracılığıyla bağlanan istemciler, Configuration Manager konsolunda, şirket içi istemcilerle aynı şekilde görünür. Daha fazla bilgi için bkz. [istemcileri izleme](../monitor-clients.md).


## <a name="monitor-traffic-in-the-console"></a>Konsolda trafiği izleme

Configuration Manager konsolunu kullanarak CMG 'deki trafiği izleyin:

1. **Yönetim** çalışma alanına gidin, **Cloud Services**öğesini genişletin ve **bulut yönetimi ağ geçidi** düğümünü seçin.  

2. Liste bölmesinde CMG 'yi seçin.  

3. CMG bağlantı noktası ve bağlandığı site sistem rolleri için Ayrıntılar bölmesinde trafik bilgilerini görüntüleyin. Bu istatistikler, bu rollere gelen istemci isteklerini gösterir. İstekler ilke, konum, kayıt, içerik, envanter ve istemci bildirimlerini içerir.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Giden trafik uyarılarını ayarlama

Giden trafik uyarıları, ağ trafiğinin 14 günlük eşik düzeyine yaklaşırsa emin olmanıza yardımcı olur. CMG 'yi oluştururken trafik uyarılarını ayarlayabilirsiniz. Bu bölümü atladıysanız, hizmet çalışmaya başladıktan sonra uyarıları ayarlamaya devam edebilirsiniz. Uyarı ayarlarını dilediğiniz zaman ayarlayın.

1. **Yönetim** çalışma alanına gidin, **Cloud Services**öğesini genişletin ve **bulut yönetimi ağ geçidi** düğümünü seçin.  

2. Liste bölmesinde CMG ' yi seçin ve ardından Şeritteki **Özellikler** ' i seçin.  

3. Eşiği ve uyarıları etkinleştirmek için **Uyarılar** sekmesine gidin. 14 günlük veri eşiğini gigabayt (GB) cinsinden belirtin. Ayrıca, farklı uyarı düzeylerini yükseltmek için eşik yüzdesini belirtin.  

4. İşiniz bittiğinde **Tamam**’ı seçin.  


## <a name="monitor-logs"></a>Günlükleri izleme

CMG, bir dizi günlük dosyasında giriş oluşturur. Daha fazla bilgi için bkz. [Configuration Manager günlükleri](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Bulut yönetimi panosu

<!--1358461-->
Sürüm 1806 ' den başlayarak, bulut yönetimi panosu CMG kullanımı için merkezi bir görünüm sağlar. Site, bulut yönetimi için [Azure hizmetlerine](../../../servers/deploy/configure/azure-services-wizard.md) eklendi, bulut kullanıcıları ve cihazları hakkındaki verileri de görüntüler.  

Aşağıdaki ekran görüntüsü, kullanılabilir kutucukların ikisini gösteren bulut yönetimi panosunun bir bölümüdür:  
![Bulut yönetimi Pano kutucukları CMG trafiği ve geçerli çevrimiçi istemcileri](media/1358461-cmg-dashboard.png)

Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Bulut yönetimi** düğümünü seçin ve Pano kutucuklarını görüntüleyin.  


## <a name="connection-analyzer"></a>Bağlantı çözümleyici

Sürüm 1806 ' den başlayarak, sorun gidermeye yardımcı olmak için CMG bağlantı çözümleyici 'yi gerçek zamanlı doğrulama için kullanın. Konsol içi yardımcı programı hizmetin geçerli durumunu ve CMG bağlantı noktası üzerinden gelen iletişim kanalını CMG trafiğine izin veren herhangi bir yönetim noktasına denetler.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Cloud Services** genişletin ve **bulut yönetimi ağ geçidi** düğümünü seçin.  

2. Hedef CMG örneğini seçin ve ardından şeritte **bağlantı Çözümleyicisi** ' ni seçin.  

3. CMG bağlantı çözümleyici penceresinde, hizmet ile kimlik doğrulamak için aşağıdaki seçeneklerden birini belirleyin:  

     1. **Azure AD kullanıcısı**: Azure AD 'ye katılmış bir Windows 10 cihazında oturum açmış bulut tabanlı bir kullanıcı kimliğiyle iletişimin benzetimini yapmak için bu seçeneği kullanın. Bu Azure AD Kullanıcı hesabının kimlik bilgilerini güvenli bir şekilde girmek için **oturum aç** ' a tıklayın.  

     2. **İstemci sertifikası**: [istemci kimlik doğrulama sertifikasıyla](certificates-for-cloud-management-gateway.md#bkmk_clientauth)Configuration Manager istemcisiyle aynı iletişimin benzetimini yapmak için bu seçeneği kullanın.  

4. Çözümlemeyi başlatmak için **Başlat** ' ı seçin. Çözümleyici penceresi sonuçları görüntüler. Açıklama alanında daha fazla ayrıntı görmek için bir giriş seçin.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a>Eşiği aştığında CMG 'yi durdur

<!--3735092-->
Sürüm 1902 ' den başlayarak, toplam veri aktarımı sınırınızı geçtiğinde artık Configuration Manager bir CMG hizmetini durdurabilir. Kullanım uyarı veya kritik düzeylere ulaştığında bildirimleri tetiklemek için [uyarıları](#set-up-outbound-traffic-alerts) kullanın. Kullanımda olan bir ani artış nedeniyle beklenmeyen Azure maliyetlerini azaltmaya yardımcı olmak için bu seçenek bulut hizmetini devre dışı bırakır.

> [!Important]  
> Hizmet çalışmıyor olsa bile, bulut hizmetiyle ilişkili maliyetler de vardır. Hizmetin durdurulması, ilişkili tüm Azure maliyetlerini ortadan kaldırmaz. Bulut hizmetinin tüm maliyetini kaldırmak için [CMG 'yi kaldırın](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> CMG hizmeti durdurulduğunda, internet tabanlı istemciler Configuration Manager ile iletişim kuramaz.  

Toplam veri aktarımı (çıkış), bulut hizmeti ve depolama hesabından alınan verileri içerir. Bu veriler aşağıdaki akışlardan gelir:

- CMG 'den istemciye  
- CMG günlük dosyaları dahil CMG-site  
- İçerik için CMG 'yi etkinleştirirseniz, depolama hesabını istemciye  

Bu veri akışları hakkında daha fazla bilgi için bkz. [CMG bağlantı noktaları ve veri akışı](plan-cloud-management-gateway.md#ports-and-data-flow).

Depolama uyarı eşiği ayrı. Bu uyarı, Azure depolama örneğinizin kapasitesini izler.

Konsolundaki **bulut yönetimi ağ geçidi** düğümünde CMG örneğini seçtiğinizde, Ayrıntılar bölmesinde toplam veri aktarımını görebilirsiniz.

Configuration Manager, her altı dakikada bir eşik değerini denetler. Kullanımda ani bir ani artış varsa, eşiğin aşıldığını algılamak ve sonra hizmeti durdurmak için Configuration Manager en fazla altı dakika sürebilir.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Bir eşiği aştığında bulut hizmetini durdurma işlemi

1. [Giden trafik uyarılarını ayarlayın](#set-up-outbound-traffic-alerts).  

2. CMG Özellikleri penceresinin **Uyarılar** sekmesinde, **kritik eşik aşıldığında bu hizmeti durdurma**seçeneğini etkinleştirin.  

Bu özelliği test etmek için aşağıdaki değerlerden birini geçici olarak daraltın:  

- **giden veri aktarımı için 14 günlük eşik (GB)**. Varsayılan değer: `10000`.  

- **Kritik uyarının tetikme eşiği yüzdesi**. Varsayılan değer: `90`.  
