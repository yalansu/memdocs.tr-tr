---
title: Öğretici-Windows 10 dağıtma
titleSuffix: Configuration Manager
description: Windows 10 ' un bir pilot grubuna dağıtılması için masaüstü Analizi ve Configuration Manager kullanma hakkında bir öğretici.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 15cf7f3621f25a82f0e16d5275369ec93225bbf7
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422835"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Öğretici: pilot 'a Windows 10 dağıtma

Bu öğretici, Windows 10 ' un bir pilot grubuna dağıtılması için masaüstü Analizi ve Configuration Manager kullanır. Şirket içi ürünle Windows 'u dağıtmak için öngörüleri sunmaya yönelik bulut hizmeti tümleştirmesini vurgular. Bir pilot gruba yerleştirilecek en iyi cihazları öğrenmek için masaüstü Analizi 'ni kullanın. Ardından Configuration Manager kullanarak Windows ile güncel bir yararlanın.

Bu öğreticide aşağıdakilerin nasıl yapılacağını öğreneceksiniz:  

> [!div class="checklist"]  
> * Azure portal masaüstü analizlerini ayarlama  
> * Configuration Manager bağlanma ve cihaz ayarlarını yapılandırma  
> * Windows 10 için masaüstü Analizi dağıtım planı oluşturma  
> * Windows 10 ' un pilot grubuna dağıtılması için Configuration Manager kullanma  

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free) oluşturun. Düzgün yapılandırıldığında, masaüstü analizlerinin kullanımı hiçbir Azure maliyetine neden olmaz.

