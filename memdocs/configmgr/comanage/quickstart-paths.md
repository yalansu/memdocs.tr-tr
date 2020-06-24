---
title: Ortak yönetim yolları
titleSuffix: Configuration Manager
description: Ortak yönetimi ayarlama konusunda iki temel yol için önkoşulları anlayın.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d481976a6c86da67670871690ba16985a67c80d8
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746468"
---
# <a name="paths-to-co-management"></a>Ortak yönetim yolları

Ortak yönetimi ayarlamanıza yönelik iki temel yol vardır. Her yol için önkoşulları anlamak önemlidir. Her biri Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune ve Windows 10 birleşimini gerektirir. 

1. [Mevcut Configuration Manager ile yönetilen cihazları Intune 'a otomatik kaydetme](#bkmk_path1)  
2. [Modern sağlama ile Configuration Manager istemcisini önyükleme](#bkmk_path2)  

![Ortak yönetim yollarının diyagramı](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a>Yol 1: mevcut istemcileri otomatik kaydetme

Bu yolu almak, mevcut Configuration Manager yönetilen cihazlarınızı Intune 'a hızlıca kaydedebilir. Bu cihazların Configuration Manager ile yönetimi, ortak yönetimi etkinleştirmeden önce öğesinden farklı değildir. Artık tüm bulut tabanlı avantajları elde edersiniz. Bu yol kullanıcılarınız için saydamdır.

Ayarlamanız gerekenler şunlardır:
- Hibrit Azure AD
    - Aşağıdaki [Azure AD karma kimlik seçeneklerinden](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin)biri:  
       - [Sorunsuz çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) ile [parola KARMASı eşitlemesi](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) (SSO)
       - [Sorunsuz çoklu oturum açma (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) ile [geçişli kimlik doğrulaması](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta)
       - [Federasyon SSO 'SU (Active Directory Federasyon Hizmetleri (AD FS) (AD FS) ile)](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium lisansı
    - Karma Azure AD-katılmayı yapılandırma (bir seçenek belirleyin):
        - Yönetilen etki alanları için
        - Federasyon etki alanları için
- Hibrit Azure AD-JOIN için istemci Aracısı ayarı
- Cihazların otomatik kaydını Intune 'a yapılandırma
- Configuration Manager içinde ortak yönetimi etkinleştirme

Bu yol hakkında bir öğretici için bkz. [öğretici: mevcut Configuration Manager istemcileri için ortak yönetimi etkinleştirme](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a>Yol 2: modern sağlama ile önyükleme

Ayarlamanız gerekenler şunlardır:

1. [Gelişmiş HTTP kurulumu](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Azure 'da bulut hizmetleri oluşturma](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Yönetim noktasını ve istemcileri bulut yönetimi ağ geçidini kullanacak şekilde yapılandırma](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Configuration Manager istemcisini dağıtmak için Intune 'U kullanma](how-to-prepare-Win10.md)  

Bu yol hakkında bir öğretici için bkz. [öğretici: yeni internet tabanlı cihazlar için ortak yönetimi etkinleştirme](tutorial-co-manage-new-devices.md).

