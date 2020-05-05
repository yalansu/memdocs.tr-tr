---
title: Kurulum Sihirbazı
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e32956d2ca9385c22e9073cfa2665e1f61b3ebd3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078643"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Configuration Manager siteleri yüklemek için Kurulum Sihirbazı 'Nı kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yeni bir Configuration Manager sitesini Kılavuzlu Kullanıcı arabirimini kullanarak yüklemek için, Configuration Manager Kurulum Sihirbazı 'Nı (Setup. exe) kullanın. Sihirbaz, birincil sitenin veya merkezi yönetim sitesinin yüklenmesini destekler. Ayrıca, Configuration Manager [bir değerlendirme yüklemesini](upgrade-an-evaluation-install-to-a-full-install.md) tam lisanslı bir yüklemeye yükseltmek için de Sihirbazı kullanırsınız. Sihirbazı kullanmak istemiyorsanız, bunun yerine bir [yükleme betiği](use-a-command-line-to-install-sites.md) kullanabilir ve Katılımsız komut satırı yüklemesi çalıştırabilirsiniz.

Configuration Manager konsolundan İkincil bir site yükler. İkincil siteler, komut dosyası komut satırı yüklemesini desteklemez.

> [!Note]  
> Sürüm 1906 ' den başlayarak, **giriş. hta** dosyası yükleme ortamının kökünde artık yok. Aşağıdaki bilgilere bağlantılar sağladı:<!--SCCMDocs-pr#3545-->
>
> - **Siteyi yükler**: `smssetup\bin\x64\setup.exe`. Daha fazla bilgi için bkz. [bir merkezi yönetim veya birincil site yüklemeye](#bkmk_primary).
> - **Başlamadan önce**: [bir site hiyerarşisi tasarlama](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Sunucu hazırlığını değerlendir**: [önkoşul denetleyicisi](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Gerekli önkoşul dosyalarını indirin**: `smssetup\bin\x64\setupdl.exe`. Daha fazla bilgi için bkz. [Kurulum Yükleyici](setup-downloader.md).
> - **Configuration Manager konsolu 'Nu yükler**: `smssetup\bin\i386\consolesetup.exe`. Daha fazla bilgi için bkz. [konsolları Install](install-consoles.md).
> - [**System Center Updates Publisher indir**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Ek işletim sistemleri için Istemcileri indir**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft uç nokta Configuration Manager-macOS Istemcisi (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [UNIX ve Linux için istemciler](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Sürüm notları**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Belgeleri okuyun**](https://docs.microsoft.com/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Yükleme yardımını edinin**: [TechNet forumları: Configuration Manager (güncel dalı) – site ve istemci dağıtımı](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Configuration Manager Community**: [System Center topluluğu: katılma](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Configuration Manager giriş**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a>Merkezi Yönetim veya birincil site yükler

Bir merkezi yönetim sitesi veya bir birincil site yüklemek için aşağıdaki yordamı kullanın. Ayrıca, değerlendirme sitesini tam lisanslı bir Configuration Manager sitesine yükseltmek için de kullanın.

Site yüklemesini başlatmadan önce aşağıdaki makalelerdeki ayrıntıları tanımanız gerekir:

- [Site yüklemeye hazırlanma](prepare-to-install-sites.md)
- [Site yükleme önkoşulları](prerequisites-for-installing-sites.md)

Bir merkezi yönetim sitesini bir site genişletme senaryosunun parçası olarak yüklüyorsanız, aşağıdaki yordamı kullanmadan önce [tek başına birincil siteyi genişletmeyi](use-the-setup-wizard-to-install-sites.md#bkmk_expand) gözden geçirin.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a>Birincil veya merkezi yönetim sitesi yüklemek için işlem

1. Sitesini yüklemek istediğiniz bilgisayarda, **Configuration Manager Kurulum Sihirbazı**' nı başlatmak için `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` ' i çalıştırın.  

    > [!NOTE]  
    > Tek başına birincil siteyi genişletmek için bir merkezi yönetim sitesi yüklediğinizde veya var olan bir hiyerarşiye yeni bir alt birincil site yüklüyorsanız, mevcut sitenin veya sitelerin sürümüyle eşleşen yükleme medyasını (kaynak dosyaları) kullanın. Daha önce yüklenen sitelerin sürümünü değiştiren konsol içi güncelleştirmeler yüklediyseniz, özgün yükleme medyasını kullanmayın. Bunun yerine, CD 'deki kaynak dosyalarını kullanın [. Güncel bir sitenin en son klasörü](../../manage/the-cd.latest-folder.md) . Configuration Manager, yeni sitenizin bağlanacağı mevcut sitenin sürümüyle eşleşen kaynak dosyalar kullanmanızı gerektirir.  

2. **Başlamadan önce** sayfasında **İleri**' yi seçin.  

3. **Başlarken** sayfasında, yüklemek istediğiniz sitenin türünü seçin:  

    - **Merkezi Yönetim sitesi**, yeni bir hiyerarşinin ilk sitesi olarak veya bağımsız bir birincil siteyi genişletirken:  

        **Configuration Manager merkezi yönetim sitesi yüklemeyi**seçin.  

        Bu yordamın sonraki adımında, bir merkezi yönetim sitesini yeni bir hiyerarşinin ilk sitesi olarak yüklemek ya da tek başına bir birincil siteyi genişletmek için merkezi yönetim sitesi yüklemek için tercih edersiniz.  

    - **Birincil site**, yeni bir hiyerarşinin ilk sitesi olan tek başına birincil site olarak veya alt birincil olarak:  

        **Configuration Manager birincil site yüklemeyi**seçin.  

        > [!TIP]  
        > Genellikle, bir test ortamında bağımsız bir birincil site yüklemek istediğinizde, tek **başına birincil site için tipik yükleme seçeneklerini kullan** seçeneğini belirleyin. Bu seçeneği belirlediğinizde, Kurulum aşağıdaki eylemleri yapar:  
        >
        > - Siteyi tek başına birincil site olarak otomatik olarak yapılandırır.  
        > - Varsayılan yükleme yolunu kullanır.  
        > - , Site veritabanı için varsayılan SQL Server bir yerel yüklemesi kullanır.  
        > - Site sunucusu bilgisayarına bir yönetim noktası ve bir dağıtım noktası kurar.  
        > - Siteyi, Configuration Manager desteklediği dillerden biriyle eşleşiyorsa birincil site sunucusundaki işletim sisteminin Ingilizce ve görüntüleme diliyle yapılandırır.  

4. **Ürün anahtarı** sayfasında:  

    - Configuration Manager değerlendirme sürümü veya lisanslı bir sürüm olarak yüklemeyi seçin.  

        - Lisanslı bir sürüm seçerseniz, ürün anahtarınızı girin ve **İleri**' yi seçin.  

        - Bir değerlendirme sürümü seçerseniz, **İleri**' yi seçin. (Değerlendirme yüklemesini daha sonra tam bir yüklemeye yükseltebilirsiniz.)  

    - Lisans sözleşmenizin **yazılım güvencesi süre sonu tarihini** de belirtebilirsiniz. Bu tarih için uygun bir anımsatıcı budur. Kurulum sırasında bu tarihi girmezseniz, daha sonra Configuration Manager konsolunun içinden belirtebilirsiniz.  

        > [!NOTE]  
        > Microsoft girdiğiniz sona erme tarihini doğrulamaz ve bu tarihi lisans doğrulaması için kullanmaz. Bunu, sona erme tarihinin bir anımsatıcısı olarak kullanabilirsiniz. Configuration Manager, çevrimiçi olarak sunulan yeni yazılım güncelleştirmelerini düzenli olarak denetlediği için bu tarih yararlıdır. Yazılım Güvencesi lisans durumunuz güncel olmalıdır, bu nedenle bu ek güncelleştirmeleri kullanmaya uygun olursunuz.  

    Daha fazla bilgi için bkz. [lisanslama ve dallar](../../../understand/learn-more-editions.md).  

5. **Microsoft yazılımı lisans koşulları** sayfasında, lisans koşullarını okuyun ve kabul edin.  

6. **Önkoşul lisanslar** sayfasında, önkoşul olan yazılımın lisans koşullarını okuyun ve kabul edin. Kurulum, yazılım yükleme ve gerektiğinde yazılımı site sistemlerine veya istemcilerine otomatik olarak yükler. Sonraki sayfaya geçmeden önce tüm koşulları kabul edin.  

7. **Önkoşul İndirmeleri** sayfasında, kurulumun en son önkoşul yeniden dağıtılabilir dosyalarını internetten indirmesi veya daha önce indirilen dosyaları kullanması gerektiğini belirtin:  

    - Kurulumun dosyaları şu anda indirmesini istiyorsanız **gerekli dosyaları indir**' i seçin. Ardından dosyaları depolamak için bir konum belirtin.  

    - Dosyaları daha önce [Kurulum Yükleyici](setup-downloader.md)'yi kullanarak indirdiyseniz, **daha önce indirilen dosyaları kullan**' ı seçin. Ardından indirme klasörünü belirtin.  

        > [!TIP]  
        > Daha önce indirilen dosyaları kullanıyorsanız, indirme klasörü yolunun dosyaların en son sürümünü içerdiğini doğrulayın.  

8. **Sunucu dili seçimi** sayfasında, Configuration Manager konsolu ve raporları için kullanılabilen dilleri seçin. (Varsayılan olarak İngilizce seçilidir ve kaldırılamaz.) Daha fazla bilgi için bkz. [dil paketleri](language-packs.md).  

9. **Istemci dili seçimi** sayfasında, istemci bilgisayarlar için kullanılabilir olan dilleri seçin. Ayrıca, mobil aygıt istemcileri için tüm istemci dillerinin etkinleştirilip etkinleştirilmeyeceğini belirtin. (Varsayılan olarak İngilizce seçilidir ve kaldırılamaz.)  

    > [!IMPORTANT]  
    > Bir merkezi yönetim sitesi kullandığınızda, merkezi yönetim sitesinde yapılandırdığınız istemci dillerinin her bir alt birincil sitede yapılandırdığınız tüm istemci dillerini içerdiğinden emin olun. Bir dağıtım noktasından yüklenen istemcilerin, üst katman sitesinden istemci dillerine erişimi vardır, ancak bir yönetim noktasından yüklenen istemciler, atanan birincil sitelerindeki istemci dillerine erişime sahip olmalıdır.  

10. **Site ve yükleme ayarları** sayfasında, yüklemekte olduğunuz yeni site için aşağıdaki ayarları belirtin:  

    - **Site kodu**: [bir hiyerarşideki her site kodu benzersiz olmalıdır](prepare-to-install-sites.md#bkmk_sitecodes). Üç alfasayısal basamak kullanın: A-Z ve 0 ile 9 arası. Site kodu klasör adlarında kullanıldığından, aşağıdakiler de dahil olmak üzere Windows ayrılmış adlarını kullanmayın:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > Kurulum, belirttiğiniz site kodunun zaten kullanımda olduğunu veya ayrılmış bir ad olup olmadığını doğrulamaz.  

    - **Site adı**: her site, siteyi belirlemenize yardımcı olabilecek bu kolay adı gerektirir.  

    - **Yükleme klasörü**: bu klasör Configuration Manager yüklemesinin yoludur. Site yüklendikten sonra konumu değiştiremezsiniz. Yol, Unicode karakterler veya sondaki boşluklar içeremez.  

        > [!NOTE]  
        > Varsayılan yükleme klasörünü kullanmak isteyip istemediğinizi göz önünde bulundurun. Bir üretim ortamında varsayılan işletim sistemi bölümünü kullanırsanız, gelecekte aşağıdaki sorunlarla karşılaşabilirsiniz:  
        >
        > - Configuration Manager, işletim sistemi bölümünde ek boş disk alanı kullanıyorsa, hiçbir Windows veya Configuration Manager düzgün şekilde çalışacaktır. Configuration Manager ayrı bir bölüme yüklerseniz, disk tüketimi işletim sistemini etkilemez.
        > - Configuration Manager performansı hızlı bir diskle daha iyidir. Bazı sunucu tasarımları, işletim sistemi diskini hız açısından iyileştirmaz.
        > - Configuration Manager yüklemenizi etkilemeden işletim sistemini hizmet edebilir, geri yükleyebilir veya yeniden yükleyebilirsiniz.  

11. **Site yükleme** sayfasında, senaryosuyla eşleşen aşağıdaki seçeneği kullanın:  

    - **Bir merkezi yönetim sitesi yüklüyorum:**  

        **Merkezi Yönetim sitesi yükleme** sayfasında, **Yeni bir hiyerarşide Ilk site olarak yükleme**' yi seçin ve ardından devam etmek için **İleri** ' yi seçin.  

    - **Tek başına bir birincisini merkezi yönetim sitesi olan bir hiyerarşide genişlettim:**  

        **Merkezi Yönetim sitesi yükleme** sayfasında, **mevcut bir bağımsız birincili bir hiyerarşiye genişlet**' i seçin. Ardından, tek başına birincil site sunucusunun FQDN 'sini belirtin ve devam etmek için **İleri** ' yi seçin.  

        Yeni Merkezi yönetim sitesini yüklemek için kullandığınız medya, birincil sitenin sürümüyle aynı olmalıdır.  

    - **Tek başına bir birincil site yüklüyorum:**  

        **Birincil site yükleme** sayfasında, **birincil siteyi tek başına site olarak yükleme**' yi seçin ve ardından **İleri**' yi seçin.  

    - **Bir alt birincil site yüklüyorum:**  

        **Birincil site yükleme** sayfasında, **birincil siteyi var olan bir hiyerarşiye Birleştir**' i seçin. Ardından merkezi yönetim sitesi için FQDN 'yi belirtin ve **İleri**' yi seçin.  

12. **Veritabanı bilgileri** sayfasında, aşağıdaki bilgileri belirtin:  

    - **SQL Server adı (FQDN)**: varsayılan olarak, bu değer site sunucusu bilgisayarına ayarlanır.  

        Özel bir bağlantı noktası kullanıyorsanız, bu bağlantı noktasını SQL Server FQDN 'sine ekleyin. SQL Server FQDN 'sini virgül ve sonra bağlantı noktası numarası ile izleyin. Örneğin, Server *SQLSERVER1.fabrikam.com*için, *1551*bağlantı noktasını belirtmek için aşağıdakileri kullanın:`SQLServer1.fabrikam.com,1551`  

    - **Örnek adı**: Bu değer varsayılan olarak boştur. Site sunucusu bilgisayarında varsayılan SQL örneğini kullanır.  

    - **Veritabanı adı**: varsayılan olarak, bu değer olarak `CM_<Sitecode>`ayarlanır. Bu değeri özelleştirebilirsiniz.  

    - **Hizmet Aracısı bağlantı noktası**: varsayılan olarak, bu değer 4022 varsayılan SQL Server hizmet Aracısı (SSB) bağlantı noktasını kullanacak şekilde ayarlanır. SQL, diğer sitelerdeki Site veritabanıyla doğrudan iletişim kurmak için onu kullanır.  

13. İkinci **veritabanı bilgileri** sayfasında, SQL Server veri dosyası için özel konumlar ve site veritabanı için SQL Server günlük dosyası belirtebilirsiniz:  

    - Varsayılan olarak, SQL Server için varsayılan dosya konumlarını kullanır.  

    - SQL Server kümesi kullandığınızda, özel dosya konumlarını belirtme seçeneği kullanılamaz.  

    - Önkoşul denetleyicisi, özel dosya konumları için boş disk alanı denetimi çalıştırmaz.  

14. **SMS sağlayıcısı ayarları** SAYFASıNDA, SMS sağlayıcısı 'nı yüklemek istediğiniz sunucu için FQDN 'yi belirtin.  

    - Varsayılan olarak, site sunucusunu belirtir.  

    - Site yüklendikten sonra, ek SMS Sağlayıcılarını yapılandırabilirsiniz. Daha fazla bilgi için bkz. [plan for SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

15. **Istemci Iletişim ayarları** sayfasında, tüm site sistemlerini ISTEMCILERDEN yalnızca HTTPS iletişimini kabul edecek şekilde mi yoksa her site sistem rolü için iletişim yönteminin mi yapılandırılacağını seçin.  

    **Tüm site sistemi rolleri istemcilerden yalnızca HTTPS iletişimini kabul et**' i seçtiğinizde, istemci bilgisayarın istemci kimlik doğrulaması için GEÇERLI bir PKI sertifikasına sahip olması gerekir. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Bu adım yalnızca birincil bir siteyi yüklediğinizde geçerlidir. Bir merkezi yönetim sitesi yüklüyorsanız, bu adımı atlayın.  

16. **Site sistemi rolleri** sayfasında, bir yönetim noktası mı yoksa dağıtım noktası mı yükleneceğini seçin. Kurulum tarafından yüklenmesini seçtiğiniz her rol için:  

    - Rolü barındıracak sunucunun **FQDN** 'sini girin. Ardından sunucunun destekleyeceği istemci bağlantı yöntemini seçin: HTTP veya HTTPS.  

    - **Tüm site sistem rolleri önceki sayfadaki istemcilerden yalnızca HTTPS iletişimini kabul et** ' i seçtiyseniz, istemci bağlantı ayarları OTOMATIK olarak https için yapılandırılır. Önceki sayfaya geri dönmediğiniz takdirde bu ayarı değiştiremezsiniz.  

    > [!NOTE]  
    > Bu adım yalnızca birincil bir siteyi yüklediğinizde geçerlidir. Bir merkezi yönetim sitesi yüklüyorsanız, bu adımı atlayın.  

    > [!NOTE]  
    > Site sistemi rollerini yüklemek için kurulum, **site sistemi yükleme hesabı**' nı kullanır. Bu, varsayılan olarak birincil sitenin bilgisayar hesabını kullanır. Bu hesap, site sistem rolünü yüklemek için uzak bilgisayarda bir yerel yönetici olmalıdır. Bu hesap gerekli izinlere sahip değilse, site sistemi yükleme hesapları olarak kullanılacak ek hesapları yapılandırdıktan sonra, site sistem rollerinin seçimini kaldırın ve daha sonra Configuration Manager konsolundan yükleme yapın. Daha fazla bilgi için bkz. [hesaplar](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. **Kullanım verileri** sayfasında, Microsoft 'un topladığı veriler hakkındaki bilgileri gözden geçirin ve ardından **İleri**' yi seçin. Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. **Hizmet bağlantı noktası kurulumu** sayfası yalnızca aşağıdaki senaryolarda kullanılabilir:  

    - Tek başına bir birincil site yüklerken.  

    - Bir merkezi yönetim sitesi yüklerken.  

    > [!NOTE]  
    > Bir alt birincil site yüklüyorsanız, bu adımı atlayın.  

     Bir merkezi yönetim sitesini bir site genişletme senaryosunun parçası olarak yüklüyorsanız ve bu rol tek başına birincil sitede zaten yüklüyse, önce bu rolü tek başına birincil siteden kaldırın. Hiyerarşide bu rolün yalnızca bir örneğine izin verilir ve yalnızca hiyerarşinin üst katman sitesinde desteklenir.  

     **Hizmet bağlantı noktası**için bir yapılandırma seçtikten sonra **İleri**' yi seçin. Kurulum tamamlandıktan sonra, bu yapılandırmayı Configuration Manager konsolu içinden değiştirebilirsiniz. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../configure/about-the-service-connection-point.md).  

19. **Ayarlar Özeti** sayfasında, seçtiğiniz ayarı gözden geçirin. Hazırsanız, önkoşul denetleyicisi ' ni başlatmak için **İleri** ' yi seçin.  

20. **Önkoşul yükleme denetimi** sayfasında, denetleyicinin tanımlayabileceği tüm sorunları listeler.  

    - Önkoşul denetleyicisi bir sorun bulduğunda, sorunu çözme hakkında ayrıntılar için listeden bir öğe seçin.  

    - Siteyi yüklemeye devam edebilmeniz için önce **başarısız** olan öğeleri çözün. Ayrıca, **Uyarı**durumunda olan öğeleri çözmeyi deneyin, ancak site yüklemesini engellemez.  

    - Sorunları çözdükten sonra, önkoşul denetleyicisi 'ni yeniden çalıştırmak için **denetimi Çalıştır** ' ı seçin.  

        Önkoşul denetleyicisi çalıştırıldığında ve hiçbir denetim **başarısız** durumu almadığınızda, site yüklemesini başlatmak için **yüklemeyi** Başlat ' ı seçebilirsiniz.  

    > [!TIP]  
    > Sihirbazın sağladığı geri bildirime ek olarak, **ConfigMgrPrereq. log** dosyasında önkoşul sorunlarıyla ilgili ek bilgiler bulabilirsiniz. Bu, siteyi yüklemekte olduğunuz bilgisayarın sistem sürücüsünün köküdür. Daha fazla bilgi için bkz. [önkoşul denetimleri listesi](list-of-prerequisite-checks.md).  

21. **Yükleme** sayfasında, kurulum yükleme durumunu görüntüler. Çekirdek site sunucusu yüklemesi tamamlandığında, Yükleme Sihirbazı 'nı **kapatabilirsiniz** . Sihirbazı kapattığınızda yükleme ve ilk site yapılandırması arka planda devam eder.  

    - Kurulum tamamlanmadan önce bir Configuration Manager konsolunu siteye bağlayabilirsiniz. Bu konsol salt okunurdur ve nesneleri ve ayarları görüntülemenize izin verir, ancak herhangi bir şeyi değiştiremezsiniz.  

    - Kurulum tamamlandıktan sonra, nesneleri ve ayarları düzenleyebilen bir konsola bağlanabilirsiniz.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a>Tek başına birincil siteyi genişletme

İlk siteniz olarak bağımsız bir birincil siteyi yüklediğinizde, daha sonra bir merkezi yönetim sitesi yükleyerek bu siteyi daha büyük bir hiyerarşiye genişletmeyi seçebilirsiniz.

Tek başına bir birincil siteyi genişlettiğinizde, mevcut tek başına birincil site veritabanını bir başvuru olarak kullanan yeni bir merkezi yönetim sitesi yüklersiniz. Yeni Merkezi Yönetim sitesi yüklendikten sonra, tek başına birincil site alt birincil site olarak çalışır.

- Tek başına birincil siteyi yalnızca yeni bir hiyerarşiye genişletebilirsiniz.  

- Yalnızca bir tek başına birincil siteyi belirli bir hiyerarşiye genişletebilirsiniz. Bu seçeneği, başka tek başına birincil siteleri aynı hiyerarşiye katmak için kullanamazsınız. Bunun yerine, verileri bir hiyerarşiden diğerine geçirmek için Geçiş Sihirbazı 'nı kullanın. Daha fazla bilgi için bkz. [hiyerarşiler arasında veri geçirme](../../../migration/migrate-data-between-hierarchies.md).  

- Tek başına bir siteyi merkezi yönetim sitesi olan bir hiyerarşiye genişlettikten sonra, ek alt birincil alt siteler ekleyebilirsiniz.  

- Bir birincil siteyi merkezi yönetim sitesi olan bir hiyerarşiden kaldırmak için öncelikle birincil siteyi kaldırın.  

Siteyi genişletmek için, aşağıdaki uyarılarla yeni bir merkezi yönetim sitesi yüklemek üzere Configuration Manager Kurulum Sihirbazı ' nı kullanın:  

- Tek başına birincil siteyle aynı Configuration Manager sürümünü kullanarak merkezi yönetim sitesini yükler.  

- Kurulum Sihirbazı ' nın **Başlarken** sayfasında, bir merkezi yönetim sitesi yükleme seçeneğini belirleyin. Kurulumun sonraki bir aşamasında, var olan bir tek başına birincil siteyi genişletme seçeneği arasından seçim yapabilirsiniz.  

- Yeni Merkezi Yönetim sitesi için **Istemci dili seçimi** sayfasını yapılandırırken, genişletmekte olduğunuz tek başına birincil site için yapılandırılmış olan istemci dillerini seçin.  

- **Site yükleme** sayfasında, tek başına birincil siteyi genişletme seçeneğini belirleyin.  

Tek başına bir birincil siteyi genişletmek için, önce [bir siteyi genişletme önkoşullarını](prerequisites-for-installing-sites.md#bkmk_expand)inceleyin. Ardından Bu makalenin önceki kısımlarında [birincil veya merkezi yönetim sitesi yüklemek için](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) yordamı kullanın.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a>İkincil site yükler

İkincil bir site yüklemek için Configuration Manager konsolunu kullanın.  

- Kullandığınız konsol, yeni ikincil sitenin üst sitesi olacak birincil siteye bağlı değilse, siteyi yüklemeye yönelik komut doğru birincil siteye çoğaltılır.  

- Site yüklemesini başlatmadan önce, Kullanıcı hesabınızın önkoşul izinlerine sahip olduğundan emin olun. Ayrıca, yeni ikincil siteyi barındıracak sunucunun ikincil site sunucusu olarak kullanım için tüm önkoşulları karşıladığından emin olun.  

- İkincil siteyi yüklediğinizde Configuration Manager, yeni siteyi üst birincil sitede yapılandırılan istemci iletişim bağlantı noktalarını kullanacak şekilde yapılandırır.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a>İkincil site yüklemek için işlem  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Yeni ikincil sitenin üst birincil sitesi olacak siteyi seçin.  

2. **Ikincil site oluşturma Sihirbazı 'nı**başlatmak Için şeritte **ikincil site oluştur** ' u seçin.  

3. **Başlamadan önce** sayfasında, listelenen birincil sitenin, yeni ikincil sitenin üst öğesi olmasını istediğiniz site olduğunu doğrulayın. Ardından **İleri**' yi seçin.  

4. **Genel** sayfasında, aşağıdaki ayarları belirtin:  

    - **Site kodu**: bir hiyerarşideki her site kodu benzersiz olmalıdır. Üç alfasayısal basamak kullanın: A-Z ve 0 ile 9 arası. Site kodu klasör adlarında kullanıldığından, aşağıdakiler de dahil olmak üzere Windows ayrılmış adlarını kullanmayın:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > Kurulum, belirttiğiniz site kodunun zaten kullanımda olduğunu veya ayrılmış bir ad olup olmadığını doğrulamaz.  

    - **Site sunucusu adı**: Bu değer, yeni ikincil sitenin yükleneceği sunucunun FQDN 'sidir.  

    - **Site adı**: her site, siteyi belirlemenize yardımcı olabilecek bu kolay adı gerektirir.  

    - **Yükleme klasörü**: bu klasör Configuration Manager yüklemesinin yoludur. Site yüklendikten sonra konumu değiştiremezsiniz. Yol, Unicode karakterler veya sondaki boşluklar içeremez.  

    > [!IMPORTANT]  
    > Bu sayfadaki ayrıntıları belirttikten sonra, sihirbazın **Özet** sayfasına doğrudan gitmek için **Özet** ' i seçebilirsiniz. Bu eylem, ikincil site seçeneklerinin geri kalanı için varsayılan ayarları kullanır.  
    > 
    > - Bu seçeneği yalnızca bu sihirbazdaki varsayılan ayarları öğreniyseniz ve kullanmak istediğiniz ayarlarsa kullanın.  
    > - Varsayılan ayarları kullandığınızda, sınır grupları dağıtım noktasıyla ilişkili değildir. İkincil site sunucusunu içeren sınır grupları yapılandırılana kadar istemciler, içerik kaynağı konumu olarak bu ikincil sitede yüklü olan dağıtım noktasını kullanmaz.  

5. **Yükleme kaynak dosyaları** sayfasında, ikincil site bilgisayarının siteyi yüklemek için kaynak dosyaları nasıl alacağını seçin.  

    CD 'yi kullandığınızda. Ağda paylaşılan veya hedef ikincil site sunucusuna yerel olarak kopyalanan en son kaynak dosyaları:  

    - **Sürüm 1802 ve öncesi**

        - CD. En son kaynak dosya konumu, **Redist**adlı bir klasör içerir. Bu **Redist** klasörünü **SMSSetup** klasörünün altında bir alt klasör olarak taşıyın.  

            > [!Note]  
            > Kurulum sırasında karma uyumsuzluğu hataları oluşursa, **Redist** klasörünü güncelleştirin. En son dosyaları almak için [Kurulum Yükleyici](setup-downloader.md) 'yi kullanın. Karma uyumsuzluğu hatasına neden olan dosyalar için, bunları güncelleştirilmiş **Redist** klasöründen **Smssetup\bin\x64** klasörüne de kopyalayın.

    - **Sürüm 1806 ve üzeri**<!-- SCCMDocs-pr issue 3164 -->

        - CD. En son kaynak dosya konumu, **Redist**adlı bir klasör içerir. Bu **Redist** klasörünü **SMSSetup** klasörünün altında bir alt klasör olarak taşıyın.  

        - Aşağıdaki dosyaları **Redist** klasöründen **Smssetup\bin\x64** klasörüne kopyalayın:  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Yeniden **dağıtım dosyalarından herhangi** bir dosya kullanılamıyorsa, Kurulum ikincil siteyi yükleyemez.  

    - İkincil site sunucusunun bilgisayar hesabı, kaynak dosya klasörü ve paylaşma için **okuma** izinlerine sahip olmalıdır.  

6. **SQL Server ayarları** sayfasında, kullanılacak SQL Server sürümünü belirtin ve ardından ilgili ayarları yapılandırın.  

    > [!NOTE]  
    > Kurulum, yüklemeye başlamadan bu sayfada girdiğiniz bilgileri doğrulamaz. Devam etmeden önce bu ayarları doğrulayın.  

    - **İkincil site bilgisayarına SQL Express 'in yerel bir kopyasını yükleyip yapılandırın**  

        - **SQL Server hizmet bağlantı noktası**: kullanılacak SQL Server Express için SQL Server hizmet bağlantı noktasını belirtin. Hizmet bağlantı noktası genellikle 1433 numaralı TCP bağlantı noktasını kullanmak üzere yapılandırılmıştır, ancak başka bir bağlantı noktası da yapılandırabilirsiniz.  

        - **SQL Server broker bağlantı noktası**: kullanılacak SQL Server Express için SQL Server hizmet Aracısı (SSB) bağlantı noktasını belirtin. Hizmet Aracısı tipik olarak 4022 numaralı TCP bağlantı noktasını kullanmak üzere yapılandırılmıştır, ancak farklı bir bağlantı noktası da yapılandırabilirsiniz. Başka bir site veya hizmetin kullandığı ve hiçbir güvenlik duvarı kısıtlaması engellenmeyen geçerli bir bağlantı noktası belirtin.  

    - **Mevcut bir SQL Server örneğini kullan**  

        - **Fqdn SQL Server**: SQL Server çalıştıran bılgısayar için FQDN 'yi gözden geçirin. İkincil site veritabanını barındırmak için SQL Server çalıştıran bir yerel sunucu kullanmanız gerekir ve bu ayarı değiştiremezsiniz.  

        - **SQL Server örneği**: ikincil site veritabanı olarak kullanılacak SQL Server örneğini belirtin. Varsayılan örneği kullanmak için bu seçeneği boş bırakın.  

        - **ConfigMgr Site veritabanı adı**: ikincil site veritabanı için kullanılacak adı belirtin.  

        - **SQL Server broker bağlantı noktası**: kullanılacak SQL Server için SQL Server hizmet Aracısı (SSB) bağlantı noktasını belirtin. Başka bir site veya hizmetin kullandığı ve güvenlik duvarı kısıtlaması bloğunun olmadığı geçerli bir bağlantı noktası belirtin.  

    > [!TIP]  
    > Configuration Manager desteklediği SQL Server sürümlerinin bir listesi için bkz. [desteklenen SQL Server sürümleri](../../../plan-design/configs/support-for-sql-server-versions.md).  

7. **Dağıtım noktası** sayfasında, dağıtım noktası için ikincil site sunucusuna yüklenecek ayarları yapılandırın.  

    - **Gerekli ayarlar:**  

        - **İstemci cihazlarının dağıtım noktasıyla nasıl iletişim kuracağını belirtin**: http ve https arasında seçim yapın.  

        - **Otomatik olarak imzalanan bir sertifika oluşturun veya BIR PKI istemci sertifikasını içeri aktarın**: kendinden imzalı bir sertifika kullanma veya PKI 'ınızdan bir sertifikayı içeri aktarma arasında seçim yapın. Otomatik olarak imzalanan bir sertifika, Configuration Manager istemcilerinden içerik kitaplığına anonim bağlantıların de izin vermenizi sağlar. Sertifika, dağıtım noktası durum iletileri göndermeden önce bir yönetim noktasına dağıtım noktasının kimliğini doğrulamak için kullanılır. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

    - **İsteğe bağlı ayarlar:**  

        - **Configuration Manager GEREKLIYSE IIS 'Yi yükleme ve yapılandırma**: daha önce yüklenmemişse, sunucuda Internet INFORMATION SERVICES (ııs) Configuration Manager yüklemek ve yapılandırmak için bu ayarı seçin. Tüm dağıtım noktalarında IIS gereklidir.  

            > [!NOTE]  
            > Bu ayar isteğe bağlı olsa da, bir dağıtım noktasının başarıyla yüklenebilmesi için önce IIS 'nin sunucuya yüklenmesi gerekir.  

        - **Bu dağıtım noktası için BranchCache 'i etkinleştirin ve yapılandırın**  

        - **Açıklama**: Bu değer, dağıtım noktasının tanımanıza yardımcı olması için kolay bir açıklamadır.  

        - **Önceden hazırlanan içerik için bu dağıtım noktasını etkinleştir**  

8. **Sürücü ayarları** sayfasında, ikincil site dağıtım noktası için sürücü ayarlarını belirtin.  

    İçerik kitaplığı ve paket paylaşımının iki disk sürücüsü için en fazla iki disk sürücüsü yapılandırabilirsiniz. Ancak, Configuration Manager, ilk ikisi yapılandırılan sürücü alanına ulaştığında ek sürücüler kullanabilir. **Sürücü ayarları** sayfası, disk sürücüleri için önceliği ve her disk sürücüsünde kalacak boş disk alanı miktarını yapılandırdığınız yerdir.  

    - **Ayrılan sürücü alanı (MB)**: Bu ayar için yapılandırdığınız değer, Configuration Manager farklı bir sürücü seçmeden önce sürücüdeki boş alan miktarını belirler ve kopyalama işlemini o sürücüye devam ettirir. İçerik dosyaları birden çok sürücüye yayılabilir.  

    - **Içerik konumları**: içerik kitaplığı ve paket paylaşımının içerik konumlarını belirtin. Configuration Manager, boş alan miktarı **ayrılan sürücü alanı (MB)** için belirtilen değere ulaşana kadar içeriği birincil içerik konumuna kopyalar.  

    Varsayılan olarak, içerik konumları **Otomatik**olarak ayarlanır. Birincil içerik konumu, yükleme sırasında en fazla disk alanına sahip disk sürücüsüne ayarlanır. İkincil konum, birincil sürücüden sonra en fazla boş disk alanına sahip disk sürücüsüne ayarlanır. Birincil ve ikincil sürücüler ayrılan sürücü alanına ulaştığında, Configuration Manager en fazla boş disk alanına sahip başka bir kullanılabilir sürücü seçer ve kopyalama işlemine devam eder.  

9. **Içerik doğrulama** sayfasında, dağıtım noktasındaki içerik dosyalarının bütünlüğünden doğrulanması gerekip gerekmediğini belirtin.  

    - Bir zamanlamaya göre İçerik doğrulamayı etkinleştirdiğinizde Configuration Manager işlemi zamanlanan saatte başlatır. Dağıtım noktasındaki tüm içerik doğrulanır.  

    - **İçerik doğrulama önceliğini**de yapılandırabilirsiniz.  

    - İçerik doğrulama işleminin sonuçlarını görüntülemek için, Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümünü seçin. Her paket türü için içeriği görüntüler. Bu türler uygulamalar, yazılım güncelleştirme paketleri ve önyükleme görüntülerini içerir.  

10. **Sınır grupları** sayfasında, bu dağıtım noktasının atandığı sınır gruplarını yönetin:  

    - İçerik dağıtımı sırasında istemciler, içerik için kaynak konumu olarak kullanmak üzere dağıtım noktasıyla ilişkili bir sınır grubunda olmalıdır.  

    - Bu sınır gruplarının dışındaki istemcilerin geri dönmesine ve tercih edilen dağıtım noktası kullanılabilir olmadığında dağıtım noktasını içerik için kaynak konumu olarak kullanmasına izin vermek için **içerik için geri dönüş kaynak konumuna Izin ver** seçeneğini belirleyebilirsiniz.  

        Daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. **Özet** sayfasında, ayarları doğrulayın ve ardından ikincil siteyi yüklemek için **İleri** ' yi seçin. Sihirbaz **tamamlama** sayfasını gösterdiğinde Sihirbazı kapatabilirsiniz. İkincil site yüklemesi arka planda devam eder.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a>İkincil site yükleme durumunu doğrulama  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Yüklemekte olduğunuz ikincil siteyi seçin ve ardından şeritte **yükleme durumunu göster** ' i seçin.  

    > [!TIP]  
    > Aynı anda birden fazla ikincil site yüklediğinizde, önkoşul denetleyicisi her seferinde tek bir siteye karşı çalışır. Sonraki siteyi denetlemeye başlamadan önce bir siteyi tamamlaması gerekir.  
