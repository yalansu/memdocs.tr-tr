---
title: İşletim sistemi yüklemek için görev dizisi oluşturma
titleSuffix: Configuration Manager
description: Bir işletim sistemi görüntüsünü ve diğer içeriği hedef bilgisayara otomatik olarak yüklemek için Configuration Manager görev dizilerini kullanın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e1b298856edea3f81cab2e9cd5ab75af49dff51
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723015"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>İşletim sistemi yüklemek için görev dizisi oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir işletim sistemi görüntüsünü bir hedef bilgisayara otomatik olarak yüklemek için Configuration Manager görev dizilerini kullanın. Hedef bilgisayarı başlatmak için kullanılan önyükleme görüntüsüne, hedef bilgisayara yüklemek istediğiniz işletim sistemi görüntüsüne ve yüklemek istediğiniz diğer uygulamalar veya yazılım güncelleştirmeleri gibi diğer ek içeriklere başvuruda bulunan bir görev dizisi oluşturabilirsiniz. Ardından görev dizisini, hedef bilgisayarı içeren koleksiyona dağıtın.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a>İşletim sistemini yüklemek için görev dizisi oluşturma

Ortamınızdaki bilgisayarlara bir işletim sistemi dağıtmak için birden çok senaryo vardır. Çoğu durumda, görev dizisi oluşturma Sihirbazı 'nda bir görev dizisi oluşturun ve **var olan bir görüntü paketini yükler** ' i seçin. Bu seçenek, işletim sistemini yükleyen, Kullanıcı ayarlarını geçirirken, yazılım güncelleştirmelerini uygulayan ve Uygulamaları yükleyen bir görev sırası oluşturur.

### <a name="prerequisites"></a>Ön koşullar

Bir işletim sistemini yüklemek için bir görev dizisi oluşturmadan önce, aşağıdaki gereksinimlerin yerinde olması gerekir:

#### <a name="required"></a>Gerekli

- [Önyükleme görüntüsü](../get-started/manage-boot-images.md)  

