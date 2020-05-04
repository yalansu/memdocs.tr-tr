---
title: Güç yönetimini yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager 'de güç yönetimini ayarlayın.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715245"
---
# <a name="configure-power-management-in-configuration-manager"></a>Configuration Manager 'de güç yönetimini yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager ' de güç yönetiminin nasıl ayarlanacağı açıklanır.

## <a name="enable-and-configure-client-settings"></a>İstemci ayarlarını etkinleştirme ve yapılandırma

Bu yordam, güç yönetimi için *varsayılan istemci ayarlarını* yapılandırır. Hiyerarşinizdeki tüm bilgisayarlar için geçerlidir.

Bu ayarların yalnızca bazı bilgisayarlara uygulanmasını istiyorsanız *özel bir cihaz istemci ayarı*oluşturun. Ardından, güç yönetimi için bilgisayarları içeren bir koleksiyona atayın. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../deploy/configure-client-settings.md).  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **istemci ayarları** düğümünü seçin ve **varsayılan istemci ayarları**' nı seçin.

1. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Güç yönetimi** grubunu seçin.  

1. **Cihazların güç yönetimine izin**vermek için istemci ayarını etkinleştirin.

1. İhtiyaç duyduğunuz ek istemci ayarlarını yapılandırın. Daha fazla bilgi için bkz. [istemci ayarları-güç yönetimi hakkında](../../deploy/about-client-settings.md#power-management).  

İstemci ilkesi bir sonraki sefer indirdiklerinde istemciler bu ayarları yapılandırır. Tek bir istemci için ilke almayı başlatmak için bkz. [istemcileri yönetme](../manage-clients.md#BKMK_PolicyRetrieval).  

## <a name="exclude-computers"></a>Bilgisayarları hariç tut

Bilgisayar koleksiyonlarının güç yönetimi ayarlarını almasını engelleyebilirsiniz. Bir bilgisayar, güç yönetimi ayarlarından çıkardığınız *herhangi* bir koleksiyonun üyesiyse, bu bilgisayar güç yönetimi ayarlarını uygulamaz. Bu davranış, güç yönetimi ayarlarını uygulayan başka bir koleksiyonun üyesi olsa da geçerlidir.  

Aşağıdaki nedenlerle bilgisayarları güç yönetimi dışında bırakmak isteyebilirsiniz:  

- Bilgisayarların her zaman açık olmasını zorunlu kılan bir iş gereksiniminiz olabilir.  

- Güç yönetimi ayarlarını uygulamak istemediğiniz bir bilgisayar denetim koleksiyonuna sahipsiniz.  

- Bilgisayarlarınızdan bazıları güç yönetimi ayarları uygulama özelliğine sahip olmayabilir.  

- Windows Server çalıştıran bilgisayarları güç yönetiminin dışında bırakmak isteyebilirsiniz.  

> [!NOTE]  
> İstemci ayarını **kullanıcıların cihazlarını güç yönetiminden dışlamalarını sağlayacak**şekilde yapılandırırsanız, kullanıcılar yazılım merkezi 'ni kullanarak kendi bilgisayarlarını güç yönetiminden hariç tutabilir.  

Hangi bilgisayarların güç yönetiminin dışında tutulduğunu öğrenmek için, **Dışlanan bilgisayarları**çalıştırın. Bu rapor hakkında daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](monitor-and-plan-for-power-management.md#BKMK_Excluded).  

> [!IMPORTANT]  
> Bir bilgisayarı güç yönetimi dışında bırakmak, tüm güç ayarlarının özgün değerlerine döndürülmesine neden olur. Güç ayarları, özgün değerlerine ayrı ayrı döndürülemez.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Bir bilgisayar koleksiyonunu güç yönetimi dışında bırakma  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin.  

1. Güç yönetiminin dışında bırakmak istediğiniz koleksiyonu seçin. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Güç yönetimi** sekmesine geçin ve **Bu koleksiyondaki bilgisayarlara güç yönetimi ayarlarını hiçbir şekilde uygulama**' yı seçin.  

## <a name="next-steps"></a>Sonraki adımlar

[Güç planı oluşturma ve uygulama](create-and-apply-power-plans.md)

[Güç yönetimini izleme ve planlama](monitor-and-plan-for-power-management.md)
