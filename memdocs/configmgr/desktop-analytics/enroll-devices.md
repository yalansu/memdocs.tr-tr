---
title: Masaüstü Analizi 'nde cihazları kaydetme
titleSuffix: Configuration Manager
description: Masaüstü Analizi 'nde cihazları kaydetmeyi öğrenin.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9cca066d389ea8d3847737651f4994977a5e2f5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723617"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Masaüstü Analizi 'nde cihazları kaydetme

Configuration Manager masaüstü analizine [bağladığınızda](connect-configmgr.md) , cihazları masaüstü analizine kaydetmek için ayarları yapılandırırsınız. Bu ayarları dilediğiniz zaman değiştirebilirsiniz. Ayrıca cihazların güncel olduğundan emin olun.

## <a name="update-devices"></a>Cihazları güncelleştirme

Masaüstü Analizi iki ana Windows bileşeni kullanır:

- **Uyumluluk bileşeni**: uyumluluk bileşeni (**Appraiser**), Windows 10 ' un en son sürümleriyle uyumluluk durumunu değerlendirmek için Windows cihazında tanılamayı çalıştırır.

- **Bağlı kullanıcı deneyimleri ve telemetri hizmeti**: Windows Tanılama verileri etkinken, bağlı kullanıcı deneyimi ve telemetri hizmeti (**diagtrack**) sistem, uygulama ve sürücü verilerini toplar. Microsoft bu verileri analiz eder ve Masaüstü analizi aracılığıyla sizi geri paylaşır.

Masaüstü analiziyle ilgili en iyi deneyimi elde etmek için bu bileşenlerin en son sürümünü yükler.

Aşağıdaki tabloda desteklenen işletim sistemi sürümlerindeki her bir bileşene ilişkin güncelleştirmeler listelenmektedir:

