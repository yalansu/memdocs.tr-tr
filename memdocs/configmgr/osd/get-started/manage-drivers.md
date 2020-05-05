---
title: Sürücüleri yönetme
titleSuffix: Configuration Manager
description: Cihaz sürücülerini içeri aktarmak, paketlerdeki sürücüleri gruplamak ve bu paketleri dağıtım noktalarına dağıtmak için Configuration Manager sürücü kataloğunu kullanın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724128"
---
# <a name="manage-drivers-in-configuration-manager"></a>Configuration Manager sürücüleri yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Configuration Manager ortamınızdaki Windows cihaz sürücülerini yönetmek için kullanabileceğiniz bir sürücü kataloğu sağlar. Cihaz sürücülerini Configuration Manager içine aktarmak, paketler halinde gruplamak ve bu paketleri dağıtım noktalarına dağıtmak için sürücü kataloğunu kullanın. Cihaz sürücüleri, hedef bilgisayara tam işletim sistemini yüklediğinizde ve Windows PE 'yi bir önyükleme görüntüsünde kullandığınızda kullanılabilir. Windows aygıt sürücüleri, kurulum bilgileri (INF) dosyasından ve cihazı desteklemek için gereken ek dosyalardan oluşur. Bir işletim sistemini dağıtırken Configuration Manager, aygıtın donanım ve platform bilgilerini kendi INF dosyasından edinir. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a>Sürücü kategorileri

Aygıt sürücülerini içe aktardığınızda bu sürücüleri bir kategoriye atayabilirsiniz. Aygıt sürücüsü kategorileri, benzer şekilde kullanılan aygıt sürücülerini sürücü kataloğunda bir arada gruplandırmanızı sağlar. Örneğin, tüm ağ bağdaştırıcısı aygıt sürücülerini belirli bir kategoriye ayarlayın. Ardından, [sürücüleri otomatik olarak Uygula](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) adımını içeren bir görev dizisi oluşturduğunuzda, bir cihaz sürücüleri kategorisi belirtin. Configuration Manager daha sonra donanımı tarar ve bu kategorideki ilgili sürücüleri, Windows Kurulumu kullanması için sistemde hazırlamak üzere seçer.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> Sürücü paketleri

İşletim sistemi dağıtımlarını kolaylaştırmaya yardımcı olmak için paketlerdeki benzer cihaz sürücülerini gruplayın. Örneğin, ağınızdaki her bilgisayar üreticisi için bir sürücü paketi oluşturun. Sürücüleri sürücü kataloğuna doğrudan **sürücü paketleri** düğümünde içeri aktarırken, bir sürücü paketi oluşturabilirsiniz. Bir sürücü paketi oluşturduktan sonra dağıtım noktalarına dağıtın. Configuration Manager istemci bilgisayarları sürücüleri gerektiği şekilde yükleyebilir. 

Aşağıdaki noktaları göz önünde bulundurun:  

- Bir sürücü paketi oluşturduğunuzda, paketin kaynak konumu, başka bir sürücü paketi tarafından kullanılmayan boş bir ağ paylaşımının üzerine göstermelidir. SMS sağlayıcısı, bu konum için **tam denetim** izinlerine sahip olmalıdır.  

- Aygıt sürücülerini bir sürücü paketine eklediğinizde Configuration Manager, paketi kaynak konumuna kopyalar. Yalnızca içeri aktardığınız ve sürücü kataloğunda etkinleştirilen aygıt sürücülerini bir sürücü paketine ekleyebilirsiniz.  

- Var olan bir sürücü paketinden aygıt sürücülerinin bir alt kümesini kopyalayabilirsiniz. İlk olarak, yeni bir sürücü paketi oluşturun. Ardından, cihaz sürücülerinin alt kümesini yeni pakete ekleyin ve ardından yeni paketi bir dağıtım noktasına dağıtın.  

- Sürücüleri yüklemek için görev dizileri kullanırken 500’den az cihaz sürücüsü içeren sürücü paketleri oluşturun.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a>Sürücü paketi oluşturma  

