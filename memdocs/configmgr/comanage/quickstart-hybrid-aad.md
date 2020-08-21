---
title: Ortak yönetim için Azure AD kullanma
titleSuffix: Configuration Manager
description: Azure AD ile, hem bulutta hem de şirket içi ortamlarda, kaynaklarınız için kullanıcılarınıza ve güvenliğine yönelik geliştirilmiş verimliliğin avantajlarından yararlanabilirsiniz.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c757632e96eb9bdaca829d4a19e5e156fcf52577
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694993"
---
# <a name="use-azure-ad-for-co-management"></a>Ortak yönetim için Azure AD kullanma

Bulutta, kimlik yeni denetim düzledir. Azure Active Directory (Azure AD), kullanıcılarınızın, cihazlarınızın ve uygulamalarınızın yanı sıra hem bulutta hem de şirket içi ortamlarda bağlantı kurmanıza olanak tanır. Cihazlarınızı Azure AD 'ye kaydetmek, kaynaklarınız için kullanıcılarınız ve güvenlik açısından üretkenliği artırmanıza olanak sağlar. Azure AD 'de cihazların olması hem ortak yönetim hem de cihaz tabanlı koşullu erişim için temelidir.

Cihaz tabanlı koşullu erişim hakkında daha fazla bilgi için bkz [. nasıl yapılır: bulut uygulaması için yönetilen cihazların koşullu erişimle erişim gerektirme](/azure/active-directory/conditional-access/require-managed-devices)

Aşağıdaki videoda, üst düzey Program Yöneticisi Sanderin deo ve ürün pazarlama yöneticisi adam Harbour tartışın ve ortak yönetim için Azure AD ile tanıtım edin:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD, şirkete ait cihazlar için kuruluşunuzun ihtiyaçlarına uygun iki seçenek sunar:  

- **Azure AD 'ye katılmış cihaz**: Windows 10 cihazlarınızı şirket içi Active Directory katılmasına gerek kalmadan Azure AD 'ye ekleyin  

  - Windows 10 ' da desteklenir

  - Şirket içi ortamlarınızda ek yapılandırma gerektirmeden ayarlayın  

  - Azure AD 'de birkaç ayarı etkinleştirerek, kullanıcılarınızın Windows kurulum deneyimi (OOBE) aracılığıyla cihazları Azure AD 'ye birleştirmesini sağlayabilirsiniz  

  - Daha fazla bilgi için bkz [. nasıl yapılır: Azure AD JOIN Uygulamanızı planlayın](/azure/active-directory/devices/azureadjoin-plan)  

- **Karma Azure AD 'ye katılmış cihaz**: mevcut etki alanına katılmış cihazlarınıza Azure AD 'ye katılma  

  - Windows 10, Windows 8.1 ve Windows 7 ' yi destekler

  - AD FS taleplerini veya Azure AD Connect kullanarak ayarlama  

  - Windows 10 için JOIN makine bağlamında gerçekleşir, bu nedenle kullanıcıların ek adımlar alması gerekmez  

  - Daha fazla bilgi için bkz. [karma Azure Active Directory JOIN uygulamanızı planlaması](/azure/active-directory/devices/hybrid-azuread-join-plan)  

Her iki seçenek de kullanıcılar için benzer işlevsellik sağlar. Gereksinimlerinize göre bunlardan birini seçmeniz esnektir. Örneğin, Active Directory katılmadıklarında bile [Şirket içi kaynaklarınıza](/azure/active-directory/devices/azuread-join-sso) Azure AD 'ye katılmış makinelerden erişebilirsiniz.

[Kimlik doğrulama yönteminiz](/azure/active-directory/hybrid/choose-ad-authn)ne olduğuna bakılmaksızın, farklı ortamlarda CIHAZLARı Azure AD 'ye ekleyebilirsiniz. Örneğin, Federasyon kimlik doğrulaması veya bulut kimlik doğrulaması.

Zaten bir şirket içi Active Directory varsa, iki seçenekten birini ayarlamak basittir.

## <a name="benefits"></a>Yararları

Cihazların Azure AD 'ye katılması, kuruluşunuza aşağıdaki avantajları sağlar:

### <a name="single-sign-on-to-cloud-resources"></a>Bulut kaynaklarında çoklu oturum açma

Azure AD 'ye katılmış cihazlarda, herhangi bir buluta veya şirket içi kaynağa erişirken tümleşik bir deneyim alırsınız. Azure AD 'ye katılmış bir Windows makinesinde oturum açtıktan sonra ek oturum açma istemleri olmadan tüm uygulamalarda çoklu oturum açma alırsınız.  

### <a name="windows-hello-for-business"></a>İş İçin Windows Hello

Iş için Windows Hello, Windows 10 ' a güçlü parola azaltır kimlik doğrulaması uygular. Cihazlarınızı Azure AD 'ye katılarak, hem bulut hem de şirket içi kaynaklar için Kullanıcı tabanınız genelinde Iş için Windows Hello 'Yu etkinleştirebilirsiniz. Iş için Windows Hello, karmaşık Parolaları hatırlama veya yanlışlıkla ortaya çıkaran sorunu ortadan kaldırır. Oturum açma işlemi hem basit hem de güvenlidir.

