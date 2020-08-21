---
title: Kullanıcı cihaz benzeşimi ile kullanıcıları ve cihazları bağlama
titleSuffix: Configuration Manager
description: Kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi ile bağlayın ve uygulamaları otomatik olarak bir kullanıcıyla ilişkili tüm cihazlara dağıtın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e1a55efa6b23aa489ea65b3296e33847163a5c4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695248"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Configuration Manager 'deki Kullanıcı cihaz benzeşimi ile Kullanıcı ve cihazları bağlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' deki Kullanıcı cihaz benzeşimi, bir kullanıcıyı bir veya daha fazla cihazla ilişkilendirir. Bu davranış, kullanıcıya uygulama dağıtmak için kullanıcının cihazlarının adlarını bilmeniz gereğini ortadan kaldırabilir. Uygulamayı kullanıcının cihazlarının her birine dağıtmak yerine, uygulamayı kullanıcıya dağıtırsınız. Ardından, Kullanıcı cihaz benzeşimi otomatik olarak uygulamanın bu kullanıcıyla ilişkilendirilmiş tüm cihazlara yüklendiğinden emin olur.  

Kullanıcıların işleri için her gün kullandığı birincil cihazları tanımlayın. Bir kullanıcı ile bir cihaz arasında benzeşim oluşturduğunuzda, daha fazla uygulama dağıtımı seçeneği elde edersiniz. Örneğin, bir Kullanıcı Microsoft Visio gerektiriyorsa, Windows Installer dağıtımı kullanarak kullanıcının birincil cihazına yükleyebilirsiniz. Bununla birlikte, birincil cihaz olmayan bir cihazda Visio 'Yu bir sanal uygulama olarak dağıtabilirsiniz. Kullanıcı oturum açmamışsa, kullanıcının cihazına yazılım ön dağıtımı yapmak için Kullanıcı cihaz benzeşimini de kullanabilirsiniz. Kullanıcı oturum açtığında, uygulama zaten yüklenir ve çalıştırılmaya hazırdır.  

Yalnızca bilgisayarlar için Kullanıcı cihaz benzeşimi bilgilerini yönetirsiniz. Configuration Manager, kaydettiği mobil cihazlar için Kullanıcı cihaz benzeşimlerini otomatik olarak yönetir.  

## <a name="manually-set-up-user-device-affinity"></a>Kullanıcı cihaz benzeşimini el ile ayarlama  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin.  

1. Cihaz seçin. Şeritteki **giriş** sekmesinde, **cihaz** grubunda, **birincil kullanıcıları Düzenle**' yi seçin.  

1. **Birincil kullanıcıları Düzenle** iletişim kutusunda, seçili cihaz için birincil kullanıcı olarak eklenecek kullanıcıları arayın ve seçin. **Ekle**' yi seçin.  

    > [!NOTE]  
    > **Birincil kullanıcılar** listesi, bu cihazın zaten birincil kullanıcıları olan kullanıcıları ve her Kullanıcı-cihaz ilişkisinin atanma yöntemini gösterir.  

## <a name="set-up-primary-devices-for-a-user"></a>Bir kullanıcı için birincil cihazları ayarlama  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Kullanıcılar** düğümünü seçin.  

1. Bir kullanıcı seçin. Şeritteki **cihaz** sekmesinde, **birincil cihazları Düzenle**' yi seçin.  

1. **Birincil cihazları Düzenle** iletişim kutusunda, seçili kullanıcı için birincil cihaz olarak eklenecek cihazları arayın ve seçin. **Ekle**' yi seçin.  

    > [!NOTE]  
    > **Birincil cihazlar** listesi, bu kullanıcı için zaten birincil cihaz olarak ayarlanmış olan cihazları ve her Kullanıcı-cihaz ilişkisinin atanma yöntemini gösterir.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Kullanıcı cihaz benzeşimlerini otomatik olarak oluşturma (yalnızca Windows bilgisayarları)

Configuration Manager, Windows olay günlüğünden Kullanıcı oturum açma olaylarıyla ilgili verileri okur. Kullanıcı cihaz benzeşimlerini otomatik olarak oluşturmak için, oturum açma olaylarını Windows olay günlüğünde depolamak üzere istemci bilgisayarlardaki yerel güvenlik ilkesinde bu iki seçeneği etkinleştirin:  

