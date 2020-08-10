---
title: Windows Defender’ı etkinleştirme | Microsoft Docs
description: Şirket kaynaklarına erişmek için Windows Defender’ı etkinleştirme hakkında bilgi edinin.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: eded7186c670699fa654b0a1be1a7d46c027a56a
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/10/2020
ms.locfileid: "88047996"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Şirket kaynaklarına erişmek için Windows Defender’ı etkinleştirme

Kuruluşlar, kaynaklarına erişen cihazların güvenli hale getirildiklerinden emin olmak istiyor ve bu nedenle [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx)kullanmanız gerekebilir. Windows Defender, Windows 'a dahil olan ve cihazınızın virüslere ve diğer kötü amaçlı yazılımlara ve tehditlere karşı korunmasına yardımcı olabilecek bir virüsten koruma yazılımıdır. 

Bu makalede, kuruluşunuzun virüsten koruma gereksinimlerini karşılamak ve erişim sorunlarını çözmek üzere cihaz ayarlarınızı güncelleştirme yöntemi açıklanır. 

## <a name="turn-on-windows-defender"></a>Windows Defender’ı etkinleştirme
Cihazınızda Windows Defender 'ı açmak için aşağıdaki adımları izleyin. 

1. **Başlat** menüsünü seçin.
2. Arama çubuğuna **Grup İlkesi**yazın.
3. **Grup Ilkesini Düzenle**' yi seçin. Yerel Grup İlkesi Düzenleyicisi açılır.
4. **Bilgisayar yapılandırması**  >  **Yönetim Şablonları**  >  **Windows bileşenleri**  >  **Windows Defender virüsten koruma**' yı seçin. 
5. Listenin en altına gidin ve **Windows Defender virüsten koruma 'yı**Kapat ' ı seçin.  
6. **Devre dışı** veya **yapılandırılmamış**' ı seçin. Adlar, Windows Defender 'ı kapatmanızı önerdiğinizi öneren bu seçenekleri belirlemek için sayaç sezgisel olabilir. Endişelenmeyin, bu seçenekler aslında açık olduğundan emin olur. 
7. **Uygula**  >  **Tamam ' ı**seçin.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Gerçek zamanlı ve buluta teslim edilen korumayı açın

Gerçek zamanlı ve buluta teslim edilen korumayı açmak için aşağıdaki adımları izleyin. Bu virüsten koruma özellikleri birlikte, sizi casus yazılımlara karşı korur ve bulut aracılığıyla kötü amaçlı yazılım sorunlarıyla ilgili düzeltmeler sunabilir. 

1. **Başlat** menüsünü seçin,
2. Arama çubuğuna **Windows güvenliği**yazın. Eşleşen sonucu seçin. 
3. **Virüs & tehdit koruması**' nı seçin.
4. **Virüs & tehdit koruması ayarları**' nın altında **Ayarları Yönet**' i seçin.
5. **Gerçek zamanlı koruma** ve **buluta teslim edilen koruma** altındaki her anahtarı açıp açmak için çevirin. 

Bu seçenekleri ekranınızda görmüyorsanız, bunlar gizlenmiş olabilir. Bunları görünür yapmak için aşağıdaki adımları izleyin.  

1. **Başlat**' ı seçin, **Denetim Masası**' nı açın.
2. Arama çubuğuna **Grup İlkesi**yazın.
3. **Grup Ilkesini Düzenle**' yi seçin. Yerel Grup İlkesi Düzenleyicisi açılır.
3. **Computer Configuration**  >  **Administrative Templates**  >  **Windows bileşenleri**  >  **Windows Güvenlik**  >  **virüsü ve tehdit koruması**Yönetim Şablonları bilgisayar yapılandırması ' nı seçin.
4. **Virüs ve tehdit koruması alanını Gizle '** yi seçin.
5. **Devre dışı**seçeneğini belirleyin  >  **Apply**  >  **Tamam**.  

## <a name="update-your-antivirus-definitions"></a>Antivirüs tanımlarınızı güncelleştirme
Virüsten koruma tanımlarınızı güncelleştirmek için aşağıdaki adımları izleyin.  
1. **Başlat** menüsünü seçin,
2. Arama çubuğuna **Windows güvenliği**yazın. Eşleşen sonucu seçin. 
3. **Virüs & tehdit koruması**' nı seçin.
4. **Virüs & tehdit koruması güncelleştirmeleri**bölümünde **Güncelleştirmeleri denetle**' yi seçin. Ekranınızda bu seçeneği görmüyorsanız, [gerçek zamanlı korumayı etkinleştirme](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection)' deki ilk adım kümesini doldurun. Sonra güncelleştirmeleri yeniden denetlemeyi deneyin. 

## <a name="next-steps"></a>Sonraki adımlar  

Bu bilgiler yardımcı olmadı mı? Şirketinizin destek bölümüne başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.
