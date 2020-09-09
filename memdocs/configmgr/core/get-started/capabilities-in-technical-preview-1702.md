---
title: Technical Preview 1702 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1702 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e9fa71060b8125b7d0872a40d197f1c423217bad
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607939"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Configuration Manager için Technical Preview 1702 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1702 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Configuration Manager konsolundan geri bildirim gönderin

Bu önizleme Configuration Manager konsolundaki yeni geri bildirim seçeneklerini tanıtır. Geri bildirim seçenekleri, Configuration Manager UserVoice geri bildirim Web sitesinin yoluyla doğrudan geliştirme ekibine geri bildirim göndermenizi sağlar.  

> **Geri bildirim** seçeneğini bulabilirsiniz:
> -  Şeritte, her bir düğümün Giriş sekmesinin en solundaki.  
>    ![Şeridi](./media/feedback-home.png)

-  Konsolda herhangi bir nesneye sağ tıkladığınızda.   
    ![Righ-tıklama seçeneği](./media/feedback-option.png)   

**Geri bildirim** seçilirse, tarayıcınızda Configuration Manager UserVoice geri bildirim Web sitesine açılır https://configurationmanager.uservoice.com/forums/300492-ideas .
##  <a name="changes-for-updates-and-servicing"></a>Güncelleştirmeler ve bakım için değişiklikler
Aşağıda bu önizleme ile birlikte sunulmuştur.

**Daha basit güncelleştirme seçimleri**  
Altyapınızda iki veya daha fazla güncelleştirme için bir sonraki sefer, yalnızca en son güncelleştirme indirilir. Örneğin, geçerli site sürümünüz mevcut en son sürümden iki veya daha eski ise, yalnızca en son güncelleştirme sürümü otomatik olarak indirilir.  

En güncel sürüm olmasa bile, diğer kullanılabilir güncelleştirmeleri indirme ve yükleme seçeneğiniz vardır. Ancak, güncelleştirmenin daha yeni bir sürümle değiştirildiğini belirten bir uyarı alırsınız. *İndirileceği*bir güncelleştirmeyi indirmek için, konsolda güncelleştirmeyi seçin ve ardından **İndir**' e tıklayın.

**Eski güncelleştirmeler için geliştirilmiş Temizleme**   
Site sunucunuzdaki ' EasySetupPayload ' klasöründen gereksiz İndirmeleri silen bir otomatik temizleme işlevi ekledik.  


## <a name="peer-cache-improvements"></a>Eş önbellek geliştirmeleri
Bu sürümden itibaren, eş önbellek kaynak bilgisayarı aşağıdaki koşullardan herhangi birini karşıladığında, eş önbellek kaynak bilgisayar bir içerik isteğini reddeder:  
-  Düşük pil modunda.
-  CPU yükü, içerik istenen zamanda %80 ' ü aşıyor.
-  Disk g/ç, 10 ' u aşan bir *Avgdiskqueuelength* öğesine sahiptir.
-  Bilgisayar için kullanılabilir başka bağlantı yok.   

Bu ayarları, Configuration Manager SDK kullandığınızda eş kaynak özelliği (*SMS_WinPEPeerCacheConfig*) için istemci Aracısı yapılandırma sınıfını kullanarak yapılandırabilirsiniz.

Bilgisayar, içerik için bir isteği reddettiğinde, istenen bilgisayar, kullanılabilir içerik kaynağı konumları havuzundaki içerik formu alternatif kaynaklarını göstermeye devam eder.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a> Cihazları, kullanıcıları ve grupları yönetmek için Azure Active Directory Domain Services kullanma

Bu Technical Preview sürümüyle Azure Active Directory (AD) etki alanı Hizmetleri tarafından yönetilen bir etki alanına katılmış cihazları yönetebilirsiniz. Ayrıca, bu etki alanındaki cihazları, kullanıcıları ve grupları çeşitli Configuration Manager bulma yöntemleriyle de bulabilirsiniz.

Technical Preview site altyapısının, istemcilerinin ve Azure AD Domain Services etki alanının tümünün Azure 'da çalışması gerekir.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Azure AD 'yi kullanmak için Configuration Manager ayarlama
Azure AD 'yi Configuration Manager kullanmak için şunlar gerekir:
- Azure aboneliği.
- Etki alanı Hizmetleri (DS) ile Azure AD.
- Azure AD 'nize katılmış bir Azure VM üzerinde çalışan bir Configuration Manager sitesi.
- Aynı Azure AD ortamında çalışan istemcileri Configuration Manager.

