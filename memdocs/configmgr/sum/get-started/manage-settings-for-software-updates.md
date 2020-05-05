---
title: Yazılım güncelleştirmesi ayarlarını yönetme
titleSuffix: Configuration Manager
description: Yazılım güncelleştirme noktasını yükledikten sonra sitenizdeki yazılım güncelleştirmeleri için uygun olan istemci ayarları hakkında bilgi edinin.
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 2c8ca66bc83ec8eb18bc331287b6dbee47af7d85
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719809"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a>Yazılım güncelleştirmeleri için ayarları yönetme  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' de yazılım güncelleştirmelerini eşitledikten sonra, aşağıdaki bölümlerdeki ayarları yapılandırın ve doğrulayın.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a>Yazılım güncelleştirmeleri için istemci ayarları  
Yazılım güncelleştirme noktasını yükledikten sonra yazılım güncelleştirmeleri istemcilerde varsayılan olarak etkinleştirilir ve istemci ayarlarında bulunan **Yazılım Güncelleştirmeleri** sayfası varsayılan değerlere sahip olur. İstemci ayarları site genelinde kullanılır ve yazılım güncelleştirmeleri uyumluluk için tarandığı zaman ve yazılım güncelleştirmelerinin istemci bilgisayarlara nasıl ve ne zaman yükleneceğini etkiler. Yazılım güncelleştirmelerini dağıtmadan önce, istemci ayarlarının sitenizdeki yazılım güncelleştirmeleri için uygun olduğunu doğrulayın.  

> [!IMPORTANT]  
>  **İstemcilerde yazılım güncelleştirmelerini etkinleştir** ayarı varsayılan olarak etkindir. Bu ayarı temizlerseniz Configuration Manager, var olan dağıtım ilkelerini istemciden kaldırır.  

İstemci ayarlarını yapılandırma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

