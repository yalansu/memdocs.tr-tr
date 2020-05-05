---
title: WSUS 'den kötü amaçlı yazılım tanımları Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Windows Server güncelleştirme hizmetleri 'ni tanım güncelleştirmelerini otomatik olarak onaylanacak şekilde yapılandırmayı öğrenin.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126032"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Configuration Manager için WSUS 'tan indirmek üzere Endpoint Protection kötü amaçlı yazılım tanımlarını etkinleştirin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kötü amaçlı yazılım tanımlarınızı güncel tutmak için WSUS kullanıyorsanız, tanım güncelleştirmelerini otomatik olarak onaylayacak şekilde yapılandırabilirsiniz. Configuration Manager yazılım güncelleştirmelerinin kullanılması, Tanımlarınızın güncel tutulması için önerilen yöntem olsa da, WSUS 'i kullanıcıların tanımları el ile güncelleştirmesine izin veren bir yöntem olarak da yapılandırabilirsiniz. WSUS’i bir tanım güncelleştirme kaynağı olarak yapılandırmak için aşağıdaki yordamları kullanın.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Configuration Manager için tanım güncelleştirmelerini eşitler

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve ardından **siteler**' i seçin.

1. Yazılım güncelleştirme noktanızı içeren siteyi seçin. Şeridin **Ayarlar** grubunda **site bileşenlerini Yapılandır**' ı seçin ve ardından **yazılım güncelleştirme noktası**' nı seçin.

1. **Yazılım güncelleştirme noktası bileşen özellikleri** penceresinde **sınıflandırmalar** sekmesine geçin. **tanım güncelleştirmeleri**' ni seçin.

1. WSUS ile güncelleştirilmiş **ürünleri** belirtmek Için, **Ürünler** sekmesine geçin.

    - Windows 10 ve üzeri için: Microsoft > Windows altında **Windows Defender**' ı seçin.

    - Windows 8.1 ve önceki sürümler için: Microsoft > Forefront altında **System Center Endpoint Protection**' yı seçin.

1. **Yazılım güncelleştirme noktası bileşen özellikleri** penceresini kapatmak için **Tamam ' ı** seçin.

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Tek başına WSUS için tanım güncelleştirmelerini eşitler

WSUS sunucunuz Configuration Manager ortamınıza tümleştirmediğinde Endpoint Protection güncelleştirmelerini yapılandırmak için aşağıdaki yordamı kullanın.

1. WSUS Yönetim konsolunda **bilgisayarlar**' ı genişletin, **Seçenekler**' i seçin ve ardından **ürünler ve sınıflandırmalar**' ı seçin.

1. WSUS ile güncelleştirilmiş **ürünleri** belirtmek Için, **Ürünler** sekmesine geçin.

    - Windows 10 ve üzeri için: Microsoft > Windows altında **Windows Defender**' ı seçin.

    - Windows 8.1 ve önceki sürümler için: Microsoft > Forefront altında **System Center Endpoint Protection**' yı seçin.

1. **Sınıflandırmalar** sekmesine geçin. **tanım güncelleştirmeleri** ve **güncelleştirmeler**' i seçin.

## <a name="approve-definition-updates"></a>Tanım güncelleştirmelerini Onayla

Endpoint Protection tanım güncelleştirmeleri, kullanılabilir güncelleştirmeler listesini isteyen istemcilere sunulmadan önce onaylanmalı ve WSUS sunucusuna indirilmelidir. İstemciler ilgili güncelleştirmeleri denetlemek ve sonra en son onaylanan tanım güncelleştirmelerini istemek için WSUS sunucusuna bağlanır.

### <a name="approve-definitions-and-updates-in-wsus"></a>WSUS 'de tanımları ve güncelleştirmeleri onaylama

1. WSUS Yönetim konsolunda, **güncelleştirmeler**' i seçin. Ardından **tüm güncelleştirmeler** ' i veya onaylamak istediğiniz güncelleştirmelerin sınıflandırmasını seçin.

1. Güncelleştirmeler listesinde, yükleme için onaylamak istediğiniz güncelleştirmeye veya güncelleştirmelere sağ tıklayın ve ardından **Onayla**' yı seçin.

1. **Güncelleştirmeleri Onayla** penceresinde, güncelleştirmeleri onaylamak istediğiniz bilgisayar grubunu seçin ve ardından **yüklenmek üzere onaylanmış**' ı seçin.

### <a name="configure-an-automatic-approval-rule"></a>Otomatik onay kuralı yapılandırma

Ayrıca, tanım güncelleştirmeleri ve Endpoint Protection güncelleştirmeleri için bir otomatik onay kuralı da ayarlayabilirsiniz. Bu eylem, WSUS tarafından indirilen Endpoint Protection tanım güncelleştirmelerini otomatik olarak onaylamak için WSUS 'yi yapılandırır.

1. WSUS Yönetim konsolunda **Seçenekler**' i ve ardından **Otomatik onaylar**' ı seçin.

1. **Güncelleştirme kuralları** sekmesinde **Yeni kural**' ı seçin.

1. **Kural Ekle** penceresindeki **Adım 1: özellikleri seçin**' in altında, **bir güncelleştirme belirli bir sınıflandırmada olduğunda**seçeneğini belirleyin.

    1. **2. Adım: özellikleri düzenleme**altında **herhangi bir sınıflandırma**seçin.

    1. **Tanım güncelleştirmeleri**dışındaki tüm seçenekleri temizleyin ve ardından **Tamam**' ı seçin.

1. **Kural Ekle** penceresindeki **Adım 1: özellikleri seçin**' in altında, **bir güncelleştirme belirli bir üründe**olduğunda seçeneğini belirleyin.

    1. **2. Adım: özellikleri düzenleme**altında **herhangi bir ürünü**seçin.

    1. Windows 8.1 ve önceki sürümleri için **System Center Endpoint Protection** dışındaki tüm seçenekleri veya Windows 10 ve üzeri Için **Windows Defender 'ı** temizleyin. Sonra **Tamam**’ı seçin.

1. **Adım 3: bir ad belirtin**altında kural için bir ad girin ve ardından **Tamam**' ı seçin.

1. **Otomatik onaylar** iletişim kutusunda yeni oluşturulan kuralı seçin ve ardından **kuralı Çalıştır**' ı seçin.

> [!NOTE]
> WSUS sunucunuz ve istemci bilgisayarlarınız üzerinde performansı en üst düzeye çıkarmak için eski tanım güncelleştirmelerini reddedin. Bu görevi gerçekleştirmek üzere, düzeltmeleri otomatik onaylamayı ve süresi dolan güncelleştirmeleri otomatik reddetmeyi yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Microsoft desteği makalesi 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md)
