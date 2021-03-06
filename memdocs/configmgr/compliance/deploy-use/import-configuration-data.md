---
title: Yapılandırma verilerini içeri aktarma
titleSuffix: Configuration Manager
description: Yapılandırma verilerini bir dolap dosyası biçiminde içeriyorsa ve desteklenen hizmet modelleme dili şemasına uygunsa içeri aktarın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 7d9760a49815b9eb33c7886f4d9a8f9637dedd21
ms.sourcegitcommit: 9f072da27aa64f46a9409470b5dac5bfac3a0fe5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89468320"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Yapılandırma verilerini Configuration Manager içeri aktarma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolunda yapılandırma temelleri ve yapılandırma öğeleri oluşturmaya ek olarak, bir dolap (. cab) dosya biçiminde bulunuyorsa ve desteklenen hizmet modelleme dili (SML) şemasına bağlı olduğunda yapılandırma verilerini içeri aktarabilirsiniz. Yapılandırma verilerini şuradan içeri aktarabilirsiniz:  

- Microsoft’tan veya diğer yazılım satıcısı sitelerinden indirilen en iyi uygulama yapılandırma verileri (Yapılandırma Paketleri).  

- System Center 2012 Configuration Manager ve sonrasında aktarılmış yapılandırma verileri.  

- Dışarıdan yazılan ve SML şemasına uyan yapılandırma verileri.  

Bir yapılandırma temelini içeri aktardığınızda yapılandırma temelinde başvurulan bazı veya tüm yapılandırma öğeleri de kabin dosyasına dahil edilebilir. İçeri aktarma işlemi sırasında, yapılandırma taban çizgisinde başvurulan tüm yapılandırma öğelerinin dolap dosyasına dahil edildiğini veya Configuration Manager sitesinde zaten var olduğunu doğrular Configuration Manager. Configuration Manager, tarafından konumlandıramediği yapılandırma verilerine başvuran bir yapılandırma temeli içeri aktarmaya çalışırsanız içeri aktarma işlemi başarısız olur.  

İçeri aktarma işleminin başarısız olabileceği diğer senaryolara şunlar dahildir:  

-   Yapılandırma verileri, Configuration Manager veritabanında ya da dolap dosyasının kendisinde konumlandıramıyor yapılandırma verilerine başvurur.  

-   Yapılandırma verileri, aynı ad ve yapılandırma verileri sürümüne sahip Configuration Manager veritabanında zaten mevcut, ancak içerik sürümü farklıdır.  

-   Yapılandırma verileri aynı içerik sürümüne sahip Configuration Manager veritabanında zaten mevcuttur, ancak karma hesaplama onu farklı olarak tanımlar.  

-   Yapılandırma verilerinin aynı ada sahip daha yeni bir sürümü zaten var veya Configuration Manager veritabanında yakın zamanda silinmiş.  

-   Çok siteli Configuration Manager hiyerarşisinde yapılandırma verileri ilk olarak bir üst siteden içeri aktarılmıştı. Verileri bir alt siteden değil, aynı siteden güncelleştirmeniz gerekir.  

### <a name="import-configuration-data"></a>Yapılandırma verilerini içeri aktarma  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk**  >  **yapılandırma öğeleri** veya **yapılandırma temelleri** ' ne tıklayın.
2.  **Giriş** sekmesinde, **Oluştur** grubunda, **yapılandırma verilerini içeri aktar**' a tıklayın.  
3.  **Yapılandırma Verilerini İçeri Aktarma Sihirbazı** ’nın **Dosya Seçin**sayfasında **Ekle**’ye tıklayıp **Aç** iletişim kutusunda içeri aktarmak istediğiniz .cab dosyalarını seçin.  
4.  İçeri aktarılan yapılandırma verilerinin Configuration Manager konsolunda düzenlenebilir olmasını istiyorsanız **içeri aktarılan yapılandırma temelleri ve yapılandırma öğelerinin yeni bir kopyasını oluştur** onay kutusunu seçin.  
5.  **Özet** sayfasında, gerçekleştirilecek eylemleri gözden geçirin ve Sihirbazı doldurun.  

İçeri aktarılan yapılandırma verileri **varlıklar ve uyumluluk** çalışma alanının **Uyumluluk ayarları** düğümünde görüntülenir.  
