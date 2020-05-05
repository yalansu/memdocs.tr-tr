---
title: Endpoint Protection istemci ayarları
titleSuffix: Configuration Manager
description: Endpoint Protection için özel istemci ayarlarını yapılandırmayı öğrenin.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724324"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Endpoint Protection’a yönelik özel istemci ayarlarını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu yordam, hiyerarşinizdeki cihaz koleksiyonlarına dağıtabileceğiniz Endpoint Protection için özel istemci ayarlarını yapılandırır.

> [!IMPORTANT]  
>  Varsayılan Endpoint Protection istemci ayarlarını yalnızca hiyerarşinizdeki tüm bilgisayarlara uygulanmasını istediğinizden emin değilseniz yapılandırın. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Endpoint Protection’ı etkinleştirmek ve özel istemci ayarlarını yapılandırmak için

1. Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2. **Yönetim** çalışma alanında **İstemci Ayarları**'nı tıklatın.  

3. **Giriş** sekmesindeki **Oluştur** grubunda, **Özel İstemci Cihaz Ayarları Oluştur**'a tıklayın.  

4. **Özel İstemci Cihaz Ayarları Oluştur** iletişim kutusunda ayar grubu için bir ad ve açıklama belirtin ve ardından **Endpoint Protection**’ı seçin.  

