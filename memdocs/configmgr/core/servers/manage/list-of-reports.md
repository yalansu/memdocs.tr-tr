---
title: Rapor listesi
titleSuffix: Configuration Manager
description: Configuration Manager ile sağlanan raporların listesini gözden geçirin. Raporlar çeşitli kategorilerde görüntülenir.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713768"
---
# <a name="list-of-reports-in-configuration-manager"></a>Configuration Manager raporların listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, yapmak isteyebileceğiniz birçok raporlama görevini kapsayan çok sayıda yerleşik rapor sağlar. Kendi raporlarınızı yazmak için bu raporlardaki SQL deyimlerini de kullanabilirsiniz.   

Aşağıdaki raporlar Configuration Manager eklenmiştir. Raporlar çeşitli kategorilerde görüntülenir.  



## <a name="administrative-security"></a>Yönetim güvenliği  

Aşağıdaki altı rapor **Yönetim güvenliği** kategorisi altında listelenir.  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Yönetim etkinlik günlüğü**|Yönetici kullanıcılar, güvenlik rolleri, güvenlik kapsamları ve koleksiyonlar için yapılan yönetim değişikliklerinin kaydını görüntüler.|  
|**Yönetim kullanıcıları güvenlik atamaları**|Yönetim kullanıcılarını, bunlarla ilişkilendirilmiş güvenlik rollerini ve her kullanıcıya ait güvenlik rolleriyle ilişkilendirilmiş güvenlik kapsamlarını görüntüler.|  
|**Tek bir güvenlik kapsamıyla korunan nesneler**|Bir yöneticinin yalnızca belirtilen güvenlik kapsamına atadığı nesneleri görüntüler. Bu rapor, bir yöneticinin birden fazla güvenlik kapsamıyla ilişkilendiğini nesneleri görüntülemez.|  
|**Belirli veya birden çok Configuration Manager nesneleri için güvenlik**|Güvenliği sağlanabilir nesneleri, bu nesnelerle ilişkilendirilmiş güvenlik kapsamlarını ve nesneler için izne sahip olan yönetim kullanıcılarını görüntüler.|  
|**Güvenlik rolleri özeti**|Güvenlik rollerini ve her rolle ilişkili Configuration Manager yöneticilerini görüntüler.|  
|**Güvenlik kapsamları özeti**|Güvenlik kapsamlarını ve her bir kapsamla ilişkili Configuration Manager yönetici kullanıcıları ve güvenlik gruplarını görüntüler.|  



## <a name="alerts"></a>Uyarılar  

Aşağıdaki iki rapor **Uyarılar** kategorisi altında listelenir.  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Uyarı puan kartı**|Belirtilen başlangıç ve bitiş tarihleri arasında oluşturulan ertelenmiş tüm uyarıların özetini görüntüler.|  
|**En Sık Oluşturulan Uyarılar**|Geçerli tarihle belirtilen özellik alanı için belirtilen tarih arasında en sık oluşturulan uyarıların özetini görüntüler.|  



## <a name="asset-intelligence"></a>Varlık Yönetim Bilgileri  

Aşağıdaki 67 raporları **varlık yönetim bilgileri** kategorisi altında listelenir.  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Donanım 01A - Belirli bir koleksiyondaki bilgisayarların özeti**|Belirttiğiniz bir koleksiyondaki bilgisayarların Varlık Yönetim Bilgileri özet görünümünü görüntüler.|  
|**Donanım 03A - Birincil bilgisayar kullanıcıları**|Kullanıcıları ve bunların birincil Kullanıcı oldukları bilgisayar sayısını görüntüler.|  
|**Donanım 03B - Belirli bir birincil konsol kullanıcının bilgisayarları**|Belirtilen kullanıcının birincil konsol kullanıcısı olduğu tüm bilgisayarları görüntüler.|  
|**Donanım 04A - Birden çok kullanıcıya sahip bilgisayarlar (paylaşılan)**|Birincil kullanıcısı olmayan bilgisayarları görüntüler çünkü hiç bir Kullanıcı %66 ' den büyük bir oturum açmamıştır.|  
|**Donanım 05A - Belirli bir bilgisayardaki konsol kullanıcıları**|Belirtilen bir bilgisayardaki tüm konsol kullanıcılarını görüntüler.|  
|**Donanım 06A - Algılanamayan konsol kullanıcılarının bilgisayarları**|Yönetim kullanıcılarının güvenlik oturumu açmayı etkinleştirmesi gereken sistemleri tanımlamasına yardımcı olur.|  
|**Donanım 07A - Üreticisine göre USB cihazları**|Üreticisine göre gruplandırılmış USB cihazlarını görüntüler.|  
|**Donanım 07B - Üreticisine ve açıklamaya göre USB cihazları**|Üreticisine ve açıklamaya göre gruplandırılmış USB cihazlarını görüntüler.|  
|**Donanım 07C - Belirli bir USB cihazı içeren bilgisayarlar**|Belirtilen USB cihazını içeren tüm bilgisayarları görüntüler.|  
|**Donanım 07D - Belirli bir cihazdaki USB cihazları**|Belirtilen bir bilgisayardaki tüm USB cihazlarını görüntüler.|  
|**Donanım 08A - Yazılım yükseltmesi için hazır olmayan donanım**|En düşük donanım gereksinimlerini karşılamayan donanımları görüntüler.|  
|**Donanım 09A - Bilgisayar arama**|Anahtar sözcük filtreleriyle eşleşen bilgisayarların özetini görüntüler. Bu filtreler bilgisayar adı, Configuration Manager sitesi, etki alanı, üst konsol kullanıcısı, işletim sistemi, üretici veya modeldir.|  
|**Donanım 10A - Belirtilen zaman çerçevesinde değiştirilmiş bir koleksiyondaki bilgisayarlar**|Belirtilen süre içinde donanım sınıfı değiştirilmiş bir koleksiyondaki bilgisayarların listesini görüntüler.|  
|**Donanım 10B - Belirtilen zaman çerçevesi içinde belirtilen bir bilgisayardaki değişiklikler**|Belirtilen süre içinde belirtilen bir bilgisayarda değiştirilen sınıfları görüntüler.|  
|**Lisans 01A - Microsoft lisans bildirimleri için Microsoft Toplu Lisans defteri**|Microsoft Toplu Lisanslama programında bulunan tüm Microsoft yazılım başlıklarının envanterini görüntüler.|  
|**Lisans 01B - Satış kanallarına göre Microsoft Toplu Lisans defteri öğesi**|Envantere kaydedilen Microsoft Toplu Lisans yazılımı için satış kanallarını tanımlar ve görüntüler.|  
|**Lisans 01C - Belirli bir Microsoft Toplu Lisans defteri öğesine ve satış kanalına sahip bilgisayarlar**|Microsoft Toplu lisans defterindeki belirli bir öğeyi içeren bilgisayarları tanımlar ve görüntüler.|  
|**Lisans 01D - Belirli bir bilgisayardaki Microsoft Toplu Lisans defteri ürünleri**|Belirtilen bilgisayardaki tüm Microsoft Toplu lisans defteri öğelerini tanımlar ve görüntüler.|  
|**Lisans 02A - Zaman aralıklarına göre süresi dolmak üzere olan lisans sayısı**|Belirtilen zaman aralığına süresi dolmak üzere olan lisans sayısı. Görüntülenmiş ürünlerin lisansları Yazılım Lisanslama hizmeti tarafından yönetiliyor.|  
|**Lisans 02B - Lisans süresi dolmak üzere olan bilgisayarlar**|Lisans süresi dolmak üzere olan belirtilen bilgisayarları görüntüler.|  
|**Lisans 02C - Belirli bir bilgisayardaki lisans bilgileri**|Belirtilen bilgisayarda, lisansları Yazılım Lisans Hizmeti tarafından yönetilen ürünleri görüntüler.|  
|**Lisans 03A - Lisans durumuna göre lisans sayısı**|Lisansları Yazılım Lisans Hizmeti tarafından yönetilen ürünleri lisans durumuna göre görüntüler.|  
|**Lisans 03B - Belirli bir lisans durumuna sahip bilgisayarlar**|Lisansları Yazılım Lisans Hizmeti tarafından yönetilen belirtilen lisans durumuna sahip ürünleri görüntüler.|  
|**Lisans 04A - Yazılım lisansı tarafından yönetilen ürün sayısı**|Lisansları Yazılım Lisans Hizmeti tarafından yönetilen ürün sayısını görüntüler.|  
|**Lisans 04B - Yazılım Lisans Hizmeti tarafından belirli bir ürüne sahip bilgisayarlar**|Yazılım Lisanslama hizmeti tarafından yönetilen, belirtilen bir ürünü içeren bilgisayarları görüntüler.|  
|**Lisans 05A - Anahtar Yönetim Hizmeti sağlayan bilgisayarlar**|Anahtar Yönetim Sunucusu olarak davranan bilgisayarları görüntüler.|  
|**Lisans 06A - İşlemci başına lisanslanan ürünler için işlemci sayısı**|İşlemci başına lisanslamayı desteğini kullanan Microsoft ürünlerini kullanan bilgisayarlardaki işlemci sayısını görüntüler.|  
|**Lisans 06B - İşlemci başına lisanslamayı destekleyen belirli bir ürüne sahip bilgisayarlar**|İşlemci başına lisanslamayı destekleyen belirtilen Microsoft ürününün yüklü olduğu bilgisayarların listesini görüntüler.|  
|**Lisans 14A - Microsoft Toplu Lisanslama mutabakat raporu**|Microsoft toplu lisans sözleşmesi aracılığıyla alınan yazılım lisanslarındaki mutabakatı ve gerçek envanter sayısını görüntüler.|  
|**Lisans 14B - MVLS’de bulunamayan Microsoft yazılım envanterinin listesi**|Bu rapor, Microsoft toplu lisans sözleşmesinde bulunmayan kullanımdaki Microsoft yazılım başlıklarını görüntüler.|  
|**Lisans 15A - Genel lisans mutabakat raporu**|Alınan genel yazılım lisanslarındaki mutabakatı ve gerçek envanter sayısını görüntüler.|  
|**Lisans 15B - Bilgisayara göre genel lisans mutabakat raporu**|Belirtilen bir sürüme sahip lisanslı ürünün yüklü olduğu bilgisayarları görüntüler.|  
|**Yazılım 01A - Belirli bir koleksiyondaki yüklü yazılımların özeti**|Envanterde bulunan örnek sayısına göre sıralanmış yüklü yazılımların özetini görüntüler.|  
|**Yazılım 02A - Belirli bir koleksiyon için ürün aileleri**|Ürün ailelerini ve belirtilen koleksiyon için bu ailedeki yazılım sayısını görüntüler.|  
|**Yazılım 02B - Belirli bir ürün ailesi için ürün kategorileri**|Belirtilen ürün ailesindeki ürün kategorilerini ve kategorideki yazılım sayısını görüntüler.|  
|**Yazılım 02C - Belirli bir ürün ailesindeki ve kategorideki yazılım**|Belirtilen ürün ailesinde ve kategorisindeki tüm yazılımları görüntüler.|  
|**Yazılım 02D - Belirli bir yazılımın yüklü olduğu bilgisayar**|Belirtilen yazılımın yüklü olduğu tüm bilgisayarları görüntüler.|  
|**Yazılım 02E - Belirli bir bilgisayarda yüklü olan yazılım**|Belirtilen bilgisayardaki yüklü tüm yazılımları görüntüler.|  
|**Yazılım 03A - Kategorilere ayrılmamış yazılım**|Bilinmeyen olarak kategorilere ayrılmış veya kategorisi olmayan yazılımı görüntüler.|  
|**Yazılım 04A - Bilgisayarlarda otomatik olarak çalışacak şekilde yapılandırılmış yazılım**|Bilgisayarlarda otomatik olarak çalışacak şekilde yapılandırılmış yazılımların listesini görüntüler.|  
|**Yazılım 04B - Otomatik olarak çalışacak şekilde yapılandırılmış belirli bir yazılıma sahip bilgisayarlar**|Otomatik olarak çalışacak şekilde yapılandırılmış belirli yazılıma sahip tüm bilgisayarları görüntüler.|  
|**Yazılım 04C - Belirli bir bilgisayarda otomatik olarak çalışacak şekilde yapılandırılmış yazılım**|Belirtilen bilgisayarda otomatik olarak çalışacak şekilde yapılandırılmış yüklü yazılımı görüntüler.|  
|**Yazılım 05A - Tarayıcı Yardımcısı Nesneleri**|Belirtilen bir koleksiyondaki bilgisayarlarda yüklü olan tarayıcı yardımcı nesnelerini görüntüler.|  
|**Yazılım 05B - Belirli bir Tarayıcı Yardımcısı Nesnesine sahip bilgisayarlar**|Belirtilen tarayıcı yardımcısı nesnesine sahip tüm bilgisayarları görüntüler.|  
|**Yazılım 05C - Belirli bilgisayardaki Tarayıcı Yardımcısı Nesneleri**|Belirtilen bilgisayardaki tüm tarayıcı yardımcı nesnelerini görüntüler.|  
|**Yazılım 06A - Yüklü yazılım arama**|Bu rapor, yüklü yazılımların özetini sağlar. Şu ölçütlere göre arama yapar: ürün adı, yayımcı veya sürüm.|  
|**Yazılım 06B - Ürün adına göre yazılım**|Belirtilen ürün adına bağlı olarak yüklü yazılımların özetini görüntüler.|  
|**Yazılım 07A - Bilgisayar sayısına göre son kullanılan yürütülebilir programlar**|Kullanıcıların yakın zamanda kullandığı yürütülebilir programları görüntüler. Ayrıca, kullanıcıların programı kullandığı bilgisayar sayısını da içerir. Raporu görüntülemek için yazılım kullanım ölçümü bu sitede etkinleştirilmelidir.|  
|**Yazılım 07B - Kısa süre önce yürütülebilir program kullanan bilgisayarlar**|Kullanıcıların belirtilen yürütülebilir programı son zamanlarda kullandığı bilgisayarları görüntüler. Bu rapor, yazılım ölçer istemci ayarını etkinleştirmenizi gerektirir.|  
|**Yazılım 07C - Belirtilen bilgisayardaki son kullanılan yürütülebilir programlar**|Kullanıcıların belirli bir bilgisayarda kısa süre önce kullandığı yürütülebilir dosyaları görüntüler. Bu rapor, yazılım ölçer istemci ayarını etkinleştirmenizi gerektirir.|  
|**Yazılım 08A - Kullanıcı sayısına göre son kullanılan yürütebilir programlar**|Kullanıcıların yakın zamanda kullandığı yürütülebilir programları görüntüler. Ayrıca, programı en son kullanan kullanıcı sayısını da içerir. Bu rapor, yazılım ölçer istemci ayarını etkinleştirmenizi gerektirir.|  
|**Yazılım 08B - Belirtilen yürütülebilir programı kullanan son kullanıcılar**|Belirtilen yürütülebilir programı en son kullanan kullanıcıları görüntüler. Bu rapor, yazılım ölçer istemci ayarını etkinleştirmenizi gerektirir.|  
|**Yazılım 08C - Belirtilen kullanıcıya göre son kullanılan yürütülebilir programlar**|Belirtilen kullanıcının son zamanlarda kullandığı yürütülebilir programları görüntüler. Bu rapor, yazılım ölçer istemci ayarını etkinleştirmenizi gerektirir.|  
|**Yazılım 09A - Sık kullanılmayan yazılımlar**|Kullanıcıların belirli bir süre boyunca kullanmayan yazılım başlıklarını görüntüler.|  
|**Yazılım 09B - Sık kullanılmayan yazılımların yüklü olduğu bilgisayarlar**|Kullanıcıların belirli bir süre boyunca kullanmamış yüklü yazılımları olan bilgisayarları görüntüler. 'Yazılım 09A - Sık kullanılmayan yazılımlar' raporunda belirtilen değere bağlı olarak belirtilen süre.|  
|**Yazılım 10A - Birden çok özel etiketlerin tanımlandığı yazılım başlıkları**|Eşleşen tüm belirtilmiş özel etiket ölçütüne göre yazılım başlıklarını görüntüler. Yazılım başlığı aramasını iyileştirmek için en fazla üç özel etiket seçilebilir.|  
|**Yazılım 10B - Özel etikete sahip yazılımların yüklü olduğu bilgisayarlar**|Belirtilen özel etiketli yazılımların yüklü olduğu bu koleksiyonda yer alan tüm bilgisayarları görüntüler.|  
|**Yazılım 11A - Belirli bir özel etiketin tanımlandığı yazılım başlıkları**|Eşleşen belirtilmiş özel etiket ölçütüne dayanan yazılım başlıklarından en az birini görüntüler.|  
|**Yazılım 12A - Özel etiketi olmayan yazılım başlıkları**|Özel bir etiket tanımlanmamış tüm yazılım başlıklarını görüntüler.|  
|**Yazılım 14A - Yazılım tanımlama etiketi etkinleştirilmiş yazılım arama**|Yazılım kimliği etiketi etkin olan yüklü yazılım sayısını görüntüler.|  
|**Yazılım 14B - Belirli bir yazılım kimliği etiketi etkin olan yüklü yazılımlara sahip bilgisayarlar**|Belirtilen yazılım tanımlama etiketi etkinleştirilmiş olan yüklü yazılımlara sahip tüm bilgisayarları görüntüler.|  
|**Yazılım 14C - Belirtilen bir bilgisayardaki yazılım kimliği etiketi etkin olan yüklü yazılımlar**|Belirtilen bir bilgisayardaki belirtilen yazılım kimliği etiketi etkin olan tüm yüklü yazılımları görüntüler.|  
|**Yaşam döngüsü 01A-belirli bir yazılım ürünü olan bilgisayarlar**|Belirtilen bir ürünün algılandığı bilgisayarların listesini görüntüleyin.|
|**Yaşam döngüsü 02A-kuruluşta süresi geçen ürünlere sahip makinelerin listesi**|Zaman aşımına ermeyen ürünlerin bulunduğu bilgisayarları görüntüleyin. Bu raporu ürün adına göre filtreleyebilirsiniz.|
|**Yaşam döngüsü 03A-kuruluşta bulunan süresi biten ürünlerin listesi**|Ortamınızdaki, süresi dolma ömrü tarihleri bulunan ürünlerin ayrıntılarını görüntüleyin.|
|**Yaşam döngüsü 04A-genel ürün yaşam döngüsüne genel bakış**|Ürün kullanım ömrü listesini görüntüleyin. Listeyi ürün adına ve günlere göre zaman aşımına göre filtreleyin.|
|**Yaşam döngüsü 05A-ürün yaşam döngüsü panosu**|Sürüm 1810 ' den başlayarak bu rapor, konsol içi pano olarak benzer bilgiler içerir.|



