---
title: İşletim sistemi dağıtımlarını izleme
titleSuffix: Configuration Manager
description: İşletim sistemi dağıtım nesnelerini izlemenize yardımcı olması için Configuration Manager konsolu, uyarılar, raporlar ve çeşitli durum göstergeleri sağlar.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9d0a430a1010611bc6a7e0871e8c59ca3d1f8de7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723834"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>Configuration Manager işletim sistemi dağıtımlarını izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolu, işletim sistemi dağıtım nesnelerini izlemenize yardımcı olmak için aşağıdaki yolları sağlar.  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> İşletim sistemi dağıtımları için uyarılar  
 Yazılım güncelleştirme dağıtımları için uyumluluk düzeyleri yapılandırılan yüzdenin altında olduğunda yönetici kullanıcıları bilgilendirmek üzere görev dizisi dağıtım ayarlarında bir uyarı yapılandırabilirsiniz.  

 Uyarı ayarlarını yapılandırdıktan sonra, belirtilen koşullar gerçekleşirse Configuration Manager bir uyarı oluşturulur. Görev dizisi dağıtım uyarılarını aşağıdaki konumlarda inceleyebilirsiniz:  

1.  Son uyarıları, **Yazılım Kitaplığı** çalışma alanındaki **İşletim Sistemleri** düğümünde gözden geçirin.  

2.  Yapılandırılmış uyarıları **İzleme** çalışma alanının **Uyarılar** düğümünde yönetin.  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a>Görev dizisi dağıtım durumu  
 Bir görev dizisini dağıttıktan sonra dağıtım durumunu izleyebilirsiniz. Bir görev dizisinin dağıtım durumunu izlemek üzere aşağıdaki prosedürü kullanın.  

#### <a name="to-monitor-deployment-status"></a>Dağıtım durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  İzleme çalışma alanında, **Dağıtımlar**'a tıklayın.  

3.  Dağıtım durumunu izlemek istediğiniz görev dizisini tıklatın.  

4.  **Giriş** sekmesinde **Dağıtım** grubunda, **Durumu Görüntüle**'yi tıklatın.  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a> İşletim sistemi dağıtım raporları  
 Çok sayıda önceden tanımlanmış işletim sistemi dağıtımı raporu bulunur. Bunlar, çeşitli kategorilerde organize edilmiştir ve durum geçişi ile görev dizisi dağıtımına ilişkin belirli bilgileri raporlamak için kullanılabilir. Önceden yapılandırılmış raporları kullanmanın yanı sıra, kurumunuzun ihtiyaçlarına göre özel yazılım güncelleştirme raporları da oluşturabilirsiniz. Daha fazla bilgi için bkz. [Raporlama Için işlemler ve bakım](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>İçeriği izle  
 Tüm paket türlerinin durumunu ilişkili dağıtım noktalarıyla ilişkili olarak gözden geçirmek için Configuration Manager konsolundaki içeriği izleyebilirsiniz. Bu, paket içeriğin içerik doğrulama durumunu, belirli bir dağıtım noktası grubuna atanmış içerik durumunu, dağıtım noktasına atanmış içeriğin durumunu ve her dağıtım noktası için isteğe bağlı özelliklerin durumunu içerebilir (içerik doğrulama, PXE ve çok noktaya yayın).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a>İçerik durumu izleme  
 **İzleme** çalışma alanındaki **İçerik Durumu** düğümü, içerik paketleri hakkında bilgi sağlar. Paket, paketin dağıtım durumu ve paket hakkındaki ayrıntılı durum bilgisine dair genel bilgileri gözden geçirebilirsiniz. İçerik durumunu görüntülemek için aşağıdaki prosedürü kullanın.  

#### <a name="to-monitor-content-status"></a>İçerik durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  İzleme çalışma alanında **Dağıtım Durumu**'nu genişletin ve **İçerik Durumu**'na tıklayın. Paketler görüntülenir.  

3.  Ayrıntılı durum bilgisinin görüntüleneceği paketi seçin.  

4.  **Giriş** sekmesinde, **Yeni Durum**'a tıklayın. Paket için ayrıntılı durum bilgisi görüntülenir.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Dağıtım noktası grubu durumu  
 **İzleme** çalışma alanındaki **Dağıtım Noktası Grubu Durumu** düğümü, dağıtım noktası grupları hakkında bilgi sağlar. Dağıtım noktası grup durumu ve uyumluluk oranının yanı sıra, dağıtım noktası grubu ayrıntılı durum bilgisi gibi dağıtım noktası grubuna ilişkin genel bilgileri gözden geçirebilirsiniz. Dağıtım noktası grubu durumunu görüntülemek için aşağıdaki yordamı kullanın.  

#### <a name="to-monitor-distribution-point-group-status"></a>Dağıtım noktası grubu durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  İzleme çalışma alanında **Dağıtım Durumu**'nu genişletin ve ardından **Dağıtım Noktası Grup Durumu**'na tıklayın. Dağıtım noktası grupları görüntülenir.  

3.  Ayrıntılı durum bilgisinin görüntüleneceği dağıtım noktası grubunu seçin.  

4.  **Giriş** sekmesinde, **Yeni Durum**'a tıklayın. Dağıtım noktası grubu için ayrıntılı durum bilgileri görüntülenir.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Dağıtım noktası yapılandırma durumu  
 **İzleme** çalışma alanındaki **Dağıtım Noktası Yapılandırma Durumu** düğümü, dağıtım noktası hakkında bilgi sağlar. Dağıtım noktası için hangi özniteliklerin etkinleştirildiğini gözden geçirebilirsiniz, örneğin PXE, Çok noktaya yayın ve içerik doğrulama. Dağıtım noktası için ayrıntılı durum bilgisini de görüntüleyebilirsiniz. Dağıtım noktası yapılandırma durumunu görüntülemek için aşağıdaki yordamı kullanın.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Dağıtım noktası yapılandırma durumunu izlemek için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  İzleme çalışma alanında **Dağıtım Durumu**'nu genişletin ve ardından **Dağıtım Noktası Yapılandırma Durumu**'na tıklayın. Dağıtım noktaları görüntülenir.  

3.  Dağıtım noktası durum bilgisinin görüntüleneceği dağıtım noktasını seçin.  

4.  Sonuçlar bölmesinde **Ayrıntılar** sekmesine tıklayın. dağıtım noktası için durum bilgileri görüntülenir.  
