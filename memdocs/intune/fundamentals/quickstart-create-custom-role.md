---
title: Hızlı Başlangıç - Intune'da özel bir rol oluşturma ve atama
description: Hızlı Başlangıç - Uzak bir cihaz yöneticisi için özel bir rol oluşturun ve atayın.
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 03/26/2019
ms.author: erikje
ms.assetid: 0b3ac749-4a61-4717-bf08-e0e6a15c3b0a
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6cb0080a63c14c2a2fe4acd5906980e63e6b832c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079986"
---
# <a name="quickstart-create-and-assign-a-custom-role"></a>Hızlı Başlangıç: Özel rol oluşturma ve atama

Bu Intune hızlı başlangıcında bir güvenlik işlemleri departmanı için belirli izinleri olan özel bir rol oluşturup atayacaksınız. Ardından rolü bu tür işletmenlerden oluşan bir gruba atayacaksınız. Hemen kullanabileceğiniz birkaç varsayılan rol bulunur. Ancak bunun gibi özel roller oluşturarak mobil cihaz yönetim sisteminizin tamamı üzerinde doğru ayarlı bir erişim denetiminiz olur.

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](free-trial-sign-up.md).

## <a name="prerequisites"></a>Önkoşullar

- Bu hızlı başlangıcı tamamlamak için [bir grup oluşturmanız](quickstart-create-group.md) gerekir.

## <a name="sign-in-to-intune"></a>Intune'da oturum açma

[Intune](https://aka.ms/intuneportal)'da Genel Yönetici veya Intune Hizmet Yöneticisi olarak oturum açın. Intune Deneme aboneliği oluşturduysanız aboneliği oluşturduğunuz hesap Genel yönetici rolüne sahip olur.

## <a name="create-a-custom-role"></a>Özel rol oluşturma

Özel bir rol oluştururken çok çeşitli eylemler için izinler belirleyebilirsiniz. Güvenlik işleri rolünde, işletmenin bir cihazın yapılandırmalarını ve ilkelerini gözden geçirebilmesi için birkaç Okuma izni ayarlayacağız.

1. Intune ' da, **Roller** > **tüm roller** > **Ekle**' yi seçin.
![Tarayıcı](./media/quickstart-create-custom-role/add-custom-role.png)
2. **Özel rol ekle** altında, **Ad** kutusuna *Güvenlik işlemleri*'ni girin.
3. **Açıklama** kutusuna *Bu rol güvenlik işletmeninin cihaz yapılandırma ve uyumluluk bilgilerini izlemesine olanak tanır* açıklamasını girin.
4.  >  **Oku****Tamam**' ın yanındaki**Kurumsal cihaz tanımlayıcılarını** >  **Yapılandır** > **Evet** ' i seçin.
![Tarayıcı](./media/quickstart-create-custom-role/corp-device-id-read.png)
5.  > **OK** **Okuma**Tamam '**ın yanındaki** **cihaz uyumluluk ilkeleri** > ' ni seçin.
6.  > **OK** **Oku**Tamam '**ın yanındaki** **cihaz yapılandırması** > ' nı seçin.
7.  > **OK** **Oku**Tamam ' ın yanındaki **kuruluş** > **Evet** ' i seçin.
8. **Tamam** > **Oluştur**seçeneğini belirleyin.

## <a name="assign-the-role-to-a-group"></a>Rolü bir gruba atama

Güvenlik işletmeninizin yeni izinleri kullanabilmesi için önce rolü güvenlik kullanıcısını içeren bir gruba atamalısınız.

1. Intune ' da, **Roller** > **tüm roller** > **güvenlik işlemleri**' ni seçin.
2. **Intune rolleri** altında **Atamalar** > **Ata**'yı seçin.
3. **Atama adı** kutusuna *Güvenlik işletmenleri* ifadesini girin.
4. **Üye (gruplar)** > **Ekle**öğesini seçin.
5. **Contoso Testçileri** grubunu seçin.
6. Tamam **Seç ' i** > **OK**seçin.
7. **Kapsam (gruplar)** > seçeneğini belirleyin > **contoso sınayıcılarını****dahil etmek için grupları seçin**.
8.  > **OK**Tamam > Tamam**Tamam ' ı**seçin. **Select**

Artık gruptaki herkes *Güvenlik işlemleri* rolünün bir üyesidir ve bir cihaz hakkındaki şu bilgileri inceleyebilir: kurumsal cihaz tanımlayıcıları, cihaz uyumluluk ilkeleri, cihaz yapılandırmaları ve kuruluş bilgileri.

## <a name="clean-up-resources"></a>Kaynakları temizleme

Yeni özel rolü artık kullanmak istemiyorsanız, silebilirsiniz. **Roller** > **tüm roller** ' i seçin > rolün yanındaki üç noktayı seçin > **silin**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta özel bir güvenlik işlemleri rolü oluşturup bir gruba atadınız. Intune’daki roller hakkında daha fazla bilgi için bkz. [Microsoft Intune ile rol tabanlı yönetim denetimi (RBAC)](role-based-access-control.md)

Bu Intune hızlı başlangıç serisini takip etmek için bir sonraki hızlı başlangıca ilerleyin.

> [!div class="nextstepaction"]
> [Hızlı başlangıç: iOS/ıpados için bir e-posta cihaz profili oluşturma](../configuration/quickstart-email-profile.md)
