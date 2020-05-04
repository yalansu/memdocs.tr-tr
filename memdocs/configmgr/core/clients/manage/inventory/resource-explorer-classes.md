---
title: Kaynak Gezgini varsayılan envanter sınıfları
titleSuffix: Configuration Manager
description: Kaynak Gezgini görünen sınıfları gösterir
ms.date: 11/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d333f4c-0f85-4278-b421-064cf01529a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81cf8e1779e072d3eee6a5ed7080b6a63fd07451
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710737"
---
# <a name="resource-explorer-default-inventory-classes"></a>Kaynak Gezgini varsayılan envanter sınıfları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Kaynak Gezgini varsayılan envanter sınıfları açıklanmaktadır.

Varsayılan envanter sınıfları şunlardır:

## <a name="1394-controller"></a>1394 denetleyicisi

Ad alanı: root\cimv2

sınıf Win32_1394Controller


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int32 Maxnumberkontrollü

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="account-sid"></a>Hesap SID 'SI

Ad alanı: root\cimv2

sınıf Win32_AccountSID

- Dizisinde Dosyalarında

- Dizisinde Ayarlanmasını



## <a name="activesync-service"></a>ActiveSync hizmeti

Ad alanı: root\SmsDm

sınıf SMS_ActiveSyncService


- Int32 MajorVersion

- Int32 MinorVersion

- Dizisinde LastSyncTime



## <a name="amt-agent"></a>AMT Aracısı

Ad alanı: Root\Cimv2\Sms

sınıf SMS_AMTObject


- Int32 DeviceID

- Dizisinde TUT

- Dizisinde AMTApps

- Dizisinde BIO sürümü

- Dizisinde BuildNumber

- Dizisinde In

- Dizisinde LegacyMode

- Dizisinde Netstack

- Int32 ProvisionMode

- Int32 ProvisionState

- Dizisinde RecoveryBuildNum

- Dizisinde RecoveryVersion

- Dizisinde İsteyin

- Int32 TLSMode

- Dizisinde Konağında VendorID

- Int32 ZTCEnabled



## <a name="appv-client-application"></a>AppV Istemci uygulaması

Ad alanı: root\AppV

sınıf AppvClientApplication


- Dizisinde Uygulama

- Dizisinde PackageID

- Dizisinde Packageversionıd

- Boolean EnabledForUser

- Boolean Enabledglobal

- Dizisinde Ada

- Dizisinde TargetPath

- Dizisinde Sürüm



## <a name="appv-client-package"></a>AppV Istemci paketi

Ad alanı: root\AppV

AppvClientPackage sınıfı


- Dizisinde PackageID

- Dizisinde VersionId

- Dizisinde [] Varlıkları

- Dizisinde DeploymentMachineData

- Dizisinde DeploymentUserData

- Boolean Hasassetıntelligence

- Boolean Vip

- Boolean Ispublishedglobal

- Boolean Ipublishedtouser

- Dizisinde Ada

- Int64 PackageSize

- Dizisinde Yolun

- Int16 PercentLoaded

- Dizisinde UserConfigurationData

- Dizisinde Sürüm



## <a name="autostart-software"></a>AutoStart yazılımı

Ad alanı: Root\Cimv2\Sms

sınıf SMS_AutoStartSoftware


- Dizisinde Dosya özellikleri karması

- Dizisinde BinFileVersion

- Dizisinde BinProductVersion

- Dizisinde Açıklaması

- Dizisinde Kısaltın

- Dizisinde FilePropertiesHashEx

- Dizisinde FileVersion

- Dizisinde Konumuna

- Dizisinde Ürünüyle

- Dizisinde ProductVersion

- Dizisinde 'In

- Dizisinde StartupType

- Dizisinde StartupValue



## <a name="baseboard"></a>Kart

Ad alanı: root\cimv2

sınıf Win32_BaseBoard


- Dizisinde Etiket

- Dizisinde Başlığını

- Dizisinde ConfigOptions []

- Dizisinde Açıklaması

- Boolean HostingBoard

- Boolean Hotswap

- Hem InstallDate

- Dizisinde Üreticisini

- Dizisinde Modelinizi

- Dizisinde Ada

- Dizisinde OtherIdentifyingInfo

- Dizisinde PartNumber

- Boolean PoweredOn

- Dizisinde Ürünüyle

- Boolean Çıkarılabilir

- Boolean Değiştirebilen

- Dizisinde Gereksinimsaçıklama

- Boolean RequiresDaughterBoard

- Dizisinde Number

- Dizisinde ISTEYIN

- Dizisinde SlotLayout

- Boolean SpecialRequirements

- Dizisinde Durumlarına

- Dizisinde Sürüm



## <a name="battery"></a>Pil

Ad alanı: root\cimv2

sınıf Win32_Battery


- Dizisinde DeviceID

- Int16 Sonrası

- Int16 Batteryıstatus

- Dizisinde Başlığını

- Int16 Kimya

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int32 Tasarım kapasitesi

- Int64 Tasarım gerilimi

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int16 EstimatedChargeRemaining

- Int32 EstimatedRunTime

- Int32 ExpectedLife

- Int32 FullChargeCapacity

- Hem InstallDate

- Int32 LastErrorCode

- Int32 MaxRechargeTime

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Smartbatteryıversion

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Int32 Timeonpili

- Int32 Timetofullücret



## <a name="bitlocker"></a>BitLocker

Ad alanı: root\cimv2\security\MicrosoftVolumeEncryption

sınıf Win32_EncryptableVolume


- Dizisinde DeviceID

- Dizisinde Letter

- Dizisinde Persistentvolumeıd

- Int32 ProtectionStatus



## <a name="bitlocker-encryption-details"></a>BitLocker şifreleme ayrıntıları

Ad alanı: root\cimv2

sınıf Win32_BitLockerEncryptionDetails


- Dizisinde Bitlockerpersistentvolumeıd

- (SInt32) Uyumluluk

- (SInt32) Dönüştürme durumu

- Dizisinde DeviceID

- Dizisinde Letter

- (SInt32) EncryptionMethod

- Dizisinde EnforcePolicyDate

- Boolean Isoto Unlockenabled

- (SInt32) Anahtar korunabilir []

- Dizisinde Mbampersistentvolumeıd

- (SInt32) MbamVolumeType

- Dizisinde Karmaşık olmayan bir algılayıcısı

- (SInt32) ProtectionStatus

- (SInt32) Reasonsforuyumsuzluk []



## <a name="bitlocker-policy"></a>BitLocker Ilkesi

Ad alanı: root\cimv2

sınıf Win32Reg_MBAMPolicy


- Dizisinde EncodedComputerName

- Int32 EncryptionMethod

- Int32 Fixeddatadriveoto kilidi açma

- Int32 Fixeddatadriveşifrelemesi

- Int32 Fixeddatadriveparolası

- Dizisinde Işareti

- Dizisinde LastConsoleUser

- Int32 MBAMMachineError

- Int32 MBAMPolicyEnforced

- Int32 Osdriveşifrelemesi

- Int32 Osdrivekoruyucusu

- Hem Usermuaf Tiondate



## <a name="boot-configuration"></a>Önyükleme yapılandırması

Ad alanı: root\cimv2

sınıf Win32_BootConfiguration


- Dizisinde Ada

- Dizisinde BootDirectory

- Dizisinde Yapılandırmayolu

- Dizisinde Açıklaması

- Dizisinde LastDrive

- Dizisinde ScratchDirectory

- Dizisinde SettingID

- Dizisinde TempDirectory



## <a name="browser-helper-object"></a>Tarayıcı Yardımcısı nesnesi

Ad alanı: Root\Cimv2\Sms

sınıf SMS_BrowserHelperObject


- Dizisinde Dosya özellikleri karması

- Dizisinde BinFileVersion

- Dizisinde BinProductVersion

- Dizisinde IN

- Dizisinde Açıklaması

- Dizisinde Kısaltın

- Dizisinde FilePropertiesHashEx

- Dizisinde FileVersion

- Dizisinde Ürünüyle

- Dizisinde ProductVersion

- Dizisinde 'In

- Dizisinde Sürüm



## <a name="ccm_rax"></a>CCM_RAX

Ad alanı: root\ccm\cımodeller

sınıf CCM_RAXInfo


- Dizisinde AppID

- Dizisinde Hostingconfiguration

- Dizisinde Kullanıcı SID 'si



## <a name="cd-rom"></a>CD-ROM

Ad alanı: root\cimv2

sınıf Win32_CDROMDrive


- Dizisinde DeviceID

- Int16 Sonrası

- Int16 Yetenekler []

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Dizisinde CompressionMethod

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Int64 DefaultBlockSize

- Dizisinde Açıklaması

- Dizisinde Sürücü

- Boolean Sürücü bütünlüğü

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde Errormetodolojisi

- Int16 FileSystemFlags

- Int32 FileSystemFlagsEx

- Dizisinde NUMARASıNı

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int64 MaxBlockSize

- Int32 MaximumComponentLength

- Int64 MaxMediaSize

- Boolean Ortam

- Dizisinde Type

- Int64 MinBlockSize

- Dizisinde Ada

- Boolean Gereksiz korlama

- Int32 Desteklenmeyen numberofmedias

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde RevisionLevel

- Int32 SCSIBus

- Int16 SCSILogicalUnit

- Int16 SCSIPort

- Int16 Scsitargetıd

- Int64 Boyutla

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Dizisinde VolumeName

- Dizisinde Birimserialnumber



## <a name="client-events"></a>İstemci olayları

Ad alanı: root\ccm\ınvagt

sınıf ClientEvents


- Dizisinde EventName

- Int16 Biriktirme



## <a name="computer-system"></a>Bilgisayar Sistemi

Ad alanı: root\cimv2

sınıf Win32_ComputerSystem


- Dizisinde Ada

- Int16 AdminPasswordStatus

- Boolean AutomaticResetBootOption

- Boolean AutomaticResetCapability

- Int16 BootOptionOnLimit

- Int16 Bootoptiononizleme

- Boolean BootROMSupported

- Dizisinde BootupState

- Dizisinde Başlığını

- Int16 ChassisBootupState

- (SInt16) CurrentTimeZone

- Boolean DaylightInEffect

- Dizisinde Açıklaması

- Dizisinde Alanını

- Int16 DomainRole

- Int16 FrontPanelResetStatus

- Boolean InfraredSupported

- Dizisinde InitialLoadInfo []

- Hem InstallDate

- Int16 KeyboardPasswordStatus

- Dizisinde Lastloadınfo

- Dizisinde Üreticisini

- Dizisinde Modelinizi

- Dizisinde NameFormat

- Boolean NetworkServerModeEnabled

- Int32 NumberOfProcessors

- Dizisinde OEMLogoBitmap

- Dizisinde OEMStringArray []

- (SInt64) PauseAfterReset

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 PowerOnPasswordStatus

- Int16 PowerState

- Int16 PowerSupplyState

- Dizisinde BIG Yownerkişisi

- Dizisinde BIW Yownername

- Int16 ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- Dizisinde Roller []

- Dizisinde Durumlarına

- Dizisinde SupportContactDescription []

- Int16 SystemStartupDelay

- Dizisinde SystemStartupOptions []

- UInt8 SystemStartupSetting

- Dizisinde SystemType

- Int16 Termalil

- Int64 TotalPhysicalMemory

- Dizisinde Nitelen

- Int16 WakeUpType



## <a name="computer-system-ex"></a>Bilgisayar sistemi EX

Ad alanı: root\cimv2

sınıf CCM_ComputerSystemExtended


- Dizisinde Ada

- Int16 PCSystemType



## <a name="computer-system-product"></a>Bilgisayar Sistemi Ürünü

Ad alanı: root\cimv2

sınıf Win32_ComputerSystemProduct


