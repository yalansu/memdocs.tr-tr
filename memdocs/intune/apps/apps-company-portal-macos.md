---
title: MacOS uygulaması için Şirket Portalı ekleyin
titleSuffix: Microsoft Intune
description: MacOS Şirket Portalı uygulamasını ekleyin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1eb64f8ed2bc67b4800a4583010dea150ade421d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914166"
---
# <a name="add-the-macos-company-portal-app"></a>MacOS Şirket Portalı uygulamasını ekleme

Cihazları yönetmek, isteğe bağlı uygulamalar yüklemek ve macOS cihazlarında Kullanıcı benzeşimi ile koşullu erişimle korunan kaynaklara erişim kazanmak için, kullanıcıların Şirket Portalı uygulamasına yüklemeleri ve oturum açması gerekir. MacOS için Şirket Portalı yüklemek üzere kullanıcılarınıza yönergeler verebilir veya doğrudan Intune 'dan kaydedilmiş cihazlara yükleyebilirsiniz.

MacOS uygulamasının Şirket Portalı yüklemek için aşağıdaki seçeneklerden herhangi birini kullanabilirsiniz:
- [Kullanıcılara Şirket Portalı indirip yüklemelerini bildirin](#instruct-users-to-download-and-install-company-portal)
- [MacOS için Şirket Portalı macOS LOB uygulaması olarak yükler](#install-company-portal-for-macos-as-a-macos-lob-app)
- [MacOS kabuğu betiği kullanarak macOS için Şirket Portalı 'i yükler](#install-company-portal-for-macos-by-using-a-macos-shell-script)

Uygulamaları yükledikten sonra uygulamaların daha güvenli ve güncel kalmasına yardımcı olmak için Şirket Portalı Uygulama Microsoft otomatik güncelleştirme (MAU) ile birlikte gelir.

> [!NOTE]
> Şirket Portalı uygulaması yalnızca doğrudan kaydolma veya otomatik cihaz kaydı kullanılarak kaydedilmiş Intune kullanan cihazlara otomatik olarak yüklenebilir. Kişisel cihaz veya el ile kaydolma için Şirket Portalı uygulamasının kayıt başlatmak üzere indirilmesi ve yüklenmesi gerekir. Bkz. [kullanıcıların şirket portalı indirip yüklemesini isteyin](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Kullanıcılara Şirket Portalı indirip yüklemelerini bildirin

Kullanıcılara macOS için Şirket Portalı indirme, yükleme ve oturum açma izni verebilirsiniz. Şirket Portalı indirme, yükleme ve oturum açma yönergeleri için bkz. [Şirket Portalı uygulamasını kullanarak macOS cihazınızı kaydetme](../user-help/enroll-your-device-in-intune-macos-cp.md).

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>MacOS için Şirket Portalı macOS LOB uygulaması olarak yükler

MacOS için Şirket Portalı, [MacOS LOB uygulamaları](lob-apps-macos.md) özelliği kullanılarak indirilebilir ve yüklenebilir. İndirilen sürüm, her zaman yüklenecek sürümdür ve kullanıcıların ilk kayıt sırasında en iyi deneyimi elde etmek için düzenli olarak güncelleştirilmeleri gerekebilir.

1. MacOS için Şirket Portalı indirin https://go.microsoft.com/fwlink/?linkid=853070 . 

2. [MacOS lob uygulamalarında](lob-apps-macos.md)MacOS lob uygulaması oluşturmak için yönergeleri izleyin.

> [!NOTE]
> Yüklendikten sonra, macOS uygulamasının Şirket Portalı, Microsoft otomatik güncelleştirme (MAU) kullanılarak otomatik olarak güncelleştirilecek.
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>MacOS kabuğu betiği kullanarak macOS için Şirket Portalı 'i yükler

MacOS için Şirket Portalı, [MacOS kabuğu betikleri](macos-shell-scripts.md) özelliği kullanılarak indirilebilir ve yüklenebilir. Bu seçenek, macOS için Şirket Portalı geçerli sürümünü her zaman yükler, ancak size [MacOS LOB uygulamalarını](lob-apps-macos.md)kullanarak uygulamalar dağıtıldığında kullanabileceğiniz uygulama yüklemesi raporlaması sunmayacak.

1. [Intune kabuğu betik örnekleri-Şirket portalı](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal)macos için şirket portalı yüklemek üzere örnek bir betik indirin.

2. MacOS kabuğu komut [dosyalarını](macos-shell-scripts.md)kullanarak MacOS kabuğu betiğini dağıtmak için yönergeleri izleyin. 
    - **Run betiğini, oturum açmış kullanıcı olarak** **(sistem bağlamında çalışacak şekilde)** ayarlayın.
    - Betik **3**' e **başarısız olursa maksimum yeniden deneme sayısını** ayarlayın.

> [!NOTE]
> Betiği, macOS için Şirket Portalı geçerli sürümünü indirmek üzere çalıştırıldığında Internet erişimi gerektirir. 
## <a name="next-steps"></a>Sonraki adımlar
- Uygulama atama hakkında daha fazla bilgi için bkz. [uygulamaları gruplara atama](apps-deploy.md).
- Otomatik cihaz kaydını yapılandırma hakkında daha fazla bilgi için bkz. [aygıt kayıt programı-macOS 'U kaydetme](../enrollment/device-enrollment-program-enroll-macos.md).
- MacOS 'ta Microsoft otomatik güncelleştirme ayarlarını yapılandırma hakkında daha fazla bilgi için bkz. [Mac Updates](/windows/security/threat-protection/microsoft-defender-atp/mac-updates).