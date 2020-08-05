---
title: Ortak yönetim ile Windows Autopilot
titleSuffix: Configuration Manager
description: Yeni Windows 10 cihazlarının kurulumunu basitleştirmek için Configuration Manager 'de ortak yönetimi ile Windows Autopilot kullanın.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f77cb76e3cfd9c932a6f3789f98e5616cdaa27eb
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546442"
---
# <a name="windows-autopilot-with-co-management"></a>Ortak yönetim ile Windows Autopilot

Yeni bir Windows 10 cihazının alınması heyecan verici. Ancak, üretken olmak için tüm ayarlarınızı ve uygulamalarınızı yapılandırmak zaman alabilir. Ortak yönetim, Windows Autopilot ile bu cihaz sağlama sorununu çözer.

Autopilot aşağıdaki durumlarda hem siz hem de kullanıcılarınız için basitleştirilmiş bir deneyim sağlar:
- Yeni Windows 10 cihazlarını ayarlama ve önceden yapılandırma  
- Mevcut cihazları sıfırlayın, geri dönüştürün ve kurtarın  

Autopilot cihazları dağıtma, yönetme ve devre dışı bırakma ile ilişkili zamanı, kaynakları ve karmaşıklığı azaltır. Aynı zamanda, kullanıcılarınız için deneyim kolay ve ilk önyüklemeden kolaydır.

Windows Autopilot, hepsi ortak yönetim ile büyütülmüş olan çeşitli senaryoları destekler:

- Kullanıcılar, karma Azure AD JOIN veya Azure Active Directory (Azure AD) ile yeni cihazların kendi dağıtımlarını Active Directory.  

- Paylaşılan cihazlar ve bilgi noktaları için Azure AD 'de yeni cihaz dağıtımlarını kendi kendine dağıtma ayarı yapabilirsiniz  

- Mevcut cihazlarda Windows Autopilot ile, mevcut bir cihazı Windows 7 ' den ve Active Directory Windows 10 ve Azure AD 'ye geçirmek için Configuration Manager kullanın  

Aşağıdaki videoda, üst düzey Program Yöneticisi Danny Gullory ve Principal program Manager Andrew McMurray tartışın ve tanıtım Windows Autopilot with Co-Management:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Yararları

Ortak yönetimi ve Autopilot birlikte kullandığınızda, ağınızı girerken yeni cihazların aynı yönetim durumunda olduğundan emin olun. Bu kurulumda, cihazlar Intune 'A kaydedilir ve bir Configuration Manager istemcisine sahiptir.  Yeni Windows 10 sağlama modelini kullanmanızı sağlar ve özel işletim sistemi görüntülerini oluşturma, bakımını yapma ve güncelleştirme ihtiyacını ortadan kaldırmanıza yardımcı olur. 

Bu senaryoların tümünde, Intune ile [ortak yönetimi](how-to-prepare-Win10.md) otomatik olarak etkinleştirebilirsiniz. Bu Otomasyon, sağlama işlemine ve cihazın devam eden yönetimine yardımcı olur.

Autopilot ile görüntüler ve sürücüler hakkında endişelenmeniz gerekmez. Intune 'U kullanarak ve ortak yönetim aracılığıyla Configuration Manager Bu otomatik süreç tarafından cihazları sağlamaya odaklanın.


Ortak yönetim ve Autopilot birlikte kullanarak şu anda yardımcı olabilir:

#### <a name="reduce-time-costs-and-complexity"></a>Süreyi, maliyetleri ve karmaşıklığı azaltma
Windows Autopilot, cihaza önceden yüklenmiş Windows 10 ' un OEM ile iyileştirilmiş sürümünü kullanır. Bu yapılandırma, kuruluşların kullanımda olan her cihaz modeli için özel görüntü ve sürücü tutma çabalarının bakımını sağlar. Cihazı yeniden Imaging yerine, var olan Windows 10 yüklemesini "iş için Ready" durumuna dönüştürün. Ayarları ve ilkeleri uygular, uygulama yüklenir ve Windows 10 sürümünü değiştirir. Örneğin, gelişmiş özellikleri destekleyebilmeniz için Windows 10 Pro 'dan Windows 10 Enterprise 'a yükseltme.

