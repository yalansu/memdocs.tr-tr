---
title: Donanım envanterini genişletme
titleSuffix: Configuration Manager
description: Configuration Manager 'de donanım envanterini genişletmenin yollarını öğrenin.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714419"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Configuration Manager 'de donanım envanterini genişletme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Donanım envanteri Windows Yönetim Araçları (WMI) kullanarak Windows PC 'lerden bilgi okur. WMI, bir kuruluştaki yönetim bilgilerine erişmek için sektör standardı olan Web tabanlı kuruluş yönetimi 'nin (WBEM) Microsoft uygulamasıdır. Configuration Manager önceki sürümlerinde, site sunucusundaki sms_def. mof dosyasını değiştirerek donanım envanterini genişletmiş olursunuz. Bu dosya, donanım envanteri tarafından okunabilen WMI sınıflarının bir listesini içeriyordu. Bu dosyayı düzenlediğinizde, var olan sınıfları etkinleştirip devre dışı bırakabilir ve stoğa yeni sınıflar da oluşturabilirsiniz.  

Configuration. mof dosyası, istemci üzerindeki donanım envanteri tarafından envantere kaydedilecek veri sınıflarını tanımlamak için kullanılır ve 2012 Configuration Manager değiştirilmez. İstemci sistemleri üzerindeki mevcut veya özel WMI depo veri sınıflarını veya kayıt defteri anahtarlarını envantere almak üzere veri sınıfları oluşturabilirsiniz.  

 Configuration.mof dosyası ayrıca donanım envanteri sırasında cihaz bilgilerine erişen WMI sağlayıcılarını tanımlar ve kaydeder. Sağlayıcıların kaydedilmesi kullanılacak sağlayıcı türünü ve sağlayıcının desteklediği sınıfları tanımlar.  

 Configuration Manager istemcileri ilke talep edildiğinde, Configuration. mof ilke gövdesine eklenir. Bu dosya daha sonra istemciler tarafından indirilir ve derlenir. Configuration.mof dosyasından veri sınıfları eklediğinizde, değiştirdiğinizde veya sildiğinizde, istemciler envanterle ilişkili veri sınıflarında yapılan bu değişiklikleri otomatik olarak derler. Configuration Manager istemcilerinde yeni veya değiştirilmiş veri sınıflarını envantere kaydetmek için başka bir eylem gerekmez. Bu dosya, birincil site sunucularında **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** yolunda bulunur.  

 Configuration Manager, artık sms_def. mof dosyasını Configuration Manager 2007 ' de yaptığınız şekilde düzenleyemezsiniz. Bunun yerine, WMI sınıflarını etkinleştirip devre dışı bırakabilir ve istemci ayarlarını kullanarak donanım envanteri tarafından toplanacak yeni sınıflar ekleyebilirsiniz. Configuration Manager, donanım envanterini genişletmek için aşağıdaki yöntemleri sağlar.  

