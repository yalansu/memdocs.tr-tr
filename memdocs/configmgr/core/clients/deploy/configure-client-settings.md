---
title: İstemci ayarlarını yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager istemci ayarları ' nı seçin.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c64895c7945b972821a1dee1702047e61b740026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713593"
---
# <a name="how-to-configure-client-settings-in-configuration-manager"></a>Configuration Manager istemci ayarlarını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager tüm istemci ayarlarını **Yönetim** > **istemcisi ayarlarından**yönetirsiniz. Uygulanan özel ayarları bulunmayan hiyerarşideki tüm kullanıcılar ve aygıtlar için ayarları yapılandırmak istediğinizde varsayılan ayarları değiştirin. Yalnızca bazı kullanıcılara veya cihazlara farklı ayarlar uygulamak istiyorsanız, özel ayarlar oluşturun ve koleksiyonlara dağıtın.  

Her istemci ayarı hakkında daha fazla bilgi için bkz. [istemci ayarları hakkında](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Aygıtların yapılandırma uyumluluğunu değerlendirmek, izlemek ve düzeltmek için istemcileri yönetmek amacıyla yapılandırma öğelerini de kullanabilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager cihaz uyumluluğunu doğrulayın](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Varsayılan istemci ayarlarını yapılandırma    

1. Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

2. **Giriş** sekmesinde **Özellikler**' i seçin.  

3. Gezinti bölmesinde ayar gruplarının her biri için istemci ayarlarını görüntüleyin ve yapılandırın.  

   İstemci ilkesini sonraki sefer indirdiklerinde, istemci bilgisayarları bu ayarlarla yapılandırılır. Tek bir istemci için ilke almayı başlatmak için bkz. [istemcileri yönetme](../../../core/clients/manage/manage-clients.md)bölümünde [Configuration Manager Istemcisi Için ilke almayı başlatma](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) .  

##  <a name="create-and-deploy-custom-client-settings"></a>Özel istemci ayarlarını oluşturma ve dağıtma  
Bu özel ayarları dağıttığınızda, bunlar varsayılan istemci ayarlarını geçersiz kılar. Bu yordama başlamadan önce bu özel istemci ayarlarını gerektiren kullanıcıları veya aygıtları içeren bir koleksiyonunuz olduğundan emin olun.  

1. Configuration Manager konsolunda **Yönetim** > **istemci ayarları**' nı seçin.  

2. **Giriş** sekmesinde, **Oluştur** grubunda, **özel istemci ayarları oluştur**' u seçin ve şunlardan birini seçin:  

   -   **Özel İstemci Cihaz Ayarları Oluştur**  

   -   **Özel İstemci Kullanıcı Ayarları Oluştur**  

3. Benzersiz bir ad ve seçenek açıklaması belirtin.  

4. Bir ayar grubunu görüntüleyen bir veya daha fazla onay kutusunu seçin.  

5. Gezinti bölmesinden her bir ayar grubunu seçin ve kullanılabilir ayarları yapılandırın ve ardından **Tamam**' a tıklayın.   

6. Oluşturduğunuz özel istemci ayarını seçin. **Giriş** sekmesinde, **istemci ayarları** grubunda, **Dağıt**' ı seçin.  

7. **Koleksiyon Seç** iletişim kutusunda, uygun koleksiyonu seçin ve ardından **Tamam**' ı seçin. Ayrıntılar bölmesinde **Dağıtımlar** sekmesini tıklatırsanız seçilen koleksiyonu doğrulayabilirsiniz.  

8. Oluşturduğunuz özel istemci ayarının sırasını görüntüleyin. Birden fazla varsayılan istemci ayarına sahip olduğunuzda, bunlar sıra numaralarına göre uygulanır. Bir çakışma varsa, en düşük sıra numarasına sahip olan ayar diğer ayarları geçersiz kılar. Sıra numarasını değiştirmek için, **giriş** sekmesinde, **istemci ayarları** grubunda, **öğeyi yukarı taşı** veya **öğeyi aşağı taşı**' yı seçin.  

   İstemci ilkesini sonraki sefer indirdiklerinde, istemci bilgisayarları bu ayarlarla yapılandırılır. Tek bir istemci için ilke almayı başlatmak için bkz. [istemcileri yönetme](../../../core/clients/manage/manage-clients.md)bölümünde [Configuration Manager Istemcisi Için ilke almayı başlatma](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) .  



##  <a name="view-client-settings"></a>İstemci ayarlarını görüntüle  
 Aynı cihaza, kullanıcıya veya kullanıcı grubuna birden fazla istemci ayarı dağıttığınızda, ayarların önceliklendirmesi ve bileşimi karmaşıktır. İstemci ayarlarını görüntülemek için:  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **cihazları** > **kullanıcıları** veya **Kullanıcı koleksiyonları**' nı seçin.  

3.  Bir aygıt, kullanıcı veya kullanıcı grubu seçin ve **İstemci Ayarları** grubunda **İstemci Sonuç Ayarları**'nı seçin.  

4.  Sol bölmeden bir istemci ayarı seçin ve ayarlar görüntülenir. Bu görünümde, ayarlar salt okunurdur. 

    > [!NOTE]  
    >  İstemci ayarlarını görüntülemek için Istemci ayarlarına okuma erişiminizin olması gerekir.  

    