## <a name="client-push"></a>İstemci gönderme  

Aşağıdaki dört rapor, **Istemci gönderme** kategorisi altında listelenir.  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**İstemci gönderme yükleme durumu ayrıntıları**|Tüm siteler için istemci gönderme yükleme işlemi bilgilerini görüntüler.|  
|**Belirtilen site için istemci gönderme yükleme durumu ayrıntıları**|Belirtilen site için istemci gönderme yükleme işlemi bilgilerini görüntüler.|  
|**İstemci gönderme yükleme durum özeti**|Tüm siteler için istemci gönderme yükleme durumuna ilişkin özet görünümünü görüntüler.|  
|**Belirtilen site için istemci gönderme yükleme durumu özeti**|Belirtilen site için istemci gönderme yükleme durumunun özet görünümünü görüntüler.|  



## <a name="client-status"></a>İstemci durumu  

Aşağıdaki yedi rapor, **Istemci durumu** kategorisi altında listelenir.  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**İstemci düzeltme ayrıntıları**|Belirttiğiniz koleksiyon için istemci düzeltme eylemlerinin ayrıntılarını görüntüler.|  
|**İstemci düzeltme özeti**|Belirtilen koleksiyon için istemci düzeltme eylemlerinin özetini görüntüler.|  
|**İstemci durumu geçmişi**|Sitedeki genel istemci durumunun geçmiş görünümünü görüntüler.|  
|**İstemci durumu özeti**|Verilen bir koleksiyon için etkin istemcilerin istemci denetim sonuçlarını görüntüler.|  
|**İstemci ilke istek süresi**|Son 30 gün içinde en az bir kez ilke isteyen istemcilerin yüzdesini görüntüler. Her gün, döngüdeki ilk günden bu yana ilkeyi istenen toplam istemcilerin yüzdesini temsil eder.|  
|**Başarısız istemci denetimi ayrıntılarına sahip istemciler**|Belirtilen bir koleksiyon için istemci denetimi başarısız olan istemcilerin ayrıntılarını görüntüler.|  
|**Etkin olmayan istemci ayrıntıları**|Verilen bir koleksiyon için etkin olmayan istemcilerin ayrıntılı listesini görüntüler.|  



## <a name="company-resource-access"></a>Şirket kaynak erişimi  

Aşağıdaki üç rapor, **Şirket kaynağı erişim** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Sertifika verme geçmişi**|Belirtilen tarih aralığı için, sertifika kayıt noktası tarafından kullanıcılara ve cihazlara verilen sertifikaların geçmişini görüntüler.|  
|**Sertifika verme durumuna göre varlıkların listesi**|Belirtilen bir sertifika profili değerlendirmesinin ardından belirtilen sertifika verme durumundaki cihazları veya kullanıcıları görüntüler.|  
|**Süresi dolmak üzere sertifikalara sahip varlıkların listesi**|Belirtilen tarihte veya bu tarihten önce süresi dolacak sertifikalara sahip cihazları veya kullanıcıları görüntüler.|  



## <a name="compliance-and-settings-management"></a>Uyumluluk ve ayarlar yönetimi  

Aşağıdaki 22 rapor, **Uyumluluk ve ayarlar yönetimi** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Yapılandırma temelinin uyumluluk geçmişi**|Belirtilen tarih aralığı için yapılandırma temeliyle uyumlu değişikliklerin geçmişini görüntüler.|  
|**Yapılandırma öğesinin uyumluluk geçmişi**|Belirtilen tarih aralığı için yapılandırma öğesiyle uyumlu değişikliklerin geçmişini görüntüler.|  
|**Bir varlığın yapılandırma temelindeki yapılandırma öğelerine ait uyumlu kuralların ayrıntıları**|Belirtilen bir cihaz veya Kullanıcı için belirtilen bir yapılandırma öğesi için uyumlu olarak değerlendirilen kurallarla ilgili bilgileri görüntüler.|  
|**Bir varlığın yapılandırma temelindeki yapılandırma öğelerine ait çakışan kuralların ayrıntıları**|Diğer kurallarla çakışan dağıtılmış bir yapılandırma öğesindeki kurallarla ilgili bilgileri görüntüler. Diğer kuralları aynı veya dağıtılan başka bir yapılandırma öğesine dahil edin.|  
|**Bir varlığın yapılandırma temelindeki yapılandırma öğelerinin hata ayrıntıları**|Belirtilen bir cihaz veya kullanıcı için belirtilen bir yapılandırma öğesi tarafından oluşturulan hatalara ilişkin bilgileri görüntüler.|  
|**Bir varlığın yapılandırma temelindeki yapılandırma öğelerinin uyumlu olmayan kurallarına ilişkin ayrıntılar**|Belirtilen bir cihaz veya kullanıcı için belirtilen bir yapılandırma öğesi için uyumsuz olarak değerlendirilen kurallarla ilgili bilgileri görüntüler.|  
|**Bir varlığın yapılandırma temelindeki yapılandırma öğelerine ait düzeltilmiş kuralların ayrıntıları**|Belirtilen bir cihaz veya kullanıcı için belirtilen bir yapılandırma öğesi tarafından düzeltilen kurallarla ilgili bilgileri görüntüler.|  
|**Yapılandırma temeli için uyumluluk durumuna göre varlıkların listesi**|Belirtilen bir yapılandırma temelinin değerlendirmesinin ardından belirtilen uyumluluk durumundaki cihazları veya kullanıcıları görüntüler.|  
|**Yapılandırma temelindeki yapılandırma öğesinin uyumluluk durumuna göre varlıkların listesi**|Belirtilen bir yapılandırma öğesinin değerlendirmesinin ardından belirtilen uyumluluk durumundaki cihazları veya kullanıcıları görüntüler.|  
|**Belirtilen kullanıcı için uyumlu olmayan Uygulama ve Cihazların listesi**|Belirttiğiniz bir ilkeyle uyumlu olmayan uygulamaların yüklendiği kullanıcılar ve cihazlar hakkındaki bilgileri görüntüler.|  
|**Bir varlık için belirtilen bir kuralla çakışan kuralların listesi**|Dağıtılan bir yapılandırma öğesi için belirtilen bir kuralla çakışan kuralların listesini görüntüler.|  
|**Yapılandırma temeli için bilinmeyen varlıkların listesi**|Belirli bir yapılandırma temeli için henüz uyumluluk verileri bildirmemiş cihazların veya kullanıcıların listesini görüntüler.|  
|**Bir yapılandırma öğesi için bilinmeyen varlıkların listesi**|Belirli bir yapılandırma öğesi için uyumluluk verilerini henüz bildirmemiş cihazların veya kullanıcıların listesini görüntüler.|  
|**Bir varlığın yapılandırma temelindeki yapılandırma öğelerinin kurallar ve hatalar özeti**|Belirli bir yapılandırma öğesi için kuralların uyumluluk durumunun ve varsa ayar hatalarının özetini görüntüler. Yapılandırma öğesinin bir cihaza veya kullanıcıya dağıtılması gerekir.|  
|**Yapılandırma temeline göre uyumluluk özeti**|Hiyerarşideki dağıtılmış yapılandırma temellerinin genel uyumluluk özetini görüntüler.|  
|**Yapılandırma temelinin yapılandırma öğelerine göre uyumluluk özeti**|Belirtilen bir yapılandırma temelindeki yapılandırma öğelerinin uyumluluk özetini görüntüler.|  
|**Yapılandırma ilkelerine göre uyumluluk özeti**|Yapılandırma ilkelerinin uyumluluk özetini görüntüler.|  
|**Bir koleksiyonun yapılandırma temelinin uyumluluk özeti**|Belirtilen bir yapılandırma temelinin genel uyumluluğunun özetini görüntüler. Yapılandırma öğesinin belirtilen koleksiyona dağıtılması gerekir.|  
|**Uyumlu Olmayan Uygulamalara Sahip Kullanıcıların Özeti**|Belirttiğiniz bir ilkeyle uyumlu olmayan uygulamaların yüklendiği kullanıcılar hakkındaki bilgileri görüntüler.|  
|**Hüküm ve Koşulların kabulü**|Hüküm ve Koşulları öğelerini ve her bir kullanıcının hangi sürümü kabul ettiğini gösterir.|  



