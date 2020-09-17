---
title: Yazılım güncelleştirmeleri için güvenlik ve gizlilik
titleSuffix: Configuration Manager
description: Yazılım güncelleştirmelerine yönelik güvenlik için en iyi uygulamaları izleyin ve Configuration Manager gizlilik bilgilerini nasıl işleyeceğinizi öğrenin.
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0838f43abf7ff972ac3f6ca2cdf44dcafda323ca
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718731"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Configuration Manager 'de yazılım güncelleştirmeleri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager yazılım güncelleştirmeleri için güvenlik ve gizlilik bilgilerini içerir.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Yazılım güncelleştirmeleri için en iyi güvenlik yöntemleri  
 İstemcilere yazılım güncelleştirmelerini dağıtırken aşağıdaki en iyi güvenlik yöntemlerini kullanın:  

-   Yazılım güncelleştirme paketlerinin varsayılan izinlerini değiştirmeyin.  

     Varsayılan olarak, yazılım güncelleştirme paketleri yöneticilere **Tam Denetim** ve kullanıcılara **Okuma** erişimi sağlamaya ayarlanmıştır. Bu ayarları değiştirirseniz bu durum, bir saldırganın yazılım güncelleştirmelerini eklemesine, kaldırmasına veya silmesine neden olabilir.  

-   Yazılım güncelleştirmelerinin indirme konumuna olan erişimi denetleyin.  

     SMS Sağlayıcısı için bilgisayar hesaplarının, site sunucusunun ve yazılım güncelleştirmelerini indirme konumuna indirecek olan yönetici kullanıcının, indirme konumuna **Yazma** erişimi olması gerekir. İndirme konumundaki yazılım güncelleştirme kaynak dosyalarının saldırganlar tarafından izinsiz değiştirilme riskini azaltmak için indirme konumuna erişimi sınırlandırın.  

     Ayrıca, indirme konumu için bir UNC paylaşımı kullanırsanız, yazılım güncelleştirme kaynak dosyalarının ağ üzerinden aktarıldığında izinsiz değiştirilmesini engellemek için IPsec veya SMB imzası kullanarak ağ kanalını güvenli hale getirin.  

-   Dağıtım zamanlarını değerlendirmek için UTC kullanın.  

     UTC yerine yerel saat kullanırsanız kullanıcılar, bilgisayarlarındaki saat dilimini değiştirerek yazılım güncelleştirmelerini geciktirebilir.  

-   Windows Server Update Services (WSUS) üzerinde SSL'i etkinleştirin ve WSUS'yi güvenli hale getirmek için en iyi yöntemleri takip edin.  

     Configuration Manager ile kullandığınız WSUS sürümü için en iyi güvenlik uygulamalarını tanımlayıp izleyin. 

     SSL 'yi etkinleştirme hakkında daha fazla bilgi için bkz. [bir yazılım güncelleştirme noktasını BIR PKI sertifikası öğreticisiyle TLS/SSL kullanmak Için yapılandırma](../get-started/software-update-point-ssl.md). 

    > [!IMPORTANT]  
    >  WSUS sunucusuna SSL iletişimini etkinleştirmek için yazılım güncelleştirme noktasını yapılandırırsanız, WSUS sunucusunda SSL için sanal kökler yapılandırmanız gerekir.  

-   CRL denetimini etkinleştirin.  

     Configuration Manager, varsayılan olarak, yazılım güncelleştirmelerindeki imzayı bilgisayarlara dağıtılmadan önce doğrulamak için sertifika iptal listesini (CRL) denetlemez. Her sertifika kullanıldığında CRL'nin denetlenmesi, iptal edilmiş sertifika kullanımına karşı daha fazla güvenlik sağlar ancak bağlantıda bir gecikmeye ve CRL denetimi yapılan bilgisayarda ek işlem yapılmasına neden olur.  

     Yazılım güncelleştirmeleri için CRL denetimini etkinleştirme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri IÇIN CRL denetimini etkinleştirme](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Özel bir web sitesi kullanmak için WSUS'yi yapılandırın.  

     Yazılım güncelleştirme noktasına WSUS'yi yüklediğinizde mevcut IIS Varsayılan Web sitesini kullanma veya özel bir WSUS web sitesi oluşturma seçenekleriniz vardır. WSUS için özel bir Web sitesi oluşturun, böylece IIS, diğer Configuration Manager site sistemleri veya diğer uygulamalar tarafından kullanılan aynı Web sitesini paylaşmak yerine, WSUS hizmetlerini ayrılmış bir sanal Web sitesinde barındırır.  

     Daha fazla bilgi için, bkz. [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a> Yazılım güncelleştirmeleri için gizlilik bilgileri  
 Yazılım güncelleştirmeleri, hangi yazılım güncelleştirmesine ihtiyacınız olduğunu belirlemek için istemci bilgisayarlarınızı tarar ve daha sonra bu bilgileri site veritabanına geri gönderir. Yazılım güncelleştirme işlemi sırasında, Configuration Manager bilgisayar ve oturum açma hesaplarını belirleyen istemciler ve sunucular arasında bilgi aktarabilir.  

 Configuration Manager, yazılım dağıtım işlemiyle ilgili durum bilgilerini tutar. Durum bilgisi, iletim veya depolama sırasında şifrelenmez. Durum bilgileri Configuration Manager veritabanında depolanır ve veritabanı bakım görevleri tarafından silinir. Durum bilgilerinin hiçbiri Microsoft'a gönderilmez.  

 İstemci bilgisayarlarına yazılım güncelleştirmelerini yüklemek için Configuration Manager yazılım güncelleştirmelerinin kullanılması, bu güncelleştirmeler için Configuration Manager yazılım lisans koşullarından ayrı olan yazılım lisans koşullarına tabi olabilir. Configuration Manager kullanarak yazılım güncelleştirmelerini yüklemeden önce yazılım lisans koşulları 'nı her zaman gözden geçirin ve kabul edin.  

 Configuration Manager, varsayılan olarak yazılım güncelleştirmelerini uygulamaz ve bilgiler toplanmadan önce çeşitli yapılandırma adımları gerektirir.  

 Yazılım güncelleştirmelerini yapılandırmadan önce gizlilik gereksinimlerinizi dikkate alın.  
