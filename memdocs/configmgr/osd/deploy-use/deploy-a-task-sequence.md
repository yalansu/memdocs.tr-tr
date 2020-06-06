---
title: Görev dizisini dağıtma
titleSuffix: Configuration Manager
description: Bir koleksiyondaki bilgisayarlara bir görev dizisi dağıtmak için bu bilgileri kullanın.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c16e89cc75bff1ccecd03a98cd12782c419a40
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455214"
---
# <a name="deploy-a-task-sequence"></a>Görev dizisini dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir görev dizisi oluşturup, başvurulan içeriği dağıttıktan sonra bir cihaz koleksiyonuna dağıtın. Bu eylem görev dizisinin bir cihazda çalışmasına izin verir. Dağıtılan bir görev dizisi otomatik olarak veya cihazın bir kullanıcısı tarafından yüklendiğinde çalıştırılabilir.

> [!WARNING]  
> Yüksek riskli görev dizisi dağıtımlarının davranışını yönetebilirsiniz. Yüksek riskli dağıtım otomatik olarak yüklenen ve istenmeyen sonuçlara neden olabilecek bir dağıtımıdır. Örneğin, bir işletim sistemini dağıtan bir görev dizisi, yüksek **Required** riskli dağıtım olarak kabul edilir. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

## <a name="process"></a>İşleme

Görev sırasını koleksiyondaki bilgisayarlara dağıtmak için aşağıdaki prosedürü kullanın.  

> [!NOTE]  
> Görev sırası dağıtımı için durum iletileri, birincil sitenin ileti penceresinde görüntülenir, ancak bir merkezi yönetim sitesinde görüntülenmez.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

2. **Görev Sırası** listesinde, dağıtmak istediğiniz görev sırasını seçin.  

3. Şeridin **giriş** sekmesinde, **dağıtım** grubunda, **Dağıt**' ı seçin.  

    > [!NOTE]  
    > **Dağıtım** kullanılamıyorsa, görev dizisinin geçerli olmayan bir başvurusu vardır. Referansı düzeltin ve ardından görev sırasını yeniden dağıtmaya çalışın.  

