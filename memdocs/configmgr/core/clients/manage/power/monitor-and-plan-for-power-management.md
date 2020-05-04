---
title: Güç yönetimi için izleme ve plan
titleSuffix: Configuration Manager
description: Configuration Manager 'de güç yönetimini izlemeyi ve planınızı öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715217"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimini izleme ve plan yapma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ' de güç yönetimini izlemenize ve planlamaya yardımcı olması için aşağıdaki bilgileri kullanın.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Güç yönetimi için raporları kullanma  
 Configuration Manager güç yönetimi, kuruluşunuzda güç tüketimini ve bilgisayar güç ayarlarını çözümlemenize yardımcı olan çeşitli raporlar içerir. Raporlar ayrıca sorunları gidermek için de kullanılabilir.  

 Güç yönetimi raporlarını kullanmadan önce hiyerarşiniz için raporlamayı yapılandırmanız gerekir. Configuration Manager raporlama hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Günlük raporlar tarafından kullanılan güç yönetimi bilgileri, Configuration Manager site veritabanında 31 gün boyunca tutulur.  
>           Aylık raporlar tarafından kullanılan güç yönetimi bilgileri, Configuration Manager site veritabanında 13 ay boyunca tutulur.  
>   
>  Raporları, güç yönetiminin izleme ve planlama ve uyumluluk aşamaları sırasında çalıştırdığınızda, daha sonra Configuration Manager tarafından kaldırıldıklarında daha sonra karşılaştırmaya yönelik verileri saklamak istediğiniz raporlardan sonuçları kaydedin veya dışarı aktarın.  

## <a name="list-of-power-management-reports"></a>Güç yönetimi raporlarının listesi  
 Aşağıdaki listeler Configuration Manager ' de kullanılabilen güç yönetimi raporlarının ayrıntılarını vermektedir.  

> [!NOTE]  
>  Güç yönetimi raporları, belirli bir koleksiyondaki fiziksel bilgisayarların ve sanal bilgisayarların sayısını gösterir. Ancak, bu raporlarda yalnızca fiziksel bilgisayarlardan alınan güç yönetimi bilgileri görüntülenir.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Bilgisayar Etkinliği raporu  
 **Bilgisayar Etkinliği** raporu, belirli bir koleksiyonda belirli bir dönem boyunca gerçekleşen şu etkinliklerin gösterildiği bir grafik görüntüler:  

- **Bilgisayar Açık** – Bilgisayar açık durumda.  

- **Monitör Açık** – Monitör açık durumda.  

- **Kullanıcı Etkin** – Bilgisayar faresinden, klavyesinden veya bilgisayara bağlanan bir Uzak Masaüstü bağlantısından etkinlik algılandı  

  Bu rapor, 24 saatlik bir dönemde gerçekleşen bilgisayar etkinliği, monitör etkinliği ve kullanıcı etkinliği arasındaki uyumu daha iyi anlamanıza yardımcı olmak amacıyla, izleme ve planlama aşaması ile zorunlu kılma aşaması sırasında kullanılır. Raporu birkaç günlüğüne çalıştırdığınızda, söz konusu günlere ait veriler toplanır. Bu rapor, belirli bir koleksiyon için iş saatlerini (yoğun saatler) ve iş dışındaki (yoğun saatler dışında) saatleri belirlemenizi sağlayarak, yapılandırılan güç yönetimi planlarını ne zaman uygulayacağınıza karar vermenize yardımcı olabilir.  

  Grafik, bir bilgisayarın açık olup kullanıcı etkinliğinin olmadığı süreleri gösterir. Bu sürelerde, açık olan ancak kullanılmayan bilgisayarların güç maliyetlerini azaltmak için daha kısıtlayıcı güç ayarları uygulayabilirsiniz. Grafta görüntülenen saat için bir dakika veya daha fazla süre boyunca bilgisayar, kullanıcı ve monitör etkinliği olduysa, bilgisayar etkin olarak kabul edilir. Bir bilgisayar, güç yönetimi verilerini raporlamıyorsa **Bilgisayar Etkinliği** raporuna dahil edilmez.  

  Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Başlangıç tarihi**|Aşağı açılan listeden bu rapor için başlangıç tarihini seçin.|  
