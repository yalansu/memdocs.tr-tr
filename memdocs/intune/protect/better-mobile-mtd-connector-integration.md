---
title: Intune ile Better Mobile tümleştirmesini ayarlama
titleSuffix: Intune on Azure
description: Intune ile Better Mobile bağlayıcısı tümleştirmesi
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6208c8f225cc3e54a61181960223f3f8cad8423d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989736"
---
# <a name="integrate-better-mobile-with-intune"></a>Better Mobile'ı Intune ile tümleştirme

Better Mobile Threat Defense çözümünü Intune ile tümleştirmek için aşağıdaki adımları tamamlayın.

## <a name="before-you-begin"></a>Başlamadan önce

Aşağıdaki adımlar [daha iyi bir mobil yönetici konsolunda](https://aad.bmobi.net) tamamlanacak ve Intune 'a kayıtlı cihazlar (cihaz uyumluluğu kullanılarak) ve kayıtlı olmayan cihazlar (uygulama koruma ilkeleri kullanılarak) Için daha Iyi bir mobil hizmete bağlantı sağlar.

Better Mobile'ı Intune ile tümleştirme sürecini başlatmadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- Microsoft Intune aboneliği

- Şu izinleri vermek için Azure Active Directory yönetici kimlik bilgileri:

  - Oturum açma ve kullanıcı profilini okuma

  - Dizine oturum açmış kullanıcı olarak erişin

  - Dizin verilerini oku

  - Intune’a cihaz bilgilerini gönderme

- Better Mobile yönetim konsoluna erişmek için yönetici kimlik bilgileri.

### <a name="better-mobile-app-authorization"></a>Better Mobile uygulama yetkilendirmesi

Better Mobile uygulama yetkilendirme işlemi şu şekildedir:

- Better Mobile hizmetine Intune'a cihazın sistem durumuyla ilgili bilgi iletme izni verme.

- Cihazının veritabanını doldurmak için Better Mobile'ı Azure AD Kayıt Grubu üyeliğiyle eşitleme.

- Better Mobile yönetim konsolunun Azure AD Çoklu Oturum Açma (SSO) kullanmasına izin verme.

- Better Mobile uygulamasının Azure AD SSO kullanarak oturum açmasına izin verme.

## <a name="to-set-up-better-mobile-integration"></a>Better Mobile tümleştirmesini ayarlamak için

1. [Better Mobile yönetim konsoluna](https://aad.bmobi.net) gidin ve kimlik bilgilerinizle oturum açın.
2. **Tümleştirme**  >  **EMM/MDM**  >  **hesabı ekle**' yi seçin.

     ![Daha Iyi mobil yönetici konsolunun görüntüsü](./media/better-mobile-mtd-connector-integration/better_mobile_console.png)

3. **Intune**'u seçin.
4. **ACCOUNT NAME** alanının yanına bir tanımlayıcı yazın.
5. **Microsoft Oturum Açma** penceresinde Intune kimlik bilgilerinizi girin.
6. **İstenen izinler** penceresinde **Kabul Et**'i seçin.
7. Better Mobile'ın cihazları hangi Azure AD Güvenlik gruplarından eşitlemesini istiyorsanız, o gruplar için arama yapın ve listeden bunları seçin. Daha sonra **Devam** seçeneğini belirleyin.
8. **Done** (Bitti) öğesini seçin.
9. **Hesap ekle** sayfası yeniden görüntülenir. Sayfayı kapatın.

## <a name="next-steps"></a>Sonraki adımlar

- [Kayıtlı cihazlar için daha Iyi mobil uygulamalar ayarlama](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Kayıtlı olmayan cihazlar için daha Iyi mobil uygulamalar ayarlama](mtd-add-apps-unenrolled-devices.md)
