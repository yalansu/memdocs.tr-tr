---
title: Endpoint Protection uyarılarını yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager Endpoint Protection uyarılarını yapılandırmayı öğrenin.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074869"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager Endpoint Protection uyarılarını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Bir kötü amaçlı yazılım bulaşma gibi belirli olaylar hiyerarşinizde oluştuğunda yönetim kullanıcılarını bilgilendirmek için Microsoft Configuration Manager 'de Endpoint Protection uyarılarını yapılandırabilirsiniz. Bildirimler, **izleme** çalışma alanının **Uyarılar** düğümündeki Configuration Manager konsolundaki Endpoint Protection panosunda görüntülenir veya belirtilen kullanıcılara e-posta ile gönderilebilir.

 Configuration Manager Endpoint Protection uyarılarını yapılandırmak için bu konudaki aşağıdaki adımları ve ek yordamları kullanın.

> [!IMPORTANT]
>  Endpoint Protection uyarılarını yapılandırmak için Koleksiyonlar için **güvenliği zorla** iznine sahip olmanız gerekir.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager Endpoint Protection uyarılarını yapılandırma adımları

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.

2.  **Varlıklar ve Uyum** çalışma alanında, **Aygıt Koleksiyonları**'nı tıklatın.

3.  **Cihaz Koleksiyonları** listesinde uyarıları yapılandırmak istediğiniz koleksiyonu seçin ve sonra **Giriş** sekmesindeki **Özellikler** grubunda **Özellikler**'e tıklayın.

    > [!NOTE]
    >  Kullanıcı koleksiyonları için uyarılar yapılandıramasınız.

4.  _<koleksiyonu adı\> _ **Özellikler** iletişim kutusunun **Uyarılar** sekmesinde, bu koleksiyonun kötü amaçlı yazılımdan koruma işlemlerine ilişkin ayrıntıları Configuration Manager konsolunun **izleme** çalışma alanında görüntülemek istiyorsanız, **Endpoint Protection panosunda bu koleksiyonu görüntüle** ' yi seçin.

    > [!NOTE]
    >  Bu seçenek **Tüm Sistemler** koleksiyonu için kullanılamaz.

5.  _<koleksiyonu adı\> _ **Özellikler** iletişim kutusunun **Uyarılar** sekmesinde **Ekle**' ye tıklayın.

6.  **Yeni koleksiyon uyarıları Ekle** iletişim kutusundaki **Bu koşullar geçerli olduğunda uyarı oluştur** bölümünde, belirtilen Endpoint Protection olayları gerçekleştiğinde Configuration Manager oluşturmasını istediğiniz uyarıları seçin ve ardından **Tamam**' a tıklayın.

7.  **Uyarılar** sekmesinin **koşullar** listesinde her bir Endpoint Protection uyarıyı seçin ve ardından aşağıdaki bilgileri belirtin:

    -   **Uyarı adı** -varsayılan adı kabul edin veya uyarı için yeni bir ad girin.

    -   **Uyarı önem derecesi** -listede, Configuration Manager konsolunda görüntülenecek uyarı düzeyini seçin.

