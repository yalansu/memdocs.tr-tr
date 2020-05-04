---
title: Bir ağ paylaşımından tanımları indirin
titleSuffix: Configuration Manager
description: Microsoft 'tan en son tanım güncelleştirmelerini el ile indirme ve ardından istemcileri bu tanımları indirmek üzere yapılandırma hakkında bilgi edinin.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715686"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Bir ağ paylaşımından indirmek Endpoint Protection kötü amaçlı yazılım tanımlarını etkinleştir

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Microsoft’tan en son tanım güncelleştirmelerini elle indirebilir ve ardından istemcileri, bu tanımları ağ üzerindeki paylaşılan bir klasörden indirecek şekilde yapılandırabilirsiniz. Bu güncelleştirme kaynağını kullandığınızda tanım güncelleştirmeleri kullanıcılar tarafından da başlatılabilir.

> [!NOTE]
>  İstemcilerin tanım güncelleştirmelerini indirebilmesi için paylaşılan klasöre okuma erişimi olmalıdır.

 Dosya paylaşımında depolanacak tanım ve altyapı güncelleştirmelerini indirme hakkında daha fazla bilgi için bkz. [en son Microsoft kötü amaçlı yazılımdan koruma ve casus yazılımdan koruma yazılımını yükleme](https://www.microsoft.com/wdsi/definitions).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Bir dosya paylaşımından tanım indirmelerini yapılandırmak için

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.

2.  **Varlıklar ve Uyum** çalışma alanında **Endpoint Protection**’ı genişletin ve **Kötü Amaçlı Yazılımdan Koruma İlkeleri**’ne tıklayın.

3.  **Varsayılan Kötü Amaçlı Yazılımdan Koruma İlkesi** ’nin özellikler sayfasını açın veya yeni bir kötü amaçlı yazılımdan koruma ilkesi oluşturun. Kötü amaçlı yazılımdan koruma ilkeleri oluşturma hakkında daha fazla bilgi için bkz. [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md).

4.  Kötü amaçlı yazılımdan koruma özellikleri iletişim kutusunun **Güvenlik Zekası güncelleştirmeleri** bölümünde **kaynağı ayarla**' ya tıklayın.
    - **Tanım güncelleştirmeleri** bölümü, Configuration Manager sürüm 1902 ' den başlayarak **Güvenlik Zekası güncelleştirmeleriyle** yeniden adlandırıldı.

5.  **Tanım Güncelleştirme Kaynaklarını Yapılandır** iletişim kutusunda **UNC dosya paylaşımlarından güncelleştirmeler**öğesini seçin.

6.  **Tamam** ’a tıklayarak **Tanım Güncelleştirme Kaynaklarını Yapılandır** iletişim kutusunu kapatın.

7.  **Yol Ayarla**’ya tıklayın. Ardından, **Tanım Güncelleştirme UNC Yollarını Yapılandır** iletişim kutusunda bir ağ paylaşımındaki tanım güncelleştirmeleri dosyalarının konumuna bir veya daha fazla UNC yolu ekleyin.

8.  **Tamam** ’a tıklayarak **Tanım Güncelleştirme UNC Yollarını Yapılandır** iletişim kutusunu kapatın.


> [!div class="button"]
> [Sonraki adım >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Geri >](endpoint-configure-alerts.md)
