---
title: Uygulama başına VPN için bir paket aile adı (PFN) bulma
titleSuffix: Configuration Manager
description: Uygulama başına VPN 'yi yapılandırabilmeniz için bir paket aile adı bulmanın iki yolu hakkında bilgi edinin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f109e4ea4bee4a1de767508d62bc3f080d24f625
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715609"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Uygulama başına VPN için bir paket aile adı (PFN) bulma

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Uygulama başına VPN’yi yapılandırabilmek için bir PFN bulmanın iki yolu vardır.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Windows 10 bilgisayarında yüklü bir uygulama için PFN bulma

Üzerinde çalıştığınız uygulama zaten bir Windows 10 bilgisayarında yüklüyse, PFN’yi almak için [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) PowerShell cmdlet’ini kullanabilirsiniz.

Get-AppxPackage cmdlet’inin söz dizimi:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> PFN 'yi alabilmek için PowerShell 'i yönetici olarak çalıştırmanız gerekebilir

Örneğin, bilgisayarda yüklü tüm evrensel uygulamalarla ilgili bilgileri almak için `Get-AppxPackage` kullanın.

Adının tamamını veya bir kısmını bildiğiniz uygulamayla ilgili bilgileri almak için `Get-AppxPackage *<app_name>` kullanın. Uygulamanın tam adını bilmediğiniz durumlarda joker karakter kullanmanın özellikle çok yararlı olduğunu aklınızda bulundurun. Örneğin, OneNote’la ilgili bilgi almak için `Get-AppxPackage *OneNote` kullanın.


OneNote için şu bilgiler alınır:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Uygulama bilgisayarda yüklü olmadığında bir PFN bulma

1. Şuraya gidin: https://www.microsoft.com/store/apps
2. Arama çubuğuna uygulamanın adını girin. Bizim örneğimizde, OneNote için arama yapın.
3. Uygulamanın bağlantısına tıklayın. Eriştiğiniz URL’nin sonunda bir dizi harf olduğuna dikkat edin. Örneğimizde URL şöyle görünür:`https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. Farklı bir sekmede, aşağıdaki URL `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`'yi yapıştırın ve adım 3 ' `<app id>` te URL 'nin sonundaki bu dizi harften https://www.microsoft.com/store/apps aldığınız uygulama kimliğiyle değiştirin. Bizim Outlook örneğimizde, şunu yapıştırırsınız: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

Microsoft Edge’de istediğiniz bilgi görüntülenir; Internet Explorer’da bilgileri görmek için **Aç**’a tıklayın. PFN değeri ilk satırda verilir. Bizim örneğimizde sonuçlar şöyle görünür:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
