---
title: Cmdlet 'ler için gizlilik bildirimi
titleSuffix: Configuration Manager
description: Microsoft 'un Configuration Manager cmdlet 'leriyle ilgili verileri nasıl toplayıp kullandığını öğrenin
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714650"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Configuration Manager cmdlet kitaplığı gizlilik bildirimi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu gizlilik bildirimi Configuration Manager cmdlet kitaplığı özelliklerini içerir.  

## <a name="usage-data"></a>Kullanım verileri  

#### <a name="what-this-feature-does"></a>Bu özelliğin yaptığı

Configuration Manager cmdlet kitaplığı, Windows PowerShell cmdlet 'leri ve betikleri kullanarak bir Configuration Manager hiyerarşisini yönetmenizi sağlar. Cmdlet kitaplığı, eğilimleri ve kullanım düzenlerini belirlemek için kitaplığındaki cmdlet 'leri nasıl kullandığınız hakkında bilgi toplar. Cmdlet kitaplığı, cmdlet 'leri kullanırken aldığınız hataların türlerini ve sayısını da toplar.  

#### <a name="information-collected-processed-or-transmitted"></a>Toplanan, işlenen veya iletilen bilgiler
   
Toplanan kullanım verileri cmdlet 'leri başlatma, durdurma ve sonlandırmayla, kullanımdan kaldırılan cmdlet 'lerin çalıştırılması ve cmdlet 'lerle ilgili SMS sağlayıcısı işlemleri için etkinlik ölçümleri içerir. Bu bilgiler kişisel olarak tanımlanabilir değildir. Toplanan hata bilgileri cmdlet 'lerin döndürdüğü hataları ve özel durum hatalarına ilişkin hata ayrıntılarını içerir. Bazı hata ayrıntısı raporlarında, bilgisayarınıza bağlı bir cihazın seri numarası gibi bireysel tanımlayıcılar yanlışlıkla bulunabilir. Cmdlet kitaplığı, Microsoft 'a iletilmadan önce bağımsız tanımlayıcıları kaldırmak için hata raporlarında bulunan bilgileri filtreleyerek ve anonimleştirir.  

#### <a name="use-of-information"></a>Bilgilerin kullanımı
   
Microsoft bu bilgileri, sunduğu ürünlerin ve hizmetlerin kalitesini, güvenliğini ve bütünlüğünü geliştirmek için kullanır.  

#### <a name="choicecontrol"></a>Seçim/Denetim   

Bu kullanım verileri özelliği varsayılan olarak etkindir. Configuration Manager cmdlet kitaplığı, bu işlevselliği denetleyen iki kayıt defteri anahtarına sahiptir.  

 Tam olarak devre dışı bırakmak için bu iki kayıt defteri anahtarı değerini ayarlayın. Bunlar, Windows için olay Izleme (ETW) sağlayıcılarının her birine yöneliktir:  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider: CeipLevel = 0 (sürücü sağlayıcısı için kullanım verilerinin dışında)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets: CeipLevel = 0 (cmdlet 'ler için kullanım verileri dışında)  

  Kullanım verileri ayarlarında yapılan değişiklikler, bulundukları bilgisayara özgüdür.  


## <a name="next-steps"></a>Sonraki adımlar

[Cmdlet kitaplığı belgelerini Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