## <a name="data-warehouse"></a>Veri ambarı  

Aşağıdaki yedi rapor, **veri ambarı** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Uygulama dağıtımı**|Geçmiş: belirli bir uygulama ve makine için uygulama dağıtımına ilişkin ayrıntıları görüntüleyin.|
|**Endpoint Protection ve Yazılım Güncelleştirme Uyumluluğu**|Geçmiş: eksik yazılım güncelleştirmeleri olan bilgisayarları görüntüleyin.|
|**Genel donanım envanteri**|Geçmiş: belirli bir makine için tüm donanım envanterini görüntüleyin.|
|**Genel Yazılım envanteri**|Geçmiş: belirli bir makine için tüm yazılım envanterini görüntüleyin.|
|**Altyapı sistem durumuna genel bakış**|Geçmiş: Configuration Manager altyapınızın sistem durumuna genel bir bakış görüntüler.|
|**Algılanan kötü amaçlı yazılım listesi**|Geçmiş: kuruluşta algılanan kötü amaçlı yazılımları görüntüleyin.|
|**Yazılım dağıtım Özeti**|Geçmiş: belirli bir tanıtım ve makine için yazılım dağıtımının bir özeti.|


## <a name="device-management"></a>Cihaz yönetimi  

Aşağıdaki 37 raporları **cihaz yönetimi** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Şirkete ait tüm mobil cihazlar**|Şirkete ait tüm mobil cihazları görüntüler.|
|**Tüm mobil cihaz istemcileri**|Tüm mobil cihaz istemcileriyle ilgili bilgileri görüntüler. Exchange Server Bağlayıcısı tarafından yönetilen cihazlar dahil değildir.|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen ve iyi durumda olmayan mobil cihazlardaki sertifika sorunları**|Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlardaki sertifika sorunlarıyla ilgili ayrıntılı bilgileri görüntüler.|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için istemci dağıtım hatası**|Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için dağıtım hatasıyla ilgili ayrıntılı bilgileri görüntüler.|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için istemci dağıtım durumu ayrıntıları**|Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazların durumuyla ilgili bilgileri görüntüler.|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için istemci dağıtım başarısı**|Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için dağıtım başarısıyla ilgili ayrıntılı bilgileri görüntüler.|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen ve iyi durumda olmayan mobil cihazlardaki iletişim sorunları**|Bu rapor, Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlardaki iletişim sorunlarıyla ilgili ayrıntılı bilgiler içerir.|  
|**Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlar için varsayılan ActiveSync posta kutusu ilkesinin uyumluluk durumu**|Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlar için varsayılan Exchange ActiveSync posta kutusu ilkesiyle uyumluluk durumunun özetini görüntüler.|  
|**Ekran yapılandırmalarına göre mobil cihaz sayısı**|Bu raporda ekran ayarlarına göre mobil cihaz sayısı görüntülenir.|  
|**İşletim sistemine göre mobil cihaz sayısı**|İşletim sistemine göre mobil cihaz sayısını görüntüler.|  
|**Program belleğine göre mobil cihaz sayısı**|Program belleğine göre mobil cihaz sayısını görüntüler.|  
|**Depolama belleği yapılandırmalarına göre mobil cihaz sayısı**|Depolama belleği yapılandırmalarına göre mobil cihaz sayısı|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için sistem durumu bilgileri**|Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için ayrıntılı sistem durumu bilgilerini görüntüler.|  
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için sistem durumu özeti**|Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlar için sistem durumu Özet bilgilerini görüntüler.|  
|**Exchange Server bağlayıcısı tarafından yönetilen etkin olmayan mobil cihazlar**|Exchange Server Bağlayıcısı tarafından yönetilen ve belirtilen gün sayısı içinde bir Exchange Server 'a bağlı olmayan mobil cihazları görüntüler.|  
|**Cihaz durumu kanıtlama durumuna göre cihazların listesi**|Durum kanıtlama hizmeti tarafından bildirilen özniteliklere sahip cihazların listesini görüntüler|
|**Microsoft Intune’da kullanıcı başına kaydedilmiş cihazların listesi**|Kullanıcının Microsoft Intune kaydolduğu tüm cihazları görüntüler.|  
|**Belirli bir cihaz kategorisindeki cihazların listesi**|Belirli bir cihaz kategorisindeki tüm cihazlar için bilgi görüntüler.|
|**Windows CE için Configuration Manager istemcisi tarafından yönetilen ve iyi durumda olmayan mobil cihazlardaki yerel istemci sorunları**|Bu rapor, Windows CE için Configuration Manager istemcisi tarafından yönetilen mobil cihazlardaki yerel istemci sorunlarıyla ilgili ayrıntılı bilgiler içerir.|  
|**Mobil cihaz istemci bilgileri**|Configuration Manager istemcisinin yüklü olduğu mobil cihazlarla ilgili bilgileri görüntüler. Yönetim noktasıyla başarıyla iletişim kuran mobil cihazları doğrulamak için bu raporu kullanabilirsiniz.|  
|**Exchange Server bağlayıcısı için mobil cihaz uyumluluk ayrıntıları**|Exchange Server bağlayıcısını kullanarak yapılandırılan varsayılan Exchange ActiveSync posta kutusu ilkesi için mobil cihaz uyumluluk ayrıntılarını görüntüler.|  
|**İşletim sistemine göre mobil cihazlar**|İşletim sistemine göre mobil cihazları görüntüler.|  
|**İşletim sistemi kısıtlamaları kaldırılmış veya kök erişim izni verilmiş mobil cihazlar**|İşletim sistemi kısıtlamaları kaldırılmış veya kök erişim izni verilmiş mobil cihazları görüntüler.|  
|**Kaydedilmelerine karşın bir siteye atanamadıkları için yönetilmeyen mobil cihazlar**|Configuration Manager kaydı tamamlanan mobil cihazları görüntüler, sertifikaya sahip, ancak site atamasını tamamlayamadı.|  
|**Belirli miktarda boş program belleğine sahip mobil cihazlar**|Belirtilen miktarda boş program belleğine sahip tüm mobil cihazları görüntüler.|  
|**Belirli miktarda boş çıkarılabilir depolama birimi belleğine sahip mobil cihazlar**|Belirtilen miktarda boş çıkarılabilir belleğe sahip tüm mobil cihazları görüntüler.|  
|**Sertifika yenileme sorunlarına sahip mobil cihazlar**|Sertifikaları yenilenemeyen kayıtlı mobil cihazları görüntüler. Süre sonu süresinden önce sertifikayı yenilemezseniz, mobil cihazlar yönetilmeyen hale gelir.|  
|**Düşük seviyede boş program belleğine sahip mobil cihazlar (belirtilen boş KB’den az)**|Program belleğinin KB olarak belirtilen bir boyuttan düşük olduğu mobil cihazları görüntüler.|  
|**Düşük seviyede boş çıkarılabilir depolama birimi belleğine sahip mobil cihazlar (belirtilen boş KB’den az)**|Çıkarılabilir depolama birimi belleğinin KB olarak belirtilen bir boyuttan düşük olduğu mobil cihazları görüntüler.|  
|**Microsoft Intune kullanıcı başına kaydolan cihaz sayısı**|Microsoft Intune aboneliği için etkinleştirilen kullanıcıları görüntüler. Ayrıca, her kullanıcı için kaydedilmiş cihazların toplam sayısını gösterir.|  
|**Mobil cihazlar için bekleyen devre dışı bırakma ve silme isteği**|Mobil cihazlar için bekleyen silme isteklerini görüntüler.|  
|**En son kaydedilen ve atanan mobil cihazlar**|Configuration Manager en son kaydedilen ve bir siteye başarıyla atanan mobil cihazları görüntüler.|  
|**Son silinen mobil cihazlar**|Başarıyla silinen son mobil cihazların listesini görüntüler.|  
|**Exchange Server bağlayıcısı tarafından yönetilen mobil cihazlar için ayar özeti**|Exchange Server Bağlayıcısı tarafından yönetilen her varsayılan Exchange ActiveSync posta kutusu ilkesi için ayarları uygulayan mobil cihaz sayısını görüntüler.|  
|**Windows RT Dışarıdan Yükleme Anahtarları Ayrıntılı Durumu**|Belirtilen Windows RT dışarıdan yükleme anahtarı için ayrıntılı durum bilgilerini görüntüler.|  
|**Windows RT Dışarıdan Yükleme Anahtarı Özeti**|Windows RT dışarıdan yükleme anahtarlarının durumunu görüntüler.|  



## <a name="driver-management"></a>Sürücü yönetimi  

Aşağıdaki 13 rapor, **sürücü yönetimi** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Tüm sürücüler**|Tüm sürücülerin listesini görüntüler.|  
|**Belirli bir platform için tüm sürücüler**|Belirtilen platform için tüm sürücüleri görüntüler.|  
|**Belirli bir önyükleme görüntüsündeki tüm sürücüler**|Belirli bir önyükleme görüntüsündeki tüm sürücüleri görüntüler.|  
|**Belirli bir kategorideki tüm sürücüler**|Belirtilen bir kategorideki tüm sürücüleri görüntüler.|  
|**Belirli bir paketteki tüm sürücüler**|Belirtilen bir paketteki tüm sürücüleri görüntüler.|  
|**Belirli bir sürücü için kategoriler**|Belirtilen bir sürücü için kategorileri görüntüler.|  
|**Belirli bir koleksiyon için sürücülerin yüklenemediği bilgisayarlar**|Belirtilen bir koleksiyon için sürücülerin yüklenemediği bilgisayarları görüntüler.|  
|**Belirli bir koleksiyon için sürücü kataloğu eşleştirme raporu**|Belirtilen bir koleksiyon için sürücü kataloğu eşleştirme raporunu görüntüler.|  
|**Belirli bir bilgisayar için sürücü kataloğu eşleştirme raporu**|Belirtilen bir bilgisayar için sürücü kataloğu eşleştirme raporunu görüntüler.|  
|**Belirli bir bilgisayardaki belirli bir cihaz için sürücü kataloğu eşleştirme raporu**|Belirtilen bilgisayardaki belirtilen cihaz için sürücü kataloğu eşleştirme raporunu görüntüler.|  
|**Belirli bir cihazı içeren belirli bir koleksiyondaki bilgisayarlar için sürücü kataloğu eşleştirme raporu**|Belirtilen cihazı içeren belirtilen koleksiyondaki bilgisayarlar için sürücü kataloğu eşleştirme raporunu görüntüler.|  
|**Belirli bir bilgisayarda yüklenemeyen sürücüler**|Belirli bir bilgisayarda yüklenemeyen sürücüleri görüntüler.|  
|**Belirli bir Sürücü için desteklenen platformlar**|Belirtilen bir sürücü için desteklenen platformları görüntüler.|  



## <a name="endpoint-protection"></a>Uç Nokta Koruma  

Aşağıdaki altı rapor **Endpoint Protection** kategorisi altında listelenmiştir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Kötü amaçlı yazılımdan koruma etkinlik raporu**|Kötü amaçlı yazılımdan koruma etkinliğine yönelik genel bakışı görüntüler.|  
|**Kötü amaçlı yazılımdan koruma genel durumu ve geçmişi**|Kötü amaçlı yazılımdan koruma genel durumunu ve geçmişini görüntüler.|  
|**Bilgisayardaki kötü amaçlı yazılım ayrıntıları**|Belirtilen bilgisayar ve bu bilgisayarda bulunan kötü amaçlı yazılımların listesi hakkında ayrıntılı bilgileri görüntüler.|  
|**Virüslü bilgisayarlar**|Belirtilen tehdidin algılandığı bilgisayarların listesini görüntüler.|  
|**Tehditlere göre ilk kullanıcılar**|En fazla algılanan tehdide sahip kullanıcı listesini görüntüler.|  
|**Kullanıcı tehdit listesi**|Belirtilen kullanıcı hesabı için bulunan tehdit listesini görüntüler.|  



## <a name="hardware---cd-rom"></a>Donanım-CD-ROM  

Aşağıdaki dört rapor, **donanım-CD-ROM** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir bilgisayar için CD-ROM bilgileri**|Belirtilen bir bilgisayardaki CD-ROM sürücülerinin bilgilerini görüntüler.|  
|**Belirli bir CD-ROM üreticisi için bilgisayarlar**|Belirttiğiniz üretici tarafından üretilen CD-ROM’a sahip bilgisayarların listesini görüntüler.|  
|**Üretici başına CD-ROM sürücüsü sayısı**|Üretici başına envantere kaydedilmiş CD-ROM sürücülerinin sayısını görüntüler.|  
|**Geçmiş-belirli bir bilgisayar için CD-ROM geçmişi**|Belirtilen bir bilgisayardaki CD-ROM sürücüleri için envanter geçmişini görüntüler.|  



## <a name="hardware---disk"></a>Donanım-disk  

