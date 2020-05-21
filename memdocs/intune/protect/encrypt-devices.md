---
title: Intune 'da Windows 10 cihazlarını BitLocker ile şifreleme
titleSuffix: Microsoft Intune
description: Cihazları BitLocker yerleşik Şifreleme yöntemiyle şifreleyin ve bu şifrelenmiş cihazların kurtarma anahtarlarını Intune portalı içinden yönetin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 8d84e8d92ba483e96a1e78da0566d2e8a389e403
ms.sourcegitcommit: 5d32dd481e2a944465755ce74e14c835cce2cd1c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551904"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Intune 'da Windows 10 için BitLocker ilkesini yönetme

Windows 10 çalıştıran cihazlarda BitLocker Sürücü Şifrelemesi yapılandırmak için Intune 'u kullanın.

BitLocker, Windows 10 veya üzerini çalıştıran cihazlarda kullanılabilir. BitLocker için bazı ayarlar cihazın desteklenen bir TPM 'ye sahip olmasını gerektirir.

Yönetilen cihazlarınızda BitLocker 'ı yapılandırmak için aşağıdaki ilke türlerinden birini kullanın

- **[Windows 10 BitLocker Için uç nokta güvenlik diski şifreleme ilkesi](#create-an-endpoint-security-policy-for-bitlocker)**. *Uç nokta güvenliği* içindeki BitLocker profili, BitLocker 'ı yapılandırmak için ayrılmış olan odaklanmış bir ayar grubudur.

  [Disk şifreleme ilkesi 'Nden BitLocker profillerinde](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)kullanılabilir olan BitLocker ayarlarını görüntüleyin.

- **[Windows 10 BitLocker için Endpoint Protection Için cihaz yapılandırma profili](#create-an-endpoint-security-policy-for-bitlocker)**. BitLocker ayarları, Windows 10 Endpoint Protection için kullanılabilir ayarlar kategorilerinden biridir.

  [Endpoint Protection profilleri form cihaz yapılandırma Ilkesinde BitLocker](../protect/endpoint-protection-windows-10.md#windows-settings)Için kullanılabilir BitLocker ayarlarını görüntüleyin.

> [!TIP]
> Intune, cihazların şifreleme durumu hakkındaki ayrıntıları, tüm yönetilen cihazlarınızda sunan yerleşik bir [şifreleme raporu](encryption-monitor.md) sağlar. Intune bir Windows 10 cihazını BitLocker ile şifreledikten sonra, şifreleme raporunu görüntülerken BitLocker kurtarma anahtarlarını görüntüleyebilir ve alabilirsiniz.
>
> Ayrıca, Azure Active Directory (Azure AD) içinde bulunan ve cihazlarınızdan BitLocker için önemli bilgilere erişebilirsiniz.
tüm yönetilen cihazlarınızda cihazların şifreleme durumu hakkında ayrıntılı bilgi sunan [şifreleme raporu](encryption-monitor.md) .

## <a name="permissions-to-manage-bitlocker"></a>BitLocker 'ı yönetme izinleri

Intune 'da BitLocker 'ı yönetmek için hesabınızın ilgili Intune [rol tabanlı erişim denetimi](../fundamentals/role-based-access-control.md) (RBAC) izinlerine sahip olması gerekir.

Aşağıda, uzak görevler kategorisinin bir parçası olan BitLocker izinleri ve izin veren yerleşik RBAC rolleri verilmiştir:

- **BitLocker anahtarlarını döndür**
  - Yardım Masası Işleci

## <a name="create-and-deploy-policy"></a>İlke oluşturma ve dağıtma

Tercih ettiğiniz ilke türünü oluşturmak için aşağıdaki yordamlardan birini kullanın.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>BitLocker için uç nokta güvenlik ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **disk şifrelemesi**  >  **ilke oluştur**' u seçin.

3. Aşağıdaki seçenekleri ayarlayın:
   1. **Platform**: Windows 10 veya üzeri
   2. **Profil**: BitLocker

   ![BitLocker profilini seçin](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. **Yapılandırma ayarları** sayfasında, BitLocker 'ın ayarlarını iş gereksinimlerinizi karşılayacak şekilde yapılandırın.  

   BitLocker 'ı sessizce etkinleştirmek istiyorsanız, bu makalede daha fazla önkoşul ve kullanmanız gereken belirli ayar yapılandırmalarının yanı sıra [cihazlarda BitLocker 'ı sessizce etkinleştirme](#silently-enable-bitlocker-on-devices)bölümüne bakın.

   **İleri**’yi seçin.

5. Scope **(Etiketler)** sayfasında kapsam etiketleri **Seç** ' i seçerek profile kapsam etiketleri atayın.

   Devam etmek için **İleri**’yi seçin.

6. **Atamalar** sayfasında, bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. Kullanıcı ve cihaz profilleri atama.

   **İleri**’yi seçin.

7. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>BitLocker için bir cihaz yapılandırma profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.

3. Aşağıdaki seçenekleri ayarlayın:
   1. **Platform**: Windows 10 ve üzeri
   2. **Profil türü**: Endpoint Protection

   ![BitLocker profilini seçin](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. **Ayarlar**  >  **Windows şifrelemesi**' ni seçin.

   ![BitLocker ayarları](./media/encrypt-devices/bitlocker-settings.png)

5. BitLocker ayarlarını, iş gereksinimlerinizi karşılayacak şekilde yapılandırın.

   BitLocker 'ı sessizce etkinleştirmek istiyorsanız, bu makalede daha fazla önkoşul ve kullanmanız gereken belirli ayar yapılandırmalarının yanı sıra [cihazlarda BitLocker 'ı sessizce etkinleştirme](#silently-enable-bitlocker-on-devices)bölümüne bakın.

6. **Tamam**’ı seçin.

7. Ek ayarların yapılandırmasını tamamladıktan sonra profili kaydedin.

## <a name="manage-bitlocker"></a>seçin,

BitLocker ilkesi alan cihazlarla ilgili bilgileri görüntülemek için bkz. [disk şifrelemeyi izleme](../protect/encryption-monitor.md). Ayrıca, şifreleme raporunu görüntülerken BitLocker kurtarma anahtarlarını görüntüleyebilir ve alabilirsiniz.

### <a name="silently-enable-bitlocker-on-devices"></a>Cihazlarda BitLocker 'ı sessizce etkinleştirin

Bir cihazda BitLocker 'ı otomatik olarak ve sessizce etkinleştirmenizi sağlayan bir BitLocker ilkesi yapılandırabilirsiniz. Diğer bir deyişle, bu kullanıcı cihazda yerel yönetici olmasa bile, BitLocker son kullanıcıya herhangi bir kullanıcı ARABIRIMI sunmadan başarıyla etkinleştirilir.

**Cihaz önkoşulları**:

Bir cihazın BitLocker 'ı sessizce etkinleştirmek için uygun olması için aşağıdaki koşullara uyması gerekir:

- Cihazın Windows 10 sürüm 1809 veya üstünü çalıştırması gerekir
- Cihazın Azure AD 'ye katılmış olması gerekir  

**BitLocker ilke yapılandırması**:

BitLocker *temel ayarları* için aşağıdaki Iki ayar BitLocker ilkesinde yapılandırılmalıdır:

- **Diğer disk şifrelemesi**  =  için uyarı *Engelle*.
- **Standart kullanıcıların Azure AD katılımı sırasında şifrelemeyi etkinleştirmesine Izin ver**  =  *Izin ver*

BitLocker ilkesi, bir başlangıç PIN 'ı veya başlangıç anahtarı kullanımını **gerektirmemelidir** . TPM başlangıç PIN 'ı veya başlangıç anahtarı *gerektiğinde*, BitLocker sessizce etkinleştirilemez ve son kullanıcıdan etkileşim gerektirir.  Bu gereksinim, aynı ilkedeki aşağıdaki üç *BitLocker işletim sistemi sürücü ayarı* aracılığıyla karşılanır:

- **Uyumlu TPM başlangıç PIN 'ı** *TPM Ile başlangıç PIN 'i gerektirecek* şekilde ayarlanmamış olmalıdır
- **Uyumlu TPM başlangıç anahtarı** *TPM Ile başlangıç anahtarı gerektirecek* şekilde ayarlanmamış olmalıdır
- **Uyumlu TPM başlangıç anahtarı ve PIN 'ı** *TPM ile başlangıç anahtarı ve PIN gerektirecek* şekilde ayarlanmamış olmalıdır

### <a name="view-details-for-recovery-keys"></a>Kurtarma anahtarlarının ayrıntılarını görüntüleme

Intune, Windows 10 cihazlarınızın BitLocker anahtar kimliklerini ve kurtarma anahtarlarını Intune portalından görüntüleyebilmeniz için BitLocker için Azure AD dikey penceresine erişim sağlar. Erişilebilir olması için cihazın, Azure AD 'ye yönelik anahtarları olması gerekir.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazlar**  >  **tüm cihazlar**' ı seçin.

3. Listeden bir cihaz seçin ve ardından *izleyici*altında **kurtarma anahtarları**' nı seçin.
  
   Azure AD 'de anahtarlar kullanılabilir olduğunda aşağıdaki bilgiler kullanılabilir:
   - BitLocker anahtar KIMLIĞI
   - BitLocker kurtarma anahtarı
   - Sürücü Türü

   Anahtarlar Azure AD 'de olmadığında, Intune *Bu cihaz Için hiçbir BitLocker anahtarı bulunamadığını*gösterir.

BitLocker için bilgi, [BitLocker yapılandırma hizmeti sağlayıcısı](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) (CSP) kullanılarak elde edilir. BitLocker CSP, Windows 10 sürüm 1703 ve üzeri sürümlerde ve Windows 10 Pro sürüm 1809 ve üzeri sürümlerde desteklenir.

### <a name="rotate-bitlocker-recovery-keys"></a>BitLocker kurtarma anahtarlarını döndür

Windows 10 sürüm 1909 veya üstünü çalıştıran bir cihazın BitLocker kurtarma anahtarını uzaktan döndürmek için bir Intune cihaz eylemini kullanabilirsiniz.

#### <a name="prerequisites"></a>Ön koşullar

Cihazların BitLocker kurtarma anahtarının döndürmesini desteklemek için aşağıdaki önkoşulları karşılaması gerekir:

- Cihazların Windows 10 sürüm 1909 veya üstünü çalıştırması gerekir

- Azure AD 'ye katılmış ve Hibriya katılmış cihazlarda anahtar döndürme özelliğinin etkinleştirilmesi için destek bulunmalıdır:

  - **İstemci tabanlı kurtarma parolası döndürme**

  Bu ayar, Windows 10 Endpoint Protection cihaz yapılandırma ilkesinin bir parçası olarak *Windows şifrelemesi* altında bulunur.

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>BitLocker kurtarma anahtarını döndürmek için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazlar**  >  **tüm cihazlar**' ı seçin.

3. Yönettiğiniz cihazların listesinde bir cihaz seçin, **daha fazla**' yı seçin ve ardından **BitLocker anahtar döndürme** cihazı uzak eylemi ' ni seçin.

4. Cihazın **genel bakış** sayfasında **BitLocker anahtar dönüşü**' ni seçin. Bu seçeneği görmüyorsanız ek seçenekleri göstermek için üç nokta (**...**) simgesini seçin ve ardından **BitLocker anahtar döndürme** cihazı uzak eylemini seçin.

   ![Daha fazla seçenek görüntülemek için üç noktayı seçin](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Sonraki adımlar

[FileVault ilkesini yönetme](../protect/encrypt-devices-filevault.md)

[Disk şifrelemesini yönetme](../protect/encryption-monitor.md)
