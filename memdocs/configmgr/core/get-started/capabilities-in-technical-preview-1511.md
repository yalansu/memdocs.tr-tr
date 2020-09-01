---
title: Technical Preview 1511 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1511 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a7b61e1a609e0693ffcd30f3f7dc931f4cb38eef
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193647"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Configuration Manager için Technical Preview 1511 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1511 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürüm, Technical Preview için yeni bir Technical Preview sitesi yükleme veya daha önceki bir Technical Preview sürümünden yükseltme için kullanabileceğiniz bir temel yüklemedir.   Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](technical-preview.md).  

Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Windows 10 ' da Iş için Windows Update tümleştirme  
 Configuration Manager artık, Windows Update for Business (WUfB) ile doğrudan bağlanmış bir Windows 10 bilgisayarını, Windows 10 güncelleştirmelerini ve yükseltmelerini almak için WSUS 'a bağlananlardan ayırt etme özelliğine sahiptir.  WUfB aracılığıyla bağlanan bilgisayarlar için, güncelleştirmeler ve yükseltmeler, Grup Ilkeleri veya MDM ilkeleri aracılığıyla yönetici kullanıcı tarafından ayarlanan temposunda üzerinden yönetilebilir ve bu güncelleştirmeler/yükseltmeler doğrudan WUfB 'den yüklenebilir.    
WUfB aracılığıyla bağlanan bilgisayarlar için Configuration Manager uyumluluk durumunu (Windows güncelleştirmeleri veya tanım güncelleştirmeleri dahil) bildiremeyecektir. Ayrıca Configuration Manager, bu bilgisayarlara Microsoft güncelleştirmeleri veya üçüncü taraf güncelleştirmeleri dağıtamayacak.  

 **Bu senaryonun önkoşulları:**  

-   Windows 10 Desktop Pro veya Windows 10 Enterprise Edition Sürüm 1511 veya üzeri  

-   [Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb) üzerinden yönetilecek bilgisayarlar.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevi tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için bu konunun en üstündeki geri bildirim bilgilerini kullanın:  

1.  Daha önce etkinleştirildiyse, WSUS’de tarama yapmaması için Windows Update Aracısı'nı devre dışı bırakın.   
    **HKEY_LOCAL_MACHINE \software\policies\microsoft\windows\windowsupdate\au\usewsusserver** kayıt defteri anahtarı, bilgisayarın WSUS veya Windows Update karşı tarama yapıp yapamadığını belirtmek üzere ayarlanabilir.  Değer 2 olduğunda, WSUS 'ye karşı tarama değildir.  

2.  Configuration Manager Kaynak Gezgini **Windows Update** düğümü altında **UseWUServer**adlı yeni özniteliği göz önünde edin.  

3.  Güncelleştirmeler ve yükseltmeler için WUfB üzerinden bağlı tüm bilgisayarlarda **UseWUServer** özniteliğini temel alan bir koleksiyon oluşturun.  

4.  Yazılım güncelleştirme iş akışını devre dışı bırakmak ve ayarı WUfB’ye doğrudan bağlı bilgisayar koleksiyonuna dağıtmak için bir istemci aracısı ayarı oluşturun.  

5.  WUfB üzerinden yönetilen bilgisayarların uyumluluk durumunda **bilinmiyor** görüntülenir ve genel uyumluluk yüzdesinin bir parçası olarak sayılmaz.  

