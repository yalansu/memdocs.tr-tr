---
title: Microsoft Bağlı Önbellek
titleSuffix: Configuration Manager
description: Teslim Iyileştirme için Configuration Manager dağıtım noktanızı yerel bir önbellek sunucusu olarak kullanma
ms.date: 09/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a42e0937748ecd31b16698904f724260b9b60512
ms.sourcegitcommit: f575b13789185d3ac1f7038f0729596348a3cf14
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2020
ms.locfileid: "90039304"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Configuration Manager 'de Microsoft bağlı önbelleği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3555764-->

Sürüm 1906 ' den başlayarak dağıtım noktalarınıza Microsoft bağlı önbellek sunucusu yükleyebilirsiniz. Bu içeriği şirket içinde önbelleğe alarak istemcileriniz, WAN bağlantılarını korumaya yardımcı olabilecek teslim Iyileştirme özelliğinden faydalanabilirsiniz.

> [!NOTE]
> Sürüm 1910 ' den başlayarak, bu özellik artık **Microsoft bağlı önbelleği**olarak adlandırılmaktadır. Daha önce teslim Iyileştirmesi-ağ önbelleği olarak bilinirdi.

Bu önbellek sunucusu teslim Iyileştirmesi tarafından indirilen içerik için isteğe bağlı bir saydam önbellek işlevi görür. Bu sunucunun yalnızca yerel Configuration Manager sınır grubunun üyelerine sunulmakta olduğundan emin olmak için istemci ayarlarını kullanın.

Bu önbellek Configuration Manager dağıtım noktası içeriğinden ayrıdır. Dağıtım noktası rolüyle aynı sürücüyü seçerseniz, içeriği ayrı olarak depolar.

> [!Note]  
> Bağlı önbellek sunucusu, Windows Server 'da yüklü bir uygulamadır. Bu uygulama hala geliştirme aşamasındadır.

## <a name="how-it-works"></a>Nasıl çalışır?

İstemcileri bağlı önbellek sunucusunu kullanacak şekilde yapılandırdığınızda, artık internet 'ten Microsoft tarafından yönetilen bir içerik isteğinde bulunmaz. İstemciler bu içeriği dağıtım noktasında yüklü olan önbellek sunucusundan ister. Şirket içi sunucu, uygulama Isteği yönlendirme (ARR) için IIS özelliğini kullanarak bu içeriği önbelleğe alır. Ardından, önbellek sunucusu aynı içerik için gelecekteki istekleri hızlıca yanıtlayabilir. Bağlı önbellek sunucusu kullanılamıyorsa veya içerik henüz önbelleğe alınmamışsa, istemciler içeriği internet 'ten indirir. İstemciler, içeriğin bölümlerini ağdaki eşlerden indirmek için teslim Iyileştirmesi da kullanır.

![Bağlı önbelleğin nasıl çalıştığına ilişkin diyagram](media/3555764-microsoft-connected-cache.png)

1. İstemci güncelleştirmeleri denetler ve içerik teslim ağının (CDN) adresini alır.

2. Configuration Manager, istemci üzerindeki, önbellek sunucusu adı da dahil olmak üzere teslim Iyileştirme (DO) ayarlarını yapılandırır.

3. İstemci A, DO Cache sunucusundan içerik ister.

4. Önbellek içeriği içermiyorsa, DO Cache Server onu CDN 'den alır.

5. Önbellek sunucusu yanıt veremezse, istemci CDN 'den içerik indirir.

6. İstemciler, eşlerden içerik parçalarını almak için bunu kullanır.

## <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar

- Aşağıdaki yapılandırmalara sahip *Şirket içi* dağıtım noktası:

  - Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 veya Windows Server 2019 çalıştırma

  - 80 numaralı bağlantı noktasında etkin olan varsayılan Web sitesi

  - IIS [uygulama Isteği yönlendirme](/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) özelliğini önceden yüklemeyin. Bağlı önbellek, ARR 'yi yüklüyor ve ayarlarını yapılandırır. Microsoft, bağlı önbelleğin ARR yapılandırmasının bu özelliği de kullanan sunucudaki diğer uygulamalarla çakışmamasını garanti edemez.

  - Dağıtım noktası, Microsoft bulutuna internet erişimi gerektirir. Belirli URL 'Ler, bulut özellikli belirli içeriklere göre farklılık gösterebilir. Teslim iyileştirme için uç noktalara de izin vermeyi unutmayın. Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../network/internet-endpoints.md).

  - Sürüm 2002 ' den başlayarak, bağlı önbellek uygulaması internet erişimi için kimliği doğrulanmamış bir ara sunucu kullanabilir. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server).<!-- 5856396 -->

- Windows 10 sürüm 1709 veya üstünü çalıştıran istemciler

## <a name="enable-connected-cache"></a>Bağlı önbelleği etkinleştir

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin.

1. Bir şirket *içi* dağıtım noktası seçin ve ardından şeritte **Özellikler**' i seçin.

