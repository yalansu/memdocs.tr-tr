---
title: Microsoft Intune kullanarak macOS cihazlarına Office 365 uygulamalarını yüklemeyin
titleSuffix: ''
description: macOS cihazlarında Office 365 uygulamalarını yüklemek için Microsoft Intune’u nasıl kullanabileceğinizi öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2372332a-7e3a-4a9c-91a9-86654e0fabe2
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14a4d66cfd5ac0ee3c0938e96794ed12d5b5fde6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989509"
---
# <a name="assign-office-365-to-macos-devices-with-microsoft-intune"></a>Microsoft Intune ile macOS cihazlara Office 365 atama

Bu uygulama türü, macOS cihazlara Office 365 2016 uygulamaları atamanızı kolaylaştırır. Bu uygulama türünü kullanarak Word, Excel, PowerPoint, Outlook, OneNote ve takımlar yükleyebilirsiniz. Uygulamaların daha güvende ve güncel tutulabilmesi amacıyla uygulamalar, Microsoft AutoUpdate (MAU) ile gelir. Intune konsolundaki uygulamalar listesinde tek bir uygulama olarak görüntülenmesini istediğiniz uygulamalar.

> [!NOTE]
> Microsoft Office 365 ProPlus, **enterprise Microsoft 365 Apps**olarak yeniden adlandırıldı. Belgelerimizde, yaygın olarak **Microsoft 365 uygulamalar**olarak başvuracağız.

## <a name="before-you-start"></a>Başlamadan önce

MacOS cihazlarına Office 365 uygulamaları eklemeye başlamadan önce aşağıdaki ayrıntıları anlayın:

- Bu uygulamaları dağıtacağınız cihazların macOS 10.10 veya üzerini çalıştırıyor olması gerekir.
- Intune yalnızca Office Mac 2016 paketindeki Office uygulamalarının eklenmesini destekler.
- Intune uygulama paketini yüklerken herhangi bir Office uygulaması açıksa kaydedilmeyen dosyalardaki veriler kaybedilebilir.

## <a name="select-microsoft-365-apps"></a>Microsoft 365 uygulamaları seçin

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **tüm uygulamalar**  >  **Ekle**' yi seçin.
3. **Uygulama türü seç** bölmesinin **Microsoft 365 uygulamalar** bölümünde **MacOS** ' u seçin.
4. 4. **Seç**' e tıklayın. **Microsoft 365 ekleme uygulamaları** adımları görüntülenir.

## <a name="step-1---app-suite-information"></a>1. adım-uygulama paketi bilgileri

Bu adımda, uygulama paketi hakkında bilgi sağlarsınız. Bu bilgiler, Intune'da uygulama paketini bulmanıza yardımcı olur ve kullanıcıların Şirket Portalı'nda paketi bulması kolaylaşır.

1. **Uygulama paketi bilgileri** sayfasında, varsayılan değerleri onaylama veya değiştirme yapabilirsiniz:
    - **Paket Adı**: Uygulama paketinin Şirket Portalı’nda görüntülenen adını girin. Kullandığınız tüm paket adlarının benzersiz olduğundan emin olun. Aynı uygulama paketi adı iki kez kullanılmışsa uygulamalardan yalnızca biri şirket portalında kullanıcılara görüntülenir.
    - **Paket Açıklaması**: Uygulama paketi için bir açıklama girin. Örneğin dahil etmek üzere seçtiğiniz uygulamaları listeleyebilirsiniz.
    - **Yayımcı**: Yayımcı olarak Microsoft gösterilir.
    - **Kategori**: isteğe bağlı olarak, yerleşik uygulama kategorilerinden birini veya oluşturduğunuz bir kategoriyi seçin. Bu ayar, kullanıcıların şirket portalına göz atarken uygulama paketlerini daha kolay bulabilmesini sağlar.
    - **Bunu şirket portalı öne çıkan uygulama olarak göster**: kullanıcılar uygulamalara gözatarken, uygulama paketini Şirket portalının ana sayfasında göze çarpacak şekilde görüntülemek için bu seçeneği belirleyin.
    - **Bilgi URL’si**: İsteğe bağlı olarak, bu uygulama hakkında bilgi içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Gizlilik URL’si**: İsteğe bağlı olarak, bu uygulamayla ilgili gizlilik bilgilerini içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Geliştirici**: Geliştirici olarak Microsoft gösterilir.
    - **Sahip**: Sahip olarak Microsoft gösterilir.
    - **Notlar**: Bu uygulamayla ilişkilendirmek istediğiniz notları girin.
    - **Logo**: kullanıcılar şirket portalına gözatarken uygulamayla birlikte Microsoft 365 Apps logosu görüntülenir.
2. **İleri** ' ye tıklayarak **kapsam etiketleri** sayfasını görüntüleyin.

## <a name="step-2---select-scope-tags-optional"></a>2. adım-kapsam etiketlerini seçin (isteğe bağlı)
Intune 'da istemci uygulama bilgilerini kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).

1. **Kapsam etiketlerini Seç** ' e tıklayarak uygulama paketi için isteğe bağlı olarak kapsam etiketleri ekleyin. 
2. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.

## <a name="step-3---assignments"></a>3. adım-atamalar

1. Uygulama paketi için, **Kayıtlı cihazlar** grubu atamalarını **gerekli** veya kullanılabilir olarak seçin. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md) ve [Microsoft Intune olan gruplara uygulama atama](apps-deploy.md).

    >[!Note]
    > ' Microsoft 365 for macOS ' uygulama paketini Intune aracılığıyla kaldıramazsınız.

2. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin. 

## <a name="step-4---review--create"></a>4. adım-Inceleme ve oluşturma

1. Uygulama paketi için girdiğiniz değerleri ve ayarları gözden geçirin.
2. İşiniz bittiğinde, uygulamayı Intune 'a eklemek için **Oluştur** ' a tıklayın.

    **Genel bakış** dikey penceresi görüntülenir. Paket, uygulama listesinde tek bir girdi olarak gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

- Windows 10 cihazlarına Office 365 uygulamaları ekleme hakkında bilgi edinmek için, bkz. [Microsoft Intune Ile Windows 10 cihazlarına Microsoft 365 uygulamaları atama](apps-add-office365.md).
- Kullanıcı gruplarında uygulama atamalarını dahil etme ve dışlama hakkında bilgi edinmek için, bkz. [Uygulama atamalarını dahil etme ve dışlama](apps-inc-exl-assignments.md).
