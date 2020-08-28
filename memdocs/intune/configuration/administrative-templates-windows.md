---
title: Microsoft Intune-Azure 'da Windows 10 cihazları için şablonları kullanma | Microsoft Docs
description: Windows 10 cihazları için ayar grupları oluşturmak üzere Microsoft Intune ve uç nokta yöneticisinde Yönetim şablonlarını kullanın. Office programlarını, Microsoft Edge 'i güvenli Internet Explorer, OneDrive 'a erişme, uzak masaüstü kullanma, otomatik yürütmeye olanak sağlama, güç yönetimi ayarlarını belirleme, HTTP yazdırmayı kullanma, Kullanıcı oturum açma denetimi ve olay günlüğü boyutunu değiştirme için bir cihaz yapılandırma profilinde Bu ayarları kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: faa217bd5e56a304b80298f2039ad3c541612e54
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992812"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Microsoft Intune 'de Grup İlkesi ayarlarını yapılandırmak için Windows 10 şablonlarını kullanın

Kuruluşunuzdaki cihazları yönetirken, farklı cihaz gruplarına uygulanan ayar grupları oluşturmak istersiniz. Örneğin, birkaç cihaz grubunuz vardır. GroupA için belirli bir ayar kümesi atamak istersiniz. GroupB için farklı bir ayar kümesi atamak istersiniz. Ayrıca yapılandırabileceğiniz ayarların basit bir görünümünü de istiyorsunuz.

Bu görevi, Microsoft Intune **Yönetim Şablonları** kullanarak tamamlayabilirsiniz. Yönetim Şablonları, Microsoft Edge sürüm 77 ve üzeri, Internet Explorer, Microsoft Office programları, Uzak Masaüstü, OneDrive, parolalar, PIN ve daha fazlasını denetleyen binlerce ayarı içerir. Bu ayarlar, grup yöneticilerinin bulutu kullanarak grup ilkelerini yönetmesine olanak tanır.

Bu özellik şu platformlarda geçerlidir:

- Windows 10 ve üzeri

Windows ayarları Active Directory (AD) içindeki Grup İlkesi (GPO) ayarlarına benzerdir. Bu ayarlar Windows 'da yerleşiktir ve XML kullanan [ADMX ile desteklenen ayarlardır](/windows/client-management/mdm/understanding-admx-backed-policies) . Office ve Microsoft Edge ayarları, ADMX kullanımına alınır ve [Office Yönetim şablonu dosyaları](https://www.microsoft.com/download/details.aspx?id=49030) ve [Microsoft Edge YÖNETIM şablonu dosyalarında](https://www.microsoftedgeinsider.com/enterprise)ADMX ayarlarını kullanır. Intune şablonları, %100 bulut tabanlı. Ayarları yapılandırmak için basit ve düz ileri bir yol sunar ve istediğiniz ayarları bulur.

**Yönetim Şablonları** , Intune 'da yerleşik olarak bulunur ve OMA-URI kullanımı dahil olmak üzere herhangi bir özelleştirme gerektirmez. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Windows 10 cihazlarınızı yönetmek için bu şablon ayarlarını tek durdurulmalı bir mağaza olarak kullanın.

Bu makalede, Windows 10 cihazları için şablon oluşturma adımları listelenir ve Intune 'da kullanılabilen tüm ayarların nasıl filtreleneceği gösterilir. Şablonu oluşturduğunuzda, bir cihaz yapılandırma profili oluşturur. Daha sonra bu profili, kuruluşunuzdaki Windows 10 cihazlarına atayabilir veya dağıtabilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce

- Bu ayarlardan bazıları Windows 10 sürüm 1709 (RS2/Build 15063) ile başlayarak kullanılabilir. Bazı ayarlar tüm Windows sürümlerinde bulunmaz. En iyi deneyim için, Windows 10 Enterprise sürüm 1903 (19H1/derleme 18362) ve daha yeni bir sürümü kullanmanız önerilir.

