---
title: İnternet tabanlı cihazları birlikte yönetme
titleSuffix: Configuration Manager
description: Windows 10 Internet tabanlı cihazlarınızı ortak yönetim için nasıl hazırlayacağınızı öğrenin.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 66e6156466d0432aaa8b3b162263f8207bdc9d78
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455115"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>İnternet tabanlı cihazları ortak yönetim için hazırlama

Bu makale, yeni internet tabanlı cihazlar için ortak yönetimin ikinci yoluna odaklanır. Bu senaryo, Azure AD 'ye eklenen ve Intune 'a otomatik olarak kaydeden yeni Windows 10 cihazlarına sahip olduğunuzda olur. Ortak yönetim durumuna ulaşmak için Configuration Manager istemcisini yüklersiniz.  

## <a name="windows-autopilot"></a>Windows Autopilot

Yeni Windows 10 cihazları için Autopilot hizmetini kullanarak, kutudan Out deneyimini (OOBE) yapılandırabilirsiniz. Bu işlem, cihazın Azure AD 'ye katılmasını ve cihazın Intune 'a kaydedilmesini içerir.  

Daha fazla bilgi için bkz. [Windows Autopilot 'e genel bakış](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Cihazlarınızı Azure AD 'ye katılarak Intune 'a otomatik olarak kaydedilecek şekilde yapılandırmak için bkz. [Microsoft Intune Için Windows cihazlarını kaydetme](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Configuration Manager bilgi toplayın

Intune tarafından gereken cihaz bilgilerini toplamak ve raporlamak için Configuration Manager kullanın. Bu bilgilere cihaz seri numarası, Windows ürün tanımlayıcısı ve bir donanım tanımlayıcısı dahildir. Windows Autopilot desteklemek için cihazı Intune 'a kaydetmek üzere kullanılır.

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama** düğümünü genişletin, **raporlar**' ı genişletin ve **donanım-genel** düğümünü seçin.  

2. Raporu çalıştırın, **Windows Autopilot cihaz bilgilerini**ve sonuçları görüntüleyin.  

3. Rapor Görüntüleyicisi 'nde **dışarı aktar** simgesini seçin ve **CSV (virgülle ayrılmış)** seçeneğini belirleyin.  

4. Dosyayı kaydettikten sonra, verileri Intune 'a yükleyin.  

Daha fazla bilgi için bkz. [Intune 'da cihaz ekleme](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Var olan cihazlar için Autopilot
<!--1358333-->

[Mevcut cihazlar Için Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) , Windows 10, sürüm 1809 veya sonraki sürümlerde kullanılabilir. Bu özellik, tek bir yerel Configuration Manager görev sırası kullanarak [Windows Autopilot Kullanıcı odaklı mod](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) Için bir Windows 7 cihazını yeniden görüntüetmenizi ve sağlamanızı sağlar.

Daha fazla bilgi için bkz. [var olan cihazlar Için Windows Autopilot görev sırası](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Configuration Manager istemcisini yükler

İkinci yoldaki Internet tabanlı cihazlar için, Intune 'da bir uygulama oluşturmanız gerekir. Bu uygulamayı, zaten Configuration Manager istemcileri olmayan Windows 10 cihazlarına dağıtın.

> [!NOTE]
> Bu uygulamayı Intune 'daki cihazlara atamadan önce, cihazların CMG sunucusu kimlik doğrulama sertifikasına güvendiğinden emin olun. Daha fazla bilgi için bkz. [Istemcilere CMG güvenilen kök sertifikası](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Bir cihaz CMG sunucusu kimlik doğrulama sertifikasına güvenmiyorsanız, istemcideki CCMSetup. log dosyasında bir WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA hatası görürsünüz.

### <a name="get-the-command-line-from-configuration-manager"></a>Configuration Manager komut satırını al

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin.  

2. Ortak yönetim nesnesini seçin ve ardından şeritte **Özellikler** ' i seçin.  

3. **Etkinleştirme** sekmesinde komut satırını kopyalayın. Sonraki işlem için kaydetmek üzere not defteri 'ne yapıştırın.  

Aşağıdaki komut satırı bir örnektir:`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Ortamınız için hangi komut satırı özelliklerine ihtiyacınız olduğuna karar verin:  

- Aşağıdaki komut satırı özellikleri tüm senaryolarda gereklidir:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- PKI tabanlı istemci kimlik doğrulama sertifikaları yerine istemci kimlik doğrulaması için Azure AD kullanılırken aşağıdaki özellikler gereklidir:  
  - AADCLIENTAPPıD  
  - AADRESOURCEURI  

- İstemci intranete geri gezinse aşağıdaki özelliği kullanın:
  - SMSMP  

- Kendi PKI sertifikanız kullanılıyorsa ve CRL 'niz Internet 'te yayınlanmamışsa, aşağıdaki parametre gereklidir:  
  - /noCRLCheck  

    Daha fazla bilgi için bkz. [CRL planlaması](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Sürüm 2002 ' den başlayarak, bir görev dizisini istemci kaydından hemen sonra önyüklemek için aşağıdaki özelliği kullanın:
  - PROVISIONTS

    Daha fazla bilgi için bkz. [istemci yükleme özellikleri-PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

Site, bulut yönetimi ağ geçidine (CMG) ek Azure AD bilgileri yayımlar. Azure AD 'ye katılmış bir istemci, bu bilgileri Ccmsetup işlemi sırasında, katıldığı aynı kiracıyı kullanarak CMG 'den alır. Bu davranış, birden fazla Azure AD kiracısı olan bir ortamda cihazların ortak yönetime kaydedilmesini kolaylaştırır. Yalnızca iki zorunlu CCMSetup özelliği **CCMHOSTNAME** ve **smssitekodu**.<!--3607731-->

> [!NOTE]
> Configuration Manager istemcisini Intune 'dan zaten dağıtıyorsanız, Intune uygulamasını yeni bir komut satırı ve yeni MSI ile güncelleştirin. <!-- SCCMDocs-pr issue 3084 -->

Aşağıdaki örnek, tüm bu özellikleri içerir:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Daha fazla bilgi için bkz. [istemci yükleme özellikleri](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Uygulamayı Intune 'da oluşturma

1. [Microsoft Endpoint Manager yönetim merkezine](https://endpoint.microsoft.com)gidin ve sol gezinti bölmesini genişletin.  

2. **Uygulamalar**  >  **tüm uygulamalar**  >  **Ekle**' yi seçin.  

3. **Diğer**altında, **iş kolu uygulaması**' nı seçin.  

4. **CCMSetup. msi** uygulama paketi dosyasını karşıya yükleyin. Bu dosyayı Configuration Manager site sunucusundaki şu klasörde bulabilirsiniz: `<ConfigMgr installation directory>\bin\i386` .  

    > [!Tip]  
    > Siteyi güncelleştirdiğinizde bu uygulamayı Intune 'da da güncelleştirdiğinizden emin olun.  

5. Uygulama güncelleştirildikten sonra, Configuration Manager ' den kopyaladığınız komut satırıyla uygulama bilgilerini yapılandırın.  

> [!IMPORTANT]
> Bu komut satırını özelleştirirseniz, 1024 karakterden uzun olmadığından emin olun. Komut satırı uzunluğu 1024 karakterden fazlaysa, istemci yüklemesi başarısız olur.
