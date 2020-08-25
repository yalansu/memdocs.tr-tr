---
title: Microsoft Endpoint Manager Yönetim Merkezi 'nden kiracı iliştirme ve uç nokta güvenlik virüsten koruma ilkesini dağıtma (Önizleme)
titleSuffix: Configuration Manager
description: " Microsoft Endpoint Manager konsolundan ve Configuration Manager koleksiyonlarında Microsoft Defender virüsten koruma ilkeleri oluşturun ve dağıtın."
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d09b519bfc116afd397d455c6a03a8748f9303cd
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88827033"
---
# <a name="tenant-attach-create-and-deploy-endpoint-security-antivirus-policy-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Kiracı iliştirme: yönetim merkezinden Endpoint Security virüsten koruma ilkesi oluşturma ve dağıtma (Önizleme)
<!--5691658-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez. 

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Microsoft Endpoint Manager konsolunda Microsoft Defender virüsten koruma ilkeleri oluşturun ve bunları Configuration Manager koleksiyonlara dağıtın.


## <a name="prerequisites"></a>Önkoşullar

- [Microsoft Endpoint Manager yönetim merkezine](https://endpoint.microsoft.com/)erişin.
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements)için E5 lisansı.
- [Karşıya yüklenen cihazlara kiracı eklenmiş](device-sync-actions.md)bir ortam.
- En az Configuration Manager sürüm 2006 ve konsolun ilgili sürümü yüklü.
   - Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.
- [Uç nokta güvenlik ilkeleri atamak için kullanılabilen](atp-onboard.md#bkmk_collections) en az bir Configuration Manager koleksiyonu

## <a name="supported-antivirus-profile-for-tenant-attached-devices"></a>Kiracı ekli cihazlar için desteklenen virüsten koruma profili

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](../../intune/protect/includes/configmgr-antivirus-profiles.md)]

## <a name="assign-antivirus-policies-to-a-collection"></a>Bir koleksiyona virüsten koruma ilkeleri atama

1. Bir tarayıcıda adresine gidin [https://aka.ms/MDAVTenantAttachPreview](https://aka.ms/MDAVTenantAttachPreview) .
1. **Endpoint Security** sonra **Virüsten koruma**' yı seçin.
1. **Ilke oluştur**' u seçin.
1. **Platform**için **Windows 10 ve Windows Server (ConfigMgr)** öğesini seçin.
1. **Profil**Için, **Microsoft Defender virüsten koruma (Önizleme)** öğesini seçin ve ardından **oluşturun**.
1. **Temel bilgiler** sayfasında bir **ad** ve Isteğe bağlı olarak bir **Açıklama** atayın.
1. **Yapılandırma ayarları** sayfasında, bu profille yönetmek istediğiniz ayarları yapılandırın. Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin. Kullanılabilir ilkeler hakkında daha fazla bilgi için bkz. [kiracı ekli cihazlar Için virüsten koruma ilkesi ayarları](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. İlkeyi **atamalar** sayfasında bir Configuration Manager koleksiyonuna atayın.

## <a name="next-steps"></a>Sonraki adımlar

[Kiracıya bağlı cihazlar için virüsten koruma ilkesi ayarları](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)