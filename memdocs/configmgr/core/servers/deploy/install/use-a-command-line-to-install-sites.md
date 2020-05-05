---
title: Komut satırı yüklemesi
titleSuffix: Configuration Manager
description: Çeşitli site yüklemeleri için komut isteminde Configuration Manager kurulumunu çalıştırmayı öğrenin.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717961"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Configuration Manager siteleri yüklemek için komut satırı kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Çeşitli site türlerini yüklemek için, bir komut isteminde Configuration Manager kurulumunu çalıştırabilirsiniz.

## <a name="supported-tasks-for-command-line-installations"></a>Komut satırı yüklemeleri için desteklenen görevler
 Kurulum 'U çalıştırma yöntemi aşağıdaki site yükleme ve site bakım görevlerini destekler:

- **Bir merkezi yönetim sitesini veya birincil siteyi komut isteminden yükler**  
  [Kurulum Için komut satırı seçeneklerini](../../../../core/servers/deploy/install/command-line-options-for-setup.md) görüntüle

- **Bir merkezi yönetim sitesinde veya birincil sitede kullanımdaki dilleri değiştirme**  
   Bir sitede yüklü olan dilleri bir komut isteminden (mobil aygıtlar için diller dahil) değiştirmek için şunları yapmanız gerekir:  

  - Site sunucusunda ** &lt;configmgrınstallationpath\>\x64** konumundan kurulum 'u çalıştırın.
  - **/MANAGELANGS** komut satırı seçeneğini kullanın,
  - Eklemek veya kaldırmak istediğiniz dilleri belirten bir dil betiği dosyası belirtin  

    Örneğin, şu komut söz dizimini kullanın: **setupwpf. exe/MANAGELANGS &lt;dil betiği dosyası\> **  

    Dil komut dosyasını oluşturmak için, [dilleri yönetmek Için komut satırı seçeneklerindeki](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang) bilgileri kullanın  

- **Katılımsız site yüklemeleri veya site kurtarma için bir yükleme komut dosyası kullanın**  
   Bir yükleme betiği kullanarak kurulum 'U bir komut isteminden çalıştırabilir ve katılımsız bir site yüklemesi çalıştırırsınız. Ayrıca, bu seçeneği bir siteyi kurtarmak için de kullanabilirsiniz.    

   Kurulum ile bir komut dosyası kullanmak için:  

  - Kurulum 'U komut satırı-seçeneği **/SCRIPT** ile çalıştırın ve bir betik dosyası belirtin.  

  - Betik dosyasının gerekli anahtarlar ve değerlerle yapılandırılması gerekir.  

    Bir merkezi yönetim sitesinin veya birincil sitenin katılımsız yüklemesi için, betik dosyası aşağıdaki bölümlere sahip olmalıdır:  

  - Kimlik    
  - Seçenekler    
  - SQLYapılandırmaSeçenekleri    
    -   HierarchyOptions    
  - Cloudconnectoroçen   

    Bir siteyi kurtarmak için betik dosyasının aşağıdaki bölümlerini de dahil etmeniz gerekir:  

  - Kimlik  
  - Kurtarma

Daha fazla bilgi için bkz. [Configuration Manager Için katılımsız Site Recovery](../../manage/unattended-recovery.md).  

