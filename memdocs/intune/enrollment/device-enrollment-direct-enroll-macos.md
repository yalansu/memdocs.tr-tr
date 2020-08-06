---
title: MacOS cihazları için doğrudan kayıt kullanma
titleSuffix: Microsoft Intune
description: Doğrudan kayıt kullanarak macOS cihazlarını kaydetmeyi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819957"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>MacOS cihazları için doğrudan kayıt kullanma

Intune, macOS cihazlarının şirket cihazları için doğrudan kayıt (DE) kullanılarak kaydedilmesini destekler. Doğrudan kayıt, cihazı temizlemez. MacOS ayarları aracılığıyla cihazı kaydeder. Bu yöntem, yalnızca **kullanıcı benzeşimi olmayan** cihazları destekler.

## <a name="prerequisites"></a>Önkoşullar

- MacOS cihazlarına fiziksel erişim
- [MDM yetkilisini ayarlama](../fundamentals/mdm-authority-set.md)
- [Apple MDM anında iletme sertifikası](apple-mdm-push-certificate-get.md)
 - Kaydolan macOS cihazlarında yönetici hakları

## <a name="create-an-apple-configurator-profile-for-devices"></a>Cihazlar için Apple Configurator profili oluşturma

Bir cihaz kayıt profili kayıt sırasında uygulanan ayarları tanımlar. Bu ayarlar yalnızca bir kez uygulanır. MacOS cihazlarını doğrudan kayıtla kaydetmek üzere bir kayıt profili oluşturmak için bu adımları izleyin.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihazlar**  >  **kayıt cihazları**  >  **Apple kaydı**  >  **Apple Configurator**' ı seçin.

2. **Profil**  >  **Oluştur**' a tıklayın.

3. **Kayıt Profili Oluştur** altında yönetim amaçları doğrultusunda profil için bir **Ad** ve **Açıklama** girin. Kullanıcılar bu ayrıntıları göremez. Azure Active Directory’de dinamik bir grup oluşturmak için bu Ad alanını kullanabilirsiniz. enrollmentProfileName parametresini, bu kayıt profiliyle cihazlara atamak amacıyla tanımlamak için profil adını kullanın. Azure Active Directory dinamik grupları hakkında daha fazla bilgi edinin.

4. **Kullanıcı benzeşimi**Için **Kullanıcı benzeşimi olmadan kaydet** ' i seçin-tek bir kullanıcıyla bağlantılı olmayan cihazlar için bu seçeneği belirleyin. Yerel kullanıcı verilerine erişmeden görevleri yerine getiren cihazlar için bunu kullanın. Kullanıcı ilişkisi gerektiren uygulamalar (iş kolu uygulamalarını yüklemek için kullanılan Şirket Portalı uygulaması dahil) çalışmaz. Doğrudan kayıt için gereklidir.

     > [!NOTE]
     > **Kullanıcı benzeşimi Ile kaydolma** , doğrudan kayıt kullanılırken MacOS 'ta desteklenmez. Kullanıcı benzeşimi gerektiren cihazlar için otomatik cihaz kaydını kullanın.

6. **Oluştur**’u seçerek profili kaydedin.

## <a name="direct-enrollment"></a>Doğrudan Kayıt
Doğrudan kayıt yalnızca Kullanıcı benzeşimi olmadan kaydı desteklediğinden, Şirket portalı kullanılabilir uygulamaları yüklemek için kullanılamaz.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Profili dışarı aktarma ve macOS cihazlarına yüklemesi

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **cihazlar**  >  **kayıt cihazları**  >  **Apple kaydı**  >  **Apple Configurator**  >  **profilleri** ' ni seçin > > **dışarı aktarma profilini**dışarı aktarmak için profili seçin.
2. **Doğrudan kayıt** altında **Profil indir**’i seçin ve dosyayı kaydedin. 

     > [!NOTE]
     > İndirilen bir kayıt profili, indirme sonrasında iki hafta boyunca geçerlidir. Bu bağlantıyı kullanarak, ihtiyacınız olan sayıda kayıt profili indirebilirsiniz. Yeni bir profil indirildikten sonra bir önceki dosya işlenmeyecektir, ancak daha önce indirilen dosyanın sona erme saati de genişlemez.
         
3. Dosyayı doğrudan yüklemek için bir macOS bilgisayarına aktarın.
4. Dosyayı profillerde açmak için kaydedildi **. mobileconfig** dosyasına çift tıklayın.
5. Yönetim profilini yüklemek isteyip istemediğiniz sorulduğunda, **yüklemek**' ı seçin.
6. Bir sonraki istem üzerinde, yönetim profilini **yüklemek**istediğinizi seçerek bunu onaylayın.
7. MacOS cihazında bir yönetici hesabının kimlik bilgilerini girin ve **Tamam**' a tıklayın.
8. MacOS cihazı artık Intune 'A kayıtlı ve hedeflenen profiller indirmeye başlayacak.

## <a name="next-steps"></a>Sonraki adımlar

MacOS cihazlarını kaydettikten sonra, [bunları yönetmeye](../remote-actions/device-management.md)başlayabilirsiniz.