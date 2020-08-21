---
title: Internet bağlantısı olmadan Microsoft 365 Apps güncelleştirmelerini eşitler
titleSuffix: Configuration Manager
description: Internet bağlantısı kesilen en üst düzey yazılım güncelleştirme noktasında Microsoft 365 Apps güncelleştirmelerini eşitler.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 49e0f5e1dff466e62cdba0def917dd34510e48ee
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696778"
---
# <a name="synchronize-microsoft-365-apps-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a> Bağlantısı kesilmiş bir yazılım güncelleştirme noktasından Microsoft 365 Apps güncelleştirmelerini eşitler

*Uygulama hedefi: Configuration Manager (geçerli dal)*
<!--4065163-->
Configuration Manager sürüm 2002 ' den başlayarak, internet 'e bağlı bir WSUS sunucusundan Microsoft 365 uygulama güncelleştirmelerini, bağlantısı kesilen Configuration Manager ortamına aktarmak için bir araç kullanabilirsiniz. Daha önce, bağlantısı kesilen ortamlarda güncelleştirilmiş yazılım için meta verileri verildiğinde ve içeri aktardığınızda Microsoft 365 Apps güncelleştirmelerini dağıtamazsınız. Microsoft 365 uygulamalar güncelleştirmeleri, bir Office API 'sinden ve Office CDN 'den indirilen, bağlantısı kesilen ortamlar için mümkün olmayan ek meta veriler gerektirir.

> [!Note]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

- En az Windows Server 2012 çalıştıran, internet 'e bağlı bir WSUS sunucusu.
- WSUS sunucusunun bu iki Internet uç noktasına bağlanması gerekir:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Offlineupdatedışarı aktarıcı aracını ve bağımlılıklarını Internet 'e bağlı WSUS sunucusuna kopyalayın.
  - Araç ve bağımlılıkları ** &lt; configmgrınstalldir>/Tools/offlineupdatevericisi** dizininde bulunur.