Katılımsız yükleme betik dosyasında kullanılacak anahtarların ve değerlerin listesi için bkz. [Katılımsız Kurulum betik dosyası anahtarları](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Komut satırı betik dosyası hakkında  
 Configuration Manager Katılımsız yüklemeleri için, kurulum 'U komut satırı seçeneği **/SCRIPT**ile çalıştırabilir ve yükleme seçeneklerini içeren bir betik dosyası belirtebilirsiniz. Aşağıdaki görevler bu yöntem kullanılarak desteklenir:  

-   Bir merkezi yönetim sitesi yükler  
-   Birincil site yükler  
-   Configuration Manager konsolu 'nu yükler  
-   Site kurtarma  

> [!NOTE]  
>  Katılımsız betik dosyasını, bir değerlendirme sitesini Configuration Manager lisanslı bir yüklemesine yükseltmek için kullanamazsınız.  

### <a name="the-cdlatest-key-name"></a>CDLatest anahtar adı
CD 'den medya kullandığınızda. Aşağıdaki dört yükleme seçeneğinin komut dosyalı bir yüklemesini çalıştırmak için en son klasör, betiğinizin değeri **1**olan **cdlatest** anahtarını içermesi gerekir:
- Yeni bir merkezi yönetim sitesi yükler
- Yeni bir birincil site yükler
- Merkezi yönetim sitesini kurtarma
- Birincil siteyi kurtarma

Bu değer, Microsoft toplu lisans sitesinden aldığınız yükleme medyasında kullanılmak üzere desteklenmez.
Bu anahtar adının betik dosyasında nasıl kullanılacağı hakkında bilgi için bkz. [komut satırı seçenekleri](command-line-options-for-setup.md) .



### <a name="create-the-script"></a>Betiği oluşturma
Yükleme betiği, [Kullanıcı arabirimini kullanarak bir site yüklemek Için kurulumu çalıştırdığınızda](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)otomatik olarak oluşturulur.  Sihirbazın **Özet** sayfasındaki ayarları onaylamanız halinde şunlar olur:  

-   Kurulum, **%Temp%\ConfigMgrAutoSave.ini**betiğini oluşturur.  Bu dosyayı kullanmadan önce yeniden adlandırabilirsiniz, ancak. ini dosya uzantısının korunması gerekir.  
-   Katılımsız yükleme betiği, sihirbazda seçtiğiniz ayarları içerir.  
-   Betik oluşturulduktan sonra, hiyerarşinizdeki diğer siteleri yüklemek için komut dosyasını değiştirebilirsiniz.  
-   Daha sonra bu betiği, Configuration Manager Katılımsız kurulumu gerçekleştirmek için kullanabilirsiniz.  

Bu betik dosyası, varsayılan ayar olmaması dışında, Kurulum Sihirbazı tarafından istemde bulunan bilgileri sağlar.   
Kullanmakta olduğunuz yükleme türü için uygulanan kurulum anahtarlarının tüm değerlerini belirtmeniz gerekir.   

Kurulum Katılımsız yükleme betiğini oluşturduğunda, kurulum sırasında girdiğiniz ürün anahtarı değeri ile doldurulur. Bu, geçerli bir ürün anahtarı veya Configuration Manager değerlendirme sürümünü yüklediğinizde **eval** olabilir. Komut dosyasındaki ürün anahtarı değeri, önkoşul denetiminin tamamlanabilmesi için doldurulur.   

Kurulum gerçek site yüklemesini başlattığında, otomatik olarak oluşturulan betiği, oluşturduğu betikteki ürün anahtarı değerini temizlemek için yeniden yazılır. Yeni bir sitenin katılımsız yüklemesi için betiği kullanmadan önce, geçerli bir ürün anahtarı sağlamak veya Configuration Manager değerlendirme yüklemesi belirtmek üzere betiği düzenleyebilirsiniz.  

### <a name="section-names-key-names-and-values"></a>Bölüm adları, anahtar adları ve değerler
Betik, bölüm adlarını, anahtar adlarını ve değerleri içerir. Aşağıdaki bilgileri not edin:
-   Gerekli bölüm anahtarı adları, komut dosyası oluşturduğunuz yükleme türüne bağlı olarak farklılık gösterir.
-   Anahtarların bölümler içindeki sırası ve bölümlerin dosya içindeki sırası önemli değildir.     
-   Anahtarlar büyük/küçük harfe duyarlı değildir.  
-   Anahtarlar için değer sağladığınızda, anahtarın adının arkasından bir eşittir işareti (=) ve anahtar değeri gelmelidir.    

> [!TIP]  
>  Tüm seçenek kümesini görüntülemek için, bkz. [Kurulum ve betikler Için komut satırı seçenekleri](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>/SCRıPT kurulum komut satırı seçeneğini kullanın

-   Bir Kurulum betik dosyası kullanmanız ve **/Script** kurulum komut satırı seçeneğinden sonra dosya adını belirtmeniz gerekir. Aşağıdaki bilgileri not edin:   
    -   Dosyanın adı **. ini** dosya adı uzantısına sahip olmalıdır.  
    -   Komut isteminde kurulum komut dosyasına başvurduğunuzda dosyanın tam yolunu belirtmeniz gerekir. Örneğin, Kurulum başlatma dosyanızın adı Setup. ini ise ve C:\Setup klasöründe depolanıyorsa, komut isteminde şunu yazın: **Setup/Script c:\setup\Setup.ini**.  

-   Kurulumu çalıştıran hesap bilgisayarda **yönetici** haklarına sahip olmalıdır. Kurulumu Katılımsız komut dosyasıyla çalıştırdığınızda **yönetici olarak çalıştır** seçeneğini kullanarak komut istemi penceresini açın.   
