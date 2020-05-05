---
title: Unicode ve ASCII desteği
titleSuffix: Configuration Manager
description: Configuration Manager nesnelerinde Unicode ve ASCII karakterleri için destek hakkında bilgi edinin.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717555"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Configuration Manager 'da Unicode ve ASCII desteği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Unicode karakterler kullanarak çoğu nesneyi oluşturur. Ancak, birkaç nesne yalnızca ASCII karakterlerini destekler veya başka sınırlamalara sahiptir.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a>ASCII karakterleri kullanan nesneler

Aşağıdaki nesneleri oluşturduğunuzda Configuration Manager yalnızca ASCII karakter kümesini destekler:  

- Site kodu  

- Tüm site sistem sunucusu bilgisayar adları  

- Aşağıdaki Configuration Manager hesapları:  

    > [!NOTE]  
    > Bu hesaplar, Rusya 'da çalışan bir sitede ASCII karakterlerini ve RUS karakterleri destekler.  

    - Client Push yükleme hesabı  

    - Yönetim noktası veritabanı bağlantı hesabı  

    - Ağ erişim hesabı  

    - Paket erişim hesabı  

    - Standart gönderici hesabı  

    - Site sistemi yükleme hesabı  

    - Yazılım güncelleştirme noktası bağlantı hesabı  

    - Yazılım güncelleştirme noktası proxy sunucu hesabı  

    > [!NOTE]  
    > Rol tabanlı yönetim için belirttiğiniz hesaplar Unicode 'U destekler.  
    >
    > Raporlama Hizmetleri noktası hesabı, RUS karakter dışında Unicode 'u destekler.  

- Site sunucuları ve site sistemleri için tam etki alanı adı (FQDN)  

- Configuration Manager için yükleme yolu  

- Örnek adlarını SQL Server  

- Aşağıdaki site sistem rolleri için yol:  

    - Kayıt noktası  

    - Kayıt proxy noktası  

    - Raporlama hizmetleri noktası  

    - Durum Geçiş noktası  

- Aşağıdaki klasörler için yol:  

    - İstemci durumu geçiş verilerini depolayan klasör  

    - Configuration Manager raporlarını içeren klasör  

    - Configuration Manager yedeklemesini depolayan klasör  

    - Site kurulumu için yükleme kaynak dosyalarını depolayan klasör  

    - Kurulum tarafından kullanılmak üzere Önkoşul indirmelerinin depolandığı klasör  

- Aşağıdaki nesneler için yol:  

    - IIS Web sitesi  

    - Sanal uygulama yükleme yolu  

    - Sanal uygulama adı  

- Önyükleme medyası ISO dosya adları  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a>Ek sınırlamalar

Desteklenen karakter kümeleri ve dil sürümleri için ek sınırlamalar aşağıda verilmiştir:  

- Configuration Manager, site sunucusu bilgisayarının yerel ayarının değiştirilmesini desteklemez.  

- Bir kuruluş sertifika yetkilisi (CA), çift baytlı karakter kümeleri (DBCS) kullanan istemci bilgisayar adlarını desteklemez. Kullanabileceğiniz istemci bilgisayar adları, ıA5 karakter kümesinin PKI sınırlamasıyla sınırlıdır. Configuration Manager,, DBCS kullanan CA adlarını veya konu adı değerlerini desteklemez.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a>Yerelleştirilmemiş nesneler

Configuration Manager veritabanı, depoladığı çoğu nesne için Unicode 'U destekler. Mümkün olduğunda, bu bilgileri bir bilgisayarın yerel ayarıyla eşleşen işletim sistemi dilinde görüntüler. İstemci arabirimi veya Configuration Manager konsolunun bilgisayarın işletim sistemi dilinde bilgi görüntülemesi için, bilgisayarın yerel ayarı bir siteye yüklediğiniz istemci veya sunucu diliyle aynı olmalıdır.  

Çeşitli Configuration Manager nesneleri Unicode 'U desteklemez. Bunlar, ASCII kullanılarak veritabanında depolanır veya ek dil kısıtlamalarına sahiptir. Bu bilgiler, her zaman ASCII karakter kümesi kullanılarak veya nesneyi oluştururken kullanımda olan dilde görüntülenir.  
