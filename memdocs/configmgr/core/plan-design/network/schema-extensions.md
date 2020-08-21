---
title: Şema uzantıları
titleSuffix: Configuration Manager
description: Active Directory şemasını Configuration Manager destekleyecek şekilde genişletin.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 81371828078264e185dc0a1883dd383257949ef4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700104"
---
# <a name="schema-extensions-for-configuration-manager"></a>Configuration Manager için şema uzantıları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Active Directory şemasını Configuration Manager destekleyecek şekilde genişletebilirsiniz. Bu, yeni bir kapsayıcı eklemek için bir ormanın Active Directory şemasını ve Configuration Manager sitelerin, istemcilerin güvenli bir şekilde kullanabileceği Active Directory anahtar bilgilerini yayımlamak için kullandığı birkaç özniteliği düzenler. Bu bilgiler istemcilerin dağıtımını ve yapılandırmasını kolaylaştırabilir ve istemcilerin dağıtılmış içeriğe sahip sunucular gibi site kaynaklarını bulmalarına ve istemcilere farklı hizmetler sağlamasına yardımcı olabilir.  

-   Active Directory şemasını genişletmek iyi bir fikirdir, ancak gerekli değildir.  

[Active Directory şemasını genişletmeden](/sccm/core/plan-design/network/extend-the-active-directory-schema) önce Active Directory Etki alanı Hizmetleri’ni tanımanız ve [Active Directory şemasını değiştirme](/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)) işlemini kolaylıkla yapabilmeniz gerekir.  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Configuration Manager için Active Directory şemasını genişletmeyle ilgili konular  

-   Configuration Manager için Active Directory şema uzantıları 2007 Configuration Manager ve Configuration Manager 2012 ' ten farklı olanlardır. İki sürümden herhangi biri için şemayı daha önce genişlettiyseniz, şemayı yeniden genişletmenize gerek yoktur.  

-   Şemayı genişletmek orman genelinde, bir kerelik ve geri alınamaz bir eylemdir.  

-   Yalnızca şema yöneticileri grubunun üyesi olan veya şemayı değiştirmek için yeterli izinlere sahip olan bir Kullanıcı şemayı genişletebilirler.  

-   Configuration Manager Kurulum 'U çalıştırmadan önce veya sonra şemayı genişletebilseniz de, sitelerinizi ve hiyerarşi ayarlarınızı yapılandırmaya başlamadan önce şemayı genişletmek iyi bir fikir olabilir. Bunun yapılması daha sonraki yapılandırma adımlarının birçoğunu kolaylaştırabilir.  

-   Şemayı genişletdikten sonra, Active Directory genel katalog orman genelinde çoğaltılır. Bu nedenle, çoğaltma trafiği ağa bağlı diğer işlemlere olumsuz şekilde etkilenmediği zaman şemayı genişletmeyi planlayın:  

    -   Windows 2000 ormanlarında şemanın genişletilmesi tüm genel kataloğun tam eşitlenmesine neden olur.  

    -   Windows 2003 ormanlarından itibaren, yalnızca yeni eklenen öznitelikler çoğaltılır.  

**Active Directory şemasını kullanmayan cihazlar ve istemciler:**  

-   Exchange Server bağlayıcısı tarafından yönetilen mobil cihazlar  

-   Mac bilgisayarları için istemci  

-   Linux ve UNIX sunucuları için istemci  

-   Configuration Manager tarafından kaydedilen mobil cihazlar  

-   Microsoft Intune tarafından kaydedilen mobil cihazlar  

-   Mobil aygıt eski istemcileri  

-   Yalnızca Internet istemci yönetimi için yapılandırılan Windows istemcileri  

-   Configuration Manager tarafından algılanan Windows istemcileri, Internet 'te olacak şekilde  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Şemayı genişletmeden yararlanan özellikler  
**İstemci bilgisayar yüklemesi ve site ataması** -bir Windows bilgisayarı yeni bir istemci yüklediğinde, istemci, yükleme özellikleri için Active Directory Domain Services arar.  

-   **Geçici çözümler:** Şemayı genişlemeyin, bilgisayarların yüklemesi gereken yapılandırma ayrıntılarını sağlamak için aşağıdaki seçeneklerden birini kullanın:  

    -   **İstemci gönderme yüklemesini kullanın**. İstemci yükleme yöntemini kullanmadan önce tüm önkoşulların karşılandığından emin olun. Daha fazla bilgi için, [Windows bilgisayarlarına istemci dağıtma önkoşulları](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)konusunun "yükleme yöntemi bağımlılıkları" bölümüne bakın.  

    -   **İstemcileri el Ile yükleme** ve CCMSetup yükleme komut satırı özelliklerini kullanarak istemci yükleme özelliklerini sağlama. Bu durum şunları içermelidir:  

        -   Bilgisayarın, istemci yüklemesi sırasında CCMSetup komut satırında **/MP: = &lt; Yönetim noktası adı bilgisayar adı \> ** veya **/Source: &lt; istemci kaynak dosyalarının \> yolunu** kullanarak yükleme dosyalarını indirebileceği bir yönetim noktası veya kaynak yolu belirtin.  

        -   İstemcinin siteye atayabilmesi ve ardından istemci ilkesi ile site ayarlarını indirmesi için kullanacağı ilk yönetim noktalarının bir listesini belirtin. Bunu gerçekleştirmek için CCMSetup Client.msi SMSMP özelliğini kullanın.  

    -   **Yönetim noktasını DNS veya WINS'de yayınlayın** ve bu hizmet konumu yöntemini kullanmak için istemcileri yapılandırın.  

