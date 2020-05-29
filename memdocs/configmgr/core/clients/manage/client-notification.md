---
title: İstemci bildirimi
titleSuffix: Configuration Manager
description: Merkezi Configuration Manager konsolundan anında işlem gerçekleştirerek istemcileri yönetin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cb7cc71618ad0f86abce3ab76d6344e0d23bfc58
ms.sourcegitcommit: 555cb8102715afbe06c4de5fdbc943608f00b52c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153432"
---
# <a name="client-notification-in-configuration-manager"></a>Configuration Manager 'de istemci bildirimi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Uzak istemcilerde acil eylem gerçekleştirmek için Configuration Manager konsolundan bir istemci bildirimi eylemi gönderin. Bu eylemleri tek bir cihazda veya bir cihaz koleksiyonunda başlatın.

## <a name="actions"></a>Eylemler

Aşağıdaki eylemler, Giriş sekmesinin cihazdaki veya koleksiyon grubundaki şeritte bulunur.

### <a name="install-client"></a>İstemci yüklemesi

**Istemci yüklemesi Sihirbazı**' nı açar. Bu sihirbaz Configuration Manager istemcisi yüklemek için client push yüklemesi kullanır. Daha fazla bilgi için bkz. [Client Push yüklemesi](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

#### <a name="permissions---install-client"></a>İzinler-istemci yüklemesi

Bu eylem **koleksiyon** nesnesinde **kaynak değiştirme** ve **okuma** izinlerini gerektirir.

Aşağıdaki yerleşik roller varsayılan olarak bu izinlere sahiptir:

- Uygulama Yöneticisi  
- Tam Yönetici  
- Altyapı Yöneticisi  
- İşlem Yöneticisi  
- İşletim sistemi Dağıtım Yöneticisi  

Bu izinleri, istemciyi göndermek için gereken tüm özel rollere ekleyin.

### <a name="run-script"></a>Betik çalıştırma

Koleksiyondaki tüm istemcilerde bir PowerShell Betiği çalıştırmak için **Betiği Çalıştır** sihirbazını açar. Daha fazla bilgi için bkz. [PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md).

#### <a name="permissions---run-script"></a>İzinler-Betiği Çalıştır

Bu eylem **koleksiyon** nesnesinde **Betiği Çalıştır** iznini gerektirir.

Aşağıdaki yerleşik roller varsayılan olarak bu izne sahiptir:

- Tam Yönetici  
- Altyapı Yöneticisi  
- İşlem Yöneticisi  

Bu izni, betikleri çalıştırması gereken herhangi bir özel role ekleyin.

### <a name="start-cmpivot"></a>CMPivot Başlat

Hedeflenen cihazlara karşı gerçek zamanlı sorgular çalıştıran **CMPivot**başlatır. Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot.md).

#### <a name="permissions---start-cmpivot"></a>İzinler-CMPivot Başlat

