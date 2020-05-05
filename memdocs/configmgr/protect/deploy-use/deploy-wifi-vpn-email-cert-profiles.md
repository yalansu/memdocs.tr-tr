---
title: Kaynak erişim profillerini dağıtma
titleSuffix: Configuration Manager
description: Configuration Manager ' de Wi-Fi, VPN ve Sertifika profillerinin nasıl dağıtılacağını öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724520"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Configuration Manager 'de kaynak erişim profillerini dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki kaynak erişim profillerinden birini oluşturduktan sonra, bir veya daha fazla koleksiyona dağıtın:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Sertifika](create-certificate-profiles.md)

Bu profilleri dağıttığınızda, hedef koleksiyonu belirtin ve istemcinin profili uyumluluk için ne sıklıkta değerlendirileceğini belirtirsiniz.  

## <a name="deploy-a-profile"></a>Profil dağıtma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve ardından uygun profil düğümünü seçin. Örneğin, **Wi-Fi profilleri**.

1. Profiller listesinde, dağıtmak istediğiniz profili seçin. Ardından, şeridin **giriş** sekmesinde, **dağıtım** grubunda, **Dağıt**' ı seçin.  

1. Profili dağıt penceresinde, aşağıdaki bilgileri belirtin:  

    - **Koleksiyon**: profili dağıtmak istediğiniz koleksiyonu seçin.

    - **Uyarı oluştur**: bir uyarı yapılandırmak için bu seçeneği etkinleştirin. Profil uyumluluğu belirtilen tarih ve saate göre belirtilen yüzdeden küçük olduğunda site bu uyarıyı oluşturur. Ayrıca, System Center Operations Manager bir uyarının gönderilmesini isteyip istemediğinizi de seçebilirsiniz.

    - **Rastgele gecikme (saat)**: basıt SERTIFIKA kayıt Protokolü (SCEP) ayarlarını içeren sertifika profilleri Için, ağ cihazı kayıt hizmeti 'NDE (NDES) aşırı işleme engel olmak için bir gecikme penceresi belirtin. Varsayılan değer `64` saattir.  

    - **Bunun için uyumluluk değerlendirme zamanlamasını belirtin... profil**: istemcinin bu profil için uyumluluğu ne sıklıkta değerlendirdileceğini belirtin. Basit bir **zamanlama** seçin veya özel bir **zamanlama**yapılandırın. Varsayılan olarak, basit zamanlama her `12` saat olur.

1. Pencereyi kapatmak ve dağıtımı oluşturmak için **Tamam ' ı** seçin.

## <a name="delete-a-deployment"></a>Bir dağıtımı silme

Bir dağıtımı silmek istiyorsanız listeden seçin. Ayrıntılar bölmesinde **dağıtımlar** sekmesine geçin. dağıtımı seçin ve ardından şeridin **dağıtım** sekmesinde **Sil**' i seçin.

> [!IMPORTANT]
> Bir VPN profili dağıtımını kaldırdığınızda Configuration Manager VPN profilini Windows 'dan kaldırmaz. Profili cihazlardan kaldırmak istiyorsanız, el ile kaldırın.

## <a name="next-steps"></a>Sonraki adımlar

[Wi-Fi ve VPN profillerini izleme](monitor-wifi-email-vpn-profiles.md)

[Sertifika profillerini izleme](monitor-certificate-profiles.md)
