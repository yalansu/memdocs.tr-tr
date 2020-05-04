---
title: Endpoint Protection için Windows Güvenlik Duvarı ilkeleri
titleSuffix: Configuration Manager
description: System Center 2012 Configuration Manager Endpoint Protection için güvenlik duvarı ilkeleri oluşturma ve dağıtma hakkında bilgi edinin.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715497"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager Endpoint Protection için Windows Güvenlik Duvarı ilkeleri oluşturma ve dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Endpoint Protection için güvenlik duvarı ilkeleri, hiyerarşinizdeki istemci bilgisayarlarda temel Windows Güvenlik Duvarı yapılandırma ve bakım görevlerini gerçekleştirmenizi sağlar. Windows Güvenlik Duvarı ilkelerini kullanarak şu görevleri gerçekleştirebilirsiniz:  

-   Windows Güvenlik Duvarının açık veya kapalı olduğunu denetleme.  

-   İstemci bilgisayarlarda gelen bağlantılara izin verilip verilmediğini denetleme.  

-   Windows Güvenlik Duvarı tarafından yeni bir program engellendiğinde kullanıcılara bildirim gönderilip gönderilmediğini denetleme.  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve uyum** çalışma alanında **Endpoint Protection**' ı genişletin ve ardından **Windows Güvenlik Duvarı ilkeleri**' ne tıklayın.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **Windows Güvenlik Duvarı İlkesi Oluştur**’a tıklayın.  

4.  **Windows Güvenlik Duvarı Oluşturma Sihirbazı** ’nın **Genel**sayfasında bu güvenlik duvarı ilkesi için bir ad ve isteğe bağlı bir açıklama belirtip **İleri**’ye tıklayın.  

5.  Sihirbazın **Profil Ayarları** sayfasında, her bir ağ profili için aşağıdaki ayarları yapılandırın:  

    > [!NOTE]  
    >  Ağ profilleri hakkında daha fazla bilgi için Windows belgelerine bakın.  

    -   **Windows Güvenlik Duvarı’nı Etkinleştir**  

        > [!NOTE]  
        >  **Windows Güvenlik Duvarı’nı Etkinleştir** seçeneği etkin değilse, sihirbazın bu sayfasındaki diğer ayarlar kullanılamaz.  

    -   **İzin verilen programlar listesindekiler dahil tüm gelen bağlantıları engelleme**  

    -   **Windows Güvenlik Duvarı yeni bir programı engellediğinde kullanıcıya bildir**  

6.  Sihirbazın **Özet** sayfasında, yapılacak eylemleri gözden geçirin ve sihirbazı tamamlayın.  

7.  Yeni Windows Güvenlik Duvarı ilkesinin **Windows Güvenlik Duvarı İlkeleri** listesinde görüntülendiğini doğrulayın.  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Windows Güvenlik Duvarı ilkesini dağıtmak için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve uyum** çalışma alanında **Endpoint Protection**' ı genişletin ve ardından **Windows Güvenlik Duvarı ilkeleri**' ne tıklayın.  

3.  **Windows Güvenlik Duvarı İlkeleri** listesinde, dağıtmak istediğiniz Windows Güvenlik Duvarı ilkesini seçin.  

4.  **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıt**'a tıklayın.  

5.  **Windows Güvenlik Duvarı İlkesi Dağıt** iletişim kutusunda, bu Windows Güvenlik Duvarı ilkesini atamak istediğiniz koleksiyon ile bir atama zamanlaması belirtin. Windows Güvenlik Duvarı ilkesi ile eşleşmesi için istemcilerdeki Windows Güvenlik Duvarı ayarlarını yeniden yapılandırmak amacıyla, bu zamanlamayı kullandığınızda Windows Güvenlik Duvarı ilkesinin uyumluluğu değerlendirilir.  

6.  **Windows Güvenlik Duvarı İlkesi Dağıt** iletişim kutusunu kapatmak ve Windows Güvenlik Duvarı ilkesini dağıtmak için **Tamam** ’a tıklayın.  

    > [!IMPORTANT]  
    >  Windows Güvenlik Duvarı ilkesini bir koleksiyona dağıttığınızda bu ilke, ağ taşmasını önlemek için 2 saat boyunca rastgele sırayla bilgisayarlara uygulanır.
