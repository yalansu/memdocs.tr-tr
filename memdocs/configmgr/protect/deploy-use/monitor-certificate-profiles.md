---
title: Sertifika profillerini izleme
titleSuffix: Configuration Manager
description: Configuration Manager Sertifika profillerinin uyumluluk durumunu izlemeyi öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722301"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Configuration Manager 'de sertifika profillerini izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager konsolundaki uyumluluk sonuçlarını görüntüleme  

SCEP sertifika uyumluluğunu izlemek için, bu konsolu kullanın, bunun yerine [raporları](#view-compliance-results-by-using-reports)kullanın. 

1. Configuration Manager konsolunda, **izleme**>  **dağıtımları**' nı seçin.  

2. İlgilendiğiniz sertifika profili dağıtımını seçin.  

3. Ana sayfada Özet sertifika uyumluluk bilgilerini gözden geçirin. Daha ayrıntılı bilgi için, sertifika profilini seçin ve **giriş** sekmesinde, **dağıtım** grubunda, **durumu görüntüle** ' yi seçerek **dağıtım durumu** sayfasını açın.  

    **Dağıtım Durumu** sayfası aşağıdaki sekmeleri içerir:  

   -   **Uyumlu**: Sertifika profilinin uyumluluğunu, etkilenen varlık sayısına göre görüntüler. **Varlıklar ve Uyumluluk** çalışma alanındaki **Kullanıcılar** düğümü altında geçici bir düğüm oluşturmak için bir kurala çift tıklayabilirsiniz. Bu düğüm sertifika profiliyle uyumlu tüm kullanıcıları içerir. **Varlık Ayrıntıları** bölmesi bu profille uyumlu olan kullanıcıları da görüntüler. Daha fazla bilgi için listede bir kullanıcıya çift tıklayın.  

       > [!IMPORTANT]  
       >  Bir sertifika profili bir istemci cihazda geçerli değilse değerlendirilmez. Bununla birlikte, uyumlu olarak bildirilir.  

   -   **Hata**: Seçili sertifika profili dağıtımı için tüm hataların listesini etkilenen varlık sayısına göre görüntüler. **Varlıklar ve Uyumluluk** çalışma alanının **Kullanıcılar** düğümü altında geçici bir düğüm oluşturmak için bir kurala çift tıklayabilirsiniz. Bu düğüm bu profille hata oluşturan tüm kullanıcıları içerir. Bir kullanıcı seçtiğinizde, **Varlık Ayrıntıları** bölmesi seçili sorundan etkilenen kullanıcıları görüntüler. Daha fazla bilgi için, listede bir kullanıcıya çift tıklayın.  

   -   **Uyumlu Değil**: Seçili sertifika profili içindeki tüm uyumsuz kuralları listesini etkilenen varlık sayısına göre görüntüler. **Varlıklar ve Uyumluluk** çalışma alanının **Kullanıcılar** düğümü altında geçici bir düğüm oluşturmak için bir kurala çift tıklayabilirsiniz. Bu düğüm bu profille uyumlu olmayan tüm kullanıcıları içerir. Bir kullanıcı seçtiğinizde, **Varlık Ayrıntıları** bölmesi seçili sorundan etkilenen kullanıcıları görüntüler. Sorunla ilgili daha fazla bilgi görüntülemek için listede bir kullanıcıyı çift tıklatın.  

   -   **Bilinmiyor**: Seçilen sertifika profili dağıtımı için uyumluluğu bildirilmeyen tüm kullanıcıların listesini, cihazların geçerli istemci durumuyla birlikte görüntüler.  

4. **Dağıtım durumu** sayfasında, dağıtılan sertifika profilinin uyumluluğuyla ilgili ayrıntılı bilgileri gözden geçirin. **Dağıtımlar** düğümünde, bu bilgileri tekrar hızla bulmanıza yardımcı olacak bir geçici düğüm oluşturulur.  

    Sertifikanın kayıt durumu numara olarak görüntülenir. Her numaranın anlamını öğrenmek için aşağıdaki tabloyu kullanın:  


   | Kayıt durumu |                                                                                                                   Açıklama                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         Kayıt başarılı olmuştur ve sertifika veriliştir.                                                                                          |
   |    0x00000002     |                                                                    İstek gönderilmiştir ve kayıt beklemededir veya istek bant dışı yayınlamıştır.                                                                    |
   |    0x00000004     |                                                                                                          Kaydın ertelenmesi gerekmektedir.                                                                                                           |
   |    0x00000010     |                                                                                                               Bir hata oluşmuştur.                                                                                                                |
   |    0x00000020     |                                                                                                        Kayıt durumu bilinmemektedir.                                                                                                        |
   |    0x00000040     | Durum bilgileri atlanmıştır. "<https://msdn.microsoft.com/windows/ms721572>" \L "_security_certification_authority_gly" sertifika yetkilisi geçerli değilse veya izleme için seçilmediyse bu durum oluşabilir. |
   |    0x00000100     |                                                                                                           Kayıt reddedilmiştir.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Raporları kullanarak uyumluluk sonuçlarını görüntüleme

Configuration Manager uyumluluk ayarları, sertifika profilleriyle ilgili bilgileri izlemek için kullanabileceğiniz yerleşik raporları içerir. Bu raporlar **Uyumluluk ve Ayarlar Yönetimi**rapor kategorisindedir.  

> [!IMPORTANT]  
>  Uyumluluk ayarlarına ait raporlarda **Cihaz filtresi** ve **Kullanıcı filtresi** parametrelerini kullandığınızda bir joker (%) karakter kullanmanız gerekir.  

SCEP sertifika uyumluluğunu izlemek için, bu sertifika raporlarını **Şirket kaynağı erişimi**rapor düğümü altında kullanın:  

-   Sertifika verme geçmişi  
-   Süresi dolmak üzere sertifikalara sahip varlıkların listesi  
-   Sertifika verme durumuna göre varlıkların listesi  



 Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  