4. **Genel** sayfasında, aşağıdaki bilgileri belirtin.  

    - **Görev sırası**: dağıtılacak görev sırasını belirtin. Varsayılan olarak, bu kutu seçili görev sırasını görüntüler.  

    - **Koleksiyon**: görev dizisini çalıştıracak bilgisayarları içeren koleksiyonu seçin.  

        Bir işletim sistemini, tüm veri merkezi sunucularınızın bir koleksiyonu gibi uygun olmayan koleksiyonlara yükleyen bir görev dizisi dağıtmayın. Seçili koleksiyonun yalnızca görev sırasını çalıştırmak istediğiniz bilgisayarları içerdiğinden emin olun.  

        Yüksek riskli dağıtımlar hakkında daha fazla bilgi için bkz. [yüksek riskli dağıtımlar](#bkmk_high-risk).

    - **Bu koleksiyonla ilişkili varsayılan dağıtım noktası gruplarını kullan**: görev sırası içeriğini koleksiyonun varsayılan dağıtım noktası grubunda depola. Seçili koleksiyonu bir dağıtım noktası grubuyla ilişkilendirmediyseniz, bu seçenek gri renkte olur.  

    - **Bağımlılıklar için Içeriği otomatik olarak dağıt**: başvurulan herhangi bir içeriğin bağımlılıkları varsa, site Ayrıca dağıtım noktalarına bağımlı içerik gönderir.  

    - **Bu görev dizisinin Içeriğini önceden indir**: daha fazla bilgi için bkz. [ön önbellek içeriğini yapılandırma](configure-precache-content.md).  

    - **Dağıtım şablonu seçin**: bir görev sırası için bir dağıtım şablonu kaydedin ve belirtin.<!--1357391-->  

        > [!IMPORTANT]  
        > Bazı öğeler şablona kaydedilmez.<!--510610--> Dağıtım Sihirbazı 'nı çalıştırdığınızda aşağıdaki öğeleri uyguladığınızdan emin olun:  
        >
        > - Yazılım yükleme
        > - Zamanlama
        > - İndirme öncesi içerik

    - **Yorumlar (isteğe bağlı)**: Görev dizisinin bu dağıtımını açıklayan ek bilgileri belirtin.  

5. **Dağıtım ayarları** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Amaç**: Açılan listede aşağıdaki seçeneklerden birini belirleyin:  

        - **Kullanılabilir**: Kullanıcı, görev dizisini yazılım merkezi 'nde görür ve isteğe bağlı olarak yükleyebilir.  

        - **Gerekli**: Configuration Manager, görev dizisini yapılandırılan zamanlamaya göre otomatik olarak çalıştırır. Görev sırası gizli değilse, Kullanıcı dağıtım durumunu yine de izleyebilir. Görev sırasını son tarihten önce yüklemek için yazılım merkezi 'ni de kullanabilirler.  

        > [!NOTE]
        > Cihazda birden çok kullanıcı oturum açmışsa, paket ve görev sırası dağıtımları yazılım merkezi 'nde görünmeyebilir.  

    - **Aşağıdakiler için kullanılabilir yap**: görev dizisinin aşağıdaki türlerden biri için kullanılabilir olup olmadığını belirtin:  

        - Yalnızca Configuration Manager istemcileri  
        - İstemcileri, medyayı ve PXE 'yi Configuration Manager  
        - Yalnızca medya ve PXE  
        - Yalnızca medya ve PXE (gizli)  

        > [!IMPORTANT]  
        > Otomatik görev sırası dağıtımları için **Yalnızca medya ve PXE (gizli)** ayarını kullanın. Bilgisayarın kullanıcı etkileşimi olmadan dağıtıma otomatik olarak önyüklemesini sağlamak için, **Katılımsız işletim sistemi dağıtımına Izin ver** ' i seçin ve **SMSTSPreferredAdvertID** değişkenini medyanın parçası olarak ayarlayın. Görev dizisi değişkenleri hakkında daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID).  

    - **Uyandırma paketleri gönder**: dağıtım **gerekliyse** ve bu seçeneği belirlerseniz, site istemci dağıtımı çalıştırmadan önce bilgisayarlara bir uyandırma paketi gönderir. Bu paket, yükleme son tarihinde bilgisayarı uykudan uyandırır. Bu seçeneği kullanmadan önce, bilgisayarlar ve ağların LAN'da Uyandırma için yapılandırılması gerekir. Daha fazla bilgi için bkz. [istemcileri uyandırmayı planlayın](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    - **Tarifeli bir Internet bağlantısı kullanan istemcilerin, yükleme son tarihinden sonra içerik Indirmelerine Izin ver, bu da ek maliyetlere neden olabilecek**: Bu seçenek yalnızca **gerekli** dağıtımlar için kullanılabilir. Bir uygulamayı yükleyen ancak işletim sistemi dağıtmayan özel bir görev diziniz varsa, Tarifeli İnternet bağlantıları kullandıklarında istemcilerin yükleme son tarihinden sonra içerik indirmelerine izin verip vermeyeceğinizi belirtebilirsiniz. İnternet sağlayıcıları bazen tarifeli bir İnternet bağlantısında olduğunuzda kullandığınız veri miktarına göre ücretlendirilir.  

        > [!NOTE]  
        > Bir işletim sistemi dağıtmayan görev dizileri için tarifeli bir internet bağlantısı kullanmak işe çalışmayabilir, bu desteklenmez.  

6. **Zamanlama** sayfasında, aşağıdaki bilgileri belirtin:  

    > [!IMPORTANT]  
    > Bir Windows PE istemcisi PXE veya önyükleme ortamından başlatıldığında, istemci dağıtım zamanlamalarını değerlendirmez. Bu zamanlamalar başlangıç, bitiş tarihi ve son tarih zamanlarını içerir. Yalnızca tam Windows IŞLETIM sisteminden başlayan istemcilere yapılan dağıtımlarda zamanlamalar yapılandırın. Windows PE'den başlatılan istemcilere dağıtılan etkin görev sıralarını denetlemek için bakım pencereleri gibi diğer yöntemleri kullanmayı düşünün.  

    - **Bu dağıtımın kullanılabilir olacağı zamanı ayarla**: Görev dizisinin hedef bilgisayarda çalıştırılmak için uygun olduğu tarihi ve saati belirtin. **UTC** seçeneğini belirlediğinizde, görev sırası birden çok bilgisayar için aynı anda kullanılabilir. Aksi takdirde dağıtım, her bilgisayardaki yerel saate göre farklı zamanlarda kullanılabilir.  

        Başlangıç saati, gereken süreden daha eski ise, istemci, görev sırası içeriğini başlangıç saatinde indirir.  

    - **Bu dağıtımın süre sonunu zamanla**: Görev dizisinin hedef bilgisayarda sona ereceği tarihi ve saati belirtin. **UTC** seçeneğini belirlediğinizde, görev sırası birden çok hedef bilgisayarda aynı anda sona erer. Aksi takdirde dağıtım, her bilgisayardaki yerel saate göre farklı zamanlarda zaman aşımına uğrar.  

    - **Atama zamanlaması**: **gerekli** bir dağıtım için, istemcinin görev sırasını ne zaman yürüttüğünde belirtin. Birden fazla zamanlama ekleyebilirsiniz. Atama zamanlaması aşağıdaki yapılandırmalardan birine sahip olabilir:  

        - Belirli bir tarih ve saat  
        - Aylık, haftalık veya özel yinelenme stili  
        - En Erken  
        - Oturum açma veya oturum kapatma olayları  

        > [!NOTE]  
        > Gerekli bir dağıtım için görev dizisinin kullanılabildiği tarih ve saatten erken bir başlangıç saati zamanladıysanız, Configuration Manager istemcisi içeriği atanan başlangıç saatinde indirir. Bu davranış, görev dizisini daha sonra kullanılabilir olacak şekilde zamanlasanız bile oluşur.<!--SCCMDocs issue 777-->  

    - **Yeniden çalıştırma davranışı**: görev dizisinin ne zaman yeniden yapacağını belirtin. Aşağıdaki seçeneklerden birini belirtin:  

        - **Dağıtılan programı hiç yeniden**çalıştırma: istemci daha önce görev sırasını çalıştırmışsa, yeniden çalıştırılmaz. Görev sırası, başlangıçta başarısız olsa veya görev sırası dosyaları değiştiyse bile yeniden çalıştırılmaz.  

        - **Programı her zaman yeniden çalıştır**: görev dizisi, dağıtım zamanlandığında istemcide her zaman yeniden çalıştırır. Görev sırası zaten başarıyla çalıştırılmış olsa bile tekrar çalışır. Bu ayar, görev dizisinin düzenli olarak güncelleştirildiği yinelenen dağıtımları kullandığınızda yararlıdır.  

            > [!IMPORTANT]  
            > Bu seçenek varsayılan olarak seçilidir. Ancak, gerekli bir dağıtımı atamaz kadar hiçbir etkisi yoktur. Bir Kullanıcı, kullanılabilir dağıtımları her zaman yeniden çalıştırabilir.  

        - **Önceki girişim başarısız olursa yeniden çalıştır**: görev dizisi, yalnızca daha önce çalışmamışsa, dağıtım zamanlandığında tekrar çalışır. Bu ayar, gerekli bir dağıtım için yararlıdır. Son çalıştırma denemesi başarısız olduysa, atama zamanlamaya göre otomatik olarak yeniden çalıştırmayı dener.  

        - **Önceki denemede başarılı olursa yeniden çalıştır**: görev dizisi, yalnızca daha önce istemcide başarıyla çalıştırıldıysa tekrar çalışır. Bu ayar, görev sırasının rutin olarak güncelleştirildiği ve her güncelleştirmenin bir önceki güncelleştirmenin başarıyla yüklenmesini gerektirdiği tekrarlayan dağıtımları kullandığınızda yararlıdır.  

        > [!NOTE]  
        > Kullanıcı, kullanılabilir bir görev sırası dağıtımını yeniden çalıştırabilir. Bir üretim ortamında kullanılabilir bir görev sırasını dağıtmadan önce, Kullanıcı görev sırasını birden çok kez yeniden çalıştırabildiğinde ne olacağını test edin.  

7. **Kullanıcı Deneyimi** sayfasında aşağıdaki bilgileri belirtin:  

    - **Kullanıcının programı atamalardan bağımsız olarak çalıştırmasına Izin ver**: kullanıcının gerekli bir dağıtımı atama zamanlaması dışında çalıştırıp çalıştıramayacağını belirtin. Bu seçenek kullanılabilir dağıtımlar için her zaman etkindir.  

    - **Görev sırası Ilerlemesini göster**: Configuration Manager istemcisinin görev dizisinin ilerlemesini görüntüleyip görüntülemediğini belirtin.  

    - **Yazılım yükleme**: kullanıcının zamanlanan saatten sonra yapılandırılan bakım penceresi dışında yazılım yüklemesine izin verilip verilmeyeceğini belirtin.  

    - **Sistem yeniden başlatma (yüklemeyi tamamlamak için gerekliyse)**: Kullanıcının, atama zamanından sonra yapılandırılmış bakış penceresi dışında yazılım yüklemesinin ardından bilgisayarı yeniden başlatmasına izin verilip verilmeyeceğini belirtin.  

    - **Windows Embedded cihazlar için filtre Işleme yaz**: Bu ayar, yazma filtresiyle etkinleştirilen Windows Embedded cihazlarındaki yükleme davranışını denetler. Yükleme son tarihinde veya bakım penceresi sırasında değişiklikleri Yürüt seçeneğini belirleyin. Bu seçeneği belirlediğinizde, yeniden başlatma gerekir ve değişiklikler cihazda kalır. Aksi takdirde, uygulama geçici bir katmana yüklenir ve daha sonra kaydedilir. Windows Embedded cihazına bir görev sırası dağıttığınızda, cihazın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun.  

    - **Görev dizisinin Internet 'te istemci için çalışmasına Izin ver**: görev dizisinin İnternet tabanlı bir istemcide çalışmasına izin verilip verilmeyeceğini belirtin. Bir işletim sistemi yüklemesi gibi Önyükleme medyası gerektiren işlemler bu ayarla desteklenmez. Bu seçeneği yalnızca standart IŞLETIM sisteminde işlemleri çalıştıran genel yazılım yüklemeleri veya komut dosyası tabanlı görev sıraları için kullanın.  

        - Bu ayar, bulut yönetimi ağ geçidi aracılığıyla Internet tabanlı istemcilere Windows 10 yerinde yükseltme görev dizisinin dağıtımları için desteklenir. Daha fazla bilgi için bkz. [CMG aracılığıyla Windows 10 yerinde yükseltme dağıtımı](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. **Uyarılar** sayfasında, bu görev sırası dağıtımı için istediğiniz uyarı ayarlarını belirtin.  

9. **Dağıtım Noktaları** sayfasında aşağıdaki bilgileri belirtin:  

    - **Dağıtım seçenekleri**: daha fazla bilgi için bkz. [dağıtım seçenekleri](#bkmk_deploy-options).

    - **Kullanılabilir yerel dağıtım noktası olmadığında uzak bir dağıtım noktası kullan**: istemcilerin, görev dizisinin gerektirdiği içeriği indirmek için bir komşu sınır grubundan dağıtım noktalarını kullanıp kullanamayacağını belirtin.  

    - **İstemcilerin varsayılan site sınırı grubundan dağıtım noktalarını kullanmasına Izin ver**: istemcilerin, geçerli veya komşu sınır gruplarındaki bir dağıtım noktasından kullanılabilir olmadığında, sitenin varsayılan sınır grubundaki bir dağıtım noktasından içerik indirip indirmemelidir.  

        > [!Note]  
        > Sürüm 1810 ' den başlayarak, bir cihaz bir görev dizisi çalıştırdığında ve içerik almaları gerektiğinde, Configuration Manager istemcisine benzer sınır grubu davranışları kullanır. Daha fazla bilgi için bkz. [sınır grupları Için görev sırası desteği](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).<!--1359025-->  

10. Bu ayarları yeniden kullanmak üzere kaydetmek için **Özet** sekmesinde **şablon olarak kaydet**' i seçin. Şablon için bir ad sağlayın ve kaydedilecek ayarları seçin.  

11. Sihirbazı tamamlayın.  

### <a name="deployment-options"></a><a name="bkmk_deploy-options"></a>Dağıtım seçenekleri

<!-- MEMDocs#328, SCCMDocs#2114 -->

Bu seçenekler, görev sırası dağıtımının **dağıtım noktaları** sekmesindedir. Bunlar, görev dizisinin dağıtım ve özniteliklerinde diğer seçimlere göre dinamik olarak belirlenir. Her zaman tüm seçenekleri görmeyebilirsiniz.

> [!NOTE]  
> Bir işletim sistemini dağıtmak için çok noktaya yayın kullandığınızda, içeriği gerektiğinde veya görev sırası çalıştırılmadan önce bilgisayarlara indirin.  

- **Çalışan görev dizisi için gerektiğinde içeriği yerel olarak indir**: istemcilerin, görev dizisinin gerektirdiği içeriği dağıtım noktasından indirmesini belirtin. İstemci görev dizisini başlatır. Görev dizisindeki bir adım içerik gerektirdiğinde, adım çalışmadan önce indirilir.  

- **Görev sırasını başlatmadan önce tüm içeriği yerel olarak indir**: istemcilerin, görev sırası çalıştırılmadan önce dağıtım noktasından tüm içeriği indirmelerini belirtin. Görev sırasını, **dağıtım ayarları** sayfasında PXE ve önyükleme medya dağıtımları için kullanılabilir hale getirmek için bu seçenek gösterilmez.  

- **Çalışan görev sırası için ihtiyaç duyduğunda, içeriğe doğrudan bir dağıtım noktasından erişin**: istemcilerin içeriği dağıtım noktasından çalıştırmasını belirtin. Bu seçenek yalnızca, görev dizisiyle ilişkili tüm paketleri dağıtım noktasında bir paket paylaşımının kullanması için etkinleştirdiğinizde kullanılabilir. İçeriği paket paylaşımı kullanmak üzere etkinleştirmek için, her paket için **Özellikler** 'deki **Veri Erişimi** sekmesine bakın.  

> [!IMPORTANT]  
> En yüksek güvenlik için, **çalışan görev dizisi için gerektiğinde içeriği yerel olarak indirme** seçeneklerini belirleyin veya **görev dizisini başlatmadan önce tüm Içeriği yerel olarak indirin**. Bu seçeneklerden birini belirlediğinizde, paket bütünlüğünü sağlamak için paketi karma Configuration Manager. **Çalışan görev sırası için gerektiğinde bir dağıtım noktasından içeriğe doğrudan erişme**seçeneğini belirlediğinizde, Configuration Manager belirtilen programı çalıştırmadan önce paket karmasını doğrulamaz. Site paket bütünlüğünü sağladığından, yönetici haklarına sahip kullanıcıların paket içeriğiyle değişiklik yapmak veya onu değiştirmesine olanak sağlamak mümkündür.  

#### <a name="example-1-one-deployment-option"></a>Örnek 1: bir dağıtım seçeneği

Diski temizler ve bir görüntü uyguladığı bir işletim sistemi dağıtımı görev dizisi dağıtırsınız. **Dağıtım ayarları** sayfasında, medyayı medya ve PXE içeren bir seçenek için kullanılabilir hale getirebilirsiniz:

:::image type="content" source="media/deploy-setting-make-available.png" alt-text="Görev sırasını dağıt, aşağıdakiler için kullanılabilir yap":::

**Dağıtım noktaları** sayfasında, yalnızca bir dağıtım seçeneği vardır:

- **Çalışan görev dizisi için gerektiğinde içeriği yerel olarak indir**

:::image type="content" source="media/deploy-option-1.png" alt-text="Görev sırasını dağıt, bir dağıtım seçeneği":::

Dağıtım medya ve PXE için kullanılabilir hale getirilmediğinden, **görev sırasını başlatmadan önce tüm içeriği yerel olarak indirme** seçeneği kullanılamaz.

**Çalışan görev dizisinin gerek duyduğu bir dağıtım noktasından içeriğe doğrudan erişme** seçeneği kullanılamaz. Başvurulan içeriğin hepsi bir paket paylaşma kullanmaz.

#### <a name="example-2-two-deployment-options"></a>Örnek 2: Iki dağıtım seçeneği

Diski temizler ve bir görüntü uyguladığı bir işletim sistemi dağıtımı görev dizisi dağıtırsınız. **Dağıtım ayarları** sayfasında, onu **yalnızca Configuration Manager istemcileri**için kullanılabilir hale getirebilirsiniz. **Dağıtım noktaları** sayfasında, kullanılabilecek iki dağıtım seçeneği vardır:

- **Çalışan görev dizisi için gerektiğinde içeriği yerel olarak indir**
- **Görev sırasını başlatmadan önce tüm içeriği yerel olarak indir**

:::image type="content" source="media/deploy-option-2.png" alt-text="Dağıtım görev sırası, iki dağıtım seçeneği":::

**Çalışan görev dizisinin gerek duyduğu bir dağıtım noktasından içeriğe doğrudan erişme** seçeneği kullanılamaz. Başvurulan içeriğin hepsi bir paket paylaşma kullanmaz.

#### <a name="example-3-three-deployment-options"></a>Örnek 3: üç dağıtım seçeneği

Yönetici betiklerine ve ilişkili içeriğe sahip birkaç paketleriniz vardır. Paket özelliklerinin **veri erişimi** sekmesinde, tüm bunları, **Bu paketteki içeriği dağıtım noktalarındaki bir paket paylaşımında kopyalayacak**şekilde yapılandırırsınız.

Bu betik paketleri için yalnızca birkaç **paket paketi** içeren bir görev dizisi oluşturur ve dağıtın. **Dağıtım ayarları** sayfasında, tek seçenek **yalnızca Configuration Manager istemcileri**için kullanılabilir hale getirmek içindir. Bu seçenek kullanılabilir tek seçenektir. Görev sırası, kendisiyle ilişkili bir önyükleme görüntüsü olmadığından, işletim sistemi dağıtımı için değil. **Dağıtım noktaları** sayfasında, üç dağıtım seçeneği mevcuttur:

- **Çalışan görev dizisi için gerektiğinde içeriği yerel olarak indir**
- **Görev sırasını başlatmadan önce tüm içeriği yerel olarak indir**
- **Çalışan görev sırası için gerektiğinde doğrudan bir dağıtım noktasından içeriğe erişin**

:::image type="content" source="media/deploy-option-3.png" alt-text="Görev sırasını dağıt, üç dağıtım seçeneği":::

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>CMG aracılığıyla Windows 10 yerinde yükseltme dağıtımı

<!-- 1357149 -->
Windows 10 yerinde yükseltme görev sırası, [bulut yönetimi ağ geçidi](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) üzerinden yönetilen internet tabanlı istemcilere dağıtımı destekler. Bu özellik, uzak kullanıcıların intranete bağlanmasına gerek kalmadan Windows 10 ' a daha kolay yükseltmesine olanak sağlar.

Yerinde yükseltme görev sırası tarafından başvurulan tüm içeriklerin içerik özellikli bir CMG 'ye dağıtıldığından emin olun. ( [CMG ayarını](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings)etkinleştirin: **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verin ve Azure depolama 'dan içerik sunabilir**.) [Bulut dağıtım noktası](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)da kullanabilirsiniz. Aksi halde cihazlar görev sırasını çalıştıramıyor.

Bir yükseltme görev dizisi dağıttığınızda, aşağıdaki ayarları kullanın:

- Dağıtımın Kullanıcı deneyimi sekmesinde **Internet 'te istemci için görev dizisinin çalışmasına Izin verin**.  

- Dağıtımın dağıtım noktaları sekmesinde aşağıdaki seçeneklerden birini belirleyin:

  - **Çalışan görev dizisi için gerektiğinde içeriği yerel olarak indirin**. Sürüm 1910 ' den başlayarak, görev dizisi altyapısı, içerik etkinleştirilmiş bir CMG veya bulut dağıtım noktasından isteğe bağlı paket indirebilir. Bu değişiklik, Internet tabanlı cihazlara Windows 10 yerinde yükseltme dağıtımlarınızla ek esneklik sağlar.<!--3601238-->

  - **Görev sırasını başlatmadan önce tüm içeriği yerel olarak indirin**. Configuration Manager sürüm 1906 ve önceki sürümlerde, **çalışan görev sırası için gerektiğinde içeriği yerel olarak indir** gibi diğer seçenekler bu senaryoda çalışmaz. Görev sırası altyapısı, bir bulut kaynağından içerik indiremez. Configuration Manager istemci, görev dizisini başlatmadan önce bulut kaynağındaki içeriği indirmelidir. Gereksinimlerinizi karşılamak için gerekliyse, sürüm 1910 ' de bu seçeneği kullanmaya devam edebilirsiniz.

- (*Isteğe bağlı*) Dağıtımın Genel sekmesinde **Bu görev dizisinin Içeriğini önceden indirin**. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](configure-precache-content.md).  

> [!NOTE]
> Görev dizisini yazılım merkezinden başlatın. Bu senaryo, Windows PE, PXE veya görev sırası medyasını desteklemez.

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a>Yüksek riskli dağıtımlar

Bir işletim sistemi gibi yüksek riskli bir dağıtım dağıttığınızda, **Koleksiyon Seç** penceresinde yalnızca sitenin özelliklerinde yapılandırılmış dağıtım doğrulama ayarlarını karşılayan özel koleksiyonlar görüntülenir. Yüksek riskli dağıtımlar her zaman özel koleksiyonlar, oluşturduğunuz koleksiyonlar ve yerleşik **Bilinmeyen Bilgisayarlar** koleksiyonu ile sınırlıdır. Yüksek riskli dağıtım oluşturduğunuzda, **Tüm sistemler**gibi yerleşik bir koleksiyon seçemezsiniz. Yapılandırılan en büyük boyuttan daha az istemci içeren tüm özel koleksiyonları görmek için, **üye sayısı sitenin en düşük boyut yapılandırmasından daha büyük olan koleksiyonları gizleme**seçeneğini devre dışı bırakın. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Dağıtım doğrulama ayarları, koleksiyonu geçerli üyeliğine bağlıdır. Görev dizisini dağıttıktan sonra, Configuration Manager yüksek riskli dağıtım ayarları için koleksiyon üyeliğini yeniden değerlendirmez.  

Örneğin, **varsayılan boyutu** 100 olarak, **en büyük boyutu** 1000 olarak ayarlayadığınızı varsayalım. Yüksek riskli bir dağıtım oluşturduğunuzda **Koleksiyon Seç** penceresinde yalnızca 100 ' den az istemci içeren koleksiyonlar görüntülenir. **Üye sayısı sitenin en düşük boyut yapılandırmasından daha büyük olan koleksiyonları Gizle** ayarını temizlerseniz, pencerede 1000 ' den az istemci içeren koleksiyonlar görüntülenir.  

Site rolü içeren bir koleksiyon seçtiğinizde, aşağıdaki davranış geçerlidir:  

- Koleksiyon bir site sistem sunucusu içeriyorsa ve dağıtım doğrulama ayarlarını site sistem sunucularıyla koleksiyonları engelleyecek şekilde yapılandırdıysanız bir hata oluşur. Dağıtımı oluşturmaya devam edilemiyor.  

- Aşağıdaki ölçütlerden biri geçerliyse, Yazılım Dağıtma Sihirbazı yüksek riskli bir uyarı görüntüler. Devam etmek için, yüksek riskli bir dağıtım oluşturmayı kabul etmeniz gerekir. Site bir denetim durumu iletisi oluşturur.  

  - Koleksiyon bir site sistem sunucusu içeriyorsa ve dağıtım doğrulama ayarlarını, site sistem sunucularıyla koleksiyonlar üzerinde uyarı verecek şekilde yapılandırdıysanız  

  - Koleksiyon varsayılan boyut değerini aşarsa

  - Koleksiyon bir sunucu içeriyorsa  

## <a name="see-also"></a>Ayrıca bkz.

[Görevleri otomatikleştirmek için görev dizilerini yönetme](manage-task-sequences-to-automate-tasks.md)
