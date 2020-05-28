---
title: Lisans ve dallar
titleSuffix: Configuration Manager
description: Configuration Manager ile kullanılabilen yükleme seçenekleri için lisans gereksinimleri hakkında bilgi edinin
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906043"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Configuration Manager için lisanslama ve dallar

*Uygulama hedefi: Configuration Manager (geçerli dal), & System Center Configuration Manager (uzun vadeli bakım dalı)*

Configuration Manager ile kullanılabilen yükleme seçenekleri için lisans gereksinimleri hakkında bilgi edinmek için bu makaleyi kullanın. Bu yükleme seçenekleri aşağıdaki dalları içerir:

- Geçerli dal
- Uzun süreli bakım dalı (LTSB)
- Geçerli dalın değerlendirmesi yüklemesi
- Technical Preview dalı

## <a name="licensing-overview"></a>Lisanslamaya genel bakış

Configuration Manager lisanslarında etkin yazılım güvencesi (SA) olan müşterilerimiz veya 1 Ekim 2016 itibariyle eşit abonelik haklarıyla, Configuration Manager 'ın 2016 Ekim 1606 sürümünü kullanma hakkı vardır. 1 Ekim 2016 ' de veya sonrasında Configuration Manager hakları olan müşteriler, yükleme sonrasında iki lisanslı seçenek bulur: geçerli dal ve uzun süreli bakım dalı (LTSB).

Microsoft Toplu Lisanslama programları aracılığıyla satın aldığınız ürünlerin tüm hüküm ve koşulları için bkz. [Lisans hüküm ve belgeleri](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).


## <a name="licensed-branches"></a>Lisanslı dallar

Bu makalede, yazılım güvencesi sözleşmesine veya eşdeğer abonelik haklarına başvurur. Bu Microsoft lisanslama sözleşmesi, Configuration Manager yüklemek ve kullanmak için haklar verir.

### <a name="current-branch"></a>Geçerli dal