|**Bitiş tarihi (İsteğe bağlı)**|Aşağı açılan listeden, bu rapor için isteğe bağlı bir bitiş tarihi seçin.|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden, rapora dahil edilmesini istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar).|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 **Bitiş tarihi (isteğe bağlı)** için bir değer belirtilmemişse bu rapor, daha fazla bilgi sağlayan bir sonraki raporun bağlantısını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Etkinliği Ayrıntıları**|Belirli bir tarih için etkin olan, etkin olmayan ve raporlama yapmayan bilgisayarların bir listesini görmek için **Ayrıntılı bilgi için tıklayın** bağlantısına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Computer Activity Details Report](#BKMK_Activity_Details) bölümüne bakın.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Bilgisayara Göre Bilgisayar Etkinliği raporu  
 **Bilgisayara Göre Bilgisayar Etkinliği** raporu, belirli bir tarihte belirli bir bilgisayar için şu etkinlikleri gösteren bir grafik görüntüler:  

- **Bilgisayar Açık** – Bilgisayar açık durumda.  

- **Monitör Açık** – Monitör açık durumda.  

- **Kullanıcı etkin** – bilgisayar faresi, bilgisayar klavyesi veya bilgisayara bir uzak masaüstü bağlantısından etkinlik algılandı.  

  Bu rapor, bağımsız olarak çalıştırılabilir veya **Bilgisayar Etkinliği Ayrıntıları** raporu tarafından çağrılabilir.  

> [!NOTE]  
>  Bilgisayar etkinliği hakkındaki bilgiler, donanım envanteri sırasında istemci bilgisayarlardan toplanır. Donanım envanterinin çalıştığı zamana bağlı olarak, yoğun saatlerde güç kullanım planının veya yoğun saatler dışında güç kullanım planının uygulandığı süreye ait etkinlik toplanabilir.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Rapor tarihi**|Aşağı açılan listeden, bu rapor için bir tarih seçin.|  
|**Bilgisayar adı**|Raporunu istediğiniz bilgisayar için bir ad girin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Ayrıntıları**|Seçilen bilgisayar için güç özelliklerini, güç ayarlarını ve uygulanan güç planlarını görmek üzere **Ayrıntılı bilgiler için tıklayın** bağlantısına tıklayın.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 **Bilgisayar Etkinliği Ayrıntıları** raporu, etkin veya etkin olmayan bilgisayarların listesini uyku ve uyanma özellikleriyle birlikte görüntüler. Bu rapor [Bilgisayar Etkinliği Raporu](#BKMK_Activity) tarafından çağrılır ve doğrudan site yöneticisi tarafından çalıştırılmak üzere tasarlanmamıştır.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Rapor tarihi**|Aşağı açılan listeden, bu rapor için kullanılacak bir tarih seçin.|  
|**Rapor saati**|Aşağı açılan listeden, bu raporun çalıştırılması için belirtilen tarihte bir saat seçin. Geçerli değerler: **00.00** ve **23.00**aralığındaki değerler.|  
|**Bilgisayar durumu**|Aşağı açılır listeden, bu raporun çalıştırılacağı bilgisayar durumunu seçin. Geçerli değerler **Tümü** (açık veya kapalı olan bilgisayarlar), **Açık** (açık olan bilgisayarlar) ve **kapalı** (kapatılan bilgisayarlar, uyku modunda veya hazırda bekletmeye açık). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  
|**Cihaz Türü**|Aşağı açılan listeden, rapora dahil edilmesini istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  
|**Uyku özellikli**|Aşağı açılan listeden, raporda uyku özellikli bilgisayarları görüntülemek isteyip istemediğinizi seçin. Geçerli değerler, **hepsi** (uyku özellikli ve uyumlu olmayan bilgisayarlar), **Hayır** (uyku özellikli olan bilgisayarlar) ve **Evet** (uyku özellikli olan bilgisayarlar).|  
|**Uykudan uyanma özellikli**|Aşağı açılan listeden, raporda uykudan uyanma özellikli bilgisayarları görüntülemek isteyip istemediğinizi seçin. Geçerli **değerler (her ikisi de uyku** modundan uyanma özellikli olan bilgisayarlar), **Hayır** (uykudan uyanma özellikli bilgisayarlar) ve **Evet** (uykudan uyanma özellikli bilgisayarlar).|  
|**Güç planı**|Aşağı açılan listeden, raporda görüntülemek istediğiniz güç planı türlerini seçin. Geçerli **değerler (herhangi** bir güç yönetimi planı uygulanmamış olan bilgisayarlar; güç yönetimi planına sahip olan bilgisayarlar; güç yönetiminden dışlanan bilgisayarlar), **belirtilen** (güç yönetimi planına sahip olmayan bilgisayarlar), **tanımlı** (güç yönetimi planı uygulanmış olan bilgisayarlar) ve **Dışlanan** (güç yönetiminin dışında tutulan bilgisayarlar).|  
|**İşletim sistemi**|Aşağı açılan listeden, raporda görüntülemek istediğiniz bilgisayar işletim sistemlerini seçin veya tüm işletim sistemlerini görüntülemek için **Tümü** seçeneğini belirtin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayara Göre Bilgisayar Etkinliği**|Seçilen bir raporlama dönemi boyunca o bilgisayar için belirli etkinlikleri görmek üzere bir bilgisayar adına tıklayın. Bu etkinlikler **üzerinde bilgisayar** (bilgisayar açık mı var?), **izleme açık** (izleyici açık mı var?) ve **Kullanıcı etkin** (bilgisayarın faresi, klavyesi veya uzak masaüstü bağlantısından etkinlik algılandı) bulunur.<br /><br /> Daha fazla bilgi için bu konunun [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) bölümüne bakın.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Bilgisayar Ayrıntıları raporu  
 **Bilgisayar Ayrıntıları** raporu, belirli bir bilgisayara uygulanan güç özellikleri, güç ayarları ve güç planlarıyla ilgili ayrıntılı bilgileri görüntüler. Bu rapor, **Bilgisayara Göre Bilgisayar Etkinliği** raporu, **Birden Çok Güç Planı Uygulanan Bilgisayarlar** raporu, **Güç Özellikleri** raporu ve **Güç Ayarları Ayrıntıları** raporu tarafından çağrılır. Rapor, doğrudan site yöneticisi tarafından çalıştırılmak üzere tasarlanmamıştır.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Bilgisayar adı**|Raporunu istediğiniz bilgisayar için bir ad girin.|  
|**Güç modu**|Aşağı açılan listeden, rapor sonuçlarında görüntülemek istediğiniz güç ayarlarının türünü seçin. Bilgisayarın prize takılı olduğu durumlar için yapılandırılan güç ayarlarını görüntülemek üzere **Prize Takılı** ’yı, bilgisayarın pil gücünden çalıştığı durumlar için yapılandırılan güç ayarlarını görüntülemek üzere **Pilde** ’yi seçin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu raporun ayarlayabileceğiniz gizli parametresi yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Ayrıntı Bildirmeyen Bilgisayar raporu  
 **Ayrıntı Bildirmeyen Bilgisayar** raporu, belirli bir koleksiyonda yer alan ve belirli bir tarih ve saatte herhangi bir güç etkinliği bildirmeyen bilgisayarların listesini görüntüler. Bu rapor **Bilgisayar Etkinliği Raporu** tarafından çağrılır ve doğrudan site yöneticisi tarafından çalıştırılmak üzere tasarlanmamıştır.  

> [!NOTE]  
>  Bilgisayarlar, güç yönetimi bilgilerini donanım envanteri zamanlamalarının bir parçası olarak bildirir. Bir bilgisayarın raporlama yapmadığına karar vermeden önce, bilgisayarın donanım envanteri raporladığından emin olun.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Rapor tarihi**|Aşağı açılan listeden, bu rapor için bir tarih seçin.|  
|**Rapor saati**|Aşağı açılan listeden, bu raporun çalıştırılması için belirtilen tarihte bir saat seçin. Geçerli değerler: **00.00** ve **23.00**aralığındaki değerler.|  
|**Cihaz Türü**|Aşağı açılan listeden, rapora dahil edilmesini istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Hariç Tutulan Bilgisayarlar  
 **Dışlanan bilgisayarlar** raporu, belirli bir koleksiyondaki Configuration Manager güç yönetiminden dışlanan bilgisayarların listesini görüntüler.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  
|**Yüzden**|Aşağı açılır listeden, bilgisayarların güç yönetiminin dışında tutulma nedenini seçin. **Yönetici tarafından dışlanan** (yalnızca bir yönetici kullanıcı tarafından dışlanan bilgisayarlar) ve **Kullanıcı tarafından dışlanan** (yalnızca yazılım merkezi 'nin bir kullanıcısı tarafından dışlanan bilgisayarlar) hariç olmak üzere, **Tümünü** (hariç tutulan tüm bilgisayarlar) görüntüleyebilirsiniz.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Güç Ayrıntıları**|Güç özelliklerini, güç ayarlarını ve seçili bilgisayar için uygulanan güç planlarını görmek için bir bilgisayar adına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Computer Details Report](#BKMK_Computer_Details) bölümüne bakın.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Birden Çok Güç Planı Uygulanan Bilgisayarlar  
 **Birden Çok Güç Planına Sahip Bilgisayarlar** raporu, her biri farklı güç planları uygulayan birden fazla koleksiyona üye olan bilgisayarların listesini görüntüler. Rapor, çakışma olasılığı bulunan güç ayarlarına sahip her bilgisayar için, bilgisayar adını ve bilgisayarın üye olduğu koleksiyonların uyguladığı güç planlarını görüntüler.  

> [!IMPORTANT]  
>  Bir bilgisayar birden fazla koleksiyonun üyesiyse, her koleksiyonun farklı güç planları varsa, en az kısıtlayıcı güç planı uygulanır.  
>   
>  Bir bilgisayar birden çok koleksiyonun üyesiyse, her koleksiyonun farklı uyandırma süreleri varsa, gece yarısına en yakın olan zaman kullanılır.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Güç Ayrıntıları**|Güç özelliklerini, güç ayarlarını ve seçili bilgisayar için uygulanan güç planlarını görmek için bir bilgisayar adına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Computer Details Report](#BKMK_Computer_Details) bölümüne bakın.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Enerji Tüketimi raporu  
 **Enerji Tüketimi** raporu aşağıdaki bilgileri görüntüler:  

- Belirli bir koleksiyonda bulunan bilgisayarların belirli bir dönemdeki aylık toplam güç tüketimini kiloWatt/saat (kW/s) cinsinden gösteren bir grafik.  

- Belirli bir koleksiyonda bulunan bilgisayarların belirli bir dönemdeki ortalama güç tüketimini kiloWatt/saat (kW/s) cinsinden gösteren bir grafik.  

- Belirli bir koleksiyonda bulunan bilgisayarların belirli bir dönemdeki aylık toplam güç tüketimini ve ortalama güç tüketimini kiloWatt/saat (kW/s) cinsinden gösteren bir tablo.  

  Bu bilgiler, ortamınızdaki güç tüketimi eğilimlerini öğrenmenize yardımcı olabilir. Seçili koleksiyondaki bilgisayarlara güç planı uygulandıktan sonra bilgisayarların güç tüketiminin azalması gerekir.  

> [!NOTE]  
>  Güç planı ekledikten sonra koleksiyonunuzda üye ekleme veya kaldırma işlemi yaparsanız, bu işlem **Enerji Tüketimi** raporu tarafından gösterilen sonuçları etkiler. Ayrıca, bu sonuçların izleme ve planlama aşaması ile zorunlu kılma aşamasından alınan sonuçlarla karşılaştırılmasını da zorlaştırabilir.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Başlangıç tarihi**|Aşağı açılan listeden, bu rapor için bir başlangıç tarihi seçin.|  
|**Bitiş tarihi**|Aşağı açılan listeden, bu rapor için bir bitiş tarihi seçin.|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden, rapora dahil edilmesini istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Masaüstü bilgisayar açık**|Masaüstü bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,07** kW/saat.|  
|**Dizüstü bilgisayar açık**|Taşınabilir bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,02** kW/saat.|  
|**Masaüstü bilgisayar uyku modunda**|Masaüstü bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,003** kW/saat.|  
|**Dizüstü bilgisayar uyku modunda**|Taşınabilir bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,001** kW/saat.|  
|**Masaüstü bilgisayar kapalı**|Masaüstü bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Dizüstü bilgisayar kapalı**|Taşınabilir bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Masaüstü bilgisayar monitörü açık**|Masaüstü bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,028** kW/saat.|  
|**Dizüstü bilgisayar monitörü açık**|Taşınabilir bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Günlük Enerji Tüketimi raporu  
 **Günlük Enerji Tüketimi** raporu aşağıdaki bilgileri görüntüler:  

- Belirli bir koleksiyonda bulunan bilgisayarların son 31 gündeki günlük toplam güç tüketimini kiloWatt/saat (kW/s) cinsinden gösteren bir grafik.  

- Belirli bir koleksiyonda bulunan bilgisayarların son 31 gündeki ortalama günlük güç tüketimini kiloWatt/saat (kW/s) cinsinden gösteren bir grafik.  

- Belirli bir koleksiyonda bulunan bilgisayarların son 31 gündeki günlük toplam güç tüketimini ve günlük ortalama güç tüketimini kiloWatt/saat (kW/s) cinsinden gösteren bir tablo.  

  Bu bilgiler, ortamınızdaki güç tüketimi eğilimlerini öğrenmenize yardımcı olabilir. Seçili koleksiyondaki bilgisayarlara güç planı uygulandıktan sonra bilgisayarların güç tüketiminin azalması gerekir.  

> [!NOTE]  
>  Güç planı ekledikten sonra koleksiyonunuzda üye ekleme veya kaldırma işlemi yaparsanız, bu işlem **Enerji Tüketimi** raporu tarafından gösterilen sonuçları etkiler. Ayrıca, bu sonuçların izleme ve planlama aşaması ile zorunlu kılma aşamasından alınan sonuçlarla karşılaştırılmasını da zorlaştırabilir.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden raporlamak istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Masaüstü bilgisayar açık**|Masaüstü bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,07** kW/saat.|  
|**Dizüstü bilgisayar açık**|Taşınabilir bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,02** kW/saat.|  
|**Masaüstü bilgisayar uyku modunda**|Masaüstü bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,003** kW/saat.|  
|**Dizüstü bilgisayar uyku modunda**|Taşınabilir bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,001** kW/saat.|  
|**Masaüstü bilgisayar kapalı**|Masaüstü bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Dizüstü bilgisayar kapalı**|Taşınabilir bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Masaüstü bilgisayar monitörü açık**|Masaüstü bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,028** kW/saat.|  
|**Dizüstü bilgisayar monitörü açık**|Taşınabilir bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Enerji Maliyeti raporu  
 **Enerji Maliyeti** raporu aşağıdaki bilgileri görüntüler:  

- Belirli bir koleksiyondaki belirli bir dönem için bilgisayarların aylık toplam güç maliyetini gösteren bir grafik.  

- Belirli bir koleksiyondaki belirtilen dönem için her bilgisayarın aylık ortalama güç maliyetini gösteren bir grafik.  

- Belirli bir koleksiyondaki son 31 gün için bilgisayarların aylık toplam güç maliyetini ve aylık ortalama güç maliyetini gösteren bir tablo.  

  Bu bilgiler, ortamınızdaki güç maliyeti eğilimlerini öğrenmenize yardımcı olabilir. Seçili koleksiyondaki bilgisayarlara güç planı uyguladıktan sonra bilgisayarların güç maliyetlerinin azalması gerekir.  

  Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Başlangıç tarihi**|Aşağı açılan listeden, bu rapor için bir başlangıç tarihi seçin.|  
|**Bitiş tarihi**|Aşağı açılan listeden, bu rapor için bir bitiş tarihi seçin.|  
|**KW/saat maliyeti**|Saatlik elektrik maliyetini Kilowatt cinsinden belirtir. Varsayılan değer: **0,09**.<br /><br /> Bu rapor tarafından kullanılan para birimini gizli parametreler bölümünden değiştirebilirsiniz.|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden raporlamak istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Masaüstü bilgisayar açık**|Masaüstü bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,07** kW/saat.|  
|**Dizüstü bilgisayar açık**|Taşınabilir bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,02** kW/saat.|  
|**Masaüstü bilgisayar uyku modunda**|Masaüstü bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,003** kW/saat.|  
|**Dizüstü bilgisayar uyku modunda**|Taşınabilir bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,001** kW/saat.|  
|**Masaüstü bilgisayar kapalı**|Masaüstü bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Dizüstü bilgisayar kapalı**|Taşınabilir bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Masaüstü bilgisayar monitörü açık**|Masaüstü bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,028** kW/saat.|  
|**Dizüstü bilgisayar monitörü açık**|Taşınabilir bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Birimindeki**|Bu rapor için kullanılacak para birimi etiketini belirtin. Varsayılan değer: **ABD Doları ($)**.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Günlük Enerji Maliyeti raporu  
 **Günlük Enerji Maliyeti** raporu aşağıdaki bilgileri görüntüler:  

- Belirli bir koleksiyondaki son 31 gün için bilgisayarların günlük toplam güç maliyetini gösteren bir grafik.  

- Belirli bir koleksiyondaki son 31 gün için her bilgisayarın günlük ortalama güç maliyetini gösteren bir grafik.  

- Belirli bir koleksiyondaki son 31 gün için bilgisayarların günlük toplam güç maliyetini ve günlük ortalama güç maliyetini gösteren bir tablo.  

  Bu bilgiler, ortamınızdaki güç maliyeti eğilimlerini öğrenmenize yardımcı olabilir. Seçili koleksiyondaki bilgisayarlara güç planı uyguladıktan sonra bilgisayarların güç maliyetlerinin azalması gerekir.  

  Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden raporlamak istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  
|**KW/saat maliyeti**|Saatlik elektrik maliyetini Kilowatt cinsinden belirtir. Varsayılan değer: **0,09**.<br /><br /> Bu rapor tarafından kullanılan para birimini gizli parametreler bölümünden değiştirebilirsiniz.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Masaüstü bilgisayar açık**|Masaüstü bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,07** kW/saat.|  
|**Dizüstü bilgisayar açık**|Taşınabilir bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,02** kW/saat.|  
|**Masaüstü bilgisayar uyku modunda**|Masaüstü bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,003** kW/saat.|  
|**Dizüstü bilgisayar uyku modunda**|Taşınabilir bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,001** kW/saat.|  
|**Masaüstü bilgisayar kapalı**|Masaüstü bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Dizüstü bilgisayar kapalı**|Taşınabilir bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Masaüstü bilgisayar monitörü açık**|Masaüstü bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,028** kW/saat.|  
|**Dizüstü bilgisayar monitörü açık**|Taşınabilir bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Birimindeki**|Bu rapor için kullanılacak para birimi etiketini belirtin. Varsayılan değer: **ABD Doları ($)**.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Çevre Etkisi raporu  
 **Çevre Etkisi** raporu aşağıdaki bilgileri görüntüler:  

- Belirtilen bir koleksiyondaki bilgisayarlar için belirtilen dönem için oluşturulan toplam aylık CO2 (ton cinsinden) gösteren bir grafik.  

- Belirtilen dönem için belirtilen koleksiyonda bulunan her bilgisayar için oluşturulan ortalama aylık CO2 (ton cinsinden) gösteren bir grafik.  

- Belirtilen dönem için belirtilen koleksiyondaki bilgisayarlar için oluşturulan toplam aylık CO2 ve ortalama aylık CO2 gösteren bir tablo.  

  **Çevre etkisi** raporu, 24 saatlik bir dönemde bir bilgisayarın veya izleyicinin açık olduğu zamanı kullanarak oluşturulan CO2 miktarını (ton cinsinden) hesaplar.  

  Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Rapor başlangıç tarihi**|Aşağı açılan listeden, bu rapor için bir başlangıç tarihi seçin.|  
|**Rapor bitiş tarihi**|Aşağı açılan listeden, bu rapor için bir bitiş tarihi seçin.|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden, rapora dahil edilmesini istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Masaüstü bilgisayar açık**|Masaüstü bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,07** kW/saat.|  
|**Dizüstü bilgisayar açık**|Taşınabilir bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,02** kW/saat.|  
|**Masaüstü bilgisayar uyku modunda**|Masaüstü bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,003** kW/saat.|  
|**Dizüstü bilgisayar uyku modunda**|Taşınabilir bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,001** kW/saat.|  
|**Masaüstü bilgisayar kapalı**|Masaüstü bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Dizüstü bilgisayar kapalı**|Taşınabilir bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Masaüstü bilgisayar monitörü açık**|Masaüstü bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,028** kW/saat.|  
|**Dizüstü bilgisayar monitörü açık**|Taşınabilir bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Karbon Faktörü (ton cinsinden kW/saat)** (CO2Mix)|Karbon faktörü (ton cinsinden kW/saat) değerini belirtir. Bu değeri elektrik şirketinizden öğrenebilirsiniz. Varsayılan değer: kW/saat başına **0,0015** ton.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Günlük Çevre Etkisi raporu  
 **Günlük Çevre Etkisi** raporu aşağıdaki bilgileri görüntüler:  

- Belirtilen koleksiyondaki son 31 gün için bilgisayarlar için oluşturulan günlük toplam CO2 (ton cinsinden) gösteren bir grafik.  

- Belirtilen koleksiyondaki son 31 gün için her bilgisayar için oluşturulan ortalama günlük CO2 (ton cinsinden) gösteren bir grafik.  

- Son 31 gün için belirtilen koleksiyondaki bilgisayarlar için oluşturulan günlük toplam CO2 ve ortalama günlük CO2 gösteren bir tablo.  

  **Güne göre çevresel etki** raporu, bir bilgisayarın veya izleyicinin 24 saatlik bir dönemde açık olduğu zamanı kullanarak oluşturulan CO2 miktarını (ton cinsinden) hesaplar.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  
|**Cihaz Türü**|Aşağı açılan listeden raporlamak istediğiniz bilgisayar türünü seçin. Geçerli **değerler şunlardır (** masaüstü ve taşınabilir bilgisayarlar), **Masaüstü** (yalnızca masaüstü bilgisayarlar) ve **dizüstü bilgisayar** (yalnızca taşınabilir bilgisayarlar). Bu değerler yalnızca seçili raporlama dönemi için döndürülür.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Masaüstü bilgisayar açık**|Masaüstü bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,07** kW/saat.|  
|**Dizüstü bilgisayar açık**|Taşınabilir bilgisayar açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,02** kW/saat.|  
|**Masaüstü bilgisayar kapalı**|Masaüstü bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Dizüstü bilgisayar kapalı**|Taşınabilir bilgisayar kapalı durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Masaüstü bilgisayar uyku modunda**|Masaüstü bilgisayar uyku moduna geçtiğinde tüketilen güç miktarını belirtir. Varsayılan değer: **0,003** kW/saat.|  
|**Dizüstü bilgisayar uyku modunda**|Uykuya geçtiğinde taşınabilir bilgisayarın güç tüketimini belirtin. Varsayılan değer: **0,001** kW/saat.|  
|**Masaüstü bilgisayar monitörü açık**|Masaüstü bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0,028** kW/saat.|  
|**Dizüstü bilgisayar monitörü açık**|Taşınabilir bilgisayar monitörü açık durumdayken tüketilen güç miktarını belirtir. Varsayılan değer: **0** kW/saat.|  
|**Karbon Faktörü (ton cinsinden kW/saat)** (CO2Mix)|Genelde güç şirketinizden alabildiğiniz karbon faktörü (ton olarak kW/s) değerini belirtin. Varsayılan değer: kW/saat başına **0,0015** ton.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, başka herhangi bir güç yönetimi raporuna bağlantı vermiyor.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Uyku Moduna Geçmeyen Bilgisayar Ayrıntıları raporu  
 **Uyku Moduna Geçmeyen Bilgisayar Ayrıntıları** raporu, belirli bir dönemde belirli bir nedenle uyku veya bekleme moduna geçmeyen bilgisayarların bir listesini görüntüler. Bu rapor, **Uyku Moduna Geçmeme Raporu** tarafından çağrılır ve doğrudan site yöneticisi tarafından çalıştırılmak üzere tasarlanmamıştır.  

 **Uyku Moduna Geçmeme Raporu** , bilgisayarları uyku özellikli olmamaları ve belirtilen rapor aralığı boyunca açık kalmış olmaları durumunda **Uyku özellikli değil** olarak gösterir. Rapor, bilgisayarları hazırda bekleme özelliğine sahip olmamaları ve belirtilen rapor aralığı boyunca açık kalmış olmaları durumunda **Hazırda bekleme özellikli değil** olarak gösterir.  

> [!NOTE]  
>  Güç yönetimi, yalnızca Windows 7 veya Windows Server 2008 R2 çalıştıran bilgisayarların uyku ya da bekleme moduna geçmesini engelleyen nedenleri toplayabilir.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Rapor aralığı (gün)**|Raporlanacak gün sayısını belirtin. Varsayılan değer **7** gündür.|  
|**Uyku Moduna Geçmeme Nedeni**|Aşağı açılan listeden, bilgisayarların uyku veya bekleme moduna geçmesini engelleyebilecek nedenlerden birini seçin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Ayrıntıları**|Seçilen bilgisayar için güç özelliklerini, güç ayarlarını ve uygulanan güç planlarını görmek üzere **Ayrıntılı bilgiler için tıklayın** bağlantısına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Computer Details Report](#BKMK_Computer_Details) bölümüne bakın.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 **Uyku Moduna Geçmeme Raporu** , bilgisayarların uyku moduna geçmesini veya hazırda beklemesini engelleyen temel nedenlerin listesini ve belirtilen süre boyunca her bir nedenden etkilenen bilgisayar sayısını görüntüler. Bir bilgisayarın uyku ya da bekleme moduna geçmesini engelleyen birçok neden olabilir. Bilgisayarda çalışan bir işlemin olması, açık bir Uzak Masaüstü oturumu veya bilgisayarın uyku ya da bekleme özellikli olmaması, bu nedenlerden bazılarıdır. Bu rapordan, **Uyku Moduna Geçmeyen Bilgisayar Ayrıntıları** raporunu açarak bilgisayarların uyku veya bekleme moduna geçmesini engelleyen nedenlerden etkilenen bilgisayarların listesini görüntüleyebilirsiniz.  

 Güç Uyku Moduna Geçmeme raporu, bilgisayarları uyku özellikli olmamaları ve belirtilen rapor aralığı boyunca açık kalmış olmaları durumunda **Uyku özellikli değil** olarak gösterir. Rapor, bilgisayarları hazırda bekleme özelliğine sahip olmamaları ve belirtilen rapor aralığı boyunca açık kalmış olmaları durumunda **Hazırda bekleme özellikli değil** olarak gösterir.  

> [!NOTE]  
>  Güç yönetimi, yalnızca Windows 7 veya Windows Server 2008 R2 çalıştıran bilgisayarların uyku ya da bekleme moduna geçmesini engelleyen nedenleri toplayabilir.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Rapor aralığı (gün)**|Raporlanacak gün sayısını belirtin. Varsayılan değer **7** gündür. En yüksek değer **365** gündür. Raporu bugünlük çalıştırmak için **0** değerini belirleyin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Uyku Moduna Geçmeyen Bilgisayar Ayrıntıları**|Seçili nedenle uyku veya bekleme moduna geçemeyen bilgisayarların listesini görmek için **Etkilenen Bilgisayarlar** sütunundaki bir sayıya tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) bölümüne bakın.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Güç Özellikleri raporu  
 **Güç Özellikleri** raporu, belirtilen koleksiyondaki bilgisayarların güç yönetimi donanım özelliklerini görüntüler. Bu rapor genellikle, kuruluşunuzdaki bilgisayarların güç yönetimi özelliklerini belirlemek amacıyla güç yönetiminin izleme aşamasında kullanılır. Raporda görüntülenen bilgiler, daha sonra güç planlarının uygulanacağı veya güç yönetiminin dışında tutulacak bilgisayar koleksiyonlarını oluşturmak üzere kullanılabilir. Bu rapor tarafından görüntülenen güç yönetimi özellikleri şunlardır:  

- **Uyku Özellikli** – Bilgisayarın, yapılandırılması durumunda uyku moduna geçme özelliğine sahip olup olmadığını belirtir.  

- **Hazırda Bekleme Özellikli** – Bilgisayarın, yapılandırılması durumunda hazırda bekleme moduna geçme özelliğine sahip olup olmadığını belirtir.  

- **Uykudan Uyanma** – Bilgisayarın, yapılandırılması durumunda uyku modundan uyanma özelliğine sahip olup olmadığını belirtir.  

- **Hazırda Beklemeden Çıkma** – Bilgisayarın, yapılandırılması durumunda hazırda bekleme modundan çıkma özelliğine sahip olup olmadığını belirtir.  

  **Güç Özellikleri** raporu tarafından bildirilen değerler, bilgisayarların uyku ve hazırda bekleme özelliği olup olmadığını Windows tarafından raporlandığı şekilde gösterir. Ancak bildirilen değerler, Windows veya BIOS ayarlarının bu işlevlerin çalışmasını engellediği durumları yansıtmaz.  

  Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  
|**Görüntüleme Filtresi**|Aşağı açılan listeden, yalnızca belirtilen koleksiyonda uyku, hazırda bekleme, uyku modundan çıkma veya hazırda beklemeden uyanma özellikli bilgisayarları göstermek için **desteklenmez** ' i seçin. Belirtilen koleksiyondaki tüm bilgisayarları görüntülemek için **Tümünü göster** ' i seçin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Bu rapor için ayarlanabilecek gizli parametre yok.  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Ayrıntıları**|Güç özelliklerini, güç ayarlarını ve seçili bilgisayar için uygulanan güç planlarını görmek için bir bilgisayar adına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Computer Details Report](#BKMK_Computer_Details) bölümüne bakın.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Güç Ayarları raporu  
 **Güç Ayarları** raporu, belirtilen koleksiyondaki bilgisayarlar tarafından kullanılan güç ayarlarının toplu listesini görüntüler. Her güç ayarı için olası güç modları, değerler ve birimler, söz konusu değerleri kullanan bilgisayar sayısıyla birlikte görüntülenir. Bu rapor, yöneticinin sitedeki bilgisayarların kullandığı mevcut güç ayarlarını anlamasına ve ideal güç ayarlarının güç yönetimi planı aracılığıyla planlanmasına yardımcı olmak amacıyla, güç yönetiminin izleme aşamasında kullanılabilir. Rapor ayrıca, güç ayarlarının doğru şekilde uygulanıp uygulanmadığını doğrulamak amacıyla sorun giderme işlemi yapmak için de kullanılabilir.  

> [!NOTE]  
>  Görüntülenen ayarlar, donanım envanteri sırasında istemci bilgisayarlardan toplanır. Donanım envanterinin çalıştığı zamana bağlı olarak, yoğun saatlerde güç kullanım planının veya yoğun saatler dışında güç kullanım planının uygulandığı süreye ait ayarlar toplanabilir.  

 Bu raporu yapılandırmak için aşağıdaki parametreleri kullanın.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon adı**|Aşağı açılan listeden, bu rapor için bir koleksiyon seçin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**numberOfLocalizations**|İstemci bilgisayarlar tarafından raporlanan güç ayarı adlarını görüntülemek istediğiniz dil sayısını seçin. Yalnızca en popüler dilde görüntülemek istiyorsanız varsayılan **1**değerini değiştirmeyin. Tüm dilleri görüntülemek için bu değeri **0**olarak ayarlayın.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Güç Ayarları Ayrıntıları**|Söz konusu satırdaki güç ayarlarını kullanan tüm bilgisayarların listesini görmek için **Bilgisayarlar** sütunundaki bilgisayar sayısına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Power Settings Details Report](#BKMK_Settings_Details) bölümüne bakın.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 **Güç Ayarları Ayrıntıları** raporu, **Güç Ayarları** raporunda seçilen bilgisayarlar hakkında daha fazla bilgi görüntüler. Bu rapor, **Güç Ayarları** raporu tarafından çağrılır ve doğrudan site yöneticisi tarafından çalıştırılmak üzere tasarlanmamıştır.  

#### <a name="required-report-parameters"></a>Gerekli rapor parametreleri  
 Bu raporun çalıştırılması için aşağıdaki parametreler belirtilmelidir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**Koleksiyon**|Aşağı açılan listeden, bu rapor için kullanılacak bir koleksiyon seçin.|  
|**Güç Ayarı GUID’i**|Aşağı açılan listeden, raporlamak istediğiniz güç ayarı GUID’ini seçin. Tüm güç ayarlarının ve kullanımları listesi için bkz. [Güç planlarını oluşturma ve uygulama](../../../../core/clients/manage/power/create-and-apply-power-plans.md)konusundaki [kullanılabilir güç yönetimi planı ayarları](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) .|  
|**Güç modu**|Aşağı açılan listeden, rapor sonuçlarında görüntülemek istediğiniz güç ayarlarının türünü seçin. Bilgisayarın prize takılı olduğu durumlar için yapılandırılan güç ayarlarını görüntülemek üzere **Prize Takılı** ’yı, bilgisayarın pil gücünden çalıştığı durumlar için yapılandırılan güç ayarlarını görüntülemek üzere **Pilde** ’yi seçin.|  
|**Ayar Dizini**|Aşağı açılan listeden, raporlamak istediğiniz seçili güç ayarı adı için bir değer seçin. Örneğin, **sabit diski kapatmak için beklenecek süre** ayarı **10** dakika olarak ayarlanan tüm bilgisayarları görüntülemek istiyorsanız, **Güç Ayarı Adı** için **sabit diski kapatmak için beklenecek süre** seçeneğini ve **Ayar Dizini** için **10**değerini belirtin.|  

#### <a name="hidden-report-parameters"></a>Gizli rapor parametreleri  
 Aşağıdaki gizli parametreler, bu raporun davranışını değiştirmek için isteğe bağlı olarak belirtilebilir.  

|Parametre Adı|Açıklama|  
|--------------------|-----------------|  
|**numberOfLocalizations**|İstemci bilgisayarlar tarafından raporlanan güç ayarı adlarını görüntülemek istediğiniz dil sayısını seçin. Yalnızca en popüler dilde görüntülemek istiyorsanız varsayılan **1**değerini değiştirmeyin. Tüm dilleri görüntülemek için bu değeri **0**olarak ayarlayın.|  

#### <a name="report-links"></a>Rapor bağlantıları  
 Bu rapor, seçili öğe hakkında daha fazla bilgi sağlayan aşağıdaki raporun bağlantılarını içerir.  

|Rapor Adı|Ayrıntılar|  
|-----------------|-------------|  
|**Bilgisayar Ayrıntıları**|Güç özelliklerini, güç ayarlarını ve seçili bilgisayar için uygulanan güç planlarını görmek için bir bilgisayar adına tıklayın.<br /><br /> Daha fazla bilgi için bu konunun [Computer Details Report](#BKMK_Computer_Details) bölümüne bakın.|  
