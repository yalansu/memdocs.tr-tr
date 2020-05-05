---
title: Updates Publisher 'ı yükler
titleSuffix: Configuration Manager
description: System Center Updates Publisher ortamınızda yüklemesi
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f83e7207207496d69342a2322909e972ada5676
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720376"
---
# <a name="install-updates-publisher"></a>Updates Publisher 'ı yükler

*Uygulama hedefi: System Center Updates Publisher*

Bu makalelerdeki bilgiler, Configuration Manager ortamınızla birlikte kullanmak üzere güncelleştirme yayımcısını indirmeniz, yüklemenize ve ayarlamanıza yardımcı olabilir.

## <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar
System Center Updates Publisher, yalnızca Configuration Manager kullanılabilir. Tek başına WSUS Hiyerarşileriyle kullanılmak üzere tasarlanmamıştır.

Aşağıdaki bölümlerde, Updates Publisher 'ı yüklemek ve kullanmak için gereken ayrıntılar ve kullanım için kısıtlamalar veya bilinen sorunlar verilmektedir.  

### <a name="operating-systems"></a>İşletim sistemleri
Aşağıdaki işletim sistemlerinin 64 bitlik sürümlerine Updates Publisher 'ı yükleyip çalıştırın. En düşük toplu güncelleştirme veya hizmet paketi gereksinimi yoktur.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, eğitim, Pro eğitim, kurumsal)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Önkoşullar
Updates Publisher çalıştıran bilgisayarda aşağıdakiler gereklidir.

-   **64-bit işletim sistemi**: Updates Publisher 'ı yüklediğiniz bilgisayar 64 bit işletim sistemi çalıştırmalıdır.
-   **WSUS 6,2 veya üzeri**:
    -   Windows Server 'da, bu gereksinimi karşılamak için varsayılan Yönetim konsolunu yükler.
    -   Windows 10 ve Windows 8.1 için, [Windows işletim sistemleri için uzak sunucu yönetim araçları (RSAT)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)yüklemesini yapın. Bu, Updates Publisher 'ı (*API ve PowerShell cmdlet 'leri*ve *Kullanıcı arabirimi yönetim konsolu*) kullanmak için gerekli desteği yüklüyor.
-   **İzinler**:
    -   Yükleme: yerel yönetici
    -   Çoğu işlem: Yerel Kullanıcı
    -   Yayımlama veya WSUS içeren işlemler: WSUS sunucusunda WSUS yöneticileri grubunun üyesi.

### <a name="supported-languages"></a>Desteklenen diller
Updates Publisher yalnızca Ingilizce dilinde kullanılabilir ancak diğer dillere yönelik güncelleştirmeleri yönetebilir. Dil desteği, güncelleştirmeleri yayımlama, oluşturma veya düzenlemeyle ilgili göreve bağlıdır.

Güncelleştirmeler dışarı aktarılırken veya yayımlandığında, Updates Publisher, yazılım güncelleştirmesinin başlığını ve açıklamasını, güncelleştirmelerin yayımcısının yüklendiği bilgisayarın yerel ayarlarına göre görüntüler.

Örneğin, Ingilizce ve Ispanyolca başlığına sahip bir yazılım güncelleştirmesi oluşturursunuz.

-   Güncelleştirmeyi yerel ayarı Ingilizce olan bir bilgisayarda oluşturursanız, varsayılan olarak başlığı ve açıklamayı Ingilizce olarak görürsünüz.
-   Daha sonra bu güncelleştirmeyi dışa aktarabilir veya yerel ayarı Ispanyolca olan bir bilgisayara yayımlarsanız, bu bilgisayarda başlık ve açıklama ' yı Ispanyolca olarak görürsünüz.

### <a name="publishing"></a>Yayımlama
Yazılım güncelleştirmelerini yayımladığınızda, yazılım güncelleştirme ikili dosyasının dilini belirtebilirsiniz. İkilinin dilden bağımsız olduğunu da belirtebilirsiniz. Aşağıdaki diller desteklenir:

-   Arapça
-   Çince (Hong Kong ÖİB)
-   seçenekleri yerine
-   Çince (Basitleştirilmiş)
-   Çekçe
-   Danca
-   Felemenkçe
-   İngilizce
-   Fince
-   Fransızca
-   Almanca
-   Yunanca
-   İbranice
-   Macarca
-   İtalyanca
-   Japonca
-   Korece
-   Norveççe
-   Lehçe
-   Portekizce
-   Portekizce (Brezilya)
-   Rusça
-   İspanyolca
-   İsveççe
-   Türkçe

### <a name="software-update-titles-and-descriptions"></a>Yazılım güncelleştirme başlıkları ve açıklamaları
Yazılım güncelleştirme başlıkları ve açıklamaları için aşağıdaki diller desteklenir.

-   seçenekleri yerine
-   Çince (Basitleştirilmiş)
-   İngilizce
-   Fransızca
-   Almanca
-   İtalyanca
-   Japonca
-   Korece
-   Portekizce (Brezilya)
-   Rusça
-   İspanyolca

## <a name="install-updates-publisher"></a>Updates Publisher 'ı yükler
[Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=55543)'nden System Center Updates Publisher yüklemek Için **Updatespubliser. msi** dosyasını alın.

Updates Publisher 'ı yüklemek için, *önkoşulları*karşılayan bir bilgisayarda **Updatespublisher. msi** ' yi çalıştırın. Yükleyici, Updates Publisher 'ı çalıştırmak için gereken dosyaları içeren aşağıdaki klasörü oluşturur:%PROGRAMFILES%\Microsoft\UpdatesPublisher *.

Bu klasör Updates Publisher 'ı kullanmak için gereken tüm dosyaları içerdiğinden, klasörü ve içeriğini yeni bir konuma veya bilgisayara kopyalayabilir ve ardından bu konumdan Updates Publisher 'ı kullanabilirsiniz. Ancak, yeni konum veya bilgisayar Updates Publisher 'ı çalıştırmak için önkoşulları karşılamalıdır.

Yükleme tamamlandıktan sonra, Updates Publisher 'ı başlatmak için *updatespublisher* klasöründen **updatespublisher. exe** ' yi çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
 Updates Publisher 'ı yükledikten sonra, Updates Publisher [seçeneklerini yapılandırmanızı](updates-publisher-options.md) öneririz. Updates Publisher 'ın bazı özelliklerini kullanabilmeniz için bazı seçenekleri yapılandırmanız gerekir.

 Ancak, varsayılan değerleri kullanmak ve güncelleştirme sunucusuna veya yönetilen cihazlara güncelleştirme dağıtmayı planlamıyorsanız, [yazılım güncelleştirme kataloglarının yönetilmesi](updates-publisher-catalogs.md)veya [yazılım güncelleştirmeleri oluşturma](create-updates-with-updates-publisher.md) ve kendinizinkini güncelleştirme katalogları oluşturma hakkını atlayabilirsiniz.
