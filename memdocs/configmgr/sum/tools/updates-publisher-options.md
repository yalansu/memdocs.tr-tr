---
title: Seçenekleri yapılandırma
titleSuffix: Configuration Manager
description: System Center Updates Publisher kullanma seçeneklerini yapılandırın
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717730"
---
# <a name="configure-options-for-updates-publisher"></a>Updates Publisher seçeneklerini yapılandırma

*Uygulama hedefi: System Center Updates Publisher*

Updates Publisher 'ın çalışmasını etkileyen seçenekleri ve ilgili ayarları gözden geçirin ve yapılandırın.

Updates Publisher seçeneklerine erişmek için konsolun sol üst köşesinde, **Updates Publisher** **özellikleri** sekmesine tıklayın ve ardından **Seçenekler**' i seçin.

![Seçenekler](media/properties1.png)   


Seçenekler aşağıdakilere ayrılmıştır:

-   Güncelleştirme Sunucusu
-   ConfigMgr sunucusu
-   Proxy ayarları
-   Güvenilir Yayımcılar
-   Gelişmiş
-   Güncelleştirmeler
-   Günlüğe Kaydetme

## <a name="update-server"></a>Güncelleştirme Sunucusu
Güncelleştirmeleri [yayımlamadan](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace)önce, Updates Publisher 'ı Windows Server Update SERVICES (WSUS) gibi güncelleştirme sunucusu ile çalışacak şekilde yapılandırmanız gerekir. Bu, sunucuyu belirtmeyi, konsolundan uzakta olduğunda bu sunucuya bağlanma yöntemlerini ve yayımladığınız güncelleştirmeleri dijital olarak imzalamak için kullanılacak bir sertifikayı içerir.

- **Bir güncelleştirme sunucusu yapılandırın**. Bir güncelleştirme sunucusu yapılandırdığınızda, tüm alt sitelerin yayımladığınız güncelleştirmelere erişimi olması için Configuration Manager hiyerarşinizdeki en üst düzey WSUS sunucusunu (güncelleştirme sunucusu) seçin.

  Güncelleştirme sunucunuz, Updates Publisher sunucusundan uzak ise, sunucunun tam etki alanı adını (FQDN) belirtin ve SSL ile bağlanacaksınız. SSL ile bağlandığınızda, varsayılan bağlantı noktası 8530 ' den 8531 ' e dönüşür. Ayarladığınız bağlantı noktasının, güncelleştirme sunucunuz tarafından kullanılan ile eşleştiğinden emin olun.

  > [!TIP]  
  > Bir güncelleştirme sunucusu yapılandırmazsanız, yazılım güncelleştirmelerini yazmak için Updates Publisher 'ı kullanmaya devam edebilirsiniz.

- **İmzalama sertifikasını yapılandırın**. İmzalama sertifikasını yapılandırmadan önce bir güncelleştirme sunucusuna yapılandırmanız ve başarıyla bağlanmanız gerekir.

  Updates Publisher, güncelleştirme sunucusunda yayınlanan yazılım güncelleştirmelerini imzalamak için imzalama sertifikasını kullanır. Güncelleştirme sunucusunun veya Updates Publisher çalıştıran bilgisayarın sertifika deposunda dijital sertifika yoksa yayımlama başarısız olur.

  Sertifikayı sertifika deposuna ekleme hakkında daha fazla bilgi için bkz. [Updates Publisher Için sertifikalar ve güvenlik](updates-publisher-security.md).

  Güncelleştirme sunucusu için otomatik olarak bir dijital sertifika algılanmazsa, aşağıdakilerden birini seçin:

  -   **Araştır**: yalnızca, güncelleştirme sunucusu konsolunu çalıştırdığınız sunucuda yüklü olduğunda kullanılabilir. Bir sertifika seçtikten sonra, bu sertifikayı güncelleştirme sunucusundaki WSUS sertifika deposuna eklemek için **Oluştur** ' u seçmeniz gerekir. Bu yöntem tarafından seçtiğiniz sertifikalar için **. pfx** dosya parolasını girmeniz gerekir.

  -   **Oluşturma:** Yeni bir sertifika oluşturmak için bu seçeneği kullanın. Bu ayrıca sertifikayı güncelleştirme sunucusundaki WSUS sertifika deposuna ekler.

  **Kendi imzalama sertifikanızı oluşturursanız**, aşağıdakileri yapılandırın:

  -   **Özel anahtarın verilmesine Izin ver** seçeneğini etkinleştirin.

  -   **Anahtar kullanımını** dijital imzaya ayarlayın.

  -   **Minimum anahtar boyutunu** 2048 bite eşit veya daha büyük bir değere ayarlayın.

  WSUS sertifika deposundan bir sertifikayı kaldırmak için **Kaldır** seçeneğini kullanın. Bu seçenek, güncelleştirme sunucusu, kullandığınız güncelleştirmeler yayımcısı konsolunda yerel olduğunda veya bir uzak güncelleştirme sunucusuna bağlanmak için **SSL** kullandığınızda kullanılabilir.

