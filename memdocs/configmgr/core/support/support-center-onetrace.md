---
title: Destek Merkezi OneTrace (Önizleme)
titleSuffix: Configuration Manager
description: OneTrace, CMTrace üzerinde geliştirmeler içeren destek merkezi 'Ni içeren yeni bir günlük görüntüleyicisine sahiptir.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723113"
---
# <a name="support-center-onetrace-preview"></a>Destek Merkezi OneTrace (Önizleme)

<!--3555962-->

Sürüm 1906 ' den başlayarak OneTrace, Destek Merkezi 'nin bulunduğu yeni bir günlük görüntüleyicisine sahiptir. Aşağıdaki geliştirmelerle CMTrace 'e benzer şekilde çalışır:

- Sekmeli Görünüm
- Dockable Windows
- Geliştirilmiş arama özellikleri
- Günlük görünümünden çıkmadan filtreleri etkinleştirebilme
- Hata kümelerini hızlı bir şekilde tanımlamak için kaydırma çubuğu ipuçları
- Büyük dosyalar için hızlı günlük açma

[![OneTrace günlük görüntüleyicisinin ekran görüntüsü](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace, şöyle birçok günlük dosyası türüyle çalışmaktadır:

- Configuration Manager istemci günlükleri
- Sunucu günlükleri Configuration Manager
- Durum iletileri
- Windows 10 ' da ETW günlük dosyası Windows Update
- Windows 7 & Windows Update günlük dosyası Windows 8.1

## <a name="prerequisites"></a>Ön koşullar

- .NET Framework sürüm 4,6 veya üzeri

## <a name="install"></a>Yükleme

OneTrace, Destek Merkezi ile yüklenir. Site sunucusunda aşağıdaki yolda bulunan destek merkezi yükleyicisini bulun: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Varsayılan olarak, OneTrace uygulaması konumunda yüklüdür `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe` .

> [!Note]  
> Destek Merkezi ve OneTrace Windows Presentation Foundation (WPF) kullanır. Bu bileşen Windows PE 'de kullanılamaz. Görev sırası dağıtımlarıyla önyükleme görüntülerinde CMTrace 'i kullanmaya devam edin.  

## <a name="log-groups"></a>Günlük grupları

<!--5559993-->

Sürüm 2002 ' den başlayarak OneTrace, Destek Merkezi 'ndeki özelliğe benzer şekilde özelleştirilebilir günlük gruplarını destekler. Günlük grupları, tek bir senaryo için tüm günlük dosyalarını açmanıza olanak tanır. OneTrace Şu anda aşağıdaki senaryolar için gruplar içermektedir:

- Uygulama yönetimi
- Uyumluluk ayarları (Istenen yapılandırma yönetimi olarak da adlandırılır)
- Yazılım güncelleştirmeleri

Günlük gruplarını göstermek için **Görünüm** menüsüne gidin ve **günlük grupları**' nı seçin.

![Uygulama yönetimi için OneTrace günlük grubunun ekran görüntüsü](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Günlük gruplarını Özelleştir

Bu grupları, varsayılan olarak aşağıdaki yolda olan yapılandırma XML 'sini değiştirerek özelleştirebilirsiniz: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml` .

Aşağıdaki örnek, varsayılan yapılandırma dosyasının bir parçasıdır:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

`GroupType`Özelliği aşağıdaki değerleri kabul eder:

- `0`: Bilinmiyor veya diğer
- `1`: Configuration Manager istemci günlükleri
- `2`: Configuration Manager sunucusu günlükleri

`GroupFilePath`Özelliği, günlük dosyaları için açık bir yol içerebilir. Boşsa OneTrace, Grup türü için kayıt defteri yapılandırmasına bağımlıdır. Örneğin, ayarlarsanız `GroupType=1` , varsayılan olarak OneTrace, gruptaki günlüklere otomatik olarak bakar `C:\Windows\CCM\Logs` . Bu örnekte, belirtmeniz gerekmez `GroupFilePath` .

## <a name="see-also"></a>Ayrıca bkz.

- [Destek Merkezi günlük Görüntüleyici](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
