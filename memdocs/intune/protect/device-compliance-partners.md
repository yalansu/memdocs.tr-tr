---
title: Microsoft Intune-Azure 'da cihaz uyumluluk iş ortakları | Microsoft Docs
description: Intune ile yönettiğiniz cihazlar için uyumluluk verilerinin kaynağı olarak bir üçüncü taraf cihaz uyumluluk ortağı kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643712"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Intune 'da üçüncü taraf cihaz uyumluluk iş ortaklarını destekleme

Microsoft Intune, bir veya daha fazla üçüncü taraf cihaz uyumluluk iş ortaklarıyla yönettiğiniz cihazlar için uyumluluk durumu verilerini Azure Active Directory (Azure AD) ekleyebilir. Bu yapılandırmayla, bu cihazlardan gelen uyumluluk verileri koşullu erişim ilkeleriniz ile kullanılabilir.

Varsayılan olarak, Intune, cihazlarınız için mobil cihaz yönetimi (MDM) yetkilisi olarak ayarlanır. Azure AD ve Intune 'a bir uyumluluk ortağı eklediğinizde, bu ortağın bir Azure AD Kullanıcı grubu üzerinden bu iş ortağına atadığınız cihazlar için bir mobil cihaz yönetimi (MDM) yetkilisi kaynağı olacak şekilde yapılandırılıyorsunuz demektir.

Cihaz uyumluluk ortaklarından veri kullanımını etkinleştirmek için aşağıdaki görevleri doldurun:

1. **Intune 'u cihaz uyumluluk ortağıyla çalışacak şekilde yapılandırın**ve ardından cihazları bu uyumluluk ortağı tarafından yönetilen Kullanıcı gruplarını yapılandırın.

2. **Uyumluluk ortağınızı Intune 'a veri gönderecek şekilde yapılandırın**.

3. **İOS veya Android cihazlarınızı bu cihaz uyumluluk ortağına kaydedin**.

Bu görevler tamamlandıktan sonra, cihaz uyumluluk ortağı cihaz durumu ayrıntılarını Intune 'a gönderir. Intune daha sonra bu bilgileri Azure AD 'ye ekler. Örneğin, uyumlu olmayan bir duruma sahip cihazlar, bu durumun Azure AD 'deki cihaz kaydına eklenmesini sağlar.

Uyumluluk durumu daha sonra, Intune tarafından yönetilen cihazlar için uyumluluk durumu verileriyle aynı olan koşullu erişim ilkeleri tarafından değerlendirilir.  Varsayılan olarak, Intune, iOS ve Android için kayıtlı bir uyumluluk iş ortağıdır. Ek iş ortakları eklediğinizde, cihazı iş gereksinimlerinize uyacak şekilde doğru iş ortağının yönettiğinden emin olmak için öncelik sırasını ayarlayabilirsiniz.

## <a name="supported-device-compliance-partners"></a>Desteklenen cihaz uyumluluk iş ortakları

Genel önizlemede:

- VMware çalışma alanı BIR UEM (eski adıyla AirWatch)

## <a name="prerequisites"></a>Ön koşullar

