---
title: Güncelleştirme oluştur
titleSuffix: Configuration Manager
description: System Center Updates Publisher yazılım güncelleştirmeleri oluşturun ve paketleyin
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723988"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Updates Publisher ile yazılım güncelleştirmeleri ve güncelleştirme paketleri oluşturma

*Uygulama hedefi: System Center Updates Publisher*

Updates Publisher ile, güncelleştirme paketleri oluşturmak için kendi güncelleştirmelerinizi oluşturmak üzere **güncelleştirme oluştur** sihirbazını ve **paket oluşturma** Sihirbazı 'nı kullanabilirsiniz.

Bu iki sihirbaz benzer bir iş akışına sahip olduğundan, bir güncelleştirme paketi oluşturma yordamı, yalnızca ayrıntılı farkları olan güncelleştirmeler oluşturma yordamına başvurur.

## <a name="use-the-create-update-wizard"></a>Güncelleştirme oluşturma Sihirbazı 'nı kullanma
1. Konsolunda **güncelleştirmeler çalışma alanı**' na gidin ve **Başlarken** bölmesinde, şeridin **giriş** sekmesinden **Güncelleştir** ' i seçin. Bu, **güncelleştirme oluştur** sihirbazını açar.

2. **Paket** sayfasında, güncelleştirmeyi yapılandırmanıza yardımcı olması için aşağıdaki bilgileri kullanın:

   -   Bir paket kaynağı olarak kullanacağınız yazılım güncelleştirme paketini bulmak için, **Gözden** geçirme ' yi seçin. Geçerli kaynaklar şunlardır. MSı,. MSP veya. EXE dosyaları. Güncelleştirmeler yayımcısının dosya karması oluşturmak için dosyaya erişmesi gerekir. Daha sonra, oluşturduğunuz güncelleştirmenin güncelleştirme meta verilerinde karma ve dosya adı kullanılır.

   -   Bu güncelleştirme için içeriğin kaynak konumunu belirtin. Normalde bu, güncelleştirme ikilisinin bir WSUS sunucusuna yayınlanma sırasında indirileceği konumdur.  **Yazılım güncelleştirme içeriğini yayımlamak için bir yerel kaynak kullan** seçeneği işaretliyse, yol gerekli değildir.

       Daha sonra, güncelleştirme bir WSUS sunucusuna yayımlandığında, Updates Publisher güncelleştirmenin ikili dosyalarını belirtilen kaynak konumundan indirir.  Hiçbir yol sağlanmazsa, Update Publisher güncelleştirme ikilisinin [yerel kaynak yayımlama yolunu](updates-publisher-options.md#advanced) arar.

   -   Yazılım güncelleştirmesinin **ikili dilini** belirtin.

   -   **Başarı dönüş kodlarını**ve güncelleştirme için **başarılı bekleyen yeniden başlatma kodlarını** belirtin. Birden çok dönüş kodunu virgül kullanarak ayırın. Güncelleştirme yüklemesinin başarılı olduğunu ve yeniden başlatma gerekne zaman gerektiğini anlamak için dönüş kodlarını kullanabilirsiniz.

       -   Windows Installer dosyaları ve düzeltme ekleri (. MSI ve. MSP dosyaları) bu değerleri otomatik olarak ayarlar ve değiştirilemeyebilir.

       -   Bekleniyor. EXE güncelleştirmeleri, tarafından tanımlanan varsayılan kodlardır. Bir dönüş kodu belirtilmemişse EXE dosyası kullanılır.

   -   Yazılım güncelleştirmesini yüklemek için gereken tüm komut satırı bağımsız değişkenlerini belirtin.

       -   Windows Installer dosyaları ve düzeltme ekleri (. MSI ve. MSP dosyaları) bu değerleri otomatik olarak ayarlar. Bu dosya türleri için bağımsız değişkenlerin ** \[ad\]=\[değeri\]** olarak belirtilmesi gerekir. Buna ek olarak, **/** ( **/qn**gibi) ile başlayan tüm seçenekler için desteklenmez. MSI veya. MSP yazılım güncelleştirmeleri.

       -   Bekleniyor. EXE güncelleştirmeleri, tüm bağımsız değişkenler geçerlidir.

