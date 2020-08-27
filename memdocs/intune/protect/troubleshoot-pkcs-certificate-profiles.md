---
title: Microsoft Intune ile sertifika sağlamak için PKCS Sertifika profillerinin kullanımıyla ilgili sorunları giderin | Microsoft Docs
description: Intune ile kullanmak üzere sertifika istemek için cihazlara özel ve ortak anahtar çifti (PKCS) profillerinin kullanımını sorun giderin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: acc61df344cb4134a863d75fff517047e78d067d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914795"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Microsoft Intune 'de PKCS sertifika dağıtımı sorunlarını giderme

Bu makaledeki bilgiler, Microsoft Intune ' de özel ve ortak anahtar çifti (PKCS) sertifikaları dağıtmaya yönelik çeşitli yaygın sorunları çözmenize yardımcı olabilir. Sorun gidermeye başlamadan önce, [Intune Ile PKCS sertifikalarını yapılandırma ve kullanma](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca)konusunda bulunan aşağıdaki görevleri tamamladığınızdan emin olun:

- [PKCS sertifika profillerini kullanma gereksinimlerini](../protect/certficates-pfx-configure.md#requirements) gözden geçirme
- Kuruluş sertifika yetkilisinden (CA) kök sertifikayı dışarı aktarma
- Sertifika yetkilisinde sertifika şablonlarını yapılandırma
- Intune sertifika bağlayıcısını yükleyip yapılandırma
- Kök sertifikayı dağıtmak için güvenilen bir sertifika profili oluşturma ve dağıtma
- PKCS sertifika profili oluşturma ve dağıtma

PKCS sertifika profilleri için en yaygın sorun kaynakları, PKCS sertifika profili yapılandırması ile değiştirilmiştir. Profil yapılandırmasını gözden geçirin ve sunucu adlarında veya tam etki alanı adlarında (FQDN) yazım hatalarını arayın ve **sertifika yetkilisini** ve **sertifika yetkilisi adının** doğru olduğunu onaylayın.

- **Sertifika yetkilisi**: sertifika yetkilisi bilgisayarının iç FQDN 'si. Örneğin, sunucu1. domain. Local.
- **Sertifika yetkilisi adı**: SERTIFIKA yetkilisi MMC 'de gösterildiği gibi sertifika yetkilisi adı. **Sertifika yetkilisi (yerel)** bölümüne bakın

Sertifika yetkilisi ve sertifika yetkilisi adı için doğru adı doğrulamak üzere CA 'daki [Certutil komut satırı programını](/windows-server/administration/windows-commands/certutil) kullanabilirsiniz.

## <a name="pkcs-communication-overview"></a>PKCS iletişimine genel bakış

Aşağıdaki grafik, Intune 'daki PKCS sertifika dağıtım sürecine temel bir genel bakış sağlar.

> [!div class="mx-imgBorder"]
> ![PKCS sertifika profili akışı](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. Yönetici, Intune 'da bir PKCS sertifika profili oluşturur.
2. Intune hizmeti, şirket içi Intune sertifika bağlayıcısının Kullanıcı için yeni bir sertifika oluşturmasını ister.
3. Intune sertifika Bağlayıcısı, Microsoft sertifika yetkilinize bir PFX blobu ve Isteği gönderir.
4. Sertifika yetkilisi sorunları ve PFX Kullanıcı sertifikasını Intune sertifika bağlayıcısına geri gönderir.
5. Intune sertifika Bağlayıcısı, şifreli PFX Kullanıcı sertifikasını Intune 'a yükler.
6. Intune, PFX Kullanıcı sertifikasının şifresini çözer ve cihaz yönetim sertifikasını kullanarak cihaz için yeniden şifreler.  Intune daha sonra PFX Kullanıcı sertifikasını cihaza gönderir.
7. Cihaz, sertifika durumunu Intune olarak bildirir.

## <a name="data-and-log-files"></a>Veri ve günlük dosyaları

İletişim ve sertifika sağlama iş akışı sorunlarını belirlemek için, hem sunucu altyapısından hem de cihazlardan günlük dosyalarını gözden geçirin. Daha sonraki bölümlerde, PKCS Sertifika profillerinin giderilmesi için bu bölümde başvurulan günlük dosyalarına bakın.

- [Altyapı ve sunucu günlükleri](#logs-for-on-premises-infrastructure)

Cihaz günlükleri cihaz platformuna bağlıdır:

- [iOS ve ıpados](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Şirket içi altyapı günlükleri
  
Sertifika dağıtımları için PKCS Sertifika profillerinin kullanımını destekleyen şirket içi altyapı Microsoft Intune Sertifika Bağlayıcısı, bir Windows Server üzerinde çalışan NDES ve sertifika yetkilisini içerir.

Bu roller için günlük dosyaları, Windows Olay Görüntüleyicisi, sertifika konsollarının yanı sıra Intune sertifika Bağlayıcısı, NDES veya şirket içi altyapının parçası olan diğer rol ve işlemlere özgü çeşitli günlük dosyaları içerir.

- **NDESConnector_date_time. svclog**:

  Bu günlük Microsoft Intune Sertifika Bağlayıcısı ile Intune bulut hizmeti arasındaki iletişimi gösterir. Bu günlük dosyasını görüntülemek için [hizmet Izleme Görüntüleyicisi aracını](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) kullanabilirsiniz.

  İlgili kayıt defteri anahtarı: *Hklm\sw\microsoft\microsofıntune\ndesconnector\connectionstatus*

  Konum: NDES 'Yi barındıran sunucuda *% Program_Files% \ Microsoft ıntune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time. svclog**:

  Bu günlük, sertifika isteklerini alıp doğrulayan NDES ilke modülünü gösterir. Bu günlük dosyasını görüntülemek için [hizmet Izleme Görüntüleyicisi aracını](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) kullanabilirsiniz.

  Konum: NDES 'Yi barındıran sunucuda *% Program_Files% \ Microsoft ıntune\ndesconnectorsvc\logs\logs*

- **NDESPlugin. log**:

  Bu günlük, sertifika isteklerinin sertifika kayıt noktasına geçişini ve bu isteklerin sonuçtaki doğrulanmasını gösterir.

  Konum: NDES 'Yi barındıran sunucuda *% Program_Files% \ Microsoft Intune\NDESPolicyModule\logs*

- **Windows uygulama günlüğü**:

  Konum: NDES 'yi barındıran sunucuda: Windows Olay Görüntüleyicisi açmak için **eventvwr. msc** dosyasını çalıştırın

### <a name="logs-for-android-devices"></a>Android cihazları için Günlükler

Android çalıştıran cihazlar için **android Şirket portalı** app günlük dosyası **OMADM. log**dosyasını kullanın. Günlükleri toplamadan ve gözden geçirebilmeniz için, [ayrıntılı günlük kaydının](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) etkinleştirildiğinden emin olun ve ardından sorunu yeniden oluşturun.

Bir cihazdan OMADM. logs toplamak için bkz. [USB kablosu kullanarak karşıya yükleme ve e-posta günlükleri](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

Ayrıca, destek için [e-posta günlükleri de yükleyebilir](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) .

### <a name="logs-for-ios-and-ipados-devices"></a>İOS ve ıpados cihazları için Günlükler

İOS/ıpados çalıştıran cihazlarda, bir Mac bilgisayarda çalışan hata ayıklama günlükleri ve **Xcode** kullanın:

1. İOS/ıpados cihazını Mac 'e bağlayın ve ardından **uygulama**  >  **yardımcı programları** ' na giderek konsol uygulamasını açın.

2. **Eylem**altında, **bilgi Iletilerini Içer** ve **hata ayıklama iletilerini içer**' i seçin.

   ![Günlük seçeneklerini seçin](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Sorunu yeniden oluşturun ve sonra günlükleri bir metin dosyasına kaydedin:
   1. **Edit**  >  Geçerli ekrandaki tüm iletileri seçmek için Düzenle Seç**Tümünü** Seç ' i seçin ve ardından **Edit**  >  iletileri panoya kopyalamak için**kopyayı** Düzenle ' yi seçin.
   2. TextEdit uygulamasını açın, kopyalanmış günlükleri yeni bir metin dosyasına yapıştırın ve dosyayı kaydedin.

İOS ve ıpados cihazlarının Şirket Portalı günlüğü, PKCS sertifika profilleri hakkında bilgi içermez.

### <a name="logs-for-windows-devices"></a>Windows cihazları için Günlükler

Windows çalıştıran cihazlarda, Intune ile yönettiğiniz cihazların kayıt veya cihaz yönetimi sorunlarını tanılamak için Windows olay günlüklerini kullanın.

Cihazda **Olay Görüntüleyicisi**  >  **uygulamalar ve hizmet günlükleri**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostics-Provider** ' ı açın.

![Windows olay günlükleri](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>Virüsten koruma dışlamaları

NDES veya sertifika bağlayıcısını barındıran sunuculara virüsten koruma dışlamaları eklemeyi göz önünde bulundurun:

- Sertifika istekleri sunucuya veya Intune sertifika bağlayıcısına ulaşmıyor, ancak başarıyla işlenmedi 
- Sertifikalar yavaş verilir

Aşağıda, dışarıda bırakabilmeniz gereken konumların örnekleri verilmiştir:

- *% Program_Files%* \Microsoft ıntune\pfxisteği
- *% Program_Files%* \Microsoft ıntune\certificaterequeststatus
- *% Program_Files%* \Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>Sık karşılaşılan hatalar

Aşağıdaki yaygın hatalar aşağıdaki bölümde verilmiştir:

- [RPC sunucusu kullanılamıyor 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [Kayıt ilkesi sunucusu, 0x80094015 konumunda bulunamıyor](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [Gönderim Beklemede](#the-submission-is-pending)
- [Parametre yanlış 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [Ilke modülü tarafından reddedildi](#denied-by-policy-module)
- [Sertifika profili beklemede olarak takıldı](#certificate-profile-stuck-as-pending)
- [Hata-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>RPC sunucusu kullanılamıyor 0x800706ba

PFX dağıtımı sırasında, güvenilen kök sertifika cihazda görünür, ancak PFX sertifikası cihazda görünmez. NDESConnector günlük dosyası, aşağıdaki örnekte görüldüğü gibi, **RPC sunucusu kullanılamıyor. 0x800706ba olan**dizeyi içerir:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Nedeni 1-Intune 'da yanlış CA yapılandırması

Bu sorun, PKCS sertifika profili yanlış sunucuyu belirttiğinde veya CA 'nın adı veya FQDN 'SI için yazım hataları içerdiğinde ortaya çıkabilir. CA, profilin aşağıdaki özelliklerinde belirtilir:

- Certification authveyaity
- Sertifika yetkilisi adı

**Çözüm**:

Aşağıdaki ayarları gözden geçirin ve yanlış olursa çözüm yapın:

- **Sertifika yetkilisi** ÖZELLIĞI, CA SUNUCUNUZUN iç FQDN 'sini görüntüler.
- **Sertifika yetkilisi adı** özelliği, CA 'nızın adını görüntüler.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Neden 2-CA, önceki CA sertifikaları tarafından imzalanan istekler için sertifika yenilemeyi desteklemez

CA FQDN 'SI ve adı PKCS sertifika profilinde doğruysa, sertifika yetkilisi sunucusundaki Windows uygulama günlüğünü gözden geçirin. Aşağıdaki örneğe benzer bir **olay kimliği 128** arayın:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

CA sertifikası yenilendiğinde, çevrimiçi sertifika durumu Protokolü (OCSP) yanıt Imzalama sertifikasını imzalayamalıdır. İmzalama, OCSP Yanıt Imzalama sertifikasının, iptal durumlarını denetleyerek diğer sertifikaları doğrulamasına olanak sağlar. Bu imzalama varsayılan olarak etkin değildir.

**Çözüm**:

Sertifikayı imzalamayı el ile zorla:

1. CA sunucusunda, yükseltilmiş bir komut Istemi açın ve şu komutu çalıştırın: **certutil-setreg Ca\usedefinedcacerınrequest 1**
2. Sertifika Hizmetleri hizmetini yeniden başlatın.

Sertifika Hizmetleri hizmeti yeniden başlatıldıktan sonra cihazlar sertifikaları alabilir.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>Kayıt ilkesi sunucusu, 0x80094015 konumunda bulunamıyor

Aşağıdaki örnekte görüldüğü gibi **bir kayıt ilkesi sunucusu** bulunamıyor ve **0x80094015**olamaz:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Neden-sertifika kayıt ilkesi sunucu adı

Bu sorun, Intune NDES bağlayıcısını barındıran bilgisayar bir sertifika kayıt ilkesi sunucusunu bulamıyorsa oluşur.

**Çözüm**:

NDES bağlayıcısını barındıran bilgisayardaki sertifika kayıt ilkesi sunucusunun adını el ile yapılandırın. Adı yapılandırmak için [Add-Certificatekayıtlarını Mentpolicyserver](/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps) PowerShell cmdlet 'ini kullanın.

### <a name="the-submission-is-pending"></a>Gönderim Beklemede

Mobil cihazlara bir PKCS sertifika profili dağıttıktan sonra, sertifikalar alınmadı ve NDESConnector günlüğü, aşağıdaki örnekte görüldüğü gibi **gönderimin beklediği**dizeyi içerir:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

Ayrıca, sertifika yetkilisi sunucusunda, **bekleyen istekler** klasöründe PFX isteğini görebilirsiniz:

> [!div class="mx-imgBorder"]
> ![Sertifika yetkilisi bekleyen istekler klasörünün ekran görüntüsü](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Neden-Istek Işleme için yanlış yapılandırma

Bu sorun, **istek durumunu Beklemede olarak ayarlarsanız oluşur. Yöneticinin** sertifika yetkilisi **özellikleri**  >  **ilke modülü**  >  **özellikleri** iletişim kutusunda sertifikayı açıkça vermesi gerekir.

> [!div class="mx-imgBorder"]
> ![Ilke modülü özelliklerinin ekran görüntüsü](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Çözüm**:

Ayarlanacak Ilke modülü özelliklerini düzenleyin: varsa **, Sertifika şablonundaki ayarları izleyin. Aksi takdirde, sertifikayı otomatik olarak verin.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>Parametre yanlış 0x80070057

Intune sertifika Bağlayıcısı başarıyla yüklenip yapılandırıldığında, cihazlar PKCS sertifikaları almaz ve NDESConnector günlüğü, aşağıdaki örnekte görüldüğü gibi **parametrenin yanlış. 0x80070057 olduğunu**içeren dizeyi içerir:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Neden-PKCS profili yapılandırması

Bu sorun, Intune 'daki PKCS profili yanlış yapılandırılursa oluşur. Aşağıdakiler yaygın yapılandırma hataları verilmiştir:

- Profil, CA için yanlış bir ad içeriyor.
- Konu alternatif adı (SAN) e-posta adresi için yapılandırılmıştır, ancak hedeflenen kullanıcının henüz geçerli bir e-posta adresi yok. Bu birleşim, geçersiz SAN için null değer değeriyle sonuçlanır.

**Çözüm**:

PKCS profili için aşağıdaki konfigürasyonları doğrulayın ve sonra ilkenin cihazda yenilenmesini bekleyin:

- CA adıyla yapılandırılır
- Doğru kullanıcı grubuna atandı
- Gruptaki kullanıcıların geçerli e-posta adresleri var

Daha fazla bilgi için bkz. [Intune Ile PKCS sertifikalarını yapılandırma ve kullanma](../protect/certficates-pfx-configure.md).

### <a name="denied-by-policy-module"></a>Ilke modülü tarafından reddedildi

Cihazlar güvenilen kök sertifikayı alırken ancak PFX sertifikasını almadığınızda ve NDESConnector günlüğü, aşağıdaki örnekte görüldüğü gibi, **gönderim başarısız oldu: Ilke modülü tarafından reddedildi**:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Neden – sertifika şablonu için bilgisayar hesabı izinleri

Bu sorun, Intune sertifika bağlayıcısını barındıran sunucunun bilgisayar hesabının sertifika şablonu için izinleri olmadığında oluşur.

**Çözüm**:

1. Yönetici ayrıcalıklarına sahip bir hesapla Kurumsal CA’nızda oturum açın.
2. **Sertifika yetkilisi** konsolunu açın, sertifika şablonları ' na sağ tıklayın **ve Yönet**' i seçin.
3. Sertifika şablonunu bulun ve şablonun **Özellikler** iletişim kutusunu açın.
4. **Güvenlik** sekmesini seçin ve Microsoft Intune sertifika Bağlayıcısı yüklediğiniz sunucunun bilgisayar hesabını ekleyin. Bu hesaba **okuma** ve **kaydetme** izinleri verin.
5. **Apply**  >  Sertifika şablonunu kaydetmek için**Tamam** ' ı seçin ve ardından **sertifika şablonları** konsolunu kapatın.
6. **Sertifika Yetkilisi** konsolunda **Sertifika Şablonları** > **Yeni** > **Yayımlanacak Sertifika Şablonu**’na sağ tıklayın.
7. Değiştirdiğiniz şablonu seçin ve ardından **Tamam**' a tıklayın.

Daha fazla bilgi için bkz. [CA 'da sertifika şablonlarını yapılandırma](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca).

### <a name="certificate-profile-stuck-as-pending"></a>Sertifika profili beklemede olarak takıldı

Microsoft Endpoint Manager Yönetim merkezinde, PKCS sertifika profilleri **bekleyen**durumuyla birlikte dağıtılamaz. NDESConnector günlük dosyasında belirgin bir hata yoktur.
Bu sorunun nedeni günlüklerde açık bir şekilde tanımlanmamışsa, aşağıdaki nedenlerden dolayı çalışın.

#### <a name="cause-1---unprocessed-request-files"></a>Neden 1-Işlenmemiş istek dosyaları

İstek dosyalarını, neden işlenemediğini belirten hatalar için gözden geçirin.

1. NDES bağlayıcısını barındıran bilgisayarda, **%ProgramFiles%\Microsoft ıntune\pfxisteğine**gitmek Için dosya Gezgini 'ni kullanın.
2. En sevdiğiniz metin düzenleyiciyi kullanarak **başarısız** ve **işleme** klasörlerindeki dosyaları gözden geçirin.

   > [!div class="mx-imgBorder"]
   > ![Pfxistek klasörünü gözden geçirin](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. Bu dosyalarda, hataları belirten veya sorun öneren girişleri arayın. Web tabanlı arama kullanarak, isteğin neden başarısız olduğuna ve bu sorunların çözümlerine ilişkin ipuçları için hata iletilerini arayın.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Neden 2-PKCS sertifika profili için yanlış yapılandırma

**Başarısız**, **işleme**veya **başarılı** klasörlerinde istek dosyalarını BULAMADıĞıNıZDA, nedeni yanlış sertifikanın PKCS sertifika profiliyle ilişkilendirilmiş olması olabilir. Örneğin, bir alt CA, profille ilişkilendirilir veya yanlış kök sertifikası kullanılır.

**Çözüm**:

1. Kuruluş CA 'nızdan cihazlara olan kök sertifikayı cihazlara dağıttığınızdan emin olmak için güvenilen sertifika profilinizi gözden geçirin.
2. Doğru CA, sertifika türü ve kök sertifikayı cihazlara dağıtan güvenilir sertifika profiline başvurduğundan emin olmak için PKCS sertifika profilinizi gözden geçirin.

Daha fazla bilgi için bkz. Microsoft Intune [kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md) .

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Hata-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

PKCS sertifikaları dağıtılamaz ve veren CA 'daki sertifika konsolu, aşağıdaki örnekte görüldüğü gibi **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED**dizesiyle bir ileti görüntüler:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Neden-"istekte sağlama" miscongifured

Bu sorun, sertifika şablonu **özellikleri** Iletişim kutusundaki **Konu adı** sekmesinde **istek seçeneğinde sağlama** etkinleştirilmemişse oluşur.

> [!div class="mx-imgBorder"]
> ![NDES özelliklerini yapılandırma](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Çözüm**:

Yapılandırma sorununu çözmek için şablonu düzenleyin:

1. Yönetici ayrıcalıklarına sahip bir hesapla Kurumsal CA’nızda oturum açın.
2. **Sertifika Yetkilisi** konsolunu açın, **Sertifika Şablonları**'na sağ tıklayın ve **Yönet**'i seçin.
3. Sertifika şablonunun Özellikler iletişim kutusunu açın.
4. **Konu Adı** sekmesinde, **İstekte sağla**'yı seçin.
5. Sertifika şablonunu kaydetmek için **Tamam** ' ı seçin ve ardından **sertifika şablonları** konsolunu kapatın.
6. **Sertifika yetkilisi** konsolunda Şablonlar ' a sağ tıklayıp verilecek **Şablonlar**  >  **Yeni**  >  **sertifika şablonu**' na tıklayın.
7. Değiştirdiğiniz şablonu seçin ve ardından **Tamam**' ı seçin.

## <a name="next-steps"></a>Sonraki adımlar

Hala bir çözüme ihtiyacınız varsa veya Intune hakkında daha fazla bilgi arıyorsanız [Microsoft Intune forumumuza](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)bir soru gönderin. Birçok destek mühendisi, MVP ve geliştirme ekibimizin üyeleri sık sık forumlardır. bu nedenle, birisinin yardımcı olması iyi bir şansınız olabilir.

Microsoft Intune ürün destek ekibiyle bir destek talebi açmak için bkz. [Microsoft Intune için destek alma](../fundamentals/get-support.md).
PKCS sertifika dağıtımı hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Intune ile PKCS sertifikalarını yapılandırma ve kullanma](../protect/certficates-pfx-configure.md)
- [Microsoft Intune'daki cihazlarınız için sertifika profili yapılandırma](../protect/certificates-configure.md)
- [Microsoft Intune’da SCEP ve PKCS sertifikalarını kaldırma](../protect/remove-certificates.md)