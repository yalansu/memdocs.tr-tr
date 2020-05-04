---
title: PFX sertifika profilleri oluşturma
titleSuffix: Configuration Manager
description: Şifrelenmiş veri değişimini destekleyen kullanıcıya özgü sertifikalar oluşturmak için Configuration Manager ' de PFX dosyalarını nasıl kullanacağınızı öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711178"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Sertifika yetkilisini kullanarak PFX Sertifika profilleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kimlik bilgileri için sertifika yetkilisi kullanan bir sertifika profili oluşturmayı öğrenin. Bu makalede kişisel bilgi değişimi (PFX) sertifika profilleri hakkında belirli bilgiler vurgulanmıştır. Bu profillerin nasıl oluşturulacağı ve yapılandırılacağı hakkında daha fazla bilgi için bkz. [sertifika profilleri](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager, bir sertifika yetkilisi tarafından verilen kimlik bilgilerini kullanarak bir PFX Sertifika profili oluşturmanızı sağlar. Sertifika yetkiliniz olarak Microsoft veya Entrust seçeneğini belirleyebilirsiniz. Kullanıcı cihazlarına dağıtıldığında PFX dosyaları, şifrelenmiş veri değişimini desteklemek üzere kullanıcıya özgü sertifikalar oluşturur.

Sertifika kimlik bilgilerini mevcut sertifika dosyalarından içeri aktarmak için bkz. [PFX Sertifika profillerini Içeri aktarma](import-pfx-certificate-profiles.md).

## <a name="prerequisites"></a>Önkoşullar

Bir sertifika profili oluşturmaya başlamadan önce gerekli önkoşulların kullanılabilir olduğundan emin olun. Daha fazla bilgi için bkz. [sertifika profilleri Için Önkoşullar](../../protect/plan-design/prerequisites-for-certificate-profiles.md). Örneğin, PFX Sertifika profilleri için bir [sertifika kayıt noktası](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) site sistem rolüne sahip olmanız gerekir.

## <a name="create-a-profile"></a>Profil oluşturma  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve **sertifika profilleri**' ni seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **sertifika profili oluştur**' u seçin.

1. **Sertifika profili oluşturma Sihirbazı**' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Ad**: Sertifika profili için benzersiz bir ad girin. En fazla 256 karakter kullanabilirsiniz.  

    - **Açıklama**: Configuration Manager konsolunda tanımlanmasına yardımcı olan sertifika profiline genel bakış sağlayan bir açıklama belirtin. En fazla 256 karakter kullanabilirsiniz.  

1. **Kişisel bilgi değişimi-PKCS #12 (PFX) ayarları-oluştur**seçeneğini belirleyin. Bu seçenek, bağlı bir şirket içi sertifika yetkilisinden (CA) Kullanıcı adına bir sertifika ister. Sertifika yetkilinizi seçin: **Microsoft** veya **Entrust Datacard**.

    > [!NOTE]
    > **Içeri aktarma** seçeneği, bir sertifika profili oluşturmak için var olan bir sertifikadan bilgileri alır. Daha fazla bilgi için bkz. [PFX Sertifika profillerini Içeri aktarma](import-pfx-certificate-profiles.md).