3. **Bilgi** sayfasında, güncelleştirme yayımlandığında veya verildiğinde dahil edilen güncelleştirme hakkındaki ayrıntıları belirtin. Ayrıntılar, güncelleştirme adı (başlık) ve açıklama gibi yerelleştirilmiş özellikleri içerir. Daha sonra, bu güncelleştirme hakkında daha fazla bilgi edinmek için sınıflandırma, satıcı, ürün ve nereden daha fazla genel Ayrıntılar belirtirsiniz.

    __Yerelleştirilmiş Özellikler:__

   - **Dil**: bir dil seçin ve ardından bir başlık ve açıklama belirtin. Daha sonra her dilin kendi başlığını ve açıklamasını desteklediği ek dilleri seçebilirsiniz.

   - **Başlık**: güncelleştirme adını girin. Bu ad, Updates Publisher konsolunun güncelleştirmeler çalışma alanında görüntülenir.

   - **Açıklama**: güncelleştirmenin kolay bir açıklaması. Güncelleştirmenin ne yüklenmesinin ve ne zaman kullanılması gerektiği dahil olabilirsiniz.

   **Sınıflandırma:** Aşağıda, farklı sınıflandırmaların ortak açıklamaları verilmiştir.

   - **Update**: Şu anda yüklü olan bir uygulama veya dosyaya yönelik bir güncelleştirme.

   - **Kritik**: güvenlikle ilgili olmayan kritik bir hatayı ele alan belirli bir sorun için yaygın olarak yayınlanan bir güncelleştirmedir.

   - **Özellik paketi**: bir ürün sürümünün dışında dağıtılan ve tipik olarak bir sonraki tam ürün sürümüne dahil edilen yeni ürün özellikleri.

   - **Güvenlik**: güvenlikle ilgili ürüne özgü bir sorun için yaygın olarak yayınlanan bir güncelleştirme.

   - **Güncelleştirme paketi**: kolay dağıtım için bir arada paketlenmiş toplu bir düzeltme kümesi. Bu düzeltmeler, güvenlik güncelleştirmeleri, kritik güncelleştirmeler, güncelleştirmeler ve benzerini içerebilir. Güncelleştirme paketi genellikle güvenlik veya ürün özelliği gibi belirli bir alana yöneliktir.

   - **Hizmet paketi**: bir uygulamaya uygulanan toplu bir düzeltme kümesi. Bu düzeltmeler, güvenlik güncelleştirmeleri, kritik güncelleştirmeler, yazılım güncelleştirmeleri ve benzerini içerebilir.

   - **Araç**: bir veya daha fazla görevi tamamlamaya yardımcı olan bir aracı veya özelliği belirtir.

   - **Sürücü**: sürücü yazılımı için bir güncelleştirme.

   **Satıcı:** Güncelleştirme için bir satıcı belirtin. Depodaki güncelleştirmelerin değerlerini kullanmak için açılan listeyi kullanabilirsiniz. Bir satıcı belirttiğinizde, sihirbaz, zaten mevcut değilse, **güncelleştirmeler çalışma alanındaki** **tüm yazılım güncelleştirmeleri** altında bu satıcı adını taşıyan bir klasör oluşturur. Aşağıda, oluşturduğunuz güncelleştirmeler için girilebilecek Windows Server Update Services (WSUS) ayrılmış adları verilmiştir:
   - Microsoft Corporation
   - Microsoft
   - Güncelleştirme
   - Yazılım Güncelleştirmesi
   - Araçlar
   - Araç
   - Kritik
   - Kritik güncelleştirmeler
   - Güvenlik
   - Güvenlik Güncelleştirmeleri
   - Özellik paketi
   - Güncelleştirme paketi
   - Hizmet Paketi
   - Sürücü
   - Sürücü güncelleştirmesi
   - Paket
   - Paket güncelleştirmesi

   **Ürün**: güncelleştirmenin için olduğu ürün türünü belirtin. Depodaki güncelleştirmelerin değerlerini kullanmak için açılan listeyi kullanabilirsiniz. **Satıcı**IÇIN kullanılamayan WSUS ayrılmış adlarının aynı listesi, **ürün**için kullanılamaz.

   **Daha fazla bilgi URL 'si**: Bu güncelleştirme hakkında daha fazla bilgi bulabileceğiniz URL 'yi belirtin. Bu URL 'YI girerken **https** veya **http** için küçük harfler kullanmanız gerekir.

