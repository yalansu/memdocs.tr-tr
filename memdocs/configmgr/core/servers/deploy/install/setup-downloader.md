---
title: Kurulum Yükleyici
titleSuffix: Configuration Manager
description: Site yüklemenizin, anahtar yükleme dosyalarının güncel sürümlerini kullandığından emin olmak için tasarlanan bu tek başına uygulama hakkında bilgi edinin.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718080"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager için kurulum yükleyicisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir Configuration Manager sitesini yüklemek veya yükseltmek için kurulum 'U çalıştırmadan önce, güncelleştirilmiş Kurulum dosyalarını indirmek için yüklemek istediğiniz Configuration Manager sürümünden Kurulum Yükleyici tek başına uygulamasını kullanabilirsiniz.  

Güncelleştirilmiş Kurulum dosyalarını kullanmak, site yüklemenizin anahtar yükleme dosyalarının geçerli sürümlerini kullanmasını sağlar. Oveview 'da:   
-   Kurulum 'u başlatmadan önce dosyaları indirmek için kurulum yükleyici 'yi kullandığınızda, dosyaları içerecek bir klasör belirlersiniz.  
-   Kurulum Yükleyici 'yi çalıştırmak için kullandığınız hesap, indirme klasörü üzerinde **tam denetim** izinlerine sahip olmalıdır.  
-   Bir siteyi yüklemek veya yükseltmek için kurulum 'U çalıştırdığınızda, daha önce indirdiğiniz dosyaların bu yerel kopyasını kullanmak için onu yönlendirebilirsiniz. Bu, site yükleme veya yükseltme ' ye başladığınızda kurulum formunun Microsoft 'a bağlanmasını engeller.  
-   Sonraki site yüklemeleri veya yükseltmeleri için kurulum dosyalarının aynı yerel kopyasını kullanabilirsiniz.  

Aşağıdaki dosya türleri kurulum yükleyici tarafından indirilir:  
-   Gerekli önkoşul yeniden dağıtılabilir dosyaları  
-   Dil paketleri  
-   Kurulum için en son ürün güncelleştirmeleri  

Kurulum Yükleyici 'yi çalıştırmak için iki seçeneğiniz vardır:
- Uygulamayı kullanıcı arabirimiyle çalıştırma
- Komut satırı seçenekleri için, uygulamayı bir komut isteminde çalıştırın


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Kurulum Yükleyici 'yi Kullanıcı arabirimiyle çalıştırma  

1.  Internet erişimi olan bir bilgisayarda, Windows Gezgini 'ni açın ve ** &lt;configmgrınstalsıyüklememedyası\>\smssetup\bin\x64**konumuna gidin.  

2.  Kurulum Yükleyici 'yi açmak için **setupdl. exe**' ye çift tıklayın.   

3. Güncelleştirilmiş yükleme dosyalarını barındıracak klasörün yolunu belirtin ve ardından **İndir**' e tıklayın. Kurulum Yükleyici, şu anda indirme klasöründeki dosyaları doğrular. Yalnızca eksik olan veya mevcut dosyalardan daha yeni olan dosyaları indirir. Kurulum Yükleyici, indirilen diller ve diğer gerekli alt klasörler için alt klasörler oluşturur.  

4.  İndirme sonuçlarını gözden geçirmek için C sürücüsünün kök dizinindeki **ConfigMgrSetup. log** dosyasını açın.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Kurulum Yükleyici 'yi bir komut isteminden çalıştırma  

1.  Bir komut istemi penceresinde, ** &lt; *Configuration Manager yükleme medyası*\>\smssetup\bin\x64**' e gidin.   