Daha fazla bilgi için bkz. [iş Için Windows Hello](/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Cihaz tabanlı koşullu erişim

Kuruluşunuzun verilerini daha iyi korumak için cihaz durumuna göre koşullu erişimi etkinleştirin. Cihaz tabanlı koşullu erişim yönetilen bir cihaz gerektirir. Bu cihaz uyumlu bir cihaz ya da karma Azure AD 'ye katılmış bir cihaz olmalıdır. Azure AD 'ye katılmış cihazlar için Intune 'un cihazı uyumlu olarak işaretlemesi gerekir. Ancak, karma Azure AD 'ye katılmış cihazlar için, koşullu erişimi değerlendirmek üzere cihaz durumunun kendisi kullanılır. Ortak yönetim, karma Azure AD 'ye katılmış cihazlar için Intune aracılığıyla uyumluluğu değerlendirmeden daha fazla avantaj sağlar. Bu özellik cihaz yapılandırmasının bozulmadan emin olmanızı sağlar.

Cihaz tabanlı koşullu erişim hakkında daha fazla bilgi için bkz. [nasıl yapılır: bulut uygulaması için yönetilen cihazların koşullu erişimle erişimine ihtiyacı](/azure/active-directory/conditional-access/require-managed-devices).  

### <a name="automatic-device-licensing"></a>Otomatik cihaz lisanslama

Azure AD 'ye katılmış tüm Windows 10 cihazları lisans denetimleri aracılığıyla gider. Bu denetimler, Microsoft bulutu aracılığıyla bunları Pro 'dan kuruluşa otomatik olarak yükseltmenize olanak tanır. İlgili aboneliği kullanıcıdan kaldırdığınızda, cihaz lisansını otomatik olarak eski sürüme düşürüdir. Bu özellik, karmaşık süreçler veya şirket içi sistemler olmadan Windows lisanslarını yönetmek için tek bir denetim bölmesi sağlar.

### <a name="self-service-functionality"></a>Self Servis işlevselliği

Self Servis işlevselliği, self servis parola sıfırlama ve BitLocker kurtarma anahtarını içerir. Azure AD Ayrıca parolanızı sıfırlamanıza veya BitLocker Kurtarma anahtarlarına erişmenize yönelik doğrudan seçenekler sağlar. Azure AD 'yi kullanarak parolanızı bir Web tarayıcısı yerine doğrudan Windows kilit ekranından sıfırlayabilirsiniz. Bu özellikler, kullanıcılar için uçuşmayı azaltır ve kuruluşunuzun yardım masası maliyetlerini kesmeye yardımcı olur.  

Daha fazla bilgi için bkz. [öğretici: kullanıcıların hesaplarının kilidini açma veya Azure Active Directory self servis parola sıfırlama kullanarak parola sıfırlama](/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Kurumsal durum dolaşımı

Azure AD 'ye katılmış tüm cihazlar, ayarlarını bulutla eşitlenebilir. Kullanıcının oturum açtığı herhangi bir cihaz, daha üretken bir deneyim için tüm ayarlarını eşitler.  

## <a name="value-proposition"></a>Değer teklifi

Her iki yöntem aracılığıyla cihazlarınızın Azure AD 'ye katılması dijital dönüşümünüzü hızlandırır. Microsoft 365 tarafından sunulan daha fazla işlevselliğe izin verebilir. Daha iyi deneyimleriniz olacak ve verileriniz için daha fazla güvenliğe sahip olacaksınız.

Azure AD, iş yüklerinizi kolaylaştırmak için çeşitli seçenekler sağlar, örneğin:

- Kuruluşunuzdaki tüm cihaz kimliklerini tek bir yerden yönetin  

- Self servis parola sıfırlamayı etkinleştirerek, yardım masası maliyetlerinizi düşürün. Daha sonra kullanıcılar, dilediğiniz zaman cihazınızda Windows 10 kilit ekranından parolanızı sıfırlayabilir.  

## <a name="configure"></a>Yapılandırma

Zaten bir şirket içi Active Directory ortamınız varsa ve etki alanına katılmış cihazlarınızı Azure AD 'ye katmak istiyorsanız, karma Azure AD 'ye katılmış cihazları yapılandırın. Daha fazla bilgi için [nasıl yapılır: karma Azure Active Directory JOIN Uygulamanızı planlayın](/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager, [Yeni Windows 10 etki alanına katılmış cihazları Azure AD 'ye otomatik olarak kaydetmek](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory)için bir istemci ayarına sahiptir. İstemci ayarlarını yapılandırma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../core/clients/deploy/configure-client-settings.md).

Cihazlarınız için Azure AD 'ye katılma 'yı şirket içi etki alanınıza katmadan yapılandırmak istiyorsanız, ortamınızda Azure AD 'ye katılma konularını gözden geçirin. Azure AD JOIN ile çalışmaya karar verdikten sonra kuruluşunuzun ihtiyaçlarına bağlı olarak bu uygulamayı dağıtmak için birçok seçeneğiniz vardır. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Nasıl yapılır: Azure AD JOIN Uygulamanızı planlayın](/azure/active-directory/devices/azureadjoin-plan)  
- [Sağlama seçeneklerinizi anlayın](/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)