4. **Isteğe bağlı bilgi** sayfasında, güncelleştirme hakkında ek bilgi sağlayan ayrıntıları yapılandırabilirsiniz.

   -   **Bülten kimliği**: Bülten kimlikleri genellikle güncelleştirme satıcıları tarafından sağlanmamıştır, ancak her zaman değildir.

   -   **Makale kimliği**: bir yazılım güncelleştirme makalesi varsa, makale kimliği, güncelleştirmeyle ilgili ek bilgi arayan bireyler için yararlı olabilir.

   -   **CVE kimlikleri:** Güncelleştirme veya güncelleştirme paketiyle ilgili güvenlik bilgileri sağlayan bir veya daha fazla ortak güvenlik açıkları ve Etkilenmeler (CVE) tanımlayıcısını listeleyin. Birden fazla listelerken, bu örnekte olduğu gibi, Cvileri ayırmak için noktalı virgül kullanın: *CVE1; CVE2.*

   -   **Destek URL 'si:** Varsa, bu güncelleştirme için destek bilgilerini içeren URL 'YI listeleyin. Bu URL 'YI girerken **https** veya **http** için küçük harfler kullanmanız gerekir.

   -   **Önem derecesi:** Bu güncelleştirme için önem derecesini ayarlayın.

   -   **Etki:** Aşağıdaki seçenekler, etki belirtmek için kullanılabilir:
       -   **Normal –** Güncelleştirmenin tipik yükleme yordamlarını gerektirdiğini belirtmek için bunu kullanın.
       -   **Ara –** Güncelleştirmenin en düşük yükleme yordamlarını gerektirdiğini belirtmek için bunu kullanın.
       -   **Özel Işlem gerektirir –** Güncelleştirmeyi diğer güncelleştirmelerden dışlayarak, güncelleştirmenin kendisi tarafından yüklenmesi gerektiğini belirtmek için bunu kullanın.   <br /><br />

   -   **Yeniden başlatma davranışı:** Güncelleştirme yeniden başlatma davranışı hakkında bilgi sağlamak için bunu kullanın. Bu ayar, güncelleştirme yüklemesinin gerçek davranışını etkilemez.

       -   **Hiçbir**şekilde yeniden başlatma: bilgisayar, yazılım güncelleştirmesini yükledikten sonra hiçbir şekilde sistem yeniden başlatma işlemini gerçekleştirmez.
       -   **Her zaman yeniden başlatma gerektirir**: bilgisayar, yazılım güncelleştirmesini yükledikten sonra her zaman bir sistem yeniden başlatması gerçekleştirir.
       -   **Yeniden başlatma Isteğinde bulunabilir**: yazılım güncelleştirmesini yükledikten sonra, bilgisayar yalnızca bir yeniden başlatma gerekliyse sistemin yeniden başlatılmasını ister. Kullanıcının yeniden başlatmayı erteleme seçeneği vardır. Varsayılan değer budur. <br /><br />