- Bir [Işletim sistemi görüntüsü](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Gerekli (kullanılıyorsa)

- [Yazılım güncelleştirmelerini](../../sum/get-started/synchronize-software-updates.md) eşitler  

- [Uygulama](../../apps/deploy-use/create-applications.md) Ekle  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>İşletim sistemini yükleyen bir görev dizisi oluşturma işlemi  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası oluştur**' u seçin. Bu eylem görev sırası oluşturma Sihirbazı 'Nı başlatır.  

3. **Yeni görev sırası oluştur** sayfasında, **var olan bir görüntü paketini yüklensin**' i seçin ve ardından **İleri**' yi seçin.  

4. **Görev sırası bilgileri** sayfasında, aşağıdaki ayarları belirtin:  

    - **Görev dizisi adı**: Görev dizisini tanımlayan adı belirtin.  

    - **Açıklama**: görev dizisinin ne yaptığını belirten bir açıklama belirtin.  

    - **Önyükleme görüntüsü**: görev dizisinin işletim sistemini hedef bilgisayara yüklemek için kullandığı önyükleme görüntüsünü belirtin. Önyükleme görüntüsü, bir Windows PE sürümü ve ek gerekli cihaz sürücüleri içerir. Daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        > Önyükleme görüntüsü, hedef bilgisayarın donanım mimarisiyle uyumlu olmalıdır.  

5. Windows 'u **yükler** sayfasında, aşağıdaki ayarları belirtin:  

    - **Görüntü paketi**: yüklenecek işletim sistemi görüntüsünü içeren paketi belirtin. Daha fazla bilgi için bkz. [OS görüntülerini yönetme](../get-started/manage-operating-system-images.md).  

    - **Görüntü**: işletim sistemi görüntü paketinde birden çok görüntü varsa, yüklenecek işletim sistemi görüntüsünün dizinini belirtin.  

    - **İşletim sistemini yükleyen hedef bilgisayarı bölümle ve biçimlendirin**: görev dizisinin işletim sistemini yüklemeden önce hedef bilgisayarı bölümleyip biçimlendirmesini isteyip istemediğinizi belirtin.  

    - **Ürün anahtarı**: gerekirse Windows ürün anahtarını belirtin. Kodlanmış toplu lisans anahtarlarını ve standart ürün anahtarlarını belirtebilirsiniz. Kodsuz bir ürün anahtarı kullanırsanız, beş karakterlik her grup bir tire () ile ayrılmalıdır `-` . Örneğin: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Sunucu lisanslama modu**: Sunucu lisansının **Bilgisayar başına**, **Sunucu başına**olup olmadığını veya lisans belirtilmediğini belirtir. Sunucu lisansı **Sunucu başına**ise maksimum sunucu bağlantısı sayısını da belirtin.  

    - Yeni işletim sistemi için yönetici hesabının nasıl işleneceğini belirtin:  

        - **Yerel yönetici hesabı parolasını rastgele oluşturun ve tüm desteklenen platformlarda hesabı devre dışı bırakın (önerilir)**: Windows, görev sırası işletim sistemi görüntüsünü dağıtduktan sonra yerel yönetici hesabını devre dışı bırakır.  

        - **Hesabı etkinleştirin ve yerel yönetici parolasını belirtin**: Windows, görev dizisinin işletim sistemi görüntüsünü dağıttığı tüm bilgisayarlarda yerel yönetici hesabı için aynı parolayı kullanır.  

6. **Ağı Yapılandır** sayfasında, aşağıdaki ayarları belirtin:  

    - **Çalışma grubuna katıl**: hedef bilgisayarı bir çalışma grubuna ekleyin.  

    - **Etki alanına katılarak**: hedef bilgisayarı bir etki alanına ekleyin. **Etki Alanı**'nda etki alanının adını belirtin.  

        > [!IMPORTANT]  
        > Yerel ormandaki etki alanlarını bulmak üzere göz atabilirsiniz ancak uzaktaki bir orman için etki alanı adını belirtmelisiniz.  

        Ayrıca, **etki alanı OU** alanında bir kuruluş BIRIMI (OU) belirtebilirsiniz. Bu ayar isteğe bağlıdır ve OU 'nun LDAP X. 500 ayırt edici adını belirtir. Henüz yoksa, Windows bu OU 'da bilgisayar hesabını oluşturur.  

    - **Hesap**: belirtilen etki alanına katma izinleri olan hesabın Kullanıcı adı ve parolası. Örneğin: *etki alanı\kullanıcı* veya *%değişken%*.  

        > [!IMPORTANT]  
        > Etki alanı ayarlarını ya da çalışma grubu ayarlarını geçirmeyi planlıyorsanız, uygun etki alanı kimlik bilgilerini girin.  

7. **Configuration Manager yüklemek** sayfasında, hedef bilgisayara yüklemek için Configuration Manager istemci paketini belirtin. Ayrıca, herhangi bir yükleme özelliği de ekleyebilirsiniz.  

8. **Durum geçişi** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Kullanıcı ayarlarını yakala**: görev sırası, Kullanıcı durumunu yakalar. Kullanıcı durumunu yakalama ve geri yükleme hakkında daha fazla bilgi için bkz. [Kullanıcı durumunu yönetme](../get-started/manage-user-state.md).  

    - **Ağ ayarlarını yakala**: görev dizisi, hedef bilgisayardan ağ ayarlarını yakalar. Ağ bağdaştırıcısı ayarlarının yanı sıra etki alanı veya çalışma grubunun üyeliğini yakalar.  

    - **Microsoft Windows ayarlarını yakala**: görev dizisi, işletim sistemi görüntüsünü yüklemeden önce hedef bilgisayardan Windows ayarlarını yakalar. Bilgisayar adını, kayıtlı Kullanıcı ve kuruluş adını ve saat dilimi ayarlarını yakalar.  

9. **Güncelleştirmeleri dahil et** sayfasında, gerekli yazılım güncelleştirmelerinin, tüm yazılım güncelleştirmelerinin mi yükleneceğini, yoksa yazılım güncelleştirmelerinin mi yükleneceğini belirtin. Yazılım güncelleştirmelerini yüklemeyi belirtirseniz Configuration Manager, yalnızca hedef bilgisayarın üyesi olduğu koleksiyonları hedefleyen yazılım güncelleştirmelerini yükler.  

10. **Uygulamaları yüklemek** sayfasında, hedef bilgisayara yüklenecek uygulamaları belirtin. Birden çok uygulamayı belirlerseniz, belirli bir uygulamanın yüklemesinin başarısız olmasına karşı, görev dizisinin devam etmesini de belirtebilirsiniz.  

11. Sihirbazı tamamlayın.  

Artık görev dizisini bilgisayar koleksiyonlarına dağıtabilirsiniz. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Ön önbellek içeriği

<!--4224642-->
Sürüm 1906 ' den başlayarak, içeriği önceden önbelleğe almak için bu tür bir görev dizisini etkinleştirebilirsiniz. Kullanılabilir görev dizileri dağıtımları için ön önbellek özelliği, istemcilerin görev dizisini yüklemeden önce ilgili içeriği indirmelerini sağlar.  

Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a>Örnek görev dizisi

Mevcut bir görüntüyü kullanarak işletim sistemi dağıtan bir görev dizisi oluştururken kılavuz olarak aşağıdaki tabloyu kullanın. Tablo, görev dizisi adımlarınız için genel sıraya ve bu görev dizisi adımlarının mantıksal gruplar halinde nasıl düzenleneceğine karar vermenize yardımcı olur. Oluşturduğunuz görev dizisi bu örnekten farklı olabilir ve daha fazla veya daha az görev dizisi adımı ve grubu içerebilir.  

> [!NOTE]  
> Bu görev dizisini oluşturmak için görev dizisi oluşturma Sihirbazı 'Nı kullanın.  
>
> Bu yeni görev dizisini oluşturmak için görev dizisi oluşturma Sihirbazı 'Nı kullandığınızda, bazı adım adları, bu görev dizisi adımlarını var olan bir görev dizisine el ile ekledikleriniz dışında farklı olur.

|Görev dizisi grubu veya adımı|Açıklama|  
|---------------------------------|-----------------|  
|Dosya ve ayarları yakala- **(yeni görev dizisi grubu)**|Bir görev dizisi grubu oluşturun. Görev dizisi grubu, benzer görev dizisi adımlarını daha iyi düzenleme ve hata denetimi için bir arada tutar.<br /><br /> Bu grup, bir başvuru bilgisayarının işletim sistemindeki dosyaları ve ayarları yakalamak için gerekli olan adımları içerir.|  
|Windows Ayarlarını Yakala|Başvuru bilgisayarından yakalanacak Microsoft Windows ayarlarını belirlemek için bu görev dizisi adımını kullanın. Bilgisayar adını, kullanıcı ve kuruluş bilgilerini ve saat dilimi ayarlarını yakalayabilirsiniz.|  
|Ağ ayarlarını yakala|Başvuru bilgisayarındaki ağ ayarlarını yakalamak için bu görev dizisi adımını kullanın. Başvuru bilgisayarının etki alanı veya çalışma grubu üyeliği ile ağ bağdaştırıcısı ayar bilgisini yakalayabilirsiniz.|  
|Kullanıcı dosyalarını ve ayarlarını yakala- **(yeni görev dizisi alt grubu)**|Görev dizisi grubu içinde bir görev dizisi grubu oluşturun. Bu alt grup, kullanıcı durumu verilerini yakalamak için gerekli olan adımları içerir. Bu alt grup, eklediğiniz ilk gruba benzer şekilde, daha iyi düzenleme ve hata denetimi için benzer görev dizisi adımlarını bir arada tutar.|  
|Kullanıcı Durumu Depolama Alanını İste|Kullanıcı durumu verilerinin depolandığı durum geçiş noktasına erişim istemek için bu görev dizisi adımını kullanın. Bu görev dizisi adımını, kullanıcı durumu bilgilerini yakalayacak veya geri yükleyecek şekilde yapılandırabilirsiniz.|  
|Kullanıcı Dosyalarını ve Ayarlarını Yakala|Kullanıcı durumunu ve bu görev adımı ile ilişkilendirilen görev dizisini alacak başvuru bilgisayarından Kullanıcı durumu ve ayarlarını yakalamak için bu görev dizisi Kullanıcı Durumu Taşıma Aracı adımını kullanın. Standart seçenekleri yakalayabilir veya hangi seçeneklerin yakalanacağını yapılandırabilirsiniz.|  
|Kullanıcı Durumu Depolama Alanını Serbest Bırak|Durum geçiş noktasına yakalama veya geri yükleme eyleminin tamamlandığını bildirmek için bu görev dizisi adımını kullanın.|  
|Işletim sistemini Kur- **(yeni görev dizisi grubu)**|Başka bir görev dizisi alt grubu oluşturun. Bu alt grup, Windows PE ortamını yüklemek ve yapılandırmak için gerekli olan adımları içerir.|  
|Windows PE'de yeniden başlat|Bu görev dizisini alan hedef bilgisayar için yeniden başlatma seçeneklerini belirtmek amacıyla bu görev dizisi adımını kullanın. Bu adım, kullanıcıya yüklemenin devam edebilmesi için bilgisayarın yeniden başlatılacağını bildiren bir ileti gösterir.<br /><br /> Bu adım salt okunur **_SMSTSInWinPE** görev dizisi değişkenini kullanır. İlişkili değer **false** ise görev dizisi adımı devam eder.|  
|Diski Bölümle 0|Bu görev dizisi adımı, hedef bilgisayardaki sabit sürücünün biçimlendirilmesi için gerekli olan eylemleri belirtir. Varsayılan disk numarası **0**'dır.<br /><br /> Bu adım salt okunur **_SMSTSClientCache** görev dizisi değişkenini kullanır. Configuration Manager istemci önbelleği yoksa bu adım çalışır.|  
|İşletim Sistemini Uygula|İşletim sistemi görüntüsünü hedef bilgisayara yüklemek için bu görev dizisi adımını kullanın. Bu adım öncelikle birimdeki tüm dosyaları siler, Configuration Manager özgü denetim dosyaları hariç. Ardından, WıM dosyasında bulunan tüm birim görüntülerini hedef bilgisayarda karşılık gelen sıralı disk birimine uygular. Bir **sysprep** yanıt dosyası belirtebilir ve ayrıca yükleme için kullanılacak olan disk bölümünü yapılandırabilirsiniz.|  
|Windows Ayarlarını Uygula|Hedef bilgisayar için Windows ayarları yapılandırma bilgilerini yapılandırmak üzere bu görev dizisi adımını kullanın. Kullanıcı ve kuruluş bilgileri, ürün veya lisans anahtarı bilgileri, saat dilimi ve yerel yönetici parolası gibi Windows ayarlarını uygulayabilirsiniz.|  
|Ağ Ayarlarını Uygula|Hedef bilgisayar için ağ veya çalışma grubu yapılandırma bilgilerini belirtmek üzere bu görev dizisi adımını kullanın. Aynı zamanda, bilgisayarın bir DHCP sunucusu kullanacağını belirtebilir veya IP adresi bilgilerini statik olarak atayabilirsiniz.|  
|Aygıt Sürücülerini Uygula|İşletim sistemi dağıtımının parçası olarak sürücüleri yüklemek için bu görev dizisi adımını kullanın. **Tüm kategorilerden sürücüleri dikkate al** ’ı seçerek Windows Kurulumu’nun var olan tüm sürücü kategorilerini aramasına izin verebilir veya **Sürücü eşleştirmesini yalnızca seçilen kategorilerdeki sürücüler dikkate alınacak şekilde sınırlandır**’ı seçerek Windows Kurulumu’nun hangi sürücü kategorilerini arayacağını sınırlandırabilirsiniz.<br /><br /> Bu adım salt okunur **_SMSTSMediaType** görev dizisi değişkenini kullanır. Bu görev dizisi adımı yalnızca değişkenin değeri **FullMedia**değerine eşit değilse çalışır.|  
|Sürücü Paketini Uygula|Bir sürücü paketindeki tüm cihaz sürücülerini Windows kurulumu tarafından kullanılabilir hale getirmek için bu görev dizisi adımını kullanın.|  
|Işletim sistemini Kur- **(yeni görev dizisi grubu)**|Başka bir görev dizisi alt grubu oluşturun. Bu alt grup, yüklü işletim sistemini kurmak için gerekli olan adımları içerir.|  
|Windows'u ve ConfigMgr'yi Kur|Configuration Manager istemci yazılımını yüklemek için bu görev dizisi adımını kullanın. Configuration Manager, Configuration Manager istemci GUID 'sini yükleyip kaydeder. Gerekli yükleme parametrelerini **yükleme özellikleri** penceresine atayabilirsiniz.|  
|Güncelleştirmeleri Yükle|Yazılım güncelleştirmelerinin hedef bilgisayara nasıl yüklendiğini belirtmek için bu görev dizisi adımını kullanın. Bu görev dizisi adımı çalıştırılıncaya kadar hedef bilgisayar ilgili yazılım güncelleştirmeleri için değerlendirilmez. Bu noktada, hedef bilgisayar, diğer Configuration Manager yönetilen istemcilere benzer yazılım güncelleştirmeleri için değerlendirilir.<br /><br /> Bu adım salt okunur **_SMSTSMediaType** görev dizisi değişkenini kullanır. Bu görev dizisi adımı yalnızca değişkenin değeri **FullMedia**değerine eşit değilse çalışır.|  
|Kullanıcı dosyalarını ve ayarlarını geri yükle- **(yeni görev dizisi alt grubu)**|Başka bir görev dizisi alt grubu oluşturun. Bu alt grup, kullanıcı dosyaları ile ayarlarını geri yüklemek için gerekli olan adımları içerir.|  
|Kullanıcı Durumu Depolama Alanını İste|Kullanıcı durumu verilerinin depolandığı durum geçiş noktasına erişim istemek için bu görev dizisi adımını kullanın.|  
|Kullanıcı Dosyalarını ve Ayarlarını Geri Yükle|Kullanıcı durumu ve ayarlarını bir hedef bilgisayara geri yüklemek için Kullanıcı Durumu Taşıma Aracı (USMT) çalıştırmak için bu görev dizisi adımını kullanın.|  
|Kullanıcı Durumu Depolama Alanını Serbest Bırak|Bu görev dizisi adımını durum geçiş noktasına kullanıcı durum verilerine artık gerek olmadığını bildirmek için kullanın.|  
