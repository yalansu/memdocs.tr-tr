---
title: Destek merkezini özelleştirme
titleSuffix: Configuration Manager
description: Destek Merkezi yapılandırma dosyasını özelleştirin.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc17437e508ea69a19043c29bf9ad4501cbac3e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078524"
---
# <a name="customize-support-center"></a>Destek merkezini özelleştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

[Destek Merkezi](support-center.md) Aracı, özelleştirebileceğiniz bir yapılandırma dosyası içerir. Varsayılan olarak, Destek Merkezi 'ni yüklediğinizde bu dosya şu yolda olur: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. Yapılandırma dosyası programın davranışını değiştirir:

- [Veri toplamayı Özelleştir](#bkmk_datacoll): veri toplama sırasında içerdiği kayıt defteri anahtarları ve WMI ad alanları kümelerini düzenleyin  

- [Günlük gruplarını Özelleştir](#bkmk_loggroups): normal ifadeler kullanarak yeni günlük dosyaları grupları tanımlayın. Ayrıca, günlük gruplarına diğer günlük dosyalarını da ekleyin.  

- [Joker karakterler kullanarak ek günlük dosyaları topla](#bkmk_wildcards): ek günlük dosyaları toplamak için joker aramaları kullanın  

Bu değişiklikleri yapmak için, destek merkezini yüklediğiniz istemcide yerel yönetici izinlerine sahip olmanız gerekir. Bu özelleştirmeleri Not defteri veya Visual Studio gibi bir metin veya XML Düzenleyicisi kullanarak yapın.

> [!Important]  
> Destek Merkezi yapılandırma dosyası XML biçimli bir dosyadır. Destek Merkezi 'nin çalışması önemlidir. Bu dosyanın değiştirilmesi yalnızca XML ve normal ifadelerle bilinen kullanıcılar için önerilir.  

Destek Merkezi yapılandırma dosyasını özelleştirebilmeniz için özgün dosyanın bir yedeğini kaydedin. Bu yedekleme, dosyayı düzenlenirken hatalar yaparsanız özgün Destek Merkezi işlevlerini kurtarmanıza izin verir. Bir yedekleme oluşturmazsanız ve yapılandırma dosyasını değiştirdikten sonra destek merkezi düzgün şekilde çalışmazsa, destek merkezini yeniden yükleyin. Ayrıca, bir yapılandırma dosyasını başka bir destek merkezi yüklemesinden de kopyalayabilirsiniz.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a>Veri toplamayı Özelleştir

İstemcideki verilerin koleksiyonunu özelleştirmek için, `<dataCollectorSettings>` öğesinde yer alan XML öğelerini kullanarak destek merkezi yapılandırma dosyasını değiştirin.


### <a name="wmi-data-collection"></a>WMI veri toplama

`<CcmWmiDataCollector>` Öğesi bir `<collectionScopes>` öğesi içerir. Destek Merkezi 'nin veri topladığı WMI ad alanlarını değiştirmek için bu öğeyi kullanın. Ayrıca bir `<ignoreScopes>` öğesi de içerir. `<collectionScopes>` Öğesinde tanımlanan ad alanları bölümlerinden veri toplamayı filtrelemek için bu öğeyi kullanın.  
    
#### <a name="example"></a>Örnek
Varsayılan yapılandırma dosyası, `root\ccm` ad alanından veri toplar. Bu yolu içindeki `<add/>` `<collectionScopes>`bir öğesinde içerir. 

Ayrıca `\cimodels`, bu ad alanı için, `\invagt` `\events`, ve `\policy` yollarının altındaki her şeyi yoksayar. Bu yollar içinde `<ignoreScopes>`yer alan `<add/>` öğelerde bulunur.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Kayıt defteri verileri toplama

`<RegistryDataCollector>` Öğesi bir `<registryKeys>` öğesi içerir. Destek Merkezi 'nin `HKEY_LOCAL_MACHINE` yol altında topladığı kayıt defteri anahtarlarını ve alt anahtarlarını değiştirmek için bu öğeyi kullanın. Destek Merkezi, diğer kök kayıt defteri yollarından kayıt defteri verilerinin toplanmasını desteklemez.

#### <a name="example"></a>Örnek
Cihazda yüklü olan klasik programların kayıt defteri anahtarlarını toplamak için, aşağıdaki `<add/>` öğesini `<registryKeys>` öğesine ekleyin:`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a>Günlük dosyası gruplarını özelleştirme

Destek Merkezi 'nin hangi günlük dosyalarının topladığı ve bunları **günlük grupları** listesinde nasıl sunmakta olduğunu özelleştirmek için, `<logGroups>` öğesindeki öğeleri kullanın. Destek Merkezi 'ni başlattığınızda, yapılandırma dosyasının bu bölümünü tarar. Daha sonra, `<add/>` `<logGroups>` öğesinde yer alan öğelerde bulunan her benzersiz anahtar öznitelik değeri için **günlük grupları** listesinde bir grup oluşturur.

- **Bileşen günlük grubu**: `<componentLogGroup>` öğesi, listede görüntülenen günlük grubunun adını tanımlamak için bir anahtar özniteliği kullanır. Ayrıca, normal ifade (Regex) içeren bir değer özniteliği kullanır. Bu, bir dizi ilgili günlük dosyasını toplamak için bu Regex kullanır.  

- **Statik günlük grubu:** `<staticLogGroup>` Öğesi, listede görüntülenen günlük grubunun adını tanımlamak için bir anahtar özniteliği kullanır. Ayrıca, bir günlük dosyası adını tanımlayan bir değer özniteliği kullanır.  

Aynı anahtar özniteliği değeri hem `<add/>` `<componentLogGroup>` öğesi hem de `<staticLogGroup>` öğesi Içindeki bir öğede kullanılıyorsa, destek merkezi tek bir grup oluşturur. Bu grup, aynı anahtarı kullanan her iki öğe tarafından tanımlanan günlük dosyalarını içerir.

#### <a name="example"></a>Örnek
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a>Joker karakterler kullanarak ek günlük dosyaları toplama

Ek günlük dosyaları toplamak için dosya yolu veya dosya adında joker karakterler kullanın. Bu joker karakterler gibi sistem genelindeki ortam değişkenlerini içerir `%WINDIR%`, ancak gibi kullanıcı kapsamlı ortam değişkenlerini hariç tutar. `%USERPROFILE%` Bu özyinelemeli olmayan günlük dosyası aramasını kullanarak ek günlük dosyaları toplamak için `<add/>` `<additionalLogFiles>` öğesi içindeki bir öğesi kullanın. 

Bu örneklerde, Destek Merkezi 'nin bu özelliği varsayılan yapılandırma dosyasında nasıl kullandığı gösterilmektedir.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Örnek 1: tüm Windows Update günlük dosyalarını Windows dizininde topla
Aşağıdaki öğe, Windows dizininde bulunan adlı `WindowsUpdate.log` tüm dosyaları toplar: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Örnek 2: Windows günlükleri dizinindeki tüm günlük dosyalarını toplama
Aşağıdaki öğe, Windows günlükleri dizininde `.log` bulunan ile biten tüm dosyaları toplar: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Tam örnek XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
