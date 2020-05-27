---
title: Microsoft Intune-Azure 'da HoloLens 2 cihazlarında Windows Defender uygulama denetimini kullanma | Microsoft Docs
description: Windows Defender uygulama denetimi (WDAC) CSP 'yi, uygulamaların Microsoft Intune 'te HoloLens 2 cihazlarında açılmasını izin verecek veya engelleyecek şekilde yapılandırın. PowerShell ve özel bir yapılandırma profili kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990134"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Microsoft Intune ile HoloLens 2 cihazlarındaki uygulamalara izin vermek veya bunları engelleme için WDAC ve Windows PowerShell kullanma

Microsoft HoloLens 2 cihazları, [APPLOCKER CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)'nin yerini alan [Windows Defender uygulama denetimi (WDAC) CSP](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp)'sini destekler.

Windows PowerShell ve Microsoft Intune kullanarak, Microsoft HoloLens 2 cihazlarında belirli uygulamaların açılmasını sağlamak veya engellemek için WDAC CSP 'yi kullanabilirsiniz. Örneğin, Cortana uygulamasının kuruluşunuzdaki HoloLens 2 cihazlarında açılmasını sağlamak veya bunu engellemek isteyebilirsiniz.

Bu özellik şu platformlarda geçerlidir:

- Windows holographic for Business çalıştıran HoloLens 2 cihazları

WDAC CSP, [Windows Defender uygulama denetimi (WDAC) özelliğini](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)temel alır. [Birden çok WDAC ilkesi de kullanabilirsiniz](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

Bu makale, şunları nasıl yapacağınızı gösterir:

1. Bir WDAC ilkesi oluşturmak için Windows PowerShell 'i kullanın.
2. Windows PowerShell kullanarak, WDAC ilke kurallarını XML 'e dönüştürmek, XML 'i güncelleştirmek ve sonra XML 'i bir ikili dosyaya dönüştürmek için Windows PowerShell 'i kullanın.
3. Microsoft Intune, [özel bir cihaz yapılandırma profili](custom-settings-windows-holographic.md)oluşturun, bu WDAC ilkesi ikili dosyasını ekleyin ve Ilkeyi HoloLens 2 cihazlarınıza uygulayın.

Intune 'da, Windows Defender uygulama denetimi (WDAC) CSP 'yi kullanmak için özel bir yapılandırma profili oluşturmanız gerekir. 

Belirli uygulamaların HoloLens 2 cihazlarında açılmasını sağlamak veya reddetmek için bu makaledeki adımları Şablon olarak kullanın.

## <a name="prerequisites"></a>Ön koşullar

- Windows PowerShell hakkında bilgi sahibi olun.
- Intune 'da bir üyesi olarak oturum açın:

  - **İlke ve Profil Yöneticisi** veya **Intune rol yöneticisi** Intune rolü

    OR

  - **Genel yönetici** veya **Intune HIZMET Yöneticisi** Azure AD rolü

  [Intune Ile rol tabanlı erişim denetimi (RBAC)](../fundamentals/role-based-access-control.md) daha fazla bilgi içerir.

- HoloLens 2 cihazlarınızla bir Kullanıcı grubu veya cihazlar grubu oluşturun. Daha fazla bilgi için bkz. [Kullanıcı grupları ve cihaz grupları karşılaştırması](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Örnek

Bu örnek Windows PowerShell 'i kullanarak bir Windows Defender uygulama denetimi (WDAC) ilkesi oluşturur. İlke, belirli uygulamaların açılmasını engeller. Ardından, ilkeyi HoloLens 2 cihazlara dağıtmak için Intune 'u kullanın.

1. Masaüstü bilgisayarınızda **Windows PowerShell** uygulamasını açın.
2. Masaüstü bilgisayarınızda yüklü uygulama paketi hakkında bilgi alın:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Örneğin şunu girin: 

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Sonra, paketin uygulama özniteliklerine sahip olduğunu doğrulayın:

    ```powershell
    $package1
    ```

    Aşağıdaki uygulama ayrıntılarına benzer öznitelikleri görürsünüz:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Bir WDAC ilkesi oluşturun ve uygulama paketini reddetme kuralına ekleyin:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. REDDETMEK istediğiniz diğer uygulamalar için adım 2 ve 3 ' ü yineleyin:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Örneğin şunu girin: 

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. WDAC ilkesini **newpolicy. xml**' ye Dönüştür:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    NewPolicy. xml ' de bir uygulamanın tüm sürümlerini hedeflemek için, `PackageVersion="65535.65535.65535.65535"` reddetme düğümü içinde olduğundan emin olun:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    İçin `PackageFamilyNameRules` aşağıdaki sürümleri kullanabilirsiniz:

    - **Izin ver**: ENTER `PackageVersion, 0.0.0.0` , bu, "Bu sürüme ve yukarıya izin ver" anlamına gelir.
    - **Reddet**: ENTER `PackageVersion, 65535.65535.65535.65535` , bu, "Bu sürümü ve aşağıdaki adımları Reddet" anlamına gelir.

6. **Newpolicy. xml** ' i Masaüstü bilgisayarınızdaki varsayılan ilkeyle birleştirin. Bu adım, **Birleştiripolicy. xml**dosyası oluşturur. Örneğin, Windows, WHQL imzalı sürücülere ve imzalı uygulamaları depolamaya izin ver:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Bu **Denetim modu** kuralını, **birleştiripolicy. xml**' de devre dışı bırakın. Birleştirme yaptığınızda Denetim modu otomatik olarak açıktır:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. **Invalidateeas öğesini, bir sistem** \ **ilke. xml**dosyasındaki yeniden başlatma kuralında etkinleştirin:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Bu kurallar hakkında daha fazla bilgi için bkz. [WDAC ilke kurallarını ve dosya kurallarını anlama](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. **Birleştiripolicy. xml** ' i ikili biçime dönüştürün. Bu adım, **Compiledpolicy. bin**oluşturur. Bu **Compiledpolicy. bin** Ikili dosyasını Intune 'a ekleyeceksiniz.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Intune 'da özel cihaz yapılandırma profili oluşturma:

    1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde bir Windows 10 özel cihaz yapılandırma profili oluşturun.

        Belirli adımlar için bkz. [Intune 'DA OMA-URI kullanarak özel profil oluşturma](custom-settings-configure.md).

    2. Profili oluştururken, aşağıdaki ayarları girin:

      - **OMA-URI**: `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>` girin. `<PolicyGUID>`Adım 6 ' da oluşturduğunuz **birleştirilkesi. xml** dosyasındaki policytypeıd düğümü ile değiştirin.

        Örneğimizi kullanarak girin `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076` .

        İlke GUID 'SI, **birleştirilkesi. xml** dosyasındaki policytypeıd düğümüyle **eşleşmelidir** (adım 6 ' da oluşturulur).

      - **Veri türü**: **base64 dosyası**olarak ayarlanır. Dosyayı otomatik olarak bin 'den Base64 'e dönüştürür.
      - **Sertifika dosyası**: **compiledpolicy. bin** ikili dosyasını yükleyin (adım 9 ' da oluşturulur).

      Ayarlarınız aşağıdaki ayarlara benzer şekilde görünür:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Microsoft Intune 'de ApplicationControl CSP 'yi yapılandırmak için özel bir OMA-URI ekleyin.":::

11. Profil, HoloLens 2 grubunuza [atandığında](device-profile-assign.md) , profil durumunu kontrol edin. Profil başarıyla uygulandıktan sonra, HoloLens 2 cihazlarını yeniden başlatın.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Intune 'da özel profiller hakkında daha fazla bilgi edinin](custom-settings-configure.md).
