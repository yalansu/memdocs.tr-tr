---
title: Uzaktan denetimi yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager uzaktan denetimi ayarlayın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076739"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Configuration Manager uzaktan denetimi yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Bu yordam, uzaktan denetim için varsayılan istemci ayarlarının yapılandırılmasını açıklamaktadır. Bu ayarlar hiyerarşinizdeki tüm bilgisayarlar için geçerlidir. Bu ayarların yalnızca bazı bilgisayarlara uygulanmasını istiyorsanız, bu bilgisayarları içeren bir koleksiyona özel bir cihaz istemci ayarı atayın. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../../../core/clients/deploy/configure-client-settings.md). 

Uzaktan Yardım veya uzak masaüstü 'Nü kullanmak için, Configuration Manager konsolunu çalıştıran bilgisayarda yüklü ve yapılandırılmış olmalıdır. Uzaktan Yardım veya Uzak Masaüstü özelliklerini yükleme ve yapılandırma hakkında daha fazla bilgi için Windows belgelerine bakın.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Uzaktan denetimi etkinleştirmek ve istemci ayarlarını yapılandırmak için  

1. Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

2. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

3. **Varsayılan** Iletişim kutusunda **Uzak Araçlar**' ı seçin.  

4. Uzaktan denetim, uzaktan yardım ve uzak masaüstü istemci ayarlarını yapılandırın. Yapılandırabileceğiniz uzak Araçlar istemci ayarlarının listesi için bkz. [Uzak Araçlar](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   **Bilgisayar Aracısı** istemci ayarlarında **Yazılım Merkezi’nde görüntülenen kuruluş adı** için bir değer yapılandırarak **ConfigMgr Uzaktan Denetim** iletişim kutusunda görüntülenen şirket adını değiştirebilirsiniz.  

   İstemci bilgisayarlar, istemci ilkesini sonraki sefer indirdiklerinde bu ayarlarla yapılandırılır. Tek bir istemci için ilke almayı başlatmak için bkz. [istemcileri yönetme](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Klavye çevirisini etkinleştir

Varsayılan olarak Configuration Manager, ana konumu görüntüleyicisinin konumundan paylaşan konumuna iletir. Bu, görüntüleyiciye farklı olan klavye yapılandırmalarına yönelik bir sorun sunabilir. Örneğin, Ingilizce Klavye içeren bir görüntüleyici bir "A" yazabilir, ancak paylaşan Fransızca klavyesi bir "Q" sağlar. Artık, bir karakterin kendisini görüntüleyiciye ve paylaşan kişinin türüne iletilmesi için uzaktan denetimi yapılandırma seçeneğiniz vardır. bu şekilde,

Klavye çevirisini açmak için **Configuration Manager uzaktan denetim**bölümünde **eylem**' i seçin ve anahtar konumunu Iletmek için **klavye çevirisini etkinleştir** ' i seçin.

> [!NOTE]
>
> ~! # @ $% Gibi özel anahtarlar doğru çevrilemeyecek.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Uzaktan denetim görüntüleyicisine yönelik klavye kısayolları

|Klavye kısayolu|Açıklama|  
|-----------------------|-----------------|  
|Alt+Page Up|Çalışan programlar arasında soldan sağa geçiş yapar.|  
|Alt+Page Down|Çalışan programlar arasında sağdan sola geçiş yapar.|  
|Alt+Insert|Çalışan programlar arasında açıldıkları sırayla geçiş yapar.|  
|Alt+Home|**Başlat** menüsünü gösterir.|  
|Ctrl+Alt+End|Windows Güvenliği iletişim kutusunu (Ctrl+Alt+Del) görüntüler.|  
|Alt+Delete|Windows menüsünü görüntüler.|  
|Ctrl+Alt+Eksi İşareti (sayısal tuş takımında)|Yerel bilgisayarın etkin penceresini uzak bilgisayar Panosuna kopyalar.|  
|Ctrl+Alt+Artı İşareti (sayısal tuş takımında)|Yerel bilgisayarın tüm pencere alanını uzak bilgisayar Panosuna kopyalar.|  
