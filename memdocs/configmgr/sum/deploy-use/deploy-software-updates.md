---
title: Yazılım güncelleştirmelerini dağıtma
titleSuffix: Configuration Manager
description: Configuration Manager konsolunda yazılım güncelleştirmelerini el ile veya otomatik olarak dağıtmayı öğrenin.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: a6e27e2d03983fdf627016d0e3b41aaa378afe29
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693480"
---
# <a name="deploy-software-updates"></a>Yazılım güncelleştirmelerini dağıtma  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yazılım güncelleştirmesi dağıtım aşaması, yazılım güncelleştirmelerini dağıtma işlemidir. Yazılım güncelleştirmelerini nasıl dağıtabileceğinizi bağımsız olarak, sitesi:
- Güncelleştirmeleri bir yazılım güncelleştirme grubuna ekler
- Güncelleştirme içeriğini dağıtım noktalarına dağıtır
- Güncelleştirme grubunu istemcilere dağıtır  

Dağıtım oluşturduktan sonra, site hedeflenen istemcilere ilişkili bir yazılım güncelleştirme ilkesi gönderir. İstemciler, yazılım güncelleştirme içerik dosyalarını bir içerik kaynağından yerel önbelleklerine indirir. Internet üzerindeki istemciler her zaman Microsoft Update bulut hizmetinden içerik indirir. Yazılım güncelleştirmeleri daha sonra istemci tarafından yüklenmek üzere kullanılabilir.   

> [!Tip]  
>  Bir dağıtım noktası yoksa, intranetteki istemciler Microsoft Update yazılım güncelleştirmelerini de indirebilir.  

