---
title: Site yüklemeye hazırlanma
titleSuffix: Configuration Manager
description: Birden çok Configuration Manager sitesi yüklemeyi planlıyorsanız, zamandan tasarruf etmenize ve hataları önlemenize yardımcı olması için bu bilgileri okuyun.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718185"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Configuration Manager siteleri yüklemeye hazırlanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir veya daha fazla Configuration Manager sitesinin başarılı bir dağıtımına hazırlanmak için, bu makaledeki ayrıntılarla ilgili bilgi sahibi olun. Bu adımlar, birden çok sitenin yüklenmesi sırasında size zaman kazandırabilir ve bir veya daha fazla siteyi yeniden yükleme gereksinimlerimizden kaynaklanan yanlış adımları önlemeye yardımcı olabilir.

> [!TIP]
> Configuration Manager sitesi ve hiyerarşi altyapısını yönetirken, *yükseltme*, *güncelleştirme ve güncelleştirme*terimleri, üç *install* ayrı kavram tanımlanmasında kullanılır. Her bir terimin nasıl kullanıldığını öğrenmek için bkz. [yükseltme, güncelleştirme ve yüklemeyi](../../../understand/upgrade-update-install.md)öğrenme.

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a>Farklı türlerde siteleri yükleme seçenekleri
Yeni bir Configuration Manager sitesi yüklediğinizde, kullanabileceğiniz kaynak dosyaların sürümü zaten hiyerarşide (varsa) bulunan sitelerin sürümüne bağlıdır. Kullanabileceğiniz yükleme yöntemleri, yüklemek istediğiniz sitenin türüne bağlıdır.  

