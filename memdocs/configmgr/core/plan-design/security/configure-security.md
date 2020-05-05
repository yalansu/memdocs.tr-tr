---
title: Güvenliği yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager için güvenlikle ilgili seçenekleri yapılandırın.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718668"
---
# <a name="configure-security-in-configuration-manager"></a>Configuration Manager güvenliği yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için güvenlikle ilgili seçenekleri ayarlamanıza yardımcı olması için bu makaledeki bilgileri kullanın. Aşağıdaki güvenlik seçeneklerini ele almaktadır:
- İstemci PKI sertifikaları için [istemci bilgisayar iletişimi](#BKMK_ConfigureClientPKI)  
- [İmzalama ve şifreleme](#BKMK_ConfigureSigningEncryption)  
- [Rol tabanlı yönetim](#BKMK_ConfigureRBA)  
- [Hesapları yönetme](#BKMK_ManageAccounts)  
- [Azure Active Directory'yi yapılandırma](#bkmk_azuread)  
- [SMS sağlayıcısı kimlik doğrulamasını yapılandırma](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> İstemci PKI sertifikaları için ayarları yapılandırma  

Internet Information Services (IIS) kullanan site sistemlerine yapılan istemci bağlantılarına yönelik ortak anahtar altyapısı (PKI) sertifikalarını kullanmak istiyorsanız bu sertifikaların ayarlarını yapılandırmak için aşağıdaki yordamı kullanın.  

#### <a name="to-configure-client-pki-certificate-settings"></a>İstemci PKI sertifikası ayarlarını yapılandırmak için  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Yapılandırılacak birincil siteyi seçin.  

2.  Şeritte **Özellikler**' i seçin. Ardından **Istemci bilgisayar iletişimi** sekmesine geçin.  

    > [!Note]
    > Sürüm 1906 ' den başlayarak bu sekmeye **Iletişim güvenliği**denir.<!-- SCCMDocs#1645 -->  

3.  IIS kullanan site sistemleri için ayarları seçin.  

    - **Yalnızca https**: siteye atanan ISTEMCILER, IIS kullanan site sistemlerine bağlandıklarında her zaman BIR istemci PKI sertifikası kullanır.  

    - **Https veya http**: istemcilerin PKI sertifikaları kullanmasına gerek yoktur.  

    - **Http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanın**: Bu ayar hakkında daha fazla bilgi için bkz. [Gelişmiş http](../hierarchy/enhanced-http.md).  

4.  İstemci bilgisayarlar için ayarları seçin.  

    - **Kullanılabilir olduğunda ISTEMCI PKI sertifikası (istemci kimlik doğrulama yeteneği) kullan**: **https veya http** site sunucusu ayarını seçerseniz, http BAĞLANTıLARı için bir istemci PKI sertifikası kullanmak üzere bu seçeneği belirleyin. İstemci, kendi kimliğini site sistemlerine doğrulatmak için otomatik olarak imzalanan sertifika yerine bu sertifikayı kullanır. **Yalnızca https**' yi seçerseniz bu seçenek otomatik olarak seçilir.  

    İstemci üzerinde birden fazla geçerli PKI istemci sertifikası kullanılabilir olduğunda, istemci sertifikası seçme yöntemlerini yapılandırmak için **Değiştir** ' i seçin.  

    İstemci sertifikası seçme yöntemi hakkında daha fazla bilgi için bkz. [Planning for PKI client certificate selection](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - **İstemciler site sistemleri için sertifika iptal listesini (CRL) denetler**: istemcilerin, iptal edilen sertifikalar IÇIN kuruluşunuzun CRL 'sini denetlemesi için bu ayarı etkinleştirin.  

    İstemcilerin CRL kontrolü hakkında daha fazla bilgi için bkz. [Planning for PKI certificate revocation](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Güvenilen kök sertifika yetkililerinin sertifikalarını içeri aktarmak, görüntülemek ve silmek için **Ayarla**' yı seçin.  

    Daha fazla bilgi için bkz. [PKI güvenilir kök sertifikaları ve sertifika verenler listesi Için planlama](plan-for-security.md#BKMK_PlanningForRootCAs).  


Hiyerarşideki tüm birincil siteler için bu yordamı yineleyin.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a>İmzalama ve şifrelemeyi yapılandırma  

Site sistemleri için sitedeki tüm istemcilerin destekleyebileceği en güvenli imza ve şifreleme ayarlarını yapılandırın. İstemcilerin site sistemleriyle HTTP üzerinden otomatik olarak imzalanan sertifikalar kullanarak iletişim kurmalarına izin verdiğinizde bu ayarlar özellikle önemlidir.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Bir sitenin imzalama ve şifrelemesini yapılandırmak için  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Yapılandırılacak birincil siteyi seçin.  

2.  Şeritte **Özellikler**' i seçin ve ardından **imzalama ve şifreleme** sekmesine geçin.  

    Bu sekme yalnızca birincil sitede kullanılabilir. **İmzalama ve şifreleme** sekmesini görmüyorsanız bir merkezi yönetim sitesine veya ikincil siteye bağlı olduğunuzdan emin olun.  

3.  İstemcilerin siteyle iletişim kurması için imzalama ve şifreleme seçeneklerini yapılandırın.  

    - **Imzalama gerektir**: istemciler yönetim noktasına göndermeden önce verileri imzalar.  

    - **SHA-256 gerektir**: istemciler, VERILERI imzalarken sha-256 algoritmasını kullanır.  

    > [!WARNING]  
    >  Önce tüm istemcilerin bu karma algoritmayı desteklediğini onaylamadan **SHA-256 gerekmez** . Bu istemciler gelecekte siteye atanabileceği olanları içerir.  
    >   
    >  Bu seçeneği belirlerseniz ve otomatik olarak imzalanan sertifikaları olan istemciler SHA-256 ' ı destekleyeirse Configuration Manager bunları reddeder. SMS_MP_CONTROL_MANAGER bileşen 5443 ileti KIMLIĞINI günlüğe kaydeder.  

    - **Şifreleme kullan**: istemciler, yönetim noktasına göndermeden önce istemci envanteri verilerini ve durum iletilerini şifreler. Bunlar 3DES algoritmasını kullanır.  

Hiyerarşideki tüm birincil siteler için bu yordamı yineleyin.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a>Rol tabanlı yönetimi yapılandırma  

Rol tabanlı yönetim güvenlik rollerini, güvenlik kapsamlarını ve atanmış koleksiyonları birleştirerek her yönetici kullanıcının yönetim kapsamını tanımlar. Kapsam, bir kullanıcının konsolunda görüntüleyebileceği nesneleri ve bu nesnelerle ilgili izinleri olan görevleri içerir. Rol tabanlı yönetim yapılandırmaları hiyerarşideki her sitede uygulanır.  

Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../../servers/deploy/configure/configure-role-based-administration.md). Bu makalede aşağıdaki eylemlerin ayrıntıları verilmiştir:  

- Özel güvenlik rolleri oluşturma  

- Güvenlik rollerini yapılandırma  

- Nesnenin güvenlik kapsamlarını yapılandırma  

- Güvenliği yönetmek için koleksiyonları yapılandırma  

- Yeni yönetici kullanıcı oluşturma  

-  Yönetici kullanıcının yönetim kapsamını değiştirme  

> [!IMPORTANT]  
>  Kendi yönetim kapsamınız, başka bir yönetici kullanıcı için rol tabanlı yönetimi yapılandırırken atayabileceğiniz nesne ve ayarları tanımlar. Rol tabanlı yönetimi planlama hakkında bilgi için bkz. [rol tabanlı yönetimin temelleri](../../understand/fundamentals-of-role-based-administration.md).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a>Configuration Manager kullandığı hesapları yönetme  

Configuration Manager birçok farklı görev ve kullanım için Windows hesaplarını destekler. Farklı görevler için yapılandırılmış hesapları görüntülemek ve Configuration Manager her hesap için kullanılan parolayı yönetmek için aşağıdaki yordamı kullanın:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Configuration Manager tarafından kullanılan hesapları yönetmek için  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **güvenlik**' i genişletin ve ardından **hesaplar** düğümünü seçin.  

2.  Bir hesabın parolasını değiştirmek için listeden hesabı seçin. Ardından Şeritteki **Özellikler** ' i seçin.  

3.  **Windows Kullanıcı hesabı** iletişim kutusunu açmak için **Ayarla** ' yı seçin. Bu hesap için kullanılacak Configuration Manager yeni parolayı belirtin.  

    > [!NOTE]  
    >  Belirttiğiniz parolanın Active Directory bu hesabın parolasıyla eşleşmesi gerekir.  

Daha fazla bilgi için bkz. [Configuration Manager kullanılan hesaplar](../hierarchy/accounts.md).



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a>Azure Active Directory Yapılandır

Ortamınızı basitleştirmek ve bulutta etkinleştirmek için Configuration Manager Azure Active Directory (Azure AD) ile tümleştirin. Site ve istemcilerin kimlik doğrulamasını Azure AD kullanarak etkinleştirin. Daha fazla bilgi için bkz. [Azure hizmetlerini yapılandırma](../../servers/deploy/configure/azure-services-wizard.md)Içindeki **bulut yönetimi** hizmeti.



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a>SMS sağlayıcısı kimlik doğrulamasını yapılandırma

Sürüm 1810 ' den başlayarak, yöneticilerin Configuration Manager sitelere erişmesi için en düşük kimlik doğrulama düzeyini belirtebilirsiniz. Bu özellik, yöneticilerin Windows 'da gerekli düzeyiyle oturum açmasını zorlar. Daha fazla bilgi için bkz. [plan for SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Ayrıca bkz.

- [Güvenliği planlama](plan-for-security.md)  

- [Configuration Manager istemcileri için güvenlik ve Gizlilik](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Uç noktalar arasında iletişim](../hierarchy/communications-between-endpoints.md)  

- [Şifreleme denetimleri teknik başvurusu](cryptographic-controls-technical-reference.md)  

- [PKI sertifikası gereksinimleri](../network/pki-certificate-requirements.md)  
