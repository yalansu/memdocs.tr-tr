---
title: Site verilerini yayımlama
titleSuffix: Configuration Manager
description: Configuration Manager siteleri Active Directory Domain Services nasıl yayımlayacağınızı öğrenin.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718367"
---
# <a name="publish-site-data-for-configuration-manager"></a>Configuration Manager için site verilerini yayımlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için Active Directory şemasını genişletdikten sonra, Active Directory Domain Services Configuration Manager siteleri yayımlayabilirsiniz (AD DS). Bu, Active Directory bilgisayarlarının güvenilen bir kaynaktan site bilgilerini güvenli bir şekilde almasına olanak tanır. Site bilgilerinin AD DS 'ye yayımlanması temel Configuration Manager işlevselliği için gerekli değildir, ancak bunu yapmak için yönetim yükünü azaltabilir.  

-   **Bir site AD DS yayımlanacak şekilde yapılandırıldığında**Configuration Manager istemciler yönetim noktalarını Active Directory yayımlamayla otomatik olarak bulabilir. Bir genel katalog sunucusunda bir LDAP sorgusu kullanırlar.  

-   **Bir site AD DS'de yayım yapmıyorsa**, istemcilerin varsayılan yönetim noktalarını bulabilmesi için alternatif bir mekanizmaya sahip olması gerekir.  

İstemcilerin bir yönetim noktasını nasıl bulduklarını öğrenmek için bkz. [İstemcilerin site kaynaklarını ve Configuration Manager hizmetleri nasıl bulduklarını anlama](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Siteleri AD DS'de yayım yapacak biçimde yapılandırma  
 Aşağıdakiler üst düzey adımlardır:  

-   Site verilerini yayımlayacağınız her ormanda [Configuration Manager için Active Directory şemasını genişletmeniz](../../../../core/plan-design/network/extend-the-active-directory-schema.md) gerekir. Ayrıca **sistem yönetimi** kapsayıcısının mevcut olduğundan emin olun.  

-   **Sistem yönetimi** kapsayıcısına ve tüm alt nesnelerine verileri **tam** olarak yayımlayabilecek her birincil sitenin bilgisayar hesabına izin vermeniz gerekir.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Configuration Manager sitesinin site bilgilerini Active Directory ormanına yayımlamasını sağlamak için

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin ve **siteler**' e tıklayın. Site verilerini yayımlamasını istediğiniz siteyi seçin. Ardından **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' e tıklayın.  

3.  Site özelliklerinin **Yayımlama** sekmesinde, bu sitenin site verilerini yayımlayacağı ormanları seçin.  

4.  Yapılandırmayı kaydetmek için **Tamam** ' ı tıklatın.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Yayımlamak üzere Active Directory ormanları ayarlamak için  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  **Yönetim** çalışma alanında, **Hiyerarşi Yapılandırması**' nı genişletin ve **Active Directory ormanları**' na tıklayın. Active Directory Orman Saptama daha önce çalıştıysa bulunan her bir ormanı sonuçlar bölmesinde görürsünüz. Active Directory Orman Saptama çalıştığında, yerel orman ve güvenilen ormanlar bulunur. Yalnızca güvenilmeyen ormanların elle eklenmesi gerekir.  

    -   Daha önce bulunan bir ormanı ayarlamak için, sonuçlar bölmesinde ormanı seçin. Ardından, **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler** ' e tıklayarak orman özelliklerini açın. Adım 3 ile devam edin.  

    -   Listelenmeyen yeni bir ormanı ayarlamak için, **giriş** sekmesinde, **Oluştur** grubunda, **orman** Ekle ' ye tıklayarak **Ormanlar Ekle** iletişim kutusunu açın. Adım 3 ile devam edin.  

3.  **Genel** sekmesinde, keşfetmesini istediğiniz ormanın tüm yapılandırmasını ve **Active Directory orman hesabını**belirtin.  

    > [!NOTE]  
    >  Active Directory Orman Saptama, bulma ve güvenilmeyen ormanlara yayımlama için genel hesap gerektirir. Site sunucusunun bilgisayar hesabını kullanmıyorsanız, yalnızca genel bir hesap seçebilirsiniz.  

4.  Sitelerin bu ormana site verilerini yayınlamasına izin vermeyi planlıyorsanız, **Yayınlama** sekmesinde bu ormana yayın yapmak için yapılandırmaları tamamlayın.  

    > [!NOTE]  
    >  Siteleri bir ormana yayımlamak üzere etkinleştirirseniz, Configuration Manager için o ormanın Active Directory şemasını genişletmeniz gerekir. Active Directory orman hesabı, bu ormandaki sistem kapsayıcısı için tam denetim izinlerine sahip olmalıdır.  

5.  Active Directory Orman Saptama ile kullanım için bu ormanın yapılandırmasını tamamladığınızda, yapılandırmayı kaydetmek için **OK** düğmesini tıklatın.  
