---
title: Microsoft Intune-Azure 'da cihaz uyumluluk iş ortakları | Microsoft Docs
description: Intune ile yönettiğiniz cihazlar için uyumluluk verilerinin kaynağı olarak bir üçüncü taraf cihaz uyumluluk ortağı kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/15/2020
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
ms.openlocfilehash: feaf07d6b01569bffe317bc765e638dd383c27ba
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091994"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Intune 'da üçüncü taraf cihaz uyumluluk iş ortaklarını destekleme

Microsoft Intune, bir veya daha fazla üçüncü taraf cihaz uyumluluk iş ortaklarıyla yönettiğiniz cihazlar için uyumluluk durumu verilerini Azure Active Directory (Azure AD) ekleyebilir. Bu yapılandırmayla, bu cihazlardan gelen uyumluluk verileri koşullu erişim ilkeleriniz ile kullanılabilir.

Varsayılan olarak, Intune, cihazlarınız için mobil cihaz yönetimi (MDM) yetkilisi olarak ayarlanır. Azure AD ve Intune 'a bir uyumluluk ortağı eklediğinizde, bu ortağın bir Azure AD Kullanıcı grubu üzerinden bu iş ortağına atadığınız cihazlar için bir mobil cihaz yönetimi (MDM) yetkilisi kaynağı olacak şekilde yapılandırılıyorsunuz demektir.

Cihaz uyumluluk ortaklarından veri kullanımını etkinleştirmek için aşağıdaki görevleri doldurun:

1. Bu iş ortağını ilgili cihazlar için bir mobil cihaz yönetimi (MDM) yetkilisi olarak belirlemek için **Azure AD 'ye cihaz uyumluluk ortağını ekleyin** .

2. **Intune 'u cihaz uyumluluk ortağıyla çalışacak şekilde yapılandırın**ve ardından cihazları bu uyumluluk ortağı tarafından yönetilen Kullanıcı gruplarını yapılandırın.

3. **Uyumluluk ortağınızı Intune 'a veri gönderecek şekilde yapılandırın**.

4. **İOS veya Android cihazlarınızı bu cihaz uyumluluk ortağına kaydedin**.

Bu görevler tamamlandıktan sonra, cihaz uyumluluk ortağı cihaz durumu ayrıntılarını Intune 'a gönderir. Intune daha sonra bu bilgileri Azure AD 'ye ekler. Örneğin, uyumlu olmayan bir duruma sahip cihazlar, bu durumun Azure AD 'deki cihaz kaydına eklenmesini sağlar.

Uyumluluk durumu daha sonra, Intune tarafından yönetilen cihazlar için uyumluluk durumu verileriyle aynı olan koşullu erişim ilkeleri tarafından değerlendirilir.  Varsayılan olarak, Intune, iOS ve Android için kayıtlı bir uyumluluk iş ortağıdır. Ek iş ortakları eklediğinizde, cihazı iş gereksinimlerinize uyacak şekilde doğru iş ortağının yönettiğinden emin olmak için öncelik sırasını ayarlayabilirsiniz.

## <a name="supported-device-compliance-partners"></a>Desteklenen cihaz uyumluluk iş ortakları

- VMWare çalışma alanı BIR (eski adıyla AirWatch)

## <a name="prerequisites"></a>Ön koşullar

