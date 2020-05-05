---
title: Güç planları oluşturma ve uygulama
titleSuffix: Configuration Manager
description: Configuration Manager güç planlarını oluşturun ve uygulayın.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ba5479a4c75d3ab8f91a8439a6799589b93972d0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076705"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Configuration Manager 'de güç planları oluşturma ve uygulama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager güç yönetimi, hiyerarşinizdeki bilgisayar koleksiyonlarına Configuration Manager sağlanan güç planlarını uygulamanızı veya kendi özel güç planlarınızı oluşturmanızı sağlar. Bilgisayarlara yerleşik veya özel bir güç planı uygulamak için bu konudaki yordamı kullanın.  

> [!IMPORTANT]  
>  Cihaz koleksiyonlarına yalnızca Configuration Manager güç planları uygulayabilirsiniz.  

 Bilgisayar, her biri farklı güç planları uygulayan birden fazla koleksiyonun üyesiyse şu işlemler uygulanır:  

- Güç planı: Bilgisayara güç ayarları için birden fazla değer uygulanmışsa en az kısıtlayıcı olan değer kullanılır.  

- Uyandırma zamanı: Masaüstü bilgisayara birden fazla uyandırma zamanı uygulanmışsa gece yarısına en yakın olan zaman kullanılır.  

  Birden çok güç planı uygulanmış tüm bilgisayarları görüntülemek için **Birden Çok Güç Planına Sahip Bilgisayarlar** raporunu kullanın. Bu rapor sayesinde güç çakışmaları olan bilgisayarları keşfedebilirsiniz. Güç yönetimi raporları hakkında daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Windows grup ilkesi kullanılarak yapılandırılan güç ayarları, Configuration Manager güç yönetimi tarafından yapılandırılan ayarları geçersiz kılar.  

 Bir Configuration Manager güç planı oluşturmak ve uygulamak için aşağıdaki yordamı kullanın.  

### <a name="to-create-and-apply-a-power-plan"></a>Güç planı oluşturmak ve uygulamak için  

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2. **Varlıklar ve Uyum** çalışma alanında, **Aygıt Koleksiyonları**'nı tıklatın.  

3. **Cihaz Koleksiyonları** listesinde, güç yönetimi ayarları uygulamak istediğiniz koleksiyona tıklayıp **Giriş** sekmesinin **Özellikler** grubunda **Özellikler**'e tıklayın.  

4. <em><koleksiyonu adı\></em>**Özellikler** iletişim kutusunun **güç yönetimi** sekmesinde, **Bu koleksiyon için güç yönetimi ayarlarını belirtin**' i seçin.  

   > [!NOTE]  
   >  Ayrıca **Gözat** ’a tıklayıp güç yönetim ayarlarını seçili koleksiyona başka bir koleksiyondan kopyalayabilirsiniz.  

5. **Başlangıç** ve **Bitiş** alanlarında yoğun saatlerin (veya çalışma saatleri) başlangıç ve bitiş zamanını belirtin.  

6. Bir masaüstü bilgisayarın uyku veya bekleme modundan çıkarak zamanlanan güncelleştirmeleri ya da yazılım yüklemelerini yükleyeceği bir zaman belirtmek için **Uyandırma saati (masaüstü bilgisayarlar)** seçeneğini etkinleştirin.  

   > [!IMPORTANT]  
   >  Güç yönetimi, bilgisayarları uyku veya hazırda bekleme modundan çıkarmak için dahili Windows uyandırma zamanı özelliğini kullanır. Uyandırma zamanı ayarları taşınabilir bilgisayarlara, prize takılı olmadıklarında uyanabilecekleri senaryoları önlemek için uygulanmaz. Uyandırma zamanı rastgeledir ve bilgisayarlar belirtilen uyandırma zamanından itibaren bir saat içinde uyandırılırlar.  

