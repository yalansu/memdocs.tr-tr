---
title: İçeriği izleme
titleSuffix: Configuration Manager
description: Configuration Manager konsolunu kullanarak dağıtılmış içeriği nasıl izleyeceğinizi anlayın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110024"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Configuration Manager ile dağıttığınız içeriği izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Dağıtılmış içeriği izlemek için Configuration Manager konsolunu kullanın, örneğin:  

- İlişkili dağıtım noktaları için tüm paket türlerinin durumu.  
- Bir paketteki içerik için içerik doğrulama durumu.  
- Belirli bir dağıtım noktası grubuna atanan içeriğin durumu.  
- Bir dağıtım noktasına atanan içeriğin durumu.  
- Her dağıtım noktası için isteğe bağlı özelliklerin durumu (içerik doğrulama, PXE ve çok noktaya yayın).  

> [!NOTE]  
> Configuration Manager yalnızca içerik kitaplığındaki bir dağıtım noktasındaki içeriği izler. Paket veya özel paylaşımlardaki dağıtım noktasında depolanan içeriği izlemez.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a>İçerik durumu izleme

**İzleme** çalışma alanındaki **İçerik Durumu** düğümü, içerik paketleri hakkında bilgi sağlar. Configuration Manager konsolunda, şunun gibi bilgileri gözden geçirin:  

- Paket adı, türü ve KIMLIĞI
- Bir paketin kaç dağıtım noktasına gönderildiği
- Uyumluluk oranı
- Paket oluşturulduğunda
- Kaynak sürümü

Aşağıdakiler de dahil olmak üzere herhangi bir paket için ayrıntılı durum bilgileri bulabilirsiniz:  

- Dağıtım durumu
- Başarısızlık sayısı
- Bekleyen dağıtımlar  
- Yükleme sayısı

Ayrıca, bir dağıtım noktasına sürmekte olan veya bir dağıtım noktasına başarıyla içerik dağıtabilecek dağıtımları da yönetebilirsiniz:  

- **Varlık ayrıntıları** bölmesindeki bir dağıtım noktasına dağıtım işinin dağıtım durumu iletisini görüntülediğinizde içeriği iptal etme veya yeniden dağıtma seçeneği kullanılabilir. Bu bölme, **devam eden** sekmesinde ya da **Içerik durumu** düğümünün **hata** sekmesinde bulunabilir.  
- Ayrıca, iş ayrıntıları **devam eden** sekmesinde bir işin ayrıntılarını görüntülediğinizde tamamlanan işin yüzdesini görüntüler. İş ayrıntıları, bir iş için kalan yeniden deneme sayısını da görüntüler. **Hata** sekmesinde bir işin ayrıntılarını görüntülediğinizde, bir sonraki yeniden deneme işleminin ne kadar süre önce gerçekleşeceğini gösterir.  

Henüz tamamlanmamış bir dağıtımı iptal ettiğinizde, içeriğin aktarılacağı dağıtım işi şu şekilde sona erer:  

- Dağıtım durumu bundan sonra, dağıtımın başarısız olduğunu ve bir kullanıcı eylemi tarafından iptal edildiğini göstermek için güncellenir.  
- Bu yeni durum **hata** sekmesinde görüntülenir.  

> [!NOTE]  
> Bir dağıtım tamamlandığında, dağıtım noktasındaki dağıtım tamamlanmadan önce bu dağıtımı iptal etme eylemi bu işlemden sonra gerçekleştirilemez. Bu gerçekleştiğinde, dağıtımı iptal etme eylemi yok sayılır ve dağıtım durumu başarılı olarak görüntülenir.  
>
> Site sunucusunda bulunan bir dağıtım noktasına bir dağıtımı iptal etme seçeneğini belirleyebilirsiniz, ancak bu, hiçbir etkiye sahip değildir. Bu davranış, site sunucusunun ve site sunucusundaki dağıtım noktasının aynı tek örnekli içerik deposunu paylaştığı bir davranıştır. İptal edilecek gerçek bir dağıtım işi yok.  

