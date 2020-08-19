---
title: Power BI örnek raporlarını yükleme
titleSuffix: Configuration Manager
description: Power BI örnek raporlarının Configuration Manager nasıl yükleneceğini öğrenin
ms.date: 08/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb55fc79c44af83c7bb7a5e0802800f55e28e6b3
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614767"
---
# <a name="install-power-bi-sample-reports"></a>Power BI örnek raporlarını yükleme
<!--5679791-->
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sürüm 2002 ' den başlayarak, [Power BI Rapor Sunucusu](https://docs.microsoft.com/power-bi/report-server/get-started) Configuration Manager raporlama ile tümleştirebilirsiniz. Configuration Manager ' de yükleyebileceğiniz, indirilebilir bir örnek rapor mevcuttur. Bu makalede, Power BI örnek raporlarının Configuration Manager nasıl yükleneceği açıklanır.

## <a name="prerequisites"></a>Ön koşullar

- [Power BI rapor sunucusu tümleşik](powerbi-report-server.md) olan Configuration Manager Reporting Services noktası

- [Microsoft Power BI Desktop (Power BI rapor sunucusu Için En Iyi duruma getirilmiş-eylül 2019)](https://www.microsoft.com/download/details.aspx?id=57271)veya üzeri

- [2002 sürümü için güncelleştirme paketi (4560496)](https://support.microsoft.com/help/4560496) önerilir, ancak gerekli değildir.

    > [!IMPORTANT]
    > Yalnızca [Microsoft Indirme merkezi](https://www.microsoft.com/download/)'ndeki Power BI Desktop sürümlerini kullanın. Microsoft Store sürüm kullanmayın.
    >
    > Yalnızca [Power BI rapor sunucusu Için En Iyi duruma getirilmiş](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop)Power BI Desktop bir sürümünü kullanın.

## <a name="download-the-sample-reports"></a>Örnek raporları indirin

Örnek raporları indirmek için:

1. Power BI örnek raporlarını [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=101452)' nden indirin.

1. `ConfigMgrSamplePowerBIReports.exe` dosyasını kaydedin.

1. Dosyayı farklı bir cihazdan indirdiyseniz Microsoft Power BI Desktop (Power BI Rapor Sunucusu için Iyileştirilmiş) yüklü bir bilgisayara taşıyın.

1. `ConfigMgrSamplePowerBIReports.exe`. Pbit dosyalarını ayıklamak için dosyayı çalıştırın.

## <a name="install-the-sample-reports"></a>Örnek raporları yükler

Örnek raporları yüklemek için:

1. Power BI rapor sunucusunda, `Sample Reports` kök Configuration Manager raporlama klasöründe adlı yeni bir klasör oluşturun.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Kök Configuration Manager raporlama klasöründe örnek rapor klasörü oluşturuluyor " lightbox="media/create-sample-reports-folder.png":::

1. Microsoft Power BI Desktop başlatın (Power BI Rapor Sunucusu için Iyileştirilmiş).

1. **Dosya** ' yı seçip **açın** ve ayıklanan. pbit dosyalarını kaydettiğiniz yere gidin.

1. Dosyadan ayıkladığınız. pbit dosyalarından birini seçin `ConfigMgrSamplePowerBIReports.exe` .

1. İstendiğinde Configuration Manager veritabanı adınızı ve veritabanı sunucusu adınızı belirtin, sonra **Yükle**' yi seçin.

    :::image type="content" source="media/sample-report-database.png" alt-text="Veritabanı ve veritabanı sunucu adını belirtin" lightbox="media/sample-report-database.png":::

    > [!NOTE]
    > Veri modeli yüklenirken veya uygulanırken, bir tane boyunca geliyorsa tüm hataları yoksayın. Örneğin, şu hatayı görürseniz: "birden fazla veritabanından tablolara bağlanma, DirectQuery modunda desteklenmez", **Kapat**' ı seçin. Ardından veri kaynağı ayarlarını yenileyin:
    >
    > 1. Power BI Desktop, şeritte **sorguları Düzenle**' yi seçin ve ardından **veri kaynağı ayarları**' nı seçin.
    > 1. **Kaynağı değiştir**' i seçin, sunucunuzu ve veritabanı adlarınızı onaylayın ve **Tamam**' ı seçin.
    > 1. Veri kaynağı ayarları penceresini kapatın ve sonra **Değişiklikleri Uygula**' yı seçin.

1. Rapor verileri yüklendiğinde **Dosya**  >  **farklı kaydet**' i seçin ve ardından **Power BI rapor sunucusu**' yi seçin.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Power BI Rapor Sunucusu olarak kaydet" lightbox="media/save-powerbi-report-server.png":::

1. Raporu, `Sample Reports` Raporlama noktasında oluşturduğunuz klasöre kaydedin.

    :::image type="content" source="media/save-sample-report.png" alt-text="Örnek Raporlar klasörüne kaydet" lightbox="media/save-sample-report.png":::

1. Diğer örnek raporlar için adımları yineleyin. İşiniz bittiğinde Microsoft Power BI Desktop (Power BI Rapor Sunucusu için Iyileştirilmiş) ' ı kapatın.

1. Configuration Manager konsolunda **izleme**  >  **Power BI raporlar**  >  **örnek raporlar**' a gidin.

1. Raporu başlatmak için raporlardan birine sağ tıklayıp **tarayıcıda Çalıştır** ' ı seçin.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Örnek raporu Configuration Manager konsolundan çalıştırın" lightbox="media/view-powerbi-report.png":::
