---
title: Windows uygulamalarını dışarıdan yükleme
titleSuffix: Microsoft Intune
description: Intune’u kullanarak iş kolu uygulamalarını dağıtmak için bunları nasıl imzalayacağınızı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e44f1756-52e1-4ed5-bf7d-0e80363a8674
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: da43cab373021107a940ce0bd71c0f4986d5e907
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179630"
---
# <a name="sign-line-of-business-apps-so-they-can-be-deployed-to-windows-devices-with-intune"></a>Intune ile Windows cihazlarına dağıtmak için iş kolu uygulamalarını imzalayın

Bir Intune Yöneticisi olarak, Şirket Portalı uygulaması da dahil olmak üzere masaüstü veya Windows 10 Masaüstü & mobil cihazlara Windows 8.1 iş kolu (LOB) Universal uygulamaları dağıtabilirsiniz. Windows 8.1 *. appx* uygulamalarını masaüstü veya Windows 10 Masaüstü & mobil cihazlara dağıtmak Için, Windows cihazlarınız tarafından zaten güvenilen bir genel sertifika yetkilisinden kod imzalama sertifikası kullanabilir veya kendi sertifika yetkilinizi kullanabilirsiniz.

 > [!NOTE]
 > Windows 8.1 Masaüstü, dışarıdan yüklemeyi etkinleştirmek için bir kuruluş ilkesi veya dışarıdan Yükleme anahtarlarının (etki alanına katılmış cihazlar için otomatik olarak etkinleştirilir) kullanılmasını gerektirir. Daha fazla bilgi için bkz. [Windows 8 dışarıdan yükleme](https://blogs.technet.microsoft.com/scd-odtsp/2012/09/27/windows-8-sideloading-requirements-from-technet/).

## <a name="windows-10-sideloading"></a>Windows 10 dışarıdan yükleme

Windows 10 ' da, dışarıdan yükleme Windows 'un önceki sürümlerinden farklıdır:

- Kurumsal bir ilke kullanarak dışarıdan yükleme için bir cihazın kilidini açabilirsiniz. Intune, "güvenilir uygulama yüklemesi" adlı bir cihaz yapılandırma ilkesi sağlar. Bunu olarak ayarlamak, <allow> appx uygulamasını imzalamak için kullanılan sertifikaya zaten güvenecek olan cihazlar için gereklidir.

- Symantec telefon sertifikaları ve dışarıdan yükleme lisans anahtarları gerekli değildir. Ancak, şirket içi bir sertifika yetkilisi yoksa, bir genel sertifika yetkilisinden kod imzalama sertifikası edinmeniz gerekebilir. Daha fazla bilgi için bkz. [kod Imzalamaya giriş](https://docs.microsoft.com/windows/desktop/SecCrypto/cryptography-tools#introduction-to-code-signing).

### <a name="code-sign-your-app"></a>Uygulamanızı kodla imzalama

İlk adım, appx paketinizi yeniden kodlayabilirseniz. Ayrıntılar için bkz. [SignTool kullanarak uygulama paketini imzalama](https://docs.microsoft.com/windows/uwp/packaging/sign-app-package-using-signtool).

### <a name="upload-your-app"></a>Uygulamanızı karşıya yükleyin

Ardından, imzalanmış appx dosyasını karşıya yüklemeniz gerekir. Ayrıntılar için bkz. [Windows iş kolu uygulaması ekleme Microsoft Intune](lob-apps-windows.md).

Uygulamayı kullanıcılara veya cihazlara gereken şekilde dağıtırsanız, ınutne Şirket Portalı uygulamasına ihtiyacınız yoktur. Ancak, uygulamayı kullanıcılara kullanılabilir olarak dağıtırsanız, ortak Microsoft Store Şirket Portalı uygulamayı kullanabilir, Iş için özel Microsoft Store Şirket Portalı uygulamayı kullanabilir veya Intune Şirket Portalı uygulamasını imzalayıp el ile dağıtmanız gerekir.

### <a name="upload-the-code-signing-certificate"></a>Kod imzalama sertifikasını karşıya yükleme

Windows 10 cihazınız sertifika yetkilisine zaten güvenmezse, appx paketinizi imzaladıktan ve Intune hizmetine yükledikten sonra, kod imzalama sertifikasını Intune portalına yüklemeniz gerekir:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Kiracı Yönetimi**bağlayıcıları ' na tıklayın  >  **ve**  >  **Windows Kurumsal sertifikalarını**belirteçler yapın.
3. **Kod imzalama sertifika dosyası**altında bir dosya seçin.
4. *. Cer* dosyanızı seçin ve **Aç**' a tıklayın.
5. Sertifika dosyanızı Intune 'a eklemek için **karşıya yükle** ' ye tıklayın.

Artık, Intune hizmeti tarafından bir appx dağıtımı olan Windows 10 Masaüstü & mobil cihaz, ilgili kurumsal sertifikayı otomatik olarak indirir ve uygulamanın yüklemeden sonra çalışmasına izin verilir.

Intune yalnızca karşıya yüklenen en son. cer dosyasını dağıtır. Kuruluşunuz ile ilişkilendirilmemiş farklı geliştiriciler tarafından oluşturulmuş birden çok appx dosyası varsa, bu dosyalara sertifika imzalama için imzasız appx dosyaları sağlamanızı veya kuruluşunuz tarafından kullanılan kod imzalama sertifikasını sağlamanızı sağlamanız gerekir.

## <a name="how-to-renew-the-symantec-enterprise-code-signing-certificate"></a>Symantec kurumsal kod imzalama sertifikasını yenileme

Windows Phone 8,1 mobil uygulamaları dağıtmak için kullanılan sertifika, 28 2019 Şubat tarihinde kaldırılmıştır ve artık Symantec 'ten yenileme için kullanılamaz. Ayrıca, Intune, 10 Ağustos 2020 itibariyle Windows 10 Mobile desteğini de sonlandırdı.

## <a name="how-to-install-the-updated-certificate-for-line-of-business-lob-apps"></a>İş kolu (LOB) uygulamaları için güncelleştirilmiş sertifika yükleme

Windows Phone 8.1

Intune hizmeti, mevcut Symantec mobil kurumsal kod imzalama sertifikasının süresi dolduktan sonra bu platform için LOB uygulamalarını artık dağıtmaz.

Windows 8.1 Masaüstü/Windows 10 Masaüstü & Mobile

Sertifika döneminin süresi dolmuşsa, appx dosyaları başlatmayı durdurabilir. Yeni bir. cer dosyası edinmeniz ve dağıtılan her bir appx dosyasını kod imzalama ve tüm appx dosyalarını ve güncelleştirilmiş. cer dosyasını Intune portalının Windows Enterprise Certificates bölümüne yeniden yükleme yönergelerini izlemeniz gerekir.

## <a name="manually-deploy-windows-10-company-portal-app"></a>Windows 10 Şirket Portalı uygulamasını el ile dağıtma

Microsoft Store erişim sağlamak istemiyorsanız, Intune 'u Iş Microsoft Store (MSFB) ile tümleştirmemiş olsanız bile Windows 10 Şirket Portalı uygulamasını doğrudan Intune 'dan el ile dağıtabilirsiniz. Alternatif olarak, tümleştirdiyseniz, [MSFB kullanarak uygulama dağıtma](store-apps-windows.md)aracılığıyla şirket portalı uygulamasını dağıtabilirsiniz.

 > [!NOTE]
 > Bu seçeneğin kullanılması, her uygulama güncelleştirmesi yayımlandığında el ile güncelleştirme dağıtılmasını gerektirir.

1. [İş için Microsoft Store](https://www.microsoft.com/business-store) hesabınızda oturum açın ve şirket portalı uygulamasının **Çevrimdışı lisans** sürümünü edinin.  
2. Uygulamayı aldıktan sonra **Envanter** sayfasında uygulamayı seçin.  
3. **Platform** olarak **Windows 10 tüm cihazlar**’ı ve uygun **Mimari**’yi seçip sonra indirin. Bu uygulama için bir uygulama lisans dosyası gerekmez.
   ![Indirme için Windows 10 x86 paketi ayrıntılarının görüntüsü](./media/app-sideload-windows/Win10CP-all-devices.png)
4. "Gerekli çerçeveler" altındaki tüm paketleri indirin. Bu, x86, x64, ARM ve ARM64 mimarileri için yapılmalıdır. Bu, aşağıda gösterildiği gibi toplam 9 paket ile sonuçlanır.

   ![İndirilecek bağımlılık dosyalarının görüntüsü ](./media/app-sideload-windows/Win10CP-dependent-files.png)
5. Şirket Portalı uygulamasını Intune’a yüklemeden önce, paketlerin aşağıdaki şekilde yapılandırıldığı bir klasör (ör. C:&#92;Company Portal) oluşturun:
   1. Şirket Portalı paketini C:\Company Portal adresine koyun. Bu konumda bir Dependencies alt klasörü oluşturun.  
      ![APPXBUN dosyasıyla kaydedilen Dependencies klasörünün görüntüsü](./media/app-sideload-windows/Win10CP-Dependencies-save.png)
   2. Dokuz bağımlılık paketini Dependencies klasörüne yerleştirin.  
      Bağımlılıklar, bu biçimde yerleştirilmezse Intune tarafından tanınamazlar ve paketin karşıya yüklenmesi sırasında karşıya yüklenemezler. Bu durumda, karşıya yükleme aşağıdaki hatayı vererek başarısız olur.  
      <img alt="Error message - The Windows app dependency must be provided." src="./media/app-sideload-windows/Win10CP-error-message.png" width="200">
6. Intune'a dönün ve Şirket Portalı uygulamasını yeni bir uygulama olarak karşıya yükleyin. Uygulamayı, istenen hedef kullanıcı kümesine gerekli bir uygulama olarak dağıtın.  

Intune’un Evrensel uygulamaların bağımlılıklarını nasıl işlediği hakkında daha fazla bilgi edinmek için bkz. [Microsoft Intune MDM aracılığıyla bağımlılıkları olan bir appxbundle dağıtma](https://blogs.technet.microsoft.com/configmgrdogs/2016/11/30/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm/).  

### <a name="how-do-i-update-the-company-portal-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>Eski uygulamaları mağazadan zaten yüklediklerinde, kullanıcılarımın cihazlarındaki Şirket Portalı güncelleştirmek Nasıl yaparım? mı?

Kullanıcılarınız Windows 8.1 Şirket Portalı uygulamaları mağazadan zaten yüklediyse, sizin veya kullanıcınız tarafından hiçbir eylemde bulunması gerekmeden otomatik olarak yeni sürüme güncelleştirilmeleri gerekir. Bu güncelleştirme gerçekleşmezse, kullanıcılarınızdan cihazlarında Mağaza uygulamaları için otomatik güncelleştirmeleri etkinleştirdiklerini denetlemelerini isteyin.

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Dışarıdan yüklenen Windows 8.1 Şirket Portalı uygulamamı Windows 10 Şirket Portalı uygulamasına nasıl yükseltebilirim?

Önerilen geçiş yolumuz, dağıtım eylemini "Kaldır" olarak ayarlayarak Windows 8.1 Şirket Portalı uygulaması için dağıtımı silmektir. Bunu yaptıktan sonra Windows 10 Şirket Portalı uygulaması yukarıdaki seçeneklerden herhangi biri kullanılarak dağıtılabilir.  

Uygulamayı dışarıdan yüklemeniz gerekiyorsa ve Windows 8.1 Şirket Portalı’nı Symantec Sertifikasıyla imzalamadan dağıttıysanız, yükseltmeyi tamamlamak için yukarıdaki Doğrudan Intune aracılığıyla dağıtma bölümünde sunulan adımları izleyin.

Uygulamayı dışarıdan yüklemeniz gerekiyorsa ve Windows 8.1 Şirket Portalı’nı Symantec kod imzalama sertifikası ile imzalayıp dağıttıysanız aşağıdaki bölümde sunulan adımları izleyin.  

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>İmzalı ve dışarıdan yüklenen Windows 8.1 Şirket Portalı uygulamamı Windows 10 Şirket Portalı uygulamasına yükseltmek Nasıl yaparım??

Önerilen geçiş yolumuz, dağıtım eylemini "Kaldır" olarak ayarlayarak Windows 8.1 Şirket Portalı uygulaması için mevcut dağıtımı silmektir. Bunu yaptıktan sonra Windows 10 Şirket Portalı uygulaması normal bir biçimde dağıtılabilir.  

Aksi takdirde, yükseltme yoluna uyulduğundan emin olmak için Windows 10 Şirket Portalı uygulamasının uygun şekilde güncelleştirilmesi ve imzalanması gerekir.  

Windows 10 Şirket Portalı uygulaması bu şekilde imzalanır ve dağıtılırsa, mağazada kullanıma sunulan her yeni uygulama güncelleştirmesi için bu işlemi tekrarlamanız gerekecektir. Mağaza güncelleştirildiğinde uygulama otomatik olarak güncelleştirilmez.  

Uygulamayı şu şekilde nasıl imzalayıp dağıtırsınız:

1. Microsoft Intune Windows 10 Şirket Portalı uygulama Imzalama betiği ' nden indirin [https://aka.ms/win10cpscript](https://aka.ms/win10cpscript) .  Bu betik, Windows 10 için Windows SDK’nın ana bilgisayara yüklenmiş olmasını gerektirir. Windows 10 için Windows SDK indirmek için, adresini ziyaret edin [https://go.microsoft.com/fwlink/?LinkId=619296](https://go.microsoft.com/fwlink/?LinkId=619296) .
2. Windows 10 Şirket Portalı uygulamasını yukarıda açıklandığı biçimde İş İçin Microsoft Mağazası'ndan indirin.  
3. Betik üst bilgisinde açıklanan giriş parametrelerini (ayıklanmış hali aşağıdadır) kullanıp betiği çalıştırarak Windows 10 Şirket Portalı uygulamasını imzalayın. Bağımlılıkların betiğe geçirilmesi gerekmez. Bunlar, yalnızca uygulama Intune Yönetici Konsolu’na yüklenirken gereklidir.

|       Parametre       |                                                                    Açıklama                                                                    |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| InputWin10AppxBundle  |                                             Kaynak appxbundle dosyasının bulunduğu yol.                                              |
| OutputWin10AppxBundle |                                                  İmzalı appxbundle dosyası için çıkış yolu.                                                  |
|       Win81Appx       |                          Windows 8.1 Şirket Portalı (. APPX) dosyası bulunur.                           |
|      PfxFilePath      |                                   Symantec Enterprise Mobil Kod İmza Sertifikası (.PFX) dosyasının yolu.                                    |
|      PfxPassword      |                                     Symantec Enterprise Mobil Kod İmza Sertifikası’nın parolası.                                      |
|      PublisherId      |      Kuruluşun Yayımcı Kimliği. Yoksa, Symantec Kurumsal Mobil Kod İmzalama Sertifikası’nın 'Konu' alanı kullanılır.       |
|        SdkPath        | Windows 10 için Windows SDK’sı kök klasörünün yolu. Bu bağımsız değişken isteğe bağlıdır ve varsayılan olarak ${env:ProgramFiles(x86)}\Windows Kits\10 değerindedir. |

Betik, çalışması tamamlandığında Windows 10 Şirket Portalı uygulamasının imzalı sürümünü çıktı olarak sunar. Ardından Intune aracılığıyla uygulamanın imzalı sürümünü bir LOB uygulaması olarak dağıtabilirsiniz. Şu anda dağıtılmış durumdaki sürümler, bu yeni uygulamaya yükseltilir.  