1. **Desteklenen platformlar** sayfasında, bu sertifika profilinin desteklediği işletim sistemi sürümlerini seçin. Configuration Manager sürümünüz için desteklenen işletim sistemi sürümleri hakkında daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemi sürümleri](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. **Sertifika yetkilileri** SAYFASıNDA, PFX sertifikalarını işlemek için sertifika kayıt noktasını (CRP) seçin:

    1. **Birincil site**: CA için CRP rolünü içeren sunucuyu seçin.
    1. **Sertifika yetkilileri**: ilgili CA 'yı seçin.

    Daha fazla bilgi için bkz. [sertifika altyapısı](../../protect/deploy-use/certificate-infrastructure.md).

**PFX sertifikası** sayfasındaki ayarlar, **genel** sayfasındaki seçili CA 'ya bağlı olarak değişir:

- [Microsoft CA](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Microsoft CA için **PFX Sertifika** ayarlarını yapılandırma

1. **Sertifika şablonu adı**için sertifika şablonunu seçin.

1. S/MIME imzalama veya şifreleme için sertifika profilini kullanmak için, **sertifika kullanımını**etkinleştirin.

    Bu seçeneği etkinleştirdiğinizde, hedef kullanıcıyla ilişkili tüm PFX sertifikalarını cihazlarıyla birlikte sunar. Bu seçeneği etkinleştirmezseniz, her cihaz benzersiz bir sertifika alır.  

1. **Konu adı biçimini** **ortak ad** veya **tam ayırt edici ad**olarak ayarlayın. Hangisini kullanacağınızdan emin değilseniz, CA yöneticinizle görüşün.

1. **Konu diğer adı**Için, **e-posta adresini** ve **Kullanıcı asıl adı 'nı (UPN)** CA 'nize uygun şekilde etkinleştirin.

1. **Yenileme eşiği**: sertifikaların, süresi dolmadan önce kalan sürenin yüzdesine göre otomatik olarak ne zaman yenilendiğini belirler.

1. **Sertifika geçerlilik süresini** sertifikanın kullanım ömrü olarak ayarlayın.

1. Sertifika kayıt noktası Active Directory kimlik bilgilerini belirttiğinde **Active Directory yayımlamayı**etkinleştirin.

1. Desteklenen bir veya daha fazla Windows 10 platformu seçtiyseniz:

    1. **Windows sertifika deposunu** **Kullanıcı**olarak ayarlayın. ( **Yerel bilgisayar** seçeneği sertifika dağıtmaz, seçmeyin.)

    1. Aşağıdaki **anahtar depolama sağlayıcısından (KSP)** birini seçin:

        - **Varsa Güvenilir Platform Modülü’ne (TPM) yükle**  
        - **Güvenilir Platform Modülü 'ye (TPM) yüklemek istemiyorsanız başarısız oldu**
        - **Iş için Windows Hello 'ya yüklemek istemiyorsanız başarısız oldu**
        - **Yazılım Anahtar Depolama Sağlayıcısına yükle**

1. Sihirbazı tamamlayın.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Entrust Datacard CA için **PFX Sertifika** ayarlarını yapılandırma

1. **DIJITAL kimlik yapılandırması**için yapılandırma profilini seçin. Entrust Yöneticisi dijital KIMLIK yapılandırma seçeneklerini oluşturur.

1. S/MIME imzalama veya şifreleme için sertifika profilini kullanmak için, **sertifika kullanımını**etkinleştirin.

    Bu seçeneği etkinleştirdiğinizde, hedef kullanıcıyla ilişkili tüm PFX sertifikalarını cihazlarıyla birlikte sunar. Bu seçeneği etkinleştirmezseniz, her cihaz benzersiz bir sertifika alır.  

1. Entrust **Konu adı biçim** belirteçlerini Configuration Manager alanlarla eşlemek Için, **Biçim**' i seçin.

    **Sertifika adı biçimlendirme** iletişim kutusu, Entrust dijital kimlik yapılandırma değişkenlerini listeler. Her Entrust değişkeni için uygun Configuration Manager alanlarını seçin.

1. Entrust **konu alternatif adı** BELIRTEÇLERINI desteklenen LDAP değişkenlerine eşlemek Için, **Biçim**' i seçin.

    **Sertifika adı biçimlendirme** iletişim kutusu, Entrust dijital kimlik yapılandırma değişkenlerini listeler. Her Entrust değişkeni için uygun LDAP değişkenini seçin.

1. **Yenileme eşiği**: sertifikaların, süresi dolmadan önce kalan sürenin yüzdesine göre otomatik olarak ne zaman yenilendiğini belirler.

1. **Sertifika geçerlilik süresini** sertifikanın kullanım ömrü olarak ayarlayın.

1. Sertifika kayıt noktası Active Directory kimlik bilgilerini belirttiğinde **Active Directory yayımlamayı**etkinleştirin.

1. Desteklenen bir veya daha fazla Windows 10 platformu seçtiyseniz:

    1. **Windows sertifika deposunu** **Kullanıcı**olarak ayarlayın. ( **Yerel bilgisayar** seçeneği sertifika dağıtmaz, seçmeyin.)

    1. Aşağıdaki **anahtar depolama sağlayıcısından (KSP)** birini seçin:

        - **Varsa Güvenilir Platform Modülü’ne (TPM) yükle**  
        - **Güvenilir Platform Modülü 'ye (TPM) yüklemek istemiyorsanız başarısız oldu**
        - **Iş için Windows Hello 'ya yüklemek istemiyorsanız başarısız oldu**
        - **Yazılım Anahtar Depolama Sağlayıcısına yükle**

1. Sihirbazı tamamlayın.

## <a name="deploy-the-profile"></a>İlkeyi dağıtma

Bir sertifika profili oluşturduktan sonra, **sertifika profilleri** düğümünde artık kullanılabilir. Dağıtımı hakkında daha fazla bilgi için bkz. [kaynak erişim profillerini dağıtma](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Ayrıca bkz.

[Yeni bir sertifika profili oluştur](../../protect/deploy-use/create-certificate-profiles.md)

[PFX sertifika profilleri içeri aktarma](import-pfx-certificate-profiles.md)

[Wi-Fi, VPN, e-posta ve sertifika profilleri dağıtma](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