- Dizisinde Identifyingnumber

- Dizisinde Ada

- Dizisinde Sürüm

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Dizisinde Skunumarası

- Dizisinde EDIN

- Dizisinde Satıcınıza



## <a name="sms-advanced-client-ports"></a>SMS Gelişmiş İstemci bağlantı noktaları

Ad alanı: root\cimv2

sınıf Win32Reg_SMSAdvancedClientPorts


- Dizisinde InstanceKey

- Int32 HttpsPortName

- Int32 PortName



## <a name="sms-advanced-client-ssl-configurations"></a>SMS Gelişmiş İstemci SSL yapılandırması

Ad alanı: root\cimv2

sınıf Win32Reg_SMSAdvancedClientSSLConfiguration


- Dizisinde InstanceKey

- Dizisinde CertificateSelectionCriteria

- Dizisinde Sertifika deposu

- Int32 Clientalwaysonınternet

- Int32 HttpsStateFlags

- Dizisinde Internetmphostname

- Int32 SelectFirstCertificate



## <a name="sms-advanced-client-state"></a>SMS Gelişmiş İstemci durumu

Ad alanı: root\ccm

sınıf CCM_InstalledComponent


- Dizisinde Ada

- Dizisinde DisplayName

- Dizisinde Sürüm



## <a name="connected-device"></a>Bağlı cihaz

Ad alanı: root\SmsDm

sınıf SMS_ActiveSyncConnectedDevice


- Dizisinde DeviceOEMInfo

- Dizisinde DeviceType

- Dizisinde OS_Major

- Dizisinde OS_Minor

- Dizisinde OS_Platform

- Dizisinde ProcessorArchitecture

- Dizisinde ProcessorLevel

- Dizisinde ProcessorRevision

- Dizisinde Instalbir ClientID

- Dizisinde Instalınstalclientserver

- Dizisinde Instalınstalclientversion

- Dizisinde LastSyncTime

- Dizisinde OS_AdditionalInfo

- Dizisinde OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

Ad alanı: Root\Cimv2\Sms

sınıf SMS_DefaultBrowser


- Dizisinde Browserprogıd



## <a name="desktop"></a>Masaüstü

Ad alanı: root\cimv2

sınıf Win32_Desktop


- Dizisinde Ada

- Int32 BorderWidth

- Dizisinde Başlığını

- Boolean CoolSwitch

- Int32 CursorBlinkRate

- Dizisinde Açıklaması

- Boolean DragFullWindows

- Int32 Gridayrıntı düzeyi

- Int32 Ispacing

- Dizisinde Ititlefacename

- Int32 Icontitleboyutu

- Boolean IconTitleWrap

- Dizisinde Kalıp

- Boolean Screensaveractıve

- Dizisinde ScreenSaverExecutable

- Boolean ScreenSaverSecure

- Int32 ScreenSaverTimeout

- Dizisinde SettingID

- Dizisinde Duvar

- Boolean Duvar kağıdı uzatılmış

- Boolean Duvar kağıdı döşeli



## <a name="desktop-monitor"></a>Masaüstü Izleyicisi

Ad alanı: root\cimv2

sınıf Win32_DesktopMonitor


- Dizisinde DeviceID

- Int16 Sonrası

- Int32 Bant genişliği

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int16 DisplayType

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Boolean IsLocked

- Int32 LastErrorCode

- Dizisinde Izleme üreticisi

- Dizisinde MonitorType

- Dizisinde Ada

- Int32 Pixelsperxlogicalinç

- Int32 Pixelsperyılogicalinç

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int32 Ekran yüksekliği

- Int32 Ekran genişliği

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName



## <a name="device-info"></a>Cihaz bilgileri

Ad alanı: ayrılmış

sınıf Device_Info


- Dizisinde Certexpi

- Dizisinde DeviceName

- Dizisinde Üreticisini

- Dizisinde Modelinizi

- Dizisinde ATAYAMADı



## <a name="mdm-devdetail"></a>MDM DevDetail

Ad alanı: root\cimv2\mdm\dmmap

sınıf MDM_DevDetail_Ext01


- Dizisinde InstanceId

- Dizisinde ParentID

- Dizisinde DeviceHardwareData

- Dizisinde WLANMACAddress



## <a name="disk"></a>Disk

Ad alanı: root\cimv2

sınıf Win32_DiskDrive


- Dizisinde DeviceID

- Int16 Sonrası

- Int32 Bytespersektör

- Int16 Yetenekler []

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Dizisinde CompressionMethod

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Int64 DefaultBlockSize

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde Errormetodolojisi

- Int32 İndeks

- Hem InstallDate

- Dizisinde InterfaceType

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int64 MaxBlockSize

- Int64 MaxMediaSize

- Boolean Ortam

- Dizisinde Type

- Int64 MinBlockSize

- Dizisinde Modelinizi

- Dizisinde Ada

- Boolean Gereksiz korlama

- Int32 Desteklenmeyen numberofmedias

- Int32 Bölüme

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int32 SCSIBus

- Int16 SCSILogicalUnit

- Int16 SCSIPort

- Int16 Scsitargetıd

- Int32 SectorsPerTrack

- Int64 Boyutla

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Int64 Toplam silindir sayısı

- Int32 TotalHeads

- Int64 Toplam kesimler

- Int64 Toplam Izler

- Int32 Trackspersilindir



## <a name="partition"></a>Bölüm

Ad alanı: root\cimv2

sınıf Win32_DiskPartition


- Dizisinde DeviceID

- Int16 Erişmesini

- Int16 Sonrası

- Int64 Kullanılanla

- Boolean Kopya

- Boolean BootPartition

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int32 DiskIndex

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde Errormetodolojisi

- Int32 Hiddensektörleri

- Int32 İndeks

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Ada

- Int64 NumberOfBlocks

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Boolean Birincil bölüm

- Dizisinde Amaçla

- Boolean RewritePartition

- Int64 Boyutla

- Int64 Startingkayması

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Dizisinde Türüyle



## <a name="dma"></a>DMA

Ad alanı: root\cimv2

sınıf Win32_DeviceMemoryAddress

- Int64 StartingAddress

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Int64 EndingAddress

- Hem InstallDate

- Dizisinde MemoryType

- Dizisinde Ada

- Dizisinde Durumlarına



## <a name="dma-channel"></a>DMA kanalı

Ad alanı: root\cimv2

sınıf Win32_DMAChannel


- Int32 DMA kanalı

- Int16 Adresssize

- Int16 Sonrası

- Boolean BurstMode

- Int16 ByteMode

- Dizisinde Başlığını

- Int16 Channelzamanlaması

- Dizisinde Açıklaması

- Hem InstallDate

- Int32 MAXTRANSFERSIZE

- Dizisinde Ada

- Int32 Bağ

- Dizisinde Durumlarına

- Int16 Transfergenişlikleri []

- Int16 Typeczamanlaması

- Int16 WordMode



## <a name="driver---vxd"></a>Sürücü-VxD

Ad alanı: root\cimv2

sınıf Win32_DriverVXD


- Dizisinde Ada

- Dizisinde SoftwareElementID

- Int16 SoftwareElementState

- Int16 TargetOperatingSystem

- Dizisinde Sürüm

- Dizisinde BuildNumber

- Dizisinde Başlığını

- Dizisinde Kod kümesi

- Dizisinde Denetimle

- Dizisinde Açıklaması

- Dizisinde DeviceDescriptorBlock

- Dizisinde Identifiationcode

- Hem InstallDate

- Dizisinde LanguageEdition

- Dizisinde Üreticisini

- Dizisinde OtherTargetOS

- Dizisinde PM_API

- Dizisinde Number

- Int32 ServiceTableSize

- Dizisinde Durumlarına

- Dizisinde V86_API



## <a name="embedded-device-information"></a>Katıştırılmış cihaz bilgileri

Ad alanı: Root\Cimv2\Sms

sınıf CCM_EmbeddedDeviceInformation


- Dizisinde DeviceType

- Dizisinde Modelinizi

- Dizisinde OEMName



## <a name="environment"></a>Ortam

Ad alanı: root\cimv2

sınıf Win32_Environment


- Dizisinde Ada

- Dizisinde Nitelen

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Hem InstallDate

- Dizisinde Durumlarına

- Boolean SystemVariable

- Dizisinde VariableValue



## <a name="firmware"></a>Üretici yazılımı

Ad alanı: Root\Cimv2\Sms

sınıf SMS_Firmware


- Boolean UEFı

- Boolean Olup



## <a name="usm-folder-redirection-health"></a>USD klasör yeniden yönlendirme sistem durumu

Ad alanı: Root\Cimv2\Sms

sınıf SMS_FolderRedirectionHealth


- Dizisinde KlasörAdı

- Dizisinde SID

- UInt8 HealthStatus

- Hem Lastbaşarıyla Fulsynctime

- UInt8 LastSyncStatus

- Hem LastSyncTime

- Boolean OfflineAccessEnabled

- Dizisinde OfflineFileNameFolderGUID

- Boolean Diğine



## <a name="ide-controller"></a>IDE denetleyicisi

Ad alanı: root\cimv2

sınıf Win32_IDEController


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int32 Maxnumberkontrollü

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="add-remove-programs-64"></a>Program kaldırma Ekle (64)

Ad alanı: root\cimv2

sınıf Win32Reg_AddRemovePrograms64


- Dizisinde ProdID

- Dizisinde DisplayName

- Dizisinde InstallDate

- Dizisinde 'In

- Dizisinde Sürüm



## <a name="add-remove-programs"></a>Program kaldır ekle

Ad alanı: root\cimv2

sınıf Win32Reg_AddRemovePrograms


- Dizisinde ProdID

- Dizisinde DisplayName

- Dizisinde InstallDate

- Dizisinde 'In

- Dizisinde Sürüm



## <a name="installed-executable"></a>Yüklenen yürütülebilir

Ad alanı: Root\Cimv2\Sms

sınıf SMS_InstalledExecutable


- Dizisinde ExecutableName

- Dizisinde ProductCode

- Dizisinde BinFileVersion

- Dizisinde BinProductVersion

- Dizisinde Açıklaması

- Dizisinde Dosya özellikleri karması

- Dizisinde FilePropertiesHashEx

- Int32 İ

- Dizisinde FileVersion

- Boolean HasPatchAdded

- Dizisinde Instalınstalfilepath

- Boolean Issystemdosyası

- Boolean Ivıtalfile

- Int32 Dildir

- Dizisinde Ürünüyle

- Dizisinde ProductVersion

- Dizisinde 'In



## <a name="installed-software"></a>Yüklü yazılım

Ad alanı: Root\Cimv2\Sms

sınıf SMS_InstalledSoftware


- Dizisinde SoftwareCode

- Dizisinde ARPDisplayName

- Dizisinde ChannelCode

- Dizisinde Channelıd

- Dizisinde CM_DSLID

- Dizisinde Açık olma

- Hem InstallDate

- Int32 Installdirectoryvalidation

- Dizisinde Instalınstalo konumu

- Dizisinde Installsource

- Int32 InstallType

- Int32 Dildir

- Dizisinde LocalPackage

- Dizisinde MPC

- Int32 OsComponent

- Dizisinde PackageCode

- Dizisinde ProductID

- Dizisinde ProductName

- Dizisinde ProductVersion

- Dizisinde 'In

- Dizisinde RegisteredUser

- Dizisinde Paketi

- Dizisinde SoftwarePropertiesHash

- Dizisinde SoftwarePropertiesHashEx

- Dizisinde UninstallString

- Dizisinde UpgradeCode

- Int32 VersionAna

- Int32 VersionMinor



## <a name="irq-table"></a>IRQ Tablosu

Ad alanı: root\cimv2

sınıf Win32_IRQResource