- **Hesap oturumu açma olaylarını denetle**  
- **Oturum açma olaylarını denetle**  

Bu ayarları yapılandırmak için Windows grup ilkesi kullanın.  

> [!IMPORTANT]  
> Bir hata Windows olay günlüğü 'nin yüksek sayıda girdi oluşturmasına neden olursa, yeni bir olay günlüğü oluşturabilir. Bu davranış gerçekleşirse, var olan oturum açma olayları Configuration Manager için kullanılamayabilir.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Siteyi otomatik olarak Kullanıcı aygıt benzeşimleri oluşturacak şekilde ayarlama  

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **istemci ayarları** düğümünü seçin.  

1. Varsayılan istemci ayarlarını değiştirmek için **varsayılan Istemci ayarları**' nı seçin. Şeritteki **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.

    Özel istemci Aracısı ayarları oluşturmak için, Şeritteki **giriş** sekmesinde, **Oluştur** grubunda, **özel istemci cihaz ayarları oluştur**' u seçin.

    > [!NOTE]  
    > Varsayılan istemci ayarlarını değiştirirseniz, site bunları hiyerarşideki tüm bilgisayarlara dağıtır. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

1. **Kullanıcı ve cihaz benzeşimi** grubunda, aşağıdaki ayarları ayarlayın:  

    - **Kullanıcı cihaz benzeşimi eşiği (dakika)**: site bir Kullanıcı cihaz benzeşimi oluşturmadan önce cihaz kullanımının dakika sayısını ayarlayın.  

    - **Kullanıcı cihaz benzeşimi eşiği (gün)**: sitenin kullanım tabanlı benzeşim eşiğini ölçtüğünden geçen gün sayısını ayarlayın.  

    - **Kullanıcı cihaz benzeşimlerini kullanım verilerinden otomatik olarak Yapılandır**: sitenin otomatik olarak Kullanıcı aygıt benzeşimleri oluşturmasını sağlamak için **true** ' ı seçin. **Yanlış**' ı seçerseniz, tüm Kullanıcı cihaz benzeşimi atamalarını el ile onaylamanız gerekir.  

    > [!TIP]  
    > Örneğin, **Kullanıcı cihaz benzeşimi eşiğini (dakika)** **60** dakikaya ayarlarsanız ve **Kullanıcı cihaz benzeşimi eşiğini (gün)** **5** güne ayarlarsanız, otomatik olarak bir Kullanıcı cihaz benzeşimi oluşturmak için kullanıcının cihazı 5 günlük bir dönemde en az 60 dakika kullanması gerekir.  

Configuration Manager otomatik bir Kullanıcı cihaz benzeşimi oluşturduktan sonra, Kullanıcı cihaz benzeşimi eşiklerini izlemeye devam eder. Kullanıcının cihaz için etkinliği ayarladığınız eşiklerin altındaysa, site Kullanıcı cihaz benzeşimini kaldırır. **Kullanıcı cihaz benzeşimi eşiği (gün)** değerini en az yedi gün olacak şekilde ayarlayın. Bu yapılandırma, Kullanıcı oturum açmadığı sırada otomatik olarak yapılandırılan bir Kullanıcı cihaz benzeşiminin kaybolduğu durumları önler. Örneğin, hafta sonu.  


## <a name="import-user-device-affinities-from-a-file"></a>Kullanıcı cihaz benzeşimlerini dosyadan içeri aktarma

Tek seferde birçok ilişki oluşturmak için, birden çok Kullanıcı aygıt benzeşimleri için ayrıntıları içeren bir dosyayı içeri aktarın. Hedef cihazların site tarafından zaten bulunduğundan ve Configuration Manager veritabanında kaynak olarak bulunduğundan emin olun.  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Kullanıcılar** ya da **cihazlar** düğümünü seçin.  

1. Şeritteki **giriş** sekmesinde, **Oluştur** grubunda, **Kullanıcı cihaz benzeşimini al**' ı seçin.  

