---
title: Windows Embedded cihazlarına istemci dağıtımını planlama
titleSuffix: Configuration Manager
description: Configuration Manager 'da Windows Embedded cihazlarına istemci dağıtımını planlayın.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623125ad64c7ed421ea209137eb68f17891d7a81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714020"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Configuration Manager 'da Windows Embedded cihazlarına istemci dağıtımını planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<a name="BKMK_DeployClientEmbedded"></a>Windows katıştırılmış cihazınız Configuration Manager istemcisi içermiyorsa, cihazın gerekli bağımlılıkları karşılaması halinde istemci yükleme yöntemlerinden herhangi birini kullanabilirsiniz. Katıştırılmış cihaz yazma filtrelerini destekliyorsa istemciyi yüklemeden önce bu filtreleri devre dışı bırakmanız ve istemci yüklenip bir siteye atandıktan sonra tekrar etkinleştirmeniz gerekir.  

 Filtreleri devre dışı bıraktığınızda, filtre sürücülerini devre dışı bırakmamanız gerektiğine dikkat edin. Genellikle bu sürücüler bilgisayar başlatıldığında otomatik olarak başlatılır. Sürücüleri devre dışı bırakmak, istemcinin yüklenmesini engeller veya yazma filtre düzenlemesini etkileyerek istemci işlemlerinin başarısız olmasına neden olur. Her bir yazma filtresiyle ilişkili çalışır halde kalması gereken hizmetler şunlardır:  

|Yazma Filtresi Türü|Sürücü|Tür|Açıklama|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Çekirdek|Korumalı birimlerde kesim düzeyinde G/Ç yönlendirmesi uygular.|  
|FBWF|FBWF|Dosya sistemi|Korumalı birimlerde dosya düzeyinde G/Ç yönlendirmesi uygular.|  
|UWF|uwfreg|Çekirdek|UWF Kayıt Defteri Yeniden Yönlendirici|  
|UWF|uwfs|Dosya Sistemi|UWF Dosya Yeniden Yönlendirici|  
|UWF|uwfvol|Çekirdek|UWF Birim Yöneticisi|  

 Yazma filtreleri, yazılım yükleme gibi değişiklikler yaptığınızda katıştırılmış cihaz üzerindeki işletim sisteminin nasıl güncelleştirileceğini denetler. Yazma filtreleri etkinleştirildiğinde değişiklikler doğrudan işletim sisteminde yapılmak yerine geçici bir katmana yeniden yönlendirilir. Değişiklikler yalnızca katmana yazılırsa, katıştırılmış cihaz kapandığında kaybedilir. Ancak, yazma filtreleri geçici olarak devre dışı kalırsa katıştırılmış cihaz her yeniden başlatıldığında değişiklikleri tekrar yapmanıza (veya yazılımı yeniden yüklemenize) gerek kalmaması için değişiklikler kalıcı hale getirilebilir. Ancak, yazma filtrelerinin geçici olarak devre dışı bırakılması ve ardından tekrar etkinleştirilmesi için bir veya daha fazla yeniden başlatma gerekir; böylece yeniden başlatmaların iş saatleri dışında gerçekleştirilmesi için bakım pencerelerini yapılandırarak bunun ne zaman meydana geleceğini denetlemek istersiniz.  

 Uygulamalar, görev dizileri, yazılım güncelleştirmeleri ve Endpoint Protection istemcisi gibi yazılımlar dağıtırken yazma filtrelerini otomatik olarak devre dışı bırakıp tekrar etkinleştirecek şekilde seçenekleri yapılandırabilirsiniz. Buradaki özel durum, otomatik düzeltme kullanan yapılandırma öğeleriyle yapılandırma temel çizgileri içindir. Bu senaryoda düzeltme her zaman katmanda oluşur, böylece yalnızca cihaz yeniden başlatılana kadar mevcut olur. Düzeltme sonraki değerlendirme döngüsünde tekrar uygulanır, ancak yalnızca başlangıçta silinen katmana uygulanır. Düzeltme değişikliklerini yürütmek üzere Configuration Manager zorlamak için yapılandırma temel çizgisini ve ardından değişikliği uygulamayı destekleyen başka bir yazılım dağıtımını mümkün olan en kısa sürede dağıtabilirsiniz.  

 Yazma filtreleri devre dışı bırakılırsa Yazılım Merkezini kullanarak Windows Katıştırılmış cihazlarına yazılım yükleyebilirsiniz. Ancak, yazma filtreleri etkinleştirilirse, yükleme başarısız olur ve Configuration Manager uygulamayı yüklemek için yeterli izniniz olmadığını belirten bir hata mesajı görüntüler.  

