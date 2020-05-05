---
title: Site sunucusu yüksek kullanılabilirliği
titleSuffix: Configuration Manager
description: Pasif mod site sunucusu ekleyerek Configuration Manager site sunucusu için yüksek kullanılabilirliği yapılandırma.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718311"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Configuration Manager 'de site sunucusu yüksek kullanılabilirliği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1128774-->

Geçmişte, ortamınızda bu rollerin birden çok örneğini bulundurarak Configuration Manager içindeki rollerin çoğuna artıklık ekleyebilirsiniz. Site sunucusunun kendisi hariç. Site sunucusu rolü için yüksek kullanılabilirlik, *Pasif* modda ek bir site sunucusu yüklemek için Configuration Manager tabanlı bir çözümdür. Merkezi Yönetim sitesi ve alt birincil siteleri pasif modda ek bir site sunucusuna sahip olabilir. Pasif moddaki site sunucusu, Azure 'da şirket içi veya bulut tabanlı olabilir.

Bu özellik aşağıdaki avantajları sunar

- Site sunucusu rolü için yedeklilik ve yüksek kullanılabilirlik  
- Site sunucusunun donanımını veya işletim sistemini daha kolay değiştirin  
- Site sunucunuzu daha kolay Azure IaaS 'ye taşıyın  

Pasif modda site sunucusu, *etkin* modda olan var olan site sunucunuza ek niteliğindedir. Pasif moddaki bir site sunucusu, gerektiğinde hemen kullanılmak üzere kullanılabilir. Configuration Manager hizmetini [yüksek oranda kullanılabilir](high-availability-options.md)hale getirmek için genel tasarımınızın bir parçası olarak bu ek site sunucusunu dahil edin.  

Pasif moddaki bir site sunucusu:

- , Etkin modda site sunucunuz ile aynı site veritabanını kullanır.
- Pasif moddayken site veritabanına veri yazmaz.
- , Etkin modda site sunucunuz ile aynı içerik kitaplığını kullanır.

Site sunucusunu pasif modda etkin hale getirmek için el ile *yükseltebilirsiniz* . Bu eylem, etkin moddaki site sunucusunu pasif modda site sunucusu olacak şekilde geçirir. Özgün etkin mod sunucusunda bulunan site sistem rolleri, bilgisayar erişilebilir olduğu sürece kullanılabilir kalır. Yalnızca site sunucusu rolü etkin ve pasif modlar arasında geçiş yapılır.

