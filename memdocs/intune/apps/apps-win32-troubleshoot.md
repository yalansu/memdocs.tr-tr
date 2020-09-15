---
title: Microsoft Intune 'de Win32 uygulamalarında sorun giderme
titleSuffix: ''
description: Microsoft Intune ile ilgili Win32 uygulama sorunlarını gidermek için en yaygın yöntemler hakkında bilgi edinin.
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
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083922"
---
# <a name="troubleshoot-win32-app-issues"></a>Win32 uygulamasında sorun giderme

Microsoft Intune ' de kullanılan Win32 uygulamalarında sorun giderirken, çeşitli yöntemler kullanabilirsiniz. Bu makalede, Win32 uygulama sorunlarını çözmenize yardımcı olacak sorun giderme ayrıntıları ve bilgiler sağlanmaktadır. Daha fazla bilgi için bkz. [Win32 uygulama yüklemesi sorun giderme](troubleshoot-app-install.md#win32-app-installation-troubleshooting) kaynakları.

> [!NOTE]
> Bu uygulama yönetimi özelliği, Windows uygulamaları için hem 32-bit hem de 64-bit işletim sistemi mimarilerini destekler.

> [!IMPORTANT]
> Win32 uygulamaları dağıttığınızda, özellikle de çok sayfalı bir Win32 uygulaması yükleyicinizin olduğu durumlarda [Intune yönetim uzantısı](../apps/intune-management-extension.md) yaklaşımını özel olarak kullanmayı düşünün. AutoPilot kaydı sırasında Win32 uygulamaları ve iş kolu (LOB) uygulamaları yüklemesini karıştırırsanız, uygulama yüklemesi başarısız olabilir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza atandığında otomatik olarak yüklenir.

## <a name="app-troubleshooting-details"></a>Uygulama sorunlarını giderme ayrıntıları

Uygulamanın ne zaman yüklendiği, değiştirildiği, hedeflendiği ve bir cihaza teslim edildiği gibi yükleme sorunlarını görüntüleyebilirsiniz. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) , **sorun giderme + Destek** bölmesinde bu ve diğer ayrıntıları sağlar. Daha fazla bilgi için bkz. [uygulama sorun giderme ayrıntıları](troubleshoot-app-install.md#app-troubleshooting-details).

## <a name="troubleshooting-app-issues-by-using-logs"></a>Günlükleri kullanarak uygulama sorunlarını giderme

Günlüklerin ayrıntılarını görüntülemek, gördüğünüz sorunların nedenini belirlemenize ve bunları çözmenize yardımcı olabilir. [Intune 'da görüntülenecek günlükleri](apps-win32-troubleshoot.md#logs-displayed-in-intune)görüntülemeyi veya [CMTrace aracılığıyla görüntülenecek günlükleri](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace)görüntülemeyi seçebilirsiniz. 

### <a name="logs-displayed-in-intune"></a>Intune 'da görünen Günlükler

Bir Win32 uygulamasıyla ilgili yükleme sorunu oluştuğunda, Intune 'da uygulamanın **Yükleme ayrıntıları** bölmesinde **günlükleri topla** seçeneğini belirleyebilirsiniz. Daha fazla ayrıntı için bkz. [Win32 uygulama yükleme sorunlarını giderme](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-through-cmtrace"></a>CMTrace aracılığıyla gösterilecek Günlükler

İstemci makinesindeki Aracı günlükleri genellikle *C:\programdata\microsoft\ıntunemanagemenısion\logs*konumundadır. Bu günlük dosyalarını görüntülemek için *CMTrace.exe* kullanabilirsiniz. Daha fazla bilgi için bkz. [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![İstemci makinesindeki aracı günlüklerinin ekran görüntüsü.](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> LOB Win32 uygulamalarının düzgün şekilde yüklenmesine ve yürütülmesine izin vermek için, kötü amaçlı yazılımdan koruma ayarları aşağıdaki dizinlerin taranarak dışlanmalıdır:<p>
> **X64 istemci makinelerde**:<br>
> *C:\Program Files (x86) \Microsoft Intune Management Extension\Content*<br>
> *C:\windows\ımecache*
>  
> **X86 istemci makinelerde**:<br>
> *C:\Program Files\Microsoft Intune yönetim Extension\Content*<br>
> *C:\windows\ımecache*
>
> Daha fazla bilgi için bkz. [Windows 'un şu anda desteklenen sürümlerini çalıştıran kurumsal bilgisayarlara yönelik virüs tarama önerileri](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>PowerShell kullanarak Win32 uygulama dosyası sürümünü algılama

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

Önceki PowerShell komutunda, `<path to binary file>` dizesini Win32 uygulama dosyanızın yoluyla değiştirin. Örnek bir yol aşağıdakine benzer olacaktır:

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Ayrıca, dizeyi, `<file version of successfully detected file>` algılamak için gereken dosya sürümü ile değiştirin. Örnek bir dosya sürümü dizesi aşağıdakine benzer:

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Win32 uygulamanızın sürüm bilgilerini almanız gerekiyorsa aşağıdaki PowerShell komutunu kullanabilirsiniz:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

Önceki PowerShell komutunda, öğesini `<path to binary file>` Dosya yolunuza göre değiştirin.

## <a name="additional-troubleshooting-areas-to-consider"></a>Dikkate alınması gereken ek sorun giderme alanı
- Aracının cihaza yüklendiğinden emin olmak için hedef denetimi yapın. Bir gruba veya bir gruba hedeflenmiş bir PowerShell betiğine hedeflenmiş bir Win32 uygulaması, bir güvenlik grubu için bir aracı yükleme ilkesi oluşturacaktır.
- İşletim sistemi sürümünü denetleyin: Windows 10 1607 ve üzeri.  
- Windows 10 SKU 'sunu denetleyin. Windows 10 S veya S modu etkinken çalışan Windows sürümleri, MSI yüklemesini desteklemez.

Win32 uygulamalarında sorun giderme hakkında daha fazla bilgi için bkz. [Win32 uygulama yükleme sorunlarını giderme](troubleshoot-app-install.md#win32-app-installation-troubleshooting). ARM64 cihazlarında uygulama türleri hakkında daha fazla bilgi için bkz. [ARM64 cihazlarında desteklenen uygulama türleri](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama yükleme sorunlarını giderme](troubleshoot-app-install.md)
