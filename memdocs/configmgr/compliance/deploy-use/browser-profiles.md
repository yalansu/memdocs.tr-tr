---
title: Microsoft Edge ayarlarını yapılandırma
titleSuffix: Configuration Manager
description: Windows 10 istemcilerinde Microsoft Edge Web tarayıcısının ayarlarını yapılandırma
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210103"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Configuration Manager 'de Microsoft Edge ayarlarını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!-- 1357310 -->
Sürüm 1802 ' den başlayarak, Windows 10 istemcilerinde [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web tarayıcısını kullanan müşteriler için, birkaç Microsoft Edge ayarını yapılandırmak üzere bir Configuration Manager uyumluluk ayarları ilkesi oluşturun. 

Bu ilke yalnızca Windows 10, sürüm 1703 veya sonraki sürümlerde istemciler için geçerlidir. <!--511552-->


## <a name="policy-settings"></a>İlke ayarları
Bu ilke şu anda aşağıdaki ayarları içerir:
- **Microsoft Edge tarayıcısını varsayılan olarak ayarla**: Web tarayıcısı için Windows 10 varsayılan uygulama ayarını Microsoft Edge olarak yapılandırır
- **Adres çubuğu açılır öğesine Izin ver**: Windows 10, sürüm 1703 veya üstünü gerektirir. Daha fazla bilgi için bkz. [Allowaddressbardropı tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Microsoft tarayıcıları arasında sık kullanılanlara eşitlemeye Izin ver**: Windows 10, sürüm 1703 veya üstünü gerektirir. Daha fazla bilgi için bkz. [Syncfavoritesbetweenıeandmicrosoftedge Browser ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Çıkışta tarama verilerini temizlemeye Izin ver**: Windows 10, sürüm 1703 veya üstünü gerektirir. Daha fazla bilgi için bkz. [Clearbrowsingdataonexit Browser ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Üst bilgileri Izlememe Izin ver**: daha fazla bilgi için bkz. [allowdonottrack tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Otomatik doldurmaya Izin ver**: daha fazla bilgi için bkz. [allowotomatik doldurma tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Tanımlama bilgilerine Izin ver**: daha fazla bilgi için bkz. [AllowCookies tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Açılır pencere engelleyiciye Izin ver**: daha fazla bilgi için bkz. [allowpopup Browser Policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Adres çubuğunda arama önerilerine Izin ver**: daha fazla bilgi için bkz. [Allowsearchmülationsınaddressbar tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Internet Explorer 'a intranet trafiği gönderilmesine Izin ver**: daha fazla bilgi için bkz. [SendIntranetTraffictoInternetExplorer Browser Policy](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Parola Yöneticisi 'Ne Izin ver**: daha fazla bilgi için bkz. [allowpasswordmanager tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Geliştirici Araçları Izin ver**: daha fazla bilgi için bkz. [AllowDeveloperTools Browser Policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Uzantılara Izin ver**: daha fazla bilgi için bkz. [AllowExtensions tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Microsoft Edge için Windows Defender SmartScreen ayarlarını yapılandırma
<!--1353701-->
Sürüm 1806 ' den başlayarak, bu ilke [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview)için üç ayar ekler. İlke artık **SmartScreen ayarları** sayfasında aşağıdaki ek ayarları içerir:

- **SmartScreen 'e Izin ver**: Windows Defender SmartScreen 'e izin verilip verilmeyeceğini belirtir. Daha fazla bilgi için bkz. [Allowsmartscreen tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Kullanıcılar siteler Için SmartScreen istemlerini geçersiz kılabilir**: kullanıcıların olası kötü amaçlı Web siteleri hakkındaki Windows Defender SmartScreen Filtresi uyarılarını geçersiz kılıp kılamayacağını belirtir. Daha fazla bilgi için [PreventSmartScreenPromptOverride Browser ilkesine](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)bakın.
- **Kullanıcılar dosyalar Için SmartScreen istemlerini geçersiz kılabilir**: kullanıcıların, doğrulanmamış dosyaları Indirme hakkındaki Windows Defender SmartScreen Filtresi uyarılarını geçersiz kılıp kılamayacağını belirtir. Daha fazla bilgi için [PreventSmartScreenPromptOverrideForFiles Browser ilkesine](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)bakın.



## <a name="create-the-microsoft-edge-browser-profile"></a>Microsoft Edge tarayıcı profili oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Uyumluluk ayarları** ' nı genişletin ve **Microsoft Edge tarayıcı profilleri** düğümünü seçin. **Microsoft Edge profili oluşturmak**için şerit seçeneğine tıklayın.
2. İlke için bir **ad** belirtin, isteğe bağlı olarak bir **Açıklama**girin ve **İleri**' ye tıklayın.
3. **Genel ayarlar** sayfasında, bu ilkeye dahil edilecek ayarlar için **yapılandırılan** değeri değiştirin ve **İleri**' ye tıklayın. **Edge tarayıcısını ayarlama** ayarı, devam etmek için yapılandırılmış olmalıdır.
4. Sürüm 1806 ve sonrasında, **SmartScreen ayarları** sayfasında ayarları yapılandırın ve ardından **İleri**' ye tıklayın. 
5. **Desteklenen platformlar** sayfasında, bu ilkenin geçerli olduğu işletim sistemi sürümlerini ve mimarilerini seçin ve **İleri**' ye tıklayın. 
6. Sihirbazı tamamlayın.



## <a name="deploy-the-policy"></a>İlkeyi dağıtma

1. İlkenizi seçin ve **dağıtmak**için şerit seçeneğine tıklayın.
2. İlkenin dağıtılacağı Kullanıcı veya cihaz koleksiyonunu seçmek için, **Araştır** ' a tıklayın. 
3. Gereken ek seçenekleri seçin.  
     a. İlke uyumlu olmadığında uyarılar oluşturun.  
     b. İstemcinin bu ilkeyle cihazın uyumluluğunu değerlendiren zamanlamayı ayarlayın. 
4. Dağıtımı oluşturmak için **Tamam** ' ı tıklatın.



## <a name="next-steps"></a>Sonraki adımlar

Tüm uyumluluk ayarları ilkeleri gibi, istemci belirttiğiniz zamanlamaya göre ayarları düzeltir. Configuration Manager konsolundaki [Cihaz uyumluluğunu izleyin ve rapor](monitor-compliance-settings.md) edin.
