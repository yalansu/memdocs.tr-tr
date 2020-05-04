---
title: Uygulama oluşturma ve dağıtma
titleSuffix: Configuration Manager
description: İş kolu uygulaması içeren bir uygulama oluşturup dağıtın ve uygulamaları etkili bir şekilde yönetmeyi öğrenin.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710513"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Configuration Manager ile uygulama oluşturma ve dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu başlığında, hemen Configuration Manager ve bir uygulama oluşturacaksınız. Bu örnekte, şirketinizde Windows 10 çalıştıran tüm bilgisayarlara yüklenmesi gereken **contoso. msi**adlı Windows bilgisayarları için iş kolu uygulaması içeren bir uygulama oluşturacaksınız ve dağıtırsınız. Bu şekilde, uygulamaları etkili bir şekilde yönetmek için yapabileceğiniz pek çok şey hakkında bilgi edineceksiniz.  

 Bu yordam, Configuration Manager uygulamalarının nasıl oluşturulacağı ve dağıtılacağı hakkında genel bir bakış sunacak şekilde tasarlanmıştır. Ancak, tüm yapılandırma seçeneklerini kapsamaz veya diğer platformlar için uygulama oluşturma ve dağıtma.  

 Her platformla ilgili özel ayrıntılar için aşağıdaki konulardan birine bakın:  

- [Windows uygulamaları oluşturma](creating-windows-applications.md)
- [Windows Phone uygulamaları oluşturma](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Mac bilgisayar uygulamaları oluşturma](creating-mac-computer-applications.md)
- [Linux ve UNIX sunucu uygulamaları oluşturma](creating-linux-and-unix-server-applications.md)
- [Windows Embedded uygulamaları oluşturma](creating-windows-embedded-applications.md)


Configuration Manager uygulamalarla zaten bilgi sahibiyseniz, bu konuyu atlayabilirsiniz. Ancak, uygulama oluştururken ve dağıtırken kullanabileceğiniz tüm seçenekler hakkında bilgi edinmek için [uygulama oluştur](../../apps/deploy-use/create-applications.md) ' u gözden geçirmek isteyebilirsiniz.  

## <a name="before-you-start"></a>Başlamadan önce  

Uygulamanızı yüklemek için sitenizi hazırladıktan ve bu konuda kullanılan terminolojiyi anladığınızdan, [uygulama yönetimine giriş](../understand/introduction-to-application-management.md) bölümündeki bilgileri gözden geçirdiğinizden emin olun.  

 Ayrıca, **contoso. msi** uygulamasına ait yükleme dosyalarının ağınızda erişilebilir bir konumda olduğundan emin olun.  

## <a name="create-the-configuration-manager-application"></a>Configuration Manager uygulaması oluşturma  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Uygulama oluşturma Sihirbazı 'Nı başlatmak ve uygulamayı oluşturmak için  

1. Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **uygulamaları**' nı seçin.  

2. **Giriş** sekmesinde, **Oluştur** grubunda, **uygulama oluştur**' u seçin.  

3. **Uygulama oluşturma Sihirbazı**' nın **genel** sayfasında **Bu uygulamayla ilgili bilgileri otomatik olarak yükleme dosyalarından algıla**' yı seçin. Bu, sihirbazdaki bazı bilgilerin, yükleme. msi dosyasından ayıklanan bilgilerle önceden doldurulur. Ardından aşağıdaki bilgileri belirtin:  

   - **Tür**: **Windows Installer (\*. msi dosyası)** öğesini seçin.  

   - **Konum**: **contoso. msi**yükleme dosyasının konumunu yazın (veya konum **seçmek için seçin** ). Yükleme dosyalarını bulmak için, konumun * \\\server\share\Configuration Manager File* biçiminde belirtilmesi gerektiğini unutmayın.  

   Aşağıdaki ekran görüntüsüne benzeyen bir şey ile karşılaşırsınız:  

   ![Uygulama Yönetimi Sihirbazı Genel sayfası](media/App-management-wizard-general-page.png)  

4. **İleri**’yi seçin. **Bilgileri Içeri aktar** sayfasında, uygulama ve Configuration Manager içeri aktarılan ilişkili dosyalarla ilgili bazı bilgiler görürsünüz. İşiniz bittiğinde **İleri** ' yi seçin.  

5. **Genel bilgiler** sayfasında, uygulamayı Configuration Manager konsolunda sıralamanıza ve bulmanıza yardımcı olmak için uygulama hakkında daha fazla bilgi sağlayabilirsiniz.  

    Ayrıca, **yükleme programı** alanı, uygulamayı bilgisayarlara yüklemek için kullanılacak tam komut satırını belirtmenize olanak tanır. Kendi özelliklerinizi eklemek için bunu düzenleyebilirsiniz (örneğin, katılımsız bir yükleme için **/q** ).  

   > [!TIP]  
   > Sihirbazın bu sayfasındaki bazı alanlar, uygulama yükleme dosyalarını içeri aktardığınızda otomatik olarak doldurulmuş olabilir.  

    Aşağıdaki ekran görüntüsüne benzer bir ekran ile karşılaşırsınız:  

    ![Uygulama Yönetimi Sihirbazı genel bilgi sayfası](media/App-management-wizard-general-information-page.png)  