Aşağıdaki sekiz rapor, **donanım disk** kategorisi altında listelenir. 

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir sabit disk boyutuna sahip bilgisayarlar**|Belirtilen sabit disk boyutuna sahip bilgisayarların listesini görüntüler.|  
|**Düşük seviyede boş disk alanına sahip bilgisayarlar (belirtilen boş alan yüzdesinden az)**|Belirtilen koleksiyonda yer alan belirtilenden daha az boş disk alanına sahip bilgisayarların listesini görüntüler.|  
|**Düşük seviyede boş disk alanına sahip bilgisayarlar (belirtilen boş MB’den az)**|Düşük seviyede boş alana sahip bilgisayarların ve disklerin listesini görüntüler. Denetlenecek boş alan miktarı MB olarak belirtilir.|  
|**Fiziksel disk yapılandırması sayısı**|Disk kapasitesine göre envantere kaydedilen sabit disk sayısını görüntüler.|  
|**Belirli bir bilgisayar için disk bilgileri-mantıksal diskler**|Belirtilen bir bilgisayardaki mantıksal diskler hakkındaki özet bilgileri görüntüler.|  
|**Belirli bir bilgisayar için disk bilgileri - Bölümler**|Belirtilen bir bilgisayardaki disk bölümleri hakkındaki özet bilgileri görüntüler.|  
|**Belirli bir bilgisayar için disk bilgileri - Fiziksel diskler**|Belirtilen bir bilgisayardaki fiziksel diskler hakkındaki özet bilgileri görüntüler.|  
|**Geçmiş - Belirli bir bilgisayar için mantıksal disk alanı geçmişi**|Belirtilen bir bilgisayardaki mantıksal disk sürücüleri için envanter geçmişini görüntüler.|  



## <a name="hardware---general"></a>Donanım-genel  

Aşağıdaki beş rapor, **donanım-genel** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir bilgisayar için bilgisayar bilgileri**|Belirtilen bir bilgisayar için özet bilgileri görüntüler.|  
|**Belirli bir çalışma grubu veya etki alanındaki bilgisayarlar**|Belirtilen bir Çalışma Grubunda ve etki alanındaki bilgisayarların listesini görüntüler.|  
|**Belirli bir koleksiyona atanmış envanter sınıfları**|Belirtilen bir koleksiyona atanmış envanter sınıflarını görüntüler.|  
|**Belirli bir bilgisayarda etkin olan envanter sınıfları**|Belirtilen bilgisayarda etkin olan envanter sınıflarını görüntüler.|  
|**Windows AutoPilot cihaz bilgileri**|Windows AutoPilot kaydı için gereken istemci cihaz bilgilerini görüntüler.|



## <a name="hardware---memory"></a>Donanım-bellek  

Aşağıdaki beş rapor, **donanım bellek** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Fiziksel belleğin değiştirildiği bilgisayarlar**|En son envanter döngüsünden sonra RAM miktarının değiştirildiği bilgisayarların listesini görüntüler.|  
|**Belirli bellek miktarına sahip bilgisayarlar**|Belirtilen RAM (Toplam Fiziksel Bellek en yakın MB değerine yuvarlanır) miktarına sahip bilgisayarların listesini görüntüler.|  
|**Düşük belleğe (MB olarak belirtilen miktardan az veya buna eşit) sahip bilgisayarlar**|Belleği düşük olan bilgisayarların listesini görüntüler. Denetlenecek bellek miktarı MB olarak belirtilir.|  
|**Bellek yapılandırmalarının sayısı**|RAM miktarına göre envantere kaydedilmiş bilgisayar sayısını görüntüler.|  
|**Belirli bir bilgisayar için bellek bilgileri**|Belirtilen bir bilgisayarda bulunan bellek hakkındaki özet bilgileri görüntüler.|  



## <a name="hardware---modem"></a>Donanım-modem  

Aşağıdaki üç rapor, **donanım-modem** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir modem üreticisi için bilgisayarlar**|Belirtilen üretici tarafından üretilen modeme sahip bilgisayarların listesini görüntüler.|  
|**Üreticisine göre modem sayısı**|Her modem üreticisi için envantere kaydedilen modem sayısını görüntüler.|  
|**Belirli bir bilgisayar için modem bilgileri**|Belirtilen bir bilgisayarda bulunan modem hakkındaki özet bilgileri görüntüler.|  



## <a name="hardware---network-adapter"></a>Donanım-ağ bağdaştırıcısı  

Aşağıdaki üç rapor, **donanım ağ bağdaştırıcısı** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir ağ bağdaştırıcısına sahip bilgisayarlar**|Belirtilen ağ bağdaştırıcısına sahip bilgisayarların listesini görüntüler.|  
|**Türe göre ağ bağdaştırıcısı sayısı**|Her tür için envantere kaydedilen ağ bağdaştırıcısı kartlarının sayısını görüntüler.|  
|**Belirli bir bilgisayar için ağ bağdaştırıcısı bilgileri**|Belirtilen bilgisayarda yüklü olan ağ bağdaştırıcısı bilgilerini görüntüler.|  



## <a name="hardware---processor"></a>Donanım-Işlemci  

Aşağıdaki beş rapor, **donanım işlemci** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir işlemci hızına göre bilgisayarlar**|Belirtilen hızda bir işlemciye sahip bilgisayarların listesini görüntüler.|  
|**Hızlı işlemcilere sahip bilgisayarlar (belirtilen saat hızından daha hızlı veya buna eşit)**|Belirtilenden hızdan daha hızlı işlemcilere sahip bilgisayarların listesini görüntüler.|  
|**Yavaş işlemcilere sahip bilgisayarlar (belirtilen saat hızından daha yavaş veya buna eşit)**|Belirtilenden hızda veya bu hızdan daha yavaş çalışan işlemcilere sahip bilgisayarların listesini görüntüler.|  
|**İşlemci hızları**|İşlemci hızına göre envantere kaydedilmiş bilgisayar sayısını görüntüler.|  
|**Belirli bir bilgisayar için işlemci bilgileri**|Belirtilen bilgisayarda yüklü olan işlemci bilgilerini görüntüler.|  



## <a name="hardware---scsi"></a>Donanım-SCSI  

Aşağıdaki beş rapor, **donanım-SCSI** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir SCSI kartı türüne sahip bilgisayarlar**|Belirtilen SCSI kartının yüklü olduğu bilgisayarların listesini görüntüler.|  
|**SCSI kart türü sayısı**|Kart türüne göre envantere kaydedilen SCSI kartlarının sayısı.|  
|**Belirli bir bilgisayar için SCSI kartı bilgileri**|Belirtilen bilgisayarda yüklü olan SCSI kartı bilgilerini görüntüler.|  



## <a name="hardware---security"></a>Donanım-güvenlik

Aşağıdaki tek rapor, **donanım güvenlik** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Cihazlarda bellenim durumlarının ayrıntıları**|UEFı, SecureBoot ve TPM durumlarının ayrıntılarını görüntüler. **Note**: Bu rapor sürüm 1810 ' de değildir.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Donanım-ses kartı  

Aşağıdaki üç rapor, **donanım-SCSI** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir ses kartına sahip bilgisayarlar**|Belirtilen ses kartına sahip bilgisayarların listesini görüntüler.|  
|**Ses kartı sayısı**|Her ses kartı türüne göre envantere kaydedilmiş bilgisayar sayısını görüntüler.|  
|**Belirli bir bilgisayar için ses kartı bilgileri**|Belirtilen bir bilgisayarda bulunan ses kartı özet bilgilerini görüntüler.|  



## <a name="hardware---video-card"></a>Donanım-ekran kartı  

Aşağıdaki üç rapor, **donanım-video kartı** kategorisinin altında listelenmiştir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir ekran kartına sahip bilgisayarlar**|Belirtilen ekran kartına sahip bilgisayarların listesini görüntüler.|  
|**Türe göre ekran kartı sayısı**|Bilgisayarlarda yüklü olan tüm ekran kartlarının listesini görüntüler. Ayrıca, her bir ekran kartı türünün sayısını gösterir.|  
|**Belirli bir bilgisayar için ekran kartı bilgileri**|Belirtilen bilgisayarda yüklü olan ekran kartının özet bilgilerini görüntüler.|  



## <a name="migration"></a>Geçiş  

Aşağıdaki beş rapor, **geçiş** kategorisinin altında listelenmiştir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Dışlama listesindeki istemciler**|Geçiş işleminde dışlanan istemcileri görüntüler.|  
|**Configuration Manager koleksiyonuna bağımlılık**|Kaynak hiyerarşisi koleksiyonuna bağlı olan nesneleri görüntüler.|  
|**Geçiş işi özellikleri**|Bu raporda belirtilen geçiş işinin içeriği görüntülenir.|  
|**Geçiş işleri**|Bu raporda geçiş işlerinin listesi görüntülenir.|  
|**Geçirilemeyen nesneler**|Son deneme sırasında geçirilemeyen nesnelerin listesini görüntüler.|  



## <a name="network"></a>Ağ  

Aşağıdaki altı rapor, **ağ** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Alt ağa göre IP adresi sayısı**|Her IP alt ağı için envantere kaydedilen IP adresi sayısını görüntüler.|  
|**IP-alt ağ maskesine göre tüm alt ağlar**|IP alt ağlarının ve alt ağ maskelerinin sayısını görüntüler.|  
|**IP-belirli bir alt ağdaki bilgisayarlar**|Belirtilen bir IP alt ağı için bilgisayarların listesini ve IP bilgilerini görüntüler.|  
|**IP-belirli bir bilgisayar için bilgiler**|Belirtilen bir bilgisayardaki IP özet bilgilerini görüntüler.|  
|**IP-belirli bir IP adresi için bilgiler**|Belirtilen IP adresi özet bilgilerini görüntüler.|  
|**MAC-belirli bir MAC adresi için bilgisayarlar**|Belirtilen Mac adresine sahip bilgisayarların adlarını ve IP adreslerini görüntüler.|  



## <a name="operating-system"></a>İşletim sistemi  

Aşağıdaki 10 rapor, **Işletim sistemi** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Bilgisayar işletim sistemi sürümü geçmişi**|Belirtilen bir bilgisayardaki işletim sisteminin envanter geçmişini görüntüler.|  
|**Belirli bir işletim sistemine sahip bilgisayarlar**|Belirli bir işletim sistemine sahip bilgisayarları görüntüler.|  
|**Belirli bir işletim sistemine ve hizmet paketine sahip bilgisayarlar**|Belirli bir işletim sistemine ve hizmet paketine sahip bilgisayarları görüntüler.|  
|**İşletim sistemi sürümü sayısı**|İşletim sistemine göre envantere kaydedilmiş bilgisayar sayısını görüntüler.|  
|**İşletim sistemi ve hizmet paketlerinin sayısı**|İşletim sistemine ve hizmet paketi birleşimlerine göre envantere kaydedilmiş bilgisayarların sayısını görüntüler.|  
|**Hizmetler - Belirli bir hizmeti çalıştıran bilgisayarlar**|Belirtilen bir hizmeti çalıştıran bilgisayarların listesini görüntüler.|  
|**Hizmetler - Uzaktan Erişim Sunucusu çalıştıran bilgisayarlar**|Uzaktan Erişim Sunucusu çalıştıran bilgisayarların listesini görüntüler.|  
|**Hizmetler - Belirli bir bilgisayar için hizmet bilgileri**|Belirtilen bir bilgisayarda hizmetlerle ilgili özet bilgileri görüntüler.|  
|**Belirli bir koleksiyon için Windows 10 Bakımı ayrıntıları**|Belirli bir koleksiyon için Windows 10 bakımı hakkında genel bilgileri görüntüler.|
|**Windows Server bilgisayarları**|Windows Server işletim sistemlerini çalıştıran bilgisayarların listesini görüntüler.|  


## <a name="power-management"></a>Güç yönetimi  

