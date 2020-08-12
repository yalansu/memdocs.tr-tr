---
title: İşletim sistemi dağıtımı için kullanıcı deneyimleri
titleSuffix: Configuration Manager
description: Configuration Manager içinde işletim sistemi dağıtımı için görev dizisi ilerleme durumu ve medya Sihirbazı gibi kullanıcı deneyimleri hakkında bilgi edinin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ad20f80f4727fe18947bed05ded6e7b107fab12
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124093"
---
# <a name="user-experiences-for-os-deployment"></a>İşletim sistemi dağıtımı için kullanıcı deneyimleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

[Bir görev dizisini dağıttıktan](../deploy-use/deploy-a-task-sequence.md)sonra, senaryoya bağlı olarak, kullanıcıların dağıtımla etkileşim kurması için farklı yollar vardır. Bu makale, işletim sistemi dağıtımları ile ilgili başlıca kullanıcı deneyimlerini ve bunları nasıl yapılandırakullanabileceğinizi gösterir:

- Yüksek etkili bir dağıtım için yazılım merkezi Kullanıcı bildirimi
- Örnek bir PXE önyükleme deneyimi
- Medyadan görev sırası Sihirbazı
- Görev sırası çalıştırıldığında ilerleme penceresi
- Görev sırası başarısız olduğunda hata penceresi

## <a name="software-center"></a>Yazılım Merkezi

Yüksek etkili bir dağıtım için Software Center 'ın görüntülediği iletiyi özelleştirebilirsiniz. Kullanıcı işletim sistemi dağıtımını yazılım merkezi 'nde açtığında, aşağıdaki pencereye benzer bir ileti görürler:

