---
title: S/MIME-Microsoft Intune-Azure kullanarak e-posta imzalama ve şifreleme | Microsoft Docs
description: Cihazlarda e-postaları imzalamak ve şifrelemek için Microsoft Intune 'da e-posta dijital sertifikalarını nasıl kullanacağınızı öğrenin. Bu sertifikalara S/MIME denir ve cihaz yapılandırma profilleri kullanılarak yapılandırılır. İmzalama ve şifreleme sertifikaları PKCS veya özel sertifikalar kullanır ve sertifikaları içeri aktarmak için bir bağlayıcı kullanır.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 863fdd219e9d75ca61322c4eb976c2cdedfd4101
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813984"
---
# <a name="smime-overview-to-sign-and-encrypt-email-in-intune"></a>Intune 'da e-posta imzalama ve şifreleme için S/MIME 'ye Genel Bakış

S/MIME sertifikası olarak da bilinen e-posta sertifikaları, şifreleme ve şifre çözme kullanarak e-posta iletişimlerinizi ek güvenlik sağlar. Microsoft Intune, aşağıdaki platformları çalıştıran mobil cihazlarda e-postaları imzalamak ve şifrelemek için S/MIME sertifikaları kullanabilir:

- Android
- iOS/iPadOS
- macOS
- Windows 10 ve üzeri

Intune, tüm platformlara otomatik olarak S/MIME şifreleme sertifikaları sunabilir. S/MIME sertifikaları, iOS üzerinde yerel posta istemcisini ve iOS ve Android cihazlarda Outlook 'U kullanan posta profilleriyle otomatik olarak ilişkilendirilir. Windows ve macOS platformları için ve iOS ve Android 'deki diğer posta istemcileri için, Intune sertifikaları teslim eder, ancak kullanıcıların posta uygulamasında S/MIME 'yi el ile etkinleştirmeleri ve S/MIME sertifikalarını seçmesi gerekir.

S/MIME e-posta imzalama ve Exchange ile şifreleme hakkında daha fazla bilgi için bkz. [s/MIME, ileti imzalama ve şifreleme için](/Exchange/policy-and-compliance/smime).

Bu makalede, cihazlarınızdaki e-postaları imzalamak ve şifrelemek için S/MIME sertifikaları kullanma hakkında genel bakış sunulmaktadır.

## <a name="signing-certificates"></a>İmzalama sertifikaları

İmzalama için kullanılan sertifikalar, istemci e-posta uygulamasının e-posta sunucusuyla güvenli bir iletişim kurmasını sağlar.

İmzalama sertifikalarını kullanmak için, sertifika yetkiliniz (CA) üzerinde imzalamaya odaklanan bir şablon oluşturun. Microsoft Active Directory Sertifika Yetkilisinde [Sunucu sertifikası şablonu yapılandırma](/windows-server/networking/core-network-guide/cncg/server-certs/configure-the-server-certificate-template) başlığı altında sertifika şablonları oluşturmak için gerekli adımlar listelenir.

Intune’da imzalama sertifikaları PKCS sertifikalarını kullanır. [PKCS sertifikaları yapılandırma ve kullanma](certficates-pfx-configure.md) başlığı altında, Intune ortamınızda nasıl PKCS sertifikası dağıtıp kullanacağınız açıklanır. Bu adımlar şunlardır:

