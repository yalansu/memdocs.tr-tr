---
title: Test istemci yükseltmeleri ön üretim koleksiyonu
titleSuffix: Configuration Manager
description: Configuration Manager içindeki bir ön üretim koleksiyonundaki istemci yükseltmelerini test edin.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715413"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Configuration Manager içindeki bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sitenin geri kalanını yükseltmeden önce yeni bir Configuration Manager istemci sürümünü bir ön üretim koleksiyonunda test edebilirsiniz.  Bunu yaptığınızda, yalnızca test koleksiyonunun parçası olan cihazlar yükseltilir. İstemciyi test etme şansınız olduktan sonra istemciyi yükselterek istemci yazılımının yeni sürümünün sitenin geri kalanı için kullanılabilir olmasını sağlayabilirsiniz.

> [!NOTE]
> Bir test istemcisini üretime yükseltmek için, **tam yönetici** güvenlik rolüne ve **tümünün**güvenlik kapsamına sahip bir kullanıcı olarak oturum açmış olmanız gerekir. Daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../../../understand/fundamentals-of-role-based-administration.md). Ayrıca, merkezi yönetim sitesine veya en üst düzey tek başına birincil siteye bağlı bir sunucuda oturum açmanız gerekir.

 İstemcileri ön üretimde test etmek için 3 temel adım vardır.  

1.  Otomatik istemci yükseltmelerini bir ön üretim koleksiyonu kullanacak şekilde yapılandırın.  

2.  İstemcinin yeni bir sürümünü içeren Configuration Manager bir güncelleştirme yükler.  

3.  Yeni istemciyi üretime yükseltin.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Otomatik istemci yükseltmelerini bir ön üretim koleksiyonu kullanacak şekilde yapılandırmak için  
> [!IMPORTANT]
> Ön üretim istemci dağıtımı, çalışma grubu bilgisayarları için desteklenmez. Dağıtım noktasının ön üretim istemci paketine erişmesi için gereken kimlik doğrulamasını kullanamaz.  Üretim istemcisi olarak yükseltildiğinde, en son istemciyi alırlar.

1. Ön üretim istemcisini dağıtmak istediğiniz bilgisayarları içeren [bir koleksiyon ayarlayın](../collections/create-collections.md) .   

2. Configuration Manager konsolunda **Yönetim** > **sitesi yapılandırma** > **siteleri**' ni açın ve **Hiyerarşi ayarları**' nı seçin.  

    **Hiyerarşi Ayarları Özellikleri** ’nin **İstemci Yükseltme**sekmesinde:  

   -   **Ön üretim koleksiyonundaki tüm istemcileri ön üretim istemcisi kullanarak otomatik olarak yükselt**’i seçin.  

   -   Ön üretim koleksiyonu olarak kullanılacak koleksiyonun adını girin  

![Test istemci yükseltmeleri](media/test-client-upgrades.png)

>[!NOTE]
>Bu ayarları değiştirmek için, hesabınız **tam yönetici** güvenlik rolünün bir üyesi ve **Tüm** güvenlik kapsamı olmalıdır.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>İstemcinin yeni bir sürümünü içeren bir Configuration Manager güncelleştirmesi yüklemek için  

1.  Configuration Manager konsolunda, **Yönetim** > **güncelleştirmeleri ve bakımı**' nı açın, **kullanılabilir** bir güncelleştirme seçin ve **güncelleştirme paketini yükler**' i seçin. (Sürüm 1702 ' den önce, güncelleştirmeler ve bakım, **Yönetim** > **Cloud Services**altındadır.)

     Güncelleştirmeleri yükleme hakkında daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../../../../core/servers/manage/updates.md)  

2.  Güncelleştirmenin yüklenmesi sırasında, sihirbazın **Istemci seçenekleri** sayfasında, **ön üretim koleksiyonunda test**' i seçin.  

3.  Sihirbazın geri kalanını tamamlayın ve güncelleştirme paketini yükleyin.  

     Sihirbaz tamamlandığında, ön üretim koleksiyonundaki istemciler güncelleştirilmiş istemciyi dağıtmaya başlar. **İzleme** > **istemci durumu** > **ön üretim istemci dağıtımı**' na giderek, yükseltilmiş istemcilerin dağıtımını izleyebilirsiniz. Daha fazla bilgi için bkz. [istemci dağıtım durumunu izleme](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Bir ön üretim koleksiyonundaki site sistem rollerini barındıran bilgisayarlardaki dağıtım durumu, istemci başarıyla dağıtıldığında bile **uyumlu değil** olarak bildirilebilir. İstemciyi üretime yükselttiğinizde dağıtım durumu doğru şekilde bildirilir.

##  <a name="to-promote-the-new-client-to-production"></a>Yeni istemciyi üretime yükseltmek için  

1.  Configuration Manager konsolunda, **Yönetim** > **güncelleştirmeleri ve bakımı**' nı açın ve **ön üretim istemcisini Yükselt**' i seçin. (Sürüm 1702 ' den önce, güncelleştirmeler ve bakım, **Yönetim** > **Cloud Services**altındadır.)

    > [!TIP]
    > **Ön Üretim İstemcisini Yükselt** düğmesi, konsoldaki **İzleme** > **İstemci Durumu** > **Ön Üretim İstemci Dağıtımı**’nda istemci dağıtımlarını izlerken de kullanılabilir.

2.  Üretim ve üretim öncesi istemci sürümlerini gözden geçirin, doğru ön üretim koleksiyonunun belirtildiğinden emin olun ve ardından **Yükselt**' e ve ardından **Evet**' e tıklayın.  

3.  İletişim kutusu kapatıldıktan sonra, güncelleştirilmiş istemci sürümü, hiyerarşinizde kullanımda olan istemci sürümünün yerini alır. Daha sonra tüm sitenizin istemcilerini yükseltebilirsiniz. Daha fazla bilgi için bkz. [Windows bilgisayarlar için istemcileri yükseltme](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) .  

>[!NOTE]
>Ön üretim istemcisini etkinleştirmek veya ön üretim istemcisini üretim istemcisine yükseltmek için, hesabınız **güncelleştirme paketleri** nesnesi için **okuma** ve **değiştirme** izinlerine sahip bir güvenlik rolünün üyesi olmalıdır.
>İstemci yükseltmeleri, yapılandırdığınız tüm Configuration Manager bakım pencerelerini dikkate almaz.
