---
title: OData akışından Power BI ile bir Intune raporu oluşturma
titleSuffix: Microsoft Intune
description: Power BI Desktop kullanarak Intune Veri Ambarı API’sinden etkileşimli bir filtre ile ağaç harita görselleştirmesi oluşturun.
keywords: Intune Veri Ambarı
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/29/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: A2C8A336-29D3-47DF-BB4A-62748339391D
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 081d293432e15fccfd2b30d2eb7b7c300789e74f
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270982"
---
# <a name="create-an-intune-report-from-the-odata-feed-with-power-bi"></a>OData akışından Power BI ile bir Intune raporu oluşturma

Bu makalede, kullanıcıların etkileşimli bir filtre Power BI Desktop kullanarak Intune verilerinizin ağaç Haritası görselleştirmesinin nasıl oluşturulacağı açıklanmaktadır. Örneğin, CFO, cihazların genel dağıtımının şirkete ait cihazlar ve kişisel cihazlar arasında nasıl Karşılaştırıldığı hakkında bilgi alabilir. Bu ağaç harita, toplam cihaz türü sayısı hakkında bilgi sağlar. Şirkete ait veya kişisel olarak sahip olunan iOS/ıpados, Android ve Windows cihazlarının sayısını gözden geçirebilirsiniz.

## <a name="overview-of-creating-the-chart"></a>Grafiği oluşturmaya genel bakış

Bu grafiği oluşturmak için şunları yapmanız gerekir:
1. Hala yüklemediyseniz Power BI Desktop yükleyin.
2. Intune Veri Ambarı ver modeline bağlanın ve model için geçerli verileri alın.
3. Veri modeli ilişkileri oluşturun veya yönetin.
4. **Cihazlar** tablosundaki verilerle grafiği oluşturun.
5. Etkileşimli bir filtre oluşturun.
6. Tamamlanan grafiği görüntüleyin.

### <a name="a-note-about-tables-and-entities"></a>Tablolar ve varlıklar hakkında bir not

Power BI’da tablolar ile çalışırsınız. Tabloların veri alanları bulunur. Her bir veri alanına ait bir veri türü vardır. Alanlar yalnızca uygun veri türüne ait verileri barındırabilir. Veri türleri numara, metin, tarih vb. şeklindedir. Power BI’daki tablolar, modeli yüklediğinizde kiracınızda bulunan geçmiş verilerle dolar. Bazı veriler zamanla değişse de, veri modeli güncelleştirilmediği sürece tablo yapısı değişmez.

