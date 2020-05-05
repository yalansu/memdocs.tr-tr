---
title: Çekme dağıtım noktası
titleSuffix: Configuration Manager
description: Configuration Manager ile bir çekme dağıtım noktası kullanmayla ilgili yapılandırma ve sınırlamalar hakkında bilgi edinin. "
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c243897a4c52eff04263325b998c4b23d6b3dde4
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166596"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Configuration Manager ile bir çekme dağıtım noktası kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolundaki standart bir dağıtım noktasına içerik dağıttığınızda, site sunucusu içeriği dağıtım noktasına gönderir. Çekme dağıtım noktası, istemci gibi bir kaynak konumdan indirerek içeriği alır.  

İçeriği birçok dağıtım noktasına dağıttığınızda, çekme dağıtım noktaları site sunucusundaki işleme yükünü azaltmaya yardımcı olur. Ayrıca, her sunucuya içerik aktarımını hızlandırabilir. Genellikle site sunucusundaki dağıtım Yöneticisi bileşeni her dağıtım noktasına içerik gönderir. Bunun yerine, site, içeriği çekme dağıtım noktalarına aktarma sürecini yükler.  

Tek tek dağıtım noktalarını çekme dağıtım noktaları olacak şekilde yapılandırırsınız. Her istek temelli dağıtım noktası için, içerik alabileceğiniz bir veya daha fazla kaynak dağıtım noktası belirtin. Çekme dağıtım noktası, yalnızca kaynak dağıtım noktası olarak belirttiğiniz bir dağıtım noktasındaki içeriği indirebilir.

İçeriği konsolunda bir çekme dağıtım noktasına dağıttığınızda, site sunucusu bu bildirimi gönderir. Çekme dağıtım noktası daha sonra içeriği bir kaynak dağıtım noktasından indirir. Çekme dağıtım noktası, içeriğin bir kopyasına zaten sahip olan bir dağıtım noktasından indirerek içerik aktarımını yönetir.  

Çekme dağıtım noktaları, tipik dağıtım noktalarıyla aynı konfigürasyonları ve işlevleri destekler. Örneğin, bir çekme dağıtım noktası şunları destekler:

- Çok noktaya yayın ve PXE yapılandırması
- İçerik doğrulama
- İsteğe bağlı içerik dağıtımı
- İstemcilerden HTTP veya HTTPS iletişimleri
- Diğer dağıtım noktalarıyla aynı sertifika seçenekleri
- Tek tek veya bir dağıtım noktası grubunun üyesi olarak yönetme  

Dağıtım noktasını yüklerken bir çekme dağıtım noktası yapılandırın. Bir dağıtım noktası oluşturduktan sonra, rol özelliklerini düzenleyerek istek temelli dağıtım noktası olarak yapılandırın. Dağıtım noktasının çekme dağıtım noktası olarak nasıl etkinleştirileceği hakkında daha fazla bilgi için bkz. [çekme dağıtım noktası](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull).  

Dağıtım noktasının özelliklerini düzenleyerek istek temelli dağıtım noktası olacak şekilde yapılandırmayı kaldırın. Yapılandırmayı bir çekme dağıtım noktası olarak kaldırdığınızda, normal işleme döner. Site sunucusu dağıtım noktasına gelecek içerik aktarımlarını yönetir.  

## <a name="distribution-process"></a>Dağıtım işlemi

İçeriği bir çekme dağıtım noktasına dağıttığınızda, aşağıdaki olaylar dizisi oluşur:

- Konsolunda bir çekme dağıtım noktasına içerik dağıttığınızda, site sunucusundaki Paket Aktarma Yöneticisi bileşeni, içeriğin bir kaynak dağıtım noktasında kullanılabilir olup olmadığını doğrulamak için site veritabanını denetler. İçeriğin çekme dağıtım noktası için bir kaynak dağıtım noktasında olduğunu doğrulayamıyorum, içerik kullanılabilir olana kadar 20 dakikada bir kontrolü tekrarlar.  

- Paket Aktarım Yöneticisi içeriğin mevcut olduğunu onaylarsa, çekme dağıtım noktasını içeriği yüklemesi için bilgilendirir. Bu bildirim başarısız olursa, çekme dağıtım noktaları için yazılım dağıtım bileşeni **yeniden deneme ayarlarına** bağlı olarak yeniden dener. Çekme dağıtım noktası bu bildirimi aldığında, içeriği kaynak dağıtım noktalarından indirmeye çalışır.  

- Çekme dağıtım noktası içeriği indirirken, Paket Aktarma Yöneticisi, çekme dağıtım noktaları için yazılım dağıtım bileşeni **durum yoklama ayarlarına** bağlı olarak durumu yoklar.  Çekme dağıtım noktası içerik indirme işlemini tamamladığında, bu durumu bir yönetim noktasına gönderir.  

## <a name="configure-site-component-settings"></a>Site bileşeni ayarlarını yapılandırma