Masaüstü analizi, Azure aboneliğinizde bir *Log Analytics çalışma alanı* kullanır. Çalışma alanı, temelde hesap bilgilerini ve hesaba ilişkin basit yapılandırma bilgilerini içeren bir kapsayıcıdır. Daha fazla bilgi için bkz. [çalışma alanlarını yönetme](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Önkoşullar

Bu öğreticiye başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:  

- Etkin bir Azure aboneliği, [**genel yönetici**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) izinlerine sahip  

    Daha fazla bilgi için bkz. [Masaüstü Analizi önkoşulları](overview.md#prerequisites).

- Configuration Manager, sürüm 1902 güncelleştirme paketi (4500571) veya üzeri, **tam yönetici** rolü ile  

- Windows 10 ' un en son sürümü için yükleme medyası

- Aşağıdaki yapılandırmalara sahip en az bir Windows 10 cihazı:  

    - Windows 10, sürüm 1709 veya üzeri, ancak kullanmayı planladığınız yükleme ortamının sürümünden daha az

    - En son Windows 10 toplu kalite güncelleştirmesi  

    - Configuration Manager Client sürüm 1902 güncelleştirme paketi (4500571) veya üzeri  

- Windows tanılama veri düzeyini pilot cihazlarda **Gelişmiş (sınırlı)** olarak yapılandırmak için iş onayı  

    Daha fazla bilgi için bkz. [Masaüstü Analizi gizliliği](privacy.md).

- Cihazdan aşağıdaki Internet uç noktalarına ağ bağlantısı:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net`(yalnızca Configuration Manager sunucu rolü)
    - `https://*.manage.microsoft.com`(yalnızca Configuration Manager sunucu rolü)

    Daha fazla bilgi için bkz. [Masaüstü analizi için veri paylaşımını etkinleştirme](enable-data-sharing.md#endpoints).  

> [!Important]  
> Bu Önkoşullar, Bu öğreticinin amaçlarına yöneliktir. Configuration Manager ile masaüstü analizlerinin genel önkoşulları hakkında daha fazla bilgi için bkz. [Önkoşullar](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Desktop Analytics’i ayarlama

Bu yordamı kullanarak, masaüstü analizine oturum açın ve aboneliğinizde yapılandırın. Bu yordam, kuruluşunuz için masaüstü analizlerini ayarlamaya yönelik tek seferlik bir işlemdir.  

1. Microsoft 365 cihaz yönetimi ' nde [Masaüstü Analizi portalını](https://aka.ms/desktopanalytics) , **genel yönetici** izinlerine sahip bir kullanıcı olarak açın. **Başlat**'ı seçin.  

2. **Hizmet sözleşmesini kabul et** sayfasında, hizmet sözleşmesini gözden geçirin ve **kabul et**' i seçin.  

3. **Aboneliğinizi onaylayın** sayfasında, gerekli koşullara uyan lisansların listesi, masaüstü analizinin Windows cihaz sistem durumu özelliklerine yöneliktir. Devam etmek için **İleri** seçeneğini belirleyin.  

4. **Kullanıcılara erişim izni** sayfasında:

    - **Masaüstü analizlerinin sizin adınıza Dizin rollerini yönetmesine Izin verin**: Masaüstü analizi, **çalışma alanı sahiplerini** **Masaüstü Analizi Yöneticisi** rolüne otomatik olarak atar. Bu gruplar zaten **genel yönetici**ise, değişiklik yoktur.  

        Bu seçeneği seçmezseniz, masaüstü Analizi kullanıcıları yine de güvenlik grubunun üyesi olarak ekler. **Genel yöneticinin** kullanıcılar Için **Masaüstü Analizi yönetici** rolünü el ile ataması gerekir.  

        Azure Active Directory ' de yönetici rolü izinleri atama hakkında daha fazla bilgi ve **Masaüstü Analizi yöneticilerine**atanan izinler hakkında daha fazla bilgi için, bkz. [Azure Active Directory içindeki yönetici rolü izinleri](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Masaüstü analizi, çalışma alanları ve dağıtım planları oluşturmak ve yönetmek için Azure Active Directory **çalışma alanı sahipleri** güvenlik grubunu önceden yapılandırır. 

        Gruba bir kullanıcı eklemek için ad veya e-posta **adresi girin** bölümüne adını veya e-posta adresini yazın. İşiniz bittiğinde **İleri**' yi seçin.

5. **Çalışma alanınızı ayarlamak**için sayfasında:  

    > [!Note]  
    > Bu adımı gerçekleştirmek için, Kullanıcı **çalışma alanı sahibi** Izinlerine ve Azure aboneliğine ve kaynak grubuna ek erişime ihtiyaç duyuyor. Daha fazla bilgi için bkz. [Önkoşullar](overview.md#prerequisites).  

    - Azure aboneliğinizi seçin.  

    - Masaüstü analizi için mevcut bir çalışma alanı kullanmak için, seçin ve sonraki adımla devam edin.  

    - Masaüstü analizi için bir çalışma alanı oluşturmak üzere **çalışma alanı Ekle**' yi seçin.  

        1. Bir **çalışma alanı adı**girin.  

        2. **Bu çalışma alanı Için Azure abonelik adını seçmek**üzere açılan listeyi seçin ve bu çalışma alanı için Azure aboneliğini seçin.  

        3. **Yeni oluştur** Kaynak grubu veya **mevcut olanı kullanın**.  

        4. Listeden **bölgeyi** seçin ve ardından **Ekle**' yi seçin.  

6. Yeni veya mevcut bir çalışma alanı seçin ve ardından **Masaüstü Analizi çalışma alanı olarak ayarla**' yı seçin.  Ardından, **erişimi onayla ve erişim izni** Iletişim kutusunda **devam** ' ı seçin.  

7. Yeni tarayıcı sekmesinde, oturum açmak için kullanılacak bir hesap seçin. **Kuruluşunuz adına izin** vermek için seçeneği belirleyin ve **kabul et**' i seçin.  


    > [!Note]  
    > Bu izin, MALogAnalyticsReader uygulamasını çalışma alanı için Log Analytics okuyucu rolü atamak içindir. Bu uygulama rolü masaüstü analizi için gereklidir. Daha fazla bilgi için bkz. [MALogAnalyticsReader uygulama rolü](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. **Çalışma alanınızı ayarlamak**için sayfaya geri dönün, **İleri**' yi seçin.  

9. **Son adımlar** sayfasında, **Masaüstü Analizi 'ne git**' i seçin. Azure portal, masaüstü Analizi **giriş** sayfasını gösterir.  



## <a name="connect-configuration-manager"></a>Configuration Manager’a bağlanma

Configuration Manager güncelleştirmek, masaüstü analizlerini bağlamak ve cihaz ayarlarını yapılandırmak için bu yordamı kullanın. Bu yordam, hiyerarşinizi bulut hizmetine eklemek için tek seferlik bir işlemdir.  

### <a name="update-configuration-manager"></a>Güncelleştirme Configuration Manager

Masaüstü analizi ile tümleştirmeyi desteklemek için Configuration Manager sürüm 1902 güncelleştirme paketi 'ni (4500571) yükler. Bu güncelleştirme hakkında daha fazla bilgi için bkz. [geçerli Configuration Manager dalı Için güncelleştirme paketi, sürüm 1902](https://support.microsoft.com/help/4500571).

1. Siteyi 1902 sürümüne yönelik güncelleştirme paketi ile güncelleştirin. Daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yüklemeyi](../core/servers/manage/install-in-console-updates.md).  

2. İstemcileri güncelleştirin. Bu işlemi basitleştirmek için otomatik istemci yükseltmesini kullanmayı göz önünde bulundurun. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Hizmete bağlanma

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin. Şeritte **Azure hizmetlerini yapılandır** ' ı seçin.  

2. Azure Hizmetleri Sihirbazı 'nın **Azure hizmetleri** sayfasında, aşağıdaki ayarları yapılandırın:  

    - Configuration Manager nesne için bir **ad** belirtin  

    - Hizmeti tanımlamanızı sağlayacak isteğe bağlı bir **Açıklama** belirtin  

    - Kullanılabilir hizmetler listesinden **Masaüstü Analizi** ' ni seçin.  
  
   **İleri**’yi seçin.  

3. **Uygulama** sayfasında, uygun **Azure ortamını**seçin. Ardından Web uygulaması için **Araştır** ' ı seçin.

4. Masaüstü Analizi bağlantısı için kolayca bir Azure AD uygulaması eklemek üzere **Oluştur** ' u seçin.

5. **Sunucu uygulaması oluştur** penceresinde aşağıdaki ayarları yapılandırın:  

    - **Uygulama adı**: Azure AD 'de uygulama için kolay bir ad.

    - **Giriş sayfası URL 'si**: bu değer Configuration Manager tarafından kullanılmaz, ancak Azure AD tarafından gerekli değildir. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.  

    - **Uygulama kimliği URI 'si**: Bu DEĞERIN Azure AD kiracınızda benzersiz olması gerekir. Hizmete erişim istemek için Configuration Manager istemcisi tarafından kullanılan erişim simgesindeki. Varsayılan olarak bu `https://ConfigMgrService` değerine ayarlanır.  

    - **Gizli anahtar geçerlilik süresi**: açılan listeden **1 yıl** veya **2 yıl** seçeneklerinden birini belirleyin. Bir yıl, varsayılan değerdir.  

    **Oturum aç**'ı seçin. Azure 'da başarıyla kimlik doğrulamasından geçtikten sonra, sayfada başvuru için **Azure AD kiracı adı** gösterilir.

    > [!Note]  
    > Bu adımı **genel yönetici**olarak doldurun. Bu kimlik bilgileri Configuration Manager tarafından kaydedilmez. Bu kişi Configuration Manager izinleri gerektirmez ve Azure Hizmetleri Sihirbazı 'Nı çalıştıran aynı hesapla aynı olmalıdır.  

    Azure AD 'de Web uygulaması oluşturmak için **Tamam** ' ı seçin ve sunucu uygulaması oluştur iletişim kutusunu kapatın. Sunucu uygulaması iletişim kutusunda **Tamam**' ı seçin. Ardından, Azure hizmetleri sihirbazının uygulama sayfasında **İleri** ' yi seçin.  

6. **Tanılama verileri** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **TICARI kimlik**: Bu değer, kuruluşunuzun kimliğiyle otomatik olarak doldurulur  

    - **Windows 10 tanılama veri düzeyi**: en az **Gelişmiş (sınırlı)** seçeneğini belirleyin  

    - **Tanılama verilerinde cihaz adına Izin ver**: **Etkinleştir** ' i seçin  
  
   **İleri**’yi seçin. **Kullanılabilir işlevsellik** sayfasında, önceki sayfadan gelen Tanılama verileri ayarları Ile kullanılabilen masaüstü Analizi işlevleri gösterilmektedir. **İleri**’yi seçin.  

7. **Koleksiyonlar** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Görünen ad**: Masaüstü Analizi portalı bu adı kullanarak bu Configuration Manager bağlantıyı görüntüler. Farklı hiyerarşiler arasında ayrım yapmak için bunu kullanın. Örneğin, *Test Laboratuvarı* veya *üretimi*.  

    - **Hedef koleksiyon**: Bu koleksiyon, ticari kimliğiniz ve tanılama veri ayarlarınızla Configuration Manager yapılandırdığı tüm cihazları içerir. Bu, Configuration Manager masaüstü Analizi hizmetine bağlanan cihazların eksiksiz kümesidir.  

    - **Hedef koleksiyondaki cihazlar giden iletişim için Kullanıcı tarafından kimliği doğrulanmış bir proxy kullanır**: varsayılan olarak bu değer **Hayır**' dır. Ortamınızda gerekliyse, **Evet**olarak ayarlayın.  

    - **Masaüstü analizi ile eşitlenmek üzere belirli koleksiyonlar seçin**: ek koleksiyonlar eklemek için **Ekle** ' yi seçin. Bu koleksiyonlar, dağıtım planlarıyla gruplamak için masaüstü Analizi portalında kullanılabilir. Pilot ve pilot dışlama koleksiyonlarını eklediğinizden emin olun.  

        Bu koleksiyonlar, üyelik değişiklikleri olarak eşitlemeye devam eder. Örneğin, Dağıtım planınız bir Windows 7 üyelik kuralıyla bir koleksiyon kullanır. Bu cihazlar Windows 10 ' a yükseltile, ve Configuration Manager koleksiyon üyeliğini değerlendirirken, bu cihazlar koleksiyon ve dağıtım planından çıkar.  

8. Sihirbazı tamamlayın.  

Configuration Manager, hedef koleksiyondaki cihazları yapılandırmak için bir ayar ilkesi oluşturur. Bu ilke, cihazların Microsoft 'a veri göndermesini sağlamak için tanılama verileri ayarlarını içerir. Varsayılan olarak, istemciler ilkeyi her saat güncelleştirir. Yeni ayarları aldıktan sonra, verilerin masaüstü analizinden kullanılabilmesi birkaç saat daha olabilir.

> [!Note]  
> Bu ayarlar hakkında daha fazla bilgi için bkz. [Windows ayarları](enroll-devices.md#windows-settings).  

Masaüstü analizi için cihazlarınızın yapılandırmasını izleyin. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Masaüstü Analizi bakım** düğümünü genişletin ve **bağlantı sistem durumu** panosunu seçin.  

Configuration Manager, bağlantı oluşturma 60 dakika içinde koleksiyonlarınızı eşitler. Masaüstü Analizi portalında, **genel pilot**' a gidin ve Configuration Manager cihaz koleksiyonlarınızı görüntüleyin. Portalın geri kalanı, tüm verileri göstermek için iki ile üç gün sürebilir. Daha fazla bilgi için bkz. [veri gecikmesi](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Masaüstü Analizi dağıtım planı oluşturma

Masaüstü Analizi 'nde bir dağıtım planı oluşturmak için bu yordamı kullanın.

1. [Masaüstü Analizi portalını](https://aka.ms/desktopanalytics)açın. En az **çalışma alanı katkıda** bulunan izinleri olan kimlik bilgilerini kullanın.  

2. Yönet grubunda **dağıtım planları** ' nı seçin.  

3. **Dağıtım planları** bölmesinde **Oluştur**' u seçin.  

4. **Dağıtım planı oluştur** bölmesinde, aşağıdaki ayarları yapılandırın:  

    - **Ad**: dağıtım planı için benzersiz bir ad, örneğin`Windows 10 pilot`  

    - **Ürünler ve sürümler**: hangi Windows 10 sürümünü dağıtacağınızı seçin. Microsoft, en son sürümü kullanan dağıtım planlarının oluşturulmasını önerir.

    - **Cihaz grupları**: Configuration Manager sekmesinden bir veya daha fazla grup seçin ve ardından **hedef gruplar olarak ayarla**' yı seçin. Bu gruplar Configuration Manager 'ten eşitlenen koleksiyonlardır.  

    - **Hazırlık kuralları**: Bu kurallar, hangi cihazların yükseltme için uygun olduğunu belirlemenize yardımcı olur. **Windows işletim sistemi** ' ni seçin ve aşağıdaki ayarları yapılandırın:  

        - **Bilgisayarlarım Windows Update sürücüleri otomatik olarak alır**: varsayılan ayar **kapalı**olur ve Configuration Manager ile dağıtıldığında önerilir.  

        - **Uygulamalarınız için düşük bir Install Count eşiği tanımlayın**: varsayılan ayar `2%` . Bu eşiğin altındaki uygulamalar otomatik olarak *düşük yüklemesi sayısı*olarak ayarlanır. Masaüstü analizi, pilot sırasında bu eklentileri doğrulamaz.  

            Bir uygulama bu eşikten daha yüksek bir bilgisayar yüzdesine yüklenirse, dağıtım planı uygulamayı en *önemli şekilde işaretler*. Ardından, Pilot aşaması sırasında test etmek için önem derecesine karar verebilirsiniz.  

    - **Tamamlanma tarihi**: Windows 'un hedeflenen tüm cihazlara tam olarak dağıtılması gereken tarihi seçin.  

5. **Oluştur**’u seçin. Yeni plan, işlendiği sırada dağıtım planları listesinde görünür. İşleme hızlandırmak için isteğe bağlı veri yenileme isteyin. Daha fazla bilgi için bkz. [Masaüstü analizi hakkında SSS](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Dağıtım planını, adını seçerek açın.  

7. Dağıtım planı menüsünde, **hazırla** grubunda, **önemi tanımla**' yı seçin.  

    1. **Uygulamalar** sekmesinde, yalnızca **Gözden geçirilmeyen** varlıkları göstermek için seçin.  

    2. Her uygulamayı seçip **Düzenle**' yi seçin. Aynı anda düzenlemek için birden çok uygulama seçebilirsiniz.  

    3. **Önem** listesinden bir önem düzeyi seçin. Pilot sırasında Masaüstü analizinin uygulamayı doğrulamasını istiyorsanız, **kritik** veya **önemli**seçeneğini belirleyin. **Önemli değil**olarak işaretlenen uygulamaları doğrulamaz. Önem düzeyi atarken [uyumluluğunu](compat-assessment.md) ve diğer plan öngörülerini değerlendirin.  

        Önem düzeyleri atarken, yükseltme kararlarını da seçebilirsiniz.  

    4. Tamamlandığında **Kaydet** ' i seçin.  

8. Dağıtım planı menüsünde, **hazırla** grubunda, **pilot 'u tanımla**' yı seçin.  

    1. Pilot için önerilen cihazları gözden geçirin.  

    2. Her bir cihazı seçin ve **pilot 'A Ekle**' yi seçin. Öneriyi kabul etmiyorsanız, **Değiştir**' i seçin.  

        Masaüstü analizinin bu önerileri nasıl yaptığı hakkında daha fazla bilgi için, **pilot bölmesini belirleme** bölmesinin sağ üst köşesindeki bilgi simgesini seçin.



## <a name="deploy-windows-10-in-configuration-manager"></a>Windows 10 ' Configuration Manager dağıtma

Configuration Manager Windows 10 ' da pilot grubuna dağıtmak için bu yordamı kullanın.

- Henüz bir hesabınız yoksa, önce [Windows 10 için bir işletim sistemi yükseltme paketi oluşturun](#bkmk_create-package)  

- Henüz bir tane yoksa, [Windows 10 için bir işletim sistemi yükseltme görev dizisi oluşturun](#bkmk_create-ts)  

- Masaüstü Analizi dağıtım planını kullanarak [görev dizisini dağıtma](#bkmk_deploy-ts)  

- [Görev sırasını,](#bkmk_install-ts) hedeflenen bir cihaza yazılım merkezi 'nden yükler  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a>Windows 10 için işletim sistemi yükseltme paketi oluşturma

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **işletim sistemi yükseltme paketleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **işletim sistemi yükseltme paketi Ekle**' yi seçin. Bu eylem, Işletim sistemi yükseltme ekleme Sihirbazı 'Nı başlatır.  

3. **Veri kaynağı** sayfasında işletim sistemi yükseltme paketinin yükleme kaynak dosyalarının ağ **yolunu** belirtin. Örneğin, `\\server\share\path`.  

    > [!NOTE]  
    > Yükleme kaynak dosyaları, işletim sistemini yüklemek için setup.exe ve diğer dosya ve klasörleri içerir.  

4. **Genel** sayfasında, işletim sistemi yükseltme paketi için benzersiz bir **ad** belirtin.  

5. Işletim sistemi yükseltme paketi ekleme Sihirbazı 'Nı doldurun.  

#### <a name="distribute-content"></a>İçeriği dağıt

Sonra, işletim sistemi yükseltme paketini dağıtım noktalarına dağıtın.  

1. Listeden işletim sistemi yükseltme paketini seçin. Şeridin **giriş** sekmesinde, **dağıtım** grubunda, **içeriği dağıt**' ı seçin. Içerik Dağıtma Sihirbazı açılır.  

2. **Genel** sayfasında, listelenen içeriğin dağıtmak istediğiniz içerik olduğunu doğrulayın ve ardından **İleri**' yi seçin.  

3. **Içerik hedefi** sayfasında **Ekle**' yi seçin ve **dağıtım noktası**' nı seçin. Var olan bir dağıtım noktası seçin ve ardından **Tamam**' ı seçin. İçerik hedefleri eklemeyi bitirdiğinizde **İleri**' yi seçin.  

4. Içerik Dağıtma Sihirbazı 'Nı doldurun.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a>Windows 10 için işletim sistemi yükseltme görev dizisi oluşturma

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası oluştur**' u seçin.  

3. Görev sırası oluşturma Sihirbazı ' nın **Yeni görev sırası oluştur** sayfasında, bir **işletim sistemini yükseltme paketinden Yükselt**' i seçin ve ardından **İleri**' yi seçin.  

4. **Görev sırası bilgileri** sayfasında, görev dizisini tanımlayan bir **görev sırası adı** belirtin.  

5. **Windows Işletim sistemini yükseltme** sayfasında, aşağıdaki ayarları belirtin ve ardından **İleri**' yi seçin:  

    - **Paketi Yükselt**: işletim sistemi yükseltme kaynak dosyalarını içeren yükseltme paketini belirtin.  

    - **Sürüm dizini**: pakette birden çok işletim sistemi sürümü dizini varsa, istenen sürüm dizinini seçin. Varsayılan olarak, sihirbaz ilk dizini seçer.  

    - **Ürün anahtarı**: işletim sisteminin yüklenmesi için Windows ürün anahtarını belirtin. Kodlanmış toplu lisans anahtarlarını veya standart ürün anahtarlarını belirtin. Standart bir ürün anahtarı kullanırsanız, her beş karakter grubunu bir tire (-) ile ayırın. Örneğin: *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*. Yükseltme bir toplu lisans sürümü için olduğunda, ürün anahtarı gerekli olmayabilir.  

        > [!Note]  
        > Bu ürün anahtarı birden çok etkinleştirme anahtarı (MAK) veya bir genel toplu lisanslama anahtarı (GVLK) olabilir. Bir GVLK, anahtar yönetimi hizmeti (KMS) istemci kurulum anahtarı olarak da adlandırılır. Daha fazla bilgi için bkz. [toplu etkinleştirme planı](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). KMS istemci kurulum anahtarlarının bir listesi için, bkz. Windows Server etkinleştirme kılavuzunun [ek a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) .

6. **Güncelleştirmeleri dahil et** sayfasında, yazılım güncelleştirmelerini yüklememe için **İleri** ' yi seçin.  

7. Uygulamaları **yüklemek** sayfasında, herhangi bir uygulama yüklememeyi açmak için **İleri** ' yi seçin.

8. Görev sırası oluşturma Sihirbazı 'Nı doldurun.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a>Masaüstü Analizi dağıtım planını kullanarak görev dizisini dağıtma

1. Configuration Manager konsolunda, **yazılım kitaplığı**' na gidin, **Masaüstü Analizi Bakımı**' nı genişletin ve **dağıtım planları** düğümünü seçin.  

2. Windows 10 pilot dağıtım planınızı seçin ve ardından şeritte **dağıtım planı ayrıntıları** ' nı seçin.  

3. **Pilot durum** kutucuğunda, açılan listeden **görev dizisi** ' ni seçin ve ardından **Dağıt**' ı seçin.  

4. Yazılım Dağıtma Sihirbazı 'nın **genel** sayfasında, **yazılım** alanının yanındaki Git ' **i seçin.** Windows 10 yerinde yükseltme görev sırasını seçin ve **İleri**' yi seçin.  

    > [!Note]  
    > Masaüstü Analizi tümleştirmesiyle, Configuration Manager dağıtım planı için otomatik olarak pilot ve üretim koleksiyonları oluşturur. Bunları kullanabilmeniz için, bu koleksiyonların eşitlenmesi zaman alabilir. Daha fazla bilgi için bkz. [sorun giderme-veri gecikmesi](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Bu koleksiyon, masaüstü Analizi dağıtım planı cihazları için ayrılmıştır. Bu koleksiyonda el ile yapılan değişiklikler desteklenmiyor.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. **İçerik** sayfasında **Ekle**' yi ve ardından **dağıtım noktası**' nı seçin. Yükleme içeriğini barındırmak için kullanılabilir bir dağıtım noktası seçin ve **Tamam**' ı seçin. Sonra **İleri**’yi seçin.  

6. **Dağıtım ayarları** sayfasında, varsayılan ayarları kabul etmek için **İleri** ' yi seçin. (Kullanılabilir bir yükleme.)  

7. **Zamanlama** sayfasında, varsayılan ayarları kabul etmek için **İleri** ' yi seçin. (Mümkün olan en kısa sürede kullanılabilir.)  

8. **Kullanıcı deneyimi** sayfasında, varsayılan ayarları kabul etmek için **İleri** ' yi seçin. (Yazılım merkezi 'nde görüntüle ve yalnızca bilgisayar yeniden başlatmaları için bildirimleri göster.)  

9. **Uyarılar** sayfasında, varsayılan ayarları kabul etmek için **İleri** ' yi seçin.  

10. Sihirbazı tamamlayın.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a>Görev sırasını yazılım merkezi 'nden yükler

1. Pilot dağıtım planının üyesi olan bir cihazda oturum açın.  

2. **Yazılım merkezini** açın ve Windows 10 için kullanılabilir işletim sistemini yükler.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Sonraki adımlar

Masaüstü Analizi dağıtım planları hakkında daha fazla bilgi edinmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]  
> [Dağıtım planları](about-deployment-plans.md)
