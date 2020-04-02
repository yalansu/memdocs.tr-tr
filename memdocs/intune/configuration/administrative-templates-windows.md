---
title: Microsoft Intune-Azure 'da Windows 10 cihazları için şablonları kullanma | Microsoft Docs
description: Windows 10 cihazları için ayar grupları oluşturmak üzere Microsoft Intune ve uç nokta yöneticisinde Yönetim şablonlarını kullanın. Office programlarını, Microsoft Edge 'i, Internet Explorer 'daki güvenli özellikleri denetlemek, OneDrive 'a erişimi denetlemek, uzak masaüstü özelliklerini kullanmak, otomatik yürütmeye olanak tanımak, uzaktan yürütmeye izin vermek, güç yönetimi ayarlarını yapmak, HTTP yazdırmayı kullanmak için bir cihaz yapılandırma profilinde Bu ayarları kullanın. farklı Kullanıcı oturum açma seçeneklerini kullanın ve olay günlüğü boyutunu denetleyin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75ef2a03c9f42f0bda78af009f0fb563fbcedb75
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220070"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Microsoft Intune 'de Grup İlkesi ayarlarını yapılandırmak için Windows 10 şablonlarını kullanın

Kuruluşunuzdaki cihazları yönetirken, farklı cihaz gruplarına uygulanan ayar grupları oluşturmak istersiniz. Örneğin, birkaç cihaz grubunuz vardır. GroupA için belirli bir ayar kümesi atamak istersiniz. GroupB için farklı bir ayar kümesi atamak istersiniz. Ayrıca yapılandırabileceğiniz ayarların basit bir görünümünü de istiyorsunuz.

Bu görevi, Microsoft Intune **Yönetim Şablonları** kullanarak tamamlayabilirsiniz. Yönetim Şablonları, Microsoft Edge sürüm 77 ve üzeri, Internet Explorer, Microsoft Office programlar, Uzak Masaüstü, OneDrive, parolalar ve PIN 'Ler gibi özellikleri denetleyen yüzlerce ayarı içerir. Bu ayarlar, grup yöneticilerinin bulutu kullanarak grup ilkelerini yönetmesine olanak tanır.

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri

Windows ayarları Active Directory (AD) içindeki Grup İlkesi (GPO) ayarlarına benzerdir. Bu ayarlar Windows 'da yerleşiktir ve XML kullanan [ADMX ile desteklenen ayarlardır](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) . Office ve Microsoft Edge ayarları, ADMX kullanımına alınır ve [Office Yönetim şablonu dosyaları](https://www.microsoft.com/download/details.aspx?id=49030) ve [Microsoft Edge YÖNETIM şablonu dosyalarında](https://www.microsoftedgeinsider.com/enterprise)ADMX ayarlarını kullanır. Intune şablonları, %100 bulut tabanlı. Ayarları yapılandırmak için basit ve düz ileri bir yol sunar ve istediğiniz ayarları bulur.

**Yönetim Şablonları** , Intune 'da yerleşik olarak bulunur ve OMA-URI kullanımı dahil olmak üzere herhangi bir özelleştirme gerektirmez. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Windows 10 cihazlarınızı yönetmek için bu şablon ayarlarını tek durdurulmalı bir mağaza olarak kullanın.

Bu makalede, Windows 10 cihazları için şablon oluşturma adımları listelenir ve Intune 'da kullanılabilen tüm ayarların nasıl filtreleneceği gösterilir. Şablonu oluşturduğunuzda, bir cihaz yapılandırma profili oluşturur. Daha sonra bu profili, kuruluşunuzdaki Windows 10 cihazlarına atayabilir veya dağıtabilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce

- Bu ayarlardan bazıları Windows 10 sürüm 1703 (RS2/Build 15063) ile başlayarak kullanılabilir. Bazı ayarlar tüm Windows sürümlerinde bulunmaz. En iyi deneyim için, Windows 10 Enterprise sürüm 1903 (19H1/derleme 18362) ve daha yeni bir sürümü kullanmanız önerilir.

- Windows ayarları [Windows Ilkesi CSP 'leri](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)kullanır. CSP 'Ler Home, Professional, Enterprise vb. gibi farklı Windows sürümlerinde çalışır. CSP 'nin belirli bir sürümde çalışıp çalışmadığını görmek için [Windows Ilke CSP 'leri](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)' ne gidin.

## <a name="create-the-template"></a>Şablonu oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **Windows 10 ve üstünü**seçin.
    - **Profil**: **Yönetim Şablonları**seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı **yönetici şablonudur: Microsoft Edge 'de xyz ayarlarını yapılandıran Windows 10 yönetici şablonu**.
    - **Açıklama**: Profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**'yi seçin.