- Aracı çalıştıran kullanıcının **WSUS yöneticileri** grubunun bir parçası olması gerekir.
- Microsoft 365 uygulamalar güncelleştirme meta verilerini ve içeriğini depolamak için oluşturulan dizin, dosyaların güvenliğini sağlamak için uygun erişim denetim listelerine (ACL 'Ler) sahip olmalıdır.
    - Bu dizin de boş olmalıdır.
- Çevrimiçi WSUS sunucusundan bağlantısı kesilen ortama taşınan veriler güvenli bir şekilde taşınmalıdır.

> [!IMPORTANT]
> Tüm Microsoft 365 Apps dilleri için içerik indirilir. Her güncelleştirmede yaklaşık 10 GB içerik bulunabilir.

## <a name="synchronize-then-decline-unneeded-microsoft-365-apps-updates"></a>Daha sonra gerekli olmayan Microsoft 365 Apps güncelleştirmelerini eşitler

1. İnternet 'e bağlı WSUS ' da WSUS konsolunu açın.
1. **Seçenekler** **, ürünler ve sınıflandırmalar '** ı seçin.
1. **Ürünler** sekmesinde **Office 365 istemcisi** ' ni seçin ve **sınıflandırmalar** SEKMESINDE **güncelleştirmeler** ' i seçin. [ ![ WSUS 'de Microsoft 365 Apps güncelleştirmeleri için ürünler ve sınıflandırmalar](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Microsoft 365 uygulamalarının WSUS 'e güncelleştirmelerini almak için **eşitlemeler** 'e gidin ve **Şimdi eşitleme** ' yi seçin.
1. Eşitleme tamamlandığında, Configuration Manager dağıtmak istemediğiniz Microsoft 365 Apps güncelleştirmelerini reddedin. İndirilmeleri için Microsoft 365 uygulama güncelleştirmelerini onaylamanız gerekmez.  
   - İstenmeyen Microsoft 365 uygulama güncelleştirmelerinin, WSUS 'ta WsusUtil.exe dışarı aktarma sırasında dışarı aktarılmasını durdurmaz, ancak Offlineupdatedışarı aktarıcı aracının içerikleri karşıdan yüklemesini durdurur.
   - Offlineupdatedışarı aktarma aracı, Microsoft 365 Apps güncelleştirmelerini sizin için indirir. Bunlar için güncelleştirmeleri dışarı aktarıyorsanız diğer ürünlerin da indirilmek üzere onaylanması gerekir.
    - WSUS 'ta gereksiz Microsoft 365 Apps güncelleştirmelerini kolayca görmek ve reddetmek için [WSUS 'ta yeni bir güncelleştirme görünümü](/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) oluşturun.
1. Karşıdan yükleme ve dışarı aktarma için diğer ürün güncelleştirmelerini onayladıysanız, sunucusundaki WSUSContent klasörünün içeriğini WsusUtil.exe dışarı ve kopyalama işlemini çalıştırmadan önce içerik indirmenin tamamlanmasını bekleyin. Daha fazla bilgi için bkz. [bağlantısı kesilmiş bir yazılım güncelleştirme noktasından yazılım güncelleştirmelerini senkronize](synchronize-software-updates-disconnected.md) etme

## <a name="exporting-the-microsoft-365-apps-updates"></a>Microsoft 365 Apps güncelleştirmelerini dışarı aktarma

1. Offlineupdatedışarı aktarıcı klasörünü Configuration Manager ' dan Internet 'e bağlı WSUS sunucusuna kopyalayın.
    - Araç ve bağımlılıkları ** &lt; configmgrınstalldir>/Tools/offlineupdatevericisi** dizininde bulunur.
1. Internet 'e bağlı WSUS sunucusunda bir komut isteminden, aracı şu kullanımla çalıştırın: **OfflineUpdateExporter.exe-O-D &lt; hedef yolu>**

   |Offlineupdatedışarı aktarıcı parametresi|Açıklama|
   |---|---|
   |**-O**|  **-Office**. Güncelleştirmeler için ürünü belirtir Office 365 veya Microsoft 365 Apps|
   |**-D**|**-Hedef**. Hedef, gerekli bir parametredir ve hedef klasörün tüm yolu gereklidir.|

   - **Offlineupdatedışarı aktarma** Aracı şunları yapar:
      - WSUS 'a bağlanır
      - WSUS 'de Microsoft 365 Apps güncelleştirme meta verilerini okur
      - Microsoft 365 Apps güncelleştirmelerinin gerektirdiği içeriği ve ek meta verileri hedef klasöre indirir

1. Internet 'e bağlı WSUS sunucusunda komut isteminde WsusUtil.exe içeren klasöre gidin. Araç, varsayılan olarak%*ProgramFiles*% \ Update Services\Tools konumunda bulunur. Örneğin, araç varsayılan konumda bulunuyorsa **cd %ProgramFiles%\Update Services\Tools**yazın.
   - Windows Server 2012 kullanıyorsanız, [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) WSUS sunucularında yüklü olduğundan emin olun.
   - WsusUtil aracını çalıştıran kullanıcı, sunucuda yerel Yöneticiler grubunun bir üyesi olmalıdır.

1. Yazılım güncelleştirme meta verilerini bir GZIP dosyasına aktarmak için aşağıdakileri yazın:  

    **WsusUtil.exe***PackageName**logfile dosyasını* dışarı aktar      

    Örnek:  

    **WsusUtil.exe dışarı aktarma export.xml. gz Export. log**

1. **export.xml. gz** dosyasını, bağlantısı kesilen ağdaki en üst düzey WSUS sunucusuna kopyalayın.
1. Diğer ürünler için güncelleştirmeleri onayladıysanız, sunucusundaki WSUSContent klasörünün içeriğini üst düzey bağlantısı kesilen WSUS sunucusunun sunucusundaki WSUSContent klasörüne kopyalayın.
1. **Offlineupdatevericisi** için kullanılan hedef klasörü, bağlantısı kesilen ağdaki en üst düzey Configuration Manager site sunucusuna kopyalayın.

## <a name="import-the-microsoft-365-apps-updates"></a>Microsoft 365 Apps güncelleştirmelerini içeri aktarma

1. Bağlantısı kesilmiş üst düzey WSUS sunucusunda, internet 'e bağlı WSUS sunucusunda oluşturduğunuz **export.xml. gz** ' den güncelleştirme meta verilerini alın.
   
    Örnek:  

    **WsusUtil.exe içeri aktarma export.xml. gz Import. log**
    
    Varsayılan olarak, WsusUtil.exe aracı%*ProgramFiles*% \ Update Services\Tools konumunda bulunur.

1. İçeri aktarma işlemi tamamlandıktan sonra, bağlantısı kesik üst düzey Configuration Manager site sunucusunda bir site denetim özelliği yapılandırmanız gerekir. Bu yapılandırma değişikliği noktaları Microsoft 365 uygulamalar için içeriğe Configuration Manager. Özelliğin yapılandırmasını değiştirmek için:
   1. [O365OflBaseUrlConfigured PowerShell betiğini](#bkmk_o365_script) en üst düzey bağlantısı kesilen Configuration Manager site sunucusuna kopyalayın.
   1. `"D:\Office365updates\content"`Microsoft 365 Apps içeriğini ve Offlineupdateverme tarafından oluşturulan meta verileri içeren kopyalanmış dizinin tam yoluna geçin.
      > [!IMPORTANT]
      > O365OflBaseUrlConfigured özelliği için yalnızca yerel yollar çalışır.
   1. Betiği şu şekilde Kaydet `O365OflBaseUrlConfigured.ps1`
   1. Bağlantısı kesilmiş üst düzey Configuration Manager site sunucusundaki yükseltilmiş bir PowerShell penceresinden, öğesini çalıştırın `.\O365OflBaseUrlConfigured.ps1` .
   1. Site sunucusunda **SMS_Executive** hizmetini yeniden başlatın.
1. **Configuration Manager** konsolunda, **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin.
1. Üst düzey sitenize sağ tıklayın ve ardından **site bileşenlerini Yapılandır**  >  **yazılım güncelleştirme noktası**' nı seçin.
1. **Sınıflandırmalar** sekmesinde *güncelleştirmeler*' i seçin. **Ürünler** sekmesinde *Office 365 istemcisi*' ni seçin.
1. Configuration Manager için [yazılım güncelleştirmelerini eşitler](synchronize-software-updates.md#manually-start-software-updates-synchronization)
1. Eşitleme tamamlandığında, Microsoft 365 Apps güncelleştirmelerini dağıtmak için normal işleminizi kullanın.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a> Ara sunucu yapılandırması

- Proxy yapılandırması, araçta yerel olarak yerleşik değildir. Proxy, aracın çalıştığı sunucudaki Internet seçeneklerinde ayarlandıysa, teorik olarak kullanılır ve düzgün şekilde çalışır.
   - Bir komut isteminden, `netsh winhttp show proxy` yapılandırılan proxy 'yi görmek için komutunu çalıştırın.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a> O365OflBaseUrlConfigured özelliğini değiştir

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Sonraki adımlar

[Yazılım güncelleştirmelerini güncelleştirme grubuna ekleme](../deploy-use/add-software-updates-to-an-update-group.md)