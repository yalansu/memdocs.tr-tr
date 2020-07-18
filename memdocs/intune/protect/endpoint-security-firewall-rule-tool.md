---
title: Microsoft Intune-Azure için uç nokta güvenliği güvenlik duvarı kuralı geçiş aracı | Microsoft Docs
description: Microsoft Intune için uç nokta güvenliği güvenlik duvarı kuralı geçiş aracının nasıl kullanılacağını anlayın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464953"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Uç nokta güvenliği güvenlik duvarı kuralı geçiş aracına genel bakış

Birçok kuruluş, modern, bulut tabanlı yönetimin kullanımını sağlamak için güvenlik yapılandırmalarını Microsoft Uç Nokta Yöneticisi 'ne taşımayı arıyor.

Endpoint Manager 'daki uç nokta güvenliği, Windows güvenlik duvarı yapılandırması ve ayrıntılı güvenlik duvarı kural yönetimi hakkında zengin yönetim deneyimleri sunar.

Birçok kuruluşta, Windows güvenlik duvarı kurallarını yönetmek için Grup Ilkeleri zaten vardır. Modern yönetime geçiş, yüzlerce güvenlik duvarı kuralı oluşturmak için el ile oluşturulabilir.

Müşterilerin, güvenlik duvarı kuralı yapılandırmalarını Endpoint Manager 'daki uç nokta güvenlik ilkelerine taşımasını sağlamak için **uç nokta güvenliği güvenlik duvarı kuralı geçiş aracı** geliştirilmiştir.

Müşteriler, bir başvuru/önceden yapılandırılmış Windows 10 istemcisinde **Endpoint Security güvenlik duvarı kuralı geçiş aracı** 'nı çalıştırabilir ve uç nokta Yöneticisi 'nde otomatik olarak uç nokta güvenliği Güvenlik Duvarı kural ilkeleri oluşturabilir. Yöneticiler, oluşturulduktan sonra MDM ve ortak yönetilen istemcileri yapılandırmak için bu kuralları Azure AD gruplarına hedefleyebilir.

