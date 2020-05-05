---
title: BitLocker ayarları başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager bulunan tüm BitLocker yönetim ayarları
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6a9c566fec22e69c0a4a7fde01b911330ec1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723932"
---
# <a name="bitlocker-settings-reference"></a>BitLocker ayarları başvurusu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!-- 5925683 -->

Configuration Manager BitLocker yönetim ilkeleri aşağıdaki ilke gruplarını içerir:

- Kurulum
- İşletim sistemi sürücüsü
- Sabit sürücü
- Çıkarılabilir sürücü
- İstemci yönetimi

Aşağıdaki bölümlerde, her bir gruptaki ayarlar için yapılandırma açıklanır ve önerilir.

> [!NOTE]
> Bu ayarlar 2002 sürümünü temel alır Configuration Manager. Sürüm 1910, tüm bu ayarları içermez.

## <a name="setup"></a>Kurulum

Bu sayfadaki ayarlar genel BitLocker şifreleme seçeneklerini yapılandırır.

### <a name="drive-encryption-method-and-cipher-strength"></a>Sürücü şifreleme yöntemi ve şifre gücü

*Önerilen yapılandırma*: varsayılan veya daha büyük şifreleme yöntemiyle **etkindir** .

> [!NOTE]
> **Kurulum** özellikleri sayfasında, farklı Windows sürümleri için iki ayar grubu bulunur. Bu bölümde her ikisi de açıklanmaktadır.

#### <a name="windows-81-devices"></a>Windows 8.1 cihazları

Windows 8.1 cihazlar için, **sürücü şifreleme yöntemi ve şifre gücüne**yönelik seçeneği etkinleştirin ve aşağıdaki şifreleme yöntemlerinden birini seçin:

- Ayırıcılı AES 128-bit
- Ayırıcılı AES 256-bit
- AES 128-bit (varsayılan)
- AES 256 bit

#### <a name="windows-10-devices"></a>Windows 10 cihazları

Windows 10 cihazlarında **sürücü şifreleme yöntemi ve şifreleme gücü (Windows 10)** için seçeneği etkinleştirin. Ardından, işletim sistemi sürücüleri, sabit veri sürücüleri ve çıkarılabilir veri sürücüleri için aşağıdaki şifreleme yöntemlerinden birini tek tek seçin:

- AES-CBC 128 bit
- AES-CBC 256 bit
- XTS-AES 128-bit (varsayılan)
- XTS-AES 256 bit

> [!TIP]
> BitLocker, şifreleme algoritması olarak Gelişmiş Şifreleme Standardını (AES) 128 veya 256 bit yapılandırılabilir anahtar uzunluklarıyla kullanır. Windows 10 cihazlarında, AES şifrelemesi Şifre blok zincirleme (CBC) veya şifreli çalmasını (XTS) destekler.
>
> Windows 10 çalıştırmayan cihazlarda çıkarılabilir sürücü kullanmanız gerekiyorsa, AES-CBC kullanın.

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Sürücü şifreleme ve şifre gücüne yönelik genel kullanım notları

- Bu ayarları devre dışı bırakır veya yapılandırmazsanız, BitLocker varsayılan şifreleme yöntemini kullanır.

- Configuration Manager BitLocker 'ı açtığınızda bu ayarları uygular.

- Sürücü zaten şifrelendiyse veya devam ediyorsa, bu ilke ayarlarında yapılan herhangi bir değişiklik cihazdaki sürücü şifrelemesini değiştirmez.

- Varsayılan değeri kullanırsanız, BitLocker bilgisayar uyumluluk raporu şifre gücünü **bilinmiyor**olarak gösterebilir. Bu sorunu geçici olarak çözmek için bu ayarı etkinleştirin ve şifre gücüne yönelik açık bir değer ayarlayın.

### <a name="prevent-memory-overwrite-on-restart"></a>Yeniden başlatma sırasında belleği üzerine yazmayı engelle

*Önerilen yapılandırma*: **Yapılandırılmadı**

Yeniden başlatma sırasında bellekte BitLocker gizli dizileri üzerine yazmadan yeniden başlatma performansını artırmak için bu ilkeyi yapılandırın.

