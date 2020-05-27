---
title: MacOS cihazlarını Intune ile Filekasası disk şifrelemesi ile şifreleme
titleSuffix: Microsoft Intune
description: MacOS cihazlarını yerleşik şifreleme yöntemi olan Filekasasıyla şifreleyin ve bu şifrelenmiş cihazların kurtarma anahtarlarını Intune portalı içinden yönetin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 99facc87d068239962ab0d40874aa081f5e19189
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989680"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Intune ile macOS için dosya Kasası disk şifrelemesini kullanma

Intune, macOS Filekasadisk şifrelemesini destekler. Filekasası, macOS ile birlikte gelen bir tam disk şifreleme programıdır. **MacOS 10,13 veya üstünü**çalıştıran cihazlarda dosya kasasını yapılandırmak Için Intune 'u kullanabilirsiniz.

Yönetilen cihazlarınızda Filekasasını yapılandırmak için aşağıdaki ilke türlerinden birini kullanın:

- **[MacOS Filekasası Için uç nokta güvenlik ilkesi](#create-an-endpoint-security-policy-for-filevault)**. *Uç nokta güvenliği* Içindeki filekasası profili, filekasasını yapılandırmak için ayrılmış olan odaklanmış bir ayar grubudur.

  [Disk şifreleme ilkesi için profillerde bulunan dosya Kasası ayarlarını](../protect/endpoint-security-disk-encryption-profile-settings.md)görüntüleyin.

- **[MacOS Filekasası için Endpoint Protection cihaz yapılandırma profili](#create-an-endpoint-security-policy-for-filevault)**. Filekasası ayarları, macOS Endpoint Protection için kullanılabilir ayar kategorilerinden biridir. Cihaz yapılandırma profili kullanma hakkında daha fazla bilgi için bkz. [ınunte cihaz profili oluşturma](../configuration/device-profile-create.md).

  [Cihaz yapılandırma ilkesi için Endpoint Protection profillerinde bulunan dosya Kasası ayarlarını](../protect/endpoint-protection-macos.md#filevault)görüntüleyin.

Windows 10 için BitLocker 'ı yönetmek için bkz. [BitLocker Ilkesini yönetme](../protect/encrypt-devices.md).

> [!TIP]
> tüm yönetilen cihazlarınızda cihazların şifreleme durumu hakkında ayrıntılı bilgi sunan [şifreleme raporu](encryption-monitor.md) .

Cihazları dosya kasası ile şifrelemek için bir ilke oluşturduktan sonra, ilke iki aşamada cihazlara uygulanır. İlk olarak cihaz, Intune 'un kurtarma anahtarını alıp yedeklemesini sağlamak için hazır hale getirilir. Bu eyleme Emanet denir. Anahtar alındıktan sonra, disk şifrelemesi başlayabilir.

Dosya kasasının bir cihazda çalışması için Kullanıcı onaylı cihaz kaydı gereklidir. Kullanıcının kaydın Kullanıcı tarafından onaylanabilmesi için sistem tercihlerinden yönetim profilini el ile onaylaması gerekir.

## <a name="permissions-to-manage-filevault"></a>Dosya kasasını yönetme izinleri

Intune 'da Filekasasını yönetmek için hesabınızın ilgili Intune [rol tabanlı erişim denetimi](../fundamentals/role-based-access-control.md) (RBAC) izinlerine sahip olması gerekir.

Aşağıda, **uzak görevler** kategorisinin bir parçası olan ve izin veren yerleşik RBAC rollerinin yer aldığı dosya Kasası izinleri verilmiştir:

- **Dosya Kasası anahtarını al**:
  - Yardım Masası Işleci
  - Uç nokta güvenlik yöneticisi

- **Filekasa anahtarını döndür**
  - Yardım Masası Işleci

## <a name="create-and-deploy-policy"></a>İlke oluşturma ve dağıtma

### <a name="create-an-endpoint-security-policy-for-filevault"></a>Filekasası için uç nokta güvenlik ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **disk şifrelemesi**  >  **ilke oluştur**' u seçin.

3. **Temel bilgiler** sayfasında, aşağıdaki özellikleri girin ve ardından **İleri**' yi seçin.
   1. **Platform**: MacOS
   2. **Profil**: dosya Kasası

   ![Filekasa profilini seçin](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. **Yapılandırma ayarları** sayfasında:
   1. *Filekasasını etkinleştir* ayarını **Evet**olarak belirleyin.
   2. *Kurtarma anahtarı türü*Için yalnızca **kişisel kurtarma anahtarı** desteklenir.
   3. Gereksinimlerinizi karşılayacak ek ayarları yapılandırın.

   Kullanıcılara cihazlarıyla ilgili kurtarma anahtarını alma hakkında yardım almak için bir ileti eklemeyi düşünün. Bu bilgiler, kişisel kurtarma anahtarı döndürme ayarını kullandığınızda kullanıcılarınız için yararlı olabilir. Bu, düzenli aralıklarla otomatik olarak yeni bir kurtarma anahtarı oluşturabilen bir cihaz için kullanılabilir.

   Örneğin: kayıp veya son döndürülen kurtarma anahtarını almak Için herhangi bir cihazdan Intune Şirket Portalı Web sitesinde oturum açın. Portalda cihazlar ' a gidin ve Filekasasının etkinleştirildiği cihazı seçin ve ardından *Kurtarma anahtarını al*' ı seçin. Geçerli kurtarma anahtarı görüntülenir.

5. Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin.

6. Scope **(Etiketler)** sayfasında kapsam etiketleri **Seç** ' i seçerek profile kapsam etiketleri atayın.

   Devam etmek için **İleri**’yi seçin.

7. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. Kullanıcı ve cihaz profilleri atama.
**İleri**’yi seçin.

8. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

### <a name="create-a-device-configuration-policy-for-filevault"></a>Filekasası için cihaz yapılandırma ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. Aşağıdaki seçenekleri ayarlayın:
   1. **Platform**: MacOS
   2. **Profil**: Endpoint Protection

   ![Filekasa profilini seçin](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. **Ayarlar**  >  **Dosya Kasası**' nı seçin.

   ![Dosya Kasası ayarları](./media/encrypt-devices-filevault/filevault-settings.png)

5. *Filekasası*için **Etkinleştir**' i seçin.

6. *Kurtarma anahtarı türü*Için yalnızca **kişisel anahtar** desteklenir.

   Kullanıcılara cihazlarıyla ilgili kurtarma anahtarını alma hakkında yardım almak için bir ileti eklemeyi düşünün. Bu bilgiler, kişisel kurtarma anahtarı döndürme ayarını kullandığınızda kullanıcılarınız için yararlı olabilir. Bu, düzenli aralıklarla otomatik olarak yeni bir kurtarma anahtarı oluşturabilen bir cihaz için kullanılabilir.

   Örneğin: kayıp veya son döndürülen kurtarma anahtarını almak Için herhangi bir cihazdan Intune Şirket Portalı Web sitesinde oturum açın. Portalda *cihazlar* ' a gidin ve filekasasının etkinleştirildiği cihazı seçin ve ardından *Kurtarma anahtarını al*' ı seçin. Geçerli kurtarma anahtarı görüntülenir.

7. Kalan [Filekasası ayarlarını](endpoint-protection-macos.md#filevault) iş gereksinimlerinizi karşılayacak şekilde yapılandırın ve ardından **Tamam**' ı seçin.

8. Ek ayarların yapılandırmasını tamamladıktan sonra profili kaydedin.

## <a name="manage-filevault"></a>Dosya kasasını yönetme

Filekasası ilkesini alan cihazlarla ilgili bilgileri görüntülemek için bkz. [disk şifrelemeyi izleme](../protect/encryption-monitor.md).

Intune, bir macOS cihazını dosya kasası ile ilk kez şifrele, kişisel bir kurtarma anahtarı oluşturulur. Şifreleme sonrasında cihaz kişisel anahtarı cihaz kullanıcısına tek bir kez görüntüler.

Intune, yönetilen cihazlarda kişisel kurtarma anahtarının bir kopyasını sağlayabilir. Anahtarların Emanet, Intune yöneticilerinin cihazları korumaya yardımcı olmak için anahtarları döndürmesine ve kullanıcıların kayıp veya döndürülmüş bir kişisel kurtarma anahtarını kurtarmasına olanak sağlar.

Intune, bir macOS cihazını Filekasası ile şifreledikten sonra:

- Yöneticiler, Intune şifreleme raporunu kullanarak Filekasasını kurtarma anahtarlarını görüntüleyebilir ve yönetebilir.
- Kullanıcılar cihazdaki Web Şirket Portalı kişisel kurtarma anahtarını görüntüleyebilir. Web Şirket Portalı içinden şifrelenmiş macOS cihazını seçin ve ardından "kurtarma anahtarını al" seçeneğini bir uzak cihaz eylemi olarak belirleyin.

> [!IMPORTANT]
> Intune tarafından değil, kullanıcılar tarafından şifrelenen cihazlar Intune tarafından yönetilemez. Bu, Intune 'un bu cihazların kişisel kurtarmasını ve kurtarma anahtarı döndürmesini yönetemeyeceği anlamına gelir. Intune 'un cihaz için dosya kasasını ve kurtarma anahtarlarını yönetebilmesi için, kullanıcının cihazının şifresini çözmesine ve ardından Intune 'un cihazı şifrelemesine izin vermelidir.

### <a name="retrieve-personal-recovery-key"></a>Kişisel kurtarma anahtarını al

Intune tarafından şifrelenen bir macOS cihazı için, son kullanıcılar iOS Şirket Portalı uygulamasını, Android Şirket Portalı uygulamasını veya Android Intune uygulamasını kullanarak kişisel kurtarma anahtarını (Filekasası anahtarı) alabilir.

Kişisel kurtarma anahtarına sahip olan cihaz Intune 'a kaydolmalıdır ve Intune aracılığıyla Filekasasıyla şifrelenir. İOS Şirket Portalı uygulamasını, Android Şirket Portalı uygulamasını, Android Intune uygulamasını veya Şirket Portalı Web sitesini kullanarak, Kullanıcı Mac cihazlarına erişmek için gereken **Filekasasını** kurtarma anahtarını görebilir.

Cihaz kullanıcıları **Devices**  >  *şifrelenmiş ve kayıtlı MacOS cihazı*  >  **Kurtarma anahtarı al**' ı seçerek cihazları seçebilir. Tarayıcıda Web Şirket Portalı gösterilir ve kurtarma anahtarı görüntülenir.

### <a name="rotate-recovery-keys"></a>Kurtarma anahtarlarını döndür

Intune, kişisel kurtarma anahtarlarını döndürmek ve kurtarmak için birden çok seçeneği destekler. Geçerli kişisel anahtarın kaybolması veya risk altında olması düşünülmek, bir anahtarı döndürmenizi bir neden olur.

- **Otomatik döndürme**: yönetici olarak, kişisel kurtarma anahtarı dönüşü için otomatik olarak yeni kurtarma anahtarı oluşturmak üzere filekasa ayarını yapılandırabilirsiniz. Bir cihaz için yeni bir anahtar oluşturulduğunda, anahtar kullanıcıya gösterilmez. Bunun yerine, kullanıcının anahtarı bir yöneticiden ya da Şirket Portalı uygulamasını kullanarak alması gerekir.

- **El ile döndürme**: yönetici olarak, Intune ile yönettiğiniz ve filekasasıyla şifrelenen bir cihazın bilgilerini görüntüleyebilirsiniz. Daha sonra, şirket cihazları için kurtarma anahtarını el ile döndürmeyi tercih edebilirsiniz. Kişisel cihazlar için kurtarma anahtarlarını döndüremezsiniz.

  Kurtarma anahtarını döndürmek için:

  1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

  2. **Cihazlar**   >  **tüm cihazlar**' ı seçin.

  3. Cihaz listesinden, şifrelenen ve anahtarını döndürmek istediğiniz aygıtı seçin. Ardından Izleyici ' nin altında, **kurtarma anahtarları**' nı seçin.
  
  4. Kurtarma anahtarları bölmesinde, **Filekasası kurtarma anahtarını Döndür**' ü seçin.

     Cihazın Intune ile bir sonraki denetlemesi sırasında kişisel anahtar döndürülür. Gerektiğinde, yeni anahtar Kullanıcı tarafından Şirket portalı üzerinden elde edilebilir.

### <a name="recover-recovery-keys"></a>Kurtarma anahtarlarını kurtar

- **Yönetici**: Yöneticiler, filekasasıyla şifrelenen cihazların kişisel kurtarma anahtarlarını görüntüleyemez.

- **Son Kullanıcı**: son kullanıcılar herhangi bir cihazdan Şirket portalı Web sitesini kullanarak yönetilen cihazlarından herhangi biri için geçerli kişisel kurtarma anahtarını görüntüler. Şirket Portalı uygulamasından kurtarma anahtarlarını görüntüleyemezsiniz.

  Kurtarma anahtarını görüntülemek için:
  
  1. Herhangi bir cihazdan *Intune şirket portalı* Web sitesinde oturum açın.

  2. Portalda **cihazlar** ' a gidin ve filekasasıyla şifrelenen MacOS cihazını seçin.

  3. **Kurtarma anahtarını al**' ı seçin. Geçerli kurtarma anahtarı görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar

[BitLocker ilkesini yönetme](../protect/encrypt-devices.md)

[Disk şifrelemesini yönetme](../protect/encryption-monitor.md)
