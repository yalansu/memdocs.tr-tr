---
title: Sunucu olay günlükleri
titleSuffix: Configuration Manager
description: Windows olay günlüğündeki olası BitLocker (MBAD) sunucu girdileri için teknik başvuru
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe7d24bc1cad27094d720a5cb5aa487caec9199d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127874"
---
# <a name="server-event-logs"></a>Sunucu olay günlükleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

Configuration Manager ' de aşağıdaki BitLocker yönetim sunucusu bileşenlerine yönelik olay günlüklerini görüntülemek için Windows Olay Görüntüleyicisi kullanın:

- Yönetim noktasındaki kurtarma hizmeti
- Self servis portalı
- Yönetim ve web sitesini izleme

Bu bileşenlerden bir veya daha fazlasını barındıran bir sunucuda, Olay Görüntüleyicisi açın. Ardından **uygulamalar ve hizmetler günlükleri**' ne gidin, **Microsoft**, **Windows**ve **mbaı-Web**' i genişletin. Varsayılan olarak, [yönetici](#admin) ve [işletimsel](#operational) olay günlükleri vardır.

Aşağıdaki bölümlerde, BitLocker yönetim sunucusu bileşenlerinde oluşabilen olay kimliklerine yönelik mesajlar ve sorun giderme bilgileri yer alabilir.

## <a name="admin"></a>Yönetici

### <a name="1-webappspnerror"></a>1: WebAppSpnError

Uygulama: {SiteName} {VirtualDirectory}, şu hizmet sorumlusu adlarını (SPN) içermiyor: {Lıfspn} hesapta gerekli SPN 'Leri kaydedin: {ExecutionAccount}.

Tümleşik Windows kimlik doğrulamasının başarılı olması için gerekli SPN 'Lerin yerinde olması gerekir. Bu ileti, uygulama için gereken SPN 'nin doğru şekilde yapılandırılmadığını gösterir. Bu olayın içerdiği ayrıntılar daha fazla bilgi sağlamalıdır.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Olası hata iletileri:

- GetMachineUsers: veritabanından Kullanıcı bilgileri alınırken bir hata oluştu.
- GetRecoveryKey: kurtarma anahtarı veritabanından alınırken bir hata oluştu.
- GetRecoveryKey: veritabanından Kullanıcı bilgileri alınırken bir hata oluştu.
- Getrecoverykeyıds: veritabanından kurtarma anahtarı kimlikleri alınırken bir hata oluştu.
- GetTpmHashForUser: kurtarma veritabanından TPM karma verileri alınırken bir hata oluştu.
- GetTpmHashForUser: kurtarma veritabanından TPM karma verileri alınırken bir hata oluştu.
- QueryDriveRecoveryData: sürücü kurtarma verileri veritabanından alınırken bir hata oluştu.
- Queryrecoverykeyıdsforuser: veritabanından kurtarma anahtarı kimlikleri alınırken bir hata oluştu.
- QueryVolumeUsers: veritabanından Kullanıcı bilgileri alınırken bir hata oluştu.

Bu ileti, kurtarma veritabanıyla iletişim kurulurken bir özel durum olduğunda günlüğe kaydedilir. Özel durumla ilgili belirli ayrıntıları almak için izlemede yer alan bilgileri okuyun.

### <a name="101-adminservicecompliancedberror"></a>101: Adminservicekarmaşıkancedberror

Olası hata iletileri:

- GetRecoveryKey: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.
- Getrecoverykeyıds: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.
- GetTpmHashForUser: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.
- Queryrecoverykeyıdsforuser: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.
- QueryDriveRecoveryData: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.

Bu ileti, uyumluluk veritabanıyla iletişim kurulurken bir özel durum olduğunda günlüğe kaydedilir. Özel durumla ilgili belirli ayrıntıları almak için izlemede yer alan bilgileri okuyun.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Bu ileti, hizmet kurtarma veritabanıyla iletişim kurmaya çalıştığında bir özel durum gösterir. Özel durum hakkında özel bilgi almak için olayda bulunan iletiyi okuyun.

MBAE uygulama havuzu hesabının, kurtarma veritabanına bağlanmak için gerekli izinlere sahip olduğunu doğrulayın.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Olası hata iletileri:

- İstemci makine hesabı veya veri geçişi Kullanıcı hesabı algılanamıyor.

    ,, `PostKeyRecoveryInfo` Veya Web yöntemlerine her çağrı yapıldığında `IsRecoveryKeyResetRequired` , `CommitRecoveryKeyRest` `GetTpmHash` çağıran kimlik bilgilerini almak için çağıran bağlamını alır. Çağıran bağlamı null veya boş ise, hizmet bu iletiyi günlüğe kaydeder.

- Arayan kimliği için hesap doğrulaması başarısız oldu.

    Bu ileti, Web yöntemi çağıranın bilgisayar hesabı olmasını bekliyorsanız günlüğe kaydedilir ve bu ileti değildir. Ayrıca, Web yönteminin bir kullanıcı hesabı olmasını beklediği ve bir kullanıcı hesabı ya da bir veri geçiş grubu hesabının üyesi olmaması da buna neden olabilir.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: Statusservicekarmaşıkancedbconfigerror

Kayıt defterindeki uyumluluk veritabanı bağlantı dizesi boş.

Uyumluluk veritabanı bağlantı dizesi geçersiz olduğunda bu ileti günlüğe kaydedilir. Kayıt defteri anahtarındaki değeri doğrulayın `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` .

### <a name="105-statusservicecompliancedberror"></a>105: Statusservicekarmaşıkancedberror

Bu hata, Web sitelerinin veya Web hizmetlerinin uyumluluk veritabanına bağlanamadığını gösterir. IIS uygulama havuzu hesabının veritabanına bağlanıp bağlanamadiğini doğrulayın.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Bilinen hatalar ve olası nedenler:

- URL isteği bir iç hataya neden oldu.

    Yönetim ve izleme Web sitesi (Yardım Masası) için uygulamada işlenmeyen bir özel durum oluştu. Belirli özel durumu bulmak için **yönetici** olay günlüğündeki günlük girişlerini gözden geçirin.

- Yürütme bağlamı bilgileri alınırken bir hata oluştu. Hizmet asıl adı (SPN) kaydı doğrulanamadı.

    İlk yardım masası Web sitesi yükleme işlemi sırasında SPN 'YI denetler. SPN 'yi doğrulamak için, yardım masası Web sitesine karşılık gelen hesap bilgileri, IIS SiteName ve ApplicationVirtualPath gerekir. Bu özniteliklerin bir veya daha fazlası geçersiz veya eksik olduğunda bu hata iletisini günlüğe kaydeder.

- Hizmet asıl adı (SPN) kaydı doğrulanırken bir hata oluştu.

    Bu ileti, SPN doğrulanırken bir güvenlik özel durumunun bulunduğunu gösterir. Olay ayrıntılarında yer alan özel duruma bakın.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Bilinen hatalar ve olası nedenler:

- Bir kullanıcı için kurtarma anahtarı alınırken bir hata oluştu

    Kurtarma anahtarı alma isteği yapıldığında beklenmeyen bir özel durumun oluşturulduğunu gösterir. Olay ayrıntılarında özel durum iletisine bakın. Yardım Masası uygulamasında izleme etkinse, ayrıntılı özel durum iletileri almak için izleme verileri ' ne bakın.

- Yürütme bağlamı bilgileri alınırken bir hata oluştu. Hizmet asıl adı (SPN) kaydı doğrulanamadı

    İlk yükleme işlemi sırasında Self Servis portalı, SPN 'yi doğrulamak üzere Self Servis Web sitesi için hesap bilgilerini, IIS SiteName 'sini ve ApplicationVirtualPath 'yi alır. Bu bir veya daha fazla öznitelik geçersiz olduğunda bu hata iletisi günlüğe kaydedilir.

- Hizmet asıl adı (SPN) kaydı doğrulanırken bir hata oluştu. EventDetails: {ExceptionMessage}

    Bu ileti SPN doğrulanırken bir güvenlik özel durumunun oluşturulduğunu gösterir. Olay ayrıntılarında yer alan özel duruma bakın.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Bilinen hatalar ve olası nedenler:

- {DomainName} etki alanı adı çözümlenirken bir hata oluştu, bir bellek ayırma hatası oluştu.

    Etki alanı adını çözümlemek için `DsGetDcName` WINDOWS API 'sini çağırır. Bu ileti `ERROR_NOT_ENOUGH_MEMORY` , bir bellek ayırma hatası olduğunu belirten bu API döndürüldüğünde günlüğe kaydedilir.

- DsGetDcName yöntemi çağrılamadı

    Bu ileti, API 'nin `DsGetDcName` konakta kullanılamadığını belirtir.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Bilinen hatalar ve olası nedenler:

- Kurtarma veritabanının yapılandırması okunurken bir hata oluştu. Kurtarma veritabanına yönelik bağlantı dizesi yapılandırılmadı.

    Bu ileti, konumundaki kurtarma veritabanı bağlantı dizesi bilgilerinin geçersiz olduğunu gösterir `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` . Verilen kayıt defteri anahtarı değerini doğrulayın.

Aşağıdaki iletilerden herhangi birini görürseniz, IIS sunucusundan uygulama havuzu kimlik bilgilerinin kurtarma veritabanıyla bağlantı yapıp yapamadığını doğrulayın:

- Yok Userhavematchingrecoverykey: bir kullanıcının kurtarma anahtarı kimlikleri alınırken bir hata oluştu.
- QueryDriveRecoveryData: sürücü kurtarma verileri alınırken bir hata oluştu.
- Queryrecoverykeyıdsforuser: bir kullanıcının kurtarma anahtarı kimlikleri alınırken bir hata oluştu.
- Kurtarma veritabanından TPM Parola karması alınırken bir hata oluştu.

### <a name="110-webappcompliancedberror"></a>110: Webappkarmaşıancedberror

Bilinen hatalar ve olası nedenler:

- Uyumluluk veritabanının yapılandırması okunurken bir hata oluştu. Uyumluluk veritabanına yönelik bağlantı dizesi yapılandırılmadı.

    Bu ileti, konumundaki uyumluluk veritabanı bağlantı dizesi bilgilerinin geçersiz olduğunu gösterir `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` . Bu kayıt defteri anahtarının değerini doğrulayın.

Aşağıdaki iletilerden herhangi birini görürseniz, IIS sunucusundan uygulama havuzu kimlik bilgilerinin uyumluluk veritabanıyla bağlantı yapıp yapamadığını doğrulayın:

- GetRecoveryKeyForCurrentUser: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.
- Queryrecoverykeyıdsforuser: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.
- Queryrecoverykeyıdsforuser: bir denetim olayı uyumluluk veritabanına yazılırken bir hata oluştu.

### <a name="111-webappdberror"></a>111: WebAppDbError

Bu hatalar aşağıdaki iki koşuldan birini gösterir

- MBAE Web siteleri/WebServices, uyumluluk veya kurtarma veritabanına bağlanamadı
- MBAMWEB siteleri/WebServices yürütme hesabı (uygulama havuzu hesabı), `GetVersion` Uyumluluk veya kurtarma veritabanında saklı yordamı çalıştıramıyor

Olayda bulunan ileti, özel durum hakkında daha fazla ayrıntı sağlar.

Uygulama havuzu hesabının uyumluluk veya kurtarma veritabanlarına bağlanabildiğini doğrulayın. Saklı yordamı çalıştırma izinleri olduğunu doğrulayın `GetVersion` .

### <a name="112-webapperror"></a>112: WebAppError

Hizmet asıl adı (SPN) kaydı doğrulanırken bir hata oluştu.

SPN 'yi doğrulamak için, SPN eşlenmiş yürütme hesabı listesini almak üzere Active Directory sorgular. Ayrıca, `ApplicationHost.config` Web sitesi bağlamalarını almak için ' i sorgular. Bu hata iletisi, Active Directory ile iletişim kuramadığını veya dosyayı yükleyemediğini belirtir `ApplicationHost.config` .

Uygulama havuzu hesabının Active Directory veya dosyayı sorgulama izinleri olduğunu doğrulayın `ApplicationHost.config` . Ayrıca, dosyadaki site bağlama girdilerini de doğrulayın `ApplicationHost.config` .

## <a name="operational"></a>Operasyonel

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Performans sayacı alınırken bir hata oluştu.

Trace iletisi, bazıları burada listelenen gerçek özel durum iletisini içerir:

- ArgumentNullException: Kategori, sayaç veya istenen performans sayacı örneği geçersiz ise bu özel durum oluşturulur.
- System. InvalidOperationException: categoryName boş bir dizedir (""). counterName Boş bir dizedir ("").
- İstenen okuma/yazma izni ayarı bu sayaç için geçersiz.
- Belirtilen kategori yok (readOnly true ise).
- Belirtilen kategori .NET Framework özel bir kategori değil (readOnly false ise).
- Belirtilen kategori çok örnekli olarak işaretlenmiş ve bir örnek adı ile performans sayacının oluşturulmasını gerektiriyor.
- InstanceName 127 karakterden daha uzun.
- categoryName ve counterName farklı dillere yerelleştirildi.
- System. ComponentModel. Win32Exception: bir sistem API 'sine erişirken hata oluştu.
- System. UnauthorizedAccessException: yönetim ayrıcalıkları olmadan yürütülen kod, bir performans sayacını okumaya çalıştı.

Olaydaki ileti, özel durum hakkında daha fazla ayrıntı sağlar.

İçin, `System.UnauthorizedAccessException` uygulama havuzu hesabının performans sayacı API 'lerine erişimi olduğunu doğrulayın.

### <a name="200-helpdeskinformation"></a>200: Helpdeskınformation

Yönetim Web sitesi uygulaması başarıyla bulundu ve kurtarma/uyumluluk veritabanının desteklenen bir sürümüne bağlandı.

Yardım Masası web sitesinden kurtarma veya uyumluluk veritabanına başarıyla bağlantı olduğunu gösterir.

### <a name="201-selfserviceportalinformation"></a>201: Selfserviceportalınformation

Self Servis Portalı uygulaması başarıyla bulundu ve kurtarma/uyumluluk veritabanının desteklenen bir sürümüne bağlandı.

Self Servis portalından kurtarmaya veya uyumluluk veritabanına başarılı bir bağlantı olduğunu gösterir.

### <a name="202-webappinformation"></a>202: Webappınformation

Uygulamanın SPN 'Leri doğru şekilde kaydedildi.

Yardım Masası web sitesi için gereken SPN 'Lerin yürütülen hesapta doğru şekilde kaydedildiğini belirtir.

## <a name="see-also"></a>Ayrıca bkz.

Bu günlükleri kullanma hakkında daha fazla bilgi için bkz. [BitLocker olay günlükleri](about-event-logs.md).

Daha fazla sorun giderme bilgisi için bkz. [BitLocker sorunlarını giderme](troubleshoot.md).

Bu Web sitelerini yükleme hakkında daha fazla bilgi için bkz. [BitLocker raporları ve portalları ayarlama](../../deploy-use/bitlocker/setup-websites.md).
