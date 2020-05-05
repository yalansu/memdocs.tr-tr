---
title: Mevcut cihazlar için Windows Autopilot
titleSuffix: Configuration Manager
description: Windows Autopilot Kullanıcı odaklı mod için bir Windows 7 cihazını yeniden görüntü ve sağlama için Configuration Manager görev dizisi kullanma
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724212"
---
# <a name="windows-autopilot-for-existing-devices"></a>Mevcut cihazlar için Windows Autopilot
<!--3607717, fka 1358333-->

*Uygulama hedefi: Configuration Manager (geçerli dal)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) , kuruluşların yeni, dokunulmamış Windows 10 cihazlarını doğrudan son kullanıcıya sunmasına ve güvenli, üretken bir Windows 10 cihazı almak için kullanıcının üzerinden gittiği sağlama akışını tanımlamasına olanak sağlar. Cihaz Windows Autopilot hizmetine kaydedilir, böylece gerekli Windows Autopilot profilini atayabilirsiniz. Bu profil, bu cihaz için hazır olmayan deneyimi (OOBE) tanımlar. 

Windows 10, sürüm 1809 veya sonraki sürümlerde [mevcut cihazlar Için Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) kullanılabilir. Bu özellik, tek bir yerel Configuration Manager görev sırası kullanarak [Windows Autopilot Kullanıcı odaklı mod](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) Için bir Windows 7 cihazını yeniden görüntüetmenizi ve sağlamanızı sağlar. 



## <a name="prerequisites"></a>Önkoşullar

- Windows 10 sürüm 1809 veya üzeri için yükleme medyasını edinin. Ardından Configuration Manager bir işletim sistemi görüntüsü oluşturun. Daha fazla bilgi için bkz. [OS görüntülerini yönetme](../get-started/manage-operating-system-images.md).