Geçerli dal, Configuration Manager için etkin bir yazılım güvencesi sözleşmesi veya eşdeğer haklar gerektirir. Daha fazla bilgi için bkz. [yazılım güvencesi ve güncel dalı](#software-assurance-and-the-current-branch).

Bu dal, Microsoft 'tan düzenli kalite ve özellik güncelleştirmeleri almak isteyen üretim ortamlarında kullanılmak üzere desteklenir. Tüm özellikleri ve geliştirmeleri kullanmak için erişim sağlar.

1710 sürümünden itibaren, her güncelleştirme sürümü, genel kullanılabilirlik yayın tarihinden itibaren 18 ay destek içinde kalır. Daha fazla bilgi için bkz. [Configuration Manager geçerli dal sürümleri Için destek](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>Uzun süreli bakım dalı (LTSB)

LTSB, 1 Ekim 2016 itibariyle Microsoft ile geçerli bir yazılım güvencesi sözleşmesi gerektirir. Daha fazla bilgi için bkz. [yazılım güvencesi ve LTSB](#software-assurance-and-the-ltsb).

Bu dal, üretim ortamlarında kullanım için desteklenir. Yazılım Güvencesi (SA) veya eşdeğer aboneliklerin haklarının Configuration Manager 1 Ekim 2016 ' den sonra dolmasına izin veren müşteriler tarafından kullanılmak üzere tasarlanmıştır. Bu dal, Güncel Dalı karşılaştırıldığında sınırlandırılır.

Configuration Manager için kritik güvenlik güncelleştirmeleri bu dal için kullanılabilir hale getirilir ancak yeni bir özellik kullanılamaz.

### <a name="evaluation-installation-of-the-current-branch"></a>Geçerli dalın değerlendirmesi yüklemesi

Değerlendirme sürümü, Microsoft ile bir yazılım güvencesi sözleşmesi gerektirmez. [Değerlendirme yüklemeleri](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) her zaman geçerli daldır ve bunları 180 gün boyunca kullanabilirsiniz.

Değerlendirme yüklemesini geçerli dalın tam yüklemesine yükseltebilirsiniz. Bir değerlendirme yüklemesini uzun vadeli bakım dalına yükseltemezsiniz.

### <a name="technical-preview-branch"></a>Technical Preview dalı

[Technical Preview dalı](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) de mevcuttur. Bu dal, yeni özellikleri denemenizi sağlayan sınırlı bir Configuration Manager derlemesi sağlar. Teknik önizlemeyi, lisanslı sürümlerden farklı bir medya kullanarak yüklersiniz. Daha fazla bilgi için bkz. [Teknik Önizleme](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Yazılım Güvencesi sözleşmeleri

Configuration Manager lisanınızdaki yazılım güvencesi veya eşittir abonelik haklarından, 1 Ekim 2016 tarihinde veya sonrasında, yükleyip kullanabileceğiniz dalı belirler.

### <a name="software-assurance-and-the-current-branch"></a>Yazılım Güvencesi ve geçerli dal

Geçerli dalı Configuration Manager kullanma hakları tarafından sağlanarak şunları yapabilirsiniz:

- **System Center:** System Center Standard veya Datacenter lisanslarında etkin SA 'sı olan müşteriler Configuration Manager geçerli dal seçeneğini yükleyebilir ve kullanabilir.

- **System Center Configuration Manager:** Configuration Manager lisanslarında etkin SA veya eşdeğer abonelik haklarıyla olan müşteriler, Configuration Manager geçerli dal seçeneğini yükleyebilir ve kullanabilir.

1 Ekim 2016 ' de veya sonrasında Configuration Manager lisanslarda veya eşit abonelik haklarında etkin bir SA 'nız varsa:

- Geçerli dalı yükleyip kullanabilirsiniz.
- SA veya aboneliğin denetimini açmaya izin verirseniz, geçerli dalı kaldırmanız gerekir.

### <a name="software-assurance-and-the-ltsb"></a>Yazılım Güvencesi ve LTSB

1 Ekim 2016 ' de veya sonrasında Configuration Manager lisanslarda veya eşit abonelik haklarında etkin bir SA 'nız varsa:

- LTSB 'yi yükleyip kullanabilirsiniz. Configuration Manager için kalıcı haklara sahip olan veya SA veya aboneliğine izin veren müşteriler, atlama sırasında geçerli olan Configuration Manager LTSB sürümünü yükleyebilir.

LTSB, geçerli şube 1606 sürümünü temel alır ve aşağıdaki sınırlamalara sahiptir:

- Geçerli dalı LTSB 'ye dönüştürme desteği yoktur. Şu anda geçerli bir dal siteniz varsa, LTSB 'yi yeni bir site olarak yüklemelisiniz.  

- LTSB, geçerli dalın tüm yeteneklerini desteklemez. Daha fazla bilgi için bkz. [uzun süreli bakım dalına giriş](introduction-to-the-ltsb.md). Bu sınırlamalar, sınırlı bir özellik kümesi, sınırlı yükseltme seçenekleri ve ayrı bir ürün destek yaşam döngüsü içerir.  

### <a name="software-assurance-expiration-date"></a>Yazılım Güvencesi sona erme tarihi

Configuration Manager için sürüm 1606 temel ortamının 2016 Ekim sürümünden başlayarak, yazılım güvencesi sözleşmenizin sona erme tarihini belirtebilirsiniz. **Yazılım güvencesi sona erme tarihi** , uygun bir anımsatıcı olarak isteğe bağlı bir değerdir. Configuration Manager kurulumunu veya üstünü Configuration Manager konsolundan çalıştırdığınızda ekleyin.

> [!NOTE]
> Microsoft belirttiğiniz süre sonu tarihini doğrulamaz ve bu tarihi lisans doğrulaması için kullanmaz. Bunu, sona erme tarihinin bir anımsatıcısı olarak kullanın. Bu değer, Configuration Manager düzenli olarak çevrimiçi sunulan yeni yazılım güncelleştirmelerini denetlediğinde yararlıdır. Yazılım Güvencesi lisans durumunuz, bu ek güncelleştirmeleri kullanmaya uygun olması için güncel olmalıdır.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Yazılım Güvencesi sona erme tarihini belirtmek için

- Configuration Manager medyasından kurulum 'U çalıştırdığınızda, Kurulum sihirbazının **ürün anahtarı** sayfasında değeri belirtin.

- Configuration Manager konsolunda, **Hiyerarşi ayarları**' nda, **Lisans** sekmesinde değeri belirtin.


## <a name="licensing-resources"></a>Lisanslama kaynakları

Ürün lisanslama ayrıntıları hakkında daha fazla bilgi için aşağıdaki kaynakları kullanın.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Toplu Lisanslama Hizmet Merkezi (VLSC)

- [VLSC 'ye Genel Bakış](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Microsoft Toplu Lisanslama Ürün Koşulları](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- Toplu lisans müşterileri, [Toplu Lisans Hizmet Merkezi](https://www.microsoft.com/Licensing/servicecenter/default.aspx)' nden lisanslarının bir özetini alabilir. **Lisanslar** menüsüne gidin ve **lisanslar Özeti**' ni seçin.

### <a name="vlsc-videos"></a>VLSC videoları

- VLSC 'nin nasıl çalıştığı hakkında eğitim videoları için, [Microsoft Toplu Lisanslama Hizmet Merkezi eğitimi ve kaynakları](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) ' na gidin ve **nasıl yapılır videoları**' nı seçin.

- [Etkin yazılım güvencesi sözleşmenizin nerede aranacağı](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (43 saniyeden itibaren)  

- [VLSC için izin alma](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Kuruluşunuzdaki diğer kişilere VLSC okuma ve yazma izinleri atayabilirsiniz.
