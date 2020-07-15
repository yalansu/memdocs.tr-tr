---
title: İstemci durumunu yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager istemci durumu ayarlarını seçin.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384919"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Configuration Manager istemci durumunu yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcileri izleyebilmeniz ve sorunları düzeltebilmeniz için önce, sitenin istemci durumu ayarlarını yapılandırın. Bu ayarlar, sitenin istemcileri devre dışı olarak işaretlemek için kullandığı parametreleri belirtir. Ayrıca, istemci etkinliği belirtilen eşiğin altına düştüğünde sizi uyarmak için seçenekleri yapılandırın.

## <a name="configure-client-status"></a>İstemci durumunu yapılandırma

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **istemci durumu** düğümünü seçin. Şeridin **giriş** sekmesinde, **Istemci durumu** grubunda **istemci durumu ayarları**' nı seçin.

1. Aşağıdaki ayarları yapılandırın:

    > [!NOTE]
    > Bir istemci ayarlardan hiçbirini karşılamıyorsa, site onu etkin değil olarak işaretler.

    - **Şu günlerde istemci ilkesi istekleri:** İstemcinin siteden ilke istemesinden itibaren geçen gün sayısını belirtin. Varsayılan değer gün değeridir `7` .

      Bu değeri, istemci ayarları istemci **ilkesi** grubundaki istemci **ilkesi yoklama aralığı** ayarıyla karşılaştırın. Varsayılan değer 60 dakikadır. Diğer bir deyişle, bir istemci her saat ilke için siteyi yoklamalıdır. Bir hafta sonra ilke istemezse, site onu etkin değil olarak işaretler.

    - **Şu günlerde sinyal bulma:** İstemcinin siteye bir sinyal bulma kaydı göndermesinden itibaren geçen gün sayısını belirtin. Varsayılan değer gün değeridir `7` .

      Bu değeri [sinyal bulma yöntemi](../../servers/deploy/configure/about-discovery-methods.md)için zamanlama ile karşılaştırın. Varsayılan olarak, site sinyal bulmayı haftada bir kez çalıştırır.

    - **Şu günlerde donanım envanteri:** İstemcinin siteye bir donanım envanteri kaydı gönderdikten itibaren geçen gün sayısını belirtin. Varsayılan değer gün değeridir `7` .

      Bu değeri, istemci ayarlarının **donanım envanteri** grubundaki **donanım envanteri zamanlama** ayarıyla karşılaştırın. Varsayılan değer yedi gündür.

    - **Şu günlerde yazılım envanteri:** İstemcinin siteye bir yazılım envanter kaydı göndermesinden itibaren geçen gün sayısını belirtin. Varsayılan değer gün değeridir `7` .

      Bu değeri, istemci ayarlarının **yazılım envanteri** grubundaki **yazılım envanterini ve dosya toplamayı zamanla** ayarı ile karşılaştırın. Varsayılan değer yedi gündür.

    - **Şu günlerde durum iletileri:** İstemci, siteye herhangi bir durum iletisi gönderdikten bu yana geçen gün sayısını belirtin. Varsayılan değer gün değeridir `7` . İstemci, görev dizisi çalıştırma gibi farklı türlerde etkinliklere yönelik durum iletileri gönderebilir. Site, eski durum iletilerini bakım görevinin bir parçası olarak siler, **eski durum iletilerini**siler.

1. Sitenin istemci durum geçmişi verilerini ne kadar süreyle tutacağını belirlemek için aşağıdaki değeri belirtin:

    - **İstemci durum geçmişini Şu sayıda gün boyunca sakla:** Varsayılan olarak, site istemci durum bilgilerini gün boyunca tutar `31` . Bu ayarın, istemci veya site davranışı üzerinde herhangi bir etkisi yoktur. İstemci durumu geçmişi için bir bakım göreviyle benzerdir.

## <a name="configure-the-schedule"></a>Zamanlamayı yapılandırma

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **istemci durumu** düğümünü seçin. Şeridin **giriş** sekmesinde, **istemci durumu** grubunda, **istemci durumu güncelleştirmesini zamanla**' yı seçin.

1. İstemci durumunun güncelleştirilmesini istediğiniz aralığı yapılandırın.

    > [!NOTE]
    > İstemci durumu güncelleştirmeleri için zamanlamayı değiştirdiğinizde, önceki zamanlamaya göre bir sonraki zamanlanmış istemci durumu güncelleştirmesine kadar etkili olmaz.

## <a name="configure-alerts"></a>Uyarı yapılandırma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin.

1. Uyarılarını yapılandırmak istediğiniz koleksiyonu seçin. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.

    > [!NOTE]
    > Kullanıcı koleksiyonları için uyarıları yapılandıramazsınız.

1. **Uyarılar** sekmesine geçin ve **Ekle**' yi seçin.

   > [!TIP]
   > Yalnızca güvenlik rolünüzün uyarılar için izinleri varsa **Uyarılar** sekmesini görüntüleyebilirsiniz.

    Sitenin istemci durum eşikleri için oluşturmasını istediğiniz uyarıları seçin ve **Tamam**' ı seçin.

1. **Uyarılar** sekmesinin **koşullar** listesinde, her bir istemci durum uyarısını seçin ve ardından aşağıdaki bilgileri belirtin:

    - **Uyarı adı**: varsayılan adı kabul edin veya uyarı için yeni bir ad girin.

    - **Uyarı önem derecesi**: Configuration Manager konsolunun görüntülediği uyarı düzeyini seçin.

    - **Uyarı oluştur**: uyarı için eşik yüzdesini belirtin.

## <a name="automatic-remediation-exclusion"></a>Otomatik Düzeltme dışlaması

1. Otomatik düzeltmeyi devre dışı bırakmak istediğiniz istemci bilgisayarda, kayıt defteri düzenleyicisini açın.

    > [!WARNING]
    > Kayıt Defteri Düzenleyicisi 'ni yanlış kullanırsanız, Windows 'u yeniden yüklemenizi gerektirebilecek önemli sorunlara neden olabilirsiniz. Microsoft, kayıt defteri Düzenleyicisi 'nin yanlış kullanılması sonucunda oluşan sorunları çözebileceğinizi garanti edemez. Bunu sizin sorumluluğunuzdadır.

1. **HKEY_LOCAL_MACHINE \Software\Microsoft\CCM\CcmEval**kayıt defteri anahtarına gidin.

1. **Yalnızca notifyentry** için değeri değiştirin:

    - `TRUE`: İstemci bulduğu sorunları otomatik olarak düzelmez. Site yine de bu istemciyle ilgili sorunlar hakkında **izleme** çalışma alanında size bildirimde bulunur.

    - `FALSE`: Bu ayar varsayılandır. İstemci sorunları bulduğunda sorunları otomatik olarak düzeltir ve site sizi **izleme** çalışma alanında bilgilendirir.

İstemcileri yüklediğinizde, onları otomatik düzeltmeden, **yalnızca notifyonly** yükleme özelliğiyle hariç bırakabilirsiniz. Daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](about-client-installation-properties.md).

## <a name="next-steps"></a>Sonraki adımlar

[İstemcileri izleme](../manage/monitor-clients.md)
