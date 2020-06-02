---
title: Windows uygulamaları oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager 'da Windows uygulamaları oluşturma ve dağıtma hakkında daha fazla bilgi edinin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ddd01055ac6edf2872854c93cc5172b396052ad2
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270863"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Configuration Manager Windows uygulamaları oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

[Uygulama oluşturmaya](../deploy-use/create-applications.md)yönelik diğer Configuration Manager gereksinimleri ve yordamlarına ek olarak, Windows cihazları için uygulama oluştururken ve dağıtırken aşağıdaki noktaları da göz önünde bulundurmanız gerekir.  

## <a name="general-considerations"></a><a name="bkmk_general"></a>Genel hususlar  

Configuration Manager, Windows 8.1 ve Windows 10 cihazları için Windows uygulama paketi (. appx) ve uygulama paketi (. appxdemeti) biçimlerinin dağıtımını destekler.

Configuration Manager konsolunda bir uygulama oluşturduğunuzda, uygulama yükleme dosya **türünü** **Windows uygulama paketi ( \* . appx, \* . AppxPackage, \* . maltı, \* . msixdemeti)** olarak seçin. Genel olarak uygulama oluşturma hakkında daha fazla bilgi için bkz. [uygulama oluşturma](../deploy-use/create-applications.md). MSIX biçimi hakkında daha fazla bilgi için bkz. [MSIX biçimi desteği](#bkmk_msix).

> [!Note]  
> Yeni Configuration Manager özelliklerinden yararlanmak için önce istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a>Bir cihazdaki tüm kullanıcılar için Windows uygulama paketleri sağlama
<!--1358310-->
Cihazdaki tüm kullanıcılar için Windows uygulama paketi ile bir uygulama sağlayın. Bu senaryonun yaygın bir örneği, bir okuldaki öğrenciler tarafından kullanılan tüm cihazlara Minecseft: eğitim sürümü gibi Iş ve eğitim Microsoft Store bir uygulama sağlamadır. Daha önce Configuration Manager yalnızca Kullanıcı başına bu uygulamaları yüklemeyi destekler. Yeni bir cihazda oturum açtıktan sonra bir öğrenciye bir uygulamaya erişmeniz gerekir. Artık uygulama tüm kullanıcılar için cihaza sağlandığında, daha hızlı bir şekilde üretken olabilirler.

> [!Important]  
> Aynı Windows uygulama paketinin farklı sürümlerini yükleme, sağlama ve güncelleştirme konusunda dikkatli olun, bu durum beklenmedik sonuçlara neden olabilir. Bu davranış, uygulamayı sağlamak için Configuration Manager kullanılırken ve sonra kullanıcıların uygulamayı Microsoft Store güncelleştirmesine izin verirken meydana gelebilir. Daha fazla bilgi için bkz. [iş için Microsoft Store uygulamaları yönetirken](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)sonraki adım Kılavuzu.  

Configuration Manager istemcisi ile Windows 10 cihazlarına çevrimdışı uygulamalar dağıttığınızda, kullanıcıların Configuration Manager dağıtımlar dışındaki uygulamaları güncelleştirmesine izin vermez. Çevrimdışı uygulamalardaki güncelleştirmelerin denetimi, özellikle sınıfsallar gibi çok kullanıcılı ortamlarda önemlidir. Daha fazla bilgi için bkz. [Configuration Manager Ile iş ve eğitim için Microsoft Store uygulamaları yönetme](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).<!-- MEMDocs#316 -->

Configuration Manager, Windows 10 ' un tüm desteklenen sürümlerinde uygulama sağlamayı destekler.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Bu özellik için bir Windows uygulama dağıtım türü yapılandırmak için, **cihazdaki tüm kullanıcılar için bu uygulamayı sağlama**seçeneğini etkinleştirin. Daha fazla bilgi için bkz. [uygulama oluşturma](../deploy-use/create-applications.md).

> [!Note]  
> Sağlanan bir uygulamayı kullanıcıların zaten oturum açmış olduğu cihazlardan kaldırmanız gerekiyorsa, iki adet kaldırma dağıtımı oluşturmanız gerekir. İlk kaldırma dağıtımını cihazları içeren bir cihaz koleksiyonuna hedefleyin. İkinci kaldırma dağıtımını, sağlanan uygulamayla cihazlarda zaten oturum açmış olan kullanıcıları içeren bir kullanıcı koleksiyonuna hedefleyin. Bir cihazda sağlanan uygulamayı kaldırırken, Windows bu uygulamayı da kullanıcılar için kaldırmıyor.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a>MSIX biçimi desteği
<!--1357427-->

Configuration Manager, Windows 10 uygulama paketi (. msix) ve uygulama paketi (. msixdemeti) biçimlerini destekler. Windows 10 sürüm 1809 veya üzeri bu biçimleri destekler.

- MALTıYA genel bakış için [maltıya daha yakından](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix)bakın.  

- Yeni bir MSIX uygulaması oluşturma hakkında bilgi için bkz. [Insider Build 17682 ' de sunulan Msix desteği](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### <a name="convert-applications-to-msix"></a>Uygulamaları MALTıYA Dönüştür
<!--3607729, fka 1359029-->

Mevcut Windows Installer (. msi) uygulamalarınızı MSIX biçimine dönüştürün.

#### <a name="prerequisites-for-msix"></a>MSIX önkoşulları

- Windows 10 sürüm 1809 veya üstünü çalıştıran bir başvuru aygıtı  

- Bu cihazdaki Windows 'da yerel yönetici haklarına sahip bir kullanıcı olarak oturum açın  

- Bu cihaza aşağıdaki uygulamaları yükler:  

  - Configuration Manager konsolu  

  - Microsoft Store 'ten [Msix paketleme aracını](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) yükler  

  - [Msix paketleme aracı sürücüsünü](https://docs.microsoft.com/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers) yükler<!--SCCMDocs-pr issue #3091-->  

Bu cihaza başka herhangi bir uygulama veya hizmet yüklemeyin. Bu, başvuru sistemdir.

#### <a name="process-to-convert-applications-to-msix-format"></a>Uygulamaları MSIX biçimine dönüştürme işlemi

1. Configuration Manager konsolunu yükseltin, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.  

2. Windows Installer (. msi) dağıtım türüne sahip bir uygulama seçin.  

    > [!Note]  
    > Başvuru cihazından uygulamanın kaynak içeriğine erişebiliyor olmanız gerekir.  
    >
    > Uygulamanın adı özel karakter içeremez. Configuration Manager, uygulama adını çıkış dosyasının adı olarak kullanır.  
    >
    > Bu uygulamayı başvuru cihazına önceden yüklemeyin.  

3. Dönüştür ' ü seçin **. Şeritte MALTıDıR** .

Sihirbaz tamamlandığında, MSIX paketleme aracı sihirbazda belirttiğiniz konumda bir MSIX dosyası oluşturur. Bu işlem sırasında, uygulamayı başvuru cihazına sessizce Configuration Manager.

İşlem başarısız olursa, Özet sayfası günlük dosyasına daha fazla bilgi ile işaret eder. Kullanıcı durumunu yakalama hakkında bir hata varsa, Windows oturumunu kapatın. Yeniden oturum açmak bu sorunu çözebilir.

Bu MALTıDAN bu uygulamayı kullanmak için önce, istemcilerin ona güvenmesi için dijital olarak imzalamanız gerekir. Bu işlemle ilgili daha fazla bilgi için aşağıdaki makalelere bakın:

- [MSIX – Maltıpaketleme aracı – MSIX paketi imzalanıyor](https://docs.microsoft.com/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [SignTool kullanarak uygulama paketini imzalama](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Uygulamayı imzalamadan sonra, Configuration Manager uygulamada yeni bir dağıtım türü oluşturun. Daha fazla bilgi için bkz. [uygulama için dağıtım türleri oluşturma](../deploy-use/create-applications.md#bkmk_create-dt).

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a>Görev sırası dağıtım türü

<!--3555953-->

> [!Note]  
> Bu Configuration Manager sürümünde, görev sırası dağıtım türü bir yayın öncesi özelliktir. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../core/servers/manage/pre-release-features.md).  

Sürüm 2002 ' den başlayarak, görev dizilerini kullanarak karmaşık uygulamaları uygulama modeli aracılığıyla yükleyebilirsiniz. Uygulamayı yüklemek ya da kaldırmak için bir uygulamaya görev dizisi dağıtım türü ekleyin. Bu dağıtım türü aşağıdaki davranışları sağlar:

<!-- - Deploy an app task sequence to a user collection -->

- Uygulama görev dizisini yazılım merkezi 'nde bir simgeyle görüntüleyin. Bir simge, kullanıcıların uygulama görev sırasını bulmasını ve belirlemesini kolaylaştırır.

- Yerelleştirilmiş bilgiler dahil olmak üzere uygulama görev sırası için ek meta veri tanımlayın

Bir uygulamaya dağıtım türü olarak yalnızca işletim sistemi olmayan dağıtım görev sırası ekleyebilirsiniz. Yüksek etki, işletim sistemi dağıtımı veya işletim sistemi yükseltme görev dizileri desteklenmez. <!--A user-targeted deployment still runs in the user context of the local System account.-->

Bu dağıtım türünü bir uygulamaya eklediğinizde, **görev sırası** sayfasında özelliklerini yapılandırın. Daha fazla bilgi için bkz. [dağıtım türü **görev dizisi** seçenekleri](../deploy-use/create-applications.md#bkmk_dt-ts).

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Bir görev dizisi dağıtım türü için Önkoşullar

Özel bir görev sırası oluşturun:

- Yalnızca işletim sistemi olmayan dağıtım adımlarını kullanın, örneğin: **paketi yüklemeyi**, **komut satırını çalıştırmayı**veya **PowerShell betiği çalıştırmayı**. Desteklenen adımların tam listesini içeren daha fazla bilgi için bkz. [işletim sistemi dışı dağıtımlar için görev dizisi oluşturma](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- Görev sırası özellikleri, **Kullanıcı bildirimi** sekmesinde, yüksek etkili bir görev dizisi seçeneğini seçmeyin.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

Uygulamayı oluştururken, bir görev dizisi dağıtım türü eklemek için, Kullanıcı hesabınızın görev dizilerini okuma izni olması gerekir.<!-- 6348976 --> Bu izinleri yapılandırmak için aşağıdaki seçeneklerden birini kullanın:

- Uygulama yöneticisinin Kullanıcı hesabını yerleşik **salt okunurdur analist** rolüne ekleyin. Bu rol, tüm Configuration Manager nesnelerini görüntülemesine izin verir.

- Özel bir rol oluşturmak için yerleşik **Uygulama Yöneticisi** rolünü kopyalayın. **Görev dizisi paketi** nesnesine **Oku** iznini ekleyin.

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Bir görev dizisi dağıtım türü için bilinen sorunlar

- Bir kullanıcı koleksiyonuna henüz bir uygulama görev sırası dağıtamazsınız

- Bu görev dizisinde **uygulama Install** adımını kullanmayın. Uygulama yüklemek için [paketi yüklemek](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) adımını kullanın.

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a>Evrensel Windows Platformu (UWP) uygulamaları için destek  

Windows 10 cihazlarında iş kolu uygulamalarını yüklemek için dışarıdan yükleme anahtarı gerekmez. Ancak, Windows 'da dışarıdan yüklemeyi etkinleştirmek için kayıt defteri anahtarının `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` değeri **1**olmalıdır.  

Bu kayıt defteri anahtarını yapılandırmazsanız, cihaza ilk kez uygulama dağıttığınızda Configuration Manager bu değeri otomatik olarak **1** ' e ayarlar. Bu değeri **0**olarak ayarlarsanız Configuration Manager değeri otomatik olarak değiştiremez ve iş kolu uygulama dağıtımınız başarısız olur.  

UWP iş kolu uygulamalarını dijital olarak imzalayın. Uygulamayı dağıttığınız her cihazda güvenilen bir kod imzalama sertifikası kullanın. Kuruluşunuzun PKI 'ınızdan sertifikaları kullanın veya genel kök sertifikaya zaten Windows tarafından güvenilen bir üçüncü taraf sağlayıcıdan sertifika satın alın.  

Mobil uygulama paketlerini imzalamak için, kullanılacak kod imzalama sertifikasının türünü öğrenmek üzere aşağıdaki tabloyu kullanın:

| Paket  | Symantec  | Symantec dışı  |
|---------|---------|---------|
| Windows 10 Mobile cihazlarında Universal **. appx** paketleri | Yes | Yes |
| **. xap** paketleri | Yes | Hayır |
| Windows 10 Mobile cihazlarına yüklemek için Windows Phone 8,1 için oluşturulan **appx** paketleri | Yes | Hayır |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a>MDM 'ye kayıtlı Windows 10 cihazlarına Windows Installer uygulamalarını dağıtma  

**MDM ( \* . msi) dağıtım türü aracılığıyla Windows Installer** , WINDOWS 10 çalıştıran MDM 'ye kayıtlı cihazlara Windows Installer tabanlı uygulamalar oluşturmanıza ve dağıtmanıza olanak tanır.  

Bu dağıtım türünü kullandığınızda, aşağıdaki noktaları göz önünde bulundurun:

- Yalnızca MSI uzantılı tek bir dosyayı karşıya yükleyin.  

- Configuration Manager, uygulamanın algılanması için dosyanın ürün kodunu ve ürün sürümünü kullanır.  

- Windows, uygulamanın varsayılan yeniden başlatma davranışını kullanır. Configuration Manager, uygulama yeniden başlatma davranışını denetlemez.  

- Tek bir kullanıcı için kullanıcı başına MSI paketleri yüklenir.  

- Cihazdaki tüm kullanıcılar için makine başına MSI paketleri yüklenir.  

- Configuration Manager uygulama güncelleştirmelerini destekler. Her sürümün MSI ürün kodu aynı olmalıdır.  
