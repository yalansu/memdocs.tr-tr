---
title: Yayımlama ve Active Directory şeması
titleSuffix: Configuration Manager
description: İstemcileri dağıtma ve yapılandırma işlemini basitleştirmek için Configuration Manager Active Directory şemasını genişletin.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718766"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Site yayımlama için Active Directory hazırlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için Active Directory şemasını genişlettiğinizde, Configuration Manager siteleri tarafından istemcilerin kolayca erişebileceği güvenli bir konumda anahtar bilgileri yayımlamak için kullanılan Active Directory yeni yapıları tanıtmanız gerekir.  

Şirket içi istemcileri yönetirken genişletilmiş bir Active Directory şeması Configuration Manager kullanmak iyi bir fikirdir. Genişletilmiş bir şema, istemcileri dağıtma ve ayarlama sürecini basitleştirebilir. Genişletilmiş bir şema ayrıca istemcilerin içerik sunucuları gibi kaynakları ve farklı Configuration Manager site sistem rollerinin sağladığı ek hizmetleri verimli bir şekilde bulmasını sağlar.  

-   Configuration Manager dağıtımı için hangi genişletilmiş şemanın sağladığı hakkında bilgi sahibi değilseniz, bu kararı vermenize yardımcı olması için [Configuration Manager şema uzantıları](../../../core/plan-design/network/schema-extensions.md) hakkında bilgi edinebilirsiniz.  

-   Genişletilmiş bir şema kullanmıyorsanız Hizmetleri ve site sistemi sunucularını bulmak için DNS ve WINS gibi diğer yöntemleri ayarlayabilirsiniz. Bu hizmet yöntemleri ek yapılandırmalar gerektirir ve istemciler tarafından tercih edilen hizmet bulma yöntemi değildir. Daha fazla bilgi edinmek için bkz. [İstemcilerin site kaynaklarını ve hizmetleri Configuration Manager nasıl bulduklarını anlama](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md),  

-   Active Directory şemanız Configuration Manager 2007 veya System Center 2012 Configuration Manager için genişletilmişse, daha fazlasını yapmanıza gerek kalmaz. Şema uzantıları değiştirilmez ve zaten yerinde olacaktır.  

Şemayı genişletmek, her orman için tek seferlik bir eylemdir. Öğesini genişletmek ve ardından genişletilmiş Active Directory şemasını kullanmak için şu adımları izleyin:  

## <a name="step-1-extend-the-schema"></a>1. Adım. Şemayı genişletme  
Şemayı Configuration Manager genişletmek için:  

-   Şema yöneticileri güvenlik grubunun üyesi olan bir hesap kullanın.  

-   Şema yöneticisi etki alanı denetleyicisinde oturum açmanız.  

-   **Extadsch. exe** aracını çalıştırın veya **ConfigMgr_ad_schema. ldf** dosyasıyla LDIFDE komut satırı yardımcı programını kullanın. Araç ve dosya, Configuration Manager yükleme medyasında **Smssetup\bin\x64** klasöründedir.  

#### <a name="option-a-use-extadschexe"></a>Seçenek A: Extadsch.exe kullanma  

1.  Active Directory şemasına yeni sınıflar ve öznitelikler eklemek için **extadsch.exe** dosyasını çalıştırın.  

    > [!TIP]  
    >  Çalışırken geri bildirimi görüntülemek için bir komut satırından bu aracı çalıştırın.  

2.  Sistem sürücüsünün kökündeki extadsch. log ' i inceleyerek şema uzantısının başarılı olduğunu doğrulayın.  

#### <a name="option-b-use-the-ldif-file"></a>Seçenek B: LDIF dosyasını kullanma  

1.  Genişletmek istediğiniz Active Directory kök etki alanını tanımlamak için **ConfigMgr_ad_schema. ldf** dosyasını düzenleyin:  

    -   Dosyadaki **DC = x**metninin tüm örneklerini, genişletilecek etki alanının tam adıyla değiştirin.  

    -   Örneğin, genişletilecek etki alanının tam adı widgets.microsoft.com olarak adlandırılmışsa, dosyadaki tüm DC = x örneklerini **DC = pencere öğeleri, DC = Microsoft, DC = com**olarak değiştirin.  

