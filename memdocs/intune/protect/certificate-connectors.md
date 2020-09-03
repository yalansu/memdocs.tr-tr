---
title: Microsoft Intune-Azure için C sertifika bağlayıcıları | Microsoft Docs
description: Basit Sertifika Kayıt Protokolü (SCEP) veya ortak anahtar şifreleme standartları (PKCS) sertifikaları ve Microsoft Intune ile sertifika profilleri için sertifika bağlayıcıları hakkında bilgi edinin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428884"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Microsoft Intune için sertifika bağlayıcıları

Kimlik doğrulama için sertifikaların kullanımını ve S/MIME kullanarak e-postanın imzalanmasını ve şifrelenmesini desteklemek için, Intune bir sertifika bağlayıcısının kullanılmasını gerektirir. Sertifika Bağlayıcısı, şirket içi bir sunucuya yüklediğiniz yazılımdır. Bağlayıcı, bulut tarafından yönetilen cihazların, veren bir sertifika yetkilisi gibi şirket içi altyapıdan sertifika sağlamasını sağlar.

Bu makalede kullanılabilir bağlayıcılar, yaşam döngüleri, kullanım önkoşulları ve bunların güncel tutulması açıklanmaktadır.  

## <a name="available-connectors"></a>Kullanılabilir bağlayıcılar

Intune için iki sertifika Bağlayıcısı vardır. Her birinin kendi kullanımları ve gereksinimleri vardır.

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>Microsoft Intune için PFX Sertifika Bağlayıcısı

**PFX Sertifika Bağlayıcısı** , sertifika istekleri #12 pcks sertifika dağıtımını destekler ve belirli bir kullanıcı için S/MIME e-posta şifrelemesi için Intune 'A aktarılan PFX dosyaları için istekleri işler.

> [!TIP]
> Bu bağlayıcı için Ağustos güncelleştirmesinden önce, PKCS #12 sertifika istekleri, *Intune sertifika Bağlayıcısı*tarafından işlenir. Ağustos güncelleştirmesiyle, tüm PKCS sertifika isteklerinin işlevselliği, bağlayıcının yeni sürümlere otomatik güncelleştirilmesini destekleyen ve .NET Framework sürüm 4.7.2 kullanılmasını gerektiren *PFX Sertifika Bağlayıcısı*'nda birleştirilir.
>
> Microsoft Intune bağlayıcısının işlevselliği kullanım dışı değildir ve PKCS sertifika profilleriyle birlikte kullanılmasına devam edebilir. Ancak, SCEP kullanmıyorsanız veya NDES kullanımını istemiyorsanız, PFX Sertifika Bağlayıcısı ' na geçebilir ve bu durumda NDES 'yi sunucularınızdan kaldırabilirsiniz. 

**PFX Sertifika Bağlayıcısı**:

