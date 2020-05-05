---
title: E-posta, Wi-Fi ve VPN profillerini izleme
titleSuffix: Configuration Manager
description: Configuration Manager ' deki e-posta, Wi-Fi ve VPN profillerinin uyumluluk durumunu nasıl izleyeceğinizi öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724499"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 'da e-posta, Wi-Fi ve VPN profillerini izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hiyerarşinizdeki kullanıcılara Configuration Manager e-posta, Wi-Fi veya VPN profilleri dağıttıktan sonra, profilin uyumluluk durumunu izlemek için aşağıdaki yordamları kullanabilirsiniz:  

-   [Configuration Manager konsolundaki uyumluluk sonuçlarını görüntüleme](#BKMK_console)  

-   [Raporları kullanarak uyumluluk sonuçlarını görüntüleme](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a>Configuration Manager konsolundaki uyumluluk sonuçlarını görüntüleme  
 Configuration Manager konsolundaki dağıtılan profillerin uyumluluğuyla ilgili ayrıntıları görüntülemek için bu yordamı kullanın.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager konsolundaki uyumluluk sonuçlarını görüntülemek için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  **İzleme** çalışma alanında, **Dağıtımlar**'ı tıklatın.  

3.  **Dağıtımlar** listesinde, uyumluluk bilgilerini incelemek istediğiniz profil dağıtımını seçin.  

4.  Ana sayfada profil dağıtımının uyumluluğuyla ilgili özet bilgileri gözden geçirebilirsiniz. Daha ayrıntılı bilgi görüntülemek için, profil dağıtımını seçin ve **giriş** sekmesinde, **dağıtım** grubunda, **durumu görüntüle** ' ye tıklayarak **dağıtım durumu** sayfasını açın.  

     **Dağıtım Durumu** sayfası aşağıdaki sekmeleri içerir:  

    -   **Uyumlu:** Etkilenen varlık sayısına göre profilin uyumluluğunu görüntüler. Bu profille uyumlu olan tüm kullanıcıları içeren **Varlıklar ve Uyumluluk** çalışma alanının **Kullanıcılar** düğümü altında geçici bir düğüm oluşturmak için bir kurala çift tıklayabilirsiniz. **Varlık ayrıntıları** bölmesi, profille uyumlu olan kullanıcıları görüntüler. Ek bilgileri görüntülemek için listede bir kullanıcıya çift tıklayın.  

        > [!IMPORTANT]  
        >  Bir profil, istemci cihazında uygulanamıyorsa değerlendirilmez; Bununla birlikte, uyumlu olarak döndürülür.  

    -   **Hata:** Etkilenen varlık sayısına dayalı olarak seçili profil dağıtımı için tüm hataların listesini görüntüler. Bir kurala çift tıklayarak **Varlıklar ve Uyumluluk** çalışma alanındaki **Kullanıcılar** düğümü altında, bu profilde hata veren tüm kullanıcıları içeren geçici bir düğüm oluşturabilirsiniz. Bir kullanıcı seçtiğinizde, **Varlık Ayrıntıları** bölmesi seçili sorundan etkilenen kullanıcıları görüntüler. Sorunla ilgili ek bilgileri görüntülemek için listede bir kullanıcıya çift tıklayın.  

    -   **Uyumlu değil:** Etkilenen varlık sayısına göre profil içindeki tüm uyumsuz kuralların listesini görüntüler. Bu profille uyumlu olmayan tüm kullanıcıları içeren **Varlıklar ve Uyum** çalışma alanının **Kullanıcılar** düğümü altında geçici bir düğüm oluşturmak için bir kuralı çift tıklatabilirsiniz. Bir kullanıcı seçtiğinizde, **Varlık Ayrıntıları** bölmesi seçili sorundan etkilenen kullanıcıları görüntüler. Sorunla ilgili daha fazla bilgi görüntülemek için listede bir kullanıcıyı çift tıklatın.  

    -   **Bilinmiyor:** Seçilen profil dağıtımı için uyumluluk bildirmeyen tüm kullanıcıların listesini cihazların geçerli istemci durumuyla birlikte görüntüler.  

5.  **Dağıtım durumu** sayfasında, dağıtılan profilin uyumluluğuyla ilgili ayrıntılı bilgileri gözden geçirebilirsiniz. **Dağıtımlar** düğümünde, bu bilgileri tekrar hızla bulmanıza yardımcı olacak bir geçici düğüm oluşturulur.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a>Raporları kullanarak uyumluluk sonuçlarını görüntüleme  
 Configuration Manager profillerin dahil olduğu uyumluluk ayarları, profillerle ilgili bilgileri izlemenize olanak sağlayan bir dizi yerleşik rapor da içerir. Bu raporlar **Uyumluluk ve Ayarlar Yönetimi**rapor kategorisindedir.  

> [!IMPORTANT]  
>  Uyumluluk ayarları raporlarında **Cihaz filtresi** ve **Kullanıcı filtresi** parametrelerini kullanırken joker karakteri (%) kullanmanız gerekir.  

 Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  