- Int32 IRQ numarası

- Int16 Sonrası

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Boolean Donanım

- Hem InstallDate

- Dizisinde Ada

- Boolean Paylaşılabilir

- Dizisinde Durumlarına

- Int16 TriggerLevel

- Int16 TriggerType

- Int32 Vektör



## <a name="keyboard"></a>Klavye

Ad alanı: root\cimv2

sınıf Win32_Keyboard


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Boolean IsLocked

- Int32 LastErrorCode

- Dizisinde Düzenle

- Dizisinde Ada

- Int16 NumberOfFunctionKeys

- Int16 Parolayı

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName



## <a name="load-order-group"></a>Yükleme sırası grubu

Ad alanı: root\cimv2

sınıf Win32_LoadOrderGroup


- Dizisinde Ada

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Boolean DriverEnabled

- Int32 GroupOrder

- Hem InstallDate

- Dizisinde Durumlarına



## <a name="logical-disk"></a>Mantıksal disk

Ad alanı: Root\Cimv2\Sms

sınıf SMS_LogicalDisk


- Dizisinde DeviceID

- Int16 Erişmesini

- Int16 Sonrası

- Int64 Kullanılanla

- Dizisinde Başlığını

- Boolean Dınız

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int32 Drvetype

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde Errormetodolojisi

- Dizisinde Biçimlendiri

- Int64 FreeSpace

- Hem InstallDate

- Int32 LastErrorCode

- Int32 MaximumComponentLength

- Int32 Type

- Dizisinde Ada

- Int64 NumberOfBlocks

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Adı

- Dizisinde Amaçla

- Int64 Boyutla

- Dizisinde Durumlarına

- Int16 StatusInfo

- Boolean SupportsFileBasedCompression

- Dizisinde SystemName

- Dizisinde VolumeName

- Dizisinde Birimserialnumber



## <a name="memory"></a>Bellek

Ad alanı: root\cimv2

sınıf CCM_LogicalMemoryConfiguration


- Dizisinde Ada

- Int64 AvailableVirtualMemory

- Int64 Totalpagespace

- Int64 TotalPhysicalMemory

- Int64 TotalVirtualMemory



## <a name="device-bluetooth"></a>Cihaz Bluetooth 'U

Ad alanı: ayrılmış

sınıf Device_Bluetooth


- Boolean Etkinletir



## <a name="device-camera"></a>Cihaz Kamerası

Ad alanı: ayrılmış

sınıf Device_Camera


- Boolean Etkinletir



## <a name="device-certificates"></a>Cihaz sertifikaları

Ad alanı: ayrılmış

sınıf Device_Certificates


- Dizisinde #C0

- Dizisinde Türüyle

- Dizisinde IssuedBy

- Dizisinde IssuedTo

- Hem ValidFrom

- Hem ValidTo



## <a name="device-client"></a>Cihaz Istemcisi

Ad alanı: ayrılmış

sınıf Device_Client


- Boolean DownloadWhenRoaming

- Boolean SyncWhenRoaming



## <a name="device-client-agent-version"></a>Cihaz Istemci Aracısı sürümü

Ad alanı: ayrılmış

sınıf Device_ClientAgentVersion


- Dizisinde Sürüm



## <a name="device-computer-system"></a>Cihaz bilgisayar sistemi

Ad alanı: ayrılmış

sınıf Device_ComputerSystem


- Dizisinde CellularTechnology

- Dizisinde DeviceClientID

- Dizisinde DeviceManufacturer

- Dizisinde DeviceModel

- Dizisinde DMVersion

- Dizisinde FirmwareVersion

- Dizisinde HardwareVersion

- Dizisinde IMEı

- Dizisinde IMSı

- UInt8 Iactivationlockenabled

- UInt8 Jailbreak uygulanmış

- Dizisinde MEıD

- Dizisinde $

- Dizisinde PhoneNumber

- Dizisinde PlatformType

- Int32 ProcessorArchitecture

- Int32 ProcessorLevel

- Int32 ProcessorRevision

- Dizisinde Ürünüyle

- Dizisinde ProductVersion

- Dizisinde Number

- Dizisinde SoftwareVersion

- Dizisinde SubscriberCarrierNetwork



## <a name="device-display"></a>Cihaz görüntüleme

Ad alanı: ayrılmış

sınıf Device_Display


- Int32 HorizontalResolution

- Int64 NumberOfColors

- Int32 VerticalResolution



## <a name="device-email"></a>Cihaz e-postası

Ad alanı: ayrılmış

sınıf Device_Email


- Dizisinde Sahipeadresi

- Dizisinde SyncDomain

- Dizisinde SyncServer

- Dizisinde SyncUser

- Dizisinde Türüyle



## <a name="device-encryption"></a>Cihaz şifreleme

Ad alanı: ayrılmış

sınıf Device_Encryption


- Int32 EmailEncryptionAlgorithm

- Int32 EmailEncryptionNegotiation

- Boolean EmailEncryptionRequired

- Boolean EmailSigningAlgorithm

- Boolean EmailSigningRequired

- Boolean Encryptionuyumluluğu

- Boolean PhoneMemoryEncrypted

- Boolean StorageCardEncrypted



## <a name="device-exchange"></a>Cihaz değişimi

Ad alanı: ayrılmış

sınıf Device_Exchange


- Boolean ConflictResolution

- (SInt32) Htmtamailkesilme

- Int32 MailFormat

- Int32 MaxCalendarAge

- Int32 MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- Int32 OffPeakSyncFrequency

- Int32 En sivri gün

- Dizisinde PeakEndTime

- Dizisinde PeakStartTime

- Int32 PeakSyncFrequency

- (SInt32) Plaintextemailkesilme

- Boolean Sendemailhemen

- Boolean SyncCalendar

- Boolean SyncContacts

- Boolean SyncEmail

- Boolean SyncTasks

- Boolean SyncWhenRoaming



## <a name="device-installed-applications"></a>Cihaz yüklü uygulamalar

Ad alanı: ayrılmış

sınıf Device_InstalledApplications


- Dizisinde Ada

- Dizisinde Sürüm



## <a name="device-irda"></a>Cihaz IrDA

Ad alanı: ayrılmış

sınıf Device_IrDA


- Boolean Etkinletir



## <a name="mobile-device-location"></a>Mobil cihaz konumu

Ad alanı: ayrılmış

sınıf MDM_RemoteFind


- (Real32) En

- (Real32) MIN



## <a name="device-memory"></a>Cihaz belleği

Ad alanı: ayrılmış

sınıf Device_Memory


- Int64 ProgramFree

- Int64 Program toplamı

- Int64 RemovableStorageFree

- Int64 RemovableStorageTotal

- Int64 StorageFree

- Int64 StorageTotal



## <a name="device-os-information"></a>Cihaz işletim sistemi bilgileri

Ad alanı: ayrılmış

sınıf Device_OSInformation


- Dizisinde Dildir

- Dizisinde Platformunun

- Dizisinde Sürüm



## <a name="device-password"></a>Cihaz parolası

Ad alanı: ayrılmış

sınıf Device_Password


- Boolean AllowRecoveryPassword

- Int32 Oto LockTimeout

- Boolean Etkinletir

- Int32 Dolmadan

- Int32 Geçmişi

- Int32 MaxAttemptsBeforeWipe

- Int32 MinComplexChars

- Int32 MinLength

- UInt8 PasswordQuality

- Int32 Türüyle



## <a name="device-policy"></a>Cihaz Ilkesi

Ad alanı: ayrılmış

sınıf Device_Policy


- Dizisinde Ada

- Boolean Zorlamalı



## <a name="device-power"></a>Cihaz gücü

Ad alanı: ayrılmış

sınıf Device_Power


- Int32 Backaçık Tactimeout

- Int32 BacklightBatTimeout

- (SInt32) Yedekleme yüzdesi

- (SInt32) % Batter



## <a name="mobile-device-security-status"></a>Mobil cihaz güvenlik durumu

Ad alanı: ayrılmış

sınıf MDM_SecurityStatus


- Int32 HardwareEncryptionCaps

- UInt8 Passcodeuyumlu

- UInt8 Passcodekarmaşıkantwithprofiles

- UInt8 Pacodepyeniden gönderildi

- UInt8 RequireEncryption



## <a name="device-windows-security-policy"></a>Cihaz Windows Güvenlik Ilkesi

Ad alanı: ayrılmış

sınıf Device_WindowsSecurityPolicy


- Int32 NUMARASıNı

- Dizisinde Ada

- Int32 Deeri



## <a name="device-wlan"></a>Cihaz WLAN

Ad alanı: ayrılmış

sınıf Device_WLAN


- Boolean Etkinletir

- Dizisinde EthernetMAC

- Dizisinde WiFiMAC



## <a name="modem"></a>Modemi

Ad alanı: root\cimv2

sınıf Win32_POTSModem


- Dizisinde DeviceID

- Int16 AnswerMode

- Dizisinde AttachedTo

- Int16 Sonrası

- Dizisinde Çamakff

- Dizisinde Görme Don

- Dizisinde Başlığını

- Dizisinde CompatibilityFlags

- Int16 Compressionınfo

- Dizisinde CompressionOff

- Dizisinde CompressionOn

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde ConfigurationDialog

- Dizisinde CountriesSupported []

- Dizisinde CountrySelected

- Dizisinde Currentşifreler []

- Dizisinde DCB

- Dizisinde Varsayılanını

- Dizisinde Açıklaması

- Dizisinde DeviceLoader

- Dizisinde DeviceType

- Int16 DialType

- Hem DriverDate

- Boolean Errortemizlendi

- Dizisinde Errorcontrolzorlandı

- Int16 Errorcontrolinınfo

- Dizisinde ErrorControlOff

- Dizisinde ErrorControlOn

- Dizisinde ErrorDescription

- Dizisinde FlowControlHard

- Dizisinde FlowControlOff

- Dizisinde FlowControlSoft

- Dizisinde InactivityScale

- Int32 InactivityTimeout

- Int32 İndeks

- Hem InstallDate

- Int32 LastErrorCode

- Int32 MaxBaudRateToPhone

- Int32 MaxBaudRateToSerialPort

- Int16 Maxnumberofparolalarla

- Dizisinde Modelinizi

- Dizisinde ModemInfPath

- Dizisinde ModemInfSection

- Dizisinde Modülationbell

- Dizisinde Modülationccıtt

- Int16 Modülationscheme

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Dizisinde Portaltsınıfı

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Koy

- Dizisinde Özelliklerinin

- Dizisinde Adı

- Dizisinde Pulse

- Dizisinde Döndürmek

- Dizisinde ResponsesKeyName

- UInt8 RingsBeforeAnswer

- Dizisinde Hoparlörlü Kermodedial

- Dizisinde Hoparlörlü Kermode kapalı

- Dizisinde Hoparlörlü Kermodeon

- Dizisinde Hoparlörkermodesetup

- Dizisinde SpeakerVolumeHigh

- Int16 Hoparlörkervolumeınfo

- Dizisinde Hoparlörlü en düşük

- Dizisinde SpeakerVolumeMed

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde StringFormat

- Boolean SupportsCallback

- Boolean SupportsSynchronousConnect

- Dizisinde SystemName

- Dizisinde Ayırıcı

- Hem TimeOfLastReset

- Dizisinde Algılayamadı

- Dizisinde VoiceSwitchFeature



## <a name="motherboard"></a>Kartı

Ad alanı: root\cimv2

sınıf Win32_MotherboardDevice


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde PrimaryBusType

- Dizisinde RevisionNumber

- Dizisinde SecondaryBusType

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName


## <a name="nap-client"></a>NAP Istemcisi

Ad alanı: root\Nap

sınıf NAP_Client


- (Dize) adı

- (Dize) açıklaması

