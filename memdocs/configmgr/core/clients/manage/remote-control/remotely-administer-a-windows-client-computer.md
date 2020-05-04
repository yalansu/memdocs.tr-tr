---
title: Windows bilgisayarı uzaktan yönetme
titleSuffix: Configuration Manager
description: Configuration Manager kullanarak uzak bir Windows istemci bilgisayarı yönetme.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715112"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Configuration Manager kullanarak bir Windows istemci bilgisayarını uzaktan yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)* Configuration Manager, **Configuration Manager uzaktan denetimi**kullanarak istemci bilgisayarlara bağlanmanızı sağlar. Uzaktan denetimi kullanmaya başlamadan önce, aşağıdaki makalelerde yer alan bilgileri gözden geçirdiğinizden emin olun:  

-   [Uzaktan denetim için önkoşullar](prerequisites-for-remote-control.md)  

-   [Uzaktan denetimi yapılandırma](configuring-remote-control.md)  

Uzaktan denetim görüntüleyicisini başlatmak için üç yol aşağıda verilmiştir:  

-   Configuration Manager konsolunda.  

-   Bir Windows komut isteminde.  

-   Windows **Başlat** menüsünden, **Microsoft System Center** program grubunda Configuration Manager konsolunu çalıştıran bir bilgisayarda.  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Bir istemci bilgisayarı Configuration Manager konsolu aracılığıyla uzaktan yönetmek için  

1.  Configuration Manager konsolunda **varlıklar ve uyumluluk** > **cihazları** ' nı veya **Cihaz Koleksiyonları**' nı seçin.  

3.  Uzaktan yönetmek istediğiniz bilgisayarı seçin ve ardından **giriş** sekmesinde, **cihaz** grubunda,**Uzaktan denetimi** **Başlat** > ' ı seçin.  

    > [!IMPORTANT]  
    >  İstemci ayarlarında **Uzaktan Denetim için kullanıcıya sor** izni **True**olarak ayarlanmışsa, uzak bilgisayardaki kullanıcı uzak denetim komut istemini kabul edene kadar bağlantı başlatılmaz. Daha fazla bilgi için bkz. [Uzaktan denetimi yapılandırma](configuring-remote-control.md).  