- [Microsoft Endpoint Manager yönetim merkezine](https://go.microsoft.com/fwlink/?linkid=2109431)Microsoft Intune ve erişim için bir abonelik.

- Cihaz uyumluluk ortağı için bir abonelik.

- Desteklenen cihaz platformları ve ek önkoşullar için uyumluluk iş ortağınızla ilgili belgeleri gözden geçirin.

## <a name="add-support-in-azure-ad-for-a-device-compliance-partner"></a>Cihaz uyumluluk ortağı için Azure AD 'de destek ekleme

Üçüncü taraf cihaz uyumluluk iş ortakları tarafından yönetilen cihazlar için desteği etkinleştirmek üzere, Azure AD 'de bu ortağı *Mobility (MDM ve MAM)* öğesine eklemeniz gerekir. Varsayılan olarak, Intune, *Mobility (MDM ve MAM)* için zaten kayıtlı.

### <a name="add-a-device-compliance-partner-to-azure-ad"></a>Azure AD 'ye cihaz uyumluluk ortağı ekleme

1. [Azure Portal](https://aad.portal.azure.com/) oturum açın ve **Azure Active Directory**  >  **Mobility (MDM ve MAM)**  >  **Uygulama Ekle**' ye gidin. ([ *MOBILITY (MDM ve MAM)* dikey penceresini doğrudan açın](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility).)

2. **Uygulama Ekle** dikey penceresinde, cihaz uyumluluk iş ortağınızın kutucuğunu seçin ve ardından **Ekle**' yi seçin.

   - *Bir çalışma alanı*Için, **VMware tarafından AirWatch** ' ı seçin

3. *Mobility (MDM ve MAM)* dikey penceresinde, **yapılandırma** dikey penceresini açmak ve kullanılabilir seçenekleri yapılandırmak için uyumluluk ortağınızı seçin.  Seçenekler **MDM Kullanıcı kapsamını**, **MDM kullanım koşulları URL 'sini**ve **MDM bulma URL**'sini içerir. Kullanıcı kapsamı **bazılarına**ayarlandığında, bu uyumluluk ortağıyla cihazları kaydedebilen Azure AD Kullanıcı gruplarını seçersiniz.

   Seçtiğiniz gruplardan hedeflenen cihazlar, iş ortağını MDM yetkilisi olarak kullanır.

4. Azure AD 'de iş ortağı yapılandırmasını gerçekleştirmek için **Kaydet** ' i seçin. Daha sonra, uyumluluk ortağını Intune 'A eklersiniz.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Intune 'U cihaz uyumluluk ortağıyla çalışacak şekilde yapılandırma

Azure AD, *Mobility (MDM ve MAM)* için bir cihaz uyumluluk ortağını destekleyecek şekilde yapılandırıldığında, Intune 'u da bu iş ortağıyla çalışacak şekilde yapılandırabilirsiniz. Bu yapılandırma, koşullu erişim ilkeleriniz ile bu iş ortağından uyumluluk durumu verilerini kullanmak istiyorsanız gereklidir.

### <a name="add-a-compliance-partner-to-intune"></a>Intune 'a uyumluluk ortağı ekleme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **iş ortağı Uyumluluk Yönetimi**  >  **Uyumluluk ortağı Ekle**' ye gidin.

   > [!div class="mx-imgBorder"]
   > ![Cihaz uyumluluk ortağı ekleme](./media/device-compliance-partners/add-compliance-partner.png)

3. **Temel bilgiler** sayfasında, **Uyumluluk ortağı** açılır ' i genişletin ve eklemekte olduğunuz iş ortağını seçin. Ardından, **Platform**için açılan eklentiyi seçin ve platformu seçin.

   Azure AD 'ye birden çok uyumluluk iş ortağı eklemiş olsanız bile, her platform için tek bir iş ortağıyla sınırlı olursunuz.

4. **Atamalar**' da, bu iş ortağı tarafından yönetilecek cihazları olacak Kullanıcı gruplarını seçin. Bu atamayla ilgili cihazlar için MDM yetkilisini bu iş ortağını kullanacak şekilde değiştirirsiniz.

5. **Gözden geçir + oluştur** sayfasında, seçimlerinizi gözden geçirin ve ardından **Oluştur** ' u seçerek bu yapılandırmayı doldurun.

Yapılandırmanız artık Iş ortağı Uyumluluk Yönetimi sayfasında görüntülenir.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Uyumluluk ortağının yapılandırmasını değiştirme

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **iş ortağı Uyumluluk Yönetimi**' ne gidin ve ardından değiştirmek istediğiniz iş ortağı yapılandırmasını seçin. Konfigürasyonlar platform türüne göre sıralanır.

3. İş ortağı yapılandırmasına **genel bakış** sayfasında, atamaları düzenleyebileceğiniz Özellikler sayfasını açmak için **Özellikler** ' i seçin.

4. **Özellikler** sayfasında, bu yapılandırmayı kullanacak grupları değiştirebileceğiniz atamalar görünümünü açmak için **Düzenle** ' yi seçin.

5. **Gözden geçir + kaydet** ' i ve ardından değişikliklerinizi kaydetmek için **Kaydet** ' i seçin.

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Uyumluluk ortağınızı Intune ile çalışacak şekilde yapılandırma

Bir cihaz uyumluluk ortağının Intune ile çalışmasını sağlamak için, bu iş ortağına özgü olan konfigürasyonları tamamlamalısınız. Bu görevle ilgili bilgi için, ilgili iş ortağı için belgelere bakın:

- [VMware çalışma alanı BIR](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>İOS veya Android cihazlarınızı bu cihaz uyumluluk ortağına kaydetme

Cihazları bu iş ortağıyla kaydetme hakkında bilgi için cihaz uyumluluk iş ortakları belgelerine bakın. Cihazlar kaydedildikten ve uyumluluk verilerini ortağa gönderdikten sonra, bu uyumluluk verileri Intune 'a iletilir ve Azure AD 'ye eklenir.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Üçüncü taraf cihaz uyumluluk iş ortakları tarafından yönetilen cihazları izleme

Üçüncü taraf cihaz uyumluluk iş ortaklarını yapılandırdıktan ve cihazları bunlara kaydettikten sonra, iş ortağı uyumluluk ayrıntılarını Intune 'a iletir. Intune bu verileri aldıktan sonra, Microsoft Endpoint Manager Yönetim merkezinde cihazların ayrıntılarını görüntüleyebilirsiniz.  

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın ve **uç nokta güvenliği**  >  **tüm cihazlar**' a gidin.  Bir üçüncü taraf iş ortağı MDM yetkilisi tarafından yönetilen cihazlar, bu ortağın adını **yönetilen** sütununda görüntüler. 

Bu görünüm hakkında daha fazla bilgi için bkz. [cihazları yönetme](../protect/endpoint-security-manage-devices.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Cihaz uyumluluk ilkesiyle çalışmaya başlama](../protect/device-compliance-get-started.md)