- (Dize) fixupURL 'Si

- (Boolean) napEnabled

- (Dize) napProtocolVersion

- (Dize) olasılık saati

- (UInt32) systemIsolationState



## <a name="nap-system-health-agent"></a>NAP sistem durumu Aracısı

Ad alanı: root\Nap

sınıf NAP_SystemHealthAgent


- Int32 NUMARASıNı

- (Dize) açıklaması

- (UInt32) fixupState

- (Dize) friendlyName

- (Dize) ınfoclsıd

- (Boolean) ısınlen

- (UInt8) yüzdesi

- (Dize) registrationDate

- (Dize) SatıcıAdı

- (Dize) sürümü



## <a name="network-adapter"></a>Ağ bağdaştırıcısı

Ad alanı: root\cimv2

sınıf Win32_NetworkAdapter


- Dizisinde DeviceID

- Dizisinde AdapterType

- Boolean Oto tanıma

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int32 İndeks

- Hem InstallDate

- Boolean Yüklendiyse

- Int32 LastErrorCode

- Dizisinde MACAddress

- Dizisinde Üreticisini

- Int32 Maxnumberkontrollü

- Int64 MaxSpeed

- Dizisinde Ada

- Dizisinde NetworkAddresses []

- Dizisinde PermanentAddress

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde ProductName

- Dizisinde HizmetAdı

- Int64 Inız

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="network-adapter-configuration"></a>Ağ bağdaştırıcısı yapılandırması

Ad alanı: root\cimv2

sınıf Win32_NetworkAdapterConfiguration


- Int32 İndeks

- Boolean ArpAlwaysSourceRoute

- Boolean ArpUseEtherSNAP

- Dizisinde Başlığını

- Dizisinde DatabasePath

- Boolean DeadGWDetectEnabled

- Dizisinde DefaultIPGateway []

- UInt8 DefaultTOS

- UInt8 DefaultTTL

- Dizisinde Açıklaması

- Boolean DHCPEtkin

- Hem DHCPLeaseExpires

- Hem Dhcpleaseedinilen

- Dizisinde Dhcpserver yazın

- Dizisinde DNSDomain

- Dizisinde Dnsdomainsonssearchorder []

- Boolean DNSEnabledForWINSResolution

- Dizisinde DNSHostName

- Dizisinde DNSServerSearchOrder []

- Boolean DomainDNSRegistrationEnabled

- Int32 Değerinin

- Boolean FullDNSRegistrationEnabled

- Int16 GatewayCostMetric []

- UInt8 IGMPLevel

- Dizisinde IPAddress []

- Int32 IPConnectionMetric

- Boolean IPEnabled

- Boolean IPFilterSecurityEnabled

- Boolean IPPortSecurityEnabled

- Dizisinde Ipsecpermıtipprotocols []

- Dizisinde IPSecPermitTCPPorts []

- Dizisinde IPSecPermitUDPPorts []

- Dizisinde IPSubnet []

- Boolean IPUseZeroBroadcast

- Dizisinde IPXAddress

- Boolean IPXEnabled

- Dizisinde IPXFrameType

- Int32 IPXMediaType

- Dizisinde IPXNetworkNumber []

- Dizisinde IPXVirtualNetNumber

- Int32 Keepaliveınterval

- Int32 KeepAliveTime

- Dizisinde MACAddress

- Int32 BOYUTUNU

- Int32 NumForwardPackets

- Boolean PMTUBHDetectEnabled

- Boolean PMTUDiscoveryEnabled

- Dizisinde HizmetAdı

- Dizisinde SettingID

- Int32 TcpipNetbiosOptions

- Int32 TcpMaxConnectRetransmissions

- Int32 TcpMaxDataRetransmissions

- Int32 TcpNumConnections

- Boolean TcpUseRFC1122UrgentPointer

- Int16 TCP

- Boolean WINSEnableLMHostsLookup

- Dizisinde WINSHostLookupFile

- Dizisinde Winsprimarrivserver

- Dizisinde Winsscopramazan

- Dizisinde WINSSecondaryServer



## <a name="network-client"></a>Ağ Istemcisi

Ad alanı: root\cimv2

sınıf Win32_NetworkClient


- Dizisinde Ada

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Hem InstallDate

- Dizisinde Üreticisini

- Dizisinde Durumlarına



## <a name="network-login-profile"></a>Ağ oturum açma profili

Ad alanı: root\cimv2

sınıf Win32_NetworkLoginProfile


- Dizisinde Ada

- Hem AccountExpires

- Int32 AuthorizationFlags

- Int32 BadPasswordCount

- Dizisinde Başlığını

- Int32 Sayfasının

- Dizisinde Açıklamanın

- Int32 CountryCode

- Dizisinde Açıklaması

- Int32 Larına

- Dizisinde FullName

- Dizisinde HomeDirectory

- Dizisinde HomeDirectoryDrive

- Hem LastLogoff

- Hem LastLogon

- Dizisinde LogonHours

- Dizisinde LogonServer

- Int64 MaximumStorage

- Int32 Oturum açma sayısı

- Dizisinde Parametrelere

- Hem Passwordavge

- Hem PasswordExpires

- Int32 PrimaryGroupID

- Int32 Ayrıcalıkları

- Dizisinde Profilinizi

- Dizisinde ScriptPath

- Dizisinde SettingID

- Int32 UnitsPerWeek

- Dizisinde UserComment

- Int32 UserID

- Dizisinde UserType

- Dizisinde İş istasyonları



## <a name="nt-eventlog-file"></a>NT EventLog dosyası

Ad alanı: root\cimv2

sınıf Win32_NTEventlogFile


- Dizisinde Ada

- Int32 AccessMask

- Boolean Arşivliyorsanız

- Dizisinde Başlığını

- Boolean Dınız

- Dizisinde CompressionMethod

- Hem CreationDate

- Dizisinde Açıklaması

- Dizisinde Sürücü

- Dizisinde Sekizinci Tdotthreefilename

- Boolean Memiştir

- Dizisinde EncryptionMethod

- Dizisinde Uzantının

- Dizisinde Kısaltın

- Int64 İ

- Dizisinde FileType

- Dizisinde FS adı

- Boolean Lene

- Hem InstallDate

- Int64 InUseCount

- Hem Lastacce

- Hem LastModified

- Dizisinde LogfileName

- Dizisinde Üreticisini

- Int32 MaxFileSize

- Int32 KayıtSayısı

- Int32 Overwritegüncelliğini yitirmiş

- Dizisinde OverWritePolicy

- Dizisinde Yolun

- Boolean Ama

- Dizisinde Kaynaklar []

- Dizisinde Durumlarına

- Boolean Sistemin

- Dizisinde Sürüm

- Boolean Yazılabilir



## <a name="office365proplusconfigurations"></a>Office365ProPlusConfigurations

Ad alanı: root\cimv2

sınıf Office365ProPlusConfigurations


- Dizisinde Işareti

- Dizisinde Oto yükselt

- Dizisinde CCMManaged

- Dizisinde CDNBaseUrl 'Si

- (Dize) cfgUpdateChannel

- Dizisinde ClientCulture

- Dizisinde ClientFolder

- Dizisinde GPOChannel

- Dizisinde GPOOfficeMgmtCOM

- Dizisinde YüklemeYolu

- Dizisinde LastScenario

- Dizisinde LastScenarioResult

- Dizisinde OfficeMgmtCOM

- Dizisinde Platformunun

- Dizisinde Sharedcomputerlisanslama

- Dizisinde UpdateChannel

- Dizisinde UpdatePath

- Dizisinde UpdatesEnabled

- Dizisinde UpdateUrl

- Dizisinde VersionToReport



## <a name="office-addin"></a>Office eklentisi

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeAddin


- Dizisinde Mimarisini

- Dizisinde NUMARASıNı

- Dizisinde OfficeUygulaması

- Dizisinde Türüyle

- Int32 AverageLoadTimeInMilliseconds

- Dizisinde IN

- Dizisinde Tadı

- Int32 CrashCount sayısı

- Dizisinde Açıklaması

- Int32 ErrorCount

- Dizisinde Kısaltın

- Int64 İ

- Int32 FileTimestamp

- Dizisinde FileVersion

- Dizisinde FriendlyName

- Dizisinde Yakarynamehash

- Dizisinde Idhash

- Int32 LoadBehavior

- Int32 LoadCount

- Int32 LoadFailCount

- Dizisinde ProductName

- Dizisinde ProductVersion



## <a name="office-client-metric"></a>Office Istemci ölçümü

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeClientMetric


- Dizisinde OfficeUygulaması

- Int32 CompatibilityErrorCount

- Int32 CrashedSessionCount

- Int32 Makro Compileerrorcount

- Int32 MacroRuntimeErrorCount

- Int32 SessionCount



## <a name="office-device-summary"></a>Office cihaz Özeti

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeDeviceSummary


- Boolean Iproplusyüklü

- Boolean IsTelemetryEnabled



## <a name="office-document-metric"></a>Office belge ölçümü

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeDocumentMetric


- Dizisinde OfficeUygulaması

- Int32 TotalCloudDocs

- Int32 TotalLegacyDocs

- Int32 TotalLocalDocs

- Int32 TotalMacroDocs

- Int32 Totalnonmakrodocs

- Int32 TotalUncDocs



## <a name="office-document-solution"></a>Office belge çözümü

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeDocumentSolution


- Dizisinde Documentsolutionıd

- Dizisinde OfficeUygulaması

- Int32 CompatibilityErrorCount

- Int32 CrashCount sayısı

- Dizisinde Örnek dosya adı

- Int32 LoadCount

- Int32 LoadFailCount

- Int32 Makro Compileerrorcount

- Int32 MacroRuntimeErrorCount

- Dizisinde Türüyle



## <a name="office-macro-error"></a>Office makro hatası

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeMacroError


- Dizisinde Documentsolutionıd

- Int32 Raporladı

- Int32 Biriktirme

- Int64 Ladin Currence

- Dizisinde Türüyle



## <a name="office-product-info"></a>Office ürün bilgileri

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeProductInfo


- Dizisinde ProductName

- Dizisinde ProductVersion

- Dizisinde Mimarisini

- Dizisinde Kanalla

- Int32 Iproplusyüklü

- Dizisinde Dildir

- Dizisinde LicenseState



## <a name="office-vba-rule-violation"></a>Office VBA kural Ihlali

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeVbaRuleViolation


- Int32 RuleId

- Int32 FileCount

- Dizisinde OfficeUygulaması



## <a name="office-vbasummary"></a>Office VbaSummary

Ad alanı: Root\ccm\ınvagt

sınıf CCM_OfficeVbaScanResultsSummary


- Int32 Tasarıma

- Int32 Design64

- Int32 DuplicateVba

- Boolean HasResults

- Int32 HasVba

- Int32 Erişilemez

- Int32 Çıkışları

- Int32 Issues64

- Int32 Issuesnone

- Int32 IssuesNone64

- Int32 Kilitlenecek

- Int32 NoVba

- Int32 Korunamadı

- Int32 RemLimited

- Int32 RemLimited64

- Int32 Remönemli

- Int32 RemSignificant64

- Int32 Inızı

- Int32 Score64

- Int32 Toplamda

- Int32 Doğrulamasına

- Int32 Validation64



## <a name="operating-system"></a>İşletim Sistemi

Ad alanı: root\cimv2

sınıf Win32_OperatingSystem


- Dizisinde Ada

- Dizisinde BootDevice

- Dizisinde BuildNumber

- Dizisinde BuildType

- Dizisinde Başlığını

- Dizisinde Kod kümesi

- Dizisinde CountryCode

- Dizisinde CSDVersion

- (SInt16) CurrentTimeZone

- Boolean H

- Dizisinde Açıklaması

