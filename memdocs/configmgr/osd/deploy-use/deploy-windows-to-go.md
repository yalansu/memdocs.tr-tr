---
title: Windows to go dağıtma
titleSuffix: Configuration Manager
description: Windows to go 'nun bir dış sürücüden önyüklenen bir Windows To Go çalışma alanı oluşturmak için Configuration Manager nasıl sağlanacağını öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3cf735dfa2dd73ed39a24c2d674a966acddf05a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125126"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Windows to go 'Yu Configuration Manager ile dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konuda, Configuration Manager Windows to go sağlama adımları sağlanmaktadır. Windows To Go, Windows 8'in, bilgisayarda çalıştırılan işletim sisteminden bağımsız olarak, Windows 7 veya Windows 8 sertifika gereksinimlerini karşılayan bilgisayarlarda bir USB bağlantılı harici sürücüden önyüklenebilecek bir Windows To Go çalışma alanının oluşturulmasını sağlayan bir kurum özelliğidir. Windows To Go çalışma alanları, kurumların masaüstü ve dizüstü bilgisayarları için kullandığı görüntünün aynısını kullanabilir ve aynı şekilde yönetilebilir.  

 Windows to go hakkında daha fazla bilgi için bkz. [Windows to go özelliğine genel bakış](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11)).  

## <a name="provision-windows-to-go"></a>Windows To Go Sağlama  
 Windows To Go, USB bağlantılı harici sürücüde depolanan bir işletim sistemidir. Windows To Go sürücüsünü, diğer işletim sistemi dağıtımlarını sağladığınıza çok benzer şekilde sağlayabilirsiniz. Ancak, Windows To Go, kullanıcı odaklı ve yüksek mobiliteli bir çözüm olacak şekilde tasarlandığından, bu sürücüleri sağlamak için biraz daha farklı bir yaklaşım sergilemelisiniz.  

 Yüksek bir seviyede, Windows To Go, Windows To Go cihazını ve önceden hazırlanan içeriği işletim sistemi dağıtımına yönelik olarak yapılandırmanızı sağlayan iki aşamalı bir dağıtımdır. Bunu kullanıcıya en az etkiyle elde edebilir ve kullanıcı bilgisayarının kapalı kalma süresini sınırlayabilirsiniz. Bilgisayarı önceden hazırladıktan sonra, bilgisayarın kullanıcı için hazır olduğundan emin olmak için sağlama işlemini tamamlamalısınız. Sağlama işlemi, geçerli işletim sistemi dağıtım işlemiyle benzerdir. Aşağıda, içeriği önceden hazırlamak ve Windows To Go'yu sağlamak için genel iş akışı listelenmiştir:  