Aşağıdaki 18 rapor, **güç yönetimi** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Güç yönetimi-bilgisayar etkinliği**|Belirli bir süre içinde belirtilen bir koleksiyon için monitör, bilgisayar ve Kullanıcı etkinliğini gösteren bir grafiği görüntüler.|  
|**Güç yönetimi-bilgisayara göre bilgisayar etkinliği**|Belirtilen tarihte belirtilen bir bilgisayar için monitör, bilgisayar ve Kullanıcı etkinliğini gösteren bir grafiği görüntüler.|  
|**Güç yönetimi-bilgisayar etkinliği ayrıntıları**|Belirtilen bir tarih ve saat için belirtilen koleksiyondaki bilgisayarların uyuma ve uyanma özelliklerinin listesini görüntüler.|  
|**Güç yönetimi-bilgisayar ayrıntıları**|Belirli bir bilgisayara uygulanan güç özellikleri, güç ayarları ve güç planlarıyla ilgili ayrıntılı bilgileri görüntüler.|  
|**Güç Yönetimi-Ayrıntıları bildirmeyen bilgisayar**|Belirtilen tarih ve saat için hiçbir güç etkinliği bildirmeyen bilgisayarların listesini görüntüler.|  
|**Güç yönetimi-dışlanan bilgisayarlar**|Güç planında dışlanan bilgisayarların listesini görüntüler.|  
|**Güç yönetimi-birden çok güç planına sahip bilgisayarlar**|Birden çok ve çakışan güç ayarları uygulanmış bilgisayarların listesini görüntüler.|  
|**Güç yönetimi-enerji tüketimi**|Belirtilen süre boyunca belirtilen bir koleksiyon için aylık toplam enerji tüketimini (kWh olarak) görüntüler.|  
|**Güç yönetimi-güne göre enerji tüketimi**|Son 31 gün içinde belirtilen koleksiyon için toplam enerji tüketimini (kWh olarak) görüntüler.|  
|**Güç yönetimi-enerji maliyeti**|Belirtilen süre boyunca belirtilen bir koleksiyon için aylık toplam enerji tüketim maliyetini görüntüler.|  
|**Güç yönetimi-günlük enerji maliyeti**|Son 31 gün içinde belirtilen koleksiyon için toplam enerji tüketimi maliyetini görüntüler.|  
|**Güç yönetimi-çevre etkisi**|Belirtilen süre boyunca belirtilen bir koleksiyon tarafından üretilen karbondioksit (CO2) emisyonunu gösteren grafiği görüntüler.|  
|**Güç yönetimi-güne göre çevresel etki**|Son 31 gün boyunca belirtilen bir koleksiyon tarafından üretilen CO2 emisyonlarını gösteren grafiği görüntüler.|  
|**Güç yönetimi-bilgisayar ayrıntıları**|Belirli bir süre içinde uyku veya bekleme süresi olmayan bilgisayarlarla ilgili ayrıntılı bilgileri görüntüler.|  
|**Güç yönetimi-Insomnia raporu**|Bilgisayarların uyumasını veya hazırda bekletmeye geçmesini önleyen genel nedenlerin listesini görüntüler. Ayrıca, belirli bir süre içinde her bir nedenle etkilenen bilgisayarların sayısını gösterir.|  
|**Güç yönetimi-güç özellikleri**|Belirtilen koleksiyondaki bilgisayarların güç yönetimi özelliklerini görüntüler.|  
|**Güç yönetimi-güç ayarları**|Belirtilen koleksiyondaki bilgisayarlar tarafından kullanılan güç ayarlarının toplu listesini görüntüler.|  
|**Güç yönetimi-güç ayarları ayrıntıları**|**Güç Yönetimi-güç ayarları** raporunda belirtilen bilgisayarlar hakkında daha fazla bilgi göstermek için kullanılır.|  



## <a name="replication-traffic"></a>Çoğaltma trafiği  

Aşağıdaki 10 rapor, **çoğaltma trafiği** kategorisinin altında listelenmiştir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Bağlantı Başına Genel Veri Çoğaltma Grafiği (çizgi grafik)**|Belirtilen gün sayısı için belirtilen bağlantının toplam genel veri çoğaltma trafiğini görüntüler.|  
|**Bağlantı Başına Genel Veri Çoğaltma Grafiği (pasta grafik)**|Belirtilen gün sayısı için belirtilen bağlantının toplam genel veri çoğaltma trafiğini görüntüler.|  
|**Bağlantıya göre Hiyerarşi Çoğaltma Trafiği**|Belirtilen gün sayısı için hiyerarşideki her bağlantının toplam çoğaltma trafiğini görüntüler.|  
|**Bağlantı Başına İlk On Hiyerarşi Çoğaltma Grubu Trafiği (pasta grafik)**|Bağlantı tarafından tanımlanan hiyerarşinin tamamında ilk 10 çoğaltma grubu için çoğaltma trafiğini görüntüler.|  
|**Bağlantı Çoğaltma Trafiği**|Belirtilen gün sayısı için tüm verilerin toplam çoğaltma trafiğini görüntüler.|  
|**Bağlantı başına çoğaltma grubu trafiği**|Belirtilen gün sayısı için belirtilen bir veritabanı çoğaltma bağlantısı üzerindeki çoğaltma grubu ağ trafiğini görüntüler.|  
|**Bağlantı Başına Site Verileri Çoğaltma Grafiği (çizgi grafik)**|Belirtilen gün sayısı için belirtilen bağlantının toplam site verileri çoğaltma trafiğini görüntüler.|  
|**Bağlantı Başına Site Verileri Çoğaltma Grafiği (pasta grafik)**|Belirtilen gün sayısı için belirtilen bağlantının toplam site verileri çoğaltma trafiğini görüntüler.|  
|**Toplam Hiyerarşi Çoğaltma Trafiği (çizgi grafik)**|Belirtilen gün sayısı için her bağlantının tüm yönlerine ait genel ve site verileri çoğaltma hiyerarşi toplamını görüntüler.|  
|**Toplam Hiyerarşi Çoğaltma Trafiği (pasta grafik)**|Belirtilen gün sayısı için her bağlantının tüm yönlerine ait genel ve site verileri çoğaltma hiyerarşi toplamını görüntüler.|  



## <a name="site---client-information"></a>Site-Istemci bilgileri  

Aşağıdaki 19 rapor, **site-Istemci bilgileri** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**İstemci atama ayrıntılı durum raporu**|İstemci atama durumuyla ilgili ayrıntılı bilgileri görüntüler.|  
|**İstemci atama hatası ayrıntıları**|İstemci atama hatasıyla ilgili ayrıntılı bilgileri görüntüler.|  
|**İstemci atama durumu ayrıntıları**|İstemci atama durumuyla ilgili genel bakış bilgilerini görüntüler.|  
|**İstemci atama başarı ayrıntıları**|Başarıyla atanan istemcilerle ilgili ayrıntılı bilgileri görüntüler.|  
|**İstemci dağıtım hatası raporu**|Dağıtılamayan istemcilerle ilgili ayrıntılı bilgileri görüntüler.|  
|**İstemci dağıtım durumu ayrıntıları**|İstemci yüklemelerinin durumuyla ilgili özet bilgileri görüntüler.|  
|**İstemci dağıtım başarı raporu**|Başarıyla dağıtılan istemciler için ayrıntılı bilgileri görüntüler.|  
|**HTTPS iletişimi kuramayan istemciler**|HTTPS Iletişim hazırlık durumu aracı 'nı çalıştıran her istemciyle ilgili ayrıntılı bilgileri ve HTTPS üzerinden iletişim kuramadığı raporları görüntüler.|  
|**Belirli bir site için atanan ancak yüklenmeyen bilgisayarlar**|Belirtilen siteye atanan ancak bu siteye bildirilmeyen bilgisayarların listesini görüntüler.|  
|**Configuration Manager istemci sürümüne sahip bilgisayarlar**|Configuration Manager istemci yazılımının belirtilen sürümünü çalıştıran bilgisayarların listesini görüntüler.|  
|**İletişim için kullanılan istemci ve protokol sayısı**|İstemciler tarafından kullanılan iletişim yöntemlerinin özetini görüntüler (HTTP veya HTTPS).|  
|**Her site için atanan ve yüklenen istemci sayısı**|Her site için atanan ve yüklenen bilgisayarların sayısını görüntüler. Birden çok siteyle ilişkilendirilmiş ağ konumuna sahip istemciler yalnızca bu siteye raporlama yapıyorsanız yüklü olarak sayılır.|  
|**HTTPS iletişimi kurabilen istemci sayısı**|HTTPS Iletişim hazırlık durumu aracı 'nı çalıştıran her istemciyle ilgili ayrıntılı bilgileri ve HTTPS üzerinden iletişim kurabildiği ya da mümkün olmayan raporları görüntüler.|  
|**Her site için istemci sayısı**|Site kodu tarafından yüklenen Configuration Manager istemcilerinin sayısını görüntüler.|  
|**İstemci sürümlerine göre Configuration Manager istemcilerinin sayısı**|Configuration Manager istemci sürümü tarafından bulunan bilgisayarların sayısını görüntüler.|  
|**Belirtilen koleksiyon için geri dönüş durum noktasına bildirilen sorunların ayrıntıları**|Belirtilen koleksiyondaki istemciler tarafından bildirilen sorunlarla ilgili ayrıntılı bilgileri görüntüler. Bu istemciler, atanmış bir geri dönüş durum noktasına sahip olmalıdır.|  
|**Belirtilen site için geri dönüş durum noktasına bildirilen sorunların ayrıntıları**|Belirtilen bir sitede istemciler tarafından bildirilen sorunlarla ilgili ayrıntılı bilgileri görüntüler. Bu istemciler, atanmış bir geri dönüş durum noktasına sahip olmalıdır.|  
|**Geri dönüş durum noktasına bildirilen sorunların özeti**|İstemciler tarafından bildirilen tüm sorunlarla ilgili bilgileri görüntüler. Bu istemciler, atanmış bir geri dönüş durum noktasına sahip olmalıdır.|  
|**Belirli bir koleksiyon için geri dönüş durum noktasına bildirilen sorunların özeti**|Belirtilen koleksiyondaki istemciler tarafından bildirilen sorunlar için Özet bilgiler görüntüler. Bu istemciler, atanmış bir geri dönüş durum noktasına sahip olmalıdır.|  



## <a name="site---discovery-and-inventory-information"></a>Site-bulma ve envanter bilgileri  

Aşağıdaki 10 rapor, **Site-bulma ve envanter bilgileri** kategorisinin altında listelenmiştir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Kısa süre önce (belirtilen gün sayısı içinde) bildirim göndermeyen istemciler**|Belirtilen gün sayısı içinde bulma verilerini, donanım envanterini veya yazılım envanterini bildirmeyen istemcilerin listesini görüntüler.|  
|**Belirli bir site tarafından bulunan bilgisayarlar**|Belirtilen sitenin bulduğu tüm bilgisayarların listesini görüntüler. Ayrıca, en son bulmanın tarihini gösterir.|  
|**Keşif yöntemiyle en son bulunan bilgisayarlar**|Sitenin belirtilen gün sayısı içinde bulduğu bilgisayarların listesini görüntüler. Ayrıca, bunları bulan aracıları listeler. Birden çok aracı bir bilgisayar tespit ederseniz, listede birden çok kez görünebilir.|  
|**Kısa süre önce (belirtilen gün sayısı içinde) bulunmayan bilgisayarlar**|Sitenin yakın zamanda bulduğu bilgisayarların listesini görüntüler. Ayrıca, sitenin bilgisayar bulmasından bu yana geçen gün sayısını gösterir.|  
|**Kısa süre önce (belirtilen gün sayısı içinde) bulunmayan bilgisayarlar**|Sitenin son envantere alınmayan bilgisayarların listesini görüntüler. Ayrıca, istemcinin bilgisayar tarafından envantere alındığı son zamanları gösterir.|  
|**Aynı Configuration Manager benzersiz tanımlayıcısını paylaşan bilgisayarlar**|Adları değiştirilen bilgisayarların listesini görüntüler. Adda bir değişiklik, bir bilgisayarın başka bir bilgisayarla Configuration Manager benzersiz tanımlayıcıyı paylaştığı bir belirtidir.|  
|**Yinelenen MAC adreslerine sahip bilgisayarlar**|MAC adresini paylaşan bilgisayarları görüntüler.|  
|**Kaynak etki alanlarındaki veya çalışma grubundaki bilgisayarların sayısı**|Her kaynak etki alanındaki veya çalışma grubundaki bilgisayarların sayısını görüntüler.|  
|**Belirli bir bilgisayar için bulma bilgileri**|Belirtilen bilgisayarı bulan aracıların ve sitelerin listesini görüntüler.|  
|**Belirli bir bilgisayar için envanter tarihleri**|Belirtilen bilgisayarda en son envanter çalıştırma tarihini ve saatini görüntüler.|  



## <a name="site---general"></a>Site - Genel  

Aşağıdaki üç rapor, **site-genel** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir sitedeki bilgisayarlar**|Belirtilen sitedeki tüm istemci bilgisayarları listeler.|  
|**Hiyerarşi için site durumu**|Hiyerarşideki sitelerin listesini ve site sürümünü ve site durum bilgilerini görüntüler.|  
|**Hiyerarşideki Configuration Manager güncelleştirmesinin durumu**|Hiyerarşi için Configuration Manager site güncelleştirmeleriyle ilgili bilgileri görüntüler.|  



## <a name="site---server-information"></a>Site-sunucu bilgileri  

Aşağıdaki tek rapor, **site-sunucu bilgileri** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir site için site sistemi rolleri ve site sistemi sunucuları**|Belirtilen site için site sistemi sunucusunun ve site sistemi rollerinin listesini görüntüler.|  



## <a name="software---companies-and-products"></a>Yazılım-şirketler ve ürünler  

