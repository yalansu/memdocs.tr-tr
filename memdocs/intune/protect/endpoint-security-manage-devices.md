---
title: Microsoft Intune için uç nokta güvenliği olan cihazları yönetme | Microsoft Docs
description: Güvenlik yöneticilerinin cihazları görüntülemek için uç nokta güvenlik düğümünü nasıl kullanabileceğinizi ve bunları Microsoft uç noktası Yöneticisi ' nde yönetmeyi nasıl sağlayabileceğini öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 8171eb3cf484c61e2b99046b36553a633d92044e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431248"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Microsoft Intune uç nokta güvenliği olan cihazları yönetme

Güvenlik Yöneticisi olarak, cihazlarınızı gözden geçirmek ve yönetmek için Microsoft Uç Nokta Yöneticisi Yönetim Merkezi 'ndeki *tüm cihazlar* görünümünü kullanın. Görünüm, Azure Active Directory (Azure AD) tüm cihazlarınızın bir listesini görüntüler. Bu, Intune ve Configuration Manager ile [birlikte ortak yönetim](https://docs.microsoft.com/configmgr/comanage/overview) aracılığıyla ıntune, Configuration Manager ve ile yönetilen cihazları içerir. Cihazlar, Azure AD 'niz ile tümleştirildiğinde bulutta ve şirket içi altyapınızdan olabilir.

 Görünümü bulmak için [Microsoft Endpoint Manager yönetim merkezini](https://go.microsoft.com/fwlink/?linkid=2109431) açın ve **uç nokta güvenliği**  >  **tüm cihazlar**' ı seçin.

İlk *tüm cihazlar* görünümü cihazlarınızı görüntüler ve her biri hakkında önemli bilgiler içerir:

- Cihazın yönetimi
- Uyumluluk durumu
- İşletim sistemi ayrıntıları
- Cihazın en son ne zaman iade edilme
- Ve daha fazlası

![Yönetim merkezinde tüm cihaz görünümü](./media/endpoint-security-manage-devices/all-device-view.png)

Cihaz ayrıntılarını görüntülerken daha fazla bilgi için detaya gitmeyi istediğiniz bir cihaz seçebilirsiniz.

## <a name="available-details-by-management-type"></a>Yönetim türüne göre kullanılabilir Ayrıntılar

Cihazları Microsoft Endpoint Manager Yönetim Merkezi 'nde görüntülerken cihazın nasıl yönetildiğini göz önünde bulundurun. Yönetim kaynağı, Yönetim merkezinde sunulan bilgileri ve cihazı yönetmek için hangi eylemlerin kullanılabildiğini etkiler.

Aşağıdaki alanları göz önünde bulundurun:

- **Yöneten** : Bu sütun cihazın nasıl yönetildiğini tanımlar. Yöneten seçenekleri şunlardır:

  - **MDM** -bu cihazlar Intune tarafından yönetilir. Uyumluluk verileri Intune tarafından yönetim merkezine toplanır ve raporlanır.

  - **ConfigMgr** : Bu cihazlar, Configuration Manager ile yönettiğiniz cihazları eklemek için *kiracı ekleme* kullandığınızda Microsoft Endpoint Manager Yönetim merkezinde görüntülenir. Yönetilmek üzere cihazın Configuration Manager istemcisini çalıştırması ve şunları yapmanız gerekir:

    - Bir çalışma grubunda (AAD 'ye katılmış ve aksi takdirde)
    - Etki alanına katılmış
    - Karma AAD 'ye katılmış (AD ve AAD 'ye katılmış)

    Configuration Manager tarafından yönetilen cihazların uyumluluk durumu, Microsoft Endpoint Manager Yönetim merkezinde görünmez.

    Daha fazla bilgi için, Configuration Manager belgelerinde [kiracı eklemeyi etkinleştirme](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions) konusuna bakın.

  - **MDM/ConfigMgr Aracısı** – bu cihazlar, ıntune ile Configuration Manager arasında ortak yönetim altındadır.

    Ortak yönetim sayesinde, hangi yönlerinin Configuration Manager veya Intune tarafından yönetildiğini belirlemek için [farklı ortak yönetim iş yüklerini seçersiniz](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) . Bu seçimler, cihazın hangi ilkelere uygulanacağını ve uyumluluk verilerinin yönetim merkezine nasıl raporlanacağı ile ilgilidir.

    Örneğin, virüsten koruma, güvenlik duvarı ve şifreleme için ilkeyi yapılandırmak üzere Intune 'u kullanabilirsiniz. Bu ilke türleri *Endpoint Protection*ilke olarak değerlendirilir. Ortak yönetilen bir cihazın Configuration Manager ilkelerini değil Intune ilkelerini kullanması için, Endpoint Protection için ortak yönetim kaydırıcısını *Intune* veya *pilot Intune*olarak ayarlayın. Kaydırıcı Configuration Manager olarak ayarlandıysa, cihaz bunun yerine Configuration Manager ilkeleri ve ayarları kullanır.

- **Uyumluluk**: uyumluluk, cihaza atanan uyumluluk ilkelerine göre değerlendirilir. Bu ilkelerin kaynağı ve konsolundaki bilgiler cihazın yönetilme yöntemine bağlıdır; Intune, Configuration Manager veya ortak yönetim. Ortak yönetilen cihazlarda uyumluluğu raporlamak üzere cihaz uyumluluğu için ortak yönetim kaydırıcısını Intune veya pilot Intune olarak ayarlayın.  

  Uyumluluk bir cihaz için yönetim merkezine bildirildikten sonra, ek ayrıntıları görüntülemek için ayrıntılara gidebilirsiniz. Bir cihaz uyumlu olmadığında, hangi ilkelerin uyumlu olmadığı hakkında bilgi edinmek için detaylarına gidin. Bu bilgiler sizi araştırmanıza ve cihazı uyumlu hale getirmenize yardımcı olabilir.

- **Son iade**: Bu alan, cihazın durumunu en son bildirdiği zamanı tanımlar.

## <a name="review-a-devices-policy"></a>Bir cihaz ilkesini gözden geçirme

Cihazların listesini görüntülerken, bu cihazın *genel bakış* sayfasını açarak ilgili daha fazla bilgi için detaya gitmeyi istediğiniz bir cihaz seçebilirsiniz.

Bir cihazın Genel Bakış sayfasında, o cihaza uygulanan uç nokta güvenlik ilkelerini görüntülemek için **uç nokta güvenlik yapılandırması** ' nı seçebilirsiniz. İlke ayrıntıları MDM ve Intune tarafından yönetilen cihazlar için kullanılabilir.

![Uç nokta güvenlik ilkesi ayrıntılarını görüntüle](./media/endpoint-security-manage-devices/view-policy-details.png)

Configuration Manager tarafından yönetilen cihazlar ilke ayrıntılarını görüntülemez. Bu cihazlarla ilgili ek bilgileri görüntülemek için Configuration Manager konsolunu kullanın.

## <a name="remote-actions-for-devices"></a>Cihazlar için uzak eylemler

Uzak eylemler, Microsoft Endpoint Manager yönetim merkezinden bir cihaza başlayabilmeniz veya uygulayabileceğiniz eylemlerdir. Bir cihazın ayrıntılarını görüntülediğinizde, cihaza uygulanan uzak eylemlere erişebilirsiniz.

Uzak eylemler, cihazların *genel bakış* sayfasının üst kısmında görüntülenir. Ekranınızdaki sınırlı alan nedeniyle görüntülenebilecek eylemler, sağ taraftaki üç nokta seçilerek kullanılabilir:

![Ek eylemleri görüntüle](./media/endpoint-security-manage-devices/view-additional-actions.png)

Kullanılabilir uzak eylemler cihazın yönetilme biçimine bağlıdır:

- **Intune**: cihaz platformu için uygulanan tüm [Intune uzak eylemleri](../remote-actions/device-management.md) kullanılabilir.  
- **Configuration Manager**: aşağıdaki Configuration Manager eylemleri kullanabilirsiniz:

  - Makine Ilkesini Eşitle
  - Kullanıcı Ilkesini eşitleme
  - Uygulama değerlendirme çevrimi

- **Ortak yönetim**: hem Intune uzak eylemlerine hem de Configuration Manager eylemlere erişebilirsiniz.

Bazı Intune uzak eylemleri, cihazların güvenli hale getirilmesine veya cihazda olabilecek verilerin korunmasına yardımcı olabilir. Uzak eylemlerle şunları yapabilirsiniz:

- Bir cihazı kilitleme
- Bir cihazı sıfırlama
- Şirket verilerini kaldırma
- Zamanlanan bir çalıştırmanın dışında kötü amaçlı yazılım taraması yapın
- BitLocker anahtarlarını döndür

Aşağıdaki Intune uzak eylemleri Güvenlik Yöneticisi ile ilgilenir ve [tam listenin](../remote-actions/device-inventory.md#view-the-device-details)bir alt kümesidir. Tüm eylemler tüm cihaz platformları için kullanılamaz. Bağlantılar, her eylem için derinlemesine ayrıntılar sağlayan içeriğe gider.

- [Cihazı eşitler](../remote-actions/device-sync.md) – cihazın Intune ile hemen iade edilmiş olmasını sağlayabilirsiniz. Bir cihaz iade edildiğinde, kendisine atanmış bekleyen eylemleri veya ilkeleri alır.  

- [Yeniden Başlat](../remote-actions/device-restart.md) – beş dakika Içinde bir Windows 10 cihazını yeniden başlamaya zorlayın. Cihaz sahibine otomatik olarak yeniden başlatma bildirilmez ve iş kaybolabilir.

- [Hızlı tarama](../configuration/device-restrictions-windows-10.md) – Defender 'ın kötü amaçlı yazılım için cihazda hızlı bir tarama çalıştırmasını ve sonuçları Intune 'a göndermesini sağlar. Hızlı tarama, kayıt defteri anahtarları ve bilinen Windows başlangıç klasörleri gibi kötü amaçlı yazılımların kaydedildiği yaygın konumlara bakar.

- [Tam tarama](../configuration/device-restrictions-windows-10.md) – Defender 'ın kötü amaçlı yazılım taraması çalıştırmasını ve sonuçları Intune 'a göndermesini sağlar. Tam tarama, kötü amaçlı yazılımın kaydedildiği yaygın konumlara bakar ve cihazdaki her dosyayı ve klasörü tarar.

- Windows Defender güvenlik zekası 'nı güncelleştirme – cihazın, Microsoft Defender virüsten koruma için kötü amaçlı yazılım tanımlarını güncelleştirmesini sağlayabilirsiniz. Bu eylem bir tarama başlatmıyor.

- [BitLocker anahtar döndürme](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – Windows 10 sürüm 1909 veya üstünü çalıştıran bir cihazın BitLocker kurtarma anahtarını uzaktan döndürün.

Aynı anda birden çok cihaz için *devre dışı bırakma* ve *silme* gibi bazı eylemleri yönetmek için **toplu cihaz eylemlerini** de kullanabilirsiniz. [Toplu eylemler](../remote-actions/bulk-device-actions.md) *tüm cihazlar* görünümünden kullanılabilir. Platform, eylem ve en fazla 100 cihaz belirtirsiniz.

![Toplu eylemleri seçin](./media/endpoint-security-manage-devices/select-bulk-actions.png)

Cihazlar için yönettiğiniz seçenekler, cihaz Intune 'a iade edilene kadar etkili olmaz.

## <a name="next-steps"></a>Sonraki adımlar

[Intune 'da Endpoint Security 'yi yönetme](../protect/endpoint-security.md)