- Boolean Dağıtılmış

- UInt8 Foregroundadboost

- Int64 FreePhysicalMemory

- Int64 FreeSpaceInPagingFiles

- Int64 FreeVirtualMemory

- Hem InstallDate

- Hem Lastbootçalışma süresi

- Hem LocalDateTime

- Dizisinde Ayarlar

- Dizisinde Üreticisini

- Int32 MaxNumberOfProcesses

- Int64 MaxProcessMemorySize

- Dizisinde MUILanguages []

- Int32 Numberoflicenusers

- Int32 Işlem sayısı

- Int32 Kullanıcı sayısı

- Int32 OperatingSystemSKU

- Dizisinde Kuruluşunuzun

- Dizisinde OSArchitecture

- Int32 OSLanguage

- Int32 OSProductSuite

- Int16 OSType

- Dizisinde Diğer tür açıklaması

- Dizisinde PlusProductID

- Dizisinde PlusVersionNumber

- Boolean Birinc

- Int32 ProductType

- Dizisinde RegisteredUser

- Dizisinde Number

- Int16 ServicePackMajorVersion

- Int16 ServicePackMinorVersion

- Int64 SizeStoredInPagingFiles

- Dizisinde Durumlarına

- Dizisinde SystemDevice

- Dizisinde SystemDirectory

- Int64 TotalSwapSpaceSize

- Int64 TotalVirtualMemorySize

- Int64 Totalvisiblememorrivsize

- Dizisinde Sürüm

- Dizisinde WindowsDirectory



## <a name="operating-system-ex"></a>İşletim sistemi EX

Ad alanı: root\cimv2

sınıf CCM_OperatingSystemExtended


- Dizisinde Ada

- Int32 ISTEYIN



## <a name="operating-system-recovery-configuration"></a>İşletim sistemi kurtarma yapılandırması

Ad alanı: root\cimv2

sınıf Win32_OSRecoveryConfiguration


- Dizisinde Ada

- Boolean Oto yeniden başlatma

- Dizisinde Başlığını

- Dizisinde DebugFilePath

- Dizisinde Açıklaması

- Boolean KernelDumpOnly

- Boolean OverwriteExistingDebugFile

- Boolean SendAdminAlert

- Dizisinde SettingID

- Boolean WriteDebugInfo

- Boolean WriteToSystemLog



## <a name="optional-feature"></a>İsteğe bağlı özellik

Ad alanı: root\cimv2

sınıf Win32_OptionalFeature


- Dizisinde Ada

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Hem InstallDate

- Int32 InstallState

- Dizisinde Durumlarına



## <a name="page-file-setting"></a>Sayfa dosyası ayarı

Ad alanı: root\cimv2

sınıf Win32_PageFileSetting


- Dizisinde Ada

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Int32 InitialSize

- Int32 Boyut

- Dizisinde SettingID



## <a name="parallel-port"></a>Paralel bağlantı noktası

Ad alanı: root\cimv2

sınıf Win32_ParallelPort


- Dizisinde DeviceID

- Int16 Sonrası

- Int16 Yetenekler []

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean DMASupport

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Int32 Maxnumberkontrollü

- Dizisinde Ada

- Boolean Osautokeşfedilen

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="bios"></a>'TAKI

Ad alanı: root\cimv2

sınıf Win32_BIOS


- Dizisinde Ada

- Dizisinde SoftwareElementID

- Int16 SoftwareElementState

- Int16 TargetOperatingSystem

- Dizisinde Sürüm

- Int16 BiosCharacteristics[]

- Dizisinde BIOSVersion []

- Dizisinde BuildNumber

- Dizisinde Başlığını

- Dizisinde Kod kümesi

- Dizisinde CurrentLanguage

- Dizisinde Açıklaması

- Dizisinde Identifiationcode

- Int16 InstallableLanguages

- Hem InstallDate

- Dizisinde LanguageEdition

- Dizisinde Lıflanguages []

- Dizisinde Üreticisini

- Dizisinde OtherTargetOS

- Boolean Primarybıos

- Hem ReleaseDate

- Dizisinde Number

- Dizisinde SMBIOSBIOSVersion

- Int16 SMBIOSMajorVersion

- Int16 SMBIOSMinorVersion

- Boolean Smbiospyeniden gönderildi

- Dizisinde Durumlarına



## <a name="pcmcia-controller"></a>PCMCIA denetleyicisi

Ad alanı: root\cimv2

sınıf Win32_PCMCIAController


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int32 Maxnumberkontrollü

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="physical-memory"></a>Fiziksel Bellek

Ad alanı: root\cimv2

sınıf Win32_PhysicalMemory


- Dizisinde CreationClassName

- Dizisinde Etiket

- Dizisinde BankLabel

- Int64 Kü

- Dizisinde Başlığını

- Int16 Veri genişliği

- Dizisinde Açıklaması

- Dizisinde DeviceLocator

- Int16 FormFactor

- Boolean Hotswap

- Hem InstallDate

- Int16 InterleaveDataDepth

- Int32 Interleaveposition

- Dizisinde Üreticisini

- Int16 MemoryType

- Dizisinde Modelinizi

- Dizisinde Ada

- Dizisinde OtherIdentifyingInfo

- Dizisinde PartNumber

- Int32 Positionınrow

- Boolean PoweredOn

- Boolean Çıkarılabilir

- Boolean Değiştirebilen

- Dizisinde Number

- Dizisinde ISTEYIN

- Int32 Inız

- Dizisinde Durumlarına

- Int16 TotalWidth

- Int16 TypeDetail

- Dizisinde Sürüm



## <a name="physicaldisk"></a>Fiziksel

Ad alanı: root\microsoft\windows\storage

sınıf MSFT_PhysicalDisk


- Dizisinde Uzantının

- Int64 Ayrılatedboyut

- Int16 BusType

- Int16 CannotPoolReason []

- Boolean CanPool

- Dizisinde Açıklaması

- Dizisinde DeviceID

- Int16 EnclosureNumber

- Dizisinde FirmwareVersion

- Dizisinde FriendlyName

- Int16 HealthStatus

- Boolean Isındicationenabled

- Boolean Ipartial

- Int64 LogicalSectorSize

- Dizisinde Üreticisini

- Int16 Type

- Dizisinde Modelinizi

- Int16 OperationalStatus []

- Dizisinde OtherCannotPoolReasonDescription

- Dizisinde PartNumber

- Dizisinde PhysicalLocation

- Int64 PhysicalSectorSize

- Dizisinde Number

- Int64 Boyutla

- Int16 SlotNumber alanlarında

- Dizisinde SoftwareVersion

- Int32 Mil hızı

- Int16 Supportedkullanımlarının []

- Dizisinde UniqueId

- Int16 Kullanımıyla



## <a name="pnp-device-driver"></a>PNP CIHAZ SÜRÜCÜSÜ

Ad alanı: root\cimv2

sınıf Win32_PnpEntity


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Dizisinde ClassGuid

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde CreationClassName

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Hizmetle

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemCreationClassName

- Dizisinde SystemName



## <a name="pointing-device"></a>İşaret eden cihaz

Ad alanı: root\cimv2

sınıf Win32_PointingDevice


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int16 DeviceInterface

- Int32 DoubleSpeedThreshold

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int16 El kullanımı

- Dizisinde HardwareType

- Dizisinde InfFileName

- Dizisinde InfSection

- Hem InstallDate

- Boolean IsLocked

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Dizisinde Ada

- UInt8 NumberOfButtons

- Dizisinde Pnpdeviceıd

- Int16 PointingType

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int32 QuadSpeedThreshold

- Int32 Çözünürlüğüne

- Int32 Örnekleray

- Dizisinde Durumlarına

- Int16 StatusInfo

- Int32 Tablosunun

- Dizisinde SystemName



## <a name="portable-battery"></a>Taşınabilir pil

Ad alanı: root\cimv2

sınıf Win32_PortableBattery


- Dizisinde DeviceID

- Int16 Sonrası

- Int16 Batteryıstatus

- Int16 CapacityMultiplier

- Dizisinde Başlığını

- Int16 Kimya

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int32 Tasarım kapasitesi

- Int64 Tasarım gerilimi

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int16 EstimatedChargeRemaining

- Int32 EstimatedRunTime

- Int32 ExpectedLife

- Int32 FullChargeCapacity

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Konumuna

- Dizisinde Üreten bir tarih

- Dizisinde Üreticisini

- Int16 MaxBatteryError

- Int32 MaxRechargeTime

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Smartbatteryıversion

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Int32 Timeonpili

- Int32 Timetofullücret



## <a name="ports"></a>Bağlantı noktaları

Ad alanı: root\cimv2

sınıf Win32_PortResource

- Int64 StartingAddress

- Boolean Ek

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Int64 EndingAddress

- Hem InstallDate

- Dizisinde Ada

- Dizisinde Durumlarına



## <a name="power-capabilities"></a>Güç özellikleri

Ad alanı: root\CCM\powermanagementagent

sınıf CCM_PwrMgmtSystemPowerCapabilities


- Int32 PreferredPMProfile

- Boolean Yeniden gönderildi

- Boolean Batteriesareshorbed

- Boolean FullWake

- Boolean Lidsun

- Dizisinde MinDeviceWakeState

- Boolean Processorazaltma

- Dizisinde RtcWake

- Boolean Systembatteriessun

- Boolean SystemS1

- Boolean SystemS2

- Boolean SystemS3

- Boolean SystemS4

- Boolean SystemS5

- Boolean Yukarı yeniden gönderildi

- Boolean Videodimpyeniden gönderildi



## <a name="power-configurations"></a>Güç yapılandırma

Ad alanı: Root\ccm\ilkemachıneactualconfig

sınıf CCM_PowerConfig


- Dizisinde Powerconfigıd

- Int32 DurationInSec

- Dizisinde En sivri olmayan Kpowerplan

- Dizisinde Peakpowerplanname

- Dizisinde PeakPowerPlan

- Dizisinde PeakPowerPlanName

- Dizisinde PeakStartTimeHoursMin

- Dizisinde WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>Güç yönetimi Inleleia nedenleri

Ad alanı: root\CCM\powermanagementagent

sınıf CCM_PwrMgmtLastSuspendError


- Dizisinde İstek sahibi

- Dizisinde RequesterType

- Dizisinde RequestType

- Hem Işınızda

- Int32 AdditionalCode

- Dizisinde AdditionalInfo

- Dizisinde RequesterInfo

- Boolean Unknownisteyenin



## <a name="power-management-daily"></a>Güç yönetimi günlük

Ad alanı: root\CCM\powermanagementagent

sınıf CCM_PwrMgmtActualDay


- Hem Güncel

- Dizisinde TypeOfEvent

- (UInt32) hr0_1

- (UInt32) hr1_2

- (UInt32) hr10_11

- (UInt32) hr11_12

- (UInt32) hr12_13

- (UInt32) hr13_14

- (UInt32) hr14_15

- (UInt32) hr15_16

- (UInt32) hr16_17

- (UInt32) hr17_18

- (UInt32) hr18_19

- (UInt32) hr19_20

- (UInt32) hr2_3

- (UInt32) hr20_21

- (UInt32) hr21_22

- (UInt32) hr22_23

- (UInt32) hr23_0

- (UInt32) hr3_4

- (UInt32) hr4_5

- (UInt32) hr5_6

- (UInt32) hr6_7

- (UInt32) hr7_8

- (UInt32) hr8_9

- (UInt32) hr9_10

- (UInt32) minutesTotal



## <a name="power-client-opt-out-settings"></a>Güç Istemcisi geri çevirme ayarları

Ad alanı: root\ccm\ClientSDK

sınıf CCM_PowerManagementClientOptoutSetting


- Boolean AdminAllowOptout

- Boolean EffectiveClientOptOut

