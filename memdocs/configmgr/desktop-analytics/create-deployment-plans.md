---
title: Dağıtım planları oluşturma
titleSuffix: Configuration Manager
description: Masaüstü analizinden dağıtım planları oluşturmak için nasıl yapılır Kılavuzu.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c42576f35d285fc7285466c4208d7ccaf370daa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723708"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Masaüstü Analizi 'nde dağıtım planları oluşturma

Bu makalede, masaüstü Analizi 'nde dağıtım planı oluşturma adımları sağlanmaktadır. Başlamadan önce, önce [dağıtım planları hakkında bilgi edinin](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Windows 10 için plan oluşturma

Windows 10 dağıtımı için bir plan oluşturmak üzere masaüstü analizlerini kullanmak için bu bölümdeki adımları izleyin.

1. [Masaüstü Analizi portalını](https://aka.ms/desktopanalytics)açın. En az **çalışma alanı katkıda** bulunan izinleri olan kimlik bilgilerini kullanın.  

2. Yönet grubunda **dağıtım planları** ' nı seçin.  

3. **Dağıtım planları** bölmesinde **Oluştur**' u seçin.  

4. **Dağıtım planı oluştur** bölmesinde, aşağıdaki ayarları yapılandırın:  

    - **Ad**: dağıtım planı için benzersiz bir ad  

    - **Ürünler ve sürümler**: hangi Windows 10 sürümünü dağıtacağınızı seçin. Microsoft, en son sürümü kullanan dağıtım planlarının oluşturulmasını önerir.  

    - **Cihaz grupları**: aynı hiyerarşiden bir veya daha fazla grup seçin. Bu gruplar Configuration Manager 'ten eşitlenen [cihaz koleksiyonlarıdır](connect-configmgr.md#bkmk_Collections) .

        Birden çok Configuration Manager hiyerarşisini aynı masaüstü Analizi örneğine bağladığınızda, hiyerarşinin görünen adı genel pilot yapılandırmasındaki koleksiyon adına ön ekler. Bu ad, Configuration Manager konsolundaki masaüstü Analizi bağlantısında **görünen ad** özelliğidir.<!-- 4814075 -->

        > [!NOTE]
        > Birden çok hiyerarşi için destek, Configuration Manager sürüm 1910 veya üstünü gerektirir.
        >
        > Birden çok hiyerarşi için Koleksiyonlar ' ı seçerseniz, Portal bir uyarı görüntüler. Birden çok hiyerarşiyle Koleksiyonlar içeren dağıtım planı oluşturamazsınız.<!-- 4814075 -->

    - **Hazırlık kuralları**: Bu kurallar, hangi cihazların yükseltme için uygun olduğunu belirlemenize yardımcı olur. Daha fazla bilgi için bkz. [hazırlık kuralları](#readiness-rules).  

    - **Tamamlanma tarihi**: Windows 'un hedeflenen tüm cihazlara tam olarak dağıtılması gereken tarihi seçin.  

5. **Oluştur**’u seçin. Yeni plan, işlendiği sırada dağıtım planları listesinde görünür. İşleme hızlandırmak için isteğe bağlı veri yenileme isteyin. Daha fazla bilgi için bkz. [Masaüstü analizi hakkında SSS](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Dağıtım planını, adını seçerek açın.  

7. Dağıtım planı menüsünde, **hazırla** grubunda, **önemi tanımla**' yı seçin.  

    1. **Uygulamalar** sekmesinde, yalnızca **Gözden geçirilmeyen** varlıkları göstermek için seçin.  

    2. Her uygulamayı seçip **Düzenle**' yi seçin. Aynı anda düzenlemek için birden çok uygulama seçebilirsiniz.  

    3. **Önem** listesinden bir önem düzeyi seçin. Pilot sırasında Masaüstü analizinin uygulamayı doğrulamasını istiyorsanız, **kritik** veya **önemli**seçeneğini belirleyin. **Önemli değil**olarak işaretlenen uygulamaları doğrulamaz. Önem düzeyi atarken [uyumluluğunu](compat-assessment.md) ve diğer plan öngörülerini değerlendirin.  

        Önem düzeyleri atarken, yükseltme kararlarını da seçebilirsiniz.  

    4. Tamamlandığında **Kaydet** ' i seçin.  

8. Dağıtım planı menüsünde, **hazırla** grubunda, **pilot 'u tanımla**' yı seçin.  

    1. Pilot için önerilen cihazları gözden geçirin.  

    2. Her bir cihazı seçin ve **pilot 'A Ekle**' yi seçin. Öneriyi kabul etmiyorsanız, **Değiştir**' i seçin.  

        Masaüstü analizinin bu önerileri nasıl yaptığı hakkında daha fazla bilgi için, **pilot bölmesini belirleme** bölmesinin sağ üst köşesindeki bilgi simgesini seçin.

## <a name="readiness-rules"></a>Hazırlık kuralları

Bu kurallar, hangi cihazların yerinde yükseltme için uygun olduğunu belirlemenize yardımcı olur. Dağıtım planı oluştururken bu kuralları ayarlayabilir veya daha sonra düzenleyebilirsiniz.

Hazırlık kurallarını değiştirmek için:

1. Masaüstü Analizi portalında dağıtım planı ' nı seçin.
1. Adın yanındaki **Düzenle**' yi seçin.
1. **Hazırlık kuralları**' nı seçin.
1. **Windows işletim sistemi**' ni seçin.
1. Gerekli değişiklikleri yapın ve **Kaydet**' i seçin.

**Windows işletim sistemi** yükseltmeleri için iki kural mevcuttur: cihaz sürücüleri ve Windows uygulamaları.

### <a name="device-drivers"></a>Aygıt sürücüleri

Cihazlarınızın Windows Update sürücüleri almasını yapılandırın. Bu değer varsayılan olarak **kapalıdır** . Sürücüler dahil güncelleştirmeleri yönetmek üzere Iş için Windows Update kullandığınızda bu kuralı etkinleştirin. Yazılım güncelleştirmelerini yönetmek için Configuration Manager kullanıyorsanız, bu kuralı **kapalı**olarak ayarlayın.

### <a name="windows-applications"></a>Windows uygulamaları

Masaüstü analizinin en önemli olarak göstereceği uygulamalar, düşük yüklemesi sayısı eşiğini *temel alır.* Dağıtım planının hazırlık kurallarında bu eşiği ayarlayın. Varsayılan olarak, bu eşik **% 2,0**' dir. Değerini `0.0` olarak `10.0`değiştirebilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar

Pilot cihazlara dağıtım için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]  
> [Pilota dağıtma](deploy-pilot.md)  
