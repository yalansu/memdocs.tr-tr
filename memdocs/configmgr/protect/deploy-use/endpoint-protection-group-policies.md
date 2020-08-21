---
title: Grup İlkelerini kullanarak Endpoint Protection yönetme
titleSuffix: Configuration Manager
description: Endpoint Protection grup Ilkelerini kullanarak yönetmeyi öğrenin.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d028dc6149ae1fee2d61634b96ccf450fc8f4b24
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700608"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>Önceki Windows sürümlerinde Endpoint Protection yönetmek için grup ilkesi ayarlarını kullanın

**Uygulama hedefi:**

- [Microsoft Defender Gelişmiş tehdit koruması (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center aşağıdaki alt düzey cihazlarda Endpoint Protection:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

Endpoint Protection, ancak Configuration Manager hiyerarşinizin dışında olan, bazı alt düzey veya eski Windows cihazlarınız olabilir. Örneğin, sivilleştirilmiş bir bölgedeki veya birleşmeler ve alımlar aracılığıyla tümleştirilmiş cihazlarda bulunan cihazlar. 

Bu tür cihazlarda Endpoint Protection aşağıdaki şekilde açıklanan grup ilkesi ayarlarını kullanarak yönetebilirsiniz:

- [Endpoint Protection ilkesi tanımlarını Kopyala](#copy-endpoint-protection-policy-definitions)
- Endpoint Protection ilkesi tanımlarını aşağıdaki konumlardan birine yükleyin:
    - [Bir etki alanı denetleyicisindeki merkezi mağaza (önerilir)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Yerel cihaz](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Windows 10, Windows Server 2019 ve Windows Server 2016 ' de Microsoft Defender virüsten koruma 'yı yönetmek için grup ilkesi ayarlarını kullanma hakkında bilgi için bkz. [Microsoft Defender virüsten koruma yapılandırmak ve yönetmek için Grup İlkesi ayarlarını kullanma](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## <a name="copy-endpoint-protection-policy-definitions"></a>Endpoint Protection ilkesi tanımlarını Kopyala

Endpoint Protection tarafından yönetilen alt düzey bir Windows cihazında, Endpoint Protection ilkesi tanım dosyalarını kopyalayın.

1. **C:\Program Files\Microsoft Security Client\Admx**adresine gidin. 

2. Aşağıdaki dosyaları bir ZIP dosyasına sıkıştırın, örneğin **SCEP_admx.zip**:
    - **EndPointProtection. adml**
    - **EndPointProtection. admx**
3. ZIP dosyasını geçici bir klasöre kopyalayın. Örneğin, **c:\ temp_SCEP_GPO_admx**.
4. Dosyayı ayıklayın. 

> [!NOTE]
> Endpoint Protection ilke ayarlarını yapılandırmak için kayıt defteri anahtarları, **HKEY_local_machine \Software\Policies\Microsoft\Microsoft antimalware**dizininde bulunur.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Endpoint Protection grup ilkesi ayarlarını bir etki alanı denetleyicisindeki merkezi depoya yükleme

[Grup ilkesi Yönetim Şablonları Için merkezi bir mağaza](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)kullanıyorsanız, Endpoint Protection Grup İlkesi ayarlarını yüklemek ve yapılandırmak için aşağıdaki adımları uygulayın. Önerilen yöntem budur.

1. Endpoint Protection ilke tanımı dosyalarını ayıkladığınız klasöre gidin.
2. . Admx ve. adml dosyalarını etki alanı denetleyicisindeki **PolicyDefinitions** klasörüne kopyalayın:
    1. **Endpointprotection. admx** öğesini ** \\ \\ \<forest.root\> \\ SYSVOL \\ \<domain\> \\ ilkeleri \\ PolicyDefinitions**öğesine kopyalayın. 
    2. **Endpointprotection. adml** 'yi ** \\ \\ \<forest.root\> \\ SYSVOL \\ \<domain\> \\ ilkeleri \\ PolicyDefinitions \\ en-US**olarak kopyalayın.  

    Örnek:
    
    - **Endpointprotection. admx** öğesini ** \\ Dc\sysvol\contoso.exe**olarak kopyalayın.
    - **Endpointprotection. adml** 'yi ** \\ Dc\sysvol\contoso.exe ile \ Ilkelerpolicydefinitions\en-US**dizinine kopyalayın.
    
    Burada **DC** , etki alanı denetleyicinizin adıdır ve **contoso.com** etki alanıdır.

3. [Grup İlkesi Yönetim Konsolu](/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) açın ve etki alanında yeni bir grup ilkesi NESNESI (GPO) oluşturun, örneğin **Endpoint Protection**.
4. Endpoint Protection için GPO 'ya sağ tıklayın ve **Düzenle**' ye tıklayın.
5. Grup İlkesi Yönetimi Düzenleyicisi, **bilgisayar yapılandırma**  >  **ilkeleri**  >  **Yönetim Şablonları: ilke tanımları**  >  **Windows bileşenleri**  >  **Endpoint Protection**' ne gidin.

   Endpoint Protection grup Ilkelerinin listesi görüntülenir.

6. Yapılandırmak istediğiniz ayarı içeren bölümü genişletin, açmak için ayarı çift tıklatın ve yapılandırma değişiklikleri yapın.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Endpoint Protection grup ilkesi ayarlarını yerel cihazınıza yükleme

Endpoint Protection ilke tanımlarını yüklemek için merkezi mağaza kullanmak yerine, bunları cihazınızda yerel olarak saklayabilirsiniz.

1. Endpoint Protection ilke tanımı dosyalarını ayıkladığınız klasöre gidin.
2. . Admx ve. adml dosyalarını yerel PolicyDefinitions klasörünüze kopyalayın.
    1. **Endpointprotection. admx** öğesini **% systemroot%/PolicyDefinitions**öğesine kopyalayın. 
    2. **Endpointprotection. adml** 'Yi **% systemroot%/PolicyDefinitions/en-US**öğesine kopyalayın.
    
    Örnek:

    - **Endpointprotection. admx** öğesini **c:\Windows\PolicyDefinitions**içine kopyalayın.
    - **Endpointprotection. adml** 'yi **C:\windows\policydefinitions\en-US**klasörüne kopyalayın.
    
3. Yerel Grup İlkesi Düzenleyicisi açın.
4. **Computer Configuration**  >  **Administrative Templates**  >  **Windows bileşenleri**  >  **Endpoint Protection**Yönetim Şablonları bilgisayar yapılandırması ' na gidin.

    Endpoint Protection grup Ilkelerinin listesi görüntülenir.

5. Yapılandırmak istediğiniz ayarı içeren bölümü genişletin, açmak için ayarı çift tıklatın ve yapılandırma değişiklikleri yapın.

## <a name="next-steps"></a>Sonraki adımlar
- Endpoint Protection bir genel bakış için bkz. [Endpoint Protection](endpoint-protection.md).
- Tek başına istemcideki Endpoint Protection el ile yapılandırma hakkında bilgi için bkz. [tek başına istemcide Endpoint Protection yapılandırma](endpoint-protection-configure-standalone-client.md).