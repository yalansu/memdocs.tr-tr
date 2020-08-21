---
title: Betik oluşturma ve çalıştırma
titleSuffix: Configuration Manager
description: İstemci cihazlarda PowerShell betikleri oluşturun ve çalıştırın.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db3a673d99efc40bd6fa0da7930c66c648136e03
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695382"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Configuration Manager konsolundan PowerShell betikleri oluşturun ve çalıştırın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1236459-->
Configuration Manager, PowerShell betikleri çalıştırmak için tümleşik bir becerisine sahiptir. PowerShell, daha büyük bir topluluk ile anlamış ve paylaşılan, gelişmiş ve otomatikleştirilmiş betikler oluşturma avantajına sahiptir. Betikler, yazılımı yönetmek için özel araçlar oluşturmayı basitleştirir ve sıradan görevlerini hızlıca gerçekleştirmenize olanak tanıyarak büyük işleri daha kolay ve tutarlı bir şekilde almanızı sağlar.  

> [!Note]  
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Configuration Manager ' de bu tümleştirmeyle, *komut dosyalarını çalıştır* işlevini kullanarak aşağıdaki işlemleri yapabilirsiniz:

- Configuration Manager ile kullanmak için betikleri oluşturun ve düzenleyin.
- Roller ve güvenlik kapsamları aracılığıyla betik kullanımını yönetin. 
- Komut dosyalarını koleksiyonlarda veya şirket içi yönetilen Windows bilgisayarlarda çalıştırın.
- İstemci aygıtlarından hızlı toplu betik sonuçları alın.
- Betik yürütmeyi izleyin ve betik çıktısından bildirim sonuçlarını görüntüleyin.

> [!WARNING]
> - Betiklerin gücü verildiğinde, kasıtlı olarak ve kullanımlarıyla ilgili bir sorun olduğunu hatırladık. Size yardımcı olmaya yönelik ek korumalar sunuyoruz; ayrılmış roller ve kapsamlar. Betikleri çalıştırmadan önce betiklerin doğruluğunu doğruladığınızdan emin olun ve istenmeyen betik yürütmeyi engellemek için güvenilir bir kaynaktan olduklarını doğrulayın. Genişletilmiş karakterler veya başka bir gizleme olun ve betikleri güvenli hale getirme hakkında kendinizi eğitin. [PowerShell betiği güvenliği hakkında daha fazla bilgi edinin](learn-script-security.md)
> - Bazı kötü amaçlı yazılımdan koruma yazılımları yanlışlıkla Configuration Manager çalıştırmak betiklerine veya CMPivot özelliklerine karşı olayları tetikleyemeyebilir. Kötü amaçlı yazılımdan koruma yazılımının bu özelliklerin girişim olmadan çalışmasına izin vermesi için%windir%\CCM\ScriptStore hariç tutulması önerilir.

## <a name="prerequisites"></a>Ön koşullar

- PowerShell betikleri çalıştırmak için, istemcinin PowerShell sürüm 3,0 veya üzerini çalıştırıyor olması gerekir. Ancak, çalıştırdığınız bir betik bir PowerShell 'in daha sonraki bir sürümünden işlevsellik içeriyorsa, betiği çalıştırdığınız istemcinin bu PowerShell sürümünü çalıştırması gerekir.
- Configuration Manager istemcileri, betikleri çalıştırmak için istemciyi 1706 sürümünden veya daha sonra çalıştırıyor olmalıdır.
- Betikleri kullanmak için uygun Configuration Manager güvenlik rolünün bir üyesi olmanız gerekir.
- Betikleri içeri ve dışarı yazmak için-hesabınız **SMS betikleri**için **oluşturma** izinlerine sahip olmalıdır.
- Betikleri onaylamak veya reddetmek için-hesabınız **SMS betikleri**için **onay** izinlerine sahip olmalıdır.
- Betikleri çalıştırmak için-hesabınızın **koleksiyonlar**Için **komut dosyası çalıştırma** izinlerine sahip olması gerekir.