## <a name="configmgr-server"></a>ConfigMgr sunucusu
Updates Publisher ile Configuration Manager kullandığınızda bu seçenekleri kullanın.

-   **Configuration Manager sunucusunu belirtin:** Configuration Manager desteğini etkinleştirdikten sonra, Configuration Manager hiyerarşinizden en üst katman site sunucusunun konumunu belirtin. Bu sunucu, yayımcı yüklemesi ' nden uzakta ise, site sunucusunun FQDN 'sini belirtin. Site sunucusuna bağlanabildiğinizden emin olmak için **Bağlantıyı Sına** ' yı seçin.

-   **Eşikleri Yapılandır:** Eşikler, güncelleştirmeleri otomatik bir yayın türüyle yayımladığınızda kullanılır. Eşik değerleri, yalnızca meta veriler yerine bir güncelleştirme için tam içeriğin ne zaman yayımlandığını belirlemesine yardımcı olur. Daha fazla yayın türü hakkında daha fazla bilgi edinmek için bkz. [bir yayına güncelleştirme atama](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)

    Aşağıdaki eşiklerden birini veya her ikisini de kullanabilirsiniz:

    -   **İstenen istemci sayısı eşiği:** Bu, güncelleştirmeler yayımcısının Bu güncelleştirme için tam içerik kümesini otomatik olarak yayımlayabilmesi için kaç istemcinin bir güncelleştirme istemesi gerektiğini tanımlar. Belirtilen istemci sayısı güncelleştirmeyi isteene kadar, yalnızca güncelleştirmeler meta verileri yayımlanır.

    -   **Paket kaynak boyutu eşiği (MB):** Bu, belirttiğiniz boyutu aşan güncelleştirmelerin otomatik olarak yayımlanmasını önler. Güncelleştirme boyutu bu değeri aşarsa yalnızca meta veriler yayımlanır. Belirtilen boyuttan daha küçük olan güncelleştirmeler, tam içeriklerinin yayımlanmasını sağlayabilir.

## <a name="proxy-settings"></a>Proxy ayarları
Updates Publisher, Internet 'ten yazılım kataloğu içeri aktardığınızda veya güncelleştirmeleri Internet 'Te yayımladığınızda proxy ayarlarını kullanır.

-   Bir proxy sunucusunun FQDN 'sini veya IP adresini belirtin. IPv4 ve IPv6 desteklenir.

-   Proxy sunucusu kullanıcıların kimliğini Internet erişimi için doğruladığında, Windows adını belirtmeniz gerekir. Evrensel bir asıl ilke adı (UPN) desteklenmez.

## <a name="trusted-publishers"></a>Güvenilir Yayımcılar
Bir güncelleştirme kataloğunu içeri aktardığınızda, bu kataloğun kaynağı (sertifikaya göre), güvenilen bir yayımcı olarak eklenir. Benzer şekilde, bir güncelleştirmeyi yayımladığınızda, güncelleştirmeler sertifikasının kaynağı güvenilen bir yayımcı olarak eklenir.

Her yayımcının sertifika ayrıntılarını görüntüleyebilir ve Güvenilen Yayımcılar listesinden bir yayımcıyı kaldırabilirsiniz.

Güvenilir olmayan yayımcıların içeriği, istemci güncelleştirmeleri taradığında istemci bilgisayarlarına zarar verebilir. Yalnızca güvendiğiniz yayımcıların içeriğini kabul etmelisiniz.

## <a name="advanced"></a>Gelişmiş
Gelişmiş seçenekler şunları içerir:

-   **Depo konumu:** **Scupdb. sdf**veritabanı dosyasının konumunu görüntüleyin ve değiştirin. Bu dosya Updates Publisher deposudur.

-   **Zaman damgası:** Etkinleştirildiğinde, imzaladığınız güncelleştirmelerin imzalandığı zamana göre tanımladığı bir zaman damgası eklenir. Bir sertifika geçerli olduğunda imzalanmış bir güncelleştirme, imzalama sertifikasının süresi dolduktan sonra kullanılabilir. Varsayılan olarak, yazılım güncelleştirmeleri, imza sertifikalarının süresi dolduktan sonra dağıtılamaz.

-   **Abone olunan kataloglarda güncelleştirmeleri denetle:** Her güncelleştirme yayımcısı başlatıldığında, abone olduğunuz kataloglara yönelik güncelleştirmeleri otomatik olarak denetleyebilir. Bir katalog güncelleştirmesi bulunduğunda, Ayrıntılar **çalışma alanının** **genel bakış** penceresinde Ayrıntılar, **son uyarılar** olarak sağlanır.

