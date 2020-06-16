---
title: Microsoft Intune | uç nokta güvenlik ilkelerini yönetme | Microsoft Docs
description: Güvenlik yöneticilerinin, Microsoft Endpoint Manager 'daki cihazların güvenlik yapılandırmasına odaklanmak için uç nokta güvenlik ilkelerini ve profillerini nasıl kullanabileceğinizi öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 8b56d902980c9e4b51ccbb62e84b4eccd9eb6395
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776914"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Microsoft Intune uç nokta güvenlik ilkeleriyle cihaz güvenliğini yönetme

Güvenlik Yöneticisi olarak, cihaz yapılandırması profilleri ve güvenlik temelleri ' nde bulunan daha büyük gövdeye ve ayarların aralığına gidilmeden cihaz güvenliğini yapılandırmak için Intune 'un *uç nokta güvenliği* ' nden güvenlik ilkelerini kullanın.

Her ilke türü bir veya daha fazla profili destekler. Profiller, ayarları yapılandırdığınız ve farklı platformlar için ya da daha büyük ilke alanına odaklanabilecek farklı alanlar için ayarları gruplabileceğiniz yerdir.

Bu ilkeleri [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde *Yönet* bölümünde bulabilirsiniz.

![İlkeleri yönetme](./media/endpoint-security-policy/endpoint-security-policies.png)

Her uç nokta güvenlik ilkesi türünün kısa açıklamaları aşağıda verilmiştir. Her biri için kullanılabilir profiller dahil olmak üzere bunlar hakkında daha fazla bilgi edinmek için, her ilke türüne adanmış içeriklere yönelik bağlantıları izleyin:

- [Virüsten](../protect/endpoint-security-antivirus-policy.md) koruma ilkeleri güvenlik yöneticilerinin, yönetilen cihazlar için ayrı virüsten koruma ayarları grubunu yönetmeye odaklanmasına yardımcı olur. Virüsten koruma ilkesini kullanmak için, Intune 'U Microsoft Defender Gelişmiş tehdit koruması (Defender ATP) ile bir mobil tehdit savunma çözümü olarak tümleştirin.

- [Disk şifrelemesi](../protect/endpoint-security-disk-encryption-policy.md) -uç nokta güvenlik diski şifreleme profilleri, yalnızca bir cihaz yerleşik Şifreleme yöntemiyle ilgili olan, filekasası veya BitLocker gibi ayarları odaklamaktadır. Bu odak, güvenlik yöneticilerinin, ilişkisiz ayarların bulunduğu bir konakta gezinmek gerekmeden disk şifreleme ayarlarını yönetmesini kolaylaştırır.

- [Güvenlik duvarı](../protect/endpoint-security-firewall-policy.md) -MacOS ve Windows 10 çalıştıran cihazlar için yerleşik bir güvenlik duvarı yapılandırmak üzere Intune 'daki uç nokta güvenliği güvenlik duvarı ilkesini kullanın. 

- [Uç nokta algılama ve yanıt](../protect/endpoint-security-edr-policy.md) -Defender ATP 'yi Intune ile tümleştirdiğinizde, EDR ayarlarını yönetmek ve CIHAZLARı Defender ATP 'ye eklemek için uç nokta algılama ve yanıt (EDR) için uç nokta güvenlik ilkelerini kullanın.

- [Saldırı yüzeyi azaltma](../protect/endpoint-security-asr-policy.md) -Defender virüsten koruma Windows 10 cihazlarınızda kullanılırken, cihazlarınız için bu ayarları yönetmek üzere saldırı yüzeyi azaltma için Intune uç nokta güvenlik ilkelerini kullanın.

- [Hesap koruması](../protect/endpoint-security-account-protection-policy.md) -hesap koruma ilkeleri, kullanıcılarınızın kimliğini ve hesaplarını korumanıza yardımcı olur. Hesap koruma ilkesi, Windows kimlik ve erişim yönetiminin bir parçası olan Windows Hello ve Credential Guard ayarlarına odaklanır.

Aşağıdaki bölümler tüm uç nokta güvenlik ilkeleri için geçerlidir.

## <a name="create-an-endpoint-security-policy"></a>Uç nokta güvenlik ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Uç nokta güvenliği** ' ni seçin ve ardından yapılandırmak istediğiniz ilke türünü seçin ve ardından **ilke oluştur**' u seçin. Aşağıdaki ilke türlerinden birini seçin:
   - Virüsten Koruma
   - Disk şifrelemesi
   - Güvenlik duvarı
   - Uç nokta algılama ve yanıt
   - Saldırı yüzeyini azaltma
   - Hesap koruması

3. Aşağıdaki özellikleri girin:
   - **Platform**: ilke oluşturmakta olduğunuz platformu seçin. Kullanılabilir seçenekler, seçtiğiniz ilke türüne bağlıdır:
     - Mac OS
     - Windows 10 ve üzeri
   - **Profil**: seçtiğiniz platform için kullanılabilir profiller arasından seçim yapın. Profiller hakkında daha fazla bilgi için, seçtiğiniz ilke türü için bu makaledeki adanmış bölümüne bakın.

4. **Oluştur**'u seçin.

5. **Temel bilgiler** sayfasında, profil için bir ad ve açıklama girin ve ardından **İleri**' yi seçin.

6. **Yapılandırma ayarları** sayfasında, her bir ayar grubunu genişletin ve bu profille yönetmek istediğiniz ayarları yapılandırın.

   Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin.

7. **Kapsam etiketleri sayfasında,** kapsam etiketlerini profile atamak için kapsam etiketlerini **Seç** ' *i seçin.*
  
   Devam etmek için **İleri**’yi seçin.

8. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

   **İleri**’yi seçin.

9. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

## <a name="duplicate-a-policy"></a>Bir ilkeyi çoğaltın

Uç nokta güvenlik ilkeleri, özgün ilkenin bir kopyasını oluşturmak için yinelemeyi destekler. Bir ilke çoğaltılırken bir senaryo yararlı olduğunda, farklı gruplara benzer ilkeler atamanız ve tüm ilkeyi el ile yeniden oluşturmak istemeniz gerekir. Bunun yerine, özgün ilkeyi çoğaltabilir ve sonra yalnızca yeni ilke için gereken değişiklikleri getirebilirsiniz. Yalnızca belirli bir ayarı ve ilkenin atandığı grubu değiştirebilirsiniz.

Bir yinelenen oluştururken, kopyaya yeni bir ad verirsiniz. Kopya, orijinalle aynı ayar yapılandırmalarında ve kapsam etiketleriyle yapılır, ancak herhangi bir atamalara sahip olmayacaktır. Atamalar oluşturmak için yeni ilkeyi daha sonra düzenlemeniz gerekir.  

Aşağıdaki ilke türleri yinelemeyi destekler:

- Virüsten Koruma
- Disk şifrelemesi
- Güvenlik duvarı
- Uç nokta algılama ve yanıt
- Saldırı yüzeyini azaltma
- Hesap koruması

Yeni ilkeyi oluşturduktan sonra, yapılandırmasında değişiklik yapmak için ilkeyi gözden geçirin ve düzenleyin.

### <a name="to-duplicate-a-policy"></a>Bir ilkeyi yinelemek için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. Kopyalamak istediğiniz ilkeyi seçin. Sonra, **Çoğalt** ' ı seçin veya ilkenin sağ tarafındaki üç nokta (**...**) simgesini seçin ve **Çoğalt**' ı seçin.
3. İlke için **Yeni bir ad** girin ve ardından **Kaydet**' i seçin.

### <a name="to-edit-a-policy"></a>Bir ilkeyi düzenlemek için

1. Yeni ilkeyi seçin ve ardından **Özellikler**' i seçin.
2. İlkedeki yapılandırma ayarlarının listesini genişletmek için ayarlar ' ı seçin. Bu görünümden ayarları değiştiremezsiniz, ancak bunların nasıl yapılandırıldığını inceleyebilirsiniz.
3. İlkeyi değiştirmek için, değişiklik yapmak istediğiniz her kategori için **Düzenle** ' yi seçin:
   - Temel Bilgiler
   - Atamalar
   - Kapsam etiketleri
   - Yapılandırma ayarları
4. Değişiklikleri yaptıktan sonra, düzenlemelerinizi kaydetmek için **Kaydet** ' i seçin.  Ek kategorilerde düzenlemeler oluşturabilmeniz için önce bir kategoride yapılan düzenlemelerin kaydedilmesi gerekir.

## <a name="manage-conflicts"></a>Çakışmaları yönetme

Uç nokta güvenlik ilkeleriyle (güvenlik ilkeleri) yönetebileceğiniz cihaz ayarlarının birçoğu Intune 'daki diğer ilke türleri aracılığıyla yönetebilirsiniz. Bu diğer ilke türleri *cihaz yapılandırma* ilkesi ve *güvenlik temellerini*içerir. Birden çok farklı ilke türüyle veya aynı ilke türünde birden çok örneğe sahip bir ayarı yönetebilmeniz için, ilke çakışmalarını belirleyip çözecek bir cihaz, bekleyen yapılandırmalara bağlı kalmamalıdır.

- Güvenlik temelleri, bir ayar için varsayılan olmayan bir değer ayarlayarak taban çizgisi adreslerinin önerilen yapılandırmasına uyum sağlar.
- Uç nokta güvenlik ilkeleri de dahil olmak üzere diğer ilke türleri varsayılan olarak *yapılandırılmamış* bir değer ayarlar. Bu diğer ilke türleri, ilkedeki ayarları açıkça yapılandırmanızı gerektirir.

İlke yönteminden bağımsız olarak, aynı cihazdaki aynı ayarı birden çok ilke türü aracılığıyla veya aynı ilke türünün birden çok örneği aracılığıyla yönetmek, kaçınılması gereken çakışmaların oluşmasına neden olabilir.

Aşağıdaki bağlantılardaki bilgiler, çakışmaları belirlemenize ve çözmenize yardımcı olabilir:

- [Intune'da ilke ve profil sorunları giderme](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Güvenlik temellerinizi izleyin](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Sonraki adımlar

[Intune 'da Endpoint Security 'yi yönetme](../protect/endpoint-security.md)
