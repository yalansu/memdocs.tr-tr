---
title: Varlık Yönetim Bilgileri’ni yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager Varlık Yönetim Bilgileri ayarlayın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56a65a0a4e1dd9a96e5725ea8c68cc435947bb08
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713957"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Configuration Manager Varlık Yönetim Bilgileri yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Varlık Yönetim Bilgileri envanterler ve yazılım lisansı kullanımını yönetir.   

## <a name="steps-to-configure-asset-intelligence"></a>Varlık Yönetim Bilgileri’ni yapılandırma adımları  
   

- **1. adım**: varlık yönetim bilgileri raporları için gereken envanter verilerini toplamak için donanım envanterini [genişletme](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)bölümünde açıklandığı gibi donanım envanteri istemci aracısını etkinleştirmeniz gerekir.
- **2. adım**: [varlık yönetim bilgileri donanım envanteri raporlama sınıflarını etkinleştirin](#BKMK_EnableAssetIntelligence).  
- **3. adım**: [varlık yönetim bilgileri eşitleme noktası yüklemesi](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **4. adım**: [başarılı oturum açma olaylarının denetlenmesini etkinleştirme](#BKMK_EnableSuccessLogonEvents)  
- **5. adım**: [yazılım lisans bilgilerini içeri aktarma](#BKMK_ImportSoftwareLicenseInformation)  
- **6. adım**: [varlık yönetim bilgileri bakım görevlerini yapılandırma](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Configuration Manager sitelerde Varlık Yönetim Bilgileri etkinleştirmek için bir veya daha fazla Varlık Yönetim Bilgileri donanım envanteri raporlama sınıfını etkinleştirmeniz gerekir. Sınıfları, **Varlık Yönetim Bilgileri** giriş sayfasından veya **Yönetim** çalışma alanındaki **İstemci Ayarları** düğümünde bulunan istemci ayarları özelliklerinden etkinleştirebilirsiniz. Aşağıdaki yordamlardan birini kullanın.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Varlık Yönetim Bilgileri donanım envanteri raporlama sınıflarını Varlık Yönetim Bilgileri giriş sayfasından etkinleştirmek için  

1.  Configuration Manager konsolunda **varlık ve uyumluluk** > **varlık yönetim bilgileri**' nı seçin.  

3.  **Giriş** sekmesinde, **varlık yönetim bilgileri** grubunda, **envanter sınıflarını Düzenle**' yi seçin.   

4.  Varlık Yönetim Bilgileri Raporlamayı etkinleştirmek için **tüm varlık yönetim bilgileri raporlama sınıflarını etkinleştir** veya **yalnızca seçili varlık yönetim bilgileri raporlama sınıflarını etkinleştir**' i seçin ve görüntülenecek sınıflardan en az bir raporlama sınıfı seçin.  

    > [!NOTE]  
    >  Bu yordamı kullanarak etkinleştirdiğiniz donanım envanteri sınıflarına bağımlı olan Varlık Yönetimi Bilgileri raporlarının görüntülenebilmesi için istemcilerin taranması ve donanım envanterlerini döndürmesi gerekir.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Varlık Yönetim Bilgileri donanım envanteri raporlama sınıflarını istemci ayarları özelliklerinden etkinleştirmek için  

1.  Configuration Manager konsolunda, **Yönetim** >  **istemci ayarları** > **varsayılan istemci Aracısı ayarları**' nı seçin. Özel istemci ayarları oluşturduysanız, bunun yerine bunları seçebilirsiniz.  

3.  **Giriş** sekmesinde > **Özellikler** grubunda, **Özellikler**' i seçin.   

4.  **Donanım envanteri** > **kümesi sınıflarını**seçin. .  

5.   >  **Kategoriye göre filtrele****varlık yönetim bilgileri raporlama sınıfları**' nı seçin. Sınıf listesi yalnızca Varlık Yönetim Bilgileri donanım envanteri raporlama sınıflarıyla yenilenir.  

6.  Listeden en az bir raporlama sınıfı seçin.  

    > [!NOTE]  
    >  Bu yordamı kullanarak etkinleştirdiğiniz donanım envanteri sınıflarına bağımlı olan Varlık Yönetimi Bilgileri raporlarının görüntülenebilmesi için istemcilerin taranması ve donanım envanterlerini döndürmesi gerekir.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolü, Configuration Manager sitelerini Varlık Yönetim Bilgileri katalog bilgilerini eşitlemek üzere System Center Online 'a bağlamak için kullanılır. Varlık Yönetim Bilgileri eşitleme noktası, yalnızca Configuration Manager hiyerarşisinin en üst düzey sitesinde bulunan bir site sistemine yüklenebilir ve TCP bağlantı noktası 443 kullanılarak System Center Online ile eşitleme için Internet erişimi gerektirir.

Varlık Yönetim Bilgileri eşitleme noktası, yeni Varlık Yönetim Bilgileri katalog bilgilerini indirmeye ek olarak özel yazılım başlığı bilgilerini kategorilere ayrılmaları amacıyla System Center Online’a yükleyebilir. Microsoft, karşıya yüklenen tüm yazılım başlıklarını genel bilgi olarak değerlendirir. Özel yazılım başlıklarınızın gizli veya özel bilgiler içermediğinden emin olun. Yazılım başlığını kategorilere ayırma isteği hakkında daha fazla bilgi için bkz. [Request a catalog update for uncategorized software titles](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolü yüklemek için  

1.  Configuration Manager konsolunda, **Yönetim**> **Site yapılandırması** > **sunucuları ve site sistem rolleri**' ni seçin.  

3.  Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolünü yeni veya var olan bir site sistemi sunucusuna ekleyin:  

    -  Yeni bir **site sistemi sunucusu**için: Sihirbazı başlatmak **için giriş** sekmesinde, **Oluştur** grubunda, **site sistemi sunucusu oluştur** ' u seçin.   

        > [!NOTE]  
        >  Varsayılan olarak, Configuration Manager bir site sistemi rolü yüklediğinde, yükleme dosyaları en fazla kullanılabilir boş sabit disk alanına sahip olan, kullanılabilir ilk NTFS biçimli sabit disk sürücüsüne yüklenir. Configuration Manager belirli sürücülere yüklenmesini engellemek için, No_sms_on_drive. SMS adlı boş bir dosya oluşturun ve site sistemi sunucusunu yüklemeden önce bu dosyayı sürücünün kök klasörüne kopyalayın.  

    -  **Var olan bir site sistemi sunucusu**için: varlık yönetim bilgileri eşitleme noktası site sistemi rolünü yüklemek istediğiniz sunucuyu seçin. Bir sunucu seçtiğinizde, sunucuda zaten yüklü olan site sistemi rollerinin bir listesi, Ayrıntılar bölmesinde görüntülenir.  

         Sihirbazı başlatmak için, **sunucu** grubunun **giriş** sekmesinde, **site sistemi rolü Ekle** ' yi seçin.  

4.  **Genel** sayfasını doldurun. Varlık Yönetim Bilgileri eşitleme noktasını mevcut bir site sistemi sunucusuna eklerken, önceden yapılandırılmış olan değerleri doğrulayın.  

5.  **Sistem rolü seçimi** sayfasında, kullanılabilir roller listesinden **varlık yönetim bilgileri eşitleme noktası** ' nı seçin.  

6.  **Varlık yönetim bilgileri eşitleme noktası bağlantı ayarları** sayfasında **İleri**' yi seçin.  

     Varsayılan olarak **Bu Varlık Yönetim Bilgileri Eşitleme Noktasını kullan** ayarı seçilidir ve bu ayar bu sayfadan yapılandırılamaz. System Center Online yalnızca TCP bağlantı noktası 443’ten gelen ağ trafiğini kabul eder; bu nedenle **SSL bağlantı noktası numarası** ayarı sihirbazın bu sayfasından yapılandırılamaz.  

7.  İsteğe bağlı olarak, System Center Online kimlik doğrulama sertifikası (. pfx) dosyası için bir yol belirtebilirsiniz. Bağlantı sertifikası genellikle site rolü yüklemesi sırasında otomatik olarak sağlandığından sertifika için bir yol belirlemeniz gerekmez.  

8.  **Proxy sunucusu ayarları** sayfasında, varlık yönetim bilgileri eşitleme noktasının kataloğu eşitlemek üzere System Center Online 'a bağlanırken bir proxy sunucusu kullanıp kullanmayacağını ve proxy sunucusuna bağlanmak için kimlik bilgilerinin kullanılıp kullanılmayacağını belirtin.  

    > [!WARNING]  
    >  System Center Online’a bağlanmak için proxy sunucusu gerekliyse, proxy sunucusu kimlik doğrulaması için yapılandırılan hesapla ilişkili kullanıcı hesabı parolasının süresi dolduğunda bağlantı sertifikası da silinebilir.  

9. **Eşitleme Zamanlaması** sayfasında, Varlık Yönetim Bilgileri kataloğunun belirli bir çizelgeye göre eşitlenip eşitlenmeyeceğini seçin. Eşitleme zamanlamasını etkinleştirdiğinizde, basit veya özel bir eşitleme zamanlaması belirtmeniz gerekir. Zamanlanan eşitleme sırasında Varlık Yönetim Bilgileri eşitleme noktası, en son Varlık Yönetim Bilgileri kataloğunu almak üzere System Center Online’a bağlanır. Varlık Yönetim Bilgileri kataloğunu Configuration Manager konsolundaki Varlık Yönetim Bilgileri düğümünden el ile eşitlemeniz sağlayabilirsiniz. Varlık Yönetim Bilgileri kataloğunu el ile eşitlemeye yönelik adımlar için, [varlık yönetim bilgileri işlemlerinde](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md) [varlık yönetim bilgileri kataloğunu el ile eşitlemeye yönelik](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) bölümüne bakın.  

10. Sihirbazı tamamlama 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Dört adet Varlık Yönetim Bilgileri raporunda, istemci bilgisayarlarındaki Windows Güvenlik olayı günlüklerinden toplanan bilgiler görüntülenir. Bilgisayar güvenlik ilkesi oturum açma ayarlarını, başarılı oturum açma olaylarının denetlenmesini sağlamak üzere yapılandırmak için aşağıdaki adımları uygulayın.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Başarılı oturum açma olaylarını günlüğe kaydetmeyi yerel güvenlik ilkesi kullanarak etkinleştirmek için  

1.  Configuration Manager istemci bilgisayarında,**Yönetim Araçları** > **yerel güvenlik ilkesi**'ni **Başlat** > ' ı seçin.  

2.  **Yerel güvenlik ilkesi** iletişim kutusunda, **güvenlik ayarları**altında **Yerel ilkeler**' i genişletin ve sonra **Denetim ilkesi**' ni seçin.  

3.  Sonuçlar bölmesinde, **oturum açma olaylarını denetle**' ye çift tıklayın, **başarı** onay kutusunun seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Başarılı oturum açma olaylarını günlüğe kaydetmeyi Active Directory etki alanı güvenlik ilkesi kullanarak etkinleştirmek için  

1.  Bir etki alanı denetleyicisi bilgisayarında **Başlat**' ı seçin, **Yönetim Araçları**' nın üzerine gelin ve ardından **etki alanı güvenlik ilkesi**' ni seçin.  

2.  **Yerel güvenlik ilkesi** iletişim kutusunda, **güvenlik ayarları**altında **Yerel ilkeler**' i genişletin ve sonra **Denetim ilkesi**' ni seçin.  

3.  Sonuçlar bölmesinde, **oturum açma olaylarını denetle**' ye çift tıklayın, **başarı** onay kutusunun seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 Aşağıdaki bölümlerde, yazılım lisansı Içeri aktarma Sihirbazı 'Nı kullanarak hem Microsoft hem de genel yazılım lisanslama bilgilerini Configuration Manager site veritabanına aktarmak için gerekli yordamlar açıklanır. Yazılım lisansı bilgilerini lisans beyanı dosyalarından site veritabanına aktardığınızda, site sunucusu bilgisayar hesabının yazılım lisansı bilgilerini içeri aktarmak için kullanılan dosya paylaşımının, NTFS dosya sisteminde **Tam Denetim** izinlerine sahip olması gerekir.  

> [!IMPORTANT]  
>  Yazılım lisansı bilgileri site veritabanına aktarıldığında, mevcut yazılım lisansı bilgilerinin üzerine yazılır. Yazılım Lisansı İçeri Aktarma Sihirbazı ile kullandığınız yazılım lisans bilgileri dosyasının, gerekli tüm yazılım lisansı bilgilerinin tam listesini içerdiğinden emin olun.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Yazılım lisansı bilgilerini Varlık Yönetim Bilgileri kataloğuna aktarmak için  

1.  **Varlık ve uyumluluk** çalışma alanında **varlık yönetim bilgileri**' yi seçin.  

2.  **Giriş** sekmesinde, **varlık yönetim bilgileri** grubunda, **yazılım lisanslarını içeri aktar**' ı seçin.   

4.  **İçeri Aktarma** sayfasında, içeri aktardığınız dosyanın Microsoft Toplu Lisanslama (MVLS) dosyası (.xml veya .csv) veya Genel Lisans Beyanı dosyası (.csv) olduğunu belirtin. Genel Lisans Beyanı dosyası oluşturma hakkında daha fazla bilgi almak için bu konunun ilerleyen kısımlarındaki [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) başlığına bakın.  

    > [!WARNING]  
    >  Varlık Yönetim Bilgileri kataloğuna aktarabileceğiniz bir MVLS dosyasını .csv biçiminde indirmek için bkz. [Microsoft Toplu Lisanslama Hizmet Merkezi](https://go.microsoft.com/fwlink/p/?LinkId=226547). Bu bilgilere erişebilmek için web sitesinde kayıtlı bir hesabınızın olması gerekir. MVLS dosyanızı .xml biçiminde alma hakkında bilgi edinmek için Microsoft hesabı temsilcinize başvurmanız gerekir.  

5.  Lisans beyanı dosyasının UNC yolunu girin veya ağda paylaşılan bir klasör ve dosya seçmek için **Araştır** ' ı seçin.  

    > [!NOTE]  
    >  Lisans bilgileri dosyasına yetkisiz erişimin engellenmesi için, paylaşılan klasörün uygun şekilde güvenli hale getirilmesi ve sihirbazın çalıştırıldığı bilgisayardaki bilgisayar hesabının, lisans içeri aktarma dosyasını içeren paylaşım için Tam Denetim izinlerine sahip olması gerekir.  

6. Sihirbazı tamamlayın.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Genel lisans beyanını Varlık Yönetim Bilgileri kataloğuna aktarmak için, virgülle ayrılmış (.csv) dosya biçiminde el ile oluşturulan bir lisans içeri aktarma dosyası da kullanılabilir.  

> [!NOTE]  
>  **Name**, **Publisher**, **Version**ve **EffectiveQuantity** alanlarında veri bulunması zorunludur ve lisans içeri aktarma dosyasının ilk satırına tüm alanların girilmesi gerekir. Tüm tarih alanlarının şu biçimde görüntülenmesi gerekir: Gün/Ay/Yıl. Örneğin, 04/08/2008.  

Varlık Yönetim Bilgileri, genel lisans beyanında belirttiğiniz ürünleri eşleştirirken ürün adını ve ürün sürümünü kullanır, ancak yayımcı adını kullanmaz. Genel lisans beyanında, site veritabanında depolanan ürün adıyla birebir eşleşen bir ürün adı kullanmanız gerekir. Varlık Yönetim Bilgileri, genel lisans bildiriminde verilen bir **efekt miktarı** numarası alır ve sayıyı Configuration Manager envanterinde bulunan yüklü ürünlerin sayısıyla karşılaştırır.  

> [!TIP]  
>  Configuration Manager site veritabanında depolanan ürün adlarının tamamen bir listesini almak için, site veritabanında aşağıdaki sorguyu çalıştırabilirsiniz: v_GS_INSTALLED_SOFTWARE 'DAN Productname0 from ' yi SEÇIN.  

 Bir ürünün tam sürümünü veya sürümün bir bölümünü (yalnızca birincil sürüm gibi) belirtebilirsiniz. Aşağıdaki örneklerde, belirli bir ürün için genel lisans beyanı sürüm girişinden elde edilen sürüm eşleştirmeleri gösterilir.  

|Genel lisans beyanı girişi|Eşleşen site veritabanı girişleri|  
|-------------------------------------|------------------------------------|  
|Ad: "MySoftware", ProductVersion0: "2"|Productname0 From: "MySoftware", ProductVersion0: "2.01.1234"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.10.1234"|  
|Ad: "MySoftware", sürüm "2,05"|Productname0 From: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> Productname0 From: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Ad: "MySoftware", sürüm "2"<br /><br /> Ad: "MySoftware", sürüm "2,05"|İçeri aktarma sırasında hata oluştu. Aynı ürün sürümüyle eşleşen birden fazla giriş varsa içeri aktarma başarısız olur.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Genel lisans beyanı içeri aktarma dosyasını Microsoft Excel aracılığıyla oluşturmak için  

1.  Microsoft Excel'i açın ve yeni bir elektronik tablo oluşturun.  

2.  Yeni elektronik tablonun ilk satırına tüm yazılım lisansı veri alanı adlarını girin.  

3.  Yeni elektronik tablonun ikinci ve sonraki satırlarına gerekli yazılım lisansı bilgilerini girin. İçeri aktarılacak her yazılım lisansı için, sonraki satırlara gerekli yazılım lisansı veri alanlarının tümünün girildiğinden emin olun. Elektronik tabloya girilen yazılım başlığının, donanım envanteri çalıştırıldıktan sonra istemci bilgisayardaki Kaynak Gezgini’nde görüntülenen yazılım başlığıyla aynı olması gerekir.  

4.  Dosyayı. csv biçiminde kaydedin.  

5.  Yazılım lisansı bilgilerini Varlık Yönetim Bilgileri kataloğuna aktarmak için, .csv dosyasını dosya paylaşımına kopyalayın.  

6.  Configuration Manager konsolunda, yeni oluşturulan. csv dosyasını içeri aktarmak için yazılım lisansını Içeri aktarma Sihirbazı 'Nı kullanın.  

7.  Lisans bilgilerinin Varlık Yönetim Bilgileri kataloğuna başarıyla aktarıldığını doğrulamak için Varlık Yönetim Bilgileri **Lisans 15A-üçüncü taraf yazılım mutabakatı raporunu** çalıştırın.  

> [!NOTE]  
>  Sınama amacıyla kullanabileceğiniz bir genel yazılım lisans dosyası örneği için bkz. [örnek varlık yönetim bilgileri genel lisans içeri aktarma dosyası](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Yazılım lisanslarını açıklamak için tablo örneği oluşturma  
 Genel lisans beyanı içeri aktarma dosyası oluştururken, Varlık Yönetim Bilgileri kataloğuna aktarılacak yazılım lisanslarını açıklamak için aşağıdaki tablolar kullanılabilir.  

|Sütun adı|Veri türü|Gerekli|Örnek|  
|-----------------|---------------|--------------|-------------|  
|Adı|En fazla 255 karakter|Yes|Yazılım başlığı|  
|Yayımcı|En fazla 255 karakter|Yes|Yazılım yayımcısı|  
|Sürüm|En fazla 255 karakter|Yes|Yazılım başlığı sürümü|  
|Dil|En fazla 255 karakter|Yes|Yazılım başlığı dili|  
|EffectiveQuantity|Tamsayı değeri|Yes|Satın alınan lisans sayısı|  
|PONumber|En fazla 255 karakter|Hayır|Satın alma siparişi bilgileri|  
|ResellerName|En fazla 255 karakter|Hayır|Satıcı bilgileri|  
|DateOfPurchase|Şu biçimdeki tarih değeri: GG/AA/YYYY|Hayır|Lisans satın alma tarihi|  
|SupportPurchased|Bit değeri|Hayır|0 veya 1: Evet için 0, Hayır için 1 yazın|  
|SupportExpirationDate|Şu biçimdeki tarih değeri: GG/AA/YYYY|Hayır|Satın alınan destek bitiş tarihi|  
|Açıklamalar|En fazla 255 karakter|Hayır|İsteğe bağlı yorumlar|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Varlık Yönetim Bilgileri için aşağıdaki bakım görevleri kullanılabilir:  

-   **Uygulama başlığını envanter bilgileriyle denetle**: yazılım envanterinde raporlanan yazılım başlığının, varlık yönetim bilgileri kataloğundaki yazılım başlığıyla karşılaştırılmadığını denetler. Varsayılan olarak, bu görev etkindir ve 12:00 saat sonra Cumartesi günü çalışmak üzere zamanlanır. ve 5:00 tarihinden önce Bu bakım görevi yalnızca Configuration Manager hiyerarşinizdeki en üst düzey sitede kullanılabilir.  

-   **Yüklü yazılım verilerini Özetle**: **varlıklar ve uyum** çalışma alanında, **varlık yönetim bilgileri** düğümünün altındaki **envantere kaydedilmiş yazılım** düğümünde görüntülenen bilgileri sağlar. Görev çalıştığında, Configuration Manager birincil sitedeki tüm envantere kaydedilmiş yazılım başlıkları için bir sayı toplar. Varsayılan olarak, bu görev etkindir ve 12:00 ' den sonra her gün çalışacak şekilde zamanlanır. ve 5:00 tarihinden önce Bu bakım görevi yalnızca birincil sitelerde kullanılabilir.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Varlık Yönetim Bilgileri bakım görevlerini yapılandırmak için  

1.  Configuration Manager konsolunda, **Yönetim** > **Site yapılandırması** > **siteler**' i seçin.  

3.  Varlık Yönetim Bilgileri bakım görevinin yapılandırılacağı siteyi seçin.  

4.  **Giriş** sekmesinde, **Ayarlar** grubunda, **Site Bakımı**' nı seçin. Bir görev seçin ve ayarları değiştirmek için **Düzenle** ' yi seçin. 

    Zaman dilimini sitenin yoğun olmayan saatlerine ayarlamanızı öneririz. Süre, görevin çalışacağı zaman aralığıdır. **Görev Özellikleri** iletişim kutusunda **Şu kadar süre sonra başlat** ve **En geç başlatma zamanı** değerleri belirtilerek tanımlanır.  

    Geçerli günü seçip **Şu kadar süre sonra başlat** değerini geçerli saatten birkaç dakika sonra olacak şekilde ayarlayarak görevi hemen başlatabilirsiniz.  

7.  Ayarlarınızı kaydetmek için **Tamam ' ı** seçin. Görev, zamanlamaya göre çalışır.  

    > [!NOTE]  
    >  Bir görev ilk denemede çalışmazsa, görev başarıyla çalışana veya görevin çalıştırılabileceği zaman dilimine kadar görevi yeniden çalıştırmayı dener Configuration Manager.  