Bir çekme dağıtım noktası kullandığınızda, aşağıdaki site bileşeni ayarlarını gözden geçirin ve yapılandırın:  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Siteyi seçin. Şeritte, **site bileşenlerini Yapılandır**' ı seçin ve **yazılım dağıtımı**' nı seçin.  

3. **Çekme dağıtım noktası** sekmesine geçin.  

4. **Yeniden deneme ayarları** grubunda, aşağıdaki değerleri gözden geçirin:  

    - **Yeniden deneme sayısı**: Paket Aktarma Yöneticisi 'nin içeriği indirmek için çekme dağıtım noktasına bildirimde bulunma sayısı. Bu sayıda kez deneme sonrasında, Paket Aktarma Yöneticisi aktarımı iptal eder. Bu değer varsayılan olarak 30 ' dur.  

    - Yeniden **denemeden önce geciktir (dakika)**: Paket Aktarma yöneticisinin denemeler arasında beklediği dakika sayısı. Bu değer varsayılan olarak 20 ' dir.  

5. **Durum yoklama ayarları** grubunda, aşağıdaki değerleri gözden geçirin:  

    - **Yoklama sayısı**: Paket Aktarma yöneticisinin iş durumunu almak için çekme dağıtım noktasıyla iletişim kurduğu sayı. İş tamamlanmadan önce bu sayıda kez çalışırsa, Paket Aktarma Yöneticisi aktarımı iptal eder. Bu değer varsayılan olarak 72 ' dir.

    - Yeniden **denemeden önce geciktir (dakika)**: Paket Aktarma yöneticisinin denemeler arasında beklediği dakika sayısı. Bu değer varsayılan olarak 60 ' dir.

    > [!NOTE]  
    >  Paket Aktarma Yöneticisi, yoklama yeniden deneme sayısını aştığından bir işi iptal ettiğinde, çekme dağıtım noktası içeriği indirmeye devam eder. Tamamlandığında, çekme dağıtım noktası uygun durum iletisini gönderir ve konsolu yeni durumu yansıtır.  

## <a name="limitations"></a>Sınırlamalar

- Bir bulut dağıtım noktasını çekme dağıtım noktası olarak yapılandıramazsınız.  

- Site sunucusunda dağıtım noktası rolünü istek temelli dağıtım noktası olarak yapılandıramazsınız.  