Microsoft Çekirdek Hizmetleri Mühendisliği ve Işlemleri, bu özelliği merkezi yönetim sitesini Microsoft Azure geçirmek için kullandı. Daha fazla bilgi için bkz. [MICROSOFT It gösterimi makalesi](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Önkoşullar

- Site içerik kitaplığı, uzak bir ağ paylaşımında olmalıdır. Her iki site sunucusu da, paylaşma ve içeriği için tam denetim izinlerine sahip olmalıdır. Daha fazla bilgi için bkz. [içerik kitaplığını yönetme](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).<!--1357525-->  

  - Site sunucusu bilgisayar hesabının, içerik kitaplığını taşıdığınız ağ yolu için **tam denetim** izinlerine sahip olması gerekir. Bu izin hem paylaşma hem de dosya sistemi için geçerlidir. Uzak sistemde yüklü bileşen yok.

  - Site sunucusunun dağıtım noktası rolü olamaz. Dağıtım noktası ayrıca içerik kitaplığını kullanır ve bu rol, uzak bir içerik kitaplığını desteklemez. İçerik kitaplığını taşıdıktan sonra, dağıtım noktası rolünü site sunucusuna ekleyemezsiniz.  

- Pasif moddaki site sunucusu, Azure 'da şirket içi veya bulut tabanlı olabilir.  

    > [!NOTE]
    > Pasif moddaki bulut tabanlı bir site sunucusu, Azure altyapı hizmetini (IaaS) kullanır. Daha fazla bilgi için aşağıdaki makalelere bakın:
    >
    >   - [Azure sanal makineleri (bulut tabanlı altyapı için)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Azure 'da Configuration Manager hakkında SSS](../../../understand/configuration-manager-on-azure.md)  

- Site sunucularının her ikisi de aynı Active Directory etki alanına katılmalıdır.  

- Configuration Manager, hiyerarşide pasif modda site sunucularını destekler. Merkezi Yönetim sitesi ve alt birincil siteleri pasif modda ek bir site sunucusuna sahip olabilir.<!-- 3607755 -->  

- Site sunucularının her ikisi de aynı site veritabanını kullanmalıdır.  

  - Veritabanı her site sunucusundan uzak olabilir. Sürüm 1810 ' den başlayarak, Configuration Manager Kurulum işlemi artık site sunucusu rolünün yük devretme kümelemesi için Windows rolü olan bir bilgisayara yüklenmesini engeller. SQL Always on bu rolü gerektirir, bu nedenle daha önce site sunucusundaki site veritabanını birlikte bulunduramıyorsunuz. Bu değişiklik ile, SQL Always on ve site sunucusu ' nu pasif modda kullanarak daha az sunucu ile yüksek oranda kullanılabilir bir site oluşturabilirsiniz.<!-- SCCMDocs issue 1074 -->  

  - Site veritabanını barındıran SQL Server, örnek, [SQL Server kümesi](use-a-sql-server-cluster-for-the-site-database.md)veya [SQL Server Always on kullanılabilirlik grubu](sql-server-alwayson-for-a-highly-available-site-database.md)olarak adlandırılan bir varsayılan örnek kullanabilir.  

  - Her iki site sunucusu da, site veritabanını barındıran SQL Server örneğinde **sysadmin** güvenlik rolüne gerek duyar. Özgün site sunucusunda bu roller zaten olmalıdır, bu nedenle bunları yeni site sunucusuna ekleyin. Örneğin, aşağıdaki SQL betiği contoso etki alanında yeni site sunucusu **VM2** için bu rolleri ekler:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Site sunucularının her ikisi de SQL Server örneğindeki site veritabanına erişime ihtiyacı vardır. Özgün site sunucusunda bu erişim zaten olmalıdır, bu nedenle yeni site sunucusuna ekleyin. Örneğin, aşağıdaki SQL betiği contoso etki alanındaki yeni site sunucusu **VM2** için **CM_ABC** veritabanına bir oturum açma ekler:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - Pasif moddaki site sunucusu, site sunucusu ile aynı site veritabanını etkin modda kullanacak şekilde yapılandırılmıştır. Pasif modda site sunucusu yalnızca veritabanından okur. Etkin moda yükseltilene kadar veritabanına yazmaz.  

- Pasif modda site sunucusu:  

  - Birincil bir siteyi yükleme önkoşulları ile Buluşmalıdır. Örneğin, .NET Framework, uzaktan değişiklikleri sıkıştırma ve Windows ADK. Listenin tamamı için bkz. [site ve site sistemi önkoşulları](../../../plan-design/configs/site-and-site-system-prerequisites.md).<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > SQL Server Native Client yüklediğinizden emin olun. Bunu yüklemezseniz Configuration Manager Kurulum sırasında önkoşul denetleyicisi eksik SQL Server izinlerle ilgili bir hata bildirir.<!-- SCCMDocs#2290 -->

  - , Site sunucusundaki yerel Yöneticiler grubunda bulunan bilgisayar hesabına etkin modda sahip olmalıdır.<!--516036-->

  - , Etkin modda site sunucusunun sürümüyle eşleşen kaynak dosyalar kullanılarak yüklenmelidir.  

  - Site sunucusunu Pasif mod rolüne yüklemeden önce, üzerinde yüklü herhangi bir sitenin site sistem rolüne sahip olamaz.  

- Her iki site sunucusu da [Configuration Manager tarafından desteklendiği](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)sürece farklı işletim sistemi veya hizmet paketi sürümleri çalıştırabilir.  

- Hizmet bağlantı noktası rolünü, yüksek kullanılabilirlik için yapılandırılmış site sunucusunda barındırmayın. Şu anda özgün site sunucusu ise, uygulamayı kaldırın ve başka bir site sistemi sunucusuna kurun. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](about-the-service-connection-point.md).  

- [Site sistemi yükleme hesabı](../../../plan-design/hierarchy/accounts.md#site-system-installation-account) için izinler  

  - Varsayılan olarak birçok müşteri, yeni site sistemlerini yüklemek için site sunucusunun bilgisayar hesabını kullanır. Gereksinim daha sonra site sunucusunun bilgisayar hesabını uzak site sistemindeki yerel **Yöneticiler** grubuna eklemektir. Ortamınız bu yapılandırmayı kullanıyorsa, yeni site sunucusunun bilgisayar hesabını tüm uzak site sistemlerinde bu yerel gruba eklediğinizden emin olun. Örneğin, tüm uzak dağıtım noktaları.  

  - Daha güvenli ve önerilen yapılandırma, site sistemini yüklemek için bir hizmet hesabı kullanmaktır. En güvenli yapılandırma, yerel bir hizmet hesabı kullanmaktır. Ortamınız bu yapılandırmayı kullanıyorsa, hiçbir değişiklik yapılması gerekmez.  

## <a name="limitations"></a>Sınırlamalar

- Her sitede yalnızca pasif moddaki tek bir site sunucusu desteklenir.  

- Pasif moddaki bir site sunucusu, ikincil bir sitede desteklenmez.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > İkincil siteler, yüksek oranda kullanılabilir site sunucularına sahip bir birincil site altında hala desteklenmektedir.

- Site sunucusunun pasif modda etkin moda yükseltilmesi el ile yapılır. Otomatik yük devretme yoktur.  

- Site sunucusunu pasif modda eklemeden önce site sistem rolleri yeni sunucuya yüklenemez.  

    > [!NOTE]
    > Site sunucusunu pasif modda yükledikten sonra, gerektiğinde ek roller ekleyebilirsiniz. Örneğin, birincil sitedeki bir yönetim noktası.

- Bir veritabanı kullanan raporlama noktası gibi roller için, veritabanını her iki site sunucusundan uzakta olan bir sunucuda barındırın.  

- Configuration Manager konsolu site sunucusuna pasif modda otomatik olarak yüklenmez.  

## <a name="add-a-site-server-in-passive-mode"></a>Pasif modda site sunucusu ekleme

Rol Ekleme genel işlemi hakkında daha fazla bilgi için bkz. [site sistemi rollerini yüklemeyi](install-site-system-roles.md).

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin, **siteler** düğümünü seçin ve şeritte **site sistem sunucusu oluştur** ' a tıklayın.

2. Site sistemi sunucusu oluşturma Sihirbazı ' nın **genel** sayfasında, site sunucusunu pasif modda barındıracak sunucuyu belirtin. Belirttiğiniz sunucu, site sunucusunu pasif modda yüklemeden önce herhangi bir site sistemi rolünü barındırmıyor.  

3. **Sistem rolü seçimi** sayfasında, yalnızca **pasif modda site sunucusu**' nu seçin.  

    > [!NOTE]  
    > Sihirbaz bu sayfada aşağıdaki ilk önkoşul denetimlerini gerçekleştirir:
    >
    > - Seçili sunucu ikincil site sunucusu değil
    > - Seçili sunucu pasif modda zaten bir site sunucusu değil
    > - Sitenin içerik kitaplığı uzak bir konumda  
    >  
    > Bu ilk önkoşul denetimi başarısız olursa, sihirbazın bu sayfasını geçmiş olarak devam edemiyorum.  

4. **Site sunucusunda, pasif modda** sayfasında, kurulum 'u çalıştırmak ve site sunucusu rolünü belirtilen sunucuya yüklemek için kullanılan aşağıdaki bilgileri sağlayın:

     - Aşağıdaki seçeneklerden birini belirleyin:  

         - **Yükleme kaynak dosyalarını, etkin modda site sunucusundan ağ üzerinden Kopyala**: Bu seçenek, sıkıştırılmış bir paket oluşturur ve bunu yeni site sunucusuna gönderir.  

         - **Site sunucusunda aşağıdaki konumda bulunan kaynak dosyalarını pasif modda kullanın**: Örneğin, kaynak dosyaları zaten kopyaladığınız yerel bir yol. Bu içeriğin, etkin moddaki site sunucusuyla aynı sürümde olduğundan emin olun.  

         - (*Önerilen*) **Şu ağ konumundaki kaynak dosyaları kullan**: doğrudan CD içeriğinin yolunu belirtin **. **Site sunucusundan etkin modda en son klasör. Örneğin, `\\Server\SMS_ABC\CD.Latest` "*sunucu*", site sunucusunun etkin moddaki adı ve "*ABC*" site kodudur.  

     - Yeni site sunucusuna Configuration Manager yükleneceği yerel yolu belirtin. Örneğin, `C:\Program Files\Configuration Manager`  

5. Sihirbazı tamamlayın. Configuration Manager daha sonra site sunucusunu belirtilen sunucuda pasif modda yükleyecek.

Ayrıntılı yükleme durumu için, konsolunda **izleme** çalışma alanına gidin ve **site sunucusu durum** düğümünü seçin. Pasif moddaki site sunucusunun durumu **yükleme**olarak görüntülenir. Daha ayrıntılı bilgi için sunucuyu seçin ve **durumu göster**' e tıklayın. Bu eylem, site sunucusu yükleme durumu penceresini açar. İşlem tamamlandığında, durum her iki sunucu için de **Tamam** ' ı gösterir.

Kurulum işlemi hakkında daha fazla bilgi için bkz. [Flowchart-site sunucusunu pasif modda ayarlama](passive-site-server-flowchart.md).

Pasif modda bir site sunucusu ekledikten sonra, konsolunun **siteler** düğümündeki **düğümler** sekmesinde her iki site sunucusuna da bakın.

Tüm Configuration Manager site sunucusu bileşenleri, site sunucusunda pasif modda bekleme konumdadır. Windows Hizmetleri çalışmaya devam etmektedir.

## <a name="site-server-promotion"></a>Site sunucusu yükseltme  

Yedekleme ve kurtarma gibi benzer şekilde, site sunucularını değiştirmek için işleminizi planlayın ve yapın. Promosyon planınızdan aşağıdaki noktaları göz önünde bulundurun:  

- Her iki site sunucusunun da çevrimiçi olduğu planlı bir yükseltme yapın. Ayrıca, etkin modda site sunucusunu zorla keserek veya kapatarak planlanmamış bir yük devretme işlemi yapın.  

- Yük devretme sırasında işletimsel işlemlerinizi ve diğer Configuration Manager yöneticilerle iletişim kurmayı öğrenin.  

- Planlı bir yükseltmeden önce:  

  - Site ve site bileşenlerinin genel durumunu kontrol edin. Ortamınız için her şeyin sağlıklı olduğundan emin olun.  

  - Siteler arasında etkin bir şekilde çoğaltılan paketlerin içerik durumunu denetleyin.  

  - İkincil site durumunu ve site çoğaltmasını denetleyin.

  - Alt veya ikincil site sunucuları üzerinde yeni bir içerik dağıtım işi veya bakım yapmayın.

    > [!NOTE]
    > Yük devretme sırasında siteler arasında dosya veya veritabanı çoğaltması devam ediyorsa, yeni site sunucusu çoğaltılan içeriği alamayabilir. Bu durumda, yeni site sunucusu etkin olduktan sonra yazılım içeriğini yeniden dağıtın.<!--515436--> Veritabanı çoğaltması için, yük devretmeden sonra ikincil bir siteyi yeniden başlatmanız gerekebilir.<!-- SCCMDocs issue 808 -->

  - Diğer zamanlanan etkinlikleri aynı anda azaltın veya kaldırın. Örneğin, siteyi yeni bir sürüme güncelleştirdikten hemen sonra bir site sunucusunu yükseltmeyi planlayın. Site güncelleştirmesi, site sunucusu promosyonu olabilecek diğer görevleri içerir.

    > [!TIP]
    > Diğer etkinliklerin site sunucusu promosyonu ile nasıl çakışabileceğinden ilgili bir örnek aşağıda verilmiştir:
    >
    > - Pazartesi: siteyi en son sürüme güncelleştirin. İstemci pilot ile otomatik istemci yükseltmesini etkinleştirin.
    > - Salı: site sunucusunu pasif modda etkin site sunucusu olacak şekilde yükseltin.
    >
    > Bu eylem, Çarşamba veya Perşembe ile yalnızca pilot koleksiyonu değil *Tüm* istemcilerin yükseltmesine neden olabilir. Bu davranış önemli ağ kullanımına ve dağıtım noktalarında beklenmeyen yüke neden olabilir.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Site sunucusunu pasif modda etkin moda yükseltmek için işlem

Bu bölümde, site sunucusunun pasif modda etkin moda nasıl değiştirileceği açıklanmaktadır. Siteye erişmek ve bu değişikliği yapmak için SMS sağlayıcısı 'nın bir örneğine erişebiliyor olmanız gerekir. Daha fazla bilgi için bkz. [birden çok SMS sağlayıcısı kullanma](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> SMS sağlayıcısının tüm örnekleri çevrimdışıysa, hiçbir sağlayıcı kullanılamadığından siteye bağlanamazsınız. Site sunucusunu pasif modda eklediğinizde, kurulum bu sunucuya SMS sağlayıcısı 'nın bir örneğini kurar.<!-- SCCMDocs#1613 -->
>
> Configuration Manager konsolu, site sunucusundaki WMI 'dan kullanılabilir SMS sağlayıcılarının listesini ister. Bir sitede birden çok SMS sağlayıcısı yüklediğinizde, site her yeni bağlantı isteğini yüklü bir SMS sağlayıcısını kullanacak şekilde rastgele atar. Belirli bir bağlantı oturumuyla kullanılacak SMS sağlayıcı konumunu belirtemezsiniz. Geçerli site sunucusu çevrimdışı olduğu için konsolunuz siteye bağlanamıyorsa, site bağlantısı penceresinde diğer site sunucusunu belirtin.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Siteyi seçin ve ardından **düğümler** sekmesine geçin. pasif modda site sunucusunu seçin ve ardından Şeritteki **etkin 'e Yükselt ' e** tıklayın. Onaylamak ve devam etmek için **Evet** ' e tıklayın.
  
2. Konsol düğümünü yenileyin. Yükseltmekte olduğunuz sunucunun **durum** sütunu, **yükseltme**olarak **düğümler** sekmesinde görüntülenir.  

3. Yükseltme tamamlandıktan sonra **durum** sütunu, etkin modda hem yeni site sunucusu için hem de pasif modda yeni site sunucusu için **Tamam** ' ı gösterir. Site için **sunucu adı** sütunu artık yeni site sunucusunun adını etkin modda görüntülüyor.

Ayrıntılı durum için **izleme** çalışma alanına gidin ve **site sunucusu durum** düğümünü seçin. **Mod** sütunu, hangi sunucunun *etkin* veya *Pasif*olduğunu tanımlar. Bir sunucuyu pasif moddan etkin moda yükselttiğinizde, etkin duruma yükselttiğiniz site sunucusunu seçin ve ardından Şeritteki **durumu göster** ' i seçin. Bu eylem, işlem hakkında ek ayrıntılar görüntüleyen site sunucusu yükseltme durumu penceresini açar.

Etkin moddaki bir site sunucusu pasif moda geçtiğinde, yalnızca site sistem rolü pasif hale getirilir. Bu bilgisayarda yüklü olan diğer tüm site sistem rolleri etkin ve istemciler tarafından erişilebilir durumda kalır.

*Planlı* yükseltme işlemi hakkında daha fazla bilgi için bkz. [akış çizelgesi-yükseltme site sunucusu (planlı)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Planlanmamış yük devretme

Etkin moddaki geçerli site sunucusu çevrimdışıysa, yükseltme için site sunucusu, etkin modda 30 dakika boyunca geçerli site sunucusuyla iletişim kurmaya çalışır. Çevrimdışı sunucu bu süreden önce geri gelirse, başarıyla bildirilir ve değişiklik düzgün şekilde devam eder. Aksi takdirde, yükseltme için site sunucusu, site yapılandırmasını etkin olacak şekilde günceller. Çevrimdışı sunucu bu tarihten sonra geri gelirse, önce site veritabanındaki geçerli durumu denetler. Daha sonra, kendisini pasif modda site sunucusuna indirgeme ile devam eder.

Bu 30 dakikalık bekleme süresi boyunca sitede etkin modda site sunucusu yoktur. İstemciler yönetim noktaları, yazılım güncelleştirme noktaları ve dağıtım noktaları gibi istemciye yönelik rollerle hala iletişim kurar. Kullanıcılar, zaten dağıtılmış olan yazılımları yükleyebilir. Bu dönemde site yönetimi mümkün değildir. Daha fazla bilgi için bkz. [site hatası etkileri](../../manage/site-failure-impacts.md).  

Çevrimdışı sunucu, dönemediğinden, bu site sunucusunu konsolundan silin. Ardından, yüksek oranda kullanılabilir bir hizmeti geri yüklemek için pasif modda yeni bir site sunucusu oluşturun.

*Planlanmamış* yük devretme süreci hakkında daha fazla bilgi için bkz. [akış çizelgesi-yükseltme site sunucusu (Planlanmamış)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Site sunucusu yükseltme sonrasında ek görevler  

Site sunucularını değiştirdikten sonra, [bir siteyi kurtarırken](../../manage/recover-sites.md#post-recovery-tasks)gerekli olduğu gibi diğer görevlerin çoğunu yapmanız gerekmez. Örneğin, parolaları sıfırlamanız veya Microsoft Intune aboneliğinizi yeniden bağlamanız gerekmez.

Ortamınızda gerekliyse aşağıdaki adımlar gerekli olabilir:  

- Dağıtım noktaları için PKI sertifikalarını içeri aktarırsanız, etkilenen sunucular için sertifikayı yeniden içeri aktarın. Daha fazla bilgi için bkz. [dağıtım noktaları için sertifikaları yeniden üretme](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Iş için Microsoft Store Configuration Manager tümleştirirseniz, bu bağlantıyı yeniden yapılandırın. Daha fazla bilgi için bkz. [iş için Microsoft Store uygulamaları yönetme](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

## <a name="daily-monitoring"></a>Günlük izleme

Pasif modda bir site sunucusu varsa, bunu günlük olarak izleyin. Durumunun tamam olduğundan ve kullanıma hazırlandığına emin olun. Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **site sunucusu durum** düğümünü seçin. Site sunucularını ve bunların geçerli durumlarını görüntüleyin. Ayrıca **Yönetim** çalışma alanındaki durumu görüntüleyin. **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Siteyi seçin ve ardından **düğümler** sekmesine geçin.

> [!NOTE]
> Siteyi yeni bir Configuration Manager sürümüne güncelleştirdiğinizde, site sunucusunu pasif modda da güncelleştirir. <!-- SCCMDocs-pr#4293 -->