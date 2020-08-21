---
title: Microsoft Edge ayarlarını yapılandırma
titleSuffix: Configuration Manager
description: Windows 10 istemcilerinde Microsoft Edge eski Web tarayıcısının ayarlarını yapılandırma
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: deededfe18275837ae93859c4075837eac870c35
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694789"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Configuration Manager 'de Microsoft Edge eski ayarlarını yapılandırma

> [!IMPORTANT]
> Microsoft Edge sürüm 77 veya üstünü kullanıyorsanız ve ayarlar bölmesini açmaya çalışıyorsanız, `edge://settings/profiles` Arama yerine tarayıcının adres çubuğuna yazın. Daha fazla bilgi için bkz. [Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know)'i öğrenin.
>
> Bu makale BT uzmanlarının Microsoft uç nokta Configuration Manager ile Microsoft Edge eski ayarlarını yönetmesine yöneliktir.

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!-- 1357310 -->
Windows 10 istemcilerinde [Microsoft Edge eski](/microsoft-edge/deploy/) Web tarayıcısını kullanan müşteriler için, tarayıcı ayarlarını yapılandırmak üzere bir Configuration Manager uyumluluk ilkesi oluşturun.

Bu ilke yalnızca Windows 10, sürüm 1703 veya sonraki sürümlerde istemciler ve Microsoft Edge eski sürüm 45 ve önceki sürümleri için geçerlidir. <!--511552-->

Microsoft Edge sürüm 77 veya üstünü Configuration Manager ile yönetme hakkında daha fazla bilgi için bkz. [Microsoft Edge, sürüm 77 ve sonraki sürümleri dağıtma](../../apps/deploy-use/deploy-edge.md). Microsoft Edge sürüm 77 veya üzeri için ilkeleri yapılandırma hakkında daha fazla bilgi için bkz. [Microsoft Edge-policies](/DeployEdge/microsoft-edge-policies).

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

> [!TIP]
> Bu ve diğer ayarları yapılandırmak için Grup İlkesi kullanma hakkında daha fazla bilgi için bkz. [Microsoft Edge eski grup ilkeleri](/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Microsoft Edge için Windows Defender SmartScreen ayarlarını yapılandırın eski
<!--1353701-->
Bu ilke, [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview)için üç ayar ekler. İlke artık **SmartScreen ayarları** sayfasında aşağıdaki ek ayarları içerir:

- **SmartScreen 'e Izin ver**: Windows Defender SmartScreen 'e izin verilip verilmeyeceğini belirtir. Daha fazla bilgi için bkz. [Allowsmartscreen tarayıcı ilkesi](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Kullanıcılar siteler Için SmartScreen istemlerini geçersiz kılabilir**: kullanıcıların olası kötü amaçlı Web siteleri hakkındaki Windows Defender SmartScreen Filtresi uyarılarını geçersiz kılıp kılamayacağını belirtir. Daha fazla bilgi için [PreventSmartScreenPromptOverride Browser ilkesine](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)bakın.

- **Kullanıcılar dosyalar Için SmartScreen istemlerini geçersiz kılabilir**: kullanıcıların, doğrulanmamış dosyaları Indirme hakkındaki Windows Defender SmartScreen Filtresi uyarılarını geçersiz kılıp kılamayacağını belirtir. Daha fazla bilgi için [PreventSmartScreenPromptOverrideForFiles Browser ilkesine](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)bakın.

## <a name="create-the-browser-profile"></a>Tarayıcı profili oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Uyumluluk ayarları** ' nı genişletin ve **Microsoft Edge tarayıcı profilleri** düğümünü seçin. Şeritte **Microsoft Edge profili oluştur**' u seçin.

2. İlke için bir **ad** belirtin, isteğe bağlı olarak bir **Açıklama**girin ve **İleri**' yi seçin.

3. **Genel ayarlar** sayfasında, ayarlar için bu ilkeye dahil edilecek **şekilde değeri** değiştirin. Sihirbaza devam etmek için, **sınır tarayıcısını varsayılan olarak ayarlamak**için ayarı yapılandırmayı unutmayın.

4. **SmartScreen ayarları** sayfasında ayarları yapılandırın.

5. **Desteklenen platformlar** sayfasında, bu ilkenin uygulanacağı işletim sistemi sürümlerini ve mimarilerini seçin.

6. Sihirbazı tamamlayın.

## <a name="deploy-the-policy"></a>İlkeyi dağıtma

1. İlkenizi seçin ve şeritte **Dağıt**' ı seçin.

2. İlkenin dağıtılacağı Kullanıcı veya cihaz koleksiyonunu seçmek için **gidin** .

3. Gereken ek seçenekleri seçin:

    1. İlke uyumlu olmadığında uyarılar oluşturun.

    2. İstemcinin bu ilkeyle cihazın uyumluluğunu değerlendiren zamanlamayı ayarlayın.

4. Dağıtımı oluşturmak için **Tamam ' ı** seçin.

## <a name="next-steps"></a>Sonraki adımlar

Tüm uyumluluk ayarları ilkeleri gibi, istemci belirttiğiniz zamanlamaya göre ayarları düzeltir. Configuration Manager konsolundaki [Cihaz uyumluluğunu izleyin ve rapor](monitor-compliance-settings.md) edin.