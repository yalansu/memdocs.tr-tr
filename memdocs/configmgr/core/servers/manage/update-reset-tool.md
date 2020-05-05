---
title: Sıfırlama aracını güncelleştirme
titleSuffix: Configuration Manager
description: Configuration Manager için konsol içi güncelleştirmeler için güncelleştirme sıfırlama aracını kullanın.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720754"
---
# <a name="update-reset-tool"></a>Sıfırlama aracını güncelleştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*  


Sürüm 1706 ' den başlayarak Configuration Manager birincil siteler ve merkezi yönetim siteleri, Configuration Manager güncelleştirme sıfırlama aracı **Cmupdatereset. exe**' yi içerir. Konsol içi güncelleştirmelerin indirme veya çoğaltma sorunları olduğunda sorunları gidermek için aracı kullanın. Araç, site sunucusunun ***\CD.exe \ Test\smssetup\tools*** klasöründe bulunur.

Bu aracı, geçerli dalın destek 'te kalan herhangi bir sürümüyle birlikte kullanabilirsiniz.

[Konsol içi bir güncelleştirme](install-in-console-updates.md) henüz yüklenmemişse ve hatalı durumdaysa bu aracı kullanın. Başarısız bir durum, güncelleştirme indirmenin devam ettiğini ancak takıldığını veya aşırı uzun sürmesi anlamına gelir. Uzun bir süre, benzer boyuttaki güncelleştirme paketlerine ait geçmiş beklentilerinden daha uzun olarak değerlendirilir. Güncelleştirme, alt birincil sitelere çoğaltılmak için de bir hata olabilir.  

Aracı çalıştırdığınızda, belirttiğiniz güncelleştirmede karşı çalışır. Araç, varsayılan olarak, başarıyla yüklenen veya indirilen güncelleştirmeleri silmez.  

### <a name="prerequisites"></a>Önkoşullar
Aracı çalıştırmak için kullandığınız hesap aşağıdaki izinleri gerektirir:
- Merkezi yönetim sitesinin ve hiyerarşinizdeki her birincil sitenin site veritabanı için **okuma** ve **yazma** izinleri. Bu izinleri ayarlamak için, Kullanıcı hesabını **db_datawriter** bir üyesi olarak ekleyebilir ve her bir sitenin Configuration Manager veritabanına **db_datareader** [sabit veritabanı rolleri](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) ekleyebilirsiniz. Araç ikincil sitelerle etkileşime girmiyor.
- Hiyerarşinizin en üst düzey sitesinde **yerel yönetici** .
- Hizmet bağlantı noktasını barındıran bilgisayarda **yerel yönetici** .

Sıfırlamak istediğiniz güncelleştirme paketinin GUID 'sine ihtiyacınız vardır. GUID 'yi almak için:
  1.   Konsolunda, **Yönetim** > **güncelleştirmeleri ve bakım**' a gidin.
  2.   Görüntü bölmesinde, sütunlardan birinin başlığına ( **durum**gibi) sağ tıklayın ve ardından bu sütunu görüntülenecek şekilde eklemek Için **paket GUID** ' i seçin.
  3.   Sütunda artık güncelleştirme paketi GUID 'SI gösterilmektedir.

> [!TIP]  
> GUID 'yi kopyalamak için, sıfırlamak istediğiniz güncelleştirme paketinin satırını seçin ve ardından CTRL + C tuşlarını kullanarak bu satırı kopyalayın. Kopyalanmış seçiminizi bir metin düzenleyicisine yapıştırırsanız, aracı çalıştırdığınızda yalnızca bir komut satırı parametresi olarak kullanılacak GUID 'yi kopyalayabilirsiniz.

### <a name="run-the-tool"></a>Aracı çalıştırma    
Aracın hiyerarşinin en üst düzey sitesinde çalıştırılması gerekir.

Aracı çalıştırdığınızda, şunu belirtmek için komut satırı parametrelerini kullanın:
- Hiyerarşinin üst katman sitesindeki SQL Server.
- Üst katman sitesindeki Site veritabanı adı.
- Sıfırlamak istediğiniz güncelleştirme paketinin GUID 'ı.

Araç, güncelleştirmenin durumuna göre erişmesi gereken ek sunucuları tanımlar.   

Güncelleştirme paketi *karşıdan yükleme sonrası* durumundaysa, araç paketi temizlemez. Bir seçenek olarak, başarıyla indirilen bir güncelleştirmenin zorla silme parametresini kullanarak kaldırılmasını zorlayabilirsiniz (Bu konunun ilerleyen kısımlarında komut satırı parametrelerine bakın).

Araç çalıştıktan sonra:
- Bir paket silinmişse, üst katman sitesindeki SMS_Executive hizmetini yeniden başlatın. Ardından, paketi yeniden indirebilmeniz için güncelleştirmeleri denetleyin.
- Bir paket silinmediği takdirde herhangi bir işlem yapmanız gerekmez. Güncelleştirme yeniden başlatılır ve sonra çoğaltmayı veya yüklemeyi yeniden başlatır.

**Komut satırı parametreleri:**  


|                        Parametre                         |                                                       Açıklama                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;en üst katman sitenizin SQL Server FQDN 'si>** | *Gerekli* <br> Hiyerarşinizin üst katman sitesi için site veritabanını barındıran SQL Server FQDN 'sini belirtin. |
|                **-D &lt;veritabanı adı>**                 |                          *Gerekli* <br> Üst katman sitesinde veritabanının adını belirtin.                          |
|                 **-P &lt;paketi GUID>**                 |                        *Gerekli* <br> Sıfırlamak istediğiniz güncelleştirme paketi için GUID 'YI belirtin.                        |
|           **-I &lt;SQL Server örnek adı>**           |                    *İsteğe Bağlı* <br> Site veritabanını barındıran SQL Server örneğini belirler.                     |
|                       **-FDELETE**                       |                       *İsteğe Bağlı* <br> Başarıyla indirilen bir güncelleştirme paketini silmeye zorlar.                        |

**Örnekler**  
Tipik bir senaryoda, indirme sorunları olan bir güncelleştirmeyi sıfırlamak istersiniz. SQL Server FQDN 'niz *server1.fabrikam.com*, site veritabanı *CM_XYZ*ve paket GUID 'si *61F16b3c-f1f6-4f9f-8647-2a524b0c802c*olur.  Şunu çalıştırırsınız: ***Cmupdatereset. exe-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

Daha Extreme bir senaryoda sorunlu güncelleştirme paketinin silinmesini zorlamak isteyebilirsiniz. SQL Server FQDN 'niz *server1.fabrikam.com*, site veritabanı *CM_XYZ*ve paket GUID 'si *61F16b3c-f1f6-4f9f-8647-2a524b0c802c*olur.  Şunu çalıştırırsınız: ***Cmupdatereset. exe-FDELETE-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
