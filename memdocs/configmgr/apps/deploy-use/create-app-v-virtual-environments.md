---
title: App-V sanal ortamları oluşturma
titleSuffix: Configuration Manager
description: Uygulamaların birbirleriyle veri paylaşabilmesi için Microsoft Application Virtualization ile sanal ortamlar oluşturun.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2280218d3d237f91f0db3150dbc2031bad3e1816
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710422"
---
# <a name="create-app-v-virtual-environments-in-configuration-manager"></a>Configuration Manager 'de App-V sanal ortamları oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bir Microsoft Application Virtualization (App-V) sanal ortamında, dağıtılan sanal uygulamalar, istemci Windows bilgisayarlarda aynı dosya sistemini ve kayıt defterini paylaşabilir. Standart sanal uygulamalardan farklı olarak, bu uygulamalar birbiriyle veri paylaşabilir. Sanal ortamlar, uygulama yüklendiğinde veya istemciler yüklü uygulamalarını değerlendirdikten sonra istemci bilgisayarlarda oluşturulur veya değiştirilir. Birden çok uygulama aynı dosya sistemi veya kayıt defteri değerlerini değiştirdiğinde, en üst sıradaki uygulama öncelikli olacak şekilde bu uygulamaları sıralayabilirsiniz.  

> [!IMPORTANT]  
>  Kötü amaçlı yazılımdan koruma sağlamak için App-V sanal ortamlarına güvenmeyin.  

 Configuration Manager bir App-V sanal ortamı oluşturmak için aşağıdaki yordamı kullanın.  

## <a name="create-an-app-v-virtual-environment"></a>App-V sanal ortamı oluşturma  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **App-V sanal ortamları**' nı seçin.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **sanal ortam oluştur**' u seçin.  

4.  **Sanal ortam oluştur** iletişim kutusunda aşağıdaki bilgileri girin:  

    -   **Ad**.  Sanal ortam için benzersiz bir ad girin (en fazla 128 karakter).  

    -   **Açıklama**. Seçim Sanal ortam için bir açıklama girin.  

5.  Sanal ortama yeni bir dağıtım türü eklemek için **Ekle**' yi seçin. En az bir dağıtım türü eklemelisiniz.  

6.  **Uygulama Ekle** iletişim kutusunda bir **Grup adı** belirtin (en fazla 128 karakter). Bu adı, sanal ortama eklediğiniz uygulama grubuna başvurmak için kullanacaksınız.  

7.  **Ekle**' yi seçin, gruba eklemek istediğiniz App-V 5 uygulamalarını ve dağıtım türlerini seçin ve ardından **Tamam**' ı seçin.  

8.  Birden çok uygulama aynı sanal ortamdaki dosya sistemi veya kayıt defteri ayarlarını değiştirmeyi denediklerinde, uygulama **Ekle** iletişim kutusunda, öncelik alan uygulamayı ayarlamak Için **sırayı artır** veya **sırayı azalt** ' ı seçebilirsiniz.  

9. **Sanal ortam oluştur** iletişim kutusuna geri dönmek için **Tamam**' ı seçin.  

10. Grupları eklemeyi tamamladığınızda, sanal ortamı oluşturmak için **Tamam** ' ı seçin. Yeni sanal ortam, Configuration Manager konsolunun **App-V sanal ortamları** düğümünde görüntülenir. App-V sanal ortam durumu raporunu kullanarak sanal ortamlarınızın durumunu izleyebilirsiniz.  

    > [!NOTE]  
    >  Sanal ortam, uygulama yüklendiğinde veya istemcinin yüklü uygulamaları bir sonraki değerlendirmesinde istemci bilgisayarlara eklenir veya değiştirilir.  
