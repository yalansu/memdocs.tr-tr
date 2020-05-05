---
title: İstemci olay günlükleri
titleSuffix: Configuration Manager
description: Windows olay günlüğündeki olası BitLocker (MBAZ) istemci girişleri için teknik başvuru
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722063"
---
# <a name="client-event-logs"></a>İstemci olay günlükleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

BitLocker yönetim ilkesi dağıttığınız Configuration Manager istemcisinde, BitLocker istemci olay günlüklerini görüntülemek için Windows Olay Görüntüleyicisi kullanın. Hem [yönetici](#admin) hem de [işletimsel](#operational) olay günlükleri Için **uygulama ve hizmet günlükleri**, **Microsoft**, **Windows**, **mbad** 'ye gidin.

## <a name="admin"></a>Yönetici

### <a name="2-volumeenactmentfailed"></a>2: Birimenactmentfailed

MBAD İlkeleri uygulanırken bir hata oluştu.

#### <a name="error-code--2144272219"></a>Hata kodu:-2144272219

Ayrıntılar: BitLocker Sürücü Şifrelemesi yalnızca ölçülü kaynak sağlanan depolama üzerinde yalnızca kullanılan alan şifrelemesini destekler.

Bu hata, Windows 10 sürüm 1803 veya önceki bir sürümünü çalıştıran bir sanal makineyi şifrelemek için BitLocker 'ı kullanmayı denerseniz oluşur. Windows 10 ' un önceki sürümleri tam disk şifrelemesini desteklemez. BitLocker yönetim ilkeleri tam disk şifrelemesi uygular.

#### <a name="error-code--2147024774"></a>Hata kodu:-2147024774

Ayrıntılar: bir sistem çağrısına geçirilen veri alanı çok küçük.

Bu sorunu çözmek için bilgisayarı yeniden başlatın.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Şifreleme durumu verileri gönderilirken bir hata oluştu.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Sistem birimi eksik. İşletim sistemi sürücüsünü şifrelemek için SystemVolume gereklidir.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

TPM donanımı eksik. TPM koruyucusu ile işletim sistemi sürücüsünü şifrelemek için TPM gerekir.

### <a name="10-machinehwexempted"></a>10: Machinehwmuaf tutulan

Bilgisayar, şifrelemeden muaf tutulur. Makinenin donanım durumu: muaf tutulan

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

Bilgisayar, şifrelemeden muaf tutulur. Makinenin donanım durumu: bilinmiyor

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Donanım muafiyet denetimi başarısız oldu.

### <a name="13-userisexempted"></a>13: Userısexempted

Kullanıcı şifrelemeden muaf tutulur.

### <a name="14-useriswaiting"></a>14: Userısbeklediği

Kullanıcı bir istisna istedi.

### <a name="15-userexemptioncheckfailed"></a>15: Usermuaf Tioncheckfailed

Kullanıcı muafiyet denetimi başarısız oldu.

### <a name="16-userpostponed"></a>16: Kullanıcı ertelendi

Kullanıcı, şifreleme işlemini erteledir.

### <a name="17-tpminitializationfailed"></a>17: Tpminitializationbaşarısız

TPM başlatması başarısız oldu. Kullanıcı BIOS değişikliklerini reddetti.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

MBAE kurtarma ve donanım hizmetine bağlanılamıyor.

#### <a name="error-code--2147024809"></a>Hata kodu:-2147024809

Ayrıntılar: parametre yanlış.

Bu hata, Web sitesi HTTPS değilse veya istemcinin bir PKI sertifikası yoksa oluşur.

### <a name="20-policymismatch"></a>20: Policyuyuşmazlık

BitLocker yönetim ilkesi çakışıyor veya bozuk.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Algılanan işletim sistemi birim şifreleme ilkeleri çakışması. İşletim sistemi sürücü koruyucuları ile ilgili BitLocker ilkelerini denetleyin.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Algılanan sabit veri sürücüsü birim şifreleme ilkeleri çakışması. Sabit veri sürücüsü sürücü koruyucuları ile ilgili BitLocker ilkelerini denetleyin.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Şifreleme sırasında bir hata oluştu. Ön Windows 8.1 makineler için FIPS modunda bir veri kurtarma aracısı (DRA) koruyucusu gerekir.

### <a name="34-tpmlockoutresetfailed"></a>34: Tpmlockoutresetbaşarısız oldu

TPM kilitleme sıfırlanamadı.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

MBAD hizmetlerinden TPM OwnerAuth alınamadı.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

WMI sağlayıcısı için DLL arama yolu güncelleştirilemedi.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Aracı durduruluyor. MBAMWMI sağlayıcı örneği beklenirken zaman aşımına uğradı.

## <a name="operational"></a>İşlemdeki

### <a name="1-volumeenactmentsuccessful"></a>1: Birimenactmentbaşarılı

BitLocker yönetim ilkeleri başarıyla uygulandı.

### <a name="3-transferstatusdatasuccessful"></a>3: Transferstatusdatabaşarılı

Şifreleme durumu verileri başarıyla gönderildi.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

MBAE kurtarma ve donanım hizmetine başarıyla bağlanıldı.

### <a name="28-tpmownerauthescrowed"></a>28: Tpmownerauthescroçar

TPM OwnerAuth, escroçar.

### <a name="29-recoverykeyescrowed"></a>29: Recoverykeyescroçar

Birim için BitLocker kurtarma anahtarı, escroçar.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

Birimin BitLocker kurtarma anahtarı güncelleştirildi.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

İlke zorla tarihi... , birim için ayarlandı

### <a name="32-enforcepolicydatecleared"></a>32: Enforcepolicydatetemizlendi

İlke zorla tarihi... birim için temizlendi.

### <a name="33-tpmlockoutresetsucceeded"></a>33: Tpmlockoutresetbaşarılı

TPM kilitleme başarıyla sıfırlandı.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

MBAD hizmetlerinden TPM OwnerAuth başarıyla alındı.

### <a name="39-removabledrivemounted"></a>39: Removabledrivetakılmış

Çıkarılabilir sürücü takıldı.

### <a name="40-removabledrivedismounted"></a>40: Removabledriveçıkarıldı

Çıkarılabilir sürücü çıkarıldı.

### <a name="41-failedtoenactendpointunreachable"></a>41: Failedtoenactendpointunerişilebilen

MBAE kurtarma ve donanım hizmetine bağlanamama hatası, BitLocker yönetim ilkelerinin birime başarıyla uygulanmasını engelledi.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Kilitli birim durumu BitLocker yönetim ilkelerinin birime başarıyla uygulanmasını engelledi.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: Transferstatusdatafailedendpointunerişilebilen

MBAD uyumluluğu ve durum hizmetine bağlanamama hatası, şifreleme durum verilerinin aktarımını engelledi.

## <a name="see-also"></a>Ayrıca bkz.

Bu günlükleri kullanma hakkında daha fazla bilgi için bkz. [BitLocker olay günlükleri](about-event-logs.md).

Daha fazla sorun giderme bilgisi için bkz. [BitLocker sorunlarını giderme](troubleshoot.md).