Bu ilkeyi yapılandırmadığınızda, bilgisayar yeniden başlatıldığında BitLocker gizli dizilerini bellekten kaldırır.

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Akıllı kart sertifikası kullanım kuralı uyumluluğunu doğrula

*Önerilen yapılandırma*: **Yapılandırılmadı**

Bu ilkeyi, akıllı kart sertifika tabanlı BitLocker korumasını kullanacak şekilde yapılandırın. Ardından Sertifika **nesne tanımlayıcısını**belirtin.

Bu ilkeyi yapılandırmadığınızda, BitLocker bir sertifikayı belirtmek için varsayılan nesne tanımlayıcısını `1.3.6.1.4.1.311.67.1.1` kullanır.

### <a name="organization-unique-identifiers"></a>Kuruluş benzersiz tanımlayıcıları

*Önerilen yapılandırma*: **Yapılandırılmadı**

Bu ilkeyi sertifika tabanlı veri kurtarma aracısı veya BitLocker To Go Okuyucusu kullanacak şekilde yapılandırın.

Bu ilkeyi yapılandırmadığınızda, BitLocker **kimlik** alanını kullanmaz.

Kuruluşunuz daha yüksek güvenlik ölçümleri gerektiriyorsa, **kimlik** alanını yapılandırın. Bu alanı hedeflenen tüm USB cihazlarda ayarlayın ve bu ayarla hizalayın.

## <a name="os-drive"></a>İşletim sistemi sürücüsü

Bu sayfadaki ayarlar, Windows 'un yüklü olduğu sürücünün şifreleme ayarlarını yapılandırır.

### <a name="operating-system-drive-encryption-settings"></a>İşletim sistemi sürücüsü şifreleme ayarları

*Önerilen yapılandırma*: **etkin**

Bu ayarı etkinleştirirseniz, kullanıcının işletim sistemi sürücüsünü koruması gerekir ve BitLocker sürücüyü şifreler. Devre dışı bırakırsanız, Kullanıcı sürücüyü koruyamaz. Bu ilkeyi yapılandırmazsanız, işletim sistemi sürücüsünde BitLocker koruması gerekli değildir.

> [!NOTE]
> Sürücü zaten şifrelendiyse ve bu ayarı devre dışı bırakırsanız, BitLocker sürücünün şifresini çözer.  

