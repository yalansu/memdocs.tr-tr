---
title: CNG sertifikalarına genel bakış
titleSuffix: Configuration Manager
description: Configuration Manager istemcileri ve sunucuları için yeni nesil şifreleme (CNG) sertifikaları desteği hakkında bilgi edinin.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4574b7ae97e8200da248a0b798677eacadb6229f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719837"
---
# <a name="cng-certificates-overview"></a>CNG sertifikalarına genel bakış
<!-- 1356191 --> 

Configuration Manager şifreleme: yeni nesil (CNG) sertifikaları için sınırlı destek içerir. Configuration Manager istemcileri, CNG Anahtar depolama sağlayıcısında (KSP) özel anahtarla PKI istemci kimlik doğrulama sertifikasını kullanabilir. KSP desteğiyle Configuration Manager istemcileri, PKI istemci kimlik doğrulama sertifikaları için TPM KSP gibi donanım tabanlı özel anahtarı destekler.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
[Şifreleme API 'si: yeni nesil (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) sertifika şablonlarını aşağıdaki senaryolar için kullanabilirsiniz:

- Bir HTTPS yönetim noktasıyla istemci kaydı ve iletişim   
- HTTPS dağıtım noktasıyla yazılım dağıtımı ve uygulama dağıtımı   
- İşletim sistemi dağıtımı  
- İstemci mesajlaşma SDK (en son güncelleştirme ile) ve ISV proxy   
- Bulut Yönetimi Ağ Geçidi yapılandırması  

Sürüm 1802 ' den başlayarak, aşağıdaki HTTPS etkin sunucu rolleri için CNG sertifikalarını kullanın: <!-- 1357314 -->   
- Yönetim noktası
- Dağıtım noktası
- Yazılım güncelleştirme noktası
- Durum Geçiş noktası     

Sürüm 1806 ' den başlayarak, aşağıdaki HTTPS etkin sunucu rolleri için CNG sertifikalarını kullanın:

- Configuration Manager ilkesi modülüyle NDES sunucusu dahil olmak üzere sertifika kayıt noktası <!--1357314-->

> [!NOTE]
> CNG, şifreleme API 'SI (CAPı) ile geriye dönük olarak uyumludur. İstemci üzerinde CNG desteği etkinken bile CAPı sertifikaları desteklenmeye devam eder.

## <a name="unsupported-scenarios"></a>Desteklenmeyen senaryolar

Şu senaryolar Şu anda desteklenmiyor:

- Aşağıdaki sunucu rolleri, HTTPS modunda yüklendiğinde, Internet Information Services Web sitesine (IIS) göre bir CNG sertifikası ile yüklendiğinde çalışır durumda değildir: 
    - Uygulama Kataloğu Web hizmeti
    - Uygulama Kataloğu web sitesi
    - Kayıt noktası  
    - Kayıt proxy noktası  

- Yazılım Merkezi, uygulama ve paketleri Kullanıcı veya Kullanıcı grubu koleksiyonlarına dağıtılan kullanılabilir olarak göstermez.

- Bir bulut dağıtım noktası oluşturmak için CNG sertifikalarını kullanma.

- NDES ilke modülü istemci kimlik doğrulaması için bir CNG sertifikası kullanıyorsa, sertifika kayıt noktasıyla iletişim başarısız olur. 
    - Bu, Configuration Manager sürüm 1806 ' den itibaren desteklenmektedir.

- Görev sırası medyası oluştururken bir CNG sertifikası belirtirseniz, sihirbaz önyüklenebilir medya oluşturamaz.
    - Bu, Configuration Manager sürüm 1806 ' den itibaren desteklenmektedir.

## <a name="to-use-cng-certificates"></a>CNG sertifikalarını kullanmak için

CNG sertifikalarını kullanmak için, sertifika yetkilinizin (CA) hedef makineler için CNG sertifika şablonları sağlaması gerekir. Şablon Ayrıntıları senaryoya göre farklılık gösterir; Ancak, aşağıdaki özellikler gereklidir:

- **Uyumluluk** sekmesi

    - **Sertifika yetkilisi** Windows Server 2008 veya sonraki bir sürümü olmalıdır. (Windows Server 2012 önerilir.)

    - **Sertifika alıcısı** Windows Vista/sunucu 2008 veya sonraki bir sürümü olmalıdır. (Windows 8/Windows Server 2012 önerilir.)

- **Şifreleme** sekmesi

    - **Sağlayıcı kategorisi** , **anahtar depolama sağlayıcısı**olmalıdır. istenir
    - **İsteğin şu sağlayıcılardan birini kullanması gerekir:** **Microsoft yazılım anahtarı depolama sağlayıcısı**olmalıdır. 

> [!NOTE]
> Ortamınız veya kuruluşunuz için gereksinimler farklı olabilir. PKI uzmanından iletişim kurun. Dikkate alınması gereken önemli nokta, bir sertifika şablonunun CNG 'den faydalanmak için anahtar depolama sağlayıcısı kullanması gerekir.

En iyi sonuçlar için, Active Directory bilgilerden konu adının oluşturulmasını öneririz. **Konu adı biçimi** Için DNS adını kullanın ve diğer konu adına DNS adını ekleyin. Aksi takdirde, cihaz sertifika profiline kaydedildiğinde bu bilgileri sağlamanız gerekir.
