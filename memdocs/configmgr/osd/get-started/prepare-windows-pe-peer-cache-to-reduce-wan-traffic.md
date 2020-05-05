---
title: WAN trafiğini azaltmak için Windows PE eş önbelleğini hazırlama
titleSuffix: Configuration Manager
description: Windows PE Eş Önbelleği, yerel bir eşten içerik almak için Windows PE 'de çalışarak yerel dağıtım noktası olmadığında WAN trafiğini en aza indirir.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724044"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Configuration Manager 'de WAN trafiğini azaltmak için Windows PE eş önbelleğini hazırlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yeni bir işletim sistemini Configuration Manager dağıtırken, görev dizisini çalıştıran bilgisayarlar bir dağıtım noktasından içerik indirmek yerine yerel bir eşten (eş önbellek kaynağı) içerik almak üzere Windows PE Eş Önbelleği kullanabilir. Bunun yapılması, yerel dağıtım noktasının mevcut olmadığı şube senaryolarında genel alan ağı (WAN) trafiğini en aza indirmeye yardımcı olur.  

 Windows PE Eş Önbelleği [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)ile benzerdir, ancak Windows önyükleme ortamı (Windows PE) içindeki işlevleri. Aşağıdaki terimler Windows PE Eş Önbelleği kullanan istemcileri tanımlamak için kullanılır:  

-   **Eş önbellek istemcisi** , Windows PE Eş Önbelleği kullanmak üzere yapılandırılan bir bilgisayardır.  

-   **Eş önbellek kaynağı** , eş önbellek için yapılandırılmış ve ilgili içeriği isteyen diğer eş önbellek istemcilerine içeriği sunan bir istemcidir.  

Eş Önbelleği yönetmek için aşağıdaki bölümleri kullanın.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a> Eş Önbelleği kaynağına depolanan nesneler  
 Windows PE Eş Önbelleği kullanmak üzere yapılandırılan bir görev dizisi, Windows PE’de çalışırken aşağıdaki içerik nesnelerini alabilir:  

- İşletim sistemi görüntüsü  

- Sürücü paketi  