- Microsoft Intune, Windows Autopilot için Profiller oluşturun. Daha fazla bilgi için bkz. [Windows Autopilot kullanarak Intune 'Da Windows cihazlarını kaydetme](https://docs.microsoft.com/intune/enrollment-autopilot).

- Windows Autopilot hizmetine kayıtlı olmayan bir cihaz. Cihaz zaten kaydedilmişse, atanan profil önceliklidir. Mevcut cihazlar için Autopilot profili yalnızca çevrimiçi profil zaman aşımına uğrarsa geçerlidir.



## <a name="create-the-configuration-file"></a>Yapılandırma dosyasını oluşturma

1. İnternet bağlantısı olan bir Windows cihazında, bir yönetim PowerShell komut penceresi açın ve aşağıdaki komutları çalıştırın:  

    1. Gerekli modülleri yükler ve devam etmek için istemleri kabul et  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Yönetici kimlik bilgileriyle Intune 'da oturum açın  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Intune kiracınızla ilişkili tüm Windows Autopilot profillerini alma  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Her profil için bir yapılandırma dosyası oluşturun. Dosyalar, profilin görünen adı için adlandırılır ve geçerli kullanıcının masaüstüne kaydedilir.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Yapılandırma dosyası yalnızca bir profil içerebilir. Her profil, süslü ayraç `{}`içinde olmalıdır.  

2. Profillerin birini **AutopilotConfigurationFile. JSON**adlı ANSI kodlu bir dosyaya kaydedin. Configuration Manager paket kaynağı olarak uygun bir konuma kaydedin.  

    > [!Tip]  
    > JSON çıkışını bir dosyaya yeniden yönlendirmek için PowerShell cmdlet **out dosyasını** kullanırsanız, varsayılan olarak Unicode kodlaması kullanır. Bu cmdlet uzun satırları da kesebilir. Uygun metin kodlamasını ayarlamak için, **set-Content** cmdlet 'ini `-Encoding ASCII` parametresiyle kullanın.   
    > 
    > Windows Not defteri varsayılan olarak ANSI kodlaması kullanır.  

3. Bu dosyayı içeren bir Configuration Manager paketi oluşturun. Bir program gerektirmez. Daha fazla bilgi için bkz. [paket oluşturma](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > Windows bu dosyanın **AutopilotConfigurationFile. JSON**olarak adlandırıldığını gerektirir. Birden fazla Autopilot profili kullanmak için ayrı Configuration Manager paketleri oluşturun.  



## <a name="create-the-task-sequence"></a>Görev sırasını oluşturma

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin. Şeritte **görev sırası oluştur** ' u seçin.  

2. **Yeni görev sırası oluştur** sayfasında, **mevcut cihazlar Için Windows Autopilot dağıtma**seçeneğini belirleyin.  

3. **Görev sırası bilgileri** sayfasında, bir ad belirtin, isteğe bağlı olarak bir açıklama ekleyin ve bir önyükleme görüntüsü seçin. Desteklenen önyükleme görüntüsü sürümleri hakkında daha fazla bilgi için bkz. [Windows 10 Için destek](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. Windows 'u **yükler** sayfasında, Windows 10 **görüntü paketini**seçin. Ardından aşağıdaki ayarları yapılandırın:  

    - **Görüntü dizini**: kuruluşunuzun gerektirdiği şekilde kurumsal, eğitim veya profesyonel seçeneklerinden birini belirleyin  

    - **İşletim sistemini yüklemeden önce hedef bilgisayarı bölümlemek ve biçimlendirmek** için seçeneği etkinleştirin  

    - **BitLocker ile kullanılacak görev sırasını Yapılandır**: Bu seçeneği etkinleştirirseniz, görev sırası BitLocker 'ı etkinleştirmek için gereken adımları içerir  

    - **Ürün anahtarı**: Windows etkinleştirmesi için bir ürün anahtarı belirtmeniz gerekiyorsa buraya girin  

    - Windows 10 ' da yerel yönetici hesabını yapılandırmak için aşağıdaki seçeneklerden birini belirleyin:  
        - **Yerel yönetici parolasını rastgele oluştur ve tüm destek platformlarındaki hesabı devre dışı bırak (önerilir)**
        - **Hesabı etkinleştirin ve yerel yönetici parolasını belirtin**

5. **Ağı Yapılandır** sayfasında, **bir çalışma grubuna katılma**seçeneğini belirleyin. Bu görev dizisi, Windows Sistem Hazırlama Aracı 'nı (Sysprep) kullanır. Cihaz bir etki alanına katılırsa, Sysprep başarısız olur.  

6. **Configuration Manager 'ı yükleme** sayfasında, ortamınız için gerekli yükleme özelliklerini ekleyin.  

    > [!Tip]  
    > Görev sırası, Sysprep çalıştırılmadan önce görev sırası sırasında Configuration Manager istemci bileşenleri gerekliyse yalnızca bu bilgiye ihtiyaç duyuyor. Örneğin, yazılım güncelleştirmelerini veya uygulamaları yüklemek için. Bu eylemleri yapmadıysanız, istemci gerekli değildir. Bu, görev dizisi Sysprep 'i çalıştırmadan önce kaldırılır.  

7. **Güncelleştirmeleri dahil et** sayfası, varsayılan olarak **herhangi bir yazılım güncelleştirmesi yüklememe**seçeneği olarak seçilir.  

    > [!Tip]  
    > En son Windows 10 kalite güncelleştirmeleriyle görüntüyü güncel tutmak için çevrimdışı görüntü Bakımı 'nı kullanın. Daha fazla bilgi için bkz. [bir işletim sistemi görüntüsüne yazılım güncelleştirmeleri uygulama](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).  

8. **Uygulamaları yüklemek** sayfasında, görev sırası sırasında yüklenecek uygulamaları seçebilirsiniz. Ancak, Microsoft bu senaryoyla imza resmi yaklaşımını yansıtmanızı önerir. Cihaz Autopilot ile gerçekleştirildikten sonra, tüm uygulama ve konfigürasyonları Microsoft Intune veya ortak yönetim Configuration Manager uygulayın. Bu işlem, yeni cihazları alan kullanıcılar ve var olan cihazlar için Windows Autopilot kullanarak tutarlı bir deneyim sağlar.  

8. **Sistem hazırlığı** sayfasında, Autopilot yapılandırma dosyasını içeren paketi seçin. Varsayılan olarak, görev dizisi Windows Sysprep çalıştırdıktan sonra bilgisayarı yeniden başlatır. Ayrıca, **Bu görev dizisi tamamlandıktan sonra bilgisayarı kapatır**seçeneğini de belirleyebilirsiniz. Bu seçenek, bir cihazı hazırlamanızı ve sonra tutarlı bir Autopilot deneyimi için bir kullanıcıya sunmanızı sağlar.  

9. Sihirbazı tamamlayın.  

Görev sırasını düzenlerseniz, var olan bir işletim sistemi görüntüsünü uygulamak için varsayılan görev dizisine benzer. Bu görev dizisi aşağıdaki ek adımları içerir:  

- **Windows Autopilot yapılandırmasını Uygula**: Bu adım, belirtilen paketten Autopilot yapılandırma dosyasını uygular. Yeni bir adım türü değildir. dosyayı kopyalamak için bir **komut satırı Çalıştır** adımı.  

- **Windows 'U yakalamaya hazırla**: Bu adım Windows Sysprep 'i çalıştırır ve **Bu eylemi çalıştırdıktan sonra bilgisayarı kapatmaya**yönelik ayara sahiptir. Daha fazla bilgi için bkz. [Windows 'U yakalamaya hazırlama](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

Var olan cihazlar için Windows Autopilot görev sırası, Azure Active Directory (Azure AD) bir cihaza katılmış bir cihazla sonuçlanır. 

> [!NOTE]  
> Windows 10 sürüm 1903 ve sürüm 1909 ile Autopilot, Sysprep 'in **AutopilotConfigurationFile. JSON** dosyasını sildiği bilinen bir sorunu vardır. Windows 10 sürüm 1903 veya sürüm 1909 ' i dağıtmak için bu yöntemi kullanırsanız, bu görev dizisini düzenleyin ve aşağıdaki değişiklikleri yapın:
>
> 1. Windows 'u **yakalamaya hazırla** adımını devre dışı bırakın.
> 2. **Windows 'U yakalamaya** devre dışı bırakma adımının hemen ardından yeni bir **komut satırı Çalıştır** adımı ekleyin. Aşağıdaki komut satırını çalıştıracak şekilde yapılandırın:`c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Daha fazla bilgi için bkz. [Windows Autopilot-bilinen sorunlar](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Windows 10 yükseltmesinden önce kullanıcının verilerinin yedeklendiğinden emin olmak için OneDrive Iş açısından [bilinen klasör taşıma](https://docs.microsoft.com/onedrive/redirect-known-folders) ' yı kullanın.



## <a name="next-steps"></a>Sonraki adımlar

Windows 10 cihazlarınızın yönetim özelliklerini geliştirmek için ortak yönetim ' i kullanın. Ortak yönetimin ikinci yolu, Windows Autopilot ile modern sağlama yoluyla yapılır. Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Ortak yönetim nedir?](../../comanage/overview.md)
- [Ortak yönetim yolları](../../comanage/quickstart-paths.md)
- [Ortak yönetim ile Windows Autopilot](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Ayrıca bkz.

- [Windows Autopilot kullanarak Windows cihazlarını Intune 'A kaydetme](https://docs.microsoft.com/intune/enrollment-autopilot)