- Her Intune kiracısı için bu bağlayıcının birden çok örneğini destekler. Bağlayıcının her bir örneği bir Windows sunucusuna yüklenmelidir ve karşıya yüklenen PFX dosyalarının parolalarını şifrelemek için kullanılan özel anahtara erişime sahip olmalıdır.
- , *Microsoft Intune bağlayıcısının*bir örneğini barındıran aynı sunucuya yüklenebilir.
- Yeni sürümlere yönelik [otomatik güncelleştirmeleri](#automatic-update) destekler. Yeni sürümleri otomatik olarak yüklemek için, bağlayıcıyı barındıran bilgisayarın **443**numaralı bağlantı noktasında **AutoUpdate.msappproxy.net** ile iletişim kurabilmesi gerekir. Bağlayıcının otomatik olarak güncelleştirilmesi başarısız olursa, bağlayıcıyı el ile güncelleştirebilirsiniz.
- Sertifika iptalini destekler (bağlayıcının çalıştırması için **6.2008.60.607** veya üzeri sürümü gerekir)
- , [Yönetilen cihazlarla](../fundamentals/intune-endpoints.md#access-for-managed-devices) aynı ağ gereksinimlerine sahiptir

  Daha fazla bilgi için bkz. [Microsoft Intune Için ağ uç noktaları](../fundamentals/intune-endpoints.md)ve [Intune ağ yapılandırma gereksinimleri ve bant genişliği](../fundamentals/network-bandwidth-use.md).

**Bağlayıcının yüklendiği Windows Server**:

- Windows Server 2012 R2 veya sonraki bir sürümü çalıştırılmalıdır.
- .NET 4.7.2 çerçevesini çalıştırın.  

**PFX Sertifika bağlayıcısını yüklemek için**:

Bu bağlayıcının kılavuz yüklemesi için bkz. [PFX Sertifika bağlayıcısını indirme, yükleme ve yapılandırma](certficates-pfx-configure.md).

### <a name="microsoft-intune-connector"></a>Microsoft Intune Bağlayıcısı

**Microsoft Intune Bağlayıcısı** bazen *Microsoft Intune sertifika Bağlayıcısı*olarak adlandırılır. Bu bağlayıcı *basit sertifika kayıt Protokolü* (SCEP) kullandığınızda ve bir Active Directory Sertifika Hizmetleri sertifika YETKILISINE (CA) sahip olduğunuzda sertifika dağıtımını destekler. Bu tür bir CA, *MICROSOFT CA*olarak da adlandırılır.

Bir Microsoft CA ile SCEP kullandığınızda, **ağ cihazı kayıt hizmeti** 'ni (NDES) da yapılandırmanız gerekir. Bu nedenle, bu bağlayıcı genellikle *NDES sertifika Bağlayıcısı*olarak adlandırılır.

[Üçüncü taraf bir sertifika yetkilisi](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration)kullanıyorsanız, bu bağlayıcıyı kullanmanız gerekmez ve NDES gerekli değildir.

**Microsoft Intune Bağlayıcısı**:

- , *PFX Sertifika bağlayıcısının*bir örneğini barındırabilen bir Windows Server 'a yüklenir.
- Her örnek ayrı bir Windows Server üzerinde olmak üzere, kiracı başına bu bağlayıcının en fazla 100 örneğini destekler. Birden çok bağlayıcı kullandığınızda:
  - Ortamınızdaki *Microsoft Intune bağlayıcısının* tüm örnekleri aynı sürümde olmalıdır.
  - Kullanılabilir bağlayıcı örnekleri sertifika isteklerinizi işleyebilmek için altyapınız yedeklilik ve yük dengelemeyi destekler.
- Bağlayıcının yeni sürümünü yüklemek için [el ile güncelleştirme](#manual-update) gerektirir. El ile güncelleştirme, geçerli bağlayıcıyı kaldırmanızı ve sonra bağlayıcının yeni sürümünü yüklemenizi gerektirir. Ek eylemler gerekli değildir.
- *Federal bilgi Işleme standardı* (FIPS) modunu destekler. FIPS gerekli değildir. FIPS etkin olduğunda, sertifika verebilir ve iptal edebilirsiniz.
- , [Yönetilen cihazlarla](../fundamentals/intune-endpoints.md#access-for-managed-devices)aynı ağ gereksinimlerine sahiptir.

  Daha fazla bilgi için bkz. [Microsoft Intune Için ağ uç noktaları](../fundamentals/intune-endpoints.md)ve [Intune ağ yapılandırma gereksinimleri ve bant genişliği](../fundamentals/network-bandwidth-use.md).

**Bağlayıcının yüklendiği Windows Server**:

- Windows Server 2012 R2 veya sonraki bir sürümü çalıştırılmalıdır.
- .NET 4,5 çerçevesini çalıştırın. Bu bağlayıcı *PFX Sertifika Bağlayıcısı*ile aynı sunucuya YÜKLENDIĞINDE, PFX Bağlayıcısı için gerekli olan .NET 4.7.2 Framework kullanmanız gerekir.
- , Veren sertifika yetkilinizi (CA) barındıran aynı sunucu olamaz.
- Bir Microsoft CA 'sı ile SCEP için kullanıldığında NDES çalıştıran bir sunucuya erişim gerekir. NDES bir Windows Server üzerinde çalışır ve bu bağlayıcı ile aynı sunucuda çalışabilir.

**NDES gerekli olduğunda**:

- Internet Explorer Artırılmış Güvenlik Yapılandırması NDES ve *Microsoft Intune bağlayıcısını*barındıran sunucuyu [barındıran sunucuda devre dışı](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) bırakılmalıdır.
- Bağlayıcının NDES ile iletişim kurması için ek yapılandırmaların olması gerekir. *Microsoft Intune bağlayıcısını*yükleme YORDAMLARıNA karşı NDES yükleme ve yapılandırma yordamlarını bulacaksınız.

  NDES hakkında daha fazla bilgi için bkz. [ağ cihazı kayıt hizmeti Kılavuzu](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

**Microsoft Intune bağlayıcısını yüklemek için**:

Bu bağlayıcının yüklenmesiyle ilgili yönergeler için bkz. [Intune Ile SCEP desteklemek için altyapıyı yapılandırma](certificates-scep-configure.md).

## <a name="connector-lifecycle"></a>Bağlayıcı yaşam döngüsü

Sertifika bağlayıcılarının güncelleştirilmiş sürümleri düzenli aralıklarla yayımlanır. Yeni bağlayıcı yayınları için Duyurular (yenilikler) içinde görünür (.. Intune için/temel Mentals/Whats-New.exe) makalesi ve bu makalenin sonundaki [Bağlayıcılar](#whats-new-for-connectors) yenilikleri bölümünde.

Yeni bir sürüm yayımlandığında, önceki sürüme yönelik destek, devam eden kullanımı için sınırlı bir yetkisiz kullanım süresi ile kullanım dışı bırakılmıştır. Yetkisiz kullanım süresi dolduktan sonra, kullanım dışı bırakılan sürüm için destek sona erer ve herhangi bir zamanda çalışmayı durdurabilir. Yetkisiz kullanım süresi altı aydır.

İlk fırsatta bir bağlayıcıyı en son sürüme güncelleştirmeyi planlayın. Her bağlayıcının farklı bir güncelleştirme yolu vardır:

- **Microsoft Intune Için PFX Sertifika Bağlayıcısı** -otomatik güncelleştirmeleri destekler.
- **Microsoft Intune Bağlayıcısı** -el ile güncelleştirme gerektirir.

### <a name="automatic-update"></a>Otomatik güncelleştirme

Bağlayıcı türü ve ortamınız tarafından desteklendikten sonra Intune, bağlayıcı sürümü yayımlandıktan kısa süre sonra bağlayıcıyı otomatik olarak en son sürüme güncelleştirebilir.  

Otomatik olarak güncelleştirmek için, bağlayıcıyı barındıran sunucunun **Azure Update hizmetine**erişmesi gerekir:

- Bağlantı noktası: **443**
- Uç nokta: **AutoUpdate.msappproxy.net**

Güvenlik duvarları, altyapı veya ağ yapılandırmalarında otomatik güncelleştirme erişimi sınırlandırdığınızda, engelleme sorunlarını çözün veya bağlayıcıyı yeni sürüme el ile güncelleştirin.

### <a name="manual-update"></a>El ile güncelleştirme

Bir sertifika bağlayıcısını el ile güncelleştirme işlemi, bağlayıcıyı yeniden yüklemek için aynıdır.

Otomatik güncelleştirmeleri desteklediğinde bile, sertifika bağlayıcısını el ile güncelleştirebilirsiniz. Örneğin, ağ yapılandırmanız otomatik bir güncelleştirmeyi engellediğinde bağlayıcıyı el ile güncelleştirebilirsiniz.  

### <a name="to-reinstall-a-certificate-connector"></a>Bir sertifika bağlayıcısını yeniden yüklemek için

1. Bağlayıcıyı barındıran Windows Server 'da, bağlayıcıyı kaldırmak için **Windows Uygulamaları ve özellikleri** ' ni kullanın.

2. Yeni sürümü yüklemek için, bağlayıcının yeni bir sürümünü yüklemek için yordamını kullanın. Bağlayıcının daha yeni bir sürümünü yüklerken yeni veya güncelleştirilmiş önkoşulları denetlediğinizden emin olun:
   - SCEP: [Intune Ile SCEP desteklemek için altyapıyı yapılandırma](certificates-scep-configure.md)
   - PKCS: [Microsoft Intune IÇIN PFX Sertifika bağlayıcısını indirin, yükleyin ve yapılandırın](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>Bağlayıcı durumu ve sürümü

Microsoft Endpoint Manager Yönetim Merkezi 'nde, durumu hakkında bilgi görüntülemek ve sürümünü doğrulamak için bir sertifika Bağlayıcısı seçebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) oturum açın

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **sertifika bağlayıcıları**' na gidin.

3. Durumunu görüntülemek için bir bağlayıcı seçin.

Bağlayıcı durumu görüntülenirken:

- Kullanım dışı bağlayıcılar, bir **Uyarı**ile gösterilir. Altı aylık yetkisiz kullanım süresinden sonra, uyarı hata olarak değişir.
- Yetkisiz kullanım süresinin ötesinde bağlayıcılar bir hata gösterir. Bu bağlayıcılar artık desteklenmemektedir ve herhangi bir zamanda çalışmayı durdurabilir.

## <a name="whats-new-for-connectors"></a>Bağlayıcılar yenilikleri

İki sertifika Bağlayıcısı için güncelleştirmeler düzenli aralıklarla yayımlanır. Bir bağlayıcıyı güncelleştirdiğimiz zaman, buradaki değişiklikler hakkında bilgi edinebilirsiniz.

### <a name="pfx-certificate-connector-release-history"></a>PFX Sertifika Bağlayıcısı yayın geçmişi

*Microsoft Intune Için PFX Sertifika Bağlayıcısı* [otomatik güncelleştirmeleri destekler](#automatic-update).

#### <a name="august-26-2020"></a>26 Ağustos 2020

**Sürüm 6.2008.60.607** -bu sürümdeki değişiklikler:

- .NET Framework sürüm 4.7.2 gerektirir
- *Microsoft Intune bağlayıcısının* kullanımını PKCS sertifika profilleriyle kullanmak üzere değiştirir. *PFX Sertifika Bağlayıcısı* artık, pcks #12 veya IÇERI aktarılmış PFX sertifikaları kullanmak için gereken tek bağlayıcıdır.
- Windows 8.1 dışındaki tüm desteklenen platformlarla PKCS sertifika profillerini kullanmaya yönelik destek ekler.
- Outlook S/MIME için sertifika iptali desteği ekler.

#### <a name="november-18-2019"></a>18 Kasım 2019

**Sürüm: 6.1911.11.602** -bu sürümdeki değişiklikler:

- PFX Içeri aktarma için S/MIME desteği eklendi.  

#### <a name="may-17-2019"></a>17 Mayıs 2019

**Sürüm 6.1905.0.404** -bu sürümdeki değişiklikler:

- Mevcut PFX sertifikalarının yeniden işlenmesine devam edildiği bir sorun düzeltildi ve bu, bağlayıcının yeni istekleri işlemeyi durdurmasına neden oluyor. 

#### <a name="may-6-2019"></a>6 Mayıs 2019

**Sürüm 6.1905.0.402** -bu sürümdeki değişiklikler:

- Bağlayıcının yoklama aralığı 5 dakikadan 30 saniyeye düşürülür.

#### <a name="april-2-2019"></a>2 Nisan 2019

**Sürüm 6.1904.0.401** -bu sürümdeki değişiklikler:

- Bu bağlayıcı artık otomatik güncelleştirmeyi desteklemektedir.
- Bağlayıcının bir genel yönetici hesabıyla oturum açtıktan sonra Intune 'a kaydolmasına neden olabilecek bir sorun düzeltildi.

### <a name="microsoft-intune-connector-release-history"></a>Microsoft Intune Bağlayıcısı yayın geçmişi

#### <a name="april-2-2019"></a>2 Nisan 2019

**Sürüm 6.1904.1.0** -bu sürümdeki değişiklikler:  

- Bağlayıcının bir genel yönetici hesabıyla oturum açtıktan sonra Intune 'a kaydolmasına neden olabilecek bir sorun düzeltildi.
- Sertifika iptalinde güvenilirlik düzeltmeleri içerir.
- PKCS sertifika isteklerinin işlenme hızını artırmak için performans düzeltmelerini içerir.

## <a name="next-steps"></a>Sonraki adımlar

Kullanmak istediğiniz her platform için SCEP, PKCS veya PKCS içeri aktarılmış sertifika profilleri oluşturun. Devam etmek için aşağıdaki makalelere bakın:

- [Intune ile SCEP sertifikalarını destekleyecek altyapıyı yapılandırma](certificates-scep-configure.md)  
- [Intune ile PKCS sertifikalarını yapılandırma ve yönetme](certficates-pfx-configure.md)  
- [PKCS içeri aktarılmış sertifika profili oluşturma](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
