---
title: Microsoft Intune-Azure için Microsoft tüneli VPN çözümünün durumunu izleyin | Microsoft Docs
description: Linux üzerinde çalışan bir VPN sunucusu olan Microsoft Tunnel Gateway 'in durumunu izleyin. Intune ile yönettiğiniz bulut tabanlı cihazlar, Microsoft tüneli ile şirket içi altyapınızla iletişime geçebilirler.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 959aea0411f25f62857d1f7aaed902c2a8005c17
ms.sourcegitcommit: 6e488937039e8437866d55f2f23e5944a4b35a35
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91022377"
---
# <a name="monitor-microsoft-tunnel"></a>Microsoft tüneli izleme

Microsoft tüneli yüklendikten sonra, sunucu yapılandırmasını ve sunucu sistem durumunu Microsoft Endpoint Manager Yönetim Merkezi 'nde (endpoint.microsoft.com) görüntüleyebilirsiniz.  

## <a name="use-the-admin-center-ui"></a>Yönetim Merkezi Kullanıcı arabirimini kullanma

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde oturum açın ve *Kiracı Yönetimi*  >  *Microsoft tünel ağ geçidi*' ne gidin ve **sistem durumu** sekmesini seçin.

Önizlemede, sistem durumu yalnızca sunucunun son 5 dakika içinde bağlanıp bağlanmadığını gösterir.  Gelecekteki geliştirmeler daha fazla ayrıntı ekleyecek.

## <a name="use-mst-cli-command-line-tool"></a>MST-CLI komut satırı aracını kullanma

Microsoft tünel sunucusu hakkında bilgi almak için **MST-CLI** komut satırı aracını kullanın. Bu dosya, Microsoft tüneli yüklediğinde Linux sunucusuna eklenir. Araç şurada bulunur: **/usr/sbin/MST-cli**.

Daha fazla bilgi ve komut satırı örnekleri için bkz. [Microsoft tüneli için MST-CLI komut satırı aracı](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel-gateway).

## <a name="next-steps"></a>Sonraki adımlar

[Microsoft tüneli için başvuru](../protect/microsoft-tunnel-reference.md)