- PKCS sertifika isteklerini desteklemek için PFX Sertifika bağlayıcısını indirip yükleyin. Bağlayıcı, [yönetilen cihazlarla](../fundamentals/intune-endpoints.md#access-for-managed-devices)aynı ağ gereksinimlerine sahiptir.
  > [!IMPORTANT]
  > PFX Sertifika Bağlayıcısı sürüm 6.2008.60.607 (Ağustos 2020 ' de yayımlanmıştır) ile başlayarak, bu bağlayıcı, sertifika istekleri #12 PCKS sertifika dağıtımını destekler ve belirli bir kullanıcı için S/MIME e-posta şifrelemesi için Intune 'a aktarılan PFX dosyaları için istekleri işler. PKCS sertifika profillerini kullanırken Microsoft Intune bağlayıcısını kullanmanız artık gerekmez.
  > 
  > Daha fazla bilgi için bkz. [sertifika bağlayıcıları](certificate-connectors.md)
- Cihazlarınız için bir güvenilen kök sertifika profili oluşturma. Bu adım, sertifika yetkiliniz için güvenilen kökü ve ara sertifikaları kullanma ve ardından profili cihazlara dağıtma işlemlerini içerir.
- Oluşturduğunuz sertifika şablonunu kullanarak PKCS sertifika profili oluşturma. Bu profil imzalama sertifikalarını cihazlara verir ve PKCS sertifika profilini cihazlara dağıtır.

Ayrıca, belirli bir kullanıcı için de imzalama sertifikası içeri aktarabilirsiniz. İmzalama sertifikası, kullanıcının kaydettiği tüm cihazlarda dağıtılır. Intune’a sertifika aktarmak için [GitHub’daki PowerShell cmdlet'lerini](https://github.com/Microsoft/Intune-Resource-Access) kullanın. E-posta imzalama amacıyla kullanılmak üzere Intune’da içeri aktarılan bir PKCS sertifikasını dağıtmak için [Intune ile PKCS sertifikalarını yapılandırma ve kullanma](certficates-pfx-configure.md) bölümündeki adımları izleyin. Bu adımlar şunlardır:

- Microsoft Intune için PFX Sertifika Bağlayıcısı'nı indirin ve yükleyin. Bu bağlayıcı, içeri aktarılan PKCS sertifikalarını cihazlara verir.
- S/MIME e-posta imzalama sertifikalarını Intune’a aktarın.
- PKCS içeri aktarılan sertifika profili oluşturun. Bu profil, içeri aktarılan PKCS sertifikalarını uygun kullanıcının cihazlarına verir.

## <a name="encryption-certificates"></a>Şifreleme sertifikaları

Şifreleme için kullanılan sertifikalar, şifrelenmiş bir e-postanın şifresinin yalnızca hedeflenen alıcı tarafından çözülebilmesini sağlar. S/MIME şifrelemesi, e-posta iletişiminizde kullanabileceğiniz yeni bir güvenlik katmanıdır.

Başka bir kullanıcıya şifrelenmiş bir e-posta gönderirken o kullanıcının şifreleme sertifikasının ortak anahtarı alınır ve gönderdiğiniz e-postayı şifreler. Alıcı, cihazındaki özel anahtarı kullanarak e-postanın şifresini çözer. Kullanıcılarda e-posta şifreleme için kullanılan sertifikaların geçmişi bulunabilir. E-posta şifrelerinin başarıyla çözülmesi için bu sertifikaların her birinin belirli bir kullanıcının tüm cihazlarına dağıtılması gerekir.

E-posta şifreleme sertifikalarının Intune’da oluşturulmaması önerilir. Intune, şifreleme destekli PKCS sertifikası vermeyi desteklese de cihaz başına benzersiz bir sertifika oluşturur. Cihaz başına benzersiz bir sertifika, şifreleme sertifikasının kullanıcının tüm cihazları arasında paylaşıldığı bir S/MIME şifreleme senaryosu için ideal bir yöntem değildir.

S/MIME sertifikalarını Intune kullanarak dağıtmak için kullanıcının şifreleme sertifikalarının tümünü Intune’a aktarmalısınız. Ardından Intune, bu sertifikaların tümünü kullanıcının kaydettiği her cihaza dağıtır. Intune’a sertifika aktarmak için [GitHub’daki PowerShell cmdlet'lerini](https://github.com/Microsoft/Intune-Resource-Access) kullanın.

E-posta şifreleme amacıyla kullanılan, Intune’a aktarılmış bir PKCS sertifikasını dağıtmak için [Intune ile PKCS sertifikalarını yapılandırma ve kullanma](certficates-pfx-configure.md) bölümündeki adımları izleyin. Bu adımlar şunlardır:

- Microsoft Intune için PFX Sertifika Bağlayıcısı'nı indirin ve yükleyin. Bu bağlayıcı, içeri aktarılan PKCS sertifikalarını cihazlara verir.
- S/MIME e-posta şifreleme sertifikalarını Intune’a aktarın.
- PKCS içeri aktarılan sertifika profili oluşturun. Bu profil, içeri aktarılan PKCS sertifikalarını uygun kullanıcının cihazlarına verir.

 > [!NOTE]
 > İçeri aktarılan S/MIME şifreleme sertifikaları, şirket verileri kaldırıldığında veya kullanıcıların yönetim kaydı silindiğinde Intune’dan kaldırılır. Ancak sertifikalar sertifika yetkilisinde iptal edilmez.

## <a name="smime-email-profiles"></a>S/MIME e-posta profilleri

S/MIME imzalama ve şifreleme sertifikası profilleri oluşturduktan sonra, [iOS/ıpados yerel postası Için s/MIME 'yi etkinleştirebilirsiniz](../configuration/email-settings-ios.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Sertifikalar için SCEP kullanma](certificates-scep-configure.md)
- [PKCS sertifikalarını kullanma](certficates-pfx-configure.md)
- [İş ortağı CA 'sını kullanma](certificate-authority-add-scep-overview.md)
- [Symantec PKI Manager Web hizmetinden PKCS sertifikaları verme](certificates-digicert-configure.md)