Azure AD etki alanı hizmetini yapılandırmak için bkz. [Azure AD Domain Services kullanmaya başlama](/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Kaynak bulma
Azure AD 'de çalışacak Configuration Manager ayarladıktan sonra, Azure AD 'yi kaynaklar için aramak üzere aşağıdaki Active Directory bulma yöntemlerini kullanabilirsiniz:  
- Active Directory Sistem Saptama
- Active Directory Kullanıcı Saptama
- Active Directory Grup Saptama  

Kullandığınız her yöntem için, LDAP sorgusunu, şirket içi Active Directory için normal olan kapsayıcılar yerine Azure AD OU yapılarını arayacak şekilde düzenleyin. Bunun yapılması, Azure aboneliğinizde Active Directory aramak için sorguyu yönlendirmelidir.  

Aşağıdaki örneklerde bir Azure AD *contoso.onmicrosoft.com*kullanılmaktadır:
- **Sistem bulma**   
  Azure AD, cihazları **Aaddc bilgisayarları** OU 'su altına depolar.  Aşağıdakini yapılandırın:  
  - *LDAP: Vou = AADDC Computers, DC = contoso, DC = onmicrosoft, DC = com*  


- **Kullanıcı keşfi** AAD kullanıcıları **Aaddc kullanıcıları** OU 'su altında depolar.  Aşağıdakini yapılandırın:
  - *LDAP: Vou = AADDC kullanıcıları, DC = contoso, DC = onmicrosoft, DC = com*


- **Grup keşfi**  
Azure AD 'nin grupları depolayan bir OU 'su yok. Bunun yerine, sistem veya Kullanıcı sorgularıyla aynı genel yapıyı kullanın ve LDAP sorgusunu, bulmayı istediğiniz grupları içeren OU 'ya işaret etmek üzere yapılandırın.

Azure AD hakkında daha fazla bilgi için aşağıdakilere bakın:  
- Azure.microsoft.com üzerinde [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) .
- Docs.microsoft.com hakkındaki [belgeleri Active Directory Domain Services](/azure/active-directory-domain-services) .

## <a name="conditional-access-device-compliance-policy-improvements"></a>Koşullu erişim cihaz uyumluluk ilkesi geliştirmeleri

Kullanıcılar uyumlu olmayan uygulamalar listesinin parçası olan uygulamaları kullanırken koşullu erişimi destekleyen kurumsal kaynaklara erişimi engellemenize yardımcı olacak yeni bir cihaz uyumluluk ilkesi kuralı kullanılabilir. Uyumlu olmayan uygulamalar listesi, **yüklenemeyen**yeni uyumlu kural uygulamaları eklenirken yönetici tarafından tanımlanabilir. Bu kural, bir uygulamayı uyumlu olmayan listesine eklerken yöneticinin **uygulama adını**, **uygulama kimliğini**ve **uygulama yayımcısını** (isteğe bağlı) girmesini gerektirir. Bu ayar yalnızca iOS ve Android cihazlar için geçerlidir.

Ayrıca, kuruluşların güvenli olmayan uygulamalar aracılığıyla veri sızıntısını azaltmasına ve belirli uygulamalarda aşırı veri tüketimini engellemesine yardımcı olur.

### <a name="try-it-out"></a>Deneyin

**Senaryo:** Şirket verilerini şirketiniz dışına göndererek veya aşırı veri tüketimine neden olan, bu uygulamaları uyumlu olmayan uygulamalar listesine ekleyen [bir koşullu erişim cihaz uyumluluk ilkesi oluşturarak](../../mdm/understand/what-happened-to-hybrid.md) veri sızıntıya neden olabilecek uygulamaları belirleyebilirsiniz. Bu, Kullanıcı engellenen uygulamayı kaldıraana kadar koşullu erişimi destekleyen kurumsal kaynaklara erişimi engeller.

## <a name="antimalware-client-version-alert"></a>Kötü amaçlı yazılımdan koruma istemcisi sürüm uyarısı
Bu önizleme sürümünden itibaren, yönetilen istemcilerin %20 ' den fazla (varsayılan) kötü amaçlı yazılımdan koruma istemcisinin (örn. Windows Defender veya Endpoint Protection istemcisi) kullanım dışı bir sürümünü kullanıyorsa Configuration Manager Endpoint Protection bir uyarı verir.

### <a name="try-it-out"></a>Deneyin
İstemci ayarları ilkesini kullanarak tüm masaüstü ve sunucu istemcilerinde Endpoint Protection etkinleştirildiğinden emin olun. Artık, bir **kötü amaçlı yazılımdan koruma istemci sürümü** ve **Endpoint Protection dağıtım durumunu** **varlıklar ve uyumluluk**  >  **genel bakış**  >  **cihazlarından**,  >  **tüm masaüstü bilgisayarlar ve istemcileri**sunarak görüntüleyebilirsiniz. Bir uyarıyı denetlemek için **izleme** çalışma alanındaki **uyarıları** görüntüleyin. Yönetilen istemcilerin %20 ' si bir kötü amaçlı yazılımdan koruma yazılımının süresi dolmuşsa, kötü amaçlı yazılımdan koruma istemcisi sürümü güncel değildir. Bu uyarı, **izleme**  >  **genel bakış** sekmesinde görünmez. Zaman aşımına uğradı istemcileri güncelleştirmek için kötü amaçlı yazılımdan koruma istemcileri için yazılım güncelleştirmelerini etkinleştirin.

Uyarının oluşturulduğu yüzdeyi yapılandırmak için, **izleme**  >  **uyarıları**  >  **tüm uyarılar**' ı genişletin, **kötü amaçlı yazılımdan koruma istemcileri güncel** değil ' e çift tıklayın ve **bir kötü amaçlı yazılımdan koruma istemcisinin güncel olmayan sürümüne sahip yönetilen istemcilerin yüzdesi seçeneğinden fazla olursa oluştur uyarısını** değiştirin.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Iş güncelleştirmeleri için Windows Update uyumluluk değerlendirmesi
Artık bir uyumluluk ilkesi güncelleştirme kuralını, koşullu erişim değerlendirmesinin bir parçası olarak Iş değerlendirmesi sonucu için bir Windows Update içerecek şekilde yapılandırabilirsiniz.
> [!IMPORTANT]
> Windows Update Iş güncelleştirmelerine yönelik uyumluluk değerlendirmesi kullanmak için Windows 10 Insider Preview derleme 15019 veya sonraki bir sürüme sahip olmanız gerekir.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Iş Windows Update Windows 10 güncelleştirmelerini yönetmesine izin ver
Windows Update Iş güncelleştirmelerine yönelik uyumluluk değerlendirmesi bilgilerini toplamak için, istemci Aracısı ayarını Iş Windows Update Windows 10 güncelleştirmelerini yönetmeye açıkça izin verecek şekilde yapılandırmak için aşağıdaki yordamı kullanın.
1. Configuration Manager konsolunda, **Yönetim**  >  **istemci ayarları**' na gidin.
2. İstemci ayarları için Özellikler ' de **yazılım güncelleştirmeleri**' ne gidin ve **Iş için Windows Update Windows 10 güncelleştirmelerini Yönet** ' i seçerek **Evet** ' i seçin.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Iş değerlendirmesi Windows Update için bir uyumluluk ilkesi oluşturma
1. Configuration Manager konsolunda **varlıklar ve uyum**  >  **Uyumluluk ayarları**  >  **uyumluluk ilkeleri**' ne gidin.
2. **Uyumluluk Ilkesi oluştur** ' a tıklayın veya değiştirmek üzere var olan bir uyumluluk ilkesi seçin.
3. Genel sayfasında, bir ad ve açıklama girin, **Configuration Manager istemcisiyle yönetilen cihazlar Için Uyumluluk kuralları**' nı seçin, raporlama için uyumsuzluk önem derecesini ayarlayın ve **İleri**' ye tıklayın.
4. Desteklenen Platformlar sayfasında **Windows 10**' u seçin ve ardından **İleri**' ye tıklayın.
5. Kurallar sayfasında, **yeni....** öğesine tıklayın ve ardından **koşul** için **Windows Update gerektir**' i seçin. **Değer** ayarı otomatik olarak **doğru**olarak ayarlanır.

Yeni ilke, **Varlıklar ve Uyum** çalışma alanının **Uyumluluk İlkeleri** düğümünde görüntülenir.

### <a name="deploy-a-compliance-policy"></a>Uyumluluk ilkesini dağıtma
1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**  >  **uyumluluğu ayarları**' na gidin ve ardından **uyumluluk ilkeleri**' ne tıklayın.
2. **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıt**'a tıklayın.
3. **Uyumluluk İlkesini Dağıt** iletişim kutusunda, ilkenin dağıtılacağı kullanıcı koleksiyonunu seçmek için **Gözat**’a tıklayın.
   Ek olarak, ilke uyumlu olmadığı taktirde uyarı oluşturma seçeneklerini ve ayrıca bu ilkenin uyumluluk değerlendirmesinde kullanılacak zamanlamayı yapılandırma seçeneklerini de belirleyebilirsiniz.
4. Bitirdiğinizde, **Tamam**’a tıklayın.

### <a name="monitor-the-compliance-policy"></a>Uyumluluk ilkesini izleme
Uyumluluk ilkesini oluşturduktan sonra, Configuration Manager konsolundaki uyumluluk sonuçlarını izleyebilirsiniz. Ayrıntılar için bkz. [Uyumluluk Ilkesini izleme](../../mdm/understand/what-happened-to-hybrid.md).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Yüksek etkili görev dizileri için yazılım merkezi ayarları ve bildirim iletileri geliştirmeleri
Bu sürüm, yüksek etki dağıtım görev dizileri için yazılım merkezi ayarları ve bildirim iletilerine yönelik aşağıdaki geliştirmeleri içerir:

- Görev dizisinin özelliklerinde, artık, işletim sistemi olmayan görev dizileri dahil olmak üzere, yüksek riskli dağıtım olarak herhangi bir görev dizisini yapılandırabilirsiniz. Belirli koşullara uyan herhangi bir görev dizisi otomatik olarak yüksek etki olarak tanımlanır. Ayrıntılar için bkz. [yüksek riskli dağıtımları yönetme](../servers/manage/settings-to-manage-high-risk-deployments.md).
- Görev dizisinin özelliklerinde, varsayılan bildirim iletisini kullanmayı veya yüksek etkili dağıtımlar için kendi özel bildirim iletinizi oluşturmayı seçebilirsiniz.
- Görev dizisinin özelliklerinde, bir yeniden başlatma gerekiyor, görev dizisinin indirme boyutu ve tahmini çalışma süresi dahil olmak üzere yazılım merkezi özelliklerini yapılandırabilirsiniz.
- Yerinde yükseltmeler için varsayılan yüksek etki dağıtım iletisi artık uygulamalarınızın, verilerinizin ve ayarlarınızın otomatik olarak geçirildiğini belirtir. Daha önce, herhangi bir işletim sistemi yüklemesi için varsayılan ileti, tüm uygulamaların, verilerin ve ayarların yerinde yükseltme için doğru olmayan kayıp olduğunu gösterdi.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Bir görev dizisini yüksek etkili bir görev dizisi olarak ayarlama
Bir görev dizisini yüksek etki olarak ayarlamak için aşağıdaki yordamı kullanın.
> [!NOTE]
> Belirli koşullara uyan herhangi bir görev dizisi otomatik olarak yüksek etki olarak tanımlanır. Ayrıntılar için bkz. [yüksek riskli dağıtımları yönetme](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **işletim sistemleri**  >  **görev dizileri**' ne gidin.
2. Düzenlenecek görev sırasını seçin ve **Özellikler**' e tıklayın.
3. **Kullanıcı bildirimi** sekmesinde, **Bu bir üst etki görevi sırası**seçin.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Yüksek riskli dağıtımlar için özel bildirim oluşturma
1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **işletim sistemleri**  >  **görev dizileri**' ne gidin.
2. Düzenlenecek görev sırasını seçin ve **Özellikler**' e tıklayın.
3. **Kullanıcı bildirimi** sekmesinde **özel metin kullan**' ı seçin.
   > [!NOTE]
   >  Kullanıcı bildirim metnini yalnızca **Bu yüksek etki düzeyi olan bir görev sırası** seçildiğinde ayarlayabilirsiniz.

4. Aşağıdaki ayarları yapılandırın (her metin kutusu için en fazla 255 karakter):

   **Kullanıcı bildirimi başlık metni**: Software Center Kullanıcı bildiriminde görüntülenen mavi metni belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölümde "Bu bilgisayardaki işletim sistemini yükseltmek istediğinizi onaylayın" gibi bir şey bulunur.

   **Kullanıcı bildirim iletisi metni**: özel bildirimin gövdesini sağlayan üç metin kutusu vardır.
   - 1. metin kutusu: genellikle kullanıcı için yönergeleri içeren metnin ana gövdesini belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölümde "işletim sistemini yükseltme süresi sürer ve bilgisayarınız birkaç kez yeniden başlatılabilir" gibi bir şey bulunur.
   - 2. metin kutusu: metnin ana gövdesinde kalın metni belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölümde "yerinde yükseltme yeni işletim sistemini yükleme ve uygulamalarınızı, verilerinizi ve ayarlarınızı otomatik olarak geçirir" gibi bir şeyler bulunur.
   - 3. metin kutusu: kalın metin altında metnin son satırını belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölüm "başlamak için yüklensin ' e tıklayın. Aksi takdirde Iptal ' e tıklayın. "   

   Özelliklerde aşağıdaki özel bildirimi yapılandıracaksınız.

   ![Görev sırası özellikleri için özel bildirim](./media/user-notification.png)

   Son Kullanıcı yükleme yazılımını Software Center 'dan açtığında aşağıdaki bildirim iletisi görüntülenir.

   ![Bir görev dizisi için özel bildirim-yazılım merkezi](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Yazılım Merkezi özelliklerini yapılandırma
Yazılım Merkezi 'nde görünen görev dizisinin ayrıntılarını yapılandırmak için aşağıdaki yordamı kullanın. Bu ayrıntılar yalnızca bilgi amaçlıdır.  
1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **işletim sistemleri**  >  **görev dizileri**' ne gidin.
2. Düzenlenecek görev sırasını seçin ve **Özellikler**' e tıklayın.
3. **Genel** sekmesinde, yazılım merkezi için aşağıdaki ayarlar kullanılabilir:
   - **Yeniden başlatma gerekli**: kullanıcının yükleme sırasında yeniden başlatma gerekip gerekmediğini bilmesini sağlar.
   - **İndirme boyutu (MB)**: görev sırası Için yazılım merkezi 'nde kaç megabayt görüntülendiğini belirtir.  
   - **Tahmini çalışma süresi (dakika)**: görev sırası Için yazılım merkezi 'nde görüntülenen tahmini çalışma süresini dakika cinsinden belirtir.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Bir uygulamayı yüklemeden önce yürütülebilir dosyaları çalıştırmaya yönelik denetim

*\<deployment type name>* Dağıtım türünün **Özellikler** Iletişim kutusunda, yükleme davranışı sekmesinde artık, çalışıyorsa dağıtım türünün yüklenmesini engelleyebilen daha fazla yürütülebilir dosyadan birini belirtebilirsiniz. Dağıtım türünün yüklenebilmesi için kullanıcının çalışan yürütülebilir dosyayı kapatması (veya gerekli amacına sahip dağıtımlar için otomatik olarak kapatılabilir) gerekir.

### <a name="try-it-out"></a>Deneyin.

1. Configuration Manager dağıtım türünün özelliklerinde, **davranışı yüklensin** sekmesini seçin.
2. Denetlemek istediğiniz bir veya daha fazla yürütülebilir dosya adı eklemek için **Ekle** ' yi seçin. Ayrıca, kullanıcıların listedeki uygulamaları belirlemesini kolaylaştırmak için bir görünen ad ekleyebilirsiniz.
3. Dağıtım için gerekli bir amaç varsa, yazılım dağıtma sihirbazında, isteğe bağlı **olarak, dağıtım türü özellikleri iletişim kutusunun Kurulum davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapatmayı**seçebilirsiniz.

Uygulama **kullanılabilir**olarak dağıtılmışsa ve Son Kullanıcı uygulamayı yüklemeye çalışırsa, yüklemeye devam edebilmek için önce belirttiğiniz çalışan yürütülebilir dosyaları kapatmaları istenir.

Uygulama **gerekli**olarak dağıtılmışsa ve **dağıtım türü özellikleri iletişim kutusunun yükleme davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapat** seçeneği işaretliyse, uygulama yükleme son tarihine ulaşıldığında belirttiğiniz yürütülebilir dosyaların otomatik olarak kapatıldığını bildiren bir iletişim kutusu görür. Bu iletişim kutularını **istemci ayarları**  >  **bilgisayar aracısında**zamanlayabilirsiniz. Son kullanıcının bu iletileri görmesini istemiyorsanız, **Yazılım Merkezi 'Nde Gizle** ' yi ve dağıtımın özelliklerinin **Kullanıcı deneyimi** sekmesindeki tüm bildirimler ' i seçin.

Uygulama **gerekli** olarak dağıtılmışsa ve **dağıtım türü özellikleri iletişim kutusunun yükleme davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapat** seçeneği seçili değilse, belirtilen uygulamalardan bir veya daha fazlası çalışıyorsa uygulamanın yüklenmesi başarısız olur.

## <a name="create-pfx-certificates-with-s-mime-support"></a>S MIME desteğiyle PFX sertifikaları oluşturma

Artık, S/MIME destekleyen bir PFX Sertifika profili oluşturabilir ve bunları kullanıcılara dağıtabilirsiniz.  Bu sertifika daha sonra, kullanıcının kaydolduğu cihazlarda S/MIME şifreleme ve şifre çözme işlemleri için kullanılabilir.

Ayrıca, artık birden fazla sertifika kayıt noktası site sistemi rolü üzerinde birden fazla sertifika yetkilisi (CA) belirtebilir ve ardından hangi CA 'Ların istekleri sertifika profilinin bir parçası olarak işleyeceğini atayabilirsiniz.

İOS cihazları için bir PFX sertifika profilini bir e-posta profiliyle ilişkilendirebilir ve S/MIME şifrelemesini etkinleştirebilirsiniz.  Böylece, iOS üzerinde yerel e-posta istemcisinde S/MIME etkinleştirilir ve doğru S/MIME şifreleme sertifikasını bu sertifikayla ilişkilendirir.

Configuration Manager sertifikalar hakkında daha fazla bilgi için bkz. [sertifika profillerine giriş]( /sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>İOS cihazları için yeni uyumluluk ayarları

İOS cihazları için yapılandırma öğelerinde kullanabileceğiniz yeni ayarlar ekledik. Bunlar, bir tek başına yapılandırmada Microsoft Intune daha önce var olan ve Intune 'U Configuration Manager ile kullandığınızda kullanılabilir olan ayarlardır. Bu ayarlardan herhangi biriyle ilgili yardıma ihtiyacınız varsa bkz. [Microsoft Intune iOS ilke ayarları](../../../intune/configuration/device-restrictions-ios.md).

- **Yönetilen uygulamalardan iCloud 'a veri eşitleme**
- **Diğer cihazdaki etkinliklere devam etmek için iletim**
- **iCloud Fotoğraf paylaşma**
- **iCloud Fotoğraf Kitaplığı**
- **Yeni kurumsal uygulama yazarlarına güven**
- **Kullanıcının iBook mağazasından ' Erotika ' olarak işaretlenmiş içerik Indirmesine Izin ver** (yalnızca denetimli mod)
- **Eşleştirilmiş Apple Watch’ları bilek algılama kullanmaya zorla**
- **AirPlay giden istekleri için parola**
- **Hesap ayarlarını değiştirme** (yalnızca denetimli mod)
- **Uygulama hücresel veri kullanımı ayarlarında yapılan değişiklikler** (yalnızca denetimli mod)
- **Tüm içerik ve ayarları sil** (yalnızca denetimli mod)
- **Cihaz kısıtlamalarını yapılandırma** (yalnızca denetimli mod)
- **İOS cihazının eşleştirilebileceği cihazları denetlemek için konak eşleştirmesini kullanın** (yalnızca denetimli mod)
- **Yapılandırma profillerini ve sertifikaları** (yalnızca denetimli mod) yükler
- **Cihaz adı değişikliği** (yalnızca denetimli mod)
- **Geçiş kodu değişikliği** (yalnızca denetimli mod)
- **Apple Watch eşleştirme** (yalnızca denetimli mod)
- **Bildirim ayarlarının değiştirilmesi** (yalnızca denetimli mod)
- **Duvar kağıdı değişikliği** (yalnızca denetimli mod)
- **Tanılama gönderme ayarlarının değiştirilmesi** (yalnızca denetimli mod)
- **Bluetooth değişikliği** (yalnızca denetimli mod)
- **AirDrop** (yalnızca denetimli mod)
- **Siri kullanarak Kullanıcı tarafından oluşturulan Içeriği Internet 'ten sorgulama** (yalnızca denetimli mod)
- **Siri küfür filtresi** (yalnızca denetimli mod)
- **Spotlight aramasında Internet 'ten sonuç Döndür** (yalnızca denetimli mod)
- **Sözcük tanımı arama** (yalnızca denetimli mod)
- Tahmine **dayalı klavyeler** (yalnızca denetimli mod)
- **Otomatik Düzeltme** (yalnızca denetimli mod)
- **Klavye yazım denetimi** (yalnızca denetimli mod)
- **Klavye kısayolları** (yalnızca denetimli mod)
  <!--- - **Enterprise app trust settings modification** --->
- **Yalnızca Apple Configurator ve iTunes kullanarak uygulama yükleme** (yalnızca denetimli mod)
- **Otomatik uygulama indirmeleri** (yalnızca denetimli mod)
- **Arkadaşlarımı bul uygulama ayarlarında değişiklik yap** (yalnızca denetimli mod)
- **IBOOKS Store 'A erişim** (yalnızca denetimli mod)
- **Mesajlar uygulaması** (yalnızca denetimli mod)
- **Pod yayınları** (yalnızca denetimli mod)
- **Apple Music** (yalnızca denetimli mod)
- **ITunes Radio** (yalnızca denetimli mod)
- **Apple News** (yalnızca denetimli mod)
- **Game Center** (yalnızca denetimli mod)
- **AirDrop 'u yönetilmeyen hedef olarak değerlendir**

## <a name="android-for-work-support"></a>Android for Work desteği

Technical Preview sürüm 1702 ' den başlayarak, hibrit MDM kiracınıza bir Google hesabı bağlayabilirsiniz. Bu, aşağıdakileri yapmanıza olanak sağlar:

- [Desteklenen Android cihazlarını](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) Android for Work olarak kaydetme, bu kayıtlı cihazlarda iş profilleri oluşturma
- Yürüt for Work Store 'da uygulamaları onaylayın, Configuration Manager konsolu ile eşitleyin ve cihazların iş profillerine dağıtın
- Bu cihazların iş profilini ve parola ayarlarını yapılandırmak için yapılandırma öğeleri oluşturun ve dağıtın
- Android cihazlarda zaten yaptığınız gibi, Android for Work cihazları için uyumluluk ilkesi öğeleri ve kaynak erişim profilleri oluşturma ve dağıtma
- Android for Work cihazlarında seçmeli Temizleme gerçekleştirme

Bir cihaz kaydettiğinizde, Android for Work, Intune 'un yönetebileceği cihazda bir iş profili oluşturur. Bu iş profili, Android cihazındaki kişisel profille yan yana bulunur. Kullanıcılar iş profili uygulamaları ve kişisel profil uygulamaları arasında kolayca geçiş yapabilir. Kişisel profildeki öğeleri yönetemezsiniz. Kişisel uygulamalar ve veriler yönetilmeden kalır. Configuration Manager, iş profili ve içeriği üzerinde tam denetime sahiptir ve cihazı cihazdan kaldırabilir.

Android for Work, Android 'den ayrı bir platformdur ve iş profillerini destekleyen Android cihazlarda hangi yönetim biçimini kullanacağınıza karar vermeniz gerekir.

### <a name="try-it-out"></a>Deneyin!
Aşağıdaki bölümlerde, Android for Work yönetimi açıklanır.

#### <a name="enable-android-for-work-management"></a>Android for Work yönetimini etkinleştir
1. https://accounts.google.com/SignUpBu Intune kiracının tüm Android for Work yönetim görevleriyle Ilişkilendirilecek Android for Work yönetici hesabınız olarak kullanmak üzere bir Google hesabı oluşturun. Bu, Android cihazlarını yöneten yöneticiler arasında paylaşılan bir Google hesabı olabilir. Bu, kuruluşunuzun Play for Work konsolunda uygulama yönetmek ve yayımlamak için kullandığı Google hesabıdır. Bu hesabı, Play for Work mağazasındaki uygulamaları onaylamak için kullanacaksınız, bu nedenle hesap adını ve parolayı takip edin.
2. Google hesabını Configuration Manager ' de yönetilen Intune kiracısına bağlayarak Android kaydını etkinleştirin:
   1. **Yönetime**  >  **genel bakış**  >  **Cloud Services**  >  **Microsoft Intune abonelikleri** ' ne gidin ve Intune aboneliğinizi seçin.
   2. Şeritte **platformları Yapılandır**  >  **Android** ' e tıklayın ve **Android kaydını etkinleştir** ' in işaretli olduğundan emin olun.
   3. Şeritte **platformları Yapılandır**  >  **Android for Work**' e tıklayın.
   4. İletişim kutusunda, **Intune konsolunda Android for Work yapılandırma**' ya tıklayın. Intune Konsolu Web tarayıcınızda açılır.
   5. Intune portalında oturum açmak için Intune yönetici kimlik bilgilerinizi kullanın.
   6. Google Play Android for Work Web sitesini açmak için **Yapılandır** ' a tıklayın.
   7. Google 'ın oturum açma sayfasında, 1. adımdaki Google hesabı kimlik bilgilerini girin ve ardından şirket bilgilerinizi sağlayın.
3. Intune portalına döndüğünüzde, Android for Work etkinleştirilir ve Android for Work cihazlar için üç kayıt seçenekleriniz vardır:
   - **Tüm cihazları Android olarak Yönet** -(devre dışı) Android for Work destekleyen cihazlar da dahil olmak üzere tüm Android cihazlar geleneksel Android cihazlar olarak kaydedilir
   - **Desteklenen cihazları Android for Work olarak yönet** - (Etkin) Android for Work destekleyen tüm cihazlar Android for Work cihazlar olarak kaydedilir. Android for Work desteklemeyen herhangi bir Android cihaz, geleneksel Android cihaz olarak kaydedilir.
   - **Yalnızca bu gruplardaki kullanıcılar için desteklenen cihazları Android for Work olarak Yönet** -(test), Android for Work yönetimini sınırlı bir kullanıcı kümesine hedeflemenizi sağlar. Yalnızca Android for Work destekleyen bir cihaz kaydeden seçili grupların üyeleri Android for Work cihazlar olarak kaydedilir. Diğerlerinin tümü Android cihaz olarak kaydedilir.
  
> [!NOTE]
> Bilinen bir sorun, **yalnızca bu gruplardaki kullanıcılar için desteklenen cihazların yönetilmesi Için Android for Work** seçeneğinin beklenen şekilde çalışmasını önler. Belirtilen Azure AD gruplarındaki kullanıcıların cihazları, Android for Work yerine Android olarak kaydedilecek. Android for Work 'u test etmek için **desteklenen tüm cihazları Android for Work olarak Yönet**' i kullanmanız gerekir.


  Android for Work kaydını etkinleştirmek için, en az iki seçenekten birini seçmeniz gerekir. **Yalnızca bu gruplardaki kullanıcılar için desteklenen cihazları Android for Work olarak Yönet** seçeneği için öncelikle Azure Active Directory güvenlik gruplarının ayarlanmış olması gerekir.

Bağlama tamamlandığında, Intune portalında hesap adı ve kuruluş adını görürsünüz; Bu noktada, her iki tarayıcıyı da kapatabilirsiniz.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Android for Work uygulamalarını onaylama ve dağıtma
Iş için Yürüt mağazasındaki uygulamaları onaylamak, Configuration Manager konsoluna eşitlemek ve bunları yönetilen Android for Work cihazlarına dağıtmak için aşağıdaki adımları izleyin. Uygulamaları kullanıcıların iş profillerine dağıtmak için, Play for Work içindeki uygulamaları onaylamanız ve ardından uygulamaları Configuration Manager konsolu ile eşitlemeniz gerekir.

1. Bir tarayıcı açın ve şuraya gidin: https://play.google.com/work .
2. Intune kiracınıza bağladınız Google Yönetici hesabını kullanarak oturum açın.
3. Ortamınızda dağıtmak istediğiniz uygulamalara gözatıp her biri için **Onayla** ' ya tıklayın.
4. Configuration Manager konsolunda, **Administrator**  >  **Overview**  >  **Cloud Services**  >  **Android for Work** Cloud Services yöneticiye genel bakış ' a gidin ve **Eşitle**' ye tıklayın.
5. Uygulamaların eşitlenmesi için en fazla 10 dakika bekleyin ve ardından **Software Library**  >  Mağaza uygulamaları için yazılım Kitaplığı **'na genel bakış**  >  **uygulama yönetimi**  >  **Lisans bilgileri**' ne gidin.
6. Çalışma için Yürüt ' den eşitlenen bir uygulamaya tıklayın ve ardından **uygulama oluştur**' a tıklayın.
7. Sihirbazı tamamlayıp **Kapat**' a tıklayın.
8. **Yazılım kitaplığı**'na  >  **genel bakış**  >  **uygulama yönetimi**  >  **uygulamalarına**gidin, bir Android for Work uygulaması seçin ve her zamanki gibi dağıtın.

Play for Work Apps 'i Configuration Manager ile eşitlemek için, Play for Work Web sitesinde en az bir uygulamayı onaylamanız gerekir.

#### <a name="enroll-an-android-for-work-device"></a>Android for Work cihazı kaydetme
Android for Work cihazlarını kaydetme işlemi, Android kaydına benzerdir. Mobil cihazınızda Android için Şirket Portalı uygulamasını indirin ve çalıştırın. Kayıt sürecinin bir parçası olarak bir iş profili oluşturmanız istenir.  İş profili oluşturulduktan sonra, Şirket Portalı yönetilen sürümüne geçmeniz gerekir. Yönetilen Şirket Portalı, sağ alt köşedeki küçük turuncu bir evrak çantası ile etiketlenir.

#### <a name="create-and-deploy-a-configuration-item"></a>Yapılandırma öğesi oluşturma ve dağıtma
Android for Work, yapılandırma öğeleri için iki ayar grubuna sahiptir:
- Parola
- İş profili

İş profilleri arasında içerik paylaşımını ve Android 6 veya üstünü çalıştıran cihazlarda aşağıdaki yapılandırma öğelerini yapılandırabilirsiniz:
- Belirli izinler isteyen uygulamalar için davranış
- İş profili içindeki uygulamalar için bildirimlerin kilit ekranında görünür olup olmadığı

Bunu denemek için standart iş akışı aracılığıyla bir yapılandırma öğesi oluşturun, **genel** sayfasında **Android for Work** ' ü seçin ve ayar gruplarının her biri için ayarları yapılandırın, yapılandırma öğesini bir taban çizgisine ekleyin ve her zamanki gibi dağıtım yapın. Bu ayarlar yalnızca Android for Work olarak kaydedilmiş cihazlara uygulanır ve Android olarak kaydedilmeyecektir.

#### <a name="perform-selective-wipe"></a>Seçmeli Temizleme gerçekleştir
Android for Work olarak kaydedilen cihazlar yalnızca iş profilini yönettiğiniz için seçmeli olarak temizlenir. Bu, kişisel profilin silinmesine karşı korunmasını sağlar. Android for Work cihazında seçmeli temizleme gerçekleştirmek, tüm uygulamalar ve veriler dahil olmak üzere iş profilini kaldırır ve cihazı kaydeder.

Bir Android for Work cihazını seçmeli olarak silmek için Configuration Manager konsolundaki normal [seçmeli silme işlemini](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) kullanın.

#### <a name="known-issues-for-android-for-work"></a>Android for Work için bilinen sorunlar
**Android for Work e-posta profillerinde eşitleme zamanlamasının yapılandırılması, bunların dağıtılmasına neden olur** Android for Work e-posta profilleri için ConfigMgr Kullanıcı arabirimindeki seçeneklerden biri "Schedule". Bu, diğer platformlarda, yöneticinin dağıtılan mobil cihazlara e-posta ve diğer e-posta hesabı verilerinin eşitlenmesi için bir zamanlama yapılandırmasına izin verir. Ancak, Android for Work e-posta profilleri için çalışmaz ve "Yapılandırılmadı" dışında herhangi bir seçeneğin seçilmesi profilin hiçbir cihaza dağıtılmamasına neden olur.