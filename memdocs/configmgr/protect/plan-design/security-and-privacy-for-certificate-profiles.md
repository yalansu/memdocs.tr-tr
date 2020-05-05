---
title: Sertifika profili güvenlik ve gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager içindeki kullanıcılar ve cihazlar için sertifika profillerini yönetmeye yönelik en iyi güvenlik yöntemleri hakkında bilgi edinin.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4b7db4537965b17cd56cc4d996eec576c2b18965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722119"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Configuration Manager 'de sertifika profilleri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Sertifika Profilleri için Güvenlik En İyi Yöntemleri  
 Kullanıcılarınızın ve aygıtlarınızın sertifika profillerini yönetirken aşağıdaki güvenlik en iyi yöntemlerini kullanın.  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Internet Information Services'de (IIS) Ağ Aygıtı Kayıt Hizmeti web sitesini, SSL gerektirecek ve istemci sertifikalarını yok sayacak şekilde yapılandırmak dahil olmak üzere, Ağ Aygıtı Kayıt Hizmeti için en iyi güvenlik yöntemlerini belirleyin ve uygulayın.|TechNet’teki Active Directory Sertifika Hizmetleri kitaplığında bulunan [Ağ Cihazı Kayıt Hizmeti Kılavuzu](https://go.microsoft.com/fwlink/p/?LinkId=309016) adlı belgeye bakın.|  
|SCEP sertifika profillerini yapılandırırken, aygıtların ve altyapınızın destekleyebildiği en güvenli seçenekleri kullanın.|Aygıtlarınız ve altyapınız için önerilmiş tüm en iyi güvenlik uygulamalarını belirleyin, uygulayın ve takip edin.|  
|Kullanıcıların birincil cihazlarını tanımlamalarına izin vermek yerine kullanıcı aygıtı benzeşimini elle belirtin. Ayrıca, kullanıcı tabanlı yapılandırmayı etkinleştirmeyin.|Bir SCEP sertifikası profilinde **Yalnızca kullanıcıların birincil cihazında sertifika kaydına izin ver** seçeneğine tıklarsanız, kullanıcılardan veya cihazlardan toplanan bilgileri güvenilir olarak görmeyin. Bu yapılandırmayla SCEP sertifikası profilleri dağıtırsanız ve güvenilen bir yönetici kullanıcı, kullanıcı aygıtı benzeşimini belirtmiyorsa yetkisiz kullanıcılar yükseltilmiş ayrıcalıklar kazanabilir ve kimlik doğrulama için sertifika elde edebilirler.<br /><br /> **Note:** Kullanım tabanlı yapılandırmayı etkinleştirirseniz, bu bilgiler Configuration Manager tarafından güvenliği olmayan durum iletileri kullanılarak toplanır. Bu tehdidi azaltmaya yardımcı olmak için istemci bilgisayarlarla yönetim noktası arasında SMB imzası veya IPsec kullanın.|  
|Sertifika şablonlarına kullanıcılar için Okuma veya Kaydetme izinleri eklemeyin ya da sertifika kayıt noktasını sertifika şablonu denetimini atlayacak şekilde yapılandırmayın.|Configuration Manager, kullanıcılar için okuma ve kaydetme güvenlik izinlerini eklerseniz ve sertifika kayıt noktasını, kimlik doğrulaması mümkün değilse bu denetimi atlamak üzere yapılandırırsanız, her ne yapılandırma en iyi güvenlik yöntemidir. Daha fazla bilgi için bkz. [sertifika profilleri için sertifika şablonu Izinlerini planlama](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Sertifika Profilleri İçin Gizlilik Bilgileri  
 Sertifika profillerini kök sertifika yetkilisi (CA) ve istemci sertifikaları dağıtmak için kullanabilir ve bu aygıtların profiller uygulandıktan sonra uyumlu olup olmadığını değerlendirebilirsiniz. Yönetim noktası uyumluluk bilgisini site sunucusuna gönderir ve Configuration Manager bu bilgileri site veritabanına depolar. Uyumluluk bilgileri konu adı ve parmak izi gibi sertifika özelliklerini kapsar. Aygıtlar bilgiyi yönetim noktasına gönderdiğinde bilgi şifrelenir, ancak site veritabanında şifreli biçimde depolanmaz. Veritabanı, varsayılan zaman aralığı olan 90 gün sonunda **Eski Yapılandırma Yönetimi Verilerini Sil** site bakım görevi tarafından silinene kadar bilgileri saklar. Silme aralığını yapılandırabilirsiniz. Uyumluluk bilgileri Microsoft'a gönderilmez.  

 Sertifika profilleri Configuration Manager bulma kullanılarak toplanan bilgileri kullanır. Bulma için gizlilik bilgileri hakkında daha fazla bilgi için bkz. [güvenlik ve gizlilik](../../core/plan-design/security/security-and-privacy.md)içindeki **bulma için gizlilik bilgileri** bölümü Configuration Manager.  

> [!NOTE]  
>  Kullanıcılara veya cihazlara verilen sertifikalar gizli bilgilere erişim sağlayabilir.  

 Varsayılan ayar olarak aygıtlar sertifika profillerini değerlendirmez. Ayrıca, sertifika profillerini yapılandırmanız ve kullanıcılara veya aygıtlara dağıtmanız gerekir.  

 Sertifika profillerini yapılandırmadan önce, gizlilik gereksinimlerinizi dikkate alın.  