7. **Yapılandırma ayarları**' nda, cihaza uygulanan ayarları (**bilgisayar yapılandırması**) ve kullanıcılara uygulanan ayarları **(Kullanıcı Yapılandırması**) yapılandırın:

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune Endpoint Manager 'daki kullanıcılara ve cihazlara ADMX şablonu ayarlarını uygulama](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. **Bilgisayar yapılandırması**' nı seçtiğinizde, ayar kategorileri gösterilir. Kullanılabilir ayarları görmek için herhangi bir kategori seçebilirsiniz.

    Örneğin, Internet Explorer 'a uygulanan tüm cihaz ayarlarını görmek için **Internet explorer** > **Windows bileşenleri** > **bilgisayar yapılandırması** ' nı seçin:

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune Endpoint Manager 'da Internet Explorer için uygulanan tüm cihaz ayarlarını görüntüleyin](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. Her cihaz ayarını görmek için **Tüm ayarlar** ' ı da seçebilirsiniz. Daha fazla ayar görmek için önceki ve sonraki okları kullanmak üzere aşağı kaydırın:

    > [!div class="mx-imgBorder"]
    > ![, ayarların örnek listesini görün ve önceki ve sonraki düğmeleri kullanın](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Herhangi bir ayarı seçin. Örneğin, **Office**üzerinde filtreleme yapın ve **Kısıtlanmış taramayı etkinleştir**' i seçin. Ayarın ayrıntılı bir açıklaması gösterilir. **Etkin**, **devre dışı**seçeneğini belirleyin veya ayarı **Yapılandırılmadı** (varsayılan) olarak bırakın. Ayrıntılı açıklama Ayrıca **etkin**, **devre dışı**veya **yapılandırılmamış**' ı seçtiğinizde ne olacağını açıklar.

    > [!TIP]
    > Intune 'daki Windows ayarları, Yerel Grup İlkesi Düzenleyicisi gördüğünüz şirket içi Grup İlkesi yoluyla bağıntılı (`gpedit`)

11. Değişikliklerinizi kaydetmek için **Tamam**’ı seçin.

    Ayarlar listesinden ilerleyin ve ortamınızda istediğiniz ayarları yapılandırın. Bazı örnekler şunlardır:

    - Word ve Excel dahil farklı Microsoft Office programlarındaki VBA makrolarını işlemek için **VBA makro bildirimi ayarları** ayarını kullanın.
    - Internet Explorer 'dan İndirmeleri izin vermek veya engellemek için **Dosya Indirmelerine Izin ver** ayarını kullanın.
    - Cihazlar uyku modundan çıktığında kullanıcılara parola istemek için bir **bilgisayar uyandığında (prize takılıyken) parola gerektir '** i kullanın.
    - Kullanıcıların Internet Explorer 'dan imzasız ActiveX denetimlerini indirmesini engellemek için **Imzasız ActiveX denetimlerini indir** ayarını kullanın.
    - Kullanıcıların cihazda sistem geri yükleme çalıştırmasını sağlamak veya bunu engellemek için **sistemi geri yüklemeyi** kapat ayarını kullanın.
    - Kullanıcıların başka bir tarayıcıdan Microsoft Edge 'e sık kullanılanları içeri aktarmaya izin vermek veya bunları engellemek için **sık kullanılanları içeri aktarmaya Izin ver** ayarını kullanın.
    - Ve çok daha fazlası...

12. **İleri**'yi seçin.
13. **Kapsam etiketleri** ' nde (isteğe bağlı), profili `US-NC IT Team` veya `JohnGlenn_ITDepartment`gıbı belirli BT gruplarına filtrelemek için bir etiket atayın. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](..//fundamentals/scope-tags.md).

    **İleri**'yi seçin.

14. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**'yi seçin.

15. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Cihaz, yapılandırma güncelleştirmelerini bir dahaki sefer denetlediğinde, yapılandırdığınız ayarlar uygulanır.

## <a name="find-some-settings"></a>Bazı ayarları bul

Bu şablonlarda yüzlerce ayar bulunur. Belirli ayarları bulmayı kolaylaştırmak için yerleşik özellikleri kullanın:

- Şablonunuzda, listeyi sıralamak için **Ayarlar**, **durum**, **ayar türü**veya **yol** sütunlarını seçin. Örneğin, **yol** sütununu seçin ve `Microsoft Excel` yolundaki ayarları görmek için bir sonraki oku kullanın:

- Şablonunuzda, belirli ayarları bulmak için **arama** kutusunu kullanın. Ayar veya yola göre arama yapabilirsiniz. Örneğin, `copy`araması yapın. `copy` olan tüm ayarlar gösterilir:

  > [!div class="mx-imgBorder"]
  > Intune 'da yönetim şablonlarındaki tüm cihaz ayarlarını göstermek için kopyalama için arama ![](./media/administrative-templates-windows/search-copy-settings.png) 

  Başka bir örnekte, `microsoft word`için arama yapın. Microsoft Word programı için ayarlayabileceğiniz ayarları görürsünüz. Şablonunuza ekleyebileceğiniz Internet Explorer ayarlarını görmek için `explorer` aratın.

## <a name="next-steps"></a>Sonraki adımlar

Şablon oluşturuldu, ancak henüz bir şey yapmamış olabilir. Sonra, [şablonu (profil olarak da bilinir) atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

[Yönetim şablonlarını kullanarak Office 365](administrative-templates-update-office.md)' i güncelleştirin.

[Öğretici: Windows 10 cihazlarında ADMX şablonları ve Microsoft Intune Grup İlkesi yapılandırmak için bulutu kullanın](tutorial-walkthrough-administrative-templates.md)