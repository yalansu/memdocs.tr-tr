---
title: Sunucu grubu hizmeti
titleSuffix: Configuration Manager
description: Configuration Manager konsolu, güncelleştirmeleri ve uyumluluğu izlemeye yönelik uyarılar ve durumlar sağlar.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 7d6d8bef145e14547e5e6a726a93cb9470b94afd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724331"
---
# <a name="service-a-server-group"></a>Sunucu grubu hizmeti

*Uygulama hedefi: Configuration Manager (geçerli dal)*

>[!IMPORTANT]
> - Configuration Manager sürüm 2002 ' den başlayarak, sunucu grupları düzenleme gruplarıyla değiştirilmiştir. Daha fazla bilgi için bkz. [düzenleme grupları](orchestration-groups.md).
> - Yayın öncesi özellikler, bir üretim ortamında erken test için Güncel Dalı olan özelliklerdir. Bu özellikler tamamen desteklenir, ancak hala etkin geliştirme aşamasındadır ve yayın öncesi kategorisinden çıkana kadar değişiklikler alabilir. Kullanılabilmesi için bu özelliği açmanız gerekir. Daha fazla bilgi için bkz. [Güncelleştirmelerden yayın öncesi sürüm özelliklerini kullanma](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

Configuration Manager sürüm 1606 ' den başlayarak, bir koleksiyon için sunucu grubu ayarlarını, kaç tane, ne kadar yüzdenin veya koleksiyondaki bilgisayarların yazılım güncelleştirmelerini yükleyeceğini tanımlayacak şekilde yapılandırabilirsiniz. Ayrıca, dağıtım öncesi ve dağıtım sonrası PowerShell betiklerini özel eylemleri çalıştıracak şekilde yapılandırabilirsiniz.

Yazılım güncelleştirmelerini sunucu grubu ayarları yapılandırılmış bir koleksiyona dağıttığınızda, Configuration Manager koleksiyondaki kaç bilgisayarın yazılım güncelleştirmelerini belirli bir zamanda yükleyebileceğini ve aynı sayıda dağıtım kilidi bulunduğunu belirler. Yalnızca bir dağıtım kilidi alan bilgisayarlar, yazılım güncelleştirme yüklemesini başlatır. Bir dağıtım kilidi kullanılabilir olduğunda, bilgisayar dağıtım kilidini alır, yazılım güncelleştirmelerini yüklenir ve ardından yazılım güncelleştirmeleri yüklemesi başarıyla tamamlandığında dağıtım kilidini serbest bırakır. Ardından, dağıtım kilidi diğer bilgisayarlar için kullanılabilir hale gelir. Bir bilgisayar bir dağıtım kilidini serbest bırakmadığında, koleksiyon için tüm sunucu grubu dağıtım kilitlerini el ile serbest bırakabilirsiniz.

>[!IMPORTANT]
>Koleksiyondaki tüm bilgisayarların aynı siteye atanması gerekir.

#### <a name="to-create-a-collection-for-a-server-group"></a>Bir sunucu grubu için koleksiyon oluşturmak için  
Sunucu grubu ayarları bir cihaz koleksiyonu için özelliklerde yapılandırılır. Bir sunucu grubuna hizmet vermek için koleksiyondaki tüm üyelerin aynı siteye atanması gerekir. Bir koleksiyon oluşturmak ve sunucu grubu ayarlarını yapılandırmak için aşağıdaki adımları kullanın:
1.  Sunucu grubundaki bilgisayarları içeren [bir cihaz koleksiyonu oluşturun](../../core/clients/manage/collections/create-collections.md) .  

2.  **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları**' na tıklayın, sunucu grubundaki bilgisayarları içeren koleksiyona sağ tıklayın ve ardından **Özellikler**' e tıklayın.  

3.  **Genel** sekmesinde, **tüm cihazlar aynı sunucu grubunun bir parçası olan**' ı seçin ve ardından **Ayarlar**' a tıklayın.  

4.  **Sunucu grubu ayarları** sayfasında, aşağıdaki ayarlardan birini belirtin:  

    -   **Makinelerin bir yüzdesinin aynı anda güncelleştirilmesine Izin ver**: herhangi bir anda yalnızca belirli bir istemci yüzdesinin güncelleştirileceğini belirtir. Örneğin, koleksiyonda 10 istemci varsa ve koleksiyon aynı anda istemcilerin %30 ' u güncelleştirmek üzere yapılandırılmışsa, belirli bir zamanda yalnızca 3 istemci yazılım güncelleştirmelerini yükler.  

    -   **Aynı anda bir dizi makinenin güncelleştirilmesine Izin ver**: herhangi bir anda yalnızca belirli sayıda istemcinin güncelleştirileceğini belirtir.  

    -   **Bakım sırasını belirtin**: koleksiyondaki istemcilerin yapılandırdığınız sırada bir seferde güncelleştirileceğini belirtir. İstemci, yazılım güncelleştirmelerini yalnızca listede bundan sonraki istemci, yazılım güncelleştirmelerini yüklemeyi tamamladığında yükler.  

5.  Dağıtım öncesi (düğüm boşaltma) betiği mi yoksa dağıtım sonrası (düğüm özgeçmişi) betiği mi kullanacağınızı belirtin.  

    > [!WARNING]
    > Özel betikler Microsoft tarafından imzalanmamıştır. Bu betiklerin bütünlüğünü sürdürmek sizin sorumluluğunuzdadır.

    > [!TIP]  
    > Aşağıda, geçerli saati bir metin dosyasına yazan dağıtım öncesi ve dağıtım sonrası betikleri için test etmek üzere kullanabileceğiniz örnekler verilmiştir:  
    >   
    >  **Dağıtım öncesi**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Dağıtım sonrası**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Yazılım güncelleştirmelerini sunucu grubuna dağıtma ve durumu izleme  
Yazılım güncelleştirmelerini, tipik dağıtım işlemini kullanarak sunucu grubu koleksiyonuna dağıtırsınız. Yazılım güncelleştirmelerini dağıttıktan sonra, Configuration Manager konsolunda yazılım güncelleştirme dağıtımını izleyebilirsiniz.
1.  [Yazılım güncelleştirmelerini](manually-deploy-software-updates.md) sunucu grubu koleksiyonuna dağıtın.   

2.  [Yazılım güncelleştirme dağıtımını izleyin](monitor-software-updates.md). Yazılım güncelleştirmeleri dağıtımı için standart izleme görünümlerine ek olarak, istemci yazılım güncelleştirmelerini yüklemeyi beklerken **kilit durumu bekleniyor** görüntülenir. Daha fazla bilgi için UpdatesDeployment. log dosyasını gözden geçirebilirsiniz.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Sunucu grubundaki bilgisayarlar için dağıtım kilitlerini temizle  
Bir bilgisayar bir dağıtım kilidini serbest bırakamazsa, koleksiyon için tüm sunucu grubu dağıtım kilitlerini el ile serbest bırakabilirsiniz. Kilitleri yalnızca bir dağıtım, koleksiyondaki bilgisayarları güncelleştirme takıldığında ve hala uyumlu olmayan bilgisayarlar varsa temizleyin.  
1.  **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları**' na tıklayın ve dağıtım kilitlerini temizlemek için koleksiyona tıklayın.  

2.  **Giriş** sekmesinde, **dağıtım** grubunda, **sunucu grubu dağıtım kilitlerini temizle**' ye tıklayın. İstemciler yazılım güncelleştirmelerini yükleyemediyse ve diğer istemcilerin yazılım güncelleştirmelerini yüklemesini engelliyorsa, dağıtım kilitleri el ile temizlenebilir.  