2.  **ConfigMgr_ad_schema. ldf** dosyasının içeriğini Active Directory Domain Services aktarmak için LDIFDE komut satırı yardımcı programını kullanın:  

    -   Örneğin, aşağıdaki komut satırı, şema uzantılarını Active Directory Domain Services içeri aktarır, ayrıntılı günlük özelliğini açar ve içeri aktarma işlemi sırasında bir günlük dosyası oluşturur: **ldifde-i-f ConfigMgr_ad_schema. ldf-v-j &lt;konum günlük dosyasını\>depolayacak**.  

3.  Şema uzantısının başarılı olduğunu doğrulamak için, önceki adımda kullanılan komut satırı tarafından oluşturulan bir günlük dosyasını gözden geçirin.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>2. Adım  Sistem Yönetimi kapsayıcısını oluşturma ve kapsayıcıya site izinleri verme  
 Şemayı genişletdikten sonra, Active Directory Domain Services (AD DS) içinde **sistem yönetimi** adlı bir kapsayıcı oluşturmanız gerekir:  

-   Bu kapsayıcıyı, Active Directory veri yayımlayacak birincil veya ikincil siteye sahip her bir etki alanında bir kez oluşturursunuz.  

-   Her kapsayıcı için, bu etki alanına veri yayımlayacak her birincil ve ikincil site sunucusunun bilgisayar hesabına izinler verirsiniz. Her **Hesap, gelişmiş**Izinle kapsayıcıya **tam denetim** gerektirir, **Bu nesneye ve tüm alt nesnelere**eşittir.  

#### <a name="to-add-the-container"></a>Kapsayıcı eklemek için  

1.  Active Directory Etki Alanı Hizmetleri'ndeki **Sistem** kapsayıcısında **Tüm Bağımlı Nesneleri Oluştur** iznine sahip bir hesap kullanın.  

2.  **ADSI Edit** (Adsiedit. msc) öğesini çalıştırın ve site sunucusunun etki alanına bağlanın.  

3.  Kapsayıcıyı oluşturun:  

    -   **Etki alanı** &lt;bilgisayar tam etki alanı adı\>' nı &lt;genişletin,\>ayırt edici ad ' ı genişletin, **CN = System**' i sağ tıklatın ve ardından **nesne** **' yi**seçin.  

    -   **Nesne oluştur** Iletişim kutusunda **kapsayıcı**' yı seçin ve ardından **İleri**' yi seçin.  

    -   **Değer** kutusuna **sistem yönetimi**' ni girin ve ardından **İleri**' yi seçin.  

4.  İzinler atayın:  

    > [!NOTE]  
    >  İsterseniz, kapsayıcıya izinler eklemek için Active Directory Kullanıcılar ve Bilgisayarlar yönetim aracı (dsa.msc) gibi başka araçlar da kullanabilirsiniz.  

    -   **CN = System Management**' a sağ tıkladıktan sonra **Özellikler**' i seçin.  

    -   **Güvenlik** sekmesini seçin, **Ekle**' yi seçin ve ardından site sunucusu bilgisayar hesabını **tam denetim** izniyle ekleyin.  

    -   **Gelişmiş**' i seçin, site sunucusunun bilgisayar hesabını seçin ve ardından **Düzenle**' yi seçin.  

    -   **Uygula** listesinde, **Bu nesne ve tüm alt nesneler**' i seçin.  

5.  Konsolu kapatmak ve yapılandırmayı kaydetmek için **Tamam** ' ı seçin.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>3. Adım Active Directory Domain Services yayımlanacak siteleri ayarlama  
 Kapsayıcı kurulduktan sonra, izinler verilir ve bir Configuration Manager birincil sitesi yüklediniz, bu siteyi Active Directory veri yayımlayacak şekilde ayarlayabilirsiniz.  

 Yayımlama hakkında daha fazla bilgi için bkz. [Configuration Manager site verilerini yayımlama](../../../core/servers/deploy/configure/publish-site-data.md).  