1. Dağıtım noktası rolünün özellikleri ' nde, **genel** sekmesinde, aşağıdaki ayarları yapılandırın:  

    1. **Bu dağıtım noktasını Microsoft bağlı önbellek sunucusu olarak kullanılmak üzere etkinleştirme** seçeneğini etkinleştirin  

        Lisans koşullarını görüntüleyin ve kabul edin.

    2. **Kullanılacak yerel sürücü**: önbellek için kullanılacak diski seçin. **Otomatik** , en fazla boş alana sahip diski kullanan varsayılan değerdir. <sup> [1. nota](#bkmk_note1)</sup>  

        > [!Note]  
        > Bu sürücüyü daha sonra değiştirebilirsiniz. Önbelleğe alınmış tüm içerikler, yeni sürücüye kopyalamadıkça kaybedilir.

    3. **Disk alanı**: GB cinsinden veya toplam disk alanının yüzdesi cinsinden ayrılacak disk alanı miktarını seçin. Varsayılan olarak, bu değer 100 GB 'dir.

        > [!Note]  
        > Varsayılan önbellek boyutu çoğu müşteri için yeterli olmalıdır. Önbellek boyutunu daha sonra ayarlayabilirsiniz.
        >
        > Diskteki önbellek boyutu ayrılan alanı aşarsa, ARR, yerleşik buluşsal yöntemlerini temel alarak içeriği kaldırarak boşluğu temizler.<!-- SCCMDocs#2045 -->

    4. **Bağlı önbellek sunucusunu devre dışı bırakırken önbelleği sakla**: önbellek sunucusunu kaldırırsanız ve bu seçeneği etkinleştirirseniz, sunucu önbelleğin içeriğini diskte tutar.  

1. İstemci ayarları ' nda, **teslim iyileştirme** grubunda, **Configuration Manager tarafından yönetilen cihazları Içerik Indirme Için Microsoft bağlı önbellek sunucularını kullanacak şekilde**yapılandırma ayarını yapılandırın.  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a> Note 1: sürücü seçimi hakkında

**Otomatik**' i seçerseniz, Configuration Manager bağlı önbellek bileşenini yüklediğinde, **no_sms_on_drive. SMS** dosyasını kabul eder. Örneğin, dağıtım noktası dosyasına sahiptir `C:\no_sms_on_drive.sms` . C: sürücüsü en fazla boş alana sahip olsa bile Configuration Manager bağlı önbelleği, önbelleği için başka bir sürücü kullanacak şekilde yapılandırır.

Zaten **no_sms_on_drive. SMS** dosyası olan belirli bir sürücü seçerseniz Configuration Manager dosyayı yoksayar. Bağlı önbelleği bu sürücüyü kullanacak şekilde yapılandırmak açık bir amaç. Örneğin, dağıtım noktası dosyasına sahiptir `F:\no_sms_on_drive.sms` . Dağıtım noktası özelliklerini **f:** sürücüsünü kullanacak şekilde açıkça yapılandırdığınızda, Configuration Manager bağlı önbelleği önbelleğinin f: sürücüsünü kullanacak şekilde yapılandırır.

Bağlı önbelleği yükledikten sonra sürücüyü değiştirmek için:

- Dağıtım noktası özelliklerini belirli bir sürücü harfini kullanacak şekilde el ile yapılandırın.

- Otomatik olarak ayarlandıysa, önce **no_sms_on_drive. SMS** dosyasını oluşturun. Ardından, bir yapılandırma değişikliğini tetiklemek için dağıtım noktası özelliklerinde bazı değişiklikler yapın.

### <a name="automation"></a>Otomasyon

<!-- SCCMDocs#1911 -->

Bir dağıtım noktasındaki Microsoft bağlı önbellek ayarlarının yapılandırılmasını otomatikleştirmek için Configuration Manager SDK 'sını kullanabilirsiniz. Tüm site rolleri için olduğu gibi, [SMS_SCI_SYSRESUSE WMI sınıfını](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)kullanın. Daha fazla bilgi için bkz. [Site rollerini programlama](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles).

Dağıtım noktası için **SMS_SCI_SysResUse** örneğini güncelleştirdiğinizde, aşağıdaki özellikleri ayarlayın:

- **AgreeDOINCLicense**: `1` Lisans koşullarını kabul edecek şekilde ayarlayın.
- **Bayraklar**: Etkinleştir `|= 4` , devre dışı bırak `&= ~4`
- **DiskSpaceDOINC**: veya olarak ayarla `Percentage``GB`
- **RetainDOINCCache**: veya olarak ayarla `0``1`
- **Localdrivedoınc**: `Automatic` olarak, veya gibi belirli bir sürücü harfini ayarla `C:``D:`

## <a name="verify"></a>Doğrulama

İstemciler bulut tarafından yönetilen içeriği indirdiğinde dağıtım noktanınızdan yüklü olan önbellek sunucusundan teslim Iyileştirmesi kullanırlar. Bulut tarafından yönetilen içerik aşağıdaki türleri içerir:

- Microsoft Mağazası uygulamaları
- Diller gibi isteğe bağlı Windows özellikleri
- [İş ilkeleri için Windows Update](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)etkinleştirirseniz: Windows 10 özellik ve kalite güncelleştirmeleri
- [Ortak yönetim iş yükleri](../../../comanage/workloads.md)için:
  - Iş için Windows Update: Windows 10 özellik ve kalite güncelleştirmeleri
  - Office Tıkla-Çalıştır uygulamaları: Microsoft 365 uygulamalar ve güncelleştirmeler
  - İstemci uygulamaları: Microsoft Store uygulamalar ve güncelleştirmeler
  - Endpoint Protection: Windows Defender tanım güncelleştirmeleri

Windows 10 sürüm 1809 veya sonraki sürümlerde, **Get-teslimat Yoptimizationstatus** Windows PowerShell cmdlet 'i ile bu davranışı doğrulayın. Cmdlet çıkışında **BytesFromCacheServer** değerini gözden geçirin. Daha fazla bilgi için bkz. [Izleyici teslim iyileştirmesi](/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

Önbellek sunucusu herhangi bir HTTP hatası döndürürse, teslim Iyileştirme istemcisi özgün bulut kaynağına geri döner.

Daha ayrıntılı bilgi için bkz. [Configuration Manager Microsoft bağlı önbellek sorunlarını giderme](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a> Intune Win32 uygulamaları için destek

<!--5032900-->

Sürüm 1910 ' den başlayarak, Configuration Manager dağıtım noktalarınızdaki bağlı önbelleği etkinleştirdiğinizde, bu kişiler Microsoft Intune Win32 uygulamalarını ortak yönetilen istemcilere sunabilir.

### <a name="prerequisites"></a>Ön koşullar

#### <a name="client"></a>İstemci

- İstemciyi en son sürüme güncelleştirin.

- İstemci cihazının en az 4 GB belleğe sahip olması gerekir.

    > [!TIP]
    > Aşağıdaki Grup İlkesi ayarını kullanın: Windows > > bileşenleri > Yönetim Şablonları > bilgisayar yapılandırması, **Eş önbelleğe alma özelliğinin (GB cinsinden) kullanımını sağlamak için gereken en düşük RAM kapasitesi (dahil)**.

#### <a name="site"></a>Site

- Dağıtım noktasında bağlı önbelleği etkinleştirin. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği](microsoft-connected-cache.md).

- İstemci ve bağlı önbellek özellikli dağıtım noktasının aynı sınır grubunda olması gerekir.

- [**Teslim iyileştirme**](../../clients/deploy/about-client-settings.md#delivery-optimization) grubunda aşağıdaki istemci ayarlarını etkinleştirin:

  - **Teslim Iyileştirme grubu KIMLIĞI için Configuration Manager sınır grupları kullanma**
  - **Yapılandırma Yöneticisi tarafından yönetilen cihazların, içerik indirme için Microsoft bağlı önbellek sunucularını kullanmasını etkinleştir**

- **Ortak yönetilen cihazlar için**yayın öncesi özelliği istemci uygulamalarını etkinleştirin. Daha fazla bilgi için bkz. [yayın öncesi Özellikler](../../servers/manage/pre-release-features.md).

- Ortak Yönetimi etkinleştirin ve **istemci uygulamaları** Iş yükünü **pilot Intune** veya **Intune**'a geçirin. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

  - [İş yükleri-Istemci uygulamaları](../../../comanage/workloads.md#client-apps)
  - [Ortak yönetimi etkinleştirme](../../../comanage/how-to-enable.md)
  - [İş yüklerinin Intune'a geçişi](../../../comanage/how-to-switch-workloads.md)

    Pilot ' da, istemciyi Istemci uygulamaları için pilot koleksiyonuna ekleyin.

#### <a name="intune"></a>Intune

- Bu özellik yalnızca Intune Win32 uygulama türünü destekler.

  - Bu amaçla Intune 'da yeni bir uygulama oluşturun ve atayın (dağıtın). (Intune sürüm 1811 ' den önce oluşturulan uygulamalar çalışmaz.) Daha fazla bilgi için bkz. [Intune Win32 uygulama yönetimi](/intune/apps/apps-win32-app-management).

  - Uygulamanın boyutunun en az 100 MB olması gerekir.
  
    > [!TIP]
    > Aşağıdaki Grup İlkesi ayarını kullanın: bilgisayar yapılandırma > Yönetim Şablonları > Windows bileşenleri > teslim Iyileştirmesi > **En düşük eş önbelleğe alma Içerik dosyası boyutu (MB)**.

## <a name="see-also"></a>Ayrıca bkz.

[Windows 10 güncelleştirmelerini teslim Iyileştirme ile iyileştirme](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Configuration Manager 'de Microsoft bağlı önbelleği sorunlarını giderme](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
