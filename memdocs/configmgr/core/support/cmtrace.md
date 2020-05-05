---
title: CMTrace
titleSuffix: Configuration Manager
description: Configuration Manager günlük dosyalarını görüntülemek için CMTrace aracının nasıl kullanılacağını öğrenin.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723428"
---
# <a name="cmtrace"></a>CMTrace

*Uygulama hedefi: Configuration Manager (geçerli dal)*

CMTrace [Configuration Manager araçlarından](tools.md)biridir. Aşağıdaki türler dahil olmak üzere günlük dosyalarını görüntülemenize ve izlemenize olanak tanır:  

- Configuration Manager veya Istemci Bileşen Yöneticisi (CCM) biçimindeki günlük dosyaları  

- Windows Installer günlükleri gibi düz ASCII veya Unicode metin dosyaları  

Araç, günlük dosyalarının vurgulanmasını, filtrelenmesini ve hata aramasını sağlayarak analiz etmenize yardımcı olur.

Sürüm 1806 ' den başlayarak, CMTrace günlük görüntüleme aracı Configuration Manager istemcisiyle birlikte otomatik olarak yüklenir. Bu, varsayılan olarak olan istemci yükleme dizinine eklenir `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace,. log dosya uzantısını açmak için Windows 'a otomatik olarak kayıtlı değildir. Daha fazla bilgi için bkz. [dosya ilişkilendirmeleri](#file-associations).  

Sürüm 1906 ' den başlayarak **Onetrace** , Destek Merkezi 'nin bulunduğu yeni bir günlük görüntüleyicisine sahiptir. Geliştirme ile CMTrace 'e benzer şekilde çalışır. Daha fazla bilgi için bkz. [Destek Merkezi OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Kullanım

**CMTrace. exe**' yi çalıştırın. Aracı ilk kez çalıştırdığınızda dosya ilişkilendirmesi için bir istem görürsünüz. Daha fazla bilgi için bkz. [dosya ilişkilendirmeleri](#file-associations).

Aşağıdaki menülerden CMTrace ' de birçok eylemi gerçekleştirebilirsiniz:

- [Dosya](#file-menu)
- [Araçlar](#tools-menu)

### <a name="file-menu"></a>Dosya menüsü

Aşağıdaki eylemler **Dosya** menüsünde mevcuttur:  

- [Aç](#open)
- [Sunucuda aç](#open-on-server)
- [Yazdırdığımda](#print)
- [Tercihler](#preferences)

Dosya menüsü, son sekiz son dosyayı da listeler. Bu günlüklerden birini Dosya menüsünden seçerek hızlıca yeniden açın.

#### <a name="open"></a>Open

Günlük dosyasına gitmek için Aç iletişim kutusunu görüntüler.

Aşağıdaki türlerin dosyaları için görünümü filtreleyin:

- Günlük dosyaları (\*. log)  
- Eski günlük dosyaları (\*. LO_)
- Tüm dosyalar (\*.\*)

Aşağıdaki iki seçenek varsayılan olarak seçilmemektedir:  

- **Mevcut satırları yoksay**: seçildiğinde, CMTrace seçili günlük dosyasının mevcut içeriğini yoksayar ve yalnızca eklendikçe yeni satırları görüntüler. Günlük dosyasının tam geçmişine ihtiyacınız olmadığında yalnızca yeni eylemleri izlemek için bu seçeneği kullanın.  

- **Seçili dosyaları birleştir**: Bu seçeneği etkinleştirir ve birden fazla günlük dosyası seçerseniz CMTrace görünümdeki seçili günlükleri birleştirir. Tek bir günlük dosyası gibi görüntüler. Birleştirilmiş günlük güncellenir ve tek bir günlük dosyası gibi diğer tüm CMTrace özelliklerini destekler.  

#### <a name="open-on-server"></a>Sunucuda aç

Bir site sistem bilgisayarındaki Configuration Manager logs klasörüne, standart tarama iletişim kutusunu kullanarak gözatamazsınız. Ayrıca, bir uzak bilgisayar için ağa da gidebilirsiniz.

Gözatabilmeniz için bir uzak bilgisayar seçtiğinizde, CMTrace Configuration Manager paylaşımının olup olmadığını denetler. Configuration Manager günlük dosyalarıyla bir paylaşma bulamazsa, bir hata iletisi görüntüler.  

Göz atma olmadan, bilinen bir bilgisayara doğrudan bağlanmak için [Aç](#open) eylemini kullanın. Ardından, UNC biçimini kullanarak bir sunucu adı girin ve paylaşma yapın.

#### <a name="print"></a>Yazdır

Standart Windows Yazdır iletişim kutusunu görüntüleyin. Bu eylem, geçerli günlük dosyasını bir yazıcıya gönderir. Çıkışı, CMTrace tercihlerinin yazdırma sekmesindeki ayarlara göre biçimlendirir.

#### <a name="preferences"></a>Tercihler

CMTrace ayarlarını yapılandırın. Aşağıdaki seçenekler mevcuttur:  

- **Genel** sekmesi  

    - **Güncelleştirme aralığı**: CMTrace 'in günlük dosyalarındaki değişiklikleri ne sıklıkta denetleyeceğini denetler ve yeni satırları yükler. Varsayılan olarak, bu değer 500 milisaniyedir.  

    - Vurgula: CMTrace 'in seçtiğiniz günlük satırlarını **vurgulamada**kullandığı rengi ayarlar. Varsayılan olarak, bu renk temel sarı (kırmızı: 255, yeşil: 255, mavi: 0).  

    - **Sütunlar**: günlük görünümünde görünür olan sütunları ve görünecekleri sırayı yapılandırır. Varsayılan olarak, günlük metnini, bileşeni, tarih/saat ve Iş parçacığını görüntüler.  

- **Yazdırma** sekmesi  

    - **Sütunlar**: günlük dosyalarını yazdırırken hangi sütunları kullandığını ve görünecekleri sırayı yapılandırın. Varsayılan olarak, görüntülendiği şekilde aynı sütunları yazdırır.  

    - **Yönlendirme**: günlük dosyalarını yazdırırken varsayılan baskı yönünü ayarlar. Yazdır iletişim kutusunda bu ayarı geçersiz kılın. Varsayılan olarak dikey yönü kullanır.  

- **Gelişmiş** sekmesi  

    - **Yenileme aralığı**: CMTrace 'in, çok sayıda satır yüklerken belirtilen bir aralıktaki günlük görünümünü güncelleştirmesine zorlar. Varsayılan olarak, bu seçenek sıfır değeriyle devre dışıdır.  

        > [!Note]  
        > Genel olarak, **yenileme aralığını**değiştirmeyin. Büyük günlük dosyaları açmak için gereken süreyi önemli ölçüde artırabilir.

### <a name="tools-menu"></a>Araçlar menüsü

**Araçlar** menüsünde aşağıdaki eylemler mevcuttur:

- [Bilgi](#find)
- [Sonrakini Bul](#find-next)
- [Panoya kopyala](#copy-to-clipboard)
- [Vurgula](#highlight)
- [Filtrele](#filter)
- [Hata arama](#error-lookup)
- [Duraklat](#pause)
- [Ayrıntıları göster/gizle](#showhide-details)
- [Bilgi bölmesini göster/gizle](#showhide-info-pane)

#### <a name="find"></a>Bul

Belirtilen bir metin dizesi için açık günlük dosyasında arama yapın.  

#### <a name="find-next"></a>Sonrakini Bul

Daha önce bul iletişim kutusunda belirttiğiniz gibi bir sonraki eşleşen dizeyi bulur.  

#### <a name="copy-to-clipboard"></a>Panoya kopyala

Seçili satırları Windows panosuna düz metin olarak kopyalar. Configuration Manager ve CCM günlük dosyalarını inceyorsanız, sütunları görünümle aynı sırayla kopyalar. Her sütunu bir sekme karakteriyle ayırır. Günlükleri e-posta iletilerine veya diğer belgelere kopyalarken bu eylemi kullanın.  

#### <a name="highlight"></a>Vurgula

Her günlük girişinin metninde arama yapmak için CMTrace 'in kullandığı bir dize girin. Daha sonra girdiğiniz dize ile eşleşen herhangi bir günlük metnini vurgular.  

- Vurgu, tercihlerinde belirttiğiniz rengi kullanır.  

- Vurgulamayı devre dışı bırakmak için bu alandan dizeyi temizleyerek.  

- Ondalık veya onaltılık bir sayı girerseniz, CMTrace değeri Iş parçacığı sütunuyla eşleştirmeye çalışır. Tek bir iş parçacığının işlenmesini, onunla etkileşime girebilecek diğer iş parçacıklarını filtrelemeden vurgulamak için bu davranışı kullanın.  

- Dizeleri servis talebine göre karşılaştırmak için, **büyük/küçük harfe duyarlı**seçeneğini etkinleştirin.  

#### <a name="filter"></a>Filtre

Belirtilen ölçütlere göre günlük satırlarını göster veya gizle. Görünür olup olmadıklarına bakılmaksızın dört sütundan herhangi birine filtre uygulayın. Bu ayarlar, her açılan günlük dosyası için geçerlidir.

Örnekler:
<!--SCCMDocs issue #603-->

- "Eylem" veya "Grup" içeren giriş metninde **Smsts. log dosyasına** filtre uygulayın.
- Giriş metninin "hedef" içerdiğinde **InventoryAgent. log dosyasına** filtre uygulayın.

#### <a name="error-lookup"></a>Hata arama

Bir açıklama göstermek için bir hata kodunu ondalık ya da onaltılık biçimde yazın veya yapıştırın. Olası hata kaynakları şunlardır: Windows, WMI veya WinHTTP.

#### <a name="pause"></a>Duraklat

Günlük izlemeyi askıya alın veya yeniden başlatın. Aşağıdaki kullanım örnekleri, bu eylemi kullanmanın olası nedenlerinden bazılarıdır:  

- CMTrace günlük dosyası bilgilerini çok hızlı görüntülüyor  

- Günlük izlemeyi duraklatdığınızda, geçerli dosya yeni bir günlüğe kaydedildiğinde CMTrace 'in görüntülediği bilgiler kaybolmaz  

- Günlük dosyasını incelerken CMTrace 'in yeni verileri görüntülemesini durdurmak istediğinizde  

#### <a name="showhide-details"></a>Ayrıntıları göster/gizle

Günlük metni dışındaki tüm sütunları göster veya gizle. Ayrıca, günlük metni sütununu pencerenin genişliğine genişletir. Günlükleri düşük ekran çözünürlüğüne sahip bir bilgisayarda görüntülerken bu eylemi kullanın. Daha fazla günlük metni görüntüler.  

> [!Note]  
> Düz metin dosyalarını görüntülerken, CMTrace her zaman boş olduklarından ayrıntıları otomatik olarak gizler.  

#### <a name="showhide-info-pane"></a>Bilgi bölmesini göster/gizle

Bilgi bölmesini gösterin veya gizleyin. Günlükleri düşük ekran çözünürlüğüne sahip bir bilgisayarda görüntülerken bu eylemi kullanın. Daha fazla günlüğe kaydetme ayrıntılarını görüntüler.  


## <a name="log-pane"></a>Günlük bölmesi

Günlük bölmesi CMTrace penceresinin en üstünde bulunur. Günlük dosyalarındaki satırları görüntüler.

Bir satırı seçtiğinizde, geçici olarak Windows seçim renk düzeni kullanılarak vurgulanır.

Vurgulanan satırlar, **Araçlar** menüsündeki **Vurgula** seçeneğiyle tanımladığınız ölçütlere göre eşleşir. Vurgu, **tercihlerinde**belirttiğiniz rengi kullanır.

CMTrace, hata içeren satırları kırmızı bir arka plan ve sarı metin rengi ile görüntüler. CCM biçimli günlüklerde, günlük girişlerinde girişi bir hata olarak belirten açık bir tür değeri vardır. Diğer günlük biçimleri için CMTrace, her girişte "hata" ile eşleşen herhangi bir metin dizesi için büyük/küçük harfe duyarsız bir arama yapar.

Sarı bir arka plan kullanarak uyarıları olan satırları görüntüler. CCM biçimli günlüklerde, günlük girişlerinde girişi uyarı olarak gösteren bir açık tür değeri vardır. Diğer günlük biçimleri için CMTrace, her girişte "uyar" ile eşleşen herhangi bir metin dizesi için büyük/küçük harfe duyarsız bir arama yapar.


## <a name="info-pane"></a>Bilgi bölmesi

Bilgi bölmesi, CMTrace penceresinin alt kısmında bulunur. Aşağıdaki özellikleri içerir:

- Şu anda seçili günlük girdisiyle ilgili ayrıntılar  

- Günlük metnini görüntüleyen metin kutusu  

- Biçimlendirilen metnin okunması daha kolay olacak şekilde satır başı görüntüler  

- Günlük bölmesinde tamamen görünmeyen uzun girdileri okumak daha kolay  

**Araçlar** menüsünde **bilgi bölmesini göster/gizle** seçeneği ile bilgi bölmesini gösterin veya gizleyin. Bilgi bölmesi günlük penceresinin yarısından fazla sürüyorsa, CMTrace onu otomatik olarak gizler.

### <a name="progress-bar"></a>İlerleme çubuğu

Bir günlük dosyasını ilk açışınızda CMTrace, bilgi bölmesini bir ilerleme çubuğu ile değiştirir. Bu işlem, var olan dosya içeriklerinin ne kadarının yüklendiğini gösterir. İlerleme, yüzde 100 ' a ulaştığında CMTrace İlerleme çubuğunu kaldırır ve bilgi bölmesi ile değiştirir. Büyük dosyaları yüklediğinizde bu davranış, yükün ne kadar süreceğine ilişkin bir gösterge sağlar.

### <a name="status-bar"></a>Durum çubuğu

Configuration Manager biçimlendirme ve CCM biçimli günlük dosyaları için durum çubuğu, seçili günlük girdileri için geçen süreyi görüntüler. Tek bir giriş seçerseniz araç, seçili girişe ilk günlük girdisinden geçen süreyi görüntüler. Birden çok giriş seçerseniz, en üstteki seçili girdiden en alttaki seçili girişe kadar olan süreyi hesaplar. CMTrace bu bilgileri aşağıdaki gibi biçimlendirir:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Windows kabuğu tümleştirmesi

CMTrace [dosya ilişkilendirmelerini](#file-associations) destekler ve [sürükle ve bırak](#drag-and-drop).

### <a name="file-associations"></a>Dosya ilişkilendirmeleri

CMTrace, kendisini. log ve. lo_ dosya adı uzantılarıyla ilişkilendirebilir. Program başladığında, bu dosya adı uzantılarıyla zaten ilişkili olup olmadığını anlamak için kayıt defterini denetler. CMTrace hiçbir dosya adı uzantısıyla ilişkili değilse, dosya adı uzantılarını CMTrace ile ilişkilendirmeniz istenir. **Bunu bana bir daha sorma**' yı seçerseniz CMTrace bu bilgisayarda her çalıştırıldığında bu denetimi atlar.

### <a name="drag-and-drop"></a>Sürükle ve bırak

CMTrace, temel sürükle ve bırak işlevlerini destekler. Bir günlük dosyasını açmak için Windows Gezgini ' nden CMTrace 'e sürükleyin.


## <a name="other-tips"></a>Diğer ipuçları

### <a name="last-directory-registry-key"></a>Son dizin kayıt defteri anahtarı

<!--511280-->
Varsayılan olarak CMTrace, açtığınız son günlük konumunu kaydeder. Bu davranış, site sunucusunda her seferinde günlük yolunda varsayılan olarak kullanılacak şekilde yararlıdır.

Bunu bir istemcide ilk kez başlattığınızda, varsayılan olarak geçerli çalışma dizini olur. Bu konum, CMTrace 'i kaydettiğiniz yol veya gibi `%userprofile%\Desktop`bir yol olabilir.

Kayıt defteri anahtarındaki `HKEY_CURRENT_USER\Software\Microsoft\Trace32` **son dizin** değeri, bu varsayılan konumu denetler. Bu değeri istemcileriniz üzerinde olarak `%windir%\CCM\Logs` ayarlarsanız, CMTrace ilk kez çalıştırdığınızda dosyaları istemci günlüğü konumunda açar.


## <a name="see-also"></a>Ayrıca bkz.

- [Günlük dosyaları](../plan-design/hierarchy/log-files.md)

- [Destek Merkezi günlük dosyası Görüntüleyici](support-center.md#support-center-log-file-viewer)

- [Destek Merkezi OneTrace](support-center-onetrace.md)