##  <a name="managing-microsoft-365-apps-for-enterprise-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Configuration Manager aracılığıyla kurumsal Istemci güncelleştirmesi için Microsoft 365 uygulamalarını yönetme  
Configuration Manager artık Configuration Manager Yazılım Güncelleştirmesi Yönetimi iş akışını kullanarak Microsoft 365 Masaüstü istemci güncelleştirmelerini yönetme özelliğine sahiptir.
Microsoft, Windows Server Updates Services (WSUS) için yeni bir Microsoft 365 Masaüstü istemci güncelleştirmesi yayımladığında, Microsoft 365 güncelleştirmesi Katalog eşitlemesinin bir parçası olacak şekilde yapılandırıldıysa, Configuration Manager güncelleştirmeyi kataloğuna eşitleyebilecektir.  Configuration Manager site sunucusu Microsoft 365 istemci güncelleştirmelerini indirir ve paketi Configuration Manager dağıtım noktalarına dağıtacaktır.  Configuration Manager istemci Microsoft 365 Masaüstü istemcilerine güncelleştirmelerin nereden alınacağını ve güncelleştirme yükleme işleminin ne zaman başlatılacağını bildirir.  

**Bu senaryonun önkoşulları:**  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevi tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için bu konunun en üstündeki geri bildirim bilgilerini kullanın:  

1. Microsoft 365 güncelleştirmelerini Configuration Manager site sunucusuna eşitleyebilir ve Configuration Manager konsolundan görüntüleyebilirsiniz.  

2. Microsoft 365 güncelleştirmelerini onaylayabilir ve başarıyla dağıtabilirsiniz.  

3. İstemcilere güncelleştirmeleri indirebilir ve başarıyla Microsoft 365.  

4. Microsoft 365 güncelleştirmeleri için uyumluluğu, konsol içi izleme veya rapor kullanarak doğrulayabilirsiniz.  

   Ayrıntılı adımlar için bkz. [Configuration Manager Technical Preview ile Microsoft 365 istemci güncelleştirmelerini yönetme](/deployoffice/manage-microsoft-365-apps-updates-configuration-manager).  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> Yüksek oranda kullanılabilir veritabanları için SQL Server AlwaysOn desteği  
 Configuration Manager artık site veritabanını barındırmak için SQL Server AlwaysOn kullanılabilirlik grupları kullanmayı desteklemektedir.  Yeni bir site yüklediğinizde, kurulumu normal bir SQL Server örneği yerine kullanılabilirlik grubu kullanacak şekilde yönlendirebilirsiniz.  

> [!NOTE]  
>  Kullanılabilirlik gruplarının başarılı bir şekilde yapılandırılması ve kullanılması, SQL Server kullanılabilirlik gruplarını yapılandırmaya rahat bir şekilde sahip olmanızı ve SQL Server belge kitaplığı 'nda sunulan belge ve yordamlara dayanmasını gerektirir.  

Kullanılabilirlik gruplarını yapılandırmak ve kullanmak için üst düzey işlem şunları içerir:  

1.  SQL Server 'de kullanılabilirlik grubunu yapılandırın.  

2.  Yeni bir Configuration Manager sitesi yükleme ve kurulum sırasında grup uç noktası belirterek siteyi kullanılabilirlik grubunu kullanmaya yönlendirme.  

**Bu senaryonun önkoşulları:**  

-   Configuration Manager Technical Preview tarafından desteklenen SQL Server bir sürümünü gerektirir  

-   SQL Server kullanılabilirlik grubunu yüklemeden önce oluşturmanız ve yapılandırmanız gerekir Configuration Manager  

-   Kullanılabilirlik grubu bir birincil çoğaltmaya sahip olmalıdır ve en çok iki zaman uyumlu ikincil çoğaltma içerebilir  

-   Kullanılabilirlik grubunun en az bir uç noktası olmalıdır  

-   Kullanılabilirlik grubundaki her bir SQL Server erişebileceği bir ağ konumuna sahip olmanız gerekir. Bu konum, kullanılabilirlik grubu yapılandırılırken kurulum tarafından kullanılır ve kurulum tamamlandıktan sonra kaldırılabilirler.  

**Bu sürüm için bilinen sorunlar:**  

-   Zaten bir site veritabanı olarak kullanılan bir kullanılabilirlik grubuna yeni bir çoğaltma üyesini başarıyla ekleyemezsiniz. Bunun yerine, yeni çoğaltma üyesi eklendikten sonra siteyi yeniden yüklemeniz gerekir.  

