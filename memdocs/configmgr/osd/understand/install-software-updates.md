---
title: Yazılım Güncelleştirmelerini Yükle
titleSuffix: Configuration Manager
description: Görev dizisi adımını kullanma önerileri Configuration Manager yazılım güncelleştirmelerini yükler.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 73acd43ef9d7924682de9df66487c5a04297e640
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697509"
---
# <a name="install-software-updates"></a>Yazılım Güncelleştirmelerini Yükle

*Uygulama hedefi: Configuration Manager (geçerli dal)*

**Yazılım güncelleştirmelerini yükler** adımı genellikle Configuration Manager görev sıralarında kullanılır. İşletim sistemini yüklerken veya güncelleştirirken güncelleştirmeleri taramak ve dağıtmak için yazılım güncelleştirmeleri bileşenlerini tetikler. Bu adım, uzun zaman aşımı gecikmeleri veya eksik güncelleştirmeler gibi bazı müşterilere yönelik güçlüklere neden olabilir. Bu makaledeki bilgileri, bu adımla ilgili yaygın sorunları azaltmaya ve şeyler yanlış olduğunda daha iyi sorun gidermeye yardımcı olması için kullanın.

Adım hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini Install](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>Öneriler

Bu işlemin başarılı olması için aşağıdaki önerileri kullanın:

- [Çevrimdışı bakım kullan](#use-offline-servicing)
- [Tek Dizin](#single-index)
- [Görüntü boyutunu azalt](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Çevrimdışı bakım kullan

Uygun yazılım güncelleştirmelerini düzenli olarak görüntü dosyalarınıza yüklemek için Configuration Manager kullanın. Bu yöntem daha sonra görev dizisi sırasında yüklemeniz gereken güncelleştirme sayısını azaltır.

Daha fazla bilgi için bkz. [bir görüntüye yazılım güncelleştirmelerini uygulama](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Tek Dizin

Birçok görüntü dosyası, farklı Windows sürümleri gibi birden çok dizin içerir. Görüntü dosyasını, gerek duyduğunuz tek bir dizine küçültün. Bu uygulama, görüntüye yazılım güncelleştirmelerinin uygulanması için geçen süreyi azaltır. Ayrıca, görüntü boyutunu azaltmak için bir sonraki öneriyi de sağlar.

Sürüm 1902 ' den başlayarak, siteye bir işletim sistemi görüntüsü eklediğinizde bu süreci otomatikleştirin. Daha fazla bilgi için bkz. [işletim sistemi görüntüsü ekleme](../get-started/manage-operating-system-images.md#BKMK_AddOSImages).<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a> Görüntü boyutunu azalt

Görüntüye yazılım güncelleştirmeleri uyguladığınızda, yenisiyle değiştirilen tüm güncelleştirmeleri kaldırarak çıktıyı iyileştirin. DıSM komut satırı aracını kullanın, örneğin:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

Sürüm 1902 ' den başlayarak, bu işlemi otomatikleştirmek için yeni bir seçenek vardır. Daha fazla bilgi için bkz. [iyileştirilmiş görüntü Bakımı](../get-started/manage-operating-system-images.md#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Görüntü Mühendisliği kararları

Görüntüleme işleminizi tasarlarken, yazılım güncelleştirmelerinin yüklenmesini etkileyebilecek çeşitli seçenekler vardır:

- [Görüntüyü düzenli aralıklarla yeniden yakala](#bkmk_goldimage)  
- [Çevrimdışı bakım kullan](#bkmk_offline)  
- [Yalnızca varsayılan görüntüyü kullan](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a> Görüntüyü düzenli aralıklarla yeniden yakala

Özel bir işletim sistemi görüntüsünü düzenli bir zamanlamaya göre yakalamaya yönelik otomatikleştirilmiş bir işleminiz vardır. Bu yakalama görev dizisi en son yazılım güncelleştirmelerini yüklüyor. Bu güncelleştirmeler toplu, toplu olmayan ve hizmet yığını güncelleştirmeleri (SSU) gibi diğer kritik güncelleştirmeleri içerebilir. Dağıtım görev sırası, yakalama sonrasında ek güncelleştirmeler yüklenir.

Bu işlemle ilgili daha fazla bilgi için bkz. bir [işletim sistemini yakalamak için görev dizisi oluşturma](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

#### <a name="advantages"></a>Avantajlar

- Dağıtım sırasında zaman ve bant genişliğini kaydeden, istemci başına dağıtım zamanında uygulanacak daha az güncelleştirme
- Yeniden başlatmalar nedeniyle endişelenmeye yönelik daha az güncelleştirme
- Kuruluş için özelleştirilmiş görüntü
- Dağıtım zamanında daha az değişken

#### <a name="disadvantages"></a>Dezavantajlar

- Görüntü oluşturma ve yakalama süresi, genellikle otomatikleştirilse de
- Görüntüyü dağıtım noktalarına dağıtmak için artan süre (etkin dağıtımlar için kesinti olarak görülemeyen)
- Ön üretim ortamları üzerinden test etmek için gereken süre, işletim sistemi düzeltme döngüsüyle daha uzun olabilir. bu durum, güncelleştirilmiş görüntüyü ilgisiz hale getirir


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a> Çevrimdışı bakım kullan

Resimlerinize yazılım güncelleştirmeleri uygulamak için Configuration Manager zamanlayın.

Daha fazla bilgi için bkz. [bir görüntüye yazılım güncelleştirmelerini uygulama](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Avantajlar

- Dağıtım sırasında zaman ve bant genişliğini kaydeden, istemci başına dağıtım zamanında uygulanacak daha az güncelleştirme
- Yeniden başlatmalar nedeniyle endişelenmeye yönelik daha az güncelleştirme
- Bakım sürecini sitede zamanlayabilirsiniz

#### <a name="disadvantages"></a>Dezavantajlar

- Güncelleştirmelerin el ile seçimi
- Görüntüyü dağıtım noktalarına dağıtmak için artırılan süre
- Yalnızca CBS tabanlı güncelleştirmeleri destekler. Microsoft 365 Apps güncelleştirmeleri uygulanamıyor

> [!Tip]  
> PowerShell kullanarak yazılım güncelleştirmelerinin seçimini otomatikleştirebilirsiniz. Güncelleştirmelerin listesini almak için [Get-CMSoftwareUpdate](/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) cmdlet 'ini kullanın. Ardından, çevrimdışı bakım zamanlamasını oluşturmak için [New-Cmoperatingsystemımageupdateschedule](/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) cmdlet 'ini kullanın. Aşağıdaki örnek, bu eylemi otomatikleştirmek için bir yöntemi gösterir:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a> Yalnızca varsayılan görüntüyü kullan

Dağıtım görev dizilerinizdeki varsayılan Windows Install. wim görüntü dosyasını kullanın.

#### <a name="advantages"></a>Avantajlar

- Olası bir sorun olarak görüntü bozulması riskini azaltan bilinen bir iyi kaynak
- Olası bir sorun olarak görüntüdeki değişiklikleri ortadan kaldırır

#### <a name="disadvantages"></a>Dezavantajlar

- Dağıtım sırasında yüksek güncelleştirme hacmi için olası
- Her cihaz için daha fazla dağıtım süresi
- Gerekli özelleştirmeler olmayabilir, özelleştirmek için ek görev dizisi adımları gerekir



## <a name="flowchart"></a>Akış Çizelgesi

Bu akış çizelgesi diyagramı, yazılım güncelleştirmelerini yükler adımını bir görev dizisine dahil ettiğinizde süreci gösterir.

[Diyagramı tam boyutta görüntüleme](media/ts-step-install-software-updates.svg)

![Yazılım güncelleştirmelerini yükler görev dizisi adımının akış çizelgesi diyagramı](media/ts-step-install-software-updates.svg)  

1. **İşlem istemcide başlatılır**: istemcide çalışan bir görev sırası, yazılım güncelleştirmelerini yükler adımını içerir.
2. **Ilkeleri derle ve değerlendir**: istemci, tüm yazılım GÜNCELLEŞTIRME Ilkelerini WMI RequestedConfigs ad alanına derler. (Cıagent. log)
3. *Bu örnek ilk çağrılışında mi?*  
    1. **Evet**: **tam taramaya** git  
    2. **Hayır**: * [yazılım güncelleştirmelerini önbelleğe alınmış tarama sonuçlarından değerlendirme](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)seçeneğiyle yapılandırılmış adımdır mi?*
        1. **Evet**: **önbelleğe alınan sonuçlardan taramaya** git
        2. **Hayır**: **tam taramaya** git
4. Tarama işlemi: önbelleğe alınan sonuçlardan tam tarama veya tarama işlemleri paralel olarak görüntüleniyor.
    1. **Tam tarama**: görev dizisi altyapısı, *tam* tarama yapmak için güncelleştirme taraması API 'si aracılığıyla yazılım güncelleştirme aracısını çağırır. (WUAHandler. log, ScanAgent. log)  
        1. **Toplam aracı taraması-tam**: WSUS çalıştıran yazılım güncelleştirme noktasıyla iletişim kuran Windows Update ARACıSı (WUA) aracılığıyla normal tarama işlemi. Geçerli güncelleştirmeleri yerel güncelleştirme deposuna ekler. (WindowsUpdate. log, UpdateStore. log)
    2. **Önbelleğe alınmış sonuçlardan tarama**: görev dizisi altyapısı, önbelleğe alınmış meta verilere karşı tarama yapmak Için güncelleştirme taraması API 'si aracılığıyla yazılım güncelleştirme aracısını çağırır. (WUAHandler. log, ScanAgent. log)
        1. **Toplam aracı taraması-önbelleğe alınmış**: Windows Update ARACıSı (WUA), yerel güncelleştirme deposunda zaten önbelleğe alınmış güncelleştirmelere karşı denetler. (WindowsUpdate. log, UpdateStore. log)
    3. **Tarama zamanlayıcısını Başlat**: görev sırası altyapısı bir Zamanlayıcı başlatır ve bekler. (Bu işlem, önbelleğe alınmış sonuçları tam tarama veya tarama işlemi ile paralel olarak gerçekleşir.)
        1. **İzleme**: görev SıRASı altyapısı Sum aracısını durum için izler.
        2. *Toplam aracıdan gelen yanıt nedir?*
            - **Devam ediyor**: Zamanlayıcı, [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)görev dizisi değişkeninde değere ulaştı mi? (Varsayılan 1 saat)
                - **Evet**: adım başarısız olur.
                - **Hayır**: **izlemeye** git
            - **Başarısız**: adım başarısız oldu.
            - **Tamam**: **güncelleştirme listesini numaralandırmaya** git
5. **Güncelleştirme listesini numaralandır**: Toplam Aracı, tarama tarafından döndürülen güncelleştirmelerin listesini, kullanılabilir veya zorunlu olduğunu belirlemek için sıralar.
6. *Tarama sonuçları listesinde herhangi bir güncelleştirme var mı?*
    - **Evet**: **güncelleştirmeleri yüklemeye** git
    - **Hayır**: yüklenecek bir şey yok, adım başarıyla tamamlandı.
7. Dağıtım işlemi: güncelleştirme yüklemesi işlemi, dağıtım izleme işlemiyle paralel olarak gerçekleşir.
    1. **Güncelleştirmeleri yükler**: görev dizisi altyapısı, tüm kullanılabilir veya yalnızca zorunlu güncelleştirmeleri yüklemek Için, güncelleştirme dağıtım API 'SI aracılığıyla toplam aracısını çağırır. Bu davranış, **yükleme-zorunlu yazılım güncelleştirmeleri Için gerekli** ' ı veya **yükleme Için hazır olan tüm yazılım güncelleştirmelerini**seçip seçmeksizin adımın yapılandırmasına dayanır. Bu davranışı [Smsınstallupdatetarget](task-sequence-variables.md#SMSInstallUpdateTarget) değişkenini kullanarak da belirtebilirsiniz.
        1. **Toplam aracı yüklemesi**: Standart içerik indirmesi ile, mevcut önbelleğe alınmış güncelleştirme listesini kullanan normal yükleme işlemi. Windows Update Aracısı (WUA) aracılığıyla güncelleştirmeyi yükler. (UpdatesDeployment. log, UpdatesHandler. log, WuaHandler. log, WindowsUpdate. log)
    2. **Dağıtım Zamanlayıcısını başlatma ve ilerleme durumunu gösterme**: görev sırası altyapısı bir yükleme zamanlayıcısını başlatır, %10 ' daki alt Ilerlemeyi TS ilerleme Kullanıcı arabiriminde gösterir ve bekler.
        1. **İzleme**: görev dizisi altyapısı, durum için toplam aracısını yoklar.
        2. *Toplam aracıdan gelen yanıt nedir?*
            - **Devam ediyor**: *yükleme işlemi 8 saat boyunca etkin değil mi?*
                - **Evet**: adım başarısız olur.
                - **Hayır**: **izlemeye** git
            - **Başarısız**: adım başarısız oldu.
            - **Tamam**: şuraya git *ayarı, **önbelleğe alınmış tarama sonuçlarından yazılım güncelleştirmelerini değerlendirme**seçeneği ile yapılandırılır.*


### <a name="timeouts"></a>Zaman aşımları

Diyagramda, bu adım için uygulanan zaman aşımı değişkenlerinin ikisi bulunur. Diğer bileşenlerden bu işlemi etkileyebilecek diğer standart zamanlayıcılar vardır.

- Güncelleştirme taraması zaman aşımı: 1 saat (Smsts. log)  
- Konum isteği zaman aşımı: 1 saat (LocationServices. log, CAS. log)  
- İçerik indirme zaman aşımı: 1 saat (DTS. log)  
- Etkin olmayan dağıtım noktası zaman aşımı: 1 saat (LocationServices. log, CAS. log)  
- Etkin olmayan toplam yüklemesi zaman aşımı: 8 saat (Smsts. log)  



## <a name="troubleshooting"></a>Sorun giderme

Bu adımla ilgili sorunları gidermenize yardımcı olması için aşağıdaki kaynakları ve ek bilgileri kullanın:

- Yazılım güncelleştirme dağıtımlarınızı görev sırası dağıtımıyla aynı koleksiyona hedeflediğinizden emin olun.  

- Yazılım güncelleştirme noktalarını sınır gruplarına eklediğinizden emin olun. Daha fazla bilgi için bu [Microsoft desteği makalesine](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager)bakın.  

- Yazılım güncelleştirme yönetimi sürecini gidermenize yardımcı olması için bkz. [yazılım güncelleştirmesi yönetimi sorun giderme](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Genel performansı artırmaya yardımcı olmak için, yazılım güncelleştirme kataloğunun boyutunu küçültün. Örnek:  

    - Gereksiz sınıflandırmaları, ürünleri ve dilleri kaldırın. Daha fazla bilgi için bkz. [eşitlenmek için sınıflandırmaları ve ürünleri yapılandırma](../../sum/get-started/configure-classifications-and-products.md).  

    - Site veritabanını yeniden dizinle istatistikleri yeniden derleyin. Daha fazla bilgi için bkz. [performans ve ölçek kılavuzu teknik incelemesi Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Gereksiz güncelleştirmeleri reddetme, örneğin:
        - Yenisiyle değiştirildi (sürüm 1810 ' den başlayarak Configuration Manager Bu eylemi sizin için yapar. Daha fazla bilgi için bkz. [sürüm 1810 ' den başlayarak WSUS temizleme davranışı](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810).)
        - Itanium
        - Beta
        - Sonraki sürüm
        - ARM
        - Dağıtmayan Windows sürümleri