1.  [Windows to go sağlama önkoşulları](#BKMK_Prereqs)  

2.  [Önceden hazırlanan ortam oluşturma](#BKMK_CreatePrestagedMedia)  

3.  [Windows To Go Oluşturan paketi oluşturma](#BKMK_CreatePackage)  

4.  [Windows To Go için BitLocker'ı etkinleştirmek üzere görev dizisini güncelleştirme](#BKMK_UpdateTaskSequence)  

5.  [Windows To Go oluşturucu paketini ve görev dizisini dağıtma](#BKMK_Deployments)  

6.  [Kullanıcının Windows To Go Oluşturucuyu çalıştırması](#BKMK_UserExperience)  

7.  [Configuration Manager, Windows To Go sürücüsünü yapılandırır ve aşamalar](#BKMK_ConfigureStageDrive)  

8.  [Kullanıcı Windows 8 ' de oturum açar](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Windows To Go sağlama önkoşulları  
 Windows to go 'yu sağlamadan önce Configuration Manager ' de şunları tamamlamalısınız:  

-   **Bir önyükleme görüntüsünü bir dağıtım noktasına dağıtma**  

     Önceden hazırlanan medya oluşturmadan önce, önyükleme görüntüsünü bir dağıtım noktasına dağıtmanız gerekir.  

    > [!NOTE]  
    >  Önyükleme görüntüleri, Configuration Manager ortamınızdaki hedef bilgisayarlara işletim sistemi yüklemek için kullanılır. Windows PE'nin, işletim sistemini ve gerekli tüm cihaz sürücülerini yükleyen bir sürümünü içerirler. Configuration Manager iki önyükleme görüntüsü sağlar: biri x86 platformlarını ve diğeri de x64 platformlarını destekler. Kendi önyükleme görüntülerinizi de oluşturabilirsiniz. Daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

-   **Windows 8 işletim sistemi görüntüsünü bir dağıtım noktasına dağıtma**  

     Önceden hazırlanan medya oluşturmadan önce, Windows 8 işletim sistemi görüntüsünü bir dağıtım noktasına dağıtmanız gerekir.  

    > [!NOTE]  
    >  İşletim sistemi görüntüleri .WIM biçiminde dosyalardır ve bir işletim sistemini bilgisayara başarıyla yüklemek ve yapılandırmak için gereken başvuru dosya ve klasörlerinden oluşan sıkıştırılmış bir koleksiyonu temsil ederler. Daha fazla bilgi için bkz. [işletim sistemi görüntülerini yönetme](../get-started/manage-operating-system-images.md).  

-   **Windows 8 Dağıtımı için bir Görev Dizisi Oluşturma**  

     Windows 8 dağıtımı için, önceden hazırlanan medya oluşturduğunuzda bakacağınız bir görev dizisi oluşturmanız gerekir. Daha fazla bilgi için bkz. [görevleri otomatikleştirmek için görev dizilerini yönetme](manage-task-sequences-to-automate-tasks.md).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a>Önceden hazırlanan medya oluşturma  
 Ön hazırlığı yapılan medya, hedef bilgisayarı çalıştırmak için kullanılan önyükleme görüntüsünü ve hedef bilgisayara uygulanan işletim sistemi görüntüsünü içerir. Önceden hazırlanmış medyayla sağladığınız bilgisayar, önyükleme görüntüsü kullanılarak başlatılabilir. Bilgisayar ardından, tam bir işletim sistemi dağıtımı yüklemek için, var olan bir işletim sistemi dağıtımı görev dizisi çalıştırabilir. İşletim sistemini dağıtan görev dizisi, medyada yer almaz.  

 Önceden hazırlama aşamasında, işletim sistemi görüntüsü ve önyükleme görüntüsüne ek olarak uygulamalar ve aygıt sürücüleri gibi içerik ekleyebilirsiniz. Böylelikle, bir işletim sistemini dağıtmak için geçen süre azaltılır ve içerik zaten sürücüde olduğundan ağ trafiği azaltılır.  

 Önceden hazırlanmış medyayı oluşturmak için aşağıdaki yordamı kullanın.  

#### <a name="to-create-prestaged-media"></a>Önhazırlığı yapılmış medya oluşturmak için  

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ne tıklayın.  

3. **Giriş** sekmesinde, **Oluştur** grubunda, Görev Sırası Medyası Oluşturma Sihirbazı'nı başlatmak için **Görev Sırası Medyası Oluştur** 'u tıklatın.  

4. **Medya Türü Seçin** sayfasında, aşağıdaki bilgileri belirttikten sonra **İleri**'y tıklatın.  

   -   **Önhazırlığı yapılan medya**'yı seçin.  

   -   Kullanıcı müdahalesi olmadan Windows To Go dağıtımına önyüklemesi için **Katılımsız işletim sistemi dağıtımına izin ver** seçeneğini tıklatın.  

       > [!IMPORTANT]  
       >  Bu seçeneği, SMSTSPreferredAdvertID özel değişkeniyle (bu yordamda daha sonra ayarlanır) kullandığınızda, kullanıcı etkileşimi gerekmez ve bilgisayar, bir Windows To Go sürücüsü algıladığında otomatik olarak Windows To Go dağıtımına önyükler. Medya parola korumalı olarak yapılandırılmışsa da kullanıcıya parola sorulur. SMSTSPreferredAdvertID değişkenini yapılandırmadan **Katılımsız işletim sistemi dağıtımına izin ver** ayarını kullanırsanız, görev dizisini dağıttığınızda bir hata oluşur.  

5. **Medya Yönetimi** sayfasında, aşağıdaki bilgileri belirtin ve ardından **İleri**'yi tıklatın.  

   -   Bir yönetim noktasının site sınırlarındaki istemci konumuna bağlı olarak medyayı başka bir yönetim noktasına yönlendirmesine izin vermek istiyorsanız **Dinamik medya** 'yı seçin.  

   -   Medyanın yalnızca belirtilen yönetim noktasıyla bağlantı kurmasını istiyorsanız **Site tabanlı medya** 'yı seçin.  

6. **Medya Özellikleri**  sayfasında, aşağıdaki bilgileri belirtin ve ardından **İleri**'ye tıklayın.  

   -   **Oluşturan**: Medyayı oluşturan kişiyi belirtin.  

   -   **Sürüm**: Medyanın sürüm numarasını belirtin.  

   -   **Açıklama**: Medyanın hangi amaçla kullanıldığına ilişkin benzersiz bir açıklama belirtin.  

   -   **Medya dosyası**: Çıkış dosyalarının adını ve yolunu belirtin. Sihirbaz çıkış dosyalarını bu konuma yazar. Örneğin: ** \\ \SunucuAdı \ KlasörAdı \ OutputFile.exe**  

7. **Güvenlik** sayfasında, aşağıdaki bilgileri belirtin ve **İleri**'yi tıklatın.  

   -   Medyanın Configuration Manager tarafından yönetilmeyen bir bilgisayara bir işletim sistemi dağıtmasına izin vermek için **bilinmeyen bilgisayar desteğini etkinleştir** ' i seçin. Configuration Manager veritabanında bu bilgisayarların kaydı yoktur. Bilinmeyen bilgisayarlar aşağıdakileri içerir:  

       -   Configuration Manager istemcisinin yüklü olmadığı bir bilgisayar  

       -   Configuration Manager içine aktarılmayan bir bilgisayar  

       -   Configuration Manager tarafından bulunmayan bir bilgisayar  

   -   **Medyayı parolayla koru** seçin ve medyanın yetkisiz erişimden korunmasına yardımcı olmak için güçlü bir parola girin. Parola belirtirseniz kullanıcının önhazırlığı yapılan medyayı kullanabilmesi için o parolayı girmesi gerekir.  

       > [!IMPORTANT]  
       >  En iyi güvenlik uygulaması olarak, önhazırlığı yapılan medyayı korumaya yardımcı olmak için her zaman parola atayın.  

       > [!NOTE]  
       >  Ön hazırlığı yapılan medyayı bir parolayla koruduğunuzda, medya **Katılımsız işletim sistemi dağıtımına izin ver** seçeneğiyle yapılandırılmış olsa bile kullanıcın parola girmesi istenir.  

   -   HTTP iletişimleri için, **Otomatik olarak imzalanan medya sertifikası oluştur**'u seçin ve sertifika için başlangıç ve sona erme tarihi belirtin.  

   -   HTTPS iletişimleri için, **PKI sertifikasını içeri aktar**'ı seçin ve içeri aktarılacak sertifikayı ve parolasını belirtin.  

        Önyükleme görüntüleri için kullanılan bu istemci sertifikası hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Kullanıcı cihaz benzeşimi**: Configuration Manager Kullanıcı merkezli yönetimi desteklemek için, medyanın kullanıcıları hedef bilgisayarla nasıl ilişkilendirmesini istediğinizi belirtin. İşletim sistemi dağıtımının Kullanıcı cihaz benzeşimini nasıl desteklediği hakkında daha fazla bilgi için bkz. [kullanıcıları bir hedef bilgisayarla ilişkilendirme](../get-started/associate-users-with-a-destination-computer.md).  

       -   Medyanın kullanıcıları hedef bilgisayarla otomatik olarak ilişkilendirmesini istiyorsanız **Otomatik onayla kullanıcı aygıtı benzeşimine izin ver** 'i belirtin. Bu işlev, işletim sistemini dağıtan görev sırasının eylemlerine bağlıdır. Bu senaryoda görev sırası, işletim sistemini hedef bilgisayara dağıtırken belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur.  

       -   Medyanın kullanıcıları hedef bilgisayarla onay verildikten sonra ilişkilendirmesini istiyorsanız **Kullanıcı aygıtı benzeşimi bekleyen yönetici onayına izin ver** 'i belirtin. Bu işlev, işletim sistemini dağıtan görev sırasının kapsamına bağlıdır. Bu senaryoda, görev sırası belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur, ancak işletim sistemi dağıtılmadan önce yönetici kullanıcıdan onay bekler.  

       -   Medyanın kullanıcıları hedef bilgisayarla ilişkilendirmesini istemiyorsanız **Kullanıcı aygıtı benzeşimine izin verme** 'yi belirtin. Bu senaryoda görev sırası, işletim sistemini dağıtırken kullanıcıları hedef bilgisayarla ilişkilendirmez.  

8. **Görev Dizisi** sayfasında, önceki bölümde oluşturduğunuz Windows 8 görev dizisini belirtin.  

9. **Önyükleme görüntüsü** sayfasında aşağıdaki ayarları belirtin ve **İleri**'yi tıklatın.  

    > [!IMPORTANT]  
    >  Dağıtılan önyükleme görüntüsünün yapısı, hedef bilgisayarın yapısına uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. EFI modundaki Windows 8 lisanslı bilgisayarlar için bir x64 önyükleme yansıması seçmeniz gerekir.  

    -   **Önyükleme görüntüsü**: Hedef bilgisayarı başlatmak için önyükleme görüntüsünü belirtin.  

    -   **Dağıtım noktası**: Önyükleme görüntüsünü barındıran dağıtım noktasını belirtin. Sihirbaz önyükleme görüntüsünü dağıtım noktasından alır ve medyaya yazar.  

        > [!NOTE]  
        >  Yönetim kullanıcısının, dağıtım noktasındaki önyükleme görüntüsü içeriğine **Okuma** erişim haklarına sahip olması gerekir. Daha fazla bilgi için bkz. [paket erişim hesabı](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Bu sihirbazın **Medya Yönetimi** sayfasında **Site tabanlı medya** seçtiyseniz, **Yönetim noktası** kutusunda, birincil bir siteden bir yönetim noktası belirtin.  

    -   Bu sihirbazın **Medya Yönetimi** sayfasında **Dinamik medya** 'yı seçtiyseniz, **İlişkili yönetim noktaları** kutusunda, kullanılacak birincil site yönetim noktalarını ve ilk iletişimler için bir öncelik sırası belirtin.  

10. **Görüntüler** sayfasında, aşağıdaki bilgileri belirtin ve ardından **İleri**'yi tıklatın.  

    -   **Görüntü paketi**: Windows 8 işletim sistemi görüntüsünü içeren paketi belirtin.  

    -   **Görüntü dizini**: Pakette birden çok işletim sistemi görüntüsü yer alıyorsa, dağıtılacak görüntüyü belirtin.  

    -   **Dağıtım noktası**: İşletim sistemi görüntü paketini barındıran dağıtım noktasını belirtin. Sihirbaz, işletim sistemi görüntüsünü dağıtım noktasından alır ve medyaya yazar.  

        > [!NOTE]  
        >  Yönetim kullanıcısının, dağıtım noktasındaki işletim sistemi görüntüsü içeriğine **Okuma** erişim haklarına sahip olması gerekir. Daha fazla bilgi için bkz. [paket erişim hesabı](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. **Uygulama Seç** sayfasında, medya dosyasına eklenecek uygulama içeriğini seçin ve ardından **İleri**'yi tıklatın.  

12. **Paket Seç** sayfasında, medya dosyasına eklenecek uygulama paketi içeriğini seçin ve ardından **İleri**'yi tıklatın.  

13. **Sürücü Paketi Seç** sayfasında, medya dosyasına eklenecek sürücü paketi içeriğini seçin ve ardından **İleri**'yi tıklatın.  

14. **Dağıtım Noktaları** sayfasında, görev dizisinin gerektirdiği içeriği içeren bir ya da birden çok dağıtım noktasını seçin ve **İleri**'yi tıklatın.  

15. **Özelleştirme** sayfasında, aşağıdaki bilgileri belirtin ve **İleri**'ye tıklayın.  

    - **Değişkenler**: Görev dizisinin işletim sistemini dağıtmak için kullandığı değişkenleri belirtin. Windows To Go için, aşağıdaki biçimi kullanarak Windows To Go dağıtımını otomatik olarak seçmek için SMSTSPreferredAdvertID değişkenini kullanın:  

       SMSTSPreferredAdvertID = {*DeploymentID*}, DeploymentID, Windows To Go sürücüsü için sağlama işlemini tamamlamak üzere kullanacağınız görev dizisiyle ilişkili dağıtım kimliğidir.  

      > [!TIP]  
      >  Bu değişkeni, katılımsız çalışmak üzere ayarlanan bir görev dizisiyle (bu yordamda daha önce ayarlanır) kullandığınızda, kullanıcı etkileşimi gerekmez ve bilgisayar, bir Windows To Go sürücüsü algıladığında otomatik olarak Windows To Go dağıtımına önyüklenir. Medya parola korumalı olarak yapılandırılmışsa da kullanıcıya parola sorulur.  

    - **Başlatma öncesi komutlar**: Görev dizisi çalışmadan önce çalıştırmak istediğiniz başlatma öncesi komutlarını belirtin. Başlatma öncesi komutlar, görev dizisi işletim sistemini yüklemek üzere çalışmadan önce, Windows PE'de kullanıcıyla etkileşime girebilen bir betik veya yürütülebilir dosya olabilir. Windows To Go dağıtımı için aşağıdakileri yapılandırın:  

      - **OSDBitLockerPIN**: Windows To Go için BitLocker bir parola gerektirir. Windows To Go sürücüsü için BitLocker parolasını ayarlamak için, **OSDBitLockerPIN** değişkenini, başlatma öncesi bir komutun parçası olarak ayarlayın.  

        > [!WARNING]  
        >  BitLocker, parola için etkinleştirildikten sonra, bilgisayarın Windows To Go sürücüsüne önyüklendiği her seferinde kullanıcının parolayı girmesi gerekir.  

      - **SMSTSUDAUsers**: Hedef bilgisayarın birincil kullanıcısını belirtir. Bu değişkeni, daha sonra kullanıcı ve aygıtı ilişkilendirmek üzere kullanılabilecek, kullanıcı adını toplamak için kullanın. Daha fazla bilgi için bkz. [kullanıcıları bir hedef bilgisayarla ilişkilendirme](../get-started/associate-users-with-a-destination-computer.md).  

        > [!TIP]  
        >  Kullanıcı adını almak için, başlatma öncesi komutun parçası olarak bir giriş kutusu oluşturabilir, kullanıcının kullanıcı adını girmesini sağlayabilir ve ardından değişkeni değerle ayarlayabilirsiniz. Örneğin, başlatma öncesi komut betik dosyasına aşağıdaki satırları ekleyebilirsiniz:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Başlatma öncesi komutunuz olarak kullanılacak bir betik dosyası oluşturma hakkında daha fazla bilgi için bkz. [görev dizisi medyası Için başlatma öncesi komutlar](../understand/prestart-commands-for-task-sequence-media.md).  

16. Sihirbazı tamamlayın.  

    > [!NOTE]  
    >  Sihirbazın önceden hazırlanmış medya dosyasını tamamlaması uzun sürebilir.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a>Windows to go oluşturan paketi oluşturma  
 Windows To Go dağıtımının parçası olarak, önceden hazırlanmış medya dosyasını dağıtacağınız bir paket oluşturmanız gerekir. Paketin, Windows To Go sürücüsünü yapılandıran ve önceden hazırlanmış medyayı sürücüye çıkaran aracı içermesi gerekir. Windows To Go Oluşturan paketini oluşturmak için aşağıdaki yordamı kullanın.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Windows To Go Oluşturan paketi oluşturmak için  

1. Windows To Go Oluşturan paket dosyalarını barındıracak sunucuda, paket kaynak dosyaları için bir kaynak klasör oluşturun.  

   > [!NOTE]  
   >  Site sunucusunun bilgisayar hesabının, kaynak klasöre **Okuma** erişim haklarına sahip olması gerekir.  

2. [Create prestaged media](#BKMK_CreatePrestagedMedia) bölümünde oluşturduğunuz önceden hazırlanmış medya dosyasını, paket kaynak klasörüne kopyalayın.  

3. Windows To Go Oluşturan aracını (WTGCreator.exe) paket kaynak klasörüne kopyalayın. Oluşturan Aracı, herhangi bir birincil site sunucusunda şu konumda bulunur: <*ConfigMgr>* ınstallasd\tools\wtg\creator.  

4. Paket ve Program Oluşturma Sihirbazı'nı kullanarak bir paket ve program oluşturun.  

5. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

6. **Yazılım Kitaplığı** çalışma alanında **Uygulama Yönetimi**'ni genişletin ve **Paketler**'i tıklatın.  

7. **Giriş** sekmesindeki **Oluştur** grubunda **Paket Oluştur**'u tıklatın.  

8. **Paket** sayfasında paketin adını ve açıklamasını belirtin. Örneğin, paket adı için **Windows to go** girin ve paket açıklaması için **Configuration Manager kullanarak bir Windows to go sürücüsü yapılandırmak üzere paketi** belirtin.  

9. **Bu paket kaynak dosyaları içerir**seçin, adım 1'de oluşturduğunuz paket kaynak klasörüne giden yolu belirtin ve ardından **İleri**'yi tıklatın.  

10. **Program Türü** sayfasında, **Standart program**'ı seçin ve ardından **İleri**'yi tıklatın.  

11. **Standart Program** sayfasında, aşağıdakileri belirtin:  

    -   **Ad**: Programın adını belirtin. Örneğin, program adı için **Creator** yazın.  

    -   **Komut Satırı**: **WTGCreator.exe /wim:PrestageName.wim**yazın; burada PrestageName, oluşturduğunuz ve Windows To Go Oluşturucu paketi için paket kaynak klasörüne kopyaladığınız önceden hazırlanmış dosyanın adıdır.  

         İsteğe bağlı olarak, aşağıdaki seçenekleri ekleyebilirsiniz:  

        -   **enableBootRedirect**: Windows To Go başlatma seçeneklerini, önyükleme yeniden yönlendirmesine izin verecek şekilde değiştirmek için komut satırı seçeneği. Bu seçeneği kullandığınızda, önyükleme sırasını bilgisayar belleniminde değiştirmeye ya da kullanıcının başlatma sırasında bir önyükleme seçenekleri listesinden seçim yapmasına gerek olmadan, bilgisayar USB'den önyüklenir. Bir Windows To Go sürücüsü algılanırsa, bilgisayar o sürücüye önyüklenir.  

    -   **Çalıştır**: Programı, sistem ve program varsayılanlarına dayanarak çalıştırmak için **Normal** seçeneğini belirtin.  

    -   **Program çalışabilir**: Programın yalnızca bir kullanıcı oturum açtığında çalışıp çalışamayacağını belirtin.  

    -   **Çalıştırma modu**: Programın, oturum açmış kullanıcılarla mı yoksa yönetim izinleriyle mi çalıştırılacağını belirtin. Windows To Go Oluşturan, çalıştırmak için, yükseltilmiş izinler gerektirir.  

    -   **Kullanıcıların program yüklemesini görüntülemesine ve etkileşimde bulunmasına izin ver**'i seçin ve ardından **İleri**'yi tıklatın.  

12. Gereksinimler sayfasında, aşağıdakileri belirtin:  

    - **Platform gereksinimleri**: Sağlamaya izin vermek için, geçerli Windows 8 platformlarını seçin.  

    - **Tahmini disk alanı**: Windows To Go Oluşturucu için paket kaynağı klasörünün boyutunu belirtin.  

    - **İzin verilen en fazla çalışma süresi (dakika)**- Programın istemci bilgisayarda çalışması beklenen en uzun süreyi belirtir. Varsayılan olarak bu değer 120 dakikaya ayarlanır.  

      > [!IMPORTANT]  
      >  Bu program çalıştırıldığı koleksiyon için bakım pencereleri kullanıyorsanız **İzin verilen en fazla çalışma süresi** değerinin zamanlanan bakım penceresinden daha uzun olması durumunda bir çakışma meydana gelebilir. İzin verilen en fazla çalışma süresi **Bilinmiyor**olarak ayarlanırsa bakım penceresi sırasında başlatılır, ancak bakım penceresi kapatıldıktan sonra tamamlanana veya başarısız olana kadar devam eder. İzin verilen en fazla çalışma süresini kullanılabilir bakım penceresi uzunluğunu aşan belirli bir süreye ayarlarsanız (Bilinmiyor olarak ayarlamazsanız) bu program çalışmaz.  

      > [!NOTE]  
      >  Değer **bilinmiyor**olarak ayarlanırsa Configuration Manager izin verilen en fazla çalışma süresini 12 saate (720 dakika) ayarlar.  

      > [!NOTE]  
      >  En fazla çalışma süresi (Kullanıcı tarafından veya varsayılan değer olarak ayarlanır) aşılırsa, **yönetici haklarıyla Çalıştır** seçilirse ve **kullanıcıların program yüklemesini görüntülemesine ve bunlarla etkileşime girmesine Izin ver** **standart program** sayfasında seçili değilse, Configuration Manager programı sonlandırır.  

      **İleri** 'yi tıklatın ve sihirbazı tamamlayın.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a>Windows To Go için BitLocker 'ı etkinleştirmek üzere görev dizisini güncelleştirme  
 Windows To Go, TPM kullanmadan bir dış önyüklenebilir sürücüde BitLocker'ı etkinleştirir. Bu nedenle, Windows To Go sürücüsünde BitLocker'ı yapılandırmak için ayrı bir araç kullanmanız gerekir. BitLocker'ı etkinleştirmek için **Windows'u ve ConfigMgr'yi Kur** adımından sonraki görev sırasına bir eylem eklemeniz gerekir.  

> [!NOTE]  
>  Windows To Go için BitLocker bir parola gerektirir. [Create prestaged media](#BKMK_CreatePrestagedMedia) adımında OSDBitLockerPIN değişkenini kullanarak parolayı başlatma öncesi komutun bir parçası olarak ayarlarsınız.  

 Windows To Go için BitLocker'ı etkinleştirmek üzere Windows 8 görev sırasını güncelleştirmek için aşağıdaki yordamı kullanın.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>BitLocker'ı etkinleştirmek üzere Windows 8 görev sırasını güncelleştirmek için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım Kitaplığı** çalışma alanında **Uygulama Yönetimi**'ni genişletin ve **Paketler**'i tıklatın.  

3.  **Giriş** sekmesindeki **Oluştur** grubunda **Paket Oluştur**'u tıklatın.  

4.  **Paket** sayfasında paketin adını ve açıklamasını belirtin. Örneğin, paket adı için **BitLocker for Windows To Go** yazın ve paket açıklaması için **Package to update BitLocker for Windows To Go** belirtin.  

5.  **Bu paket, kaynak dosyalar içeriyor**öğesini seçin, Windows To Go için BitLocker aracının konumunu belirtin ve ardından **İleri**'yi tıklatın. BitLocker Aracı, her bir Configuration Manager birincil site sunucusunda şu konumda kullanılabilir: <*Configmgrınstalyüklemeklasörü*> \OSD\Tools\WTG\BitLocker\  

6.  **Program Türü** sayfasında **Program oluşturma**öğesini seçin.  

7.  **İleri** 'yi tıklatın ve sihirbazı tamamlayın.  

8.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

9. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ne tıklayın.  

10. Önceden hazırlanmış medyada başvurduğunuz Windows 8 görev sırasını seçin.  

11. **Giriş** sekmesinde, **Görev Sırası** grubunda, **Düzenle**'ye tıklayın.  

12. **Windows'u ve ConfigMgr'yi Kur** adımını, **Ekle**, **Genel**ve ardından **Komut Satırını Çalıştır**öğesini tıklatın. Komut Satırını Çalıştır adımı, Windows'u ve ConfigMgr'yi Kur adımının sonrasına eklenir.  

13. **Komut Satırını Çalıştır** adımının **Özellikler** sekmesinde aşağıdakileri ekleyin:  

    1.  **Ad**: Komut satırı için **Enable BitLocker for Windows To Go**gibi bir ad belirtin.  

    2.  **Komut satırı**: i386\osdbitlocker_wtg.exe/Enable/pwd: < *none&#124;ad*>  

         Parametreler:  

        -   /PWD: <None&#124;AD>-BitLocker parola kurtarma modunu belirtin. Bu parametre, komut satırında /Enable parametresini kullanmanızı gerektirir.  

             BitLocker Sürücü Şifrelemesini yapılandırarak BitLocker korumalı sürücülerin kurtarma bilgilerini Active Directory Etki Alanı Hizmetlerine (AD DS) yedeklemek için **AD** öğesini seçin. BitLocker korumalı bir sürücünün kurtarma parolalarının yedeklenmesi, sürücünün kilitlenmesi durumunda yönetim kullanıcılarının sürücüyü kurtarmasına imkan tanır. Bu durum kuruluşa ait şifrelenmiş verilere yetkili kullanıcıların her zaman erişebilmesini sağlar. **Hiçbiri**seçeneğini belirttiğinizde kurtarma parolasının veya kurtarma anahtarının bir kopyasının saklanması kullanıcının sorumluluğundadır. Kullanıcı bu bilgileri kaybeder veya kuruluştan ayrılmadan önce sürücü şifresini çözmeyi ihmal ederse yönetim kullanıcıları sürücüye kolayca erişemez.  

        -   /wait: <TRUE&#124;FALSE>-görev dizisinin tamamlanmadan önce şifrelemenin tamamlanmasını bekleyip beklemediğini belirtin.  

    3.  **Paket**öğesini seçin ve ardından bu yordamın başlangıcında oluşturduğunuz paketi belirtin.  

    4.  **Seçenekler** sekmesinde aşağıdaki koşulları ekleyin:  

        -   Koşul = Görev Sırası Değişkeni  

        -   Değişken = _SMSTSWTG  

        -   Koşul = Eşittir  

        -   Değer = True  

    > [!NOTE]  
    >  Yeni komut satırı adımından sonra gelme olasılığı bulunan **BitLocker'ı Etkinleştir** adımı, Windows To Go için BitLocker'ı etkinleştirmek üzere kullanılmaz. Ancak, bu adımı bir Windows To Go sürücüsü kullanmayan Windows 8 dağıtımları için kullanmak üzere görev sırasında tutabilirsiniz.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a>Windows To Go Oluşturucu paketini ve görev dizisini dağıtma  
 Windows To Go karma bir dağıtım işlemidir. Bu nedenle Windows To Go Oluşturucu paketini ve Windows 8 görev sırasını dağıtmanız gerekir. Dağıtım işlemini tamamlamak için aşağıdaki yordamları kullanın.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Windows To Go Oluşturucu paketini dağıtmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım Kitaplığı** çalışma alanında **Uygulama Yönetimi**'ni genişletin ve **Paketler**'i tıklatın.  

3.  [Windows To Go Oluşturan paketi oluşturma](#BKMK_CreatePackage) adımında oluşturduğunuz Windows To Go paketini seçin.  

4.  **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıt**'a tıklayın.  

5.  **Genel** sayfasında, aşağıdaki ayarları belirtin:  

    1.  **Yazılım**: Windows To Go paketinin seçildiğini doğrulayın.  

    2.  **Koleksiyon**: Windows To Go paketini dağıtmak istediğiniz koleksiyonu seçmek için **Gözat** öğesine tıklayın.  

    3.  **Bu koleksiyonla ilişkili varsayılan dağıtım noktası gruplarını kullan**: Paket içeriğini koleksiyonun varsayılan dağıtım noktası grubunda depolamak istiyorsanız bu seçeneği belirleyin. Seçili koleksiyonu bir dağıtım noktası grubuyla ilişkilendirmediyseniz bu seçenek kullanılamaz.  

6.  **İçerik** sayfasında **Ekle** öğesini tıklatın ve ardından bu paket ve programla ilişkili içeriği dağıtmak istediğiniz dağıtım noktalarını veya dağıtım noktası gruplarını seçin.  

7.  **Dağıtım Ayarları** sayfasında dağıtım türü için **Kullanılabilir** öğesini seçin ve ardından **İleri**'yi tıklatın.  

8.  **Zamanlama**sayfasında bu paketin ve programın ne zaman dağıtılacağını veya ne zaman istemci aygıtlara kullanılabilir olacağını yapılandırın.  

     Bu sayfadaki seçenekler dağıtım eyleminin **Kullanılabilir** veya **Gerekli**olarak ayarlanmasına göre farklılık gösterir.  

9. **Zamanlama**sayfasında aşağıdaki ayarları yapılandırın ve ardından **İleri**'yi tıklatın.  

    1.  **Bu dağıtımın kullanılabilir olacağı zamanı ayarla**: Paket ve programın hedef bilgisayarda çalıştırılmak için uygun olduğu tarihi ve saati belirtin. **UTC**öğesini seçtiğinizde bu ayar paket ve programın hedef bilgisayarlardaki yerel saate bağlı olarak birden fazla hedef bilgisayarda farklı saatler yerine aynı saatte uygun olmasını sağlar.  

    2.  **Bu dağıtımın süre sonunu zamanla**: Paket ve programın hedef bilgisayarda sona ereceği tarihi ve saati belirtin. **UTC**öğesini seçtiğinizde bu ayar görev sırasının hedef bilgisayarlardaki yerel saate bağlı olarak birden fazla hedef bilgisayarda farklı saatler yerine aynı saatte sona ermesini sağlar.  

10. Sihirbazın **Kullanıcı Deneyimi** sayfasında aşağıdaki bilgileri belirtin:  

    -   **Yazılım yükleme**: Yazılımın yapılandırılmış herhangi bir bakım penceresinin dışında yüklenmesine olanak sağlar.  

    -   **Sistem yeniden başlatma (yüklemeyi tamamlamak için gerekliyse)**: Yazılım yüklemesi tarafından gerektirildiğinde cihazın yapılandırılmış bakım pencerelerinin dışında yeniden başlatılmasına izin verir.  

    -   **Katıştırılmış Cihazlar**: Yazma filtresi etkin Windows Embedded cihazlarına paket ve programlar dağıtırken, paket ve programları geçici katmana yüklemeyi ve değişiklikleri daha sonra gerçekleştirmeyi veya değişiklikleri yükleme son tarihinde ya da bir bakım penceresi sırasında gerçekleştirmeyi belirtebilirsiniz. Yükleme son tarihinde veya bakım penceresi sırasında değişiklik yaparsanız, yeniden başlatma gerekir ve değişiklikler aygıtta kalır.  

11. **Dağıtım Noktaları** sayfasında aşağıdaki bilgileri belirtin:  

    -   **Dağıtım seçenekleri:****İçeriği dağıtım noktasından yükle ve yerel olarak çalıştır**'ı belirtin.  

    -   **İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına izin ver**: İstemcilerin, içeriği zaten indirmiş ve önbelleğe almış ağdaki diğer istemcilerden içerik indirmesine izin vererek ağ yükünü azaltmak için bu seçeneği kullanın. Bu seçenek Windows BranchCache kullanır ve Windows Vista SP2 sonraki sürümleri çalıştıran bilgisayarlarda kullanılabilir.  

    -   **İçerik için bir geri dönüş kaynak konumu kullanabilecek olan tüm istemciler**: İstemcilerin geri dönmesine ve içerik tercih edilen bir dağıtım noktasında mevcut olmadığında tercih edilmeyen bir dağıtım noktasını içeriğin kaynak konumu olarak kullanmasına izin verip vermeyeceğinizi belirtin.  

12. Sihirbazı tamamlayın.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Windows 8 görev sırasını dağıtmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ne tıklayın.  

3.  [Prerequisites to provision Windows To Go](#BKMK_Prereqs) adımında oluşturduğunuz Windows 8 görev sırasını seçin.  

4.  **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıt**'a tıklayın.  

5.  **Genel** sayfasında, aşağıdaki ayarları belirtin:  

    1.  **Görev dizisi**: Windows 8 görev dizisinin seçildiğini doğrulayın.  

    2.  **Koleksiyon**: Bir kullanıcının Windows To Go sağlayabileceği tüm cihazları içeren koleksiyonu seçmek için **Gözat** öğesine tıklayın.  

        > [!IMPORTANT]  
        >  [Create prestaged media](#BKMK_CreatePrestagedMedia) bölümünde oluşturduğunuz önceden hazırlanmış medya SMSTSPreferredAdvertID değişkenini kullanıyorsa görev sırasını **Tüm Sistemler** koleksiyonuna dağıtabilir ve **İçerik** sayfasındaki **Yalnızca Windows PE (gizli)** ayarını belirtebilirsiniz. Görev sırası gizli olduğu için yalnızca medyada kullanılabilir.  

    3.  **Bu koleksiyonla ilişkili varsayılan dağıtım noktası gruplarını kullan**: Paket içeriğini koleksiyonun varsayılan dağıtım noktası grubunda depolamak istiyorsanız bu seçeneği belirleyin. Seçili koleksiyonu bir dağıtım noktası grubuyla ilişkilendirmediyseniz bu seçenek kullanılamaz.  

6.  **Dağıtım Ayarları** sayfasında aşağıdaki ayarları yapılandırın ve **İleri**'yi tıklatın.  

    -   **Amaç**: **Kullanılabilir**öğesini seçin. Görev sırasını bir kullanıcıya dağıttığınızda kullanıcı Uygulama Kataloğunda yayınlanan görev sırasını görür ve onu isteğe bağlı olarak talep edebilir. Görev sırasını bir aygıta dağıtırsanız kullanıcı onu Yazılım Merkezinde görür ve isteğe bağlı olarak yükleyebilir.  

    -   **Aşağıdakiler için kullanılabilir yap**: görev dizisinin istemciler, medya veya PXE Configuration Manager için kullanılabilir olup olmadığını belirtin.  

        > [!IMPORTANT]  
        >  Otomatik görev sırası dağıtımları için **Yalnızca medya ve PXE (gizli)** ayarını kullanın. Bilgisayarın bir Windows To Go sürücüsü algıladığında kullanıcı etkileşimi olmadan Windows To Go dağıtımını otomatik olarak önyüklemesi için **Katılımsız işletim sistemi dağıtımına izin ver** öğesini seçin ve SMSTSPreferredAdvertID değişkenini önceden hazırlanmış medyanın bir parçası olarak ayarlayın. Önceden hazırlanmış bu medya ayarları hakkında daha fazla bilgi için [Create prestaged media](#BKMK_CreatePrestagedMedia) bölümüne bakın.  

7.  **Zamanlama** sayfasında aşağıdaki ayarları yapılandırın ve ardından **İleri**'yi tıklatın.  

    1.  **Bu dağıtımın kullanılabilir olacağı zamanı ayarla**: Görev dizisinin hedef bilgisayarda çalıştırılmak için uygun olduğu tarihi ve saati belirtin. **UTC**öğesini seçtiğinizde bu ayar görev sırasının hedef bilgisayarlardaki yerel saate bağlı olarak birden fazla hedef bilgisayarda farklı saatler yerine aynı saatte uygun olmasını sağlar.  

    2.  **Bu dağıtımın süre sonunu zamanla**: Görev dizisinin hedef bilgisayarda sona ereceği tarihi ve saati belirtin. **UTC**öğesini seçtiğinizde bu ayar görev sırasının hedef bilgisayarlardaki yerel saate bağlı olarak birden fazla hedef bilgisayarda farklı saatler yerine aynı saatte sona ermesini sağlar.  

8.  **Kullanıcı Deneyimi** sayfasında aşağıdaki bilgileri belirtin:  

    -   **Görev sırası Ilerlemesini göster**: Configuration Manager istemcisinin görev dizisinin ilerlemesini görüntüleyip görüntülemediğini belirtin.  

    -   **Yazılım yükleme**: Kullanıcının zamanlanmış saat sonrasında yapılandırılmış bakım penceresi dışında yazılım yüklemesine izin verilip verilmeyeceğini belirtin.  

    -   **Sistem yeniden başlatma (yüklemeyi tamamlamak için gerekliyse)**: Yazılım yüklemesi tarafından gerektirildiğinde cihazın yapılandırılmış bakım pencerelerinin dışında yeniden başlatılmasına izin verir.  

    -   **Katıştırılmış Cihazlar**: Yazma filtresi etkin Windows Embedded cihazlarına paket ve programlar dağıtırken, paket ve programları geçici katmana yüklemeyi ve değişiklikleri daha sonra gerçekleştirmeyi veya değişiklikleri yükleme son tarihinde ya da bir bakım penceresi sırasında gerçekleştirmeyi belirtebilirsiniz. Yükleme son tarihinde veya bakım penceresi sırasında değişiklik yaparsanız, yeniden başlatma gerekir ve değişiklikler aygıtta kalır.  

    -   **İnternet tabanlı istemciler**: Görev dizisinin İnternet tabanlı bir istemcide çalışmasına izin verilip verilmediğini belirtin. İşletim sistem gibi yazılım yükleyen işlemler bu ayarda desteklenmez. Bu seçeneği yalnızca standart işletim sistemlerinde işlem yapan genel komut dosyası tabanlı görev sıraları için kullanın.  

9. **Uyarılar** sayfasında, bu görev sırası için istediğiniz uyarı ayarlarını belirtin ve ardından **İleri**'yi tıklatın.  

10. **Dağıtım noktası** sayfasında aşağıdaki bilgileri belirtin ve **İleri**'yi tıklatın.  

    -   **Dağıtım seçenekleri**: **Görev dizisini çalıştırarak içeriği gerektiğinde yerel olarak yükle**öğesini seçin.  

    -   **Kullanılabilir hiçbir yerel dağıtım noktası olmadığında uzak bir dağıtım noktası kullan**: İstemcilerin, görev dizisinin gerektirdiği içeriği yüklemek üzere yavaş ve güvenilmeyen ağlardaki dağıtım noktalarını kullanıp kullanamayacağını belirtin.  

    -   **İstemcilerin içerik için bir geri dönüş kaynak konumu kullanmasına Izin ver**:
        - *Sürüm 1610 ' den önce*, bu sınır gruplarının dışındaki istemcilerin geri dönmesine ve başka bir dağıtım noktası mevcut olmadığında dağıtım noktasını bir kaynak konumu olarak kullanmasına izin vermek için içerik için geri dönüş kaynak konumuna izin ver onay kutusunu seçebilirsiniz.
        - *Sürüm 1610 ' den başlayarak*artık **içerik için geri dönüş kaynak konumuna izin ver**' i yapılandırabilirsiniz.  Bunun yerine, bir istemcinin geçerli bir içerik kaynak konumu için ek sınır gruplarını aramaya ne zaman başlayabilirim belirten sınır grupları arasındaki ilişkileri yapılandırırsınız. 

11. Sihirbazı tamamlayın.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a>Kullanıcı Windows to go oluşturucuyu çalıştırır  
 Windows To Go paketini ve Windows 8 görev sırasını dağıttıktan sonra Windows To Go Oluşturucu kullanılabilir hale gelir. Kullanıcı yazılım kataloğuna veya Windows To Go Oluşturucu aygıtlara dağıtıldıysa Yazılım Merkezine giderek Windows To Go Oluşturucu programını çalıştırabilir. Oluşturucu paketi indirildikten sonra görev çubuğunda yanıp sönen bir simge gösterilir. Kullanıcı bu simgeyi tıklattığında kullanıcının sağlanacak Windows To Go sürücüsünü seçmesi (/drive komut satırı seçeneği kullanılmıyorsa) için bir iletişim kutusu gösterilir. Sürücü Windows To Go gereksinimlerini karşılamıyorsa veya sürücüde görüntünün yüklenmesi için yeterli boş disk alanı yoksa oluşturucu programı bir hata iletisi gösterir. Kullanıcı, onay sayfasından uygulanacak bir sürücü ve görüntü doğrulaması yapabilir. Oluşturucu Windows To Go sürücüsüne içerik yapılandırıp önceden hazırladığından bir ilerleme iletişim kutusu gösterir. Önceden hazırlama tamamlandıktan sonra oluşturucu, Windows To Go sürücüsünü önyükleyecek şekilde bilgisayarı yeniden başlatmaya yönelik bir uyarı gösterir.  

> [!NOTE]  
>  [Create a Windows To Go Creator package](#BKMK_CreatePackage) bölümünde oluşturucu programı için komut satırının bir parçası olarak önyükleme yönlendirmesini etkinleştirmediyseniz, kullanıcının her sistem yeniden başlatmasında Windows To Go sürücüsünü elle önyüklemesi gerekebilir.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Configuration Manager'ın Windows To Go sürücüsünü yapılandırıp hazırlaması  
 Bilgisayar Windows To Go sürücüsüne yeniden başlatıldıktan sonra, sürücü Windows PE'de önyüklenir ve yönetim noktasına bağlanarak işletim sistemi dağıtımını tamamlama ilkesini alır. Configuration Manager sürücüyü yapılandırır ve aşamalar. Sürücüyü Configuration Manager sonra, Kullanıcı sağlama işlemini tamamlamak için bilgisayarı yeniden başlatabilir (bir etki alanına katılması veya uygulamaları yüklemek gibi). Bu işlem tüm önceden hazırlanmış medyalar için aynıdır.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a> Kullanıcının Windows 8'de oturum açması  
 Configuration Manager sağlama işlemini tamamladıktan sonra Windows 8 kilit ekranı görüntülendikten sonra, Kullanıcı işletim sisteminde oturum açabilir.  
