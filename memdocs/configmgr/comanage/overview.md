---
title: Windows 10 cihazları için ortak yönetim
titleSuffix: Configuration Manager
description: Configuration Manager ve Microsoft Intune kullanarak Windows 10 cihazlarını eşzamanlı olarak yönetmeyi öğrenin.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/24/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 86bd566e9582c7dd7c83f93c22430edcc8ea0d0d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347194"
---
# <a name="what-is-co-management"></a>Ortak yönetim nedir?

<!-- 1350871 -->
Ortak yönetim, mevcut Configuration Manager dağıtımınızı Microsoft 365 buluta eklemenin birincil yöntemlerinden biridir. Koşullu erişim gibi bulut destekli ek yeteneklerin kilidini açmanıza yardımcı olur.

Ortak yönetim, Configuration Manager’ı ve Microsoft Intune’u kullanarak Windows 10 cihazlarını eş zamanlı olarak yönetmenizi sağlar. Yeni işlevler ekleyerek mevcut yatırımlarınızı bulutta Configuration Manager. Ortak yönetimi kullanarak, kuruluşunuz için en iyi şekilde çalışan teknoloji çözümünü kullanma esnekliği vardır.

Bir Windows 10 cihazının Configuration Manager istemcisi olduğunda ve Intune 'a kaydolduğu zaman, her iki hizmetin de avantajlarına sahip olursunuz. Varsa, yetkiyi Configuration Manager olan iş yüklerini Intune 'a geçirebilirsiniz. Configuration Manager, Intune 'a geçiş gerçekleştirmeyen iş yükleri ve ortak yönetimin desteklemediği diğer tüm Configuration Manager özellikleri de dahil tüm diğer iş yüklerini yönetmeye devam eder.

Ayrıca, ayrı bir cihaz koleksiyonuyla iş yüküne de başladıysanız. Piloting, daha büyük bir gruba geçmeden önce Intune işlevselliğini cihazların bir alt kümesiyle test etmenize olanak tanır.

![Ortak yönetim genel bakış Diyagramı](media/co-management-overview.svg)

[Diyagramı tam boyutta görüntüleme](media/co-management-overview.svg)