Aşağıdaki 15 rapor, **Yazılım-şirketler ve ürünler** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir yazılım şirketi için envantere kaydedilmiş tüm ürünler**|Belirtilen bir yazılım şirketine ait envantere kaydedilmiş yazılım ürünlerinin ve sürümlerinin tümünün listesini görüntüler.|  
|**Tüm yazılım şirketleri**|Envantere kaydedilmiş yazılımları üreten tüm şirketlerin listesini görüntüler.|  
|**Tüm Windows uygulamaları**|Yüklü Windows uygulamalarının özetini görüntüler. Şu ölçütleri kullanarak arar: uygulama adı, mimari veya Yayımcı.|  
|**Belirli bir ürünü içeren bilgisayarlar**|Belirtilen ürünün envantere alındığı bilgisayarların listesini ve bu ürünün sürümlerini görüntüler.|  
|**Belirli bir ürüne adını ve sürümünü içeren bilgisayarlar**|Ürünün belirtilen sürümünün envantere kaydedildiği bilgisayarların listesini görüntüler.|  
|**Program Ekle/Kaldır bölümünde kayıtlı belirli yazılımlara sahip bilgisayarlar**|Program Ekle/Kaldır veya Programlar ve Özellikler bölümünde kayıtlı belirtilen yazılımı içeren tüm bilgisayarların özetini görüntüler.|  
|**Envantere kaydedilmiş tüm ürünlerin ve bunların sürümlerinin sayısı**|Envantere kaydedilmiş yazılım ürünleri ve sürümlerinin listesini ve her birinin yüklü olduğu bilgisayarların sayısını görüntüler.|  
|**Belirli bir ürün için envantere kaydedilmiş ürünlerin ve sürümlerinin sayısı**|Belirtilen ürünün envantere kaydedilmiş sürümlerinin listesini ve her birinin yüklü olduğu bilgisayarların sayısını görüntüler.|  
|**Program Ekle/Kaldır bölümünde kayıtlı olan yazılımların tüm örneklerinin sayısı**|Belirtilen koleksiyonda yer alan bilgisayarlarda yüklü ve Program Ekle/Kaldır veya Programlar ve Özellikler bölümünde kayıtlı olan yazılımların tüm örneklerinin özetini görüntüler.|  
|**Program Ekle/Kaldır bölümünde kayıtlı olan belirli bir yazılımın örneklerinin sayısı**|Bilgisayarda yüklü ve Program Ekle/Kaldır veya Programlar ve Özellikler bölümünde kayıtlı olan belirtilen yazılım paketi örneklerinin sayısını görüntüler.|  
|**Varsayılan tarayıcı sayıları**|Windows varsayılan olarak belirli bir Web tarayıcısına sahip istemcilerin sayısını gösterir. <br>Ortak Browserprogıds için aşağıdaki başvuruyu kullanın:<br> -AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge<br> Lerim. HTTP: Microsoft Internet Explorer<br> -Bermehtml: Google Chrome<br> -Me astable: Opera yazılımı<br> -FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> -Bilinmiyor: istemci işletim sistemi sorguyu desteklemez, sorgu çalıştırılmadı veya oturum açmamış bir Kullanıcı|
|**Belirli Windows uygulamalarının yüklemeleri**|Bu raporda, belirtilen bir Windows uygulamasını içeren tüm bilgisayarlar listelenir|  
|**Belirli bir bilgisayardaki ürünler**|Belirtilen bilgisayardaki envantere kaydedilmiş yazılım ürünlerinin ve bunların üreticilerinin özetini görüntüler.|  
|**Belirli bir bilgisayardaki Program Ekle/Kaldır bölümünde kayıtlı yazılımlar**|Belirtilen bilgisayarda yüklü ve Program Ekle/Kaldır veya Programlar ve Özellikler bölümünde kayıtlı olan yazılımların özetini görüntüler.|  
|**Belirtilen kullanıcı için yüklenen Windows uygulamaları**|Belirtilen kullanıcı için yüklenen tüm Windows uygulamalarını gösterir|  



## <a name="software---files"></a>Yazılım - Dosyalar  

Aşağıdaki beş rapor, **yazılım dosyaları** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir ürün için envantere kaydedilmiş tüm dosyalar**|Belirtilen yazılım ürünüyle ilişkili envantere kaydedilmiş dosyaların özetini görüntüler.|  
|**Belirli bir bilgisayardaki envantere kaydedilmiş tüm dosyalar**|Belirtilen bilgisayarda envantere kaydedilmiş tüm dosyaların özetini görüntüler.|  
|**İki bilgisayardaki yazılım envanterinin karşılaştırması**|Belirtilen iki bilgisayar için bildirilen yazılım envanteri arasındaki farkı görüntüler.|  
|**Belirli bir dosyayı içeren bilgisayarlar**|Belirtilen dosya adı için yazılım envanteri toplayan bilgisayarların listesini görüntüler. Bir bilgisayar, dosyanın birden çok kopyasını içeriyorsa listede birden çok kez görünebilir.|  
|**Belirli bir dosya adını içeren bilgisayar adı**|Belirtilen dosya için yazılım envanteri toplayan bilgisayarların sayısını görüntüler.|  



## <a name="software-distribution---application-monitoring"></a>Yazılım dağıtımı-uygulama izleme  

Aşağıdaki 10 rapor, **yazılım dağıtımı-uygulama izleme** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Tüm uygulama dağıtımları (gelişmiş)**|Tüm uygulama dağıtımları için ayrıntılı özet bilgilerini görüntüler.|  
|**Tüm uygulama dağıtımları (temel)**|Tüm uygulama dağıtımları için özet bilgilerini görüntüler.|  
|**Uygulama uyumluluğu**|Belirtilen koleksiyon içindeki belirtilen uygulama için uyumluluk bilgilerini görüntüler.|  
|**Varlık başına uygulama dağıtımları**|Belirtilen cihaza veya kullanıcıya dağıtılan uygulamaları görüntüler.|  
|**Uygulama altyapısı hataları**|Uygulama altyapısı hatalarını görüntüler. Bu hatalar iç altyapı sorunları veya geçersiz gereksinim kurallarından kaynaklanan hatalar içerir.|  
|**Ayrıntılı Uygulama Kullanım Durumu**|Yüklü uygulamalar için kullanım ayrıntılarını görüntüler.|  
|**Uygulama Kullanımı Durumu Özeti**|Yüklü uygulamalar için kullanım özetini görüntüler.|  
|**Uygulamayı içeren görev dizisi dağıtımları**|Belirtilen bir uygulamanın yüklendiği görev dizisi dağıtımlarını görüntüler.|  


## <a name="software-distribution---collections"></a>Yazılım dağıtımı-Koleksiyonlar  

Aşağıdaki üç rapor, **yazılım dağıtımı-koleksiyonlar** kategorisinin altında listelenmiştir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Tüm koleksiyonlar**|Hiyerarşideki tüm koleksiyonları görüntüler.|  
|**Belirli bir koleksiyondaki tüm kaynaklar**|Belirtilen koleksiyondaki tüm kaynakları görüntüler.|  
|**Belirtilen istemci için kullanılabilen bakım pencereleri**|Belirtilen istemci için geçerli olan tüm bakım pencerelerini görüntüler.|  



## <a name="software-distribution---content"></a>Yazılım dağıtımı-Içerik  

Aşağıdaki 16 rapor, **yazılım dağıtımı-içerik** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Tüm etkin içerik dağıtımları**|İçeriğin yüklenmekte olduğu veya kaldırıldığı tüm dağıtım noktalarını görüntüler.|  
|**Tüm içerik**|Bir sitedeki tüm uygulamaları ve paketleri görüntüler.|  
|**Belirli bir dağıtım noktasındaki tüm içerik**|Belirtilen dağıtım listesinde yüklü olan tüm içeriği görüntüler.|  
|**Tüm dağıtım noktaları**|Her site için dağıtım noktalarıyla ilgili bilgileri görüntüler.|  
|**Belirli bir dağıtım noktasındaki belirli bir paket için tüm durum iletileri**|Belirli bir dağıtım noktasındaki belirli bir paket için tüm durum iletilerini görüntüler.|  
|**Uygulama içerik dağıtımı durumu**|Uygulama içeriğinin dağıtım durumu bilgilerini görüntüler.|  
|**Dağıtım noktası grubunu hedefleyen uygulamalar**|Belirtilen dağıtım noktası grubuna dağıtılan uygulama içeriğiyle ilgili bilgileri görüntüler.|  
|**Belirtilen dağıtım noktası grubundaki eşitlenmemiş uygulamalar**|İlişkili içerik dosyalarının, belirtilen dağıtım noktası grubundaki en son sürümle güncelleştirilmediği uygulamaları görüntüler.|  
|**Dağıtım noktası grubu**|Belirtilen dağıtım noktası grubu bilgilerini görüntüler.|  
|**Dağıtım noktası kullanım özeti**|Her dağıtım noktası için dağıtım noktası kullanım özetini görüntüler.|  
|**Belirtilen paketin dağıtım durumu**|Her dağıtım noktasındaki belirtilen paket içeriği için dağıtım durumunu görüntüler.|  
|**Dağıtım noktası grubunu hedefleyen paketler**|Belirtilen dağıtım noktası grubuna hedeflenmiş paketlerle ilgili bilgileri görüntüler.|  
|**Belirtilen dağıtım noktası grubundaki eşitlenmemiş paketler**|İlişkili içerik dosyalarının, belirtilen dağıtım noktası grubundaki en son sürümle güncelleştirilmediği paketleri görüntüler.|  
|**Eş önbellek kaynağı içeriğini reddetme**|Sınır grubu başına eş önbellek kaynak reddi sayısını görüntüler.|
|**Koşula göre eş önbellek kaynak içeriğini reddetme**|Bir koşula bağlı olarak içeriğe hizmet vermek için reddedilen eş önbellek kaynaklarını görüntüler.|
|**Eş önbellek kaynağı içerik reddetme ayrıntıları**|Bir eş kaynak tarafından reddedilen içeriğin adını görüntüler.|



## <a name="software-distribution---package-and-program-deployment"></a>Yazılım dağıtma-paket ve program dağıtımı 

Aşağıdaki beş rapor **yazılım dağıtım paketi ve program dağıtımı** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirtilen paket ve program için tüm dağıtımlar**|Belirtilen paket ve programın tüm dağıtımlarıyla ilgili bilgileri görüntüler.|  
|**Tüm paket ve program dağıtımları**|Bu sitedeki bütün paket ve program dağıtımlarını görüntüler.|  
|**Belirtilen koleksiyon için tüm paket ve program dağıtımları**|Belirtilen koleksiyon için tüm paket ve program dağıtımlarını görüntüler.|  
|**Belirtilen bilgisayar için tüm paket ve program dağıtımları**|Belirtilen bilgisayara uygulanan tüm paket ve program dağıtımlarını görüntüler.|  
|**Belirtilen kullanıcı için tüm paket ve program dağıtımları**|Belirtilen kullanıcı için tüm paket ve program dağıtımlarını görüntüler.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Yazılım dağıtma-paket ve program dağıtım durumu  

Aşağıdaki beş rapor, **yazılım dağıtma-paket ve program dağıtım durumu** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Durumları ile tüm sistem kaynak paketi ve program dağıtımları**|Site için tüm paket ve program dağıtımlarını ve her dağıtımın durumunun özetini görüntüler.|  
|**Belirtilen durumda olan belirtilen paket ve program dağıtımı için tüm sistem kaynakları**|Belirtilen paket ve program dağıtımı için belirtilen durumda olan kaynakların listesini görüntüler.|  
|**Grafik-saatlik paket ve program dağıtımı tamamlanma durumu**|Paketi başarıyla yükleyen bilgisayarların yüzdesini görüntüler. Yönetici paketi ve program dağıtımını oluşturduğundan, liste her saat için düzenler. Paket ve program dağıtımı için ortalama süreyi izlemek amacıyla kullanılabilir.|  
|**Belirtilen bir istemci ve dağıtım için paket ve program dağıtım durumu**|Belirtilen bilgisayar ve paket ve program dağıtımı için bildirilen durum iletilerini görüntüler.|  
|**Belirtilen paket ve program dağıtımının durumu**|Belirtilen paket ve program dağıtımı için durum özetini görüntüler.|  



## <a name="software-metering"></a>Yazılım kullanım ölçümü  

Aşağıdaki 13 rapor, **yazılım kullanım ölçümü** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Bu siteye uygulanan tüm yazılım kullanım ölçümü kuralları**|Sitedeki tüm yazılım kullanım ölçümü kurallarının listesini görüntüler.|  
|**Ölçümlenen bir programın yüklendiği ancak belirtilen bir tarihten bu yana programı çalıştırmayan bilgisayarlar**|Belirtilen ölçülen uygulamanın bulunduğu tüm bilgisayarları görüntüler, ancak belirtilen tarihten bu yana hiçbir Kullanıcı programı çalıştırmıştır.|  
|**Belirli bir ölçülen yazılımı çalıştıran bilgisayarlar**|Belirtilen ay ve yıl içinde belirtilen yazılım kullanım ölçümü kuralıyla eşleşen programların çalıştırıldığı bilgisayarların listesini görüntüler.|  
|**Tüm ölçülen yazılım programları için eş zamanlı kullanım**|Belirtilen ay ve yıl içinde ölçülen yazılım programlarını eş zamanlı çalıştıran en yüksek kullanıcı sayısını görüntüler.|  
|**Belirli bir ölçülen yazılım programının eş zamanlı kullanım eğilim analizi**|Önceki yıl her ay belirtilen ölçülen yazılım programını eş zamanlı çalıştıran en yüksek kullanıcı sayısını görüntüler.|  
|**Tüm ölçülen yazılım programları için yüklü ürünler**|Yazılım envanterinde bildirilen ölçülen yazılım programlarının yüklü olduğu bilgisayarların sayısını görüntüler. Bu rapor, bilgisayarın yazılım envanterini toplayıp toplamayacağını gerektirir.|  
|**Yazılım kullanım ölçümü özet oluşturma işlemi**|Bu site sunucusunda en son özetlenen ölçüm verilerinin işlenme zamanını görüntüler. Yazılım kullanım ölçümü raporları yalnızca bu tarihlerden önce işlenen ölçüm verilerini yansıtır.|  
|**Belirli bir ölçülen yazılım programının gün içinde kullanım zamanı**|Belirli bir programın son 90 gün içindeki ortalama kullanım miktarını saatlik ve günlük ayrıntılarla görüntüler.|  
|**Tüm ölçülen yazılım programları için toplam kullanım**|Belirtilen ay ve yıl içinde programları çalıştıran ve her yazılım kullanım ölçümü kuralıyla eşleşen kullanıcı sayısını görüntüler. Bu kurallar yerel olarak yüklü yazılımlar veya Terminal Hizmetleri kullanımı içindir.|  
|**Windows Terminal Sunucularındaki ölçülen yazılım programlarının tümünün toplam kullanımı**|Belirtilen ay ve yıl içinde Terminal Hizmetlerini kullanarak her yazılım kullanım ölçümü kuralıyla eşleşen programları çalıştıran kullanıcıların sayısını görüntüler.|  
|**Belirli bir ölçülen yazılım programı için toplam kullanım eğilim analizi**|Geçen yılın her ayında programları çalıştıran ve belirtilen yazılım kullanım ölçümü kuralıyla eşleşen kullanıcı sayısını görüntüler. Bu kurallar yerel olarak yüklü yazılımlar veya Terminal Hizmetleri kullanımı içindir.|  
|**Windows Terminal Sunucularındaki belirli bir ölçülen yazılım programı için toplam kullanım eğilim analizi**|Geçen yılın her ayında programları çalıştıran ve belirtilen yazılım kullanım ölçümü kuralıyla eşleşen kullanıcı sayısını görüntüler. Bu kurallar, Terminal Hizmetleri 'ni kullanmak içindir.|  
|**Belirli bir ölçülen yazılım programını çalıştıran bilgisayarlar**|Belirtilen ay ve yıl içinde programları çalıştıran ve belirtilen yazılım kullanım ölçümü kuralıyla eşleşen kullanıcıların listesini görüntüler.|  