Bir siteyi yüklemeden önce hiyerarşinizi planladığınızdan ve yüklemek istediğiniz site türünü anladığınızdan emin olun. Daha fazla bilgi için bkz. [site hiyerarşisi tasarlama](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>İlk site
Bir hiyerarşiye yüklediğiniz ilk site tek başına birincil site veya merkezi yönetim sitesi olacaktır.

**Yükleme medyası**: bir merkezi yönetim sitesini veya tek başına birincil siteyi yeni bir hiyerarşinin ilk sitesi olarak yüklemek için Configuration Manager [temel bir sürümünü kullanmanız](../../../../core/servers/manage/updates.md#bkmk_Baselines) gerekir. Yeni bir hiyerarşinin ilk sitesini CD 'den güncelleştirilmiş kaynak dosyaları kullanarak yüklemeyin [. Herhangi bir sitenin en son klasörü](../../../../core/servers/manage/the-cd.latest-folder.md) .

**Yükleme yöntemi**: [Configuration Manager Kurulum Sihirbazı 'nı](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)kullanarak iki tür siteyi yükleyebilir veya komut dosyası [komut satırı yüklemesiyle](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)kullanılacak bir betiği yapılandırabilirsiniz.


### <a name="additional-sites"></a>Ek siteler
İlk site yüklendikten sonra dilediğiniz zaman daha fazla site ekleyebilirsiniz. Siteler eklemek için aşağıdaki seçeneklere sahipsiniz ( [desteklenen sınırlara](../../../../core/plan-design/configs/size-and-scale-numbers.md)kadar):

|Sahip olduğunuz site|Yükleyebileceğiniz ek site türü|
|---|---|
|Merkezi yönetim sitesi|Alt birincil site|
|Alt birincil site|İkincil site|
|Tekil birincil site|İkincil site (birincil siteyi genişleterek tek başına birincil siteyi bir alt birincil siteye dönüştürebilirsiniz)|

**Yükleme medyası**: tek başına bir birincil siteyi genişletmek için bir merkezi yönetim sitesi yüklediğinizde veya var olan bir hiyerarşiye yeni bir alt birincil site yüklerseniz, mevcut sitenin veya sitelerin sürümüyle eşleşen yükleme medyasını (kaynak dosyaları içeren) kullanmanız gerekir.

> [!IMPORTANT]
> Daha önce yüklenen sitelerin sürümünü değiştiren konsol içi güncelleştirmeler yüklediyseniz, özgün yükleme medyasını kullanmayın. Bunun yerine, bu senaryoda CD 'deki kaynak dosyalarını kullanın [. Güncel bir sitenin en son klasörü](../../../../core/servers/manage/the-cd.latest-folder.md) . Configuration Manager, yeni sitenizin bağlanacağı mevcut sitenin sürümüyle eşleşen kaynak dosyalar kullanmanızı gerektirir.

Configuration Manager konsolundan İkincil bir site yüklü olmalıdır. Bu şekilde, ikincil siteler her zaman üst birincil sitedeki kaynak dosyalar kullanılarak yüklenir.

**Yükleme yöntemi**: ek siteleri yüklemek için kullandığınız yöntem, yüklemek istediğiniz sitenin türüne bağlıdır.
- **Merkezi Yönetim sitesi ekleme**: yeni merkezi yönetim sitesini mevcut tek başına birincil sitenize bir üst site olarak yüklemek Için Configuration Manager Kurulum Sihirbazı 'nı veya komut dosyası komut satırını kullanabilirsiniz. Daha fazla bilgi için bkz. [tek başına birincil siteyi genişletme](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Alt birincil site ekleme**: merkezi yönetim sitesinin altına bir alt birincil site eklemek Için Configuration Manager Kurulum Sihirbazı 'nı veya bir komut satırı yüklemesi kullanabilirsiniz.
- **İkincil site ekleme**: ikincil bir siteyi bir birincil sitenin altına alt site olarak yüklemek için Configuration Manager konsolunu kullanın. İkincil siteler eklemek için diğer yöntemler desteklenmez.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a>Yüklemeyi başlatmadan önce tamamlanacak olan ortak görevler
- **Dağıtımınız için kullanacağınız hiyerarşi topolojisini anlayın**    
Daha fazla bilgi için bkz. [Configuration Manager için bir site hiyerarşisi tasarlama](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Configuration Manager ile kullanım için önkoşulları ve desteklenen konfigürasyonları karşılamak üzere ayrı sunucular hazırlayın ve yapılandırın**         
Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

- **Site veritabanını barındırmak için SQL Server yükleyip yapılandırın**     
Daha fazla bilgi için bkz. [Configuration Manager için SQL Server sürümleri desteği](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Ağ ortamınızı Configuration Manager destekleyecek şekilde hazırlayın**      
Daha fazla bilgi için bkz. [Configuration Manager için hazırlanmak üzere güvenlik duvarları, bağlantı noktaları ve etki alanlarını yapılandırma](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Ortak anahtar altyapısı (PKI) kullanacaksanız, altyapınızı ve sertifikalarınızı hazırlayın**      
Daha fazla bilgi için bkz. [Configuration Manager Için PKI sertifikası gereksinimleri](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Site sunucuları veya site sistemi sunucuları olarak kullanacağınız bilgisayarlara en son güvenlik güncelleştirmelerini yükler ve gerektiğinde bunları yeniden başlatın**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>Site adları ve site kodları hakkında
Site kodları ve site adları, Configuration Manager hiyerarşisindeki siteleri tanımlamak ve yönetmek için kullanılır. Configuration Manager konsolunda, site kodu ve site adı &lt; *site kodu*\> - &lt;*site adı* \> biçiminde görüntülenir. Hiyerarşinizde kullandığınız her site kodu benzersiz olmalıdır. Active Directory şeması Configuration Manager için genişletilmişse ve siteleriniz veri yayımlıyorsa, bir Active Directory ormanında kullanılan site kodları farklı bir Configuration Manager hiyerarşisinde kullanılsalar veya daha önceki Configuration Manager yüklemelerde kullanılsalar bile benzersiz olmalıdır. Hiyerarşinizi dağıtmadan önce site kodlarınızı ve site adlarınızı dikkatle planlayın.

### <a name="specify-a-site-code-and-site-name"></a>Bir site kodu ve site adı belirtin
Configuration Manager Kurulum 'U çalıştırdığınızda, merkezi yönetim sitesi için site kodu ve site adı ve her birincil site ve ikincil site yüklemesi istenir. Bir site kodu hiyerarşideki her bir siteyi benzersiz şekilde tanımlamalıdır. Site kodu klasör adlarında kullanıldığından, site kodu için Configuration Manager ve Windows için ayrılan adları içeren aşağıdaki adları hiçbir şekilde kullanmayın:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Configuration Manager Kurulum, bir site kodunun zaten kullanımda olduğunu doğrulamaz.

Configuration Manager Kurulum 'U çalıştırırken bir sitenin site kodunu girmek için üç alfasayısal karakter girmeniz gerekir. Site kodlarında yalnızca *a* - *Z* ve *0* ile *9*arasındaki sayılara izin verilir. Harfler veya sayıların sırası, siteler arasındaki iletişim üzerinde hiçbir etkiye sahip değildir. Örneğin, bir birincil site *ABC* ve Ikincil site *def*adı vermek gerekli değildir.

Site adı, sitenin kolay ad tanımlayıcısıdır. Yalnızca *a* - *z*, *a* - *z*, *0* - *9*karakterlerini ve site adlarında tireyi (*-*) kullanabilirsiniz.

> [!IMPORTANT]
> Siteyi yükledikten sonra site kodu veya site adı değişikliği desteklenmez.

### <a name="reuse-a-site-code"></a>Site kodunu yeniden kullanma
Site kodları, özgün site ve site kodu kaldırılmış olsa da bir merkezi yönetim sitesi veya birincil site için Configuration Manager hiyerarşisinde birden fazla kez kullanılamaz. Bir site kodunu yeniden kullanırsanız, hiyerarşinizde nesne KIMLIĞI çakışmalarını riske alırsınız. İkincil site ve site kodu Configuration Manager hiyerarşinizde veya Active Directory ormanında artık kullanımda değilse, ikincil bir site için site kodunu yeniden kullanabilirsiniz.

## <a name="limits-and-restrictions-for-installed-sites"></a>Yüklü siteler için sınırlar ve kısıtlamalar
Site yüklemeden önce, siteler ve site hiyerarşileri için uygulanan aşağıdaki kısıtlamaların anlaşılması önemlidir:
- Kurulumu çalıştırdıktan sonra, siteyi kaldırmadan aşağıdaki site özelliklerini değiştiremezsiniz ve yeni değerleri kullanarak yeniden yükleyebilirsiniz:  
  - Program dosyaları yükleme dizini  
  - Site kodu  
  - Site açıklaması  
- Hiyerarşiniz bir merkezi yönetim sitesi içerdiğinde:  
  - Configuration Manager, bir alt birincil sitenin tek başına bir birincil site oluşturmak veya farklı bir hiyerarşiye iliştirilmesi için bir hiyerarşinin dışına taşınmasını desteklemez. Bunun yerine, alt birincil siteyi kaldırın ve ardından yeni bir tek başına birincil site olarak veya farklı bir hiyerarşinin merkezi yönetim sitesinin bir alt sitesi olarak yeniden yükleyin.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a>Kurulumu çalıştırmadan önce isteğe bağlı adımlar
**[Kurulum Yükleyici](../../../../core/servers/deploy/install/setup-downloader.md) 'yi el ile çalıştırma**

Configuration Manager için güncelleştirilmiş Kurulum dosyalarını indirmek için kurulum yükleyici 'yi çalıştırabilirsiniz. Kurulumu çalıştırabileceğiniz bilgisayar Internet 'e bağlı değilse veya birden çok site sunucusu yüklemeyi düşünüyorsanız, kurulum için gerekli güncelleştirmeleri indirmek için kurulum yükleyici 'yi kullanmayı düşünün. Ek bilgiler aşağıda verilmiştir:
- Varsayılan olarak, kurulum güncelleştirilmiş Kurulum dosyalarını indirmek için Internet 'e bağlanır.
- Dosyalar varsayılan olarak Redist klasöründe depolanır.
- Kurulumu, ağınızda daha önce bu dosyaların bir kopyasını depoladığınız bir konuma yönlendirebilirsiniz.

**[Önkoşul denetleyicisi 'ni](../../../../core/servers/deploy/install/prerequisite-checker.md) el ile çalıştırma**

Bir siteyi yüklemek için kurulum 'U çalıştırmadan önce sorunları belirlemek ve onarmak için ve bir sunucuya site sistemi rolü yüklemeden önce, önkoşul denetleyicisi ' ni çalıştırabilirsiniz. Önkoşul denetleyicisi, bilgisayarın site veya site sistem rolünü barındırmak için gereksinimleri karşıladığından emin olmanıza yardımcı olur. Ek bilgiler aşağıda verilmiştir:
- Varsayılan olarak, kurulum önkoşul denetleyicisi 'Ni çalıştırır.
- Herhangi bir hata oluşursa, kurulum sorun düzeltilinceye kadar duraklar.

**İsteğe bağlı bağlantı noktalarını tanımla**

Site sistemleri ve istemcilerinin kullanması için isteğe bağlı bağlantı noktaları tanımlayabilirsiniz. Ek bilgiler aşağıda verilmiştir:
- Varsayılan olarak, site sistemleri ve istemciler, iletişim kurmak için önceden tanımlanmış bağlantı noktalarını kullanır.
- Kurulum sırasında alternatif bağlantı noktalarını yapılandırabilirsiniz.

Daha fazla bilgi için bkz. [kullanılan bağlantı noktaları](../../../../core/plan-design/hierarchy/ports.md).