1. Kullanıcı aygıt benzeşimini Içeri aktarma sihirbazında **eşleme Seç** sayfasında, şu bilgileri ayarlayın:  

    - **Dosya adı**. Benzeşim oluşturmak istediğiniz kullanıcı ve cihazların listesini içeren bir virgülle ayrılmış değerler (CSV) dosyası belirtin. Bu dosyada, her bir Kullanıcı ve cihaz çifti, virgülle ayrılmış değerlerle birlikte kendi satırı üzerinde olmalıdır. Şu biçimi kullanın: `<domain>\<username>,<device NetBIOS name>`  

    - **Bu dosyada başvuru amaçlı sütun başlıkları vardır**. . Csv dosyasında bir üst satır üst bilgisi varsa, bu seçeneği seçin. Site, içeri aktarma sırasında üst bilgi satırını yoksayar.  

1. İçeri aktardığınız dosya her satırda ikiden fazla öğe içeriyorsa, hangi sütunların kullanıcıları ve cihazları temsil ettiğini ve içeri aktarma sırasında hangi sütunların yok sayılacağını belirtmek için **sütun** ve **ata** ' yı kullanın.  

1. Sihirbazı tamamlayın.  


## <a name="let-users-create-their-own-device-affinities"></a>Kullanıcıların kendi cihaz benzeşimlerini oluşturmalarına izin ver

Bir kullanıcıyı yazılım merkezi 'nde kendi Kullanıcı cihaz benzeşimini oluşturmak üzere ayarlayın.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Siteyi Kullanıcı tarafından oluşturulan kullanıcı cihaz benzeşimi isteklerine izin verecek şekilde ayarlama  

1 Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **istemci ayarları** düğümünü seçin.  

1. Varsayılan istemci ayarlarını değiştirmek için **varsayılan Istemci ayarları**' nı seçin. Şeritteki **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.

    Özel istemci Aracısı ayarları oluşturmak için, Şeritteki **giriş** sekmesinde, **Oluştur** grubunda, **özel istemci Kullanıcı ayarları oluştur**' u seçin.

    > [!NOTE]  
    > Varsayılan istemci ayarlarını değiştirirseniz, site bunları hiyerarşideki tüm bilgisayarlara dağıtır. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

1. **Kullanıcı ve cihaz benzeşimi** grubunda, **kullanıcının birincil cihazlarını tanımlamasına izin ver**ayarını etkinleştirin.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Yazılım Merkezi 'nde bir Kullanıcı cihaz benzeşimi ayarlama

Sürüm 1902 ' den başlayarak, benzeşim ayarlamak için yazılım merkezi 'ni kullanın.

1. Yazılım Merkezi 'nde **Seçenekler** sekmesine gidin.

1. **İş bilgileri** bölümünde, **işlerim için düzenli olarak bu bilgisayarı kullanıyorum**seçeneğini belirleyin.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Uygulama kataloğunda bir Kullanıcı cihaz benzeşimi ayarlama

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
>
> - [Yazılım merkezini yapılandırma](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. Uygulama kataloğunda **sistemlerim**' i seçin.  

1. **İşlerim için düzenli olarak bu bilgisayarı kullanıyorum**seçeneğini belirleyin.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Kullanıcıların kullanıcı cihaz benzeşimi isteklerini yönetme

**Kullanıcı cihaz benzeşimini kullanım verilerinden otomatik olarak yapılandırmak**için istemci ayarını devre dışı bıraktığınızda, tüm Kullanıcı cihaz benzeşimi atamalarını el ile onaylamanız gerekir.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Kullanıcı cihaz benzeşimi isteğini onaylama veya reddetme  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin.  

1. Benzeşim isteklerini yönetmek istediğiniz kullanıcı veya cihaz koleksiyonunu seçin.  

1. Şeritteki **giriş** sekmesinde, **koleksiyon** grubunda, **benzeşim isteklerini yönet**' i seçin.  

1. **Kullanıcı cihaz benzeşimi Isteklerini Yönet** iletişim kutusunda bir benzeşim isteği seçin ve ardından **Onayla** veya **Reddet**' i seçin.  


## <a name="next-steps"></a>Sonraki adımlar

Ayrıca, kayıtlı bir cihazın birincil kullanımını bulmak için Microsoft Intune de kullanabilirsiniz. Daha fazla bilgi için, Intune belgelerinde Intune [cihazının birincil kullanıcısını bulma](/intune/find-primary-user) bölümüne bakın.