> [!IMPORTANT]  
> Bir sürücü paketi oluşturmak için, başka bir sürücü paketi tarafından kullanılmayan boş bir ağ klasörünüz olması gerekir. Çoğu durumda, bu yordama başlamadan önce yeni bir klasör oluşturun.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Işletim sistemleri**' ni genişletin ve ardından **sürücü paketleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **sürücü paketi oluştur**' u seçin.  

3. Sürücü paketi için açıklayıcı bir **ad** belirtin.  

4. Sürücü paketi için isteğe bağlı bir **Açıklama** girin. Bu açıklamayı, sürücü paketinin içeriği veya amacı hakkında bilgi sağlamak için kullanın.  

5. **Yol** kutusunda, sürücü paketi için boş bir kaynak klasör belirtin. Her bir sürücü paketinin benzersiz bir klasör kullanması gerekir. Bu yol bir ağ konumu olarak gereklidir.  

   > [!IMPORTANT]  
   > Site sunucusu hesabının, belirtilen kaynak klasör için **tam denetim** izinlerine sahip olması gerekir.  

Yeni sürücü paketi herhangi bir sürücü içermez. Sonraki adım, pakete sürücü ekler.  

**Sürücü Paketleri** düğümü çeşitli paketler içeriyorsa, paketleri mantıksal gruplara ayırmak için düğüme klasör ekleyebilirsiniz.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a>Sürücü paketleri için ek eylemler  

**Sürücü paketleri düğümünden bir** veya daha fazla sürücü paketi seçtiğinizde sürücü paketlerini yönetmek için ek eylemler gerçekleştirebilirsiniz. 


#### <a name="create-prestage-content-file"></a>Önceden Hazırlanan İçerik Dosyası Oluşturma
İçeriği ve onunla ilişkili meta verilerini el ile içeri aktarmak için kullanabileceğiniz dosyaları oluşturur. Sürücü paketinin depolandığı dağıtım noktaları ve site sunucusu arasında düşük ağ bant genişliğiniz olduğunda önceden hazırlanan içerik kullanın.

#### <a name="delete"></a>Sil
Sürücü paketini **Sürücü Paketleri** düğümünden kaldırır.

#### <a name="distribute-content"></a>İçeriği Dağıt
Sürücü paketini dağıtım noktalarına, dağıtım noktası gruplarına ve koleksiyonlarla ilişkili dağıtım noktası gruplarına dağıtır.

#### <a name="manage-access-accounts"></a>Erişim Hesaplarını Yönet
Sürücü paketi için erişim hesapları ekler, değiştirir veya kaldırır.

