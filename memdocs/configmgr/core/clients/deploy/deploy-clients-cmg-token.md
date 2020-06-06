---
title: CMG için belirteç tabanlı kimlik doğrulaması
titleSuffix: Configuration Manager
description: Bir istemciyi, benzersiz bir belirteç için iç ağa kaydedin veya internet tabanlı cihazlar için bir toplu kayıt belirteci oluşturun.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5054d44371fd3114a9644f90d37dabf1e81d1997
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455030"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi için belirteç tabanlı kimlik doğrulaması

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--5686290-->

Bulut yönetimi ağ geçidi (CMG) birçok tür istemciyi destekler, ancak [GELIŞMIŞ http](../../plan-design/hierarchy/enhanced-http.md)ile birlikte bu istemciler [istemci kimlik doğrulama sertifikası](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway)gerektirir. Bu sertifika gereksinimi, genellikle dahili ağa bağlanmayan, Azure Active Directory (Azure AD) kalamamayan ve PKI tarafından verilen bir sertifika yüklemek için bir yönteme sahip olmayan Internet tabanlı istemcilere sağlanması zor olabilir.

Sürüm 2002 ' den başlayarak bu zorlukları aşmak için Configuration Manager cihaz desteğini aşağıdaki yöntemlerle genişletir:

- Benzersiz bir belirteç için iç ağa kaydolun

- Internet tabanlı cihazlar için toplu kayıt belirteci oluşturma

Bu özellikten tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Tüm senaryo, istemci sürümü de en son olana kadar işlevsel değildir. Gerekirse, [yeni istemci sürümünü üretime yükseltemediğinizden](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)emin olun.

Yönetim noktasıyla birlikte Configuration Manager istemcisi bu belirteci yönetir, bu nedenle işletim sistemi sürümü bağımlılığı yoktur. Bu özellik [desteklenen tüm istemci işletim sistemi sürümleri](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)için kullanılabilir.

> [!NOTE]
> Bu yöntemler yalnızca cihaz merkezli yönetim senaryolarını destekler.
>
> Microsoft, cihazların Azure AD 'ye katılmasını öneriyor. Internet tabanlı cihazlar Configuration Manager kimlik doğrulaması yapmak için Azure AD kullanabilir. Ayrıca, cihazın İnternet üzerinde veya iç ağa bağlı olup olmadığı hem cihaz hem de Kullanıcı senaryolarına olanak sağlar. Daha fazla bilgi için bkz. [Azure AD kimlik kullanarak Istemciyi yükleyip kaydetme](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>İç ağda kaydolun

Bu yöntem, istemcisinin ilk olarak iç ağdaki yönetim noktasına kaydolmanızı gerektirir. İstemci kaydı genellikle yüklemeden hemen sonra gerçekleşir. Yönetim noktası istemciye, kendinden imzalı bir sertifika kullandığını gösteren benzersiz bir belirteç verir. İstemci internet 'e dolaştığı zaman CMG ile iletişim kurmak için, otomatik olarak imzalanan sertifikayı yönetim noktası tarafından verilen belirteç ile çifttir. İstemci belirteci ayda bir kez yeniler ve 90 gün geçerlidir.

Site bu davranışı varsayılan olarak sunar.

## <a name="create-a-bulk-registration-token"></a>Toplu kayıt belirteci oluşturma

İç ağa istemci yükleyip kaydedemiyorum, toplu kayıt belirteci oluşturun. İstemci Internet tabanlı bir cihaza yüklediğinde ve CMG aracılığıyla kaydolduğunda bu belirteci kullanın. Toplu kayıt belirtecinin kısa geçerlilik süresi vardır ve istemci ya da sitede depolanmaz. İstemcinin otomatik olarak imzalanan sertifikayla eşleştirilmiş benzersiz bir belirteç oluşturmasını sağlar ve CMG ile kimlik doğrulamasını sağlar.

1. Hiyerarşideki en üst düzey site sunucusunda yerel yönetici ayrıcalıklarıyla oturum açın.

1. Yönetici olarak bir komut istemi açın.