> [!NOTE]  
>  Diğer dağıtım türlerinden farklı olarak, yazılım güncelleştirmelerinin hepsi istemci önbelleğine indirilir. Bu, istemcideki en büyük önbellek boyutu ayarından bağımsız olarak belirlenir. İstemci önbelleği ayarı hakkında daha fazla bilgi için bkz. [Configuration Manager istemcileri için istemci önbelleğini yapılandırma](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Zorunlu bir yazılım güncelleştirme dağıtımını yapılandırırsanız yazılım güncelleştirmeleri zamanlanan son tarihte otomatik olarak yüklenir. Alternatif olarak istemci bilgisayardaki kullanıcı son tarihten önce yazılım güncelleştirme yüklemesini zamanlayabilir veya başlatabilir. Denenen yüklemenin ardından istemci bilgisayarlar yazılım yüklemesinin başarılı olup olmadığını bildirmek üzere durum iletilerini site sunucusuna geri gönderir. Yazılım güncelleştirme dağıtımları hakkında daha fazla bilgi için bkz. [Yazılım güncelleştirme dağıtımı iş akışları](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Yazılım güncelleştirmelerini dağıtmaya yönelik üç ana senaryo vardır: 
- [El ile dağıtım](#BKMK_ManualDeployment)  
- [Otomatik dağıtım](#bkmk_auto)  
- [Aşamalı dağıtım](#bkmk_phased)  

Genellikle, istemcileriniz için bir taban çizgisi oluşturmak üzere yazılım güncelleştirmelerini elle dağıtarak başlar ve sonra otomatik veya aşamalı dağıtım kullanarak istemcilerde yazılım güncelleştirmelerini yönetirsiniz.  

> [!Note]  
> Aşamalı dağıtım ile otomatik dağıtım kuralı kullanamazsınız.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Yazılım güncelleştirmelerini el ile dağıtma
Configuration Manager konsolunda yazılım güncelleştirmeleri ' ni seçin ve dağıtım sürecini el ile başlatın. Bu dağıtım yöntemini genellikle aşağıdaki şekilde kullanabilirsiniz:  

- Aylık dağıtımları yöneten otomatik dağıtım kuralları oluşturmadan önce gerekli yazılım güncelleştirmeleriyle istemcileri güncel duruma getirmek  

- Bant dışı yazılım güncelleştirmelerini dağıtma  


Aşağıdaki listede, yazılım güncelleştirmelerinin el ile dağıtımı için genel iş akışı sağlanmaktadır:  

1. Belirli gereklilikler kullanan yazılım güncelleştirmeleri için filtre. Örneğin, 50 ' den fazla istemcide gerekli olan tüm güvenlik veya kritik yazılım güncelleştirmelerini alan ölçütler sağlayın.  

2. Yazılım güncelleştirmelerini içeren bir yazılım güncelleştirme grubu oluşturun.  

3. Yazılım güncelleştirmeleri için içeriği, yazılım güncelleştirme grubu içine indirin.  

4. Yazılım güncelleştirme grubunu el ile dağıtın.  

Daha fazla bilgi ve ayrıntılı adımlar için bkz. [yazılım güncelleştirmelerini el ile dağıtma](manually-deploy-software-updates.md).

> [!Note]
> - 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.
> - Microsoft 365 Apps istemci güncelleştirmelerini el ile dağıttığınızda, **yazılım kitaplığı** çalışma alanının **Office 365 Istemci yönetimi** altındaki **Office 365 güncelleştirmeleri** düğümünde bunları bulun. 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Yazılım güncelleştirmelerini otomatik olarak dağıt

Otomatik bir dağıtım kuralı (ADR) kullanarak otomatik yazılım güncelleştirmeleri dağıtımını yapılandırın. Bu dağıtım yöntemi, aylık yazılım güncelleştirmeleri (genellikle "Düzeltme Eki Salı" olarak bilinir) ve tanım güncelleştirmelerini yönetmek için ortaktır. Dağıtım işlemini otomatikleştirmek için bir ADR ölçütlerini tanımlarsınız. Aşağıdaki listede, yazılım güncelleştirmelerini otomatik olarak dağıtmak için genel iş akışı sağlanmaktadır:  

1.  Dağıtım ayarlarını belirten bir ADR oluşturun.  

2.  Site, yazılım güncelleştirmelerini bir yazılım güncelleştirme grubuna ekler.  

3.  Site, yazılım güncelleştirme grubunu hedef koleksiyondaki istemcilere dağıtır.  

İlk olarak, otomatik yazılım güncelleştirme dağıtım stratejinizi saptayın. Örneğin, ilk olarak bir test istemcileri koleksiyonunu hedeflemek için ADR 'yi oluşturun. Test grubunu, yazılım güncelleştirmelerini başarıyla yüklediğinizi doğruladıktan sonra, kurala yeni bir dağıtım ekleyin. Ayrıca, varolan dağıtımdaki hedeflenen koleksiyonu, daha büyük bir istemci kümesi içeren bir ile değiştirebilirsiniz. Kullanım stratejisi üzerinde karar verirken aşağıdaki davranışları göz önünde bulundurun:  

- ADR 'nin oluşturduğu yazılım güncelleştirme nesnelerinin özelliklerini değiştirebileceksiniz.   

- ADR, yazılım güncelleştirmelerini hedef koleksiyona eklediğinizde istemcilere otomatik olarak dağıtır.  

- Siz veya ADR, yazılım güncelleştirme grubuna yeni yazılım güncelleştirmeleri eklerse, site bunları otomatik olarak hedef koleksiyondaki istemcilere dağıtır.  

- ADR için istediğiniz zaman dağıtımları etkinleştirin veya devre dışı bırakın.  


ADR oluşturduktan sonra kurala başka dağıtımlar ekleyin. Bu eylem farklı koleksiyonlara farklı güncelleştirmeler dağıtma karmaşıklığını yönetmenize yardımcı olur. Her yeni dağıtım, tüm işlevlere ve dağıtım izleme deneyimine sahiptir.  

Eklediğiniz her yeni dağıtım:  

- ADR 'nin ilk çalıştırıldığında oluşturduğu güncelleştirme grubunu ve paketi kullanır  
- Farklı bir koleksiyonu hedefleyebilir  
- Aşağıdaki benzersiz dağıtım özelliklerini destekler:  
  -   Etkinleştirme zamanı  
  -   Son tarih  
  -   Kullanıcı deneyimi  
  -   Her dağıtım için ayrı uyarılar  


Daha fazla bilgi ve ayrıntılı adımlar için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](automatically-deploy-software-updates.md)



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Yazılım güncelleştirmelerini aşamalarda dağıtma

<!--1358146-->
Sürüm 1810 ' den başlayarak, yazılım güncelleştirmeleri için aşamalı dağıtımlar oluşturun. Aşamalı dağıtımlar, özelleştirilebilir ölçütlere ve gruplara göre düzenlenmiş, sıralı bir yazılım dağıtımını düzenlemenize olanak tanır.

Daha fazla bilgi için bkz. [aşamalı dağıtımlar oluşturma](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).