Configuration Manager Güvenlik rolleri hakkında daha fazla bilgi için:</br>
[Çalıştırma betikleri için güvenlik kapsamları](#security-scopes)</br>
[Çalıştırma betikleri için güvenlik rolleri](#bkmk_ScriptRoles)</br>
[Rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md).

## <a name="limitations"></a>Sınırlamalar

Çalıştırma betikleri Şu anda şunları destekler:

- Komut dosyası dilleri: PowerShell
- Parametre türleri: Integer, String ve List.


>[!WARNING]
>Parametreleri kullanırken, olası PowerShell ekleme saldırısı riski için bir yüzey alanı açıldığını unutmayın. Parametre girişini doğrulamak veya önceden tanımlanmış parametreleri kullanmak gibi normal ifadeleri kullanma gibi, etkilerini azaltmak ve çözmek için çeşitli yollar vardır. En iyi genel uygulama, PowerShell betiklerinizde gizli dizileri (parola, vb.) içermemelidir. [PowerShell betiği güvenliği hakkında daha fazla bilgi edinin](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Betik yazarlarını ve onaylayanları Çalıştır

Çalıştırma betikleri, komut dosyasının uygulanması ve yürütülmesi için ayrı roller olarak *betik yazarları* ve *betik onaylayanları* kavramını kullanır. Yazar ve onaylayan rollerinin ayrı olması, betikleri çalıştıran güçlü araç için önemli bir işlem denetimi sağlar. Betiklerin yürütülmesine izin veren ancak betikleri oluşturma veya onaylama gibi ek bir *betik* çalıştırma rolü vardır. Bkz. [betikler için güvenlik rolleri oluşturma](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Betikler rol denetimi

Varsayılan olarak, kullanıcılar yazdığı bir betiği onaylayamaz. Betikler güçlü, çok yönlü ve büyük olasılıkla birçok cihaza dağıtıldığı için, bir betiği yazar ve betiği onaylayan kişi arasında rolleri ayırabilirsiniz. Bu roller, daha fazla bakış olmadan bir betiği çalıştırmaya karşı ek bir güvenlik düzeyi sağlar. Sınama kolaylığı için ikincil onayı devre dışı bırakabilirsiniz.

### <a name="approve-or-deny-a-script"></a>Betiği onaylama veya reddetme

Betikler, çalıştırılmadan önce, *komut dosyası onaylayan* rolü tarafından onaylanmalıdır. Bir betiği onaylamak için:

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.
2. **Yazılım kitaplığı** çalışma alanında **betikler**' e tıklayın.
3. **Betik** listesinde, onaylamak veya reddetmek istediğiniz betiği seçin ve ardından **giriş** sekmesinde, **komut dosyası** grubunda, **onayla/reddet**' e tıklayın.
4. **Betiği onayla veya Reddet** iletişim kutusunda, komut dosyası için **Onayla**veya **Reddet** ' i seçin. İsteğe bağlı olarak kararınız hakkında bir yorum girin.  Bir komut dosyasını reddederseniz, istemci cihazlarda çalıştırılamaz. <br>
![Betiği onaylama](./media/run-scripts/RS-approval.png)
1. Sihirbazı tamamlayın. **Komut dosyası** listesinde, yaptığınız eyleme göre **onay durumu** sütununun değiştirilmesini görürsünüz.

### <a name="allow-users-to-approve-their-own-scripts"></a>Kullanıcıların kendi betiklerini onaylamasını sağlar

Bu onay öncelikle betik geliştirmenin test aşaması için kullanılır.

1. Configuration Manager konsolunda, **Yönetim**’e tıklayın.
2. **Yönetim** çalışma alanında, **Site Yapılandırması**'nı genişletin ve **Siteler**'e tıklayın.
3. Site listesinde, sitenizi seçin ve ardından **giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' na tıklayın.
4. **Hiyerarşi ayarları özellikleri** Iletişim kutusunun **genel** sekmesinde, **komut dosyası yazarlarına ek betik onaylayanı gerektir**onay kutusunu temizleyin.

>[!IMPORTANT]
>En iyi uygulama olarak, betik yazarının kendi betiklerini onaylamasını izin vermemelisiniz. Yalnızca bir laboratuvar ayarında izin verilmelidir. Bu ayarı bir üretim ortamında değiştirmenin olası etkisini dikkatlice göz önünde bulundurun.

## <a name="security-scopes"></a>Güvenlik kapsamları
  
Çalıştırma betikleri, Kullanıcı gruplarını temsil eden Etiketler atayarak yazma ve yürütmeyi denetlemek için, Configuration Manager mevcut bir özelliği olan güvenlik kapsamlarını kullanır. Güvenlik kapsamlarını kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Betikler için güvenlik rolleri oluşturma
Komut dosyalarını çalıştırmak için kullanılan üç güvenlik rolü Configuration Manager ' de varsayılan olarak oluşturulmaz. Komut dosyası çalıştıranlar, komut dosyası yazarları ve betik onaylayanlar rollerini oluşturmak için, özetlenen adımları izleyin.

1. Configuration Manager konsolunda, **Yönetim**  > **güvenlik**  > **güvenliği rolleri** ' ne gidin
2. Rol üzerinde sağ tıklayın ve **Kopyala**' ya tıklayın. Kopyaladığınız rolün izinleri zaten atanmış. Yalnızca istediğiniz izinleri aldığınızdan emin olun. 
3. Özel role bir **ad** ve **Açıklama**sağlayın. 
4. Güvenlik rolünü aşağıda özetlenen izinler atayın.  

### <a name="security-role-permissions"></a>Güvenlik rolü Izinleri  

**Rol adı**: betik Özeti  
- **Açıklama**: Bu izinler, yalnızca daha önce diğer roller tarafından oluşturulan ve onaylanan betikleri çalıştırmak için bu rolü etkinleştirir.  
- **İzinler:** Aşağıdakilerin **Evet**olarak ayarlandığından emin olun.  

|Kategori|İzin|Durum|
|---|---|---|
|Koleksiyon|Betiği Çalıştır|Evet|
|Site|Okuma|Evet|
|SMS betikleri|Okuma|Evet|


**Rol adı**: betik yazarları  
- **Açıklama**: Bu izinler, bu rolün betikleri yazarmasını sağlar, ancak bunları onaylayabilir veya çalıştıramazlar.  
- **İzinler**: aşağıdaki izinlerin ayarlandığından emin olun.
 
|Kategori|İzin|Durum|
|---|---|---|
|Koleksiyon|Betiği Çalıştır|Hayır|
|Site|Okuma|Evet|
|SMS betikleri|Oluştur|Evet|
|SMS betikleri|Okuma|Evet|
|SMS betikleri|Sil|Evet|
|SMS betikleri|Değiştir|Evet|


**Rol adı**: betik onaylayanları  
- **Açıklama**: Bu izinler, bu rolün betikleri onaylamasını sağlar, ancak bunları oluşturamaz veya çalıştıramazlar.  
- **İzinler:** Aşağıdaki izinlerin ayarlandığından emin olun.  

|Kategori|İzin|Durum|
|---|---|---|
|Koleksiyon|Betiği Çalıştır|Hayır|
|Site|Okuma|Evet|
|SMS betikleri|Okuma|Evet|
|SMS betikleri|Onaylama|Evet|
|SMS betikleri|Değiştir|Evet|

     
**Betik yazarları rolü için SMS betikleri izinleri örneği**  

 ![Betik yazarları rolü için SMS betikleri izinleri örneği](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Betik oluşturma

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.
2. **Yazılım kitaplığı** çalışma alanında **betikler**' e tıklayın.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **komut dosyası oluştur**' a tıklayın.
4. **Betik** oluşturma sihirbazının **komut dosyası** sayfasında, aşağıdaki ayarları yapılandırın:
    - **Betik adı** -betik için bir ad girin. Aynı ada sahip birden çok komut dosyası oluşturabilseniz de, yinelenen adları kullanmak Configuration Manager konsolunda ihtiyacınız olan betiği bulmanızı zorlaştırır.
    - **Betik dili** -Şu anda yalnızca PowerShell betikleri desteklenir.
    - **Içeri aktarma** -bir PowerShell betiğini konsoluna aktarın. Betik, **betik** alanında görüntülenir.
    - **Temizle** -komut dosyası alanından geçerli betiği kaldırır.
    - **Betik** -Şu anda alınmış olan betiği görüntüler. Bu alandaki betiği gereken şekilde düzenleyebilirsiniz.
5. Sihirbazı tamamlayın. Yeni komut dosyası, **onay bekleniyor**durumuyla birlikte **betik** listesinde görüntülenir. Bu betiği istemci cihazlarda çalıştırmadan önce, bunu onaylamanız gerekir. 

> [!IMPORTANT]
> Betikleri Çalıştır özelliğini kullanırken bir cihazın yeniden başlatılmasını veya Configuration Manager aracısının yeniden başlatılmasını önleyin. Bunun yapılması sürekli yeniden başlatma durumuna yol açabilir. Gerekirse, istemci bildirimi özelliğinde cihazların yeniden başlatılmasını sağlayan geliştirmeler vardır. [Bekleyen yeniden başlatma sütunu](../../core/clients/manage/manage-clients.md#restart-clients) , yeniden başlatma gerektiren cihazların belirlenmesine yardımcı olabilir. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Betik parametreleri

Bir betiğe parametre eklemek, çalışmanız için daha fazla esneklik sağlar. En fazla 10 parametre ekleyebilirsiniz. Aşağıda komut dosyalarını Çalıştır özelliğinin geçerli özelliği komut dosyası parametreleriyle birlikte özetlenmektedir. *String*, *Integer* veri türleri. Önceden ayarlanmış değerlerin listeleri de mevcuttur. Betiğinizin desteklenmeyen veri türleri varsa, bir uyarı alırsınız.

**Betik oluştur** iletişim **kutusunda betik ' ın altında** **betik parametreleri** ' ne tıklayın.

Betiğinizin parametrelerinin her birinin, daha fazla ayrıntı ve doğrulama eklemek için kendi iletişim kutusu vardır. Betikte varsayılan bir parametre varsa, parametre Kullanıcı arabiriminde numaralandırılır ve onu ayarlayabilirsiniz. Komut dosyasını hiçbir şekilde doğrudan değiştirmeyeceği için Configuration Manager varsayılan değerin üzerine yazmaz. Bunun için Kullanıcı arabiriminde "önceden doldurulan önerilen değerler" verilmiştir ancak Configuration Manager çalışma zamanında "varsayılan" değerlere erişim sağlamaz. Bu, komut dosyası doğru varsayılan değerlere sahip olacak şekilde düzenlenerek geçici olarak çalışabilir. <!--17694323-->

>[!IMPORTANT]
> Parametre değerleri tek tırnak içeremez. </br></br>
> Tek tırnak içine alınmış veya dahil edilen parametre değerlerinin betiğe doğru şekilde geçirilmediği bilinen bir sorun vardır. Bir betik içinde boşluk içeren varsayılan parametre değerlerini belirtirken, bunun yerine çift tırnak kullanın. Bir **betiğin**oluşturulması veya yürütülmesi sırasında varsayılan parametre değerlerini belirtirken, değerin bir boşluk içerip içermediğini ne olursa olsun, varsayılan değeri çift ya da tek tırnak içinde çevreleyen gerekli değildir.

### <a name="parameter-validation"></a>Parametre doğrulama

Betiğinizdeki her parametrenin, bu parametre için doğrulama eklemeniz için bir **betik parametresi özellikleri** iletişim kutusu vardır. Doğrulama eklendikten sonra, doğrulamasını karşılamayan bir parametre için değer giriyorsanız hata almalısınız.

#### <a name="example-firstname"></a>Örnek: *FirstName*

Bu örnekte, *adı*dize parametresinin özelliklerini ayarlayabileceksiniz.

![Betik parametreleri-dize](./media/run-scripts/RS-parameters-string.png)


**Betik parametresi özellikleri** iletişim kutusunun doğrulama bölümü, kullanmanız için aşağıdaki alanları içerir:

- **Minimum uzunluk** - *FirstName* alanının en az karakter sayısı.
- **Maksimum uzunluk**- *FirstName* alanının en fazla karakter sayısı
- **Regex** - *normal ifade*için Short. Normal Ifadeyi kullanma hakkında daha fazla bilgi için, *normal ifade doğrulamasını kullanarak*bir sonraki bölüme bakın.
- **Özel hata** -sistem doğrulama hata iletilerinin yerini alan özel hata iletinizi eklemek için faydalıdır.

#### <a name="using-regular-expression-validation"></a>Normal Ifade doğrulamasını kullanma

Normal ifade, bir karakter dizesini kodlanmış bir doğrulamaya göre denetlemek için programlama açısından bir düzenleme biçimidir. Örneğin, Regex alanına yerleştirerek *FirstName* alanındaki büyük alfabetik bir karakterin yokluğunu kontrol edebilirsiniz `[^A-Z]` . *RegEx*

Bu iletişim kutusu için normal ifade işleme .NET Framework tarafından desteklenir. Normal ifadeleri kullanma hakkında yönergeler için bkz. [.net normal ifade](/dotnet/standard/base-types/regular-expressions) ve [normal ifade dili](/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Betik örnekleri

Bu özellik ile kullanmak isteyebileceğiniz betikleri gösteren birkaç örnek aşağıda verilmiştir.

### <a name="create-a-new-folder-and-file"></a>Yeni bir klasör ve dosya oluştur

Bu betik, adlandırma girişinizi belirtilen klasör içinde yeni bir klasör ve dosya oluşturur.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>İşletim sistemi sürümünü al

Bu betik, makinenin işletim sistemi sürümü için sorgulamak üzere WMI kullanır.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> PowerShell betikleri düzenleme veya kopyalama
<!--3705507-->
*(Sürüm 1902 ile tanıtılan)*  
**Betikleri Çalıştır** özelliği ile kullanılan mevcut bir PowerShell betiğini **düzenleyebilir** veya **kopyalayabilirsiniz** . Değiştirmeniz gereken bir betiği yeniden oluşturmak yerine, şimdi doğrudan düzenleyin. Her iki eylem de yeni bir komut dosyası oluştururken kullandığınız sihirbaz deneyimini kullanır. Bir betiği düzenlerken veya kopyaladığınızda, Configuration Manager onay durumunu kalıcı durumdan tutmaz.

> [!Tip]  
> İstemcilerde etkin bir şekilde çalışan bir betiği düzenlemeyin. Özgün betiği çalıştırmayı tamammayamazlar ve bu istemcilerden amaçlanan sonuçları elde olmayabilirsiniz.  

### <a name="edit-a-script"></a>Betiği düzenleme

1. **Yazılım kitaplığı** çalışma alanının altındaki **betikler** düğümüne gidin.
1. Düzenlenecek betiği seçin, ardından şeritte **Düzenle** ' ye tıklayın. 
1. Betik **ayrıntıları** sayfasında betiğinizi değiştirin veya yeniden içeri aktarın.
1. **Özeti** görüntülemek için **İleri** ' ye tıklayın, ardından, Düzenlemeden sonra **kapatın** .

### <a name="copy-a-script"></a>Betiği Kopyala

1. **Yazılım kitaplığı** çalışma alanının altındaki **betikler** düğümüne gidin.
1. Kopyalanacak betiği seçin, sonra Şeritteki **Kopyala** ' ya tıklayın.
1. Betik **adı** alanındaki betiği yeniden adlandırın ve ihtiyacınız olabilecek ek düzenlemeler yapın.
1. **Özeti** görüntülemek için **İleri** ' ye tıklayın, ardından, Düzenlemeden sonra **kapatın** .


## <a name="run-a-script"></a>Betik çalıştırma

Bir komut dosyası onaylandıktan sonra, tek bir cihazda veya koleksiyonda çalıştırılabilir. Komut dosyanızın yürütülmesi başladıktan sonra, bir saat içinde zaman aşımına geçen yüksek öncelikli bir sistem aracılığıyla hızlı bir şekilde başlatılır. Betik sonuçları daha sonra bir durum iletisi sistemi kullanılarak döndürülür.

Betiğinizin bir hedef koleksiyonunu seçmek için:

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.
2. Varlıklar ve Uyum çalışma alanında, **Aygıt Koleksiyonları**'nı tıklatın.
3. **Cihaz Koleksiyonları** listesinde, komut dosyasını çalıştırmak istediğiniz cihaz koleksiyonuna tıklayın.
4. Seçtiğiniz bir koleksiyonu seçin, **Betiği Çalıştır**' a tıklayın.
5. **Betiği Çalıştır** sihirbazının **komut dosyası** sayfasında listeden bir komut dosyası seçin. Yalnızca onaylanan betikler gösterilir.
6. **İleri**' ye tıklayın ve Sihirbazı doldurun.

> [!IMPORTANT]
> Bir komut dosyası çalıştırılmadığı için örneğin, bir saatlik zaman diliminde bir hedef cihaz kapalı olduğu için, yeniden çalıştırmanız gerekir.

### <a name="target-machine-execution"></a>Hedef makine yürütme

Komut dosyası hedeflenen istemci (ler) de *sistem* veya *bilgisayar* hesabı olarak yürütülür. Bu hesabın sınırlı ağ erişimi vardır. Komut dosyası tarafından uzak sistemlere ve konumlara erişime uygun şekilde sağlanması gerekir.

## <a name="script-monitoring"></a>Betik İzleme

Bir cihaz koleksiyonunda betik çalıştırmayı başlattıktan sonra, işlemi izlemek için aşağıdaki yordamı kullanın. Bir betiği yürütülürken gerçek zamanlı olarak izleyebilir ve daha sonra belirli bir çalıştırma betiği yürütmesi için durum ve sonuçlara geri döneceksiniz. Betik durumu verileri, [eski Istemci işlem bakımını silme görevinin](../../core/servers/manage/reference-for-maintenance-tasks.md) bir parçası olarak temizlenir veya betiği silinir.<br>

![Betik izleyici-betik çalıştırma durumu](./media/run-scripts/RS-monitoring-three-bar.png)

1. Configuration Manager konsolunda, **izleme**' yi tıklatın.
2. **İzleme** çalışma alanında, **betik durumu**' nu tıklatın.
3. **Betik durumu** listesinde, istemci cihazlarında çalıştırdığınız her komut dosyası için sonuçları görüntüleyebilirsiniz. Bir komut dosyası çıkış kodu **0** genellikle betiğin başarıyla çalıştığını gösterir.

 
   ![Betik izleyicisinde kesilen betik](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>Betik çıkışı

İstemcinin betik sonuçlarını [ConvertTo-JSON](/powershell/module/microsoft.powershell.utility/convertto-json) cmdlet 'INE ayırarak JSON biçimlendirmesini kullanarak geri dönüş betiği çıkışı. JSON biçimi sürekli olarak okunabilir betik çıkışı döndürüyor. Nesneleri çıkış olarak döndürmeyen betikler için, ConvertTo-JSON cmdlet 'i, çıktıyı, istemcinin JSON yerine döndürdüğü basit bir dizeye dönüştürür.  

- Bilinmeyen bir sonuç elde eden veya istemcinin çevrimdışı olduğu betikler, grafiklerde veya veri kümesinde gösterilmez. <!--507179-->
- 4 KB 'ye kırpdığından büyük betik çıkışı döndürülmekten kaçının. <!--508488-->
- JSON biçimlendirmesinde doğru şekilde görüntülenebilmesi için, bir numaralandırma nesnesini betiklerdeki dize değerine dönüştürün. <!--508377-->

   ![Enum nesnesini bir sabit değere Dönüştür](./media/run-scripts/enum-tostring-JSON.png)

Ayrıntılı betik çıkışını ham veya yapılandırılmış JSON biçiminde görüntüleyebilirsiniz. Bu biçimlendirme, çıktının okunmasını ve çözümlenmesini kolaylaştırır. Betik geçerli bir JSON biçimli metin döndürürse veya çıkış, [ConvertTo-JSON](/powershell/module/microsoft.powershell.utility/convertto-json) PowerShell cmdlet 'ı kullanılarak JSON 'a dönüştürülebileceğinden, ayrıntılı çıktıyı **JSON çıktısı** veya **Ham çıktı**olarak görüntüleyin. Aksi takdirde tek seçenek **betik çıktıdır**.

### <a name="example-script-output-is-convertible-to-valid-json"></a>Örnek: betik çıkışı geçerli JSON 'a dönüştürülebilir

Komutundaki `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Örnek: betik çıkışı geçerli bir JSON değil

Komutundaki `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>Günlük dosyaları

- İstemcide, varsayılan olarak C:\Windows\CCM\logs:  
  - **Betikler. log**  
  - **CcmMessaging.log**  

- MP 'de, varsayılan olarak C:\ SMS_CCM \logs ' de:
  - **MP_RelayMsgMgr. log**  

- Site sunucusunda, varsayılan olarak C:\Program Files\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine. log**

## <a name="see-also"></a>Ayrıca Bkz.

- [Configuration Manager için rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md)