[Güvenilir Platform Modülü (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node)olmayan cihazlarınız varsa, **uyumlu bir TPM olmadan BitLocker 'a izin verme (parola gerektirir)** seçeneğini kullanın. Bu ayar, cihazın TPM 'ye sahip olmasa bile, BitLocker 'ın işletim sistemi sürücüsünü şifrelemesine olanak tanır. Bu seçeneğe izin verirseniz, Windows kullanıcıdan bir BitLocker parolası belirtmesini ister.

Uyumlu TPM içeren cihazlarda, şifrelenmiş veriler için ek koruma sağlamak üzere başlangıçta iki tür kimlik doğrulama yöntemi kullanılabilir. Bilgisayar başladığında, kimlik doğrulaması için yalnızca TPM kullanabilir veya bir kişisel kimlik numarası (PIN) girişi gerektirebilir. Aşağıdaki ayarları yapılandırın:

- **İşletim sistemi sürücüsü için koruyucu seçin**: bunu TPM ve PIN kullanacak şekilde yapılandırın ya da yalnızca TPM 'yi kullanın.

- **Başlangıç için en düşük PIN uzunluğunu Yapılandır**: PIN gerekiyorsa, bu değer kullanıcının belirtebileceğiniz en kısa uzunluktadır. Bilgisayar sürücünün kilidini açmak için önyükleme yaptığında Kullanıcı bu PIN 'ı girer. Varsayılan olarak, en küçük PIN uzunluğu olur `4`.

> [!TIP]
> Daha yüksek güvenlik için, TPM + PIN koruyucusu ile cihazları etkinleştirdiğinizde, **sistem** > **güç yönetimi** > **uyku ayarları**' nda aşağıdaki Grup İlkesi ayarlarını *devre dışı bırakmayı* göz önünde bulundurun:
>
> - Uykuda (prize takılıyken) bekleme durumlarına (S1-S3) izin ver
>
> - Uyku modundayken bekleme durumlarına (S1-S3) izin ver (Pilde)

### <a name="allow-enhanced-pins-for-startup"></a>Başlangıç için iyileştirilmiş PIN 'Ler sağla

*Önerilen yapılandırma*: **Yapılandırılmadı**

BitLocker 'ı Gelişmiş başlangıç PIN 'Lerini kullanacak şekilde yapılandırın. Bu PIN 'Ler büyük ve küçük harfler, semboller, sayılar ve boşluklar gibi ek karakterlerin kullanılmasına izin verir. Bu ayar BitLocker 'ı açtığınızda geçerlidir.

> [!IMPORTANT]
> Tüm bilgisayarlar, önyükleme öncesi ortamda gelişmiş PIN 'leri desteklemez. Kullanımını etkinleştirmeden önce, cihazlarınızın bu özellikle uyumlu olup olmadığını değerlendirin.

Bu ayarı etkinleştirirseniz, tüm yeni BitLocker başlangıç PIN 'leri kullanıcının gelişmiş PIN 'Ler oluşturmasına izin verir.

- **Yalnızca ASCII PIN 'Leri gerektir**: gelişmiş PIN 'leri önyükleme öncesi ortama girebileceğiniz karakter türlerini veya sayısını sınırlayan bilgisayarlarla daha uyumlu hale getirme yardımı.

Bu ilke ayarını devre dışı bırakır veya yapılandırmazsanız, BitLocker gelişmiş PIN kullanmaz.

### <a name="operating-system-drive-password-policy"></a>İşletim sistemi sürücüsü parola ilkesi

*Önerilen yapılandırma*: **Yapılandırılmadı**

BitLocker korumalı işletim sistemi sürücülerinin kilidini açmak üzere parola kısıtlamalarını ayarlamak için bu ayarları kullanın. İşletim sistemi sürücülerinde TPM olmayan koruyuculardan izin verirseniz, aşağıdaki ayarları yapılandırın:

- **İşletim sistemi sürücüleri için parola karmaşıklığını yapılandırma**: parola üzerinde karmaşıklık gereksinimlerini zorlamak için **parola karmaşıklığı gerektir**' i seçin.

- **İşletim sistemi sürücüsü Için en az parola uzunluğu**: varsayılan olarak en düşük uzunluk `8`.

- **Çıkarılabilir işletim sistemi sürücüleri için yalnızca ASCII parolaları iste**

Bu ilke ayarını etkinleştirirseniz, kullanıcılar tanımladığınız gereksinimleri karşılayan bir parola yapılandırabilir.

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>İşletim sistemi sürücüsü parola ilkesi için genel kullanım notları

- Bu karmaşıklık gereksinimi ayarlarının etkin olması için, **bilgisayar yapılandırması** > **Windows ayarları** > **güvenlik ayarları** > **hesap ilkeleri** > **parola ilkesi**' nde Grup İlkesi ayarı **parolasının karmaşıklık gereksinimlerini karşılaması gerekir** .

- BitLocker, bir birimin kilidini açtığınızda değil, açtığınızda bu ayarları uygular. BitLocker, sürücüde bulunan koruyucularla bir sürücünün kilidini açmanızı sağlar.

- Şifreleme, karma ve imzalama için FIPS uyumlu algoritmaları etkinleştirmek üzere Grup ilkesi kullanıyorsanız, BitLocker koruyucusu olarak parolalara izin verebilirsiniz.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>BitLocker kurtarma işleminden sonra platform doğrulama verilerini sıfırlama

*Önerilen yapılandırma*: **Yapılandırılmadı**

Windows 'un, BitLocker kurtarma işleminden sonra başlatıldığında platform doğrulama verilerini yenileip yenilemediğini denetleyin.

Bu ayarı etkinleştirir veya yapılandırmazsanız, Windows Platform doğrulama verilerini bu durumda yeniler.

Bu ilke ayarını devre dışı bırakırsanız Windows, bu durumda platform doğrulama verilerini yenilemez.

### <a name="pre-boot-recovery-message-and-url"></a>Önyükleme öncesi kurtarma iletisi ve URL 'SI

*Önerilen yapılandırma*: **Yapılandırılmadı**

BitLocker işletim sistemi sürücüsünü kilitlediğinde, özel bir kurtarma iletisi veya önyükleme öncesi BitLocker kurtarma ekranında bir URL 'YI göstermek için bu ayarı kullanın. Bu ayar yalnızca Windows 10 cihazları için geçerlidir.

Bu ayarı etkinleştirdiğinizde önyükleme öncesi kurtarma iletisi için aşağıdaki seçeneklerden birini belirleyin:

- **Varsayılan kurtarma iletisini ve URL 'Yi kullan**: önyükleme öncesi BitLocker kurtarma ekranında varsayılan BitLocker kurtarma iletisini ve URL 'sini görüntüleyin. Daha önce özel bir kurtarma iletisi veya URL yapılandırdıysanız, varsayılan iletiye geri dönmek için bu seçeneği kullanın.

- **Özel kurtarma Iletisi kullan**: önyükleme öncesi BitLocker kurtarma ekranına özel bir ileti ekleyin.

  - **Özel kurtarma iletisi seçeneği**: görüntülenecek özel iletiyi yazın. Kurtarma URL 'sini de belirtmek istiyorsanız, bu özel kurtarma iletisinin bir parçası olarak dahil edin. En fazla dize uzunluğu 32.768 karakterdir.

- **Özel kurtarma URL 'Si kullan**: önyükleme öncesi BitLocker kurtarma ekranında görünen varsayılan URL 'yi değiştirin.

  - **Özel kurtarma URL 'si seçeneği**: görüntülenecek URL 'yi yazın. En fazla dize uzunluğu 32.768 karakterdir.

> [!NOTE]
> Ön önyüklemede tüm karakterler ve diller desteklenmez. Ön önyükleme BitLocker kurtarma ekranında doğru göründüğünden emin olmak için özel iletinizi veya URL 'nizi test edin.

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Şifreleme ilkesi zorlama ayarları (işletim sistemi sürücüsü)

*Önerilen yapılandırma*: **etkin**

Kullanıcıların işletim sistemi sürücüsü için BitLocker uyumluluğunu erteleyemelerindeki gün sayısını yapılandırın. **Uyumsuzluk yetkisiz kullanım süresi** Configuration Manager ilk olarak uyumsuz olarak algıladığında başlar. Bu yetkisiz kullanım süresi dolduktan sonra, kullanıcılar gerekli eylemi erteleyebilir veya bir istisna isteyebilir.

Şifreleme işlemi kullanıcı girişi gerektiriyorsa, Windows 'ta gerekli bilgileri sağlamadıkları sürece kullanıcının kapatagerektirmediğini belirten bir iletişim kutusu görüntülenir. Hatalara veya duruma yönelik gelecekteki bildirimler bu kısıtlamaya sahip olmayacaktır.

BitLocker, bir koruyucu eklemek için Kullanıcı etkileşimi gerektirmiyorsa, yetkisiz kullanım süresi dolduktan sonra, BitLocker arka planda şifrelemeyi başlatır.

Bu ayarı devre dışı bırakır veya yapılandırmazsanız, Configuration Manager kullanıcıların BitLocker ilkeleriyle uyumlu olmasını gerektirmez.

İlkeyi hemen zorlamak için bir yetkisiz kullanım süresi ayarlayın `0`.

## <a name="fixed-drive"></a>Sabit sürücü

Bu sayfadaki ayarlar, bir cihazdaki ek veri sürücüleri için şifrelemeyi yapılandırır.

### <a name="fixed-data-drive-encryption"></a>Sabit veri sürücüsü şifrelemesi

*Önerilen yapılandırma*: **etkin**

Sabit veri sürücülerinin şifrelenme gereksinimini yönetin. Bu ayarı etkinleştirirseniz, BitLocker kullanıcıların tüm sabit veri sürücülerine koruma altına yerleştirmesidir. Daha sonra veri sürücüleri şifreler.

Bu ilkeyi etkinleştirdiğinizde, otomatik kilit açma 'yı veya **sabit veri sürücüsü parolası ilkesi**ayarlarını etkinleştirin.

- **Sabit veri sürücüsü için otomatik kilit açmayı yapılandırma**: BitLocker 'ın tüm şifreli veri sürücülerine otomatik olarak kilidini açmak için izin ver veya gerektir. Otomatik kilit açma 'yı kullanmak için, [Işletim sistemi sürücüsünü](#os-drive)şifrelemek Için de BitLocker gerekir.

Bu ayarı yapılandırmazsanız, BitLocker kullanıcıların koruma altına sabit veri sürücüleri yerleştirmesini gerektirmez.

Bu ayarı devre dışı bırakırsanız, kullanıcılar sabit veri sürücülerine BitLocker koruması altına koyulamıyor. BitLocker sabit veri sürücüleri şifreledikten sonra bu ilkeyi devre dışı bırakırsanız, BitLocker sabit veri sürücülerinin şifresini çözer.

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>BitLocker tarafından korunmayan sabit sürücülere yazma erişimini reddet

*Önerilen yapılandırma*: **Yapılandırılmadı**

Cihazdaki sabit sürücülere veri yazmak için Windows için BitLocker koruması gerekir. BitLocker Bu ilkeyi açtığınızda uygular.

Bu ayarı etkinleştirdiğinizde:

- BitLocker sabit bir veri sürücüsünü koruyorsa, Windows bu dosyayı okuma ve yazma erişimiyle bağlar.

- BitLocker 'ın korumadığı herhangi bir sabit veri sürücüsü için Windows bunu salt okunurdur.

Bu ayarı yapılandırmadığınızda, Windows tüm sabit veri sürücülerine okuma ve yazma erişimiyle takar.

<!-- ### Allow access to BitLocker-protected fixed drives from earlier versions of Windows -->

### <a name="fixed-data-drive-password-policy"></a>Sabit veri sürücüsü parola ilkesi

*Önerilen yapılandırma*: **Yapılandırılmadı**

BitLocker korumalı sabit veri sürücülerinin kilidini açmak üzere parola kısıtlamalarını ayarlamak için bu ayarları kullanın.

Bu ayarı etkinleştirirseniz kullanıcılar, tanımlı gereksinimlerinizi karşılayan bir parola yapılandırabilir.

Daha yüksek güvenlik için bu ayarı etkinleştirin ve sonra aşağıdaki ayarları yapılandırın:

- **Sabit veri sürücüsü için parola gerektir**: Kullanıcıların BitLocker korumalı sabit veri sürücüsünün kilidini açmak için bir parola belirtmesi gerekir.

- **Sabit veri sürücüleri için parola karmaşıklığını yapılandırma**: parola üzerinde karmaşıklık gereksinimlerini zorlamak için **parola karmaşıklığı gerektir**' i seçin.

- **Sabit veri sürücüsü Için en az parola uzunluğu**: varsayılan olarak en düşük uzunluk `8`.

Bu ayarı devre dışı bırakırsanız, kullanıcılar bir parolayı yapılandıramaz.

İlke yapılandırılmadığında, BitLocker varsayılan ayarlarla parolaları destekler. Varsayılan ayarlar parola karmaşıklığı gereksinimlerini içermez ve yalnızca sekiz karakter gerektirir.

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Sabit veri sürücüsü parola ilkesi için genel kullanım notları

- Bu karmaşıklık gereksinimi ayarlarının etkin olması için, **bilgisayar yapılandırması** > **Windows ayarları** > **güvenlik ayarları** > **hesap ilkeleri** > **parola ilkesi**' nde Grup İlkesi ayarı **parolasının karmaşıklık gereksinimlerini karşılaması gerekir** .

- BitLocker, bir birimin kilidini açtığınızda değil, açtığınızda bu ayarları uygular. BitLocker, sürücüde bulunan koruyucularla bir sürücünün kilidini açmanızı sağlar.

- Şifreleme, karma ve imzalama için FIPS uyumlu algoritmaları etkinleştirmek üzere Grup ilkesi kullanıyorsanız, BitLocker koruyucusu olarak parolalara izin verebilirsiniz.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Şifreleme ilkesi zorlama ayarları (Sabit veri sürücüsü)

*Önerilen yapılandırma*: **etkin**

Kullanıcıların, sabit veri sürücüleri için BitLocker uyumluluğunu erteleyedükleri gün sayısını yapılandırın. **Uyumsuzluk yetkisiz kullanım süresi** Configuration Manager ilk olarak sabit veri sürücüsünü uyumsuz olarak algıladığında başlar. İşletim sistemi sürücüsü uyumlu olana kadar sabit veri sürücüsü ilkesini zorlamaz. Yetkisiz kullanım süresi dolduktan sonra, kullanıcılar gerekli eylemi erteleyebilir veya bir istisna isteyebilir.

Şifreleme işlemi kullanıcı girişi gerektiriyorsa, Windows 'ta gerekli bilgileri sağlamadıkları sürece kullanıcının kapatagerektirmediğini belirten bir iletişim kutusu görüntülenir. Hatalara veya duruma yönelik gelecekteki bildirimler bu kısıtlamaya sahip olmayacaktır.

BitLocker, bir koruyucu eklemek için Kullanıcı etkileşimi gerektirmiyorsa, yetkisiz kullanım süresi dolduktan sonra, BitLocker arka planda şifrelemeyi başlatır.

Bu ayarı devre dışı bırakır veya yapılandırmazsanız, Configuration Manager kullanıcıların BitLocker ilkeleriyle uyumlu olmasını gerektirmez.

İlkeyi hemen zorlamak için bir yetkisiz kullanım süresi ayarlayın `0`.

## <a name="removable-drive"></a>Çıkarılabilir sürücü

Bu sayfadaki ayarlar, USB anahtarları gibi çıkarılabilir sürücüler için şifrelemeyi yapılandırır.

### <a name="removable-data-drive-encryption"></a>Çıkarılabilir veri sürücüsü şifrelemesi

*Önerilen yapılandırma*: **etkin**

Bu ayar, çıkarılabilir sürücülerde BitLocker kullanımını denetler.

- **Kullanıcıların çıkarılabilir veri sürücülerinde BitLocker koruması uygulamasına Izin ver**: kullanıcılar çıkarılabilir bir sürücü için BitLocker korumasını açabilir.

- **Kullanıcıların çıkarılabilir veri sürücülerinde BitLocker 'ı askıya almasına ve şifresini çözmesine Izin ver**: kullanıcılar BitLocker sürücü şifrelemesini çıkarılabilir bir sürücüden kaldırabilir veya geçici olarak askıya alabilir.

Bu ayarı etkinleştirdiğinizde ve kullanıcıların BitLocker koruması uygulamasına izin verdikçe Configuration Manager istemci, çıkarılabilir sürücülerle ilgili kurtarma bilgilerini yönetim noktasındaki kurtarma hizmetine kaydeder. Bu davranış, kullanıcıların koruyucu (parola) unutmaları veya kaybetmeleri durumunda sürücüyü kurtarmasına olanak tanır.

Bu ayarı etkinleştirdiğinizde:

- **Çıkarılabilir veri sürücüsü parola ilkesi** ayarlarını etkinleştirin

- Kullanıcı & bilgisayar yapılandırmalarına yönelik olarak, **sistem** > **çıkarılabilir depolama erişimi** 'nde aşağıdaki Grup İlkesi ayarlarını *devre dışı bırakın* :

  - **Tüm çıkarılabilir depolama sınıfları: tüm erişimi Reddet**
  - **Çıkarılabilir diskler: yazma erişimini engelle**
  - **Çıkarılabilir diskler: okuma erişimini engelle**

Bu ayarı devre dışı bırakırsanız, kullanıcılar BitLocker 'ı çıkarılabilir sürücülerde kullanamaz.

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>BitLocker tarafından korunmayan çıkarılabilir sürücülere yazma erişimini engelle

*Önerilen yapılandırma*: **Yapılandırılmadı**

Windows için BitLocker korumasını, cihazdaki çıkarılabilir sürücülere veri yazmak için gerekir. BitLocker Bu ilkeyi açtığınızda uygular.

Bu ayarı etkinleştirdiğinizde:

- BitLocker bir çıkarılabilir sürücüyü koruduğunda, Windows bu dosyayı okuma ve yazma erişimiyle bağlar.

- BitLocker 'ın korumadığı herhangi bir çıkarılabilir sürücü için, Windows bunu salt okunurdur.

- **Başka bir kuruluşta yapılandırılmış cihazlara yazma erişimini reddetme**seçeneğini etkinleştirirseniz, BitLocker yalnızca izin verilen kimlik alanlarıyla eşleşen kimlik alanları olan çıkarılabilir sürücülere yazma erişimi verir. Bu alanları, [Kurulum](#setup) sayfasında **kuruluşa özgü tanımlayıcı** genel ayarları ile tanımlayın.

Bu ayarı devre dışı bıraktığınızda veya yapılandırmadığınızda, Windows tüm çıkarılabilir sürücüleri okuma ve yazma erişimiyle takar.

> [!NOTE]
> Bu ayarı, **sistem** > **çıkarılabilir depolama erişimi**'ndeki Grup İlkesi ayarlarıyla geçersiz kılabilirsiniz. Çıkarılabilir diskler Grup İlkesi ayarını etkinleştirirseniz, **yazma erişimini reddet**, ardından BitLocker bu Configuration Manager ayarını yoksayar.

<!-- ### Allow access to BitLocker-protected removable data drives from earlier versions of Windows -->

### <a name="removable-data-drive-password-policy"></a>Çıkarılabilir veri sürücüsü parola ilkesi

*Önerilen yapılandırma*: **etkin**

BitLocker korumalı çıkarılabilir sürücülerin kilidini açmak üzere parola kısıtlamalarını ayarlamak için bu ayarları kullanın.

Bu ayarı etkinleştirirseniz kullanıcılar, tanımlı gereksinimlerinizi karşılayan bir parola yapılandırabilir.

Daha yüksek güvenlik için bu ayarı etkinleştirin ve sonra aşağıdaki ayarları yapılandırın:

- **Çıkarılabilir veri sürücüsü için parola gerektir**: Kullanıcıların BitLocker korumalı çıkarılabilir sürücünün kilidini açmak için bir parola belirtmesi gerekir.

- **Çıkarılabilir veri sürücüleri için parola karmaşıklığı yapılandırma**: parola üzerinde karmaşıklık gereksinimlerini zorlamak için **parola karmaşıklığı gerektir**' i seçin.

- **Çıkarılabilir veri sürücüsü Için en az parola uzunluğu**: varsayılan olarak en düşük uzunluk `8`.

Bu ayarı devre dışı bırakırsanız, kullanıcılar bir parolayı yapılandıramaz.

İlke yapılandırılmadığında, BitLocker varsayılan ayarlarla parolaları destekler. Varsayılan ayarlar parola karmaşıklığı gereksinimlerini içermez ve yalnızca sekiz karakter gerektirir.

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Çıkarılabilir veri sürücüsü parola ilkesi için genel kullanım notları

- Bu karmaşıklık gereksinimi ayarlarının etkin olması için, **bilgisayar yapılandırması** > **Windows ayarları** > **güvenlik ayarları** > **hesap ilkeleri** > **parola ilkesi**' nde Grup İlkesi ayarı **parolasının karmaşıklık gereksinimlerini karşılaması gerekir** .

- BitLocker, bir birimin kilidini açtığınızda değil, açtığınızda bu ayarları uygular. BitLocker, sürücüde bulunan koruyucularla bir sürücünün kilidini açmanızı sağlar.

- Şifreleme, karma ve imzalama için FIPS uyumlu algoritmaları etkinleştirmek üzere Grup ilkesi kullanıyorsanız, BitLocker koruyucusu olarak parolalara izin verebilirsiniz.

## <a name="client-management"></a>İstemci yönetimi

Bu sayfadaki ayarlar, BitLocker yönetim hizmetleri ve istemcilerini yapılandırır.

### <a name="bitlocker-management-services"></a>BitLocker yönetim hizmetleri

*Önerilen yapılandırma*: **etkin**

Bu ayarı etkinleştirdiğinizde, otomatik olarak Configuration Manager ve site veritabanında anahtar kurtarma bilgilerini sessizce yedekler. Bu ayarı devre dışı bırakır veya yapılandırmazsanız Configuration Manager, anahtar kurtarma bilgilerini kaydetmez.

- **Depolanacak BitLocker kurtarma bilgilerini seçin**: BitLocker kurtarma bilgilerini yedeklemek için anahtar kurtarma hizmetini yapılandırın. Bu, anahtar bilgilerinin bulunmaması nedeniyle veri kaybını önlemeye yardımcı olan BitLocker tarafından şifrelenmiş verileri kurtarmak için yönetim yöntemi sağlar.

- **Kurtarma bilgilerinin düz metin olarak depolanmasına Izin ver**: SQL Server için BitLocker yönetim şifreleme sertifikası olmadan Configuration Manager, anahtar kurtarma bilgilerini düz metin olarak depolar. Daha fazla bilgi için bkz. [kurtarma verilerini şifreleme](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **İstemci denetleme durum sıklığı (dakika)**: yapılandırılan sıklıkta istemci, bilgisayardaki BitLocker koruma ilkelerini ve durumunu denetler ve ayrıca istemci kurtarma anahtarını yedekler. Configuration Manager istemcisi varsayılan olarak, BitLocker kurtarma bilgilerini her 90 dakikada bir güncelleştirir.

### <a name="user-exemption-policy"></a>Kullanıcı muafiyet ilkesi

*Önerilen yapılandırma*: **Yapılandırılmadı**

Kullanıcıların BitLocker şifrelemesi dışında bir istisna istemesi için bir iletişim yöntemi yapılandırın.

Bu ilke ayarını etkinleştirirseniz, aşağıdaki bilgileri sağlayın:

- **En fazla erteleme günü**: kullanıcının zorlanan bir ilkeyi kaç gün erteleyebilirler. Varsayılan olarak, bu değer `7` gün (bir hafta).

- **İletişim yöntemi**: kullanıcıların nasıl bir istisna isteyekullanabileceğinizi BELIRTIN: URL, e-posta adresi veya telefon numarası.

- **İletişim**: URL, e-posta adresi veya telefon numarası belirtin. Bir Kullanıcı BitLocker korumasından bir istisna istediğinde, nasıl uygulanacağını gösteren yönergeler içeren bir Windows iletişim kutusu görür. Configuration Manager girdiğiniz bilgileri doğrulamaz.

  - **URL**: standart URL biçimini kullanın, `https://website.domain.tld`. Windows, URL 'YI bir köprü olarak görüntüler.

  - **E-posta adresi**: standart e-posta adresi `user@domain.tld`biçimini kullanın. Windows adresi şu köprü olarak görüntüler: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`.

  - **Telefon numarası**: kullanıcılarınızın aramasını istediğiniz sayıyı belirtin. Windows, numarayı şu açıklamayla görüntüler: `Please call <your number> for applying exemption`.

Bu ayarı devre dışı bırakır veya yapılandırmazsanız, Windows, kullanıcılara muafiyet isteği yönergelerini görüntülemez.

> [!NOTE]
> BitLocker, bilgisayar başına değil, Kullanıcı başına muafiyetleri yönetir. Aynı bilgisayarda birden çok kullanıcı oturum açtığında ve herhangi bir Kullanıcı muaf tutulmazsa, BitLocker bilgisayarı şifreler.

### <a name="url-for-the-security-policy-link"></a>Güvenlik ilkesi bağlantısı URL 'SI

*Önerilen yapılandırma*: **etkin**

Windows 'da **Şirket güvenlik ilkesi** olarak kullanıcılara görüntülenecek bir URL belirtin. Kullanıcılara şifreleme gereksinimleri hakkında bilgi sağlamak için bu bağlantıyı kullanın. BitLocker 'ın kullanıcıdan bir sürücü şifrelemesini isteyip istemeyeceğini gösterir.

Bu ayarı etkinleştirirseniz **güvenlik ilkesi bağlantı URL 'sini**yapılandırın.

Bu ayarı devre dışı bırakır veya yapılandırmazsanız, BitLocker güvenlik ilkesi bağlantısını göstermez.
