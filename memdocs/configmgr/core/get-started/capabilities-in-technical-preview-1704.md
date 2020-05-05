---
title: Technical Preview 1704 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1704 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721412"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Configuration Manager için Technical Preview 1704 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1704 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Android uygulamalarını uygulama yapılandırma ilkeleriyle yapılandırma
Kullanıcı, Android for Work cihazlarda bir uygulama çalıştırdığında gerekebilecek ayarları dağıtmak için Configuration Manager 'de uygulama yapılandırma ilkelerini kullanabilirsiniz. Android uygulama yapılandırma ilkeleri yalnızca Android for Work çalıştıran cihazlarda kullanılabilir ve Play for Work mağazasından onaylanan uygulamalar için geçerlidir.

### <a name="try-it-out"></a>Deneyin                 

Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **uygulama yapılandırma ilkeleri** ' ni seçin ve **uygulama yapılandırma ilkesi oluştur**' u seçin. Sihirbazın **genel** sayfasında, artık **bir yapılandırma ilkesi türü seçebilirsiniz**. Uygulama yapılandırma ilkesi tarafından hedeflenen platformu belirtin: **Android for Work uygulamaları Için yapılandırma ilkesi**. Daha sonra **ad ve değer çiftlerini belirtebilir** veya **BIR özellik listesi JSON dosyasına**gidebilirsiniz. Yeni uygulama yapılandırma ilkesi, **uygulama yapılandırma ilkeleri** düğümündeki **yazılım kitaplığı** çalışma alanında gösterilir. Bir uygulama yapılandırma ilkesini bir Android for Work uygulamasının dağıtımıyla ilişkilendirmek için [uygulamaları dağıt](../../apps/deploy-use/deploy-applications.md) konusunun yordamını kullanarak, uygulamayı normalde yaptığınız gibi dağıtın.

## <a name="hardware-inventory-collects-secure-boot-information"></a>Donanım envanteri güvenli önyükleme bilgilerini toplar
Donanım envanteri artık istemcilerde güvenli önyüklemenin etkin olup olmadığı hakkında bilgi toplar. Bu bilgiler **SMS_Firmware** sınıfında depolanır (sürüm 1702 ' de kullanıma sunulmuştur) ve varsayılan olarak donanım envanterinde etkinleştirilir. Donanım envanteri hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Bir görev dizisine alt görev dizileri ekleme
Bu sürümde, görev dizileri arasında bir üst/alt ilişki oluşturan başka bir görev dizisi çalıştıran yeni bir görev dizisi adımı ekleyebilirsiniz. Bu, yeniden kullanabileceğiniz daha modüler görev dizileri oluşturmanızı sağlar.  

Bir görev dizisine bir alt görev sırası eklediğinizde aşağıdakileri göz önünde bulundurun:

- Üst ve alt görev dizileri, istemcinin çalıştırdığı tek bir ilkede etkili bir şekilde birleştirilir.
- Başka bir görev dizisinin üst öğesi olan bir alt görev sırası eklemek desteklenmez.
- Ortam geneldir. Örneğin, bir değişken üst görev sırası tarafından ayarlanır ve sonra alt görev sırası tarafından değiştirilirse, değişken ileri doğru ilerleyerek değişir. Benzer şekilde, alt görev sırası yeni bir değişken oluşturursa, değişken üst görev dizisindeki kalan adımlar için kullanılabilir.
- Durum iletileri, tek bir görev dizisi işlemi için normal başına gönderilir.
- Görev dizileri, bir alt görev sırası başlatıldığında, bu girişi yeni günlük girişleri ile Smsts. log dosyasına yazar.
- Configuration Manager sürüm 1704 Technical Preview sürümünde, alt görev sıraları herhangi bir pakete başvuruyorsa ve ana görev sırasını yazılım merkezi 'nden çalıştırırsanız, alt görev sırası çalıştırıldığında istemci paket içeriğini bulamaz. Bu senaryoda, görev dizisini medyadan çalıştırmanız gerekir (Önyükleme medyası, PXE vb.).  

    Alt görev dizisi **komut satırı Çalıştır** (herhangi bir paket başvurusu olmadan), **Biçim**, **BitLocker**vb. gibi adımları kullanıyorsa, görev dizisi yazılım merkezi 'nden başarıyla çalıştırılır.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Bir görev dizisine bir alt görev sırası eklemek için
1. Görev sırası düzenleyicisinde, **Ekle**' ye tıklayın, **genel**' i seçin ve **görev sırasını Çalıştır**' a tıklayın.
2. Alt görev sırasını seçmek için, **Araştır** ' a tıklayın.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Önyükleme görüntülerini geçerli Windows PE sürümü ile yeniden yükle
Seçilen bir önyükleme görüntüsünde **güncelleştirme dağıtım noktalarını** çalıştırdığınızda, artık Windows PE 'nin en son sürümünü (Windows ADK yükleme dizininden) önyükleme görüntüsüne yeniden yüklemeyi tercih edebilirsiniz. Sihirbazın **genel** sayfası, site sunucusunda yüklü Windows ADK sürümü, önyükleme GÖRÜNTÜSÜNDE Windows PE 'Nin KULLANıLDıĞı Windows ADK sürümü ve Configuration Manager istemcisinin sürümü hakkında bilgi sağlar. Önyükleme görüntüsünü yeniden yükleyip yükleyemeyeceğine karar vermenize yardımcı olması için bu bilgileri kullanabilirsiniz. Ayrıca **, önyükleme görüntüleri düğümünde önyükleme** görüntülerini görüntülediğinizde yeni bir sütun (**istemci sürümü**) eklenmiştir, böylece her önyükleme görüntüsünün kullandığı Configuration Manager istemcisinin hangi sürümünü kullandığını bilirsiniz.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Önyükleme görüntüsünü geçerli Windows PE sürümü ile yeniden yüklemek için

1. Configuration Manager konsolunda **yazılım kitaplığı** > **işletim sistemleri** > **önyükleme görüntüleri**' ne gidin.
2. Bir önyükleme görüntüsü seçin ve **dağıtım noktalarını güncelleştir**' e tıklayın.
3. Sihirbazın **genel** sayfasında, **yüklü Windows ADK 'den geçerli Windows PE sürümünü kullanarak önyükleme görüntüsünü yeniden yükle**' yi seçin.

## <a name="improvements-to-operating-system-deployment"></a>İşletim sistemi dağıtımı geliştirmeleri
Kullanıcı sesli geri bildirimlerinizin sonucu olan işletim sistemi dağıtımı için aşağıdaki geliştirmeleri yaptık.

- [İşletim sistemi görüntüleri için yeni **işletim sistemi sürümü** sütunu](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): **Işletim sistemi görüntüleri** ve **işletim sistemi yükseltme paketleri** düğümlerinde bilgileri görüntülediğinizde görüntünün işletim sistemi sürümünü görüntülemek **için işletim sistemi sürümü adlı yeni** bir sütun ekledik. Yalnızca içindeki ilk dizinin sürümü. WıM görüntülenir. Diğer dizinler için işletim sistemi sürümlerini gözden geçirmek üzere görüntünün **Ayrıntılar** sekmesine gidin.

- [Smsts. log dosyasında daha verimli oturum açma](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): Bu sürümden başlayarak, artık CCM_CIVersionInfo. PolicyId bilgileri için Smsts. log dosyasına girdi yazmıyoruz. Bu sürümden önce, bu bilgileri içeren çok sayıda giriş olabilir. Bu, günlük dosyasında daha fazla ilgili bilgiyi bulmayı zorlaştırır.
