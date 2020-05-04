---
title: Varlık Yönetim Bilgileri önkoşulları
titleSuffix: Configuration Manager
description: Configuration Manager Varlık Yönetim Bilgileri için önkoşulları alın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dfed0f2c2e8149abb05d4b21047d4d494f034e53
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714132"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Configuration Manager Varlık Yönetim Bilgileri önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Varlık Yönetim Bilgileri, ürün içinde dış bağımlılıklara ve bağımlılıklara sahiptir.  

## <a name="dependencies-external-to-configuration-manager"></a>Bağımlılıklar dış Configuration Manager  
 Aşağıdaki tabloda, Configuration Manager dış Varlık Yönetim Bilgileri bağımlılıkları verilmiştir.  

|Bağımlılık|Daha Fazla Bilgi|  
|----------------|----------------------|  
|Başarılı Oturum Açma Olaylarına İlişkin Önkoşulların Denetlenmesi|Dört adet Varlık Yönetim Bilgileri raporunda, istemci bilgisayarlarındaki Windows Güvenlik olayı günlüklerinden toplanan bilgiler görüntülenir. Güvenlik olay günlüğü ayarları tüm Başarılı oturum açma olaylarını günlüğe kaydedecek şekilde yapılandırılmadıysa bu raporlar, uygun donanım envanteri raporlama sınıfı etkinleştirilse bile herhangi bir veri içermez.<br /><br /> Aşağıdaki Varlık Yönetim Bilgileri raporları, toplanan Windows Güvenliği olay günlüğü bilgilerine bağımlıdır:<br /><br /> -Donanım 03A-birincil bilgisayar kullanıcıları<br />-Donanım 03B-belirli bir birincil konsol kullanıcısı için bilgisayarlar<br />-Donanım 04A-paylaşılan (çok kullanıcılı) bilgisayarlar<br />-Donanım 05A-belirli bir bilgisayardaki konsol kullanıcıları<br /><br /> Donanım Envanteri İstemcisi Aracısı’nı bu raporları desteklemek için gereken bilgileri envantere almak üzere etkinleştirmek için, ilk olarak istemcilerdeki Windows Güvenliği olay günlüğü ayarlarını tüm Başarılı oturum açma olaylarını günlüğe kaydedecek şekilde değiştirmeniz ve **SMS_SystemConsoleUser** donanım envanteri raporlama sınıfını etkinleştirmeniz gerekir. Güvenlik olay günlüğü ayarlarını tüm Başarılı oturum açma olaylarını günlüğe kaydedecek şekilde değiştirme hakkında daha fazla bilgi için bkz. [Enable auditing of success logon events](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  **SMS_SystemConsoleUser** donanım envanteri raporlama sınıfı, güvenlik olay günlüğünün yalnızca son 90 güne ait başarılı oturum açma olay verilerini, günlüğün uzunluğundan bağımsız olarak korur. Güvenlik olay günlüğünde 90 günden az veri varsa tüm günlük okunur.  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager'ın İç Bağımlılıkları  
 Aşağıdaki tablo, Configuration Manager iç Varlık Yönetim Bilgileri bağımlılıklarını sağlar.  

|Bağımlılık|Daha Fazla Bilgi|  
|----------------|----------------------|  
|İstemci Aracısı Önkoşulları|Varlık Yönetim Bilgileri raporları, istemci donanım ve yazılım envanter raporlarından alınan istemci bilgilerine bağımlıdır. Tüm Varlık Yönetim Bilgileri raporlarının gerektirdiği bilgileri almak için aşağıdaki istemci aracılarının etkinleştirilmesi gerekir:<br /><br /> -Donanım Envanteri İstemci Aracısı<br />-Yazılım ölçer Istemci Aracısı|  
|Donanım Envanteri İstemci Aracısı Bağımlılıkları|Bazı Varlık Yönetim Bilgileri raporlarının gerektirdiği envanter verilerini toplamak için Donanım Envanteri İstemci Aracısı’nın etkinleştirilmesi gerekir. Ayrıca, Varlık Yönetim Bilgilerinin bağlı olduğu bazı donanım envanteri raporlama sınıfları, birincil site sunucusu bilgisayarlarında etkinleştirilmiş olmalıdır.<br /><br /> Donanım Envanteri İstemci Aracısı etkinleştirme hakkında daha fazla bilgi için bkz. [donanım envanterini genişletme](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Yazılım Ölçümü İstemci Aracısı Bağımlılıkları|Varlık Yönetim Bilgileri yazılım raporlarının bir kısmı, veriler için Yazılım Ölçümü İstemci Aracısı’na bağımlıdır. Yazılım ölçer Istemci Aracısı 'nı etkinleştirme hakkında bilgi için bkz. [yazılım kullanım ölçümü ile uygulama kullanımını izleme](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Aşağıdaki Varlık Yönetim Bilgileri raporları, veri sağlaması için Yazılım Ölçümü İstemci Aracısına bağımlıdır:<br /><br /> -Yazılım 07A-bilgisayar sayısına göre son kullanılan yürütülebilir dosyalar<br />-Yazılım 07B-Belirli bir yürütülebilir dosyayı son kullanan bilgisayarlar<br />-Yazılım 07C-belirli bir bilgisayarda son kullanılan yürütülebilir dosyalar<br />-Yazılım 08A-kullanıcı sayısına göre son kullanılan yürütülebilir dosyalar<br />-Yazılım 08B-belirli bir yürütülebilir dosyayı kısa süre önce kullanan kullanıcılar<br />-Yazılım 08C-belirtilen bir kullanıcı tarafından son kullanılan yürütülebilir dosyalar|  
|Varlık Yönetim Bilgileri Donanım Envanteri Raporlama Sınıfı Önkoşulları|Configuration Manager ' deki Varlık Yönetim Bilgileri raporları, belirli donanım envanteri raporlama sınıflarına bağlıdır. Donanım envanteri raporlama sınıfları etkinleştirilip istemciler bu sınıflara göre donanım envanteri raporlamadığı sürece, ilişkili Varlık Yönetim Bilgileri raporları herhangi bir veri içermez. Aşağıdaki donanım envanteri raporlama sınıflarını, Varlık Yönetim Bilgileri raporlama gereksinimlerini destekleyecek şekilde etkinleştirebilirsiniz:<br /><br /> -SMS_SystemConsoleUsage<sup>1</sup><br />-SMS_SystemConsoleUser<sup>1</sup><br />-SMS_InstalledSoftware<br />-SMS_AutoStartSoftware<br />-SMS_BrowserHelperObject<br />-Win32_USBDevice<br />-SMS_InstalledExecutable<br />-SMS_SoftwareShortcut<br />-SoftwareLicensingService<br />-SoftwareLicensingProduct<br />-SMS_SoftwareTag<br /><br /> <sup>1</sup> Varlık Yönetim Bilgileri donanım envanteri raporlama sınıfları **SMS_SystemConsoleUsage** ve **SMS_SystemConsoleUser** , varsayılan olarak etkindir.<br /><br /> **Varlık yönetim bilgileri** düğümüne tıkladığınızda **varlıklar ve uyumluluk** çalışma alanındaki Configuration Manager konsolundaki varlık yönetim bilgileri donanım envanteri raporlama sınıflarını düzenleyebilirsiniz. Daha fazla bilgi için [yapılandırma varlık yönetim bilgileri](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) konusunun [varlık yönetim bilgileri donanım envanteri raporlama sınıflarını etkinleştirme](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) bölümüne bakın.|  
|Raporlama hizmetleri noktası|Yazılım güncelleştirmeleri raporlarının görüntülenebilmesi için raporlama hizmetleri noktası site sistemi rolü yüklenmelidir. Raporlama hizmetleri noktası oluşturma hakkında daha fazla bilgi için bkz. [Configuration Manager'da Raporlamayı Yapılandırma](https://go.microsoft.com/fwlink/p/?LinkId=232661).|  
