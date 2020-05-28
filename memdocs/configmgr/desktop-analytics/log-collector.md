---
title: Günlük toplayıcı
titleSuffix: Configuration Manager
description: Masaüstü Analizi sorunlarını gidermeye yardımcı olması için Günlükler toplayıcı aracını kullanma
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8782913e40bffdcbe5a151fac8821f05b7e7fece
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268581"
---
# <a name="desktop-analytics-log-collector"></a>Masaüstü Analizi Günlük Toplayıcısı

Configuration Manager sürüm 1906 ' den başlayarak, masaüstü Analizi cihaz kayıt sorunlarını gidermeye yardımcı olması için Configuration Manager install dizininden **DesktopAnalyticsLogsCollector. ps1** aracını kullanın. Bazı temel sorun giderme adımlarını çalıştırır ve ilgili günlükleri tek bir çalışma dizininde toplar. Bu içeriği Microsoft desteği ile paylaşabilirsiniz.


## <a name="prerequisites"></a>Ön koşullar

- Windows 10, Windows 8.1 veya Windows 7 Service Pack 1 çalıştıran bir masaüstü Analizi istemcisi

- Betiği cihazda yönetici kullanıcı olarak çalıştırın ve **yönetici olarak çalıştırın**.

    > [!Tip]
    > Configuration Manager **betikleri** özelliğini bu araçla birlikte kullanabilirsiniz. Daha fazla bilgi için bkz. [örnek 5: betiği Configuration Manager **betikler**aracılığıyla dağıtma](#bkmk_ex5).

- Windows 7 Service Pack 1, PowerShell sürüm 4,0 veya üzeri için
    - [.NET Framework sürüm 4,6 veya üzeri](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [sürüm 4,0](https://support.microsoft.com/help/2819745) (aka.MS/wmf4download) veya [sürüm 5,1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.MS/wmf5download)

## <a name="usage"></a>Kullanım

Configuration Manager yükleme içeriğinden betiği alın:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parametreler

### `-LogPath`

Günlüğü ve diğer çıkış dosyalarını yerleştirmek için bir yerel veya UNC yolu belirtir.

**Değerler**:

- Yerel yol (maksimum uzunluk = 130), örneğin:`c:\myfolder`

- UNC yolu (maksimum uzunluk = 130), örneğin:`\\myserver\myfolder`

**Tür**: dize

**Konum**: 1

**Varsayılan değer**: `$Env:SystemDrive\M365AnalyticsLogs` (Bu parametre null, boş veya boşluk olduğunda, komut dosyası sistem sürücüsünün altında M365AnalyticsLogs klasörünü oluşturur.)

### `-LogMode`

Günlüklerin ayrıntı düzeyini belirtir.

**Değerler**:

- `0`: Betik iletilerini yalnızca PowerShell komut penceresinde günlüğe kaydedin.

- `1`: Çıkış klasörü ve PowerShell komut penceresi altındaki günlük dosyasına komut dosyası iletilerini günlüğe kaydedin.

- `2`: Günlük dosyası iletilerini yalnızca çıkış klasörü altında günlüğe kaydedin.

**Tür**: Int16

**Konum**: 2

**Varsayılan değer**: `1` (komut dosyası iletilerini hem günlük dosyasına hem de PowerShell komut penceresine kaydeder.)

### `-CollectNetTrace`

Betiğin ağ izlemesini toplayıp toplamayacağını belirtir.

**Değerler**:

- `0`: Ağ izlemesini etkinleştirmeyin.

- `1`(sıfır olmayan herhangi bir tamsayı değeri): ağ izlemesini etkinleştirin ve sonuçları toplayın.

**Tür**: Int16

**Konum**: 3

**Varsayılan değer**: `0` (ağ izlemesini etkinleştirmeyin)

### `-CollectUTCTrace`

Betiğin Windows UTC izleme ve çalıştırma bağlantısı tanılaması 'nı toplayıp toplamayacağını belirtir.

**Değerler**:

- `0`: UTC izlemeyi etkinleştirmeyin ya da bağlantı tanılama 'yı çalıştırın.

- `1`(sıfır olmayan herhangi bir tamsayı değeri): UTC izlemesini etkinleştirin, bağlantı tanılama 'yı çalıştırın ve sonuçları toplayın.

**Tür**: Int16

**Konum**: 4

**Varsayılan değer**: `0` (UTC izlemeyi etkinleştirmeyin veya bağlantı tanısı ' i çalıştırın)


## <a name="output"></a>Çıktı

Betik, belirtilen yolun altında bir *çalışma klasörü* oluşturur. Örneğin, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Tüm çıktı dosyalarını bu çalışma klasörüne koyar.

Komut dosyasını bir *günlük dosyasına*yazmak üzere etkinleştirirseniz, çalışma klasöründe bir tane oluşturur. Örneğin, **yy_MM_dd_HH_mm_ss. txt M365AnalyticsLogs_**.

Betik Ayrıca çalışma klasöründe diğer *Tanılama dosyalarını* da oluşturur. Örneğin:

- `installedKBs.txt`: cihazda yüklü olan Windows güncelleştirmelerinin listesi
- `appcompat`: uygulama uyumluluk verileri
- `Reg*.txt`: Windows kayıt defterinden aktarılmış verileri içeren bir dizi dosya


## <a name="examples"></a>Örnekler

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a>Örnek 1: PowerShell komut penceresi aracılığıyla betiği varsayılan değerlerle Çalıştır

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a>Örnek 2: PowerShell komut penceresi aracılığıyla betiği belirtilen parametrelerle Çalıştır

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a>Örnek 3: konum içinde belirtilen parametrelerle PowerShell komut penceresi aracılığıyla betiği çalıştırın

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a>Örnek 4: belirtilen parametre ve ayrıntılı iletilerle PowerShell komut penceresi aracılığıyla betiği çalıştırın

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a>Örnek 5: betiği Configuration Manager **betikler** aracılığıyla dağıtın

Daha fazla bilgi için, bkz. [Configuration Manager konsolundan PowerShell betikleri oluşturma ve çalıştırma](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector. ps1, Microsoft tarafından dijital olarak imzalanır. Microsoft kod imzalama sertifikasını, hedef cihaza güvenilir bir yayımcı olarak eklemeniz gerekebilir.

1. Windows Gezgini 'nde betiğin özelliklerini açın. **Dijital imzalar** sekmesine geçin ve **Ayrıntılar**' ı seçin.

2. **Genel** sekmesinde, **sertifikayı görüntüle**' yi seçin.

    > [!Note]
    > Sertifikayı diğer mekanizmalarla dağıtmak için öncelikle sertifikayı bir dosyaya dışarı aktarın. **Ayrıntılar** sekmesine gidin ve **Dosyaya Kopyala**' yı seçin.

3. **Sertifika yüklemeyi**seçin. Sertifikayı, **Güvenilen Yayımcılar** deposuna yerleştirerek içeri aktarın.


## <a name="see-also"></a>Ayrıca bkz.

- [Desktop Analytics sorunlarını giderme](troubleshooting.md)

- [Configuration Manager konsolundan PowerShell betikleri oluşturun ve çalıştırın](../apps/deploy-use/create-deploy-scripts.md)