5. İhtiyaç duyduğunuz Endpoint Protection istemci ayarlarını yapılandırın. Yapılandırabileceğiniz Endpoint Protection istemci ayarlarının tam listesi için, [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#endpoint-protection)bölümündeki Endpoint Protection bölümüne bakın.  

   > [!IMPORTANT]  
   >  Endpoint Protection için istemci ayarlarını yapılandırmadan önce Endpoint Protection site sistem rolünü yükleyebilirsiniz.  

6. **Tamam** ’a tıklayarak **Özel İstemci Cihaz Ayarları Oluştur** iletişim kutusunu kapatın. Yeni istemci ayarları **Yönetim** çalışma alanının **İstemci Ayarları** düğümünde gösterilir.  

7. Ardından, özel istemci ayarlarını bir koleksiyona dağıtın. Dağıtmak istediğiniz özel istemci ayarlarını seçin. **Giriş** sekmesinde, **Istemci ayarları** grubunda **Dağıt**' a tıklayın.  

8. **Koleksiyon Seç** iletişim kutusunda istemci ayarlarını dağıtmak istediğiniz koleksiyonu seçin ve ardından **Tamam**’a tıklayın. Yeni dağıtım, ayrıntılar bölmesinin **Dağıtımlar** sekmesinde gösterilir.  

İstemci ilkesi bir sonraki sefer indirdiklerinde istemciler bu ayarlarla yapılandırılır. Daha fazla bilgi için bkz. [Configuration Manager istemcisi için ilke almayı başlatma](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Endpoint Protection istemcisini bir disk görüntüsünde sağlama

Endpoint Protection istemcisini Configuration Manager işletim sistemi dağıtımı için disk görüntüsü kaynağı olarak kullanmayı düşündüğünüz bir bilgisayara yükleyebilirsiniz. Bu bilgisayara genellikle referans bilgisayar denir. İşletim sistemi görüntüsünü oluşturduktan sonra, görüntüyü dağıtmak için Configuration Manager işletim sistemi dağıtımı ' nı kullanın.

> [!Important]  
> Windows 10 ve Windows Server 2016 varsayılan olarak Windows Defender yüklü. Bu Windows sürümlerinde bu yordama ihtiyacınız yoktur.  

Endpoint Protection istemcisini bir referans bilgisayara yükleyip yapılandırmanıza yardımcı olması için aşağıdaki yordamları kullanın.


### <a name="prerequisites"></a>Önkoşullar

Aşağıdaki liste, bir referans bilgisayara Endpoint Protection istemci yazılımını yüklemek için gereken önkoşulları içermektedir.

- **Scepinstall. exe**Endpoint Protection istemci yükleme paketine erişiminizin olması gerekir. Bu paketi site sunucusundaki Configuration Manager yükleme klasörünün **istemci** klasöründe bulabilirsiniz.  

- Endpoint Protection istemcisini kuruluşunuzun gerekli yapılandırmasıyla dağıtmak için, bir kötü amaçlı yazılımdan koruma ilkesi oluşturun ve dışarı aktarın. Endpoint Protection istemcisini el ile yüklerken bu ilkeyi belirtin. Daha fazla bilgi için bkz. [kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md).  

  > [!NOTE]  
  >  **Varsayılan Istemci kötü amaçlı yazılımdan koruma ilkesini**dışarı aktarabilirsiniz.  

- Endpoint Protection istemcisini en son tanımlarla birlikte yüklemek isterseniz, [Windows Defender güvenlik zekası](https://www.microsoft.com/wdsi)' ndan indirin.  

> [!NOTE]  
> Configuration Manager 1802 ' den başlayarak, Windows 10 cihazlarına Endpoint Protection aracısını (Scepınstall) yüklemeniz gerekmez. Windows 10 cihazlarında zaten yüklüyse Configuration Manager kaldırmaz. Yöneticiler, en az 1802 istemci sürümünü çalıştıran Windows 10 cihazlarında Endpoint Protection aracısını kaldırabilir. SCEPInstall. exe, bazı makinelerde C:\Windows\ccmsetup içinde yine de mevcut olabilir, ancak yeni istemci yüklemeleri bunu indirmemelidir. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Referans bilgisayara Endpoint Protection istemcisi nasıl yüklenir

Endpoint Protection istemcisini bir komut isteminden referans bilgisayara yerel olarak yükler. Önce yükleme dosyasını **scepinstall. exe ' yi**alın. Daha fazla bilgi için, bkz. [Endpoint Protection istemcisini bir komut Isteminden yüklemeyin](#bkmk_manual-install).

Gerekirse, önceden yapılandırılmış bir kötü amaçlı yazılımdan koruma ilkesini veya daha önce verdiğiniz bir kötü amaçlı yazılımdan koruma ilkesini de içerir. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a>Endpoint Protection istemcisini bir komut isteminden yüklemek için

1. **Scepinstall. exe** dosyasını Configuration Manager yükleme klasörünün **istemci** klasöründen Endpoint Protection istemci yazılımını yüklemek istediğiniz bilgisayara kopyalayın.  

2. Yönetici olarak bir komut istemi açın. Dizini yükleyici ile klasör olarak değiştirin. Ardından, `scepinstall.exe`ihtiyacınız olan ek komut satırı özelliklerini ekleyerek çalıştırın:


   |  Özellik   |                                  Açıklama                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Yükleyiciyi sessizce çalıştırın                           |
   |    `/q`     |                        Kurulum dosyalarını sessizce Ayıkla                        |
   |    `/i`     |                           Yükleyiciyi normal olarak çalıştır                           |
   |  `/policy`  | Yükleme sırasında istemciyi yapılandırmak için bir kötü amaçlı yazılımdan koruma ilkesi dosyası belirtin |
   | `/sqmoptin` |     Microsoft Müşteri Deneyimini Geliştirme Programı 'yi (CEIP) kabul etme     |


3. İstemci yüklemesini gerçekleştirmek için ekrandaki yönergeleri izleyin.  

4. En son güncelleştirme tanım paketini indirdiyseniz, paketi istemci bilgisayara kopyalayın ve tanım paketini çift tıklatarak yükleyin.  

   > [!NOTE]  
   >  Endpoint Protection istemci yüklemesi tamamlandıktan sonra, istemci otomatik olarak tanım güncelleştirme denetimi gerçekleştirir. Bu güncelleştirme denetimi başarılı olursa, en son tanım güncelleştirme paketini el ile yüklemenize gerek yoktur.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Örnek: istemciyi bir kötü amaçlı yazılımdan koruma ilkesiyle birlikte yükler

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Endpoint Protection istemci yüklemesini doğrulama

Referans bilgisayarınıza Endpoint Protection istemcisini yükledikten sonra, istemcinin düzgün çalıştığını doğrulayın.

1.  Referans bilgisayarda, Windows bildirim alanından **System Center Endpoint Protection** açın.  

2.  **System Center Endpoint Protection** Iletişim kutusunun **giriş** sekmesinde, **gerçek zamanlı korumanın** **Açık**olarak ayarlandığını doğrulayın.  

3.  **Virüs ve casus yazılım tanımları**için **güncel** görüntülendiğini doğrulayın.  

4.  Referans bilgisayarınızın görüntü oluşturmaya hazır olduğundan emin olmak için, **Tarama seçenekleri**altında **tam**' ı seçin ve **Şimdi Tara**' ya tıklayın.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Endpoint Protection istemcisini görüntü oluşturmaya hazırlama

Endpoint Protection istemcisini görüntü oluşturmaya hazırlamak için aşağıdaki adımları gerçekleştirin:

1. Referans bilgisayarda, yönetici olarak oturum açın.  

2. [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec)'Dan **PsExec** indirin ve yükleyin.  

3. Yönetici olarak bir komut istemi çalıştırın, dizini PsTools 'u yüklediğiniz klasöre değiştirin ve ardından aşağıdaki komutu yazın:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Kayıt defteri düzenleyicisini bu şekilde çalıştırırken dikkatli olun. PsExec. exe bunu LocalSystem bağlamında çalıştırır.  

4. Kayıt Defteri Düzenleyicisi 'nde, aşağıdaki kayıt defteri anahtarlarını silin:  

   > [!IMPORTANT]  
   >  Referans bilgisayarı Imaging 'den önceki son adım olarak bu kayıt defteri anahtarlarını silin. Endpoint Protection istemcisi başlatıldığında bu anahtarları yeniden oluşturur. Referans bilgisayarı yeniden başlatırsanız, kayıt defteri anahtarlarını yeniden silin.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Artık referans bilgisayarı görüntü oluşturmaya hazırlamak için hazırsınız.

Endpoint Protection istemcisini içeren bir işletim sistemi görüntüsü dağıttığınızda, bilgileri cihazın atanmış Configuration Manager sitesine otomatik olarak bildirir. İstemci, hedeflenen kötü amaçlı yazılımdan koruma ilkesini indirir ve uygular.  



## <a name="see-also"></a>Ayrıca bkz.

Configuration Manager işletim sistemi dağıtımı hakkında daha fazla bilgi için bkz. [OS görüntülerini yönetme](../../osd/get-started/manage-operating-system-images.md).