- Paketler ve programlar (istemci, görev dizisini tam işletim sisteminde çalıştırmaya devam ettiğinde, görev dizisi başlangıçta Windows PE 'de çalışırken eş önbellek için yapılandırıldıysa, istemci bu içeriği bir eş önbellek kaynağından alır.)  

- Ek önyükleme görüntüleri  

  Aşağıdaki içerik nesneleri hiçbir zaman eş önbelleği kullanılarak aktarılmaz. Bunun yerine bir dağıtım noktasından veya ortamınızda Windows BranchCache öğesini yapılandırdıysanız Windows BranchCache ile aktarılır:  

- Uygulamalar  

- Yazılım güncelleştirmeleri  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a>Windows PE Eş Önbelleği nasıl çalışır?  
 Dağıtım noktasına sahip olmamasına karşın Windows PE Eş Önbelleği kullanması sağlanan birkaç istemcisi olan şubeyi içeren bir senaryo düşünün. Eş önbelleği kullanmak üzere yapılandırılan görev dizisini, eş önbelleği kaynağının bir parçası olarak yapılandırılmış birkaç istemciye dağıtın. Görev dizisini çalıştıran ilk istemci, içerik ile bir eş için istek yayınlar. Bir tane bulamadığı için WAN üzerindeki bir dağıtım noktasından içeriği alır. İstemci yeni görüntüyü yükledikten sonra içeriği Configuration Manager istemci önbelleğinde depolar, böylece diğer istemcilere eş önbellek kaynağı olarak çalışabilir. Sonraki istemci görev dizisini çalıştırdığında, eş önbellek kaynağı için alt ağda bir istek yayınlar ve bu ilk istemci yanıt vererek önbelleğe alınan içeriğini kullanılabilir hale getirir.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a> Hangi istemcilerin Windows PE eş önbelleği kaynağının bir parçası olacağını belirleme  
 Bir Windows PE Eş Önbelleği kaynağı olarak hangi bilgisayarların seçileceğini belirlemenize yardımcı olmak üzere birkaç konuyu göz önünde bulundurmanız gerekir:  

-   Windows PE Eş Önbelleği kaynağı her zaman açık olan ve eş önbelleği istemcileri tarafından kullanılabilen bir masaüstü bilgisayar olmalıdır.  

-   Windows PE Eş Önbelleği, görüntüleri depolamak için yeterli olan bir istemci önbelleği boyutuna sahiptir.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a> Bir istemcinin Windows PE Eş Önbelleği kaynağını kullanmasına yönelik gereksinimler  
 İstemcilerin bir Windows PE Eş Önbelleği kaynağı kullanması için aşağıdaki gereksinimleri karşılaması gerekir:  

-   Configuration Manager istemci, ağınızda aşağıdaki bağlantı noktaları üzerinden iletişim kurabilmelidir:  

    -   Eş önbellek kaynağı bulmak için ilk ağ yayını için bağlantı noktası: Bu, varsayılan olarak UDP bağlantı noktası 8004 ' dir.  

    -   Eş önbellek kaynağından (HTTP ve HTTPS) içerik indirme için bağlantı noktası. Varsayılan olarak, TCP bağlantı noktası 8003 ' dir.  
    
        Daha fazla bilgi için bkz. [bağlantılar için kullanılan bağlantı noktaları](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  İstemciler kullanılabilir olduğunda içeriği yüklemek için HTTPS kullanır. Ancak, aynı bağlantı noktası HTTP veya HTTPS için kullanılır.  

-   Dağıttığınız görüntüleri saklamak için yeterli alana sahip olduklarından emin olmak için istemciler üzerinde[Configuration Manager İstemcileri için İstemci Önbelleğini yapılandırın](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) . Windows PE Eş Önbelleği, istemci önbelleğinin yapılandırma veya davranışını etkilemez.  

-   Görev dizisi dağıtımının dağıtım seçenekleri, Yalnızca görev dizisi için gerektiğinde içeriği yerel olarak indir olarak yapılandırılmalıdır.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a>Windows PE eş önbelleğini yapılandırma  
 Bir istemciye eş önbellek kaynağı olarak görev yapabilecek eş önbellek içeriği sağlamak için aşağıdaki yöntemleri kullanabilirsiniz:  

- İçeriğe sahip olan bir eş önbellek bulamayan eş önbellek istemcisi bunu bir dağıtım noktasından indirir.  İstemci eş önbelleğini etkinleştiren istemci ayarlarını alırsa ve görev dizisi önbelleğe alınmış içeriği korumak için yapılandırılmışsa, istemci bir eş önbellek kaynağı haline gelir.  

- Eş önbellek istemcisi başka bir eş önbellek istemcisinden (eş önbellek kaynağı) içerik alabilir.  İstemci eş önbellek için yapılandırıldığından, önbelleğe alınan içeriği korumak üzere yapılandırılmış bir görev dizisi çalıştırdığında eş önbellek kaynağı haline gelir.  

- İstemci, Windows PE Eş Önbelleği görev dizisine dahil edilmiş ilgili içeriği önceden hazırlamak için kullanılan isteğe bağlı [Paket İçeriğini İndir](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)adımını içeren bir görev dizisi çalıştırır. Bu yöntemi kullandığınızda:  

  -   İstemcinin dağıtılmakta olan görüntüyü yüklemesi gerekmez.  

  -   **Paket İçeriğini İndir** seçeneğine ek olarak, görev dizisi **Configuration Manager istemci önbelleği** seçeneğini de kullanmalıdır. İstemcinin diğer eş önbellek istemcileri için eş önbellek kaynağı olarak hareket etmesini sağlamak üzere içeriği istemci önbelleğine depolayabilirsiniz.  

  Aşağıdaki yordamlar istemcilerde Windows PE Eş Önbelleğini yapılandırmanıza ve eş önbelleği destekleyen görev dizilerini yapılandırmanıza yardımcı olur.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Windows PE Eş Önbelleği kaynak bilgisayarlarını yapılandırmak için  

1. Configuration Manager konsolunda, **Yönetim** > **istemci ayarları**' na gidin ve ardından yeni bir **özel istemci cihaz ayarları** oluşturun veya var olan bir ayarlar nesnesini düzenleyin. Bunu ayrıca **Varsayılan İstemci Ayarlarını** nesnesi için yapılandırabilirsiniz.  

   > [!TIP]  
   >  Hangi istemcilerin bu yapılandırmayı alacağını yönetmek için bir özel ayarlar nesnesi kullanın. Örneğin, sıklık hareket halinde olan kullanıcıların dizüstü bilgisayarlarında bunu yapılandırmak istemeyebilirsiniz. Yüksek oranda mobil bir sistem diğer eş önbellek istemcilerine içerik sağlamak için kötü bir kaynak olabilir.  
   >   
   >  Ayrıca, **Varsayılan İstemci Ayarları**’nın bir parçası olarak bu ayarı yapılandırdığınızda yapılandırmanın ortamınızdaki tüm istemcilere uygulandığını unutmayın.  

2. **Istemci önbelleği ayarları**' nın altında, **tam işletim sisteminde Configuration Manager istemcisinin, içerik paylaşmasını etkinleştir** ayarını **Evet**olarak belirleyin.  

   -   Varsayılan olarak yalnızca HTTP etkinleştirilir. İstemcilerin HTTPS üzerinden içerik indirmesini etkinleştirmek istiyorsanız, **İstemci eş iletişimi için HTTPS’yi etkinleştir** ayarını **Evet**olarak belirleyin.  

   -   Varsayılan olarak, yayınlar için bağlantı noktası 8004 olarak ve içerik indirmeleri için bağlantı noktası 8003 olarak ayarlanır. Her ikisini de değiştirebilirsiniz.  

3. İstemci Ayarları’nı, eş önbelleği kaynağı olması için seçtiğiniz istemcilere kaydedin ve dağıtın.  

   Bir cihaz bu ayar nesnesi ile yapılandırıldıktan sonra, cihaz bir eş önbellek kaynağı olarak hareket edecek şekilde yapılandırılır. Gerekli bağlantı noktalarını ve protokolleri yapılandırmak üzere bu ayarlar potansiyel eş önbellek istemcilerine dağıtılmalıdır.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a>Windows PE eş önbelleği için görev dizisi yapılandırma  
 Görev dizisini yapılandırırken aşağıdaki görev dizisi değişkenlerini, görev dizisinin dağıtıldığı koleksiyonda Koleksiyon Değişkenleri olarak kullanın:  

- **SMSTSPeerDownload**  

   Değer: TRUE  

   Bu seçenek istemcinin Windows PE Eş Önbelleği kullanmasını sağlar.  

- **SMSTSPeerRequestPort**  

   Değer: <bağlantı noktası numarası\>  

   Istemci ayarları 'nda yapılandırılmış varsayılan bağlantı noktasını (8004) kullanmazsanız, bu değişkeni ilk yayın için kullanmak üzere ağ bağlantı noktasının özel bir değeriyle yapılandırmanız gerekir.  

- **SMSTSPreserveContent**  

   Değer: TRUE  

   Bu, dağıtım sonrasında Configuration Manager istemci önbelleğinde tutulacak görev dizisindeki içeriği işaretler. Bu, yalnızca görev dizisinin süresi boyunca içeriği koruyan ve Configuration Manager istemci önbelleğini değil, görev sırası önbelleğini kullanan Smstspersiscontent seçeneğinin kullanmaktan farklıdır.  

  Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md).  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a> Windows PE Eş Önbelleği kullanma başarısını doğrulama  
 Windows PE eş önbelleğini kullanarak bir görev dizisi dağıtıp yükledikten sonra, görev dizisini çalıştıran istemcideki **smsts.log** dosyasını görüntüleyerek eş önbelleğinin işlemde başarıyla kullanıldığını doğrulayabilirsiniz.  

 Günlükte, <*Sourceservername*> istemcinin içeriği aldığı bilgisayarı tanımladığı aşağıdakine benzer bir giriş bulun. Bu bilgisayar bir eş önbellek kaynağı olmalıdır ve dağıtım noktası sunucusu olmamalıdır. Diğer ayrıntılar yerel ortamınıza ve yapılandırmalarınıza göre değişir.  

-   *<! [Günlük [Indirilen dosya <SourceServerName\>: 8003/SCCM_BranchCache $/SS10000C/SCCM?/Install,wim to C:\\_SMSTaskSequence \Packages\ss10000c\ınstall,wim] log]! ><Time = "14:24:33.329 + 420" Date = "06-26-2015" Bileşen = "ApplyOperatingSystem" bağlam = "" tür = "1" iş parçacığı = "1256" File = "downloadcontent. cpp: 1626" >*  