6. **İleri**’yi seçin. Özet sayfasında, uygulama ayarlarınızı onaylayıp Sihirbazı tamamlayabilirsiniz.  

   Uygulama oluşturma işlemini tamamladınız. Bunu bulmak için, **yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve ardından **uygulamalar**' ı seçin. Bu örnek için şunları göreceksiniz:  

   ![Son uygulama grafiği](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Uygulama ve dağıtım türünün özelliklerini inceleyin  

Bir uygulama oluşturduğunuza göre, artık gerekirse uygulama ayarlarını geliştirebilirsiniz. Uygulama özelliklerine bakmak için, uygulamayı seçin ve sonra **Özellikler** grubunun **giriş** sekmesinde **Özellikler**' i seçin.  

 **<contoso\> uygulama özellikleri** iletişim kutusunda, uygulamanın davranışını iyileştirmek için yapılandırabileceğiniz birçok öğe görürsünüz. Yapılandırabileceğiniz tüm ayarlar hakkında daha fazla bilgi için bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md). Bu örnekte yalnızca uygulamanın dağıtım türüne ait bazı özellikleri değiştireceksiniz.  

 > **contoso uygulaması** dağıtım türü > **Düzenle** **dağıtım türleri** sekmesini seçin.

Bunun gibi bir iletişim kutusu görürsünüz:  

