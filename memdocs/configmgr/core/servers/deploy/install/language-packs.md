---
title: Dil paketleri
titleSuffix: Configuration Manager
description: Configuration Manager ' de kullanılabilen dil desteği hakkında bilgi edinin.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53aa7e932e782254f63b422526b315f3ce91f397
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906166"
---
# <a name="language-packs-in-configuration-manager"></a>Configuration Manager dil paketleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Configuration Manager dil desteği hakkında teknik ayrıntılar sağlar. Site sunucularının ve istemcilerinin Configuration Manager, dilden bağımsız olarak kabul edilir. Merkezi bir yönetim sitesinde ve birincil sitelerde **sunucu dil paketlerini** veya **istemci dil paketlerini** yükleyerek görüntüleme dilleri için destek ekleyin. Site yükleme işlemi sırasında kullanılabilir dil paketi dosyalarından bir sitede destekedilecek sunucu ve istemci dillerini seçersiniz.
 
Her siteye birden çok dil yükler. Yalnızca kullandığınız dilleri yüklemeniz gerekir.  

- Her site Configuration Manager konsolları için birden çok dili destekler.  

- Her bir sitede tek tek istemci dil paketlerini yükleyerek desteklemek istediğiniz istemci dilleri için destek ekleyin.  

Aşağıdaki bileşenlerle eşleşen bir dil için destek yüklediğinizde:  

- Bir bilgisayarın görüntüleme dili: hem Configuration Manager konsolu hem de söz konusu bilgisayarda çalışan istemci kullanıcı arabirimi bu dilin bilgilerini görüntüler.  

- Bir bilgisayarın Web tarayıcısı tarafından kullanılmakta olan dil tercihi: Uygulama Kataloğu veya SQL Server Reporting Services dahil olmak üzere Web tabanlı bilgilere yapılan bağlantılar bu dilde görüntülenir.  


Configuration Manager Kurulum 'u çalıştırdığınızda, önkoşul ve yeniden dağıtılabilir dosyaların bir parçası olarak dil paketi dosyalarını indirir. Kurulum 'u çalıştırmadan önce bu dosyaları indirmek için [Kurulum Yükleyici](setup-downloader.md) 'yi de kullanabilirsiniz.   



## <a name="server-languages"></a>Sunucu dilleri  

Bir yerel ayar KIMLIĞINI sunucularda desteklemek istediğiniz bir dile eşlemek için aşağıdaki tabloyu kullanın. Yerel ayar kimlikleri hakkında daha fazla bilgi için bkz. [Microsoft tarafından atanan yerel kimlikler](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Sunucu dili|Yerel Kimlik (LCID)|Üç harfli kod|  
|---------------------|------------------------|-----------------------|  
|İngilizce (varsayılan)|0409|ENU|  
|Basitleştirilmiş Çince|0804|CHS|  
|Çince (Geleneksel, Tayvan)|0404|CHT|  
|Çekçe|0405|CSY|  
|Felemenkçe - Hollanda|0413|NLD|  
|Fransızca|040c|FRA|  
|Almanca|0407|DEU|  
|Macarca|040e|HUN|  
|İtalyanca - İtalya|0410|ITA|  
|Japonca|0411|JPN|  
|Korece|0412|KOR|  
|Lehçe|0415|PLK|  
|Portekizce - Brezilya|0416|PTB|  
|Portekizce - Portekiz|0816|PTG|  
|Rusça|0419|RUS|  
|İspanyolca - İspanya|0c0a|ESN|  
|İsveççe|041d|SVE|  
|Türkçe|041f|TRK|  



## <a name="client-languages"></a>İstemci dilleri  

Bir yerel ayar KIMLIĞINI istemci bilgisayarlarında desteklemek istediğiniz bir dile eşlemek için aşağıdaki tabloyu kullanın. Yerel ayar kimlikleri hakkında daha fazla bilgi için bkz. [Microsoft tarafından atanan yerel kimlikler](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|İstemci dili|Yerel Kimlik (LCID)|Üç harfli kod|  
|---------------------|------------------------|-----------------------|  
|İngilizce (varsayılan)|0409|ENG|  
|Çince -Basitleştirilmiş|0804|CHS|  
|Çince (Geleneksel, Tayvan)|0404|CHT|  
|Çekçe|0405|CSY|  
|Danca|0406|DAN|  
|Felemenkçe - Hollanda|0413|NLD|  
|Fince|040b|FIN|  
|Fransızca|040c|FRA|  
|Almanca|0407|DEU|  
|Yunanca|0408|ELL|  
|Macarca|040e|HUN|  
|İtalyanca - İtalya|0410|ITA|  
|Japonca|0411|JPN|  
|Korece|0412|KOR|  
|Norveççe|0414|NOR|  
|Lehçe|0415|PLK|  
|Portekizce (Brezilya)|0416|PTB|  
|Portekizce (Portekiz)|0816|PTG|  
|Rusça|0419|RUS|  
|İspanyolca - İspanya|0c0a|ESN|  
|İsveççe|041d|SVE|  
|Türkçe|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Mobil aygıt istemci dilleri  
Mobil cihaz dilleri için destek eklediğinizde, desteklenen tüm mobil cihaz istemci dilleri dahildir. Mobil cihaz desteği için ayrı dil paketleri seçemezsiniz.  



## <a name="identify-installed-language-packs"></a>Yüklü dil paketlerini tanımla  
Configuration Manager istemcisini çalıştıran bir bilgisayarda yüklü olan dil paketlerini belirlemek için, bilgisayarın kayıt defterindeki yüklü dil paketlerinin yerel ayar KIMLIĞINI (LCıD) arayın. Bu bilgilere aşağıdaki kayıt defteri yolunda ulaşılabilir:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Bu bilgileri toplamak için donanım envanterini özelleştirin. Sonra dil ayrıntılarını görüntülemek için özel bir rapor oluşturun. Özel donanım envanteri toplama hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../../clients/manage/inventory/configure-hardware-inventory.md). Daha fazla bilgi için bkz. [rapor oluşturma](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
