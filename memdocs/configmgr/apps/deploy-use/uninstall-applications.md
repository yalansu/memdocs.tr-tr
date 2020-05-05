---
title: Uygulama kaldırma
titleSuffix: Configuration Manager
description: Configuration Manager kullanarak bir uygulamayı kaldırma
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075855"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Configuration Manager ile uygulamaları kaldırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Daha önce dağıttığınız bir uygulamayı kaldırmak için aşağıdaki işlemleri gerçekleştirin.

-   Dağıtım türü oluşturma Sihirbazı ' nın **içerik** sayfasında dağıtım türü içeriğini kaldırmak için komut satırını belirtin.  

-   **Kaldır**dağıtım eylemini kullanarak uygulamayı dağıtın.  

> [!IMPORTANT]  
> Bazı uygulama türleri kaldırmayı desteklemez.  

 Bu liste, uygulama kaldırma işlemlerinin nasıl çalıştığı hakkında daha fazla bilgi sağlar:  

-   Bir Configuration Manager (Configuration Manager) uygulamasını kaldırdığınızda, tüm bağımlı uygulamalar otomatik olarak kaldırılmaz.  

-   Bir kullanıcı için **Kaldır** eylemini kullanan bir uygulamayı dağıtırsanız ve uygulama bilgisayarın tüm kullanıcıları için yüklendiyse, kullanıcının hesabının uygulamayı kaldırma izni yoksa kaldırma işlemi başarısız olabilir.  

-   Kendisine dağıtılan bir uygulamayı içeren bir koleksiyondan bir kullanıcıyı veya cihazı kaldırırsanız, uygulama cihazdan otomatik olarak kaldırılmaz.  

-   **Kaldır** dağıtım amacı olan bir dağıtım, gereksinim kurallarını denetlemez. Uygulama dağıtımın çalıştırıldığı bilgisayarda yüklü ise kaldırılacaktır.  

> [!IMPORTANT]  
> Uygulamayı kaldırma eylemiyle birlikte dağıtmak için, önce mevcut uygulama dağıtımlarını, sanal dağıtımların veya bu uygulamayı içeren görev dizisi dağıtımlarını silmeniz gerekir. 

 Dağıtım türü oluşturma hakkında daha fazla bilgi için bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md).  

 Bir uygulamanın nasıl dağıtılacağı hakkında daha fazla bilgi için bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Bir uygulamayı kaldırma  

1.  Aşağıdaki yöntemlerden birini kullanarak kaldırma komut satırı ile uygulama dağıtım türünü yapılandırın.  

    -   Dağıtım oluşturma Sihirbazı ' nın **genel** sayfasında, **Bu dağıtım türü hakkındaki bilgileri yükleme dosyalarından otomatik olarak tanımla**seçeneğini seçin. Bilgiler yükleme dosyalarında mevcutsa kaldırma komut satırı otomatik olarak dağıtım türü özelliklerine eklenir.  

    -   Dağıtım türü oluşturma Sihirbazı ' nın **içerik** sayfasında, **Program kaldır** alanında, uygulamayı kaldırmak için komut satırını belirtin.  

        > [!NOTE]  
        >  **İçerik** sayfası yalnızca dağıtım türü Oluştur sihirbazının **genel** sayfasındaki **dağıtım türü bilgilerini el ile belirt** seçeneğini belirlediğinizde görüntülenir.  

    -   ** < *Dağıtım türü adı*> Özellikler** iletişim kutusunun **Programlar** sekmesinde, uygulamayı **kaldırma programı** alanından kaldırmak için komut satırını belirtin.  

2.  Uygulamayı dağıtın ve ardından yazılım dağıtma sihirbazının **dağıtım ayarları** sayfasında **Kaldır** dağıtım eylemini seçin.  

    > [!NOTE]  
    >  **Kaldır**dağıtım eylemini seçtiğinizde otomatik olarak dağıtım amacı **Gerekli**olarak yapılandırılır.  
