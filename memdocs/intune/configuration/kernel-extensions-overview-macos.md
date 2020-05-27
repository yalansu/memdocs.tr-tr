---
title: Microsoft Intune-Azure ile macOS sistemi ve çekirdek uzantıları oluşturma | Microsoft Docs
titleSuffix: ''
description: Kullanıcı geçersiz kılmasına izin vermek için sistem uzantıları veya çekirdek uzantıları yapılandıran bir macOS cihaz profili ekleyin veya oluşturun, takım tanımlayıcısı ekler ve Microsoft Intune bir paket ve takım tanımlayıcısı ekler.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990293"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>Intune 'da macOS sistemi ve çekirdek uzantıları ekleme

> [!NOTE]
> macOS çekirdek uzantıları sistem uzantıları ile değiştiriliyor. Daha fazla bilgi için bkz. [destek İpucu: Intune 'Da macOS Catalina 10,15 için çekirdek uzantıları yerine sistem uzantılarını kullanma](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

MacOS cihazlarında, çekirdek uzantıları ve sistem uzantıları ekleyebilirsiniz. Her iki çekirdek uzantısı ve sistem uzantısı, kullanıcıların işletim sisteminin yerel yeteneklerini genişleten uygulama uzantılarını yüklemelerine izin verir. Çekirdek uzantıları kendi kodlarını çekirdek düzeyinde yürütür. Sistem uzantıları, sıkı denetimli bir kullanıcı alanında çalışır.

Cihazlarınızda her zaman yüklenmesine izin verilen uzantıları eklemek için Microsoft Intune kullanın. Intune, kuruluşunuzun ihtiyaçlarına göre bu ayarları oluşturmak ve özelleştirmek için "yapılandırma profillerini" kullanır. Bu özellikleri bir profile ekledikten sonra, profili kuruluşunuzdaki macOS cihazlarına gönderirsiniz veya dağıtırsınız.

Bu makalede sistem uzantıları ve çekirdek uzantıları açıklanmaktadır. Ayrıca Intune 'da uzantıları kullanarak bir cihaz yapılandırma profili oluşturmayı gösterir.

## <a name="system-extensions"></a>Sistem uzantıları

Sistem uzantıları Kullanıcı alanında çalışır ve çekirdeğe erişemez. Amaç, güvenliği artırmaktır, daha fazla Son Kullanıcı denetimi sağlar ve çekirdek düzeyi saldırılarını sınırlar. Bu uzantılar şunları yapabilir:

- Sürücüleri USB, ağ arabirim kartı (NIC), seri denetleyicileri ve insan arabirim cihazlarına (HID) dahil sürücü uzantıları
- İçerik filtreleri, DNS proxy 'leri ve VPN istemcileri dahil ağ uzantıları
- Uç nokta algılama, uç nokta yanıtı ve virüsten koruma dahil uç nokta güvenlik uzantıları

Sistem uzantıları, uygulamanın paketine dahildir ve uygulamadan yüklenir.

Sistem uzantıları hakkında daha fazla bilgi için bkz. [sistem uzantıları](https://developer.apple.com/documentation/systemextensions) (Apple 'ın Web sitesini açar).

## <a name="kernel-extensions"></a>Çekirdek uzantıları

Çekirdek uzantıları çekirdek düzeyinde özellikler ekler. Bu özellikler, işletim sisteminin normal programların erişememe bölümlerine erişir. Kuruluşunuz, bir uygulamada ve bir cihaz özelliğinde bulunmayan belirli gereksinimlere veya gereksinimlere sahip olabilir.

Örneğin, cihazınızı kötü amaçlı içeriğe karşı tarayan bir virüs tarama programı vardır. Bu virüs tarama programının çekirdek uzantısını Intune 'da izin verilen bir çekirdek uzantısı olarak ekleyebilirsiniz. Ardından, uzantıyı macOS cihazlarınıza "atayın".

Yöneticiler, bu özellik ile kullanıcıların çekirdek uzantılarını geçersiz kılmasına, takım tanımlayıcıları eklemesine ve Intune 'A belirli çekirdek uzantıları eklemesine izin verebilir.

Çekirdek uzantıları hakkında daha fazla bilgi için bkz. [Kernel Extensions](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (Apple 'ın Web sitesini açar).

## <a name="prerequisites"></a>Ön koşullar

- Bu özellik şu platformlarda geçerlidir:

  - macOS 10.13.2 ve üzeri (çekirdek uzantıları)
  - macOS 10,15 ve üzeri (sistem uzantıları)

  MacOS 10,15 ' den 10.15.4, çekirdek uzantıları ve sistem uzantıları yan yana çalışabilir.

- Bu özelliği kullanmak için cihazların şu olması gerekir:

  - Apple 'ın Aygıt Kayıt Programı (DEP) kullanılarak Intune 'A kayıtlı. [MacOS cihazlarının otomatik olarak kaydedilmesi](../enrollment/device-enrollment-program-enroll-macos.md) daha fazla bilgi içerir.

    OR

  - "Kullanıcı onaylı kayıt" (Apple 'ın dönemi) ile Intune 'A kaydolmuş. [MacOS High Sierra içindeki çekirdek uzantılarında değişikliklere hazırlanma](https://support.apple.com/en-us/HT208019) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

## <a name="what-you-need-to-know"></a>Bilmeniz gerekenler

- İmzasız eski çekirdek uzantıları ve sistem uzantıları eklenebilir.
- Uzantının doğru takım tanımlayıcısını ve paket KIMLIĞINI girdiğinizden emin olun. Intune girdiğiniz değerleri doğrulamaz. Yanlış bilgi girerseniz, uzantı cihazda çalışmaz. Bir takım tanımlayıcısı, tam olarak 10 alfasayısal karakter uzunluğundadır.

> [!NOTE]
> Apple tüm yazılımlar için imzalama ve imza hakkında bilgi yayımladı. MacOS 10.14.5 ve daha yeni sürümlerde, Intune aracılığıyla dağıtılan çekirdek uzantıları Apple 'ın önemli ilkesini karşılamak zorunda kalmaz.
>
> Bu ilke ve tüm güncelleştirmeler veya değişiklikler hakkında bilgi için aşağıdaki kaynaklara bakın:
>
> - [Dağıtıma başlamadan önce uygulamanızı yeniden dağıtma](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (Apple 'ın Web sitesini açar) 
> - [MacOS High Sierra içindeki çekirdek uzantılarında değişikliklere hazırlanma](https://support.apple.com/en-us/HT208019) (Apple 'ın Web sitesini açar)

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **MacOS** seçin
    - **Profil**: **uzantıları**seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **MacOS: cihazlarda çekirdek uzantılarına virüsten koruma taraması ekleme**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda ayarlarınızı yapılandırın:

    - [macOS](kernel-extensions-settings-macos.md)

8. **İleri**’yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak kullanıcıları veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduktan sonra atanmak için hazırlanın. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).
