---
title: İçerik dağıtma
titleSuffix: Configuration Manager
description: Configuration Manager için dağıtım noktalarını yükledikten sonra, bunlara içerik dağıtmaya nasıl başlayabileceğiniz aşağıda verilmiştir.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7478eff1a14eeffd4d12b1539df7c5573c6a7cb6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722980"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Configuration Manager için içerik dağıtma ve yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için dağıtım noktalarını yükledikten sonra, bunlara içerik dağıtmaya başlayabilirsiniz. Genellikle içerik, ağ genelindeki dağıtım noktalarına aktarılır, ancak dağıtım noktalarına içerik almak için diğer seçenekler vardır. İçerik bir dağıtım noktasına aktarımdıktan sonra, bu içeriği dağıtım noktalarında güncelleştirebilir, yeniden dağıtabilir, kaldırabilir ve doğrulayabilirsiniz.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a>İçeriği dağıt  
Genellikle, içeriği dağıtım noktalarına dağıtarak istemci bilgisayarlar için kullanılabilir hale gelir. (Bunun özel durumu, belirli bir dağıtım için isteğe bağlı içerik dağıtımını kullandığınızda olur.)  İçeriği dağıttığınızda, Configuration Manager içerik dosyalarını bir pakette depolar ve ardından paketi dağıtım noktasına dağıtır. Dağıtabileceğiniz içerik türleri şunları içerir:  

- Uygulama dağıtım türleri  

- Paketler  

- Dağıtım paketleri  

- Sürücü paketleri  

- İşletim sistemi görüntüleri  

- İşletim sistemi yükleyicileri  

- Önyükleme görüntüleri  

- Görev dizileri  

Uygulama dağıtım türü veya dağıtım paketi gibi kaynak dosyaları içeren bir paket oluşturduğunuzda, paketin oluşturulduğu site, paket içerik kaynağı için site sahibi olur. Configuration Manager, kaynak dosyaları, nesne için belirttiğiniz kaynak dosya yolundan, paket içerik kaynağına sahip site sunucusundaki içerik kitaplığına kopyalar.  Daha sonra, Configuration Manager bilgileri ek sitelere çoğaltır. (Bunun hakkında daha fazla bilgi için bkz. [içerik kitaplığı](../../../../core/plan-design/hierarchy/the-content-library.md) .)  

İçeriği dağıtım noktalarına dağıtmak için aşağıdaki yordamı kullanın.  

#### <a name="to-distribute-content-on-distribution-points"></a>İçeriği dağıtım noktalarına dağıtmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, dağıtmak istediğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi** > **uygulamaları**' nı genişletin ve ardından dağıtmak istediğiniz uygulamaları seçin.  

    - **Paketler**: **uygulama yönetim** >  **paketleri**' ni genişletin ve ardından dağıtmak istediğiniz paketleri seçin.  

    - **Dağıtım paketleri**: **yazılım güncelleştirmeleri** >  **dağıtım paketleri**' ni genişletin ve ardından dağıtmak istediğiniz dağıtım paketlerini seçin.  

    - **Sürücü paketleri**: **işletim sistemleri** >  **sürücü paketleri**' ni genişletin ve ardından dağıtmak istediğiniz sürücü paketlerini seçin.  

    - **İşletim sistemi görüntüleri**: **işletim sistemleri** >  **işletim sistemi görüntüleri**' ni genişletin ve ardından dağıtmak istediğiniz işletim sistemi görüntülerini seçin.  

    - **İşletim sistemi yükleyicileri**: **işletim sistemleri** > **işletim sistemi yükleyicileri**' ni genişletin ve ardından dağıtmak istediğiniz işletim sistemi yükleyicilerini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri** >  **önyükleme görüntüleri**' ni genişletin ve ardından dağıtmak istediğiniz önyükleme görüntülerini seçin.  

    - **Görev dizileri**: **işletim sistemleri** >  **görev dizileri**' ni genişletin ve ardından dağıtmak istediğiniz görev sırasını seçin. Görev dizileri içerik içermese de, dağıtılan ilişkili içerik bağımlılıkları vardır.  

      > [!NOTE]  
      > Görev sırasını değiştirirseniz, içeriği yeniden dağıtmanız gerekir.  

3.  **Giriş** sekmesinde, **Dağıtım** grubunda, **İçeriği Dağıt**'ı tıklatın. Içerik Dağıtma Sihirbazı açılır.  

4.  **Genel** sayfasında, listelenen içeriğin dağıtmak istediğiniz içerik olduğunu doğrulayın, Configuration Manager seçili içerikle ilişkili içerik bağımlılıklarını algılamasını isteyip istemediğinizi seçin ve bağımlılıkları dağıtıma ekleyin ve ardından **İleri**' ye tıklayın.  

    > [!NOTE]  
    > **İlişkili içerik bağımlılıklarını Algıla** seçeneğini yapılandırma ve yalnızca uygulama içerik türü için bu dağıtım ayarına ekleme seçeneğiniz vardır. Configuration Manager, görev dizileri için bu ayarı otomatik olarak yapılandırır ve değiştirilemez.  

5.  **İçerik** sekmesinde, görüntüleniyorsa, listelenen içeriğin dağıtmak istediğiniz içerik olduğunu doğrulayın ve ardından **İleri**' ye tıklayın.  

    > [!NOTE]  
    > **İçerik** sayfası, sihirbazın **genel** sayfasında **ilişkili içerik bağımlılıklarını Algıla ve bu dağıtıma Ekle** ayarı seçildiğinde görüntülenir.  

