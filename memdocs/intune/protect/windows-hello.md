---
title: İş için Windows Hello ile Microsoft Intune tümleştirmesi
titleSuffix: Microsoft Intune
description: Cihaz kaydı sırasında yönetilen cihazlarda Iş için Windows Hello kullanımını denetlemeye yönelik bir ilke oluşturmayı öğrenin. "
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: d120ee0f55651ab1661e426e5889aaf8a4c7e670
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262872"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>İş için Windows Hello ile Microsoft Intune tümleştirmesi  

Iş için Windows Hello 'Yu (eski adıyla İş için Microsoft Passport), cihaz kaydı sırasında Microsoft Intune tümleştirebilirsiniz.

İş İçin Hello bir parolayı, akıllı kartı ya da sanal akıllı kartı değiştirmek için Active Directory veya bir Azure Active Directory hesabı kullanan alternatif bir oturum açma yöntemidir. Oturum açmak için parola yerine bir *kullanıcı hareketi* kullanmanıza imkan tanır. Kullanıcı hareketi bir PIN, Windows Hello gibi Biyometri kimlik doğrulaması veya parmak izi okuyucu gibi harici bir cihaz olabilir.

Intune, İş İçin Hello ile iki şekilde tümleşir:

- **Kiracı genelinde** (*Bu makale)*: bir Intune ilkesi, *cihaz kaydı*altında oluşturulabilir. Bu ilke, tüm kuruluşu hedefler (kiracı genelinde). Windows AutoPilot ilk çalıştırma deneyimini (OOBE) destekler ve bir cihaz kaydedildiğinde uygulanır.
- **Ayrık gruplar**: Intune 'a daha önce kaydolmuş cihazlar Için Windows Hello for Business için cihazları yapılandırmak üzere bir cihaz yapılandırma [**kimlik koruması**](../protect/identity-protection-configure.md) profili kullanın. Kimlik koruma profilleri atanan kullanıcıları veya cihazları hedefleyebilir ve iade sırasında uygulanabilir.

Ayrıca Intune, Iş için Windows Hello bazı ayarlarını yönetmek üzere aşağıdaki ilke türlerini destekler:

- [**Güvenlik temelleri**](../protect/security-baselines.md). Aşağıdaki taban çizgileri Iş için Windows Hello ayarlarını içerir:
  - [Microsoft Defender Gelişmiş tehdit koruması temel ayarları](../protect/security-baseline-settings-defender-atp.md#windows-hello-for-business)
  - [Windows MDM güvenlik taban çizgisi ayarları](../protect/security-baseline-settings-mdm-all.md#windows-hello-for-business)
- Uç nokta güvenlik [**hesabı koruma**](../protect/endpoint-security-account-protection-policy.md) ilkesi. [Hesap koruması ayarlarını](../protect/endpoint-security-account-protection-profile-settings.md#account-protection)görüntüleyin.

Bu makalenin geri kalanında, tüm kuruluşunuzu hedefleyen Iş için varsayılan bir Windows Hello ilkesi oluşturma konusu ele alınmaktadır.

> [!IMPORTANT]
> Yıldönümü Güncelleştirmesi’nden önceki Windows 10 masaüstü ve mobil sürümlerinde, kaynaklarda kimlik doğrulama için kullanılabilen iki farklı PIN ayarlayabilirsiniz:
>
> - **Cihaz PIN’i** cihazın kilidini açmak ve bulut kaynaklarına bağlanmak için kullanılabilir.
> - **Iş PIN 'i** , kullanıcının kişisel cihazlarında (KCG) Azure AD kaynaklarına erişmek için kullanıldı.
> 
> Yıldönümü Güncelleştirmesi’nde bu iki PIN, tek bir cihaz PIN’inde birleştirilmiştir.
> Cihaz PIN’ini denetlemek için ayarladığınız Intune yapılandırma ilkelerinin yanı sıra, yapılandırmış olduğunuz İş İçin Windows Hello ilkeleri de bu yeni PIN değerine ayarlanmıştır.
> PIN’i denetlemek için iki ilke türünü de ayarladıysanız, İş için Windows Hello ilkesi hem Windows 10 masaüstü cihazlara hem de Windows 10 mobil cihazlara uygulanır.
> İlke çakışmalarının çözümlendiğinden ve PIN ilkesinin düzgün şekilde uygulandığından emin olmak için, İş İçin Windows Hello İlkenizi yapılandırma ilkenizdeki ayarlarla eşleşecek şekilde güncelleştirin ve kullanıcılarınızdan cihazlarını Şifket Portalı uygulamasında eşitlemelerini isteyin.



## <a name="create-a-windows-hello-for-business-policy"></a>İş İçin Windows Hello ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazlar**  >   **kayıt**  >  **kaydetme cihazları**  >  **Windows kaydı**  >  **iş için Windows Hello**'ya gidin. Iş için Windows Hello bölmesi açılır.

3. **İş Için Windows Hello 'Yu yapılandırmak**için aşağıdaki seçenekler arasından seçim yapın:

     - **Etkin**. İş İçin Windows Hello ayarlarını yapılandırmak istiyorsanız bu ayarı seçin.  *Etkin*' i seçtiğinizde, Windows Hello için ek ayarlar görünür ve cihazlar için yapılandırılabilir.

    - **Devre dışı**. Cihaz kaydı sırasında Iş için Windows Hello 'Yu etkinleştirmek istemiyorsanız, bu seçeneği seçin. Devre dışı bırakıldığında, kullanıcılar, sağlama gerekebilecek mobil telefonlar Azure Active Directory dahil olmak üzere Iş için Windows Hello sağlayamaz. *Devre dışı*olarak ayarlandığında, bu ilke Iş Için Windows Hello 'yu Etkinleştiremese de Iş Için Windows Hello için sonraki ayarları yine de yapılandırabilirsiniz.

    - **Yapılandırılmadı**. Intune’un İş İçin Windows Hello ayarlarını denetlemesini istemiyorsanız bu ayarı seçin. Windows 10 cihazlarında mevcut Iş için Windows Hello ayarları değiştirilmez. Bölmedeki diğer ayarlardan hiçbiri kullanılamaz.

4. Önceki adımda **Etkin**’i seçtiyseniz, tüm kayıtlı Windows 10 ve Windows 10 Mobile cihazlarına uygulanacak olan gerekli ayarları yapılandırın. Bu ayarları yapılandırdıktan sonra **Kaydet**' i seçin.

   - **Güvenilir Platform Modülü (TPM) kullanın**:

     TPM yongası ek bir veri güvenliği katmanı sağlar. Aşağıdaki değerlerden birini seçin:

     - **Gerekli** (varsayılan). Yalnızca erişilebilir bir TPM’si olan cihazlar İş İçin Windows Hello sağlayabilir.
     - **Tercih edilen**. Cihazlar ilk olarak bir TPM kullanmayı dener. Bu seçenek kullanılamıyorsa, yazılım şifrelemesini kullanabilirler.

   - **MINIMUM PIN uzunluğu** ve **Maksimum PIN uzunluğu**:

     Cihazları, güvenli oturum açma için sizin belirttiğiniz minimum ve maksimum PIN uzunluklarını kullanacak şekilde yapılandırır. Varsayılan PIN uzunluğu altı karakterdir, ancak minimum dört karakterlik bir uzunluğu zorunlu tutabilirsiniz. Maksimum PIN uzunluğu 127 karakterdir.

   - PIN 'de **küçük harfler**, PIN **kodunda büyük harfler**ve **özel karakterler PIN**kodunda.

     PIN’de büyük harf, küçük harf ve özel karakter kullanımını gerekli kılarak daha güçlü PIN zorunluluğu getirebilirsiniz. Her bir için şunları seçin:

     - **Izin verildi**. Kullanıcılar PIN kodlarında karakter türünü kullanabilir, ancak bu zorunlu değildir.

     - **Gerekli**. Kullanıcılar PIN kodlarında karakter türlerinden en az birini bulundurmalıdır. Örneğin, en az bir büyük harfin ve bir özel karakterin zorunlu kılınması yaygın bir uygulamadır.

     - **İzin verilmiyor** (varsayılan). Kullanıcılar PIN’de bu karakter türlerini kullanmamalıdır. (Ayar yapılandırılmazsa, bu davranış da budur.)

       Özel karakterler şunlardır: **! "# $% &amp; ' () &#42; +,-. / : ; &lt; = &gt; ? @ [\] ^ _ &#96; {&#124;} ~**

   - **PIN süre sonu (gün)**:

     Son kullanıcıların belirli bir süre sonunda PIN’i değiştirmesini zorunlu tutmak için bir PIN kullanım süresi belirtmek iyi bir uygulamadır. Varsayılan değer 41 gündür.

   - **PIN geçmişini anımsa**:

     Daha önce kullanılan PIN'lerin yeniden kullanılmasını kısıtlar. Varsayılan olarak, son 5 PIN yeniden kullanılabilir.

   - **Biyometrik kimlik doğrulamasına Izin ver**:

     İş İçin Windows Hello için bir PIN koduna alternatif olarak yüz tanıma veya parmak izi gibi biyometrik kimlik doğrulamasını etkinleştirir. Biyometrik kimlik doğrulaması başarısız olsa bile kullanıcılar bir iş PIN kodu yapılandırmalıdır. Aşağıdakilerden birini seçin:

     - **Evet**. İş İçin Windows Hello biyometrik kimlik doğrulamasına izin verir.
     - **Hayır**. İş İçin Windows Hello, (tüm hesap türleri için) biyometrik kimlik doğrulamasını engeller.

   - **Kullanılabilir olduğunda, Gelişmiş kimlik sahtekarlığına karşı koruma kullan**:

     Windows Hello 'nun, kimlik sahtekarlığına karşı koruma özelliklerinin bunu destekleyen cihazlarda kullanılıp kullanılmayacağını yapılandırır. Örneğin, gerçek bir yüz yerine yüzün fotoğrafını algılama.

     **Evet**olarak ayarlandığında, Windows, desteklendiğinde yüz özellikleri için tüm kullanıcıların yanıltma koruması kullanmasını gerektirir.

   - **Telefonla oturum açmaya Izin ver**:

     Bu seçenek **Evet** olarak ayarlanırsa, kullanıcılar masaüstü bilgisayar kimlik doğrulaması için bir taşınabilir özel cihaz olarak hizmet verecek bir uzak passport kullanabilir. Masaüstü bilgisayarı Azure Active Directory’e katılmış olmalıdır ve özel cihaz bir İş İçin Windows Hello PIN kodu ile yapılandırılmalıdır.

## <a name="windows-holographic-for-business-support"></a>Windows 10 Holographic for Business desteği

Windows holographic for Business, Iş için Windows Hello için aşağıdaki ayarları destekler:

- Güvenilir Platform Modülü (TPM) kullanma
- Minimum PIN uzunluğu
- Maksimum PIN uzunluğu
- PIN kodunda küçük harfler
- PIN kodunda büyük harfler
- PIN kodunda özel karakterler
- PIN süre zaman aşımı (gün)
- PIN geçmişini anımsa

## <a name="next-steps"></a>Sonraki adımlar

Iş için Windows Hello hakkında daha fazla bilgi için Windows 10 belgelerindeki [kılavuza](https://technet.microsoft.com/library/mt589441.aspx) bakın.
