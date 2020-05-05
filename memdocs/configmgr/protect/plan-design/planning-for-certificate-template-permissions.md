---
title: Sertifika şablonu izinlerini planlama
titleSuffix: Configuration Manager
description: Configuration Manager tarafından kullanılan sertifika şablonlarını yapılandırmak için ihtiyaç duyduğunuz izinleri planlama hakkında bilgi edinin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 91434b70ca514430ab4cfd6815186bc6d6bc33db
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210137"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Configuration Manager sertifika profilleri için sertifika şablonu izinlerini planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Aşağıdaki bilgiler, sertifika profillerini dağıtırken Configuration Manager tarafından kullanılan sertifika şablonları için izinleri nasıl yapılandıracağınızı planlamanızı sağlamanıza yardımcı olabilir.  

## <a name="default-security-permissions-and-considerations"></a>Varsayılan Güvenlik İzinleri ve Durumlar  
 Configuration Manager sertifika şablonları için gerekli olan varsayılan güvenlik izinleri, kullanıcılar ve cihazlar için sertifika istemek üzere kullanacağı aşağıdaki gibidir:  

- Ağ Cihazı Kayıt Hizmeti uygulama havuzunun kullandığı hesabı Oku ve Kaydol  

- Configuration Manager konsolunu çalıştıran hesap için oku  

  Bu güvenlik izinleri hakkında daha fazla bilgi için bkz. [sertifika altyapısını yapılandırma](../deploy-use/certificate-infrastructure.md).  

  Bu varsayılan yapılandırmayı kullandığınızda kullanıcılar ve cihazlar sertifika şablonlarından doğrudan sertifika isteyemez ve tüm isteklerin Ağ Cihazı Kayıt Hizmeti tarafından başlatılması gerekir. Bu durum, sertifika Konusu için bu sertifika şablonlarının **İstekte Sağla** ile yapılandırılması gerektiğinden önemli bir kısıtlamadır, bu ise, dolandırıcı bir kullanıcı veya güvenliği ihlal edilmiş bir cihaz sertifika istediğinde kişiselleştirme riski olduğu anlamına gelir. Varsayılan yapılandırmada Ağ Cihazı Kayıt Hizmeti, böyle bir istek başlatmalıdır. Ancak, Ağ Cihazı Kayıt Hizmeti'ni çalıştıran hizmetin güvenliği ihlal edilirse kişiselleştirme riski devam eder. Bu riskten kaçınmak için Ağ Cihazı Kayıt Hizmeti ve bu rol hizmetini çalıştıran bilgisayar için tüm en iyi güvenlik yöntemlerini takip edin.  

  Varsayılan güvenlik izinleri iş gereksinimlerinizi yerine getirmiyorsa sertifika şablonlarındaki güvenlik izinlerini yapılandırmak için başka bir seçeneğiniz daha vardır: Kullanıcılar ve bilgisayarlar için Oku ve Kaydol izinlerini ekleyebilirsiniz.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Kullanıcılar ve Bilgisayarlar için Oku ve Kaydol İzinlerini Ekleme  
 Kullanıcılar ve bilgisayarlar için okuma ve kaydetme izinlerini eklemek, sertifika yetkilisi (CA) altyapı takımınızı ayrı bir takım yönettiğinden ve bu ayrı ekibin, kullanıcıların bir kullanıcı sertifikası istemek için bir sertifika profili göndermeden önce geçerli bir Active Directory Domain Services hesabına sahip olduğunu doğrulamak Configuration Manager uygun olabilir. Bu yapılandırma için kullanıcıları içeren bir veya daha fazla güvenlik grubu belirtmeniz ve daha sonra bu gruplara sertifika şablonlarında Oku ve Kaydol izinlerini sağlamanız gerekir. Bu senaryoda güvenlik denetimini CA yöneticisi yönetir.  

 Benzer şekilde, bilgisayar hesaplarını içeren bir veya daha fazla güvenlik grubu belirtebilirsiniz ve daha sonra bu gruplara sertifika şablonlarında Oku ve Kaydol izinlerini sağlayabilirsiniz. Etki alanı üyesi olan bir bilgisayara bilgisayar sertifika profili dağıtırsanız o bilgisayarın bilgisayar hesabına Oku ve Kaydol izinleri sağlanmalıdır. Bilgisayar bir etki alanı üyesi değilse, bu izinler gerekli değildir. Örneğin, bir çalışma grubu bilgisayarı veya kişisel mobil cihazdır.  

 Ek güvenlik denetim kullanmasına rağmen bu yapılandırmayı en iyi yöntem olarak önermiyoruz. Bunun nedeni, cihazların belirtilen kullanıcılarının veya sahiplerinin Configuration Manager bağımsız olarak sertifika isteyebilme ve başka bir kullanıcının veya cihazın kimliğine bürünmek için kullanılabilecek sertifika konusunun değerlerini sağlayabilme nedenidir.  

 Ayrıca, sertifika isteği gerçekleştiği anda kimlik doğrulaması yapılamayan hesaplar belirtirseniz sertifika isteği varsayılan olarak başarısız olur. Örneğin, Ağ Cihazı Kayıt Hizmeti'ni çalıştıran sunucu, sertifika kayıt noktası site sistem sunucusunu içeren orman tarafından güvenilmeyen bir Active Directory ormanında ise sertifika isteği başarısız olur. Etki alanı denetleyicisinden yanıt alınamadığı için bir hesabın kimlik doğrulaması yapılamıyorsa devam etmek için sertifika kayıt noktasını yapılandırabilirsiniz. Ancak, bu durum bir en iyi güvenlik yöntemi değildir.  

 Sertifika kayıt noktasının hesap izinlerini denetlemek üzere yapılandırıldığı, kullanılabilir bir etki alanı denetleyicisinin olduğu ve kimlik doğrulama isteğini reddettiği durumlarda (örneğin, hesap kilitli veya silinmiş) sertifika kayıt isteğinin başarısız olacağını unutmayın.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Kullanıcıların ve etki alanı üyesi bilgisayarların Oku ve Kaydol izinlerini denetlemek için  

1.  Sertifika kayıt noktasını barındıran site sistem sunucusunda aşağıdaki DWORD kayıt defteri anahtarını 0 değerine sahip olacak şekilde oluşturun: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Etki alanı denetleyicisinden yanıt alınamadığı için bir hesabın kimlik doğrulamasının yapılamazsa ve izin denetimini atlamak isterseniz:  

    -   Sertifika kayıt noktasını barındıran site sistem sunucusunda aşağıdaki DWORD kayıt defteri anahtarını 1 değerine sahip olacak şekilde oluşturun: HKEY_LOCAL_MACHINE \Software\microsoft\sccm\crp\skiptemplatecheckonlyifaccountaccessreddedildi  

3.  Kullanıcılara veya cihaz hesaplarına Oku ve Kaydol izinlerini sağlamak için özelliklerdeki **Güvenlik** sekmesinde bulunan sertifika veren CA'da sertifika şablonu için bir veya daha fazla güvenlik grubu ekleyin.  
