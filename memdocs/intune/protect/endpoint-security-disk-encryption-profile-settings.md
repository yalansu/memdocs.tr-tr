---
title: Intune Endpoint Security disk şifrelemesi ilke ayarları | Microsoft Docs
description: Microsoft Intune 'de BitLocker ve Filekasası için uç nokta güvenlik diski şifreleme ilkesi ayarları
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 3760aa9820495db6c2460bf2e6d2e9a08d705a10
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462040"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için disk şifreleme ilkesi ayarları

Bir [uç nokta güvenlik ilkesinin](../protect/endpoint-security-policy.md)parçası olarak, Intune 'un uç nokta güvenlik düğümündeki *disk şifreleme* ilkesi profilleri ' nde yapılandırabileceğiniz ayarları görüntüleyin.

Desteklenen platformlar ve profiller:

- **macOS**:
  - Profil: **Dosya Kasası**
- **Windows 10 ve üzeri**:
  - Profil: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Şifreleme

**Dosya kasasını etkinleştir**  
- **Yapılandırılmadı** (*varsayılan*)
- **Evet** -macos 10,13 ve üstünü çalıştıran cihazlarda FILEKASASıYLA XTS-AES 128 kullanarak tam disk şifrelemeyi etkinleştirin. Kullanıcı cihazda oturumu kapattığında Filekasası etkinleştirilir.

  *Evet*olarak ayarlandığında, filekasası için ek ayarlar yapılandırabilirsiniz.

  - **Kurtarma anahtarı türü** 
     Cihazlar için *kişisel anahtar* kurtarma anahtarları oluşturulur. Kişisel anahtar için aşağıdaki ayarları yapılandırın:

    - **Kişisel kurtarma anahtarı döndürme**  
      Bir cihaz için kişisel kurtarma anahtarının ne sıklıkta döndürüleceğini belirtin. **Yapılandırılmadı**' dan varsayılan değeri veya **1** ile **12** ay arasında bir değer seçebilirsiniz.
    - **Emanet kişisel kurtarma anahtarının konum açıklaması**  
      Kullanıcıya kişisel kurtarma anahtarını nasıl alabilecekleri hakkında daha kısa bir ileti belirtin. Kullanıcı, parola unutursa kişisel kurtarma anahtarını girmeniz istendiğinde bu iletiyi oturum açma ekranında görür.

  - **Atlayakaç kez izin verilir**  
    Kullanıcının oturum açması için dosya kasasından önce dosya kasasını etkinleştirmek üzere bir kullanıcının istekleri yoksaymasına izin sayısını belirleyin.
    - **Yapılandırılmadı** (*varsayılan*)-bir sonraki oturum açma işlemine izin verilmesi için cihazda şifreleme gerekir.
    - **1** ila **10** -bir kullanıcının cihazda şifrelemeyi gerektirmeden önce 1 ila 10 kez istemi yoksaymasına izin verin.
    - **Sınır yok, her zaman sor** -kullanıcıdan filekasayı etkinleştirmesi istenir, ancak şifreleme hiçbir zaman gerekli değildir.

  - **Oturum açana kadar ertelemeyi izin ver**  
    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -Kullanıcı oturumu kapatana kadar filekasasını etkinleştirmek için istemi erteleyin.  

  - **Oturumu kapatmak için istemi devre dışı bırak**  
    Kullanıcıdan oturum açtıklarında dosya kasasını etkinleştirdikleri isteyen kullanıcıya sorma işlemini engelleyin. Devre dışı olarak ayarlandığında, oturum kapatma istemi devre dışı bırakılır ve bunun yerine kullanıcıya oturum açtıklarında sorulur.
    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -oturum kapatma sırasında görünen dosya kasasını etkinleştirmek için istemi devre dışı bırakın.

  - **Kurtarma anahtarını gizle**  
     Şifreleme sırasında macOS cihazının kullanıcısının kişisel kurtarma anahtarını gizleyin. Disk şifrelendikten sonra, Kullanıcı Intune Şirket Portalı Web sitesi veya şirket portalı uygulaması aracılığıyla kişisel kurtarma anahtarını görüntülemek için herhangi bir cihazı kullanabilir.
    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -cihaz şifreleme sırasında kişisel kurtarma anahtarını gizleyin.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker – temel ayarlar

