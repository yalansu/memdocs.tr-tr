---
title: Uygulamaları güncelleştirme ve devre dışı bırakma
titleSuffix: Configuration Manager
description: Configuration Manager kullanarak dağıtılan uygulamaları düzeltin, yenisiyle değiştirin veya kaldırın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7770f1db0e311186a908890dc339401ed3cbeb4b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710534"
---
# <a name="update-and-retire-applications-with-configuration-manager"></a>Configuration Manager ile uygulamaları güncelleştirme ve devre dışı bırakma

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Sonuç olarak, bir uygulamada değişiklikler yapmak, uygulamayı kaldırmak veya zaten dağıtılan bir uygulamayı yeni bir uygulamayla değiştirmek isteyebilirsiniz. Configuration Manager, uygulamaları güncelleştirmenize ve devre dışı getirmenize yardımcı olmak için size bu olanakları sağlar:  

- **Uygulamaları gözden geçirin**. Bir uygulama veya dağıtım türünde değişiklikler yaptığınızda Configuration Manager değişikliklerin geçmişini tutar. Uygulamayı dilediğiniz zaman önceki bir düzeltmeye geri alabilirsiniz. Ayrıca, özelliklerini görüntüleyebilir, bir uygulamanın önceki bir düzeltmesini geri yükleyebilir veya eski bir düzeltmeyi silebilirsiniz.  

  Daha fazla bilgi için bkz. [uygulama düzeltmeleri](revise-and-supersede-applications.md#application-revisions).  

- **Uygulamaları yenisiyle değiştirme**. Bir yerine geçme ilişkisi kullanarak mevcut uygulamaları yükseltebilir ya da değiştirebilirsiniz. Bir uygulamayı yenisiyle değiştirdiğinizde, yerine geçilen uygulamanın dağıtım türünü değiştirmek için yeni bir dağıtım türü belirtebilirsiniz. Ayrıca, yerine geçen uygulama yüklenmeden önce yerine geçilen uygulamayı yükseltmeyi veya kaldırmayı belirleyebilirsiniz.  

  Daha fazla bilgi için bkz. [uygulama yerine geçme](revise-and-supersede-applications.md#application-supersedence).  

- **Uygulamaları kaldırın**. Configuration Manager bir uygulamayı kolay bir şekilde kaldırmayı kolaylaştırır. Bu, uygulama veya cihaz kullanıcısının müdahalesi olmadan sessizce gerçekleştirilebilir.  

  Daha fazla bilgi için bkz. [uygulamaları kaldırma](uninstall-applications.md).  