2.  Kurulum Yükleyici 'yi açmak için **setupdl. exe**' yi çalıştırın.

    **Setupdl. exe**ile aşağıdaki komut satırı seçeneklerini kullanabilirsiniz:   

    -   **/Verify**: dil dosyalarını içeren indirme klasöründeki dosyaları doğrulamak için bu seçeneği kullanın. Güncel olmayan dosyaların listesi için C sürücüsünün kök dizinindeki ConfigMgrSetup. log dosyasını gözden geçirin. Bu seçeneği kullandığınızda hiçbir dosya indirilmez.  

    -   **/Verifylang**: indirme klasöründeki dil dosyalarını doğrulamak için bu seçeneği kullanın. Güncel olmayan dil dosyalarının listesi için C sürücüsünün kök dizinindeki ConfigMgrSetup. log dosyasını gözden geçirin.

    -   **/Lang**: indirme klasörüne yalnızca dil dosyalarını indirmek için bu seçeneği kullanın.  

    -   **/NOUI**: kurulum yükleyici 'yi Kullanıcı arabirimini görüntülemeden başlatmak için bu seçeneği kullanın. Bu seçeneği kullandığınızda, komut isteminde komutun bir parçası olarak **indirme yolunu** belirtmeniz gerekir.  

    -   **Downloadpath\>: doğrulama veya indirme işlemini otomatik olarak başlatmak için indirme klasörünün yolunu &lt;** belirtebilirsiniz. **/NOUI** seçeneğini kullandığınızda indirme yolunu belirtmeniz gerekir. İndirme yolu belirtmezseniz, kurulum yükleyici açıldığında yolu belirtmeniz gerekir. Kurulum Yükleyici, yoksa klasörü oluşturur.  

    Örnek komutlar:

    -   **setupdl &lt;downloadpath\>**  

        -   Kurulum Yükleyici başlatılır, belirtilen indirme klasöründeki dosyaları doğrular ve yalnızca eksik olan veya mevcut dosyalardan daha yeni sürümleri olan dosyaları indirir.     

    -   **setupdl/downloadpath doğrulama &lt;\>**  

        -   Kurulum Yükleyici başlar ve belirtilen indirme klasöründeki dosyaları doğrular.  

    -   **setupdl/NOUı &lt;downloadpath\>**  

        -   Kurulum Yükleyici başlatılır, belirtilen indirme klasöründeki dosyaları doğrular ve yalnızca eksik olan veya mevcut dosyalardan daha yeni olan dosyaları indirir.  

    -   **setupdl/LANG &lt;downloadpath\>**  

        -   Kurulum Yükleyici başlatılır, belirtilen indirme klasöründeki dil dosyalarını doğrular ve yalnızca eksik olan veya mevcut dosyalardan daha yeni olan dil dosyalarını indirir.  

    -   **setupdl/VERIFY**  

        -   Kurulum Yükleyici başlar ve ardından indirme klasörünün yolunu belirtmeniz gerekir. Ardından, **Doğrula**' ya tıkladıktan sonra, kurulum yükleyici, indirme klasöründeki dosyaları doğrular.  

3.  İndirme sonuçlarını gözden geçirmek için C sürücüsünün kök dizinindeki **ConfigMgrSetup. log** dosyasını açın.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Kurulum yükleyici dosyalarını başka bir bilgisayara Kopyala

1. Windows Gezgini 'nde, aşağıdaki konumlardan birine gidin:

    - **&lt;Yükleme medyası Configuration Manager> \SMSSETUP\BIN\X64**
    - **&lt;> \BIN\X64 Configuration Manager yükleme yolu**
    
1. Aşağıdaki dosyaları diğer bilgisayardaki aynı hedef klasöre kopyalayın:
    
    - **setupdl. exe**
    - **. \\dil>\\ &lt;. dll**
      - Bu dosya, install dilinin alt klasörüdür. Örneğin, Ingilizce `00000409` alt klasördeyse.

    Örnek olarak, cihazınızdaki hedef klasörlerin şöyle görünmesi gerekir:
    - C:\configmanınstall\setupdl.exe
    - C:\configmanınstall\00000409\setupdlres.dll

1. Yukarıdaki bölümlerde açıklanan [Kullanıcı arabirimini](#bkmk_ui) veya [komut satırını](#bkmk_cmd)kullanarak kurulum yükleyici 'yi bilgisayardan başlatın.