> [!WARNING]  
>  Değişiklikleri yürütmek için Configuration Manager seçeneklerini seçmeseniz bile, değişiklikleri işleyen başka bir yazılım yüklemesi veya değişikliği yapılırsa değişiklikler uygulanabilir. Bu senaryoda yeni değişikliklere ek olarak özgün değişiklikler uygulanır.  

 Configuration Manager değişiklikleri kalıcı hale getirmek için yazma filtrelerini devre dışı bıraktığında, yalnızca yerel yönetim haklarına sahip kullanıcılar oturum açabilir ve katıştırılmış cihazı kullanabilir. Bu süre boyunca düşük haklara sahip kullanıcılar kilitlenir ve bilgisayarın bakımda olduğu için kullanılamadığını belirten bir ileti görürler. Bu özellik, cihazı değişikliklerin kalıcı olarak uygulanabileceği bir durumdayken korumaya yardımcı olur ve bu bakım modu kilitleme davranışı, kullanıcıların bu cihazlarda oturum açmayacağı bir süre boyunca bakım penceresini yapılandırmanın diğer nedenidir.  

 Configuration Manager, aşağıdaki yazma filtresi türlerini yönetmeyi destekler:  

- Dosya tabanlı yazma Filtresi (FBWF)-daha fazla bilgi Için [dosya tabanlı yazma Filtresi](https://go.microsoft.com/fwlink/?LinkID=204717)konusuna bakın.  

- Gelişmiş Yazma filtresi (EWF) RAM-daha fazla bilgi Için [Gelişmiş Yazma filtresi](https://go.microsoft.com/fwlink/?LinkId=204718)konusuna bakın.  

- Birleşik Yazma filtresi (UWF)-daha fazla bilgi Için bkz. [Birleşik Yazma filtresi](https://go.microsoft.com/fwlink/?LinkId=309236).  

  Configuration Manager, Windows Embedded cihazı EWF RAM reg modundayken yazma Filtresi işlemlerini desteklemez.  

> [!IMPORTANT]
>  Seçim yaparsanız, daha fazla verimlilik ve daha yüksek ölçeklenebilirlik için Configuration Manager dosya tabanlı yazma filtreleri (FBWF) kullanın.
> 
> **Yalnızca FBWF kullanan cihazlar için:** Cihaz yeniden başlatmaları arasında istemci durumu ve envanter verilerini kalıcı hale getirmek için aşağıdaki özel durumları yapılandırın:  
> 
> - CCMıNSTALLDIR\\*. sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Windows Embedded 8.0 ve üzeri çalıştıran cihazlar joker karakter içeren hariç tutmaları desteklemez. Bu cihazlar üzerinde aşağıdaki özel durumları tek tek yapılandırmanız gerekir:  
> 
> - CCMINSTALLDIR içindeki .sdf uzantısına sahip tüm dosyalar, genellikle:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **Yalnızca FBWF ve UWF kullanan cihazlar için:** Bir çalışma grubundaki istemciler, yönetim noktalarında kimlik doğrulaması için sertifika kullandıklarında, istemcinin yönetim noktasıyla iletişim kurmaya devam ettiğinden emin olmak için özel anahtarı da dışmalısınız. Bu cihazlarda, aşağıdaki özel durumları yapılandırın:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> Configuration Manager istemcisinin Yukarıdaki **önemli** kutusunda belgelenenlerden başka özel durumlar gerekmez. Ek Configuration Manager veya WMI (WBEM) ile ilgili özel durumlar eklemek, hizmet verme modunda veya yeniden başlatma döngülerine sahip cihazlarda bulunan cihazlar da dahil olmak üzere Configuration Manager hatalara neden olabilir. Gereksiz özel durumlar Configuration Manager istemci dizinini, CCMcache dizinini, CCMSetup dizinini, görev sırası önbellek dizinini, WBEM dizinini ve Configuration Manager ilgili kayıt defteri anahtarlarını içerir.

 Yazma filtresi etkinleştirilmiş Windows Embedded cihazlarını dağıtma ve yönetmeye yönelik örnek senaryo için Configuration Manager [Windows Embedded cihazlarında Configuration Manager istemcilerini dağıtma ve yönetmeye yönelik örnek senaryo](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md)bölümüne bakın.  

 Windows Katıştırılmış cihazları için görüntü oluşturma ve yazma filtreleri yapılandırma hakkında daha fazla bilgi için Windows Katıştırılmış belgelerinize bakın veya OEM ile iletişim kurun.  

> [!NOTE]
>  Yazılım dağıtımları ve yapılandırma öğeleri için geçerli platformları seçerken bunlar belirli sürümler yerine Windows Katıştırılmış aileleri gösterir. Belirli bir Windows Katıştırılmış sürümü liste kutusundaki seçeneklerle eşlemek için aşağıdaki listeyi kullanın:  
> 
> - **Windows XP (32 bit) tabanlı Katıştırılmış İşletim Sistemleri** şunlardır:  
> 
>   -   Windows XP Embedded  
>   -   Hizmet Noktası için Windows Embedded  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Windows 7 (32 bit) tabanlı Katıştırılmış işletim sistemleri** şunlardır:  
> 
>   -   Windows Embedded Standard 7 (32 bit)  
>   -   Windows Embedded POSReady 7 (32 bit)  
>   -   Windows ThinPC  
>   -   **Windows 7 (64 bit) tabanlı katıştırılmış işletim sistemleri** şunları içerir:  
> 
>   -   Windows Embedded Standard 7 (64 bit)  
>   -   Windows Embedded POSReady 7 (64 bit)