> [!NOTE]  
>  Configuration. mof dosyasını özel envanter sınıfları eklemek üzere el ile değiştirdiyseniz, sürüm 1602 ' ye güncelleştirdiğinizde bu değişikliklerin üzerine yazılır. Güncelleştirme yaptıktan sonra özel sınıfları kullanmaya devam etmek için, 1602 ' ye güncelleştirdikten sonra bunları Configuration. mof dosyasının "eklenen Uzantılar" bölümüne eklemeniz gerekir.  
> Ancak, bu bölüm Configuration Manager tarafından değiştirilmek üzere ayrıldığından, bu bölümün üstündeki herhangi bir şeyi değiştirmemelidir. Özel Configuration.mof dosyanızın bir yedeğini şurada bulabilirsiniz:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Yöntem|Daha fazla bilgi|  
|------------|----------------------|  
|Mevcut envanter sınıflarını etkinleştirme veya devre dışı bırakma|Varsayılan envanter sınıflarını etkinleştirin veya devre dışı bırakın ya da belirtilen istemci koleksiyonlarından farklı donanım envanteri sınıfları toplamanıza imkan tanıyan özel istemci ayarları oluşturun. Bu makaledeki [Mevcut envanter sınıflarını etkinleştirmek veya devre dışı bırakmak için](#BKMK_Enable) bölümüne bakın.|  
|Yeni envanter sınıfı ekleme|Başka bir cihazın WMI ad alanından yeni bir envanter sınıfı ekleyin. Bu makaledeki [yeni envanter sınıfı ekleme](#BKMK_Add) yordamına bakın.|  
|Donanım envanteri sınıflarını içeri ve dışarı aktarma|Configuration Manager konsolundan envanter sınıflarını içeren Yönetilen Nesne Biçimi (MOF) dosyalarını içeri ve dışarı aktarın. Bu makaledeki [Donanım envanter sınıflarını içeri aktarmak](#BKMK_Import) ve [donanım envanteri sınıflarını dışarı aktarmak](#BKMK_Export) için bölümüne bakın.|  
|NOIDMIF Dosyaları Oluşturma|Configuration Manager tarafından envantere alınmayan istemci cihazları hakkında bilgi toplamak için NOıDMıF dosyalarını kullanın. Örneğin, yalnızca cihaz üzerindeki bir etikette bulunan cihaz varlık numarası bilgilerini toplamak isteyebilirsiniz. NOIDMIF envanteri, toplandığı istemci cihaz ile otomatik olarak ilişkilendirilir. Bu makaledeki [NOıDMıF dosyaları oluşturmak için](#BKMK_NOIDMIF) bölümüne bakın.|  
|IDMIF Dosyaları Oluşturma|Kuruluşunuzdaki varlıklar hakkında bilgi toplamak için ıDMıF dosyalarını kullanın, örneğin projektörler, fotokopi makineleri ve ağ yazıcıları gibi Configuration Manager istemcisiyle ilişkilendirilmemiş. Bu makalede [ıDMıF dosyaları oluşturmak için](#BKMK_IDMIF) bölümüne bakın.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Donanım envanterini genişletme yordamları  
Bu yordamlar donanım envanteri için varsayılan istemci ayarlarını yapılandırmanıza yardımcı olur ve hiyerarşinizdeki tüm istemciler için geçerlidir. Bu ayarların yalnızca bazı istemcilere uygulanmasını istiyorsanız özel bir istemci cihaz ayarı oluşturun ve belirli bir istemci koleksiyonuna atayın. Bkz. [istemci ayarlarını yapılandırma](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Mevcut envanter sınıflarını etkinleştirmek veya devre dışı bırakmak için  

1.  Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

4.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

5.  **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

6.  **Cihaz Ayarları** listesinde **Sınıfları Ayarla**’ya tıklayın.  

7.  **Donanım Envanteri Sınıfları** iletişim kutusunda, donanım envanteri tarafından toplanacak sınıfları ve sınıf özelliklerini seçin ya da seçimi kaldırın. Bir sınıftaki belirli özellikleri seçmek ya da seçimini kaldırmak üzere sınıfları genişletebilirsiniz. Belirli sınıfları aramak için **Envanter sınıflarını ara** alanını kullanın.  

    > [!IMPORTANT]  
    >  Configuration Manager donanım envanterine yeni sınıflar eklediğinizde, toplanan ve site sunucusuna gönderilen envanter dosyasının boyutu artar. Bu durum ağınızın ve Configuration Manager sitenizin performansını olumsuz etkileyebilir. Yalnızca toplamak istediğiniz envanter sınıflarını etkinleştirin.  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Yeni envanter sınıfı eklemek için  

Varsayılan istemci ayarlarını değiştirerek yalnızca hiyerarşinin en üst düzey sunucusundan envanter sınıfları ekleyebilirsiniz. Bu seçenek özel cihaz ayarları oluşturduğunuzda kullanılamaz.

1. Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

2. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

3. **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

4. **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

5. **Donanım envanteri sınıfları** Iletişim kutusunda **Ekle**' yi seçin.  

6. **Donanım Envanteri Sınıfı Ekle** iletişim kutusunda **Bağlan**’a tıklayın.  

7. **Windows Yönetim Araçları’na (WMI) Bağlan** iletişim kutusunda WMI sınıflarını alacağınız bilgisayarın adını ve sınıfları almak için kullanılacak WMI ad alanını belirtin. Belirttiğiniz WMI ad alanının altındaki tüm sınıfları almak isterseniz **Özyinelemeli**’ye tıklayın. Bağlanmakta olduğunuz bilgisayar yerel bilgisayar değilse, uzak bilgisayardaki WMI’ya erişim iznine sahip bir hesap için oturum açma kimlik bilgilerini sağlayın.  

8. **Bağlan**’ı seçin.  

9. **Donanım envanteri sınıfı Ekle** Iletişim kutusundaki **envanter sınıfları** listesinde, donanım ENVANTERINI Configuration Manager eklemek istediğiniz WMI sınıflarını seçin.  

10. Seçili WMI sınıfıyla ilgili bilgileri düzenlemek istiyorsanız, **Düzenle**' yi seçin ve **Sınıf niteleyicileri** iletişim kutusunda aşağıdaki bilgileri sağlayın:  

    - **Görünen ad** -bu ad, kaynak Gezgini görüntülenecektir.  

    - **Özellikler** -WMI sınıfının her bir özelliğinin gösterileceği birimleri belirtin.  

      Ayrıca sınıfın her bir örneğini benzersiz bir biçimde tanımlamak için özellikleri anahtar özellik olarak belirleyebilirsiniz. Sınıf için bir anahtar tanımlanmamışsa ve istemciden sınıfın birden çok örneği bildirilirse, yalnızca bulunan en son örnek veritabanına depolanır.  

      Özellikleri yapılandırmayı tamamladığınızda, **Sınıf niteleyicileri** iletişim kutusunu ve diğer açık iletişim kutularını kapatmak için **Tamam** ' ı tıklatın. 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Donanım envanteri sınıflarını içeri aktarmak için  

Varsayılan istemci ayarlarını değiştirdiğinizde yalnızca envanter sınıflarını içeri aktarabilirsiniz. Ancak, bir şema değişikliği içermeyen bilgileri içeri aktarmak için, mevcut bir sınıfın **true** olan özelliğini **false**olarak değiştirme gibi özel istemci ayarlarını da kullanabilirsiniz.  

1.  Configuration Manager konsolunda, **Yönetim** >  **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

4.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

5.  **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

6.  **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

7.  **Donanım envanteri sınıfları** Iletişim kutusunda **içeri aktar**' ı seçin.  

8.  **Içeri aktar** iletişim kutusunda içeri aktarmak istediğiniz YÖNETILEN nesne BIÇIMI (MOF) dosyasını seçin ve ardından **Tamam**' ı seçin. İçeri aktarılacak öğeleri gözden geçirin ve ardından **Içeri aktar**' a tıklayın.  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Donanım envanteri sınıflarını dışarı aktarmak için  

1.  Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

4.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

5.  **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

6.  **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

7.  **Donanım envanteri sınıfları** Iletişim kutusunda **dışarı aktar**' ı seçin.  

    > [!NOTE]  
    >  Sınıfları dışarı aktardığınızda o anda seçili tüm sınıflar dışarı aktarılır.  

8.  **Dışarı aktar** iletişim kutusunda sınıfları dışarı aktarmak istediğiniz YÖNETILEN nesne BIÇIMI (MOF) dosyasını belirtin ve ardından **Kaydet**' i seçin.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Donanım envanterini 255 karakterden daha büyük dizeler toplayacak şekilde yapılandırma
Configuration Manager 1802 ' den başlayarak, donanım envanteri özellikleri için en fazla 255 karakterden daha fazla olan dizelerin uzunluğunu belirtebilirsiniz. Bu değişiklik yalnızca yeni eklenen sınıflar ve anahtarlar olmayan donanım envanteri özellikleri için geçerlidir. <!-- 1357389 -->

1. **Yönetim** çalışma alanında, **istemci ayarları** ' na tıklayın, düzenlemek için istemci cihaz ayarını vurgulayın, sağ tıklayın ve ardından **Özellikler**' i seçin.

2. **Donanım envanterini**seçin, sonra **sınıfları ayarlayın**ve **ekleyin**.

3. **Bağlan** düğmesine tıklayın.

4. **Bilgisayar adı**, **WMI ad alanı**' nı doldurup gerekirse **özyinelemeli** ' i seçin. Bağlanmak gerekirse kimlik bilgilerini sağlayın. Ad alanı sınıflarını görüntülemek için **Bağlan** ' a tıklayın.

5. Yeni bir sınıf seçin ve ardından **Düzenle**' ye tıklayın.

6. Anahtar dışındaki bir dize olan, özelliğin **uzunluğunu** 255 ' dan büyük olacak şekilde değiştirin. **Tamam**'a tıklayın. 

7. **Donanım envanteri sınıfı Ekle** için düzenlenmiş özelliğin seçildiğinden emin olun ve **Tamam**' a tıklayın. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Donanım envanterini genişletmek için Yönetim Bilgi Dosyaları’nı (MIF Dosyaları) Kullanma  
 Configuration Manager tarafından istemcilerden toplanan donanım envanteri bilgilerini genişletmek için yönetim bilgisi biçimi (MIF) dosyalarını kullanın. Donanım envanteri sırasında MIF dosyalarına depolanan bilgiler, istemci envanter raporuna eklenir ve verileri varsayılan istemci envanteri verilerini kullandığınız şekilde kullanabileceğiniz site veritabanına depolanır. İki tür MIF dosyası vardır, NOıDMıF ve ıDMıF.

> [!IMPORTANT]  
>  MIF dosyalarından Configuration Manager veritabanına bilgi eklemeden önce bunlar için sınıf bilgileri oluşturmanız veya içeri aktarmanız gerekir. Daha fazla bilgi için, bu makaledeki [Yeni bir envanter sınıfı eklemek](#BKMK_Add) ve [donanım envanteri sınıflarını içeri aktarmak](#BKMK_Import) için bölümlerine bakın.  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> NOIDMIF dosyaları oluşturmak için  
 NOıDMıF dosyaları, normalde Configuration Manager tarafından toplanamayacak ve belirli bir istemci cihazından ilişkili bir istemci donanım envanterine bilgi eklemek için kullanılabilir. Örneğin, birçok şirket kuruluştaki her bilgisayarı bir varlık numarasıyla etiketleyip bu numaraları el ile kataloglayın. Bir NOıDMıF dosyası oluşturduğunuzda, bu bilgiler Configuration Manager veritabanına eklenebilir ve sorgular ve raporlama için kullanılabilir. NOıDMıF dosyaları oluşturma hakkında daha fazla bilgi için Configuration Manager SDK belgelerine bakın.  

> [!IMPORTANT]  
>  Bir NOıDMıF dosyası oluşturduğunuzda, bu dosyanın ANSI kodlamalı bir biçimde kaydedilmesi gerekir. UTF-8 ile kodlanmış biçimde kaydedilen NOıDMıF dosyaları Configuration Manager tarafından okunamaz.  

 Bir NOıDMıF dosyası oluşturduktan sonra, bu dosyayı her istemcideki _% windir%_**\Ccm\ınventory\noıdmıfs** klasöründe saklayın. Configuration Manager, bir sonraki zamanlanmış donanım envanteri çevrimi sırasında bu klasördeki NODMıF dosyalarından bilgi toplar.  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> IDMIF dosyaları oluşturmak için  
 IDMıF dosyaları, normalde Configuration Manager tarafından envantere alınmayan ve belirli bir istemci cihazı ile ilişkili olmayan varlıklar hakkında Configuration Manager veritabanına bilgi eklemek için kullanılabilir. Örneğin, projektörler, DVD oynatıcılar, fotokopi makineleri veya Configuration Manager istemcisine sahip olmayan diğer donanımlar hakkında bilgi toplamak için ıDMıFS kullanabilirsiniz. IDMıF dosyaları oluşturma hakkında daha fazla bilgi için Configuration Manager SDK belgelerine bakın.  

 IDMıF dosyasını oluşturduktan sonra, istemci bilgisayarlardaki _% windir%_**\Ccm\ınventory\ıdmıfs** klasöründe saklayın. Configuration Manager, bir sonraki zamanlanmış donanım envanteri çevrimi sırasında bu dosyadan bilgi toplar. Dosyalarda bulunan bilgiler için ekleme veya içeri aktarma yoluyla yeni sınıflar bildirmeniz gerekir.  

> [!NOTE]
> MIF dosyaları büyük miktarlarda veri içerebilir ve bu verilerin toplanması sitenizin performansını olumsuz etkileyebilir. MIF toplamayı yalnızca gerekli olduğunda etkinleştirin ve donanım envanteri ayarlarında **en büyük özel MIF dosyası boyutu (KB)** seçeneğini yapılandırın. Daha fazla bilgi için bkz. [Donanım envanterine giriş](introduction-to-hardware-inventory.md).
