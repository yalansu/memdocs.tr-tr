---
title: Koleksiyon oluşturma
titleSuffix: Configuration Manager
description: Kullanıcı ve cihaz gruplarını daha kolay bir şekilde yönetmek için Configuration Manager koleksiyon oluşturun.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e81bc9b2135d17c445f8a86ff2214db394f63db
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865498"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Configuration Manager içinde koleksiyonlar oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Koleksiyonlar, Kullanıcı veya cihazların gruplanmalarıdır. Uygulamaları yönetme, uyumluluk ayarlarını dağıtma veya yazılım güncelleştirmelerini yükleme gibi görevler için koleksiyonları kullanın. Ayrıca koleksiyonları, istemci ayarları gruplarını yönetmek için veya rol tabanlı yönetimle birlikte bir yönetici kullanıcının erişebileceği kaynakları belirtmek üzere kullanabilirsiniz. Configuration Manager çeşitli yerleşik koleksiyonlar içerir. Daha fazla bilgi için bkz. [koleksiyonlara giriş](introduction-to-collections.md).  

> [!NOTE]  
> Bir koleksiyon, kullanıcıları veya cihazları içerebilir ancak ikisini birden içeremez.  


Bu makaledeki bilgiler Configuration Manager ' de koleksiyon oluşturmanıza yardımcı olabilir. Ayrıca, geçerli Configuration Manager sitesinde veya başka bir sitede oluşturulan koleksiyonları içeri aktarabilirsiniz. Koleksiyonları dışarı ve içeri aktarma hakkında daha fazla bilgi için bkz. [koleksiyonları yönetme](manage-collections.md).  


## <a name="collection-rules"></a>Koleksiyon kuralları

Configuration Manager bir koleksiyonun üyelerini yapılandırmak için kullanabileceğiniz farklı türde kurallar vardır.  


### <a name="direct-rule"></a>Doğrudan kural

Koleksiyona eklemek istediğiniz kullanıcıları veya bilgisayarları seçmek için doğrudan kuralları kullanın. Configuration Manager bir kaynağı kaldırmadığınız müddetçe üyelik değişmez. Kaynakları bir doğrudan kural koleksiyonuna ekleyebilmeniz için önce Configuration Manager bulmaları gerekir veya içeri aktarmış olmanız gerekir. Doğrudan kural koleksiyonlarının el ile değişiklikler gerektirdiğinden sorgu kuralı koleksiyonlarından daha fazla yönetim yükü vardır.


### <a name="query-rule"></a>Sorgu kuralı

Configuration Manager bir zamanlamaya göre çalıştırılan bir sorguyu temel alarak bir koleksiyonun üyeliğini dinamik olarak güncelleştirin. Örneğin, Active Directory Etki Alanı Hizmetleri'nde İnsan Kaynakları kurumsal biriminin üyesi olan kullanıcılardan oluşan bir koleksiyon oluşturabilirsiniz. Bu koleksiyon, Insan Kaynakları kuruluş birimine yeni kullanıcılar eklendiğinde veya buradan kaldırıldığında otomatik olarak güncelleştirilir.