## <a name="software-updates---a-compliance"></a>Yazılım güncelleştirmeleri-uyumluluk  

Aşağıdaki sekiz rapor, **yazılım güncelleştirmeleri-bir uyumluluk** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Uyumluluk 1 - Genel uyumluluk**|Yazılım güncelleştirme grubu için genel uyumluluk durumunu görüntüler.|  
|**Uyumluluk 2 Belirli yazılım güncelleştirmesi**|Belirtilen yazılım güncelleştirmesi için uyumluluk verilerini görüntüler.|  
|**Uyumluluk 3 - Güncelleştirme grubu (güncelleştirme başına)**|Yazılım güncelleştirme grubunda tanımlanan yazılım güncelleştirmeleri için uyumluluk verilerini görüntüler.|  
|**Uyumluluk 4 - Satıcı ayı ve yılına göre güncelleştirmeler**|Belirtilen ay ve yıl boyunca bir satıcı tarafından yayımlanan yazılım güncelleştirmeleri için uyumluluk verilerini görüntüler.|  
|**Uyumluluk 5 - Belirli bir bilgisayar**|Bu rapor, belirtilen bilgisayar için yazılım güncelleştirmesi uyumluluk verilerini döndürür. Döndürülen bilgilerin miktarını sınırlamak için satıcı ve yazılım güncelleştirme sınıflandırmasını belirtebilirsiniz.|  
|**Uyumluluk 6 - Belirli yazılım güncelleştirme durumları (ikincil)**|Belirtilen yazılım güncelleştirmesi için her uyumluluk durumundaki bilgisayarların sayısını ve yüzdesini görüntüler.|  
|**Uyumluluk 7 - Bir güncelleştirme grubu için belirli bir uyumluluk durumunda olan bilgisayarlar (ikincil)**|Bir yazılım güncelleştirme grubuna göre belirtilen genel uyumluluk durumunda olan koleksiyondaki tüm bilgisayarları görüntüler.|  
|**Uyumluluk 8 - Bir güncelleştirme için belirli bir uyumluluk durumunda olan bilgisayarlar (ikincil)**|Bir yazılım güncelleştirme grubu için belirtilen genel uyumluluk durumunda olan koleksiyondaki tüm bilgisayarları görüntüler.|  
|**Uyumluluk 9-genel durum ve uyumluluk**|Yazılım güncelleştirme grubu için genel durum ve uyumluluk verilerini görüntüler. (sürüm 1806 ' den başlayarak)| 


## <a name="software-updates---b-deployment-management"></a>Yazılım güncelleştirmeleri-B dağıtım yönetimi  

Aşağıdaki sekiz rapor, **yazılım güncelleştirmeleri-B dağıtım yönetimi** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Yönetim 1 - Bir güncelleştirme grubu için dağıtımlar**|Belirtilen yazılım güncelleştirme grubunda tanımlanan tüm yazılım güncelleştirmelerini içeren tüm dağıtımları görüntüler.|  
|**Yönetim 2 - Güncelleştirme gerekiyor, ancak dağıtılmadı**|İstemcilerin gereken şekilde algılamadığı, ancak bir yöneticinin belirtilen koleksiyona dağıtmadığı satıcıya özgü tüm yazılım güncelleştirmelerini görüntüler.|  
|**Yönetim 3 - Bir dağıtımdaki güncelleştirmeler**|Belirtilen dağıtımda yer alan yazılım güncelleştirmelerini görüntüler.|  
|**Yönetim 4 - Bir koleksiyonu hedefleyen dağıtımlar**|Belirtilen koleksiyonu hedefleyen yazılım güncelleştirmesi dağıtımını görüntüler.|  
|**Yönetim 5 - Bir bilgisayarı hedefleyen dağıtımlar**|Belirtilen bilgisayara dağıtılan tüm yazılım güncelleştirmesi dağıtımlarını görüntüler.|  
|**Yönetim 6 - Belirli bir güncelleştirmeyi içeren dağıtımlar**|Belirtilen yazılım güncelleştirmesini ve dağıtım için ilişkilendirilen hedef koleksiyonu içeren tüm dağıtımları görüntüler.|  
|**Yönetim 7 - İçeriğe sahip olmayan dağıtımdaki güncelleştirmeler**|Belirtilen bir dağıtımda ilişkili içeriğe sahip olmayan yazılım güncelleştirmelerini görüntüler. Bu durum, istemcilerin güncelleştirmeyi yüklemesini engeller, bu da dağıtımın %100 uyumluluk sağlamasını önler.|  
|**Yönetim 8 - İçeriğe sahip olmayan bilgisayarlar (ikincil)**|Belirtilen yazılım güncelleştirmesini gerektiren tüm bilgisayarları görüntüler, ancak ilişkili içerik henüz bir dağıtım noktasına dağıtılmadı.|  



## <a name="software-updates---c-deployment-states"></a>Yazılım güncelleştirmeleri-C dağıtım durumları  

Aşağıdaki altı rapor, **yazılım güncelleştirmeleri-C dağıtım durumları** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Durumlar 1 - Bir dağıtım için zorlama durumları**|Belirtilen yazılım güncelleştirmesi dağıtımı için genellikle dağıtım değerlendirmesinin ikinci aşaması olan zorlama durumlarını görüntüler.|  
|**Durumlar 2 - Bir dağıtım için değerlendirme durumları**|Belirtilen yazılım güncelleştirmesi dağıtımı için genellikle dağıtım değerlendirmesinin birinci aşaması olan değerlendirme durumlarını görüntüler.|  
|**Durumlar 3 - Dağıtım ve bilgisayar durumları**|Belirtilen bilgisayar için belirtilen dağıtımdaki tüm yazılım güncelleştirmelerinin durumunu görüntüler.|  
|**Durumlar 4 - Computers in a specific state for a deployment (secondary)**|Bir yazılım güncelleştirme dağıtımı için belirtilen durumdaki tüm bilgisayarları görüntüler.|  
|**Durumlar 5 - Bir dağıtımdaki güncelleştirmelerin durumları (ikincil)**|Belirtilen dağıtım tarafından hedeflenen belirtilen yazılım güncelleştirmesi için durumların özetini görüntüler.|  
|**Durumlar 6 - Bir güncelleştirme için belirli bir zorlama durumundaki bilgisayarlar (ikincil)**|Belirtilen yazılım güncelleştirmesi için belirtilen zorlama durumundaki tüm bilgisayarları görüntüler.|  



## <a name="software-updates---d-scan"></a>Yazılım güncelleştirmeleri-D tarama  

Aşağıdaki dört rapor, **yazılım güncelleştirmeleri-D tarama** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Tarama 1 - Koleksiyona göre son tarama durumları**|Her uyumluluk taraması durumundaki bilgisayar sayısını göstermek için bir koleksiyon belirtin. İstemciler, son uyumluluk taraması sırasında durumu döndürür.|  
|**Tarama 2 - Siteye göre son tarama durumları**|Her uyumluluk taraması durumundaki bilgisayar sayısını görüntüleyecek bir site belirtin. İstemciler, son uyumluluk taraması sırasında durumu döndürür.|  
|**Tarama 3 - Belirli bir durumu bildiren koleksiyonun istemcileri (ikincil)**|Son uyumluluk taraması sırasında belirtilen bir koleksiyon ve belirtilen bir uyumluluk taraması durumu için tüm bilgisayarları görüntüler.|  
|**Tarama 4 - Belirli bir durumu bildiren sitenin istemcileri (ikincil)**|Belirtilen uyumluluk taraması durumuna sahip tüm bilgisayarları görüntüleyen bir site belirtin. İstemciler, son uyumluluk taramasında durumu döndürür.|  



## <a name="software-updates---e-troubleshooting"></a>Yazılım güncelleştirmeleri-E sorun giderme  

Aşağıdaki dört rapor, **yazılım güncelleştirmeleri-E sorun giderme** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Sorun giderme 1-Tarama hataları**|Sitedeki tarama hatalarını ve her hatayla karşılaşılan bilgisayar sayısını görüntüler.|  
|**Sorun giderme 2-dağıtım hataları**|Sitedeki dağıtım hatalarını ve her hatayla karşılaşılan bilgisayar sayısını görüntüler.|  
|**Sorun giderme 3-belirli bir tarama hatasıyla başarısız olan bilgisayarlar (ikincil)**|Belirtilen bir hata nedeniyle başarısız olan bilgisayarların listesini görüntüler.|  
|**Sorun giderme 4 – Belirli bir dağıtım hatasıyla başarısız olan bilgisayarlar (ikincil)**|Belirtilen hata nedeniyle dağıtım güncelleştirmesinin başarısız olduğu bilgisayarları görüntüler.|  



## <a name="state-migration"></a>Durum geçişi  

Aşağıdaki üç rapor **durum geçiş** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir kaynak bilgisayar için durum geçiş bilgileri**|Belirli bir bilgisayar için durum geçiş bilgilerini görüntüler.|  
|**Belirli bir durum geçiş noktası için durum geçiş bilgileri**|Belirtilen bir durum geçiş noktası için durum geçiş bilgilerini görüntüler.|  
|**Belirli bir site için durum geçiş noktaları**|Belirtilen bir site için durum geçiş noktalarını görüntüler.|  



## <a name="status-messages"></a>Durum iletileri  

Aşağıdaki 12 rapor **durum iletileri** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir ileti kimliği için tüm iletiler**|Belirtilen ileti kimliğine sahip durum iletilerinin listesini görüntüler.|  
|**Son 12 saat içinde belirli bir site için hata bildiren istemciler**|Son 12 saat içinde hata bildiren bilgisayarları ve bileşenleri ve bildirilen hata sayısını görüntüler.|  
|**Son 12 saat içindeki bileşen iletileri**|Belirtilen bir site kodu, bilgisayar ve bileşen için son 12 saat içindeki bileşen iletilerinin listesini görüntüler.|  
|**Son bir saat içindeki bileşen iletileri**|Belirtilen sitede belirtilen bilgisayarda belirtilen bir bileşen tarafından son saat içinde oluşturulan durum iletilerinin listesini görüntüler.|  
|**Belirli bir site için son bir saat içindeki bileşen iletilerinin sayısı**|Belirtilen sitede son bir saat içinde bildirilen durum iletilerinin bileşen ve önem derecesine göre sayısını görüntüler.|  
|**Son 12 saat içindeki hata sayısı**|Son 12 saat içinde sunucu bileşeni durum iletilerinin sayısını görüntüler.|  
|**Önemli hatalar (bileşene göre)**|Bileşene göre önemli hataları bildiren bilgisayarların listesini görüntüler.|  
|**Önemli hatalar (bilgisayar adına göre)**|Bilgisayar adına göre önemli hataları bildiren bilgisayarların listesini görüntüler.|  
|**Belirli bir bilgisayar için son 1000 ileti (Hatalar ve Uyarılar)**|Belirtilen bir bilgisayar için son 1000 hata ve uyarı bileşen durum iletilerinin özetini görüntüler.|  
|**Belirli bir bilgisayar için son 1000 ileti (Hatalar, Uyarılar ve Bilgiler)**|Belirtilen bir bilgisayar için son 1000 hata, uyarı ve bilgi amaçlı bileşen durum iletilerinin özetini görüntüler.|  
|**Belirli bir bilgisayar için son 1000 ileti (Hatalar)**|Belirtilen bir bilgisayar için son 1000 hata sunucu bileşen durum iletilerinin özetini görüntüler.|  
|**Belirli bir sunucu bileşeni için son 1000 ileti**|Belirtilen sunucu bileşeni için en son 1000 durum iletisinin özetini görüntüler.|  



## <a name="status-messages---audit"></a>Durum iletileri-denetim  

Aşağıdaki üç rapor **durum iletileri-denetim** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir kullanıcı için tüm denetim iletileri**|Belirtilen kullanıcı için tüm denetim durum iletilerinin özetini görüntüler. Denetim iletileri, Configuration Manager nesneleri ekleyen, değiştiren veya silen Configuration Manager konsolunda gerçekleştirilen eylemleri anlatır.|  
|**Uzaktan denetim-belirli bir kullanıcı tarafından uzaktan denetlenen tüm bilgisayarlar**|Belirtilen kullanıcıya göre istemci bilgisayarlarının uzaktan denetimini gösteren durum iletilerinin özetini görüntüler.|  
|**Uzaktan denetim-tüm uzaktan denetim bilgileri**|İstemci bilgisayarlarının uzaktan denetimiyle ilgili durum iletilerinin özetini görüntüler.|  



## <a name="task-sequence---deployment-status"></a>Görev sırası-dağıtım durumu  

Aşağıdaki 11 rapor, **görev sırası-dağıtım durumu** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli durumdaki bir görev dizisi dağıtımı için tüm sistem kaynakları**|Belirtilen dağıtım durumundaki belirtilen görev dizisi dağıtımı için hedef bilgisayarların listesini görüntüler.|  
|**Belirli bir durumda olan ve bilinmeyen bilgisayarlar için kullanılabilen görev dizisi dağıtımı için tüm sistem kaynakları**|Belirtilen dağıtım durumunda olan belirtilen görev dizisi dağıtımı için hedef bilgisayarların listesini görüntüler.|  
|**Görev dizisi dağıtımları atanan ancak henüz çalıştırılmayan sistem kaynaklarının sayısı**|Görev dizilerini kabul eden, ancak görev dizisini çalıştırmayan bilgisayar sayısını görüntüler.|  
|**Bir bilgisayardaki görev dizisi dağıtımının geçmişi**|Belirtilen hedef bilgisayardaki belirtilen görev dizisi dağıtımı adımlarının her birinin durumunu görüntüler. Hiçbir kayıt döndürülmezse, görev sırası bilgisayarda başlatılmamıştır.|  
|**Bir görev dizisi dağıtımını çalıştırmak için belirli bir çalıştırma süresini aşan bilgisayarların listesi**|Bir görev dizisini çalıştırmak için belirtilen çalıştırma süresini aşan hedef bilgisayarların listesini görüntüler.|  
|**Belirli bir hedef bilgisayardaki belirli bir görev dizisi dağıtımı için çalışma süresi**|Belirtilen bilgisayardaki belirtilen görev dizisini başarıyla tamamlamak için gereken toplam süreyi görüntüler.|  
|**Belirli bir hedef bilgisayardaki belirli bir görev dizisi dağıtım adımlarının her biri için çalışma süresi**|Belirtilen hedef bilgisayardaki belirtilen görev dizisi dağıtımı adımlarının her birinin tamamlanma süresini görüntüler.|  
|**Belirli bir bilgisayar için belirli bir görev dizisi dağılımının durumu**|Belirtilen bilgisayardaki belirtilen görev dizisi dağıtımının durum özetini görüntüler.|  
|**Bilinmeyen bir hedef bilgisayardaki görev dizisi dağıtımının durumu**|Belirtilen bilinmeyen hedef bilgisayardaki belirtilen görev dizisi dağıtımı durumunu görüntüler.|  
|**Belirli görev dizisi dağıtımının durum özeti**|Dağıtım tarafından hedeflenen tüm kaynakların durum özetini görüntüler.|  
|**Bilinmeyen bilgisayarlar için kullanılabilen belirli bir görev dizisi dağıtımının durum özeti**|Bilinmeyen bilgisayarlar içeren bir koleksiyon tarafından kullanılabilen, belirtilen dağıtım tarafından hedeflenen tüm kaynakların durum özetini görüntüler.|  



## <a name="task-sequence---deployments"></a>Görev sırası-dağıtımlar  

Aşağıdaki 11 rapor, **görev sırası dağıtımları** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir grupta veya belirli bir görev dizisi dağıtımı aşamasında bulunan tüm sistem kaynakları**|Belirtilen grupta veya belirtilen görev dizisi dağıtımı aşamasında çalışmakta olan bilgisayarların listesini görüntüler.|  
|**Bir görev dizisi dağıtımının başarısız olduğu belirli bir grup veya aşamadaki tüm sistem kaynakları**|Belirtilen görev dizisi dağıtımının belirtilen grubunda veya aşamasında başarısız olan bilgisayarların listesini görüntüler.|  
|**Tüm görev dizisi dağıtımları**|Geçerli siteden başlatılan tüm görev dizisi dağıtımlarının ayrıntılarını görüntüler.|  
|**Bilinmeyen bilgisayarlar için kullanılabilen tüm görev dizisi dağıtımları**|Siteden başlatılan tüm görev sırası dağıtımlarının ayrıntılarını görüntüler ve bilinmeyen bilgisayarlar içeren koleksiyonlara dağıtılır.|  
|**Belirli bir görev dizisinin her aşamasında ve grubundaki hata sayısı**|Belirtilen görev dizisinin her aşamasında veya grubundaki hata sayısını görüntüler.|  
|**Belirli bir görev dizisi dağıtımının her aşamasında ve grubundaki hata sayısı**|Belirtilen görev dizisi dağıtımının her aşamasında veya grubundaki hata sayısını görüntüler.|  
|**Tüm görev dizisi dağıtımlarının dağıtım durumu**|Tüm görev dizisi dağıtımlarının genel ilerleme durumunu görüntüler.|  
|**Çalışan bir görev dizisinin ilerleme durumu**|Belirtilen görev dizisinin ilerleme durumunu görüntüler.|  
|**Çalışan bir görev dizisi dağıtımının ilerleme durumu**|Belirtilen görev dizisi dağıtımıyla ilgili özet bilgileri görüntüler.|  
|**Belirli bir görev dizisi için tüm dağıtımların ilerleme durumu**|Belirtilen görev dizisi için tüm dağıtımların ilerleme durumunu görüntüler.|  
|**Görev dizisi dağıtımı için özet raporu**|Belirtilen görev dizisi dağıtımıyla ilgili özet bilgileri görüntüler.|  



## <a name="task-sequence---progress"></a>Görev dizisi-Ilerleme durumu  

Aşağıdaki beş rapor, **görev dizisi-Ilerleme durumu** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Grafik-bir görev sırasının haftalık ilerlemesi**|Dağıtım tarihinden başlamak üzere görev dizisinin haftalık ilerleme durumunu görüntüler.|  
|**Görev dizisinin ilerleme durumu**|Belirtilen görev dizisinin ilerleme durumunu görüntüler.|  
|**Tüm görev dizilerinin ilerleme durumu**|Tüm görev dizilerinin ilerleme durumu özetini görüntüler.|  
|**İşletim sistemi dağıtımları için görev dizilerinin ilerleme durumu**|İşletim sistemlerini dağıtan tüm görev dizilerinin ilerleme durumunu görüntüler.|  
|**Bilinmeyen tüm bilgisayarların durumu**|Bir görev sırası dağıtımını çalıştırdıkları sırada bilinmeyen bilgisayarların listesini ve şimdi bilinen bilgisayarlar olup olmadığını görüntüler.|  



## <a name="task-sequences---references"></a>Görev dizileri-başvurular  

Aşağıdaki tek rapor, **görev dizileri-başvurular** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir görev dizisi tarafından başvurulan içerik**|Belirtilen görev dizisi tarafından başvurulan içeriği görüntüler.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Kullanıcı-cihaz benzeşimi  

Aşağıdaki iki rapor, **Kullanıcı-cihaz benzeşimi** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Koleksiyona göre bekleyen kullanıcı aygıt benzeşimi ilişkilendirmeleri**|Bu raporda, bir koleksiyonun üyeleri için kullanım verilerine göre bekleyen tüm kullanıcı aygıt benzeşimi atamaları görüntülenir.|  
|**Koleksiyon başına kullanıcı aygıt benzeşimi ataması**|Belirtilen koleksiyon için tüm Kullanıcı cihaz ilişkilendirmelerini görüntüler ve sonuçları koleksiyon türüne (örneğin, Kullanıcı veya cihaz) göre gruplandırır.|  



## <a name="user-data-and-profiles-health"></a>Kullanıcı verileri ve profilleri sistem durumu  

Aşağıdaki dört rapor, **Kullanıcı verileri ve profilleri sistem durumu** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Klasör Yeniden Yönlendirme Durum Raporu - Ayrıntılar**|Belirli bir kullanıcının yeniden yönlendirilen klasörlerinin her biri için klasör yeniden yönlendirme 'nin sistem durumu ayrıntılarını görüntüler.|  
|**Gezici Kullanıcı Profilleri Durum Raporu - Ayrıntılar**|Belirtilen kullanıcı için gezici kullanıcı profilinin sistem durumu ayrıntılarını görüntüler.|  
|**Kullanıcı Verileri ve Profilleri Durum Raporu - Ayrıntılar**|Klasör yeniden yönlendirme veya gezici kullanıcı profillerinin hata veya uyarı ayrıntılarını görüntüler. Bu rapor, Özet raporundan alınan Ayrıntılar hedefidir.|  
|**Kullanıcı Verileri ve Profilleri Durum Raporu - Özet**|Klasör yeniden yönlendirme ve gezici kullanıcı profili durumunun özetini görüntüler.|  



## <a name="users"></a>Kullanıcılar  

Aşağıdaki üç rapor, **Kullanıcılar** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Belirli bir kullanıcı adı için bilgisayarlar**|Belirtilen kullanıcı tarafından kullanılan bilgisayarların listesini görüntüler.|  
|**Etki alanına göre kullanıcı sayısı**|Her etki alanındaki kullanıcı sayısını görüntüler.|  
|**Belirli bir etki alanındaki kullanıcılar**|Belirtilen etki alanındaki kullanıcıların ve bilgisayarlarının listesini görüntüler.|  



## <a name="virtual-applications"></a>Sanal uygulamalar  

Aşağıdaki yedi rapor, **sanal uygulamalar** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**App-V Sanal Ortam Sonuçları**|Belirtilen koleksiyon için belirli durumda bulunan belirtilen sanal ortamla ilgili bilgileri gösterir.|  
|**Varlık için App-V Sanal Ortam Sonuçları**|Belirtilen bir varlık için belirtilen sanal ortamla ilgili bilgileri görüntüler. Ayrıca, belirtilen sanal ortam için herhangi bir dağıtım türünü gösterir.|  
|**App-V Sanal Ortam Durumu**|Belirtilen bir koleksiyona ait belirtilen sanal ortam için uyumluluk bilgilerini görüntüler.|  
|**Belirli bir sanal uygulamaya sahip bilgisayarlar**|Uygulama Sanallaştırma Yönetimi Sıralayıcı kullanılarak oluşturulan belirli App-V uygulaması kısayoluna sahip olan bilgisayarların özetini görüntüler.|  
|**Belirli bir sanal uygulama paketine sahip bilgisayarlar**|Belirtilen App-V uygulama paketine sahip bilgisayarların özetini görüntüler.|  
|**Tüm sanal uygulama paket örneklerinin sayısı**|Algılanan App-V uygulama paketlerinin sayısını görüntüler.|  
|**Tüm sanal uygulama örneklerinin sayısı**|Algılanan App-V uygulamalarının sayısını görüntüler.|  



## <a name="vulnerability-assessment"></a>Güvenlik açığı değerlendirmesi

Aşağıdaki bir rapor, **güvenlik açığı değerlendirmesi** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**Güvenlik açığı değerlendirmesi genel raporu**|Belirli bir bilgisayar için güvenlik, yönetim ve uyumluluk güvenlik açıklarını belirler|  



## <a name="wake-on-lan"></a>LAN'da Uyandırma  

Aşağıdaki yedi rapor **LAN'da Uyandırma** kategorisi altında listelenir.

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|**LAN’da Uyandırma etkinliği için hedeflenen tüm bilgisayarlar**|LAN 'da Uyandırma etkinliği için hedeflenen bilgisayarların listesini göstermek için dağıtım türünü belirtin.|  
|**Uyandırma etkinliği bekleyen tüm nesneler**|Uyandırma için zamanlanmış nesneleri görüntüler.|  
|**LAN'da Uyandırma için etkinleştirilmiş tüm siteler**|LAN'da Uyandırma için etkinleştirilmiş hiyerarşideki tüm sitelerin listesini görüntüler.|  
|**Tanımlanan süre içinde uyandırma paketleri gönderilirken alınan hatalar**|Tanımlanan süre içinde bilgisayara uyandırma paketleri gönderilirken alınan hataları görüntüler.|  
|**LAN'da Uyandırma etkinliği geçmişi**|Belirli bir süre içinde oluşan uyandırma etkinliklerinin geçmişini görüntüler.|  
|**Uyandırma Proxy'si Dağıtım Durumu Ayrıntıları**|Belirtilen koleksiyondaki her cihaz için Uyandırma Proxy’sinin dağıtım durumuyla ilgili bilgileri görüntüler.|  
|**Uyandırma Proxy'si Dağıtım Durumu Özeti**|Belirtilen koleksiyon için uyandırma proxy’sinin dağıtım durumu özetini görüntüler.|  
