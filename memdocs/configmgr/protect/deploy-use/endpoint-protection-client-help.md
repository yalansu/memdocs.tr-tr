---
title: Endpoint Protection Istemci yardımı
titleSuffix: Configuration Manager
description: Bilgisayarınızı tehditlere karşı korumanıza daha iyi yardımcı olan Endpoint Protection Özellikler ve geliştirmeler hakkında bilgi edinin.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724345"
---
# <a name="endpoint-protection-client-help"></a>Endpoint Protection Istemci yardımı

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Windows Defender veya Endpoint Protection bu sürümü, bilgisayarınızı tehditlere karşı korumaya yardımcı olmak için aşağıdaki özellikleri içerir:  

-   **Windows Güvenlik Duvarı tümleştirmesi.** Endpoint Protection kurulumu Windows Güvenlik Duvarı’nı açmanıza veya kapatmanıza olanak sağlar.  
-   **Ağ İnceleme Sistemi.** Bu özellik, bilinen ağ tabanlı güvenlik açıklarına karşı etkin bir şekilde korumaya yardımcı olmak üzere ağ trafiğini denetleyerek gerçek zamanlı korumayı iyileştirir.  
-   **Koruma Altyapısı.** Gerçek zamanlı koruma, kötü amaçlı yazılımların bilgisayarınıza yüklenmesini veya bilgisayarınızdan çalıştırılmasını algılar ve sonlandırır. Güncelleştirilmiş altyapı, gelişmiş algılama ve temizleme özellikleriyle daha iyi performans sunar.  

Windows Defender, Windows 10 işletim sisteminin bir parçası olarak gelir.  Windows 'un önceki sürümlerinde yöneticiniz, yönetim yazılımını kullanarak Windows Defender veya Endpoint Protection sağlayabilir.

Ayrıca, [Windows Defender ve Endpoint Protection için sık sorulan soruların](endpoint-protection-client-faq.md)bir listesini de bulabilirsiniz. Yardım sorunlarını giderme için bkz. [Windows Defender veya Endpoint Protection Istemcisinde sorun giderme](troubleshoot-endpoint-client.md). Yeni özelliklerin listesi için bkz. yenilikler [Windows Defender istemcisi](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Windows Güvenlik Duvarı tümleştirmesi  
 Windows Güvenlik Duvarı saldırganların veya kötü amaçlı yazılımların İnternet veya ağ üzerinden bilgisayarınıza erişmesini engellemeye yardımcı olabilir. Artık Endpoint Protection uygulamasını yüklediğinizde, yükleme sihirbazı Windows Güvenlik Duvarı’nın açık olduğunu doğrular. Windows Güvenlik Duvarı'nı bilerek kapattıysanız, onay kutusunun işaretini kaldırarak açılmasını önleyebilirsiniz. Windows Güvenlik Duvarı ayarlarını Denetim Masası'ndaki Sistem ve Güvenlik ayarlarından istediğiniz zaman değiştirebilirsiniz.  

## <a name="network-inspection-system"></a>Ağ Denetleme Sistemi  
 Saldırganlar, satıcıların güvenlik güncelleştirmeleri geliştirip dağıtmalarından önce, görünen güvenlik açıklarına karşı giderek daha fazla ağ tabanlı saldırı gerçekleştiriyor. Güvenlik açıklarıyla ilgili yapılan çalışmalar, ilk saldırının raporlanması ile uygun bir güvenlik güncelleştirmesinin geliştirilmesi, test edilmesi ve yayımlanması arasında bir ay veya daha uzun bir süre geçebildiğini gösteriyor. Bu koruma boşluğu, birçok bilgisayarı önemli bir süre için saldırılara ve kötüye kullanımlara karşı savunmasız bırakır. Ağ Denetleme Sistemi, güvenlik açıklarının bildirilmesi ve güncelleştirme dağıtımı arasında geçen süreyi birkaç haftadan birkaç saate indirerek ağ tabanlı saldırılara karşı daha iyi koruma sağlamak üzere gerçek zamanlı korumayla çalışır.  

## <a name="award-winning-protection-engine"></a>Ödüllü koruma altyapısı  
 Windows Defender 'ın veya Endpoint Protection, düzenli olarak güncellenen ödül kazanmış koruma altyapısıdır. Altyapı, günde 24 saat boyunca en yeni kötü amaçlı yazılım tehditlerine karşı yanıt sağlayan bir Microsoft Kötü Amaçlı Yazılımdan Koruma Merkezi’ndeki kötü amaçlı yazılımdan koruma araştırmacıları ekibi tarafından desteklenir.  

## <a name="windows-defender-settings"></a>Windows Defender ayarları
Windows Defender ayarları, BILGISAYARıNıZı kötü amaçlı yazılımlardan korumaya yardımcı olan ayarları etkinleştirir. Yöneticiniz bazı Windows Defender ayarlarını sizin için yönetebilir. Windows Defender ayarlarını kullanarak diğerlerini yönetebilirsiniz. BILGISAYARıNıZı ve verilerinizi korumaya yardımcı olmak için Windows Defender ayarlarını etkinleştirmenizi öneririz.

Windows Defender ayarlarını görüntülemek için bilgisayarınızda arama `Windows Defender` yapın. **Windows Defender 'ı** açın ve **Ayarlar**' ı seçin. Windows Defender ayarları şunları içerir:
- **Gerçek zamanlı koruma** -bilgisayarınızda yükleme veya çalıştırma konusunda kötü amaçlı yazılım bulun ve durdurun.
- **Bulut tabanlı koruma** -Windows Defender, olası güvenlik tehditleri hakkında bilgileri Microsoft 'a gönderir.
- **Otomatik örnek gönderimi** -kötü amaçlı yazılım algılamayı iyileştirmenize yardımcı olmak Için Windows Defender 'ın Microsoft 'a şüpheli dosya örnekleri göndermesini sağlar.
- **Dışlamaları** -belirli dosyaları, klasörleri, dosya uzantılarını veya Işlemi Windows Defender taramasının içinden de kullanabilirsiniz.
- **Gelişmiş bildirim** -bilgisayarınızın sistem durumunu bildiren bildirimleri sunar. **Kapalı** olsa da, kritik bildirimler alacaksınız.
- **Windows Defender çevrimdışı** -kötü amaçlı yazılımları bulmaya ve kaldırmaya yardımcı olması Için Windows Defender 'ı çevrimdışı çalıştırabilirsiniz. Bu tarama, bilgisayarınızı yeniden başlatacak ve yaklaşık 15 dakika sürer.

### <a name="see-also"></a>Ayrıca bkz.  
 [Endpoint Protection istemci sık sorulan sorular](endpoint-protection-client-faq.md)   
 [Windows Defender veya Endpoint Protection istemcisi sorunlarını giderme](troubleshoot-endpoint-client.md)
