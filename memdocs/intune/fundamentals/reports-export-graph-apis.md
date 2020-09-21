---
title: Intune raporlarını dışarı aktarmak için Graph API 'Lerini kullanma | Microsoft Docs
description: Graph API 'Leri kullanarak Intune raporlarını dışa aktarma hakkında bilgi edinin.
keywords: ''
ms.author: erikre
author: Erikre
manager: dougeby
ms.date: 09/15/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6739a24f105ac6b8c5c69f193ae51c55f449d383
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90816628"
---
# <a name="export-intune-reports-using-graph-apis"></a>Grafik API 'Lerini kullanarak Intune raporlarını dışarı aktarma

Intune raporlama altyapısına geçirilmiş tüm raporlar, tek bir üst düzey dışarı aktarma API 'sinden dışarı aktarmak için kullanılabilir. HTTP çağrısını yapmak için Microsoft Graph API 'sini kullanmanız gerekir. Microsoft Graph, Microsoft Bulut hizmet kaynaklarına erişmenize olanak tanıyan bir Restsize Web API 'sidir. 

> [!NOTE]
> Microsoft Graph etkileşimde bulunmak için araçlar da dahil olmak üzere REST API çağrıları yapma hakkında bilgi için bkz. [MICROSOFT Graph API 'Sini kullanma](https://docs.microsoft.com/graph/use-the-api).

Microsoft Uç Nokta Yöneticisi, raporları aşağıdaki Microsoft Graph API uç noktasına göre dışarı aktarır:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```
## <a name="example-devices-report-request-and-response"></a>Örnek cihazlar istek ve yanıtı raporlar

İsteği yaparken, `reportName` dışarı aktarmak istediğiniz rapora göre istek gövdesinin bir parçası olarak bir parametre sağlamalısınız. Aşağıda, **cihazlar** raporu için bir dışarı aktarma isteğine örnek verilmiştir. İsteğiniz üzerinde HTTP POST yöntemini kullanmanız gerekir. POST yöntemi, yeni bir kaynak oluşturmak veya bir eylem gerçekleştirmek için kullanılır.

### <a name="request-example"></a>İstek örneği

Aşağıdaki istek, Microsoft Graph istekte kullanılan HTTP yöntemini içerir.

```http
{ 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "localization": "true", 
    "ColumnName": "ui" 
} 
```
### <a name="response-example"></a>Yanıt örneği

Yukarıdaki POST isteğine bağlı olarak Graf bir yanıt iletisi döndürür. Yanıt iletisi, istediğiniz veya işlemin sonucu olan veri.

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "notStarted", 
    "url": null, 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "0001-01-01T00:00:00Z" 
} 
```
Daha sonra, `id` BIR Get isteğiyle dışarı aktarmanın durumunu sorgulamak için alanını kullanabilirsiniz: 

Örnek: ```https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('Devices_05e62361-783b-4cec-b635-0aed0ecf14a3') ```

Bir öznitelik ile yanıt alınana kadar bu URL 'YI çağırmaya devam etmeniz gerekir `status: completed` . Aşağıdaki örneğe benzer şekilde görünür:

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "completed", 
    "url": "https://amsua0702repexpstorage.blob.core.windows.net/cec055a4-97f0-4889-b790-dc7ad0d12c29/Devices_05e62361-783b-4cec-b635-0aed0ecf14a3.zip?sv=2019-02-02&sr=b&sig=%2BP%2B4gGiZf0YzlQRuAV5Ji9Beorg4nnOtP%2F7bbFGH7GY%3D&skoid=1db6df02-4c8b-4cb3-8394-7ac2390642f8&sktid=72f988bf-86f1-41af-91ab-2d7cd011db47&skt=2020-08-19T03%3A48%3A32Z&ske=2020-08-19T09%3A44%3A23Z&sks=b&skv=2019-02-02&se=2020-08-19T09%3A44%3A23Z&sp=r", 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "2020-08-19T09:44:23.8540289Z" 
} 
```
Bundan sonra, bundan sonra sıkıştırılan CSV 'yi alandan doğrudan indirebilirsiniz `url` .  

## <a name="report-parameters"></a>Rapor parametreleri

Dışarı aktarma isteğini tanımlamak için, istek gövdesinden gönderebileceğiniz üç ana parametre vardır: 

- `reportName`İstenir. Bu parametre, belirtmek istediğiniz raporun adıdır.  
- `filter`: Çoğu rapor için gerekli değildir. 
- `select`: Gerekli değil. Bir `select` değer belirtmezseniz, çoğu rapor veri kümesinin tamamı için varsayılan bir sütun kümesi alırsınız. 

## <a name="available-reports"></a>Kullanılabilir raporlar

Aşağıdaki tablo, parametresi için olası değerleri içerir `reportName` . Bunlar, dışarı aktarma için şu anda kullanılabilir raporlardır.

|         ReportName (dışarı aktarma parametresi)  |            Microsoft Endpoint Manager 'da ilişkili rapor        |
|-|-|
|         Deviceuyumluluğu  |            Cihaz uyumluluğu kuruluş        |
|         Devicenonuyumluluğu  |            Uyumlu olmayan cihazlar        |
|         Cihazlar  |            Tüm cihazlar listesi        |
|         DetectedAppsAggregate  |            Algılanan uygulamalar raporu        |
|         FeatureUpdatePolicyFailuresAggregate  |            **Devices**  >  **Monitor**  >  **Özellik güncelleştirmeleri için** cihazlar izleme hatası altında       |
|         Devicefailuırebyfeatureupdatepolicy  |            **Cihaz**altında  >  **Monitor**  >  **özellik güncelleştirmeleri için**hata izleme hatası  >  *' ye tıklayın* .        |
|         Featureupdatedevicemlak  |            **Raporlar**  >  **penceresi güncelleştirme**  >  **raporları**  >  **Windows Özellik Güncelleştirme raporu** altında         |
|         Unhealthyısavunma Deragents  |            **Endpoint Security**  >  **Antivirus**altında  >  **win10 sağlıklı uç noktalar**        |
|         Savunma Deragents  |            **Raporlar**altında  >  **microsoftdefender**  >  **Reports**  >  **Agent durumu**        |
|         ActiveMalware  |            **Endpoint Security**  >  **Antivirus**  >  **win10 algılanan kötü amaçlı yazılım**        |
|         Kötü Amaçlı Yazılımlar  |            **Raporlar**altında,  >  **microsoftdefender**  >  **raporları**  >  **algılanan kötü amaçlı yazılım**        |

Listelenen raporların her biri aşağıda açıklanmıştır.

### <a name="devicecompliance-report"></a>Deviceuyumluluk raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `DeviceCompliance` :

| Kullanılabilir özellikler |
|-|
| DeviceId |
| Intunedeviceıd |
| Aaddeviceıd |
| DeviceName |
| DeviceType |
| OSDescription |
| OSVersion |
| OwnerType |
| LastContact |
| InGracePeriodUntil |
| IMEI |
| SerialNumber |
| ManagementAgents |
| Primaryuser bilgilerini |
| UserId |
| UPN |
| UserEmail |
| UserName |
| DeviceHealthThreatLevel |
| RetireAfterDatetime |
| Partnerdeviceıd |
| Karmaşıks, |
| İşletim Sistemi |

`DeviceCompliance`Raporun çıkışını aşağıdaki sütunlara göre filtrelemeyi seçebilirsiniz:
- `ComplianceState`
- `OS` 
- `OwnerType`
- `DeviceType` 

### <a name="devicenoncompliance-report"></a>Devicenonuyumluluk raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `DeviceNonCompliance` :

|     Kullanılabilir özellikler  |
|-|
|     DeviceId  |
|            Intunedeviceıd   |
| Aaddeviceıd   |
| DeviceName   |
| DeviceType   |
| OSDescription   |
|            OSVersion   |
| OwnerType   |
| LastContact   |
| InGracePeriodUntil   |
| IMEI   |
|            SerialNumber   |
| ManagementAgents   |
| Primaryuser bilgilerini   |
| UserId     |
| UPN   |
|            UserEmail   |
| UserName   |
| DeviceHealthThreatLevel   |
| RetireAfterDatetime   |
| Partnerdeviceıd   |
|            Karmaşıks,         |
| İşletim Sistemi |

`DeviceNonCompliance`Raporun çıkışını aşağıdaki sütunlara göre filtrelemeyi seçebilirsiniz:
- `OS` 
- `OwnerType`
- `DeviceType` 
- `UserId`
- `ComplianceState`

### <a name="devices-report"></a>Cihazlar raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `Devices` :

|     Kullanılabilir özellikler |
|-|
|     DeviceId  |
| DeviceName  |
| DeviceType  |
| ClientRegistrationStatus  |
|            OwnerType  |
| CreatedDate  |
| LastContact  |
| ManagementAgents  |
| Yönetim durumu  |
|            ReferenceId  |
| CategoryId  |
| KayıtTürü  |
| CertExpirationDate  |
| Mdmstatus anahtarı  |
|            OSVersion  |
| GraphDeviceIsManaged  |
| EasID  |
| SerialNumber  |
| EnrolledByUser  |
|            Üretici  |
| Modelleme  |
| OSDescription  |
| IsManaged  |
| EasActivationStatus  |
|            IMEI  |
| Easlastsyncbaşarılı UTC  |
| EasStateReason  |
| EasAccessState  |
| EncryptionStatus  |
|            Supervısedstatus  |
| PhoneNumberE164Format  |
| InGracePeriodUntil  |
| AndroidPatchLevel  |
| WifiMacAddress  |
|            Sccmcomanagementfeatemi  |
| MEID  |
| SubscriberCarrierNetwork  |
| StorageTotal  |
| StorageFree  |
|            Managedaygıtadı  |
| LastLoggedOnUserUPN  |
| MDMWinsOverGPStartTime  |
| StagedDeviceType  |
| UserApprovedEnrollment  |
|            ExtendedProperties  |
| EntitySource  |
| Primaryuser bilgilerini  |
| KategoriAdı  |
| UserId  |
|            UPN  |
| UserEmail  |
| UserName  |
| RetireAfterDatetime  |
| Partnerdeviceıd  |
|            HasUnlockToken  |
| Karmaşık bir durum  |
| ManagedBy  |
| Sahiplik  |
| DeviceState  |
|            DeviceRegistrationState  |
| Supervısedstatusstring  |
| EncryptionStatusString  |
| İşletim Sistemi  |
| SkuFamily  |
|            JoinType  |
| PhoneNumber  |
| JailBroken  |
| EasActivationStatusString        |

`DeviceNonCompliance`Raporun çıkışını aşağıdaki sütunlara göre filtrelemeyi seçebilirsiniz:
- `OwnerType`
- `DeviceType` 
- `ManagementAgents`
- `CategoryName` 
- `ManagementState` 
- `CompliantState` 
- `JailBroken` 
- `LastContact` 
- `CreatedDate` 
- `EnrollmentType` 

### <a name="detectedappsaggregate-report"></a>DetectedAppsAggregate raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `DetectedAppsAggregate` :

|     Kullanılabilir özellikler  |
|-|
|     ApplicationKey  |
| ApplicationName  |
|            ApplicationVersion  |
| DeviceCount  |
| BundleSize  |

`DetectedAppsAggregate`Raporun çıkışını aşağıdaki sütuna göre filtrelemeye seçebilirsiniz:
- `ApplicationName`

### <a name="featureupdatepolicyfailuresaggregate-report"></a>FeatureUpdatePolicyFailuresAggregate raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `FeatureUpdatePolicyFailuresAggregate` :

| Kullanılabilir özellikler  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     NumberOfDevicesWithErrors     |

Bu raporu filtreleyemezsiniz.

### <a name="devicefailuresbyfeatureupdatepolicy-report"></a>DeviceFailuresByFeatureUpdatePolicy raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `DeviceFailuresByFeatureUpdatePolicy` :

| Kullanılabilir özellikler  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     DeviceId  |
|     Aaddeviceıd  |
|     AlertId  |
|     EventDateTimeUTC  |
|     LastUpdatedAlertStatusDateTimeUTC  |
|     AlertType  |
|     AlertStatus  |
|     AlertClassification  |
|     WindowsUpdateVersion  |
|     Yapı  |
|     AlertMessage  |
|     AlertMessageDescription  |
|     AlertMessageData  |
|     Win32ErrorCode  |
|     RecommendedAction  |
|     ExtendedRecommendedAction  |
|     StartDateTimeUTC  |
|     ResolvedDateTimeUTC  |
|     DeviceName  |
|     UPN     |

`DeviceFailuresByFeatureUpdatePolicy`Raporun çıkışını aşağıdaki sütunlara göre filtrelemeyi seçebilirsiniz:
- `PolicyId`**(Gerekli)** 
- `AlertMessage` 
- `RecommendedAction` 
- `WindowsUpdateVersion` 

### <a name="featureupdatedevicestate-report"></a>Featureupdatedevicemlak raporu

Aşağıdaki tablo, raporu çağırırken olası çıktıyı içerir `FeatureUpdateDeviceState` :

| Kullanılabilir özellikler  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     DeviceId  |
|     Aaddeviceıd  |
|     Partnerpolicyıd  |
|     EventDateTimeUTC  |
|     Lastbaşarıyla Fuldeviceupdatestatus  |
|     Lastbaşarılı Fuldeviceupdatealt durumu  |
|     Lastbaşarılı Fuldeviceupdatekara Seventdatetimeutc  |
|     CurrentDeviceUpdateStatus  |
|     Currentdeviceupdatealt durumu  |
|     Currentdeviceupdatekara Seventdatetimeutc  |
|     LatestAlertMessage  |
|     LatestAlertMessageDescription  |
|     LatestAlertRecommendedAction  |
|     LatestAlertExtendedRecommendedAction  |
|     UpdateCategory  |
|     WindowsUpdateVersion  |
|     LastWUScanTimeUTC  |
|     Yapı  |
|     DeviceName  |
|     OwnerType  |
|     UPN  |
|     AggregateState     |

`FeatureUpdateDeviceState`Raporun çıkışını aşağıdaki sütunlara göre filtrelemeyi seçebilirsiniz:
- `PolicyId`**(Gerekli)**
- `AggregateState`
- `LatestAlertMessage`
- `OwnerType`

### <a name="unhealthydefenderagents-and-defenderagents-reports"></a>Unhealthyısavunma Deragents ve savunma Deragents raporları

`UnhealthyDefenderAgents`Ve `DefenderAgents` raporları aynı özellik ve filtre kümesine sahip olan iki ayrı raporlardır. Aşağıdaki tablo, veya raporlarını çağırırken olası çıktıyı içerir `UnhealthyDefenderAgents` `DefenderAgents` :

| Kullanılabilir sütunlar  |
|-|
|     DeviceId  |
|     DeviceName  |
|     DeviceState  |
|     PendingFullScan  |
|     PendingReboot  |
|     PendingManualSteps  |
|     PendingOfflineScan  |
|     CriticalHandle hatası  |
|     MalwareProtectionEnabled  |
|     RealTimeProtectionEnabled  |
|     Networkınspectionsystemenabled  |
|     Signatureupdatevadesi geçmiş  |
|     Hızlı Tarama süresi doldu  |
|     FULLSCAN, süresi doldu  |
|     RebootRequired  |
|     FullScanRequired  |
|     EngineVersion  |
|     SignatureVersion  |
|     AntiMalwareVersion  |
|     LastQuickScanDateTime  |
|     LastFullScanDateTime  |
|     LastQuickScanSignatureVersion  |
|     LastFullScanSignatureVersion  |
|     LastReportedDateTime  |
|     UPN  |
|     UserEmail  |
|     UserName     |

`UnhealthyDefenderAgents` `DefenderAgents` Aşağıdaki sütunlara göre ve rapor çıkışını filtrelemeye seçebilirsiniz:
- `DeviceState` 
- `SignatureUpdateOverdue` 
- `MalwareProtectionEnabled`
- `RealTimeProtectionEnabled` 
- `NetworkInspectionSystemEnabled`

### <a name="activemalware-and-malware-reports"></a>ActiveMalware ve kötü amaçlı yazılım raporları

`ActiveMalware`Ve `Malware` raporları aynı özellik ve filtre kümesine sahip olan iki ayrı raporlardır. Aşağıdaki tablo, veya raporlarını çağırırken olası çıktıyı içerir `ActiveMalware` `Malware` :

| Kullanılabilir sütunlar  |
|-|
|     DeviceId  |
|     DeviceName  |
|     Malwareıd  |
|     MalwareName  |
|     Additionalınformationurl 'Si  |
|     Önem Derecesi  |
|     MalwareCategory  |
|     ExecutionState  |
|     Durum  |
|     InitialDetectionDateTime  |
|     LastStateChangeDateTime  |
|     DetectionCount  |
|     UPN  |
|     UserEmail  |
|     UserName     |

`ActiveMalware` `Malware` Aşağıdaki sütunlara göre ve rapor çıkışını filtrelemeye seçebilirsiniz:
- `Severity` 
- `ExecutionState` 
- `State` 

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Graph belgeleri](https://docs.microsoft.com/graph/)
- [Intune raporları](https://docs.microsoft.com/mem/intune/fundamentals/reports)