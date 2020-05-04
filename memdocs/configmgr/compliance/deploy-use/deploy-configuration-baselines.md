---
title: Yapılandırma taban çizgilerini dağıtma
titleSuffix: Configuration Manager
description: Yapılandırma temel dağıtımlarını tanımlamak ve dağıtımlardan yapılandırma temelleri eklemek veya kaldırmak için yapılandırma temellerini dağıtın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712340"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Configuration Manager içinde yapılandırma temelleri dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içindeki yapılandırma temelleri, bu koleksiyonlardaki istemci cihazların yapılandırma temeliyle uyumluluğunu değerlendirebilmesi için bir veya daha fazla Kullanıcı veya cihaz koleksiyonuna dağıtılmalıdır.  

Yapılandırma temellerini dağıtımlara ekleme veya kaldırmanın yanı sıra değerlendirme zamanlamasını belirtmeyi içeren yapılandırma temeli dağıtımlarını tanımlamak için **Yapılandırma Temelleri Dağıt** iletişim kutusunu kullanın.  

## <a name="deploy-a-configuration-baseline"></a>Yapılandırma temeli dağıtma  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Uyumluluk ayarları** > **yapılandırma temelleri**' ne tıklayın.  

3.  **Yapılandırma Temelleri** listesinde dağıtmak istediğiniz yapılandırma seçtikten sonra **Giriş** sekmesindeki **Dağıtım** grubunda **Dağıt**'a tıklayın.  

4.  **Yapılandırma Temellerini Dağıt** iletişim kutusundaki **Kullanılabilir yapılandırma temelleri** listesinde dağıtmak istediğiniz yapılandırma temellerini seçin. **Ekle** ’ye tıklayarak bunları **Seçili yapılandırma temelleri** listesine ekleyin.  

    > [!IMPORTANT]  
    >  Dağıtılan bir yapılandırma temeline eklenmiş bir yapılandırma öğesini değiştirirseniz, zamanlanan sonraki değerlendirme zamanına kadar düzeltilen yapılandırma öğesi uyum için değerlendirilmez.  

5.  Aşağıdaki ek bilgileri belirtin:  

    -   **Desteklendiğinde uyumsuz kuralları düzelt** – Configuration Manager tarafından kaydedilen mobil cihazların WINDOWS YÖNETIM araçları (WMI), kayıt defteri, komut dosyaları ve tüm ayarlar için uyumlu olmayan kuralları otomatik olarak düzeltir.  

    -   **Bakım süresi dışında düzeltmeye izin ver** – Yapılandırma temelini dağıtmakta olduğunuz koleksiyon için bir bakım penceresi yapılandırıldıysa, uyumluluk ayarlarının bakım penceresi dışındaki değeri düzeltmesine izin vermek üzere bu seçeneği etkinleştirin. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

6.  **Uyarı oluştur** : yapılandırma temeli uyumluluğu, belirtilen tarih ve saate göre belirtilen yüzdeden küçük olduğunda oluşturulan bir uyarı yapılandırır. System Center Operations Manager'a bir uyarının ne zaman gönderilmesini istediğinizi de belirtebilirsiniz.  

7.  **Koleksiyon** - Yapılandırma temelini dağıtmak istediğiniz koleksiyonu seçmek için **Gözat** 'a tıklayın.  

8.  **Bu yapılandırma temeline ait uyumluluk değerlendirme zamanlamasını belirtin** Dağıtılan yapılandırma temelinin istemci bilgisayarlarda değerlendirilme zamanlamasını belirtir. Bu, basit veya özel zamanlama olabilir.  

    > [!NOTE]  
    >  Yapılandırma temeli bir bilgisayara dağıtılırsa, zamanladığınız başlangıç saatinden sonraki iki saat içinde uyumluluk için değerlendirilir. Bir kullanıcıya dağıtılırsa, kullanıcı oturum açtığında uyumluluk için değerlendirilir.  

9. **Yapılandırma Temellerini Dağıt** iletişim kutusunu kapatmak ve dağıtım oluşturmak için **Tamam** ’a tıklayın. Dağıtımı izleme hakkında daha fazla bilgi için bkz. [izleyici uyumluluk ayarları](monitor-compliance-settings.md).  
