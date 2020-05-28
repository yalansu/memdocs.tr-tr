---
title: PFX sertifika profilleri içeri aktarma
titleSuffix: Configuration Manager
description: Şifrelenmiş veri değişimini destekleyen kullanıcıya özgü sertifikalar oluşturmak için Configuration Manager ' de PFX dosyalarını nasıl kullanacağınızı öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3304d480f0650191a784a9152ae464e81c2207a1
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906407"
---
# <a name="import-pfx-certificate-profiles"></a>PFX sertifika profilleri içeri aktarma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Dış sertifikalardan kimlik bilgilerini içeri aktararak bir sertifika profili oluşturmayı öğrenin. Bu makalede kişisel bilgi değişimi (PFX) sertifika profilleri hakkında belirli bilgiler vurgulanmıştır. Bu profillerin nasıl oluşturulacağı ve yapılandırılacağı hakkında daha fazla bilgi için bkz. [sertifika profilleri](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager, farklı cihazlar ve işletim sistemi sürümleri için farklı türlerdeki sertifika depolarını destekler. Örneğin, Windows 10 ve Windows 10 Mobile. Daha fazla bilgi için bkz. [sertifika profili önkoşulları](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Sertifika kimlik bilgilerini içeri aktarmak ve ardından, aygıtlara PFX dosyaları sağlamak için Configuration Manager kullanın. Bu dosyaları, şifrelenmiş veri değişimini desteklemek üzere kullanıcıya özgü sertifikalar oluşturmak için kullanabilirsiniz.

> [!TIP]  
> Bu işleme ilişkin adım adım yönergeler için, [Configuration Manager ' de PFX Sertifika profillerini oluşturma ve dağıtma](https://docs.microsoft.com/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager)Web günlüğü gönderisine bakın.  

## <a name="create-a-profile"></a>Profil oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve **sertifika profilleri**' ni seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **sertifika profili oluştur**' u seçin.

1. **Sertifika profili oluşturma Sihirbazı**' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Ad**: Sertifika profili için benzersiz bir ad girin. En fazla 256 karakter kullanabilirsiniz.  

    - **Açıklama**: Configuration Manager konsolunda tanımlanmasına yardımcı olan sertifika profiline genel bakış sağlayan bir açıklama belirtin. En fazla 256 karakter kullanabilirsiniz.  

1. **Kişisel bilgi değişimi-PKCS #12 (PFX) ayarları-Içeri aktar**' ı seçin. Bu seçenek, bir sertifika profili oluşturmak için mevcut bir sertifikadaki bilgileri içeri aktarır.

    > [!NOTE]
    > **Oluştur** seçeneği, bağlı bir şirket içi sertifika YETKILISINDEN (CA) Kullanıcı adına bir sertifika ister. Bu işlem daha sonra sertifikayı istemcilere PFX dosyaları olarak güvenli bir şekilde teslim eder. Daha fazla bilgi için bkz. [sertifika yetkilisi kullanarak PFX Sertifika profilleri oluşturma](create-pfx-certificate-profiles.md).

1. **Sertifika profili oluşturma Sihirbazı**'Nın **PFX sertifikası** sayfasında, cihaz anahtarı depolama sağlayıcısını (KSP) belirtin:

    - **Varsa Güvenilir Platform Modülü’ne (TPM) yükle**  
    - **Güvenilir Platform Modülü 'ye (TPM) yüklemek istemiyorsanız başarısız oldu**
    - **Iş için Windows Hello 'ya yüklemek istemiyorsanız başarısız oldu**
    - **Yazılım Anahtar Depolama Sağlayıcısına yükle**

1. **Desteklenen platformlar** sayfasında desteklenen cihaz platformlarını seçin.

1. Sihirbazı tamamlayın.

## <a name="deploy-the-profile"></a>İlkeyi dağıtma

Bir sertifika profili oluşturup sağlamadıktan sonra, **sertifika profilleri** düğümünde artık kullanılabilir. Dağıtımı hakkında daha fazla bilgi için bkz. [kaynak erişim profillerini dağıtma](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Birincil kullanıcıları ata

Hedef kullanıcıları, PFX sertifikalarını yüklemeniz gereken Windows 10 cihazlarında birincil kullanıcı olarak atayın. Daha fazla bilgi için bkz. [Kullanıcı cihaz benzeşimi](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Bir PFX betiği oluştur

PFX sertifikasını içeri aktarmak için aşağıdaki Configuration Manager PowerShell cmdlet 'lerini kullanarak bir PFX betiği oluşturun:

- [Get-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Import-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Örnek betik

Bir kullanıcı için bir sertifika profiline bir PFX dosyası sağlamak için, PowerShell 'i Configuration Manager konsolunun bulunduğu bir bilgisayarda açın. Değişkenleri ortamınızdaki değerlerle değiştirin.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Ayrıca bkz.

[Yeni bir sertifika profili oluştur](../../protect/deploy-use/create-certificate-profiles.md)

[Sertifika yetkilisini kullanarak PFX Sertifika profilleri oluşturma](create-pfx-certificate-profiles.md)

[Wi-Fi, VPN, e-posta ve sertifika profilleri dağıtma](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
