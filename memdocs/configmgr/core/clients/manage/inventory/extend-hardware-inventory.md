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
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427720"
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

## <a name="methods"></a>Yöntemler

### <a name="enable-or-disable"></a>Etkinleştir veya devre dışı bırak

İstemcide zaten var olan bir sınıfın tüm özniteliklerini etkinleştirin veya devre dışı bırakın. Bu eylem, donanım envanteri aracısının istemcileri üzerinde toplamasını ister. Bu eylemi varsayılan istemci ayarları veya özel cihaz istemci ayarları ' nda yapabilirsiniz. Daha fazla bilgi için bkz. [Mevcut envanter sınıflarını etkinleştirme veya devre dışı bırakma](#BKMK_Enable).

### <a name="add"></a>Ekle

İstemcide bir WMI sınıfı varsa ve site tarafından biliniyorsa, bu eylem bunu olası donanım envanteri sınıfları kümesine dahil eder. Başka bir cihazın WMI ad alanından yeni bir envanter sınıfı ekleyebilirsiniz. Bu eylem yalnızca varsayılan istemci ayarları ' dır. Daha fazla bilgi için bkz. [Yeni bir envanter sınıfı ekleme](#BKMK_Add).

### <a name="extend"></a>Genişletme

İstemciye yeni bir WMI sınıfı ekleyin. Donanım envanterini el ile genişletmek için üst düzey sitede Configuration. mof ' yi düzenleyin.<!-- SCCMDocs#1073 -->

WMI sınıfı zaten istemcide yoksa, WMI şemasını genişletmeniz gerekir:

1. Üst düzey sitede Configuration. mof ' i düzenleyin. Sitenin ekleme sitesini görmek için **veri günlüğü Dr. log** ' yı gözden geçirin.

1. Bir istemcide ilkeyi yenileyin ve yeni sınıfın derlenmesi için bekleyin.