[Uç nokta güvenliği güvenlik duvarı kuralı geçiş aracını](https://aka.ms/EndpointSecurityFWRuleMigrationTool)indirin:<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Araç kullanımı

Araç bir başvuru makinesinde çalıştırılır ve geçerli Windows güvenlik duvarı kuralı yapılandırmasını geçirir. Aracı çalıştırmak cihazda bulunan tüm etkin güvenlik duvarı kurallarını dışarı aktarır ve toplanan kurallarla otomatik olarak yeni Intune ilkeleri oluşturur.

1. Yerel yönetici ayrıcalıklarıyla referans makinesinde oturum açın.
2. Dosyayı indirip sıkıştırmasını açın `Export-FirewallRules.zip` . <br>
   ZIP dosyası betik dosyasını içerir `Export-FirewallRules.ps1` . 
3. `Export-FirewallRules.ps1`Betiği makinede çalıştırın. <br>
   Betik, çalıştırmak için gereken tüm önkoşulları indirir. İstendiğinde, uygun Intune Yöneticisi kimlik bilgilerini sağlayın. Gerekli izinler hakkında daha fazla bilgi için bkz. [gerekli izinler](#required-permissions).
4. İstendiğinde bir ilke adı belirtin. <br>
   Bu ilke, **uç nokta güvenliği**güvenlik duvarı bölmesindeki [Microsoft Uç Nokta Yöneticisi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde görünür olacaktır  >  **Firewall** . 

    > [!IMPORTANT]
    > İlke adı, kiracı için benzersiz olmalıdır.

    150 ' den fazla güvenlik duvarı kuralı bulunursa, birden çok ilke oluşturulur.

    > [!NOTE]
    > Yalnızca etkin güvenlik duvarı kuralları varsayılan olarak geçirilir ve yalnızca GPO tarafından oluşturulan güvenlik duvarı kuralları varsayılan olarak geçirilir. Bu varsayılan değerleri değiştirmek için anahtarlar sağlanır. Daha fazla bilgi için bkz. [anahtarlar](#switches).
    >
    > Bulunan Güvenlik Duvarı kurallarının sayısına bağlı olarak, aracın çalışması biraz zaman alabilir.

5. İşlem tamamlandıktan sonra, araç otomatik olarak geçirilemeyen bir güvenlik duvarı kuralı sayısını çıktı. Daha fazla bilgi için bkz. [desteklenmeyen yapılandırma](#unsupported-configuration).

## <a name="switches"></a>Anahtarlar

Aracın varsayılan işlevini değiştirmek için aşağıdaki anahtarları (parametreler) kullanabilirsiniz.

- `IncludeLocalRules`-Bu anahtarı kullanmak, dışa aktarma sırasında yerel olarak oluşturulan/varsayılan Windows güvenlik duvarı kurallarını içerir. Bu anahtarın etkinleştirilmesi, dahil edilen birçok kurala yol açabilir. 
- `IncludedDisabledRules`-Bu anahtarı kullanmak, tüm etkin ve devre dışı Windows güvenlik duvarı kurallarını dışa aktarma içinde içerir. Bu anahtarın etkinleştirilmesi, dahil edilen birçok kurala yol açabilir.

## <a name="unsupported-configuration"></a>Desteklenmeyen yapılandırma

Windows 'da MDM desteğinin bulunmaması nedeniyle, aşağıdaki kayıt defteri tabanlı ayarlar desteklenmez. Bu ayarlar sık görülen bir durumdur, ancak bu ayarların gerekli olması için lütfen standart destek kanallarınız aracılığıyla bu ihtiyacı günlüğe kaydedin.

|     GPO alanı    |     Neden    |
|-|-|
|      TÜR-değer =/"Security =" IFSECURE-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-değer =/"Security2_9 =" IFSECURE2-9-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-değer =/"Security2 =" IFSECURE2-10-VAL     |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-DEĞER =/"IF =" IF-VAL    |     Arabirim tanımlayıcısı (LUID) yönetilemez değil    |
|      TÜR-değer =/"ertele =" ertele-VAL    |     grup ilkesi veya Windows MDM aracılığıyla sunulmayan gelen NAT çapraz geçişi    |
|      TÜR-DEĞER =/"LSM =" BOOL-VAL    |     Gevşek kaynak eşlenmiş grup ilkesi veya Windows MDM aracılığıyla gösterilmez    |
|      TÜR-değer =/"Platform =" PLATFORM-VAL    |     İşletim sistemi sürümü oluşturma grup ilkesi veya Windows MDM aracılığıyla gösterilmez    |
|      TÜR-değer =/"RMauth =" STR-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-değer =/"RUAuth =" STR-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-değer =/"AuthByPassOut =" BOOL-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-DEĞER =/"LOM =" BOOL-VAL    |     grup ilkesi veya Windows MDM aracılığıyla açığa çıkarılan yerel olarak eşlenmiş    |
|      TÜR-değer =/"Platform2 =" PLATFORM-OP-VAL    |     Yedekli ayar grup ilkesi veya Windows MDM aracılığıyla gösterilmez    |
|      TÜR-değer =/"PCross =" BOOL-VAL    |     grup ilkesi veya Windows MDM aracılığıyla kullanıma sunulmayan profille izin ver    |
|      TÜR-değer =/"Lukendi =" STR-VAL    |     Yerel Kullanıcı sahibi SID 'SI MDM 'de geçerli değil    |
|      TÜR-DEĞER =/"TTK =" TRUST-TUPLE-ANAHTAR SÖZCÜĞÜ-VAL    |     grup ilkesi veya Windows MDM aracılığıyla gösterilmeyen güven grubu anahtar sözcüğüyle trafiği Eşleştir    |
|      TÜR-DEĞER =/"TTK2_22 =" GÜVEN-DEMET-ANAHTAR SÖZCÜK-VAL2 & LT-22    |     grup ilkesi veya Windows MDM aracılığıyla gösterilmeyen güven grubu anahtar sözcüğüyle trafiği Eşleştir    |
|      TÜR-DEĞER =/"TTK2_27 =" GÜVEN-DEMET-ANAHTAR SÖZCÜK-VAL2 & LT-27    |     grup ilkesi veya Windows MDM aracılığıyla gösterilmeyen güven grubu anahtar sözcüğüyle trafiği Eşleştir    |
|      TÜR-DEĞER =/"TTK2_28 =" GÜVEN-DEMET-ANAHTAR SÖZCÜK-VAL2 & LT-28    |     grup ilkesi veya Windows MDM aracılığıyla gösterilmeyen güven grubu anahtar sözcüğüyle trafiği Eşleştir    |
|      TÜR-değer =/"NND =" STR-ENC-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |
|      TÜR-değer =/"SecurityRealmId =" STR-VAL    |     IPSec ile ilgili ayar Windows MDM tarafından desteklenmiyor    |

## <a name="unsupported-setting-values"></a>Desteklenmeyen ayar değerleri
Aşağıdaki ayar değerleri geçiş için desteklenmez:

**Bağlantı noktaları**
- `PlayToDiscovery`Yerel veya uzak bağlantı noktası aralığı olarak desteklenmez.

**Adres aralıkları**
- `LocalSubnet6`Yerel veya uzak adres aralığı olarak desteklenmez. 
- `LocalSubnet4`Yerel veya uzak adres aralığı olarak desteklenmez.
- `PlatToDevice`Yerel veya uzak adres aralığı olarak desteklenmez.

Araç çalıştırıldıktan sonra, başarılı bir şekilde geçirilmeyen kurallarla bir rapor oluşturulur. İçinde bulunan ' i görüntüleyerek bu kuralların herhangi birini görüntüleyebilirsiniz `RulesError.csv` `C:\<folder needed>` . 

## <a name="required-permissions"></a>Gerekli izinler
Endpoint Security Manager, Intune Hizmet Yöneticisi veya genel yönetici kullanıcıları Windows güvenlik duvarı kurallarını uç nokta güvenlik ilkelerine geçirebilir. Alternatif olarak, güvenlik temelleri izinlerinin **silme**, **okuma**, **atama**, **oluşturma**ve **güncelleştirme** onayları ile ayarlandığı durumlarda özel bir rol de kullanılabilir. Daha fazla bilgi için bkz. [Intune 'a yönetici Izinleri verme](../fundamentals/users-add.md#grant-admin-permissions).

## <a name="next-steps"></a>Sonraki adımlar

- MDM ve ortak yönetilen istemcileri yapılandırmak için kuralları Azure AD gruplarına atayın. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md).
