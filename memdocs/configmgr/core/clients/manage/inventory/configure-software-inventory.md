---
title: Yazılım envanterini yapılandırma
titleSuffix: Configuration Manager
description: Yazılım envanterini yapılandırın ve Configuration Manager ' de yazılım envanterinden klasörleri dışlayın.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74436eb95166ae9bc78d7ae22881b709349bf847
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714433"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Configuration Manager 'de yazılım envanterini yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu yordam, yazılım envanteri için varsayılan istemci ayarlarını yapılandırır ve hiyerarşinizdeki tüm bilgisayarlar için geçerlidir. Bu ayarları yalnızca bazı bilgisayarlara uygulamak istiyorsanız, özel bir cihaz istemci ayarı oluşturun ve bir koleksiyona atayın. Özel cihaz ayarları oluşturma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Yazılım envanterini yapılandırmak için  

1. Configuration Manager konsolunda, **Yönetim** > **istemci ayarları**  **varsayılan istemci ayarları**' nı seçin.  

2. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

3. **Varsayılan ayarlar** Iletişim kutusunda **yazılım envanteri**' ni seçin.  

4. **Cihaz Ayarları** listesinde aşağıdaki değerleri yapılandırın:  

   -   **İstemcilerde yazılım envanterini etkinleştir** -aşağı açılan listeden **true değerini**seçin.  

   -   **Yazılım envanteri ve dosya toplama zamanlamasını zamanla** -istemcilerin yazılım envanterini ve dosyalarını toplayacağı aralığı yapılandırır.   

5. İhtiyacınız olan istemci ayarlarını yapılandırın. [İstemci ayarları hakkında](../../../../core/clients/deploy/about-client-settings.md) makalesinin [yazılım envanteri](../../../../core/clients/deploy/about-client-settings.md#software-inventory) bölümünde istemci ayarlarının bir listesi bulunur.  

   İstemci ilkesini sonraki sefer indirdiklerinde, istemci bilgisayarları bu ayarlarla yapılandırılır. Tek bir istemci için ilke almayı başlatmak için bkz. [istemcileri yönetme](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Inventoryprovider 'da 80041006 hata kodu. log, WMI sağlayıcısının bellek yetersiz olduğu anlamına gelir. Diğer bir deyişle, bir sağlayıcının bellek kotası sınırına ulaşıldı ve envanter sağlayıcısı devam edemez.
   > Bu durumda, envanter Aracısı 0 girişi olan bir rapor oluşturur, bu nedenle hiçbir stok öğesi bildirilmemiştir. <br/>
   > Bu hata için olası bir çözüm, yazılım envanteri koleksiyonunun kapsamını azaltmaktır. Envanter kapsamını sınırlandırdıktan sonra hata oluştuğunda, [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) sınıfında tanımlanan [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) özelliğinin artırılması bir çözüm sağlayabilir.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Klasörleri yazılım envanterinden dışlamak için  

1.  Notepad.exe kullanarak **Skpswi.dat**adlı boş bir dosya oluşturun.  

2.  **Skpswi. dat** dosyasına sağ tıklayın ve **Özellikler**' e tıklayın. Skpswi.dat dosyası için dosya özelliklerinde **Gizli** özniteliğini seçin.  

3.  **Skpswi.dat** dosyasını her bir istemci sabit sürücüsünün veya yazılım envanterinden dışlamak istediğiniz klasör yapısının köküne yerleştirin.  

> [!NOTE]  
>  Bu dosya istemci bilgisayardaki sürücüden silinmedikçe yazılım envanteri istemciyi envantere almaz.