- Boolean IsClientOptOut



## <a name="power-management-monthly"></a>Güç yönetimi aylık

Ad alanı: root\CCM\powermanagementagent

sınıf CCM_PwrMgmtMonth


- Hem MonthStart

- (UInt32) Minutescomputeractıve

- (UInt32) minutesComputerOn

- (UInt32) Minutescomputerkapatması

- (UInt32) minutesComputerSleep

- (UInt32) minutesMonitorOn

- (UInt32) minutesTotal

- Dizisinde TypeOfEvent



## <a name="power-settings"></a>Güç ayarları

Ad alanı: Root\Cimv2\Sms

sınıf SMS_PowerSettings


- Dizisinde 'INI

- Dizisinde Acsettingındex

- Dizisinde ACValue

- Dizisinde Dcsettingındex

- Dizisinde DCValue

- Dizisinde Ada

- Dizisinde Unitbelirleyicisi



## <a name="print-jobs"></a>Yazdırma Işleri

Ad alanı: root\cimv2

sınıf Win32_PrintJob


- Dizisinde Ada

- Dizisinde Başlığını

- Dizisinde X

- Dizisinde Açıklaması

- Dizisinde Belgedeki

- Dizisinde Adı

- Hem ElapsedTime

- Dizisinde HostPrintQueue

- Hem InstallDate

- Int32 No

- Dizisinde JobStatus

- Dizisinde Miyor

- Dizisinde İnde

- Int32 Pagesyazdırıldı

- Dizisinde Parametrelere

- Dizisinde PrintProcessor

- Int32 Priority

- Int32 Boyutla

- Hem StartTime

- Dizisinde Durumlarına

- Int32 StatusMask

- Hem Zaman dilimlerini kabul eden

- Int32 TotalPages

- Hem UntilTime



## <a name="printer-configuration"></a>Yazıcı yapılandırması

Ad alanı: root\cimv2

sınıf Win32_PrinterConfiguration


- Dizisinde Ada

- Int32 BitsPerPel

- Dizisinde Başlığını

- Boolean Harman

- Int32 Renk

- Int32 Serisi

- Dizisinde Açıklaması

- Dizisinde DeviceName

- Int32 DisplayFlags

- Int32 DisplayFrequency

- Int32 DitherType

- Int32 DriverVersion

- Boolean Duplex

- Dizisinde Formadı

- Int32 HorizontalResolution

- Int32 Iminkatlanmış

- Int32 ICMMethod

- Int32 Logpixel

- Int32 Type

- Int32 Mesinden

- Int32 Kağıt uzunluğu

- Dizisinde PaperSize

- Int32 Kağıt genişliği

- Int32 PelsHeight

- Int32 Pelyüzdth

- Int32 PrintQuality

- Int32 Ölçek

- Dizisinde SettingID

- Int32 SpecificationVersion

- Int32 TTOption

- Int32 VerticalResolution

- Int32 XResolution

- Int32 Yılçözüm



## <a name="printer-device"></a>Yazıcı cihazı

Ad alanı: root\cimv2

sınıf Win32_Printer


- Dizisinde DeviceID

- Int32 Özelliklerine

- Int16 Sonrası

- Int32 AveragePagesPerMinute

- Int16 Yetenekler []

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Int32 DefaultPriority

- Dizisinde Açıklaması

- Int16 DetectedErrorState

- Dizisinde Adı

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int32 HorizontalResolution

- Hem InstallDate

- Int32 JobCountSinceLastReset

- Int16 LanguagesSupported []

- Int32 LastErrorCode

- Dizisinde Konumuna

- Dizisinde Ada

- Int16 PaperSizesSupported []

- Dizisinde Pnpdeviceıd

- Dizisinde PortName

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde PrinterPaperNames []

- Int32 PrinterState

- Int16 PrinterStatus

- Dizisinde PrintJobDataType

- Dizisinde PrintProcessor

- Dizisinde SeparatorFile

- Dizisinde ServerName

- Dizisinde Madı

- Boolean SpoolEnabled

- Hem StartTime

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset

- Hem UntilTime

- Int32 VerticalResolution



## <a name="process"></a>İşleme

Ad alanı: root\cimv2

sınıf Win32_Process


- Dizisinde Tutamaçlardan

- Dizisinde Başlığını

- Hem CreationDate

- Dizisinde Açıklaması

- Dizisinde ExecutablePath

- Int16 ExecutionState

- Int32 HandleCount

- Hem InstallDate

- Int64 KernelModeTime

- Int32 MaximumWorkingSetSize

- Int32 MinimumWorkingSetSize

- Dizisinde Ada

- Dizisinde OSName

- Int64 OtherOperationCount

- Int64 OtherTransferCount

- Int32 PageFaults

- Int32 Pageusage

- Int32 ParentProcessId

- Int32 Peakpageusage

- Int64 PeakVirtualSize

- Int32 PeakWorkingSetSize

- Int32 Priority

- Int64 PrivatePageCount

- Int32 Işlem

- Int32 QuotaNonPagedPoolUsage

- Int32 QuotaPagedPoolUsage

- Int32 QuotaPeakNonPagedPoolUsage

- Int32 QuotaPeakPagedPoolUsage

- Int64 ReadOperationCount

- Int64 ReadTransferCount

- Int32 Kimliği

- Dizisinde Durumlarına

- Hem Sonlandırmatarihi

- Int32 ThreadCount

- Int64 UserModeTime

- Int64 VirtualSize

- Dizisinde WindowsVersion

- Int64 WorkingSetSize

- Int64 WriteOperationCount

- Int64 WriteTransferCount



## <a name="processor"></a>İşlemci

Ad alanı: Root\Cimv2\Sms

sınıf SMS_Processor


- Dizisinde DeviceID

- Int16 Addresyüzdth

- Int16 Mimarisini

- Int16 Sonrası

- Int16 Brandıd

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde CPUHash

- Dizisinde CPUKey

- Int16 CpuStatus

- Int32 CurrentClockSpeed

- Int16 Currentvoltaj

- Int16 Veri genişliği

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int32 ExtClock

- Int16 Family

- Hem InstallDate

- Boolean Is64Bit

- Boolean Ihyperthreadyetenekli

- Boolean Ihyperthreadenabled

- Boolean IsMobile

- Boolean Itrustedexecutionyetenekli

- Boolean Ivtualizationyetenekli

- Int32 L2CacheSize

- Int32 L2CacheSpeed

- Int32 L3CacheSize

- Int32 L3CacheSpeed

- Int32 LastErrorCode

- Int16 Düzeyde

- Int16 LoadPercentage

- Dizisinde Üreticisini

- Int32 MaxClockSpeed

- Dizisinde Ada

- Int32 NormSpeed

- Int32 Numberofçekirdekler

- Int32 Numberoflogicaliþlemciler

- Dizisinde OtherFamilyDescription

- Boolean PartOfDomain

- Int32 PCache

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde ProcessorId

- Int16 ProcessorType

- Int16 Uncaya

- Dizisinde Rolü

- Dizisinde Sockettahsisi

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde Atma

- Dizisinde SystemName

- Dizisinde UniqueId

- Int16 Upgradeyöntemi

- Dizisinde Sürüm

- Int32 VoltageCaps

- Dizisinde Grub



## <a name="protected-volume-information"></a>Korumalı birim bilgileri

Ad alanı: Root\Cimv2\Sms

sınıf CCM_ProtectedVolumeInfo


- Dizisinde Ada

- Dizisinde Letter

- Int32 Koruma türünde olmalıdır



## <a name="protocol"></a>Protokol

Ad alanı: root\cimv2

sınıf Win32_NetworkProtocol


- Dizisinde Ada

- Dizisinde Başlığını

- Boolean ConnectionlessService

- Dizisinde Açıklaması

- Boolean Esdelivery 'i garanti edin

- Boolean Garanti eden sıralama

- Hem InstallDate

- Int32 MaximumAddressSize

- Int32 MaximumMessageSize

- Boolean Messageyönelimli

- Int32 En az Umaddresssize

- Boolean PseudoStreamOriented

- Dizisinde Durumlarına

- Boolean Destektsyayını

- Boolean SupportsConnectData

- Boolean SupportsDisconnectData

- Boolean SupportsEncryption

- Boolean SupportsExpeditedData

- Boolean Supportsparçalanma

- Boolean SupportsGracefulClosing

- Boolean Supportsgaranti Edbandwidth

- Boolean Supportsmultiatama

- Boolean SupportsQualityofService



## <a name="quick-fix-engineering"></a>Hızlı düzelme Mühendisliği

Ad alanı: root\cimv2

sınıf Win32_QuickFixEngineering


- Dizisinde HotfixID

- Dizisinde ServicePackInEffect

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Dizisinde FixComments

- Hem InstallDate

- Dizisinde Tarafından Instal

- Dizisinde Üzerinde ınstalınstalde

- Dizisinde Ada

- Dizisinde Durumlarına



## <a name="ccm-recently-used-applications"></a>CCM son kullanılan uygulamalar

Ad alanı: Root\Cimv2\Sms

sınıf CCM_RecentlyUsedApps


- Dizisinde ExplorerFileName

- Dizisinde FolderPath

- Dizisinde LastUserName

- Dizisinde AdditionalProductCodes

- Dizisinde Tadı

- Dizisinde Dosya açıklaması

- Dizisinde Dosya özellikleri karması

- Int32 İ

- Dizisinde FileVersion

- Hem LastUsedTime

- Int32 Başlatma sayısı

- (String) msiDisplayName

- (String) msiPublisher

- (Dize) msiVersion

- Dizisinde OriginalFileName

- Dizisinde ProductCode

- Int32 ProductLanguage

- Dizisinde ProductName

- Dizisinde ProductVersion

- Dizisinde SoftwarePropertiesHash



## <a name="registry"></a>Kayıt Defteri

Ad alanı: root\cimv2

sınıf Win32_Registry


- Dizisinde Ada

- Dizisinde Başlığını

- Int32 CurrentSize

- Dizisinde Açıklaması

- Hem InstallDate

- Int32 Boyut

- Int32 ProposedSize

- Dizisinde Durumlarına



## <a name="scsi-controller"></a>SCSI denetleyicisi

Ad alanı: root\cimv2

sınıf Win32_SCSIController


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Int32 Controllerzamanaşımları

- Dizisinde Açıklaması

- Dizisinde DeviceMap

- Dizisinde Adı

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde HardwareVersion

- Int32 İndeks

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int32 MaxDataWidth

- Int32 Maxnumberkontrollü

- Int64 MaxTransferRate

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 ProtectionManagement

- Int16 Protokolde destekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="serial-port-configuration"></a>Seri bağlantı noktası yapılandırması

Ad alanı: root\cimv2

sınıf Win32_SerialPortConfiguration


- Dizisinde Ada

- Boolean Abortreadwritehata

- Int32 Baud

- Boolean BinaryModeEnabled

- Int32 BitsPerByte

- Dizisinde Başlığını

- Boolean Continuexmıtonxoff

- Boolean CTSOutflowControl

- Dizisinde Açıklaması

- Boolean DiscardNULLBytes

- Boolean DSROutflowControl

- Boolean Dsrduyarlılık

- Dizisinde DTRFlowControlType

- Int32 EOFCharacter

- Int32 ErrorReplaceCharacter

- Boolean ErrorReplacementEnabled

- Int32 EventCharacter

- Boolean Imeşgul

- Dizisinde Eşlik

- Boolean ParityCheckEnabled

- Dizisinde RTSFlowControlType

- Dizisinde SettingID

- Dizisinde StopBits

- Int32 XOffCharacter

- Int32 XOffXMitThreshold

- Int32 XOnCharacter

- Int32 XOnXMitThreshold

- Int32 XOnXOffInFlowControl

