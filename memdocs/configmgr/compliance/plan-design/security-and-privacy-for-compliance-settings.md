---
title: Uyumluluk ayarları için güvenlik ve Gizlilik
titleSuffix: Configuration Manager
description: Configuration Manager uyumluluk ayarları için en iyi güvenlik yöntemleri hakkında bilgi edinin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5021a88966c6c57a3b49a907e14bbe06e28286ff
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240652"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Configuration Manager uyumluluk ayarları için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*


## <a name="security-best-practices-for-compliance-settings"></a>Uyumluluk ayarları için en iyi güvenlik yöntemleri  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Hassas verileri izlemeyin.|Bilgilerin açıklanmasının önlenmesine yardım etmek için yapılandırma öğelerini olası hassas bilgileri izlemek üzere yapılandırmayın.|  
|Son kullanıcılar tarafından değiştirilebilecek verileri kullanan uyumluluk kuralları yapılandırmayın.|Yapılandırma seçeneklerine yönelik kayıt defteri ayarları gibi, kullanıcıların değiştirebileceği verilere dayalı bir uyumluluk kuralı oluşturursanız, uyumluluk sonuçları güvenilir olmaz.|  
|Microsoft System Center yapılandırma paketlerini ve diğer yapılandırma verilerini, yalnızca güvenilir bir yayımcıdan geçerli dijital imzası olan dış kaynaklardan içeri aktarın.|Yayımlanan yapılandırma verileri dijital olarak imzalanabilir, böylece yayımlama kaynağını doğrulayabilir ve verilerin değiştirilmediğinden emin olabilirsiniz. Dijital imza denetimi başarısız olursa bir uyarı alırsınız ve içeri aktarmaya devam etmek isteyip istemediğiniz sorulur. Verilerin kaynağını ve bütünlüğünü doğrulayamıyorsanız imzalanmamış verileri içeri aktarmayın.|  
|Başvuru bilgisayarlarını korumak için erişim denetimleri uygulayın.|Yönetici kullanıcı bir kayıt defteri veya dosya sistemi ayarını referans bilgisayara giderek yapılandırırken, referans bilgisayarın tehlikede olmadığından emin olun.|  
|Referans bilgisayara göz atarken iletişim kanalını güvenli hale getirin.|Ağ üzerinden aktarılırken verilerin değiştirilmesini engellemek için, Configuration Manager konsolunu çalıştıran bilgisayar ve referans bilgisayar arasında Internet Protokolü güvenliği (IPSec) veya sunucu ileti bloğu (SMB) kullanın.|  
|Uyumluluk Ayarları Yöneticisi rol tabanlı güvenlik rolü verilen yönetici kullanıcılarını kısıtlayın ve izleyin.|**Uyumluluk Ayarları Yöneticisi** rolü verilen yönetici kullanıcılar, yapılandırma öğelerini hiyerarşideki tüm cihazlara ve tüm kullanıcılara dağıtabilir. Yapılandırma öğeleri çok güçlü olabilir ve örneğin, betikler ve kayıt defterinin yeniden yapılandırmalarını içerebilir.|  

## <a name="privacy-information-for-compliance-settings"></a>Uyumluluk ayarları için gizlilik bilgileri  
 İstemci cihazlarınızın yapılandırma temellerinde dağıttığınız yapılandırma öğeleriyle uyumlu olup olmadığını değerlendirmek için uyumluluk ayarlarını kullanabilirsiniz. Bazı ayarlar uyumsuz olmaları durumunda otomatik olarak düzeltilebilir. Uyumluluk bilgisi yönetim noktası tarafından site sunucusuna gönderilir ve site veritabanında depolanır. Aygıtlar bilgiyi yönetim noktasına gönderdiğinde bilgi şifrelenir, ancak site veritabanında şifreli biçimde depolanmaz. Bilgiler, **Eski Yapılandırma Yönetimi Verilerini Sil** adlı site bakım görevi tarafından 90 günde bir silinene kadar veritabanında tutulur. Silme aralığını yapılandırabilirsiniz. Uyumluluk bilgileri Microsoft'a gönderilmez.  

 Varsayılan ayar olarak, cihazlar uyumluluk ayarlarını değerlendirmez. Ayrıca, yapılandırma öğelerini ve yapılandırma temellerini yapılandırmanız ve ardından bunları cihazlara dağıtmanız gerekir.  