Daha önce bir dağıtım noktasına aktarılamayan içeriği yeniden dağıttığınızda, Configuration Manager hemen bu içeriği dağıtım noktasına dağıtmaya başlar. Configuration Manager, yeniden dağıtımın devam eden durumunu yansıtmak için dağıtımın durumunu güncelleştirir.  

### <a name="tasks-to-monitor-content"></a>İçeriği izlemek için görevler

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümünü seçin. Bu düğüm paketleri görüntüler.  

2. Yönetmek istediğiniz paketi seçin.  

3. Şeridin **giriş** sekmesinde, **Içerik** grubunda, **durumu görüntüle**' yi seçin. Konsol, paket için ayrıntılı durum bilgilerini görüntüler.

Ek eylemler için aşağıdaki bölümlerden birine geçin:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Devam eden bir dağıtımı iptal etme  

1. **Devam eden** sekmesine geçin.

2. **Varlık ayrıntıları** bölmesinde, iptal etmek istediğiniz dağıtımın girişine sağ tıklayın ve **iptal**' i seçin.  

3. Eylemi onaylamak için **Evet** ' i seçin ve dağıtım işini söz konusu dağıtım noktasına iptal edin.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Dağıtım başarısız olan içeriği yeniden dağıtma  

1. **Hata** sekmesine geçin.

2. **Varlık ayrıntıları** bölmesinde, yeniden dağıtmak istediğiniz dağıtımın girişine sağ tıklayın ve yeniden **Dağıt**' ı seçin.  

3. Eylemi doğrulamak ve bu dağıtım noktasına yeniden dağıtım işlemini başlatmak için **Evet** ' i seçin.  


## <a name="distribution-point-group-status"></a> Dağıtım noktası grubu durumu

**İzleme** çalışma alanındaki **Dağıtım Noktası Grubu Durumu** düğümü, dağıtım noktası grupları hakkında bilgi sağlar. Şunun gibi bilgileri gözden geçirebilirsiniz:  

- Dağıtım noktası Grup adı, açıklaması ve durumu
- Dağıtım noktası grubuna kaç tane dağıtım noktası üye?
- Gruba kaç paket atandı
- Uyumluluk oranı

Aşağıdaki ayrıntılı durum bilgilerini de görüntüleyebilirsiniz:  

- Dağıtım noktası grubu hataları  
- Kaç dağıtım sürüyor
- Kaç tane başarıyla dağıtıldı  

### <a name="monitor-distribution-point-group-status"></a>Dağıtım noktası grubu durumunu izleme  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **dağıtım durumu**' nu genişletin ve ardından **dağıtım noktası Grup durumu** düğümünü seçin. Dağıtım noktası gruplarını görüntüler.  

2. Ayrıntılı durum bilgilerini istediğiniz dağıtım noktası grubunu seçin.  

3. Şeridin **giriş** sekmesinde, **durumu görüntüle**' yi seçin. Dağıtım noktası grubu için ayrıntılı durum bilgilerini görüntüler.  


## <a name="distribution-point-configuration-status"></a>Dağıtım noktası yapılandırma durumu

**İzleme** çalışma alanındaki **Dağıtım Noktası Yapılandırma Durumu** düğümü, dağıtım noktası hakkında bilgi sağlar. Dağıtım noktası için hangi özniteliklerin etkinleştirildiğini gözden geçirebilirsiniz, örneğin PXE, çok noktaya yayın, içerik doğrulama. Ayrıca dağıtım noktası için dağıtım durumunu gözden geçirin.

> [!WARNING]  
> Dağıtım noktası yapılandırma durumu, son 24 saate göredir. Dağıtım noktasında bir hata varsa ve kurtarıldığında, dağıtım noktası kurtarıldığında hata durumu 24 saate kadar görüntülenebilir.  

