---
title: Uygulama dağıtımları için sorun giderme ipuçları
titleSuffix: Configuration Manager
description: Configuration Manager 'da uygulama dağıtım sorunlarını gidermeye yönelik ipuçları
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710590"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Uygulama dağıtımları için sorun giderme ipuçları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Uygulama dağıtımlarıyla ilgili tipik sorunlar aşağıdaki kategorilerden birine girer:

- Uygulama indirme sorunları

- Uygulama dağıtımı uyumluluğu %0 ' da takıldı

Bu sorunlardan biriyle karşılaşırsanız, bu makalede sorun gidermek için kullanabileceğiniz bazı adımlar sağlanmaktadır. Daha ayrıntılı sorun giderme için bkz. [uygulama dağıtımı teknik başvurusu sorunlarını giderme](../understand/app-deployment-technical-reference.md).


## <a name="download-failures"></a>İndirme başarısızlığı

Uygulama indirme hataları aşağıdaki sorunları içerir:

- İstemci, bir uygulamayı karşıdan yüklemeye takılmış

- İstemci uygulama içeriğini indiremiyor

- Uygulama indirilirken istemci %0 ' da takıyor

Uygulama indirme hatalarıyla karşılaşdığınızda denetlenecek ilk şey eksik veya yanlış yapılandırılmış sınırlar ve sınır grupları içindir. Örneğin, istemci intranet üzerindeyse ve yalnızca İnternet istemci yönetimi için yapılandırılmamışsa, ağ konumu yapılandırılmış bir sınır içinde olmalıdır. Ayrıca, istemcinin içerik indirmesi için bu sınıra atanmış bir sınır grubu olması gerekir. Daha fazla bilgi için bkz. [site sınırlarını ve sınır gruplarını tanımlama](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

Bir istemci için sınır yapılandıramıyorum veya belirli bir sınır grubu başka bir sınır grubunun üyesi olamaz:

1. Configuration Manager konsolunda, **dağıtım türünün**özelliklerini açın.  

1. **İçerik** sekmesine geçin.

1. Bir komşu sınır grubundan veya varsayılan site sınır grubundan bir dağıtım noktası kullanmak için bölümünde, dağıtım **noktasından Içerik indirmek ve yerel olarak çalıştırmak**için **dağıtım seçeneklerini** değiştirin. (Varsayılan olarak bu ayar **içerik indirmez**.)

İstemci uygulama içeriğini indiremez bir dağıtım noktasına dağıtılmış olduğundan emin olun. Bu yapılandırmayı doğrulamak için, dağıtım noktalarına içerik dağıtımını izlemek üzere konsol içi Özellikler ' i kullanın. Daha fazla bilgi için bkz. [dağıttığınız Içeriği izleme](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  


## <a name="compliance-stuck-at-0"></a>Uyumluluk %0 ' da takıldı

Uygulamanın dağıtım uyumluluğu %0 olduğunda, **dağıtımlar** düğümü altındaki **izleme** çalışma alanında uygulamanın dağıtım durumunu denetleyin.

- **Devam ediyor**: istemci [içerik indirmek](#download-failures) için takılmış olabilir

- **Hata**: Bu sorunu giderme hakkında daha fazla bilgi için şu blog gönderisine bakın: [Ipuçları ve püf noktaları: başarısız bir dağıtımı rapor eden varlıklar üzerinde işlem](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019) yapma

- **Bilinmiyor**: Bu durum genellikle istemcinin ilke almamasıdır. İstemcinin alıp aldığına bakmak için istemci ilkesini el ile yenileyin. Daha fazla bilgi için bkz. [Configuration Manager istemcisi için ilke almayı başlatma](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).
  
Bu eylemler sorunu çözmezse, istemci durumunu kontrol edin. İstemciyle ilgili daha ayrıntılı bir sorun olabilir. Daha fazla bilgi için bkz. [istemcileri izleme](../../core/clients/manage/monitor-clients.md).


## <a name="next-steps"></a>Sonraki adımlar

- [Uygulamaları izleme](monitor-applications-from-the-console.md)
- [Uygulamaları dağıtma](deploy-applications.md)
- [Uygulamalar için yönetim görevleri](management-tasks-applications.md)
- [Uygulama dağıtımı teknik başvurusu sorunlarını giderme](../understand/app-deployment-technical-reference.md)
