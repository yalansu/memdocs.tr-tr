---
title: Intune’daki cihazları gruplar halinde kategorilere ayırma
titleSuffix: Microsoft Intune
description: Daha kolay yönetim için cihazları gruplar halinde kategorilere ayırmayı öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7b668c37-40b9-4c69-8334-5d8344e78c24
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b10d56e9eb915273d5be9a5b14ca4528a64a2057
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327098"
---
# <a name="categorize-devices-into-groups"></a>Cihazları gruplar halinde kategorilere ayırma

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Cihaz yönetimini kolaylaştırmak için Microsoft Intune cihaz gruplarını kullanabilir ve tanımladığınız cihaz kategorilerine dayanarak cihazları gruplara otomatik olarak ekleyebilirsiniz.

Cihaz kategorileri aşağıdaki iş akışını kullanır:
1. Kullanıcıların cihazlarını kaydederken arasından seçim yapabileceği kategoriler oluşturun.
2. İOS/ıpados ve Android cihazlarının kullanıcıları bir cihazı kaydettiğinde, yapılandırdığınız kategori listesinden bir kategori seçmesi gerekir. Bir Windows cihaza kategori atamak için kullanıcıların Şirket Portalı web sitesini kullanmaları gerekir.
3. Ardından bu gruplara ilkeler ve uygulamalar dağıtabilirsiniz.

İstediğiniz herhangi bir cihaz kategorisini oluşturabilirsiniz. Örneğin:
- Satış noktası cihazı
- Tanıtım cihazı
- Satışlar
- Muhasebe
- Yönetici

## <a name="how-to-configure-device-categories"></a>Cihaz kategorilerini yapılandırma

### <a name="step-1-create-device-categories-on-the-intune-blade-of-the-azure-portal"></a>1. Adım: Azure portalının Intune dikey penceresinde cihaz kategorileri oluşturma
1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın, **cihazlar** > **cihaz kategorileri**' ni seçin.
2. Yeni bir kategori eklemek için **cihaz kategorileri** sayfasında **Oluştur** ' u seçin.
3. **Cihaz kategorisi oluştur** dikey penceresinde, yeni kategori için bir **Ad** ve isteğe bağlı bir **Açıklama** girin.
4. İşiniz bittiğinde **Oluştur**'u seçin. Kategori listesinde yeni kategoriyi görebilirsiniz.

2. adımda Azure Active Directory (Azure AD) güvenlik grupları oluştururken cihaz kategorisi adını kullanacaksınız.

### <a name="step-2-create-azure-active-directory-security-groups"></a>2. Adım: Active Directory güvenlik grupları oluşturma
Bu adımda, Azure portalında cihaz kategorisi ve cihaz kategorisi adına dayalı dinamik gruplar oluşturacaksınız.

Devam etmek için Azure AD belgelerindeki [Gelişmiş kurallar oluşturmak için öznitelikleri kullanma](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/#using-attributes-to-create-rules-for-device-objects) konusuna bakın.

**deviceCategory** özniteliğini kullanarak gelişmiş bir kural ile bir cihaz grubu oluşturmak için bu bölümdeki bilgilerden yararlanın. Örneğin (**device.deviceCategory -eq** “*Azure portalından aldığınız cihaz kategorisi adı*”.

Siz cihaz gruplarını yapılandırdıktan ve kullanıcılar cihazlarını kaydettikten sonra, onlara sizin yapılandırdığınız kategori listesi gösterilir. Kullanıcılar kategoriyi seçip kaydı tamamladıktan sonra, cihazları seçtikleri kategoriye karşılık gelen Active Directory güvenlik grubuna eklenir.

### <a name="view-the-categories-of-devices-that-you-manage"></a>Yönettiğiniz cihazların kategorilerini görüntüleme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın, **cihazlar** > **tüm cihazlar**' ı seçin.

2. Cihaz listesinde **Cihaz kategorisi** sütununu inceleyin.

**Cihaz kategorisi** sütunu gösterilmemişse, **sütunlar** > **kategorisi** > **Uygula**' yı seçin.

### <a name="change-the-category-of-a-device"></a>Bir cihazın kategorisini değiştirme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın, **cihazlar** > **tüm cihazlar** ' ı seçin > > **özellikleri**istediğiniz cihazı seçin.
2. Sonraki dikey pencerede, seçili cihazın **Cihaz kategorisi**’ni daha önce yapılandırmış olduğunuz herhangi bir kategori adıyla değiştirebilirsiniz.

## <a name="after-you-configure-device-groups"></a>Cihaz gruplarını yapılandırdıktan sonra

İOS/ıpados ve Android cihazlarının kullanıcıları cihazlarını kaydettiklerinde, yapılandırdığınız kategori listesinden bir kategori seçmesi gerekir. Kategoriyi seçip kaydı tamamladıktan sonra cihazlar, seçtikleri kategoriye karşılık gelen Intune cihaz grubuna veya Active Directory güvenlik grubuna eklenir.

Windows kullanıcıları bir kategori seçmek için Şirket Portalı web sitesini kullanmalıdır.

Platformları ne olursa olsun kullanıcılarınız cihazlarını kaydettikten sonra istedikleri zaman portal.manage.microsoft.com adresine gidebilir. Kullanıcının Şirket Portalı Web sitesine erişmesini ve **Cihazlarım**' a gitmesini sağlayabilirsiniz. Kullanıcı, sayfada listelenen kayıtlı bir cihazı ve sonra da kategoriyi seçebilir.

Bir kategori seçtikten sonra cihaz, oluşturduğunuz karşılık gelen gruba otomatik olarak eklenir. Kategorileri yapılandırmadan önce kaydedilmiş bir cihaz varsa kullanıcı, Şirket Portalı web sitesinde bu cihaz hakkında bildirim alır. Bu, kullanıcının iOS/ıpados veya Android 'de Şirket Portalı uygulamasına bir sonraki erişimlerse bir kategori seçmesini bilmesini sağlar.

## <a name="further-information"></a>Daha fazla bilgi
- Azure Portalı’nda cihaz kategorisini düzenleyebilirsiniz ama bu kategoriye başvuran tüm Azure AD güvenlik gruplarını kendiniz güncelleştirmeniz gerekir.

- Bir kategoriyi silerseniz, bu kategoriye atanmış olan tüm cihazlar **Atanmamış** kategori adını görüntüler.