- **İşletim sistemi ve sabit veri sürücüleri için tam disk şifrelemesini etkinleştir**  
  CSP: [Requiredeviceencryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Bu ilke uygulanmadan önce sürücü şifrelendiyse, ek bir eylem yapılmaz. Şifreleme yöntemi ve seçenekleri bu ilkeyle eşleşiyorsa, yapılandırma başarılı döndürmelidir. Yerinde bir BitLocker yapılandırma seçeneği bu ilkeyle eşleşmezse, yapılandırma muhtemelen bir hata döndürür.
  
  Bu ilkeyi zaten şifrelenmiş bir diske uygulamak için sürücünün şifresini çözün ve MDM ilkesini yeniden uygulayın. Windows varsayılan, BitLocker Sürücü Şifrelemesi gerektirmemelidir. Ancak, Azure AD 'ye katılması ve Microsoft hesabı (MSA) kaydı/oturum açma otomatik şifrelemesi, XTS-AES 128-bit Şifrelemeli BitLocker 'ı etkinleştirmek için uygulanabilir.

  - **Yapılandırılmadı** (*varsayılan*)-BitLocker zorlaması gerçekleşmez.
  - **Evet** -BitLocker kullanımını zorunlu kıl.

- **Depolama kartlarının şifrelenmesini gerektir (yalnızca mobil)**  
  CSP: [Requirestooygecardencryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Bu ayar yalnızca Windows Mobile ve mobil kurumsal SKU cihazları için geçerlidir.
  - **Yapılandırılmadı** (*varsayılan*)-ayar, depolama kartı şifrelemesi gerektirmeyen işletim sistemi varsayılana döner.
  - **Evet** -depolama kartlarında şifreleme, mobil cihazlar için gereklidir.

- **Üçüncü taraf şifreleme hakkında istemi gizle**  
  CSP: [Allowwarningforotherdiskencryption](https://go.microsoft.com/fwlink/?linkid=872525)

  BitLocker, üçüncü taraf bir şifreleme ürünü tarafından zaten şifrelenmiş bir sistemde etkinleştirildiyse, cihazı kullanılamaz olarak işleyebilir. Veri kaybı oluşabilir ve Windows 'u yeniden yüklemeniz gerekebilir. Üçüncü taraf şifrelemenin yüklü veya etkin olduğu bir cihazda BitLocker 'ı hiçbir şekilde etkinleştirmek kesinlikle önerilir.

  Varsayılan olarak, BitLocker kurulum Sihirbazı kullanıcılardan bir üçüncü taraf şifreleme olmadığını onaylamasını ister.

  - **Yapılandırılmadı** (*varsayılan*) – BitLocker kurulum Sihirbazı bir uyarı görüntüler ve kullanıcılardan üçüncü taraf şifrelemenin mevcut olmadığını onaylamasını ister.
  - **Evet** -kullanıcılardan BitLocker kurulum sihirbazları isteğini gizleyin.

  BitLocker sessiz etkinleştirme özellikleri gerekliyse, gerekli istem sessiz etkinleştirme iş akışlarını bozken, üçüncü taraf şifreleme uyarısı gizli olmalıdır.

  *Evet*olarak ayarlandığında, aşağıdaki ayarı yapılandırabilirsiniz:

  - **Autopilot sırasında standart kullanıcıların şifrelemeyi etkinleştirmesine izin ver**  
    CSP: [Allowstandarduserencryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Yapılandırılmadı** (*varsayılan*) – Azure Active Directory JOIN (asıfatı) sessiz etkinleştirme senaryolarında, kullanıcıların BitLocker 'ı etkinleştirmek için yerel Yöneticiler olması gerekmez.
    - **Evet** -ayar, istemci varsayılan olarak bırakılır, bu, BitLocker 'ı etkinleştirmek için yerel yönetici erişimi gerektirir.

    Sessiz olmayan etkinleştirme ve Autopilot senaryoları için, kullanıcının BitLocker kurulum Sihirbazı 'nı tamamlaması için bir yerel yönetici olması gerekir.

- **İçin istemci odaklı kurtarma parolasını etkinleştir**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Iş hesabı ekleme (AWA, resmi olmayan Iş yeri) cihazları, anahtar döndürme için desteklenmez.
  - **Yapılandırılmadı** (*varsayılan*) – istemci, BitLocker kurtarma anahtarlarını döndürmez.
  - **Devre dışı**
  - **Azure AD 'ye katılmış cihazlar**
  - **Azure AD ve Hibriya katılmış cihazlar**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker-sabit sürücü ayarları

- **BitLocker sabit sürücü ilkesi**  
  [BitLocker grup ilkesi ayarları](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Sabit sürücü kurtarma**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    BitLocker korumalı sabit veri sürücülerinin gerekli başlangıç anahtarı bilgileri yokluğunda nasıl kurtarıldığını denetleyin.

    - **Yapılandırılmadı** (*varsayılan*)-varsayılan kurtarma seçenekleri, VERI kurtarma aracısı (DRA) dahil olmak üzere desteklenir. Son Kullanıcı Kurtarma seçeneklerini belirtebilir ve kurtarma bilgileri Azure Active Directory için yedeklenmez.
    - **Yapılandır** – çeşitli sürücü kurtarma tekniklerini yapılandırmak için erişimi etkinleştirin.

    *Yapılandırmak* için ayarlandığında aşağıdaki ayarları kullanılabilir:

    - **Kurtarma anahtarının Kullanıcı tarafından oluşturulması**  
      - **Engellendi** (*varsayılan*)
      - **Gerekli**
      - **İzin verildi**

    - **BitLocker kurtarma paketini yapılandırma**
      - **Parola ve anahtar** (*varsayılan*)-yönetici ve kullanıcılar tarafından, korunan sürücülerin kilidini açmak için kullanılan BitLocker kurtarma parolasının yanı sıra, yöneticiler tarafından veri kurtarma amaçları için kullanılan kurtarma anahtar paketleri dahil olmak üzere Active Directory.
      - **Yalnızca parola** -kurtarma anahtar paketleri gerektiğinde erişilebilir olmayabilir.

    - **Cihazın kurtarma bilgilerini Azure AD 'ye yedeklemesini gerektir**
      - **Yapılandırılmadı** (*varsayılan*)-Azure AD 'ye kurtarma anahtarı yedeklemesi başarısız olsa bile, BitLocker etkinleştirmesi tamamlanır. Bu, hiçbir kurtarma bilgisinin dışarıdan depolanmayacak şekilde sonuçlanabilir.
      - **Evet** -kurtarma anahtarları Azure Active Directory başarılı bir şekilde kaydedilinceye kadar BitLocker etkinleştirme tamamlanmaz.

    - **Kurtarma parolasının Kullanıcı tarafından oluşturulması**  
      - **Engellendi** (*varsayılan*)
      - **Gerekli**
      - **İzin verildi**

    - **BitLocker kurulumu sırasında kurtarma seçeneklerini gizle**
      - **Yapılandırılmadı** (*varsayılan*)-kullanıcının ek kurtarma seçeneklerine erişmesine izin verin.
      - **Evet** -son kullanıcının BitLocker kurulum Sihirbazı sırasında kurtarma anahtarları yazdırma gibi ek kurtarma seçenekleri seçmelerini engelleyin.

    - **Kurtarma bilgilerinin depolanması için BitLocker 'ı etkinleştir**
      - **Yapılandırılmadı** (*varsayılan*)  
      - **Evet**

    - **Sertifika tabanlı veri kurtarma aracısı (DRA) kullanımını engelleyin**
      - Yapılandırılmadı (*varsayılan*)-DRA 'Nın **ayarlanmayana** kullanılmasına izin verin. DRA ayarlandığında, DRA aracısını ve sertifikalarını dağıtmak için bir Kurumsal PKI ve grup ilkesi nesneleri gerekir.
      - **Evet** -BitLocker özellikli sürücüleri kurtarmak Için veri kurtarma ARACıSı (DRA) kullanma özelliğini engelleyin.

  - **BitLocker tarafından korunmayan sabit veri sürücülerine yönelik yazma erişimini engelleyin**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Bu ayar *BitLocker sabit sürücü Ilkesi* *Yapılandır*olarak ayarlandığında kullanılabilir.

    - **Yapılandırılmadı** (*varsayılan*)-veriler, şifrelenmemiş sabit sürücülere yazılabilir.
    - **Evet** -Windows, BitLocker korumalı olmayan sabit sürücülere hiçbir verinin yazılmasına izin vermez. Sabit bir sürücü şifrelenmemişse, yazma erişimi verilmeden önce kullanıcının BitLocker kurulum Sihirbazı 'nı tamamlaması gerekir.

  - **Sabit veri sürücüleri için şifreleme yöntemini yapılandırma**  
    CSP: [Encryptionmethodbydrivetype](https://go.microsoft.com/fwlink/?linkid=872526)  

    Sabit veri sürücüleri diskleri için şifreleme yöntemini ve şifre gücünü yapılandırın. *XTS-AES 128-bit* , Windows varsayılan şifreleme yöntemidir ve önerilen değerdir.

    - **Yapılandırılmadı** (*varsayılan*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### <a name="bitlocker---os-drive-settings"></a>BitLocker-işletim sistemi sürücüsü ayarları

- **BitLocker sistem sürücüsü ilkesi**  
  CSP: [BitLocker Grup İlkesi ayarları](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Yapılandır** (*varsayılan*)  
  - **Yapılandırılmadı**

  *Yapılandırma* olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

  - **Başlangıç kimlik doğrulaması gerekiyor**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -GÜVENILIR Platform Modülü (TPM) veya başlangıç PIN gereksinimlerinin kullanımı da dahil olmak üzere sistem başlangıcında ek kimlik doğrulama gereksinimlerini yapılandırın.

    *Evet* olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

    - **Uyumlu TPM başlatması**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      BitLocker için TPM kullanılması önerilir. Bu ayar yalnızca BitLocker etkinleştirildikten sonra, BitLocker zaten etkinse geçerlidir.

      - **Engellenen** (*varsayılan*)-BitLocker TPM 'yi kullanmaz.
      - **Gerekli** -BITLOCKER yalnızca TPM varsa ve kullanılabilir olduğunda etkinleştirilir.
      - **Izin verilen** -BitLocker varsa TPM 'yi kullanır.

    - **Uyumlu TPM başlangıç PIN 'ı**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Engellendi** (*varsayılan*)-PIN kullanımını engelleyin.
      - **Gerekli** -BitLocker 'ı ETKINLEŞTIRMEK için PIN gerektır ve TPM var olmalıdır.
      - **Izin verilen** -BitLocker varsa TPM 'yi kullanır ve bir başlangıç PIN 'inin Kullanıcı tarafından yapılandırılmasına izin verir.

      Sessiz etkinleştirme senaryolarında bunu *engellenmiş*olarak ayarlamanız gerekir. Kullanıcı etkileşimi gerektiğinde sessiz etkinleştirme senaryoları (Autopilot dahil) başarılı olmayacaktır.

    - **Uyumlu TPM başlangıç anahtarı**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Engellendi** (*varsayılan*)-başlangıç anahtarlarının kullanımını engelleyin.
      - **Gerekli** -BitLocker 'ı etkinleştirmek için bir başlangıç anahtarı ve TPM 'nin mevcut olması gerekir.
      - **Izin verilen** -BitLocker varsa TPM 'yi kullanır ve sürücülerin kilidini açmak için bir başlangıç ANAHTARıNıN (USB sürücü gibi) mevcut olmasını sağlar.

      Sessiz etkinleştirme senaryolarında bunu *engellenmiş*olarak ayarlamanız gerekir. Kullanıcı etkileşimi gerektiğinde sessiz etkinleştirme senaryoları (Autopilot dahil) başarılı olmayacaktır.

    - **Uyumlu TPM başlangıç anahtarı ve PIN 'ı**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Engellendi** (*varsayılan*)-BIR başlangıç anahtarı ve PIN birleşiminin kullanımını engelleyin.
      - **Gerekli** -BitLocker 'ın, etkin hale gelmesi için bir başlangıç anahtarı ve PIN 'in mevcut olması gerekir.
      - **Izin verilen** -BitLocker varsa TPM 'yi kullanır ve bir başlangıç anahtarına izin verir) ve PIN birleşimini kullanır.

      Sessiz etkinleştirme senaryolarında bunu *engellenmiş*olarak ayarlamanız gerekir. Kullanıcı etkileşimi gerektiğinde sessiz etkinleştirme senaryoları (Autopilot dahil) başarılı olmayacaktır.

    - **TPM 'nin uyumsuz olduğu cihazlarda BitLocker 'ı devre dışı bırakma**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      TPM yoksa, BitLocker başlatma için bir parola veya USB sürücü gerektirir.

      Bu ayar yalnızca BitLocker etkinleştirildikten sonra, BitLocker zaten etkinse geçerlidir.

      - **Yapılandırılmadı** (*varsayılan*)
      - **Evet** -BitLocker 'ın uyumlu bir TPM yongası olmadan yapılandırılmasını engelleyin.

    - **Ön önyükleme kurtarma iletisini ve URL 'yi etkinleştir**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **Yapılandırılmadı** (*varsayılan*) – varsayılan BitLocker önyükleme öncesi kurtarma bilgilerini kullanın.
      - **Evet** – kullanıcılarınızın kurtarma parolalarını nasıl bulacağınızı anlamalarına yardımcı olmak için özel bir önyükleme öncesi kurtarma iletisi ve URL 'si yapılandırmasını etkinleştirin. Önyükleme öncesi ileti ve URL, kullanıcılar bılgısayar kurtarma modunda kilitlendiğinde kullanıcılar tarafından görülür.

      *Evet* olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

      - **Ön önyükleme kurtarma iletisi**  
        Özel önyükleme öncesi kurtarma iletisi belirtin.

      - **Ön önyükleme kurtarma URL 'si**  
        Özel önyükleme öncesi kurtarma URL 'SI belirtin.

    - **Sistem sürücüsü kurtarma**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Yapılandırılmadı** (*varsayılan*)  
      - **Yapılandır** -ek ayarların yapılandırmasını etkinleştirin.

      *Yapılandırmak* için ayarlandığında aşağıdaki ayarları kullanılabilir:

      - **Kurtarma anahtarının Kullanıcı tarafından oluşturulması**  
        - **Engellendi** (*varsayılan*)
        - **Gerekli**
        - **İzin verildi**

      - **BitLocker kurtarma paketini yapılandırma**
        - **Parola ve anahtar** (*varsayılan*)-yönetici ve kullanıcılar tarafından, korunan sürücülerin kilidini açmak için kullanılan BitLocker kurtarma parolasının yanı sıra, yöneticiler tarafından veri kurtarma amaçları için kullanılan kurtarma anahtar paketleri dahil olmak üzere Active Directory.
        - **Yalnızca parola** -kurtarma anahtar paketleri gerektiğinde erişilebilir olmayabilir.

      - **Cihazın kurtarma bilgilerini Azure AD 'ye yedeklemesini gerektir**
        - **Yapılandırılmadı** (*varsayılan*)-Azure AD 'ye kurtarma anahtarı yedeklemesi başarısız olsa bile, BitLocker etkinleştirmesi tamamlanır. Bu, hiçbir kurtarma bilgisinin dışarıdan depolanmayacak şekilde sonuçlanabilir.
        - **Evet** -kurtarma anahtarları Azure Active Directory başarılı bir şekilde kaydedilinceye kadar BitLocker etkinleştirme tamamlanmaz.

      - **Kurtarma parolasının Kullanıcı tarafından oluşturulması**  
        - **Engellendi** (*varsayılan*)
        - **Gerekli**
        - **İzin verildi**

      - **BitLocker kurulumu sırasında kurtarma seçeneklerini gizle**
        - **Yapılandırılmadı** (*varsayılan*)-kullanıcının ek kurtarma seçeneklerine erişmesine izin verin.
        - **Evet** -son kullanıcının BitLocker kurulum Sihirbazı sırasında kurtarma anahtarları yazdırma gibi ek kurtarma seçenekleri seçmelerini engelleyin.

      - **Kurtarma bilgilerinin depolanması için BitLocker 'ı etkinleştir**
        - **Yapılandırılmadı** (*varsayılan*)  
        - **Evet**

      - **Sertifika tabanlı veri kurtarma aracısı (DRA) kullanımını engelleyin**
        - Yapılandırılmadı (*varsayılan*)-DRA 'Nın **ayarlanmayana** kullanılmasına izin verin. DRA ayarlandığında, DRA aracısını ve sertifikalarını dağıtmak için bir Kurumsal PKI ve grup ilkesi nesneleri gerekir.
        - **Evet** -BitLocker özellikli sürücüleri kurtarmak Için veri kurtarma ARACıSı (DRA) kullanma özelliğini engelleyin.

    - **Minimum PIN uzunluğu**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      BitLocker etkinleştirmesi sırasında TPM + PIN gerekliyse en düşük başlangıç PIN uzunluğunu belirtin. PIN uzunluğu 4 ile 20 basamak arasında olmalıdır.

      Bu ayarı yapılandırmazsanız, kullanıcılar herhangi bir uzunlukta bir başlangıç PIN 'ı yapılandırabilir (4 ila 20 basamak arasında)

      Bu ayar yalnızca BitLocker etkinleştirildikten sonra, BitLocker zaten etkinse geçerlidir.

  - **Işletim sistemi sürücüleri için şifreleme yöntemini yapılandırma**  
   CSP: [Encryptionmethodbydrivetype]( https://go.microsoft.com/fwlink/?linkid=872526)

    İşletim sistemi sürücüleri için şifreleme yöntemini ve şifre gücünü yapılandırın. *XTS-AES 128-bit* , Windows varsayılan şifreleme yöntemidir ve önerilen değerdir.

    - **Yapılandırılmadı** (*varsayılan*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker-çıkarılabilir sürücü ayarları

- **Işletim sistemi sürücüleri için şifreleme yöntemini yapılandırma**  
  CSP: [BitLocker Grup İlkesi ayarları](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Yapılandırılmadı** (*varsayılan*)  
  - **Yapılandır**

  *Yapılandırma* olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz.

  - **Çıkarılabilir veri sürücüleri için şifreleme yöntemini yapılandırma**  
    CSP: [Encryptionmethodbydrivetype](https://go.microsoft.com/fwlink/?linkid=872526)

    Çıkarılabilir veri sürücüleri diskleri için istenen şifreleme yöntemini seçin.

    - **Yapılandırılmadı** (*varsayılan*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **BitLocker tarafından korunmayan çıkarılabilir veri sürücülerine yönelik yazma erişimini engelleyin**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Yapılandırılmadı** (*varsayılan*)-veriler, şifrelenmemiş çıkarılabilir sürücülere yazılabilir.
    - **Evet** -Windows, verilerin BitLocker korumalı olmayan çıkarılabilir sürücülere yazılmasına izin vermez. Takılan bir çıkarılabilir sürücü şifrelenmemişse, sürücüye yazma erişimi verilmeden önce Kullanıcı BitLocker kurulum Sihirbazı 'nı tamamlamalıdır.

    - **BitLocker tarafından korunmayan çıkarılabilir veri sürücülerine yönelik yazma erişimini engelleyin**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Yapılandırılmadı** (*varsayılan*)-BitLocker şifreli herhangi bir sürücü kullanılabilir.
      - **Evet** -kuruluşunuzun sahip olduğu bir bilgisayarda şifrelenmedikleri takdirde çıkarılabilir sürücülere erişimi engelleyin.

## <a name="next-steps"></a>Sonraki adımlar

[Disk şifrelemesi için uç nokta güvenlik ilkesi](../protect/endpoint-security-disk-encryption-policy.md)
