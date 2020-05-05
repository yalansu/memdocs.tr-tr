---
title: Destek Merkezi hızlı başlangıç
titleSuffix: Configuration Manager
description: Sorun giderme için Configuration Manager istemcisinin durumunu hızlıca yakalayın.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723120"
---
# <a name="support-center-quickstart-guide"></a>Destek Merkezi Hızlı Başlangıç Kılavuzu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Destek Merkezi, sorun giderme ve gerçek zamanlı günlük görüntüleme gibi güçlü yeteneklere sahiptir. Ayrıca, bir Configuration Manager istemci bilgisayarının durumunu yakalamak için yalnızca birkaç dakika içinde de kullanılabilir. Bu özellik uzak istemcilere erişimi de içerir.

İstemci durumunu yakalayan, tamamen *sorun giderme paketi* dosyası (. zip) oluşturun. Paket yalnızca günlük dosyaları içermiyor. Kayıt defteri ayarları ve istemci yapılandırması gibi diğer veri türlerini içerebilir. Paketi, Destek Merkezi Görüntüleyicisi 'Ni kullanan bir destek teknisyenine sağlar.



## <a name="prerequisites"></a>Önkoşullar

- Configuration Manager istemcisinde yerel yönetici hakları  

- Destek Merkezi Yükleyicisi. Bu dosya, adresindeki `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`site sunucusudur. Daha fazla bilgi için bkz. [Destek Merkezi-yüklemesi](support-center.md#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>1. Adım: yerel bir istemcide veri paketi oluşturma

1.  Configuration Manager istemcisine Destek Merkezi 'ni yükler.  

2.  **Başlat** menüsüne gidin, **Microsoft System Center** grubunda **Destek Merkezi**' ni seçin.  

3.  Şeridin Giriş sekmesinde, **seçili verileri topla**' yı seçin. Varsayılan olarak, destek merkezi yalnızca en düşük veri kümesini toplar: günlük dosyaları, istemci yapılandırması ve işletim sistemi.  

4.  Sorun giderme paketi dosyasını (. zip) bilgisayardaki bir klasöre kaydedin. Varsayılan olarak, dosya adı aşağıdaki örneğe benzer: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>2. Adım: Destek Merkezi Görüntüleyicisi 'Ni kullanarak veri paketini görüntüleme

1.  **Destek Merkezi Görüntüleyicisi 'ni**başlatın. Bu eylem, destek merkezini yüklediğiniz herhangi bir bilgisayarda gerçekleşebilir.  

2.  **Paket aç**' ı seçin, paket dosyasına gidin ve **Aç**' ı seçin.  

3.  Destek Merkezi Görüntüleyicisi dosyayı işlediğinde, kullanılabilir her bir sekmeye geçin. Destek Merkezi 'nin varsayılan olarak topladığı veri türlerini görüntüleyin:  

    - **Yapılandırma**  

        - Configuration Manager istemci yapılandırması  

        - İşletim sistemi  

        - Bilgisayar  

        - Hizmetler  

        - Ağ bağdaştırıcıları  

    - **Günlükler**: listede bir veya daha fazla girdi seçin ve **Aç**' ı seçin. Bu eylem, günlük görüntüleyicisinde seçili günlük dosyalarını açar. Hata kodlarını aramak için bu özelliği kullanın ve günlük dosyalarını daha hızlı çözümlemenize yardımcı olması için gelişmiş filtreler kullanın.  



## <a name="collect-more-data"></a>Daha fazla veri toplayın

Bu temel yeteneklerin ötesinde, Destek Merkezi diğer birçok istemci durum bilgilerini de toplayabilir. **Destek merkezini** açın ve **tüm verileri topla**' yı seçin. Bu işlem, genellikle daha yeni bilgisayarlarda bile birkaç dakika sürer. Destek Merkezi aşağıdaki ek verileri toplar:

- **İlke**: istenen ilke yapılandırması ve gerçek ilke yapılandırması da dahil olmak üzere ilke ayarlarını Configuration Manager  

- **Sertifikalar**: istemci sertifikaları için ortak anahtar bilgileri. Destek Merkezi, sertifika özel anahtarlarını toplamaz.  

- **İstemci kayıt defteri**: kayıt defterinden istemci yapılandırma bilgilerini toplar. Destek Merkezi yalnızca Configuration Manager kayıt defteri bilgilerini toplar.  

- **ISTEMCI WMI**: WMI 'dan istemci yapılandırma bilgileri. Destek Merkezi istemci ilkesi toplanmaz.  

- **Sorun giderme**: Active Directory, yönetim noktaları, ağ, ilke atamaları ve kayıt ile yaygın istemci sorunlarını tanılamaya yardımcı olmak için gerçek zamanlı sorun giderme verileri.  

- **Hata ayıklama dökümleri**: istemcinin ve ilgili işlemlerin hata ayıklama dökümünü yapın. Hata ayıklama dökümleri büyük olabilir. Bu seçeneği yalnızca istemci performansıyla ilgili sorunları giderirken etkinleştirin.  