*Varlık* ve *tablo* terimlerinin kullanımı aklınızı karıştırabilir. Veri modeline bir OData (açık veri Protokolü) akışı aracılığıyla erişilebilir. OData evreninde tablo olarak bilinen öğelere Power BI’da varlık adı verilir. Her iki terim de aslında aynı olup verilerinizi taşıyan şeye verilen addır. OData hakkında daha fazla bilgi için bkz. [OData 'e genel bakış](/odata/overview).

## <a name="install-power-bi-desktop"></a>Power BI Desktop uygulamasını yükleme

En yeni Power BI Desktop sürümünü yükleyin. Power BI Desktop’ı şu adresten indirebilirsiniz: [PowerBI.microsoft.com](https://powerbi.microsoft.com/desktop)

## <a name="connect-to-the-odata-feed-for-the-intune-data-warehouse-for-your-tenant"></a>Kiracınız için Intune Veri Ambarı OData akışına bağlanma

> [!Note]  
> Intune’da **Raporlar** izniniz olmalıdır. Daha fazla bilgi için bkz. [Yetkilendirme](reports-api-url.md#authorization).

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Raporlar**  >  **Intune veri ambarı**  >  **veri ambarı**' nı seçin.
3. Özel akış URL’sini kopyalayın. Örneğin, `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0`
4. Power BI Desktop'ı açın.
5. MenüÇubuğu ' ndan **Dosya**  >  **veri al**  >  **OData akışı**' nı seçin.
6. Önceki adımdan kopyaladığınız özel akış URL 'sini **OData akış** penceresindeki URL kutusuna yapıştırın.
7. **Temel**'i seçin.

    ![Kiracınız için Intune veri ambarı için OData akışı](./media/reports-proc-create-with-odata/reports-create-01-odatafeed.png)

8. **Tamam**’ı seçin.
9. **Kuruluş hesabı**’nı seçin ve Intune kimlik bilgilerinizle oturum açın.

    ![Kuruluş hesabı kimlik bilgileri](./media/reports-proc-create-with-odata/reports-create-02-org-account.png)

10. **Bağlan**'ı seçin. Gezgin açılacak ve size Intune Veri Ambarı’ndaki tabloların listesini gösterecektir.

    ![Gezgin 'in ekran görüntüsü-veri ambarı tablolarının listesi](./media/reports-proc-create-with-odata/reports-create-02-loadentities.png)

11. **cihazlar** ve **ownerTypes** tablolarını seçin.  **Yükle**’yi seçin. Power BI modele veri yükler.

## <a name="create-a-relationship"></a>Bir ilişki oluşturma

Çözümlemek için birden fazla tabloyu içeri aktarabilirsiniz, yani yalnızca bir tablodaki verileri değil, farklı tablolardaki ilişkili verileri alabilirsiniz. Power BI, sizin için ilişkileri bulmayı ve oluşturmayı deneyen **Otomatik Algıla** adlı bir özelliğe sahiptir. Veri ambarındaki tablolar, Power BI Otomatik Algıla özelliği ile çalışacak şekilde oluşturulmuştur. Ancak Power BI ilişkileri otomatik olarak bulamazsa, ilişkileri yine de yönetmeye devam edebilirsiniz.

![Tablolar arasında ilgili verilerin ilişkilerini yönetme](./media/reports-proc-create-with-odata/reports-create-03-managerelationships.png)

1. **İlişkileri Yönet**’i seçin.
2. Power BI zaten ilişki algılamıyorsa **otomatik algıla...** seçeneğini belirleyin.

İlişki, Kaynak ve Hedef sütunlarında görüntülenir. Bu örnekte **cihazlar** tablosundaki **ownerTypeKey** veri alanı, **ownerTypes** tablosundaki **ownerTypeKey** veri alanına bağlantı sağlar. **Cihazlar** tablosundaki cihaz türü kodunun düz adını aramak için ilişkiyi kullanırsınız.

## <a name="create-a-treemap-visualization"></a>Ağaç haritası görselleştirmesi oluşturma

Ağaç Haritası grafiği, hiyerarşik verileri kutular içindeki kutular olarak gösterir. Hiyerarşinin her bir dalında kutular bulunur. Bu kutular ise alt dalları gösteren daha küçük kutular barındırır. Intune kiracı verilerinizin bir ağaç haritasını oluşturmak için Power BI Masaüstü 'nü kullanarak, cihaz üreticisi türlerinin göreli miktarları gösterilmektedir.

![Power BI ağaç Haritası görselleştirmeleri](./media/reports-proc-create-with-odata/reports-create-03-treemap.png)

1. **Görsel öğeler** bölmesinde, **ağaç Haritası**' nı bulup seçin. **Treemap** grafiği rapor tuvaline eklenecektir.
2. **Alanlar** bölmesinde, `devices` tabloyu bulun.
3. Tabloyu genişletin `devices` ve `manufacturer` veri alanını seçin.
4. `manufacturer`Veri alanını rapor tuvaline sürükleyin ve **treemap** grafiğine bırakın.
5. `deviceKey`Tablodaki veri alanını, `devices` **görsel öğeler** bölmesine sürükleyin ve **veri alanı Ekle**etiketli kutudaki **değerler** bölümünün altına bırakın.  

Artık kuruluşunuzdaki cihaz üreticileri dağılımını gösteren bir görseliniz var.

![Verilerle ağaç Haritası-cihazların üreticilerinin dağılımı](./media/reports-proc-create-with-odata/reports-create-06-treemapwdata.png)

## <a name="add-a-filter"></a>Filtre ekleme

Uygulamanızı kullanarak ilave sorular yanıtlayabilmek için ağaç haritanıza bir filtre ekleyebilirsiniz.

1. Filtre eklemek için, rapor tuvali ' ni seçin ve ardından görsel öğeler altında **dilimleyici simgesini** ( ![ veri modeli ve desteklenen ilişkilerle ağaç Haritası ](./media/reports-proc-create-with-odata/reports-create-slicer.png) ) seçin **Visualizations**. Boş **dilimleyici** görselleştirmesi tuvalde görünür.
2. **Alanlar** bölmesinde, `ownerTypes` tabloyu bulun.
3. Tabloyu genişletin `ownerTypes` ve `ownerTypeName` veri alanını seçin.
4. `onwerTypeName`Tablodaki veri alanını `ownerTypes` **Filtreler** bölmesine sürükleyin ve **Bu sayfadaki filtreler** altında **veri alanları Ekle**etiketli kutuda bu sayfaya bırakın.  

   `OwnerTypes`Tabloda, bir `OwnerTypeKey` cihazın şirkete ait veya kişisel olup olmadığı gibi bir veri içeren adlı bir veri alanı bulunur. Bu filtrede kolay adlar göstermek istiyorsanız, `ownerTypes` tabloya bakın ve **ownerTypeName** öğesini dilimleyiciye sürükleyin. Bu örnek, veri modelinin tablolar arasındaki ilişkiyi nasıl desteklediğini gösterir.

![Filter ile treemap-tablolar arasındaki ilişkileri destekler](./media/reports-proc-create-with-odata/reports-create-08_ownertype.png)

Artık şirkete ait ve kişisel cihazlar arasında geçiş yapmak üzere kullanılacak bir filtreniz var. Dağılımın nasıl değiştiğini görmek için bu filtreyi kullanın.

1. Şirkete ait cihaz dağıtımına sahip olduğunu görmek için Dilimleyicinin içindeki **Şirket** ' ı seçin.
2. Kişisel cihazları görmek için Dilimleyicinin içinden **Kişisel** ' i seçin.

## <a name="next-steps"></a>Sonraki adımlar

- Power BI Desktop’ta [ilişki oluşturma ve yönetme](https://powerbi.microsoft.com/documentation/powerbi-desktop-create-and-manage-relationships/) hakkında Power BI belgelerinden daha fazla bilgi edinin.
- [Intune Veri Ambarı](reports-ref-data-model.md)’na başvurun.
