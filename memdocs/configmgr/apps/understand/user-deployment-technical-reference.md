---
title: Kullanıcılara uygulama dağıtımı teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager için uygulama dağıtımlarının kullanıcılara yönelik teknik başvuru sorunlarını giderme.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710800"
---
# <a name="application-deployment-policy-for-users"></a>Kullanıcılar için uygulama dağıtım Ilkesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir uygulama bir kullanıcı koleksiyonuna dağıtıldığında, dağıtımın ilkesi yalnızca gerekli dağıtımlar için oluşturulur. Kullanılabilir dağıtımlar için, Kullanıcı uygulamayı yazılım merkezinden yüklemeyi denediğinde ilke oluşturulur. Bu makalede, gereken dağıtım ve kullanılabilir dağıtımlar için dağıtım süreci açıklanacaktır.

> [!TIP]
> İstemci günlüklerini gözden geçirmek için gereken tüm bilgiler, [başlamadan önce](app-deployment-technical-reference.md#before-you-begin) bölümünde başvurulan SQL sorgusu çalıştırılarak elde edilebilir.

## <a name="required-deployments"></a>Gerekli dağıtımlar

Bir kullanıcı koleksiyonuna gerekli bir uygulama dağıtımının ilkesi, dağıtım oluşturulduğunda koleksiyondaki tüm kullanıcılara yöneliktir. Bu dağıtımlar için istemci tarafı işleme, bir cihaz koleksiyonuna gereken dağıtıma benzer. Dağıtım etkinleştirme tanımlı kullanılabilir zamanda gerçekleşir ve uygulama tanımlanan son tarihte gerçekleşir. Daha fazla bilgi için bkz. [cihaz koleksiyonlarına uygulama dağıtımı](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Kullanılabilir dağıtımlar

Kullanılabilir olarak bir kullanıcı koleksiyonuna dağıtılan uygulamalar farklı davranır. Bu davranış değişikliği, yöneticinin ilke için kaynak çekişmesine neden olmadan uygulamaları kullanıcılara kullanabilmesini sağlar. Bir kullanıcı yazılım merkezini başlattığında, Kullanıcı için kullanılabilen uygulamaların bir listesi, yönetim noktasından gerçek zamanlı olarak sorgulanır. Bu istek yönetim noktasındaki `CMUserService_WindowsAuth` sanal dizine yapılır ve istemci üzerindeki **SCClient_ [UserName]. log** dosyasında görünebilirler.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Yönetim noktası bu isteği aldığında, saklı yordamı yürüterek `usp_GetApplicationPropertyValuesFiltered` Kullanıcı tarafından kullanılabilen uygulamaların listesini sorgular. Bu etkinlik yönetim noktasındaki **Userservice. log** dosyasında izlenebilir.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Yazılım Merkezi listeyi alır ve kullanıcının yükleyebileceği uygulamaları görüntüler. Kullanıcı uygulamaya tıkladığında, uygulama hakkındaki ek bilgiler, usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp vb. gibi saklı yordamların yürütülmesini içeren yönetim noktasından sorgulanır.

Kullanıcı uygulamayı seçip **Install** düğmesine tıkladığında dağıtım etkinleştirilir ve uygulamayı değerlendirmek IÇIN bir DCM Aracısı işi oluşturulur. Uygulama geçerliyse, uygulamayı indirmek ve zorlamak için başka bir DCM Aracısı Işi oluşturulur. Bu etkinlik, istemcideki **Dcmagent. log** dosyasında izlenebilir.

## <a name="next-steps"></a>Sonraki Adımlar

- [Uygulama dağıtımı istemci bileşenlerini anlama](client-components-technical-reference.md)