![Yazılım Merkezi 'nden son kullanıcıya özelleştirilmiş görev sırası bildirimi](../media/user-notification-enduser.png)

Bu penceredeki iletiyi özelleştirme hakkında daha fazla bilgi için bkz. [yüksek riskli dağıtımlar için özel bildirim oluşturma](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

Ayrıca, pencerenin üst kısmındaki kuruluş adını da özelleştirebilirsiniz. (Yukarıdaki örnek, varsayılan değerini gösterir `IT Organization` ). **Bilgisayar Aracısı** grubundaki **kuruluş adı** istemci ayarını değiştirin. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak Için yazılım merkezi 'Ni kullanma](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Farklı donanım modelleriyle PXE için farklı deneyimler vardır. Ağı önyüklemek için, UEFı tabanlı cihazlar genellikle `Enter` anahtarı kullanır ve BIOS tabanlı cihazlar bu `F12` anahtarı kullanır.

Aşağıdaki örnek, Hyper-V Gen1 (BIOS) PXE deneyimini göstermektedir:

![Hyper-V sanal makinesinden örnek BIOS PXE ekranı](media/hyperv-pxe.png)

Cihaz PXE aracılığıyla başarılı bir şekilde önyüklendiğinde, önyüklenebilir medyada benzer şekilde davranır. Daha fazla bilgi için, [görev dizisi Sihirbazı](#task-sequence-wizard)'nda bir sonraki bölüme bakın.

Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

> [!WARNING]
> PXE dağıtımlarını kullanır ve ilk önyükleme aygıtı olarak ağ bağdaştırıcısı ile cihaz donanımını yapılandırırsanız, bu cihazlar Kullanıcı etkileşimi olmadan bir işletim sistemi dağıtımı görev sırasını otomatik olarak başlatabilir. Dağıtım doğrulaması bu yapılandırmayı yönetmez. Bu yapılandırma işlemi basitleştirecek ve kullanıcı etkileşimini azaltmasına karşın, yanlışlıkla yeniden görüntü için cihazı daha fazla riske koyar.

## <a name="task-sequence-wizard"></a>Görev sırası Sihirbazı

[Görev sırası medyası](../deploy-use/create-task-sequence-media.md)kullandığınızda, görev sırası Sihirbazı işleme kılavuzluk etmek için çalışır.

### <a name="welcome-to-the-task-sequence-wizard"></a>Görev sırası sihirbazına hoş geldiniz

![Görev sırası sihirbazının ana sayfasının ekran görüntüsü](media/welcome-task-sequence-wizard.png)

- Medyayı parolayla koruduğunuzda, kullanıcının bu hoş geldiniz sayfasında parolayı girmesi gerekir.

- Statik bir IP adresi veya diğer özel ağ ayarlarını belirtmek için **ağ ayarlarını yapılandır** ' ı seçin. Aksi takdirde, cihaz varsayılan olarak DHCP kullanır.

- Ağınız için bir ara sunucu gerekiyorsa, **proxy ayarlarını yapılandır**' ı seçin.

### <a name="select-a-task-sequence-to-run"></a>Çalıştırılacak görev sırasını seçin

Cihaza birden fazla görev sırası dağıtırsanız, bir görev dizisi seçmek için bu sayfayı görürsünüz. Görev diziniz için kullanıcıların anlayabilmesi için bir ad ve açıklama kullandığınızdan emin olun.

![Görev sırası sihirbazının görev dizisi seçimi sayfasının ekran görüntüsü](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Görev sırası değişkenlerini Düzenle

Herhangi bir görev dizisi değişkeni boş değerler içeriyorsa, sihirbaz değişken değerlerini düzenlemek için bir sayfa gösterir.

![Görev sırası Sihirbazı 'nın görev sırası değişkenlerini düzenleme sayfasının ekran görüntüsü](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Başlatma öncesi komutları

Bir başlatma öncesi komutu çalıştırmak için görev dizisi medyası veya önyükleme görüntülerini özelleştirebilirsiniz. Bir başlatma öncesi komutu, görev dizisi başlamadan önce çalışır. Aşağıdaki eylemler daha yaygın olanlardır:

- Kullanıcıdan bilgisayar adı gibi dinamik değerler iste
- Ağ yapılandırmasını belirtin
- Kullanıcı cihaz benzeşimini ayarla

Başlatma öncesi komutu, bir komut dosyası veya program ile belirttiğiniz bir komut satırdır. Kullanıcı deneyimi, bu betik veya program için benzersizdir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Görev dizisi ortamı için başlatma öncesi komutları](prestart-commands-for-task-sequence-media.md)
- [Önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md#customization)
- [Görev sırası medyası](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Görev sırası ilerleme durumu

Görev sırası çalıştırıldığında, **yükleme ilerleme durumu** penceresini görüntüler:

![Görev sırası Ilerleme penceresi örneği](media/task-sequence-progress.png)

- Bu pencere her zaman en üstte; taşıyabilirsiniz, ancak onu kapatabilir veya en aza indirmiş olursunuz.

- Pencerenin üst kısmında kuruluş adını özelleştirebilirsiniz. (Yukarıdaki örnek, varsayılan değerini gösterir `IT Organization` ). **Bilgisayar Aracısı** grubundaki **kuruluş adı** istemci ayarını değiştirin. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#computer-agent).

    > [!TIP]
    > Görev sırası bu değeri salt- [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName)değişkeni içinde depolar.

- Alt başlığı özelleştirebilirsiniz. (Yukarıdaki örnek, varsayılan değeri gösterir `Running: <task sequence name>` .) Görev dizisinin özelliklerinde, ilerleme durumu bildirim metni için **özel metin kullanma** seçeneğini belirleyin. En fazla 255 karakter sağlar.

- **Çalıştırma eylemi**: ilk satır, geçerli görev dizisi adımının adını gösterir. Aşağıdaki ilerleme çubuğu, görev dizisinin genel tamamlanmasını gösterir.

- İkinci satır yalnızca daha ayrıntılı ilerleme sağlayan bazı adımları gösterir.

- Görev dizisinin ilerleme durumunu görüntüleyeceğini denetlemek için [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) görev dizisi değişkenini kullanın.

    İlerleme penceresini tamamen devre dışı bırakmak için, görev dizisi dağıtımının **Kullanıcı deneyimi** sayfasında **görev dizisi ilerlemesini gösterme** seçeneğini devre dışı bırakın.

Sürüm 2002 ' den başlayarak, görev sırası ilerleme durumu penceresi aşağıdaki geliştirmeleri içerir:<!--5932692-->

- Geçerli adım numarasını, toplam adım sayısını ve tamamlanma yüzdesini gösterir

- Kuruluş adını tek bir satırda daha iyi göstermek için daha fazla alan sağlamak üzere pencerenin genişliği artırılmıştır

![Örnek görev sırası ilerleme penceresi](media/2356386-task-sequence-progress.png)

Varsayılan olarak, görev dizisi ilerleme durumu penceresi varolan metni kullanır. Hiçbir değişiklik yaparsanız, sürüm 1910 ve önceki sürümlerde olduğu gibi çalışmaya devam eder. Yeni ilerleme bilgilerini göstermek için, [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel)görev dizisi değişkenini belirtin.

Tamamlanan sayı ve yüzde yalnızca genel rehberlik amaçlarına yöneliktir. Bu değerler görev dizisindeki adımların toplam sayısını temel alır. Görev dizisi mantığına göre koşullu olarak çalışan adımlarla daha karmaşık bir görev sırası için ilerleme, doğrusal olmayan bir durum olabilir.

Toplam adımların sayısı görev dizisine aşağıdaki öğeleri içermez:

- Gruplandıran. Bu öğe, bir adımın kendisi değil diğer adımlar için bir kapsayıcıdır.

- **Görev dizisi adımını Çalıştır** adımının örnekleri. Bu adım, diğer adımlar için bir kapsayıcıdır.

- Açıkça devre dışı bırakabilmeniz gereken adımlar. Devre dışı bir adım görev sırası sırasında çalışmaz.

- Sürüm 2006 ' den başlayarak, devre dışı bırakılmış bir gruptaki etkin adımları saymaz.<!--6448412--> Sürüm 2002 ' de, devre dışı bırakılmış bir gruptaki etkin adımlar, yine de toplam sayıma dahil edilmiştir.

## <a name="task-sequence-error"></a>Görev sırası hatası

Görev sırası başarısız olursa, **görev dizisi hata** penceresini görüntüler.

![Örnek görev dizisi hata penceresi](media/task-sequence-error.png)

- Üstbilgi bilgilerini görev sırası ilerleme penceresiyle aynı şekilde özelleştirebilirsiniz.

- Görev dizisinin adını, bir hata kodunu ve kullanıcılar için genel bir iletiyi görüntüler. Örnek: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- Pencere, bir zaman aşımı süresinden sonra otomatik olarak kapanır. Varsayılan olarak, bu zaman aşımı 15 dakikadır. Bu değeri, [Smstserrordialogtimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout)görev dizisi değişkeniyle özelleştirebilirsiniz.
