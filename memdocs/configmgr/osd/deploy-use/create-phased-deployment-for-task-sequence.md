---
title: Aşamalı dağıtımlar oluşturma
titleSuffix: Configuration Manager
description: Yazılım dağıtımını çeşitli koleksiyonlara otomatik hale getirmek için aşamalı dağıtımlar kullanın.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36da7d35b75d2675fc775ed46e49e8adf2e6af3f
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591744"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Configuration Manager aşamalı dağıtımlar oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşamalı dağıtımlar, birden çok koleksiyonda yazılım Eşgüdümlü, sıralı bir şekilde piyasaya dağıtımını otomatik hale getirir. Örneğin, bir pilot koleksiyonuna yazılım dağıtın ve sonra başarı ölçütlerine göre dağıtımı otomatik olarak devam eder. Varsayılan iki aşamadan oluşan aşamalı dağıtımlar oluşturun veya birden çok aşamayı el ile yapılandırın. 

Aşağıdaki nesneler için aşamalı dağıtımlar oluşturun:
- **Görev dizisi**  
    - Görev dizilerinin aşamalı dağıtımı PXE veya medya yüklemesini desteklemez   
- **Uygulama** (sürüm 1806 ' den başlayarak) <!--1358147-->  
- **Yazılım güncelleştirmesi** (sürüm 1810 ' den başlayarak) <!--1358146-->  
    - Aşamalı dağıtım ile otomatik dağıtım kuralı kullanamazsınız

> [!Tip]  
> Aşamalı dağıtım özelliği ilk olarak sürüm 1802 ' de [yayın öncesi bir özellik](../../core/servers/manage/pre-release-features.md)olarak sunulmuştur. Sürüm 1806 ' den başlayarak, artık yayın öncesi bir özellik değildir.<!--1356837-->  



## <a name="prerequisites"></a>Ön koşullar

#### <a name="security-scope"></a>Güvenlik kapsamı
Aşamalı dağıtımlar tarafından oluşturulan dağıtımlar, **Tüm** güvenlik kapsamına sahip olmayan herhangi bir yönetici kullanıcıya görüntülenemez. Daha fazla bilgi için bkz. [Güvenlik kapsamları](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

#### <a name="distribute-content"></a>İçeriği dağıt
Aşamalı dağıtım oluşturmadan önce ilişkili içeriği bir dağıtım noktasına dağıtın.<!--518293-->  

- **Uygulama**: konsolda hedef uygulamayı seçin ve Şeritteki **İçerik Dağıt** eylemini kullanın. Daha fazla bilgi için bkz. [Içerik dağıtma ve yönetme](../../core/servers/deploy/configure/deploy-and-manage-content.md).   

- **Görev sırası**: görev dizisini oluşturmadan önce, işletim sistemi yükseltme paketi gibi başvurulan nesneleri oluşturmanız gerekir. Dağıtım oluşturmadan önce bu nesneleri dağıtın. Her nesne veya görev dizisi üzerinde **Içerik dağıt** eylemini kullanın. Başvurulan tüm içeriğin durumunu görüntülemek için, görev sırasını seçin ve Ayrıntılar bölmesindeki **Başvurular** sekmesine geçin. Daha fazla bilgi için bkz. [işletim sistemi dağıtımına hazırlanma](../get-started/prepare-for-operating-system-deployment.md)içinde belirli nesne türü.   

- **Yazılım güncelleştirmesi**: dağıtım paketini oluşturun ve dağıtın. Yazılım güncelleştirmelerini Indirme Sihirbazı 'Nı kullanın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini indirme](../../sum/deploy-use/download-software-updates.md).  



## <a name="phase-settings"></a><a name="bkmk_settings"></a> Aşama ayarları

Bu ayarlar aşamalı dağıtımlar için benzersizdir. Aşamalı dağıtım işleminin zamanlamasını ve davranışını denetlemek üzere aşamalar oluştururken veya düzenlenirken bu ayarları yapılandırın. 


#### <a name="criteria-for-success-of-the-first-phase"></a>İlk aşamanın başarısı için ölçütler  

- **Dağıtım başarı yüzdesi**: başarılı olması için ilk aşamanın dağıtımı başarıyla tamamlaması gereken cihazların yüzdesini belirtin. Varsayılan olarak, bu değer %95 ' dir. Diğer bir deyişle, site, bu dağıtım için cihazların %95 ' ının uyumluluk durumu **başarılı** olduğunda ilk aşamayı başarılı kabul eder. Daha sonra site ikinci aşamaya devam eder ve bir sonraki koleksiyona yazılım dağıtımı oluşturur.  
- **Başarıyla dağıtılan cihaz sayısı**: Configuration Manager sürüm 1902 ' de eklendi. Başarılı olmak için ilk aşamanın dağıtımı başarıyla tamamlaması gereken cihaz sayısını belirtin. Bu seçenek, koleksiyonun boyutu değişken olduğunda ve sonraki aşamaya geçmeden önce başarıyı göstermek için belirli sayıda cihaza sahip olduğunuzda yararlıdır. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>İlk aşamanın başarılı olduktan sonra dağıtımın ikinci aşamasına yönelik koşullar  

- **Bir erteleme döneminden (gün) sonra bu aşamayı otomatik olarak Başlat**: ilk işlemin başarısından sonra ikinci aşamaya başlamadan önce beklenecek gün sayısını seçin. Varsayılan olarak, bu değer bir gündür.  

- **Dağıtımın ikinci aşamasına el ile başlayın**: ilk aşama başarılı olduktan sonra site ikinci aşamayı otomatik olarak başlamaz. Bu seçenek, ikinci aşamayı el ile başlatmanız gerekir. Daha fazla bilgi için bkz. [sonraki aşamaya geçme](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Bu seçenek, uygulamaların aşamalı dağıtımları için kullanılamaz.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Bu yazılımın kademeli olarak bu süre içinde kullanılabilmesini sağlama (gün)
<!--1358578-->
Sürüm 1806 ' den başlayarak, her aşamada dağıtım için bu ayarı, aşamalı olarak gerçekleşecek şekilde yapılandırın. Bu davranış, dağıtım sorunları riskini azaltmaya yardımcı olur ve içeriğin istemcilerine dağıtılması nedeniyle ağdaki yükü düşürür. Site, her bir aşamanın yapılandırmasına bağlı olarak yazılımı aşamalı olarak kullanılabilir hale getirir. Bir aşamadaki her istemcinin, yazılımın kullanılabilir hale getirilme zamanına göre son tarihi vardır. Kullanılabilir saat ve son tarih arasındaki zaman penceresi, bir aşamadaki tüm istemciler için aynıdır. Bu ayarın varsayılan değeri sıfırdır, bu nedenle varsayılan olarak dağıtım kısıtlanmıyor. Değeri 30 ' dan yüksek bir değere ayarlayın.<!--SCCMDocs-pr issue 2767--> 

![Başarı ayarları için aşamalı dağıtım ölçütleri](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Yazılımın kullanılabilir duruma getirilme tarihine göre son tarih davranışını yapılandırın  

- **Yükleme mümkün olan en kısa sürede gereklidir**: cihaz hedeflendiği anda cihazda yükleme için son tarih ayarlayın.  

- **Bu süre sonunda yükleme gereklidir**: cihaz hedeflendikten sonra yükleme için belirli bir gün sayısını ayarlayın. Varsayılan olarak, bu değer yedi gündür.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a> Otomatik olarak varsayılan iki aşamalı dağıtım oluştur

1. Configuration Manager konsolundaki aşamalı dağıtım oluşturma Sihirbazı 'nı başlatın. Bu eylem, dağıtmakta olduğunuz yazılımın türüne göre farklılık gösterir:  

    - **Uygulama** (yalnızca sürüm 1806 veya üzeri sürümlerde): **yazılım kitaplığı**'Na gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar**' ı seçin. Mevcut bir uygulamayı seçin ve ardından şeritte **aşamalı dağıtım oluştur** ' u seçin.  

    - **Yazılım güncelleştirmesi** (yalnızca sürüm 1810 veya üzeri sürümlerde): **yazılım kitaplığı**'Na gidin, **yazılım güncelleştirmeleri**' ni genişletin ve **tüm yazılım güncelleştirmeleri**' ni seçin. Bir veya daha fazla güncelleştirme seçin ve şeritte **aşamalı dağıtım oluştur** ' u seçin.  

        Bu eylem, aşağıdaki düğümlerden yazılım güncelleştirmeleri için kullanılabilir:  
        - Yazılım Güncelleştirmeleri  
            - **Tüm yazılım güncelleştirmeleri**  
            - **Yazılım güncelleştirme grupları**   
        - Windows 10 bakımı, **tüm Windows 10 güncelleştirmeleri**  
        - Office 365 Istemci yönetimi, **office 365 güncelleştirmeleri**  

    - **Görev sırası**: **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin. Var olan bir görev dizisini seçin ve ardından şeritte **aşamalı dağıtım oluştur** ' u seçin.  

2. **Genel** sayfasında, aşamalı dağıtıma bir **ad**, **Açıklama** (Isteğe bağlı) verin ve **otomatik olarak varsayılan iki aşamalı dağıtım oluştur**' u seçin.  

3. **Araştır** ' ı seçin ve hem **ilk koleksiyon** hem de **ikinci koleksiyon** alanları için bir hedef koleksiyon seçin. Bir görev dizisi ve yazılım güncelleştirmeleri için Cihaz Koleksiyonları ' ndan seçim yapın. Bir uygulama için Kullanıcı veya cihaz koleksiyonları ' nı seçin. **İleri**’yi seçin.  

    > [!Important]  
    > Bir dağıtım potansiyel olarak yüksek riskli ise, aşamalı dağıtım oluşturma Sihirbazı sizi bilgilendirmez. Daha fazla bilgi için, bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) ve [bir görev dizisi dağıtırken](deploy-a-task-sequence.md)bu notun konusu.  

4. **Ayarlar** sayfasında, zamanlama ayarlarının her biri için bir seçenek belirleyin. Daha fazla bilgi için bkz. [aşama ayarları](#bkmk_settings). Tamamlandığında **İleri ' yi** seçin.  

5. **Aşamalar** sayfasında, belirlenen koleksiyonlar için sihirbazın oluşturduğu iki aşamaya bakın. **İleri**’yi seçin. Bu yönergeler otomatik olarak varsayılan iki aşamalı dağıtım oluşturma yordamını kapsar. Sihirbaz aşamalı dağıtım için aşamaları eklemenize, kaldırmanıza, yeniden sıralamanıza, düzenlemenize veya görüntülemenize olanak sağlar. Bu ek eylemler hakkında daha fazla bilgi için bkz. [el ile yapılandırılan aşamalarla aşamalı dağıtım oluşturma](#bkmk_manual).  

6. **Özet** sekmesinde seçimlerinizi onaylayın ve sonra Sihirbazı tamamladıktan sonra **İleri** ' yi seçin.  

> [!NOTE]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager üründe ve belgelerde eski adı görmeye devam edebilirsiniz.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a> El ile yapılandırılan aşamalarla aşamalı bir dağıtım oluşturma
<!--1358148--> 

Sürüm 1806 ' den başlayarak, bir görev dizisi için el ile yapılandırılan aşamalarla aşamalı bir dağıtım oluşturun. Aşamalı dağıtım oluşturma sihirbazının **aşamalar** sekmesinden 10 ' a kadar ek aşama ekleyin. 

> [!Note]  
> Şu anda bir uygulama için aşamaları el ile oluşturamazsınız. Sihirbaz, uygulama dağıtımları için otomatik olarak iki aşama oluşturur.


1. Bir görev dizisi ya da yazılım güncelleştirmeleri için aşamalı dağıtım oluşturma Sihirbazı 'nı başlatın.  

2. Aşamalı dağıtım oluşturma sihirbazının **genel** sayfasında, aşamalı dağıtıma bir **ad**, **Açıklama** (isteğe bağlı) verin ve **tüm aşamaları el ile yapılandır**' ı seçin.  

3. Aşamalı dağıtım oluşturma sihirbazının **aşamalar** sayfasında, aşağıdaki eylemler kullanılabilir:  

    - Dağıtım Aşamaları listesini **filtreleyin** . Order, Name veya Collection sütunlarının büyük/küçük harf duyarsız eşleşmesi için bir karakter dizesi girin. 

    - Yeni aşama **ekleyin** :  

        1. Aşama Ekleme sihirbazının **genel** sayfasında, aşama Için bir **ad** belirtin ve ardından hedef **aşama koleksiyonuna**gidin. Bu sayfadaki ek ayarlar, normalde bir görev dizisi veya yazılım güncelleştirmeleri dağıtmasıyla aynıdır.  

        2. Aşama Ekleme sihirbazının **aşama ayarları** sayfasında zamanlama ayarlarını yapılandırın ve tamamlandığında **İleri** ' yi seçin. Daha fazla bilgi için bkz. [Ayarlar](#bkmk_settings).   

            > [!Note]  
            > İlk aşamada aşama ayarlarını, **dağıtım başarı yüzdesini** veya **cihazların başarıyla dağıtıldığı** (sürüm 1902 veya üzeri) sayısını düzenleyemezsiniz. Bu ayar yalnızca önceki bir aşamasına sahip aşamalar için geçerlidir.  

        3. Aşama Ekleme sihirbazının **Kullanıcı deneyimi** ve **dağıtım noktaları** sayfalarındaki ayarlar, normalde bir görev dizisi veya yazılım güncelleştirmeleri dağıtmasıyla aynıdır.  

        4. **Özet** sayfasında ayarları gözden geçirin ve ardından aşama Ekleme Sihirbazı ' nı doldurun.  

    - **Düzenle**: Bu eylem, seçili aşamanın Özellikler penceresi açar ve bu da, aşama Ekleme sihirbazının sayfalarıyla aynı sekmeleri içerir.  

    - **Kaldır**: Bu eylem, seçili aşamayı siler.  

       > [!Warning]  
       > Hiçbir onay yoktur ve bu eylemi geri almanın bir yolu yoktur.  

    - **Yukarı taşı** veya **aşağı taşı**: sihirbaz, aşamaları nasıl ekleyebileceğiniz ile sıralar. En son eklenen aşama listede en sonda bulunur. Sıralamayı değiştirmek için bir aşama seçin ve ardından bu düğmeleri kullanarak aşamanın konumunu listede taşıyın.  

       > [!Important]  
       > Sırayı değiştirdikten sonra aşama ayarlarını gözden geçirin. Aşağıdaki ayarların bu aşamalı dağıtım için gereksinimlerinize uygun olmaya devam ettiğinden emin olun:  
       > 
       > - Önceki aşamanın başarısı için ölçütler  
       > - Önceki aşamanın başarılı olduktan sonra dağıtımın bu aşamasına başlama koşulları   

5. **İleri**’yi seçin. **Özet** sayfasında ayarları gözden geçirin ve ardından aşamalı dağıtım oluşturma Sihirbazı ' nı doldurun.  


Aşamalı dağıtım oluşturduktan sonra, değişiklikler yapmak için özelliklerini açın:  

- Varolan bir aşamalı dağıtıma ek aşamalar **ekleyin** .  

- Bir aşama etkin değilse, **düzenleyebilir**, **kaldırabilir**veya **taşıyabilirsiniz** . Etkin bir aşamanın önüne taşıyamazsınız.  

- Bir aşama etkin olduğunda, salt okunurdur. Düzenleyemez, kaldıramazsınız veya listede konumunu taşıyamazsınız. Tek seçenek, aşamanın özelliklerini **görüntüler** .  

- Uygulama aşamalı dağıtımı her zaman salt okunurdur.  



## <a name="next-steps"></a>Sonraki adımlar

Aşamalı dağıtımları yönetme ve izleme:
- [Uygulama](manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)
- [Yazılım güncelleştirmesi](manage-monitor-phased-deployments.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Görev dizisi](manage-monitor-phased-deployments.md)  