5. **Önkoşul** sayfasında, bu güncelleştirmenin yüklenebilmesi için bir bilgisayara yüklenmesi gereken önkoşulları belirtin. Önkoşullar, kimlik veya diğer güncelleştirmeler için **algılayıcısı** olabilir. Algılayıcısı, bilgisayarların CPU 'sunu 64 bitlik bir işlemci olmasını gerektiren bir tane gibi üst düzey kurallardır. Detectoıds, bu güncelleştirme yüklenmeden önce yüklenmesi gereken belirli güncelleştirmeleri de belirtebilir.

   -   Daha iyi performans için, aynı denetimi veya eylemi gerçekleştiren *yüklenebilir* ve *yüklü kuralları* oluşturmak yerine, algılayıcısı kullanın.

   Belirli güncelleştirmeleri veya algılayıcısı bulmanıza yardımcı olması için **kullanılabilir yazılım güncelleştirmeleri ve algılayıcısı** için arama seçeneğini kullanın. Örneğin, belirli CPU mimarisine göre yüklemeyi sınırlandırmanıza olanak sağlayan algılayıcısı bulmak için **CPU** 'da arama yapın.

   Bir önkoşul olarak eklemek için bir veya daha fazla öğeyi tek seferde seçebilirsiniz. Önkoşullar eklenirken, seçilen detecıd 'ler bir veya daha fazla grup olarak eklenir. Yüklemeyi nitelemek için, bir bilgisayarın yapılandırdığınız her bir grubun en az bir üyesinin gereksinimini karşılaması gerekir:

   -   **Önkoşul Ekle** ' ye tıkladığınızda, seçtiğiniz tüm öğeler ayrı, bireysel, gruplara eklenir. Bu güncelleştirmeye uygun olması için, bir bilgisayarın bu gruptaki önkoşulları karşılaması ve yapılandırılmış ek gruplar için gereksinimleri geçirmesi gerekir.

   -   **Grup Ekle** ' ye tıkladığınızda, seçtiğiniz tüm öğeler tek bir gruba eklenir. Bu güncelleştirmeye uygun olması için bir bilgisayarın bu gruptaki en az birini karşılaması ve yapılandırılmış ek gruplar için gereksinimleri geçirmesi gerekir.

6. **Yerine geçme** sayfasında, bu güncelleştirme tarafından değiştirilen (yerine geçilen) güncelleştirmeleri belirtin. Bu güncelleştirme yayımlandığında Configuration Manager, yenisiyle değiştirilen her güncelleştirmeyi **zaman aşımına erdiğinden**işaretleyecek. İstemciler, yenisiyle değiştirilen güncelleştirmeler yerine bu güncelleştirmeyi yükler.

7. **Uygulanabilirlik** sayfasında, bir cihazın bu güncelleştirmenin gerekip gerekmediğini belirleyen bir kurallar kümesi tanımlamak Için **kural düzenleyicisini** kullanın. (Bu sayfa, **yüklenen** sayfa ile benzerdir, bu da bunu izler.)

   Yeni bir kural eklemek için, üzerine tıklayın ![Yeni Kural](media/newrule.png). Bu, kuralları yapılandırabileceğiniz uygulanabilirlik kuralı sayfasını açar.

   Oluşturabileceğiniz kuralların türleri şunlardır:

   -   **Dosya** – Bu güncelleştirme uygulanmadan önce, bir cihazın belirttiğiniz bir veya daha fazla ölçütü karşılayan bir dosyaya sahip bir dosyanın olmasını gerektirmek için bu kuralı kullanın.

   -   **Kayıt defteri –** Bir cihaz bu güncelleştirmeyi yüklemeye uygun olmadan önce mevcut olması gereken kayıt defteri ayrıntılarını belirtmek için bu türü kullanın.

   -   **Sistem –** Bu kural, uygulanabilirliği belirlemede sistem ayrıntılarını kullanır. Cihazların işletim sistemini tanımlamak için bir Windows sürümü, Windows dili, işlemci mimarisi tanımlamayı veya bir WMI sorgusu belirtmeyi seçebilirsiniz.

   -   **Windows Installer –** Yüklü olan uygulanabilirliği öğrenmek için bu kural türünü kullanın. MSI veya Windows Installer Patch (. MSP). Ayrıca, gereksinimin bir parçası olarak belirli bileşenlerin veya özelliklerin yüklenip yüklenmediğini da belirleyebilirsiniz.

       > [!IMPORTANT]  
       > Yönetilen cihazlarda, Windows Update Aracısı Kullanıcı başına yüklenen Windows yükleme paketlerini algılayamaz. Bu kural türünü kullandığınızda, Windows Installer paketinin Kullanıcı başına veya sistem başına olarak düzgün bir şekilde algılanabilmesi için dosya sürümleri veya kayıt defteri anahtarı değerleri gibi ek uygulanabilirlik kurallarını yapılandırın.

   -   **Kaydedilen kural –** Bu seçenek *, kurallar çalışma alanında oluşturduğunuz*kuralları bulmanızı ve kullanmanızı sağlar.

       Bir kural oluşturduktan sonra, kuralı değiştirmek için diğer simgeleri ve bu kurallar arasındaki ilişkileri tanımlamak için birden fazla kural varsa kullanabilirsiniz.

   Kuralları oluşturma ve ekleme bittiğinde, bu kümeyi kaydetmek için **kural kümesi oluştur** Iletişim kutusunda **Tamam** ' a tıklayın. Daha sonra **Yeni** bir kural oluşturabilir ve bu kurala göre kümesini de ekleyebilirsiniz.

   Bir güncelleştirmeye eklemek üzere birden çok kural veya kural kümesi olduğunda, kurallar arasındaki koşulları ve bunların hangi sırayla işleyeceğini anlamak için **kural düzenleyicisinde** mantıksal işleçleri kullanabilirsiniz.

