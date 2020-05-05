---
title: Uygulamaları onaylama
titleSuffix: Configuration Manager
description: Configuration Manager ' de uygulama onayına yönelik ayarlar ve davranışlar hakkında bilgi edinin.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fac75f0f13141c86b29d0213b3c7b06b9f603062
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643236"
---
# <a name="approve-applications-in-configuration-manager"></a>Configuration Manager uygulamaları onaylama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' de [bir uygulama](deploy-applications.md) dağıttığınızda, yüklemeden önce onay isteyebilirsiniz. Kullanıcılar uygulamayı Yazılım Merkezi 'nde ister ve sonra Configuration Manager konsolundaki isteği gözden geçirin. İsteği onaylayabilir veya reddedebilirsiniz.

## <a name="approval-settings"></a><a name="bkmk_approval"></a>Onay ayarları

Uygulama onay davranışı, önerilen [isteğe bağlı uygulama onay deneyimini](#bkmk_opt)etkinleştirip etkinleştirmediğinize bağlıdır. Aşağıdaki onay ayarlarından biri, uygulama dağıtımının **dağıtım ayarları** sayfasında görünür:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a>Bir yöneticinin cihazda bu uygulama için bir isteği onaylaması gerekir

> [!Note]  
> Configuration Manager Bu özelliği varsayılan olarak etkinleştirmez. Kullanmadan önce, **cihaz başına kullanıcılara yönelik uygulama Isteklerini Onayla**özelliğini etkinleştirin. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
>
> Bu özelliği etkinleştirmezseniz, [önceki deneyimi](#bkmk_prior)görürsünüz.  

Yönetici, kullanıcının istenen cihaza yüklenebilmesi için önce uygulamaya yönelik kullanıcı isteklerini onaylar. Yönetici isteği onayladığında, Kullanıcı yalnızca bu cihaza uygulamayı kurabilir. Kullanıcı başka bir cihaza uygulamayı yüklemek için başka bir istek göndermesi gerekir. Bu seçenek, dağıtım amacı **gerekli**olduğunda ya da uygulamayı bir cihaz koleksiyonuna dağıttığınızda gri olur. <!--1357015-->  

> [!Note]  
> Yeni Configuration Manager özelliklerinden yararlanmak için önce istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.<!--SCCMDocs issue 646-->  

Configuration Manager konsolunun **yazılım kitaplığı** çalışma alanında **uygulama yönetimi** altındaki **uygulama isteklerini** görüntüleyin. (Sürüm 1902 ve önceki sürümlerde bu düğüm **onay istekleri**olarak adlandırılır.) Artık her istek için listede bir **cihaz** sütunu var. İstek üzerinde eylem gerçekleştirdiğinizde, uygulama Isteği iletişim kutusu ayrıca kullanıcının isteği gönderdiği cihaz adını da içerir.

Bir istek 30 gün içinde onaylanmazsa, kaldırılır. İstemciyi yeniden yüklemek bekleyen onay isteklerini iptal edebilir.  

Bir cihaz koleksiyonuna bir dağıtımda onay almanız gerektiğinde, uygulama yazılım merkezi 'nde gösterilmez. Bir kullanıcı koleksiyonuna dağıtım üzerinde onay almanız gerekiyorsa, uygulama yazılım merkezi 'nde görüntülenir. İstemci ayarı olan kullanıcılar tarafından hala gizlenebilir, **Yazılım Merkezi 'nde onaylanmamış uygulamaları gizleyin**. Daha fazla bilgi için bkz. [Software Center istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-center).

Bir uygulamayı yükleme için onayladıktan sonra, Configuration Manager konsolundaki isteği **reddedebilirsiniz** . Kullanıcılar uygulamayı henüz yüklemediyse, bu eylem, yazılım merkezi 'nden uygulamanın yeni kopyalarını yüklemekten bu işlemi sonlandırır. Bir uygulama daha önce onaylanmış ve yüklenmişse, uygulama isteğini **reddetmeniz** durumunda istemci uygulamayı kullanıcının cihazından kaldırır.<!--1357891-->

Sürüm 1906 ' den başlayarak, konsolundaki bir uygulama isteğini onaylar ve sonra reddetmeniz durumunda yeniden onaylayabilirsiniz. Uygulamayı onayladıktan sonra, uygulama istemciye yeniden yüklenir.  <!-- 4224910 -->

Onay işlemini [onaylama-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) PowerShell cmdlet 'i ile otomatikleştirin. Sürüm 1902 ' den başlayarak, bu cmdlet **ınstallactionbehavior** parametresini içerir. Uygulamanın hemen mi yoksa iş dışı saatlerde mı yükleneceğini belirtmek için bu parametreyi kullanın.<!-- SCCMDocs-pr issue #3418 -->

1906 ' den başlayarak hangi dağıtımların onay gerektirdiğini görebilirsiniz. **Uygulamalar** düğümünde bir uygulama seçin. Ayrıntılar bölmesinde **dağıtımlar** sekmesine geçin. Varsayılan olarak yeni bir sütun görüntülenir, **onay gerektirir**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a>Önceden onaylanan uygulamalar yüklemesini yeniden deneyin

<!--4336307-->
Sürüm 1906 ' den başlayarak, daha önce bir kullanıcı veya cihaz için onaylanmış bir uygulamanın yüklemesini yeniden deneyebilirsiniz. Onay seçeneği yalnızca kullanılabilir dağıtımlar içindir. Kullanıcı uygulamayı kaldırırsa veya ilk yükleme işlemi başarısız olursa, Configuration Manager durumunu yeniden değerlendirmez ve yeniden yüklemez. Bu özellik destek teknisyeninin, yardım için çağıran bir kullanıcı için uygulama yüklemeyi hızlı bir şekilde yeniden denemesini sağlar.

1. Uygulama nesnesi üzerinde **onaylama** iznine sahip bir kullanıcı olarak Configuration Manager konsolunu açın. Örneğin, **Uygulama Yöneticisi** veya **uygulama yazarı** yerleşik rollerinin bu izni vardır.

1. Onay gerektiren bir uygulama dağıtın ve onaylayın.

    > [!Tip]  
    > Alternatif olarak, [bir cihaz için bir uygulama da yükler](install-app-for-device.md). Cihazda uygulama için onaylanan bir istek oluşturur.  

Uygulama başarıyla yüklenemezse veya Kullanıcı uygulamayı kaldırırsa, yeniden denemek için aşağıdaki işlemi kullanın:

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **Uygulama istekleri** düğümünü seçin. (Sürüm 1902 ve önceki sürümlerde bu düğüm **onay istekleri**olarak adlandırılır.)

1. Daha önce onaylanan uygulamayı seçin. Şeridin onay Isteği grubunda, **yüklemeyi yeniden dene**' yi seçin.

#### <a name="other-app-approval-resources"></a>Diğer uygulama onay kaynakları

- [ConfigMgr 1810 uygulama onayı geliştirmeleri](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Configuration Manager 'de uygulama onay işlemine yönelik güncelleştirmeler](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a>Kullanıcıların bu uygulamayı istemesi durumunda yönetici onayı iste

> [!Note]  
> Bu deneyim, önerilen [isteğe bağlı uygulama onay deneyimini](#bkmk_opt)etkinleştirmezseniz geçerlidir.

Yönetici, Kullanıcı tarafından yüklenmeden önce uygulamanın kullanıcı isteklerini onaylar. Bu seçenek, dağıtım amacı **gerekli**olduğunda ya da uygulamayı bir cihaz koleksiyonuna dağıttığınızda gri olur.  

Uygulama onay istekleri, **yazılım kitaplığı** çalışma alanındaki **uygulama yönetimi** altında bulunan uygulama **istekleri** düğümünde görüntülenir. (Sürüm 1902 ve önceki sürümlerde bu düğüm **onay istekleri**olarak adlandırılır.) Bir istek 30 gün içinde onaylanmazsa, kaldırılır. İstemciyi yeniden yüklemek bekleyen onay isteklerini iptal edebilir.  

Bir uygulamayı yükleme için onayladıktan sonra, Configuration Manager konsolundaki isteği **reddedebilirsiniz** . Bu eylem, istemcinin uygulamayı herhangi bir cihazdan kaldırmasına neden olmaz. Kullanıcıların yazılım merkezi 'nden uygulamanın yeni kopyalarını yüklemesini engeller.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a>E-posta bildirimleri

<!--1321550-->

Uygulama onay istekleri için e-posta bildirimleri yapılandırabilirsiniz. Bir Kullanıcı bir uygulama istediğinde, bir e-posta alırsınız. Configuration Manager konsolu gerekmeden isteği onaylamak veya reddetmek için e-postadaki bağlantılar ' a tıklayın.

Uygulama için yeni bir dağıtım oluştururken isteği onaylayabilecek veya reddedebilen kullanıcıların e-posta adreslerini tanımlayabilirsiniz. Daha sonra e-posta adresleri listesini değiştirmeniz gerekiyorsa, **izleme** çalışma alanına gidin, **Uyarılar**' ı genişletin ve **abonelikler** düğümünü seçin. Uygulama dağıtımınızla ilgili **e-posta abonelikleri aracılığıyla onaylama uygulamasının** birinden **Özellikler** ' i seçin.

Birden fazla uyarı varsa, hangi uyarının hangi dağıtıma gideceğini belirleyebilirsiniz. Uyarı özelliklerini açın ve **Seçili uyarıların** listesini Genel sekmesinde görüntüleyin. Dağıtım bu abonelik için uyarı olarak etkinleştirilir.

Kullanıcılar, yazılım merkezi 'nden isteğe bir yorum ekleyebilir. Bu açıklama Configuration Manager konsolundaki uygulama isteğini gösterir. Sürüm 1902 ' den başlayarak, bu açıklama e-postada de görüntülenir. Bu yorumu e-postaya eklemek, onaylayanlara isteği onaylama veya reddetme konusunda daha iyi bir karar vermesini sağlar.<!--3594063-->

### <a name="prerequisites"></a>Önkoşullar

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>E-posta bildirimleri göndermek ve iç ağ üzerinde işlem gerçekleştirmek için

Bu önkoşullara sahip alıcılar, istek bildirimi içeren bir e-posta alır. Bunlar iç ağ üzerinde yer alıyorsa, e-postadaki isteği de onaylayabilir veya reddedebilir.

- [İsteğe bağlı özelliği](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **cihaz başına Kullanıcı için uygulama isteklerini Onayla**' yı etkinleştirin.  

- [Uyarılar için e-posta bildirimini](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)yapılandırın.  

- Birincil sitede bir sertifika kullanmak için SMS sağlayıcısı 'nı etkinleştirin.<!--SCCMDocs-pr issue 3135--> Aşağıdaki seçeneklerden birini kullanın:  

  - Önerilen Birincil site için [GELIŞMIŞ http](../../core/plan-design/hierarchy/enhanced-http.md) 'yi etkinleştirin.

    > [!Note]  
    > Birincil site, SMS sağlayıcısı için bir sertifika oluşturduğunda, istemci üzerindeki Web tarayıcısı tarafından güvenilir olmayacaktır. Güvenlik ayarlarınıza bağlı olarak, bir uygulama isteğine yanıt vermediğinde bir güvenlik uyarısı görürsünüz.  

  - PKI tabanlı bir sertifikayı, birincil sitedeki SMS sağlayıcısı rolünü barındıran sunucuda IIS 'de 443 numaralı bağlantı noktasına el ile bağlayın.

> [!NOTE]
> Bir hiyerarşide birden fazla alt birincil siteniz varsa, bu özelliği etkinleştirmek istediğiniz her birincil site için bu önkoşulları yapılandırın. E-posta bildiriminin bağlantıları, birincil sitede yönetim hizmeti içindir.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Internet 'ten işlem yapmak için

Bu ek isteğe bağlı önkoşullara sahip olan alıcılar, internet erişimi olan her yerden gelen istekleri onaylayabilir veya reddedebilir.

- Bulut yönetimi ağ geçidi aracılığıyla SMS Sağlayıcısı yönetim hizmetini etkinleştirin. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin. SMS sağlayıcı rolüyle sunucuyu seçin. Ayrıntılar bölmesinde, **SMS sağlayıcı** rolünü seçin ve site rolü sekmesindeki şeritte **Özellikler** ' i seçin. **Yönetim hizmeti için bulut yönetimi ağ geçidi trafiğine izin Configuration Manager verme**seçeneğini belirleyin.  

  - SMS sağlayıcısı, **.NET 4.5.2** veya üstünü gerektirir.  

- [Bulut yönetimi ağ geçidi](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

- Siteyi **bulut yönetimi** için [Azure hizmetlerine](../../core/servers/deploy/configure/azure-services-wizard.md) ekleme  

  - [Azure AD Kullanıcı bulmayı](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc) etkinleştir  

  - Azure AD 'de ayarları el ile yapılandır:  

        1. *Genel yönetici* izinlerine sahip bir kullanıcı olarak [Azure Portal](https://portal.azure.com) gidin. **Azure Active Directory**gidin ve **uygulama kayıtları**' i seçin.  

        2. Configuration Manager **bulut yönetimi** tümleştirmesi için oluşturduğunuz uygulamayı seçin.  

        3. **Yönet** menüsünde **kimlik doğrulaması**' nı seçin.  

            1. **Yeniden yönlendirme URI 'leri** bölümünde aşağıdaki yolu yapıştırın:`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Bulut `<CMG FQDN>` yönetimi ağ geçidi (CMG) hizmetinizin tam etki alanı adı (FQDN) ile değiştirin. Örneğin, GraniteFalls.Contoso.com.  

            3. Sonra **Kaydet**' i seçin.  

        4. **Yönet** menüsünde, **bildirim**' ı seçin.  

            1. Bildirim Düzenleme bölmesinde **oauth2AllowImplicitFlow** özelliğini bulun.  

            2. Değerini **true**olarak değiştirin. Örneğin, tüm satır aşağıdaki satıra benzer görünmelidir:`"oauth2AllowImplicitFlow": true,`  

            3. **Kaydet**’i seçin.  

### <a name="configure-email-approval"></a>E-posta onayını yapılandırma

1. Configuration Manager konsolunda, bir uygulamayı bir kullanıcı koleksiyonuna kullanılabilir olarak [dağıtın](deploy-applications.md) . **Dağıtım ayarları** sayfasında, onay için etkinleştirin. Ardından, bildirim almak için bir veya daha fazla e-posta adresi girin. E-posta adreslerini noktalı virgül (`;`) ile ayırın.  

     > [!Note]  
     > Azure AD kuruluşunuzda e-postayı alan herkes isteği onaylayabilir. İşlem yapmak istemediğiniz müddetçe e-postayı başkalarına iletmeyin.  

2. Bir kullanıcı olarak, uygulamayı Yazılım Merkezi 'nde isteyin.  

3. Beş dakika içinde bir e-posta bildirimi alırsınız. E-postanın içeriği aşağıdaki örneğe benzer:  

![Uygulama onayı için örnek e-posta bildirimi](media/1321550-email.png)

> [!Note]  
> Onaylama veya reddetme bağlantısı, tek seferlik kullanım içindir. Örneğin, bildirimleri almak için bir grup diğer adı yapılandırırsınız. Meg, isteği onaylar. Şimdi deneme yanılması isteği reddedemez.  

Sorun giderme için site sunucusundaki **NotiCtrl. log** dosyasını gözden geçirin.

## <a name="maintenance"></a>Bakım

Configuration Manager, uygulama onayı isteğiyle ilgili bilgileri site veritabanında depolar. İptal edilen veya reddedilen istekler için, site 30 gün sonra istek geçmişini siler. Bu silme davranışını, **eski uygulama Isteği verilerini sil** [site bakım görevi](../../core/servers/manage/maintenance-tasks.md)ile yapılandırabilirsiniz. Site hiçbir onaylanan veya bekleyen uygulama isteğini hiçbir şekilde silmez.
