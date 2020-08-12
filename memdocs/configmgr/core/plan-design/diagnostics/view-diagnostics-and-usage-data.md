---
title: Tanılama verilerini görüntüle
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşinizin gizli bilgiler içerdiğini onaylamak için tanılama ve kullanım verilerini görüntüleyin.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a11b5779eca41ed25a8e53e555f91b596452e51b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128578"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Configuration Manager için tanılama ve kullanım verilerini görüntüleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager hiyerarşinizdeki tanılama ve kullanım verilerini, hassas veya tanımlanabilir bilgiler içerdiğini doğrulamak için görüntüleyebilirsiniz. Site, tanılama verilerini, site veritabanının **TEL_TelemetryResults** tablosuna özetler ve depolar. Programlı olarak kullanılabilir ve etkili olacak verileri biçimlendirir.

Bu makaledeki bilgiler, Microsoft 'a gönderilen tam verilerin bir görünümünü sunar. Veri analizi gibi diğer amaçlar için kullanılmak üzere tasarlanmamıştır.  

## <a name="view-data-in-database"></a>Veritabanındaki verileri görüntüleme

Bu tablonun içeriğini görüntülemek ve gönderilen tam verileri göstermek için aşağıdaki SQL komutunu kullanın:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Verileri dışarı aktarma

Hizmet bağlantı noktası çevrimdışı modda olduğunda, geçerli verileri bir virgülle ayrılmış değerler (CSV) dosyasına aktarmak için hizmet bağlantı aracını kullanın. Hizmet bağlantı aracını hizmet bağlantı noktasında **-Export** parametresiyle çalıştırın.

Daha fazla bilgi için bkz. [hizmet bağlantı aracını kullanma](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a>Tek yönlü karma

Bazı veriler rastgele alfasayısal karakter dizelerinden oluşur. Configuration Manager, tek yönlü karmaları oluşturmak için SHA-256 algoritmasını kullanır. Bu işlem, Microsoft 'un potansiyel olarak gizli olmayan verileri toplamıyor olmasını sağlar. Karma veriler hala bağıntı ve karşılaştırma amaçları için kullanılabilir.

Örneğin, site veritabanındaki tabloların adlarını toplamak yerine, her tablo adı için tek yönlü karmayı yakalar. Bu davranış, herhangi bir özel tablo adının görünür olmadığından emin olur. Microsoft daha sonra varsayılan SQL tablo adlarının tek yönlü karma işlemini yapar. İki sorgunun sonuçlarını karşılaştırmak, veritabanı şemanızın ürün varsayılanından sapmasını belirler. Bu bilgiler daha sonra SQL şemasında değişiklik yapılmasını gerektiren güncelleştirmeleri geliştirmek için kullanılır.  

Ham verileri görüntülerken, her veri satırında ortak bir karma değer görüntülenir. Bu karma, hiyerarşi KIMLIĞIDIR. Müşteri veya kaynak tanımlanmaksızın aynı hiyerarşiyle verileri ilişkilendirmek için kullanılır.

### <a name="how-the-one-way-hash-works"></a>Tek yönlü karma nasıl çalışacaktır?

1. Configuration Manager veritabanında SQL Management Studio 'de aşağıdaki SQL sorgusunu çalıştırarak hiyerarşi KIMLIĞINIZI alın:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Hiyerarşi KIMLIĞINIZIN tek yönlü karmasını yapmak için aşağıdaki Windows PowerShell betiğini kullanın.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Betik çıkışını ham verilerdeki GUID ile karşılaştırın. Bu işlem verilerin nasıl gizlençalıştığını gösterir.

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Tanılama kullanım verileri düzeyleri](levels-overview.md)