Bu eylem, [Betiği Çalıştır](#run-script) eylemiyle aynı izinleri gerektirir.

Sürüm 1906 ' den başlayarak, **koleksiyon** nesnesi üzerinde **CMPivot Çalıştır** iznini kullanabilirsiniz.

## <a name="client-notification"></a>İstemci bildirimi

Bu eylemler, Giriş sekmesinin cihazdaki veya koleksiyon grubundaki şeritte **İstemci bildirimi** menüsü altında bulunur.

Sürüm 1806 veya önceki sürümlerde, **Istemci bildirim** seçeneği yalnızca cihaz koleksiyonu düğümünden veya bir cihaz koleksiyonunun üyeliğini görüntülerken kullanılabilir. Sürüm 1810 ' den başlayarak, **Istemci bildirimini** doğrudan **cihazlar** düğümünden başlatabilirsiniz. Artık bir koleksiyon üyeliği görünümü içinde olması gerekmez. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>İzinler-Istemci bildirimi

<!--SCCMDocs-pr issue #2972-->
Sürüm 1810 ' den başlayarak, istemci bildirim eylemleri artık koleksiyon nesnesi üzerinde **kaynağı bilgilendir** iznini gerektirir. Bu izin, **İstemci bildirimi** menüsünün altındaki tüm eylemler için geçerlidir.

Aşağıdaki yerleşik roller varsayılan olarak bu izne sahiptir:

- Tam Yönetici  
- İşlem Yöneticisi  

Bu izni, istemci bildirimi eylemlerini kullanması gereken herhangi bir özel role ekleyin.

### <a name="download-computer-policy"></a>Bilgisayar ilkesini indir

Cihaz İlkesini yenileyin. Daha fazla bilgi için bkz. [Configuration Manager istemcisi için ilke almayı başlatma](manage-clients.md#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Kullanıcı ilkesini indir

Kullanıcı İlkesini yenileyin.  

### <a name="collect-discovery-data"></a>Bulma verilerini topla

Bir bulgu verileri kaydı (DDR) göndermek için istemcileri tetikleyin. Daha fazla bilgi için bkz. [sinyal keşfi](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

### <a name="collect-software-inventory"></a>Yazılım envanterini topla

İstemcileri bir yazılım envanteri döngüsünü çalıştıracak şekilde tetikleyin. Daha fazla bilgi için bkz. [yazılım envanterine giriş](inventory/introduction-to-software-inventory.md).  

### <a name="collect-hardware-inventory"></a>Donanım envanteri toplama

İstemcileri bir donanım envanteri döngüsünü çalıştıracak şekilde tetikleyin. Daha fazla bilgi için bkz. [Donanım envanterine giriş](inventory/introduction-to-hardware-inventory.md).  

### <a name="evaluate-application-deployments"></a>Uygulama dağıtımlarını değerlendir

İstemcileri bir uygulama dağıtımı değerlendirme döngüsünü çalıştıracak şekilde tetikleyin. Daha fazla bilgi için bkz. [dağıtımlar için yeniden değerlendirmeyi zamanlama](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Yazılım güncelleştirme dağıtımlarını değerlendir

İstemcileri bir yazılım güncelleştirmeleri dağıtımı değerlendirme döngüsünü çalıştıracak şekilde tetikleyin. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerine giriş](../../../sum/understand/software-updates-introduction.md).  

### <a name="switch-to-the-next-software-update-point"></a>Sonraki yazılım güncelleştirme noktasına geç

İstemcileri, bir sonraki kullanılabilir yazılım güncelleştirme noktasına geçiş yapmak için tetikleyin. Daha fazla bilgi için bkz. [yazılım güncelleştirme noktası değiştirme](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching).  

### <a name="evaluate-device-health-attestation"></a>Cihaz durumu kanıtlamayı değerlendir

En son cihaz sistem durumunu denetlemek ve göndermek için Windows 10 istemcilerini tetikler. Daha fazla bilgi için bkz. [sistem durumu kanıtlama](../../servers/manage/health-attestation.md).  

### <a name="wake-up"></a>Uyandır

Sürüm 1810 ' den başlayarak, lan 'da uyandırma paketini göndermek için aynı alt ağdaki diğer cihazları kullanarak uyandırma, LAN 'da uyandırma 'yı destekleyecek şekilde yapılandırılmış olan cihazları tetikler. Daha fazla bilgi için bkz. [LAN 'Da uyandırma yapılandırma](../deploy/configure-wake-on-lan.md).

### <a name="restart"></a>Yeniden başlat

Seçilen cihazları yeniden başlatmak için tetikleyin. Daha fazla bilgi için bkz. [Istemcileri yeniden başlatma](manage-clients.md#restart-clients).

## <a name="client-diagnostics"></a>İstemci tanılama
<!--4433455-->

Sürüm 1910 ' den başlayarak, Configuration Manager konsolundaki **Istemci tanılama** için yeni cihaz eylemleri vardır. Aşağıdaki eylemler eklendi:

- **Ayrıntılı günlüğü etkinleştir**: CCM bileşeni için genel günlük düzeyini Verbose olarak değiştirin ve hata ayıklama günlüğünü etkinleştirin.
- **Ayrıntılı günlüğe kaydetmeyi devre dışı bırak**: genel günlük düzeyini varsayılana değiştirin ve hata ayıklama günlüğünü devre dışı bırakın.
- **Istemci günlüklerini topla** (2002 'den başlayarak): SITE, CCM günlüklerini toplamak için seçili istemcilere bir istemci bildirim iletisi gönderir. İstemci, günlükleri yazılım envanteri dosya koleksiyonuyla aynı kanalı kullanarak yönetim noktasına gönderir. <!--4226618--> İstemci ayarlarında yazılım envanterini etkinleştirmeniz gerekmez.<!-- MEMDocs#305 -->
   - Sıkıştırılmış istemci günlükleri için boyut sınırı 100 MB 'tır. <!--6366098-->
   - Bu dosyaları yönetmek ve görüntülemek [Kaynak Gezgini](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) kullanın.

   [![Konsoldan istemci günlüklerini toplayın](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - Bu eylemler yalnızca boyut veya geçmişi değil, günlük ayrıntı düzeyini değiştirir. Daha ayrıntılı günlük kaydı daha fazla günlük içeriği oluşturabilir.
> - Yönetim noktası rolü CCM bileşenini de kullanır. Hedeflenen cihaz aynı zamanda bir yönetim noktası ise, bu eylem bu rol için de geçerlidir.

Bu ayarlar hakkında daha fazla bilgi için bkz. [günlük dosyaları hakkında](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client).

İstemcideki **Tanılama. log** dosyasında görevin durumunu izleyin. İstemci günlükleri toplandığında, daha fazla bilgi, site sunucusundaki yönetim noktasında ve **Sinvproc. log** dosyasında **MP_SinvCollFile. log dosyasına** kaydedilir.

> [!Tip]
> Toplanan istemci günlükleri, yazılım envanteri dosya koleksiyonu ayarlarına göre saklanır. Dosyalar, site sunucusunda **ınboxes\sinv\nbox\filecol** dizininde depolanır. Sürüm sayısında tanımlı bir sınır yoktur. [Eski toplanan dosyaları sil](../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-collected-files) site bakım görevi, varsayılan olarak her 90 günde bir zamanlamaya göre dosyaları siler.

### <a name="prerequisites---client-diagnostics"></a>Önkoşullar-Istemci tanılama

- Hedef istemciyi en son sürüme güncelleştirin.

- Configuration Manager Yönetici Kullanıcı, **kaynağı bilgilendir** iznine sahip olmalıdır.

  Aşağıdaki yerleşik roller varsayılan olarak bu izne sahiptir:

  - Tam Yönetici  
  - Altyapı Yöneticisi  

  Bu izni, istemci bildirimi eylemlerini kullanması gereken herhangi bir özel role ekleyin.


## <a name="endpoint-protection"></a>Uç Nokta Koruma

Aşağıdaki eylemler **Endpoint Protection** menüsünde verilmiştir. Bu menü, Giriş sekmesinin koleksiyon grubundaki şeritte bulunur. Bir veya daha fazla cihaz seçtiğinizde, bu eylemler şeridin **Seçili nesne** sekmesi üzerinde bulunur.

Daha fazla bilgi için [Configuration Manager Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)bakın.

### <a name="permissions---endpoint-protection"></a>İzinler-Endpoint Protection

Bu eylem, **koleksiyon** nesnesi üzerinde **güvenlik zorla** iznini gerektirir.

Aşağıdaki yerleşik roller varsayılan olarak bu izne sahiptir:

- Tam Yönetici  
- Endpoint Protection Yöneticisi  
- İşlem Yöneticisi  

Bu izni, Endpoint Protection eylemleri tetiklemeniz gereken herhangi bir özel role ekleyin.

### <a name="full-scan"></a>Tam tarama

*Tam* bir kötü amaçlı yazılımdan koruma taraması çalıştırmak için Endpoint Protection veya Windows Defender 'ı tetikler.  

### <a name="quick-scan"></a>Hızlı tarama

*Hızlı* kötü amaçlı yazılımdan koruma taraması çalıştırmak için Endpoint Protection veya Windows Defender 'ı tetikleyin.  

### <a name="download-definition"></a>Tanımı indir

En son kötü amaçlı yazılımdan koruma tanımlarını indirmek için Endpoint Protection veya Windows Defender 'ı tetikler.  

## <a name="see-also"></a>Ayrıca bkz.

- [İstemcileri yönetme](manage-clients.md)
- [Koleksiyonları yönetme](collections/manage-collections.md)