7. Yoğun saatler (veya mesai saatleri) için özel bir güç planı yapılandırmak istiyorsanız **Yoğun saatler planı** açılır listesinden **Özelleştirilmiş Yoğun Saatler (ConfigMgr)** seçeneğini belirtip **Düzenle**’ye tıklayın. Yoğun olmayan saatler (veya mesai saatleri harici) için bir güç planı yapılandırmak istiyorsanız **Yoğun olmayan saatler planı** açılır listesinden **Özelleştirilmiş Yoğun Olmayan Saatler (ConfigMgr)** seçeneğini belirtip **Düzenle**’ye tıklayın.  

   > [!NOTE]  
   >  Bilgisayar koleksiyonlarına güç planı uygularken yoğun olan ve olmayan saatler için kullanılacak zaman çizelgelerini belirlemek için **Bilgisayar Etkinliği** raporunu kullanabilirsiniz. Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

    Ayrıca **Dengeli (ConfigMgr)**, **Yüksek Performans (ConfigMgr)** ve **Güç Tasarrufu (ConfigMgr)** yerleşik güç planlarından seçiminizi yapıp her güç planının özelliklerini görüntülemek için **Görüntüle** ’ye tıklayabilirsiniz.  

   > [!NOTE]  
   >  Yerleşik güç planlarını değiştiremezsiniz.  

