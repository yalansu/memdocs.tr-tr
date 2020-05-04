---
title: BitLocker raporlarını görüntüleme
titleSuffix: Configuration Manager
description: Configuration Manager 'de BitLocker yönetim raporları hakkında bilgi edinin
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d10717f980922e1f6d1fca9224e288b4df709da2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717359"
---
# <a name="view-bitlocker-reports"></a>BitLocker raporlarını görüntüleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

Raporları Raporlama Hizmetleri noktasına [yükledikten](setup-websites.md) sonra raporları görüntüleyebilirsiniz. Raporlar, kuruluşun ve bireysel cihazların BitLocker uyumluluğunu gösterir. Bunlar tablosal bilgi ve grafikler sağlar ve farklı açılardan verileri görüntülemenize izin veren filtrelere sahiptir.

Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin. Aşağıdaki raporlar **BitLocker yönetim** kategorisinde bulunur:

- [BitLocker bilgisayar uyumluluğu](#bkmk-compliancereport)

- [BitLocker kurumsal uyumluluk panosu](#bkmk-dashboard)

- [BitLocker kurumsal uyumluluk ayrıntıları](#bkmk-compliancedetails)

- [BitLocker kurumsal uyumluluk Özeti](#bkmk-compliancesummary)

- [Kurtarma denetim raporu](#bkmk-audit)

Bu raporların tümüne doğrudan raporlama hizmetleri noktası Web sitesinden erişebilirsiniz.

> [!NOTE]
> Bu raporların tüm verileri görüntülemesi için:
>
> - Bir cihaz koleksiyonuna bir BitLocker yönetim ilkesi oluşturma ve dağıtma
> - Hedef koleksiyondaki istemcilerin donanım envanterini gönderebilmesi gerekir

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a>BitLocker bilgisayar uyumluluğu

Bir bilgisayara özgü bilgileri toplamak için bu raporu kullanın. İşletim sistemi sürücüsü ve tüm sabit veri sürücüleri hakkında ayrıntılı şifreleme bilgileri sağlar. Her sürücünün ayrıntılarını görüntülemek için bilgisayar adı girişini genişletin. Ayrıca, bilgisayardaki her sürücü türüne uygulanan ilkeyi belirtir.

[![BitLocker bilgisayar uyumluluk raporunun örnek ekran görüntüsü](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

Bu raporu, kaybolan veya çalınan bilgisayarların bilinen son BitLocker şifreleme durumunu öğrenmek için de kullanabilirsiniz. Configuration Manager, dağıttığınız BitLocker ilkelerine bağlı olarak cihazın uyumluluğunu belirler. Bir cihazın BitLocker şifreleme durumunu belirlemeyi denemeden önce, kendisine dağıttığınız ilkeleri doğrulayın.

> [!NOTE]
> Bu rapor, çıkarılabilir veri birimi şifreleme durumunu göstermez.

### <a name="computer-details"></a>Bilgisayar Ayrıntıları

|Sütun&nbsp;adı|Açıklama|
|----------------|----|
|Bilgisayar adı|Kullanıcı tarafından belirtilen DNS bilgisayar adı.|
|Etki alanı adı|Bilgisayar için tam etki alanı adı.|
|Bilgisayar türü|Bilgisayar türü, geçerli türler **taşınabilir değil** ve **Taşınabilir**değildir.|
|İşletim sistemi|Bilgisayarın işletim sistemi türü.|
|Genel uyumluluk|Bilgisayarın genel BitLocker uyumluluk durumu. Geçerli durumlar **uyumlu** ve **uyumlu değil**. [Sürücü başına uyumluluk durumu](#bkmk_volume) , farklı uyumluluk durumlarını gösterebilir. Ancak, bu alan belirtilen ilkeden uyumluluk durumunu temsil eder.|
|İşletim sistemi uyumluluğu|Bilgisayardaki işletim sisteminin uyumluluk durumu. Geçerli durumlar **uyumlu** ve **uyumlu değil**.|
|Sabit veri sürücüsü uyumluluğu|Bilgisayardaki sabit bir veri sürücüsünün uyumluluk durumu. Geçerli durumlar **uyumlu** ve **uyumlu değil**.|
|Son güncelleştirme tarihi|Uyumluluk durumunu raporlamak için bilgisayarın sunucuyla son iletişim kurmadığı tarih ve saat.|
|Dışarıda|Kullanıcının BitLocker ilkesinden muaf mı yoksa muaf mı ayrılmadığını gösterir.|
|Muaf tutulan Kullanıcı|BitLocker ilkesinden muaf tutulan Kullanıcı.|
|Muafiyet tarihi|Muafiyet verildiği tarih.|
|Uyumluluk durumu ayrıntıları|Belirtilen ilkeden bilgisayarın uyumluluk durumu hakkında hata ve durum iletileri.|
|İlke şifreleme düzeyi|BitLocker yönetim ilkesinde seçtiğiniz şifre gücü.|
|İlke: Işletim sistemi sürücüsü|İşletim sistemi sürücüsü için şifreleme gerekip gerekmediğini ve uygun koruyucu türünü gösterir.|
|İlke: sabit veri sürücüsü|Sabit veri sürücüsü için şifrelemenin gerekip gerekmediğini gösterir.|
|Üretici|Bilgisayar BIOS 'unda göründüğü gibi bilgisayar üreticisi adı.|
|Model|Bilgisayar BIOS 'unda göründüğü şekliyle bilgisayar üreticisi model adı.|
|Cihaz kullanıcıları|Bilgisayardaki bilinen kullanıcılar.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a>Bilgisayar hacmi

|Sütun&nbsp;adı|Açıklama|
|----------------|----|
|Sürücü harfi|Bilgisayardaki sürücü harfi.|
|Sürücü türü|Sürücü türü. Geçerli değerler, **Işletim sistemi sürücüsü** ve **sabit veri sürücüsüdür**. Bu girişler mantıksal birimler yerine fiziksel sürücülerdir.|
|Şifreleme düzeyi|BitLocker yönetim ilkesinde sırasında seçtiğiniz şifre gücü.|
|Koruyucu türleri|Sürücüyü şifrelemek için ilkede seçtiğiniz koruyucunun türü. Bir işletim sistemi sürücüsü için geçerli koruyucu türleri **TPM** veya **TPM + PIN**' tür. Sabit veri sürücüsü için geçerli koruyucu türü **parola**.|
|Koruyucu durumu|Bilgisayarın ilkede belirtilen koruyucu türünü etkinleştirdiğini belirtir. Geçerli durumlar **Açık** veya **kapalı**.|
|Şifreleme durumu|Sürücünün şifreleme durumu. Geçerli durumlar **şifrelenir**, **şifrelenmez**veya **şifrelidir**.|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a>BitLocker kurumsal uyumluluk panosu

Bu rapor, kuruluşunuzda BitLocker uyumluluk durumunu gösteren aşağıdaki grafikleri sağlar:

- Uyumluluk durumu dağılımı

- Uyumlu olmayan hatalar dağıtım

- Sürücü türüne göre uyumluluk durumu dağılımı

[![BitLocker kurumsal uyumluluk panosunun örnek ekran görüntüsü](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>Uyumluluk durumu dağılımı

Bu pasta grafik, kuruluştaki bilgisayarlar için uyumluluk durumunu gösterir. Ayrıca, Seçili koleksiyondaki toplam bilgisayar sayısı ile karşılaştırıldığında, bu uyumluluk durumundaki bilgisayarların yüzdesini gösterir. Her durumu içeren gerçek bilgisayar sayısı da gösterilir.

Pasta grafiğinde aşağıdaki uyumluluk durumları gösterilmektedir:

- Uyumlu

- Uyumlu değil

- Kullanıcı muaf

- Geçici Kullanıcı muafiyeti

- İlke zorlanmaz

- Bilinmeyen. Bu bilgisayarlar bir durum hatası raporladı veya koleksiyonun bir parçasıdır ancak uyumluluk durumunu hiçbir şekilde bildirmemiştir. Bilgisayarın kuruluşa bağlantısı kesildiğinde uyumluluk durumunun olmaması meydana gelebilir.

### <a name="non-compliant---errors-distribution"></a>Uyumlu olmayan hatalar dağıtım

Bu pasta grafik, kuruluşunuzda BitLocker Sürücü Şifrelemesi ilkesiyle uyumlu olmayan bilgisayarların kategorilerini gösterir. Ayrıca, her bir kategorideki bilgisayarların sayısını gösterir. Rapor, koleksiyondaki uyumlu olmayan bilgisayarların toplam sayısından her yüzdeyi hesaplar.

- Kullanıcı şifrelemeyi ertelendi

- Uyumlu TPM bulunamıyor

- Sistem bölümü kullanılamıyor veya yeterince büyük

- TPM görünür ancak başlatılmamış

- İlke çakışması

- TPM otomatik sağlaması bekleniyor

- Bilinmeyen bir hata oluştu

- Bilgi yok. Bu bilgisayarlarda BitLocker yönetim aracısı yüklü değil veya yüklü ancak etkinleştirilmemiş. Örneğin, hizmet çalışmıyor.

### <a name="compliance-status-distribution-by-drive-type"></a>Sürücü türüne göre uyumluluk durumu dağılımı

Bu çubuk grafik, geçerli BitLocker uyumluluk durumunu sürücü türüne göre gösterir. Durumlar **uyumludur** ve **uyumlu**değildir. Çubuklar, sabit veri sürücüleri ve işletim sistemi sürücüleri için gösterilir. Rapor, sabit veri sürücüsü olmayan bilgisayarları içerir ve yalnızca **Işletim sistemi sürücü** çubuğunda bir değeri gösterir. Grafik, BitLocker Sürücü Şifrelemesi ilkesi veya Ilke yok kategorisinden bir istisna vermiş olan kullanıcıları içermez.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a>BitLocker kurumsal uyumluluk ayrıntıları

Bu rapor, BitLocker yönetim ilkesini dağıttığınız bilgisayarların toplanması için kuruluşunuzdaki genel BitLocker uyumluluğu hakkındaki bilgileri gösterir.

[![BitLocker kurumsal uyumluluk ayrıntılarının örnek ekran görüntüsü](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|Sütun adı|Açıklama|
|--- |--- |
|Yönetilen bilgisayarlar|BitLocker yönetim ilkesi dağıttığınız bilgisayar sayısı.|
|% Uyumlu|Kuruluştaki uyumlu bilgisayarların yüzdesi.|
|% Uyumlu değil|Kuruluştaki uyumlu olmayan bilgisayarların yüzdesi.|
|Bilinmeyen uyumluluk yüzdesi|Uyumluluk durumu bilinmeyen bilgisayarların yüzdesi.|
|Muaf tutulan yüzdesi|BitLocker şifreleme gereksiniminden muaf tutulan bilgisayarların yüzdesi.|
|Muaf olmayan%|BitLocker şifreleme gereksiniminden muaf tutulan bilgisayarların yüzdesi.|
|Uyumlu|Kuruluştaki uyumlu bilgisayar sayısı.|
|Uyumlu Değil|Kuruluştaki uyumlu olmayan bilgisayarların sayısı.|
|Bilinmeyen uyumluluk|Bilinen bir uyumluluk durumu olan bilgisayar sayısı.|
|AF|BitLocker şifreleme gereksiniminden muaf tutulan bilgisayarların sayısı.|
|Muaf olmayan|BitLocker şifreleme gereksiniminden muaf olmayan bilgisayar sayısı.|

### <a name="computer-details"></a>Bilgisayar Ayrıntıları

|Sütun adı|Açıklama|
|--- |--- |
|Bilgisayar adı|Yönetilen cihazın DNS bilgisayar adı.|
|Etki alanı adı|Bilgisayar için tam etki alanı adı.|
|Uyumluluk durumu|Bilgisayarın genel uyumluluk durumu. Geçerli durumlar **uyumlu** ve **uyumlu değil**.|
|Dışarıda|Kullanıcının BitLocker ilkesinden muaf mı yoksa muaf mı ayrılmadığını gösterir.|
|Cihaz kullanıcıları|Cihazın kullanıcıları.|
|Uyumluluk durumu ayrıntıları|Belirtilen ilkeden bilgisayarın uyumluluk durumu hakkında hata ve durum iletileri.|
|Son iletişim|Uyumluluk durumunu raporlamak için bilgisayarın sunucuyla son iletişim kurmadığı tarih ve saat.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a>BitLocker kurumsal uyumluluk Özeti

Kuruluşunuz genelinde genel BitLocker uyumluluğunu göstermek için bu raporu kullanın. Ayrıca, BitLocker yönetim ilkesini dağıttığınız ayrı bilgisayarların uyumluluğunu gösterir.

[![BitLocker kurumsal uyumluluk özetinin örnek ekran görüntüsü](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|Sütun adı|Açıklama|
|--- |--- |
|Yönetilen bilgisayarlar|BitLocker ilkesiyle yönettiğiniz bilgisayarların sayısı.|
|% Uyumlu|Kuruluşunuzdaki uyumlu bilgisayarların yüzdesi.|
|% Uyumlu değil|Kuruluşunuzdaki uyumlu olmayan bilgisayarların yüzdesi.|
|Bilinmeyen uyumluluk yüzdesi|Uyumluluk durumu bilinmeyen bilgisayarların yüzdesi.|
|Muaf tutulan yüzdesi|BitLocker şifreleme gereksiniminden muaf tutulan bilgisayarların yüzdesi.|
|Muaf olmayan%|BitLocker şifreleme gereksiniminden muaf tutulan bilgisayarların yüzdesi.|
|Uyumlu|Kuruluşunuzdaki uyumlu bilgisayarların sayısı.|
|Uyumlu değil|Kuruluşunuzdaki uyumlu olmayan bilgisayarların sayısı.|
|Bilinmeyen uyumluluk|Bilinen bir uyumluluk durumu olan bilgisayar sayısı.|
|AF|BitLocker şifreleme gereksiniminden muaf tutulan bilgisayarların sayısı.|
|Muaf olmayan|BitLocker şifreleme gereksiniminden muaf olmayan bilgisayar sayısı.|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a>Kurtarma denetim raporu

> [!NOTE]
> Bu rapor, [BitLocker yönetim ve izleme Web sitesinden](helpdesk-portal.md#reports)de kullanılabilir.
>
> Bu raporu Configuration Manager konsolunda görüntülemek için **izleme** çalışma alanına gidin. Gezinti bölmesinde, **Raporlama** düğümünü genişletin, **raporlar**' ı genişletin ve ardından **BitLocker yönetim** klasörünü genişletin. Raporun yerelleştirilmiş sürümü için alt klasörü seçin, örneğin, **en-US**.

BitLocker Kurtarma anahtarlarına erişim isteğinde bulunan kullanıcıları denetlemek için bu raporu kullanın. Aşağıdaki ölçütlere göre filtre uygulayabilirsiniz:

- Belirli bir kullanıcı türü, örneğin bir yardım masası kullanıcısı veya Son Kullanıcı
- İstek başarısız olduysa veya başarılı olduysa
- İstenen belirli anahtar türü: kurtarma anahtarı parolası, kurtarma anahtarı KIMLIĞI veya TPM Parola karması
- Almanın gerçekleştiği bir tarih aralığı

[![BitLocker kurtarma denetim raporunun örnek ekran görüntüsü](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|Sütun&nbsp;adı|Açıklama|
|----------------|----|
|İstek tarihi ve saati|Son kullanıcının veya yardım masası kullanıcısının bir anahtarı istediği tarih ve saat.|
|Denetim isteği kaynağı|İsteğin geldiği site. Geçerli değerler **Self-Service Portal** veya **Yardım Masası**.|
|İstek sonucu|İsteğin durumu. Geçerli değerler **başarılı** veya **başarısız**.|
|Yardım Masası kullanıcısı|Anahtarı isteyen yönetici kullanıcı. Bir yardım masası Yöneticisi, Kullanıcı adını belirtmeden anahtarı kurtardığında, **Son Kullanıcı** alanı boştur. Standart bir yardım masası kullanıcısının bu alanda görünen kullanıcı adını belirtmesi gerekir. Self Servis portalı üzerinden kurtarma için, bu alan ve **Son Kullanıcı** alanı, isteği yapan kullanıcının adını görüntüler.|
|Son kullanıcı|Anahtar alımı isteyen kullanıcının adı.|
|Bilgisayar|Kurtarılan bilgisayarın adı.|
|Anahtar türü|Kullanıcının istediği anahtarın türü. Üç tür anahtar şunlardır:<br/><br/>- **Kurtarma anahtarı parolası**: bir bilgisayarı kurtarma modunda kurtarmak için kullanılır<br/>- **Kurtarma anahtarı kimliği**: başka bir kullanıcı için kurtarma modundaki bir bilgisayarı kurtarmak için kullanılır<br/>- **TPM Parola karması**: bir BILGISAYARı kilitli TPM ile kurtarmak için kullanılır|
|Neden açıklaması|Kullanıcının, formda seçili olan seçeneğe göre belirtilen anahtar türünü neden istediği.|
