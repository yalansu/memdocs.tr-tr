---
title: Exchange bağlayıcısını yükleme
titleSuffix: Configuration Manager
description: Mobil cihazları ActiveSync aracılığıyla yönetmek için Exchange bağlayıcısını Configuration Manager için yükleyip yapılandırın.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d854e4b70a59a364b8611947feea89d4678e7e6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721958"
---
# <a name="install-and-configure-the-exchange-connector"></a>Exchange bağlayıcısını yükleyip yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mobil cihazları yönetmek üzere bir Exchange Server bağlayıcısını yüklemek ve yapılandırmak için bu yordamı kullanın. Configuration Manager, bir Exchange kuruluşunda yalnızca bir bağlayıcıyı destekler.

Configuration Manager için Exchange Server bağlayıcısını yüklemeden önce, gerekli izinlere ve sürümlere sahip olduğunuzdan emin olun. Daha fazla bilgi için bkz. [Exchange Ile cihaz yönetimi ve Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Exchange bağlantı hesabı

Mobil cihazları yönetmek için Exchange İstemci Erişimi sunucusuna hangi hesabın bağlanacağına karar verin. Bu hesap, site sunucusunun bilgisayar hesabı veya Windows kullanıcı hesabı olabilir.

Ardından, aşağıdaki Exchange Server cmdlet 'lerini çalıştırmak için bir Exchange rol grubundaki bu hesabı yapılandırın:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Posta kutusu al**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Kullanıcı al**  

- **Set-ActiveSyncOrganizationSettings**  

Aşağıdaki Exchange Server yönetim rolleri Şu cmdlet 'leri içerir:

- Alıcı yönetimi
- Yalnızca görüntüleme Kuruluş Yönetimi
- Sunucu Yönetimi

Daha fazla bilgi için bkz. Exchange Server 2013 belgelerindeki [Yönetim rolü gruplarını anlama](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help) .

> [!TIP]  
> Exchange Server bağlayıcısını gereken cmdlet 'ler olmadan yüklemeyi veya kullanmayı denerseniz, site sunucusu bilgisayarındaki EasDisc. log dosyasında şu hatayı görürsünüz: `Invoking cmdlet <cmdlet> failed`.

## <a name="install-the-connector"></a>Bağlayıcıyı yükler

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Hiyerarşi Yapılandırması**' nı genişletin ve **Exchange Server bağlayıcıları**' nı seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **Exchange Server Ekle**' yi seçin.

1. Exchange Server ekleme Sihirbazı ' nın **genel** sayfasında, Exchange Server ortamlarından birini seçin:

    - **Şirket Içi Exchange Server**: her bir Active Directory sitesi için tek bir sunucu veya Istemci erişim sunucusu dizisi belirtin.

        Sunucu veya dizi çevrimdışıysa, Configuration Manager kullanılacak bir Istemci erişim sunucusu bulmayı dener. Başarısız olursa, Configuration Manager Istemci erişim sunucusuyla bağlantı kurmak için bir posta kutusu sunucusunu kullanmaya geri döner. Bağlantıyı yeniden denediğinde, site sunucusu bilgisayarındaki EasDisc. log dosyasında şu uyarıları günlüğe kaydeder: `Failed to open runspace for site <site_name>`.

    - **Barındırılan Exchange Server**: Exchange Online ortamınızın sunucu adresini belirtin.

    Ardından, Exchange Server bağlayıcısını çalıştırmak için birincil siteyi seçin.

1. **Hesap** sayfasında, Exchange Server 'a bağlanmak için hesabı belirtin. Daha fazla bilgi için [Exchange bağlantı hesabı](#exchange-connection-account)' na bakın.

1. **Bulma** sayfasında, cihazları bulmaya yönelik eşitleme zamanlamasını ve kurallarını yapılandırın.

1. **Ayarlar** sayfasında, aşağıdaki gruplardaki mobil cihaz ayarlarını yapılandırın:

    - **Genel**
    - **Parola**
    - **E-posta yönetimi**
    - **Güvenlik**
    - **Uygulama**

    Daha fazla bilgi için bkz. [Exchange Connector ayarları](manage-mobile-devices-with-exchange-activesync.md#policies).

    Ayrıca, [Şirket ıçı MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)Configuration Manager kullanarak mobil cihazları kaydederseniz, **dış mobil cihaz yönetimine izin ver**seçeneğini etkinleştirin. Bu ayar, bu mobil cihazların Configuration Manager kaydettikten sonra Exchange 'den e-posta almaya devam etmesine izin verir.

1. Sihirbazı tamamlayın.

## <a name="verify-and-monitor"></a>Doğrulama ve izleme

Durum iletileri ve günlük dosyaları ile Exchange Server bağlayıcısının yüklenmesini doğrulayın:

- Site Bileşen Yöneticisi Exchange Server bağlayıcısını başarıyla yüklediğini doğrulayın. **SMS_EXCHANGE_CONNECTOR** bileşeninden ILETI durumu kimliği **1015** ' i arayın.

    Belirtilen Istemci erişim sunucusu çevrimdışıysa, yükleme başarısız olabilir. Configuration Manager bağlayıcıyı başarıyla yükleyememe Configuration Manager, yüklemeyi her 60 dakikada bir yeniden dener. Yükleme başarılı olana veya Exchange Server bağlayıcısını kaldırana kadar yeniden denemeye devam eder.

- Site sunucusu bilgisayarında, şu girdi için **Sitecomp. log** ' u gözden geçirin: `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Sonra, başarılı yüklemeyi şu metinle günlüğe kaydeder: `STATMSG: ID=1015`.

Yüklemeyi tamamladıktan sonra, bağlayıcı tarafından bulunan ve yönetilen mobil cihazları izleyin. Mobil cihaz koleksiyonlarını görüntüleyin ve mobil cihazlar için raporları kullanın.

> [!NOTE]  
> Configuration Manager, bulduğu mobil cihazlar için adlar üretir. *Kullanıcı adı*_*cihaz türü*biçimini kullanır. Örneğin, **jdoe_WindowsPhone**. Bir kullanıcının aynı cihaz türünde birden çok mobil cihazı varsa, bu mobil cihazlar için konsolda ve raporlarda aynı adı görüntüler Configuration Manager.  

## <a name="see-also"></a>Ayrıca bkz.

- [Yapılandırma istemcileri ve site sistemleri tarafından kullanılan bağlantı noktaları](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Proxy sunucu desteği](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Mobil cihazlar için güvenlik önerileri](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Exchange Server Bağlayıcısı ile yönetilen mobil cihazlar için gizlilik bilgileri](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)