1. Yeni sınıfı donanım envanterine [eklemek](#add) için varsayılan istemci ayarlarını kullanın. Varsayılan istemci ayarlarında bu sınıfı etkinleştirmeniz gerekmez. Bunu, özel bir cihaz istemci ayarında etkinleştirebilirsiniz.

### <a name="import-and-export"></a>İçeri ve dışarı aktarma

Envanter sınıflarını içeren Yönetilen Nesne Biçimi (MOF) dosyalarını içeri ve dışarı aktarmak için Configuration Manager konsolunu kullanın. Daha fazla bilgi için bkz. [donanım envanteri sınıflarını içeri](#BKMK_Import) aktarma ve [donanım envanteri sınıflarını dışa aktarma](#BKMK_Export).

### <a name="create-noidmif-files"></a>NOIDMIF Dosyaları Oluşturma

Configuration Manager stokunuzun istemci cihazları hakkında bilgi toplamak için NOıDMıF dosyalarını kullanın. Örneğin, yalnızca cihazda bir etiket olarak bulunan cihaz varlık numarası bilgilerini toplayın. NOIDMIF envanteri, toplandığı istemci cihaz ile otomatik olarak ilişkilendirilir. Daha fazla bilgi için bkz. [NOıDMıF dosyaları oluşturma](#BKMK_NOIDMIF).

### <a name="create-idmif-files"></a>IDMIF Dosyaları Oluşturma

Kuruluşunuzda bir Configuration Manager istemcisiyle ilişkili olmayan varlıklar hakkında bilgi toplamak için ıDMıF dosyalarını kullanın. Örneğin, projektörler, fotokopi makineleri ve ağ yazıcıları. Daha fazla bilgi için bkz. [ıDMıF dosyaları oluşturma](#BKMK_IDMIF).

## <a name="procedures-to-extend-hardware-inventory"></a>Donanım envanterini genişletme yordamları

Bu yordamlar donanım envanteri için varsayılan istemci ayarlarını yapılandırmanıza yardımcı olur ve hiyerarşinizdeki tüm istemciler için geçerlidir. Bu ayarların yalnızca bazı istemcilere uygulanmasını istiyorsanız özel bir istemci cihaz ayarı oluşturun ve belirli bir istemci koleksiyonuna atayın. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Mevcut envanter sınıflarını etkinleştirme veya devre dışı bırakma  

1. Configuration Manager konsolunda, **Yönetim**  >  **istemci ayarları**  >  **varsayılan istemci ayarları**' nı seçin.  

1. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

1. **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

1. **Donanım Envanteri Sınıfları** iletişim kutusunda, donanım envanteri tarafından toplanacak sınıfları ve sınıf özelliklerini seçin ya da seçimi kaldırın. Bir sınıftaki belirli özellikleri seçmek ya da seçimini kaldırmak üzere sınıfları genişletebilirsiniz. Belirli sınıfları aramak için **Envanter sınıflarını ara** alanını kullanın.  

    > [!IMPORTANT]  
    >  Configuration Manager donanım envanterine yeni sınıflar eklediğinizde, toplanan ve site sunucusuna gönderilen envanter dosyasının boyutu artar. Bu durum ağınızın ve Configuration Manager sitenizin performansını olumsuz etkileyebilir. Yalnızca toplamak istediğiniz envanter sınıflarını etkinleştirin.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Yeni bir envanter sınıfı Ekle  

Varsayılan istemci ayarlarını değiştirerek hiyerarşinin en üst düzey sunucusundan envanter sınıfları ekleyebilirsiniz. Bu seçenek özel cihaz ayarları oluşturduğunuzda kullanılamaz.

1. Configuration Manager konsolunda, **Yönetim**  >  **istemci ayarları**  >  **varsayılan istemci ayarları**' nı seçin.  

1. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

1. **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

1. **Donanım envanteri sınıfları** Iletişim kutusunda **Ekle**' yi seçin.  

1. **Donanım envanteri sınıfı Ekle** Iletişim kutusunda **Bağlan**' ı seçin.  

1. **Windows Yönetim Araçları Bağlan (WMI)** iletişim kutusunda, WMI sınıflarını alacağınız bilgisayarın adını ve sınıfları almak IÇIN kullanılacak WMI ad alanını belirtin. Belirttiğiniz WMI ad alanının altındaki tüm sınıfları almak isterseniz **özyinelemeli**' i seçin. Bağlanmakta olduğunuz bilgisayar yerel bilgisayar değilse, uzak bilgisayardaki WMI 'ya erişim iznine sahip olan bir hesabın kimlik bilgilerini sağlayın.

1. **Bağlan**’ı seçin.  

1. **Donanım envanteri sınıfı Ekle** Iletişim kutusundaki **envanter sınıfları** listesinde, donanım ENVANTERINI Configuration Manager eklemek istediğiniz WMI sınıflarını seçin.  

1. Seçili WMI sınıfıyla ilgili bilgileri düzenlemek istiyorsanız, **Düzenle**' yi seçin ve **Sınıf niteleyicileri** iletişim kutusunda aşağıdaki bilgileri sağlayın:  

    - **Görünen ad**: Bu ad, kaynak Gezgini görüntülenecektir.  

    - **Özellikler**: WMI sınıfının her bir özelliğinin gösterileceği birimleri belirtin.  

      Ayrıca, sınıfın her örneğini benzersiz bir şekilde tanımlamak için özellikleri anahtar özellik olarak ayarlayabilirsiniz. Sınıf için bir anahtar tanımlanmamışsa ve istemciden sınıfın birden çok örneği bildirilirse, yalnızca bulunan en son örnek veritabanına depolanır.  

      Özellikleri yapılandırmayı tamamladığınızda, **Sınıf niteleyicileri** iletişim kutusunu ve diğer açık iletişim kutularını kapatmak için **Tamam** ' ı seçin.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Donanım envanteri sınıflarını içeri aktar

Varsayılan istemci ayarlarını değiştirdiğinizde yalnızca envanter sınıflarını içeri aktarabilirsiniz. Ancak, bir şema değişikliği içermeyen bilgileri içeri aktarmak için, mevcut bir sınıfın **true** olan özelliğini **false**olarak değiştirme gibi özel istemci ayarlarını da kullanabilirsiniz.  

1. Configuration Manager konsolunda, **Yönetim**  >   **istemci ayarları**  >  **varsayılan istemci ayarları**' nı seçin.

1. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

1. **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

1. **Donanım envanteri sınıfları** Iletişim kutusunda **içeri aktar**' ı seçin.  

1. **Içeri aktar** iletişim kutusunda içeri aktarmak istediğiniz YÖNETILEN nesne BIÇIMI (MOF) dosyasını seçin ve ardından **Tamam**' ı seçin. İçeri aktarılacak öğeleri gözden geçirin ve ardından **Içeri aktar**' ı seçin.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Donanım envanteri sınıflarını dışarı aktar  

1. Configuration Manager konsolunda, **Yönetim**  >  **istemci ayarları**  >  **varsayılan istemci ayarları**' nı seçin.  

1. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Varsayılan Istemci ayarları** Iletişim kutusunda **donanım envanteri**' ni seçin.  

1. **Cihaz ayarları** listesinde **sınıfları ayarla**' yı seçin.  

1. **Donanım envanteri sınıfları** Iletişim kutusunda **dışarı aktar**' ı seçin.  

    > [!NOTE]  
    > Sınıfları dışarı aktardığınızda o anda seçili tüm sınıflar dışarı aktarılır.  

1. **Dışarı aktar** iletişim kutusunda sınıfları dışarı aktarmak istediğiniz YÖNETILEN nesne BIÇIMI (MOF) dosyasını belirtin ve ardından **Kaydet**' i seçin.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Donanım envanterini 255 karakterden daha büyük dizeler toplayacak şekilde yapılandırma

Donanım envanteri özellikleri için 255 karakterden daha büyük olacak dizelerin uzunluğunu belirtebilirsiniz. Bu eylem yalnızca yeni eklenen sınıflar ve anahtarlar olmayan donanım envanteri özellikleri için geçerlidir. <!-- 1357389 -->

1. **Yönetim** çalışma alanında **istemci ayarları**' nı seçin. Düzenlenecek bir istemci cihaz ayarı seçin ve ardından **Özellikler**' i seçin.

1. **Donanım envanterini**seçin, sonra **sınıfları ayarlayın**ve **ekleyin**.

1. **Bağlan**'ı seçin.

1. **Bilgisayar adı**, **WMI ad alanı**' nı doldurup gerekirse **özyinelemeli** ' i seçin. Bağlanmak gerekirse kimlik bilgilerini sağlayın. Ad alanı sınıflarını görüntülemek için **Bağlan** ' ı seçin.

1. Yeni bir sınıf seçin ve ardından **Düzenle**' yi seçin.

1. Anahtarınızın **uzunluğu** , anahtar dışındaki bir dize, 255 ' den büyük olacak şekilde değiştirin. **Tamam**’ı seçin.

1. **Donanım envanteri sınıfı Ekle**için düzenlenmiş özelliğin seçildiğinden emin olun ve **Tamam**' ı seçin.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>Donanım envanterini genişletmek için MIF dosyalarını kullanma

Configuration Manager tarafından istemcilerden toplanan donanım envanteri bilgilerini genişletmek için yönetim bilgisi biçimi (MIF) dosyalarını kullanın. Donanım envanteri sırasında MIF dosyalarına depolanan bilgiler, istemci envanter raporuna eklenir ve verileri varsayılan istemci envanteri verilerini kullandığınız şekilde kullanabileceğiniz site veritabanına depolanır. İki tür MIF dosyası vardır: NOıDMıF ve ıDMıF.

> [!IMPORTANT]  
> MIF dosyalarından Configuration Manager veritabanına bilgi eklemeden önce bunlar için sınıf bilgileri oluşturmanız veya içeri aktarmanız gerekir. Daha fazla bilgi için, bu makaledeki [Yeni bir envanter sınıfı eklemek](#BKMK_Add) ve [donanım envanteri sınıflarını içeri aktarmak](#BKMK_Import) için bölümlerine bakın.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>NOıDMıF dosyaları oluşturma

NOıDMıF dosyaları, normalde Configuration Manager tarafından toplanamayacak ve belirli bir istemci cihazından ilişkili bir istemci donanım envanterine bilgi eklemek için kullanılabilir. Örneğin, birçok şirket kuruluştaki her bilgisayarı bir varlık numarasıyla etiketleyip bu numaraları el ile kataloglayın. Bir NOıDMıF dosyası oluşturduğunuzda, bu bilgiler Configuration Manager veritabanına eklenebilir ve sorgular ve raporlama için kullanılabilir. NOıDMıF dosyaları oluşturma hakkında daha fazla bilgi için Configuration Manager SDK belgelerine bakın.  

> [!IMPORTANT]  
> Bir NOıDMıF dosyası oluşturduğunuzda, bu dosyanın ANSI kodlamalı bir biçimde kaydedilmesi gerekir. UTF-8 ile kodlanmış biçimde kaydedilen NOıDMıF dosyaları Configuration Manager tarafından okunamaz.  

Bir NOıDMıF dosyası oluşturduktan sonra, bu dosyayı `%Windir%\CCM\Inventory\Noidmifs` her bir istemcideki klasöründe saklayın. Configuration Manager, bir sonraki zamanlanmış donanım envanteri çevrimi sırasında bu klasördeki NODMıF dosyalarından bilgi toplar.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a>IDMıF dosyaları oluşturma

IDMıF dosyaları, normalde Configuration Manager tarafından envantere alınmayan ve belirli bir istemci cihazı ile ilişkili olmayan varlıklar hakkında Configuration Manager veritabanına bilgi eklemek için kullanılabilir. Örneğin, projektörler, DVD oynatıcılar, fotokopi makineleri veya Configuration Manager istemcisine sahip olmayan diğer donanımlar hakkında bilgi toplamak için ıDMıFS kullanabilirsiniz. IDMıF dosyaları oluşturma hakkında daha fazla bilgi için Configuration Manager SDK belgelerine bakın.  

Bir ıDMıF dosyası oluşturduktan sonra, bunu `%Windir%\CCM\Inventory\Idmifs` istemci bilgisayarlarındaki klasöründe saklayın. Configuration Manager, bir sonraki zamanlanmış donanım envanteri çevrimi sırasında bu dosyadan bilgi toplar. Dosyaları ekleyerek veya içeri aktararak dosyada yer alan bilgiler için yeni sınıflar bildirin.  

> [!NOTE]
> MIF dosyaları büyük miktarlarda veri içerebilir ve bu verilerin toplanması sitenizin performansını olumsuz etkileyebilir. MIF toplamayı yalnızca gerekli olduğunda etkinleştirin ve donanım envanteri ayarlarında **en büyük özel MIF dosyası boyutu (KB)** seçeneğini yapılandırın. Daha fazla bilgi için bkz. [Donanım envanterine giriş](introduction-to-hardware-inventory.md).
