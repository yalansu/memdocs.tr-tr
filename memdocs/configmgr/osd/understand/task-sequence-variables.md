---
title: Görev dizisi değişkeni başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager görev sırasını denetlemek ve özelleştirmek için değişkenler hakkında bilgi edinin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3ddd1a4b59ba750e9fca5f8386762b4a5dddb13
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429799"
---
# <a name="task-sequence-variables"></a>Görev dizisi değişkenleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, tüm kullanılabilir değişkenler için alfabetik sırada bir başvurudur. Belirli bir değişkeni bulmak için tarayıcı **bul** işlevini (genellikle **CTRL**  +  **F**) kullanın. Değişken, belirli bir adıma özgü ise notlar. [Görev dizisi adımındaki](task-sequence-steps.md) makale her bir adıma özgü değişkenlerin listesini içerir.

Daha fazla bilgi için bkz. [görev dizisi değişkenlerini kullanma](using-task-sequence-variables.md).

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a>Görev dizisi değişken başvurusu

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a>_OSDDetectedWinDir

Görev dizisi, Windows PE başladığında bilgisayarın sabit sürücülerinde önceki bir işletim sistemi yüklemesi için tarar. Windows klasörünün konumu bu değişkende depolanır. Görev dizinizi bu değeri ortamdan alacak ve yeni işletim sistemi yüklemesinde kullanılmak üzere aynı Windows klasörü konumunu belirtmek üzere kullanacak şekilde yapılandırabilirsiniz.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a>_OSDDetectedWinDrive

Görev dizisi, Windows PE başladığında bilgisayarın sabit sürücülerinde önceki bir işletim sistemi yüklemesi için tarar. İşletim sisteminin yüklendiği sabit sürücü konumu bu değişkende depolanır. Görev dizinizi bu değeri ortamdan alacak ve yeni işletim sistemi için aynı sabit sürücü konumunu belirtmek üzere kullanacak şekilde yapılandırabilirsiniz.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a>_OSDMigrateUsmtPackageID