![Uygulama yönetimi uygulaması Özellikler sayfası](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Dağıtım türüne bir gereksinim ekleme

 Gereksinimler, uygulama bir cihaza yüklenmeden önce karşılanması gereken koşuları belirtir.  Yerleşik gereksinimler arasından seçim yapabilir veya kendinizinkini oluşturabilirsiniz. Bu örnekte, uygulamanın yalnızca Windows 10 çalıştıran bilgisayarlarda yüklü olacağını bir gereksinim eklersiniz.  

1. Yeni açtığınız dağıtım türü özellikleri sayfasında **gereksinimler** sekmesini seçin.  

2. **Gereksinim Oluştur** iletişim kutusunu açmak için **Ekle** ' yi seçin.  

3. **Gereksinim Oluştur** iletişim kutusunda şu bilgileri belirtin:  

    - **Kategori**: **cihaz**  

    - **Koşul**: **işletim sistemi**  

    - **Kural türü**: **değer**  

    - **İşleç**: **aşağıdakilerden biri**  

    - İşletim sistemi listesinde **Windows 10**’u seçin.  

    Şunun gibi görünen bir iletişim kutusu açılır:  

    ![Uygulama yönetimi gereksinimleri sayfası](media/App-management-requirements-page.png)  

4. Açtığınız her bir özellik sayfasını kapatmak için **Tamam ' ı** seçin. Ardından Configuration Manager konsolundaki **uygulamalar** listesine geri dönün.  

> [!TIP]  
> Gereksinimler, ihtiyacınız olan Configuration Manager koleksiyonlarının sayısını azaltmaya yardımcı olabilir. Yalnızca uygulamanın yalnızca Windows 10 çalıştıran bilgisayarlara yüklenebileceğini belirttiğinden, daha sonra bunu birçok farklı işletim sistemi çalıştıran bilgisayarları içeren bir koleksiyona dağıtabilirsiniz. Ancak uygulama yalnızca Windows 10 bilgisayarlara yüklenir.

## <a name="add-the-application-content-to-a-distribution-point"></a>Uygulama içeriğini dağıtım noktasına ekleme  

Ardından, uygulamayı bilgisayarlara dağıtmak için, uygulama içeriğinin bir dağıtım noktasına kopyalandığından emin olun. Bilgisayarlar uygulamayı yüklemek için dağıtım noktasına erişir.  

> [!TIP]  
> Configuration Manager 'de dağıtım noktaları ve içerik yönetimi hakkında daha fazla bilgi edinmek için bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

1. Configuration Manager konsolunda **yazılım kitaplığı**' nı seçin.  

2. **Yazılım kitaplığı** çalışma alanında **uygulamalar**' ı genişletin. Ardından, uygulamalar listesinde, oluşturduğunuz **contoso uygulamasını** seçin.  

3. **Giriş** sekmesinde, **dağıtım** grubunda, **içeriği dağıt**' ı seçin.  

4. **Içerik Dağıtma Sihirbazı**' nın **genel** sayfasında uygulama adının doğru olup olmadığını denetleyin ve ardından **İleri**' yi seçin.  

5. **İçerik** sayfasında dağıtım noktasına kopyalanacak bilgileri gözden geçirin ve ardından **İleri**' yi seçin.  

6. **Içerik hedefi** sayfasında, bir veya daha fazla dağıtım noktası ya da uygulama içeriğinin yükleneceği dağıtım noktası grupları seçmek için **Ekle** ' yi seçin.  

7. Sihirbazı tamamlayın.  

Uygulama içeriğinin dağıtım noktasına başarıyla kopyalanıp kopyalanmadığını, **dağıtım durumu** > **İçerik durumu**' nun altındaki **izleme** çalışma alanından denetleyebilirsiniz.  

## <a name="deploy-the-application"></a>Uygulamayı dağıtma  

Ardından, uygulamayı hiyerarşinizdeki bir cihaz koleksiyonuna dağıtın. Bu örnekte, uygulamayı **Tüm sistemler** cihaz koleksiyonuna dağıtırsınız.  

> [!TIP]  
> Daha önce seçtiğiniz gereksinimler nedeniyle yalnızca Windows 10 bilgisayarlarının uygulamayı yükleyeceğini unutmayın.

1. Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **uygulamaları**' nı seçin.  

2. Uygulamalar listesinden, daha önce oluşturduğunuz uygulamayı (**contoso uygulaması**) seçin ve ardından **dağıtım** grubundaki **giriş** sekmesinde **Dağıt**' ı seçin.  

3. **Yazılım Dağıtma Sihirbazı**'nın **genel** sayfasında, **Tüm sistemler** cihaz koleksiyonunu seçmek için, **Araştır** ' ı seçin.  

4. **İçerik** sayfasında, bilgisayarların uygulamayı yüklemesini istediğiniz dağıtım noktasının seçili olduğundan emin olun.  

5. **Dağıtım ayarları** sayfasında dağıtım eyleminin **yüklenmek**üzere ayarlandığından ve dağıtım amacının **gerekli**olarak ayarlandığından emin olun.  

    > [!TIP]  
    > Dağıtım amacını **gerekli**olarak ayarlayarak uygulamanın ayarladığınız gereksinimleri karşılayan bilgisayarlara yüklendiğinden emin olursunuz. Bu değeri **Kullanılabilir**olarak ayarlarsanız, kullanıcılar uygulamayı Yazılım Merkezi'nden isteğe bağlı olarak yükleyebilir.

6. **Zamanlama** sayfasında uygulamanın ne zaman yükleneceğini yapılandırabilirsiniz. Bu örnekte **Eldeki süreden sonraki en kısa süre içinde**öğesini seçin.  

7. **Kullanıcı deneyimi** sayfasında, varsayılan değerleri kabul etmek için **İleri** ' yi seçin.  

8. Sihirbazı tamamlayın.  

Uygulama dağıtımınızın durumunu görmek için aşağıdaki bilgileri kullanın **Uygulama bölümünü izleyin** .  

## <a name="monitor-the-application"></a>Uygulamayı izleme

 Bu bölümde, yeni dağıttığınız uygulamanın dağıtım durumuna hızlıca göz atalım.  

### <a name="to-review-the-deployment-status"></a>Dağıtım durumunu gözden geçirmek için  

1. Configuration Manager konsolunda, **izleme** > **dağıtımları**' nı seçin.  

2. Dağıtımları listesinden **Contoso Uygulaması**’nı seçin.  

3. **Giriş** sekmesinde, **dağıtım** grubunda, **durumu görüntüle**' yi seçin.  

4. Uygulama dağıtımı hakkında daha fazla durum güncelleştirmesi görmek için aşağıdaki sekmelerden birini seçin:  

    - **Başarılı**: uygulama belirtilen bilgisayarlara başarıyla yüklendi.  

    - **Devam ediyor**: uygulama henüz yüklemeyi tamamlamadı.  

    - **Hata**: uygulama belirtilen bilgisayarlara yüklenirken bir hata oluştu. Ayrıca hata hakkında daha fazla bilgi görüntülenir.  

    - **Gereksinimler Karşılanmadı**: belirtilen cihazlarda, yapılandırdığınız gereksinimleri karşılamadığından yükleme girişimi yapılmadı (Bu örnekte, Windows 10 ' da çalıştırılmadıklarından).  

    - **Bilinmiyor**: Configuration Manager dağıtımın durumunu bildiremedi. Daha sonra yeniden denetleyin.  

> [!TIP]  
> Uygulama dağıtımlarını izlemek için birkaç yol vardır. Tüm ayrıntılar için bkz. [uygulamaları izleme](../deploy-use/monitor-applications-from-the-console.md).

## <a name="end-user-experience"></a>Son kullanıcı deneyimi  

Configuration Manager tarafından yönetilen ve Windows 10 çalıştıran bilgisayarlara sahip kullanıcılar, contoso uygulamasını yüklemeleri gerektiğini söyleyen bir ileti görür. Yüklemeyi kabul ettikten sonra uygulama yüklenir.  

Configuration Manager sürüm 1906 ' den başlayarak, **yeni yazılım kullanılabilir** bildirim, bir kullanıcı için belirli bir uygulama ve düzeltme için bir kez görünür. Kullanıcı artık her oturum açtıklarında bildirimi görmez. Bunlar, uygulamanın değişmesi veya yeniden dağıtılması durumunda yalnızca bir uygulama için başka bir bildirim görür.

## <a name="next-steps"></a>Sonraki adımlar

[Uygulamaları izleme](../deploy-use/monitor-applications-from-the-console.md)