Paket erişim hesapları hakkında daha fazla bilgi için bkz. [Configuration Manager kullanılan hesaplar](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Taşı
Sürücü paketini, **Sürücü Paketleri** düğümünde başka bir klasöre taşır.

#### <a name="update-distribution-points"></a>Dağıtım Noktalarını Güncelleştir
Paketin depolandığı tüm dağıtım noktalarında aygıt sürücü paketini güncelleştirir. Bu eylem yalnızca, son dağıtıldığından beri değişen içeriği kopyalar.

#### <a name="properties"></a>Özellikler
**Özellikler** iletişim kutusunu açar. Sürücünün içeriğini ve özelliklerini gözden geçirin ve değiştirin. Örneğin, sürücünün adını ve açıklamasını değiştirin, etkinleştirin veya devre dışı bırakın ve hangi platformların çalıştırabileceği belirtin. 

<!--3607716, fka 1358270-->
Sürüm 1810 ' den başlayarak, sürücü paketlerinin **üretici** ve **model**için meta veri alanları vardır. Bu alanları, genel muhasebe 'de yardım almak veya silebilecekleri eski ve yinelenen sürücüleri belirlemek için sürücü paketlerini etiketlemek üzere kullanın. **Genel** sekmesinde, açılan listelerden varolan bir değeri seçin veya yeni bir giriş oluşturmak için bir dize girin.

**Sürücü paketleri** düğümünde, bu alanlar listede **sürücü üreticisi** ve **sürücü modeli** sütunları olarak görüntülenir. Bunlar, arama ölçütleri olarak da kullanılabilir.

Sürüm 1906 ' den başlayarak, bir istemcideki içeriği önceden önbelleğe almak için bu öznitelikleri kullanın. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Cihaz sürücüleri

Sürücüleri, dağıtılan işletim sistemi görüntüsüne dahil etmeden, hedef bilgisayarlara yükleyebilirsiniz. Configuration Manager, Configuration Manager içe aktardığınız tüm sürücülere başvurular içeren bir sürücü kataloğu sağlar. Sürücü kataloğu, **Yazılım Kitaplığı** çalışma alanında bulunur ve iki düğümden oluşur: **Sürücüler** ve **Sürücü Paketleri**. **Sürücüler** düğümü, sürücü kataloğu içine aktardığınız tüm sürücüleri listeler.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a>Aygıt sürücülerini sürücü kataloğuna aktarma  

Bir işletim sistemini dağıtırken bir sürücü kullanabilmeniz için önce sürücüyü sürücü kataloğuna aktarın. Daha iyi yönetmek için, yalnızca işletim sistemi dağıtımlarınızın bir parçası olarak yüklemeyi planladığınız sürücüleri içeri aktarın. Ağınızdaki donanım cihaz gereksinimleri değiştiğinde mevcut sürücüleri yükseltmenin kolay bir yolunu sağlamak için katalogdaki birçok sürücü sürümünü depolayın.  

Aygıt sürücüsü için içeri aktarma işleminin bir parçası olarak, Configuration Manager sürücü hakkında aşağıdaki özellikleri okur:
- Sağlayıcı
- Sınıf
- Sürüm
- İmza
- Desteklenen donanım
- Desteklenen platform bilgileri

Varsayılan olarak, sürücü, desteklediği ilk donanım cihazından sonra adlandırılır. Aygıt sürücüsünü daha sonra yeniden adlandırabilirsiniz. Desteklenen platformlar listesi, sürücünün INF dosyasındaki bilgilere dayanır. Bu bilgilerin doğruluğu farklılık gösterebileceğinden, bu bilgileri kataloğa aktardıktan sonra sürücünün desteklendiğini el ile doğrulayın.  

Aygıt sürücülerini kataloğa aktardıktan sonra, bunları sürücü paketlerine veya önyükleme görüntü paketlerine ekleyin.  

> [!IMPORTANT]  
> Cihaz sürücülerini doğrudan **sürücüler** düğümünün bir alt klasörüne içeri aktaramazsınız. Cihaz sürücüsünü bir alt klasöre aktarmak için önce cihaz sürücüsünü **Sürücüler** düğümüne aktarın ve ardından sürücüyü alt klasöre taşıyın.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Windows cihaz sürücülerini sürücü kataloğuna aktarma işlemi  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Işletim sistemleri**' ni genişletin ve **sürücüler** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **yeni sürücü içeri aktarma Sihirbazı 'Nı**başlatmak için **sürücüyü içeri aktar** ' ı seçin.  

3. **Sürücüyü bul** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Aşağıdaki ağ yolundaki (UNC) tüm sürücüleri Içeri aktar**: belirli bir klasördeki tüm cihaz sürücülerini içeri aktarmak için, ağ yolunu belirtin. Örneğin: `\\servername\share\folder`.  

        > [!NOTE]  
        > Çok sayıda alt klasör ve çok sayıda sürücü INF dosyası varsa, bu işlem zaman alabilir.  

    - **Belirli bir sürücüyü Içeri aktar**: bir klasörden belirli bir sürücüyü içeri aktarmak için Windows CIHAZ sürücüsü INF dosyasının ağ yolunu belirtin.  

    - **Yinelenen sürücüler için seçeneği belirtin**: yinelenen bir cihaz sürücüsü içeri aktardığınızda sürücü kategorilerini nasıl yöneteceğini Configuration Manager istediğinizi seçin  
        - **Sürücüyü içeri aktarın ve mevcut kategorilere yeni bir kategori ekleyin**  
        - **Sürücüyü içeri aktarın ve mevcut kategorileri tutun**  
        - **Sürücüyü içeri aktarın ve mevcut kategorilerin üzerine yazın**  
        - **Sürücüyü içeri aktarma**  

    > [!IMPORTANT]  
    > Sürücüleri içeri aktardığınızda, site sunucusunun klasörde **Okuma** izni olması gerekir, aksi takdirde içeri aktarma başarısız olur.  

4. **Sürücü ayrıntıları** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Depolama veya ağ sınıfında olmayan sürücüleri gizle (önyükleme görüntüleri için)**: Bu ayarı yalnızca depolama ve ağ sürücülerini göstermek için kullanın. Bu seçenek, genellikle bir video sürücüsü veya modem sürücüsü gibi önyükleme görüntüleri için gerekli olmayan diğer sürücüleri gizler.  

    - **Dijital olarak imzalanmamış sürücüleri gizle**: Microsoft yalnızca dijital olarak imzalanan sürücüleri kullanmanızı önerir  

    - Sürücüler listesinde, sürücü kataloğuna aktarmak istediğiniz sürücüleri seçin.  

    - **Bu sürücüleri etkinleştirin ve bilgisayarların bunları yüklemesine izin verin**: Bilgisayarların cihaz sürücülerini yüklemesine izin vermek için bu ayarı seçin. Bu seçenek varsayılan olarak etkindir.  

        > [!IMPORTANT]  
        > Bir cihaz sürücüsü soruna yol açıyorsa veya bir cihaz sürücüsünün yüklenmesini askıya almak istiyorsanız, içeri aktarma sırasında devre dışı bırakın. Ayrıca, sürücüleri içeri aktardıktan sonra devre dışı bırakabilirsiniz.  

    - Cihaz sürücülerini "masaüstleri" veya "Not defterleri" gibi filtreleme amacıyla bir yönetim kategorisine atamak için **Kategoriler**' i seçin. Ardından varolan bir kategoriyi seçin veya yeni bir kategori oluşturun. [Sürücüleri otomatik olarak Uygula](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) görev dizisi adımı tarafından hangi cihaz sürücülerinin uygulanacağını denetlemek için kategorileri kullanın.  

5. **Sürücü paketlerine Ekle** sayfasında, sürücülerin bir pakete eklenip eklenmeyeceğini seçin.  

    - Aygıt sürücülerini dağıtmak için kullanılan sürücü paketlerini seçin.  

        Gerekirse, yeni bir sürücü paketi oluşturmak için **yeni paket** ' i seçin. Yeni bir sürücü paketi oluşturduğunuzda, başka sürücü paketleri tarafından kullanımda olmayan bir ağ paylaşımının sağlanması gerekir.  

    - Paket zaten dağıtım noktalarına dağıtılmışsa, dağıtım noktalarındaki önyükleme görüntülerini güncelleştirmek için iletişim kutusunda **Evet** ' i seçin. Cihaz sürücülerini, dağıtım noktalarına dağıtılana kadar kullanamazsınız. **Hayır**' ı seçerseniz, önyükleme görüntüsünü kullanmadan önce **dağıtım noktasını Güncelleştir** eylemini çalıştırın. Sürücü paketi hiç dağıtılmadıysa, **sürücü paketleri** düğümündeki **İçerik dağıtma** eylemini kullanmanız gerekir.  

6. **Önyükleme görüntülerine sürücü ekle** sayfasında, mevcut önyükleme görüntülerine cihaz sürücüleri eklenip eklenmeyeceğini seçin.  

    > [!NOTE]  
    > Önyükleme görüntülerine yalnızca depolama ve ağ sürücülerini ekleyin.  

    - Dağıtım noktalarında önyükleme görüntülerini güncelleştirmek için iletişim kutusunda **Evet** ' i seçin. Cihaz sürücülerini, dağıtım noktalarına dağıtılana kadar kullanamazsınız. **Hayır**' ı seçerseniz, önyükleme görüntüsünü kullanmadan önce **dağıtım noktasını Güncelleştir** eylemini çalıştırın. Sürücü paketi hiç dağıtılmadıysa, **sürücü paketleri** düğümündeki **İçerik dağıtma** eylemini kullanmanız gerekir.  

    - Configuration Manager, bir veya daha fazla sürücü mimarisi seçtiğiniz önyükleme görüntülerinin mimarisiyle eşleşmezse sizi uyarır. Eşleşmiyorsa **Tamam**' ı seçin. **Sürücü ayrıntıları** sayfasına dönün ve seçilen önyükleme görüntüsünün mimarisiyle eşleşmeyen sürücüleri temizleyin. Örneğin, bir x64 ve x86 önyükleme görüntüsü seçerseniz tüm sürücüler her iki mimariyi de desteklemelidir. Bir x64 önyükleme görüntüsü seçerseniz tüm sürücüler x64 mimarisini desteklemelidir.  

        > [!NOTE]  
        > - Mimari, üreticiden gelen INF dosyasında bildirilen mimariye dayanır.  
        > - Bir sürücü her iki mimariyi de destekliyorsa, bunu önyükleme görüntüsüne aktarabilirsiniz.  

    - Configuration Manager, bir önyükleme görüntüsüne ağ veya depolama sürücüsü olmayan cihaz sürücüleri eklediğinizde sizi uyarır. Çoğu durumda, önyükleme görüntüsü için gerekli değildir. Sürücüleri önyükleme görüntüsüne eklemek için **Evet** ' i veya geri dönüp sürücü seçiminizi değiştirmek için **Hayır** ' ı seçin.  

    - Configuration Manager, seçilen sürücülerden biri veya daha fazlası düzgün şekilde dijital olarak imzalanmamışsa sizi uyarır. Devam etmek için **Evet** ' i seçin ve geri dönüp sürücü seçiminizde değişiklikler yapmak için **Hayır** ' ı seçin.  

7. Sihirbazı tamamlayın.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Sürücü paketindeki aygıt sürücülerini yönetme  

Sürücü paketlerini ve önyükleme görüntülerini değiştirmek için aşağıdaki yordamları kullanın. Bir sürücü eklemek veya kaldırmak için, önce bu sürücüyü **sürücüler** düğümünde bulun. Ardından seçili sürücünün ilişkilendirildiği paketleri veya önyükleme görüntülerini düzenleyin.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Işletim sistemleri**' ni genişletin ve ardından **sürücüler** düğümünü seçin.  

2. Bir sürücü paketine eklemek istediğiniz cihaz sürücülerini seçin.  

3. Şeridin **giriş** sekmesinde, **sürücü** grubunda **Düzenle**' yi seçin ve ardından **sürücü paketleri**' ni seçin.  

4. Bir aygıt sürücüsü eklemek için, aygıt sürücülerini eklemek istediğiniz sürücü paketlerinin onay kutusunu seçin. Bir aygıt sürücüsünü kaldırmak için, aygıt sürücüsünü kaldırmak istediğiniz sürücü paketlerinin onay kutusunun seçimini kaldırın.  

    Sürücü paketleriyle ilişkili cihaz sürücüleri ekliyorsanız, isteğe bağlı olarak yeni bir paket oluşturabilirsiniz. **Yeni sürücü paketi** iletişim kutusunu açan **yeni paket**' i seçin.  

5. Paket zaten dağıtım noktalarına dağıtılmışsa, dağıtım noktalarındaki önyükleme görüntülerini güncelleştirmek için iletişim kutusunda **Evet** ' i seçin. Cihaz sürücülerini, dağıtım noktalarına dağıtılana kadar kullanamazsınız. **Hayır**' ı seçerseniz, önyükleme görüntüsünü kullanmadan önce **dağıtım noktasını Güncelleştir** eylemini çalıştırın. Sürücü paketi hiç dağıtılmadıysa, **sürücü paketleri** düğümündeki **İçerik dağıtma** eylemini kullanmanız gerekir. Sürücüler kullanılabilir olmadan önce dağıtım noktalarında sürücü paketini güncelleştirmeniz gerekir.  

    Bittiğinde **Tamam ' ı** seçin.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a>Önyükleme görüntüsündeki aygıt sürücülerini yönetme  

Kataloğa aktarılmış Windows cihaz sürücülerine önyükleme görüntüleri ekleyebilirsiniz. Aygıt sürücülerini bir önyükleme yansımasına eklerken aşağıdakileri kullanın:  

- Önyükleme görüntülerine yalnızca depolama ve ağ sürücülerini ekleyin. Diğer sürücü türleri genellikle Windows PE 'de gerekli değildir. Gerekli olmayan sürücüler, önyükleme görüntüsünün boyutunu gereksiz şekilde artırır.  

- Önyükleme görüntüsüne yalnızca Windows 10 cihaz sürücülerini ekleyin. Gerekli olan Windows PE sürümü Windows 10 ' a dayalıdır.  

- Önyükleme görüntüsünün mimarisi için doğru aygıt sürücüsünü kullandığınızdan emin olun. X64 önyükleme görüntüsüne x86 aygıt sürücüsü eklemeyin.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Önyükleme görüntüsüyle ilişkili aygıt sürücülerini değiştirme işlemi  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Işletim sistemleri**' ni genişletin ve ardından **sürücüler** düğümünü seçin.  

2. Sürücü paketine eklemek istediğiniz cihaz sürücülerini seçin.  

3. Şeridin **giriş** sekmesinde, **sürücü** grubunda **Düzenle**' yi seçin ve ardından **önyükleme görüntüleri**' ni seçin.  

4. Bir aygıt sürücüsü eklemek için, aygıt sürücülerini eklemek istediğiniz önyükleme görüntüsünün onay kutusunu seçin. Bir aygıt sürücüsünü kaldırmak için, aygıt sürücüsünü kaldırmak istediğiniz önyükleme görüntüsünün onay kutusunun seçimini kaldırın.  

5. Önyükleme görüntüsünün depolandığı dağıtım noktalarını güncelleştirmek istemiyorsanız, **tamamlandığında dağıtım noktalarını güncelleştir** onay kutusunun işaretini kaldırın. Varsayılan olarak, önyükleme görüntüsü güncelleştirildiğinde dağıtım noktaları güncelleştirilir.  

    - Dağıtım noktalarında önyükleme görüntülerini güncelleştirmek için iletişim kutusunda **Evet** ' i seçin. Cihaz sürücülerini, dağıtım noktalarına dağıtılana kadar kullanamazsınız. **Hayır**' ı seçerseniz, önyükleme görüntüsünü kullanmadan önce **dağıtım noktasını Güncelleştir** eylemini çalıştırın. Sürücü paketi hiç dağıtılmadıysa, **sürücü paketleri** düğümündeki **İçerik dağıtma** eylemini kullanmanız gerekir.  

    - Configuration Manager, bir veya daha fazla sürücü mimarisi seçtiğiniz önyükleme görüntülerinin mimarisiyle eşleşmezse sizi uyarır. Eşleşmiyorsa **Tamam**' ı seçin. **Sürücü ayrıntıları** sayfasına dönün ve seçilen önyükleme görüntüsünün mimarisiyle eşleşmeyen sürücüleri temizleyin. Örneğin, bir x64 ve x86 önyükleme görüntüsü seçerseniz tüm sürücüler her iki mimariyi de desteklemelidir. Bir x64 önyükleme görüntüsü seçerseniz tüm sürücüler x64 mimarisini desteklemelidir.  

        > [!NOTE]
        > - Mimari, üreticiden gelen INF dosyasında bildirilen mimariye dayanır.  
        > - Bir sürücü her iki mimariyi desteklediğini bildirirse bu sürücüyü herhangi bir önyükleme görüntüsüne alabilirsiniz.  

    - Configuration Manager, bir önyükleme görüntüsüne ağ veya depolama sürücüsü olmayan cihaz sürücüleri eklediğinizde sizi uyarır. Çoğu durumda, önyükleme görüntüsü için gerekli değildir. Sürücüleri önyükleme görüntüsüne eklemek için **Evet** ' i veya geri dönüp sürücü seçiminizi değiştirmek için **Hayır** ' ı seçin.  

    - Configuration Manager, seçilen sürücülerden biri veya daha fazlası düzgün şekilde dijital olarak imzalanmamışsa sizi uyarır. Devam etmek için **Evet** ' i seçin veya geri dönüp sürücü seçiminizde değişiklikler yapmak için **Hayır** ' ı seçin.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a>Cihaz sürücüleri için ek eylemler  

Sürücüleri **sürücüler** düğümünde seçtiğinizde, sürücüleri yönetmek için ek eylemler gerçekleştirebilirsiniz.  

#### <a name="categorize"></a>Sınıflandırma
Seçili sürücüler için bir yönetim kategorisini temizler, yönetir veya ayarlar.

#### <a name="delete"></a>Sil
Sürücüyü **sürücüler** düğümünden kaldırır ve ayrıca sürücüyü ilişkili dağıtım noktalarından kaldırır.

#### <a name="disable"></a>Devre Dışı Bırak
Sürücünün yüklenmesini yasaklar. Bu eylem, sürücüyü geçici olarak devre dışı bırakır. Bir işletim sistemini dağıtırken, görev dizisi devre dışı bırakılmış bir sürücü yükleyemez. 

> [!Note]  
> Bu eylem yalnızca sürücülerin **otomatik olarak Uygula** görev dizisi adımını kullanarak yüklenmesini engeller.

#### <a name="enable"></a>Etkinleştirme
, İşletim sistemini dağıtırken istemci bilgisayarlarının ve Görev sıralarının cihaz sürücüsünü yüklemesine Configuration Manager sağlar.

#### <a name="move"></a>Taşı
Cihaz sürücüsünü **Sürücüler** düğümünde başka bir klasöre taşır.

#### <a name="properties"></a>Özellikler
**Özellikler** iletişim kutusunu açar. Sürücünün özelliklerini gözden geçirin ve değiştirin. Örneğin, adını ve açıklamasını değiştirin, etkinleştirin veya devre dışı bırakın ve hangi platformların çalıştırılabileceği belirtin.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a>Sürücüleri yüklemek için görev dizilerini kullanma  

İşletim sisteminin nasıl dağıtıldığını otomatikleştirmek için görev dizilerini kullanın. Görev dizisindeki her adım, bir sürücü yükleme gibi belirli bir eylemi gerçekleştirebilir. Bir işletim sistemini dağıtırken aygıt sürücülerini yüklemek için aşağıdaki iki görev dizisi adımını kullanabilirsiniz:  

- [Sürücüleri Otomatik Uygula](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Bu adım, bir işletim sistemi dağıtımının parçası olarak cihaz sürücülerini otomatik olarak eşleştirmenizi ve yüklemenizi sağlar. Algılanan her bir donanım aygıtı için yalnızca en iyi eşleşen sürücüyü yüklemek üzere görev dizisi adımını yapılandırabilirsiniz. Alternatif olarak, adımın algılanan her bir donanım aygıtı için tüm uyumlu sürücüleri yüklemesini ve sonra en iyi sürücüyü Windows Kurulumu seçmesini sağlayabilirsiniz. Ayrıca, bu adım için kullanılabilir olan sürücüleri sınırlandırmak için bir sürücü kategorisi belirtebilirsiniz.  

- [Sürücü Paketini Uygula](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Bu adım, belirli bir sürücü paketinde bulunan tüm cihaz sürücülerini Windows Kurulumu için kullanılabilir kılmanızı sağlar. Windows Kurulumu belirlenen sürücü paketlerinde, gerekli olan aygıt sürücülerini arar. Tek başına medya oluşturduğunuzda tüm aygıt sürücülerini yüklemek için bu adımı kullanmalısınız.  

Bu görev dizisi adımlarını kullandığınızda, sürücülerin işletim sistemini dağıttığınız bilgisayara nasıl yükleneceğini de belirtebilirsiniz. Daha fazla bilgi için bkz. [görevleri otomatikleştirmek için görev dizilerini yönetme](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a>Sürücü raporları  

Sürücü kataloğundaki cihaz sürücüleriyle ilgili genel bilgileri belirlemek için **Sürücü Yönetimi** rapor kategorisindeki birkaç raporu kullanabilirsiniz. Raporlar hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).