8.  Seçtiğiniz uyarıya bağlı olarak, aşağıdaki ek bilgileri belirtin:

    -   **Kötü amaçlı yazılım algılama** -izlediğiniz koleksiyondaki herhangi bir bilgisayarda kötü amaçlı yazılım algılanırsa bu uyarı oluşturulur. **Kötü amaçlı yazılım algılama eşiği** , bu uyarının oluşturulduğu kötü amaçlı yazılım algılama düzeylerini belirtir:

        -   **Yüksek-tüm algılamalar** -Endpoint Protection istemcisinin hangi eylemde olduğuna bakılmaksızın, belirtilen koleksiyonda herhangi bir kötü amaçlı yazılımın algılandığı bir veya daha fazla bilgisayar olduğunda bu uyarı oluşturulur.

        -   **Orta algılanan, bekleyen eylem** -kötü amaçlı yazılımın algılandığı belirtilen koleksiyonda bir veya daha fazla bilgisayar olduğunda uyarı oluşturulur ve kötü amaçlı yazılımı el ile kaldırmanız gerekir.

        -   **Düşük algılanan, hala etkin** -kötü amaçlı yazılımın algılandığı ve hala etkin olduğu belirtilen koleksiyonda bir veya daha fazla bilgisayar olduğunda bu uyarı oluşturulur.

    -   **Kötü amaçlı yazılım kesmesi** -bu uyarı, izlediğiniz koleksiyonda belirtilen bir bilgisayar yüzdesinde belirtilen kötü amaçlı yazılım algılanırsa oluşturulur.

        -   **Kötü amaçlı yazılım algılanan bilgisayarların yüzdesi** -koleksiyonda algılanan kötü amaçlı yazılım olan bilgisayarların yüzdesi belirttiğiniz yüzdeyi aştığında uyarı oluşturulur. **1** ile **99**arasında bir yüzde belirtin.

            > [!NOTE]
            >  Yüzde değeri koleksiyondaki bilgisayar sayısına bağlıdır, ancak Configuration Manager istemcisinin yüklü olmadığı bilgisayarları dışlar. Endpoint Protection istemcisinin henüz yüklenmediği bilgisayarları içerir.

    -   **Yinelenen kötü amaçlı yazılım algılama** -bu uyarı, belirli bir kötü amaçlı yazılımın izlediğiniz koleksiyondaki bilgisayarlarda belirtilen sayıda saat boyunca belirli sayıda kez algılanırsa oluşturulur. Bu uyarıyı yapılandırmak için aşağıdaki bilgileri belirtin:

        -   **Kötü amaçlı yazılımın algılanma sayısı:** - Aynı kötü amaçlı yazılım, koleksiyondaki bilgisayarlarda belirtilenden fazla sayıda algılandığında bu uyarı oluşturulur. **2** ile **32**arasında bir sayı belirtin.

        -   **Algılama aralığı (saat):** Kötü amaçlı yazılım algılamaları oluşması gereken algılama aralığını (saat cinsinden) belirtin. **1** ile **168**arasında bir sayı belirtin.

    -   **Birden çok kötü amaçlı yazılım algılama** -bu uyarı, izlediğiniz koleksiyondaki bilgisayarlarda belirtilen sayıda kötü amaçlı yazılım türü algılanırsa oluşur. Bu uyarıyı yapılandırmak için aşağıdaki bilgileri belirtin:

        -   **Algılanan kötü amaçlı yazılım türlerinin sayısı:** Koleksiyondaki bilgisayarlarda belirtilen sayıda farklı kötü amaçlı yazılım türü algılandığında uyarı oluşturulur. **2** ile **32**arasında bir sayı belirtin.

        -   **Algılama aralığı (saat):** Kötü amaçlı yazılım algılama sayısının oluşması gereken bir algılama aralığı (saat cinsinden) belirtin. **1** ile **168**arasında bir sayı belirtin.

9. _<koleksiyonu adı\> _ **Özellikler** iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.  

## <a name="alert-for-outdated-malware-client"></a>Güncel olmayan kötü amaçlı yazılım istemcisi için uyarı

Configuration Manager sürüm 1702 ' den başlayarak, Endpoint Protection istemcilerinin güncel olmamasını sağlamak için bir uyarı yapılandırabilirsiniz. Artık herhangi bir cihaz koleksiyonundan aşağıdaki özniteliklerin **kötü amaçlı yazılımdan koruma Istemci sürümü** ve **Endpoint Protection dağıtım durumu**için listeye sütun ekleyebilirsiniz. Örneğin, konsolunda **varlıklar ve uyum** > **genel bakış** > **Cihaz Koleksiyonları** > **Tüm masaüstleri ve sunucu istemcileri**' ne gidin. Sütun başlığına sağ tıklayın ve eklenecek sütunları seçin. Bir uyarıyı denetlemek için **izleme** çalışma alanındaki **uyarıları** görüntüleyin. Yönetilen istemcilerin %20 ' si bir kötü amaçlı yazılımdan koruma yazılımının süresi dolmuşsa, kötü amaçlı yazılımdan koruma istemcisi sürümü güncel değildir. Bu uyarı, **izleme** > **genel bakış** sekmesinde görünmez. Zaman aşımına uğradı istemcileri güncelleştirmek için kötü amaçlı yazılımdan koruma istemcileri için yazılım güncelleştirmelerini etkinleştirin.

Uyarının oluşturulduğu yüzdeyi yapılandırmak için, **izleme** > **uyarıları** > **tüm uyarılar**' ı genişletin, **kötü amaçlı yazılımdan koruma istemcileri güncel** değil ' e çift tıklayın ve **bir kötü amaçlı yazılımdan koruma istemcisinin güncel olmayan sürümüne sahip yönetilen istemcilerin yüzdesi seçeneğinden fazla olursa oluştur uyarısını** değiştirin.

> [!div class="button"]
> [Sonraki adım >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Geri >](endpoint-protection-site-role.md)
