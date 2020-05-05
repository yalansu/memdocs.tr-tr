---
title: Cihazları toplu kaydetme
titleSuffix: Configuration Manager
description: Configuration Manager içindeki şirket içi mobil cihaz yönetimi (MDM) ile cihazları otomatik olarak toplu kaydetme.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720684"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Configuration Manager Şirket içi MDM ile cihazları toplu kaydetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Şirket içi mobil cihaz yönetimi (MDM) içindeki toplu kayıt, cihazları kaydetmek için otomatikleştirilmiş bir yöntemdir. Diğer yöntem, kullanıcıların cihazı kaydetmek için kimlik bilgilerini girmesini gerektiren Kullanıcı kaydı ' dır. Toplu kayıt, kayıt sırasında cihazın kimliğini doğrulamak için bir kayıt paketi kullanır. Paket, kaydı desteklemek için sertifika ve Wi-Fi profilleri de içerebilen bir. ppkg dosyasıdır.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a>Sertifika profili oluşturma

Cihaza bir güvenilen kök sertifikayı otomatik olarak yüklemek için bir sertifika profili ekleyin. Bu kök sertifika, şirket içi MDM için gereken cihazlar ve site sistem rolleri arasındaki güvenilir iletişim için gereklidir.

Siteyi şirket içi MDM için hazırlarken, güvenilen kök sertifikayı dışarı aktardınız. Bu sertifikayı kayıt paketinin sertifika profilinde kullanın. Güvenilen kök sertifikayı alma hakkında daha fazla bilgi için bkz. [Güvenilen kök sertifikayı dışarı aktarma](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Sertifika profili oluşturmak için, dışarıya aktarılmış sertifikayı kullanın. Daha fazla bilgi için bkz. [sertifika profilleri oluşturma](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a>Wi-Fi profili oluşturma

Toplu kayıt paketinin başka bir bileşeni bir Wi-Fi profilidir. Bu profil, cihazın kaydı desteklemesi için ağ bağlantısına sahip olduğundan emin olabilir.

Configuration Manager ' de Wi-Fi profili oluşturma hakkında daha fazla bilgi için bkz. [Wi-Fi profilleri oluşturma](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Wi-Fi profili sınırlamaları

Şirket içi MDM toplu kaydı için bir Wi-Fi profili oluşturduğunuzda, aşağıdaki sınırlamaları gözden geçirin.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Şirket içi MDM için Wi-Fi güvenlik yapılandırması

Configuration Manager geçerli dalı yalnızca şirket içi MDM için aşağıdaki Wi-Fi güvenlik yapılandırmasını destekler:

- Güvenlik türleri: **WPA2 Enterprise** veya **WPA2 Kişisel**

- Şifreleme türleri: **AES** veya **TKIP**

- EAP türleri: **Akıllı Kart veya diğer sertifika** ya da **PEAP**

#### <a name="proxy-server"></a>Proxy sunucu

Configuration Manager, Wi-Fi profilinde ara sunucu bilgileri için bir ayara sahip olsa da, cihaz kaydedildiğinde proxy 'yi yapılandırmaz. Toplu kayıtlı cihazlarda bir ara sunucu ayarlamanız gerekirse:

- Cihazların kaydı yapıldıktan sonra yapılandırma öğelerini kullanarak ayarları dağıtın.

- Windows görüntü ve yapılandırma Tasarımcısı 'nı (ICD) kullanarak ikinci bir paket oluşturun ve toplu kayıt paketiyle birlikte dağıtın.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a>Kayıt profili oluşturma

Kayıt profili, cihaz kaydı için gerekli ayarları belirtmenize olanak tanır. Bu ayarlar, bir [sertifika profili](#bkmk_createCert) ve bir [Wi-Fi profili](#CreateWifi)içerir.

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **şirkete ait tüm cihazlar**' ı genişletin, **Windows**' u genişletin ve **kayıt profilleri** düğümünü seçin.

1. Şeritte **kayıt profili oluştur**' u seçin.

1. Kayıt profili oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:

    - **Ad**: profili tanımlamak için benzersiz bir ad

    - **Açıklama**: profili daha ayrıntılı bir şekilde açıklamaya yönelik isteğe bağlı bir alan

    - **Yönetim yetkilisi**: yalnızca **Şirket içi** seçeneğini belirleyin

1. **Site ataması** sayfasında, bir cihaz yönetim noktasıyla **Yönetim sitesi kodunu** seçin.

1. **Kayıt proxy noktası seç** sayfasında **yalnızca Intranet**' i seçin ve ardından bir veya daha fazla kayıt proxy noktası seçin. Cihaz, kayıt işlemini başlatmak için bu sunucuları kullanacaktır.

1. **Güvenilen kök sertifika seç** sayfasında, güvenilen kök sertifikayı içeren sertifika profilini seçin.

1. **Wi-Fi profilleri** sayfasında, bağlanacak cihazlar için gerekli ağ ayarlarını içeren Wi-Fi profilini seçin.

    > [!TIP]
    > Kayıt paketiniz için bir Wi-Fi profili kullanmıyorsanız bu adımı atlayın.

1. Sihirbazı tamamlayın.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>Kayıt paketi oluşturma

Kayıt paketi (ppkg), şirket içi MDM için cihazları toplu kaydetmek üzere kullandığınız dosyadır. Bu dosyayı Configuration Manager oluşturun. Windows ICD ile benzer türlerde paketler oluşturabileceğiniz gibi, şirket içi MDM için cihazları kaydetmek üzere yalnızca Configuration Manager içinde oluşturduğunuz paketler kullanılabilir. Windows ICD ile oluşturduğunuz bir paket, yalnızca kayıt için gerekli Kullanıcı asıl adını (UPN) sağlayabilir, gerçek kayıt işlemini başlatamaz.

Kayıt paketi oluşturma işlemi, Windows 10 için Windows Değerlendirme ve Dağıtım Araç Seti’ni (ADK) gerektirir. Configuration Manager konsolunu çalıştıran bilgisayarda, Windows ADK 'nin en son sürümünü yükler. **Görüntüleme ve yapılandırma Tasarımcısı (ICD)** özelliğini ve tüm bağımlılıkları seçin. (Bu sürümün, Configuration Manager sitesi tarafından işletim sistemi dağıtımı için kullanılan sürümle eşleşmesi gerekmez.) Daha fazla bilgi için bkz. [Windows 10 Için WINDOWS ADK 'Yi indirme](https://docs.microsoft.com/windows-hardware/get-started/adk-install).

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **şirkete ait tüm cihazlar**' ı genişletin, **Windows**' u genişletin ve **kayıt profilleri** düğümünü seçin.

1. Mevcut bir kayıt profili seçin. Şeritte **dışarı aktar**' ı seçin.

1. Kayıt paketini dışarı aktar penceresinde, aşağıdaki bilgileri belirtin:

    - **Geçerlilik süresi (gün)**: varsayılan olarak, Configuration Manager kayıt paketini iki hafta (14 gün) ile sona ermek üzere ayarlar. Geçerlilik süresi dolduktan sonra cihaz kaydı için paketi kullanamazsınız. 1 ile 30 arasında bir tamsayı girin.

    - **Paket dosyası**:. ppkg dosyası için bir yerel veya ağ dosyası yolu ve adı belirtin.

    - **Paketi şifreleyin**: paketi parolayla korumak için bu seçeneği etkinleştirin. Paketi dışarı aktardıktan sonra, Configuration Manager oluşturulan parolayı görüntüler. Parolayı kopyalayıp güvenli bir konuma kaydedin. Parola olmadan, dışarıya aktarılmış kayıt paketini kullanamazsınız.

        > [!IMPORTANT]
        > Configuration Manager parolayı kaydetmez ve özelleştiremez veya değiştiremezsiniz. Parolayı görüntüleyen pencereyi kapattıktan sonra parolayı almanın bir yolu yoktur.

1. **Export** (Dışarı aktar) öğesini seçin. Configuration Manager kayıt paketini oluşturmak için Windows ADK 'yi kullanır.

Configuration Manager geçerli kayıt paketlerini izler. Konsolunda, **kayıt profili** düğümünü genişletin ve **aktarılmış paketler**' i seçin.

> [!TIP]
> Configuration Manager konsolundan bir kayıt paketini kaldırırsanız, cihazları kaydetmek için kullanamazsınız. Başkalarının toplu kayıt için kullanmasını istemediğiniz kayıt paketlerini yönetmek için bu yöntemi kullanın.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>Bir cihazı toplu kaydetme

Cihazın, kullanıma hazır deneyim (OOBE) işleminden önce veya sonra cihazları kaydetmek için paketi kullanabilirsiniz. Kayıt paketi, özgün ekipman üreticisi (OEM) sağlama paketinin bir parçası olarak da dahil edilebilir.

Toplu kayıt için paketi kullanmak için cihaza fiziksel olarak teslim etmeniz gerekir. Gereksinimlerinize bağlı olarak çeşitli yöntemler vardır, örneğin:

- Dosya sisteminden Kopyala

- E-postaya iliştirme

- Yakın alan iletişimi (NFC) bağlantısı üzerinden Kopyala

- Bellek kartından kopyalama

- Barkod tarama

- Internet paylaşımlı bir cihazdan kopyalama

- OEM sağlama paketine dahil etme

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Toplu kayıt paketiyle bir cihaz kaydetme

1. Bir cihazda,. ppkg dosyasını açın. Gerekirse yönetici olarak çalıştır.

1. Windows, paketin güvenilir bir kaynaktan olup olmadığını sorar, **Evet**' i seçin.

Kayıt işlemi başlar.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>Kaydı doğrula

### <a name="verify-bulk-enrollment-on-the-device"></a>Cihazdaki toplu kaydı doğrulama

1. Cihazda **Ayarlar**' ı açın.

1. **Hesaplar**' ı seçin ve **Iş veya okul erişimi**' ni seçin. Kayıt başarılı olduğunda, **CompanyApps**altında bir hesap görürsünüz.

1. Hesabı seçin ve ardından **Eşitle**' yi seçin. Bu eylem, Configuration Manager Yönetimi başlatır.

### <a name="verify-enrollment-in-the-console"></a>Konsolda kaydı doğrulama

Cihazların başarıyla kaydedildiğini doğrulamak için Configuration Manager konsolunu kullanın. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar**' ı seçin. Cihaz listesinde kayıtlı cihaza gözatıp arama yapın.
