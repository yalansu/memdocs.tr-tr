---
title: Microsoft Intune 'de Win32 uygulamalarında sorun giderme
titleSuffix: ''
description: Microsoft Intune ile kullanılan Win32 uygulama sorunlarını gidermek için en yaygın yöntemler hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aec8ebdd5d91e71c3706df906ce0b18f88edc02
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003455"
---
# <a name="troubleshoot-win32-app-issues"></a>Win32 uygulamasında sorun giderme

Microsoft Intune 'de kullanılan Win32 uygulamalarında sorun giderirken kullanabileceğiniz birkaç yöntem vardır. Bu konu, sorun giderme ayrıntılarının yanı sıra, Win32 uygulama sorunlarını çözmenize yardımcı olacak ek bilgiler sağlar.  [Win32 uygulaması yükleme sorunlarını giderme](troubleshoot-app-install.md#win32-app-installation-troubleshooting) kaynakları.

> [!NOTE]
> Bu uygulama yönetimi özelliği, Windows uygulamaları için hem 32-bit hem de 64-bit işletim sistemi mimarisini destekler.

> [!IMPORTANT]
> Win32 uygulamalarını dağıttığınızda, özellikle de çok sayfalı bir Win32 uygulaması yükleyicinizin olduğu durumlarda, [Intune yönetim uzantısı](../apps/intune-management-extension.md) yaklaşımını özel olarak kullanmayı düşünün. AutoPilot kaydı sırasında Win32 uygulamaları ve iş kolu uygulamaları yüklemesini karıştırırsanız, uygulama yüklemesi başarısız olabilir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza atandığında otomatik olarak yüklenir.

## <a name="app-troubleshooting-details"></a>Uygulama sorunlarını giderme ayrıntıları

Uygulamanın ne zaman yüklendiği, değiştirildiği, hedeflendiği ve bir cihaza teslim edildiği gibi yükleme sorunlarını görüntüleyebilirsiniz. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) , **sorun giderme + Destek** bölmesinde bu ve diğer ayrıntıları sağlar. Daha fazla bilgi için bkz. [uygulama sorun giderme ayrıntıları](troubleshoot-app-install.md#app-troubleshooting-details).

## <a name="troubleshoot-app-issues-using-logs"></a>Günlükleri kullanarak uygulama sorunlarını giderme

Günlüklerin ayrıntılarını görüntülemek, gördüğünüz sorunun nedenini belirlemenize yardımcı olabilir ve bunları çözmeye yardımcı olur. [Intune 'da görüntülenecek günlükleri](apps-win32-troubleshoot.md#logs-displayed-in-intune)görüntülemeyi veya [CMTrace kullanarak görüntülenecek günlükleri](apps-win32-troubleshoot.md#logs-displayed-using-cmtrace)görüntülemeyi seçebilirsiniz. 

### <a name="logs-displayed-in-intune"></a>Intune 'da görünen Günlükler

Bir Win32 uygulamasıyla ilgili yükleme sorunu oluştuğunda, Intune 'da uygulamanın **Yükleme ayrıntıları** bölmesinde **günlükleri topla** seçeneğini belirleyebilirsiniz. Daha fazla ayrıntı için bkz. [Win32 uygulama yükleme sorunlarını giderme](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-using-cmtrace"></a>CMTrace kullanılarak gösterilecek Günlükler

İstemci makinesindeki aracı günlükleri genellikle `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs` yolunda bulunur. Bu günlük dosyalarını görüntülemek için `CMTrace.exe` dosyasından yararlanabilirsiniz. Daha fazla bilgi için bkz. [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![İstemci makinesindeki aracı günlüklerinin ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> LOB Win32 uygulamalarının düzgün yüklenmesine ve yürütülmesine izin vermek için, kötü amaçlı yazılımdan koruma ayarları aşağıdaki dizinlerin taranmasını hariç tutmalıdır:<p>
> **X64 istemci makinelerde**:<br>
> *C:\Program Files (x86) \Microsoft Intune Management Extension\Content*<br>
> *C:\windows\ımecache*
>  
> **X86 istemci makinelerde**:<br>
> *C:\Program Files\Microsoft Intune yönetim Extension\Content*<br>
> *C:\windows\ımecache*
>
> Daha fazla bilgi için bkz. [Windows 'un şu anda desteklenen sürümlerini çalıştıran kurumsal bilgisayarlara yönelik virüs tarama önerileri](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## <a name="detecting-the-win32-app-file-version-using-powershell"></a>PowerShell kullanarak Win32 uygulama dosyası sürümü algılanıyor

Win32 uygulama dosyası sürümünü algılamayla karşılaşıyorsanız, aşağıdaki PowerShell komutunu kullanmayı veya değiştirmeyi düşünün:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

Yukarıdaki PowerShell komutunda, `<path to binary file>` dizeyi Win32 uygulama dosyanızın yoluyla değiştirin. Örnek bir yol aşağıdakine benzer olacaktır:<br>
`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Ayrıca, dizeyi, `<file version of successfully detected file>` algılamak için gereken dosya sürümü ile değiştirin. Örnek bir dosya sürümü dizesi aşağıdakine benzer:<br>
`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Win32 uygulamanızın sürüm bilgilerini almanız gerekiyorsa aşağıdaki PowerShell komutunu kullanabilirsiniz:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

Yukarıdaki PowerShell komutunda, öğesini `<path to binary file>` Dosya yolunuza göre değiştirin.

## <a name="additional-troubleshooting-areas-to-consider"></a>Dikkate alınması gereken ek sorun giderme alanı
- Aracının cihazda yüklü olduğundan emin olmak için hedefi denetleyin - Bir grubu hedefleyen Win32 uygulaması veya bir grubu hedefleyen PowerShell Betiği, güvenlik grubu için aracı yükleme ilkesi oluşturur.
- İşletim sistemi sürümünü denetleyin – Windows 10 1607 veya üzeri.  
- Windows 10 SKU'sunu denetleyin - Windows 10 S veya S modu etkinleştirilmiş olarak çalışan Windows sürümleri MSI yüklemesini desteklemez.

Win32 uygulamalarında sorun giderme hakkında daha fazla bilgi için bkz. [Win32 uygulama yükleme sorunlarını giderme](troubleshoot-app-install.md#win32-app-installation-troubleshooting). ARM64 cihazlarında uygulama türleri hakkında daha fazla bilgi için bkz. [ARM64 cihazlarında desteklenen uygulama türleri](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama yükleme sorunlarını giderin](troubleshoot-app-install.md).
