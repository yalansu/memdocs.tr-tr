---
title: Gönderme Zamanlaması Aracı
titleSuffix: Configuration Manager
description: Configuration Manager istemcisinde bir zamanlamayı tetiklemek için zamanlama Gönder aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723127"
---
# <a name="send-schedule-tool"></a>Gönderme Zamanlaması Aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Zamanlama Gönder aracı [Configuration Manager araçlarından](tools.md)biridir. İstemci üzerindeki bir zamanlamayı tetiklemek veya belirtilen bir yapılandırma temelinin değerlendirmesini tetiklemek için bu uygulamayı kullanın. Yerel bilgisayar için veya uzak bir istemciyi hedefleyerek kullanılır.  

Örneğin, aracı kullanarak bir envanter zamanlaması veya uyumluluk değerlendirmesi tetikleyin. Çok sayıda Configuration Manager istemci Envanter veya uyumluluk durumu bildirmediyse, her istemcide gerekli zamanlamayı başlatmak için aracı çalıştırın.



## <a name="usage"></a>Kullanım

**Sendschedule. exe** ' yi yönetici olarak çalıştırın. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Bir iletiyi (GUID) tetikledikten sonra, bkz. **Smsclientmethodprovider. log**. Kullanılabilir ileti GUID 'Leri hakkında daha fazla bilgi için bkz. [Ileti kimlikleri](#bkmk_sendschedule-guids).

Bir yapılandırma temelinin (DCM UID) değerlendirmesini tetikledikten sonra, bkz. **Dcmagent. log**.



## <a name="command-line-options"></a>Komut satırı seçenekleri


### <a name="option-l"></a>Seçeneği`/L` 
Gönderme için kullanılabilen tüm Ileti GUID 'sini veya DCM UID listesini listeleyin. Her biri için veri tablosunda iletilerin anlamlı adlarını görüntüleyin. Bilgisayar adı yoksa, yerel bilgisayarı kullanır. Makine adı olmadan bir ileti belirtirseniz, bu ileti yerel makineye gönderilir. 



## <a name="examples"></a>Örnekler

#### <a name="list-the-available-messages-on-the-local-machine"></a>Yerel makinedeki kullanılabilir iletileri listeleme 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>İstemci MyPC 'de kullanılabilir iletileri listeleyin: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Yerel makinede donanım envanterini Tetikle
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>MyPC üzerinde donanım envanterini tetikle: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>MyPC üzerinde belirli bir yapılandırma temelinin değerlendirmesini tetikleyin: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a>İleti kimlikleri

|İleti KIMLIĞI  |Görünen Ad  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Donanım Envanteri|
|{00000000-0000-0000-0000-000000000002}|Yazılım Envanteri|
|{00000000-0000-0000-0000-000000000003}|Bulma envanteri|
|{00000000-0000-0000-0000-000000000010}|Dosya koleksiyonu|
|{00000000-0000-0000-0000-000000000011}|IDMıF koleksiyonu|
|{00000000-0000-0000-0000-000000000021}|Makine atamalarını iste|
|{00000000-0000-0000-0000-000000000022}|Makine Ilkelerini değerlendir|
|{00000000-0000-0000-0000-000000000023}|Varsayılan MP görevini Yenile|
|{00000000-0000-0000-0000-000000000024}|LS (konum hizmeti) konumları yenileme görevi|
|{00000000-0000-0000-0000-000000000025}|LS zaman aşımı yenileme görevi|
|{00000000-0000-0000-0000-000000000026}|İlke Aracısı Istek ataması (Kullanıcı)|
|{00000000-0000-0000-0000-000000000027}|İlke Aracısı atamayı değerlendir (Kullanıcı)|
|{00000000-0000-0000-0000-000000000031}|Yazılım kullanım ölçümü kullanım raporu oluşturma|
|{00000000-0000-0000-0000-000000000032}|Kaynak güncelleştirme Iletisi|
|{00000000-0000-0000-0000-000000000037}|Proxy ayarları önbelleği temizleniyor|
|{00000000-0000-0000-0000-000000000040}|Makine Ilkesi aracısını Temizleme|
|{00000000-0000-0000-0000-000000000041}|Kullanıcı Ilkesi aracısını Temizleme|
|{00000000-0000-0000-0000-000000000042}|İlke aracısı makine Ilkesini/atamayı doğrula|
|{00000000-0000-0000-0000-000000000043}|İlke Aracısı Kullanıcı Ilkesini/atamayı doğrular|
|{00000000-0000-0000-0000-000000000051}|MP 'de AD 'de sertifikaları yeniden deneme/yenileme|
|{00000000-0000-0000-0000-000000000061}|Eş DP durum bildirimi|
|{00000000-0000-0000-0000-000000000062}|Eş DP paket denetim zamanlamasını bekliyor|
|{00000000-0000-0000-0000-000000000063}|Toplam güncelleştirme yüklemesi zamanlaması|
|{00000000-0000-0000-0000-000000000101}|Donanım envanteri toplama çevrimi|
|{00000000-0000-0000-0000-000000000102}|Yazılım envanteri toplama çevrimi|
|{00000000-0000-0000-0000-000000000103}|Bulgu verileri toplama çevrimi|
|{00000000-0000-0000-0000-000000000104}|Dosya toplama çevrimi|
|{00000000-0000-0000-0000-000000000105}|IDMıF toplama çevrimi|
|{00000000-0000-0000-0000-000000000106}|Yazılım ölçümü kullanım raporu çevrimi|
|{00000000-0000-0000-0000-000000000107}|Kaynak listesi güncelleştirme döngüsünü Windows Installer|
|{00000000-0000-0000-0000-000000000108}|Yazılım güncelleştirmeleri Ilke eylemi yazılım güncelleştirmeleri atamaları değerlendirme çevrimi|
|{00000000-0000-0000-0000-000000000109}|PDP bakım Ilkesi dal dağıtım noktası bakım görevi|
|{00000000-0000-0000-0000-000000000110}|DCM ilkesi|
|{00000000-0000-0000-0000-000000000111}|Gönderilmemiş durum Iletisi gönder|
|{00000000-0000-0000-0000-000000000112}|Durum sistem ilkesi önbelleği temizleme|
|{00000000-0000-0000-0000-000000000113}|Kaynak ilkesini Güncelleştir|
|{00000000-0000-0000-0000-000000000114}|Depolama Ilkesini Güncelleştir|
|{00000000-0000-0000-0000-000000000115}|Durum sistem ilkesi toplu gönderme yüksek|
|{00000000-0000-0000-0000-000000000116}|Durum sistem ilkesi toplu gönderme düşük|
|{00000000-0000-0000-0000-000000000121}|Uygulama Yöneticisi ilke eylemi|
|{00000000-0000-0000-0000-000000000122}|Uygulama Yöneticisi Kullanıcı ilkesi eylemi|
|{00000000-0000-0000-0000-000000000123}|Uygulama Yöneticisi Genel değerlendirme eylemi|
|{00000000-0000-0000-0000-000000000131}|Güç yönetimi başlatma özetleyicisi|
|{00000000-0000-0000-0000-000000000221}|Uç nokta dağıtımı yeniden değerlendirme|
|{00000000-0000-0000-0000-000000000222}|Uç noktanın ilke yeniden hesaplanması|
|{00000000-0000-0000-0000-000000000223}|Dış olay algılama|



