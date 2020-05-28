---
title: Yazılım güncelleştirmeleri için önkoşullar
titleSuffix: Configuration Manager
description: Configuration Manager 'de yazılım güncelleştirmeleri için Önkoşullar hakkında bilgi edinin.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: a870d2bf18b9e7f064e914f450aee0f5e3e2e545
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906710"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Configuration Manager 'de yazılım güncelleştirmeleri için Önkoşullar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede Configuration Manager yazılım güncelleştirmeleri için Önkoşullar listelenmektedir. Her bir önkoşul için dış bağımlılıklar ve iç bağımlılıklar ayrı tablolarda listelenmiştir.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager dış olan yazılım güncelleştirme bağımlılıkları  
 Aşağıdaki bölümler yazılım güncelleştirmeleri için dış bağımlılıkları listeler.  

### <a name="internet-information-services"></a>Internet Information Services  
 Yazılım güncelleştirme noktasını, yönetim noktasını ve dağıtım noktasını çalıştırmak için site sistem sunucularında Internet Information Services (IIS) yüklü olmalıdır. Daha fazla bilgi için bkz. [site sistem rolleri önkoşulları](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Yazılım güncelleştirmeleri eşitlemesi ve istemcilerde yazılım güncelleştirmeleri Uygulanabilirlik taraması için Windows Server Update Services (WSUS) gereklidir. Yazılım güncelleştirme noktası rolünü oluşturmadan önce WSUS sunucusunun yüklenmesi gerekir. Yazılım güncelleştirme noktası için aşağıdaki WSUS sürümleri desteklenir:  

- WSUS 10.0.14393 (Windows Server 2016 ' de rol)
- WSUS 10.0.17763 (Windows Server 2019 ' de rol) (Configuration Manager 1810 veya üzeri) gerektirir)
- WSUS 6,2 ve 6,3 (Windows Server 2012 ve Windows Server 2012 R2 'deki rol)
  - Windows 10 yükseltmeleri dağıtırsanız, [kb 3095113 ve kb 3159706 (veya eşdeğer bir güncelleştirme)](#BKMK_wsus2012) WSUS 6,2 ve 6,3 için gereklidir.

> [!NOTE]
> - Bir sitede birden çok yazılım güncelleştirme noktanız olduğunda, bunların tümünün aynı WSUS sürümünü çalıştırdığından emin olun.

### <a name="wsus-administration-console"></a>WSUS Yönetim Konsolu  
Yazılım güncelleştirme noktası uzak bir site sistem sunucusunda olduğunda ve WSUS site sunucusunda zaten yüklü değilse, Configuration Manager site sunucusunda WSUS Yönetim Konsolu gereklidir.  

> [!IMPORTANT]  
> - Site sunucusundaki WSUS sürümü, yazılım güncelleştirme noktalarında çalışan WSUS sürümüyle aynı olmalıdır.
> - WSUS ayarlarını yapılandırmak için WSUS Yönetim Konsolu 'Nu kullanmayın. Configuration Manager, yazılım güncelleştirme noktasında çalışan WSUS örneğine bağlanır ve uygun ayarları yapılandırır.  


### <a name="windows-update-agent"></a>Windows Update Aracısı  
 Windows Update Aracısı (WUA) istemcisi, WSUS sunucusuna bağlanabilmeleri için istemcilerde gereklidir. WUA, uyumluluk için taranması gereken yazılım güncelleştirmelerinin listesini alır.  

 Configuration Manager yüklediğinizde, WUA 'nın en son sürümü indirilir. Daha sonra, Configuration Manager istemcisini yüklediğinizde WUA, gerekirse yükseltilir. Yükleme başarısız olursa, WUA 'yı yükseltmek için farklı bir yöntem kullanmanız gerekir.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager iç yazılım güncelleştirme bağımlılıkları  
 Aşağıdaki bölümlerde Configuration Manager içindeki yazılım güncelleştirmelerine yönelik iç bağımlılıklar listelenmektedir.  

### <a name="management-points"></a>Yönetim noktaları  
 Yönetim noktaları, istemci bilgisayarlar ve Configuration Manager sitesi arasında bilgi aktarır. Yazılım güncelleştirmeleri için yönetim noktaları gereklidir.  

### <a name="software-update-points"></a>Yazılım güncelleştirme noktaları  
 Configuration Manager ' de yazılım güncelleştirmelerini dağıtmak için WSUS sunucusuna bir yazılım güncelleştirme noktası yüklemelisiniz. Daha fazla bilgi için bkz. [yazılım güncelleştirme noktası yükleyip yapılandırma](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Dağıtım noktaları  
 Dağıtım noktaları, yazılım güncelleştirmelerinin içeriğini depolamak için gereklidir. Dağıtım noktalarının nasıl yükleneceği ve içeriğin nasıl yönetileceği hakkında daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Yazılım güncelleştirmeleri için istemci ayarları  
Yazılım güncelleştirmeleri varsayılan olarak istemciler için etkinleştirilmiştir. İstemcilerin yazılım güncelleştirmelerinin uyumluluğunu nasıl ve ne zaman değerlendirmekte olduğunu ve yazılım güncelleştirmelerinin nasıl yükleneceğini kontrol eden başka kullanılabilir ayarlar vardır.  

 Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [Yazılım güncelleştirmeleri için istemci ayarları](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Yazılım güncelleştirmeleri istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Raporlama hizmetleri noktaları  
 Raporlama hizmetleri noktası site sistemi rolü yazılım güncelleştirmeleriyle ilgili raporları görüntüleyebilir. Bu rol isteğe bağlıdır, ancak önerilir. Raporlama Hizmetleri noktası oluşturma hakkında daha fazla bilgi için bkz. [raporlamayı yapılandırma](../../core/servers/manage/configuring-reporting.md).  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a>WSUS 6,2 ve 6,3 ' de hangi güncelleştirmeler gerekli?

WSUS 6,2 ve 6,3 ' de **yükseltmeler** sınıflandırmasını eşitlemek için iki güncelleştirme gerekir. Bazen, KB3095113 ve KB3159706 yüklenmeden önce eşitlendiğinde yükseltmeleri indirme veya dağıtma hatasıyla karşılaşabilirsiniz. Olası sorunlar hakkında daha fazla bilgi için sonraki bölümde yer verilir.  

- **Yükseltmeler** sınıflandırmasını eşitlemeden önce yazılım güncelleştirme noktalarınıza ve site sunucularınıza 2015 Ekim ' de yayınlanan [KB 3095113](https://support.microsoft.com/kb/3095113)sürümünü yüklemelisiniz.
  - Bu güncelleştirme, **yükseltmeler** sınıflandırmasını sunar.
- Windows 10 sürüm 1607 ve üzeri Hizmetleri için [KB 3159706](https://support.microsoft.com/help/3159706)' yi yükleyip yapılandırmanız gerekir. KB 3159706 Mayıs 2016 ' de yayımlandı.
  - Bu güncelleştirme, WSUS 'nin Windows 10 sürüm 1607 ve üstünü yükseltmek için kullanılan dosyaların yerel olarak şifresini çözmesine olanak sağlar.

>[!IMPORTANT]
> KB 3095113 ve KB 3159706 her ikisi de, 2017 Haziran 'dan itibaren **güvenlik aylık kalite toplamasına** dahildir. Bu, bir toplama ile yüklenmiş olabileceğinden, yüklü güncelleştirmeler olarak KB 3095113 ve KB 3159706 görmeyeceğiniz anlamına gelir. Ancak, Bu güncelleştirmelerden birine ihtiyacınız varsa, WSUS 'nin ClientWebService üzerinde bellek kullanımını azaltmak için ek bir WSUS güncelleştirmesi içerdiklerinden beri, 2017 Ekim 'den sonra yayımlanan bir **güvenlik aylık kalite toplaması** yüklemenizi öneririz.

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a>Windows 10 yükseltmeleri indirmesi "hata: geçersiz sertifika imzası" veya 0xc1800118 hatasıyla başarısız oluyor

Bu bölümde açıklanan güncelleştirmeler ve sorunlar yalnızca Windows Server 2012 veya Windows Server 2012 R2 makinelerinde (WSUS 6,2 ve 6,3) çalışan WSUS için geçerlidir. Genellikle, bu bölümde açıklanan sorunları yalnızca WSUS 'u 2017 Temmuz 'dan önce yüklediyseniz ve **yükseltme** sınıflandırmasını son zamanlarda etkinleştirdiyseniz görürsünüz. Ancak, bu sorunları başka durumlarda da görmek mümkündür.

### <a name="historical-information-about-kb-3095113"></a>KB 3095113 hakkında geçmiş bilgileri

 [KB 3095113](https://support.microsoft.com/kb/3095113) , WSUS 'e Windows 10 yükseltmeleri için destek eklemek üzere 2015 Ekim 'de [bir düzeltme olarak yayımlanmıştır](https://docs.microsoft.com/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113) . Güncelleştirme, WSUS 'nin Windows 10 için **yükseltmeler** sınıflandırmasında güncelleştirmeleri eşitlemesini ve dağıtmasını sağlar.

Önce [KB 3095113](https://support.microsoft.com/kb/3095113)yüklenmeden herhangi bir yükseltmeyi EŞITLERSENIZ, WSUS veritabanını (SUSDB) kullanılamayan verilerle doldurursunuz. Yükseltmelerin düzgün bir şekilde dağıtılması için önce bu verilerin temizlenmesi gerekir. Bu durumdaki Windows 10 yükseltmeleri yazılım güncelleştirmelerini Indirme Sihirbazı kullanılarak indirilemiyor.

Yazılım güncelleştirmelerini Indirme Sihirbazı 'nın tamamlama sayfasında aşağıdakine benzer hatalar görüntülenir:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Ayrıca, aşağıdaki gibi bir benzer hatalar PatchDownloader. log dosyasında günlüğe kaydedilir:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Tarihsel olarak, bu hatalar oluştuğunda, [WSUS için çözüm adımlarının](https://docs.microsoft.com/archive/blogs/wsus/how-to-delete-upgrades-in-wsus)değiştirilmiş bir sürümü çalıştırılarak çözümlenirler. Bu adımlar, KB 3159706 yüklemesinden sonra gereken adımları el ile yapmamız için çözünürlüğe benzer olduğundan, her iki adım kümesini aşağıdaki bölümde tek bir çözünürlükte birleştirdik:

- [Kb 3095113 veya kb 3159706 ' ü yüklemeden önce yükseltmeleri eşitlemeden kurtarmak için](#bkmk_fix-upgrades).

### <a name="historical-information-about-kb-3159706"></a>KB 3159706 hakkında geçmiş bilgileri

KB 3148812, Windows 10 paketlerini yükseltmek için kullanılan. ESD dosyalarının yerel olarak şifresini çözmesine olanak tanımak üzere başlangıçta 2016 Nisan 'da yayımlanmıştır. [Kb 3148812 bazı müşteriler için sorun oluşmasına neden oldu](https://docs.microsoft.com/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues) ve [KB 3159706](https://support.microsoft.com/help/3159706)ile değiştirilmiştir. Windows 10 sürüm 1607 ve üzeri cihazlara hizmet vermeden önce, KB 3159706 ' nin tüm yazılım güncelleştirme noktalarınızda ve site sunucularınızda yüklü olması gerekir. Bununla birlikte, KB 'yi fark etmezseniz sorunlar ortaya çıkabilir, yüklemeden sonra aşağıdaki el ile gerçekleştirilecek adımlar gerekir:

1. Yükseltilmiş bir komut isteminden çalıştırın `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` .
1. WSUS hizmetini tüm WSUS sunucularında yeniden başlatın.

KB 3159706 ' nin yükleme sonrasında el ile adımlar olduğunu fark etmezseniz veya KB 3159706 ' yi yüklemeden önce Windows 10 1607 ' ye yükseltme ile eşitledikten sonra, WSUS konsoluna bağlanma ve yükseltmeyi dağıtma sorunlarıyla karşılaşırsınız. İstemci, yükseltme dosyasını indirdiği zaman, bir [ **0Xc1800118** hata kodu](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus)alır.

Çözüm adımları KB 3095113 yüklemesinden önceki yükseltmeleri eşitlemeye yönelik çözünürlüğe benzer olduğundan, her iki adım kümesini de sonraki bölümde tek bir çözünürlükte birleştirdik.
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>KB 3095113 veya KB 3159706 ' ü yüklemeden önce yükseltmeleri eşitlemeden kurtarmak için

0xc1800118 hatasını ve "hata: geçersiz sertifika imzası" sorununu çözmek için aşağıdaki adımları izleyin:

1. Hem WSUS hem de Configuration Manager **yükseltmeler** sınıflandırmasını devre dışı bırakın. Bu yönergeler tarafından yönlendirilene kadar eşitlemenin gerçekleşmesini istemezsiniz.  
   - Üst düzey sitedeki yazılım güncelleştirme noktası bileşen özelliklerindeki **yükseltmeler** sınıflandırmasının işaretini kaldırın.
     - Daha fazla bilgi için bkz. [sınıflandırmaları ve ürünleri yapılandırma](../get-started/configure-classifications-and-products.md).
   - [ **Seçenekler** sayfasında](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations), **ürünler ve sınıflandırmalar** altındaki **WSUS sınıflandırmalarının** seçimini kaldırın veya yönetici olarak çalışan PowerShell ISE 'yi kullanın.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - WSUS veritabanını birden çok WSUS sunucusu arasında paylaşırsanız, her veritabanı için yalnızca bir kez **yükseltmeler** seçeneğinin işaretini kaldırmanız gerekir.  
1. Her WSUS sunucusunda, yükseltilmiş bir komut isteminden şunu çalıştırın: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` . Ardından WSUS hizmetini WSUS sunucusunda yeniden başlatın.
   -  WSUS, hizmet verme 'nin gerekli olup olmadığını kontrol etmeden önce veritabanını [tek kullanıcı moduna](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) koyar. Hizmet, denetim sonuçlarına göre çalışır veya çalışmaz. Daha sonra, veritabanı birden çok kullanıcı moduna geri konur. 
   - WSUS veritabanını birden çok WSUS sunucusu arasında paylaşırsanız, bu hizmeti her bir veritabanı için yalnızca bir kez yapmanız gerekir.
1. Yönetici olarak çalışan PowerShell ıSE 'yi kullanarak her WSUS veritabanından tüm Windows 10 yükseltmelerini silin.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Yazılım güncelleştirme noktalarınız tarafından kullanılan WSUS veritabanlarının her birinden tbFile tablosundan dosya silin. WSUS veritabanında SQL Server Management Studio ' den aşağıdaki komutları çalıştırın:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Configuration Manager en üst düzey sitenizde yazılım güncelleştirmeleri eşitlemesini başlatın ve bunun tamamlanmasını bekleyin. **Yükseltmeleri**kaldırdığımızda sınıflandırmalarla bir değişiklik yaptığımız için tam eşitleme gerçekleşir Configuration Manager. (Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini Synchronize](../get-started/synchronize-software-updates.md).
1. Yazılım güncelleştirme noktası bileşen özellikleri ' nde **yükseltmeler** sınıflandırmasını seçin. Ardından, **YÜKSELTMELERI** WSUS ve Configuration Manager geri getirmek için başka bir yazılım güncelleştirmeleri eşitlemesi başlatın. Configuration Manager sizin için yapabileceğinizden, WSUS 'de **yükseltmeler** sınıflandırmasını etkinleştirmeniz gerekmez.
1. İstemcileriniz bir yükseltmeyi indirirken **0Xc1800118** hata kodu aldıysa, Windows Update Aracısı tarafından kullanılan veri deposunu silmeniz gerekir. Ayrıca, cihazdaki gizli ~ BT klasörünü de silmeniz gerekebilir. İstemci bir dahaki sefer tarandığında, Delta yerine WSUS sunucusunda tam tarama olacaktır. Aşağıdaki örnek betiğe benzer bir PowerShell betiği kullanabilirsiniz:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Sonraki adımlar
[Yazılım güncelleştirme yönetimine hazırlanma](../get-started/prepare-for-software-updates-management.md)
