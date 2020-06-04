---
title: Dağıtım noktalarını yönet
titleSuffix: Configuration Manager
description: Dağıtım noktalarını, aygıtlara ve kullanıcılara dağıttığınız içeriği barındırmak için kullanın.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1d93dd446a65fda0b259bb10e0c944780d41059
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347100"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Configuration Manager dağıtım noktalarını yükleyip yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Cihazlara ve kullanıcılara dağıttığınız içerik dosyalarını barındırmak için Configuration Manager dağıtım noktaları yükleyebilirsiniz. Dağıtım noktalarını yönetmeyi ve dağıtım noktalarına içerik dağıtmayı kolaylaştırmak için dağıtım noktası grupları oluşturun.  

Yükleme Sihirbazı 'nı kullanarak *Yeni bir dağıtım noktası yüklersiniz* . Daha fazla bilgi için bkz. [dağıtım noktası yüklemesi](#bkmk_install). *Var olan bir dağıtım noktasının özelliklerini yönetmek*için dağıtım noktasının özelliklerini düzenleyin. Daha fazla bilgi için bkz. [dağıtım noktası yapılandırma](#bkmk_configs).

Her iki yöntemle de dağıtım noktası ayarlarının çoğunu yapılandırın. Birkaç ayar yalnızca yüklerken veya düzenlenirken kullanılabilir ancak her ikisini de kullanamazsınız:  

- Yalnızca bir dağıtım noktası yüklerken kullanılabilir olan ayarlar:  

    - **Dağıtım noktası bilgisayarında Configuration Manager IIS yüklemesine izin ver**

    - **Dağıtım noktası için sürücü alanı ayarlarını yapılandırma**  

- Yalnızca bir dağıtım noktasının özelliklerini düzenlediğinizde kullanılabilir ayarlar:  

    - **Dağıtım noktası grubu ilişkilerini yönetme**  

    - **Dağıtım noktasına dağıtılan Içeriği görüntüle**  

    - **Dağıtım noktalarına veri aktarımları için hız sınırlarını yapılandırın**  

    - **Dağıtım noktalarına veri aktarımları için zamanlamaları yapılandırma**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a>Dağıtım noktası yükler  