1. Aracı, `\bin\X64` site sunucusundaki Configuration Manager yükleme dizininin klasöründen çalıştırın: `BulkRegistrationTokenTool.exe` . Parametresiyle yeni bir belirteç oluşturun `/new` . Örneğin, `BulkRegistrationTokenTool.exe /new`. Daha fazla bilgi için bkz. [toplu kayıt belirteci aracı kullanımı](#bulk-registration-token-tool-usage).

1. Belirteci kopyalayın ve güvenli bir konuma kaydedin.

1. Configuration Manager istemcisini Internet tabanlı bir cihaza yükler. İstemci yükleme parametresini ekleyin: [**/regtoken**](about-client-installation-properties.md#regtoken). Aşağıdaki örnek komut satırı, gerekli diğer kurulum parametrelerini ve özelliklerini içerir:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Bu komut satırı hakkında daha fazla bilgi için bkz. [Azure AD kimlik kullanarak Istemciyi yükleyip kaydetme](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Bu işlem benzerdir, yalnızca Azure AD özelliklerini kullanmaz.

Doğrulamak için, benzer bir giriş için aşağıdaki günlük dosyasını gözden geçirin:<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

### <a name="known-issues"></a>Bilinen sorunlar

Pasif modda site sunucusu olan bir sitede toplu kayıt belirteci oluşturamazsınız.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Toplu kayıt belirteci aracı kullanımı

`BulkRegistrationTokenTool.exe`Araç, `\bin\X64` site sunucusundaki Configuration Manager yükleme dizininin klasöründedir. Site sunucusunda oturum açın ve yönetici olarak çalıştırın. Aşağıdaki komut satırı parametrelerini destekler:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Bu kullanım bilgilerini görüntüleyin.

Örnek: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/Yeni

Yeni bir toplu kayıt belirteci oluşturun.

Örnek: `BulkRegistrationTokenTool.exe /new`

Araç aşağıdaki bilgileri görüntüler:
  
- Sitenin verilen belirteçleri izlemek için kullandığı GUID
- Varsayılan olarak üç gün olan belirteç geçerlilik süresi.
- Toplu kayıt belirteci.

Belirteç istemcide veya sitede depolanmaz. Belirteci komut isteminden kopyalamaya ve güvenli bir yerde sakladığınızdan emin olun.

#### <a name="lifetime"></a>/Lifetime

`/new`Belirtecin belirteç geçerlilik süresini belirtmek için parametresiyle birlikte kullanın. Dakikalar içinde bir tamsayı değeri belirtin. Varsayılan değer 4.320 ' dir (üç gün). En büyük değer 10.080 ' dir (yedi gün).

Örnek: `BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>Toplu kayıt belirteci yönetimi

Daha önce oluşturulan toplu kayıt belirteçlerini ve bunların yaşam sürelerini Configuration Manager konsolunda görebilir ve gerekirse kullanımlarını engelleyebilirsiniz. Ancak, site veritabanı toplu kayıt belirteçlerini depolar.

### <a name="review-a-bulk-registration-token"></a>Toplu kayıt belirtecini gözden geçirme

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin.

2. **Güvenlik**' i genişletin ve **Sertifikalar** düğümünü seçin. Konsol, site ile ilgili tüm sertifikaları ve toplu kayıt belirteçlerini Ayrıntılar bölmesinde listeler.

3. Gözden geçirilecek toplu kayıt belirtecini seçin.

**Tür** sütununu filtreleyebilir veya sıralayabilirsiniz. GUID 'lerine göre belirli toplu kayıt belirteçlerini belirler. Toplu kayıt belirteci oluşturduğunuzda araç, GUID 'YI görüntüler.

### <a name="block-a-bulk-registration-token"></a>Toplu kayıt belirtecini engelle

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin.

2. **Güvenlik**' i genişletin, **Sertifikalar** düğümünü seçin ve engellenecek toplu kayıt belirtecini seçin.

3. Şerit çubuğunun **giriş** sekmesinde veya sağ tıklama bağlam menüsünde **Engelle**' yi seçin. Daha önce engellenen toplu kayıt belirteçlerini kaldırmak için **Engellemeyi kaldır** eylemini seçin.

## <a name="see-also"></a>Ayrıca bkz.

- [Bulut yönetimi ağ geçidi için planlama](../manage/cmg/plan-cloud-management-gateway.md)

- [Kimlik doğrulaması için Azure AD 'yi kullanarak Configuration Manager Windows 10 istemcileri yükleyip atama](deploy-clients-cmg-azure.md)
