---
title: Microsoft Edge, sürüm 77 ve üstünü dağıtma ve güncelleştirme
titleSuffix: Configuration Manager
description: Configuration Manager ile Microsoft Edge, sürüm 77 ve üstünü dağıtma ve güncelleştirme
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 423864c2c954cc67da4ef54d55d7263ae346e786
ms.sourcegitcommit: 24ce7df7dadf2385afe364b817ec58feeb04c700
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86212294"
---
# <a name="microsoft-edge-management"></a>Microsoft Edge yönetimi

*Uygulama hedefi: Configuration Manager (Güncel Dalı)*

Tüm yeni Microsoft Edge iş için hazırlayın. Configuration Manager sürüm 1910 ' den başlayarak, artık kullanıcılarınıza [Microsoft Edge, sürüm 77 ve üstünü](https://docs.microsoft.com/deployedge/) dağıtabilirsiniz. Seçilen Edge derlemesini yüklemek için bir PowerShell betiği kullanılır. Komut dosyası Ayrıca, Configuration Manager ile yönetilebilmesi için otomatik güncelleştirmeleri devre dışı bırakır.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a>Microsoft Edge 'i dağıtma
<!--4561024-->
Yöneticiler, dağıtım için Microsoft Edge istemcisinin bir sürümüyle birlikte Beta, dev veya kararlı kanal seçebilir. Her sürüm müşterilerimiz ve topluluğumuza dersleri ve geliştirmeler içerir.

### <a name="prerequisites-for-deploying"></a>Dağıtım önkoşulları

Microsoft Edge dağıtımıyla hedeflenen istemciler için:

- PowerShell [yürütme Ilkesi](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) kısıtlı olarak ayarlanamaz.
  - Yüklemeyi gerçekleştirmek için PowerShell yürütülür.

- Microsoft Edge yükleyicisi ve [CMPivot](../../core/servers/manage/cmpivot.md) , **Microsoft kod imzalama** sertifikasıyla imzalanır. Bu sertifika, **Güvenilen Yayımcılar** deposunda listelenmemişse, eklemeniz gerekir. Aksi halde, PowerShell yürütme ilkesi **AllSigned**olarak ayarlandığında Microsoft Edge yükleyicisi ve CMPivot çalışmaz. <!--7585106-->

Configuration Manager konsolunu çalıştıran cihazın aşağıdaki uç noktalara erişmesi gerekir:

|Konum|Kullanın|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Microsoft Edge yayınları hakkında bilgi|
|`http://dl.delivery.mp.microsoft.com`|Microsoft Edge yayınları için içerik|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a>Microsoft Edge güncelleştirme ilkelerini doğrulama

#### <a name="configuration-manager-version-1910"></a>Configuration Manager sürüm 1910

Sürüm 1910 ' de, Microsoft Edge dağıtıldığında yükleme betiği, Microsoft Edge için otomatik güncelleştirmeleri kapatarak Configuration Manager yönetilebilmesi için devre dışı bırakır. Grup ilkesi kullanarak bu davranışı değiştirebilirsiniz. Daha fazla bilgi için bkz. Microsoft Edge ve [Microsoft Edge güncelleştirme ilkelerini](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies) [dağıtımınızı planlayın](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) .

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager sürüm 2002 ve üzeri
<!--4561024-->
Sürüm 2002 ' den başlayarak, otomatik güncelleştirmeleri devre dışı bırakmak yerine otomatik güncelleştirmeleri alacak şekilde ayarlanmış bir Microsoft Edge uygulaması oluşturabilirsiniz. Bu değişiklik, Microsoft Edge için güncelleştirmeleri Configuration Manager yönetmeyi veya Microsoft Edge 'in otomatik olarak güncelleştirmesine izin vermeyi seçmenizi sağlar. Uygulamayı oluştururken Microsoft Edge **ayarları** sayfasında, **son kullanıcının cihazında istemcinin sürümünü otomatik olarak güncelleştirmesine izin ver** ' i seçin. Daha önce bu davranışı değiştirmek için grup ilkesi kullandıysanız, grup ilkesi Microsoft Edge yüklemesi sırasında Configuration Manager tarafından yapılan ayarın üzerine yazılır.