| İşletim sistemi sürümü | Appraiser | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | Dahil edilen <sup> [notta 1](#bkmk_note1)</sup> | [En son birikimli güncelleştirme](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | Dahil | [En son birikimli güncelleştirme](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | Dahil | [En son birikimli güncelleştirme](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | Dahil | [En son birikimli güncelleştirme](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | Dahil | [En son birikimli güncelleştirme](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup> [Note 2](#bkmk_note2)</sup> | [En son aylık toplu](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup> [Note 3](#bkmk_note3)</sup> | [En son aylık toplu](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Bu güncelleştirmeleri otomatik olarak yüklemek için Configuration Manager kullanın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini dağıtma](../sum/deploy-use/deploy-software-updates.md).
>
> Uyumluluk güncelleştirmelerini ilk kez yükledikten sonra cihazları yeniden başlatın.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a>Note 1: Windows 10

Windows 10 varsayılan olarak bu bileşenleri içerdiğinde, Windows 10 cihazlarında masaüstü analizinin tüm işlevlerini almak için en son birikimli güncelleştirme gerekir. Örneğin, cihazı en son işletim sistemi sürümüne karşı uyumluluğu değerlendirmek ve dağıtımlar ve kayıt durumu hakkında neredeyse gerçek zamanlı bilgileri almak için.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a>2. nota: Windows 8.1

Microsoft bu bileşen için güncelleştirmeleri düzenli olarak arttırır, ancak ilişkili KB numarası değişmez. Her zaman güncelleştirmenin en son sürümüne sahip olduğunuzdan emin olun.

Bu bileşen, Windows Müşteri Deneyimini Geliştirme Programı katılan Windows 8.1 sistemlerde tanılama çalıştırır. Bu Tanılamalar, Windows 10 ' a yükseltirken uyumluluk sorunlarıyla karşılaşıp olup olmadığınızı belirlemenize yardımcı olur.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a>3. göz: Windows 7

Kuruluşunuz, Windows 7 cihazlarına "aylık kalite toplaması" güncelleştirmelerini uygulayamazsa ve yalnızca "yalnızca güvenlik" güncelleştirmelerini uygularsa, [KB 2952664 yerine geçen güncelleştirmeler listesindeki](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c)bazı "yalnızca güvenlik" güncelleştirmelerini bulacaksınız. Bu yeni güncelleştirmeleri, KB 2952664 yerine yükleyebilirsiniz.

> [!NOTE]
> Windows 8.1 için, Microsoft yalnızca "aylık kalite toplaması" güncelleştirmelerinin bir parçası olarak KB 2976978 ' ü yeniden düzeltir.

## <a name="device-enrollment"></a>Cihaz kaydı

Masaüstü Analizi hizmeti 'nin yüklenecek bir Aracısı yok. Cihaz kaydı, izlemek istediğiniz cihazlarda ayarları yapılandırmanızı gerektirir. Bu ayarlar, cihazın hangi masaüstü analizi örneği tarafından gönderilmesi gerektiğini ve diğer yapılandırma seçeneklerini denetlemelidir.

> [!Note]  
> Daha önce Windows Analytics kullandıysanız, bu masaüstü analizi için aynı çalışma alanını kullanın. Cihazları daha önce Windows Analytics 'e kaydettiğiniz masaüstü analizlerini yeniden kaydetmeniz gerekir.
>
> Her Azure AD kiracısı için yalnızca bir masaüstü Analizi çalışma alanınız olabilir. Cihazlar yalnızca bir çalışma alanına Tanılama verileri gönderebilir.  

Configuration Manager, bu ayarları yönetmek ve istemcilere dağıtmak için tümleşik bir deneyim sağlar. En iyi deneyim için Configuration Manager kullanın.

Configuration Manager masaüstü analizine bağladığınızda, cihazları kaydetmek için ayarları yapılandırırsınız. Daha fazla bilgi için bkz. [Masaüstü analiziyle Configuration Manager bağlama](connect-configmgr.md#bkmk_connect).

Bu ayarları değiştirmek için aşağıdaki yordamı kullanın:

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure hizmetleri** düğümünü seçin. Masaüstü Analizi bağlantısını seçin ve şeritte **Özellikler** ' i seçin.

2. **Tanılama verileri** sayfasında, aşağıdaki ayarlarda gereken değişiklikleri yapın:  

    - **TICARI kimlik**: Bu değer, kuruluşunuzun kimliğiyle otomatik olarak doldurulur. Aksi takdirde, proxy sunucunuzun devam etmeden önce tüm gerekli [uç noktalara](enable-data-sharing.md#endpoints) izin verecek şekilde yapılandırıldığından emin olun. Ayrıca, ticari KIMLIĞINIZI [Masaüstü Analizi portalından](monitor-connection-health.md#bkmk_ViewCommercialID)el ile de alabilirsiniz.

    - **Windows 10 tanılama veri düzeyi**: daha fazla bilgi için bkz. [Tanılama veri düzeyleri](enable-data-sharing.md#diagnostic-data-levels).  

    - **Tanılama verilerinde cihaz adına Izin ver**: daha fazla bilgi için bkz. [Cihaz adı](#device-name).  

    Bu sayfada değişiklik yaptığınızda, **kullanılabilir işlevsellik** sayfasında, seçilen Tanılama verileri ayarlarına sahip masaüstü Analizi işlevselliğinin önizlemesi gösterilir.  

3. **Masaüstü Analizi bağlantısı** sayfasında, aşağıdaki ayarlarda gereken değişiklikleri yapın:

    - **Görünen ad**: Masaüstü Analizi portalı bu adı kullanarak bu Configuration Manager bağlantıyı görüntüler.  

    - **Hedef koleksiyon**: Bu koleksiyon, ticari kimliğiniz ve tanılama veri ayarlarınızla Configuration Manager yapılandırdığı tüm cihazları içerir. Bu, Configuration Manager masaüstü Analizi hizmetine bağlanan cihazların eksiksiz kümesidir.  

    - **Hedef koleksiyondaki cihazlar giden iletişim için Kullanıcı tarafından kimliği doğrulanmış bir proxy kullanır**: varsayılan olarak bu değer **Hayır**' dır. Ortamınızda gerekliyse, **Evet**olarak ayarlayın. Daha fazla bilgi için bkz. [proxy sunucusu kimlik doğrulaması](enable-data-sharing.md#proxy-server-authentication).

    - **Masaüstü analiziyle eşitlenmek üzere belirli koleksiyonlar seçin**: **hedef koleksiyon** hiyerarşinizden ek koleksiyonlar eklemek için **Ekle** ' yi seçin. Bu koleksiyonlar, dağıtım planlarıyla gruplamak için masaüstü Analizi portalında kullanılabilir. Pilot ve pilot dışlama koleksiyonlarını eklediğinizden emin olun.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Bu koleksiyonlar, üyelik değişiklikleri olarak eşitlemeye devam eder. Örneğin, Dağıtım planınız bir Windows 7 üyelik kuralıyla bir koleksiyon kullanır. Bu cihazlar Windows 10 ' a yükseltile, ve Configuration Manager koleksiyon üyeliğini değerlendirirken, bu cihazlar koleksiyon ve dağıtım planından çıkar.

### <a name="windows-settings"></a>Windows ayarları

Configuration Manager, cihazları masaüstü analizine kaydettiğinde, cihazı masaüstü analizi için yapılandırmak üzere Windows ilkelerini ayarlar. Çoğu durumda bu ayarları yapılandırmak için yalnızca Configuration Manager kullanın. Bu ayarları etki alanı Grup İlkesi nesnelerinde da uygulamayın.

Daha fazla bilgi için bkz. [Masaüstü Analizi Için Grup İlkesi ayarları](group-policy-settings.md).

### <a name="device-name"></a>Cihaz adı

Windows 10, sürüm 1803 ' den başlayarak, cihaz adı artık varsayılan olarak toplanmaz. Tanılama verileriyle cihaz adının toplanması ayrı bir kabul gerektirir. Cihaz adı olmadan, Windows 'un yeni bir sürümüne yükseltmeyi değerlendirirken hangi cihazların dikkat gerektirdiğini belirlemeniz daha zordur.

Cihaz adı göndermezseniz, masaüstü analizlerinin "bilinmiyor" olarak görünmesi gerekir:

!["Bilinmeyen" adları gösteren masaüstü Analizi cihaz listesi](media/unknown-device-name.png)

Bu seçeneği yapılandırmak için masaüstü analizlerinin Configuration Manager ayarlarında bir seçenek vardır: **Tanılama verilerinde cihaz adına Izin ver**. Bu Configuration Manager ayarı, **allowdevicenameintelemetry** [Windows ilke ayarını](group-policy-settings.md)denetler.

### <a name="conflict-resolution"></a>Çakışma çözümleme

Genel olarak, masaüstü Analizi ayarlarını ve kaydını hedeflemek için Configuration Manager koleksiyonları kullanın. Cihazları koleksiyona dahil etmek veya hariç tutmak için doğrudan üyeliği veya sorguları kullanın. Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](../core/clients/manage/collections/create-collections.md).

Configuration Manager yalnızca bir değer yoksa, Windows ayarlarını yapılandırır. Benzersiz bir cihaz grubu için farklı ayarlar yapılandırmanız gerekiyorsa, [Grup İlkesi](group-policy-settings.md)kullanabilirsiniz. Grup İlkesi tarafından hedeflenen ayarlar Configuration Manager ayarlarından önceliklidir.

Tanılama veri düzeyini yapılandırırken, cihazın üst sınırını ayarlarsınız. Varsayılan olarak, Windows 10, sürüm 1803 ve üzeri sürümlerde, kullanıcılar daha düşük bir düzey ayarlamayı seçebilirler. Bu davranışı Grup İlkesi ayarını kullanarak denetleyebilir, **telemetri katılım ayarı Kullanıcı arabirimini yapılandırın**. Daha fazla bilgi için bkz. [Masaüstü Analizi Için Grup İlkesi ayarları](group-policy-settings.md).

### <a name="proxy-settings"></a>Proxy ayarları

Kuruluşunuz internet erişimi için proxy sunucusu kimlik doğrulamasını kullanıyorsa, veya cihazlarınızı doğru bir şekilde yapılandırdığınızdan emin olun. Daha fazla bilgi için bkz. [proxy sunucusu kimlik doğrulaması](enable-data-sharing.md#proxy-server-authentication).

## <a name="next-steps"></a>Sonraki adımlar

Masaüstü analizinden dağıtım planları oluşturmak için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Dağıtım planları oluşturma](create-deployment-plans.md)