-   **Sertifika iptali:** Sertifika iptal denetimlerini etkinleştirmek için bu seçeneği belirleyin.

-   **Yerel kaynak yayımlama:** Updates Publisher, bu güncelleştirmeyi Internet 'ten indirmeden önce yayımlamakta olduğunuz bir güncelleştirmenin yerel bir kopyasını kullanabilir. Konum, Updates Publisher çalıştıran bilgisayardaki bir klasör olmalıdır. Varsayılan olarak, bu konum My **Documents\LocalSourcePublishing.** Daha önce bir veya daha fazla güncelleştirme indirdiyseniz veya dağıtmak istediğiniz bir güncelleştirmede değişiklik yaptıysanız bunu kullanın.

-   **Yazılım güncelleştirmeleri Temizleme Sihirbazı:** Güncelleştirmeler Temizleme Sihirbazı 'nı başlatın. Sihirbaz güncelleştirme sunucusunda olan ancak Updates Publisher deposunda olmayan güncelleştirmeler için zaman aşımına uğrar. Daha fazla ayrıntı için bkz. [başvurulmayan güncelleştirmeler sona erme tarihi](#expire-unreferenced-software-updates) .

## <a name="updates"></a>Güncelleştirmeler
 Updates Publisher her açıldığında yeni güncelleştirmeleri otomatik olarak denetleyebilir. Ayrıca, Updates Publisher 'ın önizleme derlemelerini almayı da tercih edebilirsiniz.

Güncelleştirmeleri el ile denetlemek için, güncelleştirmeler Publisher konsolunda ![Özellikler ' e tıklayın.](media/properties2.png)  
**Updates Publisher özelliklerini**açın ve ardından **güncelleştirme için denetle**' yi seçin.

Updates Publisher yeni bir güncelleştirme bulduktan sonra, **güncelleştirme kullanılabilir** penceresi görüntülenir ve daha sonra yüklemeyi tercih edebilirsiniz. Güncelleştirmeyi yüklememeyi seçerseniz, konsolu bir sonraki açışınızda sunulur.

## <a name="logging"></a>Günlüğe Kaydetme
Updates Publisher, Updates Publisher ile ilgili temel bilgileri **%windir%\temp\updatespublisher.log dizinine**kaydeder.

Günlüğü görüntülemek için Notepad veya **CMTrace** kullanın. CMTrace, Configuration Manager günlük dosyası aracıdır ve Configuration Manager kaynak ortamının **\Smssetup\tools** klasöründe bulunabilir.

Günlüğün boyutunu ve ayrıntı düzeyini değiştirebilirsiniz.

Veritabanı günlüğünü etkinleştirdiğinizde, Updates Publisher veritabanında çalıştırılan sorgular hakkında bilgiler dahil edilir. Veritabanı günlüğünün kullanımı, Updates Publisher bilgisayarının performansının düşmesine yol açabilir.

Günlük dosyasını görüntülemek için ![konsolunda Özellikler](media/properties2.png) ' e tıklayarak **Updates Publisher özelliklerini**açın ve **günlük dosyasını görüntüle**' yi seçin.

## <a name="expire-unreferenced-software-updates"></a>Başvurulmayan yazılım güncelleştirmelerinin süreleri doluyor
**Yazılım güncelleştirme Temizleme Sihirbazı 'nı** çalıştırarak güncelleştirme sunucunuzdaki güncelleştirmelerin süresini sona erdirmek Için Updates Publisher deposunda ' i kullanabilirsiniz. Bu, daha sonra bu güncelleştirmeleri gelecekteki dağıtımlardan kaldıran Configuration Manager bildirir.

Bir güncelleştirmenin süresi dolmak üzere olan işlem tersine çevrilemez. Yalnızca seçtiğiniz yazılım güncelleştirmelerinin kuruluşunuz tarafından artık gerekli olmadığından eminseniz bu görevi gerçekleştirin.

### <a name="to-remove-expired-software-updates"></a>Süre dolduğunda, yazılım güncelleştirmelerini kaldırmak için
1.  Updates Publisher ![konsolunda](media/properties2.png) Özellikler ' e tıklayarak **Updates Publisher özelliklerini**açın ve **Seçenekler**' i seçin.

2.  **Gelişmiş**' i seçin ve ardından **yazılım güncelleştirme Temizleme Sihirbazı** altında **Başlat**' ı seçin.

3.  Sona ermek istediğiniz yazılım güncelleştirmelerini seçin ve ardından **İleri**' yi seçin.

4.  Seçimlerinizi inceledikten sonra, seçimleri kabul etmek ve bu güncelleştirmelerin süresini sona erdirmek için **İleri** ' yi seçin.

5.  Sihirbaz tamamlandıktan sonra Sihirbazı tamamladıktan sonra **Kapat** ' ı seçin.