6.  **Içerik hedefi** sayfasında, **Ekle**' ye tıklayın, aşağıdakilerden birini seçin ve ardından ilişkili adımı izleyin:  

    - **Koleksiyonlar**: **Kullanıcı koleksiyonları** veya **Cihaz Koleksiyonları**' nı seçin, bir veya daha fazla dağıtım noktası grubu Ile ilişkili koleksiyona tıklayın ve ardından **Tamam**' a tıklayın.  

        > [!NOTE]  
        > Yalnızca bir dağıtım noktası grubuyla ilişkili koleksiyonlar görüntülenir. Koleksiyonları dağıtım noktası gruplarıyla ilişkilendirme hakkında daha fazla bilgi için, [Configuration Manager için dağıtım noktalarını yükleyip yapılandırma](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) konusunun [dağıtım noktası gruplarını yönetme](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) bölümüne bakın.  

    - **Dağıtım noktası**: var olan bir dağıtım noktası seçin ve ardından **Tamam**' a tıklayın. İçeriği daha önce almış olan dağıtım noktaları görüntülenmez.  

    - **Dağıtım noktası grubu**: var olan bir dağıtım noktası grubunu seçin ve ardından **Tamam**' a tıklayın. İçeriği daha önce almış olan dağıtım noktası grupları gösterilmez.  

    İçerik hedefleri eklemeyi bitirdiğinizde **İleri**' ye tıklayın.  

7.  **Özet** sayfasında, devam etmeden önce dağıtımın ayarlarını gözden geçirin. İçeriği seçili hedeflere dağıtmak için **İleri**' ye tıklayın.  

8.  **Ilerleme durumu** sayfası dağıtımın ilerlemesini görüntüler.  

9. **Onay** sayfası, içeriğin noktalara başarıyla atandığını görüntüler. İçerik dağıtımını izlemek için, [Configuration Manager ile dağıttığınız Içeriği izleme](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)bölümüne bakın.  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a>Önceden hazırlanan içerik kullan  
Uygulamalar ve paket türleri için içerik dosyalarını önceden hazırlayabilirsiniz:  

- Configuration Manager konsolunda, ihtiyacınız olan içeriği seçin ve ardından, seçtiğiniz içerik için dosyaları ve ilişkili meta verileri içeren sıkıştırılmış, önceden hazırlanmış bir içerik dosyası oluşturmak üzere **önceden hazırlanan Içerik dosyası oluşturma Sihirbazı 'nı** kullanın.  

- Daha sonra içeriği bir site sunucusunda, ikincil sitede veya dağıtım noktasında el ile içeri aktarabilirsiniz.  

- Önceden hazırlanan içerik dosyasını bir site sunucusuna aktardığınızda, içerik dosyaları site sunucusundaki içerik kitaplığına eklenir ve ardından site sunucusu veritabanına kaydedilir.  

- Önceden hazırlanan içerik dosyasını bir dağıtım noktasına aktardığınızda, içerik dosyaları dağıtım noktasındaki içerik kitaplığına eklenir ve site sunucusuna, siteye içeriğin dağıtım noktasında kullanılabilir olduğunu bildiren bir durum iletisi gönderilir.  

**Önceden hazırlanan içerik için sınırlamalar ve önemli noktalar:**  