- [Microsoft Endpoint Manager yönetim merkezine](https://go.microsoft.com/fwlink/?linkid=2109431)Microsoft Intune ve erişim için bir abonelik.

- Cihaz uyumluluk ortağı için bir abonelik.

- Desteklenen cihaz platformları ve ek önkoşullar için uyumluluk iş ortağınızla ilgili belgeleri gözden geçirin.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Intune 'U cihaz uyumluluk ortağıyla çalışacak şekilde yapılandırma

Koşullu erişim ilkeleriniz ile bu iş ortağından uyumluluk durumu verilerini kullanmak için bir cihaz uyumluluk ortağının desteğini etkinleştirin.

### <a name="add-a-compliance-partner-to-intune"></a>Intune 'a uyumluluk ortağı ekleme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **iş ortağı Uyumluluk Yönetimi**  >  **Uyumluluk ortağı Ekle**' ye gidin.

   > [!div class="mx-imgBorder"]
   > ![Cihaz uyumluluk ortağı ekleme](./media/device-compliance-partners/add-compliance-partner.png)

3. **Temel bilgiler** sayfasında, **Uyumluluk ortağı** açılır ' i genişletin ve eklemekte olduğunuz iş ortağını seçin.

   - VMware çalışma alanını iOS veya Android platformları için uyumluluk ortağı olarak kullanmak için, **VMware çalışma alanını tek bir mobil uyumluluk**' i seçin.

   Ardından, **Platform**için açılan eklentiyi seçin ve platformu seçin. macOS bu önizleme ile desteklenmiyor.

   Azure AD 'ye birden çok uyumluluk iş ortağı eklemiş olsanız bile, her platform için tek bir iş ortağıyla sınırlı olursunuz.

4. **Atamalar**' da, bu iş ortağı tarafından yönetilecek cihazları olacak Kullanıcı gruplarını seçin. Bu atamayla ilgili cihazlar için MDM yetkilisini bu iş ortağını kullanacak şekilde değiştirirsiniz. İş ortağı tarafından yönetilen cihazlara sahip kullanıcılara ayrıca bir Intune lisansı atanmalıdır.

5. **Gözden geçir + oluştur** sayfasında, seçimlerinizi gözden geçirin ve ardından **Oluştur** ' u seçerek bu yapılandırmayı doldurun.

Yapılandırmanız artık Iş ortağı Uyumluluk Yönetimi sayfasında görüntülenir.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Uyumluluk ortağının yapılandırmasını değiştirme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **iş ortağı Uyumluluk Yönetimi**' ne gidin ve ardından değiştirmek istediğiniz iş ortağı yapılandırmasını seçin. Konfigürasyonlar platform türüne göre sıralanır.

3. İş ortağı yapılandırmasına **genel bakış** sayfasında, atamaları düzenleyebileceğiniz Özellikler sayfasını açmak için **Özellikler** ' i seçin.

4. **Özellikler** sayfasında, bu yapılandırmayı kullanacak grupları değiştirebileceğiniz atamalar görünümünü açmak için **Düzenle** ' yi seçin.

5. **Gözden geçir + kaydet** ' i ve ardından değişikliklerinizi kaydetmek için **Kaydet** ' i seçin.

6. *Bu adım yalnızca VMware çalışma alanını bir tane kullandığınızda geçerlidir*:

   Çalışma alanı BIR UıEM konsolunun içinden, Microsoft Endpoint Manager Yönetim merkezinde kaydettiğiniz değişiklikleri el ile eşitlemeniz gerekir. Değişiklikleri el ile eşitleene kadar, çalışma alanı yapılandırma değişikliklerinin farkında değildir ve atadığınız yeni gruplardaki kullanıcılar uyumluluğu başarıyla raporlamaz.

   Azure hizmetlerinden el ile eşitleme yapmak için:
   1. VMware çalışma alanınızda BIR UıEM konsolunda oturum açın.
   2. **Ayarlar**  >  **sistem**  >  **kurumsal tümleştirme**  >  **Dizin Hizmetleri**' ne gidin.
   3. *Azure hizmetlerini eşitleme*için **Eşitle**' ye tıklayın.

      İlk yapılandırmadan veya son el ile eşitlemeden bu yana yaptığınız tüm değişiklikler Azure hizmetlerinden UEM 'ye eşitlenir.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Uyumluluk ortağınızı Intune ile çalışacak şekilde yapılandırma

Bir cihaz uyumluluk ortağının Intune ile çalışmasını sağlamak için, bu iş ortağına özgü olan konfigürasyonları tamamlamalısınız. Bu görevle ilgili bilgi için, ilgili iş ortağı için belgelere bakın:

- [VMware çalışma alanı BIR UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>İOS veya Android cihazlarınızı bu cihaz uyumluluk ortağına kaydetme

Cihazları bu iş ortağıyla kaydetme hakkında bilgi için cihaz uyumluluk iş ortakları belgelerine bakın. Cihazlar kaydedildikten ve uyumluluk verilerini ortağa gönderdikten sonra, bu uyumluluk verileri Intune 'a iletilir ve Azure AD 'ye eklenir.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Üçüncü taraf cihaz uyumluluk iş ortakları tarafından yönetilen cihazları izleme

Üçüncü taraf cihaz uyumluluk iş ortaklarını yapılandırdıktan ve cihazları bunlara kaydettikten sonra, iş ortağı uyumluluk ayrıntılarını Intune 'a iletir. Intune bu verileri aldıktan sonra Azure portal cihazlarla ilgili ayrıntıları görüntüleyebilirsiniz.

Azure Portal oturum açın ve **Azure AD**  >  **cihazlar**  >  [**tüm cihazlar**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/)' a gidin.

## <a name="next-steps"></a>Sonraki adımlar

Cihazlar için uyumluluk ilkeleri oluşturmak üzere üçüncü taraf iş ortağınızdan belgeleri kullanın.

- [VMware çalışma alanı BIR UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