- Int32 XOnXOffOutFlowControl



## <a name="serial-ports"></a>Seri bağlantı noktaları

Ad alanı: root\cimv2

sınıf Win32_SerialPort


- Dizisinde DeviceID

- Int16 Sonrası

- Boolean Ý

- Int16 Yetenekler []

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Int32 MaxBaudRate

- Int32 MaximumInputBufferSize

- Int32 MaximumOutputBufferSize

- Int32 Maxnumberkontrollü

- Dizisinde Ada

- Boolean Osautokeşfedilen

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Dizisinde ProviderType

- Boolean SettableBaudRate

- Boolean SettableDataBits

- Boolean SettableFlowControl

- Boolean Settableeşlik

- Boolean SettableParityCheck

- Boolean SettableRLSD

- Boolean SettableStopBits

- Dizisinde Durumlarına

- Int16 StatusInfo

- Boolean Supports16BitMode

- Boolean SupportsDTRDSR

- Boolean Supportselapsedzamanaşımları

- Boolean Supportsıntzamanaşımları

- Boolean SupportsParityCheck

- Boolean SupportsRLSD

- Boolean SupportsRTSCTS

- Boolean SupportsSpecialCharacters

- Boolean SupportsXOnXOff

- Boolean Supportsxonxsapmayı

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="server-feature"></a>Sunucu Özelliği

Ad alanı: root\cimv2

sınıf Win32_ServerFeature


- Int32 NUMARASıNı

- Dizisinde Ada

- Int32 ParentID



## <a name="services"></a>Hizmetler

Ad alanı: root\cimv2

sınıf Win32_Service


- Dizisinde Ada

- Boolean AcceptPause

- Boolean AcceptStop

- Dizisinde Başlığını

- Int32 Mak

- Dizisinde Açıklaması

- Boolean Desktopetkileşime

- Dizisinde DisplayName

- Dizisinde ErrorControl

- Int32 ExitCode

- Hem InstallDate

- Dizisinde PathName

- Int32 Işlem

- Int32 ServiceSpecificExitCode

- Dizisinde Türü

- Boolean Başlama

- Dizisinde StartMode

- Dizisinde StartName

- Dizisinde Durumunda

- Dizisinde Durumlarına

- Dizisinde SystemName

- Int32 TagId

- Int32 WaitHint



## <a name="shares"></a>Paylaşımlar

Ad alanı: root\cimv2

sınıf Win32_Share


- Dizisinde Ada

- Int32 AccessMask

- Boolean AllowMaximum

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Hem InstallDate

- Int32 MaximumAllowed

- Dizisinde Yolun

- Dizisinde Durumlarına

- Int32 Türüyle



## <a name="sw-licensing-product"></a>SW lisanslama ürünü

Ad alanı: root\cimv2

Class SoftwareLicensingProduct


- Dizisinde NUMARASıNı

- Dizisinde Uygulama

- Dizisinde Açıklaması

- Hem EvaluationEndDate

- Int32 GracePeriodRemaining

- Int32 Unlicensed

- Dizisinde MachineURL

- Dizisinde Ada

- Dizisinde Offlineınstald kimliği

- Dizisinde PartialProductKey

- Dizisinde ProcessorURL

- Dizisinde Productkeyıd

- Dizisinde ProductKeyURL 'Si

- Dizisinde UseLicenseURL



## <a name="sw-licensing-service"></a>SW Lisanslama hizmeti

Ad alanı: root\cimv2

Class SoftwareLicensingService


- Dizisinde Sürüm

- Dizisinde Clientmachineıd

- Int32 IsKeyManagementServiceMachine

- Int32 KeyManagementServiceCurrentCount

- Dizisinde KeyManagementServiceMachine

- Dizisinde Keymanagementserviceproductkeyıd

- Int32 PolicyCacheRefreshRequired

- Int32 RequiredClientCount

- Int32 Vlactivationınterval

- Int32 VLRenewalInterval



## <a name="software-shortcut"></a>Yazılım kısayolu

Ad alanı: Root\Cimv2\Sms

sınıf SMS_SoftwareShortcut


- Dizisinde ShortcutKey

- Dizisinde BinFileVersion

- Dizisinde BinProductVersion

- Dizisinde Açıklaması

- Dizisinde Dosya özellikleri karması

- Dizisinde FilePropertiesHashEx

- Int32 İ

- Dizisinde FileVersion

- Int32 Dildir

- Dizisinde ParentName

- Dizisinde Ürünüyle

- Dizisinde ProductCode

- Dizisinde ProductVersion

- Dizisinde 'In

- Dizisinde ShortcutName

- Int32 ShortcutType

- Dizisinde TargetExecutable



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

Ad alanı: Root\Cimv2\Sms

sınıf SMS_SoftwareTag


- Dizisinde TagCreatorRegid

- Dizisinde UniqueId

- Dizisinde DisplayVersion

- Boolean EntitlementRequired

- Dizisinde ProductName

- Dizisinde SoftwareCreator

- Dizisinde SoftwareCreatorRegid

- Dizisinde Softwarelisans verme

- Dizisinde SoftwareLicensorRegid

- Dizisinde TagCreator

- (SInt32) VersionAna

- (SInt32) VersionMinor



## <a name="sound-devices"></a>Ses cihazları

Ad alanı: root\cimv2

sınıf Win32_SoundDevice


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Int16 DMABufferSize

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int32 Mpu401 adresi

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde ProductName

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName



## <a name="system-account"></a>Sistem Hesabı

Ad alanı: root\cimv2

sınıf Win32_SystemAccount


- Dizisinde Alanını

- Dizisinde Ada

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Hem InstallDate

- Dizisinde SID

- UInt8 SIDType

- Dizisinde Durumlarına



## <a name="system-boot-data"></a>Sistem önyükleme verileri

Ad alanı: root\CCM

sınıf CCM_SystemBootData


- Int64 SystemStartTime

- Int32 BIO süresi

- Int16 BootDiskMediaType

- Int32 BootDuration

- Int32 EventLogStart

- Int32 GPDuration

- Dizisinde OSVersion

- Int32 UpdateDuration



## <a name="system-boot-summary"></a>Sistem önyükleme Özeti

Ad alanı: root\CCM

sınıf CCM_SystemBootSummary


- Int32 Averagebootflik

- Int32 Latestbiossüresi

- Int32 LatestBootDuration

- Int32 LatestCoreBootDuration

- Int32 LatestEventLogStart

- Int32 LatestGPDuration

- Int32 LatestUpdateDuration

- Int32 Maxbıo süresi

- Int32 MaxBootDuration

- Int32 MaxCoreBootDuration

- Int32 MaxEventLogStart

- Int32 MaxGPDuration

- Int32 MaxUpdateDuration

- Int32 MedianBiosDuration

- Int32 MedianBootDuration

- Int32 MedianCoreBootDuration

- Int32 MedianEventLogStart

- Int32 MedianGPDuration

- Int32 MedianUpdateDuration



## <a name="system-console-usage"></a>Sistem konsolu kullanımı

Ad alanı: Root\Cimv2\Sms

sınıf SMS_SystemConsoleUsage


- Hem SecurityLogStartDate

- Dizisinde TopConsoleUser

- Int32 TotalConsoleTime

- Int32 TotalConsoleUsers

- Int32 TotalSecurityLogTime



## <a name="system-console-user"></a>Sistem konsolu kullanıcısı

Ad alanı: Root\Cimv2\Sms

sınıf SMS_SystemConsoleUser


- Dizisinde SystemConsoleUser

- Hem LastConsoleUse

- Int32 Numberofconsoleoturumlarda

- Int32 TotalUserConsoleMinutes



## <a name="system-devices"></a>Sistem cihazları

Ad alanı: Root\Cimv2\Sms

sınıf CCM_SystemDevices


- Dizisinde Ada

- Dizisinde Compatibleıds []

- Dizisinde DeviceID

- Dizisinde HardwareIds []

- Boolean IsPnP



## <a name="system-drivers"></a>Sistem sürücüleri

Ad alanı: root\cimv2

sınıf Win32_SystemDriver


- Dizisinde Ada

- Boolean AcceptPause

- Boolean AcceptStop

- Dizisinde Başlığını

- Dizisinde Açıklaması

- Boolean Desktopetkileşime

- Dizisinde DisplayName

- Dizisinde ErrorControl

- Int32 ExitCode

- Hem InstallDate

- Dizisinde PathName

- Int32 ServiceSpecificExitCode

- Dizisinde Türü

- Boolean Başlama

- Dizisinde StartMode

- Dizisinde StartName

- Dizisinde Durumunda

- Dizisinde Durumlarına

- Dizisinde SystemName

- Int32 TagId



## <a name="system-enclosure"></a>Sistem Kutusu

Ad alanı: root\cimv2

sınıf Win32_SystemEnclosure


- Dizisinde Etiket

- Boolean AudibleAlarm

- Dizisinde BreachDescription

- Dizisinde CableManagementStrategy

- Dizisinde Başlığını

- Int16 ChassisTypes []

- (SInt16) Currentrequiredorüretilen

- Dizisinde Açıklaması

- Int16 HeatGeneration

- Boolean Hotswap

- Hem InstallDate

- Boolean Locksun

- Dizisinde Üreticisini

- Dizisinde Modelinizi

- Dizisinde Ada

- Int16 NumberOfPowerCords

- Dizisinde OtherIdentifyingInfo

- Dizisinde PartNumber

- Boolean PoweredOn

- Boolean Çıkarılabilir

- Boolean Değiştirebilen

- Int16 Securityihlal

- Int16 SecurityStatus

- Dizisinde Number

- Dizisinde ServiceDescriptions []

- Int16 Servicefelseno []

- Dizisinde ISTEYIN

- Dizisinde SMBIOSAssetTag

- Dizisinde Durumlarına

- Dizisinde TypeDescriptions []

- Dizisinde Sürüm

- Boolean VisibleAlarm



## <a name="tape-drive"></a>Bant sürücüsü

Ad alanı: root\cimv2

sınıf Win32_TapeDrive


- Dizisinde DeviceID

- Int16 Sonrası

- Int16 Yetenekler []

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Int32 Masıyla

- Dizisinde CompressionMethod

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Int64 DefaultBlockSize

- Dizisinde Açıklaması

- Int32 ECC

- Int32 EOTWarningZoneSize

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde Errormetodolojisi

- Int32 Kortureshigh

- Int32 Kortureslow

- Dizisinde NUMARASıNı

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int64 MaxBlockSize

- Int64 MaxMediaSize

- Int32 MaxPartitionCount

- Dizisinde Type

- Int64 MinBlockSize

- Dizisinde Ada

- Boolean Gereksiz korlama

- Int32 Desteklenmeyen numberofmedias

- Int32 Doldurmayı

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int32 Reportsetiþaretleri

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName



## <a name="time-zone"></a>Saat Dilimi

Ad alanı: root\cimv2

sınıf Win32_TimeZone


- Dizisinde StandardName

- (SInt32) Göre

- Dizisinde Başlığını

- (SInt32) Daylightsapması

- Int32 DaylightDay

- UInt8 DaylightDayOfWeek

- Int32 Dayaçık Thour

- Int32 Daylightmilisaniyelik

- Int32 DaylightMinute

- Int32 DaylightMonth

- Dizisinde DaylightName

- Int32 DaylightSecond

- Int32 Dayıntyear

- Dizisinde Açıklaması

- Dizisinde SettingID

- Int32 Standartsapma

- Int32 Standartgün

- UInt8 StandardDayOfWeek

- Int32 StandardHour

- Int32 Standardmilisaniyelik

- Int32 StandardMinute

- Int32 StandardMonth

- Int32 StandardSecond

- Int32 Standartyıl



## <a name="tpm"></a>TPM

