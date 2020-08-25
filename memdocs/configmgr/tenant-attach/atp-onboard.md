---
title: Microsoft Endpoint Manager Yönetim Merkezi 'nden Microsoft Defender ATP 'ye kiracı ekleme Configuration Manager istemcileri (Önizleme)
titleSuffix: Configuration Manager
description: Yönetim merkezinden yönetilen istemcileri Configuration Manager için Microsoft Defender ATP uç nokta algılama ve yanıt (EDR) ekleme ilkelerini dağıtın.
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 50f8e206-a2af-469a-9f1b-0f7a87166f48
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a17d6fb437f83ae14895e8dd6d081ee4b6bd80fb
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88827039"
---
# <a name="tenant-attach-onboard-configuration-manager-clients-to-microsoft-defender-atp-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Kiracı iliştirme: Yönetim Merkezi 'nden Microsoft Defender ATP 'ye Configuration Manager istemcileri ekleme (Önizleme)
<!--5691658-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Yönetilen istemcileri Configuration Manager için Microsoft Defender ATP uç noktası algılama ve yanıt (EDR) ekleme ilkeleri dağıtabilirsiniz. Bu istemciler Azure AD veya MDM kaydı gerektirmez ve ilke, Azure AD grupları yerine ConfigMgr koleksiyonlarına hedeflenmiş olur.

## <a name="prerequisites"></a>Önkoşullar

- [Microsoft Endpoint Manager yönetim merkezine](https://endpoint.microsoft.com/)erişin.
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements)için E5 lisansı.
- [Karşıya yüklenen cihazlara kiracı eklenmiş](device-sync-actions.md)bir ortam.
- En az Configuration Manager sürüm 2006 ve konsolun ilgili sürümü yüklü.
   - Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.

## <a name="make-configuration-manager-collections-available-to-assign-endpoint-security-policies"></a><a name="bkmk_collections"></a> Uç nokta güvenlik ilkeleri atamak için Configuration Manager koleksiyonlarının kullanılabilmesini sağlama

Cihaz koleksiyonlarının Endpoint Security ilkeleriyle Intune 'a çalışmasını etkinleştirdiğinizde, bu koleksiyonlardaki cihazları Microsoft Defender ATP ile birlikte çalışmak üzere yapılandırıyorsunuz demektir.

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](../../intune/protect/includes/make-configmgr-collection-available-edr.md)]

## <a name="create-microsoft-defender-atp-endpoint-detection-and-response-edr-onboarding-policies"></a><a name="bkmk_onboard"></a> Microsoft Defender ATP uç noktası algılama ve yanıt (EDR) ekleme ilkeleri oluşturun

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://endpoint.microsoft.com)oturum açın.

1. **Uç nokta güvenlik**  >  **uç noktası algılama ve yanıt**  >  **oluşturma ilkesi**seçin.

1. İlkenizin için aşağıdaki platformu ve profili seçin:

   - Platform: **Windows 10 ve Windows Server (ConfigMgr)**
   - Profil: **Endpoint Detection ve yanıt (ConfigMgr)**

1. **Oluştur**’u seçin.

1. **Temel bilgiler** sayfasında, profil için bir ad ve açıklama girin ve ardından **İleri**' yi seçin.

1. **Yapılandırma ayarları** sayfasında, bu profille yönetmek istediğiniz ayarları yapılandırın. Ekleme paketi otomatik olarak eklenir ve yapılandırabileceğiniz bir şey değildir.

   Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin.

1. **Atamalar** sayfasında, bu ilkeyi alacak koleksiyonları seçin. Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenen ve Microsoft Defender ATP ilkesi için etkinleştirilen Configuration Manager koleksiyonları seçin.

   Şu anda koleksiyonlar atamaz ve daha sonra bir atama eklemek için ilkeyi düzenleyelim ' i seçebilirsiniz.

   Devam etmeye hazırsanız **İleri**' yi seçin.

1. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin.

   Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar

[Kiracı ekli cihazlara Endpoint Security virüsten koruma ilkesi oluşturma ve dağıtma](deploy-antivirus-policy.md)