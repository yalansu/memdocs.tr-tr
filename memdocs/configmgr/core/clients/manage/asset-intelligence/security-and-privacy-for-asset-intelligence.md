---
title: Varlık Yönetim Bilgileri güvenlik gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager Varlık Yönetim Bilgileri için güvenlik ve gizlilik bilgilerini alın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3cf35b050b110c655ac85e82a7990f9ea2ac3636
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714146"
---
# <a name="security-and-privacy-for-asset-intelligence-in-configuration-manager"></a>Configuration Manager Varlık Yönetim Bilgileri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager Varlık Yönetim Bilgileri yönelik güvenlik ve gizlilik bilgilerini içerir.  

##  <a name="security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Varlık Yönetim Bilgileri için en iyi güvenlik uygulamaları  
 Varlık Yönetim Bilgileri’ni kullanırken aşağıdaki en iyi güvenlik uygulamalarını kullanın.  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Bir lisans dosyasını içeri aktardığınızda (Microsoft Toplu Lisanslama dosyası veya bir Genel Lisans Beyanı dosyası) dosyanın ve iletişim kanalının güvenliğini sağlayın.|İçeri aktarma işlemi sırasında site sunucusuna aktarılırken verilerinizin bütünlüğünü sağlamak amacıyla, yalnızca yetkili kullanıcıların lisans dosyalarına erişebildiğinden ve Sunucu İleti Bloğu (SMB) imzasını kullandığından emin olmak için NTFS dosya sistemi izinlerini kullanın.|  
|Lisans dosyalarını içeri aktarmak için en düşük izinler ilkesini kullanın.|Lisans dosyalarını içeri aktaran yönetici kullanıcıya Varlık Yönetim Bilgilerini Yönetme iznini vermek için rol tabanlı yönetimi kullanın. Varlık Yöneticisi’nin yerleşik rolü bu izni içerir.|  

##  <a name="privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Varlık Yönetim Bilgileri için gizlilik bilgileri  
 Varlık Yönetim Bilgileri, kuruluşta daha yüksek düzeyde varlık görünürlüğü sağlamak için Configuration Manager stok özelliklerini genişletir. Varlık Yönetim Bilgileri otomatik olarak etkin değildir. Donanım envanteri raporlama sınıflarını etkinleştirerek toplanan bilgi türünü değiştirebilirsiniz. Daha fazla bilgi için bkz. [varlık yönetim bilgileri yapılandırma](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Varlık Yönetim Bilgileri bilgiler Configuration Manager veritabanında envanter bilgileriyle aynı şekilde depolanır. İstemciler HTTPS kullanarak yönetim noktalarına bağlandığında, yönetim noktasına aktarım sırasında veriler her zaman şifrelenir. İstemciler HTTP kullanarak bağlandığında envanter verileri aktarımını imzalanacak ve şifrelenecek şekilde yapılandırabilirsiniz. Envanter verileri, veritabanında şifreli biçimde depolanmaz. Bilgiler, **Eski Envanter Geçmişini Sil** adlı site bakım görevi tarafından 90 günlük aralıklarla silinene kadar veritabanında tutulur. Silme aralığını yapılandırabilirsiniz.  

 Varlık Yönetim Bilgileri, Microsoft'a kullanıcılar, bilgisayarlar ya da lisans kullanımı hakkında bilgi göndermez. Kategorilere ayırma için System Center Online istekleri göndermeyi seçebilirsiniz; diğer bir deyişle, kategorilere ayrılmamış bir veya daha fazla yazılım başlığını etiketleyebilir ve araştırma ve kategorilere ayırma amacıyla System Center Online’a gönderebilirsiniz. Bir yazılım başlığı karşıya yüklendikten sonra, Microsoft araştırmacıları bu bilgiyi belirler, kategorisine atar ve çevrimiçi hizmeti kullanan tüm müşteriler için kullanılabilir hale getirir. Bilgileri System Center Online'a göndermenin aşağıdaki gizlilik etkilerini bilmeniz gerekir:  

- Karşıya yükleme yalnızca System Center Online’a göndermeyi seçtiğiniz genel yazılım başlığı bilgileri (ad, yayımcı vb.) için geçerlidir. Envanter bilgileri bir karşıya yükleme ile gönderilmez.  

- Karşıya yükleme hiçbir zaman otomatik olarak gerçekleşmez ve sistem bu görevin otomatikleştirilmesi için tasarlanmamıştır. Her yazılım programının yüklenmesini elle seçmeniz ve onaylamanız gerekir.  

- Karşıya yükleme işlemi başlamadan önce, bir iletişim kutusunda tam olarak hangi verilerin karşıya yükleneceği gösterilir.  

- Lisans bilgileri Microsoft'a gönderilmez. Lisans bilgileri Configuration Manager veritabanının ayrı bir alanında saklanır ve Microsoft 'a gönderilemez.  

- Karşıya yüklenen tüm yazılım başlıkları, belirtilen uygulamanın bilgisi ve kategorisi System Center Online Varlık Yönetim Bilgileri kataloğunun bir parçası haline geldiğinden ve ardından kataloğun diğer müşterilerine indirildiğinden herkese açık hale gelir.  

- Yazılım başlığının kaynağı Varlık Yönetim Bilgileri kataloğuna kaydedilmez ve diğer müşterilerin kullanımına sunulmaz. Ancak, özel bir bilgi içeren herhangi bir uygulama başlığını karşıya yüklemediğinizi yine de doğrulamanız gerekir.  

- Yüklenen veriler geri çekilemez.  

  Varlık Yönetim Bilgileri veri toplamasını yapılandırmadan ve System Center Online’a bilgi gönderme kararı vermeden önce, kuruluşunuzun gizlilik gereksinimlerini dikkate alın.  
