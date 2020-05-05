---
title: İstemci yönetimi temelleri
titleSuffix: Configuration Manager
description: Configuration Manager istemcilerini yönetmek için çalıştırdığınız görevler hakkında bilgi edinin.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722868"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>Configuration Manager için istemci yönetim görevlerinin temelleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcilerini yükledikten sonra, istemcileri yönetmek için çalıştırdığınız birkaç görev vardır.  Görevlerden bazıları Configuration Manager konsolundan çalıştırılır. Diğer görevler Configuration Manager istemci uygulamasından çalıştırılır. Configuration Manager istemci uygulaması, Configuration Manager istemci yazılımıyla birlikte yüklenir.

## <a name="configuration-manager-console-tasks"></a>Configuration Manager Konsol görevleri
 Configuration Manager konsolunda çeşitli istemci yönetim görevlerini gerçekleştirebilirsiniz:  

-   Uygulamaları, yazılım güncelleştirmelerini, bakım komut dosyalarını ve işletim sistemlerini dağıtabilirsiniz. Yüklemeyi belirli bir tarih ve saat için yapılandırın, yazılımın istendiğinde kullanıcıların yüklemesine izin vermek veya uygulamaları kaldırılacak şekilde yapılandırmak.  

-   Bilgisayarların kötü amaçlı yazılımlardan ve güvenlik tehditlerinden korunmasına ve sorunlar algılandığında size bildirilmesine yardımcı olabilirsiniz.  

-   İzlemek istediğiniz istemci yapılandırma ayarlarını tanımlayın ve bunların uyumsuz olup olmadığını düzeltin.  

-   Microsoft'tan lisans bilgilerini izleme ve karşılaştırmayı içeren donanım ve yazılım envanteri bilgilerini toplayabilirsiniz.  

-   Uzaktan denetim kullanılarak bilgisayarlarda sorun giderin.  

-   Bilgisayarların güç tüketimini yönetmek ve izlemek için güç yönetim ayarlarını uygulayabilirsiniz.  

Configuration Manager konsolu, önceki görevleri neredeyse gerçek zamanlı olarak izler. Her görev için bildirim ve durum bilgileri Configuration Manager konsolunda kullanılabilir. Verileri yakalamak ve geçmiş eğilimleri belirlemek için SQL Server Reporting Services tümleşik raporlama yeteneklerini kullanın. İstemciler ayrıntıları siteye istemci durumu olarak gönderir.  İstemci durum bilgileri, istemci ve istemci etkinliğinin sistem durumu hakkında veri sağlar ve konsolda veya Configuration Manager yerleşik raporları kullanılarak görüntülenir. Bu veriler, yanıt vermeyen bilgisayarların belirlenmesine yardımcı olur ve bazı durumlarda sorunlar otomatik olarak düzeltilebilir.  

 İstemciler için yönetim görevleri hakkında daha fazla bilgi için bkz. [istemcileri yönetme](../../core/clients/manage/manage-clients.md) ve [Linux ve UNIX sunucuları için istemcileri yönetme](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Rapor kullanma hakkında bilgi edinmek için bkz.   
            [Raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Configuration Manager istemci uygulaması  
 Configuration Manager istemci yazılımını yüklediğinizde, Configuration Manager istemci uygulaması da yüklenir. Yazılım Merkezi 'nin aksine, Configuration Manager istemci uygulaması, son kullanıcı yerine yardım masası için tasarlanmıştır. Bazı yapılandırma seçenekleri yerel yönetim izinleri gerektirir ve çoğu seçenek Configuration Manager istemci uygulamasının nasıl çalıştığı hakkında teknik bilgi gerektirir. Aşağıdaki görevleri bir istemcide gerçekleştirmek için bu uygulamayı kullanabilirsiniz:  

-   İstemciyle ilgili yapı numarası, atanan sitesi, iletişim kurduğu yönetim noktası ve istemcinin ortak anahtar altyapısı (PKI) sertifikası mı yoksa otomatik olarak imzalanan bir sertifika mı kullandığını gösteren özellikleri görüntüleyin.  

-   İstemci ilk kez yüklendikten sonra istemcinin istemci ilkesini başarıyla indirdiğini doğrulayın. Ayrıca, Configuration Manager konsolunda yapılandırılan istemci ayarlarına göre istemci ayarlarının beklendiği gibi etkinleştirildiğini veya devre dışı bırakıldığını doğrulayın.  

-   İstemci eylemlerini başlatın. Örneğin, Configuration Manager konsolunda yakın bir yapılandırma değişikliği varsa ve zamanlanan bir sonraki saate kadar beklemek istemiyorsanız istemci ilkesini indirin.  

-   Bir istemciyi Configuration Manager bir siteye el ile atayın veya bir site bulmayı deneyin. Ardından, DNS 'de yayımlanan Yönetim noktaları için etki alanı adı sistemi (DNS) sonekini belirtin.  

-   Dosyaları geçici olarak depolayan istemci önbelleğini yapılandırın. Ardından, yazılım yüklemek için daha fazla disk alanına ihtiyaç duyuyorsanız önbellekteki dosyaları silin.  

-   Internet tabanlı istemci yönetimi için ayarları yapılandırabilirsiniz.  

-   İstemciye dağıtılan yapılandırma temel çizgilerini görüntüleyebilir, uyumluluk değerlendirmesini başlatabilir ve uyumluluk raporlarını görüntüleyebilirsiniz.  
