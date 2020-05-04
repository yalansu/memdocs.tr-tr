---
title: Yazılım envanteri güvenlik gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager ' de yazılım envanteri için güvenlik ve gizlilik bilgilerini alın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710674"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Configuration Manager 'de yazılım envanteri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager ' de yazılım envanteri için güvenlik ve gizlilik bilgilerini içerir.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Yazılım envanteri için en iyi güvenlik yöntemleri  
 İstemcilerden yazılım envanteri verileri topladığınız durumlar için aşağıdaki en iyi güvenlik yöntemlerini kullanın:  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Envanter verilerini imzalama ve şifreleme|İstemciler HTTPS kullanarak yönetim noktalarıyla iletişim kurduğunda, gönderdikleri tüm veriler SSL kullanılarak şifrelenir. Bununla birlikte, istemci bilgisayarlar intranet üzerindeki yönetim noktaları ile iletişim kurmak için HTTP kullandığında, istemci envanter verileri ve toplanan dosyalar imzalanmamış ve şifrelenmemiş olarak gönderilebilir. Sitenin imzalama gerektirecek ve şifreleme kullanacak şekilde yapılandırıldığından emin olun. Ek olarak, istemciler SHA-256 algoritmasını destekliyorsa SHA-256 isteme seçeneğini belirleyin.|  
|Kritik dosyaları veya hassas bilgileri toplamak için dosya koleksiyonu kullanmayın|Configuration Manager yazılım envanteri, kayıt defteri veya güvenlik hesabı veritabanı gibi kritik sistem dosyalarının kopyalarını toplama özelliğine sahip LocalSystem hesabının tüm haklarını kullanır. Bu dosyalar site sunucusunda kullanılabilir olduğunda, depolanan dosya konumunda Kaynak Okuma haklarına veya NTFS haklarına  sahip birisi içerikleri çözümleyebilir ve güvenliğini tehlikeye atabilmek için muhtemelen istemci hakkındaki önemli ayrıntıları ayırt edebilir.|  
|İstemci bilgisayarlarda yerel yönetici haklarını kısıtlama|Yerel yönetici haklarına sahip bir kullanıcı, envanter bilgisi olarak geçersiz veriler gönderebilir.|  

### <a name="security-issues-for-software-inventory"></a>Yazılım envanteri için güvenlik sorunları  
 Envanterin toplanması olası güvenlik açıklarını ortaya çıkarır. Saldırganlar aşağıdaki işlemleri yapabilirler:  

- Yazılım envanteri istemci ayarı devre dışı bırakıldığında ve dosya koleksiyonu etkin olmadığında bile yönetim noktası tarafından kabul edilecek geçersiz veriler gönderme.  

- Tek bir dosyada aşırı büyük miktarlarda ve çok sayıda dosya içinde veri göndererek hizmet reddine neden olma.  

- Configuration Manager aktarıldığından envanter bilgilerine erişin.  

  Kullanıcılar **Skpswi.dat** adlı gizli bir dosya oluşturabileceklerini ve bu dosyayı bir istemci sabit sürücüsünün köküne yerleştirebileceklerini biliyorsa, bu bilgisayardan yazılım envanteri verilerini toplayamazsınız.  

  Yerel yönetici ayrıcalıklarına sahip bir Kullanıcı herhangi bir bilgiyi envanter verileri olarak gönderebildiğinden, Configuration Manager tarafından toplanan envanter verilerini yetkili olarak düşünmeyin.  

  Yazılım envanteri varsayılan olarak bir istemci ayarı olarak etkindir.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Yazılım envanteri için gizlilik bilgileri  
 Donanım envanteri, Configuration Manager istemcilerde kayıt defterine ve WMI 'ye depolanan tüm bilgileri almanızı sağlar. Yazılım envanteri belirtilen bir türdeki tüm dosyaları bulmanızı veya istemcilerden herhangi bir belirtilen dosyayı toplamanızı sağlar. Varlık Yönetim Bilgileri, donanım ve yazılım envanterini genişleterek ve yeni lisans yönetimi işlevselliği ekleyerek envanter özelliklerini geliştirir.  

 Donanım envanteri, istemci ayarı olarak varsayılan olarak etkindir ve toplanan WMI bilgileri, belirlediğiniz seçeneklere göre belirlenir. Yazılım envanteri varsayılan olarak etkindir, ancak dosyalar varsayılan olarak toplanmaz. Varlık Yönetim Bilgileri veri toplama işlemi otomatik olarak etkinleştirilir, ancak donanım envanteri raporlama sınıflarının etkinleştirilmesini seçebilirsiniz.  

 Envanter bilgileri Microsoft'a gönderilmez. Envanter bilgileri Configuration Manager veritabanında depolanır. İstemciler yönetim noktalarına bağlanmak için HTTPS kullandığında, siteye gönderdikleri envanter verileri aktarım sırasında şifrelenir. İstemciler yönetim noktalarına bağlanmak için HTTP kullanırsa, envanter şifrelemeyi etkinleştirme seçeneğiniz vardır. Envanter verileri, veritabanında şifreli biçimde depolanmaz. Bilgiler, **Eski Envanter Verilerini Sil** veya **Eski Toplanan Dosyaları Sil** site bakım görevleri tarafından her 90 günde bir silinene kadar veritabanında tutulur. Silme aralığını yapılandırabilirsiniz.  

 Donanım envanterini, yazılım envanterini, dosya koleksiyonunu veya Varlık Yönetim Bilgileri veri toplamasını yapılandırmadan önce gizlilik gereksinimlerinizi dikkate alın.  
