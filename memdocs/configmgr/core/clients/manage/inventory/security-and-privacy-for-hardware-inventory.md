---
title: Donanım envanteri güvenlik gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager 'de donanım envanteri için güvenlik ve gizlilik bilgilerini alın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710688"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Configuration Manager 'de donanım envanteri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager ' deki donanım envanteri için güvenlik ve gizlilik bilgilerini içerir.  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Donanım envanteri için en iyi güvenlik yöntemleri  
 İstemcilerden donanım envanteri verileri topladığınız durumlar için aşağıdaki en iyi güvenlik yöntemlerini kullanın:  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Envanter verilerini imzalama ve şifreleme|İstemciler HTTPS kullanarak yönetim noktalarıyla iletişim kurduğunda, gönderdikleri tüm veriler SSL kullanılarak şifrelenir. Bununla birlikte, istemci bilgisayarlar intranet üzerindeki yönetim noktaları ile iletişim kurmak için HTTP kullandığında, istemci envanter verileri ve toplanan dosyalar imzalanmamış ve şifrelenmemiş olarak gönderilebilir. Sitenin imzalama gerektirecek ve şifreleme kullanacak şekilde yapılandırıldığından emin olun. Ek olarak, istemciler SHA-256 algoritmasını destekliyorsa SHA-256 isteme seçeneğini belirleyin.|  
|Yüksek güvenlikli ortamlarda IDMIF ve NOIDMIF dosyalarını toplama|Donanım envanteri koleksiyonunu genişletmek için IDMIF ve NOIDMIF dosya koleksiyonunu kullanabilirsiniz. Gerektiğinde, Configuration Manager yeni tablolar oluşturur veya ıDMıF ve NOıDMıF dosyalarındaki özelliklere uyum sağlamak için Configuration Manager veritabanında var olan tabloları değiştirir. Ancak, Configuration Manager ıDMıF ve NOıDMıF dosyalarını doğrulamaz, bu nedenle bu dosyalar değiştirilmesini istemediğiniz tabloları değiştirmek için kullanılabilir. Geçersiz veriler geçerli verilerin üzerine yazılabiliyordu. Ayrıca, büyük miktarlarda veri eklenebilir ve bu verilerin işlenmesi tüm Configuration Manager işlevlerde gecikmelere neden olabilir. Bu riskleri azaltmak için **MIF dosyalarını topla** donanım envanteri istemci ayarını **Hiçbiri**olarak yapılandırın.|  

### <a name="security-issues-for-hardware-inventory"></a>Donanım envanteri için güvenlik sorunları  
 Envanterin toplanması olası güvenlik açıklarını ortaya çıkarır. Saldırganlar aşağıdaki işlemleri yapabilirler:  

- Yazılım envanteri istemci ayarı devre dışı bırakıldığında ve dosya koleksiyonu etkin olmadığında bile yönetim noktası tarafından kabul edilecek geçersiz veriler gönderme.  

- Tek bir dosyada aşırı büyük miktarlarda ve çok sayıda dosya içinde veri göndererek hizmet reddine neden olma.  

- Configuration Manager aktarıldığından envanter bilgilerine erişin.  

  Yerel yönetici ayrıcalıklarına sahip bir Kullanıcı herhangi bir bilgiyi envanter verileri olarak gönderebildiğinden, Configuration Manager tarafından toplanan envanter verilerini yetkili olarak düşünmeyin.  

  Donanım envanteri varsayılan olarak bir istemci ayarı olarak etkindir.  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Donanım envanteri için gizlilik bilgileri  
 Donanım envanteri, Configuration Manager istemcilerde kayıt defterine ve WMI 'ye depolanan tüm bilgileri almanızı sağlar. Yazılım envanteri belirtilen bir türdeki tüm dosyaları bulmanızı veya istemcilerden herhangi bir belirtilen dosyayı toplamanızı sağlar. Varlık Yönetim Bilgileri, donanım ve yazılım envanterini genişleterek ve yeni lisans yönetimi işlevselliği ekleyerek envanter özelliklerini geliştirir.  

 Donanım envanteri, istemci ayarı olarak varsayılan olarak etkindir ve toplanan WMI bilgileri, belirlediğiniz seçeneklere göre belirlenir. Yazılım envanteri varsayılan olarak etkindir, ancak dosyalar varsayılan olarak toplanmaz. Varlık Yönetim Bilgileri veri toplama işlemi otomatik olarak etkinleştirilir, ancak donanım envanteri raporlama sınıflarının etkinleştirilmesini seçebilirsiniz.  

 Envanter bilgileri Microsoft'a gönderilmez. Envanter bilgileri Configuration Manager veritabanında depolanır. İstemciler yönetim noktalarına bağlanmak için HTTPS kullandığında, siteye gönderdikleri envanter verileri aktarım sırasında şifrelenir. İstemciler yönetim noktalarına bağlanmak için HTTP kullanırsa, envanter şifrelemeyi etkinleştirme seçeneğiniz vardır. Envanter verileri, veritabanında şifreli biçimde depolanmaz. Bilgiler, **Eski Envanter Verilerini Sil** veya **Eski Toplanan Dosyaları Sil** site bakım görevleri tarafından her 90 günde bir silinene kadar veritabanında tutulur. Silme aralığını yapılandırabilirsiniz.  

 Donanım envanterini, yazılım envanterini, dosya koleksiyonunu veya Varlık Yönetim Bilgileri veri toplamasını yapılandırmadan önce gizlilik gereksinimlerinizi dikkate alın.  