- **Dağıtım noktası site sunucusunda bulunduğunda**, önceden hazırlanan içerik için dağıtım noktasını etkinleştirmeyin. Bunun yerine, [site sunucusundaki bir dağıtım noktasındaki içeriği önceden hazırlama](#bkmk_dpsiteserver)bölümündeki yordamı kullanın.  

- **Dağıtım noktası bir çekme dağıtım noktası olarak yapılandırıldığında**, önceden hazırlanan içerik için dağıtım noktasını etkinleştirmeyin. Dağıtım noktası için önceden hazırlanan içerik yapılandırması, istek temelli dağıtım noktası yapılandırmasını geçersiz kılar. Önceden hazırlanan içerik için yapılandırılan bir çekme dağıtım noktası, kaynak dağıtım noktasından içerik çekmez ve site sunucusundan içerik almaz.  

- İçeriği **dağıtım noktasına önceden hazırlamak için önce dağıtım noktasında içerik kitaplığının oluşturulması gerekir**. İçeriği dağıtım noktasına önceden oluşturmadan önce ağ üzerinden en az bir kez içerik dağıtın.  

- **Uzun paket kaynak yolu olan bir paket için içerik önceden hazırladıktan** sonra (örneğin, 140 karakterden fazla), içerik Ayıkla komut satırı aracı o paketin içeriğini içerik kitaplığına başarıyla ayıklayamayabilir.  

İçerik dosyalarının önceden hazırlanması hakkında daha fazla bilgi için bkz. [içerik yönetimi için ağ bant genişliğini yönetme](../../../plan-design/hierarchy/manage-network-bandwidth.md) konusunda *önceden hazırlanan içerik* .  

İçeriği önceden hazırlamak için aşağıdaki bölümleri kullanın.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a>1. Adım: önceden hazırlanan Içerik dosyası oluşturma  
Configuration Manager konsolunda seçtiğiniz içerik için dosyaları ve ilişkili meta verileri içeren sıkıştırılmış, önceden hazırlanmış bir içerik dosyası oluşturabilirsiniz. Önceden hazırlanan bir içerik dosyası oluşturmak için aşağıdaki yordamı kullanın.  

##### <a name="to-create-a-prestaged-content-file"></a>Önceden hazırlanan içerik dosyası oluşturmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, önceden hazırlamak istediğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi**' ni genişletin, **uygulamalar**' a tıklayın ve ardından önceden hazırlamak istediğiniz uygulamaları seçin.  

    - **Paketler**: **uygulama yönetimi**' ni genişletin, **paketler**' e tıklayın ve ardından önceden hazırlamak istediğiniz paketleri seçin.  

    - **Sürücü paketleri**: **işletim sistemleri**' ni genişletin, **sürücü paketleri**' ne tıklayın ve ardından önceden hazırlamak istediğiniz sürücü paketlerini seçin.  

    - **Işletim sistemi görüntüleri**: **işletim sistemleri**' ni genişletin, **işletim sistemi görüntüleri**' ni tıklatın ve ardından önceden hazırlamak istediğiniz işletim sistemi görüntülerini seçin.  

    - **Işletim sistemi yükleyicileri**: **işletim sistemleri**' ni genişletin, **işletim sistemi yükleyicileri**' ni tıklatın ve ardından önceden hazırlamak istediğiniz işletim sistemi yükleyicilerini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri**' ni genişletin, **önyükleme yansımaları**' nı tıklatın ve ardından önceden hazırlamak istediğiniz önyükleme görüntülerini seçin.  

    - **Görev dizileri**: **işletim sistemleri**' ni genişletin, **görev dizileri**' ni tıklatın ve ardından önceden hazırlamak istediğiniz görev sırasını seçin.  

3.  **Giriş** sekmesinde, **dağıtım** grubunda, **önceden hazırlanan içerik dosyası oluştur**' a tıklayın. Önceden hazırlanan Içerik dosyası oluşturma Sihirbazı açılır.  

    > [!NOTE]  
    > **Uygulamalar için:** **Giriş** sekmesinde, **uygulama** grubunda, **önceden hazırlanan içerik dosyası oluştur**' a tıklayın.  
    >   
    > **Paketler için:** **Giriş** sekmesinde, &lt; *PackageName*> grubunda, **önceden hazırlanan içerik dosyası oluştur**' a tıklayın.  

4.  **Genel** sayfasında, **Araştır**' a tıklayın, önceden hazırlanan içerik dosyasının konumunu seçin, dosya için bir ad belirtin ve ardından **Kaydet**' e tıklayın. Bu önceden hazırlanan içerik dosyasını birincil site sunucularında, ikincil site sunucularında veya dağıtım noktalarında kullanarak içeriği ve meta verileri içeri aktarabilirsiniz.  

5.  Uygulamalar için **tüm bağımlılıkları dışarı aktar** ' ı seçerek Configuration Manager algılamasını ve uygulamayla ilişkili bağımlılıkları önceden hazırlanan içerik dosyasına ekleyin. Bu ayar varsayılan olarak seçilidir.  

6.  **Yönetici açıklamaları**' nda, önceden hazırlanan içerik dosyası hakkında isteğe bağlı açıklamalar girin ve ardından **İleri**' ye tıklayın.  

7.  **İçerik** sayfasında, listelenen içeriğin önceden hazırlanan içerik dosyasına eklemek istediğiniz içerik olduğunu doğrulayın ve ardından **İleri**' ye tıklayın.  

8.  **Içerik konumları** sayfasında, önceden hazırlanan içerik dosyası için içerik dosyalarının alınacağı dağıtım noktalarını belirtin. İçeriği almak için birden fazla dağıtım noktası seçebilirsiniz. Dağıtım noktaları, Içerik konumları bölümünde listelenir. **İçerik** sütunu her dağıtım noktasında seçilen paketlerin veya uygulamalardan kaç tane kullanılabilir olduğunu gösterir. Configuration Manager, seçilen içeriği almak için listedeki ilk dağıtım noktasıyla başlar ve daha sonra önceden hazırlanan içerik dosyası için gerekli kalan içeriği almak için listeyi aşağı kaydırır. Dağıtım noktalarının öncelik sırasını değiştirmek için **Yukarı taşı** veya **aşağı taşı** ' ya tıklayın. Listedeki dağıtım noktaları seçili içeriğin tümünü içermiyorsa, içerik içeren listeye dağıtım noktaları eklemeniz veya sihirbazdan çıkmanız, içeriği en az bir dağıtım noktasına dağıtmanız ve ardından Sihirbazı yeniden başlatmanız gerekir.  

9. **Özet** sayfasında, ayrıntıları onaylayın. Önceki sayfalara dönüp değişiklik yapabilirsiniz. Önceden hazırlanan içerik dosyasını oluşturmak için **İleri** ' ye tıklayın.  

10. **İlerleme** sayfasında, önceden hazırlanan içerik dosyasına eklenmekte olan içerik görüntülenir.  

11. **Tamamlama** sayfasında, önceden hazırlanan içerik dosyasının başarıyla oluşturulduğunu doğrulayın ve ardından **Kapat**' ı tıklatın.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a>2. Adım: Içeriği dağıtım noktalarına atama  
 İçerik dosyasını önceden hazırladıktan sonra, içeriği dağıtım noktalarına atayın.  

> [!NOTE]  
> Bir site sunucusundaki içerik kitaplığını kurtarmak için önceden hazırlanmış bir içerik dosyası kullandığınızda ve içerik dosyalarını bir dağıtım noktasında önceden hazırlamak zorunda değilseniz, bu yordamı atlayabilirsiniz.  

 Önceden hazırlanan içerik dosyasındaki içeriği dağıtım noktalarına atamak için aşağıdaki yordamı kullanın.  

> [!IMPORTANT]  
> Önceden hazırlamak istediğiniz dağıtım noktalarının önceden hazırlanmış dağıtım noktaları olarak yapılandırıldığını veya içeriğin ağ kullanılarak dağıtım noktalarına dağıtıldığını doğrulayın.  

##### <a name="to-assign-the-content-to-distribution-points"></a>İçeriği dağıtım noktalarına atamak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, önceden hazırlanan içerik dosyasını oluştururken seçtiğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi**' ni genişletin, **uygulamalar**' a tıklayın ve ardından önceden hazırladığınız uygulamaları seçin.  

    - **Paketler**: **uygulama yönetimi**' ni genişletin, **paketler**' e tıklayın ve ardından önceden hazırladığınız paketleri seçin.  

    - **Dağıtım paketleri**: **yazılım güncelleştirmeleri**' ni genişletin, **dağıtım paketleri**' ni tıklatın ve ardından önceden hazırladığınız dağıtım paketlerini seçin.  

    - **Sürücü paketleri**: **işletim sistemleri**' ni genişletin, **sürücü paketleri**' ne tıklayın ve ardından önceden hazırladığınız sürücü paketlerini seçin.  

    - **Işletim sistemi görüntüleri**: **işletim sistemleri**' ni genişletin, **işletim sistemi görüntüleri**' ni tıklatın ve ardından önceden hazırladığınız işletim sistemi görüntülerini seçin.  

    - **Işletim sistemi yükleyicileri**: **işletim sistemleri**' ni genişletin, **işletim sistemi yükleyicileri**' ni tıklatın ve ardından önceden hazırladığınız işletim sistemi yükleyicilerini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri**' ni genişletin, **önyükleme yansımaları**' nı tıklatın ve ardından önceden hazırladığınız önyükleme görüntülerini seçin.  

3.  **Giriş** sekmesinde, **Dağıtım** grubunda, **İçeriği Dağıt**'ı tıklatın. Içerik Dağıtma Sihirbazı açılır.  

4.  **Genel** sayfasında, listelenen içeriğin önceden hazırladığınız içerik olduğunu doğrulayın, Configuration Manager seçili içerikle ilişkili içerik bağımlılıklarını algılamasını isteyip istemediğinizi seçin ve bağımlılıkları dağıtıma ekleyin ve ardından **İleri**' ye tıklayın.  

    > [!NOTE]  
    > **İlişkili içerik bağımlılıklarını Algıla** seçeneğini yapılandırma ve yalnızca uygulama içerik türü için bu dağıtım ayarına ekleme seçeneğiniz vardır. Configuration Manager, görev dizileri için bu ayarı otomatik olarak yapılandırır ve değiştirilemez.  

5.  **İçerik** sayfasında, görüntüleniyorsa, listelenen içeriğin dağıtmak istediğiniz içerik olduğunu doğrulayın ve ardından **İleri**' ye tıklayın.  

    > [!NOTE]  
    > **İçerik** sayfası, sihirbazın **genel** sayfasında **ilişkili içerik bağımlılıklarını Algıla ve bu dağıtıma Ekle** ayarı seçildiğinde görüntülenir.  

6.  **Içerik hedefi** sayfasında, **Ekle**' ye tıklayın, önceden hazırlanan dağıtım noktalarını içeren aşağıdakilerden birini seçin ve ardından ilişkili adımı izleyin:  

    - **Koleksiyonlar**: **Kullanıcı koleksiyonları** veya **Cihaz Koleksiyonları**' nı seçin, bir veya daha fazla dağıtım noktası grubu Ile ilişkili koleksiyona tıklayın ve ardından **Tamam**' a tıklayın.  

      > [!NOTE]  
      > Yalnızca bir dağıtım noktası grubuyla ilişkili koleksiyonlar görüntülenir.  Daha fazla bilgi için [Configuration Manager dağıtım noktalarını yükleyip yapılandırma](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) konusunun [dağıtım noktası gruplarını yönetme](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) bölümüne bakın.  

    - **Dağıtım noktası**: var olan bir dağıtım noktası seçin ve ardından **Tamam**' a tıklayın. İçeriği daha önce almış olan dağıtım noktaları görüntülenmez.  

    - **Dağıtım noktası grubu**: var olan bir dağıtım noktası grubunu seçin ve ardından **Tamam**' a tıklayın. İçeriği daha önce almış olan dağıtım noktası grupları gösterilmez.  

    İçerik hedefleri eklemeyi bitirdiğinizde **İleri**' ye tıklayın.  

7.  **Özet** sayfasında, devam etmeden önce dağıtımın ayarlarını gözden geçirin. İçeriği seçili hedeflere dağıtmak için **İleri**' ye tıklayın.  

8.  **Ilerleme durumu** sayfası dağıtımın ilerlemesini görüntüler.  

9. **Onay** sayfası, içeriğin dağıtım noktalarına başarıyla atanıp atanmadığını görüntüler. İçerik dağıtımını izlemek için, [Configuration Manager ile dağıttığınız Içeriği izleme](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)bölümüne bakın.  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a>Adım 3: Içeriği önceden hazırlanan Içerik dosyasından Ayıkla  
Önceden hazırlanan içerik dosyasını oluşturduktan ve içeriği dağıtım noktalarına atadıktan sonra, içerik dosyalarını bir site sunucusundaki veya dağıtım noktasındaki içerik kitaplığına ayıklayabilirsiniz. Genellikle önceden hazırlanmış içerik dosyasını USB sürücü gibi taşınabilir bir sürücüye kopyaladınız ya da içeriği DVD gibi bir medyaya veya içeriği gerektiren site sunucusu veya dağıtım noktası konumunda kullanılabilir hale getirin.  

İçeriği Ayıkla komut satırı aracını kullanarak içerik dosyalarını önceden hazırlanan içerik dosyasından el ile dışarı aktarmak için aşağıdaki yordamı kullanın.  

> [!IMPORTANT]  
> Içerik Ayıkla komut satırı aracını çalıştırdığınızda, araç önceden hazırlanan içerik dosyasını oluştururken geçici bir dosya oluşturur. Sonra, dosya hedef klasöre kopyalanır ve geçici dosya silinir. Bu geçici dosya için yeterli disk alanına sahip olmanız veya işlem başarısız olabilir. Geçici dosya şu konumda oluşturulur:  
>   
> - Geçici dosya, önceden hazırlanan içerik dosyası için hedef klasör olarak belirttiğiniz klasörde oluşturulur.  

> [!IMPORTANT]  
> Içerik Ayıkla komut satırı aracını çalıştıran kullanıcının, önceden hazırlanmış içeriği ayıkladığınız bilgisayarda **yönetici** haklarına sahip olması gerekir.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Önceden hazırlanan içerik dosyasından içerik dosyalarını ayıklamak için  

1.  Önceden hazırlanan içerik dosyasını içeriği ayıklamak istediğiniz bilgisayara kopyalayın.  

2.  İçerik Ayıkla komut satırı aracını &lt; *configmgrınstallationpath*> \Bin\\&lt;*Platform*> ' dan önceden hazırlanan içerik dosyasını ayıklamak istediğiniz bilgisayara kopyalayın.  

3.  Komut istemi ' ni açın ve önceden hazırlanan içerik dosyası ve Içerik Ayıkla aracının klasör konumuna gidin.  

    > [!NOTE]  
    > Bir site sunucusu, ikincil site sunucusu veya dağıtım noktasındaki bir veya daha fazla önceden hazırlanan içerik dosyasını ayıklayabilirsiniz.  

4.  Tek bir dosyayı içeri aktarmak için **ExtractContent/p:**&lt;*PrestagedFileLocation*>**\\**&lt;*PrestagedFileName*> **/s** yazın.  

    Önceden hazırlanan tüm dosyaları belirtilen klasöre aktarmak için **ExtractContent/p:**&lt;*PrestagedFileLocation*> **/s** yazın.  

    Örneğin, **ExtractContent/p: D:\PrestagedFiles\MyPrestagedFile.pkgx/s** yazın; burada `D:\PrestagedFiles\` PrestagedFileLocation `MyPrestagedFile.pkgx` , önceden hazırlanan dosya adıdır ve `/S` yalnızca dağıtım noktasındaki mevcut olan içerik dosyalarını ayıklamak için Configuration Manager bildirir.  

    Önceden hazırlanan içerik dosyasını bir site sunucusuna ayıkladığınızda, içerik dosyaları site sunucusundaki içerik kitaplığına eklenir ve ardından içerik kullanılabilirliği site sunucusu veritabanına kaydedilir. Önceden hazırlanan içerik dosyasını bir dağıtım noktasına aktardığınızda, içerik dosyaları dağıtım noktasındaki içerik kitaplığına eklenir, dağıtım noktası ana birincil site sunucusuna bir durum iletisi gönderir ve ardından içerik kullanılabilirliği site veritabanına kaydedilir.  

    > [!IMPORTANT]  
    > Aşağıdaki senaryoda, içerik yeni bir sürüme güncelleştirildiği zaman önceden hazırlanan içerik dosyasından ayıkladığınız içeriği güncelleştirmeniz gerekir:  
    >   
    >  1.  Bir paketin 1. sürümü için önceden hazırlanan içerik dosyası oluşturursunuz.  
    >  2.  Sürüm 2 ile paketin kaynak dosyalarını güncelleştirin.  
    >  3.  Önceden hazırlanan içerik dosyasını (paketin 1. sürümü) bir dağıtım noktasına ayıklayın.  
    >   
    > Configuration Manager paket sürüm 2 ' yi dağıtım noktasına otomatik olarak dağıtmaz. Yeni dosya sürümünü içeren yeni bir önceden hazırlanmış içerik dosyası oluşturmanız ve ardından içeriği ayıklayarak, değiştirilen dosyaları dağıtmak için dağıtım noktasını güncelleştirmeniz veya paketteki tüm dosyaları yeniden dağıtmanız gerekir.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a>Site sunucusundaki bir dağıtım noktasındaki içeriği önceden hazırlama  
Bir site sunucusuna bir dağıtım noktası yüklendiğinde, içeriği başarıyla önceden hazırlamak için aşağıdaki yordamı kullanmanız gerekir. Bunun nedeni içerik dosyalarının zaten içerik kitaplığında olması.  

Dağıtım noktası önceden hazırlanan içerik için etkin olmadığında veya dağıtım noktası bir site sunucusunda bulunmuyorsa, bu konudaki [önceden hazırlanan Içerik kullanma](#bkmk_prestage) bölümüne bakın.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Site sunucusunda bulunan dağıtım noktalarında içeriği önceden hazırlamak için  

1.  Dağıtım noktasının önceden hazırlanan içerik için etkin olmadığından emin olmak için aşağıdaki adımları kullanın.  

    1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

    2.  **Yönetim** çalışma alanında **dağıtım noktaları**' na tıklayın ve ardından site sunucusunda bulunan dağıtım noktasını seçin.  

    3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

    4.  **Genel** sekmesinde, **önceden hazırlanan içerik için bu dağıtım noktasını etkinleştir** onay kutusunun seçili olmadığından emin olun.  

2.  Bu konudaki [1. Adım: önceden hazırlanan Içerik dosyası oluşturma](#BKMK_CreatePrestagedContentFile) bölümünü kullanarak önceden hazırlanan içerik dosyasını oluşturun.  

3.  Bu konudaki [2. Adım: Içeriği dağıtım noktalarına atama](#BKMK_AssignContentToDistributionPoint) bölümüne tıklayarak içeriği dağıtım noktasına atayın.  

4.  Site sunucusunda, bu konunun [3. Adım: önceden hazırlanan Içerik dosyasından Içerik ayıklama](#BKMK_ExportContentFromPrestagedContentFile) bölümünde yer alan içeriği önceden hazırlanan içerik dosyasından ayıklayın.  

    > [!NOTE]  
    > Dağıtım noktası ikincil bir sitede olduğunda, en az 10 dakika bekleyin ve ardından üst birincil siteye bağlı bir Configuration Manager konsolu kullanarak, içeriği ikincil sitedeki dağıtım noktasına atayın.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a>Dağıttığınız içeriği yönetin  
İçeriği yönetmek için aşağıdaki seçenekleriniz vardır:  
- [İçeriği Güncelleştir](#update-content)
- [İçeriği yeniden Dağıt](#redistribute-content)
- [İçeriği kaldır](#remove-content)
- [içeriği doğrula](#validate-content)

### <a name="update-content"></a>İçeriği Güncelleştir
Dağıtım için kaynak dosya konumu yeni dosyalar eklenerek veya mevcut dosyaları daha yeni bir sürüme göre güncelleştirilerek, dağıtım noktalarını **Güncelleştir** veya **içeriği** Güncelleştir eylemini kullanarak dağıtım noktalarındaki içerik dosyalarını güncelleştirebilirsiniz:  
- İçerik dosyaları, kaynak dosya yolundan paket içerik kaynağına sahip olan sitedeki içerik kitaplığına kopyalanır  
- Paket sürümü artırılır  
- Site sunucularındaki ve dağıtım noktalarındaki içerik kitaplığının her örneği yalnızca değişmiş olan dosyalarla güncelleştirilir  

> [!WARNING]  
> Uygulamalar için paket sürümü her zaman 1 ' dir. Bir uygulama dağıtım türü için içeriği güncelleştirdiğinizde, Configuration Manager dağıtım türü için yeni bir içerik KIMLIĞI oluşturur ve paket yeni içerik KIMLIĞINE başvurur.  

#### <a name="to-update-content-on-distribution-points"></a>Dağıtım noktalarındaki içeriği güncelleştirmek için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, dağıtmak istediğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi** > **uygulamaları**' nı genişletin ve ardından dağıtmak istediğiniz uygulamaları seçin. **Dağıtım türleri** sekmesine tıklayın ve ardından güncelleştirmek istediğiniz dağıtım türünü seçin.  

    - **Paketler**: **uygulama yönetim** > **paketleri**' ni genişletin ve ardından güncelleştirmek istediğiniz paketleri seçin.  

    - **Dağıtım paketleri**: **yazılım güncelleştirmeleri** > **dağıtım paketleri**' ni genişletin ve sonra güncelleştirmek istediğiniz dağıtım paketlerini seçin.  

    - **Sürücü paketleri**: **işletim sistemleri** > **sürücü paketleri**' ni genişletin ve sonra güncelleştirmek istediğiniz sürücü paketlerini seçin.  

    - **İşletim sistemi görüntüleri**: **işletim sistemleri** > **işletim sistemi görüntüleri**' ni genişletin ve ardından güncelleştirmek istediğiniz işletim sistemi görüntülerini seçin.  

    - **İşletim sistemi yükleyicileri**: **işletim sistemleri** > **işletim sistemi yükleyicileri**' ni genişletin ve ardından güncelleştirmek istediğiniz işletim sistemi yükleyicilerini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri** >  **önyükleme görüntüleri**' ni genişletin ve ardından güncelleştirmek istediğiniz önyükleme görüntülerini seçin.  

3.  **Giriş** sekmesinde, **dağıtım** grubunda, **dağıtım noktalarını güncelleştir**' i tıklatın ve ardından içeriği güncelleştirmek istediğinizi onaylamak için **Tamam** ' ı tıklatın.  

    > [!NOTE]  
    > Uygulamaların içeriğini güncelleştirmek için **dağıtım türleri** sekmesine tıklayın, dağıtım türüne sağ tıklayın, **içeriği Güncelleştir**' e tıklayın ve ardından **Tamam** ' a tıklayarak içeriği yenilemek istediğinizi onaylayın.  

    > [!NOTE]  
    > Önyükleme görüntülerinin içeriğini güncelleştirdiğinizde dağıtım noktasını Yönetme Sihirbazı açılır. **Özet** sayfasındaki bilgileri gözden geçirin ve ardından içeriği güncelleştirmek için Sihirbazı doldurun.  

### <a name="redistribute-content"></a>İçeriği yeniden Dağıt
Paketteki tüm içerik dosyalarını dağıtım noktalarına veya dağıtım noktası gruplarına kopyalamak için bir paketi yeniden dağıtabilir ve böylece var olan dosyaların üzerine yazabilirsiniz.  

Paketteki içerik dosyalarını onarmak veya başlangıç dağıtımı başarısız olduğunda içeriği yeniden göndermek için bu işlemi kullanın. Bir paketi şuradan yeniden dağıtabilirsiniz:  

- Paket özellikleri  
- Dağıtım noktası özellikleri  
- Dağıtım noktası grubu özellikleri.  


#### <a name="to-redistribute-content-from-package-properties"></a>İçeriği paket özelliklerinden yeniden dağıtmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, dağıtmak istediğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi** >  **uygulamaları**' nı genişletin ve ardından yeniden dağıtmak istediğiniz uygulamayı seçin.  

    - **Paketler**: **uygulama yönetim** > **paketleri**' ni genişletin ve ardından yeniden dağıtmak istediğiniz paketi seçin.  

    - **Dağıtım paketleri**: **yazılım güncelleştirmeleri** >  **dağıtım paketleri**' ni genişletin ve ardından yeniden dağıtmak istediğiniz dağıtım paketini seçin.  

    - **Sürücü paketleri**: **işletim sistemleri** > **sürücü paketleri**' ni genişletin ve ardından yeniden dağıtmak istediğiniz sürücü paketini seçin.  

    - **İşletim sistemi görüntüleri**: **işletim sistemleri** > **işletim sistemi görüntüleri**' ni genişletin ve ardından yeniden dağıtmak istediğiniz işletim sistemi görüntüsünü seçin.  

    - **İşletim sistemi yükleyicileri**: **işletim sistemleri** > **işletim sistemi yükleyicileri**' ni genişletin ve ardından yeniden dağıtmak istediğiniz işletim sistemi yükleyicisini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri** >  **önyükleme görüntüleri**' ni genişletin ve ardından yeniden dağıtmak istediğiniz önyükleme görüntüsünü seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **Içerik konumları** sekmesine tıklayın, içeriği yeniden dağıtmak istediğiniz dağıtım noktasını veya dağıtım noktası grubunu seçin, yeniden **Dağıt**' a ve ardından **Tamam**' a tıklayın.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>İçeriği dağıtım noktası özelliklerinden yeniden dağıtmak için  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında **dağıtım noktaları**' na tıklayın ve ardından içeriği yeniden dağıtmak istediğiniz dağıtım noktasını seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **İçerik** sekmesine tıklayın, yeniden dağıtmak için içeriği seçin, yeniden **Dağıt**' a tıklayın ve ardından **Tamam**' a tıklayın.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>İçeriği dağıtım noktası grubu özelliklerinden yeniden dağıtmak için  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında, **dağıtım noktası grupları**' na tıklayın ve ardından içeriği yeniden dağıtmak istediğiniz dağıtım noktası grubunu seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **İçerik** sekmesine tıklayın, yeniden dağıtmak için içeriği seçin, yeniden **Dağıt**' a tıklayın ve ardından **Tamam**' a tıklayın.  

    > [!IMPORTANT]  
    > Paketteki içerik, dağıtım noktası grubundaki tüm dağıtım noktalarına yeniden dağıtılır.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>İçerik çoğaltmasını zorlamak için SDK 'Yı kullanma
Dağıtım Yöneticisi 'nin içeriği kaynak konumdan içerik kitaplığına kopyalamasını zorlamak için Configuration Manager SDK 'dan **Retrycontentreplication** WINDOWS YÖNETIM araçları (WMI) sınıfı yöntemini kullanabilirsiniz.  

Bu yöntemi yalnızca, içeriğin normal çoğaltmasıyla ilgili sorunlar olduktan sonra içeriği yeniden dağıtmanız gerektiğinde çoğaltmaya zorlamak için kullanın (genellikle konsolun Izleme düğümü kullanılarak onaylanır).   

Bu SDK seçeneği hakkında daha fazla bilgi için, MSDN 'de [SMS_CM_UpdatePackages sınıfında Retrycontentreplication yöntemi](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) bölümüne bakın. Microsoft.com.

### <a name="remove-content"></a>İçeriği kaldır
Dağıtım noktalarınız üzerinde artık içerik gerekmiyorsa, dağıtım noktasındaki içerik dosyalarını kaldırabilirsiniz.  

- Paket özellikleri  
- Dağıtım noktası özellikleri  
- Dağıtım noktası grubu özellikleri.  

Ancak, içerik aynı dağıtım noktasına dağıtılan başka bir paketle ilişkilendirildiğinde, içeriği kaldıramazsınız.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Paket içerik dosyalarını dağıtım noktalarından kaldırmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, silmek istediğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi** > **uygulamaları**' nı genişletin ve ardından kaldırmak istediğiniz uygulamayı seçin.  

    - **Paketler**: **uygulama yönetim** > **paketleri**' ni genişletin ve ardından kaldırmak istediğiniz paketi seçin.  

    - **Dağıtım paketleri**: **yazılım güncelleştirmeleri** > **dağıtım paketleri**' ni genişletin ve ardından kaldırmak istediğiniz dağıtım paketini seçin.  

    - **Sürücü paketleri**: **işletim sistemleri** > **sürücü paketleri**' ni genişletin ve ardından kaldırmak istediğiniz sürücü paketini seçin.  

    - **İşletim sistemi görüntüleri**: **işletim sistemleri** > **işletim sistemi görüntüleri**' ni genişletin ve ardından kaldırmak istediğiniz işletim sistemi görüntüsünü seçin.  

    - **İşletim sistemi yükleyicileri**: **işletim sistemleri** > **işletim sistemi yükleyicileri**' ni genişletin ve ardından kaldırmak istediğiniz işletim sistemi yükleyicisini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri** > **önyükleme görüntüleri**' ni genişletin ve ardından kaldırmak istediğiniz önyükleme görüntüsünü seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **Içerik konumları** sekmesine tıklayın, içeriği kaldırmak istediğiniz dağıtım noktasını veya dağıtım noktası grubunu seçin, **Kaldır**' a ve ardından **Tamam**' a tıklayın.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Paket içeriğini dağıtım noktası özelliklerinden kaldırmak için  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında **dağıtım noktaları**' na tıklayın ve ardından içeriğini silmek istediğiniz dağıtım noktasını seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **İçerik** sekmesine tıklayın, kaldırılacak içeriği seçin, **Kaldır**' a ve ardından **Tamam**' a tıklayın.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>İçeriği dağıtım noktası grubu özelliklerinden kaldırmak için  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında, **dağıtım noktası grupları**' na tıklayın ve ardından içeriğini kaldırmak istediğiniz dağıtım noktası grubunu seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **İçerik** sekmesine tıklayın, kaldırılacak içeriği seçin, **Kaldır**' a ve ardından **Tamam**' a tıklayın.  


### <a name="validate-content"></a>İçeriği doğrula
İçerik doğrulama işlemi, dağıtım noktalarında içerik dosyalarının bütünlüğünü doğrular. Bir zamanlamaya göre İçerik doğrulamayı etkinleştirir veya dağıtım noktaları ve paketlerin özelliklerinden el ile içerik doğrulaması başlatabilirsiniz.  

İçerik doğrulama işlemi başladığında Configuration Manager dağıtım noktalarında içerik dosyalarını doğrular ve dağıtım noktasındaki dosyalar için dosya karması beklenmiyorsa, Configuration Manager **izleme** çalışma alanında gözden geçirebilmeniz için bir durum iletisi oluşturur.  

İçerik doğrulama zamanlamasını yapılandırma hakkında daha fazla bilgi için, [Configuration Manager için dağıtım noktalarını yükleyip yapılandırma](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) konusunun [dağıtım noktası yapılandırması](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) bölümüne bakın.  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Dağıtım noktasındaki tüm içerik için içerik doğrulaması başlatmak için  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında **dağıtım noktaları**' na tıklayın ve ardından içeriğini doğrulamak istediğiniz dağıtım noktasını seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **İçerik** sekmesinde, içeriğini doğrulamak istediğiniz paketi seçin, **Doğrula**' ya tıklayın, **Tamam**' a ve ardından **Tamam**' a tıklayın. İçerik doğrulama işlemi, dağıtım noktasındaki paket için başlatılır.  

5.  İçerik doğrulama işleminin sonuçlarını görüntülemek için, **izleme** çalışma alanında **dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümüne tıklayın. Her paket türü (örneğin, uygulama, yazılım güncelleştirme paketi ve önyükleme görüntüsü) içeriği görüntülenir. İçerik durumunu izleme hakkında daha fazla bilgi için, [Configuration Manager ile dağıttığınız Içeriği izleme](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)bölümüne bakın.  

#### <a name="to-initiate-content-validation-for-a-package"></a>Bir paket için içerik doğrulaması başlatmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında, doğrulamak istediğiniz içerik türü için aşağıdaki adımlardan birini seçin:  

    - **Uygulamalar**: **uygulama yönetimi** > **uygulamaları**' nı genişletin ve ardından doğrulamak istediğiniz uygulamayı seçin.  

    - **Paketler**: **uygulama yönetim** > **paketleri**' ni genişletin ve ardından doğrulamak istediğiniz paketi seçin.  

    - **Dağıtım paketleri**: **yazılım güncelleştirmeleri** > **dağıtım paketleri**' ni genişletin ve ardından doğrulamak istediğiniz dağıtım paketini seçin.  

    - **Sürücü paketleri**: **işletim sistemleri** > **sürücü paketleri**' ni genişletin ve ardından doğrulamak istediğiniz sürücü paketini seçin.  

    - **İşletim sistemi görüntüleri**: **işletim sistemleri** > **işletim sistemi görüntüleri**' ni genişletin ve ardından doğrulamak istediğiniz işletim sistemi görüntüsünü seçin.  

    - **İşletim sistemi yükleyicileri**: **işletim sistemleri** >  **işletim sistemi yükleyicileri**' ni genişletin ve ardından doğrulamak istediğiniz işletim sistemi yükleyicisini seçin.  

    - **Önyükleme görüntüleri**: **işletim sistemleri** > **önyükleme görüntüleri**' ni genişletin ve ardından önceden hazırlamak istediğiniz önyükleme görüntüsünü seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  **Içerik konumları** sekmesinde, içeriğini doğrulamak istediğiniz dağıtım noktasını veya dağıtım noktası grubunu seçin, **Doğrula**' ya tıklayın, **Tamam**' a tıklayın ve ardından **Tamam**' a tıklayın. İçerik doğrulama işlemi, seçili dağıtım noktasındaki veya dağıtım noktası grubundaki içerik için başlar.  

5.  İçerik doğrulama işleminin sonuçlarını görüntülemek için, **izleme** çalışma alanında **dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümüne tıklayın. Her paket türü (örneğin, uygulama, yazılım güncelleştirme paketi ve önyükleme görüntüsü) içeriği görüntülenir. İçerik durumunu izleme hakkında daha fazla bilgi için, [Configuration Manager ile dağıttığınız Içeriği izleme](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)bölümüne bakın.  
