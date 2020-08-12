---
title: Windows’u ağ üzerinden dağıtmak için önyüklenebilir ortam kullanma
titleSuffix: Configuration Manager
description: Hedef bilgisayar başladığında işletim sistemini dağıtmak için Configuration Manager 'da önyüklenebilir medya dağıtımlarını kullanın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124765"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile ağ üzerinden Windows dağıtmak için önyüklenebilir medya kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Önyüklenebilir medya yalnızca önyükleme görüntüsünü ve görev dizisine yönelik bir işaretçiyi içerir. İşletim sistemi görüntüsünü ve diğer başvurulan içeriği ağdan indirir. Önyüklenebilir medya çok fazla içerik içermediğinden, medyayı değiştirmek zorunda kalmadan görev dizisini ve en fazla içeriği güncelleştirebilirsiniz.

Aşağıdaki senaryolarda önyükleme medyasından işletim sistemlerini ağ üzerinden dağıtın:

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)

- [Mevcut bir bilgisayarı değiştirme ve ayarları aktarma](replace-an-existing-computer-and-transfer-settings.md)

İşletim sistemi dağıtım senaryolarından birindeki adımları tamamladıktan sonra, işletim sistemini dağıtmak için önyüklenebilir medyayı kullanmak üzere aşağıdaki bölümleri kullanın.

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma

İşletim sistemi dağıtım işlemini başlatmak üzere önyüklenebilir medya kullandığınızda, işletim sistemini medya tarafından kullanılabilir hale getirmek için görev dizisi dağıtımını yapılandırın. Dağıtımın **dağıtım ayarları** sayfasında bu seçeneği ayarlayın. **Aşağıdakiler için kullanılabilir yap** ayarı için, aşağıdaki seçeneklerden birini seçin:

- İstemcileri, medyayı ve PXE 'yi Configuration Manager

- Yalnızca medya ve PXE

- Yalnızca medya ve PXE (gizli)

Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="create-the-bootable-media"></a>Önyüklenebilir medya oluşturma

Önyüklenebilir medya oluştururken, bunun bir USB flash sürücü veya CD/DVD seti olup olmadığını belirtin. Medyayı başlatan bilgisayar önyüklenebilir sürücü olarak belirlediğiniz seçeneği desteklemelidir. Daha fazla bilgi için bkz. [önyüklenebilir medya oluşturma](create-bootable-media.md).

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a>Önyükleme medyasından işletim sistemini yükler

İşletim sistemini yüklemek için önyüklenebilir medyayı yerleştirin ve ardından bilgisayarı kapatın.

## <a name="support-for-cloud-based-content"></a>Bulut tabanlı içerik desteği

<!--6209223-->

Sürüm 2006 ' den başlayarak önyüklenebilir medya, bulut tabanlı içeriği indirebilir. Örneğin, cihazlarını yeniden görüntüetmek için uzak ofisteki bir kullanıcıya USB anahtarı gönderirsiniz. Ya da yerel bir PXE sunucusuna sahip olan bir Office, ancak cihazların bulut hizmetlerini mümkün olduğunca önceliklendirmesine olanak tanır. Önyükleme medyası ve PXE dağıtımları büyük işletim sistemi dağıtım içeriğini indirmek için WAN kullanımı yerine artık bulut tabanlı kaynaklardan içerik alabilir. Örneğin, içerik paylaşmak için etkinleştirdiğiniz bir bulut yönetimi ağ geçidi (CMG).

> [!NOTE]
> Cihazın hala yönetim noktasına bir intranet bağlantısı olması gerekir.

Görev sırası çalıştırıldığında, bulut tabanlı kaynaklardan içerik indirir. İstemcideki **Smsts. log dosyasına** bakın.

### <a name="prerequisites"></a>Ön koşullar

- **Cloud Services** grubunda şu istemci ayarını etkinleştirin: **bulut dağıtım noktasına erişime izin ver**. İstemci ayarının hedef istemcilere dağıtıldığından emin olun. Daha fazla bilgi için bkz. [istemci ayarları-bulut hizmetleri hakkında](../../core/clients/deploy/about-client-settings.md#cloud-services).

- İstemcinin bulunduğu sınır grubu için:

  - İçerik özellikli CMG veya bulut dağıtım noktası site sistemlerini ilişkilendirin. Daha fazla bilgi için bkz. [sınır grubunu yapılandırma](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Şu seçeneği etkinleştirin: Şirket **içi kaynaklar üzerinde bulut tabanlı kaynakları tercih**edin. Daha fazla bilgi için bkz. [eş İndirmeleri Için sınır grubu seçenekleri](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Görev dizisi tarafından başvurulan içeriği içerik özellikli CMG veya bulut dağıtım noktasına dağıtın.

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemi dağıtımı için kullanıcı deneyimleri](../understand/user-experience.md#task-sequence-wizard)
