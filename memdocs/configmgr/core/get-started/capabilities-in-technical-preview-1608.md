---
title: Technical Preview 1608 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1608 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074189"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Configuration Manager için Technical Preview 1608 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1608 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Yakalama görev dizisi adımı için ConfigMgr İstemcisini Yakalamaya Hazırla’da yapılan geliştirmeler  
ConfigMgr Istemcisini hazırla adımı yalnızca anahtar bilgilerini kaldırmak yerine Configuration Manager istemcisini tamamen kaldırır. Görev dizisi yakalanan işletim sistemi görüntüsünü dağıttığında, her seferinde yeni bir Configuration Manager istemci yükler.  


## <a name="improvements-to-software-center"></a>Yazılım Merkezi geliştirmeleri
* Software Center **uygulamaları**, **güncelleştirmeleri**ve **işletim sistemleri** sekmeleri artık son zamanlarda hangi yazılımların eklendiğini gösterir. Gezinti bölmesindeki sayılar her bir sekmede kaç tane yeni yazılım parçası olduğunu gösterir.
* Kullanıcılar artık uygulamalar için onay isteyebilir ve ardından, yazılım merkezi 'nde **uygulama ayrıntıları** görünümünde istek geçmişini görüntüleyebilir. **Uygulama ayrıntılarında** **istek** düğmesi artık Web tabanlı uygulama kataloğu yeniden yönlendirmediğini.

## <a name="improvements-to-asset-intelligence"></a>Varlık Yönetim Bilgileri geliştirmeleri
Envantere kaydedilmiş yazılımların özelliklerine, diğer yazılımlarla bir üst ve alt ilişki ayarlamanıza olanak tanıyan bir alan ekledik. Envantere kaydedilen yazılım listesinde, herhangi bir yazılımın üst öğesini görüntüleyebilir ve ayrıca tüm alt yazılımları gizleyebilirsiniz.

### <a name="configure-a-parent-to-child-relationship"></a>Üst öğeye alt öğe ilişkisini yapılandırma
  1. Üst yazılımı ayarlamak için envantere kaydedilmiş yazılım düğümünde, **envantere kaydedilmiş yazılım** listesindeki bir yazılım öğesine sağ tıklayın ve **Özellikler**' i seçin.
  2. Açılan iletişim kutusunda, ilk seçiminiz için üst yazılım olarak ayarlamak istediğiniz yazılımı seçin.

### <a name="filter-the-software-display"></a>Yazılım görüntüsünü filtrele
Üst-alt ilişkileri tanımladıktan sonra, görünümünüzü yalnızca üst öğe olan veya tanımlı ilişki olmayan yazılımları gösterecek şekilde filtreleyebilirsiniz. Bu, başka bir envantere kaydedilmiş yazılımın alt öğesi olarak ayarlanan tüm yazılımları gizler. Bunu yapmak için:
   1. Arama çubuğu için **ölçüt eklemeyi** seçin
   2. **Üst yazılımı** seçin ve ardından ölçüt değerini **boş**olarak değiştirin ve ardından **Ara**' ya tıklayın.

Ekranda artık yalnızca üst yazılım öğeleri veya tanımlı ilişki olmayan yazılımlar gösterilir. Yalnızca başka bir başlığın alt öğesi olan yazılım görüntülenmez.

## <a name="remote-control-keyboard-translation"></a>Uzaktan denetim klavye çevirisi
Geçmişte Configuration Manager, ana konumu görüntüleyicisinin konumundan paylaşan konuma aktardı. Bu, görüntüleyiciye farklı olan klavye yapılandırmalarının Paylaşanı ile ilgili sorunlardır. Örneğin, Ingilizce Klavye içeren bir görüntüleyici bir "A" yazabilir, ancak paylaşan Fransızca klavyesi bir "Q" sağlar. Varsayılan davranışı, karakterin kendisi de görüntüleyicinin, paylaşan ' dan paylaşan ' a iletilmesi ve bu sayede görüntüleyicinin, paylaşan türe ulaşması için ne kadar amaçladığı için değiştiriyorsunuz.

Bu davranış, paylaşan klavye düzenine göre yazmak tercih ediyorsanız Görüntüleyici tarafından kapatılabilir. Davranışı değiştirmek için, **Uzaktan denetim Configuration Manager**, **eylem**' i seçin ve anahtar konumunu Iletmek için **klavye çevirisini etkinleştir** ' i seçin.

> [!NOTE]
>
> ~! # @ $% Gibi özel anahtarlar doğru çevrilemeyecek.
