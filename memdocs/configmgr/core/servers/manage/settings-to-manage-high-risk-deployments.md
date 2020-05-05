---
title: Yüksek riskli dağıtımları yönetme
titleSuffix: Configuration Manager
description: Yüksek riskli bir dağıtım oluşturduklarında yöneticileri uyarmak için Configuration Manager dağıtım doğrulama site ayarlarını yapılandırın.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719991"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Configuration Manager için yüksek riskli dağıtımları yönetme ayarları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, *dağıtım doğrulama* site ayarlarını yapılandırabilirsiniz. Bu ayarlar, yüksek riskli bir görev dizisi dağıtımı oluşturduklarında yöneticileri uyarır. Yüksek riskli dağıtım:  

- Otomatik olarak yüklenen bir dağıtım  

- İstenmeyen sonuçlara neden olma olasılığı vardır  

Örneğin, amacı **gerekli** olan ve bir işletim sistemini dağıtan bir görev dizisi, yüksek riskli olarak kabul edilir.  

> [!WARNING]
> PXE dağıtımlarını kullanır ve ilk önyükleme aygıtı olarak ağ bağdaştırıcısı ile cihaz donanımını yapılandırırsanız, bu cihazlar Kullanıcı etkileşimi olmadan bir işletim sistemi dağıtımı görev sırasını otomatik olarak başlatabilir. Dağıtım doğrulaması bu yapılandırmayı yönetmez. Bu yapılandırma işlemi basitleştirecek ve kullanıcı etkileşimini azaltmasına karşın, yanlışlıkla yeniden görüntü için cihazı daha fazla riske koyar.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a>Dağıtım doğrulama ayarları

İstenmeyen yüksek riskli dağıtım riskini azaltmak için, bu dağıtım doğrulama ayarlarında boyut sınırlarını yapılandırabilirsiniz:  

- **Koleksiyon boyutu sınırları**: bir dağıtım oluşturduğunuzda, sınırınızdan daha fazla istemci içeren koleksiyonları gizleyin.  

  - **Varsayılan boyut**: bir dağıtım oluşturduğunuzda, bu ayar, bu sınırdan daha fazla istemci içeren koleksiyonları varsayılan olarak gizler. Dağıtımı oluştururken bu koleksiyonları görmeye devam edebilirsiniz, ancak bunlar varsayılan olarak gizlidir. Varsayılan değer **100**' dir. Bu ayarı yok saymak için **0**değeri girin.  

  - **En büyük boyut**: bir dağıtım oluşturduğunuzda, bu ayar her zaman bu sınırdan daha fazla istemci içeren koleksiyonları gizler. Varsayılan değer **0**' dır ve bu ayarı yok sayar. **En büyük boyut** değeri **Varsayılan boyut** değerinden büyük olmalıdır.  

    Örneğin, **varsayılan boyut** olarak 100 ve **en büyük boyut** 1000 olarak ayarlanır. Yüksek riskli bir dağıtım oluşturduğunuzda **Koleksiyon Seç** penceresinde yalnızca 100 ' den az istemci içeren koleksiyonlar görüntülenir. **Üye sayısı sitenin en düşük boyut yapılandırmasından daha büyük olan koleksiyonları gizleme**ayarını temizlerseniz, pencerede 1000 ' den az istemci içeren koleksiyonlar görüntülenir.  

- **Site sistem sunucularına sahip koleksiyonlar**: hedef koleksiyon, site sistem rolüne sahip bir bilgisayar içerdiğinde, dağıtımı oluşturmadan önce dağıtımları engelleyin veya doğrulama gerektir. Bir dağıtım engellendiğinde, dağıtımı oluşturmaya devam etmek için dağıtım doğrulama ölçütlerini karşılayan farklı bir koleksiyon seçin.  

> [!NOTE]
> Yüksek riskli dağıtımlar her zaman özel koleksiyonlar, oluşturduğunuz koleksiyonlar ve yerleşik **Bilinmeyen Bilgisayarlar** koleksiyonu ile sınırlıdır. Yüksek riskli dağıtım oluşturduğunuzda, **Tüm sistemler**gibi yerleşik bir koleksiyon seçemezsiniz.  

## <a name="configure-deployment-verification"></a>Dağıtım doğrulamasını yapılandırma

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin, **siteler**' i seçin ve ardından yapılandırılacak birincil siteyi seçin.

2. Şeritte **Özellikler**' i seçin ve ardından **dağıtım doğrulama** sekmesine geçin.

3. Kullanmak istediğiniz [ayarları](#bkmk_settings) yapılandırın ve ardından **Tamam** ' ı seçerek yapılandırmayı kaydedin ve özellikleri kapatın.

## <a name="next-steps"></a>Sonraki adımlar

[Görev dizilerini yönetme-yüksek etki ayarları](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Siteleri ve hiyerarşileri yapılandırma](../deploy/configure/configure-sites-and-hierarchies.md)
