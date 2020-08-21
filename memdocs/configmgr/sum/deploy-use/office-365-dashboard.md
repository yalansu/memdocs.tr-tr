---
title: Office 365 Istemci yönetimi panosu
titleSuffix: Configuration Manager
description: Office 365 Istemci yönetimi panosundan Microsoft 365 Apps istemci bilgilerini gözden geçirme
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: bae995b0704e2b2774d5f002cbf907777a3edcf0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697050"
---
# <a name="office-365-client-management-dashboard"></a>Office 365 Istemci yönetimi panosu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Note]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

Configuration Manager sürüm 1802 ' den başlayarak, Office 365 Istemci yönetimi panosundan Microsoft 365 Apps istemci bilgilerini gözden geçirebilirsiniz. Office 365 istemci yönetimi panosu, grafik bölümleri seçildiğinde ilgili cihazların bir listesini görüntüler. <!--1357281 -->

## <a name="prerequisites"></a>Ön koşullar

### <a name="enable-hardware-inventory"></a>Donanım envanterini etkinleştirme

Office 365 Istemci yönetimi panosunda görüntülenen veriler donanım envanterinden gelir. Donanım envanterini etkinleştirin ve panoda görüntülenecek veriler için **Office 365 ProPlus yapılandırması** donanım envanteri sınıfını seçin.
 
