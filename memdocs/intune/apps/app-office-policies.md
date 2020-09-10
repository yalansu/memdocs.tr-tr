---
title: Office uygulamalarına yönelik ilkeler
titleSuffix: Microsoft Intune
description: Office uygulamaları için kullanılabilen ilkeleri anlayın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644016"
---
# <a name="policies-for-office-apps"></a>Office uygulamalarına yönelik ilkeler

Intune, özellikle Microsoft Office uygulamalar için ilkeler sağlar. Microsoft 365 hizmetlerine bağlanan Office mobil uygulamaları için mobil uygulama yönetimi ilkeleri oluşturmak üzere belirli seçenekleri belirleyebilirsiniz. Office uygulamaları için Microsoft Intune ekleyebileceğiniz ve son kullanıcı gruplarına uygulayabileceğiniz birçok ilke vardır.

Office uygulaması ilkelerinin yalnızca birkaçını aşağıda verilmiştir:
- Microsoft Word: *Outlook 'tan açılan ekler Için korumalı görünümü* kapat
- Microsoft Visio: *makroları Internet 'Ten Office dosyalarında çalıştırmayı engelle*
- Microsoft Project: *ağ üzerinde güvenilen konumlara Izin ver*
- Microsoft Publisher: *Yayımcı Otomasyonu güvenlik düzeyi*
- Microsoft PowerPoint: *Outlook 'tan açılan eklerle Ilgili korumalı görünümü* kapat

> [!NOTE]
> Belirli bir uygulama ilkesini yapılandırmayı seçtiğinizde, ek ilke ayrıntıları sağlanır. Önerilen **güvenlik temeli** ilkelerini hızlıca seçmek için Office ilkesi listesini filtreleyebilirsiniz.

İOS için Outlook ve karma modern kimlik doğrulamasıyla etkinleştirilmiş Android için Intune uygulama koruma ilkeleri oluşturarak şirket içi Exchange posta kutularına erişimi de koruyabilirsiniz. Bu özelliği kullanmadan önce, Office bulut ilkesi hizmetini kullanma gereksinimlerini karşılamanız gerekir. Uygulama koruma ilkeleri, şirket içi Exchange veya SharePoint hizmetlerine bağlanan diğer uygulamalar için desteklenmez. İlgili bilgiler için bkz. [Enterprise için Microsoft 365 uygulamaları Için Office bulut İlkesi Hizmeti 'Ne genel bakış](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).

## <a name="prerequisites"></a>Önkoşullar

Office uygulamalarına yönelik ilkeleri kullanmak için gereksinimleri karşılamanız gerekir. Daha fazla bilgi için bkz. [Office bulut ilkesi hizmetini kullanma gereksinimleri](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service).

## <a name="to-add-an-office-app-policy"></a>Office uygulama ilkesi eklemek için

Kuruluşunuz için Intune 'u ayarladıktan sonra bir Office uygulama ilkesi oluşturabilirsiniz.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Apps**  >  **Office uygulamaları oluşturmak için uygulama ilkeleri**' ni seçin  >  **Create**.
3. Aşağıdaki değerleri ekleyin:
    - **Adı:** Yeni ilkeniz için bir ad yazın (gereklidir).
    - **Açıklama:** (İsteğe bağlı) Bir açıklama yazın.
    - **Tür seçin:** Bu ilke yapılandırmasının nasıl uygulanacağını seçin.
    - **Grup seçin:** Bu ilke yapılandırması için grubu seçin.
    - **Ilkeleri Yapılandır:** Uygulamak istediğiniz Office ilkesini seçin. Belirtilen listeyi ilke, Platform, uygulama, öneri ve duruma göre sıralayabilirsiniz.
4. **Oluştur**’u seçin. İlke oluşturulur ve **ilke yapılandırması** bölmesindeki tabloda görüntülenir.

   > [!TIP]
   > **İlke konfigürasyonları** bölmesi, her Ilke için **sistem durumunu** sağlar.

## <a name="additional-information"></a>Ek bilgiler

- [Enterprise için Microsoft 365 uygulamaları için Office bulut ilkesi hizmetine genel bakış](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [Kuruluş için Microsoft 365 uygulamalar için gizlilik denetimlerini yönetmek üzere ilke ayarlarını kullanma](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [Mac için Office gizlilik denetimlerini yönetmek için tercihleri kullanma](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [İOS cihazlarda Office için gizlilik denetimlerini yönetmek için tercihleri kullanma](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [Android cihazlarda Office için gizlilik denetimlerini yönetmek üzere ilke ayarlarını kullanma](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme](apps-monitor.md)