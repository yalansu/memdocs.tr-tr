---
title: Uygulamalardan yalnızca şirket verilerini temizleme
titleSuffix: Microsoft Intune
description: Microsoft Intune ile yalnızca şirket verilerini Intune tarafından yönetilen uygulamalardan seçerek silmeyi öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 42605e6e-5b84-44ff-b86e-346ea123b53e
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1640928bfb1ca27d4ee72e014adad88db0976a2d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078354"
---
# <a name="how-to-wipe-only-corporate-data-from-intune-managed-apps"></a>Intune tarafından yönetilen uygulamalardan kurumsal verileri temizleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Cihaz kaybolduğunda veya çalındığında ya da çalışan şirketten ayrıldığında, şirket uygulama verilerinin cihazdan kaldırıldığından emin olmak istersiniz. Ancak özellikle cihaz çalışana aitse kişisel verilerin kaldırılmasını istemeyebilirsiniz.

>[!NOTE]
> İOS/ıpados, Android ve Windows 10 platformları şu anda Intune tarafından yönetilen uygulamalardan şirket verilerini silmek için desteklenen platformlardır. Intune ile yönetilen uygulamalar, Intune uygulama SDK 'sını içeren ve kuruluşunuz için lisanslı bir kullanıcı hesabına sahip olan uygulamalardır. Uygulama koruma Ilkelerinin dağıtımı, uygulama seçmeli silme özelliğini etkinleştirmek için gerekli değildir.

Şirket uygulaması verilerini seçmeli olarak silmek için bu konu başlığındaki adımları kullanarak bir silme isteği oluşturun. İstek tamamlandıktan sonra, uygulama cihaz üzerinde ilk kez çalıştığında şirket verileri uygulamadan kaldırılır. Silme isteğine ek olarak, Uygulama Koruma İlkeleri (APP) Erişim ayarlarının koşullarına uyulmadığında yeni bir eylem olarak kuruluşunuzun verilerinin seçmeli silinmesini yapılandırabilirsiniz. Bu özellik, önceden yapılandırılmış ölçütler temelinde hassas kuruluş verilerini otomatik olarak korumanıza ve uygulamalardan kaldırmanıza yardımcı olur.

>[!IMPORTANT]
> Uygulamadan yerel adres defterine doğrudan eşitlenen kişiler kaldırılır. Yerel adres defterinden başka bir dış kaynağa eşitlenen kişiler silinemez. Şu anda bu özellik yalnızca Microsoft Outlook uygulaması için geçerlidir.