İstemci ayarları hakkında daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md).  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a> Yazılım güncelleştirmeleri için grup ilkesi ayarları  
Yazılım güncelleştirme noktasında çalıştırılan WSUS'a bağlanmak üzere istemci bilgisayarlarında Windows Update Aracısı (WUA) tarafından kullanılan belirli grup ilkesi ayarları vardır. Bu grup ilkesi ayarları aynı zamanda yazılım güncelleştirmeleri uyumluluğu için başarıyla tarama yapmak ve yazılım güncelleştirmeleri ile WUA'yı otomatik olarak güncelleştirmek üzere kullanılır.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Intranet Microsoft Update Hizmet Konumunu Belirt yerel ilkesi  
Yazılım güncelleştirme noktası bir site için oluşturulduğunda istemciler, yazılım güncelleştirme noktası sunucu adını sağlayan ve bilgisayardaki **Intranet Microsoft update hizmet konumunu belirt** yerel ilkesini yapılandıran bir makine ilkesini alır. WUA, **Güncelleştirmelerin algılanması için intranet update hizmetini kur** ayarında belirtilen sunucu adını alır ve yazılım güncelleştirmeleri uyumluluğu için tarama yaptığında bu sunucuya bağlanır. **Intranet Microsoft update hizmet konumunu belirt** ayarı için bir etki alanı ilkesi oluşturulduğunda bu ilke yerel ilkeyi geçersiz kılar ve WUA, yazılım güncelleştirme noktasının dışındaki bir sunucuya bağlanabilir. Bu durumda istemci, farklı ürünlere, sınıflandırmalara ve dillere bağlı olarak yazılım güncelleştirme uyumluluğu için tarama yapabilir. Bu nedenle, Active Directory ilkesini istemci bilgisayarları için yapılandırmamanız gerekir.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Microsoft Update Hizmet Konumu'ndan Alınan İçeriğe İzin Ver grup ilkesi  
Bilgisayarlardaki WUA, System Center Updates Publisher ile oluşturulan ve yayınlanan yazılım güncelleştirmeleri için tarama yapmadan önce **Microsoft update hizmet konumundan alınan imzalı içeriğe izin ver** Grup İlkesi ayarını etkinleştirmeniz gerekir. İlke ayarı etkinleştirildiğinde, bir intranet konumu üzerinden alınan yazılım güncelleştirmeleri yerel bilgisayarın **Güvenilir Yayımcılar** sertifika deposunda imzalanırsa WUA bu yazılım güncelleştirmelerini kabul eder. Updates Publisher için gereken Grup İlkesi ayarları hakkında daha fazla bilgi için bkz. [Updates Publisher 2011 Belge Kitaplığı](https://go.microsoft.com/fwlink/p/?LinkId=232476).  

### <a name="automatic-updates-configuration"></a>Otomatik güncelleştirmeler yapılandırması  
Otomatik Güncelleştirmeler güvenlik güncelleştirmelerinin ve diğer önemli indirmelerin istemci bilgisayarlarında alınmasını sağlar. Otomatik Güncelleştirmeler **Otomatik Güncelleştirmeleri Yapılandır** Grup İlkesi ayarı veya yerel bilgisayardaki Denetim Masası üzerinden yapılandırılır. Otomatik Güncelleştirmeler etkinleştirildiğinde istemci bilgisayarları güncelleştirme bildirimlerini alır ve yapılandırma ayarlarına bağlı olarak gerekli güncelleştirmeleri indirir ve yükler. Otomatik Güncelleştirmeler yazılım güncelleştirmeleriyle bir arada bulunduğunda tüm istemci bilgisayarları aynı güncelleştirme için bildirim simgelerini ve açılan ekran bildirimlerini görüntüleyebilir. Aynı zamanda, bir yeniden başlatma gerektiğinde tüm istemci bilgisayarları aynı güncelleştirme için bir yeniden başlatma iletişim kutusunu görüntüleyebilir.  

### <a name="self-update"></a>Kendi Kendine Güncelleştirme  
Otomatik Güncelleştirmeler istemci bilgisayarlarında etkinleştirildiğinde, yeni bir sürümün kullanılabilir olduğu veya bir WUA bileşeniyle ilgili sorunlar olduğu durumlarda WUA otomatik olarak kendi kendini güncelleştirir. Otomatik Güncelleştirmeler yapılandırılmamışsa veya devre dışı bırakılmışsa ve istemci bilgisayarları WUA'nın önceki bir sürümüne sahipse istemci bilgisayarlarının WUA yükleme dosyasını çalıştırması gerekir.  

## <a name="software-updates-properties"></a>Yazılım güncelleştirme özellikleri
Yazılım güncelleştirme özellikleri, yazılım güncelleştirmeleri ve ilgili içerik hakkında bilgi sağlar. Ayrıca bu özellikleri yazılım güncelleştirmeleri için ayarları yapılandırmak için kullanabilirsiniz. Çoklu yazılım güncelleştirmeleri özelliklerini açtığınızda, sadece **Maksimum Çalıştırma Süresi** ve **Özel Önem Derecesi** sekmeleri görüntülenir.   

Yazılım güncelleştirme özelliklerini açmak için aşağıdaki prosedürü kullanın.  

#### <a name="to-open-software-update-properties"></a>Yazılım güncelleştirme özelliklerini açmak için  

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  
2. Yazılım Kitaplığı çalışma alanında **Yazılım Güncelleştirmeleri**'ni genişletin ve **Tüm Yazılım Güncelleştirmeleri**'ne tıklayın.  
3. Bir veya daha fazla yazılım güncelleştirmesi seçin ve ardından **Giriş** sekmesinde, **Özellikler** grubundan **Özellikler** 'e tıklayın.  

   > [!NOTE]  
   >  **Tüm yazılım güncelleştirmeleri** düğümünde Configuration Manager, yalnızca **kritik** ve **güvenlik** sınıflandırmasına sahip olan ve son 30 gün içinde yayınlanan yazılım güncelleştirmelerini görüntüler.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a>Yazılım güncelleştirme bilgilerini gözden geçirme  
Yazılım güncelleştirme özelliklerinde, yazılım güncelleştirmesi hakkındaki ayrıntılı bilgileri gözden geçirebilirsiniz. Birden fazla yazılım güncelleştirmesini seçtiğinizde ayrıntılı bilgiler görüntülenmez. Aşağıdaki bölümlerde, seçilen yazılım güncelleştirmesi için mevcut bilgiler tanımlanır.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a>Yazılım Güncelleştirme ayrıntıları  
**Güncelleştirme Ayrıntıları** sekmesinde, seçilen yazılım güncelleştirmesi hakkında aşağıdaki özet bilgileri görüntüleyebilirsiniz:  

- **Bülten Kimliği**: Güvenlik yazılım güncelleştirmeleriyle ilişkili bülten kimliğini belirtir. Güvenlik bülteni ayrıntılarını, [Microsoft Güvenlik Yanıt Merkezi](https://portal.msrc.microsoft.com/) Web SAYFASıNDAKI bülten kimliğini arayarak bulabilirsiniz.  

> [!NOTE]
> Microsoft belgelerinin güvenlik güncelleştirmelerinin değişme şekli. Önceki model, Güvenlik Bülteni Web sayfalarını ve dahil olan güvenlik bülteni KIMLIK numaralarını (ör. MS16-XXX) Özet noktası olarak kullandı. Bülten KIMLIK numaraları da dahil olmak üzere bu güvenlik güncelleştirme belgelerinin devre dışı bırakılması ve güvenlik güncelleştirmesi Kılavuzu ile değiştirilmeleri. Bülten kimlikleri yerine, yeni kılavuz güvenlik açığı KIMLIK numaraları ve BB makale KIMLIĞI numaralarına göre özetlerdi. Daha fazla bilgi için bkz. [güvenlik güncelleştirme Kılavuzu SSS](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **Makale Kimliği**: Yazılım güncelleştirmesi makale kimliğini belirtir. Söz edilen makale, yazılım güncelleştirmesi ve yazılım güncelleştirmesinin düzelttiği veya geliştirdiği sorun konusunda daha ayrıntılı bilgi sunar.  

- **Düzeltme tarihi**: Yazılım güncelleştirmesinin son değiştirildiği tarihi belirtir.  

- **En yüksek önem derecesi**: Yazılım güncelleştirmesinin satıcı tanımlı önem derecesini belirtir.  

- **Açıklama**: Yazılım güncelleştirmesinin düzelttiği veya geliştirdiği durumla ilgili genel bir bakış sunar.  

- **Geçerli diller**: Yazılım güncelleştirmesinin geçerli olduğu dilleri listeler.  

- **Etkilenen ürünler**: Yazılım güncelleştirmesinin geçerli olduğu ürünleri listeler.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a>İçerik bilgileri  
**İçerik Bilgisi** sekmesinde, seçilen yazılım güncelleştirmesiyle ilişkili içerik hakkında aşağıdaki bilgileri gözden geçirin:  

-   **İçerik Kimliği**: Yazılım güncelleştirmesi içerik kimliğini belirtir.  

-   **İndirildi**: Configuration Manager yazılım güncelleştirme dosyalarını indirip indirmediğini belirtir.  

-   **Dil**: Yazılım güncelleştirmesi için dilleri belirtir.  

-   **Kaynak Yolu**: Yazılım güncelleştirmesi kaynak dosyalarının yolunu belirtir.  

-   **Boyut (MB)**: Yazılım güncelleştirmesi kaynak dosyalarının boyutunu belirtir.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a>Özel paket bilgileri  
**Özel Paket Bilgileri** sekmesinde, yazılım güncelleştirmesi için özel paket bilgilerini gözden geçirin. Seçilen yazılım güncelleştirmesi, yazılım güncelleştirme dosyasında bulunan paketli yazılım güncelleştirmelerini içeriyorsa, bunlar **Paket bilgileri** bölümünde görüntülenir. Bu sekme, farklı diller için güncelleştirme dosyaları gibi **İçerik Bilgisi** sekmesinde görüntülenen paketlenmiş yazılım güncelleştirmelerini görüntülemez.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a>Yenisiyle değiştirme bilgileri  
**Yenileriyle Değiştirme Bilgileri** sekmesinde, yazılım güncelleştirmesini yenisiyle değiştirme konusunda aşağıdaki bilgileri görüntüleyebilirsiniz:  

- **Bu güncelleştirme, aşağıdaki güncelleştirmelerle değiştirilmiştir**: Bu güncelleştirmenin yerine gelen yazılım güncelleştirmelerini belirtir, yani listelenen güncelleştirmeler yeni olanlardır. Çoğu durumda, yazılım güncelleştirmesinin yerini alan yazılım güncelleştirmelerinden birini dağıtırsınız. Listede görüntülenen yazılım güncelleştirmeleri, yazılım güncelleştirmeleri konusunda daha fazla bilgi sağlayan web sayfalarına köprüler içerir. Bu güncelleştirme yenilenmediğinde **Yok** görüntülenir.  

- **Bu güncelleştirme aşağıdaki güncelleştirmeleri değiştirmiştir**: Bu yazılım güncelleştirmesinin yerini aldığı yazılım güncelleştirmelerini belirtir, yani bu yazılım güncelleştirmesi yeni olandır. Çoğu durumda, bu yazılım güncelleştirmesini değiştirilen yazılım güncelleştirmelerini değiştirmek için dağıtırsınız. Listede görüntülenen yazılım güncelleştirmeleri, yazılım güncelleştirmeleri konusunda daha fazla bilgi sağlayan web sayfalarına köprüler içerir. Bu güncelleştirme başka bir güncelleştirmeyle yenilenmediğinde **Yok** görüntülenir.  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a>Yazılım güncelleştirme ayarlarını yapılandırma  
Özellikler kısmında yazılım güncelleştirme ayarlarını bir veya daha fazla yazılım güncelleştirmesi için yapılandırabilirsiniz. Çoğu yazılım güncelleştirme ayarını sadece merkezi yönetim sitesinden veya bağımsız birincil siteden yapılandırabilirsiniz. Aşağıdaki bölümler, yazılım güncelleştirmeleri ayarlarını yapılandırmanıza yardımcı olur.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a>Maksimum çalışma süresini ayarla  
**Maksimum Çalıştırma Süresi** sekmesinde, bir yazılım güncelleştirmesinin istemci bilgisayarlarda tamamlanması için ayrılan maksimum süre miktarını belirleyin. Güncelleştirme en uzun çalışma süresi değerinden uzun sürerse, Configuration Manager bir durum mesajı oluşturur ve yazılım güncelleştirmeleri yüklemesi için dağıtımı izlemeyi durduruyor. Bu ayarı sadece merkezi yönetim sitesinde veya bağımsız birincil sitede yapılandırabilirsiniz.  

Configuration Manager ayrıca, yazılım güncelleştirme yüklemesinin yapılandırılmış bir bakım penceresi içinde başlatılıp başlatılmayacağını anlamak için bu ayarı kullanır. Maksimum çalıştırma süresi, bakım penceresinde mevcut kalan süreden fazlaysa, yazılım güncelleştirme yüklemesi bir sonraki bakım penceresinin başlatılmasına kadar ertelenir. İstemci bilgisayarda yapılandırılmış bakım penceresiyle (zaman çerçevesi) yüklenecek birden fazla yazılım güncelleştirmesi olduğunda, önce en düşük maksimum çalıştırma süresine sahip yazılım güncelleştirmesi yüklenir, ardından bir sonraki en düşük maksimum çalıştırma süresi olan yazılım güncelleştirmesi yüklenir ve bu biçimde devam eder. İstemci, her yazılım güncelleştirmesini yüklemeden önce, mevcut bakım penceresinin yazılım güncelleştirmesini yüklemek için yeterli zaman sağlayacağını doğrular. Yazılım güncelleştirmesi yüklenmeye başladıktan sonra, yükleme bakım penceresinin bitimini aşsa bile yüklenmeye devam eder. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

**Çalışma Zamanı Üst Sınırı** sekmesinde aşağıdaki ayarları görüntüleyebilir ve yapılandırabilirsiniz:  

- **En fazla çalışma süresi**: yükleme artık Configuration Manager tarafından izlenmediği için, bir yazılım güncelleştirme yüklemesinin tamamlaması için ayrılan en fazla dakika sayısını belirtir. Bu ayar, ayrıca bakım penceresi sonlanmadan önce güncelleştirmeyi yüklemek için yeterli zaman kalıp kalmadığını belirlemek için kullanılır. Varsayılan ayar, hizmet paketleri için 60 dakikadır. Daha önceki bir sürümden yükseltme yaptığınızda, diğer yazılım güncelleştirme türleri için varsayılan değer 10 dakikadır. Configuration Manager sürüm 1511 veya daha yüksek bir sürümü ve 5 dakika. Değerler 5 ila 9999 dakika arasında değişebilir.  

> [!IMPORTANT]  
>  Maksimum çalıştırma süresi değerini yapılandırılan bakım penceresi süresinden daha küçük bir değere ayarladığınızdan emin olun veya bakım penceresi süresini maksimum çalışma zamanından daha büyük bir değere yükseltin. Aksi takdirde, yazılım güncelleştirme yüklemesi hiç başlamaz.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a>Özel önem derecesi ayarla  
Bir yazılım güncelleştirmesinin özelliklerinde yazılım güncelleştirmesinin özel önem derecesi değerlerini yapılandırmak için **Özel Önem Derecesi** sekmesini kullanabilirsiniz. Önceden tanımlı değerler ihtiyaçlarınızı karşılamıyorsa bunun yapılması gerekebilir. Özel değerler Configuration Manager konsolundaki **özel önem derecesi** sütununda listelenir. Yazılım güncelleştirmelerini tanımlı özel önem derecesi değerlerine göre sıralayabilir ve ayrıca bu değerleri filtreleyebilen sorgu ve raporlar da oluşturabilirsiniz. Bu ayarı sadece merkezi yönetim sitesinde veya bağımsız birincil sitede yapılandırabilirsiniz.  

**Özel Önem Derecesi** sekmesinde aşağıdaki ayarları yapılandırabilirsiniz.  

- **Özel önem derecesi**: Yazılım güncelleştirmeleri için özel bir önem derecesi değeri ayarlar. Listeden **Kritik**, **Önemli**, **Orta**veya **Düşük** seçeneğini belirleyin. Varsayılan olarak özel önem derecesi değeri boştur.

## <a name="crl-checking-for-software-updates"></a>Yazılım güncelleştirmeleri için CRL denetimi
Varsayılan olarak, Configuration Manager yazılım güncelleştirmelerinde imza doğrulanırken sertifika iptal listesi (CRL) kontrol edilmez. Her sertifika kullanıldığında CRL'nin denetlenmesi, iptal edilmiş sertifika kullanımına karşı daha fazla güvenlik sağlar ancak bağlantıda bir gecikmeye ve CRL denetimi yapılan bilgisayarda ek işlem yapılmasına neden olur.  

Kullanılıyorsa, yazılım güncelleştirmelerini işleyen Configuration Manager konsolları üzerinde CRL denetlemesi etkinleştirilmelidir.  

#### <a name="to-enable-crl-checking"></a>CRL denetimini etkinleştirmek için  
CRL denetimini gerçekleştiren bilgisayarda, ürün DVD 'sinden aşağıdaki komutu çalıştırın: **\\\smssetup\bin\x64**<*Language*>**\UpdDwnldCfg.exe/checkrevocation**.  

Örneğin, Ingilizce (US) için **\Smssetup\bin\x64\00000409\upddwnldcfg.exe/checkrevocation** çalıştırın  
