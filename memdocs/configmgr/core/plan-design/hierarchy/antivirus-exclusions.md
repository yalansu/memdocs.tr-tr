---
title: Virüsten koruma dışlamaları
titleSuffix: Configuration Manager
description: Olası sorunları giderirken kullanılmak üzere önerilen virüsten koruma dışlamaları hakkında bilgi edinin.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f3f38de1d7440ffd0293bde359deeb6be3bbeffb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906202"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Configuration Manager için önerilen antivirüs dışlamaları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, bir yöneticinin virüsten koruma yazılımıyla birlikte kullanıldığında Configuration Manager site sunucuları, site sistemleri ve istemcilerinin desteklenen bir sürümünü çalıştıran bir bilgisayarda olası kararsızlık nedenini belirlemesine yardımcı olabilecek öneriler içerir.

> [!IMPORTANT]
>
> - Bir sistemi değerlendirmek için bu yordamları geçici olarak uygulamanızı öneririz. Bu makalede yapılan öneriler tarafından sistem performansı veya kararlılığı iyileştiriliyorsa, yönergeler ve virüsten koruma yazılımının güncelleştirilmiş bir sürümü için virüsten koruma yazılımı satıcınıza başvurun.
> - Bu makale, güvenlik ayarlarının daha düşük veya bir bilgisayardaki güvenlik özelliklerini geçici olarak devre dışı bırakma konusunda nasıl yardımcı olduğunu gösteren bilgiler içerir. Belirli bir sorunun doğasını anlamak için bu değişiklikleri yapabilirsiniz. Bu değişiklikleri yapmadan önce, bu geçici çözümü özel ortamınızda uygulamayla ilişkili riskleri değerlendirmeniz önerilir.

## <a name="possible-symptoms"></a>Olası belirtiler 

Virüsten koruma gerçek zamanlı koruma, Configuration Manager site sunucuları, site sistemleri ve istemcilerde birçok soruna neden olabilir.

Olası belirtilerin kapsamlı olmayan bir listesi aşağıda verilmiştir:

- Uzak site sistemi bileşenleri yüklü değil. SiteComp. log, Distmgr. log, HMAN. log veya diğer Configuration Manager günlük dosyalarında hata 80070005 gibi hatalar bulunabilir.
- Configuration Manager istemcisi Client Push kullanılarak yüklenemez.
- İstemci Envanter bilgileri hatalı, eksik veya güncel değil.
- Biriktirme listeleri *Install_Directory*\Program Files\Microsoft Configuration manager\kutularının klasörlerinde oluşur.
- Yazılım Merkezi, istemci sistemlerinde dağıtılan yazılımlar tarafından doldurulmaz veya başlatılmaz. Ayrıca, CCMRepair. log dosyasında aşağıdaki örneğe benzer hatalar bulunabilir:

  > Veritabanı doğrulaması şu sonuçla başarısız oldu: 0x80004005 ancak DB: C:\windows\ccm\dosyaadı. sdf açılabilir, DB onarımı atlanıyor.

- İstemcilere dağıtılan yazılım yüklenemez.
- Yazılım dağıtımları için uyumluluk verileri yanlış.

## <a name="exclusions"></a>Dışlamalar

Bu tür sorunları engellemek için aşağıdaki gerçek zamanlı koruma dışlamalarını eklemenizi öneririz:

### <a name="default-installation-folders"></a>Varsayılan yükleme klasörleri

|  |  |
| - | - |
|*ConfigMgr yükleme klasörü*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*MP yükleme klasörü*  |% ProgramFiles% \ SMS_CCM  |  
|*İstemci yükleme klasörü*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Site sunucuları için klasör dışlamaları

- *ConfigMgr yükleme klasörü*\gelen kutuları
- *ConfigMgr yükleme klasörü*\Logs
- *ConfigMgr yükleme klasörü*\Easysetuppayload

### <a name="folder-exclusions-for-site-systems"></a>Site sistemleri için klasör dışlamaları

- Yönetim noktaları
  - *MP yükleme klasörü*\Servicedata
  - Aşağıdakilerden biri:
    - *ConfigMgr yükleme klasörü*\Mp\outkutularý
    - *Yükleme sürücüsü*\Sms\mp\outkutularý
- Dağıtım noktaları
  - *İstemci yükleme klasörü*\Servicedata
  - *ContentLib_Drive*\ SMS_DP $
  - *ContentLib_Drive*\Smspkg*Drive_Letter*$
  - *ContentLib_Drive*\Smspkg
  - *ContentLib_Drive*\Smspkgsig
  - *ContentLib_Drive*\Smssıg $
- Site veritabanı sunucuları
  - [SQL Server çalıştıran bilgisayarlarda çalıştırılacak virüsten koruma yazılımı seçme](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>İstemciler için klasör dışlamaları

- *Istemci yükleme klasörü* \\ \* . sdf
- *Istemci yükleme klasörü*\Servicedata
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Istemci yükleme klasörü*\Logs

### <a name="file-exclusions-for-mps"></a>MPs için dosya dışlamaları

- POL00000. pol
  - *MP yükleme klasörü*\Polreqhazırlama

### <a name="process-exclusions"></a>İşlem dışlamaları

İşlem Dışlamaları yalnızca, agresif virüsten koruma programları Configuration Manager program dosyalarını (. exe dosyaları) yüksek riskli işlemler olacak şekilde kabul ediyorsanız gereklidir.

- *ConfigMgr yükleme klasörü*\bin\64\Smsexec.exe
- Aşağıdaki işlemlerden birini yapın:
  - *Istemci yükleme klasörü*\Ccmexec.exe
  - *MP yükleme klasörü*\Ccmexec.exe
- *Istemci yükleme klasörü*\Cmrcservice.exe (istemci tarafı)
- *ConfigMgr yükleme klasörü*\Bin\64\sitecomp.exe
- *ConfigMgr yükleme klasörü*\Bin\64\smswriter.exe
- *ConfigMgr yükleme klasörü*\bin\64\smsssınbkup.exe veya SMS_*sqlfqdn*\Bin\x64\smsssınbkup.exe
- *ConfigMgr yükleme klasörü*\Bin\64\cmupdate.exe
- *Istemci yükleme klasörü*\Ccmrepair.exe (istemci tarafı)
- %*windir*% \ CCMSetup\Ccmsetup.exe (istemci tarafı)

## <a name="next-steps"></a>Sonraki adımlar

Virüsten koruma dışlamaları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

[Configuration Manager Güncel Dalı antivirüs dışlamaları-System Center Premier alan Mühendisi blogu](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-current-branch-antivirus-exclusions/ba-p/884831)

[OSD ve önyükleme görüntüleri hakkında daha fazla ayrıntı içeren System Center 2012 Configuration Manager virüsten koruma dışlamaları güncelleştirildi](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/updated-system-center-2012-configuration-manager-antivirus/ba-p/884371)

[SQL Server çalıştıran bilgisayarlarda çalıştırılacak virüsten koruma yazılımı seçme](https://support.microsoft.com/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Windows 'un şu anda desteklenen sürümlerini çalıştıran kurumsal bilgisayarlara yönelik virüs tarama önerileri](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