-   Bu senaryo için, yönetim noktası sunucusundaki **SQL Server 2012 yerel istemcisini** ([SQL Server 2012 özellik paketinden](https://www.microsoft.com/download/details.aspx?id=29065)) yüklemeniz gerekebilir. Bu durum SQL bağlantı hatalarını önler (yönetim noktası sunucusunda **MP_GetAuth. log** dosyasında günlüğe kaydedilir).  

### <a name="try-it-out"></a>Deneyin!  
Aşağıdaki görevleri tamamlamayı deneyin ve daha sonra bu konunun en üstündeki geri bildirim bilgilerini kullanarak nasıl çalıştıhaberdar etmemizi sağlayın:  

-   SQL AlwaysOn Kullanılabilirlik Grupları için yapılandırılmış bir veritabanı sunucusunu kullanan bir birincil site yükleyebiliyorum  

-   SQL AlwaysOn kullanılabilirlik grubumu gruptaki yeni bir kopyaya devreder ve birincil site hala çalışıyor  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configuration Manager için SQL Server AlwaysOn yapılandırma  
 Önce kullanılabilirlik grubunu oluşturup yapılandırmak için aşağıdaki yordamları kullanın ve ardından kullanılabilirlik grubunu kullanan yeni bir Configuration Manager sitesini yüklemeniz gerekir.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn kullanılabilirlik grubu oluşturmak için  
[SQL Server kullanılabilirlik grubu oluşturma](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15) işlemi SQL Server belge kitaplığında belgelenmiştir.  Kullanılabilirlik grubunu oluşturduğunuzda, Configuration Manager ile kullanım için aşağıdaki gereksinimlerin karşılandığından emin olun:  

-   En fazla üç üye:  

    -   Bir birincil çoğaltma ve en fazla iki ikincil çoğaltma  

    -   İkincil çoğaltmaların zaman uyumlu olması gerekir.  

        > [!TIP]  
        >  İkincil çoğaltmaların Salt okunabilir olacak şekilde yapılandırılmasını öneririz. Bu, site işlemlerine yönelik birincil çoğaltmanın performansını sürdürirken raporlama gibi işlevler için ikincil bir çoğaltma kullanmanıza olanak sağlar.  

-   En az bir uç nokta. Configuration Manager sitesini yüklediğinizde, bu uç noktanın sanal adı kullanılacaktır.  

    > [!TIP]  
    >  Grup birden çok uç nokta içerebilse de Configuration Manager yalnızca birini kullanabilir.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Kullanılabilirlik grubunu kullanan bir Configuration Manager sitesini yüklemek için  
SQL Server kullanılabilirlik grubu kullanan bir site yüklemek için:  

1.  Configuration Manager Kurulum tarafından istendiğinde aşağıdakini değiştirin:  

    -   **SQL Server adı**: kullanılabilirlik grubunu oluştururken yapılandırdığınız uç noktanın sanal adını girin. Sanal ad, ** &lt; endpointserver \> . fabrikam.com**gibi bir tam DNS adı olmalıdır.  

    -   **Örnek**: Bu değer boş kalmalıdır. Bu yapılandırmada örnek yok.  

    -   **Veritabanı**: kullanılabilirlik grubunun birincil çoğaltmasında oluşturduğunuz veritabanının adını girin.  

2.  Sonra, gruptaki her bir SQL Server erişebileceği bir ağ konumu sağlamalısınız:  

    -   Her bir SQL Server bilgisayar hesabı ve hizmet hesabı, bu konuma tam denetim erişimi gerektirir.  

    -   Bu konum yalnızca kurulum sırasında kullanılır ve kurulum tamamlandıktan sonra ve site yüklendikten sonra, paylaşılmayan veya silinebilirler.  

3.  Bu bilgileri verdikten sonra, kurulum 'u normal işlem ve konfigürasyonlarınızla doldurun.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> Sunucu kümesi hizmeti  
Artık bir kümedeki sunucuları içeren bir koleksiyon oluşturabilir ve ardından kümeye güncelleştirmeleri dağıtırken kullanılacak küme ayarlarını yapılandırabilirsiniz. Belirli bir zamanda çevrimiçi olan sunucuların yüzdesini denetleyebilir ve dağıtım öncesi ve dağıtım sonrası PowerShell betiklerini özel eylemleri çalıştıracak şekilde yapılandırabilirsiniz.  

**Bu sürüm için bilinen sorunlar:**  

-   Raporlama, küme sunucuları için yazılım güncelleştirmeleri dağıtımının durumunu denetlemek için kullanılabilir değildir.  

-   **Küme ayarları** sayfasındaki bakım sırası seçeneği devre dışı bırakılmış ve bu sürümde kullanılamıyor.  

### <a name="try-it-out"></a>Deneyin!  
Aşağıdaki görevi tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için bu konunun en üstündeki geri bildirim bilgilerini kullanın:  

-   Sunucu kümesini temsil eden bir koleksiyon oluşturbiliyorum. Bu test için, toplama üyelik kurallarınızı bu koleksiyonda 2 makineye sahip olacak şekilde yapılandırabilirsiniz.  

-   Kümedeki sunucuların yalnızca %50 ' sinin küme hizmeti 'nin herhangi bir noktasında çevrimdışı olduğunu belirtebilir. Dağıtım öncesi ve dağıtım sonrası betikleri belirtmek için yordamdaki örnek betikleri kullanın.  

-   Bu koleksiyona bir güncelleştirme dağıtın. C:\Temp ' teki start.txt ve end.txt dosyalarını gözden geçirin ve kümedeki sunucularda dağıtımın başlangıç ve bitiş zamanlarını doğrulayın. Daha fazla bilgi için UpdatesDeployment. log dosyasını gözden geçirin.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Sunucu kümesine yönelik bir koleksiyon oluşturmak için  

1.  Kümedeki sunucuları içeren [bir cihaz koleksiyonu oluşturun](../clients/manage/collections/create-collections.md) .  

2.  **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları**' na tıklayın, kümedeki sunucuları içeren koleksiyona sağ tıklayın ve ardından **Özellikler**' e tıklayın.  

3.  **Genel** sekmesinde, **tüm cihazlar aynı sunucu kümesinin bir parçası olduğundan**, **Ayarlar**' ı seçin.  

4.  **Küme ayarları** sayfasında, yazılım güncelleştirmelerinin yüklenmesi için aynı anda çevrimdışı alınabilecek sunucu yüzdesini seçin. Bir küme sunucusu, sağladığınız yüzdeden bağımsız olarak, bir seferde çevrimdışı olabilir. Configuration Manager, aynı anda hizmet vermek istediğiniz sunucu sayısını seçerken aşağı yuvarlar. Örneğin, %51 seçeneğini belirlerseniz ve kümede 4 sunucu varsa, aynı anda 2 sunucu çevrimdışı duruma getirilir.  

5.  Dağıtım öncesi (düğüm boşaltma) betiği mi yoksa dağıtım sonrası (düğüm özgeçmişi) betiği mi kullanacağınızı belirtin.  

    > [!TIP]  
    >  Aşağıda, geçerli saati bir metin dosyasına yazan dağıtım öncesi ve dağıtım sonrası betikleri için test etmek üzere kullanabileceğiniz örnekler verilmiştir:  
    >   
    >  **Dağıtım öncesi**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Dağıtım sonrası**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Yazılım güncelleştirmelerini sunucu kümesine dağıtmak için  

1.  [Yazılım güncelleştirmelerini](../../sum/deploy-use/deploy-software-updates.md) sunucu kümesi koleksiyonuna dağıtın.  

2.  [Yazılım güncelleştirme dağıtımını izleyin](../../sum/deploy-use/monitor-software-updates.md).