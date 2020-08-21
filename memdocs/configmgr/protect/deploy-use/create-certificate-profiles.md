---
title: SCEP sertifika profilleri oluşturma
titleSuffix: Configuration Manager
description: Sertifika profillerini, ihtiyaç duydukları sertifikalarla yönetilen cihazları sağlamak için kullanmayı öğrenin
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f1ea48887f89cf06ed4b41d0de0dfc24e9d508
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697135"
---
# <a name="create-certificate-profiles"></a>Sertifika profilleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Şirket kaynaklarına erişmek için ihtiyaç duydukları sertifikalara sahip yönetilen cihazları sağlamak için Configuration Manager 'deki sertifika profillerini kullanın. Sertifika profillerini oluşturmadan önce, [sertifika altyapısını ayarlama bölümünde açıklandığı](certificate-infrastructure.md)gibi sertifika altyapısını ayarlayın.  

> [!TIP]
> Ortak yönetilen cihazlar için, [ **kaynak erişim ilkeleri** iş yükünü](../../comanage/workloads.md#resource-access-policies) Intune 'a taşımayı düşünün. Daha sonra bu sertifikaları yönetmek için Intune ilkelerini kullanın. Daha fazla bilgi için bkz. [iş yüklerini değiştirme](../../comanage/how-to-switch-workloads.md).

Bu makalede, güvenilen kök ve Basit Sertifika Kayıt Protokolü (SCEP) Sertifika profillerinin nasıl oluşturulacağı açıklanır. PFX Sertifika profilleri oluşturmak istiyorsanız bkz. [PFX Sertifika profilleri oluşturma](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

Bir sertifika profili oluşturmak için:

1. Sertifika profili oluşturma Sihirbazı 'Nı başlatın.
1. Sertifikayla ilgili genel bilgileri sağlayın.
1. Güvenilen sertifika yetkilisi (CA) sertifikası yapılandırın.  
1. SCEP sertifika bilgilerini yapılandırın.  
1. Sertifika profili için desteklenen platformları belirtin.

## <a name="start-the-wizard"></a>Sihirbazı Başlat  

Sertifika oluşturma profilini başlatmak için:

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve **sertifika profilleri** düğümünü seçin.  

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **sertifika profili oluştur**' u seçin.  

## <a name="general"></a>Genel

**Sertifika Profili Oluşturma** Sihirbazı'nın Genel sayfasında aşağıdaki bilgileri belirtin:  

- **Ad**: Sertifika profili için benzersiz bir ad girin. En fazla 256 karakter kullanabilirsiniz.  

- **Açıklama**: sertifika profiline genel bakış sağlayan bir açıklama belirtin. Ayrıca, Configuration Manager konsolunda tanımlanmasına yardımcı olan diğer ilgili bilgileri de içerir. En fazla 256 karakter kullanabilirsiniz.  

- Oluşturmak istediğiniz sertifika profili türünü belirtin:

  - **GÜVENILEN CA sertifikası**: Kullanıcı veya cihazın başka bir cihaz için kimlik doğrulaması yapması gerektiğinde bir sertifika güven zinciri oluşturmak için güvenilen bir kök sertifika YETKILISI (CA) veya ara CA sertifikası dağıtmak üzere bu türü seçin. Örneğin, cihaz bir Uzak Kimlik Denetimi İçeri Arama Kullanıcı Hizmeti (RADIUS) sunucusu veya bir sanal özel ağ (VPN) sunucusu olabilir.
  
    Bir SCEP sertifika profili oluşturabilmeniz için bir güvenilen CA sertifika profili de yapılandırın. Bu durumda, güvenilen CA sertifikasının, sertifikayı kullanıcıya veya cihaza veren CA için olması gerekir.  

  - **Basit sertifika kayıt Protokolü (SCEP) ayarları**: basit sertifika kayıt Protokolü ve ağ cihazı kayıt HIZMETI (NDES) rol hizmeti ile bir kullanıcı veya cihaz için sertifika istemek üzere bu türü seçin.

  - **Kişisel bilgi DEĞIŞIMI PKCS #12 (PFX) ayarları-Içeri aktar**: bir PFX sertifikasını içeri aktarmak için bu seçeneği belirleyin. Daha fazla bilgi için bkz. [PFX Sertifika profillerini Içeri aktarma](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - **Kişisel bilgi DEĞIŞIMI PKCS #12 (PFX) ayarları-oluştur**: bir sertifika YETKILISI kullanarak PFX sertifikalarını işlemek için bu seçeneği belirleyin. Daha fazla bilgi için bkz. [PFX Sertifika profilleri oluşturma](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## <a name="trusted-ca-certificate"></a>Güvenilen CA sertifikası  

> [!IMPORTANT]  
> Bir SCEP sertifika profili oluşturmadan önce en az bir güvenilen CA sertifika profili yapılandırın.
>
> Sertifika dağıtıldıktan sonra, bu değerlerden herhangi birini değiştirirseniz, yeni bir sertifika istenir:
>
> - Anahtar depolama alanı sağlayıcısı
> - Sertifika şablonu adı
> - Sertifika türü
> - Konu adı biçimi
> - Konu diğer adı
> - Sertifika geçerlilik süresi
> - Anahtar kullanımı
> - Anahtar boyutu
> - Genişletilmiş anahtar kullanımı
> - Kök CA sertifikası

1. Sertifika Profili Oluşturma Sihirbazı'nın **Güvenilir SA Sertifikası** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Sertifika dosyası**: **içeri aktar**' ı seçin ve ardından sertifika dosyasına gidin.  

    - **Hedef depo**: Birden çok sertifika deposuna sahip cihazlar için sertifikanın depolanacağı yeri seçin. Yalnızca bir depoya sahip cihazlarda bu ayar yok sayılır.  

2. Doğru sertifikayı içeri aktardığınızı doğrulamak için **sertifika parmak izi** değerini kullanın.  

## <a name="scep-certificates"></a>SCEP sertifikaları

### <a name="1-scep-servers"></a>1. SCEP sunucuları

Sertifika Profili Oluşturma Sihirbazı’nın **SCEP Sunucuları** sayfasında, SCEP üzerinden sertifika verecek NDES Sunucularının URL’lerini belirtin. Sertifika kayıt noktasının yapılandırmasına göre otomatik olarak bir NDES URL 'SI atayabilir veya URL 'Leri el ile ekleyebilirsiniz.  

### <a name="2-scep-enrollment"></a>2. SCEP Kaydı

Sertifika profili oluşturma sihirbazının **SCEP kayıt** sayfasını doldurun.

- **Yeniden denemeler**: cihazın NDES sunucusuna sertifika isteğini otomatik olarak kaç kez yeniden deneyeceğini belirtin. Bu ayar, bir CA yöneticisinin kabul edilmeden önce bir sertifika isteğini onaylaması gereken senaryoyu destekler. Bu ayar genellikle, yüksek güvenlikli ortamlar için veya bir kuruluş sertifika yetkilisi yerine bir tek başına yayımlayan sertifika yetkiliniz varsa kullanılır. Bu ayarı, yayımlayan sertifika yetkilisi, sertifika talebini tanımlamadan önce sertifika talebi seçeneklerini inceleyebilmeniz adına test amaçlı olarak da kullanabilirsiniz. Bu ayarı, **Yeniden deneme gecikmesi (dakika)** ayarıyla birlikte kullanın.  

- **Yeniden deneme gecikmesi (dakika)**: Veren sertifika yetkilisi sertifika isteğini işlemeden önce CA yöneticisi onayı kullandığınızda, her bir kayıt denemesi arasındaki aralığı dakika cinsinden belirtin. Test amaçlı olarak yönetici onayı kullanıyorsanız, düşük bir değer belirtin. Daha sonra, isteği onayladıktan sonra cihazın sertifika isteğini yeniden denemesi uzun zaman beklemiyoruz.

    Bir üretim ağında yönetici onayı kullanıyorsanız, daha yüksek bir değer belirtin. Bu davranış, CA yöneticisinin bekleyen onayları onaylaması veya reddetmesi için yeterli zaman sağlar.  

- **Yenileme eşiği (%)**: Cihazın, sertifikanın yenilenmesini istemesi için kalan sertifika ömrünün yüzde kaç olması gerektiğini belirtin.  

- **Anahtar depolama sağlayıcısı (KSP)**: sertifika anahtarının depolanacağı yeri belirtin. Aşağıdaki değerlerden birini seçin:  

  - **Varsa Güvenilir Platform Modülü'ne (TPM) yükle**: Anahtarı TPM'ye yükler. TPM yoksa, anahtar, yazılım anahtarı için depolama sağlayıcısına yüklenir.  

  - **Güvenilir Platform Modülü'ne (TPM) yükle, yoksa başarısız kıl**: Anahtarı TPM'ye yükler. TPM modülü yoksa, yükleme başarısız olur.  

  - **İş Için Windows Hello 'Ya yüklemek istemiyorsanız başarısız oldu**: Bu seçenek Windows 10 cihazlarında kullanılabilir. Bu, sertifikayı Multi-Factor Authentication tarafından korunan Iş için Windows Hello Mağazası 'nda depolamanıza olanak tanır. Daha fazla bilgi için bkz. [iş Için Windows Hello](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Bu seçenek, sertifika özellikleri sayfasındaki Gelişmiş anahtar kullanımı için akıllı kartla oturum açmayı desteklemez.

  - **Yazılım Anahtar Depolama Sağlayıcısı'na Yükle**: Anahtarı yazılım anahtarı depolama sağlayıcısına yükler.  

- **Sertifika kaydı Için cihazlar**: sertifika profilini bir kullanıcı koleksiyonuna dağıtırsanız, yalnızca kullanıcının birincil cihazında veya kullanıcının oturum açtığı herhangi bir cihazda sertifika kaydına izin verin.

    Sertifika profilini bir cihaz koleksiyonuna dağıtırsanız, yalnızca cihazın birincil kullanıcısı veya cihazda oturum açarken kullanılan tüm kullanıcılar için sertifika kaydına izin verin.  

### <a name="3-certificate-properties"></a>3. Sertifika Özellikleri

Sertifika Profili Oluşturma Sihirbazı'nın **Sertifika Özellikleri** sayfasında, aşağıdaki bilgileri belirtin:  

- **Sertifika şablonu adı**: NDES 'de yapılandırdığınız ve veren bir CA 'ya eklenen bir sertifika şablonunun adını seçin. Sertifika şablonlarına başarıyla gitmek için Kullanıcı hesabınızın sertifika şablonu için **okuma** izni olması gerekir. Sertifikaya **gözatamıyorsanız** adını yazın.  

  > [!IMPORTANT]
  > Sertifika şablonu adı ASCII dışı karakterler içeriyorsa, sertifika dağıtılmaz. (Bu karakterlerin bir örneği Çince alfabeden oluşur.) Sertifikanın dağıtıldığından emin olmak için, önce CA 'da sertifika şablonunun bir kopyasını oluşturun. Ardından, ASCII karakterleri kullanarak kopyayı yeniden adlandırın.  

  - Sertifika şablonunun adını seçmek için *gözatdıysanız* sayfadaki bazı alanlar otomatik olarak sertifika şablonundan doldurulur. Bazı durumlarda, farklı bir sertifika şablonu seçmediğiniz takdirde bu değerleri değiştiremezsiniz.  

  - Sertifika şablonunun adını *yazarsanız* , adın sertifika şablonlarından biriyle tam olarak eşleştiğinden emin olun. NDES sunucusunun kayıt defterinde listelenen adlarla aynı olmalıdır. Sertifika şablonunun görünen adını değil, sertifika şablonu adını belirttiğinizden emin olun.  

    Sertifika şablonlarının adlarını bulmak için aşağıdaki kayıt defteri anahtarına gidin: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP` . **EncryptionTemplate**, **Generaldeðersetemplate**ve **SignatureTemplate**için değerler olarak sertifika şablonlarını listeler. Varsayılan olarak, tüm üç sertifika şablonu için değer **IPSECIntermediateOffline**'dır, bu, **IPSec (Çevrimdışı talep)** şablon ekran adına eşlenir.  

    > [!WARNING]  
    > Sertifika şablonunun adını yazdığınızda Configuration Manager, sertifika şablonunun içeriğini doğrulayamaz. Sertifika şablonunun desteklemediği seçenekleri belirleyebilirsiniz, bu durum başarısız bir sertifika isteğine neden olabilir. Bu davranış gerçekleştiğinde, CPR. log dosyasında, sertifika imzalama isteği (CSR) ve güçlük ile ilgili şablon adının eşleşmediğinden w3wp.exe için bir hata iletisi görürsünüz.  
    >
    > **Generalstasetemplate** değeri için belirtilen sertifika şablonunun adını yazdığınızda, bu sertifika profili için **anahtar şifreleme** ve **dijital imza** seçeneklerini belirleyin. Bu sertifika profilinde yalnızca **anahtar şifreleme** seçeneğini etkinleştirmek Istiyorsanız, **EncryptionTemplate** anahtarı için sertifika şablonu adını belirtin. Benzer şekilde, bu sertifika profilinde yalnızca **Dijital imza** seçeneğini etkinleştirmek istiyorsanız, **SignatureTemplate** anahtarı için sertifika şablonu adını belirtin.  

- **Sertifika türü**: sertifikanın bir cihaza mı yoksa bir kullanıcıya mı dağıtılacağını seçin.  

- **Konu adı biçimi**: Configuration Manager sertifika isteğinde konu adını otomatik olarak nasıl oluşturduğunu seçin. Sertifika bir kullanıcı içinse, konu adına kullanıcının e-posta adresini de ekleyebilirsiniz.

    > [!NOTE]  
    > **IMEI numarası** veya **seri numarası**' nı seçerseniz, aynı kullanıcıya ait olan farklı cihazlar arasında ayrım yapabilirsiniz. Örneğin, bu cihazlar ortak bir ad paylaşabilir, ancak ıMEı numarası veya seri numarası değil. Cihaz ıMEı veya seri numarası bildirmezse, sertifika ortak ad ile verilir.

- **Konu diğer adı**: Configuration Manager sertifika isteğinde konu alternatif adı (San) için değerleri otomatik olarak nasıl oluşturduğunu belirtin. Örneğin, bir kullanıcı sertifikası türü seçtiyseniz, konu alternatif adına kullanıcı asıl adını (UPN) ekleyebilirsiniz. İstemci sertifikası bir ağ Ilkesi sunucusu için kimlik doğrulaması yapacaktır, konu diğer adı ' nı UPN olarak ayarlayın.  

- **Sertifika geçerlilik süresi**: veren CA 'da özel bir geçerlilik süresi ayarlarsanız, sertifikanın süresi dolmadan önce kalan sürenin miktarını belirtin.

    > [!TIP]
    > Aşağıdaki komut satırı ile özel bir geçerlilik süresi ayarlayın: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Bu komut hakkında daha fazla bilgi için bkz. [sertifika altyapısı](certificate-infrastructure.md).  

    Belirtilen sertifika şablonundaki geçerlilik süresinden düşük bir değer belirtebilirsiniz, ancak daha yüksek olabilir. Örneğin, sertifika şablonunda sertifika geçerlilik süresi iki yılsa, beş yıl değerini değil, bir yıl değeri belirtebilirsiniz. Değerin, yayımlayan sertifika yetkilisinin sertifikası için kalan geçerlilik süresinden de düşük olması gerekir.  

- **Anahtar kullanımı**: Sertifika için anahtar kullanımı seçeneklerini belirtin. Aşağıdaki seçeneklerden birini seçin:  

  - **Anahtar şifreleme**: Yalnızca anahtar şifreli olduğunda anahtar değişimine izin verir.  

  - **Dijital imza**: Yalnızca anahtarın korunmasına bir dijital imza yardımcı olduğunda anahtar değişimine izin verir.  

  Bir sertifika şablonu için gözatıdıysanız, farklı bir sertifika şablonu seçmediğiniz takdirde bu ayarları değiştiremezsiniz.  

  Seçilen sertifika şablonunu, yukarıdaki iki anahtar kullanım seçeneğinden biri veya her ikisiyle yapılandırın. Aksi takdirde, sertifika kayıt noktası günlük dosyasında ( **CRP. log**) şu iletiyi görürsünüz: **CSR 'de anahtar kullanımı ve zorluk eşleşmiyor**  

- **Anahtar boyutu (bit)**: Bit cinsinden anahtar boyutunu seçin.  

- **Genişletilmiş anahtar kullanımı**: sertifikanın amaçlanan amacı için değerler ekleyin. Çoğu durumda, kullanıcı veya cihazın bir sunucuya kimliğini doğrulayabilmesi için, sertifika **İstemci Kimlik Doğrulaması** gerektirir. Gerektiğinde başka herhangi bir anahtar kullanımı ekleyebilirsiniz.  

- **Karma algoritması**: Bu sertifika ile kullanmak için uygun karma algoritması türlerinden birini seçin. Bağlanan cihazların destekleyeceği en güçlü güvenlik düzeyini seçin.  

  > [!NOTE]  
  > **SHA-2** , SHA-256, SHA-384 ve SHA-512’yi destekler. **SHA-3** , yalnızca SHA-3’ü destekler.  

- **Kök CA sertifikası**: daha önce yapılandırdığınız ve kullanıcıya ya da cihaza dağıttığınız BIR kök CA sertifika profili seçin. Bu CA sertifikası, bu sertifika profilinde yapılandırdığınız sertifikayı verecek CA 'nın kök sertifikası olmalıdır.  

  > [!IMPORTANT]  
  > Kullanıcıya veya cihaza dağıtılmamış bir kök CA sertifikası belirtirseniz Configuration Manager, bu sertifika profilinde yapılandırdığınız sertifika isteğini başlatmaz.  

## <a name="supported-platforms"></a>Desteklenen platformlar  

Sertifika profili oluşturma Sihirbazı ' nın **Desteklenen platformlar** sayfasında, sertifika profilini yüklemek istediğiniz işletim sistemi sürümlerini seçin. Sertifika profilini kullanılabilir tüm işletim sistemlerine yüklemek için **Tümünü Seç ' i** seçin.

## <a name="next-steps"></a>Sonraki adımlar

Yeni sertifika profili **varlıklar ve uyum** çalışma alanındaki **sertifika profilleri** düğümünde görünür. Kullanıcılara veya cihazlara dağıtım için hazırız. Daha fazla bilgi için bkz. [profilleri dağıtma](deploy-wifi-vpn-email-cert-profiles.md).