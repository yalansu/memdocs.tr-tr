---
title: BitLocker yönetimini dağıtma
titleSuffix: Configuration Manager
description: İstemcileri ve kurtarma hizmetini yönetim noktalarına Configuration Manager için BitLocker yönetim aracısını dağıtma
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 018b8f09b0f5595c854eee761f495974665a45ce
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574687"
---
# <a name="deploy-bitlocker-management"></a>BitLocker yönetimini dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

Configuration Manager 'de BitLocker Yönetimi aşağıdaki bileşenleri içerir:

- **BitLocker yönetim aracısı**: Configuration Manager [bir ilke oluşturup](#create-a-policy) [bir koleksiyona dağıttığınızda](#deploy-a-policy), bu aracıyı bir cihazda sağlar.

- **Kurtarma hizmeti**: istemcilerden BitLocker kurtarma verilerini alan sunucu bileşeni. Daha fazla bilgi için bkz. [kurtarma hizmeti](#recovery-service).

BitLocker yönetim ilkeleri oluşturup dağıtmadan önce:

- [Önkoşulları](../../plan-design/bitlocker-management.md#prerequisites) gözden geçirin

- Gerekirse, site veritabanındaki [kurtarma anahtarlarını şifreleyin](encrypt-recovery-data.md)

## <a name="create-a-policy"></a>İlke oluşturma

Bu ilkeyi oluştururken ve dağıttığınızda, Configuration Manager istemcisi cihazdaki BitLocker yönetim aracısını etkinleştirilir.

> [!NOTE]
> Bir BitLocker yönetim ilkesi oluşturmak için, Configuration Manager ' de **tam yönetici** rolüne sahip olmanız gerekir.

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Endpoint Protection**' i genişletin ve **BitLocker yönetim** düğümünü seçin.

1. Şeritte **BitLocker yönetim denetim Ilkesi oluştur**' u seçin.

1. **Genel** sayfasında, bir ad ve isteğe bağlı bir açıklama belirtin. Bu ilkeyle istemcilerde etkinleştirilecek bileşenleri seçin:  

    - **Işletim sistemi sürücüsü**: işletim sistemi sürücüsünün şifrelenip şifrelenmediğini yönetme

    - **Sabit sürücü**: bir cihazdaki ek veri sürücüleri için şifrelemeyi yönetme

    - **Çıkarılabilir sürücü**: bir cihazdan kaldırabilmeniz gereken sürücüler IÇIN bir USB anahtarı gibi şifrelemeyi yönetme

    - **Istemci yönetimi**: BitLocker Sürücü Şifrelemesi kurtarma bilgilerinin anahtar kurtarma hizmeti yedeklemesini yönetme  

1. **Kurulum** sayfasında, BitLocker Sürücü Şifrelemesi için aşağıdaki genel ayarları yapılandırın:

    > [!NOTE]
    > Configuration Manager BitLocker 'ı etkinleştirdiğinizde bu ayarları uygular. Sürücü zaten şifrelendiyse veya devam ediyorsa, bu ilke ayarlarında yapılan herhangi bir değişiklik cihazdaki sürücü şifrelemesini değiştirmez.
    >
    > Bu ayarları devre dışı bırakır veya yapılandırmazsanız, BitLocker varsayılan şifreleme yöntemini (AES 128-bit) kullanır.

    - Windows 8.1 cihazlar için, **sürücü şifreleme yöntemi ve şifre gücü**seçeneklerini etkinleştirin. Ardından şifreleme yöntemini seçin.

    - Windows 10 cihazlarında **sürücü şifreleme yöntemi ve şifreleme gücü (Windows 10)** için seçeneği etkinleştirin. Ardından, işletim sistemi sürücüleri, sabit veri sürücüleri ve çıkarılabilir veri sürücüleri için şifreleme yöntemini tek tek seçin.

    Bu sayfadaki bu ve diğer ayarlar hakkında daha fazla bilgi için bkz. [Ayarlar başvurusu-kurulum](../../tech-ref/bitlocker/settings.md#setup).

1. **Işletim sistemi sürücüsü** sayfasında, aşağıdaki ayarları belirtin:  

    - **Işletim sistemi sürücüsü şifreleme ayarları**: Bu ayarı etkinleştirirseniz, kullanıcının işletim sistemi sürücüsünü koruması gerekir ve BitLocker sürücüyü şifreler. Devre dışı bırakırsanız, Kullanıcı sürücüyü koruyamaz.  

    Uyumlu TPM içeren cihazlarda, şifrelenmiş veriler için ek koruma sağlamak üzere başlangıçta iki tür kimlik doğrulama yöntemi kullanılabilir. Bilgisayar başladığında, kimlik doğrulaması için yalnızca TPM kullanabilir veya bir kişisel kimlik numarası (PIN) girişi gerektirebilir. Aşağıdaki ayarları yapılandırın:

    - **İşletim sistemi sürücüsü için koruyucu seçin**: bunu TPM ve PIN kullanacak şekilde yapılandırın ya da yalnızca TPM 'yi kullanın.

    - **Başlangıç için en düşük PIN uzunluğunu Yapılandır**: PIN gerekiyorsa, bu değer kullanıcının belirtebileceğiniz en kısa uzunluktadır. Bilgisayar sürücünün kilidini açmak için önyükleme yaptığında Kullanıcı bu PIN 'ı girer. Varsayılan olarak, en küçük PIN uzunluğu olur `4` .

    Bu sayfadaki bu ve diğer ayarlar hakkında daha fazla bilgi için bkz. [Ayarlar başvurusu-işletim sistemi sürücüsü](../../tech-ref/bitlocker/settings.md#os-drive).

1. **Sabit sürücü** sayfasında, aşağıdaki ayarları belirtin:

    - **Sabit veri sürücüsü şifrelemesi**: Bu ayarı etkinleştirirseniz BitLocker, kullanıcıların tüm sabit veri sürücülerine koruma altına yerleştirmesidir. Daha sonra veri sürücüleri şifreler. Bu ilkeyi etkinleştirdiğinizde, otomatik kilit açma 'yı veya **sabit veri sürücüsü parolası ilkesi**ayarlarını etkinleştirin.

    - **Sabit veri sürücüsü için otomatik kilit açmayı yapılandırma**: BitLocker 'ın tüm şifreli veri sürücülerine otomatik olarak kilidini açmak için izin ver veya gerektir. Otomatik kilit açma 'yı kullanmak için, işletim sistemi sürücüsünü şifrelemek için de BitLocker gerekir.

    Bu sayfadaki bu ve diğer ayarlar hakkında daha fazla bilgi için bkz. [Ayarlar başvurusu-sabit sürücü](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. **Çıkarılabilir sürücü** sayfasında, aşağıdaki ayarları belirtin:

    - **Çıkarılabilir veri sürücüsü şifrelemesi**: Bu ayarı etkinleştirdiğinizde ve kullanıcıların BitLocker koruması uygulamasına izin verdikçe Configuration Manager istemci, çıkarılabilir sürücülerle ilgili kurtarma bilgilerini yönetim noktasındaki kurtarma hizmetine kaydeder. Bu davranış, kullanıcıların koruyucu (parola) unutmaları veya kaybetmeleri durumunda sürücüyü kurtarmasına olanak tanır.

    - **Kullanıcıların çıkarılabilir veri sürücülerinde BitLocker koruması uygulamasına Izin ver**: kullanıcılar çıkarılabilir bir sürücü için BitLocker korumasını açabilir.

    - **Çıkarılabilir veri sürücüsü parola ilkesi**: BitLocker korumalı çıkarılabilir sürücülerin kilidini açmak üzere parola kısıtlamalarını ayarlamak için bu ayarları kullanın.

    Bu sayfadaki bu ve diğer ayarlar hakkında daha fazla bilgi için bkz. [Ayarlar başvurusu-çıkarılabilir sürücü](../../tech-ref/bitlocker/settings.md#removable-drive).

1. **Istemci yönetimi** sayfasında, aşağıdaki ayarları belirtin:

    > [!IMPORTANT]
    > HTTPS etkin Web sitesi olan bir yönetim noktanız yoksa, bu ayarı yapılandırmayın. Daha fazla bilgi için bkz. [kurtarma hizmeti](#recovery-service).

    - **BitLocker Management Services 'ı yapılandırma**: Bu ayarı etkinleştirdiğinizde, otomatik olarak Configuration Manager ve site veritabanında anahtar kurtarma bilgilerini sessizce yedekler. Bu ayarı devre dışı bırakır veya yapılandırmazsanız Configuration Manager, anahtar kurtarma bilgilerini kaydetmez.

        - **Depolanacak BitLocker kurtarma bilgilerini seçin**: kurtarma parolasını ve anahtar paketini veya yalnızca kurtarma parolasını kullanacak şekilde yapılandırın.

        - **Kurtarma bilgilerinin düz metin olarak depolanmasına Izin ver**: BitLocker yönetim şifreleme sertifikası olmadan Configuration Manager, anahtar kurtarma bilgilerini düz metin olarak depolar. Daha fazla bilgi için bkz. [kurtarma verilerini şifreleme](encrypt-recovery-data.md).

    Bu sayfadaki bu ve diğer ayarlar hakkında daha fazla bilgi için bkz. [Ayarlar başvurusu-istemci yönetimi](../../tech-ref/bitlocker/settings.md#client-management).

1. Sihirbazı tamamlayın.

Mevcut bir ilkenin ayarlarını değiştirmek için listeden seçin ve **Özellikler**' i seçin.

Birden fazla ilke oluşturduğunuzda, onun göreli önceliğini yapılandırabilirsiniz. Bir istemciye birden çok ilke dağıtırsanız, ayarlarını belirlemede öncelik değeri kullanır.

Sürüm 2006 ' den başlayarak, bu görev için Windows PowerShell cmdlet 'lerini kullanabilirsiniz. Daha fazla bilgi için bkz. [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting).

## <a name="deploy-a-policy"></a>İlke dağıtma

1. **BitLocker yönetim** düğümünde mevcut bir ilkeyi seçin. Şeritte **Dağıt**' ı seçin.

1. Dağıtımın hedefi olarak bir cihaz koleksiyonu seçin.

1. Cihazın sürücüleri istediğiniz zaman şifrelemesine veya şifresini çözmesine istiyorsanız **bakım penceresi dışında düzeltmeye Izin ver**seçeneğini belirleyin. Koleksiyonda herhangi bir bakım penceresi varsa, bu BitLocker ilkesini yine de düzeltir.

1. **Basit** veya **özel** bir zamanlama yapılandırın. İstemci, zamanlamada belirtilen ayarlara göre uyumluluğunu değerlendirir.

1. İlkeyi dağıtmak için **Tamam ' ı** seçin.

Aynı ilkenin birden çok dağıtımını oluşturabilirsiniz. Her dağıtımla ilgili ek bilgileri görüntülemek için **BitLocker yönetim** düğümünde ilkeyi seçin ve ardından Ayrıntılar bölmesinde **dağıtımlar** sekmesine geçin.

> [!IMPORTANT]
> Bir Uzak Masaüstü Protokolü bağlantısı etkinse, MBAMCLIENT BitLocker Sürücü Şifrelemesi eylem başlatamaz. Tüm uzak konsol bağlantıları kapatılmalıdır ve BitLocker Sürücü Şifrelemesi başlamadan önce bir kullanıcının fiziksel konsol oturumunda oturum açması gerekir.

Sürüm 2006 ' den başlayarak, bu görev için Windows PowerShell cmdlet 'lerini kullanabilirsiniz. Daha fazla bilgi için bkz. [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment).

## <a name="monitor"></a>İzleyici

**BitLocker yönetim** düğümünün Ayrıntılar bölmesinde ilke dağıtımıyla ilgili temel uyumluluk istatistiklerini görüntüleyin:

- Uyumluluk sayısı
- Hata sayısı
- Uyumsuzluk sayısı

Uyumluluk yüzdesini ve önerilen eylemi görmek için **dağıtımlar** sekmesine geçin. Dağıtımı seçin ve ardından şeritte **durumu görüntüle**' yi seçin. Bu eylem, görünümü **izleme** çalışma alanına, **dağıtımlar** düğümüne geçirir. Diğer yapılandırma ilkesi dağıtımlarının dağıtımına benzer şekilde, bu görünümde daha ayrıntılı uyumluluk durumu görebilirsiniz.

İstemcilerin BitLocker yönetim ilkesiyle uyumlu olmadığını bildiren nedenleri anlamak için, bkz. [uyumsuzluk kodları](../../tech-ref/bitlocker/non-compliance-codes.md).

Daha fazla sorun giderme bilgisi için bkz. [BitLocker sorunlarını giderme](../../tech-ref/bitlocker/troubleshoot.md).

İzlemek ve sorunlarını gidermek için aşağıdaki günlükleri kullanın:

### <a name="client-logs"></a>İstemci günlükleri

- MBAı olay günlüğü: Windows Olay Görüntüleyicisi, Microsoft > Windows > MBAD > uygulamalar ve hizmetler ' e gidin.  Daha fazla bilgi için bkz. [BitLocker olay günlükleri](../../tech-ref/bitlocker/about-event-logs.md) ve [Istemci olay günlükleri](../../tech-ref/bitlocker/client-event-logs.md)hakkında.

- Varsayılan olarak, istemci günlükleri yolunda **Bitlockermangementhandler. log** `%WINDIR%\CCM\Logs`

### <a name="management-point-logs-recovery-service"></a>Yönetim noktası günlükleri (kurtarma hizmeti)

- Kurtarma hizmeti olay günlüğü: Windows Olay Görüntüleyicisi, Microsoft > Windows > MBAZ-Web > uygulamalar ve hizmetler ' e gidin. Daha fazla bilgi için bkz. [BitLocker olay günlükleri](../../tech-ref/bitlocker/about-event-logs.md) ve [sunucu olay günlükleri](../../tech-ref/bitlocker/server-event-logs.md)hakkında.

- Kurtarma hizmeti izleme günlükleri: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Kurtarma hizmeti

BitLocker kurtarma hizmeti, Configuration Manager istemcilerinden BitLocker kurtarma verilerini alan bir sunucu bileşenidir. Site, bir BitLocker yönetim ilkesi oluşturduğunuzda kurtarma hizmetini dağıtır. Configuration Manager, kurtarma hizmetini her bir yönetim noktasına otomatik olarak HTTPS özellikli bir Web sitesi ile kurar.

Configuration Manager, kurtarma bilgilerini site veritabanına depolar. BitLocker yönetim şifreleme sertifikası olmadan Configuration Manager, anahtar kurtarma bilgilerini düz metin olarak depolar.

Daha fazla bilgi için bkz. [kurtarma verilerini şifreleme](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Geçiş fikirleri

Şu anda Microsoft BitLocker yönetim ve Izleme (MBAD) kullanıyorsanız, yönetimi Configuration Manager 'e sorunsuzca geçirebilirsiniz. BitLocker yönetim ilkelerini Configuration Manager dağıtırken istemciler, kurtarma anahtarlarını ve paketleri Configuration Manager kurtarma hizmetine otomatik olarak yükler.

> [!IMPORTANT]
> Tek başına MBAK 'dan Configuration Manager BitLocker yönetimine geçiş yaptığınızda, tek başına MBAE 'nin mevcut işlevselliğine ihtiyaç duyuyorsanız, tek başına mbaı sunucularını veya bileşenlerini Configuration Manager BitLocker Yönetimi ile birlikte yeniden kullanmayın. Bu sunucuları yeniden kullanırsanız, Configuration Manager BitLocker Yönetimi bileşenlerini bu sunuculara yüklediğinde tek başına MBAD çalışmayı durdurur. Tek başına MBAD sunucularında BitLocker portallarını ayarlamak için MBAMWebSiteInstaller.ps1 betiğini çalıştırmayın. Configuration Manager BitLocker yönetimini ayarlarken ayrı sunucular kullanın.

### <a name="group-policy"></a>Grup İlkesi

- BitLocker yönetim ayarları, MBAD Grup İlkesi ayarlarıyla tamamen uyumludur. Cihazlar hem Grup İlkesi ayarlarını hem de Configuration Manager ilkelerini alıyorsa, bunları eşleşecek şekilde yapılandırın.

  > [!NOTE]
  > Tek başına MBAD için bir Grup İlkesi ayarı varsa, Configuration Manager tarafından denenen eşdeğer ayarı geçersiz kılar. Tek başına MBAD, etki alanı Grup İlkesi 'ni kullanır, Configuration Manager BitLocker Yönetimi için yerel ilkeler ayarlıyor. Etki alanı ilkeleri yerel Configuration Manager BitLocker yönetim ilkelerini geçersiz kılar. Tek başına MBAB etki alanı Grup İlkesi Configuration Manager ilkesiyle eşleşmiyorsa, Configuration Manager BitLocker Yönetimi başarısız olur. Örneğin, bir etki alanı Grup ilkesi, anahtar kurtarma hizmetleri için tek başına MBAı sunucusunu ayarlarsa, Configuration Manager BitLocker Yönetimi yönetim noktası için aynı ayarı ayarlayamıyorum. Bu davranış, istemcilerin kurtarma anahtarlarını yönetim noktasındaki Configuration Manager BitLocker yönetim anahtarı kurtarma hizmetine raporlamasına neden olur.

- Configuration Manager, tüm MBAD Grup İlkesi ayarlarını uygulamaz. Grup İlkesi 'nde ek ayarlar yapılandırırsanız, Configuration Manager istemcilerindeki BitLocker yönetim Aracısı bu ayarları alır.

  > [!IMPORTANT]
  > Configuration Manager BitLocker Management 'ın belirttiği bir ayar için bir grup ilkesi ayarlamamış. Yalnızca Configuration Manager BitLocker yönetiminde mevcut olmayan ayarlar için Grup ilkeleri ayarlayın. Configuration Manager sürüm 2002, tek başına MBAD ile özellik eşliği içerir. Configuration Manager sürüm 2002 ve üzeri sürümlerde, çoğu örnekte, BitLocker ilkelerini yapılandırmak için etki alanı grup ilkelerini ayarlama nedeni olmamalıdır. Çakışma ve sorunları önlemek için, BitLocker için Grup ilkeleri kullanmaktan kaçının. Tüm ayarları Configuration Manager BitLocker yönetim ilkeleri aracılığıyla yapılandırın.

### <a name="tpm-password-hash"></a>TPM Parola karması

- Önceki MBAA istemcileri Configuration Manager için TPM parola karmasını karşıya yüklememe. İstemci yalnızca TPM parola karmasını bir kez yükler.

- Bu bilgileri Configuration Manager kurtarma hizmetine geçirmeniz gerekiyorsa, cihazdaki TPM 'YI temizleyin. Yeniden başlatıldıktan sonra, yeni TPM parola karmasını kurtarma hizmetine yükleyecek.

### <a name="re-encryption"></a>Yeniden şifreleme

Configuration Manager zaten BitLocker Sürücü Şifrelemesi korunan sürücüleri yeniden şifrelemez. Sürücünün geçerli korumasıyla eşleşmeyen bir BitLocker yönetim ilkesi dağıtırsanız, uyumlu değil olarak rapor edin. Sürücü hala korunuyor.

Örneğin, sürücüyü AES-XTS 128 şifreleme algoritması ile şifrelemek için MBAM kullandınız, ancak Configuration Manager ilkesi AES-XTS 256 gerektirir. Sürücü şifrelense de, sürücü ilkeyle uyumlu değil.

Bu davranışı geçici olarak çözmek için, önce cihazda BitLocker 'ı devre dışı bırakın. Ardından yeni ayarlarla yeni bir ilke dağıtın.

## <a name="co-management-and-intune"></a>Ortak yönetim ve Intune

<!-- SCCMDocs#2321 -->

BitLocker için Configuration Manager istemci işleyicisi ortak yönetilebiliyor. Cihaz ortak yönetilmiyorsa ve [Endpoint Protection iş yükünü](../../../comanage/workloads.md#endpoint-protection) Intune 'a geçerseniz, Configuration Manager istemci BitLocker ilkesini yoksayar. Cihaz, Intune 'dan Windows şifreleme ilkesini alır.

> [!NOTE]
> İstenen şifreleme algoritmasının sürdürülmesi sırasında şifreleme yönetimi yetkililerini değiştirmek, istemcide ek eylem gerektirmez. Ancak, şifreleme yönetimi yetkililerini değiştirirseniz ve istenen şifreleme algoritması da değişirse, [yeniden şifrelemeyi](#re-encryption)planlamanız gerekir.

BitLocker 'ı Intune ile yönetme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Intune ile cihaz şifrelemesini kullanma](../../../../intune/protect/encrypt-devices.md)
- [Microsoft Intune 'de BitLocker ilkeleri sorunlarını giderme](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Sonraki adımlar

[BitLocker raporlarını ve portallarını ayarlama](setup-websites.md)
