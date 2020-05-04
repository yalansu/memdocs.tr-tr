---
title: Hızlı Başlangıç - Kullanıcıları yönetmek için grup oluşturma
titleSuffix: Microsoft Intune
description: Bu hızlı başlangıçta mevcut kullanıcılara dayanan bir grup oluşturmak için Microsoft Intune kullanacaksınız.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/17/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 723f4b4e-3090-4811-84ff-6af652abea5a
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7adb23f4709bf3ead07a01cb00d1b38fcb23c40
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330810"
---
# <a name="quickstart-create-a-group-to-manage-users"></a>Hızlı Başlangıç: Kullanıcıları yönetmek için grup oluşturma

Bu hızlı başlangıçta mevcut bir kullanıcıya dayanan bir grup oluşturmak için Intune kullanacaksınız. Gruplar, kullanıcılarınızı yönetmek ve çalışanlarınızın şirket kaynaklarınıza erişimini denetlemek için kullanılır. Bu kaynaklar şirketinizin intranetinin bir parçası veya SharePoint siteleri, SaaS uygulamaları ve web uygulamaları gibi dış kaynaklar olabilir.

Intune aboneliğiniz yoksa [ücretsiz deneme hesabı için kaydolun](free-trial-sign-up.md).

>[!NOTE]
>Intune size kolaylık sağlamak adına konsolda önceden oluşturulmuş ve yerleşik iyileştirmeleri bulunan **Tüm Kullanıcılar** ve **Tüm Cihazlar** gruplarını sağlar.

## <a name="prerequisites"></a>Önkoşullar

- Microsoft Intune Abonelik- [ücretsiz deneme hesabı için kaydolun](../fundamentals/free-trial-sign-up.md).
- Bu hızlı başlangıcı tamamlamak için [bir kullanıcı oluşturmanız](quickstart-create-user.md) gerekir.

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Microsoft uç nokta yöneticisinde Intune 'da oturum açma

[Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) [genel yönetici veya Intune Hizmet Yöneticisi](users-add.md#types-of-administrators)olarak oturum açın. Intune Deneme aboneliği oluşturduysanız aboneliği oluşturduğunuz hesap Genel yönetici rolüne sahip olur.

## <a name="create-a-group"></a>Grup oluşturma

Daha sonra bu hızlı başlangıç serisinde kullanılacak bir grup oluşturacaksınız. Bir grup oluşturmak için:

1. **Microsoft Uç Nokta Yöneticisi 'ni**açtıktan sonra **gruplar** > **Yeni Grup**' u seçin.
2. Açılan **Grup türü** kutusunda **Güvenlik**’i seçin.
3. **Grup adı** alanına yeni grup için bir ad girin (örneğin, **contoso Sınayıcılar**).
4. Grup için bir **Grup açıklaması** ekleyin.
5. **Üyelik türü**’nü **Atandı** olarak ayarlayın. 
6. **Üyeler**altında, bağlantıyı seçin ve listeden bir veya daha fazla üye ekleyin.

    ![Microsoft Intune'da grup oluşturma işleminin ekran görüntüsü](./media/quickstart-create-group/quickstart-use-groups-01.png)

7. Oluştur **Seç** > **Create**' e tıklayın.

Grup başarıyla oluşturulduğunda **Tüm gruplar** listesinde görünür. 

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta mevcut bir kullanıcıya dayanan bir grup oluşturmak için Intune kullanacaksınız. Intune’a grup ekleme hakkında daha fazla bilgi için bkz. [Kullanıcıları ve cihazları düzenlemek için grup ekleme](groups-add.md).

Bu Intune hızlı başlangıç serisini takip etmek için bir sonraki hızlı başlangıca ilerleyin.

> [!div class="nextstepaction"]
> [Hızlı Başlangıç: Windows 10 cihazları için otomatik kaydı ayarlama](../enrollment/quickstart-setup-auto-enrollment.md)
