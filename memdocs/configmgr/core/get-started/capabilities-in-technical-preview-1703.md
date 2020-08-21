---
title: Technical Preview 1703 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1703 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9209a1a948c43a21f097ba836a6761b53ddc9530
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692970"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Configuration Manager için Technical Preview 1703 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1703 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Toplu satın alınan iOS uygulamalarını cihaz koleksiyonlarına dağıtma

Artık, lisanslanan uygulamaları cihazlara ve kullanıcılara dağıtabilirsiniz. Cihaz lisansını desteklemeye yönelik uygulamalara bağlı olarak, dağıtım sırasında aşağıdaki gibi uygun bir lisans talep edilir:

| Configuration Manager sürümü | Uygulama, cihaz lisansını destekliyor mu? | Dağıtım koleksiyonu türü | Talep edilen lisans |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|1702 öncesi|Evet|Kullanıcı|Kullanıcı Lisansı|
|1702 öncesi|Hayır|Kullanıcı|Kullanıcı Lisansı|
|1702 öncesi|Evet|Cihaz|Kullanıcı Lisansı|
|1702 öncesi|Hayır|Cihaz|Kullanıcı Lisansı|
|1702 ve üzeri|Evet|Kullanıcı|Kullanıcı Lisansı|
|1702 ve üzeri|Hayır|Kullanıcı|Kullanıcı Lisansı|
|1702 ve üzeri|Evet|Cihaz|Cihaz lisansı|
|1702 ve üzeri|Hayır|Cihaz|Kullanıcı Lisansı|


## <a name="direct-links-to-applications-in-software-center"></a>Yazılım Merkezi 'nde uygulamaların doğrudan bağlantıları

Artık son kullanıcılara yazılım merkezi 'nde bir uygulamaya doğrudan bağlantı sağlayabilirsiniz. Bu, artık yazılım merkezi 'ni açmak ve uygulamayı yüklemeden önce bir uygulama aramak zorunda olmayacağı anlamına gelir. Bu, yalnızca Configuration Manager uygulamalar için kullanılabilir, paketler ve programlar veya görev dizileri için geçerlidir.

### <a name="try-it-out"></a>Deneyin                 

Yazılım merkezini belirli bir uygulamaya açmak için aşağıdaki URL biçimini kullanın:

**Softwarecenter: SoftwareID =_uygulama tanımlayıcısı_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Uygulamanın uygulama tanımlayıcısını alma.

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.
2. Yazılım Kitaplığı çalışma alanında **uygulama yönetimi**' ni genişletin ve ardından **uygulamalar**' a tıklayın.
3. **Uygulamalar** görünümünde, sütun başlıklarından birine sağ tıklayın ve sonra listeden **CI benzersiz kimliği**' ni seçin. Her uygulamanın benzersiz KIMLIĞININ artık listede gösterildiğini görürsünüz.
4. Bağlantı sağlamak istediğiniz uygulamanın **CI BENZERSIZ kimliğini** aklınızda yapın, örneğin: **ScopeId_1672B0CD-912a-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405C-AD37-c753400b895f/2**
5. Daha sonra, bu durumda **/2**uygulama GUID 'sini izleyen tüm metinleri kaldırın. Bu, sizi uygulama tanımlayıcısı ile bırakır.
6. Son olarak, bağlantıyı oluşturma işleminin tamamlanabilmesi için, **Softwarecenter: SoftwareID =** ile önüne geçin. Yukarıdaki örneği kullanarak son bağlantı şu şekilde okunacak: **Softwarecenter: SoftwareID = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405C-AD37-c753400b895f**.

Bu bağlantıyı kullanarak, son kullanıcılar yazılım merkezini doğrudan belirttiğiniz uygulamaya açabilir.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Configuration Manager Windows istemci bilgisayarları için PFX sertifikaları

Artık Windows 10 çalıştıran Configuration Manager istemci bilgisayarlara, içeri aktardığınız PFX Sertifika profillerini dağıtabilirsiniz.

### <a name="try-it-out"></a>Deneyin