Ad alanı: root\CIMv2\Security\MicrosoftTpm

sınıf Win32_Tpm


- Boolean IsActivated_InitialValue

- Boolean IsEnabled_InitialValue

- Boolean IsOwned_InitialValue

- Int32 Manufacturerkimliği

- Dizisinde Manufacturersürümü

- Dizisinde Manufacturerversionınfo

- Dizisinde PhysicalPresenceVersionInfo

- Dizisinde SpecVersion



## <a name="tpm-status"></a>TPM durumu

Ad alanı: Root\Cimv2\Sms

sınıf SMS_TPM


- Boolean Iısready

- Int32 Bilgi

- Boolean Iuygulanabilir



## <a name="ts-issued-license"></a>TS verilen lisans

Ad alanı: root\cimv2

sınıf Win32_TSIssuedLicense


- Int32 LicenseID

- Hem ExpirationDate

- Hem IssueDate

- Int32 Keypackıd

- Int32 Unlicensed

- (String) Shardwareıd

- (Dize) Sıssuedtocomputer

- (Dize) Sıssuedtouser



## <a name="ts-license-key-pack"></a>TS lisans anahtarı paketi

Ad alanı: root\cimv2

sınıf Win32_TSLicenseKeyPack


- Int32 Keypackıd

- Int32 Availablelisanslar

- Dizisinde Açıklaması

- Int32 Issuedlisansları

- Int32 KeyPackType

- Int32 ProductType

- Dizisinde ProductVersion

- Int32 Toplam lisans



## <a name="uninterruptible-power-supply"></a>Kesintisiz güç kaynağı

Ad alanı: root\cimv2

sınıf Win32_UninterruptiblePowerSupply


- Dizisinde DeviceID

- Int16 Activeınputvoltaj

- Int16 Sonrası

- Boolean Batter, yüklü

- Boolean Uzaktan kapatma

- Dizisinde Başlığını

- Dizisinde CommandFile

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int16 EstimatedChargeRemaining

- Int32 EstimatedRunTime

- Int32 FirstMessageDelay

- Hem InstallDate

- Boolean Isswitchingarz

- Int32 LastErrorCode

- Boolean Lowbatteryısignal

- Int32 MessageInterval

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Boolean PowerFailSignal

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int32 Range1InputFrequencyHigh

- Int32 Range1InputFrequencyLow

- Int32 Range1InputVoltageHigh

- Int32 Range1InputVoltageLow

- Int32 Range2InputFrequencyHigh

- Int32 Range2InputFrequencyLow

- Int32 Range2InputVoltageHigh

- Int32 Range2InputVoltageLow

- Int16 RemainingCapacityStatus

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Int32 TimeOnBackup

- Int32 TotalOutputPower

- Int16 Tür Ofrangeswıın

- Dizisinde UPSPort



## <a name="usb-controller"></a>USB denetleyicisi

Ad alanı: root\cimv2

sınıf Win32_USBController


- Dizisinde DeviceID

- Int16 Sonrası

- Dizisinde Başlığını

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde Açıklaması

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Hem InstallDate

- Int32 LastErrorCode

- Dizisinde Üreticisini

- Int32 Maxnumberkontrollü

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Hem TimeOfLastReset



## <a name="usb-device"></a>USB cihazı

Ad alanı: root\cimv2

sınıf Win32_USBDevice


- Dizisinde DeviceID

- Dizisinde Başlığını

- Dizisinde ClassGuid

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde CreationClassName

- Dizisinde Açıklaması

- Dizisinde Üreticisini

- Dizisinde Ada

- Dizisinde Pnpdeviceıd

- Dizisinde Hizmetle

- Dizisinde Durumlarına

- Dizisinde SystemCreationClassName

- Dizisinde SystemName



## <a name="usm-user-profile"></a>USA Kullanıcı profili

Ad alanı: root\cimv2

sınıf Win32_UserProfile


- Dizisinde SID

- UInt8 HealthStatus

- Dizisinde LastAttemptedProfileDownloadTime

- Dizisinde LastAttemptedProfileUploadTime

- Dizisinde LastBackgroundRegistryUploadTime

- Hem LastDownloadTime

- Hem LastUploadTime

- Hem LastUseTime

- Boolean Yüklenemedi

- Dizisinde LocalPath

- Int32 RefCount

- Boolean RoamingConfigured

- Dizisinde RoamingPath

- Boolean RoamingPreference

- Boolean Spec

- Int32 Durumlarına



## <a name="video-controller"></a>Video denetleyicisi

Ad alanı: root\cimv2

sınıf Win32_VideoController


- Dizisinde DeviceID

- Int16 Ivatorcapabilities []

- Dizisinde AdapterCompatibility

- Dizisinde AdapterDACType

- Int32 AdapterRAM

- Int16 Sonrası

- Dizisinde CapabilityDescriptions []

- Dizisinde Başlığını

- Int32 ColorTableEntries

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Int32 CurrentBitsPerPixel

- Int32 CurrentHorizontalResolution

- Int64 CurrentNumberOfColors

- Int32 CurrentNumberOfColumns

- Int32 CurrentNumberOfRows

- Int32 CurrentRefreshRate

- Int16 CurrentScanMode

- Int32 CurrentVerticalResolution

- Dizisinde Açıklaması

- Int32 Devicespecifickalemleri

- Int32 DitherType

- Hem DriverDate

- Dizisinde DriverVersion

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Int32 Iminkatlanmış

- Int32 ICMMethod

- Dizisinde InfFilename

- Dizisinde InfSection

- Hem InstallDate

- Dizisinde InstalledDisplayDrivers

- Int32 LastErrorCode

- Int32 Maxmemorydestekleniyor

- Int32 Maxnumberkontrollü

- Int32 MaxRefreshRate

- Int32 MinRefreshRate

- Boolean Tek renkli

- Dizisinde Ada

- Int16 Numberofcolordüzlemi

- Int32 NumberOfVideoPages

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Int16 Protokolde destekleniyor

- Int32 ReservedSystemPaletteEntries

- Int32 SpecificationVersion

- Dizisinde Durumlarına

- Int16 StatusInfo

- Dizisinde SystemName

- Int32 SystemPaletteEntries

- Hem TimeOfLastReset

- Int16 VideoArchitecture

- Int16 VideoMemoryType

- Int16 VideoMode

- Dizisinde VideoModeDescription

- Dizisinde VideoProcessor



## <a name="virtual-application-packages"></a>Sanal uygulama paketleri

Ad alanı: root\Microsoft\appvirt\client

sınıf paketi


- Dizisinde PackageGUID

- Int64 CachedLaunchSize

- Int16 CachedPercentage

- Int64 CachedSize

- Int64 Başlatma boyutu

- Dizisinde Ada

- Dizisinde SftPath

- Int64 Toplam Boyut

- Dizisinde Sürüm

- Dizisinde VersionGUID



## <a name="virtual-applications"></a>Sanal Uygulamalar

Ad alanı: root\Microsoft\appvirt\client

sınıf uygulaması


- Dizisinde Ada

- Dizisinde Sürüm

- Dizisinde CachedOsdPath

- Int32 GlobalRunningCount

- Hem LastLaunchOnSystem

- Boolean Yükleniyor

- Dizisinde OriginalOsdPath

- Dizisinde PackageGUID



## <a name="virtual-machine-64"></a>Sanal makine (64)

Ad alanı: root\cimv2

sınıf Win32Reg_SMSGuestVirtualMachine64


- Dizisinde InstanceKey

- Dizisinde PhysicalHostName

- Dizisinde PhysicalHostNameFullyQualified



## <a name="virtual-machine"></a>Sanal Makine

Ad alanı: root\cimv2

sınıf Win32Reg_SMSGuestVirtualMachine


- Dizisinde InstanceKey

- Dizisinde PhysicalHostName

- Dizisinde PhysicalHostNameFullyQualified



## <a name="virtual-machine-details"></a>Sanal makine ayrıntıları

Ad alanı: root\vm\VirtualServer

sınıf VirtualMachine


- Dizisinde Ada

- Int32 Cpukullanımı

- Int64 DiskBytesRead

- Int64 DiskBytesWritten

- Int64 DiskSpaceUsed

- Int64 HeartbeatCount

- Int32 HeartbeatInterval

- Int32 HeartbeatPercentage

- Int32 HeartbeatRate

- Int64 NetworkBytesReceived

- Int64 NetworkBytesSent

- Int64 Physicalmemoryalbulunan

- Int32 Hizmet



## <a name="volume"></a>Birim

Ad alanı: root\cimv2

sınıf Win32_Volume


- Dizisinde DeviceID

- Int16 Erişmesini

- Boolean Otomatik bağlama

- Int16 Sonrası

- Int64 Kullanılanla

- Int64 Kü

- Dizisinde Başlığını

- Boolean Dınız

- Int32 ConfigManagerErrorCode

- Boolean ConfigManagerUserConfig

- Dizisinde CreationClassName

- Dizisinde Açıklaması

- Boolean DirtyBitSet

- Dizisinde Letter

- Int32 Drvetype

- Boolean Errortemizlendi

- Dizisinde ErrorDescription

- Dizisinde Errormetodolojisi

- Dizisinde Biçimlendiri

- Int64 FreeSpace

- Boolean Indexingenabled

- Hem InstallDate

- Dizisinde Etiketin

- Int32 LastErrorCode

- Int32 Maximumdosyaadıuzunluğu

- Dizisinde Ada

- Int64 NumberOfBlocks

- Dizisinde Pnpdeviceıd

- Int16 PowerManagementCapabilities []

- Boolean Powermanagementdestekleniyor

- Dizisinde Amaçla

- Boolean QuotasEnabled

- Boolean Quotascomplete

- Boolean Quotasyeniden oluşturma

- Int32 Number

- Dizisinde Durumlarına

- Int16 StatusInfo

- Boolean SupportsDiskQuotas

- Boolean SupportsFileBasedCompression

- Dizisinde SystemCreationClassName

- Dizisinde SystemName



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

Ad alanı: root\ccm\cımodeller

sınıf CCM_WebAppInstallInfo


- Dizisinde Appdeliverytypeıd

- Int32 AppDtRevision

- Dizisinde TargetURL

- Dizisinde Kullanıcı SID 'si

- Dizisinde URL dosya adı

- Dizisinde URL yolu



## <a name="sms_windows8application"></a>SMS_Windows8Application

Ad alanı: Root\Cimv2\Sms

sınıf SMS_Windows8Application


- Dizisinde FullName

- Dizisinde ApplicationName

- Dizisinde Mimarisini

- Boolean ConfigMgrManaged

- Dizisinde DependencyApplicationNames

- Dizisinde FamilyName

- Dizisinde Instalınstalo konumu

- Boolean IsFramework

- Dizisinde 'In

- Dizisinde PublisherId

- Dizisinde Sürüm



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

Ad alanı: Root\Cimv2\Sms

sınıf SMS_Windows8ApplicationUserInfo


- Dizisinde FullName

- Dizisinde Usersecurityıd

- Dizisinde InstallState

- Dizisinde UserAccountName



## <a name="windows-update"></a>Windows Update

Ad alanı: root\cimv2

sınıf Win32Reg_SMSWindowsUpdate


- Dizisinde InstanceKey

- Int32 AUOptions

- Int32 Nootomatik güncelleştirme

- Int32 UseWUServer



## <a name="windows-update-agent-version"></a>Windows Update Aracısı sürümü

Ad alanı: Root\Cimv2\Sms

sınıf Win32_WindowsUpdateAgentVersion


- Dizisinde Sürüm



## <a name="write-filter-state"></a>Filtre durumunu yaz

Ad alanı: Root\Cimv2\Sms

sınıf CCM_WriteFilterState


- Boolean WriteFilterEnabled
