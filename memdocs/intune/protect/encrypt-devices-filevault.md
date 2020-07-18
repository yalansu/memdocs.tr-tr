---
title: MacOS cihazlarını Intune ile Filekasası disk şifrelemesi ile şifreleme
titleSuffix: Microsoft Intune
description: MacOS cihazlarını yerleşik şifreleme yöntemi olan Filekasasıyla şifreleyin ve bu şifrelenmiş cihazların kurtarma anahtarlarını Intune portalı içinden yönetin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460493"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Intune ile macOS için dosya Kasası disk şifrelemesini kullanma

Intune, macOS Filekasadisk şifrelemesini destekler. Filekasası, macOS ile birlikte gelen bir tam disk şifreleme programıdır. **MacOS 10,13 veya üstünü**çalıştıran cihazlarda dosya kasasını yapılandırmak Için Intune 'u kullanabilirsiniz.

Yönetilen cihazlarınızda Filekasasını yapılandırmak için aşağıdaki ilke türlerinden birini kullanın:

- **[MacOS Filekasası Için uç nokta güvenlik ilkesi](#create-endpoint-security-policy-for-filevault)**. *Uç nokta güvenliği* Içindeki filekasası profili, filekasasını yapılandırmak için ayrılmış olan odaklanmış bir ayar grubudur.

  [Disk şifreleme ilkesi için profillerde bulunan dosya Kasası ayarlarını](../protect/endpoint-security-disk-encryption-profile-settings.md)görüntüleyin.

- **[MacOS Filekasası için Endpoint Protection cihaz yapılandırma profili](#create-endpoint-security-policy-for-filevault)**. Filekasası ayarları, macOS Endpoint Protection için kullanılabilir ayar kategorilerinden biridir. Cihaz yapılandırma profili kullanma hakkında daha fazla bilgi için bkz. [ınunte cihaz profili oluşturma](../configuration/device-profile-create.md).

  [Cihaz yapılandırma ilkesi için Endpoint Protection profillerinde bulunan dosya Kasası ayarlarını](../protect/endpoint-protection-macos.md#filevault)görüntüleyin.

Windows 10 için BitLocker 'ı yönetmek için bkz. [BitLocker Ilkesini yönetme](../protect/encrypt-devices.md).

> [!TIP]
> Intune, cihazların şifreleme durumu hakkındaki ayrıntıları, tüm yönetilen cihazlarınızda sunan yerleşik bir [şifreleme raporu](encryption-monitor.md) sağlar.

Cihazları dosya kasası ile şifrelemek için bir ilke oluşturduktan sonra, ilke iki aşamada cihazlara uygulanır. İlk olarak cihaz, Intune 'un kurtarma anahtarını alıp yedeklemesini sağlamak için hazır hale getirilir. Bu eyleme Emanet denir. Anahtar alındıktan sonra, disk şifrelemesi başlayabilir.

Bir cihazı dosya kasası ile şifrelemek için Intune ilkesi kullanmanın yanı sıra, Intune ['un cihaz Kullanıcı tarafından şifrelendiğinde dosya kasasının yönetimini varsaymasını](#assume-management-of-filevault-on-previously-encrypted-devices)sağlamak için ilkeyi yönetilen bir cihaza dağıtabilirsiniz. Bu senaryo, cihazın Intune 'dan dosya Kasası ilkesi almasını ve ardından kullanıcının kişisel kurtarma anahtarını Intune 'a yüklemesini gerektirir.

Dosya kasasının bir cihazda çalışması için Kullanıcı onaylı cihaz kaydı gereklidir. Kullanıcının kaydın Kullanıcı tarafından onaylanabilmesi için sistem tercihlerinden yönetim profilini el ile onaylaması gerekir.

## <a name="permissions-to-manage-filevault"></a>Dosya kasasını yönetme izinleri

Intune 'da Filekasasını yönetmek için hesabınızın ilgili Intune [rol tabanlı erişim denetimi](../fundamentals/role-based-access-control.md) (RBAC) izinlerine sahip olması gerekir.

Aşağıda, **uzak görevler** kategorisinin bir parçası olan ve izin veren yerleşik RBAC rollerinin yer aldığı dosya Kasası izinleri verilmiştir:

- **Dosya Kasası anahtarını al**:
  - Yardım Masası Işleci
  - Uç nokta güvenlik yöneticisi

- **Filekasa anahtarını döndür**
  - Yardım Masası Işleci

## <a name="create-device-configuration-policy-for-filevault"></a>Filekasası için cihaz yapılandırma ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. **Profil oluştur** sayfasında, aşağıdaki seçenekleri ayarlayın ve ardından **Oluştur**' a tıklayın:
   - **Platform**: MacOS
   - **Profil**: Endpoint Protection

   ![Filekasa profilini seçin](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. **Temel bilgiler** sayfasında, aşağıdaki özellikleri girin:

   - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı profil türünü ve platformunu içerebilir.

   - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

5. **Yapılandırma ayarları** sayfasında, kullanılabilir ayarları genişletmek Için **Dosya Kasası** ' nı seçin:

   > [!div class="mx-imgBorder"]
   > ![Dosya Kasası ayarları](./media/encrypt-devices-filevault/filevault-settings.png)

6. Aşağıdaki ayarları yapılandırın:
  
   - *Dosya kasasını etkinleştir*için **Evet**' i seçin.

   - *Kurtarma anahtarı türü*için **kişisel anahtar**' ı seçin.

   - *Kişisel kurtarma anahtarının Emanet konumu açıklaması*için, kullanıcılara cihazının [Kurtarma anahtarını alma](#retrieve-a-personal-recovery-key) hakkında rehberlik eden bir ileti ekleyin. Bu bilgiler, kişisel kurtarma anahtarı döndürme ayarını kullandığınızda kullanıcılarınız için yararlı olabilir. Bu, düzenli aralıklarla otomatik olarak yeni bir kurtarma anahtarı oluşturabilen bir cihaz için kullanılabilir.

     Örneğin: kayıp veya son döndürülen kurtarma anahtarını almak Için herhangi bir cihazdan Intune Şirket Portalı Web sitesinde oturum açın. Portalda *cihazlar* ' a gidin ve filekasasının etkinleştirildiği cihazı seçin ve ardından *Kurtarma anahtarını al*' ı seçin. Geçerli kurtarma anahtarı görüntülenir.

   Kalan [Filekasası ayarlarını](endpoint-protection-macos.md#filevault) iş gereksinimlerinizi karşılayacak şekilde yapılandırın ve ardından **İleri**' yi seçin.

7. Scope **(Etiketler)** sayfasında kapsam etiketleri **Seç** ' i seçerek profile kapsam etiketleri atayın.

   Devam etmek için **İleri** seçeneğini belirleyin.

8. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. Kullanıcı ve cihaz profilleri atama.
**İleri**’yi seçin.

9. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

## <a name="create-endpoint-security-policy-for-filevault"></a>Filekasası için uç nokta güvenlik ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **disk şifrelemesi**  >  **ilke oluştur**' u seçin.

3. **Temel bilgiler** sayfasında, aşağıdaki özellikleri girin ve ardından **İleri**' yi seçin.
   - **Platform**: MacOS
   - **Profil**: dosya Kasası

   ![Filekasa profilini seçin](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. **Yapılandırma ayarları** sayfasında:
   1. *Filekasasını etkinleştir* ayarını **Evet**olarak belirleyin.
   2. *Kurtarma anahtarı türü*Için yalnızca **kişisel kurtarma anahtarı** desteklenir.
   3. Gereksinimlerinizi karşılayacak ek ayarları yapılandırın.

   Kullanıcılara cihazlarıyla ilgili [Kurtarma anahtarını alma](#retrieve-a-personal-recovery-key) hakkında yardım almak için bir ileti eklemeyi düşünün. Bu bilgiler, kişisel kurtarma anahtarı döndürme ayarını kullandığınızda kullanıcılarınız için yararlı olabilir. Bu, düzenli aralıklarla otomatik olarak yeni bir kurtarma anahtarı oluşturabilen bir cihaz için kullanılabilir.

   Örneğin: kayıp veya son döndürülen kurtarma anahtarını almak Için herhangi bir cihazdan Intune Şirket Portalı Web sitesinde oturum açın. Portalda cihazlar ' a gidin ve Filekasasının etkinleştirildiği cihazı seçin ve ardından *Kurtarma anahtarını al*' ı seçin. Geçerli kurtarma anahtarı görüntülenir.

5. Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin.

6. Scope **(Etiketler)** sayfasında kapsam etiketleri **Seç** ' i seçerek profile kapsam etiketleri atayın.

   Devam etmek için **İleri** seçeneğini belirleyin.

7. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. Kullanıcı ve cihaz profilleri atama.
**İleri**’yi seçin.

8. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

## <a name="manage-filevault"></a>Dosya kasasını yönetme

Filekasası ilkesini alan cihazlarla ilgili bilgileri görüntülemek için bkz. [disk şifrelemeyi izleme](../protect/encryption-monitor.md).

Intune, bir macOS cihazını dosya kasası ile ilk kez şifrele, kişisel bir kurtarma anahtarı oluşturulur. Şifreleme sonrasında cihaz kişisel anahtarı cihaz kullanıcısına tek bir kez görüntüler.

Intune, yönetilen cihazlarda kişisel kurtarma anahtarının bir kopyasını sağlayabilir. Anahtarların Emanet, Intune yöneticilerinin cihazları korumaya yardımcı olmak için anahtarları döndürmesine ve kullanıcıların kayıp veya döndürülmüş bir kişisel kurtarma anahtarını kurtarmasına olanak sağlar.

Intune, Intune ilkesi bir cihazı şifrelediği veya bir kullanıcı el ile şifrelediği cihaz için kurtarma anahtarını karşıya yükledikten sonra bir kurtarma anahtarı gerektirir.

Intune tamamlandıktan sonra kişisel kurtarma anahtarı:

- Yöneticiler, Intune şifreleme raporunu kullanarak yönetilen macOS cihazlarınızın dosya Kasası kurtarma anahtarlarını yönetebilir ve döndürebilir.
- Yöneticiler, yalnızca *Şirket*olarak Işaretlenmiş yönetilen MacOS cihazları için kişisel kurtarma anahtarını görüntüleyebilir. Kişisel cihazlar için kurtarma anahtarını görüntüleyeamazlar.
- Kullanıcılar [, kişisel kurtarma anahtarlarını desteklenen bir konumdan](#retrieve-a-personal-recovery-key)görüntüleyebilir ve alabilir. Örneğin, Şirket Portalı Web sitesinden Kullanıcı, *Kurtarma anahtarını* uzak cihaz eylemi olarak almayı seçebilir.

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>Daha önce şifrelenen cihazlarda dosya kasasının yönetimini varsay

Intune, Intune ilkeleri kullanılarak şifrelenen macOS cihazlarında dosya Kasası disk şifrelemesini yönetebilir. Intune, Intune ilkesi aracılığıyla değil, cihaz kullanıcıları tarafından şifrelenen cihazlarda dosya kasasının yönetimini de alabilir.

#### <a name="prerequisites-to-assume-management-of-filevault"></a>Dosya kasasının yönetimini varsayma önkoşulları

Daha önce şifrelenen aygıtın yönetimini varsaymak için aşağıdaki koşulların karşılanması gerekir:

1. **Cihaza bir dosya Kasası Ilkesi dağıtın**. Daha önce şifrelenen cihaz, dosya Kasası disk şifrelemesini etkinleştiren bir Intune ilkesi almalıdır.

   Bu senaryoda ilke, cihazın şifresini çözemez veya yeniden şifrelemez. Bunun yerine, ilke Intune 'un cihazda zaten etkinleştirilmiş olan dosya Kasası şifrelemesinin yönetimini varsaymasını sağlar.  Cihazları dosya kasası ile şifrelemek için uç nokta güvenlik diski şifreleme ilkesi veya cihaz yapılandırma uç nokta koruma ilkesini kullanabilirsiniz.

   Bkz. [Ilke oluşturma ve dağıtma](#create-device-configuration-policy-for-filevault).

2. **Kullanıcılar kişisel kurtarma anahtarını Intune 'a yükler**.  Cihaz, dosya Kasası ilkesini aldıktan sonra, kişisel kurtarma anahtarını Intune 'a yüklemek üzere cihazı şifrelenen cihaz kullanıcısını yönlendirin. Anahtar başarıyla girilirse, Intune, dosya Kasası şifrelemesinin yönetimini varsayar ve cihaz ve Kullanıcı için yeni bir kişisel kurtarma anahtarı oluşturulur.

   > [!IMPORTANT]
   > Intune, şifrelemeyi tamamlaması için kullanıcıları kişisel kurtarma anahtarını karşıya yüklemesi gerektiğini uyarmaz. Bunun yerine, normal BT iletişim kanallarınızı kullanarak macOS cihazını daha önce, kendi kişisel kurtarma anahtarını Intune 'a yüklememeleri gereken Filekasası ile şifrelenmiş kullanıcılar için uyarır.  
   >
   > Uyumluluk ilkenize bağlı olarak, Intune cihazdaki dosya Kasası şifrelemesini başarıyla yönetilene kadar cihazların kurumsal kaynaklara erişimi engellenebilir.

#### <a name="upload-a-personal-recovery-key"></a>Kişisel kurtarma anahtarını karşıya yükle

Intune 'un daha önce şifrelenen bir cihazda dosya kasasını yönetmesine olanak tanımak için, cihaz kullanıcısının cihaz için geçerli kişisel kurtarma anahtarını Intune 'a yüklemesi için Şirket Portalı Web sitesini kullanması gerekir.  Karşıya yükleme sonrasında Intune, daha sonra gerektiğinde daha sonra kurtarmak üzere Intune tarafından depolanan yeni bir kişisel kurtarma anahtarı oluşturmak için anahtarı döndürür.

Şirket Portalı Web sitesinde Kullanıcı, şifreli macOS cihazını bulur ve **Mağaza kurtarma anahtarı**seçeneğini belirler. Kişisel kurtarma anahtarı girildiğinde, Intune yeni bir anahtar oluşturmak için anahtarı döndürmeye çalışır. Döndürme, girilen anahtarın o cihaz için doğru olduğunu doğrulamak için yapılır. Bu yeni anahtar daha sonra Intune tarafından ileride kullanılmak üzere depolanır ve yönetilir ve Kullanıcı cihazlarını kurtarmak zorunda olmalıdır.

Anahtar döndürme başarısız olursa, cihaz dosya Kasası ilkesini işlemedi veya girilen anahtar cihaz için doğru değil.

Başarılı döndürmeden sonra, Kullanıcı, [desteklenen bir konumdan yeni kişisel kurtarma anahtarlarını alabilir](#retrieve-a-personal-recovery-key).

 [Kişisel kurtarma anahtarının karşıya yüklenmesi için Son Kullanıcı içeriğini](../user-help/store-recovery-key.md)görüntüleyin.

> [!IMPORTANT]
> Intune tarafından değil, bir kullanıcı tarafından şifrelenen bir cihaz için, Intune bu cihaz bir dosya Kasası ilkesi alıncaya ve cihaz kullanıcısı kişisel kurtarma anahtarını başarıyla karşıya yüklemeyana kadar cihazlar Filekasası şifrelemesini yönetemez.

### <a name="retrieve-a-personal-recovery-key"></a>Kişisel kurtarma anahtarını alma

Intune tarafından yönetilen bir macOS cihazında, son kullanıcılar, herhangi bir cihaz kullanarak kişisel kurtarma anahtarını (Filekasası anahtarı) aşağıdaki konumlardan alabilir:

- Şirket Portalı web sitesi
- iOS/ıpados Şirket Portalı uygulaması
- Android Şirket Portalı uygulaması
- Intune uygulaması

Yöneticiler, bir *Kurumsal* cihaz olarak Işaretlenmiş şifreli MacOS cihazları için kişisel kurtarma anahtarlarını görüntüleyebilir. Kişisel bir cihaz için kurtarma anahtarını görüntüleyemez.

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