8. <em><güç planı\>adı</em>**Özellikler** iletişim kutusunda, aşağıdaki ayarları yapılandırın:  

   -   **Ad:** Bu güç planı için bir ad belirtin veya sağlanan varsayılan değeri kullanın.  

   -   **Açıklama:**  Bu güç planı için bir açıklama belirtin veya sağlanan varsayılan değeri kullanın.  

   -   **Bu güç planı için özellikleri belirtin:** Güç planı özelliklerini yapılandırın. Bir özelliği devre dışı bırakmak için onay kutusunun işaretini kaldırın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bu konudaki [Available power management plan settings](#BKMK_Plans) bölümüne bakın.  

       > [!IMPORTANT]  
       >  Etkinleştirilen ayarlar, bilgisayarlara güç planı uygulandığında uygulanır. Bir güç ayarının onay kutusunun işaretini kaldırırsanız istemci bilgisayardaki değer, güç planı uygulandığında değiştirilmez. Onay kutusunun işaretini kaldırdığınızda güç ayarını uygulamadığınız sürece ayar, önceki değerine döndürülmez.  

9. <em><güç planı adı\></em>**Özellikler** iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.  

10. <em><koleksiyon adı\></em>**ayarları** iletişim kutusunu kapatmak ve güç planını uygulamak için **Tamam** ' ı tıklatın.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 Aşağıdaki tabloda Configuration Manager bulunan güç yönetimi ayarları listelenmektedir. Bilgisayarın prize takıldığı veya pil gücüyle çalıştığı zamanlar için ayrı ayarlar yapılandırabilirsiniz. Kullandığınız Windows sürümüne bağlı olarak bazı ayarlar yapılandırılamayabilir.  

> [!NOTE]  
>  Yapılandırmadığınız güç ayarları, istemci bilgisayarlardaki geçerli değerlerini korurlar.  

|Adı|Açıklama|  
|----------|-----------------|  
|**Ekranı kapatmadan önce geçen süre (dakika)**|Ekran kapatılmadan önce bilgisayarın etkin olmaması gereken süre uzunluğunu dakika cinsinden belirtir. Güç yönetiminin ekranı kapatmasını istemiyorsanız **0** değerini belirleyin.|  
|**Uyku moduna geçirmeden önce geçen süre (dakika)**|Uyku moduna geçirilmeden önce bilgisayarın etkin olmaması gereken süre uzunluğunu dakika cinsinden belirtir. Güç yönetiminin bilgisayarı uyku moduna geçirmesini istemiyorsanız **0** değerini belirleyin.|  
|**Uyanırken parola gerektir**|**Evet** veya **Hayır** değeri, uyku modundan uyanma girildiğinde bilgisayarın kilidini açmak için bir parolanın gerekli olup olmadığını belirtir.|  
|**Güç düğmesi eylemi**|Bilgisayarın güç düğmesine basıldığında gerçekleştirilecek eylemi belirtir. Olası değerler **hiçbir şey**, **uyku**, **hazırda bekleme**ve **kapatma**yapmaz.|  
|**Başlat menüsü güç düğmesi**|Bilgisayarın **Başlat** menüsü güç düğmesine bastığınızda oluşan eylemi belirtir. Olası değerler **Sleep**, **hazırda bekleme**ve **kapatma**.|  
|**Uyku düğmesi eylemi**|Bilgisayarın **uyku** düğmesine bastığınızda gerçekleştirilecek eylemi belirtir. Olası değerler **hiçbir şey**, **uyku**, **hazırda bekleme**ve **kapatma**yapmaz.|  
|**Kapak kapatma eylemi**|Kullanıcı taşınabilir bir bilgisayarın kapağını kapattığında uygulanacak eylemi belirtir. Olası değerler **hiçbir şey**, **uyku**, **hazırda bekleme**ve **kapatma**yapmaz.|  
|**Sabit diski kapatmak için beklenecek süre (dakika)**|Bilgisayarın sabit diskinin devre dışı bırakılmadan önce devre dışı olması gereken süre uzunluğunu dakika cinsinden belirtir. Güç yönetiminin bilgisayarın sabit diskini kapatmasını istemiyorsanız **0** değerini belirtin.|  
|**Hazırda beklemeden önce geçecek süre (dakika)**|Hazırda bekleme moduna geçirilmeden önce bilgisayarın etkin olmaması gereken süre uzunluğunu dakika cinsinden belirtir. Güç yönetiminin bilgisayarı hazırda bekleme moduna geçirmesini istemiyorsanız **0** değerini belirleyin.|  
|**Düşük pil eylemi**|Bilgisayarın pili belirtilen düşük pil bildirimi düzeyine ulaştığında gerçekleşecek eylemi belirtir. Olası değerler **hiçbir şey**, **uyku**, **hazırda bekleme**ve **kapatma**yapmaz.|  
|**Kritik pil eylemi**|Bilgisayarın pili belirtilen kritik pil bildirimi düzeyine ulaştığında gerçekleştirilecek eylemi belirtir. **Pille** çalışırken, **uyku**, **hazırda bekleme**ve **kapatma**değerlerini. Olası değerler **prize takılıyken** **hiçbir şey**, **uyku**, **hazırda bekleme**ve **kapatma**yapmaz.|  
|**Karma uykuya izin ver**|**Açık** veya **kapalı** değerini seçmek, Windows 'un uyku moduna girerken bir hazırda bekleme dosyası kaydedilip edilmeyeceğini belirtir. Bu, uyku moduna geçtiğinde bilgisayarın durumunu güç kaybı durumunda geri yüklemek için kullanılabilir.<br /><br /> Karma uyku masaüstü bilgisayarlar için tasarlanmıştır ve varsayılan olarak taşınabilir bilgisayarlarda etkin değildir. Windows 7 çalıştıran bilgisayarlarda karma uykuyu etkinleştirdiğinizde hazırda bekleme işlevi devre dışı bırakılır.|  
|**Uyuma eyleminde bekleme konumuna izin ver**|**Açık** veya **kapalı** değerini seçmek bilgisayarın bekleme durumunda olmasına olanak sağlar ve bu da daha fazla güç tüketir, ancak bilgisayarın daha hızlı uyanmasını sağlar. Bu ayar **Kapalı**olarak ayarlanırsa bilgisayar yalnızca hazırda bekleme konumuna geçebilir veya kapatılabilir.|  
|**Uyku modu için gereken boşta kalma oranı (%)**|Bilgisayarın uyku moduna geçmesi için gereken bilgisayar işlemci süresindeki bekleme süresi oranını belirtir. Windows 7 çalıştıran bilgisayarlar için, bu değer her zaman **0**olarak ayarlanır.|  
|**Masaüstü bilgisayarlar için Windows uyandırma zamanlayıcısı etkinleştirme**|**Etkinleştir** veya **devre dışı bırak** değerinin belirlenmesi, yerleşik Windows süreölçerinin güç yönetimi tarafından bir masaüstü bilgisayarı uyanması için kullanılmasını sağlayabilir. Bir masaüstü bilgisayarı Windows uyandırma zamanlayıcısı kullanılarak uyandırıldığında varsayılan olarak bilgisayarın güncelleştirmeleri yüklemesi veya ilkeleri alması için 10 dakika uyanık kalır.<br /><br /> Uyandırma zamanlayıcıları prize takılı olmadıklarında uyanabilecekleri senaryoları önlemek için taşınabilir bilgisayarlarda desteklenmez.|  