#### <a name="improve-the-user-experience"></a>Kullanıcı deneyimini geliştirme
En iyi kullanıcı deneyimi en az kesintiye neden olur ve bunların çalışmasına odaklanmasına yardımcı olur. Windows Autopilot, kullanıcılarınızın birkaç basit tıklamayla ve Azure AD kimlik bilgileriyle hızlı bir şekilde ayarlamaya yardımcı olacak basit bir yaklaşım sunar. Büyük bir uzak çalışanlar alanı olan birçok kuruluş için Windows Autopilot kullanarak yeni cihazları doğrudan üreticiden sunun.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Mevcut Windows 7 cihazlarını Windows 10 ' a geçirmek için Autopilot ve Configuration Manager kullanma
Mevcut cihazlarda Windows Autopilot ile bir yapılandırma dosyası oluşturup Configuration Manager bir görev dizisiyle dağıtırsınız. Bu işlem, mevcut cihazları Windows 7 ' den Windows 10 ' a kolayca geçirir. Configuration Manager bir imza Windows 10 görüntüsü kullanır ve ardından bunu Autopilot yapılandırmasına sahip mevcut Windows 7 cihazına uygularsınız. Kullanıcı cihazı başlattığında, Autopilot Kullanıcı odaklı ekleme işlemini kullanırlar.

Mevcut cihazlarda Autopilot için adımlar aşağıda verilmiştir:

![Mevcut cihazlarda Windows Autopilot için işleme genel bakış](media/autopilot-for-existing-devices.png)

1. Bilinen klasörleri OneDrive 'a yönlendirmek için Grup İlkesi dağıtma
2. Autopilot yapılandırma dosyası oluştur
3. Windows 10 ' a yükseltmek için görev sırası dağıtma
4. Windows 10 makinesi ilk önyüklemede Autopilot üzerinden gider

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Tüm çalışan türleri için cihaz sağlamayı modernleştiriliyor
Autopilot ile, artık kendi kendine Dağıtım modunu kullanarak cihazlara veya paylaşılan cihazlara sorunsuz bir işletim sistemi dağıtımı sağlayabilirsiniz. Bu kurulum, tüm farklı çalışan tiplerinizin ihtiyaçlarını karşılar. Ayrıca, Windows Autopilot Reset işlevi, bir cihazın yeni bir kullanıcıya yeniden sağlanması basit ve kolay hale geldiğinden emin olur. Bu işlem, mevsimleriniz veya sözleşme çalışanları olduğunda geleneksel olarak ne kadar zor bir görev olduğunu basitleştirir. 



## <a name="case-study"></a>Örnek olay incelemesi

Almanya lojistik ve Kııl nakliye şirketi DB Schenker, çalışan üretkenliğini artırmak ve BT ekiplerinin günlük destek görevlerinde çalışmasını sağlamak için Autopilot kullanır. DB Schenker geleneksel görüntü merkezinden uzağa taşındı ve bulut aracılığıyla sağlama ile değiştirildi. Artık yeni cihazları hızla çalışır duruma getirmek için Azure AD-JOIN ve Intune 'U kullanır. 

Kendi uzak çalışanları, BT Hizmetleri ile bir konuma seyahat etmek yerine, DB Schenker artık Windows Autopilot kullanmaktadır. Çalışanların donanımını doğrudan üreticiden yerel alan ofisine sevk ederler. Çalışan, yeni cihazı internet 'e bağlar ve Azure AD kimlik bilgileriyle oturum açtıklarında. Daha sonra cihaz, DB Schenker 'ın BT departmanı kullanıcının bireysel profiline atadığı uygulamalara ve hizmetlere bağlanır.

Daha fazla bilgi için bkz. [küresel lojistik firması merkezileştirme, modern dijital çalışma alanıyla çalışanları tek tek](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Değer teklifi

Kullanıcılarınız için daha iyi bir kullanıcı deneyimi oluşturarak kuruluşunuzda memnuniyet oluşturun. Maliyetleri düşürmek için Windows Autopilot kullanın. Kuruluşunuz için daha fazla değer ve etki sağlamak üzere diğer projelere odaklanmak için zaman boşaltın.



## <a name="configure"></a>Yapılandırma

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

[Intune kullanarak Windows Autopilot profilleri oluşturma](https://docs.microsoft.com/intune/enrollment-autopilot)

[Mevcut cihazlar için Windows Autopilot](../../autopilot/existing-devices.md)