Pfx profilini içeri aktarmak, profili dağıtmak ve sonra sertifikanın hedeflenen kullanıcı için yüklenip yüklenmediğini kontrol etmek için [PFX Sertifika profillerinin nasıl oluşturulduğu](../../mdm/deploy-use/create-pfx-certificate-profiles.md) konusundaki yönergeleri kullanın.



## <a name="configure-azure-services-wizard"></a>Azure hizmetlerini Yapılandırma Sihirbazı
Technical Preview 1703, **Azure hizmetlerini yapılandırma** Sihirbazı 'nı tanıtır. Bu sihirbaz, Configuration Manager ile kullandığınız bulut hizmetlerini ayarlamak için bireysel iş akışlarının yerini alan ortak bir yapılandırma deneyimi sağlar. Bu işlem, Azure ile yeni bir Configuration Manager bileşeni veya hizmeti her yaptığınızda girdiğiniz abonelik ve yapılandırma ayrıntılarını sağlamak için bir **Azure Web uygulaması** kullanılarak yapılır.

Technical Preview 1703 ile, bu sihirbaz kullanılarak yalnızca Iş için Windows Mağazası (WSfB) yapılandırılır.  Diğer bulut hizmetleri ayrı iş akışları kullanılarak yapılandırılır.

- [Configuration Manager iş Için Windows Mağazası 'ndan uygulamaları yönetme](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)güncel dalı konusunun [Iş için Windows Mağazası eşitlemesini ayarlama](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) bölümünde bulunan yapılandırma adımlarını değiştirmek için bu önizleme konusundaki bilgileri kullanın.

- Web Apps hakkında daha fazla bilgi için [Azure App Service 'Da kimlik doğrulaması ve yetkilendirme](/azure/app-service/app-service-authentication-overview)ve [Web Apps genel bakış](/azure/app-service-web/app-service-web-overview)bölümüne bakın.

### <a name="prerequisites-and-planning"></a>Önkoşullar ve planlama
Configuration Manager ile Iş için Windows Mağazası arasında bir bağlantı ayarladığınızda, mağazadan eşitlenen uygulama içeriğinin tutulacağı bir klasör sağlamalısınız. Bu klasörün güvenli olduğundan ve içeriğinin cihazlara dağıtılabilmesi için aşağıdaki izinlerin sağlandığından emin olun:
- Hizmet bağlantı noktası site sistemi rolünü (hiyerarşideki üst düzey site) yüklediğiniz bilgisayar, **bilgisayar $** hesabı kullanılırken belirttiğiniz klasöre okuma ve yazma izinlerine sahip olmalıdır.  

- Uygulama yazarı, belirttiğiniz klasör üzerinde okuma izinlerine sahip olmalıdır.  

- SMS sağlayıcısı 'nın bir örneğini barındıran her bilgisayarın **bilgisayar $** hesabı, belirttiğiniz klasörü kullanabilmelidir.

Azure Active Directory, Configuration Manager bir Web uygulaması veya Web API 'SI yönetim aracı olarak kaydettirin. Bu, daha sonra ihtiyacınız olacak istemci KIMLIĞINI oluşturur.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>WSfB bulut hizmetini yapılandırmak için Sihirbazı kullanın

1. Konsolunda **Yönetim**  >  **genel bakış**  >  **Cloud Services yönetim**  >  **Azure**  >  **Azure hizmetleri**' ne gidin ve Azure Hizmetleri **Sihirbazı**' nı başlatmak için **Azure hizmetlerini yapılandır** ' ı seçin.

2. **Azure hizmetleri** sayfasında, yapılandırmak istediğiniz hizmeti seçin ve ardından **İleri**' ye tıklayın. Bu önizleme ile yalnızca WSfB yapılandırılabilir.

3. **Genel** sayfasında, **Azure hizmeti adı** ve isteğe bağlı bir açıklama için kolay bir ad girin ve ardından **İleri**' ye tıklayın.

4. **Uygulama** sayfasında, Azure ortamınızı belirtin ve ardından, sunucu uygulaması penceresini açmak Için, **Araştır** ' a tıklayın.

5. **Sunucu uygulaması** penceresinde, kullanmak istediğiniz sunucu uygulamasını seçin ve ardından **Tamam**' a tıklayın.
   Sunucu uygulamaları, kiracı KIMLIĞINIZ, Istemci KIMLIĞINIZ ve istemciler için gizli anahtar dahil olmak üzere Azure hesabınıza yönelik yapılandırmaların bulunduğu Azure Web Apps ' dir. Kullanılabilir bir sunucu uygulamanız yoksa, aşağıdakilerden birini kullanın:
   - **Oluştur**: yeni bir sunucu uygulaması oluşturmak için **Oluştur**' a tıklayın. Uygulama ve kiracı için kolay bir ad sağlayın. Ardından, Azure 'da oturum açtıktan sonra, Web uygulaması ile kullanmak üzere Istemci KIMLIĞI ve gizli anahtar dahil olmak üzere Azure 'da Web uygulaması oluşturur Configuration Manager. Daha sonra, bunları Azure portal görüntüleyebilirsiniz.
   - **Içeri aktar**: Azure aboneliğinizde zaten mevcut olan bir Web uygulamasını kullanmak Için **içeri aktar**' a tıklayın. Uygulama ve kiracı için kolay bir ad sağlayın ve ardından Configuration Manager kullanmak istediğiniz Azure Web uygulaması için kiracı KIMLIĞINI, Istemci KIMLIĞINI ve gizli anahtarı belirtin. Bilgileri **doğruladıktan** sonra, devam etmek için **Tamam** ' ı tıklatın.  </br></br>

6. **Bilgi** sayfasını gözden geçirin ve yönlendirilmiş olarak tüm ek adımları ve konfigürasyonları doldurun. Bu yapılandırmaların Configuration Manager hizmeti kullanması gerekir.
   Örneğin, WSfB 'yi yapılandırmak için:

   1. Azure 'da Configuration Manager bir Web uygulaması veya Web API 'SI olarak kaydetmeniz ve istemci KIMLIĞINI kaydetmeniz gerekir. Ayrıca yönetim aracı (Configuration Manager) tarafından kullanılacak bir istemci anahtarı da belirtirsiniz.

   2.    WSfB konsolunda mağaza yönetim aracı olarak Configuration Manager yapılandırmalı, çevrimdışı lisanslı uygulamalar için desteği etkinleştirip en az bir uygulama satın almalısınız.   </br>

   Devam etmeye hazırsanız **İleri** ' ye tıklayın.

7. **Uygulama konfigürasyonları** sayfasında, bu hizmet için uygulama kataloğunu ve dil yapılandırmasını tamamlayıp **İleri**' ye tıklayın.
8. Sihirbaz tamamlandıktan sonra, Configuration Manager konsolu, **iş Için Windows Mağazası** 'Nı bir **bulut hizmeti türü**olarak yapılandırdığınıza ilişkin olduğunu gösterir.

Artık, Iş için Windows Mağazası uygulamalarını eşitlemeniz, oluşturup dağıtmak ve izlemek üzere WSfB 'den uygulamaları yönetmek için [güncel dalı içeriğinin](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) kalanını kullanabilirsiniz.

### <a name="modify-a-cloud-service-configuration"></a>Bulut hizmeti yapılandırmasını değiştirme
Yapılandırmayı değiştirmek için bir bulut hizmetinin özelliklerini görüntüleyebilir ve düzenleyebilirsiniz.

Konsolunda **Yönetim**  >  **genel bakış**  >  **Cloud Services yönetim**  >  **Azure**  >  **Azure hizmetleri**' ne gidin ve ardından **Azure hizmetlerini yapılandır**' ı seçin, bir bulut hizmeti seçin ve ardından **Özellikler**' i seçin.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Yerinde yükseltme sırasında BIOS 'tan UEFı 'ye dönüştürme
Windows 10 Creators Update, işlemi UEFı etkin donanımlar için sabit diski yeniden bölümlemek ve dönüştürme aracını Windows 10 yerinde yükseltme işlemine tümleştiren bir basit dönüştürme aracı sunuyor. Bu aracı işletim sistemi yükseltme görev diziniz ve bellenimi BIOS 'tan UEFı 'ye dönüştüren OEM aracı ile birleştirdiğinizde, Windows 10 Creators Update 'e yerinde yükseltme sırasında bilgisayarlarınızı BIOS 'tan UEFı 'e dönüştürebilirsiniz. Ayrıntılar için bkz. [BIOS 'TAN UEFI dönüştürmeyi yönetmeye yönelik görev dizisi adımları](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

## <a name="collapsible-task-sequence-groups"></a>Daraltılabilir görev dizisi grupları
Bu sürüm, görev dizisi gruplarını genişletme ve daraltma özelliğini tanıtır. Tek tek grupları genişletebilir veya daraltabilir veya aynı anda tüm grupları genişletebilir veya daraltabilirsiniz.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Yükseltme Hazırlığı için Windows analizlerini yapılandırmak için istemci ayarları
Bu sürümden itibaren, Configuration Manager Yükseltme Hazırlığı gibi Windows Analytics çözümlerini kullanmak için gereken Windows Tanılama verilerinin yapılandırılmasını basitleştirmek üzere cihaz istemci ayarlarını kullanabilirsiniz. Configuration Manager, Windows Analytics 'ten, istemci bilgisayarlarınız tarafından bildirilen Windows Tanılama verilerine dayalı olarak ortamınızın geçerli durumu hakkında değerli Öngörüler sağlayabilen verileri alabilir. Windows Tanılama verileri, istemci bilgisayarlar tarafından Windows Tanılama hizmetine bildirilir ve ardından ilgili veriler daha sonra kuruluşunuzun OMS çalışma alanlarından birinde barındırılan Windows Analytics çözümlerine aktarılır. Yükseltme Hazırlığı, yönetilen cihazlarınız için Windows yükseltmeleriyle ilgili kararları önceliklendirmenize yardımcı olabilecek bir Windows Analytics çözümüdür.

### <a name="prerequisites"></a>Ön koşullar
- Sitenizi Yükseltme Hazırlığı bulut hizmetini kullanacak şekilde yapılandırmış olmanız gerekir.

### <a name="configure-windows-analytics-client-settings"></a>Windows Analytics istemci ayarlarını yapılandırma
Windows Analytics 'i yapılandırmak için, Configuration Manager konsolunda **Yönetim**  >  **istemci ayarları**' na gidin, **özel cihaz istemci ayarları oluştur** ' a çift tıklayın ve ardından **Windows Analytics**' i işaretleyin.  

Ardından, **Windows Analytics** ayarları sekmesine gitmeden sonra aşağıdakileri yapılandırın:
- **Ticari KIMLIK**  
Ticari KIMLIK anahtarı, yönettiğiniz cihazlardan gelen bilgileri, kuruluşunuzun Windows Analytics verilerini barındıran OMS çalışma alanına eşler. Yükseltme Hazırlığı ile kullanmak üzere zaten bir ticari KIMLIK anahtarı yapılandırdıysanız, bu KIMLIĞI kullanın. Henüz ticari KIMLIK anahtarınız yoksa ticari KIMLIK anahtarınızı oluşturun.

- **Windows 10 cihazları Için tanılama veri düzeyi** ayarlama

- **Windows 7, 8 ve 8,1 cihazlarda ticari veri toplamayı kabul** etmek için seçin   

- **Internet Explorer veri toplamayı yapılandırma** Windows 8.1 veya daha önceki bir sürümü çalıştıran cihazlarda, Internet Explorer veri toplama, Yükseltme Hazırlığı Windows 10 ' a sorunsuz yükseltmeyi engelleyebilecek Web uygulaması uyumsuzluklarını algılamasına izin verebilir. Internet Explorer veri toplama, internet alanı başına temelinde etkinleştirilebilir.