- Dağıtım noktası için ön önceden hazırlanan içerik yapılandırması, istek temelli dağıtım noktası yapılandırmasını geçersiz kılar. Bu dağıtım noktasını bir çekme dağıtım noktasında **önceden hazırlanan içerik Için etkinleştirme seçeneğini etkinleştirirseniz** , içerik bekler. Kaynak dağıtım noktasından içerik çekmez. Önceden hazırlanmış içerik için etkinleştirilen standart bir dağıtım noktası gibi, site sunucusundan içerik almaz. Daha fazla bilgi için bkz. [önceden hazırlanan içerik](manage-network-bandwidth.md#BKMK_PrestagingContent).  

- Çekme dağıtım noktası, zamanlama veya hız sınırı yapılandırmasını kullanmaz. Daha önce yüklenmiş bir dağıtım noktasını çekme dağıtım noktası olacak şekilde yapılandırdığınızda, zamanlama ve hız sınırları için yapılandırma kaydedilir, ancak kullanılmaz. Daha sonra çekme dağıtım noktası yapılandırmasını kaldırırsanız, zamanlama ve hız sınırı yapılandırmaları önceden yapılandırılmış olarak uygulanır.  

    > [!NOTE]  
    >  **Zamanlama** ve **oran limitleri** sekmeleri, dağıtım noktasının özelliklerinde görünmez.  

- Çekme dağıtım noktaları, her site için **yazılım dağıtım bileşeni özelliklerinin** **genel** sekmesindeki ayarları kullanmaz. Bu ayarlar **eşzamanlı dağıtım** ve **çok noktaya yayın yeniden deneme**içerir.  

- İçeriği uzak bir ormandaki kaynak dağıtım noktasından aktarmak için, istek temelli dağıtım noktasına Configuration Manager istemcisini yükler. Ayrıca, kaynak dağıtım noktasına erişebilen bir ağ erişim hesabı yapılandırın. Site seçeneğini **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanacak**şekilde etkinleştirirseniz, ağ erişim hesabına gerek kalmaz.<!--1358228-->  

- Çekme dağıtım noktası aynı zamanda bir Configuration Manager istemcuysa, istemci sürümü, çekme dağıtım noktasını yükleyen Configuration Manager sitesiyle aynı olmalıdır. Çekme dağıtım noktası hem çekme dağıtım noktası hem de Configuration Manager istemcisi için ortak olan CCMFramework 'Ü kullanır.  

## <a name="about-source-distribution-points"></a>Kaynak dağıtım noktaları hakkında  

İstek temelli dağıtım noktasını yapılandırdığınızda, bir veya daha fazla kaynak dağıtım noktası belirtin:  

- Sihirbaz yalnızca kaynak dağıtım noktası olarak nitelendirmek gereken dağıtım noktalarını görüntüler.  

- Bir çekme dağıtım noktası, başka bir çekme dağıtım noktası için kaynak dağıtım noktası olarak belirtilebilir.  

- Configuration Manager konsolunu kullandığınızda, yalnızca HTTP 'yi destekleyen dağıtım noktaları kaynak dağıtım noktaları olarak belirtilebilir.  

- HTTPS için yapılandırılmış bir kaynak dağıtım noktası belirtmek için Configuration Manager SDK 'sını kullanın. HTTPS için yapılandırılmış bir kaynak dağıtım noktası kullanmak için, istek temelli dağıtım noktasına Configuration Manager istemcisini yükler.  

- Uzak ofislerinizin internete daha iyi bağlantısı varsa veya WAN bağlantılarınızda yükü azaltmak için kaynak olarak Microsoft Azure bir [bulut dağıtım noktası](use-a-cloud-based-distribution-point.md) kullanın. Çekme dağıtım noktası, Microsoft Azure ile iletişim kurmak için internet erişimine ihtiyaç duyuyor. İçeriğin kaynak bulut dağıtım noktasına dağıtılması gerekir.<!--1321554-->  

    > [!Note]  
    > Bu özellik, veri depolama ve ağ çıkışı için Azure aboneliğinize ücret vermez. Daha fazla bilgi için bkz. [bulut dağıtım noktası kullanma maliyeti](use-a-cloud-based-distribution-point.md#bkmk_cost).  

> [!Tip]  
> İstek temelli dağıtım noktası, kaynak dağıtım noktasından içerik yüklediğinde, söz konusu istek temelli dağıtım noktası **Çekme noktası kullanım özeti** raporunun **İstemci Erişimli (Benzersiz)** sütununda istemci olarak kabul edilir.  

### <a name="source-priorities"></a>Kaynak öncelikleri

- Her kaynak dağıtım noktasına ayrı bir öncelik atayın veya aynı önceliğe birden fazla kaynak dağıtım noktası atayın.  

- Öncelik, çekme dağıtım noktasının kaynak dağıtım noktalarından içerik istemesi sırasını belirler.  

- Çekme dağıtım noktaları, başlangıçta en düşük öncelik değerine sahip kaynak dağıtım noktasıyla temasa geçeri. Aynı önceliğe sahip birden fazla kaynak dağıtım noktası varsa, çekme dağıtım noktası bu önceliğe sahip kaynaklardan birini rastgele seçer.  

- İçerik seçili bir kaynakta yoksa, çekme dağıtım noktası, içeriği aynı önceliğe sahip başka bir dağıtım noktasından indirmeyi dener.  

- Verilen önceliğe sahip dağıtım noktalarından hiçbirinde içerik yoksa, çekme dağıtım noktası bir kaynak dağıtım noktasındaki içeriği bir sonraki öncelik düzeyiyle indirmeyi dener. İçerik bulunana kadar bu aramaya devam eder.

- Atanan kaynak dağıtım noktalarından hiçbirinde içerik yoksa, çekme dağıtım noktası 30 dakika bekler ve sonra işlemi yeniden başlatır.  

## <a name="inside-the-pull-distribution-point"></a>Çekme dağıtım noktası içinde

- İstek temelli dağıtım noktaları, içerik aktarımını yönetmek için **CCMFramework** bileşenini kullanır. Configuration Manager istemcisi bu bileşeni içerir.  

- Çekme dağıtım noktasını etkinleştirdiğinizde, site, **PullDP. msi**' yi yüklüyor. Bu yükleyici, CCMFramework bileşenini de ekler. Çerçeve Configuration Manager istemcisi gerektirmez.  

- Çekme dağıtım noktası yüklendikten sonra, birincil olarak çalışmak için **ccmexec** hizmetini kullanır.  

- Çekme dağıtım noktası içerik aktarırken, Windows içinde yerleşik **arka plan Akıllı Aktarım Hizmeti** (BITS) kullanır. Çekme dağıtım noktası, IIS sunucusu için BITS uzantısını yüklemenizi gerektirmez.<!--sms.503672 -Clarified BITS use-->

- İşletimsel Ayrıntılar için, çekme dağıtım noktasındaki aşağıdaki günlük dosyalarına bakın:  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> İstek temelli dağıtım noktası ekledikten sonra günlük dosyalarında HTTP 403 hataları görürseniz, aşağıdaki değişikliği yapın:
>
> 1. Kaynak dağıtım noktasında, aşağıdaki kayıt defteri değerini ayarlayın:`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. Kaynak dağıtım noktası sunucusunu yeniden başlatın.
>
> Sonra çekme dağıtım noktası, kaynaktan içerik yüklemeye başlamalıdır. Bu kayıt defteri anahtarı hakkında daha fazla bilgi için bkz. [TLS-SSL (Schannel SSP) genel bakış](https://docs.microsoft.com/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview).<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>Ayrıca bkz.  

[İçerik yönetimi için temel kavramlar](fundamental-concepts-for-content-management.md)
