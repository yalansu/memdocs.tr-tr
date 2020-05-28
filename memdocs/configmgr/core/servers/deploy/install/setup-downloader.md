---
title: Kurulum yükleyici aracı
titleSuffix: Configuration Manager
description: Kurulum için anahtar yükleme dosyalarının güncel sürümlerini indirmek için tek başına aracını kullanın.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428845"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager için kurulum yükleyicisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir siteyi yüklemek veya yükseltmek üzere Configuration Manager kurulumunu çalıştırmadan önce, güncelleştirilmiş Kurulum dosyalarını indirmek için kurulum yükleyici tek başına aracını kullanabilirsiniz. Aracı yüklemek istediğiniz Configuration Manager sürümünden çalıştırın. Site yüklemenizin, anahtar yükleme dosyalarının güncel sürümlerini kullandığından emin olmak için güncelleştirilmiş Kurulum dosyalarını kullanın.

Kurulum Yükleyici 'yi kullandığınızda, dosyaları içerecek bir klasör belirtirsiniz. Aracı çalıştırmak için kullandığınız hesabın, indirme klasörü üzerinde **tam denetim** izinlerine sahip olması gerekir. Bir siteyi yüklemek veya yükseltmek için kurulum 'u çalıştırdığınızda, daha önce indirdiğiniz dosyaların bu yerel kopyasını belirtebilirsiniz. Bu davranış, site yükleme veya yükseltme ' ye başladığınızda kurulum 'un Microsoft 'a bağlanmasını engeller. Aynı sürüme ait diğer site yüklemeleri veya yükseltmeleri için kurulum dosyalarının aynı yerel kopyasını kullanabilirsiniz.

Kurulum yükleyici aracı aşağıdaki dosya türlerini indirir:

- Gerekli önkoşul yeniden dağıtılabilir dosyaları
- Dil paketleri
- Kurulum için en son ürün güncelleştirmeleri

Kurulum Yükleyici 'yi çalıştırmak için iki seçeneğiniz vardır:

- Uygulamayı kullanıcı arabirimiyle çalıştırma
- Ek komut satırı seçenekleri için uygulamayı komut isteminde çalıştırın

Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, aracın internet uç noktalarına erişmesine izin vermeniz gerekir. Aracı çalıştıracağınız cihaz, hizmet bağlantı noktasıyla aynı internet erişimi gerektirir. Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../../plan-design/network/internet-endpoints.md#bkmk_scp).<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Kurulum Yükleyici 'yi Kullanıcı arabirimiyle çalıştırma

1. İnternet erişimi olan bir bilgisayarda, yüklemek istediğiniz Configuration Manager sürümü için yükleme medyasına gidin.

1. **Smssetup\bin\x64** alt klasöründe **setupdl. exe**' yi çalıştırın.

1. Güncelleştirilmiş yükleme dosyalarının depolandığı klasörün yolunu belirtin ve ardından **İndir**' i seçin. Kurulum Yükleyici, şu anda indirme klasöründeki dosyaları doğrular. Yalnızca eksik olan veya mevcut dosyalardan daha yeni olan dosyaları indirir. İndirilen diller ve diğer gerekli bileşenleri için alt klasörler oluşturur.

1. İndirme sonuçlarını gözden geçirmek için bkz. **C:\configmgrsetup.log**.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Kurulum Yükleyici 'yi bir komut isteminden çalıştırma

1. Bir komut istemi açın ve yüklemek istediğiniz Configuration Manager sürümünün dizinini yükleme medyası ile değiştirin.

1. Dizini **Smssetup\bin\x64** alt klasörü olarak değiştirin ve gerekli seçeneklerle **setupdl. exe dosyasını** çalıştırın.

1. İndirme sonuçlarını gözden geçirmek için bkz. **C:\configmgrsetup.log**.

### <a name="command-line-options"></a>Komut satırı seçenekleri

**Setupdl. exe**ile aşağıdaki komut satırı seçeneklerini kullanabilirsiniz:

- **/Verify**: dil dosyalarını içeren indirme klasöründeki dosyaları doğrulayın. Güncel olmayan dosyaların listesi için **C:\configmgrsetup.log dosyasını**gözden geçirin. Bu seçeneği kullandığınızda, hiçbir dosya indirmez.

- **/Verifylang**: yalnızca indirme klasöründeki dil dosyalarını doğrulayın. Güncel olmayan dil dosyalarının listesi için **C:\configmgrsetup.log dosyasını**gözden geçirin.

- **/Lang**: indirme klasörüne yalnızca dil dosyalarını indirin.

- **/NOUI**: kurulum yükleyici 'yi Kullanıcı arabirimi olmadan başlatın. Bu seçeneği kullandığınızda, **indirme yolu** gereklidir.

- **İndirme yolu**: doğrulama veya indirme işlemini otomatik olarak başlatmak için indirme klasörünün yolunu belirtin. **/NOUI** seçeneğini kullandığınızda indirme yolu gereklidir. İndirme yolu belirtmezseniz, kurulum yükleyici yolu belirtmenizi ister. Klasör yoksa, kurulum yükleyici tarafından oluşturulur.

### <a name="example-commands"></a>Örnek komutlar

#### <a name="example-1"></a>Örnek 1

Kurulum Yükleyici, belirtilen indirme klasöründeki dosyaları doğrular ve ardından dosyaları indirir.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Örnek 2

Kurulum yükleyici yalnızca belirtilen indirme klasöründeki dosyaları doğrular.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Örnek 3

Kurulum Yükleyici, belirtilen indirme klasöründeki dosyaları doğrular ve ardından dosyaları indirir. Araç hiçbir Kullanıcı arabirimini göstermez.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Örnek 4

Kurulum Yükleyici, belirtilen indirme klasöründeki dil dosyalarını doğrular ve ardından yalnızca dil dosyalarını indirir.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Kurulum yükleyici dosyalarını başka bir bilgisayara Kopyala

1. Windows Gezgini 'nde, aşağıdaki konumlardan birine gidin:

    - **&lt;Yükleme medyası Configuration Manager> \SMSSETUP\BIN\X64**

    - **&lt;> \BIN\X64 Configuration Manager yükleme yolu**

1. Aşağıdaki dosyaları diğer bilgisayardaki aynı hedef klasöre kopyalayın:

    - **setupdl. exe**

    - **.\\&lt; Dil > \\ setupdlres. dll**

        > [!NOTE]
        > Bu dosya, install dilinin alt klasörüdür. Örneğin, Ingilizce `00000409` alt klasördeyse.

    Cihazınızdaki hedef klasörler aşağıdaki örnekteki gibi görünmelidir:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Kurulum Yükleyici 'yi hedef bilgisayardan çalıştırın. [Kullanıcı arabirimini](#bkmk_ui) veya [komut satırını](#bkmk_cmd)kullanın.