- Windows ayarları [Windows Ilkesi CSP 'leri](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)kullanır. CSP 'Ler Home, Professional, Enterprise vb. gibi farklı Windows sürümlerinde çalışır. CSP 'nin belirli bir sürümde çalışıp çalışmadığını görmek için [Windows Ilke CSP 'leri](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)' ne gidin.

## <a name="create-the-template"></a>Şablonu oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **Windows 10 ve üstünü**seçin.
    - **Profil**: **Yönetim Şablonları**seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı **yönetici şablonudur: Microsoft Edge 'de xyz ayarlarını yapılandıran Windows 10 yönetici şablonu**.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda **Tüm** ayarlar ' ı seçerek tüm ayarların alfabetik bir listesini görüntüleyin. Ya da, cihazlara (**bilgisayar yapılandırması**) uygulanan ayarları ve kullanıcılara uygulanan ayarları **(Kullanıcı Yapılandırması**) yapılandırın:

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune Endpoint Manager 'daki kullanıcılara ve cihazlara ADMX şablonu ayarlarını uygulama](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. **Tüm ayarlar**' ı seçtiğinizde, her ayar listelenir. Daha fazla ayar görmek için önceki ve sonraki okları kullanmak üzere aşağı kaydırın:

    > [!div class="mx-imgBorder"]
    > ![Ayarların örnek listesini görüntüleyin ve önceki ve sonraki düğmeleri kullanın](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

9. Herhangi bir ayarı seçin. Örneğin, **Office**üzerinde filtreleme yapın ve **Kısıtlanmış taramayı etkinleştir**' i seçin. Ayarın ayrıntılı bir açıklaması gösterilir. **Etkin**, **devre dışı**seçeneğini belirleyin veya ayarı **Yapılandırılmadı** (varsayılan) olarak bırakın. Ayrıntılı açıklama Ayrıca **etkin**, **devre dışı**veya **yapılandırılmamış**' ı seçtiğinizde ne olacağını açıklar.

    > [!TIP]
    > Intune 'daki Windows ayarları Yerel Grup İlkesi Düzenleyicisi () ' de gördüğünüz şirket içi Grup İlkesi yoluyla bağıntılı `gpedit`

10. **Bilgisayar yapılandırması** veya **Kullanıcı Yapılandırması**' nı seçtiğinizde, ayar kategorileri gösterilir. Kullanılabilir ayarları görmek için herhangi bir kategori seçebilirsiniz.

    Örneğin, **Computer configuration**  >  Internet Explorer 'a uygulanan tüm cihaz ayarlarını görmek için bilgisayar yapılandırması**Windows bileşenleri**  >  **Internet Explorer** ' ı seçin:

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune Endpoint Manager 'da Internet Explorer için uygulanan tüm cihaz ayarlarını görüntüleyin](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

11. Değişikliklerinizi kaydetmek için **Tamam**’ı seçin.

    Ayarlar listesinden ilerleyin ve ortamınızda istediğiniz ayarları yapılandırın. İşte bazı örnekler:

    - Word ve Excel dahil farklı Microsoft Office programlarındaki VBA makrolarını işlemek için **VBA makro bildirimi ayarları** ayarını kullanın.
    - Internet Explorer 'dan İndirmeleri izin vermek veya engellemek için **Dosya Indirmelerine Izin ver** ayarını kullanın.
    - Cihazlar uyku modundan çıktığında kullanıcılara parola istemek için bir **bilgisayar uyandığında (prize takılıyken) parola gerektir '** i kullanın.
    - Kullanıcıların Internet Explorer 'dan imzasız ActiveX denetimlerini indirmesini engellemek için **Imzasız ActiveX denetimlerini indir** ayarını kullanın.
    - Kullanıcıların cihazda sistem geri yükleme çalıştırmasını sağlamak veya bunu engellemek için **sistemi geri yüklemeyi** kapat ayarını kullanın.
    - Kullanıcıların başka bir tarayıcıdan Microsoft Edge 'e sık kullanılanları içeri aktarmaya izin vermek veya bunları engellemek için **sık kullanılanları içeri aktarmaya Izin ver** ayarını kullanın.
    - Ve çok daha fazlası...

12. **İleri**’yi seçin.
13. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](..//fundamentals/scope-tags.md).

    **İleri**’yi seçin.

14. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    Profil kullanıcı gruplarına atanırsa, yapılandırılan ADMX ayarları kullanıcının kaydettiği herhangi bir cihaza uygulanır ve oturum açar. Profil cihaz gruplarına atanırsa, yapılandırılan ADMX ayarları, bu cihazda oturum açan tüm kullanıcılara uygulanır. Bu atama, ADMX ayarı bir bilgisayar yapılandırması ( `HKEY_LOCAL_MACHINE` ) veya bir Kullanıcı Yapılandırması () ise gerçekleşir `HKEY_CURRENT_USER` . Bazı ayarlarla, bir kullanıcıya atanan bir bilgisayar ayarı bu cihazdaki diğer kullanıcıların deneyimini de etkileyebilir.

    Daha fazla bilgi için bkz. [Kullanıcı grupları ve cihaz grupları karşılaştırması](device-profile-assign.md#user-groups-vs-device-groups).

    **İleri**’yi seçin.

15. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

Cihaz, yapılandırma güncelleştirmelerini bir dahaki sefer denetlediğinde, yapılandırdığınız ayarlar uygulanır.

## <a name="find-some-settings"></a>Bazı ayarları bul

Bu şablonlarda binlerce ayar mevcuttur. Belirli ayarları bulmayı kolaylaştırmak için yerleşik özellikleri kullanın:

- Şablonunuzda, listeyi sıralamak için **Ayarlar**, **durum**, **ayar türü**veya **yol** sütunlarını seçin. Örneğin, **yol** sütununu seçin ve yoldaki ayarları görmek için bir sonraki oku kullanın `Microsoft Excel` .

- Şablonunuzda, belirli ayarları bulmak için **arama** kutusunu kullanın. Ayar veya yola göre arama yapabilirsiniz. Örneğin, **Tüm ayarlar**' ı seçin ve arama yapın `copy` . Tüm ayarlar `copy` gösterilir:

  > [!div class="mx-imgBorder"]
  > ![Intune 'da yönetim şablonlarındaki tüm cihaz ayarlarını göstermek için Kopyala araması yapın](./media/administrative-templates-windows/search-copy-settings.png) 

  Başka bir örnekte, için arama yapın `microsoft word` . Microsoft Word programı için ayarlayabileceğiniz ayarları görürsünüz. `explorer`Şablonunuza ekleyebileceğiniz Internet Explorer ayarlarını görmek için arama yapın.

- Ayrıca, aramanızı yalnızca **bilgisayar yapılandırması** veya **Kullanıcı Yapılandırması**seçerek daraltabilirsiniz.

  Örneğin, tüm kullanılabilir Internet Explorer Kullanıcı ayarlarını görmek için  **Kullanıcı Yapılandırması**' nı seçin ve arama yapın `Internet Explorer` . Yalnızca kullanıcılara uygulanan IE ayarları gösterilir:

  :::image type="content" source="./media/administrative-templates-windows/show-all-internet-explorer-settings-user-configuration.png" alt-text="ADMX şablonunda, Kullanıcı Yapılandırması ' nı seçin ve Microsoft Intune Internet Explorer için arama veya filtreleme yapın.":::

## <a name="next-steps"></a>Sonraki adımlar

Şablon oluşturuldu, ancak henüz bir şey yapmamış olabilir. Sonra, [şablonu (profil olarak da bilinir) atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

[Yönetim şablonlarını kullanarak Microsoft 365](administrative-templates-update-office.md)güncelleştirin.

[Öğretici: Windows 10 cihazlarında ADMX şablonları ve Microsoft Intune Grup İlkesi yapılandırmak için bulutu kullanın](tutorial-walkthrough-administrative-templates.md)