[![Microsoft Edge otomatik güncelleştirme ayarı](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Dağıtım oluşturma

Microsoft Edge 'in daha kolay yönetilmesini sağlayan yerleşik uygulama deneyimini kullanarak bir Microsoft Edge uygulaması oluşturun:

1. Konsolunda, **yazılım kitaplığı**altında **Microsoft Edge yönetimi**adlı yeni bir düğüm vardır.
1. Şeritten **Microsoft Edge uygulaması oluştur** ' u seçin ya da **Microsoft Edge yönetimi** düğümüne sağ tıklayın.

   ![Microsoft Edge yönetimi düğümü sağ tıklama eylemi](./media/4561024-create-microsoft-edge-application.png)

1. Sihirbazın **uygulama ayarları** sayfasında, uygulamanın içeriği için bir ad, açıklama ve konum belirtin. Belirttiğiniz içerik konumu klasörünün boş olduğundan emin olun.
1. **Microsoft Edge ayarları** sayfasında şunları seçin:
   - Dağıtılacak Kanal
   - Dağıtılacak sürüm
   - Microsoft Edge 'in, **son kullanıcının cihazında istemci sürümünü otomatik olarak güncelleştirmesine izin** vermek istiyorsanız (sürüm 2002 ' de eklenmiştir)
1. **Dağıtım** sayfasında, uygulamayı dağıtmak istediğinize karar verin. **Evet**' i seçerseniz, uygulama için dağıtım ayarlarınızı belirtebilirsiniz. Dağıtım ayarları hakkında daha fazla bilgi için bkz. [uygulamaları dağıtma](deploy-applications.md#bkmk_deploy-general).
1. İstemci cihazdaki **Yazılım Merkezi** 'nde, Kullanıcı uygulamayı görebilir ve yükleyebilir.

   ![Dağıtım sihirbazında Microsoft Edge ayarları sayfası](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Dağıtım için günlük dosyaları

|Konum|Log|Kullanın|
|---|---|---|
| Site sunucusu|SMSProv.log|Uygulamanın veya dağıtımın oluşturulması başarısız olursa ayrıntıları gösterir.|
| [Değişir](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| İçerik indirme başarısız olursa ayrıntıları gösterir|
| İstemci|  AppEnforce.log|Yükleme bilgilerini gösterir|

## <a name="update-microsoft-edge"></a>Microsoft Edge 'i Güncelleştir
<!--4831871-->

Configuration Manager sürüm 1910 ' den başlayarak, **Microsoft Edge yönetimi**altında **tüm Microsoft Edge güncelleştirmeleri** adlı bir düğüm görürsünüz. Bu düğüm, tüm Microsoft Edge kanalları için güncelleştirmeleri yönetmenize yardımcı olur.<!--initial edge updates released Jan 15,2020-->

1. Microsoft Edge güncelleştirmelerini almak için, **güncelleştirme** sınıflandırmasına ve **Microsoft Edge** ürününe [eşitleme için seçili](../../sum/get-started/configure-classifications-and-products.md)olduğundan emin olun.

   [![Yazılım güncelleştirme noktası özelliklerinde Microsoft Edge 'i ürün olarak seçin](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. **Yazılım kitaplığı** çalışma alanında **Microsoft Edge yönetimi** ' ni genişletin ve **tüm Microsoft Edge güncelleştirmeleri** düğümüne tıklayın.

1. Gerekirse, bir eşitlemeyi başlatmak için Şeritteki **yazılım güncelleştirmelerini Eşitle** ' ye tıklayın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini Synchronize](../../sum/get-started/synchronize-software-updates.md).

   ![Tüm Microsoft Edge Updates düğümü](./media/4831871-all-microsoft-edge-updates.png)

1. Microsoft Edge güncelleştirmelerini, bunları [Otomatik dağıtım kuralınıza](../../sum/deploy-use/automatically-deploy-software-updates.md)ekleme gibi diğer güncelleştirmeler gibi yönetin ve dağıtın. **Tüm Microsoft Edge Updates** düğümünden gerçekleştirebileceğiniz bazı yaygın güncelleştirme görevleri şunlardır:

   - [Aşamalı dağıtım oluşturma](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Yazılım güncelleştirmelerini el ile dağıtma](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Yazılım güncelleştirmelerini indirme](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a>Microsoft Edge Yönetim Panosu
<!--3871913-->
*(Sürüm 2002 ' de tanıtılmıştır)*

Configuration Manager 2002 ' den başlayarak, Microsoft Edge yönetimi panosu, Microsoft Edge ve diğer tarayıcıların kullanımı hakkında öngörüler sağlar. Bu panoda şunları yapabilirsiniz:

- Cihazlarınızdan kaç tane Microsoft Edge yüklü olduğunu görün
- Kaç istemcinin Microsoft Edge 'in farklı sürümlerine sahip olduğunu görün.
   - Bu grafik Canary kanalını içermez.
- Cihazlarda yüklü tarayıcıların bir görünümüne sahip olmak
- Cihaza göre tercih edilen tarayıcı görünümüne sahip olmak <!--5907383-->
   - Şu anda 2002 sürümü için bu grafik boş olacaktır.

### <a name="prerequisites-for-the-dashboard"></a>Pano önkoşulları

Aşağıdaki özellikleri, Microsoft Edge Yönetim Panosu için aşağıdaki [donanım envanteri](../../core/clients/manage/inventory/extend-hardware-inventory.md) sınıflarında etkinleştirin:

- **Yüklü yazılım-Varlık Yönetim Bilgileri (SMS_InstalledSoftware)**
   - Yazılım kodu
   - Ürün Adı
   - Ürün sürümü

- **Varsayılan tarayıcı (SMS_DefaultBrowser)**
   - Tarayıcı program KIMLIĞI

- **Tarayıcı kullanımı (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>Panoyu görüntüleme

Panoyu görmek için, **yazılım kitaplığı** çalışma alanında **Microsoft Edge yönetimi** ' ne tıklayın. **Araştır** ' a tıklayıp başka bir koleksiyon seçerek Grafik verilerinin koleksiyonunu değiştirin. Varsayılan olarak, beş en büyük koleksiyonunuz açılan listede bulunur. Listede olmayan bir koleksiyon seçtiğinizde, yeni seçilen koleksiyon, aşağı açılan listenizde en alttaki noktayı alır.

[![Microsoft Edge Yönetim Panosu](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="hardware-inventory-may-fail-to-process"></a>Donanım envanteri işlem gerçekleştiremeyebilir
<!--7535675-->
Cihazlar için donanım envanteri işleyemeyebilir. Aşağıdakine benzer hatalar, veri bağlantısı \ Dr. log dosyasında görünebilir:

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**Risk azaltma:** Bu sorunu geçici olarak çözmek için, tarayıcı kullanımı (SMS_BrowerUsage) donanım envanteri sınıfı koleksiyonunu devre dışı bırakın.

## <a name="next-steps"></a>Sonraki adımlar

[Uygulamaları izleme](monitor-applications-from-the-console.md)

[Yazılım güncelleştirmelerini izleme](../../sum/deploy-use/monitor-software-updates.md)

[Aşamalı dağıtım izleme ve yönetme](../../osd/deploy-use/manage-monitor-phased-deployments.md)
