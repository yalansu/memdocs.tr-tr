---
title: Hibrit Azure AD’yi ayarlama
titleSuffix: Configuration Manager
description: Ortamınızda Şu anda etki alanına katılmış Windows 10 cihazları varsa, ortak yönetimi etkinleştirmeden önce karma Azure AD 'yi ayarlayın
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e2f7bbb51c72fa3d0f2a36e8a5419552d468b4c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711479"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Ortak yönetim için karma Azure AD ayarlama

Şirket içi Active Directory katılmış Windows 10 cihazlarınız varsa, Configuration Manager ortak yönetimi 'ni etkinleştirmeden önce, önce bu cihazları Azure Active Directory (Azure AD) 'e katın. Bu işleme karma Azure AD katılımı adı verilir. 

Aşağıdaki videoda, üst düzey Program Yöneticisi Sanderin deo ve ürün pazarlama yöneticisi adam Harbour, Azure AD 'de cihazları yapılandırma:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Hibrit Azure AD-katılım işlemi, şirket içi etki alanına katılmış cihazlarınızı Azure AD 'ye otomatik olarak kaydeder. Bu işlemle ilgili daha fazla bilgi için aşağıdaki makalelere bakın:
- [Azure Active Directory'de cihaz yönetimine giriş](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Hibrit Azure AD katılırsanız nasıl planlanacağı](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Hibrit Azure AD katılımı, ortak yönetim için temel temellerinden biridir. Bu işlem bazı müşteriler için zor olabilir, örneğin:
- Kuruluşunuz bir üçüncü taraf kimlik çözümü kullanıyor 
- Active Directory Federasyon Hizmetleri (AD FS) ayarlamanın karmaşıklıkları (ADFS)

Bu güçlüklerin çözümlenmesi bazı kılavuzlardan yararlanabilir. Bu makale, tüm gecikmeleri azaltmaya yardımcı olur.


## <a name="how-to-do-it"></a>Nasıl yapılır?

Korumak istediğiniz bir kimlik oluşturulurken cihazlar kullanıcılara benzerdir. Bir cihazın kimliğini dilediğiniz zaman ve herhangi bir konumda korumak için, bu cihazın kimliğini Azure AD 'ye taşımanız gerekir.

Kullanmakta olduğunuz etki alanı türüne göre, bunu gerçekleştirmenin iki temel yolu vardır. Aşağıdaki etki alanı türlerinden biri için karma Azure AD JOIN 'i yapılandırın:  
- [Federasyon etki alanları](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Yönetilen etki alanları](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Yukarıdaki iki yöntem en iyi deneyimi sağlar. Tam el ile gerçekleştirilen işlem dahil daha ayrıntılı bilgi için aşağıdaki makalelere bakın:
- [Karma Azure AD 'ye katılmış cihazları el ile yapılandırma](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- Azure AD bulmayı içeren [karma Azure AD Için ADFS geçişli geçişli kimlik doğrulaması](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview)  

Sorun giderme kılavuzu için bkz. [Windows 10 karma Azure AD 'ye ekleme sorun giderme kılavuzu](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Örnek olay incelemesi

100.000 ' den fazla kullanıcısı olan büyük Avrupa yazılım şirketi, karma Azure AD JOIN 'i etkinleştirmeye yönelik ayrıntılı ve aşamalı bir yaklaşım gerçekleştirdi.

Planlama aşamasında, karma Azure AD katılımı ortak Yönetimi destekleyen bir anahtar öğe olduğundan, Configuration Manager yöneticileri kimlik ekibi ile birlikte çalışmıştır. Bu yazılım şirketi birçok ADFS kuralına sahipti ve bunlardan bazıları karmaşıktı. Bu sorunu gidermek için kimlik ekibi, karma Azure AD JOIN 'i etkinleştirilmeden önce var olan ADFS kurallarını incelendi. BT ekibi Azure AD Connect en son sürüme yükseltmeyi de tercih edebilirsiniz. Azure AD Connect artık karma Azure AD JOIN 'i etkinleştirmek için otomatik bir işlem akışı sağlar.

Üretim öncesi ortamında başarılı dağıtım ve test sonrasında, bu müşteri tüm üretim için hibrit Azure AD katılımı 'nı etkinleştirdi. Bir hafta içinde, her Windows 10 cihazının birlikte yönetilmesine sahip olurlar.



## <a name="contact-fasttrack"></a>FastTrack 'e başvurun

İşlemin herhangi bir noktasında Azure AD 'yi ayarlamak için yardıma ihtiyacınız varsa [Microsoft FastTrack](https://Microsoft.com/FastTrack/)' a gidin, oturum açın ve yardım isteyin. 

Daha fazla bilgi için bkz. [FastTrack 'ten yardım alın](quickstart-fasttrack.md). 

