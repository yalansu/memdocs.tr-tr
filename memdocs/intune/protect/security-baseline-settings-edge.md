---
title: Microsoft Edge için Intune güvenlik temelleri ayarları
titleSuffix: Microsoft Intune
description: Intune tarafından Microsoft Edge tarayıcısını yönetmek için desteklenen güvenlik temeli ayarları
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fd6943be69f66d4cd6fde2e9c08bec9323005a5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914438"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Intune için Microsoft Edge taban çizgisi ayarları

Microsoft Intune tarafından desteklenen Microsoft Edge Web tarayıcısı taban çizgisi ayarlarını görüntüleyin. Microsoft Edge taban çizgisi Varsayılanları, Microsoft Edge tarayıcıları için önerilen yapılandırmayı temsil eder ve diğer güvenlik temelleri için temel varsayılanlarla eşleşmeyebilir.

::: zone pivot="edge-october-2019"

> [!NOTE]
> Ekim 2019 için Microsoft Edge taban çizgisi genel önizlemededir.

::: zone-end
::: zone pivot="edge-april-2020"

Önceki sürümlerden taban çizgisinin bu sürümü ile nelerin değiştirildiğini anlamak için, bu taban çizgisi için *sürümler* bölmesi görüntülenirken kullanılabilen [temelleri Karşılaştır](../protect/security-baselines.md#compare-baseline-versions) eylemini kullanın. Önceki sürümlerden taban çizgisinin bu sürümü ile nelerin değiştirildiğini anlamak için, bu taban çizgisi için *sürümler* bölmesi görüntülenirken kullanılabilen [temelleri Karşılaştır](../protect/security-baselines.md#compare-baseline-versions) eylemini kullanın.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Desteklenen kimlik doğrulama şemaları**  
  Hangi HTTP kimlik doğrulama düzenlerinin desteklendiğini belirtir. İlkeyi şu değerleri kullanarak yapılandırabilirsiniz: *Basic*, *Digest*, *NTLM*ve *Negotiate*. Birden çok değeri virgülle ayırın. Bu ilkeyi yapılandırmazsanız dört düzen de kullanılır.

  - **Etkin** (*varsayılan*)-seçtiğiniz şemalar kullanılır.
  - **Devre dışı**
  - **Yapılandırılmadı** -dört düzen de kullanılır.
  
  *Etkin* olarak ayarlandığında, hangi kimlik doğrulamasını kullanacağınızı seçtiğiniz aşağıdaki ayarı yapılandırabilirsiniz:

  - **Desteklenen kimlik doğrulama şemaları**  
    Aşağıdaki seçeneklerden seçim yapın:
    - **Temel**
    - **Bilgisi**
    - **NTLM** *(varsayılan olarak seçilidir)*
    - **Anlaş** *(varsayılan olarak seçilidir)*

- **Varsayılan Adobe Flash ayarı**  
  CSP: [Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)ve [Browser/Allowflashtıklatorun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Adobe Flash eklentisini çalıştırmaya yönelik davranışı yapılandırabileceğiniz aşağıdaki ayara erişimi etkinleştirin.  

  - **Etkin** (*varsayılan*)
  - **Devre dışı**
  - **Yapılandırılmadı**

  *Etkin* olarak ayarlandığında, aşağıdaki ayarı yapılandırabilirsiniz.

  - **Varsayılan Adobe Flash ayarı**

    - **Adobe Flash eklentisini engelle** (*varsayılan*)-tüm sitelerde Adobe Flash 'ı engelle
    - **Oynatmak Için tıklayın** -Adobe Flash çalıştırmaları, ancak kullanıcının uygulamayı başlatma seçeneğini belirleyip seçmelidir.

- **Hangi uzantıların yükleneyüklenmediğini denetleme**  
  Kullanıcıların Microsoft Edge 'de yükleye, uzantıları belirten bir listenin kullanımını etkinleştirin. Liste kullanımda olduğunda, listede daha önce yüklenmiş olan tüm ayarlar devre dışı bırakılır ve Kullanıcı bunları etkinleştiremez. Engellenen uzantılar listesinden bir öğeyi kaldırırsanız, bu uzantı önceden yüklenmiş olduğu her yerde otomatik olarak yeniden etkinleştirilir.

  - **Etkin** (*varsayılan*)-uzantıları engellemek için listenin kullanımını etkinleştirin.
  - **Devre dışı**
  - **Yapılandırılmadı** -kullanıcılar Microsoft Edge 'de herhangi bir uzantıyı yükleyebilir.
  
  *Etkin*olarak ayarlandığında, engellenecek uzantıların listesini tanımlayan aşağıdaki ayarı yapılandırabilirsiniz.

  - **Uzantı kimlikleri kullanıcının yüklemesi engellenmelidir (veya * tümü için)**

    **Ekle** ' yi seçin ve ek uzantıları belirtin. **\*** Varsayılan olarak seçilidir.

- **Kullanıcı düzeyindeki yerel mesajlaşma konaklarına izin ver (yönetici izinleri olmadan yüklenir)**  
  Yerel mesajlaşma konakları için Kullanıcı düzeyinde yüklemeyi mümkün.

  - **Etkin**
  - **Devre dışı** (*varsayılan*)-Microsoft Edge, yalnızca sistem düzeyinde yüklü yerel mesajlaşma Konakları kullanır.
  - **Yapılandırılmadı** -varsayılan olarak, Microsoft Edge kullanıcı düzeyindeki yerel mesajlaşma ana bilgisayarlarının kullanımına izin verir.

- **Parola yöneticisine parolaların kaydedilmesini etkinleştir**  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Kullanıcı parolalarını kaydetmek için Microsoft Edge 'i etkinleştirin.

  - **Etkin** -kullanıcılar parolalarını Microsoft Edge 'e kaydedebilir. Siteyi daha sonra ziyaret ettiklerinde, Microsoft Edge parolayı otomatik olarak girer. Kullanıcılar Microsoft Edge 'de bu ilkeyi değiştiremez veya geçersiz kılamazsınız.
  - **Devre dışı** (*varsayılan*)-kullanıcılar yeni parolaları kaydedemez, ancak daha önce kaydedilen parolaları kullanmaya devam edebilir. Kullanıcılar Microsoft Edge 'de bu ilkeyi değiştiremez veya geçersiz kılamazsınız.
  - **Yapılandırılmadı** -kullanıcılar parolaları kaydedebilir ve bu özelliği kapatabilir.

- **Siteler için Microsoft Defender SmartScreen istemlerinin atlanmasını engelle**  
  CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Kullanıcıların olası kötü amaçlı Web siteleri hakkında Microsoft Defender SmartScreen uyarılarını geçersiz kılıp kılamayacağını belirleyin.

  - **Etkin** (*varsayılan*)-kullanıcılar Microsoft Defender SmartScreen uyarılarını yok sayamazlar ve siteye devam etmeleri engellenir.
  - **Devre dışı** -kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve siteye devam edebilir.
  - **Yapılandırılmadı** Kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve siteye devam edebilir

- **İndirmeler hakkında Microsoft Defender SmartScreen uyarılarını atlamayı engelle**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Kullanıcıların doğrulanmamış indirmeler hakkında Microsoft Defender SmartScreen uyarılarını geçersiz kılıp kılamayacağını belirleme.

  - **Etkin** (*varsayılan*)-kullanıcılar Microsoft Defender SmartScreen uyarılarını yok sayamazlar ve doğrulanmamış İndirmeleri tamamlamada engellenirler.
  - **Devre dışı** -kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve doğrulanmamış İndirmeleri tamamlayabilir.
  - **Yapılandırılmadı** -kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve doğrulanmamış İndirmeleri tamamlayabilir.

- **Her site için site yalıtımını etkinleştir**  
  Kullanıcıların tüm siteleri yalıtma varsayılan davranışının dışında bırakılmasını engellemek için site yalıtımını yapılandırın.
  
  - **Etkin** (*varsayılan*)-kullanıcılar, her sitenin kendi sürecinde çalıştığı varsayılan davranışı geri çevirebilir.
  - **Devre dışı** -kullanıcılar, site yalıtımına geri çevirebilir. Site yalıtımı kapalı değil.
  - **Yapılandırılmadı** -kullanıcılar site yalıtımını devre dışı bırakabilirsiniz. Site yalıtımı kapalı değil.

  Microsoft Edge Ayrıca, ek ve daha ayrıntılı kaynakları ayırabilmek için de [ısotekaynakları](/deployedge/microsoft-edge-policies#isolateorigins) ilkesini destekler.  Intune, ısotekaynaklar ilkesini yapılandırmayı desteklemez.
  
- **Microsoft Defender SmartScreen 'i yapılandırma**  
  CSP: [tarayıcı/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen, kullanıcıların olası kimlik avı dolandırıcılarından ve kötü amaçlı yazılımlardan korunmasına yardımcı olmak için uyarı iletileri sağlar. Varsayılan olarak, Microsoft Defender SmartScreen açıktır.
  
  - **Etkin** (*varsayılan*)-Microsoft Defender SmartScreen açık ve kullanıcılar bu özelliği kapatamaz.
  - **Devre dışı** -Microsoft Defender SmartScreen kapalı ve kullanıcılar açamaz.
  - **Yapılandırılmadı**  Kullanıcılar, Microsoft Defender SmartScreen 'i kullanıp kullanmayacağınızı seçebilirler.

  Bu ilke yalnızca Microsoft etkin bir etki alanına katılmış Windows örneklerinde veya cihaz yönetimi için kaydedilen Windows 10 Pro veya Enterprise örneklerinde kullanılabilir.

- **Microsoft Defender SmartScreen 'i istenmeyebilecek uygulamaları engelleyecek şekilde yapılandırma**  
    İstenmeyebilecek uygulamaları engellemek için Microsoft Defender SmartScreen davranışını yapılandırın. Microsoft Defender SmartScreen, kullanıcıların reklam yazılımı, para Miners, paketlemeli ve diğer web siteleri tarafından barındırılan diğer düşük noktalı uygulamalardan korunmasına yardımcı olmak için bir uyarı mesajı verebilir. Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engelleme özelliği varsayılan olarak kapalıdır.

  - **Etkin** (*varsayılan*)-istenmeyebilecek uygulamalar engellenir.
  - **Devre dışı** -istenmeyebilecek uygulamalar engellenmiyor.
  - **Yapılandırılmadı** -kullanıcılar, Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engelleme kullanılıp kullanılmayacağını seçebilirler.

  Bu ilke yalnızca Microsoft etkin bir etki alanına katılmış Windows örneklerinde veya cihaz yönetimi için kaydedilen Windows 10 Pro veya Enterprise örneklerinde kullanılabilir.

- **Kullanıcıların SSL uyarı sayfasından devam edebilsin**  
   CSP: [Browser/Preventcerterrorkılmalar](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge, kullanıcılar SSL hatalarına sahip siteleri ziyaret ettiğinde bir uyarı sayfası gösterir.
  - **Etkin** -kullanıcılar, uyarı sayfalarına tıklabilirler.
  - **Devre dışı** (*varsayılan*)-kullanıcıların herhangi bir uyarı sayfasında tıklalanması engellenir.
  - **Yapılandırılmadı** -kullanıcılar bu uyarı sayfalarında tıklabilirler.

- **En düşük SSL sürümü etkin**  
  SSL 'nin desteklenen en düşük sürümünü ayarlama seçeneğini etkinleştirin.

  - **Etkin** (*varsayılan*)-kullanılacak en düşük TLS sürümünü belirttiğiniz bir sonraki ayara erişimi etkinleştirin.
  - **Devre dışı**
  - **Yapılandırılmadı** -Microsoft Edge varsayılan en düşük *TLS 1,0*sürümünü kullanır.

  *Etkin*olarak ayarlandığında, aşağıdaki AYARı kullanarak TLS yapılandırabilirsiniz.

  - **En düşük SSL sürümü etkin** Kullanılacak en düşük TLS sürümünü ayarlayın. Microsoft Edge, belirtilen sürümden daha düşük bir SSL/TLS sürümü kullanmaz.
    - **TLS 1,0**
    - **TLS 1.1**
    - **TLS 1,2** (*varsayılan*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Siteler için Microsoft Defender SmartScreen istemlerinin atlanmasını engelle**  
  **Varsayılan**: etkin  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Bu ilke ayarı, kullanıcıların olası kötü amaçlı Web siteleri hakkında Microsoft Defender SmartScreen uyarılarını geçersiz kılıp kılamayacağını belirlemenize olanak sağlar. 
  - Bu ayarı etkinleştirirseniz, kullanıcılar Microsoft Defender SmartScreen uyarılarını yok sayamazlar ve siteye devam etmeleri engellenir. 
  - Bu ayarı devre dışı bırakır veya yapılandırmazsanız, kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve siteye devam edebilir.

- **En düşük SSL sürümü etkin**  
  **Varsayılan**: etkin  

  SSL 'nin desteklenen en düşük sürümünü ayarlayın. Bu ilkeyi *Yapılandırılmadı*olarak ayarlarsanız, Microsoft Edge varsayılan en düşük *TLS 1,0*sürümünü kullanır. *Etkin*olarak ayarlandığında, aşağıdaki değerlerden en düşük sürümü seçebilirsiniz:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **En düşük SSL sürümü etkin**  
    **Varsayılan**: TLS 1,2

- **İndirmeler hakkında Microsoft Defender SmartScreen uyarılarını atlamayı engelle**  
  **Varsayılan**: etkin  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Bu ilke, kullanıcıların doğrulanmamış indirmeler hakkında Microsoft Defender SmartScreen uyarılarını geçersiz kılıp kılamayacağını belirlemenizi sağlar.
  - Bu ilkeyi etkinleştirirseniz kuruluşunuzdaki kullanıcılar Microsoft Defender SmartScreen uyarılarını yok sayamazlar ve doğrulanmamış İndirmeleri tamamlamada engellenirler.
  - Bu ilkeyi devre dışı bırakır veya yapılandırmazsanız, kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve doğrulanmamış İndirmeleri tamamlayabilir.

- **Kullanıcıların SSL uyarı sayfasından devam edebilsin**  
  **Varsayılan**: devre dışı  
  Microsoft Edge CSP: [Browser/Preventcerterrorkılmalar](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge, kullanıcılar SSL hatalarına sahip siteleri ziyaret ettiğinde bir uyarı sayfası gösterir. Bu ilkeyi *etkin* veya *yapılandırılmamış*olarak ayarlarsanız, kullanıcılar bu uyarı sayfalarında tıklabilirler. Bu ilke *devre dışı*bırakıldığında, kullanıcıların herhangi bir uyarı sayfasında tıklamakla engellenir. 

- **Varsayılan Adobe Flash ayarı**  
  **Varsayılan**: etkin  
  Microsoft Edge CSP: [Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)ve [Browser/Allowflashtıklatorun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  ' Pluginsallodilimforurls ' veya ' PluginsBlockedForUrls ' tarafından kapsanmayan Web sitelerinin Adobe Flash eklentisini otomatik olarak çalıştırıp çalıştıramayacağını belirler. 

  - Tüm sitelerde Adobe Flash 'ı engellemek için ' Blockeklentiler ' seçeneğini belirleyin
  - Adobe Flash 'ın çalışmasına izin vermek, ancak kullanıcının uygulamayı başlatmak için yer tutucuya tıklamasına izin vermek için ' ClickToPlay ' seçeneğini belirleyin.
  
  Herhangi bir durumda, ' Pluginsallodilimforurls ' ve ' PluginsBlockedForUrls ' ilkeleri ' DefaultPluginsSetting ' üzerinden önceliklidir. Otomatik kayıttan yürütmeye yalnızca ' Pluginsallodilimforurls ' ilkesinde açık olarak listelenen etki alanları için izin verilir. 
   Tüm siteler için otomatik kayıttan yürütmeyi etkinleştirmek istiyorsanız, bu listeye http://* ve https://* eklemeyi göz önünde bulundurun.

  - Bu ilkeyi *Yapılandırılmadı*olarak ayarlarsanız, Kullanıcı bu ayarı el ile değiştirebilir. * 2 = Adobe Flash eklentisini engelle * 3 = önceki ' 1 ' seçenek kümesini izin ver-All ' ı oynatmak için tıklayın, ancak bu işlev artık yalnızca ' Pluginsallodilimforurls ' ilkesi tarafından işlenir. ' 1 ' kullanan mevcut ilkeler tıklama-yürütme modunda çalışır.  

  - **Varsayılan Adobe Flash ayarı**  
    **Varsayılan**: Adobe Flash eklentisini engelle

- **Her site için site yalıtımını etkinleştir**  
  **Varsayılan**: etkin  

  ' SitePerProcess ' ilkesi, kullanıcıların tüm siteleri yalıtma için varsayılan davranışı yerine almasını engellemek için kullanılabilir. Ayrıca, ek ve daha hassas kaynakları yalıtmak için ısotekaynakları ilkesini de kullanabilirsiniz.

  - Bu ilke *etkin*olarak ayarlandığında, kullanıcılar her sitenin kendi sürecinde çalıştığı varsayılan davranışı geri çevirebilir. 
  - *Devre dışı* veya *yapılandırılmamış*olarak kullanırsanız, Kullanıcı site yalıtımını devre dışı bırakabilirsiniz. (Örneğin, edge://flags içinde "site yalıtımını devre dışı bırak" girişini kullanarak) İlkeyi devre dışı bırakmak veya ilkeyi yapılandırmak, site yalıtımını kapatamaz.

- **Desteklenen kimlik doğrulama şemaları**  
  **Varsayılan**: etkin  

  Hangi HTTP kimlik doğrulama düzenlerinin desteklendiğini belirtir. İlkeyi şu değerleri kullanarak yapılandırabilirsiniz: ' Basic ', ' Digest ', ' NTLM ' ve ' anlaş '. Birden çok değeri virgülle ayırın. Bu ilkeyi yapılandırmazsanız dört düzen de kullanılır.

  - **Desteklenen kimlik doğrulama şemaları**  
    Aşağıdaki seçeneklerden seçim yapın:
    - Temel
    - Bilgisi
    - NTLM *(varsayılan olarak seçilidir)*
    - Anlaş *(varsayılan olarak seçilidir)*

- **Parola yöneticisine parolaların kaydedilmesini etkinleştir**  
  **Varsayılan**: devre dışı  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Kullanıcı parolalarını kaydetmek için Microsoft Edge 'i etkinleştirin.
  - Bu ilkeyi etkinleştirirseniz kullanıcılar parolalarını Microsoft Edge 'e kaydedebilir. Siteyi daha sonra ziyaret ettiklerinde, Microsoft Edge parolayı otomatik olarak girer.
  - Bu ilkeyi devre dışı bırakırsanız, kullanıcılar yeni parolaları kaydedemez, ancak daha önce kaydedilen parolaları kullanmaya devam edebilirler.
  
  Bu ilkeyi *etkin* veya *devre dışı*olarak ayarlarsanız, kullanıcılar Microsoft Edge 'de bu ilkeyi değiştiremez veya geçersiz kılamazsınız.
  
  Bunu *Yapılandırılmadı*olarak ayarlarsanız, kullanıcılar parolaları kaydedebilir ve bu özelliği kapatabilir.

- **Hangi uzantıların yükleneyüklenmediğini denetleme**  
  **Varsayılan**: etkin  

  Kullanıcıların Microsoft Edge 'e yükleyene özel uzantıları listeleyin. Bu ilkeyi dağıttığınızda, bu listede daha önce yüklenmiş olan uzantılar devre dışıdır ve Kullanıcı bunları etkinleştiremeyecektir. Engellenen uzantılar listesinden bir öğeyi kaldırırsanız, bu uzantı önceden yüklenmiş olduğu her yerde otomatik olarak yeniden etkinleştirilir.
  
  **\*** İzin verilenler listesinde açıkça listelenmeyen tüm uzantıları engellemek için kullanın. Bu ilke *Yapılandırılmadı*olarak ayarlandıysa, kullanıcılar Microsoft Edge 'de herhangi bir uzantıyı yükleyebilir.
  
  Örnek değer: extension_id1 extension_id2.  
  <br>
  - **Uzantı kimlikleri kullanıcının yüklemesi engellenmelidir (veya * tümü için)**  
    **Ekle** ' yi seçin ve ek uzantıları belirtin. **\*** Varsayılan olarak seçilidir.

- **Microsoft Defender SmartScreen 'i yapılandırma**  
  **Varsayılan**: etkin  
  Microsoft Edge CSP: [tarayıcı/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Bu ilke ayarı, Microsoft Defender SmartScreen 'i açıp kullanmayacağınızı yapılandırmanızı sağlar. Microsoft Defender SmartScreen, kullanıcılarınızın olası kimlik avı dolandırıcılarından ve kötü amaçlı yazılımlardan korunmasına yardımcı olmak için uyarı iletileri sağlar.
  
  - Varsayılan olarak, Microsoft Defender SmartScreen açıktır. Bu ayarı etkinleştirirseniz, Microsoft Defender SmartScreen açık olur ve kullanıcılar bu özelliği kapatamaz.
  - Bu ayarı devre dışı bırakırsanız, Microsoft Defender SmartScreen kapalıdır ve kullanıcılar açamaz.
  - *Yapılandırılmadı*olarak ayarlandığında, kullanıcılar Microsoft Defender SmartScreen 'i kullanıp kullanmayacağınızı seçebilirler.
  
  Bu ilke yalnızca Microsoft etkin bir etki alanına katılmış Windows örneklerinde veya cihaz yönetimi için kaydedilen Windows 10 Pro veya Enterprise örneklerinde kullanılabilir.

- **Kullanıcı düzeyindeki yerel mesajlaşma konaklarına izin ver (yönetici izinleri olmadan yüklenir)**  
  **Varsayılan**: devre dışı

  Yerel mesajlaşma konakları için Kullanıcı düzeyinde yüklemeyi mümkün. 
  - Bu ilkeyi devre dışı bırakırsanız, Microsoft Edge yalnızca sistem düzeyinde yüklü yerel mesajlaşma Konakları kullanır. Varsayılan olarak, bu ilkeyi yapılandırmazsanız, Microsoft Edge kullanıcı düzeyindeki yerel mesajlaşma ana bilgisayarlarının kullanılmasına izin verir.

::: zone-end

## <a name="next-steps"></a>Sonraki adımlar

- [Güvenlik temelleri hakkında bilgi edinin](security-baselines.md)
- [Çakışmaları önleyin](security-baselines.md#avoid-conflicts)
- [Intune'da ilke ve profil sorunları giderme](../configuration/troubleshoot-policies-in-microsoft-intune.md)