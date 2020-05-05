---
title: Bakım görevleri için başvuru
titleSuffix: Configuration Manager
description: Configuration Manager site bakım görevlerinin her biri için Ayrıntılar
ms.date: 03/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9964834bf3a6bfa8e5c0a0bb70039554134490ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723876"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Configuration Manager 'de bakım görevlerine yönelik başvuru

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, her bir Configuration Manager site bakım görevinin ayrıntıları listelenmektedir. Her giriş, görevin kullanılabildiği site türlerini ve varsayılan olarak etkinleştirilip etkinleştirilmediğini belirtir.

Daha fazla bilgi için bkz. [bakım görevlerini ayarlama](maintenance-tasks.md#set-up-maintenance-tasks).  

## <a name="tasks"></a>Görevler

### <a name="backup-site-server"></a>Site Sunucusunu Yedekle

Bir siteyi ve Configuration Manager veritabanını geri yüklemek için kritik bilgilerinizin bir yedeğini oluşturmak için bu görevi kullanın. Daha fazla bilgi için bkz. [bir Configuration Manager sitesini yedekleme](backup-and-recovery.md).  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin değil|
|İkincil site|Kullanılamaz|

### <a name="check-application-title-with-inventory-information"></a>Uygulama başlığını envanter bilgileriyle denetle

Yazılım envanteri ve Varlık Yönetim Bilgileri kataloğu arasındaki yazılım başlıklarının tutarlılığını sağlamak için bu görevi kullanın. Daha fazla bilgi için bkz. [varlık yönetim bilgileri giriş](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|Birincil site|Kullanılamaz|
|İkincil site|Kullanılamaz|

### <a name="clear-undiscovered-clients"></a>Keşfedilmemiş Istemcileri temizle

> [!Tip]
> Bu görevi Ayrıca, **temiz Install bayrağını**adlı konsolda de görebilirsiniz.

**Istemci yeniden keşif** süresi sırasında sinyal bulma kaydı gönderolmayan istemciler için yüklü bayrağını kaldırmak üzere bu görevi kullanın. Yüklü bayrağı, etkin bir Configuration Manager istemcisi olabilecek bir bilgisayara otomatik istemci gönderme yüklemesini önler.  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin değil|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-application-request-data"></a>Eski uygulama Isteği verilerini sil

Eski uygulama isteklerini veritabanından silmek için bu görevi kullanın. Daha fazla bilgi için bkz. [uygulama oluşturma ve dağıtma](../../../apps/get-started/create-and-deploy-an-application.md).  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-application-revisions"></a>Eski uygulama düzeltmelerini Sil

Artık başvurulmayan uygulama düzeltmelerini silmek için bu görevi kullanın. Daha fazla bilgi için bkz. [uygulamaları gözden geçirme ve değiştirme](../../../apps/deploy-use/revise-and-supersede-applications.md).

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-client-download-history"></a>Eski Istemci Indirme geçmişini sil

İstemciler tarafından kullanılan indirme kaynağıyla ilgili geçmiş verileri silmek için bu görevi kullanın. Site, [Istemci veri kaynakları panosunu](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)doldurmak için indirme kaynağı bilgilerini kullanır.

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-client-operations"></a>Eski İstemci İşlemlerini Sil

Bu görevi, istemci işlemleri için tüm eski verileri site veritabanından silmek üzere kullanın. Örneğin, bu veriler aşağıdaki işlemleri içerir:

- Makine veya Kullanıcı ilkesi için indirme istekleri gibi eski veya olmayan istemci bildirimleri
- Endpoint Protection, istemcilerin bir taramayı çalıştırması veya güncelleştirilmiş tanımları indirmesi için yönetici kullanıcı tarafından yapılan istekler gibi

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-client-presence-history"></a>Eski Istemci varlığı geçmişini sil
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
İstemci bildirimi tarafından kaydedilen istemcilerin çevrimiçi durumuyla ilgili geçmiş bilgilerini silmek için bu görevi kullanın. Belirtilen süreden daha eski durumuna sahip istemcilerin bilgilerini siler. Daha fazla bilgi için bkz. [istemcileri izleme](../../clients/manage/monitor-clients.md).

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Eski Bulut Yönetimi Ağ Geçidi trafiği verilerini sil

Bu görevi, [bulut yönetimi ağ geçidiyle](../../clients/manage/cmg/plan-cloud-management-gateway.md)geçen trafikle ilgili tüm eski verileri site veritabanından silmek için kullanın. Bu veriler şunlardır:

- İstek sayısı
- Toplam istek baytları
- Toplam Yanıt baytı
- Başarısız istek sayısı
- En fazla eşzamanlı istek sayısı

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-cmpivot-results"></a>Eski CMPivot sonuçlarını Sil

Bu görevi, CMPivot sorguları içindeki istemcilerden gelen site veritabanından eski bilgileri silmek için kullanın. Daha fazla bilgi için bkz. [CMPivot for Real Time Data](cmpivot.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-collected-files"></a>Eski toplanan dosyaları sil

Bu görevi, toplanan dosyalarla ilgili eski veritabanı bilgilerini silmek için kullanın. Bu görev ayrıca toplanan dosyaları seçilen sitede site sunucusu klasör yapısından da siler. Varsayılan olarak, toplanan dosyaların en son beş kopyası site sunucusunda **ınboxes\sinv\nbox\filecol** dizininde depolanır. Daha fazla bilgi için bkz. [yazılım envanterine giriş](../../clients/manage/inventory/introduction-to-software-inventory.md).  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-computer-association-data"></a>Eski Bilgisayar İlişkilendirme Verilerini Sil

Bu görevi, eski işletim sistemi dağıtımı bilgisayar ilişkilendirme verileri veritabanından silmek için kullanın. Bu bilgiler, bir görev dizisi sırasında Kullanıcı durumu geri yüklenirken kullanılır. Daha fazla bilgi için bkz. [Kullanıcı durumunu yönetme](../../../osd/get-started/manage-user-state.md).  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-console-connection-data"></a>Eski konsol bağlantı verilerini sil

Bu görev site veritabanından konsol bağlantıları hakkındaki verileri siler.<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-delete-detection-data"></a>Eski silme algılama verilerini sil

Bu görevi, ayıklama görünümleri tarafından oluşturulan veritabanından eski verileri silmek için kullanın. Dış sistemler tarafından kullanılan eski veri değişikliği bilgilerini veritabanından verileri ayıklayarak siler.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-device-wipe-record"></a>Eski cihaz silme kaydını sil

Bu görevi, mobil cihaz silme eylemlerine ilişkin eski verilerden veritabanını silmek için kullanın. Daha fazla bilgi için bkz. [uzaktan silme, kilitleme veya parola sıfırlama ile verileri koruma](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-discovery-data"></a>Eski Bulma Verilerini Sil

Eski bulma verilerini veritabanından silmek için bu görevi kullanın. Bu veriler şunlar arasında kayıt içerebilir:

- Sinyal keşfi
- Ağ bulma
- Active Directory bulma yöntemleri: sistem, Kullanıcı ve Grup

Bu görev Ayrıca, kullanımdan kaldırılan olarak işaretlenen eski cihazları da kaldırır. Bu görev bir sitede çalıştırıldığında, o siteyle ilişkili veriler silinir ve bu değişiklikler diğer sitelere çoğaltılır. Daha fazla bilgi için bkz. [bulmayı çalıştırma](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-distribution-point-usage-stats"></a>Eski dağıtım noktası kullanım Istatistiklerini Sil

Bu görevi, belirli bir süreden daha uzun bir süre saklanan dağıtım noktaları için eski verileri veritabanından silmek için kullanın.  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-enrolled-devices"></a>Eski kayıtlı cihazları Sil

Bu görevi, belirli bir süredir siteye herhangi bir bilgi bildirmeyen mobil cihazlarla ilgili eski verileri site veritabanından silmek için kullanın.

Bu görev, [Şirket ıçı MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)Configuration Manager kayıtlı cihazlar için geçerlidir. Bu cihazlar hakkında daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemleri](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin değil|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-ep-health-status-history-data"></a>Eski EP sistem durumu geçmiş verilerini sil

Endpoint Protection (EP) için veritabanı eski durum bilgilerini silmek için bu görevi kullanın. Daha fazla bilgi için bkz. [izleme Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-exchange-partnership"></a>Eski Exchange ortaklığını Sil

> [!Tip]
> > Bu görevi, **Exchange Server Bağlayıcısı tarafından yönetilen eski cihazları Sil**adlı konsolda de görebilirsiniz.

Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlara ilişkin eski verileri silmek için bu görevi kullanın. Site, bu verileri Exchange Server Bağlayıcısı özelliklerinin **bulma** sekmesindeki **(gün) daha fazla süre için etkin olmayan mobil cihazlara** göre siler. Daha fazla bilgi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-inventory-history"></a>Eski envanter geçmişini sil

Bu görevi, belirli bir süreden daha uzun süredir depolanan veritabanı envanter verilerinden silmek için kullanın. Daha fazla bilgi için bkz. [donanım envanterini görüntülemek için kaynak Gezgini kullanma](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-log-data"></a>Eski günlük verilerini sil

Bu görevi, sorun giderme için kullanılan eski günlük verilerini veritabanından silmek için kullanın. Bu veriler Configuration Manager bileşen işlemleriyle ilgili değildir.  

> [!IMPORTANT]  
> Bu görev, varsayılan olarak her sitede günlük olarak çalıştırılır. Bir merkezi yönetim sitesinde ve birincil sitelerde, görev 30 günden eski olan verileri siler. İkincil bir sitede SQL Server Express kullandığınızda, bu görevin günlük olarak çalıştığından ve yedi gün boyunca etkin olmayan verileri sildiğinden emin olun.  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|**İkincil site**|Etkin|

### <a name="delete-aged-metering-data"></a>Eski ölçüm verilerini sil

Bu görevi, belirli bir süreden daha uzun süredir depolanan yazılım kullanım ölçümü için eski verileri veritabanından silmek üzere kullanın. Daha fazla bilgi için bkz. [yazılım kullanım ölçümü](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-metering-summary-data"></a>Eski ölçüm özet verilerini sil

Bu görevi, belirli bir süreden daha uzun süredir depolanan yazılım kullanım ölçümü için eski veritabanı Özet verilerinden silmek üzere kullanın. Daha fazla bilgi için bkz. [yazılım kullanım ölçümü](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-notification-server-history"></a>Eski bildirim sunucusu geçmişini sil

Bu görev eski istemci varlığı geçmişini siler.

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-notification-task-history"></a>Eski bildirim görevi geçmişini sil

Bu görevi, istemci bildirim görevleriyle ilgili site veritabanı bilgilerini silmek için kullanın. Bu görev, belirli bir süre için güncelleştirilmemiş veriler için geçerlidir. Daha fazla bilgi için bkz. [istemci bildirimleri](../../clients/manage/client-notification.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-passcode-records"></a>Eski geçiş kodu kayıtlarını Sil

Eski geçiş kodu Windows Phone cihazların verilerini sıfırlamasını silmek için bu görevi hiyerarşinizin en üst düzeyindeki sitesinde kullanın. Geçiş kodu sıfırlama verileri şifrelenir ancak cihazlar için PIN 'ı içerir. Varsayılan olarak, bu görev etkindir ve bir günden eski olan verileri siler.  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-replication-data"></a>Eski çoğaltma verilerini sil

Configuration Manager siteleri arasında veritabanı çoğaltmasıyla ilgili eski veritabanından silmek için bu görevi kullanın. Bu bakım görevinin yapılandırmasını değiştirdiğinizde, yapılandırma hiyerarşideki geçerli tüm sitelere uygulanabilir. Daha fazla bilgi için bkz. [veritabanı çoğaltmasını izleme](monitor-replication.md).  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|**İkincil site**|Etkin|

### <a name="delete-aged-replication-summary-data"></a>Eski çoğaltma Özeti verilerini sil

Bu görevi, belirli bir süre boyunca güncelleştirilmemiş eski çoğaltma Özeti verilerini site veritabanından silmek için kullanın. Daha fazla bilgi için bkz. [veritabanı çoğaltmasını izleme](monitor-replication.md).  

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|**İkincil site**|Etkin|

### <a name="delete-aged-status-messages"></a>Eski durum Iletilerini Sil

Bu görevi, durum filtre kurallarında yapılandırılmış eski durum iletisi verilerini veritabanından silmek için kullanın. Daha fazla bilgi için bkz. [Configuration Manager durum sistemini izleme](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-threat-data"></a>Eski tehdit verilerini sil

Bu görevi, belirli bir süreden daha uzun süredir depolanan eski Endpoint Protection tehdit verilerini veritabanından silmek için kullanın. Daha fazla bilgi için bkz. [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-unknown-computers"></a>Eski Bilinmeyen Bilgisayarları Sil

Bu görevi, belirli bir süre boyunca güncelleştirilmemiş site veritabanından bilinmeyen bilgisayarlara ilişkin bilgileri silmek için kullanın. Daha fazla bilgi için bkz. [bilinmeyen bilgisayar dağıtımları Için hazırlanma](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-aged-user-device-affinity-data"></a>Eski Kullanıcı cihaz benzeşimi verilerini sil

Eski Kullanıcı cihaz benzeşimi verilerini veritabanından silmek için bu görevi kullanın. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-duplicate-system-discovery-data"></a>Yinelenen sistem bulma verilerini sil

Bu görevi, sistem bulma tarafından oluşturulan yinelenen kayıtları site veritabanından silmek için kullanın.<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|Birincil site|Kullanılamaz|
|İkincil site|Kullanılamaz|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Süre dolmamış MDM toplu kayıt paketi kayıtlarını Sil

Kayıt sertifikasının süresi dolduktan sonra eski toplu kayıt sertifikalarını ve ilgili profilleri silmek için bu görevi kullanın. Daha fazla bilgi için bkz. [sertifika profilleri oluşturma](../../../protect/deploy-use/create-certificate-profiles.md).

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-inactive-client-discovery-data"></a>Etkin olmayan Istemci bulma verilerini sil

Etkin olmayan istemciler için veritabanı bulma verilerinden silmek için bu görevi kullanın. İstemci eski olarak işaretlendiğinde ve istemci durumu için yapılan yapılandırmalarda, site istemcileri etkin değil olarak işaretler.

Bu görev yalnızca Configuration Manager istemci kaynakları üzerinde çalışır. Eski bulma verilerini **Sil** görevinden farklıdır, bu, eski bulgu verileri kaydını siler. Bu görev bir sitede çalıştırıldığında, verileri bir hiyerarşideki tüm sitelerde veritabanından siler. Daha fazla bilgi için bkz. [istemci durumunu yapılandırma](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> Etkinleştirildiğinde, bu görevi **sinyal bulma** zamanlamadan daha büyük bir aralıkta çalışacak şekilde yapılandırın. Bu yapılandırma, etkin istemcilerin istemci kayıtlarını etkin olarak işaretlemek için bir sinyal bulma kaydı göndermesini sağlar, bu nedenle bu görev onları silmez.  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin değil|
|İkincil site|Kullanılamaz|

### <a name="delete-obsolete-alerts"></a>Artık kullanılmayan uyarıları Sil

Bu görevi, belirli bir süreden daha uzun bir süre saklanan, süresi dolmayan uyarıları silmek için kullanın. Daha fazla bilgi için bkz. [uyarıları ve durum sistemini kullanma](use-alerts-and-the-status-system.md).

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-obsolete-client-discovery-data"></a>Artık kullanılmayan Istemci bulma verilerini sil

Eski istemci kayıtlarını veritabanından silmek için bu görevi kullanın. Kullanım dışı olarak işaretlenen bir kayıt, genellikle aynı istemci için daha yeni bir kayıtla değiştirilmiştir. Yeni kayıt istemcinin geçerli kaydı olur. Bulma hakkında bilgi için bkz. [bulmayı çalıştırma](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> Etkinleştirildiğinde, bu görevi sinyal bulma zamanlamadan daha büyük bir aralıkta çalışacak şekilde yapılandırın. Bu yapılandırma, istemcinin eski durumu doğru şekilde ayarlayan bir sinyal bulma kaydı göndermesini sağlar.  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin değil|
|İkincil site|Kullanılamaz|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Artık kullanılmayan orman bulma sitelerini ve alt ağlarını Sil

Active Directory siteleri, alt ağlar ve etki alanları hakkındaki verileri silmek için bu görevi kullanın. Son 30 gün içinde, sitenin Active Directory orman bulma yöntemi tarafından bulunmayan verileri kaldırır. Bu görev, bulma verilerini kaldırır, ancak bu bulgu verilerinden oluşturduğunuz sınırları etkilemez. Daha fazla bilgi için bkz. [bulmayı çalıştırma](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="delete-orphaned-client-deployment-state-records"></a>Yalnız bırakılmış Istemci dağıtımı durum kayıtlarını Sil

İstemci dağıtım durumu bilgilerini içeren tabloyu düzenli aralıklarla temizlemek için bu görevi kullanın. Bu görev, eski veya kullanımdan kaldırılan cihazlarla ilişkili kayıtları temizler.  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="evaluate-collection-members"></a>Koleksiyon üyelerini değerlendir

Koleksiyon üyeliği değerlendirmesini bir site bileşeni olarak yapılandırırsınız. Daha fazla bilgi için bkz. [site bileşenleri](../deploy/configure/site-components.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="monitor-keys"></a>Anahtarları izle

Configuration Manager veritabanı birincil anahtarlarının bütünlüğünü izlemek için bu görevi kullanın. Birincil anahtar, bir sütunu veya bir satırı benzersiz bir şekilde tanımlayan sütunların bir birleşimidir. Anahtar, Microsoft SQL Server veritabanı tablosundaki diğer satırlardan satırı ayırır.

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="rebuild-indexes"></a>Dizinleri yeniden oluştur

Configuration Manager veritabanı dizinlerini yeniden derlemek için bu görevi kullanın. Dizin, veri alımını hızlandırmak için veritabanı tablosunda oluşturulan bir veritabanı yapısıdır. Örneğin, dizinli bir sütunu aramak, dizinlenmemiş bir sütunu aramadan genellikle çok daha hızlıdır.

Performansı artırmak için Configuration Manager veritabanı dizinleri, veritabanında depolanan sürekli değişen verilerle eşitlenmiş olarak kalacak şekilde sık güncelleştirilir. Bu görev:

- Veritabanı sütunlarında en az yüzde 50 benzersiz olan dizinler oluşturur
- %50 ' den az benzersiz olan sütunlarda dizinleri bırakır
- Veri benzersizliği ölçütünü karşılayan mevcut tüm dizinleri yeniden oluşturur

|||
|---------|---------|
|**Merkezi yönetim sitesi**|Etkin değil|
|**Birincil site**|Etkin değil|
|**İkincil site**|Etkin değil|

### <a name="summarize-file-usage-metering-data"></a>Dosya kullanımı ölçüm verilerini özetleme

Yazılım kullanım ölçümü dosya kullanımı için birden çok kayıttan alınan verileri tek bir genel kayıtta özetlemek için bu görevi kullanın. Veri özetleme, Configuration Manager veritabanında depolanan veri miktarını sıkıştırabilir.

Yazılım kullanım ölçümü verilerini özetlemek ve veritabanında disk alanından tasarruf etmek için bu görevi **yazılım ölçümü aylık kullanım verilerini Özetle** göreviyle birlikte kullanın. Daha fazla bilgi için bkz. [yazılım kullanım ölçümü](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="summarize-installed-software-data"></a>Yüklü yazılım verilerini Özetle

Birden çok kaydı tek bir genel kayıtta birleştirmek için donanım envanteri aracılığıyla toplanan varlık yönetim bilgileri yazılım bilgilerinden verileri özetlemek üzere bu görevi kullanın. Veri özetleme, Configuration Manager veritabanında depolanan veri miktarını sıkıştırabilir. Daha fazla bilgi için bkz. [varlık yönetim bilgileri bakım görevlerini yapılandırma](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="summarize-monthly-usage-metering-data"></a>Aylık kullanım ölçümü verilerini özetleme

Yazılım ölçümü aylık kullanımı için birden çok kayıttan alınan verileri tek bir genel kayıtta özetlemek için bu görevi kullanın. Veri özetleme, Configuration Manager veritabanında depolanan veri miktarını sıkıştırabilir.

Yazılım kullanım ölçümü verilerini özetlemek ve veritabanında yer kazanmak için bu görevi **yazılım ölçümü dosyası kullanım verilerini Özetle** göreviyle birlikte kullanın. Daha fazla bilgi için bkz. [yazılım kullanım ölçümü](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="update-application-available-targeting"></a>Uygulama için kullanılabilir hedefleme 'yi Güncelleştir

Bu görevi, koleksiyonlardaki kaynaklarla ilke ve uygulama dağıtımlarının eşlemesini yeniden hesaplamak Configuration Manager için kullanın. Bir koleksiyona ilke veya uygulama dağıttığınızda, Configuration Manager dağıttığınız nesneler ile koleksiyon üyeleri arasında bir ilk eşleme oluşturur.

Bu eşlemeler hızlı başvuru için bir tabloda depolanır. Bir koleksiyon üyeliği değiştiğinde, site bu değişiklikleri yansıtacak şekilde bu saklı eşlemeleri güncelleştirir. Ancak, bu eşlemelerin eşitlenmemiş olması mümkündür. Örneğin, site bir bildirim dosyasını düzgün bir şekilde işleyemezse, bu değişiklik eşlemelere bir değişikliğe yansıtılmayabilir. Bu görev, geçerli koleksiyon üyeliğine göre eşlemeyi yeniler.  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|

### <a name="update-application-catalog-tables"></a>Uygulama Kataloğu tablolarını güncelleştirme

Uygulama Kataloğu web sitesi veritabanı önbelleğini en son uygulama bilgileriyle eşleştirmek için bu görevi kullanın. Bu bakım görevinin yapılandırmasını değiştirdiğinizde, hiyerarşideki tüm birincil siteler için geçerli olur.  

|||
|---------|---------|
|Merkezi yönetim sitesi|Kullanılamaz|
|**Birincil site**|Etkin|
|İkincil site|Kullanılamaz|


## <a name="see-also"></a>Ayrıca bkz.

[Bakım görevleri](maintenance-tasks.md)