1. Henüz etkinleştirilmemişse, donanım envanterini etkinleştirin. Ayrıntılar için bkz. [donanım envanterini yapılandırma](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. Configuration Manager konsolunda, **Yönetim**  >  **istemci ayarları**  >  **varsayılan istemci ayarları**' na gidin.  
3. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  
4. **Varsayılan İstemci Ayarları** iletişim kutusunda **Donanım Envanteri**’ne tıklayın.  
5. **Cihaz Ayarları** listesinde **Sınıfları Ayarla**’ya tıklayın.  
6. **Donanım envanteri sınıfları** Iletişim kutusunda **Office 365 ProPlus yapılandırması**' nı seçin.  
7. Değişikliklerinizi kaydetmek için **Tamam** ’a tıklayın ve **Donanım Envanteri Sınıfları** iletişim kutusunu kapatın.

Office 365 Istemci yönetimi panosu, donanım envanteri bildirildiği için verileri görüntülemeye başlar.

### <a name="connectivity-for-top-level-site-server"></a>Üst düzey site sunucusu için bağlantı

*(Bir önkoşul olarak sürüm 1906 ' de kullanıma sunulmuştur)*

En üst düzey site sunucunuzun, hazırlık dosyasını indirmek için aşağıdaki uç noktaya erişmesi gerekir:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> Bu senaryoların herhangi birine yönelik istemci cihazları için Internet bağlantısı gerekli değildir.

### <a name="enable-data-collection-for-microsoft-365-apps"></a>Microsoft 365 uygulamalar için veri toplamayı etkinleştirme

*(Bir önkoşul olarak sürüm 1910 ' de kullanıma sunulmuştur)*

Sürüm 1910 ' den başlayarak, Microsoft 365 uygulamaların  **Office 365 ProPlus pilot ve sistem durumu panosundaki**bilgileri doldurması için veri toplamayı etkinleştirmeniz gerekir. Veriler Configuration Manager site veritabanında depolanır ve Microsoft 'a gönderilmez.

Bu veriler, [Microsoft 365 uygulamalardan Microsoft 'a gönderilen tanılama verileri](/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft)bölümünde açıklanan tanılama verilerinden farklıdır.

Grup ilkesi kullanarak ya da kayıt defterini düzenleyerek veri toplamayı etkinleştirebilirsiniz.

#### <a name="enable-data-collection-from-group-policy"></a>grup ilkesi veri toplamayı etkinleştir

1. En son [yönetim şablonu dosyalarını Microsoft Indirme Merkezi ' nden](https://www.microsoft.com/download/details.aspx?id=49030)indirin.
2. Altındaki **telemetri verilerini toplamayı aç** ilkesi ayarını etkinleştirin `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard` .
    - Alternatif olarak, [Office bulut İlkesi Hizmeti](/DeployOffice/overview-office-cloud-policy-service)ile ilke ayarını uygulayın.
    - Bu ilke ayarı, bu veri koleksiyonu için dağıtım yapmanız gerekmeyen Office telemetri panosu tarafından da kullanılır.

#### <a name="enable-data-collection-from-the-registry"></a>Kayıt defterinden veri toplamayı etkinleştirme

Aşağıdaki komut, kayıt defterinden veri toplamayı etkinleştirme örneğidir:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Office 365 Istemci yönetimi panosunu görüntüleme

Office 365 istemci yönetimi panosunu Configuration Manager konsolunda görüntülemek için, **yazılım kitaplığı**  >  **'na genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin. Panonun üst kısmında, belirli bir koleksiyonun üyelerine Pano verilerini filtrelemek için **koleksiyon** açılan ayarını kullanın. Configuration Manager sürüm 1802 ' den başlayarak Pano, grafik bölümleri seçildiğinde ilgili cihazların bir listesini görüntüler.

Office 365 Istemci yönetimi panosu, aşağıdaki bilgiler için grafikler sağlar:

- Microsoft 365 Apps istemcilerinin sayısı
- Microsoft 365 Apps istemci sürümleri
- Microsoft 365 Apps istemci dilleri
- Microsoft 365 uygulamalar İstemci kanalları daha fazla bilgi Için bkz. [Microsoft 365 uygulamalar için güncelleştirme kanallarına genel bakış](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-microsoft-365-apps-readiness"></a><a name="bkmk_o365_readiness"></a> Microsoft 365 uygulama hazırlığı için tümleştirme
<!--3735402-->
Configuration Manager sürüm 1902 ' den başlayarak, Microsoft 365 uygulamalarına yükseltmeye hazırlanma ve yüksek güvenilirlikli cihazları tanımlamak için panoyu kullanabilirsiniz. Bu tümleştirme, ortamınızdaki eklentiler ve makrolarla ilgili olası uyumluluk sorunları hakkında öngörüler sağlar. Daha sonra Configuration Manager kullanarak Microsoft 365 uygulamalarını kullanıma yönelik cihazlara dağıtın.

Office 365 istemci yönetimi panosu, **office 365 ProPlus yükseltme hazırlığı**yeni bir kutucuk içerir. Bu kutucuk, aşağıdaki durumlarda cihazların bir çubuk grafiğidir:
- Değerlendirilmedi
- Yükseltmeye hazırlanma
- Gözden geçirme gerekiyor

Bir cihaz listesine gitmek için bir durum seçin. Bu hazırlık raporu, cihazlar hakkında daha fazla ayrıntı gösterir. Bu, hem eklentilerin hem de makroların uyumluluk durumunun sütunlarını içerir.

### <a name="prerequisites-for-microsoft-365-apps-readiness-integration"></a>Microsoft 365 uygulamalar için hazır olma durumu tümleştirmesi önkoşulları

- İstemci ayarlarında donanım envanterini etkinleştirin. Daha fazla bilgi için [Önkoşullar](#prerequisites) bölümüne bakın.  

- Cihazın bir eklenti hazırlık dosyasını indirmek için Office içerik teslimi ağı 'na (CDN) bağlanması gerekir. Daha fazla bilgi için bkz. [içerik teslim ağları](/office365/enterprise/content-delivery-networks). Cihaz bu dosyayı indiremez, eklentiler durumu *gözden geçirmeniz gerekir*.  

    > [!Note]  
    > Bu özellik için Microsoft 'a veri gönderilmez.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a> Ayrıntılı makro hazırlığı

Varsayılan olarak, tarama Aracısı her cihazda en son kullanılan (MRU) dosyalar listesine bakar. Bu listedeki makroları destekleyen dosyaları sayar. Bu dosyalar aşağıdaki türleri içerir:
- Excel makro içerebilen çalışma kitapları (. xlsm) veya Word makro içerebilen belge (. docm) gibi makro içerebilen Office dosya biçimleri  
- Makro içeriğinin olup olmadığını belirten eski Office biçimleri. Örneğin, bir Excel 97-2003 çalışma kitabı (. xls).

Makro uyumluluğu hakkında daha ayrıntılı bilgi için, makro dosyalarındaki kodu çözümlemek üzere **Office Için hazırlık araç setini** dağıtın. Olası uyumluluk sorunları olup olmadığını denetler. Örneğin, dosya Office 'in daha yeni bir sürümünde değişen bir işlevi kullanır. Office için hazırlık araç setini çalıştırdıktan sonra, **Bu bilgisayarda en son kullanılan Office belgelerinin ve yüklü eklentilerin**bir seçeneğini belirledikten veya `-mru` komut satırındaki bayrağını kullanarak, sonuçlar Configuration Manager donanım envanteri Aracısı tarafından alınabilir. Bu ek veriler, cihaz hazırlık hesaplamasını geliştirir. Daha fazla bilgi için bkz. [Microsoft 365 uygulamalar için uygulama uyumluluğunu değerlendirmek üzere Office Için hazırlık araç setini kullanma](https://aka.ms/readinesstoolkit).

Hazırlık araç seti 'nin taramayı gerçekleştirmek için her hedef cihaza yüklenmesi gerekmediğini unutmayın. İstediğiniz her cihazı taramak için aşağıdaki örnek komut satırı seçeneğini kullanabilirsiniz.  Çıkış bayrağı gereklidir, ancak dosyalar panodaki sonuçları oluşturmak için kullanılmayacak, bu nedenle geçerli konum seçilebilir.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Daha fazla bilgi için bkz. [bir kuruluştaki birden fazla kullanıcı için hazır olma bilgileri alma](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="microsoft-365-apps-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a> Microsoft 365 uygulamalar hazır olma panosu

*(Sürüm 1906 ' de tanıtılmıştır)*

<!--4021125-->
Hangi cihazların Microsoft 365 uygulamalarına yükseltmeye hazır olduğunu belirlemenize yardımcı olmak için 1906 sürümünden itibaren hazır olma panosu vardır. Bu, geçerli sürüm 1902 Configuration Manager yayınlanan **Office 365 ProPlus yükseltme hazırlığı** kutucuğunu içerir. Bu panodaki aşağıdaki yeni kutucuklar eklenti ve makro hazırlığını değerlendirmenize yardımcı olur:

- Dağıtım
- Cihaz hazırlığı
- Eklenti hazırlığı
- Eklenti destek deyimleri
- Sürüm sayısına göre en çok kullanılan eklentiler
- Makroları olan cihazların sayısı
- Makro hazırlığı
- Makro Danışma belgeleri

Aşağıdaki videoda, daha fazla bilgi içeren bir Ignite 2019 oturumu verilmiştir:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Uyumluluk değerlendirmesi için en iyi uygulamalar ve Configuration Manager Office hazırlığı Microsoft Office 365 ProPlus yükseltmeleri](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-microsoft-365-apps-upgrade-readiness-dashboard"></a>Microsoft 365 Apps yükseltme hazırlığı panosunu kullanma

[Önkoşulları](#prerequisites)doğruladıktan sonra, Panoyu kullanmak için aşağıdaki yönergeleri kullanın:
 
1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin ve **Office 365 istemci yönetimi**' ni genişletin.
1. **Microsoft 365 Apps yükseltme hazırlığı** düğümünü seçin.
1. Panoda geçirilen bilgileri değiştirmek için **koleksiyonu** ve **hedef Office mimarisini** değiştirin.

[![Microsoft 365 Apps yükseltme hazırlığı panosu](./media/4021125-office-365-upgrade-readiness-dashboard.png)](./media/4021125-office-365-upgrade-readiness-dashboard.png#lightbox)

[![Microsoft 365 Apps yükseltme hazırlığı Pano eklentileri](./media/4021125-office-365-to-add-ins.png)](./media/4021125-office-365-to-add-ins.png#lightbox)

[![Microsoft 365 Apps yükseltme hazırlığı panosu makro belgeleri](./media/4021125-office-365-macro-advisories.png)](./media/4021125-office-365-macro-advisories.png#lightbox)

### <a name="device-readiness-information"></a>Cihaz hazırlığı bilgileri

Her cihazdaki eklenti ve makro envanteri hesaplandıktan sonra, cihazlar daha sonra bilgilere göre gruplandırılır. Durumu **yükseltme Için hazırlık** olarak listelenen cihazların herhangi bir uyumluluk sorununa sahip olma olasılığı yoktur.

Grafikteki **yükseltmeye hazırlanma** kategorisi seçildiğinde, sınırlandırma koleksiyonundaki cihazlarla ilgili daha fazla ayrıntı gösterilir. Cihaz listesini gözden geçirebilir, iş gereksinimlerinize göre seçimler yapabilir ve seçiminizden yeni bir cihaz koleksiyonu oluşturabilirsiniz. Configuration Manager ile Microsoft 365 uygulamaları dağıtmak için yeni koleksiyonunuzu kullanın.

Uyumluluk sorunları açısından riskli olabilecek cihazlar, **gereksinimler incelemesi**olarak işaretlenir. Bu cihazların Microsoft 365 uygulamalarına yükseltmeden önce yapılması gereken eylemler gerekebilir. Örneğin, kritik eklentileri daha yeni bir sürüme güncelleştirebilirsiniz.

### <a name="add-in-information"></a>Eklenti bilgileri

 Her cihazda, yüklenmiş tüm eklentilerin envanterini toplanır. Daha sonra envanter, Microsoft 'un Microsoft 365 uygulamalarda eklenti performansı hakkında bilgi ile karşılaştırılır. Yükseltmeden sonra sorunlara neden olabilecek bir eklenti bulunursa, eklentiye sahip tüm cihazlar gözden geçirilmek üzere işaretlenir.

### <a name="macro-information"></a>Makro bilgileri

Configuration Manager her cihazda en son kullanılan dosyaları arar. Bu listede, aşağıdaki türler dahil olmak üzere makroları destekleyen dosyalar sayılır:

- Makro içerebilen Office dosya biçimleri.
- Makro içeriğine işaret eden eski Office biçimleri.

Bu rapor, en son hangi cihazların makrolar içerebilecek dosyaları belirlemek için kullanılabilir. Daha sonra, daha ayrıntılı bilgi gerektiren tüm cihazları taramak için Configuration Manager kullanılarak **Office Için hazırlık araç seti** dağıtılabilir ve potansiyel uyumluluk sorunları olup olmadığını kontrol edebilirsiniz. Örneğin, dosya Microsoft 365 uygulamaların daha yeni bir sürümünde değiştirilen bir işlevi kullanıyorsa.

Taramayı gerçekleştirme hakkında daha fazla bilgi için bkz. [ayrıntılı makro hazırlığı](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a> Office 365 ProPlus pilot ve sistem durumu panosu
<!--4488272, 4488301-->
*(Sürüm 1910 ' de tanıtılmıştır)*

Sürüm 1910 ' den başlayarak, **Office 365 ProPlus pilot ve sistem durumu panosu** , Microsoft 365 Apps dağıtımını planlayıp gerçekleştirmenize yardımcı olur. Pano, dağıtım planlarınızı etkileyebilecek olası sorunları belirlemenize yardımcı olmak üzere Microsoft 365 uygulamalar içeren cihazlar için sistem durumu öngörüleri sağlar. **Office 365 ProPlus pilot ve sistem durumu panosu** , eklenti envanterini temel alan pilot cihazlar için bir öneri sunar. Panoda aşağıdaki kutucuklar bulunur:

- Pilot oluştur
- Önerilen pilot cihazlar
- Pilot dağıtma
- Sistem durumu verileri gönderen cihazlar
- Cihaz sistem durumu hedeflerini karşılamıyor
- Sistem durumu hedeflerini buluşma, eklentiler
- Makrolar sistem durumu hedeflerini karşılamıyor

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Office 365 ProPlus pilot ve sistem durumu panosunu kullanma

[Önkoşulları](#prerequisites)doğruladıktan sonra, Panoyu kullanmak için aşağıdaki yönergeleri kullanın:

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin ve **Office 365 istemci yönetimi**' ni genişletin.
1. **Office 365 Pilot ve sistem durumu** düğümünü seçin.

![Office 365 ProPlus pilot ve sistem durumu panosu](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Pilot oluştur

Bir düğmeye tıkladığınızda sınırlayan koleksiyondan bir pilot önerisi oluşturun. Eylem başlatıldıktan hemen sonra, bir arka plan görevi pilot koleksiyonunuzu hesaplamaya başlar. Sınırlandırmaya yönelik koleksiyonunuz, ProPlus olmayan bir Office sürümü olan en az bir cihaz içermelidir.

### <a name="recommended-pilot-devices"></a>Önerilen pilot cihazlar

**Önerilen pilot cihazlar** , pilot uygulamayı oluştururken kullandığınız sınırlandırma koleksiyonu genelinde yüklenmiş tüm eklentileri temsil eden en düşük cihaz kümesidir. Bu cihazların bir listesini almak için detaya gidin. Ardından, gerekirse pilot bilgisayardan tüm cihazları dışlamak için ayrıntıları kullanın. Eklentilerinizin tümü zaten Microsoft 365 Apps cihazlarında varsa, bu eklentilere sahip cihazlar hesaplamaya dahil değildir. Bu Ayrıca, Microsoft 365 uygulamaların yüklendiği cihazlarda tüm eklentilerinizin görülebilmesi için, pilot koleksiyonunuzda herhangi bir sonuç elde edilmeyeceğiniz anlamına gelir.

### <a name="deploy-pilot"></a>Pilot dağıtma

Pilot cihazlarınızı kabul ettikten sonra, aşamalı dağıtım Sihirbazı 'nı kullanarak pilot koleksiyonuna Microsoft 365 uygulamalar dağıtın. Yöneticiler, dağıtımları yönetmek için sihirbazda pilot ve sınırlama toplamayı tanımlayabilir.

### <a name="health-data"></a>Sistem durumu verileri

Microsoft 365 uygulamalar yüklendikten sonra, pilot cihazlarınızda sistem durumu verilerini etkinleştirin. Sistem durumu verileri, hangi eklentilerin ve makroların sistem durumu hedeflerini karşılamadığında fikir verir. Grafiği **dağıtmaya hazırlanma cihazları** , sistem durumu öngörüleri kullanılarak dağıtıma için hazırlanma ve pilot olmayan cihazları tanımlar. **Sistem durumu verileri grafik gönderen cihazlardan** sistem durumu verileri gönderen cihazların sayısını alın.

### <a name="devices-not-meeting-health-goals"></a>Cihaz sistem durumu hedeflerini karşılamıyor

Bu kutucuk, Eklentiler, makrolar veya her ikisiyle sorun olan cihazları özetler.

### <a name="add-ins-not-meeting-health-goals"></a>Sistem durumu hedeflerini buluşma, eklentiler

- Yükleme başarısız: eklenti başlatılamadı.
- Kilitlenmeler: eklenti çalışırken başarısız oldu.
- Hata: eklenti bir hata bildirdi.
- Birden çok sorun: eklenti, Yukarıdaki sorunlardan birine göre daha fazlasını içeriyor.

### <a name="macros-not-meeting-health-goals"></a>Makrolar sistem durumu hedeflerini karşılamıyor

- Yükleme başarısız: belge yüklenemedi.
- Çalışma zamanı hataları: makro çalışırken bir hata oluştu. Bu hatalar girdilere bağlı olabilir, bu nedenle her zaman gerçekleşmeyebilir.
- Derleme hataları: makro, çalıştırmayı denemeyecek şekilde doğru derlenmedi.
- Birden çok sorun: makroda Yukarıdaki sorunlardan birden fazlası vardır.

> [!NOTE]
> Makro envanteri, Office için hazır olma araç seti ve son kullanılan veri dosyaları verileri tarafından doldurulur. Makro sistem durumu sistem durumu verileri tarafından doldurulur. Farklı veri kaynakları nedeniyle, makro envanteri **taranmaz**makro sistem durumunun **incelenmesi gerekir** . <!--5922845-->

### <a name="known-issues"></a>Bilinen sorunlar

**Pilot kutucuk dağıtımı** ile ilgili bilinen bir sorun var. Şu anda bir pilot 'a dağıtmak için kullanılamaz. Geçici çözüm, aşamalı dağıtım Sihirbazı 'nı kullanarak bir uygulamayı dağıtmaya yönelik mevcut iş akışıdır. <!--5525871-->

## <a name="next-steps"></a>Sonraki adımlar

[Configuration Manager ile Microsoft 365 Apps güncelleştirmelerini yönetme](manage-office-365-proplus-updates.md)