---
title: Azure AD kimlik doğrulaması iş akışı
titleSuffix: Configuration Manager
description: Azure Active Directory kimlik doğrulamasıyla bir Windows 10 cihazında istemci yükleme işleminin Configuration Manager ayrıntıları
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714125"
---
# <a name="azure-ad-authentication-workflow"></a>Azure AD kimlik doğrulaması iş akışı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Azure Active Directory (Azure AD) ile birleştirilen bir Windows 10 cihazında Configuration Manager istemci yükleme işlemine yönelik teknik bir başvurudur. Cihaz kimlik doğrulaması ve istemci yüklemesi için iş akışı sürecini ayrıntılarından  
 

## <a name="azure-ad-token-request-workflow"></a>Azure AD belirteç isteği iş akışı

![Azure AD CCMSetup iş akışı diyagramı](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Azure AD belirteç isteği

Windows 10 Azure AD etki alanına katılmış istemci, belirteç istemek için Azure AD parametrelerini kullanır. **CCMSetup. log dosyasına**aşağıdaki girişler kaydedilir:

- Azure AD cihaz belirteci iste:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Bir cihaz belirteci alamazsanız bir Azure AD Kullanıcı belirteci ister:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> İstemci, Azure AD 'ye katıldığında bir Workplace JOIN (WPJ) sertifikası almalıdır. Bir çalışma alanına katılma sertifikası bulunamazsa istemci, güvenlik belirteci hizmeti iletişim kanalını (CCM_STS) kullanarak isteği oluşturmaya çalışır. Bu davranış, istemcinin isteğe bir Azure AD belirteci ekleyemediği için oluşur. İstemci Azure AD 'ye düzgün şekilde katılmamışsa, bu sertifikaya genellikle sahip değildir.
>
> Ayrıca, belirteç geçerli değilse, bulut yönetimi ağ geçidi (CMG) isteği iç site rollerine iletmez. Kiracı, Configuration Manager ' de bir bulut yönetimi hizmeti olarak kaydedilmemişse belirteç geçersiz olabilir.


### <a name="2-configuration-manager-client-token-request"></a>2. istemci belirteci isteği Configuration Manager

İstemcide bir Azure AD belirteci varsa, bir Configuration Manager istemci (CCM) belirteci ister.

Aşağıdaki girişler CMG sanal makinesinin **CCMSetup. log dosyasına** kaydedilir:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2,1 CMG isteği alıyor

Aşağıdaki girişler **IIS. log günlüğüne**kaydedilir:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2,2 CMG isteği CMG bağlantı noktasına iletir

Aşağıdaki girişler **Cmgservice. log dosyasına**kaydedilir:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2,3 CMG bağlantı noktası CMG istemci isteğini Yönetim noktası istemci isteğine dönüştürür

Aşağıdaki girişler **SMS_CLOUD_PROXYCONNECTOR. log günlüğüne**kaydedilir:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2,4 yönetim noktası site veritabanındaki kullanıcı belirtecini doğrular

Aşağıdaki girişler **CCM_STS. log günlüğüne**kaydedilir:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>İçerik konumu isteği

İstemci CCM belirtecine bir yanıt aldıktan sonra, bu, CMG aracılığıyla site bilgilerini ve içerik konumunu istemek için önbelleğe alır ve kullanır. **CCMSetup. log dosyasına**aşağıdaki girişler kaydedilir:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>İstemci yüklemesi

Cihaz, istemci içeriğini indirir ve yüklemeyi başlatır.

### <a name="communication-validation"></a>İletişim doğrulama

- CMG, CMG, CMG bağlantı noktası ve HTTP (S) ve yönetim noktası veritabanı isteği ile istemci belirtecini doğrular.
- İstemci CMG hizmet sertifikasını veya yönetim sertifikasını doğrular
- CMG hizmet sertifikası için PKI: Istemci yerel depoda CMG sertifikasının kök sertifika yetkilisini (CA) gerektirir
- Üçüncü taraf CMG hizmet sertifikası: Istemciler, kök CA 'sını Internet 'te yayımlanan bir sertifikayı otomatik olarak doğrular


## <a name="common-issues"></a>Genel sorunlar

- Kök CA yok
- CRL denetimi etkin: Internet 'te CRL yayımlama veya komut satırındaki **/NoCRLCheck** seçeneğini kullanma
- WPJ sertifikası bulunamadı: istemci Azure AD 'ye kayıtlı, ancak Azure AD 'ye katılmadı

/NoCRLCheck kullanılması yalnızca CCMSetup önyüklemesi için iyidir. İstemcilerin tam olarak işlevsel olması için CRL 'yi İnternet üzerinde yayımlamanız gerekir. Geçici bir çözüm olarak, sitenin istemci iletişim yapılandırmasındaki CRL denetimini devre dışı bırakabilirsiniz. Aksi takdirde, güvenlik ayarları konum hizmeti tarafından yenilendikten sonra istemciler sunucusuyla iletişim kurmasını durdurur.


## <a name="client-registration"></a>İstemci kaydı

![Azure AD kayıt iş akışı diyagramı](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Configuration Manager istemci isteği kaydı

Aşağıdaki girişler **Clienentidmanagerstartup. log**dosyasında günlüğe kaydedilir:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Configuration Manager Azure AD belirtecini istemcisini kaydetmek için isteyin

Aşağıdaki girişler **Adaloperationprovider. log dosyasına**kaydedilir:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2,1 Configuration Manager istemci kayıtlı  

Aşağıdaki girişler **Clienentidmanagerstartup. log**dosyasında günlüğe kaydedilir:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> İstemci kaydı sırasında, sertifika doğrulaması her zaman çalışır. Bu işlem, istemciyi kaydetmek için Azure AD kimlik doğrulama yöntemini kullanıyor olsanız bile gerçekleşir.


### <a name="3-configuration-manager-client-token-request"></a>3. Configuration Manager istemci belirteci isteği

Site istemciyi kaydettiğinde istemci bir CCM belirteci ister. CCM belirteci, yerel sistem hesabı (S-1-5-18) için şifrelenir ve sekiz saat için önbelleğe alınır. Sekiz saat sonra, belirtecin süresi dolar ve istemci, belirteç yenilemesi ister.

Aşağıdaki girişler **Clienentidmanagerstartup. log**dosyasında günlüğe kaydedilir:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3,1 CMG isteği alıyor

Aşağıdaki girişler **IIS. log günlüğüne**kaydedilir:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3,2 CMG isteği CMG bağlantı noktasına iletir

Aşağıdaki girişler **Cmgservice. log dosyasına**kaydedilir:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3,3 CMG bağlantı noktası CMG istemci isteğini Yönetim noktası istemci isteğine dönüştürür

Aşağıdaki girişler **SMS_CLOUD_PROXYCONNECTOR. log günlüğüne**kaydedilir:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3,4 yönetim noktası site veritabanındaki kullanıcı belirtecini doğrular

Aşağıdaki girişler **CCM_STS. log günlüğüne**kaydedilir:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
