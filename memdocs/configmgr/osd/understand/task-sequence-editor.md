---
title: Görev dizisi düzenleyicisini kullanma
titleSuffix: Configuration Manager
description: Configuration Manager konsolunda görev sırası düzenleyicisinin nasıl kullanılacağını anlayın
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a4aaaab8eb9195f4f5dce4deb890540b0837852
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697472"
---
# <a name="use-the-task-sequence-editor"></a>Görev dizisi düzenleyicisini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Görev **dizisi düzenleyicisini**kullanarak Configuration Manager konsolundaki görev dizilerini düzenleyin. Düzenleyiciyi kullanarak şunları yapın:  

- Görev dizisinin salt okunurdur görünümünü açma

- Görev dizisinde adım ekleme veya kaldırma  

- Görev dizisinin adımlarının sırasını değiştirme  

- Adım grupları ekleme veya kaldırma  

- Görev dizileri arasında kopyalama ve yapıştırma adımları

- Bir hata oluştuğunda görev dizisinin devam edip etmediğini gibi adım seçeneklerini ayarlayın  

- Bir görev dizisinin adımları ve gruplarına koşullar ekleme  

- Bir görev dizisindeki adımlar arasında kopyalama ve yapıştırma koşulları

- Adımları hızlı bir şekilde bulmak için görev dizisini arayın

