---
title: Configuration Manager Araçları
titleSuffix: Configuration Manager
description: Configuration Manager altyapınızı yönetmenize ve sorunlarını gidermenize yardımcı olacak araçlar hakkında bilgi edinin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb2529dbbe923a5035f0b7586dab696cd6fc917e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699424"
---
# <a name="configuration-manager-tools"></a>Configuration Manager Araçları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager araçları [istemci tabanlı](#client-tools) ve [sunucu tabanlı araçları](#server-tools)içerir. Configuration Manager altyapınızı desteklemeye ve sorunlarını gidermenize yardımcı olması için bu araçları kullanın.

Configuration Manager sürüm 1806 ' den başlayarak, bu araçlar `CD.Latest\SMSSETUP\Tools` site sunucusundaki klasörüne dahil edilmiştir. Başka bir yükleme gerekli değildir.<!--1357145--> Configuration Manager sürüm 1806 ve üzeri ile araçların bu sürümlerini kullanın.

[İstemciler ve cihazlar Için desteklenen işletim sistemlerinde](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) desteklenen istemciler olarak listelenen tüm Windows işletim sistemleri, bu araçlarla kullanılmak üzere desteklenir.

> [!Note]  
> [System Center 2012 R2 Configuration Manager araç seti](https://www.microsoft.com/download/details.aspx?id=50012) , Microsoft İndirme Merkezi 'nden hala kullanılabilir. Configuration Manager sürüm 1806 ve üzeri için CD 'deki araçların sürümlerini kullanın. Site sunucusundaki en son klasör. Bazı araçlar daha önce araç setinde yer almaktadır ancak sürüm 1806 ' de yoktu. Bu eski araçlar artık desteklenmemektedir.


## <a name="client-tools"></a>İstemci araçları

Bu araçlar `ClientTools` alt klasörüdür:

- [CMTrace](cmtrace.md): Configuration Manager günlük dosyalarını görüntüleyin, izleyin ve çözümleyin  

- [Istemci Spy](clispy.md): yazılım dağıtımı, envanter ve ölçüm ile ilgili sorunları giderme

- [Dağıtım Izleme aracı](deployment-monitoring-tool.md): uygulamalarda, güncelleştirmelerde ve temel dağıtımların sorunlarını giderme  

- [Ilke Spy](policy-spy.md): ilke atamalarını görüntüleme  

- [Power Viewer aracı](power-viewer-tool.md): güç yönetimi özelliğinin durumunu görüntüleme  

- [Zamanlama aracı gönder](send-schedule-tool.md): yapılandırma temellerinin zamanlamalarını ve değerlendirmesini tetikleme  

> [!Note]  
> `ClientTools`Klasör Microsoft.Diagnostics.Tracing.EventSource.dll dosyasını da içerir. Bu kitaplığın çeşitli istemci araçları gerekir. Doğrudan kullanamazsınız.  


## <a name="server-tools"></a>Sunucu araçları

Bu araçlar `ServerTools` alt klasörüdür:

- [DP Iş kuyruğu Yöneticisi](dp-job-manager.md): içerik dağıtım işlerinin dağıtım noktalarına yönelik sorunlarını giderir  

- [Koleksiyon değerlendirme Görüntüleyicisi](ceviewer.md): koleksiyon değerlendirmesi ayrıntılarını görüntüleme  

- [Içerik kitaplığı Gezgini](content-library-explorer.md): içerik kitaplığı tek örnek deposunun içeriğini görüntüleme  

- [Içerik kitaplığı aktarımı](content-library-transfer.md): içerik kitaplığını sürücüler arasında aktarır  

- [Içerik sahipliği aracı](content-ownership-tool.md): yalnız bırakılmış paketlerin sahipliğini değiştirir. Bu paketler sitede sahip olan bir site sunucusu olmadan bulunur.

- [Rol tabanlı yönetim ve Denetim Aracı](rbaviewer.md): yöneticilerin rol yapılandırmasını denetlemenize yardımcı olur  

- Ölçüm [özetleme aracını Çalıştır](run-meter-summ.md): ölçüm özetleme görevi çalıştırma ve ölçüm verilerini çözümleme

> [!Note]  
> ServerTools klasörü de aşağıdaki dosyaları içerir:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Bu kitaplıkların çeşitli sunucu araçları gerekir. Onları doğrudan kullanamazsınız.  

## <a name="other-tools-and-toolkits"></a>Diğer araçlar ve araç takımları

- [Destek Merkezi](support-center.md): sorun giderirken daha kolay analiz için istemcilerden bilgi toplayın.

    Sürüm 1906 ' den başlayarak **Onetrace** , Destek Merkezi 'nin bulunduğu yeni bir günlük görüntüleyicisine sahiptir. Geliştirme ile CMTrace 'e benzer şekilde çalışır. Daha fazla bilgi için bkz. [Destek Merkezi OneTrace](support-center-onetrace.md).

- [Microsoft Azure şirket içi siteyi genişletme ve geçirme](azure-migration-tool.md): Configuration Manager için programlı olarak Azure sanal makineleri (VM 'ler) oluşturmanıza yardımcı olur. <!--3556022--> 

- [İçerik kitaplığı Temizleme Aracı](../plan-design/hierarchy/content-library-cleanup-tool.md): **ContentLibraryCleanup.exe** `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` bir dağıtım noktasından yalnız bırakılmış içeriği kaldırmak için içindeContentLibraryCleanup.exekullanın.  

- [Hiyerarşi bakım aracı](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): **Preinst.exe** `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` komutları hiyerarşi Yöneticisi bileşenine geçirmek için site sunucusundaki paylaşılan klasördePreinst.exekullanın.  

- [Güncelleştirme sıfırlama aracı](../servers/manage/update-reset-tool.md): **CMUpdateReset.exe** `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` konsol içi güncelleştirmelerin indirme veya çoğaltma sorunları olduğunda sorunları gidermek için içindeCMUpdateReset.exekullanın.  

- [Hizmet bağlantı aracı](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): **ServiceConnectionTool.exe** `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` hizmet bağlantı noktanız çevrimdışı olduğunda sitenizi güncel tutmak içinServiceConnectionTool.exekullanın.   

- [Microsoft Dağıtım Araç Seti (MDT)](../../mdt/use-the-mdt.md): Masaüstü ve sunucu işletim sistemi dağıtımlarını otomatikleştirmek için bir araçlar, süreçler ve kılavuz topluluğu.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): özel yazılım güncelleştirmelerini yönetmek ve içeri aktarmak için tek başına bir araç.

- [Paket Dönüştürme Yöneticisi](../../apps/pcm/package-conversion-manager.md): eski paketleri uygulamalara Dönüştür.