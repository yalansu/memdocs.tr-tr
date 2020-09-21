---
title: Microsoft Intune-Azure 'da macOS uzantı ayarları | Microsoft Docs
titleSuffix: ''
description: System Extensions ve Kernel uzantıları kullanmak için macOS cihazlarında Ayarlar ekleyin, yapılandırın veya oluşturun. Ayrıca, kullanıcıların onaylanan uzantıları geçersiz kılmasına, bir takım tanımlayıcısından tüm uzantılara izin vermelerine veya Microsoft Intune içindeki belirli uzantılara veya uygulamalara izin erişmesine izin verin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f10a84415f42632b0a9d7b17829feb0b7c99d0a4
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815417"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>Intune 'da çekirdek ve sistem uzantılarını yapılandırmak ve kullanmak için macOS cihaz ayarları

> [!NOTE]
> macOS çekirdek uzantıları sistem uzantıları ile değiştiriliyor. Daha fazla bilgi için bkz. [destek İpucu: Intune 'Da macOS Catalina 10,15 için çekirdek uzantıları yerine sistem uzantılarını kullanma](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Bu makalede, macOS cihazlarında denetleyebilmeniz için farklı çekirdek ve sistem uzantısı ayarları listelenmektedir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, cihazlarınızda uzantıları eklemek ve yönetmek için bu ayarları kullanın.

Intune ve Önkoşullar hakkında daha fazla bilgi edinmek için bkz. [macOS uzantıları ekleme](kernel-extensions-overview-macos.md).

Bu ayarlar, Intune'da bir cihaz yapılandırma profiline eklenir ve daha sonra macOS cihazlarınıza atanır veya dağıtılır.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS uzantıları cihaz yapılandırma profili](kernel-extensions-overview-macos.md)oluşturun.

> [!NOTE]
> Bu ayarlar farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [MacOS kaydı](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Çekirdek uzantıları

Bu özellik şu platformlarda geçerlidir:

- macOS 10.13.2 ve üzeri
- Kullanıcı tarafından onaylanan cihaz kaydı gereklidir 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Ayarlar için geçerlidir: Kullanıcı tarafından onaylanan cihaz kaydı, otomatik cihaz kaydı

- **Kullanıcı geçersiz kılmalara Izin ver**: **Evet** seçeneği, kullanıcıların, yapılandırma profilinde bulunmayan çekirdek uzantılarını onaylamasını sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların yapılandırma profilinde bulunmayan uzantılara izin vermesini engelleyebilir. Anlamı olarak yalnızca yapılandırma profiline eklenen uzantılara izin verilir.

  Bu özellik hakkında daha fazla bilgi için bkz. [Kullanıcı onaylı çekirdek uzantısı yüklemesi](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (Apple 'ın Web sitesini açar).

- **Izin verilen takım tanımlayıcıları**: bir veya daha fazla takım kimliğine izin vermek için bu ayarı kullanın. Girdiğiniz ekip kimlikleriyle imzalanan tüm çekirdek uzantılarına izin verilir ve bunlar güvenilir. Diğer bir deyişle, belirli bir geliştirici veya iş ortağı olabilecek aynı takım KIMLIĞI içindeki tüm çekirdek uzantılarına izin vermek için bu seçeneği kullanın.

  Yüklenecek geçerli ve imzalı çekirdek uzantılarının ekip tanımlayıcısını **ekleyin** . Birden çok takım tanımlayıcısı ekleyebilirsiniz. Takım tanımlayıcısının alfasayısal (harfler ve rakamlar) olması ve 10 karaktere sahip olması gerekir. Örneğin, `ABCDE12345` girin.

  Ekip tanımlayıcı ekledikten sonra da silinebilir.

  [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

- **Izin verilen çekirdek uzantıları**: belirli çekirdek uzantılarına izin vermek için bu ayarı kullanın. Yalnızca girdiğiniz çekirdek uzantılarına izin verilir veya güvenilir.

  Yüklenecek çekirdek uzantısının paket tanımlayıcısını ve takım tanımlayıcısını **ekleyin** . İmzasız eski çekirdek uzantıları için boş bir takım tanımlayıcısı kullanın. Birden çok çekirdek uzantısı ekleyebilirsiniz. Takım tanımlayıcısının alfasayısal (harfler ve rakamlar) olması ve 10 karaktere sahip olması gerekir. Örneğin, `com.contoso.appname.macos` **paket kimliği**için ve `ABCDE12345` **Takım tanımlayıcısı**için girin.

  > [!TIP]
  > Bir macOS cihazında çekirdek uzantısının paket KIMLIĞINI (KEXT) almak için şunları yapabilirsiniz:
  >
  > 1. Terminalde çalıştırın `kextstat | grep -v com.apple` ve çıktıyı aklınızda yapın. İstediğiniz yazılımı veya KEXT 'yi yükler. `kextstat | grep -v com.apple`Yeniden çalıştırın ve değişiklikler olup olmadığına bakın.
  >
  >    Terminalde, `kextstat` işletim sistemindeki tüm çekirdek uzantılarını listeler. 
  >
  > 2. Cihazda, bir KEXT için bilgi özelliği liste dosyasını (Info. plist) açın. Paket KIMLIĞI gösterilir. Her bir KEXT içinde depolanan Info. plist dosyasına sahiptir.

> [!NOTE]
> Takım tanımlayıcıları ve çekirdek uzantıları eklemeniz gerekmez. Bir veya diğerini yapılandırabilirsiniz.

## <a name="system-extensions"></a>Sistem uzantıları

Bu özellik şu platformlarda geçerlidir:

- macOS 10,15 ve üzeri
- Kullanıcı tarafından onaylanan cihaz kaydı gereklidir

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Ayarlar için geçerlidir: Kullanıcı tarafından onaylanan cihaz kaydı, otomatik cihaz kaydı

- **Kullanıcı geçersiz kılmalarını engelle**: **Evet** seçeneği, kullanıcıların izin verilenler listesinde olmayan sistem uzantılarını onaylamayı engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların yapılandırma profilinde bulunmayan bilinmeyen uzantıları onaylamasını sağlayabilir. Anlamı, yapılandırma profiline dahil olmayan uzantılara izin verilir.

- **Izin verilen takım tanımlayıcıları**: bir veya daha fazla takım kimliğine izin vermek için bu ayarı kullanın. Girdiğiniz ekip kimlikleriyle imzalanan tüm sistem uzantılarına her zaman izin verilir ve güvenilir. Diğer bir deyişle, belirli bir geliştirici veya iş ortağı olabilecek aynı takım KIMLIĞI içindeki tüm sistem uzantılarına izin vermek için bu seçeneği kullanın.

  Yüklenecek geçerli ve imzalı sistem uzantılarının **ekip tanımlayıcısını** **ekleyin** . Birden çok takım tanımlayıcısı ekleyebilirsiniz. Takım tanımlayıcısının alfasayısal (harfler ve rakamlar) olması ve 10 karaktere sahip olması gerekir. Örneğin, `ABCDE12345` girin.

  Ekip tanımlayıcı ekledikten sonra da silinebilir.

  [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

- **Izin verilen sistem uzantıları**: Bu ayarı, belirli sistem uzantılarına her zaman izin vermek için kullanın. Yalnızca girdiğiniz sistem uzantılarına izin veriliyor veya güvenilir.

  Yüklenecek bir sistem uzantısının **paket tanımlayıcısını** ve **Takım tanımlayıcısını** **ekleyin** . İmzasız eski sistem uzantıları için boş bir takım tanımlayıcısı kullanın. Birden çok sistem uzantısı ekleyebilirsiniz. Takım tanımlayıcısının alfasayısal (harfler ve rakamlar) olması ve 10 karaktere sahip olması gerekir. Örneğin, `com.contoso.appname.macos` **paket kimliği**için ve `ABCDE12345` **Takım tanımlayıcısı**için girin.

- **Izin verilen sistem uzantısı türleri**: takım kimliği ve bu takım kimliği için izin verilecek sistem uzantısı türlerini girin:
  - **Takım tanımlayıcısı**: belirli uzantı türlerine izin vermek istediğiniz başka bir sistem UZANTıSıNıN takım kimliğini girin. Ya da **Izin verilen sistem uzantılarına**eklediğiniz BIR takım kimliği girin.
  - **Izin verilen sistem uzantısı türleri**: her takım kimliği için izin verilecek sistem uzantısı türlerini seçin. Seçenekleriniz şunlardır:
    - Tümünü seç
    - Sürücü uzantıları
    - Ağ uzantıları
    - Uç nokta güvenlik uzantıları

    Bu uzantı türleri hakkında daha fazla bilgi için bkz. [System Extensions](https://developer.apple.com/system-extensions/) (Apple 'ın Web sitesini açar).

    **Izin verilen sistem uzantıları** listesinden bır takım kimliği ekleyebilir ve belirli bir uzantı türüne izin verebilirsiniz. Uzantı izin verilmeyen bir tür ise, uzantı çalışmayabilir.

    Bir takım KIMLIĞI için tüm uzantı türlerine izin vermek üzere, takım KIMLIĞINI **Izin verilen sistem uzantıları** listesine ekleyin. Takım KIMLIĞINI **Izin verilen sistem uzantısı türleri** listesine eklemeyin. Diğer bir deyişle, bir takım KIMLIĞI izin verilen sistem **uzantıları** listesinde ise, izin verilen **sistem uzantısı türleri** listesinde DEĞILSE, bu takım kimliği için tüm uzantı türlerine izin verilir.

> [!NOTE]
> **Izin verilen sistem uzantıları** ve **izin verilen takım tanımlayıcıları** için aynı takım kimliğini eklemek hata ve profil başarısız olmasına neden olabilir. Aynı tam takım tanımlayıcısını her iki ayarı da eklemeyin. 

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).
