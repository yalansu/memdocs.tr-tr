---
title: Yazılım güncelleştirmelerini izleme
titleSuffix: Configuration Manager
description: Configuration Manager konsolu, güncelleştirmeleri ve uyumluluğu izlemeye yönelik uyarılar ve durumlar sağlar.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110381"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Configuration Manager yazılım güncelleştirmelerini izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, yazılım güncelleştirme nesnelerini, süreçlerini ve uyumluluk bilgilerini izlemenize yardımcı olmak için birçok yol sunar. Yazılım güncelleştirmelerini izlemek için aşağıdaki bölümleri kullanın.

## <a name="software-updates-dashboard"></a>Yazılım güncelleştirmeleri panosu

*(Sürüm 1610 ' de tanıtılmıştır)*

Configuration Manager sürüm 1610 ' den başlayarak, kuruluşunuzdaki cihazların geçerli uyumluluk durumunu görüntülemek için yazılım güncelleştirmeleri panosunu kullanabilir ve hangi cihazların risk altında olduğunu görmek için verileri hızlıca çözümleyebilirsiniz. Panoyu görüntülemek için **izleme** > **genel bakış** > **güvenlik** > **yazılım güncelleştirmeleri panosuna**gidin.

## <a name="drill-through-required-updates"></a>Gerekli güncelleştirmeler arasında detaya gitme
<!--4224414-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Hangi cihazların belirli bir Microsoft 365 Apps yazılım güncelleştirmesi gerektirdiğini görmek için uyumluluk istatistikleri detayına gidebilirsiniz. Cihaz listesini görüntülemek için, cihazların ait olduğu güncelleştirmeleri ve koleksiyonları görüntülemek için izninizin olması gerekir. Cihaz listesinin detayına gitmek için:

1. Yazılım **kitaplığı** > **yazılım** > güncelleştirmeleri**tüm yazılım güncelleştirmeleri**' ne gidin.
1. En az bir cihaz için gerekli olan herhangi bir güncelleştirmeyi seçin.
1. **Özet** sekmesine bakın ve **İstatistikler**altında Pasta grafiğini bulun.
1. Cihaz listesinin detayına gitmek için pasta grafiğinin yanındaki **gereken köprüyü görüntüle** ' yi seçin.
1. Bu eylem sizi, güncelleştirme gerektiren cihazları görebileceğiniz **cihazlarda** geçici bir düğüme götürür. Ayrıca, bir düğüm için, listeden yeni koleksiyon oluşturma gibi işlemler gerçekleştirebilirsiniz.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a>Yazılım güncelleştirme uyarıları  
 Yazılım güncelleştirmeleri uyarılarını, yazılım güncelleştirme dağıtımları için uyumluluk düzeyleri yapılandırılan yüzdenin altında olduğunda yönetici kullanıcıları bilgilendirmek üzere yapılandırabilirsiniz. Yazılım güncelleştirme dağıtımları uyarını aşağıdaki konumlarda yapılandırabilirsiniz:  

-   ADR ayarı: Uyarı ayarlarını Otomatik Dağıtım Kuralı Sihirbazında ve ADR özelliklerinde yapılandırabilirsiniz.  

-   Dağıtım ayarı: Uyarı ayarlarını Yazılım Güncelleştirmelerini Dağıt Sihirbazında ve dağıtım özelliklerinde yapılandırabilirsiniz.  

Uyarı ayarlarını yapılandırdıktan sonra, belirtilen koşullar gerçekleşirse Configuration Manager bir uyarı oluşturulur. Yazılım güncelleştirme uyarını aşağıdaki konumlarda gözden geçirebilirsiniz:  

1.  Son uyarıları, **Yazılım Kitaplığı** çalışma alanındaki **Yazılım Güncelleştirme** düğümünde gözden geçirin.  

2.  Yapılandırılmış uyarıları **İzleme** çalışma alanının **Uyarılar** düğümünde yönetin.  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a>Yazılım güncelleştirmeleri eşitleme durumu  
 Eşitleme işlemini başlattıktan sonra, hiyerarşinizdeki tüm yazılım güncelleştirme noktaları için Configuration Manager konsolundan eşitleme işlemini izleyebilirsiniz. Yazılım güncelleştirme eşitlemesini izlemek için aşağıdaki prosedürü kullanın.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Yazılım güncelleştirmeleri eşitleme işlemini izlemek için  

- Configuration Manager konsolunda, **izleme** > **genel bakış** > **yazılım güncelleştirme noktası eşitleme durumu**' na gidin.  

    Configuration Manager hiyerarşinizdeki yazılım güncelleştirme noktaları sonuçlar bölmesinde görüntülenir. Bu görünümden, tüm yazılım güncelleştirme noktalarının eşitleme durumunu izleyebilirsiniz. Eşitleme işlemi hakkında daha ayrıntılı bilgi için, her site sunucusunda <*Configmgrınstallationpath*> \logs dizininde bulunan wsyncmgr. log dosyasını gözden geçirebilirsiniz.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a>Yazılım güncelleştirmesi dağıtım durumu  
 Yazılım güncelleştirmelerini bir yazılım güncelleştirme grubuna dağıttıktan veya bağımsız bir yazılım güncelleştirmesi dağıttıktan sonra, dağıtım durumunu izleyebilirsiniz. Bir yazılım güncelleştirme grubu veya yazılım güncelleştirmesi için dağıtım durumunu izlemek üzere aşağıdaki prosedürü kullanın.  

#### <a name="to-monitor-deployment-status"></a>Dağıtım durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme** > **genel bakış** > **dağıtımlar**' a gidin.  

2.  Dağıtım durumunu izlemek istediğiniz yazılım güncelleştirme grubunu veya yazılım güncelleştirmesine tıklayın.  

3.  **Giriş** sekmesinde **Dağıtım** grubunda, **Durumu Görüntüle**'yi tıklatın.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Yazılım güncelleştirme raporları  
 Yazılım güncelleştirmelerine yönelik durum iletileri, yazılım güncelleştirmelerinin uyumluluğu ve yazılım güncelleştirme dağıtımlarının değerlendirilmesi ve uygulanma durumu hakkında bilgi verir. Yazılım güncelleştirme raporlarını çalıştırarak bu durum iletilerini görüntüleyebilirsiniz. 30'dan fazla öntanımlı yazılım güncelleştirme raporu bulunur. Bunlar, çeşitli kategorilerde düzenlenirler ve yazılım güncelleştirmeleri ve dağıtımlarıyla ilgili belirli bilgileri raporlamak için kullanılabilir. Önceden yapılandırılmış raporları kullanmanın yanı sıra, kurumunuzun ihtiyaçlarına göre özel yazılım güncelleştirme raporları da oluşturabilirsiniz. Daha fazla bilgi için bkz. [Raporlama Için işlemler ve bakım](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Önerilen yazılım güncelleştirmeleri raporları
Aşağıdakiler, olası sorunları belirlemek için yararlı olan raporlardan bazılarıdır: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Uyumluluk 9-genel durum ve uyumluluk (sürüm 1806 ' den başlayarak)
Rapor aşağıdaki bölümleri içerir:

- **Sağlıklı istemciler ve toplam istemci**sayısı: Bu çubuk grafik, belirtilen dönemde siteyle iletişim kurulan "sağlıklı" istemcileri, belirtilen koleksiyondaki toplam istemci sayısına göre karşılaştırır.
- **Uyumluluk genel bakış**: Bu pasta grafik, belirtilen koleksiyondaki etkin istemcilerde belirli yazılım güncelleştirme grubu için genel uyumluluk durumunu gösterir.
- **Önde gelen 5 makale kimliğiyle uyumlu değil**: Bu çubuk grafik, belirtilen koleksiyondaki etkin istemcilerde uyumsuz olmayan, belirtilen gruptaki ilk beş yazılım güncelleştirmesini görüntüler.
- Raporun en altında, belirtilen gruptaki yazılım güncelleştirmelerini listeleyen daha fazla ayrıntı içeren bir tablo bulunur.

#### <a name="management-2---updates-required-but-not-deployed"></a>Yönetim 2 - Güncelleştirme gerekiyor, ancak dağıtılmadı

Bu rapor, istemcilerde gerekli olarak algılanan ancak belirli bir koleksiyona dağıtılmamış belirli bir güncelleştirme sınıflandırmasında satıcıya özgü yazılım güncelleştirmelerini görüntüler. 

#### <a name="troubleshooting-2---deployment-errors"></a>Sorun giderme 2-dağıtım hataları

Bu rapor, sitedeki dağıtım hatalarını ve her hata yaşayan bilgisayar sayısını döndürür. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>İçeriği izle  
 Tüm paket türlerinin durumunu ilişkili dağıtım noktalarıyla ilişkili olarak gözden geçirmek için Configuration Manager konsolundaki içeriği izleyebilirsiniz. Bu, paket içeriğin içerik doğrulama durumunu, belirli bir dağıtım noktası grubuna atanmış içerik durumunu, dağıtım noktasına atanmış içeriğin durumunu ve her dağıtım noktası için isteğe bağlı özelliklerin durumunu içerebilir (içerik doğrulama, PXE ve çok noktaya yayın).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a>İçerik durumu izleme  
 **İzleme** çalışma alanındaki **İçerik Durumu** düğümü, içerik paketleri hakkında bilgi sağlar. Paket, paketin dağıtım durumu ve paket hakkındaki ayrıntılı durum bilgisine dair genel bilgileri gözden geçirebilirsiniz. İçerik durumunu görüntülemek için aşağıdaki prosedürü kullanın.  

#### <a name="to-monitor-content-status"></a>İçerik durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme** > **genel bakış** > **dağıtım durumu** > **İçerik durumu**' na gidin. Paketler görüntülenir.  

2.  Ayrıntılı durum bilgisinin görüntüleneceği paketi seçin.  

3.  **Giriş** sekmesinde, **Yeni Durum**'a tıklayın. Paket için ayrıntılı durum bilgisi görüntülenir.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Dağıtım noktası grubu durumu  
 **İzleme** çalışma alanındaki **Dağıtım Noktası Grubu Durumu** düğümü, dağıtım noktası grupları hakkında bilgi sağlar. Dağıtım noktası grup durumu ve uyumluluk oranının yanı sıra, dağıtım noktası grubu ayrıntılı durum bilgisi gibi dağıtım noktası grubuna ilişkin genel bilgileri gözden geçirebilirsiniz. Dağıtım noktası grubu durumunu görüntülemek için aşağıdaki yordamı kullanın.  

#### <a name="to-monitor-distribution-point-group-status"></a>Dağıtım noktası grubu durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme** > **genel bakış** > **dağıtım durumu** > **dağıtım noktası Grup durumu**' na gidin. Dağıtım noktası grupları görüntülenir.  

2.  Ayrıntılı durum bilgisinin görüntüleneceği dağıtım noktası grubunu seçin.  

3.  **Giriş** sekmesinde, **Yeni Durum**'a tıklayın. Dağıtım noktası grubu için ayrıntılı durum bilgileri görüntülenir.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Dağıtım noktası yapılandırma durumu  
 **İzleme** çalışma alanındaki **Dağıtım Noktası Yapılandırma Durumu** düğümü, dağıtım noktası hakkında bilgi sağlar. Dağıtım noktası için hangi özniteliklerin etkinleştirildiğini gözden geçirebilirsiniz, örneğin PXE, Çok noktaya yayın ve içerik doğrulama. Dağıtım noktası için ayrıntılı durum bilgisini de görüntüleyebilirsiniz. Dağıtım noktası yapılandırma durumunu görüntülemek için aşağıdaki yordamı kullanın.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Dağıtım noktası yapılandırma durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme** > **genel bakış** > **dağıtım durumu** > **dağıtım noktası yapılandırma durumu**' na gidin. Dağıtım noktaları görüntülenir.  

2.  Dağıtım noktası durum bilgisinin görüntüleneceği dağıtım noktasını seçin.  

3.  Sonuçlar bölmesinde **Ayrıntılar** sekmesine tıklayın. dağıtım noktası için durum bilgileri görüntülenir.  

## <a name="next-steps"></a>Sonraki adımlar

- [Yazılım güncelleştirmeleri için günlük dosyaları](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Yazılım güncelleştirme yönetimi teknik incelemesi](https://www.microsoft.com/download/confirmation.aspx?id=44578)