> [!Note]  
> Windows 10 cihazlarını aynı anda hem Configuration Manager hem de Microsoft Intune ile yönettiğinizde, bu yapılandırmaya *ortak yönetim*denir. Configuration Manager olan cihazları yönetirken ve bir üçüncü taraf MDM hizmetine kaydettiğinizde, bu yapılandırmaya birlikte *bulunma*denir. İkisi arasında düzgün şekilde yönetilemeyeceği tek bir cihaz için iki yönetim yetkilisinin olması zor olabilir. Ortak yönetim sayesinde, Configuration Manager ve Intune, çakışma olmadığından emin olmak için [iş yüklerini](#workloads) dengeleyin. Bu etkileşim, üçüncü taraf hizmetlerde mevcut olmadığından, birlikte bulunma yönetim özellikleri ile ilgili sınırlamalar vardır. Daha fazla bilgi için bkz. [Configuration Manager Ile üçüncü taraf MDM birlikte bulunma](coexistence.md).

## <a name="paths-to-co-management"></a>Ortak yönetim yolları

Ortak yönetime ulaşmak için iki ana yol vardır:  

- **Mevcut Configuration Manager istemcileri**: zaten Configuration Manager Istemci olan Windows 10 cihazlardır. Hibrit Azure AD 'yi ayarlayın ve bunları Intune 'a kaydedin.  

- **Yeni internet tabanlı cihazlar**: Azure AD 'ye katılarak ve Intune 'a otomatik olarak kaydeden yeni Windows 10 cihazlarınız vardır. Ortak yönetim durumuna ulaşmak için Configuration Manager istemcisini yüklersiniz.  

Yollar hakkında daha fazla bilgi için bkz. [ortak yönetime yönelik yollar](quickstart-paths.md).

## <a name="benefits"></a>Avantajlar

Mevcut Configuration Manager istemcilerini ortak yönetime kaydettiğinizde aşağıdaki hemen değeri elde edersiniz:  

- Cihaz uyumluluğuyla koşullu erişim  

- Intune tabanlı uzak eylemler, örneğin: restart, Remote Control veya factory reset

- Cihaz durumunun merkezi görünürlüğü  

- Kullanıcıları, cihazları ve uygulamaları Azure Active Directory bağlama (Azure AD)  

- Windows Autopilot ile modern sağlama  

- Uzak eylemler

Ortak yönetimden bu acil değer hakkında daha fazla bilgi için bkz. [Co-Management Ile bulut bağlantısı](quickstarts.md)için hızlı başlangıç serisi.

Ortak yönetim, çeşitli iş yükleri için Intune ile organize etmenize de olanak sağlar. Daha fazla bilgi için [Iş yükleri](#workloads) bölümüne bakın.

## <a name="prerequisites"></a>Önkoşullar

Ortak yönetim aşağıdaki alanlarda önkoşulları içerir:

- [Lisans](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [İzinler ve roller](#permissions-and-roles)  

### <a name="licensing"></a>Lisanslama

- Azure AD Premium

    > [!Note]  
    > Enterprise Mobility + Security (EMS) aboneliği hem Azure Active Directory Premium hem de Microsoft Intune içerir.

- Intune portalına erişmek için yönetici olarak en az bir Intune lisansı.

    > [!Tip]
    > Kiracınızda oturum açmak için kullandığınız hesaba bir Intune lisansı atadığınızdan emin olun. Aksi takdirde, oturum açma "Kullanıcı tanınmıyor" hata iletisiyle başarısız olur.
    >
    > Artık kullanıcılarınıza tek tek Intune veya EMS lisansı satın almanız ve atamanız gerekmez. Daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="configuration-manager"></a>Configuration Manager

Ortak yönetim Configuration Manager sürüm 1710 veya üstünü gerektirir.

Configuration Manager sürüm 1806 ' den başlayarak, birden çok Configuration Manager örneğini tek bir Intune kiracısına bağlayabilirsiniz. <!--1357944-->  

Ortak yönetimin etkinleştirilmesi, sitenizi Azure AD 'ye eklemenizi gerektirmez. [İkinci yol senaryosunda](#paths-to-co-management), ınternet tabanlı Configuration Manager istemcileri [bulut yönetimi ağ geçidini](../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) gerektirir. CMG, sitenin [bulut yönetimi Için Azure AD 'ye eklendi](../core/servers/deploy/configure/azure-services-wizard.md)olmasını gerektirir.

### <a name="azure-ad"></a>Azure AD

- Windows 10 cihazlarının Azure AD 'ye bağlı olması gerekir. Bunlar aşağıdaki türlerden biri olabilir:  

  - Cihazın şirket içi Active Directory katıldığı ve Azure Active Directory kaydettiğiniz [karma Azure AD 'ye katılmış](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid).

  - [Azure AD-yalnızca birleştirilmiş](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Bu tür bazen "bulut etki alanına katılmış" olarak adlandırılır)<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Intune’u ayarlama](https://docs.microsoft.com/intune/setup-steps)  

- [Windows 10 otomatik kayıt özelliğini etkinleştirme](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Cihazlarınızı Windows 10, sürüm 1709 veya sonraki bir sürüme yükseltin. Daha fazla bilgi için bkz. [Windows 'u hizmet olarak benimseme](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Windows 10 Mobile cihazları birlikte yönetim 'i desteklemez.

### <a name="permissions-and-roles"></a>İzinler ve roller

<!--SCCMDocs issue #667-->
| Eylem | Rol gerekli |
|----|----|
| Configuration Manager bir bulut yönetimi ağ geçidi ayarlama | Azure **Abonelik Yöneticisi** |
| Configuration Manager Azure AD uygulamaları oluşturma | Azure AD **genel Yöneticisi** |
| Azure uygulamalarını Configuration Manager içeri aktarma | Configuration Manager **tam yönetici**<br>Ek Azure rolü gerekmez |
| Configuration Manager içinde ortak yönetimi etkinleştirme | Bir Azure AD kullanıcısı<br>**Tüm** kapsam haklarıyla **tam yönetici** Configuration Manager.<!--SCCMDoc issue 626--> |

Azure rolleri hakkında daha fazla bilgi için bkz. [farklı rolleri anlama](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Configuration Manager rolleri hakkında daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../core/understand/fundamentals-of-role-based-administration.md).

## <a name="workloads"></a>İş yükleri

İş yüklerini değiştirmek zorunda değilsiniz veya hazırsanız tek tek yapabilirsiniz. Configuration Manager, Intune 'a geçiş gerçekleştirmeyen iş yükleri ve ortak yönetimin desteklemediği diğer tüm Configuration Manager özellikleri de dahil tüm diğer iş yüklerini yönetmeye devam eder.

Ortak yönetim aşağıdaki iş yüklerini destekler:

- Uyumluluk ilkeleri  

- Windows Update ilkeleri  

- Kaynak erişim ilkeleri  

- Uç Nokta Koruma  

- Cihaz yapılandırması  

- Office Tıkla-Çalıştır uygulamaları  

- İstemci uygulamaları  

Daha fazla bilgi için bkz. [Iş yükleri](workloads.md).

## <a name="monitor-co-management"></a>Ortak yönetimi izleme

Ortak Yönetim Panosu, ortamınızda ortak olarak yönetilen makineleri incelemenizi sağlar. Grafikler ilgilenilmesi gerekebilecek cihazları belirlemenize yardımcı olabilir.

![Ortak yönetim panosunun ekran görüntüsü](media/co-management-dashboard.png)

Daha fazla bilgi için bkz. [ortak yönetimi izleme](how-to-monitor.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Anında değer ve birlikte çalışmaya başlama hakkında daha fazla bilgi edinin](quickstarts.md)  

- [Öğretici: mevcut Configuration Manager istemcileri için ortak yönetimi etkinleştirme](tutorial-co-manage-clients.md)  