Koleksiyon oluşturmak için kullanabileceğiniz sorgular için bkz. [sorgu oluşturma](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Cihaz kategorisi kuralı

Cihaz kategorilerini cihaz koleksiyonlarıyla ilişkilendirerek, cihazlarınızın yönetimini kolaylaştırın. 

Daha fazla bilgi için bkz. [cihazları koleksiyonlara otomatik olarak kategorilere ayırma](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Koleksiyonu dahil etme kuralı

Bir Configuration Manager koleksiyonuna başka bir koleksiyonun üyelerini ekleyin. Dahil edilen koleksiyon değişirse, Configuration Manager geçerli koleksiyonun üyeliğini bir zamanlamaya göre güncelleştirir.

Bir koleksiyona, birden çok koleksiyonu dahil etme kuralı ekleyebilirsiniz.


### <a name="exclude-collection-rule"></a>Koleksiyonu hariç tutma kuralı

Koleksiyonu hariç tutma kuralları, bir koleksiyonun üyelerini başka bir Configuration Manager koleksiyonundan dışlayamazsınız. Dışlanan koleksiyon değişirse, Configuration Manager geçerli koleksiyonun üyeliğini bir zamanlamaya göre güncelleştirir.

Bir koleksiyona, birden çok koleksiyonu hariç tutma kuralı ekleyebilirsiniz. Bir koleksiyon, hem koleksiyonu dahil etme hem de koleksiyonu hariç tutma kuralları içeriyorsa ve bir çakışma varsa, koleksiyonu hariç tutma kuralı önceliklidir.

#### <a name="example"></a>Örnek
Tek bir koleksiyon ekleme kuralına ve bir koleksiyonu hariç tutma kuralına sahip bir koleksiyon oluşturursunuz. Koleksiyonu dahil etme kuralı bir Dell masaüstü bilgisayar koleksiyonu için olsun. Hariç tutma koleksiyonu, 4 GB 'den az RAM 'e sahip bilgisayarların toplanması içindir. Yeni koleksiyon, en az 4 GB RAM 'e sahip Dell masaüstü bilgisayarları içerir.



## <a name="create-a-collection"></a><a name="bkmk_create"></a>Koleksiyon oluşturma  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin.  

    - Bir *cihaz koleksiyonu*oluşturmak Için **Cihaz Koleksiyonları** düğümünü seçin. Ardından, şeridin **giriş** sekmesinde, **Oluştur** grubunda, **cihaz koleksiyonu oluştur**' u seçin.  

    - Bir *Kullanıcı koleksiyonu*oluşturmak Için **Kullanıcı koleksiyonları** düğümünü seçin. Ardından, şeridin **giriş** sekmesinde, **Oluştur** grubunda, **Kullanıcı koleksiyonu oluştur**' u seçin.  

2. Sihirbazın **genel** sayfasında, bir **ad** ve **Açıklama**girin. **Sınırlama koleksiyonu** bölümünde, **Araştır**' ı seçin ve ardından bir sınırlandırma koleksiyonu seçin. Oluşturmakta olduğunuz koleksiyon yalnızca sınırlama koleksiyonunun üyelerini içerir.  

4. **Üyelik kuralları** sayfasında, **Kural Ekle** listesinde, koleksiyon için kullanmak istediğiniz üyelik kuralı türünü seçin. Her bir koleksiyon için birden çok kural yapılandırabilirsiniz. Her kuralın yapılandırması değişir. Her kuralı yapılandırma hakkında daha fazla bilgi için bu makalenin aşağıdaki bölümlerine bakın:  
    - [Doğrudan kural](#bkmk-direct)
    - [Sorgu kuralı](#bkmk-query)
    - [Cihaz kategorisi kuralı](#bkmk-category)
    - [Koleksiyonu dahil etme kuralı](#bkmk-include)
    - [Koleksiyonu hariç tutma kuralı](#bkmk-exclude)

5. Ayrıca **Üyelik kuralları** sayfasında, aşağıdaki ayarları gözden geçirin.

    - **Bu koleksiyon için Artımlı güncelleştirmeleri kullan**: önceki koleksiyon değerlendirmesinden yalnızca yeni veya değiştirilmiş kaynakları düzenli olarak taramak ve güncelleştirmek için bu seçeneği belirleyin. Bu işlem, tam bir koleksiyon değerlendirmesinden bağımsızdır. Varsayılan olarak, artımlı güncelleştirmeler 5 dakikalık aralıklarla gerçekleşir.  

        > [!IMPORTANT]  
        >  Aşağıdaki sınıfları kullanan sorgu kuralları olan koleksiyonlar Artımlı güncelleştirmeleri desteklemez:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (yalnızca kullanıcı koleksiyonları için)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (yalnızca kullanıcı koleksiyonları için)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Bu koleksiyonda tam güncelleştirme zamanla**: Koleksiyon üyeliğinin düzenli bir tam değerlendirmesini zamanlayın.  

        Sürüm 1810 ' den başlayarak, koleksiyon değerlendirme davranışında yapılan bu değişiklikler site performansını iyileştirebilir:<!--3607726-->  

        - Daha önce, sorgu tabanlı bir koleksiyonda bir zamanlama yapılandırdığınızda, **Bu koleksiyonda tam bir güncelleştirme zamanlamak**için koleksiyon ayarını etkinleştirmediyseniz, site sorguyu değerlendirmeye devam edebilir. Zamanlamayı tamamen devre dışı bırakmak için, zamanlamayı **none**olarak değiştirmeniz gerekiyordu.

            Artık bu ayarı devre dışı bıraktığınızda site zamanlamayı temizler. Koleksiyon değerlendirmesi için bir zamanlama belirtmek üzere **Bu koleksiyonda tam bir güncelleştirme zamanlama**seçeneğini etkinleştirin.  

            Sitenizi güncelleştirdiğinizde, bir zamanlama belirttiğiniz mevcut herhangi bir koleksiyon için, site **Bu koleksiyonda tam güncelleştirme planlama**seçeneğini sağlar. Bu yapılandırma sizin amacınızı olmasa da, siteyi güncelleştirdikten önce zamanlamanın gerçek davranışından kaynaklanabilir. Bir zamanlamaya göre bir koleksiyonu değerlendiren siteyi durdurmak için bu seçeneği devre dışı bırakın.  

        - **Tüm sistemler**gibi yerleşik koleksiyonların değerlendirmesini devre dışı bırakamıyorum, ancak artık zamanlamayı yapılandırabilirsiniz. Bu davranış, bu eylemi gereksinimlerinize uygun bir zamanda özelleştirmenize olanak sağlar. 

            > [!TIP]  
            > Yerleşik Koleksiyonlar üzerinde yalnızca özel zamanlamanın **saatini** değiştirin. **Yineleme modelini**değiştirmeyin. Gelecekteki yinelemeler belirli bir yinelenme düzeninin uygulanmasını sağlayabilir.  

6. Yeni koleksiyonu oluşturmak için sihirbazı tamamlayın. Yeni koleksiyon, **Varlıklar ve Uyumluluk** çalışma alanının **Cihaz Koleksiyonları** düğümünde görüntülenir.  

> [!NOTE]  
> Koleksiyon üyelerini görmek için Configuration Manager konsolunu yenilemeniz veya yeniden yüklemeniz gerekir. İlk zamanlanan güncelleştirmeden sonra koleksiyonda görünmez. Ayrıca, koleksiyon için **üyeliği Güncelleştir** ' i el ile seçebilirsiniz. Bir koleksiyon güncelleştirmesinin tamamlanması birkaç dakika sürebilir.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a>Doğrudan kural yapılandırma  

1. **Doğrudan üyelik kuralı oluşturma Sihirbazı**' nın **kaynak ara** sayfasında, aşağıdaki bilgileri belirtin.  

    - **Kaynak sınıfı**: aramak ve koleksiyona eklemek istediğiniz kaynak türünü seçin. Örnek:
        - **Sistem kaynağı**: istemci bilgisayarlardan döndürülen envanter verileri için arama yapın.
        - **Bilinmeyen bilgisayar**: bilinmeyen bilgisayarlar tarafından döndürülen değerler arasından seçim yapın.
        - **Kullanıcı kaynağı**: Configuration Manager tarafından toplanan kullanıcı bilgilerini arayın.
        - **Kullanıcı grubu kaynağı**: Configuration Manager tarafından toplanan Kullanıcı grubu bilgilerini arayın.

    - **Öznitelik adı**: aramak istediğiniz seçili kaynak sınıfıyla ilişkili özniteliği seçin. Örnek:  

        - Bilgisayarları NetBIOS adına göre seçmek istiyorsanız **kaynak sınıfı** listesinde **sistem kaynağı** ' nı, **öznitelik adı** listesinde **NetBIOS adı** ' nı seçin.  

        - Kullanıcıları kuruluş birimi (OU) adına göre seçmek istiyorsanız, **kaynak sınıfı** listesinde **Kullanıcı kaynağı** ' nı ve **öznitelik adı** listesinde **Kullanıcı OU adı** ' nı seçin.  

    - **Eski olarak işaretlenen kaynakları hariç tut**: bir istemci bilgisayar eski olarak işaretlenmişse, bu değeri arama sonuçlarına eklemeyin.  

    - **Configuration Manager istemcisi yüklü olmayan kaynakları hariç tut**: Bu kaynaklar arama sonuçlarında gösterilmez.  

    - **Değer**: seçili öznitelik adını aramak için bir değer girin. Yüzde karakterini (%) kullanın joker karakter olarak. Örnek:  
        - NetBIOS adı "d" ile başlayan bilgisayarları aramak için bu alana **% d** girin.  
        - Contoso OU 'sunda Kullanıcı aramak için bu alana **contoso** girin.

2. **Kaynakları seçin** sayfasında, **kaynaklar** listesinden koleksiyona eklemek istediğiniz kaynakları seçin ve ardından **İleri**' yi seçin.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a>Sorgu kuralı yapılandırma  

**Sorgu kuralı özellikleri** iletişim kutusunda, aşağıdaki bilgileri belirtin.  

- **Ad**: sorgu için benzersiz bir ad belirtin.  

- **Sorgu Ifadesini Içeri aktar**: **sorgu araştır** iletişim kutusunu açar. Koleksiyon için sorgu kuralı olarak kullanılacak bir [Configuration Manager sorgusu](../../../servers/manage/create-queries.md) seçin.   

- **Kaynak sınıfı**: aramak ve koleksiyona eklemek istediğiniz kaynak türünü seçin. İstemci bilgisayarlardan veya **Bilinmeyen bilgisayardan** , bilinmeyen bilgisayarlar tarafından döndürülen değerleri seçmek için döndürülen envanter verilerini aramak için **sistem** kaynağından bir değer seçin.  

- **Sorgu Ifadesini Düzenle**: koleksiyon için kural olarak kullanılacak bir sorgu yazabileceğiniz **sorgu ekstresi özellikleri** iletişim kutusunu açar. Sorgular hakkında daha fazla bilgi için bkz. [sorgulara giriş](../../../servers/manage/introduction-to-queries.md).  

    > [!TIP]  
    > Genel sekmesinde, yinelenen satırları atlamak için onay kutusunu seçmek **(benzersiz Seç)** , daha az satır döndürülmesine ve çok daha hızlı sonuçlara neden olabilir.

### <a name="device-category-rule"></a><a name="bkmk-category"></a>Cihaz kategorisi kuralı

Aşağıdaki eylemler **cihaz kategorileri Seç** penceresinde kullanılabilir.

- **Oluştur**: yeni bir kategori oluşturmak için bir ad belirtin.
- **Yeniden Adlandır**: Seçili kategoriyi yeniden adlandırın.
- **Sil**: bir veya daha fazla kategori seçin ve bu eylemi listeden kaldırmak için kullanın.

Daha fazla bilgi için bkz. [cihazları koleksiyonlara otomatik olarak kategorilere ayırma](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a>Bir koleksiyonu dahil etme kuralı yapılandırma  

**Koleksiyon Seç** iletişim kutusunda, yeni koleksiyona dahil etmek istediğiniz koleksiyonları seçin ve ardından **Tamam**' ı seçin.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a>Koleksiyonu hariç tutma kuralı yapılandırma  

**Koleksiyon Seç** iletişim kutusunda, yeni koleksiyondan hariç tutmak istediğiniz koleksiyonları seçin ve ardından **Tamam**' ı seçin.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a>Bir koleksiyonu içeri aktarma  

Bir siteden bir koleksiyonu dışarı aktardığınızda, Configuration Manager dosyayı bir Yönetilen Nesne Biçimi (MOF) dosyası olarak kaydeder. Bu yordamı, bu dosyayı site veritabanınıza aktarmak için kullanın. Bu yordamı gerçekleştirmek için Koleksiyonlar sınıfında **oluşturma** izinlerine sahip olmanız gerekir.

> [!IMPORTANT]  
> - Dosyanın yalnızca koleksiyon verileri içerdiğinden, güvenilen bir kaynaktan geldiğinden ve üzerinde oynanmadığından emin olun.  
> 
> - Dosyanın, kullanmakta olduğunuz Configuration Manager aynı sürümünü çalıştıran bir siteden aktarılmış olduğundan emin olun.  

Koleksiyonları dışarı aktarma hakkında daha fazla bilgi için bkz. [koleksiyonları yönetme](manage-collections.md).


1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Kullanıcı koleksiyonlarını** veya **Cihaz Koleksiyonları** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **koleksiyonları içeri aktar**' ı seçin.  

3. **Koleksiyonları Içeri aktarma Sihirbazı**' nın **genel** sayfasında **İleri**' yi seçin.  

4. **MOF dosya adı** sayfasında, **Araştır**' ı seçin. İçeri aktarmak istediğiniz koleksiyon bilgilerini içeren MOF dosyasına gidin.  

5. Koleksiyonu içeri aktarmak için sihirbazı tamamlayın. Yeni koleksiyon, **Varlıklar ve Uyumluluk** çalışma alanının **Kullanıcı Koleksiyonları** veya **Cihaz Koleksiyonları** düğümünde görüntülenir. Yeni içeri aktarılan koleksiyon için koleksiyon üyelerini görmek üzere Configuration Manager konsolunu yenileyin veya yeniden yükleyin.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a>Koleksiyon üyeliği sonuçlarını Azure Active Directory gruplarıyla eşitler

<!--3607475-->
> [!Tip]  
> Bu özellik ilk olarak sürüm 1906 ' de [yayın öncesi özelliği](../../../servers/manage/pre-release-features.md)olarak sunulmuştur. Sürüm 2002 ' den başlayarak, artık yayın öncesi bir özellik değildir.  

Koleksiyon üyeliklerinin Azure Active Directory (Azure AD) grubuna eşitlenmesini sağlayabilirsiniz. Bu eşitleme, koleksiyon üyeliği sonuçlarına dayalı olarak Azure AD grup üyelikleri oluşturarak bulutta mevcut şirket içi gruplandırma kurallarınızı kullanmanıza olanak sağlar. Cihaz koleksiyonlarını senkronize edebilirsiniz. Yalnızca Azure Active Directory kaydına sahip cihazlar Azure AD grubuna yansıtılır. Hem karma Azure AD 'ye katılmış hem de Azure Active Director 'a katılmış cihazlar desteklenir.

Azure AD eşitleme her beş dakikada bir gerçekleşir. Configuration Manager Azure AD 'ye kadar tek yönlü bir işlemdir. Azure AD 'de yapılan değişiklikler Configuration Manager koleksiyonlara yansıtılmaz, ancak Configuration Manager tarafından üzerine yazılmaz. Örneğin, Configuration Manager koleksiyonunda iki cihaz varsa ve Azure AD grubunda üç farklı cihaz varsa, eşitlemeden sonra Azure AD grubunda beş cihaz vardır.

### <a name="prerequisites"></a>Önkoşullar

- [Bulut yönetimi](../../../servers/deploy/configure/azure-services-wizard.md) IÇIN Azure AD ile tümleştirme
- [Kullanıcı keşfi Azure Active Directory](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- HTTPS veya [Gelişmiş BIR http](../../../plan-design/hierarchy/enhanced-http.md) etkin yönetim noktası
- **Tüm sistemler** koleksiyonuna erişim

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Azure AD 'de Grup oluşturma ve sahibi ayarlama

1. Adresine gidin [https://portal.azure.com](https://portal.azure.com) .
1. **Azure Active Directory**  >  **gruplar**  >  **tüm gruplar**' a gidin.
1. **Yeni Grup** ' a tıklayın ve bir **Grup adı** ve isteğe bağlı olarak **Grup açıklaması**yazın.
1. **Üyelik türünün** **atandığından**emin olun.
1. **Sahipler**' i seçin ve ardından Configuration Manager eşitleme ilişkisini oluşturacak kimliği ekleyin.
1. Azure AD grubunu oluşturmayı bitirmeden **Oluştur** ' a tıklayın.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Azure hizmeti için koleksiyon eşitlemesini etkinleştirme

1. Configuration Manager konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **Azure hizmetleri**' ne gidin.
1. Grubu oluşturduğunuz Azure AD kiracısına sağ tıklayın ve **Özellikler**' i seçin.
1. **Koleksiyon eşitleme** sekmesinde, **Azure dizin grubu eşitlemesini etkinleştir**onay kutusunu işaretleyin.
1. Ayarları kaydetmek için **Tamam** ' ı tıklatın.

### <a name="enable-the-collection-to-synchronize"></a>Koleksiyonu eşitlemeye izin et

1. Configuration Manager konsolunda **varlıklar ve uyum**  >  **genel bakış**  >  **Cihaz Koleksiyonları**' na gidin.
1. Eşitlemek için koleksiyona sağ tıklayın, ardından **Özellikler**' e tıklayın. 
1. **Bulut eşitleme** sekmesinde, **Ekle**' ye tıklayın.
1. Açılan menüden, Azure AD grubunuzu oluşturduğunuz **kiracıyı** seçin.
1. **Ad ile başlayan** arama ölçütlerinizi yazın ve ardından **Ara**' ya tıklayın.
  - Oturum açmanız istenirse, Azure AD grubu için sahip olarak belirttiğiniz kimliği kullanın.
1. Hedef grubunu seçin ve ardından koleksiyon özelliklerinden çıkmak için **Tamam** ' a tıklayarak grubu ekleyin ve tekrar **Tamam** ' a tıklayın.
1. Azure portal grup üyeliklerini doğrulayabilmeniz için önce 5 ila 7 dakika beklemeniz gerekir.
   - Tam eşitleme başlatmak için koleksiyona sağ tıklayıp **üyeliği Eşitle**' yi seçin.


### <a name="verify-the-azure-ad-group-membership"></a>Azure AD grup üyeliğini doğrulama

1. Adresine gidin [https://portal.azure.com](https://portal.azure.com) .
1. **Azure Active Directory**  >  **gruplar**  >  **tüm gruplar**' a gidin.
1. Oluşturduğunuz grubu bulun ve **Üyeler**' i seçin. 
1. Üyelerin Configuration Manager koleksiyonunda olanları yansıttığından emin olun.
   - Yalnızca Azure AD kimliğine sahip cihazlar grupta görünür.


![Koleksiyonları Azure AD 'ye eşitler](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a>PowerShell 'i kullanma

Koleksiyonları oluşturmak ve içeri aktarmak için PowerShell 'i kullanabilirsiniz. Daha fazla bilgi için bkz.

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Sonraki adımlar

[Koleksiyonları Yönet](manage-collections.md)