## <a name="deployed-wip-policies-without-user-enrollment"></a>Kullanıcı kaydı olmadan dağıtılan WIP ilkeleri 
Windows Information Protection (WıP) ilkeleri, MDM kullanıcılarının Windows 10 cihazını kaydetmesine gerek kalmadan dağıtılabilir. Bu yapılandırma, kullanıcıların Windows cihazlarının yönetimini sürdürmesini sağlarken şirketlerin de kurumsal belgelerini WIP yapılandırmasına göre korumasını sağlar. Belgeler bir WıP ilkesiyle korunduktan sonra, korunan veriler bir Intune Yöneticisi ([genel yönetici veya Intune Hizmet Yöneticisi](../fundamentals/users-add.md#types-of-administrators)) tarafından seçmeli olarak silinebilir. Kullanıcı ve cihaz seçilerek ve bir silme isteği gönderilerek WIP İlkesi aracılığıyla korunan tüm veriler kullanılamaz hale getirilir. Azure Portal Intune 'da, **istemci uygulama** > **uygulaması seçmeli silme**' yi seçin. Daha fazla bilgi için bkz. [Intune ile Windows Bilgi Koruması (WIP) uygulama koruma ilkesi oluşturma ve dağıtma](windows-information-protection-policy-create.md).

## <a name="create-a-device-based-wipe-request"></a>Cihaz tabanlı silme isteği oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar** > **uygulaması seçmeli silme** > **silme isteği oluştur**' u seçin.<br>
   **Temizleme Isteği oluştur** bölmesi görüntülenir.
3. **Kullanıcı Seç**' e tıklayın, uygulama verilerini silmek istediğiniz kullanıcıyı seçin ve **Kullanıcı Seç** bölmesinin en altında bulunan **Seç** ' e tıklayın.

    ![' Kullanıcı Seç ' bölmesinin ekran görüntüsü](./media/apps-selective-wipe/apps-selective-wipe-01.png)

4. **Cihazı seç**' e tıklayın, cihazı seçin ve **cihaz Seç** bölmesinin en altında bulunan **Seç** ' e tıklayın.

    ![Cihazın seçildiği ' temizleme isteği oluştur ' bölmesinin ekran görüntüsü](./media/apps-selective-wipe/apps-selective-wipe-02.png)

5. Silme isteği **oluşturmak Için oluştur** ' a tıklayın.

Hizmet, cihazdaki korunan her uygulama için ayrı bir silme isteği oluşturur ve bu isteklerle temizleme isteği ile ilişkilendirilmiş kullanıcıyı izler.

   ![' Istemci uygulamalar-uygulama seçmeli silme ' bölmesinin ekran görüntüsü](./media/apps-selective-wipe/apps-selective-wipe-03.png)

## <a name="create-a-user-based-wipe-request"></a>Kullanıcı tabanlı silme isteği oluştur

Kullanıcı düzeyi temizlemeye Kullanıcı ekleyerek, tüm Kullanıcı cihazlarındaki tüm uygulamalara otomatik olarak temizleme komutları yayınlarız.  Kullanıcı tüm cihazlardan her iadede Temizleme komutlarını almaya devam edecektir.  Bir kullanıcıyı yeniden etkinleştirmek için bunları listeden kaldırmanız gerekir.  

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar** > **uygulaması seçmeli silme** > **silme isteği oluştur**' u seçin.<br>
   **Kullanıcı düzeyinde silme** seçin
3. **Ekle** ' ye tıklayın ve Kullanıcı bölmesi görüntülenir ' i **seçin** .
4. Uygulama verilerini silmek istediğiniz kullanıcıyı **seçin ve Seç**' e tıklayın.

## <a name="monitor-your-wipe-requests"></a>Silme isteklerinizi izleme

Temizleme isteğinin genel durumunu gösteren ve bekleyen isteklerle hataların sayısını içeren bir özet raporunuz olabilir. Daha fazla bilgi almak için şu adımları izleyin:

1. **Uygulamalar** > **uygulaması seçmeli silme** bölmesinde, isteklerinizin kullanıcılara göre gruplandırılmış listesini görebilirsiniz. Sistem, cihazda çalışan her korumalı uygulama için bir temizleme isteği oluşturduğundan, bir kullanıcı için birden çok istek görebilirsiniz. Durum, temizleme isteğinin **bekliyor**, **başarısız** veya **başarılı** olup olmadığını gösterir.

    ![Uygulama seçmeli silme bölmesinde temizleme isteği durumunun ekran görüntüsü](./media/apps-selective-wipe/wipe-request-status-1.png)

Buna ek olarak, cihaz adını ve cihaz türünü görebilirsiniz; bunlar raporları okurken yararlı olabilir.

>[!IMPORTANT]
> Silmenin gerçekleşmesi için kullanıcı uygulamayı açmalıdır ve silme işlemi, istekte bulunulduktan sonra 30 dakikaya kadar zaman alabilir.

## <a name="delete-a-device-wipe-request"></a>Bir cihaz silme isteğini silme

Bekleme durumundaki silmeler, siz bunları elle silinceye kadar görüntülenir. Temizleme isteğini el ile silmek için:

1. **İstemci Uygulamalar - Uygulama seçmeli silme** bölmesinde.

2. Listede silmek istediğiniz temizleme isteğine sağ tıklayın ve **Temizleme isteğini sil**’i seçin.

    ![Uygulama seçmeli silme bölmesinde temizleme isteği listesinin ekran görüntüsü](./media/apps-selective-wipe/delete-wipe-request.png)

3. Silme işlemini onaylamanız istenir; **Evet** veya **Hayır**’ı seçin, sonra da **Tamam**’a tıklayın.

## <a name="delete-a-user-wipe-request"></a>Kullanıcı Temizleme isteğini silme

Kullanıcı silinince, yönetici tarafından kaldırılana kadar listede kalır. Bir kullanıcıyı listeden kaldırmak için:

1. **Istemci uygulamaları-uygulama seçmeli silme** bölmesinde **Kullanıcı düzeyinde silme ' yi** seçin
2. Listeden, silmek istediğiniz kullanıcıya sağ tıklayın ve **Sil**' i seçin. 


## <a name="see-also"></a>Ayrıca bkz.
[Uygulama koruma ilkesi nedir](app-protection-policy.md)

[Uygulama yönetimi nedir](app-management.md)