**İstemciden sunucuya iletişim Için bağlantı noktası yapılandırması** -istemci yüklediğinde, Active Directory depolanan bağlantı noktası bilgileri ile yapılandırılır. Bir site için istemci-sunucu iletişimi bağlantı noktasını daha sonra değiştirirseniz, istemci bu yeni bağlantı noktası ayarını Active Directory Domain Services alabilir.  

-   **Geçici çözümler**: Şemayı genişletmezseniz, mevcut istemcilere yeni bağlantı noktası yapılandırmaları sağlamak için aşağıdaki seçeneklerden birini kullanın:  

    -   Yeni bağlantı noktasını yapılandıran seçenekleri kullanarak **Istemcileri yeniden yükleyin** .  

    -   **İstemcilere bağlantı noktası bilgilerini güncelleştiren özel bir betik dağıtın**. İstemciler bir bağlantı noktası değişikliği nedeniyle bir siteyle iletişim kuramıyorsa, bu betiği dağıtmak için Configuration Manager kullanamazsınız. Örneğin, Grup İlkesi'ni kullanabilirsiniz.  

**İçerik dağıtım senaryoları** -bir sitede içerik oluşturup bu içeriği hiyerarşideki başka bir siteye dağıttığınızda, alan site, imzalı içerik verilerinin imzasını doğrulayabilmelidir. Bu durum, bu veriyi oluşturduğunuz kaynak sitenin ortak anahtarına erişimi gerektirir. Configuration Manager için Active Directory şemasını genişlettiğinizde, bir sitenin ortak anahtarı hiyerarşideki tüm siteler için kullanılabilir.  

-   **Geçici çözüm**: Şemayı genişletmezseniz, güvenli anahtar bilgilerini siteler arasında değiştirmek için **preinst.exe** adlı hiyerarşi bakım aracını kullanın.  

     Örneğin, bir birincil sitede içerik oluşturmayı ve bu içeriği farklı bir birincil sitenin altında ikincil bir siteye dağıtmayı planlıyorsanız, İkincil sitenin kaynak birincil sitenin ortak anahtarını almasına izin vermek için Active Directory şemasını genişletmeli ya da iki site arasında anahtarları doğrudan paylaşmak için preinst.exe kullanabilirsiniz.  

## <a name="active-directory-attributes-and-classes"></a>Active Directory öznitelikleri ve sınıfları  
Şemayı Configuration Manager uzatdığınızda, şemaya aşağıdaki sınıflar ve öznitelikler eklenir ve bu Active Directory ormanındaki tüm Configuration Manager siteleri için kullanılabilir.  

-   Öznitelikler:  

    -   CN = mS-SMS-atama-site-kodu  

    -   CN = mS-SMS-Capabilities  

    -   CN = MS-SMS-default-MP  

    -   CN = mS-SMS-Device-Management-Point  

    -   CN = mS-SMS-sağlık-State  

    -   CN = MS-SMS-MP-Address  

    -   CN = MS-SMS-MP-adı  

    -   CN = MS-SMS-Ranşlı-IP-High  

    -   CN = MS-SMS-Ranşlı-IP-düşük  

    -   CN = MS-SMS-dolaşım-sınırlar  
        on  

    -   CN = MS-SMS-site-sınırları  

    -   CN = MS-SMS-site-kodu  

    -   CN = mS-SMS-kaynak-orman  

    -   CN = mS-SMS-sürümü  

-   Sınıflar:  

    -   CN = MS-SMS-Management-Point  

    -   CN = MS-SMS-dolaşım-sınır aralığı  

    -   CN = MS-SMS-Server-Locator-Point  

    -   CN = MS-SMS-site  

> [!NOTE]
> 
>  Şema uzantıları, ürünün önceki sürümlerinden ileri taşınan ancak Configuration Manager tarafından kullanılmayan öznitelikleri ve sınıfları içerebilir. Örnek:  
> 
> 
> - Öznitelik: CN = MS-SMS-site-sınırları  
>   -   Sınıf: CN = MS-SMS-Server-Locator-Point  

ConfigMgr_ad_schema görüntüleyerek yukarıdaki listelerin güncel olduğundan emin olabilirsiniz **. LDF** dosyası Configuration Manager yükleme ortamının **\Smssetup\bin\x64** klasöründen.