### <a name="monitor-distribution-point-configuration-status"></a>Dağıtım noktası yapılandırma durumunu izleme  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **dağıtım durumu**' nu genişletin ve ardından **dağıtım noktası yapılandırma durumu** düğümünü seçin.  

2. Bir dağıtım noktası seçin.  

3. Sonuçlar bölmesinde, **Ayrıntılar** sekmesine geçin. Dağıtım noktası için durum bilgilerini görüntüler.  


## <a name="client-data-sources-dashboard"></a>İstemci veri kaynakları panosu

İstemcilerin ortamınızda içerik aldığı yeri daha iyi anlamak için **Istemci veri kaynakları** panosunu kullanın. Pano, istemci içeriği indirdikten sonra verileri görüntülemeye başlar ve bu bilgileri siteye geri bildirir. Bu işlem, 24 saate kadar sürebilir.

> [!Note]  
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Kullanmadan önce **Istemci eş önbelleği** özelliğini etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../manage/install-in-console-updates.md#bkmk_options).  

Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **dağıtım durumu**' nu genişletin ve **istemci veri kaynakları** düğümünü seçin. Panoya uygulanacak bir zaman aralığı seçin. Ardından, bilgilerini görüntülemek istediğiniz sınır grubunu seçin. Farklı içerik veya ilke kaynakları hakkında daha fazla ayrıntı görmek için farenizi kutucukların üzerine getirebilirsiniz.

Ayrıca, her sınır grubu için istemci veri kaynaklarının bir özetini görüntülemek için, **Istemci veri kaynakları-özetleme**raporunu kullanın.

### <a name="dashboard-tiles"></a>Pano kutucukları

Pano aşağıdaki kutucukları içerir:  

#### <a name="client-content-sources"></a>İstemci Içerik kaynakları

İstemcilerin içerik aldığı kaynakları görüntüler:

- Dağıtım noktası
- [Bulut dağıtım noktası](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Eş önbellek](../../../plan-design/hierarchy/client-peer-cache.md)
- [Teslim iyileştirme](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (sürüm 1906 ' den başlayarak)<sup>[1. nota](#bkmk_note1)</sup>
- Microsoft Update: cihazlar, Configuration Manager istemcisi Microsoft bulut hizmetleri 'nden yazılım güncelleştirmelerini indirdiğinde bu kaynağı raporlar. Bu hizmetler, Enterprise için Microsoft Update ve Microsoft 365 uygulamalarını içerir.

![Panodaki istemci Içerik kaynakları kutucuğu](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> 1906 sürümünden başlayarak<!--3555759-->Bu panoya teslim Iyileştirmesi eklemek için aşağıdaki eylemleri yapın:
>
> - İstemci ayarını yapılandırın, yazılım güncelleştirmeleri grubundaki **Istemcilerde hızlı güncelleştirme yüklemesini etkinleştirin**
>
> - Windows 10 Express güncelleştirmelerini dağıtma
>
> Daha fazla bilgi için bkz. [Windows 10 güncelleştirmeleri Için hızlı yükleme dosyalarını yönetme](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Dağıtım noktaları

Seçilen sınır grubunun parçası olan dağıtım noktalarının sayısını görüntüler.

#### <a name="clients-that-used-a-distribution-point"></a>Bir dağıtım noktası kullanan istemciler

Seçilen sınır grubunda olan istemci sayısı bu kutucuk, içerik almak için kaç tane kullanılmış bir dağıtım noktası kullanıldığını gösterir.

#### <a name="peer-cache-sources"></a>Eş önbellek kaynakları

Seçilen sınır grubu için bu kutucuk, kaç tane eş önbellek kaynağının indirme geçmişi raporladığını gösterir.

#### <a name="clients-that-used-a-peer"></a>Bir eş kullanan istemciler

Seçilen sınır grubunda olan istemci sayısı bu kutucuk, içerik almak için kaç tane eş önbellek kaynağı kullanıldığını gösterir.

#### <a name="top-distributed-content"></a>En yüksek dağıtılmış Içerik

Kaynak türüne göre en çok dağıtılan paketler
