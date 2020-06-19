---
title: Android için uygulama SDK 'Sı geliştirici test Kılavuzu Microsoft Intune
description: Android için Microsoft Intune uygulama SDK 'Sı test Kılavuzu, Intune ile yönetilen Android uygulamanızı test etmenize yardımcı olur.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd4ece62215d48f3481923e099feecc992d7aa6d
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093374"
---
# <a name="microsoft-intune-app-sdk-for-android-developers-testing-guide"></a>Android için Microsoft Intune uygulama SDK 'Sı geliştiriciler test Kılavuzu

Android için Microsoft Intune uygulama SDK 'Sı test Kılavuzu, Intune ile yönetilen Android uygulamanızı test etmenize yardımcı olmak için tasarlanmıştır.

## <a name="demo-tenant-setup"></a>Tanıtım kiracı kurulumu
Şirketiniz ile zaten bir kiracınız yoksa önceden oluşturulmuş verilerle veya olmadan bir tanıtım kiracısı oluşturabilirsiniz. Microsoft CDX erişimi için bir [Microsoft iş ortağı](https://partner.microsoft.com/en-us/business-opportunities/why-microsoft) olarak kaydolmanız gerekir. Yeni bir hesap oluşturmak için:
1. [Microsoft CDX kiracı oluşturma sitesine](https://cdx.transform.microsoft.com/my-tenants/create-tenant) gidin ve bir Microsoft 365 Kurumsal kiracı oluşturun.
2. [Intune](../fundamentals/setup-steps.md) 'u mobil cihaz YÖNETIMI (MDM) etkinleştirecek şekilde ayarlayın.
3. [Kullanıcı oluşturun](../fundamentals/users-add.md).
4. [Grupları oluşturun](../fundamentals/groups-add.md).
5. Test testiniz için uygun şekilde [lisans atayın](../fundamentals/licenses-assign.md) .


## <a name="azure-portal-policy-configuration"></a>Azure portal ilkesi yapılandırması
[Azure Portal Intune dikey](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview)penceresinde [Uygulama koruma ilkeleri oluşturun ve atayın](../apps/app-protection-policies.md) . Ayrıca, Intune dikey penceresinde [uygulama yapılandırma ilkenizi](../apps/app-configuration-policies-overview.md) oluşturup atayabilirsiniz.

> [!NOTE]
> Uygulamanız Azure portal listelenmemişse, **daha fazla uygulama** seçeneğini belirleyerek ve metin kutusunda paket adını sağlayarak bu ilkeyi bir ilkeyle hedefleyebilirsiniz.

## <a name="test-cases"></a>Test Çalışmaları

Aşağıdaki test çalışmaları yapılandırma ve onay adımları sağlar. Yeni tümleşik Android uygulamanızı doğrulamak için bu testleri kullanın.

### <a name="required-pin-and-corporate-credentials"></a>Gerekli PIN ve şirket kimlik bilgileri

Şirket kaynaklarına erişmek için PIN 'ı zorunlu kılabilirsiniz. Ayrıca, kullanıcıların yönetilen uygulamaları kullanabilmesi için önce şirket kimlik doğrulamasını uygulayabilirsiniz. Bunu yapmak için:

1. **Erişim IÇIN PIN gerektir** ' i ayarlayın ve **Evet**' e **erişmek için kurumsal kimlik bilgileri gerektir** . Daha fazla bilgi için, bkz. [Microsoft Intune Android uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-android.md#access-requirements).
2. Aşağıdaki koşulları onaylayın:
    - Uygulama başlatma, PIN girişi veya Şirket Portalı kayıt sırasında kullanılan üretim kullanıcısı için bir istem sunmalıdır.
    - Geçerli bir oturum açma istemi sunamaması, özellikle Azure Active Directory kimlik doğrulaması kitaplığı (ADAL) Tümleştirmesi (SkipBroker, ClientID ve Authority) için değerler olarak yanlış yapılandırılmış bir Android bildiriminin nedeni olabilir.
    - Herhangi bir istem sunma hatası, yanlış tümleşik bir değerden kaynaklanıyor olabilir `MAMActivity` . Hakkında daha fazla bilgi için `MAMActivity` bkz. [Android için uygulama SDK 'sı geliştirici kılavuzu Microsoft Intune](app-sdk-android.md).

> [!NOTE] 
> Önceki test çalışmıyorsa, aşağıdaki testler de başarısız olur. [SDK](app-sdk-android.md#sdk-integration) ve [adal](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal) tümleştirmesini gözden geçirin.

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>Diğer uygulamalarla veri aktarımını ve almayı kısıtlama
Kurumsal yönetilen uygulamalar arasında veri aktarımını şu şekilde denetleyebilirsiniz:

1. **Uygulamanın diğer uygulamalara veri aktarmasına Izin ver** **ilkesini ilkeyle yönetilen uygulamalar**olarak ayarlayın.
2. **Uygulamanın diğer uygulamalardan tüm uygulamalara veri almasına Izin ver** ' **All apps**i ayarlayın. 

Amaç ve içerik sağlayıcılarının kullanımı, bu ilkelerden etkilenir.
3. Aşağıdaki koşulları onaylayın:
    - Yönetilmeyen bir uygulamadan uygulama işlevlerinizi doğru açma.
    - Uygulamanız ve yönetilen uygulamalar arasında içerik paylaşımına izin verilir.
    - Uygulamanızdan Yönetilemeyen uygulamalara (örneğin, Chrome) paylaşım engellenir.


#### <a name="restrict-receiving-data-from-other-apps"></a>Diğer uygulamalardan veri almayı kısıtla

1. **Kuruluş verilerini diğer uygulamalara** **tüm uygulamalara**Gönder ' i ayarlayın.
2. Diğer uygulamalardan **ilkeyle yönetilen uygulamalara** **veri al** ' a ayarlayın. 
3. Aşağıdaki koşulları onaylayın:
    - Uygulama işlevinizden yönetilmeyen bir uygulamaya doğru gönderme.
    - Uygulamanız ve yönetilen uygulamalar arasında içerik paylaşımına izin verilir.
    - Yönetilmeyen uygulamalardan (örneğin, Chrome) uygulamanıza paylaşılması engellenir.

Uygulamanız [Tümleşik ' açık ' denetimleri](app-sdk-android.md#opening-data-from-a-local-or-cloud-storage-location)gerektiriyorsa, **açma** işlevini aşağıdaki şekilde denetleyebilirsiniz:

1. Diğer uygulamalardan **ilkeyle yönetilen uygulamalara** **veri al** ' a ayarlayın. 
2. Açık verileri, **engellemek**için **kuruluş belgelerine** ayarlayın. 
3. Aşağıdaki koşulları onaylayın:
    - Açmak yalnızca uygun yönetilen konumlara kısıtlıdır.

### <a name="restrict-cut-copy-and-paste"></a>Kesme, kopyalama ve yapıştırmayı kısıtla
Sistem panosunu yönetilen uygulamalarla kısıtlamak için aşağıdaki adımları kullanabilirsiniz:

1. **' In yapıştırma ile yönetilen ilkeye** **, diğer uygulamalarla kesme, kopyalama ve yapıştırmayı Kısıtla seçeneğini** belirleyin.
2. Aşağıdaki koşulları onaylayın:
    - Uygulamanızdan yönetilmeyen bir uygulamaya (örneğin, Iletiler) metin kopyalama engellenir.

### <a name="prevent-save"></a>Kaydetmeyi engelle
Uygulamanız [Tümleşik farklı kaydet denetimleri](app-sdk-android.md#example-data-transfer-between-apps-and-device-or-cloud-storage-locations)gerektiriyorsa, farklı **Kaydet** işlevlerini aşağıdaki şekilde denetleyebilirsiniz:

1. **' Farklı Kaydet '** ayarını **Evet**olarak belirleyin.
2. Aşağıdaki koşulları onaylayın:
    - Kaydet yalnızca uygun yönetilen konumlara kısıtlıdır.

### <a name="file-encryption"></a>Dosya şifreleme
Aygıttaki verileri aşağıdaki gibi şifreleyebilirsiniz:

1. **Uygulama verilerini şifreleyin** ' i **Evet**olarak ayarlayın.
2. Aşağıdaki koşulları onaylayın:
    - Normal uygulama davranışı etkilenmez.

### <a name="prevent-android-backups"></a>Android yedeklemelerini engelle
Uygulama yedeklemesini aşağıdaki şekilde kontrol edebilirsiniz:

1. [Tümleşik yedekleme kısıtlamaları](app-sdk-android.md#protecting-backup-data)ayarladıysanız, **Android yedeklemelerini** **Evet**olarak ayarlayın seçeneğini belirleyin.
2. Aşağıdaki koşulları onaylayın:
    - Yedeklemeler kısıtlıdır.

### <a name="wipe"></a>Silme
Yönetilen uygulamaları, şirket e-posta ve belgelerinin bulunduğu yerden uzaktan silebilirsiniz. Kişisel verilerin şifresi artık yönetildiğinde çözülür. Bunu yapmak için:

1. Azure portal, [silme](../apps/apps-selective-wipe.md)işlemi yapın.
2. Uygulamanız herhangi bir silme işleyicisine kaydolmazsa, aşağıdaki koşulları onaylayın:
    - Uygulamanın tam temizleme işlemi gerçekleşir.
3. Uygulamanız veya için kaydedilmişse `WIPE_USER_DATA` `WIPE_USER_AUXILARY_DATA` , aşağıdaki koşulları onaylayın:
    - Yönetilen içerik uygulamadan kaldırılır. Daha fazla bilgi için bkz. [Android Için Intune uygulama SDK 'sı Geliştirici Kılavuzu-seçmeli silme](app-sdk-android.md#selective-wipe).

### <a name="multi-identity-support"></a>Çoklu kimlik desteği
[Çoklu kimlik desteğini](app-sdk-android.md#multi-identity-optional) tümleştirme, kapsamlı bir şekilde test olması gereken yüksek riskli bir değişiklik. En yaygın sorunlar, etkin kimliğin ( `Context` iş parçacığı düzeyi) veya düzgün bir şekilde izleme dosya kimliklerinin () düzgün bir şekilde ayarlanması nedeniyle oluşur `MAMFileProtectionManager` .

En düşük düzeyde, aşağıdakileri onaylayın:

- **Farklı kaydet** ilkesi, Yönetilen kimlikler için doğru şekilde çalışıyor.
- Kopyalama ve yapıştırma kısıtlamaları, yönetilene doğru şekilde uygulanır.
- Yalnızca yönetilen kimliğe ait veriler şifrelenir ve kişisel dosyalar değiştirilmez.
- Kayıt kaldırma sırasında seçmeli Temizleme yalnızca yönetilen kimlik verilerini kaldırır.
- Yönetilmeyen bilgisayardan yönetilen bir hesaba (yalnızca ilk kez) değiştirilirken, son kullanıcıdan koşul başlatması istenir.

### <a name="app-configuration-optional"></a>Uygulama yapılandırması (isteğe bağlı)
Yönetilen uygulamaların davranışını yapılandırabilirsiniz. Uygulamanız herhangi bir uygulama yapılandırma ayarını kullanıyorsa, uygulamanızın sizin (yönetici olarak) ayarlayabileceğiniz tüm değerleri doğru bir şekilde işlediğini test etmelisiniz. Intune 'da [uygulama yapılandırma ilkeleri](../apps/app-configuration-policies-overview.md) oluşturabilir ve atayabilirsiniz.