İçerik istemci bilgisayarlar için kullanılabilir hale gelmeden önce dağıtım noktası olarak bir site sistem sunucusu seçin. Şirket içi istemci bilgisayarları, bu dağıtım noktasını içerik kaynağı konumu olarak kullanabilmeniz için en az bir [sınır grubuna](boundary-groups.md#distribution-points) bir dağıtım noktası atayın. Dağıtım noktası rolünü yeni bir site sistemi sunucusuna ekleyin veya var olan bir site sistemi sunucusuna ekleyin.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a>Kaynakları

Yeni bir dağıtım noktası yüklediğinizde, kullanılabilir ayarlar boyunca size kılavuzluk eden bir yükleme sihirbazı kullanın. Başlamadan önce, aşağıdaki önkoşulları göz önünde bulundurun:  

- Bir dağıtım noktası oluşturmak ve yapılandırmak için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:  

    - **Dağıtım noktası** nesnesi için **Oku**  

    - **Dağıtım noktası** nesnesi Için **dağıtım noktasına Kopyala**  

    - **Site** nesnesi için **Değiştir**  

    - **Site** nesnesi Için **Işletim sistemi dağıtımı sertifikalarını yönetme**  

- Dağıtım noktasını barındıran Windows Server üzerinde Internet Information Services (IIS) ' yi yükler. Ya da, site sistem rolünü yüklediğinizde Configuration Manager IIS 'yi sizin için yükleyebilir ve yapılandırabilir.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a>Dağıtım noktası yüklemek için yordam  

Yeni bir dağıtım noktası eklemek için bu yordamı kullanın. Var olan bir dağıtım noktasının yapılandırmasını değiştirmek için [dağıtım noktası yapılandırma](#bkmk_configs) bölümüne bakın.  

[Site sistem rollerini yüklemek](install-site-system-roles.md)için genel prosedürü kullanmaya başlayın. Site sistemi sunucusu oluşturma Sihirbazı ' nın **sistem rolü seçimi** sayfasında **dağıtım noktası** rolünü seçin. Bu eylem, sihirbaza aşağıdaki sayfaları ekler:  

- [Dağıtım noktası](#bkmk_config-general)
- [İletişim](#bkmk_config-comm)
- [Sürücü Ayarları](#bkmk_config-drive)
- [Çekme dağıtım noktası](#bkmk_config-pull)
- [PXE ayarları](#bkmk_config-pxe)
- [Noktalı](#bkmk_config-multicast)
- [İçerik Doğrulaması](#bkmk_config-valid)
- [Sınır grupları](#bkmk_config-boundary)

> [!Important]  
> Aşağıdaki ayarlar yalnızca bir dağıtım noktası yüklerken kullanılabilir:  
>
> - **Dağıtım noktası bilgisayarında Configuration Manager IIS yüklemesine izin ver**  
>
> - **Dağıtım noktası için sürücü alanı ayarlarını yapılandırma**  

Sihirbazın dağıtım noktası rolüne özgü sayfaları hakkında daha fazla bilgi için [dağıtım noktası yapılandırma](#bkmk_configs) bölümüne bakın. Örneğin, dağıtım noktasını bir [çekme dağıtım noktası](#bkmk_config-pull)olarak yüklemek istiyorsanız, **Bu dağıtım noktasının diğer dağıtım noktalarından Içerik çekmesini etkinleştir**seçeneğini belirleyin. Ardından, çekme dağıtım noktalarının gerektirdiği ek konfigürasyonları yapın.  

Site sistemi sunucusu oluşturma Sihirbazı 'nı tamamladıktan sonra site, dağıtım noktası rolünü site sistem sunucusuna ekler.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a>Dağıtım noktası gruplarını yönetme  

Dağıtım noktası grupları içerik dağıtımı için dağıtım noktalarına mantıksal bir gruplama sağlar. Birden çok siteye yayılan dağıtım noktaları için merkezi bir konumdan içerik yönetmek ve izlemek için bu grupları kullanın. Aşağıdaki noktayı aklınızda bulundurun:

- Hiyerarşideki herhangi bir siteden bir dağıtım noktası grubuna bir veya daha fazla dağıtım noktası ekleyin.  

- Birden fazla dağıtım noktası grubuna bir dağıtım noktası ekleyin.  

- Bir dağıtım noktası grubuna içerik dağıttığınızda, Configuration Manager içeriği grubun üyesi olan tüm dağıtım noktalarına dağıtır.  

- İlk içerik dağıtımı sonrasında gruba bir dağıtım noktası eklerseniz, Configuration Manager içeriği otomatik olarak yeni dağıtım noktası üyesine dağıtır.  

- Bir koleksiyonu bir dağıtım noktası grubuyla ilişkilendirin. İçeriği bu koleksiyona dağıttığınızda, Configuration Manager koleksiyon ile hangi grupların ilişkilendirildiğini belirler. Daha sonra içeriği bu grupların üyesi olan tüm dağıtım noktalarına dağıtır.  

    > [!NOTE]  
    > İçeriği bir koleksiyona dağıttıktan sonra, koleksiyonu yeni bir dağıtım noktası grubuyla ilişkilendirirseniz, içerik yeni dağıtım noktası grubuna dağıtılmadan önce içeriği koleksiyona yeniden dağıtmanız gerekir.  

Sonraki bölümlerde dağıtım noktası gruplarını yönetmek için aşağıdaki eylemlerin yordamları listelenmektedir:  

- [Yeni bir dağıtım noktası grubu oluşturma ve yapılandırma](#bkmk_dpgroup-create)
- [Var olan bir dağıtım noktası grubunu değiştirme](#bkmk_dpgroup-modify)
- [Seçili dağıtım noktalarını mevcut dağıtım noktası gruplarına Ekle](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a>Yeni bir dağıtım noktası grubu oluşturma ve yapılandırma yordamı  

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktası grupları** düğümünü seçin.  

2. Şeritte **Grup Oluştur**' u seçin.  

3. Yeni dağıtım noktası grubu Oluştur penceresinde, grup için **ad**ve isteğe bağlı olarak bir **Açıklama** girin.  

4. **Üyeler** sekmesinde **Ekle**' yi seçin.  

5. Dağıtım noktaları Ekle penceresinde, grubun üyesi olarak eklemek için bir veya daha fazla dağıtım noktası seçin. Ardından **Tamam**' ı seçin.  

6. Gerekirse, yeni dağıtım noktası grubu oluştur penceresinin **koleksiyonlar** sekmesine geçin ve **Ekle**' yi seçin.  

7. Koleksiyonları Seç penceresinde, dağıtım noktası grubuyla ilişkilendirilecek koleksiyonları seçin ve ardından **Tamam**' ı seçin.  

8. Yeni dağıtım noktası grubu Oluştur penceresinde, grubu oluşturmak için **Tamam** ' ı seçin.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Var olan bir dağıtım noktasından yeni bir grup oluştur

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin. Yeni bir dağıtım noktası grubuna eklemek için bir veya daha fazla dağıtım noktası seçin.  

2. Şeritte **Seçili öğeleri ekle**' yi seçin ve ardından **Seçili öğeleri yeni dağıtım noktası grubuna ekle**' yi seçin.  

Bu işlem, yeni dağıtım noktası grubu oluştur penceresinin **Üyeler** sekmesini seçili sunucularla otomatik olarak doldurur.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a>Var olan bir dağıtım noktası grubunu değiştirme yordamı  

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktası grupları** düğümünü seçin.  

2. Değiştirilecek var olan bir dağıtım noktası grubunu seçin. Şeritte **Özellikler**' i seçin.  

3. Yeni koleksiyonları bu grupla ilişkilendirmek için **koleksiyonlar** sekmesine geçin ve **Ekle**' yi seçin. Koleksiyonları seçin ve ardından **Tamam**' ı seçin.  

4. Bu gruba yeni dağıtım noktaları eklemek için, **Üyeler** sekmesine geçin ve **Ekle**' yi seçin. Dağıtım noktalarını seçin ve ardından **Tamam**' ı seçin.  

5. Değişiklikleri dağıtım noktası grubuna kaydetmek için **Tamam ' ı** seçin.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a>Mevcut dağıtım noktası gruplarına Seçili dağıtım noktalarını ekleme yordamı  

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin. Var olan bir gruba eklemek için bir veya daha fazla dağıtım noktası seçin.  

2. Şeritte **Seçili öğeleri ekle**' yi seçin ve ardından **Seçili öğeleri mevcut dağıtım noktası gruplarına Ekle**' yi seçin.  

3. **Kullanılabilir dağıtım noktası grupları**' nda, seçilen dağıtım noktalarının üye olarak eklendiği grupları seçin. Ardından **Tamam**' ı seçin.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a>Dağıtım noktasını yeniden atama

<!-- 1306937 -->

Birçok müşterinin büyük Configuration Manager altyapıları vardır ve bunların ortamlarını basitleştirmek için birincil veya ikincil siteleri azaltmaktadır. Ayrıca, yönetilen istemcilere içerik sağlamak için şube konumlarında dağıtım noktalarını korumaları gerekir. Bu dağıtım noktaları genellikle birden çok terabayt veya daha fazla içerik içerir. Bu içerik, bu uzak sunuculara dağıtılacak zaman ve ağ bant genişliği açısından maliyetlidir.

Bu özellik, içeriği yeniden dağıtmadan bir dağıtım noktasını başka bir birincil siteye yeniden atamanıza olanak tanır. Bu eylem, sunucudaki tüm içeriği kalıcı hale yaparken site sistem atamasını güncelleştirir. Birden çok dağıtım noktasını yeniden atamanız gerekiyorsa, önce bu eylemi tek bir dağıtım noktasında gerçekleştirin. Daha sonra aynı anda ek sunucularla devam edin.

> [!IMPORTANT]  
> Hedef sunucu yalnızca dağıtım noktası rolünü barındırabilirler. Site sistemi sunucusu durum geçiş noktası gibi başka bir Configuration Manager sunucu rolü barındırıyorsa, dağıtım noktasını yeniden atayamazsınız. Bir bulut dağıtım noktasını yeniden atayamazsınız.

Bir dağıtım noktasını yeniden atamak için, hedef site sunucusunun bilgisayar hesabını hedef dağıtım noktası sunucusundaki yerel yönetici grubuna ekleyin.

Bir dağıtım noktasını yeniden atamak için aşağıdaki adımları izleyin:

1. Configuration Manager konsolunda, merkezi yönetim sitesine bağlanın.  

2. **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin.  

3. Hedef dağıtım noktasına sağ tıklayın ve **dağıtım noktasını yeniden ata**' yı seçin.  

4. Bu dağıtım noktasını yeniden atamak istediğiniz hedef site sunucusunu ve site kodunu seçin.  

Yeni bir rol eklediğinizde farklı şekilde yeniden atamayı izleyin. En basit yöntem, birkaç dakika sonra konsol görünümünü yenilekullanmaktır. Görünüme site kodu sütununu ekleyin. Bu değer, Configuration Manager sunucuyu yeniden işaretladığında değişir. Konsol görünümünü yenilemeden önce hedef sunucuda başka bir eylem gerçekleştirmeye çalışırsanız, "nesne bulunamadı" hatası oluşur. İşlemin tamamlandığından emin olun ve sunucudaki diğer eylemleri başlatmadan önce konsol görünümünü yenileyin.

Bir dağıtım noktasını yeniden atayarak, sunucunun sertifikasını yenileyin. Yeni site sunucusunun ortak anahtarını kullanarak bu sertifikayı yeniden şifrelemesi ve site veritabanında depolaması gerekir. Daha fazla bilgi için dağıtım noktası özelliklerinin [genel](#bkmk_config-general) sekmesindeki **dağıtım noktası için otomatik olarak imzalanan sertifika oluşturma veya ortak anahtar altyapısı (PKI) istemci sertifikasını içeri aktarma** bölümüne bakın.

- PKI sertifikaları için yeni bir sertifika oluşturmanız gerekmez. Aynısını içeri aktarın. PFX ve parolayı girin.  

- Otomatik olarak imzalanan sertifikalar için, güncelleştirmek üzere sona erme tarihi veya saatini ayarlayın.  

- Sertifikayı yenilemezseniz dağıtım noktası yine de içerik sunar, ancak aşağıdaki işlevler başarısız olur:  

    - İçerik doğrulama iletileri (Distmgr. log, sertifikanın şifresini çözemeyecek olduğunu gösterir)  

    - İstemciler için PXE desteği  

### <a name="tips"></a>İpuçları

- Bu eylemi merkezi yönetim sitesinden gerçekleştirin. Bu uygulama, birincil sitelere çoğaltmaya yardımcı olur.  

- İçeriği hedef sunucuya dağıtmayın ve sonra yeniden atamayı denemeyin. Devam eden içerik görevlerinin dağıtılması yeniden atama işlemi sırasında başarısız olabilir, ancak normal başına yeniden denemeler yapılır.  

- Sunucu ayrıca bir Configuration Manager istemcili, istemciyi yeni birincil siteye de yeniden atadıktan emin olun. Bu adım, içerik indirmek için istemci bileşenlerini kullanan çekme dağıtım noktaları için özellikle önemlidir.  

- Bu işlem, dağıtım noktasını eski sitenin varsayılan sınır grubundan kaldırır. Gerekirse, yeni sitenin varsayılan sınır grubuna el ile eklemeniz gerekir. Diğer tüm sınır grubu atamaları aynı kalır.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a>Bakım modu

<!--3555754-->

Sürüm 1902 ' den başlayarak, bakım modunda bir dağıtım noktası ayarlayabilirsiniz. Yazılım güncelleştirmelerini yüklerken veya sunucuda donanım değişiklikleri yaparken bakım modunu etkinleştirin.

Dağıtım noktası bakım modundayken aşağıdaki davranışlara sahiptir:

- Site herhangi bir içerik dağıtmaz.  

- Yönetim noktaları, bu dağıtım noktasının konumunu istemcilere döndürmez.

- Siteyi güncelleştirdiğinizde bakım modundaki bir dağıtım noktası hala güncellenir.

- Dağıtım noktası özellikleri salt okunurdur. Örneğin, sertifikayı değiştiremez veya sınır grupları ekleyemezsiniz.  

- İçerik doğrulama gibi herhangi bir zamanlanmış görev hala aynı zamanlamaya göre çalışır.

Birden fazla dağıtım noktasında bakım modunu etkinleştirme konusunda dikkatli olun. Bu eylem, diğer dağıtım noktalarınız için bir performans etkisi oluşmasına neden olabilir. Sınır grubu yapılandırmalarına bağlı olarak, istemciler indirme sürelerini artırabilir veya içerik indiremeyebilir.

Bakım modu, herhangi bir dağıtım noktası için uzun vadeli bir durum olmamalıdır. Uzun süreli herhangi bir eylem için önce dağıtım noktası rolünü kaldırmayı düşünün.

> [!NOTE]
> Dağıtım noktası bakım modundayken, aşağıdaki eylemleri yapmayın:<!-- SCCMDocs-pr #4699 -->
>
> - Rolü kaldır
> - Dağıtım noktasını yeniden ata

### <a name="enable-maintenance-mode"></a>Bakım modunu etkinleştirme

Dağıtım noktasını bakım moduna almak için, Kullanıcı hesabınız **site** sınıfında **değiştirme** iznine sahip olmalıdır. Örneğin, **Altyapı Yöneticisi** ve **tam yönetici** yerleşik rollerinin bu izni vardır.<!-- SCCMDocs-pr issue #3407 -->

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin.  

2. **Dağıtım noktaları** düğümünü seçin.  

3. Hedef dağıtım noktasını seçin ve şeritten **bakım modunu etkinleştir** ' i seçin.  

Dağıtım noktalarının geçerli durumunu görüntülemek için, "bakım modu" sütununu konsolundaki **dağıtım noktaları** düğümüne ekleyin.

Configuration Manager SDK ile bu işlemi otomatikleştirme hakkında daha fazla bilgi için, bkz. [SetDPMaintenanceMode Method in class SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a>Dağıtım noktası yapılandırma  

Tek tek dağıtım noktaları, çeşitli farklı yapılandırmaların tümünü destekler. Ancak, tüm dağıtım noktası türleri tüm konfigürasyonları desteklemez. Örneğin, bulut dağıtım noktaları PXE veya çok noktaya yayın özellikli dağıtımları desteklemez. Belirli sınırlamalar hakkında daha fazla bilgi için aşağıdaki makalelere bakın:  

- [Bulut dağıtım noktası kullan](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [İstek temelli dağıtım noktası kullanma](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

Aşağıdaki bölümlerde, [Yeni bir tane yüklerken](#bkmk_install-procedure) veya [mevcut bir tane düzenlenirken](#bkmk_change-procedure)dağıtım noktası yapılandırmalarının açıklaması verilmiştir:  

- [Genel ayarlar](#bkmk_config-general)
- [İletişim](#bkmk_config-comm)
- [Sürücü Ayarları](#bkmk_config-drive)
- [Güvenlik Duvarı ayarları](#bkmk_firewall)
- [Çekme dağıtım noktası](#bkmk_config-pull)
- [PXE ayarları](#bkmk_config-pxe)
- [Noktalı](#bkmk_config-multicast)
- [İçerik Doğrulaması](#bkmk_config-valid)
- [Sınır grupları](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a>Dağıtım noktasını değiştirme yordamı

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin.  

2. Yapılandırılacak dağıtım noktasını seçin. Şeritte **Özellikler**' i seçin.  

3. Dağıtım noktasının özelliklerini düzenlemekte olduğunuz sırada aşağıdaki bölümlerde bulunan bilgileri kullanın.  

4. İstediğiniz değişiklikleri yaptıktan sonra, ayarlarınızı kaydetmek ve dağıtım noktası özelliklerini kapatmak için **Tamam** ' ı seçin.  

### <a name="general"></a><a name="bkmk_config-general"></a>Genel  

> [!Note]  
> Sürüm 1902 ve önceki sürümlerde bu sayfada HTTP/HTTPS ve sertifikaları için ek ayarlar bulunur. Sürüm 1906 ' den başlayarak bu ayarlar artık [iletişim](#bkmk_config-comm) sayfasıdır.

Aşağıdaki ayarlar, site sistemi sunucusu oluşturma Sihirbazı 'nın **dağıtım noktası** sayfasında ve dağıtım noktası özellikleri penceresinin **genel** sekmesindedir:  

- **Açıklama**: Bu dağıtım noktası rolü için isteğe bağlı bir açıklama.  

- **Configuration Manager GEREKLIYSE IIS 'Yi yükleme ve yapılandırma**: IIS sunucuda zaten yüklü değilse, Configuration Manager yükler ve yapılandırır. Configuration Manager tüm dağıtım noktalarında IIS gerektirir. Bu ayarı seçemezsiniz ve IIS sunucuda yüklü değilse, önce Configuration Manager dağıtım noktasını başarıyla yükleyebilmesi için önce IIS 'yi yüklemeniz gerekir.  

    > [!NOTE]  
    > Bu seçenek yalnızca site sistemi sunucusu oluşturma sihirbazının **dağıtım noktası** sayfasında bulunur. Yalnızca [Yeni bir dağıtım noktası yüklerken](#bkmk_install-procedure)kullanılabilir.  

- **Bu dağıtım noktası Için BranchCache 'ı etkinleştir ve Yapılandır**: dağıtım noktası sunucusunda Windows branchcache 'i Configuration Manager izin vermek için bu ayarı seçin. Daha fazla bilgi için bkz. [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Kullanılmayan ağ bant genişliğini (Windows LEDBAT) kullanmak için indirme hızını ayarlayın**<!--1358112-->: Sürüm 1806 ' den başlayarak, ağ tıkanıklık denetimini kullanmak için dağıtım noktalarını etkinleştirin. Daha fazla bilgi için bkz. [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). LEDBAT desteği için minimum gereksinimler:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager sürüm 1806 (genel sürüm)  

        - Windows Server, sürüm 1709 veya üzeri  

    - Güncelleştirme paketi ile Configuration Manager sürüm 1806 (4462978) veya üzeri  

        - Windows Server, sürüm 1709 veya üzeri
        - Windows Server 2016 aşağıdaki güncelleştirmelerle:
           - Toplu güncelleştirme KB4132216, 21 Haziran 2018 veya sonraki bir toplu güncelleştirmedir.
           - Hizmet yığını güncelleştirme KB4284833, 18 Mayıs 2018 veya sonraki bir hizmet yığını güncelleştirmesi yayınlandı.

    - Configuration Manager sürüm 1810 veya üzeri:

        - Windows Server, sürüm 1709 veya üzeri
        - Windows Server 2016 aşağıdaki güncelleştirmelerle:
           - Toplu güncelleştirme KB4132216, 21 Haziran 2018 veya sonraki bir toplu güncelleştirmedir.
           - Hizmet yığını güncelleştirme KB4284833, 18 Mayıs 2018 veya sonraki bir hizmet yığını güncelleştirmesi yayınlandı.
        - Windows Server 2019  

- **Önceden hazırlanan içerik için bu dağıtım noktasını etkinleştir**: Bu ayar, yazılımı dağıtmadan önce sunucuya içerik eklemenizi sağlar. İçerik dosyaları zaten içerik kitaplığında olduğundan, yazılımı dağıtırken ağ üzerinden aktarılmaz. Daha fazla bilgi için bkz. [önceden hazırlanan içerik](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).  

- **Bu dağıtım noktasını Microsoft bağlı önbellek sunucusu olarak kullanılacak şekilde etkinleştirin**: sürüm 1906 ' den başlayarak, dağıtım noktalarınıza Microsoft bağlı önbellek sunucusu yükleyebilirsiniz. Bu içeriği şirket içinde önbelleğe alarak istemcileriniz teslim Iyileştirme özelliğinden yararlanabilir, ancak WAN bağlantılarını korumaya yardımcı olabilirsiniz. Ek ayarların açıklaması dahil daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a>Kurulan

> [!Note]  
> Sürüm 1906 ' den başlayarak, aşağıdaki ayarlar **iletişim** sekmesindedir. Sürüm 1902 ve önceki sürümlerde bu ayarlar [genel](#bkmk_config-general) sekmesinde yer alır.

Aşağıdaki ayarlar site sistemi sunucusu oluşturma Sihirbazı 'nın **iletişim** sayfasında ve dağıtım noktası özellikleri penceresinde bulunur:  

- **İstemci cihazların dağıtım noktasıyla nasıl iletişim kuracağını yapılandırın**: **http** veya **https**kullanmanın avantajları ve dezavantajları vardır. Daha fazla bilgi için bkz. [içerik yönetimi için En Iyi güvenlik uygulamaları](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

- **İstemcilerin anonim olarak bağlanmasına Izin ver**: Bu ayar, dağıtım noktasının Configuration Manager istemcilerinden içerik kitaplığına adsız bağlantılara izin verip vermeyeceğini belirtir.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Otomatik olarak imzalanan bir sertifika oluşturun veya BIR PKI istemci sertifikasını içeri aktarın**: Configuration Manager Bu sertifikayı aşağıdaki amaçlarla kullanır:  

    - Dağıtım noktası durum iletileri göndermeden önce bir yönetim noktasına dağıtım noktasının kimliğini doğrular.  

    - **PXE ayarları** sayfasında **istemciler Için PXE desteğini etkinleştirdiğinizde** , dağıtım noktası bunu PXE önyüklemesi yapan bilgisayarlara gönderir. Ardından bu bilgisayarlar, işletim sistemi dağıtım işlemi sırasında bir yönetim noktasına bağlanmak için kullanır.  

    HTTP için sitesindeki tüm yönetim noktalarınızı yapılandırdığınızda, **otomatik olarak imzalanan sertifika oluşturma**seçeneğini belirleyin. HTTPS için yönetim noktalarını yapılandırırken, sertifikayı PKI 'dan **Içeri aktarma** seçeneğini kullanın.  

    Sertifikayı içeri aktarmak için geçerli bir ortak anahtar şifreleme standardı (PKCS #12) dosyasına gidin. Bu PFX veya CER dosyası, Configuration Manager için aşağıdaki gereksinimlere sahip PKI sertifikasına sahiptir:  

    - Hedeflenen kullanım istemci kimlik doğrulamasını içerir  

    - Özel anahtarın verilmesini etkinleştir  

    > [!TIP]  
    > Sertifika konusu veya konu alternatif adı (SAN) için belirli gereksinimler yoktur. Gerekirse, birden fazla dağıtım noktası için aynı sertifikayı kullanın.  

    Sertifika gereksinimleri hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

    Bu sertifikanın örnek dağıtımı için bkz. [dağıtım noktaları için istemci sertifikasını dağıtma](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a>Sürücü Ayarları  

> [!NOTE]  
> Bu seçenekler yalnızca yeni bir dağıtım noktası yüklerken kullanılabilir.  

Dağıtım noktası için sürücü ayarlarını belirtin. İçerik kitaplığı ve paket paylaşımının iki disk sürücüsü için en fazla iki disk sürücüsü yapılandırın. Configuration Manager, ilk ikisi yapılandırılan sürücü alanına ulaştığında ek sürücüler kullanabilir. **Sürücü ayarları** sayfası, disk sürücüleri için önceliği ve her disk sürücüsünde kalan boş disk alanı miktarını yapılandırır.  

- **Ayrılan sürücü alanı (MB)**: Bu değer, Configuration Manager farklı bir sürücü seçmeden önce sürücüdeki boş alan miktarını belirler ve kopyalama işlemini o sürücüye devam ettirir. İçerik dosyaları birden çok sürücüye yayılabilir.  

- **İçerik konumları**: Bu dağıtım noktasındaki içerik kitaplığı ve paket paylaşımının konumlarını belirtin. Varsayılan olarak, tüm içerik konumları **Otomatik**olarak ayarlanır. Configuration Manager, boş alan miktarı **ayrılan sürücü alanı (MB)** için belirtilen değere ulaşana kadar içeriği birincil içerik konumuna kopyalar. **Otomatik**' i seçtiğinizde Configuration Manager birincil içerik konumlarını, yükleme sırasında en fazla disk alanına sahip disk sürücüsüne ayarlar. İkincil konumları, ikinci en fazla boş disk alanına sahip disk sürücüsüne ayarlar. Birincil ve ikincil konumlar ayrılan sürücü alanına ulaştığında, kopyalama işlemine devam etmek için en fazla boş disk alanına sahip başka bir kullanılabilir sürücü seçer Configuration Manager.  

> [!Tip]  
> Configuration Manager belirli bir sürücüye yüklenmesini engellemek için, **no_sms_on_drive. SMS** adlı boş bir dosya oluşturun ve dağıtım noktasını yüklemeden önce bu dosyayı sürücünün kök klasörüne kopyalayın.  

Daha fazla bilgi için bkz. [içerik kitaplığı](../../../plan-design/hierarchy/the-content-library.md).

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a>Güvenlik Duvarı ayarları

Dağıtım noktasında Windows güvenlik duvarında aşağıdaki gelen kurallar yapılandırılmış olmalıdır:

- Windows Yönetim Araçları (DCOM-In)
- Windows Yönetim Araçları (WMI-In)

Bu kurallar olmadan istemciler, içerik indirmeye çalışırken DataTransferService. log dosyasında 0x801901F4 hatası alır.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a>Çekme dağıtım noktası  

**Bu dağıtım noktasının diğer dağıtım noktalarından içerik çekmesini etkinleştirdiğinizde, bu**bir çekme dağıtım noktası haline gelir. Dağıtım noktasının, kendisine dağıttığınız içeriği alma davranışını değiştirirsiniz. Daha fazla bilgi için bkz. [çekme dağıtım noktası kullanma](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

Yapılandırdığınız her bir çekme dağıtım noktası için, içeriği aldığı bir veya daha fazla kaynak dağıtım noktası belirtin:  

- **Ekle**' yi seçin ve ardından kaynak olacak kullanılabilir dağıtım noktalarından birini veya birkaçını seçin.  

- Önceliği ayarlamak için ok düğmelerini kullanın. Çekme dağıtım noktası içeriği aktarmaya çalıştığında, öncelik, kaynak dağıtım noktalarıyla iletişim kurduğu sıradır. Önce en düşük değere sahip dağıtım noktalarıyla iletişim kurar.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a>PXE  

Dağıtım noktasında PXE 'nin etkinleştirilip etkinleştirilmeyeceğini belirtin. İstemcilerdeki işletim sistemi dağıtımlarını başlatmak için PXE 'yi kullanın. Configuration Manager 'de PXE kullanma hakkında daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

PXE 'yi etkinleştirdiğinizde Configuration Manager, gerekirse sunucuya Windows Dağıtım Hizmetleri 'ni (WDS) yüklerse. WDS, işletim sistemlerini yüklemek için PXE önyüklemesini gerçekleştiren hizmettir. Dağıtım noktasını oluşturmak için Sihirbazı tamamladıktan sonra, Configuration Manager WDS 'de PXE önyükleme işlevlerini kullanan bir sağlayıcı yükler.

Sürüm 1806 ' den başlayarak, WDS olmadan bir dağıtım noktasında PXE 'yi etkinleştirebilirsiniz.

**İstemciler IÇIN PXE desteğini etkinleştirme**seçeneğini belirleyin ve ardından aşağıdaki ayarları yapılandırın:  

> [!Note]  
> PXE 'yi etkinleştirmek istediğinizi onaylamak için **PXE Için gereken bağlantı noktalarını gözden geçirin** Iletişim kutusunda **Evet** ' i seçin. Configuration Manager, Windows güvenlik duvarında varsayılan bağlantı noktalarını otomatik olarak yapılandırır. Farklı bir güvenlik duvarı kullanıyorsanız, bağlantı noktalarını el ile yapılandırın.  
>
> WDS ve DHCP 'yi aynı sunucuya yüklerseniz, WDS 'yi farklı bir bağlantı noktasında dinlemek üzere yapılandırın. Varsayılan olarak, DHCP aynı bağlantı noktasını dinler. Daha fazla bilgi için bkz. [WDS ve DHCP’yi aynı sunucuda bulundurmayla ilgili önemli noktalar](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

- **Bu dağıtım noktasının gelen PXE isteklerine yanıt vermesine Izin ver**: WDS 'nin PXE hizmet isteklerine yanıt vermesi için etkinleştirilip etkinleştirilmeyeceğini belirtin. Dağıtım noktasından PXE işlevini kaldırmadan hizmeti etkinleştirmek ve devre dışı bırakmak için bu ayarı kullanın.  

- **Bilinmeyen bilgisayar desteğini etkinleştir**: Configuration Manager yönetmeyen bilgisayarlar için desteğin etkinleştirilip etkinleştirilmeyeceğini belirtin. Daha fazla bilgi için bkz. [bilinmeyen bilgisayar dağıtımları Için hazırlanma](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

- **Windows dağıtım hizmeti olmadan BIR PXE Yanıtlayıcıu etkinleştirme**: sürüm 1806 ' den başlayarak, bu seçenek DAĞıTıM noktasında WDS GEREKTIRMEYEN bir PXE Yanıtlayıcısı sağlar. Bu PXE Yanıtlayıcısı IPv6 ağlarını destekler. Bu seçeneği, zaten PXE özellikli olan bir dağıtım noktasında etkinleştirirseniz, Configuration Manager WDS hizmetini askıya alır. Bu seçeneği devre dışı bırakırsanız ancak **istemciler IÇIN PXE desteğini hala etkinleştirirseniz**, DAĞıTıM noktası WDS 'yi yeniden etkinleştirir.<!--1357580-->  

    > [!Note]  
    > Sürüm 1810 ve önceki sürümlerde, aynı zamanda bir DHCP sunucusu çalıştıran sunucularda WDS olmadan PXE Yanıtlayıcı 'yı kullanmak desteklenmez.
    >
    > Sürüm 1902 ' den başlayarak, bir dağıtım noktasında Windows dağıtım hizmeti olmadan bir PXE Yanıtlayıcı 'yı etkinleştirdiğinizde, artık DHCP hizmetiyle aynı sunucuda olabilir. <!--3734270-->  

- **BILGISAYARLAR PXE kullanırken parola iste**: PXE dağıtımlarınızda ek güvenlik sağlamak için güçlü bir parola belirtin.  

- **Kullanıcı cihaz benzeşimi**: DAĞıTıM noktasının PXE dağıtımları için kullanıcıları hedef bilgisayarla nasıl ilişkilendireceğini belirtin. Aşağıdaki seçeneklerden birini belirleyin:  

  - **Kullanıcı cihaz benzeşimine otomatik onay Ile Izin ver**: kullanıcıları hedef bilgisayarla onay beklemeden otomatik olarak ilişkilendirmek için bu ayarı seçin.  

  - **Kullanıcı cihaz benzeşimi bekleyen yönetici onayına Izin ver**: kullanıcılar hedef bilgisayarla ilişkilendirilmeden önce bir yönetici kullanıcıdan onay beklemek için bu ayarı seçin.  

  - **Kullanıcı cihaz benzeşimine izin verme**: kullanıcıların hedef bilgisayarla ilişkilendirilmediğinden emin olmak için bu ayarı seçin. Bu varsayılan ayardır.  

    Kullanıcı cihaz benzeşimi hakkında daha fazla bilgi için bkz. [Kullanıcı cihaz benzeşimi ile kullanıcıları ve cihazları bağlama](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

- **Ağ arabirimleri**: dağıtım noktasının tüm ağ arabirimlerinden veya belirli ağ arabirimlerinden PXE isteklerine yanıt verdiğini belirtin. Dağıtım noktası belirli ağ arabirimlerine yanıt verirse, her bir ağ arabirimi için MAC adresini sağlayın.  

    > [!Note]  
    > Ağ arabirimini değiştirirken, yapılandırmayı düzgün şekilde kaydettiğinden emin olmak için WDS hizmetini yeniden başlatın. Sürüm 1806 ' den başlayarak, PXE Yanıtlayıcı hizmetini kullanırken **CONFIGMGR PXE Yanıtlayıcı hizmeti** 'ni (sccmpxe) yeniden başlatın.<!--SCCMDocs issue 642-->  

- **PXE sunucusu yanıt gecikmesini (saniye) belirtin**: bırden fazla PXE sunucusu kullandığınızda, bu PXE 'yi destekleyen dağıtım noktasının bilgisayar isteklerine yanıt vermeden önce ne kadar beklemesi gerektiğini belirtin. Varsayılan olarak, Configuration Manager PXE 'yi destekleyen dağıtım noktası hemen yanıt verir.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a>Noktalı  

Dağıtım noktasında çok noktaya yayının etkinleştirilip etkinleştirilmeyeceğini belirtin. Çok noktaya yayın dağıtımları, eşzamanlı olarak birden çok Configuration Manager istemcisine veri göndererek ağ bant genişliğini korur. Sunucu çok noktaya yayın olmadan her bir istemciye verilerin bir kopyasını ayrı bir bağlantı üzerinden gönderir. İşletim sistemi dağıtımı için çok noktaya yayın kullanma hakkında daha fazla bilgi için bkz. [ağ üzerinden Windows dağıtmak için çok noktaya yayın kullanma](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)

Çok noktaya yayını etkinleştirdiğinizde, Configuration Manager gerekirse sunucuya Windows Dağıtım Hizmetleri 'ni (WDS) yüklenir.  

Çok **noktaya yayının birden çok istemciye eşzamanlı olarak veri göndermesini sağlamak**için seçeneğini belirleyin ve ardından aşağıdaki ayarları yapılandırın:  

- **Çok noktaya yayın bağlantı hesabı**: çok noktaya yayın için Configuration Manager veritabanı bağlantılarını yapılandırırken kullanılacak hesabı belirtin. Daha fazla bilgi için bkz. [çok noktaya yayın bağlantı hesabı](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Çok noktaya yayın adres ayarları**: hedef bilgisayarlara veri göndermek için IP adreslerini belirtin. Varsayılan olarak, çok noktaya yayın adreslerini dağıtmak için etkinleştirilen bir DHCP sunucusundan IP adresini alır. Ağ ortamına bağlı olarak, 239.0.0.0 ile 239.255.255.255 arasında bir IP adresi aralığı belirtebilirsiniz.  

    > [!IMPORTANT]  
    > Yapılandırdığınız IP adreslerine, işletim sistemi görüntüsünü isteyen hedef bilgisayarlardan erişilebilir olması gerekir. Yönlendiricilerin ve güvenlik duvarlarının hedef bilgisayarla dağıtım noktası arasında çok noktaya yayın trafiğine izin verildiğini doğrulayın.  

- **Çok noktaya yayın Için UDP bağlantı noktası aralığı**: hedef bilgisayarlara veri göndermek IÇIN kullanılan UDP bağlantı noktası aralığını belirtin.  

    > [!IMPORTANT]  
    > UDP bağlantı noktalarına, işletim sistemi görüntüsünü isteyen hedef bilgisayarlardan erişilebilir olması gerekir. Yönlendiricilerin ve güvenlik duvarlarının hedef bilgisayarla site sunucusu arasında çok noktaya yayın trafiğine izin verildiğini doğrulayın.  

- **Maksimum istemci**sayısı: Bu dağıtım noktasından işletim sistemi görüntüsünü indirebileceğiniz en fazla hedef bilgisayar sayısını belirtin.  

- **Zamanlanmış çok noktaya yayını etkinleştir**: Configuration Manager, işletim sistemlerinin hedef bilgisayarlara ne zaman başlatılacağını nasıl denetlediğini belirtin. Aşağıdaki seçenekleri yapılandırın:  

    - **Oturum başlatma gecikmesi (dakika)**: Configuration Manager ilk dağıtım isteğine yanıt vermeden önce bekleyeceği dakika sayısını belirtin.  

    - **En düşük oturum boyutu (istemciler)**: Configuration Manager işletim sistemini dağıtmaya başlamadan önce kaç istek alınması gerektiğini belirtin.  

> [!IMPORTANT]  
> Sürüm 1806 ' den başlayarak, dağıtım noktası özelliklerinin **çok noktaya** yayın sekmesinde çok noktaya yayını etkinleştirmek ve yapılandırmak için, dağıtım noktasının Windows dağıtım hizmeti kullanması gerekir.  
>
> - **İstemciler IÇIN PXE desteğini etkinleştirir** ve çok **noktaya yayının birden çok istemciye eşzamanlı olarak veri göndermesini**Isterseniz, **WINDOWS dağıtım hizmeti olmadan bir PXE yanıtlayıcıu etkinleştiremezsiniz**.  
>
> - **İstemciler IÇIN PXE desteğini etkinleştirir** ve **Windows Dağıtım HIZMETI olmadan bir PXE yanıtlayıcıu etkinleştirirseniz**, çok **noktaya yayının birden çok Istemciye eşzamanlı olarak veri göndermesini olanaklı hale** temezsiniz  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a>Grup ilişkileri  

> [!NOTE]  
> Bu seçenekler yalnızca daha önce yüklenmiş bir dağıtım noktasının özelliklerini düzenlediğinizde kullanılabilir.  

Bu dağıtım noktasının üyesi olduğu dağıtım noktası gruplarını yönetin.  

Bu dağıtım noktasını varolan bir dağıtım noktası grubuna üye olarak eklemek için **Ekle**' yi seçin. Dağıtım noktası gruplarına Ekle penceresinde, var olan bir grubu seçin ve ardından **Tamam**' ı seçin.  

Bu dağıtım noktasını bir dağıtım noktası grubundan kaldırmak için, listeden grubu seçin ve ardından **Kaldır**' ı seçin. Dağıtım noktasının bir dağıtım noktası grubundan kaldırılması, dağıtım noktasından içerik kaldırmaz.

### <a name="content"></a><a name="bkmk_config-content"></a>İçeriði  

> [!NOTE]  
> Bu seçenekler yalnızca daha önce yüklenmiş bir dağıtım noktasının özelliklerini düzenlediğinizde kullanılabilir.  

Dağıtım noktasına dağıttığınız içeriği yönetin. Dağıtım paketleri listesinden öğesini seçin ve aşağıdaki eylemleri gerçekleştirin:  

- **Doğrula**: yazılım için içerik dosyalarının bütünlüğünü doğrulamak üzere işlemi başlatın. İçerik doğrulama işleminin sonuçlarını görüntülemek için, **izleme** çalışma alanında **dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümünü seçin. Daha fazla bilgi için bkz. [Içeriği doğrulama](deploy-and-manage-content.md#validate-content).  

- Yeniden **Dağıt**: seçili yazılımın tüm içerik dosyalarını dağıtım noktasına kopyalar ve mevcut dosyaların üzerine yazar. Bu eylemi, genellikle içerik dosyalarını onarmak için kullanırsınız. Daha fazla bilgi için bkz. [içeriği yeniden dağıtma](deploy-and-manage-content.md#redistribute-content).  

- **Kaldır**: yazılımın içerik dosyalarını dağıtım noktasından kaldırır. Daha fazla bilgi için bkz. [Içeriği kaldırma](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a>İçerik doğrulama  

Dağıtım noktasındaki içerik dosyalarının bütünlüğünü doğrulamak için bir zamanlama ayarlayın. Bir zamanlamaya göre İçerik doğrulamayı etkinleştirdiğinizde Configuration Manager işlemi zamanlanan saatte başlatır. Dağıtım noktasındaki tüm içeriği yerel SMS_PackagesInContLib SCCMDP sınıfına göre doğrular. İçerik doğrulama önceliğini de yapılandırabilirsiniz. Varsayılan olarak, öncelik **En düşük**olarak ayarlanır. Önceliği artırmak, doğrulama işlemi sırasında sunucudaki işlemci ve disk kullanımını artırabilir, ancak daha hızlı tamamlanır.

İçerik doğrulama işleminin sonuçlarını görüntülemek için, **izleme** çalışma alanında **dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümünü seçin. Her yazılım türü için içeriği (örneğin, uygulama, yazılım güncelleştirme paketi ve önyükleme görüntüsü) gösterir.  

> [!WARNING]  
> İçerik doğrulama zamanlamasını bilgisayarın yerel saatini kullanarak belirtmenize karşın, Configuration Manager konsolu zamanlamayı UTC olarak gösterir.  

Daha fazla bilgi için bkz. [Içeriği doğrulama](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a>Sınır grupları  

Bu dağıtım noktasını atadığınız sınır gruplarını yönetin. Dağıtım noktasını en az bir sınır grubuna ekleyin. İçerik dağıtımı sırasında istemciler, içerik için kaynak konumu olarak bu dağıtım noktasını kullanmak üzere bir dağıtım noktasıyla ilişkili bir sınır grubunda olmalıdır.

Bir istemcinin içerik bulmak için ne zaman ve hangi sınır gruplarının geri dönebileceği belirleyen sınır grubu *ilişkilerini* yapılandırın. Daha fazla bilgi için bkz. [sınır grupları](boundary-groups.md).

**Ekle** ' yi seçin ve listeden varolan bir sınır grubunu seçin.

Bu dağıtım noktası için yeni bir sınır grubu oluşturmak için **Oluştur**' u seçin. Sınır grubu oluşturma ve yapılandırma hakkında daha fazla bilgi için bkz. [sınır grupları Için yordamlar](boundary-group-procedures.md).

Daha önce yüklenmiş bir dağıtım noktasının özelliklerini düzenlediğinizde, **isteğe bağlı dağıtım Için etkinleştirme**seçeneğini yönetin. Bu seçenek, bir istemci istediğinde Configuration Manager içeriği otomatik olarak bu sunucuya dağıtmasını sağlar. Daha fazla bilgi için bkz. [isteğe bağlı içerik dağıtımı](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="schedule"></a><a name="bkmk_config-sched"></a>Çizelgesini  

> [!NOTE]  
> Bu seçenekler yalnızca daha önce yüklenmiş bir dağıtım noktasının özelliklerini düzenlediğinizde kullanılabilir.
>
> Bu sekme yalnızca, site sunucusundan uzakta olan bir dağıtım noktasının özelliklerini düzenlerken kullanılabilir.  

Configuration Manager dağıtım noktasına veri aktarabilmesi durumunda sınırlayan bir zamanlama yapılandırın. Verileri önceliğe göre kısıtlayın veya seçili zaman dilimleriyle bağlantıyı kapatın.

Verileri kısıtlamak için kılavuzdaki zaman dilimini seçin ve ardından **kullanılabilirlik**için aşağıdaki ayarlardan birini seçin:  

- **Tüm önceliklere açık**: Configuration Manager verileri dağıtım noktasına hiçbir kısıtlama olmadan gönderir. Bu ayar tüm dönemler için varsayılandır.  

- **Orta ve yüksek önceliğe Izin ver**: Configuration Manager dağıtım noktasına yalnızca orta öncelikli ve yüksek öncelikli verileri gönderir.  

- **Yalnızca yüksek önceliğe Izin ver**: Configuration Manager dağıtım noktasına yalnızca yüksek öncelikli verileri gönderir.  

- **Kapalı**: Configuration Manager dağıtım noktasına herhangi bir veri göndermez.  

Yazılımın **Dağıtım önceliğini** , yazılımın özelliklerinin **dağıtım ayarları** sekmesinde yapılandırın.

> [!IMPORTANT]  
> Zamanlama, dağıtım noktasından değil, gönderen sitenin saat dilimini temel alır.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a>Oran limitleri  

> [!NOTE]  
> Bu seçenekler yalnızca daha önce yüklenmiş bir dağıtım noktasının özelliklerini düzenlediğinizde kullanılabilir.  
>
> Bu sekme yalnızca, site sunucusundan uzakta olan bir dağıtım noktasının özelliklerini düzenlerken kullanılabilir.  

Configuration Manager dağıtım noktasına içerik aktarmak için kullandığı ağ bant genişliğini denetlemek için hız sınırlarını yapılandırın. Aşağıdaki seçeneklerden birini seçin:  

- **Bu hedefe gönderirken sınırsız**: Configuration Manager, bir ücret sınırı kısıtlaması olmadan dağıtım noktasına içerik gönderir. Bu varsayılan ayardır.  

- **Darbe modu**: Bu seçenek, site sunucusunun dağıtım noktasına gönderdiği veri bloklarının boyutunu belirtir. Ayrıca gönderilen her veri öbeği arasındaki gecikme süresini de belirtebilirsiniz. Dağıtım noktasına çok düşük bant genişliğine sahip bir ağ bağlantısı üzerinden veri göndermeniz gerektiğinde bu seçeneği kullanın. Örneğin, bağlantının hızına veya belirli bir zamanda kullanımına bakılmaksızın beş saniyede bir 1 KB veri gönderme kısıtlamalarına sahip olursunuz.  

- **Saate göre belirtilen maksimum aktarım hızlarıyla sınırlı**: bir sitenin yalnızca yapılandırdığınız sürenin yüzdesini kullanarak dağıtım noktasına veri göndermesini sağlamak için bu ayarı belirtin. Bu seçeneği kullandığınızda, Configuration Manager ağın kullanılabilir bant genişliğini tanımlamaz. Bunun yerine, veri göndereme süresini böler. Sunucu kısa bir süre boyunca veri gönderir ve bu, verilerin gönderilmediği zaman dilimleriyle gelir. Örneğin, **sınır kullanılabilir bant genişliğini** **%50**olarak ayarlarsanız, Configuration Manager verileri bir süre ve ardından veri gönderilmediği zaman dilimi boyunca iletir. Verilerin gerçek boyut miktarı veya veri bloğunun boyutu yönetilmez. Yalnızca veri gönderdiği süreyi yönetir.  