*[Kullanıcı durumunu yakala](task-sequence-steps.md#BKMK_CaptureUserState) adımı için geçerlidir.*

(giriş)

USMT dosyalarını içeren Configuration Manager paketinin paket KIMLIĞINI belirtir. Bu değişken gereklidir.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a>_OSDMigrateUsmtRestorePackageID

*[Kullanıcı durumunu geri yükle](task-sequence-steps.md#BKMK_RestoreUserState) adımı için geçerlidir.*

(giriş)

USMT dosyalarını içeren Configuration Manager paketinin paket KIMLIĞINI belirtir. Bu değişken gereklidir.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a>_SMSTSAdvertID

Çalışan geçerli görev dizisi dağıtımının bağımsız kimliğini depolar. Configuration Manager yazılım dağıtımı dağıtım KIMLIĞI ile aynı biçimi kullanır. Görev dizisi tek başına ortamdan çalıştırılıyorsa değişken tanımlı değildir.

#### <a name="example"></a>Örnek

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a>_SMSTSAssetTag

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayarın varlık etiketini belirtir.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a>_SMSTSBootImageID

Çalışan geçerli görev dizisi bir Önyükleme yansıma paketine başvuruyorsa, bu değişken önyükleme görüntüsü paket KIMLIĞINI depolar. Görev sırası bir önyükleme görüntü paketine başvurmazsa, bu değişken ayarlı değildir.

#### <a name="example"></a>Örnek

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a>_SMSTSBootUEFI

Görev sırası, UEFı modundaki bir bilgisayarı algıladığında bu değişkeni ayarlar.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a>_SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
Görev sırası, yerel sürücüdeki içeriği önbelleğe aldığında bu değişkeni ayarlar. Değişken, önbelleğin yolunu içerir. Bu değişken yoksa, önbellek yoktur.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a>_SMSTSClientGUID

Configuration Manager istemci GUID değerini depolar. Görev dizisi tek başına medyadan çalışıyorsa, bu değişken ayarlı değildir.

#### <a name="example"></a>Örnek

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a>_SMSTSCurrentActionName

O an çalışan görev sırası adımının adını belirtir. Bu değişken, görev sırası yöneticisi her adımı çalıştırmadan önce ayarlanır.

#### <a name="example"></a>Örnek

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a>_SMSTSDefaultGateways

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayar tarafından kullanılan varsayılan ağ geçitlerini belirtir.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a>_SMSTSDownloadOnDemand

Geçerli görev dizisi isteğe bağlı indirme modunda çalışıyorsa, bu değişken olur `true` . İsteğe bağlı indirme modu, görev dizisi yöneticisinin içeriği yalnızca içeriğe erişmesi gerektiğinde yerel olarak indirdiği anlamına gelir.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a>_SMSTSInWinPE

Geçerli görev dizisi adımı Windows PE 'de çalışırken, bu değişken olur `true` . Geçerli işletim sistemi ortamını öğrenmek için bu görev dizisi değişkenini test edin.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a>_SMSTSIPAddresses

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayar tarafından kullanılan IP adreslerini belirtir.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a>_SMSTSLastActionName

Çalıştırılan son eylemin adını depolar. Bu değişken **_SMSTSLastActionRetCode**ile ilgilidir. Görev sırası bu değerleri Smsts. log dosyasına kaydeder. Bu değişken, görev dizisinde sorun giderirken faydalıdır. Bir adım başarısız olduğunda, özel bir betik dönüş koduyla birlikte adım adını içerebilir.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a>_SMSTSLastActionRetCode

Çalıştırılan son eylemden dönüş kodunu depolar. Bu değişken, bir sonraki adımın çalıştırılıp çalıştırılmadığını belirlemek için bir koşul olarak kullanılabilir.

#### <a name="example"></a>Örnek

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a>_SMSTSLastActionSucceeded

- Son adım başarılı olursa bu değişken olur `true` .  

- Son adım başarısız olduysa, bu `false` .  

- Görev dizisi son eylemi atladığında, adım devre dışı bırakıldığından veya ilişkili koşul **false**olarak değerlendirildiğinden, bu değişken sıfırlanmaz. Yine de önceki eyleme ait değeri barındırır.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a>_SMSTSLastContentDownloadLocation

<!-- 2840337 -->
Sürüm 1906 ' den başlayarak bu değişken, görev dizisinin indirilen veya içeriği indirmeye çalıştığı son konumu içerir. Bu içerik konumu için istemci günlüklerini ayrıştırmak yerine bu değişkeni inceleyin.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a>_SMSTSLaunchMode

Görev dizisinin aşağıdaki yöntemlerden biri aracılığıyla başlatıldığını belirtir:  

- **SMS**: bir kullanıcı tarafından yazılım merkezinden başlatıldığında olduğu gibi Configuration Manager istemcisi
- **UFD**: eski USB medya
- **UFD + Format**: daha yeni USB medyası
- **CD**: önyüklenebilir CD
- **DVD**: ÖNYÜKLENEBILIR bir DVD
- **PXE**: PXE ile ağ önyüklemesi
- **HD**: sabit diskte önceden hazırlanan medya

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a>_SMSTSLogPath

Günlük dizininin tam yolunu depolar. Görev dizisi adımlarının eylemlerini günlüğe kaydetmelerini öğrenmek için bu değeri kullanın. Bu değer bir sabit sürücü kullanılamadığında ayarlanamaz.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a>_SMSTSMacAddresses

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayar tarafından kullanılan MAC adreslerini belirtir.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a>_SMSTSMachineName

Bilgisayar adını depolar ve belirtir. Görev dizisinin tüm durum iletilerini günlüğe kaydetmek için kullanacağı bilgisayarın adını depolar. Yeni işletim sisteminde bilgisayar adını değiştirmek için [OSDComputerName](#OSDComputerName-input) değişkenini kullanın.

### <a name="_smstsmake"></a><a name="SMSTSMake"></a>_SMSTSMake

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayarın markasını belirtir.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a>_SMSTSMDataPath

[SMSTSLocalDataDrive](#SMSTSLocalDataDrive) değişkeni tarafından tanımlanan yolu belirtir. Bu yol, görev dizisinin çalışırken hedef bilgisayardaki geçici önbellek dosyalarını nerede depoladığını belirtir. Görev dizisi başlamadan önce SMSTSLocalDataDrive tanımladığınızda, örneğin bir koleksiyon değişkenini ayarlayarak Configuration Manager, görev sırası başladıktan sonra _SMSTSMDataPath değişkenini tanımlar.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a>_SMSTSMediaType

Yüklemeyi başlatmak için kullanılan medya türünü belirtir. Medya türlerine örnek olarak Önyükleme Medyası, Tam Medya, PXE ve Önceden Hazırlanmış Medya verilebilir.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a>_SMSTSModel

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayarın modelini belirtir.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a>_SMSTSMP

Configuration Manager yönetim noktasının URL 'sini veya IP adresini depolar.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a>_SMSTSMPPort

Configuration Manager yönetim noktasının bağlantı noktası numarasını depolar.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a>_SMSTSOrgName

Görev dizisinin ilerleme durumu iletişim kutusunda görüntülediği marka başlığı adını depolar.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a>_SMSTSOSUpgradeActionReturnCode

*[İşletim sistemini yükseltme](task-sequence-steps.md#BKMK_UpgradeOS) adımı için geçerlidir.*

Başarılı veya başarısız olduğunu göstermek için Windows Kurulumu döndürdüğü çıkış kodu değerini depolar. Bu değişken `/Compat` komut satırı seçeneğiyle yararlı olur.

#### <a name="example"></a>Örnek

Yalnızca uyumluluk taraması tamamlandığında, hata veya başarı çıkış koduna bağlı olarak sonraki adımlarda işlem yapın. Başarı durumunda yükseltmeyi başlatın. Ya da ortamda donanım envanteriyle toplanacak bir işaret ayarlayın. Örneğin, bir dosya ekleyin veya bir kayıt defteri anahtarı ayarlayın. Yükseltmeye hazırlanma veya yükseltmeden önce eylem gerektiren bilgisayarların bir koleksiyonunu oluşturmak için bu işaretleyiciyi kullanın.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a>_SMSTSPackageID

Çalışan geçerli görev dizisi kimliğini depolar. Bu KIMLIK Configuration Manager paket KIMLIĞI ile aynı biçimi kullanır.

#### <a name="example"></a>Örnek

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a>_SMSTSPackageName

Çalışan geçerli görev dizisi adını depolar. Bir Configuration Manager yönetici görev dizisini oluştururken bu adı belirtir.

#### <a name="example"></a>Örnek

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a>_SMSTSRunFromDP

`true`Geçerli görev sırası, çalıştırma-dağıtım noktası modunda çalışıyorsa olarak ayarlayın. Bu mod, görev dizisi yöneticisinin gerekli paket paylaşımlarını dağıtım noktasından alacağı anlamına gelir.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a>_SMSTSSerialNumber

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayarın seri numarasını belirtir.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a>_SMSTSSetupRollback

Windows Kurulumu yerinde yükseltme sırasında geri alma işlemi gerçekleştirip gerçekleştirmediğini belirtir. Değişken değerleri `true` veya olabilir `false` .

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a>_SMSTSSiteCode

Configuration Manager sitesinin site kodunu depolar.

#### <a name="example"></a>Örnek

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a>_SMSTSTimezone

Bu değişken, saat dilimi bilgilerini aşağıdaki biçimde depolar:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Örnek

Saat dilimi **Doğu saati (ABD ve Kanada)** için:

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a>_SMSTSType

O sırada çalışan görev dizisinin türünü belirtir. Aşağıdaki değerlerden birine sahip olabilir:  

- **1**: genel görev sırası
- **2**: BIR işletim sistemi dağıtımı görev dizisi

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a>_SMSTSUseCRL

Görev sırası, yönetim noktasıyla iletişim kurmak için HTTPS kullandığında, bu değişken sertifika iptal listesini (CRL) kullanıp kullanmadığını belirtir.

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a>_SMSTSUserStarted

Bir kullanıcının görev dizisini başlatılıp başlatılamayacağını belirtir. Bu değişken, yalnızca görev dizisi yazılım merkezi 'nden başlatılmışsa ayarlanır. Örneğin, [_SMSTSLaunchMode](#SMSTSLaunchMode) olarak ayarlanmışsa `SMS` .

Bu değişken aşağıdaki değerlere sahip olabilir:  

- `true`: Görev dizisinin yazılım merkezi 'nden bir kullanıcı tarafından el ile başlatıldığını belirtir.  

- `false`: Görev dizisinin Configuration Manager Zamanlayıcı tarafından otomatik olarak başlatıldığını belirtir.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a>_SMSTSUseSSL

Görev dizisinin Configuration Manager yönetim noktasıyla iletişim kurmak için SSL kullanıp kullanmadığını belirtir. Site sistemlerinizi HTTPS için yapılandırırsanız, değer olarak ayarlanır `true` .

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a>_SMSTSUUID

*[Dinamik değişkenleri ayarla](task-sequence-steps.md#BKMK_SetDynamicVariables) adımı için geçerlidir.*

Bilgisayarın UUID’sini belirtir.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a>_SMSTSWTG

Bilgisayarın Windows To Go cihazı olarak çalışıp çalışmadığını belirtir.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a>_TS_CRMEMORY

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Minimum bellek (MB)** denetiminin true ( `1` ) veya false () döndürdüğünden emin olup olmadığı için salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a>_TS_CRSPEED

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Minimum işlemci hızı (MHz)** denetiminin true ( `1` ) veya false () döndürdüğünden emin olup olmadığı için salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a>_TS_CRDISK

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Minimum boş disk alanı (MB)** denetiminin true ( `1` ) veya false () olarak döndürülüp döndürülmeyeceğini bir salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a>_TS_CROSTYPE

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Geçerli işletim sisteminin yenilenmesinin** true ( `1` ) veya false () olarak döndürüldüğünden emin olmak için salt okunurdur bir değişken `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a>_TS_CRARCH

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Geçerli işletim sistemi denetiminin mimarisinin** true ( `1` ) veya false () döndürdüğünden bağımsız olarak salt okunurdur bir değişken `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a>_TS_CRMINOSVER

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**En düşük işletim sistemi sürümü** denetiminin true ( `1` ) veya false () döndürülüp döndürülmeyeceğini bir salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a>_TS_CRMAXOSVER

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**En yüksek işletim sistemi sürümü** denetiminin true ( `1` ) veya false () döndürülüp döndürülmeyeceğini bir salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a>_TS_CRCLIENTMINVER

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**En düşük istemci sürümü** denetiminin true ( `1` ) veya false () döndürülüp döndürülmeyeceğini bir salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a>_TS_CROSLANGUAGE

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Geçerli işletim sistemi denetiminin dilin** true ( `1` ) veya false () döndürdüğünden emin olup olmadığı için salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a>_TS_CRACPOWER

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**AC güç takılı** denetiminin true ( `1` ) veya false () döndürdüğünden emin olmak için salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a>_TS_CRNETWORK

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Ağ bağdaştırıcısı bağlı** denetiminin true ( `1` ) veya false () döndürdüğünden, salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a>_TS_CRWIRED

*2002 sürümünden başlayarak* <!--6005561-->  
*[Hazırlık denetimi](task-sequence-steps.md#BKMK_CheckReadiness) adımını uygular.*

**Ağ bağdaştırıcısının kablosuz denetim olmadığında** true ( `1` ) veya false () döndürülmeyeceğini bir salt okunurdur `0` . Denetimi etkinleştirmezseniz, salt okunurdur bu değişkenin değeri boştur.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a>_TSAppInstallStatus

Görev sırası bu [değişkeni uygulama yükleme adımı sırasında](task-sequence-steps.md#BKMK_InstallApplication) uygulamanın yükleme durumuyla ayarlar. Aşağıdaki değerlerden birini ayarlar:  

- **Tanımsız**: uygulamayı yüklemeyi Çalıştır adımı çalıştırılmadı.  

- **Hata**: uygulama yüklemesi adımı sırasında bir hata nedeniyle en az bir uygulama başarısız oldu.  

- **Uyarı**: uygulama yüklemesi adımı sırasında hata oluşmadı. Bir gereksinim karşılanmadığı için bir veya daha fazla uygulama ya da gerekli bağımlılık yüklenmedi.  

- **Başarılı**: uygulama yüklemesi adımı sırasında hata veya uyarı algılanmadı.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a>_TSSecureBoot

*2002 sürümünden başlayarak* <!--5842295-->  

UEFı özellikli bir cihazda güvenli önyükleme durumunu öğrenmek için bu değişkeni kullanın. Değişkeni aşağıdaki değerlerden birine sahip olabilir:

- `NA`: İlişkili kayıt defteri değeri yok, bu, cihazın güvenli önyüklemeyi desteklemediği anlamına gelir.
- `Enabled`: Cihazda güvenli önyükleme etkin.
- `Disabled`: Cihazda güvenli önyükleme devre dışı bırakıldı.

### <a name="osdadapter"></a><a name="OSDAdapter"></a>OSDAdapter

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Bu görev dizisi değişkeni bir *dizi* değişkenidir. Dizideki her öğe, bilgisayardaki tek bir ağ bağdaştırıcısının ayarlarını temsil eder. Dizi değişkeni adını sıfır tabanlı ağ bağdaştırıcısı diziniyle ve özellik adıyla birleştirerek her bir bağdaştırıcının ayarlarına erişin.

Ağ ayarlarını Uygula adımı birden çok ağ bağdaştırıcısı yapılandırıyorsa, değişken adındaki dizin **1** ' i kullanarak *ikinci* ağ bağdaştırıcısının özelliklerini tanımlar. Örneğin: OSDAdapter1EnableDHCP, Osdadapter1ıpaddresslist ve OSDAdapter1DNSDomain.

Yapılandırma adımı için *ilk* ağ bağdaştırıcısının özelliklerini tanımlamak üzere aşağıdaki değişken adlarını kullanın:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Bu ayar zorunludur. Olası değerler: `True` veya `False`. Örneğin:

`true`: bağdaştırıcı için dinamik ana bilgisayar Yapılandırma Protokolü 'Nü (DHCP) etkinleştirin

#### <a name="osdadapter0ipaddresslist"></a>Osdadapter0ıpaddresslist: bağdaştırıcı

Bağdaştırıcının IP adreslerinin virgülle ayrılmış listesi. **EnableDHCP** , olarak ayarlanmadığı takdirde bu özellik yoksayılır `false` . Bu ayar zorunludur.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Alt ağ maskelerinin virgülle ayrılmış listesi. **EnableDHCP** , olarak ayarlanmadığı takdirde bu özellik yoksayılır `false` . Bu ayar zorunludur.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

IP ağ geçidi adreslerinin virgülle ayrılmış listesi. **EnableDHCP** , olarak ayarlanmadığı takdirde bu özellik yoksayılır `false` . Bu ayar zorunludur.

#### <a name="osdadapter0dnsdomain"></a>Osdadapter0dnsdomain: bağdaştırıcı

Bağdaştırıcı için etki alanı adı sistemi (DNS) etki alanı.

#### <a name="osdadapter0dnsserverlist"></a>Osdadapter0dnsserverlist: bağdaştırıcı

Bağdaştırıcı için DNS sunucularının virgülle ayrılmış listesi. Bu ayar zorunludur.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

`true`BAĞDAŞTıRıCıSıNıN IP ADRESINI DNS 'de kaydetmek için olarak ayarlayın.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

`true`DNS 'deki BAĞDAŞTıRıCıNıN IP adresini bilgisayar için tam DNS adı altında kaydetmek üzere olarak ayarlayın.

#### <a name="osdadapter0enableipprotocolfiltering"></a>Osdadapter0enableıpprotocolfiltering: bağdaştırıcıda

`true`BAĞDAŞTıRıCıSıNDA IP protokolü filtrelemeyi etkinleştirmek için olarak ayarlayın.

#### <a name="osdadapter0ipprotocolfilterlist"></a>Osdadapter0ıpprotocolfilterlist

IP üzerinden çalışmasına izin verilen protokollerin virgülle ayrılmış listesi. **EnableIPProtocolFiltering** değeri olarak ayarlandıysa bu özellik yoksayılır `false` .

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

`true`Bağdaştırıcı IÇIN TCP bağlantı noktası filtrelemeyi etkinleştirmek üzere olarak ayarlayın.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

TCP için erişim izinleri verilecek bağlantı noktalarının virgülle ayrılmış listesi. **EnableTCPFiltering** ayarı olarak ayarlandıysa bu özellik yoksayılır `false` .

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

TCP/IP üzerinden NetBIOS seçenekleri. Olası değerler aşağıdaki gibidir:  

- `0`: DHCP sunucusundan NetBIOS ayarlarını kullan  
- `1`: TCP/IP üzerinden NetBIOS 'u etkinleştir  
- `2`: TCP/IP üzerinden NetBIOS 'u devre dışı bırak  

#### <a name="osdadapter0enablewins"></a>Osdadapter0enablewıns

`true`Ad çözümlemesi IÇIN WINS kullanmak üzere olarak ayarlayın.

#### <a name="osdadapter0winsserverlist"></a>Osdadapter0wınsserverlist

WINS sunucusu IP adreslerinin virgülle ayrılmış listesi. **Enablewins** , olarak ayarlanmadığı takdirde bu özellik yoksayılır `true` .

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

Ayarları fiziksel ağ bağdaştırıcısı ile eşleştirmek için kullanılan MAC adresi.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

Ağ bağlantısı Denetim Masası programında göründüğü şekilde ağ bağlantısının adı. Ad, 0 ila 255 karakter uzunluğunda.

#### <a name="osdadapter0index"></a>Osdadapter0ındex

Ayarlar dizisindeki ağ bağdaştırıcısı ayarlarının dizini.

#### <a name="example"></a>Örnek

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **Osdadapter0ıpaddresslist: bağdaştırıcı** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a>OSDAdapterCount

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarda yüklü olan ağ bağdaştırıcılarının sayısını belirtir. **OSDAdapterCount** değerini ayarladığınızda, her bir bağdaştırıcı için tüm yapılandırma seçeneklerini de ayarlayın.

Örneğin, ilk bağdaştırıcı için **OSDAdapter0TCPIPNetbiosOptions** değerini ayarlarsanız, bu bağdaştırıcının tüm değerlerini yapılandırmanız gerekir.

Bu değeri belirtmezseniz, görev sırası tüm **Osdavdapter** değerlerini yoksayar.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a>Osdapplydriverbootcriticalcontentuniqueıd ayarlandıysa

*[Sürücü paketini Uygula](task-sequence-steps.md#BKMK_ApplyDriverPackage) adımı için geçerlidir.*

(giriş)

Sürücü paketinden yüklemek için yığın depolama cihazı sürücüsünün içerik kimliğini belirtir. Bu değişken belirtilmemişse, yığın depolama sürücüsü yüklenmez.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a>Osdapplydriverbootcriticalhandle donanım bileşeni

*[Sürücü paketini Uygula](task-sequence-steps.md#BKMK_ApplyDriverPackage) adımı için geçerlidir.*

(giriş)

Bir yığın depolama cihazı sürücüsünün yüklü olup olmadığını belirtir, bu değişken **SCSI**olmalıdır.

[Osdapplydriverbootcriticalhandle Contentuniqueıd](#OSDApplyDriverBootCriticalContentUniqueID) ayarlandıysa, bu değişken gereklidir.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a>Osdapplydriverbootcriticalhandle kimliği

*[Sürücü paketini Uygula](task-sequence-steps.md#BKMK_ApplyDriverPackage) adımı için geçerlidir.*

(giriş)

Yüklenecek yığın depolama cihazı sürücüsünün kritik başlatma kimliğini belirtir. Bu KIMLIK, cihaz sürücüsünün Txtsetup. OEM dosyasının **SCSI** bölümünde listelenir.

[Osdapplydriverbootcriticalhandle Contentuniqueıd](#OSDApplyDriverBootCriticalContentUniqueID) ayarlandıysa, bu değişken gereklidir.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a>Osdapplydriverbootkritikinfdosyası

*[Sürücü paketini Uygula](task-sequence-steps.md#BKMK_ApplyDriverPackage) adımı için geçerlidir.*

(giriş)

Yüklenecek yığın depolama sürücüsünün INF dosyasını belirtir.

[Osdapplydriverbootcriticalhandle Contentuniqueıd](#OSDApplyDriverBootCriticalContentUniqueID) ayarlandıysa, bu değişken gereklidir.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a>Osdadutoapplydriveren iyi eşleşme

*[Sürücüleri otomatik olarak Uygula](task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı için geçerlidir.*

(giriş)

Sürücü kataloğunda donanım cihazıyla uyumlu birden çok cihaz sürücüsü varsa, bu değişken adımın eylemini belirler.

#### <a name="valid-values"></a>Geçerli değerler

- `true`(varsayılan): yalnızca en iyi cihaz sürücüsünü yükler  

- `false`: Tüm uyumlu cihaz sürücülerini yüklerse ve Windows kullanılacak en iyi sürücüyü seçer  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a>Osdadutoapplydrivercategorylist

*[Sürücüleri otomatik olarak Uygula](task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı için geçerlidir.*

(giriş)

Sürücü kataloğu kategorisi benzersiz kimliklerinin virgülle ayrılmış listesi. **Sürücüyü otomatik olarak Uygula** adımı yalnızca belirtilen kategorilerden en az birinde bulunan sürücüleri dikkate alır. Bu değer isteğe bağlıdır ve varsayılan olarak ayarlı değildir. Sitedeki **SMS_CategoryInstance** nesnelerinin listesini numaralandırarak kullanılabilir kategori kimliklerini elde edin.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a>OSDBitLockerRebootCount

*[BitLocker 'ı devre dışı bırak](task-sequence-steps.md#BKMK_DisableBitLocker) adımını uygular.*

<!-- 4512937 -->
Sürüm 1906 ' den başlayarak, korumanın sürdürülme sayısını ayarlamak için bu değişkeni kullanın.

#### <a name="valid-values"></a>Geçerli değerler

İle arasında bir `1` tamsayı `15` .

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a>OSDBitLockerRebootCountOverride

*[BitLocker 'ı devre dışı bırak](task-sequence-steps.md#BKMK_DisableBitLocker) adımını uygular.*

<!-- 4512937 -->
Sürüm 1906 ' den başlayarak, bu değeri, Step veya [Osdbitlockerrebootcount](#OSDBitLockerRebootCount) değişkeni tarafından ayarlanan sayıyı geçersiz kılmak için ayarlayın. Diğer yöntemler yalnızca 1 ile 15 değerlerini kabul ederken, bu değişkeni 0 olarak ayarlarsanız, BitLocker süresiz olarak devre dışı kalır. Bu değişken, görev dizisi bir değer ayarladığında, ancak cihaz başına veya koleksiyon başına temelinde ayrı bir değer ayarlamak istediğinizde faydalıdır.

#### <a name="valid-values"></a>Geçerli değerler

İle arasında bir `0` tamsayı `15` .

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a>OSDBitLockerRecoveryPassword

*[BitLocker 'ı etkinleştir](task-sequence-steps.md#BKMK_EnableBitLocker) adımını uygular.*

(giriş)

**BitLocker 'ı etkinleştir** adımı, rastgele bir kurtarma parolası oluşturmak yerine belirtilen değeri kurtarma parolası olarak kullanır. Değerin geçerli bir sayısal BitLocker kurtarma parolası olması gerekir.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a>OSDBitLockerStartupKey

*[BitLocker 'ı etkinleştir](task-sequence-steps.md#BKMK_EnableBitLocker) adımını uygular.*

(giriş)

**Yalnızca USB üzerinde** anahtar yönetim seçeneği başlangıç anahtarı için rastgele bir başlangıç anahtarı oluşturmak yerine, **BitLocker 'ı etkinleştir** adımı başlangıç anahtarı olarak Güvenilir Platform Modülü (TPM) kullanır. Değerin geçerli, 256 bit Base64 kodlamalı BitLocker başlangıç anahtarı olması gerekir.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a>OSDCaptureAccount

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Yakalanan görüntüyü ağ paylaşımında ([Osdcapturedestination](#OSDCaptureDestination)) depolama izinlerine sahip bir Windows hesabı adı belirtir. [OSDCaptureAccountPassword](#OSDCaptureAccountPassword)öğesini de belirtin.

İşletim sistemi görüntüsü Yakala hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a>OSDCaptureAccountPassword

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Yakalanan görüntüyü bir ağ paylaşımında ([Osdcapturedestination](#OSDCaptureDestination)) depolamak Için kullanılan Windows hesabının ([osdcaptureaccount](#OSDCaptureAccount)) parolasını belirtir.

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a>OSDCaptureDestination

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Görev dizisinin yakalanan işletim sistemi görüntüsünü kaydettiği konumu belirtir. Dizin adının uzunluğu en fazla 255 karakter olabilir. Ağ paylaşımının kimlik doğrulaması gerekiyorsa, [Osdcaptureaccount](#OSDCaptureAccount) ve [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) değişkenlerini belirtin.

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a>OSDComputerName (giriş)

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Hedef bilgisayarın adını belirtir.

#### <a name="example"></a>Örnek

`%_SMSTSMachineName%`varsayılanını

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a>OSDComputerName (çıkış)

*[Windows ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureWindowsSettings) adımı için geçerlidir.*

Bilgisayarın NetBIOS adına ayarlanır. Değer, yalnızca [Osdmigratecomputername](#OSDMigrateComputerName) değişkeni olarak ayarlandıysa ayarlanır `true` .

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a>OSDConfigFileName

*[İşletim sistemi görüntüsünü Uygula](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) adımı için geçerlidir.*

(giriş)

İşletim sistemi dağıtımı görüntü paketiyle ilişkili işletim sistemi dağıtımı yanıt dosyasının dosya adını belirtir.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a>Osddataımageındex

*[Veri görüntüsünü Uygula](task-sequence-steps.md#BKMK_ApplyDataImage) adımı için geçerlidir.*

(giriş)

Hedef bilgisayara uygulanan görüntünün dizin değerini belirtir.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a>Osddiskındex

*[Biçim ve Bölüm diski](task-sequence-steps.md#BKMK_FormatandPartitionDisk) adımı için geçerlidir.*

(giriş)

Bölümlenecek fiziksel diskin numarasını belirtir.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a>OSDDNSDomain

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın kullandığı birincil DNS sunucusunu belirtir.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a>Osddnssontsearchorder

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayar için DNS arama sırasını belirtir.

### <a name="osddomainname"></a><a name="OSDDomainName"></a>OSDDomainName

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın katılacağı Active Directory etki alanının adını belirtir. Belirtilen değer, geçerli bir Active Directory Etki Alanı Hizmetleri etki alanı adı olmalıdır.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a>Osddomainons adı

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın katıldığı kuruluş biriminin (OU) RFC 1779 biçim adını belirtir. Belirtilmişse değerin tam yolu içermesi gerekir.

#### <a name="example"></a>Örnek

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a>OSDDoNotLogCommand

<!--1358493-->
*[Paketi Kur](task-sequence-steps.md#BKMK_InstallPackage) adımı için geçerlidir.*

*1902 sürümünden başlayarak*  
*[Komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımı için geçerlidir.*

(giriş)

Büyük olasılıkla hassas verilerin görüntülenmesini veya günlüğe kaydedilmesini engellemek için, bu değişkeni olarak ayarlayın `TRUE` . Bu değişken, bir **paket yüklemesi** sırasında **Smsts. log** dosyasındaki program adını maskeler.

Sürüm 1902 ' den başlayarak, bu değişkeni olarak ayarlarsanız `TRUE` , komut satırını günlük dosyasındaki **komut satırı Çalıştır** adımından da gizler.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a>OSDEnableTCPIPFiltering

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

TCP/IP filtrelemesinin etkinleştirilip etkinleştirilmeyeceğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`varsayılanını  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a>OSDGPTBootDisk

*[Biçim ve Bölüm diski](task-sequence-steps.md#BKMK_FormatandPartitionDisk) adımı için geçerlidir.*

(giriş)

GPT sabit diskinde bir EFı bölümü oluşturulup oluşturulmayacağını belirtir. EFı tabanlı bilgisayarlar bu bölümü başlangıç diski olarak kullanır.

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`varsayılanını

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a>OSDImageCreator

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Görüntüyü oluşturan kullanıcının isteğe bağlı adı. Bu ad, WIM dosyasında depolanır. Kullanıcı adının uzunluğu en fazla 255 karakter olabilir.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a>Osdımagedescription

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Yakalanan işletim sistemi görüntüsünün isteğe bağlı kullanıcı tanımlı bir açıklaması. Bu açıklama WIM dosyasında depolanır. Açıklama uzunluğu en fazla 255 karakter olabilir.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a>Osdımageındex

*[İşletim sistemi görüntüsünü Uygula](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Hedef bilgisayara uygulanan WıM dosyasının görüntü dizini değerini belirtir.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a>Osdımageversion

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

(giriş)

Yakalanan işletim sistemi görüntüsüne atanacak, Kullanıcı tanımlı isteğe bağlı bir sürüm numarası. Bu sürüm numarası WIM dosyasında depolanır. Bu değer, en fazla 32 uzunluğunda alfasayısal karakterlerden oluşan herhangi bir bileşim olabilir.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a>Osdınstalldriversadditionaloptions

<!--516679/2840016-->
*[Sürücü paketini Uygula](task-sequence-steps.md#BKMK_ApplyDriverPackage) adımı için geçerlidir.*

(giriş)

Bir sürücü paketi uygulanırken DıSM komut satırına eklemek için ek seçenekler belirtir. Görev sırası komut satırı seçeneklerini doğrulamaz.

Bu değişkeni kullanmak için, **sürücü paketini Uygula** adımında sürücü **paketini DISM 'yi recurse ile çalıştırarak Install seçeneğini**etkinleştirin.

Daha fazla bilgi için bkz. [Windows 10 DISM komut satırı seçenekleri](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a>OSDJoinAccount

*Aşağıdaki adımlar için geçerlidir:*  

- [Ağ Ayarlarını Uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Etki Alanına veya Çalışma Grubuna Katıl](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(giriş)

Hedef bilgisayarı etki alanına eklemek için kullanılan etki alanı kullanıcı hesabını belirtir. Bu değişken, bir etki alanına katılırken gereklidir.

Görev sırası etki alanına katılma hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a>OSDJoinDomainName

*[Katılma etki alanı veya çalışma grubu](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın katılacağı Active Directory etki alanının adını belirtir. Etki alanı adının uzunluğu 1 ile 255 karakter arasında olmalıdır.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a>Osdjoindomainons adı

*[Katılma etki alanı veya çalışma grubu](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın katıldığı kuruluş biriminin (OU) RFC 1779 biçim adını belirtir. Belirtilmişse değerin tam yolu içermesi gerekir. OU adının uzunluğu 0 ile 32.767 karakter arasında olmalıdır. [Osdjointype](#OSDJoinType) değişkeni `1` (çalışma grubuna katıl) olarak ayarlandıysa bu değer ayarlanır.

#### <a name="example"></a>Örnek

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a>OSDJoinPassword

*Aşağıdaki adımlar için geçerlidir:*  

- [Ağ Ayarlarını Uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Etki Alanına veya Çalışma Grubuna Katıl](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(giriş)

Hedef bilgisayarın Active Directory etki alanına katılması için kullandığı [Osdjoinaccount](#OSDJoinAccount) için parolayı belirtir. Görev dizisi ortamı bu değişkeni içermiyorsa Windows Kurulumu boş bir parola dener. [Osdjointype](#OSDJoinType) değişkeni, `0` (etki alanına katılarak) olarak ayarlandıysa bu değer gereklidir.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a>OSDJoinSkipReboot

*[Katılma etki alanı veya çalışma grubu](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) adımı için geçerlidir.*

(giriş)

Hedef bilgisayar etki alanına veya çalışma grubuna katıldıktan sonra yeniden başlatmanın atlanıp atlanmayacağını belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a>OSDJoinType

*[Katılma etki alanı veya çalışma grubu](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın Windows etki alanına mı çalışma grubuna mı katılacağını belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `0`: Hedef bilgisayarı bir Windows etki alanına katma  
- `1`: Hedef bilgisayarı bir çalışma grubuna ekleme  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a>OSDJoinWorkgroupName

*[Katılma etki alanı veya çalışma grubu](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın katıldığı çalışma alanının adını belirtir. Çalışma alanı adının uzunluğu 1 ile 32 karakter arasında olmalıdır.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a>OSDKeepActivation

*[Windows 'U yakalamaya hazırla](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) adımı için geçerlidir.*

(giriş)

Sysprep 'in ürün etkinleştirme bayrağını tutmayacağını veya sıfırlamayacağını belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`: etkinleştirme bayrağını tut
- `false`(varsayılan): etkinleştirme bayrağını sıfırlama

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a>OSDLocalAdminPassword değişkeninin

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

(giriş)

Yerel yönetici hesabının parolasını belirtir. **Yerel yönetici parolasını rastgele oluşturma ve tüm desteklenen platformlarda hesabı devre dışı bırakma**seçeneğini etkinleştirirseniz, adım bu değişkeni yoksayar. Belirtilen değerin uzunluğu 1 ile 255 karakter arasında olmalıdır.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a>OSDLogPowerShellParameters

<!--3556028-->
*1902 sürümünden başlayarak*  
*[PowerShell Betiği Çalıştır](task-sequence-steps.md#BKMK_RunPowerShellScript) adımı için geçerlidir.*

(giriş)

Potansiyel olarak gizli verilerin günlüğe kaydedilmesini engellemek için, **PowerShell Betiği Çalıştır** adımı **Smsts. log** dosyasında komut dosyası parametrelerini günlüğe kaydetmez. Komut dosyası parametrelerini görev sırası günlüğüne dahil etmek için, bu değişkeni **true**olarak ayarlayın.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a>OSDMigrateAdapterSettings

*[Ağ ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureNetworkSettings) adımı için geçerlidir.*

(giriş)

Görev dizisinin ağ bağdaştırıcısı bilgilerini yakalayıp yakalamayacağını belirtir. Bu bilgiler TCP/IP, DNS ve WINS için yapılandırma ayarlarını içerir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`varsayılanını
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a>OSDMigrateAdditionalCaptureOptions

*[Kullanıcı durumunu yakala](task-sequence-steps.md#BKMK_CaptureUserState) adımı için geçerlidir.*

(giriş)

Kullanıcı durumu taşıma aracı (USMT) için görev dizisinin Kullanıcı durumunu yakalamak için kullandığı ek komut satırı seçeneklerini belirtin. Adım, görev dizisi düzenleyicisinde bu ayarları kullanıma sunmaz. Bu seçenekleri, görev dizisinin ScanState için otomatik olarak oluşturulan USMT komut satırına ekleyinin bir dize olarak belirleyin.

Bu görev dizisi değişkeniyle belirtilen USMT seçenekleri, görev sırası çalıştırılmadan önce doğruluk için doğrulanmadı.

Kullanılabilir seçenekler hakkında daha fazla bilgi için bkz. [Scanstate sözdizimi](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a>OSDMigrateAdditionalRestoreOptions

*[Kullanıcı durumunu geri yükle](task-sequence-steps.md#BKMK_RestoreUserState) adımı için geçerlidir.*

(giriş)

Kullanıcı durumu taşıma aracı (USMT) için görev dizisinin Kullanıcı durumunu geri yüklerken kullandığı ek komut satırı seçeneklerini belirtir. Görev dizisinin, LoadState için otomatik olarak oluşturulan USMT komut satırına ekleyek seçenekleri bir dize olarak belirtin.

Bu görev dizisi değişkeniyle belirtilen USMT seçenekleri, görev sırası çalıştırılmadan önce doğruluk için doğrulanmadı.

Kullanılabilir seçenekler hakkında daha fazla bilgi için bkz. [LoadState sözdizimi](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a>OSDMigrateComputerName

*[Windows ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureWindowsSettings) adımı için geçerlidir.*

(giriş)

Bilgisayar adının geçirilip geçirilmeyeceğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`(varsayılan). [OSDComputerName (çıktı)](#OSDComputerName-output) değişkeni bilgisayarın NetBIOS adına ayarlanır.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a>Olarak ayarlanırsa OSDMigrateConfigFiles

*[Kullanıcı durumunu yakala](task-sequence-steps.md#BKMK_CaptureUserState) adımı için geçerlidir.*

(giriş)

Kullanıcı profillerinin yakalanmasını denetlemek için kullanılan yapılandırma dosyalarını belirtir. Bu değişken, yalnızca [OSDMigrateMode](#OSDMigrateMode) olarak ayarlandığında kullanılır `Advanced` . Bu virgülle ayrılmış liste değeri, özelleştirilmiş kullanıcı profili geçişi işlemini gerçekleştirmek için ayarlanır.

#### <a name="example"></a>Örnek

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a>Osdmigratedevam Onlockedfiles

*[Kullanıcı durumunu yakala](task-sequence-steps.md#BKMK_CaptureUserState) adımı için geçerlidir.*

(giriş)

USMT bazı dosyaları yakalayamaz, bu değişken Kullanıcı durumu yakalamanın devam etmesine izin verir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`varsayılanını  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a>Osdmigratedevam OnRestore

*[Kullanıcı durumunu geri yükle](task-sequence-steps.md#BKMK_RestoreUserState) adımı için geçerlidir.*

(giriş)

USMT bazı dosyaları geri yükleyemiyor olsa bile işleme devam edin.

#### <a name="valid-values"></a>Geçerli değerler

- `true`varsayılanını  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a>OSDMigrateEnableVerboseLogging

*Aşağıdaki adımlar için geçerlidir:*  

- [Kullanıcı Durumunu Yakala](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Kullanıcı Durumunu Yeniden Yükle](task-sequence-steps.md#BKMK_RestoreUserState)  

(giriş)

USMT için ayrıntılı günlük kaydını etkinleştir. Adım için bu değer gereklidir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`varsayılanını  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a>OSDMigrateLocalAccounts

*[Kullanıcı durumunu geri yükle](task-sequence-steps.md#BKMK_RestoreUserState) adımı için geçerlidir.*

(giriş)

Yerel bilgisayar hesabının geri yüklenip yüklenmeyeceğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`varsayılanını  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a>OSDMigrateLocalAccountPassword

*[Kullanıcı durumunu geri yükle](task-sequence-steps.md#BKMK_RestoreUserState) adımı için geçerlidir.*

(giriş)

[OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) değişkeni ise `true` , bu değişkenin *Tüm* geçirilmiş yerel hesaplara atanan parolayı içermesi gerekir. USMT, geçirilen tüm yerel hesaplara aynı parolayı atar. Bu parolayı geçici olarak değerlendirin ve daha sonra başka bir yöntemle değiştirin.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a>OSDMigrateMode ayarlandığında

*[Kullanıcı durumunu yakala](task-sequence-steps.md#BKMK_CaptureUserState) adımı için geçerlidir.*

(giriş)

USMT 'nin yakaladığı dosyaları özelleştirmenize olanak sağlar.

#### <a name="valid-values"></a>Geçerli değerler

- `Simple`: Görev sırası yalnızca standart USMT yapılandırma dosyalarını kullanır  

- `Advanced`: [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) görev dizisi DEĞIŞKENI, USMT 'nin kullandığı yapılandırma dosyalarını belirtir  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a>OSDMigrateNetworkMembership

*[Ağ ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureNetworkSettings) adımı için geçerlidir.*

(giriş)

Görev dizisinin çalışma grubu veya etki alanı üyeliği bilgilerini geçirip geçirmediğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`varsayılanını
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a>Osdmigrateregistrationınfo

*[Windows ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureWindowsSettings) adımı için geçerlidir.*

(giriş)

Adımın Kullanıcı ve kuruluş bilgilerini geçirip geçirmediğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`(varsayılan). [OSDRegisteredOrgName (output)](#OSDRegisteredOrgName-output) değişkeni, bilgisayarın kayıtlı kuruluş adına ayarlanır.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a>OSDMigrateSkipEncryptedFiles

*[Kullanıcı durumunu yakala](task-sequence-steps.md#BKMK_CaptureUserState) adımı için geçerlidir.*

(giriş)

Şifrelenmiş dosyaların yakalanıp yakalanmayacağını belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`varsayılanını  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a>OSDMigrateTimeZone

*[Windows ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureWindowsSettings) adımı için geçerlidir.*

(giriş)

Bilgisayarın saat diliminin geçirilip geçirilmeyeceğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`(varsayılan). [Osdtimezone (çıktı)](#OSDTimeZone-output) değişkeni bilgisayarın saat dilimine ayarlanır.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a>OSDNetworkJoinType

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın bir Active Directory etki alanına mı yoksa çalışma grubuna mı katılacağını belirtir.

#### <a name="value-values"></a>Değer değerleri

- `0`: Active Directory etki alanına ekleme  
- `1`: Bir çalışma grubuna katıl

### <a name="osdpartitions"></a><a name="OSDPartitions"></a>OSDPartitions

*[Biçim ve Bölüm diski](task-sequence-steps.md#BKMK_FormatandPartitionDisk) adımı için geçerlidir.*

(giriş)

Bu görev dizisi değişkeni, Bölüm ayarlarının dizi değişkenidir. Dizideki her öğe, sabit diskteki tek bir bölümün ayarlarını temsil eder. Dizi değişkeni adını sıfır tabanlı disk bölüm numarası ve özellik adı ile birleştirerek her bölüm için tanımlanan ayarlara erişin.

Bu adımın sabit diskte oluşturduğu *ilk* bölümün özelliklerini tanımlamak için aşağıdaki değişken adlarını kullanın:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Bölüm türünü belirtir. Bu özellik gereklidir. Geçerli değerler `Primary` ,, `Extended` `Logical` ve `Hidden` .

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Bölüm biçimlendirilirken kullanılacak dosya sistemi türünü belirtir. Bu özellik isteğe bağlıdır. Bir dosya sistemi belirtmezseniz, adım bölümü biçimlendirmez. Geçerli değerler `FAT32` ve ' dir `NTFS` .

#### <a name="osdpartitions0bootable"></a>Osdpartitions0bootable: bölümün

Bölümün önyüklenebilir olup olmadığını belirtir. Bu özellik gereklidir. Bu değer `TRUE` MBR diskleri için olarak ayarlandıysa, adım bu bölümü etkin olarak işaretler.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Kullanılan biçim türünü belirtir. Bu özellik gereklidir. Bu değer olarak ayarlanırsa `TRUE` , adım hızlı bir biçim gerçekleştirir. Aksi takdirde, adım tam bir biçim gerçekleştirir.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Biçimlendirildikleri sırada birime atanan adı belirtir. Bu özellik isteğe bağlıdır.

#### <a name="osdpartitions0size"></a>: Osdpartitions0size

Bölümün boyutunu belirtir. Bu özellik isteğe bağlıdır. Bu özellik belirtilmezse bölüm, kalan tüm boş alan kullanılarak oluşturulur. Birimler **OSDPartitions0SizeUnits** değişkeni ile belirtilir.

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

Adım **: OSDPartitions0Size** değişkenini yorumlamak için bu birimleri kullanır. Bu özellik isteğe bağlıdır. Geçerli değerler şunlardır `MB` (varsayılan), `GB` , ve `Percent` .

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Bu adım bölümler oluşturduğunda, her zaman Windows PE 'de bir sonraki kullanılabilir sürücü harfini kullanır. Başka bir görev dizisi değişkeninin adını belirtmek için bu isteğe bağlı özelliği kullanın. Bu adım, daha sonra başvurmak üzere yeni sürücü harfini kaydetmek için bu değişkeni kullanır.

Bu görev dizisi adımıyla birden çok bölüm tanımlarsanız, *ikinci* bölümün özellikleri değişken adında **1** dizin kullanılarak tanımlanır. Örneğin: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**ve **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a>OSDPartitionStyle

*[Biçim ve Bölüm diski](task-sequence-steps.md#BKMK_FormatandPartitionDisk) adımı için geçerlidir.*

(giriş)

Disk bölümlenirken kullanılacak bölümleme stilini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `GPT`: GUID bölümleme tablosu stilini kullanın
- `MBR`: Ana önyükleme kaydı bölümleme stilini kullanın

### <a name="osdproductkey"></a><a name="OSDProductKey"></a>OSDProductKey

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

(giriş)

Windows ürün anahtarını belirtir. Belirtilen değerin uzunluğu 1 ile 255 karakter arasında olmalıdır.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a>OSDRandomAdminPassword

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

(giriş)

Yeni işletim sistemindeki yerel yönetici hesabı için rastgele oluşturulmuş bir parolayı belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`(varsayılan): Windows Kurulumu hedef bilgisayardaki yerel yönetici hesabını devre dışı bırakır  

- `false`: Windows Kurulumu hedef bilgisayardaki yerel yönetici hesabını sağlar ve hesap parolasını [OSDLocalAdminPassword](#OSDLocalAdminPassword) değerine ayarlar.  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a>OSDRegisteredOrgName (giriş)

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni işletim sistemindeki varsayılan kayıtlı kuruluş adını belirtir. Belirtilen değerin uzunluğu 1 ile 255 karakter arasında olmalıdır.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a>OSDRegisteredOrgName (çıkış)

*[Windows ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureWindowsSettings) adımı için geçerlidir.*

Bilgisayarın kayıtlı kuruluş adına ayarlanır. Değer yalnızca [osdmigrateregistrationınfo](#OSDMigrateRegistrationInfo) değişkeni olarak ayarlandıysa ayarlanır `true` .

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a>OSDRegisteredUserName

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

(giriş)

Yeni işletim sistemindeki varsayılan kayıtlı Kullanıcı adını belirtir. Belirtilen değerin uzunluğu 1 ile 255 karakter arasında olmalıdır.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a>OSDServerLicenseConnectionLimit

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

(giriş)

İzin verilen en yüksek bağlantı sayısını belirtir. Belirtilen bağlantı sayısının 5 ile 9999 aralığında olması gerekir.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a>OSDServerLicenseMode

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

(giriş)

Kullanılan Windows Server lisans modunu belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a>OSDSetupAdditionalUpgradeOptions

*[Işletim sistemini yükseltme](task-sequence-steps.md#BKMK_UpgradeOS) adımı için geçerlidir.*

(giriş)

Windows 10 yükseltmesi sırasında Windows Kurulumu eklenen ek komut satırı seçeneklerini belirtir. Görev sırası komut satırı seçeneklerini doğrulamaz.

Daha fazla bilgi için bkz. [Windows Kurulumu Komut Satırı Seçenekleri](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a>OSDStateFallbackToNAA

*[Durum depolama iste](task-sequence-steps.md#BKMK_RequestStateStore) adımı için geçerlidir.*

(giriş)

Bilgisayar hesabı durum geçiş noktasına bağlanamadığında, bu değişken, görev dizisinin ağ erişim hesabı 'nı (NAA) kullanmaya geri dönüp gerçekleşmeyeceğini belirtir.

Ağ erişim hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Geçerli değerler

- `true`  
- `false`varsayılanını  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a>OSDStateSMPRetryCount

*[Durum depolama iste](task-sequence-steps.md#BKMK_RequestStateStore) adımı için geçerlidir.*

(giriş)

Görev dizisi adımının, durum geçiş noktası bulmayı kaç kere denedikten sonra başarısız olacağını belirtir. Belirtilen sayı 0 ile 600 arasında olmalıdır.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a>OSDStateSMPRetryTime

*[Durum depolama iste](task-sequence-steps.md#BKMK_RequestStateStore) adımı için geçerlidir.*

(giriş)

Görev dizisi adımının yeniden denemeler arasında bekleyeceği saniye sayısını belirtir. Saniye sayısı en çok 30 karakter olabilir.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a>OSDStateStorePath

*Aşağıdaki adımlar için geçerlidir:*  

- [Kullanıcı Durumunu Yakala](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Durum Depolama Alanını Serbest Bırak](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Durum Depolama Alanını İste](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Kullanıcı Durumunu Yeniden Yükle](task-sequence-steps.md#BKMK_RestoreUserState)  

(giriş)

Görev dizisinin Kullanıcı durumunu kaydettiği veya geri yüklediği klasörün ağ paylaşımının veya yerel yol adı. Varsayılan değer yoktur.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a>OSDTargetSystemDrive

*[İşletim sistemi görüntüsünü Uygula](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) adımı için geçerlidir.*

(çıkış)

Görüntü uygulandıktan sonra işletim sistemi dosyalarını içeren bölümün sürücü harfini belirtir.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a>OSDTargetSystemRoot (giriş)

*[İşletim sistemi görüntüsünü yakala](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) adımı için geçerlidir.*

Başvuru bilgisayarında yüklü işletim sisteminin Windows dizini yolunu belirtir. Görev sırası, Configuration Manager tarafından yakalama için desteklenen bir işletim sistemi olarak doğrular.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a>Osdtargetsistemkökü (çıkış)

*[Windows 'U yakalamaya hazırla](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) adımı için geçerlidir.*

Başvuru bilgisayarında yüklü işletim sisteminin Windows dizini yolunu belirtir. Görev sırası, Configuration Manager tarafından yakalama için desteklenen bir işletim sistemi olarak doğrular.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a>OSDTimeZone (giriş)

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni işletim sisteminde kullanılan varsayılan saat dilimi ayarını belirtir.

Bu değişkenin değerini saat diliminin dil sabit adı olarak ayarlayın. Örneğin, `Std` aşağıdaki kayıt defteri anahtarı altındaki bir saat dilimi değerindeki dizeyi kullanın: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones` .

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a>OSDTimeZone (çıkış)

*[Windows ayarlarını yakala](task-sequence-steps.md#BKMK_CaptureWindowsSettings) adımı için geçerlidir.*

Bilgisayarın saat dilimine ayarlanır. Değer, yalnızca [OSDMigrateTimeZone](#OSDMigrateTimeZone) değişkeni olarak ayarlandıysa ayarlanır `true` .

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a>Osdwindowssettingsınputlocale

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni işletim sisteminde kullanılan varsayılan giriş yerel ayar ayarını belirtir.

Windows kurulumu yanıt dosyası değeri hakkında daha fazla bilgi için bkz. [Microsoft-Windows-International-Core-InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a>OSDWindowsSettingsSystemLocale

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni IŞLETIM sisteminde kullanılan varsayılan sistem yerel ayar ayarını belirtir.

Windows kurulumu yanıt dosyası değeri hakkında daha fazla bilgi için bkz. [Microsoft-Windows-International-Core-SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a>OSDWindowsSettingsUILanguage

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni işletim sisteminde kullanılan varsayılan kullanıcı arabirimi dili ayarını belirtir.

Windows kurulumu yanıt dosyası değeri hakkında daha fazla bilgi için bkz. [Microsoft-Windows-International-Core-UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a>OSDWindowsSettingsUILanguageFallback

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni işletim sisteminde kullanılan geri dönüş Kullanıcı arabirimi dili ayarını belirtir.

Windows kurulumu yanıt dosyası değeri hakkında daha fazla bilgi için bkz. [Microsoft-Windows-International-Core-UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a>OSDWindowsSettingsUserLocale

*[Windows ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyWindowsSettings) adımı için geçerlidir.*

Yeni işletim sisteminde kullanılan varsayılan kullanıcı yerel ayar ayarını belirtir.

Windows kurulumu yanıt dosyası değeri hakkında daha fazla bilgi için bkz. [Microsoft-Windows-International-Core-UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a>OSDWipeDestinationPartition

*[Veri görüntüsünü Uygula](task-sequence-steps.md#BKMK_ApplyDataImage) adımı için geçerlidir.*

(giriş)

Hedef bölümde bulunan dosyaların silinip silinmeyeceğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `true`varsayılanını
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a>OSDWorkgroupName

*[Ağ ayarlarını uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarın katıldığı çalışma alanının adını belirtir.

Bu değişkeni ya da [OSDDomainName](#OSDDomainName) değişkenini belirtin. Çalışma grubu adı en çok 32 karakter içerebilir.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a>SetupCompletePause

*[Işletim sistemini yükseltme](task-sequence-steps.md#BKMK_UpgradeOS) adımı için geçerlidir.*

<!-- 4680263 -->

Sürüm 1910 ' den başlayarak, Windows kurulumu tamamlandığında yüksek performanslı cihazlarda pencere 10 yerinde yükseltme görev dizisiyle zamanlama sorunlarını gidermek için bu değişkeni kullanın. Bu değişkene saniye cinsinden bir değer atadığınızda, Windows kurulum işlemi, görev dizisini çalıştırmadan önce bu süreyi geciktirir. Bu zaman aşımı Configuration Manager istemcisinin başlatılması için ek zaman sağlar.

Aşağıdaki günlük girişleri, bu sorunun bu değişkenle düzeltilebileceğiyle ilgili yaygın örneklerdir:

- TSManager bileşeni, **Smsts. log**dosyasında aşağıdaki hatalara benzer girdileri kaydeder:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Windows kurulumu, **SetupComplete. log**dosyasında aşağıdaki hatalara benzer girdileri kaydeder:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a>Smsclientınstallproperties

*[Windows 'u ve ConfigMgr 'Yi Kur](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) adımı için geçerlidir.*

(giriş)

Configuration Manager istemcisini yüklerken görev dizisinin kullandığı istemci yükleme özelliklerini belirtir.

Daha fazla bilgi için bkz. [istemci yükleme parametreleri ve özellikleri hakkında](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a>SMSConnectNetworkFolderAccount

*[Ağ klasörüne Bağlan](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) adımı için geçerlidir.*

(giriş)

[Smsconnectnetworkfolderpath](#SMSConnectNetworkFolderPath)içindeki ağ paylaşımıyla bağlantı kurmak için kullanılan Kullanıcı hesabını belirtir. [Smsconnectnetworkfolderpassword](#SMSConnectNetworkFolderPassword) değeriyle hesap parolasını belirtin.

Görev dizisi ağ klasörü bağlantı hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a>Smsconnectnetworkfoldersürücüharfi

*[Ağ klasörüne Bağlan](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) adımı için geçerlidir.*

(giriş)

Bağlanılacak ağ sürücü harfini belirtir. Bu değer isteğe bağlıdır. Belirtilmemişse, ağ bağlantısı bir sürücü harfine eşlenmez. Bu değer belirtilmişse, değer D ile Z aralığında olmalıdır. X kullanmayın, Windows PE aşaması sırasında Windows PE tarafından kullanılan sürücü harftir.

#### <a name="examples"></a>Örnekler

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a>SMSConnectNetworkFolderPassword

*[Ağ klasörüne Bağlan](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) adımı için geçerlidir.*

(giriş)

[Smsconnectnetworkfolderpath](#SMSConnectNetworkFolderPath)içindeki ağ paylaşımıyla bağlantı kurmak Için kullanılan [Smsconnectnetworkfolderaccount](#SMSConnectNetworkFolderAccount) parolasını belirtir.

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a>SMSConnectNetworkFolderPath

*[Ağ klasörüne Bağlan](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) adımı için geçerlidir.*

(giriş)

Bağlantının ağ yolunu belirtir. Bu yolu bir sürücü harfine eşlemeniz gerekiyorsa, [Smsconnectnetworkfoldersürücüharfi](#SMSConnectNetworkFolderDriveLetter) değerini kullanın.

#### <a name="example"></a>Örnek

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a>Smsınstallupdatetarget

*[Yazılım güncelleştirmelerini yüklemek](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) adımını uygular.*

(giriş)

Tüm güncelleştirmelerin mi yoksa yalnızca zorunlu güncelleştirmelerin mi yükleneceğini belirtir.

#### <a name="valid-values"></a>Geçerli değerler

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a>SMSRebootMessage

*[Bilgisayarı yeniden Başlat](task-sequence-steps.md#BKMK_RestartComputer) adımı için geçerlidir.*

(giriş)

Hedef bilgisayarı yeniden başlatmadan önce kullanıcılara gösterilecek iletiyi belirtir. Bu değişken ayarlanmamışsa, varsayılan ileti metni görüntülenir. Belirtilen ileti 512 karakterden uzun olamaz.

#### <a name="example"></a>Örnek

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a>SMSRebootTimeout

*[Bilgisayarı yeniden Başlat](task-sequence-steps.md#BKMK_RestartComputer) adımı için geçerlidir.*

(giriş)

Bilgisayar yeniden başlatılmadan önce uyarının kullanıcıya kaç saniye boyunca gösterileceğini belirtir.

#### <a name="examples"></a>Örnekler

- `0`(varsayılan): yeniden başlatma iletisi gösterme  
- `60`: Bir dakika için uyarı görüntüleme  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a>SMSTSAssignmentsDownloadInterval

İlke olmayan son denemeden bu yana istemci, ilkeyi indirmeyi denemeden önce beklenecek saniye sayısı. Varsayılan olarak, istemci yeniden denemeden önce **0** saniye bekler.

Medyadan veya PXE'den bir başlatma öncesi komutu kullanarak bu değişkeni ayarlayabilirsiniz.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a>SMSTSAssignmentsDownloadRetry

İlk denemede ilke bulunamadığında istemcinin ilkeyi indirmeye kaç kez deneme sayısı. Varsayılan olarak, istemci **0** kez yeniden dener.

Medyadan veya PXE'den bir başlatma öncesi komutu kullanarak bu değişkeni ayarlayabilirsiniz.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a>SMSTSAssignUsersMode

Bir görev dizisinin kullanıcıları hedef bilgisayar ile nasıl ilişkilendirdiğini belirtir. Değişkeni aşağıda verilen değerlerden birine ayarlayın:  

- **Otomatik**: görev dizisi, işletim sistemini hedef bilgisayara dağıttığında, belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur.  

- **Bekliyor**: görev dizisi, belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur. Bir yöneticinin onu ayarlamaya yönelik ilişkiyi onaylaması gerekir.  

- **Devre dışı**: görev dizisi, işletim sistemini dağıtırken kullanıcıları hedef bilgisayarla ilişkilendirmez.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a>SMSTSDisableStatusRetry

<!--512358-->
Bağlantısı kesik senaryolarda, görev dizisi altyapısı, yönetim noktasına sürekli olarak durum iletileri göndermeyi dener. Bu senaryoda bu davranış, görev dizisi işlemede gecikmelere neden olur.

Bu değişkeni olarak ayarlayın `true` ve görev dizisi altyapısı, ilk ileti gönderilmediğinde durum iletilerini göndermeye çalışmaz. Bu ilk denemede birden çok yeniden deneme vardır.

Görev sırası yeniden başlatıldığında, bu değişkenin değeri devam ettirir. Ancak, görev sırası bir başlangıç durum iletisi göndermeye çalışır. Bu ilk denemede birden çok yeniden deneme vardır. Başarılı olursa, görev dizisi, bu değişkenin değerinden bağımsız olarak durum göndermeye devam eder. Durum gönderemezse, görev sırası bu değişkenin değerini kullanır.

> [!NOTE]  
> [Görev dizisi durum raporlaması](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) , her adımın ilerleme durumunu, geçmişini ve ayrıntılarını göstermek için bu durum iletilerini kullanır. Durum iletileri gönderemediği takdirde, bunlar kuyruğa alınmamış olur. Bağlantı, yönetim noktasına geri yüklendiğinde, daha sonra gönderilmeyecektir. Bu davranış, görev dizisi durum raporlama 'nın tamamlanmamış ve eksik öğeler olmasına neden olur.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a>SMSTSDisableWow64Redirection

*[Komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımı için geçerlidir.*

(giriş)

Varsayılan olarak, 64 bitlik bir IŞLETIM sisteminde görev sırası, WOW64 dosya sistemi yeniden yönlendiricisi kullanarak programı bulur ve komut satırından çalıştırır. Bu davranış, komutun işletim sistemi programlarının ve DLL 'lerin 32 bitlik sürümlerini bulmasına olanak tanır. Bu değişken `true` , WOW64 dosya sistemi yeniden yönlendiricisinin kullanımını devre dışı bırakmak için ayarlanıyor. Komutu, işletim sistemi programlarının ve DLL 'lerin yerel 64 bit sürümlerini bulur. Bu değişken, 32 bitlik bir IŞLETIM sisteminde çalışırken etkisizdir.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a>SMSTSDownloadAbortCode

Bu değişken, dış program yükleyici için iptal kodu değerini içerir. Bu program [SMSTSDownloadProgram](#SMSTSDownloadProgram) değişkeninde belirtilmiştir. Program, SMSTSDownloadAbortCode değişkeninin değerine eşit bir hata kodu döndürürse içerik indirme başarısız olur ve başka bir indirme yöntemi denenmez.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a>SMSTSDownloadProgram

Alternatif bir içerik sağlayıcısı (ACP) belirtmek için bu değişkeni kullanın. Bir ACP içerik indirmek için kullanılan bir yükleyici programıdır. Görev dizisi varsayılan Configuration Manager yükleyici yerine ACP 'yi kullanır. İçerik indirme işleminin bir parçası olarak, görev sırası bu değişkeni denetler. Belirtilmişse, görev dizisi içeriği indirmek için programı çalıştırır.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a>SMSTSDownloadRetryCount

Configuration Manager bir dağıtım noktasından içerik indirmeyi kaç kez denediğinde. Varsayılan olarak, istemci **2** kez yeniden dener.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a>SMSTSDownloadRetryDelay

Configuration Manager bir dağıtım noktasından içerik indirmeyi yeniden denemeden önce bekleyeceği saniye sayısı. Varsayılan olarak, istemci yeniden denemeden önce **15** saniye bekler.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a>SMSTSDriverRequestConnectTimeOut

*[Sürücüleri otomatik olarak Uygula](task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı için geçerlidir.*

Sürücü kataloğu istenirken, bu değişken, görev dizisinin HTTP sunucusu bağlantısı için bekleyeceği saniye sayısıdır. Bağlantı zaman aşımı ayarından daha uzun sürerse, görev sırası isteği iptal eder. Varsayılan olarak, zaman aşımı **60** saniyeye ayarlanır.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a>SMSTSDriverRequestReceiveTimeOut

*[Sürücüleri otomatik olarak Uygula](task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı için geçerlidir.*

Sürücü kataloğu istenirken, bu değişken, görev dizisinin yanıt beklediği saniye sayısıdır. Bağlantı zaman aşımı ayarından daha uzun sürerse, görev sırası isteği iptal eder. Varsayılan olarak, zaman aşımı **480** saniyeye ayarlanır.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a>SMSTSDriverRequestResolveTimeOut

*[Sürücüleri otomatik olarak Uygula](task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı için geçerlidir.*

Sürücü kataloğu istenirken, bu değişken, görev dizisinin HTTP ad çözümlemesi için beklediği saniye sayısıdır. Bağlantı zaman aşımı ayarından daha uzun sürerse, görev sırası isteği iptal eder. Varsayılan olarak, zaman aşımı **60** saniyeye ayarlanır.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a>SMSTSDriverRequestSendTimeOut

*[Sürücüleri otomatik olarak Uygula](task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı için geçerlidir.*

Sürücü kataloğu için bir istek gönderilirken, bu değişken, görev dizisinin isteği göndermek için bekleyeceği saniye sayısıdır. İstek zaman aşımı ayarından daha uzun sürerse, görev sırası isteği iptal eder. Varsayılan olarak, zaman aşımı **60** saniyeye ayarlanır.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a>SMSTSErrorDialogTimeout

Bir görev dizisinde bir hata oluştuğunda, hata içeren bir iletişim kutusu görüntüler. Görev sırası, bu değişken tarafından belirtilen saniye sayısından sonra otomatik olarak bir süre atar. Varsayılan olarak, bu değer **900** saniyedir (15 dakika).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a>SMSTSLanguageFolder

Önyükleme görüntüsünün dilden bağımsız görüntüleme dilini değiştirmek için bu değişkeni kullanın.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a>SMSTSLocalDataDrive

Görev dizisinin, çalışırken hedef bilgisayarda geçici önbellek dosyalarını nerede depoladığını belirtir.

Bu değişkeni, görev dizisi başlamadan önce, örneğin bir koleksiyon değişkenini ayarlayarak ayarlayın. Görev sırası başladıktan sonra, Configuration Manager SMSTSLocalDataDrive değişkeninin ne şekilde tanımlandığına göre [_SMSTSMDataPath](#SMSTSMDataPath) değişkenini tanımlar.

### <a name="smstsmp"></a><a name="SMSTSMP"></a>SMSTSMP

Configuration Manager yönetim noktasının URL 'sini veya IP adresini belirtmek için bu değişkeni kullanın.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a>SMSTSMPListRequestTimeoutEnabled

*Aşağıdaki adımlar için geçerlidir:*  

- [Uygulamayı Yükle](task-sequence-steps.md#BKMK_InstallApplication)  
- [Yazılım Güncelleştirmelerini Yükle](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(giriş)

İstemci intranette değilse, istemciyi yenilemek için tekrarlanan MPList isteklerini etkinleştirmek üzere bu değişkeni kullanın. Varsayılan olarak, bu değişken olarak ayarlanır `True` .

İstemciler Internet üzerinde olduğunda, `False` gereksiz gecikmelerden kaçınmak için bu değişkeni olarak ayarlayın.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a>SMSTSMPListRequestTimeout

*Aşağıdaki adımlar için geçerlidir:*  

- [Uygulamayı Yükle](task-sequence-steps.md#BKMK_InstallApplication)  
- [Yazılım Güncelleştirmelerini Yükle](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(giriş)

Görev sırası, konum hizmetlerinden yönetim noktası listesini (MPList) alamadığında, bu değişken adımı yeniden denemeden önce kaç milisaniye bekleyeceğini belirtir. Varsayılan olarak, görev sırası `60000` yeniden denemeden önce milisaniye (60 saniye) bekler. En fazla üç kez yeniden dener.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a>SMSTSPeerDownload

İstemcinin Windows PE Eş Önbelleği kullanmasını sağlamak için bu değişkeni kullanın. Bu işlevi sağlamak için bu değişkeni ayarlama `true` .

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a>SMSTSPeerRequestPort

Windows PE Eş Önbelleği 'nin ilk yayın için kullandığı özel bir ağ bağlantı noktası. İstemci ayarları 'nda yapılandırılmış varsayılan bağlantı noktası **8004**' dir.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a>SMSTSPersistContent seçeneğinin

Görev dizisi önbelleğindeki içeriği geçici olarak devam ettirmek için bu değişkeni kullanın. Bu değişken, görev dizisi tamamlandıktan sonra Configuration Manager istemci önbelleğinde içerik tutan [SMSTSPreserveContent](#SMSTSPreserveContent)'den farklıdır. SMSTSPersistContent seçeneğinin, görev sırası önbelleğini kullanır, SMSTSPreserveContent Configuration Manager istemci önbelleğini kullanır.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a>SMSTSPostAction

Görev dizisi tamamlandıktan sonra çalıştırılan bir komutu belirtir. Örneğin, `shutdown.exe /r /t 30 /f` görev dizisi tamamlandıktan sonra bilgisayarı 30 saniye yeniden başlatmak istediğinizi belirtin.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a>SMSTSPreferredAdvertID

Görev dizisini hedef bilgisayarda belirli bir hedeflenen dağıtımı çalıştırmaya zorlar. Medyadan veya PXE 'den bir başlatma öncesi komutu aracılığıyla bu değişkeni ayarlayın. Bu değişken ayarlanmışsa, görev dizisi gerekli tüm dağıtımları geçersiz kılar.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a>SMSTSPreserveContent

Bu değişken, görev dizisindeki içeriği dağıtımdan sonra Configuration Manager istemci önbelleğinde tutulacak şekilde işaretler. Bu değişken, yalnızca görev dizisi süresinin içeriğini tutan [SMSTSPersistContent seçeneğinin](#SMSTSPersistContent)öğesinden farklıdır. SMSTSPersistContent seçeneğinin, görev sırası önbelleğini kullanır, SMSTSPreserveContent Configuration Manager istemci önbelleğini kullanır. `true`Bu işlevi etkinleştirmek Için SMSTSPreserveContent olarak ayarlayın.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a>SMSTSRebootDelay

Bilgisayar yeniden başlatılmadan kaç saniye bekleneceğini belirtir. Bu değişken sıfır (0) ise, görev dizisi Yöneticisi, yeniden başlatmadan önce bir bildirim iletişim kutusu görüntülemez.

#### <a name="example"></a>Örnek

- `0`: bildirim gösterme  

- `60`: bir dakika için bildirim görüntüleme  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a>SMSTSRebootDelayNext

<!--4447680-->
Sürüm 1906 ' den başlayarak, bu değişkeni var olan [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) değişkeniyle birlikte kullanın. Daha sonraki yeniden başlatmaların, birinciden farklı bir zaman aşımı ile gerçekleşmesini istiyorsanız, SMSTSRebootDelayNext değerini saniye cinsinden farklı bir değere ayarlayın.

#### <a name="example"></a>Örnek

Kullanıcılara Windows 10 yerinde yükseltme görev dizisinin başlangıcında 60 dakikalık bir yeniden başlatma bildirimi vermek istiyorsunuz. Bu ilk uzun zaman aşımından sonra, yalnızca 60 saniye olması için ek zaman aşımları isteyeceksiniz. SMSTSRebootDelay to `3600` ve SMSTSRebootDelayNext to olarak ayarlayın `60` .  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a>SMSTSRebootMessage

Yeniden başlatma bildirimi iletişim kutusunda görüntülenecek iletiyi belirtir. Bu değişken ayarlanmamışsa, varsayılan bir ileti görüntülenir.

#### <a name="example"></a>Örnek

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a>SMSTSRebootRequested

Geçerli görev dizisi adımı tamamlandıktan sonra bir yeniden başlatma isteğinin olduğunu belirtir. Görev sırası adımı eylemi tamamlamaya yönelik yeniden başlatma gerektiriyorsa, bu değişkeni ayarlayın. Bilgisayar yeniden başlatıldıktan sonra görev dizisi sonraki görev dizisi adımından çalışmaya devam eder.

- `HD`: Yüklü işletim sistemi için yeniden başlatın
- `WinPE`: İlişkili önyükleme görüntüsüne yeniden başlatın

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a>SMSTSRetryRequested

Geçerli görev dizisi adımı tamamlandıktan sonra bir yeniden deneme isteğinde bulunur. Bu görev dizisi değişkeni ayarlandıysa, [SMSTSRebootRequested](#SMSTSRebootRequested) değişkenini olarak da ayarlayın `true` . Bilgisayar yeniden başlatıldıktan sonra, görev dizisi Yöneticisi aynı görev dizisi adımını yeniden çalıştırır.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a>SMSTSRunCommandLineAsUser

*2002 sürümünden başlayarak* <!-- 5573175 -->  
*[Komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımı için geçerlidir.*

**Komut satırını Çalıştır** adımı için kullanıcı bağlamını yapılandırmak üzere görev dizisi değişkenlerini kullanın. [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) ve [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) değişkenlerini kullanmak için bir yer tutucu hesabıyla **komut satırı Çalıştır** adımını yapılandırmanız gerekmez.

`SMSTSRunCommandLineAsUser`Aşağıdaki değerlerden biriyle yapılandırın:

- `true`: Başka **çalışan komut satırı** adımları içinde belirtilen kullanıcı bağlamında çalışır `SMSTSRunCommandLineUserName` .

- `false`: Başka **çalışan komut satırı** adımları, adımda yapılandırdığınız bağlamda çalışır.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a>SMSTSRunCommandLineUserName

*[Komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımı için geçerlidir.*

(giriş)

Komut satırını çalıştıran hesabı belirtir. Değeri, kullanıcı adı veya etki alanı\kullanıcı adı biçiminde bir dizedir. [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) değişkeniyle hesap parolasını belirtin.

> [!NOTE]
> Sürüm 2002 ' den başlayarak, bu adım için kullanıcı bağlamını yapılandırmak üzere Bu değişkenle birlikte [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) değişkenini kullanın.
>
> Sürüm 1910 ve önceki sürümlerde, **komut satırını Çalıştır** adımını **Bu adımı şu hesap olarak çalıştırma**ayarıyla yapılandırın. Bu seçeneği etkinleştirdiğinizde, Kullanıcı adını ve parolayı değişkenlerle birlikte ayarlarsanız, hesap için herhangi bir değer belirtin.

Görev sırası farklı çalıştır hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a>SMSTSRunCommandLineUserPassword

*[Komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımı için geçerlidir.*

(giriş)

[SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) değişkeni tarafından belirtilen hesabın parolasını belirtir.

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a>SMSTSRunPowerShellAsUser

*2002 sürümünden başlayarak* <!-- 5573175 -->  
*[PowerShell Betiği Çalıştır](task-sequence-steps.md#BKMK_RunPowerShellScript) adımı için geçerlidir.*

**PowerShell Betiği Çalıştır** adımının kullanıcı bağlamını yapılandırmak için görev dizisi değişkenlerini kullanın. [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) ve [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) değişkenlerini kullanmak için **PowerShell Betiği Çalıştır** adımını bir yer tutucu hesapla yapılandırmanız gerekmez.

`SMSTSRunPowerShellAsUser`Aşağıdaki değerlerden biriyle yapılandırın:

- `true`: Diğer tüm **çalışan PowerShell betiği** adımları içinde belirtilen kullanıcı bağlamında çalışır `SMSTSRunPowerShellUserName` .

- `false`: Diğer tüm **çalışan PowerShell betiği** adımları, adımda yapılandırdığınız bağlamda çalışır.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a>SMSTSRunPowerShellUserName

*[PowerShell Betiği Çalıştır](task-sequence-steps.md#BKMK_RunPowerShellScript) adımı için geçerlidir.*

(giriş)

PowerShell betiğinin çalıştırıldığı hesabı belirtir. Değeri, kullanıcı adı veya etki alanı\kullanıcı adı biçiminde bir dizedir. [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) değişkeniyle hesap parolasını belirtin.

> [!NOTE]
> Bu değişkenleri kullanmak için **PowerShell Betiği Çalıştır** adımını, **Bu adımı aşağıdaki hesap olarak çalıştırma**ayarıyla yapılandırın. Bu seçeneği etkinleştirdiğinizde, Kullanıcı adını ve parolayı değişkenlerle birlikte ayarlarsanız, hesap için herhangi bir değer belirtin.

Görev sırası farklı çalıştır hesabı hakkında daha fazla bilgi için bkz. [hesaplar](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a>SMSTSRunPowerShellUserPassword

*[PowerShell Betiği Çalıştır](task-sequence-steps.md#BKMK_RunPowerShellScript) adımı için geçerlidir.*

(giriş)

[SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) değişkeni tarafından belirtilen hesabın parolasını belirtir.

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a>SMSTSSoftwareUpdateScanTimeout

*[Yazılım güncelleştirmelerini yüklemek](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) adımını uygular.*

(giriş)

Bu adım sırasında yazılım güncelleştirmeleri taraması için zaman aşımını denetleyin. Örneğin, tarama sırasında çok sayıda güncelleştirme bekleliyorsanız, değeri arttırın. Varsayılan değer `3600` saniyedir (60 dakika). Değişken değeri saniye cinsinden ayarlanır.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a>SMSTSUDAUsers

Hedef bilgisayarın birincil kullanıcılarını şu biçimi kullanarak belirtir: `<DomainName>\<UserName>` . Birden çok kullanıcıyı virgülle () ayırarak ayırın `,` . Daha fazla bilgi için bkz. [kullanıcıları bir hedef bilgisayarla ilişkilendirme](../get-started/associate-users-with-a-destination-computer.md).

#### <a name="example"></a>Örnek

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a>SMSTSWaitForSecondReboot

*[Yazılım güncelleştirmelerini yüklemek](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) adımını uygular.*

(giriş)

Bu isteğe bağlı görev dizisi değişkeni, bir yazılım güncelleştirmesi yüklemesi iki kez yeniden başlatma gerektirdiğinde istemci davranışını denetler. Yazılım güncelleştirme yüklemesinden ikinci bir yeniden başlatma nedeniyle bir görev dizisinin başarısız olmasını engellemek için bu adımdan önce bu değişkeni ayarlayın.

Bilgisayar yeniden başlatılırken bu adımda görev dizisinin ne kadar süre duraklayacağını belirtmek için SMSTSWaitForSecondReboot değerini saniye cinsinden ayarlayın. İkinci bir yeniden başlatma durumunda yeterli zamana izin verin.

Örneğin, SMSTSWaitForSecondReboot olarak ayarlarsanız `600` , görev sırası ek adımlar çalıştırılmadan önce yeniden başlatmanın ardından 10 dakika boyunca duraklatılır. Bu değişken, tek bir yazılım güncelleştirmelerini yükleme görev dizisi adımı yüzlerce yazılım güncelleştirmesini yüklediğinde yararlı olur.

> [!Note]
> Bu değişken yalnızca işletim sistemi dağıtan bir görev dizisi için geçerlidir. Özel bir görev dizisinde çalışmaz. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a>TSDebugMode

<!--3612274-->
Sürüm 1906 ' den başlayarak, bu değişkeni `TRUE` görev dizisinin dağıtıldığı bir koleksiyon veya bilgisayar nesnesi üzerinde olarak ayarlayın. Bu değişken kümesine sahip herhangi bir cihaz, kendisine dağıtılan herhangi bir görev dizisini hata ayıklama moduna koyar.

Daha fazla bilgi için bkz. [görev dizisinde hata ayıklama](../deploy-use/debug-task-sequence.md).

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a>Tsdebughata

<!-- 5012536 -->
Sürüm 1910 ' den başlayarak, `TRUE` görev dizisi hata döndürdüğünde [görev sırası hata ayıklayıcısını](../deploy-use/debug-task-sequence.md) otomatik olarak başlatmak için bu değişkeni olarak ayarlayın.

Bu değişkeni kullanarak ayarla:

- [Görev sırası değişkenini ayarla](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımı

- Bir koleksiyon değişkeni. Daha fazla bilgi için bkz. [değişkenleri ayarlama](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a>TSDisableProgressUI

<!-- 1354291 -->
Görev sırasının son kullanıcılara ilerlemeyi ne zaman görüntüleyeceğini denetlemek için bu değişkeni kullanın. İlerlemeyi farklı zamanlarda gizlemek veya göstermek için, bu değişkeni bir görev dizisinde birden çok kez ayarlayın.  

- `true`: Görev dizisi ilerlemesini gizle  

- `false`: Görev sırası ilerleme durumunu görüntüle  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a>TSErrorOnWarning

*[Uygulama yüklemesi](task-sequence-steps.md#BKMK_InstallApplication) adımı için geçerlidir.*

(giriş)

Bu adım sırasında görev sırası altyapısının algılanan bir uyarıyı hata olarak kabul etmediğini belirtin. Görev sırası bir [_TSAppInstallStatus](#TSAppInstallStatus) `Warning` veya daha fazla uygulama ya da gerekli bağımlılık, bir gereksinimi karşılayamadığı için yüklenemediği zaman _TSAppInstallStatus değişkenini ayarlar. Bu değişkeni olarak ayarlarsanız `True` ve görev dizisi **_TSAppInstallStatus** olarak ayarlandığında `Warning` , sonuç bir hatadır. Değeri `False` varsayılan davranıştır.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a>TSProgressInfoLevel

*2002 sürümünden başlayarak*<!--5932692-->  

Görev sırası ilerleme penceresinin görüntülediği bilgi türünü denetlemek için bu değişkeni belirtin. Bu değişken için aşağıdaki değerleri kullanın:

- `1`: İlerleme metnine geçerli adımı ve toplam adımları ekleyin. Örneğin, **2/10**.
- `2`: Geçerli adımı, toplam adımları ve tamamlanan yüzdeyi dahil edin. Örneğin, **2/10 (tamamlanan %20)**.
- `3`: Tamamlanan yüzdeyi dahil et. Örneğin, **(%20 Tamam)**.

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a>Tsuefıdrive

**Değişken** ALANıNDAKI bir FAT32 bölümünün özelliklerinde kullanın. Görev dizisi bu değişkeni algıladığında, bilgisayarı yeniden başlatılmadan önce diski UEFı 'ye geçişe hazırlar. Daha fazla bilgi için bkz. [BIOS 'TAN UEFI dönüştürmeyi yönetmeye yönelik görev dizisi adımları](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a>WorkingDirectory

*[Komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımı için geçerlidir.*

(giriş)

Bir komut satırı eyleminin başlangıç dizinini belirtir. Belirtilen dizin adı 255 karakterden uzun olamaz.

#### <a name="examples"></a>Örnekler

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Kullanım dışı değişkenler

Aşağıdaki değişkenler kullanım dışıdır:

- **Osdallowunsigneddriver**: Windows Vista ve sonraki işletim sistemleri dağıtıldığında kullanılmıyor
- **Osdbuildstoragedriverlist**: yalnızca Windows XP ve windows Server 2003 için geçerlidir
- **Osddiskpartbıoscompatibilitymode**: yalnızca Windows XP veya windows Server 2003 dağıtımında gereklidir
- **Osdınstaltaditionındex**: gerekli değildir-Windows Vista sonrası
- **OSDPreserveDriveLetter**: daha fazla bilgi için bkz. [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Bu görev dizisi değişkeni kullanım dışıdır.
>
> Bir işletim sistemi dağıtımı sırasında, varsayılan olarak Windows Kurulumu kullanılacak en iyi sürücü harfini belirler (genellikle C:).

*Önceki davranış*: bir görüntü uygulanırken, Osdprevervesürücüharfi değişkeni, görev dizisinin görüntü dosyasında (WIM) yakalanan sürücü harfini kullanıp kullanmadığını belirler. Bu değişkenin değerini, `false` **Işletim sistemini Uygula** görev dizisi adımında **hedef** ayarı için belirttiğiniz konumu kullanacak şekilde ayarlayın. Daha fazla bilgi için bkz. [OS görüntüsünü uygulama](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Ayrıca bkz.

- [Görev dizisi adımları](task-sequence-steps.md)
- [Görev sırası değişkenlerini kullanma](using-task-sequence-variables.md)
- [Otomatikleştirme görevlerini planlama konuları](../plan-design/planning-considerations-for-automating-tasks.md)