4.  **Configuration Manager Uzaktan Denetim** penceresi açıldıktan sonra istemci bilgisayarı uzaktan yönetebilirsiniz. Bağlantıyı yapılandırmak için aşağıdaki seçenekleri kullanın.  

    > [!NOTE]  
    >  Bağlandığınız bilgisayarın birden çok İzleyicisi varsa, tüm izleyicilerinden ekran, uzaktan denetim penceresinde gösterilir.  

    -   **Dosya**
        - **Bağlan** -başka bir bilgisayara bağlanın. Bir uzaktan denetim oturumu etkin olduğunda bu seçenek kullanılamaz.  
        -   **Bağlantıyı kes** -etkin uzaktan denetim oturumunun bağlantısını keser ancak **Configuration Manager uzaktan denetim** penceresini kapatmaz.  
        - **Exit** -etkin uzaktan denetim oturumunun bağlantısını keser ve **Configuration Manager uzaktan denetim** penceresini kapatır.  

        > [!NOTE]  
        >  Bir uzaktan denetim oturumunun bağlantısını sonlandırdığınızda, görüntülediğiniz bilgisayardaki Windows Pano içeriği silinir.


    - **Görünüm**
      - **Renk derinliği** -piksel başına 16 bit ya da 32 bit seçin.
      -  **Tam ekran** - **Configuration Manager uzaktan denetim** penceresini en üst düzeye çıkarır. Tam ekran modundan çıkmak için Ctrl+Alt+Break tuşlarına basın.  
      - **Düşük bant genişliğine sahip bağlantı Için iyileştirin** -bağlantı bant genişliği düşük ise bu seçeneği belirleyin.
      - **Görüntülenme**
        - **Tüm ekranlar** -Configuration Manager 1902 ' de eklendi. Bağlandığınız bilgisayarın birden çok İzleyicisi varsa, tüm izleyicilerinden ekran, uzaktan denetim penceresinde gösterilir. **Tüm ekranlar** 1902 ' dan önce birden çok monitöre sahip bilgisayarlar için tek görünümüdür.
        -  **Ilk ekran** Configuration Manager 1902 ' de eklendi. *İlk ekran* , Windows görüntüleme ayarları ' nda gösterildiği gibi en üstte ve sol uçta bulunur. Belirli bir ekran seçemezsiniz. Görüntüleyicisinin yapılandırmasını değiştirdiğinizde, uzak oturumu yeniden bağlayın. Görüntüleyici gelecekteki bağlantılara yönelik tercihinizi kaydeder.
        -  Uzak bilgisayarın görüntüsünü, **Configuration Manager uzaktan denetim** penceresinin boyutuna sığacak şekilde **ölçeklendirin** .
        - **Durum çubuğu** - **Configuration Manager uzaktan denetim** penceresi durum çubuğunun görünümünü değiştirir.  

       > [!NOTE]  
       >  Görüntüleyici gelecekteki bağlantılara yönelik tercihinizi kaydeder.

    -   **Eylem**
        - **Ctrl + Alt + Del tuş gönder** -uzak bilgisayara bir Ctrl + Alt + Del tuş bileşimi gönderir. 
        - **Pano paylaşımını etkinleştir** -uzak bilgisayara ve uzak bilgisayardan öğe kopyalayıp yapıştırmanıza olanak tanır. Bu değeri değiştirirseniz, değişikliğin geçerli olması için uzaktan denetim oturumunu yeniden başlatmanız gerekir.   
          - Configuration Manager konsolunda Pano paylaşımının etkinleştirilmesini istemiyorsanız, konsolunu çalıştıran bilgisayarda, **HKEY_CURRENT_USER \Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** kayıt defteri anahtarının değerini **0**olarak ayarlayın.
        - **Klavye çevirisini etkinleştir** -konsolu çalıştıran bilgisayarın klavye yerleşimini bağlı cihazın düzenine çevirir.
        - Uzak **klavyeyi kilitle ve fare** , uzak klavyeyi ve fareyi kilitler ve kullanıcının uzak bilgisayarı kullanmasını engelleyin.  

    -   **Yardım**
        - **Uzaktan denetim hakkında** -görüntüleyicisinin geçerli sürümünü görüntüler.  

5.  Uzak bilgisayardaki kullanıcılar, Configuration Manager **Uzaktan denetim** simgesine tıkladıklarında uzaktan denetim oturumu hakkında daha fazla bilgi görüntüleyebilir. Simge, Windows bildirim alanında veya uzaktan denetim oturum çubuğundaki simgede bulunur.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Uzaktan denetim görüntüleyicisini Windows komut satırından başlatmak için  

-   Windows komut isteminde _<Configuration Manager yükleme\>klasörü_**\AdminConsole\Bin\i386\CmRcViewer.exe** yazın.  

CmRcViewer.exe, aşağıdaki komut satırı seçeneklerini destekler:  

- *Adres* -bağlanmak istediğiniz Istemci bilgisayarın NetBIOS adını, tam etki alanı adını (FQDN) veya IP adresini belirtir.
- *Site sunucusu adı* -uzaktan denetim oturumuyla ilgili durum iletilerini göndermek istediğiniz Configuration Manager site sunucusunun adını belirtir.
- **/?** -Uzaktan Denetim Görüntüleyicisi için komut satırı seçeneklerini görüntüler.  
     
**Örnek: CmRcViewer. exe** *<adresi\> * * < \\\site sunucu adı>* 

> [!NOTE]  
> Uzaktan Denetim Görüntüleyicisi, Configuration Manager konsolu için desteklenen tüm işletim sistemlerinde desteklenir. Daha fazla bilgi için bkz. [Configuration Manager konsolları Için desteklenen konfigürasyonlar](../../../plan-design/configs/supported-operating-systems-consoles.md) ve [Uzaktan denetim önkoşulları](prerequisites-for-remote-control.md).

## <a name="next-steps"></a>Sonraki adımlar

[Uzaktan denetim kullanımını denetleme](audit-remote-control-usage.md)
