---
title: Kötü amaçlı yazılım tanımları Endpoint Protection
titleSuffix: Configuration Manager
description: İstemci bilgisayarlarına tanım güncelleştirmeleri sunacak Configuration Manager yazılım güncelleştirmelerini yapılandırmayı öğrenin.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126073"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Tanım güncelleştirmeleri sunmak için Configuration Manager kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemci bilgisayarlara tanım güncelleştirmelerini otomatik olarak sunmak için Configuration Manager yazılım güncelleştirmelerini yapılandırabilirsiniz. Otomatik dağıtım kuralları oluşturmaya başlamadan önce Configuration Manager yazılım güncelleştirmelerini yapılandırdığınızdan emin olun. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerine giriş](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Bu yordam Endpoint Protection özeldir. Otomatik dağıtım kuralları hakkında daha fazla genel bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri**' ni genişletin ve ardından **Otomatik dağıtım kuralları**' nı seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **Otomatik dağıtım kuralı oluştur**' u seçin.

1. **Otomatik Dağıtım Kuralı Oluşturma Sihirbazı** 'nın **Genel**sayfasında aşağıdaki bilgileri belirtin:

    - **Ad**: Otomatik dağıtım kuralı için benzersiz bir ad belirtin.

    - **Koleksiyon**: tanım güncelleştirmelerini dağıtmak istediğiniz cihaz koleksiyonunu seçin.

        > [!NOTE]
        > Tanım güncelleştirmelerini bir kullanıcı koleksiyonuna dağıtamazsınız.

1. **Mevcut bir yazılım güncelleştirme grubuna ekle**' yi seçin.

1. **Bu kural çalıştırıldıktan sonra dağıtımı etkinleştir**' i seçin.

1. Sihirbazın **dağıtım ayarları** sayfasında, **ayrıntı düzeyi**için **yalnızca hata iletileri**' ni seçin.

    > [!NOTE]
    > **Yalnızca hata iletilerini**seçtiğinizde, tanım dağıtımının gönderdiği durum iletilerinin sayısını azaltır. Bu yapılandırma Configuration Manager sunucularındaki CPU işlemeyi azaltmaya yardımcı olur.

1. **Yazılım güncelleştirmeleri** sayfasında:

    1. **Sınıflandırmayı Güncelleştir** özellik filtresini seçin. **Arama ölçütleri** listesinde, **\>bulunacak öğeleri<** seçin.

        **Arama ölçütleri** penceresinde, **tanım güncelleştirmeleri**' ni seçin ve ardından **Tamam**' ı seçin.

    1. **Ürün** özelliği filtresini seçin. **Arama ölçütleri** listesinde, **\>bulunacak öğeleri<** seçin.

        **Arama ölçütleri** penceresinde, Windows 8.1 ve önceki sürümleri Için **System Center Endpoint Protection** , Windows 10 ve üzeri için **Windows Defender** ' ı seçin ve ardından **Tamam**' ı seçin.

    > [!NOTE]
    > İsteğe bağlı olarak, yenisiyle değiştirilen güncelleştirmeleri filtreleyebilirsiniz. **Yenisiyle değiştirilen** özellik filtresini seçin. **Arama ölçütleri** listesinde, **\>bulunacak öğeleri<** seçin. **Arama ölçütleri** penceresinde **Hayır**' ı seçin ve ardından **Tamam**' ı seçin.

1. Sihirbazın **değerlendirme zamanlaması** sayfasında, **herhangi bir yazılım güncelleştirme noktası eşitlemesinden sonra kuralı Çalıştır**' ı seçin.

1. Sihirbazın **Dağıtım Zamanlaması** sayfasında aşağıdaki ayarları yapılandırın:

    - **Saat temeli**: tüm istemcilerin en son tanımları aynı anda yüklemesini istiyorsanız **UTC**' yi seçin. Gerçek yükleme süresi iki saat içinde farklılık gösterecektir.

    - **Yazılım uygunluk saati**: Bu kuralın oluşturduğu dağıtım için uygun saati belirtin. Belirtilen saat, otomatik dağıtım kuralının çalıştırılmasından en az bir saat sonra olmalıdır. Bu yapılandırma, içeriğin dağıtım noktalarına çoğaltılması için yeterli zamana sahip olduğundan emin olmanızı sağlar. Bazı tanım güncelleştirmeleri ayrıca dağıtım noktalarına ulaşması daha uzun sürebilecek kötü amaçlı yazılımdan koruma altyapısı güncelleştirmeleri içerebilir.

    - **Yükleme son tarihi**: **Hemen**’i seçin.

        > [!NOTE]
        > Yazılım güncelleştirmesi son tarihleri iki saatlik bir döneme göre değişir. Bu davranış, tüm istemcilerin aynı anda bir güncelleştirme istememelerini engeller.

1. Sihirbazın **Kullanıcı deneyimi** sayfasında, **Kullanıcı bildirimleri**için, **Yazılım Merkezi 'nde ve tüm bildirimlerde Gizle**' yi seçin. Bu yapılandırmayla, tanım güncelleştirmeleri sessizce yüklenir.

1. Sihirbazın **dağıtım paketi** sayfasında, mevcut bir dağıtım paketi seçin veya yeni bir tane oluşturun.

    > [!NOTE]
    > Tanım güncelleştirmelerini, diğer yazılım güncelleştirmelerini içermeyen bir pakete yerleştirmeyi düşünün. Bu strateji, tanım güncelleştirme paketinin boyutunu küçük tutmaya ve dolayısıyla dağıtım noktalarına daha hızlı çoğaltılmasına imkan tanır.

1. Yeni bir dağıtım paketi oluşturursanız, sihirbazın **dağıtım noktaları** sayfasında bir veya daha fazla dağıtım noktası seçin. Site bu paketin içeriğini bu dağıtım noktalarına kopyalar.

1. **Yükleme konumu** sayfasında, **yazılım güncelleştirmelerini Internet 'ten indir**' i seçin.

1. **Dil seçimi** sayfasında, indirilecek güncelleştirmelerin her bir dil sürümünü seçin.

1. **Yükleme ayarları** sayfasında, gerekli yazılım güncelleştirmeleri indirme davranışını seçin.

1. Sihirbazı tamamlayın.

Configuration Manager konsolunun **Otomatik dağıtım kuralları** düğümünde yeni kuralı görüntülediğinizi doğrulayın.

> [!div class="nextstepaction"]
> [Kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md)
