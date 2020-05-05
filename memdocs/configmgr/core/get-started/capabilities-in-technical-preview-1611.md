---
title: Technical Preview 1611 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1611 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721552"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Configuration Manager için Technical Preview 1611 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*



Bu makalede, sürüm 1611 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    

**Bu teknik önizlemede bilinen sorunlar:**   
- ***Önkoşul durumu***: sürüm 1611 ' yi yüklediğinizde, önkoşulların genel durumu uyarılarla geçti olarak gösterilebilir, ancak uyarılara hangi önkoşulların neden olduğunu listelemez. Bunun nedeni aşağıdaki iki önkoşul olabilir:
  - SQL dizini bellek oluşturma seçenekleri
  - Desteklenen SQL Server sürümünü denetler  

  Bunlar yalnızca uyarılar olduğundan yoksayılabilir.

- ***PowerShell***: Configuration Manager konsolundan Windows PowerShell 'e bağlandığınızda şu hatayı alabilirsiniz: **Microsoft. ConfigurationManagement. PowerShell. Types. ps1xml dijital olarak imzalanmadı**.  

   Bu sorunu, 1610 sürümündeki imzalı sürümleri içeren bazı dosyaları değiştirerek çözebilirsiniz. Aşağıdaki **.ps1xml**uzantılara **.psm1** **.psd1** ** &lt;\\ ** sahip tüm dosyaları sürüm 1610 yükleme:. psd1,. ps1xml ve. psm1 yükleme> dizininde bulunan \adminconsole\bin klasöründen kopyalayın. Bu dosyaları ** &lt;\\ ** Technical Preview 1611 yüklemenizin yükleme dizinine>, dosyaların 1611 sürümünün üzerine yazarak yapıştırın.


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Kullanılabilir dağıtımlar ve görev dizileri için ön önbelleğe alma içeriği
Bu teknik önizlemede, kullanılabilir dağıtımlar ve görev dizileri için, kullanıcıların içeriği yüklemeden önce istemcilerin yalnızca ilgili içeriği indirmesini sağlamak üzere ön önbellek özelliğini kullanmayı seçebilirsiniz.

Örneğin, Windows 10 yerinde yükseltme görev sırasını dağıtmak istediğinizi, yalnızca tüm kullanıcılar için tek bir görev sırası istediğinizi ve birden fazla mimarinin ve/veya dile sahip olduğunu varsayalım. Güncel Dalı, kullanılabilir bir dağıtım oluşturursanız ve ardından Kullanıcı yazılım merkezi 'nde **yükler** ' i tıklarsa, içerik o anda indirilir. Bu, yükleme başlatılmaya hazırlanmadan önce ek süre ekler. Alternatif olarak Güncel Dalı, kullanılabilir bir görev sırası dağıtımı oluşturursanız, görev dizisinde başvurulan tüm içerikler indirilir. Bu, tüm diller ve mimarilere yönelik işletim sistemi yükseltme paketini içerir. Her birinin boyutu kabaca 3 GB ise, indirme paketi oldukça büyük olabilir.

Önbelleğe alma öncesi içerik özelliği, istemcinin yalnızca dağıtımı aldığında geçerli içeriği indirmesine izin verme seçeneğini sunar. Bu nedenle, Kullanıcı yazılım merkezi 'nde **yükleme** ' ye tıkladığında içerik hazırlayın ve içerik yerel sabit sürücüde olduğundan yükleme işlemi hızlı bir şekilde başlatılır.

### <a name="to-configure-the-pre-cache-feature"></a>Ön bellek özelliğini yapılandırmak için

1. Belirli mimariler ve diller için işletim sistemi yükseltme paketleri oluşturun. Paketin **veri kaynağı** sekmesinde mimariyi ve dili belirtin. Dil için, ondalık dönüştürmeyi kullanın (örneğin, 1033 Ingilizce için ondalık ve 0x0409 onaltılık eştir). Ayrıntılar için bkz. bir [işletim sistemini yükseltmek için görev dizisi oluşturma](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

    Mimari ve dil değerleri, işletim sistemi yükseltme paketinin ön belleğe alınıp alınmayacağını öğrenmek için bir sonraki adımda oluşturacağınız görev dizisi adım koşullarını eşleştirmek için kullanılır.
2. Farklı diller ve mimarilere yönelik koşullu adımları içeren bir görev dizisi oluşturun. Örneğin, Ingilizce sürüm için aşağıdaki gibi bir adım oluşturabilirsiniz:

    ![ön önbellek özellikleri](media/precacheproperties2.png)

    ![ön önbellek seçenekleri](media/precacheoptions2.png)  

3. Görev sırasını dağıtın. Ön önbellek özelliği için aşağıdakileri yapılandırın:
    - **Genel** sekmesinde, **Bu görev dizisinin içeriğini önceden indir**' i seçin.
    - **Dağıtım ayarları** sekmesinde, görev dizisini **amacına** **uygun** şekilde yapılandırın. **Gerekli** bir dağıtım oluşturursanız, ön önbellek işlevselliği çalışmaz.
    - **Zamanlama** sekmesinde, **Bu dağıtımın kullanılabilir olacağı zaman çizelgesi** için, dağıtım kullanıcılara kullanılabilir hale gelmeden önce istemcilerin içeriği önceden önbelleğe almak için yeterli zaman sunmasına izin veren bir zaman seçin. Örneğin, içeriğin önceden önbelleğe alınması için yeterli süre sağlamak üzere gelecekte kullanılabilir süreyi 3 saat olacak şekilde ayarlayabilirsiniz.  
    - **Dağıtım noktaları** sekmesinde, **dağıtım seçenekleri** ayarlarını yapılandırın. İçerik, bir Kullanıcı yüklemeyi başlatılmadan önce istemcide önceden önbelleğe alınmamışsa, bu ayarlar kullanılır.


### <a name="user-experience"></a>Kullanıcı deneyimleri
- İstemci dağıtım ilkesini aldığında içerik önceden önbelleğe alınır. Bu, başvurulan tüm içeriği (diğer paket türleri) ve yalnızca, görev dizisinde ayarladığınız koşullara göre istemciyle eşleşen işletim sistemi yükseltme paketini içerir.
- Dağıtım kullanıcılara kullanılabilir hale geldiğinde (dağıtımın **zamanlama** sekmesinde ayarı), kullanıcıları yeni dağıtım hakkında bilgilendirmek için bir bildirim görüntülenir ve dağıtım yazılım merkezi 'nde görünür hale gelir. Kullanıcı yazılım merkezi 'ne gidebilir ve yüklemeyi başlatmak için **yükleme** ' ye tıklayabilir.
- İçerik tam olarak önceden önbelleğe alınmamışsa, dağıtımın **dağıtım seçeneği** sekmesinde belirtilen ayarları kullanacaktır. Dağıtımın ne zaman oluşturulduğu ve dağıtımın, istemcilerin içeriği önceden önbelleğe almak için yeterli zaman sunabileceği zaman arasında yeterli zaman olmasını öneririz.


## <a name="see-also"></a>Ayrıca Bkz.
[Configuration Manager için teknik önizleme](../../core/get-started/technical-preview.md)