8. **Yüklü** sayfada, bir cihazın yapılandırdığınız güncelleştirmeyi zaten yükleyip yüklememediğini belirleyen bir kurallar kümesi tanımlamak **için kural düzenleyicisini** kullanın. (Bu sayfa, bu sayfaya devam eden **uygulanabilirlik** sayfasına benzerdir.)

   Sihirbazın bu sayfası, **uygulanabilirlik** sayfasıyla aynı seçenek ve ölçütlere sahip kuralların yapılandırılmasını destekler.

   Sihirbaz tamamlandığında, yeni güncelleştirme, bu güncelleştirme için kullandığınız **satıcı** ve **ürün** adı tarafından tanımlanan **güncelleştirmeler çalışma alanındaki** bir düğüme eklenir.

## <a name="use-the-create-bundle-wizard"></a>Paket oluşturma Sihirbazı 'nı kullanma
Bu sihirbaz [güncelleştirme Oluştur Sihirbazı](#use-the-create-update-wizard)olarak aynı iş akışını kullandığından, bu iş akışını kullanın, ancak şu paketlerde aşağıdaki farka göz önünde unutmayın:

1.  Sihirbazı başlatmak için konsolunda **güncelleştirmeler çalışma alanı**' na gidin ve ardından şeridin **giriş** sekmesinden **paket** ' i seçin.

2.  Güncelleştirme oluşturma sihirbazının aksine, paket oluşturulurken paket sayfası yoktur.

3.  **Bilgi** sayfasında, güncelleştirme yayımlandığında veya verildiğinde bulunan güncelleştirme paketiyle ilgili ayrıntıları belirtin.

4.  **Isteğe bağlı bilgi** sayfasında, güncelleştirme paketi hakkında ek bilgiler sağlayan ayrıntıları yapılandırabilirsiniz. Kullanılabilir seçenekler güncelleştirme oluşturma ile aynıdır. Ancak, etki ve yeniden başlatma davranışı seçenekleri, paket için uygulanmadığından kullanılamaz.

5.  **Önkoşul** sayfasında, bu paketin yüklenebilmesi için bir bilgisayara yüklenmesi gereken önkoşulları belirtin. Bu kurallar, bireysel güncelleştirmeler için görüldüğü ile aynıdır.

6.  **Yerine geçme** sayfasında, bu güncelleştirme paketi tarafından değiştirilen (yerine geçilen) güncelleştirmeleri belirtin. Bu kurallar, bireysel güncelleştirmeler için görüldüğü ile aynıdır.

7.  **Üyeler** sayfasında, güncelleştirme paketine eklemek için güncelleştirmeler ' i seçin. Yalnızca oluşturduğunuz veya Updates Publisher 'a aktardığınız güncelleştirmeler kullanılabilir.

Sihirbaz tamamlandığında, yeni güncelleştirme paketi, güncelleştirme paketi için kullandığınız **satıcı** adı tarafından tanımlanan **güncelleştirmeler çalışma alanındaki** bir düğüme eklenir.
