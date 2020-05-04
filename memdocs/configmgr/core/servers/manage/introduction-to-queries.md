---
title: Sorgulara giriş
titleSuffix: Configuration Manager
description: Sorgu ölçütlerinizle eşleşen bir Configuration Manager hiyerarşisinde nesneleri bulmak için sorgular oluşturun ve çalıştırın.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713824"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Configuration Manager sorgulara giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sorgu ölçütlerinizle eşleşen bir Configuration Manager hiyerarşisinde nesneleri bulmak için sorgular oluşturabilir ve çalıştırabilirsiniz. Bu nesneler, belirli bilgisayar türleri veya Kullanıcı grupları gibi öğeler içerir. Sorgular, siteler, koleksiyonlar, uygulamalar ve envanter verileri dahil olmak üzere çoğu Configuration Manager nesne türünü döndürebilir.  

## <a name="query-creation-overview"></a>Sorgu oluşturmaya genel bakış

 Sorgu oluşturduğunuzda en az iki parametre belirtmeniz gerekir: Arama yapmak istediğiniz konum ve aramak istediğiniz şey. Örneğin, bir Configuration Manager sitesindeki tüm bilgisayarlarda kullanılabilir sabit disk alanı miktarını bulmak için, **mantıksal disk** öznitelik sınıfını ve **boş alan (MB)** özniteliğini aramak üzere bir sorgu oluşturabilirsiniz.  

 İlk sorguyu oluşturduktan sonra ek sorgu ölçütleri belirtebilirsiniz. Örneğin, sorgu sonuçlarına yalnızca belirli bir siteye atanmış bilgisayarların dahil edileceğini belirtebilirsiniz. Sonuçları sizin için anlamlı bir sırada görüntüleyebilmeniz için sonuçların görüntülenme şeklini de değiştirebilirsiniz. Örneğin, sonuçların boş sabit disk alanı miktarına göre artan veya azalan sırada sıralanacağını belirtebilirsiniz.  

 Bir sorgu oluşturduğunuzda, Configuration Manager tarafından depolanır ve **izleme** çalışma alanındaki **sorgular** düğümünde gösterilir. Bu konumdan yeni sorgular oluşturabilir ve mevcut sorguları çalıştırabilir, güncelleştirebilir ve yönetebilirsiniz.  

 Ayrıca, bir Configuration Manager koleksiyonundaki sorgu kuralına bir sorgu içeri aktarabilirsiniz. Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Sonraki adımlar

 [Sorgu oluşturma](../../../core/servers/manage/create-queries.md)
