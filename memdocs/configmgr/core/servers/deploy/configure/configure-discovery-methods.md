---
title: Bulmayı yapılandırma
titleSuffix: Configuration Manager
description: Ağınızı, Active Directory ve Azure Active Directory yönetilecek kaynakları bulmak için bulma yöntemlerini yapılandırın.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cfda27df7df537ededb1f103afdd6107354af786
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347296"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configuration Manager için bulma yöntemlerini yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Ağınızı, Active Directory ve Azure Active Directory (Azure AD) tarafından yönetilecek kaynakları bulmak için bulma yöntemlerini yapılandırın. İlk olarak, ortamınızda aramak için kullanmak istediğiniz her yöntemi etkinleştirin ve yapılandırın. Ayrıca, etkinleştirmek için kullandığınız yordamın aynısını kullanarak bir yöntemi devre dışı bırakabilirsiniz. Bu işlemin tek özel durumu, sinyal bulma ve sunucu bulma ' ya sahiptir:  

- Varsayılan olarak, Configuration Manager birincil sitesini yüklediğinizde **sinyal keşfi** zaten etkindir. Temel bir zamanlamaya göre çalışacak şekilde yapılandırılmıştır. Sinyal bulmayı etkin tutun. Cihazlar için keşif verileri kayıtlarının (DDR 'ler) güncel olduğundan emin olur. Sinyal bulma hakkında daha fazla bilgi için bkz. [sinyal bulma hakkında](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Sunucu bulma** bir otomatik bulma yöntemidir. Site sistemleri olarak kullandığınız bilgisayarları bulur. Yapılandırmaz veya devre dışı bırakabilirsiniz.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a>Active Directory orman keşfi  

Active Directory Orman Saptama yapılandırmasını sona erdirmesi için, Configuration Manager konsolunun aşağıdaki konumlarında ayarları yapılandırın:  

- **Bulma yöntemleri** düğümünde:

  - Bu bulma yöntemini etkinleştirin.  

  - Bir yoklama zamanlaması ayarlayın.  

  - Bulmanın, bulduğu Active Directory siteler ve alt ağlar için otomatik olarak sınırlar oluşturup oluşturamayacağını seçin.  

- **Active Directory ormanları** düğümünde:

  - Keşfetmesini istediğiniz ormanları ekleyin.  

  - Bu ormandaki Active Directory Siteleri ve alt ağları bulmayı etkinleştirin.  

  - Configuration Manager sitelerinin site bilgilerini ormana yayımlamasına olanak tanıyan ayarları yapılandırın.  

  - Her orman için Active Directory orman hesabı olarak kullanılacak bir hesap atayın.  

Active Directory orman bulmayı etkinleştirmek ve tek tek ormanları Active Directory orman keşfi ile kullanılmak üzere yapılandırmak için aşağıdaki yordamları kullanın.  

### <a name="configure-active-directory-forest-discovery"></a>Active Directory orman bulmayı yapılandırma  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **bulma yöntemleri** düğümünü seçin.  

2. Bulmayı yapılandırmak istediğiniz site için Active Directory orman bulma yöntemini seçin.  

3. Şeridin **giriş** sekmesinde **Özellikler**' i seçin.  

4. Özelliklerin **genel** sekmesinde aşağıdaki ayarları yapılandırın:  

    - Bulma yöntemini etkinleştirin.

    - Bulunan konumlar için site sınırları oluşturma seçeneklerini belirtin.  

    - Bulmanın ne zaman çalışacağını belirten bir zamanlama belirtin.  

5. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Active Directory orman keşfi için bir orman yapılandırma  

1. **Yönetim** çalışma alanında, **Hiyerarşi Yapılandırması**' nı genişletin ve **Active Directory ormanları** düğümünü seçin. Active Directory Orman Saptama daha önce çalıştıysa bulunan her bir ormanı sonuçlar bölmesinde görürsünüz. Bu bulma yöntemi çalıştırıldığında, yerel ormanı ve güvenilen ormanları bulur. Güvenilmeyen ormanları el ile ekleyin.  

    - Daha önce bulunan bir ormanı yapılandırmak için, sonuçlar bölmesinde ormanı seçin. Şeritte, orman özelliklerini açmak için **Özellikler** ' i seçin.

    - Listelenmeyen yeni bir ormanı yapılandırmak için, şeridin **giriş** sekmesinde, **Oluştur** grubunda, **Orman Ekle**' yi seçin. Bu eylem, **Orman Ekle** iletişim kutusunu açar.

2. **Genel** sekmesinde, keşfetmesini istediğiniz ormanın yapılandırmasını ve **Active Directory orman hesabını**belirtin. Bu hesap hakkında daha fazla bilgi için bkz. [hesaplar](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > Active Directory Orman Saptama, bulma ve güvenilmeyen ormanlara yayımlama için genel hesap gerektirir. Site sunucusunun bilgisayar hesabını kullanmıyorsanız, yalnızca genel bir hesap seçebilirsiniz.  

3. Sitelerin bu ormana site verilerini yayımlamasına izin vermek istiyorsanız **Yayımlama** sekmesinde, bu ormana yayımlama için yapılandırmayı sona erdirin.  

    > [!NOTE]  
    > Sitelerin bir ormana yayımlamasına izin verirseniz, Configuration Manager için o ormanın Active Directory şemasını genişletin. Active Directory orman hesabı, bu ormandaki sistem kapsayıcısı için tam denetim izinlerine sahip olmalıdır.  

4. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a>Bilgisayarlar, kullanıcılar veya gruplar için Active Directory bulma  

Bilgisayarları, kullanıcıları veya grupları bulmayı yapılandırmak için şu ortak adımlarla başlayın:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **bulma yöntemleri** düğümünü seçin.  

2. Bulmayı yapılandırmak istediğiniz site için yöntemini seçin.  

3. Şeridin **giriş** sekmesinde **Özellikler**' i seçin.  

4. Özelliklerin **genel** sekmesinde, bulmayı etkinleştirmek için onay kutusunu seçin. İsterseniz bulmayı şimdi yapılandırabilir ve daha sonra bulmayı etkinleştirmek için geri dönebilirsiniz.  

Ardından, belirli bulma yöntemlerini yapılandırmak için aşağıdaki bölümlerdeki bilgileri kullanın:  

- [Active Directory Grup Saptama](#bkmk_config-adgd)  

- [Active Directory Sistem Saptama](#bkmk_config-adgd)  

- [Active Directory Kullanıcı Saptama](#bkmk_config-adud)  

> [!NOTE]  
> Bu bölümdeki bilgiler Active Directory orman keşfi için geçerlidir.  

Bu bulma yöntemlerinin her biri diğerlerinden bağımsız olsa da benzer seçenekleri paylaşır. Bu yapılandırma seçenekleri hakkında daha fazla bilgi için bkz. [Grup, sistem ve Kullanıcı keşfi Için paylaşılan seçenekler](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> Bu bulma yöntemlerinin her biri tarafından yoklama Active Directory, önemli ağ trafiği oluşturabilir. Bu ağ trafiği ağınızın iş kullanımlarını olumsuz yönde etkilemediği zaman, her bulma yöntemini tek seferde çalışacak şekilde zamanlamayı göz önünde bulundurun.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a>Active Directory grubu bulmayı yapılandırma  

1. Active Directory grubu bulma Özellikler penceresi **genel** sekmesinde, bulma kapsamını yapılandırmak için **Ekle** ' yi seçin. **Grupların** veya **konumun**birini seçin. Ardından, **Grup Ekle** veya **Active Directory konum Ekle** iletişim kutusunda aşağıdaki konfigürasyonları tamamlayın:  

    1. Bu bulma kapsamı için bir **ad** belirtin.  

    2. Aranacak bir **Active Directory etki alanı** veya **konum** belirtin:  

        - **Gruplar**' ı seçerseniz, keşfedilecek bir veya daha fazla Active Directory grubu belirtin.  

        - **Konum**' u seçerseniz, bulunacak konum olarak bir Active Directory kapsayıcısı belirtin. Ayrıca, bu konum için Active Directory alt kapsayıcıların özyinelemeli aramasını etkinleştirebilirsiniz.  

    3. Sitenin bu keşif kapsamını aramak için kullandığı **Active Directory Grup bulma hesabını** belirtin. Daha fazla bilgi için bkz. [hesaplar](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Bulma kapsamı yapılandırmasını kaydetmek için **Tamam ' ı** seçin.  

2. Tanımlamak istediğiniz her ek keşif kapsamı için önceki adımları tekrarlayın.  

3. **Yoklama zamanlaması** sekmesinde, hem tam keşif yoklama zamanlamasını hem de Delta Keşfi yapılandırın.

4. **Seçenekler** sekmesinde, eski bilgisayar kayıtlarını bulma veya hariç tutmak için ayarları yapılandırın. Ayrıca, dağıtım gruplarının üyeliğini bulmayı da yapılandırın.  

    > [!NOTE]  
    > Varsayılan olarak, Active Directory Grup keşfi yalnızca güvenlik gruplarının üyeliğini bulur.  

5. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a>Active Directory sistem bulmayı yapılandırma  

1. Active Directory sistem keşfi Özellikler penceresi **genel** sekmesinde yeni bir Active Directory kapsayıcısı belirtmek için yeni **simgesini yeni simgesini seçin** ![ ](media/Disc_new_Icon.gif) . **Active Directory kapsayıcı** iletişim kutusunda aşağıdaki konfigürasyonları izleyin:  

    1. **Yol**için bir konum yazın veya gidin. Bu değer, bir kapsayıcı veya kuruluş birimi (OU) için geçerli bir LDAP yoludur. Site bu yolu kaynaklar için sorgular. Örneğin, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Arama davranışını değiştiren seçenekleri belirtin:  

        - **Active Directory gruplar içindeki nesneleri bul**: site Ayrıca bu yoldaki grupların üyeliklerine de bakar.  

        - **Yinelemeli arama Active Directory alt kapsayıcılar**: Bu seçeneği etkinleştirirseniz, site, yukarıdaki yolun içindeki ek kapsayıcıları veya OU 'ları arar. Bu seçeneği devre dışı bırakırsanız, site yalnızca belirli yoldaki kaynakları arar.  

          Sürüm 1806 ' den başlayarak, bu özyinelemeli aramanın dışında tutulacak alt kapsayıcılar ' ı seçin. Bu seçenek, bulunan nesne sayısını azaltmaya yardımcı olur. Yukarıdaki yolun altındaki kapsayıcıları seçmek için **Ekle** ' yi seçin. Yeni kapsayıcı Seç iletişim kutusunda, dışlanacak bir alt kapsayıcı seçin. Yeni kapsayıcı Seç iletişim kutusunu kapatmak için **Tamam ' ı** seçin.<!--1358143-->

          > [!Tip]  
          > Active Directory sistem keşfi Özellikler penceresi Active Directory kapsayıcıları listesi, bir sütunun **dışlamaları vardır**. Dışlanacak kapsayıcıları seçtiğinizde, bu değer **Evet**' tir.  

    3. Her konum için **Active Directory bulma hesabı**olarak kullanılacak hesabı belirtin. Daha fazla bilgi için bkz. [hesaplar](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Belirtilen her konum için, bir bulma seçenekleri kümesi ve benzersiz bir Active Directory keşif hesabı yapılandırabilirsiniz.  

    4. Active Directory kapsayıcı yapılandırmasını kaydetmek için **Tamam ' ı** seçin.  

2. **Yoklama zamanlaması** sekmesinde, hem tam keşif yoklama zamanlamasını hem de Delta Keşfi yapılandırın.  

3. **Active Directory öznitelikleri** sekmesinde, bulmasını istediğiniz bilgisayarlar için ek Active Directory öznitelikleri yapılandırın. Bu sekme varsayılan nesne özniteliklerini listeler.  

    > [!Tip]  
    > Örneğin, kuruluşunuz Active Directory bilgisayar hesabındaki **Description** özniteliğini kullanır. **Özel**' i seçin ve `Description` özel bir öznitelik olarak ekleyin. Bu bulma yöntemi çalıştıktan sonra, bu öznitelik Configuration Manager konsolundaki cihaz özellikleri sekmesinde gösterilir.<!--513948-->  

4. **Seçenekler** sekmesinde, eski bilgisayar kayıtlarını bulma veya hariç tutmak için ayarları yapılandırın.  

5. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a>Active Directory Kullanıcı bulmayı yapılandırma  

1. Active Directory Kullanıcı keşfi Özellikler penceresi **genel** **sekmesinde yeni** ![ ](media/Disc_new_Icon.gif) bir Active Directory kapsayıcısı belirtmek için yeni simge yeni simgesini seçin. **Active Directory kapsayıcı** iletişim kutusunda aşağıdaki konfigürasyonları izleyin:  

    1. Aranacak bir veya daha fazla konum belirtin.  

    2. Her konum için, arama davranışını değiştiren seçenekleri belirtin.  

    3. Her konum için **Active Directory bulma hesabı**olarak kullanılacak hesabı belirtin. Daha fazla bilgi için bkz. [hesaplar](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Belirtilen her konum için, benzersiz bir bulma seçenekleri kümesi ve benzersiz bir Active Directory keşif hesabı yapılandırabilirsiniz.  

    4. Active Directory kapsayıcı yapılandırmasını kaydetmek için **Tamam ' ı** seçin.  

2. **Yoklama zamanlaması** sekmesinde, hem tam keşif yoklama zamanlamasını hem de Delta Keşfi yapılandırın.  

3. **Active Directory öznitelikleri** sekmesinde, bulmasını istediğiniz bilgisayarlar için ek Active Directory öznitelikleri yapılandırın. Bu sekme varsayılan nesne özniteliklerini listeler.  

4. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a>Azure AD Kullanıcı keşfi

Azure AD Kullanıcı keşfi etkin değil veya diğer keşif yöntemleriyle aynı şekilde yapılandırılmadı. Azure AD 'ye Configuration Manager sitesini eklediğinizde bunu yapılandırın.

Daha fazla bilgi için bkz. [Azure AD Kullanıcı keşfi](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Önkoşullar

Bu bulma yöntemini etkinleştirmek ve yapılandırmak için [Azure hizmetlerini](azure-services-wizard.md) **bulut yönetimi**için yapılandırın.

Azure uygulamasını *oluşturmak* için Configuration Manager kullanıyorsanız, uygulamayı gerekli izinlerle yapılandırır.

Uygulamayı önce Azure 'da oluşturup Configuration Manager *içeri aktarırsanız* , uygulamayı el ile yapılandırmanız gerekir. Bu yapılandırma, dizin verilerini okumak için sunucu uygulamasına izin verilmesini içerir.

1. [Azure Portal](https://portal.azure.com) , *genel yönetici* izinlerine sahip bir kullanıcı olarak açın. **Azure Active Directory**gidin ve **uygulama kayıtları**' i seçin. Gerekirse **tüm uygulamalara** geçiş yapın.

1. Hedef uygulamayı seçin.

1. **Yönet** menüsünde, **API izinleri**' ni seçin.  

    1. **API izinleri** panelinde **izin Ekle**' yi seçin.  

    2. **API Izinleri iste** panelinde **Kuruluşumun kullandığı API**'lere geçin.  

    3. **Microsoft Graph** API 'sini arayın ve seçin.  

        > [!Tip]
        > Sürüm 1810 ve önceki sürümlerde **Azure Active Directory Graph** API 'sini kullanın.

    4. **Uygulama izinleri** grubunu seçin. **Dizin**' i genişletin ve **Dizin. Read. All**' u seçin.  

    5. **Izin Ekle**' yi seçin.  

1. **API izinleri** panelinde, **izin verme** bölümünde, **yönetici onayı ver...** seçeneğini belirleyin. **Evet**' i seçin.  

### <a name="configure-azure-ad-user-discovery"></a>Azure AD Kullanıcı bulmayı yapılandırma

**Bulut yönetimi** Azure hizmetini yapılandırırken:

- Sihirbazın **bulma** sayfasında, **Kullanıcı bulmayı Azure Active Directory etkinleştirme**seçeneğini belirleyin.
- **Ayarlar**' ı seçin.
- Azure AD Kullanıcı keşfi ayarları iletişim kutusunda bulma işleminin gerçekleştiği zaman için bir zamanlama yapılandırın. Ayrıca, Azure AD 'de yalnızca yeni veya değiştirilmiş hesapları denetleyen Delta Keşfi de etkinleştirebilirsiniz.

> [!Note]  
> Kullanıcı federe veya eşitlenmiş bir kimlik ise, Configuration Manager [Active Directory Kullanıcı keşfi](about-discovery-methods.md#bkmk_aboutUser) ve Azure AD Kullanıcı keşfi ' ni kullanmanız gerekir. Karma kimlikler hakkında daha fazla bilgi için bkz. [karma kimlik benimseme stratejisi tanımlama](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Azure AD Kullanıcı grubu bulma

<!--3611956-->
> [!Tip]  
> Bu özellik ilk olarak sürüm 1906 ' de [yayın öncesi özelliği](../../manage/pre-release-features.md)olarak sunulmuştur. Sürüm 2002 ' den başlayarak, artık yayın öncesi bir özellik değildir.  

Azure AD 'den bu grupların Kullanıcı gruplarını ve üyelerini bulabilirsiniz. Site, daha önce bulunmayan Azure AD gruplarındaki kullanıcıları bulduğunda, bunları Configuration Manager yeni kullanıcı kaynakları olarak ekler. Grup bir güvenlik grubu olduğunda, bir Kullanıcı grubu kaynak kaydı oluşturulur.

### <a name="prerequisites"></a>Önkoşullar

- Bulut yönetimi [Azure hizmeti](azure-services-wizard.md)
- Azure AD gruplarını okuma ve arama izni

### <a name="limitations"></a>Sınırlamalar

Azure AD Kullanıcı grubu bulma için Delta Keşfi 1906 sürümünde devre dışı bırakıldı. Configuration Manager sürüm 1910 ' den başlayarak başlatabilirsiniz.

### <a name="log-files"></a>Günlük dosyaları

Sorun giderme için SMS_AZUREAD_DISCOVERY_AGENT. log ' i kullanın. Bu günlük Ayrıca Azure AD Kullanıcı keşfi ile paylaşılır. Daha fazla bilgi için bkz. [günlük dosyaları](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Azure AD Kullanıcı grubu bulmayı etkinleştir

Mevcut bir **bulut yönetimi** Azure hizmetinde bulmayı etkinleştirmek için:

1. **Yönetim** çalışma alanına gidin, **Cloud Services**öğesini genişletin ve ardından **Azure hizmetleri** düğümünü seçin.
1. Azure hizmetlerinizin birini seçip Şeritteki **Özellikler** ' i seçin.
1. **Bulma** sekmesinde, **Azure Active Directory grubu bulmayı etkinleştirmek**için kutuyu işaretleyin ve ardından **Ayarlar**' ı seçin.
1. **Bulma kapsamları** sekmesinin altında **Ekle** ' yi seçin.
    - **Yoklama zamanlamasını** diğer sekmede değiştirebilirsiniz.
1. Bir veya daha fazla Kullanıcı grubu seçin. Ada göre **arama** yapabilir ve **yalnızca güvenlik gruplarını**görmek istiyorsanız öğesini seçebilirsiniz.
    - İlk kez **Ara** ' yı seçtiğinizde Azure 'da oturum açmanız istenir.
1. Grupları seçmeyi bitirdiğinizde **Tamam ' ı** seçin.
1. Bulma işlemi tamamlandıktan sonra, **Kullanıcılar** DÜĞÜMÜNDEKI Azure AD Kullanıcı gruplarınıza gözatabilmeniz gerekir.

Yeni bir **bulut yönetimi** Azure hizmeti yapılandırılırken bulmayı etkinleştirmek için:

- Sihirbazın **bulma** sayfasında, **Azure Active Directory grubu bulmayı etkinleştirme**seçeneğini belirleyin.
- **Ayarlar**' ı seçin.
- Azure AD grup keşfi ayarları iletişim kutusunda bulma kapsamınızı ve bulma işleminin gerçekleştiği zaman için bir zamanlama yapılandırın.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a>Sinyal keşfi

Birincil bir siteyi yüklerken sinyal bulma yöntemini Configuration Manager. Her yedi günde bir varsayılan zamanlamayı kullanmak istiyorsanız, yapılandırmak için başka bir şey yoktur. Aksi takdirde, yalnızca istemcilerin sinyal bulma verileri kaydını bir yönetim noktasına ne sıklıkta gönderecağına yönelik zamanlamayı yapılandırmanız gerekir.  

> [!NOTE]  
> Aynı sitede **yükleme bayrağını temizle** için hem istemci gönderme yüklemesini hem de site bakım görevini etkinleştirirseniz, sinyal bulma zamanlamasını, **yükleme bayrağını temizle** site bakım görevinin **istemci yeniden keşif süresinden** daha az olacak şekilde ayarlayın. Site bakım görevleri hakkında daha fazla bilgi için bkz. [bakım görevleri](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Sinyal bulma zamanlamasını yapılandırma  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **bulma yöntemleri** düğümünü seçin.  

2. Sinyal bulmayı yapılandırmak istediğiniz site için **sinyal bulma** yöntemini seçin.  

3. Şeridin **giriş** sekmesinde **Özellikler**' i seçin.  

4. İstemcilerin bir sinyal bulma veri kaydı gönderme sıklığını yapılandırın. Ardından, yapılandırmayı kaydetmek için **Tamam** ' ı seçin.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a>Ağ bulma  

Ağ bulmayı yapılandırmadan önce aşağıdaki konuları anlayın:  

- Kullanılabilir ağ bulma düzeyleri  

- Kullanılabilir ağ bulma seçenekleri  

- Ağ üzerinde ağ bulmayı sınırlandırma  

Daha fazla bilgi için bkz. [ağ bulma hakkında](about-discovery-methods.md#bkmk_aboutNetwork).  

Aşağıdaki bölümlerde ağ bulma için ortak yapılandırma bilgileri sağlanmaktadır. Aynı bulma çalışması sırasında kullanılmak üzere bu yapılandırmalardan bir veya daha fazla yapılandırma yapılandırabilirsiniz. Birden çok yapılandırma kullanıyorsanız, bulma sonuçlarını etkileyebilecek etkileşimler için plan yapın.  

Örneğin, belirli bir SNMP topluluk adı kullanan tüm basit ağ Yönetim Protokolü (SNMP) cihazlarını keşfedebilirsiniz. Aynı bulma çalıştırması için, belirli bir alt ağda bulmayı devre dışı bırakabilirsiniz. Bulma çalıştığında, ağ bulma devre dışı bıraktığınız alt ağda belirtilen topluluk adına sahip SNMP cihazlarını bulamaz.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a>Ağ topolojinizi belirleme  

Ağınızı eşlemek için yalnızca topoloji bulma kullanabilirsiniz. Bu tür bir keşif potansiyel istemcileri bulamaz. Yalnızca topoloji ağ bulma SNMP 'yi kullanır.  

Ağ topolojinizi eşlerken, **ağ bulma özellikleri** Iletişim kutusundaki **SNMP** sekmesinde **en fazla atlama sayısını** yapılandırın. Yalnızca birkaç atlama, bulma çalışırken kullanılan ağ bant genişliğini denetlemenize yardımcı olabilir. Ağınızı daha fazla buldıkça, ağ topolojinizi daha iyi anlamak için atlama sayısını artırın.  

Ağ topolojinizi anladıktan sonra, ağ bulma için ek özellikler yapılandırın. Bu özellikler potansiyel istemcileri ve bunların işletim sistemlerini bulmaya yardımcı olur. Ayrıca, arama yaptığı ağ kesimlerini sınırlamak için ağ bulmayı yapılandırın.  

Daha fazla bilgi için bkz. [Ağ topolojinizi belirleme](#bkmk_proc-top)

### <a name="network-discovery-search-options"></a>Ağ bulma arama seçenekleri

Configuration Manager, ağı aramak için aşağıdaki yöntemleri destekler:

- [Alt ağları kullanarak aramaları sınırlama](#BKMK_LimitBySubnet)
- [Belirli bir etki alanında arama](#BKMK_SearchByDomain)
- [SNMP topluluk adlarını kullanarak aramaları sınırlama](#BKMK_LimitBySNMPname)
- [Belirli bir DHCP sunucusunda arama](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a>Alt ağları kullanarak aramaları sınırlama  

Ağ bulmayı, bulma çalışması sırasında belirli alt ağları arayacak şekilde yapılandırabilirsiniz. Varsayılan olarak, ağ bulma, bulmayı çalıştıran sunucunun alt ağını arar. Yapılandırdığınız ve etkinleştirdiğiniz tüm ek alt ağlar yalnızca SNMP ve DHCP arama seçenekleri için geçerlidir. Ağ bulma etki alanlarını aradığında, alt ağlar için yapılandırmalarda sınırlı değildir.  

**Ağ bulma özellikleri** Iletişim kutusundaki **alt ağlar** sekmesinde bir veya daha fazla alt ağ belirtirseniz, yalnızca **etkin**olarak işaretlediğiniz alt ağları arar.  

Bir alt ağı devre dışı bıraktığınızda, site onu keşiften dışlar ve aşağıdaki koşullar geçerli olur:  

- SNMP tabanlı sorgular alt ağda çalışmaz.  

- DHCP sunucuları, alt ağda bulunan bir kaynak listesiyle yanıt vermez.  

- Etki alanı tabanlı sorgular, alt ağda yer alan kaynakları bulabilir.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a>Belirli bir etki alanında arama  

Ağ bulmayı, bulma çalışması sırasında belirli bir etki alanını veya etki alanı kümesini arayacak şekilde yapılandırabilirsiniz. Varsayılan olarak, ağ bulma, bulmayı çalıştıran sunucunun yerel etki alanını arar.  

**Ağ bulma özellikleri** Iletişim kutusundaki **etki alanları** sekmesinde bir veya daha fazla etki alanı belirtirseniz, yalnızca **etkin**olarak işaretlediğiniz etki alanlarını arar.  

Bir etki alanını devre dışı bıraktığınızda, site onu keşiften dışlar ve aşağıdaki koşullar geçerli olur:  

- Ağ bulma, bu etki alanındaki etki alanı denetleyicilerini sorgulayamaz.  

- SNMP tabanlı sorgular, etki alanındaki alt ağlarda çalışmaya devam edebilir.  

- DHCP sunucuları, etki alanında yer alan kaynakların listesiyle yine de yanıt verebilir.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a>SNMP topluluk adlarını kullanarak aramaları sınırlama  

Ağ bulmayı, belirli bir SNMP Community veya bir bulma çalışması sırasında bir topluluk kümesi arayacak şekilde yapılandırırsınız. Varsayılan olarak, yöntemi **ortak** topluluk adını yapılandırır.  

Ağ bulma, SNMP cihazları olan yönlendiricilere erişim kazanmak için topluluk adlarını kullanır. Yönlendirici, ilk yönlendiriciyle bağlantılı diğer yönlendiriciler ve alt ağlar hakkında bilgi içeren ağ keşfi sağlayabilir.  

> [!NOTE]  
> SNMP topluluk adları parolalara benzer. Ağ bulma, yalnızca bir topluluk adı belirttiğiniz SNMP cihazından bilgi alabilir. Her SNMP cihazı kendi topluluk adına sahip olabilir, ancak çoğunlukla aynı topluluk adı birkaç cihaz arasında paylaşılır. Ayrıca, çoğu SNMP cihazı varsayılan bir **topluluk adına sahiptir.** Ancak bazı kuruluşlar, **genel** topluluk adını cihazlarından güvenlik önlemi olarak siler.  

**Ağ bulma özellikleri** Iletişim kutusundaki **SNMP** sekmesinde birden çok SNMP topluluğu eklerseniz, bunları gösterildikleri sırayla arar. En sık kullanılan adların listenin en üstünde bulunduğundan emin olun. Bu yapılandırma, farklı adlar kullanarak bir cihazla bağlantı kurmaya çalıştığında sitenin oluşturduğu ağ trafiğini en aza indirmeye yardımcı olur.

> [!NOTE]  
> SNMP topluluk adını kullanarak, belirli bir SNMP cihazının IP adresini veya çözümlenebilen adını belirtebilirsiniz. Bu eylemi, **ağ bulma özellikleri** Iletişim kutusundaki **SNMP cihazları** sekmesinde gerçekleştirebilirsiniz.  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a>Belirli bir DHCP sunucusunda arama  

Bir bulma çalışması sırasında DHCP istemcilerini bulmak için ağ bulmayı belirli bir DHCP sunucusunu veya birden çok sunucuyu kullanacak şekilde yapılandırabilirsiniz.  

Ağ bulma, **ağ bulma özellikleri** Iletişim kutusundaki **DHCP** sekmesinde belirttiğiniz her DHCP sunucusunu arar. Keşfi çalıştıran sunucu IP adresini bir DHCP sunucusundan kiraladığında, bulmayı bu DHCP sunucusunu arayacak şekilde yapılandırabilirsiniz. **Site sunucusunun kullanmak üzere YAPıLANDıRıLDıĞı DHCP sunucusunu dahil etme**seçeneğiyle bu davranışı etkinleştirin.  

> [!NOTE]  
> Ağ bulma 'da bir DHCP sunucusunu başarılı bir şekilde yapılandırmak için ortamınızın IPv4 desteklemesi gerekir. Ağ bulmayı Yerel bir IPv6 ortamında bir DHCP sunucusu kullanacak şekilde yapılandıramazsınız.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a>Ağ bulmayı yapılandırma  

Önce yalnızca ağ topolojinizi bulmak için aşağıdaki yordamları kullanın, ardından ağ bulmayı, kullanılabilir ağ bulma seçeneklerinden birini veya birkaçını kullanarak olası istemcileri bulmak üzere yapılandırın.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a>Ağ topolojinizi belirleme  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **bulma yöntemleri** düğümünü seçin.  

2. Ağ kaynaklarını bulmak istediğiniz site için **ağ bulma** yöntemini seçin.  

3. Şeridin **giriş** sekmesinde **Özellikler**' i seçin.  

    - **Genel** sekmesinde, **Ağ bulmayı etkinleştirme**seçeneğini belirleyin. Ardından **bulma seçenekleri türünden** **topoloji** ' yi seçin.  

    - **Alt ağlar** sekmesinde, **yerel alt ağları ara** seçeneğini belirleyin.  

      > [!TIP]  
      > Ağınızı oluşturan belirli alt ağları biliyorsanız, **yerel alt ağları ara** onay kutusunun işaretini kaldırın. Sonra **Yeni** simge ![ Yeni simgesini seçin ](media/Disc_new_Icon.gif) ve aramak istediğiniz belirli alt ağları ekleyin. Büyük ağlarda, ağ bant genişliği kullanımını en aza indirmek için tek seferde yalnızca bir veya iki alt ağ arayın.  

    - **Etki alanları** sekmesinde, **yerel etki alanı arama**seçeneğini belirleyin.  

    - **SNMP** sekmesinde, **en fazla atlama** açılan listesinden bir seçenek belirleyin. Bu seçenek, ağ bulma 'nın topolojinizi eşlerken kaç yönlendirici atlama yapabileceğini belirtir.  

      > [!TIP]  
      > Ağ topolojinizi ilk kez eşlediğinizde, ağ bant genişliği kullanımını en aza indirmek için yalnızca birkaç yönlendirici atlaması yapılandırın.  

4. **Zamanlama** sekmesinde **Yeni** simge ![ Yeni simgesini seçin ](media/Disc_new_Icon.gif) ve bulma işlemini çalıştırmak için bir zamanlama ayarlayın.  

    > [!NOTE]  
    > Ayrı ağ bulma zamanlamalarına farklı bir keşif yapılandırması atayamazsınız. Ağ bulma her çalıştığında, geçerli bulma yapılandırmasını kullanır.  

5. Konfigürasyonları kabul etmek için **Tamam ' ı** seçin. Ağ bulma zamanlanan saatte çalışır.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a>Ağ bulmayı yapılandırma  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **bulma yöntemleri** düğümünü seçin.  

2. Ağ kaynaklarını bulmak istediğiniz site için **ağ bulma** yöntemini seçin.  

3. Şeridin **giriş** sekmesinde **Özellikler**' i seçin.  

4. **Genel** sekmesinde, **Ağ bulmayı etkinleştirme**seçeneğini belirleyin.  

    - **Bulma seçenekleri türünden** , çalıştırmak istediğiniz bulma türü arasından seçim yapın.  

    - Düşük bant genişliğine sahip ağlarda otomatik ayarlamalar yapmak üzere Configuration Manager için **yavaş ağ** seçeneğini etkinleştirin.  

5. Alt ağları aramak üzere bulmayı yapılandırmak için **alt ağlar** sekmesine geçin. Sonra aşağıdaki seçeneklerden birini veya birkaçını yapılandırın:  

    - Bulmayı çalıştıran bilgisayarda yerel olan alt ağlarda bulmayı çalıştırmak için **yerel alt ağları arama**seçeneğini etkinleştirin.  

    - Belirli bir alt ağı aramak için alt ağın **Aranacak alt ağlarda** listelendiğinden ve **arama** değerinin **etkin**olduğundan emin olun:  

      1. Alt ağ listelenmiyorsa **Yeni** simge ![ Yeni simgesini seçin ](media/Disc_new_Icon.gif) . **Yeni alt ağ ataması** iletişim kutusunda, **alt ağ** ve **maske** bilgilerini girin ve ardından **Tamam**' ı seçin. Varsayılan olarak, arama için yeni bir alt ağ etkinleştirilmiştir.  

      2. Listelenen alt ağın **arama** değerini değiştirmek için listeden seçin. Sonra **Değiştir** simgesini seçerek değeri **devre dışı** ve **etkin**arasında değiştirin.  

6. Bulma işlemini etki alanlarını arayacak şekilde yapılandırmak için, **etki alanları** sekmesine geçin. Sonra aşağıdaki seçeneklerden birini veya birkaçını yapılandırın:  

    - Bulmayı çalıştıran bilgisayarın etki alanında bulmayı çalıştırmak için **yerel etki alanı arama**seçeneğini etkinleştirin.  

    - Belirli bir etki alanını aramak için, etki **alanının etki alanında listelendiğinden ve bir** **arama** değerinin **etkin**olduğundan emin olun:  

      1. Etki alanı listede yoksa **Yeni** simge ![ Yeni simgesini seçin ](media/Disc_new_Icon.gif) . **Etki alanı özellikleri** iletişim kutusunda, **etki alanı** bilgilerini girin ve ardından **Tamam**' ı seçin. Varsayılan olarak, arama için yeni bir etki alanı etkinleştirilmiştir.  

      2. Listelenen bir etki alanının **arama** değerini değiştirmek için listeden seçin. Sonra **Değiştir** simgesini seçerek değeri **devre dışı** ve **etkin**arasında değiştirin.  

7. Bulma 'yı SNMP cihazları için belirli SNMP topluluk adlarını arayacak şekilde yapılandırmak için **SNMP** sekmesine geçin. Sonra aşağıdaki seçeneklerden birini veya birkaçını yapılandırın:  

    - SNMP topluluk **adları**listesine SNMP topluluk adı eklemek için **Yeni** simge yeni simgesini seçin ![ ](media/Disc_new_Icon.gif) . **Yenı SNMP topluluk adı** iletişim kutusunda, SNMP topluluğunun **adını** belirtin ve ardından **Tamam**' ı seçin.  

    - SNMP topluluk adını kaldırmak için topluluk adını seçin ve **sonra simgeyi Sil simgesini Sil** simgesini seçin ![ ](media/Disc_delete_Icon.gif) .  

    - SNMP topluluk adlarının arama sırasını ayarlamak için listeden bir topluluk adı seçin. Sonra **öğeyi yukarı** Taşı simgesini ![ ](media/Disc_moveUp_Icon.gif) veya **öğeyi aşağı** Taşı simgesini seçin simge aşağı taşı simgesi ![ ](media/Disc_moveDown_Icon.gif) . Bulma çalıştığında, topluluk adları yukarıdan aşağıya doğru bir düzende aranır. 

    - SNMP aramaları tarafından kullanılmak üzere en fazla yönlendirici atlama sayısını yapılandırmak için, **en fazla atlama** sayısı açılan listesinden atlama sayısını seçin.  

8. SNMP cihazını yapılandırmak için **SNMP cihazları** sekmesine geçin. Cihaz listede yoksa **Yeni** simge ![ Yeni simgesini seçin ](media/Disc_new_Icon.gif) . **Yenı SNMP aygıtı** ILETIŞIM kutusunda SNMP cihazının IP adresini veya cihaz adını belirtin ve ardından **Tamam**' ı seçin.  

    > [!NOTE]  
    > Bir cihaz adı belirtirseniz, Configuration Manager NetBIOS adını bir IP adresine çözümleyebilmelidir.  

9. Bulmayı belirli DHCP sunucularını sorgulamak üzere yapılandırmak için **DHCP** sekmesine geçin. Sonra aşağıdaki seçeneklerden birini veya birkaçını yapılandırın:  

    - Bulma işlemini çalıştıran bilgisayardaki DHCP sunucusunu sorgulamak için, **site sunucusunun DHCP sunucusunu her zaman kullanma**seçeneğini etkinleştirin.  

      > [!NOTE]  
      > Bu seçeneği kullanmak için sunucu bir DHCP sunucusundan IP adresini kiramalıdır ve statik bir IP adresi kullanamaz.  

    - Belirli bir DHCP sunucusunu sorgulamak için **Yeni** simge ![ Yeni simgesini seçin ](media/Disc_new_Icon.gif) . **Yenı DHCP sunucusu** iletişim kutusunda, DHCP sunucusunun IP adresini veya sunucu adını belirtin ve ardından **Tamam**' ı seçin.  

      > [!NOTE]  
      > Bir sunucu adı belirtirseniz, Configuration Manager NetBIOS adını bir IP adresine çözümleyebilmelidir.  

10. Bulmanın ne zaman çalışacağını yapılandırmak için **zamanlama** sekmesine geçin. Sonra, **New** ![ ](media/Disc_new_Icon.gif) Ağ bulmayı çalıştırmaya yönelik bir zamanlama ayarlamak için yeni simge yeni simgesini seçin. Birden çok yinelenen zamanlamayı ve tekrarsız birden çok zamanlamayı yapılandırabilirsiniz.  

    > [!NOTE]  
    > **Zamanlama** sekmesi aynı anda birden fazla zamanlama gösteriyorsa, ağ bulma işlemi zamanlamada belirtilen sürede yapılandırıldığı sırada tüm zamanlamalar için çalışır. Bu davranış yinelenen zamanlamalar için de geçerlidir.  

11. Yapılandırmalarınızı kaydetmek için **Tamam ' ı** seçin.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a>Ağ bulmanın tamamlandığını doğrulama  

Ağ bulmanın tamamlaması gereken süre, aşağıdaki faktörlerden birine veya daha fazlasına bağlı olarak değişebilir:  

- Ağınızın boyutu  

- Ağınızın topolojisi  

- Ağdaki yönlendiricileri bulmak için yapılandırılmış en fazla atlama sayısı  

- Çalıştırılmakta olan bulma türü  

Ağ bulma tamamlandığında sizi uyarmak için ileti oluşturmaz. Bulmanın ne zaman tamamlandığını doğrulamak için aşağıdaki yordamı kullanın:  

1. Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Sistem durumu**' nu genişletin ve ardından **durum iletisi sorguları** düğümünü seçin.  

2. **Tüm durum iletileri** sorgusunu seçin.  

3. Şeridin **giriş** sekmesinde, **durum Iletisi sorguları** grubunda **iletileri göster**' i seçin.  

4. Tüm durum Iletileri penceresinde, bulmanın ne kadar süre önce başlatıldığını içeren **Tarih ve saat** açılan listesinden bir değer seçin. Ardından **Tamam** ' ı seçerek **Configuration Manager durum iletisi görüntüleyicisini**açın.  

    > [!TIP]  
    > Ayrıca, bulmayı çalıştırdığınız belirli bir tarih ve saati seçmek için **Tarih ve saat belirt** seçeneğini de kullanabilirsiniz. Bu seçenek, belirli bir tarihte ağ bulmayı çalıştırdığınızda ve yalnızca bu tarihten itibaren iletileri almak istediğinizde yararlıdır.  

5. Ağ bulmanın tamamlandığını doğrulamak için, aşağıdaki ayrıntılara sahip olan bir durum iletisi arayın:  

    - İleti KIMLIĞI: **502**  

    - Bileşen: **SMS_NETWORK_DISCOVERY**  

    - Açıklama: **Bu bileşen durduruldu**  

    Bu durum iletisi yoksa, ağ bulma bitmedi.  

6. Ağ bulmanın ne zaman başlatıldığını doğrulamak için, aşağıdaki ayrıntılara sahip bir durum iletisi arayın:  

    - İleti KIMLIĞI: **500**  

    - Bileşen: **SMS_NETWORK_DISCOVERY**  

    - Açıklama: **Bu bileşen başlatıldı**  

    Bu bilgiler ağ bulmanın başlatıldığını doğrular. Bu bilgiler yoksa, ağ bulmayı yeniden zamanlayın.  