Bir görev dizisini düzenleyebilmeniz için önce oluşturmanız gerekir. Daha fazla bilgi için bkz. [görev dizilerini yönetme ve oluşturma](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>Görev sırası Düzenleyicisi hakkında

Görev sırası Düzenleyicisi aşağıdaki bileşenleri içerir:

![Örnek görev sırası Düzenleyicisi penceresinin açıklamalı ekran görüntüsü](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Görev dizisinin adı
2. Aramanız. Daha fazla bilgi için bkz. [arama](#bkmk_search).
3. Dizideki seçili grubun veya adımın **özellikleri**

    Belirli bir adımın özellikleri ve seçenekleri hakkında daha fazla bilgi için bkz. [görev dizisi adımları hakkında](task-sequence-steps.md).

4. Dizideki seçili grup veya adım için **Seçenekler**

    Tüm adımlarla ilgili genel seçenekler veya belirli bir adımın seçenekleri hakkında daha fazla bilgi için bkz. [görev dizisi adımları hakkında](task-sequence-steps.md).

    Koşulların nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [koşullar](#bkmk_conditions).

5. Grup veya adımlar **ekleyin**
6. Grup veya adımları **kaldırma**
7. Tüm grupları Daralt veya tüm grupları Genişlet
8. Bir grubun veya adımın konumunu sırada taşı (yukarı taşı, aşağı taşı)
9. Görev sırası:
    - Adım ve grupların sırasını görün.
    - Bir grubu genişletin veya daraltın.
    - **Seçeneklerinde**bir adımı veya grubu devre dışı bıraktığınızda, bu, dizide gri renkte görünür.
    - Adımla ilgili bir sorun varsa, adımın simgesi kırmızı bir hata olarak değişir. Örneğin, gerekli bir değer eksik.
10. **Tamam**: Kaydet ve Kapat
11. **İptal**: değişiklikleri kaydetmeden kapat
12. **Uygula**: Değişiklikleri Kaydet ve açık tut

Standart Windows denetimlerini kullanarak görev dizisi düzenleyicisini yeniden boyutlandırabilirsiniz. İki ana bölme genişliğini yeniden boyutlandırmak için, fareyi kullanarak görev dizisi ve adım özellikleri arasındaki çubuğu seçin ve sonra sola veya sağa sürükleyin.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a> Görev sırasını görüntüleme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

2. **Görev sırası** listesinde, görüntülemek istediğiniz görev sırasını seçin.  

3. Şeridin **giriş** sekmesinde, **görev dizisi** grubunda, **Görünüm**' ü seçin.

    > [!TIP]
    > Bu eylem varsayılandır. Bir görev dizisini çift tıklattığınızda, görev dizisini **görüntüleyebilirsiniz** .

Bu eylem, görev sırası düzenleyicisini salt okuma modunda açar. Bu modda aşağıdaki işlemleri yapabilirsiniz:

- Tüm grupları, adımları, özellikleri ve seçenekleri görüntüleyin
- Grupları Genişlet ve Daralt
- Görev dizisinde ara
- Düzenleyici penceresini yeniden boyutlandır

Bu salt okunurdur modunda, bir adım veya koşulu kopyalama dahil olmak üzere herhangi bir değişiklik yapamazsınız. Bu eylem aynı zamanda görev dizisini düzenlenmek üzere kilitlemez. Bu kilitler hakkında daha fazla bilgi için bkz. [görev dizilerini görüntülemek Için geri kazanma kilidi](#bkmk_sedo).

Bir görev dizisinde değişiklik yapmak için, salt okuma modunda açtığınız görev sırası düzenleyicisini kapatın. Ardından görev dizisini [düzenleyin](#bkmk_edit) .

> [!NOTE]  
> Görev sırası oluşturma Sihirbazı tarafından oluşturulan bir görev sırasını görüntülerken veya düzenlerken, adımın adı eylem veya adımın türü olabilir. Örneğin, "Bölüm diski 0" adlı bir adım görebilirsiniz. Bu, [Biçim ve Bölüm diski](task-sequence-steps.md#BKMK_FormatandPartitionDisk)türünde bir adımın eylemi. Tüm görev dizisi adımları, düzenleyicinin görüntülediği adımın adı değil, *türlerine*göre belgelenmiştir.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Bir görev dizisini düzenleme

Mevcut bir görev sırasını değiştirmek için aşağıdaki yordamı kullanın:  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

2. **Görev Sırası** listesinde düzenlemek istediğiniz görev sırasını seçin.  

3. Şeridin **giriş** sekmesinde, **görev dizisi** grubunda **Düzenle**' yi seçin. Ardından aşağıdaki eylemlerden herhangi birini yapın:  

    - **Adım ekleyin**: **Ekle**' yi seçin, bir kategori seçin ve ardından eklenecek adımı seçin. Örneğin, [komut satırını Çalıştır](task-sequence-steps.md#BKMK_RunCommandLine) adımını eklemek Için: **Ekle**' yi seçin, **genel** kategorisini seçin ve ardından **komut satırını Çalıştır**' ı seçin. Bu eylem, şu anda seçili olan adımdan sonraki adımı ekler.

    - **Grup Ekle**: **Ekle**' yi seçin ve ardından **Yeni Grup**' u seçin. Bir grup ekledikten sonra bu gruba adım ekleyin.  

    - **Sırayı değiştirme**: yeniden sıralamak istediğiniz adımı veya grubu seçin. Ardından **Yukarı taşı** veya **aşağı taşı** simgelerini kullanın. Aynı anda yalnızca bir adım veya grup taşıyabilirsiniz. Bu eylemler bir grup veya adıma sağ tıkladığınızda da kullanılabilir.

        Bir grubu veya adımı kesebilir, kopyalayabilir ve yapıştırabilirsiniz. Öğeye sağ tıklayın ve eylemi seçin. Her eylem için standart klavye kısayollarını da kullanabilirsiniz:

        - Kes: **CTRL**  +  **X**
        - Kopyala: **CTRL**  +  **C**
        - Yapıştır: **CTRL**  +  **V**

    - **Bir adımı veya grubu kaldırın**: adımı veya grubu seçin ve **Kaldır**' ı seçin.  

4. Değişikliklerinizi kaydetmek ve pencereyi kapatmak için **Tamam** ' ı seçin. Değişikliklerinizi atıp pencereyi kapatmak için **iptal** ' i seçin. Değişikliklerinizi kaydetmek için **Uygula** ' yı seçin ve görev sırası düzenleyicisini açık tutun.  

Kullanılabilir görev dizisi adımlarının bir listesi için bkz. [görev dizisi adımları](task-sequence-steps.md).  

> [!IMPORTANT]  
> Görev dizisinin, düzenleme sonucu olarak bir nesneye ilişkilendirilmemiş başvuruları varsa, düzenleyici, kapatmadan önce başvuruyu çözmenizi gerektirir. Olası eylemler şunlardır:  
>
> - Başvuruyu düzeltin
> - Başvurulmayan nesneyi görev dizisinden Sil  
> - Bozuk başvuru düzeltilene veya kaldırılana kadar, başarısız görev dizisi adımını geçici olarak devre dışı bırakın  

Görev sırası düzenleyicisinin birden fazla örneğini aynı anda açabilirsiniz. Bu davranış, birden çok görev dizisini karşılaştırmanıza veya aralarındaki adımları kopyalayıp yapıştırmanıza olanak tanır. Bir görev dizisini **düzenleyebilir** ve diğeri **görüntüleyebilirsiniz** , ancak aynı görev dizisinde her iki eylemi de yapamazsınız.

## <a name="conditions"></a><a name="bkmk_conditions"></a> Durumunda

Görev dizisinin nasıl davranacağını denetlemek için koşulları kullanın. Tek bir adıma veya bir adım grubuna koşul ekleyin. Görev dizisi, cihazda adımı çalıştırmadan önce koşulları değerlendirir. Yalnızca koşulların doğru değerlendirmesi durumunda bu adımı çalıştırır. Bir koşul yanlış değerlendirilirse, görev dizisi grubu veya adımı atlar.

Koşulları yönetmek için **Seçenekler** sekmesini kullanın:

![Görev sırası Düzenleyicisi 'nin Seçenekler sekmesinde koşulları yönetme](media/4621098-copy-paste-ts-condition.png)

Aşağıdaki koşul türleri kullanılabilir:

- **IF deyimleri**: koşulları gruplamak için bir *IF* ifadesini kullanın. **Tüm koşulları**, **herhangi bir koşulu**veya **hiçbirini**değerlendirebilirsiniz.

- **Görev dizisi değişkeni**. Görev dizisi ortamında herhangi bir yerleşik, eylem, özel veya salt okuma [görev dizisi değişkeninin](task-sequence-variables.md) geçerli değerini değerlendirin. Daha fazla bilgi için bkz. [adım koşulları](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > Bu koşulda bir dizi değişkeni kullanabilirsiniz, ancak belirli dizi üyesini belirtmeniz gerekir. Örneğin, `OSDAdapter0EnableDHCP` *ilk* ağ bağdaştırıcısının DHCP 'yi etkinleştirip etkinleştirmediğini belirtir. Daha fazla bilgi için bkz. [dizi değişkenleri](using-task-sequence-variables.md#bkmk_array).

- **Işletim sistemi sürümü**: görev dizisinin çalıştığı cihazın işletim sistemi sürümünü değerlendirin. Bu liste, Configuration Manager tamamında kullanılan genel işletim sistemi sürümleridir. Windows 10 ' un belirli bir sürümü gibi daha ayrıntılı bir işletim sistemi sürümünü değerlendirmek için **WMI 'Yı sorgula** koşulunu kullanın.

- **Işletim sistemi dili**: görev dizisinin çalıştığı cihazın işletim sistemi dilini değerlendirin. Bu liste Windows 'un desteklediği 257 dili içerir.

- **Dosya özellikleri**: cihazda görev dizisinin çalıştırıldığı herhangi bir dosyanın sürümünü veya zaman damgasını değerlendirin.

- **Klasör özellikleri**: cihazda görev dizisinin çalıştırıldığı herhangi bir klasörün zaman damgasını değerlendirin.

- **Kayıt defteri ayarı**: görev dizisinin çalıştığı cihazın kayıt defteri anahtarı değerini değerlendirin.

- **WMI sorgula**: görev dizisinin çalıştığı cihazda değerlendirilecek ad alanını ve sorguyu belirtin.

- **Yüklü yazılım**: görev dizisinin çalıştığı cihazda eşleştirilecek ürün bilgilerini yüklemek için bir Windows Installer dosyası belirtin. Belirli bir ürüne veya ürünün herhangi bir sürümüne göre eşleme yapabilirsiniz.

### <a name="cmdlets-for-conditions"></a>Koşullar için cmdlet 'ler

Koşulları aşağıdaki PowerShell cmdlet 'leriyle yönetin:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-Cmtsstepconditionifdeyimin](/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Koşulları Kopyala ve Yapıştır

<!-- 4621098 -->

Koşulları bir adımdan diğerine yeniden kullanmak için sürüm 1910 ' den başlayarak artık görev sırası düzenleyicisinde koşulları kopyalayabilir ve yapıştırabilirsiniz. Kesmek veya kopyalamak için bir koşul seçin. Bir koşulun alt öğesi varsa, tüm bloğu kopyalar. Panoda bir koşul varsa, aşağıdaki seçeneklerle yapıştırabilirsiniz:

- Önce Yapıştır
- Sonra Yapıştır
- Buraya Yapıştır (yalnızca iç içe geçmiş koşullar için geçerlidir)

Kopyalamak için standart klavye kısayollarını kullanın (**CTRL**  +  **C**) ve Kes (**CTRL**  +  **X**). Standart **CTRL**  +  **V** klavye kısayolu, **sonra Yapıştır eyleminden sonra** yapılır.

Ayrıca, koşulları listede yukarı veya aşağı taşımaya yönelik yeni seçenekler de vardır.

> [!Note]  
> Bir görev dizisindeki adımlar arasında koşullar kopyalayabilir ve yapıştırabilirsiniz. Bu eylem, farklı görev dizileri arasında desteklenmez.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> Düzenlenmek üzere geri kazanmak için kilitle

<!--3699337-->
Configuration Manager konsolu yanıt vermeyi durdurursa, kilit 30 dakika sonra sona erene kadar daha fazla değişiklik yapmaktan ayrılabilir. Bu kilit Configuration Manager SEDO (dağıtılmış nesnelerin serileştirilmiş düzenlemesi) sisteminin bir parçasıdır. Daha fazla bilgi için bkz. [Configuration Manager SEDO](../../develop/core/understand/sedo.md).

Sürüm 1906 ' den başlayarak, bir görev dizisi üzerinde kilidi temizleyebilirsiniz. Bu eylem yalnızca kilidi olan Kullanıcı hesabınız için ve sitenin kilidi tarafından verilen aynı cihazda geçerlidir. Kilitli bir görev dizisine erişmeye çalıştığınızda artık **değişiklikleri atabilir**ve nesneyi düzenlemeyle devam edebilirsiniz. Kilidin süre dolduğunda bu değişiklikler kaybedilir.

> [!TIP]
> Sürüm 1910 ' den başlayarak, Configuration Manager konsolundaki herhangi bir nesne üzerindeki kilidi temizleyebilirsiniz. Daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> Aramanız

<!-- 4621085 -->

Birçok grup ve adım içeren büyük bir görev diziniz varsa, belirli adımları bulmak zor olabilir. Sürüm 1910 ' den başlayarak artık görev sırası düzenleyicisinde arama yapabilirsiniz. Bu eylem görev dizisindeki adımları daha hızlı bulmanızı sağlar.

![Görev sırası düzenleyicisinde arama](media/4621085-task-sequence-search.png)

Başlamak için bir arama terimi girin. Aşağıdaki türleri kullanarak aramanızın kapsamını belirleyebilirsiniz:

- Adım adı
- Adım açıklaması
- Adım türü
- Grup adı
- Grup açıklaması
- Değişken adı
- Koşullar
- Diğer içerik (örneğin, değişken değerleri veya komut satırları gibi dizeler)

Tüm kapsamları varsayılan olarak sunar.

Ayrıca, aşağıdaki özniteliklerle tüm adımlara filtre uygulayabilirsiniz:

- Hatada devam et
- Koşulları vardır

Varsayılan olarak filtre yapmaz.

Arama yaptığınızda, düzenleyici penceresi, arama ölçütlerinizle eşleşen adımları sarı renkle vurgular.

Bu arama alanlarına hızlıca erişin ve aşağıdaki klavye kısayollarıyla arama sonuçlarına gidin:

- **CTRL**  +  **F**: bir arama dizesi girin
- **CTRL**  +  **O**: sonuçların kapsamını belirlemek için arama seçeneklerini belirleyin
- **F3** veya **ENTER**: sonuçlar boyunca ilerme
- **SHIFT**  +  **F3**: sonuçlarda geriye doğru adımla

## <a name="see-also"></a>Ayrıca bkz.

- [Görev dizilerini yönetme ve oluşturma](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Görev dizisi adımları hakkında](task-sequence-steps.md)

- [Görev dizisi değişkenlerini kullanma](using-task-sequence-variables.md)

- [Configuration Manager konsolunu kullanma](../../core/servers/manage/admin-console.md)