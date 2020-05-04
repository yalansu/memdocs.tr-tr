---
title: Koleksiyonlar güvenlik ve Gizlilik
titleSuffix: Configuration Manager
description: Configuration Manager içindeki koleksiyonlardaki güvenlik ve gizlilik için en iyi uygulamaları alın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714496"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Configuration Manager koleksiyonlar için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager içindeki koleksiyonlar için en iyi güvenlik uygulamalarını ve gizlilik bilgilerini içerir.  

 Configuration Manager içindeki koleksiyonlar için özel olarak gizlilik bilgisi yoktur. Koleksiyonlar kullanıcı ve cihazlar gibi kaynaklar için kapsayıcı görevi görür. Koleksiyon üyeliği genellikle standart işlem sırasında Configuration Manager topladığı bilgilere bağlıdır. Örneğin, bulma veya envanter tarafından toplanan kaynak bilgilerini kullanarak belirtilen ölçütleri karşılayan cihazları içeren bir koleksiyon yapılandırılabilirsiniz. Koleksiyonlar ayrıca, yazılım dağıtımı ve uyumluluk denetimi gibi istemci yönetim işlemleriyle ilgili geçerli durum bilgilerinden de uyarlanabilir. Bu sorgu tabanlı koleksiyonlara ek olarak yönetici kullanıcılar da koleksiyonlara kaynak ekleyebilir.  

 Koleksiyonlar hakkında daha fazla bilgi için bkz. [koleksiyonlara giriş](../../../../core/clients/manage/collections/introduction-to-collections.md). Koleksiyon üyeliğini yapılandırmak için kullanılabilecek Configuration Manager işlemler için en iyi güvenlik uygulamaları ve gizlilik bilgileri hakkında daha fazla bilgi için bkz. [Configuration Manager için En Iyi güvenlik uygulamaları ve gizlilik bilgileri](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Koleksiyonlar için En İyi Yöntemler  
 Koleksiyonlar için aşağıdaki en iyi güvenlik yöntemlerini kullanın.  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Ağ konumuna kaydedilmiş bir koleksiyonu Yönetilen Nesne Biçimi (MOF) dosyası kullanarak içeri veya dışarı aktarırken konumun ve ağ kanalının güvenliğini sağlayın.|Ağ klasörüne erişebilecek kişileri kısıtlayın.<br /><br /> Bir saldırganın dışarı aktarılan koleksiyon verilerinize müdahale etmesini önlemek için ağ konumu ve site sunucusu arasında Sunucu İleti Bloğu (SMB) imzası veya İnternet Protokolü Güvenliği (IPsec) kullanın. Bilgilerin açığa çıkmasını önlemek amacıyla ağdaki verileri şifrelemek için IPsec kullanın.|  

### <a name="security-issues-for-collections"></a>Koleksiyonlar için Güvenlik Sorunları  
 Koleksiyonlar aşağıdaki güvenlik sorunları bulunur:  

-   Koleksiyon değişkenleri kullanıyorsanız yerel yöneticiler olası duyarlı bilgileri okuyabilir.  

     İşletim sistemi dağıtırken koleksiyon değişkenleri kullanabilirsiniz.  
