---
title: Uygulama grupları oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager ' de tek bir dağıtım olarak Kullanıcı veya cihaz koleksiyonuna gönderebilmeniz için bir uygulama grubu oluşturun.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643126"
---
# <a name="create-application-groups"></a>Uygulama grupları oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3555907-->

Sürüm 1906 ' den başlayarak, bir kullanıcı veya cihaz koleksiyonuna tek bir dağıtım olarak gönderebilmeniz için bir uygulama grubu oluşturun. Uygulama grubu hakkında belirttiğiniz meta veriler yazılım merkezi 'nde tek bir varlık olarak görülür. Bu uygulamaları, istemcinin belirli bir sırada yüklemesi için Grup içindeki sıraya alabilirsiniz.

> [!Note]  
> Bu Configuration Manager sürümünde, uygulama grupları yayın öncesi bir özelliktir. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../core/servers/manage/pre-release-features.md).  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Uygulama yönetimi** ' ni genişletin ve **uygulama grubu** düğümünü seçin.  

1. Şeritteki Oluştur grubunda, **uygulama grubu oluştur**' u seçin.

1. **Genel bilgiler** sayfasında, uygulama grubuyla ilgili bilgileri belirtin.  

1. **Yazılım Merkezi** sayfasında, yazılım merkezi 'nde gösterilen bilgileri ekleyin.  

1. **Uygulama grubu** sayfasında **Ekle**' yi seçin. Bu grup için bir veya daha fazla uygulama seçin. **Yukarı taşı** ve **aşağı taşı** eylemlerini kullanarak bunları yeniden sıralayın.  

1. Sihirbazı tamamlayın.  

Uygulama grubunu bir uygulamayla aynı işlemi kullanarak dağıtın. Daha fazla bilgi için bkz. [uygulamaları dağıtma](deploy-applications.md). Sürüm 1910 ' den başlayarak, bir uygulama grubunu cihaza veya Kullanıcı koleksiyonlarına dağıtabilirsiniz.

Grubu dağıttıktan sonra:

- Gruba yeni bir uygulama eklerseniz, yeni uygulama içeriğini dağıtım noktalarına ayrı olarak dağıtmanız gerekir.

- Uygulama grubundaki bir uygulamayı değiştirirseniz, içeriği yeniden dağıtın.

Uygulama grubu dağıtımında sorun gidermek için, istemcisinde aşağıdaki günlük dosyalarını kullanın:

- **AppGroupHandler. log**
- **AppEnforce.log**
- **SettingsAgent. log**

> [!Important]  
> Hiyerarşinin tamamını ve hedeflenen istemcileri en az sürüm 1906 ' e güncelleştirene kadar bir uygulama grubu oluşturmayın veya dağıtmayın.

### <a name="known-issues"></a>Bilinen sorunlar

- *Sürüm 1906*: gruptaki uygulamalar yalnızca **Windows Installer** veya **betik** dağıtım türlerini içerebilir.
  - *Sürüm 1906*: dağıtım türü yükleme davranışını **sistem için yükleme**olarak ayarlayın.
- Şu dağıtım seçenekleri çalışmayabilir: uyarılar, onay, aşamalı dağıtım, onarım.
- Uygulama gruplarını dışarı veya içeri aktaramazsınız.
- Yeniden başlatma gerektiren tüm uygulamaları gruba eklemeyin veya grup dağıtımı başarısız olabilir.
- *Sürüm 1906*: uygulama grubunu bir kullanıcı koleksiyonuna dağıtamazsınız.
- *Sürüm 1906*: kullanıcılar, yazılım merkezi 'nde uygulama grubunu **kaldıramaz** .
- Uygulama grubunun bir parçası olan bir uygulamayı silerseniz, uygulama grubunun özelliklerini bir daha görüntülediğinizde şu uyarıyı görürsünüz: "gruptaki tüm uygulamalarla ilgili bilgiler yüklenemiyor." Uygulama grubunda basit bir değişiklik yapın ve kaydedin. Örneğin, **yönetici açıklamalarına**bir boşluk ekleyin. Değişikliği kaydettiğinizde, silinen uygulamayı gruptan kaldırır.<!-- 7099542 -->
